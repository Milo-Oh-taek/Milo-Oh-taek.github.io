---
title: react gitlab aws s3 ci/cd
date: 2025-09-12 20:40:00 +01:00
categories: [CICD]
tags: [react, s3, aws, cicd, gitlab]
---

## Create a S3 bucket

### 권한

- 모든 퍼블릭 액세스 차단 Disable
- 버킷 정책

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "Statement1",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::ohtvitebucket/*"
        }
    ]
}
```

> Resource: arn + "/\*"

## Create IAM User

- AmazonS3FullAccess

## Gitlab

### Secret settings

#### Project -> Settings -> CI/CD -> Variables

- AWS_ACCESS_KEY_ID
- AWS_SECRET_ACCESS_KEY
- AWS_DEFAULT_REGION
- S3_BUCKET

### .gitlab-ci.yml

```
stages:
    - build
    - deploy

build:
    stage: build
    image: node:23
    script:
        - echo "build started"
        - npm install
        - npm run build
    artifacts:
        paths:
            - dist/

deploy:
    stage: deploy
    image:
        name: amazon/aws-cli
        entrypoint: [""]
    script:
        - aws --version
```

> build 산출물 dist를 artifacts 지정하여 deploy에서 사용
