# 그리드 페이징

그리드에 페이징을 하기 위해서는 ax5ui-grid(http://ax5.io/ax5ui-grid/demo/14-paging.html) API를 먼저 알아야 합니다.
그리드에 setData를 다음과 같이 페이지정보를 포함하여 하면 그리드 하단에 페이징이 출력됩니다.
```js
myGrid.setData({
    list: list,
    page: {
        currentPage: _pageNo || 0,
        pageSize: 50,
        totalElements: 500,
        totalPages: 100
    }
});
```
사용자가 페이지를 클릭하면 setConfig에서 정의한 `page.onChange` 함수가 실행되고 함수안에 page정보가 있습니다.
 
AXBOOT에서는 gridBuilder를 이용하여 ax5ui-grid를 만들게 되므로 약간 다른 방식으로 페이징 이벤트를 처리 합니다.

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

searchView는 `axboot.searchView`를 상속받았으므로 `axboot.searchView`에 정의된 setPageNumber를 이용하여 `this.pageNumber`에 값을 변경 하게 됩니다.
페이지 정보들은 `searchView.getData` 에서 리턴 하도록 되어 있으므로 API는 페이징 정보를 받아 페이징된 데이터를 리턴 하게 됩니다.

