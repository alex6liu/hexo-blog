---
title: web typography
date: 2019-05-09 15:16:54
tags: [CSS]
---

## [web safe fonts](https://www.w3schools.com/cssref/css_websafe_fonts.asp)

The font-family property should hold several font names as a "fallback" system, to ensure maximum compatibility between browsers/operating systems. If the browser does not support the first font, it tries the next font.

Start with the font you want, and end with a generic family, to let the browser pick a similar font in the generic family, if no other fonts are available:

``` css
p {
  font-family: "Times New Roman", Times, serif;
}
```

## [custom web fonts](https://stackoverflow.com/questions/12144000/using-custom-fonts-using-css)

Generically, you can use a custom font using @font-face in your CSS. Here's a very basic example:

``` css
@font-face {
    font-family: 'YourFontName'; /*a name to be used later*/
    src: url('http://domain.com/fonts/font.ttf'); /*URL to font*/
}
```

Then, trivially, to use the font on a specific element:

``` css
.classname {
    font-family: 'YourFontName';
}
```

## font formats

- TrueType Fonts (TTF)

TrueType is a font standard developed in the late 1980s, by Apple and Microsoft. TrueType is the most common font format for both the Mac OS and Microsoft Windows operating systems.

- OpenType Fonts (OTF)

OpenType is a format for scalable computer fonts. It was built on TrueType, and is a registered trademark of Microsoft. OpenType fonts are used commonly today on the major computer platforms.

- The Web Open Font Format (WOFF)

WOFF is a font format for use in web pages. It was developed in 2009, and is now a W3C Recommendation. WOFF is essentially OpenType or TrueType with compression and additional metadata. The goal is to support font distribution from a server to a client over a network with bandwidth constraints.

- The Web Open Font Format (WOFF 2.0)

TrueType/OpenType font that provides better compression than WOFF 1.0.

- SVG Fonts/Shapes

SVG fonts allow SVG to be used as glyphs when displaying text. The SVG 1.1 specification define a font module that allows the creation of fonts within an SVG document. You can also apply CSS to SVG documents, and the @font-face rule can be applied to text in SVG documents.

- Embedded OpenType Fonts (EOT)

EOT fonts are a compact form of OpenType fonts designed by Microsoft for use as embedded fonts on web pages.

## icon fonts

Icon fonts are fonts that contain symbols and glyphs instead of letters or numbers. 

## [font-face](https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face)

