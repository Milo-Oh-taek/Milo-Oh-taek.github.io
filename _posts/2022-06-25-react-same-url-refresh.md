---
title: react url changed, not refresh
date: 2022-06-25 23:30:00 +09:00
categories: [REACT, Error]
tags: [react]
---

## react router에서 url 변경시 새로고침이 안되는 경우가 있다.

### 현상
- /product/1  => /product/2   
- url은 변경되지만 렌더링은 일어나지 않음으로 화면은 변경되지 않는다.   

### 해결법
- 위와 같은 같은 url 끼리의 이동이라면
- useParams를 이용하여 변경되었는지 확인한 후 데이터를 재 fetch 해오면 된다.
[useParams in React-Router-Dom v6](http://milo-oh-taek.github.io/posts/React-router-dom-v6/)



