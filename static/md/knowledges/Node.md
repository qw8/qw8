---
title: Node
date: 2019-12-08 19:25:55
categories: 
- 前端知识
tags:
- Node
---
### 对 Node 的优点和缺点提出了自己的看法？

**优点：**

1. 因为 Node 是基于事件驱动和无阻塞的，所以非常适合处理并发请求，因此构建在 Node 上的代理服务器相比其他技术实现（如 Ruby）的服务器表现要好得多。
2. 与 Node 代理服务器交互的客户端代码是由 javascript 语言编写的，因此客户端和服务器端都用同一种语言编写，这是非常美妙的事情。
3. 擅长处理高并发，适合I/O密集型应用。
4. 事件驱动，通过闭包很容易实现客户端的生命活期。
5. 不用担心多线程，锁，并行计算的问题。
6. V8 引擎速度非常快。
7. 对于游戏来说，写一遍游戏逻辑代码，前端后端通用。

**缺点：**

1. Node 是一个相对新的开源项目，所以不太稳定，它总是一直在变。nodejs 更新很快，可能会出现版本兼容；还不算成熟，还没有大制作；
2. nodejs 不像其他的服务器，对于不同的链接，不支持进程和线程操作
3. 不适合CPU密集运算；不能充分利用多核CPU；可靠性低，某个环节出错会导致整个系统崩溃



### Node 的应用场景

- RESTFUL API
- 工具类应用：前端部署(npm, gulp)

- 实时应用：如实时在线聊天，图文直播，实时通知推送等等（如 socket.io）
- 客户端逻辑强大的单页 APP：本地化的在线音乐应用，本地化的在线搜索应用，本地化的在线 APP 等。
- 分布式应用：通过高效的并行 I/O 使用已有的数据
- 工具类应用：海量的工具，小到前端压缩部署（如 grunt），大到桌面图形界面应用程序
- 游戏类应用：游戏领域对实时和并发有很高的要求（如网易的 pomelo 框架）
- 利用稳定接口提升 Web 渲染能力
- 前后端编程语言环境统一：前端开发人员可以非常快速地切入到服务器端的开发（如著名的纯 Javascript 全栈式 MEAN 架构）

[参考](https://www.cnblogs.com/kevin9103/p/5053517.html)



### node有哪些特征，与其他服务器端对比

　　特征：单线程、事件驱动、非阻塞I/O

　　node 无法直接渲染静态页面，提供静态服务

　　node 没有根目录的概念

　　node 必须通过路由程序指定文件才能渲染文件

　　node 比其他服务端性能更好，速度更快

 

### Node.js简介

简单的说 Node.js 就是运行在服务端的 JavaScript。Node.js 是一个基于 [Chrome V8](https://developers.google.com/v8/) 引擎的 JavaScript 运行环境。Node.js 使用了一个事件驱动、非阻塞式 I/O 的模型，使其轻量又高效。Node.js 的包管理器 [npm](https://www.npmjs.com/)，是全球最大的开源库生态系统。



### 下载安装Node.js

打开官网下载链接:https://nodejs.org/en/download/ 我下载的是node-v14.17.5-x64.mis，下载完成后，双击文件开始安装Node.js；

点击【Next】按钮，勾选复选框；

D盘新建node目录，点击【Next】按钮，修改好目录后，点击【Next】按钮，点击【Next】按钮；

勾选复选框，点击【Next】按钮；

点击【Install】按钮；

安装完后点击【Finish】按钮完成安装。

至此Node.js已经安装完成，可以先进行下简单的测试安装是否成功了，后面还要进行环境配置
在键盘按下【win+R】键，输入cmd，然后回车，打开cmd窗口

输入node -v显示node.js的版本，说明已经安装成功
输入npm -v显示npm版本，说明自带的npm已经安装成功（npm的作用就是对Node.js依赖的包进行管理，也可以理解为用来安装/卸载Node.js需要装的东西）

#### 环境配置

说明：这里的环境配置主要配置的是npm安装的全局模块所在的路径，以及缓存cache的路径，之所以要配置，是因为以后在执行类似：npm install express [-g] （后面的可选参数-g，g代表global全局安装的意思）的安装语句时，会将安装的模块安装到【C:\Users\用户名\AppData\Roaming\npm】路径中，占C盘空间。
例如：我希望将全模块所在路径和缓存路径放在我node.js安装的文件夹中，则在我安装的文件夹【D:\Develop\nodejs】下创建两个文件夹【node_global】及【node_cache】。

创建完两个空文件夹之后，打开cmd命令窗口，输入

```
npm config set prefix "D:\program\node\node_global"
npm config set cache "D:\program\node\node_cache"
```

接下来设置环境变量，关闭cmd窗口，“我的电脑”-右键-“属性”-“高级系统设置”-“高级”-“环境变量”

进入环境变量对话框，在【系统变量】下新建【NODE_PATH】，输入【D:\program\node\node_global\node_modules\】，点击【用户变量】下的“编辑”，将npm结尾的那个修改为【D:\program\node\node_global\】，点击确定。

#### 测试

配置完后，安装个module测试下，我们就安装最常用的vue，打开cmd窗口，
输入如下命令进行模块的全局安装：

```
npm install -g vue     # -g是全局安装的意思
```

遇到code EPERM npm ERR!这个错误，删除npmrc文件之后再次安装即可。文件在C:\Users\\\{账户\\}\下的.npmrc文件

code EPERM npm ERR! syscall mkdir npm ERR!或者以管理员身份运行cmd，再执行命令即可



### 安装淘宝镜像

```
npm install -g cnpm -registry=https://registry.npm.taobao.org
```

查看cnpm是否真安装成功

```
cnpm -v
```

出现cnpm 是不是内部或者外部命令，不要着急  配置电脑path变量

#### 配置电脑变量

电脑设置上搜索“高级系统设置”，点击“高级”-“环境变量”-系统环境变量Path中新增

```
D:\program\node\node_global
```

#### npm 不能安装cnpm的解决方法，  或者不能连外网安装依赖出现的错误

原因是资源的问题，电脑里没有配置淘宝镜像，需要配置淘宝镜像，配置方法

```
npm config set registry https://registry.npm.taobao.org
```

配置完成后检验是否成功

```
npm config get registry
```

配置成功有淘宝镜像网显示

重新安装项目依赖

#### cnpm : 无法加载文件

C:\Users\admin\AppData\Roaming\npm\cnpm.ps1，因为在此系统上禁止运行脚本。

有关详细信息，请参阅 https:/go.microsoft.com/fwlink/?LinkID=135170 中的 about_Execution_Policies。

解决方式：

1、在系统中搜索框 输入 Windos [PowerShell](https://so.csdn.net/so/search?q=PowerShell&spm=1001.2101.3001.7020)

2、点击“管理员身份运行”

3、输入“ set-ExecutionPolicy RemoteSigned”回车

4、根据提示，输入A，回车

5、再次回到cnpm -v执行成功。



### NPM重新安装

Step1：找到C盘，admin用户下AppData下的Roaming目录（可能是你自己的用户名，比如我的就是C:\Users\152022\Roaming）

Step2：删除上述目录中的npm和npm-cache文件夹

Step3：重新去node官网下载最新的安装包，[以往的版本](https://nodejs.org/zh-cn/download/releases/)，然后重新安装即可

最后确认一下是否安装成功，打开命令行，输入npm -v查看是否能正确显示出版本号

 

### 使用NPM有哪些好处？

通过NPM，你可以安装和管理项目的依赖，并且能够指明依赖项的具体版本号。

对于Node应用开发而言，你可以通过`package.json`文件来管理项目信息，配置脚本，以及指明依赖的具体版本



### AMD CMD规范的区别

　　CommonJS和AMD都是JavaScript模块化规范

　　CMD依赖就近，而AMD依赖前置

　　CMD是延迟执行的，而AMD是提前执行的

　　AMD的API默认是一个当多个用，CMD的API严格区分，推崇职责单一

 

### CommonJS中require/exports和ES6中import/export区别

　　CommonJS模块的重要特性是加载时执行，及脚本代码在require的时候，就会全部执行。一旦出现某个模块被“循环加载”就只输出已经执行的部分，还没有执行的部分是不输出的

　　ES6模块是动态引用，如果使用import从一个模块加载变量，那些变量不会缓存，而是成为一个指向被加载模块的引用,impor/export最终都是编译为require/exports来执行的



### 如何判断当前脚本运行在浏览器还是node环境中

　　通过判断 Global 对象是否为 window ，如果不为window ，当前脚本没有运行在浏览器中

 

### 几种常见模块化规范的简介

　　 CommonJS规范主要用于服务端编程，加载模块是同步的，这并不适合在浏览器环境，因为同步意味着阻塞加载，浏览器资源是异步加载的

　　AMD规范在浏览器环境中异步加载模块，而且可以并行加载多个模块。不过，AMD规范开发成本高，代码的阅读和书写比较困难

　　CMD规范与AMD规范很相似，都用于浏览器编程，依赖就近，延迟执行，可以很容易在Node.js中运行（依赖SPM 打包，模块的加载逻辑偏重）

　　ES6 在语言标准的层面上，实现了模块功能，而且实现得相当简单，完全可以取代 CommonJS 和 AMD 规范，成为浏览器和服务器通用的模块解决方案

 

### app.use和app.get区别

　　app.use(path,callback)中的callback既可以是router(路由)对象又可以是函数

　　app.get(path,callback)中的callback只能是函数

 

### node怎么跟MongoDB建立连接

　　1）引入mongoose

　　2）使用mongoose.connect()方法连接到MongoDB数据库

　　3）监听连接是否成功

　　4）然后通过node，书写接口，对数据库进行增删改查

 

### node 和 前端项目怎么解决跨域的

通过在node服务器端设置

```
        //解决跨域问题
        app.use(async(ctx, next) => \\{
            
            //指定服务器端允许进行跨域资源访问的来源域。可以用通配符*表示允许任何域的JavaScript访问资源，但是在响应一个携带身份信息(Credential)的HTTP请求时，必需指定具体的域，不能用通配符
            ctx.set("Access-Control-Allow-Origin", "*");

            //可选。它的值是一个布尔值，表示是否允许客户端跨域请求时携带身份信息(Cookie或者HTTP认证信息)。默认情况下，Cookie不包括在CORS请求之中。当设置成允许请求携带cookie时，需要保证"Access-Control-Allow-Origin"是服务器有的域名，而不能是"*";如果没有设置这个值，浏览器会忽略此次响应。
            ctx.set("Access-Control-Allow-Credentials", true);
            
            //指定服务器允许进行跨域资源访问的请求方法列表，一般用在响应预检请求上
            ctx.set("Access-Control-Allow-Methods", "OPTIONS, GET, PUT, POST, DELETE");
            
            //必需。指定服务器允许进行跨域资源访问的请求头列表，一般用在响应预检请求上
            ctx.set("Access-Control-Allow-Headers", "x-requested-with, accept, origin, content-type");
            // ctx.set("X-Powered-By", ' 3.2.1');
            
            //告诉客户端返回数据的MIME的类型，这只是一个标识信息,并不是真正的数据文件的一部分
            ctx.set("Content-Type", "application/json;charset=utf-8");
            
            //如果不设置mode，直接设置content-type为application/json，则fetch会默认这是跨域模式（mode:'cors'），在跨域POST之前，客户端会先发一条OPTIONS请求来”探探路”，如果服务器允许，再继续POST数据。对于这种OPTIONS请求，需要在服务器配置允许接受OPTIONS请求，这样写就是直接允许了所有的OPTIONS请求，也可以按照需求来判断OPTIONS请求中更详细的信息
            if (ctx.request.method == "OPTIONS") \\{
                ctx.response.status = 200
            \\}
            await next();
        \\});
```



### 什么是 error-first callback ？

答案：error-first callback 用来传递错误和数据。第一个参数永远是一个错误对象（error-object），回调函数必须检查它。余下的参数用不过来传递数据。

解析：

```js
fs.readFile(filePath, function(err, data) \\{
  if (err) \\{
    //处理出现错误的情况
  \\}
  //处理数据
\\});
```

考察面试者对于 Node 异步操作基本知识的见解



### Node 程序如何监听 80 端口？

答案：脑筋急转弯！你不应该直接使用 Node 监听 80 端口（在\*nix 系统中），这样做需要 root 权限，对于运行程序来说这不是一个好主意。

不过，你可以使 Node 监听 1024 以上的端口，然后在 Node 前面部署 nginx 反向代理。

解析：[参考](https://blog.csdn.net/newborn2012/article/details/23860687)



### 使用什么工具检查代码风格？

答案：

- JSLint by Douglas Crockford
- JSHint
- ESLint
- JSCS
  开发团队项目时，强制指定代码风格和使用静态分析，捕捉常见的错误，这些工具都非常有用。



### 操作错误和程序错误的区别是什么？

答案：操作错误不是 bug，是系统的问题，例如超时或者硬件故障。
另一方面，程序错误（programmer errors）是实际的错误。



### 为什么 npmshrinkwarp 非常有用？

答案：这个命令在部署 Node.js 应用时是非常有用的——它可以保证所部属的版本就是依赖的版本。

解析：[参考](http://www.tuicool.com/articles/EBVNV37)



### 什么是 stub？说出它的用途？举个使用场景？

stub是用于模拟一个组件行为或模块的函数或程序。

Stubs 提供已知的答案来调用函数，另外你还可以断言哪个 stubs 被调用

在测试用例中，简单的说，你可以用stub去模拟一个方法，从而避免调用真实的方法，使用stub你还可以返回虚构的结果。你可以配合断言使用stub。

举个例子，在一个读取文件的场景中，当你不想读取一个真正的文件时：

```
var fs = require('fs');
var readFileStub = sinon.stub(fs, 'readFile', function (path, cb) \\{
	return cb(null, 'filecontent'); 
\\});
expect(readFileStub).to.be.called;
readFileStub.restore(); 
```

在单元测试中：Stub是完全模拟一个外部依赖，而Mock常用来判断测试通过还是失败



### 什么是测试金字塔？在做 HTTP API 的时候要怎么实现？

答案：测试金字塔意思是在写测试时应该编写的底层但愿测试要多于高级的端到端测试。
对于 HTTP APIs，应该归结为：

- 对你的模型多很多单元测试
- 在你的模型与其他交互时更少的集成测试
- 更少的验收测试，在 HTTP 端



### 你最喜欢的 HTTP 框架，并说明原因？

答案：LiteHttp 好多的优点
单线程 灵活的架构 轻量级 多文件上传 自动重定向 禁用一种或多种网络

解析：[参考](http://blog.csdn.net/kymjs/article/details/45716797)



### 需求：实现一个页面操作不会整页刷新的网站，并且能在浏览器前进、后退时正确响应。给出你的技术实现方案？

答案：至少给出自己的思路（url-hash,可以使用已有的一些框架 history.js 等）



### 为什么用Nodejs,它有哪些缺点？

- 事件驱动，通过闭包很容易实现客户端的生命活期。
- 不用担心多线程，锁，并行计算的问题
- V8引擎速度非常快
- 对于游戏来说，写一遍游戏逻辑代码，前端后端通用

当然Nodejs也有一些缺点：

- nodejs更新很快，可能会出现版本兼容
- nodejs还不算成熟，还没有大制作
- nodejs不像其他的服务器，对于不同的链接，不支持进程和线程操作



### 什么是错误优先的回调函数？

错误优先(Error-first)的回调函数（Error-First Callback）用于同时返回错误和数据。第一个参数返回错误，并且验证它是否出错；其他参数返回数据。

```
  fs.readFile(filePath, function(err, data)
  \\{
      if (err)
      \\{
          // 处理错误
          return console.log(err);
      \\}
      console.log(data);
  \\});
```



### 如何避免回调地狱？

以下方式避免回调地狱

- 模块化：将回调函数转换为独立的函数
- 使用流程控制库，例如[aync]
- 使用Promise
- 使用aync/await



### 什么是Promise?

Promise可以帮助我们更好地处理异步操作。下面的实例中，100ms后会打印result字符串。catch用于错误处理。多个Promise可以链接起来。

```
  new Promise((resolve, reject) =>
      \\{
          setTimeout(() =>
          \\{
              resolve('result');
          \\}, 100)
      \\})
      .then(console.log)
      .catch(console.error);
```



### 用什么工具保证一致的代码风格？为什么要这样？

- 团队协作时，保证一致的代码风格是非常重要的，这样团队成员才可以更快地修改代码，而不需要每次去适应新的风格。这些工具可以帮助我们：
- [ESLint] (http://eslint.org/)
- [Standard] (https://standardjs.com/)
- JSLint
- JSHint
- ESLint
- JSCS推荐



### 什么是stub？举例说明

stub用于模块的行为。测试时，stub可以为函数调用返回模拟的结果。比如说，我们写文件时，实际上并不需要真正去写。

```
      var fs = require('fs');
      var writeFileStub = sinon.stub(fs, 'writeFile', function(path, data, cb)
      \\{
          return cb(null);
      \\});
      expect(writeFileStub).to.be.called;
      writeFileStub.restore();
```



### 什么是测试金字塔？举例说明

测试金字塔反应了需要写的单元测试，集成测试以及端到端测试的比例：
![img](https://img-blog.csdnimg.cn/img_convert/d8e54e6efab0aaee7cfa04b9d01fc1c0.png)

- 测试HTTP接口时应该是这样的：
- 很多单元测试，分别测试各个模块(依赖需要stub)
- 较少的集成测试，测试各个模块之间的交互(依赖不能stub)
- 少量端到端测试，去调用真正地接口(依赖不能stub)



### 如何用Node监听80端口

- 这题有陷阱！在类Unix系统中你不应该去监听80端口，因为这需要超级用户权限。因此不推荐让你的应用直接监听这个端口。
- 目前，如果你一定要让你的应用80端口的话，你可以有通过在Node应用的前方再添加一层反向代理（例如nginx）来实现，如下图。否则，建议你直接监听大于1024的端口
  ![img](https://img-blog.csdnimg.cn/img_convert/f8268836da6ec8cca9519798f76c899d.png)
- 方向代理指的是以代理服务器来接收Internet上的连接请求，然后将请求转发给内部网络上的服务器， 并且将服务器返回的结果发送给客户端。



### NodeJS 的工作原理

答案：事件循环



### 什么是事件循环（event loop）？

答案：至少从开发者的角度来看，Node.js 是单线程运行的。底层使用 libuv 使用多线程。
每一个 I/O 操作都需要一个回调，一旦操作完成会被事件循环执行

解析：[参考](http://blog.csdn.net/yanghua_kobe/article/details/12145537)



### 什么是事件循环

Node采用的是单线程的处理机制(所有的I/O请求都采用非阻塞的工作方式)，至少从Node.js开发者的角度是这样的。而在底层，Node.js借助libuv来作为抽象封装层，从而屏蔽不同操作系统的差异，Node可以借助livuv来实现线程。下图表示Node和libuv的关系
![img](https://img-blog.csdnimg.cn/img_convert/e0887371264c92388e3bdadf42970cde.png)

Libuv库负责Node API的执行。它将不同的任务分配给不同的线程，形成一个事件循环，以异步的方式将任务的执行结果返回给V8引擎。可以简单用下面这张图来表示
![img](https://img-blog.csdnimg.cn/img_convert/f7b0149e185dbecabd4490f3f4293a30.png)

每一个I/O都需要一个回调函数————一旦执行完便堆到事件循环上用于执行



### 运算错误与程序员错误的区别

运算错误并不是bug，这是和系统相关的问题，例如请求超时或者硬件故障。而程序员错误就是所谓的bug



### 1、Node模块机制

#### 1.1 请介绍一下node里的模块是什么

Node中，每个文件模块都是一个对象，它的定义如下：

```
function Module(id, parent) \\{
 this.id = id;
 this.exports = \\{\\};
 this.parent = parent;
 this.filename = null;
 this.loaded = false;
 this.children = [];
\\}
 
module.exports = Module;
 
var module = new Module(filename, parent);
```

所有的模块都是 Module 的实例。可以看到，当前模块（module.js）也是 Module 的一个实例。



#### 1.2 请介绍一下require的模块加载机制

这道题基本上就可以了解到面试者对Node模块机制的了解程度基本上面试提到

1、先计算模块路径

2、如果模块在缓存里面，取出缓存

3、加载模块

4、的输出模块的exports属性即可

```
// require 其实内部调用 Module._load 方法
Module._load = function(request, parent, isMain) \\{
 // 计算绝对路径
 var filename = Module._resolveFilename(request, parent);
 
 // 第一步：如果有缓存，取出缓存
 var cachedModule = Module._cache[filename];
 if (cachedModule) \\{
 return cachedModule.exports;
 
 // 第二步：是否为内置模块
 if (NativeModule.exists(filename)) \\{
 return NativeModule.require(filename);
 \\}
  
 /********************************这里注意了**************************/
 // 第三步：生成模块实例，存入缓存
 // 这里的Module就是我们上面的1.1定义的Module
 var module = new Module(filename, parent);
 Module._cache[filename] = module;
 
 /********************************这里注意了**************************/
 // 第四步：加载模块
 // 下面的module.load实际上是Module原型上有一个方法叫Module.prototype.load
 try \\{
 module.load(filename);
 hadException = false;
 \\} finally \\{
 if (hadException) \\{
  delete Module._cache[filename];
 \\}
 \\}
 
 // 第五步：输出模块的exports属性
 return module.exports;
\\};
```

接着上一题继续发问



#### 1.3 加载模块时，为什么每个模块都有__dirname,__filename属性呢，new Module的时候我们看到1.1部分没有这两个属性的，那么这两个属性是从哪里来的

```
// 上面(1.2部分)的第四步module.load(filename)
// 这一步，module模块相当于被包装了，包装形式如下
// 加载js模块，相当于下面的代码（加载node模块和json模块逻辑不一样）
(function (exports, require, module, __filename, __dirname) \\{
 // 模块源码
 // 假如模块代码如下
 var math = require('math');
 exports.area = function(radius)\\{
  return Math.PI * radius * radius
 \\}
\\});
```

也就是说，每个module里面都会传入__filename, __dirname参数，这两个参数并不是module本身就有的，是外界传入的



#### 1.4 我们知道node导出模块有两种方式，一种是exports.xxx=xxx和Module.exports=\\{\\}有什么区别吗

- exports其实就是module.exports
- 其实1.3问题的代码已经说明问题了，接着我引用廖雪峰大神的讲解，希望能讲的更清楚

```
module.exports vs exports
很多时候，你会看到，在Node环境中，有两种方法可以在一个模块中输出变量：

方法一：对module.exports赋值：

// hello.js

function hello() \\{
 console.log('Hello, world!');
\\}

function greet(name) \\{
 console.log('Hello, ' + name + '!');
\\}

module.exports = \\{
 hello: hello,
 greet: greet
\\};
方法二：直接使用exports：

// hello.js

function hello() \\{
 console.log('Hello, world!');
\\}

function greet(name) \\{
 console.log('Hello, ' + name + '!');
\\}

function hello() \\{
 console.log('Hello, world!');
\\}

exports.hello = hello;
exports.greet = greet;
但是你不可以直接对exports赋值：

// 代码可以执行，但是模块并没有输出任何变量:
exports = \\{
 hello: hello,
 greet: greet
\\};
如果你对上面的写法感到十分困惑，不要着急，我们来分析Node的加载机制：

首先，Node会把整个待加载的hello.js文件放入一个包装函数load中执行。在执行这个load()函数前，Node准备好了module变量：

var module = \\{
 id: 'hello',
 exports: \\{\\}
\\};
load()函数最终返回module.exports：

var load = function (exports, module) \\{
 // hello.js的文件内容
 ...
 // load函数返回:
 return module.exports;
\\};

var exported = load(module.exports, module);
也就是说，默认情况下，Node准备的exports变量和module.exports变量实际上是同一个变量，并且初始化为空对象\\{\\}，于是，我们可以写：

exports.foo = function () \\{ return 'foo'; \\};
exports.bar = function () \\{ return 'bar'; \\};
也可以写：

module.exports.foo = function () \\{ return 'foo'; \\};
module.exports.bar = function () \\{ return 'bar'; \\};
换句话说，Node默认给你准备了一个空对象\\{\\}，这样你可以直接往里面加东西。

但是，如果我们要输出的是一个函数或数组，那么，只能给module.exports赋值：

module.exports = function () \\{ return 'foo'; \\};
给exports赋值是无效的，因为赋值后，module.exports仍然是空对象\\{\\}。

结论
如果要输出一个键值对象\\{\\}，可以利用exports这个已存在的空对象\\{\\}，并继续在上面添加新的键值；

如果要输出一个函数或数组，必须直接对module.exports对象赋值。

所以我们可以得出结论：直接对module.exports赋值，可以应对任何情况：

module.exports = \\{
 foo: function () \\{ return 'foo'; \\}
\\};
或者：

module.exports = function () \\{ return 'foo'; \\};
最终，我们强烈建议使用module.exports = xxx的方式来输出模块变量，这样，你只需要记忆一种方法。
```



### 2、Node的异步I/O

本章的答题思路大多借鉴于朴灵大神的《深入浅出的NodeJS》

#### 2.1 请介绍一下Node事件循环的流程

- 在进程启动时，Node便会创建一个类似于while(true)的循环，每执行一次循环体的过程我们成为Tick。
- 每个Tick的过程就是查看是否有事件待处理。如果有就取出事件及其相关的回调函数。然后进入下一个循环，如果不再有事件处理，就退出进程。

![img](https://img.jbzj.com/file_images/article/201910/2019100915292637.png)

#### 2.2 在每个tick的过程中，如何判断是否有事件需要处理呢？

1. 每个事件循环中有一个或者多个观察者，而判断是否有事件需要处理的过程就是向这些观察者询问是否有要处理的事件。
2. 在Node中，事件主要来源于网络请求、文件的I/O等，这些事件对应的观察者有文件I/O观察者，网络I/O的观察者。
3. 事件循环是一个典型的生产者/消费者模型。异步I/O，网络请求等则是事件的生产者，源源不断为Node提供不同类型的事件，这些事件被传递到对应的观察者那里，事件循环则从观察者那里取出事件并处理。
4. 在windows下，这个循环基于IOCP创建，在*nix下则基于多线程创建



#### 2.3 请描述一下整个异步I/O的流程

![img](https://img.jbzj.com/file_images/article/201910/2019100915292638.png)



### 3、V8的垃圾回收机制

#### 3.1 如何查看V8的内存使用情况

使用process.memoryUsage(),返回如下

```
\\{
 rss: 4935680,
 heapTotal: 1826816,
 heapUsed: 650472,
 external: 49879
\\}
```

heapTotal和heapUsed代表V8的内存使用情况。external代表V8管理的，绑定到Javascript的C++对象的内存使用情况。rss, 驻留集大小, 是给这个进程分配了多少物理内存(占总分配内存的一部分) 这些物理内存中包含堆，栈，和代码段。



#### 3.2 V8的内存限制是多少，为什么V8这样设计

64位系统下是1.4GB， 32位系统下是0.7GB。因为1.5GB的垃圾回收堆内存，V8需要花费50毫秒以上，做一次非增量式的垃圾回收甚至要1秒以上。这是垃圾回收中引起Javascript线程暂停执行的事件，在这样的花销下，应用的性能和影响力都会直线下降。



#### 3.3 V8的内存分代和回收算法请简单讲一讲

在V8中，主要将内存分为新生代和老生代两代。新生代中的对象存活时间较短的对象，老生代中的对象存活时间较长，或常驻内存的对象。

![img](https://img.jbzj.com/file_images/article/201910/2019100915292739.png)

3.3.1 新生代

新生代中的对象主要通过Scavenge算法进行垃圾回收。这是一种采用复制的方式实现的垃圾回收算法。它将堆内存一份为二，每一部分空间成为semispace。在这两个semispace空间中，只有一个处于使用中，另一个处于闲置状态。处于使用状态的semispace空间称为From空间，处于闲置状态的空间称为To空间。

![img](https://img.jbzj.com/file_images/article/201910/2019100915292740.png)

- 当开始垃圾回收的时候，会检查From空间中的存活对象，这些存活对象将被复制到To空间中，而非存活对象占用的空间将会被释放。完成复制后，From空间和To空间发生角色对换。
- 应为新生代中对象的生命周期比较短，就比较适合这个算法。
- 当一个对象经过多次复制依然存活，它将会被认为是生命周期较长的对象。这种新生代中生命周期较长的对象随后会被移到老生代中。

3.3.2 老生代

老生代主要采取的是标记清除的垃圾回收算法。与Scavenge复制活着的对象不同，标记清除算法在标记阶段遍历堆中的所有对象，并标记活着的对象，只清理死亡对象。活对象在新生代中只占叫小部分，死对象在老生代中只占较小部分，这是为什么采用标记清除算法的原因。

3.3.3 标记清楚算法的问题

主要问题是每一次进行标记清除回收后，内存空间会出现不连续的状态

![img](https://img.jbzj.com/file_images/article/201910/2019100915292741.png)

- 这种内存碎片会对后续内存分配造成问题，很可能出现需要分配一个大对象的情况，这时所有的碎片空间都无法完成此次分配，就会提前触发垃圾回收，而这次回收是不必要的。
- 为了解决碎片问题，标记整理被提出来。就是在对象被标记死亡后，在整理的过程中，将活着的对象往一端移动，移动完成后，直接清理掉边界外的内存。

3.3.4 哪些情况会造成V8无法立即回收内存

闭包和全局变量

3.3.5 请谈一下内存泄漏是什么，以及常见内存泄漏的原因，和排查的方法

什么是内存泄漏

- 内存泄漏(Memory Leak)指由于疏忽或错误造成程序未能释放已经不再使用的内存的情况。
- 如果内存泄漏的位置比较关键，那么随着处理的进行可能持有越来越多的无用内存，这些无用的内存变多会引起服务器响应速度变慢。
- 严重的情况下导致内存达到某个极限(可能是进程的上限，如 v8 的上限;也可能是系统可提供的内存上限)会使得应用程序崩溃。常见内存泄漏的原因内存泄漏的几种情况:



### 一、全局变量

```
a = 10; 
//未声明对象。 
global.b = 11; 
//全局变量引用 
这种比较简单的原因，全局变量直接挂在 root 对象上，不会被清除掉。
```



### 二、闭包

```
function out() \\{ 
 const bigData = new Buffer(100); 
 inner = function () \\{ 
  
 \\} 
\\} 
```

闭包会引用到父级函数中的变量，如果闭包未释放，就会导致内存泄漏。上面例子是 inner 直接挂在了 root 上，那么每次执行 out 函数所产生的 bigData 都不会释放，从而导致内存泄漏。

需要注意的是，这里举得例子只是简单的将引用挂在全局对象上，实际的业务情况可能是挂在某个可以从 root 追溯到的对象上导致的。



### 三、事件监听

Node.js 的事件监听也可能出现的内存泄漏。例如对同一个事件重复监听，忘记移除(removeListener)，将造成内存泄漏。这种情况很容易在复用对象上添加事件时出现，所以事件重复监听可能收到如下警告：

```
emitter.setMaxListeners() to increase limit
```

例如，Node.js 中 Agent 的 keepAlive 为 true 时，可能造成的内存泄漏。当 Agent keepAlive 为 true 的时候，将会复用之前使用过的 socket，如果在 socket 上添加事件监听，忘记清除的话，因为 socket 的复用，将导致事件重复监听从而产生内存泄漏。

原理上与前一个添加事件监听的时候忘了清除是一样的。在使用 Node.js 的 http 模块时，不通过 keepAlive 复用是没有问题的，复用了以后就会可能产生内存泄漏。所以，你需要了解添加事件监听的对象的生命周期，并注意自行移除。

**排查方法**

- 想要定位内存泄漏，通常会有两种情况：
- 对于只要正常使用就可以重现的内存泄漏，这是很简单的情况只要在测试环境模拟就可以排查了。
- 对于偶然的内存泄漏，一般会与特殊的输入有关系。想稳定重现这种输入是很耗时的过程。如果不能通过代码的日志定位到这个特殊的输入，那么推荐去生产环境打印内存快照了。
- 需要注意的是，打印内存快照是很耗 CPU 的操作，可能会对线上业务造成影响。快照工具推荐使用 heapdump 用来保存内存快照，使用 devtool 来查看内存快照。
- 使用 heapdump 保存内存快照时，只会有 Node.js 环境中的对象，不会受到干扰(如果使用 node-inspector 的话，快照中会有前端的变量干扰)。
- PS：安装 heapdump 在某些 Node.js 版本上可能出错，建议使用 npm install heapdump -target=Node.js 版本来安装。



### 4、Buffer模块

#### 4.1 新建Buffer会占用V8分配的内存吗

不会，Buffer属于堆外内存，不是V8分配的。



#### 4.2 Buffer.alloc和Buffer.allocUnsafe的区别

Buffer.allocUnsafe创建的 Buffer 实例的底层内存是未初始化的。 新创建的 Buffer 的内容是未知的，可能包含敏感数据。 使用 Buffer.alloc() 可以创建以零初始化的 Buffer 实例。



#### 4.3 Buffer的内存分配机制

为了高效的使用申请来的内存，Node采用了slab分配机制。slab是一种动态的内存管理机制。Node以8kb为界限来来区分Buffer为大对象还是小对象，如果是小于8kb就是小Buffer，大于8kb就是大Buffer。

例如第一次分配一个1024字节的Buffer，Buffer.alloc(1024),那么这次分配就会用到一个slab，接着如果继续Buffer.alloc(1024),那么上一次用的slab的空间还没有用完，因为总共是8kb，1024+1024 = 2048个字节，没有8kb，所以就继续用这个slab给Buffer分配空间。

如果超过8bk，那么直接用C++底层地宫的SlowBuffer来给Buffer对象提供空间。



#### 4.4 Buffer乱码问题

例如一个份文件test.md里的内容如下：

```
床前明月光，疑是地上霜，举头望明月，低头思故乡
```

我们这样读取就会出现乱码：

```
var rs = require('fs').createReadStream('test.md', \\{highWaterMark: 11\\});
// 床前明???光，疑???地上霜，举头???明月，???头思故乡
```

一般情况下，只需要设置rs.setEncoding('utf8')即可解决乱码问题



### 5、webSocket

#### 5.1 webSocket与传统的http有什么优势

- 客户端与服务器只需要一个TCP连接，比http长轮询使用更少的连接
- webSocket服务端可以推送数据到客户端
- 更轻量的协议头，减少数据传输量



#### 5.2 webSocket协议升级时什么，能简述一下吗？

首先，WebSocket连接必须由浏览器发起，因为请求协议是一个标准的HTTP请求，格式如下：

```
GET ws://localhost:3000/ws/chat HTTP/1.1
Host: localhost
Upgrade: websocket
Connection: Upgrade
Origin: http://localhost:3000
Sec-WebSocket-Key: client-random-string
Sec-WebSocket-Version: 13
```

该请求和普通的HTTP请求有几点不同：

- GET请求的地址不是类似/path/，而是以ws://开头的地址；
- 请求头Upgrade: websocket和Connection: Upgrade表示这个连接将要被转换为WebSocket连接；
- Sec-WebSocket-Key是用于标识这个连接，并非用于加密数据；
- Sec-WebSocket-Version指定了WebSocket的协议版本。

随后，服务器如果接受该请求，就会返回如下响应：

```
HTTP/1.1 101 Switching Protocols
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Accept: server-random-string
```

该响应代码101表示本次连接的HTTP协议即将被更改，更改后的协议就是Upgrade: websocket指定的WebSocket协议。



### 6、https

#### 6.1 https用哪些端口进行通信，这些端口分别有什么用

- 443端口用来验证服务器端和客户端的身份，比如验证证书的合法性
- 80端口用来传输数据（在验证身份合法的情况下，用来数据传输）



#### 6.2 身份验证过程中会涉及到密钥， 对称加密，非对称加密，摘要的概念，请解释一下

- 密钥：密钥是一种参数，它是在明文转换为密文或将密文转换为明文的算法中输入的参数。密钥分为对称密钥与非对称密钥，分别应用在对称加密和非对称加密上。
- 对称加密：对称加密又叫做私钥加密，即信息的发送方和接收方使用同一个密钥去加密和解密数据。对称加密的特点是算法公开、加密和解密速度快，适合于对大数据量进行加密，常见的对称加密算法有DES、3DES、TDEA、Blowfish、RC5和IDEA。
- 非对称加密：非对称加密也叫做公钥加密。非对称加密与对称加密相比，其安全性更好。对称加密的通信双方使用相同的密钥，如果一方的密钥遭泄露，那么整个通信就会被破解。而非对称加密使用一对密钥，即公钥和私钥，且二者成对出现。私钥被自己保存，不能对外泄露。公钥指的是公共的密钥，任何人都可以获得该密钥。用公钥或私钥中的任何一个进行加密，用另一个进行解密。
- 摘要： 摘要算法又称哈希/散列算法。它通过一个函数，把任意长度的数据转换为一个长度固定的数据串（通常用16进制的字符串表示）。算法不可逆。



#### 6.3 为什么需要CA机构对证书签名

如果不签名会存在中间人攻击的风险，签名之后保证了证书里的信息，比如公钥、服务器信息、企业信息等不被篡改，能够验证客户端和服务器端的“合法性”。



#### 6.4 https验证身份也就是TSL/SSL身份验证的过程

简要图解如下

**![img](https://img.jbzj.com/file_images/article/201910/2019100915292742.jpg)**



### 7、进程通信

#### 7.1 请简述一下node的多进程架构

面对node单线程对多核CPU使用不足的情况，Node提供了child_process模块，来实现进程的复制，node的多进程架构是主从模式，如下所示：

![img](https://img.jbzj.com/file_images/article/201910/2019100915292743.png)

```
var fork = require('child_process').fork;
var cpus = require('os').cpus();
for(var i = 0; i < cpus.length; i++)\\{
 fork('./worker.js');
\\}
```

在linux中，我们通过ps aux | grep worker.js查看进程

![img](https://img.jbzj.com/file_images/article/201910/2019100915292844.png)

这就是著名的主从模式，Master-Worker



#### 7.2 请问创建子进程的方法有哪些，简单说一下它们的区别

创建子进程的方法大致有：

- spawn()： 启动一个子进程来执行命令
- exec(): 启动一个子进程来执行命令，与spawn()不同的是其接口不同，它有一个回调函数获知子进程的状况
- execFlie(): 启动一个子进程来执行可执行文件
- fork(): 与spawn()类似，不同电在于它创建Node子进程需要执行js文件
- spawn()与exec()、execFile()不同的是，后两者创建时可以指定timeout属性设置超时时间，一旦创建的进程超过设定的时间就会被杀死
- exec()与execFile()不同的是，exec()适合执行已有命令，execFile()适合执行文件。



#### 7.3 请问你知道spawn在创建子进程的时候，第三个参数有一个stdio选项吗，这个选项的作用是什么，默认的值是什么。

- 选项用于配置在父进程和子进程之间建立的管道。
- 默认情况下，子进程的 stdin、 stdout 和 stderr 会被重定向到 ChildProcess 对象上相应的 subprocess.stdin、subprocess.stdout 和 subprocess.stderr 流。
- 这相当于将 options.stdio 设置为 ['pipe', 'pipe', 'pipe']。



#### 7.4 请问实现一个node子进程被杀死，然后自动重启代码的思路

在创建子进程的时候就让子进程监听exit事件，如果被杀死就重新fork一下

```
var createWorker = function()\\{
 var worker = fork(__dirname + 'worker.js')
 worker.on('exit', function()\\{
  console.log('Worker' + worker.pid + 'exited');
  // 如果退出就创建新的worker
  createWorker()
 \\})
\\}
```



#### 7.5 在7.4的基础上，实现限量重启，比如我最多让其在1分钟内重启5次，超过了就报警给运维

- 思路大概是在创建worker的时候，就判断创建的这个worker是否在1分钟内重启次数超过5次
- 所以每一次创建worker的时候都要记录这个worker 创建时间，放入一个数组队列里面，每次创建worker都去取队列里前5条记录
- 如果这5条记录的时间间隔小于1分钟，就说明到了报警的时候了



#### 7.6 如何实现进程间的状态共享，或者数据共享

我自己没用过Kafka这类消息队列工具，问了java,可以用类似工具来实现进程间通信，更好的方法欢迎留言



### 8、中间件

#### 8.1 如果使用过koa、egg这两个Node框架，请简述其中的中间件原理，最好用代码表示一下

![img](https://img.jbzj.com/file_images/article/201910/2019100915292845.png)

上面是在网上找的一个示意图，就是说中间件执行就像洋葱一样，最早use的中间件，就放在最外层。处理顺序从左到右，左边接收一个request，右边输出返回response

一般的中间件都会执行两次，调用next之前为第一次，调用next时把控制传递给下游的下一个中间件。当下游不再有中间件或者没有执行next函数时，就将依次恢复上游中间件的行为，让上游中间件执行next之后的代码

例如下面这段代码

```
const Koa = require('koa')
const app = new Koa()
app.use((ctx, next) => \\{
 console.log(1)
 next()
 console.log(3)
\\})
app.use((ctx) => \\{
 console.log(2)
\\})
app.listen(3001)
执行结果是1=>2=>3
```

koa中间件实现源码大致思路如下：

```
// 注意其中的compose函数，这个函数是实现中间件洋葱模型的关键
// 场景模拟
// 异步 promise 模拟
const delay = async () => \\{
 return new Promise((resolve, reject) => \\{
 setTimeout(() => \\{
  resolve();
 \\}, 2000);
 \\});
\\}
// 中间间模拟
const fn1 = async (ctx, next) => \\{
 console.log(1);
 await next();
 console.log(2);
\\}
const fn2 = async (ctx, next) => \\{
 console.log(3);
 await delay();
 await next();
 console.log(4);
\\}
const fn3 = async (ctx, next) => \\{
 console.log(5);
\\}

const middlewares = [fn1, fn2, fn3];

// compose 实现洋葱模型
const compose = (middlewares, ctx) => \\{
 const dispatch = (i) => \\{
 let fn = middlewares[i];
 if(!fn)\\{ return Promise.resolve() \\}
 return Promise.resolve(fn(ctx, () => \\{
  return dispatch(i+1);
 \\}));
 \\}
 return dispatch(0);
\\}

compose(middlewares, 1);
```



### 9、其它

现在在重新过一遍node 12版本的主要API，有很多新发现，比如说

- fs.watch这个模块，事件的回调函数有一个参数是触发的事件名称，但是呢，无论我增删改，都是触发rename事件（如果更改是update事件，删除delete事件，重命名是rename事件，这样语义明晰该多好）。后来网上找到一个node-watch模块，此模块增删改都有对应的事件， 并且还高效的支持递归watch 文件。
- util模块有个promisify方法，可以让一个遵循异常优先的回调风格的函数，即 (err, value) => ... 回调函数是最后一个参数，返回一个返回值是一个 promise 版本的函数。

```
const util = require('util');
const fs = require('fs');

const stat = util.promisify(fs.stat);
stat('.').then((stats) => \\{
 // 处理 `stats`。
\\}).catch((error) => \\{
 // 处理错误。
\\});
```



#### 10、杂想

- crypto模块，可以考察基础的加密学知识，比如摘要算法有哪些（md5, sha1, sha256，加盐的md5,sha256等等）,接着可以问如何用md5自己模拟一个加盐的md5算法， 接着可以问加密算法（crypto.createCiphe）中的aes,eds算法的区别，分组加密模式有哪些（比如ECB,CBC,为什么ECB不推荐），node里的分组加密模式是哪种（CMM），这些加密算法里的填充和向量是什么意思，接着可以问数字签名和https的流程（为什么需要CA，为什么要对称加密来加密公钥等等）
- tcp/ip，可以问很多基础问题，比如链路层通过什么协议根据IP地址获取物理地址（arp），网关是什么，ip里的ICMP协议有什么用，tcp的三次握手，四次分手的过程是什么，tcp如何控制重发，网络堵塞TCP会怎么办等等，udp和tcp的区别，udp里的广播和组播是什么，组播在node里通过什么模块实现。
- os，操作系统相关基础，io的流程是什么（从硬盘里读取数据到内核的内存中，然后内核的内存将数据传入到调用io的应用程序的进程内存中），冯诺依曼体系是什么，进程和线程的区别等等（我最近在看马哥linux教程，因为自己不是科班出身，听了很多基础的计算机知识，受益匪浅，建议去bilibili看）
- linux相关操作知识（node涉及到后台，虽然是做中台，不涉及数据库，但是基本的linux操作还是要会的）
- node性能监控（自己也正在学习中）
- 测试，因为用的egg框架，有很完善的学习单元测试的文档，省略这部分
- 数据库可以问一些比如事务的等级有哪些，mysql默认的事务等级是什么，会产生什么问题，然后考一些mysql查询的笔试题。。。和常用优化技巧，node的mysql的orm工具使用过没有。。。（比如我自己是看的尚硅谷mysql初级+高级视频，书是看的mysql必知必会，我自己出于爱好学习一下。。。没有实战过）



### 第1题, 什么是nodejs？我们在哪里使用它？

Nodejs是服务器端的一门技术。它是基于Google V8 JavaScript引擎而开发的。用来开发可扩展的服务端程序。



### 第2题，为什么要使用node js？

nodejs会让我们的编程工作变得简单，它主要包含如下几点几个好处:

执行快速。

永远不会阻滞。

JavaScript是通用的编程语言。

异步处理机制。

避免并行所带来的问题。



### 第3题，nodejs有哪些特点？

是单线程的，但是有很高的可扩展性，使用JavaScript作为主流编程语言。使用的是异步处理机制和事件驱动。处理高效。



### 第4题， Set immediate和set time out 区别在哪里?

Set immediate就是马上执行的意思。Set time out, 时间参数传为0，也想获得同样的功能。只不过前者要快一些。



### 第5题，如何更新nodejs的版本?

npm install npm -g



### 第6题，为什么nodejs是单线程的？

Nodejs使用的是单线程没错，但是通过异步处理的方式，可以处理大量的数据吞吐量，从而有更好的性能和扩可扩展性。



### 第7题，什么是回调函数？

回调函数是指用一个函数作为参数传入另一个函数，这个函数会被在某个时机调用。



### 第8题, 什么叫做回调地狱?

回调地狱是由嵌套的回调函数导致的。这样的机制会导致有些函数无法到达，并且很难维护。



### 第9题，如何阻止回调地狱?

有三种方法， 对每个错误都要处理到， 保证代码的贯通， 程序代码模块化。



### 第10题，解释一下repl的作用?

Read evaluate print loop， 用于测试，调试和实验用。



### 第11题，API函数的类型有哪些?

有两种，

一种是阻滞型函数。阻滞型函数会等待操作完成以后再进行下一步。

另外一种是非阻滞型函数。这种函数使用回调函数来处理当前函数获取的结果。



### 第12题，回调函数的第1个参数是什么?

通常是错误对象。如果这个参数为空，表示没有错误。



### 第13题，NPM的作用是什么?

Node package manager, 主要有两个功能。

它是一个网端模块的存储介质。

它的另一个作用是安装程序依赖和版本管理。



### 第14题，nodejs和ajax的区别是什么？

Nodejs和ajax也就是asynchronous JavaScript and xml，都是通过JavaScript来表现的，但是他们的目的截然不同。

Ajax是设计用来动态的更新页面的某个区域，从而不需要更新整个页面。

Nodejs是用来开发客户服务器类型应用的。



### 第15题，解释一下nodejs中chaining.

Chaining是指从一个数据流到另一个数据流的链接，从而实现多个流操作。



### 第16题，什么是streams？解释一下有哪些类型?

流的概念是不间断的，它可以不间断的从某个地方读取数据，或者向某个地方写入数据。

有4种类型的流数据。可读，可写。既可读，又可写，转化。



### 第17题，退出代码是什么？有哪些退出代码?

退出代码是指中断nodejs运行时返回的代码。

有这么几种unused, uncaught fatal exception, fatal error, non function internal exception handler, internal exception handler run time failure,internal JavaScript evaluation failure.



### 第18题, 什么是globals?

有三个global的关键字。

Global代表的是最上层的命名空间,用来管理所有其他的全局对象。

Process 是一个全局对象，可以把异步函数转化成异步回调, 它可以在任何地方被访问，它主要是用来返回系统的应用信息和环境信息.

Buffer, 是用来处理二进制数据的类.



### 第19题， Angular js和node js的区别是什么?

Angular js是网络应用开发框架，而nodejs是一个实时系统。



### 第20题, 为什么统一的风格儿非常重要，有什么工具可以保证这一点?

统一的风格可以让所有的组成员按照一种规矩来写代码。工具有Standard和eslint.



### 第21题, 用什么方法来处理没有被处理的异常?

在应用和node js之间使用domain来处理这样的异常。



### 第22题, Node js是如何支持多处理器平台的?

Cluster模块是用来支持这方面的。它可以允许多个nodejs工作进程运行在相同的端口上。



### 第23题, 如何配置开发模式和生产模式的环境?

首先有一个配置文件，然后通过环境变量参数来获取对应的配置内容。



### 第24题, nodejs中跟时间相关的函数有哪些?

Set time out, clear time out.

Set interval, clear interval.

Set immediate, clear immediate.

Process.nextTick.



### 第25题, 解释一下什么是reactor pattern。

Reactor pattern主要是非阻滞的i/o操作。提供一个回调函数来关联io操作。io请求完成以后会不会提交给demultiplexer, 这是一个通知接口用来处理并发性的非阻滞的io操作，这个功能是通过查询一个event loop来实现的.



### 第26题，lts版本是什么意思？

也就是long term support版本。至少会被支持18个月。使用的是偶数来标识。这种版本有稳定性和安全性的保证。



### 第27题，你为什么需要把express APP和server分开？

分开以后方便维护以及测试，在测试某个模块的时候，尤其是APP模块的时候，你不需要去对网络方面的连接配置做工作。



### 第28题，next tick和setImmediate的区别是什么？

Next tick会等待当前的event执行完成或者下一轮儿事件循环到达再执行。

Set immediate, 会在下一轮的事件循环中，执行回调并且返回当前的循环来做读写操作.