---
title: Media queries
date: 2019-05-09 14:57:24
tags: [CSS]
---

[mdn](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries)

**Media queries** let you adapt your site or app depending on the presence or value of various device characteristics and parameters.

They are a key component of responsive design. For example, a media query can shrink the font size on small devices, increase the padding between paragraphs when a page is viewed in portrait mode, or bump up the size of buttons on touchscreens.

In CSS, use the `@media` at-rule to conditionally apply part of a style sheet based on the result of a media query. Use `@import` to conditionally apply an entire style sheet.

## [Using media queries](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries)

``` css
/* Set the background color of body to tan */
body {
  background-color: tan;
}

/* On screens that are 992px or less, set the background color to blue */
@media screen and (max-width: 992px) {
  body {
    background-color: blue;
  }
}

/* On screens that are 600px or less, set the background color to olive */
@media screen and (max-width: 600px) {
  body {
    background-color: olive;
  }
}
```

### Media types

- all
Suitable for all devices.
- print
Intended for paged material and documents viewed on a screen in print preview mode. (Please see paged media for information about formatting issues that are specific to these formats.)
- screen
Intended primarily for screens.
- speech
Intended for speech synthesizers.

### Media features

width, height and etc.

### Logical operators

- and
- not
- only
- ,