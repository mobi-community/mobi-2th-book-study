##### | 모던 자바스크립트 DeepDive <br />

###### range: 04. 변수 <br />

###### date: day02(2024.01.04) <br />

<hr />
<br />

## Variable ?

<br />

변수란 하나의 값을 저장하기 위해 확보한 메모리 공간을 식별하기 위해 붙인 이름 <br />
값의 위치를 가리키는 상징적은 식별자로 이름을 지을 때에는 네이밍 규칙을 준수 <br />
선언을 통해 JS에 존재를 알림 <br />

```
    코드는 컴퓨터에게 내리는 명령이자 개발자를 위한 문서
    개발자의 의도를 나타내는 명확한 네이밍은 코드의 이해를 돕고 협업과 품질 향상에 도움
    변수 이름은 첫 아이의 이름을 짓듯이 심사숙고할 것
```

<details>
    <summary>네이밍 규칙</summary>
    <p> - 문자,숫자,언더스코어(_), 달러($) 사용 가능 (그 외 특수문자 X)</p>
    <p> - 숫자로 시작 X</p>
    <p> - 네이밍 컨벤션 지키기</p>
    <p> - 예약어 사용 X</p>
    <p>예약어의 종류</p>
    <table>
    <tr>
        <td>await</td>
        <td>break</td>
        <td>case</td>
        <td>catch</td>
        <td>class</td>
        <td>const</td>
    </tr>
    <tr>
        <td>continue</td>
        <td>debugger</td>
        <td>default</td>
        <td>delete</td>
        <td>do</td>
        <td>else</td>
    </tr>
    <tr>
        <td>enum</td>
        <td>export</td>
        <td>extends</td>
        <td>false</td>
        <td>finally</td>
        <td>for</td>
    </tr>
    <tr>
        <td>function</td>
        <td>if</td>
        <td>implements</td>
        <td>import</td>
        <td>in</td>
        <td>instanceof</td>
    </tr>
    <tr>
        <td>interface</td>
        <td>let</td>
        <td>new</td>
        <td>null</td>
        <td>package</td>
        <td>private</td>
    </tr>
    <tr>
        <td>protected</td>
        <td>public</td>
        <td>return</td>
        <td>super</td>
        <td>static</td>
        <td>switch</td>
    </tr>
    <tr>
        <td>this</td>
        <td>throw</td>
        <td>true</td>
        <td>try</td>
        <td>typeof</td>
        <td>var</td>
    </tr>
    <tr>
        <td>void</td>
        <td>while</td>
        <td>with</td>
        <td>yield</td>
        <td></td>
        <td></td>
    </tr>
    </table>
</details>
<details>
    <summary>식별자</summary>
    <br />
    <p> - 값이 아닌 메모리 주소를 기억</p>
    <p> - 메모리 주소에 붙인 이름</p>
    <p> - 메모리 상 존재하는 값을 식별할 수 있는 모든 이름</p>
</details>

## How to use Variable

선언 : 값을 저장하기 위한 메모리 공간을 확보 ➡️ 확보된 메모리 공간의 주소를 연결 ➡️ 값 저장

선언 시에는 var, let, const 키워드를 사용

```
왜 var는 지양하는가

블록 레벨 스코프가 아닌 함수 레벨 스코프 지원 ➡️ 의도치 않게 전역 변수가 선언 되어 예상치 못한 부작용 발생 가능성 농후

var 단점 보완을 위해 let, const 도입

```

<br />

1. 선언 단계 : 변수 이름 등록, JS 엔진에 변수의 존재 알림

2. 초기화 단계 : 값 저장을 위한 메모리 공간 확보, undifined로 초기화

3. 값 할당 : 연산자(=)를 통해 할당, 하나의 문으로 단축 표현 가능

4. 재할당 : 변수인 let 가능, 상수인 const 불가능

<br />

1과 2는 동시에 진행되며 단축시켜 표현해도 선언과 할당을 나눠 실행 <br />
선언과 초기화 단계는 런타임 이전에 실행되며 값의 할당은 런타임에 실행 <br />

---

### 네이밍 컨벤션

```

 카멜 케이스 (camelCase)
 let firstName;

 스네이크 케이스 (snake_case)
 let first_name;

 파스칼 케이스 (PascalCase)
 let FirstName;

 헝가리언 케이스 (type + identifier)
 let strFirstName;

```

일관성만 유지된다면 크게 상관 없지만 일반적으로는 아래와 같이 사용

변수, 함수명 : 카멜케이스 <br />
셍상지 힘수, 클래스명 : 파스칼 케이스 <br />
