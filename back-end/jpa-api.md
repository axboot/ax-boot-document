# ModelExtractor를 사용하여 역공학으로 AXBoot 클래스 생성하기

1. 클래스를 만들 대상 테이블이 아직 없다면, 새로운 테이블을 생성합니다.
![CAPTURE 12.png](../assets/5EF573759B28AB16CDFE7136A53BAE7D.png)

2. http://{host}:{port}/modelExtractor/db 접속하여 클래스를 생성할 테이블을 선택합니다. 
예제에서는 TUTORIAL이라는 테이블을 신규로 생성했습니다. 
![CAPTURE 13.png](../assets/585555EB4B2D799F877B702EC027FFBC.png)
해당 테이블명을 선택하면 AXBoot에서 바로 사용할 수 있는 클래스가 새창에서 생성됩니다.
![CAPTURE 4.png](../assets/768CC5B1F703E8C6DACD1C6F491CFAB3.png)
데스크탑 output 폴더에도 코드가 자동으로 생성됩니다
![CAPTURE 5.png](../assets/9E9157F5E98B1EDC5C9F2E6F8422481E.png)

3. `Tutorial.java, TutorialRepository.java, TutorialService.java` 3개의 클래스파일을 `ax-boot-admin/src/main/java/com/chequer/axboot/admin/domain` 도메인 패키지 하위에 새로운 패키지를 생성후 (예제에서는 tutorial 로 생성했습니다) 붙여넣기 합니다
![CAPTURE 7.png](../assets/916E70C99945F78CCB09115FA89E3FA6.png)

4. `TutorialController.java` 컨트롤러 클래스를 `ax-boot-admin/src/main/java/com/chequer/axboot/admin/controllers` 컨트롤러 패키지에 붙여넣기 합니다. ![CAPTURE 8.png](../assets/F208CF319FC14F18DD399C216CFA3E3A.png) 컨트롤러 클래스를 열고 서비스와 엔티티를 임포트 합니다.
5. 도메인 패키지가 포함된 프로젝트에서 Maven Clean 골과 Compile골을 한번씩 실행합니다.
6. 톰캣을 재시작합니다.

7. http://localhost:8080/swagger/index.html 에서 API를 테스트 해봅니다. ![CAPTURE 10.png](../assets/009C3A25C931FA686776DD5AA2FD0F28.png) `Try it out`버튼을 클릭하면 GET API 결과를 미리볼 수 있습니다. ![CAPTURE 11.png](../assets/DF5D8A107C9D53555530C85E48FEEB58.png) 
8. [PUT] /api/v1/tutorials에 다음과 같은 JSON을 입력하고 `Try it out` 버튼을 클릭하면 PUT 테스트를 진행할 수 있습니다.
```json
{
  "testKey": "TEST",
  "testName": "TEST NAME",
  "testDesc": "....."
}
```
9. 이후 GET API를 호출하면 다음과 같이 저장한 데이터를 GET API를 통해 확인할 수 있습니다.
```json
{
  "page": {
    "totalPages": 0,
    "totalElements": 0,
    "currentPage": 0,
    "pageSize": 0
  },
  "list": [
    {
      "id": 7,
      "testKey": "TEST",
      "testName": "TEST NAME",
      "testDesc": ".....",
      "dataStatus": "ORIGIN",
      "__deleted__": false,
      "__created__": false,
      "__modified__": false
    }
  ]
}
```



