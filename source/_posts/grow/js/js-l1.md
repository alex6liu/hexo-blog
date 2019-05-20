---
title: js l1
date: 2019-05-14 09:49:06
tags: [js, l1]
---

value代表这个值。

literals代表如何表达这个值。

## Arrays

### Array literals

`var array = [1, 2, 3];`

### Know several options how to create Array

``` js
var a = [],            // these are the same
b = new Array(),   // a and b are arrays with length 0

c = ['foo', 'bar'],           // these are the same
d = new Array('foo', 'bar'),  // c and d are arrays with 2 strings

// these are different:
e = [3],             // e.length == 1, e[0] == 3
f = new Array(3);   // f.length == 3, f[0] == undefined
```

### Array length

`Array.length()`

### Know how Array length property works

- Reading the length

1) For a dense array, this means that the length corresponds strictly to the number of elements:

``` js
var fruits = ['orange', 'apple', 'banana']; //fruits is a dense array  
fruits.length // prints 3, the real count of elements

fruits.push('mango');  
fruits.length // prints 4, one element was added

var empty = [];  
empty.length // prints 0, empty array  
```

The dense array does not have empties and the number of items corresponds to highestIndex + 1. In [3, 5, 7, 8] the highest index is 3 of element 8, thus the array size is 3 + 1 = 4.

2) In a sparse array (which has empties), the number of elements does not correspond to length value, but still is determined by the highest index:

``` js
var animals = ['cat', 'dog', , 'monkey']; // animals is sparse  
animals.length // prints 4, but real number of elements is 3

var words = ['hello'];  
words[6] = 'welcome'; //the highest index is 6. words is sparse  
words.length //prints 7, based on highest index 
```

- Modifying the length

1) Modifying the property leads to cut the elements (if the new value is smaller than the highest index):

``` js
var numbers = [1, 3, 5, 7, 8];

numbers.length = 3; // modify the array length  
numbers // prints [1, 3, 5], elements 7 and 8 are removed
```

2) or creating a sparse array (if the new value is bigger than the highest index):

``` js
var osTypes = ['OS X', 'Linux', 'Windows'];

osTypes.length = 5; // creating a sparse array. Elements at indexes 3 and 4  
                    // do not exist

osTypes // prints ['OS X', 'Linux', 'Windows', , , ] 
```

## Closures Basics

### Nested functions

```js
function verify (name) {            // outer function  
    function isJohn() {             // inner function
        return name === "John";     // full access to argument        
    }
    if (isJohn()) {
        alert("Yep, this is John");
    }
}
verify("John");
```

### Able to create nested functions

### Understand variables visibility for nested scopes

``` js
function outer() {
	var a = 1;

	function inner() {
		var b = 2;

		// we can access both `a` and `b` here
		console.log( a + b );	// 3
	}

	inner();

	// we can only access `a` here
	console.log( a );			// 1
}

outer();
```

## ECMAScript Basics

### cost, let declarations
### Understand differences between [var], [let] and [const]
### Know block scope and [let] visibility

Variables declared with `let` & `const` keyword are visible only inside the **block** in which it’s defined.

### Able to explain dead zone concept for [let]

accessing let and const values before they are initialized can cause a ReferenceError because of something called the temporal dead zone(暂时性死区).

当程序的控制流程在新的作用域（module function 或 block 作用域）进行实例化时，在此作用域中用let/const声明的变量会先在作用域中被创建出来，但因此时还未进行词法绑定，所以是不能被访问的，如果访问就会抛出错误。因此，在这运行流程进入作用域创建变量，到变量可以被访问之间的这一段时间，就称之为暂时死区。

```js
console.log(aVar); // undefined
console.log(aLet); // causes ReferenceError: aLet is not defined
var aVar = 1;
let aLet = 2;
```

### Arrow functions

`() => {}`

### Know difference between arrow and usual functions

- 箭头函数不绑定`Arguments` 对象
- 箭头函数没有定义`this`绑定
- 箭头函数不能用作构造器，和 `new`一起用会抛出错误。
- 箭头函数没有`prototype`属性。
-  `yield` 关键字通常不能在箭头函数中使用（除非是嵌套在允许使用的函数内）。因此，箭头函数不能用作生成器。

### Able to discover cases for both arrow and usual functions using

## Expressions, Operators, Statements

### Operators
### Know logic, mathematic operators

- logic: `||`, `&&`, `!`
- math: `+`, etc

### Know operators priority

`i++` 优先级高于 `++i`

### Be able to use operators
### Conditions
### Know and able to use conditional statements
### Loops
### Know loop types
### Understand loops differences and applicability

- A `for` loop is used when you know the number of iterations the loop needs to make. 
- A `while` loop can be used when you need your loop to run an unknown number of times until a specific condition is met. 
- `for/in` - loops through the properties of an object. `while` - loops through a block of code while a specified condition is true. `do/while` - loops through a block of code once, and then repeats the loop while a specified condition is true.
- `for/of`

### Be able to skip loop iteration or break loop

- The `break` statement "jumps out" of a loop.

- The `continue` statement "jumps over" one iteration in the loop.

## Functions

### Function declaration/expression

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

### Know both Function expression and Function declaration

- Function Declaration

```js
function foo() { ... }
```

Because of function hoisting, the function declared this way can be called both after and before the definition.

- Function Expression

1. Named Function Expression

```js
var foo = function bar() { ... }
```

2. Anonymous Function Expression

```js
var foo = function() { ... }
```

`foo()` can be called only after creation.

### Be able to explain declaration/expression differences

- Function **declarations** load before any code is executed.
- Function **expressions** load only when the interpreter reaches that line of code.

## Objects

### Object literals

```js
var myObject = {
    sProp: 'some string value',
    numProp: 2,
    bProp: false
};
```

### Know several ways how to create object

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

## Variables, Values, Data Types

### Variables - Know how to declare variables
### Values - Know how to assign values to variables
### Literals - Know basic String, Number, Object, Array literals
### Primitive Data Types

- Boolean — true or false
- Null — no value
- Undefined — a declared variable but hasn’t been given a value
- Number — integers, floats, etc
- String — an array of characters i.e words
- Symbol — a unique value that's not equal to any other value

### Discover primitive data types

## Advanced Expressions

### Hoisting

JavaScript 仅提升声明，而不提升初始化。如果你先使用的变量，再声明并初始化它，变量的值将是 undefined。

```js
console.log(a) // undefined
var a = 5
```

```js
var x = 1;                 // 声明 + 初始化 x
console.log(x + " " + y);  // '1 undefined'
var y = 2;                 // 声明 + 初始化 y


//上面的代码和下面的代码是一样的 
var x = 1;                 // 声明 + 初始化 x
var y;                     //声明 y
console.log(x + " " + y);  //y 是未定义的
y = 2;                     // 初始化  y 
```

### Understand hoisting concept

- 变量申明跟函式申明都會提升(函数优先级高)

```js
console.log(a) //[Function: a]
var a
function a(){}
```

- 只有申明会提升，賦值不会提升
- 別忘了函数里面还有传进来的参数

```js
function test(v){
  console.log(v)  // 10, 因为调用了test(10)
  var v = 3
}
test(10)
```

**如果没有hoisting, 无法完成函数的互相调用**

```js
function loop(n){
  if (n>1) {
    logEvenOrOdd(--n)
  }
}
  
function logEvenOrOdd(n) {
  console.log(n, n % 2 ? 'Odd' : 'Even')
  loop(n)
}
  
loop(10)
```

#### [理解 variable object 和 execution context](https://blog.techbridge.cc/2018/11/10/javascript-hoisting/)

- 把参数放到 VO 里面并定好值，传进来什么就是什么，沒有值的设成 undefined
- 把 function 申明放到 VO 里，如果已经有同名的就覆盖
- 把变量申明放到 VO 里，如果已经有同名的则忽略

### Able to use hoisting in development
### Auto data type conversion

#### 自动转换为布尔值

JavaScript 遇到预期为布尔值的地方（比如`if`语句的条件部分），就会将非布尔值的参数自动转换为布尔值。系统内部会自动调用`Boolean`函数。

因此除了以下五个值，其他都是自动转为`true`。

``` js
undefined
null
+0或-0
NaN
''（空字符串）
```

下面两种写法，有时也用于将一个表达式转为布尔值。它们内部调用的也是`Boolean`函数。

```js
// 写法一
expression ? true : false

// 写法二
!! expression
```

#### 自动转换为字符串

JavaScript 遇到预期为字符串的地方，就会将非字符串的值自动转为字符串。具体规则是，先将复合类型的值转为原始类型的值，再将原始类型的值转为字符串。

字符串的自动转换，主要发生在字符串的加法运算时。当一个值为字符串，另一个值为非字符串，则后者转为字符串。

```js
'5' + 1 // '51'
'5' + true // "5true"
'5' + false // "5false"
'5' + {} // "5[object Object]"
'5' + [] // "5"
'5' + function (){} // "5function (){}"
'5' + undefined // "5undefined"
'5' + null // "5null"
```

#### 自动转换为数值

JavaScript 遇到预期为数值的地方，就会将参数值自动转换为数值。系统内部会自动调用`Number`函数。

除了加法运算符（+）有可能把运算子转为字符串，其他运算符都会把运算子自动转成数值。

```js
'5' - '2' // 3
'5' * '2' // 10
true - 1  // 0
false - 1 // -1
'1' - 1   // 0
'5' * []    // 0
false / '5' // 0
'abc' - 1   // NaN
null + 1 // 1
undefined + 1 // NaN
```

**注意**：`null`转为数值时为0，而`undefined`转为数值时为`NaN`。

一元运算符也会把运算子转成数值。

```js
+'abc' // NaN
-'abc' // NaN
+true // 1
-false // 0
```

### [Know rules of auto data types conversion](https://juejin.im/entry/584918612f301e005716add6)

### Be able to discover cases of implicit data types conversion into boolean, string, number
### Strict comparison

- `===` 严格相等，会比较两个值的类型和值
- `==`  抽象相等，比较时，会先进行类型转换，然后再比较值

### Be able to discover difference between strict and non-strict comparison
### Be able to provide use cases of both types of comparison

## Advanced Functions

### [arguments](https://segmentfault.com/a/1190000014196082)
### Understand [arguments] and dynamic amount of parameters

- (1) 由于 JavaScript 允许函数有不定数目的参数，所以需要一种机制，可以在函数体内部读取所有参数。这就是arguments对象的由来。

- (2) arguments对象包含了函数运行时的所有参数，arguments[0]就是第一个参数，arguments[1]就是第二个参数，以此类推。这个对象只有在函数体内部，才可以使用。

- arguments对象的length属性显示实参的个数，函数的length属性显示形参的个数

注意:

- （1）需要注意的是，虽然arguments很像数组，但它是一个对象。数组专有的方法（比如slice和forEach），不能在arguments对象上直接使用。
- （2）如果要让arguments对象使用数组方法，真正的解决方法是将arguments转为真正的数组。
- （3）下面是两种常用的转换方法：slice方法和逐一填入新数组。

### Be able to use [arguments], retrieve additional parameters

```js
function con(a,b, ...additional){
  console.log(a,b)
}

con(10, 11, 12, 12)
```

### [this] scope

[link](https://www.ibm.com/developerworks/cn/web/1207_wangqf_jsthis/index.html)

函数也可以直接被调用，此时 this 绑定到全局对象。在浏览器中，window 就是该全局对象。函数被调用时，this 被绑定到全局对象

```js
function makeNoSense(x) { 
this.x = x; 
} 
 
makeNoSense(5); 
x;// x 已经成为一个值为 5 的全局变量
```

对于内部函数，即声明在另外一个函数体内的函数，这种绑定到全局对象的方式会产生另外一个问题。

```js
var point = { 
x : 0, 
y : 0, 
moveTo : function(x, y) { 
    // 内部函数
    var moveX = function(x) { 
    this.x = x;//this 绑定到了哪里？
   }; 
   // 内部函数
   var moveY = function(y) { 
   this.y = y;//this 绑定到了哪里？
   }; 
 
   moveX(x); 
   moveY(y); 
   } 
}; 
point.moveTo(1, 1); 
point.x; //==>0 
point.y; //==>0 
x; //==>1 
y; //==>1
```

这属于 JavaScript 的设计缺陷，正确的设计方式是内部函数的 this 应该绑定到其外层函数对应的对象上，为了规避这一设计缺陷，聪明的 JavaScript 程序员想出了变量替代的方法，约定俗成，该变量一般被命名为 that。

```js
var point = { 
x : 0, 
y : 0, 
moveTo : function(x, y) { 
     var that = this; 
    // 内部函数
    var moveX = function(x) { 
    that.x = x; 
    }; 
    // 内部函数
    var moveY = function(y) { 
    that.y = y; 
    } 
    moveX(x); 
    moveY(y); 
    } 
}; 
point.moveTo(1, 1); 
point.x; //==>1 
point.y; //==>1
```

### Understand difference between function and method

- 函数（function）是可以执行的javascript代码块，由javascript程序定义或javascript实现预定义。函数可以带有实际参数或者形式参数，用于指定这个函数执行计算要使用的一个或多个值，而且还可以返回值，以表示计算的结果。

- 方法（method）是通过对象调用的javascript函数。也就是说，方法也是函数，只是比较特殊的函数。

假设有一个函数是fn，一个对象是obj，那么就可以定义一个method：

```js
obj.method = fn;

obj.method();    //定义之后的调用
```

函数和方法之间并没有技术上的区别，真正的差别在于设计和目的，方法是用来对this对象进行操作的，this对象是方法的一个重要属性，当this对象出现在方法主体内部，this值就指向调用该方法的对象。而函数通常是独立的，并不需要经常使用this对象。

### Understand how [this] works, realize [this] possible issues

[111](#this-scope)

### Manage [this] scope
### Be able to replace [this] scope
### Be able to use [call] and [apply] Function build-in methods

## Arrays Built-in methods

### Know how to copy array

The `Array.from()` method creates a new, shallow-copied `Array` instance from an array-like or iterable object.

```js
console.log(Array.from('foo'));
// expected output: Array ["f", "o", "o"]

console.log(Array.from([1, 2, 3], x => x + x));
// expected output: Array [2, 4, 6]
```

### Know how to copy array part

The `slice()` method returns a shallow copy of a portion of an array into a new array object selected from begin to end (end not included). The original array will not be modified.

### Know how to modify array

- pop
- push
- shift
- unshift

## Arrays Iterating, Sorting, Filtering

### Know how to sort Array

`Array.sort()`

### Be able to custom sorting for Array

```js
function compare(a, b) {
  if (a is less than b by some ordering criterion) {
    return -1;
  }
  if (a is greater than b by the ordering criterion) {
    return 1;
  }
  // a must be equal to b
  return 0;
}
```

Example: 

``` js
var numbers = [4, 2, 5, 1, 3];
numbers.sort(function(a, b) {
  return a - b;
});
console.log(numbers);

// [1, 2, 3, 4, 5]
```

### Be able to filter Array elements

The `filter()` method creates a new array with all elements that pass the test implemented by the provided function.

```js
var words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];

const result = words.filter(word => word.length > 6);

console.log(result);
// expected output: Array ["exuberant", "destruction", "present"]
```

### Know several method how to iterate Array elements

- Basic For Loop

- Lodash forEach

- The `forEach()` method executes a provided function once for each array element.

- The `map()` method creates a new array with the results of calling a provided function on every element in the calling array.

- The `entries()` method returns a new Array Iterator object that contains the key/value pairs for each index in the array.

### Be able to compare Hash and Array performance

## Closures Advanced

### Context (lexical environment)


### Understand function creation context (lexical environment)



### Be able to explain difference between scope and context

作用域就是变量和函数的可访问范围，控制着变量和函数的可见性与生命周期，换句话说，作用域决定了代码区块中变量和其他资源的可见性。在JavaScript中变量的作用域有全局作用域和局部作用域。JavaScript采用词法作用域(lexical scoping)，也就是静态作用域。

上下文(context)是用来指定代码某些特定部分中this的值。作用域(scope) 是指变量的可访问性，上下文(context)是指this在同一作用域内的值。我们也可以使用call()、apply()、bind()、箭头函数等改变上下文。在浏览器中在全局作用域(scope)中上下文中始终是Window对象。在Node.js中在全局作用域(scope)中上下文中始终是Global 对象。

上下文始终坚持一个原理：this 永远指向最后调用它的那个对象

### Inner/outer lexical environment

```js
let a = 'global';
  function outer() {
    let b = 'outer';
    function inner() {
      let c = 'inner'
      console.log(c);   // prints 'inner'
      console.log(b);   // prints 'outer'
      console.log(a);   // prints 'global'
    }
    console.log(a);     // prints 'global'
    console.log(b);     // prints 'outer'
    inner();
  }
outer();
console.log(a);         // prints 'global'
```

Here the `inner` function can access the variables defined in its own scope, the `outer` function’s scope, and the global scope. And the `outer` function can access the variable defined in its own scope and the global scope.

So a scope chain of the above code would be like this:

```js
Global {
  outer {
    inner
  }
}
```

Notice that `inner` function is surrounded by the lexical scope of `outer` function which is, in turn, surrounded by the global scope. That’s why the `inner` function can access the variables defined in `outer` function and the global scope.

### Understand lexical environment traversing mechanism

[link](https://blog.bitsrc.io/a-beginners-guide-to-closures-in-javascript-97d372284dda)

To really understand how closures work in JavaScript, we have to understand the two most important concepts in JavaScript, that is, 1) Execution Context and 2) Lexical Environment.

#### Execution Context

An execution context is an abstract environment where the JavaScript code is evaluated and executed. When the global code is executed, it’s executed inside the global execution context, and the function code is executed inside the function execution context.

There can only be one currently running execution context (Because JavaScript is single threaded language), which is managed by a stack data structure known as Execution Stack or Call Stack.

An execution stack is a stack with LIFO (Last in, first out) structure in which items can only be added or removed from the top of the stack only.

The currently running execution context will be always on the top of the stack, and when the function which is currently running completes, its execution context is popped off from the stack and the control reaches to the execution context below it in the stack.

#### Lexical Environment

Every time the JavaScript engine creates an execution context to execute the function or global code, it also creates a new lexical environment to store the variable defined in that function during the execution of that function.

A lexical environment is a data structure that holds identifier-variable mapping. (here identifier refers to the name of variables/functions, and the variable is the reference to actual object [including function type object] or primitive value).

A Lexical Environment has two components: (1) the environment record and (2) a reference to the outer environment.

The environment record is the actual place where the variable and function declarations are stored.
The reference to the outer environment means it has access to its outer (parent) lexical environment. This component is the most important in order to understand how closures work.
A lexical environment conceptually looks like this:

```js
lexicalEnvironment = {
  environmentRecord: {
    <identifier> : <value>,
    <identifier> : <value>
  }
  outer: < Reference to the parent lexical environment>
}
```

So let’s again take a look at above code snippet:

```js
let a = 'Hello World!';
function first() {
  let b = 25;  
  console.log('Inside first function');
}
first();
console.log('Inside global execution context');
```

When the JavaScript engine creates a global execution context to execute global code, it also creates a new lexical environment to store the variables and functions defined in the global scope. So the lexical environment for the global scope will look like this:

```js
globalLexicalEnvironment = {
  environmentRecord: {
      a     : 'Hello World!',
      first : < reference to function object >
  }
  outer: null
}
```

Here the outer lexical environment is set to null because there is no outer lexical environment for the global scope.

When the engine creates execution context for first() function, it also creates a lexical environment to store variables defined in that function during execution of the function. So the lexical environment of the function will look like this:

```js
functionLexicalEnvironment = {
  environmentRecord: {
      b    : 25,
  }
  outer: <globalLexicalEnvironment>
}
```

The outer lexical environment of the function is set to the global lexical environment because the function is surrounded by the global scope in the source code.

Note — When a function completes, its execution context is removed from the stack, but its lexical environment may or may not be removed from the memory depending on if that lexical environment is referenced by any other lexical environments in their outer lexical environment property.

### Understand connection between function and lexical environment
### Be able to discover cases where lexical environment required
### Be able to create and use closures

## ECMAScript Advanced

### Promises

[promise](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)

Syntax: `new Promise( function(resolve, reject) {...} /* executor */  );`

Promise 对象是一个代理对象（代理一个值），被代理的值在Promise对象创建时可能是未知的。它允许你为异步操作的成功和失败分别绑定相应的处理方法（handlers）。 这让异步方法可以像同步方法那样返回值，但并不是立即返回最终执行结果，而是一个能代表未来出现的结果的promise对象

### Know how [Promise] works

一个 Promise有以下几种状态:

- pending: 初始状态，既不是成功，也不是失败状态。
- fulfilled: 意味着操作成功完成。
- rejected: 意味着操作失败。

![](https://raw.githubusercontent.com/alex6liu/blog-images/master/js/promise.png)

### Know promise chain pattern

A common need is to execute two or more asynchronous operations back to back, where each subsequent operation starts when the previous operation succeeds, with the result from the previous step. We accomplish this by creating a **promise chain**.

the `then()` function returns a **new promise**

```js
doSomething()
.then(function(result) {
  return doSomethingElse(result);
})
.then(function(newResult) {
  return doThirdThing(newResult);
})
.then(function(finalResult) {
  console.log('Got the final result: ' + finalResult);
})
.catch(failureCallback);
```

### Be able to compare promise and callback patterns

callback hell

### Be able to handle errors in promises
### Be able to use promisification pattern
### Iterators

[link](https://segmentfault.com/a/1190000010747122)

Iterators -> ES5

JavaScript 中 迭代器是一个对象，它提供了一个next() 方法，用来返回序列中的下一项。这个方法返回包含两个属性：done和 value。

迭代器对象一旦被创建，就可以反复调用next()。

```js
function makeIterator(array){
    var nextIndex = 0;
    return {
       next: function(){
           return nextIndex < array.length ?
               {value: array[nextIndex++], done: false} :
               {done: true};
       }
    };
}
```

一旦初始化，`next()`方法可以用来依次访问对象中的键值：

```js
var it = makeIterator(['yo', 'ya']);
console.log(it.next().value); // 'yo'
console.log(it.next().value); // 'ya'
console.log(it.next().done);  // true
```

### Know [Iterator] interface
### Be able to create custom iterator

Iterator 返回一个对象，这个对象存在一个next()方法，当next()方法被调用时，返回格式{ value: 1, done: false}的结果对象。
因此，我们可以这么定义：迭代器是一个拥有next()方法的特殊对象，每次调用next()都返回一个结果对象。

### Generators

Generators -> ES6 下的 Iterators

虽然自定义的迭代器是一个有用的工具，但由于需要显式地维护其内部状态，因此需要谨慎地创建。Generators提供了一个强大的选择：它允许你定义一个包含自有迭代算法的函数， 同时它可以自动维护自己的状态。

GeneratorFunction 是一个可以作为迭代器工厂的特殊函数。当它被执行时会返回一个新的Generator对象。 如果使用function*语法，则函数将变为GeneratorFunction。

```js
function* idMaker() {
  var index = 0;
  while(true)
    yield index++;
}

var gen = idMaker();

console.log(gen.next().value); // 0
console.log(gen.next().value); // 1
console.log(gen.next().value); // 2
// ...
```

### Know generator syntax

`function *createIterator(items) { ... }`

或者

`let createIterator = function *(item) { ... }`

### Be able to compare generator and iterator

- iterator -> es5
- generator -> es6, 使用yield

### Understand how [yield] works

yield 关键字用来暂停和恢复一个生成器函数

### Understand plain async code
### Be able to handle errors in generators

在生成器内部通过try-catch代码块来捕获这些错误：

```js
function *createIterator() {
    let first = yield 1;
    let second;
    
    try {
        second = yield first + 2;  // yield 4 + 2, 然后抛出错误
    } catch(e) {
        second = 6;
    }
    yield second + 3;
}

let iterator = createIterator();

console.log(iterator.next());                    // "{ value: 1, done: false }"
console.log(iterator.next(4));                   // "{ value: 6, done: false }"
console.log(iterator.throw(new Error("Boom")));  // "{ value: 9, done: false }"
console.log(iterator.next());                    // "{ value: undefined, done: true }"
```

## ECMAScript Classes

### Class declaration

要声明一个类，你可以使用带有class关键字的类名

### Know [class] declaration syntax

```js
class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
}
```

### Know how [class] declaration works under the hood

函数声明和类声明之间的一个重要区别是函数声明会提升，类声明不会。你首先需要声明你的类，然后访问它，否则会抛出一个ReferenceError

### Understand difference between [class] and function constructor



### Understand difference between method and [class] method
### Be able to develop in OOP style using [class] declaration
### [constructor] keyword
### Inheritance
### Know [extends] syntax and how it works
### Getter/setter
### Be able to create getter / setter [class] methods

## ECMAScript Data Types & Expressions

### Object [keys/values]
### Object calculated props
### [Symbol] data type
### Know [Symbol] data type specific
### Be able to explain difference between usual object key and symbol
### [Set/Map] data types
### [WeakSet/WeakMap] data types

## ECMAScript Intermediate

### Function default parameters

```js
function multiply(a, b = 1) {
  return a * b;
}

console.log(multiply(5, 2));
// expected output: 10

console.log(multiply(5));
// expected output: 5
```

### Discover default parameters concept and limitations

- 默认值表达式在函数调用时自左向右求值，这也意味着，默认表达式可以使用该参数之前已经填充好的其它参数值。
- 传递 `undefined` 值等效于不传值
- 没有默认值的参数隐式默认为 `undefined`

### Spread operator for Function

[mdn](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Spread_syntax)

展开语法(Spread syntax), 可以在函数调用/数组构造时, 将数组表达式或者string在语法层面展开；还可以在构造字面量对象时, 将对象表达式按key-value的方式展开。(译者注: 字面量一般指 [1, 2, 3] 或者 {name: "mdn"} 这种简洁的构造方式)

```js
function sum(x, y, z) {
  return x + y + z;
}

const numbers = [1, 2, 3];

console.log(sum(...numbers));
// expected output: 6

console.log(sum.apply(null, numbers));
// expected output: 6
```

### Know how to use spread operator for Function arguments

- 替代 `apply()`

```js
function myFunction(x, y, z) { }
var args = [0, 1, 2];
myFunction.apply(null, args);

function myFunction(x, y, z) { }
var args = [0, 1, 2];
myFunction(...args);
```

### Be able to compare [arguments] and spread operator

[mdn](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/Rest_parameters)

- 替代 `arguments`

### Spread operator for Array
### Understand and able to use spread operator for Array concatenation

- 合并数组

```js
var arr1 = ['two', 'three'];
var arr2 = ['one', ...arr1, 'four', 'five'];

// ["one", "two", "three", "four", "five"]
```

- 拷贝数组

```js
var arr = [1,2,3];
var arr2 = [...arr]; // 和arr.slice()差不多
arr2.push(4)
```

### Destruction

[mdn](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

```js
var a, b, rest;
[a, b] = [10, 20];

console.log(a);
// expected output: 10

console.log(b);
// expected output: 20

[a, b, ...rest] = [10, 20, 30, 40, 50];

console.log(rest);
// expected output: [30,40,50]
```

### Be able to discover destruction concept



### Understand variables and Function arguments destruction
### String templates

`string text ${expression} string text`

### Know String template syntax and rules

在模版字符串内使用反引号（`）时，需要在它前面加转义符（\）。

```js
`\`` === "`" // --> true
```

### [for..of] loop

[mdn](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/for...of)

```js
for (variable of iterable) {
    //statements
}

// example
let iterable = [10, 20, 30];

for (let value of iterable) {
    value += 1;
    console.log(value);
}
// 11
// 21
// 31
```

对于for...of的循环，可以由break, throw  continue    或return终止。

### Know how [for..of] loop works

1. 首先调用(for…of…)的对象的属性里必须有一个函数，它的函数名必须为Symbol.iterator； 
2. 该函数的返回值必须为一个对象，且对象内包含一个next()函数； 
3. next()函数也必须有一个返回值，返回值类型也为一个对象。其包含两个属性：done和value。 
4. 程序会根据该对象的done来处理后续行为，如果done为false，则把该对象的value赋值给of前面的变量。否则就会继续调用next，直至done为true再终止。

### Be able to compare [for..of] loop with other types of loops

- `for...in` 语句以原始插入顺序迭代对象的可枚举属性。
- `for...of` 语句遍历可迭代对象定义要迭代的数据。

1. 与forEach()不同的是，(for…of…)可以正确响应break、continue和return语句; 
2. 与(for..in…)相比，除了能够快速的得到属性值外，它还避开了（for…in…)所有的缺陷； 
3. (for..of…)循环不仅支持数组，还支持大多数类数组对象，例如DOM NodeList对象； 
4. (for..of…)循环也支持字符串遍历，它将字符串视为一系列的Unicode字符来进行遍历；

## Functional Inheritance

[JavaScript常用八种继承方案](https://juejin.im/post/5bcb2e295188255c55472db0)

### Rent a constructor

```js
function Father(){
   this.num = ['12'];
}
function Child(){
  //继承father
   Father.call(this);
}

var c1 = new Child();
c1.num.push(13);
console.log(c1.num);//12,13
var c2 = new Child();
console.log(c2.num);//12
```

### Know functional inheritance pattern



### Be able to explain difference between functional and prototypal inheritance
### Be able to discover benefits and drawback of both prototypal and functional inheritance
### Mix-ins
### Know mix-in pattern
### Know mix-in specific and limitations
### Able to explain benefits and drawbacks comparing with inheritance

## Functional Patterns

### Immediate function
### Know immediate function pattern
### Be able to explain the purposes of immediate function usage
### Callback (Function as argument)
### Know callback pattern
### Understand callback limitations (callback hell)
### Binding
### Know how to bind [this] scope to function
### Be able to provide cases when it's required

## Functional Scope

### Know global scope and functional scope
### Know variables visibility areas
### Understand nested scopes and able work with them

## Functions Parameters / Arguments

### Know how to define Function parameters
### Know difference between parameters passing by value and by reference
### Know how to handle dynamic amount of Function parameters

## JavaScript Errors

### [try..catch] statement
### Know how to handle errors
### Be able to explain [try..catch] performance issues
### Throw errors
### Custom errors

## Object as Hash

### Be able to use Object as a Hash
### Be able to loop though Object keys

## Object Oriented Programming

### [new] keyword
### Understand how [new] keyword works
### Understand the difference in calling function with / without [new] keyword
### Function constructor
### Know function constructor concept
### Know function constructor pattern
### Able to create constructor functions
### Public, private, static members
### Know how to create public members
### Know how to create private members
### Know how to create static members
### Understand OOP emulation patterns and conventions

## Objects Built-in methods

### Know how to use built-in methods
### Know static Object methods

## Prototypal Inheritance Basics

### [__proto__] property
### Understand [__proto__] object property
### Understand how interpreter traverses object properties
### Able to work with object [__proto__]
### Able to use [Object.create] and define [__proto__] explicitly
### Able to set / get object prototype
### [prototype] property
### Know function [prototype] property
### Understand dependency between function constructor [prototype] and instance [__proto__]
### Able to create 'class' methods using function [prototype] property

## Regular Expressions Basics

### String methods
### Know String methods for regular expressions
### Understand regular expressions performance issues
### RegExp methods and flags
### Metacharacters
### Quantifiers

## optional

## Advanced Functional Patterns

### Chaining
### Know chaining pattern and cases where it will be useful
### Currying
### Know how to bind arguments to function
### Memorization
### Know memorization optimization
### Understand problem with non-primitive arguments memorization

## ECMAScript Classes Advanced

### [super] keyword
### Understand [super] reference
### Able to use [super] reference (in constructor, in class methods)
### [static] keyword
### Know static members concept
### Be able to create [class] static properties and methods

## Functions Recursion

### Know recursion concept and able to use it
### Able to explain recursion risks, benefits and drawbacks

## Object Property Descriptor

### Know how to use property descriptors
### Be able to explain enumerable, configurable, writable property attributes
### Be able to create property getter/setter

## Prototypal Inheritance Advanced

### Temporary constructor
### Know prototypal inheritance mechanism
### Know prototypal inheritance temporary constructor pattern
### Be able to explain prototypal chain from instance to its 'class' and 'class' parent
### Be able to develop in OOP style using prototypal inheritance pattern
### [instanceof] operator
### Be able to use [instanceof] operator
### Know how [instanceof] operator works

## Regular Expressions Advanced

### Ranges
### Grouping
### Greedy and lazy search
### Replacements

## Strict mode

### Strict mode activation
### Strict mode limitations