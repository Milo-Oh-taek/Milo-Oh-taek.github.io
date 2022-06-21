---
title: js slice splice
date: 2022-06-21 23:00:00 +09:00
categories: [JS]
tags: [javascript]
---
## Array.prototype.slice()
### 원본배열은 수정하지 않고 begin - end 전까지의 복사본을 새로운 배열 객체로 반환   
### slice does not alter the original array. It returns a shallow copy of elements from the original array.   
### shallow copy return 함으로 객체배열 가공 사용에 적합하지 않음
`````
const animals = ['ant', 'bison', 'camel', 'duck', 'elephant'];

console.log(animals.slice(2));
// expected output: Array ["camel", "duck", "elephant"]

console.log(animals.slice(2, 4));
// expected output: Array ["camel", "duck"]

console.log(animals.slice(1, 5));
// expected output: Array ["bison", "camel", "duck", "elephant"]

console.log(animals.slice(-2));
// expected output: Array ["duck", "elephant"]

console.log(animals.slice(2, -1));
// expected output: Array ["camel", "duck"]

console.log(animals.slice());
// expected output: Array ["ant", "bison", "camel", "duck", "elephant"]
`````

## Array.prototype.splice()
### 원본 배열의 요소 삭제, 교체 혹은 추가
`````
splice(start, deleteCount, item1, item2, itemN)	// start index부터 deleteCount(몇개) 지우고 item.. 추가
`````
> start: The index at which to start changing the array.
> deleteCount: An integer indicating the number of elements in the array to remove from start.
> item: The elements to add to the array, beginning from start.

`````
const months = ['Jan', 'March', 'April', 'June'];
months.splice(1, 0, 'Feb');
// inserts at index 1
console.log(months);
// expected output: Array ["Jan", "Feb", "March", "April", "June"]

months.splice(4, 1, 'May');
// replaces 1 element at index 4
console.log(months);
// expected output: Array ["Jan", "Feb", "March", "April", "May"]
`````

## Reference
[mozilla - slice](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)   
[mozilla - splice](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)










