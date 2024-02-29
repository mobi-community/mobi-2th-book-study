> ✏️제너레이터와 async/await

###### 코드블록의 실행을 일시 중지했다가 필요한 시점에 재개할 수 있는 특수한 함수

## 제너레이터란?

```
1️⃣ 제너레이터 함수는 함수 호출자에게 함수 실행의 제어권을 양도할 수 있다
2️⃣ 제너레이터 함수는 함수 호출자와 함수의 상태를 주고받을 수 있다
3️⃣ 제너레이터 함수를 호출하면 제너레이터의 객체를 반환한다
```


## 제너레이터 함수의 정의

제너레이터 함수는 `function*` 키워드로 선언 </br>
하나 이상의 _yield_ 표현식을 포함


## 제너레이터 객체

제너레이터 함수를 호출하면 일반 함수처럼 함수 코드 블록을 실행하는 것이 아니라</br>
제너레이터 객체를 생성해 반환한다

#### 제너레이터 함수가 반환한 제너레이터 객체는 이터러블 이면서 동시에 이터레이터이다.


##### generator.next()

제너레이터 함수의 yield 표현식까지 코드 블록을 실행하고 </br>
yield 된 값을 value 프로퍼티 값으로, </br>
false를 done프로퍼티 값으로 갖는 이터레이터 리절트 객체 반환

##### generator.return()

인수로 전달받은 값을 value 프로퍼티 값으로, </br>
true를 done 프로퍼티 값으로 갖는 이터레이터 리절트 객체를 반환

##### generator.throw()

인수로 전달받은 에러를 발생시키고, undefined를  value 프로퍼티 값으로, </br>
true를 done 프로퍼티 값으로 갖는 이터레이터 리절트 객체 반환



## 제너레이터의 일시 중지와 재개

제너레이터는 _yield_ 키워드와 _next_ 메서드를 통해 실행을 일시 중지했다가 필요한 시점에 다시 재개할 수 있다</br>
(일반 함수는 호출 이후 제어권을 함수가 독점, 제너레이터는 호출권 양도)

#### _yield_ :  제너레이터 함수의 실행을 일시 중지 시키거나, _yield_ 뒤에 오는 표현식의 평가 결과를 제너레이터 함수 호출자에게 반환

제너레이터 객체의 _next_ 메서드를 호출하면 _yield_ 표현식까지 실행되고 일시 중지. </br>
이때 함수의 제어권이 다시 호출자로 양도(yield)됨 </br>

이후 필요한 시점에 호출자가 또다시 _next_ 메서드를 호출하면 </br>
일시 중지된 코드부터 실행을 재개하기 시작하여 다음 _yield_ 표현식까지 실행되고 또 다시 일시 중지!

#### 제너레이터 객체 next 메서드는 `value, done` 프로퍼티를 갖는 이터레이터 리절트 객체를 반환
next메서드가 반환한 이터레이터 리절트 객체의 value 프로퍼티는  </br>
yield 표현식에서 yield된 값이 할당되고 

done 프로퍼티에는 제너레이터 함수가 끝까지 실행되었는지를 나타내는  </br>
불리언 값이 할당된다


## async/await

제너레이터보다 간단하고 가독성 좋게 비동기 처리를 동기처리처럼 동작하도록 구현하기 위해 도입됨

### async 함수
_await_ 키워드는 반드시 _async_ 내부에서 사용해야 한다</br>
명시적으로 프로미스를 반환하지 않더라도, 암묵적으로 반환값을 _resolve_ 하는 "프로미스"를 반환


### await 키워드
_await_ 은 프로미스가 settled 상ㅌ태가 될 때까지 대기하다 되면, 프로미스가 resolve한 처리 결과 res 변수에 할당

##### await 키워드는 반드시 프로미스 앞에서 사용해야한다

```jsx
const fetch = require("node-fetch");

const getGithubUserName = async (id) => {
  const res = await fetch(`https://api.github.com/users/${id}`); //1
  const { name } = await res.json(); //2
  console.log(name); //Kimi
};

getGithubUserName("Kimi");
```

_await_ 은 다음 실행을 일시 중지시켰다가 프로미스가 _settled_ 상태가 되면 다시 재개함


개별적으로 수행되는ㄴ 비도ㅗㅇ기 처리이므로 대기할 필요 없다. 이렇게 처리해주기

```jsx
async function foo() {
  const res = await Promise.all([
    new Promise((resolve) => setTimeout(() => resolve(1), 3000)),
    new Promise((resolve) => setTimeout(() => resolve(2), 2000)),
    new Promise((resolve) => setTimeout(() => resolve(3), 1000)),
  ]);

  console.log(res); // [1, 2, 3]
}

foo(); // 약 3초 소요
```


#### 순차적으로 비동기 처리를 수행해야하는 경우(앞선 비동기 처리 결과를 가지고 다음 비동기 처리 수행), _await_ 사용하기

```jsx
async function bar(n) {
  // 수행시 처리 결과가 필요하다
  const a = await new Promise((resolve) => setTimeout(() => resolve(1), 3000));
  const b = await new Promise((resolve) => setTimeout(() => resolve(2), 2000));
  const c = await new Promise((resolve) => setTimeout(() => resolve(3), 1000));

  console.log([a, b, c)); //[1,2,3]
}

bar(1); // 약 6초 소요
```


## 에러 처리

async/await에서 `try ... catch`문 사용하여 에러처리 할 수 있다</br>
콜백함수를 인수로 전달받는 비동기와는 달리 프로미스를 반환하는 비동기 함수는 </br>
명시적으로 호출할 수 있기때문에 **호출자가 명확하다**

##### async 함수 내에서 catch문을 사용하여 에러를 처리하지 않으려면 async 함수는 발생한 에러를 reject하는 프로미스 반환

```jsx
foo()
  .then(console.log)
  .catch(console.error); //TypeError: failed to fetch
```

