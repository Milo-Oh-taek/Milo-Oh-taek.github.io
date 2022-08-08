---
title: modern js tutorial call and apply
date: 2022-08-08 19:00:00 +09:00
categories: [JS]
tags: [javascript]
---

## func.call

### func.call(context, arg1, arg2, ...)

`````
func(1, 2, 3);
func.call(obj, 1, 2, 3);

동일하지만, func.call 에서는 this가 obj로 고정됨.

1.
function sayHi() {
  alert(this.name);
}

let user = { name: "John" };
let admin = { name: "Admin" };

sayHi.call( user ); // this = John
sayHi.call( admin ); // this = Admin

2.
function say(phrase) {
  alert(this.name + ': ' + phrase);
}

let user = { name: "John" };

say.call( user, "Hello" ); // John: Hello
`````

## func.apply

### func.apply(context, args)

call은 복수 인수를 따로따로 받음.   
apply는 인수를 유사 배열 객체로 받음.   

`````
func.call(context, ...args); // 전개 문법을 사용해 인수가 담긴 배열을 전달하는 것과
func.apply(context, args);   // call을 사용하는 것은 동일합니다.

`````


## References
[Modern Javascript Tutorial](https://ko.javascript.info/)   
