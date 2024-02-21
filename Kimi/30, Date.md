> ✏️Date

###### 표준 빌트인 객체 Date
###### 날짜와 시간(연, 월, 일, 시, 분, 초, 밀리초)을 위한 메서드를 제공하는 빌트인 객체이면서 생성자 함수
###### UTC는 협정 세계시이다


# Date 생성자 함수

### new Date()

```jsx
//Date객체
new Date(); //-> Mon Jul 06 2020 01:03:23 GMT +0920 (대한민국 표준시)

//new 없이 호출 시 객체가 아닌 문자열 반환
Date(); //-> "Mon Jul 06 2020 01:03:23 GMT +0920 (대한민국 표준시)"
```

##### new Date(year, month[, day, hour, minute, second, millisecond])

![image](https://github.com/mobi-community/mobi-2th-book-study/assets/134191815/63c9b11f-ae7b-4b19-a6f5-5ee6406d759f)


# Date 메서드

### Date.now
1970년 1월 1일 00:00:00(UTC) 기점 현재 시간까지 경과한 밀리초를 숫자로 반환


### Date.parse
1970년 1월 1일 00:00:00(UTC) 기점 ~ 지정 시간까지의 밀리초를 숫자로 반환

### Date.UTC
1970년 1월 1일 00:00:00(UTC) 기점 ~ 지정 시간까지의 밀리초를 숫자로 반환


### Date.prototype.getFullYear
객체의 연도를 나타내는 정수를 반환

### Date.prototype.setFullyear
Date객체에 연도를 나타내는 정수 설정(옵션으로 월,일도 설정가능)

```jsx
const today = new Date();

//년도 지정
today.setFullYear(2000);
today.getFullYear(); //-> 2000

//년/월/일 지정
today.setFullYear(1990, 0, 1);
today.getFullYear(); //-> 1990
```

### Date.prototype.getMonth
Date 객체의 월을 나타내는 0~11정수를 반환

###### 1월은 0, 12월은 11이다.

### Date.prototype.setMonth
Date 객체에 월을 나타내는 0~11의 정수 설정

```jsx
const today = new Date();

//월 지정
today.setMonth(0); //1월
today.getMonth(0); //0


//월/일 지정
today.setMonth(11, 1); //12월 1일
today.getMonth(); //11
```

### Date.prototype.getDate
Date 객체의 날짜(1~31)를 나타내는 정수 반환


### Date.prototype.setDate
Date 객체의 날짜(1~31)를 나타내는 정수 설정
```jsx
const today = new Date();

//날짜 지정
today.setDate(1);
today.getDate(); //-> 1
```

### Date.prototype.getDay
Date 객체의 요일(0~6)을 나타내는 정수 반환</br>
일: 0, 월: 1, 화: 2~~~~~


###### 이런식으로 getHours, setHours, getMinutes, setMinutes, getSeconds, setSeconds, getMilliseconds, setMilliseconds, getTime, setTime, 이 있다


### Date.prototype.toDateString
```jsx
const today = new Date("2020/7/24/12:30");

today.toString(); //-> Fri Jul 24 2020 12:30:00 GMT +09:00 (대한민국 표준시)
today.toDateString(); //-> Fri Jul 24 2020 
```


### Date.prototype.toTimeString
```jsx
const today = new Date("2020/7/24/12:30");

today.toString(); //-> Fri Jul 24 2020 12:30:00 GMT +09:00 (대한민국 표준시)
today.toTimeString(); //-> 12:30:00 GMT +09:00 (대한민국 표준시)
```

### Date.prototype.toISOString
```jsx
const today = new Date("2020/7/24/12:30");

today.toString(); //-> Fri Jul 24 2020 12:30:00 GMT +09:00 (대한민국 표준시)
today.toISOString(); //-> 2020-07-24T03:30:000Z

today.toISOString().slice(0, 10); // -> 2020-07-24
today.toISOString().slice(0, 10).replace(/-/g, ''); //-> 20200724
```

### Date.prototype.toLocalString
```jsx
const today = new Date("2020/7/24/12:30");

today.toString(); //-> Fri Jul 24 2020 12:30:00 GMT +09:00 (대한민국 표준시)
today.toLocalString((); //-> 20220. 7. 24. 오후 12:30:00
```


### Date.prototype.toLocalTimeString
```jsx
const today = new Date("2020/7/24/12:30");

today.toString(); //-> Fri Jul 24 2020 12:30:00 GMT +09:00 (대한민국 표준시)
today.toLocalTimeString((); //-> 오후 12:30:00
```



