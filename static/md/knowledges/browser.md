---
title: 浏览器
date: 2021-03-12 10:10:10
categories: 
- 前端知识
tags:
- 存储技术
- 事件机制
- 跨域
- Service Worker
- 渲染机制
- 浏览器内核
---

## 浏览器端的存储技术有哪些？

### cookie

cookie又叫会话跟踪技术（会员卡的意思）由web服务器保存在用户浏览器上的小文本文件，包含用户的相关信息。cookie 其实最开始是服务器端用于记录用户状态的一种方式，由服务器设置，在客户端存储，然后每次发起同源请求时，发送给服务器端。cookie 最多能存储 4 k 数据，它的生存时间由 expires 属性指定，并且 cookie 只能被同源的页面访问共享。

我的理解是 cookie 是服务器提供的一种用于维护会话状态信息的数据，通过服务器发送到浏览器，浏览器保存在本地，当下一次有同源的请求时，将保存的 cookie 值添加到请求头部，发送给服务端。这可以用来实现记录用户登录状态等功能。cookie 一般可以存储 4k 大小的数据，并且只能够被同源的网页所共享访问。

服务器端可以使用 Set-Cookie 的响应头部来配置 cookie 信息。一条cookie 包括了9个属性值 name、value、expires、domain、path、secure、HttpOnly、SameSite、Priority。其中 name 和 value 分别是 cookie 的名字和值。expires 指定了 cookie 失效的时间，domain 是域名、path是路径，domain 和 path 一起限制了 cookie 能够被哪些 url 访问。secure 规定了 cookie 只能在确保安全的情况下传输，HttpOnly 规定了这个 cookie 只能被服务器访问，不能使用 js 脚本访问。SameSite 属性用来限制第三方 cookie，可以有效防止 CSRF 攻击，从而减少安全风险。Priority 是 chrome 的提案，定义了三种优先级，当 cookie 数量超出时低优先级的 cookie 会被优先清除。

在发生 xhr 的跨域请求的时候，即使是同源下的 cookie，也不会被自动添加到请求头部，除非显示地规定。

cookie是存放在浏览器中的，在每一个浏览器安装目录下，都存在一个文件夹，存放着不同域下对应的cookie。**当浏览器通过http请求某一个域时，此时浏览器就会将该域下面的cookie自动放入request header中**。我们需要注意，浏览器自动帮我们携带，此时如果很多无关紧要的数据都存放在cookie中，都会随着请求发送给后台，这样就无形当中增加了网络开销。此时我们再想想什么数据在每一次都需要?其实我们的身份认证信息在每一次都需要携带，所以存放在cookie的数据最合适的是身份认证信息，其他信息都不合适。

详细资料可以参考：
[《HTTP cookies》 ](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Cookies)
[《聊一聊 cookie》 ](https://segmentfault.com/a/1190000004556040)

#### 特点：

- 禁用cookie后，用户无法正常注册登录

- cookie与浏览器相关，不同浏览器之间保存的cookie是不能互相访问的；`cookie`还需要指定作用域，不可以跨域调用。

- cookie的安全性不高，易受xss攻击

- cookie值的类型先定位string类型，cookie大小一般只有4kb，可以进行单独配置
- 持久保存客户端数据提供了方便，分担了服务器存储的负担，极高的扩展性和可用性

#### Cookie 的弊端

- `Cookie`数量和长度的限制。每个 domain 特定的域名下最多只能有 20 条 cookie，每个 cookie 长度不能超过 4KB，否则会被截掉。
- 安全性问题。如果 cookie 被人拦截了，那人就可以取得所有的 session 信息。即使加密也与事无补，因为拦截者并不需要知道 cookie 的意义，他只要原样转发 cookie 就可以达到目的了。
- 有些状态不可能保存在客户端。例如，为了防止重复提交表单，我们需要在服务器端保存一个计数器。如果我们把这个计数器保存在客户端，那么它起不到任何作用。
- 在请求头上带着数据，导致流量增加。

### 改进办法

- 通过良好的编程，控制保存在cookie中的session对象的大小。
- 通过加密和安全传输技术（SSL），减少cookie被破解的可能性。
- 只在cookie中存放不敏感数据，即使被盗也不会有重大损失。
- 控制cookie的生命期，使之不会永远有效。偷盗者很可能拿到一个过期的cookie。

#### cookie的作用

- 保存用户登录状态。例如将用户id存储于一个cookie内，这样当用户下次访问该页面时就不需要重新登录了，现在很多论坛和社区都提供这样的功能。cookie还可以设置过期时间，当超过时间期限后，cookie就会自动消失。因此，系统往往可以提示用户保持登录状态的时间：常见选项有一个月、三个 月、一年等。
- 跟踪用户行为。例如一个天气预报网站，能够根据用户选择的地区显示当地的天气情况。如果每次都需要选择所在地是烦琐的，当利用了 cookie后就会显得很人性化了，系统能够记住上一次访问的地区，当下次再打开该页面时，它就会自动显示上次用户所在地区的天气情况。因为一切都是在后台完成，所以这样的页面就像为某个用户所定制的一样，使用起来非常方便。
- 定制页面。如果网站提供了换肤或更换布局的功能，那么可以使用cookie来记录用户的选项，例如：背景色、分辨率等。当用户下次访问时，仍然可以保存上一次访问的界面风格。

#### 存储位置

浏览器控制面板(f12) - Application选项里面 - 左侧cookie

通过控制面板删除选中的或者全部的cookie

#### 操作方式

```html
// 设置 cookie
document.cookie = "username=John Doe; expires=Thu, 18 Dec 2013 12:00:00 GMT;path=/" 
// 删除 cookie
document.cookie = "username=; expires=Thu, 01 Jan 1970 00:00:00 GMT"
```

设置 cookie 的方法比较简单，其中除了键和值，还有几个参数可以添加

**expires**
过期时间，当过了到期日期时，浏览器会自动删除该 cookie，如果想删除一个 cookie，只需要把它过期时间设置成过去的时间即可
比如希望设置过期时间一年：new Date().getTime() + 365 _ 24 _ 60 _ 60 _ 1000

如果不设置过期时间，则表示这个 cookie 生命周期为浏览器会话期间，只要关闭浏览器窗口，cookie 就消失了。

**path**
路径，值可以是一个目录，或者是一个路径。

如果 cc.com/test/index.html 建立了一个 cookie，那么在 cc.com/test/目录里的所有页面，以及该目录下面任何子目录里的页面都可以访问这个 cookie。因此在 cc.com/test/test2/test3 里的任何页面都可以访问 cc.com/test/index.html 建立的 cookie。若 cc.com/test/ 若想访问 cc.com/test/index.html 设置的 cookes，需要把 cookies 的 path 属性设置成“/”。
在指定路径的时候，凡是来自同一服务器，URL 里有相同路径的所有 WEB 页面都可以共享 cookies。

**domain**
主机名，是指同一个域下的不同主机，例如：www.baidu.com 和 map.baidu.com 就是两个不同的主机名。默认情况下，一个主机中创建的 cookie 在另一个主机下是不能被访问的，但可以通过 domain 参数来实现对其的控制：document.cookie = "name=value;domain=.baidu.com"，这样，所有\*.baidu.com 的主机都可以访问该 cookie。



### 什么是Cookie 隔离？（或者说：请求资源的时候不要带cookie怎么做）

- 通过使用多个非主要域名来请求静态文件，如果静态文件都放在主域名下，那静态文件请求的时候都带有的cookie的数据提交给server的，非常浪费流量，所以不如隔离开，静态资源放CDN。
- 因为cookie有域的限制，因此不能跨域提交请求，故使用非主要域名的时候，请求头中就不会带有cookie数据，这样可以降低请求头的大小，降低请求时间，从而达到降低整体请求延时的目的。
- 同时这种方式不会将cookie传入Web Server，也减少了Web Server对cookie的处理分析环节，提高了webserver的http请求的解析速度。



### Cookie如何防范XSS攻击

XSS（跨站脚本攻击）是指攻击者在返回的HTML中嵌入javascript脚本，为了减轻这些攻击，需要在HTTP头部配上，set-cookie：

- httponly-这个属性可以防止XSS,它会禁止javascript脚本来访问cookie。
- secure - 这个属性告诉浏览器仅在请求为https的时候发送cookie。

结果应该是这样的：Set-Cookie=.....



### 在 HTTP 响应 Header 中，set-cookie 选项有哪些，分别代表什么含义？

Set-Cookie: <cookie-name>=<cookie-value>

- Expires=`<date>`
- Max-Age=`<non-zero-digit>`
- Domain=`<domain-value>`
- Path=`<path-value>`
- Secure
- HttpOnly
- SameSite=Strict
- SameSite=Lax

```js
name = name; // 需要设置cookie的值(name不能使用";"和","号),有多个name值时用";"分隔例如：name1=name1;name2=name2;name3=name3

expires; //cookie的有效期限,格式为:expires="Wdy,DD-Mon-YYYY HH:MM:SS"

path; //设置cookie支持的路径,如果path是一个路径，则cookie对这个目录下的所有文件及子目录生效，例如：path="/cgi-bin/"，如果path是一个文件，则cookie指对这个文件生效，例如：path="/cgi-bin/cookie.cgi"

domain; //对cookie生效的域名，例如：domain="gzdzw.51.net"

secure; //如果给出此标志，表示cookie只能通过SSL协议的https服务器来传递,cookie的接收是通过设置环境变量HTTP_COOKIE来实现的，CGI程序可以通过检索该变量获取cookie信息
```

解析：Cookie 相关的 Http 头

有两个 Http 头部和 Cookie 有关：Set-Cookie 和 Cookie

- Set-Cookie 由服务器发送，它包含在响应请求的头部中。它**用于在客户端创建一个 Cookie**
- Cookie 头由客户端发送，包含在 HTTP 请求的头部中。注意，只有 cookie 的 domain 和 path 与请求的 URL 匹配才会发送这个 cookie。



### localStorage

`localStorage`是以键值对(Key-Value)的方式持久化的本地存储，永久存储，永不失效，除非手动删除。IE8+支持，每个域名限制 5M

打开同域的新页面也能访问得到

操作方式：

window.localStorage.username = 'hehe' // 设置
window.localStorage.setItem('username', 'hehe') // 设置
window.localStorage.getItem('username') // 读取
window.localStorage.removeItem('username') // 删除
window.localStorage.key(1) // 读取索引为 1 的值
window.localStorage.clear() // 清除所有
可以存储数组、数字、对象等可以被序列化为字符串的内容



### sessionStorage

`sessionStorage`用于本地存储一个会话（session）中的数据，这些数据只有在同一个会话中的页面才能访问并且当会话结束后数据也随之销毁。因此`sessionStorage`不是一种持久化的本地存储，仅仅是会话级别的存储。

sessionStorage 是 html5 提供的一种浏览器本地存储的方法，它借鉴了服务器端 session 的概念，代表的是一次会话中所保存的数据。它一般能够存储 5M 或者更大的数据，它在当前窗口关闭后就失效了，并且sessionStorage 只能被**同一个窗口的同源页面**所访问共享。

sessionStorage 操作的方法与 localStroage 是一样的，区别在于 sessionStorage 在关闭页面后即被清空，而 localStorage 则会一直保存。很多时候数据只需要在用户浏览一组页面期间使用，关闭窗口后数据就可以丢弃了，这种情况使用 sessionStorage 就比较方便。

注意，刷新页面 sessionStorage 不会清除，但是打开同域新页面访问不到



### 描述 cookies、sessionStorage 和 localStorage 的区别？

他们都是保存在浏览器端的存储方式。

**与服务器交互：**

- cookie 是网站为了标示用户身份而储存在用户本地终端上的数据（通常经过加密），服务器和客户端都可以访问。

- cookie 始终会**在同源 http 请求头中携带**（即使不需要），在浏览器和服务器间来回传递。

  因为每次 http 请求都会携带 cookie，所以 cookie 只适合保存很小的数据，如会话标识。

- sessionStorage 和 localStorage 不会自动把数据发给服务器，仅**在客户端（即浏览器）中保存**

**有效时间：**

- localStorage    保存在本浏览器数据缓存区，用于持久化的本地存储，除非主动删除数据，否则数据是永远不会过期的。

- sessionStorage    用于本地存储一个session中的数据，这些数据保存在当前会话窗口，数据在当前浏览器窗口关闭（页面会话结束）后自动删除。

  重新加载或恢复页面仍会保持原来的页面会话，**在新标签或窗口**打开一个页面时会在顶级浏览上下文中初始化一个新的会话。

  **Storage共同点：都是保存在浏览器端、仅同源可用的存储方式**

- cookie    设置的cookie过期时间之前一直有效，与浏览器是否关闭无关

**存储大小：**

- cookie 数据根据不同浏览器限制，大小一般不能超过 4k
- sessionStorage 和 localStorage 虽然也有存储大小的限制，但比cookie大得多，可以达到5M或更大

**存储格式：**

cookie只能以字符串格式保存；

webStorage以key-value格式保存，更便于存取（sessionStorage.setItem("key","value")，sessionStorage.getItem("key")）；

**作用域不同：**

- sessionStorage 只在同源的同窗口（或标签页）中共享数据，也就是只在当前会话中共享。

  不在不同的浏览器页面中共享，即使是同一个页面（比如同一页面打开为两个标签页）

- localStorage 在所有同源窗口中都是共享的；

- cookie 也是在所有同源窗口中都是共享的。

- 在浏览器多个 tab 页中，cookie、localStorage 可以共享数据，sessionStorage 仅保存在当前 tab 页中不能共享。

**操作方法：**

`Web Storage`拥有`setItem,getItem,removeItem,clear`等方法，不像`cookie`需要前端开发者自己封装`setCookie，getCookie`。

上面几种方式都是存储少量数据的时候的存储方式，当我们需要在本地存储大量数据的时候，我们可以使用浏览器的 indexDB 这是浏览器提供的一种本地的数据库存储机制。它不是关系型数据库，它内部采用对象仓库的形式存储数据，它更接近 NoSQL 数据库。
   [《浏览器数据库 IndexedDB 入门教程》](http://www.ruanyifeng.com/blog/2018/07/indexeddb.html)



### cookie 和session 的区别：

- `session`： 是一个抽象概念，开发者为了实现中断和继续等操作，将 `user agent `和 `server` 之间一对一的交互，抽象为“会话”，进而衍生出“会话状态”，也就是 `session` 的概念
- `cookie`：它是一个世纪存在的东西，`http` 协议中定义在 `header` 中的字段，可以认为是 `session` 的一种后端无状态实现

> 现在我们常说的 `session`，是为了绕开 `cookie` 的各种限制，通常借助 `cookie`本身和后端存储实现的，一种更高级的会话状态实现

`session` 的常见实现要借助`cookie`来发送 `sessionID`

1.  cookie数据存放在客户的浏览器上，session数据放在服务器上。
2. cookie不是很安全，别人可以分析存放在本地的COOKIE并进行COOKIE欺骗
   考虑到安全应当使用session。
3. session会在一定时间内保存在服务器上。当访问增多，会比较占用你服务器的性能
   考虑到减轻服务器性能方面，应当使用COOKIE。
4. 单个cookie保存的数据不能超过4K，很多浏览器都限制一个站点最多保存20个cookie。
5. 所以个人建议：
   将登陆信息等重要信息存放为SESSION
   其他信息如果需要保留，可以放在COOKIE中



### web storage（包含sessionStorage和localStorage）和cookie的区别

Cookie的作用**是与服务器进行交互**，作为HTTP规范的一部分而存在

而Web Storage仅仅是为了**在本地“存储”数据**而生。

cookie 数据还有路径（path）的概念，可以限制 cookie 只属于某个路径下。

Web Storage 支持事件通知机制，可以将数据更新的通知发送给监听者。

Web Storage 的 api 接口使用更方便，cookie 的原生接口不友好，需要自己封装。

- Web Storage的概念和cookie相似，区别是它是为了更大容量存储设计的。Cookie的大小是受限的，并且每次你请求一个新的页面的时候Cookie都会被发送过去，这样无形中浪费了带宽，另外cookie还需要指定作用域，不可以跨域调用

- 除此之外，WebStorage拥有setItem,getItem,removeItem,clear等方法，不像cookie需要前端开发者自己封装setCookie，getCookie

- 但是cookie也是不可以或缺的：cookie的作用是与服务器进行交互，作为HTTP规范的一部分而存在 ，而Web Storage仅仅是为了在本地“存储”数据而生

- 浏览器的支持除了IE７及以下不支持外，其他标准浏览器都完全支持(ie及FF需在web服务器里运行)，值得一提的是IE总是办好事，例如IE7、IE6中的userData其实就是javascript本地存储的解决方案。通过简单的代码封装可以统一到所有的浏览器都支持web storage

- localStorage和sessionStorage都具有相同的操作方法，例如setItem、getItem和removeItem等



### 如何实现浏览器内多个标签页之间的通信?

调用 localstorge、cookies 等本地存储方式，注意sessionstorge不可以哦



### 安全性

需要注意的是，不是什么数据都适合放在 Cookie、localStorage 和 sessionStorage 中的，因为它们保存在本地容易被篡改，使用它们的时候，需要时刻注意是否有代码存在 XSS 注入的风险。所以千万不要用它们存储你系统中的敏感数据。







## 事件机制

我们在网页中的某个操作（有的操作对应多个事件）。例如：当我们点击一个按钮就会产生一个**事件**。是可以被 JavaScript 侦测到的行为。



### 请解释什么是事件代理

事件代理（Event Delegation），又称之为事件委托。是 JavaScript 中常用绑定事件的常用技巧。

顾名思义，“事件代理”即是**把原本需要绑定的事件委托给父元素，让父元素担当事件监听的职务。**

**原理**是DOM元素的事件冒泡。

使用事件代理的好处是**可以提高性能**

**怎么实现：**在元素的父节点注册事件，通过事件冒泡，在父节点捕获事件



### 事件触发三阶段

- document 往事件触发处传播，遇到注册的捕获事件会触发
- 传播到事件触发处时触发注册的事件
- 从事件触发处往 document 传播，遇到注册的冒泡事件会触发

> 事件触发一般来说会按照上面的顺序进行，但是也有特例，如果给一个目标节点同时注册冒泡和捕获事件，事件触发会按照注册的顺序执行

```
// 以下会先打印冒泡然后是捕获
node.addEventListener('click',(event) =>\\{
	console.log('冒泡')
\\},false);
node.addEventListener('click',(event) =>\\{
	console.log('捕获 ')
\\},true)
```



### 注册事件

- 通常我们使用 `addEventListener` 注册事件，该函数的第三个参数可以是布尔值，也可以是对象。对于布尔值 `useCapture` 参数来说，该参数默认值为 `false` 。`useCapture` 决定了注册的事件是捕获事件还是冒泡事件
- 一般来说，我们只希望事件只触发在目标上，这时候可以使用 `stopPropagation` 来阻止事件的进一步传播。通常我们认为 `stopPropagation` 是用来阻止事件冒泡的，其实该函数也可以阻止捕获事件。`stopImmediatePropagation` 同样也能实现阻止事件，但是还能阻止该事件目标执行别的注册事件

```javascript
node.addEventListener('click',(event) =>\\{
	event.stopImmediatePropagation()
	console.log('冒泡')
\\},false);
// 点击 node 只会执行上面的函数，该函数不会执行
node.addEventListener('click',(event) => \\{
	console.log('捕获 ')
\\},true)
```



### 事件代理

> 如果一个节点中的子节点是动态生成的，那么子节点需要注册事件的话应该注册在父节点上

```html
<ul id="ul">
	<li>1</li>
    <li>2</li>
	<li>3</li>
	<li>4</li>
	<li>5</li>
</ul>
<script>
	let ul = document.querySelector('##ul')
	ul.addEventListener('click', (event) => \\{
		console.log(event.target);
	\\})
</script>
```

> 事件代理的方式相对于直接给目标注册事件来说，有以下优点

- 节省内存
- 不需要给子节点注销事件



### 介绍DOM0，DOM2，DOM3事件处理方式区别

- DOM0级事件处理方式：
  - `btn.onclick = func;`
  - `btn.onclick = null;`
- DOM2级事件处理方式：
  - `btn.addEventListener('click', func, false);`
  - `btn.removeEventListener('click', func, false);`
  - `btn.attachEvent("onclick", func);`
  - `btn.detachEvent("onclick", func);`
- DOM3级事件处理方式：
  - `eventUtil.addListener(input, "textInput", func);`
  - `eventUtil` 是自定义对象，`textInput` 是DOM3级事件



### 事件的三个阶段

捕获、目标、冒泡



### 介绍事件“捕获”和“冒泡”执行顺序和事件的执行次数？

按照W3C标准的事件：首是进入捕获阶段，直到达到目标元素，再进入冒泡阶段

事件执行次数（DOM2-addEventListener）：元素上绑定事件的个数
- 注意1：前提是事件被确实触发
- 注意2：事件绑定几次就算几个事件，即使类型和功能完全一样也不会“覆盖”

事件执行顺序：判断的关键是否目标元素
- 非目标元素：根据W3C的标准执行：捕获->目标元素->冒泡（不依据事件绑定顺序）
- 目标元素：依据事件绑定顺序：先绑定的事件先执行（不依据捕获冒泡标准）
- 最终顺序：父元素捕获->目标元素事件1->目标元素事件2->子元素捕获->子元素冒泡->父元素冒泡
- 注意：子元素事件执行前提    事件确实“落”到子元素布局区域上，而不是简单的具有嵌套关系



### 在一个DOM上同时绑定两个点击事件：一个用捕获，一个用冒泡。事件会执行几次，先执行冒泡还是捕获？

* 该DOM上的事件如果被触发，会执行两次（执行次数等于绑定次数）
* 如果该DOM是目标元素，则按事件绑定顺序执行，不区分冒泡/捕获
* 如果该DOM是处于事件流中的非目标元素，则先执行捕获，后执行冒泡



### 事件的代理/委托

事件委托是指将事件绑定目标元素的到父元素上，利用冒泡机制触发该事件

优点：
- 可以减少事件注册，节省大量内存占用
- 可以将事件应用于动态添加的子元素上

缺点：
使用不当会造成事件在不应该触发时触发

示例：

```
ulEl.addEventListener('click', function(e)\\{
    var target = event.target || event.srcElement;
    if(!!target && target.nodeName.toUpperCase() === "LI")\\{
        console.log(target.innerHTML);
    \\}
\\}, false);
```



### DOM事件的总结

**知识点主要包括以下几个方面：**

- 基本概念：`DOM`事件的级别

> 面试不会直接问你，DOM有几个级别。但会在题目中体现：“请用`DOM2` ....”。


- `DOM`事件模型、`DOM`事件流

> 面试官如果问你“**DOM事件模型**”，你不一定知道怎么回事。其实说的就是**捕获和冒泡**。

**DOM事件流**，指的是事件传递的**三个阶段**。

- 描述`DOM`事件捕获的具体流程

> 讲的是事件的传递顺序。参数为`false`（默认）、参数为`true`，各自代表事件在什么阶段触发。

能回答出来的人，寥寥无几。也许有些人可以说出一大半，但是一字不落的人，极少。

- `Event`对象的常见应用（`Event`的常用`api`方法）

> `DOM`事件的知识点，一方面包括事件的流程；另一方面就是：怎么去注册事件，也就是监听用户的交互行为。第三点：在响应时，`Event`对象是非常重要的。

**自定义事件（非常重要）**

> 一般人可以讲出事件和注册事件，但是如果让你讲**自定义事件**，能知道的人，就更少了。

**DOM事件的级别**

> `DOM`事件的级别，准确来说，是**DOM标准**定义的级别。包括：

**DOM0的写法：**

```javascript
  element.onclick = function () \\{

  \\}
```


> 上面的代码是在 `js` 中的写法；如果要在`html`中写，写法是：在`onclick`属性中，加 `js` 语句。


**DOM2的写法：**


```javascript
  element.addEventListener('click', function () \\{

  \\}, false);
```

>【重要】上面的第三参数中，**true**表示事件在**捕获阶段**触发，**false**表示事件在**冒泡阶段**触发（默认）。如果不写，则默认为false。


**DOM3的写法：**


```javascript
    element.addEventListener('keyup', function () \\{

    \\}, false);
```

> `DOM3`中，增加了很多事件类型，比如鼠标事件、键盘事件等。

> PS：为何事件没有`DOM1`的写法呢？因为，`DOM1`标准制定的时候，没有涉及与事件相关的内容。

**总结**：关于“DOM事件的级别”，能回答出以上内容即可，不会出题目让你做。



### DOM事件模型

> `DOM`事件模型讲的就是**捕获和冒泡**，一般人都能回答出来。

- 捕获：从上往下。
- 冒泡：从下（目标元素）往上。

**DOM事件流**

> `DOM`事件流讲的就是：浏览器在于当前页面做交互时，这个事件是怎么传递到页面上的。

**完整的事件流，分三个阶段：**

1. 捕获：从 `window` 对象传到 目标元素。
2. 目标阶段：事件通过捕获，到达目标元素，这个阶段就是目标阶段。
3. 冒泡：从**目标元素**传到 `Window` 对象。

![](http://img.smyhvae.com/20180306_1058.png)

![](http://img.smyhvae.com/20180204_1218.jpg)


**描述DOM事件捕获的具体流程**

> 很少有人能说完整。

**捕获的流程**


![](http://img.smyhvae.com/20180306_1103.png)

**说明**：捕获阶段，事件依次传递的顺序是：`window` --> `document` --> `html`--> `body` --> 父元素、子元素、目标元素。

- PS1：第一个接收到事件的对象是 **window**（有人会说`body`，有人会说`html`，这都是错误的）。
- PS2：`JS`中涉及到`DOM`对象时，有两个对象最常用：`window`、`doucument`。它们俩也是最先获取到事件的。

代码如下：

```javascript
    window.addEventListener("click", function () \\{
        alert("捕获 window");
    \\}, true);

    document.addEventListener("click", function () \\{
        alert("捕获 document");
    \\}, true);

    document.documentElement.addEventListener("click", function () \\{
        alert("捕获 html");
    \\}, true);

    document.body.addEventListener("click", function () \\{
        alert("捕获 body");
    \\}, true);

    fatherBox.addEventListener("click", function () \\{
        alert("捕获 father");
    \\}, true);

    childBox.addEventListener("click", function () \\{
        alert("捕获 child");
    \\}, true);

```


**补充一个知识点：**

> 在 `js`中：

- 如果想获取 `body` 节点，方法是：`document.body`；
- 但是，如果想获取 `html`节点，方法是`document.documentElement`。



### 冒泡的流程

> 与捕获的流程相反


**Event对象的常见 api 方法**

> 用户做的是什么操作（比如，是敲键盘了，还是点击鼠标了），这些事件基本都是通过`Event`对象拿到的。这些都比较简单，我们就不讲了。我们来看看下面这几个方法：

**方法一**

```javascript
    event.preventDefault();
```

- 解释：阻止默认事件。
- 比如，已知`<a>`标签绑定了click事件，此时，如果给`<a>`设置了这个方法，就阻止了链接的默认跳转。

**方法二：阻止冒泡**

> 这个在业务中很常见。

> 有的时候，业务中不需要事件进行冒泡。比如说，业务这样要求：单击子元素做事件`A`，单击父元素做事件B，如果不阻止冒泡的话，出现的问题是：单击子元素时，子元素和父元素都会做事件`A`。这个时候，就要用到阻止冒泡了。


> `w3c`的方法：（火狐、谷歌、`IE11`）

```javascript
    event.stopPropagation();
```

> `IE10`以下则是：

```javascript
	event.cancelBubble = true;
```

> 兼容代码如下：

```javascript
   box3.onclick = function (event) \\{

        alert("child");

        //阻止冒泡
        event = event || window.event;

        if (event && event.stopPropagation) \\{
            event.stopPropagation();
        \\} else \\{
            event.cancelBubble = true;
        \\}
    \\}
```

> 上方代码中，我们对`box3`进行了阻止冒泡，产生的效果是：事件不会继续传递到 `father`、`grandfather`、`body`了。


**方法三：设置事件优先级**


```javascript
    event.stopImmediatePropagation();
```

这个方法比较长，一般人没听说过。解释如下：

> 比如说，我用`addEventListener`给某按钮同时注册了事件`A`、事件`B`。此时，如果我单击按钮，就会依次执行事件A和事件`B`。现在要求：单击按钮时，只执行事件A，不执行事件`B`。该怎么做呢？这是时候，就可以用到`stopImmediatePropagation`方法了。做法是：在事件A的响应函数中加入这句话。

> 大家要记住 `event` 有这个方法。

**属性4、属性5（事件委托中用到）**


```javascript
    event.currentTarget   //当前所绑定的事件对象。在事件委托中，指的是【父元素】。

    event.target  //当前被点击的元素。在事件委托中，指的是【子元素】。

```

上面这两个属性，在事件委托中经常用到。


> **总结**：上面这几项，非常重要，但是容易弄混淆。


**自定义事件**

> 自定义事件的代码如下：


```javascript
    var myEvent = new Event('clickTest');
    element.addEventListener('clickTest', function () \\{
        console.log('smyhvae');
    \\});

	//元素注册事件
    element.dispatchEvent(myEvent); //注意，参数是写事件对象 myEvent，不是写 事件名 clickTest

```

> 上面这个事件是定义完了之后，就直接自动触发了。在正常的业务中，这个事件一般是和别的事件结合用的。比如延时器设置按钮的动作：

```javascript
    var myEvent = new Event('clickTest');

    element.addEventListener('clickTest', function () \\{
        console.log('smyhvae');
    \\});

    setTimeout(function () \\{
        element.dispatchEvent(myEvent); //注意，参数是写事件对象 myEvent，不是写 事件名 clickTest
    \\}, 1000);
```



### IE与火狐的事件机制有什么区别？ 如何阻止冒泡？

IE只事件冒泡，不支持事件捕获；火狐同时支持件冒泡和事件捕获（Firefox同时支持两种事件模型，也就是：捕获型事件和冒泡型事件）

ev.stoPropagation();（旧ie的方法 ev.cancelBubble = true;）



### 如何添加 html 元素的事件，有几种方法？请列举

直接在标签里添加；在元素上添加、使用事件注册函数添加



### 事件模型

- DOM0<br>
  直接绑定

```
<input onclick="sayHi()"/>

btn.onclick = function() \\{\\}
btn.onclick = null

```

- DOM2<br>
  DOM2 级事件可以冒泡和捕获
  通过 addEventListener 绑定
  通过 removeEventListener 解绑

```
// 绑定
btn.addEventListener('click', sayHi)
// 解绑
btn.removeEventListener('click', sayHi)

```

- DOM3<br>
  DOM3 具有更多事件类型
  DOM3 级事件在 DOM2 级事件的基础上添加了更多的事件类型，全部类型如下：

```
UI事件，当用户与页面上的元素交互时触发，如：load、scroll
焦点事件，当元素获得或失去焦点时触发，如：blur、focus
鼠标事件，当用户通过鼠标在页面执行操作时触发如：dbclick、mouseup
滚轮事件，当使用鼠标滚轮或类似设备时触发，如：mousewheel
文本事件，当在文档中输入文本时触发，如：textInput
键盘事件，当用户通过键盘在页面上执行操作时触发，如：keydown、keypress
合成事件，当为IME（输入法编辑器）输入字符时触发，如：compositionstart
变动事件，当底层DOM结构发生变化时触发，如：DOMsubtreeModified

```

解析：[参考](https://www.jianshu.com/p/3acdf5f71d5b)



### 如何自定义事件

1. 原生提供了 3 个方法实现自定义事件
2. createEvent，设置事件类型，是 html 事件还是 鼠标事件
3. initEvent 初始化事件，事件名称，是否允许冒泡，是否阻止自定义事件
4. dispatchEvent 触发事件

[MDN](https://developer.mozilla.org/zh-CN/docs/Web/Guide/Events/Creating_and_triggering_events)



### IE的事件处理和W3C的事件处理有哪些区别？

* 绑定事件
  - W3C: targetEl.addEventListener('click', handler, false);
  - IE: targetEl.attachEvent('onclick', handler);

* 删除事件
  - W3C: targetEl.removeEventListener('click', handler, false);
  - IE: targetEl.detachEvent(event, handler);

* 事件对象
  - W3C: var e = arguments.callee.caller.arguments[0]
  - IE: window.event

* 事件目标
  - W3C: e.target
  - IE: window.event.srcElement

* 阻止事件默认行为
  - W3C: e.preventDefault()
  - IE: window.event.returnValue = false

* 阻止事件传播
  - W3C: e.stopPropagation()
  - IE: window.event.cancelBubble = true



### W3C事件的 target 与 currentTarget 的区别？

* target 只会出现在事件流的目标阶段
* currentTarget 可能出现在事件流的任何阶段
* 当事件流处在目标阶段时，二者的指向相同
* 当事件流处于捕获或冒泡阶段时：currentTarget 指向当前事件活动的对象(一般为父级)



### 如何派发事件(dispatchEvent)？（如何进行事件广播？）

* W3C: 使用 dispatchEvent 方法
* IE: 使用 fireEvent 方法

```javascript
var fireEvent = function(element, event)\\{
    if (document.createEventObject)\\{
        var mockEvent = document.createEventObject();
        return element.fireEvent('on' + event, mockEvent)
    \\}else\\{
        var mockEvent = document.createEvent('HTMLEvents');
        mockEvent.initEvent(event, true, true);
        return !element.dispatchEvent(mockEvent);
    \\}
\\}
```



## 跨域

> 因为浏览器出于安全考虑，有同源策略。也就是说，如果协议、域名或者端口有一个不同就是跨域，Ajax 请求会失败

### JSONP

> JSONP 的原理很简单，就是利用 <script> 标签没有跨域限制的漏洞。通过 <script> 标签指向一个需要访问的地址并提供一个回调函数来接收数据当需要通讯时

```html
<script src="http://domain/api?param1=a&param2=b&callback=jsonp"></script>
<script>
    function jsonp(data) \\{
    	console.log(data)
	\\}
</script>
```

- JSONP 使用简单且兼容性不错，但是只限于 get 请求



### CORS

- `CORS`需要浏览器和后端同时支持
- 浏览器会自动进行 `CORS` 通信，实现CORS通信的关键是后端。只要后端实现了 `CORS`，就实现了跨域。
- 服务端设置 `Access-Control-Allow-Origin` 就可以开启 `CORS`。 该属性表示哪些域名可以访问资源，如果设置通配符则表示所有网站都可以访问资源



### document.domain

- 该方式只能用于二级域名相同的情况下，比如 `a.test.com` 和 `b.test.com` 适用于该方式。
- 只需要给页面添加 `document.domain = 'test.com'` 表示二级域名都相同就可以实现跨域



### postMessage

> 这种方式通常用于获取嵌入页面中的第三方页面数据。一个页面发送消息，另一个页面判断来源并接收消息

```javascript
// 发送消息端
window.parent.postMessage('message', 'http://test.com');

// 接收消息端
var mc = new MessageChannel();
mc.addEventListener('message', (event) => \\{
    var origin = event.origin || event.originalEvent.origin; 
    if (origin === 'http://test.com') \\{
        console.log('验证通过')
    \\}
\\});
```



## Event loop

### JS中的event loop

> 众所周知 JS 是门非阻塞单线程语言，因为在最初 JS 就是为了和浏览器交互而诞生的。如果 JS 是门多线程的语言话，我们在多个线程中处理 DOM 就可能会发生问题（一个线程中新加节点，另一个线程中删除节点）

JS 在执行的过程中会产生执行环境，这些执行环境会被顺序的加入到执行栈中。如果遇到异步的代码，会被挂起并加入到 Task（有多种 task） 队列中。

一旦执行栈为空，Event Loop 就会从 Task 队列中拿出需要执行的代码并放入执行栈中执行，所以本质上来说 JS 中的异步还是同步行为。

```javascript
console.log('script start');

setTimeout(function() \\{
  console.log('setTimeout');
\\}, 0);

console.log('script end');
```

> 不同的任务源会被分配到不同的 `Task` 队列中，任务源可以分为 微任务（`microtask`） 和 宏任务（`macrotask`）。在 `ES6` 规范中，`microtask` 称为 jobs，macrotask 称为 task


```javascript
console.log('script start');

setTimeout(function() \\{
  console.log('setTimeout');
\\}, 0);

new Promise((resolve) => \\{
    console.log('Promise')
    resolve()
\\}).then(function() \\{
  console.log('promise1');
\\}).then(function() \\{
  console.log('promise2');
\\});

console.log('script end');
// script start => Promise => script end => promise1 => promise2 => setTimeout
```

> 以上代码虽然 `setTimeout` 写在 `Promise` 之前，但是因为 `Promise` 属于微任务而 `setTimeout` 属于宏任务

**微任务**

- `process.nextTick`
- `promise`
- `Object.observe`
- `MutationObserver`

**宏任务**

- `script `
- `setTimeout`
- `setInterval `
- `setImmediate `
- `I/O `
- `UI rendering`

> 宏任务中包括了 script ，浏览器会先执行一个宏任务，接下来有异步代码的话就先执行微任务

**所以正确的一次 Event loop 顺序是这样的**

- 执行同步代码，这属于宏任务
- 执行栈为空，查询是否有微任务需要执行
- 执行所有微任务
- 必要的话渲染 UI
- 然后开始下一轮 `Event loop`，执行宏任务中的异步代码

> 通过上述的 `Event loop` 顺序可知，如果宏任务中的异步代码有大量的计算并且需要操作 `DOM` 的话，为了更快的响应界面响应，我们可以把操作 `DOM` 放入微任务中



### Node 中的 Event loop

- `Node` 中的 `Event loop` 和浏览器中的不相同。
- `Node` 的 `Event loop` 分为`6`个阶段，它们会按照顺序反复运行


```javascript
┌───────────────────────┐
┌─>│        timers         │
│  └──────────┬────────────┘
│  ┌──────────┴────────────┐
│  │     I/O callbacks     │
│  └──────────┬────────────┘
│  ┌──────────┴────────────┐
│  │     idle, prepare     │
│  └──────────┬────────────┘      ┌───────────────┐
│  ┌──────────┴────────────┐      │   incoming:   │
│  │         poll          │<──connections───     │
│  └──────────┬────────────┘      │   data, etc.  │
│  ┌──────────┴────────────┐      └───────────────┘
│  │        check          │
│  └──────────┬────────────┘
│  ┌──────────┴────────────┐
└──┤    close callbacks    │
   └───────────────────────┘
```

**timer**

- `timers` 阶段会执行 `setTimeout` 和 `setInterval`
- 一个 timer 指定的时间并不是准确时间，而是在达到这个时间后尽快执行回调，可能会因为系统正在执行别的事务而延迟

**I/O**

- `I/O` 阶段会执行除了 `close` 事件，定时器和 `setImmediate` 的回调

idle, prepare
idle, prepare 阶段内部实现

**poll**

- `poll` 阶段很重要，这一阶段中，系统会做两件事情
  - 执行到点的定时器
  - 执行 `poll` 队列中的事件
  
- 并且当 poll 中没有定时器的情况下，会发现以下两件事情
  - 如果 poll 队列不为空，会遍历回调队列并同步执行，直到队列为空或者系统限制
  - 如果 poll 队列为空，会有两件事发生
  - 如果有 `setImmediate` 需要执行，`poll` 阶段会停止并且进入到 `check` 阶段执行 `setImmediate`
  - 如果没有 `setImmediate` 需要执行，会等待回调被加入到队列中并立即执行回调
  - 如果有别的定时器需要被执行，会回到 `timer` 阶段执行回调。

**check**

- `check` 阶段执行 `setImmediate`

**close callbacks**

- `close callbacks` 阶段执行 `close` 事件
- 并且在 `Node` 中，有些情况下的定时器执行顺序是随机的

```javascript
setTimeout(() => \\{
    console.log('setTimeout');
\\}, 0);
setImmediate(() => \\{
    console.log('setImmediate');
\\})
// 这里可能会输出 setTimeout，setImmediate
// 可能也会相反的输出，这取决于性能
// 因为可能进入 event loop 用了不到 1 毫秒，这时候会执行 setImmediate
// 否则会执行 setTimeout
```

> 上面介绍的都是 macrotask 的执行情况，microtask 会在以上每个阶段完成后立即执行

```javascript
setTimeout(()=>\\{
    console.log('timer1')

    Promise.resolve().then(function() \\{
        console.log('promise1')
    \\})
\\}, 0)

setTimeout(()=>\\{
    console.log('timer2')

    Promise.resolve().then(function() \\{
        console.log('promise2')
    \\})
\\}, 0)

// 以上代码在浏览器和 node 中打印情况是不同的
// 浏览器中一定打印 timer1, promise1, timer2, promise2
// node 中可能打印 timer1, timer2, promise1, promise2
// 也可能打印 timer1, promise1, timer2, promise2
```

> `Node` 中的 `process.nextTick` 会先于其他 `microtask` 执行


```javascript
setTimeout(() => \\{
 console.log("timer1");

 Promise.resolve().then(function() \\{
   console.log("promise1");
 \\});
\\}, 0);

process.nextTick(() => \\{
 console.log("nextTick");
\\});
// nextTick, timer1, promise1
```



## Service Worker代理服务器

> Service workers 本质上充当Web应用程序与浏览器之间的代理服务器，也可以在网络可用时作为浏览器和网络间的代理。
>
> 它们旨在（除其他之外）使得能够创建有效的离线体验，拦截网络请求并基于网络是否可用以及更新的资源是否驻留在服务器上来采取适当的动作。
>
> 他们还允许访问推送通知和后台同步API。

**目前该技术通常用来做缓存文件，提高首屏速度**

```javascript
// index.js
if (navigator.serviceWorker) \\{
  navigator.serviceWorker
    .register("sw.js")
    .then(function(registration) \\{
      console.log("service worker 注册成功");
    \\})
    .catch(function(err) \\{
      console.log("servcie worker 注册失败");
    \\});
\\}
// sw.js
// 监听 `install` 事件，回调中缓存所需文件
self.addEventListener("install", e => \\{
  e.waitUntil(
    caches.open("my-cache").then(function(cache) \\{
      return cache.addAll(["./index.html", "./index.js"]);
    \\})
  );
\\});

// 拦截所有请求事件
// 如果缓存中已经有请求的数据就直接用缓存，否则去请求数据
self.addEventListener("fetch", e => \\{
  e.respondWith(
    caches.match(e.request).then(function(response) \\{
      if (response) \\{
        return response;
      \\}
      console.log("fetch source");
    \\})
  );
\\});
```

> 打开页面，可以在开发者工具中的 Application 看到 Service Worker 已经启动了

![](https://user-gold-cdn.xitu.io/2018/3/28/1626b1e8eba68e1c?w=1770&h=722&f=png&s=192277)


> 在 Cache 中也可以发现我们所需的文件已被缓存

![](https://user-gold-cdn.xitu.io/2018/3/28/1626b20dfc4fcd26?w=1118&h=728&f=png&s=85610)

当我们重新刷新页面可以发现我们缓存的数据是从 Service Worker 中读取的



## 渲染机制

**浏览器的渲染机制一般分为以下几个步骤**

- 处理 `HTML` 并构建 `DOM` 树。
- 处理 `CSS` 构建 `CSSOM` 树。
- 将 `DOM` 与 `CSSOM` 合并成一个渲染树。
- 根据渲染树来布局，计算每个节点的位置。
- 调用 `GPU` 绘制，合成图层，显示在屏幕上

![](https://user-gold-cdn.xitu.io/2018/4/11/162b2ab2ec70ac5b?w=900&h=352&f=png&s=49983)

- 在构建 CSSOM 树时，会阻塞渲染，直至 CSSOM 树构建完成。并且构建 CSSOM 树是一个十分消耗性能的过程，所以应该尽量保证层级扁平，减少过度层叠，越是具体的 CSS 选择器，执行速度越慢
- 当 HTML 解析到 script 标签时，会暂停构建 DOM，完成后才会从暂停的地方重新开始。也就是说，如果你想首屏渲染的越快，就越不应该在首屏就加载 JS 文件。并且 CSS 也会影响 JS 的执行，只有当解析完样式表才会执行 JS，所以也可以认为这种情况下，CSS 也会暂停构建 DOM



### 浏览器的渲染过程

- 解析HTML构建 DOM(DOM树)，并行请求 css/image/js
- CSS 文件下载完成，开始构建 CSSOM(CSS树)（解析CSS生成CSSOM规则树）
- CSSOM 规则树构建结束后，和 DOM 一起生成 Render Tree(渲染树)
- 遍历渲染树开始布局(Layout)：计算出每个节点在屏幕中的位置、大小信息。
- 显示(Painting)：将渲染树每个节点绘制到屏幕（通过显卡把页面画到屏幕上）

解析：

- 使用 HTML 创建文档对象模型（DOM）
- 使用 CSS 创建 CSS 对象模型（CSSOM）
- 基于 DOM 和 CSSOM 执行脚本（Scripts）
- 合并 DOM 和 CSSOM 形成渲染树（Render Tree）
- 使用渲染树布局（Layout）所有元素
- 渲染（Paint）所有元素

[参考](https://jinlong.github.io/2017/05/08/optimising-the-front-end-for-the-browser/)



### DOM树 和 渲染树 的区别：

DOM树与HTML标签一一对应，包括head和隐藏元素

渲染树不包括head和隐藏元素，大段文本的每一个行都是独立节点，每一个节点都有对应的css属性



### 图层

> 一般来说，可以把普通文档流看成一个图层。特定的属性可以生成一个新的图层。
>
> 不同的图层渲染互不影响，所以对于某些频繁需要渲染的建议单独生成一个新图层，提高性能。
>
> 但也不能生成过多的图层，会引起反作用

**通过以下几个常用属性可以生成新图层**

- 3D 变换：`translate3d`、`translateZ`
- `will-change`
- `video`、`iframe` 标签
- 通过动画实现的 `opacity` 动画转换
- `position: fixed`



## 浏览器内核

### 常见的浏览器内核有哪些？

Trident 内核：IE,MaxThon,TT,The World,360,搜狗浏览器等。[又称 MSHTML]

Gecko 内核：Netscape6 及以上版本，FF,MozillaSuite/SeaMonkey 等

Presto 内核：Opera7 及以上。 [Opera 内核原为：Presto，现为：Blink;]

Webkit 内核：Safari,Chrome 等。 [ Chrome 的：Blink（WebKit 的分支）]



### 对浏览器内核的理解？

主要分成两部分：渲染引擎(layout engineer或Rendering Engine)和JS引擎。

渲染引擎：负责取得网页的内容（HTML、XML、图像等等）、整理讯息（例如加入CSS等），以及计算网页的显示方式，然后会输出至显示器或打印机。浏览器的内核的不同对于网页的语法解释会有不同，所以渲染的效果也不相同。所有网页浏览器、电子邮件客户端以及其它需要编辑、显示网络内容的应用程序都需要内核。

JS引擎则：解析和执行javascript来实现网页的动态效果。

最开始渲染引擎和JS引擎并没有区分的很明确，后来JS引擎越来越独立，内核就倾向于只指渲染引擎。
