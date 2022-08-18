---
title: modern js tutorial prototype inheritance
date: 2022-08-18 19:00:00 +09:00
categories: [JS]
tags: [javascript]
---

## 상속
### [[Prototype]]
#### 객체는 [[prototype]]라는 숨김 프로퍼티를 갖는데, null이거나 다른 객체에 대한 참조이다. 다른 객체를 참조하는 경우 참조 대상을 '프로토타입'이라 한다.

#### 프로토타입 상속: object에서 프로퍼티를 읽으려고 하는데 해당 프로퍼티가 없으면 자동으로 프로토타입에서 프로퍼티를 찾음.




`````
let animal = {
  eats: true
};
let rabbit = {
  jumps: true
};

rabbit.__proto__ = animal;
rabbit.eats		// true

-> rabbit의 프로토타입은 animal이다. rabbit은 animal을 상속받는다.


- __proto__는 [[Prototype]]의 getter이자 setter이다.

- __proto__의 값은 객체나 null만 가능하다.

- 객체엔 오직 하나의 [[Prototype]]만 있을 수 있다.
`````

`````
let animal = {
  eats: true,
  walk() {
  }
};

let rabbit = {
  __proto__: animal
};

rabbit.walk = function() {
  alert("토끼가 깡충깡충 뜁니다.");
};

rabbit.walk(); // 실행시 프로토타입이 아닌 객체 rabbit에 직접 추가한 메서드가 실행됨

`````

#### this는 언제나 .앞에 있는 객체이다.
`````
let animal = {
  walk() {
    if (!this.isSleeping) {
      alert(`동물이 걸어갑니다.`);
    }
  },
  sleep() {
    this.isSleeping = true;
  }
};

let rabbit = {
  name: "하얀 토끼",
  __proto__: animal
};

// rabbit에 새로운 프로퍼티 isSleeping을 추가하고 그 값을 true로 변경합니다.
rabbit.sleep();

alert(rabbit.isSleeping); // true
alert(animal.isSleeping); // undefined (프로토타입에는 isSleeping이라는 프로퍼티가 없습니다.)
`````

#### for...in은 상속 프로퍼티도 순회대상에 포함시킨다.
`````
let animal = {
  eats: true
};

let rabbit = {
  jumps: true,
  __proto__: animal
};

// Object.keys는 객체 자신의 키만 반환.
alert(Object.keys(rabbit)); // jumps

// for..in은 객체 자신의 키와 상속 프로퍼티의 키 모두를 순회.
for(let prop in rabbit) alert(prop); // jumps, eats

// hasOwnProperty 사용하여 자신의 키 or 상속을 구별할 수 있다.
for(let prop in rabbit) {
  let isOwn = rabbit.hasOwnProperty(prop);

  if (isOwn) {
    alert(`객체 자신의 프로퍼티: ${prop}`); // 객체 자신의 프로퍼티: jumps
  } else {
    alert(`상속 프로퍼티: ${prop}`); // 상속 프로퍼티: eats
  }
}

`````
> rabbit은 animal을 상속
> animal은 Object.prototype을 상속(animal이 객체 리터럴 방식이기에)
> Object.prototype은 null을 상속


#### 프로토 체인의 프로퍼티를 공유하게 되는 경우
`````
let hamster = {
  stomach: [],

  eat(food) {
    this.stomach.push(food);
  }
};

let speedy = {
  __proto__: hamster,
  stomach: []	// 여기에 stomach가 없으면 speedy에는 stomach가 없기에 
  				// hamster의 stomach를 공유하게 된다.
};

let lazy = {
  __proto__: hamster,
  stomach: []
};

// 햄스터 speedy가 음식을 먹습니다.
speedy.eat("apple");
alert( speedy.stomach ); // apple
`````


## References
[Modern Javascript Tutorial](https://ko.javascript.info/prototype-inheritance)   
