---
title: RequireJS
date: 2019-10-28 19:45:42
categories: 
- 前端知识
tags:
- RequireJS
- 模块化
- AMD规范
---

RequireJS是一个JavaScript文件和模块加载器，可视为模块管理工具。



### 为什么使用RequireJS呢？

- 有效防止命名冲突
- 声明不同JS文件之间的依赖
- JS代码以模块化的方式组织

RequireJS为帮助解决前端代码库的组织难题，提供了两种解决思路：

- 模块化组织JS文件
- 异步加载JS文件



### 你用过 require.js 吗？它有什么特性？

（1）实现 js 文件的异步加载，避免网页失去响应；
（2）管理模块之间的依赖性，便于代码的编写和维护。



### requireJS 的核心原理是什么？（如何动态加载的？如何避免多次加载的？如何 缓存的？）

核心是 js 的加载模块，**通过正则匹配模块以及模块的依赖关系**，保证文件加载的先后顺序，根据文件的路径对加载过的文件做了缓存



### 让你自己设计实现一个 requireJS，你会怎么做？

核心是实现 js 的加载模块，维护 js 的依赖关系，控制好文件加载的先后顺序







## JavaScript模块化编程

JavaScript模块化编程目的是为了让开发者仅需实现核心的业务逻辑，其他都加载他人已写好的模块。但是JavaScript并不是一种模块化的编程语言，虽然ECMAScript6中间正式支持类和模块。但对于之前的版本实际上是不支持类（class），也就更不用说模块（module）。

什么是模块呢？模块是实现特定功能的一组方法。



### 模块的原始写法

将不同函数以及记录状态的变量放在一起，算是一个模块。

```javascript
function fn1()\\{...\\}
function fn2()\\{...\\}
```

缺点：污染全局变量，无法保证与其他模块发生变量命名冲突，而且模块成员之间看不出直接关系。



### 模块的对象写法

将模块定义为一个对象，所有模块成员都放在对象里面。

```jsx
//将属性和操作都封装在对象中
var module = new Object(\\{
  _prop:0,
  fn1:function()\\{...\\},
  fn2:function()\\{...\\}
\\});
// 使用时直接调用对象的属性
module.fn1();
```

缺点：暴露了模块成员，内部状态可被外部改写。

```cpp
module._prop = 100;
```



### 立即执行函数写法

立即执行函数（IIFE, Immediately-Invoked Function Expression）可达到不暴露私有成员的目的。

```jsx
var module = (function()\\{
  var _prop = 0;
  var fn1 = function()\\{...\\};
  var fn2 = function()\\{...\\};
  return \\{fn1:fn1, fn2:fn2\\};
\\})();
```



### 放大模式

如果一个模块很大，必须分成几个部分，或者是一个模块需要继承另一个模块，此时就有必要采用放大模式（augmentation）。

```jsx
var module = (function(mod)\\{
  mod.fn = function()\\{...\\};
  return mod;
\\})(module);
```



### 宽放大模式

浏览器环境中模块各部分通常是从网上获取的，有时不知道那个部分会首先加载。采用放大模式，第一个执行的部分可能加载一个不存在的空对象，此时需采用“宽放大模式（Loose Augmentation）”。

```javascript
var module = (function(mod)\\{
  mod.fn = function()\\{...\\};
  return mod;
\\})(window.module || \\{\\});
```



### 输入全局变量

独立性是模块的重要特点，模块内部最好不要与程序其他部分直接交互。为了在模块内调用全局变量，必须显式地将其他变量输入模块。

```jsx
var module = (function($)\\{
  
\\})(jQuery);
```







## AMD规范

为什么模块很重要呢？如何规范地使用模块呢？

因为有了模块就可很方便地使用别人的代码，想要什么样的功能就可加载什么模块。不过前提是大家必须以同样的方式编写模块。而JS模块目前还没有官方规范，通行的JS模块规范有2种方式：CommonJS和AMD。



### CommonJS

老实说在浏览器环境下，没有模块并不是特别大的问题，毕竟网页程序的复杂性有限。但对于服务端，一定要有模块，与操作系统和其他应用程序交互，否则根本无法编程。

2009年，美国程序员Ryan Dahl创建了NodeJS项目，将JS用于服务端编程。由此标志着JS模块化编程的正式诞生。

NodeJS的模块系统是参照CommonJS规范实现的，在CommonJS中有一个全局方法`require()`，用于加载模块。

```csharp
var math = require("math");
math.add(1, 2);
```

自从有了JS服务端模块以后，对于客户端模块，如何做到兼容，使得一个模块不用修改就可以在服务端和客户端浏览器上都能运行呢？由于一个重大的局限，使得CommonJS规范不适用于浏览器环境。问题是对于服务器而言模块都放在本地，可同步加载等待时间只是硬盘读取时间。但是当浏览器中使用服务端的模块时，等待时间取决于网速快慢，长时间的等待会造成浏览器处于“假死”状态。

因此浏览器端的模块不能采用“同步加载（synchronous）”，只能采用“异步加载（asynchronous）”方式，这就是AMD规范诞生的背景。



### AMD

AMD(Asynchronous Module Definition)异步模块加载，模块加载不影响后续语句的执行。所有依赖于模块的语句都定义在一个回调函数中，等到加载完成后，回调函数才会执行。

AMD也采用了`require()`语句加载模块，不同于CommonJS的是，它要求两个参数。

```jsx
// module参数为一个数组，里面的成员是要加载的模块
// callback参数是模块加载成功后执行的回调函数
require([module], callback)

// math模块与math.add()加载不是同步的，浏览器不会发生假死，因此AMD比较适合浏览器环境。
require(["math"], function(math)\\{
  math.add(1, 2);
\\});
```







## RequireJS

早期JS代码都会写在一个文件中，仅需加载一个文件即可。后来代码越来越多，必须分割成多个文件，依次加载。问题是这种加载的方式，浏览器会停止页面渲染，加载文件越多，网页失去响应的时间越长。另外JS文件之间存在依赖关系，必须严格保证加载顺序。当依赖关系非常复杂的时候，代码的编写和维护变得异常困难。

RequireJS的诞生是为了解决这两个问题：

- 实现JS文件的异步加载避免页面失去响应
- 管理模块之间的依赖关系，便于代码编写和维护。



### 加载资源文件

```html
<script src="https://cdn.bootcss.com/require.js/2.3.5/require.js"></script>
```

在引入`require.js`文件之后，整个`windows`对象就有`require()`方法。可通过`require()`方法来加载其他JS文件。RequireJS的入口是引入时指定的`data-main`属性，在RequireJS引入后，会自动执行指向`data-main`属性所指定的入口文件。`data-main="js/main"`表示让RequireJS去`js`目录下寻找`main.js`文件，默认`main.js`是项目全局配置文件。

由于引入RequireJS文件本身可能会造成页面失去响应，解决的方式可将其放在网页底部加载，或使用延迟加载。

```xml
<script src="./assets/scripts/require-2.3.5.js" data-main="js/main" async="true" defer></script>
```

`async="true"`的作用和jQuery中AJAX的`async=true`的目的一样，表示一边加载RequireJS一边执行它。如果设置为`false`则表示等待RequireJS完全加载完成后才执行，这种方式的缺陷是在网络延迟较大时页面会出现空白。如果`script`标签不再`head`中而在页面尾部，则不会出现空白现象。另外，IE并不支持`async`属性，仅支持`defer`属性。



### 主模块

`data-main`加载的是主模块，意思是页面的入口，类似C语言的`main()`函数，所有代码从此处开始运行。

RequireJS以一个相对于`baseUrl`的地址来加载所有代码，页面顶层``标签内含有一个特殊的属性`data-main`，RequireJS使用它来启动脚本加载过程，`baseUrl`一般设置到该属性相一致的目录。RequireJS目的是鼓励代码模块化，鼓励在使用脚本时以`module ID`替代 URL 地址。

```html
$ vim index.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>app</title>
</head>
<body>
    <script type="text/javascript" src="./js/require-2.3.5.js" data-main="js/main"></script>
</body>
</html>
```

`baseUrl`可通过`requirejs.config`手动设置，若没有显式指定`config`及`data-main`，则默认的`baseUrl`为包含RequireJS的那个HTML页面的所属目录。

```javascript
$ vim js/main.js
/**
 * RequireJS全局配置文件
 */
requirejs.config(\\{
    //设置项目路径，项目会以baseUrl作为相对路径去查找模块文件
    baseUrl:"./js",
    //预加载JS文件的配置项，默认可不用添加.js后缀
    paths:\\{
        //RequireJS默认假定所有的依赖资源都是JS脚本，因此无需再module ID上再加上js后缀。
        jquery:"../scripts/jquery-3.3.1"
    \\}
\\});
```

正常情况下，主模块是依赖于其他模块的，此时就要使用AMD规范定义的`require()`函数。

```jsx
require([module], function(module)\\{...\\});

/**
 * RequireJS全局配置文件
 */
requirejs.config(\\{
    //设置项目路径，项目会以baseUrl作为相对路径去查找模块文件
    baseUrl:"./js",
    //预加载JS文件的配置项，默认可不用添加.js后缀
    paths:\\{
        //RequireJS默认假定所有的依赖资源都是JS脚本，因此无需再module ID上再加上js后缀。
        jquery:"https://cdn.bootcss.com/jquery/3.3.1/jquery",
        bootstrap:"https://cdn.bootcss.com/bootstrap/4.1.1/js/bootstrap"
    \\}
\\});

requirejs(['jquery', 'bootstrap'],function($, undefined)\\{

\\});
```

RequireJS要求每个模块是一个的单独的JS文件，如果加载多个模块会发出多次HTTP请求，会影响页面的加载速度。

RequireJS加载的模块采用AMD规范，也就是说模块必须按照AMD的规定来书写。具体说来模块必须采用特定的`define()`函数来定义，如果一个模块不依赖其他模块，可直接定义在`define()`函数之中。

但是实际上，虽然部分流行的函数库符合AMD规范，但更多的库并不符合。RequireJS如何加载非规范的模块呢？在使用`require()`之前，需在`require.config()`函数中定义非规范模块的特征。

`require.config()`接收一个配置对象，此对象除了`paths`属性之外，还有一个`shim`属性，专门用来配置不兼容的模块。每个模块需要定义`exports`值即输出的变量名，表明这个模块外部调用名称。其次`deps`数组属性表明该模块的依赖性。



### RequireJS常用方法

- `requirejs.config()`
- `require()`
- `define()`







## RequireJS源码解析

### RequireJS工作流程

1. 载入模块
2. 通过模块名解析出模块信息并计算出URL
3. 通过创建`script`的形式将模块加载到页面
4. 判断被加载脚本若存在依赖则加载，若不存在则直接执行`factory()`。
5. 等待所有脚本都加载完毕后执行回调函数

```jsx
// 定义全局变量
var requirejs,require,define;
// 自执行函数
(function(global, setTimeout)\\{
  //...
\\})(this, (typeof setTimeout==='undefined'?undefined:setTimeout));
```



### RequireJS可分为三部分

1. 定义全局变量和帮助函数
2. 模块加载核心部分
3. 定义`require`和`define`方法以及项目入口