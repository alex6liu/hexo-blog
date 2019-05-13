---
title: js Arrays
date: 2019-05-10 09:50:43
tags: [js, array]
---

## Array literals

array literal notation is where you define a new array using just empty brackets.`var myArray = [];`

It is the "new" way of defining arrays, and I suppose it is shorter/cleaner.

The examples below explain the difference between them:

``` js
var a = [],            // these are the same
b = new Array(),   // a and b are arrays with length 0

c = ['foo', 'bar'],           // these are the same
d = new Array('foo', 'bar'),  // c and d are arrays with 2 strings

// these are different:
e = [3],             // e.length == 1, e[0] == 3
f = new Array(3);   // f.length == 3, f[0] == undefined
```

## Methods

- forEach
- map
- push // add to the end
- unshift // add to the front
- pop // remove from the end
- shift // remove from the front
- splice // remove
- slice // sub array

## [Array.length](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/length)

### how Array length property works

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