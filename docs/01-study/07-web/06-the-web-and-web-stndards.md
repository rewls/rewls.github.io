---
layout: default
title: The web and web standards
parent: Web
grand_parent: Study
nav_order: 6
mathjax: true
mermaid: true
permalink: /docs/web/6
---

# The web and web standards
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

## Brief history of the web

### In the late 1960s

- The US military developed a communication network called ARPANET

- This can be considered a forerunner of the Web, as it worked on packet switching, and featured the first implementation of the TCP/IP protocol suite

- These two technologies form the basis of the infrastructure that the internet is built on

### In 1980

- Tim Berners-Lee (often referred to as TimBL) wrote a notebook program called ENQUIRE, which featured the concept of links between different nodes

### In 1989

- TimBL wrote information Management: A Proposal and HyperText at CERN; these two publications together provided the background for how the web would work

- They received a fair amount of interest, enough to convince TimBL's bosses to allow him to go ahead and create a global hyptertext system

### By late 1990

- TimBL had created all the things needed to run the first version of the web $---$ HTTP, HTML, the first web browser, which was called WorldWideWeb, an HTTP server, and some web pages to look at

### In the next few yours that followed

- The web exploded, with multiple browsers being released, thousands of web servers being set up, and milions of web pages being created.

### In 1994

- One last significant data point to share is TimBL founded the World Wide Web Consortium (W3C), an organization that brings together representatives from many different technology companies to work together on the creation of web technology specifications

- After that other technologies followed such as CSS and JavaScript, and the web started to look more like the web we know today

---

## Web standards

- Web standards are the technologies we use to build web sites

- These standards exist as long technical documents called specifications, which detail exactly how the technology should work

- These documents are not very useful for learning how to use the technologies they desciribe, but instead are intended to be used by software engineers to implement these technologies (usually in web browsers)

- For example, the [HTML Living Standard](https://html.spec.whatwg.org/multipage/) describes exactly how HTML (all the HTML elements, and their associated APIs, and other surrounding technologies) should be implemented

- Web standards are created by standards bodies $---$ institutions that invite groups of people from different technology companies to come together and agree on how the technologies should work in the best way to fulfill all of their use cases

- Web standards bodies: W3C, WHATWG (who maintain the living standards for the HTML language), ECMA (who publish the standart for ECMAScript, which JavaScript is based on), Khronos (who publish technologies for 3D graphics, such as WebGL), and others

### Open standards

- One of the key aspects of web standards, which TimBL and the W3C agreed on from the start, is that the web (and web technologies) should be free to both contribute and use, and not encumbered by patents/licensing

- This allows the web to remain a freely-available public resource

### Don't break the web

- The idea is that any new web technology that is introduced should be backwards compatible with what went before it, and forwards compatible

---

## Overview of modern web technologies

### Browsers

- Web browsers are the software programs people use to consume the web, and include Firefox, Chrome, ...

### HTTP

- Hypertext Transfer Protocol, or HTTP, is a messaging protocol that allows web browsers to ommunicate with web servers (where web sites are stored)

### HTML, CSS, and JavaScript

- HTML, CSS, and JavaScript are the main three technologies you'll use to build a website

##### HTML

- Hypertext markup language, or HTML, is a markup language consisting of different elements you can wrap (mark up) content in to given it meaning (semantics) and structure

- Simple HTML looks like this

```html
<h1>This is a top-level heading</h1>

<p>This is a paragraph of text.</p>

<img src="cat.jpg" alt="A picture of my cat">
```

##### CSS

- Cascading Style Sheets (CSS) is a rule-based language used to apply styles to your HTML

- As a simple example, the following code would turn our HTML paragraph red

```css
p {
  color: red;
}
```

##### JavaScript

- JavaScript is the programming language we use to add interactivity to web sites, from dynamic style switching, to fetching updates from the server, right through to complex 3D graphics

- The following simple JavaScript will store a reference to our paragraph in memory and change the text inside it:

```javascript
let pElem = document.querySelector('p');
pElem.textContent = 'We changed the text!';
```

### Tooling

- The developer tools inside modern browsers that can be used to debug your code

- Testing tools that can be used to run tests to show whether your code is behaving as you intended it to

- Libraries and frameworks built on top of JavaScript that allow you to build certain types of web site much more quickly and effectively

- So-called Linters, which take a set of rules, look at your code, and highlight places where you haven't followed the rules properly

- Minifiers, which remove all the whitespace from your code files to make it so that they are smaller and therefore download from the server more quickly

### Server-side languages and frameworks

- HTML, CSS, and JavaScript are front-end (or client-side) languages, which means they are run by the browser to produce a website front-end that your users can use

- There are another class of languages called back-end (or server-side) languages, meaning that they are run on the server before the result is then sent to the browser to be displayed

- A typical use for a server-side language is to get some data out of a database and generate some HTML to contain the data, before then sending the HTML over to the browser to display it to ther user

- Example server-side language: ASP.NET, Python, PHP, and NodeJS

---

## Web best practices

- We are trying to make the web work for all, as mush as possible

### Cross-browser compatiblity

- The practice of trying to make sure your webpage works across as many devices as possible.

- This includes using technologies that all the browsers support, delivering better experiences to browsers that can hendle them (progressive enhancement), and/or writing code so that it falls back to a simpler but still usable experience in older browsers (graceful degradation)

- It also involves a lot of testing to see if anything fails in certain browsers, and then more work to fix those failures

### Responsive web design

- The practice of making your functionality and layouts flexible so they can automatically adapt to different browsers

### Performance

- Getting web sites to load as quickly as possible, but also making them intuitive and easy to use so that users don't get frustrated and go somewhere else

### Accessibility

- Making your websites usable by as many different kinds of people as possible (related concepts are diversity and inclusion, and inclusive design)

- This includes people with visaul impairments, hearing impairments, cognitive disabilities, or physical disabilities.

- It also goes beyond people with disabilities $---$ how about young or old people, people from different cultures, people using mobile devices, or people with unreliable or slow network connections?

### Internationalization

- Making websites usable by people from different cultures, who speak different languages to your own

### Privacy & Security

- Privacy refers to allowing people to go about their business privately and not spying on them or collecting more of their data than you absolutely need to

- Security refers to constructing your website in a secure way so that malicious users cannot steal information contained on it from you or your users
