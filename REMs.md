# REMs

## Introduction

Browsers and devices calculate pixel sizes differently. There may be many more pixels crammed into the same space on your phone as there are on a wide screen tv. How can you be sure that what you have designed on your screen will be delivered to someone else's in the same format and looking the same??

#### What is a REM?

A REM is a **scalable** unit of measurement which the web browser converts to a pixel value. 

Remember, in contrast, a `px` value is _not scalable_.

The browser looks at the **root element** i.e. the `<html>` element and understands 1rem to be the font-size of that root element.

By default (determined by the browser's settings) this is usually `16px`.

#### What does REM stand for?

REM actually stands for "Relative EM":

- Relative meaning - relative to the root element
- EM meaning - literally the size of one 'M' based on the font size of **this particular element**.

EMs, therefore, unlike REMs _**inherit**_ their value from parent elements. 

#### Why Use REMs?

- ##### Accesibility

Users may wish to change the default font size on their browser to make it easier to read. But, by using rem units, if a user increases their font size, the integrity of the layout will be _preserved_, and the text won’t get squashed up in a rigid space meant for smaller text.

- ##### Consistency

The most important thing in Web Design is being able to conclude that what you see before will look that way for everyone else. Pixel perfect design is a misconception in Web Design - some people have more of them, some people zoom in on them. Just make sure that your site can adapt.

## Usage Pattern

##### Declare the Root element font-size.

```css
html {
    font-size: 1rem;
}

/*  Allow the user to determine for themselves if they want to view things a little bigger.
    Give the root element 1 x the browser's font-size. 
*/
```

##### Calculate Padding / Margin / Font-size in REMs

Assume the root font-size is `16px` (it usually is) and do your calculations from there.

Want 10px of padding inside this element?

`10/16 = 0.625`

Looks like you need 0.625rems of padding here. 

```css
.card {
    padding: 0.875rem 0; /* 14px 0 */
}
.card__title {
    margin: 0.25rem auto; /* 4px auto */
    font-size: 1.25rem; /* 20px */ 
}

```