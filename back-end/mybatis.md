# MyBatis 사용하기

AXBoot에는 다음과 같이 MyBatis 설정이 구성되어. MyBatis 사용을 원하시면 매퍼 XML과 인터페이스만 생성하시면 됩니다.

```java
@Bean
public SqlSessionFactory sqlSessionFactory(SpringManagedTransactionFactory springManagedTransactionFactory, DataSource dataSource) throws Exception {
    SqlSessionFactoryBean sqlSessionFactoryBean = new SqlSessionFactoryBean();
    sqlSessionFactoryBean.setDataSource(dataSource);
    sqlSessionFactoryBean.setTypeAliasesPackage(GlobalConstants.CORE_DOMAIN_PACKAGE);
    sqlSessionFactoryBean.setTransactionFactory(springManagedTransactionFactory);

    Properties properties = new Properties();
    properties.put("mapUnderscoreToCamelCase", true);
    sqlSessionFactoryBean.setConfigurationProperties(properties);
    return sqlSessionFactoryBean.getObject();
}

@Bean
public MapperScannerConfigurer mapperScannerConfigurer() throws Exception {
    MapperScannerConfigurer mapperScannerConfigurer = new MapperScannerConfigurer();
    mapperScannerConfigurer.setBasePackage(GlobalConstants.CORE_DOMAIN_PACKAGE);
    mapperScannerConfigurer.setMarkerInterface(MyBatisMapper.class);
    mapperScannerConfigurer.setSqlSessionFactoryBeanName("sqlSessionFactory");
    return mapperScannerConfigurer;
}
```

### 1. MyBatis Interface 생성하기
```java
import com.chequer.axboot.core.mybatis.MyBatisMapper;

public interface UserMapper extends MyBatisMapper {
    
    List<User> findAll();
    ...
}
```
>AXBoot Core에서 제공되는 MyBatisMapper 인터페이스를 상속받으면 이미 구성된 MapperScan이 해당 매퍼를 스프링 빈으로 자동 등록합니다. 

### 2. MyBatis XML 생성하기
```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<mapper namespace="com.chequer.axboot.user.UserMapper">

    <select id="findAll" parameterType="hashmap" resultType="user">
        
		...
		
    </select>
</mapper>
```
>namespace에 패키지를 포함한 매퍼 인터페이스 이름을 입력합니다. **XML 파일의 위치는 resources 하위에 위치하며 인터페이스 파일과 패키지가 동일하게 구성되어야 합니다.**

예) src/java/com/chequer/axboot/user/UserMapper.java 파일을 생성하였다면, XML 파일은 src/resources/com/chequer/axboot/user/UserMapper.xml 에 위치하여야 합니다.

### 3. MyBatis Mapper 사용하기
```java

public void UserService {

    @Inject
    private UserMapper userMapper;

    public List<User> findAll() {
        return userMapper.findAll();
    }

    ...
}
```
>UserMapper를 스프링 빈처럼 사용하면 됩니다.