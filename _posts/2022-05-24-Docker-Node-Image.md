---
title: Docker Node Image 만들기
date: 2022-05-24 00:50:00 +09:00
categories: [DOCKER]
tags: [docker]
---
## 도커를 이용해 Node.js 애플리케이션 만들기
1. Node.js application 만들기
2. 도커 이미지 생성

![node1](https://user-images.githubusercontent.com/56327550/169707544-387a1006-c6e5-4465-82b9-8e3005dfaba5.JPG)

- COPY 하는 이유: 이미지 생성 과정에서 임시 컨테이너 안에 package.json이 없기때문에 npm install 과정에서 에러가 발생한다. 따라서 package.json을 컨테이너 안으로 넣어줘야 한다.

`````
빌드
\react\nodejs-docker-app>docker build -t milo/node-app ./
`````

**하지만 실행하면 server.js를 못찾는 에러 발생! package.json과 같이 server.js도 컨테이너 안으로 넣어줘야한다.**

![node2](https://user-images.githubusercontent.com/56327550/169707790-7750fcb4-201e-4ac1-8a9e-be3102aa06e7.JPG)

`````
빌드
\react\nodejs-docker-app>docker build -t milo/node-app ./

실행
\react\nodejs-docker-app>docker run -p 5000:8080 milo/node-app
server listening...
`````
> PORT Mapping(-p option)   
> 로컬호스트 포트와 컨테이너 포트가 나뉘어 있어서   
> **브라우저에서 애플리케이션에 접속하려면 포트 매핑 필요.**
`````
$ docker run -p <localhost Port>:<Container Port> <Image name>
`````

### 작업 directory 설정하기 
- COPY 한 파일들이 컨테이너 안의 최상단 폴더에 위치하게 되어 기존 파일을 덮어쓰게될 위험이 있다. 
- 폴더가 복잡해진다.
`````
*directory설정 안했을 때 컨테이너 파일구조
Dockerfile  boot  etc   lib    media  node_modules  package-lock.json  proc  run   server.js  sys  usr
bin         dev   home  lib64  mnt    opt           package.json       root  sbin  srv        tmp  var
`````

Dockerfile에 WORKDIR 추가
`````
FROM node

WORKDIR /usr/src/app

COPY ./ ./

RUN npm install

CMD [ "node", "server.js" ]
`````

## 코드 수정할 때마다 모든 종속성을 다시 다운받지 않도록 수정
`````
FROM node

WORKDIR /usr/src/app

COPY package.json ./

RUN npm install

COPY ./ ./

CMD [ "node", "server.js" ]
`````
RUN npm install  전 단계의 COPY에서 조금이라도 변화가 있다면 다시 내려받고,    
아무런 변화가 없다면 캐시를 이용해 이과정을 생략한다.   

## Docker volume 이용하기   
- 파일들을 컨테이너로 복사하지않고 참조하도록 설정하는 것.
- COPY 사용시 코드가 변경될 때마다 복사, 빌드, 실행을 해야한다.   
volume을 이용하면 호스트 디렉터리의 파일을 참조하기때문에 COPY하여 이미지를 빌드할 필요가 없다.   
`````
$ docker run -p 3000:8080 -v /usr/src/app/node_modules -v %cd%:/usr/src/app milo/node-app 
`````
> 뒤에 있는 -v의 의미: cd(절대경로) 뒤의 작업 directory를 참고해 애플리케이션 실행한다.
> 앞에 있는 -v의 의미: node_modules는 호스트를 참조하지않는다.


## Reference
- 따라하며 배우는 도커와 CI환경 -위키북스









