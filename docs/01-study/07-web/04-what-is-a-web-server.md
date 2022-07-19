---
layout: default
title: What is a web server?
parent: Web
grand_parent: Study
nav_order: 4
mathjax: true
mermaid: true
permalink: /docs/web/04
---

# What is a web server?
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

> 참고: [What is a web server?](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_web_server)

- Objective: You will learn what a web server is and gain a general understanding of how it works

## To review

- to fetch a webpage, your browser sends a request to the web server, which searches for the requestes file in its own storage space.

- Upon finding the file, the server reads it, processes it as-needed, and sends it to the browser

## Web server

- The term web server can refer to hardware or software, or both of them working together

### On the hardware side

- a web server is a computer that stores web server software and a website's component files

- A web server connects to the Internet and supports physical data interchange with other devices connected to the web

### On the software side

- A web server includes several parts that control how web users access hosted files

- At a minimum, this is an HTTP server

- An HTTP server is software that understands URLs (web addresses) and HTTP (the protocol your browser uses to view webpages

- An HTTP server can be accessed through the domain names of the websites it stores, and it delivers the content of these hosted websites to the end user's device

### At the most basic level

- whenever a browser needs a file that is hosted on a web server, the browser requests the file via HTTP

- When the request reaches the correct (hardware) web server, the (software) HTTP server accepts the request, finds the requested document, and sends it back to the browser, also through HTTP

- If the server doesn't find the requested document, it returns a 404 response instead

<center markdown=block>
![web-server](/assets/web/images/04-web-server.svg)
</center>

## Hosting files

- First, a web server has to store the website's files

- Technically, you could host all those files on your own computer, but it's far more convenient to store files all on a dedicated web server

- For all below resons, finding a good hosting provider is a key part of building your website

### Because

- A dedicated web server is typically more available (up and running)

- Excluding downtime and systems troubles, a dedicated web server is always connected to the Internet

- A dedicated web server can have the same IP address all the time

	- This is known as a dedicated IP address (not all ISPs provide a fixed IP address for home lines)

- A dedicated web server is typically maintained by a third-party

## Communication through HTTP

- Second, a web server provides support for HTTP(Hypertext Transfer Protocol)

- HTTP specifies how to transfer htpertext (linked web documents) between two computers

- A Protocol is a set of rules for communication between two computer.

- HTTP is a textual, stateless protocol

### Textual

- All commands are plain-text and human-readable

### Stateless

- Neither the server nor the client remember previous communications

- You need an application server for tasks like that

### HTTP

- HTTP provides clear rules for how a client and server communicate

- Usually only clients make HTTP requests, and only to servers

- Servers respond to a client's HTTP request.

- A server can also populate data into a client cache, in advance of it being requested, through a mechanism called a server push

- When requesting a file via HTTP, clients must provide the file's URL

- The web server must answer every HTTP request, at least with an error message

### HTTP server working processes

- On a web server, the HTTP server is responsible for processing and answering incoming requests

1. Upon receiving a reuest, an HTTP server first checks if the requested URL matches an existing file

2. If so, the web server sends the file content back to the browser. If not, an application server builds the necessary file

3. If neither process is possible, the tweb server returns an error message to the browser, most commonly 404 Not Found.

### Static vs. dynamic content

- To publish a website, you need either a static or a dinamic web server

### Static web server

- A static web server, or stack, consists of a computer (hardware) with an HTTP server (software)

- we call it static because the server sends its hosted files as-is to your browser

### Dynamic web server

- A dynamic web server consists of a static web server plus extra software, most commonly an application server and a database

- we call it dynamic because the application server updates the hosted files before sending content to your browser via the HTTP server

- For example, to produce the final webpages you see in the browser, the application server might fill an HTML template with content from a database.
