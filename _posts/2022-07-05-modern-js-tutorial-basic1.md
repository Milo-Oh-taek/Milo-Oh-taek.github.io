---
title: modern js tutorial basic 1
date: 2022-07-05 14:30:00 +09:00
categories: [JS]
tags: [javascript]
---

## Javascript
### 정의
- '웹페이지에 생동감을 불어넣기 위해' 만들어진 프로그래밍 언어.
- 브라우저 및 서버에서 실행 가능.
- 브라우저 엔진
	- V8 - Chrome, Opera
	- SpiderMonkey - Firefox
	- ChakgraCore - Microsoft Edge
	- SquirrelFish - Safari

### 엔진 동작 방식
- 엔진이 스크립트를 읽는다(파싱)
- 기계어로 전환(컴파일)
- 기계어로 전환된 코드를 실행

### JS의 강점
- HTML/CSS와 완전 통합 가능
- 간단한 일은 간단하게 처리 가능
- 모든 주요 브라우저에서 지원, 기본 언어로 사용

### JS 기본 자료형
- 숫자형 - 정수, 부동 소주점 숫다 등
- bigint - 길이 제약 없는 정수
- 문자형 - 문자열
- boolean - true or false
- null
- undefined - 할당되지 않은 값
- 객체형 - 복잡한 데이터 구조 표현
- 심볼형 - 객체의 고유 식별자를 만들 때 사용

### '&&' and '||'
- '&&'는 첫 번째 falsy 값을 찾는다.
- '&&'는 모든 피연산자가 true로 평가되는 경우 => 마지막 피연상자가 반환된다.
- "||"는 첫 번째 truthy 값을 찾고 boolean이 아닌 해당 피연산자의 **변환 전** 원래 값 반환한다.
- "||"는 truthy 값이 없을 경우 마지막 피연산자를 반환한다. 

### nullish 병합 연산자 '??'
`````
x = (a !== null && a !== undefined) ?  a: b;
`````

### '??'와 '||'의 차이
`````
let height = 0;

alert(height || 100); // 100
alert(height ?? 100); // 0
`````
** 안정성 관련 이슈 때문에 ??는 &&나 ||와 함께 사용하지 못합니다.(괄호 사용 필요)**

## References
[Modern Javascript Tutorial](https://ko.javascript.info/)   
