---
title: JavaScript执行机制
date: 2024-02-27 10:24:57
categories: 
- 前端知识
tags:
- JavaScript
---

### 简述同步和异步的区别，如何避免回调地狱

　　同步方法调用一旦开始，调用者必须等到方法调用返回后，才能继续后续的行为

　　异步方法调用一旦开始，方法调用就会立即返回，调用者就可以继续后续的操作。而异步方法通常会在另外一个线程中，整个过程，不会阻碍调用者的工作

　　避免回调地狱：

　　1）Promise

　　2）async/await

　　3）generator

　　4）事件发布/监听模式



### JS中try.. catch..的用法

**try** 测试代码块的错误。

**catch** 语句处理错误。

**throw** 创建并跑出错误。

```
 try
   \\{
   //在这里运行代码
     抛出错误
   \\}
 catch(err)
   \\{
   //在这里处理错误
   \\}
```

```
<p>请输出一个 5 到 10 之间的数字:</p>
<input id="demo" type="text">
<button type="button" onclick="myFunction()">测试输入</button>
<p id="mess"></p>

</body>
</html>
<script type="text/javascript">
    function myFunction()\\{
    try\\{ 
        var x=document.getElementById("demo").value;   取元素的值
        
        if(x=="")    throw "值为空";       根据获取的值，抛出错误
        if(isNaN(x)) throw "不是数字";
        if(x>10)     throw "太大";
        if(x<5)      throw "太小";
    \\}
    catch(err)\\{
        var y=document.getElementById("mess");     抓住上面throw抛出的错误，给p标签显示
        y.innerHTML="错误：" + err + "。";
    \\}
\\}
</script>
```

```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>try_catch</title>
</head>
<body>
</body>
	<script>
		//try_catch好处：发现错误但不让程序终止，继续执行之后的语句
		try\\{
			//先从上到下执行try里面的语句，一旦发现错误则跳出try，不再执行try下面的语句
			console.log("a");
			console.log(b);
			console.log("c");
		\\}catch(e)\\{
			//如果try中发现错误，则执行catch中的语句，如果没有错误，则跳过catch
			//e是个系统封装好的对象，包含name和message两个属性
			//分别是错误名称(ex:ReferenceError)和错误信心(ex:b is not defined)
			console.log(e.name+":"+e.message);
		\\}
		console.log('d');
	</script>
</html>
```



### async 

用于申明一个 function 是异步的，而 await 用于等待一个异步方法执行完成。

另外还有一个很有意思的语法规定，await 只能出现在 async 函数中。



### JavaScript执行机制

不论你是javascript新手还是老鸟，不论是面试求职，还是日常开发工作，我们经常会遇到这样的情况：给定的几行代码，我们需要知道其输出内容和顺序。因为javascript是一门单线程语言，所以我们可以得出结论：

javascript是按照语句出现的顺序执行的

看到这里读者要打人了：我难道不知道js是一行一行执行的？还用你说？稍安勿躁，正因为js是一行一行执行的，所以我们以为js都是这样的：

```javascript
let a = '1';
console.log(a);

let b = '2';
console.log(b);
```

![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2017/11/20/15fd87f7221d0dbe~tplv-t2oaga2asx-zoom-in-crop-mark:1512:0:0:0.awebp)

然而实际上js是这样的：

```javascript
setTimeout(function()\\{
    console.log('定时器开始啦')
\\});

new Promise(function(resolve)\\{
    console.log('马上执行for循环啦');
    for(var i = 0; i < 10000; i++)\\{
        i == 99 && resolve();
    \\}
\\}).then(function()\\{
    console.log('执行then函数啦')
\\});

console.log('代码执行结束');
```

![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2017/11/20/15fd87d38acc4905~tplv-t2oaga2asx-zoom-in-crop-mark:1512:0:0:0.awebp)

依照**js是按照语句出现的顺序执行**这个理念，我自信的写下输出结果：

```javascript
//"定时器开始啦"
//"马上执行for循环啦"
//"执行then函数啦"
//"代码执行结束"
```

去chrome上验证下，结果完全不对，瞬间懵了，说好的一行一行执行的呢？

![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2017/11/20/15fd8840f3c3f109~tplv-t2oaga2asx-zoom-in-crop-mark:1512:0:0:0.awebp)

我们真的要彻底弄明白javascript的执行机制了。

### 1.关于javascript

javascript是一门**单线程**语言，在最新的HTML5中提出了Web-Worker，但javascript是单线程这一核心仍未改变。所以一切javascript版的"多线程"都是用单线程模拟出来的，一切javascript多线程都是纸老虎！



### 2.javascript事件循环

既然js是单线程，那就像只有一个窗口的银行，客户需要排队一个一个办理业务，同理js任务也要一个一个顺序执行。如果一个任务耗时过长，那么后一个任务也必须等着。那么问题来了，假如我们想浏览新闻，但是新闻包含的超清图片加载很慢，难道我们的网页要一直卡着直到图片完全显示出来？因此聪明的程序员将任务分为两类：

- 同步任务
- 异步任务

当我们打开网站时，网页的渲染过程就是一大堆同步任务，比如页面骨架和页面元素的渲染。而像加载图片音乐之类占用资源大耗时久的任务，就是异步任务。关于这部分有严格的文字定义，但本文的目的是用最小的学习成本彻底弄懂执行机制，所以我们用导图来说明：

![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2017/11/21/15fdd88994142347~tplv-t2oaga2asx-zoom-in-crop-mark:1512:0:0:0.awebp)

导图要表达的内容用文字来表述的话：

- 同步和异步任务分别进入不同的执行"场所"，同步的进入主线程，异步的进入Event Table并注册函数。
- 当指定的事情完成时，Event Table会将这个函数移入Event Queue。
- 主线程内的任务执行完毕为空，会去Event Queue读取对应的函数，进入主线程执行。
- 上述过程会不断重复，也就是常说的Event Loop(事件循环)。

我们不禁要问了，那怎么知道主线程执行栈为空啊？js引擎存在monitoring process进程，会持续不断的检查主线程执行栈是否为空，一旦为空，就会去Event Queue那里检查是否有等待被调用的函数。

说了这么多文字，不如直接一段代码更直白：

```javascript
let data = [];
$.ajax(\\{
    url:www.javascript.com,
    data:data,
    success:() => \\{
        console.log('发送成功!');
    \\}
\\})
console.log('代码执行结束');
```

上面是一段简易的`ajax`请求代码：

- ajax进入Event Table，注册回调函数`success`。
- 执行`console.log('代码执行结束')`。
- ajax事件完成，回调函数`success`进入Event Queue。
- 主线程从Event Queue读取回调函数`success`并执行。

相信通过上面的文字和代码，你已经对js的执行顺序有了初步了解。接下来我们来研究进阶话题：setTimeout。



### 3.又爱又恨的setTimeout

大名鼎鼎的`setTimeout`无需再多言，大家对他的第一印象就是异步可以延时执行，我们经常这么实现延时3秒执行：

```javascript
setTimeout(() => \\{
    console.log('延时3秒');
\\},3000)
```

渐渐的`setTimeout`用的地方多了，问题也出现了，有时候明明写的延时3秒，实际却5，6秒才执行函数，这又咋回事啊？

先看一个例子：

```javascript
setTimeout(() => \\{
    task();
\\},3000)
console.log('执行console');
```

根据前面我们的结论，`setTimeout`是异步的，应该先执行`console.log`这个同步任务，所以我们的结论是：

```javascript
//执行console
//task()
```

去验证一下，结果正确！ 然后我们修改一下前面的代码：

```javascript
setTimeout(() => \\{
    task()
\\},3000)

sleep(10000000)
```

乍一看其实差不多嘛，但我们把这段代码在chrome执行一下，却发现控制台执行`task()`需要的时间远远超过3秒，说好的延时三秒，为啥现在需要这么长时间啊？

这时候我们需要重新理解`setTimeout`的定义。我们先说上述代码是怎么执行的：

- `task()`进入Event Table并注册,计时开始。
- 执行`sleep`函数，很慢，非常慢，计时仍在继续。
- 3秒到了，计时事件`timeout`完成，`task()`进入Event Queue，但是`sleep`也太慢了吧，还没执行完，只好等着。
- `sleep`终于执行完了，`task()`终于从Event Queue进入了主线程执行。

上述的流程走完，我们知道`setTimeout`这个函数，是经过指定时间后，把要执行的任务(本例中为`task()`)加入到Event Queue中，又因为是单线程任务要一个一个执行，如果前面的任务需要的时间太久，那么只能等着，导致真正的延迟时间远远大于3秒。

我们还经常遇到`setTimeout(fn,0)`这样的代码，0秒后执行又是什么意思呢？是不是可以立即执行呢？

答案是不会的，`setTimeout(fn,0)`的含义是，指定某个任务在主线程最早可得的空闲时间执行，意思就是不用再等多少秒了，只要主线程执行栈内的同步任务全部执行完成，栈为空就马上执行。举例说明：

```javascript
//代码1
console.log('先执行这里');
setTimeout(() => \\{
    console.log('执行啦')
\\},0);
//代码2
console.log('先执行这里');
setTimeout(() => \\{
    console.log('执行啦')
\\},3000);  
```

代码1的输出结果是：

```javascript
//先执行这里
//执行啦
```

代码2的输出结果是：

```javascript
//先执行这里
// ... 3s later
// 执行啦
```

关于`setTimeout`要补充的是，即便主线程为空，0毫秒实际上也是达不到的。根据HTML的标准，最低是4毫秒。有兴趣的同学可以自行了解。

#### 延时0毫秒有什么用？

`setTimeout` 函数用于设定一个定时器，在指定的时间后执行某个函数。即使延迟时间为0 (`0ms`)，`setTimeout` 仍然有一些重要的用途：

1. **异步执行**：即使延迟为0，`setTimeout` 也会把回调函数放入事件循环的“定时器队列”中。这意味着它会在当前同步代码执行完毕后，在下一个事件循环周期执行该回调。这可以防止回调函数阻塞当前执行栈。

2. **微任务与宏任务**：JavaScript 引擎区分了两种类型的任务，即微任务（microtasks）和宏任务（macrotasks）。`setTimeout` 属于宏任务，而像 `Promise` 的 `.then` 回调则属于微任务。因此，即使是0毫秒的 `setTimeout` 也会在当前宏任务完成之后执行，但在所有微任务完成之前。

3. **释放UI渲染**：在浏览器环境中，使用 `setTimeout` 可以让浏览器有机会去重绘和回流页面。这对于性能优化特别有用，例如，在进行大量DOM操作时，可以将多个DOM操作放在一个 `setTimeout` 的回调中，以减少重绘次数。

4. **避免栈溢出**：在递归调用或其他可能导致栈深度过大的情况下，使用 `setTimeout` 可以帮助避免栈溢出错误，因为它确保了每次递归调用都是在一个新的栈帧中执行的。

5. **脚本执行限制**：在某些情况下，长时间运行的脚本可能会被浏览器挂起，特别是在移动设备上。使用 `setTimeout` 可以帮助脚本在达到执行时间限制之前暂停，然后在下一周期继续执行。

综上所述，即使延迟为0，`setTimeout` 也有其存在的必要性和应用场景。在你的例子中，通过 `setTimeout` 调用 `sensorsTrack` 函数，可以确保该跟踪事件在当前执行栈清空后才被执行，不会干扰到当前的同步流程。



### 4.又恨又爱的setInterval

上面说完了`setTimeout`，当然不能错过它的孪生兄弟`setInterval`。他俩差不多，只不过后者是循环的执行。对于执行顺序来说，`setInterval`会每隔指定的时间将注册的函数置入Event Queue，如果前面的任务耗时太久，那么同样需要等待。

唯一需要注意的一点是，对于`setInterval(fn,ms)`来说，我们已经知道不是每过`ms`秒会执行一次`fn`，而是每过`ms`秒，会有`fn`进入Event Queue。一旦**`setInterval`的回调函数`fn`执行时间超过了延迟时间`ms`，那么就完全看不出来有时间间隔了**。这句话请读者仔细品味。



### 5.Promise与process.nextTick(callback)

传统的定时器我们已经研究过了，接着我们探究`Promise`与`process.nextTick(callback)`的表现。

`Promise`的定义和功能本文不再赘述，不了解的读者可以学习一下阮一峰老师的[Promise](https://link.juejin.cn?target=http\\%3A\\%2F\\%2Fes6.ruanyifeng.com\\%2F\\%23docs\\%2Fpromise)。而`process.nextTick(callback)`类似node.js版的"setTimeout"，在事件循环的下一次循环中调用 callback 回调函数。

我们进入正题，除了广义的同步任务和异步任务，我们对任务有更精细的定义：

- macro-task(宏任务)：包括整体代码script，setTimeout，setInterval
- micro-task(微任务)：Promise，process.nextTick

不同类型的任务会进入对应的Event Queue，比如`setTimeout`和`setInterval`会进入相同的Event Queue。

事件循环的顺序，决定js代码的执行顺序。进入整体代码(宏任务)后，开始第一次循环。接着执行所有的微任务。然后再次从宏任务开始，找到其中一个任务队列执行完毕，再执行所有的微任务。听起来有点绕，我们用文章最开始的一段代码说明：

```javascript
setTimeout(function() \\{
    console.log('setTimeout');
\\})

new Promise(function(resolve) \\{
    console.log('promise');
\\}).then(function() \\{
    console.log('then');
\\})

console.log('console');
```

- 这段代码作为宏任务，进入主线程。
- 先遇到`setTimeout`，那么将其回调函数注册后分发到宏任务Event Queue。(注册过程与上同，下文不再描述)
- 接下来遇到了`Promise`，`new Promise`立即执行，`then`函数分发到微任务Event Queue。
- 遇到`console.log()`，立即执行。
- 好啦，整体代码script作为第一个宏任务执行结束，看看有哪些微任务？我们发现了`then`在微任务Event Queue里面，执行。
- ok，第一轮事件循环结束了，我们开始第二轮循环，当然要从宏任务Event Queue开始。我们发现了宏任务Event Queue中`setTimeout`对应的回调函数，立即执行。
- 结束。

事件循环，宏任务，微任务的关系如图所示：

![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2017/11/21/15fdcea13361a1ec~tplv-t2oaga2asx-zoom-in-crop-mark:1512:0:0:0.awebp)

我们来分析一段较复杂的代码，看看你是否真的掌握了js的执行机制：

```javascript
console.log('1');

setTimeout(function() \\{
    console.log('2');
    process.nextTick(function() \\{
        console.log('3');
    \\})
    new Promise(function(resolve) \\{
        console.log('4');
        resolve();
    \\}).then(function() \\{
        console.log('5')
    \\})
\\})
process.nextTick(function() \\{
    console.log('6');
\\})
new Promise(function(resolve) \\{
    console.log('7');
    resolve();
\\}).then(function() \\{
    console.log('8')
\\})

setTimeout(function() \\{
    console.log('9');
    process.nextTick(function() \\{
        console.log('10');
    \\})
    new Promise(function(resolve) \\{
        console.log('11');
        resolve();
    \\}).then(function() \\{
        console.log('12')
    \\})
\\})
```

第一轮事件循环流程分析如下：

- 整体script作为第一个宏任务进入主线程，遇到`console.log`，输出1。
- 遇到`setTimeout`，其回调函数被分发到宏任务Event Queue中。我们暂且记为`setTimeout1`。
- 遇到`process.nextTick()`，其回调函数被分发到微任务Event Queue中。我们记为`process1`。
- 遇到`Promise`，`new Promise`直接执行，输出7。`then`被分发到微任务Event Queue中。我们记为`then1`。
- 又遇到了`setTimeout`，其回调函数被分发到宏任务Event Queue中，我们记为`setTimeout2`。

| 宏任务Event Queue | 微任务Event Queue |
| ----------------- | ----------------- |
| setTimeout1       | process1          |
| setTimeout2       | then1             |

- 上表是第一轮事件循环宏任务结束时各Event Queue的情况，此时已经输出了1和7。
- 我们发现了`process1`和`then1`两个微任务。
- 执行`process1`,输出6。
- 执行`then1`，输出8。

好了，第一轮事件循环正式结束，这一轮的结果是输出1，7，6，8。那么第二轮时间循环从`setTimeout1`宏任务开始：

- 首先输出2。接下来遇到了`process.nextTick()`，同样将其分发到微任务Event Queue中，记为`process2`。`new Promise`立即执行输出4，`then`也分发到微任务Event Queue中，记为`then2`。

| 宏任务Event Queue | 微任务Event Queue |
| ----------------- | ----------------- |
| setTimeout2       | process2          |
|                   | then2             |

- 第二轮事件循环宏任务结束，我们发现有`process2`和`then2`两个微任务可以执行。
- 输出3。
- 输出5。
- 第二轮事件循环结束，第二轮输出2，4，3，5。
- 第三轮事件循环开始，此时只剩setTimeout2了，执行。
- 直接输出9。
- 将`process.nextTick()`分发到微任务Event Queue中。记为`process3`。
- 直接执行`new Promise`，输出11。
- 将`then`分发到微任务Event Queue中，记为`then3`。

| 宏任务Event Queue | 微任务Event Queue |
| ----------------- | ----------------- |
|                   | process3          |
|                   | then3             |

- 第三轮事件循环宏任务执行结束，执行两个微任务`process3`和`then3`。
- 输出10。
- 输出12。
- 第三轮事件循环结束，第三轮输出9，11，10，12。

整段代码，共进行了三次事件循环，完整的输出为1，7，6，8，2，4，3，5，9，11，10，12。 (请注意，node环境下的事件监听依赖libuv与前端环境不完全相同，输出顺序可能会有误差)



### 6.写在最后

#### (1)js的异步

我们从最开头就说javascript是一门单线程语言，不管是什么新框架新语法糖实现的所谓异步，其实都是用同步的方法去模拟的，牢牢把握住单线程这点非常重要。

#### (2)事件循环Event Loop

事件循环是js实现异步的一种方法，也是js的执行机制。

#### (3)javascript的执行和运行

执行和运行有很大的区别，javascript在不同的环境下，比如node，浏览器，Ringo等等，执行方式是不同的。而运行大多指javascript解析引擎，是统一的。

#### (4)setImmediate

微任务和宏任务还有很多种类，比如`setImmediate`等等，执行都是有共同点的，有兴趣的同学可以自行了解。

#### (5)最后的最后

- javascript是一门单线程语言
- Event Loop是javascript的执行机制

牢牢把握两个基本点，以认真学习javascript为中心，早日实现成为前端高手的伟大梦想！

![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2017/11/21/15fdd96beade6575~tplv-t2oaga2asx-zoom-in-crop-mark:1512:0:0:0.awebp)


原文链接：https://juejin.cn/post/6844903512845860872







# 代码题: 看代码说结果, 事件循环 + async 函数

### 1.基本的 async/await 和事件循环

```
console.log('1');

async function asyncFunc() \\{
    console.log('2');
    await Promise.resolve();
    console.log('3');
\\}

asyncFunc();

console.log('4');
```

#### 执行顺序：

执行顺序：

1. 打印 `1`

2. 定义异步函数 `asyncFunc`，但并不执行它。

3. 调用

   ```
   asyncFunc()
   ```

   - 打印 `2`
   - 遇到 `await`，所以 `asyncFunc` 的后续代码（打印 `3`）被移到事件队列中等待。

4. 打印 `4`

5. 所有同步代码执行完毕后，事件循环开始执行队列中的任务。

   - 打印 `3`

#### 预期输出：

```
1
2
3
4
```



### 2.setTimeout 和 async/await 的结合

```
console.log('1');

setTimeout(() => \\{
    console.log('2');
\\}, 0);

async function asyncFunc() \\{
    console.log('3');
    await Promise.resolve();
    console.log('4');
\\}

asyncFunc();

console.log('5');
```

#### 执行顺序：

1. 打印 1
2. 将 setTimeout 回调（打印 2）设置为在0毫秒后执行。但实际上，它会被放入宏任务队列，等待所有微任务完成。
3. 定义异步函数 asyncFunc，但并不执行。
4. 调用 asyncFunc()。
   打印 3
   遇到 await，所以 asyncFunc 的后续代码（打印 4）被移到微任务队列中等待。
5. 打印 5
6. 执行微任务队列中的任务（因为微任务的优先级高于宏任务）。
   打印 4
7. 执行宏任务队列中的任务。
   打印 2

#### 预期输出：

```
1
3
5
4
2
```



### 3.嵌套的 async/await

```
console.log('1');

async function firstAsync() \\{
    console.log('2');
    await secondAsync();
    console.log('3');
\\}

async function secondAsync() \\{
    console.log('4');
    await Promise.resolve();
    console.log('5');
\\}

firstAsync();

console.log('6');
```

#### 执行顺序：

1. 打印 1
2. 定义两个异步函数，但不执行。
3. 调用 firstAsync()。
   打印 2
   调用 secondAsync()。
           打印 4
           遇到 await，所以 secondAsync 的后续代码（打印 5）被移到微任务队列中等待。
   firstAsync 的后续代码（打印 3）也被移到微任务队列中等待。
4. 打印 6
5. 执行微任务队列中的任务。
   打印 5
   打印 3

#### 预期输出：

```
1
2
4
6
5
3
```


### 4.多个异步函数

```
async function asyncOne() \\{
 console.log('1');
 await Promise.resolve();
 console.log('2');
\\}

async function asyncTwo() \\{
    console.log('3');
    await Promise.resolve();
    console.log('4');
\\}

console.log('5');

asyncOne();
asyncTwo();

console.log('6');
```

#### 执行顺序：

1. 定义两个异步函数，但不执行。
2. 打印 5
3. 调用 asyncOne()。
   打印 1
   遇到 await，所以 asyncOne 的后续代码（打印 2）被移到微任务队列中等待。
4. 调用 asyncTwo()。
   打印 3
   遇到 await，所以 asyncTwo 的后续代码（打印 4）被移到微任务队列中等待。
5. 打印 6
6. 执行微任务队列中的任务。
   打印 2
   打印 4

#### 预期输出：

```
5
1
3
6
2
4
```


### 5.Promise 的基本行为

```
console.log('1');

Promise.resolve().then(() => \\{
    console.log('2');
\\});

console.log('3');
```

#### 执行顺序：

1. 打印 1
2. 创建一个已解决的Promise，并在微任务队列中注册一个回调。
3. 打印 3
4. 当同步代码执行完成后，事件循环开始处理微任务队列，执行回调。
5. 打印 2

#### 预期输出：

```
1
3
2
```


#### 6.setTimeout 与 Promise 的组合

```
console.log('1');

setTimeout(() => \\{
    console.log('2');
\\}, 0);

Promise.resolve().then(() => \\{
    console.log('3');
\\}).then(() => \\{
    console.log('4');
\\});

console.log('5');
```

#### 执行顺序：

1. 打印 1
2. 将setTimeout的回调加入宏任务队列
3. 创建一个已解决的Promise，并在微任务队列中注册第一个回调
4. 在第一个then的回调中，注册第二个then的回调到微任务队列
5. 打印 5
6. 事件循环开始处理微任务，首先执行第一个then的回调
7. 打印 3
8. 紧接着，事件循环处理第二个then的回调
9. 打印 4
10. 最后，事件循环处理宏任务队列
11. 打印 2

#### 预期输出：

```
1
5
3
4
2
```




### 7.多个 async/await 的嵌套

```
console.log('1');

async function outerAsync() \\{
    console.log('2');
    await innerAsync();
    console.log('3');
\\}

async function innerAsync() \\{
    console.log('4');
    await new Promise(resolve => setTimeout(resolve, 0));
    console.log('5');
\\}

outerAsync();

console.log('6');
```

#### 执行顺序：

1. 打印 1
2. 定义两个异步函数，但此时并未执行它们
3. 调用 outerAsync()
4. 打印 2
5. 调用 innerAsync()
6. 打印 4
7. 遇到setTimeout，所以它的回调被加入宏任务队列
8. await将后续代码（打印 5 和 outerAsync 中的打印 3）移至微任务队列
9. 打印 6
10. 事件循环开始处理微任务，但在此之前，必须先完成setTimeout的回调，**必须要等里面完成才能完成外面**
11. 打印 5
12. 继续执行outerAsync中的代码
13. 打印 3

#### 预期输出：

```
1
2
4
6
5
3
```


### 8.多个微任务队列（这个不会）

```
console.log('1');

async function firstFunc() \\{
    console.log('2');
    await Promise.resolve();
    console.log('3');
\\}

async function secondFunc() \\{
    console.log('4');
    await Promise.resolve().then(() => \\{
        console.log('5');
    \\});
    console.log('6');
\\}

firstFunc();
secondFunc();
console.log('7');
```

#### 执行顺序：

1. 打印 1
2. 调用 firstFunc()
3. 打印 2
4. await使其后续代码（打印 3）移到微任务队列中
5. 调用 secondFunc()
6. 打印 4
7. await和then使其后续代码（首先打印 5，然后打印 6）移到微任务队列中
8. 打印 7
9. 事件循环开始处理微任务队列
10. 打印 5
11. 打印 3
12. 打印 6

#### 预期输出：

```
1
2
4
7
5
3
6
```


### 9.复杂的async/await与setTimeout

```
console.log('1');

setTimeout(() => \\{
    console.log('2');
\\}, 0);

async function asyncFunction() \\{
    console.log('3');
    await Promise.resolve();
    console.log('4');
    setTimeout(() => \\{
```

原文链接：https://blog.csdn.net/weixin_43850639/article/details/132599505







# promise

### promise是什么？

1、主要用于异步计算
 2、可以将异步操作队列化，按照期望的顺序执行，返回符合预期的结果
 3、可以在对象之间传递和操作promise，帮助我们处理队列



### 为什么会有promise？

**为了避免界面冻结（任务）**

- 同步：假设你去了一家饭店，找个位置，叫来服务员，这个时候服务员对你说，对不起我是“同步”服务员，我要服务完这张桌子才能招呼你。那桌客人明明已经吃上了，你只是想要个菜单，这么小的动作，服务员却要你等到别人的一个大动作完成之后，才能再来招呼你，这个便是同步的问题：也就是“顺序交付的工作1234，必须按照1234的顺序完成”。
- 异步：则是将耗时很长的A交付的工作交给系统之后，就去继续做B交付的工作，。等到系统完成了前面的工作之后，再通过回调或者事件，继续做A剩下的工作。
   AB工作的完成顺序，和交付他们的时间顺序无关，所以叫“异步”。



### 异步操作的常见语法

1. 事件监听

```jsx
document.getElementById('#start').addEventListener('click', start, false);
function start() \\{
  // 响应事件，进行相应的操作
\\}
// jquery on 监听
$('#start').on('click', start)
```

1. 回调

```jsx
// 比较常见的有ajax
$.ajax('http://www.wyunfei.com/', \\{
 success (res) \\{
   // 这里可以监听res返回的数据做回调逻辑的处理
 \\}
\\})

// 或者在页面加载完毕后回调
$(function() \\{
 // 页面结构加载完成，做回调逻辑处理
\\})
```



### 有了nodeJS之后...对异步的依赖进一步加剧了

大家都知道在nodeJS出来之前PHP、Java、python等后台语言已经很成熟了，nodejs要想能够有自己的一片天，那就得拿出点自己的绝活：
 **无阻塞高并发，是nodeJS的招牌，要达到无阻塞高并发异步是其基本保障**
 举例：查询数据从数据库，PHP第一个任务查询数据，后面有了新任务，那么后面任务会被挂起排队；而nodeJS是第一个任务挂起交给数据库去跑，然后去接待第二个任务交给对应的系统组件去处理挂起，接着去接待第三个任务...**那这样子的处理必然要依赖于异步操作**



### 异步回调的问题：

- 之前处理异步是通过纯粹的回调函数的形式进行处理
- 很容易进入到回调地狱中，剥夺了函数return的能力
- 问题可以解决，但是难以读懂，维护困难
- 稍有不慎就会踏入回调地狱 - 嵌套层次深，不好维护

![img](https:////upload-images.jianshu.io/upload_images/15311104-f36baae9a21490c7.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

回调地狱

一般情况我们一次性调用API就可以完成请求。
 有些情况需要多次调用服务器API，就会形成一个链式调用，比如为了完成一个功能，我们需要调用API1、API2、API3，依次按照顺序进行调用，这个时候就会出现回调地狱的问题



### promise

- promise是一个对象，对象和函数的区别就是对象可以保存状态，函数不可以（闭包除外）
- 并未剥夺函数return的能力，因此无需层层传递callback，进行回调获取数据
- 代码风格，容易理解，便于维护
- 多个异步等待合并便于解决



### promise详解

```jsx
new Promise(
  function (resolve, reject) \\{
    // 一段耗时的异步操作
    resolve('成功') // 数据处理完成
    // reject('失败') // 数据处理出错
  \\}
).then(
  (res) => \\{console.log(res)\\},  // 成功
  (err) => \\{console.log(err)\\} // 失败
)
```

- resolve作用是，将Promise对象的状态从“未完成”变为“成功”（即从 pending 变为 resolved），在异步操作成功时调用，并将异步操作的结果，作为参数传递出去；
   reject作用是，将Promise对象的状态从“未完成”变为“失败”（即从 pending 变为 rejected），在异步操作失败时调用，并将异步操作报出的错误，作为参数传递出去。
- promise有三个状态：
   1、pending[待定]初始状态
   2、fulfilled[实现]操作成功
   3、rejected[被否决]操作失败
   当promise状态发生改变，就会触发then()里的响应函数处理后续步骤；
   promise状态一经改变，不会再变。
- Promise对象的状态改变，只有两种可能：
   从pending变为fulfilled
   从pending变为rejected。
   这两种情况只要发生，状态就凝固了，不会再变了。

##### 最简单示例：

```jsx
new Promise(resolve => \\{
  setTimeout(() => \\{
    resolve('hello')
  \\}, 2000)
\\}).then(res => \\{
  console.log(res)
\\})
```

##### 分两次，顺序执行

```jsx
new Promise(resolve => \\{
    setTimeout(() => \\{
      resolve('hello')
    \\}, 2000)
  \\}).then(val => \\{
    console.log(val) //  参数val = 'hello'
    return new Promise(resolve => \\{
      setTimeout(() => \\{
        resolve('world')
      \\}, 2000)
    \\})
  \\}).then(val => \\{
    console.log(val) // 参数val = 'world'
  \\})
```

##### promise完成后then()

```jsx
let pro = new Promise(resolve => \\{
   setTimeout(() => \\{
     resolve('hello world')
   \\}, 2000)
 \\})
 setTimeout(() => \\{
   pro.then(value => \\{
   console.log(value) // hello world
 \\})
 \\}, 2000)
```

结论：promise作为队列最为重要的特性，我们在任何一个地方生成了一个promise队列之后，我们可以把他作为一个变量传递到其他地方。

##### 假如在.then()的函数里面不返回新的promise，会怎样？



### .then()

1、接收两个函数作为参数，分别代表fulfilled（成功）和rejected（失败）
 2、.then()返回一个新的Promise实例，所以它可以链式调用
 3、当前面的Promise状态改变时，.then()根据其最终状态，选择特定的状态响应函数执行
 4、状态响应函数可以返回新的promise，或其他值，不返回值也可以我们可以认为它返回了一个null；
 5、如果返回新的promise，那么下一级.then()会在新的promise状态改变之后执行
 6、如果返回其他任何值，则会立即执行下一级.then()

##### .then()里面有.then()的情况

1、因为.then()返回的还是Promise实例
 2、会等里面的then()执行完，再执行外面的

![img](https:////upload-images.jianshu.io/upload_images/15311104-53b61cb990d856b5.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

then嵌套

- 对于我们来说，此时最好将其展开，也是一样的结果，而且会更好读：

  ![img](https:////upload-images.jianshu.io/upload_images/15311104-7aa75490f79e0725.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

  展开增加可读性

##### 错误处理

Promise会自动捕获内部异常，并交给rejected响应函数处理。

1. 第一种错误处理

   ![img](https:////upload-images.jianshu.io/upload_images/15311104-d93b7cf287478e43.png?imageMogr2/auto-orient/strip|imageView2/2/w/860/format/webp)

   第一种错误处理

2. 第二种错误处理

   ![img](https:////upload-images.jianshu.io/upload_images/15311104-5e3ab96cbdcde863.png?imageMogr2/auto-orient/strip|imageView2/2/w/861/format/webp)

   第二种错误处理

- 错误处理两种做法：
   第一种：reject('错误信息').then(() => \\{\\}, () => \\{错误处理逻辑\\})
   第二种：throw new Error('错误信息').catch( () => \\{错误处理逻辑\\})
   推荐使用第二种方式，更加清晰好读，并且可以捕获前面所有的错误（可以捕获N个then回调错误）



### catch() + then()

- 第一种情况：

  ![img](https:////upload-images.jianshu.io/upload_images/15311104-f63f673f5fbb74d1.png?imageMogr2/auto-orient/strip|imageView2/2/w/917/format/webp)

  第一种情况

  ![img](https:////upload-images.jianshu.io/upload_images/15311104-947df4320e99263b.png?imageMogr2/auto-orient/strip|imageView2/2/w/417/format/webp)

  第一种情况 - 结果

  结论：catch也会返回一个promise实例，并且是resolved状态

- 第二种情况：

  ![img](https:////upload-images.jianshu.io/upload_images/15311104-1aa27776f33dc101.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

  第二种情况

![img](https:////upload-images.jianshu.io/upload_images/15311104-a1d408c57330e14b.png?imageMogr2/auto-orient/strip|imageView2/2/w/460/format/webp)

第二种情况结果

结论：抛出错误变为rejected状态，所以绕过两个then直接跑到最下面的catch



### Promise.all() 批量执行

Promise.all([p1, p2, p3])用于将多个promise实例，包装成一个新的Promise实例，返回的实例就是普通的promise
 它接收一个数组作为参数
 数组里可以是Promise对象，也可以是别的值，只有Promise会等待状态改变
 当所有的子Promise都完成，该Promise完成，返回值是全部值得数组
 有任何一个失败，该Promise失败，返回值是第一个失败的子Promise结果

```jsx
//切菜
    function cutUp()\\{
        console.log('开始切菜。');
        var p = new Promise(function(resolve, reject)\\{        //做一些异步操作
            setTimeout(function()\\{
                console.log('切菜完毕！');
                resolve('切好的菜');
            \\}, 1000);
        \\});
        return p;
    \\}

    //烧水
    function boil()\\{
        console.log('开始烧水。');
        var p = new Promise(function(resolve, reject)\\{        //做一些异步操作
            setTimeout(function()\\{
                console.log('烧水完毕！');
                resolve('烧好的水');
            \\}, 1000);
        \\});
        return p;
    \\}

    Promise.all([cutUp(), boil()])
        .then((result) => \\{
            console.log('准备工作完毕');
            console.log(result);
        \\})
```

##### Promise.race() 类似于Promise.all() ，区别在于它有任意一个完成就算完成

```jsx
let p1 = new Promise(resolve => \\{
        setTimeout(() => \\{
            resolve('I\`m p1 ')
        \\}, 1000)
    \\});
    let p2 = new Promise(resolve => \\{
        setTimeout(() => \\{
            resolve('I\`m p2 ')
        \\}, 2000)
    \\});
    Promise.race([p1, p2])
        .then(value => \\{
            console.log(value)
        \\})
```

- 常见用法：
   异步操作和定时器放在一起，，如果定时器先触发，就认为超时，告知用户；
   例如我们要从远程的服务家在资源如果5000ms还没有加载过来我们就告知用户加载失败
- 现实中的用法
   回调包装成Promise，他有两个显而易见的好处：
   1、可读性好
   2、返回 的结果可以加入任何Promise队列

> 实战示例，回调地狱和promise对比：

```jsx
/***
   第一步：找到北京的id
   第二步：根据北京的id -> 找到北京公司的id
   第三步：根据北京公司的id -> 找到北京公司的详情
   目的：模拟链式调用、回调地狱
 ***/
 
 // 回调地狱
 // 请求第一个API: 地址在北京的公司的id
 $.ajax(\\{
   url: 'https://www.easy-mock.com/mock/5a52256ad408383e0e3868d7/lagou/city',
   success (resCity) \\{
     let findCityId = resCity.filter(item => \\{
       if (item.id == 'c1') \\{
         return item
       \\}
     \\})[0].id
     
     $.ajax(\\{
       //  请求第二个API: 根据上一个返回的在北京公司的id “findCityId”，找到北京公司的第一家公司的id
       url: 'https://www.easy-mock.com/mock/5a52256ad408383e0e3868d7/lagou/position-list',
       success (resPosition) \\{
         let findPostionId = resPosition.filter(item => \\{
           if(item.cityId == findCityId) \\{
             return item
           \\}
         \\})[0].id
         // 请求第三个API: 根据上一个API的id(findPostionId)找到具体公司，然后返回公司详情
         $.ajax(\\{
           url: 'https://www.easy-mock.com/mock/5a52256ad408383e0e3868d7/lagou/company',
           success (resCom) \\{
             let comInfo = resCom.filter(item => \\{
               if (findPostionId == item.id) \\{
                 return item
               \\}
             \\})[0]
             console.log(comInfo)
           \\}
         \\})
       \\}
     \\})
   \\}
 \\})
```



```jsx
// Promise 写法
  // 第一步：获取城市列表
  const cityList = new Promise((resolve, reject) => \\{
    $.ajax(\\{
      url: 'https://www.easy-mock.com/mock/5a52256ad408383e0e3868d7/lagou/city',
      success (res) \\{
        resolve(res)
      \\}
    \\})
  \\})

  // 第二步：找到城市是北京的id
    cityList.then(res => \\{
      let findCityId = res.filter(item => \\{
        if (item.id == 'c1') \\{
          return item
        \\}
      \\})[0].id
      
      findCompanyId().then(res => \\{
        // 第三步（2）：根据北京的id -> 找到北京公司的id
        let findPostionId = res.filter(item => \\{
            if(item.cityId == findCityId) \\{
              return item
            \\}
        \\})[0].id

        // 第四步（2）：传入公司的id
        companyInfo(findPostionId)

      \\})

    \\})

  // 第三步（1）：根据北京的id -> 找到北京公司的id
  function findCompanyId () \\{
    let aaa = new Promise((resolve, reject) => \\{
      $.ajax(\\{
        url: 'https://www.easy-mock.com/mock/5a52256ad408383e0e3868d7/lagou/position-list',
        success (res) \\{
          resolve(res)
        \\}
      \\})
    \\})
    return aaa
  \\}

// 第四步：根据上一个API的id(findPostionId)找到具体公司，然后返回公司详情
function companyInfo (id) \\{
  let companyList = new Promise((resolve, reject) => \\{
    $.ajax(\\{
      url: 'https://www.easy-mock.com/mock/5a52256ad408383e0e3868d7/lagou/company',
      success (res) \\{
        let comInfo = res.filter(item => \\{
            if (id == item.id) \\{
               return item
            \\}
        \\})[0]
        console.log(comInfo)
      \\}
    \\})
  \\})
\\}
```

原文链接：https://www.jianshu.com/p/1b63a13c2701

