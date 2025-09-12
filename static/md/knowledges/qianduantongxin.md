---
title: 前端通信
date: 2020-12-10 21:51:01
categories: 
- 前端知识
tags:
- 同源策略
- 通信方式
- Ajax
- JSON
- 跨域通信
- 异步
---


## 前言

**前端通信类的问题，主要包括以下内容**：

**前后端如何通信**：如果你不准备，估计也就只能说出`ajax`。这个可以考察出知识面。

**如何创建Ajax**

> `Ajax`在前后端通信中经常用到。做业务时，可以借助第三方的库，比如`vue`框架里的库、`jQuery`也有封装好的方法。但如果让你用原生的`js`去实现，该怎么做？

这就是考察你的动手能力，以及框架原理的掌握。如果能写出来，可以体现出你的基本功。是加分项。

> 在回答 `Ajax` 的问题时，要回答以下几个方面：

1. `XMLHttpRequest` 的工作原理
2. 兼容性处理

> `XMLHttpRequest`只有在高级浏览器中才支持。在回答问题时，这个兼容性问题不要忽略。

3. 事件的触发条件
4. 事件的触发顺序

> `XMLHttpRequest`有很多触发事件，每个事件是怎么触发的。

**跨域通信的几种方式**

> 这部分非常重要。无非就是问你：什么是跨域、跨域有什么限制、**跨域有几种方式**。



## 1.同源策略的概念和具体限制



### 请解释一下 JavaScript 的同源策略

**同源策略**：限制从一个源加载的文档或脚本如何与来自另一个源的资源进行交互。这是一个用于隔离潜在恶意文件的关键的安全机制。

是客户端脚本（尤其是 Javascript）的重要的安全度量标准。它最早出自 Netscape Navigator2.0，其目的是**防止某个文档或脚本从多个不同源装载**。

所谓**同源**指的是：协议，域名，端口相同，同源策略是一种安全协议，指一段脚本只能读取来自同一来源的窗口和文档的属性。

**具体解释：**

1. `源`包括三个部分：协议、域名、端口（`http`协议的默认端口是`80`）。如果有任何一个部分不同，则`源`不同，那就是跨域了。
2. `限制`：这个源的文档没有权利去操作另一个源的文档。这个限制体现在：（要记住）

- `Cookie`、`LocalStorage`和`IndexDB`无法获取。
- 无法获取和操作`DOM`。
- 不能发送`Ajax`请求。我们要注意，`Ajax`只适合**同源**的通信。



### 为什么要有同源限制？

我们举例说明：比如一个黑客程序，他利用Iframe把真正的银行登录页面嵌到他的页面上，当你使用真实的用户名，密码登录时，他的页面就可以通过Javascript读取到你的表单中input中的内容，这样用户名，密码就轻松到手了。

**缺点**

同源策略带来的麻烦：ajax 在不同域名下的请求无法实现，需要进行跨域操作

现在网站的JS都会进行压缩，一些文件用了严格模式，而另一些没有。这时这些本来是严格模式的文件，被 merge后，这个串就到了文件的中间，不仅没有指示严格模式，反而在压缩后浪费了字节。







## 2. 前后端如何通信

### 主要有以下几种方式：

- `Ajax`：不支持跨域。
- `WebSocket`：不受同源策略的限制，支持跨域
- `CORS`：不受同源策略的限制，支持跨域。一种新的通信协议标准。可以理解成是：**同时支持同源和跨域的Ajax**。



### 前后端通讯

1、**ajax**：短连接

2、**websocket** ：长连接，双向的。

　 node搭建的websocket服务器，推送信息给客户端浏览器 ：https://www.cnblogs.com/fps2tao/p/7875669.html （亲测有效，代码实现不难）

3、**server-sent event （简称 SSE）**：只是从服务器端往客户端单向传输数据。概念：http://www.ruanyifeng.com/blog/2017/05/server-sent_events.html 

  教程：http://www.runoob.com/html/html5-serversentevents.html （很简单的）

　 通过实践检测，感觉就隔几秒发送一个get请求获取数据（可能是因为PHP代码的程序不符合使用的代码）。 [ https://blog.csdn.net/iteye_5904/article/details/82648587](https://blog.csdn.net/iteye_5904/article/details/82648587) （）

4、使用EventSource实现页面消息推送 与 websocket 的区别 ： https://blog.csdn.net/bamboolsu/article/details/48653317

5、传统轮询,长轮询,EventSource与WebSocket ： https://blog.csdn.net/Holmofy/article/details/78111715

6、Web 实时推送技术的总结 ： [参考链接](https://mp.weixin.qq.com/s?__biz=MzAxODE2MjM1MA==&mid=2651556073&idx=1&sn=7009b6f2c95e3e48254964f43e838d9b&chksm=80255f28b752d63e89e5e96b3d462ea025bb7a4cc03783e5c8f8c86fcfdcb51b8d3c901035b8&mpshare=1&scene=1&srcid=#rd)

注：所有的通信都是由 客户端 先发起的(建立连接)。正是因为是客户端先发起的，所有客户端才会对返回的数据进行接受处理。不然服务器端先发起，客户端都没有和服务器建立连接怎么进行通信呢



### 多个页面之间如何进行通信

- cookie
- web worker
- localeStorage 和 sessionStorage







## Ajax



### 什么是 Ajax

Ajax 是全称是Asynchronous Javascript And XML，异步传输+js+xml，即异步 JavaScript 和 xml；

主要用来实现客户端与服务器异步数据交互，不用重载整个网页，实现页面局部刷新。

所谓异步，在这里简单地解释就是：向服务器发送请求的时候，我们不必等待结果，而是可以同时做其他的事情，等到有了结果它自己会根据设定进行后续操作，与此同时，页面是不会发生整页刷新的，提高了用户体验。



### ajax 的优点

1. 来自服务器的新内容可以动态更改，通过异步模式，无需重新加载整个页面，实现页面局部刷新
2. 避免用户不断刷新或者跳转页面，提高用户体验
3. 优化了浏览器和服务器之间的传输，降低数据传输量，减少不必要的数据往返，减少了带宽占用
4. Ajax 在客户端运行，承担了一部分本来由服务器承担的工作，减少了大用户量下的服务器负载。



### ajax 的缺点

1. ajax 不支持浏览器 back 按钮，要实现 ajax 下的前后退功能成本较大
2. 可能造成请求数的增加跨域问题限制；
3. 安全问题： AJAX 暴露了与服务器交互的细节。
4. 对搜索引擎的支持比较弱。
5. 破坏了程序的异常机制。



###  如何创建一个Ajax？

(1)创建XMLHttpRequest对象,也就是创建一个异步调用对象

(2)创建一个新的HTTP请求,并指定该HTTP请求的方法、URL及验证信息

(3)设置响应HTTP请求状态变化的函数

(4)发送HTTP请求

(5)获取异步调用返回的数据

(6)使用JavaScript和DOM实现局部刷新



### Ajax 是什么? 如何创建一个Ajax？

> ajax的全称：Asynchronous Javascript And XML

- 异步传输+js+xml
- 所谓异步，在这里简单地解释就是：向服务器发送请求的时候，我们不必等待结果，而是可以同时做其他的事情，等到有了结果它自己会根据设定进行后续操作，与此同时，页面是不会发生整页刷新的，提高了用户体验

- 创建XMLHttpRequest对象,也就是创建一个异步调用对象
- 建一个新的HTTP请求,并指定该HTTP请求的方法、URL及验证信息
- 设置响应HTTP请求状态变化的函数
- 发送HTTP请求
- 获取异步调用返回的数据
- 用JavaScript和DOM实现局部刷新



### 创建 ajax 过程

基本步骤 5步走：（创建对象、建立连接、发送数据、接收数据、局部刷新）

1.创建 XMLHttpRequest 对象,也就是创建一个异步调用对象

```
 var xhr=new XMLHttpRequest() //创建对象
```

2.创建一个新的 HTTP 请求,并指定该 HTTP 请求的方法、URL 及验证信息，跟服务器建立一个连接，设置响应 HTTP 请求状态变化的函数

```
xhr.open("type 提交方式", "url  提交的地址")

如果是post请求，需要设置请求头

xhr.setRequestHeader("Content-Type","application/x-www-form-urlencoded");
```

3.我要发送数据给服务器（发送 HTTP 请求）

​    如果是get 请求，请求的数据在地址的后面。

```
  xhr.send() //发送数据，这一步不能省略
```

4.获取异步调用服务器返回的数据
        服务端返回数据会调用一个回调函数，通过回调函数去接收数据.   

```
xhr.onreadystatechange=function()\\{
            if(xhr.readyState==4)\\{ 响应完成了
                    if(xhr.status==200)\\{ //响应成功了
                          responseText 属性接收服务端返回的数据.
                    \\}
            \\}
    \\}
```

5.使用 JavaScript 和 DOM 实现局部刷新



### 创建 `ajax` 步骤：

- 1.创建 `XMLHttpRequest` 对象
- 2.创建一个新的 `HTTP` 请求，并指定该 `HTTP` 请求的类型、验证信息
- 3.设置响应 `HTTP` 请求状态变化的回调函数
- 4.发送 `HTTP` 请求
- 5.获取异步调用返回的数据
- 6.使用 `JavaScript` 和 `DOM` 实现局部刷新

```js
var xhr = new XMLHttpRequest();
xhr.open("POST", url, true);
xhr.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
xhr.onreadystatechange = function () \\{
    if (xhr.readyState == 4 && (xhr.status == 200 || xhr.status == 304)) \\{
        fn.call(this, xhr.responseText);
    \\}
\\};
xhr.send(data);
```



### Ajax 实现的原理

浏览器提供的 XMLHttpRequest 对象



### ajax 如何实现，readyState 的五种状态的含义？

- 0 － （未初始化）还没有调用 send()方法
- 1 － （载入）已调用 send()方法，正在发送请求
- 2 － （载入完成）send()方法执行完成，已经接收到全部响应内容
- 3 － （交互）正在解析响应内容
- 4 － （完成）响应内容解析完成，可以在客户端调用了

解析：

(0)未初始化

此阶段确认 XMLHttpRequest 对象是否创建，并为调用 open()方法进行未初始化作好准备。值为 0 表示对象已经存在，否则浏览器会报错－－对象不存在。

(1)载入

此阶段对 XMLHttpRequest 对象进行初始化，即调用 open()方法，根据参数(method,url,true)完成对象状态的设置。并调用 send()方法开始向服务端发送请求。值为 1 表示正在向服务端发送请求。

(2)载入完成

此阶段接收服务器端的响应数据。但获得的还只是服务端响应的原始数据，并不能直接在客户端使用。值为 2 表示已经接收完全部响应数据。并为下一阶段对数据解析作好准备。

(3)交互

此阶段解析接收到的服务器端响应数据。即根据服务器端响应头部返回的 MIME 类型把数据转换成能通过 responseBody、responseText 或 responseXML 属性存取的格式，为在客户端调用作好准备。状态 3 表示正在解析数据。

(4)完成

此阶段确认全部数据都已经解析为客户端可用的格式，解析已经完成。值为 4 表示数据解析完毕，可以通过 XMLHttpRequest 对象的相应属性取得数据。

[参考](https://blog.csdn.net/u011565547/article/details/78979030)



### ajax 加载的页面，跳转到另外一个页面再跳转回来，内容相同，如何节约读取请求?

后台做缓存，读取缓存里面的数据。CDN



### Ajax 解决浏览器缓存问题？

1、在ajax发送请求前加上      anyAjaxObj.setRequestHeader("If-Modified-Since","0")。

2、在ajax发送请求前加上    anyAjaxObj.setRequestHeader("Cache-Control","no-cache")。

3、在URL后面加上一个随机数： "fresh=" + Math.random();。

4、在URL后面加上时间搓："nowtime=" + new Date().getTime();。

5、如果是使用jQuery，直接这样就可以了    $.ajaxSetup(\\{cache:false\\})。这样页面的所有ajax都会执行这条语句就是不需要保存缓存记录



### GET 和 POST 的区别，何时使用 POST？

**GET：**

- 一般用于信息获取，使用 URL 传递参数，对所发送信息的数量也有限制，一般在 2000 个字符，有的浏览器是 8000 个字符；
- 请求的参数都暴露在 url 地址当中，如果传递中文参数，需要自己进行编码操作，安全性较低。

**POST：**

- 一般用于提交数据和修改服务器上的资源，对所发送的信息没有限制
- 提交的数据内容存在于 http 请求体中，数据不会暴漏在 url 地址中。

**在以下情况中，请使用 POST 请求：**

1. 无法使用缓存文件（更新服务器上的文件或数据库）
2. 向服务器发送大量数据（POST 没有数据量限制）
3. 发送包含未知字符的用户输入时，POST 比 GET 更稳定也更可靠



### ajax 请求时，如何解析 json 数据

使用 eval() 或者 JSON.parse() 鉴于安全性考虑，推荐使用 JSON.parse()更靠谱，对数据的安全性更好。



### 发送 get 请求和 post 请求

> `get`请求举例：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
<h1>Ajax 发送 get 请求</h1>
<input type="button" value="发送get_ajax请求" id='btnAjax'>

<script type="text/javascript">
    // 绑定点击事件
    document.querySelector('#btnAjax').onclick = function () \\{
        // 发送ajax 请求 需要 五步

        // （1）创建异步对象
        var ajaxObj = new XMLHttpRequest();

        // （2）设置请求的参数。包括：请求的方法、请求的url。
        ajaxObj.open('get', '02-ajax.php');

        // （3）发送请求
        ajaxObj.send();

        //（4）注册事件。 onreadystatechange事件，状态改变时就会调用。
        //如果要在数据完整请求回来的时候才调用，我们需要手动写一些判断的逻辑。
        ajaxObj.onreadystatechange = function () \\{
            // 为了保证 数据 完整返回，我们一般会判断 两个值
            if (ajaxObj.readyState == 4 && ajaxObj.status == 200) \\{
                // 如果能够进到这个判断 说明 数据 完美的回来了,并且请求的页面是存在的
                // 5.在注册的事件中 获取 返回的 内容 并修改页面的显示
                console.log('数据返回成功');

                // 数据是保存在 异步对象的 属性中
                console.log(ajaxObj.responseText);

                // 修改页面的显示
                document.querySelector('h1').innerHTML = ajaxObj.responseText;
            \\}
        \\}
    \\}
</script>
</body>
</html>
```

> `post` 请求举例：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
<h1>Ajax 发送 get 请求</h1>
<input type="button" value="发送put_ajax请求" id='btnAjax'>
<script type="text/javascript">

    // 异步对象
    var xhr = new XMLHttpRequest();

    // 设置属性
    xhr.open('post', '02.post.php');

    // 如果想要使用post提交数据,必须添加此行
    xhr.setRequestHeader("Content-type", "application/x-www-form-urlencoded");

    // 将数据通过send方法传递
    xhr.send('name=fox&age=18');

    // 发送并接受返回值
    xhr.onreadystatechange = function () \\{
        // 这步为判断服务器是否正确响应
        if (xhr.readyState == 4 && xhr.status == 200) \\{
            alert(xhr.responseText);
        \\}
    \\};
</script>
</body>
</html>
```



### onreadystatechange 事件

> 注册 `onreadystatechange` 事件后，每当 `readyState` 属性改变时，就会调用 `onreadystatechange` 函数。

> `readyState`：（存有 `XMLHttpRequest` 的状态。从 `0` 到 `4` 发生变化）

- `0`: 请求未初始化
- `1`: 服务器连接已建立
- `2`: 请求已接收
- `3`: 请求处理中
- `4`: 请求已完成，且响应已就绪



### 事件的触发条件

![](http://img.smyhvae.com/20180307_1443.png)



### 事件的触发顺序

![](http://img.smyhvae.com/20180307_1445.png)



### 实际开发中用的 原生Ajax请求

```javascript

    var util = \\{\\};

    //获取 ajax 请求之后的json
    util.json = function (options) \\{

        var opt = \\{
            url: '',
            type: 'get',
            data: \\{\\},
            success: function () \\{
            \\},
            error: function () \\{
            \\},

        \\};
        util.extend(opt, options);
        if (opt.url) \\{
            //IE兼容性处理：浏览器特征检查。检查该浏览器是否存在XMLHttpRequest这个api，没有的话，就用IE的api
            var xhr = XMLHttpRequest ? new XMLHttpRequest() : new window.ActiveXObject('Microsoft.XMLHTTP');

            var data = opt.data,
                url = opt.url,
                type = opt.type.toUpperCase();
            dataArr = [];
        \\}

        for (var key in data) \\{
            dataArr.push(key + '=' + data[key]);
        \\}

        if (type === 'GET') \\{
            url = url + '?' + dataArr.join('&');
            xhr.open(type, url.replace(/\?$/g, ''), true);
            xhr.send();
        \\}

        if (type === 'POST') \\{
            xhr.open(type, url, true);
            // 如果想要使用post提交数据,必须添加此行
            xhr.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
            xhr.send(dataArr.join('&'));
        \\}

        xhr.onload = function () \\{
            if (xhr.status === 200 || xhr.status === 304) \\{ //304表示：用缓存即可。206表示获取媒体资源的前面一部分
                var res;
                if (opt.success && opt.success instanceof Function) \\{
                    res = xhr.responseText;
                    if (typeof res === 'string') \\{
                        res = JSON.parse(res);  //将字符串转成json
                        opt.success.call(xhr, res);
                    \\}
                \\}
            \\} else \\{
                if (opt.error && opt.error instanceof Function) \\{
                    opt.error.call(xhr, res);
                \\}
            \\}
        \\};
    \\}


```

参考链接：

http://www.runoob.com/ajax/ajax-tutorial.html

http://3ms.huawei.com/km/blogs/details/5434911







## 4.json

### 什么是 json

- JSON(JavaScript Object Notation) 是一种轻量级的数据交换格式
- 它是基于JavaScript的一个子集。数据格式简单, 易于读写, 占用带宽小
- JSON字符串转换为JSON对象:

```
var obj =eval('('+ str +')');
var obj = str.parseJSON();
var obj = JSON.parse(str);
```

- JSON对象转换为JSON字符串：

```
var last=obj.toJSONString();
var last=JSON.stringify(obj);
```



### json优点:

1. 数据格式比较简单，易于读写，支持复合数据类型（数组、对象、字符串、数字）
2.  轻量级，格式都是压缩的，占用带宽小
3. 便于机器（JavaScript）解析, 客户端 javascript 可以简单的通过 eval()进行 JSON 数据的读取搜索
4. 支持多种语言, 包括 ActionScript, C, C#, ColdFusion, Java, JavaScript, Perl, php, Python, Ruby 等语言服务器端语言, 便于服务器端的解析
5. 在 PHP 世界, 已经有 PHP-JSON 和 JSON-PHP 出现了, 便于 PHP 序列化后的程序直接调用. PHP 服务器端的对象、数组等能够直接生 JSON 格式, 便于客户端的访问提取. 另外 PHP 的 PEAR 类已经提出了支持 (http://pear.php.net/pepr/pepr-proposal-show.php?id=198)
6. 因为 JSON 格式能够直接为服务器端代码使用, 大大简化了服务器端和客户端的代码开发量, 但是完成的任务不变, 且易于维护



### json缺点:

1. 没有 XML 格式这么推广的深入人心和使用广泛, 没有 XML 那么通用性
2. JSON 格式目前在 Web Service 中推广还属于初级阶段 PS: 据说 Google 的 Ajax 是使用 JSON+模板 做的



### XML和JSON的区别？

- 数据体积方面
  - JSON相对于XML来讲，数据的体积小，传递的速度更快些。
- 数据交互方面
  - JSON与JavaScript的交互更加方便，更容易解析处理，更好的数据交互
- 数据描述方面
  - JSON对数据的描述性比XML较差
- 传输速度方面
  - JSON的速度要远远快于XML







## 5.跨域



### 如何解决跨域问题?

jsonp、 iframe、window.name、window.postMessage、服务器上设置代理页面



### 如何解决跨域问题?

1. jsonp ，允许 script 加载第三方资源
2. 反向代理（nginx 服务内部配置 Access-Control-Allow-Origin \*）
3. cors 前后端协作设置请求头部，Access-Control-Allow-Origin 等头部信息
4. iframe 嵌套通讯，postmessage

解析：

理解跨域的概念：协议、域名、端口都相同才同域，否则都是跨域

[参考](https://zhuanlan.zhihu.com/p/41479807)
[跨域资源共享 CORS 阮一峰](http://www.ruanyifeng.com/blog/2016/04/cors.html)



### 跨域通信的几种方式

> 方式如下：

1. `JSONP`
2. `WebSocket`
3. `CORS`
4. `Hash`
5. `postMessage`

> 上面这五种方式，在面试时，都要说出来。

### 5.1 JSONP

> 面试会问：`JSONP`的原理是什么？怎么实现的？

- 在`CORS`和`postMessage`以前，我们一直都是通过`JSONP`来做跨域通信的。

> **JSONP的原理**：通过`<script>`标签的异步加载来实现的。比如说，实际开发中，我们发现，`head`标签里，可以通过`<script>`标签的`src`，里面放`url`，加载很多在线的插件。这就是用到了`JSONP`。

**JSONP的实现：**

> 比如说，客户端这样写：

```html
    <script src="http://www.smyhvae.com/?data=name&callback=myjsonp"></script>
```

> 上面的`src`中，`data=name`是get请求的参数，`myjsonp`是和后台约定好的函数名。
服务器端这样写：

```js
  myjsonp(\\{
      data: \\{\\}

  \\})
```


> 于是，本地要求创建一个`myjsonp` 的**全局函数**，才能将返回的数据执行出来。

**实际开发中，前端的JSONP是这样实现的：**

```html
<script>

    var util = \\{\\};

    //定义方法：动态创建 script 标签
    /**
     * [function 在页面中注入js脚本]
     * @param  \\{[type]\\} url     [description]
     * @param  \\{[type]\\} charset [description]
     * @return \\{[type]\\}         [description]
     */
    util.createScript = function (url, charset) \\{
        var script = document.createElement('script');
        script.setAttribute('type', 'text/javascript');
        charset && script.setAttribute('charset', charset);
        script.setAttribute('src', url);
        script.async = true;
        return script;
    \\};


    /**
     * [function 处理jsonp]
     * @param  \\{[type]\\} url      [description]
     * @param  \\{[type]\\} onsucess [description]
     * @param  \\{[type]\\} onerror  [description]
     * @param  \\{[type]\\} charset  [description]
     * @return \\{[type]\\}          [description]
     */
    util.jsonp = function (url, onsuccess, onerror, charset) \\{
        var callbackName = util.getName('tt_player'); //事先约定好的 函数名
        window[callbackName] = function () \\{      //根据回调名称注册一个全局的函数
            if (onsuccess && util.isFunction(onsuccess)) \\{
                onsuccess(arguments[0]);
            \\}
        \\};
        var script = util.createScript(url + '&callback=' + callbackName, charset);   //动态创建一个script标签
        script.onload = script.onreadystatechange = function () \\{   //监听加载成功的事件，获取数据
            if (!script.readyState || /loaded|complete/.test(script.readyState)) \\{
                script.onload = script.onreadystatechange = null;
                // 移除该script的 DOM 对象
                if (script.parentNode) \\{
                    script.parentNode.removeChild(script);
                \\}
                // 删除函数或变量
                window[callbackName] = null;  //最后不要忘了删除
            \\}
        \\};
        script.onerror = function () \\{
            if (onerror && util.isFunction(onerror)) \\{
                onerror();
            \\}
        \\};
        document.getElementsByTagName('head')[0].appendChild(script); //往html中增加这个标签，目的是把请求发送出去
    \\};

</script>

```

### 5.2 WebSocket

> `WebSocket`的用法如下：

```javascript
    //

    var ws = new WebSocket('wss://echo.websocket.org'); //创建WebSocket的对象。参数可以是 ws 或 wss，后者表示加密。

    //把请求发出去
    ws.onopen = function (evt) \\{
        console.log('Connection open ...');
        ws.send('Hello WebSockets!');
    \\};


    //对方发消息过来时，我接收
    ws.onmessage = function (evt) \\{
        console.log('Received Message: ', evt.data);
        ws.close();
    \\};

    //关闭连接
    ws.onclose = function (evt) \\{
        console.log('Connection closed.');
    \\};
```

> 面试一般不会让你写这个代码，一般是考察你是否了解 `WebSocket`概念，知道有这么回事即可。

### 5.3 CORS

> `CORS` 可以理解成是**既可以同步、也可以异步**的Ajax。

- fetch` 是一个比较新的`API`，用来实现`CORS`通信。用法如下：

```javascript
      // url（必选），options（可选）
      fetch('/some/url/', \\{
          method: 'get',
      \\}).then(function (response) \\{  //类似于 ES6中的promise

      \\}).catch(function (err) \\{
        // 出错了，等价于 then 的第二个参数，但这样更好用更直观
      \\});
```

> 另外，如果面试官问：“CORS为什么支持跨域的通信？”

> 答案：跨域时，浏览器会拦截`Ajax`请求，并在`http`头中加`Origin`。

### 5.4 Hash

- `url`的`#`后面的内容就叫`Hash`。**Hash的改变，页面不会刷新**。这就是用 `Hash` 做跨域通信的基本原理。

> 补充：`url`的`?`后面的内容叫`Search`。`Search`的改变，会导致页面刷新，因此不能做跨域通信。

**使用举例：**

**场景**：我的页面 `A` 通过`iframe`或`frame`嵌入了跨域的页面 `B`。

> 现在，我这个`A`页面想给`B`页面发消息，怎么操作呢？

1. 首先，在我的`A`页面中：

```javascript
    //伪代码
    var B = document.getElementsByTagName('iframe');
    B.src = B.src + '#' + 'jsonString';  //我们可以把JS 对象，通过 JSON.stringify()方法转成 json字符串，发给 B
```

2. 然后，在`B`页面中：

```javascript
    // B中的伪代码
    window.onhashchange = function () \\{  //通过onhashchange方法监听，url中的 hash 是否发生变化
        var data = window.location.hash;
    \\};
```

### 5.5 postMessage()方法

> `H5`中新增的`postMessage()``方法，可以用来做跨域通信。既然是H5中新增的，那就一定要提到。

**场景**：窗口 A (`http:A.com`)向跨域的窗口 B (`http:B.com`)发送信息。步骤如下

1. 在`A`窗口中操作如下：向`B`窗口发送数据：


```javascript
	// 窗口A(http:A.com)向跨域的窗口B(http:B.com)发送信息
 	Bwindow.postMessage('data', 'http://B.com'); //这里强调的是B窗口里的window对象
```

2. 在`B`窗口中操作如下：

```javascript
    // 在窗口B中监听 message 事件
    Awindow.addEventListener('message', function (event) \\{   //这里强调的是A窗口里的window对象
        console.log(event.origin);  //获取 ：url。这里指：http://A.com
        console.log(event.source);  //获取：A window对象
        console.log(event.data);    //获取传过来的数据
    \\}, false);
```



### 如何解决跨域问题

###### **JSONP：**

- 原理是：动态插入`script`标签，通过`script`标签引入一个`js`文件，这个`js`文件载入成功后会执行我们在`url`参数中指定的函数，并且会把我们需要的`json`数据作为参数传入
- 由于同源策略的限制，`XmlHttpRequest`只允许请求当前源（域名、协议、端口）的资源，为了实现跨域请求，可以通过`script`标签实现跨域请求，然后在服务端输出`JSON`数据并执行回调函数，从而解决了跨域的数据请求
- 优点是兼容性好，简单易用，支持浏览器与服务器双向通信。缺点是只支持GET请求
- `JSONP`：`json+padding`（内填充），顾名思义，就是把`JSON`填充到一个盒子里

```js
  function createJs(sUrl)\\{

      var oScript = document.createElement('script');
      oScript.type = 'text/javascript';
      oScript.src = sUrl;
      document.getElementsByTagName('head')[0].appendChild(oScript);
  \\}

  createJs('jsonp.js');

  box(\\{
     'name': 'test'
  \\});

  function box(json)\\{
      alert(json.name);
  \\}
```

**CORS**

- 服务器端对于`CORS`的支持，主要就是通过设置`Access-Control-Allow-Origin`来进行的。如果浏览器检测到相应的设置，就可以允许`Ajax`进行跨域的访问

**通过修改document.domain来跨子域**

- 将子域和主域的`document.domain`设为同一个主域.前提条件：这两个域名必须属于同一个基础域名!而且所用的协议，端口都要一致，否则无法利用`document.domain`进行跨域。主域相同的使用`document.domain`

**使用window.name来进行跨域**

- `window`对象有个name属性，该属性有个特征：即在一个窗口(`window`)的生命周期内,窗口载入的所有的页面都是共享一个`window.name`的，每个页面对window.name都有读写的权限，`window.name`是持久存在一个窗口载入过的所有页面中的

**使用HTML5中新引进的window.postMessage方法来跨域传送数据**

- 还有`flash`、在服务器上设置代理页面等跨域方式。个人认为`window.name`的方法既不复杂，也能兼容到几乎所有浏览器，这真是极好的一种跨域方法

**如何解决跨域问题?**

- `jsonp`、 `iframe`、`window.name`、`window.postMessage`、服务器上设置代理页面
- 如何解决跨域问题?
  - `document.domain + iframe`：要求主域名相同 //只能跨子域
  - `JSONP(JSON with Padding)``：`response: callback(data)`` //只支持 GET 请求
  - 跨域资源共享`CORS(XHR2)``：`Access-Control-Allow` //兼容性 IE10+
  - 跨文档消息传输(HTML5)：`postMessage + onmessage`  //兼容性 IE8+
  - `WebSocket(HTML5)：new WebSocket(url) + onmessage` //兼容性 IE10+
  - 服务器端设置代理请求：服务器端不受同源策略限制



### 5.1 跨域

> 很多种方法，但万变不离其宗，都是为了搞定同源策略。重用的有 `jsonp`、`iframe`、`cors`、`img`、H`TML5 postMessage`等等。其中用到 `html` 标签进行跨域的原理就是 `html` 不受同源策略影响。但只是接受 `Get` 的请求方式，这个得清楚。

> **延伸1：img iframe script 来发送跨域请求有什么优缺点？**

**1. `iframe`**

- 优点：跨域完毕之后`DOM`操作和互相之间的`JavaScript`调用都是没有问题的
- 缺点：1.若结果要以`URL`参数传递，这就意味着在结果数据量很大的时候需要分割传递，巨烦。2.还有一个是`iframe`本身带来的，母页面和`iframe`本身的交互本身就有安全性限制。

**2. script**

- 优点：可以直接返回`json`格式的数据，方便处理
- 缺点：只接受`GET`请求方式

**3. 图片ping**

- 优点：可以访问任何`url`，一般用来进行点击追踪，做页面分析常用的方法
- 缺点：不能访问响应文本，只能监听是否响应

> **延伸2：配合 webpack 进行反向代理？**

`webpack` 在 `devServer` 选项里面提供了一个 `proxy` 的参数供开发人员进行反向代理

```js
'/api': \\{
  target: 'http://www.example.com', // your target host
  changeOrigin: true, // needed for virtual hosted sites
  pathRewrite: \\{
    '^/api': ''  // rewrite path
  \\}
\\},
```

> 然后再配合 `http-proxy-middleware` 插件对 `api` 请求地址进行代理

```js
const express = require('express');
const proxy = require('http-proxy-middleware');
// proxy api requests
const exampleProxy = proxy(options); // 这里的 options 就是 webpack 里面的 proxy 选项对应的每个选项

// mount `exampleProxy` in web server
const app = express();
app.use('/api', exampleProxy);
app.listen(3000);
```

> 然后再用 `nginx` 把允许跨域的源地址添加到报头里面即可

> 说到 `nginx` ，可以再谈谈 `CORS` 配置，大致如下

```js
location / \\{
  if ($request_method = 'OPTIONS') \\{
    add_header 'Access-Control-Allow-Origin' '*';  
    add_header 'Access-Control-Allow-Methods' 'GET, POST, OPTIONS'; 
    add_header 'Access-Control-Allow-Credentials' 'true';
    add_header 'Access-Control-Allow-Headers' 'DNT, X-Mx-ReqToken, Keep-Alive, User-Agent, X-Requested-With, If-Modified-Since, Cache-Control, Content-Type';  
    add_header 'Access-Control-Max-Age' 86400;  
    add_header 'Content-Type' 'text/plain charset=UTF-8';  
    add_header 'Content-Length' 0;  
    return 200;  
  \\}
\\}
```



### 解释 jsonp 的原理，以及为什么不是真正的 ajax

jsonp 是用来解决跨域获取数据的一种解决方案，具体是通过动态创建 script 标签，然后通过标签的 src 属性获取 js 文件中的 js 脚本，该脚本的内容是一个函数调用，参数就是服务器返回的数据，为了处理这些返回的数据，需要事先在页面定义好回调函数，本质上使用的并不是 ajax 技术



### jsonp 优缺点

优点

完美解决在测试或者开发中获取不同域下的数据,用户传递一个 callback 参数给服务端，然后服务端返回数据时会将这个 callback 参数作为函数名来包裹住 JSON 数据，这样客户端就可以随意定制自己的函数来自动处理**返回数据了。简单来说数据的格式没有发生很大变化**

- 它不像 XMLHttpRequest 对象实现的 Ajax 请求那样受到同源策略的限制，JSONP 可以跨越同源策略；
- 它的兼容性更好，在更加古老的浏览器中都可以运行，不需要 XMLHttpRequest 或 ActiveX 的支持
- 在请求完毕后可以通过调用 callback 的方式回传结果。将回调方法的权限给了调用方。这个就相当于将 controller 层和 view 层终于*分 开了。我提供的 jsonp 服务只提供纯服务的数据，至于提供服务以 后的页面渲染和后续 view 操作都由调用者来自己定义就好了。如果*有两个页面需要渲染同一份数据，你们只需要有不同的渲染逻辑就可以了，逻辑都可以使用同 一个 jsonp 服务。

缺点

- 它只支持 GET 请求而不支持 POST 等其它类型的 HTTP 请求，

  也即是说如果想传给后台一个 json 格式的数据,此时问题就来了,浏览器会报一个 http 状态码 415 错误,告诉你请求格式不正确,这让我很蛋疼(在登录注册中需要给后台传一大串数据),如果都用参数的形式拼接在 url 后面的话不太现实,后台取值也会显得繁琐。

- 它只支持跨域 HTTP 请求这种情况，不能解决不同域的两个页面之间如何进行 JavaScript 调用的问题。

- jsonp 在调用失败的时候不会返回各种 HTTP 状态码。

- 在登录模块中需要用到 session 来判断当前用户的登录状态,这时候由于是跨域的原因,前后台的取到的 session 是不一样的,那么就不能就行 session 来判断.

- 缺点是安全性。万一假如提供 jsonp 的服务存在页面注入漏洞，即它返回的 javascript 的内容被人控制的。那么结果是什么？所有调用这个 jsonp 的网站都会存在漏洞。于是无法把危险控制在一个域名下。所以在使用 jsonp 的时候必须要保证使用的 jsonp 服务必须是安全可信的

  由于 jsonp 存在安全性问题(不知 qq 空间的跨域是怎么解决的,还是另有高招?)，后来考虑到上面的一系列问题,采用的是后台进行设置允许跨域请求(但还是存在缺陷的,实质上还是跨域,如上面说的 session 问题).Header set Access-Control-Allow-Origin

  为了防止 XSS 攻击我们的服务器， 我们可以限制域，比如 Access-Control-Allow-Origin: http://blog.csdn.net







## 6.其他

### 同步和异步的区别?

**同步：阻塞的**

-张三叫李四去吃饭，李四一直忙得不停，张三一直等着，直到李四忙完两个人一块去吃饭

=浏览器向服务器请求数据，服务器比较忙，浏览器一直等着（页面白屏），直到服务器返回数据，浏览器才能显示页面

**异步：非阻塞的**

-张三叫李四去吃饭，李四在忙，张三说了一声然后自己就去吃饭了，李四忙完后自己去吃

=浏览器向服务器请求数据，服务器比较忙，浏览器可以自如的干原来的事情（显示页面），服务器返回数据的时候通知浏览器一声，浏览器把返回的数据再渲染到页面，局部更新



### 异步加载和延迟加载

1.异步加载的方案： 动态插入 script 标签

2.通过 ajax 去获取 js 代码，然后通过 eval 执行

3.script 标签上添加 defer 或者 async 属性

4.创建并插入 iframe，让它异步执行 js

5.延迟加载：有些 js 代码并不是页面初始化的时候就立刻需要的，而稍后的某些情况才需要的。



### 一个页面从输入 URL 到页面加载显示完成，这个过程中都发生了什么？

1.浏览器地址栏输入 url

2.浏览器会先查看浏览器缓存--系统缓存--路由缓存，如有存在缓存，就直接显示。如果没有，接着第三步

3.域名解析（DNS）获取相应的 ip

4.浏览器向服务器发起 tcp 连接，与浏览器建立 tcp 三次握手

5.握手成功，浏览器向服务器发送 http 请求，请求数据包

6.服务器请求数据，将数据返回到浏览器

7.浏览器接收响应，读取页面内容，解析 html 源码，生成 DOm 树

8.解析 css 样式.浏览器渲染，js 交互绑定多个域名，数量不限；



### 页面编码和被请求的资源编码如果不一致如何处理？

答案：get 请求中的中文需要 encodeURIComponent 编码处理，post 请求不需要进行编码



### Ajax 和 Fetch 区别

- ajax 是使用 XMLHttpRequest 对象发起的，但是用起来很麻烦，所以 ES6 新规范就有了 fetch，fetch 发一个请求不用像 ajax 那样写一大堆代码。
- 使用 fetch 无法取消一个请求，这是因为 fetch 基于 Promise，而 Promise 无法做到这一点。
- 在默认情况下，fetch 不会接受或者发送 cookies
- fetch 没有办法原生监测请求的进度，而 XMLHttpRequest 可以
- fetch 只对网络请求报错，对 400，500 都当做成功的请求，需要封装去处理
- fetch 由于是 ES6 规范，兼容性上比不上 XMLHttpRequest



### XML 和 JSON 的区别？

- 数据体积方面：JSON 相对于 XML 来讲，数据的体积小，传递的速度更快些。
- 数据交互方面：JSON 与 JavaScript 的交互更加方便，更容易解析处理，更好的数据交互。
- 数据描述方面：JSON 对数据的描述性比 XML 较差。
- 传输速度方面：JSON 的速度要远远快于 XML。



### RESTful

REST 指的是**一组架构约束条件和原则**。满足这些约束条件和原则的应用程序或设计就是 RESTful。

- **GET**

  get 方法在 Rest 中主要用于获取资源，能够发送参数，不过有限制，且参数都会以?开头的形 式附加在 URL 尾部。
  规范的 get 方法处理器应该是幂等的，也就是说对一个资源不论发送多少次 get 请求都不会更改数据或造成破坏。

- **POST**
  post 方法在 Rest 请求中主要用于添加资源，参数信息存放在请求报文的消息体中相对安全，且可发送较大信息

- **PUT**
  put 方法在 Rest 中主要用于更新资源，因为大多数浏览器不支持 put 和 delete，会自动将 put 和 delete 请求转化为 get 和 post. 因此为了使用 put 和 delete 方法,
  需要以 post 发送请求，在表单中使用隐藏域发送真正的请求。
  put 方法的参数是同 post 一样是存放在消息中的，同样具有安全性，可发送较大信息。
  put 方法是幂等的，对同一 URL 资源做出的同一数据的任意次 put 请求其对数据的改变都是一致的。

- **DELETE**
  Delete 在 Rest 请求中主要用于删除资源，因为大多数浏览器不支持 put 和 delete，会自动将 put 和 delete 请求转化为 get 和 post。
  因此为了使用 put 和 delete 方法,需要以 post 发送请求，在表单中使用隐藏域发送真正的请求。
  Delete 方法的参数同 post 一样存放在消息体中,具有安全性，可发送较大信息 Delete 方法是幂等的，不论对同一个资源进行多少次 delete 请求都不会破坏数据

解析：[参考](https://blog.csdn.net/jnshu_it/article/details/80203696)



### withCredentials详细介绍

withCredentials是一个布尔值，用于指定是否在跨域请求中发送身份凭据（如cookie，HTTP认证和客户端SSL证明），默认为false。

跨域请求通常被浏览器限制，因为它们可能会引发安全风险。浏览器将通常只向同域发送身份凭据。然而，有时候我们需要在跨域请求中发送身份凭据，以实现认证、授权或其他相关功能。

当withCredentials设置为true时，浏览器在发送跨域请求时会包含身份凭据。服务器必须正确配置CORS（跨域资源共享）以接受带有身份凭据的请求。如果服务器没有正确配置CORS，浏览器将拒绝响应。

下面是一个使用withCredentials的示例：

```javascript
var xhr = new XMLHttpRequest();
xhr.withCredentials = true;
xhr.open('POST', 'https://api.example.com/login', true);
xhr.onreadystatechange = function() \\{
  if (xhr.readyState === 4 && xhr.status === 200) \\{
    // 处理响应
  \\}
\\};
xhr.send();
```

在这个示例中，我们创建了一个XMLHttpRequest对象，并将withCredentials设置为true。然后，我们打开一个跨域请求，并监听xhr对象的onreadystatechange事件。当请求完成并成功时（readyState为4且status为200），我们可以处理响应。

请注意，在跨域请求中发送身份凭据可能会导致安全风险。确保只在必要的情况下使用withCredentials，并在服务器端正确配置CORS以确保安全性。

