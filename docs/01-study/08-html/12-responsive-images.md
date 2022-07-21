---
layout: default
title: Responsive images
parent: HTML
grand_parent: Study
nav_order: 12
mathjax: true
mermaid: true
permalink: /docs/html/12
---

# Responsive images
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

> 참고: [Responsive images](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images)

- Objective: Learn how to use features like `srcset` and the `<picture>` element to implement responsive image solutions on websites

## Why responsive images?

- A typical website may contain a header image and some content images below the header

- The header image will likely span the whole of the width of the header, and the conten image will fit somewhere inside the content column

### Simple example

- you can [see the example live](https://mdn.github.io/learning-area/html/multimedia-and-embedding/responsive-images/not-responsive.html) and find the [source code](https://github.com/mdn/learning-area/blob/main/html/multimedia-and-embedding/responsive-images/not-responsive.html) on GitHub

- We won't discuss the CSS much in this lesson, except to say that:

	- The body content has been set to a maximum width of 1200 pixels $---$ in viewports above that width, the body remains at 1200px and centers itself in the available space. In viewports below that width, the body will stay at 100% of the width of the view port

	- The header image has been set so that its center always stays in the center of the header, no matter what width the heading is set at. If the site is being viewed on a narrower screen, the important detail in the center of the image can still be seen, and the excess is lost off either side. It is 200px high

	- The content images have been set so that if the body element becomes smaller than the image, the images start to shrink so that they always stay inside the body

### Issues

##### Narrow screen device

- Issues arise when you start to view above site on a narrow sceen device

- The header below looks OK, but it's starting to take up a lot of the screen height for a mobile device

- And at this size, it is difficult to see faces of the two people within the first content image

- An improvement would be to display a cropped version of the image which displays the important details of the image when the site is viewed on a narrow screen

	- A second cropped image could be displayed for a medium-width screen device, like a tablet.

	- The general problem whereby you want to serve different cropped images in that way, for various layouts, is commonly known as the art direction problem

###### Resolution switching problem: different sizes

- In addition, there is no need to embed such large images on the page if it is being viewed on a mobile screen. And conversely, a small raster image starts to look grainy when displayed larger than its original size

- This is called the resolution switching problem

##### Resolution switching problem: same size, different resolutions

- Conversely, it is unnecessary to display a large image on a screen significantly smaller than the size it was meant for

	- Doing so can waste bandwidth

- Ideally, multiple resolutions would be made available to the user's web browser

	- The browser could then determine the optimal resolution to load based on the screen size of the user's device

##### need larger images

- To make thins more complicated, some devices have high resolution screens that need larger images than you might expect to display nicely

- You might think that vector images would solve these problems, and they do to a certain degree

- Vector images are great for simple graphics, patterns, interface element, etc., but It starts to get very complex to create a vector-based image with the kind of detial that you'd find in say, a photo

- Raster image formats such as JPEGs are more suited to the kind of images we see in the above example

### Solution

- Responsive image technologies were implemented recently to solve the problems indicated above by letting you offer the browser several image files, either all showing the same thing but containing different numbers of pixels (resolution switching), or different images suitable for different space allocations (art direction)

> Note
>
> The new features discussed in this article $---$ `srcset`/`sizes`/`<picture>` $---$ are all supported in modern desktop and mobile browsers

## How do you create responsive images?

- Note that we will be focusing on `<img>` elements for this section

### Resolution switching: Different sizes

- We want to display identical image content, just larger or smaller depending on the device

- We can use two new attributes $---$ `srcset` and `sizes` $---$ to provide several additional source images along with hints to help the browser pick the right one

```html
<img srcset="elva-fairy-480w.jpg 480w,
             elva-fairy-800w.jpg 800w"
     sizes="(max-width: 600px) 480px,
            800px"
     src="elva-fairy-800w.jpg"
     alt="Elva dressed as a fairy">
```

- They're not too hard to understand If you format them as shown above, with a different part of the attribute value on each line

- Each value contains a comma-separated list, and each part of those lists is made up of three sub-parts

##### `srcset`

- This defines the set of images we will allow the browser to choose between, and what size each image is

- Each set of image information is separated from the previous one by a comma

- For each one, we write:

	1. An image filename (`elva-fairy-480w.jpg`)

	2. A space

	3. The image's intrinsic width in pixels (`480w`) $---$ note that this uses the `w` unit, not `px` as you might expect

		- An image's intrinsic size is its real size, which can be found by inspecting the image file on your computer

##### `sizes`

- This defines a set of media conditions (e.g. screen widths) and indicates what image size would be best to choose, when certain media conditions are true

- In this case, before each comma we write

	1. A media condition (`(max-width:600px)`) $---$ you'll learn more about these in the CSS topic, but for now let's just say that a media condition describes a possible state that the screen can be in.

		- In this case, we are saying "when the viewport width is 600 pixels or less"

	2. A space

	3. The sidth of the slot the image will fill when the media condition is true (`480px`)

> Note
>
> For the slot width, rather than providing an absolute width, you can alternatively provide a width (for example, `480px`) relative to the viewport (for example, `50vw`) $---$ but not a percentage. You may have noticed that the last slot width has no media condition (this is the default that is chosen when none of the media condition are true). The browser ignores everything after the first matching condition, so be careful how you order the media conditions

##### So with these attributes in place, the browser will:

1. Look at its device width

2. Work out which media condition in the `sizes` list is the first one to be true

3. Look at the slot size given to that media query

4. Load the image referenced in the `srcset` list that has the same size as the slot or, if there isn't one, the first image that is bigger than the chosen slot size

> Note
>
> When tesing this with a desktop browser, if the browser fails to load the narrower images when you've got its window set to the narrowest width, have a look at what the viewport is (you can approximate it by going into the browser's JavaScript console and typing in `document.querySelector('html').clientWidth`). When testing it with a mobile browser, you can use tools like Firefox's `about:debugging` page to inspect the page loaded on the mobile using desktop develop tools.
>
> To see which images were loaded, you can use Firefox DevTools's Network Monitor tab

- Older browsers that don't support these features will just ignore them.

- Instead, those browsers will go ahead and load the image referenced in the `src` attribute as normal

> Note
>
> In the `<head>` of the example linked above, you'll find the line `<meta name="viewport" content="width=device-width">`: this forces mobile browsers to adopt their real viewport width for loading web pages (some mobile browsers lie about their viewport width, and instead load pages at a larger viewport width then shrink the loaded page down, which is not very helpful for responsive images or design)

### Resolution switching: Same size, different resolutions

- If you're supporting multiple display resolutions, but everyone sees your image at the same real-world size on the screen, you can allow the browser to choose a appropriate resolution image by using `srcset` with x-descriptors and without `sizes`

- You can find an example of what this looks like in [srcset-resolutions.html](https://mdn.github.io/learning-area/html/multimedia-and-embedding/responsive-images/srcset-resolutions.html) (see also [source code](https://github.com/mdn/learning-area/blob/main/html/multimedia-and-embedding/responsive-images/srcset-resolutions.html))

```html
<img srcset="elva-fairy-320w.jpg,
             elva-fairy-480w.jpg 1.5x,
             elva-fairy-640w.jpg 2x"
     src="elva-fairy-640w.jpg"
     alt="Elva dressed as a fairy">
```

- In this example, the following CSS is applied to the image so that it will have a width of 320 pixels on the screen (also clalled CSS pixels)

```css
img {
  width: 320px;
}
```

- In this case, `sizes` is not needed $---$ the browser works out what resolution the display is that it is being shown on, and serves the most appropriate image referenced in the `srcset`

- So if the device accessing the page has a standard/low resolution display, with one device pixel representing each CSS pixel, the `elva-fairy-320w.jpg` image will be loaded (the 1x is implied, so you don't need to include it)

- If the device has a high resolution of two device pixels per CSS pixel or more, the `elva-fairy-640w.jpg` image will be loaded

### Art direction

- To recap, the art direction problem involves wanting to change the image displayed to suit different image display sizes

- The `<picture>` element allows us to implement just this kind of solution

- the `<picture>` element is a wrapper containing several `<source>` elements that provide different sources for the browser to choose from, followed by the all-important `<img>` element

- The code in [responsive.html](https://mdn.github.io/learning-area/html/multimedia-and-embedding/responsive-images/responsive.html) looks like so:

```html
<picture>
  <source media="(max-width: 799px)" srcset="elva-480w-close-portrait.jpg">
  <source media="(min-width: 800px)" srcset="elva-800w.jpg">
  <img src="elva-800w.jpg" alt="Chris standing up holding his daughter Elva">
</picture>
```

- The `<source>` element include a `media` attribute that conatains a media condition the first one that returns true will be displayed

- The `srcset` attributes contain the path to the image to display

	- `<source>` can take a `srcset` attribute with multiple images referenced, as well as a `sizes` attribute

- In all cases, you must provide an `<img>` element, with `src` and `alt`, right before `</picture>`, otherwise no images will appear

	- This provides a defulat case that will apply when none of the media conditions return true, and a fallback for browsers that don't dupport the `<picture>` element

> Note
>
> You should use the `media` attribute only in art direction scenario; when you do use `media, don't also offer media conditions within the `sizes` attribute

### Why can't we just do this using CSS or JavaScript?

- When the browser starts to load a page, it starts to download (preload) any images before the main parser has started to load and interpret the page's CSS and JavaScript

- That mechanism is useful in general for reducing page load times, but it is not helpful for responsive images $---$ hence the need to implement solutions like `srcset`

- For example, you couldn't load the `<img>` element, then detect the viewport width with JavaScript, and then dynamically change the source image to a smaller one if desired

- By then, the original image would already have been loaded, and you would load the small image as well, which is even worse in responsive image terms

### Use modern image formats boldly

- New image formats like WebP and AVIF can maintain a low file size and high quality at the same time

	- These formats now have relatively broad browser support but little "historical depth"

- `<picture>` lets us continue catering to older browsers. You can supply MIME types inside `type` attributes so the browser can immediately reject unsupported file types

```html
<picture>
  <source type="image/svg+xml" srcset="pyramid.svg">
  <source type="image/webp" srcset="pyramid.webp">
  <img src="pyramid.png" alt="regular pyramid built from four equilateral triangles">
</picture>
```

- Do not use the `media` attribute, unless you also need art direction

- In a `<source>` element, you can only refer to images of the type declared in `type`

- Use comma-separated lists with `srcset` and `sizes`, as needed
