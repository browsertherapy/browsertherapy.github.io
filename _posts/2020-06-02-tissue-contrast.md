---
title:  "Coding Challenge: Tissue Contrast Illusion"
excerpt: "In this exercise, we will replicate the Tissue Contrast Illusion by Arthur Shapiro."
toc: true
categories: Challenges
tags: featured
---
{% include video id="9zMDmtWzBN8" provider="youtube" %}
Source: [Curiosity Stream](https://curiositystream.com/video/1259/brightness-and-contrast){:target="_blank"}

## Overview
The goal of this exercise is to replicate the Tissue Contrast Illusion in the browser. We've broken the problem into logical steps and provided (hidden) sample code if you get stuck. *But*, keep in mind there are many (and possibly better) ways to solve this problem.

## Prerequisites
This activity should be approachable for beginners but some understanding of the following technologies will be beneficial: [HTML basics](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/HTML_basics){:target="_blank"}, [CSS basics](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/CSS_basics){:target="_blank"} and the [CSS box model](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/The_box_model){:target="_blank"}.

## Topics covered
The sample code (below) further incorporates the following concepts and technologies: [Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/){:target="_blank"}, [viewport units](https://www.youtube.com/watch?v=_sgF8I-Q1Gs){:target="_blank"}, [linear gradients](https://css-tricks.com/css3-gradients/){:target="_blank"}, [transparent](https://css-tricks.com/almanac/properties/o/opacity/){:target="_blank"} [images](https://www.youtube.com/watch?v=33IinMVJf-M){:target="_blank"} and [absolute positioning](https://youtu.be/P6UgYq3J3Qs){:target="_blank"}.

## Planning it out
Let's break down this exercise according to how elements need to overlap:

1. Two identical grey circles
2. **Under the circles**: split-colour background
3. **On top of the circles**: semi-transparent image.

These objectives are further broken down below. Remember: sample code is provided in case you get stuck but there are many ways to achieve the desired results.

### Sample code
{:.no_toc}

<details markdown="1">
  <summary>HTML Structure</summary>
```html
<!-- The parent-child relationship of the `container` and `item`s is crucial to how Flexbox operates later. -->
<main class="container split-bg">
  <div class="item circle"></div>
  <div class="item circle"></div>
</main>
<!-- Placed at the end so that it sits on top when positioned later. -->
<div class="image"></div>
```
</details>

## Objective 1: Create and position two grey circles
<figure style="width: 500px" class="align-center">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/illusions/tissue-step-1.png" alt="Two grey patches">
  <figcaption>Two identical grey (50% black) patches, each centered in their half of the viewport (i.e. the viewable portion of a web page).</figcaption>
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

**Coming from print?**: Check out this excellent video by Jen Simmons: [Designing for a Viewport](https://www.youtube.com/watch?v=QY3lTBZnJmE){:target="_blank"}.
{:.notice--info}

**Pro tip**: Viewport units are amazing for global layout but try `em/rem` units for smaller page elements such as [cards](https://www.google.com/search?q=ux+card+pattern){:target="_blank"}).
{:.notice--info}

</details>
<details markdown="1">
  <summary>Each circle, centred in their half of the viewport</summary>

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

**Getting fancy**: Check out the [Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/){:target="_blank"} for more ways to control your items with properties like `justify-content` and `align-items`.
{:.notice--info}

**Pro tip**: Flexbox is very handy for laying out [navigation menus](https://www.google.com/search?q=flexbox+navbar){:target="_blank"}, [hero sections](https://www.google.com/search?q=flexbox+hero+sections){:target="_blank"} and [cards](https://www.google.com/search?q=flexbox+cards){:target="_blank"}.
{:.notice--info}
</details>

## Objective 2: Add a split-colour background
<figure style="width: 500px" class="align-center">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/illusions/tissue-step-2.png" alt="Two grey patches">
  <figcaption>Two identical grey patches on a split-colour (very light and very dark) background. Notice the left circle appears slightly darker than the one on the right.</figcaption>
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

**Creative text effects**: [Mandy Michael](https://www.youtube.com/watch?v=lKRdfw4xcGo){:target="_blank"} uses this gradient technique in many of [her](https://codepen.io/mandymichael/pen/mNPvKo){:target="_blank"} [amazing](https://codepen.io/mandymichael/pen/MpqJMa){:target="_blank"} [designs](https://codepen.io/mandymichael/pen/peZgxW){:target="_blank"}.
{:.notice--info}
</details>

## Objective 3: Overlap viewport with a semi-transparent image
<figure style="width: 500px" class="align-center">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/illusions/tissue-step-3.png" alt="Two grey patches">
  <figcaption>Ovelapping a semi-transparent image over top of the viewport enhances the effect of the illusion.</figcaption>
</figure> 

### Sample code
{:.no_toc}

<details markdown="1">
  <summary>Add a viewport-sized CSS image</summary>

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

**Extra Points**: Absolute positioning is the classic method. Try using a newer technique: [explicit item placement with CSS Grid](https://youtu.be/EashgVqboWo){:target="_blank"}. Each have their advantages depending on your situation.
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

## Cleaning things up with resets
A "reset" is CSS we add to change default browser behaviour. 

For example, you might see an irritating horizontal (and/or vertical) scroll bar in your browser window. This is because most browsers add a default margin to their body tag. When we set the `width` and `height` of an element to fill the viewport, this `margin` is added to the final size of the page (hence, a scroll bar).

Below are two resets that most professional developers will use in every project.

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
  /* make size calculations take 'padding' and 'border' into account */
  box-sizing: border-box;
}
```
**Optional**: `box-sizing` doesn't apply to the sample code as written but elements with added `padding` and `border` might benefit from this handy reset.
{:.notice--info}
</details>
## Mobile Considerations
Sure, this illusion seems to work on the laptop but what if you want to text your codepen link to your mom? Try adding a media query that declares the following CSS when the viewport is in the portrait orientation:

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
**One nail, two hammers**: Using `display: grid` instead of `flex-direction: column` produces the same results. Why? Because CSS.
{:.notice--info}
</details>

## Final Demo


<p class="codepen" data-height="265" data-theme-id="light" data-default-tab="result" data-user="funwithcodeyyc" data-slug-hash="MWKaode" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Exercise Spoilers: Tissue Contrast Illusion">
  <span>See the Pen <a href="https://codepen.io/funwithcodeyyc/pen/MWKaode">
  Exercise Spoilers: Tissue Contrast Illusion</a> by Tony Grimes (<a href="https://codepen.io/funwithcodeyyc">@funwithcodeyyc</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>