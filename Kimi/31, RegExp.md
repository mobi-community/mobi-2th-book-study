> ✏️RegExp

###### 정규표현식은 문자열을 대상으로 패턴매칭 기능을 제공한다
###### 장점 | 반복문과 조건문 없이 패턴을 정의하고 테스트하는 것으로 간단히 체크가 가능하다
###### 단점 | 주석이나 공백을 허용하지 않고 여러가지 기호 혼합하여 사용하기 때문에 가독성이 좋지않다

# 1, 정규 표현식의 생성
정규 표현식 객체를 생성하기 위해서는 정규 표현식 리터럴과 RegExp 생성자 함수를 사용할 수 있다

![image](https://github.com/mobi-community/mobi-2th-book-study/assets/134191815/a8cc6192-2653-4d7a-a1ab-0e9d4836aeb2)

```jsx
const target = "is this all there is?";

//패턴: is
//플래그: i => 대소문자를 구별하지 않고 검색한다.
const regexp = /is/i;

//test 메서드는 target문자열에 대해 정규 표현식 regexp의 패턴을 검색하여
//매칭결과를 불리언 값으로 반환한다
regexp.test(target); //-> true
```

RegExp 생성자 함수를 사용하여 RegExp 객체 생성도 가능하다

```jsx
const target = "is this all there is?";

const regexp = new RegExp(/is/i);
// const regexp = new RegExp(/is/, 'i');
// const regexp = neew RegExp('is', 'i');

regexp.test(target); //-> true
```

# 2, RegExp 메서드

#### RegExp.prototype.exec

인수로 전달받은 문자열에 대해 정규표현식의 패턴을 검색하여 매칭 결과를 배열로 반환</br>
매칭 결과 없는 경우 `null`반환

```jsx
regExp.exec(target);
```

#### RegExp.prototype.test
인수로 전달받은 문자열에 대해 정규표현식의 패턴을 섬색하여 매칭 결과를 불리언 값으로 반환


#### RegExp.prototype.match
대상 문자열과 인수로 전달받은 정규 표현식과의 매칭결과를 배열로 반환


# 3, 플래그

|플래그|의미|설명|
|------|---|---|
|i|Ignore case|대소문자를 구별하지 않고 패턴을 검색한다|
|g|Global|대상 문자열 내에서 패턴과 일치하는 모든 문자열을 전역 검색한다|
|m|Multi line|문자열의 행이 바뀌더라도 패턴 검색을 계속한다|


# 4, 패턴

#### 반복검색
`{m,n}`: 앞선 패턴이 최소 m번, 최대 n번 반복되는 문자열 의미 (콤마 뒤에 공백 없어야한다!!!)


#### NOT 검색
`^`: not의 이미를 갖는다

```jsx
//숫자를 제외한 문자열을 전역 검색한다
//+ : 분해되지 않은 단어 레벨로 검색하기 위함
const regExp = /[^0-9]+/g;
```

#### 시작 위치로 검색
```jsx
//'http'로 시작한는지 검사
const regExp = /^http/;
```

#### 마지막 위치로 검색
```jsx
//'com'으로 끝나는지 검사
const regExp = /com$/;
```



# 5, 자주 사용하는 정규표현식

#### 특정 단어로 시작하는지 검사
```jsx
const url = 'http~'
//http:// 또는 https://로 시작하는지 검사
/^http?:\/\//.test(url);
```


#### 특정 단어로 끝나는지 검사

```jsx
const fileName = 'index.html'
//html로 끝나는지 검사
/html$/.test(fileName);
```



#### 숫자로만 이루어진 문자열인지 검사
```jsx
const target = '12345'
//숫자로만 이뤄진 문자열인지 검사
/^d+$/.teest(target);
```


#### 하나이상의 공백으로 시작하는지 검사
```jsx
const target = ' Hi!'
//하나 이상의 공백으로 시작하는지 검사
/^[\s]+/.test(targeet);
```


#### 아이디로 사용가능한지 검사
```jsx
const id = 'abc123';

//알파벳 대소문자 또는 숫자로 시작하고 끝나며 4~10자리인지 검사한다
/^[A-Za-z0-9]{4,10}$/.test(id);
```

#### 메일 주소 형식에 맞는지 검사
```jsx
const email = 'kimi@kimi.com';

/^[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*@[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*\.[a-zA-Z]{2,3}$/.test(email);
//인터넷 메세지 형식 약인 RFC 5322에 맞는 정교한 패턴 매칭이 필요하다면 무척 복잡한 식이 있으니 검색 하기
```



#### 핸드폰 번호 형식에 맞는지 검사

```jsx
const phone = '010-1234-5678';

/^\d{3}-\d{3,4}-\d{4}$/.test.(phone);
```

#### 특수 문자 포함 여부 검사
```jsx
const target = 'abc#123'

(/[^A-Za-z0-9]/gi).text(target);
```


