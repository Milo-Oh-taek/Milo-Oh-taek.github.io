---
title: modern js tutorial spread
date: 2022-07-23 23:30:00 +09:00
categories: [JS]
tags: [javascript]
---

## ...

`````
function sumAll(...args) { // args는 배열의 이름입니다.
  let sum = 0;

  for (let arg of args) sum += arg;

  return sum;
}

alert( sumAll(1) ); // 1
alert( sumAll(1, 2) ); // 3
alert( sumAll(1, 2, 3) ); // 6
`````

**변수가 여러개 일 때, 나머지 매개변수는 항상 마지막에 있어야 한다.**

## arguments

arguments는 유사배열객체이면서 이터러블 객체.   
하지만 배열은 아니기에 배열 메서드 사용 불가.   

**화살표 함수에서는 arguments 객체 지원 불가**


`````
function showName() {
  alert( arguments.length );
  alert( arguments[0] );
  alert( arguments[1] );

  // arguments는 이터러블 객체이기 때문에
  // for(let arg of arguments) alert(arg); 를 사용해 인수를 펼칠 수 있습니다.
}

// 2, Bora, Lee가 출력됨
showName("Bora", "Lee");

// 1, Bora, undefined가 출력됨(두 번째 인수는 없음)
showName("Bora");
`````

## spread

**배열 및 이터러블 객체라면 스프레드 문법 사용 가능**

`````
let arr = [3, 5, 1];

alert( Math.max(arr) ); // NaN // 숫자 목록을 인수로 받는다.
alert( Math.max(...arr) );  // 5

let arr = [3, 5, 1];
let arr2 = [8, 9, 15];

let merged = [0, ...arr, 2, ...arr2];  // 병합

let str = "Hello";  // 문자열
alert( [...str] ); // H,e,l,l,o
alert( Array.from(str) ); // H,e,l,l,o
`````
> Array.from - 유사배열객체, 이터러블 객체 둘 다 사용 가능
> spread - 이터러블 객체에만 사용 가능

## copy 
`````
let arr = [1, 2, 3];
let arrCopy = [...arr];

alert(JSON.stringify(arr) === JSON.stringify(arrCopy)); // true
alert(arr === arrCopy); // false

let obj = { a: 1, b: 2, c: 3 };
let objCopy = { ...obj };

alert(JSON.stringify(obj) === JSON.stringify(objCopy)); // true
alert(obj === objCopy); // false
`````

## References
[Modern Javascript Tutorial](https://ko.javascript.info/)   
