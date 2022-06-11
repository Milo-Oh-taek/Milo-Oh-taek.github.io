---
title: docker react setting
date: 2022-06-06 19:00:00 +09:00
categories: [DOCKER]
tags: [docker]
---
## React docker dev circumstance
### Dockerfile.dev
`````
FROM node

WORKDIR /usr/src/app

COPY package.json ./

RUN npm install

COPY ./ ./

CMD ["npm", "run", "start"]
`````
### build & execute
`````
$ docker build -f Dockerfile.dev -t milo/docker-react-app ./
$ docker run -it -p 3000:3000  milo/docker-react-app
`````

### 코드 변경시 빌드할 필요없이 실행할 수 있도록 docker volume 사용법
`````
$ docker run -p 3000:3000 -v /usr/src/app/node_modules -v %cd%:/usr/src/app milo/docker-react-app
`````

### docker compose로 쉽게 실행하기
### docker-compose-dev.yml
`````
version: "3"	// docker compose version
services:	// define containers
  react:	// service name
    build:	// build info
      context: .	// location of files and folders
      dockerfile: Dockerfile.dev	// docker file
    ports:	// local : container
      - "3000:3000"
    volumes:
      - /usr/src/app/node_modules
      - ./:/usr/src/app
    environment:
      - CHOKIDAR_USEPOLLING=true	// hot reloading
    stdin_open: true
  tests:
    build:
      context: .
      dockerfile: Dockerfile.dev
    volumes:
      - /usr/src/app/node_modules
      - ./:/usr/src/app
    command: ["npm", "run", "test"]
`````


### 테스트 진행법
`````
$ docker build -f Dockerfile.dev ./
$ docker run -it milo/docker-react-app npm run test
`````

## React docker prod circumstance

1. Builder Stage : build file create
2. Run Stage : respond static files through Nginx

### Dockerfile
`````
FROM node:alpine as builder		// notice that it's builder stage til next 'FROM' by using 'as builder'
WORKDIR '/usr/src/app'
COPY package.json .
RUN npm install
COPY ./ ./
RUN npm run build

FROM nginx
COPY --from=builder /usr/src/app/build /usr/share/nginx/html
`````

`````
$ docker build -t milo/docker-react-app ./
$ docker run -p 8080:80 milo/docker-react-app
`````

### docker-compose.yml
`````
version: "3"
services:
  react:
    build:
      context: .
      dockerfile: Dockerfile
    ports:
      - "80:80"
    volumes:
      - /usr/src/app/node_modules
      - ./:/usr/src/app
    stdin_open: true

`````



## Reference
[https://docs.docker.com/network/overlay/#publish-ports](https://docs.docker.com/network/overlay/#publish-ports)










