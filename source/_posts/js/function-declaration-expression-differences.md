---
title: function declaration/expression differences
date: 2019-05-10 14:40:27
tags: [js]
---

- Function **declarations** load before any code is executed.

- Function **expressions** load only when the interpreter reaches that line of code.

So if you try to call a function expression before it's loaded, you'll get an error! If you call a function declaration instead, it'll always work, because no code can be called until all declarations are loaded.

Example: Function Expression

``` js
alert(foo()); // ERROR! foo wasn't loaded yet
var foo = function() { return 5; } 
```

Example: Function Declaration

``` js
alert(foo()); // Alerts 5. Declarations are loaded before any code can run.
function foo() { return 5; } 
```

## Function Declaration

```js
function foo() { ... }
```

Because of function hoisting, the function declared this way can be called both after and before the definition.

## Function Expression

1. Named Function Expression

```js
var foo = function bar() { ... }
```

2. Anonymous Function Expression

```js
var foo = function() { ... }
```

`foo()` can be called only after creation.
