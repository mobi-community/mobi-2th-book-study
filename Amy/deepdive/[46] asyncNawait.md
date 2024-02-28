##### | 모던 자바스크립트 DeepDive <br />

###### range: 46. 제너레이터와 async/await <br />

###### date: day31 (2024.02.28) <br />

<hr />
<br />

### 제너레이터란?

ES6에서 도입된 제너레이터(generator)는 코드 블록의 실행을 일시 중지했다가 필요한 시점에 재개할 수 있는 특수한 함수다. 제너레이터와 일반 함수의 차이는 다음과 같다.

1️⃣ 제너레이터 함수는 함수 호출자에게 함수 실행의 제어권을 양도할 수 있다. <br />
제너레이터는 함수 호출자가 함수 실행을 일시 중지시키거나 재개시킬 수 있다. 이는 함수의 제어권을 함수가 독점하는 것이 아니라 함수 호출자에게 양도(yield)할 수 있다는 것을 의미한다.

2️⃣ 제너레이터 함수는 함수 호출자와 함수의 상태를 주고받을 수 있다. <br />
제너레이터 함수는 함수 호출자에게 상태를 전달할 수 있고 함수 호출자로부터 상태를 전달받을 수도 있다.

3️⃣ 제너레이터 함수를 호출하면 제너레이터 객체를 반환한다. <br />
제너레이터 함수를 호출하면 함수 코드를 실행하는 것이 아니라 이터러블이면서 동시에 이터레이터인 제너레이터 객체를 반환한다.

<br />

### 제너레이터 함수의 정의

제너레이터 함수는 function\* 키워드로 선언한다. 그리고 하나 이상의 yield 표현식을 포함한다. 이것을 제외하면 일반 함수를 정의하는 방법과 같다.

```javascript
// 제너레이터 함수 선언문
function* genDecFunc() {
  yield 1;
}

// 제너레이터 함수 표현식
const genExpFunc = function* () {
  yield 1;
};

// 제너레이터 메서드
const obj = {
  *genObjMethod() {
    yield 1;
  },
};

// 제너레이터 클래스 메서드
class MyClass {
  *genClsMethod() {
    yield 1;
  }
}
```

애스터리스크(\*) 의 위치는 function 키워드와 함수 이름 사이라면 어디든지 상관없다. 하지만 일관성을 유지하기 위해 function 키워드 바로 뒤에 붙이는 것을 권장한다.

```javascript
function* genFunc() {
  yield 1;
}

function* genFunc() {
  yield 1;
}

function* genFunc() {
  yield 1;
}

function* genFunc() {
  yield 1;
}
```

```javascript
// 제너레이터 함수는 화살표 함수로 정의 불가
const genArrowFunc = * () => {
  yield 1;
}; // SyntaxError: Unexpected token '*'
```

```javascript
// 제너레이터 함수는 new 연산자와 함께 생성자 함수로 호출 불가
function* genFunc() {
  yield 1;
}
new genFunc(); // TypeError: genFunc is not a constructor
```

<br />

### 제너레이터 객체

제너레이터 함수를 호출하면 일반 함수처럼 함수 코드 블록을 실행하는 것이 아니라 제너레이터 객체를 생성해 반환한다. 제너레이터가 반환한 제너레이터 객체는 이터러블(iterable)이면서 동시에 이터레이터(iterator)다.

다시 말해, 제너레이터 객체는 Symbol.iterator 메서드를 상속받는 이터러블이면서 value, done 프로퍼티를 갖는 이터레이터 리절트 객체를 반환하는 next 메서드를 소유하는 이터레이터다.

제너레이터 객체는 next 메서드를 가지는 이터레이터이므로 Symbol.iterator 메서드를 호출해서 별도로 이터레이터를 생성할 필요가 없다.

```javascript
// 제너레이터 함수
function* genFunc() {
  yield 1;
  yield 2;
  yield 3;
}

// 제너레이터 함수를 호출하면 제너레이터 객체를 반환한다.
const generator = genFunc();

// 제너레이터 객체는 이터러블이면서 동시에 이터레이터다.
// 이터러블은 Symbol.iterator 메서드를 직접 구현하거나 프로토타입 체인을 통해 상속받은 객체다.
console.log(Symbol.iterator in generator); // true
// 이터레이터는 next 메서드를 갖는다.
console.log("next" in generator); // true
```

제너레이터 객체는 next 메서드를 갖는 이터레이터이지만 이터레이터에는 없는 return,throw 메서드를 갖는다. 제너레이터 객체의 세 개의 메서드를 호출하면 다음과 같이 동작한다.

1️⃣ next 메서드를 호출하면 제너레이터 함수의 yield 표현식까지 코드 블록을 실행하고 이터레이터 리절트 객체를 반환한다.

2️⃣ return 메서드를 호출하면 인수로 전달받은 값을 value 프로퍼티 값으로, true를 done 프로퍼티 값으로 갖는 이터레이터 리절트 객체를 반환한다.

```javascript
function* genFunc() {
  try {
    yield 1;
    yield 2;
    yield 3;
  } catch (e) {
    console.error(e);
  }
}

const generator = genFunc();

console.log(generator.next()); // {value: 1, done: false}
console.log(generator.return("End!")); // {value: "End!", done: true}
```

throw 메서드를 호출하면 인수로 전달받은 에러를 발생시키고 undefined를 value 프로퍼티 값으로, true를 done 프로퍼티 값으로 갖는 이터레이터 리절트 객체를 반환한다.

```javascript
function* genFunc() {
  try {
    yield 1;
    yield 2;
    yield 3;
  } catch (e) {
    console.error(e);
  }
}

const generator = genFunc();

console.log(generator.next()); // {value: 1, done: false}
console.log(generator.throw("Error!")); // {value: undefined, done: true}
```

<br />

### 제너레이터의 일시 중지와 재개

제너레이터는 yield 키워드와 next 메서드를 통해 실행을 일시 중지했다가 필요한 시점에 다시 재개할 수 있다.

일반 함수는 호출 이후 제어권을 해당 함수가 독점하지만, 제너레이터는 함수 호출자에게 제어권을 양도(yield)하여 필요한 시점에 함수 실행을 재개할 수 있다.

next 메서드를 통해 제너레이터를 실행할 경우, 코드 블록 내에 yield 키워드 뒤에 오는 표현식의 평가 결과를 제너레이터 함수 호출자에게 리절트 객체형식으로 반환한다.

```javascript
// 제너레이터 함수
function* genFunc() {
  yield 1;
  yield 2;
  yield 3;
}

// 제너레이터 함수를 호출하면 제너레이터 객체를 반환한다.
// 이터러블이면서 동시에 이터레이터인 제너레이터 객체는 next 메서드를 갖는다.
const generator = genFunc();

console.log(generator.next()); // {value: 1, done: false}
console.log(generator.next()); // {value: 2, done: false}
console.log(generator.next()); // {value: 3, done: false}
console.log(generator.next()); // {value: undefined, done: true}
```

제너레이터 객체의 next 메서드를 호출하면 yield 표현식까지 실행되고 일시 중지된다. 이때 함수의 제어권이 다시 호출자로 양도(yield)된다. 이후 필요한 시점에 홏출자가 또다시 next 메서드를 호출하면 일시 중지된 코드부터 실행을 재개하기 시작하여 다음 yield 표현식까지 실행되고 또 다시 일시 중지된다.

리절트 객체 { value : , done : }를 반환하는데, yield 표현식이 끝까지 실행될 경우 value 에는 undefined를, done 은 true인 리절트 객체를 반환하고 종료된다.

<br />

### async/await

위와 같은 방법으로 제너레이터를 사용해서 비동기 처리를 마치 동기처럼 동작하도록 구현할 수 있다. 하지만 코드가 무척이나 장황해지고 가독성도 나빠졌다.

ES8에서는 제너레이터보다 간단하고 가독성 좋게 비동기 처리를 동기 처리처럼 동작하도록 구현할 수 있는 async/await가 도입되었다.

**async/await는 프로미스를 기반으로 동작**한다.

async/await를 사용하면 프로미스의 then/catch/finally 등의 후속 처리 메서드에 콜백 함수를 전달해서 비동기 처리 결과를 후속 처리할 필요 없이 **마치 동기 처리처럼 프로미스를 사용**할 수 있다.

다시 말해, 프로미스의 후속 처리 메서드 없이 마치 동기 처리처럼 **프로미스가 처리 결과를 반환하도록 구현**할 수 있다.

### async

1️⃣ await 키워드는 반드시 async 함수 내부에서 사용해야 한다.

2️⃣ async 함수는 async 키워드를 사용해 정의하며 언제나 프로미스를 반환한다.

3️⃣ async 함수가 명시적으로 프로미스를 반환하지 않더라도 async 함수는 암묵적으로 반환 값을 resolve하는 프로미스를 반환한다.

```javascript
// async 함수 선언문
async function foo(n) {
  return n;
}
foo(1).then((v) => console.log(v)); // 1

// async 함수 표현식
const bar = async function (n) {
  return n;
};
bar(2).then((v) => console.log(v)); // 2

// async 화살표 함수
const baz = async (n) => n;
baz(3).then((v) => console.log(v)); // 3

// async 메서드
const obj = {
  async foo(n) {
    return n;
  },
};
obj.foo(4).then((v) => console.log(v)); // 4

// async 클래스 메서드
class MyClass {
  async bar(n) {
    return n;
  }
}
const myClass = new MyClass();
myClass.bar(5).then((v) => console.log(v)); // 5
```

클래스의 constructor(생성자 함수) 메서드는 async 메서드가 될 수 없다. 클래스의 constructor는 인스턴스를 반환해야 하지만 async 함수는 언제나 프로미스를 반환해야 한다.

```javascript
class MyClass {
  async constructor() { }
  // SyntaxError: Class constructor may not be an async method
}

const myClass = new MyClass();
```

<br />

### await

await 키워드는 프로미스가 settled 상태(비동기 처리가 수행된 상태)가 될 때까지 대기하다가 settled 상태가 되면 프로미스가 resolve한 처리 결과를 반환한다. await 키워드는 반드시 프로미스 앞에서 사용해야 한다.

```javascript
const fetch = require("node-fetch");

const getGithubUserName = async (id) => {
  const res = await fetch(`https://api.github.com/users/${id}`); // ①
  const { name } = await res.json(); // ②
  console.log(name); // Amy
};

getGithubUserName("Amy");
```

모든 프로미스에 await 키워드를 사용하는 것은 주의해야 한다. 위 예제의 foo 함수는 호출부터 종료까지 약 6초가 소요된다. await 키워드를 사용한다면, 각 프로미스의 상태가 settled 될 때까지 기다리기 때문이다.

이것이 의도한 것이라면 상관없지만, 3개의 비동기 처리는 서로 연관이 없이 개별적으로 수행되는 비동기처리 이므로 앞선 비동기 처리가 완료될 때까지 대기해서 순차적으로 처리할 필요가 없다.

```javascript
async function foo() {
  const res = await Promise.all([
    new Promise((resolve) => setTimeout(() => resolve(1), 3000)),
    new Promise((resolve) => setTimeout(() => resolve(2), 2000)),
    new Promise((resolve) => setTimeout(() => resolve(3), 1000)),
  ]);

  console.log(res); // [1, 2, 3]
}

foo(); // 약 3초 소요된다.
```

<br />

### 에러 처리

비동기 처리를 위한 콜백 패턴의 단점 중 가장 심각한 것은 에러 처리가 곤란하다는 것이다. 에러는 호출자(caller) 방향으로 전파된다. 즉, 콜 스택의 아래 방향(실행 중인 실행 컨텍스트가 푸시되기 직전에 푸시된 실행 컨텍스트 방향)으로 전파된다. 하지만 비동기 함수의 콜백 함수를 호출한 것은 비동기 함수가 아니기 때문에 try ... catch 문을 사용해 에러를 캐치할 수 없다.

```javascript
try {
  setTimeout(() => {
    throw new Error("Error!");
  }, 1000);
} catch (e) {
  // 에러를 캐치하지 못한다!
  console.error("캐치한 에러", e);
}
```

async/await에서 에러 처리는 try ... catch 문을 사용할 수 있다. 콜백 함수를 인수로 전달받는 비동기 함수와는 달리 프로미스를 반환하는 **비동기 함수는 명시적으로 호출할 수 있기 때문에 호출자가 명확**하다.

```javascript
const fetch = require("node-fetch");

const foo = async () => {
  try {
    const wrongURL = "https://wrong.url";
    const response = await fetch(wrongURL);
    const data = await response.json();
    console.log(data);
  } catch (err) {
    console.error(err); // TypeError : Failed to fetch
  }
};
foo();
```

위 예제의 함수의 catch 문은 HTTP 통신에서 발생한 네트워크 에러뿐 아니라 try 코드 블록 내의 모든 문에서 발생한 일반적인 에러까지 모두 캐치할 수 있다.
