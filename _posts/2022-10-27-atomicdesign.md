---
title: atomic design 아토믹 디자인
date: 2022-10-27 21:00:00 +09:00
categories: [ETC]
tags: [design]
---

## Atomic design
#### 아토믹 디자인이란 5단계로 구성되어 더욱 계획적/계층적으로 인터페이스를 만들어가는 방법론.
> Atomic design is a methodology composed of five distinct stages working together to create interface design systems in a more deliberate and hierarchical manner.

## Stages
1. Atoms
2. Molecules
3. Organisms
4. Templates
5. Pages

![atomic-design-process](https://user-images.githubusercontent.com/56327550/198270076-af6fbb40-6dfa-4f5c-82e0-d6480eecb26e.png)

### Atoms
#### 기본적인 HTML Elements들(labels, inputs, buttons, etc...)

### Molecules
#### UI elements들의 그룹으로서, 하나의 기능 동작 가능한 요소
> molecules are relatively simple groups of UI elements functioning together as a unit.

![molecule-search-form](https://user-images.githubusercontent.com/56327550/198270715-9f4e68ab-0592-42f2-a6f0-c3e77c0fa5d5.png)

> Input + Button = search form

### Organisms
#### molecules과 atoms들로 구성된 하나의 유기체.(ex. nav bar)
> Organisms are relatively complex UI components composed of groups of molecules and/or atoms and/or other organisms.

### Templates
#### 뼈대가 완성된(contents만 빠진 skeleton layout)

### Pages
#### 완성된 페이지


### Instagram example
![instagram-atomic](https://user-images.githubusercontent.com/56327550/198271793-042839d9-93b5-43c4-ba1d-369f3abc1ffe.png)


### example
![화면 캡처 2022-10-27 203925](https://user-images.githubusercontent.com/56327550/198274800-31b5a603-91c0-4287-8f9d-9ed72ab85af0.jpg)





## References
[Atomic Design Methodology](https://atomicdesign.bradfrost.com/chapter-2/)   
