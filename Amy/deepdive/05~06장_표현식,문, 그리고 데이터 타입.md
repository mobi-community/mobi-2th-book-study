##### | 모던 자바스크립트 DeepDive <br />

###### range: 05. 표현식과 문, 06. 데이터타입 <br />

###### date: day03(2024.01.06) <br />

<hr />
<br />

### | 값 Value = 표현식 expression ➡️ 평가 evaluate

<br />

<table align="center"> 
    <tr>
        <td rowspan="3">값(value)</td>
        <td>표현식이 평가된 결과</td>
        <td rowspan="3"></td>
    </tr>
    <tr>
        <td>데이터 타입 보유</td>
    </tr>
    <tr>
        <td>변수 식별자를 참조하면 값이 됨</td>
    </tr>
    <tr>
        <td rowspan="2">표현식(expression)</td>
        <td>값으로 표현될 수 있는 모든 문</td>
        <td>ex. 리터럴</td>
    </tr>
    <tr>
        <td>값처럼 사용 가능</td>
        <td></td>
    </tr>
    <tr>
        <td>평가 (evaluate)</td>
        <td>식을 해석해 값을 생성/참조</td>
        <td></td>
    </tr>
</table>

<br />

- 동치(equivalent) : 표현식과 표현식이 평가된 값, 동등한 관계

<br />

### | 표현식과 문 ⭐️

<details>
    <summary>문(statement)과 표현식(expression), 왜 구분해야하는가?</summary>
    <br />
    <p> - JS 엔진의 입장에서 코드 읽기 가능 ➡️ 실행 예측에 도움</p>
    <p> - 버그를 줄이고 코드의 품질을 향상</p>
</details>

<br />

##### 문이란?

<br />

<table align="center">
    <tr>
        <td align="center" colspan="3">문 statement</td>
    </tr>
    <tr>
        <td>설명</td>
        <td>예시</td>
    </tr>
    <tr>
        <td>프로그램을 구성하는 기본 단위, 최소 실행 단위</td>
        <td></td>
    </tr>
    <tr>
        <td>여러 개의 토큰(token)으로 구성</td>
        <td>let sum = 1 + 2;</td>
    </tr>
    <tr>
        <td>컴퓨터에 내리는 명령</td>
        <td></td>
    </tr>
    <tr>
        <td>선언문, 할당문, 조건문, 반복문 ...</td>
        <td></td>
    </tr>
</table>

<br />

<table align="center">
    <tr>
        <td rowspan="2">토큰(token)</td>
        <td>문법적인 의미를 갖는 가장 작은 단위</td>
        <td rowspan="2">키워드, 식별자, 연산자, 리터럴, 세미콜론(;), 마침표(.)</td>
    </tr>
    <tr>
        <td>코드의 기본 요소</td>
    </tr>
</table>

<br />

##### 표현식인 문과 표현식이 아닌 문

이 문이 표현식인지 아닌지 구분하는 가장 간단 명료한 방법 👉 변수에 할당해보기

<br />

변수 선언문은 표현식 X

```
// 표현식이 아닌 문은 값처럼 사용 불가

let foo = let x ; // SyntaxError: Unexpected token
```

할당문은 그 자체로 표현식

```
// 변수 선언문은 문
let x

// 할당문은 자체로 표현식 && 완전한 문 (표현식인 문)
let x = 100 ;
```

할당문을 값처럼 변수에 할당하게 되면 할당한 값으로 평가

```
// 표현식인 문은 값처럼 사용 가능
let foo = x = 100 ;
console.log(foo);  // 100
```

<br />

#### | Literal ?

<details>
    <summary>리터럴 literal</summary>
    <br />
    <p> - 사람이 이해할 수 있는 문자/약속된 기호를 사용한 표기법 </p>
    <p> - 값을 생성하는 가장 기본적인 방법 </p>
    <p> - 런타임에 평가 </p>
    <p> - 다양한 종류의 값 생성 가능  </p>
    <table>
        <tr>
            <td>literal</td>
            <td>example</td>
            <td>💬</td>
        </tr>
        <tr>
            <td>정수 리터럴</td>
            <td>100</td>
            <td></td>
        </tr>
        <tr>
            <td>부동소수점 리터럴</td>
            <td>10.5</td>
            <td></td>
        </tr>
        <tr>
            <td>2진수 리터럴</td>
            <td>ob01000001</td>
            <td>ob로 시작</td>
        </tr>
        <tr>
            <td>8진수 리터럴</td>
            <td>0o101</td>
            <td>0o로 시작 (ES6)</td>
        </tr>
        <tr>
            <td>16진수 리터럴</td>
            <td>0x41</td>
            <td>0x로 시작 (ES6)</td>
        </tr>
        <tr>
            <td>문자열 리터럴</td>
            <td>'hello world'</td>
            <td>'', "" 둘 다 가능</td>
        </tr>
        <tr>
            <td rowspan="2">불리언 리터럴</td>
            <td>true</td>
            <td rowspan="2"></td>
        </tr>
        <tr>
            <td>false</td>
        </tr>
        <tr>
            <td>null 리터럴</td>
            <td>null</td>
            <td></td>
        </tr>
        <tr>
            <td>undefined 리터럴</td>
            <td>undefined</td>
            <td></td>
        </tr>
        <tr>
            <td>객체 리터럴</td>
            <td>[{name: 'Peanut'}, {workplace : '역삼동'}]</td>
            <td></td>
        </tr>
        <tr>
            <td>배열 리터럴</td>
            <td>[1,2,3]</td>
            <td></td>
        </tr>
        <tr>
            <td>함수 리터럴</td>
            <td>function(){ ... }</td>
            <td></td>
        </tr>
        <tr>
            <td>정규 표현식 리터럴</td>
            <td>/[A-Z]+/g</td>
            <td></td>
        </tr>
    </table>
</details>

<br />

## 데이터 타입

<br />

JS에서는 7개의 데이터 타입을 제공하며 이는 원시 타입과 객체 타입으로 분류할 수 있다. <br />
숫자 타입의 1과 문자열 타입의 '1'은 비슷해보이지만 전혀 다른 값이다. <br />
각각 생성한 목적과 용도가 다르기 때문에 개발자도 JS 엔진도 구별해서 값을 취급한다.

<br />

##### 데이터 타입의 종류

<table align="center">
    <tr>
        <td>구분</td>
        <td>데이터 타입</td>
        <td>설명</td>
        <td>비고</td>
    </tr>
    <tr>
        <td rowspan="12">primitive 타입</td>
        <td rowspan="2">number 타입</td>
        <td>숫자, 정수, 실수 구분 없이 모두 숫자 타입</td>
        <td rowspan="2">Infinity, -Infinity, NaN</td>
    </tr>
    <tr>
        <td>2진수, 8진수, 16진수 구분 X 👉 모두 10진수로 해석</td>
    </tr>
    <tr>
        <td rowspan="5">string 타입</td>
        <td>문자열, 텍스트 테이터로 변경 불가능한 값(immutable value)</td>
        <td rowspan="3">""(큰따옴표),''(작은따옴표),``(백틱)</td>
    </tr>
    <tr>
        <td>0개 이상의 16비트 유니코드 문자(UTC-16)의 집합으로 표현</td>
    </tr>
    <tr>
        <td>토큰과 구분하기 위해 따옴표를 쓰며 공백 포함 가능</td>
    </tr>
    <tr>
        <td>멀티라인을 위해 escape sequence 사용</td>
        <td>*라인 피드와 캐리지 리턴</td>
    </tr>
    <tr>
        <td>템플릿 리터럴 내 표현식 삽입 가능</td>
        <td>+ 혹은 ${} 사용</td>
    </tr>
    <tr>
        <td>boolean 타입</td>
        <td>논리적 true, false</td>
        <td>8장 조건문에서 자주 사용</td>
    </tr>
    <tr>
        <td>undefined 타입</td>
        <td>var, let 키워드로 선언된 변수에 암묵적으로 할당되는 값</td>
        <td>"정의되지 않은"</td>
    </tr>
    <tr>
        <td>null 타입</td>
        <td>"값이 없다"는 것을 의도적으로 명시할 때 사용하는 값</td>
        <td>의도적 부재, 더 이상 참조 X</td>
    </tr>
    <tr>
        <td rowspan="2">symbol 타입</td>
        <td>유일무이한 값 (중복 X)</td>
        <td rowspan="2">(ES6) 외부 노출 X</td>
    </tr>
    <tr>
        <td>객체의 유일한 프로퍼티 키를 만들기 위해 사용</td>
    </tr>
    <tr>
        <td rowspan="2" colspan="2">object/reference 타입</td>
        <td>JS를 이루고 있는 대부분이 객체</td>
        <td rowspan="2">객체, 함수, 배열 등</td>
    </tr>
    <tr>
        <td>위 7가지를 제외한 나머지는 전부 객체 타입</td>
    </tr>

</table>

<br />

##### 왜 필요할까?

1. 데이터 타입에 따라 확보할 메모리의 공간 크기 결정을 위해
2. 값을 참조할 때 한 번에 알아야 할 메모리 공간의 크기 결정을 위해
3. 메모리에서 읽어 들인 2진수를 어떻게 해석할지 결정하기 위해

<br />

## 동적 타입 언어와 정적 타입 언어

<br />

<table>
    <tr>
        <td colspan="2">데이터 타입 종류</td>
        <td>특징</td>
        <td>종류</td>
    </tr>
    <tr>
        <td rowspan="5">정적 타입</td>
        <td rowspan="5">static/strong type</td>
        <td>명시적 타입 선언, 데이터 타입을 사전에 선언</td>
        <td rowspan="5">C, C++, Java, Kotlin, Go, Haskell, Rust, Scala ...</td>
    </tr>
    <tr>
        <td>변수의 타입 변경 불가능, 타입에 일관성 부여</td>
    </tr>
    <tr>
        <td>타입에 맞는 값만 할당 가능</td>
    </tr>
    <tr>
        <td>컴파일 시점에 타입 체크, 에러 발생률 저하</td>
    </tr>
    <tr>
        <td>안정적인 코드의 구현</td>
    </tr>
    <tr>
        <td rowspan="5">동적 타입</td>
        <td rowspan="5">dynamic/weak type</td>
        <td>할당에 의해 타입이 결정, 타입 추론</td>
        <td rowspan="5">JavaScript, Python, PHP, Ruby, Lisp, Perl ...</td>
    </tr>
    <tr>
        <td>typeof 연산자로 타입 조사 가능</td>
    </tr>
    <tr>
        <td>자유롭게 할당 가능, 재할당 가능</td>
    </tr>
    <tr>
        <td>높은 유연성, 낮은 신뢰성</td>
    </tr>
</table>
