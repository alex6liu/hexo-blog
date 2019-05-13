---
title: positioning
date: 2019-05-09 15:33:45
tags: [CSS]
---

## [Document flow](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Normal_Flow)

By default, a block level element's content is 100% of the width of its parent element, and as tall as its content. Inline elements are as tall as their content, and as wide as their content. You can't set width or height on inline elements — they just sit inside the content of block level elements. If you want to control the size of an inline element in this manner, you need to set it to behave like a block level element with display: block; (or even,display: inline-block; which mixes characteristics from both.)

## [Position properties](https://www.w3schools.com/css/css_positioning.asp)

- static
- relative
- fixed
- absolute
- sticky

## Overflow

- visible - Default. The overflow is not clipped. The content renders outside the element's box
- hidden - The overflow is clipped, and the rest of the content will be invisible
- scroll - The overflow is clipped, and a scrollbar is added to see the rest of the content
- auto - Similar to scroll, but it adds scrollbars only when necessary

## z-index

The z-index property specifies the stack order of an element.

An element with greater stack order is always in front of an element with a lower stack order.

**Note**: z-index only works on positioned elements (position: absolute, position: relative, position: fixed, or position: sticky).