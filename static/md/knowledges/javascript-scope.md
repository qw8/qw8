---
title: JavaScript作用域
date: 2020-01-07 21:10:40
categories: 
- 前端知识
tags:
- JavaScript
- 作用域
---

### 作用域的概念及作用

**概念：** **对变量起保护作用的一块区域**，一个函数可以访问其他函数中的变量。

- 在Java、C等语言中，作用域为for语句、if语句或\\{\\}内的一块区域，称为作用域；
- 而在 JavaScript 中，作用域为function()\\{\\}内的区域，称为函数作用域。

**作用：** 作用域外部无法获取到作用域内部声明的变量，作用域内部能够获取到作用域外界声明的变量。

**分类：**块作用域、词法作用域、动态作用域

1 块作用域 花括号 \\{\\}

2 词法作用域（js 属于词法作用域）
作用域只跟在何处被创建有关系，跟在何处被调用没有关系

3 动态作用域
作用域只跟在何处被调用有关系，跟在何处被创建没有关系



### 说说你对作用域链的理解

全局函数无法查看局部函数的内部细节，但局部函数可以查看其上层的函数细节，直至全局细节

当需要从局部函数查找某一属性或方法时，如果当前作用域没有找到，就会上溯到上层作用域查找，直至全局函数，这种组织形式就是作用域链

作用域链的作用是保证执行环境里有权访问的变量和函数是有序的，作用域链的变量只能向上访问，变量访问到 window 对象即被终止，作用域链向下访问变量是不被允许的。



### 什么是闭包（closure），为什么要用它？

闭包是指**有权访问另一个函数作用域中变量的函数**。定义一个函数就开辟了一个局部作用域，整个 js 执行环境有一个全局作用域（闭包是一个受保护的变量空间）

**创建闭包的最常见的方式：**就是在一个函数内创建另一个函数，通过另一个函数访问这个函数的局部变量,利用闭包可以突破作用链域，将函数内部的变量和方法传递到外部。

**闭包的特性：**

- 函数内再嵌套函数
- 内部函数可以引用外层的参数和变量
- 参数和变量不会被垃圾回收机制回收

```
//li节点的onclick事件都能正确的弹出当前被点击的li索引
 <ul id="testUL">
    <li> index = 0</li>
    <li> index = 1</li>
    <li> index = 2</li>
    <li> index = 3</li>
</ul>
<script type="text/javascript">
  	var nodes = document.getElementsByTagName("li");
	for(i = 0;i<nodes.length;i+= 1)\\{
	    nodes[i].onclick = (function(i)\\{
	    	return function() \\{
	        	console.log(i);
	        \\} //不用闭包的话，值每次都是4
		\\})(i);
	\\}
</script>
```

- 执行say667()后,say667()闭包内部变量会存在,而闭包内部函数的内部变量不会存在
- 使得Javascript的垃圾回收机制GC不会收回say667()所占用的资源
- 因为say667()的内部函数的执行需要依赖say667()中的变量
- 这是对闭包作用的非常直白的描述

```
function say667() \\{
	// Local variable that ends up within closure
	var num = 666;
	var sayAlert = function() \\{
		alert(num);
	\\}
	num++;
	return sayAlert;
\\}

 var sayAlert = say667();
 sayAlert()//执行结果应该弹出的667
```

```js
var f = (function fn() \\{
  var name = 1;
  return function () \\{
    name++;
    console.log(name)
  \\}
\\})()

==>undefined 有疑问
```



### JavaScript变量声明提升

-  在JavaScript中，函数声明与变量声明经常被JavaScript引擎隐式地提升到当前作用域的顶部。
-  声明语句中的赋值部分并不会被提升，只有名称被提升
-  函数声明的优先级高于变量，如果变量名跟函数名相同且未赋值，则函数声明会覆盖变量声明
-  如果函数有多个同名参数，那么最后一个参数（即使没有定义）会覆盖前面的同名参数



### 解释 JavaScript 中的作用域与变量声明提升？

- 我对作用域的理解是只会对某个范围产生作用，而不会对外产生影响的封闭空间。在这样的一些空间里，外部不能访问内部变量，但内部可以访问外部变量。
- 所有申明都会被提升到作用域的最顶上
- 同一个变量申明只进行一次，并且因此其他申明都会被忽略
- 函数声明的优先级优于变量申明，且函数声明会连带定义一起被提升



### 使用 let、var 和 const 创建变量有什么区别

用 var 声明的变量的作用域是它当前的执行上下文，它可以是嵌套的函数，也可以是声明在任何函数外的变量。let 和 const 是块级作用域，意味着它们只能在最近的一组花括号（function、if-else 代码块或 for 循环中）中访问。

```js
function foo() \\{
  // 所有变量在函数中都可访问
  var bar = "bar";
  let baz = "baz";
  const qux = "qux";

  console.log(bar); // bar
  console.log(baz); // baz
  console.log(qux); // qux
\\}

console.log(bar); // ReferenceError: bar is not defined
console.log(baz); // ReferenceError: baz is not defined
console.log(qux); // ReferenceError: qux is not defined
```

```js
if (true) \\{
  var bar = "bar";
  let baz = "baz";
  const qux = "qux";
\\}

// 用 var 声明的变量在函数作用域上都可访问
console.log(bar); // bar
// let 和 const 定义的变量在它们被定义的语句块之外不可访问
console.log(baz); // ReferenceError: baz is not defined
console.log(qux); // ReferenceError: qux is not defined
```

var 会使变量提升，这意味着变量可以在声明之前使用。let 和 const 不会使变量提升，提前使用会报错。

```js
console.log(foo); // undefined

var foo = "foo";

console.log(baz); // ReferenceError: can't access lexical declaration 'baz' before initialization

let baz = "baz";

console.log(bar); // ReferenceError: can't access lexical declaration 'bar' before initialization

const bar = "bar";
```

用 var 重复声明不会报错，但 let 和 const 会。

```js
var foo = "foo";
var foo = "bar";
console.log(foo); // "bar"

let baz = "baz";
let baz = "qux"; // Uncaught SyntaxError: Identifier 'baz' has already been declared

```

let 和 const 的区别在于：let 允许多次赋值，而 const 只允许一次。

```js
// 这样不会报错。
let foo = "foo";
foo = "bar";

// 这样会报错。
const baz = "baz";
baz = "qux";
```

解析：[参考](https://github.com/yangshun/front-end-interview-handbook/blob/master/Translations/Chinese/questions/javascript-questions.md#\\%E4\\%BD\\%BF\\%E7\\%94\\%A8letvar\\%E5\\%92\\%8Cconst\\%E5\\%88\\%9B\\%E5\\%BB\\%BA\\%E5\\%8F\\%98\\%E9\\%87\\%8F\\%E6\\%9C\\%89\\%E4\\%BB\\%80\\%E4\\%B9\\%88\\%E5\\%8C\\%BA\\%E5\\%88\\%AB)



### 变量声明提升

`js` 代码在运行前都会进行 `AST` 解析，**函数申明默认会提到当前作用域最前面，变量申明也会进行提升。**

但赋值不会得到提升。关于 `AST` 解析，这里也可以说是形成词法作用域的主要原因



### js 属于哪种作用域

词法作用域（函数作用域）

解析：

```js
// 块作用域
/*\\{
        var num =123;
    \\}
    console.log(num);*/
// 如果js属于块作用域，那么在花括号外部就无法访问到花括号内部的声明的num变量。
// 如果js不属于块级作用域，那么花括号外部就能够访问到花括号内部声明的num变量
// 能够输出num变量，也就说明js不属于块级作用。
// 在ES6 之前的版本js是不存在块级作用域的。

//js属于词法作用域还是动态作用域

// js中函数可以帮我们去形成一个作用域

/* function fn()\\{
        var num =123;
    \\}
    fn();
    //在函数外界能否访问到num这样一个变量
    console.log(num)*/ //Uncaught ReferenceError: num is not defined
// 如果函数能够生成一个作用域，那么在函数外界就无法访问到函数内部声明的变量。
// js中的函数能够生成一个作用。  函数作用域 。

// 词法作用域：作用的外界只跟作用域在何处创建有关系，跟作用域在何处被调用没有关系

var num = 123;
function f1() \\{
  console.log(num); //
\\}
function f2() \\{
  var num = 456;
  f1(); //f1在f2被调用的时候会被执行 。
\\}
f2();

//如果js是词法作用域，那么就会输出f1被创建的时候外部的num变量 123
//如果js是动态作用域，那么f1执行的时候就会输出f1被调用时外部环境中的num  456

```



### 变量提升

A、js 代码执行的过程

- 1 变量提升
- 2 代码从上到下依次执行

var 关键字和 function 关键字声明的变量会进行变量提升

B、变量提升发生的环境：发生在代码所处的当前作用域。

- 变量提升
- 1 var 关键字进行的变量提升，会把变量提前声明，但是不会提前赋值 。
- 2 function 关键字对变量进行变量提升，既会把变量提前声明，又会把变量提前赋值，也就是把整个函数体提升到代码的顶部
- 3 有一些代码是不会执行的但是仍旧会发生变量提升,规则适用于 1,2
- 3.1 return 之后的代码依旧会发生变量提升，规则适用于 1，2
- 3.2 代码报错之后的代码依旧会发生变量提升，规则适用于 1，2
- 3.3 break 之后的代码依旧会发生变量提升，规则适用于 1,2
- 4 有一些代码是不会执行但是仍旧会发生变量提升，但是规则要发生变化
- 4.1 if 判断语句 if 判断语句中 var 关键字以及 function 关键字声明的变量只会发生提前声明，不会发生提前赋值,也就是不会吧函数体整体提升到当前作用域顶部。规则跟 1,2 不适用
- 4.2 switch case 规则跟 1,2 不适用
- 4.3 do while 规则跟 1,2 不适用
- 4.4 try catch catch 中声明的变量只会发生提前声明，不会发生提前赋值。
- Ps:在条件判断语句和 try catch 中的声明的变量不管是否能够执行，都只会发生提前
- 声明，不会发生提前赋值。

解析：

```js
// 如果一个变量声明了但是未赋值，那么输出这个变量就会输出 undefined
var num;
console.log(num);

// 如果一个变量没有声明也没有赋值，那么就会报一个错：
console.log(num); // 输出一个不存在的变量 Uncaught ReferenceError: num is not defined

```

```js
// var 关键字进行的变量提升
console.log(num);
var num = 123;
console.log(num);
var num = 456;
console.log(num);

// 变量提升之后的代码：
var num;
console.log(num);
num = 123;
console.log(num);
num = 456;
console.log(num);

```

```js
// function 关键字的变量提升
console.log(fn);
function fn() \\{
  console.log(1);
\\}

// 变量提升之后的代码：
function fn() \\{
  console.log(1);
\\}
console.log(fn); // 输出fn的函数体

```

```js
// 3.1 return 之后的代码依旧会发生变量提升  规则适用于1，2
function fn() \\{
  console.log(num);
  return;
  var num = 123;
\\}
fn();

// 变量提升之后的代码：
function fn() \\{
  var num;
  console.log(num);
  return;
  num = 123;
\\}
fn(); // undefined

function fn() \\{
  console.log(fo);
  return;
  function fo() \\{\\}
\\}
fn();

// 变量提升之后的代码：
function fn() \\{
  function fo() \\{\\}
  console.log(fo);
  return;
\\}
fn(); //输出fo的函数体

```

```js
//3.2 代码报错之后的代码依旧会进行变量提升，规则适用于1,2
console.log(num);
xsasfgdsfqdfsdf; //报一个错
var num = 123;
console.log(num);

// 变量提升之后的代码：
var num;
console.log(num); //输出 undefined
dsagdsqghdwfh; // 报一个错误 ，错误之后的代码不会被执行
num = 123;
console.log(num);

```

```js
//function 关键字
console.log(fn);
sasgfdhwhsdqg;
function fn() \\{\\}
console.log(fn);

// 变量提升之后的代码：
function fn() \\{\\}
console.log(fn); // 输出 fn 的函数体
asdgsdgdfgfdg; // 报一个错误，报错之后的代码不会被执行
console.log(fn);

```

```js
//4 代码不执行，但是会进行变量提升，不过规则不适用于1,2
//4.1 if判断语句
console.log(num);
if (false) \\{
	var num = 123;
\\}
console.log(num)

//  变量提升之后的代码：
var num;
console.log(num); //undefined
if (false) \\{
	num = 123;
\\}
console.log(num) //undefined

console.log(fn);
if (false) \\{
	function fn() \\{\\}
\\}
console.log(fn);

// 变量提升之后的代码：
var fn;
function fn;
console.log(fn) //undefined
if (false) \\{
	function fn() \\{\\}
\\}
console.log(fn) //undefined
/*function fn//Uncaught SyntaxError: Unexpected end of input*/

```

```js
// try catch
try \\{
  console.log(num);
\\} catch (e) \\{
  var num = 123;
\\}
console.log(num);

var num;
try \\{
  console.log(num); // undefined
\\} catch (e) \\{
  num = 123;
\\}
console.log(num); // undefined

try \\{
  console.log(fn);
\\} catch (e) \\{
  function fn() \\{\\}
\\}
console.log(fn);

var fn;
try \\{
  console.log(fn); // undefined
\\} catch (e) \\{
  num = 123;
\\}
console.log(fn); // undefined

```

[对应面试题](../编程题/变量提升.md)

