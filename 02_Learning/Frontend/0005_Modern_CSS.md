---
tags:
  - css
  - frontend
---
# Scroll snap

```css
.reel {
	--gap: 1rem;
	display: grid;
	gap: var(--gap);
	grid-auto-flow: column; /* Same as **flex-direction: column;** */
	grid-auto-columns: calc(50% - var(--gap) / 2);
	overflow-x: scroll;
	scroll-snap-type: x mandatory;
	scroll-padding: var(--gap);
}

.reel > * {
	scroll-snap-align: start;
}
```

# Grid-template-areas

It is a easier way to work with grid in css. It simplifies the way we create templates with the auto columns and rows inside of grid and working with media queries is much more easier than the auto columns and rows.


```css
.testimonial-grid {
  display: grid;
  gap: 1.5rem;
  grid-auto-columns: 1fr;
  grid-template-areas:
   'one'
   'two'
   'three'
   'four'
   'five';

  padding-block: 2rem;
  width: min(95%, 70rem);
  margin-inline: auto;
}

.testimonial {
  font-size: var(--fs-400);
  padding: 2rem;
  border-radius: 0.5rem;
  box-shadow: 2.5rem 3.75rem 3rem -3rem hsl(var(--clr-secondary-400) / 0.25);
}

.testimonial:nth-child(1) {
  grid-area: one;
}
.testimonial:nth-child(2) {
  grid-area: two;
}
.testimonial:nth-child(3) {
  grid-area: three;
}
.testimonial:nth-child(4) {
  grid-area: four;
}
.testimonial:nth-child(5) {
  grid-area: five;
}

@media screen and (min-width: 33em) {
  .testimonial-grid {
      grid-template-areas:
      "one one"
      "two three"
      "five five"
      "four four";
  }
}

@media screen and (min-width: 38em) {
  .testimonial-grid {
    grid-template-areas:
     'one one'
     'two five'
     'three five'
     'four four';
  }
}

@media screen and (min-width: 54em) {
  .testimonial-grid {
      grid-template-areas:
      "one one two"
      "five five five"
      "three four four";
  }
}

@media screen and (min-width: 75em) {
  .testimonial-grid {
      grid-template-areas:
      "one one two five"
      "three four four five";
  }
}
```

# Grid short hands

Grid column start and end short hands for using the span.

```css
.container {
	display: grid;
	....
	....
}

.child {
	grid-column: 1 / 2; /* it basically says that the columns start should be 1 and end should be 2 */
	/* which is equivalent to grid-column: span 2;  */
}
```

# :has() selector

This is a modern css selector which helps selecting the parent element of the provided selector inside the parenthesis

```css
/* Selects an h1 heading with a
paragraph element that immediately follows
the h1 and applies the style to h1 */

h1:has(+ p) {
  margin-bottom: 0;
}
```

```css
body:has(video, audio) {
  /* styles to apply if the content contains audio OR video */
}
body:has(video):has(audio) {
  /* styles to apply if the content contains both audio AND video */
}
```


# :is() selector 

This is also a modern CSS selector which allows us to group multiple selectors into one, which can help reduce typing effort and create identical CSS code. For exampl, instead of writing three seperate selectors for h1, h2, and h3 you can use the `:is()` selector like this 

```css
:is(h1, h2, h3) {
	color: blue;
}
```


# :where() selector

This is also a modern CSS selector, its almost the same with the [[#is() selector]] but the only difference is about the specificity of both selectors where the [[#is() selector]] takes the most specificity of the passed selectors but on the other hand the :where() selector has a **0** specificity of its own.

**E.g**

```html
<article>
  <h2>:is()-styled links</h2>
  <section class="is-styling">
    <p>
      Here is my main content. This
      <a href="https://mozilla.org">contains a link</a>.
    </p>
  </section>

  <aside class="is-styling">
    <p>
      Here is my aside content. This
      <a href="https://developer.mozilla.org">also contains a link</a>.
    </p>
  </aside>

  <footer class="is-styling">
    <p>
      This is my footer, also containing
      <a href="https://github.com/mdn">a link</a>.
    </p>
  </footer>
</article>

<article>
  <h2>:where()-styled links</h2>
  <section class="where-styling">
    <p>
      Here is my main content. This
      <a href="https://mozilla.org">contains a link</a>.
    </p>
  </section>

  <aside class="where-styling">
    <p>
      Here is my aside content. This
      <a href="https://developer.mozilla.org">also contains a link</a>.
    </p>
  </aside>

  <footer class="where-styling">
    <p>
      This is my footer, also containing
      <a href="https://github.com/mdn">a link</a>.
    </p>
  </footer>
</article>
```

```css
html {
  font-family: sans-serif;
  font-size: 150%;
}

:is(section.is-styling, aside.is-styling, footer.is-styling) a {
  color: red;
}

:where(section.where-styling, aside.where-styling, footer.where-styling) a {
  color: orange;
}
```

**The output of this code follows as this**

![[Pasted image 20240721194713.png]]

Here the last `a` in the footer for the `:where()` selector doesn't get the styling from the selector because it has specificity of 0 and the last css is applied to that is the `footer a {...}` which cascades the older one with the `:where()` selector itself.