# 기본템플릿

> 기본 템플릿은 [demo.axboot.com](http://demo.axboot.com) 접속 후 `레이아웃 샘플 > 기본템플릿` 메뉴를 선택하면 확인 할 수 있습니다. 기본 템플릿은 검색 바와 인라인 편집 기능이 포함된 그리드를 기본 구성으로 하는 샘플 페이지입니다.
> API 로는 `/api/v1/samples/parent` [GET][PUT] 을 사용합니다.

![기본템플릿 미리보기](https://raw.githubusercontent.com/axboot/ax-boot-document/master/assets/basic-template.png)

---

## VIEW
```html
<%@ page contentType="text/html; charset=UTF-8" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ taglib prefix="ax" tagdir="/WEB-INF/tags" %>

<ax:set key="title" value="${pageName}"/>
<ax:set key="page_desc" value="${PAGE_REMARK}"/>
<ax:set key="page_auto_height" value="true"/>
```
페이지의 선언 구문 입니다. 레이아웃 (`WEB-INF/tags/layout/base.tag`) 에 전달할 변수를 `ax:set`으로 정의 합니다.
시스템관리 -> 메뉴관리에서 지정한 메뉴명은 Request 속성 변수에 담겨있습니다. 해당 값들은 `${pageName}` 형태로 페이지에서 사용할 수 있습니다.

```html
<ax:layout name="base">
    <jsp:attribute name="script">
        <script type="text/javascript" src="<c:url value='js/basic.js' />"></script>
    </jsp:attribute>
</ax:layout>
```
페이지에서 사용 할 자바스크립트 파일을 지정 합니다. `jsp:attribute`는 `script`외에도 레이아웃에 정의된 키 값이면 확장하여 사용할 수 있습니다.
단. AXBoot에서는 여러개의 `jsp:attribute`가 있을 경우 반드시 `jsp:body` 윗 부분에 위치하도록 하여 `jsp:body`가 코드 가장 마지막에 나오도록 해야합니다.

`basic.js` 와 같은 프로그램 자바스크립트 파일은 레이아웃 페이지에 선언된 `axboot.js`에 의해 `fnObj.pageStart`함수가 실행됩니다.

---

```html
<jsp:body>
    <ax:page-buttons></ax:page-buttons>
</jsp:body>
```
---
프로그램과 메뉴가 가진 권한에 따라 페이지의 버튼을 출력하는 사용자 정의 태그입니다. `WEB-INF/tags/page-buttons.tag` 에서 확인할 수 있습니다.
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
```
프로그램 페이지는 `role="page-header"`, `role="page-content"` 로 나누어 집니다.
페이지가 시작되거나, 페이지 크기가 변경될 때마다 브라우저 높이에 맞게 화면을 출력하기 위해 `page-header`를 뺀 나머지 영역을 계산하여 `page-content`의 높이로 사용합니다.

![AXBoot-페이지롤](https://raw.githubusercontent.com/axboot/ax-boot-document/master/assets/page-layout-role.png)

높이 자동 계산 코드는 `axboot.js`에서 확인할 수 있습니다

---

```html
<ax:split-layout name="ax1" orientation="horizontal">
    <ax:split-panel width="*" style="">

        <!-- 목록 -->
        <div class="ax-button-group" data-fit-height-aside="grid-view-01">
            <div class="left">
                <h2><i class="cqc-list"></i>프로그램 목록 </h2>
            </div>
            <div class="right">
                <button type="button" class="btn btn-default" data-grid-view-01-btn="add"><i class="cqc-circle-with-plus"></i> 추가</button>
                <button type="button" class="btn btn-default" data-grid-view-01-btn="delete"><i class="cqc-circle-with-plus"></i> 삭제</button>
            </div>
        </div>
        <div data-ax5grid="grid-view-01" data-fit-height-content="grid-view-01" style="height: 300px;"></div>

    </ax:split-panel>
</ax:split-layout>
```
`ax:split-layout`는 화면을 종/횡으로 나눌 수 있는 레이아웃입니다 JSTL 태그 내부에서 `role="page-content"` 속성을 만들기 때문에 페이지 높이가 자동으로 최적화 됩니다.
`name`이 고유하기만 하면 여러번 중복하여 사용할 수 있습니다. `orientation`은 `vertical`과 `horizontal`로 사용하면 됩니다.

---

## JS

```js
var fnObj = {};
```
페이지에서 사용하는 기본 변수 객체 입니다.

```js
var ACTIONS = axboot.actionExtend(fnObj, {
    PAGE_SEARCH: function(){
        axboot.ajax({
            type: "GET",
            url: ["samples", "parent"],
            data: caller.searchView.getData(),
            callback: function (res) {
                caller.gridView01.setData(res);
            }
        });
        return false;        
    },
    dispatch: function(){
        var result = ACTIONS.exec(caller, act, data);
        if (result != "error") {
            return result;
        } else {
            // 직접코딩
            return false;
        }
    }
});
```
ACTIONS 객체는 `axboot > src > view-action.js`의 actionExtend 함수를 확장합니다.
ACTIONS 뷰 사이의 통신 방식을 메서드로 정의한 객체입니다. 예제에서 `PAGE_SEARCH`는 AJAX 요청으로 JSON을 가져와서 GridView에 넘겨주는 예제입니다.   
이는 메시지를 기반으로 통신하므로 뷰와 뷰 사이의 의존성을 제거하며 뷰의 재활용성을 높여줍니다.  

> AJAX URL을 재활용 하기위해 axboot.ajax는 URL 별칭기능을 제공합니다. axboot.config.js의 `axboot.def["API"]`에 별칭을 선언하면 됩니다. url["sample","parent"] 에서 "sample"은 별칭에서, "parent"는 별칭에서 가져온 주소 뒤쪽에 추가로 연결됩니다. "sample"의 주소가 `/api/v1/sample` 이라면 생성되는 최종 URL은 `/api/v1/samples/parent`가 됩니다.  

---

```js
// fnObj 기본 함수 스타트와 리사이즈
fnObj.pageStart = function () {
    this.pageButtonView.initView();
    this.searchView.initView();
    this.gridView01.initView();

    ACTIONS.dispatch(ACTIONS.PAGE_SEARCH);
};

fnObj.pageResize = function () {

};
```

각 페이지는 `head` 태그에 `axboot.js`를 임포트 하고 있습니다.
`axboot.js`에서는 `$(document.body).ready`를 사용하여 `axboot.init` > `axboot.pageStart` > `fnObj.pageStart` 순으로 호출합니다.

`fnObj.pageStart`에서는 페이지가 처음 시작된 후 실행 해야하는 `ACTIONS`를 선언하고, 페이지에 정의된 뷰를 `initView` 함수를 통해 초기화 합니다.

---

```js
fnObj.pageButtonView = axboot.viewExtend({
    initView: function () {
        axboot.buttonClick(this, "data-page-btn", {
            "search": function () {
                ACTIONS.dispatch(ACTIONS.PAGE_SEARCH);
            },
            "save": function () {
                ACTIONS.dispatch(ACTIONS.PAGE_SAVE);
            },
            "excel": function () {

            }
        });
    }
});
```
뷰는 개별 뷰에서 일어나는 일들만 기술하는 것을 원칙으로 하며, 해당 뷰에 데이터를 전달하거나 외부 뷰에서 해당 뷰의 데이터를 요청하거나 변경 할 때는 `getData`, `setData` 함수를 사용합니다.

---

그리드뷰는 `axboot.gridView` 상속하여 선언합니다. `axboot.gridView`는 `assets/js/axboot/src/view-action.js` 파일에서 확인할 수 있습니다.
몇몇 메서드는 미리 정의된 함수가 있으므로 기본 기능만 사용하는 경우 정의할 필요가 없습니다.

gridView.initView에서 `axboot.gridBuilder` 를 실행하여 `ax5ui-grid`를 초기화한 후 target에 연결합니다.

> axboot.buttonClick 을 이용하면 버튼을 클릭했을 때 이벤트를 편리하게 다룰 수 있습니다. 
axboot.buttonClick 함수는 `button data-grid-view-01-btn="add"`버튼을 클릭 했을 때 `add` 함수를 호출 할 수 있도록 하는 예제입니다.

```js
/**
 * gridView
 */
fnObj.gridView01 = axboot.viewExtend(axboot.gridView, {
    initView: function () {
        var _this = this;

        this.target = axboot.gridBuilder({
            showRowSelector: true,
            frozenColumnIndex: 0,
            multipleSelect: true,
            target: $('[data-ax5grid="grid-view-01"]'),
            columns: [
                {key: "key", label: "KEY", width: 160, align: "left", editor: "text"},
                {key: "value", label: "VALUE", width: 350, align: "left", editor: "text"},
                {key: "etc1", label: "ETC1", width: 100, align: "center", editor: "text"},
                {key: "ect2", label: "ETC2", width: 100, align: "center", editor: "text"},
                {key: "ect3", label: "ETC3", width: 100, align: "center", editor: "text"},
                {key: "ect4", label: "ETC4", width: 100, align: "center", editor: "text"}
            ],
            body: {
                onClick: function () {
                    this.self.select(this.dindex);
                }
            }
        });
        
        axboot.buttonClick(this, "data-grid-view-01-btn", {
            "add": function () {
                ACTIONS.dispatch(ACTIONS.ITEM_ADD);
            }
        });
    }
});
```

### axboot.gridBuilder
ax5ui-grid는 상당한 양의 설정옵션이 있습니다. 하지만 프로젝트 성격에 따라서는 동일한 설정코드가 반복적으로 나타날 수 있습니다. 그리드의 반복적인 설정 코드를 한데모아 적용해주는 `gridBuilder`를 사용하면 이런 문제를 해결할 수 있습니다.  

```js
var defaultGridConfig = {
    showLineNumber: true,
    lineNumberColumnWidth: 50,
    rowSelectorColumnWidth: 28,
    multipleSelect: false,
    header: {
        align: "center",
        columnHeight: 28
    },
    body: {
        columnHeight: 28,
        onClick: function () {
            this.self.select(this.dindex);
        }
    },
    page: {
        navigationItemCount: 9,
        height: 30,
        display: true,
        firstIcon: '<i class="cqc-controller-jump-to-start"></i>',
        prevIcon: '<i class="cqc-triangle-left"></i>',
        nextIcon: '<i class="cqc-triangle-right"></i>',
        lastIcon: '<i class="cqc-controller-next"></i>'
    }
};
```
`gridBuilder` 함수는 `js/axboot/src/gridBuilder.js` 에 선언되어 있습니다. 위는  `gridBuilder`에 선언된 그리드 기본 설정 옵션으로, 추가적인 설정을 선언하면 설정이 오버라이딩 되어 최종 그리드가 생성됩니다.