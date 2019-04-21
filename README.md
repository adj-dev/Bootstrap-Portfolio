*This is Homework Assignment 2A for The Coding Bootcamp through the University of Minnesota.* 

# Introduction

The purpose of this project is to use Bootstrap to control most of the layout and styling of a Portfolio Web Application. This was achieved with the use of Bootstrap **components** and **grid** system. 

- a `<nav>` component exists at the top of all pages and a `<form>` was used for the *contact* page. 
- the grid system was used in both the main content `<div>` and the `<footer>` section. Sub-rows and columns were used in the main content `<div>` on the *portfolio* page. 

# Challenges

## First Challenge

```css
a.nav-link:hover {
  top-border: 1px solid rgb(204, 204, 204);
}
```

To add some interactivity to the UX I wanted a horizontal line to appear above a link when the cursor hovered over it. To achieve this I planned on adding a `border-top` property to the `<a>` tags in the `<nav>` with the `:hover` pseudo class. There were two distinct issues I encountered: 
1. The introduction of a top border to one of the three links caused the other two links to slightly shift in position. This made for an awkward experience when moving the cursor over the links.
2. Naturally, when a top border was rendered it stretched the entire span of the element. Although this was expected it left desire for a shorter top border that would preferably be equal in length to the word it appeared over.

My solutions for these problems, respectively:

1. I added `top-border: 1px solid rgba(0, 0, 0, 0);` to all nav links (*not* in a pseudo class). This created an invisible top border, so there was no change in positioning when hovering over a link.
2. The `<a>`'s box-sizing were determined by the Bootstrap CSS with padding. To accomplish the desired effect on the top border I removed the left-right padding with `padding: .5rem 0 !important;` (the `!important` keyword was required to overcome the specificity of Bootstrap's styling) and replaced the missing padding with margin, `margin: 0 .5rem`. 

```css
a.nav-link {
  border-top: 1px solid rgba(0, 0, 0, 0);
  padding: 0.5rem 0 !important;
  margin: 0 0.5rem;
  transition: all 0.4s ease; /* adds fade-in/fade-out effect */
}

a.nav-link:hover {
  border-top: 1px solid rgb(204, 204, 204);
}
```

## Second Challenge

I liked the idea of having a sticky `<footer>`, but I didn't like that it would overlap any and all content if the browser window was made short enough. To go about solving this I decided to use `@media` queries to change the `<footer>` positioning from `fixed` (to the bottom of the viewport) to  `static` (with a `top-margin` giving distance from the page content). 

Essentially, my goal was for the `<footer>` to remain sticky to the bottom of the viewport until doing so would cause overlap with any other content rendered on screen. 

To accomplish this I added `@media` queries for each responsive breakpoint on each page. Because the content `<div>` was a different height on each page, it required for each `.html` file to have it's own dedicated `.css`. In addition, once the viewport width got small enough the collapsed menu was activated in the `<nav>` which caused all content to move down quite a bit when the menu was expanded. This required me to increase the `padding-top` for the `<footer>` for these special conditions. 

```css
@media screen and (max-width: 767px) {
  .footer {
    margin-top: 80px;
  }
}

@media screen and (min-width: 768px) and (max-width: 991px) and (max-height: 799px) {
  .footer {
    margin-top: 171px;
  }
}

@media screen and (min-width: 768px) and (max-width: 991px) and (min-height: 800px) {
  .footer {
    position: fixed;
    bottom: 0;
    margin-top: 96px;
  }
}

@media screen and (min-width: 992px) and (max-width: 1199px) and (min-height: 784px) {
  .footer {
    position: fixed;
    bottom: 0;
  }
}

@media screen and (min-width: 1200px) and (min-height: 856px) {
  .footer {
    position: fixed;
    bottom: 0;
  }
}
```

Reference **footer-about.css**, **footer-contact.css**, and **footer-portfolio.css** to view the all solution code.

## Third Challenge

For the *Portfolio* page I wanted a sleek and intuitive way to present project titles with their respective images. I decided to place a hidden `<h3 class="overlay">` as a sibling to each `<img>` that would appear when the mouse was hovering over the image. This `<h3>` would contain the title of the project and needed to be placed directly on top of the image. Due to Bootstraps wonderfully expansive styling achieving this wasn't quite as straight-forward as one might have hoped. 

### Steps

1. Give the `<h3 class="overlay">` a position of "absolute" so it can be placed over the `<img>`.
```css
.overlay {
  display: none;
  position: absolute;
  z-index: 1;
  bottom: 0;
}
```
2. Center the text. (This proved the most difficult part. In order to center the text, the `<h3>` needed its width to be 100%. For some reason the width seemed to take the padding of the parent element into account and extended past the right-side of the content, so the text couldn't be centered using a relative width. To counter against this I measured the width of the images per breakpoint and used `@media` queries to adjust the `<h3>` width accordingly)
```css
.overlay {
  display: none;
  position: absolute;
  z-index: 1;
  bottom: 0;
  text-align: center;
}

@media screen and (min-width: 1200px) {
  .overlay {
    width: 339.33px;
  }
}

@media screen and (min-width: 992px) and (max-width: 1199px) {
  .overlay {
    width: 279.33px;
  }
}

@media screen and (min-width: 768px) and (max-width: 991px) {
  .overlay {
    width: 199.33px;
  }
}
```
There was a caveat: once the screen width got below 768px the images resized automatically with a *relative* width, this made it impossible to center the text using a *static* width such as pixels. My solution to this was to remove the original cause of the issue: the `padding` on the parent `<div>`. This allowed me to use `width: 100%` on the `<h3>`.
```css
@media screen and (max-width: 767px) {
  .overlay {
    width: 100%;
  }

  div.hover-text {
    padding: 0;
    margin: 0 15px;
  }
}
```
This didn't perform well when images were placed adjacent horizontally, thus I was only able to apply it to mobile layouts (thus `max-width: 767px`).

3. I had to account for mobile layouts not allowing users the ability to hover with a cursor over the links.

```css
@media screen and (max-width: 767px) {
  .overlay {
    display: block;
  }
}
```

The total solution:

```css
.overlay {
  display: none;
  position: absolute;
  z-index: 1;
  bottom: 0;
  text-align: center;
  color: white;
  background-color: rgba(0, 0, 0, 0.48);
  margin-bottom: 0;
  padding: 5% 0;
}

div.hover-text:hover > a > .overlay {
  display: block;
}

@media screen and (min-width: 1200px) {
  .overlay {
    width: 339.33px;
  }
}

@media screen and (min-width: 992px) and (max-width: 1199px) {
  .overlay {
    width: 279.33px;
  }
}

@media screen and (min-width: 768px) and (max-width: 991px) {
  .overlay {
    width: 199.33px;
  }
}

@media screen and (max-width: 767px) {
  .overlay {
    display: block;
    width: 100%;
  }

  div.hover-text {
    padding: 0;
    margin: 0 15px;
  }
}
```
