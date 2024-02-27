✏️REST API

###### HTTP의 장점을 최대한 활용할 수 있는 아키텍처
###### REST의 기본 원칙을 성실히 지킨 서비스 디자인 "RESTful"
###### REST: HTTP를 기반으로 클라이언트가 서버의 리소스에 접근하는 방식을 규정한 아키텍처
###### REST API: REST를 기반으로 서비스 API를 구현한 것

# 1, REST API의 구성
REST API는 자원, 행위, 표현 3가지 요소로 구성됨 </br>
REST는 자체 표현 구조로 구성되어 REST API만으로 HTTP 요청의 내용을 이해할 수 있다.


|구성 요소|내용|표현방법|
|------|---|---|
|자원 `resource`|자원|URI(엔드포인트)|
|행위 `verb`|자원에 대한 행위|HTTP 요청 메서드|
|표현 `representations`|자원에 대한 행위의 구체적 내용|페이로드|


# 2, REST API의 설계 원칙
#### URI는 리소스를 표현하는 데에 집중하고, 
#### 행위에 대한 정의는 HTTP 요청 메서드를 통해 하는 것이 RESTful API를 설계하는 중심 규칙


#### (1) URI는 리소스를 표현해야한다
리소스를 표현하는 데에 중점을 두기</br>
동사보다는 명사사용 </br>
이름에 get같은 행위에 대한 표현이 들어가서는 안됨
```
#good
GET / todos/1
```

#### (2) 리소스에 대한 행윈는 HTTP 요청 메서드로 표현한다

![image](https://github.com/mobi-community/mobi-2th-book-study/assets/134191815/d3aed10d-8e37-47ed-84cb-95e93af1a8be)

```
#good
DELETE / todos/1
```
