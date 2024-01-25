##### | 모던 자바스크립트 DeepDive <br />

###### range: 08. 제어문 <br />

###### date: day05(2024.01.10) <br />

<hr />
<br />

## 제어문

###### control flow statement

조건에 따라 실행문/반복문을 실행할 때 사용 <br />
코드의 흐름을 인위적으로 제어 ➡️ 가독성을 해침 ➡️ 사용 억제, 복잡성 해결 <br />

<br />

<table>
    <tr>
        <td rowspan='9'>제어문</td>
    </tr>
    <tr>
        <td rowspan='2'>조건문</td>
        <td rowspan='2'>조건식 결과에 따라 코드 실행을 결정</td>
        <td>if ... else</td>
        <td>논리적 결과에 따라 실행할 코드 결정 시 사용</td>
    </tr>
    <tr>
        <td>switch</td>
        <td>다양한 상황에 따라 실행할 코드 결정 시 사용</td>
    </tr>
    <tr>
        <td rowspan='3'>반복문</td>
        <td rowspan='3'>참인 조건식의 코드를 거짓이 될 때까지 실행</td>
        <td>for ⭐️</td>
        <td>반복 횟수가 명활할 때 사용</td>
    </tr>
    <tr>
        <td>while</td>
        <td>반복 횟수가 불명확할 때 사용</td>
    </tr>
    <tr>
        <td>do ... while</td>
        <td>블록을 먼저 실행, 조건식 평가</td>
    </tr>
    <tr>
        <td>break 문</td>
        <td colspan="3">레이블 문, 반복문, switch 문에서만 사용. fall through 방지</td>
    </tr>
    <tr>
        <td rowspan="2">continue 문</td>
        <td colspan="3">반복문의 코드 실행을 중단하고 반복문의 증감식으로 실행 흐름을 이동</td>
    </tr>
    <tr>
        <td colspan="3">if 문 내 실행 코드가 한 줄일 경우 사용 👍🏻, 길 경우 들여쓰기가 추가되므로 비추</td>
    </tr>
</table>

<br />

#### | 문 별 예외 상황

switch 문에서 break을 생략한 폴스루가 유용한 경우 <br />
대부분의 if ... else 문은 삼항 연산자로 변환 가능 <br />
레이블 문은 중첩된 for 문의 탈출에 용이하지만 그 외 사용은 권장 X <br />
