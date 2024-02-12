> ✏️strict mode

###### ESLint같은 린트 도구 사용해도 strict mode와 유사한 효과
###### 린트 도구는 정적 분석 기능을 통해 소스코드 실행 전 스캔하여 문법적 오류~잠재적 오류까지 찾안내고 원인 리포팅

# strict mode의 적용
**즉시 실행 함수**로 스크립트 전체를 감싸서 스코프를 구분하고 선두에 `use strict`를 추가한다 </br>
전역에 사용시 script단위로 적용됨 피하자.

```jsx
(function foo() {
  "use strict";
  x = 10; //ReferenceError: x is not defined
}());
```
