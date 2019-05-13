---
title: Parameters & Arguments in JavaScript
date: 2019-05-13 09:59:00
tags: [js]
---

[link](https://codeburst.io/parameters-arguments-in-javascript-eb1d8bd0ef04)

- Parameters are variables listed as a part of the function definition.
- Arguments are values passed to the function when it is invoked.

``` js
// Basic function with three parameters that logs the sum of all the parameters
function argCheck(parameter1, parameter2, parameter3){
  console.log(parameter1 + parameter2 + parameter3);
}

// Function with extra arguments
argCheck(1,2,3,4);
// Logs 6 (1 + 2 + 3, ignores 4)

// Function with missing arguments
argCheck(1,2);
// Logs NaN because by default if a corresponding argument is missing, it is set to undefined. 
// parameter3 is assigned undefined and so 1+2+undefined = NaN

// Note that, no error is thrown
```

```js
function argumentVar(parameter1, parameter2, parameter3){
  console.log(arguments.length); // Logs the number of arguments passed.
  console.log(arguments[3]); // Logs the 4th argument. Follows array indexing notations. 
}

argumentVar(1,2,3,4,5);
// Log would be as follows
// 5
// 4

// 5 is the number of arguments
// 4 is the 4th argument
```

```js
function restParam(parameter1, ...restArgs){
  console.log(restArgs.length); // Logs the number of arguments that do not have a corresponding parameter
  console.log(restArgs[2]); // Logs the 3rd argument after the number of arguments that do not have a corresponding parameter
}

restParam(1,2,3,4,5);
// Log would be as follows
// 4
// 4

// 4 is the number of arguments that do not have a corresponding parameter
// 4 is the 4th 3rd argument after the number of arguments that do not have a corresponding parameter
```

