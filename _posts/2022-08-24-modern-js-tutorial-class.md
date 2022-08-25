---
title: modern js tutorial class
date: 2022-08-24 00:45:00 +09:00
categories: [JS]
tags: [javascript]
---

## 기본문법
`````
class User {

  constructor(name) {
    this.name = name;
  }

  sayHi() {
    alert(this.name);
  }

}

let user = new User("John");
user.sayHi();
`````

- class 또한 함수로 분류됨.
- 하지만 class로 생성한 함수엔 특수 내부 프로퍼티 '[[IsClassConstructor]]: true'
- 클래스에 정의된 메서드는 non-enumerable
- strict mode 적용








## References
[Modern Javascript Tutorial](https://ko.javascript.info/prototype-inheritance)   
