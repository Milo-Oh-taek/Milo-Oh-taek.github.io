---
title: docker react deployment - travis ci, aws elastic beanstalk
date: 2022-06-15 23:00:00 +09:00
categories: [DOCKER]
tags: [docker, aws, travisci]
---
## travis ci
### CI - Continuous Integration
github에서 코드 변경과 같은 특정 이벤트에 따라 자동으로 테스트 및 빌드, 배포 가능.
대표적으로 Travis CI, Jenkins.


1. [https://travis-ci.com](https://travis-ci.com)
2. Sign in with github account
3. Verifying email
4. activate repositories
5. register Plan (settings - plan - free trial)
6. .travis.yml
7. github push

`````
.travis.yml

sudo: required		//관리자 권한 부여

language: generic		// language platform

services:
  - docker

before_install:
  - echo "start creating an image with dockerfile"
  - docker build -t milo/docker-react-app -f Dockerfile.dev .

script:			// test
  - docker run -e CI=true milo/docker-react-app npm run test -- --coverage

after_success:
  - echo "Test Success"
`````

(travis-cli)My Repositories - Current
![travis](https://user-images.githubusercontent.com/56327550/172177168-8605bc5b-fe61-46ef-8130-62c71467edc3.JPG)

## aws - elastic beanstalk
AWS Elastic Beanstalk는 Java, .NET, PHP, Node.js, Python, Ruby, Go 및 Docker를 사용하여 개발된 웹 애플리케이션 및 서비스를 Apache, Nginx, Passenger 및 IIS와 같은 친숙한 서버에서 손쉽게 배포하고 확장할 수 있는 서비스   

**인스턴스, 데이터베이스, 보안그룹, 로드밸런서 등 다양한 서비스를 포함한 환경을 구성하고 관리해준다!**

### aws - Elastic Beanstalk - create application

- application name: docker-react-app
![elastic app](https://user-images.githubusercontent.com/56327550/172178866-df87ae6f-c8fb-450d-9b5f-eddfdd222542.JPG)

`````
.travis.yml

sudo: required

language: generic

services:
  - docker

before_install:
  - echo "start creating an image with dockerfile"
  - docker build -t milo/docker-react-app -f Dockerfile.dev .

script:
  - docker run -e CI=true milo/docker-react-app npm run test -- --coverage
after_success:
  - echo "Test Success"

deploy:				// add new
  edge: true
  provider: elasticbeanstalk	// service ex)elasticbeanstalk, firebase, s3, ...
  region: ap-northeast-2		// aws region. seoul: ap-northeast-2
  app: docker-react-app		// app name
  env: DockerReactApp-env		// UpperCamelCase(=PascalCase) of app name
  bucket_name: elasticbeanstalk-ap-northeast-2-879757627605		// s3 bucket name
  bucket-path: docker-react-app
  on:
    branch: main		// sense which branch ex) main, dev, ...
`````

### IAM user 생성
IAM - 액세스 관리 - 사용자 - 사용자 추가   
user : docker-react-user   
aws자격증명유형 : 액세스 키 - 프로그래밍 방식   
권한: 기존정책직접연결 : AdministratorAccess-AWSElasticBeanstalk   
key, pass 복사   

travis-ci dashboard - More options : Settings - Environment Variables   
AWS_ACCESS_KEY, AWS_SECRET_ACCESS_KEY 입력   

`````
.travis.yml에 추가

access_key_id: $AWS_ACCESS_KEY
secret_access_key: $AWS_SECRET_ACCESS_KEY
`````

`````
DockerFile

FROM node:alpine as builder
WORKDIR '/usr/src/app'
COPY package.json .
RUN npm install
COPY ./ ./
RUN npm run build

FROM nginx
EXPOSE 80			// 포트 설정 추가
COPY --from=builder /usr/src/app/build /usr/share/nginx/html
`````

![finished](https://user-images.githubusercontent.com/56327550/172192706-0816c7e4-404c-46e9-944d-90c8058fe5ec.JPG)

## Reference
[https://docs.docker.com/network/overlay/#publish-ports](https://docs.docker.com/network/overlay/#publish-ports)










