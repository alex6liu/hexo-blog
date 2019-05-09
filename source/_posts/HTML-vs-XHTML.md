---
title: HTML vs XHTML
date: 2019-05-08 16:04:08
tags: [HTML]
---

## The Most Important Differences from HTML:

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

### <!DOCTYPE ....> Is Mandatory

An XHTML document must have an XHTML DOCTYPE declaration.

A complete list of all the XHTML Doctypes is found in our HTML Tags Reference.

The <html>, <head>, <title>, and <body> elements must also be present, and the xmlns attribute in <html> must specify the xml namespace for the document.

This example shows an XHTML document with a minimum of required tags:

``` html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">

<head>
  <title>Title of document</title>
</head>

<body>
  some content 
</body>

</html>
```

### XHTML Elements Must Be Properly Nested

In HTML, some elements can be improperly nested within each other, like this:

``` html
<b><i>This text is bold and italic</b></i>
```

In XHTML, all elements must be properly nested within each other, like this:

``` html
<b><i>This text is bold and italic</i></b>
```

### XHTML Elements Must Always Be Closed

This is correct:

``` html
<p>This is a paragraph</p>
<p>This is another paragraph</p>
```

### Empty Elements Must Also Be Closed

This is correct:

``` html
A break: <br />
A horizontal rule: <hr />
An image: <img src="happy.gif" alt="Happy face" />
```

### XHTML Elements Must Be In Lower Case

``` html
<body>
<p>This is a paragraph</p>
</body>
```

### XHTML Attribute Names Must Be In Lower Case

``` html
<table width="100%">
```

### Attribute Values Must Be Quoted

``` html
<table width="100%">
```

### Attribute Minimization Is Forbidden

Wrong:

``` html
<input type="checkbox" name="vehicle" value="car" checked />
```

Correct:

``` html
<input type="checkbox" name="vehicle" value="car" checked="checked" />
```

## How to Convert from HTML to XHTML

- Add an XHTML <!DOCTYPE> to the first line of every page
- Add an xmlns attribute to the html element of every page
- Change all element names to lowercase
- Close all empty elements
- Change all attribute names to lowercase
- Quote all attribute values

[Link](https://www.w3schools.com/html/html_xhtml.asp)