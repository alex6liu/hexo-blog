---
title: CSS selectors
date: 2019-05-09 14:28:41
tags: [CSS]
---

[MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors)

## Simple selectors

- Type selector
  - Selects all elements that match the given node name.
  - Syntax: eltname
  - Example: input will match any <input> element.
- Class selector
  - Selects all elements that have the given class attribute.
  - Syntax: .classname
  - Example: .index will match any element that has a class of "index".
- ID selector
  - Selects an element based on the value of its id attribute. There should be only one element with a given ID in a document.
  - Syntax: #idname
  - Example: #toc will match the element that has the ID "toc".
- Universal selector
  - Selects all elements. Optionally, it may be restricted to a specific namespace or to all namespaces.
  - Syntax: * ns|* *|*
  - Example: * will match all the elements of the document.
- Attribute selector
  - Selects elements based on the value of the given attribute.
  - Syntax: [attr] [attr=value] [attr~=value] [attr|=value] [attr^=value] [attr$=value] [attr*=value]
  - Example: [autoplay] will match all elements that have the autoplay attribute set (to any value).

## Combinators

- Adjacent sibling combinator
  - The + combinator selects adjacent siblings. This means that the second element directly follows the first, and both share the same parent.
  - Syntax: A + B
  - Example: h2 + p will match all <p> elements that directly follow an <h2>.
- General sibling combinator
  - The ~ combinator selects siblings. This means that the second element follows the first (though not necessarily immediately), and both share the same parent.
  - Syntax: A ~ B
  - Example: p ~ span will match all <span> elements that follow a <p>, immediately or not.
- Child combinator
  - The > combinator selects nodes that are direct children of the first element.
  - Syntax: A > B
  - Example: ul > li will match all <li> elements that are nested directly inside a <ul> element.
- Descendant combinator
  - The   (space) combinator selects nodes that are descendants of the first element.
  - Syntax: A B
  - Example: div span will match all <span> elements that are inside a <div> element.
- Column combinator 
  - The || combinator selects nodes which belong to a column.
  - Syntax: A || B
  - Example: col || td will match all <td> elements that belong to the scope of the <col>.

## Pseudo-classes

Pseudo-classes allow the selection of elements based on state information that is not contained in the document tree.

- Example: a:visited will match all <a> elements that have been visited by the user.

## Pseudo-elements

Pseudo-elements represent entities that are not included in HTML.

- Example: p::first-line will match the first line of all <p> elements.
