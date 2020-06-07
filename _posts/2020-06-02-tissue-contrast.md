---
title:  "Coding Challenge: Tissue Contrast Illusion"
excerpt: "This is the excerpt"
---
## Exploring the Tissue Contrast Illusion
{% include video id="9zMDmtWzBN8" provider="youtube" %}

## Relevant Resources
### Cheatsheets
- Box Model
- Display Modes
- CSS images
- Flexbox
- Positioning

## Spoilers
### Sample HTML
```html
<main class="container bg">
  <div class="item circle"></div>
  <div class="item circle"></div>
</main>
<div class="image"></div>
```

### Two grey circles
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
### Equally spaced flex items, centred in the viewport
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

### Split-colour background

```css
.container {
  /* note: only the final `background` declaration is used; the others are included for clarity */

  /* basic gradient; default gradient line direction: bottom to top (0deg)  */
  background: linear-gradient(white, black);

  /* change default direction: left to right (90deg) */
  background: linear-gradient(90deg, white, black);

  /* hide gradient area by adding identical colour stops */
  background: linear-gradient(90deg, white 50%, black 50%);
}
```

### Overlapped image
```css
.image {
  /* create a new block formatting context and enable `top` and `left` */
  position: absolute;

  /* explicitly move top-left corner of image to top-left corner of <body> */
  top: 0;
  left: 0;
}
```

### Viewport-sized image
```css
.image {
  /* explicitly set element size to viewport */
  width: 100vw;
  height: 100vh;
  
  /* add full-size, centered background image to element */
  background-image: url('https://picsum.photos/500/500');
  background-size: contain;
  background-position: center;
}
```

### Semi-transparency
```css
.image {
  /* set element opacity to 50% */
  opacity: 0.5;
}
```