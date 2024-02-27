> ✏️Ajax

# Ajax란?
자바스크립트를 사용하여 브라우저가 서버에게 비동기 방식으로 데이터를 요청하고, </br>
서버가 응답한 데이터를 수신하여 웹페이지를 동적으로 갱신하는 프로그래밍 방식

###### Ajax는 브라우저에서 제공하는 WebAPI인 XMLHttpRequest 객체를 기반으로 동작한다.
###### XMLHttpRequest는 HTTP비동기 통신을 위한 메서드와 프로퍼티를 제공한다.

### ■ Ajax(Asynchronous Javascript And XML) 등장 배경

- 웹 브라우저의 정보 요청에 서버는 해당 정보를 포함한 전체 페이지를 전달했다.

- 브라우저와 서버는 매번 전체 페이지를 렌더링, 생성해야 했기에 부담이 되었다.

* Ajax를 사용하지 않는 사이트가 특유의 깜빡거림 현상을 보이는 이유는 매번 페이지를 싹 지우고

  처음부터 렌더링 하기 때문이다.

 

### ■ Ajax(Asynchronous Javascript And XML) 역사

- 1999.3  개념이 정립되어 IE5에 등장하였지만, 윈도우에 탑재된 ActiveX를 거쳐 사용해야 했기에 성능 문제로

  잘 사용되지 않았다.

- 2004.4  구글이 발표한 GMail과 구글 지도가 플러그인 없이 Ajax로 구현된 Web App이라는 사실이 밝혀진 열흘 후,

  Jesse James Garret에 의해 Ajax라는 용어로 불려 고유 명사로 굳어졌다.

* axios나 oboe등 라이브러리는 비동기 HTTP 요청을 전문적으로 처리한다.


서버로부터 웹페이지의 변경에 필요한 데이터만 비동기 방식으로 전송받아</br>
웹 페이지를 변경할 필요가 없는 부분은 다시 랜더링하지 않고, </br>
변경할 필요가 있는 부분만 한저적으로 랜더링하는 방식이 가능해짐


이를 통해 브라우저에서도 데스크톱 애플리케이션과 유사한 빠른 퍼포먼스와 부드러운 화면 전환이 가능해짐


```
Ajax의 장점

1. 변경할 부분을 갱신하는 데 필요한 데이터만 서버로부터 전송받기 때문에 불필요한 데이터 통신 발생X
2. 변경할 필요 없는 부분은 다시 랜더링X => 화면이 순간적으로 깜빡이는 현상 발생X
3. 클라이언트와 서버와의 통신이 비동기적으로 동작하여 서버에게 요청을 보낸 이후 블로킹(작업 중단) 발생X 
```

# JSON
클라이언트와 서버간의 HTTP 통신을 위한 텍스트 데이터 포맷

### JSON 표기 방식
자바스크립트의 객체 리터럴과 유사하게 키와 값으로 구성된 순수한 텍스트
```json
{
  "name": "Lee",
  "age": 20,
  "hobby": ["soccer", "tennis"]
}
```


##### JSON.stringfy
이 메서드는 객체를 JSON 포맷의 문자열로 변환 </br>
클라이언트가 서버로 객체를 전송하려면 객체를 문자열화해야 하는데 이를 직렬화라고 한다.

객체 뿐만아니라 배열도 JSON 포맷의 문자열로 변환 가능


##### JSON.parse
반대로 문자열을 객체로 변환</br>
문자열을 객체로서 사용하려면 JSON 포맷의 문자열을 객체화해야하는데 이를 역직렬화 라고한다.


# XMLHttpRequest
브라우저는 주소창이나 HTML의 form 태그 또는 a태그를 통해 HTTP요청 전송 기능을 기본 제공</br>
자바스크립트를 사용하여 HTTP 요청을 전송하려면 `XMLHttpRequest` 객체를 사용한다.

### HTTP 요청 전송
1. XMLHttpRequest.prototype.open 메서드로 HTTP요청 초기화
2. 필요에따라 XMLHttpRequest.prototype.setRequestHeader 메서드로 특정 HTTP 요청의 헤더값 설정.
3. XMLHttpRequest.prototype.send 메서드로 HTTP 요청 전송

```jsx
//XMLHttpRequest 객체 생성
const xhr = new XMLHttpRequest();

//HTTP요청 초기화
xhr.open('GET', '/users');

//HTTP 요청 헤더 설정
//클라이언트가 서버로 전송할 데이터의 MINE타입 지정: json
xhr.setRequestHeader('content-type', 'application/josn');

//HTTP 요청 전송
xhr.send();
```

![image](https://github.com/mobi-community/mobi-2th-book-study/assets/134191815/d4d0792a-def5-408c-9bfa-45ed3600cad5)
