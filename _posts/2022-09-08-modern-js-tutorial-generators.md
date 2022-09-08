---
title: js generators
date: 2022-09-08 23:03:00 +09:00
categories: [JS]
tags: [javascript]
---

## Generators
#### 제너레이터는 여러 개의 값을 필요에 따라 하나씩 반환할 수 있다.

### Generator func
`````
function* generateSequence() {
  yield 1;
  yield 2;
  return 3;
}

let generator = generateSequence();
generator	// [Object Generator]

let one = generator.next();
one	// {value: 1, done: false}

let two = generator.next();
two // {value: 2, done: false}

let three = generator.next();
three // {value: 3, done: true}

let four = generator.next();
four // {value: undefined, done: true}

`````

### Iterable
`````
function* generateSequence() {
  yield 1;
  yield 2;
  yield 3;
}

let generator = generateSequence();

for(let value of generator) {
  alert(value); // 1, 2, 3
}

let sequence = [0, ...generateSequence()];
alert(sequence); // 0, 1, 2, 3
`````

> 3이 yield가 아닌 return이면 1,2 까지만 출력됨.
> done:true면 마지막 value 무시됨







## References
[Modern Javascript Tutorial](https://ko.javascript.info/prototype-inheritance)   
