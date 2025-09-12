---
title: HTML
date: 2020-07-26 11:11:11
categories: 
- 前端知识
tags:
- HTML
- Web
- 标签
- 浏览器
---

### HTML是什么

HTML的全称为超文本标记语言，是一种标记语言。它包括一系列标签．通过这些标签可以将网络上的文档格式统一，使分散的资源连接为一个逻辑整体。HTML文本是由HTML命令组成的描述性文本。



### HTML中元素分类

HTML中元素可分：行内元素(inline)、块级元素(block)

#### 行内元素(inline)

行内元素也称为内联元素，行内元素不占有独立区域，其大小仅仅被动的依赖于自身内容的大小（例如文字和图片），所以一般不能随意设置其宽高、对齐等属性。

#### 行内元素的特点：

- 总是和相邻的行内元素在同一行上。
- 设置宽高无效，水平方向的padding和margin属性可以设置，但是垂直方向上的无效。
- 默认宽度是他自身内容的宽度。
- 行内元素只能容纳其他行内元素或者文本。 

#### 常见的行内元素：

```
<span>、<a>、<b>、<i>、<u>、<li>、<em>、<strong>
<img>、<input>、<button>、<textarea>、<select>、<section>、<label>
<sup>、<sub>、<big>、<small>、<ins>、<del>、<code>、<cite>、<dfn>、<kbd>、<var>
```

#### 块级元素(block)

块级元素占据其父元素（容器）的整个水平空间，垂直空间等于其内容高度，因此创建了一个“块”

#### 块级元素的特点：

- 总是在新行上开始；
- 高度，行高以及外边距和内边距都可控制；
- 宽度缺省是它的容器的100\\%，除非设定一个宽度。
- 它可以容纳内联元素和其他块元素

#### 常见的块级元素：

```
<div>、<p>、<h1>~<h6>
<nav>、<aside>、<header>、<footer>、<section>、<article>
<ul>、<li>、<ol>、<dl>、<dt>、<dd>
<form>、<address>、<caption>
<table>、<thead>、<tbody>、<tfoot>、<td>、<th>、<tr>
```

#### 行内元素与块级元素的区别？

HTML4中，元素被分成两大类：inline （内联元素）与 block （块级元素）。

（1） 格式上，默认情况下，行内元素不会以新行开始，而块级元素会新起一行。
（2） 内容上，默认情况下，行内元素只能包含文本和其他行内元素。而块级元素可以包含行内元素和其他块级元素。
（3） 行内元素与块级元素属性的不同，主要是盒模型属性上：行内元素设置 width 无效，height 无效（可以设置 line-height），设置 margin 和 padding 的上下不会对其他元素产生影响。

### 空元素定义

   标签内没有内容的 HTML 标签被称为空元素。空元素是在开始标签中关闭的。

   常见的空元素有：

```
<br>、<hr>、<img>、<input>、<link>、<meta>
```

#### HTML5 元素的分类

   HTML4中，元素被分成两大类: inline（内联元素）与 block（块级元素）。但在实际的开发过程中，因为页面表现的需要，前端工程师经常把 inline 元素的 display 值设定为 block （比如 a 标签），也经常把 block 元素的 display 值设定为inline 之后更是出现了 inline-block 这一对外呈现 inline 对内呈现 block 的属性。因此，简单地把 HTML 元素划分为inline 与 block 已经不再符合实际需求。

   HTML5中，元素主要分为7类：Metadata Flow Sectioning Heading Phrasing Embedded Interactive



### 简述一下你对 HTML 语义化的理解？

 （1） html 语义化主要指的是我们应该使用合适的标签来划分网页内容的结构;
 （2） html 语义化让页面的内容结构化，结构更清晰，易于理解，便于对浏览器、搜索引擎解析;
 （3） 即使在去掉或者丢失样式 CSS 情况下也以一种文档格式显示，呈现出清晰的结构，并且是容易阅读的;
 （4） 有助于爬虫抓取更多的有效信息，搜索引擎的爬虫也依赖于 HTML 标记来确定上下文和各个关键字的权重，有利于 SEO ;
 （5） 使阅读源代码的人对网站更容易将网站分块，便于阅读维护理解。便于团队开发和维护，语义化更具可读性，遵循W3C标准的团队都遵循这个标准，可以减少差异化

 （6)   方便其他设备解析（如屏幕阅读器、盲人阅读器、移动设备）以意义的方式来渲染网页

   回答：

比如说我们常用的 b 标签和 strong 标签，它们在样式上都是文字的加粗，但是 strong 标签拥有强调的语义。
对于一般显示来说，可能我们看上去没有差异，但是对于机器来说，就会有很大的不同。如果用户使用的是屏幕阅读器来访问网页的话，使用 strong 标签就会有明显的语调上的变化，而 b 标签则没有。如果是搜索引擎的爬虫对我们网页进行分析的话，那么它会依赖于 html 标签来确定上下文和各个关键字的权重，一个语义化的文档对爬虫来说是友好的，是有利于爬虫对文档内容解读的，从而有利于我们网站的 SEO 。从 html5 我们可以看出，标准是倾向于以语义化的方式来构建网页的，比如新增了 header 、footer 这些语义标签，删除了 big 、font 这些没有语义的标签。

   详细资料可以参考：
   [《语义化的 HTML 结构到底有什么好处？》](https://www.html.cn/archives/1668)
   [《如何理解 Web 语义化？》](https://www.zhihu.com/question/20455165)
   [《我的 HTML 会说话——从实用出发，谈谈 HTML 的语义化》](https://juejin.im/post/5a9c8866f265da23741072bf#heading-5)



### html5有哪些新特性、移除了那些元素？

HTML5 现在已经不是 SGML的子集，主要是关于图像，位置，存储，多任务等功能的增加

新增功能

- 用于媒介回放的 video 和 audio 元素;
- 本地离线存储 localStorage 长期存储数据，浏览器关闭后数据不丢失;
- sessionStorage 的数据在浏览器关闭后自动删除;
- 语意化更好的内容元素，比如 article、footer、header、nav、section、aside;
- 表单控件，calendar、date、time、email、url、search
- 新的技术webworker, websocket, Geolocation
- 新的文档属性 document.visibilityState
- 拖拽释放(Drag and drop) API
- 地理(Geolocation) API
- 画布(Canvas) API;

移除的元素：

- 纯表现的元素：basefont，big，center，font, s，strike，tt，u;
- 对可用性产生负面影响的元素：frame，frameset，noframes



### 如何处理HTML5新标签的浏览器兼容问题？


支持HTML5新标签：

* IE8/IE7/IE6支持通过document.createElement方法产生的标签，
  可以利用这一特性让这些浏览器支持HTML5新标签，

  浏览器支持新标签后，还需要添加标签默认的样式：

* 当然最好的方式是直接使用成熟的框架、使用最多的是html5shim框架
  
   ```
   <!--[if lt IE 9]>
   	<script> src="http://html5shim.googlecode.com/svn/trunk/html5.js"</script>
   <![endif]-->
   ```




### HTML和HTML5的区别

#### 什么是HTML？

HTML全称为超文本标记语言(Hyper Text Markup Language)，它包括一系列标签，通过这些标签可以将网络上的文档格式统一，使分散的Internet资源连接为一个逻辑整体。

#### 什么是HTML5?

HTML5是HTML的第五个版本，HTML5已经远远超越了标记语言的范畴，它的设计目的是在移动设备上支持多媒体，和HTML比起来，深度和广度上都做了进一步提升。HTML5更方便书写、精简，有利于程序员快速的阅读和开发。

#### 区别：

1.文档声明

 HTML： 

```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
```


或

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
```

 HTML5： 

```
<!DOCTYPE html>
```

 2.结构语义

```
HTML：没有体现结构语义化的标签，如<div id="" class=""></div>
HTML5：添加了许多具有语义化的标签，如<article>、<aside>、<audio>、<bdi>、<canvas>...
```

3.绘图方式
HTML：指可伸缩矢量图形，用于定义网络的基于矢量的图形。
HTML5：HTML5的canvas元素使用脚本（通常使用JavaScript）在网页上绘制图像，可以控制画布每一个像素。

4.音频和视频支持
HTML如果不使用Flash播放器支持，它不支持音频和视频。
HTML5使用<audio>和<video>标签来支持音频和视频控制。

5.语法处理
HTML无法处理不准确的语法。
HTML5能够处理不准确的语法。



### DOCTYPE 的作用是什么？

相关知识点：

   ```
   IE5.5 引入了文档模式的概念，而这个概念是通过使用文档类型（DOCTYPE）切换实现的。
   <!DOCTYPE>声明位于 HTML 文档中的第一行，处于 <html> 标签之前。告知浏览器的解析器用什么文档标准解析这个文档。
   DOCTYPE 不存在或格式不正确会导致文档以兼容模式呈现。
   ```

   回答（参考1-5）：

   ```
   <!DOCTYPE>  声明一般位于文档的第一行，它的作用主要是告诉浏览器以什么样的模式来解析文档。一般指定了之后会以标准模式来
   进行文档解析，否则就以兼容模式进行解析。在标准模式下，浏览器的解析规则都是按照最新的标准进行解析的。而在兼容模式下，浏
   览器会以向后兼容的方式来模拟老式浏览器的行为，以保证一些老的网站的正确访问。

   在 html5 之后不再需要指定 DTD 文档，因为 html5 以前的 html 文档都是基于 SGML 的，所以需要通过指定 DTD 来定义文
   档中允许的属性以及一些规则。而 html5 不再基于 SGML 了，所以不再需要使用 DTD。
   ```



### 标准模式与兼容模式各有什么区别？

标准模式的渲染方式和 JS 引擎的解析方式都是以该浏览器支持的最高标准运行。在兼容模式中，页面以宽松的向后兼容的方式显示，模拟老式浏览器的行为以防止站点无法工作。



### HTML5 为什么只需要写 `<!DOCTYPE HTML>`，而不需要引入 DTD？

HTML5 不基于 SGML，因此不需要对 DTD 进行引用，但是需要 DOCTYPE 来规范浏览器的行为（让浏览器按照它们应该的方式来运
行）。

而 HTML4.01 基于 SGML ，所以需要对 DTD 进行引用，才能告知浏览器文档所使用的文档类型。



### SGML 、 HTML 、XML 和 XHTML 的区别？

SGML（Standard Generalized Markup language）是标准通用置标语言，是一种定义电子文档结构和描述其内容的国际标准语言，是所有电子文档标记语言的起源。

HTML（HyperText Markup Language）是超文本标记语言，主要是用于规定怎么显示网页。

XML（Extensible Markup Language）是可扩展标记语言是未来网页语言的发展方向，XML 和 HTML 的最大区别就在于 XML 的标签是可以自己创建的，数量无限多，
而 HTML 的标签都是固定的而且数量有限。

XHTML（Extensible Hypertext Markup Language）也是现在基本上所有网页都在用的标记语言，他其实和 HTML 没什么本质的区别，标签都一样，用法也都一样，就是比 HTML 
更严格，比如标签必须都用小写，标签都必须有闭合标签等。



### DTD 介绍

DTD（ Document Type Definition 文档类型定义）是一组机器可读的规则，它们定义 XML 或 HTML 的特定版本中所有允许元素及它们的属性和层次关系的定义。在解析网页时，浏览器将使用这些规则检查页面的有效性并且采取相应的措施。

DTD 是对 HTML 文档的声明，还会影响浏览器的渲染模式（工作模式）。



### link 标签定义

link 标签定义文档与外部资源的关系。

link 元素是空元素，它仅包含属性。 此元素只能存在于 head 部分，不过它可出现任何次数。

link 标签中的 rel 属性定义了当前文档与被链接文档之间的关系。常见的 stylesheet 指的是定义一个外部加载的样式表。



### 页面导入样式时，使用 link 和 @import 有什么区别？

   （1）从属关系区别。 @import 是 CSS 提供的语法规则，只有导入样式表的作用；link 是 HTML 提供的标签，不仅可以加载 CSS 文件，还可以定义 RSS、rel 连接属性、引入网站图标等。

   （2）加载顺序区别。加载页面时，link 标签引入的 CSS 被同时加载；@import 引入的 CSS 将在页面加载完毕后被加载。

   （3）兼容性区别。@import 是 CSS2.1 才有的语法，故只可在 IE5+ 才能识别；link 标签作为 HTML 元素，不存在兼容性问题。

   （4）DOM 可控性区别。可以通过 JS 操作 DOM ，插入 link 标签来改变样式；由于 DOM 方法是基于文档的，无法使用 @import 的方式插入样式。



### 你对浏览器的理解？

   浏览器的主要功能是将用户选择的 web 资源呈现出来，它需要从服务器请求资源，并将其显示在浏览器窗口中，资源的格式通常是 HTML，也包括 PDF、image 及其他格式。用户用 URI（Uniform Resource Identifier 统一资源标识符）来指定所请求资源的位置。

   HTML 和 CSS 规范中规定了浏览器解释 html 文档的方式，由 W3C 组织对这些规范进行维护，W3C 是负责制定 web 标准的组织。

   但是浏览器厂商纷纷开发自己的扩展，对规范的遵循并不完善，这为 web 开发者带来了严重的兼容性问题。

   简单来说浏览器可以分为两部分，shell 和 内核。

   其中 shell 的种类相对比较多，内核则比较少。shell 是指浏览器的外壳：例如菜单，工具栏等。主要是提供给用户界面操作，参数设置等等。它是调用内核来实现各种功能的。内核才是浏览器的核心。内核是基于标记语言显示内容的程序或模块。也有一些浏览器并不区分外壳和内核。从 Mozilla 将 Gecko 独立出来后，才有了外壳和内核的明确划分。



### 介绍一下你对浏览器内核的理解？

   主要分成两部分：渲染引擎和 JS 引擎。

   渲染引擎的职责就是渲染，即在浏览器窗口中显示所请求的内容。默认情况下，渲染引擎可以显示 html、xml 文档及图片，它也可以借助插件（一种浏览器扩展）显示其他类型数据，例如使用 PDF 阅读器插件，可以显示 PDF 格式。

   JS 引擎：解析和执行 javascript 来实现网页的动态效果。

   最开始渲染引擎和 JS 引擎并没有区分的很明确，后来 JS 引擎越来越独立，内核就倾向于只指渲染引擎。



### 常见的浏览器内核比较

   Trident：这种浏览器内核是 IE 浏览器用的内核，因为在早期 IE 占有大量的市场份额，所以这种内核比较流行，以前有很多网页也是根据这个内核的标准来编写的，但是实际上这个内核对真正的网页标准支持不是很好。但是由于 IE 的高市场占有率，微软也很长时间没有更新 Trident 内核，就导致了 Trident 内核和 W3C 标准脱节。还有就是 Trident 内核的大量 Bug 等安全问题没有得到解决，加上一些专家学者公开自己认为 IE 浏览器不安全的观点，使很多用户开始转向其他浏览器。

   Gecko：这是 Firefox 和 Flock 所采用的内核，这个内核的优点就是功能强大、丰富，可以支持很多复杂网页效果和浏览器扩展接口，但是代价是也显而易见就是要消耗很多的资源，比如内存。

   Presto：Opera 曾经采用的就是 Presto 内核，Presto 内核被称为公认的浏览网页速度最快的内核，这得益于它在开发时的天生优势，在处理 JS 脚本等脚本语言时，会比其他的内核快3倍左右，缺点就是为了达到很快的速度而丢掉了一部分网页兼容性。

   Webkit：是 Safari 采用的内核，它的优点就是网页浏览速度较快，虽然不及 Presto 但是也胜于 Gecko 和 Trident，缺点是对于网页代码的容错性不高，也就是说对网页代码的兼容性较低，会使一些编写不标准的网页无法正确显示。WebKit 前身是 KDE 小组的 KHTML 引擎，可以说 WebKit 是 KHTML 的一个开源的分支。

   Blink：谷歌在 Chromium Blog 上发表博客，称将与苹果的开源浏览器核心 Webkit 分道扬镳，在 Chromium 项目中研发 Blink 渲染引擎（即浏览器核心），内置于 Chrome 浏览器之中。其实 Blink 引擎就是 Webkit 的一个分支，就像 webkit 是KHTML 的分支一样。Blink 引擎现在是谷歌公司与 Opera Software 共同研发，上面提到过的，Opera 弃用了自己的 Presto 内核，加入 Google 阵营，跟随谷歌一起研发 Blink。

   详细的资料可以参考：
   [《浏览器内核的解析和对比》](http://www.cnblogs.com/fullhouse/archive/2011/12/19/2293455.html)
   [《五大主流浏览器内核的源起以及国内各大浏览器内核总结》](https://blog.csdn.net/Summer_15/article/details/71249203)



### 常见浏览器所用内核

​    （1） IE 浏览器内核：Trident 内核，也是俗称的 IE 内核；

​    （2） Chrome 浏览器内核：统称为 Chromium 内核或 Chrome 内核，以前是 Webkit 内核，现在是 Blink内核；

​    （3） Firefox 浏览器内核：Gecko 内核，俗称 Firefox 内核；

​    （4） Safari 浏览器内核：Webkit 内核；

​    （5） Opera 浏览器内核：最初是自己的 Presto 内核，后来加入谷歌大军，从 Webkit 又到了 Blink 内核；

​    （6） 360浏览器、猎豹浏览器内核：IE + Chrome 双内核；

​    （7） 搜狗、遨游、QQ 浏览器内核：Trident（兼容模式）+ Webkit（高速模式）；

​    （8） 百度浏览器、世界之窗内核：IE 内核；

​    （9） 2345浏览器内核：好像以前是 IE 内核，现在也是 IE + Chrome 双内核了；

​    （10）UC 浏览器内核：这个众口不一，UC 说是他们自己研发的 U3 内核，但好像还是基于 Webkit 和 Trident ，还有说是基于火狐内核。



### 浏览器的渲染原理？

​    （1）首先解析收到的文档，根据文档定义构建一棵 DOM 树，DOM 树是由 DOM 元素及属性节点组成的。

​    （2）然后对 CSS 进行解析，生成 CSSOM 规则树。

​    （3）根据 DOM 树和 CSSOM 规则树构建渲染树。渲染树的节点被称为渲染对象，渲染对象是一个包含有颜色和大小等属性的矩形，渲染对象和 DOM 元素相对应，但这种对应关系不是一对一的，不可见的 DOM 元素不会被插入渲染树。还有一些DOM元素对应几个可见对象，它们一般是一些具有复杂结构的元素，无法用一个矩形来描述。

​    （4）当渲染对象被创建并添加到树中，它们并没有位置和大小，所以当浏览器生成渲染树以后，就会根据渲染树来进行布局（也可以叫做回流）。这一阶段浏览器要做的事情是要弄清楚各个节点在页面中的确切位置和大小。通常这一行为也被称为“自动重排”。

​    （5）布局阶段结束后是绘制阶段，遍历渲染树并调用渲染对象的 paint 方法将它们的内容显示在屏幕上，绘制使用 UI 基础组件。

​     值得注意的是，这个过程是逐步完成的，为了更好的用户体验，渲染引擎将会尽可能早的将内容呈现到屏幕上，并不会等到所有的html 都解析完成之后再去构建和布局 render 树。它是解析完一部分内容就显示一部分内容，同时，可能还在通过网络下载其余内容。

   详细资料可以参考：
   [《浏览器渲染原理》](https://juejin.im/book/5bdc715fe51d454e755f75ef/section/5bdc7207f265da613c09425d)
   [《浏览器的渲染原理简介》](https://coolshell.cn/articles/9666.html)
   [《前端必读：浏览器内部工作原理》](https://kb.cnblogs.com/page/129756/)
   [《深入浅出浏览器渲染原理》](https://blog.fundebug.com/2019/01/03/understand-browser-rendering/)



### 渲染过程中遇到 JS 文件怎么处理？（浏览器解析过程）

​    JavaScript 的加载、解析与执行会阻塞文档的解析，也就是说，在构建 DOM 时，HTML 解析器若遇到了 JavaScript，那么它会暂停文档的解析，将控制权移交给 JavaScript 引擎，等 JavaScript 引擎运行完毕，浏览器再从中断的地方恢复继续解析文档。

​    也就是说，如果你想首屏渲染的越快，就越不应该在首屏就加载 JS 文件，这也是都建议将 script 标签放在 body 标签底部的原因。当然在当下，并不是说 script 标签必须放在底部，因为你可以给 script 标签添加 defer 或者 async 属性。



### async和defer的作用是什么？有什么区别？（浏览器解析过程）

​    （1）脚本没有 defer 或 async，浏览器会立即加载并执行指定的脚本，也就是说不等待后续载入的文档元素，读到就加载并执行。

​    （2）defer 属性表示延迟执行引入的 JavaScript，即这段 JavaScript 加载时 HTML 并未停止解析，这两个过程是并行的。
​        当整个 document 解析完毕后再执行脚本文件，在 DOMContentLoaded 事件触发之前完成。多个脚本按顺序执行。

​    （3）async 属性表示异步执行引入的 JavaScript，与 defer 的区别在于，如果已经加载好，就会开始执行，也就是说它的执行仍然会阻塞文档的解析，只是它的加载过程不会阻塞。多个脚本的执行顺序无法保证。

   详细资料可以参考：
   [《defer 和 async 的区别》](https://segmentfault.com/q/1010000000640869)



### 什么是文档的预解析？（浏览器解析过程）

 Webkit 和 Firefox 都做了这个优化，当执行 JavaScript 脚本时，另一个线程解析剩下的文档，并加载后面需要通过网络加载的资源。这种方式可以使资源并行加载从而使整体速度更快。需要注意的是，预解析并不改变 DOM 树，它将这个工作留给主解析过程，自己只解析外部资源的引用，比如外部脚本、样式表及图片。



### CSS 如何阻塞文档解析？（浏览器解析过程） 

​    理论上，既然样式表不改变 DOM 树，也就没有必要停下文档的解析等待它们，然而，存在一个问题，JavaScript 脚本执行时可能在文档的解析过程中请求样式信息，如果样式还没有加载和解析，脚本将得到错误的值，显然这将会导致很多问题。

​    所以如果浏览器尚未完成 CSSOM 的下载和构建，而我们却想在此时运行脚本，那么浏览器将延迟 JavaScript 脚本执行和文档的解析，直至其完成 CSSOM 的下载和构建。也就是说，在这种情况下，浏览器会先下载和构建 CSSOM，然后再执行 JavaScript，最后再继续文档的解析。



### 渲染页面时常见哪些不良现象？（浏览器渲染过程）

​    FOUC：主要指的是样式闪烁的问题，由于浏览器渲染机制（比如firefox），在 CSS 加载之前，先呈现了 HTML，就会导致展示出无样式内容，然后样式突然呈现的现象。会出现这个问题的原因主要是 CSS 加载时间过长，或者 CSS 被放在了文档底部。

​    白屏：有些浏览器渲染机制（比如chrome）要先构建 DOM 树和 CSSOM 树，构建完成后再进行渲染，如果 CSS 部分放在 HTML 尾部，由于 CSS 未加载完成，浏览器迟迟未渲染，从而导致白屏；也可能是把 JS 文件放在头部，脚本的加载会阻塞后面文档内容的解析，从而页面迟迟未渲染出来，出现白屏问题。

   详细资料可以参考：
    [《前端魔法堂：解秘 FOUC》](https://juejin.im/entry/58f867045c497d0058e2ff3a)
    [《白屏问题和 FOUC》](https://www.jianshu.com/p/6617efa874b0)



### 如何优化关键渲染路径？（浏览器渲染过程）

​    为尽快完成首次渲染，我们需要最大限度减小以下三种可变因素：

​    （1）关键资源的数量。
​    （2）关键路径长度。
​    （3）关键字节的数量。

​    关键资源是可能阻止网页首次渲染的资源。这些资源越少，浏览器的工作量就越小，对 CPU 以及其他资源的占用也就越少。

​    同样，关键路径长度受所有关键资源与其字节大小之间依赖关系图的影响：某些资源只能在上一资源处理完毕之后才能开始下载，并且资源越大，下载所需的往返次数就越多。

​    最后，浏览器需要下载的关键字节越少，处理内容并让其出现在屏幕上的速度就越快。要减少字节数，我们可以减少资源数（将它们删除或设为非关键资源），此外还要压缩和优化各项资源，确保最大限度减小传送大小。

​    优化关键渲染路径的常规步骤如下：

​    （1）对关键路径进行分析和特性描述：资源数、字节数、长度。
​    （2）最大限度减少关键资源的数量：删除它们，延迟它们的下载，将它们标记为异步等。
​    （3）优化关键字节数以缩短下载时间（往返次数）。
​    （4）优化其余关键资源的加载顺序：您需要尽早下载所有关键资产，以缩短关键路径长度。

   详细资料可以参考：
   [《优化关键渲染路径》](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/optimizing-critical-rendering-path?hl=zh-cn)



### 什么是重绘和回流？（浏览器绘制过程）

​    重绘: 当渲染树中的一些元素需要更新属性，而这些属性只是影响元素的外观、风格，而不会影响布局的操作，比如 background-color，我们将这样的操作称为重绘。
​    回流：当渲染树中的一部分（或全部）因为元素的规模尺寸、布局、隐藏等改变而需要重新构建的操作，会影响到布局的操作，这样的操作我们称为回流。

​    常见引起回流属性和方法：

​    任何会改变元素几何信息（元素的位置和尺寸大小）的操作，都会触发回流。

​    （1）添加或者删除可见的 DOM 元素；
​    （2）元素尺寸改变——边距、填充、边框、宽度和高度
​    （3）内容变化，比如用户在 input 框中输入文字
​    （4）浏览器窗口尺寸改变——resize事件发生时
​    （5）计算 offsetWidth 和 offsetHeight 属性
​    （6）设置 style 属性的值
​    （7）当你修改网页的默认字体时。

​    回流必定会发生重绘，重绘不一定会引发回流。回流所需的成本比重绘高的多，改变父节点里的子节点很可能会导致父节点的一系列回流。

   常见引起重绘属性和方法：

   ![常见引起回流属性和方法](https://cavszhouyou-1254093697.cos.ap-chongqing.myqcloud.com/note-14.png)

   常见引起回流属性和方法：

   ![常见引起重绘属性和方法](https://cavszhouyou-1254093697.cos.ap-chongqing.myqcloud.com/note-13.png)

   详细资料可以参考：
   [《浏览器的回流与重绘》](https://juejin.im/post/5a9923e9518825558251c96a)



### 如何减少回流？（浏览器绘制过程）

​    （1）使用 transform 替代 top

​    （2）不要把节点的属性值放在一个循环里当成循环里的变量

​    （3）不要使用 table 布局，可能很小的一个小改动会造成整个 table 的重新布局

​    （4）把 DOM 离线后修改。如：使用 documentFragment 对象在内存里操作 DOM

​    （5）不要一条一条地修改 DOM 的样式。与其这样，还不如预先定义好 css 的 class，然后修改 DOM 的 className。



### 为什么操作 DOM 慢？（浏览器绘制过程）

 一些 DOM 的操作或者属性访问可能会引起页面的回流和重绘，从而引起性能上的消耗。



### 如何处理 HTML5 新标签的浏览器兼容问题？

（1） IE8/IE7/IE6 支持通过 document.createElement 方法产生的标签，可以利用这一特性让这些浏览器
        支持 HTML5 新标签，浏览器支持新标签后，还需要添加标签默认的样式。

（2） 当然也可以直接使用成熟的框架，比如 html5shiv ;

   ```html
<!--[if lt IE 9]>
   <script> src="https://cdn.jsdelivr.net/npm/html5shiv/dist/html5shiv.min.js"</script>
<![endif]-->

[if lte IE 9]……[endif] 判断 IE 的版本，限定只有 IE9 以下浏览器版本需要执行的语句。
   ```



### b 与 strong 的区别和 i 与 em 的区别？

   ```
    从页面显示效果来看，被 <b> 和 <strong> 包围的文字将会被加粗，而被 <i> 和 <em> 包围的文字将以斜体的形式呈现。
    但是 <b> <i> 是自然样式标签，分别表示无意义的加粗，无意义的斜体，表现样式为 \\{ font-weight: bolder\\}，仅仅表示「这里应该用粗体显示」或者「这里应该用斜体显示」，此两个标签在 HTML4.01 中并不被推荐使用。
    而 <em> 和 <strong> 是语义样式标签。 <em> 表示一般的强调文本，而 <strong> 表示比 <em> 语义更强的强调文本。
    使用阅读设备阅读网页时：<strong> 会重读，而 <b> 是展示强调内容。
   ```

   详细资料可以参考：
   [《HTML5 中的 b/strong，i/em 有什么区别？》](https://www.zhihu.com/question/19551271)



### 前端需要注意哪些 SEO ？

​    （1）合理的 title、description、keywords：搜索对着三项的权重逐个减小，title 值强调重点即可，重要关键词出现不要超过2次，而且要靠前，不同页面 title 要有所不同；description 把页面内容高度概括，长度合适，不可过分堆砌关键词，不同页面 description 有所不同；keywords 列举出重要关键词即可。

​    （2）语义化的 HTML 代码，符合 W3C 规范：语义化代码让搜索引擎容易理解网页。

​    （3）重要内容 HTML 代码放在最前：搜索引擎抓取 HTML 顺序是从上到下，有的搜索引擎对抓取长度有限制，保证重要内容肯定被抓取。

​    （4）重要内容不要用 js 输出：爬虫不会执行 js 获取内容

​    （5）少用 iframe：搜索引擎不会抓取 iframe 中的内容

​    （6）非装饰性图片必须加 alt

​    （7）提高网站速度：网站速度是搜索引擎排序的一个重要指标



### iframe 有那些缺点？

​    iframe 元素会创建包含另外一个文档的内联框架（即行内框架）。

​    主要缺点有：

​    （1） iframe 会阻塞主页面的 onload 事件。window 的 onload 事件需要在所有 iframe 加载完毕后（包含里面的元素）才会触发。在 Safari 和 Chrome 里，通过 JavaScript 动态设置 iframe 的 src 可以避免这种阻塞情况。
​    （2） 搜索引擎的检索程序无法解读这种页面，不利于网页的 SEO 。
​    （3） iframe 和主页面共享连接池，而浏览器对相同域的连接有限制，所以会影响页面的并行加载。
​    （4） 浏览器的后退按钮失效。
​    （5） 小型的移动设备无法完全显示框架。

   详细的资料可以参考：
   [《使用 iframe 的优缺点》](https://blog.csdn.net/yintianqin/article/details/72625785)
   [《iframe 简单探索以及 iframe 跨域处理》](https://segmentfault.com/a/1190000009891683)



### Label 的作用是什么？是怎么用的？

label标签来定义表单控制间的关系，当用户选择该标签时，浏览器会自动将焦点转到和标签相关的表单控件上。

   ```
    <label for="Name">Number:</label>
    <input type=“text“ name="Name" id="Name"/>
   ```



### HTML5 的 form 的自动完成功能是什么？

​    autocomplete 属性规定输入字段是否应该启用自动完成功能。默认为启用，设置为 autocomplete=off 可以关闭该功能。

​    自动完成允许浏览器预测对字段的输入。当用户在字段开始键入时，浏览器基于之前键入过的值，应该显示出在字段中填写的选项。

​    autocomplete 属性适用于 <form>，以及下面的 <input> 类型：text, search, url, telephone, email, password, datepickers, range 以及 color。



### 如何实现浏览器内多个标签页之间的通信? 

   相关资料：

​    （1）使用 WebSocket，通信的标签页连接同一个服务器，发送消息到服务器后，服务器推送消息给所有连接的客户端。

​    （2）使用 SharedWorker （只在 chrome 浏览器实现了），两个页面共享同一个线程，通过向线程发送数据和接收数据来实现标签页之间的双向通行。

​    （3）可以调用 localStorage、cookies 等本地存储方式，localStorge 另一个浏览上下文里被添加、修改或删除时，它都会触发一个 storage 事件，我们通过监听 storage 事件，控制它的值来进行页面信息通信；

​    （4）如果我们能够获得对应标签页的引用，通过 postMessage 方法也是可以实现多个标签页通信的。

   回答：

​    实现多个标签页之间的通信，本质上都是通过中介者模式来实现的。因为标签页之间没有办法直接通信，因此我们可以找一个中介者，让标签页和中介者进行通信，然后让这个中介者来进行消息的转发。

​    第一种实现的方式是使用 websocket 协议，因为 websocket 协议可以实现服务器推送，所以服务器就可以用来当做这个中介者。
​    标签页通过向服务器发送数据，然后由服务器向其他标签页推送转发。

​    第二种是使用 ShareWorker 的方式，shareWorker 会在页面存在的生命周期内创建一个唯一的线程，并且开启多个页面也只会使用同一个线程。这个时候共享线程就可以充当中介者的角色。标签页间通过共享一个线程，然后通过这个共享的线程来实现数据的交换。

​    第三种方式是使用 localStorage 的方式，我们可以在一个标签页对 localStorage 的变化事件进行监听，然后当另一个标签页修改数据的时候，我们就可以通过这个监听事件来获取到数据。这个时候 localStorage 对象就是充当的中介者的角色。

​    还有一种方式是使用 postMessage 方法，如果我们能够获得对应标签页的引用，我们就可以使用postMessage 方法，进行通信。

   详细的资料可以参考：

   [《WebSocket 教程》](http://www.ruanyifeng.com/blog/2017/05/websocket.html)
   [《WebSocket 协议：5分钟从入门到精通》](https://www.cnblogs.com/chyingp/p/websocket-deep-in.html)
   [《WebSocket 学习（一）——基于 socket.io 实现简单多人聊天室》](https://segmentfault.com/a/1190000011538416)
   [《使用 Web Storage API》](https://developer.mozilla.org/zh-CN/docs/Web/API/Web_Storage_API/Using_the_Web_Storage_API)
   [《JavaScript 的多线程，Worker 和 SharedWorker》](https://www.zhuwenlong.com/blog/article/590ea64fe55f0f385f9a12e5)
   [《实现多个标签页之间通信的几种方法》](https://juejin.im/post/5acdba01f265da23826e5633#heading-1)



### webSocket 如何兼容低版本浏览器？

 Adobe Flash Socket 、
 ActiveX HTMLFile (IE) 、
 基于 multipart 编码发送 XHR 、
 基于长轮询的 XHR



### 如何在页面上实现一个圆形的可点击区域？

​    （1）纯 html 实现，使用 <area> 来给 <img> 图像标记热点区域的方式，<map> 标签用来定义一个客户端图像映射，<area> 标签用来定义图像映射中的区域，area 元素永远嵌套在 map 元素内部，我们可以将 area 区域设置为圆形，从而实现可点击的圆形区域。

​    （2）纯 css 实现，使用 border-radius ，当 border-radius 的长度等于宽高相等的元素值的一半时，即可实现一个圆形的点击区域。

​    （3）纯 js 实现，判断一个点在不在圆上的简单算法，通过监听文档的点击事件，获取每次点击时鼠标的位置，判断该位置是否在我们规定的圆形区域内。

   详细资料可以参考：
   [《如何在页面上实现一个圆形的可点击区域？》](https://maizi93.github.io/2017/08/29/\\%E5\\%A6\\%82\\%E4\\%BD\\%95\\%E5\\%9C\\%A8\\%E9\\%A1\\%B5\\%E9\\%9D\\%A2\\%E4\\%B8\\%8A\\%E5\\%AE\\%9E\\%E7\\%8E\\%B0\\%E4\\%B8\\%80\\%E4\\%B8\\%AA\\%E5\\%9C\\%86\\%E5\\%BD\\%A2\\%E7\\%9A\\%84\\%E5\\%8F\\%AF\\%E7\\%82\\%B9\\%E5\\%87\\%BB\\%E5\\%8C\\%BA\\%E5\\%9F\\%9F\\%EF\\%BC\\%9F/)
   [《HTML <area><map> 标签及在实际开发中的应用》](https://www.zhangxinxu.com/wordpress/2017/05/html-area-map/)



### 如何在页面上实现一个圆形的可点击区域？

答案：css3、js、map 加 area

一.border-radius (css3)

对于圆形，最直接的方法想到的就是 css3 的圆角属性，这个属性可以将 html 元素的形状设置为圆形，这之后你想对该圆形区域设置什么事件就设置什么事件(当然包括点击)。（这里就不做具体的 test 了）

二.纯js实现 需要求一个点在不在圆上简单算法、获取鼠标坐标等等

通过事件坐标来实现（js），也就是通过 js 来进行一个区域判断，进而简介地的形成可点区域，以下给出主要的 js 测试代码：

```js
// 获取目标元素
var box = document.getElementById("box");

// 对目标元素target的圆形区域进行一个点击事件绑定
function bindClickOnCircleArea(target, callback) \\{
  target.onclick = function(e) \\{
    e = e || window.event;

    // target中心点的坐标
    var x1 = 100;
    var y1 = 100;

    // 事件源坐标
    var x2 = e.offsetX;
    var y2 = e.offsetY;

    // 校验是否在圆形点击区，在的话就执行callback回调
    // 计算事件触发点与target中心的位置
    var len = Math.abs(Math.sqrt(Math.pow(x2 - x1, 2) + Math.pow(y2 - y1, 2)));
    // 通过半径进行校验
    if (len <= 100) \\{
      callback();
    \\} else \\{
      alert("死鬼，跑哪去啊，你老婆我是黄皮肤还是白皮肤都分不清了吗");
    \\}
  \\};
\\}

// 执行
bindClickOnCircleArea(box, function() \\{
  alert("老婆，你让我好找啊，呜呜呜");
\\});
```

三.通过 map 加 area或者svg

```html
<img src="../imgs/test.jpg" width="200" border="0" usemap="#Map" />
<map name="Map" id="Map">
  <area
    shape="circle"
    coords="100,100,100"
    href="http://www.baidu.com"
    target="_blank"
  />
</map>
```

[参考](https://zhuanlan.zhihu.com/p/48168812)



### 实现不使用 border 画出 1 px 高的线，在不同浏览器的标准模式与怪异模式下都能保持一致的效果。

   ```html
<div style="height:1px;overflow:hidden;background:red"></div>
   ```



### title 与 h1 的区别？

 title 属性没有明确意义只表示是个标题，h1 则表示层次明确的标题，对页面信息的抓取也有很大的影响。



### `<img>` 的 title 和 alt 有什么区别？

​    title 通常当鼠标滑动到元素上的时候显示

​    alt 是 <img> 的特有属性，是图片内容的等价描述，用于图片无法加载时显示、读屏器阅读图片。可提图片高可访问性，除了纯装
​    饰图片外都必须设置有意义的值，搜索引擎会重点分析。



### Canvas 和 SVG 有什么区别？

 Canvas 是一种通过 JavaScript 来绘制 2D 图形的方法。Canvas 是逐像素来进行渲染的，因此当我们对 Canvas 进行缩放时，会出现锯齿或者失真的情况。

 SVG 是一种使用 XML 描述 2D 图形的语言。SVG 基于 XML，这意味着 SVG DOM 中的每个元素都是可用的。我们可以为某个元素
 附加 JavaScript 事件监听函数。并且 SVG 保存的是图形的绘制方法，因此当 SVG 图形缩放时并不会失真。

 详细资料可以参考：
   [《SVG 与 HTML5 的 canvas 各有什么优点，哪个更有前途？》](https://www.zhihu.com/question/19690014)



### 网页验证码是干嘛的，是为了解决什么安全问题？

 （1）区分用户是计算机还是人的公共全自动程序。可以防止恶意破解密码、刷票、论坛灌水
 （2）有效防止黑客对某一个特定注册用户用特定程序暴力破解方式进行不断的登陆尝试



### attribute 和 property 的区别是什么？

 attribute 是 dom 元素在文档中作为 html 标签拥有的属性；
 property 就是 dom 元素在 js 中作为对象拥有的属性。
 对于 html 的标准属性来说，attribute 和 property 是同步的，是会自动更新的，
 但是对于自定义的属性来说，他们是不同步的。



### 对 web 标准、可用性、可访问性的理解

可用性（Usability）：产品是否容易上手，用户能否完成任务，效率如何，以及这过程中用户的主观感受可好，是从用户的角度来看
产品的质量。可用性好意味着产品质量高，是企业的核心竞争力

可访问性（Accessibility）：Web 内容对于残障用户的可阅读和可理解性

可维护性（Maintainability）：一般包含两个层次

一是当系统出现问题时，快速定位并解决问题的成本，成本低则可维护性好。
二是代码是否容易被人理解，是否容易修改和增强功能。



### IE 各版本和 Chrome 可以并行下载多少个资源？

 （1）  IE6 2 个并发
 （2）  iE7 升级之后的 6 个并发，之后版本也是 6 个
 （3）  Firefox，chrome 也是6个



### Flash、Ajax 各自的优缺点，在使用中如何取舍？

​    Flash：
​    （1） Flash 适合处理多媒体、矢量图形、访问机器
​    （2） 对 CSS、处理文本上不足，不容易被搜索

​    Ajax：
​    （1） Ajax 对 CSS、文本支持很好，支持搜索
​    （2） 多媒体、矢量图形、机器访问不足

​    共同点：
​    （1） 与服务器的无刷新传递消息
​    （2） 可以检测用户离线和在线状态
​    （3） 操作 DOM



### 怎么重构页面？

 （1） 编写 CSS
 （2） 让页面结构更合理化，提升用户体验
 （3） 实现良好的页面效果和提升性能



### 浏览器架构

 * 用户界面
   * 主进程
   * 内核
       * 渲染引擎
       * JS 引擎
           * 执行栈
       * 事件触发线程
           * 消息队列
               * 微任务
               * 宏任务
       * 网络异步线程
       * 定时器线程



### 常用的 meta 标签

   ```
    <meta> 元素可提供有关页面的元信息（meta-information），比如针对搜索引擎和更新频度的描述和关键词。
    <meta> 标签位于文档的头部，不包含任何内容。<meta> 标签的属性定义了与文档相关联的名称/值对。

    <!DOCTYPE html>  H5标准声明，使用 HTML5 doctype，不区分大小写
    <head lang="en"> 标准的 lang 属性写法
    <meta charset="utf-8">    声明文档使用的字符编码
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1"/>   优先使用 IE 最新版本和 Chrome
    <meta name="description" content="不超过150个字符"/>       页面描述
    <meta name="keywords" content=""/>      页面关键词者
    <meta name="author" content="name, email@gmail.com"/>    网页作
    <meta name="robots" content="index,follow"/>      搜索引擎抓取
    <meta name="viewport" content="initial-scale=1, maximum-scale=3, minimum-scale=1, user-scalable=no"> 为移动设备添加 viewport
    <meta name="apple-mobile-web-app-title" content="标题"> iOS 设备 begin
    <meta name="apple-mobile-web-app-capable" content="yes"/>  添加到主屏后的标题（iOS 6 新增）
    是否启用 WebApp 全屏模式，删除苹果默认的工具栏和菜单栏
    <meta name="apple-itunes-app" content="app-id=myAppStoreID, affiliate-data=myAffiliateData, app-argument=myURL">
    添加智能 App 广告条 Smart App Banner（iOS 6+ Safari）
    <meta name="apple-mobile-web-app-status-bar-style" content="black"/>
    <meta name="format-detection" content="telphone=no, email=no"/>  设置苹果工具栏颜色
    <meta name="renderer" content="webkit">  启用360浏览器的极速模式(webkit)
    <meta http-equiv="X-UA-Compatible" content="IE=edge">     避免IE使用兼容模式
    <meta http-equiv="Cache-Control" content="no-siteapp" />    不让百度转码
    <meta name="HandheldFriendly" content="true">     针对手持设备优化，主要是针对一些老的不识别viewport的浏览器，比如黑莓
    <meta name="MobileOptimized" content="320">   微软的老式浏览器
    <meta name="screen-orientation" content="portrait">   uc强制竖屏
    <meta name="x5-orientation" content="portrait">    QQ强制竖屏
    <meta name="full-screen" content="yes">              UC强制全屏
    <meta name="x5-fullscreen" content="true">       QQ强制全屏
    <meta name="browsermode" content="application">   UC应用模式
    <meta name="x5-page-mode" content="app">    QQ应用模式
    <meta name="msapplication-tap-highlight" content="no">    windows phone 点击无高光
    设置页面不缓存
    <meta http-equiv="pragma" content="no-cache">
    <meta http-equiv="cache-control" content="no-cache">
    <meta http-equiv="expires" content="0">
   ```

   详细资料可以参考：
   [《Meta 标签用法大全》](http://www.cnblogs.com/qiumohanyu/p/5431859.html)



### css reset 和 normalize.css 有什么区别？

   相关知识点：

​    为什么会有 CSS Reset 的存在呢？那是因为早期的浏览器支持和理解的 CSS 规范不同，导致渲染页面时效果不一致，会出现很多兼容性问题。

​    reset 的目的，是将所有的浏览器的自带样式重置掉，这样更易于保持各浏览器渲染的一致性。

​    normalize 的理念则是尽量保留浏览器的默认样式，不进行太多的重置，而尽力让这些样式保持一致并尽可能与现代标准相符合。


​    1.Normalize.css 保护了有价值的默认值

​    Reset 通过为几乎所有的元素施加默认样式，强行使得元素有相同的视觉效果。 相比之下，Normalize.css 保持了许多默认的浏
​    览器样式。 这就意味着你不用再为所有公共的排版元素重新设置样式。 当一个元素在不同的浏览器中有不同的默认值时，Normali
​    ze.css 会力求让这些样式保持一致并尽可能与现代标准相符合。


​    2.Normalize.css 修复了浏览器的 bug

​    它修复了常见的桌面端和移动端浏览器的 bug。这往往超出了 Reset 所能做到的范畴。关于这一点，Normalize.css 修复的问题
​    包含了 HTML5 元素的显示设置、预格式化文字的 font-size 问题、在 IE9 中 SVG 的溢出、许多出现在各浏览器和操作系统中
​    的与表单相关的 bug。


​    3.Normalize.css 没有复杂的继承链

​    使用 Reset 最让人困扰的地方莫过于在浏览器调试工具中大段大段的继承链。在 Normalize.css 中就不会有这样的问题，因为在
​    我们的准则中对多选择器的使用时非常谨慎的，我们仅会有目的地对目标元素设置样式。


​    4.Normalize.css 是模块化的

​    这个项目已经被拆分为多个相关却又独立的部分，这使得你能够很容易也很清楚地知道哪些元素被设置了特定的值。因此这能让你自己
​    选择性地移除掉某些永远不会用到部分（比如表单的一般化）。


​    5.Normalize.css 拥有详细的文档

​    Normalize.css 的代码基于详细而全面的跨浏览器研究与测试。这个文件中拥有详细的代码说明并在 Github Wiki 中有进一步的
​    说明。这意味着你可以找到每一行代码具体完成了什么工作、为什么要写这句代码、浏览器之间的差异，并且你可以更容易地进行自己
​    的测试。

   回答：

​    css reset 是最早的一种解决浏览器间样式不兼容问题的方案，它的基本思想是将浏览器的所有样式都重置掉，从而达到所有浏览器样式保持一致的效果。但是使用这种方法，可能会带来一些性能上的问题，并且对于一些元素的不必要的样式的重置，其实反而会造成画蛇添足的效果。

​    后面出现一种更好的解决浏览器间样式不兼容的方法，就是 normalize.css ，它的思想是尽量的保留浏览器自带的样式，通过在原有的样式的基础上进行调整，来保持各个浏览器间的样式表现一致。相对与 css reset，normalize.css 的方法保留了有价值的默认值，并且修复了一些浏览器的 bug，而且使用 normalize.css 不会造成元素复杂的继承链。

   详细资料可以参考：
   [《关于CSS Reset 那些事（一）之 历史演变与 Normalize.css》](https://segmentfault.com/a/1190000003021766#articleHeader0)
   [《Normalize.css 和 Reset CSS 有什么本质区别没？》](https://segmentfault.com/q/1010000000117189)



### 用于预格式化文本的标签是？

预格式化就是保留文字在源码中的格式 最后显示出来样式与源码中的样式一致 所见即所得。

   ```
<pre> 定义预格式文本，保持文本原有的格式
   ```



### DHTML 是什么？

​    DHTML 将 HTML、JavaScript、DOM 以及 CSS 组合在一起，用于创造动态性更强的网页。通过 JavaScript 和 HTML DOM，能够动态地改变 HTML 元素的样式。

​    DHTML 实现了网页从 Web 服务器下载后无需再经过服务的处理，而在浏览器中直接动态地更新网页的内容、排版样式和动画的功能。例如，当鼠标指针移到文章段落中时，段落能够变成蓝色，或者当鼠标指针移到一个超级链接上时，会自动生成一个下拉式子链接目录等。

​    包括：
​    （1）动态内容（Dynamic Content）：动态地更新网页内容，可“动态”地插入、修改或删除网页的元件，如文字、图像、标记等。

​    （2）动态排版样式（Dynamic Style Sheets）：W3C 的 CSS 样式表提供了设定 HTML 标记的字体大小、字形、样式、粗细、文字颜色、行高度、加底线或加中间横线、缩排、与边缘距离、靠左右或置中、背景图片或颜色等排版功能，而“动态排版样式”即可以“动态”地改变排版样式。



### head 标签中必不少的是？

```
<head> 标签用于定义文档的头部，它是所有头部元素的容器。<head> 中的元素可以引用脚本、指示浏览器在哪里找到样式表、提供元信息等等。
<title> 定义文档的标题，它是 head 部分中唯一必需的元素。
```

文档的头部描述了文档的各种属性和信息，包括文档的标题、在 Web 中的位置以及和其他文档的关系等。绝大多数文档头部包含的数据都不会真正作为内容显示给读者。

​    下面这些标签可用在 head 部分：<base>, <link>, <meta>, <script>, <style>, 以及 <title>。

​    

### HTML5 新增的表单元素有？

 datalist 规定输入域的选项列表，通过 option 创建！ 

 keygen 提供一种验证用户的可靠方法，密钥对生成器，私钥存于客户端，公钥发到服务器，用于之后验证客户端证书！

 output 元素用于不同类型的输出！



### 在 HTML5 中，哪个方法用于获得用户的当前位置？

   ```
getCurrentPosition()
   ```



### 文档的不同注释方式？

```
HTML 的注释方法 <!--注释内容--> 
CSS 的��释方法 /*注释内容*/ 
JavaScript 的注释方法 /* 多行注释方式 */ //单行注释方式
```



### disabled 和 readonly 的区别？

disabled 指当 input 元素加载时禁用此元素。input 内容不会随着表单提交。
readonly 规定输入字段为只读。input 内容会随着表单提交。

无论设置 readonly 还是 disabled，通过 js 脚本都能更改 input 的 value



### 主流浏览器内核私有属性 css 前缀？

 mozilla 内核 （firefox,flock 等）    -moz
 webkit  内核 （safari,chrome 等）   -webkit
 opera   内核 （opera 浏览器）        -o
 trident 内核 （ie 浏览器）           -ms



### Chrome 中的 Waterfall ？

   详细资料可以参考：
   [《前端性能之 Chrome 的 Waterfall》](https://blog.csdn.net/carian_violet/article/details/84954360)
   [《教你读懂网络请求的瀑布图》](https://blog.csdn.net/csdn_girl/article/details/54911632)

[《前端妹子跟我抱怨她们的页面加载很慢的时候，如何在她面前优雅地装逼？》](https://www.zhihu.com/question/27085552/answer/35194131)



### Html 规范中为什么要求引用资源不加协议头`http`或者`https`？

​    如果用户当前访问的页面是通过 HTTPS 协议来浏览的，那么网页中的资源也只能通过 HTTPS 协议来引用，否则浏览器会出现警告信息，不同浏览器警告信息展现形式不同。

​    为了解决这个问题，我们可以省略 URL 的协议声明，省略后浏览器照样可以正常引用相应的资源，这项解决方案称为protocol-relative URL，暂且可译作协议相对 URL。

​    如果使用协议相对 URL，无论是使用 HTTPS，还是 HTTP 访问页面，浏览器都会以相同的协议请求页面中的资源，避免弹出类似的警告信息，同时还可以节省5字节的数据量。

   详细资料可以参考：
   [《协议相对 URL》](https://www.ludou.org/the-protocol-relative-url.html)
   [《Why you need protocol-relative URLs *now*》](https://www.tuicool.com/articles/nEjU7b)



### 行内元素

首先：CSS规范规定，每个元素都有display属性，确定该元素的类型，每个元素都有默认的display值，如div的display默认值为“block”，则为“块级”元素；span默认display属性值为“inline”，是“行内”元素

一个行内元素只占据它对应标签的边框所包含的空间<br>
一般情况下，行内元素只能包含数据和其他行内元素

常用：`a b span img input select strong`（强调的语气）

```
big, i, small, tt
abbr, acronym, cite, code, dfn, em, kbd, samp, var
bdo, br,  map, object, q, script, sub, sup
button, label, textarea
```



### 块级元素

占据一整行，高度、行高、内边距和外边距都可以改变，可以容纳块级标签和其他行内标签

常用：`div ul ol li dl dt dd h1 h2 h3 h4…p`

```
header,form,table,article,hr,aside,figure,canvas,video,audio,footer
```



###  空(void)元素有那些？

常见的空元素:` <br> <hr> <img> <input> <link> <meta>`



### Iframe的作用？

####  用法：

Iframe是用来在网页中插入第三方页面，早期的页面使用 iframe 主要是用于导航栏这种很多页面都相同的部分，这样可以在切换页面的时候避免重复下载。

#### 优点：

- 便于修改，模块分离，像一些信息管理系统会用到。
- iframe 能够原封不动的把嵌入的网页展现出来。
- 用来加载速度较慢的第三方内容如图标和广告
- 可以使脚本可以并行下载，可以实现跨子域通信
- 如果有多个网页引用 iframe，那么你只需要修改 iframe 的内容，就可以实现调用的每一个页面内容的更改，方便快捷。
- 网页如果为了统一风格，头部和版本都是一样的，就可以写成一个页面，用 iframe 来嵌套，可以增加代码的可重用。

#### 缺点：

- iframe 的创建比一般的 DOM 元素慢了 1-2 个数量级

- 会产生很多页面，不容易管理，iframe 页面会增加服务器的 http 请求

- 搜索引擎的检索程序（爬虫）无法解读这种页面，不利于 SEO；替代方案一般就是动态语言的 Incude 机制和 ajax 动态填充内容等。

- 框架结构中出现各种滚动条

- 使用框架结构时，保证设置正确的导航链接。

- iframe 会阻塞主页面的 Onload （加载）事件，如果页面的onload 事件不能及时触发，会让用户觉得网页加载很慢，用户体验不好；

- 本上不推荐使用，如果需要使用`iframe`，在 Safari 和 Chrome 中可以通过`javascript`动态给`iframe`添加`src`属性值来避免阻塞。

- iframe 和主页面共享连接池，而浏览器对相同域的连接有限制，所以会影响页面的并行加载。

  

### HTML 与 XHTM有什么区别，你觉得应该使用哪一个并说出理由。

**区别：** HTML是一种基本的 WEB 网页设计语言，XHTML 是一个基于 XML 的置标语言。

应该使用XHTML，因为XHTML是XML重写了HTML的规范，比HTML更加严格，表现如下：

1、XHTML中所有的标记都必须有一个相应的结束标签；XHTML文档必须拥有根元素。

2、XHTML所有标签的元素和属性的名字都必须使用小写；

3、所有的XML标记都必须合理嵌套；

4、所有的属性都必须用引号“”括起来；

5、把所有<和&特殊符号用编码表示；

6、给所有属性附一个值；

7、不要在注释内容中使用“--”；

8、图片必须使用说明文字。



### display：none；与 visibility： hidden 的区别是什么？

display：none；

使用该属性后，HTML 元素（对象）的宽度、高度等各种属性值都将“丢失”；

visibility：hidden； 

使用该属性后，HTML 元素（对象）仅仅是在视觉上看不见（完全透明），而它所占据的空间位置仍然存在，也即是说它仍具有高度、宽度等属性值。



### 语义化

1.HTML标签的语义化是指：

通过使用包含语义的标签（如h1-h6）恰当地表示文档结构。

就是让浏览器更好的读懂你写的代码，在进行 HTML 结构、表现、行为设计时，尽量使用语义化的标签，使程序代码简介明了，易于进行Web 操作和网站 SEO，方便团队协作的一种标准，以图实现一种“无障碍”的  Web 开发。

2.css命名的语义化是指：

为html标签添加有意义的class



### 为什么需要语义化：

- 去掉样式后页面呈现清晰的结构
- 盲人使用读屏器更好地阅读
- 搜索引擎更好地理解页面，有利于收录
- 便团队项目的可持续运作及维护



### 简述一下你对 HTML 语义化的理解？

①**用正确的标签做正确的事情。**

②html 语义化让页面的**内容结构化，结构更清晰**，便于对浏览器、搜索引擎解析；即使在没有样式 CSS 情况下也以一种文档格式显示，并且是容易阅读的;

③ 搜索引擎的爬虫也依赖于 HTML 标记来确定上下文和各个关键字的权重，**利于 SEO**;

④ 使阅读源代码的人对网站更容易将网站分块，**便于阅读维护理解**。



### Doctype作用？标准模式与兼容模式各有什么区别?

- DOCTYPE 是一种标准通用标记语言的文档类型声明，位于位`于HTML`文档中的第一行，处于 `<html>` 标签之前。
- 它的目的是要告诉浏览器的标准通用标记语言解析器，它应该按照何种规范（HTML 或 XHTML 规范）或使用什么样的文档类型定义（DTD）来解析文档。（如果你的页面没有 DOCTYPE 的声明，那么 compatMode 默认就是 BackCompat,浏览器按照自己的方式解析渲染页面）
- 只有确定了一个正确的文档类型，超文本标记语言或可扩展超文本标记语言中的标签和层叠样式表才能生效，甚至对 javascript 脚本都会有所影响。
- DOCTYPE不存在或格式不正确会导致文档以兼容模式呈现。
- 标准模式的排版 和JS运作模式都是以该浏览器支持的最高标准运行。在兼容模式中，页面以宽松的向后兼容的方式显示,模拟老式浏览器的行为以防止站点无法工作

```
<!DOCTYPE>声明是用来指示web浏览器关于页面使用哪个HTML版本进行编写的指令。
```


浏览器本身分为两种模式，一种是标准模式，一种是怪异模式，浏览器通过 doctype 来区分这两种模式，doctype 在 html 中的作用就是触发浏览器的标准模式，如果 html 中省略了 doctype，浏览器就会进入到 Quirks 模式的怪异状态，在这种模式下，有些样式会和标准模式存在差异，而 html 标准和 dom 标准值规定了标准模式下的行为，没有对怪异模式做出规定，因此不同浏览器在怪异模式下的处理也是不同的，所以一定要在 html 开头使用 doctype。



### HTML5 为什么只需要写 `<!DOCTYPE HTML>`？

- HTML5 不基于 SGML，因此不需要对DTD进行引用，但是需要doctype来规范浏览器的行为（让浏览器按照它们应该的方式来运行）
- 而HTML4.01基于SGML,所以需要对DTD进行引用，才能告知浏览器文档所使用的文档类型

其中，SGML 是标准通用标记语言,简单的说，就是比 HTML,XML 更老的标准，这两者都是由 SGML 发展而来的。BUT，HTML5 不是的。

`<!DOCTYPE>`声明位于位于 HTML 文档中的第一行，处于 `<html>` 标签之前。作用：告知浏览器的解析器用什么文档标准解析这个文档。DOCTYPE 不存在或格式不正确



### 块级排列

Div元素默认的向下排列的术语称为**块级排列**（Block-level layout）或者遵循**标准流**（Normal Flow）。在CSS中，块级元素（block-level elements）如`div`，默认情况下会一个接一个地从上到下排列，每个元素占据自己的行，这种排列方式就是所谓的“块级排列”。在标准流中，块级元素沿垂直轴（通常指高度方向）堆叠，而行内元素（inline elements）则在块级元素内部沿水平轴（宽度方向）排列。 



### 什么是BFC？

#### 定义：

BFC(Block formatting context)直译为"块级格式化上下文"。它是一个独立的渲染区域，只有Block-level box 参与， 它规定了内部的Block-level Box 如何布局，并且与这个区域外部毫不相干。

#### 布局规则：

A.  内部的 Box 会在垂直方向，一个接一个地放置。

B. Box 垂直方向的距离由 margin 决定。属于同一个 BFC 的两个相邻 Box的margin 会发生重叠。

C.  每个元素的 margin box 的左边， 与包含块 border box 的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。

D. BFC 的区域不会与 float box 重叠。

E.  BFC 就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。

F.  计算 BFC 的高度时，浮动元素也参与计算。

#### 哪些元素会生成 BFC：

A.  根元素

B. float 属性不为 none

C. position 为 absolute 或 fixed

D. display 为 inline-block， table-cell，table-caption， flex， inline-flex F. overflow 不为visible

#### 特点和作用：

1. **渲染规则**：在BFC内部，块级盒（block-level boxes）会在垂直方向上一个接一个地排列，其布局不受外部元素的影响。这意味着，在BFC内部，元素不会与外部浮动元素发生重叠，同时，BFC内部的浮动元素也不影响其外部的布局。

2. **防止外边距折叠**：当两个垂直相邻的元素都处于同一个BFC中时，它们的外边距不会发生折叠现象。而如果两个元素不在同一个BFC内，它们的外边距可能会合并（取两者中的最大值）。

3. **包含浮动**：BFC可以包含其内部的浮动元素，这意味着计算BFC的高度时，会自动将浮动元素的高度纳入计算，从而避免了高度塌陷的问题。

4. **布局隔离**：BFC为内部元素创建了一个隔离的环境，使得内部元素的布局不会影响外部元素，反之亦然。这有助于解决一些布局冲突问题。

#### 创建BFC的方式

有多种，满足以下任意一条即可触发一个新的BFC：

- 根元素（html）。
- `float`属性不为`none`。
- `position`属性为`absolute`或`fixed`。
- `display`属性为`inline-block`, `table-cell`, `table-caption`, `flex`, 或 `inline-flex`。
- `overflow`属性不为`visible`（通常是`hidden`, `auto`, 或 `scroll`）。

理解和运用BFC是解决CSS布局问题（如清除浮动、防止外边距重叠、实现自适应两栏布局等）的重要手段。



### 表格自动换行怎么实现？

word-break：normal 使用浏览器默认的换行规则；

break-all允许单词内换行；

keep-all只能在半角空格或连字符处换行

word-wrap：normal 是用浏览器默认的换行规则；break-word 在长单词或 URL 地址内部进行换行。



### box-sizing

Box-sizing： 用来指定盒模型的大小的计算方式。主要分为boreder-box（从边框固定盒子大小）、content-box（从内容固定盒子大小）两种计算方式。



### HTML5 的 form 如何关闭自动完成功能？

答案：将不想要自动完成的 `form` 或 `input` 设置为 `autocomplete=off`

解析：[MDN](https://developer.mozilla.org/zh-CN/docs/Web/Security/Securing_your_site/Turning_off_form_autocompletion)



### 如何处理HTML5新标签的浏览器兼容问题？

支持 HTML5 新标签：

- IE8/IE7/IE6 支持通过 document.createElement 方法产生的标签，
  可以利用这一特性让这些浏览器支持 HTML5 新标签，
  浏览器支持新标签后，还需要添加标签默认的样式：
- 当然最好的方式是直接使用成熟的框架、使用最多的是 html5shim 框架

```html
<!--[if lt IE 9]>
  <script>
    src = "http://html5shim.googlecode.com/svn/trunk/html5.js";
  </script>
<![endif]-->
```



### 如何区分 HTML 和HTML5？

DOCTYPE声明\新增的结构元素\功能元素



### HTML5的离线储存怎么使用，工作原理能不能解释一下？

用户在线时，保存更新用户机器上的缓存文件；当用户离线时，可以正常访离线储存问站点或应用内容

- 在线的情况下，浏览器发现html头部有manifest属性，它会请求manifest文件，如果是第一次访问app，那么浏览器就会根据manifest文件的内容下载相应的资源并且进行离线存储。
- 如果已经访问过app并且资源已经离线存储了，那么浏览器就会使用离线的资源加载页面，然后浏览器会对比新的manifest文件与旧的manifest文件，如果文件没有发生改变，就不做任何操作，如果文件改变了，那么就会重新下载文件中的资源并进行离线存储
- 离线的情况下，浏览器就直接使用离线存储的资源

原理：HTML5的离线存储是基于一个新建的.appcache文件的缓存机制(不是存储技术)，通过这个文件上的解析清单离线存储资源，这些资源就会像cookie一样被存储了下来。之后当网络在处于离线状态下时，浏览器会通过被离线存储的数据进行页面展示

参考链接：[有趣的HTML5：离线存储](https://segmentfault.com/a/1190000000732617)



### HTML5 的离线储存怎么使用，工作原理能不能解释一下？

在用户没有与因特网连接时，可以正常访问站点或应用，在用户与因特网连接时，更新用户机器上的缓存文件。

原理：HTML5 的离线存储是基于一个新建的 .appcache 文件的缓存机制（不是存储技术），通过这个文件上的解析清单离线存储资源，这些资源就会像 cookie 一样被存储了下来。之后当网络在处于离线状态下时，浏览器会通过被离线存储的数据进行页面展示。

   ```
如何使用：
    （1）创建一个和 html 同名的 manifest 文件，然后在页面头部像下面一样加入一个 manifest 的属性。
        <html lang="en" manifest="index.manifest">
    （2）在如下 cache.manifest 文件的编写离线存储的资源。
      	CACHE MANIFEST
      	#v0.11
      	CACHE:
      	js/app.js
      	css/style.css
      	NETWORK:
      	resourse/logo.png
      	FALLBACK:
      	/ /offline.html

        CACHE: 表示需要离线存储的资源列表，由于包含 manifest 文件的页面将被自动离线存储，所以不需要把页面自身也列出来。
        NETWORK: 表示在它下面列出来的资源只有在在线的情况下才能访问，他们不会被离线存储，所以在离线情况下无法使用这些资源。不过，如果在 CACHE 和 NETWORK 中有一个相同的资源，那么这个资源还是会被离线存储，也就是说 CACHE 的优先级更高。
        FALLBACK: 表示如果访问第一个资源失败，那么就使用第二个资源来替换他，比如上面这个文件表示的就是如果访问根目录下任何一个资源失败了，那么就去访问 offline.html 。

    （3）在离线状态时，操作 window.applicationCache 进行离线缓存的操作。
    如何更新缓存：

    （1）更新 manifest 文件
    （2）通过 javascript 操作
    （3）清除浏览器缓存

    注意事项：
    （1）浏览器对缓存数据的容量限制可能不太一样（某些浏览器设置的限制是每个站点 5MB）。
    （2）如果 manifest 文件，或者内部列举的某一个文件不能正常下载，整个更新过程都将失败，浏览器继续全部使用老的缓存。
    （3）引用 manifest 的 html 必须与 manifest 文件同源，在同一个域下。
    （4）FALLBACK 中的资源必须和 manifest 文件同源。
    （5）当一个资源被缓存后，该浏览器直接请求这个绝对路径也会访问缓存中的资源。
    （6）站点中的其他页面即使没有设置 manifest 属性，请求的资源如果在缓存中也从缓存中访问。
    （7）当 manifest 文件发生改变时，资源请求本身也会触发更新。
   ```

   详细的使用可以参考：
   [《HTML5 离线缓存-manifest 简介》](https://yanhaijing.com/html/2014/12/28/html5-manifest/)
   [《有趣的 HTML5：离线存储》](https://segmentfault.com/a/1190000000732617)



### 浏览器是怎么对 HTML5 的离线储存资源进行管理和加载的呢？

​    在线的情况下，浏览器发现 html 头部有 manifest 属性，它会请求 manifest 文件，如果是第一次访问 app ，那么浏览器就会根据 manifest 文件的内容下载相应的资源并且进行离线存储。如果已经访问过 app 并且资源已经离线存储了，那么浏览器就会使用离线的资源加载页面，然后浏览器会对比新的 manifest 文件与旧的 manifest 文件，如果文件没有发生改变，就不做任何操作，如果文件改变了，那么就会重新下载文件中的资源并进行离线存储。

​    离线的情况下，浏览器就直接使用离线存储的资源。



### HTML5的离线储存使用：

- 在文档的 html 标签设置 manifest 属性，如 manifest="/offline.appcache"

  ```html
  <!DOCTYPE html>
  <html manifest="cache.manifest">
    ...
  </html>
  ```

- 在项目中新建 manifest 文件，manifest 文件的命名建议：xxx.appcache

- 在 web 服务器配置正确的 MIME-type，即 text/cache-manifest

  如何使用：

- 页面头部像下面一样加入一个manifest的属性；

- 在cache.manifest文件的编写离线存储的资源

- 在离线状态时，操作window.applicationCache进行需求实现

```
CACHE MANIFEST
    #v0.11
    CACHE:
    js/app.js
    css/style.css
    NETWORK:
    resourse/logo.png
    FALLBACK:
    / /offline.html
```

代码说明：

离线存储的 manifest 一般由三个部分组成:

1. CACHE:表示需要离线存储的资源列表，由于包含 manifest 文件的页面将被自动离线存储，所以不需要把页面自身也列出来。
2. NETWORK:表示在它下面列出来的资源只有在在线的情况下才能访问，他们不会被离线存储，所以在离线情况下无法使用这些资源。不过，如果在 CACHE 和 NETWORK 中有一个相同的资源，那么这个资源还是会被离线存储，也就是说 CACHE 的优先级更高。
3. FALLBACK:表示如果访问第一个资源失败，那么就使用第二个资源来替换他，比如上面这个文件表示的就是如果访问根目录下任何一个资源失败了，那么就去访问 offline.html。

[参考](https://www.cnblogs.com/zhangym118/archive/2016/09/22/5897056.html)



### HTML5的form如何关闭自动完成功能？

给不想要提示的 form 或某个 input 设置为 autocomplete=off。



### 如何实现浏览器内多个标签页之间的通信？（阿里）

- WebSocket

- SharedWorker(Web Worker API)

- 也可以调用localstorge、cookies等本地存储方式，storage 事件(localStorge API)

- iframe + contentWindow

- postMessage




### webSocket如何兼容低浏览器？(阿里)

- Adobe Flash Socket 、
- ActiveX HTMLFile (IE) 、
- 基于 multipart 编码发送 XHR 、
- 基于长轮询的 XHR



### Label 的作用是什么？是怎么用的？

label 标签来定义表单控制间的关系，**当用户选择该标签时，浏览器会自动将焦点转到和标签相关的表单控件上**。

解析：两种用法：**一种是 id 绑定，一种是嵌套**

```html
使用方法1：
  `<label for="mobile">Number:</label>`
  `<input type="text" id="mobile"/>`
使用方法2：
  `<label>Date:<input type="text"/></label>`
```



### 如何处理HTML5新标签的浏览器兼容问题？

- 通过 document.createElement 创建新标签
- 使用垫片 html5shiv.js



### HTML5 存储类型有什么区别？

答案：Media API、Text Track API、Application Cache API、User Interaction、Data Transfer API、Command API、Constraint Validation API、History API



### HTML5 引入什么新的表单属性？

Datalist datetime output keygen date month week time number range emailurl



### 标签上title 与 alt 属性的区别是什么?

 Alt 当图片不显示时，用文字代表。Title为该属性提供信息。

 

### 改变元素的外边距用什么属性？改变元素的内填充用什么属性？

改变元素的外边距用 margin，改变元素的内填充用 padding。

 

### 在新窗口打开链接的方法是？

 target：_blank。

 

### 合理的页面布局中常听过结构与表现分离，那么结构是什么？表现是什么？

结构是 html，表现是 css。



### 新的 HTML5 文档类型和字符集是？

```8
HTML5文档类型：<!doctype html>
HTML5使用的编码<meta charset=”UTF-8”>
```



### 请谈一下你对网页标准和标准制定机构重要性的理解。

答案：降低开发难度及开发成本，减少各种 BUG、安全问题， 提高网站易用性



### 对 web 标准、可用性、可访问性的理解

可用性（Usability）：产品是否容易上手，用户能否完成任务，效率如何，以及这过程中用户的主观感受可好，是从用户的角度来看产品的质量。可用性好意味着产品质量高，是企业的核心竞争力。

可访问性（Accessibility）：Web 内容对于残障用户的可阅读和可理解性

可维护性（Maintainability）：一般包含两个层次，一是当系统出现问题时，快速定位并解决问题的成本，成本低则可维护性好。二是代码是否容易被人理解，是否容易修改和增强功能。



### 前端页面有哪三层构成，分别是什么？作用是什么？

答案：分成：结构层、表示层、行为层。

1. 结构层（structural layer）

由 HTML 或 XHTML 之类的标记语言负责创建。标签，也就是那些出现在尖括号里的单词，对网页内容的语义含义做出了描述，但这些标签不包含任何关于如何显示有关内容的信息。例如，P 标签表达了这样一种语义：“这是一个文本段。”

2. 表示层（presentation layer）

由 CSS 负责创建。 CSS 对“如何显示有关内容”的问题做出了回答。

3. 行为层（behaviorlayer）

负责回答“内容应该如何对事件做出反应”这一问题。这是 Javascript 语言和 DOM 主宰的领域。



### 对于 WEB 标准以及 W3C 的理解与认识问题

<b>web 标准</b>简单来说可以分为<b>结构、表现和行为</b>。其中结构主要是有 HTML 标签组成。或许通俗点说，在页面 body 里面我们写入的标签都是为了页面的结构。表现即指 css 样式表，通过 css 可以是页面的结构标签更具美感。行为是指页面和用户具有一定的交互，同时页面结构或者表现发生变化，主要是有 js 组成。

web 标准一般是将该三部分独立分开，使其更具有模块化。但一般产生行为时，就会有结构或者表现的变化，也使这三者的界限并不那么清晰。

答案：标签闭合、标签小写、不乱嵌套、提高搜索机器人搜索几率、使用外 链 css 和 js 脚本、结构行为表现的分离、文件下载与页面速度更快、内容能被更多的用户所访问、内容能被更广泛的设备所访问、更少的代码和组件，容易维 护、改版方便，不需要变动页面内容、提供打印版本而不需要复制内容、提高网站易用性。

W3C 对 web 标准提出了规范化的要求，也就是在实际编程中的一些代码规范：包含如下几点

#### 1.对于结构要求：

（标签规范可以提高搜索引擎对页面的抓取效率，对 SEO 很有帮助）

1）标签字母要小写

2）标签要闭合

3）标签不允许随意嵌套

#### 2.对于 css 和 js 来说

1）尽量使用外链 css 样式表和 js 脚本。是结构、表现和行为分为三块，符合规范。同时提高页面渲染速度，提高用户的体验。

2）样式尽量少用行间样式表，使结构与表现分离，标签的 id 和 class 等属性命名要做到见文知义，标签越少，加载越快，用户体验提高，代码维护简单，便于改版

3）不需要变动页面内容，便可提供打印版本而不需要复制内容，提高网站易用性。



### 实现不使用 border 画出1px高的线，在不同浏览器的标准模式与怪异模式下都能保持一致的效果

```
<div style="height:1px;overflow:hidden;background:red"></div>
```



### 网页验证码是干嘛的，是为了解决什么安全问题

- 区分用户是计算机还是人的公共全自动程序。可以防止恶意破解密码、刷票、论坛灌水
- 有效防止黑客对某一个特定注册用户用特定程序暴力破解方式进行不断的登陆尝试



### title与h1的区别、b与strong的区别、i与em的区别？

- `title`属性没有明确意义只表示是个标题，H1则表示层次明确的标题，对页面信息的抓取也有很大的影响
- `strong`是标明重点内容，有语气加强的含义，使用阅读设备阅读网络时：<strong>会重读，而<B>是展示强调内容
- i内容展示为斜体，em表示强调的文本



### 页面导入样式时，使用 link 和 @import 有什么区别？

- link 属于HTML标签，除了加载CSS外，还能用于定 RSS等；@import 只能用于加载CSS
- 页面加载的时，link 会同时被加载，而 @import 引用的 CSS 会等到页面被加载完再加载
- @import 只在 IE5 以上才能被识别，而 link 是HTML标签，无兼容问题



### HTML5有哪些新特性？

* 新增选择器 document.querySelector、document.querySelectorAll
* 拖拽释放(Drag and drop) API
* 媒体播放的 video 和 audio
* 本地存储 localStorage 和 sessionStorage
* 离线应用 manifest
* 桌面通知 Notifications
* 语意化标签 article、footer、header、nav、section
* 增强表单控件 calendar、date、time、email、url、search
* 地理位置 Geolocation
* 多任务 webworker
* 全双工通信协议 websocket
* 历史管理 history
* 跨域资源共享(CORS) Access-Control-Allow-Origin
* 页面可见性改变事件 visibilitychange
* 跨窗口通信 PostMessage
* Form Data 对象
* 绘画 canvas



### HTML5移除了那些元素？

* 纯表现的元素：basefont、big、center、font、s、strike、tt、u
* 对可用性产生负面影响的元素：frame、frameset、noframes



### webSocket 如何兼容低浏览器？

* Adobe Flash Socket
* ActiveX HTMLFile (IE)
* 基于 multipart 编码发送 XHR
* 基于长轮询的 XHR



### 标签

  * 自然样式标签：b, i, u, s, pre
  * 语义样式标签：strong, em, ins, del, code
  * 应该准确使用语义样式标签, 但不能滥用。如果不能确定时，首选使用自然样式标签



### title 与 h1 的区别

title 表示是整个页面标题，h1 则表示层次明确的标题，对页面信息的抓取有很大的影响

①title用于网站信息标题，突出网站标题或关键字，一个网站可以有多个title，seo权重高于H1；H1概括的是文章主题，一个页面最好只用一个H1，seo权重低于title。

解析：

A.从网站角度而言，title则重于网站信息标题，突出网站标题或关键字用title，一篇文章，一个页面最好只

用一个H1，H1用得太多，会稀释主题；一个网站可以有多个title，最好一个单页用一个title以便突出网站页面

主题信息。

B.从文章角度而言，H1则概括的是文章主题，突出文章主题，用H1，面对的用户，要突出其视觉效果。

C.从SEO角度而言，title的权重高于H1，其适用性要比H1广。



### b 与 strong 的区别

strong 标明重点内容，有语气加强的含义，使用阅读设备阅读网络时，strong 会重读，而 b 是展示强调内容

②b为了加粗而加粗，strong为了标明重点而加粗

解析：

A.b这个标签对应 bold，即文本加粗，其目的仅仅是为了加粗显示文本，是一种样式／风格需求；

B.strong这个标签意思是加强字符的语气，表示该文本比较重要，提醒读者／终端注意。为了达到这个目的，浏览器等终端将其加粗显示；



### i 与 em 的区别？

i 内容展示为斜体，em 表示强调的文本

③ 同②i为了斜体而斜体，em为了标明重点而斜体，且对于搜索引擎来说strong和em比b和i要重视的多








## 其他



### 简述一下 src 与 href 的区别

答案：src 用于引用资源，替换当前元素；href 用于在当前文档和引用资源之间确立联系。

解析：

#### href

href 标识超文本引用，用在 link 和 a 等元素上，href 是引用和页面关联，是在当前元素和引用资源之间建立联系

href（hypertext reference/超文本引用）指向网络资源所在位置，建立和当前元素（锚点）或当前文档（链接）之间的链接，如果我们在文档中添加

```
<link href="common.css" rel="stylesheet"/>
```

那么浏览器会识别该文档为css文件，就会并行下载资源并且不会停止对当前文档的处理。

这也就是为什么建议使用link方式加载css而不是使用@import方式。

#### src

src 表示引用资源，替换当前元素，用在 img，script，iframe 上，src 是页面内容不可缺少的一部分。

当浏览器解析到 src ，会暂停其他资源的下载和处理（图片不会暂停其他资源下载和处理），直到将该资源加载、编译、执行完毕，图片和框架等也如此，类似于将所指向资源应用到当前内容。这也是为什么建议把 js 脚本放在底部而不是头部的原因。

src（source）指向外部资源的位置，指向的内容将会嵌入到文档中当前标签所在位置；在请求src资源时会将其指向的资源下载并应用到文档中，如js脚本，img图片和iframe等元素。
当浏览器解析到该元素时，会暂停其他资源的下载和处理，直到将该资源加载、编译、执行完毕，类似于将所指向资源嵌入当前标签内。

[参考](https://blog.csdn.net/lhjuejiang/article/details/80795081)



### css引入方式

1.link
2.@import "style.css";/@import url("style.css")

(官方定义  import规则一定要先于除了@charset的其他任何css规则)
不建议使用@import的理由：

1.影响浏览器的并行下载

2.多个@import导致下载顺序紊乱



### 详解为什么要避免使用@import

如果使用css @import，这样会导致css无法并行下载，在使用@import引用的文件只有在引用它的那个css文件被下载、解析之后，浏览器才会知道还有另外一个css需要下载，这时才会去下载，然后下载后开始解析、构建渲染树（render tree）等一系列操作，因此css @import 引起的css解析延迟会加长页面留白期。所以，要尽量避免使用css @import而尽量采用link标签的方式引入。



### link和@import的详细区别？

1、link属于XHTML标签，除了加载css，还能用于定义RSS，定义rel链接属性等作用；而@import是CSS提供的，只能用于加载CSS。
2、页面被加载时，link会并行加载，而@import引用的CSS会等到页面被加载完再加载（详细如上。）
3、import是CSS2.1提出的，只在IE5以上才被识别，而linkXHTML标签无兼容问题；



### css、js的性能优化，从用户刷新网页开始，一次js请求一般情况下哪些地方会有缓存处理？

dns缓存，cdn缓存，浏览器缓存，服务器缓存。
（附：缓存介绍）

#### DNS（Domain Name System/域名解析系统）：

短时间内多次访问某个网址，系统会设计一个本地“dns缓存”，当第一次访问chenxixunhan.com，dns返回了正确的ip后，系统就会将这个结果临时存储起来，这就是dns缓存。它会有一个失效时间，在这时间内，当再次访问时，系统会从电脑本地的dns缓存中把结果交还给你，而不必再去询问dns服务器，变相“加速”了网址的解析。

#### CDN（Content Delivery Network/内容分发网络）

通过在不同地点缓存内容，然后通过负载平衡等技术将用户请求定向到最近的缓存服务器上获取内容，提高用户访问网站的响应速度。

#### 浏览器缓存

为了节约网络的资源加速浏览，浏览器在用户磁盘上对最近请求过的文档进行存储，当访问者再次请求这个页面时，浏览器就可以从本地磁盘显示文档，这样就可以加速页面的阅览。

#### web服务器缓存

Web缓存服务器的应用模式主要是正向代理和反向代理。正向代理(Proxy)模式是代理网络用户访问internet，客户端将本来要直接发送到internet上源服务器的连接请求发送给代理服务器处理。正向代理的目的是加速用户在使用浏览器访问Internet时的请求响应时间，并提高广域网线路的利用率。正向代理浏览器无需和该站点建立联系，只访问到Web缓存即可。通过正向代理，大大提高了后续用户的访问速度，使他们无需再穿越Internet，只要从本地Web缓存就可以获取所需要的信息，避免了带宽问题，同时可以大量减少重复请求在网络上的传输，从而降低网络流量，节省资费。
反向代理(Reverse Proxy)模式是针对Web服务器加速功能的，在该模式中，缓存服务器放置在web应用服务器的前面，当用户访问web应用服务器的时候，首先经过缓存服务器，并将用户的请求和应用服务器应答的内容写入缓存服务器中，从而为后续用户的访问提供更快的响应。



### `<table>`元素中的字体

CSS 中，对于 font 的属性都是可以继承的。怪异模式下，对于 table 元素，字体的某些元素将不会从 body 等其他封装元素继承中的得到，特别是 font-size 属性。



### img 上 title 与 alt

title 指图片的信息、alt 指图片不显示时显示的文字



### 以前端的角度出发做好SEO(Search Engine Optimization/搜索引擎优化)需要考虑什么？

1、了解搜索引擎如何抓取网页和如何索引网页。
2、meta标签优化
包括主题（title），网站描述（description），和关键字（keywords）。还有其它的隐藏文字如author（作者），category（目录），language（编码语种）等。
（拓展：meta？（元信息/meta-information））
meta元素可提供有关页面的元信息，如针对搜索引擎和更新频度的描述。
位于文档头部，一种辅助性的标签（详细：[https://zhidao.baidu.com/question/2052283721385566387.html](https://link.jianshu.com/?t=https://zhidao.baidu.com/question/2052283721385566387.html)）

​    3、如何选取关键词并在网页中放置关键词
​            搜索就得用关键词。关键词分析和选择是SEO最重要的工作之一。首先给网站确定关键词（一般在5个上下），然后针对这些关键字进行优化，包括关键词密度（Density），相关度（Relavacy），突出性（Prominency）等等。
​    4、了解主要的搜索引擎
​            对网站流量主要起决定作用的几个。
​            英文：Google，Yahoo，Bing等；
​            中文：百度，搜狗，有道等。
​            不同的搜索引擎对页面的抓取和索引、排序的规则都不一样。各搜索门户和搜索引擎的关系。
​    5、主要的互联网目录。
​    6、按点击付费的搜索引擎
​    7、搜索引擎登录
​    8、链接交换和链接广泛度
​    9、合理的标签使用（详细链接http://www.jb51.net/css/238279.html 第十六点）



### html5的新特性？处理html5标签的浏览器兼容问题？

htm5现在已经不是SGML的子集，主要关于图像、位置、存储，多任务等功能的增加；
1.绘画canvas；
2.用于媒介回放的video和audio
3.本地离线存储localStorage长期存储数据，浏览器关闭后数据不丢失。
4.sessionStorage的数据在浏览器关闭后自动删除；
5.语义化更好的内容元素，如article、footer、header、nav、section
6.表单控件，calendar、date、time、email、url、search；
7.新的计数webworker（多线程），websocket（双向通信），geolocation（地理定位）；（新的理解）

​    兼容性：
​            1.ie6~ie8支持通过document.createElement方法产生的标签,利用这一特性让这些浏览支持html5新标签，并需要添加默认样式。

   2. 使用成熟的框架如：html5shiv；

      ```
      <!--[if lt IE 9]>
      <script> src="http://html5shim.googlecode.com/svn/trunk/html5.js"</script>
      <![endif]-->
      ```



### 从输入url到网页最终展现到用户面前，中间发生了什么？

1、输入地址
2、浏览器查找域名的ip地址
（包括dns查找：浏览器缓存->系统缓存->路由器缓存）
dns查找过程如下：
1、浏览器缓存——浏览器会缓存dns记录一段时间，但是操作系统不会告诉浏览器存储dns的记录事件，所以不同浏览器会自固定一个时间（2~30分钟）；
2、系统缓存——如果在浏览器缓存里没有找到需要的记录，浏览器会做一个系统调用，以便获得系统缓存中的记录；
3、路由器缓存——接着，请求发向路由器，它一般会有自己的dns缓存；
4、ISP（网络服务提供商）DNS缓存——接下来检查ISP缓存DNS的服务器。这里一般能找到相应的缓存记录。
5、递归搜索——ISP的DNS服务器从根域名服务器开始进行递归搜索，从com顶级域名服务器到example的域名服务器。
3、浏览器给web服务器发送一个HTTP请求
请求中可能包含存储该域名的cookies，也会存储登录用户名和密码以及一些用户设置等。
4、HTTP（超文本传输协议）请求的建立
建立TCP（传输控制协议）链接：在HTTP工作开始之前，web浏览器首先要通过网络与web服务器建立连接，该连接通过TCP来完成的，该协议与IP协议共同构建Internet，即著名的TCP/IP协议族，因此Internet又被称作是TCP/IP网络。HTTP是比TCP更高层的应用层协议。根据规则只有低层协议建立之后，才能进行更高层协议的连接。因此，首先要建立TCP链接，一般TCP链接的端口号是80。在TCP/IP协议中，TCP协议提供可靠的连接服务，采用三次握手建立一个连接。
第一次握手：主机A发送位码syn=1，随机产生seq（sequence序列号） number=1234567的数据包到服务器，主机B由syn=1知道，A要求建立联机；
第二次握手：主机B收到请求后确认联机信息，向A发送ack（Acknowledgement 确认信息） number=(主机A的seq+1)，syn=1，ack=1.随机产生seq=7654321的包；
第三次握手：主机A收到后检查ack number是否正确，即第一次发送的seq number+1，以及位码syn是否为1，若正确，主机A会再发送ack number=（主机B的seq+1），ack=1；主机B收到后确认seq值与ack=1则链接建立成功。
完成三次握手，主机A与主机B开始传送数据。
一旦建立了TCP连接，web浏览器就会向web服务器发送请求命令。
浏览器发送其求命令之后，还要以头信息的形式向web服务器发送一些别的信息，之后浏览器发送一空白行来通知服务器，它已经结束了该头信息的发送。
5、服务器的永久重定向响应
服务器给浏览器响应一个301永久重定向响应，这样浏览器就会访问“[http://www.chenxixunhan.com/](https://link.jianshu.com/?t=http://www.chenxixunhan.com/)”而非"[http://chenxixunhan.com/](https://link.jianshu.com/?t=http://chenxixunhan.com/)"。
为什么要重定向而不直接发回用户想看到的网页内容？
其中一个原因跟搜索引擎排名相关。
如果一个页面有两个地址，就像“[http://www.chenxixunhan.com/](https://link.jianshu.com/?t=http://www.chenxixunhan.com/)”和"[http://chenxixunhan.com/](https://link.jianshu.com/?t=http://chenxixunhan.com/)"，搜索引擎会认为他们是两个网站，结果造成每一个的搜索链接都减少从而降低排名。而搜索引擎知道301永久重定向，会把访问带www的和不带www的地址归到同一个网站排名下。
还有一个原因是用不同的地址会造成缓存友好性变差。当一个页面有好几个名字时，它可能会在缓存里出现好几次。
HTTP/1.1 301 Moved Permanently
Cache-Control: private, no-store, no-cache, must-revalidate, post-check=0,
pre-check=0
Expires: Sat, 01 Jan 2000 00:00:00 GMT
Location: [HTTP://www.facebook.com/](https://link.jianshu.com/?t=HTTP://www.facebook.com/)
P3P: CP=”DSP LAW”
Pragma: no-cache
Set-Cookie: made_write_conn=deleted; expires=Thu, 12-Feb-2009 05:09:50 GMT;
path=/; domain=.facebook.com; httponly
Content-Type: text/html; charset=utf-8
X-Cnection: close
Date: Fri, 12 Feb 2010 05:09:51 GMT
Content-Length: 0
6、浏览器跟踪重定向地址
现在，浏览器知道了“[http://www.chenxixunhan.com/](https://link.jianshu.com/?t=http://www.chenxixunhan.com/)”才是要访问的正确地址，所以它会发送另一个获取请求也就是
GET [HTTP://www.facebook.com/](https://link.jianshu.com/?t=HTTP://www.facebook.com/) HTTP/1.1
Accept: application/x-ms-application, image/jpeg, application/xaml+xml, [...]Accept-Language: en-US
User-Agent: Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1; WOW64; [...]Accept-Encoding: gzip, deflate
Connection: Keep-Alive
Cookie: lsd=XW[...]; c_user=21[...]; x-referer=[...]Host: [www.facebook.com](https://link.jianshu.com/?t=http://www.facebook.com)
头信息以之前请求中的意义相同；
7、服务器“处理”请求
服务器接收到获取请求，然后处理返回一个响应。
8、服务器发回一个HTML响应
HTTP/1.1 200 OKCache-Control: private, no-store, no-cache, must-revalidate, post-check=0,pre-check=0Expires: Sat, 01 Jan 2000 00:00:00 GMTP3P: CP=”DSP LAW”Pragma: no-cacheContent-Encoding: gzipContent-Type: text/html; charset=utf-8X-Cnection: closeTransfer-Encoding: chunkedDate: Fri, 12 Feb 2010 09:05:55 GMT 2b3Tn@[...]整个响应大小为35kB，其中大部分在整理后以blob（二进制）类型传输。
内容编码头告诉浏览器整个响应体用gzip算法进行压缩。解压blob块后，你可以看到html文档。
关于压缩，头信息说明了是否缓存这个页面，如果缓存的话如何去做，有什么cookies要去设置（前面响应没有这点）和隐私信息等等。
注意：报头中把Content-type设置为“text/html”。报头让浏览器将该响应内容以HTML形式呈现，而不是以文件格式下载它。浏览器会根据报头信息决定如何解释该响应，不过同时也会考虑像URL扩展内容等其他因素。
9、浏览器开始显示HTML
在浏览器没有完整接受全部HTML文档时，它就开始显示这个页面了。
10、浏览器发送获取嵌入在HTML中的对象
在浏览器显示HTML时，它会注意到需要获取其它地址内容的标签。这时，浏览器会发送一个获取请求来重新获得这些文件。
下面几个是一个叫雷锋的作者访问facebook.com时需要重获取的几个URL
\* 图片
[HTTP://static.ak.fbcdn.net/rsrc.php/z12E0/hash/8q2anwu7.gif](https://link.jianshu.com/?t=HTTP://static.ak.fbcdn.net/rsrc.php/z12E0/hash/8q2anwu7.gif)
[HTTP://static.ak.fbcdn.net/rsrc.php/zBS5C/hash/7hwy7at6.gif](https://link.jianshu.com/?t=HTTP://static.ak.fbcdn.net/rsrc.php/zBS5C/hash/7hwy7at6.gif)
…* CSS 式样表
[HTTP://static.ak.fbcdn.net/rsrc.php/z448Z/hash/2plh8s4n.css](https://link.jianshu.com/?t=HTTP://static.ak.fbcdn.net/rsrc.php/z448Z/hash/2plh8s4n.css)
[HTTP://static.ak.fbcdn.net/rsrc.php/zANE1/hash/cvtutcee.css](https://link.jianshu.com/?t=HTTP://static.ak.fbcdn.net/rsrc.php/zANE1/hash/cvtutcee.css)
…* JavaScript 文件
[HTTP://static.ak.fbcdn.net/rsrc.php/zEMOA/hash/c8yzb6ub.js](https://link.jianshu.com/?t=HTTP://static.ak.fbcdn.net/rsrc.php/zEMOA/hash/c8yzb6ub.js)
[HTTP://static.ak.fbcdn.net/rsrc.php/z6R9L/hash/cq2lgbs8.js](https://link.jianshu.com/?t=HTTP://static.ak.fbcdn.net/rsrc.php/z6R9L/hash/cq2lgbs8.js)

​            这些地址都要经历一个和HTML读取类似的过程。所以浏览器会在DNS查找这些域名，发送请求，重定向等等。
​            但不像动态页面那样，静态文件会允许浏览器对其进行缓存。有的文件可能不需要与服务器通讯，而从缓存中直接读取。服务器的相应中包含了静态文件保存的期限信息，所以浏览器知道要把它们缓存多长时间。还有，每个响应度可能包含像版本号一样的ETag（电子标签）头（被请求变量的实体值），如果浏览器观察到文件的版本ETag信息已经存在，就马上停止这个文件的传输。
11、浏览器发送异步（Ajax）请求
​            在web2.0伟大精神的指引下，页面显示完成后客户仍与服务器端保持着联系。
​            以Facebook聊天功能为例，它会持续与服务器保持联系来及时更新你那写亮亮灰灰的好友状态。
​            为了更新这些头像亮着的好友状态，在浏览器中执行的javascript代码服务器发送异步请求。这个异步请求发送给特定的地址，它是一个按照程式构造的获取或发送请求。
​            facebook聊天功能提供了关于ajax一个有意思的问题案例：把数据从服务器端推送到客户端，因为HTTP是一个请求-响应协议，所以聊天服务器不能把新消息发给客户。取而代之的是客户端不得不隔几秒就轮询下服务器端看自己有没有新消息。
​            这些情况发生时长轮询是个减轻服务器负载挺有趣的技术。如果当被轮询时服务器没有新消息，它就不理这个客户端。而当尚未超时的情况下收到了该客户的新消息，服务器就会找到未完成的请求，把新消息作为响应返回给客户端。
​            （源自：http://www.qdfuns.com/notes/15102/a5bee6b87d22ab0ecb28101f385db2e4.html）

​            （拓展：请求url响应返回状态代码及其文本描述？（详情：D:\notes_web_book\HTTP协议详解.pdf））
​                    状态代码由三位数字组成，第一个数字定义了响应的类别，且有五种可能取值：
​                            1xx：指示信息--表示请求已接收，继续处理
​                            2xx：成功--表示请求已被成功接收、理解、接受
​                            3xx：重定向--要完成请求必须进行更进一步的操作
​                            4xx：客户端错误--请求有语法错误或请求无法实现
​                            5xx：服务器端错误--服务器未能实现合法的请求

​                    常见状态代码、状态描述说明：
​                            200 OK //客户端请求成功
​                            400 Bad Request //客户端请求有语法错误，不能被服务器所理解
​                            401 Unauthorized //请求未经授权，这个状态代码必须和WWW-Authenticate报头域一起使用
​                            403 Forbidden //服务器收到请求，但是拒绝提供服务
​                            404 Not Found //请求资源不存在，eg：输入了错误的 URL
​                            500 Internal Server Error //服务器发生不可预期的错误
​                            503 Server Unavailable //服务器当前不能处理客户端的请求，一段时间后，可能恢复正常
​                            eg：HTTP/1.1 200 OK



### 请描述下 SEO 中的 TDK？

答案：在 SEO 中，所谓的 TDK 其实就是 title、description、keywords 这三个标签，title 标题标签，description 描述标签，keywords 关键词标签



### 严格模式与混杂模式

严格模式：以浏览器支持的最高标准运行

混杂模式：页面以宽松向下兼容的方式显示，模拟老式浏览器的行为



### 列举 IE 与其他浏览器不一样的特性？

a. IE 的排版引擎是 Trident （又称为 MSHTML）

b. Trident 内核曾经几乎与 W3C 标准脱节（2005 年）

c. Trident 内核的大量 Bug 等安全性问题没有得到及时解决

d. JS 方面，有很多独立的方法，例如绑定事件的 attachEvent、创建事件的 createEventObject 等

e. CSS 方面，也有自己独有的处理方式，例如设置透明，低版本 IE 中使用滤镜的方式



### 为什么用多个域名存储网站资源更有效？

1、CDN 缓存更方便

2、突破浏览器并发限制

3、节约 cookie 带宽

4、节约主域名的连接数，优化页面响应速度

5、防止不必要的安全问题



### 页面可见性（Page Visibility API） 可以有哪些用途？

这个新的 API 的意义在于，通过监听网页的可见性，可以预判网页的卸载，还可以用来节省资源，减缓电能的消耗。比如，一旦用户不看网页，下面这些网页行为都是可以暂停的。

​    （1）对服务器的轮询
​    （2）网页动画
​    （3）正在播放的音频或视频

- 通过 visibilityState 的值检测页面当前是否可见，以及打开网页的时间等;

* 在页面被切换到其他后台进程的时候，自动暂停音乐或视频的播放
* 当用户浏览其他页面，暂停网站首页幻灯自动播放
* 完成登陆后，无刷新自动同步其他页面的登录状态

#### 页面可见性： 

就是对于用户来说，页面是显示还是隐藏, 所谓显示的页面，就是我们正在看的页面；隐藏的页面，就是我们没有看的页面。 因为，我们一次可以打开好多标签页面来回切换着，始终只有一个页面在我们眼前，其他页面就是隐藏的，还有一种就是.........，(把浏览器最小化，所有的页面就都不可见了)。

API 很简单，document.hidden 就返回一个布尔值，如果是 true, 表示页面可见，false 则表示，页面隐藏。 不同页面之间来回切换，触发 visibilitychange 事件。 还有一个 document.visibilityState, 表示页面所处的状态，取值：visible, hidden 等四个。

```js
document.addEventListener("visibilitychange", function() \\{
  if (document.hidden) \\{
    document.title = "hidden";
  \\} else \\{
    document.title = "visibile";
  \\}
\\});
```

我们打开这个页面，然后再打开另一个页面，来回点击这两个页面，当我们看到这个页面时，标题显示 visiable ,当我们看另一个页面时，标题显示 hidden;

动画，视频，音频都可以在页面显示时打开，在页面隐藏时关闭

解析：[参考](https://www.cnblogs.com/king18181753985/p/6510315.html)

详细资料可以参考：[《Page Visibility API 教程》](http://www.ruanyifeng.com/blog/2018/10/page_visibility_api.html)



### Quirks(怪癖）模式是什么？它和 Standards（标准）模式有什么区别

1 以 ie6 为例，如果写了 DTD，就意味着这个页面将采用对 CSS 支持更好的布局，而如果没有，则采用兼容之前的布局方式。这就是 Quirks 模式（怪癖模式，诡异模式，怪异模式）。

2 区别：总体会有布局、样式解析和脚本执行三个方面的区别。

设置一个元素的宽度和高度

给`<span>`等行内元素设置 width 和 height

用 margin:0 auto 设置水平居中

从 IE6 开始，引入了 Standards 模式，标准模式中，浏览器尝试给符合标准的文档在规范上的正确处理达到在指定浏览器中的程度。

在 IE6 之前 CSS 还不够成熟，所以 IE5 等之前的浏览器对 CSS 的支持很差， IE6 将对 CSS 提供更好的支持，然而这时的问题就来了，因为有很多页面是基于旧的布局方式写的，而如果 IE6  支持 CSS 则将令这些页面显示不正常，如何在即保证不破坏现有页面，又提供新的渲染机制呢？

在写程序时我们也会经常遇到这样的问题，如何保证原来的接口不变，又提供更强大的功能，尤其是新功能不兼容旧功能时。遇到这种问题时的一个常见做法是增加参数和分支，即当某个参数为真时，我们就使用新功能，而如果这个参数   不为真时，就使用旧功能，这样就能不破坏原有的程序，又提供新功能。IE6 也是类似这样做的，它将 DTD（文档类型定义）当成了这个“参数”，因为以前的页面大家都不会去写 DTD，所以 IE6 就假定   如果写了 DTD，就意味着这个页面将采用对 CSS 支持更好的布局，而如果没有，则采用兼容之前的布局方式。这就是 Quirks 模式（怪癖模式，诡异模式，怪异模式）。

区别：

总体会有布局、样式解析和脚本执行三个方面的区别。

盒模型：在 W3C 标准中，如果设置一个元素的宽度和高度，指的是元素内容的宽度和高度，而在 Quirks  模式下，IE 的宽度和高度还包含了 padding 和 border。

设置行内元素的高宽：在 Standards 模式下，给`<span>`等行内元素设置 wdith 和 height 都不会生效，而在 quirks 模式下，则会生效。

设置百分比的高度：在 standards 模式下，一个元素的高度是由其包含的内容来决定的，如果父元素没有设置百分比的高度，子元素设置一个百分比的高度是无效的

用 margin:0 auto 设置水平居中：使用 margin:0 auto 在 standards 模式下可以使元素水平居中，但在 quirks 模式下却会失效。

（还有很多，答出什么不重要，关键是看他答出的这些是不是自己经验遇到的，还是说都是看文章看的，甚至完全不知道。）



### div+css 的布局较 table 布局有什么优点？

答案：分离 方便改版 快清晰简洁 seo

1.改版的时候更方便 只要改 css 文件。

2.页面加载速度更快、结构化清晰、页面显示简洁。

3.表现与结构相分离。

4.易于优化（seo）搜索引擎更友好，排名更容易靠前。



###  知道什么是微格式吗？谈谈理解。在前端构建中应该考虑微格式吗？

答案：微格式（Microformats）是一种让机器可读的语义化 XHTML 词汇的集合，是结构化数据的开放标准。是为特殊应用而制定的特殊格式。

优点：将智能数据添加到网页上，让网站内容在搜索引擎结果界面可以显示额外的提示。（应用范例：豆瓣，有兴趣自行 google）



### webSocket 如何兼容低版本浏览器？

答案：对于低端不支持 websocket 的浏览器，一般有几个解决方案

1. 使用轮询或长连接的方式实现伪 websocket 的通信
2. 使用 flash 或其他方法实现一个 websocket 客户端 ：

[参考](https://segmentfault.com/q/1010000005000671/a-1020000005003936)
[参考](https://blog.csdn.net/u011925826/article/details/17532465)



### 前端需要注意哪些 SEO

1. 合理的 title、description、keywords：搜索对着三项的权重逐个减小，title 值强调重点即可，重要关键词出现不要超过 2 次，而且要靠前，不同页面 title 要有所不同；description 把页面内容高度概括，长度合适，不可过分堆砌关键词，不同页面 description 有所不同；keywords 列举出重要关键词即可
2. 语义化的 HTML 代码，符合 W3C 规范：语义化代码让搜索引擎容易理解网页
3. 重要内容 HTML 代码放在最前：搜索引擎抓取 HTML 顺序是从上到下，有的搜索引擎对抓取长度有限制，保证重要内容一定会被抓取
4. 重要内容不要用 js 输出：爬虫不会执行 js 获取内容
5. 少用 iframe：搜索引擎不会抓取 iframe 中的内容
6. 非装饰性图片必须加 alt
7. 提高网站速度：网站速度是搜索引擎排序的一个重要指标

解析：[参考](https://www.cnblogs.com/passkey/p/10081589.html)



### HTML 全局属性(global attribute)有哪些

- accesskey:设置快捷键，提供快速访问元素如<a href="#" accesskey="a">aaa</a>在 windows 下的 firefox 中按 alt + shift + a 可激活元素
- class:为元素设置类标识，多个类名用空格分开，CSS 和 javascript 可通过 class 属性获取元素
- contenteditable: 指定元素内容是否可编辑
- contextmenu: 自定义鼠标右键弹出菜单内容
- data-\*: 为元素增加自定义属性
- dir: 设置元素文本方向
- draggable: 设置元素是否可拖拽
- dropzone: 设置元素拖放类型： copy, move, link
- hidden: 表示一个元素是否与文档。样式上会导致元素不显示，但是不能用这个属性实现样式效果
- id: 元素 id，文档内唯一
- lang: 元素内容的的语言
- spellcheck: 是否启动拼写和语法检查
- style: 行内 css 样式
- tabindex: 设置元素可以获得焦点，通过 tab 可以导航
- title: 元素相关的建议信息
- translate: 元素和子孙节点内容是否需要本地化

解析：[参考](https://funteas.com/topic/5906a8bc8783c1370b809c2a)



### meta viewport 原理是什么？

答案：meta viewport 标签的作用是让当前 viewport 的宽度等于设备的宽度，同时不允许用户进行手动缩放

viewportde 原理：移动端浏览器通常都会在一个比移动端屏幕更宽的虚拟窗口中渲染页面，这个虚拟窗口就是 viewport; 目的是正常展示没有做移动端适配的网页，让他们完整的展示给用户；

解析：Viewport ：字面意思为视图窗口，在移动 web 开发中使用。表示将设备浏览器宽度虚拟成一个特定的值（或计算得出），这样利于移动 web 站点跨设备显示效果基本一致。移动版的 Safari 浏览器最新引进了 viewport 这个 meta tag，让网页开发者来控制 viewport 的大小和缩放，其他手机浏览器也基本支持。

在移动端浏览器当中，存在着两种视口，一种是可见视口（也就是我们说的设备大小），另一种是视窗视口（网页的宽度是多少）。
举个例子：如果我们的屏幕是 320 像素 \* 480 像素的大小（iPhone4），假设在浏览器中，320 像素的屏幕宽度能够展示 980 像素宽度的内容。那么 320 像素的宽度就是可见视口的宽度，而能够显示的 980 像素的宽度就是视窗视口的宽度。

为了显示更多的内容，大多数的浏览器会把自己的视窗视口扩大，简易的理解，就是让原本 320 像素的屏幕宽度能够容下 980 像素甚至更宽的内容（将网页等比例缩小）。



### Viewport 属性值

- width 设置 layout viewport 的宽度，为一个正整数，或字符串"width-device"
- initial-scale 设置页面的初始缩放值，为一个数字，可以带小数
- minimum-scale 允许用户的最小缩放值，为一个数字，可以带小数
- maximum-scale 允许用户的最大缩放值，为一个数字，可以带小数
- height 设置 layout viewport 的高度，这个属性对我们并不重要，很少使用
- user-scalable 是否允许用户进行缩放，值为"no"或"yes", no 代表不允许，yes 代表允许这些属性可以同时使用，也可以单独使用或混合使用，多个属性同时使用时用逗号隔开就行了。



### Canvas 和 SVG 有什么区别？

Canvas 和 SVG 都允许您在浏览器中创建图形，但是它们在根本上是不同的。

#### Canvas

描述：Canvas 元素用于在网页上绘制图形，该元素标签强大之处在于可以直接在 HTML 上进行图形操作。

- 通过 Javascript 来绘制 2D 图形。
- 是逐像素进行渲染的。
- 在 canvas 中，一旦图形被绘制完成，它就不会继续得到浏览器的关注。如果其位置发生变化，那么整个场景也需要重新绘制，包括任何或许已被图形覆盖的对象。

- 依赖分辨率
- 不支持事件处理器
- 弱的文本渲染能力
- 能够以 .png 或 .jpg 格式保存结果图像
- 最适合图像密集型的游戏，其中的许多对象会被频繁重绘

### SVG

一种使用 XML 描述的 2D 图形的语言

SVG 基于 XML 意味着，SVG DOM 中的每个元素都是可用的，可以为某个元素附加 Javascript 事件处理器。
在 SVG 中，每个被绘制的图形均被视为对象。如果 SVG 对象的属性发生变化，那么浏览器能够自动重现图形。

- 不依赖分辨率
- 支持事件处理器
- 最适合带有大型渲染区域的应用程序（比如谷歌地图）
- 复杂度高会减慢渲染速度（任何过度使用 DOM 的应用都不快）
- 不适合游戏应用



### 为什么最好把 CSS 的`<link>`标签放在`<head></head>`之间？

把`<link>`标签放在`<head></head>`之间是规范要求的内容。此外，这种做法可以让页面逐步呈现，提高了用户体验。将样式表放在文档底部附近，会使许多浏览器（包括 Internet Explorer）不能逐步呈现页面。一些浏览器会阻止渲染，以避免在页面样式发生变化时，重新绘制页面中的元素。这种做法可以防止呈现给用户空白的页面或没有样式的内容。



### 为什么最好把 JS 的`<script>`标签恰好放在`</body>`之前，有例外情况吗？

脚本在下载和执行期间会阻止 HTML 解析。把`<script>`标签放在底部，保证 HTML 首先完成解析，将页面尽早呈现给用户。

例外情况是当你的脚本里包含`document.write()`时。但是现在，`document.write()`不推荐使用。同时，将`<script>`标签放在底部，意味着浏览器不能开始下载脚本，直到整个文档（document）被解析。也许，对此比较好的做法是，`<script>`使用`defer`属性，放在`<head>`中。



### DOM结构 —— 两个节点之间可能存在哪些关系以及如何在节点之间任意移动。

（[通俗易懂的来讲讲DOM](http://www.cnblogs.com/season-huang/p/4322451.html)、[两个节点之间可能存在哪些关系以及如何在节点之间任意移动](https://www.jianshu.com/p/e45821392c8c)）

DOM: Document Object Module, 文档对象模型。

节点的关系：父（parent）、子（child）和同胞（sibling）等节点关系；

\- 在节点树中，顶端节点被称为根（root）

\- 每个节点都有父节点、除了根（它没有父节点）

\- 一个节点可拥有任意数量的子

\- 同胞是拥有相同父节点的节点



![img](https://upload-images.jianshu.io/upload_images/11446313-95107bc0d94c56f2.jpg?imageMogr2/auto-orient/strip|imageView2/2/w/572/format/webp)



### DOM操作 —— 如何添加、移除、移动、复制、创建和查找节点等

#### 查找DOM：

document.**getElementById**()和document.**getElementsByTagName**()，以及CSS选择器document.**getElementsByClassName**()；**querySelector**()和**querySelectorAll**()【低版本的IE<8不支持，8有限支持】。

document.getElementById()可以直接定位唯一的一个DOM节点。

document.getElementsByTagName()和document.getElementsByClassName()总是返回一组DOM节点。

#### 创建DOM：

document.**createElement**(newElement)；

#### 更新DOM：

innerHTML和innerText、textContent；

#### 插入DOM：

innerHTML 和 parentNode.**appendChild**(childNode)，parentElement.**insertBefore**(newElement, referenceElement)；

#### 删除DOM：

parent.**removeChild**(childElement)；



### XMLHttpRequest —— 这是什么、怎样完整地执行一次GET请求、怎样检测错误。

（老版本IE ajax核心对象为ActiveXObject）

XMLHttpRequest 对象提供了在网页加载后与服务器进行通信的方法。

获取ajax核心对象：

```
var request = false;
　try \\{
　　request = new XMLHttpRequest();
　\\} catch (trymicrosoft) \\{
　　try \\{
　　　request = new ActiveXObject("Msxml2.XMLHTTP");
　　\\} catch (othermicrosoft) \\{
　　　try \\{
　　　　request = new ActiveXObject("Microsoft.XMLHTTP");
　　　\\} catch (failed) \\{
　　　　request = false;
　　　}}}
```



### 严格模式与混杂模式 —— 如何触发这两种模式，区分它们有何意义

DOCTYPE（是Document Type文档类型的简写）是一组机器可读的规则，它们指示(X)HTML文档中允许有什么，不允许有什么，DOCTYPE正是用来告诉浏览器使用哪种DTD，三种 DTD 类型分别是严格版本、过渡版本以及基于框架的 HTML 文档。声明位于文档中的最前面的位置，处于标签之前。如果DOCTYPE声明不是页面上的第一个元素，那么IE 6会自动切换到混杂模式。

严格模式是浏览器根据web标准去解析页面，是一种要求严格的DTD，不允许使用任何表现层的语法，如<br/>
。混杂模式则是一种向后兼容的解析方法，就是可以实现IE5.5以下版本浏览器的渲染模式。

总结：

（1） <!DOCTYPE>声明位于文档中的最前面，处于标签之前。告知浏览器的解析器，用什么文档类型规范来解析这个文档。

（2）严格模式的排版和 JS 运作模式是  以该浏览器支持的最高标准运行。

（3）在混杂模式中，页面以宽松的向后兼容的方式显示。模拟老式浏览器的行为以防止站点无法工作。

（4）DOCTYPE不存在或格式不正确会导致文档以混杂模式呈现。



### 盒模型 —— 外边距、内边距和边框之间的关系，及IE8以下版本的浏览器中的盒模型

***CSS 盒子模型(Box Model)***

所有HTML元素可以看作盒子，在CSS中，"box model"这一术语是用来设计和布局时使用。

CSS盒模型本质上是一个盒子，封装周围的HTML元素，它包括：边距，边框，填充，和实际内容。

盒模型允许我们在其它元素和周围元素边框之间的空间放置元素。

**属性：**box-sizing；

**属性值1：**box-sizing：border-box；标准盒子模型——元素的内边距和边框不再会增加它的宽度，即元素宽度width包含了元素的内边距padding和边框宽度border-width，元素内容宽度 = width - padding - border；

**属性值2：**box-sizing： content-box；（默认值）IE盒子模型（怪异盒模型）——元素的内边距和边框会增加它的宽度，即元素实际宽度等于width加上元素的内边距padding和边框宽度border-width，元素内容宽度 = width；（IE8以下浏览器的盒模型中定义的元素的宽高不包括内边距和边框）



### 块级元素与行内元素 —— 怎么用CSS控制它们、以及如何合理的使用它们（[参考链接](https://jeffjade.com/2015/06/24/2015-06-24-css-block-inline/)）

（1）CSS规范规定，每个元素都有display属性，比如div默认display属性值为“block”，成为“块级”元素，总是独占一行，表现为另起一行开始，而且其后的元素也必须另起一行显示；span默认display属性值为“inline”，是“行内”元素，可以和相邻的内联元素在同一行。

（2）行内元素

```
a b span img input select strong···
```

（3）块级元素有

```
div ul ol li dl dt dd h1 h2 h3 h4…p 
```

（4）知名的空元素

```
 <br/>，<hr/>  <img/>  <input/>  <link> <meta>
 // 鲜为人知的是：
 <area> <base> <command> <col> <embed>  <keygen>  <param> <source>   <track>  <wbr>
```

  

### 浮动元素 —— 怎么使用它们、它们有什么问题以及怎么解决这些问题。

属性：**float**；

属性值：**left**：往左浮动；**right**：往右浮动；

浮动元素引起的问题：

1.父元素的高度无法被撑开，影响与父元素同级的元素；

2.与浮动元素同级的非浮动元素会跟随其后；

3.若非第一个元素浮动，则该元素之前的元素也需要浮动，否则会影响页面显示的结构；

解决方法：

清浮动，使用CSS中的**clear:both;**属性来清除同级子元素的浮动问题

给父元素添加clearfix样式，解决父元素高度无法撑开问题：

```
.clearfix:after \\{
    content: "";
    display: block;
    clear: both;
\\}
```

（[参考链接](http://www.w3school.com.cn/css/css_positioning_floating.asp)）



### HTML与XHTML —— 二者有什么区别，你觉得应该使用哪一个并说出理由

**主要区别：**HTML是一种基本的WEB网页设计语言，XHTML是一个基于XML的置标语言；

XHTML元素必须被正确地嵌套；

XHTML元素必须被关闭；

标签名必须用小写字母；

XHTML文档必须拥有根元素。



### JSON —— 作用、用途、设计结构

JSON(JavaScript Object Notation) 是一种轻量级的数据交换格式。易于人阅读和编写。同时也易于机器解析和生成。

JSON建构于两种结构：“名称/值”对的集合（A collection of name/value pairs）。

不同的语言中，它被理解为对象（object）、纪录（record）、结构（struct）、字典（dictionary）、哈希表（hash table）、有键列表（keyed list）或者[关联数组](https://www.baidu.com/s?wd=关联数组&tn=44039180_cpr&fenlei=mv6quAkxTZn0IZRqIHckPjm4nH00T1YLm17WPhc1uHu9nj0vnAFh0ZwV5Hcvrjm3rH6sPfKWUMw85HfYnjn4nH6sgvPsT6KdThsqpZwYTjCEQLGCpyw9Uz4Bmy-bIi4WUvYETgN-TLwGUv3EPjcYPHnvPHbLPWmkPjR3PWRz)（associative array）、值的有序列表（An ordered list of values）。在大部分语言中，它被理解为数组（array）。
