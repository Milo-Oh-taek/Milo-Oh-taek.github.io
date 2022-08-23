---
title: Docker command
date: 2022-05-23 00:50:00 +09:00
categories: [DOCKER]
tags: [docker]
---
## 기본적인 도커 클라이언트 명령어

### 도커 이미지 내부 파일 구조 보기

`````
$docker run alpine ls

Unable to find image 'alpine:latest' locally
latest: Pulling from library/alpine
df9b9388f04a: Pull complete
Digest: sha256:4edbd2beb5f78b1014028f4fbb99f3237d9561100b6881aabbf5acce2c4f9454
Status: Downloaded newer image for alpine:latest
bin
dev
etc
home
lib
media
mnt
opt
proc
root
run
sbin
srv
sys
tmp
usr
var
`````

- alpine image file snapshot 안에는 ls 명령어를 사용할 수 있는 파일이 존재하기에 사용 가능.

`````
$ docker run hello-world ls

docker: Error response from daemon: failed to create shim: OCI runtime create failed: container_linux.go:380: starting container process caused: exec: "ls": executable file not found in $PATH: unknown.
`````

### 현재 실행 중인 컨테이너 나열
`````
$ docker ps (-a : 중단된 컨테이너도 다 보기 옵션)

CONTAINER ID   IMAGE     COMMAND             CREATED          STATUS         PORTS     NAMES
dd5b16cda50d   alpine    "ping google.com"   10 seconds ago   Up 9 seconds             frosty_agnesi
`````

### 컨테이너 생성 및 실행
`````
$ docker run = docker create + docker start

$ docker start (-a : print results)
`````

### 컨테이너 멈추기
`````
$ docker stop : stop after being finished
$ docker kill : stop immediately
`````

### 컨테이너 삭제
`````
$ docker rm
$ docker rm `docker ps -a -q` : 중지된 모든 컨테이너 삭제
$ docker rmi : 도커 이미지 같이 삭제
$ docker system prune : 사용하지 않는 데이터 삭제
`````

### 실행중인 컨테이너에 명령어 전달
`````
$ docker exec (-it : 명령어 실행 후 계속 명령어 적을 수 있는 옵션)
`````
### 실행중인 컨테이너에서 터미널 사용
`````
$ docker exec -it sh
$ docker run -it sh
$ docker run -d // detached mode
`````

### Run vs Start
- Docker Run: build a new container based on the image, Attached Mode
- Docker Start: restart already built one, Detached Mode(background running)

## Reference
- 따라하며 배우는 도커와 CI환경 -위키북스
- [udemy](https://www.udemy.com/course/docker-kubernetes-2022)









