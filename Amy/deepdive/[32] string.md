##### | 모던 자바스크립트 DeepDive <br />

###### range: 32. string <br />

###### date: day23 (2024.02.19) <br />

<hr />
<br />

### string 생성자 함수

### string 메서드

string 객체의 메서드는 언제나 새로운 문자열 반환.
문자열은 변경 불가능한 원시 값이므로 String 래퍼 객체도 읽기 전용 객체로 제공.

<br />

### 사용 빈도가 높은 String 메서드

#### indexOf

대상 문자열에서 인수로 전달받은 문자열을 검색해 첫 번째 인덱스를 반환. <br />
검색에 실패하면 -1 반환. <br />
두 번째 인수로 검색을 시작할 인덱스 전달 가능.

ES6에서 도입된 `String.prototyupe.includes` 메서드를 사용하면 더 가독성 좋게 표현 가능 <br />

<br />

#### includes

대상 문자열에 인수로 전달받은 문자열이 포함되어 있는지 확인해 그 결과를 불리언 타입으로 반환.<br />
두 번째 인수로 검색을 시작할 인덱스 전달 가능.

<br />

#### search

대상 문자열에서 인수로 전달받은 정규 표현식과 매치하는 문자열을 검색해 일치하는 문자열의 인덱스를 반환. <br />
검색에 실패하면 -1을 반환.

<br />

#### startsWith

대상 문자열이 인수로 전달받은 문자열로 시작하는지 확인해 그 결과를 불리언 타입으로 반환. <br />
두 번째 인수로 검색을 시작할 인덱스 전달 가능.

<br />

#### endsWith

대상 문자열이 인수로 전달받은 문자열로 끝나는지 확인해 그 결과를 불리언 타입으로 반환.<br />
두 번째 인수로 검색할 문자열의 길이 전달 가능.

<br />

#### CharAt

대상 문자열에서 인수로 전달받은 인덱스에 위치한 문자를 검색해 반환. <br />
인덱스는 문자열의 범위 사이의 정수여야 하며 인덱스가 문자열의 범위를 벗어난 정수인 경우 빈 문자열을 반환. <br />

유사한 문자열 메서드로는 `String.prototype.CharCodeAt`, `String.prototype.CodePointAt`이 있다.

<br />

#### substring

대상 문자열에서 첫 번째 인수로 전달받은 인덱스에 위치하는 문자부터 두 번째 인수로 전달받은 인덱스에 위치하는 문자의 바로 이전 문자까지의 부분 문자열을 반환.

```javascript
const str = "hello, world";

// index 1 ~ 4 이전까지의 부분 문자열 반환
str.substring(1, 4); // ell
```

두 번째 인수는 생략 가능. <br />
이때 첫 번째 인수로 전달한 인덱스에 위치하는 문자부터 마지막 문자까지 부분 문자열을 반환.

`String.prototype.indexOf`와 함께 사용하면 특정 문자열을 기준으로 앞뒤에 위치한 부분 문자열 취득 가능.

```javascript
const str = "hello, world";

// space를 기준으로 앞에 있는 부분 문자열 취득
str.substring(0, str, indexOf("  ")); // hello

// space를 기준으로 뒤에 있는 부분 문자열 취득
str.substring(str.indexOf("  ") + 1, str.length); // world
```

<br />

#### slice

substring과 동일하게 동작하지만 slice는 음수인 인수 전달이 가능하다는 점에서 차이가 있다.<br />
음수인 인수를 전달하면 대상 문자열의 가장 뒤에서부터 시작해 문자열을 잘라내 반환.

#### toUpperCase

대상 문자열을 모두 대문자로 변경한 문자열을 반환

#### toLowerCase

대상 문자열을 모두 소문자로 변경한 문자열을 반환

#### trim

대상 문자열 앞뒤에 공백 문자가 있을 경우 이를 제거한 문자열을 반환 <br />
`String.prototype.replace` 메서드에 정규 표현식을 인수로 전달해 공백 문자 제거도 가능. <br />

<br />

#### replace

대상 문자열에서 첫 번째 인수로 전달받은 문자열/정규표현식을 검색해 두 번째 인수로 전달한 문자열로 치환한 문자열을 반환. <br />

특수한 교체 패턴 이용 가능. <br />
ex. $&는 검색된 문자열을 의미. <br />

두 번째 인수로 치환 함수 전달 가능. <br />
첫 번째 인수로 전달한 문자열/정규표현식에 매치한 결과를 두 번째 인수로 전달한 치환 함수의 인수로 전달하면서 호출하고 치환 함수가 반환한 결과와 매치 결과를 치환.

ex) 카멜 케이스를 스네이크 케이스로 변경하는 함수

```javascript
const snakeCase = "hello_world";

function snackToCamel(snakeCase) {
  return snakeCase.replace(/_[a-z]/g, (match) => {
    console.log(match); // '_w'
    return match[1].toUpperCase();
  });
}
snackToCamel(snakeCase); // 'helloWorld'
```

<br />

#### repeat

대상 문자열을 인수로 전달받은 정수만큼 반복해 연결한 새로운 문자열을 반환. <br />
전달받은 정수가 0이면 빈 문자열을 반환. 인수 생략 시 기본값 0으로 설정. <br />
음수면 RangeError. <br />

```javascript
const str = "abc";

str.repeat(2); // abcabc
```

<br />

#### split

대상 문자열에서 첫 번째 인수로 전달한 문자열 또는 정규 표현식을 검색해 문자열을 구분한 후 분리된 각 문자열로 이뤄진 배열 반환. <br />
인수로 빈 문자열 전달 시 각 문자를 모두 분리. <br />
인수 생략 시 대상 문자열 전체를 단일 요소로 하는 배열 반환. <br />

두 번째 인수로 배열의 길이 지정 가능. <br />

배열을 반환하기 때문에 `reverse`, `join` 메서드와 함께 사용하면 문자열을 역순으로 뒤집을 수 있다.
