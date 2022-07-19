---
layout: default
title: What's in the head? Metadata in HTML
parent: HTML
grand_parent: Study
nav_order: 2
mathjax: true
mermaid: true
permalink: /docs/web/2
---

# What's in the head? Metadata in HTML
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

> 참고: [What's in the head? Metadata in HTML](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/The_head_metadata_in_HTML)

- The head of an HTML document is the part that is not displayed in the web browser when the page is loaded

- It contains information such as the page `<title>`, links to CS, links to custom favicons, and other metadata

- Web browsers use information contained in the head to render the HTML document correctly

- Objective: To learn about the HTML head, its purpose, the most important items it can contain, and what effect it can have on the HTML document

## What is the HTML head?

- The HTML head is the contents of the `<head>` element

- Unlike the contents of the `<body>` element, the head's content is not displayed on the page

- Instead, the haed's job is to contain metadata about the document

## Adding a title

- `<title>` element can be used to add a title to the document

- `<h1>` element appears on the page when loaded in the browser $---$ generally this should be used once per page, to mark up the title of your page content

- `<title>` element is metadata that represents the title of the overall THTML document (not the dcument's content)

## Metadata: the `<meta>` element

- Metadata is data that describes data, and HTML has an official way of adding metadata to a document $---$ the `<meta>` element.

### Specifying your document's character encoding

```html
<meta charset="utf-8">
```

- This element specifies the document's character encoding $---$ the character set that the document is permitted to use

### Adding an author and description

- Many `<meta>` elements include `name` and `content` attributes

- `name` specifies the type of meta elements it is; what type of information it contains

- `content` specifies the actual meta content

- Two such meta elements that are useful to include on your page define the author of the page, and provide a concise description of the page

```html
<meta name="author" content="Chris Mills">
<meta name="description" content="The MDN Web Docs Learning Area aims to provide complete beginners to the Web with all they need to know to get started with developing web sites and applications.">
```

- Specifying a description that includes keywords relating to the content of your page is useful as it has the potential to make your page appear higher in relevant searches performed in search engines (such activities are termed Search Engine Optimization, or SEO)

> Note
>
> In Google, you will see some relevant subpages listed below the main homepage link $---$ these are called sitelinks, and are configurable in Google's webmaster tools $---$ a way to make your site's search results better in the Google search engine

> Note
>
> Many `<meta> features just aren't used any more $---$ which is supposed to provide keywords for search engines to determine relevance of that page for different search terms $---$ is ignored by search engines, because spammers were just filling the keyword list with hundreds of keywords, biasing results

### Other types of metadata

- For example, Open Graph Data is a metadata protocol that Facebook invented to provide richer metadata for websites

- In the MDN Web Docs sourcecode, you'll find this

```html
<meta property="og:image" content="https://developer.mozilla.org/static/img/opengraph-logo.png">
<meta property="og:description" content="The Mozilla Developer Network (MDN) provides
information about Open Web technologies including HTML, CSS, and APIs for both Web sites
and HTML5 Apps. It also documents Mozilla products, like Firefox OS.">
<meta property="og:title" content="Mozilla Developer Network">
```

- One effect of this is that when you link to MDN Web Docs on Facebook, the link appears along with an image and description

- Twitter also has its own similar proprietary metadata called Twitter Cards, which has a similar effect when the site's URL is displayed on twitter.com

```html
<meta name="twitter:title" content="Mozilla Developer Network">
```

## Adding custom icons to your site

- You can add references to custom icons in your metadata, and these will be displayed in certain contexts

- The most commonly used of these is the favicon (short for "favorites icon", referring to its use in the "favorites" or "bookmarks" lists in browsers)

- It is the first icon of this type: a 16-pixel square icon used in multiple places

- You may see depending on the browser)

- favicons displayed in the browser tab containing each open page, and next to bookmarked pages in the bookmarkes panel

## Adding favicon

1. Saving it in the same directory as the site's index page, saved in `.ico` format

2. Adding the following line into your HTML's `<head>` block to reference it

```html
<link rel="icon" href="favicon.ico" type="image/x-icon">
```

- There are lots of other icon types to consider these days as well

- For example, you'll find this in the source code of the MDN Web Docs homepage

```html
<!-- third-generation iPad with high-resolution Retina display: -->
<link rel="apple-touch-icon-precomposed" sizes="144x144" href="https://developer.mozilla.org/static/img/favicon144.png">
<!-- iPhone with high-resolution Retina display: -->
<link rel="apple-touch-icon-precomposed" sizes="114x114" href="https://developer.mozilla.org/static/img/favicon114.png">
<!-- first- and second-generation iPad: -->
<link rel="apple-touch-icon-precomposed" sizes="72x72" href="https://developer.mozilla.org/static/img/favicon72.png">
<!-- non-Retina iPhone, iPod Touch, and Android 2.1+ devices: -->
<link rel="apple-touch-icon-precomposed" href="https://developer.mozilla.org/static/img/favicon57.png">
<!-- basic favicon -->
<link rel="icon" href="https://developer.mozilla.org/static/img/favicon32.png">
```

> Note
>
> If your site uses a Content Security Policy (CSP) to enhance its security, the policy applies to the favicon. If you encounter problems with the favicon not loading, verify that the `Content-Security-Policy` header's `img-src` directive is not preventing access to it

## Applying CSS and JavaScript to HTML

- The `<link>` element should alwyas go inside the head of your document. This takes two attributes, `rel="stylesheet"`, which indicates that it is the document's stylesheet, and `href`, which contains the path to the stylesheet file

```html
<link rel="stylesheet" href="my-css-file.css">
```

- The `<script>` element should also go into the head, and should include a `src` attributes containing the path to the JavaScript you want to load, and `defer`, which basically instructs the browser to load the JavaScript after the page has finished parsing the HTML

	- This is useful as it makes sure that the HTML is all loaded before the JavaScript runs so that you don't get errors resulting from JavaScript trying to access an HTML element that doesn't exist on the page yet

```html
<script src="my-js-file.js" defer>
</script>
```

> Note
>
> `<script>` element may look like an empty element, but it's not, and so needs a closing tag. Instead of pointing to an external script file, you can also choose to put your script inside the `<script>` element

## Wetting the primary language of the document

- Finally, it's worth mentioning that you can (and really should` set the language of your page

- this can be done by adding the `lang` attribute to the opening HTML tag

```html
<html lang="en-US">
```

- This is useful in many ways Your HTML document will be indexed more effectively by search engines if its language is set (allowing it to appear correctly in language-specific results, for example), and it is useful to people with visual impairments using screen readers (for example, the word "six" exists in both French and English, but is pronounced differently

- You can also set subsections of your document to be recognized as different languages

```html
<p>Japanese example: <span lang="ja">ご飯が熱い。</span>.</p>
```

- You can find more about them in [Language tags in HTML and XML](https://www.w3.org/International/articles/language-tags/)
