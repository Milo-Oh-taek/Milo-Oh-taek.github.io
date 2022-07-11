---
title: modern js tutorial data structure
date: 2022-07-11 15:30:00 +09:00
categories: [JS]
tags: [javascript]
---

## 자료구조

### 원시값의 메서드

JS에서 원시값을 마치 객체처럼 다룰 수 있으며 메서드를 호출할 수 있다.   
#### 원시값(primitive)
- 문자(string), 숫자(number), bigint, 불린(boolean), 심볼(symbol), null, undefined

#### 객체(object)
- 프로퍼티에 다양한 종류의 값을 저장할 수 있다.

#### 원시 래퍼 객체(object wrapper)
- 원시값은 원시값 그대로 남겨둬 단일 값 형태를 유지한다.
- 문자열, 숫자, 불린, 심볼의 메서드와 프로퍼티에 접근할 수 있도록 언어 차원에서 허용한다.
- 이를 가능하게 하기 위해, 원시값이 메서드나 프로퍼티에 접근하려 하면 추가 기능을 제공해주는 특수한 객체, "원시 래퍼 객체(object wrapper)"를 만들어 준다. 이 객체는 곧 삭제된다.   
- **String, Number, Boolean, Symbol**

`````
let str = "Hello";

alert( str.toUpperCase() ); // HELLO
`````
1. toUpperCase에 접근하는 순간 특별한 객체가 만들어짐.
2. 메서드가 실행되고 새로운 문자열이 반환됨.
3. 특별한 객체는 파괴되고, 원시값 str만 남음.

### 숫자형

#### 다수의 0을 입력하기
- 0의 개수를 'e' 뒤에 추가한다. 123e6은 0이 6개인 숫자, 123000000을 나타냄.
- 'e' 다음에 음수가 오면 음수의 절댓값 만큼 10을 거듭제곱한 숫자로 주어진 숫자를 나눈다. 123e-6은 0.000123   

#### Number Parse (parseInt, parseFloat)
불가능할 때까지 문자열에서 숫자를 읽는다.   
읽는 도중 오류가 발생하면 이미 수집된 숫자를 반환.   
**읽을 수 있는 숫자가 없으면 NaN **   

`````
alert( parseInt('100px') ); // 100
alert( parseFloat('12.5em') ); // 12.5

alert( parseInt('12.3') ); // 12, 정수 부분만 반환됩니다.
alert( parseFloat('12.3.4') ); // 12.3, 두 번째 점에서 숫자 읽기를 멈춥니다.
`````

### 배열

#### 배열 shift 메서드 호출시 수행되는 작업
1. 인덱스 0인 요소를 제거.
2. 모든 요소를 왼쪽으로 이동.
3. length 프로퍼티 값 갱신.

**따라서 shift, unshift는 push, pop에 비해 속도가 느리다**

#### 배열에는 되도록이면 for..in을 쓰지말자.
1. for..in은 모든 프로퍼티를 대상으로 순회한다. 키가 숫자가 아닌 프로퍼티도 순회 대상. 예를들어 유사배열의 경우 불필요한 프로퍼티로 인해 문제가 발생할 소지가 높다.
2. for..in은 객체와 함께 사용할 때 최적화 되어 있다.

#### 배열 'length' 프로퍼티는 배열 내 요소 개수가 아닌 가장 큰 인덱스+1 이다.

#### 배열의 toString 
배열엔 toString 메서드가 구현되어있다.   
`````
let arr = [1, 2, 3];

alert( arr ); // 1,2,3
alert( String(arr) === '1,2,3' ); // true
`````

#### 배열 여부 확인 Array.isArray
`````
alert(Array.isArray({})); // false

alert(Array.isArray([])); // true
`````


## References
[Modern Javascript Tutorial](https://ko.javascript.info/)   
