---
title: 'Understanding external, internal, and inline CSS styles'
date: 2019-05-09 13:31:32
tags: [CSS]
---

Cascading Style Sheets (CSS) are files with styling rules that govern how your website is presented on screen. CSS rules can be applied to your website’s HTML files in various ways. You can use an **external stylesheet**, an **internal stylesheet**, or an **inline style**. Each method has advantages that suit particular uses.

An **external stylesheet** is a standalone .css file that is linked from a web page. The advantage of external stylesheets is that it can be created once and the rules applied to multiple web pages. Should you need to make widespread changes to your site design, you can make a single change in the stylesheet and it will be applied to all linked pages, saving time and effort.

An **internal stylesheet** holds CSS rules for the page in the **head** section of the HTML file. The rules only apply to that page, but you can configure CSS classes and IDs that can be used to style multiple elements in the page code. Again, a single change to the CSS rule will apply to all tagged elements on the page.

**Inline styles** relate to a specific HTML tag, using a **style** attribute with a CSS rule to style a specific page element. They’re useful for quick, permanent changes, but are less flexible than external and internal stylesheets as each inline style you create must be separately edited should you decide to make a design change.

## Using external CSS stylesheets

An HTML page styled by an external CSS stylesheet must reference the .css file in the document head. Once created, the CSS file must be uploaded to your server and linked in the HTML file with code such as:

``` html
<link href="style.css" rel="stylesheet" type="text/css">
```

## Using internal CSS stylesheets

Rather than linking an external .css file, HTML files using an internal stylesheet include a set of rules in their **head** section. CSS rules are wrapped in `<style>` tags, like this:

``` html
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

You can name your stylesheet whatever you wish, but it should have a .css file extension.

## Using inline styles
Inline styles are applied directly to an element in your HTML code. They use the **style** attribute, followed by regular CSS properties.

For example:

``` html
<h1 style="color:red;margin-left:20px;">Today’s Update</h1>
```