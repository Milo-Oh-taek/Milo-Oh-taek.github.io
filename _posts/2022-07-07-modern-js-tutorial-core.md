---
title: modern js tutorial obj
date: 2022-07-07 21:30:00 +09:00
categories: [JS]
tags: [javascript]
---

## 객체
### computed property
객체 프로퍼티 키가 대괄호로 둘러싸여 있는 경우   
`````
let fruit = prompt("어떤 과일을 구매하시겠습니까?", "apple");

let bag = {
  [fruit]: 5, // 변수 fruit에서 프로퍼티 이름을 동적으로 받아 옵니다.
};

alert( bag.apple ); // fruit에 "apple"이 할당되었다면, 5가 출력됩니다.
`````
`````
let fruit = 'apple';
let bag = {
  [fruit + 'Computers']: 5 // bag.appleComputers = 5
};
`````
### 'in'연산자로 객체 프로퍼티 존재 확인   
`````
let user = { name: "John", age: 30 };

alert( "age" in user ); // user.age가 존재하므로 true가 출력됩니다.
alert( "blabla" in user ); // user.blabla는 존재하지 않기 때문에 false가 출력됩니다.
`````

### 객체의 복사
#### for문 복사
`````
let user = {
  name: "John",
  age: 30
};

let clone = {}; // 새로운 빈 객체

// 빈 객체에 user 프로퍼티 전부를 복사해 넣습니다.
for (let key in user) {
  clone[key] = user[key];
}

// 이제 clone은 완전히 독립적인 복제본이 되었습니다.
clone.name = "Pete"; // clone의 데이터를 변경합니다.

alert( user.name ); // 기존 객체에는 여전히 John이 있습니다.
`````

#### Object.assign 복사
`````
let user = { name: "John" };

let permissions1 = { canView: true };
let permissions2 = { canEdit: true };

// permissions1과 permissions2의 프로퍼티를 user로 복사합니다.
Object.assign(user, permissions1, permissions2);

// now user = { name: "John", canView: true, canEdit: true }
`````

**위 두 방법 모두 객체의 모든 프로퍼티가 원시값일 경우만 가능하다.**   
**객체 안에 또 다른 객체 형태가 존재한다면 깊은복사 알고리즘 구현 or lodash의  _.cloneDeep(obj)이용**

### 가비지 컬렉션
garbage collector은 끊임없이 동작하며 모든 객체를 모니터링하고, 도달할 수 없는 객체는 삭제한다.   

#### mark-and-sweep
- 가비지 컬렉터는 루트 정보를 수집하고 이를 mark 한다.
- 루트가 참조하고 있는 모든 객체를 방문하고 이것들을 mark 한다.
- mark된 모든 객체에 방문하고 그 객체들이 참조하는 객체도 mark 한다.
- 한번 방문한 객체는 전부 mark하기에 같은 객체를 다시 방문하는 일은 없다.
- 루트에서 도달 가능한 모든 객체를 방문할 때까지 위 과정을 반복한다.
- mark 되지 않은 모든 객체를 메모리에서 삭제한다.

### this
- this 값은 런타임에 결정됨.
- object.method() 같이 메서드 형태로 호출시 this는 object를 참조함.
- 화살표 함수 안에서 this 사용시 외부에서 this 값을 가져옴.

`````
let user = {
  firstName: "보라",
  sayHi() {
    let arrow = () => alert(this.firstName);
    arrow();
  }
};

user.sayHi(); // 보라
`````

### 생성자 함수
생성자 함수는 아래 두 관례를 따른다.
1. 함수 이름의 첫 글자는 대문자로 시작.
2. 반드시 'new' 연산자를 붙여 실행.

`````
function User(name) {
  this.name = name;
  this.isAdmin = false;
}

let user = new User("보라");

alert(user.name); // 보라
alert(user.isAdmin); // false
`````




## References
[Modern Javascript Tutorial](https://ko.javascript.info/)   
