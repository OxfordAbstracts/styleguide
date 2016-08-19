# Re-writing CSS

## DRY

CSS cascades, but that doesn't mean you should overwrite styles by default. Go back, check, what can be abstracted out of a class, how can I write less CSS. 

###### *I am **not** encouraging the use of DRYCSS, [which is a thing](http://simianuprising.com/2012/03/07/video-of-my-dry-css-talk/), and obviously encourages the dryest css, but I do not feel it suits our project.*

This is not dry:

```
.primary-action-button {
  background-color: #00AA61;
  color: #FFFFFF;
  text-align: center;
  border-radius: 0.1em;
  padding: 0.4em;
  cursor: pointer;
  text-decoration: none;
  border: none;
  margin: 10px;
  font-size: 1.125em;
}

.alternative-action-button {
  background-color: #82E3C3;
  color: #000000;
  text-align: center;
  border-radius: 0.1em;
  padding: 0.4em;
  cursor: pointer;
  text-decoration: none;
  border: none;
  margin: 10px;
  font-size: 1.125em;
}

.secondary-action-button {
  background-color: #DBDBDB;
  color: #000000;
  text-align: center;
  border-radius: 0.1em;
  padding: 0.4em;
  cursor: pointer;
  text-decoration: none;
  border: none;
  margin: 10px;
  font-size: 1.125em;
}
```
*(I shit you not, I found this in app.css)*


This is dry:

```
.action-button {
    color: #000000;
    text-align: center;
    border-radius: 0.1em;
    padding: 0.4em;
    cursor: pointer;
    text-decoration: none;
    border: none;
    margin: 10px;
    font-size: 1.125em;
}

.primary {
    background-color: #00AA61;
    color: #FFFFFF;
}
.alternative {
    background-color: #82E3C3;
}
.secondary {
    background-color: #DBDBDB;
}
```

Those two blocks of CSS produce the same visual outcome. Now let's learn to write dry CSS in a [methodological](https://www.youtube.com/watch?v=fP31Gu6_u_I) way. 

---

---
## Block | Element | Modifier

##### BEM is a methodology for separating Content from Structure and Presentation in order to develop something that is modular, scalable, and maintainable. 

BEM works when you have a good idea of what you're styling. We have designs, we have an understanding of how the app should operate and so we can properly plan and set up our CSS. No more is there a need to make a new rule for every new bit of the app as and when it turns up. No more CSS scrubbishness. 

Anyway:

### What is a block?

A block is a high-level element or group of elements. It can be simple or complex and one block can contain others.

#### What kind of names do blocks have?

Blocks are **not to be in context**. Don't call you blocks things like:

`.privacy-message` or `.authors`

Instead, call them by their *UI element names*. Things like:

`.button`

`.card`

`.navbar`


The point is to create readable, maintainable CSS. Once it is possible to read the HTML and conclude:

> ah, here is a card with a button

and then reach for the CSS only to say:

> so this is what a card and a button looks like and I understand the relationship between them 

we are winning at life. 



### What is an Element?

An element is the next level down from a block. It must be hierarchically one level beneath a block.

*If you're looking at an element and thinking, this is independent of the block in which it is nested, then it probably isn't an element.*

#### So what do Elements look like?

Following on from the examples above, an element might be:

`.button__label`

`.card__title`

`.navbar__link`

#### And how do I apply them?

within the HTML you might expect to see something like this:

```
<div class="card">
    <h3 class="card__title">Event Name</h3>
    <p class="card__description">Some user-facing description...</p>
    <button class="button">Duplicate</button>
    <div class="button">
        <span class="button__label">Delete</span>
    </div>
</div>
```

The example I've detailed here actually highlights another point about BEM:

> Don't rely on element styling e.g. `button { styles }`

You never know how the markup will change or rearrange - the only thing you can be sure of is that, if something has the right class (in this case `button`), it will look like a muhfuggin button. 

#### What about nesting? How do I name an Element nested in another Element?

Elements can be nested. No worries. 

```
<div class="card">
    <div class="card__header">
        <h3 class="card__title">Event Name</h3>
    </div>
</div>
```

Both elements above are dependent on the Block: `.card`. Yes they are nested within each other but the only relationship we are concerned with is the one that connects them to their block. 

___

**With all of this** please try and keep best practices about semantic HTML and 'not-too-deeply-nested' HTML in the forefront of your mind. Don't litter the page with `<h1>`'s

### What is a Modifier?

A modifier is a state thing. They are used when elements must take a different form of themselves. According to the BEM website: “A modifier is a property of a block or an element that alters its look or behavior. A modifier has a name and a value. Several modifiers can be used at once.”

A great example is on button:

`.button--disabled`
`.button--big`

And, as we all know, the way CSS works means that these styles must be used to override the standard `.button` styles whatsoever they are. 

The button block section of CSS might look something like this:

```
/* Button Block*/

.button {
    background: #00AA61;
    box-shadow: inset 0px -1px 2px 0px rgba(0,0,0,0.50), inset 0px 1px 2px 0px #FFFFFF;
    border-width: 1px;
    border-style: solid;
    border-color: #333333;
    border-radius: 3px;
}

.button--disabled {
    background: #cdcdcd;
    border-colour: #888888
}

.button--big {
    padding: 1em 2em;
}
```

These means that the final HTML would something like this:

```
<div class="button button--disabled button--big">
    <span class="button__label"></span>
</div>
```

Which means I can read that partial and not only know where to look to change its styles but also it semantically explains itself **from a user's perspective**. ALSO, when you revisit it later or reuse that partial for something else you won't forget what UI component it is. 

### Avoid Descendant Selectors

so stuff like this:

```
.manage-users-row .manage-users-cell {
```

## [Actually Doing the re-writing](/action-plan.md)

It's tricky at first and may take some getting used to - but the work will pay off down the line. 

