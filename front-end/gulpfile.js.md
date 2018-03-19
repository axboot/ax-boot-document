# gulpfile.js

AXBoot는 프론트엔드 빌드 자동화 도구로 `Gulp`를 사용하고 있습니다.
`gulpfile.js`는 Gulp의 설정 파일로서 여러 작업(task)들이 정의되어 있습니다.


### AXBoot에서 사용하는 Gulp 작업들에 대한 설명입니다.

작업(task) | 설명
--- | ---
plugin update | bower.json 에 명시된 plugin 컴포넌트를 최신 버전으로 업데이트합니다.
plugin-js | bower를 통해 설치된 plugin 컴포넌트를 병합하여 `plugin.js`와 plugin.js가 압축된 버전인 `plugin.min.js` 파일을 생성합니다.
axboot-js | assets/js/axboot/src 디렉토리에 위치한 _axboot.js 파일에 modules 폴더의 모듈들을 병합하여 [`axboot.js`](https://api.axboot.com/front-end/axboot.js.html)와 axboot.js가 압축된 버전인 `axboot.min.js` 파일을 생성합니다. 
scss | assets/scss 디렉토리에 위치한 scss 파일들을 컴파일한 후  병합, 압축하여 `axboot.css` 파일을 생성합니다. 
scss-ie9 | IE9 버전을 위한 css 파일을 생성합니다. <br/> assets/scss 디렉토리에 위치한 scss 파일들을 컴파일한 후  병합, 압축하여 `axboot-01.css`, `axboot-02.css`, `axboot-03.css` 총 세 개의 파일을 생성합니다.
dashboard-scss | 대시보드용 css 파일을 생성합니다.
watching | 리소스의 변화를 감지하여 axboot-js, scss task 가 자동으로 실행됩니다. <br/><br/> ex) watching task 를 실행 후 scss 파일을 수정하면, 파일의 수정을 감지하여 해당되는 task(여기서는 scss task)가 자동적으로 실행됩니다.
default | 터미털에서 gulp 명령어를 실행하면 default에 작성한 스크립트가 실행됩니다. <br/> default에는 watching task를 수행하라는 스크립트가 작성되어 있습니다.
