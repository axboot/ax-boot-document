# 개발환경

![env.jpg](https://raw.githubusercontent.com/axboot/ax-boot-document/master/assets/DD33823FBF7DACE5BA716AA0BC475698.jpg)

- Browser
    - Internet Explorer : 9 버전 이상
    - Google Chrome : 32.0.1700 이상
    - Opera : Opera 2014 이상
    - Safari : Safari 7 이상
    - Firefox : 32.0 버전 이상

- Web Server
    - 웹 서버는 AXBoot로 개발한 애플리케이션을 운영시에 부가적으로 필요한 Proxy, Load Balancer의 역할로 버전에 대한 제한이 없습니다.
    
- Web Application Server
    - Servlet 3.0 스펙을 준수하는 WAS라면 사용가능합니다.
    - Tomcat 7.x 이상
    - JBoss EAP 7 이상
    - Wildfly 8 이상
    - WebLogic 12c 이상
    - WebSphere 8 이상
    - JEUS 7 이상

- Database
    - 데이터베이스에 대한 별도의 제한은 없습니다. 기본적으로 H2 데이터베이스를 내장하고 있으며, 개발 및 테스트 용도로 H2를 사용할 수 있습니다. 구현하고자 하는 시스템에 맞는 데이터베이스 종류 및 버전을 사용하면 됩니다.

- Java
     JDK 1.8.0 이상