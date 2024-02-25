> ✏️Set과 Map

###### Set: 중복되지 않는 유일한 값들의 집합
###### Map: 키와 값의 쌍으로 이루어진 컬렉션


# Set
>수학적 집합을 구현하기 위한 자료구조 (이를 통해 교집합, 합집합, 차집합 여집합 구현 가능)

## Set 객체의 생성
Set생성자 함수로 생성

```jsx
//인수전달 안할 시 Set객체 생성
const set = new Set();
console.log(set); //Set(0) {}

//이터러블을 인수로 전달받아 객체 생성
const set1 = new Set([1, 2, 3, 4])
console.log(set1); //Set(3) {1, 2, 3}

const set2 = new Set('hello');
console.log(set2); //Set(4) {'h', 'e', 'l', 'o'}
```

 중복을 허용하지 않는 Set객체의 특성활용하여 배열에서 중복요소 제거 가능

```jsx
const uniq = arr => arr.filter((v, i, self) => self.indexOf(v) === i);
console.log(uniq([2,1,3,4,3,4])); // [2,1,3,4]

//Set을 이용
const uniq = arr => [...new Set(arr)];
console.log(uniq([2,1,2,3,4,3,4])); // [2,1,3,4]
```

## 요소 개수 확인

##### Set.pototype.size

```jsx
const { size } = new Set([1, 2, 3, 4]);
console.log(size); //3
```


## 요소 추가

##### Seet.prrototype.add

```jsx
const set = new Set();
console.log(set); //Set(0) {}

set.add(1);
console.log(set); //Set(1) {1}

//새로 호출된 요소 반환
set.add(2).add(3)
console.log(set); //Set(3) {1,2,3}
```

## 요소 존재 여부 화인

##### Set.prrototype.has

```jsx
const set = new Set([1, 2, 3]);

console.log(set.has(2)); //true
console.log(set.has(4)); //false
```

## 요소 삭제

##### Set.prototype.delete

add메서드와 달리 연속적 호출이 안된다.



## 요소 일괄 삭제


##### Set.prototype.clear

언제나 `undefined`를 반환



## 요소 순회

##### Set.prototype.forEach 

- 첫 번째 인수: 현재 순회 중인 요소값
- 두 번째 인수: 현재 순회 중인 요소값
- 세 번째 인수: 현재 순회 중인 Set 객체 자체

```jsx
const set = new Set([1, 2, 3]);

set.forEAch((v, v2, set) =>  console.log(v, v2, set));
/*
1 1 set(3) {1,2,3}
2 2 set(3) {1,2,3}
3 3 set(3) {1,2,3}
*/
```


### Set객체는 이터러블이다

`for...of`문과 `스프레드` 문법 사용이 가능하다.

```jsx
const set = new Set([1, 2, 3]);

for (const el of set) {
  console.log(el); // 1 2 3
}

console.log([...set]); // [1, 2, 3]

//이터러블인 Set객체는 배열 디스트럭처링 할당의 대상이 될 수 있다
const [a, ...rest] = set;
console.log(a, rest); //1, [2, 3]
```

# Map
Map 생성자 함수는 이터러블을 인수로 전달받아 Map함수 생성 </br>
이때 인수로 전달되는 이터러블은 키와 값의 쌍으로 이루어진 요소로 구성

## Map 객체의 생성
Map 생성자 함수로 생성

```jsx
const map = new Map();
console.log(map); //Map(0) {}

//키와 값의 쌍
const map1 = new Map([['key1', 'value1'], ['key2', 'value2']]);
console.log(map1); //Map(2) {'key1' => 'value1', 'key2' => 'value2'}
```

Map 객체에는 중복된 키를 갖는 요소가 존재할 수 없다.


## 요소의 개수 확인

##### Map.prototype.size



## 요소 추가

##### Map.prototype.set

```jsx
const map = new Map();


map
  .set('key1', 'value1')
  .set('key2', 'value2');

console.log(map); //Map(2) {'key1' => 'value1', 'key2' => 'value2'}
```


## 요소 취득

##### Map.prototype.get

```jsx
const map = new Map();

const lee = { name: 'Lee' };
const kim = { name: 'Kim' };


map
  .set(lee, 'developer')
  .set(kim, 'designer');

console.log(map.get(lee)); //developer
```

## 요소 존재 여부 확인

##### Map.prototype.has

```jsx
console.log(map.has(kim)); //true
```

## 요소 삭제

##### Map.prototype.delete

연속 호출 불가


## 일괄 삭제

##### Map.prototype.clear


## 요소 순회

##### Map.prototype.forEach

`for...of`와 `스프레드`문법 사용 가능

![image](https://github.com/mobi-community/mobi-2th-book-study/assets/134191815/2ff65026-805e-46b6-9cb9-0ebf3a3f60c0)

