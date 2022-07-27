---
title: modern js tutorial closure
date: 2022-07-26 23:45:00 +09:00
categories: [JS]
tags: [javascript]
---

## Lexical Environment

### 변수

1. 환경 레코드(Environment Record): 모든 지역 변수를 프로퍼티로 저장하고 있는 객체. this값과 같은 기타 정보 포함.
2. 외부 렉시컬(Outer Lexical Environment): 외부 코드와 연관됨.

**'변수'는 환경 레코드의 프로퍼티.**


### 함수 선언문

**함수 선언문으로 선언한 함수는 바로 초기화 된다.**

### 내부와 외부 Lexical Environment

`````
let phrase = 'Hello';

function say(name){
  alert( `${phrase}, ${name});
}

say("John");
`````
- 함수 호출 중 내부 렉시컬 환경과 외부 렉시컬 환경을 갖게 됨.
- 내부 렉시컬 환경 : name(John)
- 외부 렉시컬 환경 = 전역 렉시컬 환경 : phrase, say   

**코드에서 변수에 접근할 때, 먼저 내부 렉시컬 환경 검색. **
**내부에 원하는 변수가 없으면 내부 렉시컬 환경이 참조하는 외부 렉시컬 환경으로 확장 **
**이 과정은 검색 범위가 전역 렉시컬 환경으로 확장될 때까지 반복 **

### 함수를 반환하는 함수

`````
function makeCounter(){
  let count = 0;
  
  return function(){
    return count++;
  }
}

let counter = makeCounter();
`````

- makeCounter()를 호출할 때마다 새로운 렉시컬 환경 객체가 만들어지고, 여기에 makeCounter를 실행하는데 필요한 변수들이 저장된다.
- **모든 함수는 함수가 생성된 곳의 렉시컬 환경을 기억한다.([[Environment]]라 불리는 숨김 프로퍼티)**
- **따라서 counter.[[Environment]]에는 {count:0}이 있는 렉시컬 환경에 대한 참조 저장**
- **count++가 실행되면서 count 값이 증가하는데, 변숫값 갱신은 변수가 저장된 렉시컬 환경에서 이뤄짐.**


### 가비지 컬렉션

함수 호출이 끝나면 함수에 대응하는 렉시컬 환경이 메모리에서 제거됨.(객체는 도달 가능한 상태일 때만 메모리에 유지)   

**호출이 끝난 후에도 여전히 도달 가능한 중첩 함수가 있을 수 있고, [[Environment]]에 외부 함수 렉시컬 환경에 대한 정보가 저장됨**

`````
function f() {
  let value = 123;

  return function() {
    alert(value);
  }
}

let g = f(); // g가 살아있는 동안엔 연관 렉시컬 환경도 메모리에 살아있습니다.

g = null; // 도달할 수 없는 상태가 되었으므로 메모리에서 삭제됩니다.
`````

하지만 실제로는 자바스크립트 엔진이 이를 지속해서 최적화 작업 진행.   
**외부 변수가 사용되지 않는다고 판단하면 이를 메모리에서 제거.(V8에서 제거된 변수는 사용할 수 없음)**

`````
let value = "이름이 같은 다른 변수";

function f() {
  let value = "가장 가까운 변수";

  function g() {
    debugger; // 콘솔에 alert(value);를 입력하면 '이름이 같은 다른 변수'가 출력됩니다.
  }

  return g;
}

let g = f();
g();
`````



## References
[Modern Javascript Tutorial](https://ko.javascript.info/)   
