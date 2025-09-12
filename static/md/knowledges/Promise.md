---
title: Promise
date: 2019-12-11 19:25:55
categories: 
- 前端知识
tags:
- Promise
---

### 大白话讲解Promise（一）

去年6月份， ES2015正式发布（也就是ES6，ES6是它的乳名），其中Promise被列为正式规范。作为ES6中最重要的特性之一，我们有必要掌握并理解透彻。本文将由浅到深，讲解Promise的基本概念与使用方法。

 

### ES6 Promise 先拉出来遛遛

复杂的概念先不讲，我们先简单粗暴地把Promise用一下，有个直观感受。那么第一个问题来了，Promise是什么玩意呢？是一个类？对象？数组？函数？

别猜了，直接打印出来看看吧，console.dir(Promise)，就这么简单粗暴。

![img](https://images2015.cnblogs.com/blog/520134/201603/520134-20160311003722741-755677508.png)

这么一看就明白了，Promise是一个构造函数，自己身上有all、reject、resolve这几个眼熟的方法，原型上有then、catch等同样很眼熟的方法。这么说用Promise new出来的对象肯定就有then、catch方法喽，没错。

那就new一个玩玩吧。

```
var p = new Promise(function(resolve, reject)\\{
    //做一些异步操作
    setTimeout(function()\\{
        console.log('执行完成');
        resolve('随便什么数据');
    \\}, 2000);
\\});
```

Promise的构造函数接收一个参数，是函数，并且传入两个参数：resolve，reject，分别表示异步操作执行成功后的回调函数和异步操作执行失败后的回调函数。其实这里用“成功”和“失败”来描述并不准确，按照标准来讲，**resolve是将Promise的状态置为fullfiled，reject是将Promise的状态置为rejected。**不过在我们开始阶段可以先这么理解，后面再细究概念。

在上面的代码中，我们执行了一个异步操作，也就是setTimeout，2秒后，输出“执行完成”，并且调用resolve方法。

运行代码，会在2秒后输出“执行完成”。注意！我只是new了一个对象，并没有调用它，我们传进去的函数就已经执行了，这是需要注意的一个细节。所以我们用Promise的时候**一般是包在一个函数中，在需要的时候去运行这个函数**，如：

```
function runAsync()\\{
    var p = new Promise(function(resolve, reject)\\{
        //做一些异步操作
        setTimeout(function()\\{
            console.log('执行完成');
            resolve('随便什么数据');
        \\}, 2000);
    \\});
    return p;            
\\}
runAsync()
```

这时候你应该有两个疑问：1.包装这么一个函数有毛线用？2.resolve('随便什么数据');这是干毛的？

我们继续来讲。在我们包装好的函数最后，会return出Promise对象，也就是说，执行这个函数我们得到了一个Promise对象。还记得Promise对象上有then、catch方法吧？这就是强大之处了，看下面的代码：

```
runAsync().then(function(data)\\{
    console.log(data);
    //后面可以用传过来的数据做些其他操作
    //......
\\});
```

**在runAsync()的返回上直接调用then方法，then接收一个参数，是函数，并且会拿到我们在runAsync中调用resolve时传的的参数。**

运行这段代码，会在2秒后输出“执行完成”，紧接着输出“随便什么数据”。

这时候你应该有所领悟了，原来then里面的函数就跟我们平时的回调函数一个意思，能够在runAsync这个异步任务执行完成之后被执行。这就是Promise的作用了，简单来讲，就是能把原来的回调写法分离出来，在异步操作执行完后，用链式调用的方式执行回调函数。

你可能会不屑一顾，那么牛逼轰轰的Promise就这点能耐？我把回调函数封装一下，给runAsync传进去不也一样吗，就像这样：

```
function runAsync(callback)\\{
    setTimeout(function()\\{
        console.log('执行完成');
        callback('随便什么数据');
    \\}, 2000);
\\}

runAsync(function(data)\\{
    console.log(data);
\\});
```

效果也是一样的，还费劲用Promise干嘛。那么问题来了，有**多层回调**该怎么办？如果callback也是一个异步操作，而且执行完后也需要有相应的回调函数，该怎么办呢？总不能再定义一个callback2，然后给callback传进去吧。而Promise的优势在于，**可以在then方法中继续写Promise对象并返回，然后继续调用then来进行回调操作。**

 

### 链式操作的用法

所以，从表面上看，Promise只是能够**简化层层回调的写法**，而实质上，**Promise的精髓是“状态”，用维护状态、传递状态的方式来使得回调函数能够及时调用，它比传递callback函数要简单、灵活的多。**

所以使用Promise的正确场景是这样的：

```
runAsync1()
.then(function(data)\\{
    console.log(data);
    return runAsync2();
\\})
.then(function(data)\\{
    console.log(data);
    return runAsync3();
\\})
.then(function(data)\\{
    console.log(data);
\\});
```

这样能够按顺序，每隔两秒输出每个异步回调中的内容，在runAsync2中传给resolve的数据，能在接下来的then方法中拿到。运行结果如下：

![img](https://images2015.cnblogs.com/blog/520134/201603/520134-20160311004311507-221152206.png)

猜猜runAsync1、runAsync2、runAsync3这三个函数都是如何定义的？没错，就是下面这样（代码较长请自行展开）：

```
function runAsync1()\\{
    var p = new Promise(function(resolve, reject)\\{
        //做一些异步操作
        setTimeout(function()\\{
            console.log('异步任务1执行完成');
            resolve('随便什么数据1');
        \\}, 1000);
    \\});
    return p;            
\\}
function runAsync2()\\{
    var p = new Promise(function(resolve, reject)\\{
        //做一些异步操作
        setTimeout(function()\\{
            console.log('异步任务2执行完成');
            resolve('随便什么数据2');
        \\}, 2000);
    \\});
    return p;            
\\}
function runAsync3()\\{
    var p = new Promise(function(resolve, reject)\\{
        //做一些异步操作
        setTimeout(function()\\{
            console.log('异步任务3执行完成');
            resolve('随便什么数据3');
        \\}, 2000);
    \\});
    return p;            
\\}
```

在then方法中，你也可以直接return数据而不是Promise对象，在后面的then中就可以接收到数据了，比如我们把上面的代码修改成这样：

```
runAsync1()
.then(function(data)\\{
    console.log(data);
    return runAsync2();
\\})
.then(function(data)\\{
    console.log(data);
    return '直接返回数据';  //这里直接返回数据
\\})
.then(function(data)\\{
    console.log(data);
\\});
```

那么输出就变成了这样：

![img](https://images2015.cnblogs.com/blog/520134/201603/520134-20160311004444163-67067993.png)

 

### reject的用法

到这里，你应该对“Promise是什么玩意”有了最基本的了解。那么我们接着来看看ES6的Promise还有哪些功能。我们光用了resolve，还没用reject呢，它是做什么的呢？事实上，我们前面的例子都是只有“执行成功”的回调，还没有“失败”的情况，reject的作用就是把Promise的状态置为rejected，这样我们在then中就能捕捉到，然后执行“失败”情况的回调。看下面的代码。

```
function getNumber()\\{
    var p = new Promise(function(resolve, reject)\\{
        //做一些异步操作
        setTimeout(function()\\{
            var num = Math.ceil(Math.random()*10); //生成1-10的随机数
            if(num<=5)\\{
                resolve(num);
            \\}
            else\\{
                reject('数字太大了');
            \\}
        \\}, 2000);
    \\});
    return p;            
\\}

getNumber()
.then(
    function(data)\\{
        console.log('resolved');
        console.log(data);
    \\}, 
    function(reason, data)\\{
        console.log('rejected');
        console.log(reason);
    \\}
);
```

getNumber函数用来异步获取一个数字，2秒后执行完成，如果数字小于等于5，我们认为是“成功”了，调用resolve修改Promise的状态。否则我们认为是“失败”了，调用reject并传递一个参数，作为失败的原因。

运行getNumber并且在then中传了两个参数，then方法可以接受两个参数，第一个对应resolve的回调，第二个对应reject的回调。所以我们能够分别拿到他们传过来的数据。多次运行这段代码，你会随机得到下面两种结果：

![img](https://images2015.cnblogs.com/blog/520134/201603/520134-20160311004607960-1156803894.png) 或者 ![img](https://images2015.cnblogs.com/blog/520134/201603/520134-20160311004616257-1024778840.png)

 

### catch的用法

我们知道Promise对象除了then方法，还有一个catch方法，它是做什么用的呢？其实它和then的第二个参数一样，用来指定reject的回调，用法是这样：

```
getNumber()
	.then(function(data)\\{
    	console.log('resolved');
    	console.log(data);
	\\})
	.catch(function(reason)\\{
    	console.log('rejected');
    	console.log(reason);
	\\});
```

效果和写在then的第二个参数里面一样。不过它还有另外一个作用：在执行resolve的回调（也就是上面then中的第一个参数）时，**如果抛出异常了（代码出错了），那么并不会报错卡死js，而是会进到这个catch方法中。**请看下面的代码：

```
getNumber()
	.then(function(data)\\{
    	console.log('resolved');
    	console.log(data);
    	console.log(somedata); //此处的somedata未定义
	\\})
	.catch(function(reason)\\{
    	console.log('rejected');
    	console.log(reason);
	\\});
```

在resolve的回调中，我们console.log(somedata);而somedata这个变量是没有被定义的。如果我们不用Promise，代码运行到这里就直接在控制台报错了，不往下运行了。但是在这里，会得到这样的结果：

![img](https://images2015.cnblogs.com/blog/520134/201603/520134-20160311004747147-1508291069.png)

也就是说进到catch方法里面去了，而且把错误原因传到了reason参数中。即便是有错误的代码也不会报错了，这与我们的try/catch语句有相同的功能。

 

### all的用法

Promise的all方法提供了并行执行异步操作的能力，并且在所有异步操作执行完后才执行回调。我们仍旧使用上面定义好的runAsync1、runAsync2、runAsync3这三个函数，看下面的例子：

```
Promise
.all([runAsync1(), runAsync2(), runAsync3()])
.then(function(results)\\{
    console.log(results);
\\});
```

用Promise.all来执行，all接收一个数组参数，里面的值最终都算返回Promise对象。这样，三个异步操作的并行执行的，等到它们都执行完后才会进到then里面。那么，三个异步操作返回的数据哪里去了呢？都在then里面呢，all会把所有异步操作的结果放进一个数组中传给then，就是上面的results。所以上面代码的输出结果就是：

![img](https://images2015.cnblogs.com/blog/520134/201603/520134-20160311004843491-346782307.png)

有了all，你就可以**并行执行多个异步操作，并且在一个回调中处理所有的返回数据**，是不是很酷？有一个场景是很适合用这个的，一些游戏类的素材比较多的应用，打开网页时，预先加载需要用到的各种资源如图片、flash以及各种静态文件。所有的都加载完后，我们再进行页面的初始化。

 

### race的用法

all方法的效果实际上是「**谁跑的慢，以谁为准执行回调**」，那么相对的就有另一个方法「**谁跑的快，以谁为准执行回调**」，这就是race方法，这个词本来就是赛跑的意思。race的用法与all一样，我们把上面runAsync1的延时改为1秒来看一下：

```
Promise
.race([runAsync1(), runAsync2(), runAsync3()])
.then(function(results)\\{
    console.log(results);
\\});
```

这三个异步操作同样是并行执行的。结果你应该可以猜到，1秒后runAsync1已经执行完了，此时then里面的就执行了。结果是这样的：

![img](https://images2015.cnblogs.com/blog/520134/201603/520134-20160311004946022-706413123.png)

你猜对了吗？不完全，是吧。在then里面的回调开始执行时，runAsync2()和runAsync3()并没有停止，仍旧再执行。于是再过1秒后，输出了他们结束的标志。

这个race有什么用呢？使用场景还是很多的，比如我们**可以用race给某个异步请求设置超时时间，并且在超时后执行相应的操作**，代码如下：

```
//请求某个图片资源
function requestImg()\\{
    var p = new Promise(function(resolve, reject)\\{
        var img = new Image();
        img.onload = function()\\{
            resolve(img);
        \\}
        img.src = 'xxxxxx';
    \\});
    return p;
\\}

//延时函数，用于给请求计时
function timeout()\\{
    var p = new Promise(function(resolve, reject)\\{
        setTimeout(function()\\{
            reject('图片请求超时');
        \\}, 5000);
    \\});
    return p;
\\}

Promise
.race([requestImg(), timeout()])
.then(function(results)\\{
    console.log(results);
\\})
.catch(function(reason)\\{
    console.log(reason);
\\});
```

requestImg函数会异步请求一张图片，我把地址写为"xxxxxx"，所以肯定是无法成功请求到的。timeout函数是一个延时5秒的异步操作。我们把这两个返回Promise对象的函数放进race，于是他俩就会赛跑，如果5秒之内图片请求成功了，那么遍进入then方法，执行正常的流程。如果5秒钟图片还未成功返回，那么timeout就跑赢了，则进入catch，报出“图片请求超时”的信息。运行结果如下：

![img](https://images2015.cnblogs.com/blog/520134/201603/520134-20160311005040272-341718790.png)

 

### 总结

ES6 Promise的内容就这些吗？是的，能用到的基本就这些。

我怎么还见过done、finally、success、fail等，这些是啥？这些并不在Promise标准中，而是我们自己实现的语法糖。

本文中所有异步操作均以setTimeout为例子，之所以不使用ajax是为了避免引起混淆，因为谈起ajax，很多人的第一反应就是jquery的ajax，而jquery又有自己的Promise实现。如果你理解了原理，就知道使用setTimeout和使用ajax是一样的意思。说起jquery，我不得不吐槽一句，jquery的Promise实现太过垃圾，各种语法糖把人都搞蒙了，我认为Promise之所以没有全面普及和jquery有很大的关系。后面我们会细讲jquery。

 

------



### 大白话讲解Promise（二）理解Promise规范

上一篇我们讲解了ES6中Promise的用法，但是知道了用法还远远不够，作为一名专业的前端工程师，还必须通晓原理。所以，为了补全我们关于Promise的知识树，有必要理解Promise/A+规范，理解了它你才能知道Promise内部是怎么回事，我们ES6中的Promise是如何一路走来的。

网上关于Promise/A+的翻译文档很多，所以我就不翻译一次了，本篇的目的在于为文档增加一些标注，以帮助我们更好的理解。翻译内容引用自：http://malcolmyu.github.io/malnote/2015/06/12/Promises-A-Plus/，部分我认为不太合适的有作修改。

 

### 术语

#### Promise

promise 是一个拥有 `then` 方法的对象或函数，其行为符合本规范；

#### thenable

是一个定义了 `then` 方法的对象或函数，文中译作“拥有 `then` 方法”；

#### 值（value）

指任何 JavaScript 的合法值（包括 `undefined` , thenable 和 promise）；

#### 异常（exception）

是使用 `throw` 语句抛出的一个值。

#### 拒绝原因（reason）

表示一个 promise 的拒绝原因。



### 要求

#### Promise 的状态

一个 Promise 的当前状态必须为以下三种状态中的一种：**等待态（Pending）、完成态（Fulfilled）和拒绝态（Rejected）**。

#### 等待态（Pending）

处于等待态时，promise 需满足以下条件：

- 可以迁移至完成态或拒绝态

#### 完成态（Fulfilled）

处于完成态时，promise 需满足以下条件：

- 不能迁移至其他任何状态
- 必须拥有一个**不可变**的终值

#### 拒绝态（Rejected）

处于拒绝态时，promise 需满足以下条件：

- 不能迁移至其他任何状态
- 必须拥有一个**不可变**的据因

这里的不可变指的是恒等（即可用 `===` 判断相等），而不是意味着更深层次的不可变（**译者注：** 盖指当 value 或 reason 不是基本值时，只要求其引用地址相等，但属性值可被更改）。



### Then 方法

一个 promise 必须提供一个 `then` 方法以访问其当前值、终值和据因。

promise 的 `then` 方法接受两个参数：

promise.then(onFulfilled, onRejected)

参数可选

`onFulfilled` 和 `onRejected` 都是可选参数。

- 如果 `onFulfilled` 不是函数，其必须被忽略
- 如果 `onRejected` 不是函数，其必须被忽略

注：如果我们只想传onRejected而不想传onFulfilled，可以这么写：pormise.then(null, onRejected)

#### `onFulfilled` 特性

如果 `onFulfilled` 是函数：

- 当 `promise` 执行结束后其必须被调用，其第一个参数为 `promise` 的终值
- 在 `promise` 执行结束前其不可被调用
- 其调用次数不可超过一次

#### `onRejected` 特性

如果 `onRejected` 是函数：

- 当 `promise` 被拒绝执行后其必须被调用，其第一个参数为 `promise` 的据因
- 在 `promise` 被拒绝执行前其不可被调用
- 其调用次数不可超过一次

#### 调用时机

`onFulfilled` 和 `onRejected` 只有在[执行环境](http://es5.github.io/#x10.3)堆栈仅包含**平台代码**时才可被调用 [注1](http://malcolmyu.github.io/malnote/2015/06/12/Promises-A-Plus/#note-1)

#### 调用要求

`onFulfilled` 和 `onRejected` 必须被作为函数调用（即没有 `this` 值）[注2](http://malcolmyu.github.io/malnote/2015/06/12/Promises-A-Plus/#note-2) 

注：也就是说，我们在promise中就别用this了。

#### 多次调用

`then` 方法可以被同一个 `promise` 调用多次

- 当 `promise` 成功执行时，所有 `onFulfilled` 需按照其注册顺序依次回调
- 当 `promise` 被拒绝执行时，所有的 `onRejected` 需按照其注册顺序依次回调

注：这里解释了我们可以链式调用，promise.then().then().then()

#### 返回

`then` 方法必须返回一个 `promise` 对象 [注3](http://malcolmyu.github.io/malnote/2015/06/12/Promises-A-Plus/#note-3)

promise2 = promise1.then(onFulfilled, onRejected);

注：这就是我们能够进行链式调用的原因，因为then方法返回的还是一个promise对象。

如果 `onFulfilled` 或者 `onRejected` 返回一个值 `x` ，则运行下面的 **Promise 解决过程**：`[[Resolve]](promise2, x)`

- 如果 `onFulfilled` 或者 `onRejected` 抛出一个异常 `e` ，则 `promise2` 必须拒绝执行，并返回拒因 `e`
- 如果 `onFulfilled` 不是函数且 `promise1` 成功执行， `promise2` 必须成功执行并返回相同的值
- 如果 `onRejected` 不是函数且 `promise1` 拒绝执行， `promise2` 必须拒绝执行并返回相同的据因



### Promise 解决过程

**Promise 解决过程** 是一个抽象的操作，其需输入一个 `promise` 和一个值，我们表示为 `[[Resolve]](promise, x)`，如果 `x` 有`then` 方法且看上去像一个 Promise ，解决程序即尝试使 `promise` 接受 `x` 的状态；否则其用 `x` 的值来执行 `promise` 。

这种 *thenable* 的特性使得 Promise 的实现更具有通用性：只要其暴露出一个遵循 Promise/A+ 协议的 `then` 方法即可；这同时也使遵循 Promise/A+ 规范的实现可以与那些不太规范但可用的实现能良好共存。

运行 `[[Resolve]](promise, x)` 需遵循以下步骤：

#### `x` 与 `promise` 相等

如果 `promise` 和 `x` 指向同一对象，以 `TypeError` 为据因拒绝执行 `promise`

#### `x` 为 Promise

如果 `x` 为 Promise ，则使 `promise` 接受 `x` 的状态 [注4](http://malcolmyu.github.io/malnote/2015/06/12/Promises-A-Plus/#note-4)：

- 如果 `x` 处于等待态， `promise` 需保持为等待态直至 `x` 被执行或拒绝
- 如果 `x` 处于完成态，用相同的值执行 `promise`
- 如果 `x` 处于拒绝态，用相同的据因拒绝 `promise`

注：这里就是解释我们链式调用then时，可以继续进行异步操作，只要在onFulfilled中继续返回一个promise对象即可。例如：

```
runAsync1()
.then(function(data)\\{
  console.log(data);
  return runAsync2(); //返回值为promise对象
\\})
.then(function(data)\\{
  console.log(data);
  return runAsync3();
\\})
```

#### `x` 为对象或函数

如果 `x` 为对象或者函数：

- 把 `x.then` 赋值给 `then` [注5](http://malcolmyu.github.io/malnote/2015/06/12/Promises-A-Plus/#note-5)
- 如果取 `x.then` 的值时抛出错误 `e` ，则以 `e` 为据因拒绝 `promise`
- 如果 `then` 是函数，将 `x` 作为函数的作用域 `this` 调用之。传递两个回调函数作为参数，第一个参数叫做 `resolvePromise` ，第二个参数叫做 `rejectPromise`:
- - 如果 `resolvePromise` 以值 `y` 为参数被调用，则运行 `[[Resolve]](promise, y)`
  - 如果 `rejectPromise` 以据因 `r` 为参数被调用，则以据因 `r` 拒绝 `promise`
  - 如果 `resolvePromise` 和 `rejectPromise` 均被调用，或者被同一参数调用了多次，则优先采用首次调用并忽略剩下的调用
  - 如果调用 `then` 方法抛出了异常 `e`：
  - - 如果 `resolvePromise` 或 `rejectPromise` 已经被调用，则忽略之
    - 否则以 `e` 为据因拒绝 `promise`
  - 如果 `then` 不是函数，以 `x` 为参数执行 `promise`
- 如果 `x` 不为对象或者函数，以 `x` 为参数执行 `promise`

如果一个 promise 被一个循环的 *thenable* 链中的对象解决，而 `[[Resolve]](promise, thenable)` 的递归性质又使得其被再次调用，根据上述的算法将会陷入无限递归之中。算法虽不强制要求，但也鼓励施者检测这样的递归是否存在，若检测到存在则以一个可识别的`TypeError` 为据因来拒绝 `promise` [注6](http://malcolmyu.github.io/malnote/2015/06/12/Promises-A-Plus/#note-6)。

- **注1** 这里的**平台代码**指的是引擎、环境以及 promise 的实施代码。实践中要确保 `onFulfilled` 和 `onRejected` 方法异步执行，且应该在 `then` 方法被调用的那一轮事件循环之后的新执行栈中执行。这个事件队列可以采用“宏任务（macro-task）”机制或者“微任务（micro-task）”机制来实现。由于 promise 的实施代码本身就是平台代码（**译者注：** 即都是 JavaScript），故代码自身在处理在处理程序时可能已经包含一个任务调度队列或[『跳板』](https://en.wikipedia.org/wiki/Trampoline_(computing))。

  **译者注：** 这里提及了 macrotask 和 microtask 两个概念，这表示异步任务的两种分类。在挂起任务时，JS 引擎会将所有任务按照类别分到这两个队列中，首先在 macrotask 的队列（这个队列也被叫做 task queue）中取出第一个任务，执行完毕后取出 microtask 队列中的所有任务顺序执行；之后再取 macrotask 任务，周而复始，直至两个队列的任务都取完。

  两个类别的具体分类如下：

- - **macro-task:** script（整体代码）, `setTimeout`, `setInterval`, `setImmediate`, I/O, UI rendering

  - **micro-task:** `process.nextTick`, `Promises`（这里指浏览器实现的原生 Promise）, `Object.observe`,`MutationObserver`

    详见 [stackoverflow 解答](http://stackoverflow.com/questions/25915634/difference-between-microtask-and-macrotask-within-an-event-loop-context) 或 [这篇博客](http://wengeezhang.com/?p=11)

- **注2** 也就是说在 **严格模式（strict）** 中，函数 `this` 的值为 `undefined` ；在非严格模式中其为全局对象。

- **注3** 代码实现在满足所有要求的情况下可以允许 `promise2 === promise1` 。每个实现都要文档说明其是否允许以及在何种条件下允许 `promise2 === promise1` 。

- **注4** 总体来说，如果 `x` 符合当前实现，我们才认为它是真正的 *promise* 。这一规则允许那些特例实现接受符合已知要求的 Promises 状态。

- **注5** 这步我们先是存储了一个指向 `x.then` 的引用，然后测试并调用该引用，以避免多次访问 `x.then` 属性。这种预防措施确保了该属性的一致性，因为其值可能在检索调用时被改变。

- **注6** 实现不应该对 *thenable* 链的深度设限，并假定超出本限制的递归就是无限循环。只有真正的循环递归才应能导致 `TypeError` 异常；如果一条无限长的链上 *thenable* 均不相同，那么递归下去永远是正确的行为。

补充：Promise/A+并未规定all和race方法，也就是说这两个方法是ES6自己增加的了。因为Promise/A+只是规范，ES6是做了自己的实现，当然可以自己加了。实现Promise规范的库有很多，比如jquery、dojo等，jquery在实现的时候还增加了更多的方法，我们在下一篇会做讲解。网上也有不少朋友自己实现过Promise/A+，列出来供大家参考：

https://github.com/linkFly6/Promise

https://github.com/hanan198501/promise

对于规范，有些同学不太想看，我平时在面试的时候问起一些规范相关的问题，大多数面试者都回答不来。有些人或许会说，作为司机会开车不就行了，难道要知道汽车是怎么造的吗？那我这里想反问一下，你准备当一辈子司机吗？对于规范可以不那么充分研究，但是起码得知道关键部分，有这样一个意识，对于以后自己成长为大牛也有所帮助。



### 大白话讲解Promise（三）搞懂jquery中的Promise

[前两篇](http://www.cnblogs.com/lvdabao/p/es6-promise-1.html)我们讲了ES6中的Promise以及Promise/A+规范，在Promise的知识体系中，jquery当然是必不可少的一环，所以本篇就来讲讲jquery中的Promise，也就是我们所知道的Deferred对象。

事实上，在此之前网上有很多文章在讲jquery Deferred对象了，但是总喜欢把ajax和Deferred混在一起讲，容易把人搞混。when、done、promise、success、error、fail、then、resolve、reject、always这么多方法不能揉在一起讲，需要把他们捋一捋，哪些是Deferred对象的方法，哪些是ajax的语法糖，我们需要心知肚明。

 

#### **先讲$.Deferred**

jquery用$.Deferred实现了Promise规范，$.Deferred是个什么玩意呢？还是老方法，打印出来看看，先有个直观印象：

```
var def = $.Deferred();
console.log(def);
```

输出如下：

![img](https://images2015.cnblogs.com/blog/520134/201603/520134-20160329213911379-199799420.png)

$.Deferred()返回一个对象，我们可以称之为Deferred对象，上面挂着一些熟悉的方法如：done、fail、then等。jquery就是用这个Deferred对象来注册异步操作的回调函数，修改并传递异步操作的状态。

Deferred对象的基本用法如下，为了不与ajax混淆，我们依旧举setTimeout的例子：

```
function runAsync()\\{
    var def = $.Deferred();
    //做一些异步操作
    setTimeout(function()\\{
        console.log('执行完成');
        def.resolve('随便什么数据');
    \\}, 2000);
    return def;
\\}
runAsync().then(function(data)\\{
    console.log(data)
\\});
```

在runAsync函数中，我们首先定义了一个def对象，然后进行一个延时操作，在2秒后调用def.resolve()，最后把def作为函数的返回。调用runAsync的时候将返回def对象，然后我们就可以.then来执行回调函数。

是不是感觉和ES6的Promise很像呢？我们来回忆一下第一篇中ES6的例子：

```
function runAsync()\\{
    var p = new Promise(function(resolve, reject)\\{
        //做一些异步操作
        setTimeout(function()\\{
            console.log('执行完成');
            resolve('随便什么数据');
        \\}, 2000);
    \\});
    return p;           
\\}
runAsync()
```

区别在何处一看便知。由于jquery的def对象本身就有resolve方法，所以我们在创建def对象的时候并未像ES6这样传入了一个函数参数，是空的。在后面可以直接def.resolve()这样调用。

这样也有一个弊端，因为执行runAsync()可以拿到def对象，而def对象上又有resolve方法，那么岂不是可以在外部就修改def的状态了？比如我把上面的代码修改如下：

```
var d = runAsync();
d.then(function(data)\\{
    console.log(data)
\\});
d.resolve('在外部结束');
```

现象会如何呢？并不会在2秒后输出“执行完成”，而是直接输出“在外部结束”。因为我们在异步操作执行完成之前，没等他自己resolve，就在外部给resolve了。这显然是有风险的，比如你定义的一个异步操作并指定好回调函数，有可能被别人给提前结束掉，你的回调函数也就不能执行了。

怎么办？jquery提供了一个promise方法，就在def对象上，他可以返回一个受限的Deferred对象，所谓受限就是没有resolve、reject等方法，无法从外部来改变他的状态，用法如下：

```
function runAsync()\\{
    var def = $.Deferred();
    //做一些异步操作
    setTimeout(function()\\{
        console.log('执行完成');
        def.resolve('随便什么数据');
    \\}, 2000);
    return def.promise(); //就在这里调用
\\}
```

这样返回的对象上就没有resolve方法了，也就无法从外部改变他的状态了。这个promise名字起的有点奇葩，容易让我们搞混，其实他就是一个返回受限Deferred对象的方法，与Promise规范没有任何关系，仅仅是名字叫做promise罢了。虽然名字奇葩，但是推荐使用。

 

### then的链式调用

既然Deferred也是Promise规范的实现者，那么其他特性也必须是支持的。链式调用的用法如下：

```
var d = runAsync();

d.then(function(data)\\{
    console.log(data);
    return runAsync2();
\\})
.then(function(data)\\{
    console.log(data);
    return runAsync3();
\\})
.then(function(data)\\{
    console.log(data);
\\});
```

与我们第一篇中的例子基本一样，可以参照。

 

### done与fail

我们知道，Promise规范中，then方法接受两个参数，分别是执行完成和执行失败的回调，而jquery中进行了增强，还可以接受第三个参数，就是在pending状态时的回调，如下：

```
deferred.then( doneFilter [, failFilter ] [, progressFilter ] )
```

除此之外，jquery还增加了两个语法糖方法，done和fail，分别用来指定执行完成和执行失败的回调，也就是说这段代码：

```
d.then(function()\\{
    console.log('执行完成');
\\}, function()\\{
    console.log('执行失败');
\\});
```

与这段代码是等价的：

```
d.done(function()\\{
    console.log('执行完成');
\\})
.fail(function()\\{
    console.log('执行失败');
\\});
```



### always的用法

jquery的Deferred对象上还有一个always方法，不论执行完成还是执行失败，always都会执行，有点类似ajax中的complete。不赘述了。

 

#### $.when的用法

jquery中，还有一个$.when方法来实现Promise，与ES6中的all方法功能一样，并行执行异步操作，在所有的异步操作执行完后才执行回调函数。不过$.when并没有定义在$.Deferred中，看名字就知道，$.when，它是一个单独的方法。与ES6的all的参数稍有区别，它接受的并不是数组，而是多个Deferred对象，如下：

```
$.when(runAsync(), runAsync2(), runAsync3())
.then(function(data1, data2, data3)\\{
    console.log('全部执行完成');
    console.log(data1, data2, data3);
\\});
```

jquery中没有像ES6中的race方法吗？就是以跑的快的为准的那个方法。对的，jquery中没有。

以上就是jquery中Deferred对象的常用方法了，还有一些其他的方法用的也不多，干脆就不记它了。接下来该说说ajax了。

 

#### **ajax与Deferred的关系**

jquery的ajax返回一个受限的Deferred对象，还记得受限的Deferred对象吧，也就是没有resolve方法和reject方法，不能从外部改变状态。想想也是，你发一个ajax请求别人从其他地方给你取消掉了，也是受不了的。

既然是Deferred对象，那么我们上面讲到的所有特性，ajax也都是可以用的。比如链式调用，连续发送多个请求：

```
req1 = function()\\{
    return $.ajax(/*...*/);
\\}
req2 = function()\\{
    return $.ajax(/*...*/);
\\}
req3 = function()\\{
    return $.ajax(/*...*/);
\\}

req1().then(req2).then(req3).done(function()\\{
    console.log('请求发送完毕');
\\});
```

明白了ajax返回对象的实质，那我们用起来就得心应手了。

 

#### **success、error与complete**

这三个方法或许是我们用的最多的，使用起来是这样的：

```
$.ajax(/*...*/)
.success(function()\\{/*...*/\\})
.error(function()\\{/*...*/\\})
.complete(function()\\{/*...*/\\})
```

分别表示ajax请求成功、失败、结束的回调。这三个方法与Deferred又是什么关系呢？其实就是语法糖，success对应done，error对应fail，complete对应always，就这样，只是为了与ajax的参数名字上保持一致而已，更方便大家记忆，看一眼源码：

```
deferred.promise( jqXHR ).complete = completeDeferred.add;
jqXHR.success = jqXHR.done;
jqXHR.error = jqXHR.fail;
```

complete那一行那么写，是为了减少重复代码，其实就是把done和fail又调用一次，与always中的代码一样。deferred.promise( jqXHR )这句也能看出，ajax返回的是受限的Deferred对象。

 

jquery加了这么些个语法糖，虽然上手门槛更低了，但是却造成了一定程度的混淆。一些人虽然这么写了很久，却一直不知道其中的原理，在面试的时候只能答出一些皮毛，这是很不好的。这也是我写这篇文章的缘由。

 

jquery中Deferred对象涉及到的方法很多，本文尽量分门别类的来介绍，希望能帮大家理清思路。总结一下就是：$.Deferred实现了Promise规范，then、done、fail、always是Deferred对象的方法。$.when是一个全局的方法，用来并行运行多个异步任务，与ES6的all是一个功能。ajax返回一个Deferred对象，success、error、complete是ajax提供的语法糖，功能与Deferred对象的done、fail、always一致。就酱。

