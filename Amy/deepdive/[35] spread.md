##### | 모던 자바스크립트 DeepDive <br />

###### range: 35. 스프레드 문법 <br />

###### date: day24 (2024.02.20) <br />

<hr />
<br />

### 스프레드 문법

스프레드 문법을 사용할 수 있는 대상은 for ... of 문으로 순회할 수 있는 이터러블에 한정됨. <br />
스프레드 문법의 결과는 값이 아니므로 이를 변수에 할당할 수 없다. <br />
스프레드 문법의 결과는 쉼표로 구분한 값의 목록으로 사용하는 문맥에서만 사용 가능하다. <br />

    - 함수 호출문의 인수 목록
    - 배열 리터럴의 요소 목록
    - 객체 리터럴의 프로퍼티 목록

<br />

### 함수 호출문의 인수 목록에서 사용하는 경우

요소들의 집합인 배열을 펼쳐서 개별적인 값들의 목록을 만든 후, 이를 함수의 인수 목록으로 전달해야 하는 경우가 있다.

```javascript
const arr = [1, 2, 3];
const max = Math.max(arr); // NaN
```

배열에서 가장 큰 수를 찾으려고 Math.max() 메서드를 사용했으나 결과로는 NaN이 출력된다. 이는 Math.max() 메서드에 숫자가 아닌 배열을 인수로 전달하면 최대값을 구할 수 없기 때문이다.

이 같은 문제를 해결하기 위해 배열을 펼쳐서 요소들을 개별적인 값들의 목록으로 만든 후 전달해야 한다.

스프레드 문법이 제공되기 이전에는 이럴 때 `Function.prototype.apply`를 사용했다. 스프레드 문법을 사용하면 더 간결하고 가독성 좋게 표현이 가능하다.

```javascript
const arr = [1, 2, 3];
const max = Math.max(null, ...arr);
```

<br />

⚠️ <br />
스프레드 문법은 Rest 파라미터와 형태가 동일해 혼동할 수 있으므로 주의가 필요. <br />
둘은 정 반대의 개념.

    Rest parameter
    함수에 전달된 인수들의 목록을 배열로 전달받기 위해 매개변수 이름 앞에 ...을 붙임

    function foo(...rest) {
        console.log(rest)
    }

    spread 문법
    이터러블을 펼쳐서 개별적인 값들의 목록을 만드는 것

    foo(...[1,2,3])

<br />

### 배열 리터럴 내부에서 사용하는 경우

#### concat

2개의 배열을 하나의 배열로 결합하고 싶은 경우 배열 리터럴만으로는 해결할 수 없어 concat 메서드를 사용해야 한다.

```javascript
let arr = [1, 2].concat([3, 4]);
```

스프레드 문법을 사용하면 별도의 메서드 사용 없이 결합이 가능하다.

```javascript
const arr = [...[1, 2], ...[3, 4]];
```

#### splice

배열의 중간에 다른 배열의 요소들을 추가하거나 제거하기 위해 splice 메서드를 사용한다.

```javascript
let arr1 = [1, 4];
let arr2 = [2, 3];

arr1.splice(1, 0, arr2);

// 기대한 결과 : [1,2,3,4]
// 출력될 결과 : [1,[2,3],4]
```

```javascript
arr1.splice(1, 0, ...arr2);
```

#### slice

배열을 복사할 때 사용하는 slice 메서드.

```javascript
let origin = [1, 2];
let copy1 = origin.slice();

let copy2 = [...origin]; // spread
```

#### 이터러블을 배열로 반환

이전에는 이터러블을 배열로 반환하기 위해 `Function.prototype.apply`, `Function.prototype.call` 메서드를 사용해 slice 메서드를 호출했다.

이제는 스프레드 문법을 통해 더 간편히 이터러블을 배열로 변환할 수 있다.

arguments 객체는 이터러블이면서 유사 배열 객체이므로 스프레드 문법의 대상이 될 수 있다.

```javascript
function sum() {
  // 이터러블이면서 유사배열 객체인 arguments를 배열로 반환
  return [...arguments].reduce((pre, cur) => pre + cur, 0);
}

// rest 파라미터 사용
const sum2 = (...args) => args.reduce((pre, cur) => pre + cur, 0);
```

단, 이터러블이 아닌 유사 배열 객체는 스프레드 문법의 대상 X
유사 배열 객체는 `Array.from` 메서드를 사용해야 한다.

<br />

### 객체 리터럴 내부에서 사용하는 경우

스프레드 문법의 대상은 이터러블이어야 하지만 스프레드 프로퍼티 제안은 일반 객체를 대상으로도 스프레드 문법의 사용을 허용한다.

```javascript
// spread property

// 객체 얕은 복사
const obj = { x: 1, y: 2 };
const copy = { ...obj };

// 객체 병합
const merged = { x: 1, y: 2, ...{ a: 3, b: 4 } };
```

스프레드 프로퍼티가 제안되기 이전에는 `Object.assign`메서드를 사용했다.
