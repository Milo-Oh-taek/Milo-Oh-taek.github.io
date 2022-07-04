---
title: react scroll throttle and debounce
date: 2022-06-30 21:30:00 +09:00
categories: [REACT]
tags: [react]
---

## Throttle & Debounce 사용이유
Scroll, Submit 등의 이벤트가 과도하게 동작하거나 중복처리 됨을 방지하기 위해서 사용.   
예를들어 [here](https://codepen.io/chriscoyier/pen/vOZNQV) 에서 확인해보면 이벤트 발생 횟수를 비교해 볼 수 있다.   
밑의 React 코드도 마찬가지이다.   

## 정의

- Throttle : 마지막 함수가 호출된 후 일정 시간이 지나기 전에 다시 호출되지 않도록 하는 것
	- ex) Scroll event
	- [Infinite scrolling throttled](https://codepen.io/dcorb/pen/eJLMxa)
- Debounce : 연이어 호출되는 함수들 중 마지막 함수(또는 제일 처음)만 호출하도록 하는 것
	- ex) Search시 입력을 멈췄을 때
	- only works once!

## 사용
아래 React 코드와 같이 직접 구현해도 되지만   
lodash, underscore의 _.throttle or _.debounce도 많이 이용하는 것으로 보인다.   

`````
const handleScroll = (e) => {
  console.log(window.scrollY);
};

//normal
useEffect(() => {
  window.addEventListener("scroll", handleScroll);

  return () => {
    window.removeEventListener("scroll", handleScroll);
  };
}, []);

// debounce
useEffect(() => {
  var timer;
  window.addEventListener("scroll", () => {
    if (timer) {
      clearTimeout(timer);
    }

    timer = setTimeout(() => {
      timer = null;
      handleScroll();
    }, 200);
  });
  return () => {
    window.removeEventListener("scroll", handleScroll);
  };
}, []);

// throttle
useEffect(() => {
  var timer;
  window.addEventListener("scroll", () => {
    if (!timer) {
      timer = setTimeout(() => {
        timer = null;
        handleScroll();
      }, 200);
    }
  });
  return () => {
    window.removeEventListener("scroll", handleScroll);
  };
});
`````

## References
[https://codepen.io/dcorb/pen/eJLMxa](https://codepen.io/dcorb/pen/eJLMxa)   
[https://codepen.io/chriscoyier/pen/vOZNQV](https://codepen.io/chriscoyier/pen/vOZNQV)   
[https://www.zerocho.com/category/JavaScript/post/59a8e9cb15ac0000182794fa](https://www.zerocho.com/category/JavaScript/post/59a8e9cb15ac0000182794fa)