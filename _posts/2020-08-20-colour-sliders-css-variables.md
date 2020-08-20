---
title:  "Code Challenge: Colour sliders with JS, HSL and CSS Variables"
toc: true
categories: Challenges
tags: featured
---
## Prerequisites
Research into the following areas may help with this exercise.
- [HTML range sliders](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/range)
- [CSS variables](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties)
- [HSL colour](https://css-tricks.com/yay-for-hsla/)
- [Javascript variables](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/Variables)
- [Introduction to Javascript events](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events)

## Exercise Objective
The goal for this exercise is to control page presentation using CSS Variables. We will create a slider that will change the hue of multiple colors with one CSS variable. By the time we're finished, you should have a page that looks similar to this demo:

<p class="codepen" data-height="450" data-theme-id="dark" data-default-tab="result" data-user="browsertherapy" data-slug-hash="dyMGgaV" style="height: 450px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Colour Slider with CSS Variables and HSL">
  <span>See the Pen <a href="https://codepen.io/browsertherapy/pen/dyMGgaV">
  Colour Slider with CSS Variables and HSL</a> by Tony Grimes (<a href="https://codepen.io/browsertherapy">@browsertherapy</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

**Sandbox environments**: [Codepen.io](https://www.codepen.io){:target="_blank"} is a handy tool (one of many) that helps you code directly in the browser.
{:.notice--info}

## Planning it out
With this goal in mind, we will focus on the following objectives, starting with our HTML, then the CSS and finally the Javascript:

1. Create an HTML heading, circle and range input (to be our colour slider).
2. Create a CSS variable for the hue angle of our HSL colours.
3. Make a circle. Apply a saturated background colour to the circle using the `--hue` variable.
4. Apply a dark text colour to the heading using the `--hue` variable.
5. Create `root` and `slider` Javascript element variables.
6. Add a `input` event handler to the slider.
7. Set the `--hue` CSS variable to the current value of the slider.

## Objective 1: Create an HTML heading, circle and slider
As most things Web, we need some HTML content to play with. Eventually, the colour hue of the heading and circle will change based on the slider position.

```html
<h1>Yay for CSS Variables!</h1>
<div class="circle"></div>
<input type="range" min="0" max="360">
```

## Objective 2: Create a `--hue` CSS variable
The `:root` pseudo-selector is the same as an `html` selector, but with higher specificity. Most developers attach CSS variables to `:root` by convention.

```css
:root {
  --hue: 180;
}
```

CSS Variables are quirky but amazing. Check out this 50 minute video for the nitty gritty: [CSS Variable Secrets](https://youtu.be/UQRSaG1hQ20) by Lea Verou.
{: .notice--info}

## Objective 3: Set the background colour of a circle using `--hue`
Our `div` element needs a little help being a circle. We will define a saturated background colour using the `--hue` variable we created. Any colour we define with this variable will eventually be editable using the slider.

```css
.circle {
  /* make it square */
  width: 40vmin;
  height: 40vmin;
  
  /* make it visible */
  background: hsl(var(--hue), 100%, 50%);

  /* make it circular */
  border-radius: 50%; 
}
```

**Don't forget**: By default, a block-level element is as wide as its parent and has no height if empty. We will explicitly set our `width` and `height` to whip our `div` into (an eventually circular) shape.
{: .notice--info}

## Objective 4: Apply a dark text colour using `--hue`
This is where HSL helps us out. Although our circle and heading colours are defined with the same hue, we're making the heading a darker version of that hue by setting a lightness value of `30%` (instead of the circle lightness of `50%` ).

```css
h1 {
  color: hsl(var(--hue), 100%, 30%);
}
```

## Objective 5: Create `root` and `slider` JS element variables with `element.querySelector()`
`document.querySelector()` is a popular way to assign an HTML element to a JS variable. It accepts any valid CSS selector and will return the first DOM element it matches.

**Terminology Warning:** Don't confuse CSS variables with Javascript variables! The official term for a CSS variable is *CSS Custom Property*.
{: .notice--warning}

```js
const root = document.querySelector(':root');
const slider = document.querySelector('input');
```

**Tool-time**: From here on in, you'll be relying on your browser's Web Console to troubleshoot Javascript issues. How to open the Web Console on [FireFox](https://developer.mozilla.org/en-US/docs/Tools/Web_Console/Opening_the_Web_Console){:target="_blank"} and [Chrome](https://developers.google.com/web/tools/chrome-devtools/console){:target="_blank"}.
{:.notice--info}

**Bug hunt**: If you see an error like `slider is not defined` or similar, chances are there's a problem with the selector you're passing to `querySelector()`.
{: .notice--warning}

## Objective 6: Add an `input` handler for our `slider` using `addEventListener()`
Now that we have a slider variable, let's do something with it. Javascript is [all about events](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events) like clicks/touches, mouse/finger movement, form submission, etc. We can tell the browser to run code when a particular event happens, like the click of our button. We use the `addEventListener()` method (all HTML elements have one) to attach a handler to our button.

```js
slider.addEventListener('input', function(){
  
  // Objective 7 code here. It will be invoked every time the value of slider is changed.
  
});
```

**Event reference**: The [`input`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/input_event) event fires when the value of an `input`, `select` or `textarea` is changed. There's a list of all available events in the [MDN Event Reference](https://developer.mozilla.org/en-US/docs/Web/Events){:target="_blank"}.
{:.notice--info}

## Objective 7: Set `--hue` value to the current value of the slider
Now we take advantage of the `element.style.setProperty()` method. This is allows us to directly update the CSS property value of an HTML element.

```js
button.addEventListener('input', function(){
  
  root.style.setProperty("--hue", slider.value);
  
});
```

## Making things pretty(ish)
Functionality isn't everything. The following code will centre our elements in the middle of the viewport

```css
/* The page body will be our Flex container. */
body {
  /* Get rid of pesky scroll bars */
  margin: 0;
  
  /* Make the body the height of the viewport. This is needed to centre the button. */
  height: 100vh;
  
  /* Center the button in the middle of the viewport. */
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
```

**Getting fancy**: Check out the [Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/){:target="_blank"} for a handy, visual reference for everything Flexbox.
{:.notice--info}

This code tweaks our fonts and spacing to make everything less ugly, relatively.

```css
h1 {
  font-size: 1.5rem;
  font-family: MS Sans Serif, Geneva, sans-serif;
  font-variant: small-caps;
  text-align: center;
}

.circle {
  margin-bottom: 1em;
}
```

## Fly high, Icarus
You should now have a basic understanding of how page presentation can be controlled with CSS variables. Try extending your knowledge by adding more CSS variables (and form controls, if you'd like) or by finding more uses for `--hue`.

What other CSS properties accept an angle as a parameter? What else can our slider control with this one CSS variable?

Good luck!

