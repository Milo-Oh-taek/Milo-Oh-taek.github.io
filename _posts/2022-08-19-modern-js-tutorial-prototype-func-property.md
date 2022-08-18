---
title: modern js tutorial prototype func property
date: 2022-08-19 00:12:00 +09:00
categories: [JS]
tags: [javascript]
---

## 생성자 '함수’를 사용해 객체를 만든 경우
`````
let animal = {
  eats: true
};

function Rabbit(name) {
  this.name = name;
}

Rabbit.prototype = animal;

let rabbit = new Rabbit("흰 토끼"); //  rabbit.__proto__ == animal

alert( rabbit.eats ); // true
`````

## func default property
`````
function Rabbit(){}

Rabbit.prototype	// {constructor: Rabbit()}

let rabbit = new Rabbit();

rabbit.constructor == Rabbit;	//true -> [[Prototype]]을 거쳐 접근
`````

## 새로운 객체 생성
`````
function Rabbit(name) {
  this.name = name;
  alert(name);
}

let rabbit = new Rabbit("흰 토끼");

let rabbit2 = new rabbit.constructor("검정 토끼");
`````

## prototype 변경
`````
function Rabbit() {}

Rabbit.prototype.jumps = true	// Rabbit.prototype.constructor은 유지됨

Rabbit.prototype = {
  jumps: true
};


`````



## References
[Modern Javascript Tutorial](https://ko.javascript.info/prototype-inheritance)   
