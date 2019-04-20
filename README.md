# Bootstrap-Portfolio
Homework 2A

## The Good Stuff

To add some interactivity to the UX I wanted a horizontal line to appear above a link when the cursor hovered over it. To achieve this I planned on adding a `border-top` property to the `<a>` tags in the `<nav>` with the `:hover` pseudo class. There were two distinct issues I encountered while coding it out: 
1. The introduction of a top border to one of the three links caused the other two links to slightly shift in position. This made for an awkward experience when moving the cursor over the links.
2. Naturally, when a top border was rendered it stretched the entire span of the element. Although this was expected it left desire for a shorter top border that would preferably be equal in length to the word it appeared over.

My solutions for these problems, respectively:

1. I added `top-border: 1px solid rgba(0, 0, 0, 0);` to the all the nav links (*not* on a pseudo class). This created a completely invisible top border, so there was no change in positioning when hovering over a link.
2. The `<a>`'s box-sizing were determined by the Bootstrap CSS with padding. To accomplish the desired effect on the top border I removed the left-right padding with `padding: .5rem 0 !important;` (the `!important` keyword was required to overcome the specificity of Bootstrap's styling) and replaced the missing padding with margin, `margin: 0 .5rem`. 


