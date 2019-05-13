---
title: js Objects
date: 2019-05-10 14:47:33
tags: [js, object]
---

## Object Literal

A JavaScript object literal is a comma-separated list of name-value pairs wrapped in curly braces. Object literals encapsulate data, enclosing it in a tidy package.

an example object literal:

```js
var myObject = {
    sProp: 'some string value',
    numProp: 2,
    bProp: false
};
```

Object literal property values can be of any data type, including array literals, functions, and nested object literals.

### Object Literal Syntax

Object literals are defined using the following syntax rules:

- A colon separates property name from value.
- A comma separates each name-value pair from the next.
- There should be no comma after the last name-value pair.

## several ways how to create object

Objects can be initialized using `new Object()`, `Object.create()`, or using the literal notation (initializer notation). 

```js
// Using the Object() constructor:
var d = new Object();
```

```js
// Using Object.create() method:
var a = Object.create(null);
```

```js
// Using the bracket's syntactig sugar:
var b = {};
```

```js
// Using a function constructor
var Obj = function(name) {
  this.name = name
}
var c = new Obj("hello"); 
```

```js
// Using the function constructor + prototype:
function myObj(){};
myObj.prototype.name = "hello";
var k = new myObj();
```

```js
// Using ES6 class syntax:
class myObject  {
  constructor(name) {
    this.name = name;
  }
}
var e = new myObject("hello");
```

```js
// Singleton pattern:
var l = new function(){
  this.name = "hello";
}
```