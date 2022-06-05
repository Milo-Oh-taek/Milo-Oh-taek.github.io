---

title: Docker basic

date: 2022-05-22 17:50:00 +09:00

categories: [DOCKER]

tags: [docker]

---

## 도커를 사용하는 이유

어떠한 프로그램을 내려받는 과정을 간단하게 만들기 위해서



### 도커 사용 vs 도커 미사용

- 도커 미사용시(without Docker) : Installer download => Excute Installer => Install complete



이러한 경우 Server, Package version, OS 에 따라 Error 발생 가능성 높음



### Docker?

- Container : 코드와 모든 종속성을 패키지화하여 응용 프로그램이 한 컴퓨팅 환경에서 다른 컴퓨팅 환경으로 빠르고 안정적으로 실행되도록 하는 소프트웨어의 표준 단위.



- Docker Image : 코드, 런타임, 시스템 도구, 시스템 라이브러리 및 설정과 같은 응용 프로그램을 실행하는 데 필요한 모든 것을 포함하는 가볍고 독립적이며 실행 가능한 소프트웨어 패키지.



=> **도커 컨테이너는 도커 이미지로 만든다.**   

=> **도커 이미지 안에는 응용 프로그램을 실행하는 데 필요한 모든 설정과 종속성이 필요하다.**   

=> **도커 컨테이너를 도커 이미지의 인스턴스라고 부른다.**   

=> **도커 이미지를 이용해 컨테이너를 생성하고 컨테이너를 이용해 프로그램을 실행한다.**   



> Docker is a software platform that allows you to build, test, and deploy applications quickly. Docker packages software into standardized units called containers that have everything the software needs to run including libraries, system tools, code, and runtime. Using Docker, you can quickly deploy and scale applications into any environment and know your code will run. - ([aws](https://aws.amazon.com/docker/?nc1=h_ls))



> 도커(Docker)는 리눅스의 응용 프로그램들을 프로세스 격리 기술들을 사용해 컨테이너로 실행하고 관리하는 오픈 소스 프로젝트이다. - [wikipedia](https://ko.wikipedia.org/wiki/%EB%8F%84%EC%BB%A4_(%EC%86%8C%ED%94%84%ED%8A%B8%EC%9B%A8%EC%96%B4))



### Install

[Install](https://www.docker.com/get-started/)



check Install & version

`````

$docker version



Server: Docker Desktop 4.8.2 (79419)

 Engine:

  Version:          20.10.14

  API version:      1.41 (minimum version 1.12)

  Go version:       go1.16.15

  Git commit:       87a90dc

  Built:            Thu Mar 24 01:46:14 2022

  OS/Arch:          linux/amd64

`````



- **Client가 mac or windows 여도, docker server는 linux vm 환경에서 실행됨**

- **따라서 도커 컨테이너를 격리할 수 있는 Cgroup, namespace 사용 가능**





hello world

`````

$docker run hello-world



Unable to find image 'hello-world:latest' locally

latest: Pulling from library/hello-world

2db29710123e: Pull complete

Digest: sha256:80f31da1ac7b312ba29d65080fddf797dd76acfb870e677f390d5acba9741b17

Status: Downloaded newer image for hello-world:latest



Hello from Docker!

This message shows that your installation appears to be working correctly.





To generate this message, Docker took the following steps:

 1. The Docker client contacted the Docker daemon.

 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.

    (amd64)

 3. The Docker daemon created a new container from that image which runs the

    executable that produces the output you are currently reading.

 4. The Docker daemon streamed that output to the Docker client, which sent it

    to your terminal.

`````

1. 클라이언트에서 도커 서버로 요청

2. 로컬에서 hello-world 이미지 있는지 확인

3. 없기 때문에 'Unable to find image~~' 출력

4. Docker hub에서 hello-world 이미지 가져오고 로컬에 보관

5. 이미지 이용해서 컨테이너 생성

6. 이미지에서 받은 설정이나 조건에 따라 프로그램 실행



## Reference

- 따라하며 배우는 도커와 CI환경 -위키북스

- https://aws.amazon.com/docker/























