---
layout: default
title: Week 2-2 WebGoat Without Password
parent: Wargame
grand_parent: Study
nav_order: 1
mathjax: true
mermaid: true
permalink: /docs/wargame/week2-2
---

# Week 2-2 WebGoat Without Password
{: .no_toc }

<details markdown="block">
  <summary>
	Table of contents
  </summary>
{: .fs-3 .text-delta }
- TOC
{:toc}
</details>

---

### WebGoat 접속 방법

1. 자바가 설치된 환경

2. WebGoat `.jar` 파일 다운로드

	> [WebGoat releases](https://github.com/WebGoat/WebGoat/releases)

3. `.jar` 파일 실행

	```shell
	java -jar <파일경로>
	```
4. http://\<ip주소\>:\<포트번호>/WebGoat 접속

## Without Password

### Description

Can you login as Larry?

## Solving

### 관찰

<center markdown="block">
![main-page](/assets/wargame/images/2-2-main-page.png)

Main page
</center>

### Step 1

- Username: Larry, Password: ' OR '1' = '1

```
Congratulations, you solved the challenge. Here is your flag: ...
```

<center markdown="block">
![solve](/assets/wargame/images/2-2-solve.png)

Solve page
</center>
