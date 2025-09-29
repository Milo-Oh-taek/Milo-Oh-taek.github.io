---
title: springboot dto groups - validation created일때만 적용하기
date: 2025-09-25 23:47:00 +01:00
categories: [SPRINGBOOT]
tags: [springboot, jpa]
---

### DTO를 Create, Update 공용으로 사용할때, Create일때만 validation 적용하기

#### Interface file 생성

CreateValidationGroup이라는 빈 인터페이스를 만들어준다.

```
com.demo.microservice
ㄴ validators
  ㄴ CreateValidationGroup
```

#### DTO groups 지정

해당 DTO Field Validation에 groups을 지정한다.

```
@NotBlank(groups = CreateValidationGroup.class, message = "Registered date is required")
    private String registerDate;
```

#### Controller에 적용

PUT에는 Default만 적용, POST에는 Default + CreateValidationGroup

```
@PostMapping
    public ResponseEntity<ResponseDTO> create(@Validated({Default.class, CreateValidationGroup.class}) @RequestBody RequestDTO RequestDTO){
    }
```
