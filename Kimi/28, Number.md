> ✏️Number

###### 원시타입인 숫자를 다룰 때 유용한 프로퍼티와 메서드 제공


# 1, Number 생성자 함수
>`Number`: 표준 빌트인 객체, 생성자 함수 객체</br>
>`new`연산자와 함게 호출하여 Number인스턴스 생성


```jsx
const numObj = new Number(10);
console.log(numObj); //-> 10

//인수로 숫자가 아닌 값 전달시 인수를 숫자로 강제 변환
const numObj = new Number("10");
console.log(numObj); //-> 10

const numObj = new Number("song");
console.log(numObj); //-> NaN

```

# 2, Number 프로퍼티

### Number.EPSILON
1과 1볻다 큰 숫자 중 가장 작은 숫자와의 차이와 같음

### Number.MAX_VALUE
자바스크립트에서 표현할 수 있는 가장 큰 양수 값 (*보다 큰 숫자는 `Infinity`다.)

### Number.Min_VALUE
자바스크립트에서 표현할 수 있는 가장 작은 양수 값 (*보다 작은 숫자는 0)

### Number.MAX_SAFE_INTEGER
가장 안전하게 표현할 수 있는 가장 큰 정수 값

### Number.MIN_SAFE_INTEGER
가장 안전하게 표현할 수 있는 가장 작은 정수의 값


### Number.POSITIVE_IFINITY
양의 무한대를 나타내는 숫자 Infinity와 같음

### Number.NEGATIVE_IFINITY
음의 무한대를 나타내는 숫자 -Infinity와 같음

### Number.NaN
숫자가 아님을 나타냄(Not-a-Number) === window.NaN


# 3, Number 메서드

### Number.isFinitee
유한수이면 `true`, 무한수이거나 NaN이면 `false`

### Number.isInteger
정수인지 아닌지 `boolean`

### Number.isNaN
NaN `boolean`

### Number.prototype.toFixed
숫자를 반올림하여 문자열로 반환

```jsx
(12345.6789).toFixed(); //12346
//한 자리 유효, 나머지 반올림 
(12345.6789).tofixed(1); //12345.7
```

### Number.prototype.toString
숫자를 문자열로 변환하여 반환

```jsx
//toString("진수")안에 진수를 넣으면 해당 []진수로 반환됨
(10).toString(); //->"10"
```








