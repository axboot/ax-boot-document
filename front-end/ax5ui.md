# AX5UI

![AX5UI](https://github.com/ax5ui/ax5ui-kernel/raw/master/src/preview.png)

AX5UI는 jQuery/Bootstrap과 함께 사용하는 HTML5 웹표준 Javascript UI 플러그인입니다. (데모 : http://ax5.io) AX5UI를 사용하기 위해서는 "HTML, JS, CSS"에 대한 기본지식이 있어야 합니다. "HTML, JS, CSS"에 대한 지식은 검색엔진을 이용하여 쉽게 얻을 수 있습니다.

### jQuery

UI 플러그인 개발을 보다 빠르고 합리적으로 하기위해 jQuery 라이브러리를 사용하고 있습니다. 
AX5UI에서 jQuery 라이브러리의 역할은 원하는 엘리먼트를 찾고 지우고 추가하고 이벤트를 연결하는데 사용합니다. 
jQuery는 전세계에게 가장 많은 개발자가 사용중인 JS 라이브러리 입니다 (http://jquery.com/).

### Bootstrap

Bootstrap은 각종 레이아웃, 버튼, 입력창등의 디자인을 CSS와 Javascript로 미리 만들어진 프레임워크 입니다. 
웹 디자인의 혁명이라 불릴정도로 폭발적인 반응이 있었고, 전 세계적으로 가장 많이 사용된 프론트앤드 프레임워크 중에 하나입니다. 
AX5UI의 테마시스템은 SCSS코드로 제작되어, 최종 산출물인 CSS파일이 만들어지는 구조로 설계되었습니다. 
SCSS코드내 변수구조가 Bootstrap SCSS구조와 호환되도록 설계되어있고, 입력창등의 CSS 클래스 사용법을 Bootstrap와 같은 구조에서 최적화 되도록 개발 및 테스트 되었습니다.

## AX5UI Install

AX5UI는 별도의 설치과정 없이 소스코드를 웹페이지에 연결하는 것으로 준비가 완료 됩니다. 다음의 방법들 중 하나로 소스코드를 다운로드 받을 수 있습니다.

- Github에서 직접 다운로드.
- NPM 패키지 매니지먼트 이용. `npm install ax5core --save`
- Bower 패키지 매니지먼트 이용. `bower install ax5core --save`
- CDN 사용
- 클론하여 사용하기 `git clone https://github.com/ax5ui/ax5ui-kernel`

직접 다운로드 하는 방법은 잦은 패치를 적용하기 어렵습니다. NPM이나 Bower를 이용하여 업데이트를 하면 손쉽게 최신 버전의 라이브러리를 이용할 수 있습니다.
이런저런 것들이 귀찬다면 CDN을 이용하는 방법도 있습니다.

### AX5UI CDN 

```html
<!-- jquery -->
<script type="text/javascript" src="https://code.jquery.com/jquery-1.12.3.min.js"></script>

<!-- ax5core-->
<script type="text/javascript" src="https://cdn.rawgit.com/ax5ui/ax5core/master/dist/ax5core.min.js"></script>

<!-- ax5ui-mask -->
<link rel="stylesheet" type="text/css" href="https://cdn.rawgit.com/ax5ui/ax5ui-mask/master/dist/ax5mask.css" />
<script type="text/javascript" src="https://cdn.rawgit.com/ax5ui/ax5ui-mask/master/dist/ax5mask.min.js"></script>

<!-- ax5ui-dialog -->
<link rel="stylesheet" type="text/css" href="https://cdn.rawgit.com/ax5ui/ax5ui-dialog/master/dist/ax5dialog.css" />
<script type="text/javascript" src="https://cdn.rawgit.com/ax5ui/ax5ui-dialog/master/dist/ax5dialog.min.js"></script>

<!-- ax5ui-toast -->
<link rel="stylesheet" type="text/css" href="https://cdn.rawgit.com/ax5ui/ax5ui-toast/master/dist/ax5toast.css" />
<script type="text/javascript" src="https://cdn.rawgit.com/ax5ui/ax5ui-toast/master/dist/ax5toast.min.js"></script>

<!-- ax5ui-modal -->
<link rel="stylesheet" type="text/css" href="https://cdn.rawgit.com/ax5ui/ax5ui-modal/master/dist/ax5modal.css" />
<script type="text/javascript" src="https://cdn.rawgit.com/ax5ui/ax5ui-modal/master/dist/ax5modal.min.js"></script>

<!-- ax5ui-calendar -->
<link rel="stylesheet" type="text/css" href="https://cdn.rawgit.com/ax5ui/ax5ui-calendar/master/dist/ax5calendar.css" />
<script type="text/javascript" src="https://cdn.rawgit.com/ax5ui/ax5ui-calendar/master/dist/ax5calendar.min.js"></script>

<!-- ax5ui-picker -->
<link rel="stylesheet" type="text/css" href="https://cdn.rawgit.com/ax5ui/ax5ui-picker/master/dist/ax5picker.css" />
<script type="text/javascript" src="https://cdn.rawgit.com/ax5ui/ax5ui-picker/master/dist/ax5picker.min.js"></script>

<!-- ax5ui-formatter -->
<script type="text/javascript" src="https://cdn.rawgit.com/ax5ui/ax5ui-formatter/master/dist/ax5formatter.min.js"></script>

<!-- ax5ui-menu -->
<link rel="stylesheet" type="text/css" href="https://cdn.rawgit.com/ax5ui/ax5ui-menu/master/dist/ax5menu.css" />
<script type="text/javascript" src="https://cdn.rawgit.com/ax5ui/ax5ui-menu/master/dist/ax5menu.min.js"></script>

<!-- ax5ui-media-viewer -->
<link rel="stylesheet" type="text/css" href="https://cdn.rawgit.com/ax5ui/ax5ui-media-viewer/master/dist/ax5media-viewer.css" />
<script type="text/javascript" src="https://cdn.rawgit.com/ax5ui/ax5ui-media-viewer/master/dist/ax5media-viewer.min.js"></script>

<!-- ax5ui-select -->
<link rel="stylesheet" type="text/css" href="https://cdn.rawgit.com/ax5ui/ax5ui-select/master/dist/ax5select.css" />
<script type="text/javascript" src="https://cdn.rawgit.com/ax5ui/ax5ui-select/master/dist/ax5select.min.js"></script>

<!-- ax5ui-layout -->
<link rel="stylesheet" type="text/css" href="https://cdn.rawgit.com/ax5ui/ax5ui-layout/master/dist/ax5layout.css" />
<script type="text/javascript" src="https://cdn.rawgit.com/ax5ui/ax5ui-layout/master/dist/ax5layout.min.js"></script>

<!-- ax5ui-combobox -->
<link rel="stylesheet" type="text/css" href="https://cdn.rawgit.com/ax5ui/ax5ui-combobox/master/dist/ax5combobox.css" />
<script type="text/javascript" src="https://cdn.rawgit.com/ax5ui/ax5ui-combobox/master/dist/ax5combobox.min.js"></script>

<!-- ax5ui-autocomplete -->
<link rel="stylesheet" type="text/css" href="https://cdn.rawgit.com/ax5ui/ax5ui-autocomplete/master/dist/ax5autocomplete.css" />
<script type="text/javascript" src="https://cdn.rawgit.com/ax5ui/ax5ui-autocomplete/master/dist/ax5autocomplete.min.js"></script>

<!-- ax5ui-grid -->
<link rel="stylesheet" type="text/css" href="https://cdn.rawgit.com/ax5ui/ax5ui-grid/master/dist/ax5grid.css" />
<script type="text/javascript" src="https://cdn.rawgit.com/ax5ui/ax5ui-grid/master/dist/ax5grid.min.js"></script>
```

ax5.ui.xxx 로 각 UI플러그인의 클래스가 있습니다. UI플러그인들은 헤더에 UI JS파일이 import 되면 생성됩니다.
UI를 사용하는 방법은 jQuery extends방식과 new 연산자를 이용한 객체 생성 후 사용하는 2가지 방법이 있습니다.

## 객체 선언 방식

```js
var dialog = new ax5.ui.dialog({
    title: "AX5 Dialog"
});
// dialog 객체 생성

$('#alert-open').click(function () {
    dialog.alert('Alert message');
    // 객체의 메소드 호출
});
$('#alert-close').click(function () {
    dialog.close();
    // 객체의 메소드 호출
});
```

## jQuery Extends
```html
<div class="row">
    <div class="col-md-6">
        <div class="form-group">
            <div data-ax5select="select1" data-ax5select-config="{}"></div>
        </div>
    </div>
    <div class="col-md-6">
        <div class="form-group">
            <div data-ax5select="select2" data-ax5select-config="{
                                multiple: true,
                                reset:'<i class=\'fa fa-trash\'></i>'
                             }">
            </div>
        </div>
    </div>
</div>
```

```js
<script type="text/javascript">
var options = [];
for (var i = 0; i < 100; i++) {
    options.push({value: "optionValue" + i, text: "optionText" + i});
}
$(document.body).ready(function(){
    $('[data-ax5select]').ax5select({
        options: options
    });
});
</script>
```

각각의 UI별 예제와 사용법, API는 http://ax5.io 를 이용해주시고 질문은 gitHub 이슈나 StackOverflow 에 남겨주시면 저희가 추적해내어 해결해드립니다.
(StackOverflow에 질문하시면 더욱 성실히 답변 해드리겠네요.)
