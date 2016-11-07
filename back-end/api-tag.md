# API Tag

AJAX API를 페이지가 호출 되는 시점에 '동기'로 API를 호출하고 싶을 경우, API 태그를 사용할 수 있습니다.
`GET`메서드로 사용되는 API들는 다음 `<ax:api>` 태그를 사용하면, 간단한 형태로 JSON 혹은 Request Scope Variable로 데이터를 전달받을 수 있습니다

### Parameter
- url : API URL (scheme, port를 제외한 Path와 QueryString 부분만 기술)
>예) /api/v1/users
- key :  해당 JSON or Object가 저장될 키
>예) "test"로 지정한경우, JavaScript에서는 다음과 같이 사용가능
```js
var testJson = (function(s){return s})(${test});
```
- type : API 요청 결과를 JSON으로 받을지, JSTL에서 사용할 수 있는 JavaObject로 받을지를 결정.
>(사용할 수 있는 값 : json or object, 기본값 : json)

---
### API 요청후 JavaScript에서 JSON으로 사용하기
```html
<ax:api url="/api/v1/basicCodes/name" key="basicCodes" type="json"/>
혹은(기본값이 JSON이라 json은 생략가능)
<ax:api url="/api/v1/basicCodes/name" key="basicCodes"/>

<jsp:attribute name="script">
    <script type="text/javascript">
        var basicCodes = (function(s){return s})(${basicCodes});
        console.log(basicCodes.list);
    </script>
</jsp:attribute>
```

---
### API 요청후 JSTL에서 사용하기 
```html
<ax:api url="/api/v1/basicCodes/name" key="basicCodes" type="object"/>

<c:forEach var="basicCode" items="${basicCodes.list}">
    <c:out value="${basicCode.basicCd}"/> <br/>
</c:forEach>
```

api 태그의 실제 구현부 인 `api.tag`는 `WEB-INF > tags` 에 있습니다.