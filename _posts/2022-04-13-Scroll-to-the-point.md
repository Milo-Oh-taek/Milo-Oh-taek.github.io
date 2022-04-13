---
title: Scroll to the specific point
date: 2022-04-13 09:50:00 +09:00
categories: [REACT]
tags: [react]
---
## Scroll 특정 포인트로 이동 2 method   

최상단 이동은 (https://milo-oh-taek.github.io/posts/React-scroll-to-the-top/) 참고   

### 1. html basic function   
`````
<Link to="/business#product">
`````
> '/business' -> page name   
> '#product' -> Id of point you want to go   

If Link(react router dom) doesn't work, try with a tag.

### 2. react-router-hash-link   
https://github.com/rafgraph/react-router-hash-link
`````
$npm i react-router-hash-link
`````

`````
import { HashLink } from 'react-router-hash-link';

...

<HashLink to="/some/path#with-hash-fragment">Link to Hash Fragment</HashLink>
`````
github을 보니 모바일 이동안되는 이슈? 확인해 볼 것










