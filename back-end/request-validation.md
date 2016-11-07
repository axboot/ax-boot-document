# @Valid 애너테이션을 통해 요청 데이터 검증하기

#### 1. PUT 요청을 처리하는 컨트롤러 메서드 매개변수 @RequestBody 앞에 @Valid 애너테이션을 추가합니다
```java
... 

public Model save(@Valid @RequestBody Model request) {
    service.saveProcess(request);
    return request;
}

...
```

---

#### 2. Entity 클래스 (혹은 VO 클래스)에 검증 애너테이션을 추가합니다
```java
@NotNull(message = "이름을 입력하세요.")
private String name;
```
- 사용 가능한 애너테이션 목록

![VALID_ANNOTATION.png](https://raw.githubusercontent.com/axboot/ax-boot-document/master/assets/VALID_ANNOTATION.png)

>더 자세한 정보는 JSR-303과 Hibernate Validator문서를 참고하세요. - [JSR-303](https://jcp.org/en/jsr/detail?id=303) / [HibernateValidator](http://hibernate.org/validator/)]
---

#### 3. 예외 발생시 JSON으로 응답을 자동으로 생성해줍니다.
```java
@ExceptionHandler({MethodArgumentNotValidException.class})
public Object processValidationError(MethodArgumentNotValidException ex) {
    FieldError fieldError = (FieldError)ex.getBindingResult().getFieldErrors().get(0);
    ApiResponse error = ApiResponse.error(ApiStatus.SYSTEM_ERROR, fieldError.getDefaultMessage());
    error.getError().setRequiredKey(fieldError.getField());
    return error;
}
```
>BaseController 클래스에서 유효성 검사 시 에러가 발생하면 해당되는 필드의 에러메시지를 가져와 출력합니다.