# Plan of Action

## Step 1: Identify Blocks

###### Getting to know the UI

Imagine them like Building Blocks. A site is made up of building blocks. Each block can have many blocks within.

#### Let's say this is the UI

<img src="img/site.png" alt="">

#### We can Identify some key groups that could be considered blocks:

<img src="img/site-marked.png" alt="">

Note that these would be in addition to some bigger blocks such as containers, sections, headers, and, ultimately, the `<body>` and `<html>`.

#### Mark them up and give them unique names:

<img src="img/head-marked.png" alt="">

Notice, again how blocks are nested within each other.

## Step 2: Identify Elements within those blocks

<img src="img/menu-items.png" alt="">

#### This is, let's say, a Search Block
<img src="img/search-block.png" alt="">

#### It contains 
<img src="img/search-block-marked.en_.png" alt="">

## Step 3: What does what

Next comes the task of figuring out which rules that have already been written affect which blocks and block-elements. This is [no mean feat](https://en.wiktionary.org/wiki/no_mean_feat).

### So what's the process?
###### Work in progress (to be refined)

1. Arm yourself with Text styles and colours as determined by the [Styleguide]()
1. Delete this evil, shameful, sinful thing: `<link rel="stylesheet" href="https://code.getmdl.io/1.1.2/material.indigo-pink.min.css">`. *C'mon, you knew this was coming.*
1. Run the app
2. Load a view on one screen. 
2. Determine and inspect a **Block**
3. Find the bit of CSS that styles it **and**
4. Find the markup partial(s) (remember that changing the css is like bookkeeping - you do it all twice)
    - Finding the partial may require searching through all the views so if you can do an equivalent to ST2's "Find in Files" then do so. 
5. Determine what lives inside this block - **Elements** and **other Blocks**
6. Gather all of those pieces together to the same place in the CSS file. 
    - if they don't exist then create them

### Example

- I have identified that the Card that shows information about an event (on the Client / all Events view) is a Block.
- Inspecting it reveals that it has the class `.box`
- I find the `.box {}` style declaration at line 291 of `app.css` and leave it open
- In a new tab I find `<div class="box">` is in two partials so I open them both
    - `event.html` features a `.box` 4 times
    - `client.html` features a `.box` once.
  
  *The client view is the one I'm actually looking at one the screen so I'll focus on this one.*

- I determine that the Card block contains:
    - 2 Button Blocks
    - A Header Element
    - A title Element
    - A body Element
    - A subtitle Element (Submissions)
    - 4 Label Elements
    - 4 Data Elements
- I gather all of the CSS rules that pertain to these elements together (just focusing on the Card elements for now) to where the `.box` rule is in the CSS. 
    - In the process of doing so I created rules for the identified elements:
```
.card__header {}
.card__title {}
.card__body {}
.card__subtitle {}
.card__label {}
.card__data {}
```

- Don't re-name anything just yet!
    
I have gathered the following incumbent rules:
```
.border-bottom-div {
.no-margin {
.text-type-one {
.text-type-two {
.small-height-div {
.go-to-button-div {
```
- This means I can now confidently go through the partial and remove any styles that I do not have control over and should no longer have any effect *(assuming you actually repented for your sins and followed step 2)* - namely things like: `mdl-grid` and `mdl-cell--4-col-tablet`.

### Before:

#### client.html:30-74

```
<div class="box">
  <div class="mdl-grid border-bottom-div">
    <div class="mdl-cell mdl-cell--8-col mdl-cell--4-col-tablet">
      <h5>{{this.event_title}}</h5>
    </div>
    <div class="mdl-cell mdl-cell--4-col mdl-cell--4-col-tablet">
      <a class='secondary-action-button right' href='/clients/{{this.client_id}}/events/{{this.event_id}}/update-page'> Edit Event</a>
      {{#if @root.admin}}
        <a class ='primary-action-button right ' href='/events/{{this.event_id}}'>Go to event</a>
      {{/if}}
    </div>
  </div>
  {{#unless @root.admin}}
  <div class="mdl-grid">
    <div class="mdl-cell mdl-cell--4-col mdl-cell--4-col-tablet">
      <h6 class="no-margin">Date</h6>
      <p class="text-type-one">{{this.event_date}}</p>
    </div>
    <div class="mdl-cell mdl-cell--8-col mdl-cell--4-col-tablet">
      <h6 class="no-margin">Venue</h6>
      <p class="text-type-one">{{this.venue}}</p>
    </div>
  </div>

  <div class="mdl-grid small-height-div">
    <div class="mdl-cell mdl-cell--12-col">
      <h6 class="no-margin">Submissions</h6>
    </div>
  </div>

  <div class="mdl-grid">
    <div class="mdl-cell mdl-cell--8-col mdl-cell--4-col-tablet">
      <h6 class="text-type-one">Deadline Date</h6>
      <p class="text-type-two">{{this.deadline_date}}</p>
      <h6 class="text-type-one">Notification Date</h6>
      <p class="text-type-two">{{this.outcome_notification_date}}</p>
    </div>

    <div class="mdl-cell mdl-cell--4-col mdl-cell--4-col-tablet go-to-button-div">
      <a class ='primary-action-button right go-to-button' href='/events/{{this.event_id}}'>Go to event</a>
    </div>
  </div>
  {{/unless}}

</div>
```

### Before:

#### app.css:291-316

```
.box {
  margin-left: 3em;
  margin-right: 3em;
  margin-bottom: 3em;
  border: 1px solid #808080;
  box-shadow: 5px 5px 5px #888888;
}

.dashboard-box {
  margin:1em;
  border: 1px solid #808080;
  box-shadow: 2px 2px 2px #888888;
}

.primary-background {
  background-color: #003066;
}

.primary-border {
  border: 2px solid #003066;
}

.primary-border-left {
  border-left: 2px solid #003066;
}

```
