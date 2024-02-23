##### | 모던 자바스크립트 DeepDive <br />

###### range: 36. 디스트럭처링 할당 <br />

###### date: day24 (2024.02.21) <br />

<hr />
<br />

## 구조 분해 할당

디스트럭처링 할당(destructuring assignment), 즉 구조 분해 할당은 구조화된 배열(이터러블, 객체 등)을 비구조화/구조 파괴해 1개 이상의 변수에 개별적으로 할당하는 것.

배열(이터러블, 객체 리터럴 등)에서 필요한 값만 추출해 변수헤 할당할 때 유용.

<br />

### 배열 구조 분해 할당

배열 구조 분해 할당의 대상(할당문의 우변)은 **이터러블**, 할당 기준은 **배열의 인덱스**이므로 순서대로 할당된다. <br />
이때 변수의 개수와 이터러블의 요소 개수가 반드시 일치할 필요는 없다.

<br />

배열 구조 분해 할당을 위한 변수에 기본값 설정 가능. <br />
이때 기본값보다는 할당된 값이 우선시된다. 기본값을 갖고 있는 상태에서 다른 값을 할당받으면 값이 덮어씌워진다.

```javascript
//default value
const [a, b, c = 3] = [1, 2];
cnosole.log(a, b, c); // 1,2,3
```

배열 구조 분해 할당은 배열(이터러블)에서 필요한 요소만 추출해 변수에 할당하고 싶을 때 유용하게 사용 가능하다.

URL을 파싱해 protocol, host, path 프로퍼티를 갖는 객체를 생성해 반환하는 함수를 만들 수도 있다.

```javascript
function parseURL(url = "") {
  /* 
        '://' 앞의 문자열(protocol)
        '/' 이전의 슬래시로 시작하지 않는 문자열(host)
        '/' 이후의 문자열(path)
    */
  const parsedURL = url.match(/^(\w+):\/\/([^/]+)\/(.*)$/);
  console.log(parsedURL);
  /* 
  console의 값은 아래와 같다 :
  'https://developer.mozilla.org/ko/docs/Web/JavaScript',
  'https', → protocol
  'developer.mozilla.org', → host
  'ko/docs/Web/JavaScript' → path
  index: 0,
  input: 'https://developer.mozilla.org/ko/docs/Web/JavaScript',
  groups: undefined
  */

  if (!parsedURL) return {};

  // 구조 분해 할당으로 이터러블에서 필요한 요소만 추출
  const [, protocol, host, path] = parsedURL;
  return { protocol, host, path };
}

const parsedURL = parsedURL(
  "https://developer.mozilla.org/ko/docs/Web/JavaScript"
);
console.log(parsedURL);

/* 
    {
        protocol: 'https',
        host: 'developer.mozilla.org',
        path: 'ko/docs/Web/JavaScript'
    }
*/
```

배열 구조 분해 할당을 위해 변수에 Rest 파라미터와 유사하게 Rest 요소 ...을 사용할 수 있다. Rest 요소는 Rest 파라미터와 마찬가지로 반드시 마지막에 위치해야 한다.

<br />

### 객체 구조 분해 할당

객체의 각 프로퍼티를 객체로부터 구조 분해하여 변수에 할당하기 위해선 프로퍼티 키를 사용해야 한다.

```javascript
const user = { firstName: "mobi", lastName: "Kim" };
const { firstName, lastName } = user;
```

객체 구조 분해 할당은 객체를 인수로 전달받는 함수의 매개변수에도 사용 가능하다.
<br />
배열의 요소가 객체인 경우 배열 구조 분해 할당과 객체 구조 분해 할당을 혼용할 수 있다.

```javascript
const todos = [
  { id: 1, content: "HTML", completed: true },
  { id: 1, content: "CSS", completed: false },
  { id: 1, content: "JS", completed: false },
];

// todos 배열의 두 번째 요소인 객체로부터 id만 추출
const [, { id }] = todos;
```
