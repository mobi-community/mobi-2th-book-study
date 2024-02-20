##### | 모던 자바스크립트 DeepDive <br />

###### range: 34. 이터러블 <br />

###### date: day24 (2024.02.20) <br />

<hr />
<br />

### 이터레이션 프로토콜

순회 가능한 데이터 컬렉션을 만들기 위한 약속된 규칙 <br />

ES6 : 순회 가능한 데이커 컬렉션을 이터레이션 프로토콜을 준수하는 이터러블로 통일해 for...of문, 스프레드 문법, 배열 디스트럭처링 할당의 대상으로 사용할 수 있게 일원화. <br />

이터러블 프로토콜

    well-known Symbol인 Symbol.iterator를 프로퍼티 키로 사용한 메서드를 직접 구현하거나 프로토타입 체인을 통해 상속받은 Symbol.iterator를 호출하면 이터레이터 프로토콜을 준수한 이터레이터 반환.
    이런 규약을 이터러블 프로토콜이라 하며 이터러블 프로토콜을 준수한 객체를 이터러블이라 한다.

이터레이터 프로포콜

    이터러블의 Symbol.iterator를 호출하면 이터레이터 프로토콜을 준수한 이터레이터를 반환. 이터레이터는 next 메서드를 소유하며 이를 호출하면 이터러블을 순회하며 value와 done 프로퍼티를 갖는 이터레이터 리절트 객체를 반환.
    이러한 규약을 이터레이터 프로토콜이라 하며 이터레이터 프로초콜을 주수한 객체를 이터레이터라 한다.

<br />

#### 이터러블

이터러블 프로토콜을 준수한 객체 = 이터러블 <br />
Symbol.iterator를 프로퍼티 키로 사요앟ㄴ 메서드를 직접 구현하거나 프로토타입 체인을 통해 상속받은 객체.

```javascript
// 이터러블인지 확인하는 함수
const isIterable = (v) =>
  v !== null && typeof v[Symbol.iterator] === "function";
```

<br />

#### 이터레이터

이터레이터의 next 메서드는 이터러블의 각 요소를 순회하기 위한 포인터의 역할. <br />
next 메서드를 호출하면 이터레이터 리절트 객체를 반환. <br />

리절트 객테의 value 프로퍼티는 현재 순회 중인 이터벌의 값을, done 프로퍼티는 이터러블의 순화 완료 여부를 나타낸다.

<br />

### 빌트인 이터러블

<table>
    <tr>
        <td>built-in iterable</td>
        <td>Symbol.iterator method</td>
    </tr>
    <tr>
        <td>Array</td>
        <td>Array.prototype[Symbol.iterator]</td>
    </tr>
    <tr>
        <td>String</td>
        <td>String.prototype[Symbol.iterator]</td>
    </tr>
    <tr>
        <td>Map</td>
        <td>Map.prototype[Symbol.iterator]</td>
    </tr>
    <tr>
        <td>Set</td>
        <td>Set.prototype[Symbol.iterator]</td>
    </tr>
    <tr>
        <td>TypedArray</td>
        <td>TypedArray.prototype[Symbol.iterator]</td>
    </tr>
    <tr>
        <td>arguments</td>
        <td>arguments[Symbol.iterator]</td>
    </tr>
    <tr>
        <td rowspan="2">Dom collection</td>
        <td>NodeList.prototype[Symbol.iterator]</td>
    </tr>
    <tr>
        <td>HTMLCollection.prototype[Symbol.iterator]</td>
    </tr>
</table>

<br />

### for ... of 문

`for (변수 선언문 of 이터러블) { .... }`

for of문은 내부적으로 이터레이터의 next 메서드를 호출해 이터러블을 순회. <br />
next 메서드가 반환한 이터레이터 리절트 객체의 value 프로퍼티 값을 변수에 할당. <br />

`for (변수 선언문 in 객체) { .... }`

for in문은 객체의 프로토타입 중 프로퍼티 어트리뷰트의 [[Enumberable]] 값이 true인 프로퍼티를 순회하며 열거.

<br />

### 이터러블과 유사배열 객체

유사배열 객체 :

    배열처럼 인덱스로 프로퍼티 값에 접근 가능
    Length 프로퍼티를 갖기 때문에 for문 순회 가능
    일반 객체 (이터러블 X)

    단, 예외 존재 : arguments, NodeList, HTMLCollection

<br />

### 이터레이션 프로토콜의 필요성

이터레이션 프로토콜을 준수하는 이터러블 데이터 소스 목록 :

    Array, String, Map, Set, TypedArray, arguments

이터러블은 for ...of문, 스프레드 문법, 배열 디스트럭처링 할당과 같은 데이터 소비자에 의해 사용되므로 데이터 공급자의 역할을 한다고 볼 수 있다.

데이터 공급자가 이터레이션 프로토콜을 준수하도록 규정하면 데이터 소비자는 이터레이션 프로토콜만 지원하도록 구현하면 된다.

즉, 이터러블을 지원하는 데이터 소비자는 내부에서 Symbol.iterator 메서드를 호출해 이터레이터를 생성하고 이터레이터의 next 메서드를 호출해 이터러블을 순회하며 이터레이터 리절트 객체를 반환한다. 그리고 이러레이터 리절트 객체의 value/done 프로퍼티 값을 취득한다.

이터레이션 프로토콜은 다양한 공급자가 하나의 순회 방식을 갖도록 규정해 데이터 소비자가 효율적으로 다양한 데이터 공급자를 사용할 수 있도록 **데이터 소비자와 데이터 공급자를 연결하는 인터페이스의 역할**

<br />

### 사용자 정의 이터러블

#### 무한 이러터블과 지연 평가

지연 평가

    데이터가 필요한 시점 이전까지는 미리 데이터를 생성하지 않다가 데이터가 필요한 시점이 되면 그때야 비로소 데이터를 생성하는 기법

지연 평가를 사용하면 불필요한 데이터를 미리 생성하지 않고 필요한 데이터를 필요한 순간에 생성하므로 빠른 실행 속도를 기대할 수 있고 불필요한 메모리 소비를 막을 수 있다. <br />
무한도 표현이 가능하다.

```javascript
// 무한 이터러블을 생성하는 함수 피보나치
const fibonacciFunc = function () {
  let [pre, cur] = [0, 1];

  // Symbol.iterator 메서드와 next 메서드를 소유한 이터러블이면서 이터레이터인 객체 반환
  return {
    [Symbol.iterator]() {
      return this;
    },
    // next 메서드는 이터레이터 리절트 객체를 반환
    next() {
      [pre, cur] = [cur, pre + cur];
      // 무한 구현 위해 done 생략
      return { value: cur };
    },
  };
};

// fibonacciFunc는 무한 이터러블 생성하게 됨
for (const num of fibonacciFunc()) {
  if (num > 10000) break; // 1 3 5 8 ... 4181 6765
  console.log(num);
}

// 배열 디스트럭처링 할당을 통해 무한 이터러블에서 3개의 요소만 취득 가능
const [f1, f2, f3] = fibonacciFunc();

console.log(f1, f2, f3); // 1 2 3
```
