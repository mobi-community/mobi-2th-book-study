##### | 모던 자바스크립트 DeepDive <br />

###### range: 45. 프로미스 <br />

###### date: day30 (2024.02.27) <br />

<hr />
<br />

## 비동기 처리를 위한 콜백 패턴의 단점

### 콜백 헬

콜백 함수 호출이 중첩되어 복잡도가 높아지는 현상이 발생

```javascript
const get = (url) => {
  const xhr = new XMLHttpRequest();
  xhr.open("GET", url);
  xhr.send();

  xhr.onload = () => {
    if (xhr.status === 200) {
      console.log(JSON.parse(xhr.response));
    } else {
      console.error(`${xhr.status} ${xhr.statusText}`);
    }
  };
};
get("https://jsonplaceholder.typicode.com/posts/1");
```

비동기함수

- 함수 내부에 비동기로 동작하는 코드를 포함한 함수
- 처리 결과를 외부로 반환하거나 상위 스코프의 변수에 할당하면 기대한 대로 동작 X

<br />

### 에러 처리의 한계

```javascript
try {
  setTimeout(() => {
    throw new Error("Error!");
  }, 1000);
} catch (e) {
  console.error("캐치한 에러", e);
}
```

1️⃣ 콜백 패턴의 심각한 문제점, 에러 처리가 곤란하다는 것 <br />
2️⃣ 에러는 호출자 방향으로 전파 <br /> - setTimeout 함수의 콜백함수를 호출한 것은 setTimeout 함수 X <br /> - catch 블록에서 캐치 X

<br />

### 프로미스 생성

**프로미스는 비동기 처리 상태와 처리 결과를 관리하는 객체**

```javascript
// 프로미스 생성
const promise = new Promise((resolve, reject) => {
    // Promise 함수의 콜백 함수 내부에서 비동기 처리를 수행
    if (...) resolve('result');
    else reject('failure reason');
});
```

```javascript
const promiseGet = (url) => {
  return new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest();
    xhr.open("GET", url);
    xhr.send();

    xhr.onload = () => {
      if (xhr.status === 200) resolve(JSON.parse(xhr.response));
      else reject(new Error(xhr.status));
    };
  });
};

// promiseGet 함수는 프로미스를 반환
promiseGet("https://jsonplaceholder.typicode.com/posts/1");
```

<table>
    <tr>
        <td>promise 상태 정보</td>
        <td>의미</td>
        <td>상태 변경 조건</td>
    </tr>
    <tr>
        <td>pending</td>
        <td>비동기 처리가 아직 수행되지 않은 상태</td>
        <td>프로미스가 생성된 직후 기본 상태</td>
    </tr>
    <tr>
        <td>fulfilled</td>
        <td>비동기 처리가 수행된 상태(성공)</td>
        <td>resolve 함수 호출</td>
    </tr>
    <tr>
        <td>rejected</td>
        <td>비동기 처리가 수행된 상태(실패)</td>
        <td>reject 함수 호출</td>
    </tr>
</table>

<br />

- 프로미스의 상태는 resolve 또는 reject함수를 호출 하는 것으로 결정
- 비동기 처리 성공 : resolve 함수를 호출해 프로미스를 fulfilled 상태로 변경
- 비동기 처리 실패 : reject 함수를 호출해 프로미스를 rejected 상태로 변경
- fullfilled 또는 rejected 상태를 settled 상태라고 함
- settled 상태가 되면 다른 상태로 변화 X
- 비동기 처리 상태와 더불어 비동기 처리 결과도 상태로 갖음

<br />

### 프로미스의 후속 처리 메서드

프로미스의 비동기 처리 상태가 변화하면 후속 처리 메서드에 인수로 전달한 콜백 함수가 선택적으로 호출 <br />
모든 후속 처리 메서드는 프로미스를 반환하며, 비동기로 동작 <br />

<br />

1️⃣ Promise.prototype.then

두 개의 콜백 함수를 인수로 전달 받는다.

1. 프로미스가 fulfilled 상태가 되면 호출, 성공 처리 콜백 함수
2. 프로미스가 rejected 상태가 되면 호출, 실패 처리 콜백 함수

```javascript
// fulfilled
new Promise((resolve) => resolve("fulfilled")).then(
  (v) => console.log(v),
  (e) => console.error(e)
);

// rejected
new Promise((_, reject) => reject(new Error("rejected"))).then(
  (v) => console.log(v),
  (e) => console.error(e)
);
```

<br />

2️⃣ Promise.prototype.catchPermalink

한 개의 콜백 함수를 인수로 전달 받는다. <br />

1. 프로미스가 rejected 상태인 경우 호출 <br />

```javascript
// rejected
new Promise((_, reject) => reject(new Error("rejected"))).catch((e) =>
  console.error(e)
);
```

then(undefined, onRejected)와 동일하다.

<br />

3️⃣ Promise.prototype.finally

한 개의 콜백 함수를 인수로 전달 받는다.

1. 프로미스의 성공 또는 실패와 상관없이 무조건 한 번 호출

```javascript
new Promise(() => {}).finally(() => console.log("finally"));
```

상태와 상관없이 공통적으로 수행해야 할 처리 내용이 있을 때 유용

<br />

### 프로미스의 에러 처리

1️⃣ catch <br />
catch 메서드를 호출하면 내부적으로 then(undefined, onRejected)을 호출한다. <br />
단, then 메서드의 두 번째 콜백 함수는 첫 번째 콜백 함수에서 발생한 에러를 캐치하지 못하고, 코드가 복잡해져서 가독성이 좋지 않다. <br />
catch 메서드를 모든 then 메서드를 호출한 이후에 호출하면 then 메서드 내부에서 발생한 에러까지 모두 캐치할 수 있다.

<br />

### 프로미스 체이닝

then, catch, finally 후속 처리 메서드는 항상 프로미스를 반환하므로 연속적으로 호출할 수 있다.

<table>
    <tr>
        <td>후속 처리 메서드</td>
        <td>콜백 함수의 인수</td>
        <td>후속 처리 메서드의 반환값</td>
    </tr>
    <tr>
        <td>then</td>
        <td>promiseGet 함수가 반환한 프로미스가 resolve한 값(id가 1인 post)</td>
        <td>콜백 함수가 반환한 프로미스</td>
    </tr>
    <tr>
        <td>then</td>
        <td>첫 번째 then메서드가 반환한 프로미스가 resolve한 값(post의 userId로 취득한 user 정보)</td>
        <td>콜백 함수가 반환한 값(undefined)을 resolve한 프로미스</td>
    </tr>
    <tr>
        <td>catch (* 에러X, 호출X)</td>
        <td>promiseGet 함수 또는 앞선 후속 처리 메서드가 반환한 프로미스가 reject한 값</td>
        <td>콜백 함수가 반환한 값(undefined)을 resolve한 프로미스</td>
    </tr>
<table>

- es8에서 도입된 async/await 를 통해 해결 가능

<br />

### 프로미스의 정적 메서드

1️⃣ Promise.resolve / Promise.reject

이미 존재하는 값을 래핑하여 프로미스를 생성하기 위해 사용

```javascript
// 배열을 resolve하는 프로미스를 생성
const resolvePromise = Promise.resolve([1, 2, 3]);
resolvePromise.then(console.log);

const resolvePromise = new Promise((resolve) => resolve([1, 2, 3]));
resolvePromise.then(console.log);
```

```javascript
// 에러 객체를 reject하는 프로미스를 생성
const rejectedPromise = Promise.reject(new Error("Error"));
rejectedPromise.catch(console.log);

const rejectedPromise = new Promise((_, reject) => reject(new Error("Error")));
rejectedPromise.catch(console.log);
```

<br />

2️⃣ Promise.all

여러 개의 비동기 처리를 모두 병렬 처리할 때 사용

```javascript
const requestData1 = () =>
  new Promise((resolve) => setTimeout(() => resolve(1), 3000));
const requestData2 = () =>
  new Promise((resolve) => setTimeout(() => resolve(2), 2000));
const requestData3 = () =>
  new Promise((resolve) => setTimeout(() => resolve(3), 1000));

// 세 개의 비동기 처리를 순차적으로 처리
const res = [];
requestData1()
  .then((data) => {
    res.push(data);
    return requestData2();
  })
  .then((data) => {
    res.push(data);
    return requestData3();
  })
  .then((data) => {
    res.push(data);
    console.log(res);
  })
  .catch(console.error);
```

세 개의 비동기 처리를 순차적으로 처리 → 총 6초 이상 소요 <br />
각 비동기 처리는 서로 의존하지 않고 개별적으로 수행 → 순차적으로 처리 할 필요가 없음

```javascript
Promise.all([requestData1(), requestData2(), requestData3()])
  .then(console.log)
  .catch(console.error);
```

전달받은 모든 프로미스가 fulfilled 상태가 되면 모든 처리 결과를 배열에 저장해 새로운 프로미스를 반환.

첫 번째 프로미스가 가장 나중에 fulfilled 상태가 되어도 첫 번째 프로미스가 resolve한 처리 결과부터 차례대로 배열에 저장. 처리 순서가 보장.

프로미스가 하나라도 rejected 상태가 되면 즉시 종료!

```javascript
Promise.all([
  new Promise((_, reject) =>
    setTimeout(() => reject(new Error("Error 1")), 3000)
  ),
  new Promise((_, reject) =>
    setTimeout(() => reject(new Error("Error 2")), 2000)
  ),
  new Promise((_, reject) =>
    setTimeout(() => reject(new Error("Error 3")), 1000)
  ),
])
  .then(console.log)
  .catch(console.error);
```

인수로 전달받은 이터러블의 요소가 프로미스가 아닌 경우 Promise.resolve 메서드를 통해 프로미스로 래핑

```javascript
Promise.all([
  1, // Promise.resolve(1)
  2, // Promise.resolve(2)
  3, // Promise.resolve(3)
])
  .then(console.log)
  .catch(console.error);
```

```javascript
const promiseGet = (url) => {
  return new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest();
    xhr.open("GET", url);
    xhr.send();

    xhr.onload = () => {
      if (xhr.status === 200) {
        resolve(JSON.parse(xhr.response));
      } else {
        reject(new Error(xhr.status));
      }
    };
  });
};

const githubIds = ["jeresig", "ahejlsberg", "ungmo2"];

Promise.all(
  githubIds.map((id) => promiseGet(`https://api.github.com/users/${id}`))
)
  .then((users) => users.map((user) => user.name))
  .then(console.log)
  .catch(console.error);
```

<br />

3️⃣ Promise.race

가장 먼저 fulfilled 상태가 된 프로미스의 처리 결과를 resolve하는 새로운 프로미스 반환 <br />
프로미스가 rejected 상태가 되면 Promise.all 메서드와 동일하게 처리

```javascript
Promise.race([
  new Promise((resolve) => setTimeout(() => resolve(1), 3000)),
  new Promise((resolve) => setTimeout(() => resolve(2), 2000)),
  new Promise((resolve) => setTimeout(() => resolve(3), 1000)),
])
  .then(console.log)
  .catch(console.error);
```

<br />

4️⃣ allSettled

프로미스를 요소로 갖는 배열 등의 이터러블을 인수로 전달 <br />
전달받은 프로미스가 모두 settled 상태(비동기 처리가 수행된 상태)가 되면 처리 결과를 배열로 반환

```javascript
Promise.allSettled([
  new Promise((resolve) => setTimeout(() => resolve(1), 2000)),
  new Promise((_, reject) =>
    setTimeout(() => reject(new Error("Error!")), 1000)
  ),
]).then(console.log);
```

<br />

### 마이크로태스크 큐

프로미스의 후속 처리 메서드의 콜백 함수는 태스크 큐가 아니라 마이크태스크 큐에 저장한다. <br />
**마이크로태스크 큐는 태스크 큐보다 우선순위가 높다.** <br />
이벤트 루프는 콜 스택이 비면 먼저 마이크로태스크 큐에서 대기하고 있는 함수를 가져와 실행한다.<br />
이후 마이크로태스크 큐가 비면 태스크 큐에서 대기하고 있는 함수를 가져와 실행한다.

<br />

### fetch

XMLHttpRequest 객체와 마찬가지로 HTTP 요청 전송 기능을 제공하는 클라이언트 사이드 Web API <br />
XMLHttpRequest 객체보다 사용법이 간단한고 프로미스를 지원 <br />

fetch 함수는 **HTTP 응답을 나타내는 Response 객체를 래핑한 Promise 객체를 반환** <br />

<br />
