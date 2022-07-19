---
layout: default
title: Creating hyperlinks
parent: HTML
grand_parent: Study
nav_order: 4
mathjax: true
mermaid: true
permalink: /docs/web/4
---

# Creating hyperlinks
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

> 참고: [Creating hyperlinks](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/Creating_hyperlinks)

- Hyperlinks are really important $---$ they are what makes the Web a web

- Objective: To learn how to implement a hyperlink effectively, and link multiple files together

## What is a hyperlink?

- Hyperlinks are one of the most exciting innovations the Web has to offer

- They've been a feature of the Web since the beginnning, and are what makes the Web a web

- Hyperlinks allow us to link documents to other documents or resources, link to specific parts of documents, or make apps available at a web address

> Note
>
> A URL can point to HTML files, text files, images, text documents, video an audio files, or anything else that lives on the Web. If the web browser doesn't know how to display or handle the file, it will ask you if you want to open the file (in which case the duty of opening or handling the file is passed to a suitable native app on the device) or download the file (in which case you can try to deal with it later on)

## Anatomy of a link

- A basic link is created by wrapping the text or other content, inside an `<a>` element and using the `href` attribute, also known as a Hypertext Reference, or target, that contains the web address

```html
<p>I'm creating a link to
<a href="https://www.mozilla.org/en-US/">the Mozilla homepage</a>.
</p>
```

<p>I'm creating a link to
<a href="https://www.mozilla.org/en-US/">the Mozilla homepage</a>.
</p>

### Ading supporting information with the title attribute

- Another attribute you may want to add to your links is `title`

- The title contains additional information about the link

```html
<p>I'm creating a link to
<a href="https://www.mozilla.org/en-US/"
   title="The best place to find more information about Mozilla's
          mission and how to contribute">the Mozilla homepage</a>.
</p>
```

<p>I'm creating a link to
<a href="https://www.mozilla.org/en-US/"
   title="The best place to find more information about Mozilla's
          mission and how to contribute">the Mozilla homepage</a>.
</p>

> Note
>
> A link title is only revealed on mouse hover, which means that people relying on keyboard controls or touchscreens to navigate web pages will have difficulty accessing title information. if a title's information is truly important to the usability of the page, then you should present it in a manner that will be accessible to all users, for example by putting it in the regular text

### Block level links

- Almost any content can be made into a link, even block-level elements

```html
<a href="https://www.mozilla.org/en-US/">
  <img src="mozilla-image.png" alt="mozilla logo that links to the Mozilla homepage">
</a>
```

<a href="https://www.mozilla.org/en-US/">
  <img src="mozilla-image.png" alt="mozilla logo that links to the Mozilla homepage">
</a>

## A quick primer on URLs and paths

- A URL, or Uniform Resource Locator is a string of text that defines where somethin is located on the Web

- URLs use paths to find files

- Paths specify where the file you're interested in is located in the filesystem

### Document fragments

- It's possible to link to a specific part of an HTML document, known as a document fragment

- To do this you first have to assign an `id` attribute to the elements you want tto link to

```html
<h2 id="Mailing_address">Mailing address</h2>
```

- Then to linke to that specific `id` you'd include it at the end of the URL, preceded by a hash/pound symbol (`#`)

```html
<p>Want to write us a letter? Use our <a href="contacts.html#Mailing_address">mailing address</a>.</p>
```

- You can even use the document fragment reference on its own to link to another part of the current document

```html
<p>The <a href="#Mailing_address">company mailing address</a> can be found at the bottom of this page.</p>
```

### Absolute vs. relative URLs

##### Absolute URL

- Points to a locations defines by its absolute location on the web, including protocol and domain name

- An absolute URL will always point to the same location

##### Relative URL

- Points to a location that is relative to the file you are linking from

- A relative URL will point ot different places depending onthe actual location of the file you refer from

## Link best practices

### Use clear link wording

- We need to make our links accessible to all reders

- Screen reader users like jumping around from link to link on the page, and reading links out of context

- Search engines use link text to index target files, so it is a good idea to include keywords in your link text to effectively describe what is being linked to

- Visual readers skim over the page rather than reading every word, and their eyes will be drawn to page features that tand out, like links

- Good link text

```html
<p><a href="https://www.mozilla.org/firefox/">
  Download Firefox
</a></p>
```

<p><a href="https://www.mozilla.org/firefox/">
  Download Firefox
</a></p>

- Bad link text

```html
<p><a href="https://www.mozilla.org/firefox/">
  Click here
</a>
to download Firefox</p>
```

<p><a href="https://www.mozilla.org/firefox/">
  Click here
</a>
to download Firefox</p>

##### Other tips

- Don't repeat the URL as part of the link text

- Don't say "link" or "links to" in the link text

- Keep your link text as short as possible

- Minimize instances where multiple copies of the same text are linked to different places

### Linking to non-HTML resources $---$ leave clear signposts

- When linking to a resource that will be downloaded, streamed, or has another potentially unexpected effect, you should add clear wording to reduce any confusion

```html
<p><a href="https://www.example.com/large-report.pdf">
  Download the sales report (PDF, 10MB)
</a></p>

<p><a href="https://www.example.com/video-stream/" target="_blank">
  Watch the video (stream opens in separate tab, HD quality)
</a></p>

<p><a href="https://www.example.com/car-game">
  Play the car game (requires Flash)
</a></p>
```

<p><a href="https://www.example.com/large-report.pdf">
  Download the sales report (PDF, 10MB)
</a></p>

<p><a href="https://www.example.com/video-stream/" target="_blank">
  Watch the video (stream opens in separate tab, HD quality)
</a></p>

<p><a href="https://www.example.com/car-game">
  Play the car game (requires Flash)
</a></p>

### E-mail links

- It's possible to create links or buttons that, when clicked, open a new outgoing email message

- This is done using the `<a>` element and the `mailto:`  URL scheme

- In its most basic and commonly used form, a `mailto:` link indicates the email address of the intended recipient

```html
<a href="mailto:nowhere@mozilla.org">Send email to nowhere</a>
```

<a href="mailto:nowhere@mozilla.org">Send email to nowhere</a>

- In fact, the elmail address is optional

- If you omit it and your `href` is `mailto:`, a new outgoing email window will be opened by the user's email client with no destination address

- This is often useful as "Share" links that users can click to send an email to an address of their choosing

### Specifying details

- In addition to the email address, you can provide other information

- In fact, any standard mail header fields can be added to the `mailto` URL you provide

- The most commonly used of these are "subject", "cc", and "body" (which is not a true header field, but allows you to specify a short content message for the new email)o

- Each field and its value is speciied as a query term

- Here's an example that includes a cc, bcc, subject and body:

```html
<a href="mailto:nowhere@mozilla.org?cc=name2@rapidtables.com&bcc=name3@rapidtables.com&subject=The%20subject%20of%20the%20email&body=The%20body%20of%20the%20email">
  Send mail with cc, bcc, subject and body
</a>
```

> Note
>
> The values of each field must be URL-encoded with non-printing characters (invisible characters like tabs, carriage returns, and page breaks) and spaces percent-escaped. Also, note the use of the question mark (`?`) to separate the main URL from the field values, and ampersands (`&`) to separate each field in the `mailto:` URL. This is standard URL query notation
