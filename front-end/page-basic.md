# 페이지 구조설명

## 기본 페이지 구성


## ax커스텀 태그
AXBOOT JSP페이지는 JSTL2.0 스펙을 이용한 커스텀태그를 지원합니다.
커스텀 태그는 WEB-INF > tags 아래에 *.tag 파일들로 원하는 태그를 직접 만들어 사용할 수 있습니다.
AXBOOT에서는 웹 애플리케이션 개발에 필요한 커스텀 태그를 미리 만들어 제공하고 있습니다. AXBOOT의 커스텀 태그를 이용하여 개발에 날개를 달아보세요. 
다음은 몇가지 커스텀 태그 샘플을 소개 하겠습니다.

## ax:tbl, ax:tr, ax:td
```html
<ax:form name="formView01">
    <input type="hidden" name="hiddenValue" value=""/>
    <ax:tbl clazz="ax-form-tbl" minWidth="500px">
        <ax:tr>
            <ax:td label="이름" width="300px">
                <input type="text" name="userNm" data-ax-path="userNm" maxlength="15" title="이름" class="av-required form-control W120" value=""/>
            </ax:td>
            <ax:td label="아이디" width="220px">
                <input type="text" name="userCd" data-ax-path="userCd" maxlength="100" title="아이디" class="av-required form-control W150" value=""/>
            </ax:td>
        </ax:tr>
        <ax:tr>
            <ax:td label="내용" width="100%">
                <input type="password" name="userPs" data-ax-path="userPs" maxlength="128" class="form-control W120" value="" readonly="readonly"/>
            </ax:td>
        </ax:tr>
    </ax:tbl>
</ax:form>
```

**ax:table 출력결과 예**

![ax-table](../assets/ax-table.png)