---
layout: default
title: Dealing with files
parent: Web
grand_parent: Study
nav_order: 6
mathjax: true
mermaid: true
permalink: /docs/web/6
---

# Dealing with files
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

> 참고: [Dealing with files](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/Dealing_with_files)

- When you're building a website, you need to assemble these files into a sensible structure on your local computer, make sure they can talk to one another, and get all your content looking right before you eventually upload them to a server

## Where should your website live on your computer?

- When you are working on a website locally on your computer, you should keep all the related files in a single folder that mirrors the published website's file structure on the server

## An aside on casing and spacing

- You'll notice that throughout this article, we ask you to name folders and files completely in lowercase with no spaces

### Because

1. Many computers, particularly webservers, are case-sensitive.

2. Browsers, web servers, and programming languages do not handle spaces consistently

	- It's better to separate words with hyphens

	- The Google search engine treats a hyphen as a word separator but does not regard an underscore that way

## What structure should your website have?

1. `index.html`: This file will generally contain your homepage content

2. `images` folder: This folder will contain all the images that you use on your site

3. `styles` folder: This folder will contain the CSS code used to style you content

4. `scripts` folder: This folder will contain all the JavaScript code used to add interactie functionality to your site
