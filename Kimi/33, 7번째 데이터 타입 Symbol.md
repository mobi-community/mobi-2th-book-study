> ✏️7번째 데이터 타입 Symbol

###### 자바스크립트에는 6개의 타입 문자열, 숫자, 불리언, undefined, null, 객체 타입이 있음
###### "심벌"은 7번째 데이터 타입으로 변경 불가능한 원시타입의 값이다.
###### 심벌은 다른 값과 중복되지 않는 유일무이한 값

# 심벌 값의 생성
심벌 값은 Symbol 함수를 호출하여 생성 </br>
### 다른값과 절대 중복되지 않는 유일무이한 값이다.

```jsx
const mySymbol =  Symbol();
console.log(typeof mySymbol); //symbol

//심벌 값은 외부로 노출되지 않아 확인할 수 없다.
console.log(mySymbol); // Symbol()
```

`new`연산자로 호출할 수 없다 // TypeError: Symbol is a not a constructor


# Symbol.for / Symbol.keyFor 메서드

#### Symbol.for
전역에서 중복되지 않는 유일무이한 상수인 심벌 값을 단 하나만 생성하여 전역 심벌 레지스트리를 통해 공유할 수 있다

#### Symbol.keyFor
전역 심벌 레지스트리에 저장된 심벌 값의 키를 추출할 수 있다

# 심벌과 프로퍼티 키
### 심벌은 유일무이한 값이므로 심벌 값으로 프로퍼티 키를 만들면 다른 프로퍼티 키와 절대 충돌하지 않는다

```jsx
const obj = {
  //심벌값으로 프로퍼티 키 생성
  [Symbol.for('mySymbol')]: 1
};

obj[Symbol.for('mySymbol')]; //-> 1
```


