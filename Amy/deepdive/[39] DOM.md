##### | 모던 자바스크립트 DeepDive <br />

###### range: 39. DOM <br />

###### date: day26 (2024.02.23) <br />

<hr />
<br />

## DOM

브라우저 렌더링 엔진은 HTML 문서를 파싱하여 브라우저가 이해할 수 있는 자료구조인 DOM을 생성한다.
DOM은 HTML 문서의 계층적 구조와 정보를 표현하며 이를 제어할 수 있는 API, 즉 프로퍼티와 메서드를 제공하는 트리 자료구조다.

<br />

### 노드의 객체 타입

`문서 노드 (document node)`

DOM 트리의 최상단에 존재하는 루트노드, document 객체 <br />
document 객체는 브라우저가 렌더링한 HTML 문서 전체를 가르킴 <br />
전역 객체의 document프로퍼티에 바인딩 → document로 참조 가능 <br />
최상단에 있기 때문에 DOM 트리의 노드들에 접근하기 위한 진입점 역할 <br />

`요소 노드 (element node)`

HTML 요소를 가르키는 객체 <br />
HTML 요소들의 중첩관계를 통해 문서의 구조를 표현

`어트리뷰트 노드 (attribute node)`

HTML 요소의 어트리뷰트를 가르키는 객체 <br />
어트리뷰트 노드는 해당 요소 노드에만 연결

`텍스트 노드 (text node)`
HTML 요소의 텍스트를 가르키는 객체 <br />
해당 요소 노드의 자식 노드이며 말단 노드

<br />

### 노드 객체의 상속 구조

<img src="https://github.com/mobi-community/mobi-2th-book-study/assets/134191817/d769f757-93fc-41c7-bc7b-42e530eaf8a1" />

<br />

### 요소 노드 취득

###### 4가지 방법

#### id를 이용한 요소 노드 취득

Document.prototype.getElementById 메서드로 취득 <br />
인수로 전달한 id 어트리뷰트 값과 일치하는 요소 노드를 반환 <br />
만약 해당 id를 갖는 요소가 여러개면 맨 처음 노드를 반환 <br />
일치하는 요소 노드가 없으면 null 반환

HTML 요소에 id 어트리뷰트를 부여하면 id값과 동일한 이름의 전역 변수가 암묵적으로 생성되고 해당 노드 객체가 할당되는 부수 효과 발생 <br />
만약 id값과 동일한 전역 변수가 이미 있으면 노드 객체 할당 X

```javascript
<!DOCTYPE html>
<html>
  <body>
    <ul>
      <li id="apple">Apple</li>
      <li id="banana">Banana</li>
      <li id="orange">Orange</li> <!--글씨 색깔 오렌지 -->
      <li id="orange">Orange2</li>
    </ul>
    <script>
      const $elem = document.getElementById('orange');
      $elem.style.color = 'orange';
      let apple = '사과';
      console.log(orange); // orange 노드 객체
      console.log(apple); // '사과'
      console.log(banana); // banana 노드 객체

    </script>
  </body>
</html>
```

#### 태그 이름을 이용한 요소 노드 취득

Document.prototype.getElementsByTagName 메서드로 취득 <br />
인수로 전달한 태그인 모든 요소 노드를 갖는 HTMLCollection 객체를 반환 <br />
해당 요소 노드가 없으면 빈 HTMLCollection 객체 반환 <br />
HTMLCollection 객체는 유사 배열 객체,이터러블임 <br />
모든 노드 선택시 '\*'

```javascript
<!DOCTYPE html>
<html>
  <body>
    <ul>
      <li id="apple">Apple</li> <!--글씨 색깔 보라색 -->
      <li id="banana">Banana</li> <!--글씨 색깔 보라색 -->
      <li id="orange">Orange</li> <!--글씨 색깔 보라색 -->
    </ul>
    <script>
      const $elems = document.getElementsByTagName('li');
      console.log($elems); // 모든 li 요소 노드를 갖는 HTMLCollection 객체
      [...$elems].forEach(x=>x.style.color = 'purple');
    </script>
  </body>
</html>
```

#### class를 이용한 요소 노드 취득

인수로 전달한 class 값을 갖는 모든 요소들을 갖는 HTMLCollection 객체를 반환 <br />

인수로 전달하는 class 값들은 공백으로 여러개의 class 지정 가능 <br />
`document.getElementsByClassName('food instant');` → class가 food인 요소 노드 + class가 instant인 요소 노드가 아니고 class가 food 와 instant 둘다 가지는 요소 노드를 탐색

- `Document.prototype.getElementsByClassName`
- `Element.prototype.getElementsByClassName`

#### CSS 선택자를 이용한 요소 노드 취득

인수로 전달한 CSS 선택자를 만족시키는 하나의 요소 노드를 반환, 없으면 null 반환

- `Document.prototype.querySelector`
- `Element.prototype.querySelector`

인수로 전달한 CSS 선택자를 만족하는 모든 노드를 구하려면

- `Document.prototype.querySelectorAll`
- `Element.prototype.querySelectorAll`

모든 요소 노드를 담은 NodeList 객체를 반환 <br />
NodeList 객체는 유사 배열 객체,이터러블임

<br />

### 특정 요소 노드를 취득할 수 있는지 확인

Element.prototype.matches 메서드 <br />
인수로 전달한 CSS 선택자로 해당 요소 노드를 취득할 수 있는지 true,false 반환 <br />
**이벤트 위임을 사용할 때 유용**

<br />

### HTMLCollection과 NodeList

`HTMLCollection`은 노드 객체의 상태 변화를 실시간으로 반영하는 살아 있는 객체 <br />

`NodeList`
querySelectorAll 메서드는 NodeList 객체를 반환 <br />
NodeList 객체는 실시간으로 노드 객체의 상태 변경을 반영하지 않는 non-live 객체 <br />
하지만 childNodes 프로퍼티가 반환하는 NodeList 객체는 live 객체임 <br />

<br />

### 노드 탐색

<img  src="https://github.com/mobi-community/mobi-2th-book-study/assets/134191817/534dfde2-5544-4d90-8bd7-2c320f03a3d5" />

<br />

`공백 텍스트 노드`

공백 문자(탭,줄바꿈 등)는 공백 텍스트 노드를 생성함 <br />
노드를 탐색할 때 공백 문자에 의해 생성된 공백 텍스트 노드 주의 <br />

`자식 노드 탐색`

- Node.prototype.childNodes : 텍스트 노드를 포함한 NodeList 객체 반환

- Element.prototype.children : 텍스트 노드 제외한 HTMLCollection 객체 반환

- Node.prototype.firstChild : 첫 번째 자식 노드 반환, 텍스트 노드 일수도

- Node.prototype.lastChild : 마지막 자식 노드 반환, 텍스트 노드 일수도

- Element.prototype.firstElementChild : 첫 번째 요소 자식 노드 반환

- Element.prototype.lastElementChild : 마지막 요소 자식 노드 반환

`자식 노드 존재 확인`

Node.prototype.hasChildNodes 메서드로 확인 (true,false 반환) <br />
텍스트 노드도 포함해서 자식 노드의 존재를 확인함 <br />
텍스트 노드 제외 하려면 children.length, childElementCount 프로퍼티로! <br />

`요소 노드의 텍스트 노드 탐색`

텍스트 노드는 요소 노드의 자식이기 때문에 firstChild 프로퍼티로 접근 가능

`부모 노드 탐색`

Node.prototype.parentNode 프로퍼티로 탐색

`형제 노드 탐색`

- Node.prototype.previousSibling : 텍스트 노드 포함 이전 형제 노드
- Node.prototype.nextSibling : 텍스트 노드 포함 다음 형제 노드
- Node.prototype.previousElementSibling : 이전 형제 요소 노드
- Node.prototype.nextElementSibling : 다음 형제 요소 노드

<br />

### 노드 정보 취득

```javascript
<!DOCTYPE html>
<html>
  <body>
    <div id="box">안녕하세요</div>
    <script>
      const $box= document.getElementById('box');
      const $textNode = $box.firstChild;
      console.log($box.nodeName,$box.nodeType); // DIV 1
      console.log(document.nodeName,document.nodeType); // #document 9
      console.log($textNode.nodeName,$textNode.nodeType); // #text 3
    </script>
  </body>
</html>
```

<br />

### 어트리뷰트

#### 어트리뷰트 노드와 attributes 프로퍼티

`<input id="user" type="text" value="user name">`

HTML 요소의 시작 태그에 어트리뷰트 이름 = "어트리뷰트 값" 형식으로 정의 <br />
HTML 문서가 파싱될 때 각각의 어트리뷰트는 각각의 어트리뷰트 노드로 변환 <br />
HTML 요소의 어트리뷰트가 3개이면 어트리뷰트 노드도 3개 <br />
모든 어트리뷰트 노드의 참조는 NamedNodeMap 객체에 담겨 요소 노드의 attributes 프로퍼티에 저장 <br />
attributes 프로퍼티는 getter만 있는 접근자 프로퍼티 <br />
값에 접근 하려면 요소.attributes.어트리뷰트명.value로 접근 <br />

```javascript
<!DOCTYPE html>
<html>
  <body>
    <input type="text" id="name" value="Aj">
    <script>
      const {attributes} = document.getElementById('name');
      console.log(attributes.id.value);
      console.log(attributes.type.value);
      console.log(attributes.value.value);
    </script>
  </body>
</html>
```

#### HTML 어트리뷰트 조작

attributes 프로퍼티를 통하지 않고 요소 노드에서 메서드로 바로 HTML 어트리뷰트 값 접근 가능

- Element.prototype.getAttribute(attributeName)
- Element.prototype.setAttribute(attributeName,attributeValue)
- Element.prototype.hasAttribute(attributeName)
- Element.prototype.removeAttribute(attributeName)

#### HTML 어트리뷰트 vs DOM 프로퍼티

요소 노드 객체에는 HTML 어트리뷰트에 대응하는 프로퍼티가 존재 <br />
이러한 DOM 프로퍼티들은 HTML 어트리뷰트 값을 초기값으로 갖고 있음 <br />
DOM 프로퍼티는 setter,getter 둘다 있는 접근자 프로퍼티 <br />

<br />

HTML 어트리뷰트 : HTML 요소의 초기 상태를 지정 <br />
DOM 프로퍼티 : 요소 노드의 최신 상태를 관리

요소 노드의 초기값과 최신값 모두 관리를 해줘야 한다.
단 모든 DOM 프로퍼티가 사용자 입력에 의해 변경된 최신 상태를 관리하지는 않는다.

<br />

### data 어트리뷰트와 dataset 프로퍼티

사용자 정의 어트리뷰트 <br />
data-사용자정의 어트리뷰트 이름 = "값" 형식으로 선언 <br />
HTMLElement.dataset 프로퍼티는 모든 data 어트리뷰트를 담은 DOMStringMap 객체 반환 <br />
DOMStringMap 객체는 사용자정의 어트리뷰트 이름을 카멜케이스로 변환한 프로퍼티를 갖는다 <br />

```javascript
<!DOCTYPE html>
<html>
  <body>
    <ul>
      <li data-user-id="1" data-sex="male">John Doe</li>
      <li data-user-id="2" data-sex="female">Jane Doe</li>
    </ul>
    <script>
      const users = [...document.querySelector('ul').children];
      const female = users.find(x => x.dataset.sex ==='female');
      console.log(female.textContent); // Jane Doe
      console.log(female.dataset.userId); // 2
    </script>
  </body>
</html>
```

<br />

### DOM 표준

HTML과 DOM 표준은 W3C와 WHATWG가 협력으로 공통된 표준을 만들어 왔으나 2018년부터 구글, 애플, 마이크로소프트, 모질라로 구성된 WHATWG가 단일 표준을 제공하기로 두 단체가 합의 <br />

DOM은 현재 4개의 버전이 있음 <br />
WHATWG(Web Hypertext Application Technology Working Group)
