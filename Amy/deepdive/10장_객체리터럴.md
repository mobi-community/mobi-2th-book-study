##### | 모던 자바스크립트 DeepDive <br />

###### range: 10. 객체 리터럴 <br />

###### date: day01(2024.01.15) <br />

<hr />
<br />

### 객체란?

- JS를 구성하는 거의 모든 것 (👉 원시 값을 제외한 나머지 값이 모두 객체)
- 다양한 타입의 값을 하나의 단위로 구성한 자료구조
- 변경 가능한 값
- 프로퍼티와 메서드로 구성된 집합체

<br />

#### 프로퍼티

##### 프로퍼티란?

```
let Peanut = {
  name: 'Peter', 👉 property (key = name, value = Peter)
  age: 20, 👉 property
};
```
- 식별자 네이밍 규칙을 따르지 않는 이름에는 반드시 따옴표 사용
- 키를 동적으로 생성할 경우, 키로 사용할 표현식은 대괄호로 묶을 것
- 예약어를 사용해도 에러가 발생하지 않지만 예상치 못한 에러 발생 확률 o, 권장 x
- 중복 선언 시 덮어씀

##### 접근

- 마침표 표기법(dot notation)      마침표 프로퍼티 접근 연산자를 사용 
- 대괄호 표기법(bracket notation)  대괄호 프로퍼티 접근 연산자 사용 

```javascript
let Peter = {
  name: 'topDragon',
  age: 20,
  nickname: 'peanut',
  isMovvi: true,
  isOperator: true,
  isDirector: true
}
```

- 키가 식별자 네이밍 규칙을 준수하지 않는 이름이라면 반드시 대괄호 표기법 사용
- 키가 숫자로 이뤄진 문자열인 경우 따옴표 생략 가능, 그 외는 따옴표 필수

```javascript
console.log(Peter.name) // topDragon
console.log(Peter[nickname])  // peanut
```


##### 갱신

이미 존재하는 값을 할당하면 갱신됨

```javascript
console.log(Peter.name) // topDragon
Peter.name = '성용'
console.log(Peter.name) // 성용
```

##### 동적 생성

존재하지 않는 프로퍼티에 값을 할당하면 동적으로 생성돼 추가되고 값이 할당됨

```javascript
Peter.height = 190;
```

##### 삭제

delete 연산자를 사용해 삭제

```javascript
delete Peter.height;
```

##### 확장 기능 (ES6)
###### 프로퍼티 축약 표현
변수를 프로퍼티 값으로 사용하는 경우, 변수 이름과 프로퍼티 키가 동일한 이름일 때 키 생략 가능

```
let x = 1, y = 2;
const obj = {x, y};

console.log(obj);   // {x : 1, y: 2 }
```

###### 계산된 프로퍼티 이름
문자열 또는 문자열로 타입 변환 가능한 값으로 평가되는 표현식을 사용해 동적 생성 가능 <br />
프로퍼티 키로 사용할 표현식은 대괄호 표기법 사용

```javascript
let prefix = 'prop';
let i = 0;
let obj = {};

obj[ prefix + '-' + ++i ] = i;
obj[ prefix + '-' + ++i ] = i;
obj[ prefix + '-' + ++i ] = i;

console.log(obj);   // { prop-1: 1, prop-2: 2, prop-3: 3 }
```

<br />

#### 메서드

```javascript
let counter = {
  num: 0,      👉 property
  increase: function(){     👉 method
    this.num++;
  }
}
```
- 값이 함수일 경우 일반 함수와 구분하기 위해 메서드라고 부른다.

##### 축약 표현 (확장 기능 (ES6))

```javascript
let counter = {
  num: 0,       👉 property
  increase(){     👉 method
    this.num++;
  }
}
```

- function 키워드를 생략해 축약할 수 있다.
- 축약 표현으로 정의한 메서드는 프로퍼티에 할당한 함수와 다르게 동작한다. 👉 26장. 메서드



---


### 객체 생성 방법

- 객체 리터럴
- Object 생성자 함수
- 생성자 함수
- Object.create 메서드
- 클래스 (ES6)








