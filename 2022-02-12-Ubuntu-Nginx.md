---
title: EC2 ubuntu18 nginx
date: 2022-02-12 10:40:00 +09:00
categories: [AWS, Ubuntu]
tags: [ubuntu, nginx]
---

## Nginx 설치
패키지 목록 업데이트 & nginx 설치
```
$sudo apt update
$sudo apt install nginx
```
## Nginx 전체 삭제
```
$sudo apt-get purge nginx nginx-common
```
## Nginx 시작
```
$sudo systemctl start nginx
```
## Nginx 재시작
```
$sudo systemctl restart nginx
```
## Nginx 중지
```
$sudo systemctl stop nginx
```
## Nginx 설정 test
```
$sudo nginx -t
```
## Nginx 경로
모든 Nginx 구성 파일 위치
```
/etc/nginx
```
기본 구성 파일 위치
```
/etc/nginx/nginx.conf
```


