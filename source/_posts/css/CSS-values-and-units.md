---
title: CSS values and units
date: 2019-05-09 14:34:39
tags: [CSS]
---

[MDN](https://developer.mozilla.org/en-US/docs/Learn/CSS/Introduction_to_CSS/Values_and_units)

- Numeric values: Length values for specifying e.g. element width, border thickness, or font size, and unitless integers for specifying e.g. relative line width or number of times to run an animation.
- Percentages: Can also be used to specify size or length — relative to a parent container's width or height for example, or the default font-size. These are often to facilitate responsive design (e.g. creating "liquid layouts", which automatically adjust to fit on different screen sizes).
- Colors: For specifying background colors, text colors, etc.
- Functions: For specifying e.g. background images or background image gradients.

**Pixels** (px) are referred to as **absolute units** because they will always be the same size regardless of any other related settings. Other absolute units are as follows:

- q, mm, cm, in: Quarter millimeters, millimeters, centimeters, or inches.
- pt, pc: Points (1/72 of an inch) or picas (12 points.)

You probably won't use any of these very often except pixels.

There are also **relative units**, which are relative to the current element's **font-siz**e or **viewport** size:

- em: 1em is the same as the font-size of the current element. The default base font-size given to web pages by web browsers before CSS styling is applied is 16 pixels, which means the computed value of 1em is 16 pixels for an element by default. But beware — font sizes are inherited by elements from their parents, so if different font sizes have been set on parent elements, the pixel equivalent of an em can start to become complicated. Don't worry too much about this for now — we'll cover inheritance and font-sizing in more detail in later articles and modules. em are the most common relative unit you'll use in web development.
- ex, ch: Respectively these are the height of a lower case x, and the width of the number 0. These are not as commonly used or well-supported as em.
- rem: The rem (root em) works in exactly the same way as the em, except that it will always equal the size of the default base font-size; inherited font sizes will have no effect, so this sounds like a much better option than em, although rems don't work in older versions of Internet Explorer (see more about cross-browser support in Debugging CSS.)
- vw, vh: Respectively these are 1/100th of the width of the viewport, and 1/100th of the height of the viewport. Again, these are not as widely supported as em.
- %