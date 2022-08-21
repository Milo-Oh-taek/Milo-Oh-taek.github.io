---
title: modern js tutorial prototype methods
date: 2022-08-22 00:45:00 +09:00
categories: [JS]
tags: [javascript]
---

## prototype methods

#### Object.create(proto, [descriptors]) - [[Prototype]]이 proto를 참조하는 빈객체를 생성.
#### Object.getPrototypeOf(obj) - obj의 [[Prototype]]을 반환.
#### Object.setPrototypeOf(obj, proto) - obj의 [[Prototype]]이 proto가 되도록 설정.

`````
let animal = {
  eats: true
};

// 프로토타입이 animal인 새로운 객체를 생성.
let rabbit = Object.create(animal, {
  jumps: {
    value: true
  }
});

rabbit.jumps	// true
rabbit.eats // true

Object.getPrototypeOf(rabbit) === animal); // true

Object.setPrototypeOf(rabbit, {}); // rabbit의 프로토타입을 {}으로 바꿈.

`````

#### 모든 프로퍼티 복사
`````
let clone = Object.create(Object.getPrototypeOf(obj), Object.getOwnPropertyDescriptors(obj));
`````

#### Simple Object
`````
let test1 = {};
test1	//  [[Prototype]]: Object

let test2 = Object.create(null);
test2	// No properties - 내장 메서드 없음


`````


## References
[Modern Javascript Tutorial](https://ko.javascript.info/prototype-inheritance)   
