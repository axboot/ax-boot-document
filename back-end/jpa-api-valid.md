# @Valid 애너테이션을 컬렉션 타입 @RequestBody에 사용하기

Spring Controller @RequestBody에 @Valid를 사용할경우, 단일 Object 타입일 때는 Validator가 잘 동작하지만, Collection 타입으로 감싸져 있을 경우에는 Validator가 동작을 하지 못했습니다. 원인을 찾아보기 위해 디버깅으로 클래스들을 추적해보니..

RequestResponseBodyMethodProcessor -> AbstractMessageConverterMethodArgumentResolver -> DataBinder (validate)로 이어지는데, AbstractMessageConverterMethodArgumentResolver의 validateIfApplicable에서 @Valid 애너테이션이 있는지 확인을 한 후, 애너테이션이 있을 경우 DataBinder의 validate를 호출하여 유효성 검사를 하게되더군요.

```java
protected void validateIfApplicable(WebDataBinder binder, MethodParameter methodParam) {
	Annotation[] annotations = methodParam.getParameterAnnotations();
	for (Annotation ann : annotations) {
		Validated validatedAnn = AnnotationUtils.getAnnotation(ann, Validated.class);
		if (validatedAnn != null || ann.annotationType().getSimpleName().startsWith("Valid")) {
			Object hints = (validatedAnn != null ? validatedAnn.value() : AnnotationUtils.getValue(ann));
			Object[] validationHints = (hints instanceof Object[] ? (Object[]) hints : new Object[] {hints});
			binder.validate(validationHints);
			break;
		}
	}
}
```

DataBinder의 validate를 살펴보면, JSR303 구현체 (targetValidator)의 validate를 호출하도록 되어있고, 유효성 검사 결과를 기반으로 유효성이 위반된 내역이 있을경우 에러 메시지를 처리출력 위해 processConstraintViolations 메서드를 호출하게 됩니다.

```java
@Override
public void validate(Object target, Errors errors, Object... validationHints) {
	if (this.targetValidator != null) {
		Set<Class<?>> groups = new LinkedHashSet<Class<?>>();
		if (validationHints != null) {
			for (Object hint : validationHints) {
				if (hint instanceof Class) {
					groups.add((Class<?>) hint);
				}
			}
		}
		processConstraintViolations(this.targetValidator.validate(target, groups.toArray(new Class<?>[groups.size()])), errors);
	}
}
```

HibernateValidator를 사용할 경우, ValidatorImpl 클래스의 validate가 호출되는데, BeanMetaDataManager를 통해 해당 클래스가 Validator에서 검사를 할 수 있는 클래스인지를 확인합니다.

```java
@Override
public final <T> Set<ConstraintViolation<T>> validate(T object, Class<?>... groups) {
	Contracts.assertNotNull( object, MESSAGES.validatedObjectMustNotBeNull() );
 
	if ( !beanMetaDataManager.isConstrained( object.getClass() ) ) {
		return Collections.emptySet();
	}
 
	ValidationOrder validationOrder = determineGroupValidationOrder( groups );
	ValidationContext<T> validationContext = getValidationContext().forValidate( object );
 
	ValueContext<?, Object> valueContext = ValueContext.getLocalExecutionContext(
			object,
			beanMetaDataManager.getBeanMetaData( object.getClass() ),
			PathImpl.createRootPath()
	);
 
	return validateInContext( valueContext, validationContext, validationOrder );
}
```

바로 이부분에서 Collection 타입이 isConstrained를 통과하지 못하면서, 결국 유효성 검사는 Collections.emptySet()만 반환하고 끝나게 되는데요, JSR 303은 Bean Validation에 대한 명세인데, 아마도 Collection이 JavaBeans 명세에 포함되지 않아서 그런게 아닐까 싶습니다. 하지만 JSR303 Bean Validation 스펙을 읽다보니 3.1.3에 해당 빈이 Iterable을 구현하고 있으면, 재귀적으로 유효성 검사를 한다고 되어 있네요. 즉, Controller에 다음과 같이 한번더 감싸진 형태의 DTO를 RequestBody로 받고, 해당 DTO에서 Collection타입으로 선언하면 유효성 검사가 가능할 것 같습니다.

```java
@RequestMapping(method = {RequestMethod.PUT}, produces = APPLICATION_JSON)
public ApiResponse save(@Valid @NotNull @RequestBody public ApiResponse save(@Valid @NotNull @RequestBody RequestDTO request) {
    basicCodeService.saveCommonCode(request.getList());
    return ok();
}
```

```java
public class RequestDTO {
    
    @Valid
    private List<?> list;
 
    public List<?> getList() {
        return list;
    }
 
    public void setList(List<?> list) {
        this.list = list;
    }
}
```

하지만, 위와 같은 방식으로 변경할경우, [{}] 형태로 JSON 요청을 { “list”: [] } 형태로 모두 변경해야하기때문에, 기존에 서비스중인 API가 있을 경우에는 변경하기가 쉽지 않을 수 있을것 같습니다.

이제 내부 동작을 알았으니, 약간의 꼼수로 API 구조 변경없이 Collection 타입에 포함된 객체 유효성 검사를 해보시죠!

컨트롤러는 기존과 그대로 유지하고, CollectionValidator라는 클래스를 생성합니다.

```java
@RequestMapping(method = {RequestMethod.PUT}, produces = APPLICATION_JSON)
public ApiResponse save(@Valid @NotNull @RequestBody List<CommonCode> basicCodes) {
    basicCodeService.saveCommonCode(basicCodes);
    return ok();
}
```

```java
public class CollectionValidator implements Validator {
 
    private final Validator validator;
 
    public CollectionValidator(LocalValidatorFactoryBean validatorFactory) {
        this.validator = validatorFactory;
    }
 
    @Override
    public boolean supports(Class<?> clazz) {
        return true;
    }
 
    @Override
    public void validate(Object target, Errors errors) {
        if (target instanceof List) {
            Collection collection = (Collection) target;
            for (Object object : collection) {
                ValidationUtils.invokeValidator(validator, object, errors);
            }
        }
    }
}
```
supports는 모두 true로 반환하도록 합니다. 이는 컨트롤러에서 Validator가 해당 컨트롤러와 동작하는데 적합한지를 검사하는데, false가 반환될 경우, 컨트롤러가 동작에 아무런 문제가 없는데도 불구하고 예외를 발생을 시키더라고요.

validate 로직은 간단합니다. 컬렉션 타입인지를 검사한 후, 컬렉션 타입이면 컬렉션 객체들을 하나씩 꺼내서 유효성 검사를 합니다~

이제, 해당 Validator가 Collection 타입의 @RequestBody에 모두 적용될 수 있도록, ControllerAdvice를 생성하고 Validator로 추가하면 됩니다.

```java
@ControllerAdvice
public class BaseController {
 
    @Inject
    protected LocalValidatorFactoryBean validator;
 
    @InitBinder
    public void initBinder(WebDataBinder binder) {
        binder.addValidators(new CollectionValidator(validator));
    }
	...
}
```
LocalValidatorFactoryBean이 없다고 에러가 나면, 빈을 생성해 줍니다.

```java
@Bean
public LocalValidatorFactoryBean validatorFactoryBean() {
    return new LocalValidatorFactoryBean();
}
```

> 원문참조 : http://brantiffy.axisj.com/archives/641