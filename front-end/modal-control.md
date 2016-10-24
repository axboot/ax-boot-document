# 모달 컨트롤

웹 애플리케이션 모달창을 컨트롤 하여 데이터를 넘겨주고 또 모달에서 다시 부모창으로 값을 돌려받는 일은 상당히 번거롭고 개발 할 때 마다 만족스럽지 못한 일입니다.
모달창에서 부모창의 즉 `opener` 또는 `parent`의 도큐먼트의 정해진 함수를 호출하여 값을 주고 받아야 하는데. 모달 때문에 애플리케이션의 함수를 지저분 하게 짜는 일은 정말 피하고 싶기 때문입니다.

AXBOOT에서는 `axboot.modal` 함수를 이용하여 값을 주고 받는 함수를 함수의 아규먼트 형태로 만들었습니다.

### samples / grid-modal
```js
var ACTIONS = axboot.actionExtend(fnObj, {
    ETC3FIND: function (caller, act, data) {
        axboot.modal.open({
            modalType: "SAMPLE-MODAL",
            param: "",
            sendData: function(){
                // 모달창에 전달할 오브젝트.
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

### samples / modal
모달창쪽에서는 다음과 같이 getData, callBack 할 수 있다.

#### getData
```js
fnObj.pageStart = function () {
    var _this = this;
    
    console.log(parent.axboot.modal.getData());
    // {"sendData": "AX5UI"} 부모창에서 가져온 값
};
```

#### callback
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