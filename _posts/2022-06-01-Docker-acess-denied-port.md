---
title: "Docker localhost에서 연결을 거부했습니다 에러 access denied"
date: 2022-06-01 21:00:00 +09:00
categories: [DOCKER, Error]
tags: [docker, access, port]
---
## 도커 실행후 웹브라우저로 접근시 access denied with localhost error 발생
나의 경우는 포트 설정의 문제였다.

### 도커 컨테이너 포트 포워딩 설정

`````
$ docker run -p <host port>:<container port>/<protocol> [IMAGE NAME]
`````

- host port : 호스트 시스템 사용 포트
- container port : 컨테이너 내의 포트 번호
- protocol 생략시 기본 tcp 프로토콜로 설정

`````
$ -p 8080:80  // 호스트 8080포트 - 컨테이너 80포트 연결

$ docker ps  // PORTS : 0.0.0.0:8080->80/tcp
`````

## Reference
[https://docs.docker.com/network/overlay/#publish-ports](https://docs.docker.com/network/overlay/#publish-ports)










