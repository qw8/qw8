---
title: JavaScript速查表
date: 2020-02-07 21:10:40
categories: 
- 前端知识
tags:
- JavaScript
- 数组
---

 JavaScript是一种轻量级、开源且跨平台的编程语言。它在现代开发中无处不在，被全世界的程序员用来创建动态的交互式 Web 内容，比如应用程序和浏览器。它是万维网的核心技术之一，与 HTML 和 CSS 并驾齐驱，并通过帮助创建美观且速度极快的网站，成为快速发展的互联网背后的强大动力。

本文提供了一份深入的 JavaScript 速查表，是每个 Web 开发人员的必备工具。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/HLN2IKtpicicEjjUsMtd9JibHfxM1MicIhkZS4y4QzXfQG0aqoyqGzMhuPzToOia2K69yFibBUYYB0538I4FphS1kfgw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

### **什么是 JavaScript 速查表？**

我们这份全面的 JavaScript 速查表旨在帮助初学者和经验丰富的程序员掌握这门多功能的编程语言。无论你是构建交互式网页、创建动态内容，还是增强用户体验，这份快速参考指南都提供了基本概念、语法和现成的代码片段。

### **内容目录：**

- 基础知识
- 变量
- 数据类型
- 运算符
- JavaScript 作用域和作用域链
- 函数
- 数组
- 循环
- 条件语句 (if-else)
- 字符串
- 正则表达式
- 数据转换
- 日期对象
- DOM
- 数字和数学
- 事件
- 错误
- 窗口属性

### **基础知识**

要在网站上使用 JavaScript，我们需要将 JavaScript 文件附加到 HTML 文件。为了更好地编写代码，我们还应该在代码中添加注释。注释有两种类型：单行注释和多行注释。

- 为了让浏览器知道代码是用 JavaScript 编写的并执行它，我们必须将代码包含在 `  <script>  ` 标签中，以便将其包含在 HTML 页面上。

```
<script type="text/javascript">
  // 你的 JavaScript 代码写在这里
</script>
```

- 外部 JavaScript 文件也可以单独编写，并使用 `script` 标签包含在我们的 HTML 文件中，如下所示：

```
<script src="filename.js"></script>
```

- JavaScript 注释对于解释 JavaScript 代码非常有用，可以帮助理解代码中发生了什么，并使其更易读。

- - **单行注释：** 以 “//” 开头单行注释。
  - **多行注释：** 如果注释跨越多行，则将其包裹在 `/*` 和 `*/` 中。

### **变量**

JavaScript 中的变量是用于存储数据的容器。JavaScript 允许以下三种方式使用变量：

| 变量  | 描述                                   | 示例               |
| :---- | :------------------------------------- | :----------------- |
| var   | 用于初始化值，可以重新声明和重新赋值。 | `var x = value;`   |
| let   | 类似于 var，但作用域是块级作用域。     | `let y = value;`   |
| const | 用于声明一个不能更改的固定值。         | `const z = value;` |

```
// 使用 var 关键字
console.log("使用 var 关键字");
var x = 1;
if (x === 1) \\{
  var x = 2;
  console.log(x); // 输出：2
\\}
console.log(x); // 输出：2

// 使用 let 关键字
console.log("使用 let 关键字");
let x1 = 1;
if (x1 === 1) \\{
  let x1 = 2;
  console.log(x1); // 输出：2
\\}
console.log(x1); // 输出：1

// 使用 const 关键字
console.log("使用 const 关键字");
const number = 48;

// 更改 const 值将显示 TypeError
try \\{
  const number = 42;
\\} catch (err) \\{
  console.log(err);
\\}
console.log(number); // 输出：48
```

### **数据类型**

JavaScript 变量中可以存储不同类型的数据。为了使机器能够对变量进行操作并正确地计算表达式，了解所涉及变量的类型非常重要。JavaScript 中有以下基本数据类型和非基本数据类型：

| 数据类型  | 描述                                 | 示例                                                |
| :-------- | :----------------------------------- | :-------------------------------------------------- |
| Number    | 数值可以是实数或整数。               | `var x = number;`                                   |
| String    | 用引号括起来的多个字符的序列。       | `var x = "characters";`                             |
| Boolean   | 只有两个值：true 或 false。          | `var x = true/false;`                               |
| Null      | 特殊值，表示变量为空。               | `var x = null;`                                     |
| Undefined | 表示已声明但未赋值的变量。           | `let x; / let x = undefined;`                       |
| Object    | 复杂数据类型，允许我们存储数据集合。 | `var x = \\{ key: "value"; key: "value"; \\}`           |
| Array     | 在单个变量中存储多个相同类型的值。   | `var x = ["y1", "y2" ,"y3" ,"y4"]; y: 任何数据类型` |
| Function  | 函数是可以调用以执行代码块的对象。   | `function x(arguments)\\{ 代码块 \\}`                   |

```
// 字符串
let str = "hello geeks";
console.log(str);

// 数字
const num = 10;
console.log(num);

// 布尔值
const x = "true";
console.log(x);

// 未定义
let name;
console.log(name);

// 空值
const number = null;
console.log(number);

// 符号
const value1 = Symbol("hello");
const value2 = Symbol("hello");
console.log(value1);
console.log(value2);

// 这里两个值是不同的
// 因为它们是符号类型
// 是不可变对象
const object = \\{
  firstName: "geek",
  lastName: null,
  batch: 2,
\\};
console.log(object);
```

### **运算符**

JavaScript 运算符是用于对变量（操作数）执行各种操作的符号。以下是不同类型的运算符：

| 运算符     | 描述                                                         | 符号                                    |
| :--------- | :----------------------------------------------------------- | :-------------------------------------- |
| 算术运算符 | 用于对变量（操作数）执行基本的算术运算。                     | `+`, `-`, `*`, `/`, `\\%`, `++`, `--`     |
| 比较运算符 | 比较运算符用于比较两个操作数。                               | `==`, `===`, `!=`, `>`, `<`, `>=`, `<=` |
| 位运算符   | 用于执行位运算。                                             | `&`, `|`, `^`, `~`, `<<`, `>>`, `>>>`   |
| 逻辑运算符 | JavaScript 中有三个逻辑运算符： 逻辑与：当所有操作数都为真时； 逻辑或：当一个或多个操作数为真时； 逻辑非：将 true 转换为 false。 | `exp1 && exp2`, `exp1 || exp2`, `!exp`  |
| 赋值运算符 | 赋值运算符将值赋给 JavaScript 变量。                         | `=`, `+=`, `-=`, `*=`, `/=`, `\\%=`       |

```
let x = 5;
let y = 3;

// 加法
console.log("x + y = ", x + y); // 8

// 减法
console.log("x - y = ", x - y); // 2

// 乘法
console.log("x * y = ", x * y); // 15

// 除法
console.log("x / y = ", x / y);

// 取余
console.log("x \\% y = ", x \\% y); // 2

// 递增
console.log("++x = ", ++x); // x 现在是 6
console.log("x++ = ", x++);
console.log("x = ", x); // 7

// 递减
console.log("--x = ", --x); // x 现在是 6
console.log("x-- = ", x--);
console.log("x = ", x); // 5

// 幂运算
console.log("x ** y = ", x ** y);

// 比较
console.log(x > y); // true

// 等于运算符
console.log(2 == 2); // true

// 不等于运算符
console.log(3 != 2); // true

// 严格等于运算符
console.log(2 === 2); // true

// 严格不等于运算符
console.log(2 !== 2); // false

// 逻辑运算符

// 逻辑与
console.log(x < 6 && y < 5); // true

// 逻辑或
console.log(x < 6 || y > 6); // true

// 逻辑非
console.log(!(x < 6)); // false
```

### **JavaScript 作用域和作用域链**

- **作用域：** 作用域 定义了 JavaScript 中变量的可访问性或可见性。也就是说，程序的哪些部分可以访问给定的变量，以及变量可以在哪里看到。通常有三种类型的作用域。
- **作用域链：** 作用域链 用于解析 JavaScript 中变量名的值。如果没有作用域链，如果在不同的作用域中多次定义了某个变量名，JavaScript 引擎将不知道该选择哪个值。如果 JavaScript 引擎在当前作用域中找不到变量，它将查看外部作用域，并将继续这样做，直到找到变量或到达全局作用域。如果它仍然找不到变量，它将在全局作用域中隐式声明该变量（如果不在严格模式下），或者返回错误。

| 作用域     | 描述                                                     |
| :--------- | :------------------------------------------------------- |
| 函数作用域 | 在函数内部声明的变量位于函数作用域内，也称为局部作用域。 |
| 全局作用域 | 全局作用域中的变量可以从程序中的任何位置访问。           |
| 块级作用域 | 块级作用域限制了对块外部变量的访问。                     |

```
let z = 3;

function foo() \\{
  if (true) \\{
    var x = "1"; // 存在于函数作用域
    const y = "2"; // 存在于块级作用域
  \\}
  console.log(x);
  // console.log(y); // 会报错
  console.log(z); // 存在于全局作用域
\\}

foo();
```

### **函数**

JavaScript 函数  是一段代码块，旨在执行特定任务。它在被调用时执行。你可以将相同的代码片段放在函数中，并在需要时调用该函数，而不是一遍又一遍地编写相同的代码片段。JavaScript 函数可以使用 `function` 关键字创建。JavaScript 中的一些函数如下：

| 函数         | 描述                                         |
| :----------- | :------------------------------------------- |
| parseInt()   | 解析传递给它的参数并返回一个整数。           |
| parseFloat() | 解析参数并返回一个浮点数。                   |
| isNaN()      | 确定给定值是否为非数字。                     |
| Number()     | 将参数转换为数字后返回该参数。               |
| eval()       | 用于计算以字符串形式表示的 JavaScript 程序。 |
| prompt()     | 创建一个对话框，用于从用户那里获取输入。     |
| encodeURI()  | 将 URI 编码为 UTF-8 编码方案。               |
| match()      | 用于在字符串中搜索与正则表达式匹配的内容。   |

```
// JS parseInt 函数
const num1 = parseInt("3.14");
console.log("使用 parseInt("3.14") = " + num1);

// JS parseFloat 函数
// 它会返回浮点数，直到遇到非数字字符
const num2 = parseFloat("2018.12@geeksforgeeks");
console.log("parseFloat("2018@geeksforgeeks") = " + num2);

// JS isNaN 函数
console.log(isNaN(12));

// JS Number() 函数
const num3 = Number(true);
console.log("值 "true"：" + num3);

// JS eval() 函数
function evalfn() \\{
  const a = 4;
  const b = 4;
  const value = eval(new String(a * b));
  console.log(value);
\\}
evalfn();

// JS encodeURI 函数
const url = "https://www.google.com/search?q=geeks for geeks";
const encodedURL = encodeURI(url);
console.log(encodedURL);
```

### **数组**

在 JavaScript 中，数组  是一个用于存储不同元素的变量。当我们想要存储元素列表并通过单个变量访问它们时，经常使用它。数组使用数字作为索引来访问其“元素”。
数组的声明：  基本上有两种方法来声明一个数组。

```
// 例子：
var House = \[]; // 方法 1
var House = new Array(); // 方法 2
```

可以使用 JavaScript 方法对数组执行各种操作。其中一些方法如下：

| 方法          | 描述                                         |
| :------------ | :------------------------------------------- |
| push()        | 在数组的末尾添加一个新元素。                 |
| pop()         | 移除数组的最后一个元素。                     |
| concat()      | 将多个数组合并成一个数组。                   |
| shift()       | 移除数组的第一个元素。                       |
| unShift()     | 在数组的开头添加新元素。                     |
| reverse()     | 反转数组中元素的顺序。                       |
| slice()       | 将数组的一部分复制到一个新数组中。           |
| splice()      | 以特定方式和位置添加元素。                   |
| toString()    | 将数组元素转换为字符串。                     |
| valueOf()     | 返回给定对象的原始值。                       |
| indexOf()     | 返回找到给定元素的第一个索引。               |
| lastIndexOf() | 返回给定元素出现的最后一个索引。             |
| join()        | 将数组的元素组合成一个字符串并返回该字符串。 |
| sort()        | 根据某些条件对数组元素进行排序。             |

```
// 声明和初始化数组

// 数字数组
let arr = [10, 20, 30, 40, 50];
let arr1 = [110, 120, 130, 140];

// 字符串数组
let string_arr = ["Alex", "peter", "chloe"];

// push: 在数组末尾添加元素
arr.push(60);
console.log("push 操作后：" + arr);

// unshift(): 在数组开头添加元素
arr.unshift(0, 10);
console.log("unshift 操作后：" + arr);

// pop: 从数组末尾移除元素
arr.pop();
console.log("pop 操作后：" + arr);

// shift(): 从数组开头移除元素
arr.shift();
console.log("shift 操作后：" + arr);

// splice(x,y): 从索引 y 开始移除 x 个元素
arr.splice(2, 1);
console.log("splice 操作后：" + arr);

// reverse(): 反转数组中元素的顺序
arr.reverse();
console.log("reverse 操作后：" + arr);

// concat(): 合并两个或多个数组
console.log("concat 操作后：" + arr.concat(arr1));
```

### **循环**

循环  是大多数编程语言中一个有用的特性。使用循环，你可以重复执行一组指令/函数，直到达到特定条件。它们允许你在某个条件为真时，使用不同的值多次运行代码块。循环可以通过以下几种方式在 JavaScript 中创建：

| 循环     | 描述                                          | 语法                                             |
| :------- | :-------------------------------------------- | :----------------------------------------------- |
| for      | 循环遍历代码块，条件在开头指定。              | `for (初始化条件; 测试条件; 递增/递减) \\{ 语句 \\}` |
| while    | 入口控制循环，在检查条件后执行。              | `while (布尔条件) \\{ 循环语句 \\}`                  |
| do-while | 出口控制循环，在检查条件之前执行一次。        | `do \\{ 语句 \\} while (条件);`                      |
| for-in   | 另一种版本的 for 循环，提供更简单的迭代方式。 | `for (变量名 in 对象) \\{ 语句 \\}`                  |

```
// for 循环示例
let x;

// for 循环从 x=2 开始
// 并运行到 x <= 4
for (x = 2; x <= 4; x++) \\{
  console.log("x 的值：" + x);
\\}

// for..in 循环示例
// 创建一个对象
let languages = \\{
  first: "C",
  second: "Java",
  third: "Python",
  fourth: "PHP",
  fifth: "JavaScript",
\\};

// 使用 for..in 循环迭代对象的每个属性
// 并打印所有属性
for (itr in languages) \\{
  console.log(languages[itr]);
\\}

// while 循环示例
let y = 1;

// 当 x 大于 4 时退出
while (y <= 4) \\{
  console.log("y 的值：" + y);

  // 为下一次迭代增加 y 的值
  y++;
\\}

// do-while 循环示例
let z = 21;

do \\{
  // 即使条件为假，也会打印这一行
  console.log("z 的值：" + z);

  z++;
\\} while (z < 20);
```

### **条件语句 (if-else)**

JavaScript 中的 if-else 语句  用于根据条件执行代码块。它们用于设置代码块运行的条件。如果满足某个条件，则执行某个代码块，否则执行 else 代码块。JavaScript 还允许我们在 if 语句中嵌套 if 语句。也就是说，我们可以将一个 if 语句放在另一个 if 语句中。

```
if (条件) \\{
  // 如果条件为真，则执行此代码块
\\} else \\{
  // 如果条件为假，则执行此代码块
\\}

// JavaScript 程序示例，说明 if-else 语句
const i = 10;

if (i < 15)
  console.log("i 的值小于 10");
else 
  console.log("i 的值大于 10");
```

### **字符串**

JavaScript 中的 字符串  是基本数据类型，用于存储和操作文本数据，它可以是零个或多个字符，由字母、数字或符号组成。JavaScript 提供了许多操作字符串的方法。一些最常用的方法如下：

| 方法          | 描述                                       |
| :------------ | :----------------------------------------- |
| concat()      | 用于将多个字符串连接成一个字符串。         |
| match()       | 用于查找字符串中与提供的模式匹配的内容。   |
| replace()     | 用于查找和替换字符串中的给定文本。         |
| substr()      | 用于从给定字符串中提取指定长度的字符。     |
| slice()       | 用于提取字符串的某个区域并返回它。         |
| lastIndexOf() | 用于返回指定值最后一次出现的索引（位置）。 |
| charAt()      | 用于返回字符串特定索引处的字符。           |
| valueOf()     | 用于返回字符串对象的原始值。               |
| split()       | 用于将字符串对象拆分成字符串数组。         |
| toUpperCase() | 用于将字符串转换为大写。                   |
| toLowerCase() | 用于将字符串转换为小写。                   |

```
let gfg = "GFG ";
let geeks = "stands-for-GeeksforGeeks";

// 按原样打印字符串
console.log(gfg);
console.log(geeks);

// concat() 方法
console.log(gfg.concat(geeks));

// match() 方法
console.log(geeks.match(/eek/));

// charAt() 方法
console.log(geeks.charAt(5));

// valueOf() 方法
console.log(geeks.valueOf());

// lastIndexOf() 方法
console.log(geeks.lastIndexOf("for"));

// substr() 方法
console.log(geeks.substr(6));

// indexOf() 方法
console.log(gfg.indexOf("G"));

// replace() 方法
console.log(gfg.replace("FG", "fg"));

// slice() 方法
console.log(geeks.slice(2, 8));

// split() 方法
console.log(geeks.split("-"));

// toUpperCase() 方法
console.log(geeks.toUpperCase());

// toLowerCase() 方法
console.log(geeks.toLowerCase());
```

### **正则表达式**

正则表达式  是一个字符序列，它构成一个搜索模式。搜索模式可以用于文本搜索和文本替换操作。正则表达式可以是单个字符或更复杂的模式。

**语法：**

```
/pattern/modifiers;
```

**你也可以使用 `RegExp()` 在 JavaScript 中创建正则表达式：**

```
const regex1 = /^ab/;
const regex2 = new RegExp('/^ab/');
```

让我们看看 JavaScript 如何允许正则表达式：

### **正则表达式修饰符：**

修饰符可以用于执行多行搜索。JavaScript 中允许的一些模式修饰符：

| 修饰符 | 描述                               |
| :----- | :--------------------------------- |
| [abc]  | 查找括号内的任何字符。             |
| [0-9]  | 查找括号内 0 到 9 之间的任何数字。 |
| (x\|y) | 查找用 `                           |

### **正则表达式模式：**

元字符是具有特殊含义的字符。JavaScript 中允许的一些元字符：

| 元字符 | 描述                                      |
| :----- | :---------------------------------------- |
| .      | 用于查找单个字符，换行符或行终止符除外。  |
| \d     | 用于查找数字。                            |
| \s     | 用于查找空白字符。                        |
| \uxxxx | 用于查找由十六进制数指定的 Unicode 字符。 |

### **量词：**

它们提供输入中字符、组或字符类的最小实例数，以便找到匹配项。JavaScript 中允许的一些量词如下：

| 量词 | 描述                                    |
| :--- | :-------------------------------------- |
| n+   | 用于匹配包含至少一个 n 的任何字符串。   |
| n*   | 用于匹配包含零个或多个 n 的任何字符串。 |
| n?   | 用于匹配包含零个或一个 n 的任何字符串。 |
| n\\{x\\} | 匹配包含 X 个 n 序列的字符串。          |
| ^n   | 匹配第一个位置是 n 的字符串。           |

以下是一个示例，可以帮助你更好地理解正则表达式。

```
// 验证电子邮件地址的程序
function validateEmail(email) \\{
  // 电子邮件的正则表达式模式
  const re = /\S+@\S+\.\S+/g;

  // 检查电子邮件是否有效
  let result = re.test(email);

  if (result) \\{
    console.log("电子邮件有效。");
  \\} else \\{
    console.log("电子邮件无效。");
  \\}
\\}

// 输入电子邮件 ID
let email = "abc@gmail.com";
validateEmail(email);

email = "abc#$#@45com";
validateEmail(email);
```

### **数据转换**

数据转换是将数据从一种格式转换为另一种格式。它可以通过使用高阶函数来完成，高阶函数可以接受一个或多个函数作为输入，并返回一个函数作为结果。所有将函数作为输入的高阶函数都是 `map()`、`filter()` 和 `reduce()`。

| 方法     | 描述                                   | 语法                                                         |
| :------- | :------------------------------------- | :----------------------------------------------------------- |
| map()    | 迭代数组并对数组的每个元素调用函数。   | `array.map(function(currentValue, index, arr), thisValue)`   |
| filter() | 在应用条件后从给定数组创建一个新数组。 | `array.filter(callback(element, index, arr), thisValue)`     |
| reduce() | 使用函数将数组简化为单个值。           | `array.reduce(function(total, currentValue, currentIndex, arr), initialValue)` |

```
const num = [16, 25];

/* 使用 JS map() 方法 */
console.log(num.map(Math.sqrt));

const ages = [19, 37, 16, 42];

/* 使用 JS filter() 方法 */
console.log(ages.filter(checkAdult));

function checkAdult(age) \\{
  return age >= 18;
\\}

/* 使用 JS reduce() 方法 */
const numbers = [165, 84, 35];
console.log(numbers.reduce(myFunc));

function myFunc(total, num) \\{
  return total - num;
\\}
```

### **日期对象**

日期对象  是 JavaScript 语言的内置数据类型。它用于处理和更改日期和时间。声明日期有四种不同的方法，基本方法是通过 `new Date()` 运算符创建日期对象。**语法：**

```
new Date()
new Date(milliseconds)
new Date(dataString)
new Date(year, month, date, hour, minute, second, millisecond)
```

JavaScript 中有各种方法用于获取日期和时间值或创建自定义日期对象。其中一些方法如下：

| 方法          | 描述                                           |
| :------------ | :--------------------------------------------- |
| getDate()     | 用于返回月份中的日期，以数字形式表示（1-31）。 |
| getTime()     | 用于获取自 1970 年 1 月 1 日以来的毫秒数。     |
| getMinutes()  | 返回当前分钟数（0-59）。                       |
| getFullYear() | 返回当前年份，以四位数的值表示（yyyy）。       |
| getDay()      | 返回一个数字，表示星期几（0-6）。              |
| parse()       | 返回自 1970 年 1 月 1 日以来的毫秒数。         |
| setDate()     | 返回当前日期，以数字形式表示（1-31）。         |
| setTime()     | 设置时间（自 1970 年 1 月 1 日以来的毫秒数）。 |

```
// 这里通过创建一个日期对象来赋值日期
let DateObj = new Date("October 13, 1996 05:35:32");

// getDate()
let A = DateObj.getDate();

// 打印月份中的日期
console.log(A);

// getTime()
let B = DateObj.getTime();

// 打印毫秒数的时间。
console.log(B);

// getMinutes()
let minutes = DateObj.getMinutes();

// 打印分钟数。
console.log(minutes);

// getFullYear()
let C = DateObj.getFullYear();

// 打印年份
console.log(C);

// getDay()
let Day = DateObj.getDay();

// 打印星期几
console.log("星期几的数字：" + Day);

// setDate
DateObj.setDate(15);

let D = DateObj.getDate();

// 打印月份中的新日期
console.log(D);

// parse()，以错误的日期字符串作为输入。
let date = "February 48, 2018 12:30 PM";

// 调用 parse 函数。
let msec = Date.parse(date);
console.log(msec);
```

### **DOM**

DOM  代表**文档对象模型**。它定义了文档的逻辑结构以及访问和操作文档的方式。JavaScript 无法理解 HTML 文档中的标签，但可以理解 DOM 中的对象。以下是 JavaScript 提供的一些用于操作 DOM 中的节点及其属性的方法：

| 方法                   | 描述                                              |
| :--------------------- | :------------------------------------------------ |
| appendChild()          | 添加一个新的子节点作为最后一个子节点。            |
| cloneNode()            | 复制 HTML 元素。                                  |
| hasAttributes()        | 如果元素有任何属性，则返回 true，否则返回 false。 |
| removeChild()          | 使用 `Child()` 方法从元素中移除子节点。           |
| getAttribute()         | 返回元素节点提供的属性的值。                      |
| getElementsByTagName() | 返回所有子元素的列表。                            |
| isEqualNode()          | 确定两个元素是否相同。                            |

```
<!DOCTYPE html>
<html>
<head>
  /* CSS 用于美化输出 */
  <style>
    #sudo \\{
      border: 1px solid green;
      background-color: green;
      margin-bottom: 10px;
      color: white;
      font-weight: bold;
    \\}

    h1, h2 \\{
      text-align: center;
      color: green;
      font-weight: bold;
    \\}
  </style>
</head>
<body>
  <h1>GeeksforGeeks</h1>
  <h2>DOM appendChild() 方法</h2>
  <div id="sudo">
    好的网站是学习计算机科学的地方 -
  </div>
  <button onclick="geeks()">提交</button>
  <br />
  <div style="border: 3px solid green">
    <h1>GeeksforGeeks</h1>
    <h2>一个面向极客的计算机科学门户网站</h2>
  </div>
  <h2>DOM cloneNode() 方法</h2>
  <button onclick="nClone()">
    点击这里克隆上面的元素。
  </button>
  <br />
  <h2>DOM hasAttributes() 方法</h2>
  <p id="gfg">
    点击按钮检查 body 元素是否有任何属性
  </p>
  <button type="button" onclick="hasAttr()">
    提交
  </button>
  <br />
  <h2>DOM removeChild() 方法</h2>
  <p>排序算法</p>
  <ul id="listitem">
    <li>插入排序</li>
    <li>归并排序</li>
    <li>快速排序</li>
  </ul>
  <button onclick="Geeks()">
    点击这里！
  </button>
  <br />
  <h2>DOM getAttribute() 方法</h2>
  <br />
  <button id="button" onclick="getAttr()">
    提交
  </button>
  <p id="gfg1"></p>
  <br />
  <h2>DOM getElementsByTagName()</h2>
  <p>一个面向极客的计算机科学门户网站。</p>
  <button onclick="getElement()">
    试一试
  </button>
  <h3>DOM isEqualNode() 方法。</h3>
  <!-- 3 个 div 元素 -->
  <div>GeeksforGeeks</div>
  <div>GfG</div>
  <div>GeeksforGeeks</div>
  <button onclick="isequal()">
    检查
  </button>
  <p id="result"></p>
  <script>
    function geeks() \\{
      var node = document.createElement("P");
      var t = document.createTextNode("GeeksforGeeks");
      node.appendChild(t);
      document.getElementById("sudo").appendChild(node);
    \\}
    function nClone() \\{
      // 使用变量 geek 访问 div 属性
      var geek = document.getElementsByTagName("DIV")[0];

      // 将 geek 变量克隆到名为 clone 的变量中
      var clone = geek.cloneNode(true);

      // 将我们的 clone 变量添加到文档末尾
      document.body.appendChild(clone);
    \\}
    function hasAttr() \\{
      var s = document.body.hasAttributes();
      document.getElementById("gfg").innerHTML = s;
       \\}

    function Geeks() \\{
      var doc = document.getElementById("listitem");
      doc.removeChild(doc.childNodes[0]);
    \\}

    /* 使用 getElementById */
    function getAttr() \\{
      var rk = document.getElementById("button").getAttribute("onClick");
      document.getElementById("gfg1").innerHTML = rk;
    \\}

    /* 使用 getElementsByTagName */
    function getElement() \\{
      var doc = document.getElementsByTagName("p");
      doc[0].style.background = "green";
      doc[0].style.color = "white";
    \\}

    /* 检查是否相等 */
    function isequal() \\{
      var out = document.getElementById("result");
      var divele = document.getElementsByTagName("div");
      out.innerHTML +=
        "元素 1 等于元素 1：" +
        divele[0].isEqualNode(divele[0]) +
        "<br/>";
      out.innerHTML +=
        "元素 1 等于元素 2：" +
        divele[0].isEqualNode(divele[1]) +
        "<br/>";
      out.innerHTML +=
        "元素 1 等于元素 3：" +
        divele[0].isEqualNode(divele[2]) +
        "<br/>";
    \\}
  </script>
</body>
</html>
```

### **数字和数学**

JavaScript 提供了各种属性和方法来处理数字和数学运算。

数字属性  包括最大值、最小值、NaN（非数字）、负无穷大、正无穷大等等。JavaScript 中用于处理数字的一些方法如下：

| 方法            | 描述                                 |
| :-------------- | :----------------------------------- |
| valueOf()       | 以原始形式返回数字。                 |
| toString()      | 返回整数的字符串表示形式。           |
| toFixed()       | 返回带有指定小数位数的数字字符串。   |
| toPrecision()   | 将数字转换为指定长度的字符串。       |
| toExponential() | 返回以指数表示法表示的舍入后的数字。 |

```
<script type="text/javascript">
  var num = 213;
  var num1 = 213.3456711;

  // JS valueOf() 方法
  console.log("输出：" + num.valueOf());

  // JS toString() 方法
  console.log("输出：" + num.toString(2));

  // JS toFixed() 方法
  console.log("输出：" + num1.toString(2));

  // JS toPrecision() 方法
  console.log("输出：" + num1.toPrecision(3));

  // JS toExponential() 方法
  console.log("输出：" + num1.toExponential(4));
</script>
```

JavaScript 提供了 `Math` 对象，用于对数字执行数学运算。`Math` 对象有许多属性，包括欧拉数、圆周率、平方根、对数等等。JavaScript 中用于处理数学属性的一些方法如下：

| 方法           | 描述                              |
| :------------- | :-------------------------------- |
| max(x, y, z…n) | 返回最大值。                      |
| min(x, y, z…n) | 返回最小值。                      |
| exp(x)         | 返回 x 的指数值。                 |
| log(x)         | 返回 x 的自然对数（以 E 为底）。  |
| sqrt(x)        | 返回 x 的平方根值。               |
| pow(x, y)      | 返回 x 的 y 次方。                |
| round(x)       | 将 x 的值四舍五入到最接近的整数。 |
| sin(x)         | 求 x 的正弦值（x 为弧度）。       |
| tan(x)         | 求角度 (x) 的正切值。             |

```
<script>
  document.getElementById("GFG").innerHTML =
    "Math.LN10: " + Math.LN10 + "<br>" +
    "Math.LOG2E: " + Math.LOG2E + "<br>" +
    "Math.Log10E: " + Math.LOG10E + "<br>" +
    "Math.SQRT2: " + Math.SQRT2 + "<br>" +
    "Math.SQRT1_2: " + Math.SQRT1_2 + "<br>" +
    "Math.LN2: " + Math.LN2 + "<br>" +
    "Math.E: " + Math.E + "<br>" +
    "Math.round: " + Math.round(5.8) + "<br>" +
    "Math.PI: " + Math.PI + "<br>" +
    "<p><b>Math.sin(90 * Math.PI / 180):</b> " +
    Math.sin(90 * Math.PI / 180) + "</p>
 " +
    "<p><b>Math.tan(90 * Math.PI / 180):</b> " +
    Math.tan(90 * Math.PI / 180) + "</p>
 " +
    "<p><b>Math.max(0, 150, 30, 20, -8, -200):</b> " +
    Math.max(0, 150, 30, 20, -8, -200) + "</p>
 " +
    "<p><b>Math.min(0, 150, 30, 20, -8, -200):</b> " +
    Math.min(0, 150, 30, 20, -8, -200) + "</p>
 " +
    "<p><b>Math.pow(3,4):</b> " + Math.pow(3, 4) + "</p>
 ";
</script>
```

### **事件**

JavaScript 中的 事件  提供了与网页的动态交互。当用户或浏览器操作页面时，就会发生事件。这些事件与文档对象模型 (DOM) 中的元素相关联。JavaScript 支持的一些事件如下：

| 事件          | 描述                                 |
| :------------ | :----------------------------------- |
| onclick()     | 当点击元素时触发事件。               |
| onkeyup()     | 当按下键后释放键时执行指令。         |
| onmouseover() | 当鼠标指针悬停在元素上时触发事件。   |
| onmouseout()  | 当鼠标指针移出元素时触发事件。       |
| onchange()    | 检测监听此事件的任何元素的值的变化。 |
| onload()      | 当元素完全加载时触发事件。           |
| onfocus()     | 当元素获得焦点时触发。               |
| onblur()      | 当元素失去焦点时触发事件。           |
| onsubmit()    | 当提交表单时触发事件。               |
| ondrag()      | 当拖动元素时触发事件。               |
| oninput()     | 当输入字段获取任何值时触发。         |

```
<!DOCTYPE html>
<html>
<head>
  /* CSS 用于美化输出 */
  <style>
    #geeks \\{
      border: 1px solid black;
      padding: 15px;
      width: 60\\%;
    \\}

    h1 \\{
      color: green;
    \\}
  </style>
  <script>
    function hiThere() \\{
      alert("你好！");
    \\}
    function focused() \\{
      var e = document.getElementById("inp");
      if (confirm("明白了吗？")) \\{
        e.blur();
      \\}
    \\}

    /* 鼠标悬停事件 */
    document.getElementById("hID").addEventListener("mouseover", over);

    /* 鼠标移出事件 */
    document.getElementById("hID").addEventListener("mouseout", out);

    /* 悬停时变为绿色 */
    function over() \\{
      document.getElementById("hID").style.color = "green";
    \\}

    /* 移出时变为黑色 */
    function out() \\{
      document.getElementById("hID").style.color = "black";
    \\}

    function Geeks() \\{
      var x = document.getElementById("GFG").value;
      document.getElementById("sudo").innerHTML = "选择的科目：" + x;
    \\}

    /* 成功提醒 */
    function Geek() \\{
      alert("表单提交成功。");
    \\}
    function Function() \\{
      document.getElementById("geeks").style.fontSize = "30px";
      document.getElementById("geeks").style.color = "green";
    \\}
  </script>
</head>
<body>
  <!-- onload 事件 -->
  <img onload="alert("图片完全加载")" alt="GFG-Logo"
    src="https://media.geeksforgeeks.org/wp-content/cdn-uploads/GeeksforGeeksLogoHeader.png" />
  <br />

  <!-- onclick 事件 -->
  <h2>onclick 事件</h2>
  <button type="button" onclick="hiThere()">
    点击我
  </button>

  <!-- onfocus 事件 -->
  <h2>onfocus 事件</h2>
  <p>将焦点放在下面的输入框中：</p>
  <input id="inp" onfocus="focused()" />

  <!-- onblur 事件 -->
  <h2>onblur 事件</h2>
  <p>
    在输入框中输入一些内容，
    然后点击文档主体中的其他位置。
  </p>
  <input onblur="alert(this.value)" />

  <!-- onmouseover 和 onmouseout 事件 -->
  <h2 id="hID">onmouseover 事件</h2>
  <h2>onchange 事件</h2>
  <p>选择科目：</p>
  <select id="GFG" onchange="Geeks()">
    <option value="Data Structure">
      数据结构
    </option>
    <option value="Algorithm">
      算法
    </option>
    <option value="Computer Network">
      计算机网络
    </option>
    <option value="Operating System">
      操作系统
    </option>
    <option value="HTML">
      HTML
    </option>
  </select>

  <p id="sudo"></p>

  <!-- onsubmit 事件 -->
  <h2>onsubmit 事件</h2>
  <form onsubmit="Geek()">
    名：<input type="text" value="" />
    <br />
    姓：<input type="text" value="" />
    <br />
    <input type="submit" value="提交" />
  </form>

  <!-- ondrag 事件 -->
  <h2>ondrag 事件属性</h2>
  <div id="geeks" ondrag="Function()">
    GeeksforGeeks：一个面向极客的计算机科学门户网站
  </div>
</body>
</html>
```

### **错误**

在执行 JavaScript 代码时，当 JavaScript 引擎遇到语法无效的代码时，肯定会发生 错误。这些错误可能是由于程序员方面的错误、输入错误，甚至是程序逻辑问题造成的。JavaScript 中有一些语句可以处理这些错误：

| 语句    | 描述                           |
| :------ | :----------------------------- |
| try     | 测试代码块以检查错误。         |
| catch   | 处理错误（如果有）。           |
| throw   | 允许构造新的错误。             |
| finally | 在 try 和 catch 之后执行代码。 |

```
<!DOCTYPE html>
<html>
<body>
  <h2>
    JavaScript throw try catch finally 关键字
  </h2>
  <p>请输入一个数字：</p>
  <input id="demo" type="text" />
  <button type="button" onclick="myFunction()">
    测试输入
  </button>
  <p id="p01"></p>
  <script>
    function myFunction() \\{
      const message = document.getElementById("p01");
      message.innerHTML = "";
      let x = document.getElementById("demo").value;

      /* 使用 try.. catch.. 和条件 */
      try \\{
        if (x == "") throw "为空";
        if (isNaN(x)) throw "不是数字";
        x = Number(x);
        if (x > 20) throw "太高";
        if (x <= 20) throw "太低";
      \\} catch (err) \\{
        message.innerHTML = "输入" + err;
      \\} finally \\{
        document.getElementById("demo").value = "";
      \\}
    \\}
  </script>
</body>
</html>
```

### **窗口属性**

窗口对象  是 DOM 层次结构的最顶层对象。每当屏幕上出现一个窗口来显示文档的内容时，就会创建一个窗口对象。要访问窗口对象的属性，你需要指定对象名称，后跟一个句点符号 (.) 和属性名称。

**语法：**

```
window.property_name
```

下表列出了常用的一些 Window 对象的属性和方法：

| 属性      | 描述                                           |
| :-------- | :--------------------------------------------- |
| window    | 返回当前窗口或框架。                           |
| screen    | 返回窗口的 Screen 对象。                       |
| toolbar   | 创建一个工具栏对象，可以在窗口中切换其可见性。 |
| navigator | 返回窗口的 Navigator 对象。                    |
| frames[]  | 返回当前窗口中的所有 `` 元素。                 |
| document  | 返回对 document 对象的引用。                   |
| closed    | 布尔值，用于检查窗口是否已关闭。               |
| length    | 表示当前窗口中的框架数量。                     |
| history   | 提供窗口的 History 对象。                      |

```
<!DOCTYPE html>
<html>
<body>
  <h1>窗口属性</h1>
  <h2>origin 属性</h2>

  <p id="demo"></p>
  <br />
  <button type="button" onclick="getResolution();">
    获取分辨率
  </button>
  <br />
  <button type="button" onclick="checkConnectionStatus();">
    检查连接状态
  </button>
  <br />
  <button type="button" onclick="getViews();">
    获取浏览次数</button>
  <br />
  <p>
    <button onclick="closeWin()">
      关闭“myWindow”
    </button>
  </p>

  <script>
    // JS location 属性
    let origin = window.location.origin;
    document.getElementById("demo").innerHTML = origin;

    // JS screen 属性
    function getResolution() \\{
      alert("你的屏幕分辨率是：" + screen.width + "x" + screen.height);
    \\}

    // JS toolbar 属性
    var visible = window.toolbar.visible;

    // JS navigator 属性
    function checkConnectionStatus() \\{
      if (navigator.onLine) \\{
        alert("应用程序在线。");
      \\} else \\{
        alert("应用程序离线。");
      \\}
    \\}
    // JS history 属性
    function getViews() \\{
      alert(
        "你在本次会话中访问了 " + history.length + " 个网页。"
      );
    \\}
    // JS close 属性
    let myWindow;
    function closeWin() \\{
      if (myWindow) \\{
        myWindow.close();
      \\}
    \\}
  </script>
</body>
</html>
```

| 方法           | 描述                                     |
| :------------- | :--------------------------------------- |
| alert()        | 在警报框中显示一条消息和一个“确定”按钮。 |
| print()        | 打印当前窗口的内容。                     |
| blur()         | 移除当前窗口的焦点。                     |
| setTimeout()   | 在指定的时间间隔后计算表达式。           |
| clearTimeout() | 移除使用 `setTimeout()` 设置的定时器。   |
| setInterval()  | 以用户定义的间隔计算表达式。             |
| prompt()       | 显示一个对话窗口，请求访客提供反馈。     |
| close()        | 关闭当前打开的窗口。                     |
| focus()        | 设置当前窗口的焦点。                     |
| resizeTo()     | 将窗口调整为提供的宽度和高度。           |

```
<!DOCTYPE html>
<html>
<head>
  <title>JavaScript Window 方法</title>
  /* CSS 用于美化输出 */
  <style>
    .gfg \\{
      font-size: 36px;
    \\}

    form \\{
      float: right;
      margin-left: 20px;
    \\}
  </style>
</head>
<body>
  <div class="gfg">JavaScript Window 方法</div>
  <br />
  <button onclick="windowOpen()">
    JavaScript window Open
  </button>
  <button onclick="resizeWin()">
    JavaScript window resizeTo
  </button>
  <button onclick="windowBlur()">
    JavaScript window Blur
  </button>
  <button onclick="windowFocus()">
    JavaScript window Focus
  </button>
  <button onclick="windowClose()">
    JavaScript window Close
  </button>
  <br />
  <br />
  <p id="g"></p>
  <form>
    <button onclick="setTimeout(wlcm, 2000);">
      2 秒后弹出提示
    </button>
    <button onclick="geek()">点击我！</button>
    <input type="button" value="打印" onclick="window.print()" />
  </form>
  <br /><br />
  <button id="btn" onclick="fun()" style="color: green">
    JavaScript 使用 setTimeOut
  </button>
  <button id="btn" onclick="stop()">
    JavaScript clearTimeout
  </button>
  <script>
    var gfgWindow;

    // 打开新窗口的函数
    function windowOpen() \\{
      gfgWindow = window.open(
        "https://www.geeksforgeeks.org/",
        "_blank",
        "width=200, height=200"
      );
    \\}

    // 调整打开窗口大小的函数
    function resizeWin() \\{
      gfgWindow.resizeTo(400, 400);
      gfgWindow.focus();
    \\}

    // 关闭打开窗口的函数
    function windowClose() \\{
      gfgWindow.close();
    \\}

    // 使打开窗口失去焦点的函数
    function windowBlur() \\{
      gfgWindow.blur();
    \\}

    // 使打开窗口获得焦点的函数
    function windowFocus() \\{
      gfgWindow.focus();
    \\}

    // 警报函数
    function wlcm() \\{
      alert("欢迎来到 GeeksforGeeks");
    \\}

    // 提示函数
    function geek() \\{
      var doc = prompt("请输入一些文本", "GeeksforGeeks");
      if (doc != null) \\{
        document.getElementById("g").innerHTML = "欢迎来到 " + doc;
      \\}
    \\}

    // setTimeout 和 clearTimeout 函数
    var t;
    function color() \\{
      if (document.getElementById("btn").style.color == "blue") \\{
        document.getElementById("btn").style.color = "green";
      \\} else \\{
        document.getElementById("btn").style.color = "blue";
      \\}
    \\}
    function fun() \\{
      t = setTimeout(color, 3000);
    \\}
    function stop() \\{
      clearTimeout(t);
    \\}
  </script>
</body>
</html>
```

### **使用 JavaScript 速查表的好处**

JavaScript 速查表是一个重要的工具，它简化了编写 JavaScript 代码的过程，帮助你的 Web 应用程序顺利运行，并使你能够创建交互式和动态的 Web 内容。

**以下是使用 JavaScript 速查表的一些主要好处：**

- **高效的 Web 开发：** JavaScript 速查表为 Web 开发人员提供了一个快速参考指南，可以更快、更高效地编写代码。它有助于减少花在搜索语法或函数上的时间，从而提高生产力。
- **全面的函数参考：** 速查表包含了大量的 JavaScript 函数、方法和属性，涵盖了从基本变量和运算符到复杂对象和事件的所有内容。这使得它成为初学者和经验丰富的开发人员的宝贵资源。
- **动态内容创建：** 通过在速查表中包含 JavaScript 函数，开发人员可以创建更具交互性和动态性的 Web 内容。它有助于增强网页的用户体验和参与度。
- **互操作性：** JavaScript 是 Web 的核心技术。在使用其他 Web 技术（如 HTML、CSS 和各种 Web 开发框架）时，JavaScript 速查表可能会有所帮助。
- **性能优化：** 使用正确函数和方法编写结构良好的 JavaScript 代码可以显著提高 Web 应用程序的性能。速查表可以指导开发人员创建性能优化的脚本。
- **事件处理：** 速查表涵盖了处理用户交互和浏览器事件的方法，从而实现更具响应性和交互性的 Web 内容。

请记住，使用 JavaScript 速查表可以极大地改善你的 Web 开发过程，使其成为每个 Web 开发人员的必备工具。

> 原文：https://www.geeksforgeeks.org/javascript-cheat-sheet-a-basic-guide-to-javascript/
>
> 译文：https://mp.weixin.qq.com/s/NSDbNp1pZizM1thgpHvhHA