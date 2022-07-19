---
layout: default
title: HTML text fundamentals
parent: HTML
grand_parent: Study
nav_order: 3
mathjax: true
mermaid: true
permalink: /docs/web/3
---

# HTML text fundamentals
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

> 참고: [HTML text fundamentals](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/HTML_text_fundamentals)

- Objective: Learn how to mark up a basic page of text to give it structure and meaning $---$ including paragraphs, headings, lists, emphasis, and quotations

## The basics: headings and paragraphs

##### paragraphs

- `<p>` element

```html
<p>I am a paragraph, oh yes I am.</p>
```

##### headings

- `<h1>`, `<h2>`, `<h3>`, `<h4>`, `<h5>`, `<h6>`

```html
<h1>I am the title of the story.</h1>
```

### Implementing structural hierarchy

- Proferably, you should use a single `<h1>` per page $---$ this is the top level heading, and all others sit below this in the hierarchy

- Make sour you use the headings in the correct order in the hierarchy.

- Of the six heading levels available, you should aim to use no mor than three per page, unless you feel it is necessary

### Why do we need structure?

- Search engines indexing your page consider the contents of headings as important keywords for influencing the page's search rankings

- Without headings, your page will perform poorly in terms of SEO (Search Engine Oprimization)

- To style content with CSS, or make it do interesting things with JavaScript, you need to have elements wrapping the relevant content, so CSS/JavaScript can effectively target it

### Why do we need semantics?

- We are using the correct elements, giving our content the correct meaning, function, or appearance

## Lists

### Unordered

- Unordered lists are used to mark up lists of items for which the order of the items doesn's matter

```html
<ul>
  <li>milk</li>
  <li>eggs</li>
  <li>bread</li>
  <li>hummus</li>
</ul>
```

- `<ul>` element $---$ this wraps around all the list items

- `<li>` element $---$ this wraps each list item

### Ordered

- Ordered lists are lists in which the order of the items does matter

- `<ol>` element $---$ this wraps around all the list items

- `<li>` element $---$ this wraps each list item

```html
<ol>
  <li>Drive to the end of the road</li>
  <li>Turn right</li>
  <li>Go straight across the first two roundabouts</li>
  <li>Turn left at the third roundabout</li>
  <li>The school is on your right, 300 meters up the road</li>
</ol>
```

### Nesting lists

- You might want to have some sub-bullets sitting below a top-level bullet

```html
<ol>
  <li>Remove the skin from the garlic, and chop coarsely.</li>
  <li>Remove all the seeds and stalk from the pepper, and chop coarsely.</li>
  <li>Add all the ingredients into a food processor.</li>
  <li>Process all the ingredients into a paste.
    <ul>
      <li>If you want a coarse "chunky" hummus, process it for a short time.</li>
      <li>If you want a smooth hummus, process it for a longer time.</li>
    </ul>
  </li>
</ol>
```

## Emphasis and importance

- HTML provides various semantic elements to allow us to mark up textual content with such effects

### Emphasis

- When we want to add emphasis in written language we tend to stress words by putting them in italics

- In HTML we use the `<em>` (emphasis) element to mark up such instances

- These are recognize by screen readers and spoken out in a different tone of voice

- Browsers style this as italic by default, but you shouldn't use this tag purely to get italic styling

- To do that, you'd use a `<span>` element and some CSS, or perhaps an `<i>` element

```html
<p>I am <em>glad</em> you weren't <em>late</em>.</p>
```

### Strong importance

- To emphasize important words, we tend to bold them in written language

- In HTML we use the `<strong>` (strong importance) element to mark up such instances

- These are recognized by screen readers and spoken in a different tone of voice

- Browsers style this as bold text by default, but you shouldn't use this tag purely to get bold styling

- To do that, you'd use a `<span>` element and some CSS, or perhaps a `<b>` element

```html
<p>This liquid is <strong>highly toxic</strong>.</p>

<p>I am counting on you. <strong>Do not</strong> be late!</p>
```

- You can nest strong and emphasis inside one another if desired

```html
<p>This liquid is <strong>highly toxic</strong> —
if you drink it, <strong>you may <em>die</em></strong>.</p>
```

### Italic, bold, underline...

- The elements we've discussed so far have clearcut associated semantics

- The situation with `<b>`, `<i>`, and `<u>` is somewhat more complicated

- They came about so people could write bold, italics, or underlined text in an era when CSS was still supported poorly or not at all

- Elements like this, which only affect presentation and not semantics, are known as presentational elements and should no longerbe used because semantics is so important to accessibility, SEO, etc.

- HTML5 redefined `<b>`, `<i>`, and `<u>` with ew, somewhat confusing, sementic roles

- It's only appropriate to use `<b>`, `<i>`, or `<u>` to convey a meaning traditionally conveyed with bold, italics, or underline when there isn't a more suitable element; and there usually is.

- Consider whether `<string>`, `<em>`, `<mark>`, or `<span>` might be more appropriate

- `<i>` is used to convey a meaning traditionally conveyed by italic: foreign words, taxonomic designation, technical terms, a thought...

- `<b>` is used to convey a meaning traditionally conveyed by bold: keywords, product names, lead sentence...

- `<u>` is used to convey a meaning traditionally conveyed by underline: proper name, misspelling

> Note
>
> People strongly associate underlining with hyperlinks. Therefore, on the web, It's best to only underline links. Use the `<u>` element when it's semantically appropriate, but consider using CSS to change the default underline to something more appropriate on the web. The example below illustrates how it can be done

```html
<!-- scientific names -->
<p>
  The Ruby-throated Hummingbird (<i>Archilochus colubris</i>)
  is the most common hummingbird in Eastern North America.
</p>

<!-- foreign words -->
<p>
  The menu was a sea of exotic words like <i lang="uk-latn">vatrushka</i>,
  <i lang="id">nasi goreng</i> and <i lang="fr">soupe à l'oignon</i>.
</p>

<!-- a known misspelling -->
<p>
  Someday I'll learn how to <u class="spelling-error">spel</u> better.
</p>

<!-- term being defined when used in a definition -->
<dl>
  <dt>Semantic HTML</dt>
  <dd>Use the elements based on their <b>semantic</b> meaning, not their appearance.</dd>
</dl>
```


