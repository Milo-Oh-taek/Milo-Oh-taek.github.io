---
title: modern js tutorial bind
date: 2022-08-09 19:00:00 +09:00
categories: [JS]
tags: [javascript]
---

## bind

`````
let user = {
  firstName: "John",
  sayHi() {
    alert(`Hello, ${this.firstName}!`);
  }
};

setTimeout(user.sayHi, 1000); // Hello, undefined!

user.sayHi만 전달 되기 때문에 user의 firstName 읽지 못함.
// setTimeout은 인수로 전달받은 함수 호출 할 때 this에 window를 할당함.   
// this.firstName = undefined

1. 래퍼 - 외부 렉시컬 환경에서 가져오기
setTimeout(function() {
  user.sayHi(); // Hello, John!
}, 1000);
`````




## References
[Modern Javascript Tutorial](https://ko.javascript.info/)   
