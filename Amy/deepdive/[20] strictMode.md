##### | 모던 자바스크립트 DeepDive <br />

###### range: 20. strict mode <br />

###### date: day16 (2024.02.11) <br />

<hr />
<br />

### strict mode?

자바스크립트 언어의 문법을 좀 더 엄격히 적용해 오류 발생 가능성이 높거나 최적화 작업에 문제를 일으킬 우려가 있는 코드에 명시적 에러 발생
ESLint 같은 린트 도구로도 유사한 효과

ESLint는 코딩 컨벤션을 정의해 강제할 수 있어 더욱 강력한 효과

<br />

### strict mode

전역의 선두 / 함수 몸체의 선두에 `'use strict';` 추가
전역의 선두에 적용 시 스크립트 전체에 적용

- 전역에 적용하는 strict mode 사용 지양
  strict-mode 적용 스크립트와 non-strict-mode 적용 스크립트를 혼용하는 오류 발생 가능성 O

- 함수 단위의 strict mode 사용 지양
  모든 함수에 일일이 적용하기 번거로움
  strict-mode가 적용된 함수가 참조할 함수 외부의 컨텍스트에 strict-mode 미적용 시 문제 발생 가능성 O

##### 그럼 어떻게 써..?

-> 즉시 실행 함수로 감싼 스크립트 단위로 적용하는 것이 바람직

```javascript
function foo() {
  "use-strict";
  let = 20; // SyntaxError: Unexpected strict mode reserved word
}
foo();
```

<br />

### strict mode가 발생시키는 에러

##### 암묵적 전역

선언하지 않은 변수 참조 시 ReferenceError

##### 변수, 함수, 매개변수의 삭제

delete 연산자로 삭제 시 SyntaxError

##### 매개변수 이름의 중복

SyntaxError

##### with 문의 사용

SyntaxError
with 문은 전달된 객체를 스코프 체인에 추가
with 문은 동일한 객체의 프로퍼티를 반복해 사용할 때 객체 이름 생략이 가능해 코드가 간결해지지만
성능과 가독성이 나빠지는 단점. -> 지양 추천

<br />

### strict mode 기대효과

##### 일반 함수의 this

strict mode에서 일반 함수 호출 시 this에 undefined가 바인딩
생성자 함수가 아닌 일반 함수 내부에서는 this 사용 필요 X

##### arguments 객체

매개변수에 전달된 인수를 재할당해 변경해도 arguments 객체에 반영 X
