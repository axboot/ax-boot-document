# AXBoot 테마

[https://github.com/axboot/ax-boot-themes](https://github.com/axboot/ax-boot-themes) 에 AXBoot 테마가 공개 되어 있습니다.

### 사용법

`ax-boot-framework/ax-boot-admin/src/main/resources/axboot.json` 을 다음과 같이 수정하세요.
```json
{
  "title": "AXBoot :: Advanced Web Application Development Framework",
  "copyrights": "AXBoot 2.0.0 - Web Application Framework © 2010-2016",
  "logo": {
    "header": "[테마별주소]/images/header-logo.png",
    "login": "/assets/images/login-logo.png",
    "logo": "logo.png"
  },
  "background": {
    "login": "/assets/images/login-bg.jpg"
  },
  "layout": {
    "leftSideMenu": "visible"
  },
  "extendedCss": [
    "[테마별주소]axboot.css"
  ]
}
```

