---
layout: default
title: Week 3-1 webhacking.kr Challenge 38
parent: Wargame
grand_parent: Study
nav_order: 1
mathjax: true
mermaid: true
permalink: /docs/wargame/week3-1
---

# Week 3-1 webhacking.kr Challenge 38
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

## Challenge 38

> [Challenge 38](https://webhacking.kr/challenge/bonus-9/index.php)

### Description

- Log injection

## Solving

### 관찰

<center markdown="block">
![main-page](/assets/wargame/images/3-1-main-page.png)

Main page
</center>

##### asdf 입력

<center markdown="block">
![main-page](/assets/wargame/images/3-1-main-page.png)

Response page
</center>

##### 소스

```html
<html>
<head>
<title>Challenge 38</title>
</head>
<body>
<h1>LOG INJECTION</h1>
<form method=post action=index.php>
<input type=text name=id size=20>
<input type=submit value='Login'>
</form>
<!-- <a href=admin.php>admin page</a> -->
</body>
</html>
```

##### admin page 접속

- https://webhacking.kr/challenge/bonus-9/admin.php

<center markdown="block">
![main-page](/assets/wargame/images/3-1-admin-page.png)

Admin page
</center>

- log 형식: `<ip주소>:이름`

### 아이디어1

- log에 <ip주소>:admin을 찍으면 되는 듯하다.

##### admin 입력

<center markdown="block">
![main-page](/assets/wargame/images/3-1-input-admin.png)

Response page
</center>

- log에는 아무것도 찍히지 않는다.

### 아이디어2

- guest<개행><ip주소>:admin으로 우회해보자

##### 개행문자 입력

- %0d, \<br\>, \n 모두 먹히지 않는다.

### 아이디어3

- html php 입력 개행으로 서치하다 여러줄을 입력받을 수 있는 html textarea 태그를 발견했다.

##### textarea 태그 적용

- input $\rightarrow$ textarea

<center markdown="block">
![textarea](/assets/wargame/images/3-1-textarea.png)

Response page
</center>

- 입력

	```
	guest
	<ip주소>:admin
	```

<center markdown="block">
![textarea](/assets/wargame/images/3-1-solve.png)

Solve
</center>
