# AXBoot
### Full Stack Java Web Development Framework

1950년, 컴퓨터 개발과 더불어 시작된 인터넷의 역사는 군사목적으로 사용되었던 아파넷을 기반으로 인터네트워킹으로 발전했고, 현대의 인터넷(웹) 시대가 열렸습니다. 단순한 정적 페이지에 불과했던 초기 웹은 CGI와, 서블렛 등의 등장으로 빠르게 동적 기반의 새로운 애플리케이션 영역으로 자리잡았고, 최근 HTML5의 등장과, Javascript의 재조명을 받으며 더욱 빠른 속도로 영역을 확장하고 있습니다. 

웹 애플리케이션은 사용자가 인터랙션하는 프런트엔드 영역과, 사용자가 요청한 데이터를 저장,수정,삭제 하는 백엔드영역으로 크게 나누어 볼 수 있습니다. 하지만 현대의 웹 애플리케이션은 단순한 인터랙션을 넘어서 빠르고 편리한 UI/UX 프런트엔드 기술과 수천만, 수억의 데이터를 빠르고 효율적으로 관리할 수 있는 백엔드기술이 더욱 중요해졌습니다. Facebook, Google, Twitter 등 수많은 세계적 기업들이 웹 기술을 이끌면서 매일 새로운 기술들이 넘쳐나고 있지만, 정작 이 기술들을 한데 모아 쉽고 빠르게 웹 애플리케이션을 만들 수 있는 풀 스택 애플리케이션 프레임워크는 아직 존재하지 않습니다.

AXBoot는 HTML5와 순수 자바스크립트 기술로 개발된 AX5UI와, 한국에서 가장 선호하는 자바, 스프링 에코시스템을 기반으로 누구나 쉽고 빠르게 웹 애플리케이션을 개발할 수 있도록 만들어진 풀 스택 프레임워크 입니다. 

AXBoot Initializr를 통해 베이스 코드를 내려받고, IDE에서 소스코드를 임포트하고, 서버를 실행하는 데까지 채 5분이 걸리지 않으며, 미리 구성된 프레임워크 설정과 UI 컴포넌트, 레이아웃 시스템 덕분에, 샘플 예제를 기반으로 즉시 개발을 시작할 수 있습니다. 

또한 로그인, 로그아웃, 세션관리, 사용자관리, 권한관리 등 웹 애플리케이션 개발에 항상 반복적인 부분을 확장가능한 형태로 미리 제공하며 역공학 모델 추출기능과 로깅, 슬로우 쿼리 감지 등 웹 애플리케이션 개발, 운영에 필요한 다양한 기능들을 함께 제공합니다. 


[AXBoot Demonstration](http://demo.axboot.com)
> AXBoot Demonstration Site

[AXBoot Initializr](http://start.axboot.com)
> AXBoot Project Initializr (like Spring Initializr)

[AXBoot Documentation](http://api.axboot.com)
> AXBoot Documentation (now, Korean only)

[AXBoot UI Framework](http://ax5.io)
> AXBoot UI Framework Documentation (now, English only)

[AXBoot User Group](https://www.facebook.com/groups/axboot/)
> AXBoot Facebook User Group (Q&A or Communication)




## AXBoot 탄생 배경
앞서 이야기한것처럼, 웹 애플리케이션 개발에는 다양한 기술이 사용됩니다. 최근에는 더 급격한 속도로 웹 기술이 발전되고 있으며, 
아름답고 편리한 UI/UX를 위한 프런트엔드 기술과, 대용량 데이터, 분산처리를 효율적으로 하기위한 백엔드 기술들이 더욱 중요시되고 있고, 
각 기술들은 점점 세분화되어 전문성을 요구하고 있습니다. 

---

- 그림1) 프런트엔드 스펙트럼

![spectrum.png](https://raw.githubusercontent.com/axboot/ax-boot-document/master/assets/3294546972B83DFE881C853B483E6654.png)
출처 : https://www.frontendhandbook.com

---

- 그림2) 프런트엔드 기술 트렌드

![front-end-skills.png](https://raw.githubusercontent.com/axboot/ax-boot-document/master/assets/AFD4014AAED1F0B167C8430973368CFF.png)
출처 : https://www.frontendhandbook.com

---

- 그림3) 백엔드 영역 프레임워크 점유율

![report-screen-min.png](https://raw.githubusercontent.com/axboot/ax-boot-document/master/assets/48E65A5F9D62235452EDF4FECA47C296.png)
출처 : https://zeroturnaround.com/


---

- 그림4) JVM 기반 언어 점유율  

![TnT-2016-podium-jvm-languages-v1.jpg](https://raw.githubusercontent.com/axboot/ax-boot-document/master/assets/4986752B3DAE5A4DC47A3F812CC0FC99.png)
출처 : https://zeroturnaround.com/

---

- 그림5) 백엔드 기술 도구

![Screen Shot 2016-09-18 at 3.50.40 PM.png](https://raw.githubusercontent.com/axboot/ax-boot-document/master/assets/2C9D46174B758B88F24C9A4FBC83D010.png)
출처 : https://zeroturnaround.com/

이처럼 현대의 웹 애플리케이션은 수가지~수십가지의 기술들과 도구를 조합하여 개발하게 되며, 
개발이 완료된 애플리케이션을 배포하여 운영 할 때에는 더 많은 기술과 도구가 필요합니다. 

더 많은 개발자들이 뛰어난 UI와 안정성을 가진 웹 애플리케이션 개발을 할 수 있도록 지원하고, 
대한민국 웹 애플리케이션 생태계를 바꾸어보고자 AXBoot팀은 다년간의 웹 애플리케이션 노하우와 수십가지의 오픈소스, 
자체개발한 Web UI Framework를 하나로 묶어 풀 스택 웹 애플리케이션 프레임워크를 개발했습니다.
 
**AXBoot를 사용하면 Java, Spring, HTML5 기반의 웹 애플리케이션을 쉽고 빠르게 개발할 수 있으며, 
확장성과 유지보수성, 안정성이 뛰어난 웹 애플리케이션을 운영할 수 있습니다.**

---

# AXBoot 특징 및 장점

- AXBoot는 자체개발한 UI Framework와 Spring Framework, 수십개의 오픈소스 컴포넌트들로 이루어진 풀 스택 웹 애플리케이션 개발 프레임워크 입니다. 또한 사용자관리, 시스템 메뉴, 권한 관리, 세션관리 등 이미 구현된 어드민 팩을 기반으로 즉시 사용가능한 관리 시스템(어드민)을 개발할 수 있습니다. 또한 HTML5, CSS3, JavaScript, Java8, Spring Framework, Maven 등의 표준화된 기술과 널리 사용되는 오픈소스를 기반으로 개발하였기 때문에 기존 웹 애플리케이션 개발자들에게 친숙하고 편리한 프레임워크로 느껴집니다.

- 운영시 발생하는 여러가지 에러들을 사용자 정보와 파라미터, 로그들과 함께 추적하고, 실시간으로 알람을 제공하는 로그 시스템이 내장되어 있어, 중(소) 규모의 애플리케이션 운영시에는 별도의 로그 수집, 관리, 모니터링 시스템 없이도 안정적으로 운영할 수 있습니다.

- Dialog, Toast, Modal, Calendar, Picker, Formatter, Menu, Selector, Combobox, Grid 등 17여가지의 웹 컴포넌트를 제공하고 있으며 해당 컴포넌트들은 CSS(SCSS)를 통해 룩앤필(Look&Feel)을 손쉽게 제어할 수 있습니다.

- 자바 기반 웹 애플리케이션 개발자들이 익숙한 JSP를 템플릿 엔진으로 사용했고, UI 컴포넌트를 JSP 내에서 쉽고 편리하게 사용할 수 있는 JSTL 확장 태그를 제공합니다.

- Multiline SQL, SQL Mapper, ORM 등 다양한 방식으로 데이터를 영속화 할 수 있으며, 기존 생성된 테이블은 역공학을 통해 Controller, Service, Entity, Repository를 자동으로 생성해주는 스키마 추출 도구를 제공합니다.
