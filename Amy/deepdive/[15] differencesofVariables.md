##### | 모던 자바스크립트 DeepDive <br />

###### range: 15. let, const 키워드와 블록 레벨 스코프 <br />

###### date: day11 (2024.01.27) <br />

<hr />
<br />

## 변수를 선언하는 키워드별 차이

var의 문제점

- 중복 선언 허용으로 의도치 않게 먼저 선언된 변수 값이 변경될 우려
- 함수 외부의 변수는 모두 전역으로 취급,
  의도치 않게 전역 변수가 중복 선언될 우려 + 전역 변수의 남발

- 변수 호이스팅이 발생하므로 스코프의 선두로 끌어 올려져 동작
  변수 선언문 이전에 참조하게 될 경우 언제나 undefined 반환

<br />

<table>
    <tr>
        <td>keyword</td>
        <td>var</td>
        <td>let</td>
        <td>const</td>
    </tr>
    <tr>
        <td>중복 가능 여부</td>
        <td>O</td>
        <td>X</td>
        <td>X</td>
    </tr>
    <tr>
        <td>재할당 가능 여부</td>
        <td>O</td>
        <td>O</td>
        <td>X</td>
    </tr>
    <tr>
        <td>변수 호이스팅</td>
        <td>O</td>
        <td colspan="2">O (x)</td>
    </tr>
    <tr>
        <td>스코프 범위</td>
        <td>함수 레벨</td>
        <td colspan="2">블록 레벨</td>
    </tr>
</table>

<br />

## 변수 선언 시 주의사항

- ES6 이후부터는 var 사용 지양
- 재할당이 필요한 경우에 한 해 let 사용, 이때 스코프는 최대한 좁게 할 것
- 안정성을 위해 읽기 전용 값과 원시 값, 객체에는 const 사용
