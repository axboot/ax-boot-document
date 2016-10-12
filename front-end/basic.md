# 페이지 구조설명

```jsp
<%@ page contentType="text/html; charset=UTF-8" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ taglib prefix="ax" tagdir="/WEB-INF/tags" %>
 
<!-- 레이아웃 전달 하고 싶은 변수를 선언합니다. -->
<ax:set key="title" value="${pageName}"/>
<ax:set key="page_desc" value="${PAGE_REMARK}"/>
<ax:set key="page_auto_height" value="true"/>
 
<!-- 사용하려는 레이아웃 명을 입력합니다. (레이아웃은 WEB-INF > tags > layout 에서 관리됩니다.) -->
<ax:layout name="base">
 
    <!-- 페이지에서 사용하는 스크립트 파일을 선언합니다. attribute script의 출력위치는 layout에서 결정합니다. -->
    <jsp:attribute name="script">
        <script type="text/javascript" src="<c:url value='js/page-structure.js' />"></script>
    </jsp:attribute>
 
    <!-- 페이지의 본문 영역입니다. -->
    <jsp:body>
 
        <!-- 프로그램 권한과 메뉴에서 정의한 사용권한 정보를 이용하여 프로그램에서 사용 가능한 버튼을 자동 처리 합니다. -->
        <ax:page-buttons></ax:page-buttons>
 
        <div role="page-header">
            <ax:form name="searchView0">
                <ax:tbl clazz="ax-search-tbl" minWidth="500px">
                    <ax:tr>
                        <ax:td label='메뉴그룹' width="300px">
                            <ax:common-code groupCd="MENU_GROUP" id="menuGrpCd"/>
                        </ax:td>
                    </ax:tr>
                </ax:tbl>
            </ax:form>
            <div class="H10"></div>
        </div>
 
        <!-- role="page-header" 높이를 뺀 나머지 높이를 role="page-content" 가 차지하게 됩니다 -->
        <div role="page-content">
 
        </div>
 
    </jsp:body>
</ax:layout>
```