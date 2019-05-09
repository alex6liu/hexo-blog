---
title: Pseudo-classes and pseudo-elements
date: 2019-05-09 14:25:08
tags: [CSS]
---

[MDN](https://developer.mozilla.org/en-US/docs/Learn/CSS/Introduction_to_CSS/Pseudo-classes_and_pseudo-elements)

## Pseudo-classes

A CSS **pseudo-class** is a keyword added to the end of a selector, preceded by a colon (:), which is used to specify that you want to style the selected element but only when it is in a certain state. For example, you might want to style a link element only when it is being hovered over by the mouse pointer, or a checkbox when it is disabled or checked, or an element that is the first child of its parent in the DOM tree.

![](https://raw.githubusercontent.com/alex6liu/blog-images/master/html%26css/pseudo-classes.png)

## Pseudo-elements

Pseudo-elements are very much like pseudo-classes, but they have differences. They are keywords, this time preceded by two colons (::), that can be added to the end of selectors to select a certain part of an element.

- ::after
- ::before
- ::first-letter
- ::first-line
- ::selection
- ::backdrop