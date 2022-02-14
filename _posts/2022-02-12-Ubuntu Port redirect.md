---
title: EC2 ubuntu port redirect 포트 리다이렉트 포워딩
date: 2022-02-12 10:40:00 +09:00
categories: [AWS]
tags: [ubuntu, port]
---

## Port Redirect (ex. 80 => 3000)
```
$sudo iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 80 -j REDIRECT --to-port 3000
```
## 사용중인 Port redirect list
```
$sudo iptables -t nat -L --line-numbers
```
## Port Redirect 삭제
```
$sudo iptables -t nat -D PREROUTING 번호
```
>Redirect List 조회 후 해당 번호로 삭제


