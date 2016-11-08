# 페이지구조 & 사용자정의 태그

## 기본 페이지 구성

```html
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

## AXBoot 사용자정의 태그
AXBoot JSP페이지는 JSTL을 이용한 사용자정의 태그를 지원합니다. 사용자정의 태그는 WEB-INF > tags 아래에 .tag 파일로 선언되어 있으며, 요구사항에 따라 태그를 추가하거나 기본제공되는 태그를 변경할 수 있습니다.

## ax:tbl, ax:tr, ax:td
테이블 코드를 간단하게 작성할 수 있도록 도와주는 사용자정의 태그입니다.
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
**ax:tbl 출력결과 예**

![ax:table출력결과](https://raw.githubusercontent.com/axboot/ax-boot-document/master/assets/ax-table.png)

> `ax:tbl`은 반응형 테이블로 생성됩니다. `ax:td`는 한 컬럼에 `라벨과` `데이터`를 한번에 표현합니다. 위 예제에서 처럼 <ax:td label="이름"><input...></ax:td> 태그는 한 컬럼에 `이름` 라벨과 함께 `input` 컨트롤이 추가됩니다. 한 컬럼의 너비는 `width` 속성으로 정의 하고, 컬럼 내의 라벨 너비는 `labelWidth`로 정의합니다.

---

## ax:split-layout, ax:split-panel
동적 크기 조정이 가능한 레이아웃 시스템을 제공합니다. 좌우/상하 레이아웃이 구현된 샘플은 [좌우레이아웃][상하레이아웃] 을 확인하세요.
```html
<ax:split-layout name="ax1" orientation="vertical">
    <ax:split-panel width="300" style="padding-right: 10px;">
        너비가 300인 왼쪽 패널
    </ax:split-panel>
    <!-- splitter -->
    <ax:splitter></ax:splitter>
    <ax:split-panel width="*" style="padding-left: 10px;" id="split-panel-form" scroll="true">
        너비가 나머지인 오른쪽 패널 (건텐츠의 높이가 넘칠 경우 스크롤)
    </ax:split-panel>
</ax:split-layout>
<ax:split-layout name="ax1" orientation="horizontal">
    <ax:split-panel height="300" style="padding-bottom: 10px;">
        높이가 300인 상단 패널
    </ax:split-panel>
    <!-- splitter -->
    <ax:splitter></ax:splitter>
    <ax:split-panel height="*" style="padding-top: 10px;" id="split-panel-form" scroll="true">
        높이가 나머지인 하단 패널 (건텐츠의 높이가 넘칠 경우 스크롤)
    </ax:split-panel>
</ax:split-layout>
```
![ax-layout](https://raw.githubusercontent.com/axboot/ax-boot-document/master/assets/ax-layout.png)

---

## ax:tab-layout
컨텐츠를 복수개의 탭으로 분리하여 표현할 수 있는 탭 레이아웃입니다. 
```html
<ax:tab-layout name="ax2" data_fit_height_content="layout-view-01" style="height:100%;">
    <ax:tab-panel label="기본정보" scroll="scroll">
        <p>
            기본정보
        </p>
    </ax:tab-panel>
    <ax:tab-panel label="일반정보" scroll="scroll" active="true">
    	<p>
            일반정보
        </p>
    </ax:tab-panel>
</ax:tab-layout>
```
![ax-tabl-layout](https://raw.githubusercontent.com/axboot/ax-boot-document/master/assets/ax-tab-layout.png)
