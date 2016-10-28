# 그리드 페이징

자세한 그리드 페이징 문서는 [ax5ui-grid](http://ax5.io/ax5ui-grid/demo/14-paging.html)를 참고하세요.

그리드 setData에 다음과 같이 페이지정보를 포함하면 그리드 하단에 페이징UI가 출력됩니다.
```js
myGrid.setData({
    list: list,
    page: {
        currentPage: pageNo || 0,
        pageSize: 50,
        totalElements: 500,
        totalPages: 100
    }
});
```
사용자가 페이지를 클릭하면 `setConfig`에 정의된 `page.onChange` 함수가 실행되고, 함수 매개변수로 페이징 정보가 전달됩니다. 
다음 예제는 `gridBuilder`에 페이징 처리를 공통으로 한 후 onPageChange 함수를 통해 페이징을 구현한 예제 입니다.

## gridView
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
            target: $('[data-ax5grid="grid-view-01"]'),
            columns: [
                {key: "key", label: "KEY", width: 80, align: "left"},
                {key: "value", label: "VALUE", width: 120, align: "left"},
                {key: "etc1", label: "ETC1", width: 70, align: "center"},
                {key: "ect2", label: "ETC2", width: 70, align: "center"},
                {key: "ect3", label: "ETC3", width: 70, align: "center"},
                {key: "ect4", label: "ETC4", width: 70, align: "center"}
            ],
            body: {
                onClick: function () {
                    this.self.select(this.dindex);
                    ACTIONS.dispatch(ACTIONS.ITEM_CLICK, this.item);
                }
            },
            onPageChange: function (pageNumber) {
                // 사용자가 페이지를 클릭했을 때.
                ACTIONS.dispatch(ACTIONS.PAGE_SEARCH, {page: {pageNumber: pageNumber}});
            }
        });
    }
});
```

## ACTIONS
```js
var ACTIONS = axboot.actionExtend(fnObj, {
    PAGE_SEARCH: function (caller, act, data) {

        // 넘겨받은 페이지번호를 searchView로 전달해줍니다.
        if (data && data.page) {
            caller.searchView.setPageNumber(data.page.pageNumber);
        }

        axboot.ajax({
            type: "GET",
            url: ["samples", "parent"],
            data: caller.searchView.getData(),
            callback: function (res) {
                caller.gridView01.setData(res);
            },
            options: {
                onError: function (err) {
                    console.log(err);
                }
            }
        });

        return false;
    }
});
```
위 예제에서는 그리드의 페이지가 변경되면 `onPageChange`함수가 호출된 후 `PAGE_SEARCH` 액션을 호출합니다. 
- ACTIONS에 정의된 `PAGE_SEARCH` 액션은 `searchView`의 `getData`를 통해 조회 조건을 수집하고 
- `gridView`의 `getPageData`를 통해 페이징 조건을 수집한 후 AJAX 요청 매개변수로 전달하게 됩니다.
