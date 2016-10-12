# 기본템플릿

> 기본 템플릿은 demo.axboot.com 접속 후 `레이아웃 샘플 > 기본템플릿` 메뉴를 선택하시면 확인 할 수 있습니다. 기본 템플릿은 검색바와 인라인 에디트를 지원하는 그리드를 기본 구성으로 하는 샘플 페이지 입니다.
> API 로는 `/api/v1/samples/parent` [GET][PUT] 을 사용합니다.

![기본템플릿 미리보기](../assets/basic-template.png)

## VIEW
```html
<%@ page contentType="text/html; charset=UTF-8" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ taglib prefix="ax" tagdir="/WEB-INF/tags" %>

<ax:set key="title" value="${pageName}"/>
<ax:set key="page_desc" value="${PAGE_REMARK}"/>
<ax:set key="page_auto_height" value="true"/>
```
페이지의 선언 구문 입니다. 레이아웃 (`WEB-INF/tags/layout/base.tag`) 파일에 전달된 변수를 `ax:set`으로 정의 합니다.
각각의 프로그램 페이지는 시스템에서 설정한 메뉴이름을 session변수로 가지고 있습니다. 세션변수로 전달된 값들은 `${pageName}`으로 jstl 에서 사용 할 수 있습니다.

```html
<ax:layout name="base">
    <jsp:attribute name="script">
        <script type="text/javascript" src="<c:url value='js/basic.js' />"></script>
    </jsp:attribute>
```
페이지에서 사용 할 JS파일을 지정 합니다. `jsp:attribute`는 script뿐 아니라 레이아웃에서 정의한 키 값이면 모두 사용 할 수 있습니다.
단. AXBOOT에서는 `jsp:body`가 항상 가장 마지막 요소 이어야 하므로 `jsp:attribute`를 먼저 선언 후 `jsp:body`를 마지막에 두어야 합니다.  


```html
    <jsp:body>
        <ax:page-buttons></ax:page-buttons>
```
프로그램이 가진 권한에 따라 페이지의 버튼을 출력 시켜주는 커스텀 태그 입니다. `WEB-INF/tags/page-buttons.tag` 에서 확인 할 수 있습니다.


```html
        <div role="page-header">
            <ax:form name="searchView0">
                <ax:tbl clazz="ax-search-tbl" minWidth="500px">
                    <ax:tr>
                        <ax:td label='검색조건' width="300px">
                            <input type="text" class="form-control" />
                        </ax:td>
                        <ax:td label='검색조건 1' width="300px">
                            <input type="text" class="form-control" />
                        </ax:td>
                        <ax:td label='검색조건 2' width="300px">
                            <input type="text" class="form-control" />
                        </ax:td>
                    </ax:tr>
                </ax:tbl>
            </ax:form>
            <div class="H10"></div>
        </div>

        <ax:split-layout name="ax1" oriental="horizontal">
            <ax:split-panel width="*" style="">

                <!-- 목록 -->
                <div class="ax-button-group" data-fit-height-aside="grid-view-01">
                    <div class="left">
                        <h2><i class="cqc-list"></i>
                            프로그램 목록 </h2>
                    </div>
                    <div class="right">
                        <button type="button" class="btn btn-default" data-grid-view-01-btn="add"><i class="cqc-circle-with-plus"></i> 추가</button>
                        <button type="button" class="btn btn-default" data-grid-view-01-btn="delete"><i class="cqc-circle-with-plus"></i> 삭제</button>
                    </div>
                </div>
                <div data-ax5grid="grid-view-01" data-fit-height-content="grid-view-01" style="height: 300px;"></div>

            </ax:split-panel>
        </ax:split-layout>
    </jsp:body>
</ax:layout>
```

