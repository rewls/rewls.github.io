---
layout: default
title: How do you set up a local testing server?
parent: Web
grand_parent: Study
nav_order: 5
mathjax: true
mermaid: true
permalink: /docs/web/05
---

# How do you set up a local testing server?
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

> 참고: [How do you set up a local testing server?](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/set_up_a_local_testing_server)

- Objective: You will learn how to set up a local testing server

## Local files vs. remote fils

- You can open your examples in a browser

- If the web address path starts with `file://` followed by the path to the file on your local hard drive, a local file is being used

- In contrast if you view one of our examples hosted on GitHub (or an example on some other remote server), the web address will statr with `http://` or `https://`, to show that the file has been received via HTTP

## the problem with testing local files

- Some examples won't run if you open them as local files

### Reasons the most likely being

##### They feature asynchronous requests.

- Some browsers(including Chrome) will not run async requests if you just run the example from a local file

- This because of security restrictions

##### They feature a server-side language

- Server-side languages (such as PHP or Python) require a special server to interpret the code and deliver the results

##### They include other files

- Browsers commonly treat requests to load resources using the `file://` schema as cross-origin requests

- So if you load a local file that includes other local files, this may trigger a CORS error

## Running a simple local HTTP server

- To get around the problem of async requests, we need to test such examples by running them through a local web server

- One of the easiest ways to do this for our purposes is to use Python's `http.server` module

> Note
>
> Python 3 기준

1. Install Python

```shell
sudo pacman -S python
```

```shell
python -V
```

2. Navigate to the directory that your example is inside

3. Enter the command to start up the server in that directory

```shell
python -m http.server
```

4. By default, this will run the contents of the directory on a local web server, on port 8000

	- You can go to this server by going to the URL `localhost:8000` in your web browser

	- Here you'll see the contents of the directory listed - click the HTML file you want to run

> Note
>
> You can choose another port by running the server command followed by an alternative port number, e.g. `python -m http.server 7800`

## Running server-side languages locally

- Python's `http.server` module is merely a sstatic file server; it doesn't know how to run code written in languages such as Python, PHP or JavaScript

### Few examples

- To run Python server-side code, you'll need to use a Python web framework. (Django, Flask, Pyramid)

- To run Node.js (JavaScript) server-side code, your'll need to use raw node or a framework built on top of it (Express

- To run PHP server-side fode, launch PHP's built-in development server

	```shell
	php -S localhost:8000
	```

