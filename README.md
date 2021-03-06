# [Living Style Guide](https://app.frontify.com/d/0nvkJOFPhUB2/ui-library)

*Living Style Guide Last updated 3 Nov 2016*

## Why?

#### Design Inconsistencies

*The wireframes don't look like the wireframes*
As the application has been designed, it's patterns and principles have incrementally evolved. As a result, the most recently designed wireframes do not look like the earliest wireframes!

#### Design / CSS Inconsistencies

*the elements don't look like the wireframes*
Partly due to the above, and a lack of clear CSS guidlines, there are many inconsistencies between elements their wireframe counterparts.

#### CSS Inconsistencies

*the elements don't look like the elements*
Without any guiding principles for writing CSS for this project there are a number of inconsistencies between declarations: namely, colours, sizes, and alignment.  

---

## How?

#### With [Frontify](https://frontify.com/)

The files within this repository are simply a proving ground for the CSS. The real living style-sheet can be found at the link below. 

With a free account we can have 100mb of data and up to 3 editors. If you want access just let me know. 

Frontify also allows us to define all other parts of a style guide, not just components. 

---

## What in Practice

#### Single source of Truth

I suggest we modularise the stylesheet in this repository. Using [RawGit](https://rawgit.com/) I have generated a CDN link to this stylesheet. This link connects the stylesheet here to Frontify.

#### [Re-writing CSS: Block, Element, Modifier](/re-writing-css.md)

Consistent CSS patterns make for easier reading, maintenance, and implementation. They also reinforce the design patterns into the code.

[B.E.M.](http://getbem.com/naming/) is a methodology, that helps you to achieve reusable components and code sharing in the front-end.

I want us to adopt this methodology and offer my own services in doing so.

[Harry Roberts says:](http://csswizardry.com/2015/03/more-transparent-ui-code-with-namespaces/)

> [Developer confidence] is the main reason we end up with bloated code bases, full of legacy and unknown CSS that we daren't touch. We lack the confidence to be able to work with and modify existing styles because we fear the consequences of CSS' globally operating and leaky nature. Almost all problems with CSS at scale boil down to confidence (or lack thereof): People don't know what things do any more. People daren't make changes because they don't know how far reaching the effects will be.

---


#### A Note on Sizing

In a previous life I was a front-end developer and I grew a great fondness for `rem`s. The Root Em is a proportional expression of the root-element's font-size (which will be declared in pixels) ((and which is most often the `<html>` element)). [Browser support is good](http://caniuse.com/#search=rem) 

I have found in the Application a mixture of `px`'s and `em`'s. 

Since [a pixel is not always a pixel](http://stackoverflow.com/questions/27382331/how-a-css-pixel-size-is-calculated), and using the compound inheritence of an em can lead to some very bespoke declarations.

So, I suggest a system similar to [this one](https://css-tricks.com/rems-ems/) with:

- Root level: **declared in `px`**
- Block level: **declared in `rem`**
- Element level: **declared in `em`**

This works well for our project because it's design pattern is "component-focused" with many repeated "sections" and "cards". It also allows for very light, but holistic changes to be made: changing the `font-size` of a *block* from `1rem` to `0.75rem` (with a media query) will proportionally change all of the dependent elements within to the same degree.


