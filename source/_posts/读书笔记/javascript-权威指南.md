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

