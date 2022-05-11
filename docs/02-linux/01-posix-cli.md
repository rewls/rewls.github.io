---
layout: default
title: POSIX-CLI1
parent: Linux
nav_order: 1
---

# POSIX CLI1
{: .no_toc }

> [강의](https://opentutorials.org/module/3747)

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

- CLI(Command Line Interface)

- POSIX(Portable Operating System Interface)

	- Unix 계열 표준

### 수업의 목적

|        | File            | Directory |
|--------|-----------------|-----------|
| Create | editor          | mkdir     |
| Read   | editor, cat, ls | ls        |
| Update | editor, mv      | mv        |
| Delete | rm              | rm        |

- 표에 있는 명령어 익히기

### 디렉토리의 사용

| Command | Description             |
|---------|-------------------------|
| `pwd`   | print working directory |
| `/`     | root directory          |
| `~`     | home directory          |
| `cd`    | change directory        |

### 현재 디렉토리의 상태보기와 명령어의 형식

| Command       | Description        |
|---------------|--------------------|
| `--help`      | simple manual      |
| `man command` | manual             |
| `ls`          | list               |
|               | `-l` : long format |
|               | `-a` : all files   |
| `touch`       | make empty file    |
| `.filename`   | hidden file        |

### 디렉토리의 생로병사

| Command | Description                        |
|---------|------------------------------------|
| `mkdir` | make directory                     |
| `./`    | curent directory                   |
| `mv`    | move(rename)                       |
| `rm`    | remove                             |
|         | `-r` : recursive, directory remove |

### 절대경로 VS 상대경로

- relative path vs absolute path

| Command | Description      |
|---------|------------------|
| `../`   | parent directory |

### 파일생성과 읽기

| Command | Description |
|---------|-------------|
| `vi`    | text editor |

| `cat` | print contents|

### 순서대로 실행하기

| Command | Description                              |
|---------|------------------------------------------|
| `ls -R` | recursive, 하위 디렉토리 파일까지 보여줌 |
| `;`     | command seperator                        |

### 자동화-실패하면 멈추기

| Command | Description  |
|---------|--------------|
| `&&`    | and operater |

### 수업을 마치며

##### 후속공부

- shell script : 자동화

- package manager

	- `apt-get`, `yum`

- for maintain, computer architecture

	- `htop`

- Network
