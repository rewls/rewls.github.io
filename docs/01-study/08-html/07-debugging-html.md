---
layout: default
title: Debugging HTML
parent: HTML
grand_parent: Study
nav_order: 7
mathjax: true
mermaid: true
permalink: /docs/html/7
---

# Debugging HTML
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

> 참고: [Debugging HTML](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/Debugging_HTML)

- Objective: Learn the basics of using debugging tools to find problems in HTML

## HTML and debugging

- HTML is not compiled into a different form before the browser parses it and shows the result (it is interpreted, not compiled)

- The way that browsers parse HTML is a lot more permissive than how programming languages are run, which is bothe a good and a bad thing

### Permissive code

- Generally when you do something wrong in code, there are two main types of error

- Syntax errors: These are spelling or punctuation errors in your code that actually cause the program no to run

- Logic errors: These are errors where the syntax is actually correct, but the code is not what you intended it to be, meaning that the program runs incorrectly

- HTML itself doesn't suffer from syntax errors because browsers parse it permissively, meaning that the page still displays even if there are syntax errors

- Browsers have built-in rules to state how to interpret incorrectly written markup, so you'll get something running, even if it is not what you expected

> Note
>
> HTML is parsed permissively because when the web was first created, it was decided that allowing people to get their content published was more important than making sure the synta was absolutely correct

### HTML validation

- The best strategy is to start by running your HTML page through the Markup Validation Service $---$ created and maintained by the W3C, the organization that looks after the speifications that define HTML, CSS, and other web technologies

- This webpage takes an HTML document as an input goes through it, and gives you a report to tell you what is wrong with your HTML

- To specify the HTML to validate, you can provide a web address, upload an HTML file, or directly input some HTML code.
