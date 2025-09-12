---
title: BOM
date: 2019-10-08 15:38:24
categories: 
- 前端知识
tags:
- BOM
- window对象
---

### BOM是什么

BOM由一系列相关的对象构成，并且每个对象都提供了很多方法与属性，由于BOM主要用于管理窗口与窗口之间的通讯，因此其核心对象是window；

前端BOM（Browser Object Model，浏览器对象模型）是Web编程中一个非常重要的概念。它是一组对象和方法的集合，允许JavaScript访问并操作浏览器窗口及其相关功能。BOM提供了一种方式让网页能够与用户进行交互，并且可以控制浏览器的行为。下面将对BOM中的关键对象及它们的功能做详细介绍。

#### 核心对象：`window`

- **全局对象**：在浏览器环境中，`window`对象是最顶层的对象，所有的其他BOM对象都是它的属性。同时，它也是全局作用域的代表，这意味着在全局作用域内声明的所有变量和函数都会成为`window`对象的属性。
- **文档加载事件**：可以通过`window.onload`监听整个页面加载完成的事件。
- **定时器**：使用`setTimeout()`和`setInterval()`设置一次性或周期性的任务；相应的`clearTimeout()`和`clearInterval()`用于取消这些定时器。
- **弹出对话框**：`alert()`, `confirm()`, 和 `prompt()` 用来显示警告信息、确认对话框以及输入提示框。
- **位置控制**：`scrollTo()`和`scrollBy()`控制页面滚动；`moveTo()`和`moveBy()`改变窗口的位置。
- **打开/关闭窗口**：`open()`创建新浏览器窗口；`close()`关闭当前窗口。
- **尺寸获取**：`innerWidth`, `innerHeight`获取视口大小；`outerWidth`, `outerHeight`获取浏览器窗口大小（包括边框等）。
- **屏幕信息**：通过`screen`属性获取屏幕相关信息，如分辨率。

#### 其他重要对象

- **`navigator`**：包含关于浏览器的信息，比如`userAgent`、`platform`、支持的语言列表等。
- **`location`**：表示当前URL信息，并提供了导航到新页面的方法，例如`href`、`assign()`、`reload()`。
- **`history`**：允许脚本读取会话历史记录并导航到之前的页面，方法有`back()`、`forward()`、`go()`。
- **`screen`**：提供用户的屏幕细节，如宽度、高度、颜色深度等。
- **`document`**：虽然严格来说属于DOM的一部分，但它是`window`的一个属性，因此通常也归类于BOM讨论范围内。它代表了加载进浏览器窗口的HTML文档。

### BOM 常用对象

 1、window对象 ，是JS的最顶层对象，其他的BOM对象都是window对象的属性；
 2、document对象，文档对象；
 3、location对象，浏览器当前URL信息；
 4、navigator对象，浏览器本身信息；
 5、screen对象，客户端屏幕信息；
 6、history对象，浏览器访问历史信息；

#### 注意事项

由于BOM不是由W3C或其他标准化组织正式定义的标准，不同的浏览器可能会有不同的实现细节。因此，在开发时需要考虑跨浏览器兼容性问题。随着现代浏览器标准逐渐统一，这种差异已经减少了许多，但仍需保持警惕以确保代码能在各种环境下正常工作。







# window对象

#### window对象属性

| 属性          | 描述                             | 可读写性 | 兼容性 |
| ------------- | -------------------------------- | -------- | ------ |
| innerWidth    | 浏览器窗口宽度                   | 只读     | >ie8   |
| innerHeight   | 浏览器窗口高度                   | 只读     | >ie8   |
| screen.width  | 屏幕宽度(分辨率)                 | 只读     | 全部   |
| screen.height | 屏幕高度(分辨率)                 | 只读     | 全部   |
| top           | 返回窗口体系中的最顶层窗口的引用 | 只读     | 全部   |

#### window对象方法

| 属性     | 参数      | 返回值                 | 功能                                           | 兼容性 |
| -------- | --------- | ---------------------- | ---------------------------------------------- | ------ |
| alert    | string    | undefined              | 弹出带有一段消息和一个确认按钮的警告框         | 全部   |
| confirm  | string    | boolean                | 弹出带有一段消息以及确认按钮和取消按钮的对话框 | 全部   |
| prompt   | string    | undefined              | 弹出可提示用户输入的对话框                     | 全部   |
| open     | url       | 新窗口的window对象引用 | 通过脚本打开新的窗口                           | 全部   |
| close    | 无        | undefined              | 关闭当前浏览器窗口                             | 全部   |
| scrollBy | xpos,ypos | undefined              | 在窗口中按指定的偏移量滚动文档                 | 全部   |
| scrollTo | xpos,ypos | undefined              | 在窗口中将文档滚动到指定位置                   | 全部   |

#### 定时器

| 属性          | 参数                        | 返回值                           | 功能                                                 | 兼容性                                |
| ------------- | --------------------------- | -------------------------------- | ---------------------------------------------------- | ------------------------------------- |
| setInterval   | `callback,time(ms)[,param]` | 该时间函数的id值，可用于取消执行 | 按照指定时间间隔执行回调函数  **一直执行，直到清除** | 全部(IE9及一下版本不支持该第三个参数) |
| clearInterval | name                        | undefined                        | 清除指定时间函数进程                                 | 全部                                  |
| setTimeout    | `callback,time(ms)[,param]` | 该时间函数的id值，可用于取消执行 | 在指定的时间后执行回调函数   **只执行一次**          | 全部                                  |
| clearTimeout  | name                        | undefined                        | 清除指定的延时函数进程                               | 全部                                  |

`setInterval` 与 `clearTimeout`参数分别是

1. callback： 必填。 函数，代表指定时间后执行该段代码
2. time： 必填。 时间间隔，以毫秒计，不写单位
3. param： 可选。传给执行函数的其他参数，多个参数以`,`隔开(IE9 及其更早版本不支持该参数)



### 窗口关系及框架

- window.frame[0]
- window.frame['topFrame']
- window.parent
- window.top
- top.frame[0]
- 特别注意跨域问题



### 窗口位置

#### screenLeft screenTop screenX screenY

- IE Safari Opear Chrome 提供了 screenLeft 和 screenTop属性，分别用于表示窗口相对于屏幕左边和上边
- Firefox在screenX和screenY属性中提供了相同的窗口位置信息，Safari和Chrome也同时支持这两个属性。Opera虽然也支持screenX和screenY属性，单与screenLeft和screenTop并不对应。
- 兼容代码

```javascript
var leftPos = ( typeof window.screenLeft === "number" ) ? window.screenLeft : window.screenX;
var topPos = ( typeof window.screenTop === "number" ) ? window.screenTop : window.screenY;
```

- 但是 仍然会有些计算不精确的小问题 浏览器的问题

#### moveTo moveBy

- 将窗口精确地移动到一个新位置
- moveTo 接受两个参数， 新位置的X,Y值
- moveBy 接收的是在水平和垂直方向上移动的像素数
- 但是这两个方法可能被浏览器禁用



### 窗口大小

> 跨浏览器确定窗口大小不是一件简单的事情

#### 获取可视区域大小

- IE9+ Firefox Safari Opera 和 Chrome均为此提供了四个属性—— `innerWidth`、 `innerHeight`、 `outerWidth`、 `outerHeight`
- 在IE9+ Safari 和 Firefox中， outerWidth 和 outerHeight返回浏览器窗口本身的尺寸（无论从最外层的window对象还是从某个框架访问）。
- 在Opera中，这两个属性的值表示页面视图容器的大小（无论是从最外层的window对象还是从某个框架访问）
- 在Opera中，这两个属性的值表示页面视图容器的大小。而innerWidth和innerHeight则表示该容器中页面视图区的大小（减去边框宽度）。
- 在Chrome中，outerWidth、outerHeight与innerWidth、innerHeight返回相同的值，即视口（viewport）大小而非浏览器窗口大小
- IE8及更糟的版本没有提供取得当前浏览器窗口尺寸的属性。不过，它通过DOM提供了页面可见区域的相关信息。
- 在IE Firefox Safari Opera 和 Chrome中，`document.documentElement.clientWidth` 和 `document.documentElement.clientHeight`中保存了页面视口的信息。
- 在IE6中， 这些属性必须在标准模式下才有效。如果是混杂模式，就必须通过`document.body.clientWidth`和`document.body.clientHeight`取得相同信息。
- 而对于混杂模式下的Chrome，则无论通过`document.documentElement`还是`document.body`中的`clientWidth`和`clientHeight`属性，都可以取得视口大小。
- 虽然最终无法确定浏览器窗口本身的大小，但却可以取得页面视口大小。

```javascript
var pageWidth = window.innerWidth,
    pageHeight = window.innerHeight;
if( typeof pageWidth != "number" )\\{
    if( document.compatMode == "CSS1Compat" )\\{
        pageWidth = document.documentElement.clientWidth;
        pageHeight = document.documentElement.clientHeight;
    \\} else \\{
        pageWidth = document.body.clientWidth;
        pageHeight = document.body.clientHeight;
    \\}
\\}    
```

#### 调整浏览器窗口大小

- resizeTo() 接收浏览器窗口的新宽度和新高度
- resizeABy() 接收新窗口与原窗口的宽度和高度之差
- 只能在最外层window对象使用 IE7及更高版本中默认是金庸的

#### 弹出关闭窗口

- window.open 详细参数看mdn
- window.close 一般是通过JS或者用户点击打开的才会执行
- 检测window.open的返回值可以确定弹出窗口是否被屏蔽
  1. 如果浏览器内置的屏蔽程序阻止的弹出窗口，那么window.open()很可能返回null
  2. 如果浏览器扩展或其他程序阻止弹出窗口，那么window.open()通常会抛出一个错误



### 关于 IE 的 window 对象表述正确的有：

```
A. window.opener属性本身就是指向window对象
B. window.reload()方法可以用来刷新当前页面  应该是location.reload或者window.location.reload
C. window.location=”a.html”和window.location.href=”a.html”的作用都是把当前页面替换成a.html页面
D. 定义了全局变量g；可以用window.g的方式来存取该变量
```

答案：ACD



### Window open() 方法

[![Window 对象参考手册](https://www.runoob.com/images/up.gif) Window 对象](https://www.runoob.com/jsref/obj-window.html)

#### 定义和用法

open() 方法用于打开一个新的浏览器窗口或查找一个已命名的窗口。

#### 语法

window.open(*URL,name,specs,replace*)

#### URL

可选。打开指定的页面的URL。如果没有指定URL，打开一个新的空白窗口

#### name

可选。指定target属性或窗口的名称。支持以下值：

- _blank - URL加载到一个新的窗口。这是默认
- _parent - URL加载到父框架
- _self - URL替换当前页面
- _top - URL替换任何可加载的框架集
- *name* - 窗口名称

#### specs

可选。一个逗号分隔的项目列表。支持以下值：

| channelmode=yes\|no\|1\|0 | 是否要在影院模式显示 window。默认是没有的。仅限IE浏览器      |
| ------------------------- | ------------------------------------------------------------ |
| directories=yes\|no\|1\|0 | 是否添加目录按钮。默认是肯定的。仅限IE浏览器                 |
| fullscreen=yes\|no\|1\|0  | 浏览器是否显示全屏模式。默认是没有的。在全屏模式下的 window，还必须在影院模式。仅限IE浏览器 |
| height=pixels             | 窗口的高度。最小.值为100                                     |
| left=pixels               | 该窗口的左侧位置                                             |
| location=yes\|no\|1\|0    | 是否显示地址字段.默认值是yes                                 |
| menubar=yes\|no\|1\|0     | 是否显示菜单栏.默认值是yes                                   |
| resizable=yes\|no\|1\|0   | 是否可调整窗口大小.默认值是yes                               |
| scrollbars=yes\|no\|1\|0  | 是否显示滚动条.默认值是yes                                   |
| status=yes\|no\|1\|0      | 是否要添加一个状态栏.默认值是yes                             |
| titlebar=yes\|no\|1\|0    | 是否显示标题栏.被忽略，除非调用HTML应用程序或一个值得信赖的对话框.默认值是yes |
| toolbar=yes\|no\|1\|0     | 是否显示浏览器工具栏.默认值是yes                             |
| top=pixels                | 窗口顶部的位置.仅限IE浏览器                                  |
| width=pixels              | 窗口的宽度.最小.值为100                                      |

#### replace

Optional.Specifies规定了装载到窗口的 URL 是在窗口的浏览历史中创建一个新条目，还是替换浏览历史中的当前条目。支持下面的值：

- true - URL 替换浏览历史中的当前条目。
- false - URL 在浏览历史中创建新的条目。







# Navigator对象

#### Navigator的属性

| 属性          | 描述                                         | 值                                                           |
| ------------- | -------------------------------------------- | ------------------------------------------------------------ |
| language      | 返回当前浏览器的语言                         | "zh-CN"、"en"等                                              |
| cookieEnabled | 返回指明浏览器中是否启用 cookie 的布尔值     | true,false                                                   |
| onLine        | 返回指明系统是否处于联网状态的布尔值         | true,false                                                   |
| platform      | 返回运行浏览器的操作系统平台。               | "Win32", "Linux i686", "MacPPC", "MacIntel", 等              |
| userAgent     | 返回由客户机发送服务器的 user-agent 头部的值 | userAgent: "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_2) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/72.0.3626.109 Safari/537.36" |



### 检测插件

- 非IE可以使用plugins数组来达到目的。
- 1. name： 插件的名字
  2. description： 插件的描述
  3. filename 插件的文件名
  4. length 插件所处理的MIME类型数量

```javascript
// 检测插件 在IE中无效
function hasPlugin( name )\\{
    var name = name.toLowerCase();
    for( var i = 0, l = navigator.plugins.length; i < l; i++ )\\{
        if( navigator.plugins[i].name.toLowerCase().indexOf(name) > -1 )\\{
            return true
        \\};
    \\}
    return false
\\}
alert( hasPlugin("Flash") )
```

#### 检测IE中的插件

- 使用专有的ActiveXObject类型
- IE是以COM独享的方式实现插件的，而COM对象使用唯一标识符来标识，因此，要检查特定的插件，就必须知道其COM标识符。

```javascript
function hasIEPlugin( name )\\{
    try\\{
        new ActiveXObject( name );
        return true
    \\} catch (ex)\\{
        return false
    \\}
\\}

// 检测 QuickTime
alert( hasIEPlugin( "QuickTime.QuickTime" ) )
```

#### registerContentHandler() 和 registerProtocolHandler()

- 这两个方法可以让一个站点指明它可以处理特定类型的信息。







# location对象

> 一个完整的url 包括9个部分 协议://用户名：密码@域名：端口/路径；参数？查询#片段 不过几乎没有哪个url包含这些所有组件，最重要的三部分是协议，域名和路径。

#### location 对象属性

```
http://www.baidu.com:80/javascript/?file=001/BOM/README.md/#location对象
```

| 属性     | 描述                                               | 可读写性 | 结果                                                         |
| -------- | -------------------------------------------------- | -------- | ------------------------------------------------------------ |
| href     | 包含整个URL的一个字符串                            | 读写     | `http://www.baidu.com:80/javascript/001/BOM/?file=README.md#location对象` |
| origin   | 包含页面来源的域名的标准形式字符串                 | 只读     | `http://www.baidu.com:80`                                    |
| protocol | 包含URL对应协议的字符串，最后有一个":"             | 只读     | `http:`                                                      |
| host     | 包含了域名和端口号的字符串，如没有端口号则只有域名 | 只读     | `www.baidu.com:80`                                           |
| hostname | 包含URL域名的字符串                                | 只读     | `www.baidu.com`                                              |
| port     | 包含端口号的字符串                                 | 只读     | `80`                                                         |
| pathname | 包含URL中路径部分的字符串，开头有一个"/"           | 只读     | `/javascript/001/BOM/`                                       |
| search   | 包含URL参数（查询字符串）的字符串，开头有一个“?”   | 只读     | `?file=README.md`                                            |
| hash     | 包含块标识符的字符串，开头有一个"#"                | 只读     | `#location对象`片段                                          |

#### location 对象方法

| 属性     | 参数    | 返回值              | 功能                                                         | 兼容性 |
| -------- | ------- | ------------------- | ------------------------------------------------------------ | ------ |
| assign   | url     | undefined           | 加载给定URL的内容资源                                        | 全部   |
| reload   | Boolean | undefined           | 重新加载来自当前 URL的资源(刷新本页)                         | 全部   |
| replace  | url     | undefined           | 用给定的URL替换掉当前的资源                                  | 全部   |
| toString | 无      | 包含整个URL的字符串 | 获取本窗口的url(只能获取，无法修改，读取效果与`location.href`相同) | 全部   |

`location.reload` 的参数：

- false或未写参数：检测服务器上的文档是否已改变。如果文档已改变，reload() 会再次下载该文档。如果文档未改变，则该方法将从缓存中装载文档。这与用户单击浏览器的刷新按钮的效果是完全一样的。
- true：那么无论文档的最后修改日期是什么，它都会绕过缓存，从服务器上重新下载该文档。这与用户在单击浏览器的刷新按钮时按住 Shift 健的效果是完全一样。



location对象既是window对象的属性，也是document对象的属性。

换句话说，window.location和document.loaction引用的是同一个对象。

参数

1. hash 返回url中的hash 不存在返回空字符串
2. host 服务器名称和端口号
3. hostname 不带端口号的服务器名称
4. href 返回当前加载页面的完整URL location.toString()方法也返回这个值
5. pathname 返回url中的目录和（或）文件名
6. port 返回url中指定的端口号。如果url中年不包含端口号，返回空字符串
7. protocol 返回页面使用的协议 通常是HTTP https
8. search 返回url的查询字符串。字符串以问号开头

查询字符串参数

```JavaScript
function getQueryStringArgs()\\{
    // 取得查询字符串并去掉开头的问号
    var qs = ( location.search.length > 0  ? location.search.substring(1) : "" ),
        args = \\{\\},
        items = qs.length ? qs.split("&") : [],
        item = null,
        name = null,
        value = null,
        i = 0,
        len = items.length;
        
    // 逐个加到args对象中
    for( i = 0; i < len; i++ )\\{
        item = items[i].split("=");
        name = decodeURIComponent( item[0] );
        value = decodeURIComponent( item[1] );
        if( name.length )\\{
            args[name] = value;
        \\}
    \\}
    return args;
\\}
```

- assign() 立即打开新URL并在历史记录中生成一条新纪录
- replace() 打开的URL history不会记录 用户不能后退到上个页面



### window.location.hash属性介绍

location是javascript里边管理地址栏的内置对象，比如location.href就管理页面的url，用location.href=url就可以直接将页面重定向url。而location.hash则可以用来获取或设置页面的标签值。比如http://domain/#admin的location.hash="#admin"。



### window.location.hash简单应用

location是javascript里边管理地址栏的内置对象，比如location.href就管理页面的url，用location.href=url就可以直接将页面重定向url。而location.hash则可以用来获取或设置页面的标签值。比如http://domain/#admin的location.hash="#admin"。利用这个属性值可以做一个非常有意义的事情。

#### 一、#的涵义

\#代表网页中的一个位置。其右面的字符，就是该位置的标识符。比如，

　　http://www.example.com/index.html#print

就代表网页index.html的print位置。浏览器读取这个URL后，会自动将print位置滚动至可视区域。

为网页位置指定标识符，有两个方法。一是使用锚点，比如<a name="print"></a>，二是使用id属性，比如<div id="print" >。

#### 二、HTTP请求不包括#

\#是用来指导浏览器动作的，对服务器端完全无用。所以，HTTP请求中不包括#。

比如，访问下面的网址，

　　http://www.example.com/index.html#print

浏览器实际发出的请求是这样的：

　　GET /index.html HTTP/1.1

　　Host: [www.example.com](http://www.example.com/)

可以看到，只是请求index.html，根本没有"#print"的部分。

#### 三、#后的字符

在第一个#后面出现的任何字符，都会被浏览器解读为位置标识符。这意味着，这些字符都不会被发送到服务器端。

比如，下面URL的原意是指定一个颜色值：

　　http://www.example.com/?color=#fff

但是，浏览器实际发出的请求是：

　　GET /?color= HTTP/1.1

　　Host: [www.example.com](http://www.example.com/)

可以看到，"#fff"被省略了。只有将#转码为\\%23，浏览器才会将其作为实义字符处理。也就是说，上面的网址应该被写成：

　　http://example.com/?color=\\%23fff

#### 四、改变#不触发网页重载

单单改变#后的部分，浏览器只会滚动到相应位置，不会重新加载网页。

比如，从

　　http://www.example.com/index.html#location1

改成

　　http://www.example.com/index.html#location2

浏览器不会重新向服务器请求index.html。

#### 五、改变#会改变浏览器的访问历史

每一次改变#后的部分，都会在浏览器的访问历史中增加一个记录，使用"后退"按钮，就可以回到上一个位置。

这对于ajax应用程序特别有用，可以用不同的#值，表示不同的访问状态，然后向用户给出可以访问某个状态的链接。

值得注意的是，上述规则对IE 6和IE 7不成立，它们不会因为#的改变而增加历史记录。

#### 六、window.location.hash读取#值

window.location.hash这个属性可读可写。读取时，可以用来判断网页状态是否改变；写入时，则会在不重载网页的前提下，创造一条访问历史记录。

#### 七、onhashchange事件

这是一个HTML 5新增的事件，当#值发生变化时，就会触发这个事件。IE8+、Firefox 3.6+、Chrome 5+、Safari 4.0+支持该事件。

它的使用方法有三种：

　　window.onhashchange = func;

　　<body onhashchange="func();">

　　window.addEventListener("hashchange", func, false);

对于不支持onhashchange的浏览器，可以用setInterval监控location.hash的变化。

#### 八、Google抓取#的机制

默认情况下，Google的网络蜘蛛忽视URL的#部分。

但是，Google还规定，如果你希望Ajax生成的内容被浏览引擎读取，那么URL中可以使用"#!"，Google会自动将其后面的内容转成查询字符串_escaped_fragment_的值。

比如，Google发现新版twitter的URL如下：

　　http://twitter.com/#!/username

就会自动抓取另一个URL：

　　http://twitter.com/?_escaped_fragment_=/username

通过这种机制，Google就可以索引动态的Ajax内容。



### window.location和location有什么区别

在浏览器环境中，`window.location` 和 `location` 通常指的是同一个对象。`location` 是 `window` 对象的一个属性，它提供了当前窗口中加载文档的信息，并且可以用来改变这个文档的URL。

具体来说：

- `window.location` 是一个全局对象，你可以通过 `window` 对象来访问它。它是 `Window` 接口的一个属性，表示当前显示的资源的 URL 信息。
- `location` 是 `window.location` 的一个快捷方式，因为 `window` 是全局对象，所以在全局作用域中可以直接使用 `location` 来引用 `window.location`。

例如，下面的代码片段展示了如何使用这两个对象来获取当前页面的URL：

```javascript
// 使用 window.location
var url1 = window.location.href;

// 使用 location（这是 window.location 的简写）
var url2 = location.href;

// 这两个变量将包含相同的值
console.log(url1); // 输出当前页面的URL
console.log(url2); // 输出与上面相同的URL
```

两者之间的主要区别在于语法上的便捷性。直接使用 `location` 更加简洁，而使用 `window.location` 则更明确地表明了你正在访问的是 `window` 对象的属性。在大多数情况下，选择哪一种形式是个人或团队编码风格的问题。不过，在某些特殊的情况下，比如在一个函数内部，如果已经有一个局部变量叫做 `location`，那么为了防止混淆，最好还是使用 `window.location` 来指代浏览器的 `location` 对象。







# history对象

#### history 对象属性

| 属性   | 描述                           | 可读写性 | 兼容性 |
| ------ | ------------------------------ | -------- | ------ |
| length | 包含当前页面在内的历史记录个数 | 只读     | 全部   |

### history 对象方法

| 属性    | 参数   | 返回值    | 功能                                                  | 兼容性 |
| ------- | ------ | --------- | ----------------------------------------------------- | ------ |
| back    | 无     | undefined | 加载 history 列表中的前一个 URL(等价于history.go(-1)) | 全部   |
| forward | 无     | undefined | 加载 history 列表中的下一个 URL(等价于history.go(1))  | 全部   |
| go      | number | undefined | 通过当前页面的相对位置从浏览器历史记录加载页面        | 全部   |







# 其他

### 什么是Bom？有哪些常用的Bom属性？

Bom是浏览器对象

#### location对象

location.href-- 返回或设置当前文档的URL
location.search -- 返回URL中的查询字符串部分。例如 http://www.dreamdu.com/dreamd... 返回包括(?)后面的内容?id=5&name=dreamdu
location.hash -- 返回URL#后面的内容，如果没有#，返回空 location.host -- 返回URL中的域名部分，例如www.dreamdu.com
location.hostname -- 返回URL中的主域名部分，例如dreamdu.com
location.pathname -- 返回URL的域名后的部分。例如 http://www.dreamdu.com/xhtml/ 返回/xhtml/
location.port -- 返回URL中的端口部分。例如 http://www.dreamdu.com:8080/xhtml/ 返回8080
location.protocol -- 返回URL中的协议部分。例如 http://www.dreamdu.com:8080/xhtml/ 返回(//)前面的内容http:
location.assign -- 设置当前文档的URL

location.reload() -- 重载当前页面

##### location.replace() 

设置当前文档的URL，并且在history对象的地址列表中移除这个URL location.replace(url);

`window.location.replace` 是一个JavaScript的方法，用于将当前窗口的地址替换为新的URL地址。这个方法不会在浏览器的历史记录中留下新的记录，也就是说用户使用后退按钮不能返回到这个方法执行前的页面。

语法如下：

```javascript
window.location.replace(url);
```

这里的 `url` 参数是要加载的新页面的URL地址。当调用 `window.location.replace` 方法时，它会立即加载提供的URL，并且当前页面会被新的页面所替代。

#### history对象

history.go() -- 前进或后退指定的页面数
history.go(num); history.back() -- 后退一页
history.forward() -- 前进一页

#### Navigator对象

navigator.userAgent -- 返回用户代理头的字符串表示(就是包括浏览器版本信息等的字符串)
navigator.cookieEnabled -- 返回浏览器是否支持(启用)cookie



### js刷新当前页面方法：

#### 方法1：reload() 方法

reload()方法用于刷新当前文档。

reload() 方法类似于你浏览器上的刷新页面按钮。

```
location.reload();
```

在按钮中可以使用 onclick 事件：

```
<input type="button" onclick="javascript:location.reload();" value="刷新当前页面">
```

更多关于reload() 方法请参考文档：https://www.runoob.com/jsref/met-loc-reload.html

------

#### 方法2：replace() 方法

**replace() 方法**可用一个新文档取代当前文档。

```
window.location.replace("https://www.runoob.com")
```

<iframe width="100\\%" height="300" src="https://c.runoob.com/iframe/89" allowfullscreen="allowfullscreen" frameborder="0" style="border: 0px; margin: 0px; padding: 0px; color: rgb(51, 51, 51); font-family: &quot;Helvetica Neue&quot;, Helvetica, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Noto Sans CJK SC&quot;, &quot;WenQuanYi Micro Hei&quot;, Arial, sans-serif; font-size: 14px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial;"></iframe>
更多关于replace() 方法请参考文档：https://www.runoob.com/jsref/met-loc-replace.html

------

#### 方法3：页面自动刷新

页面自动刷新：把如下代码加入<head>区域中

```
<meta http-equiv="refresh" content="5">
```

其中 5 指每隔 5 秒刷新一次页面。

#### 方法4：

```
history.go(0)
```



### js跳转页面方法汇总：

- window.open(url)

  1.点击某一个链接之后跳转到新页面显示

  ```javascript
  window.open('http://www.baidu.com','_blank');
  ```

  2.需要刷新当前页面或者覆盖当前页面

  ```javascript
  window.open('http://www.baidu.com','_self');
  ```

- location.href = ""

- location.assign(url)
