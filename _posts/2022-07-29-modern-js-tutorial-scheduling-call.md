---
title: modern js tutorial scheduling call
date: 2022-07-29 23:45:00 +09:00
categories: [JS]
tags: [javascript]
---

## setTimeout
**일정 시간이 지난 후에 함수를 실행하는 방법**

### 사용법
`````
function sayHi(who, phrase) {
  alert( who + ' 님, ' + phrase );
}

setTimeout(sayHi, 1000, "홍길동", "안녕하세요."); // 홍길동 님, 안녕하세요.

// 잘못된 코드 - 함수에 ()를 붙이면 return값이 들어온다.
setTimeout(sayHi(), 1000);
`````

`````
스케줄링 취소
let timerId = setTimeout(...);
clearTimeout(timerId);
`````

### 중첩(setInterval보다 좀 더 유연하게 사용 가능)
`````
let timerId = setTimeout(function tick() {
  alert('째깍');
  timerId = setTimeout(tick, 2000); // (*)
}, 2000);
`````

## setInterval
**일정 시간 간격을 두고 함수를 실행하는 방법**

`````
// 2초 간격으로 메시지를 보여줌
let timerId = setInterval(() => alert('째깍'), 2000);

// 5초 후에 정지
setTimeout(() => { clearInterval(timerId); alert('정지'); }, 5000);
`````

**setInterval 사용시 함수 실행 소모 시간도 지연 간격에 포함되기 때문에 실제 설정한 시간보다 짧아짐**
**중첩 setTimeout 사용시 설정한 지연 시간이 보장된다.**

## References
[Modern Javascript Tutorial](https://ko.javascript.info/)   
