##### | 모던 자바스크립트 DeepDive <br />

###### range: 18. 일급 객체 <br />

###### date: day14 (2024.01.00) <br />

<hr />
<br />

### 일급 객체

일급 객체의 조건

    무명의 리터럴로 생성 가능. 즉, 런타임에서 생성이 가능
    변수나 자료 구조에 저장이 가능
    함수의 매개 변수에 전달이 가능
    함수의 반환값으로 사용이 가능

```javascript
// 1. 함수는 무명의 리터럴로 생성할 수 있다.
// 2. 함수는 변수에 저장할 수 있다.
// 런타임(할당 단계)에 함수 리터럴이 평가되어 함수 객체가 생성되고 변수에 할당된다.
const increase = function (num) {
  return ++num;
};

const decrease = function (num) {
  return --num;
};

// 2. 함수는 객체에 저장할 수 있다.
const auxs = { increase, decrease };

// 3. 함수의 매개변수에게 전달할 수 있다.
// 4. 함수의 반환값으로 사용할 수 있다.
function makeCounter(aux) {
  let num = 0;

  return function () {
    num = aux(num);
    return num;
  };
}

// 3. 함수는 매개변수에게 함수를 전달할 수 있다.
const increaser = makeCounter(auxs.increase);
console.log(increaser()); // 1
console.log(increaser()); // 2

// 3. 함수는 매개변수에게 함수를 전달할 수 있다.
const decreaser = makeCounter(auxs.decrease);
console.log(decreaser()); // -1
console.log(decreaser()); // -2
```

일급 객체라는 의미는 함수를 객체와 동일하게 사용이 가능하다는 의미이다.
함수의 매개변수, 반환값으로 사용할 수 있다는 특징으로 인해 자바스크립트의 함수형 프로그래밍이 가능해진다.
하지만 함수는 일반 객체와는 차이가 있다.
일반 객체는 호출할 수 없지만 함수는 호출이 가능하다. 또한 함수 객체는 일반 객체에는 없는 함수 고유의 프로퍼티를 소유한다.

<br />

---

### 함수 객체의 프로퍼티

함수는 객체이므로 프로퍼티를 가질 수 있다.
**proto**는 함수 객체의 고유 프로퍼티가 아닌, Object.prototype 객체의 프로퍼티를 상속 받는다.

### arguments 프로퍼티

    arguments 객체
    함수 호출 시 전달된 인수들의 정보를 담고 있는 순회 가능한 유사 배열 객체

함수 내부에서 지역 변수처럼 사용되며, 함수 외부에서는 참조가 불가능하다.arguments 객체는 매개 변수를 확정할 수 없는 가변 인자 함수 구현에 유용

ES5 까지 arguments 객체는 유사 배열 객체로 구분되었기 때문에 배열이 아니었다.
따라서 배열 메서드를 사용할 경우 에러가 발생했다.
ES6부터 이터러블이 도입되어 arguments 객체는 유사 배열 객체이면서 동시에 이터러블이 되었다.
