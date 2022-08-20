---
title: modern js tutorial prototype native
date: 2022-08-20 22:12:00 +09:00
categories: [JS]
tags: [javascript]
---

## Object.prototype
#### 객체를 생성하면 [[Prototype]]은 Object.prototype을 참조한다.
`````
let obj = {};

alert(obj.__proto__ === Object.prototype); // true

alert(obj.toString === obj.__proto__.toString); //true
alert(obj.toString === Object.prototype.toString); //true
`````

## 내장 객체 프로토타입
#### 배열 [1,2,3] 생성시 Array.prototype이 프로토타입이 되며, 배열 메서드 사용가능.
#### Array, Function, Number는 Object.prototype을 상속
#### 체인 맨 위에는 null

`````
let arr = [1, 2, 3];

alert( arr.__proto__ === Array.prototype ); // true

alert( arr.__proto__.__proto__ === Object.prototype ); // true

alert( arr.__proto__.__proto__.__proto__ ); // null
`````

## 메서드 빌리기
`````
let obj = {
  0: "Hello",
  1: "world!",
  length: 2,
};

obj.join = Array.prototype.join;

alert( obj.join(',') ); // Hello,world!
`````


## References
[Modern Javascript Tutorial](https://ko.javascript.info/prototype-inheritance)   
