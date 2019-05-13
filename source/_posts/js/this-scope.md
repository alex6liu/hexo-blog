---
title: '[this] scope'
date: 2019-05-13 10:09:43
tags: [js, this]
---

## Global Scope

In a browser, the global scope is the `window` object.

if in your code you simply have: `var x = 9;` You’re actually setting the property `window.x` to 9 (when working in a browser). You could type `window.x = 9`;

## Local Scope

JavaScript scopes at a function level.

```js
function myFunc() {
	var x = 5;
};
console.log(x); //undefined
```

If you declare a variable & forget to use the `var` keyword, that variable is automatically made global. So this code would work:

```js
function myFunc() {
	x = 5;
});
console.log(x); //5
```

## this

`this` is a variable that is automatically set for you when a function is invoked. 

Depending on how a function is invoked, `this` is set differently:

```js
function foo() {
	console.log(this); //global object
};
```

```js
myapp = {};
myapp.foo = function() {
	console.log(this); //points to myapp object
}
```

```js
var link = document.getElementById("myId");
link.addEventListener("click", function() {
	console.log(this); //points to link
}, false);
```

### 在函数内部时，`this`由函数怎么调用来确定。

#### Simple call

简单调用，即独立函数调用。由于`this`没有通过`call`来指定，且`this`必须指向对象，那么默认就指向全局对象。

```js
function f1(){
  return this;
}

f1() === window; // global object
```

在严格模式下，`this`保持进入execution context时被设置的值。如果没有设置，那么默认是`undefined`。它可以被设置为任意值(**包括`null/undefined/1`等等基础值，不会被转换成对象**)。

```js
function f2(){
  "use strict"; // see strict mode
  return this;
}

f2() === undefined;
```

#### Arrow functions

在箭头函数中，`this`由词法/静态作用域设置（set lexically）。它被设置为包含它的execution context的`this`，并且不再被调用方式影响（call/apply/bind）。

```js
var globalObject = this;
var foo = (() => this);
console.log(foo() === globalObject); // true

// Call as a method of a object
var obj = {foo: foo};
console.log(obj.foo() === globalObject); // true

// Attempt to set this using call
console.log(foo.call(obj) === globalObject); // true

// Attempt to set this using bind
foo = foo.bind(obj);
console.log(foo() === globalObject); // true
```

#### As an object method

当函数作为对象方法调用时，`this`指向该对象。

```js
var o = {
  prop: 37,
  f: function() {
    return this.prop;
  }
};

console.log(o.f()); // logs 37
```

`this` on the object's prototype chain

原型链上的方法根对象方法一样，作为对象方法调用时`this`指向该对象。

#### 构造函数

在构造函数（函数用`new`调用）中，`this`指向要被constructed的新对象。

#### call和apply

`Function.prototype`上的`call`和`apply`可以指定函数运行时的`this`。

```js
function add(c, d){
  return this.a + this.b + c + d;
}

var o = {a:1, b:3};
add.call(o, 5, 7); // 1 + 3 + 5 + 7 = 16
add.apply(o, [10, 20]); // 1 + 3 + 10 + 20 = 34
```

注意，当用`call`和`apply`而传进去作为`this`的不是对象时，将会调用内置的`ToObject`操作转换成对象。所以4将会装换成`new Number(4)`，而`null/undefined`由于无法转换成对象，全局对象将作为`this`。

#### bind

ES5引进了`Function.prototype.bind`。`f.bind(someObject)`会创建新的函数（函数体和作用域与原函数一致），但`this`被永久绑定到`someObject`，不论你怎么调用。

#### As a DOM event handler

`this`自动设置为触发事件的dom元素。

## 参考链接

[从这两套题，重新认识JS的this、作用域、闭包、对象](https://juejin.im/post/59aa71d56fb9a0248d24fae3)
[深入理解JS中声明提升、作用域（链）和`this`关键字](https://github.com/creeperyang/blog/issues/16)