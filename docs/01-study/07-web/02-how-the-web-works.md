---
layout: default
title: How the web works
parent: Web
grand_parent: Study
nav_order: 2
mathjax: true
mermaid: true
permalink: /docs/web/02
---

# How the web works
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

> 참고: [How the web works](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/How_the_Web_works)

## Clients and servers

- Computers connected the web are called clients and servers

<center markdown=block>
<div class=mermaid>
graph LR;
	client --requests--> server;
	server --responses--> client;
</div>
</center>

- Clients are the typical web user's internet-connected devices

- Servers are computers that store webpages, sites or apps

	- When a client device wants to access a webpage, a copy of the webpage is downloded from the server onto the client machine to be displayed in the user's web browser

## The other parts of the toolbox

### Your internet connection

- Allows you to wend and receive data on the web

### TCP/IP

- Transmission Control Protocol and Internet Protocol

- They are communication protocols that define how data should travel across the internet

### DNS

- Domain Name System

- When you type a web address in your browser, the browser looks at the DNS to find the website's IP address before it can retrieve the website

- The browser needs to find out which server the website lives on, so it can send HTTP messages to the right place

### HTTP

- Hypertext Transfer Protocol

- It is an application protocol that defines a language for clients and servers to speak to each other

### Component files

- A website is made up of many different files

- Code files: Websites are built primarily from HTML, CSS, and JavaScript

- Assets: This is a collective name for all the other stuff that makes up a website

## So what happens, exactly?

- When you type a web address into your browser

1. The browser goes to the DNS server, and finds the real address of the server that the website lives on


2. The browser wends an HTTP request message to the server, asking it to send a copy of the website to the client

	- This message, and all other data sent between the client and the server, is sent across your internet connection using TCP/IP

3. If the server approves the client's request, the server sends the client a "200 OK" message, and then starts sending the website's files to the browser as a series of small shunks called data packets

4. The browser assembles the small chunks into a complete web page and displays it to you

## Order in which component files are parsed

- When browsers send requests to servers for HTML files, those HTML files often contain `<link>` elements referencing external CSS stylesheets and `<script>` elements referencing external JavaScript scripts.

- It's important to know the order in which those files are parsed by the browser as the browser loads the page

1. The browser parses the HTML file first, and that leads to the browser recognizing any `<link>`-element references to external CSS stylesheets and any `<script>`-element references to scripts

2. As the browser parsed the HTML, it sends requests back to the server for any CSS file it has found from `<link>` elements, and any JavaScript files it has found from `<script>` elements, and from those, then parses the CSS and JavaScript

3. The browser generates an in-memory DOM tree from the parsed HTML, generates an in-memory CSSOM structure from the parsed CSS, and compiles and executes the parsed JavaScript

4. As the browser builds the DOM tree and applies the styles from the CSSOM tree and executes the JavaScript, a visual representation of the page is painted to the screen, and the user sees the page content and can begin to interact with it

## DNS explained

- Domain Name Servers

- IP address represents a unique location on the web.

- DNS was invented to make it easy to remember IP address

- These are special servers that match up a seb address you type into your browser(like google.com) to the website's real (IP) address

## Packets explained

- Basically, when data is sent across the web, it is sent in thousand of small chunks.

- There are multiple reasons why data is sent in small packets

- They are sometimes dropped or corrupted, and it's easier to replace small chunks when this happens

- The packets can be routed along different paths, making the exchange faster and allowing many different users to download the same website at the same time
