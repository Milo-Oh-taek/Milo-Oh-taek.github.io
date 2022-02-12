---
title: WARNING REMOTE HOST IDENTIFICATION HAS CHANGED!
date: 2022-02-12 10:40:00 +09:00
categories: [AWS, ERROR]
tags: [aws, ssh]
---

### 원인
IP는 동일하나 목적지 서버 장비 등이 바뀌었을 때 발생

### 해결법

```
ssh-keygen -R [host]
```

> **-R hostname** Removes all keys belonging to hostname from a known_hosts file. This option is useful to delete hashed hosts (see the -H option above).




