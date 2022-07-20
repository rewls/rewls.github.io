---
layout: default
title: From object to iframe - other embedding technologies
parent: HTML
grand_parent: Study
nav_order: 10
mathjax: true
mermaid: true
permalink: /docs/html/10
---

# From object to iframe - other embedding technologies
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

> 참고: [From object to iframe - other embedding technologies](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Other_embedding_technologies)

- To learn how to embed items into web pages using `<object>`, `<embed>`, and `<iframe>`, like PDF documents and other webpages

## A short history of embedding

##### A long time ago on the Web

- It was popular to use frames to create websites $---$ small parts of a website stored in individual HTML pages

- These were embedded in a master document called a frameset, which allowed you to specify the area on the screen that each frame filled, rather like sizing the columns and rows of a table

- These were considered the height of coolness in the mid to late 90s, and there was evidence that having a webpage split up into smaller chunks like this was better for download speeds $---$ exspecially noticeable with network connections being so slow back then

- They did however have many problems, which far outweighted any positives as network speeds got faster, so you don't see them being used anymore

##### A little while later (late 90s, early 2000s)

- Plugin technologies became very popular, such as Java Applets and Flash $---$ these allowed web developers to embed rich content into webpages

- Embedding these technologies was achieved through elements like `<object>`, and the lesser-used `<embed>`, and they were very useful at the time

- They have since fallen out of fashion due to many problems, including accessibility, wecurity, file size, and more

##### Finally

- the `<iframe>` element appeared (along with other ways of embedding content, such as `<canvas>`, `<video>`, etc)

- This provides a way to embed an entire web document inside another one, as if it were an `<img>` or other such element, and is used regularly today

### Active learning: classic embedding uses

##### Youtube

- Let's look at how YouTube allows us to embed a video in any page we like using a `<iframe>`

1. First, go to YouTube and find a video you like

2. Below the video, you',, find a Share button $---$ select this to display the sharing oprions

3. Select the Embed button and you'll be given some `<iframe>` code $---$ copy this

4. Insert it into the your page

##### Google map

- You could also try embedding a Google Map

1. Go to Google Maps and find a map you like

2. Click on the "Hamburger Menu" (three horizontal lines) in the top left of the UI

3. Select the Share or embed map option

4. Select the Embed map option which will give you some `<iframe>` code $---$ copy this

5. Insert it into the your page

### iframes in detail

- `<iframe>` elements are designed to allow you to embed other web documents into the current document

- This is great for incorporating third-party content into your website that you might not have direct control over and don't want to have to implement your own version of

- There are some serious Security concerns to consider with `<iframe>`s, but this doesn't mean that you shouldn't use them in your websites

```html
<head>
  <style> iframe { border: none } </style>
</head>
<body>
  <iframe src="https://developer.mozilla.org/en-US/docs/Glossary"
          width="100%" height="500" allowfullscreen sandbox>
    <p>
      <a href="/en-US/docs/Glossary">
         Fallback link for browsers that don't support iframes
      </a>
    </p>
  </iframe>
</body>
```

- This example includes the basic essential needed to use an `<iframe>`

##### `vorder: none`

- If used, the `<iframe>` is displayed without a surrounding border

- Otherwise, by default, browsers display the `<iframe>` with a surrounding border

##### `allowfullscreen`

- If set, the `<iframe>` is able to be placed in fullscreen mode using the Fullscreen API

##### `src`

- This attribute contains a path pointing to the URL of the document to be embedded

##### `width` and `height`

- These attributes specify the width and height you want the iframe to be

##### Fallback content

- You can include fallback content between the opening and closing `<iframe></iframe>` tags that will appear if the browser doesn't support the `<iframe>`

##### `sandbox`

- This attributes, which works in slightly more modern browsers than the rest of the `<iframe>` features requests heightened security settings

> Note
>
> In order to improve speed, it's a good idea to set the iframe's `src` attribute with JavaScript after the main content is done with loading. This makes your page usable sooner and decreases your official page load time (an important SEO metric)

### Security concerns

- There is no need to be scared and not use `<iframe>`s $---$ you just need to be careful

- Browser makers and Web developers have learned the hard way that iframes are a comman target (official term: attck vector) for bad people on the Web (often termed hackers, or more accurately, crackers) to attack if they are trying to maliciously modify your webpage, or trick people into doing something they don't want to do

- Because of this, spec engineers and browser developers have developed various security mechanisms for making `<iframe`s more secure, and there are also best practives to consider

> Note
>
> Clickjacking is one kind of common iframe attack where hackers embed an invisible iframe into your document (for embed your document into their own malicious website) and use it to capture users' interactions. This is a common way to mislead users or steal sensitive data

- A quick example first though $---$ try loading the previous example we showed above into your browser $---$ you can

- You'll probably see some kind of message to the effect of "I can't open this page", and if you look at the Console in the browser developer tools, you'll see a message telling you why

- In Firefox

```
The loading of “https://developer.mozilla.org/en-US/docs/Glossary” in a frame is denied by “X-Frame-Options“ directive set to “DENY“.
```

- This is because the developers that built MDN have included a setting on the server that serves the website pages to disallow them from being emgedded inside `<iframe>`s

##### Only embed when necessary

- You can save yourself a lot of headaches if you only embed third-party content when completely necessary

- A good rule for web security is "You can never be too cautious. If you made it, double-check it anyway. If someone else made it, assume it's dangerous until proven otherwise

- Besides security, you should also be aware of intellectual property issues

- If the content is licensed, you must obey the license terms

##### Use HTTPS

- HTTPS is the encrypted version of HTTP

- You should serve your websites using HTTPS whenever possible

	1. HTTPS reduces the chance that remote content has been tampered with in transit

	2. HTTPS prevents embedded content from accessing content in your paren document, and vice versa

- HTTPS-enabling your site requires a special security certificate to be installed

- Many hosting providers offer HTTPS-enabled hosting without you needing to do any setup on your own to pur a certificate in place

- But if you do need to set up HTTPS support for your site on your own, Let's Encrypt provides tools and insturctions you can use for automatically creating and installing the necessary certificate $---$ with built-in support for the most widely-used web servers, including the Apache web server, Nginx, and others.

- The Let's Encrypt tooling is designed to make the process as easy as possible

##### Always use the `sandbox` attribute

- You want to give attackers as little power as you can to do bad things on your website, therefore you should give embedded content only the permissions needed for doing its job

- A container for code where it can be used appropriately but can't cause any harm to the rest of the codebase is called a sandbox

- Unsandboxed content can do way too much (executing JavaScript, submitting forms, popup windows, etc)

- By default, you should impose all available restrictions by using the `sandbox` attribute with no parameters

- If absolutely required, you can add permissions back one by one (inside the `sandbox=""` attribute value) $---$ see the [sandbox](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe#attr-sandbox)

- One important note is that you should never add both `allow-scripts` and `allow-same`origin` to your sandbox` attribute $---$ in that case, the embedded content could bypass the Same-origin policy that Same-origin policy that stops sites from executing scripts,and use JavaScript to turn off sandboxing altogether

> Note
>
> Sandboxing provides no protection if attackers can fool people into visiting malicious content directly (outside an `iframe`). If there's any chance that certain content may be malicious (e.g., user-generated content), please serve it from a different domain to your main site

##### Configure CSP directives

- CSP stands for content security policy and provides a set of HTTP Headers (metadata sent along with your web pages when they are served from a web server) designed to improve the security of your HTML document

- When it comes to securing `<iframe>`s, you can configure your server to send an appropriate `X-Frame-Options` header

- This can prevent other websites from embedding your content in their web pages (which would enable clickjacking and a host of other attacks)

## The `<embed>` and `<object>` elements

- The `<embed>` and `<object>` elements serve a different function to `<iframe>` $---$ these elements are general purpose embedding tools for embedding external content, such as PDFs

- If you need to display  PDFs, it's usually better to link to them, rather than embedding them in the page

- Historically these elements have also been used for embedding content handled by browser plugins such as Adobe Flash, but this technology is now obsolete and is not supported by modern browsers

- If you find yourself needing to embed plugin content, this is the kind of information you'll need, at a minimum

| |`<embed>`|`<object>`|
|-|-|-|
|URL of the embedded content|`src`|`data`|
|accurate media type of the embedded content|`type`|`type`|
|heihgt and width(in CSS pixels) of the box controlled by the plugin|`height` `width`|`height` `width`|
|names and values, to feed the plugin as parameters| ad hoc attributes with those names and values|single-tag `<param>` elements, contained within `<object>`|
|independent HTML content as fallback for an unavailable resource|not supported (`<noembed>` is obsolete)|contained within `<object>`, after `<param>` elements

- Let's look at an `<object>` example that embeds a PDF into a page

```html
<object data="mypdf.pdf" type="application/pdf"
        width="800" height="1200">
  <p>You don't have a PDF plugin, but you can
    <a href="mypdf.pdf">download the PDF file.
    </a>
  </p>
</object>
```

- PDFs were a necessary stepping stone between paper and digital, but they pose many accessibility challenges and can be hard to read on smal screens

- They do still tend to be popular in some circles, but it is much better to link to them so they can be downloaded or read on a separate page, rather than embedding them in a webpage
