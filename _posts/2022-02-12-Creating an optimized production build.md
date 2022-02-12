---
title: Creating an optimized production build...
date: 2022-02-12 10:40:00 +09:00
categories: [AWS, ERROR]
tags: [aws]
---

빌드시 Creating an optimized production build... 에서 Freeze

## 원인
메모리 부족... 프리티어의 비애

## 해결법
1. GENERATE_SOURCEMAP option off
    ```
    "build": GENERATE_SOURCEMAP=false npx react-scripts build
    ```
    디버깅 정보 불포함하여 빌드 됨

2. Memory swap
    ```
    1.sudo dd if=/dev/zero of=/mnt/swapfile bs=1M count=2048
    2.sudo mkswap /mnt/swapfile
    3.sudo swapon /mnt/swapfile
    ```
    >순서대로 명령어 실행   
    >메모리의 부족한 부분을 디스크의 일부를 사용하여 대신 사용
    >스왑 사용시 속도가 느려진다는 단점

    ```
    swap 해제
    1.sudo dd if=/dev/zero of=/mnt/swapfile bs=1M count=2048
    2.sudo mkswap /mnt/swapfile
    3.sudo swapon /mnt/swapfile
```


출처: https://progdev.tistory.com/26 [플머의 개발 연구소]




