> ✏️Math

###### 수학적인 상수와 함수를 위한 프로퍼티와 메서드 제공
###### 생성자 함수가 아니다

# Math 프로퍼티

### Math.PI
원주율 값 반환 (3.141592~~~~)


# Math 메서드

### Math.abs
인수로 전달된 숫자의 절대값 반환
###### 절대값은 반드시 0 또는 양수여아 함

```jsx
Math.abs(-1); //-> 1
Math.abs("-1") //-> 1
Math.abs('') //-> 0
Math.abs([]) //-> 0
Math.abs(null) //-> 0
Math.abs(undefined) //-> NaN
```

### Math.round
인수로 전달된 숫자의 소수점 이하를 반올림한 정수 반환

```jsx
Math.round(1.4); //-> 1
Math.round(2.6); //-> 3
Math.round(-1.4); //-> -1
Math.round(-2.6); //-> -3
```

### Math.ceil
인수로 전달된 숫자의 소수점 이하를 올림한 정수 반환

```jsx
Math.ceil(1.4); //-> 2
Math.ceil(2.6); //-> 3
Math.ceil(-1.4); //-> -1
Math.ceil(-2.6); //-> -2
```

### Math.floor
인수로 전달된 숫자의 소수점 이하를 내림한 정수 반환

```jsx
Math.floor(1.4); //-> 1
Math.floor(2.6); //-> 2
Math.floor(-1.4); //-> -2
Math.floor(-2.6); //-> -3
```


### Math.sqrt
인수로 전달된 숫자의 제곱근 반환

```jsx
Math.sqrt(9); //-> 3
Math.sqrt(-9); //-> NN
```


### Math.random
임의의 난수(랜덤 숫자)를 반환

##### Math.random 메서드가 반환한 난수는 0~1미만의 실수다. 0은 포함되지만 1은 포함X
```jsx
const random = Math.floor((Math.raandom() * 10) + 1);
console.log(random) // 1~10 범위의 정수
```

### Math.pow
첫 번째 인수를 밑, 두 번째 인수를 지수로 거듭제곱한 결과 반환 `(2**2**2)`


### Math.max
전달받은 인수 중 가장 큰 수 반환
```jsx
Math.max(1,2,3) //-> 3
```

### Math.min
전달받은 인수 중 가장 작은 수 반환




