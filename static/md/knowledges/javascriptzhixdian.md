---
title: JavaScript知识点
date: 2020-01-18 10:24:57
categories: 
- 前端知识
tags:
- JavaScript
---

[TOC]

## 概述

js一门运行在浏览器语言

js能做什么：

- 动画效果
- 页面交互效果
- 表单提交
- 与后台进行数据获取/传输
- 操作页面dom
- 操作浏览器
- nodejs
- 封装插件
- 游戏/h5
- …..

js诞生记

布兰登 . 艾奇    10天   函数式编程+ 面向对象编程  1995年

js一门弱类型的轻量级解释型（即时编译型）语言



### JavaScript的组成

|        组成         |     描述      |
| :-----------------: | :-----------: |
|     ECMAscript      |  js基本语法   |
| BOM  浏览器对象模型 |  操作浏览器   |
|  DOM  文档对象模型  | 操作页面/html |

ECMAScript（核心）：JavaScript 语言基础

DOM（文档对象模型）：规定了访问HTML和XML的接口

BOM（浏览器对象模型）：提供了浏览器窗口之间进行交互的对象和方法



### DOM和BOM有什么区别

#### 文档对象模型（Document Object Model）

- DOM 是为了操作文档出现的 API，document 是其的一个对象
- DOM 和文档有关，这里的文档指的是网页，也就是 html 文档。DOM 和浏览器无关，他关注的是网页本身的内容。

#### 浏览器对象模型（Browser Object Model）

- BOM 是为了操作浏览器出现的 API，window 是其的一个对象
- window 对象既为 javascript 访问浏览器提供 API，同时在 ECMAScript 中充当 Global 对象



### 什么是Window对象? 什么是Document对象?

- Window 对象表示当前浏览器的窗口，是JavaScript的顶级对象。

  我们创建的所有对象、函数、变量都是 Window 对象的成员。

  Window 对象的方法和属性是在全局范围内有效的。

- Document 对象是 HTML 文档的根节点与所有其他节点（元素节点，文本节点，属性节点, 注释节点），可以使我们可以通过脚本对 HTML 页面中的所有元素进行访问

  **Document 对象是 Window 对象的一个属性**，可通过 window.document 属性对其进行访问

  Document对象是Documentd对象（HTML 文档对象）的一个只读引用



### js特点

- 弱类型
- 解释性/即时编译型
- 基于对象：一切皆对象
- 事件驱动：鼠标事件，键盘事件等等
- 单线程/异步



### js引入方式

文件后缀： .js

- 嵌入式

  ```html
  <script>
    	alert(1);
  </script>
  ```

- 外部引入

  ```html
  <script src="js路径"></script>
  ```



### js注释

- 单行文本注释

  ```js
  // 单行注释 ctrl + / 
  ```

- 多行文本注释

  ```js
  /*
  	多行文本注释
  */
  shift  +  alt  + a
  ```



### 输入输出工具

|        方法        |          描述          |               示例               |
| :----------------: | :--------------------: | :------------------------------: |
| `document.write()` |   输出内容到body页面   | `document.write("hello, world")` |
|     `prompt()`     |         输入框         |    `prompt("请输入您的姓名")`    |
|     `alert()`      |         弹出框         |          `alert(22222)`          |
|  `console.log()`   | 输出内容到浏览器控制台 |     `console.log("js真好")`      |



### 变量

> 采用var  声明变量

声明变量规则：

![image-20200820095245168](C:\Users\a\AppData\Roaming\Typora\typora-user-images\image-20200820095245168.png)

- 严格区分大小写
- 可以使用字母，_  或者 $ 开头，不可以使用中文
- js命名习惯
  - 驼峰命名法  getElementById
  - 首字母大写： Object
- 命名要有意义



声明一个变量： `var num;`

声明多个变量： `var a, b, c;` 

初始化：

- 先声明再初始化

  ```js
  var num;
  num = 1;
  ```

- 声明的同时初始化

  ```js
  var num = 2;
  var a = 0, b=1, c;
  ```




### 运算符

算术运算符： 加(+)、减(-)、乘(*)、除(/)、取余(\\%)、自增(++)、自减(--)、求幂(**)

- null 和 false 转换成数字是 0 

- true 转换成数字是 1

- undefined 转换不了是 NaN

- 可以转换成数字的转换成数字进行运算，转换不了就转换成 NaN

- 所有与字符串进行相加都属于字符串拼接

- 字符串除了+运算以外，进行其他运算的时候可以转换成数字就转换成数字进行运算，

  不可以转换的就是NaN

- ++n  先运算在输出， n++ 先输出在运算

- —n   先运算在输出， n-- 先输出在运算

关系(比较)运算符：大于(>)、小于(<)、大于等于(>=)、小于等于(<=)、值相等(==)、值不等(!=)、全等(===)、不全等(!==)

- 可以转换成数字的转换成数字进行比较，转换不了都是false
- 字符串和字符串进行比较，对照着ASCII码表一个字符一个字符进行比较
- == 代表值相等， === 值相等以及数据类型也相等

赋值运算符：=、+=、-=、*=、/=、\\%=、**=

逻辑运算符：与(&&)、或(||)、非(!)

- && 与： 只要有一个是假，结果就是假
- || 或 ： 只要有一个是真，结果就是真
- ！非  ： 取反

  短路原则：&&左边为假右边不执行，||左边为真右边不执行

一元运算符：typeof、new、delete、instanceof等

三元运算符

```js
条件表达式 ?  表达式为真执行 :  表达式为假执行
typeof null == 'object' ? alert(1) : console.log("不等")
```

特殊运算符： , 逗号， 括号()

```js
// 逗号运算符：多个表达式可以用逗号分开，其中用逗号分开的表达式的值分别结算，但整个表达式的值是最后一个表达式的值。
var i=0,j=0; 
for(;j<6,i<10;i++,j++)\\{ 
    k = i+j; 
\\} 
console.log(k);

var i=0,j=0;
for(;i<10,j<6;i++,j++)\\{
    k = i+j;   
\\}
console.log(k);
```



###  流程控制

> ​	流程：代码的执行顺序

|   机构   |               描述               |
| :------: | :------------------------------: |
| 顺序结构 |    代码按照从上到下的顺序执行    |
| 选择结构 | 根据不同的条件来执行不同的代码块 |
| 循环结构 |    代码按照一定的顺序反复执行    |



### 选择结构

if分支

* 单路分支

  ```js	
  if(条件)\\{
      //条件成立执行
  \\}
  ```

* 双路分支

  ```js	
  if(条件)\\{
      //条件成立执行
  \\}else\\{
      //条件不成立执行
  \\}
  ```

* 多路分支

  ```js	
  if(条件1)\\{
      //条件1成立执行
  \\}else if(条件2)\\{
      //条件1不成立；条件2成立执行
  \\}else if(条件3)\\{
      //条件1，条件2不成立；条件3成立执行
  \\}else\\{
      //条件1，条件2，条件3都不成立
  \\}
  ```

* 嵌套分支

  ```js
  if(条件1)\\{
      //条件1成立执行
      if(条件2)\\{
          //条件1成立并且条件2成立执行
      \\}else if(条件3)\\{
          //条件1成立并且条件3条件
          //条件2不成立
      \\}else\\{
          // 条件1成立，条件2/3都不成立执行
      \\}
  \\}else\\{
      //条件1不成立
  \\}
  ```


switch 分支

```js
switch(需要判断的值)\\{
    case 值1：
        当需要判断的值==值1，执行代码
        break;
    case 值2：
        当需要判断的值==值2，执行代码
        break;
    case 值3：
        当需要判断的值==值3，执行代码
        break;
    default:
        默认执行
\\}
```



### 循环结构

* for 循环

  ```js	
  for (初始值;条件;步进值)\\{
      //循环体
  \\}
   奇数之和
  var sum = 0;
  for(i=1;i<100;i++)\\{
      if (i\\%2==1)\\{
        sum +=i;
        continue
    	\\}  
  \\}
  console.log(sum);       
  ```

  break 终止循环

  continue  跳出当前循环

  **如果有两个终止条件，以逗号隔开，是逗号运算符，以最后一个终止条件截止**

* while 循环

  ```js
  while(条件表达式)\\{
      //循环体
  \\}
  
  var i=1;
  do\\{
  	document.write("<div style='width:40px;height:40px;border-		radius:50\\%;background:red;float:left; text-align: center;line-height: 40px;'>"+i+"</div>");
      i++;     
  \\}while(i<=100)
  ```
  
* do while 循环

  ```js
  var i=1;
      do\\{
      document.write("<div style='width:40px;height:40px;border-radius:50\\%;border:10px solid red;float:left; text-align: center;line-height: 40px;'>"+i+"</div>");
      i++;
  \\}while(i<=100)
  ```
  



### for和while选择

1.存在一直循环次数情况下使用for循环

   while循环次数可以不确定

2.使用时优先考虑for循环，当无法写出循环条件的**起始结束步进值**时考虑用while循环



### while和do...while的选择

\- do  while循环的循环体至少执行一次
\- 当循环的判断条件所需的值来自于循环体时，可以使用do  while 循环



### 函数

函数：将包含某一特定的功能的代码封装起来，并且可以重复使用

* 方便代码重复使用
* 可以传入不同的参数返回不同的结果
* 代码更加简洁



### 函数声明

* 具名函数

  ```js 
  function 函数名称()\\{
      函数体
  \\}
  //例如
  function fn()\\{
      console.log("具名函数")
  \\}
  //函数名称 都是一般都是英文开头  也可以是_开头  不能是是数字 中文
  ```

* 匿名函数         

  ```js 
  var 变量名=function()\\{
      函数体
  \\}
  //例如
  var fun = function()\\{
      console.log("匿名函数")
  \\}
  //函数名称 都是一般都是英文开头  也可以是_开头  不能是是数字 中文
  ```

* 实例化构造函数

  ```js
  var 变量名 = new Function();
  //例如
  var b = new Function(
  	console.log("实例化构造函数")
  );
  ```



### 函数调用

* 通过括号()调用

  ```js	
  函数名称();   //具名函数调用：fn()
  变量名();     //匿名函数调用：fun()  | b()
  ```

* 自调用

  ```js	
  //第一种
  (function()\\{
  	函数体
  \\})();
  
  //第二种
  (function()\\{
  	函数体
  \\}());
  
  //第三种
  !function()\\{
  	函数体
  \\}();
  ```
  
* 通过事件方式调用

  ```html
  <div onclick = "函数名()"></divs>
  ```



### 注意事项

- [ ] 具名函数可以在函数前后都可以调用匿名函数只能在后面调用前面调用会报错

- [ ] 如果具名函数或者匿名函数函数名或者变量名相同的情况下，后面的函数会将前面的函数替换掉，

- [ ] 在不同的script代码块，不管是具名函数还是匿名函数只能在后面的代码块中调用，前面的代码块中调用会报错。

  

### 参数

函数根据不同的参数返回不同的结果

类型：

* 实参：(函数调用时传入的参数)

* 形参：(函数声明时接收的参数)

  ```js
  //输出1-n
  function fn(n)\\{  //n是形参
      for(var i=1;i<=n;i++ ) \\{
          document.write(i);
      \\}
  \\}
  fn(100);//100是实参
  ```
  

![image-20200821144149059](C:\Users\a\AppData\Roaming\Typora\typora-user-images\image-20200821144149059.png)

#### 注意事项

参数可以是任意类型的数据

参数命名

参数的个数

* 实参和形参的个数都是一一对应的

  ```js
  function fn(num,str)\\{
      //num =100;str="abc";
  \\}
  fn(100,"abc");
  ```

* 形参的个数 大于  实参的个数是，多余的形参的值为undefined

  ```js
  function fn(num,str,flag)\\{
      //num =100;str="abc"   flag=undefined;
  \\}
  fn(100,"abc");
  ```

* 形参 小于 实参的情况下,函数在声明的同时会隐式创建`arguments`对象，多余的实参可以通过`arguments`这个对象获取    这个arguments只能在函数内部使用

  ```js
  //arguments  只能在函数内部使用
  function fn(num)\\{
      //num =100;
      console.log(arguments);
      console.log(arguments.length);  //形参的个数
      console.log(arguments[1]);  //"abc"
    	console.log(arguments[2]);  //true
  \\}
  fn(100,"abc"，true);
  ```




### 函数返回值

> 需要将函数的结果进行操作，通过return进行函数返回

* 返回值可以是任意类型的值

* 终止当前函数

* 每个函数都有返回值，如果没有返回值，默认返回值是`undefined`

* 函数只能返回一个值，如果写多个返回值，返回的是最后一个值

  ```js 
  function fn()\\{
      return 1,true,'abc';
  \\}
  var str = fn();
  conlose.log(str);  //'abc'
  ```



### 简介基本类型和引用类型

> 摘自《高程3》版本 朋友推荐《高性能JS》这部分讲的比较细致

#### 变量类型

- JavaScript 是`变量松散类型`，不存在定义某个变量必须要保存何种数据类型规则，变量的值及其数据类型可以在脚本的生命周期内改变。

#### 基本类型 引用类型

> 在将一个值赋值给变量时，解析器必须确定这个值是基本类型值还是引用类型值。

**基本类型值**

- Undefined
- Null
- Boolean
- Number
- String

**引用类型值**

- 引用类型值是保存在内存中的对象，与其他语言不同，JS不允许直接访问内存中的位置，也就是不能直接操作对象的内存空间。
- 在操作对象时，实际上是在操作对象的引用而不是实际的对象，为此，引用类型的值是按引用访问的。

#### 动态的属性

- 定义基本类型值和引用类型值的方式是类似的： 创建一个变量并为该变量赋值。
- 对于引用类型的值，我们可以为其添加属性和方法，也可以改变和删除其属性和方法。

#### 复制变量值

> 除了保存的方式不同外，再从一个变量向另一个变量赋值基本类型值和引用类型值时，也不同。

**基本类型**

- 如果从一个变量向另一个变量复制基本类型的值，会在变量对象上创建一个新值，然后把该值复制到心变量分配的位置上。

**引用类型**

- 当从一个变量向另一个变量复制引用类型的值时，同样也会将存储在变量对象中的值复制一份放到为心变量分配的空间中。
- 不同的是，这个值的副本实际上是一个指针，而这个指针指向存储在`堆`中的一个对象。

#### 传递参数

- 所有函数的参数都是**按值**传递的，但是会根据值的类型——`基本类型值`、`引用类型值`产生两种复制方式。
- 在向参数传递引用类型的值时，会把这个值在内存中的地址复制给一个局部变量，因此这个局部变量的变化会反映在函数的外部。
- 在向参数传递基本类型的值时，被传递的值会被复制给一个局部变量（即命名参数，或者用ECMAScript的概念来说，就是arguments对象中的一个元素）。
- 假如将对象obj作为参数传递给函数，当在函数内部重写obj时，这个变量引用的就是一个局部对象了。而这个局部对象会在函数执行完毕后立即被销毁。
- 在向参数传递基本类型的值时，被传递的值会复制给一个局部变量（即命名参数，或者用ECMAScrip的概念来说，就是arguments对象中的一个元素）。
- 在向参数传递引用类型的值时，会把这个值在内存中的地址复制给一个局部变量。

#### 类型检测

- 基本类型使用 `typeof`
- 引用类型使用 `instanceof`



### 执行环境和作用域

#### 概念

- 执行环境（有时也称`环境`）。
- 执行环境定义了变量和函数有权访问的其他数据，决定了他们各自的行为。
- 每个执行环境都有一个与之关联的变量对象（ `varibale object` ）
- 环境中定义的所有变量和函数都保存在这个对象中。
- 我们编写的代码无法访问这个对象，但是解析器在处理数据时会在后台使用它。

**全局执行环境**

- 全局执行环境是最外围的一个执行环境。根据`ECMAScript`实现所在的宿主环境不用，表示执行环境的对象也不一样。
- 在`Web`浏览器中，全局执行环境被认为是`window对象`，因此所有全局变量和函数都是作为`window对象`的属性和方法创建的。
- 某个执行环境中的所有代码执行完毕后，该环境被销毁，保存在其中的所有变量和函数定义也随之销毁。
- 全局执行华景知道引用程序退出： 例如关闭网页或浏览器时才会被销毁。

**作用域链**

- 当代码在一个环境中执行时，会创建变量对象的一个`作用域链`。
- `作用域链`的用途，是保证对执行环境有权访问的所有变量和函数的有序访问。
- 作用域链的前端，始终都是当前执行的代码所在环境的变量对象。
- 如果这个环境是函数，则将其`活动对象`作为变量对象。
- 活动对象在最开始时，只包含一个变量，即`arguments`对象（这个对象在全局环境中是不存在的）
- 作用域链中的下一个变量对象来自包含（外部）环境，而在下一个变量对象则来自下一个包含环境。这样，一直延续到全局环境。
- 全局执行环境的变量对象始终都是作用域链中的最后一个对象。

**标识解析**

- 沿着作用域链一级一级地搜索标识符的过程。
- 搜索过程始终从作用域链的前端开始，然后逐级地向后回溯，直至找到标识符为止。
- 如果找不到标识符，通常会发生错误。

#### 延长作用域链

- 执行环境的类型总共有两种——全局和局部（函数）。
- 有些语句可以在作用域链的前端临时增加一个变量对象，该变量对象会在代码执行后被移除。
- `try-catch`的`catch`块、 `with`

**catch和with**

- 这两个语句都谁在作用域链的前端添加一个变量对象。
- 对`with`语句来说，会将指定对象添加到作用域链中。
- 对`catch`语句来说，会创建一个新的变量对象，其中包含的是被抛出的错误对象的声明。
- 在<=IE8版本的JS实现中，存在一个与标准不一致的地方，在`catch`语句中捕获的错误对象会被添加到执行环境的变量对象，而不是`catch`语句的变量对象中

#### 没有块级作用域

- 花括号在JS中并不是一个块级作用域(es6是了)。

**声明变量**

- 使用`var`申明的变量会自动被添加到最接近的环境中。
- 如果初始化变量时，没有使用`var`声明，该变量会自动被添加到全局环境。
- 不声明而直接初始化变量是一个常见的错误做法，在严格模式下，初始化未经声明的变量会导致错误。

**查询标识符**

- 当在某个环境中为了读取或写入而引用一个标识符时，必须通过搜索来确定该标识符实际代表什么。
- 搜索过程从作用域链的前端开始，向上逐级查询与给定名字匹配的标识符。
- 如果再局部环境中找到了该标识符，搜索过程停止，变量就绪。
- 如果在局部环境中没有找到该变量名，则继续沿作用域链向上搜索。
- 搜索过程将一直追溯到全局环境的变量对象。
- 如果在全局环境中也没有找到这个标识符，这意味着该变量尚未声明。



### 作用域

> 作用域就是一般代码的作用范围

环境：

* 宿主环境：浏览器
* 执行环境：
  * 全局环境、全局变量
  * 局部环境/函数环境
  * eval()

- [ ] 全局环境：在全局环境使用var 声明的变量属于全局变量

- [ ] 局部环境：在函数内部的叫局部环境


```js
function  fn()\\{
    var num =1;
    console.log(num);  //1
\\}
console.log(num);  //报错num is not defined
```

**作用域链**：在函数内部嵌套多个函数，全局环境与多个函数环境进行嵌套，变量会在当前环境中找，如果当前环境中没有则去上一个环境找，直到找到全局环境为止，**如果变量在当前环境中找到了，并且在声明变量之前，则该变量是undefined，如果是声明变量之后，则是函数内部变量的值。如果全局环境都没有找到，则报错。**

**变量提升**：js在编译过程中，解释器会把所有声明“移动”，到所在作用域的最上面，而赋值其他逻辑会留在原地，这就是变量提升。



### 回调函数

> 将一个函数作为另一个函数的参数，这个函数就叫做回调函数。

```js
function foo(callback)\\{
    callback();
    console.log("主函数");
\\}
foo(function\\{
    console.log("回调函数")
\\})
```



### 递归函数

使用递归实现一些常用的应用：

#### 递归实现阶乘

阶乘是数学上一个常见的算法，类似于上面求和，只是把运算符改为乘法。

```
1*2*3*4*5*...
```

```js
function multi(n) \\{
    if(n == 1)\\{
        return n;
    \\}
    return n*multi(n-1);
\\}

console.log(multi(10));//3628800
```

#### 斐波纳契数列

斐波纳契数列，又称黄金分割数列，指的是这样一个数列：1、1、2、3、5、8、13、21、……

```js
function fibonacci(n) \\{
    if (n == 1 || n == 2) \\{  
        return 1;       
    \\}
    return fibonacci(n-1)+fibonacci(n-2);    
\\}

console.log(fibonacci(10));//55
```

#### 汉诺塔问题

古代有一个梵塔，塔内有三个座A、B、C，A座上有64个盘子，盘子大小不等，大的在下，小的在上。 有一个和尚想把这64个盘子从A座移到C座，但每次只能允许移动一个盘子，并且在移动过程中，3个座上的盘子始终保持大盘在下，小盘在上。在移动过程中可以利用B座。要求输入层数，运算后输出每步是如何移动的。

```js
function  moveDish(level, from, inter, to) \\{ 
    if (level == 1) \\{ 
        console.log("从" + from + " 移动盘子" + level + " 号到" + to);
    \\} else \\{
        // 递归调用：将level-1个盘子从from移到inter(不是一次性移动，每次只能移动一个盘子,其中to用于周转)
        moveDish(level - 1, from, to, inter); // 递归调用，缩小问题的规模
        // 将第level个盘子从A座移到C座
        console.log("从" + from + " 移动盘子" + level + " 号到" + to); 
        // 递归调用：将level-1个盘子从inter移到to,from 用于周转
        moveDish(level - 1, inter, from, to); // 递归调用，缩小问题的规模
    \\}
\\}

moveDish(10,'A','B','C');
```

#### 二叉树问题

二叉树是一个类似 一分二，二分四，四分为八的树状模型，二叉树的每个节点都有左右两个子节点。

二叉树的第n层有几个节点，这个问题比较简单，它的每层节点树是一个有规律的数列，类似1 2 4 8 16 32 ...，使用递归很容易求值。

```js
function tree(n) \\{
    if(n==1)\\{
        return n;
    \\}
    return 2*tree(n-1);
\\}
console.log(tree(10));//512
```

二叉树深度遍历问题，二叉树的深度可以通过三种方法遍历，前序，中序和后序遍历。

```js
function preorderTraversal(root) \\{//前序
    let result = []
    let preorder = (root) => \\{
        if (root) \\{
            result.push(root.value)
            preorderTraversal(root.left)
            preorderTraversal(root.right)
        \\}
    \\}
    return result
\\};

function inorder(root) \\{//中序
    let result = []
    let inorder = (node) => \\{
        if (!node) \\{
            return
        \\}
        inorder(node.left);
        result.push(node.value);
        inorder(node.right);
    \\}
    inorder(root)
    return result
\\};

function postorder(root) \\{//后序
    let result = []
    let postorder = (node) => \\{
        if (!node) \\{
            return
        \\}
        postorder(node.left)
        postorder(node.right)
        result.push(node.value)
    \\}
    postorder(root)
    return result
\\};
```



### 闭包函数

>  闭包（closure）是定义在一个外部函数内部，并且能够访问外部函数中变量的函数。  
>
>  闭包函数的原理是作用链
>
>  在函数内部 返回另一个函数  避免全局变量被污染

```
function  fun()\\{
	return   function()\\{
		retrun 1;
	\\}
\\}

fun()(); 调用到内部的function()
```

闭包特点：

* 函数嵌套函数
* 函数内部可以引用外部的参数和变量
* 参数和变量不会被垃圾回收机制回收

闭包缺点：常驻内存，会增大内存使用量，使用不当容易造成内存泄漏。

闭包优点：

* 希望一个局部变量长期驻扎在内存中
* 避免全局变量的污染
* 私有成员的存在

```js
function fu(n)\\{
    return function(m)\\{
        return n*m
    \\}
\\}

console.log(fu(2)(3)); //6   
```

### 内置顶层函数

>  ECMAscript自带的函数
>  顶层：函数的作用范围，作用范围为全局

\- Number() 任意类型数据转化为数字
\- parselnt() 任意类型数据转化为整数
\- parseFloat() 任意类型数据转化为浮点数
\- String0 任意类型数据转化为字符串
\- Boolean() 任意类型数据转化为布尔值
\- isNaN) 判断一个数据能否转换为数值，如果能转换成数值返回false，不能返回为true
\- eval()；将传入的字符串当做 JavaScript 代码进行执行

```js
eval("2+3”)； //6
eval("alert(1)")； //弹出1
```

Number.isFinite()用来检查一个值是否为有限的。
Number.isNaN(用来检查一个值是否是NaN。
Number.islnteger()用来判断一个值是否为整数。







### 函数重载

后面的函数会将前面的函数覆盖

可以通过argument.length 获取参数的长度

## 数组

> 存放一系列相关数据的容器，为了解决大量数据存储

### 创建数组

* 隐式创建  内部调用实例化构造函数

  ```js
  var arr = [];
  ```

* 实例化构造函数

  ```js
  var arr = new Array();
  ```

### 数组赋值

* 创建的同时赋值

  ```js
  var arr = [1,2,3,4,5,6];
  
  var arr = new Array('a','b','c','d');
  ```

* 创建之后再赋值

  数组按照一定的序号进行赋值，这个序号叫下标

  数组的下标是从0开始的，数组的长度是：数组名.length

  赋值语句：`数组名[下标]`

```js
var arr=[];
arr[0]='a';
arr[1]='b';
arr[3]='d';
console.log(arr);//['a','b','c']

var arr = new Array();
arr[0] =1;
arr[1] =2;
arr[3] =3;
console.log(arr);//[1,2,3]
console.log(arr.length); //数组的长度是4
```

### 数组访问

* 通过下标进行访问:数组名[下标]

  ```js	
  var arr =[1,2,3];
  console.log(arr[0]);   //1
  console.log(arr[2]);   //3
  ```

* 通过数组长度访问:数组名.length

  数组最后一个数据的下标是`数组名.length-1`

  ```js
  var arr=[1,2,3]
  console.log(arr.length); //3
  console.log(arr[arr.length-1]);   //3
  ```

### 数组遍历

* for

  ```js 
  var arr[1,2,3];
  for(var i=0;i<arr.length;i++)\\{
      //i  下标
      console.log(i);  //0 1 2
      // arr[i]  下标对于的值
      console.log(arr[i]); // 1 2 3
  \\}    
  ```

  

* for ... in

  ```js
  var arr[1,2,3];
  for(var i in arr)\\{
      //i  下标
      console.log(i)  //0 1 2
      // arr[i]  下标对于的值
      console.log(arr[i]); // 1 2 3
  \\}
  
  ```

![image-20200928091108077](C:\Users\a\AppData\Roaming\Typora\typora-user-images\image-20200928091108077.png)

![image-20200928091123458](C:\Users\a\AppData\Roaming\Typora\typora-user-images\image-20200928091123458.png)



```js
//数组去重
//方法一：
var arr =[1,2,3,4,5,6,5,4,3,2,1，1，2];
var srr = []
for(var i in arr)\\{
  if(srr.includes(arr[i]))\\{
    continue
  \\}else\\{
    srr[srr.length]=arr[i]
  \\}
\\}
console.log(srr);

//方法二

 for(var i=0;i<arr.length;i++)\\{
            for(var j=i+1; j<arr.length;j++)\\{
                if(arr[i]==arr[j])\\{
                    arr.splice(j,1);
                    j--;
                \\}else\\{
                    continue
                \\}
            \\}
        \\}
```

forEach       for of  遍历



### Math对象

#### Math上的属性

| **属性** | **属性描述**                                      |
| -------- | ------------------------------------------------- |
| **PI**   | 返回圆周率（约等于3.14159）。                     |
| **E**    | 返回算术常量 e，即自然对数的底数（约等于2.718）。 |
| LN2      | 返回 2 的自然对数（约等于0.693）。                |
| LN10     | 返回 10 的自然对数（约等于2.302）。31             |
| LOG2E    | 返回以 2 为底的 e 的对数（约等于 1.414）。        |
| LOG10E   | 返回以 10 为底的 e 的对数（约等于0.434）。        |
| SQRT1_2  | 返回返回 2 的平方根的倒数（约等于 0.707）。       |
| SQRT2    | 返回 2 的平方根（约等于 1.414）。                 |

#### Math的常用方法

​     	加粗表示常用方法

| 方法                      | 方法描述                                    |
| ------------------------- | ------------------------------------------- |
| Math.abs(x)               | 返回x的绝对值。                             |
| **Math.round(x)**         | 返回x四舍五入之后的整数值                   |
| **Math.ceil(x)**          | 返回x的近似值，向上取整                     |
| **Math.floor(x)**         | 返回x的近似值，向下取整                     |
| **Math.max(x,y)**         | 返回x,y中的最大值                           |
| **Math.min(x,y)**         | 返回x,y中的最小值                           |
| **Math.random()**         | 返回一个0~1之间的数字                       |
| Math.trunc(x)             | 将x的小数部分去除，返回整数部分(ie不能使用) |
| **Math.pow(x,y)**         | 取x的y次幂                                  |
| Math.sqrt(x)              | 返回x的平方根                               |
| Math.sin(x)               | 返回x的正弦值                               |
| Math.cos(x)               | 返回x的余弦值                               |
| Math.tan(x)               | 返回x的正切值                               |
| Math.asin(x)              | 返回x的反正弦值                             |
| Math.acos(x)              | 返回x的反余弦值                             |
| Math.atan(x)              | 返回x的反正切值                             |
| NumberObject.toFixed(num) | 可把 Number 四舍五入为指定小数位数的数字    |

#### 小技巧

1. 取x的y次方根

   ```js
   Math.pow(x,1/y)
   ```

2. 查找数组中最大和最小的数字

   ```js
   var arr=[23,4,651,461,1231,411];
   var maxArr=Math.max(...arr);    //  arr数组中的最大值
   var minArr=Math.min(...arr);   //  arr数组中的最小值
   ```

3. 取x-y的随机数、随机整数

   ```js
   Math.floor( Math.random() * (y - x) + x )      // 包含x不包含y
   Math.floor( Math.random() * (y - x + 1) + x  )      // 包含x包含y
   ```

   > 注：取随机整数必须使用`Math.floor`取整， `Math.ceil`和`Math.round`会导致两端的值取到几率变小

生成一个1000到10000之间的随机整数

```
let state = Math.ceil(Math.random() * 9000) + 1000
```

`Math.random()`函数会生成一个0到1之间的随机小数。然后乘以9000，结果的范围就变成了0到9000。然后使用`Math.ceil()`函数对结果进行向上取整，确保不会有小数部分。最后再加上1000，结果的范围就变成了1000到10000之间的整数。 



### toFixed() 方法

> toFixed() 方法可把 Number 四舍五入为指定小数位数的数字。

```
//语法
NumberObject.toFixed(num)
```

| 参数 | 描述                                                         |
| ---- | ------------------------------------------------------------ |
| num  | 必需。规定小数的位数，是 0 ~ 20 之间的值，包括 0 和 20，有些实现可以支持更大的数值范围。如果省略了该参数，将用 0 代替。 |



### var与let的区别

> let是es6里面的声明变量

用var声明的变量会进行变量提升

```js
\\{
  let a=1;
  var b=2;
\\}
a//报错
b//2
```

使用let声明的变量不存在变量提升，作用域为块级作用域

```js
//使用let
for(let i=0;i<5;i++)\\{
    console.log(i); // 0 1 2 3 4
\\}

console.log(i)  //报错：i  is  not defined
//使用var
for(let i=0;i<5;i++)\\{
    console.log(i);//0 1 2 3 4
\\}
 console.log(i);//5
```

let不允许在相同作用域内，重复声明同一个变量,var声明的变量后面的会把前面的覆盖掉。

```js
\\{
    let num=10;
    let num=20;
    comsole.log(num);
    //报错 'num' has already been declared
\\}
```

常见问题：

```js
//使用var
for(vari=0;i<10;i++)\\{
    setTimeout(function()\\{
        //执行此代码时，同步代码for循环已经执行完成，结果为10
        console。log(i);
    \\}，0)
\\}

// 使用let
for(let i=0;i<10;i++)\\{
    setTimeout(function()  \\{
        //i是循环体内局部作用域，不受外界影响
        console.log(i);
    \\}, 0);
\\}
//输出结果
0 1 2 3 4 5 6 7 8 9
```



### 事件基础

#### 鼠标事件

| 事件          | 描述                                   |
| :------------ | :------------------------------------- |
| onclick       | 点击                                   |
| ondblclick    | 双击                                   |
| onmousedown   | 按下                                   |
| onmouseup     | 抬起                                   |
| onmousemove   | 移动                                   |
| onmouseover   | 移入                                   |
| onmouseout    | 移出                                   |
| onmouseenter  | 鼠标指针移动到元素上时触发(不支持冒泡) |
| onmouseleave  | 鼠标指针移出元素上时触发(不支持冒泡)   |
| oncontextmenu | 右键                                   |

#### 键盘事件

| 事件       | 描述                       |
| :--------- | :------------------------- |
| onkeydown  | 按下                       |
| onkeyup    | 抬起                       |
| onkeypress | 按下(只能触发数字字母符号) |

#### 表单事件

| 事件     | 描述                     |
| :------- | :----------------------- |
| onfocus  | 获得焦点                 |
| onblur   | 失去焦点                 |
| onchange | 失去焦点并内容改变       |
| onsubmit | 提交事件（form标签事件） |
| onreset  | 重置事件（form标签事件） |
| oninput  | 表单输入                 |

#### 其他事件

| 事件             | 描述                       |
| :--------------- | :------------------------- |
| onscroll         | 滚动条事件(滚动条位置改变) |
| onwheel          | 鼠标滚轮事件               |
| onresize         | 页面尺寸改变               |
| onload           | 页面加载完成之后执行该事件 |
| DOMContentLoaded | 页面结构加载完成执行该事件 |

### 事件高级

#### 绑定事件的方式

* 标签绑定事件

```js
<button onclick="click_fn()">click</button>
<script>
  function click_fn()\\{
    console.log(this);
  \\}
</script>
```

* ### Document对象来绑定事件

> 注意：重复监听某一事件，后者会覆盖前者，而不会两者先后触发

```js
<button>click</button>
<script>
    var button1 = document.querySelector('button')
    button1.onclick=function()\\{
        console.log("第一个点击事件的方法");
    \\}
    var button2 = document.querySelector('button')
    button2.onclick=function()\\{
        console.log("第二个点击事件的方法");
    \\}      //第二个点击事件的方法会覆盖第一个方法,所以点击只会触发第二次的点击事件方法     
</script>
```

* 事件监听

> 为一个事件添加多个事件处理程序，解决了上面两种方法不能添加多个方法 更精细的控制事件监听器的触发阶段

```js
dom元素.addEventListener(event,callback,bool);
//事件监听的语法  dom元素.addEventListener(event,callback,bool);
//参数 事件没有On  函数，  布尔类型
//布尔类型 true 捕获阶段， false  冒泡阶段。


//兼容性问题
标签.addEventListener("事件名称",function()\\{\\},false);    //兼容到IE9及其以上
标签.attachEvent("事件名称",function()\\{\\})    //  ie8及以下
//处理ie8兼容性问题
// $box.attachEvent('onclick',fun);       // 添加
// $box.detachEvent('onclick',fun);  	  //移除


//移除事件
dom元素.removeEventListener(event,callback,bool);

//例子
<button id="myBtn"></button>
<script type="text/javascript">
  var btn=document.getElementById('myBtn');
  function handle()\\{
    console.log(this);
  \\}
  //兼容到IE9及其以上
  btn.addEventListener('click',handle,false);      //添加事件处理程序
  btn.removeEventListener('click',handle,false);    //移除事件处理程序

  //  ie8及以下
  btn.attachEvent('onclick',handle);       // 添加
  btn.detachEvent('onclick',handle);       // 移除
</script>
```

#### 事件对象

> 在触发DOM上的某个事件时，会产生一个事件对象event，这个对象中包含着所有与事件有关的信息。所有浏览器都支持event对象，但支持方式不同。

```js
<div class="bos"></div>
<script>
    let $bos = document.querySelector(".bos")
    let $body = $bos.parentElement;
    console.log($body);
    $body.onclick=function(event)\\{
        //鼠标 距离浏览器窗口的横向距离和纵向距离
        // console.log(event.clientX);
        // console.log(event.clientY);
        //鼠标 距离事件源的位置  事件源输出事件源  事件源是body所有的元素
        console.log(event.target);
        console.log(event.offsetX);
        // console.log(event.offsetY);
        //当鼠标事件发生的时候，鼠标相对于浏览器X轴的位置，包含页面横向滚动距离
        // 当鼠标事件发生的时候，鼠标相对于浏览器X轴的位置，包含页面纵向滚动距离
        // console.log(event.pageX);
        // console.log(event.pageY);
    \\}
    // document.onkeydown=function(event)\\{
    //     console.log(event.ctrlKey);
    // \\}
</script>
```

* 兼容性写法

  

  ```js
  <div id="box" style="height:30px;width:200px;background:pink;"></div>
  <script>
  var oBox = document.getElementById('box');
  oBox.onclick = function(e)\\{
    e = e || event;
    box.innerHTML = e;
  \\}
  </script>
  ```

  

#### 事件对象常用的方法和属性

##### 鼠标事件相关

| 属性    | 含义                                                         |
| :------ | :----------------------------------------------------------- |
| clientX | 当鼠标事件发生的时候，鼠标相对于浏览器X轴的位置              |
| clientY | 当鼠标事件发生的时候，鼠标相对于浏览器Y轴的位置              |
| offsetX | 当鼠标事件发生的时候，鼠标相对于事件源X轴的位置              |
| offsetY | 当鼠标事件发生的时候，鼠标相对于事件源Y轴的位置              |
| pageX   | 当鼠标事件发生的时候，鼠标相对于浏览器X轴的位置，包含页面横向滚动距离 |
| pageY   | 当鼠标事件发生的时候，鼠标相对于浏览器X轴的位置，包含页面纵向滚动距离 |

##### 滚轮事件相关

| 属性       | 含义   |
| :--------- | :----- |
| wheelDelta | 滚动量 |

```
e.wheelDelta
上： 120  240
下：-120 -240
```

##### 键盘事件相关

| 属性     | 含义                          |
| :------- | :---------------------------- |
| key      | 获取当前所按键的名称          |
| keyCode  | 获取当前所按键的键盘码        |
| ctrlKey  | 判断当前ctrl键是否按下的状态  |
| shiftKey | 判断当前shift键是否按下的状态 |
| altKey   | 判断当前alt键是否按下的状态   |

##### 其他属性和方法

| 属性              | 含义                                                         |
| :---------------- | :----------------------------------------------------------- |
| preventDefault()  | 阻止浏览器默认行为                                           |
| stopPropagation() | 阻止事件流的传播                                             |
| currentTarget     | 指向被绑定事件的元素                                         |
| target            | 指向事件触发的对象，当事件是处在冒泡或者捕获阶段调用的时候，指向最先触发事件的事件源 |
| type              | 返回当前所触发事件的事件名称                                 |

#### 事件流

> 事件发生时会在元素节点与根节点之间按照特定的顺序传播，路径所经过的所有节点都会收到该事件，这个传播过程即DOM事件流。 事件传播的顺序对应浏览器的两种事件流模型：捕获型事件流和冒泡型事件流。

* 冒泡型事件流：事件的传播是从最特定的事件目标到最不特定的事件目标。
* 捕获型事件流：事件的传播是从最不特定的事件目标到最特定的事件目标。

##### DOM事件流

DOM标准规定事件流包括三个阶段：事件捕获阶段、处于目标阶段和事件冒泡阶段。
eventPhase属性返回一个整数值，表示事件目前所处的事件流阶段:0表示事件没有发生，1表示捕获阶段，2表示目标阶段，3表示冒泡阶段

- 事件捕获阶段：实际目标<div>``在捕获阶段不会接收事件。也就是在捕获阶段，事件从document到``再到`<html>`就停止了<body>。
- 处于目标阶段：事件在`<div>`上发生并处理。但是事件处理会被看成是冒泡阶段的一部分。
- 冒泡阶段：事件又传播回文档。
- 所有的事件都要经过捕获阶段和处于目标阶段，但是有些事件会跳过冒泡阶段：如，获得输入焦点的focus事件和失去输入焦点的blur事件。

##### 事件委派

> 事件委派的原理用到的就是事件冒泡和目标元素，把事件处理器添加到父元素，等待子元素事件冒泡，并且父元素能够通过target（IE为srcElement）判断是哪个子元素，从而做相应处理。 e.target获取到目标源

- 用法

1. 子元素的事件加到父元素上
2. 触发事件时判断 触发该事件的元素是什么（e.target）
   - 判断内容 innerHTML innerText
   - 标签名 nodeName (判断的时候，标签名需要大写)
   - 属性 e.target.hasAttribute("属性名"); 有则是true 无则是false
   - 类名 ID e.target.classList.contains("类名")； 有则是true 无则是false
3. 在判断成功中写对应的处理函数

- 应用场合

1. 需要给大量元素添加同一事件处理程序的时候，提高代码运行的效率
2. 在页面加载完成后新创建的元素， 比如通过ajax异步加载生成dom对象





## Ajax

* 为什么使用ajax

> 以前通过使用form表单来提交或者请求数据，由于表单必须是在response请求返回成功之后继续执行，那么在请求数据的同时用户是不能在页面进行操作的，所以2005年才正式被大众使用

* ajax是什么

> 一种用于创建快速动态网页的技术，在不刷新整个页面的情况下对页面的某一部分进行更新。

a------异步

j-------jacascript

a------and

x------xml(1、svg格式，2、存储数据)

* 作用有哪些
  * 发送数据：在不重新加载页面的情况下发送数据请求
  * 接收数据：接收并使用从服务器发来的数据

* 应用场景：增删改查，数据验证

* 步骤

  * 创建XMLHttpRequest()实例
  * 调用xhr.open() '方式' ‘地址 ’‘
  *  发送HTTP请求：调用xhr.send()   get发送 时在地址上
  *    **xhr.responseType="json |  text  |  xml"    设置响应数据的格式**
  * 监视 xhr.onreadystatechange
  * 判断是否与服务器响应成功 xhr.readystate==4
  * 响应成功数据是否成功  xhr.status
  * 更新网页数据

* 使用方式

  ```js
  <script>
    // 创建ajax  XMLHttpRequest实例化对象
    var  xhr=new XMLHttpRequest();
  // 告诉xhr去哪儿拿/怎么去，
  
  // 请求方式
  /* 
       1.get 获取数据     发送数据字符串的时候是将Url+date进行拼接
       2.put 修改数据
       3.delete 删除数据
  		 4.post 提交数据  直接调用对象
  		 5.options 等待
  		*/
  //  请求地址：没有服务器，可以使用json 数据来代替
  //xhr.open("请求方式"，"请求地址","同步false还是异步true")
  xhr.open('get','demo.json',true)
  // 出发/发送
  xhr.send();
  // 时刻监视数据动向
  xhr.onreadystatechange=()>=\\{
     /*  
     xhr.readyState 返回整数：
     0 send方法还没有调用
     1 send方法已经调用，正在发送请求
     2 send方法发送成功，已经接受响应内容
     3.正在解析内容
     4.响应完成，可以在客户端使用了
     */
    
    // 响应成功
    if(xhr.readyState == 4)\\{
      /*  
     xhr.status 返回状态码：
     200 表示成功
   	 304 代表有缓存文件
     401 代表未授权
     403 代表禁止访问
     404 代表未找到服务器
     500 服务器内部错误
    */
      if(xhr.status == 200)\\{
      //数据成功返回  
        document.write("大功告成")
      \\}else\\{
        //数据返回失败
        document.write("惨不忍睹")
      \\}
    \\}else\\{
    //正在请求数据
  \\}
  
  \\}
  </script>
  ```
  



* get 和 post的区别

  * 发送数据的方式不同：get携带在地址栏上，post实在调用的send方法的时候携带

  * 功能：get是从服务器上获取数据（查询），post是像服务器上传递数据（增加/提交）

  * 数据量：get的地址不可过长，ie浏览器对字节有限制2083字节，post传送的数据量大，不受限制

  * 安全性：get请求的数据会被缓存起来，可以在历史记录中读取，post相对安全性能高

    ```js
    //get 形式传参数
    xhr.open('get','./test.json?username=aa&password=123456',true)
    xhr.send()
    
    //post形式传参数
    xhr.post('post','./test.json',true);
    //post请求设置头信息
    xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded;charset=utf-8');
    xhr.send(传递的数据);
    ```

* 属性描述

  | 属性         | 描述                                           |
  | ------------ | ---------------------------------------------- |
  | response     | 响应返回的数据题，数据类型有responseType来决定 |
  | responseType | 该值能够改变响应数据类型                       |
  | responseText | 响应数据文本                                   |
  | responseXML  | 响应数据返回document对象                       |

* ajax其他方法

|    事件     |                 含义                 |
| :---------: | :----------------------------------: |
|   onabort   |      当发生中止事件时触发的事件      |
|   onerror   |      当发生加载错误是触发的事件      |
|   onload    | 当加载结束后触发的事件，不论成功与否 |
|  onloadend  |         加载结束后触发的事件         |
| onloadstart |        当加载开始时触发的事件        |
| onprogress  |      在加载过程中不断触发的事件      |
|  ontimeout  |         加载超时后执行的事件         |

* 实例化XMLHttpRequest()兼容性

  ```js
  var xhr = window.XMLHttpRequest?new XMLHttpRequest():new ActiveXObject("Miscrosoft.XMLHTTP")
  ```

## 跨域

* 同源

> 源是指协议、域名、端口，若地址里面的协议、域名、端口号均相同则属于同源，三者有一个不同则代表着不同源

* 同源策略

> 同源策略是浏览器的一个安全功能，不同源的客户端脚本在没有明确授权的情况下，不能读写对方的资源
>
> 

* 跨域的解决方式
  * jsonp
  * 第三方代理、例如nginx
  * 后台设置允许跨域



```js
图片改变时显示当前图片
function filechange(c)\\{
  var fr = new FileReader(); //创建NEW  FileRaader()对象
  var imgobj=c.files[0]; //获取图片
  fr.readAsDataURL(imgobj);//将图片读取为DataURL
  fr.onload=function()\\{
    $("editDialog img")[0].src=this.result;
  \\}
\\}
```

![image-20201014174826954](C:\Users\a\AppData\Roaming\Typora\typora-user-images\image-20201014174826954.png)

![image-20201014174841351](C:\Users\a\AppData\Roaming\Typora\typora-user-images\image-20201014174841351.png)



### history 对象详解

　　我们浏览一个网页时可能不太会注意网页前进后退这些操作，但是在开发时你是否想过页面之间的跳转经历了什么，浏览器时怎么保存的页面信息，重新返回上一个页面的时候是否需要重新加载页面呢，会有很对疑问，要想解决这些问题，首先需要知道浏览器中的window下的history对象，本文来详细总结一下该对象的相关知识点。

　　history 对象表示当前窗口首次使用以来用户的导航历史记录。因为 history 是 window 的属性，所以每个 window 都有自己的 history 对象。出于安全考虑，这个对象不会暴露用户访问过的 URL，但可以通过它在不知道实际 URL 的情况下前进和后退。

#### 　　1、路由导航

　　history.go() 方法可以在用户历史记录中沿任何方向导航，可以前进也可以后退。这个方法只接收一个参数，这个参数可以是一个整数，表示前进或后退多少步。

```
        history.go(-1);// 后退一页
        history.go(1);// 前进一页
        history.go(2);// 前进两页
        // go() 有两个简写方法： back() 和 forward() 。
        history.back();// 后退一页
        history.forward();// 前进一页
```

　　history 对象还有一个 length 属性，history.length == 1表示这是用户窗口中的第一个页面

　　histroy的go方法，back方法、forword方法以及用户在浏览器手动的前进后退按钮都会导致页面刷新后跳转。

#### 　　2、历史状态管理API

##### 　　（1）hashchange 事件

　　hashchange：history 对象的一个新特性是hashchange，会在页面 URL 的散列变化时被触发，开发者可以在此时执行某些操作。当URL的片段标识符更改时，将触发hashchange事件 (跟在＃符号后面的URL部分，包括＃符号)。而状态管理API 则可以让开发者改变浏览器 URL 而不会加载新页面。比如：pushState和replaceState方法，页面并不会刷新，但是路由会发生改变。

##### 　　（2）popstate 事件

　　当活动历史记录条目更改时，将触发popstate事件。如果被激活的历史记录条目是通过对history.pushState（）的调用创建的，或者受到对history.replaceState（）的调用的影响，popstate事件的state属性包含历史条目的状态对象的副本。需要注意的是调用history.pushState()或history.replaceState()不会触发popstate事件。只有在做出浏览器动作时，才会触发该事件，如用户点击浏览器的回退按钮（或者在Javascript代码中调用history.back()或者history.forward()方法）

##### 　　（3）history.pushState() 方法

　　pushState() 方法向当前浏览器会话的历史堆栈中添加一个状态（state）。这个方法接收 3 个参数：一个 state 对象、一个新状态的标题和一个（可选的）相对 URL。pushState() 方法执行后，状态信息就会被推到历史记录中，浏览器地址栏也会改变以反映新的相对 URL。URL栏显示新地址, 但是不会加载 页面，甚至不会检查页面是否存在，该方法会增加history.length

##### 　　（4）history.replaceState()方法

　　replaceState()方法修改当前历史记录实体。这个方法接收 3 个参数：一个 state 对象、一个新状态的标题和一个（可选的）相对 URL。replaceState() 方法执行后，将会更新当前的state对象或者当前历史实体的URL来响应用户的的动作,URL栏显示新地址, 但是不会加载 页面，甚至不会检查页面是否存在。该方法不会增加history.length。

```
<body>
  <button onclick="handleNext()">点我到下一页</button><br>
  <button onclick="handleLast()">点我到上一页</button><br>
  <script>
    window.onload = function () \\{
      console.log(window.history);
    \\}
    window.addEventListener('hashchange', function () \\{
      console.log('The hash has changed!')
    \\}, false);
    window.addEventListener('popstate', (event) => \\{
      console.log("location: " + document.location + ", state: " + JSON.stringify(event.state));
    \\});
    function handleNext() \\{
      const state = \\{ userId: "1234", page: "2" \\}
      const title = '二'
      const url = 'page2.html'
      window.history.pushState(state, title, url)
      console.log(window.history);
    \\}
    function handleLast() \\{
      const state = \\{ userId: "1234", page: "21" \\}
      const title = '一'
      const url = 'page21.html'
      window.history.replaceState(state, title, url)
      console.log(window.history);
    \\}
  </script>
</body>
```

运行结果如下：![img](https://img2020.cnblogs.com/blog/2182006/202111/2182006-20211105143256472-772445952.gif)

#### 　　3、补充：URL的hash

　　URL的hash也就是锚点(#), 本质上是改变window.location的href属性，我们可以通过直接赋值location.hash来改变href, 但是页面不发生刷新,如下图所示：

![img](https://img2020.cnblogs.com/blog/2182006/202111/2182006-20211105143430810-61225220.gif)

https://www.cnblogs.com/zaishiyu/p/15513220.html



### 兼容性问题

* `document.body`与`document.docunmentElement`

```JS
//例如
document.body.scrollTop=document.documentElement.scrollTop=0;
```

```js
//兼容到IE9及其以上
  btn.addEventListener('click',handle,false);      //添加事件处理程序
  btn.removeEventListener('click',handle,false);    //移除事件处理程序

//  ie8及以下
btn.attachEvent('onclick',handle);       // 添加
btn.detachEvent('onclick',handle);       // 移除
```

* 实例化XMLHttpRequest()兼容性

  ```js
  var xhr = window.XMLHttpRequest?new XMLHttpRequest():new ActiveXObject("Miscrosoft.XMLHTTP")
  ```



cdn.js在线地址

- [http://www.bootcdn.cn/jquery/](http://www.bootcdn.cn/jquery/)

- https://code.jquery.com/

- http://cdn.code.baidu.com/




console.log('距离顶部高度',this.$refs.view.getBoundingClientRect().top);