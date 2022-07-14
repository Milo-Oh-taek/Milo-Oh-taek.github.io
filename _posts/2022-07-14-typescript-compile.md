---
title: typescript compile
date: 2022-07-14 14:30:00 +09:00
categories: [TS]
tags: [typescript]
---

## Typescript compile

### 기본(1 file)
`````
$tsc app.ts
`````

### 자동 컴파일(1 file)
`````
$tsc app.ts --watch
`````

### 다수 파일 (전체 프로젝트)
`````
$tsc --init // 프로젝트 초기에 한번만 실행

$tsc // 전체 컴파일

$tsc --watch // 전체 컴파일 자동
`````

### 특정 파일들만 컴파일
tsconfig.json   
`````
{
  "compilerOptions": {
	...
  },
  "include": ["app.ts", "basic.ts"]
}

`````

### tsconfig.json
- target: 변환하고자 하는 js version
- lib: 사용할 라이브러리
	- es6 default(주석처리시): dom, es6, dom.iterable, scripthost
- sourceMap: 브라우저 Sources에서 ts 파일 확인 가능(디버깅 용이)
- outDir: 컴파일된 js파일 저장 위치
- rootDir: 컴파일 시작 위치(default: 가장 상위 디렉토리)





## References
[https://www.typescriptlang.org/docs/handbook/tsconfig-json.html](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html)   
[https://www.udemy.com/course/best-typescript-21/](https://www.udemy.com/course/best-typescript-21/)   
