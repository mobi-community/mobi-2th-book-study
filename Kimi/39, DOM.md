> ✏️DOM

###### HTML 문서의 계층적 구조와 정보를 표현
###### 이를 제어할 수 있는 API, 즉 프로퍼티와 메서드를 제공하는 트리 자료구조


# 노드

### HTML 요소와 노드 객체

HTML요소는 문서를 구성하는 개별적인 요소들을 의미함

![image](https://github.com/mobi-community/mobi-2th-book-study/assets/134191815/5d1650aa-fa78-47b3-94d1-f714bc85dbb6)

HTML 요소의 어트리뷰트는 > 어트리뷰트 노드로, </br>
텍스트 콘텐츠는 > 텍스트 노드로 변환됨


##### 트리 자료구조
노드 객체들로 구성된 트리자료구조를 DOM이라고 한다. (=DOM트리)

![image](https://github.com/mobi-community/mobi-2th-book-study/assets/134191815/59f5a74d-62de-4303-8e0c-f2aa8cd94b2f)


### 노드 객체의 상속 구조

![image](https://github.com/mobi-community/mobi-2th-book-study/assets/134191815/d115bdff-7af7-495e-94bd-1e0eff38b388)

DOM은 HTML문서의 계층적 구조와 정보를 표현</br>
노드 객체의 종류, 노드 타입에 따라 필요한 기능을 프로퍼티와 메서드의 집합인 DOM API로 제공 </br>
이 DOM API를 통해 HTML구조놔 내용 또는 스타일 등을 동적으로 조작.


## 요소 노드 취득

### id를 이용한 요소 노드 취득

##### document.protype.getElementById

```jsx
<body>
  <ul>
      <li id="apple">Apple</li>
      <li id="banana">Banana</li>
      <li id="orange">Orange</li>
  </ul>
</body>
<script>
  const $elem = document.getElementById('banana');

  //취득한 요소 노드의 style.color 프로퍼티 값 변경
  $elem.style.color = 'red';
</script>
```


### 태그 이름을 이용한 요소 노드 취득

##### document.prototype.getElemnetsByTagName

인수로 전달한 태그 이름을 갖는 모든 요소 노드들 탐색하여 반환

```jsx
<body>
  <ul>
      <li id="apple">Apple</li>
      <li id="banana">Banana</li>
      <li id="orange">Orange</li>
  </ul>
</body>
<script>
  //HTMLCollection 객체는 유사 배열 객체이면서 이터러블
  //모든 요소를 취득하려면 ('*')를 전달
  const $elem = document.getElemnetsByTagName('li');

  //취득한 모든 요소 노드의 style.colorr 프로퍼티 값 변경
  //HTMLCollection 객체를 배열로 변환하여 순회하며 color프로퍼티 값 변경
  [...$elems].forEach(elem => { elem.style.color = 'red' });
</script>
```


### class를 이용한 요소 노드 취득

##### Document.prortotype.getElementsByClassName



### CSS 선택자를 이용한 요소 노드 취득
```css
/*input요소 중이 type어트리뷰트 값이 'text'인 요소 모두 선택*/
input[type=text] {...}

/*후손 선택자: div요소의 후손 요소중 p 요소 모두 선택*/
div p {...}

/*인접 형제 선택자: p요소의 자식 요소중 p요소 모두 선택*/
div > p {...}

/*인접 형제 선택자: p 요소의 형제 요소 중에 p요소 바로 뒤에 위치하는 ul요소 선택*/
p + ul {...}

/*일반 형제 선택자: p요소의 형제 요소 중에 p요소 뒤에 위치하는 ul요소를 모두 선택*/
p ~ ul {...}

/*가상 클래스 선택자: hover 상태인 a요소 모두 선택*/
a:hover {...}

/*가상 요소 선택자: p요소의 콘텐츠의 앞에 위치하는 공간을 선택
일반적으로 content 프로퍼티와 함께 사용됨 */
p::before {...}
```

##### document.prototype.querySelector
인수로 전달한 css선택자를 만족시키는 요소 노드가 여러 개인 경우 첫 번째 요소 노드만 반환


##### document.prototype.querySelectorAll
인수로 전달한 CSS선택자를 만족시키는 모든 요소 노드를 탐색하여 반환


## 요소 노드의 텍스트 조작

### textContent
```jsx
<body>
  <div id="foo">Hello <span>World!</span></div>
</body>
<script>
  console.log(document.getElementById('foo').textContent); //Hello World!
  document.getElementById('foo').innerContent = 'Hi <span>there!</span>'
</script>
```

## DOM 조작

### innerText
```jsx
<body>
  <div id="foo">Hello <span>World!</span></div>
</body>
<script>
  console.log(document.getElementById('foo').innerHTML); //"Hello <span>World!</span>"
  document.getElementById('foo').innerHTML = 'Hi <span>there!</span>'
</script>
```

## 어트리뷰트
```jsx
<body>
  <input id="user" type="text" value="kimi">
</body>
<script>
  const { attributes } = document.getElementById('user');
  console.log(attributes);

  //어트리뷰트 값 취득
  console.log(attributes.id.value); //user
  console.log(attributes.type.value); //text
  cosnole.log(attributes.value.value); //kimi
</script>
```









