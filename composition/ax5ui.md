## UI Framework (AX5UI)

- ax5ui 소개 사이트 http://ax5.io
- ax5ui Github : https://github.com/ax5ui

> AXBoot 프런트엔드는 HTML5, CSS3 (SCSS), JavaScript를 기반으로 UI 프레임워크 및 레이아웃 시스템을 내장하고 있습니다. 
UI 프레임워크에는 다음과 같은 모듈이 포함되어 있습니다.

- Mask
    - 마스크는 요청을 처리하는 동안 사용자 인터랙션을 잠시동안 막고 UI에 변화를 주는 컴포넌트 입니다.
    ![ax5ui-mask](../assets/5D5816FA378CF6F2D93146B886EC86D8.png)


- Dialog 
    - 레이어 다이얼로그 컴포넌트 입니다. 경고창, 확인창, 입력창등의 구현을 Dialog 확장하여 구현할 수 있습니다.
    ![ax5ui-dialog](../assets/255A9AD0F3A32F513DD003CE7ECBC219.png)
    ![ax5ui-dialog](../assets/AA2F115AF908A7AE00BE3487FFF8625D.png)
    ![ax5ui-dialog](../assets/749CCEEA0C8FA0E14702AA0A70441EF8.png)

- Toast
    - 처리완료, 알림 등을 표현할 수 있는 토스트 컴포넌트 입니다.
    ![ax5ui-toast](../assets/FEEC6CABBC5204C894EB56C09447F88D.png)
    ![ax5ui-toast](../assets/E094DF49AFB099FAEE5FABDAC12252AE.png)

- Modal
    - 레이어 모달 컴포넌트 입니다. 팝업 윈도우 보다 UI 인터랙션이 우수한 레이어 기반의 모달을 사용할 수 있습니다.
    ![ax5ui-modal](../assets/92D74E0E7092444CC55B977C9696C8E7.png)

- Calendar
    - 달력 컴포넌트 입니다. 년/월/일 선택이 매우 편리하고 디자인이 우수한 달력을 제공합니다.
    - 기간선택 및 특정 기간만 활성화, 다중선택, 이벤트 표시 등의 기능이 있습니다.
    ![ax5ui-calendar](../assets/BF4C56B9338D5227B5A61D06D427FEAA.png)

- Picker 
    - Input, Button 등에 피커기능을 확장할 수는 피커 컴포넌트 입니다. 날짜, 기간, 가상키보드, 가상키패드 등의 피커를 사용할 수 있습니다.
    ![ax5ui-picker](../assets/1DBFBE75DC8627AF445DD59E9950CA4A.png)
    ![ax5ui-picker](../assets/259A79A5453AF822E15E637D3CE1204A.png)
    ![ax5ui-picker](../assets/FEC20ACD1685A2715965CDCB5D802FB6.png)

- Formatter
    - Input값에 포맷을 지정할 수 있는 컴포넌트 입니다. 화폐, 날짜, 시간 등의 기본제공 포맷을 비롯해 필요한 포맷기능을 확장하여 사용할 수 있습니다.
    ![ax5ui-formatter](../assets/E9293126CEF58CF6002681185A022EE7.png)
    ![ax5ui-formatter](../assets/30B858148E07466365A5E3C713CD5E54.png)

- Menu
    - 메뉴 기능을 제공하는 컴포넌트 입니다. 컨텍스트 메뉴(마우스 우측 클릭)과 드롭다운 메뉴를 제공합니다. 
    ![ax5ui-menu](../assets/22ACD285EC59616C873232227CDA8A21.png)
    ![ax5ui-menu](../assets/519EFB7C5F5E49EBC682B8386156B3B2.png)

- Media-Viwer
    - 미디어(동영상, 사진)를 모아서 볼 수 있는 미디어 뷰 컴포넌트 입니다. Youtube, Vimeo, 사진 등의 미디어를 추가하면 슬라이드 뷰 형태로 미디어를 볼 수 있도록 해줍니다.
    ![ax5ui-media-viewer](../assets/413A7F6B2CD2A5D4C99E279D9CB73C39.png)

- Select
    - HTML의 Select 기능을 구현한 컴포넌트 입니다. JavaScript를 통해 간편하게 이벤트를 주고 받을 수 있으며, 선택, 다중선택, 연쇄 선택, 그룹기능을 제공합니다.
    ![ax5ui-select](../assets/6D21510D320E2A36722F6C6C4797CEA3.png)
    ![ax5ui-select](../assets/5EF6053C42078E3F41F31A28E4CF3E6B.png)

- Layout
    - 동적 레이아웃을 제공하는 컴포넌트 입니다. 각 영역의 크기를 동적으로 제어할 수 있습니다.
    ![ax5ui-layout](../assets/09CDFA02A31A9049651EE652F7F2D79B.png)

- Combobox
    - 단일, 다중선택이 가능한 콤보박스 컴포넌트 입니다. 
    ![ax5ui-combobox](../assets/58F8E5CA435CE834C18A8EA1995281DA.png)
    
- AutoComplete
    - 자동완성 기능을 제공하는 컴포넌트 입니다. 
    ![ax5ui-autocomplete](../assets/F0D56332B05460FA793C887B23EA443A.png)
    
- Grid
    - 그리드 컴포넌트 입니다. 다중 컬럼그룹, 틀고정, 정렬, 소계, 합계 기능을 제공합니다.
    ![ax5ui-grid](../assets/799D5C8C1641AC0184EB3DC746F05808.png)
    ![ax5ui-grid](../assets/E54BE4908EBECBD633671F66539807C3.png)
    
AXBoot프레임워크를 ax5ui의 기능들과 함께 사용 했을 때 그 효율성이 극대화 되지만 다양한 니드에 맞는 UI들이 필요할 때. 기능이 부족하거나 없는 UI가 있을 수 있습니다.
AXBoot의 UI시스템은 jQuery와 Bootstrap과 100% 호환되도록 설계 제작되었기 때문에 필요한 플러그인들은 웹에서 검색하여 적용 할 수 있습니다.