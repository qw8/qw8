---
title: JavaScript函数
date: 2020-04-05 21:10:40
categories: 
- 前端知识
tags:
- JavaScript
- 函数
---

### 内置函数(原生函数)

- String
- Number
- Boolean
- Object
- Function
- Array
- Date
- RegExp
- Error
- Symbol



### 简述创建函数的几种方式

```
//第一种（函数声明）：
function sum1(num1,num2)\\{
   return num1+num2;
\\}

//第二种（函数表达式）：
var sum2 = function(num1,num2)\\{
   return num1+num2;
\\}

//第三种（函数对象方式）：
var sum3 = new Function("num1","num2","return num1+num2");
```



### JavaScript 中，调用函数有哪几种方式？

* 方法调用模式          Foo.foo(arg1, arg2);
* 函数调用模式          foo(arg1, arg2);
* 构造器调用模式        (new Foo())(arg1, arg2);
* call/applay调用模式   Foo.foo.call(that, arg1, arg2);
* bind调用模式          Foo.foo.bind(that)(arg1, arg2)();



### 什么是函数节流？介绍一下应用场景和原理？


* 函数节流(throttle)是指阻止一个函数在很短时间间隔内连续调用。
  只有当上一次函数执行后达到规定的时间间隔，才能进行下一次调用。
  但要保证一个累计最小调用间隔（否则拖拽类的节流都将无连续效果）

* 函数节流用于 onresize, onscroll 等短时间内会多次触发的事件

* 函数节流的原理：使用定时器做时间节流。
  当触发一个事件时，先用 setTimout 让这个事件延迟一小段时间再执行。
  如果在这个时间间隔内又触发了事件，就 clearTimeout 原来的定时器，
  再 setTimeout 一个新的定时器重复以上流程。

* 函数节流简单实现：

```javascript
function throttle(method, context) \\{
     clearTimeout(methor.tId);
     method.tId = setTimeout(function()\\{
         method.call(context);
     \\}， 100); // 两次调用至少间隔 100ms
\\}
// 调用
window.onresize = function()\\{
    throttle(myFunc, window);
\\}
```



### setTimeout、setInterval和requestAnimationFrame；**（[参考链接](https://blog.csdn.net/qingyafan/article/details/52335753)）**（requestAnimationFrame）

**基本用法与区别**

**setTimeout**(code, millseconds) 用于延时执行参数指定的代码，如果在指定的延迟时间之前，你想取消这个执行，那么直接用clearTimeout(timeoutId)来清除任务，timeoutID 是 setTimeout 时返回的；

***setInterval***(code, millseconds)用于每隔一段时间执行指定的代码，永无停歇，除非你反悔了，想清除它，可以使用 clearInterval(intervalId)，这样从调用 clearInterval 开始，就不会在有重复执行的任务，intervalId 是 setInterval 时返回的；

**requestAnimationFrame**(code)，一般用于动画，与 setTimeout 方法类似，区别是 setTimeout 是用户指定的，而 requestAnimationFrame 是浏览器刷新频率决定的，一般遵循 W3C 标准，它在浏览器每次刷新页面之前执行。



### 分析 ['1', '2', '3'].map(parseInt) 答案是多少？

- 答案:[1, NaN, NaN]

* parseInt(string, radix) 第2个参数 radix 表示进制。省略 radix 或 radix = 0，则数字将以十进制解析，因为 parseInt 需要两个参数 (val, radix)，其中 radix 表示解析时用的基数。
* map 每次为 parseInt 传3个参数(elem, index, array)，其中 index 为数组索引
* 因此，map 遍历 ["1", "2", "3"]，相应 parseInt 接收参数如下

```
parseInt('1', 0);  // 1
parseInt('2', 1);  // NaN
parseInt('3', 2);  // NaN
```

-  所以，parseInt 参数 radix 不合法，导致返回值为 NaN解析失败。



### 使用构造函数的注意点

1 一般情况下构造函数的首字母需要大写，因为我们在看到一个函数首字母

大写的情况，就认定这是一个构造函数，需要跟new关键字进行搭配使用，创建一个新的

实例（对象）

2 构造函数在被调用的时候需要跟new关键字搭配使用。

3 在构造函数内部通过this+属性名的形式为实例添加一些属性和方法。

4 构造函数一般不需要返回值，如果有返回值

- 如果返回值是一个基本数据类型，那么调用构造函数，返回值仍旧是那么创建出来的对象。
- 如果返回值是一个复杂数据类型，那么调用构造函数的时候，返回值就是这个return之后的那个复杂数据类型。



### 定时器 setInterval 有一个有名函数 fn1，setInterval（fn1,500）与 setInterval（fn1(),500）有什么区别？

第一个是重复执行每 500 毫秒执行一次，后面一个只执行一次。



### Javascript 中，有一个函数，执行时对象查找时，永远不会去查找原型，这个函数是？

HasOwnProperty



### window.location.search() 返回的是什么？

查询(参数)部分。除了给动态语言赋值以外，我们同样可以给静态页面,并使用 javascript 来获得相信应的参数值
返回值：?ver=1.0&id=timlq 也就是问号后面的！



### window.location.hash  返回的是什么？

锚点 ，  返回值：#love ；



### apply/call/bind 自我实现

> `call/apply/bind` 日常编码中被开发者用来实现 “对象冒充”，也即 “显示绑定 `this`“。
>
> https://github.com/ZengLingYong/Blog/issues/30

面试题：“call/apply/bind源码实现”，事实上是对 JavaScript 基础知识的一个综合考核。

相关知识点：

1. 作用域；
2. this 指向；
3. 函数柯里化；
4. 原型与原型链；

### 思路初探

```
Function.prototype.myCall = function(context) \\{
    // 原型中 this 指向的是实例对象，所以这里指向 [Function: bar]
    console.log(this);  // [Function: bar]
    // 在传入的上下文对象中，创建一个属性，值指向方法 bar
    context.fn = this;  // foo.fn = [Function: bar]
    // 调用这个方法，此时调用者是 foo，this 指向 foo
    context.fn();
    // 执行后删除它，仅使用一次，避免该属性被其它地方使用（遍历）
    delete context.fn;
\\};

let foo = \\{
    value: 2
\\};

function bar() \\{
    console.log(this.value);
\\}
// bar 函数的声明等同于：var bar = new Function("console.log(this.value)");

bar.call(foo);   // 2;
```



### call 的源码实现

初步思路有个大概，剩下的就是完善代码。

```
// ES6 版本
Function.prototype.myCall = function(context, ...params) \\{
  // ES6 函数 Rest 参数，使其可指定一个对象，接收函数的剩余参数，合成数组
  if (typeof context === 'object') \\{
    context = context || window;
  \\} else \\{
    context = Object.create(null);
  \\}

  // 用 Symbol 来作属性 key 值，保持唯一性，避免冲突
  let fn = Symbol();
  context[fn] = this;
  // 将参数数组展开，作为多个参数传入
  const result = context[fn](...params);
  // 删除避免永久存在
  delete(context[fn]);
  // 函数可以有返回值
  return result;
\\}

// 测试
var mine = \\{
    name: '以乐之名'
\\}

var person = \\{
  name: '无名氏',
  sayHi: function(msg) \\{
    console.log('我的名字：' + this.name + '，', msg);
  \\}
\\}

person.sayHi.myCall(mine, '很高兴认识你！');
// 我的名字：以乐之名，很高兴认识你！
```

*知识点补充：*

1. ES6 新的原始数据类型 `Symbol`，表示独一无二的值;
2. `Object.create(null)` 创建一个空对象

```
// 创建一个空对象的方式

// eg.A
let emptyObj = \\{\\};

// eg.B
let emptyObj = new Object();

// eg.C
let emptyObj = Object.create(null);
```

使用 `Object.create(null)` 创建的空对象，不会受到原型链的干扰。原型链终端指向 `null`，不会有构造函数，也不会有 `toString`、 `hasOwnProperty`、`valueOf` 等属性，这些属性来自 `Object.prototype`。有原型链基础的伙伴们，应该都知道，所有普通对象的原型链都会指向 `Object.prototype`。

所以 `Object.create(null)` 创建的空对象比其它两种方式，更干净，不会有 `Object` 原型链上的属性。

ES5 版本：

1. 自行处理参数；
2. 自实现 `Symobo`

```
// ES5 版本

// 模拟Symbol
function getSymbol(obj) \\{
  var uniqAttr = '00' + Math.random();
  if (obj.hasOwnProperty(uniqAttr)) \\{
    // 如果已存在，则递归自调用函数
    arguments.callee(obj);
  \\} else \\{
    return uniqAttr;
  \\}
\\}

Function.prototype.myCall = function() \\{
  var args = arguments;
  if (!args.length) return;

  var context = [].shift.apply(args);
  context = context || window;

  var fn = getSymbol(context);
  context[fn] = this;

  // 无其它参数传入
  if (!arguments.length) \\{
    return context[fn];
  \\}

  var param = args[i];
  // 类型判断，不然 eval 运行会出错
  var paramType = typeof param;
  switch(paramType) \\{
    case 'string':
      param = '"' + param + '"'
    break;
    case 'object':
      param = JSON.stringify(param);
    break;
  \\}

  fnStr += i == args.length - 1 ? param : param + ',';

  // 借助 eval 执行
  var result = eval(fnStr);
  delete context[fn];
  return result;
\\}

// 测试
var mine = \\{
    name: '以乐之名'
\\}

var person = \\{
  name: '无名氏',
  sayHi: function(msg) \\{
    console.log('我的名字：' + this.name + '，', msg);
  \\}
\\}

person.sayHi.myCall(mine, '很高兴认识你！');
// 我的名字：以乐之名，很高兴认识！
```



### apply 的源码实现

`call` 的源码实现，那么 `apply` 就简单，两者只是传递参数方式不同而已。

```
Function.prototype.myApply = function(context, params) \\{
    // apply 与 call 的区别，第二个参数是数组，且不会有第三个参数
    if (typeof context === 'object') \\{
        context = context || window;
    \\} else \\{
        context = Object.create(null);
    \\}

    let fn = Symbol();
    context[fn] = this;
    const result context[fn](...params);
    delete context[fn];
    return result;
\\}
```



### bind 的源码实现

1. `bind` 与 `call/apply` 的区别就是返回的是一个待执行的函数，而不是函数的执行结果;
2. `bind` 返回的函数作为构造函数与 `new` 一起使用，绑定的 `this` 需要被忽略;

> 调用绑定函数时作为this参数传递给目标函数的值。如果使用new运算符构造绑定函数，则忽略该值。—— MDN

```
Function.prototype.bind = function(context, ...initArgs) \\{
    // bind 调用的方法一定要是一个函数
    if (typeof this !== 'function') \\{
      throw new TypeError('not a function');
    \\}
    let self = this;
    let F = function() \\{\\};
    F.prototype = this.prototype;
    let bound = function(...finnalyArgs) \\{
      // 将前后参数合并传入
      return self.call(this instanceof F ? this : context || this, ...initArgs, ...finnalyArgs);
    \\}
    bound.prototype = new F();
    return bound;
\\}
```

不少伙伴还会遇到这样的追问，不使用 `call/apply`，如何实现 `bind` ？

骚年先别慌，不用 `call/apply`，不就是相当于把 `call/apply` 换成对应的自我实现方法，算是偷懒取个巧吧。

本篇 `call/apply/bind` 源码实现，算是对之前文章系列知识点的一次加深巩固。

“心中有码，前路莫慌。”

参考文档：

- MDN - Function.prototype.bind()
- 不用call和apply方法模拟实现ES5的bind方法



![img](https://mmbiz.qpic.cn/mmbiz_jpg/5b4ibbmryfW6hzwffvRZAmfPOMlL6NKhjd9icIuYZk4UQUPzUAE0j9VNkWxAdreLhzNIjeFoI3WCm4q3xQwsvibBg/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

[参考链接](https://www.jianshu.com/p/56a9c2d11adc)



### JS中switch方法

JavaScript switch 语句是一种根据不同条件在代码中做出决策的方法。它比使用 if-else 语句更有条理、更简洁。switch 语句通过计算给定的表达式（可以是变量或值），并将其与几种可能的情况进行比较。如果表达式的值与其中一种情况匹配，则执行关联的代码块（一组指令）。如果未找到匹配项，则可以执行可选的默认情况作为后备，这意味着它会在其他情况都不适用时运行。

通过掌握 switch 语句，我们可以编写更干净、更高效、组织更好的 JavaScript 代码，最终提高我们的整体编程技能。

#### switch 基础介绍

switch 语句以关键字 switch 开头，后跟括号中的表达式。该表达式与包含在 switch 块中的一系列 case 标签进行比较。每个 case 标签代表一个不同的值，当表达式与 case 标签的值匹配时，执行 case 后面的代码块。语句break通常用于在执行匹配的 case 后退出 switch 块，确保仅运行预期的代码块，并防止跳到下一个 case。同时还可以包含默认情况，以便在没有任何情况标签与表达式匹配时提供后备操作，从而确保对未知值的响应。

使用语法：

```
switch(expression) \\{
    case \\{value1\\}:
    // 要执行的代码
    break
    case \\{value2\\}:
    // 要执行的代码
    break 
    default: 
    // 默认情况
\\}
```

#### case

判断条件，case的条件相当于===，即全等条件下才成立。

#### default

当没有其他情况与提供的表达式匹配时，将执行 switch 语句中的默认情况。它可以作为处理意外或未知值的后备措施，确保即使没有匹配的情况也能提供响应。

#### break

break关键字用在 switch 语句中，一旦找到并执行匹配的 case 就退出 switch 块。它阻止代码继续执行剩余的情况，确保只生成正确的输出。

一个 case 在 switch 语句中不能有多个条件。要在一种情况下合并多个条件，可以在case中省略break，从而允许代码执行继续到下一个 case，直到遇到下一个break或到达 switch 块的末尾。当多个条件共享相同的输出或操作时，这可能很有用。

```
switch (day) \\{
  case "Monday":
  case "Tuesday":
  case "Wednesday":
  case "Thursday":
  case "Friday":
    console.log("工作日");
    break;
  default:
    console.log("周末");
\\}
```

#### switch 与 if-else

当需要处理多个条件时，switch 语句是使用 if-else 语句的替代方法。虽然 if-else 语句适合检查一系列可以表示为 true 或 false 的条件，但 switch 语句在处理可以采用多个不同值的单个表达式时更有效。从本质上讲，当我们有多个相关条件需要管理时，switch 语句可以使我们的代码更干净、更有组织性并且更易于阅读。

例如，以下是一个 if-else 结构的例子：

```
if (color === "red") \\{
  console.log("The color is red");
\\} else if (color === "blue") \\{
  console.log("The color is blue");
\\} else if (color === "green") \\{
  console.log("The color is green");
\\} else \\{
  console.log("Unknown color");
\\}
```


使用switch语法：

```
switch (color) \\{
  case "red":
    console.log("The color is red");
    break;
  case "blue":
    console.log("The color is blue");
    break;
  case "green":
    console.log("The color is green");
    break;
  default:
    console.log("Unknown color");
\\}
```


在处理大量条件的情况下，switch 语句提供了一种更有组织性和可读性的方式来处理多个条件。在 switch 语句中，括号内的变量或值（在本例中为变量color）是需要计算的表达式。

#### 什么时候使用switch

- 大量单变量条件：当需要处理大量条件时，switch 语句通常比 if-else 链更有组织性且更易于阅读。
- 单变量评估：如果我们的条件是基于具有多个不同值的单个变量或表达式，则 switch 语句可以提供比 if-else 模式更高效、更清晰的结构。
- 更快的代码执行速度：在某些情况下，JavaScript 引擎可以优化 switch 语句，与一系列 if-else 语句相比，可以实现更快的代码执行速度。
- 更容易维护： switch 语句可以使添加、删除或修改条件变得更加容易，因为每个条件在 switch 块中都是独立的。相反，当需要更改时，if-else 链可能需要更广泛的修改。
- 默认回退： switch 语句提供可选的默认情况，当其他情况都不与给定表达式匹配时可以执行该默认情况。此功能允许以一种干净的方式处理意外或未知值。

#### 什么时候使用if-else

- 复杂条件：如果我们的条件涉及复杂逻辑、多个变量或关系和逻辑运算符，则 if-else 模式提供了更大的灵活性，并且比 switch 语句更适合这些情况。
- 基于范围的条件：当我们需要检查一系列非离散值或条件时，if-else 模式提供了更好的解决方案，因为 switch 语句是为比较离散值而设计的。
- 条件数量少：如果只有几个简单的条件需要检查，则使用 if-else 模式比 switch 语句更直接、更容易编写。
  非常量： switch 语句需要 case 标签为常量值，这意味着它们不能是在运行时更改的表达式。如果我们需要判断非常量值的条件，则 if-else 模式是合适的选择。
- 判断true或false值：当我们需要检查值是真值还是假值时，If-else 模式适用。switch 语句不是为这种类型的评估而设计的，并且需要更详细的代码才能完成相同的结果。
- 提前退出条件：如果我们有提前退出条件，一旦满足特定条件就不需要进一步判断，则 if-else 模式可能会更有效。使用 switch 语句，即使发现早期匹配，也会判断所有情况（除非我们使用了break语句）。

#### 常见问题

1.多个case执行（忘记使用该break语句）
使用 switch 语句时的一个常见错误是在每个 case 后面都没有包含break语句。此错误会导致执行所有的case.

2.不正确的比较值和类型
switch 语句使用严格比较，这在比较不同数据类型时可能会导致意外结果。在下面的示例中，字符串"2"不等于数字2。

```
const num = '2';
switch (num) \\{
  case 2:
    console.log(2);
    break;
  default:
    console.log('不是数字2');
\\}
// 输出 不是数字2
```

3.范围界定问题
switch 语句中的一个常见错误是声明了没有块作用域或不正确作用域的变量，导致它们在其他情况下可以访问，或者产生语法错误。

范围界定问题
switch 语句中的一个常见错误是声明了没有块作用域或不正确作用域的变量，导致它们在其他情况下可以访问，或者产生语法错误。

#### switch一般写法

不过本文的主角是 switch。大家都了解 switch 的写法一般来说是 switch 变量或表达式，case 常量。嗯，比如说，一个百分制成绩，90 及 90 分以上算优秀，80 及以上 90 以下算良好，60 及以上 80 以下算合格，60 以下为不合格，用 switch 大概会这么写：

```
function calcGrade(score) \\{
    const line = score / 10 | 0;
    switch (line) \\{
        case 10: case 9:
            return "优秀";
        case 8:
            return "良好";
        case 7: case 6:
            return "合格";
        default:
            return "不合格";
    \\}
\\}
```

 代码中 `score / 10 | 0` 和 `Math.floor(score / 10)` 是一样的效果，就是除以 10 取商的整数部分。

这段 switch 用得中规中矩，用取整的办法来避免使用一长串 if ... else 分支也算是取了巧。

但是现在规则改了，将合格和良好的分隔点从 80 分降到 75 分，该怎么办？

按上面取整的办法依然可以，不过这次除数不再是 10，而是 5。相应地，case 也多了很多：

- 18、19、20 是优秀
- 15、16、17 是良好
- 12、13、14 是合格
- 剩下的是不合格

写 9 个 case，真不如用 if ... else 算了。

#### switch简单写法

是吗？其实用 switch 也有简单一些的写法：

```
function calcGrade(score) \\{
    switch (true) \\{
        case score >= 90:
            return "优秀";
        case score >= 75:
            return "良好";
        case score >= 60:
            return "合格";
        default:
            return "不合格";
    \\}
\\}
```

是不是感觉有些奇怪？这完全不是习惯了的 switch 表达式 case 常量，而是正好相反，switch 常量 case 表达式！如果你拿这段程序去跑一下，会发现一点问题都没有。因为——**switch 和 case 是按 `===` 来匹配的**，它并不在乎是表达式还是常量，或者说，switch 和 case 后面都可以接表达式！

#### 个税计算

```
	var income = 10000; // 税前月薪
    var personSocialRatio = 0.105; // 个人社保比例
    var personFundRatio = 0.12; // 个人公积金比例
    var tax = 0 // 个税

    // 首次加载
    init()

    // 初始化
    function init() \\{
        taxCompute()
        console.log('个税', tax);
    \\}

/*  个税计算方法，先判断年收入等级：x =（【含税月收入】-个人月公积金 - 个人月社保）* 12
        ①x < 36000
        个税 =（【含税月收入】-个人月社保 - 个人月公积金 - 5000）* 12 * 3 \\%
        ②36000 < x < 144000
        个税 =（【含税月收入】-个人月社保 - 个人月公积金 - 5000）* 12 * 10 \\% -2520
        ③144000 < x < 300000
        个税 =（【含税月收入】-个人月社保 - 个人月公积金 - 5000）* 12 * 20 \\% -16920
        ④300000 < x < 420000
        个税 =（【含税月收入】-个人月社保 - 个人月公积金 - 5000）* 12 * 25 \\% -31920
        ⑤420000 < x < 660000
        个税 =（【含税月收入】-个人月社保 - 个人月公积金 - 5000）* 12 * 30 \\% -52920
        ⑥660000 < x < 960000
        个税 =（【含税月收入】-个人月社保 - 个人月公积金 - 5000）* 12 * 35 \\% -85920
        ⑥x > 960000
        个税 =（【含税月收入】-个人月社保 - 个人月公积金 - 5000）* 12 * 45 \\% -181920
    */
    function taxCompute(list) \\{
        // 月收入
        var month = income * (1 - personSocialRatio - personFundRatio)
        // 年收入
        var x = month * 12
        console.log(month, x);

        switch (true) \\{
            case x > 960000:
                console.log(7);
                tax = (month - 5000) * 12 * 0.45 - 181920
                break;
            case x > 660000:
                console.log(6);
                tax = (month - 5000) * 12 * 0.35 - 85920
                break;
            case x > 420000:
                console.log(5);
                tax = (month - 5000) * 12 * 0.30 - 52920
                break;
            case x > 300000:
                console.log(4);
                tax = (month - 5000) * 12 * 0.25 - 31920
                break;
            case x > 144000:
                console.log(3);
                tax = (month - 5000) * 12 * 0.20 - 16920
                break;
            case x > 36000:
                console.log(2);
                tax = (month - 5000) * 12 * 0.1 - 2520
                break;
            case x > 0:
                console.log(1);
                tax = (month - 5000) * 12 * 0.03
                break;
            default:
                break;
        \\}
    \\}
```