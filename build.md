# 빌드 및 배포

> AXBoot는 빌드 관리자로 Maven을 사용합니다. Maven Package 골을 사용하여 WAR 파일을 생성할 수 있습니다.

- 터미널에서는 `mvn package` 명령을 사용하면 됩니다.
- Eclipse에서는 pom.xml에서 우측 마우스 클릭 -> Maven Build -> Goal에 package를 입력 후 Build 버튼을 클릭합니다.
- IntelliJ에서는 우측 Maven Projects 패널에서 Lifecycle -> package를 더블클릭 합니다.
- 생성된 WAR 파일은 target/{프로젝트명}/{artifcatId}-{version}.war 파일로 생성됩니다.