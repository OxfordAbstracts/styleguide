# Re-writing CSS

## Block | Element | Modifier

BEM works when you have a good idea of what you're styling. We have designs, we have an understanding of how the app should operate and so we can properly plan and set up our CSS. No more is there a need to make a new rule for every new bit of the app as and when it turns up. No more CSS scrubbishness. 

Anyway:

### What is a block?

A block is a high-level element or group of elements.

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

A modifier is a state thing. They are used when elements must take a different form of themselves. 

## Doing the re-writing

