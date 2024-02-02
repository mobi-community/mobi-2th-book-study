##### | 모던 자바스크립트 DeepDive <br />

###### range: 17. 생성자 함수에 의한 객체 생성 <br />

###### date: day13 (2024.02.02) <br />

<hr />
<br />

## Object 생성자 함수

new 연산자와 함께 호출하여 빈 객체(인스턴스)를 생성하는 함수

**생성자 함수** <br />

객체 리터럴을 사용한 객체 생성 방식은 매우 편리하고 가장 일반적으로 사용되는 방법


```javascript
const circle = {
  raduis: 5
} // 객체 리터럴로 생성하는 방식
```

하지만 객체 리터럴에 의한 객체 생성 방식의 문제점이 존재

1. 중복을 처리하기 어려움
2. 캡슐화가 불가능
3. 프로토타입 상속이 복잡해짐

<br />

**생성자 함수** <br />

생성자 함수는 new 키워드를 사용하여 인스턴스를 생성할 수 있는 함수

이 함수를 호출하면 this 바인딩을 통해 새 객체가 생성되고, 이 객체는 함수의 프로토타입을 상속 <br />
생성자 함수는 일반적으로 첫 글자를 대문자로 작성하여 다른 개발자에게 생성자 함수임을 알림 <br />

생성자 함수로 객체를 만들면, 재사용성, 프로토타입 기반 상속, 캡슐화의 장점

```javascript
function Person(name) {
  this.name = name; // 재사용성
  let age = 0; // 캡슐화

  this.getAge = function() { // 캡슐화된 속성에 대한 접근자
    return age;
  }

  this.birthday = function() { // 캡슐화된 속성을 수정하는 메서드
    age++;
  }
}

Person.prototype.greet = function() { // 프로토타입 기반 상속
  console.log(`Hello, my name is ${this.name}`);
}

let person1 = new Person('John');
let person2 = new Person('Jane');

person1.greet(); // "Hello, my name is John"
person2.greet(); // "Hello, my name is Jane"

console.log(person1.getAge()); // 0
person1.birthday();
console.log(person1.getAge()); // 1
```

<br />
