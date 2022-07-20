---
layout: default
title: Images in HTML
parent: HTML
grand_parent: Study
nav_order: 8
mathjax: true
mermaid: true
permalink: /docs/html/8
---

# Images in HTML
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

> 참고: [Images in HTML](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Images_in_HTML)

- Objective: To learn how to embed simple images in HTML, annotate them with captions, and how HTML images relate to CSS background images

## How do we put an image on a webpage?

- In order to put a simple image on a webpage, we use the `<img>` element

- This is an empty element that requires a minimum of one attribute to be useful $---$ `src` (source)

- The `src` attribute contains a path pointing to the image you want to embed in the page which can be a relative or absolute URL

```html
<img src="images/dinosaur.jpg">
```

> Note
>
> Search engines also read image filenames and count them towards SEO. Therefore, you should give your image a descriptive filename

- But this is pointless, as it just makes the browser do more work, looking up the IP address from the DNS server all over again, etc.

- You'll almost always keep the images for your website on the same server as your HTML

> Warning
>
> Most images are copyrighted. Do not display an image on your webpage unless
>
> - You own the image
>
> - You have received explicit, written permission from the image owner
>
> - You have ample proof that the image is, in fact, in the public domain
>
> In addition, never point your `src` attribute at an image hosted on someone else's website that you don't have permission to link to. This is called "hotlinking". Again, stealing someone's bandwidth is illegal. It also slows down your page, leaving you with no control over whether the image is removed or replaced with something embarrassing

> Note
>
> Element like `<img>` and `<video>` are sometimes referred to as replaced elements. This is because the element's content and size are defined by an external resource, not by the contents of the element itself

### Alternative text

- The next attribute we'll look at is `alt`

- Its value is supposed to be a textual description of the image, for use in situations where the image cannot be seen/displayed or takes a long time to render because of a slow internet connection

```html
<img src="images/dinosaur.jpg"
     alt="The head and torso of a dinosaur skeleton;
          it has a large head with long sharp teeth">
```

<img src="images/dinosaur.jpg"
     alt="The head and torso of a dinosaur skeleton;
          it has a large head with long sharp teeth">

##### Why would you ever see or need alt text

- In fact, having alt text available to describe images is useful to most users

- The spelling of the file or path name might be wrong

- The browser doesn't support the image type

- You may want to provide text for search engines to utilize

- Users have turned off images to reduce data transfer volume and distractions. This is especially common on mobile phones, and in countries where bandwidth is limited or expensive

##### What exactly should you write inside your `alt` attribute

- Decoration.

	- You should use CSS background images for decorative images, but if you must use HTML, add a blank `alt=""`. If the image isn't part of the content, a screen reader shouldn't waste time reading it

- Content

	- If your image provides significant information, provide the same information in a brief `alt` text $---$ or even better, in the main text which everybody can see

	- If the image is described adequately by the main text body, you can jst use `alt=""`

- Link

	- If you put an image inside `<a>` tags, to turn an image into a link, you still must provide accessible link text

	- In such cases you may, either, write it inside the same `<a>` element, or inside the image's `alt` attribute

- Text

	- You should not put your text into images

	- However, If you really can't avoid doing this, you should supply the text inside the `alt` attribute

- Essentially, the key is to deliver a usable experience, even when the images can't be seen

### Width and height

- Your can use the `width` and `height` attributes to specify the width and height of your image

- This doesn't result in must difference to the display, under normal circunstances

- But if the image isn't being displayed, you'll notice the browser is leaving a space for the image to appear in

- This is a good thing to do, resulting in the page loading quicker and more smoothly

- However, you shouldn't alter the size of your images using HTML attributes.

- If you set the image size too big, you'll end up with images that look grainy, fuzzy, or too small, and wasting bandwidth downloading an image that is not fitting the user's needs.

- You sould use an image editor to put your image at the correct size before putting it on your webpage

> Note
>
> If you do need to alter an image's size, you should use CSS instead

### Image titles

- You can add `title` attributes to images, to provide further supportig information if needed

```html
<img src="images/dinosaur.jpg"
     alt="The head and torso of a dinosaur skeleton;
          it has a large head with long sharp teeth"
     width="400"
     height="341"
     title="A T-Rex on display in the Manchester University Museum">
```

- This gives us a tooltip on mouse hover

- However, this is not recommended $---$ `title` has a number of accessibility problems

- It is better to include such supporting information in the main article text

## Annotating images with figures and figure captions

- There are a number of ways that you could add a caption to go with your image

- For example, there would be nothing to stop you from doing this

```html
<div class="figure">
  <img src="images/dinosaur.jpg"
       alt="The head and torso of a dinosaur skeleton;
            it has a large head with long sharp teeth"
       width="400"
       height="341">

  <p>A T-Rex on display in the Manchester University Museum.</p>
</div>
```

- There is nothing that semantically links the image to its caption, which can cause problems for screen readers

- A better solution is to use the HTML5 `<figure>` and `<figcaption>` elements.

- These are created for exactly this purpose: to provide a semantic container for figures, and to clearly link the figure to the caption

```html
<figure>
  <img src="images/dinosaur.jpg"
       alt="The head and torso of a dinosaur skeleton;
            it has a large head with long sharp teeth"
       width="400"
       height="341">

  <figcaption>A T-Rex on display in the Manchester University Museum.</figcaption>
</figure>
```

- The `<figcaption>` element tells browsers, and assistive technology that the caption describes the other content of the `<figure>` element

> Note
>
> Captions and `alt` text shouldn't just say the same thing, because they both appear when the image is gone. Try turning images off in your browser and see how it looks

- A figure doesn't have to be an image. It is an independent unit of content that:

	- Expresses your meaning in a compact, easy-to-grasp way

	- Could go in several places in the page's linear flow

	- Provides essential information supporting the main text

- A figure could be several images, a code snippet, audio, video, equations, a table, or something else

## CSS background images

- You can also use CSS to embed images into webpages

- The CSS `background-image` property, and the other `background-*` properties, are used to control background image placement

- For example, to place a background image on every paragraph on a page

```html
p {
  background-image: url("images/dinosaur.jpg");
}
```

- The resulting embedded image is arguably easier to position and control than HTML images

- CSS background images are for decoration only

- Such images have no semantic meaning at all

- They can't have any text equivalents

- If an image has meaning, in terms of your content, you should use an HTML image

- If an image is purely decoration, you should use CSS backgroud images
