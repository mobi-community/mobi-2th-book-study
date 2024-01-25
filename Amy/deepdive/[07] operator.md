##### | 모던 자바스크립트 DeepDive <br />

###### range: 07. 연산자 <br />

###### date: day04(2024.01.08) <br />

<hr />
<br />

## 연산자?

- operator 연산자 : 하나 이상의 표현식을 대상으로 연산을 수행해 하나의 값 생성
- operend 피연산자 : 값으로 평가될 수 있는 표현식으로 연산의 대상

<br />

### | 산술

###### arithmetic

수학적 계산을 수행해 새로운 숫자 값 생성 <br />
산술이 불가한 경우, NaN <br />

증가/감소 연산자(++/--)는 피연산자의 값을 변경하는 부수 효과가 있다 <br />
숫자 타입이 아닌 피연산자에 + 단항 연산자를 사용 시 **암묵적 타입 변환(강제 타입 변환)** <br />

<table align="center">
    <tr>
        <td colspan="6">산술</td>
    </tr>
    <tr>
        <td colspan="3">이항</td>
        <td colspan="3">단항</td>
    </tr>
    <tr>
        <td>기호/부호</td>
        <td>의미</td>
        <td>부수 효과</td>
        <td>기호/부호</td>
        <td>의미</td>
        <td>부수 효과</td>
    </tr>
        <tr>
        <td>+</td>
        <td>덧셈</td>
        <td>X</td>
        <td>++</td>
        <td>증가</td>
        <td>O</td>
    </tr>
    </tr>
        <tr>
        <td>-</td>
        <td>뺄셈</td>
        <td>X</td>
        <td>--</td>
        <td>감소</td>
        <td>O</td>
    </tr>
    </tr>
        <tr>
        <td>*</td>
        <td>곱셈</td>
        <td>X</td>
        <td>+</td>
        <td>문자열 연결 가능</td>
        <td>X</td>
    </tr>
    </tr>
        <tr>
        <td>/</td>
        <td>나눗셈</td>
        <td>X</td>
        <td>-</td>
        <td>양수 ↔️ 음수를 반전한 값 반환</td>
        <td>X</td>
    </tr>
    </tr>
        <tr>
        <td>%</td>
        <td>나머지</td>
        <td>X</td>
        <td rowspan="3"></td>
    </tr>
</table>

<br />

### | 힐딩

###### assignment

<table align="center">
    <tr>
        <td colspan="4">할당</td>
    </tr>
    <tr>
        <td>기호/부호</td>
        <td>ex.</td>
        <td>동일 표현</td>
        <td>부수 효과</td>
    </tr>
        <tr>
        <td>=</td>
        <td>x = 5</td>
        <td></td>
        <td rowspan="6">O</td>
    </tr>
        <tr>
        <td>+=</td>
        <td>x += 5</td>
        <td>x = x + 5</td>
    </tr>
        <tr>
        <td>-=</td>
        <td>x -= x</td>
        <td>x = x - 5</td>
    </tr>
        <tr>
        <td>*=</td>
        <td>x =* 5</td>
        <td>x = x * 5</td>
    </tr>
        <tr>
        <td>/=</td>
        <td>x /= 5</td>
        <td>x = x / 5</td>
    </tr>
        <tr>
        <td>%=</td>
        <td>x %= 5</td>
        <td>x = x % 5</td>
    </tr>
</table>

<br />

### | 비교

###### comparison

좌항과 우항의 피연산자를 비교해 true/false 값을 반환 <br />
if 문이나 for 문과 같은 제어문과 조건문에서 주로 사용 <br />
동등 비교 시 먼저 암묵적 타입 변환을 통해 타입을 일치 시킨 후 값 비교 <br />
NaN은 자기 자신과 일치하지 않는 유일한 값 👉 일치 비교 시 Number.isNaN 사용 <br />
숫자 0에는 음의 0, 양의 0이 각각 존재하는데 비교 시 true를 반환

<table align="center">
    <tr>
        <td colspan="5">비교</td>
    </tr>
    <tr>
        <td colspan="5">동등/일치</td>
    </tr>
    <tr>
        <td>기호/부호</td>
        <td>의미</td>
        <td>ex.</td>
        <td>설명</td>
        <td>부수효과</td>
    </tr>
    <tr>
        <td>==</td>
        <td>동등 비교</td>
        <td>x == y</td>
        <td>값이 같음</td>
        <td rowspan="4">X</td>
    </tr>
    <tr>
        <td>===</td>
        <td>일치 비교</td>
        <td>x === y</td>
        <td>값과 타입이 모두 같음</td>
    </tr>
    <tr>
        <td>!=</td>
        <td>부동등 비교</td>
        <td>x != y</td>
        <td>값이 다름</td>
    </tr>
    <tr>
        <td>!==</td>
        <td>불일치 비교</td>
        <td>x !== y</td>
        <td>값과 타입이 모두 다름</td>
    </tr>
    <tr>
        <td colspan="5">대소관계</td>
    </tr>
    <tr>
        <td>>, ></td>
        <td colspan="2">x < y</td>
        <td>보다 크다/작다</td>
        <td rowspan="2">X</td>
    </tr>
    <tr>
        <td>>=, <=</td>
        <td colspan="2">x < y</td>
        <td>같거나 크다/작다</td>
    </tr>
</table>

<br />

### | 삼항 조건

###### ternary

삼항 조건 연산자 표현식은 값으로 평가될 수 있는 표현식인 문이기 때문에 다른 표현식의 일부가 될 수 있어 매우 유용 <br />
조건에 따라 수행해야 할 문이 하나라면 삼항 조건 연산자로, 여러 개라면 if ... else

<p align="center">
    <img src="https://github.com/mobi-community/mobi-2th-book-study/assets/134191817/e94618a9-2a0c-4fe7-9696-915fd62749e2" />
</p>

<br />

### | 논리

###### logical

논리 부정 연산자는 언제나 불리언 값을 반환

<table align="center">
    <tr>
        <td colspan="3">논리</td>
    </tr>
    <tr>
        <td>기호/부호</td>
        <td>의미</td>
        <td colspan="3">부수효과</td>
    </tr>
    <tr>
        <td>||</td>
        <td>논리합, OR</td>
        <td>X</td>
    </tr>
    <tr>
        <td>&&</td>
        <td>논리곱, AND</td>
    </tr>
    <tr>
        <td>!</td>
        <td>부정, NOT</td>
    </tr>
</table>

```
    드 모르간의 법칙

    복잡한 논리 연산자 표현식을 더 가독성 좋은 표현식으로 변환 가능

    !(x || y) === (!x && !y)
    !(x && y) === (!x || !y)

```

<br />

### | typeof

###### type of

피연산자의 데이터 타입을 문자열로 반환, 7개의 데이터 타입과 정확한 일치 X <br />

```
typeof ''               // "string"
typof NaN               // "number"
typof undefined         // "undefined"
typeof []               // "object"
typeof {}               // "object"
typeof null             // "object"
typeof new Date()       // "object"
```

null 👉 "object" \* 자바스크립트의 첫 번째 버그 <br />
값이 null 타입인지 확인하기 위해서는 일치 연산자를 사용해야 한다.

<br />

### | 지수

###### exponent

좌항을 밑(base)으로 우항을 지수로 거듭 제곱해 숫자 값 반환 <br />
ES7에 도입된 지수 이전에는 Math.pow 메서드를 사용

```

    // **

        2 ** 2      ➡️  4
        1 ** -2     ➡️  0.25

        let num = 5;
        num ** = 2      ➡️  25


    // Math.pow

        Math.pow(2,2)       ➡️  4
        Math.pow(2,-2)      ➡️  0.25

```

<br />

### | 그 외

<table align="center">
    <tr>
        <td colspan="3">그 외</td>
    </tr>
    <tr>
        <td>부호/기호</td>
        <td>개요</td>
        <td>비고</td>
    </tr>
    <tr>
        <td>?.</td>
        <td>옵셔널 체이닝 연산자</td>
        <td>9장</td>
    </tr>
    <tr>
        <td>??</td>
        <td>null 병합 연산자</td>
        <td>9장</td>
    </tr>
    <tr>
        <td>delete</td>
        <td>프로퍼티 삭제</td>
        <td>10장</td>
    </tr>
    <tr>
        <td>new</td>
        <td>생성자 함수를 호출할 때 사용해 인스턴스를 생성</td>
        <td>17장</td>
    </tr>
    <tr>
        <td>instanceof</td>
        <td>좌변의 객체가 우변의 생성자 함수와 연결된 인스턴스인지 판별</td>
        <td>19장</td>
    </tr>
    <tr>
        <td>in</td>
        <td>프로퍼티 존재 확인</td>
        <td>19장</td>
    </tr>
</table>

<br />
