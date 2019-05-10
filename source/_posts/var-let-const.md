---
title: var let const
date: 2019-05-10 10:32:38
tags: [js]
---

[Scoping with var, let & const](https://blog.usejournal.com/scoping-with-var-let-const-c0060135e09d)
[var vs let vs const in JavaScript](https://tylermcginnis.com/var-let-const/)

## var

- `var` has **functional** scope not block scope

```js
function foo() {
  var bar = 'hello';
  console.log(bar);
}
console.log(bar); // ReferenceError: bar is not defined
```

variables defined with var keyword are not block scoped

``` js
function foo() {
  if (true) {
    var bar = 'hello';
  }
  console.log(bar);
}
foo(); // prints hello
```

- Variables declared with var keyword are hoisted.

```js
function foo() {
  if (false) {
    var bar = 'hello';
  }
  console.log(bar);
}
foo(); // prints undefined
```

The variable bar defined inside if block is visible to the outside block but within the function foo’s scope. This is because the JavaScript engine read the above code as following:

```js
function foo() {
  var bar; // hoisted the declaration but not assignment
  if (false) {
    bar = 'hello';
  }
  console.log(bar); // undefined but no reference error
}
foo(); // prints undefined
```

- Variables defined with var keywords can be redeclared in the same scope

``` js
function foo() {
 var bar = 'hello';
 if (true) {
   var bar = 'hi'; // no error !! replaced easily
 }
 console.log(bar);
}
foo(); // prints hi
```

## let & const 

- Variables declared with `let` & `const` keyword are visible only inside the **block** in which it’s defined.

```js
function foo () {
  if(true) {
    const baz = 'hi';
    let bar = 'hello';
    console.log(baz, bar); // prints hello hi
  }
  console.log(baz, bar); // ReferenceError: baz is not defined
}
foo();
```

- Variables declared with `let` & `const` keyword are **not** subjected to hoisting.

```js
function foo () {
  console.log(bar); // ReferenceError: bar is not defined
  let bar = 'hello';
}
foo();
```

- Variables defined with `let` & `const` keywords **cannot** be redeclared in the same block scope.

``` js
function foo () {
  let bar = 'hello';
  const bar = 'hi';
}
foo(); // SyntaxError: Identifier 'bar' has already been declared
```

But a variable can be redeclared in function scope, given its declared within a **different** block scope.

``` js
function foo () {
  let bar = 'hello';
  if(true) {
    let bar = 'hi';
    console.log(bar); // prints hi
  }
  console.log(bar); // prints hello 
}
```

## Able to explain dead zone concept for [let]

[stackoverflow](https://stackoverflow.com/questions/33198849/what-is-the-temporal-dead-zone)

accessing let and const values before they are initialized can cause a ReferenceError because of something called the temporal dead zone.

```js
console.log(aVar); // undefined
console.log(aLet); // causes ReferenceError: aLet is not defined
var aVar = 1;
let aLet = 2;
```

> It appears from these examples that `let` declarations (and `const`, which works the same way) may not be hoisted, since `aLet` does not appear to exist before it is assigned a value.

> That is not the case, however—`let` and `const` are **hoisted** (like `var`, `class` and `function`), but there is a period between entering scope and being declared where they cannot be accessed. This period is the **temporal dead zone** (TDZ).

> The TDZ ends when `aLet` is declared, rather than assigned:

``` js
let and const have two broad differences from var:

They are block scoped.
Accessing a var before it is declared has the result undefined; accessing a let or const before it is declared throws ReferenceError:
console.log(aVar); // undefined
console.log(aLet); // causes ReferenceError: aLet is not defined
var aVar = 1;
let aLet = 2;
 Run code snippetExpand snippet
It appears from these examples that let declarations (and const, which works the same way) may not be hoisted, since aLet does not appear to exist before it is assigned a value.

That is not the case, however—let and const are hoisted (like var, class and function), but there is a period between entering scope and being declared where they cannot be accessed. This period is the temporal dead zone (TDZ).

The TDZ ends when aLet is declared, rather than assigned:

//console.log(aLet)  // would throw ReferenceError

let aLet;
console.log(aLet); // undefined
aLet = 10;
console.log(aLet); // 10
```

This example shows that `let` is hoisted:

``` js
let x = 'outer value';
(function() {
  // start TDZ for x
  console.log(x);
  let x = 'inner value'; // declaration ends TDZ for x
}());
```

Accessing `x` in the inner scope still causes a `ReferenceError`. If `let` were not hoisted, it would log `outer value`.

The TDZ is a good thing because it helps to highlight bugs—accessing a value before it has been declared is rarely intentional.