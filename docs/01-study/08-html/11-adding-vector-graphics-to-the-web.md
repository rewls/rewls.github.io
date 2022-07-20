---
layout: default
title: Adding vector graphics to the web
parent: HTML
grand_parent: Study
nav_order: 11
mathjax: true
mermaid: true
permalink: /docs/html/11
---

# Adding vector graphics to the web
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

> 참고: [Adding vector graphics to the web](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Adding_vector_graphics_to_the_Web)

- Vector graphics are very useful in many circumstances $---$ they have small file sizes and are highly scalable, so they don't pixelate when zoomed in or blown up to a large size

- Objective: Learn how to embed a SVG (vector) image into a webpage

## What are vector graphics?

- On the web, you'll work with two types of images $---$ raster images, and vector images

- Raster images are defined using a grid of pixels $---$ a raster image file contains information showing exactly where each pixel is to be placed, and exactly what color it should be

	- Popular web raster formats include Bitmap (`.bmp`), PNG (`.png`), JPEG (`.jpg`), and GIF (`.gif`)

- Vector images are defined using algorithms $---$ a vector image file contains shape and path definitions that the computer can use to work out what the image should look like when rendered on the screen

	- The SVG format allows us to create powerful vector graphics for use on the Web

- The difference becomes apparent when you zoom in the page $---$ the PNG image becomes pixelated as you zoom in because it contains information on where each pixel should be (and what color).

- The vector image however continues to look nice and crisp, because no matter what size it is, the algorithms are used to work out the shapes in the image, with the values being scaled as it gets bigger

- Moreover, vector image files are much lighter than their raster equivalents, because they only need to hold a handful of algorithms, rather than information on every pixel in the image individually

## What is SVG

- SVG is an XML-based language for describing vector images

- It's basically markup like HTML, except that you've got many different elements for defining the shapes you want to appear in your image, and the effects you want to apply to those shapes

- SVG is for marking up graphics, not content

- Atthe simplest end of the spectrum, you've got elements for creating simple shapes, like `<circle>` and `<rect>`

- More advanced SVG features include `<feColorMatrix>` (transform colors using a transformation matrix), `<animate>` (animate parts of your vector graphic) and `<mask>` (apply a mask over the top of your image)

- As a simple example, the following code creates a circle and a rectangle

```html
<svg version="1.1"
     baseProfile="full"
     width="300" height="200"
     xmlns="http://www.w3.org/2000/svg">
  <rect width="100%" height="100%" fill="black" />
  <circle cx="150" cy="100" r="90" fill="blue" />
</svg>
```

<svg version="1.1"
     baseProfile="full"
     width="300" height="200"
     xmlns="http://www.w3.org/2000/svg">
  <rect width="100%" height="100%" fill="black" />
  <circle cx="150" cy="100" r="90" fill="blue" />
</svg>

- You can handcode simple SVG in a text editor, but for a complex image this quickly starts to get very difficult

- For creating SVG images, most people use a vector graphics editor like Inkscape or Illustrator

- These packages allow you to create a variety of illustrations using various graphics tools, and create approximations of photos

##### Advatages

- Text in vector images remains accessible (which also benefits your SEO)

- SVGs lend themselves well to styling/scripting, because each component of the image is an element that can be styled via CSS or scripted via JavaScript

##### Disadvantages

- SVG can get complicated very quickly, meaning that file sizes can grow; complex SVGs can also take significant processing time in the browser

- SVG can be harder to create than raster images depending on what kind of image you are trying to create

- SVG is not supported in older browsers, so may not be suitable if you need to support older versions of Internet Explorer with your web site (SVG started being supported as of IE9

- Raster graphics are arguably better for complex precision images such as photos

> Note
>
> In Inkscape, save your files as Plain SVG to save space

## Adding SVG to your pages

### The quick way: `img` element

- To embed an SVG via an `<img>` element, you just need to reference it in the src attribute

- You will need a `height` or a `width` attribute (or both if your SVG has no inherent aspect ratio)

```html
<img
    src="equilateral.svg"
    alt="triangle with all three sides equal"
    height="87"
    width="100" />
```

##### Pros

- Quick, familiar image syntax with built-in text equivalent available in the `alt` attribute

- You can make the image into a hyperlink easily by nesting the `<img>`inside an `<a>` element

- The SVG file can be cached by the browser, resulting in faster loading times for any page that used the image loaded in the future

##### Cons

- You cannotmanipulate the image with JavaScript

- If you want to control the SVG content with CSS, you must include inline CSS styles in your SVG code (External stylesheets invoke from the SVG file take no effect

- You cannot restyle the image with CSS pseudoclasses (like `:focus`)

### Troubleshooting and crosss-browser support

- For browsers that don't support SVG, you could reference a PNG or JPG from your `src` attribute and use a `srcset` attribute (which only recent browsers recognize) to reference the SVG

- This being the case, only supporting browsers will load the SVG $---$ older browsers will load the PNG instead

```html
<img src="equilateral.png" alt="triangle with equal sides" srcset="equilateral.svg">
```

- You can also use SVGs as CSS background images

- In the below code, older browsers will stick with the ONG that they understand, while newer browsers will load the SVG

```css
background: url("fallback.png") no-repeat center;
background-image: url("image.svg");
background-size: contain;
```

- Inserting SVGs uwingCSS background images means that the SVG can't be manipulated with JavaScript, and is also subject to the same CSS limitations

- If your SVGs aren't showing up at all, it might be because your server isn't set up properly. if that's the problem, [A word on Webservers](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Getting_Started#a_word_on_webservers) article will point you in the right direction.

### How to include SVG code inside your HTML

- You can also open up the SVG file in a text editor, copy the SVG code, and paste it into your HTML document $---$ this is sometimes called putting your SVG inline, or inlining SVG

- Make sure your SVG code snippet begins with an `<svg>` start tag and ends with an `</svg>` end tag

- Here's a very simple example of what you might paste into your document

```html
<svg width="300" height="200">
    <rect width="100%" height="100%" fill="green" />
</svg>
```

##### Pros

- Putting your SVG inline saves an HTTP request, andtherefore can reduce a bit your loading time

- You can assign `class`es and `id`s to SVG elements and style them with CSS, either within the SVG or wherever you put the CSS style rules for your HTML document

	- You can use any SVG presentation attribute as a CSS property

- Inlining SVG is the only approach that lets you use CSS interactions (like `:focus`) and CSS animationson your SVG image (even in your regular stylesheet)

- You can make SVG markup into a hyperlink by wrapping it in an `<a>` element

##### Cons

- this method is only suitalbe if you're using the SVG in only one place

	- Duplication makes for resource-intensive maintenance

- Extra SVG code increases the size of your HTML file

- The browser cannot cache inline SVG as it would cache regular image assets, so pages that include the image will not load faster after the first page containing the image is loaded

- You may include fallback in a `<foreignObject>` element, but browsers that support SVG still download any fallback images.

	- You need to weight whether the extra overhead is really worthwhile, just to support obsolescent browsers

### How to embed an SVG with an `iframe`

- You can open SVG images in your browser just like webpages. So embedding an SVG document with an `<iframe>` is done

```html
<iframe src="triangle.svg" width="500" height="500" sandbox>
    <img src="triangle.png" alt="Triangle with three unequal sides" />
</iframe>
```

- This is definitely not the best method to choose

##### Cons

- `iframe`s do have a fallback mechanism, but browsers only display the fallback if they lack support for `iframe`s altogether

- Moreover, unless the SVG and your current webpage have the same origin, you cannot use JavaScript on your main webpage to manipulate the SVG
