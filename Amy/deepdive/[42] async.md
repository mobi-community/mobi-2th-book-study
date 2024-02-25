##### | 모던 자바스크립트 DeepDive <br />

###### range: 42. 비동기 프로그래밍 <br />

###### date: day28 (2024.02.25) <br />

<hr />
<br />

## 비동기 프로그래밍

자바스크립트 엔진은 싱글 스레드 방식으로 동작하며, 하나의 콜스택을 가집니다.

그렇기 때문에 태스크들이 여러 개 있더라도 순차적으로 하나씩 태스크를 처리하는데 이를 동기 처리라고 합니다.

동기 처리: 현재 실행 중인 태스크가 종료할 때까지 다음에 실행될 태스크가 대기하는 방식

- 장점 : 태스크를 순서대로 하나씩 처리하기 때문에 실행 순서가 보장된다.

- 단점 : 태스크가 하나씩 처리되기 때문에 앞선 태스크가 시간이 오래 걸리는 경우 블로킹이 발생한다.

<br />

```javascript
// sample
function foo() {
  console.log("foo");
}

function bar() {
  console.log("bar");
}

setTimeout(foo, 3 * 1000);
bar(); // blocking X
```

[ 실행 순서 ]

1. 전역 코드가 평가 되어 전역 실행 컨텍스트가 생성되고 콜 스택(실행 컨텍스트 스택)에 푸시

2. 전역 실행 컨텍스트 실행

3. setTimeout 함수가 호출되고, setTimeout 함수의 함수 실행 컨텍스트가 생성되고 콜 스택에 push

4. setTimeout 함수가 실행되고, 콜 스택에서 pop

이때, 브라우저에서 타이머가 만료를 기다리다가 만료되면 태스크 큐에 콜백함수를 푸시

5. bar 함수가 호출되어 콜 스택에 push → 실행 종료 후 콜 스택에서 pop

6. 전역 실행 컨텍스트가 pop

7. 이때 콜 스택에 처리할 태스크가 없기 때문에 이벤트 루프에 의해 태스크 큐에서 대기 중인 foo가 콜 스택에 push

8. foo 실행 컨텍스트가 콜스택에 push → 실행 후 콜스택에서 pop

<br />

`태스크 큐`
비동기 함수의 콜백 함수 또는 이벤트 핸들러가 일시적으로 보관되는 영역

프로미스의 후속 처리 메서드(then, catch, finally)는 마이크로태스크 큐에 보관되며 우선순위는 마이크로태스크 큐가 더 높다.

<br />

`이벤트 루프`
콜 스택을 관찰하다가 비어있으면, 태스크 큐에 대기 중인 함수를 체크하고 있다면 콜스택으로 이동시킨다.

이처럼 비동기 처리는 브라우저에서 병행 처리 되기 때문에 블로킹이 발생하지 않고 동시에 태스크를 수행하는 것처럼 보입니다.

<br />

`비동기 처리`
현재 실행 중인 태스크가 종료되지 않은 상태라 해도 다음 태스크를 곧바로 실행한다.

- 장점: 블로킹이 발생하지 않는다.
- 단점: 태스크의 실행 순서가 보장되지 않는다.

<br />

⚠️ 타이머 함수인 setTimeout, setInterval, HTTP 요청, 이벤트 핸들러는 비동기 처리 방식으로 동작