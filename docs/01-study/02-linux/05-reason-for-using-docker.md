---
layout: default
title: Reason for Using Docker
parent: Linux
grand_parent: Study
nav_order: 5
mathjax: true
permalink: /docs/linux/reason-docker
---

# 도커를 사용하는 이유
{: .no_toc }

> [참고](https://www.44bits.io/ko/post/why-should-i-use-docker-container)

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


## 눈송이 서버들(Snowflake Servers)

- 서로 모양이 다른 서버들이 존재하는 상황을 눈송이 서버라고 한다.

- 이런 상황을 개선하고자 서버의 운영 기록을 코드화

```
도커 파일 = 서버 운영 기록 코드화
도커 이미지 = 도커 파일 + 실행 시점
```

## 테스트 주도 개발의 관점에서 도커파일 바라보기

테스트 주도 개발$^{\text{Test Driven Development}}$ 방식과 비슷하게 빌드할 수 있다.

1. 도커 파일을 만들고
2. 도커 이미지 만들기에 실패하고,
3. 도커 파일을 작성/수정한 후,
4. 도커 이미지 만드는 데 성공한다.
5. 필요 없는 부분은 지우고 합칠 수 있는 명령은 합친다.(=효율화)
6. 1번으로 돌아간다.

- 서버를 만들 때 미리 실패해보는 일은 상당히 중요하다. 서비스 장애로 이어지기 때문

> tip. 기반 이미지로 컨테이너를 하나 실행한 다음 거기서 원하는 명령어들을 입력하고 원하는 경과가 나왔을 때 해당 명령어를 도커 파일로 옮기는 식으로 작업하면 실패 -> 수정 과정을 훨씬 더 빨리 반복할 수 있다.

```
docker run -d my-container
```

- 도커 이미지로 서버를 실행하면 도커 컨테이너가 만들어진다.

```
도커 파일 = 서버 운영 기록 코드화
도커 이미지 = 도커 파일 + 실행 시점
도커 컨테이너 = 도커 이미지 + 환경 변수
```

## 클래스와 인스턴스처럼 도커 이미지 바라보기

- 도커 덕분에 서버를 설치하고 운영 기록을 별도로 관리하는 고단함 없이, 잘 만들어진 서버를 사용할 수 있다.(도커 허브$^{\text{Docker Hub}}$에 다른 사람들이 만들어둔 도커 이미지들이 있다.)

- 한 도커 이미지로 생성할 수 있는 컨테이너 개수에는 제한이 없다.

## 서버 코드화의 장점

1. 서버 제작 과정에 견고함과 유연성을 더할 뿐 아니라
2. 다른 이가 만든 서버를 소프트웨어 사용하듯 가져다 쓸 수 있고
3. 여러 대에 배포할 수 있는 확장성이 있다.

