##### | 모던 자바스크립트 DeepDive <br />

###### range: 43. ajax <br />

###### date: day29 (2024.02.26) <br />

<hr />
<br />

## ajax

Ajax (Asynchronous JavaScript and XML)

자바스크립트를 사용해 브라우저가 서버에게 비동기 방식으로 데이터를 요청하고,
서버가 응답한 데이터를 수신해 웹페이지를 동적으로 갱신하는 프로그래밍 방식

Ajax는 브라우저에서 제공하는 Web API인 XMLHttpRequest 객체를 기반으로 동작하고, XMLHttpRequest는 HTTP 비동기 통신을 위한 메서드와 프로퍼티를 제공한다.

<br />

Ajax의 등장은 이전의 전통적인 패러다임을 획기전으로 전환.<br />
즉, 서버로부터 웹페이지의 변경에 필요한 데이터만 비동기 방식으로 전송ㅂ다아 웹페이지를 변경할 필요가 없는 부분은 다시 렌더링하지 않고, 변경할 필요가 있는 부분만 한정적으로 렌더링하는 방식이 가능해짐. <br />

이를 통해 빠른 퍼포먼스와 부드러운 화면 전환이 가능해짐. <br />

Ajax의 장점

    1. 변경할 부분을 갱신하는 데 필요한 데이터만 서버로부터 전송받아 불필요한 통신 X
    2. 변경하지 않아도 되는 부분은 렌더링 X (화면 깜빡임 현상 X)
    3. 클라이언트, 서버 간의 통신이 비동기적으로 동작하므로 서버에게 요청을 보낸 후 블로킹 X

<br />

### JSON

JSON(Javascript Object Notation)

클라이언트와 서버 간의 HTTP 통신을 위한 텍스트 데이터 포맷. <br />
자바스크립트에 종속되지 않는 언어 독립형 데이터 포맷이므로 대부분의 프로그래밍 언어에서 사용 가능.

<br />

#### 표기 방식

객체 리터럴과 유사하게 키와 값으로 구성된 순수한 텍스트.

```javascript
{
    "name" : "Jane Doe",
    "age" : 20,
    "hobby" : ["coding", "sleeping"],
    "alive" : true,
}
```

##### JSON.stringify

직렬화 : 객체/배열 → JSON 포맷의 문자열 <br />

##### JSON.parse

역직렬화 : JSON 포맷의 문자열 → 객체 <br />

##### XMLHttpRequest

자바스크립트를 사용해 HTTP 요청을 전송하려면 XMLHttpRequest 객체를 사용. <br />
