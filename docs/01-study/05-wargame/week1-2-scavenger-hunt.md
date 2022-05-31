---
layout: default
title: Week 1-2 Scavenger Hunt
parent: Wargame
grand_parent: Study
nav_order: 1
mathjax: true
mermaid: true
permalink: /docs/wargame/week1-2
---

# Week 1-2 Scavenger Hunt
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

> [Scavenger Hunt](https://play.picoctf.org/practice/challenge/161?category=1&page=1&search=)

<center markdown="block">
![1-2](/assets/wargame/1-2.png)
</center>

## Scavenger Hunt(폐품 수집)

- Tags: `Category: Web Exploitation`

### Description

- There is some interesting information hidden around this site [http://mercury.picoctf.net:39698/](http://mercury.picoctf.net:39698/). Can you find it?

### Hint

1. You should have enough hints to find the files, don't run a brute forcer.

## Solving

### 관찰

<center markdown="block">
![main-page](/assets/wargame/1-2-main-page.png)

Main page
</center>

##### How 클릭

- Response page

	<center markdown="block">
	![how-response-page](/assets/wargame/1-2-how-response-page.png)

	Response page
	</center>

##### What 클릭

- Response page

	<center markdown="block">
	![what-response-page](/assets/wargame/1-2-what-response-page.png)

	Response page
	</center>

### 아이디어1

- What tab의 내용에 있는 HTML, CSS, JS 파일을 본다.

### 실행1

##### HTML

```html
<!--Here's the first part of the flag: ...-->
```

##### CSS

```css
/* CSS makes the page look nice, and yes, it also has part of the flag. Here's part 2: ... */
```

##### JS

```javascript
/* How can I keep Google from indexing my website? */
```

### 아이디어2

- 플래그를 얻는 것이 목적이므로 아래 방법 중 정보가 들어 있을 수 있는 `robots.txt`를 살펴본다.

##### 구글이 특정 웹 페이지를 indexing하지 못하도록 하는 방법

> [How to prevent google from indexing certin web pages](https://www.ilfusion.com/how-to-prevent-google-from-indexing-certain-web-pages)

1. `noindex` 메타 태그

	- `<head>`에 아래 메타 태그 삽입

		```html
		<meta name="robots" content="noindex">
		```

2. `X-Robots-Tag` HTTP response header

	- `X-Robots-Tag: noindex`

3. `robots.txt`

	- [Create a robots.txt file](https://developers.google.com/search/docs/advanced/robots/create-robots-txt?hl=en&visit_id=637895822363783848-1731081026&rd=1)

### 실행2

- `robots.txt`는 루트에 위치하므로 [http://mercury.picoctf.net:39698/robots.txt](http://mercury.picoctf.net:39698/robots.txt)에 접속한다.

	```
	User-agent: *
	Disallow: /index.html
	# Part 3: ...
	# I think this is an apache server... can you Access the next flag?
	```

### 아이디어3

- 아파치 서버만의 어떤 파일이 있을 것 같다.

- [Apache 2.4 docs](https://httpd.apache.org/docs/2.4/)

- 목차에 `.htaccess` 파일이 보인다.

### 실행3

- [http://mercury.picoctf.net:39698/.htaccess](http://mercury.picoctf.net:39698/.htaccess) 접속

	```
	# Part 4: ...
	# I love making websites on my Mac, I can Store a lot of information there.
	```

### 아이디어4

- Store의 앞 알파벳이 대문자인 것을 보면 Mac에는 저장 관련해서 어떤 파일이 있는 것 같다.

- google에 `mac store file`을 검색해보니 `DS_Store` 파일이 있다.

### 실행4

- [http://mercury.picoctf.net:39698/.DS_Store](http://mercury.picoctf.net:39698/.DS_Store) 접속

	```
	Congrats! You completed the scavenger hunt. Part 5: ...}
	```
