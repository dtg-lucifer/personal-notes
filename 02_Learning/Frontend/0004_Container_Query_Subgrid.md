---
tags:
  - css
  - frontend
---
# Sub-grid

Ref - [Documentation MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_grid_layout/Subgrid)

It is way to define the grid template of the container and letting the children elements follow the same template as their own layout inside their box model. Just like the example shown below

![[Pasted image 20240715113307.png]]

It is simply helping to simplify and unify the layout for the all cards, as some titles are larger than the others so those are taking more space than others and causing the images to take shorter spaces than the others. 

Here comes the ==subgrid==, by defining the **template rows: 120px auto auto** we are defining the whole grid layout indeed for the main container but the cards are actually gonna use that template as their own layout as we set each car/ds template row as subgrid in the css so that every card image is taking the 120px height and the titles and the other parts are gonna take the auto and auto area.

**Important:** it is important to span all the cards to 3 rows because we are trying to take all the space the container gives us as a single repeation of the row (120px auto auto) and we are setting the same row repeation inside the cards layout.

# Container Query

Ref - [Documentations MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_containment/Container_queries)

Unlike a media query a container query is like the abstracted way to add some styles to a component on just depending on a singular container not the whole view port of the document.

Suppose i have a product card and i have used that in several times and several containers but in some cases some containers do have only one of the card inside them where as other containers have multiple cards inside them so depending on that the singular card should have flex direction row row and others should have flex direction of column. The thing is we cant do that using typical media queries as that will only look for the whole viewport where as we want only to look for that specific container (in this case card) so we can do one thing we can set each card as containers and add queries on to the containers.

like this

![[Pasted image 20240715131922.png]]

```html
<div class="post">
  <div class="card">
    <h2>Card title</h2>
    <p>Card content</p>
  </div>
</div>
```

```css
.post {
  container-type: inline-size;
}

/* Default heading styles for the card title */
.card h2 {
  font-size: 1em;
}

/* If the container is larger than 700px */
@container (min-width: 700px) {
  .card h2 {
    font-size: 2em;
  }
}

```

---

**We can also name each container to identify themselves from other containers to abstract them from others**


```css
.post {
  container-type: inline-size;
  container-name: sidebar;
}

@container sidebar (min-width: 700px) {
  .card {
    font-size: 2em;
  }
}

```

**Important thing to note:** maximum of the time we would need to just look up on the width of an container but if we need to look upon the height of the container then we would need to update a single property `container-type: block-size;`

---

# Image overlays with image borders

![[Pasted image 20240830191353.png]]

---
