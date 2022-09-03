---
title: js promise api
date: 2022-09-03 21:03:00 +09:00
categories: [JS]
tags: [javascript]
---

## Promise.all
#### 여러 개의 promise를 동시에 실행하고 모든 promise를 기다림
`````
Promise.all([
  new Promise(resolve => setTimeout(() => resolve(1), 3000)), // 1
  new Promise(resolve => setTimeout(() => resolve(2), 2000)), // 2
  new Promise(resolve => setTimeout(() => resolve(3), 1000))  // 3
]).then(alert);

// 3초뒤 1,2,3 
`````

#### Promise 하나라도 거부시 전체 Error 반환됨
`````
Promise.all([
  new Promise((resolve, reject) => setTimeout(() => resolve(1), 1000)),
  new Promise((resolve, reject) => setTimeout(() => reject(new Error("에러 발생!")), 2000)),
  new Promise((resolve, reject) => setTimeout(() => resolve(3), 3000))
]).catch(alert);

// 2초뒤 Error: 에러 발생!
`````

## Promise.allSettled

#### 모든 promise 기다리나, promise중 실패값이 있어도 다른 promise는 정상적으로 수행됨
- 응답 성공시 : {status:"fulfilled", value:result}
- 응답 실패시 : {status:"rejected", reason:error}

`````
let urls = [
  'https://api.github.com/users/iliakan',
  'https://api.github.com/users/Violet-Bora-Lee',
  'https://no-such-url'
];

Promise.allSettled(urls.map(url => fetch(url)))
  .then(results => { // (*)
    results.forEach((result, num) => {
      if (result.status == "fulfilled") {
        alert(`${urls[num]}: ${result.value.status}`);
      }
      if (result.status == "rejected") {
        alert(`${urls[num]}: ${result.reason}`);
      }
    });
  });

//
[
  {status: 'fulfilled', value: ...응답...},
  {status: 'fulfilled', value: ...응답...},
  {status: 'rejected', reason: ...에러 객체...}
]
`````

#### 폴리필
`````
if(!Promise.allSettled) {
  Promise.allSettled = function(promises) {
    return Promise.all(promises.map(p => Promise.resolve(p).then(value => ({
      status: 'fulfilled',
      value
    }), reason => ({
      status: 'rejected',
      reason
    }))));
  };
}
`````

## Promise.race
#### Promise.all과 비슷하나 먼저 처리되는 promise만 반환
`````
Promise.race([
  new Promise((resolve, reject) => setTimeout(() => resolve(1), 1000)),
  new Promise((resolve, reject) => setTimeout(() => reject(new Error("에러 발생!")), 2000)),
  new Promise((resolve, reject) => setTimeout(() => resolve(3), 3000))
]).then(alert); // 1
`````







## References
[Modern Javascript Tutorial](https://ko.javascript.info/prototype-inheritance)   
