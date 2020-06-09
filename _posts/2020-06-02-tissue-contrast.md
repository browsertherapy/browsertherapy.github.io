---
title:  "Code Challenge: Tissue Contrast Illusion"
excerpt: "In this exercise, we will replicate the Tissue Contrast Illusion as shown by Arthur Shapiro."
---
In this exercise, we will replicate the Tissue Contrast Illusion as shown by Arthur Shapiro below ([source](https://curiositystream.com/video/1259/brightness-and-contrast)). The images in the spoiler code use the [Lorem Picsum](https://picsum.photos/) image service (they're awesome!) to respect copyright 'n stuff.

{% include video id="9zMDmtWzBN8" provider="youtube" %}

## Topics covered
- making a circle with the [CSS Box Model](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Introduction_to_the_CSS_box_model)
- vertically centering elements with [Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
- defining background colour and split-colour backgrounds ([example](https://codepen.io/mandymichael/pen/mNPvKo))
- placing a CSS image with [Lorem Picsum](https://picsum.photos/)
- overlapping elements with [absolute positioning](https://youtu.be/P6UgYq3J3Qs)
- controlling [opacity](https://developer.mozilla.org/en-US/docs/Web/CSS/opacity)

## Objective 1: Create and position two grey circles
<figure style="width: 500px" class="align-center">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/illusions/tissue-step-1.png" alt="Two grey patches">
  <figcaption>Two identical grey patches, equally spaced in the centre of the viewport.</figcaption>
</figure> 

### Spoilers

<details markdown="1">
  <summary>Sample HTML</summary>
```html
<main class="container split-bg">
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

## Objective 2: Add a split-colour background
<figure style="width: 500px" class="align-center">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/illusions/tissue-step-2.png" alt="Two grey patches">
  <figcaption>Two identical grey patches on a split-colour background. Notice the left circle appears slightly darker than the one on the right.</figcaption>
</figure> 

### Spoilers
<details markdown="1">
  <summary>Add a split-colour background</summary>

```css
.split-bg {
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

## Objective 3: Overlap viewport with a semi-transparent image
<figure style="width: 500px" class="align-center">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/illusions/tissue-step-3.png" alt="Two grey patches">
  <figcaption>Ovelapping a semi-transparent image over top of the background and circles greatly enhances the effect of the illusion.</figcaption>
</figure> 

### Spoilers
<details markdown="1">
  <summary>Add a viewport-sized image</summary>

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
  <summary>Overlap the image</summary>

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
  <summary>Make the image semi-transparent</summary>

```css
.image {
  /* set element opacity to 50% */
  opacity: 0.5;
}
```
</details>

## Cleaning things up
You might see an irritating horizontal (and vertical) scroll bar in your browser window. This is because most browsers add a default margin to their body tag. Let's remove that.

### Spoilers
<details markdown="1">
  <summary>Reset default browser margins</summary>

```css
body {
  /* remove pesky scroll bars */
  margin: 0;
}
```
</details>

## Mobile Considerations
Sure, this illusion seems to work on the laptop but it doesn't look the best on mobile. Try adding a media query that declares the following when the viewport is in the portrait orientation:

1. Place the circles vertically so one is above the other;
2. Change the gradient line direction to run from top to bottom.

### Spoilers
<details markdown="1">
  <summary>Add support for portrait orientation</summary>

```css
@media (orientation: portrait) {
  /* Apply these styles when the screen is in 'portrait' orientation */
  .container {
    /* place circles in an up/down orientation */
    flex-direction: column;
    
    /* change the direction of the split-colour background to match */
    background: linear-gradient(180deg, white 50%, black 50%);
  }
}
```
</details>

## Final Demo
<p class="codepen" data-height="265" data-theme-id="light" data-default-tab="result" data-user="funwithcodeyyc" data-slug-hash="MWKaode" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Exercise Spoilers: Tissue Contrast Illusion">
  <span>See the Pen <a href="https://codepen.io/funwithcodeyyc/pen/MWKaode">
  Exercise Spoilers: Tissue Contrast Illusion</a> by Tony Grimes (<a href="https://codepen.io/funwithcodeyyc">@funwithcodeyyc</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>