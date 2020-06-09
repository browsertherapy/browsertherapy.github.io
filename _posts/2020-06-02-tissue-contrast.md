---
title:  "Code Challenge: Tissue Contrast Illusion"
excerpt: "This is the excerpt"
---
In this exercise, we will replicate (as closely as possible) the Tissue Contrast Illusion as shown by Arthur Shapiro below ([source](https://curiositystream.com/video/1259/brightness-and-contrast)). The images in the spoiler code use the [Lorem Picsum](https://picsum.photos/) image service (they're awesome!) to respect copyright 'n stuff.

{% include video id="9zMDmtWzBN8" provider="youtube" %}

## Topics covered
- making a circle with the [CSS Box Model](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Introduction_to_the_CSS_box_model)
- vertically centering elements with [Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
- defining background colour and split-colour backgrounds ([example](https://codepen.io/mandymichael/pen/mNPvKo))
- placing a CSS image with [Lorem Picsum](https://picsum.photos/)
- overlapping elements with [absolute positioning](https://youtu.be/P6UgYq3J3Qs)
- controlling [opacity](https://developer.mozilla.org/en-US/docs/Web/CSS/opacity)

## Objectives 
### 1. Create and position two grey circles
<figure style="width: 500px" class="align-center">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/illusions/tissue-step-1.png" alt="Two grey patches">
  <figcaption>Two identical grey patches, equally spaced in the centre of the viewport.</figcaption>
</figure> 

Creating **circles** using CSS has been straight forward for for awhile now. Three box model declarations ought to do it. 

Surprisingly, centering elements in the viewport was pretty painful until [Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) saved us around 2012 (the end of the world for float columns). The spoilers do this with only three declarations. Praise the browser deities!

### 2. Add a split-colour background
<figure style="width: 500px" class="align-center">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/illusions/tissue-step-2.png" alt="Two grey patches">
  <figcaption>Two identical grey patches on a split-colour background. Notice the left circle appears slightly darker than the one on the right.</figcaption>
</figure> 

At first, creating a split background may seem complicated. Luckily, there is a simple way to trick a gradient into creating the desired effect.

### 3. Overlap viewport with a semi-transparent image
<figure style="width: 500px" class="align-center">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/illusions/tissue-step-3.png" alt="Two grey patches">
  <figcaption>Ovelapping a semi-transparent image over top of the background and circles greatly enhances the effect of the illusion.</figcaption>
</figure> 

This is the most involved part of the illusion. [Lorem Picsum](https://picsum.photos/) is a convenient image service that simplifies things. Then, things get more involved:
1. Will you place the image using HTML or CSS? Both are valid but the spoilers use CSS.
2. How will you overlap this image? The classic option is absolute positioning which we use in the spoilers. Feeling fancy? Try using [explicit item placement with CSS Grid](https://youtu.be/EashgVqboWo)!

## Spoilers
<details markdown="1">
  <summary>Sample HTML</summary>
```html
<main class="container bg">
  <div class="item circle"></div>
  <div class="item circle"></div>
</main>
<div class="image"></div>
```
</details>

<details markdown="1">
  <summary>Two grey circles</summary>

```css
.circle {
  /* make it visible */
  background: grey;

  /* make it square */
  width: 30vmin;
  height: 30vmin;

  /* make it circular */
  border-radius: 50%;
}
```
</details>
<details markdown="1">
  <summary>Equally spaced flex items, centred in the viewport</summary>

```css
.container {
  /* change default behaviour of `margin: auto` below */
  display: flex;

  /* explicitly set height to viewport; `margin: auto` needs room to work */
  height: 100vh;
}

.item {
  /* equally distribute left over margin among flex items */
  margin: auto;
}
```
</details>

<details markdown="1">
  <summary>Split-colour background</summary>

```css
.container {
  /* note: only the final `background` declaration is used; the others are included for clarity and are overridden */

  /* basic gradient; default gradient line direction: bottom to top (0deg)  */
  background: linear-gradient(white, black);

  /* change default direction: left to right (90deg) */
  background: linear-gradient(90deg, white, black);

  /* hide gradient area by adding identical colour stops */
  background: linear-gradient(90deg, white 50%, black 50%);
}
```
</details>
<details markdown="1">
  <summary>Overlapped image</summary>

```css
.image {
  /* create a new block formatting context and enable `top` and `left` */
  position: absolute;

  /* explicitly move top-left corner of image to top-left corner of <body> */
  top: 0;
  left: 0;
}
```
</details>
<details markdown="1">
  <summary>Viewport-sized image</summary>

```css
.image {
  /* explicitly set element size to viewport */
  width: 100vw;
  height: 100vh;
  
  /* add full-size, centered background image to element */
  background-image: url('https://picsum.photos/500/500');
  background-size: cover;
  background-position: center;
}
```
</details>
<details markdown="1">
  <summary>Semi-transparency</summary>

```css
.image {
  /* set element opacity to 50% */
  opacity: 0.5;
}
```
</details>
<details markdown="1">
  <summary>Final Demo</summary>

<p class="codepen" data-height="265" data-theme-id="light" data-default-tab="result" data-user="funwithcodeyyc" data-slug-hash="MWKaode" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Exercise Spoilers: Tissue Contrast Illusion">
  <span>See the Pen <a href="https://codepen.io/funwithcodeyyc/pen/MWKaode">
  Exercise Spoilers: Tissue Contrast Illusion</a> by Tony Grimes (<a href="https://codepen.io/funwithcodeyyc">@funwithcodeyyc</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
</details>