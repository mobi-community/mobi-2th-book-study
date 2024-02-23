> ✏️String

###### 표준 빌트인 객체인 String은 원시 타입인 문자열을 다룰 때 유용한 프로퍼티와 메서드를 제공한다

# String 생성자 함수

```jsx
consst strObj = new String("Kim");
console.log(strObj)
//String {0:"K", 1:"i", 2:"m", length:3, [[PrimitiveVaaluee]]: "Kim"}
```

자바나 C++같은 클래스 기반 언어에서 this는 언제나 클래스가 생성하는 인스턴스를 가리키지만, </br>
**자바스크립트의 this는 함수가 호출되는 방식에 따라 this 바인딩이 동적으로 결정됨**


# length 프로퍼티
length 프로퍼티는 문자열의 문자개수를 반환한다

# String 메서드
문자열은 변경 불가능한 원시 값이기 때문에 String 래퍼 객체도 읽기전용 객체로 제공된다


#### String.prototype.indexOf
`indexOf`메서드는 대상 문자열에서 인수로 전달받은 문자열을 검색하여 첫 번째 인덱스 반환 </br>
검색 실패시 `-1` 반환

```jsx
str.indexOf('i', 3); //3번째 인덱스부터 시작하여 i찾아서 해당 인덱스 반환
```

str에 특정 문자열이 존재하는가?
```jsx
//1.
if(str.indexOf("string") !== -1 {}

//2.
if(str.includes("string")) {}
```



#### String.prototype.startsWith

```jsx
const str = "Hello World";

str.startsWith('He'); //->true /특정 문자열로 시작하는지 확인


// 5부터 시작하는 문자열이 ' '로 시작하는지 확인
str.startsWith(' ', 5)//=>true
```

#### String.prototype.endsWith

```jsx
const str = "Hello World";

str.endsWith('ld'); //->true /특정 문자열로 끝나는지 확인
```


#### String.prototype.charAt
```jsx
const str = 'Hello';

for(let i=0; i < str.lenght; i++) {
  console.log(str.charAt(i)); // H e l l o
}
```


#### String.prototype.substring vs String.prototype.slice
substring과 slice모두 문자열을 잘라서 반환한다는 점은 동일하지만, slice 는 음수를 전달할 수 있다(뒤에서 부터 시작하여 문자열 잘라내 반환)

#### String.prototype.toUpperCase
대상 문자열을 모두 대문자로 변환하여 반환

#### String.prototype.toLowerCase
대상 문자열을 모두 소문자로 변환하여 반환


#### String.prototype.trim
대상 문자열 앞뒤에 공백 문자 있을 경우 이를 제거한 문자열 반환

#### String.prototype.repeat
대상 문자열을 인수로 전달받은 정수만큼 반복해 연결한 새로우 문자열 반환

정수 0이면 빈문자열 반환, 음수이면 RangeError발생시킨다

#### String.prototype.replace
대상 문자열에서 첫 번째 인수로 전달받은 문자열 또는 정규표현식 검색하여 두 번재 인수로 전달한 문자열 치환하여 반환한다
```jsx
const str = "Hellow World";

str.replace("World", "Lee"); //-> "Hello Lee"
```


#### String.prototype.split

```jsx
const str = "How are you doing?";

// 공백으로 구분하여 배열로 반환
str.split(" "); //-> ["How", "are", "you", "doing?"]

//인수로 빈문자열을 전달하면 각 문자 모두 분리한다
str.split("");//-> ["H", "o", "w", " ", "a" ...]


// reverse(): 인수로 전달받은 문자열 역순으로 뒤집는다
function reverseString(str) {
  retrun str.split('').reverse().join('');
}

reverseString("Hello World!"); //->"!dlroW olleH"

```

