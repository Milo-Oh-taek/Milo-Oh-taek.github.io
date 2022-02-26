---
title: ES6 반복문 Loops and iteration
date: 2022-02-26 21:07:00 +09:00
categories: [JS]
tags: [javascript, es6, loops, iteration]
---

## for...of
> The for...of statement creates a loop iterating over iterable objects, including: built-in String, Array, array-like objects (e.g., arguments or NodeList), TypedArray, Map, Set, and user-defined iterables.

for...of 는 반복가능한 객체(Array, Map, Set, String, TypedArray 등)를 반복한다.   


### 사용법
`````
const arr = [1,2,3];
for(item of arr){
  console.log(item);
}
`````

### 원리
##### The iterator protocol
> The iterator protocol defines a standard way to produce a sequence of values (either finite or infinite), and potentially a return value when all values have been generated.
> 순회가능한 객체가 되기 위한 규약

##### Iterable = 순회 가능한 객체 : Symbol.iterator 라는 *symbol을 속성으로 가지고 있으며, 이터레이터 객체를 반환하는 객체.   
>Symbol은 Boolean, null, undefined, Number, String, Object에 이어 새로 추가된 타입으로, 변경 불가능한 원시 타입의 값. 주로 이름의 충돌 위험이 없는 유일한 객체의 프로퍼티 키를 만들기 위해 사용된다.


##### Iterator = 두 개의 속성(value, done)을 반환하는 next() 메소드를 사용하여 객체의 Iterator protocol을 구현함.   

위의 arr 안에는 Symbol(Symbol.iterator) 라는 symbol 속성을 가지고 있다.   

`````
arr[Symbol.iterator]	//ƒ values() { [native code] }
const iter = arr[Symbol.iterator]();	//iter라는 iterator 생성
iter.next();	//{value: 1, done: false}
iter.next();	//{value: 2, done: false}
iter.next();	//{value: 3, done: false}
iter.next();	//{value: undefined, done: true}
`````
Sequence의 마지막 값이 산출되면 done 값은 true가 된다.   

## 전개연산자
`````
const a = [1, 2];
log([...a, ...[3,4]]);	// [1,2,3,4]
`````


## 제너레이터
> 이터레이터이자 이터러블을 생성하는 함수

`````
function *gen() {
  yield 1;
  yield 2;
  yield 3;
}
let iter = gen();
log(iter.next());	//{value: 1, done: false}
log(iter.next());	//{value: 2, done: false}
log(iter.next());	//{value: 3, done: false}
log(iter.next());	//{value: undefined, done: true}
`````







## Reference
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of
- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Iteration_protocols
- https://www.inflearn.com/course/functional-es6






