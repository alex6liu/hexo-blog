---
title: javascript 权威指南
date: 2019-05-24 10:40:01
tags: [javascript, 笔记]
---

## 第三章 类型、值、变量

数据类型:

- 原始类型
  - 数字
  - 字符串
  - 布尔值
  - null
  - undefined
  - symbol
- 对象类型
  - 对象
    - 全局对象
  - 数组
  - 函数

### 3.1.4 二进制浮点数和四舍五入错误

JavaScript 中使用实数的时候, 常常只是真实值的一个近似表示

JavaScript 采用**二进制表示法**

```js
var x = .3 - .2
var y = .2 - .1
x == y // false
x == .1 // false
y == .1 // true
```

`NaN` 和任何值都不相等, 包括自身

```js
var x // x 是 NaN
x == NaN // false
x != x // true 用来判断是不是 NaN, 效果等同于 isNaN()
```

### 3.2.3 字符串的使用

**JavaScript 中字符串是固定不变的,** 类似 `replace()`和`toUpperCase()`的方法都返回新字符串, 原字符串本身没有发生改变

### 3.3 布尔值

会被转换成 `false`

```js
undefined
null
0
-0
NaN
''
```

所有其他值, 包括所有**对象(数组)**都会转换成`true`

### 3.4 `null` 和 `undefined`

`null` 常用来描述 '空值'

```js
typeof null // 返回 object
```

`undifined` 表明变量没有初始化, 说明这个属性或元素不存在

如果函数没有返回任何值, 则返回 `undifined`

``` js
typeof x // 返回 undefined
```

判断相等运算符`==` 认为两者是相等的, 要用`===`才能区分他们

### 3.5 全局对象

- 全局属性
- 全局函数
- 构造函数
- 全局对象

### 3.6 包装对象

JavaScript对象时一种复合值: 它是属性或已命名值得集合. 通过 `.`符号来引用属性值. **当属性值是一个函数的时候, 称其为方法**

可以用`String(), Number(), Boolean`构造函数来显示创建包装对象

```js
var s = 'test', n = 1, b = true
var S = new String(s)
var N = new Number(n)
var B = new Boolean(b)
```

`==` 视原始值和其包装对象相等, 但`===`视为不等

### 3.7 不可变的原始值和可变的对象引用

**原始值**(`undefined`, `null`, 布尔值, 数字, 字符串)是不可改变的

原始值的比较是值得比较, 只有在他们的值相等时它们才相等

**对象**是可变的, 它们的值是可修改的

```js
var o = { x : 1 }
o.x = 2
o.y = 3
```

对象的比较并非值得比较: 即使两个对象包含同样的属性和值, 它们也是不相等的

通常将对象称为引用类型(reference type)

对象的比较是**基于引用的比较**: 当且仅当它们引用同一个基对象时, 它们才相等

```js
var a = []
var b = a
b[0] = 1
a[0] // 1 变量a也会修改
a === b // true
```

### 3.8.3 对象转换为原始值

- 对象到布尔值

所有的对象(包括数组和函数)都转换为`true`, 对于包装对象亦是如此: `new Boolean(fasle)`是一个对象而不是原始值, 它将转换为`true`

- 对象到字符串
	- `toString()`
	- `valueOf()`

数组: `[1,2,3] => '1,2,3'`

- 对象到数字
	- `toString()`
	- `valueOf()`

数组: `[] => 0`, `[1] => 1`

### 3.9 变量申明

`var a`

使用`var`语句重复声明变量是合法且无害的, 如果重复声明带有初始化器, 那么这就和一条简单的赋值语句一样

如果试图读取一个没有声明的变量的值, JavaScript会报错

在严格模式中, 给一个没有声明的变量赋值也会报错

在非严格模式下, 给一个未声明的变量赋值, JavaScript实际上**会给全局对象创建一个同名属性**, 并且工作起来像(但不完全一样)一个正确声明的全局变量

### 3.10 变量作用域(scope)

全局变量拥有全局作用域, 然而在函数内声明的变量只在函数体内有定义

在函数体内, **局部变量的优先级高于同名的全局变量**

**声明局部变量时必须用`var`语句**

#### 声明提前(hoisting)

JavaScript的函数作用域是指在函数内声明的所有变量在函数体内始终是可见的, 这意味着变量在声明之前甚至已经可用, 被称为声明提前

```js
var scope = 'global'
function f() {
	console.log(scope) // 输出undifined, 而不是global
	var scope = 'local'
	console.log(scope) // 输出local
}
```

上述过程等价于:

```js
function f() {
	var scope // 在函数顶部声明了局部变量
	console.log(scope) // 变量存在, 值是undefined
	scope = 'local' // 初始化并赋值
	console.log(scope)
}
```

#### 3.10.2 作为属性的变量

当声明一个JavaScript全局变量时, 实际上是定义了全局对象的一个属性

当使用`var`声明一个变量时, 创建的这个属性是不可配置的, 也就是说这个变量无法通过`delete`删除

如果没有使用严格模式并给一个未声明的变量赋值, JavaScript会自动创建一个全局变量, 以这种方式创建的变量是全局对象的正常的可配置属性, 并可以删除它们:

```js
var a = 1 // 声明一个不可删除的全局变量
b = 2 // 创建全局对象的一个可删除属性
this.b2 = 3 // 同上
delete a // false, 变量并没有被删除
delete b // true, 变量被删除
delete this.b2 // true, 变量被删除
```

#### 3.10.3 作用域链

当JavaScript需要查找变量`x`的值得时候(这个过程称作"变量解析" variable resolution), 它会从链中的第一个对象开始查找, 如果这个对象有一个名为`x`的属性, 则会直接使用这个属性的值. 否则, JavaScript会继续查找链上的下一个对象.

如果作用域链上没有任何一个对象含有属性`x`, 那么就抛出一个引用错误(ReferenceError)异常

## 第四章 表达式和运算符

### 4.1 原始表达式(primary expression):

- 常量或直接量
- 关键字
- 变量

### 4.2 对象和数组的初始化表达式

数组:

```js
[]
[1,2]
[[1,2], [2,3]]
```

```js
var a = [1,,,,5] // 逗号之间的空位会填充3个undifined
```

数组直接量的列表结尾处可以留下单个逗号, 这时并不会创建一个新的undifined元素

对象:

```js
var p = {x:2,y:3}
```

### 4.7 操作符概述

`*`会将操作数转换为数字: `"3"*"5"` -> 返回数字15, 而不是"15"

#### 4.7.4 操作符的副作用

`=`, `++`, `--`, `delete`

#### 4.7.5 运算符的优先级

属性访问表达式和调用表达式的优先级要比运算符高

### 4.8

#### 4.8.1 `+`运算符

`+`可以对两个数字做加法,也可以做字符串连接操作

如果一个操作数是字符串或者转换为字符串的对象, 另一个也会转为字符串

如果两个都不是类字符串的,那么将进行算术加法运算(转换成数字或者`NaN`)

```js
1 + 2  // 3
'1' + '2' // '12'
'1' + 2 // '12'
1 + {} // '1[object Object]'
true + true // 2
2 + null // 2
2 + undifined // NaN: undifined转化成NaN后做加法
```

```js
1 + 2 + 'bland' // '3bland'
1 + (2 + 'blind') // '12blind'
```

#### 4.8.2 一元算术运算符

- `+`

把操作数转换为数字或者`NaN`, 并返回这个转换后的数字, 如果操作数就是数字, 则直接返回

- `-`

根据需要把操作数转换为数字, 然后改变运算结果的符号

- `++`

将操作数转换为数字, 然后给数字加1, 并将加1后的数值重新赋值给变量

`++i`: 增量计算并返回计算后的值

`i++`: 增量计算, 但返回未做增量计算的值

```js
var i = 1, j = ++i // i,j = 2
var i = 1, j = i++ // i = 2, j = 1
```

`++x`和`x=x+1`并不完全一样, `++`从不进行字符串连接操作, 它总会将操作数转换为数字并加1

- `--`

#### 4.8.3 位运算符

位运算符会将操作数转换为32位整型数字

位运算符会将`NaN`, `Infinity`, `-infinity`都转换为0

- `&`
- `|`
- `^`
- `~`

对一个值使用`~`相当于改变它的符号并减1. `~0x0F = -16`

- `<<`

左移1位相当于乘以2

- `>>`

右移1位相当于除以2

- `>>>`

无符号右移, 同`>>`, 只是左边的高位总是补0, 与原来操作数的符号无关, `-1>>4 = -1`

### 4.9

#### 4.9.1 相等和不等运算符

`===` 严格相等运算符比较过程中没有任何类型转换

- 如果两个值都是`null`或者都是`undifined`, 则它们不相等
- 如果一个是`NaN`或者两个都是`NaN`, 则它们不相等. `NaN`和其他任何值都是不相等的, 包括它本身
- 如果一个为`0`,一个为`-0`, 它们相等
- 如果两个值为字符串, 且所含的对应位上的16位数完全相等, 则它们相等. 两个字符串可能显示出的字符一样, 但具有不同的16位值, `===`和`==`的结果也是不相等
- 如果两个引用值指向同一个对象,数组或函数, 则它们相等. 如果指向不同的对象, 尽管两个对象具有完全一样的属性, 它们也是不相等

`==` 会进行一些类型转换

- 一个是`null`, 一个是`undifined`, 它们相等

#### 4.9.2 比较运算符

`>`, `<`, `>=`, `<=`

- 如果两个操作数是字符串, 将按字母表顺序(16位Unicode索引)进行比较
- 如果至少有一个不是字符串, 将都转换为数字进行比较, 如果一个操作数是`NaN`, 总会返回`false`

**字符串的比较是区分大小写的**, 所有大写的ASCII字母都**小于**小写的

**当一个操作符是`NaN`时, 所有4个比较运算符均返回`false`**

#### 4.9.3 in运算符

```js
var point = { x:1, y:1 }
"x" in point // true, 有x属性
"z" in point // false, 没有z属性
"toString" in point // true, 继承toString()方法

var data = [7,8,9]
"0" in data // true, 包含元素0
1 in data // true, 数字转换为字符串
3 in data // false, 没有索引为3的元素
```

#### 4.9.4 instanceof 运算符

```js
var a= [1,2,3]
a instanceof Array // true
a instanceof Object // true
```

需要注意, 所有对象都是Object的实例, 当通过`instanceof`判断一个对象是否是一个类的实例的时候, 这个判断也会包含对"父类"的检测

如果左操作数不是对象, 返回`false`, 如果右操作数不是函数, 则抛出一个类型错误异常

### 4.10

#### 4.10.1 逻辑与(&&)

首先计算左侧表达式, 如果结果是假值, 返回左操作数的值. 如果结果是真值, 返回右操作数的值.

```js
var o = { x:1 }
var p = null
o && o.x // 1
p && p.x // null
```

### 4.11 赋值表达式

赋值操作符的结合性是从右至左

```js
i=j=k=0 // i,j,k=0
```

### 4.12 表达式计算

使用全局函数`eval()`

```js
eval("3+2") // 5
```

`eval()`只有一个参数, 如果传入的参数不是字符串, 它直接返回这个参数, 如果参数是字符串, 它会把字符串当成JavaScript代码进行编译.

如果编译失败则抛出一个语法错误(SyntaxError).

如果编译成功, 则开始执行这段代码, 并返回字符串中最后一个表达式或语句的值, 如果最后一个表达式或语句没有值, 则最终返回`undefined`.

最重要的是, 它使用了它的变量作用域环境, 和局部作用域一样.

如果一个函数定义了一个局部变量`x`, 然后`eval("x")`, 它会返回局部变量的值. 如果调用`eval("x=1")`, 它会改变局部变量的值.

需要注意的是, 不能通过`eval()`往函数中任意粘贴代码片段.

```js
var foo = function(a) {
	eval(a);
}
foo("return;") // SyntaxError: Illegal return statement
```

#### 4.12.2 全局eval()

```js
var geval = eval // 使用别名调用eval将是全局eval
var x = 'global', y = 'global' // 2个全局变量
function f() { // 函数内执行的是局部eval
	var x = 'local' // 局部变量
	eval("x += 'changed';") // 直接eval更改了局部变量的值
	return x // 返回更改后的局部变量
}
function g(){ // 执行的是全局eval
	var y = 'local' // 局部变量
	geval("y+='changed'") // 间接调用改变了全局变量的值
	return y // 返回未更改的局部变量
}
console.log(f(), x) // localchanged global
console.log(g(), y) // local globalchanged 
```

### 4.13 其他运算符

- `?:`
- `typeof`

```js
    x          typeof x
--------------------------
undefined     "undefined"
null          "object"
true/false    "boolean"
number/NaN    "number"
string        "string"
function      "function"
内置对象(非函数 "object"
例如数组)
```

- `delete`

用来删除对象属性或者数组元素

```js
var o = { x:1, y:2 }
delete o.x
"x" in o // false
typeof o.x // undefined
delete o.x // true
delete o // false, 不能删除通过var声明的变量, 在严格模式下抛出异常

var a = [1,2,3]
delete a[2]
2 in a // false
a.length // 3, 数组长度并没有被改变

delete 1 // true
this.x = 1 // 给全局变量一个属性
delete x // 非严格模式下返回true
```

- `void`
- `,`

## 第五章 语句

- 条件语句 `if`, `switch`

`switch case`按照`===`进行比较

- 循环语句 `while`, `for`, `do/while`, `for in`
- 跳转语句 `break`, `return`, `throw`, `continue`, `try/catch/finally`

`break`立即退出最内层循环或switch语句

`continue`执行下一次循环

`return`函数执行终止

- 表达式语句
- 复合语句和空语句
- 声明语句 `var`, `function`

- `with`

临时扩展作用域链

严格模式不推荐用`with`, 运行的慢

- `debugger`
- `use strict`

## 第六章 对象

除了字符串, 数字, true, false, null和undefined之外, JavaScript中的值都是对象

### 6.1 创建对象

- 对象直接量
- `new`构造函数
- `Object.create()`

#### 6.1.3 原型

所有通过对象直接量创建的对象都具有同一个原型对象, 并可以通过JavaScript代码`Object.prototype`获得对原型对象的引用

通过`new`和构造函数调用创建的对象的原型就是构造函数的`prototype`属性的值

同使用`{}`创建对象一样, 通过`new Object()`创建的对象也继承自`Object.prototype`

没有原型的对象不多, `Object.prototype`就是其中之一, 他不继承任何属性

#### 6.1.4 Object.create()

`Object.create()`是一个静态函数, 使用方法: `var o1 = Object.create({x:1, y:2})`

可以通过传入参数`null`来创建一个没有原型的新对象, 但通过这种方式创建的对象不会继承任何东西, 甚至不包括基础方法, 比如`toString()`

如果想创建一个普通的空对象, 需要传入`Object.prototype`

```js
var o3 = Object.create(Object.prototype) // o3和{}和new Object()一样
```

### 6.3 删除属性

`delete`只是断开属性和宿主对象的联系, 而不会去操作属性中的属性

`delete`只能删除自有属性, 不能删除继承属性

`delete`表达式删除成功或没任何副作用时, 它返回`true`. 如果`delete`后不是一个属性访问表达式, `delete`同样返回`true`

`delete`不能删除那些可配置性为`false`的属性, 如通过变量声明和函数声明创建的全局对象的属性

### 6.4 检测属性

- `in`

如果对象的自有属性或继承属性中包含这个属性则返回`true`

也可以使用`!==`判断一个属性是否是`undefined`

但有一种场景只能使用`in`运算符而不能使用`!==`. `in`可以区分不存在的属性和存在但值为`undefined`的属性.

- `hasOwnPreperty()`

对于继承属性将返回`false`

- `propertyIsEnumerable()`

只有检测到是自有属性且这个属性的可枚举性为`true`时它才返回`true`

### 6.6 属性getter和setter

不具有可写性

### 6.8 对象的三个属性

原型, 类, 可扩展性

#### 6.8.1 原型属性

对象的原型属性是用来继承属性的

通过`isPrototypeOf()`检测一个对象是否是另一个对象的原型(或处于原型链中)

`__proto__`的属性用以直接查询/设置对象的原型, 但并不推荐使用

#### 6.8.2 类属性

可以调用`toString()`方法, 返回`[object class]`, 然后提取已返回字符串的字符

#### 6.8.3 可扩展性

### 6.9 序列化对象

`JSON.stringify`, `JSON.parse()`

### 6.10 对象方法

- `toString()`
- `toLocaleString()`
- `toJSON()`
- `valueOf()`

## 第七章 数组

- 数组是值的有序集合
- JavaScript数组是无类型的: 数组元素可以是任意类型
- 数组的索引是基于0的32位数值, 最大索引位 2^32 - 2
- 数组是动态的, 根据需要会增长或缩减
- 数组可能是稀疏的: 数组元素的索引不一定要连续的, 他们之间可以有空缺
- 每个数组都有一个length属性

### 7.1 创建数组

- 数组直接量

```js
var empty = []
var p = [1,2,3]
var c = [1, , 3]
```

数组直接量的语法允许有可选的结尾的逗号, 故`[,,]`只有2个元素而非3个

- 构造函数`Array()`

```js
var a = new Array()
var a = new Array(10)
var a = new Array(5,4,3,2,1)
```

### 7.2 数组元素的读和写

所有的索引都是属性名, 但只有在 0 ~ 2^32-2 之间的整数属性名才是索引

所有的数组都是对象, 可以为其创建任意名字的属性

但如果使用的属性是数组的索引, 数组的特殊行为就是将根据需要更新他们的length属性值.

注意, 可以使用负数或非整数来索引数组. 这种情况下, 数值转换为字符串, 字符串作为属性名来用. 只能当成常规的对象属性, 而非数组的索引.

如果使用了是非负整数的字符串, 他就当做数组索引, 而非对象属性.

### 7.3 稀疏数组

注意, 当在数组直接量中省略值时不会创建稀疏数组, 省略的元素值是`undefined`

```js
var a1 = [,,,] // [undefined, undefined, undedined]
var a2 = new Array(3) // 没有元素
```

### 7.4 数组长度

数组长度保证大于它每个元素的索引值

- 如果为一个数组元素赋值, 它的索引i大于或等于现有数组的长度时, length属性的值将设置为i+1
- 设置length属性为一个小于当前长度的非负整数n时, 当前数组中那些索引值大于或等于n的元素将从中删除

### 7.8 数组方法

- `join()`
- `reverse()`
- `sort()`
- `concat()`

**不会修改调用的数组**

- `slice()`

**不会修改调用的数组**

返回数组的一个片段或者子数组

- `splice()`

在数组中插入或删除元素

**修改原始数组**

- `push()`, `pop()`

**修改原始数组**

- `unshift()`, `shift()`

- `toString()`, `toLocaleString()`

### 7.9 ECMAScript 5 中的数组方法

- `forEach()`

无返回值

无法再所有元素都传递给调用的函数之前终止遍历

如果要提前终止, 必须把`forEach()`放在一个`try`块中,并能抛出一个异常

- `map()`

有返回值, 返回的是新数组, 不修改原数组

- `filter()`

返回新数组

- `every()`, `some()`

返回`true`或`false`

一旦确认该返回什么值他们就会停止遍历数组元素

`some()`在判定函数第一次返回`true`后就返回`true`

`every()`在判定函数第一次返回false后就返回`false`

在空数组上调用时, `every()`返回`true`, `some()`返回`false`

- `reduce()`, `reduceRight()`

使用指定函数将数组元素进行组合, 生成单个值

- `indexOf()`, `lastIndexOf()`

### 7.10 数组类型

用`Array.isArray()`来判断是否是数组

`typeof`返回的是`object`

### 7.11 类数组对象

### 7.12 作为数组的字符串

```js
var s = 'test'
s.charAt(0) // 't'
s[1] // 'e'
```

## 第八章 函数

