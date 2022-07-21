---
layout: default
title: HTML table advanced features and accessibility
parent: HTML
grand_parent: Study
nav_order: 14
mathjax: true
mermaid: true
permalink: /docs/html/14
---

# HTML table advanced features and accessibility
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

> 참고: [HTML table advanced features and accessibility](https://developer.mozilla.org/en-US/docs/Learn/HTML/Tables/Advanced)

- Objective: To learn about more advanced HTML table features, and the accessibility of tables

## Adding a caption to your table with `<caption>`

- You can give your table a caption by putting it inside a `<caption>` elva and nesting that inside the `<table>` elva

- You should put it just below the opening `<table>` tag

```html
<table>
  <caption>Dinosaurs in the Jurassic period</caption>

  …
</table>
```

- The caption is meant to contain a description of the table contents

- Rather than hvae a screenreader read out the contents of many cells just to find out what the table is about, the user can rely on a caption and then decide whether or not to read the table in greater detail

> Note
>
> The `summary` attribute` can also be used on the `<table>` elva to provide a description $---$ this is also read out by screenreaders. We'd recommend using the `<caption>` elva instead, however, as `summary` is deprecated by the HTML5 spec and can't be read by sighted users (it doesn't appear on the page

## Adding structure with `<thead>`, `<tfoot>`, and `<tbody>`

- As your tables get a bit more complex in structure, it is useful to give them more structural definition

- One clear way to do this is by using `<thead>`, `<tfoot>`, and `<tbody>`, which allow you to mark up a header, footer, and body section for the table

- These elements don't make the table any more accessible to screenreader users, and don't result in any visual enhancement on their own

- They are however very useful for styling and layout $---$ acting as useful hooks for adding CSS to your table

- To give you some interesting examples, in the case of a long table you could make the table header and footer repeat on every printed page, and you could make the table body display on a single page and have the contents available by scrolling up and down

### To use them

- The `<thead>` elements must wrap the part of the table that is the header. If you are using `<col>`/`<colgroup>` elements, the table header should come just below those

- The `<tfoot>` elements needs to wrap the part of the table that is the footer

	- You can include the table footer right at the bottom of the table, or just below the table header (the browser will still render it at the bottom of the table)

- The `<tbody>` elements needs to wrap the other parts of the table content that aren't in the table header or footer.

> Note
>
> `<tbody>` is always included in every table, implicitly if you don't specify it in your code. You should include `<tbody>`, because it gives you more control over your table structure and styling

## Nesting tables

- It is possible to nest a table inside another one, as long as you include the complete structure, including the `<table>` element

- This is generally not really advised, as it makes the markup more confusing and less accessible to screenreader users, and in many cases you might as well just insert extra cells/rows/columns into the existing table

- It is however sometimes necessary, for example if you want to import content easily from other sources

```html
<table id="table1">
  <tr>
    <th>title1</th>
    <th>title2</th>
    <th>title3</th>
  </tr>
  <tr>
    <td id="nested">
      <table id="table2">
        <tr>
          <td>cell1</td>
          <td>cell2</td>
          <td>cell3</td>
        </tr>
      </table>
    </td>
    <td>cell2</td>
    <td>cell3</td>
  </tr>
  <tr>
    <td>cell4</td>
    <td>cell5</td>
    <td>cell6</td>
  </tr>
</table>
```

## Tables for visually impaired users

- With the proper markup we can replace visual associations by programmatic ones

### Using column and row headers

- Screenreaders will identify all headers and use them to make programmatic associations between those headers and the cells they relate to

- The combination of column and row headers will identify and interpret the data in each cell so that screenreader users can interpret the table similarly to how a sighted user does

### The scope attribute

- `scope` attribute, which can be added to the `<th>` element to tell screenreaders exactly what cells the header is a header for $---$ is it a header for the row it is in, or the column

```html
<thead>
  <tr>
    <th scope="col">Purchase</th>
    <th scope="col">Location</th>
    <th scope="col">Date</th>
    <th scope="col">Evaluation</th>
    <th scope="col">Cost (€)</th>
  </tr>
</thead>
```

```html
<tr>
  <th scope="row">Haircut</th>
  <td>Hairdresser</td>
  <td>12/09</td>
  <td>Great idea</td>
  <td>30</td>
</tr>
```

- `scope` has two more possible values $---$ `colgroup` and `rowgroup`

- These are used for headings that sit over the top of multiple columns or rows

### The id and headers attributes

- An alternative to using the `scope` attribute is to use `id` and `headers` attributes to create associations between headers and cells

- The way they are sued is as follows:

	1. You add a unique `id` to each `<th>` element

	2. You add a `headers` attribute to each `<td>` element

		- Each `headers` attribute has to contain a list of the `id`s of all the `<th>` element that act as a header for that cell, separated by spaces

- This gives your HTML table an explicit definition of the position of each cell in the table, defined by the header(s) for each column and row it is part of, kind of like a spreadsheet

- For it to work well, the table really needs both column and row headers

```html
<thead>
  <tr>
    <th id="purchase">Purchase</th>
    <th id="location">Location</th>
    <th id="date">Date</th>
    <th id="evaluation">Evaluation</th>
    <th id="cost">Cost (€)</th>
  </tr>
</thead>
<tbody>
<tr>
  <th id="haircut">Haircut</th>
  <td headers="location haircut">Hairdresser</td>
  <td headers="date haircut">12/09</td>
  <td headers="evaluation haircut">Great idea</td>
  <td headers="cost haircut">30</td>
</tr>

  …

</tbody>
```

> Note
>
> This method creates very precise associations between headers and data cells but it uses a lot more markup and does not leave any room for errors. The `scope` approach is usually enough for most tables
