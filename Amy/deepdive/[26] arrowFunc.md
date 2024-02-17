##### | 모던 자바스크립트 DeepDive <br />

###### range: 26. ES6 함수의 추가 기능 <br />

###### date: day21 (2024.02.16) <br />

<hr />
<br />

### 함수의 구분

<table>
    <tr>
        <td>ES6 함수 구분</td>
        <td>constructor</td>
        <td>prototype</td>
        <td>super</td>
        <td>args</td>
    </tr>
    <tr>
        <td>일반 함수</td>
        <td>O</td>
        <td>O</td>
        <td>X</td>
        <td>O</td>
    </tr>
    <tr>
        <td>메서드</td>
        <td>X</td>
        <td>X</td>
        <td>O</td>
        <td>O</td>
    </tr>
    <tr>
        <td>화살표 함수</td>
        <td>X</td>
        <td>X</td>
        <td>X</td>
        <td>X</td>
    </tr>
</table>

<br />

### 메서드

축약 표현으로 정의된 함수

```javascript
const obj = {
  x: 1,
  foo() {
    return this.x;
  },
  bar: function () {
    return this.x;
  },
};
```

foo는 메서드이고 bar에 바인딩된 함수는 일반 함수다.

<br />

### 화살표 함수

function 키워드 대신 화살표를 사용해 간략하게 함수 정의

콜백 함수 내부에서 this가 전역 객체를 가리키는 문제를 해결하기 위한 대안으로 유용

```javascript
const person = (name) =>
  ({
    sayHi() {
      return `hello, I'm ${name}!`;
    },
  }("Lee"));
```

#### 일반 함수와의 차이

- 화살표 함수는 인스턴스 생성 불가 (non-constructor)
- 중복된 매개변수 이름 선언 불가
- 함수 자체의 this, args, super, new.target 바인딩 X

<br />
