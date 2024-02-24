##### | 모던 자바스크립트 DeepDive <br />

###### range: 40. event <br />

###### date: day27 (2024.02.24) <br />

<hr />
<br />

## 이벤트

#### mouse event

<table>
    <tr>
        <td>e type</td>
        <td>e 발생 시점</td>
    </tr>
    <tr>
        <td>click</td>
        <td>마우스 버튼 클릭 시</td>
    </tr>
    <tr>
        <td>dblclick</td>
        <td>마우스 더블 클릭 시</td>
    </tr>
    <tr>
        <td>mousedown</td>
        <td>마우스 버튼 눌렀을 시</td>
    </tr>
    <tr>
        <td>mouseup</td>
        <td>누르고 있던 마우스 버튼을 놓았을 시</td>
    </tr>
    <tr>
        <td>mousemove</td>
        <td>마우스 커서 움직였을 시</td>
    </tr>
    <tr>
        <td>mouseenter</td>
        <td>마우스 커서가 HTML 요소 안으로 이동했을 시 (버블링 X)</td>
    </tr>
    <tr>
        <td>mouseover</td>
        <td>마우스 커서가 HTML 요소 안으로 이동했을 시 (버블링 O)</td>
    </tr>
    <tr>
        <td>mouseleave</td>
        <td>마우스 커서를 HTML 밖으로 이동했을 시 (버블링 X)</td>
    </tr>
    <tr>
        <td>mouseout</td>
        <td>마우스 커서를 HTML 밖으로 이동했을 시 (버블링 O)</td>
    </tr>
</table>

#### keyboard event

ctrl, option, shift, tab, delete, enter, 방향 키, 문자, 숫자, 특수문자 키를 눌렀을 때 발생 <br />
그 외의 키는 한 번만 발생

<table>
    <tr>
        <td>e type</td>
        <td>e 발생 시점</td>
    </tr>
    <tr>
        <td>keydown</td>
        <td>모든 키를 눌렀을 때</td>
    </tr>
    <tr>
        <td>keypress</td>
        <td>문자 키를 눌렀을 때 연속적으로 발생 (사용 권장 X)</td>
    </tr>
    <tr>
        <td>keyup</td>
        <td>누르고 있던 키를 놨을 때 한 번만 발생</td>
    </tr>
</table>

#### focus event

focusin, focusout은 사파리와 크롬에서 정상 작동 X <br />
addEventHandler 메서드 방식을 사용해 등록해야 함

<table>
    <tr>
        <td>e type</td>
        <td>e 발생 시점</td>
    </tr>
    <tr>
        <td>focus</td>
        <td>HTML 요소가 포커스를 받았을 시 (버블링 X)</td>
    </tr>
    <tr>
        <td>blur</td>
        <td>HTML 요소가 포커스를 잃었을 시 (버블링 X)</td>
    </tr>
    <tr>
        <td>focusin</td>
        <td>HTML 요소가 포커스를 받았을 시 (버블링 O)</td>
    </tr>
    <tr>
        <td>focusout</td>
        <td>HTML 요소가 포커스를 잃었을 시 (버블링 O)</td>
    </tr>
</table>

#### form event

<table>
    <tr>
        <td>e type</td>
        <td>e 발생 시점</td>
    </tr>
    <tr>
        <td>submit</td>
        <td>
            1. form 요소 내의 input(text, checkbox, radio), select 입력 필드(textarea X)에서 엔터 키 <br />
            2. form 요소 내의 submit 버튼 클릭 <br />
        </td>
    </tr>
    <tr>
        <td>clear</td>
        <td>form 요소 내의 reset 버튼 클릭 시 (근래 사용 X)</td>
    </tr>
</table>

#### value-change event

<table>
    <tr>
        <td>e type</td>
        <td>e 발생 시점</td>
    </tr>
    <tr>
        <td>input</td>
        <td>input(text, radio, checkbox), select, textarea 요소의 값이 입력됐을 때</td>
    </tr>
    <tr>
        <td>change</td>
        <td>input(text, radio, checkbox), select, textarea 요소의 값이 변경됐을 때</td>
    </tr>
    <tr>
        <td>readystatechange</td>
        <td>HTML 문서의 로드와 파싱 상태를 나타내는 document.readyState 프로퍼티 값이 변경됐을 때</td>
    </tr>
</table>

#### DOM mutation event

<table>
    <tr>
        <td>e type</td>
        <td>e 발생 시점</td>
    </tr>
    <tr>
        <td>DOMcontentLoaded</td>
        <td>HTML 문서의 로드와 파싱이 완료되어 DOM 생성이 완료됐을 때</td>
    </tr>
</table>

#### view event

<table>
    <tr>
        <td>e type</td>
        <td>e 발생 시점</td>
    </tr>
    <tr>
        <td>resize</td>
        <td>브라우저 원도우 크기를 리자이즈할 때 연속적으로 발생</td>
    </tr>
    <tr>
        <td>scroll</td>
        <td>웹페이지/HTML 요소를 스크롤할 때 연속적으로 발생</td>
    </tr>
</table>

#### resource event

<table>
    <tr>
        <td>e type</td>
        <td>e 발생 시점</td>
    </tr>
    <tr>
        <td>load</td>
        <td>DOMcontentLoaded 이벤트가 발생한 후 모든 리소스 로딩이 완료됐을 때</td>
    </tr>
    <tr>
        <td>unload</td>
        <td>리소스가 언로드될 때</td>
    </tr>
    <tr>
        <td>abort</td>
        <td>리소스 로딩이 중단됐을 때</td>
    </tr>
    <tr>
        <td>error</td>
        <td>리소스 로딩이 실패했을 때</td>
    </tr>
</table>

<br />

### 이벤트 객체의 상속 구조

<img src="https://github.com/mobi-community/mobi-2th-book-study/assets/134191817/7be0e5c5-4a6a-4e3c-8f46-dfe33535a70c" />

<br />

### 이벤트 객체의 공동 프로퍼티

<table>
    <tr>
        <td>common props</td>
        <td>desc</td>
        <td>type</td>
    </tr>
    <tr>
        <td>type</td>
        <td>이벤트 타입</td>
        <td>string</td>
    </tr>
    <tr>
        <td>target</td>
        <td>이벤트를 발생시킨 돔 요소</td>
        <td>DOM element node</td>
    </tr>
    <tr>
        <td>currentTarget</td>
        <td>이벤트 핸들러가 바인딩 된 돔 요소</td>
        <td>DOM element node</td>
    </tr>
    <tr>
        <td>eventPhase</td>
        <td>이벤트 전파 단계<br />0: 이벤트 없음<br />1: 캡처링 단계 <br />2 : 타겟 단계 <br /> 3: 버블링 단계</td>
        <td>number</td>
    </tr>
    <tr>
        <td>bubbles</td>
        <td>이벤트를 버블링으로 전파하는지 여부. 다음 이벤트들은 버블링X (focus/blur, load/unload/abort/error, mousenter/mouseleave)</td>
        <td>boolean</td>
    </tr>
    <tr>
        <td>cancelable</td>
        <td>preventDefault 메서드를 호출해 이벤트의 기본 동작 취소 가능 여부. 다음 이벤트는 불가능 (focus/blur, load/unload/abort/error, delclick/mouseenter/mouseleave)</td>
        <td>boolean</td>
    </tr>
    <tr>
        <td>defaultPrevented</td>
        <td>preventDefault 메서드를 호출해 이벤트 취소했는지 여부 확인</td>
        <td>boolean</td>
    </tr>
    <tr>
        <td>isTrusted</td>
        <td>사용자의 행위에 의해 발생한 이벤트인지 여부 확인</td>
        <td>boolean</td>
    </tr>
    <tr>
        <td>timeStamp</td>
        <td>이벤트가 발생한 시각</td>
        <td>number</td>
    </tr>
</table>

<br />

### 이벤트 전파

<img src="https://github.com/mobi-community/mobi-2th-book-study/assets/134191817/aeb22893-ce82-44b8-ac4a-b3a5993402c4" />

<br />
