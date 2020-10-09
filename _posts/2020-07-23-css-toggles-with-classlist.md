---
title:  "Code Challenge: CSS Toggles with `element.classList`"
toc: true
categories: Challenges
tags: featured
---
## Prerequisites
Research into the following areas may help with this exercise.
- [CSS basics](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/CSS_basics){:target="_blank"}
- [Class selectors](https://css-tricks.com/almanac/selectors/c/class/)
- [Javascript variables](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/Variables)
- [Introduction to Javascript events](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events)

## Objective
The goal for this exercise is to control CSS styles using the `classList` Javascript API. It will allow us to toggle (i.e. flip back-and-forth) a CSS class of our choosing on an element (or more) of our choosing. By the time we're finished, you should have a page that looks similar to this demo:

<p class="codepen" data-height="446" data-theme-id="light" data-default-tab="result" data-user="browsertherapy" data-slug-hash="jOWdRze" style="height: 446px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="CSS Toggle with Element.classList.toggle()">
  <span>See the Pen <a href="https://codepen.io/browsertherapy/pen/jOWdRze">
  CSS Toggle with Element.classList.toggle()</a> by Tony Grimes (<a href="https://codepen.io/browsertherapy">@browsertherapy</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

**Sandbox environments**: [Codepen.io](https://www.codepen.io){:target="_blank"} is a handy tool (one of many) that helps you code directly in the browser.
{:.notice--info}

## Planning it out
With this goal in mind, we will focus on the following objectives, starting with our HTML, then the CSS and finally the Javascript:

1. Create and position a button and circle using [Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/).
2. Create `button` and `circle` Javascript element variables with [`element.querySelector()`](#Finding_the_first_element_matching_a_classhttps://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector).
3. Add a `click` handler for our button using [`addEventListener()`](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events#addEventListener_and_removeEventListener).
4. Toggle a CSS class with [`element.classList.toggle()`](https://developer.mozilla.org/en-US/docs/Web/API/Element/classList).

## Objective 1: Create and position a `button` and circle using Flexbox

### Objective 1a
As most things Web, we need some HTML content to play with. Eventually, the colour of the circle will change back-and-forth (i.e. toggle) each time the `button` is clicked.

```html
<!-- HTML is for Content -->
<div class="circle"></div>
<button>Toggle</button>
```

### Objective 1b
Our `div` element needs a little help being a circle. This will be the element that will flip back-and-forth when our button is clicked.

**Don't forget**: By default, a block-level element is as wide as its parent and has no height if empty. We will explicitly set our `width` and `height` to whip our `div` into (an eventually circular) shape.
{: .notice--info}

```css
/* CSS is for Presentation */

.circle {
  /* make it square */
  width: 30vmin;
  height: 30vmin;

  /* make it visible */
  border: 1px solid grey;

  /* make it circular */
  border-radius: 50%;
}
```

### Objective 1c
Position page elements in the center of the viewport. There are more elegant ways to do this but we've written this for clarity (hopefully). We're using the `body` element as our Flex container to simplify our HTML.

**Don't forget**: The `body` element is much like a normal block-level element: it will only be as tall as the content it contains. It needs to be as tall as the viewport in order for its items to be centered on the page so we explicitly set its height to `100vh` (100% of the viewport, in theory).
{: .notice--info}

```css
body {
  /* Make the body the height of the viewport. This is needed to give Flexbox room to operate. */
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

### Objective 1d
One last bit of CSS: we need a class to toggle with Javascript! In the next steps will hook up our button so that it will toggle this class so that the circle will alternate colours (in this case, between `rebeccapurple` and the default: `transparent`)

```css
/* Any element with a class of .fancy will have a (rebecca)purple background. */
.fancy {
  background: rebeccapurple;
}
```

## Objective 2: Create `button` and `circle` JS element variables with `element.querySelector()`
`document.querySelector()` is a popular way to assign an HTML element to a JS variable. It accepts any valid CSS selector and will return the first DOM element it matches.

```js
const circle = document.querySelector('.circle');
const button = document.querySelector('button');
```

**Tool-time**: From here on in, you'll be relying on your browser's Web Console to troubleshoot Javascript issues. How to open the Web Console on [FireFox](https://developer.mozilla.org/en-US/docs/Tools/Web_Console/Opening_the_Web_Console){:target="_blank"} and [Chrome](https://developers.google.com/web/tools/chrome-devtools/console){:target="_blank"}.
{:.notice--info}

**Bug hunt**: If you see an error like `button is not defined` or similar, chances are there's a problem with the selector you're passing to `querySelector()`.
{: .notice--warning}

## Objective 3: Add a `click` handler for our `button` using `addEventListener()`
Now that we have a button variable, let's do something with it. Javascript is [all about events](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events) like clicks/touches, mouse/finger movement, form submission, etc. We can tell the browser to run code when a particular event happens, like the click of our button. We use the `addEventListener()` method (all HTML elements have one) to attach a `click handler` to our button.

```js
button.addEventListener('click', function(){
  
  // Objective 4 code here. It will be invoked every time the button is clicked.
  
});
```

**Event reference**: Bored of clicks? There's a list of all available events in the [MDN Event Reference](https://developer.mozilla.org/en-US/docs/Web/Events){:target="_blank"}.
{:.notice--info}

## Objective 4: Toggle a CSS class with `element.classList.toggle()`
When you add a list of classes to an HTML element (using the `class` attribute), the browser stores them in a list in memory. Normally, we add classes by typing some HTML but we can also use a useful Javascript API called `classList`. It allows us to add, remove, toggle and replace class names programmatically.

**More about classList**: The MDN [documentation on `element.classList`](https://developer.mozilla.org/en-US/docs/Web/API/Element/classList) is a little sparse but a quick skim of the example code will give you a good idea of what it does: it adds/removes/toggles/replaces the class names of HTML elements. Very handy!
{: .notice--info}

```js
button.addEventListener('click', function(){
  
  // Each time the button is clicked: if the `circle` element has a class of .fancy, remove it. If .fancy is already absent, add it.
  circle.classList.toggle('fancy');
  
});
```

**What's the point?** If you're looking for a real work application for a CSS toggle, look no further than the mighty [hamburger menu](https://www.google.com/search?q=css+hamburger+menus)!
{: .notice--info}

## Cleaning up our code: Making things pretty(ish)
Functionality isn't everything. Browser default `button` styling suucks, so let's make it more "buttony" (technical web development term).

```css
button {
  /* Make the button bigger, and more... buttony */
  padding: .5rem 1rem;
  margin: 1rem;
  border-radius: 1rem;
  
  /* Try to make boring fonts look less boring. */
  font-size: 1.5rem;
  font-family: MS Sans Serif, Geneva, sans-serif;
  font-variant: small-caps;
  
  /* By default, buttons don't get the pointy hand when you hover. */
  cursor: pointer;
}
```

## Fly high, Icarus
Now that you've got a basic understanding of how CSS toggles work, try adding two to the [Tissue Contrast Illusion exercise](http://browsertherapy.com/challenges/tissue-contrast/): one to toggle `.split-bg` and another to hide/show the transparent image (hint: this might call for a new class named `.hidden`).

Good luck!

