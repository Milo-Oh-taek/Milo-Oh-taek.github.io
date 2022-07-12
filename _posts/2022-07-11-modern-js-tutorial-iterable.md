---
title: modern js tutorial iterable
date: 2022-07-12 00:30:00 +09:00
categories: [JS]
tags: [javascript]
---

## 자료구조

### iterable 객체
배열 및 문자열 같이 반복 할 수 있는 객체.   

#### Symbol.iterator
1. for..of가 시작되자마자 for..of는 Symbol.iterator를 호출한다. Symbol.iterator은 iterator를 반환한다.
2. 이후 for..of는 반환된 객체만을 대상으로 동작한다.
3. for..of 다음 값이 필요하면 iterator의 next() 메서드를 호출한다.
4. next()의 반환 값은 {done: Boolean, value: any} 형태.

`````
let range = {
  from: 1,
  to: 5,

  [Symbol.iterator]() {
    this.current = this.from;
    return this;
  },

  next() {
    if (this.current <= this.to) {
      return { done: false, value: this.current++ };
    } else {
      return { done: true };
    }
  }
};

for (let num of range) {
  alert(num); // 1, then 2, 3, 4, 5
}
`````

#### 이터러블과 유사배열
- 이터러블(iterable): Symbol.iterator가 구현된 객체
- 유사배열(array-like): 인덱스와 length 프로퍼티가 있어서 배열처럼 보이는 객체

`````
let arrayLike = { // 인덱스와 length프로퍼티가 있음 => 유사 배열
  0: "Hello",
  1: "World",
  length: 2
};

// Symbol.iterator가 없으므로 에러 발생
for (let item of arrayLike) {}
`````

#### Array.from
이터러블이나 유사배열을 받아 Array로 만들어줌.   
`````
let arrayLike = {
  0: "Hello",
  1: "World",
  length: 2
};

let arr = Array.from(arrayLike); // 이터러블 or 유사배열 조사후 새로운 배열 생성 및 복사
alert(arr.pop()); // World (메서드가 제대로 동작합니다.)
`````

mapping 함수 적용 : 배열에 요소를 추가하기 전에 mapFn 적용 가능   
`````
Array.from(obj[, mapFn, thisArg])

// 각 숫자를 제곱
let arr = Array.from(range, num => num * num);

alert(arr); // 1,4,9,16,25
`````


## References
[Modern Javascript Tutorial](https://ko.javascript.info/)   
