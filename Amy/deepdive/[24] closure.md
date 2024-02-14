##### | 모던 자바스크립트 DeepDive <br />

###### range: 24. 클로저 <br />

###### date: day19 (2024.02.14) <br />

<hr />
<br />

### Closure

클로저는 자바스크립트 고유의 개념X
함수를 일급 객체를 취급하는 함수형 프로그래밍 언에서 사용되는 중요한 특성

```javascript
const x = 1;

function outerFunc() {
  const x = 10;

  function innerFunc() {
    console.log(x); // 10
  }

  innerFunc();
}

outerFunc();
```

outer 함수 내부에서 중첩 함수 innerFunc가 정의되고 호출되었다. 이때 중첩 함수 innerFunc의 상위 스코프는 외부 함수 outerFunc의 스코프이다. 따라서 중첩 함수 innerFunc 내부에서 자신을 포함하고 있는 외부 함수 outerFunc의 x 변수에 접근할 수 있다.

만약 innerFunc 함수가 outerFunc 함수의 내부에서 정의된 함수가 아니라면 innerFunc 함수를 outerFunc 함수의 내부에서 호출한다 하더라도 outerFunc 함수의 변수에 접근할 수 없다.

이 같은 현상이 발생하는 이유는 자바스크립트가 렉시컬 스코프를 따르는 프로그래밍 언어이기 때문이다.

<br />

### 렉시컬 스코프

자바스크립트 엔진은 함수를 어디서 호출했는지가 아니라 함수를 어디에서 정의했는지에 따라 상위 스코프를 결정하는데 이를 렉시컬 스코프(정적 스코프)라고 한다.

```javascript
const x = 1;

function foo() {
  const x = 10;
  bar();
}

function bar() {
  console.log(x);
}

foo(); // 1
bar(); // 1
```

위의 예제를 보면 foo 함수와 bar 함수는 전역에서 정의된 함수이다.
함수의 상위 스코프는 함수를 어디서 정의했느냐에 따라 결정되므로 foo 함수와 bar 함수의 상위 스코프는 전역이다.
함수를 어디서 호출하는지는 함수의 상위 스코프 결정에 어떠한 영향도 주지 못한다.
즉, 함수의 상위 스코프는 함수를 정의한 위치에 의해 정적으로 결정되고 변하지 않는다.

실행 컨텍스트 에서 스코프의 실체는 실행 컨텍스트의 렉시컬 환경이다.
이 렉시컬 환경은 자신의 외부 렉시컬 환경에 대한 참조 를 통해 상위 렉시컬 환경과 연결되고 이를 바로 스코프 체인이라 한다.

따라서 **함수의 상위 스코프를 결정한다**는 것은 **렉시컬 환경의 외부 렉시컬 환경에 대한 참조에 저장할 참조값을 결정한다**는 것과 같다.
렉시컬 환경의 외부 렉시컬 환경에 대한 참조에 저장할 참조값이 바로 상위 렉시컬 환경에 대한 참조이며, 이것이 상위 스코프이기 때문이다.

렉시컬 스코프는 정리하면 렉시컬 환경의 외부 렉시컬 환경에 대한 참조에 저장할 참조값, 즉 **상위 스코프에 대한 참조는 함수 정의가 평가되는 시점에 함수가 정의된 환경(위치)에 의해 결정**된다.

<br />

### 함수 객체의 내부 슬롯 [[Environment]]

함수가 정의된 환경과 호출되는 환경은 다를 수 있다. 따라서 렉시컬 스코프가 가능하려면 함수는 자신이 호출되는 환경과는 상관없이 자신이 정의된 환경(상위 스코프)를 기억해야 한다. 이를 위해 함수는 자신의 내부 슬롯 [[Environment]]에 자신이 정의된 환경(상위 스코프)의 참조를 저장한다.

따라서 함수 객체에 내부 슬롯[[Environment]]에 저장된 현재 실행 중인 실행 컨텍스트의 렉시컬 환경의 참조가 바로 상위 스코프이다. 또한 자신이 호출되었을 때 생성될 함수 렉시컬 환경의 외부 렉시컬 환경에 대한 참조 에 저장될 참조값이다. 함수 객체는 내부 슬롯 [[Environment]]에 저장한 렉시컬 환경의 참조, 즉 상위 스코프로 자신이 존재하는 한 기억한다.

<br />

### 클로저와 렉시컬 환경

```javascript
const x = 1;

// 1️⃣
function outer() {
  const x = 10;
  const inner = function () {
    console.log(x);
  }; // 2️⃣
  return inner;
}

// outer 함수를 호출하면 중첩 함수 inner를 반환
// outer 함수의 실행 컨텍스트는 실행 컨텍스트 스택에서 팝 되어 제거
const innerFunc = outer(); // 43️⃣
innerFunc(); // 4️⃣ 10
```

위의 예제에서 outer 함수를 호출하면 outer 함수는 중첩 함수 inner를 반환하고 생명 주기를 마감한다.
즉, outer 함수의 실행이 종료되면 outer 함수의 실행 컨텍스트는 실행 컨텍스트 스택에서 제거된다.
이때 outer 함수의 지역 변수 x와 변수 값 10을 저장하고 있던 outer 함수의 실행 컨텍스트가 제거되었으므로 outer 함수의 지역 변수 x 또한 생명주기를 마감한다. 따라서 outer 함수의 지역 변수 x 는 더이상 유효하지 않게 되어 x 변수에 접근할 수 있는 방법은 달리 없어 보인다.

그러나 위 코드의 실행결과는 outer 함수의 지역 변수 x의 값인 10이다.
이미 생명 주기가 종료되어 실행 컨텍스트 스택에서 제거된 outer 함수의 지역 변수 x가 동작되고 있다.

이처럼 외부 함수보다 중첩 함수가 더 오래 유지되는 경우 중첩 함수는 이미 생명 주기가 종료한 외부 함수의 변수를 참조할 수 있다.
이러한 중첩 함수를 클로저라고 부른다.

> 클로저는 함수와 그 함수가 선언된 렉시컬 환경과의 조합이다.

자바스크립트의 모든 함수는 자신의 상위 스코프를 기억한다. 모든 함수가 기억하는 상위 스코프는 함수를 어디서 호출하든 상관없이 유지된다.
따라서 함수를 어디서 호출하든 상관없이 함수는 언제나 자신이 기억하는 상위 스코프의 식별자를 참조할 수 있으며 식별자에 바인딩된 값을 변경할 수도 있다.

위 예제에서 inner 함수는 자신이 평가될 때 자신이 정의된 위치에 의해 결정된 상위 스코프를 [[Environment]] 내부 슬롯에 저장한다.
이때 저장된 상위 스코프는 함수가 존재하는 한 유지된다.

위의 예제에서 1️⃣ outer 함수가 평가되어 함수 객체를 생성할 때
현재 실행 중인 실행 컨텍스트의 렉시컬 환경, 즉 전역 렉시컬 환경을 outer 함수 객체의 [[Environment]] 내부 슬롯 스코프로서 저장한다.

outer 함수를 호출하면 outer 함수의 렉시컬 환경이 생성되고 앞서 outer 함수 객체의 [[Environment]] 내부 슬롯에 저장된 전역 렉시컬 환경을 outer 함수 렉시컬 환경의 외부 렉시컬 환경에 대한 참조 에 할당한다.

2️⃣ 그리고 중첩 함수 inner가 평가된다.
이때 중첩 함수 inner는 자신의 [[Environment]] 내부 슬롯에 현재 실행중인 실행 컨텍스트의 렉시컬 환경, 즉 outer 함수의 렉시컬 환경을 상위 스코프로서 저장한다.

3️⃣ outer 함수의 실행이 종료하면 inner 함수를 반환하면서 outer 함수의 생명주기가 종료된다.
즉, outer 함수의 실행 컨텍스트가 실행 컨텍스트 스택에서 제거된다.
이때 outer 함수의 실행 컨텍스트는 실행 컨텍스트 스택에서 제거되지만 outer 함수의 렉시컬 환경까지 소멸하는 것은 아니다.

outer 함수의 렉시컬 환경은 inner 함수의 [[Environment]] 내부 슬롯에 의해 참조되고 있고 inner 함수는 전역 변수 innerFunc에 의해 참조되고 있으므로 가비지 컬렉션 대상이 아니기 때문이다.

4️⃣ outer 함수가 반환한 inner 함수를 호출하면
inner 함수의 실행 컨텍스트가 생성되고 실행 컨텍스트 스택에 푸쉬된다.
그리고 렉시컬 환경의 외부 렉시컬 환경에 대한 참조는 inner 함수 객체의 [[Environment]] 내부 슬롯에 저장되어 있는 참조값이 할당된다.

중첩 함수 inner는 외부 함수 outer보다 더 오래 생존했다.
이때 외부 함수보다 더 오래 생존한 중첩 함수는 외부 함수의 생존 여부와 상관없이 자신의 정의된 위치에 의해 결정된 상위 스코프를 기억한다.
이처럼 중첩 함수 inner의 내부에서는 상위 스코프를 참조할 수 있으므로 상위 스코프의 식별자를 참조할 수 있고 식별자의 값도 변경할 수도 있다.

클로저는 중첩 함수가 상위 스코프의 식별자를 참조하고 있고 중첩 함수가 외부 함수보다 더 오래 유지되는 경우에 한정하는 것이 일반적이다.

클로저에 의해 참조되는 상위 스코프의 변수를 자유 변수라고 부른다. 클로저란 함수가 자유 변수에 의해 닫혀있다라는 뜻이다.

이론적으로 클로저는 상위 스코프를 기억해야 하므로 불필요한 메모리 점유를 걱정할 수도 있다.
하지만 모던 자바스크립트 엔진은 클로저가 참조하고 있지 않는 식별자는 기억하지 않는다.

<br />

### 클로저의 활용

클로저는 상태를 안전하게 변경하고 유지하기 위해 사용한다. 다시 말해 상태가 의도치 않게 변경되지 않도록 **상태를 안전하게 은닉**하고 **특정 함수에게만 상태 변경을 허용하기 위해 사용**한다.

```javascript
const counter = function () {
  // 카운트 상태 변수
  let num = 0;

  // 클로저인 메서드를 갖는 객체를 반환
  // 객체 리터럴은 스코프 생성 X
  // 따라서 아래 메서드들의 상위 스코프는 즉시 실행 함수의 렉시컬 환경
  return {
    // num: 0 👉 프로퍼티는 public 하므로 은닉 X
    increase() {
      return ++num;
    },
    decrease() {
      return num > 0 ? --num : 0;
    },
  };
};

console.log(counter.increase()); // 1
console.log(counter.increase()); // 2

console.log(counter.decrease()); // 1
console.log(counter.decrease()); // 0
```

즉시 실행함수는 한 번만 실행되므로 increase 가 호출될 때마다 num 변수가 재차 초기화 될 일이 없다.
위의 예제의 increase, decrease 메서드의 상위 스코프는 increase, decrease 메서드가 평가되는 시점에 실행중인 실행 컨텍스트인 즉시 실행 함수 실행컨텍스트의 렉시컬 환경이다.

```javascript
// 함수를 인수로 전달받고 함수를 반환하는 고차 함수
// 이 함수는 카운트 상태를 유지하기 위한 자유 변수 counter를 기억하는 클로저를 반환
function makeCounter(predicate) {
  // 카운트 상태를 유지하기 위한 자유 변수
  let counter = 0;

  // 클로저를 반환
  return function () {
    // 인수로 전달받은 보조 함수에 상태 변경을 위임
    counter = predicate(counter);
    return counter;
  };
}

// 보조 함수
function increase(n) {
  return ++n;
}

// 보조 함수
function decrease(n) {
  return --n;
}

// 함수로 함수를 생성
// makeCounter 함수는 보조 함수를 인수로 전달받아 함수를 반환
const increaser = makeCounter(increase); // 1
console.log(increaser()); // 1
console.log(increaser()); // 2

// increaser 함수와는 별개로 독립된 렉시컬 환경을 갖기 때문에 카운터 상태가 연동 X
const decreaser = makeCounter(decrease); // 2
console.log(decreaser()); // -1
console.log(decreaser()); // -2
```

makeCounter 함수를 호출해 함수를 반환할 때 반환된 함수는 자신만의 독립된 렉시컬 환경을 갖는다.
전역 변수 increaser 와 decreaser 에 할당된 함수는 각각 자신만의 독립된 렉시컬 환경을 갖기 때문에 카운트를 유지하기 위한 자유 변수 counter 를 공유하지 않아 카운터의 증감이 연동되지 않는다.
따라서 독립된 카운터가 아니라 연동하여 증감이 가능한 카운터를 만들려면 렉시컬 환경을 만들려면 렉시컬 환경을 공유하는 클로저를 만들어야 한다.

```javascript
// 함수를 반환하는 고차 함수
// 이 함수는 카운트 상태를 유지하기 위한 자유 변수 counter를 기억하는 클로저를 반환
const counter = (function () {
  // 카운트 상태를 유지하기 위한 자유 변수
  let counter = 0;

  // 함수를 인수로 전달받는 클로저를 반환
  return function (predicate) {
    // 인수로 전달받은 보조 함수에 상태 변경을 위임
    counter = predicate(counter);
  	return counter;
  };
}());


// 보조 함수
function increase(n) {
  return ++n;
}

// 보조 함수
function decrease(n) {
  return --n;
}

// 함수로 함수를 전달하여 호출
console.log(counter(increase()); // 1
console.log(counter(increase()); // 2

// 자유 변수를 공유
console.log(counter(decrease()); // 1
console.log(counter(decrease()); // 0
```

<br />

### 캡슐화와 정보 은닉

캡슐화는 **객체의 상태를 나타내는 프로퍼티와 프로퍼티를 참조하고 동작할 수 있는 동작인 메서드를 하나로 묶은 것**을 말한다.
**캡슐화는 객체의 특정 프로퍼티나 메서드를 감출 목적으로 사용**하기도 하는데 이를 **정보 은닉**이라 한다.

자바스크립트 객체의 모든 프로퍼티와 메서드는 기본적으로 외부에 공개되어 있다.

```javascript
function Person(name, age) {
  this.name = name; // public
  let _age = age; // private

  // 인스턴스 메서드
  this.sayHi = function () {
    console.log(`Hi My name is ${this.name}. I am ${_age}`);
  };
}

const me = new Person(`Lee`, 20);
me.sayHi(); // Hi! My name is Lee. I am 20

console.log(me.name); // Lee
console.log(me._age); // undefined
```

위의 예제 name 프로퍼티는 외부로 공개되어 있어서 참조와 변경이 자유롭다. 즉 name 프로퍼티는 public 하다.
하지만 \_age 변수는 Person 생성자 함수의 지역 변수이므로 Person 생성자 함수 외부에서 참조하거나 변경할 수 없다.
즉, \_age 변수는 private 하다.

```javascript
const Person = (function () {
  let _age = 0; // private

  // 생성자 함수
  function Person(name, age) {
    this.name = name; // public
    _age = age;
  }

  // 프로토타입 메서드
  Person.prototype.sayHi = function () {
    console.log(`Hi! My name is ${this.name}. I am ${_age}.`);
  };

  // 생성자 함수를 반환
  return Person;
})();

const me = new Person("Lee", 20);
me.sayHi(); // Hi! My name is Lee. I am 20.
console.log(me.name); // Lee
console.log(me._age); // undefined
```

정보 은닉이 가능한 것처럼 보이지만, Person 생성자 함수가 여러 개의 인스턴스를 생성할 경우 \_age 변수의 상태가 유지되지 않는다.

```javascript
const me = new Person("Lee", 20);
me.sayHi(); // Hi! My name is Lee. I am 20.

const you = new Person("Kim", 30);
you.sayHi(); // Hi! My name is Kim. I am 30.

// _age 변수 값이 변경
my.sayHi(); // Hi! My name is Lee. I am 30
```

이는 `Person.prototype.sayHi` 메서드가 단 한 번 생성되는 클로저이기 때문에 발생하는 현상이다.
`Person.prototype.sayHi` 메서드는 즉시 실행 함수가 호출될 때 생성된다.

이처럼 자바스크립트는 정보 은닉을 완벽하게 지원하지 않는다.
