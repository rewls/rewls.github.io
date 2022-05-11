---
layout: default
title: Ch1 Getting Started
parent: Git
nav_order: 1
mermaid: true
permalink: /docs/git/ch1-getting-start
---

# Ch1 시작하기
{: .no_toc }

> [참고](https://git-scm.com/book/ko/v2/%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-%EB%B2%84%EC%A0%84-%EA%B4%80%EB%A6%AC%EB%9E%80%3F)

<details open markdown="block">
  <summary>
    Toggle
  </summary>

## Table of contents
{: .no_toc .text-delta }

- TOC
{:toc}
</details>

---

## 1.1 버전 관리란?

- 파일 변화를 시간에 따라 기록했다가 나중에 특정 시점의 버전을 다시 꺼내올 수 있는 시스템

### 분산 버전 관리 시스템(DVCS)

- Git의 클라이언트는 저장소를 히스토리와 더불어 전부 복제한다.

- 서버에 문제가 생기면 이 복제물로 다시 작업을 시작할 수 있다.

![distributed](./img/distributed.png)

---

## 1.2 Git의 목표

- 빠른 속도

- 단순한 구조

- 비선형적인 개발(수천 개의 동시 다발적인 브랜치)

- 완벽한 분산

- Linux 커널 같은 대형 프로젝트에도 유용할 것(속도나 데이터 크기 면에서)

---

## 1.3 Git 기초

### Git이 데이터를 다루는 방법

- 커밋하거나 프로젝트의 상태를 저장할 때마다 파일이 존재하는 그 순간을 중요하게 여긴다.

- Git은 데이터를 **스냅샷의 스트림**처럼 취급하고 그 크기는 아주 작다.

![snapshots](./img/snapshots.png)

### 거의 모든 명령을 로컬에서 실행

- 거의 모든 명령이 로컬 파일과 데이터만 사용하기 때문에 네트워크의 속도에 영향을 받지 않는다.

- 프로젝트의 모든 히스토리가 로컬 디스크에 있기 때문에 모든 명령이 빠르게 실행된다.

- 오프라인 상태일 때도 히스토리를 조회하고 커밋할 수 있다.

### Git의 무결성

- Git은 데이터를 저장하기 전에 항상 checksum 구하고 그 checksum으로 데이터를 관리한다.

- Git은 SHA-1 해시를 사용하여 checksum을 만든다. 만든 checksum은 40자의 16진수 문자열이다.

### Git은 데이터를 추가할 뿐

- git으로 무얼 하든 Git 데이터베이스에서 데이터를 되돌리거나 삭제할 방법은 없다.

### 세 가지 상태

- Git은 파일을 **committed, Modified, Staged** 세 가지 상태로 관리한다.

	- Committed: 데이터가 로컬 데이터 베이스에 안전하게 저장됐다는 것을 의미

	- Modified: 수정한 파일을 아직 로컬 데이터베이스에 커밋하지 않은 것을 의미

	- Staged: 현재 수정한 파일을 곧 커밋할 거라고 표시한 상태를 의미

![areas](./img/areas.png)

- Working tree는 프로젝트의 특정 버전을 Checkout한 것이다. 작업 위치에 있는 `📁.git` 안의 데이터베이스에서 파일을 가져온다.

- Staging Area는 하나의 파일이고 `📁.git`에 있다. 곧 커밋할 파일에 대한 정보를 저장한다.

- `📁.git`는 Git이 프로젝트의 메타데이터와 객체 데이터베이스를 저장하는 곳을 말한다. 저장소를 clone할 때 `📁.git`가 만들어진다.

### Basic Git workflow

1. 워킹 트리에서 파일을 수정한다.

2. Staging Area에 파일을 Stage해서 커밋할 스냅샷을 만든다. 모든 파일을 추가할 수도 있고 선택하여 추가할 수도 있다.

3. Staging Area에 있는 파일들을 커밋해서 `📁.git`에 영구적인ㅇ 스냅샷으로 저장한다.

---

## 1.4 CLI

- Git의 모든 기능을 지원하는 것은 CLI 뿐이다.

---

## 1.5 Git 설치

### Linux

각 배포판에서 사용하는 패키지 관리도구를 사용하여 설치한다.

```
git --version
```

- git 설치 확인

##### Ubuntu

```
sudo apt-get git-all
```

##### Arch

```
sudo pacman -S git
````

---

## 1.6 Git 최초 설정

### config 파일

##### `📝/etc/gitconfig`

```
git config --system
```

- 시스템의 모든 사용자와 모든 저장소에 적용되는 설정. 관리자 권한 필요.

##### `📝~/.gitconfig`, `📝~/.config/git/config`

```
git config --global
```

- 특정 사용자에게만 적용되는 설정

- 특정 사용자의 모든 저장소 설정에 적용

##### `📝.git/config`

```
git config --local(기본 옵션)
```

- `📁.git`에 있고 특정 저장소에만 적용된다.

각 설정은 역순으로 우선시 된다.

### 사용자 정보

- Git을 설치하고 나서 가장 먼저 해야 하는 것은 사용자이름과 이메일 주소를 설정하는 것이다.

- Git은 커밋할 때마다 이 정보를 사용한다. 한 번 커밋한 후에는 정보를 변경할 수 없다.

```
git config --global user.name "rewls"
git config --global user.email rew0316@gmail.com
```

- `--global` 옵션으로 설정하는 것은 딱 한 번만 하면 된다. 해당 시스템에서 해당 사용자가 사용할 때는 이 정보를 사용한다.

- 만약 프로젝트마다 다른 이름과 이메일 주소를 사용하고 싶으면 `--global` 옵션을 빼고 명령을 실행한다.

### 편집기

- Git에서 사용할 텍스트 편집기를 고른다. 기본적으로 Git은 시스템의 기본 편집기를 사용한다.

```
git config --global core.editor neovim
```

### 설정 확인

```
git config --list
```

- 설정한 모든 것을 보여준다.

- Git은 같은 키를 여러 파일에서 읽기 때문에 같은 키가 여러 개 있을 수 있다. Git은 나중 값을 사용한다.

```
git config <key>
```

- Git이 특정 Key에 대해 어떤 값을 사용하는지 확인할 수 있다.

> 노트
>
> 키에 설정된 값이 어디에서 설정되었는지 확인
> ```
> git config --show-origin <key>
> ```

---

## 1.7 도움말 보기

```
git help <verb>
man git-<verb>
```

- Git 명령을 `-h`, `--help` 옵션과 함께 사용하면 Git 명령에서 사용할 수 있는 옵션에 대한 간단한 도움말을 출력한다.
