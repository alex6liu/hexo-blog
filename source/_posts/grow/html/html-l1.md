---
title: html l1
date: 2019-05-14 09:48:24
tags: [html, l1]
---

## Document Type Definition

### Doctype element, HTML and XHTML syntax differences

#### Doctype element

The <!DOCTYPE> declaration must be the very first thing in your HTML document, before the <html> tag.

The <!DOCTYPE> declaration is not an HTML tag; it is an instruction to the web browser about what version of HTML the page is written in.

**Tip**

- Always add the <!DOCTYPE> declaration to your HTML documents, so that the browser knows what type of document to expect.
- The <!DOCTYPE> declaration is NOT case sensitive.

#### HTML and XHTML syntax differences

- Document Structure
  - XHTML DOCTYPE is **mandatory**
  - The xmlns attribute in <html> is **mandatory**
  - <html>, <head>, <title>, and <body> are **mandatory**
- XHTML Elements
  - XHTML elements must be **properly nested**
  - XHTML elements must always be **closed**
  - XHTML elements must be in **lowercase**
  - XHTML documents must have **one root element**
- XHTML Attributes
  - Attribute names must be in **lower case**
  - Attribute values must be **quoted**
  - Attribute minimization is **forbidden**

### Browser modes

- Quirks Mode
- Standards Mode

## Layout and text formatting tags

### Layout tags

- `<header>` - Defines a header for a document or a section
- `<nav>` - Defines a container for navigation links
- `<section>` - Defines a section in a document
- `<article>` - Defines an independent self-contained article
- `<aside>` - Defines content aside from the content (like a sidebar)
- `<footer>` - Defines a footer for a document or a section
- `<details>` - Defines additional details
- `<summary>` - Defines a heading for the `<details>` element

### HTML 5 structural and semantic tags

A semantic element clearly describes its meaning to both the browser and the developer.

Examples of non-semantic elements: `<div>` and `<span>` - Tells nothing about its content.

Examples of semantic elements: `<form>`, `<table>`, and `<article>` - Clearly defines its content.

#### New Semantic Elements in HTML5

- `<article>`
- `<aside>`
- `<details>`
- `<figcaption>`
- `<figure>`
- `<footer>`
- `<header>`
- `<main>`
- `<mark>`
- `<nav>`
- `<section>`
- `<summary>`
- `<time>`

### Formatting tags: bold, italic, upper, lower cases and etc.

- `<b>` - Bold text
- `<strong>` - Important text
- `<i>` - Italic text
- `<em>` - Emphasized text
- `<mark>` - Marked text
- `<small>` - Small text
- `<del>` - Deleted text
- `<ins>` - Inserted text
- `<sub>` - Subscript text
- `<sup>` - Superscript text

## Metadata, Styles, Scripts

### Meta tags

The `<meta>` tag provides metadata about the HTML document. Metadata will not be displayed on the page, but will be machine parsable.

### page encoding

To display an HTML page correctly, a web browser must know which character set (character encoding) to use.

This is specified in the `<meta>` tag:

For HTML4: `<meta http-equiv="Content-Type" content="text/html;charset=ISO-8859-1">`

For HTML5: `<meta charset="UTF-8">`

### Add inline styles, include internal and external CSS

Using external CSS: `<link href="style.css" rel="stylesheet" type="text/css">`

Using internal CSS: 

```html
<head>
<style type="text/css">

    h1 {
            color:#fff
            margin-left: 20px;
       }

    p {
        font-family: Arial, Helvetica, Sans Serif;     
       }


</style>
</head>
```

Using inline styles: `<h1 style="color:red;margin-left:20px;">Today’s Update</h1>`

### Include internal and external Script

Using internal:

```html
<script>
document.getElementById("demo").innerHTML = "My First JavaScript";
</script>
```

Using external: `<script src="myScript.js"></script>`

### Meta viewport property

The viewport is the user's visible area of a web page. It varies with the device, and will be smaller on a mobile phone than on a computer screen.

`<meta name="viewport" content="width=device-width, initial-scale=1.0">`

A `<meta>` viewport element gives the browser instructions on how to control the page's dimensions and scaling.

## Page structure

### Root HTML tags

`<html></html>`

### Tree model

DOM tree

### Basic HTML elements: headers, listings, links, rare tags and etc.

### HTML tag attributes

## Table, Form, Input Tags

### Table layout tags

- Use the HTML `<table>` element to define a table
- Use the HTML `<tr>` element to define a table row
- Use the HTML `<td>` element to define a table data
- Use the HTML `<th>` element to define a table heading
- Use the HTML `<caption>` element to define a table caption
- Use the CSS `border` property to define a border
- Use the CSS `border-collapse` property to collapse cell borders
- Use the CSS `padding` property to add padding to cells
- Use the CSS `text-align` property to align cell text
- Use the CSS `border-spacing` property to set the spacing between cells
- Use the `colspan` attribute to make a cell span many columns
- Use the `rowspan` attribute to make a cell span many rows
- Use the `id` attribute to uniquely define one table

### Table attributes

- align
- bgcolor
- border
- cellpadding
- cellspacing

### Form tags and attributes

attributes:

- action
- method
- target

### Input types

- button: A push button with no default behavior.
- checkbox: A check box allowing single values to be selected/deselected.

### HTML 5 input types

- color: **HTML5** A control for specifying a color. A color picker's UI has no required features other than accepting simple colors as text (more info).
- date: **HTML5** A control for entering a date (year, month, and day, with no time).
- datetime-local: **HTML5** A control for entering a date and time, with no time zone.
- email: **HTML5** A field for editing an e-mail address.