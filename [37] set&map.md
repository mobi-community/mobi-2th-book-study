##### | 모던 자바스크립트 DeepDive <br />

###### range: 37. set과 map <br />

###### date: day24 (2024.02.21) <br />

<hr />
<br />

## Set

set 객체는 중복되지 않는 유일한 값들의 집합이다.<br />

<table>
    <tr>
        <td>차이</td>
        <td>Array</td>
        <td>Set object</td>
    </tr>
    <tr>
        <td>동일한 값의 중복 포함 가능 여부</td>
        <td>O</td>
        <td>X</td>
    </tr>
    <tr>
        <td>요소 순서에 의미 여부</td>
        <td>O</td>
        <td>X</td>
    </tr>
    <tr>
        <td>인덱스로 요소 접근 가능 여부</td>
        <td>O</td>
        <td>X</td>
    </tr>
</table>

### Set 객체 생성

set 생성자 함수는 이터러블을 인수로 전달받아 set 객체를 생성. <br />
이때 이터러블의 중복된 값은 set 객체에 요소로 저장되지 않음.

```javascript
const set = new Set();
```

### 요소 개수 확인

size 프로퍼티를 사용해 확인 가능하다.
getter 함수만 존재하는 접근자 프로퍼티이므로 개수 변경은 불가능하다.

```javascript
const { size } = new Set([1, 2, 3, 3]);
console.log(size); // 3
```

### 요소 추가

add 메서드를 사용해 추가 가능하다. <br />
add 메서드는 연속적으로 호출 가능하다. <br />
이때 중복된 요소의 추가는 허용되지 않는데 에러가 발생하지는 않고 무시된다.

```javascript
const set = new Set();
set.add(1);

console.log(set); // Set(1) {1}
```

### 요소 존재 여부 확인

```javascript
const set = new Set([1, 2, 3]);

console.log(set.has(2)); // true
```

### 요소 삭제

존재하지 않는 요소를 지우려고 하면 무시된다.<br />
delete 메서드는 삭제 성공 여부를 불리언 타입으로 반환.<br />
add처럼 연속적으로 호출하는 것은 불가능하다.

```javascript
const set = new Set([1, 2, 3]);
set.delete(0);
set.delete(1);
```

### 요소 일괄 삭제

clear 메서드는 언제나 undefined 반환

```javascript
const set = new Set([1, 2, 3]);
set.clear();
```

### 요소 순회

첫 번째 인수 : 현재 순회 중인 요소 값 <br />
두 번째 인수 : 현재 순회 중인 요소 값 <br />
세 번째 인수 : 현재 순회 중인 객체 자체 <br />

```javascript
const set = new Set([1, 2, 3]);

set.forEach((v, v2, set) => console.log(v, v2, set));
/* 
    1 1 set(3){1,2,3} 
    2 2 set(3){1,2,3}
    3 3 set(3){1,2,3}
*/
```

### 집합 연산

set 객체는 수학적 집합을 구현하기 위한 자료구조 <br />
집합 연산을 수행하는 프로토타입 메서드를 구현하면 아래와 같다.

```javascript
// 교집합

// 1️⃣
Set.prototype.intersection = function (set) {
  const result = new Set();

  // 2개의 set 요소가 공통되는 요소를 모아
  for (const value of set) {
    if (this.has(value)) result.add(value);
  }
  return result;
};

// 2️⃣
Set.prototype.intersection = function (set) {
  return new Set([...this].filter((v) => set.has(v)));
};
```

```javascript
// 합집합

// 1️⃣
Set.prototype.union = function (set) {
  // this(set객체) 복사
  const result = new Set(result);

  for (const value of set) {
    // 두 개의 집합 중 중복되는 요소를 제외한 모든 요소
    result.add(value);
  }
  return result;
};

// 2️⃣
Set.prototype.union = function (set) {
  return new Set([...this, ...set]);
};
```

```javascript
// 차집합

// 1️⃣
Set.prototype.difference = function (set) {
  // this(set 객체) 복사
  const result = new Set(this);

  for (const value of set) {
    // 어느 한쪽에만 존재하는 요소
    result.delete(value);
  }
  return result;
};

// 2️⃣
Set.prototype.difference = function (set) {
  return new set([...this].filter((v) => !set.has(v)));
};
```

```javascript
// 한 집합이 다른 집합 안에 포함되는 경우
// 부분 집합 (포함이 된 집합) & 상위 집합 (포함 한 집합)

// 상위 집합인지 확인
// 1️⃣
Set.prototype.isSuperset = function (subset) {
  for (const value of subset) {
    // superset의 모든 요소가 subset의 모든 요소를 포함하는지 확인
    if (!this.has(value)) return false;
  }
  return true;
};

// 2️⃣
Set.prototype.isSuperset = function (subset) {
  const supersetArr = [...this];
  return [...subset].every((v) => supersetArr.includes(v));
};
```

<br />

## Map

Map 객체는 키와 값의 쌍으로 이뤄진 컬렉션.<br />

<table>
    <tr>
        <td>차이</td>
        <td>Object</td>
        <td>Map object</td>
    </tr>
    <tr>
        <td>key로 사용 가능한 값</td>
        <td>string || symbol</td>
        <td>객체를 포함한 모든 값</td>
    </tr>
    <tr>
        <td>이터러블</td>
        <td>X</td>
        <td>O</td>
    </tr>
    <tr>
        <td>요소 개수 확인</td>
        <td>Object.keys(obj).length</td>
        <td>map.size</td>
    </tr>
</table>

<br />

### Map 객체 생성

Map 생성자 함수는 이터러블을 인수로 받아 Map 객체 생성. <br />
이때 인수로 전달되는 이터러블은 키와 값의 쌍으로 이뤄진 요소로 구성돼 있어야 한다. <br />

```javascript
const map = new Map();
const map = new Map([
  ["key1", "value1"],
  ["key2", "value2"],
]);
```

### 요소 개수 확인

```javascript
const { size } = new Map([
  ["key1", "value1"],
  ["key2", "value2"],
]);

console.log(size); // 2
```

### 요소 추가

set 메서드는 연속적으로 호출 가능

```javascript
const map = new Map();
map.set("key1", "value1");
map.set("key1", "value1").set("key2", "value2");
```

객체도 키로 사용 가능

```javascript
const map = new Map();

const Lee = { name: "lee" };
map.set(lee, "developer");

console.log(map);
// Map(1){{name: 'lee'} => developer}
```

### 요소 취득

```javascript
console.log(map.get(lee)); // developer
```

### 요소 존재 여부 확인

```javascript
console.log(map.has(lee)); // true
```

### 요소 삭제

delete 메서드를 연속적으로 호출할 수 없다.

```javascript
map.delete(lee);
```

### 요소 일괄 삭제

```javascript
map.clear();
```

### 요소 순회

첫 번재 인수 : 현재 순회 중인 요소 값 <br />
두 번째 인수 : 현재 순회 중인 요소 키 <br />
세 번째 인수 : 현재 순회 중인 Map 객체 자체 <br />

```javascript
const lee = { name: "lee" };
const kim = { name: "kim" };

const map = new Map([
  [lee, "developer"],
  [kim, "designer"],
]);

map.forEach((v, k, map) => console.log(v, k, map));
/* 
    developer {name: 'lee'} Map(2) {
        {name: 'lee'} => 'developer',
        {name: 'kim'} => 'designer'
    }
    designer {name: 'kim'} Map(2){
        {name: 'lee'} => 'developer',
        {name: 'kim'} => 'designer'
    }
*/
```

for ...of 문으로 순회 가능

```javascript
for (const entry of map) {
  console.log(entry);
}
// [{name: 'lee'}, "developer"] [{name: 'kim'}, 'designer']
```

Map 객체는 요소의 순서에 의미를 갖지 않지만 Map 객체를 순회하는 순서는 요소가 추가된 순서를 따른다. <br />
