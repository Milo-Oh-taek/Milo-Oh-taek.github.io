---
title: 리액트 사용 이유 Why is React better than jQuery
date: 2022-02-18 18:20:00 +09:00
categories: [REACT]
tags: [react, jquery]
---

# React vs jQuery  
![trend](https://user-images.githubusercontent.com/56327550/154674644-81ba1a55-3b0b-4f62-9bd5-f0259f0eaae0.JPG)   

## Speed   
>One of the biggest things that React has going for it is the use of the Virtual DOM (Document Object Model) instead of the traditional DOM. While jQuery works with the DOM directly, React uses the virtual DOM which is what makes React so much faster.

업데이트가 필요할 때 **jQuery는 직접적으로 DOM을 수정**하는 반면, **React는 Virtual DOM을 이용**한다.   
<mark>직접적으로 수정하는 경우 DOM TREE의 최상단으로부터 update가 이루어지는 반면,   
Virtual DOM은 변경 전 DOM을 Screenshot처럼 기억해 두었다가 변경된 부분만 변경이 가능하다.</mark>   
따라서 업데이트가 빈번할수록, DOM TREE 사이즈가 클수록 성능차이는 커지게 된다.

아래 영상을 보면 React의 Virtual DOM의 컨셉을 쉽게 이해할 수 있다.
<iframe width="560" height="315" src="https://www.youtube.com/embed/BYbgopx44vo" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>   

## Visibility   
jQuery는 프로젝트가 복잡하고 커질수록 유지보수가 힘들어지는 면이 있다.


## Reference
- https://www.educative.io/edpresso/jquery-vs-react   
- https://javascript.plainenglish.io/why-you-should-use-react-instead-of-jquery-d68b5b129bbb






