##### | 모던 자바스크립트 DeepDive <br />

###### range: 16. 프로퍼티 어트리뷰트 <br />

###### date: day12 (2024.01.00) <br />

<hr />
<br />

## property attr & descriptor

**property attr** <br />

프로퍼티의 상태를 나타냄 <br />
어트리뷰트 생성 시 자동 정의 <br />

**property descriptor** <br />

프로퍼티 어트리뷰트의 정보 제공 <br />

<br />

<table>
    <tr>
        <td>property</td>
        <td>설명</td>
        <td>종류</td>
    </tr>
    <tr>
        <td>data</td>
        <td>키와 값으로 구성된 일반적인 프로퍼티</td>
        <td>[[Value]], [[Writable]], [[Enumerable]], [[Configurable]]</td>
    </tr>
    <tr>
        <td>accessor</td>
        <td>자체적인 값 X, 데이터 프로퍼티의 값을 읽거나 저장할 때 호출되는 접근자 함수로 구성된 프로퍼티</td>
        <td>[[Get]], [[Set]], [[Enumerable]], [[Configurable]]</td>
    </tr>
</table>

**property ?**

프로퍼티 정의란 새로운 프로퍼티를 추가하면서 프로퍼티 어트리뷰트를 명시적으로 정의하거나 기존 프로퍼티의 어트리뷰트를 재정의하는 것 <br />

Object.defineProperty 메서드를 사용 <br />
인수로는 객체의 참조와 데이터 프로퍼티(키), 프로퍼티 디스크립터 객체 전달

<br />

<table>
    <tr>
        <td>property descriptor 객체의 프로퍼티</td>
        <td>대응하는 프로퍼티 attr</td>
        <td>생략 시 기본값</td>
    </tr>
    <tr>
        <td>value</td>
        <td>[[Value]]</td>
        <td rowspan="3">undefined</td>
    </tr>
    <tr>
        <td>get</td>
        <td>[[Get]]</td>
    </tr>
    <tr>
        <td>set</td>
        <td>[[Set]]</td>
    </tr>
    <tr>
        <td>writable</td>
        <td>[[Writable]]</td>
        <td rowspan="3">false</td>
    </tr>
    <tr>
        <td>enumerable</td>
        <td>[[Enumerable]]</td>
    </tr>
    <tr>
        <td>configurable</td>
        <td>[[Configurable]]</td>
    </tr>
</table>

<br />

## 객체 변경 방지

객체는 변경 가능한 값이므로 재할당 없이 직접 변경 가능 <br />
프로퍼티 추가/삭제 가능, 갱신 및 재정의 가능 <br />
객체 변경 방지를 위한 다양한 메서드들을 제공하는데 각 금지 정도가 다름 <br />

<table>
    <tr>
        <td>구분</td>
        <td>메서드</td>
        <td>프로퍼티 추가</td>
        <td>프로퍼티 삭제</td>
        <td>프로퍼티 읽기</td>
        <td>프로퍼티 쓰기</td>
        <td>프로퍼티 재정의</td>
    </tr>
        <tr>
        <td>객체 확장 금지</td>
        <td>Object.preventExtensions</td>
        <td>X</td>
        <td colspan="4">O</td>
    </tr>
        <tr>
        <td>객체 밀봉</td>
        <td>Object.seal</td>
        <td>X</td>
        <td>X</td>
        <td>O</td>
        <td>O</td>
        <td>X</td>
    </tr>
        <tr>
        <td>객체 동결</td>
        <td>Object.freeze</td>
        <td>X</td>
        <td>X</td>
        <td>O</td>
        <td>X</td>
        <td>X</td>
    </tr>
</table>
