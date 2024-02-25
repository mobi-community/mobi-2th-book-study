##### | 모던 자바스크립트 DeepDive <br />

###### range: 38. 브라우저의 렌더링 과정 <br />

###### date: day25 (2024.02.22) <br />

<hr />
<br />

웹 애플리케이션의 클라이언트 사이드 자바스크립트는 브라우저에서 HTML, CSS와 함께 실행된다. 따라서 브라우저 환경을 고려할 때 더 효율적인 클라이언트 사이드 자바스크립트 프로그래밍이 가능하다.

### 브라우저 렌더링 과정

1. 렌더링에 필요한 리소스를 요청하고 서버로부터 응답

2. 브라우저의 렌더링 엔진은 서버로부터 응답된 HTML, CSS를 파싱해 DOM, CSSOM을 생성하고 결합해 렌더 크리 생성

3. 브라우저의 렌더링 엔진은 서버로부터 응답된 JS를 파싱해 AST를 생성 후 바이트코드로 변환해 실행 <br />
   이때 JS는 DOM API를 통해 DOM이나 CSSOM 변경 가능 (변경된 경우 렌더 트리로 재결합)

4. 렌더 트리를 기반으로 HTML 요소의 레이아웃을 계산, 브라우저 화면에 HTML 요소를 페인팅

<br />

파싱(parsing)

    파싱은 플그래밍 언어의 문법에 맞게 작성된 텍스트 문서를 읽어 실행하기 위해 텍스트 문서의 문자열을 토큰으로 분해하고 문법적 의미와 구조를 반영해 트리 구조의 자료구조인 파스 트리를 생성하는 일련의 과정.

    일반적으로 파싱이 완료된 후에는 파스 트리를 기반으로 중간 언어인 바이트코드를 생성하고 실행.

렌더링(rendering)

HTML, CSS, JS로 작성된 문서를 파싱해 브라우저에 시각적으로 출력하는 것

<br />

### 요청과 응답

브라우저의 핵심 기능 : 필요한 리소스를 서버에 요청하고 서버로부터 응답받아 브라우저에 시각적으로 렌더링하는 것. <br />

즉, 렌더링에 필요한 리소스는 모두 서버에 존재하므로 필요한 리소스를 서버에 요청하고 서버가 응답한 리소스를 파싱해 렌더링하는 것. <br />

##### 서버에게 데이터를 요청하는 방법

1️⃣ 주소창

    서버는 루트 요청에 의해 서버의 루트 폴더에 존재하는 정적 파일(index.html)을 클라이언트로 응답.

    만약 index.html이 아닌 다른 정적 파일을 서버에 요청하려면 브라우저의 주소창에 요청할 정적 파일의 경로와 파일 이름을 URI의 호스트 뒤에 path에 기술해 요청하도록 한다.

2️⃣ JavaScript

    자바스크립트를 통해 동적으로 서버에 정적/동적 데이터를 요청할 수도 있는데 이는 43.ajax와 44.REST API에서 자세히 다룰 예정

<br />

### HTTP 1.1 , 2.0

HTTP : 웹에서 브라우저와 서버가 통신하기 위한 프로토콜(규약)

- HTTP/1.1

  커넥션당 하나의 요청과 응답만 처리
  요청할 리소스의 개수에 비례해 응답 시간도 증가

- HTTP/2.0

  커넥션당 여러 개의 요청과 응답 가능
  1.1에 비해 페이지 로드 속도가 약 50% 빠르다고 알려짐

<br />

### HTML 파싱과 DOM 생성

브라우저의 렌더링 엔진은 응답받은 HTML 문서를 파싱해 브라우저가 이해할 수 있는 자료구조인 DOM을 생성한다.
즉, DOM은 HTML 문서를 파싱한 결과물이다.

<br />

### CSS 파싱과 CSSOM 생성

서버로부터 css 파일이 응답되면 렌더링 엔진은 html과 동일한 해석 과정을 거쳐 css를 파싱해 cssom을 생성한다.

<br />

### 렌더 트리 생성

렌더링 엔진은 서버로부터 응답된 html, css를 파싱해 각각 DOM, CSSOM을 생성한다. 그리고 DOM, CSSOM은 렌더링을 위해 렌더 트리로 결합된다.

렌더 트리는 렌더링을 위한 트리 구조의 자료구조이다.
따라서 브라우저 화면에 렌더링되지 않는 노드와 css에 의해 비표시되는 노드들은 포함하지 않는다.

즉, 렌더 트리는 브라우저 화면에 렌더링되는 노드만으로 구성돼 있다.

이후 완성된 렌더 트리는 각 HTML 요소의 레이아웃을 계산하는데 사용되며 브라우저 화면에 픽셀을 렌더링하는 페인팅 처리에 입력된다.

<br />

### 자바스크립트 파싱과 실행

자바스크립트 코드에서 DOM API를 사용하면 이미 생성된 DOM을 동적 조작할 수 있다.

자바스크립트 파싱과 실행은 브라우저의 렌더링 엔진이 아닌 자바스크립트 엔진이 실행하다. 자바스크립트 엔진은 자바스크립트 코드를 파싱해 CPU가 이해할 수 있는 저수준의 언어로 변환하고 실행하는 역할을 한다.

렌더링 엔진이 HTML, CSS를 파싱해 DOM, CSSOM을 생성하듯 자바스크립트 엔진은 자바스크립트를 해석해 AST를 생성한다.

<br />

토크나이징

    단순한 문자열인 자바스크립트 소스코드를 어휘 분석해 토큰들로 분해하는 과정.
    렉싱이라고 부르기도 함.

파싱

    토큰들의 집합을 구문 분석해 AST를 생성한다. AST를 사용하면 TS, babel, prettier 같은 트랜스파일러 구현도 가능하다.

바이트코드 생성과 실행

    파싱의 결과물로서 생성된 AST는 인터프리터가 실행할 수 있는 중간 코드인 바이트코드로 변환되고 인터프리터에 의해 실행된다.
    만약 코드의 사용 빈도가 적어지면 다시 디옵티마이징하기도 한다.

<br />

### 리플로우와 리페인트

만약 자바스크립트 코드에 DOM, CSSOM을 변경하는 DOM API가 사용된 경우 DOM이나 CSSOM이 변경된다. 이때 변경된 DOM과 CSSOM은 다시 렌더 트리로 결합되고 변경된 렌더 트리를 기반으로 레이아웃과 페인트 과정을 거쳐 브라우저의 화면에 다시 렌더링된다.

이를 리플로우, 리페인트라고 한다.

reflow

    레이아웃 계산을 다시 하는 것.
    노드 추가/삭제, 요소의 크기/위치 변경, 윈도우 리사이징 등 레이아웃에 영향을 주는 변경이 발생한 경우에 한해 실행된다.

repaint

    재결합된 렌더 트리를 기반으로 다시 페인트하는 것.

<br />

### 자바스크립트 파싱에 의한 HTML 파싱 중단

브라우저가 동기적으로(순차적으로) HTML, CSS, JS를 파싱하고 실행한다.<br />

이는 script 태그의 위치에 따라 HTML 파싱이 블로킹되어 DOM 생성이 지연될 수 있다는 것을 의미한다. 따라서 script 태그의 위치는 중요한 의미를 갖는다.

body 요소 가장 아래에 자바스크립트를 위치하는 것이 좋은 아이디어인데 그 이유는 아래와 같다 :

- dom이 완성되지 않은 상태에서 자바스크립트가 dom을 조작하면 에러가 발생할 우려가 있음

- 자바스크립트 로딩/파싱/실행으로 인해 html 요소들의 렌더링에 지장받는 일이 발생하지 않아 페이지 로딩 시간이 단축됨

<br />

### script 태그의 async/defer attr.

- async

  html 파싱과 외부 자바스크립트 파일의 로드가 비동기적으로 동시에 실행.
  자바스크립트의 파싱과 실행은 자바스크립트 파일의 로드가 완료된 직후 진행되며 이때 html 파싱이 중단됨.

  여러 개의 script 태그에 async 어트리뷰트를 지정하면 script태그의 순서와는 상관없이 로드가 완료된 자바스크립트부터 먼저 실행.(순서 보장 X)

- defer

  마찬가지로 html 파싱과 자바스크립트 파일의 로드가 비동기적으로 동시에 진행.
  단, 자바스크립트의 파싱과 실행은 html 파싱이 완료된 직후(dom 생성 완료 직후) 진행. 따라서 dom 생성이 완료된 이후 실행돼야 할 자바스크립트에 유용.