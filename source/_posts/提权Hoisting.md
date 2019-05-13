---
title: 提权Hoisting
date: 2019-05-10 14:59:33
tags: [js]
---

Hoisting is JavaScript's default behavior of moving all declarations to the top of the current scope (to the top of the current script or the current function).

## Declarations are Hoisted

### var

Hoisted

### The let and const Keywords

Variables and constants declared with let or const are <font color=red>not hoisted!</font>

## Initializations are Not Hoisted

JavaScript only hoists declarations, not initializations.

``` js
var y;
console.log(y); // undefined
y = 7;
```

This is because only the declaration (`var y`), not the initialization (`=7`) is hoisted to the top.

Because of hoisting, `y` has been declared before it is used, but because initializations are not hoisted, the value of `y` is undefined.

[ES6 系列之 let 和 const](https://juejin.im/post/5b0238f66fb9a07aca7a74ba)