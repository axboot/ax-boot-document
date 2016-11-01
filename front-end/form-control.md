# 폼 컨트롤

이제는 웹 애플리케이션 API에서 JSON을 사용하는 것이 너무도 당연하게 되었습니다.
업계에서 10년전까지는 XML를 쓰는 것이 보편적이었으나, JSON의 유연하고 가벼운 구조 때문에 이제 XML를 사용하는 API는 찾아보기 힘들 지경입니다.

AXBoot에서도 모든 API에 JSON을 이용하고 있습니다. 

그럼 JSON데이터를 어떻게 하면 효과적으로 form 안에 form-control들에게 뿌려주고, 사용자가 입력한 값을 수집하여 API로 전달할 수 있을까요?

jQuery에는 `$(document.myform).serialize()` 같은 메소드가 있습니다. 한 때 제가 가장 많이 사용하던 메소드 중에 하나 입니다.
서버로 클라이언트의 입력값을 전달하기 위한 기본중에 기본이니까요.
하지만 아쉽게도 JSON데이터를 받아 form에 출력하고 다시 수집하여 JSON데이터 그대로 API로 보내기 위해선 개발자의 손목에 무리가 갈정도의 작업이 필요합니다.

```js
// 데이터 출력
$('#name').val(data.name);
$('#title').val(data.title);
$('#age').val(data.age);

// 데이터 수집
var returnData = {};
returnData["name"] = $('#name').val();
returnData["title"] = $('#title').val();
returnData["age"] = $('#age').val();
```

3개까지는 일일이 타이핑 할 수 있겠지만.. 그 이상은 무리가 있네요.. 게다가 단순히 코드양만의 문제가 아니라. 
서버로부터 받은 JSON데이터 중에 일부만 변경하고 사용자가 입력한 일부의 키 값만 수정하고 다시 서버로 전달 해야 하는 경우엔 좀 더 상황이 복잡해 집니다.
 
```js

// 데이터 수집
var returnData = {};
returnData["name"] = $('#name').val();
returnData["title"] = $('#title').val();
returnData["age"] = $('#age').val();

$.ajax({
    url:"",  data: $.extend({}, serverData, returnData)
});
```
serverData를 잃어버리지 않게 조심히 다루어야 겠습니다.

## 2Way Binding

이런 문제를 해결 하기 위해선 2Way Binding이라는 개념이 필요합니다. 
쉽게 애기하면, 데이터를 조작하면 VIEW에 표시값이 자동 변경되고, VIEW에 값을 변경하면 데이터의 값이 자동 변경 되게 해주는 것 을 말합니다.
하지만 좋은 것은 항상 조금 어렵습니다.

설정이 많고 복잡합니다. (물론 좀 더 많은 것을 할 수 있습니다. 예를 들어 AngularJS, knockoutjs 등이 대표 적입니다.)
간단한 폼을 만드는데 이렇게 많은 코드가 필요한 걸까?.

이런 고민을 하다, 정말 간단한 2Way Binding을 지원하는 ax5ui-binder를 만들었습나다.

## ax5ui-binder

```html
<ax:form name="formView01">
    <ax:tbl clazz="ax-form-tbl">
        <ax:tr>
            <ax:td label="키(KEY) *" width="300px">
                <input type="text"  class="form-control" data-ax-path="key" title="키(KEY)" data-ax-validate="required" />
                <!-- 
                data-ax-path="key" : input value를 data["key"]의 값을 사용하고 input value가 변경되면 data["key"] 값을 변경 해주도록 정의.
                title="키(KEY)" data-ax-validate="required" : 폼의 값을 검증할 때 해당 input를 체크 하겠다는 의미 이며 검증시 데이터의 타이틀을 "키(KEY)"로 정의.
                -->
            </ax:td>
        </ax:tr>
        <ax:tr>
            <ax:td label="값(VALUE)" width="300px">
                <input type="text" data-ax-path="value" class="form-control" />
            </ax:td>
        </ax:tr>
        <ax:tr>
            <ax:td label="ETC1" width="300px">
                <input type="text" data-ax-path="etc1" class="form-control" data-ax5formatter="money" />
            </ax:td>
            <ax:td label="ETC2" width="300px">
                <select data-ax-path="etc2" class="form-control W100">
                    <option value="ko_KR">대한민국</option>
                    <option value="en_US">미국</option>
                </select>
            </ax:td>
        </ax:tr>
        <ax:tr>
            <ax:td label="비고" width="100%">
                <textarea data-ax-path="etc4" class="form-control"></textarea>
            </ax:td>
        </ax:tr>
    </ax:tbl>
</ax:form>
```

```js

/**
 * formView01
 */
fnObj.formView01 = axboot.viewExtend(axboot.formView, {
    getDefaultData: function () {
        return $.extend({}, axboot.formView.defaultData, {});
    },
    initView: function () {
        this.target = $("#formView01");
        this.model = new ax5.ui.binder();
        this.model.setModel(this.getDefaultData(), this.target);
        this.modelFormatter = new axboot.modelFormatter(this.model); // 모델 포메터 시작
        this.initEvent();

        axboot.buttonClick(this, "data-form-view-01-btn", {
            "form-clear": function () {
                ACTIONS.dispatch(ACTIONS.FORM_CLEAR);
            }
        });
    },
    initEvent: function () {
        var _this = this;
    },
    getData: function () {
        var data = this.modelFormatter.getClearData(this.model.get()); // 모델의 값을 포멧팅 전 값으로 치환.
        return $.extend({}, data);
    },
    setData: function (data) {
        if (typeof data === "undefined") data = this.getDefaultData();
        data = $.extend({}, data);

        this.target.find('[data-ax-path="key"]').attr("readonly", "readonly");

        this.model.setModel(data);
        this.modelFormatter.formatting(); // 입력된 값을 포메팅 된 값으로 변경
    },
    validate: function () {
        var rs = this.model.validate();
        if (rs.error) {
            alert(rs.error[0].jquery.attr("title") + '을(를) 입력해주세요.');
            rs.error[0].jquery.focus();
            return false;
        }
        return true;
    },
    clear: function () {
        this.model.setModel(this.getDefaultData());
        this.target.find('[data-ax-path="key"]').removeAttr("readonly");
    }
});
```

initView에서 `this.model = new ax5.ui.binder();` 즉 fnObj.formView01.model 에 바인더의 객체를 정의하고 
setModel로 모델의 초기화, `setData`, `getData`를 이용하여 데이터를 뿌리고 수집합니다.
VIEW와 컨트롤이 완전히 분리되어 `퍼블리셔`와 협업이 매우 용이한 구조를 가지고 있습니다. 아무리 좋은 프레임워크라도 혼자서 다 만들어야 한다면 괴로우니까요.

게다가 `this.modelFormatter = new axboot.modelFormatter(this.model);` 라는 구문이 `data-ax5formatter` 속성 값을 이용하여 필드의 포멧팅을 자동 처리 해줍니다.
하지만 서버로 포멧팅 된 값을 전달하면 문제가 될 수 있기 때문에 getData에서 `var data = this.modelFormatter.getClearData(this.model.get());` 하여 포멧팅 된 값을 모두 제거하게 됩니다.
포멧팅 속성에 대한 확장은 `ax-boot-framework/ax-boot-admin/src/main/webapp/assets/js/axboot/src/modules/modelFormatter.js` 에서 확인 할 수 있고.

```js
/**포멧터의 포멧터 패턴 확장**/
ax5.ui.formatter.formatter["chequer"] = {
    getEnterableKeyCodes: function (_opts) {
        var enterableKeyCodes = {
            '189': '-' // eventKeyCode
        };
        return jQuery.extend(
            enterableKeyCodes,
            ax5.ui.formatter.formatter.ctrlKeys,
            ax5.ui.formatter.formatter.numKeys
        );
    },
    getPatternValue: function (_opts, optIdx, e, val, eType) {
        val = val.replace(/\D/g, "");
        var regExpPattern = /^([0-9]{2})\-?([0-9]{2})?\-?([0-9]{2})?\-?([0-9]{2})?/;
        return val.replace(regExpPattern, function (a, b) {
            var nval = [arguments[1]];
            if (arguments[2]) nval.push(arguments[2]);
            if (arguments[3]) nval.push(arguments[3]);
            if (arguments[4]) nval.push(arguments[4]);
            return nval.join("-");
        });
    }
};
```

처럼 사용자 패턴을 추가 정의 할 수 있습니다.

### 참고

```html
<input type="text" class="form-control W120" value="" data-ax-path="hpNo" data-ax5formatter="phone"/>

// 필수입력 필드
<input type="text" class="form-control" value="" 
data-ax-validate="required" title="매장코드" 
data-ax-path="storCd"/>

// 달력선택
<input type="text" class="form-control" value="" 
data-ax-path="closeDt" data-ax5formatter="date" data-ax5picker="date"/>

// 통화 입력
<input type="text" class="form-control" value="" 
data-ax-path="cost" data-ax5formatter="money"/>

// 기간 선택 달력
<div class="form-group" data-ax5picker="date">
    <div class="input-group">
        <input type="text" class="form-control" data-ax-path="storeInfoJson.계약시작일" data-ax5formatter="date"/>
        <span class="input-group-addon">~</span>
        <input type="text" class="form-control" data-ax-path="storeInfoJson.계약종료일" data-ax5formatter="date"/>
        <span class="input-group-addon"><i class="cqc-calendar"></i></span>
    </div>
</div>

// inline input
<input type="text" class="form-control W250 inline-block" value="" placeholder="주소" readonly="readonly" data-ax-path="storeInfoJson.주소"/>
<input type="text" class="form-control W250 inline-block" value="" placeholder="기타주소" maxlength="50"  data-ax-path="storeInfoJson.기타주소"/>
```