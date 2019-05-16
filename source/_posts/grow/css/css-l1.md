---
title: css l1
date: 2019-05-14 09:48:47
tags: [css, l1]
---

## Basic knowledge

### Syntax, properties and capabilities etc.

#### syntax

![](https://raw.githubusercontent.com/alex6liu/blog-images/master/html%26css/css-syntax.gif)

#### properties

- display
- width / height
- margin / padding
- border
- float
- color
- background
- font
  
#### capabilities

- Specify fonts other than the default for the browser
- Specify color and size of text and links
- Apply colors to backgrounds
- Contain webpage elements in boxes and float those boxes to specific positions on the page

## Pseudo-class and pseudo-elements

### Special states and parts of elements

#### pseudo-class

A CSS pseudo-class is a keyword added to a selector that specifies a special state of the selected element(s). 

``` css
selector:pseudo-class {
  property: value;
}

/* example */
button:hover {
  color: blue;
}
```

**Note**: In contrast to pseudo-elements, pseudo-classes can be used to style an element based on its state.

#### pseudo-element

A CSS pseudo-element is a keyword added to a selector that lets you style a specific part of the selected element(s).

```css
selector::pseudo-element {
  property: value;
}

/* example */
p::first-line {
  color: blue;
  text-transform: uppercase;
}
```

**Note**: In contrast to pseudo-classes, pseudo-elements can be used to style a specific part of an element.

## Selectors

### Specificity, inheritance, cascade rules, CSS3 extension, selector attributes

#### [Specificity](https://developer.mozilla.org/en-US/docs/Learn/CSS/Introduction_to_CSS/Cascade_and_inheritance#Specificity)

**Specificity** is basically a measure of how specific a selector is — how many elements it could match. As shown in the example seen above, element selectors have low specificity. Class selectors have a higher specificity, so will win against element selectors. ID selectors have an even higher specificity, so will win against class selectors. A sure way to win against an ID selector is to use `!important`.

| Selector | Thousands | Hundreds | Tens | Ones | Total Specificity |
| ---- | ----- | ---- | ----- | --- | ---- |
|h1|0|0|0|1|0001|
|h1 + p::first-letter|0|0|0|3|0003|
|li > a[href*="en-US"] > .inline-warning|0|0|2|2|0022|
|#identifier|0|1|0|0|0100|
|No selector, with a rule inside an element's style attribute|1|0|0|0|1000|

**Note**: Universal selector (*), combinators (+, >, ~, ' ') and negation pseudo-class (`:not`) have no effect on specificity.

**Note**: If multiple selectors have the same importance and specificity, which selector wins is decided by which comes later in the Source order.

#### [inheritance](https://developer.mozilla.org/en-US/docs/Learn/CSS/Introduction_to_CSS/Cascade_and_inheritance#Inheritance)

elements will take some property values from their parents, but not others

- it makes sense for `font-family` and `color` to be inherited
- it makes sense for `margin`, `padding`, `border`, and `background-image` to **NOT** be inherited.

#### cascade rules

When several CSS rules match the same element, they are **all applied to that element**. Only after that are any conflicting properties evaluated to see which individual styles will win over others.

#### [CSS3 extension](https://mobilesite.github.io/2014/03/06/CSS-selectors/)

- Simple selectors
  - tag
  - class
  - id
  - *
  - [Attribute selectors](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Attribute_selectors)

选择器名称|	选择器符号|	匹配内容
--------|----------|-------
通用选择器|	*|	所有元素
元素类型选择器|	使用元素类型（即元素标签名）进行选择|	所有指定标签名的元素
类选择器|	.类名|	选中class属性中含有指定类名的所有元素
id选择器|	#id名|	所有id属性为指定id的元素
属性选择器|	[条件]|	具有匹配制定条件的属性的元素（此处支持的类型条件请见下表）

元素属性选择器的条件|	说明
------|------
[attr]|	选择定义了attr属性的元素，不管该属性的值是什么，只要定义了该属性就会选中
[attr="val"]|	选择定义了attr属性，且该属性的值为val字符串的元素
[attr~="val"]|	选择定义了attr属性，且该属性具有一个或多个值，其中一个值即为val字符串的元素。例如对于<a class="class1 class2">link</a>以及<a class="class2">link</a>就都可以用选择器[class~="class2"]来进行选中
[attr&#124;="val"]|	选择定义了attr属性，且该属性的值为连字符(-)分割的一个或多个值，其中第一个字符串为val的元素。例如，用选择器[lang&#124;="en"]可以选择<a lang="en-us">en-us</a>以及<a lang="en">en</a>
[attr^="val"]|	选择定义了attr属性，且该属性的值以val字符串打头的元素
[attr$="val"]|	选择定义了attr属性，且该属性的值以val字符串结尾的元素
[attr*="val"]|	选择定义了attr属性，且该属性的值包含val字符串的元素

- extension
  - Pseudo-classes
  - Pseudo-elements
  - Combinators
    - A, B
    - A B
    - A > B
    - A + B
    - A ~ B
  - Multiple selectors

#### selector attributes

what is that???

## Units

### Relative and Absolute Units (em, %, px, pt etc.)

#### absolute

Unit |	Description
-----|-------
in |	inches – 1in is equal to 2.54cm.
cm |	centimeters.
mm |	millimeters.
pt |	points – In CSS, one point is defined as 1/72 inch (0.353mm).
pc |	picas – 1pc is equal to 12pt.
px |	pixel units – 1px is equal to 0.75pt.

#### relative

Unit |	Description
-----|-----
em |	the current font-size
ex |	the x-height of the current font

## Block document model and display

### Standard and box block model

#### box block model

- margin
- border
- padding
- content

### Display property

```css
p.ex1 {display: none;}
p.ex2 {display: inline;}
p.ex3 {display: block;}
p.ex4 {display: inline-block;}
```

## CSS3: Animation and Transformation

### Transition, key frames, transformation, rotation, scaling , blend mode

#### Transition
CSS transitions allows you to change property values smoothly (from one value to another), over a given duration.

#### key frames

The `@keyframes` CSS at-rule is used to define the behavior of one cycle of a CSS animation.

`@keyframes` 规则通过在动画序列中定义关键帧（或waypoints）的样式来控制CSS动画序列中的中间步骤。这比 transition 更能控制动画序列的中间步骤。

```css
@keyframes slidein {
  from {
    margin-left: 100%;
    width: 300%;
  }

  to {
    margin-left: 0%;
    width: 100%;
  }
}
```

#### transformation

The `transform` property applies a 2D or 3D transformation to an element. This property allows you to rotate, scale, move, skew, etc., elements.

#### rotation

The `rotation` property rotates a block-level element counterclockwise around a given point defined by the rotation-point property.

#### scaling

The `scale()` CSS function defines a transformation that resizes an element on the 2D plane. 

#### blend mode

The `<blend-mode>` CSS data type describes how colors should appear when elements overlap. It is used in the background-blend-mode and mix-blend-mode properties.

混合模式是当层重叠时计算像素最终颜色值的方法，每种混合模式采用前景和背景颜色值（分别为顶部颜色和底部颜色），执行其计算并返回颜色值。最终的可见层是对混合层中的每个重叠像素执行混合模式计算的结果。

## CSS3: Media Queries

### Syntax and declaration, types, features/properties, operators, usage

#### Syntax and declaration

Media queries are useful when you want to modify your site or app depending on a device's general type (such as print vs. screen) or specific characteristics and parameters (such as screen resolution or browser viewport width).

```css
@media not|only mediatype and (expressions) {
  CSS-Code;
}
```

#### types

Value |	Description
-----|------
all	| Used for all media type devices
print	| Used for printers
screen	| Used for computer screens, tablets, smart-phones etc.
speech	| Used for screenreaders that "reads" the page out loud

#### features/properties

[Media_features](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries#Media_features)

#### operators

[operators](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries#Logical_operators)

- and
- not
- only
- ,

#### usage

Media queries are used for the following:

- To conditionally apply styles with the CSS `@media` and `@import` at-rules.
- To target specific media for the `<link>`, `<source>`, and other HTML elements.
- To test and monitor media states using the `Window.matchMedia()` and `MediaQueryList.addListener()` JavaScript methods.

## CSS3: Visual effects

### Shadows, rounded corners, gradients, filters etc.

#### Shadows

- text-shadow
- box-shadow

#### rounded corners

- border-radius

#### gradients

CSS gradients let you display smooth transitions between two or more specified colors.

- Linear Gradients (goes down/up/left/right/diagonally)
- Radial Gradients (defined by their center)

```css
background-image: linear-gradient(direction, color-stop1, color-stop2, ...);
```

#### filters

The filter CSS property applies graphical effects like blur or color shift to an element. Filters are commonly used to adjust the rendering of images, backgrounds, and borders.

```css
.mydiv {
  filter: grayscale(50%);
}
```

## CSS3: Web Typography

### Web safe fonts, custom web fonts, font formats, icon fonts, font-face, font generators/services etc.

#### Web safe fonts

Web safe fonts are fonts that are included with most operating systems, the implication of such high availability is that a designer can expect typography involving web safe fonts to appear exactly as intended to most users. 

#### custom web fonts

create a custom font using `@font-face` in CSS

#### font formats

- TTF/OTF
- WOFF
- WOFF2
- SVG
- EOT

#### icon fonts

icon

#### font-face

create a custom font

#### font generators/services

## Positioning

### Document flow

In normal flow, **inline** elements display in the inline direction, that is in the direction words are displayed in a sentence according to the Writing Mode of the document. **Block** elements display one after the other, as paragraphs do in the Writing Mode of that document. In English therefore, inline elements display one after the other, starting on the left, and block elements start at the top and move down the page.

### Position properties

`position: static|absolute|fixed|relative|sticky|initial|inherit;`

### Overflow

The `overflow` property specifies whether to clip the content or to add scrollbars when the content of an element is too big to fit in the specified area.

The `overflow` property has the following values:

- `visible` - Default. The overflow is not clipped. The content renders outside the element's box
- `hidden` - The overflow is clipped, and the rest of the content will be invisible
- `scroll` - The overflow is clipped, and a scrollbar is added to see the rest of the content
- `auto` - Similar to `scroll`, but it adds scrollbars only when necessary

### z-index

The `z-index` property specifies the stack order of an element.

An element with greater stack order is always in front of an element with a lower stack order.

Note: `z-index` only works on positioned elements (position: absolute, position: relative, position: fixed, or position: sticky).

## CSS3: Flexbox

### Flex layout, axis, directions, flexibility, order, alignment

#### Flex layout

The Flexible Box Layout Module, makes it easier to design flexible responsive layout structure without using float or positioning.

`display: flex;`

#### axis

- main axis
- cross axis

#### directions

- row
- row-reverse
- column
- column-reverse
- wrap
- wrap-reverse

#### [flexibility](https://www.w3.org/TR/2011/WD-css3-flexbox-20111129/#flexibility)

The `flex()` function is used to specify the parameters of a flexible length: the positive and negative flexibility, and the preferred size.

#### [order](https://www.w3.org/TR/2011/WD-css3-flexbox-20111129/#ordering-orientation)

`flex-order` assigns flexbox items to ordinal groups.

Ordinal groups control the order in which flexbox items appear. A flexbox will lay out its content starting from the lowest numbered ordinal group and going up. Items with the same ordinal group are laid out in the order they appear in the source document.

#### [alignment](https://www.w3.org/TR/2011/WD-css3-flexbox-20111129/#alignment)

After a flexbox's contents have finished their flexing, they can be aligned in both the main axis with `flex-pack` and the cross axis with `flex-align`. These properties make many common types of alignment trivial, including some things that were very difficult in CSS 2.1, like horizontal and vertical centering.