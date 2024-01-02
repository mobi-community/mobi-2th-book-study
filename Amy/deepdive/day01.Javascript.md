##### | 모던 자바스크립트 DeepDive <br />
###### range: 01. 프로그래밍, 02. 자바스크립트란?, 03. 자바스크립트 개발 환경과 실행 방법 <br />
###### date: day01(2024.01.02) <br />
<hr />
<br />

## Programming?
<br />
프로그래밍이란 요구사항의 집합을 분석해서 적절한 자료 구조와 함수의 집합으로 변환한 후, 그 흐름을 제어하는 것 <br />

<br />
컴퓨터에게 실행을 요구하는 커뮤니케이션으로 정확하고 상세하게 요구사항을 설명하는 직업으로 그 결과가 코드로 나타난다. <br />
<br />

<table align="center">
    <tr>
    <td> 능력 </td>
    <td colspan="2"> 설명 </td>
    <td> 비고 </td>
  </tr>
  <tr>
    <td rowspan="6"> 문제 해결 능력 </td>
    <td colspan="2"> 요구사항(해결해야 할 문제)를 명확히 이해하기  </td>
    <td rowspan="6"> 직감과 직관의 영역 </td>
  </tr>
  <tr >
    <td rowspan="5" > 문제 해결 순서  </td>
    <td> 1. 문제의 명확한 이해  </td>
  </tr>
  <tr >
    <td> 2. 복잡함을 단순하게 분해  </td>
  </tr>
  <tr >
    <td> 3. 자료 정리  </td>
  </tr>
  <tr >
    <td> 4. 구분  </td>
  </tr>
  <tr >
    <td> 5. 순서에 맞게 행위 배열  </td>
  </tr>
  <tr>
    <td rowspan="5" > 컴퓨팅 사고 </td>
    <td colspan="2"> 해결 방안 고려 시 컴퓨터의 입장에서 바라보기  </td>
    <td rowspan="5"> 사고와 경험에 영향 </td>
  </tr>
  <tr>
    <td rowspan="4"> 사고하는 순서  </td>
    <td> 1. 해결 과제를 작은 단위로 분해  </td>
  </tr>
  <tr>
    <td> 2. 패턴화  </td>
  </tr>
  <tr>
    <td> 3. 추출  </td>
  </tr>
  <tr>
    <td> **프로그래밍 내에서 사용될 모든 개념은 평가 가능하도록 </td>
  </tr>
</table>
<br />

#### 어떻게 해결방안을 컴퓨터에 전달하나?

<p align="center">
<img width="80%" src="https://github.com/mobi-community/mobi-2th-book-study/assets/134191817/5a4f3496-c5e4-4e58-b335-fc4ca064bd1b" />
</p>
<br />

언어는 자연어와 인공어로 구분할 수 있다. <br />
프로그래밍 언어는 사람과 컴퓨터 모두가 이해할 수 있는 약속된 형태의 인공어이다.


####  프로그래밍 언어는 구문과 언어의 조합으로 표현되므로 의미(semantics)를 갖는 동시에 문법(syntax)에 맞는 문장을 구성을 이룰 것   

<br />


## Javascript?

1. 웹 브라우저에서 동작하는 유일한 프로그래밍 언어
2. 개발자가 별도의 컴파일 작업을 수행하지 않는 인터프리터 언어
3. 프로토타입 기반의 객체 지향 언어
4. 멀티 패러다임 프로그래밍 언어

크로스 브라우징 이슈를 해결하기 위해 등장
크로스 브라우징 이슈 : 브라우저에 따라 웹 페이지가 정상적으로 동작하기 않는 현상
모든 브라우저에서 정상 동작하는 웹 페이지의 개발이 어려워짐

1999년, Javascript  ECMA에 표준화 신청

<p align="center">
  <img width="30%" src="https://github.com/mobi-community/mobi-2th-book-study/assets/134191817/ac0e6dfe-a6a3-4198-a0ef-143ee89ae513" />
</p>

Ajax  JS를 이용해 서버의 브라우저가 비동기 방식으로 데이터를 교환할 수 있는 통신 기능 등장

2006년, jQuery  DOM을 더욱 쉽게 제어가 가능

2009년, Node.js  구글 v8 자바스크립트 엔진으로 빌트된 JS 런타임 환경
                 자바스크립트 엔진을 브라우저로부터 독립
                 프론트엔드와 백엔드 영역 모두 JS를 사용할 수 있게 되면서 통형성을 갖게 됨


SPA framework  모든 웹 애플리케이션의 상용화로 많은 패턴과 라이브러리 등장
                애플리케이션 아키텍처의 구축을 위해 등장
                CBD 방법론 기반의 SPA framework 대중화
                ex. Angular, React, Vue, Svelte ...




## Javascript 개발 환경과 실행 방법

<p align="center">
  <img width="50%" src="https://github.com/mobi-community/mobi-2th-book-study/assets/134191817/af669560-1cd9-4496-b842-e027cfd10ec9" />
</p>
                
