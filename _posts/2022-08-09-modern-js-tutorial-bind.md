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

### func.bind(context)는 특수객체를 반환하며, 이 객체를 호출하면 this가 context로 고정된 func가 반환됨.
`````
let user = {
  firstName: "John"
};

function func() {
  alert(this.firstName);
}

let funcUser = func.bind(user);
funcUser(); // John

let user = {
  firstName: "John",
  sayHi() {
    alert(`Hello, ${this.firstName}!`);
  }
};

let sayHi = user.sayHi.bind(user); // (*)

// 이제 객체 없이도 객체 메서드를 호출할 수 있습니다.
sayHi(); // Hello, John!

setTimeout(sayHi, 1000); // Hello, John!
`````

### 부분 적용(2개의 인수 중 1개 고정)
`````
function mul(a, b) {
  return a * b;
}

let double = mul.bind(null, 2);

alert( double(3) ); // = mul(2, 3) = 6
alert( double(4) ); // = mul(2, 4) = 8
alert( double(5) ); // = mul(2, 5) = 10
`````




## References
[Modern Javascript Tutorial](https://ko.javascript.info/)   
