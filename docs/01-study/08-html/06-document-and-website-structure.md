---
layout: default
title: Document and website structure
parent: HTML
grand_parent: Study
nav_order: 6
mathjax: true
mermaid: true
permalink: /docs/html/6
---

# Document and website structure
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

> 참고: [Document and website structure](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/Document_and_website_structure)

- In addition to defining individual parts of your page, HTML also boasts a number of block level element used to define areas of your website (such as "the header", "the navigation menu", "the main content column")

- Objective: Learn how to structure your document using semantic tags, and how to work out the structure of a simple website

## Basic sections of a document

- Webpages all tend to share similar standard components

##### Header

- Usually a big strip across the top with a big heading, logo, and perhaps a tagline

- This usually stays the same from one webpage to another

##### Navigation bar

- Links to the site's main sections; usually represented by menu buttons, links, or tabs

- Like the header this content usually remains consistent from one webpage to another

##### Main content

- A big area in the center that contains most of the unique content of a given webpage

- you'll find som recurring elements like a secondary navigation system

##### footer

- A strip across the bottom of the page that generally contains fine print, copyright notices, or contact info

- It's a place to put common information but usually, that information is not criticall or secondary to the website itself

- The footer is also sometimes used for SEO purposes, by providing links for quick access to popular content

## HTML for structuring content

- We need to respect semantics and use the right element for the right job

##### Tags

- To implement such semantic mark up, HTML provides dedicated tags that you can use to represent such sections

- header: `<header>`

- navigation bar: `<nav>`

- main content: `<main>`, with various content subsections represented by `<article>`, `<section>`, and `<div>` elements

- sidebar: `<aside>`; often placed inside `<main>`

- footer: `<footer>`

## HTML layout elements in more detail

##### `<main>`

- This is for content unique to this page

- Use `<main>` only once per page, and put it directly inside `<body>`

- Ideally this shouldn't be nested within other elements

##### `<article>`

- This encloses a block of related content that makes sense on its own without the rest of the page

##### `<section>`

- This is similar to `<article>`, but it is more for grouping together a single part of the page that constitutes one single piece of functionality (e.g., a mini map, or a set of article headlines and summaries), or a theme

- It's considered best practice to begin each section with a heading; also note that you can break `<article>`s up into different `<section>`s, or `<section>`s up into different `<article>`s, depending on the context

##### `<aside>`

- This contains content that is not directly related to the main content but can provide additional information indirectly related to it(glossary entries, author biography, related links, etc.)

##### `<header>`

- This represents a group of introductory content

- If it is a child of `<body>` it defines the global header of a webpage, but if it's a child of an `<article>` or `<section>` it defines a specific header for that section

##### `<nav>`

- This contains the main navigation functionality for the page

- Secondary links, etc., would not go in the navigation

##### `<footer>`

- This represents a group of end content for a page

### Non-semantic wrappers

- Sometimes you'll come across a situation where you can't find an ideal semantic element to group some items together or wrap some content

- Sometimes you might want to just group a set of elements together to affect them all as a single entity with some CSS or JavaScript

- For cases like these, HTML provides the `<div>` and `<span>` elements

- You should use these preferably with a suitable `class` attribute, to provide some kind of label for them so they can be easily targeted

- `<span>` is an inline non-semantic element, which you should only use if you can't think of a better semantic text element to wrap your content, or don't want to add any specific meaning

```html
<p>The King walked drunkenly back to his room at 01:00, the beer doing nothing to aid
him as he staggered through the door <span class="editor-note">[Editor's note: At this point in the
play, the lights should be down low]</span>.</p>
```

- `<div>` is a block level non-semantic element, which you should only use if you can't think of a better semantic block element to use, or don't want to add any specific meaning

```html
<div class="shopping-cart">
  <h2>Shopping cart</h2>
  <ul>
    <li>
      <p><a href=""><strong>Silver earrings</strong></a>: $99.95.</p>
      <img src="../products/3333-0985/thumb.png" alt="Silver earrings">
    </li>
    <li>
      …
    </li>
  </ul>
  <p>Total cost: $237.89</p>
</div>
```

> Warning
>
> Divs are so convenient to use that it's easy to use them too much. As they carry no semantic value, they just clutter your HTML code. Take care to use them only when there is no better semantic solution and try to reduce their usage to the minimum

### Line breaks and horizontal rules

- `<br>` creates a line break in a paragraph; it is the only way to force a rigid structure in a situation where you want a series of fixed short lines

```html
<p>There once was a man named O'Dell<br>
Who loved to write HTML<br>
But his structure was bad, his semantics were sad<br>
and his markup didn't read very well.</p>
```

<p>There once was a man named O'Dell<br>
Who loved to write HTML<br>
But his structure was bad, his semantics were sad<br>
and his markup didn't read very well.</p>

- `<hr>` elements create a horizontal rule in the document that denotes a thematic change in the text

```html
<p>Ron was backed into a corner by the marauding
   netherbeasts. Scared, but determined to protect his friends, he raised his
   wand and prepared to do battle, hoping that his distress call had made it through.</p>
<hr>
<p>Meanwhile, Harry was sitting at home, staring at his royalty statement
  and pondering when the next spin off series would come out, when an enchanted
  distress letter flew through his window and landed in his lap. He read it
  hazily and sighed; "better get back to work then", he mused.</p>
```

<p>Ron was backed into a corner by the marauding
   netherbeasts. Scared, but determined to protect his friends, he raised his
   wand and prepared to do battle, hoping that his distress call had made it through.</p>
<hr>
<p>Meanwhile, Harry was sitting at home, staring at his royalty statement
  and pondering when the next spin off series would come out, when an enchanted
  distress letter flew through his window and landed in his lap. He read it
  hazily and sighed; "better get back to work then", he mused.</p>

## Planning a simple website

- Once you've planned out the structure of a simple webpage, the next logical step is to try to work out what content you want to try to work out what content you want to put on a whole website, what pages you need, and how they should be arranged and link to one another for the best possible user experience

- This is called Information architecture

1. Bear in mind that you'll have a few elements common to most (if not all) pages $---$ such as the navigation menu, and the footercontent. Note down what you want to have common to every page

2. Next, draw a rough sketch of what you might want the structure of each page to look like. Note what each block is going to be

3. Now, brainstorm all the other (not common to every page) content you want to have on your website $---$ write a big list down

4. Next, try to sort all these content items into groups to give you an idea of what parts might live together on different pages

5. Now try to sketch a rough sitemap $---$ have a bubble for each page on your site, and draw lines to show the typical workflow between pages

- The homepage will probably be in the center, and link to most if not all of the others; most of the pages in a small site should be available from the main navigation, although there are exceptions

- You might also want to include notes about how things might be presented
