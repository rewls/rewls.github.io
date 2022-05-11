---
layout: default
title: Docker Introduction
parent: Linux
nav_order: 6
mathjax: true
---

# Docker Introduction
{: .no_toc }

> [참고](https://www.44bits.io/ko/post/easy-deploy-with-docker)

<details open markdown="block">
  <summary>
    Toggle
  </summary>
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
</details>

---

- 리눅스 상에서 컨테이너 방식으로 프로세스를 격리해서 실해하고 관리할 수 있도록 도와주며, 계층화된 파일 시스템에 기반해 효율적으로 이미지(프로세스 실행 환경)을 구축할 수 있도록 해준다.

- 도커를 사용하면 이미지 기반으로 컨테이너를 실행할 수 있으며, 다시 특정 컨테이너의 상태를 변경해 이미지로 만들 수 있다.

- 이미지는 파일로 보관하거나 원격 저장소를 사용해 쉽게 공유할 수 있으며, 도커만 설치되어 있다면 필요할 때 컨테이너로 실행할 수 있다.

## 도커 시작하기: 우분투에서 센트OS로 프로세스 실행하기

- 컨테이너는 하드웨어를 소프트웨어로 재구현하는 가상화(=가상머신)와는 달리 프로세스의 실행 환경을 격리한다.

- 컨테이너가 실행되고 있는 호스트 입장에서 컨테이너는 단순히 프로세스에 불과하지만 사용자나 컨테이너 입장에서는 호스트와는 무관하게 동작하는 가상머신처럼 보인다.

- 도커는 가상머신과 같이 하드웨어를 가상화하는 것이 아니라, 리눅스 운영체제에서 지원하는 다양한 기능을 사용해 컨테이너(하나의 프로세스)를 실행하기 위한 별도의 환경(파일 시스템)을 준비하고, 리눅스 네임스페이스와 다양한 커널 기능을 조합해 프로세스를 특별하게 실행시켜준다.

- 운영체제 상에서 지원하는 방법을 통해서 하나의 프로세스(컨테이너)를 실행하기 위한 별도의 환경을 구축한다. 도커는 프로세스를 격리시켜 실행해주는 도구이다.

```
docker run -it --rm centos:latest bash
```

```
cat /etc/*release
```

---

## 도커(Docker) 설치 및 기본 설정

```
curl -s https://get.docker.com | sudo sh
```

```
docker -v
```

```
dpkg --get-selections | grep docker
```

```
docker ps
```

- 현재 실행 중인 모든 컨테이너 목록 출력

---

## 도커 이미지(Docker Image) 기초

- 이미지는 어떤 애플리케이션을 실행하기 위한 환경이다.

- 이 환경은 파일들의 집합이다.

- 도커에서는 애플리케이션을 실행하기 위한 파일들을 모아놓고, 애플리케이션과 함께 이미지로 만들 수 있다.

- 이 이미지를 기반으로 애플리케이션을 바로 배포할 수 있다.

앞에서 살펴 본 예제에서는 centos 컨테이너에서 bash 셸을 실행했다. 이 과정을 좀 더 풀어 써보면 다음과 같다.

1. **도커 레지스트리에서 centos 이미지를 pull 받는다.**

2. 이 이미지를 통해서 컨테이너를 실행한다.

```
docker images
```

- 이미지 목록

```
docker pull <IMAGE_NAME>
```

- 이미지를 pull한다.

- 이미지 이름은 :을 구분자로 이미지 이름과 태그로 구분된다. 태그를 지정하지 않으면 기본값으로 latest가 사용된다.

- 도커는 먼저 이 이미지를 로컬에서 찾아보고, 찾을 수 없으면 도커 공식 저장소에서 찾아본다.

```
docker push
```

- 이미지 업로드

```
docker commit
```

- 새로운 이미지 생성

```
docker diff
```

- 이미지의 차이 확인

- 도커에서는 하나의 이미지를 저장소$^{\text{repository}}$라고 한다.

- TAG는 임의로 붙여진 추가적인 이름. 일반적으로 이미지의 버저닝을 하기 위해서 사용한다.

### 도커 허브(Docker Hub) - 공식 이미지 레지스트리

> [도커 허브](https://hub.docker.com/)

```
docker info | grep Registry
```

- index.docker.io는 도커 허브의 과거 도메인

- 일반적으로 도커가 제공하는 공식 이미지에는 네임스페이스가 없다(생략됨).

- 이미지 이름에 슬래시가 있을 경우 슬래시 앞 부분이 네임스페이스가 되고 슬래시 뒷 부분이 실제 이미지 이름이 된다.

---

## 컨테이너(Container) 이해하기 - 격리된 환경에서 실행되는 프로세서

1. 도커 레지스트리에서 centos 이미지를 pull 받는다.

2. **이 이미지를 통해서 컨테이너를 실행한다.**

- 이미지는 환경이 구성되어있는 상태를 저장해놓은 파일 집합이고, 컨테이너는 이 파일들의 집합 위해서 실행된 특별한 프로세스이다.

```
docker run -it <이미지이름:태그> <명령어>
```

```
docker run -it centos:latest bash
```

- 컨테이너 실행

- 여기서는 SSH를 통해 서버에 접속한 것이 아니라, 호스트OS와 격리된 환경에서 bash 프로그램을 실행한 것

```
docker ps
```

- 현재 실행중인 컨테이너 목록 출력

- `docker run --name <name>` : 컨테이너 이름 지정

	- 지정하지 않으면 임의의 이름이 자동적으로 부여된다.

- `rename` : 컨테이너 이름 변경

- `docker ps -a` : 모든 컨테이너 목록 출력

- 보통 이미지들은 명령어 기본값이 지정되어 있다.

	- 어플리케이션을 담고 있는 이미지라면 기본적으로 어플리케이션을 실행하는 스크립트가 기본 명령어로 지정되어 있다.

```
exit or Ctrl+D
```

- 셸 종료

- 컨테이너는 SSH 서버가 아니라 배시 셸 프로세스이기 때문에 셸을 종료하면 컨테이너도 종료된다.

```
docker restart <컨데이너 id>
```

- 컨테이너 재시작

```
docker attach <컨테이너 id>
```

- 재시작한 컨테이너 실행

```
Ctrl+p, Ctrl+q
```

- 컨테이너를 종료하지 않고 나온다.


- `stop`: 실행된 컨테이너 강제 종료

- `rm`: 종료된 컨테이너 삭제

- `run --rm`: 컨테이너가 종료되면 자동으로 삭제

> 컨테이너는 **가상머신**이라기보다는 **프로세스**이다.

---

## 도커와 버전 관리 시스템

- 컨테이너를 굴려도 이미지에는 변화가 생기지 않는다.

- 계층화된 파일 시스템을 사용한다.

- 특정 이미지로부터 생성된 컨테이너에 어떤 변경사항을 더하고 변경된 상태를새로운 이미지로 만들 수 있다.

- 공식 우분트 이미지는 사용자가 루트로 설정되어 있다. 따라서 `sudo`와 같은 명령어가 없어도 `apt`를 직접 사용해 패키지를 설치할 수 있다.

```
docker diff <컨테이너 id> | head
```

- `A` : Add / `C` : Change / D : Delete

```
docker commit <컨테이너 id> <이미지명>:<태그>
```

- 이미지에서 파생된 (종료 상태를 포함한) 컨테이너가 남아있으면 이미지는 삭제할 수 없다. 컨테이너를 종료하고 삭제해줘야한다.

```
docker rm
```

- 컨테이너 삭제

```
docker rmi
```

- 이미지 삭제

---

## Dockerfile로 이미지 만들기

### 도커 이미지 추가하는 방법

1. `pull`을 사용해 미리 만들어져 있는 이미지 가져오기

2. `commit`을 사용해 컨테이너의 변경사항으로부터 이미지 만들기

	- 이렇게 이미지를 만드는 경우는 거의 없다.

3. **Dockerfile 빌드**

	- 도커의 DSL로 이미지를 정의하는 파일

#### Dockerfile로 Git이 설치된 우분투 이미지 정의

```
From ubuntu:bionic
Run apt-get update
Run apt-get install -y git
```

- `FROM`: 어떤 이미지로부터 이미지를 생성할지 지정. 필수 항목

- `RUN`: 명령어 실행

---

## 모니위키(moniwiki) 도커 파일 작성하기

- 모니위키는 PHP와 아파치 서버를 기반으로 동작하는 웹 애플리케이션

- 애플리케이션 실행을 위해 도커 이미지를 만드는 작업을 도커라이징$^{\text{Dockerizing}}$이라고 한다.

- 미리 만들어 둔 Dockerfile의 내용을 살펴본다.

```
git clone https://github.com/nacyot/docker-moniwiki.git
cd docker-moniwiki/moniwiki
```

```
FROM ubuntu:14.04

RUN apt-get update &&\
  apt-get -qq -y install git curl build-essential apache2 php5 libapache2-mod-php5 rcs

WORKDIR /tmp
RUN \
  curl -L -O https://github.com/wkpark/moniwiki/archive/v1.2.5p1.tar.gz &&\
  tar xf /tmp/v1.2.5p1.tar.gz &&\
  mv moniwiki-1.2.5p1 /var/www/html/moniwiki &&\
  chown -R www-data:www-data /var/www/html/moniwiki &&\
  chmod 777 /var/www/html/moniwiki/data/ /var/www/html/moniwiki/ &&\
  chmod +x /var/www/html/moniwiki/secure.sh &&\
  /var/www/html/moniwiki/secure.sh

RUN a2enmod rewrite

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2

EXPOSE 80

CMD bash -c "source /etc/apache2/envvars && /usr/sbin/apache2 -D FOREGROUND"
```

- `&&\`: Run 하나에 여러 명령어를 나눠 실행하는 데 사용

- `WORKDIR : 이후에 실행되는 모든 작업의 실행 디렉터리 변경

	- 매번 실행 위치가 초기화되기 때문에 `cd`보다는 `WORKDIR`을 사용한다.

- `ENV`: 컨테이너 실행 환경에 적용되는 호나경변수의 기본값을 지정

- `EXPOSE`: 가상머신에 오픈할 포트 지정

- `CMD`: 컨테이너에서 실행될 명령어 지정

```
docker build -t nacyot/moniwiki:latest .
```

```
docker run -d -p 9999:80 nacyot/moniwiki:latest
```

- `-d`: `-i`의 반대. 컨테이너를 백그라운드에서 실행한다.

- `-p`: 포트포워딩 지정

	- `:`을 경계로 앞에는 외부 포트, 뒤에는 컨테이너 내부 포트 지정

- ip주소:9999/moniwiki/wiki.php 접속

### 도커파일 작성하기

- 대부분의 경우 `FROM`, `RUN`, `WORKDIR`, `ADD`, `CMD` 정도면 원하는 이미지를 만들 수 있다.

- Dockerfile을 처음부터 완성하기보다는 중간중간 빌드하면서 작업한다.

	- 도커는 도커 이미지 빌드 과정을 캐시하기 때문에 내용이 변하지 않은 부분까지는 빠르게 빌드된다.

### 도커의 이미지 빌드 과정

- 지시자 하나 하나가 스탭이 된다.

- 스탭 하나를 빌드할 때마다, 1. 컨테이너 생성, 2. 지시자 실행, 3. 임시 이미지 생성 과정을 거친다.

```
docker history moniwiki:latest
```

- 생성된 중간 이미지 확인

- 이미지가 `<missing>인 경우는 베이스 이미지인 우분투 이미지의 빌드 내용

- 중간 이미지는 로컬 머신에서 직접 빌드한 경우에만 생성된다.

- 중간 이미지에서 컨테이너를 실행할 수도 있다.

---

## 실전: 도커 이미지로 서버 애플리케이션 배포하기

- 애플리케이션을 서버에서 운영하려면 프로비저닝 과정을 거쳐야 한다.

	- 프로비저닝은 서버의 환경을 어떤 애플리케이션이 실행 가능한 상태로 준비하는 과정을 의미한다.

- 도커만 있으면 미리 준비한 이미지를 실행할 수 있기 때문에 리눅스 계열이라면 서버 환경에 크게 구애받지 않는다.

- 컨테이너로 실행되는 독자적인 환경을 가지고 있기 때문에 서버의 변화에도 거의 영향을 받지 않는다.

- 과거에 만들어둔 이미지가 있다면 대부분의 경우 잘 동작한다.

	- 이미지는 없고 Dockerfile만 있다면 잘 되리라 보장하기 어렵다.

	- 초기화 작업에 외부 의존성이 없다면 큰 문제 없이 실행된다.

### 도커 허브에 이미지 올리기

```
docker info | grep Registry
```

- 도커 허브의 API 서버 주소 출력됨

- 도커 클라이언트는 기본적으로 도커 레지스트리를 도커 허브로 사용한다.

- 도커 이미지의 풀네임에는 도커 레지스트리의 주소가 포함되어있다.

	- ubuntu:bionic의 풀네임은 docker.io/library/ubuntu:bionic

```
docker pull docker.io/library/ubuntu:bionic
```

- 이미지 풀네임 `도커 레지스트리의 서버 주소/네임스페이스/이미지 이름:태그` 형식

- 도커 허브의 경우 네임스페이스가 곧 사용자 이름이다. library는 도커 공식 이미지를 제공하는 네임스페이스

- 하나의 이미지 저장소는 태그가 다른 다수의 이미지를 가질 수 있다.

- 편의상 docker.io를 생략하더라도 기본 레지스트리 서버로 사용한다- 하나의 이미지 저장소는 태그가 다른 다수의 이미지를 가질 수 있다.

- 편의상 docker.io를 생략하더라도 기본 레지스트리 서버로 사용한다..

- 도커 허브에 이비지를 올릴 때 퍼블릭 도커 이미지는 무료로 제공되며, 프라이빗 이미지를 사용하는 경우 비용 발생

```
docker login
```

- 서버를 지정할 수 있다. 지정하지 않으면 도커 허브에 로그인

```
docker tag nacyot/moniwiki:latest rewls/moniwiki:latest
```

- 이름 변경

```
docker push rewls/moniwiki:latest
```

- 이름 규칙만 맞으면 푸시 작업 과정에서 이미지 저장소를 생성해준다.

### 다른 서버에서 도커로 모니위키 컨테이너 실행

```
curl -s https://get.docker.com | sudo sh
```

- 도커 설치

```
docker run -d -p 9999:80 <DOCKER_HUB_ID>/moniwiki:latest
```

- push한 이미지로 컨테이너 실행
