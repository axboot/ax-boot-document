# 설치 및 실행방법
## 준비

1. Java : http://www.oracle.com/technetwork/java/javase/downloads/index.html에 방문하여 Oracle JDK 1.8.0 이상을 설치합니다.
2. Tomcat : http://tomcat.apache.org 에 방문하여 Tomcat 7.0 버전 이상을 설치합니다.
3. Eclipse : IDE로 Eclipse를 사용할 경우, http://www.eclipse.org에 방문하여 Luna 이상의 버전(최신버전 권장)을 설치합니다.
4. STS(Spring Tool Suite) : IDE로 STS를 사용할 경우 https://spring.io/tools에 방문하여 3.7.0 이상 (최신버전 권장)을 설치합니다.
5. IntelliJ IDEA :IDE로 IntelliJ를 사용할 경우 12버전 이상의 Ultimate 버전 (최신버전 권장)을 설치합니다.
6. Git : https://git-scm.com에 방문하여 Git을 설치합니다.
7. Lombok : Eclipse를 사용할 경우 https://projectlombok.org에 방문하여 lombok.jar를 통해 Eclipse에 Lombok 플러그인을 설치합니다. IntelliJ를 사용할 경우 Lombok Plugin을 설치합니다.

## 소스코드 내려받기
1. AXBoot Github에 접속합니다. https://github.com/axboot/ax-boot-framework 
2. Clone or Download 버튼을 클릭한 후 해당 주소를 복사합니다.
3. Git 명령줄에서 다음과 같이 명령어를 입력하여 소스코드를 복사합니다.


```
$ git clone https://github.com/axboot/ax-boot-framework 
```
   
## 소스코드 열기 (Eclipse / STS)
1. File -> Import -> Maven -> Existing Maven Projects를 선택합니다.
2. Git을 통해 내려받은 소스코드 디렉토리를 선택하고 Finish 버턴을 클릭합니다.

## 소스코드 열기 (IntelliJ IDEA)
1. 시작화면에서 Open을 선택하고 Git을 통해 내려받은 AXBoot 소스코드를 선택합니다.

## 실행하기 (Eclipse / STS)
1. File -> New -> Other -> Server -> Server를 선택 후 Next 버튼을 클릭합니다.
2. Apache -> Tomcat (설치한 버전)을 선택합니다.
3. 톰캣이 설치된 디렉토리와 JRE를 선택하고 Finish를 클릭합니다.
4. Navigator에 있는 ax-boot-admin 프로젝트에서 마우스 우측버튼을 클릭한 후 Properties를 클릭합니다
5. Web Project Settings를 선택 후 Context root에 /를 입력 후 OK를 클릭합니다.
6. Servers 탭에 추가한 서버를 더블클릭 한 후, Modules 탭으로 이동합니다.
7. Add Web Module 버튼을 클릭 한 후 다음과 같은 화면이 나온면 OK를 클릭합니다.
8. 서버에서 마우스 우측 버튼을 클릭한 후 서버를 시작합니다.