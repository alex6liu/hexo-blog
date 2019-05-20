---
title: Auto data type conversion
date: 2019-05-10 15:20:21
tags: [js]
---

## 自动转换为布尔值

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

## 自动转换为字符串

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

## 自动转换为数值

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

## [Know rules of auto data types conversion](https://juejin.im/entry/584918612f301e005716add6)

- `===`
  - 如果Type(x)和Type(y)不同，返回false
  - 如果Type(x)和Type(y)相同
    - 如果Type(x)是Undefined，返回true
    - 如果Type(x)是Null，返回true
    - 如果Type(x)是String，当且仅当x,y字符序列完全相同（长度相同，每个位置上的字符也相同）时返回true，否则返回false
    - 如果Type(x)是Boolean，如果x,y都是true或x,y都是false返回true，否则返回false
    - 如果Type(x)是Symbol，如果x,y是相同的Symbol值，返回true,否则返回false
    - 如果Type(x)是Number类型
      - 如果x是NaN，返回false
      - 如果y是NaN，返回false
      - 如果x的数字值和y相等，返回true
      - 如果x是+0，y是-0，返回true
      - 如果x是-0，y是+0，返回true
      - 其他返回false

- `==`
  - 如果Type(x)和Type(y)相同，返回x===y的结果
  - 如果Type(x)和Type(y)不同
    - 如果x是null，y是undefined，返回true
    - 如果x是undefined，y是null，返回true
    - 如果Type(x)是Number，Type(y)是String，返回 x==ToNumber(y) 的结果
    - 如果Type(x)是String，Type(y)是Number，返回 ToNumber(x)==y 的结果
    - 如果Type(x)是Boolean，返回 ToNumber(x)==y 的结果
    - 如果Type(y)是Boolean，返回 x==ToNumber(y) 的结果
    - 如果Type(x)是String或Number或Symbol中的一种并且Type(y)是Object，返回 x==ToPrimitive(y) 的结果
    - 如果Type(x)是Object并且Type(y)是String或Number或Symbol中的一种，返回 ToPrimitive(x)==y 的结果
    - 其他返回false

- Type(x) : 获取x的类型
- ToNumber(x) : 将x转换为Number类型
- ToBoolean(x) : 将x转换为Boolean类型
- ToString(x) : 将x转换为String类型
- SameValueNonNumber(x,y) : 计算非数字类型x,y是否相同
- ToPrimitive(x) : 将x转换为原始值

js中的原始类型：

- Null: null值.
- Undefined: undefined 值.
- Number: 所有的数字类型，例如0,1,3.14等 以及NaN, 和 Infinity.
- Boolean: 两个值true和false.
- String: 所有的字符串，例如’abc’和’’.
- 其他的都是’非原始’的，像Array,Function,Object等。

注意：typeof null 得到的结果是object。这里是由于js在最初的设计的问题。但其实null应该是属于原始类型的。

## Strict comparison

- `===` 严格相等，会比较两个值的类型和值
- `==`  抽象相等，比较时，会先进行类型转换，然后再比较值