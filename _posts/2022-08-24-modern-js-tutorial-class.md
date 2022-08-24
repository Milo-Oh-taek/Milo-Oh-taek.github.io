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




## References
[Modern Javascript Tutorial](https://ko.javascript.info/prototype-inheritance)   
