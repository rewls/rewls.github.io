---
layout: default
title: Getting started with HTML
parent: HTML
grand_parent: Study
nav_order: 1
mathjax: true
mermaid: true
permalink: /docs/web/1
---

# Getting started with HTML
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

> 참고: [Getting started with HTML](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/Getting_started)

- Objective: To gain basic familarity with HTML, and practice writing a few HTML elements

## What is HTML?

- HTML (Hypertext Markup Language) is a markup language that tell web browsers how to structure the web pages you visit

- HTML consists of a series of elements, which you use to enclose, wrap, or mark up different parts of content to make it appear or act in a certain way

> Note
>
> Tags in HTML are not case-sensitive. however, it is best practice to write all tags in lowercase for consistency and readability

## Anatomy of an HTML element

```html
<p>My cat is very grumpy</p>
```

### The opening tage

- In this example, `<p>`

- This consists of the name of the element (in this example, `p` for paragraph), wrapped in opening and closing angle brackets

- This opening tag marks where the element begins or starts to take effect

##### The content

- In this example, `My cat is very grumpy`

- This is the content of the element

##### The closing tag

- In this example, `</p>`

- This is the same as the opening tag, except that it includes a forward slash befor the element name

- This marks where the element ends

##### The element

- In this example, `<p>My cat is very grumpy</p>`

- This is the opening tag, followed by content, follewed by the closing tag

### Active learning: creating your first HTML element

```html
<em>This is my text</em>
```

- `<em>`: Italic text formatting

### Nesting elements

- Elements can be placed within other elements. This is called nesting

```html
<p>My cat is <strong>very</strong> grumpy.</p>
```

- The tags have to open and close in a way that they are inside or outside one another

### Block vs. inline elements

##### Block-level elements

- These form a visibel block on a page

- A block-level element appears on a new line following the content that preceds it

- Block-level elements are usually structural elements on the page

- A block-level element wouldn't be nested inside an inline element, but it might be nested inside another block-level element

##### Inline elements

- These are contained within block-level elements, and surround only small parts of the document's content

- An inline element will not cause a new line to appear in the document

- It is typically used with text

```html
<em>first</em>
<em>second</em>
<em>third</em>

<p>fourth</p>
<p>fifth</p>
<p>sixth</p>
```

- `<em>` is an inline element

- `<p>` is a block-level element

> Note
>
> HTML5 redefine the element categories.

> Note
>
> The terms block and inline, as used in this article, should not be confused with the types of CSS boxes that have the same names. Changing the CSS display tyype doesn't change the category of the element, and doesn't affect which elements it can contain and which elements it can be contained in

### Empty elements

- Some elements consist of a sigle tag, which is typically used to inser/embed somthing in the document

```html
<img src="https://raw.githubusercontent.com/mdn/beginner-html-site/gh-pages/images/firefox-icon.png">
```

> Note
>
> Empty elements are sometimes called void elements

> Note
>
> In HTML there is no requirement to add a `/` at the end of an empty element's tag. However, it is also a valid syntax and you may do this when you want your HTML to be valid XML

## Attributes

- Elements can also have attributes

```html
<p class="editor-note">My cat is very grumpy</p>
```

- Attributes contain extra information about the element that won't appear in the content

- `class` attribute is an identifying name used to targat the element with style information

##### An attribute should have

- A space between it and the element name. (For an element with more than one attribute, the attributes should be separated by spaces too)

- The attribute name, followed by an equal sign

- An attribute value, wrapped with opening and closing quote marks

### Active learning: Adding attributes to an element

```html
<a href="https://google.com" title="google" target="_blank">google</a>
```

- `<a>`: anchor. This can make the text it encloses into a hyperlink

##### `<a>` attributes

- `href`: This attribute's value specifies the web address for the link

- `title`: This attribute specifies extra information about the link. This appers as a tooltip when a cursor hovers over the element

- `target`: This specifies the browsing context used to display the link

	- `_blank` will display the link in a new tab

### Boolean attributes

- Sometimes you will see attributes written without values. These are called Boolean attributes

- Boolean attributes can only have one value, which is generally the same as the attributes name

- For example, cosider the `disabled` attribute, which you can assign to form input elements

	- You use this to disable the form input elements so the user can't make entries

```html
<input type="text" disabled="disabled">
```

As shorthand

```html
<input type="text" disabled>

<input type="text">
```

### Omitting quotes around attribute values

- Attribute values without quotes is permitted in certain circumstances, but it can also break your markup in other circumstances

- Always include the attribute quotes

### Single or double quotes?

- This is a matter of style

- Make sure you don't mix single quotes and double quotes

- If you use one type of quote, you can include the other type of quote inside your attribute values

- To use quote marks inside other quote marks of the same type, use HTML entities

```html
<a href='https://www.example.com' title='Isn&apos;t this fun?> A link to my example.</a>
```

## Anatomy of an HTML document

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
	<title>My test page</title>
  </head>
  <body>
    <p>This is my page</p>
  </body>
</html>
```

##### `<!DOCTYPE html>`

- The doctype

- In 1991-1992, doctypes were meant to act as links to a set of rules that the HTML page had to follow to be considered good HTML

- More recently, the doctype is a historical artifact that needs to be included for everything else to work right

##### `<html></html>`

- The `<html>` element

- This element wraps all the content on the page

- It is somtimes known as the root element

##### `<head></head>`

- The `<head>` element

- This element acts as a container for everything you want to include on the HTML page, that isn't the content the page will show to viewers

- This includes keywords and a page description that would appear insearch results, CSS to style content, character set declarations, and more

##### `<meta charset="utf-8">`

- The `<meta>` element

- This element represents metadata that cannot be represented by other HTML meta-related element, like `<base>`, `<link>`, `<script>`, `<style>` or `<title>`

- The `charset` attributes sets the character set for your document to UTF-8, which includes most characters from the vast majority of human written languages

##### `<title></title>`

- The `<title>` element

- this sets the title of the page, which is the title that appears in the browser tab the page is loaded in

##### `<body></body>`

- The `<body>` element

- This contains all the content that displays on the page

### Active learning: Adding some features to an HTML document

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>My test page</title>
  </head>
  <body>
    <h1>This is my page</h1>
    <strong>bold</strong> text
  </body>
</html>
```

- `<strong>`: Bold text formatting

- `<h1>`: main title

### Whitespace in HTML

- No matter how much whitespace you use inside HTML element content, the HTML parser reduces each sequence of whitespace to a single space when rendering the code

- It can be easier to understand what is going on in your code if you have it nicely formatted

## Entity references: Including special characters in HTML

- In HTML, the characters `<`, `>`, `"`, `'` and `&` are special characters

- They are parts of the HTML syntax itself

- Character references are special codes that represent characters

- Each character reference starts with an ampersand (&), and ends with a semicolon (;)

|Literal character|Character reference equivalent|
|-|-|
|<|`&lt;`|
|>|`&gt;`|
|"|`&quot;`|
|'|`&apos;`|
|&|`&amp;`|

- To find more about entit reference, see [List of XML and HTML character entity references](https://en.wikipedia.org/wiki/List_of_XML_and_HTML_character_entity_references)(Wikipedia)

## HTML comments

- Browsers ignore comments

- The purpose of comments is to allow you to include notes in the code to explain your logic or coding

- To write an HTML comment, wrap it in the special markers `<!--` and `-->`

```html
<p>I'm not inside a comment</p>

<!-- <p>I am!</p> -->
```
