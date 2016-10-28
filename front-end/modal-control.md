# 모달 컨트롤

AX5UI의 모달 컨트롤은 `sendData`과 `callback` 두가지 함수만 작성하면 됩니다.     

### 모달창 호출
```js
var ACTIONS = axboot.actionExtend(fnObj, {
    ETC3FIND: function (caller, act, data) {
        axboot.modal.open({
            modalType: "SAMPLE-MODAL",
            param: "",
            sendData: function(){
                // 모달창에 전달할 객체
                return {
                    "sendData": "AX5UI"
                };
            },
            callback: function (data) {
                // 모달창에서 실행 data를 넘겨 받습니다.
                caller.formView01.setEtc3Value({
                    key: data.key,
                    value: data.value
                });
                // 모달창을 닫으려면 여기서 this는 modal UI 인스턴스가 됩니다.
                this.close();
            }
        });
    }
});
```
---

### 모달창

#### getData
`getData` 함수를 통해 부모창에서 `setData`를 통해 전달한 데이터를 받을 수 있습니다
```js
fnObj.pageStart = function () {
    var _this = this;
    
    console.log(parent.axboot.modal.getData());
    // {"sendData": "AX5UI"} 부모창에서 가져온 값
};
```

#### callback
`parent.axboot.modal.callback` 함수를 통해 모달창에서 부모창으로 처리한 결과를 전달할 수 있습니다.`
```js
var ACTIONS = axboot.actionExtend(fnObj, {
    PAGE_CLOSE: function (caller, act, data) {
        if (parent) {
            parent.axboot.modal.close(); // 창을 닫습니다.
        }
    },
    PAGE_CHOICE: function (caller, act, data) {
        var list = caller.gridView01.getData("selected");
        if (list.length > 0) {
            if (parent && parent.axboot && parent.axboot.modal) {
                parent.axboot.modal.callback(list[0]); // 부모창에 callback 
            }
        } else {
            alert("선택된 목록이 없습니다.");
        }
    }
});
```