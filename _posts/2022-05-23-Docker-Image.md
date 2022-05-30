---
title: Docker Image create 도커 이미지 만들기
date: 2022-05-23 00:50:00 +09:00
categories: [DOCKER]
tags: [docker]
---
## 직접 도커 이미지 생성하기
1. 도커파일(Dockerfile) 작성 : 컨테이너가 어떻게 행동해야 하는지에 대한 설정
2. 도커파일에 입력한 명령어들이 도커 클라이언트에 전달
3. 도커 클라이언트에 전달된 명령들을 도커 서버에서 처리후 도커 이미지 생성

### Dockerfile 생성

1. Base Image  : Windows, MacOS, Linux ...
2. 애플리케이션 실행하는 데 필요한 파일들을 이미지 안에 내려받기 위한 명령어 명시
3. 명령어 명시

#### Dockerfile basic structure
![캡처555](https://user-images.githubusercontent.com/56327550/169705118-829404fe-2246-47af-a3dc-6286b0325b49.JPG)
- FROM
  - 이미지 생성시 기반이 되는 이미지 레이어 명시
  - <이미지 이름>:<태그> 형식
  - ex) ubuntu:14.04
- RUN
  - 도커 이미지가 생성되기 전에 수행할 셸 명령어
- CMD
  - 컨테이너가 시작됐을 때 실행할 실행 파일 또는 셸 스크립트
  - 이 명령어는 도커 파일 내에서 한 번만 사용 가능

#### Say Hello Image Simple example 만들기
![hello1](https://user-images.githubusercontent.com/56327550/169705582-c6a72ffd-7f1f-4675-be29-03f66d2c372a.JPG)

`````
빌드
\react\dockerfile-folder>docker build .

Sending build context to Docker daemon  2.048kB
Step 1/2 : FROM alpine
 ---> 0ac33e5f5afa
Step 2/2 : CMD [ "echo", "hello" ]
 ---> Running in 30dd11c5a82c
Removing intermediate container 30dd11c5a82c
 ---> b8e25d022de6
Successfully built b8e25d022de6
`````
> 빌드과정은 다음과 같다.
> 1. 베이스 이미지를 가져온다. (alpine)
> 2. 임시 컨테이너를 생성한다.
> 3. alpine 이미지 내의 파일 snapshot을 컨테이너의 하드디스크로 복사.
> 4. 실행할 명령어 'echo', 'hello'가 임시 컨테이너로 들어감.
> 5. 임시 컨테이너 기반으로 실제 컨테이너 생성

`````
실행
\react\dockerfile-folder>docker run -it b8e25d022de6
hello
`````
`````
naming Image
\react\dockerfile-folder>docker build -t milo/hello:latest .

\react\dockerfile-folder>docker run -it milo/hello
hello
`````


## Reference
- 따라하며 배우는 도커와 CI환경 -위키북스









