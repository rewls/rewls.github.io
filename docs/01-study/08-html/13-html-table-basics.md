---
layout: default
title: HTML table basics
parent: HTML
grand_parent: Study
nav_order: 13
mathjax: true
mermaid: true
permalink: /docs/html/13
---

# HTML table basics
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

> 참고: [HTML table basics](https://developer.mozilla.org/en-US/docs/Learn/HTML/Tables/Basics)

- Objective: To gain basic familiarity with HTML tables

## What is a table?

- A table is a structured set of data made up of rows and columns (tabular data)

### When should you NOT use HTML tables?

- In short, using tables for layout rather than CSS layout techniques is a bad idea

###### Main reasons

1. Layout tables reduce accessibility for visually impaired users

	- Screenreaders interpret the tags that exist in an HTML page and read out the contents to the user

	- Because tables are not the right tool for layout, and the markup is more complex than with CSS layout techniques, the screenreaders' output will be confusing to their users

2. Tables produce tag soup

	- table layouts generally involve more complex markup structures than proper layout techniques.

	- This can result in the code being harder to write, maintain, and debug

3. Tables are not automatically responsive

	- When you use proper layout containers (such as `<header>`, `<section>`, `<article>`, or `<div>`), their width defaults to 100% of their parent element

	- Tables on the other hand are sized according to their content by default, so extra measures are needed to get table layout styling to effectively work across a variety of devices

## Activelearning: Creating your first table

1. The content of every table is enclosed by these two tags: `<table></table>`. Add these inside the body of your HTML

2. The smallest container inside a table is a table cell, which is created by a `<td>` element ('td' stands for 'table data') . Add `<td>` element inside your table tags

```html
<td>Hi, I'm your first cell.</td>
```

3. If we want a row of four cells, we need to copy these tags three times. The cells are not placed underneath each other, rather they are automatically aligned with each other on the same row

```html
<td>Hi, I'm your first cell.</td>
<td>I'm your second cell.</td>
<td>I'm your third cell.</td>
<td>I'm your fourth cell.</td>
```

4. To stop this row from growing and start placing subsequent cells on a second row, we need to use the `<tr>` element ('tr' stands for 'table row'). Place the fourcells you've already created inside `<tr>` tags

```html
<tr>
  <td>Hi, I'm your first cell.</td>
  <td>I'm your second cell.</td>
  <td>I'm your third cell.</td>
  <td>I'm your fourth cell.</td>
</tr>
```

5. You have a go at making one or two more $---$ each row needs to be wrapped in an additional `<tr>` element, with each cell contained in a `<td>`

## Adding headers with `<th>` elements

- Table headers $---$ special cells that go at the start of a row or column and define the type of data that row or column contains

### Active learning: table headers

- To recognize the table headers as headers, both visually and semantically, you can use the `<th>` elements ('th' stands for 'table header')

	- This works in exactly the same way as a `<td>`, except that it denotes a header, not a normal cell

### Why are headers useful?

- It is easier to find the data you are looking for when the headers clearly stand out, and the design just generally looks better

- Along with the `scope` attribute, they allow you to make tables more accessible by associating each header with all the data in the same row or column

	- Screenreaders are then able to read out a whole row or column of data at once

## Allowing cells to span multiple rows and columns

- Sometimes we want cells to span multiple rows or columns

- Table headers and cells have the `colspan` and `rowspan` attributes, which allow us to do just those things

- Both accept a unitless number value, which equals the number of rows or columns you want spanned

```html
<table>
  <tr>
	<th colspan="2">Animals</th>
  </tr>
  <tr>
	<th colspan="2">Hippopotamus</th>
  </tr>
  <tr>
	<th rowspan="2">Horse</th>
	<td>Mare</td>
  </tr>
  <tr>
	<td>Stallion</td>
  </tr>
  <tr>
	<th colspan="2">Crocodile</th>
  </tr>
  <tr>
	<th rowspan="2">Chicken</th>
	<td>Hen</td>
  </tr>
  <tr>
	<td>Rooster</td>
  </tr>
</table>
```

## Providing common styling to columns

### Styling with `<col>`

- HTML has a method of defining styling information for an entire column of data all in one place $---$ the `<col>` and `<colgroup>` elements

- We can specify the information once, on a `<col>` element.

- `<col>` elements are specified inside a `<colgroup>` container just below the opening `<table>` tag

```html
<table>
  <colgroup>
    <col>
    <col style="background-color: yellow">
  </colgroup>
  <tr>
    <th>Data 1</th>
    <th>Data 2</th>
  </tr>
  <tr>
    <td>Calcutta</td>
    <td>Orange</td>
  </tr>
  <tr>
    <td>Robots</td>
    <td>Jazz</td>
  </tr>
</table>
```

- We are not styling the first column, but we still have to include a blank `<col>` element

- If we wanted to apply the styling information to both columns, we could just include one `<col>` element with a span attribute on it, like this

```html
<colgroup>
  <col style="background-color: yellow" span="2">
</colgroup>
```

- Just like `colspan` and `rowspan`, `span` takes a unitless number value that specifies the number of columns you want the styling to apply to.
> Note
>
> Styling columns like this is limited to a few properties: `border`, `background`, `width`, and `visibility`. To set other properties you'll have to either style every `<td>` or `<th>` in the column, or use a omplex selector such as `:nth-child`
