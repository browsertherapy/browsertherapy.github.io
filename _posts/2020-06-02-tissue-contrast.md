---
title:  "Coding Challenge: Tissue Contrast Illusion"
excerpt: "In this exercise, we will replicate the Tissue Contrast Illusion as shown by Arthur Shapiro."
toc: true
---
## Overview
In this exercise, we will replicate the Tissue Contrast Illusion as shown by Arthur Shapiro. The images in the spoiler code use the [Lorem Picsum](https://picsum.photos/) image service (they're awesome!) to respect copyright 'n stuff.

{% include video id="9zMDmtWzBN8" provider="youtube" %}
Source: [Curiosity Stream](https://curiositystream.com/video/1259/brightness-and-contrast)

## Topics covered
- making a circle with the [CSS Box Model](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Introduction_to_the_CSS_box_model)
- vertically centering elements with [Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
- defining `background-colour` and split-colour backgrounds using `linear-gradient()` ([example](https://codepen.io/mandymichael/pen/mNPvKo))
- placing a CSS image with [Lorem Picsum](https://picsum.photos/)
- overlapping elements with [absolute positioning](https://youtu.be/P6UgYq3J3Qs)
- controlling [opacity](https://developer.mozilla.org/en-US/docs/Web/CSS/opacity)

## Planning it out
We'll break down this exercise according to how elements need to overlap:

1. Two identical grey circles
2. Under the circles: split-colour background
3. On top of the circles: semi-transparent image.

Most of the objectives can be solved with some clever use of backgrounds with a splash of Flexbox and absolute positioning. 

### Sample code
{:.no_toc}

<details markdown="1">
  <summary>HTML Structure</summary>
```html
<main class="container split-bg">
  <div class="item circle"></div>
  <div class="item circle"></div>
</main>
<div class="image"></div>
```
</details>

## Objective 1: Create and position two grey circles
<figure style="width: 500px" class="align-center">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/illusions/tissue-step-1.png" alt="Two grey patches">
  <figcaption>Two identical grey patches, equally spaced in the centre of the viewport.</figcaption>
</figure> 

### Sample code
{:.no_toc}

<details markdown="1">
  <summary>Two grey circles</summary>

```css
.circle {
  /* make it square */
  width: 30vmin;
  height: 30vmin;

  /* make it visible */
  background: grey;

  /* make it circular */
  border-radius: 50%;
}
```

**Video**: New to Viewport units? Check out this excellent summary by Jen Simmons: [Introduction to Viewport Units](https://youtu.be/_sgF8I-Q1Gs){:target="_blank"}.
{:.notice--info}

**Pro tip**: Viewport units are amazing for global layout but try `em/rem` units for smaller layouts such as [cards](https://www.google.com/search?q=ux+card+pattern){:target="_blank"}).
{:.notice--info}

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
  /* equally distribute extra horizontal/vertical space among flex items; block elements only do this for `margin-left` and `margin-right` */
  margin: auto;
}
```

**Pro tip**: Going to use more Flexbox? Have the [Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/){:target="_blank"} open in another tab. It has pictures!
{:.notice--info}
</details>

## Objective 2: Add a split-colour background
<figure style="width: 500px" class="align-center">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/illusions/tissue-step-2.png" alt="Two grey patches">
  <figcaption>Two identical grey patches on a split-colour background. Notice the left circle appears slightly darker than the one on the right.</figcaption>
</figure> 

### Sample code
{:.no_toc}

<details markdown="1">
  <summary>Add a split-colour background</summary>

```css
.split-bg {
  /* note: the final `background` declaration overrides the others,
  which are included for clarity but can safely be ignored */

  /* basic gradient; default gradient line direction: bottom to top (0deg)  */
  background: linear-gradient(white, black);

  /* change default direction: left to right (90deg) */
  background: linear-gradient(90deg, white, black);

  /* hide gradient area by adding identical colour stops */
  background: linear-gradient(90deg, white 50%, black 50%);
}
```

**Article**: Everything you ever wanted to know about [CSS Gradients](https://css-tricks.com/css3-gradients/){:target="_blank"}.
{:.notice--info}
</details>

## Objective 3: Overlap viewport with a semi-transparent image
<figure style="width: 500px" class="align-center">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/illusions/tissue-step-3.png" alt="Two grey patches">
  <figcaption>Ovelapping a semi-transparent image over top of the background and circles greatly enhances the effect of the illusion.</figcaption>
</figure> 

### Sample code
{:.no_toc}

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

**Alternate Solution**: Another valid option is to use an HTML image using an `img` element with the `object-fit` property.
{:.notice--info}
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

**Extra Points**: Absolute positioning is the classic method. Step into the future: [explicit item placement with CSS Grid](https://youtu.be/EashgVqboWo){:target="_blank"}
{:.notice--info}

</details>
<details markdown="1">
  <summary>Make the image semi-transparent</summary>

```css
.image {
  /* set element opacity to 50% */
  opacity: 0.5;
}
```
**More Transparency**: `opacity` isn't the only way to create transparency in CSS. Gradients accept `transparent` as a colour keyword and you can add an alpha channel to `rgb()` or `hsl()` when defining a colour.
{:.notice--info}

</details>

## Cleaning things up
You might see an irritating horizontal (and vertical) scroll bar in your browser window. This is because most browsers add a default margin to their body tag. Let's remove that.

### Sample code
{:.no_toc}

<details markdown="1">
  <summary>Reset default margins</summary>

```css
body {
  /* remove pesky scroll bars */
  margin: 0;
}
```
</details>
<details markdown="1">
  <summary>Reset default `box-sizing`</summary>
```css
* {
  /* make element width calculations a little more intuitive */
  box-sizing: border-box;
}
```
**Optional**: `box-sizing` doesn't apply to the sample code as written but elements with `padding` might benefit from this handy reset.
{:.notice--info}
</details>
## Mobile Considerations
Sure, this illusion seems to work on the laptop but it doesn't look the best on mobile. Try adding a media query that declares the following when the viewport is in the portrait orientation:

1. Place the circles vertically so one is above the other;
2. Change the gradient line direction to run from top to bottom.

### Sample code
{:.no_toc}

<details markdown="1">
  <summary>Add support for portrait orientation</summary>

```css
@media (orientation: portrait) {
  /* Apply these styles when the screen is in 'portrait' orientation */
  .container {
    /* place circles in an up/down orientation */
    flex-direction: column;
    
    /* change the direction of the split-colour background to match the new direction */
    background: linear-gradient(180deg, white 50%, black 50%);
  }
}
```
**One nail, two hammers**: It turns out that using `display: grid` instead of `flex-direction: column` produces the same results. Why? 'cuz CSS.
{:.notice--info}
</details>

## Final Demo
<p class="codepen" data-height="265" data-theme-id="light" data-default-tab="result" data-user="funwithcodeyyc" data-slug-hash="MWKaode" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Exercise Spoilers: Tissue Contrast Illusion">
  <span>See the Pen <a href="https://codepen.io/funwithcodeyyc/pen/MWKaode">
  Exercise Spoilers: Tissue Contrast Illusion</a> by Tony Grimes (<a href="https://codepen.io/funwithcodeyyc">@funwithcodeyyc</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>