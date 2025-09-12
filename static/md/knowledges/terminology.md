---
title: 术语名词
date: 2021-10-28 15:55:55
categories: 
- 前端知识
tags:
- 名词
---

最近写了太多技术文章，今天想写一点简单的东西。当一个新人问：如何开始学前端？很多知乎人都会发这样的脑图：

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/c624a52c672b72b4b148d47c8f87f279.png)

新人表示很淦，并点上右上角的“关闭”。

个人也有很讨厌找学习资源的时候，老手总是给一些“大而全”但对新人极度不友好的答案，我知道发图的人可能真的想为了新人好，但是这种图除了增加焦虑，没有大多作用。

但是前端发明了那么多的“名词”，不去了解又会一头雾水。这篇文章就给大家盘一盘前端开发那些“名词”的由来。



### 万维网

让我们把时间倒回 1989 年。一个英国佬 Tim Berners-Lee

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/9d55bf0b6c368aaec8b5712f4bc9e579.jpeg)

发现他们实验室 CERN(European Organization for Nuclear Research)[1] 的资料越来越难管理了，资料很容易“丢失”，比如文件名忘了、或者维护这个文件的人走了，那么这些文件可能就永远“消失”在茫茫资料中了。

> 这个 CERN 实验室其实是研究物理的，并不是搞计算机的！但是当时各个地方的实验室都和这个实验室有合作，就难免要相互分享资料。当资料变得越发庞大的时候就很难管理了。另一个点是 CERN 的全名并不是英文名，而是法文：Conseil européen pour la recherche nucléaire

为此，Lee 提出 “Linked information systems” 的构想，并称为 **World Wide Web**，也即我们熟知的“万维网”。

两年后，在 1990 年，Lee 又发了第二个提案[2]。最后提出需要2个人在6个月内造出的万维网的想法。最后造出了第一个网站：http://info.cern.ch/。

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/e2123ec46de8ade7a2bbe81c69a82b4e.png)

从上面可以看到，一个简单的 Client-Server 架构已经出现了。把文件放到服务器上，在客户端上访问它。

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/33d76daa8a7332f3ce9db7a6cbe8f557.png)



### 构建页面骨架

对于学术论文，一般都是有专业格式的，如果只是纯文字展示，换谁也受不了呀。

所以，Lee 受 SGML(Standard Generalized Markup Language) 的启发创建了 **HTML(Hyper Text Markup Language)**。一般常用的标签有：h1~h6, div, header, body, main, footer, table, ul, li, button 等。

```javascript
<header>头</header>
<main>身</main>
<footer>脚</footer>
```

如果你简单尝试写一个 .html 出来，会发现 `` 和 `` 的效果是一样的。但是，为了代码更**语义化**，也即可以让后面的人能看得懂，一般在头部会使用 ``，如果是文章则用 `` 作代码块的区分。如果非要扛：我就喜欢用 div 行不行，那不用扛了，当然行！



### 美化页面

虽然标签可以做一些简单的样式，但是依然满足不了设计师的样式要求。

为了解决网页的样式问题，Lee 的同事 Håkon Wium Lie[3] 在 1994 年，起草并提出了 **CSS(Cascading Styling Sheet)**。一段简单的 CSS 就可以让页面丰富起来了：

```javascript
body \\{
  color: red;
\\}
```

很多人可能都知道 CSS 这个玩意，用得理所当然，但是你有没有想过，其实 XML 也可以用来表示样式的，比如在 Android 上就是这么做的。在那个时候， DSSSL[4] 和  FOSI[5] 也曾是浏览器样式的候选人，但是用这两玩意来写样式太麻烦了，所以最后才选择 CSS 作为浏览器的样式书写标准。

现在我们使用 CSS 已经是非常好用了，但在以前 CSS 的标准化之路是充满着坎坷的：

•当 CSS1.0 发布后，几乎没多少浏览器可以支持它。等支持 CSS1.0 的时候 CSS2.0 都已经被放出来了•CSS2.0 增加了更多的样式选择。CSS2.0 是在1997年提出来的，但是在升级为 3.0 的时候经历了大幅的打回、重改，重新提名。直到 2011年 CSS2.1 才作为标准发布出来•到了 CSS3.0，它不像 1.0 和 2.0 那样整个版本升级，而是将样式的升级模块化。现在，虽然我们用的还是 “CSS3.0”，但是其实某些模块已经可以算是 4.0

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/1cd7e3650f520b3cd4b512efb87bb3ae.png)



### CSS UI 库

写了很多次 CSS 后，前端工程师们发现，一些好看的 CSS 样式可以拿出来共享呀，比如我写好了一个按钮的样式：

```javascript
.btn \\{
  ...
\\}
```

然后，其它人只要复制这个 CSS 到他的项目里，然后在 HTML 用上 CSS 类名，就可以直接用上我写的效果啦。

```javascript
<button class="btn">我的按钮</button>
```

在这段时间里，各种 UI 小组件的 CSS 样式满天飞，比如今天出个按钮的，明天就出了个输入框的。市面上还曾出现过很多类似《XX个好看的UI组件》和《XXXX年最好看的Y个UI组件》的文章。

不久后，开发者就发现另一 个问题：组件样式之间的冲突，比如，按钮的样式影响了自定义按钮的样式。另一个大问题是，单看一个组件的样式挺好看的，但是如果一个网页用了4 5 个别人写好的 CSS 样式，就会显得非常不协调，没有统一感。兼容性也很差。

Twitter 的 Mark Otto 和 Jacob Thornton 也想过这个问题，所以他们开发了 **Bootstrap** UI 库：

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/155940849d5119096dbd2cefa9170b78.png)

```javascript
<div class="input-group mb-3">
  <span class="input-group-text" id="basic-addon1">@</span>
  <input type="text" class="form-control" placeholder="Username" aria-label="Username" aria-describedby="basic-addon1">
</div>
```

把常用的按钮、字体、输入框的一些样式都写好了，还提供示例代码。这个 UI 库发布了之后，几乎所有开发者用过了，毕竟 CSS 终于可以不用自己写了。

当时我的也用 Bootstrap 写过课堂作业，那真是爽啊，一行 CSS 都没写过。



### 响应式布局

2011年，苹果发布了那款经典的 iPhone4S，标志着智能手机真正成为人们不可或缺的一部分，而手机上访问的需求也同时增加了不少。

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/d95aa56f0ad03cd0419e6701883fe762.jpeg)

当年在手机上看网页，用户都要先进入页面，手动放大，点击对应链接再进入下一个网页，操作非常复杂，而且界面很丑陋。

另一个方面，随着手机进入人们的生活，手机上的 App 也像雨后春笋一样疯狂冒出。这时，程序员就想：就把网页做成 App 的样子不就好看了嘛。

那怎么判断用户用的是手机还是电脑呢？很简单：通过屏幕宽度来判断嘛，而 CSS 的 **media query（媒体查询）** 正好可以用来解决这个问题：

```javascript
/*屏幕宽度在 600px 以内时，背景色显示红色*/
@media only screen and (max-width: 600px) \\{
  body \\{
    background-color: red;
  \\}
\\}

/*大于 600它时，背景色显示白色*/
@media only screen and (min-width: 600px) \\{
  body \\{
    background-color: white;
  \\}
\\}
```

问题又来了：难道每个兼容样式都要写两遍？能不能只写一种样式就能兼容手机和电脑端呢？程序员们开始通过百分比，em，rem，优化布局等方式，使得屏幕变小后样式还是不会乱。

这种写 CSS 的思路就叫做 **响应式** 布局，兼容了手机和网页。

不过 **响应式** 也不是万能的。比如今天淘宝页面里的一些花里胡哨的样式就没法兼容手机端，所以现在的做法是做两套网页，电脑端做一套，手机端做一套。区别是：手机端的样式做得像 App 一些，而且功能不会太多，样式也不会很复杂，而且提供“从XX App”打开的按钮，向自家的 App 引流。电脑端更酷炫，功能更强大。毕竟现在应该没人在手机网页上购物吧？

如果你仔细看手机端的网页地址，都会以 m.xxxxx 开头，就表示网页只在手机上看的。



### JavaScript 将内容动起来

> 注意：上面的 HTML、CSS 都不属于编程语言，HTML 是标记语言，而 CSS 是样式表。

现在我们有 HTML 和 CSS 已经可以让页面变好看了，但是页面内容都是定死的。为了能让页面“动”起来，浏览器必须要引入一种编程语言。那就是 **JavaScript**。

当年，本来有人想把 Java 用作浏览器的编程语言的，但是搞 Java 的 Sun 公司说：没空理你。所以，网景公司 NetSpace 只好自研编程语言。本来新语言想叫作 LiveScript，但是觉得这个名字又平平无其，不能一炮而红。当时 Java 正如日中天，所以，为了做个标题党、蹭个热度，在 12 月发布的时候改名为 **JavaScript**，并引入了一些 Java 的特性，然而，令人没想到的是，这些特性将会成为前端工程师的噩梦。

JavaScript 除了做一些简单的业务逻辑，比如判断是男是女：

```javascript
if (you === 'male') \\{
  console.log('男男')
\\}
```

还会操作 HTML，但是 HTML 不是一段文本么？怎么操作呢？实际上当浏览器拿到 .html 文件后，会自动解析 HTML 文本，将其转为为 **DOM(Document Object Modal)**，将普通的文本转换为一棵树的结构。

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/816151e9b764baf1861c3d7d94997e28.png)

JS 只需操作 DOM 就可以修改 HTML 的布局和结构了。

```javascript
document.getDocumentById('hello').textContent = '我是帅哥' // 内容变成“我是帅哥”
```

**JavaScript** 是一个设计极其糟糕的语言，比如 `getMonth()` 时，如果现在是1 月，返回的则是 `0`，而 `getHours()` 又会准确返回当前的小时数。对于数组的操作又少得可怜，比如没有 `unique`, `findBy` 这些 API。

为了给 JavaScript 的设计擦屁股，一些工具库营运而生：

•jQuery: 提供很多操作 DOM 的 API•moment, dayjs：提供很多操作 Date 对象的 API•lodash：更多像是个工具库



### 服务端渲染

虽然 JS 能动态修改内容了，但是，在以前发异步请求是一件很麻烦的事情。

Java 程序员想到了一个办法：JSP。反正要访问服务端，不如在你访问的时候，我直接从数据库里把数据读出来，生成一个 HTML 给你不就好了嘛。这种技术就叫做 JSP。

代码语言：javascript

复制

```javascript
<\\%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"\\%>
<\\%@ page import="java.io.*,java.util.*" \\%>
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>菜鸟教程(runoob.com)</title>
</head>
<body>
<h2>HTTP 头部请求实例</h2>
<table width="100\\%" border="1" align="center">
<tr bgcolor="#949494">
<th>Header Name</th><th>Header Value(s)</th>
</tr>
<\\%
   Enumeration headerNames = request.getHeaderNames();
   while(headerNames.hasMoreElements()) \\{
      String paramName = (String)headerNames.nextElement();
      out.print("<tr><td>" + paramName + "</td>\n");
      String paramValue = request.getHeader(paramName);
      out.println("<td> " + paramValue + "</td></tr>\n");
   \\}
\\%>
</table>
</body>
</html>
```

被程序员一直喊为 “世界上最好的编程语言” PHP也沿用了这个思路。这类通过服务端动态生成 HTML 的方法就叫 

 **服务端渲染**。

但是这上面有两个问题：

1.如果 Java 里有报错的时候，页面会显示整个错误 Stack 给用户，体验非常不友好，而且一崩全崩

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/6b3e54c8fb0d5f091e54cb34cc621ecd.png)

1.高度耦合的代码非常不利于维护，比如，第一眼看上面的代码能看出个啥子哦2.一个工程师除了要处理服务端的逻辑、也要考虑样式要怎么写、页面逻辑，职责不明确

虽然上面的 JSP 和 PHP 流行过一段时间，但是程序员们为了分工更明确，都选择了前端程序员管页面开发、而后端程序员管服务端的开发。这种开发模式也被称作 **前后端分离**。

而前后端的重要沟通桥梁就是**异步请求**，也即大家现在经常说的 **Ajax请求**，但是在很久以前，异步请求还是一个实现上特别困难的事情。在那个时候发完请求，页面就不得不重新刷新一遍，用户体验非常差。



### JSONP

上面说到的问题在于：浏览器很难在不刷新页面的情况下，向服务器发异步请求来获取内容。

聪明的程序员就开始想：什么东西能发异步请求呢？然后他们发现如果直接创建一个 img 标签并写上 src 就会向服务器发一个 xxx.jpg 的异步请求了：

```javascript
<img src="xxx.jpg">
```

那么如果要发个异步的 Get 请求，可以这样搞呀：

1.偷偷摸摸地创建一个看不见的 img 标签2.把要访问的 url 放到 src 里

```javascript
function getData(url) \\{
  var imgEl = document.createElement('img') // 创建 img 标签

  imgEl.visibility = 'none' // 把 img 标签变成不可见

  imgEl.src = url

  document.appendChild(img) // 加在网页上，自动发送 Get 请求
\\}
```

但是上面这么又引出下面的问题：

1.不知道什么时候要清理新生成的 img2.请求发了就发了，响应后不知道怎么获取数据3.每次都要写 `imgEl.visibility = 'none' // 把 img 标签变成不可见` 这句话

为此，程序员再次想了很多办法。

首先，不再使用 img 标签，而使用 script 标签，就可以把第 3 步省略了。

第二步，在全局定义一个函数用于获取 users 信息：

```javascript
function getUsers(users) \\{
  console.log(users)
\\}
```

在写 url 的时候加一个参数上去：`https://www.baidu.com/users?callback=getUsers`。服务端从参数里读取到 getUsers，向浏览器返回 JS 脚本：

```javascript
getUsers(['Jack'. 'Mary'])
```

由于刚刚添加的标签是 script 标签，所以等服务器返回后，`getUsers(['Jack'. 'Mary'])` 就会被马上执行，最终就会将 `users` 打印出来。这种技术就叫做 **JSONP**，全称为 JSON with padding。

JSONP 另一个好处是可以实现跨域请求，因为 script 标签可以请求非同源策略的资源并获取返回的数据。但是这非常不安全，服务器很容易被一些恶意的 JS 代码给攻击了。



### Ajax

从上面看出来 JSONP 能用但是很不规范，程序员们非常想要一套完善的异步请求机制。

2004 年，Google 在开发 Gmail 和 Map 两个应用的时候，完善了异步请求的机制，并制定了一些标准。

2006年时， W3C 起草了第一份 XMLHttpRequest 的草案，然后不断完善，一直到最后一份草案则在 2016年 被提出，**XMLHttpRequest** 才成为正式的标准。我们经常所说的 Ajax 请求其实就是使用这个对象来发请求的。下面就是用这个对象发送请求的代码：

```javascript
// 生成请求对象
xmlhttp = new XMLHttpRequest();
// 监听请求的状态和返回
xmlhttp.onreadystatechange = function () \\{
  if (xmlhttp.readyState === 4) \\{
    if (xmlhttp.status === 200) \\{ // 200 = OK
      console.log('成功');
    \\} else \\{
      console.log('失败');
    \\}
  \\}
\\};
// 打开通道
xmlhttp.open('GET', url, true)
// 发送请求
xmlhttp.send(null);
```

**Ajax** 全名是 Asynchronous JavaScript[6] and XML[7]，它不是单单一门技术，而是多门技术的全集，所表求的是：在客户端创建异步应用的一系列技术。只不过核心其中一步就是发异步请求，而 XMLHttpRequest 正好可以帮助我们完成这项工作。



### Node.js

2009 年，前端另一大飓风席卷了全球。Ryan Dahl 编写了第一个最初版本的 Node.js，使得 JavaScript 除了可以在浏览器里运行，也可以在拥有 Node.js 平台的地方运行，比如自己电脑的终端里。

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/d8de1dd5e751be71d2d41bb05738febe.png)

JavaScript 终于不再是客户端语言，也可以做服务端的开发了。为了更方便做服务端的开发，TJ Holowaychuk 一个国外超级大佬，借鉴了 Ruby 社区的 Rack，开发了 Express.js，一个简易的 JS 服务器框架。

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/f896eecae3af973eeb919ab01f9bf3b0.png)

由于 Express.js 提供的功能太简单了，所以，很多开发者不断给这个框架开发各种各样的[中间件](https://cloud.tencent.com/product/tdmq?from_column=20065&from=20065)，使用者可以用这些中间件增强自己服务器的功能，比如 **body-parser, cookie-parser, passport** 等。

后来，TJ 觉得 Express.js 写得还是不够精简，本来想重构的，但是重构成本太大了，干脆再造一个轮子吧，这个轮子也就是我们熟悉的 Koa.js。

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/c18663262de077852d6c8d485de18570.png)

为了让 JS 更好地完成服务端开发的工作，前端开发人员把后端开发的一些工具都造了一遍：

•连接数据库：mysql, mysql2, mongodb•缓存：session, redis•ORM: TypeORM, sequelize•定时任务：node-schedule, cron•...



### Serverless

当很多人都开始用 Node.js 的时候，大家又发现一些问题：

1.写完代码，本地跑起来也挺好的，那怎么部署到服务器上呢？2.服务器要怎么买？HTTPS证书从哪里获取？Nginx是个啥？啊，好烦啊，我只想 `npm run start` 啊

作为前端程序员，平时搬砖就够累了，还要我配置服务器，一剑杀了我算了。

聪明的程序员发现，不管你写 Express.js 还是 Koa.js 不就是写响应函数么？

```javascript
app.get('/users', (req, res) => \\{
  res.send('我是帅哥')
\\})
```

那我把服务器、证书、域名这些东西都统统给你弄好，你就负责写相应函数和给钱不就很爽了么？这就是 [**Serverless**](https://cloud.tencent.com/product/serverless-catalog?from_column=20065&from=20065) 的由来。它的好处是不再操心服务器的配置、扩展等琐碎的事情，只需要写好响应函数就好了。而这种“响应函数”也被称为 [**云函数**](https://cloud.tencent.com/product/scf?from_column=20065&from=20065)，Amazon 称此为 **Lambda**。

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/519f3ed090dd59e4f7884b77581d193c.png)

这时候有人发现，我自己写好的一些服务，比如收发邮件、数据库的存取也可以作为一种服务对外提供，前端工程师只需要给钱，然后请求我提供的 API 接口就可以享受我的服务啦。这也是很多云厂商另一种收入来源：卖服务。

比如，常见的：语言翻译服务、手机短信发送服务、鉴黄师、图形识别等。



### 模块化

当工具变得越来越多，Web 应用体积也变得越来越大了。一个大项目里可能有成百上千个 JavaScript 文件，它们之间相互依赖，可怕的是当前没有工具可以告诉你到底哪个文件是最先被执行的。

文件的管理就成了一个大问题，所以以应用需要划分模块。

在 ES6 之前，社区制定了一些模块加载方案，最主要的有 **CommonJS** 和 **AMD** 两种。前者用于服务器，后者用于浏览器。

```javascript
const xxx = require('xxx')
```

ES6 在语言标准的层面上，实现了模块功能，而且实现得相当简单，完全可以取代 CommonJS 和 AMD 规范，成为浏览器和服务器通用的模块解决方案。ES6 模块的设计思想是尽量的静态化，使得编译时就能确定模块的依赖关系，以及输入和输出的变量。

```javascript
import xxx from 'xxx'

export default xxx
```

模块化思想的提出大大提高了 JS 程序员的幸福感，所有的 JS 文件都不再是同一层级，而可以分块管理了。对前端的工程化有着不可或缺的作用。



### 包管理工具

有的工程师发现，自己抽象出来的模块其实也可以放在社区让别人使用，比如发异步请求的 axios，工具库 lodash 等。这就需要一个中心仓库来存放这些库了，同时也需要一个包管理工具来管理包的发布、安装、升级等。

目前 **npm** 就是使用最多的包管理工具，当电脑里装了 Node.js 后，**npm** 也会一并装上。不过使用 npm 在国内下载时会很慢，一般推荐使用 **yarn** 这个包管理工具，速度更快。



### 工程化

模块拆分使得写代码时候爽了，但是如果把这些 JS 文件都引入到一个 HTML 上是不是太恐怖了？一个 HTML 里有 1000 个 script 标签，比内容还多也有点反人类了吧。CSS 文件同理。

为了解决这个问题，前端工程师提出了 bundle 这个概念——不管你的模块多乱，多分散，最终通过一个工具，直接转换为1 个 .js 文件。这样的工具就叫做打包工具。

在 2016 年，Grunt，一个 JavaScript Task Runner 被制作出来了，开发者可以编写自己的任务，然后流水线地执行。这已经有了工程化的雏形了。

但是 Grunt 的打包速度太慢了。工程师们受不了了，又造了一个 **Glup** 的打包工具，功能差不多，但是一个字快！

与此同时，另一只巨兽也在悄然进化——**Webpack**。

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/10a722e3b8e6e092873151ec42fde490.png)

**Webpack** 以其强大的功能、高灵活配置度的特性直接抢夺了 Glup 的市场，很多人都纷纷用起了 Webpack。

随着 Webpack 的功能不断增强，开发者的要求也不断提高，市面上充斥着大量的 Loader 和插件：

•热加载•代码混淆•代码压缩•精简代码、TreeShaking•loader: file-loader, css-loader, vue-loader•...

Webpack 的另一个问题是，不同环境需要不同的 Webpack 打包配置，导致 Webpack 的配置越来越繁琐，前端工程师除了平常写代码之外，还要负责维护 `webpack.config.js` 的配置项目。

而 **Parcel** 的出现正好打破了这一局面，使用 Parcel 就像使用 iPhone 一样，不用太多配置可以马上跑出小网页。但是，治本不治根，在大型项目面前，还是没办法解决繁琐配置的问题。所以，Webpack 依旧是占领市场的巨头。

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/f216bc99cfb7c84445841c1076c0ff26.jpeg)

使用 Webpack 的另一个问题是本地开发打包很慢，Webpack 一般先打包构建再启动开发服务器。而 Evan You 则想到另一个方法：先启动开发服务器，当代码执行到模块加载时再请求对应模块的文件。加快本地开发时的打包编译速度，然后造出了 **Vite**。目前 Vite 还是个新生儿，可以关注一波，看看以它以后会迸发出什么好玩的东西。

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/cbcce8db1eb350605e4f3ca74dbfe5ad.png)



### CSS 预处理器

CSS 让人诟病的一点是不够简洁，很多东西不能复用。比如：

```javascript
.container \\{ 
  background: red; /*背景为红色*/
\\}

.container .title \\{ 
  color: red; /*标题字体为红色*/
\\}
```

为什么不写成这样呢：

```javascript
.container \\{
  backtround: red; /*背景为红色*/
  .title \\{
    color: red; /*标题字体为红色*/
  \\}
\\}
```

遗憾的是，浏览器只认识 CSS，不认识上面这样的写法。程序员又开始思考了：其实我不用浏览器认识第二种写法，我只要把第二种写法在打包的时候转换成 CSS 不就行了嘛。有了打包工具的加成，这件事我觉得能成！所以，第二种高级写法被称为 **CSS 预处理器**，即这些写法要先被处理成 CSS，然后再以普通 CSS 使用。

于是，在 2007 年，**Sass** 诞生了，借鉴了 Ruby 社区的 Sass 语法，但是前端程序员比较傲娇：凭啥要跟你叫一个名，就叫为 Scss，不过一般叫法还是叫 Sass，因为 Scss 不会读，哈哈。

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/9933848d228476458a2ca34d4ef739fa.png)

后来在 2009 年，**Less** 被创造出来了，语法 Scss 差不多，没多大差别。

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/6ebc30397dbd04f2e70617a7281b8fb6.jpeg)

在 2010 年，又一个预处理器 **Stylus** 诞生了。

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/83507d22446d72182ec0e6a9555c0da6.png)

目前 Scss 和 Less 用的比较多，Stylus 名气比较小。新手不用担心，这三玩意语法都差不多，大同小异，会一个相当于3个都会了。



### 进击的 JavaScript

虽然 JavaScript 本来是一个设计非常糟糕的编程语言，但是 JS 它不是咸鱼，它也要努力成为世界上最好的编程语言！

JavaScript 总不能一成不变吧？但是也不能一下子就变天了吧？所以，需要有一个起草方案，审核方案，同意方案，变成规范的过程，这需要大量的人力和专家，那不如做一个 “JS爱好者协会”？**European Computer Manufacturers Association (ECMA)** 就是类似这样的组织，不过这个组织格局比“JS爱好者协会”的格局大多了，主要任务是是将 Computer System 标准化。

ECMA International 在 ECMA-262[8] 里规范了 JavaScript，可以认为 ECMAScript 就是标准的 JavaScript，所有浏览器都要支持标准的 JavaScript。这个 262 的标准规范从 1997 年开始提出了第 1 版。

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/31b06ca57905dca132dc754fe91a2bb3.png)

从上面可以看到，往后几年就是第 N 代的 ES 标准对应标准的 JavaScript 就是 ECMAScript 201(N-1)，比如我们最熟悉的 ES6 其实就是 ECMAScript 2015。而 ES6 对 JavaScript 一个大变革，后面的 ES7，ES8 新增的东西就很少了，所以现在 ES6 其实是 ES6+ 的一个泛指。

但是你有没有想过一个问题：虽然我用最新的语法做开发，但是用户用的可能还是老版本的浏览器呀，这要怎么办呢？

再次得益于自动化打包工具的兴起，我们可以在开发的时候用最新的语法，在打包生产代码时将新语法都转成旧语法就好了嘛。这种语法的转换听起来就很麻烦，不过，聪明的前端工程师已经帮各位大哥大嫂做好，那就是 **Babel**。

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/5369b1cb59b565ac5f718995ae2b7b77.png)

**Babel** 发展到了现在，除了做新旧语法的转换，还支持 JSX 语法的转换。



### TypeScript

虽然 ES6 新增的语法和 API 已经大幅提升前端程序员的幸福感了，但是 JavaScript 依然是个弱类型的语言：

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/d0c5946d24b587c7c779f3c2ac88ffae.jpeg)

类型不规范，同事两行泪。当不正确使用类型时：

那能不能强行给 JavaScript 加上类型呢？微软说：可以！由微软牵头，开发了 **TypeScript** 编程语言和 TypeScript 的编译器，前者其实是 JavaScript 的超集，只是多加了很多料；后者则是负责将 TypeScript 编译成 JavaScript。

> 注意：这里的 TypeScript -> JavaScript 是不能用 Babel 实现的，因为这一步是编译，而不是新旧语法的替换。TypeScript 不是新语法，是一门正经的编程语言，只不过可以被编译成 JavaScript。

有了 TypeScript，开发者终于享受到了强类型约束的福利了：

```javascript
const x: string = '123'
```

再再再一次得益于自动化打包工具人 Webpack，可以在输出生产代码时将 TypeScript 编译成 JavaScript，如果再加上 Babel，则能进一步转为某个时代的 ECMAScript。



### 单页应用

在打包工具不断厮杀的同时，单页应用框架也一并发展。

在以前，大部分都是一直在用 jQuery 直接操作 DOM 来更新页面。

每次操作 DOM 时就不得不写一些面条代码。但是这样很麻烦啊，操作 DOM 这一步能不能封装一下，数据更新时自动操作 DOM 去更新页面？

2010 年，Google 研发的 **Angular.js** 率先实现了 **MVVM** 想法，即开发者不再需要操作 DOM，可以直接拿数据渲染页面 Modal-View，而页面的变化，比如输入值改变，可以反过来改变数据内容。后来又研发了 Angular2，但是无论是 Angular.js 还是 Angular 本身都太复杂了，借鉴了非常多的后端设计，前端工程师上手难度非常巨大，最终并没有形成大潮流。

> 注意 Angular.js 和 Angular 是两个不同的东西！

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/6010408ba5076c450fe69b6076c57e35.png)

2013 年，一个新的前端框架诞生了——Facebook 的 React.js。React 可以说是一个非常纯净的 JS 框架，没有 Angular 繁琐的内容，开发者只需要关注单向数据流就可以上手撸页面了。最后 React.js 在前端社区流行了起来。

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/85a7c0240e136a6b5640032592a5fc11.png)

但是 React.js 也有自己的问题：由于 React.js 内容太过于纯净了，本身没有太多的功能，导致开发 React 应用时出现非常多的解决方案，但没有一个方案是最优的，各有各的优缺点。这也导致了 React 社区总是骂战不断、帮派林立、出现各式各样的鄙视链的局面。

比如，在写样式时你可以直接 import 样式文件：

```javascript
import 'xxx.css'

const xxx = <button className="xxx">xxx</button>
```

也可以用 CSS module

```javascript
import styles from 'xxx.css'

const xxx = <button className=\\{styles.xxx\\}>xxx</button>
```

也可以用 styled-component

```javascript
const Button = styled.a`
  color: white;
`

const xxx = <Button>xxx</Button>
```

但是偏偏有人说 styled-components 是高级人，别的都是垃圾，使用 CSS Module 的人就受不了了，说你天天引那么多库来干嘛？

另一个麻烦点是，单向数据流并不是所有人都喜欢的，人们开始怀念 Angular 的数据双向绑定了。

到了 2014 年，那个男人来了，他带着 **Vue.js** 来了！

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/86c283b7e2e5dba13748d0a195af9de8.jpeg)

Evan You 以前在 Google 和 Meteor 工作过。**Vue.js** 取了 Angular 和 React 的中间位置，以一种优雅、轻便的姿态登陆前端社区。保留了 Angular 的数据双向绑定，但是摒弃了 Angular 很多复杂的设计和 API，同时不像 React.js 那么纯净，开放很多方便的 API 给使用者爽爽。而且还基于 Webpack 开发了 vue-loader 用来解析 .vue 模板文件。这种 .vue 模板文件和 .html 非常相象，新人上手十分简单。

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/d3c32e0ee440b2085525a5fc80b70412.png)

同时，得益于 Vue 简洁好看的中文官方文档，Vue.js 在中国迅速抢占了小公司的市场。

但是由于 Vue.js 太容易上手了，所以经常被 React.js 社区的一些人觉得写 Vue.js 的人都是新手。而 Vue.js 的人又觉得写 React.js 的人天天折腾这么多“最佳实践”，简直是在浪费生命，而且 JSX 的语法太丑了，不如我的 template 语法简洁好懂。直到现在，Vue 和 React 社区时不时就会爆发小规模的骂战。

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/41f9f48cfcfbe96fc6d21116aed860c1.png)

另一个问题出现了：原来的 UI 库仅仅提供了简单的 CSS 和原生的 JS，这些 JS 放到单页应用里显得有点冗余了，有的还会报错，因为大多数都是 DOM 的操作。所以 UI 库必须要配合对应的 SPA 框架进行升级。在别的 UI 库升级的同时，饿了么针对 Vue.js 开发 Element UI，而蚂蚁金服则针对 React 开发了 Antd。随后，更多的 UI 库再次涌现，比如 iView、Ant Design for Vue, Ant Design for Angular 等。

总得来说，Angular, React.js, Vue.js 都开发了自己的一套单页应用框架，这套框架最后要做的就是 SPA(Single Page Application) 单页应用。即所有的逻辑都打包在 JavaScript 文件里了，对外，只会看到一个 .html，一个 .css 和一个 .js 文件。

等一下？一个 .html 文件？那不同页面怎么做跳转呢？这就是前端路由的由来了。



#### 前端路由

不妨想想以前是怎么做路由的：用户页是 user.html，首页是 index.html，一个 url 对应着一个文件，也就说我们每次键入 url 时，实际上是访问某个 .html。

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/18810ca08c84e3c16517902ba1fb9010.png)

而浏览器里有一个监听浏览器地址改变的功能，单页应用的开发者就想了：我只要监听地址 url 的变化，再用 JS 渲染对应的页面组件，不就可以实现前端控制路由了么？这就是前端路由的基本思想。

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/70332ccc4dbb79b3adaf785f2c9ee76b.png)

上面的三大单页应用框架都有自己的前端路由框架：**@angular/router, react-router, vue-router**。

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/a0e29cee63b5d94cfeda163820c47e52.png)



#### 数据管理

单页应用框架另一个问题就是数据的管理，子组件访问的数据都只能靠父组件传过来，如果一个在很深的子组件想要最外层组件的数据时，就不得不把数据从头一路传到尾。

为了应对这种数据很难共享的问题，程序员就想：我把数据都存到一个公共的地方不就行了嘛？要的时候随便拿。

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/ea4d9aee11a0bfbbab8d704cff41bf42.png)

那公共地方是哪里呢？存全局变量？不行啊，会被别人覆盖啊，而且数据改了之后视图不能随之改变呀。所以，工程师又开发一些全局数据管理库：**mobx, vuex, redux。**

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/41241d492ca57d29612e87c050cfdfd8.jpeg)



### 同构渲染

用多了单页框架之后，程序员们又发现问题了，单页最后生成的 HTML 是这样的：

```javascript
<body>
  <div id="root"></div>
  <script src="bundle.js"></script>
</body>
```

要知道搜索引擎每天都会用**网络爬虫**抓取成千上万个网页，分析 HTML 里的内容，以此来提高搜索准确性，这种做法做叫 SEO(Search engine optimization) 搜索引擎优化。但是你看上面这样的结构，搜索引擎根本不知道你这个网页是用来干嘛的。另一个问题是，如果用户网络环境很差，那只要 JS 还没被加载出来，网页永远是一片白色，这非常影响用户体验。这要怎么解决呢？

大家开始怀念当时 JSP、PHP 服务端渲染 HTML 的时候了，因为服务端渲染 HTML 可以马上返回 HTML 结构，页面会先展示一些内容，不至于白屏，而且有了大概的 HTML 结构，搜索引擎更容易做 SEO。

前端工程师想到了：对于一些静态内容，比如商品种类、导航栏内容，其实可以在生成 HTML 的时候就加上，不需要再通过 API 获取了。这样的技术就叫做 SSG(Static Site Generation)。那动态的内容，比如朋友圈列表怎么做呢？初始展示的数据可以先通过服务端先渲染，等用户与页面发生交互，比如点击按钮后再发请求获取数据。这就是 **同构渲染**。

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/908abb3695329c0c1b09136587593379.png)

与传统的服务端渲染不同，同构渲染的服务端也使用 JavaScript 来编写，这样一来前后端都使用上了 JavaScript 了。

同构渲染简单来说就是一份代码，服务端先通过服务端渲染(server-side rendering)，生成html以及初始化数据，客户端拿到代码和初始化数据后，通过对 html 的 dom 进行 patch 和事件绑定对 Dom 进行客户端激活(client-side hydration)。

这个整体的过程叫同构渲染。既可以吸取服务端的优点，比如加速首屏渲染，又保留了 SPA 应用的特点，比如前端控制路由跳转，使得跳转时不需要再渲染新 HTML。



### Single-SPA

当越来越多项目用上了 SPA 框架后，当公司要把多个项目合并成一个项目的时候，这就很麻烦了，不同项目可能用的框架都不一样，比如用户详情用的是 Vue.js，而首页用的是 React.js，怎么把这两者结合呢？

**single-spa** 和国内阿里开发的**乾坤**就是解决这种问题的。本质上相当于造一个更大的“单页的应用”，这个“单页应用”里又会有多个单页的应用。

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/782de91bef50204600af7a28e9f8e68a.png)

这种将多个 SPA 整合成一个大 Project 的技术就是 **微前端**。



### 自动化测试

随着前端越来越工程化，自动化测试是比不可少的一件事。当造好一些轮子后，就需要接入自动化测试，不然每次修改都要做点点点的人工测试。

最简单的莫过于单元测试，目前单测常用的库有 ***ava, jest, moch, sinon, chai** 等。而前端又是一个非常依赖环境的工种，经常要用到不同的环境，比如 JSX 环境、浏览器环境，Vue 环境。又催生出很多提供 Mock 环境的库，比如 **enzyme** 就是用来提供 React 环境的。

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/612edada3869ed46f346ec72420082d3.png)

同时，为了模拟一些特定的场景，前端还要 Mock 一些东西，比如 localStorage, indexedDB, cookie 等。这些都有不同的库和工具来实现，比如 mock-axios, mock-redux, mock-cookie 等。

上面的只是属于白盒测试的做法，前端能不能直接模拟人工做点点点的操作呢？可以的，这就叫**端对端测试**、或者叫 **e2e 测试**，或者叫集成测试。现在比较火的工具是 **cypress** 和 **nightwatch**。

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/765e9dd968ff611cdd4b79074b47074f.png)

不过对于业务经常频繁改动的项目，自动化测试并不是一件好事，改动频繁的业务带来的是变化无常的测试用例。写太多的测试代码，有时候变得事倍功半。



### 手机H5

随着智能手机发展得越来越快，微信等一些应用里都不得不内嵌一些前端的 H5 页面，比如微信公众号文章，其实就是一个小型网页。

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/aa06ea432b78c0eb0cab0571d136d484.jpeg)

另一个应用场景是，工程师们发现 App 里也可以嵌入 H5 来做简单的展示和交互，这样一来移动端就可以少开发一些内容了。这种内嵌H5页面的应用开发也称为**混合开发**，开发出来的 App 就是 **Hybird App**.

现在我们手机上的支付宝、微信、QQ 等都是采用了混合开发的模式，既能使用原生的代码保证流畅度，同时又可以内嵌H5提升开发速度（注意，速度不等于效率）。



### 低代码

手机上的 H5 写多了之后，前端工程师们又发现很多 H5 都千篇一律，很多都是模板一套，再改个颜色就OK了。

因此，聪明的程序员就想到了能不能用拖拽就生成网页呢？其实拖拽生成网页并不是什么新鲜事，也不难实现，早在 wordpress 的时代已经出现拖拽生成个人博客的工具了。只不过现在用到手机上了。

但是拖拽的问题在于不灵活，有时候非常死板。有些运营人员还是懂一点代码的。所以拖拽工具再度进化成了：可以给别人留个入口做一些简单的自定义事情。这种模板+简单代码做开发的就称为**“低代码”开发**，通过简单的配置就能自动生成页面。



### 需求生成代码

除了拖拽，有没有更高级的生成代码工具呢？有！比如，用文字描述场景来生成前端代码，这也是阿里正在做的事情，它们正在研究 P2C （PRD to Code）。个人觉得这是一件好事，对于简单需求来说可以直接生成比什么都快。

![img](https://ask.qcloudimg.com/http-save/yehe-1045939/77b489809adbe660d8095a1abf5b38e7.png)

有人会担心：这会不会取代前端工程师呢？答案是不可能，也不科学。再厉害的人工智能最终也无法实现设计复杂、灵活多变、千奇百怪、疯狂迭代的产品需求。最终取代的是只会写简单 html、css 的低级工程师。



### 最后

不知不觉就写好了多东西，可见前端东西真的很多很杂。其实再下写去还能再细写下去，但是文章实在太长了，到此结束了。

这篇文章除了带大家了解前端常见的“名词”之外，还希望大家学前端时不要上来就我要精通XXX。你看前端的发展多么坎坷、都是通过解决一个一个问题才有今天的前端，学习也是同样的道理，先实现一个最 Low 的版本，再慢慢升级自己。

#### References

`[1]` CERN(European Organization for Nuclear Research): *https://en.wikipedia.org/wiki/CERN* 

`[2]` 第二个提案: *http://cds.cern.ch/record/369245/files/dd-89-001.pdf* 

`[3]` Håkon Wium Lie: *https://en.wikipedia.org/wiki/H\\%C3\\%A5kon_Wium_Lie* 

`[4]` CSS4 (disambiguation): *https://en.wikipedia.org/wiki/Document_Style_Semantics_and_Specification_Language* 

`[5]` Formatting Output Specification Instance: *https://en.wikipedia.org/wiki/Formatting_Output_Specification_Instance* 

`[6]` JavaScript: *https://en.wikipedia.org/wiki/JavaScript* 

`[7]` XML: *https://en.wikipedia.org/wiki/XML* 

`[8]` ECMA-262: *https://www.ecma-international.org/publications/standards/Ecma-262.htm*

原文链接：https://mp.weixin.qq.com/s/1UZtXP83OTGEFHUTqDQVEw







# 前端

### 1、什么是mvc、mvp、mvvm？什么是前后端分离，前后端分离的优缺点？

mvc是model-view-control

![https://img1.sycdn.imooc.com//5b71441c00015da504160175.jpg](https://img1.sycdn.imooc.com//5b71441c00015da504160175.jpg)



### 2、什么是单页面应用？为什么使用单页面应用？单页面应用路由实现的方法和原理？

单页面应用可以叫做单页面多片段切换应用。通过控制页面的删除或者隐藏来实现单页面应用。单页面在移动端使用比较广泛。可以带来极致的体验。

![https://img1.sycdn.imooc.com//5b725f76000141a506980682.jpg](https://img1.sycdn.imooc.com//5b725f76000141a505000489.jpg)



### 3、什么是单线程？单线程与多线程的区别？什么是进程？进程和线程的区别和联系？

单线程：就是同一时间只能做一件事情。JavaScript是单线程的。

多线程：就是同一时间可以同时做好几件事情。

进程中包含多个线程，单线程，多线程都是相对于同一个进程来说的。

一个浏览器tab页面就是一个进程。进程中包含js引擎线程，GUI线程、事件触发线程等。

进程是CPU资源分配的最小单位。

线程是CPU的最小调度单位。



### 4、异步调用的常用方法？什么是异步调用？

回调函数、promise、async/await、generate。

异步调用主要是通过状态来管理的，到了这个时间点，或者任务完成后，就开始着手工作。例如：

setTimeout(function()\\{\\},100),这个也可以看成是异步调用，100ms后开始执行函数内的代码。



### 5、对webpack的理解？为什么需要webpck？对构建、打包、编译的理解？

webpack它是代码编译工具，有入口，出口、loader和插件。其天生就代码分割、模块化，webpack2.0中加入tree shaking，用来提取公共代码，去掉死亡代码。

构建、打包、编译他们都是为了提高开发效率，让前端朝着标准化的路上继续迈进



### 6、git常用命令？git和svn的区别？github是什么，npm又是什么？

git的全部工作都是在这三个区之间工作。三个区是工作区，暂存区、远程仓库区。

建立一个git仓库：git init

clone 远程仓库：git clone +git仓库地址

本地仓库和远程仓库建立连接：git remote add origin +git地址

拉去远程仓库 git pull origin master(master分支)

提交到暂存区：git add +文件

提交到master，此时Header指针指到这里：git commit -m '文件描述’

推送到远程仓库：git push origin master

新建分支：git branch dev

删除本地分支：git branch -d dev (*删除分支时，必须切换到另一个分支，才能删除想要删除的分支*)

删除远程分支：git push origin -d dev

版本回退：git reset --hard HEAD^。



github是全球最大的代码托管平台。npm是全球最大的包管理工具。

github使用git clone +代码 ，可以下载代码。

npm通过npm install 安装，可以直接使用。



### 7、什么是构造函数？什么是原型链？原型链的用途？什么是对象？对象的用途？

构造函数也是函数，无非让其具有扩展性功能，它使用扩展性功能又用了原型链的原理，原型链又用了计算机中核心局部性原理，你自身没有往上级找，上级没有继续往外找，这其中其实闭包也用了这种原理。

对象：万物皆是对象，就是先总体看待事情，然后再局部。对象中又有key和value。也可能包含方法。



### 8、对http的认识？从输入url到页面展现都发生了什么？

这个参考链接：

```
`https://segmentfault.com/a/1190000013662126`
```



### 9、什么是BFC？如何实现BFC？盒子模型认识？如何实现标准盒模型？

这个是css中的块级格式化上下文。

盒子模型有标准盒模型和IE盒模型，

![https://img1.sycdn.imooc.com//5b725e3500018c4207550100.jpg](https://img1.sycdn.imooc.com//5b725e3500018c4205000067.jpg)

- 当设置为box-sizing:content-box时，将采用标准模式解析计算，也是默认模式；
- 当设置为box-sizing:border-box时，将采用怪异模式解析计算；



### 10、什么是栈，什么是堆？栈用来存储什么，堆用来存储什么？

栈用来存储基本变量类型（number\string\Boolean\undifeind\null）和指针地址。

堆用来存储对象（key和val）或者函数大括号里面的代码。

栈和堆有下面的连接关系

​           ![https://img1.sycdn.imooc.com//5b7129ec0001bbfc03830419.jpg](https://img1.sycdn.imooc.com//5b7129ec0001bbfc03830419.jpg)



### 11、什么是组件？什么是插件？组件和插件的区别和联系？

组件是模版和UI逻辑的结合。而插件可以是一堆组件的结合，它是框架在功能上的扩展，如vue.prototype.add=function()\\{\\}

他们都是在封装、继承、多态思想上产生而来。

区别：

1. vue插件可以将自己的模块添加到Vue原型对象上，然后组件中可以通过this直接引用。还要就是通过插件机制，可以通过一个入口，就可以将一系列组件添加到环境中，直接使用
2. 插件是采用通用接口编写的，多用于制作好的东西功能扩展。
3. vue组件只是一个独立的模块，可重复使用并且可以和其他对象进行交互的对象
4. 插件通常会为 Vue 添加全局功能。插件的范围没有限制——一般有下面几种：
   添加全局方法或者属性，如: vue-custom-element
   添加全局资源：指令/过滤器/过渡等，如 vue-touch
   通过全局 mixin 方法添加一些组件选项，如: vue-router
   添加 Vue 实例方法，通过把它们添加到 Vue.prototype 上实现。
   一个库，提供自己的 API，同时提供上面提到的一个或多个功能，如 vue-router
   Vue.js 的插件应当有一个公开方法 install 。
5. 如果你的模块或者组件想对外公开，最友好的方式就是通过插件机制提供



### 12、对nodejs的认识？什么是事件驱动？什么是非阻塞I/O？

nodejs是基于chrome V8引擎，以事件驱动，非阻塞I/O模型。他是一个可以在服务端运行js的环境。

事件驱动：就是触发一个事件，然后回调，再执行的过程。

非阻塞I/O：以异步来执行函数，先执行同步任务，耗时任务放在事件队列中，以此轮询执行



### 13、什么是hybrid？为什么使用hybrid？hybrid为什么可以不用审核直接发布？hybrid如何使用？

hybrid：H5与原生端交互混合技术方案

web、native两个人交流，要么web主动，要么native主动，要么web、native都主动。

- web主动就是webView UI 方案。也是市面上大部分采用的方案。通过jsbridge完成h5与native的双向通信，从而把native的一些原生能力（拍照、从相册中选取照片、查看通讯录、获取地理位置等，这些调用系统级别的能力，h5没有，所以这也是其不受审核，可以快速上线的原因）赋予给h5.（重点是webview渲染）

- native主动就是native UI 方案。例如reac-native\weex，在赋予h5原生api能力的基础上。进一步通过jsbridge将js解析成虚拟节点树virtual Dom传递到native并使用原生渲染。（重点是原生端渲染）

- 两者都主动。目前流行的小程序。通过更加定制化的jsbridge，并使用webview双线程的模式，隔离了js逻辑与UI渲染，形成了特殊的开发模式。加强了h5与Native混合，提高了交互体验和页面性能。

  ![https://img1.sycdn.imooc.com//5b72410e000122ac03230303.jpg](https://img1.sycdn.imooc.com//5b72410e000122ac03230303.jpg)

hybrid本质是在原生的App中，使用webview作为容器承载web页面。这样就需要h5与native实现双向通信，这里我们就需要翻译员，保证我们两者的正常通信---跨语言通讯方案。native使用Java，object-c，h5使用jsbridge。两者通信翻译员就是jsBridge。是要有翻译员就要给他提供最优质的环境webview。一切的翻译也是通过webview的翻译机制。

基于webview的机制和开发的api，有三种方案

1. API注入，原理其实就是native获取JavaScript环境上下文，直接在JavaScript上插入原生方法或者对象，使用js（图灵完备语言，有逻辑）直接调用。
2. webview中prompt、alert、console拦截。通常使用prompt，但这个方法使用频率较低

- 3.webview URL Scheme跳转拦截，通过webview信息冒泡传递的拦截，从而达到通讯。

  **流程：定制协议---拦截协议----参数传递---回调机制**

  **（协议有http协议、https协议、file协议等）**

  原理：在webview中发出的网络请求，客户端都能够监听和捕获到。

  ![https://img1.sycdn.imooc.com//5b72509b00010a5504640260.jpg](https://img1.sycdn.imooc.com//5b72509b00010a5504640260.jpg)



### 14、什么是浅拷贝？什么是深拷贝？如何实现深拷贝？

浅拷贝可以看做是一个快捷方式，实际共用一个内存地址。es6中的Object.assign(\\{target\\},\\{obj\\})就是浅拷贝。

深拷贝相对于新开辟一块内存地址。使用JSON.stringify()可以实现深拷贝。



### 15、什么是缓存？缓存的分类？cache、localStorage和sessionStorage和理解？

缓存是为了更快的进行磁盘I/O而存在的。有浏览器缓存、CDN缓存、路由缓存、服务器缓存等。

cache中会有http响应头和响应行的信息，如cache-control：max-age:20000。

还有就是cookie。cookie一般浏览器不超过4k ,主要是用来保存用户登陆信息。当发送请求时，会自动把其带上。

而localStorage和sessionStorage是浏览器本地storage中用来存取值的，sessionStorage浏览器关闭了就不存在了，localStorage浏览器关闭依然存在。



### 16、什么是闭包？闭包的用途？什么是递归？递归调用的用途？

闭包就是有权访问另一个函数作用域内的变量函数都是闭包。

闭包就是一个函数引用另外一个函数的变量，因为变量被引用着所以不会被回收，因此可以用来封装一个私有变量。这是优点也是缺点，**不必要的闭包只会徒增内存消耗！**另外使用闭包也要注意变量的值是否符合你的要求，因为他就像一个静态私有变量一样

下面的就是闭包

![https://img1.sycdn.imooc.com//5b72628900011edd03260248.jpg](https://img1.sycdn.imooc.com//5b72628900011edd03260248.jpg)


原文链接：https://www.imooc.com/article/details/id/67905



### 前端hook

在前端开发中，特别是在使用Vue.js这样的框架时，"Hook" 通常指的是一种机制，允许开发者在组件的特定生命周期阶段或满足某些条件时执行自定义的代码。然而，在Vue 2中，并没有直接引入名为"Hook"的概念，而是使用了一系列的选项（如`data`、`methods`、`computed`、`watch`等）和生命周期钩子（如`created`、`mounted`、`updated`、`destroyed`等）来实现类似的功能。

不过，从Vue 3开始，Vue引入了Composition API，其中的`setup`函数可以被视为一种“Hook”机制。

在`setup`函数中，你可以使用Vue提供的响应式系统、生命周期钩子和其他功能来组织你的组件逻辑。







# 技术

### 解耦

#### 解耦的定义

解耦（Decoupling）是指通过降低代码之间的依赖性，减少模块或组件之间的耦合程度。在软件开发中，解耦是一种良好的设计原则，它可以提高代码的可维护性、可测试性和可扩展性。

当两个模块或组件之间高度耦合时，它们的改动往往会相互影响，一个模块的修改可能会导致其他模块的变动，这增加了系统的复杂性和风险。

#### 解耦的目标

解耦的目标是将这种紧密耦合的关系松散化，使得模块之间的改动互不影响或最小化影响。

#### 实现解耦的方法

- 接口和抽象
  使用接口和抽象类定义模块之间的通信协议，而不是直接依赖具体实现。这样，当一个模块的实现发生变化时，其他模块不受影响，只需要适配新的实现即可。
- 依赖注入（DI）
  使用依赖注入来管理模块之间的依赖关系。通过将依赖关系的创建和绑定移到外部容器中，模块之间不再直接依赖具体实现，而是通过接口或抽象来进行通信，从而降低耦合度。

- 事件驱动编程
  使用事件驱动的方式来解耦模块之间的通信。模块通过发布和订阅事件来进行通信，而不是直接调用对方的方法。这样，模块之间的依赖关系可以通过事件进行解耦，每个模块只需要对感兴趣的事件进行订阅，而不需要知道具体的实现。
- 模块化设计
  将系统拆分成独立的模块，每个模块具有清晰的责任和功能。模块之间通过定义明确定义的接口进行通信，模块之间的依赖关系尽可能降低。

#### 解耦的优点

通过解耦，可以使系统更加灵活、可扩展和可维护。当一个模块需要修改或替换时，对其他模块的影响将最小化，使系统更具弹性和可扩展性。

同时，解耦也有助于提高代码的可测试性，因为模块可以更容易地进行单独的单元测试，而不需要依赖整个系统的其他部分。



### 转测是什么意思

转测在软件开发领域主要有两层含义：

1. **在软件开发流程中**，转测指的是开发人员完成软件功能的编写后，将工作成果移交给测试团队进行专业测试的环节。这时，开发人员通常会发送一封转测邮件给测试团队，邮件中会详细说明本次转测的内容（包括变更及影响范围）、提供转测所需的软件包或访问地址、指明负责的开发人员，并可能附带相关辅助材料，如SQL脚本、配置手册等。转测的目的是全面检查软件的功能、性能、兼容性等，确保其达到既定的质量标准。

2. **在数据库和系统迁移场景下**，转测涉及验证现有系统中的数据能否成功转移到新的替代系统中。这包括测试数据转换的完整性和准确性，确保转换后的系统能够正常运作。转换测试（Conversion Testing）是确保数据处理软件或系统在经过转换后仍能正确工作的关键步骤，特别关注数据库和程序代码的转换效果。

简而言之，转测是一个确保软件质量的重要阶段，无论是从开发到测试的流程传递，还是在系统迁移中的数据与功能验证，都是为了发现并修复潜在问题，提升软件的稳定性和用户满意度。



### 提测和转测有啥区别

提测和转测的区别是概念不同。

提测是指开发完成一个阶段的目标，将代码提交给测试人员，由测试人员对代码进行验证和测试。

而转测则是软件开发过程中一个特定的测试阶段，通常是在所有需求都开发完成并通过自测后进行的。转测的目的是对整个软件进行系统性的测试，以确保软件的整体质量和稳定性。 

在软件开发和测试流程中，“转测”和“提测”是常用的术语，但不同团队或公司可能存在使用差异。以下是它们的典型定义和区别：

---

**1. 转测（移交测试）**
• 定义：指开发团队将已开发完成的代码或功能模块正式移交给测试团队，进入系统测试阶段。

• 关键点：

  • 责任转移：开发团队确认代码达到可测试标准（如完成自测、冒烟测试通过），测试团队开始介入。

  • 阶段性标志：通常代表开发阶段结束，测试阶段启动。

  • 形式：可能涉及文档、代码、测试用例的同步移交。


• 示例：

  > “后端服务已完成联调，申请今日转测，测试环境已部署完毕。”

---

**2. 提测（提交测试）**
• 定义：指开发人员将代码或版本提交到测试环境，供测试团队执行测试。

• 关键点：

  • 动作性质：更强调“提交”动作，可能发生在开发过程中（如迭代提测）。

  • 频率：可能多次发生（如敏捷开发中每个迭代周期都会提测）。

  • 范围：可能是完整功能，也可能是部分代码（如修复BUG后的重新提测）。


• 示例：

  > “用户登录功能已修复，请将最新代码部署到测试环境，我们申请提测。”

---

**核心区别**
| 维度     | 转测                         | 提测                         |
| -------- | ---------------------------- | ---------------------------- |
| 主体     | 团队间移交（开发→测试）      | 开发主动提交到测试环境       |
| 阶段     | 标志开发阶段结束             | 可能发生在开发过程中多次提交 |
| 形式意义 | 更正式，伴随完整交付         | 可能是日常操作               |
| 前提条件 | 通常需通过冒烟测试、代码评审 | 可能仅需完成当前开发任务     |

---

**注意事项**
• 术语可能混用：部分团队可能不严格区分两者，需结合上下文理解。

• 流程差异：有些公司用“提测”指代“转测”，关键看团队规范。

---

**总结**
• 如果开发团队说“转测”，通常意味着他们确认代码已准备好全面测试；

• 如果说“提测”，可能是通知测试人员“新代码已部署，可以开始测试了”。



### 软件环境dev、sit、uat、pet、sim、prd

按开发、测试、上线的时间线排序：

DEV Development 开发环境

SIT System Integrate Test 系统集成测试环境（内测）

UAT User Acceptance Test 用户验收测试环境

PET Performance Evaluation Test 性能评估测试环境（压测）

SIM Simulation 高仿真环境

PRD/PROD Production 正式/生产环境







# 其他

### toA、toB、toC、ToG是什么？有什么区别？

TOA、TOB、TOC和ToG都是不同的业务模型或策略，它们分别针对不同的客户群体和市场。以下是这些术语的解释和它们之间的区别：

1. TOA（Targeting of Audience）：即“瞄准目标受众”。这种策略强调对目标受众的深入了解和分析，以便为他们提供定制化的产品或服务。它类似于艺术家在创作画作前思考观众的口味和需求，销售人员努力满足广泛的需求，使产品或服务更容易被大众接受。
2. TOB（Targeting of Business）：即“面向企业”或“面向商业”。这种策略专注于为企业客户提供产品或服务，如设备制造商为企业提供设备。TOB市场策略侧重于吸引和满足其他企业的需求，通常需要更为专业的方法。销售人员需要深入了解客户的业务，提供针对性的解决方案。
3. TOC（Targeting of Consumers）：即“瞄准消费者”或“面向消费者”。这种策略主要针对个人用户的日常必需品，如衣食住行。这类需求普遍且客户群体庞大，因此需求指标多且分散。TOC模式关注的是如何满足消费者的日常需求，并提供具有吸引力的产品或服务。
4. ToG（Targeting of Government）：即“面向政府”或“面向公共部门”。这种策略主要为政府或公共部门提供产品或服务，如IT解决方案提供商为政府开发定制的软件系统。ToG模式关注的是如何满足政府或公共部门的需求，并提供符合其特定要求的产品或服务。

这些策略之间的主要区别在于它们所针对的客户群体和市场不同。TOA、TOB和TOC分别针对一般消费者、企业客户和个人消费者，而ToG则针对政府或公共部门。此外，这些策略在业务模式和营销策略上也可能存在差异，以适应不同客户群体的需求和偏好。



### RSS订阅是什么

简易信息聚合订阅

RSS订阅，即简易信息聚合订阅，是一种基于XML的格式，用于发布和同步经常更新的网站内容，如新闻头条、博客文章、音频、视频等。

RSS订阅使得用户可以根据自己的兴趣，订阅感兴趣的网站信息，然后通过RSS阅读器或聚合器，用户可以自动接收新内容，无需手动访问每个网站。RSS订阅的系统通过内部推送机制获取网站生成的更新XML文档，将用户关心的最新网站信息及时主动地推送到用户桌面。

此外，RSS是一个开放标准，可以在各种设备和平台上使用，网站通常会提供一个RSS图标或链接，指向RSS源，让访问者知道他们可以订阅这个源。订阅过程通常只需要复制RSS源的URL并粘贴到阅读器中。



### minio是什么

MinIO 是一款高性能、分布式、开源的对象存储系统，专为大规模非结构化数据存储而设计。它采用 Go 语言编写，兼容 Amazon S3 API，支持多云、私有云及边缘计算环境，是云原生架构中广泛应用的存储解决方案。

核心特性

1. 高性能与可扩展性
    MinIO 在标准硬件上可实现每秒数百 GB 的读写速度，支持水平扩展。通过去中心化的无共享架构，数据均匀分布在多节点多硬盘中，并通过纠删码（Erasure Coding）技术保障高可用性。例如，在 4 台服务器的集群中，数据可被分割为多个分片并存储冗余校验块，即使部分节点或硬盘故障，仍能恢复数据。

2. S3 兼容性
    完全兼容 Amazon S3 API，用户可无缝迁移现有基于 S3 的应用至 MinIO，且支持 S3 生态工具（如 SDK、CLI），降低了开发和迁移成本。

3. 架构与数据保护
    • 纠删码技术：将对象分割为数据块（Data Blocks）和校验块（Parity Blocks），通过公式 `S = K + M` 实现灵活的数据冗余。例如，配置为 8 数据块 + 8 校验块时，最多允许 8 块磁盘损坏仍可恢复数据。

   • Bitrot 保护：实时校验数据哈希值，自动修复静默数据损坏，保障端到端的数据完整性。

4. 轻量级与开源
    单二进制文件部署，无外部依赖，资源占用低。遵循 GNU AGPL v3 协议，用户可自由修改、集成，并活跃于开源社区，支持持续迭代。

5. 适用场景
    广泛应用于非结构化数据存储，如：
    • 多媒体文件（图片、视频）

   • 大数据与 AI（日志分析、机器学习模型存储）

   • 混合云与灾备（跨云数据同步、零停机迁移）

企业级能力
 • 多租户与安全性：支持 IAM 身份认证、数据加密（传输/静态）及审计日志，满足企业级安全需求。

• 全球一致性：通过联合集群实现跨地域统一命名空间，适用于全球化数据管理。

部署灵活性
 • 可运行于裸机、Docker、Kubernetes 或 Windows 环境，并提供 Nginx、HAProxy 等负载均衡方案。

目前，MinIO 已被阿里巴巴、腾讯、华为等企业采用，成为替代传统存储和公有云服务的高性价比选择。



### Swagger

是一个规范和完整的框架，用于生成、描述、调用和可视化 RESTful 风格的 Web 服务。

总体目标是使客户端和文件系统作为服务器以同样的速度来更新。

文件的方法，参数和模型紧密集成到服务器端的代码，允许API来始终保持同步。