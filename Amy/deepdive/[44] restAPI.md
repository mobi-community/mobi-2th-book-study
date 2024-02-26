##### | 모던 자바스크립트 DeepDive <br />

###### range: 43. REST API <br />

###### date: day29 (2024.02.26) <br />

<hr />
<br />

## REST API

REST는 HTTP를 기반으로 클라이언트가 서버의 리소스에 접근하는 방식을 규정한 아키텍처.<br />
REST API는 REST를 기반으로 서비스 API를 구현한 것.

<br />

### REST API의 구성

<table>
    <tr>
        <td>구성 요소</td>
        <td>내용</td>
        <td>표현 방법</td>
    </tr>
        <tr>
        <td>resource(자원)</td>
        <td>자원</td>
        <td>URI (endpoint)</td>
    </tr>
        <tr>
        <td>verb(행위)</td>
        <td>자원에 대한 행위</td>
        <td>HTTP 요청 메서드</td>
    </tr>
        <tr>
        <td>representations(표현)</td>
        <td>자원에 대한 행위의 구체적인 내용</td>
        <td>payload</td>
    </tr>
</table>

<br />

### REST API 설계 원칙

1️⃣ **URI는 리소스를 표현해야 한다**

리소스를 식별할 수 있는 이름은 동사보다는 명사 권장. <br />
따라서 이름에 행위에 대한 표현이 들어가서는 안 됨. <br />

2️⃣ **리소스에 대한 행위는 HTTP 메서드로 표현**

HTTP 요청 메서드는 클라이언트가 서버에게 요청의 종류와 목적을 알리는 방법. <br />
주로 5가지를 사용해 CRUD를 구현. <br />

<table>
    <tr>
        <td>HTTP 요청 메서드</td>
        <td>종류</td>
        <td>목적</td>
        <td>페이로드</td>
    </tr>
    <tr>
        <td>GET</td>
        <td>index/retrieve</td>
        <td>모든/특정 리소스 취득</td>
        <td>X</td>
    </tr>
    <tr>
        <td>POST</td>
        <td>create</td>
        <td>리소스 생성</td>
        <td>O</td>
    </tr>
    <tr>
        <td>PUT</td>
        <td>replace</td>
        <td>리소스 전체 교체</td>
        <td>O</td>
    </tr>
    <tr>
        <td>PATCH</td>
        <td>modify</td>
        <td>리소스 일부 수정</td>
        <td>O</td>
    </tr>
    <tr>
        <td>DELETE</td>
        <td>delete</td>
        <td>모든/특정 리소스 삭제</td>
        <td>X</td>
    </tr>
</table>

<br />

###
