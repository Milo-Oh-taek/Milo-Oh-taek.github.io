---
title: modern js tutorial property getter setter
date: 2022-08-17 19:00:00 +09:00
categories: [JS]
tags: [javascript]
---

## property getter & setter

`````
let user = {
  name: "John",
  surname: "Smith",

  get fullName() {
    return `${this.name} ${this.surname}`;
  },

  set fullName(value) {		// set의 인수는 하나
    [this.name, this.surname] = value.split(" ");
  }
};

user.fullName	//'John Smith'
user.fullName = 'Milo Oh';
user.fullName	//'Milo Oh';
`````

### 활용
`````
let user = {
  get name() {
    return this._name;
  },

  set name(value) {
    if (value.length < 4) {
      alert("입력하신 값이 너무 짧습니다. 네 글자 이상으로 구성된 이름을 입력하세요.");
      return;
    }
    this._name = value;
  }
};

user.name = "Pete";
alert(user.name); // Pete
`````
**user의 이름은 _name에 저장됨.**   
**"_"로 시작하는 프로퍼티는 객체 내부에서만 활용하고 외부에서는 건드리지 않는 것이 관습.**

`````
function User(name, birthday) {
  this.name = name;
  this.birthday = birthday;

  // age는 현재 날짜와 생일을 기준으로 계산됩니다.
  Object.defineProperty(this, "age", {
    get() {
      let todayYear = new Date().getFullYear();
      return todayYear - this.birthday.getFullYear();
    }
  });
}

let john = new User("John", new Date(1992, 6, 1));

alert( john.birthday ); // birthday를 사용할 수 있습니다.
alert( john.age );      // age 역시 사용할 수 있습니다.
`````

**다음과 같이 설정하면 john.age = 3000 과 같이 임의적으로 설정이 불가능 하다.**
**따라서 제약조건을 설정하거나 제한을 둘 때 사용가능.**


## References
[Modern Javascript Tutorial](https://ko.javascript.info/)   
