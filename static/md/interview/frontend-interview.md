---
title: 前端面试
date: 2024-03-29 01:25:00
categories: 
- 前端面试
tags:
- JavaScript
- DOM
- BOM
- 事件循环
---

### new操作符具体干了什么呢?

- 创建一个空对象，并且 this 变量引用该对象，同时还继承了该函数的原型。
- 属性和方法被加入到 this 引用的对象中。
- 新创建的对象由 this 所引用，并且最后隐式的返回 this

```
var obj  = \\{\\};
obj.__proto__ = Base.prototype;
Base.call(obj);
```



### new操作符具体干了什么呢?

```
function Test()\\{\\}
const test = new Test()
```

1. 创建一个**新的空对象实例**。

```
const obj = \\{\\}
```

2. 设置新对象的 constructor 属性为构造函数的名称，设置新对象的**proto**属性指向构造函数的 prototype 对象（设置原型链）

```
obj.constructor = Test
obj.__proto__ = Test.prototype
```

3. 使用新对象调用函数，函数中的 this 被指向新实例对象（执行构造函数，传入相应的参数，如果没有参数就不用传；让 Func 中的 this 指向 obj，并执行 Func 的函数体）

```
Test.call(obj)
```

4. 将初始化完毕的新对象地址，保存到等号左边的变量中。判断 Func 的返回值类型： 如果无返回值或者返回一个非对象值，则就将步骤（1）创建的对象返回；如果返回值是一个新对象的话那么直接直接返回该对象。



### new操作符

```js
function Father()\\{
  this.lastName="老王";
  this.work=function(num)\\{
    console.log('军人');
    console.log(num);
    return '999'
  \\}
\\}
// let obj= new Father();
// 相当于 new 做了下面的三件事
let obj=\\{\\};
obj.__proto__=Father.prototype;
Father.call(obj)  // 继承的同时，将this指向obj  谁继承this指向谁
console.log(obj);
```

1.创建了一个空对象obj

2.将这个空对象__proto__指向构造函数的prototype

3.将构造函数的this指针替换成obj，然后在调用构造函数，于是obj对象就拥有了构造函数上的属性和方法



### 模拟new

new操作符做了这些事：

- 它创建了一个全新的对象
- 它会被执行[[Prototype]]（也就是**proto**）链接
- 它使this指向新创建的对象
- 通过new创建的每个对象将最终被[[Prototype]]链接到这个函数的prototype对象上
- 如果函数没有返回对象类型Object(包含Functoin, Array, Date, RegExg, Error)，那么new表达式中的函数调用将返回该对象引用

```
// objectFactory(name, 'cxk', '18')
function objectFactory() \\{
  const obj = new Object();
  const Constructor = [].shift.call(arguments);

  obj.__proto__ = Constructor.prototype;

  const ret = Constructor.apply(obj, arguments);

  return typeof ret === "object" ? ret : obj;
\\}
```







### call/apply/bind 的区别

1. 三者都可用于显示绑定 `this`;

2. `call/apply` 的区别方式在于参数传递方式的不同；

   `fn.call(obj, arg1, arg2, ...)`， **传参数列表**，以逗号隔开；作为 call 的参数传入（从第二个参数开始）。

   `fn.apply(obj, [arg1, arg2, ...])`， **传参数数组**；将多个参数组合成为一个数组传入。

3. `bind` 返回的是一个**待执行函数**，是函数柯里化的应用；而 `call/apply` 则是**立即执行函数**；

对于 apply 和 call 两者在作用上是相同的，即是**调用一个对象的一个方法，以另一个对象替换当前对象**。

将一个函数的对象上下文从初始的上下文改变为由 thisObj 指定的新对象。



### call() 和 apply() 的含义和区别？

#### 含义：

- call：调用一个对象的一个方法，用另一个对象替换当前对象。

  例如：B.call(A, args1,args2);即 A 对象调用 B 对象的方法。

- apply：调用一个对象的一个方法，用另一个对象替换当前对象。

  例如：B.apply(A, arguments);即 A 对象应用 B 对象的方法。

#### 相同点：

- 方法的含义是一样的，即方法功能是一样的；
- 第一个参数的作用是一样的；

#### 不同点：

两者传入的列表形式不一样

- call 可以传入多个参数；
- apply 只能传入两个参数，所以其第二个参数往往是作为数组形式传入



### call 与 apply 区别

第二个参数的类型不同

解析：

call 和 apply 的作用，完全一样，唯一的区别就是在参数上面。

call 接收的参数不固定，第一个参数是函数体内 this 的指向，第二个参数以下是依次传入的参数。

apply 接收两个参数，第一个参数也是函数体内 this 的指向。第二个参数是一个集合对象（数组或者类数组）



### this 和 apply 的应用

比如求数组的最大值 Math.max.apply(this, 数组)

```js
var numbers = [5, 458, 120, -215];
var maxInNumbers = Math.max.apply(this, numbers); //第一个参数也可以填Math或null
console.log(maxInNumbers); // 458
var maxInNumbers = Math.max.call(this, 5, 458, 120, -215);
console.log(maxInNumbers); // 458
```



### bind、call、apply 的区别

call 和 apply 其实是一样的，区别就在于传参时参数是一个一个传或者是以一个数组的方式来传。
call 和 apply 都是在调用时生效，改变调用者的 this 指向。

```
let name = 'Jack'
const obj = \\{name: 'Tom'\\}
function sayHi() \\{console.log('Hi! ' + this.name)\\}

sayHi() // Hi! Jack
sayHi.call(obj) // Hi! Tom

```

bind 也是改变 this 指向，不过不是在调用时生效，而是返回一个新函数。

```
const newFunc = sayHi.bind(obj)
newFunc() // Hi! Tom
```



### call，apply，bind 三者用法和区别

参数、绑定规则（显示绑定和强绑定），运行效率（最终都会转换成一个一个的参数去运行）、运行情况（`call`，`apply` 立即执行，`bind` 是`return` 出一个 `this` “固定”的函数，这也是为什么 `bind` 是强绑定的一个原因）

> 注：“固定”这个词的含义，它指的固定是指只要传进去了 `context`，则 `bind` 中 `return` 出来的函数 `this` 便一直指向 `context`，除非 `context` 是个变量



### .call() 和 .apply() 的区别？

- 例子中用 add 来替换 sub，add.call(sub,3,1) == add(3,1) ，所以运行结果为：alert(4);
- 注意：js 中的函数其实是对象，函数名是对 Function 对象的引用。

```
function add(a,b)
\\{
    alert(a+b);
\\}

function sub(a,b)
\\{
    alert(a-b);
\\}

add.call(sub,3,1);
```



### .call() 和 .apply() 的区别和作用？

作用：动态改变某个类的某个方法的运行环境。
区别参见：[JavaScript学习总结（四）function函数部分](http://segmentfault.com/blog/trigkit4/1190000000660786#articleHeader15)







### js 的事件循环eventloop是什么？

事件循环是一个单线程循环，用于监视调用堆栈并检查是否有工作即将在任务队列中完成。

如果调用堆栈为空并且任务队列中有回调函数，则将回调函数出队并推送到调用堆栈中执行。

- 所有同步任务都在主线程上执行，形成一个执行栈

- 当主线程中的执行栈为空时，检查事件队列是否为空，如果为空，则继续检查；如不为空，则执行3

- 取出任务队列的首部，加入执行栈

- 执行任务

- 检查执行栈，如果执行栈为空，则跳回第 2 步；如不为空，则继续检查

相关知识点：

事件队列是一个存储着待执行任务的队列，其中的任务严格按照时间先后顺序执行，排在队头的任务将会率先执行，而排在队尾的任务会最后执行。事件队列每次仅执行一个任务，在该任务执行完毕之后，再执行下一个任务。执行栈则是一个类似于函数调用栈的运行容器，当执行栈为空时，JS 引擎便检查事件队列，如果不为空的话，事件队列便将第一个任务压入执行栈中运行。

回答：

因为 js 是单线程运行的，在代码执行的时候，通过将不同函数的执行上下文压入执行栈中来保证代码的有序执行。在执行同步代码的时候，如果遇到了异步事件，js 引擎并不会一直等待其返回结果，而是会将这个事件挂起，继续执行执行栈中的其他任务。

当异步事件执行完毕后，再将异步事件对应的回调加入到与当前执行栈中不同的另一个任务队列中等待执行。任务队列可以分为宏任务对列和微任务对列，当当前执行栈中的事件执行完毕后，js 引擎首先会判断微任务对列中是否有任务可以执行，如果有就将微任务队首的事件压入栈中执行。

当微任务对列中的任务都执行完成后再去判断宏任务对列中的任务。

#### 微任务（microtask）

promise 的回调、node 中的 process.nextTick 、对 Dom 变化监听的 MutationObserver

- process.nextTick
- promise
- Object.observe （已废弃）
- MutationObserver

#### 宏任务（macrotask）

script 脚本的执行、setTimeout ，setInterval ，setImmediate 一类的定时事件，还有如 I/O 操作、UI 渲染等

- script
- setTimeout
- setInterval
- setImmediate
- I/O
- UI rendering

#### 执行顺序

1. 执行同步代码，这属于宏任务
2. 执行栈为空，查询是否有微任务需要执行
3. 必要的话渲染 UI
4. 然后开始下一轮 Event loop，执行宏任务中的异步代码

同步和异步任务分别进入不同的执行"场所"，同步的进入主线程，异步的进入 Event Table 并注册函数。

当指定的事情完成时，Event Table 会将这个函数移入 Event Queue。

主线程内的任务执行完毕为空，会去 Event Queue 读取对应的函数，进入主线程执行。 

上述过程会不断重复，也就是常说的 Event Loop(事件循环)。

```javascript
let data = [];
$.ajax(\\{
  url: www.javascript.com,
  data: data,
  success: () => \\{
    console.log("发送成功!");
  \\}
\\});
console.log("代码执行结束");

// ajax进入Event Table，注册回调函数success。
// 执行console.log('代码执行结束')。
// ajax事件完成，回调函数success进入Event Queue。
// 主线程从Event Queue读取回调函数success并执行。
```

详细资料可以参考：

[《这一次，彻底弄懂 JavaScript 执行机制》](https://juejin.im/post/59e85eebf265da430d571f89)

[《浏览器事件循环机制（event loop）》](https://juejin.im/post/5afbc62151882542af04112d)

[《详解 JavaScript 中的 Event Loop（事件循环）机制》](https://zhuanlan.zhihu.com/p/33058983)

[《什么是 Event Loop？》](http://www.ruanyifeng.com/blog/2013/10/event_loop.html)

 





### 回流（reflow）和重绘（repaint）

> 传送门 [DOM 操作成本到底高在哪儿？](https://segmentfault.com/a/1190000014070240?utm_source=feed-content)

**reflow(回流)**: 根据 Render Tree 布局(几何属性)，意味着元素的内容、结构、位置或尺寸发生了变化，需要重新计算样式和渲染树；

**repaint(重绘)**: 意味着元素发生的改变只影响了节点的一些样式（背景色，边框颜色，文字颜色等），只需要应用新样式绘制这个元素就可以了；

reflow 回流的成本开销要高于 repaint 重绘，一个节点的回流往往回导致子节点以及同级节点的回流；

#### 引起 reflow 回流

1. 页面第一次渲染（初始化）
2. DOM 树变化（如：增删节点）
3. Render 树变化（如：padding 改变）
4. 浏览器窗口 resize
5. 获取元素的某些属性：
6. 浏览器为了获得正确的值也会提前触发回流，这样就使得浏览器的优化失效了，这些属性包括 offsetLeft、offsetTop、offsetWidth、offsetHeight、 scrollTop/Left/Width/Height、clientTop/Left/Width/Height、调用了 getComputedStyle()或者 IE 的 currentStyle

#### 引起 repaint 重绘

1. reflow 回流必定引起 repaint 重绘，重绘可以单独触发
2. 背景色、颜色、字体改变（注意：字体大小发生变化时，会触发回流）

#### 优化方式

1. 避免逐个修改节点样式，尽量一次性修改
2. 使用 DocumentFragment 将需要多次修改的 DOM 元素缓存，最后一次性 append 到真实 DOM 中渲染
3. 可以将需要多次修改的 DOM 元素设置 display: none，操作完再显示。（因为隐藏元素不在 render 树内，因此修改隐藏元素不会触发回流重绘）
4. 避免多次读取某些属性（见上）
5. 将复杂的节点元素脱离文档流，降低回流成本

**为什么一再强调将 css 放在头部，将 js 文件放在尾部** + DOMContentLoaded 和 load 

DOMContentLoaded 事件触发时，仅当 DOM 加载完成，不包括样式表，图片... 

load 事件触发时，页面上所有的 DOM，样式表，脚本，图片都已加载完成 + CSS 资源阻塞渲染 

1. 构建 Render 树需要 DOM 和 CSSOM，所以 HTML 和 CSS 都会阻塞渲染。所以需要让 CSS 尽早加载（如：放在头部），以缩短首次渲染的时间。 + JS 资源 1. 阻塞浏览器的解析，也就是说发现一个外链脚本时，需等待脚本下载完成并执行后才会继续解析 HTML - 这和之前文章提到的浏览器线程有关，浏览器中 js 引擎线程和渲染线程是互斥的，详见[《从 setTimeout-setInterval 看 JS 线程》](https://segmentfault.com/a/1190000013702430#articleHeader2) 
2. 普通的脚本会阻塞浏览器解析，加上 defer 或 async 属性，脚本就变成异步，可等到解析完毕再执行 - async 异步执行，异步下载完毕后就会执行，不确保执行顺序，一定在 onload 前，但不确定在 DOMContentLoaded 事件的前后 - defer 延迟执行，相对于放在 body 最后（理论上在 DOMContentLoaded 事件前）



### 如何最小化重绘(repaint)和回流(reflow)？

- 尽量避免用table布局（table元素一旦触发回流就会导致table里所有的其它元素回流，造成整个 table 的重新布局）
- `CSS` 选择符从右往左匹配查找，避免 `DOM` 深度过深
- 避免使用css表达式(expression)，因为每次调用都会重新计算值（包括加载页面）
- 尽量使用 css 属性简写，如：用 border 代替 border-width, border-style, border-color
- 批量修改元素样式：elem.className 和 elem.style.cssText 代替 elem.style.xxx

- 使用 `translate` 替代 `top`
- 使用 `visibility` 替换` display: none` ，因为前者只会引起重绘，后者会引发回流（改变了布局）
- 需要要对元素进行复杂的操作时，可以先隐藏(display:"none")，操作完成后再显示
- 动画实现的速度的选择，动画速度越快，回流次数越多，也可以选择使用 `requestAnimationFrame`
- 将频繁运行的动画变为图层，图层能够阻止该节点回流影响别的元素。比如对于 `video `标签，浏览器会自动将该节点变为图层
- 需要创建多个DOM节点时，使用DocumentFragment创建完后一次性的加入document
- 缓存Layout属性值，如：var left = elem.offsetLeft; 这样，多次使用 left 只产生一次回流



### 重绘和回流（重排）的区别和关系？

- 重绘：当渲染树中的元素外观（如：颜色）发生改变，不影响布局时，产生重绘
- 回流：当渲染树中的元素的布局（如：尺寸、位置、隐藏/状态状态）或者几何属性发生改变时，产生重绘回流
- 注意：JS获取Layout属性值（如：offsetLeft、scrollTop、getComputedStyle等）也会引起回流。因为浏览器需要通过回流计算最新值
- 回流必将引起重绘，而重绘不一定会引起回流。
- 回流所需的成本比重绘高的多，改变深层次的节点很可能导致父节点的一系列回流。

**所以以下几个动作可能会导致性能问题**：

- 改变 window 大小
- 改变字体
- 添加或删除样式
- 文字改变
- 定位或者浮动
- 盒模型

**很多人不知道的是，重绘和回流其实和 Event loop 有关**

- 当 Event loop 执行完 `Microtasks` 后，会判断 `document` 是否需要更新。因为浏览器是 `60Hz `的刷新率，每 `16ms `才会更新一次。
- 然后判断是否有 `resize` 或者 `scroll` ，有的话会去触发事件，所以 `resize` 和 `scroll` 事件也是至少 `16ms` 才会触发一次，并且自带节流功能。
- 判断是否触发了` media query`
- 更新动画并且发送事件
- 判断是否有全屏操作事件
- 执行 `requestAnimationFrame` 回调
- 执行 `IntersectionObserver` 回调，该方法用于判断元素是否可见，可以用于懒加载上，但是兼容性不好
- 更新界面
- 以上就是一帧中可能会做的事情。如果在一帧中有空闲时间，就会去执行 `requestIdleCallback` 回调



### 重排与重绘的区别，什么情况下会触发？

#### 简述重排的概念

浏览器下载完页面中的所有组件（HTML、JavaScript、CSS、图片）之后会解析生成两个内部数据结构（DOM 树和渲染树），DOM 树表示页面结构，渲染树表示 DOM 节点如何显示。

**重排是 DOM 元素的几何属性变化，DOM 树的结构变化，渲染树需要重新计算。**

#### 简述重绘的概念

重绘是一个**元素外观的改变所触发的浏览器行为**，例如改变 visibility、outline、背景色等属性。浏览器会根据元素的新属性重新绘制，使元素呈现新的外观。由于浏览器的流布局，对渲染树的计算通常只需要遍历一次就可以完成。但 table 及其内部元素除外，它可能需要多次计算才能确定好其在渲染树中节点的属性值，比同等元素要多花两倍时间，这就是我们尽量避免使用 table 布局页面的原因之一。

#### 简述重绘和重排的关系

**重绘不会引起重排，但重排一定会引起重绘**，一个元素的重排通常会带来一系列的反应，甚至触发整个文档的重排和重绘，性能代价是高昂的。

#### 什么情况下会触发重排？

- 页面渲染初始化时；（这个无法避免）
- 浏览器窗口改变尺寸；
- 元素尺寸改变时；
- 元素位置改变时；
- 元素内容改变时；
- 添加或删除可见的 DOM 元素时。

#### 重排优化有如下五种方法

- 将多次改变样式属性的操作合并成一次操作，减少 DOM 访问。
- 如果要批量添加 DOM，可以先让元素脱离文档流，操作完后再带入文档流，这样只会触发一次重排。（fragment 元素的应用）
- 将需要多次重排的元素，position 属性设为 absolute 或 fixed，这样此元素就脱离了文档流，它的变化不会影响到其他元素。例如有动画效果的元素就最好设置为绝对定位。
- 由于 display 属性为 none 的元素不在渲染树中，对隐藏的元素操作不会引发其他元素的重排。如果要对一个元素进行复杂的操作时，可以先隐藏它，操作完成后再显示。这样只在隐藏和显示时触发两次重排。
- 在内存中多次操作节点，完成后再添加到文档中去。例如要异步获取表格数据，渲染到页面。可以先取得数据后在内存中构建整个表格的 html 片段，再一次性添加到文档中去，而不是循环添加每一行。







### 一个页面从输入URL到页面加载显示完成，这个过程中都发生了什么？（流程说的越详细越好）

> 注：这题胜在区分度高，知识点覆盖广，再不懂的人，也能答出几句，
>
> 而高手可以根据自己擅长的领域自由发挥，从URL规范、HTTP协议、DNS、CDN、数据库查询、
>
> 到浏览器流式解析、CSS规则构建、layout、paint、onload/domready、JS执行、JS API绑定等等；

详细版：

- 浏览器会开启一个线程来处理这个请求，对 URL 分析判断如果是 http 协议就按照 Web 方式来处理;
- 调用浏览器内核中的对应方法，比如 WebView 中的 loadUrl 方法;
- 通过DNS解析获取网址的IP地址，设置 UA 等信息发出第二个GET请求;
- 进行HTTP协议会话，客户端发送报头(请求报头);
- 进入到web服务器上的 Web Server，如 Apache、Tomcat、Node.JS 等服务器;
- 进入部署好的后端应用，如 PHP、Java、JavaScript、Python 等，找到对应的请求处理;
- 处理结束回馈报头，此处如果浏览器访问过，缓存上有对应资源，会与服务器最后修改时间对比，一致则返回304;
- 浏览器开始下载html文档(响应报头，状态码200)，同时使用缓存;
- 文档树建立，根据标记请求所需指定MIME类型的文件（比如css、js）,同时设置了cookie;
- 页面开始渲染DOM，JS根据DOM API操作DOM,执行事件绑定等，页面显示完成。

简洁版：

- 浏览器根据请求的URL交给DNS域名解析，找到真实IP，向服务器发起请求；
- 服务器交给后台处理完成后返回数据，浏览器接收文件（HTML、JS、CSS、图象等）；
- 浏览器对加载到的资源（HTML、JS、CSS等）进行语法解析，建立相应的内部数据结构（如HTML的DOM）；
- 载入解析到的资源文件，渲染页面，完成。







### 数组去重

#### 方案1：ES6

```
const numbers = [1, 2, 1, 1, 2, 1, 3, 4, 1 ];
const uniq = [...new Set(numbers)] // => [ 1, 2, 3, 4 ];
const uniq2 = Array.from(new Set(numbers)) // => [ 1, 2, 3, 4 ];
```

#### 方案2：filter

```
function unique (arr) \\{
     var res = arr.filter(function (item, index, array) \\{
     // array.indexOf(item) === index 说明这个元素第一次出现，后面这个item再出现他的item肯定不是index了
         return array.indexOf(item) === index; 
\\}) return res; \\}
```

#### 方案3

遍历数组，建立新数组，利用indexOf判断是否存在于新数组中，不存在则push到新数组，最后返回新数组

```
function unique(ar) \\{
    var ret = [];

    for (var i = 0, j = ar.length; i < j; i++) \\{
        if (ret.indexOf(ar[i]) === -1) \\{
            ret.push(ar[i]);
        \\}
    \\}

    return ret;
\\}
```

#### 方案4

遍历数组，利用object对象保存数组值，判断数组值是否已经保存在object中，未保存则push到新数组并用object[arrayItem]=1的方式记录保存，这个效率比方案3高

```
function unique(ar) \\{
    var tmp = \\{\\},
        ret = [];

    for (var i = 0, j = ar.length; i < j; i++) \\{
        if (!tmp[ar[i]]) \\{
            tmp[ar[i]] = 1;
            ret.push(ar[i]);
        \\}
    \\}

    return ret;
\\}
```







# 中高级前端面试必知必会

## Chrome 浏览器进程

> 在资源不足的设备上，将服务合并到浏览器进程中

### 浏览器主进程

- 负责浏览器界面显示
- 各个页面的管理，创建以及销毁
- 将渲染进程的结果绘制到用户界面上
- 网络资源管理

### GPU 进程

- 用于 3D 渲染绘制

### 网络进程

- 发起网络请求

### 插件进程

- 第三方插件处理，运行在沙箱中

### 渲染进程

- 页面渲染
- 脚本执行
- 事件处理



## 网络传输流程

### 生成 HTTP 请求消息

1. 输入网址

2. 浏览浏览器解析 URL

3. 生成 HTTP 请求信息

   ![img](https://mmbiz.qpic.cn/mmbiz_png/y0rsINPrlZwiaiaDhnq7zdoCEsbMhMzSk7u6oElshWJ46iaORk0ShuVEZr0QNT2KbbYBdUzrD5PdSpFllUWKwW7DA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

   ![img](https://mmbiz.qpic.cn/mmbiz_png/y0rsINPrlZwiaiaDhnq7zdoCEsbMhMzSk7Flia7qJfMgWFypTBQO4wSwJvkRgIXicn9sujJ3JGqXgunNBJoEQibBuWQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

4. 收到响应

   | 状态码 | 含义                     |
   | :----- | :----------------------- |
   | 1xx    | 告知请求的处理进度和情况 |
   | 2xx    | 成功                     |
   | 3xx    | 表示需要进一步操作       |
   | 4xx    | 客户端错误               |
   | 5xx    | 服务端错误               |

### 向 DNS 服务器查询 Web 服务器的 IP 地址

1. Socket 库提供查询 IP 地址的功能
2. 通过解析器向 DNS 服务器发出查询

### 全世界 DNS 服务器的大接力

1. 寻找相应的 DNS 服务器并获取 IP 地址
2. 通过缓存加快 DNS 服务器的响应

### 委托协议栈发送消息

> 协议栈通过 TCP 协议收发数据的操作。

1. 创建套接字

![img](https://mmbiz.qpic.cn/mmbiz_png/y0rsINPrlZwiaiaDhnq7zdoCEsbMhMzSk7A1rqCUkoCoD5GOukw4ETP2lQicMxKibgHLKaFbqzeAjRFV2o40phPhGQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

- 浏览器，邮件等一般的应用程序收发数据时用 TCP
- DNS 查询等收发较短的控制数据时用 UDP

1. 连接服务器

> 浏览器调用 Socket.connect

- 在 TCP 模块处创建表示连接控制信息的头部
- 通过 TCP 头部中的发送方和接收方端口号找到要连接的套接字

![img](https://mmbiz.qpic.cn/mmbiz_png/y0rsINPrlZwiaiaDhnq7zdoCEsbMhMzSk7GwcQ5QiaFLjibTicleT7Izkc9WGFYzUvwkbFRZpDGV5oH9sTSNo61icibyw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

1. 收发数据

> 浏览器调用 Socket.write

- 将 HTTP 请求消息交给协议栈

- 对较大的数据进行拆分，拆分的每一块数据加上 TCP 头，由 IP 模块来发送

- 使用 ACK 号确认网络包已收到

- 根据网络包平均往返时间调整 ACK 号等待时间

- 使用窗口有效管理 ACK 号

  ![img](https://mmbiz.qpic.cn/mmbiz_png/y0rsINPrlZwiaiaDhnq7zdoCEsbMhMzSk7vGw4vghYWZjFlCviaJKpibPyFPLJbcNTYD5WdDmznibJ3x81VtPxuNMjw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

- ACK 与窗口的合并

- 接收 HTTP 响应消息

1. 断开管道并删除套接字

> 浏览器调用 Socket.close

- 数据发送完毕后断开连接

  ![img](https://mmbiz.qpic.cn/mmbiz_png/y0rsINPrlZwiaiaDhnq7zdoCEsbMhMzSk7zcLBK07icxeYSXyCgW9AhBBokALyPNy0qwpxcDg7PqsxMHPjBEYKeMA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

- 删除套接字

- 1. 客户端发送 FIN
  2. 服务端返回 ACK 号
  3. 服务端发送 FIN
  4. 客户端返回 ACK 号

![img](https://mmbiz.qpic.cn/mmbiz_png/y0rsINPrlZwiaiaDhnq7zdoCEsbMhMzSk7HkgGQnMsoLM1CJrL1BK4Iycqb4y9DBlxWmVs9AiaHw1qmxcO9AwCgHA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

![img](https://mmbiz.qpic.cn/mmbiz_png/y0rsINPrlZwiaiaDhnq7zdoCEsbMhMzSk7d7gS9bmwv4o0tFJlQJCN8qYvDhENHGr6YnF8T2PVsL3YSrqVWtxiaKw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



## 跨域

### 同源策略

> 同源策略是一个重要的安全策略，它用于限制一个origin的文档或者它加载的脚本如何能与另一个源的资源进行交互。它能帮助阻隔恶意文档，减少可能被攻击的媒介。

如果两个 URL 的 **protocol** 、 **port** (如果有指定的话)和 **host** 都相同的话，则这两个 URL 是同源。

例如：

| URL                                               | 结果 | 原因                               |
| :------------------------------------------------ | :--- | :--------------------------------- |
| `http://store.company.com/dir2/other.html`        | 同源 | 只有路径不同                       |
| `http://store.company.com/dir/inner/another.html` | 同源 | 只有路径不同                       |
| `https://store.company.com/secure.html`           | 失败 | 协议不同                           |
| `http://store.company.com:81/dir/etc.html`        | 失败 | 端口不同 ( `http://` 默认端口是80) |
| `http://news.company.com/dir/other.html`          | 失败 | 主机不同                           |

### 主要的跨域处理

**JSONP**

JSONP的原理是：静态资源请求不受同源策略影响。实现如下：

```
const script = document.createElement('script')
script.type = 'text/javascript'
script.src = 'https://www.domain.com/a?data=1&callback=cb'
const cb = res => \\{
    console.log(JSON.stringify(res))
\\}
```

**CORS**

CORS：跨域资源共享(CORS) 是一种机制，它使用额外的 HTTP 头来告诉浏览器  让运行在一个 origin (domain) 上的Web应用被准许访问来自不同源服务器上的指定的资源。

在各种服务端代码实现如下：

```
// 根据不同语言规则，具体语法有所不同，此处以NodeJs的express为例
//设置跨域访问  
app.all('*', function(req, res, next) \\{  
    res.header("Access-Control-Allow-Origin", "*");  
    res.header("Access-Control-Allow-Headers", "X-Requested-With");  
    res.header("Access-Control-Allow-Methods","PUT,POST,GET,DELETE,OPTIONS");
    next();  
\\});   
```

Nginx实现如下：

```
server \\{
    ...
    
    add_header Access-Control-Allow-Credentials true;
    add_header Access-Control-Allow-Origin $http_origin;
    
        
    location /file \\{
        if ($request_method = 'OPTIONS') \\{
            add_header Access-Control-Allow-Origin $http_origin;
            add_header Access-Control-Allow-Methods $http_access_control_request_method;
            add_header Access-Control-Allow-Credentials true;
            add_header Access-Control-Allow-Headers $http_access_control_request_headers;
            add_header Access-Control-Max-Age 1728000;
            return 204;
        \\}         
    \\}
	
    ...
\\}
```



## 网络协议

![img](https://mmbiz.qpic.cn/mmbiz_png/y0rsINPrlZwiaiaDhnq7zdoCEsbMhMzSk73M6kkzgomFeGIlkj7nibFl8jL1KicOE9a4u46pyQokeMibJVRRnwH3Lrg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

### TCP

传输控制协议（TCP，Transmission Control Protocol）是一种面向连接的、可靠的、基于字节流的传输层通信协议，由 IETF 的 RFC 793 定义。

- 基于流的方式
- 面向连接
- 丢包重传
- 保证数据顺序

### UDP

Internet 协议集支持一个无连接的传输协议，该协议称为用户数据报协议（UDP，User Datagram Protocol）。UDP 为应用程序提供了一种无需建立连接就可以发送封装的 IP 数据包的方法。RFC 768 描述了 UDP。

- UDP 是非连接的协议，也就是不会跟终端建立连接
- UDP 包信息只有 8 个字节
- UDP 是面向报文的。既不拆分，也不合并，而是保留这些报文的边界
- UDP 可能丢包
- UDP 不保证数据顺序

### HTTP

- HTTP/0.9：GET，无状态的特点形成

- HTTP/1.0：支持 POST，HEAD，添加了请求头和响应头，支持任何格式的文件发送，添加了状态码、多字符集支持、多部分发送、权限、缓存、内容编码等

- HTTP/1.1：默认长连接，同时 6 个 TCP 连接，CDN 域名分片

- HTTPS：HTTP + TLS（ **非对称加密** 与 **对称加密** ）

- 1. 客户端发出 https 请求，请求服务端建立 SSL 连接
  2. 服务端收到 https 请求，申请或自制数字证书，得到公钥和服务端私钥，并将公钥发送给客户端
  3. 户端验证公钥，不通过验证则发出警告，通过验证则产生一个随机的客户端私钥
  4. 客户端将公钥与客户端私钥进行对称加密后传给服务端
  5. 服务端收到加密内容后，通过服务端私钥进行非对称解密，得到客户端私钥
  6. 服务端将客户端私钥和内容进行对称加密，并将加密内容发送给客户端
  7. 客户端收到加密内容后，通过客户端私钥进行对称解密，得到内容

- HTTP/2.0：多路复用（一次 TCP 连接可以处理多个请求），服务器主动推送，stream 传输。

- HTTP/3：基于 UDP 实现了 QUIC 协议

- - 建立好 HTTP2 连接
  - 发送 HTTP2 扩展帧
  - 使用 QUIC 建立连接
  - 如果成功就断开 HTTP2 连接
  - 升级为 HTTP3 连接

**注：RTT = Round-trip time**



## 页面渲染流程

> 构建 DOM 树、样式计算、布局阶段、分层、绘制、分块、光栅化和合成

1. 创建 DOM tree

2. - 遍历 DOM 树中的所有可见节点，并把这些节点加到布局树中。
   - 不可见的节点会被布局树忽略掉。

3. 样式计算

4. - 创建 CSSOM tree
   - 转换样式表中的属性值
   - 计算出 DOM 节点样式

5. 生成 layout tree

6. 分层

7. - 生成图层树（LayerTree）
   - 拥有层叠上下文属性的元素会被提升为单独的一层
   - 需要剪裁（clip）的地方也会被创建为图层
   - 图层绘制

8. 将图层转换为位图

9. 合成位图并显示在页面中



## 页面更新机制

- 更新了元素的几何属性（重排）

- 更新元素的绘制属性（重绘）

- 直接合成

- - CSS3 的属性可以直接跳到这一步



## JS 执行机制

### 代码提升（为了编译）

- 变量提升
- 函数提升（优先级最高）

### 编译代码

**V8 编译 JS 代码的过程**

1. 生成抽象语法树（AST）和执行上下文

2. 第一阶段是分词（tokenize），又称为词法分析

3. 第二阶段是解析（parse），又称为语法分析

4. 生成字节码

   字节码就是介于 AST 和机器码之间的一种代码。但是与特定类型的机器码无关，字节码需要通过解释器将其转换为机器码后才能执行。

5. 执行代码

**高级语言编译器步骤：**

1. 输入源程序字符流
2. 词法分析
3. 语法分析
4. 语义分析
5. 中间代码生成
6. 机器无关代码优化
7. 代码生成
8. 机器相关代码优化
9. 目标代码生成

### 执行代码

- 执行全局代码时，创建全局上下文
- 调用函数时，创建函数上下文
- 使用 eval 函数时，创建 eval 上下文
- 执行局部代码时，创建局部上下文



## 类型

### 基本类型

- Undefined
- Null
- Boolean
- String
- Symbol
- Number
- Object
- BigInt

### 复杂类型

- Object



## 隐式转换规则

### 基本情况

- 转换为布尔值
- 转换为数字
- 转换为字符串

### 转换为原始类型

对象在转换类型的时候，会执行原生方法 **ToPrimitive** 。

其算法如下：

1. 如果已经是 **原始类型**，则返回当前值；
2. 如果需要转 **字符串** 则先调用`toSting`方法，如果此时是 **原始类型** 则直接返回，否则再调用`valueOf`方法并返回结果；
3. 如果不是 **字符串**，则先调用`valueOf`方法，如果此时是 **原始类型** 则直接返回，否则再调用`toString`方法并返回结果；
4. 如果都没有 **原始类型** 返回，则抛出 **TypeError** 类型错误。

当然，我们可以通过重写`Symbol.toPrimitive`来制定转换规则，此方法在转原始类型时调用优先级最高。

```
const data = \\{
  valueOf() \\{
    return 1;
  \\},
  toString() \\{
    return "1";
  \\},
  [Symbol.toPrimitive]() \\{
    return 2;
  \\}
\\};
data + 1; // 3
```

### 转换为布尔值

对象转换为布尔值的规则如下表：

| 参数类型  | 结果                                                         |
| :-------- | :----------------------------------------------------------- |
| Undefined | 返回 `false`。                                               |
| Null      | 返回 `false`。                                               |
| Boolean   | 返回 当前参数。                                              |
| Number    | 如果参数为`+0`、`-0`或`NaN`，则返回 `false`；其他情况则返回 `true`。 |
| String    | 如果参数为空字符串，则返回 `false`；否则返回 `true`。        |
| Symbol    | 返回 `true`。                                                |
| Object    | 返回 `true`。                                                |

### 转换为数字

对象转换为数字的规则如下表：

| 参数类型  | 结果                                                         |
| :-------- | :----------------------------------------------------------- |
| Undefined | 返回 `NaN`。                                                 |
| Null      | Return +0.                                                   |
| Boolean   | 如果参数为 `true`，则返回 `1`；`false`则返回 `+0`。          |
| Number    | 返回当前参数。                                               |
| String    | 先调用 **ToPrimitive** ，再调用 **ToNumber** ，然后返回结果。 |
| Symbol    | 抛出 `TypeError`错误。                                       |
| Object    | 先调用 **ToPrimitive** ，再调用 **ToNumber** ，然后返回结果。 |

### 转换为字符串

对象转换为字符串的规则如下表：

| 参数类型  | 结果                                                         |
| :-------- | :----------------------------------------------------------- |
| Undefined | 返回 `"undefined"`。                                         |
| Null      | 返回 `"null"`。                                              |
| Boolean   | 如果参数为 `true` ,则返回 `"true"`；否则返回 `"false"`。     |
| Number    | 调用 **NumberToString** ，然后返回结果。                     |
| String    | 返回 当前参数。                                              |
| Symbol    | 抛出 `TypeError`错误。                                       |
| Object    | 先调用 **ToPrimitive** ，再调用 **ToString** ，然后返回结果。 |



## this

this 是和执行上下文绑定的。

**执行上下文：**

- 全局执行上下文：全局执行上下文中的 this 也是指向 window 对象。
- 函数执行上下文：使用对象来调用其内部的一个方法，该方法的 this 是指向对象本身的。
- eval 执行上下文：执行 eval 环境内部的上两个情况。

根据优先级最高的来决定 `this` 最终指向哪里。

首先，`new` 的方式优先级最高，接下来是 `bind` 这些函数，然后是 `obj.foo()` 这种调用方式，最后是 `foo` 这种调用方式，同时，箭头函数的 `this` 一旦被绑定，就不会再被任何方式所改变。

三点注意：

1. 当函数作为对象的方法调用时，函数中的 this 就是该对象；
2. 当函数被正常调用时，在严格模式下，this 值是 undefined，非严格模式下 this 指向的是全局对象 window；
3. 嵌套函数中的 this 不会继承外层函数的 this 值。
4. 我们还提了一下箭头函数，因为箭头函数没有自己的执行上下文，所以箭头函数的 this 就是它外层函数的 this。



## 闭包

**没有被引用的闭包会被自动回收，但还存在全局变量中，则依然会内存泄漏。**

在 JavaScript 中，根据词法作用域的规则，内部函数总是可以访问其外部函数中声明的变量，当通过调用一个外部函数返回一个内部函数后，即使该外部函数已经执行结束了，但是内部函数引用外部函数的变量依然保存在内存中，我们就把这些变量的集合称为闭包。比如外部函数是 foo，那么这些变量的集合就称为 foo 函数的闭包。

```
var getNum;
function getCounter() \\{
  var n = 1;
  var inner = function() \\{
    n++;return n;
  \\};
  return inner;
\\}
getNum = getCounter();
getNum(); // 2
getNum(); // 3
getNum(); // 4
getNum(); // 5
```



## 作用域

### 全局作用域

对象在代码中的任何地方都能访问，其生命周期伴随着页面的生命周期。

### 函数作用域

函数内部定义的变量或者函数，并且定义的变量或者函数只能在函数内部被访问。函数执行结束之后，函数内部定义的变量会被销毁。

### 局部作用域

使用一对大括号包裹的一段代码，比如函数、判断语句、循环语句，甚至单独的一个\\{\\}都可以被看作是一个块级作用域。



## 作用域链

### 词法作用域

词法作用域就是指作用域是由代码中函数声明的位置来决定的，所以词法作用域是静态的作用域，通过它就能够预测代码在执行过程中如何查找标识符。

词法作用域是代码阶段就决定好的，和函数是怎么调用的没有关系。

## 原型&原型链

其实每个 JS 对象都有 `__proto__` 属性，这个属性指向了原型。

原型也是一个对象，并且这个对象中包含了很多函数，对于 `obj` 来说，可以通过 `__proto__` 找到一个原型对象，在该对象中定义了很多函数让我们来使用。

原型链：

- `Object` 是所有对象的爸爸，所有对象都可以通过 `__proto__` 找到它
- `Function` 是所有函数的爸爸，所有函数都可以通过 `__proto__` 找到它
- 函数的 `prototype` 是一个对象
- 对象的 `__proto__` 属性指向原型， `__proto__` 将对象和原型连接起来组成了原型链



## V8 工作原理

### 数据存储

- 栈空间：先进后出的数据结构，调用栈，存储执行上下文，以及存储原始类型的数据。
- 堆空间：用数组实现的二叉树，存储引用类型。堆空间很大，能存放很多大的数据。存放在堆内存中的对象，变量实际保存的是一个指针，这个指针指向另一个位置。

原始类型的赋值会完整复制变量值，而引用类型的赋值是复制引用地址。

### 垃圾回收

- 回收调用栈内的数据：执行上下文结束且没有被引用时，则会通过向下移动 **记录当前执行状态的指针（称为 ESP）** 来销毁该函数保存在栈中的执行上下文。

- 回收堆里的数据：

  > V8 中会把堆分为新生代和老生代两个区域，
  >
  > 新生代中存放的是生存时间短的对象，
  >
  > 老生代中存放的生存时间久的对象。
  >
  > 垃圾回收重要术语：

- - 大部分对象在内存中存在的时间很短
  - 不死的对象，会活得更久
  - 代际假说
  - 分代收集

**副垃圾回收器：**

主要负责新生代的垃圾回收。

这个区域不大，但是垃圾回收比较频繁。

新生代的垃圾回收算法是 Scavenge 算法。

主要把新生代空间对半划分为两个区域：对象区域，空闲区域。

当对象区域快被写满时，则会进行一次垃圾清理。

流程如下：

1. 对对象区域中的垃圾做标记
2. 把存活的对象复制到空闲区域中
3. 把这些对象有序地排列起来
4. 清理完之后，对象区域会与空闲区域互换

**主垃圾回收器：**

主垃圾回收器主要负责老生区中的垃圾回收。

除了新生区中晋升的对象，一些大的对象会直接被分配到老生区。

因此老生区中的对象有两个特点，一个是对象占用空间大，另一个是对象存活时间长。

流程如下：

1. 从一组根元素开始，递归遍历这组根元素，在这个遍历过程中，区分活动对象以及垃圾数据
2. 标记过程和清除过程使用标记 - 清除算法
3. 碎片过多会导致大对象无法分配到足够的连续内存时，会使用标记 - 整理算法

一旦执行垃圾回收算法，会导致 **全停顿（Stop-The-World）** 。

但是 V8 有 **增量标记算法** 。

V8 将标记过程分为一个个的子标记过程，同时让垃圾回收标记和 JavaScript 应用逻辑交替进行，直到标记阶段完成。



## 浏览器安全

### 攻击方式

- xss：将代码注入到网页

- - **持久型** ：写入数据库
  - **非持久型** ：修改用户代码

- csrf：跨站请求伪造。攻击者会虚构一个后端请求地址，诱导用户通过某些途径发送请求。

- 中间人攻击：中间人攻击是攻击方同时与服务端和客户端建立起了连接，并让对方认为连接是安全的，但是实际上整个通信过程都被攻击者控制了。攻击者不仅能获得双方的通信信息，还能修改通信信息。

- - DNS 欺骗：入侵 DNS 来将用户访问目标改为入侵者指定机器
  - 会话劫持：在一次正常的通信过程中，攻击者作为第三方参与到其中，或者是在数据里加入其他信息，甚至将双方的通信模式暗中改变，即从直接联系变成有攻击者参与的联系。

### 防御措施

1. 预防 XSS

- 使用转义字符过滤 html 代码

  ```
  const escapeHTML = value => \\{
    if (!value || !value.length) \\{
      return value;
    \\}
    return value
      .replace(/&/g, "&amp;")
      .replace(/</g, "&lt;")
      .replace(/>/g, "&gt;")
      .replace(/"/g, "&quot;")
      .replace(/'/g, "&#39;");
  \\};
  ```

- 过滤 SQL 代码

  ```
  const replaceSql = value => \\{
    if (!value || !value.length) \\{
      return value;
    \\}
    return value.replace(/select|update|delete|exec|count|'|"|=|;|>|<|\\%/gi, "");
  \\};
  ```

1. 预防 CSRF

2. - 验证 HTTP Referer 字段
   - 在请求地址中添加 token 并验证
   - 在 HTTP 头中自定义属性并验证
   - Get 请求不对数据进行修改
   - 接口防跨域处理
   - 不让第三方网站访问用户 cookie

3. 预防中间人攻击

- 对于 DNS 欺骗：检查本机的 HOSTS 文件
- 对于会话劫持：使用交换式网络代替共享式网络，还必须使用静态 ARP、捆绑 MAC+IP 等方法来限制欺骗，以及采用认证方式的连接等。

1. 内容安全策略（CSP）

内容安全策略 (CSP) 是一个额外的安全层，用于检测并削弱某些特定类型的攻击，包括跨站脚本 (XSS) 和数据注入攻击等。无论是数据盗取、网站内容污染还是散发恶意软件，这些攻击都是主要的手段。

措施如下：

- HTTP Header 中的 `Content-Security-Policy`

- <meta http-equiv="Content-Security-Policy">



## 浏览器性能

### DNS 预解析

- ``
- Chrome 和 Firefox 3.5+ 能自动进行预解析
- 关闭 DNS 预解析：``

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

### 强缓存

1. Expires

2. - 缓存过期时间，用来指定资源到期的时间，是服务器端的具体的时间点。
   - Expires 是 HTTP/1 的产物，受限于本地时间，如果修改了本地时间，可能会造成缓存失效。

3. Cache-Control

   ![img](https://mmbiz.qpic.cn/mmbiz_png/y0rsINPrlZwiaiaDhnq7zdoCEsbMhMzSk7GE8dpRBNgrbVFr7O6b7DnE5qKP5oM8MT9jZxZdxJ4mibx3bLnh22cQQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

   ![img](https://mmbiz.qpic.cn/mmbiz_png/y0rsINPrlZwiaiaDhnq7zdoCEsbMhMzSk7tC27M3AegicxA83Hur6IxibvC6RNE2ZQAKPssuqcX7qe3oibyVDSicVb9Q/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

### 协商缓存

> 协商缓存就是强制缓存失效后，浏览器携带缓存标识向服务器发起请求，由服务器根据缓存标识决定是否使用缓存的过程。

- 服务器响应头：Last-Modified，Etag
- 浏览器请求头：If-Modified-Since，If-None-Match

**Last-Modified** 与 **If-Modified-Since** 配对。`Last-Modified` 把 Web 应用最后修改时间告诉客户端，客户端下次请求之时会把 `If-Modified-Since` 的值发生给服务器，服务器由此判断是否需要重新发送资源，如果不需要则返回 304，如果有则返回 200。这对组合的缺点是只能精确到秒，而且是根据本地打开时间来记录的，所以会不准确。

**Etag** 与 **If-None-Match** 配对。它们没有使用时间作为判断标准，而是使用了一组特征串。`Etag`把此特征串发生给客户端，客户端在下次请求之时会把此特征串作为`If-None-Match`的值发送给服务端，服务器由此判断是否需要重新发送资源，如果不需要则返回 304，如果有则返回 200。

![img](https://mmbiz.qpic.cn/mmbiz_png/y0rsINPrlZwiaiaDhnq7zdoCEsbMhMzSk7P5OgXNGuhlkibctNoDSs9dbp8d6Gpm0micMxe0FfMVLHxzYhyzgMDwiaQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



## NodeJs

### 单线程

基础概念：

- 进程：进程（英语：process），是指计算机中已运行的程序。进程曾经是分时系统的基本运作单位。
- 线程：线程（英语：thread）是操作系统能够进行运算调度的最小单位。大部分情况下，它被包含在进程之中，是进程中的实际运作单位。
- 协程：协程（英语：coroutine），又称微线程，是计算机程序的一类组件，推广了协作式多任务的子程序，允许执行被挂起与被恢复。

Node 中最核心的是 v8 引擎，在 Node 启动后，会创建 v8 的实例，这个实例是多线程的，各个线程如下：

- 主线程：编译、执行代码。
- 编译/优化线程：在主线程执行的时候，可以优化代码。
- 分析器线程：记录分析代码运行时间，为 Crankshaft 优化代码执行提供依据。
- 垃圾回收的几个线程。

### 非阻塞 I/O

**阻塞** 是指在 Node.js 程序中，其它 JavaScript 语句的执行，必须等待一个非 JavaScript 操作完成。这是因为当 **阻塞** 发生时，事件循环无法继续运行 JavaScript。

在 Node.js 中，JavaScript 由于执行 CPU 密集型操作，而不是等待一个非 JavaScript 操作（例如 I/O）而表现不佳，通常不被称为 **阻塞**。在 Node.js 标准库中使用 libuv 的同步方法是最常用的 **阻塞** 操作。原生模块中也有 **阻塞** 方法。

### 事件循环

```
   ┌───────────────────────────┐
┌─>│           timers          │
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │     pending callbacks     │
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │       idle, prepare       │
│  └─────────────┬─────────────┘      ┌───────────────┐
│  ┌─────────────┴─────────────┐      │   incoming:   │
│  │           poll            │<─────┤  connections, │
│  └─────────────┬─────────────┘      │   data, etc.  │
│  ┌─────────────┴─────────────┐      └───────────────┘
│  │           check           │
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
└──┤      close callbacks      │
   └───────────────────────────┘
```

**注意：每个框被称为事件循环机制的一个阶段。**

**在 Windows 和 Unix/Linux 实现之间存在细微的差异，但这对演示来说并不重要。**

阶段概述：

- **定时器** ：本阶段执行已经被 `setTimeout()` 和 `setInterval()` 的调度回调函数。
- **待定回调** ：执行延迟到下一个循环迭代的 I/O 回调。
- **idle, prepare** ：仅系统内部使用。
- **轮询** ：检索新的 I/O 事件;执行与 I/O 相关的回调（几乎所有情况下，除了关闭的回调函数，那些由计时器和 `setImmediate()` 调度的之外），其余情况 node 将在适当的时候在此阻塞。
- **检测** ：`setImmediate()` 回调函数在这里执行。
- **关闭的回调函数** ：一些关闭的回调函数，如：`socket.on('close', ...)`。

在每次运行的事件循环之间，Node.js 检查它是否在等待任何异步 I/O 或计时器，如果没有的话，则完全关闭。

**`process.nextTick()`** ：它是异步 API 的一部分。从技术上讲不是事件循环的一部分。不管事件循环的当前阶段如何，都将在当前操作完成后处理 `nextTickQueue`。这里的一个*操作*被视作为一个从底层 C/C++ 处理器开始过渡，并且处理需要执行的 JavaScript 代码。

### Libuv

Libuv 是一个跨平台的异步 IO 库，它结合了 UNIX 下的 libev 和 Windows 下的 IOCP 的特性，最早由 Node.js 的作者开发，专门为 Node.js 提供多平台下的异步 IO 支持。Libuv 本身是由 C++ 语言实现的，Node.js 中的非阻塞 IO 以及事件循环的底层机制都是由 libuv 实现的。

在 Windows 环境下，libuv 直接使用 Windows 的 IOCP 来实现异步 IO。在 非 Windows 环境下，libuv 使用多线程（线程池 Thread Pool）来模拟异步 IO，这里仅简要提一下 libuv 中有线程池的概念，之后的文章会介绍 libuv 如何实现进程间通信。



## 其它知识

### typeof vs instanceof

`instanceof` 运算符用来检测 `constructor.prototype`是否存在于参数 `object` 的原型链上。

`typeof` 操作符返回一个字符串，表示未经计算的操作数的类型。

在 JavaScript 最初的实现中，JavaScript 中的值是由一个表示类型的标签和实际数据值表示的。对象的类型标签是 0。由于 `null` 代表的是空指针（大多数平台下值为 0x00），因此，null 的类型标签是 0，`typeof null` 也因此返回 `"object"`。

### 递归

> 递归（英语：Recursion），又译为递回，在数学与计算机科学中，是指在函数的定义中使用函数自身的方法。
>
> 例如：
>
> 大雄在房里，用时光电视看着未来的情况。电视画面中的那个时候，他正在房里，用时光电视，看着未来的情况。电视画面中的电视画面的那个时候，他正在房里，用时光电视，看着未来的情况……
>
> 简单来说，就是 **无限套娃**

我们以斐波那契数列（Fibonacci sequence）为例，看看输入结果会为正无穷的值的情况下，各种递归的情况。

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

首先是普通版

```
const fib1 = n => \\{
  if (typeof n !== "number") \\{
    throw new Error("..");
  \\}
  if (n < 2) \\{
    return n;
  \\}
  return fib1(n - 1) + fib1(n - 2);
\\};
```

从上面的代码分析，我们不难发现，在`fib1`里，JS 会不停创建执行上下文，压入栈内，而且在得出结果前不会销毁，所以数大了之后容易爆栈。

![img](https://mmbiz.qpic.cn/mmbiz_png/y0rsINPrlZwiaiaDhnq7zdoCEsbMhMzSk7haf1o7jXwicKFocBQiaGVf8xaOjIdL3mWWaVSqRSdia4Lzyjq1uL30hXA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

所以我们可以对其进行优化，就是利用 **尾调用** 进行优化。

尾调用是指函数的最后一步只返回一个纯函数的调用，而没有别的数据占用引用。代码如下：

```
const fib2 = (n, a = 0, b = 1) => \\{
  if (typeof n !== "number") \\{
    throw new Error("..");
  \\}
  if (n === 0) \\{
    return a;
  \\}
  return fib2(n - 1, b, a + b);
\\};
```

不过很遗憾，在 Chrome 83.0.4103.61 里还是会爆。

![img](https://mmbiz.qpic.cn/mmbiz_png/y0rsINPrlZwiaiaDhnq7zdoCEsbMhMzSk7CTmtENaFaWpco5TfC0GM3aPAoCQycrADXNc1fJJRGVZrKJrK7MzMbw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

然后我们还有备忘录递归法，就是另外申请空间去存储每次递归的值，是个自顶向下的算法。

![img](https://mmbiz.qpic.cn/mmbiz_png/y0rsINPrlZwiaiaDhnq7zdoCEsbMhMzSk75nOibAImLu4DdExI6D8cx3GCOkJiauhcSWacNjsb0IyrrTMCOTvzXtkQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

可惜，还是挂了。

不过在一些递归问题上，我们还可以利用动态规划（Dynamic programming，简称 DP）来解决。

动态规划是算法里比较难掌握的一个概念之一，但是基本能用递归来解决的问题，都能用动态规划来解决。

动态规划背后的基本思想非常简单。大致上，若要解一个给定问题，我们需要解其不同部分（即子问题），再根据子问题的解以得出原问题的解。

跟备忘录递归刚好相反，是自底向上的算法。具体代码如下：

```
const fib3 = n => \\{
  if (typeof n !== "number") \\{
    throw new Error("..");
  \\}
  if (n < 2) \\{
    return n;
  \\}
  let a = 0;
  let b = 1;
  while (n--) \\{
    [a, b] = [b, a + b];
  \\}
  return a;
\\};

```

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

效果很好，正确输出了正无穷~

## 参考资料

1. 浏览器工作原理与实践
2. 浏览器的运行机制—2.浏览器都包含哪些进程？
3. 「中高级前端面试」JavaScript 手写代码无敌秘籍
4. JavaScript 深拷贝
5. bailnl/promise
6. 网络是怎样连接的？
7. 浏览器工作原理与实践
8. 浏览器的工作原理：新式网络浏览器幕后揭秘
9. 内容安全策略( CSP )
10. 前端面试之道
11. HTTP 各版本的区别
12. CORS解决跨域问题（Nginx跨域配置）
13. 你觉得 Node.js 是单线程这个结论对吗？
14. Node 指南
15. 深入理解浏览器的缓存机制

转自https://mp.weixin.qq.com/s/SrKdXN4FF4IThFbDxivN4A







### 说说你对[闭包](https://so.csdn.net/so/search?q=闭包&spm=1001.2101.3001.7020)的理解

使用闭包主要是为了设计私有的方法和变量。闭包的优点是可以避免[全局变量](https://so.csdn.net/so/search?q=全局变量&spm=1001.2101.3001.7020)的污染，缺点是闭包会常驻内存，会增大内存使用量，使用不当很容易造成内存泄露。

闭包有三个特性:

> 1.函数[嵌套](https://so.csdn.net/so/search?q=嵌套&spm=1001.2101.3001.7020)函数
> 2.函数内部可以引用外部的参数和变量
> 3.参数和变量不会被[垃圾回收](https://so.csdn.net/so/search?q=垃圾回收&spm=1001.2101.3001.7020)机制回收



## CSS 相关问题

### display:none和visibility:hidden的区别？

display:none  隐藏对应的元素，在文档布局中不再给它分配空间，它各边的元素会合拢，
就当他从来不存在。

visibility:hidden  隐藏对应的元素，但是在文档布局中仍保留原来的空间。



### CSS中 link 和@import 的区别是？

(1) link属于HTML标签，而@import是CSS提供的; 
(2) 页面被加载的时，link会同时被加载，而@import引用的CSS会等到页面被加载完再加载;
(3) import只在IE5以上才能识别，而link是HTML标签，无兼容问题; 
(4) link方式的样式的权重 高于@import的权重.



### position:absolute和float属性的异同

A：共同点：
对内联元素设置`float`和`absolute`属性，可以让元素脱离文档流，并且可以设置其宽高。

B：不同点：
float仍会占据位置，position会覆盖文档流中的其他元素。



### CSS 选择符有哪些？哪些属性可以继承？优先级算法如何计算？ CSS3新增伪类有那些？

```
1.id选择器（ # myid）
2.类选择器（.myclassname）
3.标签选择器（div, h1, p）
4.相邻选择器（h1 + p）
5.子选择器（ul > li）
6.后代选择器（li a）
7.通配符选择器（ * ）
8.属性选择器（a[rel = "external"]）
9.伪类选择器（a: hover, li:nth-child）
```

- 可继承的样式： font-size font-family color, text-indent;
- 不可继承的样式：border padding margin width height ;
- 优先级就近原则，同权重情况下样式定义最近者为准;
- 载入样式以最后载入的定位为准;

> 优先级为:

```
!important >  id > class > tag  

important 比 内联优先级高,但内联比 id 要高
```

> CSS3新增伪类举例：

```
p:first-of-type 选择属于其父元素的首个 <p> 元素的每个 <p> 元素。
p:last-of-type  选择属于其父元素的最后 <p> 元素的每个 <p> 元素。
p:only-of-type  选择属于其父元素唯一的 <p> 元素的每个 <p> 元素。
p:only-child    选择属于其父元素的唯一子元素的每个 <p> 元素。
p:nth-child(2)  选择属于其父元素的第二个子元素的每个 <p> 元素。
:enabled  :disabled 控制表单控件的禁用状态。
:checked        单选框或复选框被选中。
```



### position的值， relative和absolute分别是相对于谁进行定位的？

```
absolute 
        生成绝对定位的元素， 相对于最近一级的 定位不是 static 的父元素来进行定位。

fixed （老IE不支持）
    生成绝对定位的元素，相对于浏览器窗口进行定位。 

relative 
    生成相对定位的元素，相对于其在普通流中的位置进行定位。 

static  默认值。没有定位，元素出现在正常的流中
```



### XML和JSON的区别？

(1).数据体积方面。
JSON相对于XML来讲，数据的体积小，传递的速度更快些。
(2).数据交互方面。
JSON与JavaScript的交互更加方便，更容易解析处理，更好的数据交互。
(3).数据描述方面。
JSON对数据的描述性比XML较差。
(4).传输速度方面。
JSON的速度要远远快于XML。



### 对BFC规范的理解？

​      BFC，块级格式化上下文，一个创建了新的BFC的盒子是独立布局的，盒子里面的子元素的样式不会影响到外面的元素。在同一个BFC中的两个毗邻的块级盒在垂直方向（和布局方向有关系）的margin会发生折叠。
​    （W3C CSS 2.1 规范中的一个概念，它决定了元素如何对其内容进行布局，以及与其他元素的关系和相互作用。）



### 解释下 CSS sprites，以及你要如何在页面或网站中使用它。

CSS Sprites其实就是把网页中一些背景图片整合到一张图片文件中，再利用CSS的“background-image”，“background- repeat”，“background-position”的组合进行背景定位，background-position可以用数字能精确的定位出背景图片的位置。这样可以减少很多图片请求的开销，因为请求耗时比较长；请求虽然可以并发，但是也有限制，一般浏览器都是6个。对于未来而言，就不需要这样做了，因为有了`http2`。



## html部分

### Doctype作用? 严格模式与混杂模式如何区分？它们有何意义?

（1）<!DOCTYPE> 声明位于文档中的最前面，处于 <html> 标签之前。告知浏览器以何种模式来渲染文档。 

（2）严格模式的排版和 JS 运作模式是  以该浏览器支持的最高标准运行。

（3）在混杂模式中，页面以宽松的向后兼容的方式显示。模拟老式浏览器的行为以防止站点无法工作。

（4）DOCTYPE不存在或格式不正确会导致文档以混杂模式呈现。



### 你知道多少种Doctype文档类型？

 该标签可声明三种 DTD 类型，分别表示严格版本、过渡版本以及基于框架的 HTML 文档。
 HTML 4.01 规定了三种文档类型：Strict、Transitional 以及 Frameset。
 XHTML 1.0 规定了三种 XML 文档类型：Strict、Transitional 以及 Frameset。
Standards （标准）模式（也就是严格呈现模式）用于呈现遵循最新标准的网页，而 Quirks
 （包容）模式（也就是松散呈现模式或者兼容模式）用于呈现为传统浏览器而设计的网页。



### HTML与XHTML——二者有什么区别

区别：
1.所有的标记都必须要有一个相应的结束标记
2.所有标签的元素和属性的名字都必须使用小写
3.所有的XML标记都必须合理嵌套
4.所有的属性必须用引号""括起来
5.把所有<和&特殊符号用编码表示
6.给所有属性赋一个值
7.不要在注释内容中使“--”
8.图片必须有说明文字



### 常见兼容性问题？

* png24位的图片在iE6浏览器上出现背景，解决方案是做成PNG8.也可以引用一段脚本处理.

* 浏览器默认的margin和padding不同。解决方案是加一个全局的*\\{margin:0;padding:0;\\}来统一。

* IE6双边距bug:块属性标签float后，又有横行的margin情况下，在ie6显示margin比设置的大。 

* 浮动ie产生的双倍距离（IE6双边距问题：在IE6下，如果对元素设置了浮动，同时又设置了margin-left或margin-right，margin值会加倍。）
  #box\\{ float:left; width:10px; margin:0 0 0 100px;\\} 

 这种情况之下IE会产生20px的距离，解决方案是在float的标签样式控制中加入 ——_display:inline;将其转化为行内属性。(_这个符号只有ie6会识别)

* 渐进识别的方式，从总体中逐渐排除局部。 

  首先，巧妙的使用“\9”这一标记，将IE游览器从所有情况中分离出来。 
  接着，再次使用“+”将IE8和IE7、IE6分离开来，这样IE8已经独立识别。

  ```
  css
      .bb\\{
       background-color:#f1ee18;/*所有识别*/
      .background-color:#00deff\9; /*IE6、7、8识别*/
      +background-color:#a200ff;/*IE6、7识别*/
      _background-color:#1e0bd1;/*IE6识别*/ 
      \\} 
  ```

*  IE下,可以使用获取常规属性的方法来获取自定义属性,
   也可以使用getAttribute()获取自定义属性;
   Firefox下,只能使用getAttribute()获取自定义属性. 
   解决方法:统一通过getAttribute()获取自定义属性.

* IE下,event对象有x,y属性,但是没有pageX,pageY属性; 
  Firefox下,event对象有pageX,pageY属性,但是没有x,y属性.

* 解决方法：（条件注释）缺点是在IE浏览器下可能会增加额外的HTTP请求数。

* Chrome 中文界面下默认会将小于 12px 的文本强制按照 12px 显示, 
  可通过加入 CSS 属性 -webkit-text-size-adjust: none; 解决.

* 超链接访问过后hover样式就不出现了 被点击访问过的超链接样式不在具有hover和active了解决方法是改变CSS属性的排列顺序:
L-V-H-A :  a:link \\{\\} a:visited \\{\\} a:hover \\{\\} a:active \\{\\}

* 怪异模式问题：漏写DTD声明，Firefox仍然会按照标准模式来解析网页，但在IE中会触发怪异模式。为避免怪异模式给我们带来不必要的麻烦，最好养成书写DTD声明的好习惯。现在可以使用[html5](http://www.w3.org/TR/html5/single-page.html)推荐的写法：`<doctype html>`

* 上下margin重合问题
  ie和ff都存在，相邻的两个div的margin-left和margin-right不会重合，但是margin-top和margin-bottom却会发生重合。
  解决方法，养成良好的代码编写习惯，同时采用margin-top或者同时采用margin-bottom。

* ie6对png图片格式支持不好(引用一段脚本处理)



### 解释下浮动和它的工作原理？清除浮动的技巧

浮动元素脱离文档流，不占据空间。浮动元素碰到包含它的边框或者浮动元素的边框停留。

1.使用空标签清除浮动。
   这种方法是在所有浮动标签后面添加一个空标签 定义css clear:both. 弊端就是增加了无意义标签。
2.使用overflow。
   给包含浮动元素的父标签添加css属性 overflow:auto; zoom:1; zoom:1用于兼容IE6。
3.使用after伪对象清除浮动。
   该方法只适用于非IE浏览器。具体写法可参照以下示例。使用中需注意以下几点。一、该方法中必须为需要清除浮动元素的伪对象中设置 height:0，否则该元素会比实际高出若干像素；



### 浮动元素引起的问题和解决办法？

浮动元素引起的问题：

（1）父元素的高度无法被撑开，影响与父元素同级的元素
（2）与浮动元素同级的非浮动元素（内联元素）会跟随其后
（3）若非第一个元素浮动，则该元素之前的元素也需要浮动，否则会影响页面显示的结构

解决方法：
使用`CSS`中的`clear:both`;属性来清除元素的浮动可解决2、3问题，对于问题1，添加如下样式，给父元素添加`clearfix`样式：

```
.clearfix:after\\{content: ".";display: block;height: 0;clear: both;visibility: hidden;\\}
.clearfix\\{display: inline-block;\\} /* for IE/Mac */
```

**清除浮动的几种方法：**

```
1，额外标签法，<div style="clear:both;"></div>（缺点：不过这个办法会增加额外的标签使HTML结构看起来不够简洁。）
2，使用after伪类

#parent:after\\{
    content:".";
    height:0;
    visibility:hidden;
    display:block;
    clear:both;
    \\}

3,浮动外部元素
4,设置`overflow`为`hidden`或者auto
```



### IE 8以下版本的浏览器中的盒模型有什么不同

IE8以下浏览器的盒模型中定义的元素的宽高不包括内边距和边框



### DOM操作——怎样添加、移除、移动、复制、创建和查找节点。

（1）创建新节点

​      createDocumentFragment()    //创建一个DOM片段

​      createElement()   //创建一个具体的元素

​      createTextNode()   //创建一个文本节点

（2）添加、移除、替换、插入

​      appendChild()

​      removeChild()

​      replaceChild()

​      insertBefore() //在已有的子节点前插入一个新的子节点

（3）查找

​      getElementsByTagName()    //通过标签名称

​      getElementsByName()    //通过元素的Name属性的值(IE容错能力较强，会得到一个数组，其中包括id等于name值的)

​      getElementById()    //通过元素Id，唯一性



### iframe的优缺点？

1.`<iframe>`优点：

​    解决加载缓慢的第三方内容如图标和广告等的加载问题
​    Security sandbox
​    并行加载脚本

2.`<iframe>`的缺点：


​    *iframe会阻塞主页面的Onload事件；

​    *即时内容为空，加载也需要时间
​    *没有语意 



### 如何实现浏览器内多个标签页之间的通信?

调用localstorge、cookies等本地存储方式



### 线程与进程的区别

一个程序至少有一个进程,一个进程至少有一个线程. 
线程的划分尺度小于进程，使得多线程程序的并发性高。 
另外，进程在执行过程中拥有独立的内存单元，而多个线程共享内存，从而极大地提高了程序的运行效率。 
线程在执行过程中与进程还是有区别的。每个独立的线程有一个程序运行的入口、顺序执行序列和程序的出口。但是线程不能够独立执行，必须依存在应用程序中，由应用程序提供多个线程执行控制。 
从逻辑角度来看，多线程的意义在于一个应用程序中，有多个执行部分可以同时执行。但操作系统并没有将多个线程看做多个独立的应用，来实现进程的调度和管理以及资源分配。这就是进程和线程的重要区别。



### 你如何对网站的文件和资源进行优化？

期待的解决方案包括：
 文件合并
 文件最小化/文件压缩
 使用 CDN 托管
 缓存的使用（多个域名来提供缓存）
 其他



### 请说出三种减少页面加载时间的方法。

 1.优化图片 
 2.图像格式的选择（GIF：提供的颜色较少，可用在一些对颜色要求不高的地方） 
 3.优化CSS（压缩合并css，如margin-top,margin-left...) 
 4.网址后加斜杠（如www.campr.com/目录，会判断这个“目录是什么文件类型，或者是目录。） 
 5.标明高度和宽度（如果浏览器没有找到这两个参数，它需要一边下载图片一边计算大小，如果图片很多，浏览器需要不断地调整页面。这不但影响速度，也影响浏览体验。 
当浏览器知道了高度和宽度参数后，即使图片暂时无法显示，页面上也会腾出图片的空位，然后继续加载后面的内容。从而加载时间快了，浏览体验也更好了。） 
 6.减少http请求（合并文件，合并图片）。



### 你都使用哪些工具来测试代码的性能？

```
Profiler, JSPerf（http://jsperf.com/nexttick-vs-setzerotimeout-vs-settimeout）, Dromaeo
```



### 什么是 FOUC（无样式内容闪烁）？你如何来避免 FOUC？

```
 FOUC - Flash Of Unstyled Content 文档样式闪烁
 <style type="text/css" media="all">@import "../fouc.css";</style> 
而引用CSS文件的@import就是造成这个问题的罪魁祸首。IE会先加载整个HTML文档的DOM，然后再去导入外部的CSS文件，因此，在页面DOM加载完成到CSS导入完成中间会有一段时间页面上的内容是没有样式的，这段时间的长短跟网速，电脑速度都有关系。
 解决方法简单的出奇，只要在<head>之间加入一个<link>或者<script>元素就可以了。
```



### null和undefined的区别？

`null`是一个表示”无”的对象，转为数值时为0；`undefined`是一个表示”无”的原始值，转为数值时为`NaN`。

当声明的变量还未被初始化时，变量的默认值为`undefined`。
`null`用来表示尚未存在的对象，常用来表示函数企图返回一个不存在的对象。

#### `undefined`表示”缺少值”，就是此处应该有一个值，但是还没有定义。典型用法是：

（1）变量被声明了，但没有赋值时，就等于undefined。

（2) 调用函数时，应该提供的参数没有提供，该参数等于undefined。

（3）对象没有赋值的属性，该属性的值为undefined。

（4）函数没有返回值时，默认返回undefined。

#### `null`表示”没有对象”，即该处不应该有值。典型用法是：

（1） 作为函数的参数，表示该函数的参数不是对象。

（2） 作为对象原型链的终点。



### js延迟加载的方式有哪些？

defer和async、动态创建DOM方式（创建script，插入到DOM中，加载完毕后callBack）、按需异步载入js



### 如何解决跨域问题?

jsonp、 document.domain+iframe、window.name、window.postMessage、服务器上设置代理页面
jsonp的原理是动态插入script标签

具体参见：[详解js跨域问题](http://segmentfault.com/blog/trigkit4/1190000000718840)



### documen.write和 innerHTML的区别

document.write只能重绘整个页面

innerHTML可以重绘页面的一部分



### 哪些操作会造成内存泄漏？

内存泄漏指任何对象在您不再拥有或需要它之后仍然存在。
垃圾回收器定期扫描对象，并计算引用了每个对象的其他对象的数量。如果一个对象的引用数量为 0（没有其他对象引用过该对象），或对该对象的惟一引用是循环的，那么该对象的内存即可回收。

setTimeout 的第一个参数使用字符串而非函数的话，会引发内存泄漏。
闭包、控制台日志、循环（在两个对象彼此引用且彼此保留时，就会产生一个循环）

详见：[详解js变量、作用域及内存](http://segmentfault.com/blog/trigkit4/1190000000687844)



### JavaScript中的作用域与变量声明提升？

详见：[详解JavaScript函数模式](http://segmentfault.com/blog/trigkit4/1190000000758184#articleHeader5)



### 如何判断当前脚本运行在浏览器还是node环境中？

通过判断Global对象是否为window，如果不为window，当前脚本没有运行在浏览器中



### WEB应用从服务器主动推送Data到客户端有那些方式？

Javascript数据推送

> Commet：基于HTTP长连接的服务器推送技术
>
> 基于WebSocket的推送方案
>
> SSE（Server-Send Event）：服务器推送数据新方式



### 对前端界面工程师这个职位是怎么样理解的？它的前景会怎么样？

前端是最贴近用户的程序员，比后端、数据库、产品经理、运营、安全都近。
    1、实现界面交互
    2、提升用户体验
    3、有了Node.js，前端可以实现服务端的一些事情


前端是最贴近用户的程序员，前端的能力就是能让产品从 90分进化到 100 分，甚至更好，

 参与项目，快速高质量完成实现效果图，精确到1px；

 与团队成员，UI设计，产品经理的沟通；

 做好的页面结构，页面重构和用户体验；

 处理hack，兼容、写出优美的代码格式；

 针对服务器的优化、拥抱最新前端技术。



### 你有哪些性能优化的方法？

（[详情请看雅虎14条性能优化原则](http://segmentfault.com/blog/trigkit4/1190000000656717)）。

  （1） 减少http请求次数：CSS Sprites, JS、CSS源码压缩、图片大小控制合适；网页Gzip，CDN托管，data缓存 ，图片服务器。

  （2） 前端模板 JS+数据，减少由于HTML标签导致的带宽浪费，前端用变量保存AJAX请求结果，每次操作本地变量，不用请求，减少请求次数

  （3） 用innerHTML代替DOM操作，减少DOM操作次数，优化javascript性能。

  （4） 当需要设置的样式很多时设置className而不是直接操作style。

  （5） 少用全局变量、缓存DOM节点查找的结果。减少IO读取操作。

  （6） 避免使用CSS Expression（css表达式)又称Dynamic properties(动态属性)。

  （7） 图片预加载，将样式表放在顶部，将脚本放在底部  加上时间戳。

详情：http://segmentfault.com/blog/trigkit4/1190000000691919



### 一个页面从输入 URL 到页面加载显示完成，这个过程中都发生了什么？

​    分为4个步骤：
​    （1），当发送一个URL请求时，不管这个URL是Web页面的URL还是Web页面上每个资源的URL，浏览器都会开启一个线程来处理这个请求，同时在远程DNS服务器上启动一个DNS查询。这能使浏览器获得请求对应的IP地址。
​    （2）， 浏览器与远程Web服务器通过TCP三次握手协商来建立一个TCP/IP连接。该握手包括一个同步报文，一个同步-应答报文和一个应答报文，这三个报文在 浏览器和服务器之间传递。该握手首先由客户端尝试建立起通信，而后服务器应答并接受客户端的请求，最后由客户端发出该请求已经被接受的报文。
​    （3），一旦TCP/IP连接建立，浏览器会通过该连接向远程服务器发送HTTP的GET请求。远程服务器找到资源并使用HTTP响应返回该资源，值为200的HTTP响应状态表示一个正确的响应。
​    （4），此时，Web服务器提供资源服务，客户端开始下载资源。

请求返回后，便进入了我们关注的前端模块
简单来说，浏览器会解析HTML生成DOM Tree，其次会根据CSS生成CSS Rule Tree，而javascript又可以根据DOM API操作DOM

详情：[从输入 URL 到浏览器接收的过程中发生了什么事情？](http://segmentfault.com/blog/trigkit4/1190000000697254)



### 平时如何管理你的项目？

先期团队必须确定好全局样式（globe.css），编码模式(utf-8) 等；

编写习惯必须一致（例如都是采用继承式的写法，单样式都写成一行）；

标注样式编写人，各模块都及时标注（标注关键样式调用的地方）；

页面进行标注（例如 页面 模块 开始和结束）；

CSS跟HTML 分文件夹并行存放，命名都得统一（例如style.css）；

 JS 分文件夹存放 命名以该JS功能为准的英文翻译。

图片采用整合的 images.png png8 格式文件使用 尽量整合在一起使用方便将来的管理 



### 说说最近最流行的一些东西吧？常去哪些网站？

Node.js、Mongodb、npm、MVVM、MEAN、three.js,React 。
网站：w3cfuns,sf,hacknews,CSDN,慕课，博客园，InfoQ,w3cplus等



### javascript对象的几种创建方式

1，工厂模式
2，构造函数模式
3，原型模式
4，混合构造函数和原型模式
5，动态原型模式
6，寄生构造函数模式
7，稳妥构造函数模式



### javascript继承的6种方法

1，原型链继承
2，借用构造函数继承
3，组合继承(原型+借用构造)
4，原型式继承
5，寄生式继承
6，寄生组合式继承

详情：[JavaScript继承方式详解](http://segmentfault.com/blog/trigkit4/1190000002440502)



### ajax过程

(1)创建XMLHttpRequest对象,也就是创建一个异步调用对象.

(2)创建一个新的HTTP请求,并指定该HTTP请求的方法、URL及验证信息.

(3)设置响应HTTP请求状态变化的函数.

(4)发送HTTP请求.

(5)获取异步调用返回的数据.

(6)使用JavaScript和DOM实现局部刷新.

详情：[JavaScript学习总结（七）Ajax和Http状态字](http://segmentfault.com/blog/trigkit4/1190000000691919)



### 异步加载和延迟加载

1.异步加载的方案： 动态插入script标签
2.通过ajax去获取js代码，然后通过eval执行
3.script标签上添加defer或者async属性
4.创建并插入iframe，让它异步执行js
5.延迟加载：有些 js 代码并不是页面初始化的时候就立刻需要的，而稍后的某些情况才需要的。



## 前端安全问题？

### sql注入原理

就是通过把`SQL`命令插入到`Web`表单递交或输入域名或页面请求的查询字符串，最终达到欺骗服务器执行恶意的SQL命令。

总的来说有以下几点：

1.永远不要信任用户的输入，要对用户的输入进行校验，可以通过正则表达式，或限制长度，对单引号和双"-"进行转换等。
2.永远不要使用动态拼装SQL，可以使用参数化的SQL或者直接使用存储过程进行数据查询存取。
3.永远不要使用管理员权限的数据库连接，为每个应用使用单独的权限有限的数据库连接。
4.不要把机密信息明文存放，请加密或者hash掉密码和敏感的信息。



### XSS原理及防范

`Xss(cross-site scripting)`攻击指的是攻击者往Web页面里插入恶意`html`标签或者`javascript`代码。比如：攻击者在论坛中放一个
看似安全的链接，骗取用户点击后，窃取cookie中的用户私密信息；或者攻击者在论坛中加一个恶意表单，
当用户提交表单的时候，却把信息传送到攻击者的服务器中，而不是用户原本以为的信任站点。



### XSS防范方法

1.代码里对用户输入的地方和变量都需要仔细检查长度和对`”<”,”>”,”;”,”’”`等字符做过滤；其次任何内容写到页面之前都必须加以`encode`，避免不小心把`html tag` 弄出来。这一个层面做好，至少可以堵住超过一半的`XSS` 攻击。


2.避免直接在`cookie` 中泄露用户隐私，例如`email`、密码等等。
3.通过使cookie 和系统ip 绑定来降低`cookie` 泄露后的危险。这样攻击者得到的cookie 没有实际价值，不可能拿来重放。


4.尽量采用POST 而非GET 提交表单



### XSS与CSRF有什么区别吗？

`XSS`是获取信息，不需要提前知道其他用户页面的代码和数据包。`CSRF`是代替用户完成指定的动作，需要知道其他用户页面的代码和数据包。

要完成一次CSRF攻击，受害者必须依次完成两个步骤：

　　1.登录受信任网站A，并在本地生成Cookie。
　　2.在不登出A的情况下，访问危险网站B。



### CSRF的防御

1.服务端的CSRF方式方法很多样，但总的思想都是一致的，就是在客户端页面增加伪随机数。
2.使用验证码



### ie各版本和chrome可以并行下载多少个资源

IE6 两个并发，iE7升级之后的6个并发，之后版本也是6个

Firefox，chrome也是6个



### javascript里面的继承怎么实现，如何避免原型链上面的对象共享

用构造函数和原型链的混合模式去实现继承，避免对象共享可以参考经典的extend()函数，很多前端框架都有封装的，就是用一个空函数当做中间变量



### grunt， YUI compressor 和 google clojure用来进行代码压缩的用法。

```
YUI Compressor 是一个用来压缩 JS 和 CSS 文件的工具，采用Java开发。

使用方法：

//压缩JS
java -jar yuicompressor-2.4.2.jar --type js --charset utf-8 -v src.js > packed.js
//压缩CSS
java -jar yuicompressor-2.4.2.jar --type css --charset utf-8 -v src.css > packed.css
```

详情请见：[你需要掌握的前端代码性能优化工具](http://segmentfault.com/blog/trigkit4/1190000002585760)



### Flash、Ajax各自的优缺点，在使用中如何取舍？

1、Flash ajax对比
Flash适合处理多媒体、矢量图形、访问机器；对CSS、处理文本上不足，不容易被搜索。
Ajax对CSS、文本支持很好，支持搜索；多媒体、矢量图形、机器访问不足。
共同点：与服务器的无刷新传递消息、用户离线和在线状态、操作DOM



### 请解释一下 JavaScript 的同源策略。

概念:同源策略是客户端脚本（尤其是`Javascript`）的重要的安全度量标准。它最早出自`Netscape Navigator2.0`，其目的是防止某个文档或脚本从多个不同源装载。

这里的同源策略指的是：协议，域名，端口相同，同源策略是一种安全协议。
指一段脚本只能读取来自同一来源的窗口和文档的属性。



### 为什么要有同源限制？

我们举例说明：比如一个黑客程序，他利用`Iframe`把真正的银行登录页面嵌到他的页面上，当你使用真实的用户名，密码登录时，他的页面就可以通过`Javascript`读取到你的表单中`input`中的内容，这样用户名，密码就轻松到手了。



### 什么是 “use strict”; ? 使用它的好处和坏处分别是什么？

`ECMAscript 5`添加了第二种运行模式：”严格模式”（strict mode）。顾名思义，这种模式使得`Javascript`在更严格的条件下运行。

设立”严格模式”的目的，主要有以下几个：

```
- 消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为;
- 消除代码运行的一些不安全之处，保证代码运行的安全；
- 提高编译器效率，增加运行速度；
- 为未来新版本的Javascript做好铺垫。
```

注：经过测试`IE6,7,8,9`均不支持严格模式。

缺点：
现在网站的`JS` 都会进行压缩，一些文件用了严格模式，而另一些没有。这时这些本来是严格模式的文件，被 `merge` 后，这个串就到了文件的中间，不仅没有指示严格模式，反而在压缩后浪费了字节。



### GET和POST的区别，何时使用POST？

​    GET：一般用于信息获取，使用URL传递参数，对所发送信息的数量也有限制，一般在2000个字符
​    POST：一般用于修改服务器上的资源，对所发送的信息没有限制。

​    GET方式需要使用Request.QueryString来取得变量的值，而POST方式通过Request.Form来获取变量的值，
​    也就是说Get是通过地址栏来传值，而Post是通过提交表单来传值。

然而，在以下情况中，请使用 POST 请求：
无法使用缓存文件（更新服务器上的文件或数据库）
向服务器发送大量数据（POST 没有数据量限制）
发送包含未知字符的用户输入时，POST 比 GET 更稳定也更可靠



### 哪些地方会出现css阻塞，哪些地方会出现js阻塞？

**js的阻塞特性：**

所有浏览器在下载`JS`的时候，会阻止一切其他活动，比如其他资源的下载，内容的呈现等等。直到`JS`下载、解析、执行完毕后才开始继续`并行下载`其他资源并呈现内容。为了提高用户体验，新一代浏览器都支持并行下载`JS`，但是`JS`下载仍然会阻塞其它资源的下载（例如.图片，css文件等）。

由于浏览器为了防止出现`JS`修改`DOM`树，需要重新构建`DOM`树的情况，所以就会阻塞其他的下载和呈现。

嵌入`JS`会阻塞所有内容的呈现，而外部`JS`只会阻塞其后内容的显示，2种方式都会阻塞其后资源的下载。也就是说外部样式不会阻塞外部脚本的加载，但会阻塞外部脚本的执行。

`CSS`怎么会阻塞加载了？

`CSS`本来是可以并行下载的，在什么情况下会出现阻塞加载了(在测试观察中，`IE6`下`CSS`都是阻塞加载）

当`CSS`后面跟着嵌入的`JS`的时候，该`CSS`就会出现阻塞后面资源下载的情况。而当把嵌入`JS`放到`CSS`前面，就不会出现阻塞的情况了。

根本原因：

因为浏览器会维持`html`中`css`和`js`的顺序，样式表必须在嵌入的JS执行前先加载、解析完。而嵌入的`JS`会阻塞后面的资源加载，所以就会出现上面`CSS`阻塞下载的情况。



### 嵌入`JS`应该放在什么位置？

   1、放在底部，虽然放在底部照样会阻塞所有呈现，但不会阻塞资源下载。

   2、如果嵌入JS放在head中，请把嵌入JS放在CSS头部。

   3、使用defer（只支持IE）

   4、不要在嵌入的JS中调用运行时间较长的函数，如果一定要用，可以用`setTimeout`来调用



### Javascript无阻塞加载具体方式

- **将脚本放在底部。**`<link>`还是放在`head`中，用以保证在`js`加载前，能加载出正常显示的页面。`<script>`标签放在`</body>`前。
- **成组脚本**：由于每个`<script>`标签下载时阻塞页面解析过程，所以限制页面的`<script>`总数也可以改善性能。适用于内联脚本和外部脚本。
- **非阻塞脚本**：等页面完成加载后，再加载`js`代码。也就是，在`window.onload`事件发出后开始下载代码。
  （1）`defer`属性：支持IE4和`fierfox3.5`更高版本浏览器
  （2）动态脚本元素：文档对象模型（DOM）允许你使用js动态创建`HTML`的几乎全部文档内容。代码如下：

```
<script>
    var script=document.createElement("script");
    script.type="text/javascript";
    script.src="file.js";
    document.getElementsByTagName("head")[0].appendChild(script);
</script>
```

此技术的重点在于：无论在何处启动下载，文件额下载和运行都不会阻塞其他页面处理过程。即使在head里（除了用于下载文件的http链接）。



### 闭包相关问题？

详情请见：[详解js闭包](http://segmentfault.com/blog/trigkit4/1190000000652891)



### js事件处理程序问题？

详情请见：[JavaScript学习总结（九）事件详解](http://segmentfault.com/blog/trigkit4/1190000002174034)



### eval是做什么的？

它的功能是把对应的字符串解析成JS代码并运行；
应该避免使用eval，不安全，非常耗性能（2次，一次解析成js语句，一次执行）。



### JavaScript原型，原型链 ? 有什么特点？

*  原型对象也是普通的对象，是对象一个自带隐式的 __proto__ 属性，原型也有可能有自己的原型，如果一个原型对象的原型不为null的话，我们就称之为原型链。
*  原型链是由一些用来继承和共享属性的对象组成的（有限的）对象链。



### 事件、IE与火狐的事件机制有什么区别？ 如何阻止冒泡？

 1. 我们在网页中的某个操作（有的操作对应多个事件）。例如：当我们点击一个按钮就会产生一个事件。是可以被 JavaScript 侦测到的行为。  
 2. 事件处理机制：IE是事件冒泡、firefox同时支持两种事件模型，也就是：捕获型事件和冒泡型事件。；
 3.  ev.stopPropagation();注意旧ie的方法 ev.cancelBubble = true;



### ajax 是什么?ajax 的交互模型?同步和异步的区别?如何解决跨域问题?

详情请见：[JavaScript学习总结（七）Ajax和Http状态字](http://segmentfault.com/blog/trigkit4/1190000000691919)

1. 通过异步模式，提升了用户体验

  2. 优化了浏览器和服务器之间的传输，减少不必要的数据往返，减少了带宽占用

  3. Ajax在客户端运行，承担了一部分本来由服务器承担的工作，减少了大用户量下的服务器负载。

  2. Ajax的最大的特点是什么。

  Ajax可以实现动态不刷新（局部刷新）
  readyState属性 状态 有5个可取值： 0=未初始化 ，1=启动 2=发送，3=接收，4=完成

ajax的缺点

  1、ajax不支持浏览器back按钮。

  2、安全问题 AJAX暴露了与服务器交互的细节。

  3、对搜索引擎的支持比较弱。

  4、破坏了程序的异常机制。

  5、不容易调试。

跨域： jsonp、 iframe、window.name、window.postMessage、服务器上设置代理页面



### js对象的深度克隆

```
  function clone(Obj) \\{   
        var buf;   
        if (Obj instanceof Array) \\{   
            buf = [];  //创建一个空的数组 
            var i = Obj.length;   
            while (i--) \\{   
                buf[i] = clone(Obj[i]);   
            \\}   
            return buf;   
        \\}else if (Obj instanceof Object)\\{   
            buf = \\{\\};  //创建一个空对象 
            for (var k in Obj) \\{  //为这个对象添加新的属性 
                buf[k] = clone(Obj[k]);   
            \\}   
            return buf;   
        \\}else\\{   
            return Obj;   
        \\}   
    \\}
```



### AMD和CMD 规范的区别？

详情请见：[详解JavaScript模块化开发](http://segmentfault.com/blog/trigkit4/1190000000733959)



### 网站重构的理解？

网站重构：在不改变外部行为的前提下，简化结构、添加可读性，而在网站前端保持一致的行为。也就是说是在不改变UI的情况下，对网站进行优化，在扩展的同时保持一致的UI。

对于传统的网站来说重构通常是：

表格(table)布局改为DIV+CSS
使网站前端兼容于现代浏览器(针对于不合规范的CSS、如对IE6有效的)
对于移动平台的优化
针对于SEO进行优化
深层次的网站重构应该考虑的方面

减少代码间的耦合
让代码保持弹性
严格按规范编写代码
设计可扩展的API
代替旧有的框架、语言(如VB)
增强用户体验
通常来说对于速度的优化也包含在重构中

压缩JS、CSS、image等前端资源(通常是由服务器来解决)
程序的性能优化(如数据读写)
采用CDN来加速资源加载
对于JS DOM的优化
HTTP服务器的文件缓存



### 如何获取UA？

```
<script> 
    function whatBrowser() \\{  
        document.Browser.Name.value=navigator.appName;  
        document.Browser.Version.value=navigator.appVersion;  
        document.Browser.Code.value=navigator.appCodeName;  
        document.Browser.Agent.value=navigator.userAgent;  
    \\}  
</script>
```



### js数组去重

以下是数组去重的三种方法：

```
Array.prototype.unique1 = function () \\{
  var n = []; //一个新的临时数组
  for (var i = 0; i < this.length; i++) //遍历当前数组
  \\{
    //如果当前数组的第i已经保存进了临时数组，那么跳过，
    //否则把当前项push到临时数组里面
    if (n.indexOf(this[i]) == -1) n.push(this[i]);
  \\}
  return n;
\\}

Array.prototype.unique2 = function()
\\{
    var n = \\{\\},r=[]; //n为hash表，r为临时数组
    for(var i = 0; i < this.length; i++) //遍历当前数组
    \\{
        if (!n[this[i]]) //如果hash表中没有当前项
        \\{
            n[this[i]] = true; //存入hash表
            r.push(this[i]); //把当前数组的当前项push到临时数组里面
        \\}
    \\}
    return r;
\\}

Array.prototype.unique3 = function()
\\{
    var n = [this[0]]; //结果数组
    for(var i = 1; i < this.length; i++) //从第二项开始遍历
    \\{
        //如果当前数组的第i项在当前数组中第一次出现的位置不是i，
        //那么表示第i项是重复的，忽略掉。否则存入结果数组
        if (this.indexOf(this[i]) == i) n.push(this[i]);
    \\}
    return n;
\\}
```



### HTTP状态码

```
100  Continue  继续，一般在发送post请求时，已发送了http header之后服务端将返回此信息，表示确认，之后发送具体参数信息
200  OK   正常返回信息
201  Created  请求成功并且服务器创建了新的资源
202  Accepted  服务器已接受请求，但尚未处理
301  Moved Permanently  请求的网页已永久移动到新位置。
302 Found  临时性重定向。
303 See Other  临时性重定向，且总是使用 GET 请求新的 URI。
304  Not Modified  自从上次请求后，请求的网页未修改过。

400 Bad Request  服务器无法理解请求的格式，客户端不应当尝试再次使用相同的内容发起请求。
401 Unauthorized  请求未授权。
403 Forbidden  禁止访问。
404 Not Found  找不到如何与 URI 相匹配的资源。

500 Internal Server Error  最常见的服务器端错误。
503 Service Unavailable 服务器端暂时无法处理请求（可能是过载或维护）。
```



### js操作获取和设置cookie

```
//创建cookie
function setCookie(name, value, expires, path, domain, secure) \\{
    var cookieText = encodeURIComponent(name) + '=' + encodeURIComponent(value);
    if (expires instanceof Date) \\{
        cookieText += '; expires=' + expires;
    \\}
    if (path) \\{
        cookieText += '; expires=' + expires;
    \\}
    if (domain) \\{
        cookieText += '; domain=' + domain;
    \\}
    if (secure) \\{
        cookieText += '; secure';
    \\}
    document.cookie = cookieText;
\\}

//获取cookie
function getCookie(name) \\{
    var cookieName = encodeURIComponent(name) + '=';
    var cookieStart = document.cookie.indexOf(cookieName);
    var cookieValue = null;
    if (cookieStart > -1) \\{
        var cookieEnd = document.cookie.indexOf(';', cookieStart);
        if (cookieEnd == -1) \\{
            cookieEnd = document.cookie.length;
        \\}
        cookieValue = decodeURIComponent(document.cookie.substring(cookieStart + cookieName.length, cookieEnd));
    \\}
    return cookieValue;
\\}

//删除cookie
function unsetCookie(name) \\{
    document.cookie = name + "= ; expires=" + new Date(0);
\\}
```



### 说说TCP传输的三次握手策略

为了准确无误地把数据送达目标处，TCP协议采用了三次握手策略。用TCP协议把数据包送出去后，TCP不会对传送  后的情况置之不理，它一定会向对方确认是否成功送达。握手过程中使用了TCP的标志：SYN和ACK。
发送端首先发送一个带SYN标志的数据包给对方。接收端收到后，回传一个带有SYN/ACK标志的数据包以示传达确认信息。最后，发送端再回传一个带ACK标志的数据包，代表“握手”结束
若在握手过程中某个阶段莫名中断，TCP协议会再次以相同的顺序发送相同的数据包。



### 说说你对Promise的理解

依照 `Promise/A+` 的定义，`Promise` 有四种状态：

```
pending: 初始状态, 非 fulfilled 或 rejected.
fulfilled: 成功的操作.
rejected: 失败的操作.
settled: Promise已被fulfilled或rejected，且不是pending
```

另外， `fulfilled` 与 `rejected` 一起合称 `settled`。

`Promise` 对象用来进行延迟(deferred) 和异步(asynchronous ) 计算。

> Promise 的构造函数

构造一个 `Promise`，最基本的用法如下：

```
var promise = new Promise(function(resolve, reject) \\{
    if (...) \\{  // succeed
        resolve(result);
    \\} else \\{   // fails
        reject(Error(errMessage));
    \\}
\\});
```

`Promise` 实例拥有 `then` 方法（具有 `then` 方法的对象，通常被称为 `thenable`）。它的使用方法如下：

```
promise.then(onFulfilled, onRejected)
```

接收两个函数作为参数，一个在 `fulfilled` 的时候被调用，一个在 `rejected` 的时候被调用，接收参数就是 `future，onFulfilled` 对应 `resolve`, `onRejected` 对应 `reject`。



## Javascript垃圾回收方法

### 标记清除（mark and sweep）

这是`JavaScript`最常见的垃圾回收方式，当变量进入执行环境的时候，比如函数中声明一个变量，垃圾回收器将其标记为“进入环境”，当变量离开环境的时候（函数执行结束）将其标记为“离开环境”。

垃圾回收器会在运行的时候给存储在内存中的所有变量加上标记，然后去掉环境中的变量以及被环境中变量所引用的变量（闭包），在这些完成之后仍存在标记的就是要删除的变量了



### 引用计数(reference counting)

在低版本`IE`中经常会出现[内存泄露](https://so.csdn.net/so/search?q=内存泄露&spm=1001.2101.3001.7020)，很多时候就是因为其采用引用计数方式进行垃圾回收。引用计数的策略是跟踪记录每个值被使用的次数，当声明了一个 变量并将一个引用类型赋值给该变量的时候这个值的引用次数就加1，如果该变量的值变成了另外一个，则这个值得引用次数减1，当这个值的引用次数变为0的时 候，说明没有变量在使用，这个值没法被访问了，因此可以将其占用的空间回收，这样垃圾回收器会在运行的时候清理掉引用次数为0的值占用的空间。

在IE中虽然`JavaScript`对象通过标记清除的方式进行垃圾回收，但BOM与DOM对象却是通过引用计数回收垃圾的，也就是说只要涉及BOM及DOM就会出现循环引用问题。



### 谈谈性能优化问题

代码层面：避免使用css表达式，避免使用高级选择器，通配选择器。
缓存利用：缓存Ajax，使用CDN，使用外部js和css文件以便缓存，添加Expires头，服务端配置Etag，减少DNS查找等
请求数量：合并样式和脚本，使用css图片精灵，初始首屏之外的图片资源按需加载，静态资源延迟加载。
请求带宽：压缩文件，开启GZIP，



### 移动端性能优化

> 尽量使用`css3`动画，开启硬件加速。适当使用`touch`事件代替`click`事件。避免使用`css3`渐变阴影效果。
> 尽可能少的使用`box-shadow`与`gradients`。`box-shadow`与`gradients`往往都是页面的性能杀手



### 什么是Etag？

浏览器下载组件的时候，会将它们存储到浏览器缓存中。如果需要再次获取相同的组件，浏览器将检查组件的缓存时间，
假如已经过期，那么浏览器将发送一个条件GET请求到服务器，服务器判断缓存还有效，则发送一个304响应，
告诉浏览器可以重用缓存组件。

那么服务器是根据什么判断缓存是否还有效呢?答案有两种方式，一种是前面提到的ETag，另一种是根据`Last-Modified`



### Expires和Cache-Control

`Expires`要求客户端和服务端的时钟严格同步。HTTP1.1引入`Cache-Control`来克服Expires头的限制。如果max-age和Expires同时出现，则max-age有更高的优先级。

```
Cache-Control: no-cache, private, max-age=0
ETag: abcde
Expires: Thu, 15 Apr 2014 20:00:00 GMT
Pragma: private
Last-Modified: $now // RFC1123 format
```



### 栈和队列的区别?

栈的插入和删除操作都是在一端进行的，而队列的操作却是在两端进行的。
队列先进先出，栈先进后出。
栈只允许在表尾一端进行插入和删除，而队列只允许在表尾一端进行插入，在表头一端进行删除 



### 栈和堆的区别？

栈区（stack）—   由编译器自动分配释放   ，存放函数的参数值，局部变量的值等。
堆区（heap）   —   一般由程序员分配释放，   若程序员不释放，程序结束时可能由OS回收。
堆（数据结构）：堆可以被看成是一棵树，如：堆排序；
栈（数据结构）：一种先进后出的数据结构。 



### 关于Http 2.0 你知道多少？

`HTTP/2`引入了“服务端推（serverpush）”的概念，它允许服务端在客户端需要数据之前就主动地将数据发送到客户端缓存中，从而提高性能。
`HTTP/2`提供更多的加密支持
`HTTP/2`使用多路技术，允许多个消息在一个连接上同时交差。
它增加了头压缩（header compression），因此即使非常小的请求，其请求和响应的`header`都只会占用很小比例的带宽。



### get请求传参长度的误区、get和post请求在缓存方面的区别

误区：我们经常说get请求参数的大小存在限制，而post请求的参数大小是无限制的。

实际上HTTP 协议从未规定 GET/POST 的请求长度限制是多少。对get请求参数的限制是来源与浏览器或web服务器，浏览器或web服务器限制了url的长度。为了明确这个概念，我们必须再次强调下面几点:

HTTP 协议 未规定 GET 和POST的长度限制
GET的最大长度显示是因为 浏览器和 web服务器限制了 URI的长度
不同的浏览器和WEB服务器，限制的最大长度不一样
要支持IE，则最大长度为2083byte，若只支持Chrome，则最大长度 8182byte
补充补充一个get和post在缓存方面的区别：

get请求类似于查找的过程，用户获取数据，可以不用每次都与数据库连接，所以可以使用缓存。
post不同，post做的一般是修改和删除的工作，所以必须与数据库交互，所以不能使用缓存。因此get请求适合于请求缓存。



### 模块化发展历程

可从IIFE、AMD、CMD、CommonJS、UMD、webpack(require.ensure)、ES Module、`<script type="module">` 这几个角度考虑。

模块化主要是用来抽离公共代码，隔离作用域，避免变量冲突等。

IIFE： 使用自执行函数来编写模块化，特点：在一个单独的函数作用域中执行代码，避免变量冲突。

```
(function()\\{
  return \\{
    data:[]
  \\}
\\})()
```

AMD： 使用requireJS 来编写模块化，特点：依赖必须提前声明好。

```
define('./index.js',function(code)\\{
    // code 就是index.js 返回的内容
\\})
```

CMD： 使用seaJS 来编写模块化，特点：支持动态引入依赖文件。

```
define(function(require, exports, module) \\{  
  var indexCode = require('./index.js');
\\})
```

CommonJS： nodejs 中自带的模块化。

```
var fs = require('fs');
```

UMD：兼容AMD，CommonJS 模块化语法。

webpack(require.ensure)：webpack 2.x 版本中的代码分割。

ES Modules： ES6 引入的模块化，支持import 来引入另一个 js 。

```
import a from 'a';
```



### npm 模块安装机制，为什么输入 npm install 就可以自动安装对应的模块？

#### npm 模块安装机制：

发出npm install命令
查询node_modules目录之中是否已经存在指定模块

若存在，不再重新安装
若不存在

npm 向 registry 查询模块压缩包的网址
下载压缩包，存放在根目录下的.npm目录里
解压压缩包到当前项目的node_modules目录
#### npm 实现原理

输入 npm install 命令并敲下回车后，会经历如下几个阶段（以 npm 5.5.1 为例）：

##### 执行工程自身 preinstall

当前 npm 工程如果定义了 preinstall 钩子此时会被执行。

##### 确定首层依赖模块

首先需要做的是确定工程中的首层依赖，也就是 dependencies 和 devDependencies 属性中直接指定的模块（假设此时没有添加 npm install 参数）。

工程本身是整棵依赖树的根节点，每个首层依赖模块都是根节点下面的一棵子树，npm 会开启多进程从每个首层依赖模块开始逐步寻找更深层级的节点。

##### 获取模块

获取模块是一个递归的过程，分为以下几步：

获取模块信息。在下载一个模块之前，首先要确定其版本，这是因为 package.json 中往往是 semantic version（semver，语义化版本）。此时如果版本描述文件（npm-shrinkwrap.json 或 package-lock.json）中有该模块信息直接拿即可，如果没有则从仓库获取。如 packaeg.json 中某个包的版本是 ^1.1.0，npm 就会去仓库中获取符合 1.x.x 形式的最新版本。
获取模块实体。上一步会获取到模块的压缩包地址（resolved 字段），npm 会用此地址检查本地缓存，缓存中有就直接拿，如果没有则从仓库下载。
查找该模块依赖，如果有依赖则回到第1步，如果没有则停止。

##### 模块扁平化（dedupe）

上一步获取到的是一棵完整的依赖树，其中可能包含大量重复模块。比如 A 模块依赖于 loadsh，B 模块同样依赖于 lodash。在 npm3 以前会严格按照依赖树的结构进行安装，因此会造成模块冗余。

从 npm3 开始默认加入了一个 dedupe 的过程。它会遍历所有节点，逐个将模块放在根节点下面，也就是 node-modules 的第一层。当发现有重复模块时，则将其丢弃。

这里需要对重复模块进行一个定义，它指的是模块名相同且 semver 兼容。每个 semver 都对应一段版本允许范围，如果两个模块的版本允许范围存在交集，那么就可以得到一个兼容版本，而不必版本号完全一致，这可以使更多冗余模块在 dedupe 过程中被去掉。

比如 node-modules 下 foo 模块依赖 lodash@^1.0.0，bar 模块依赖 lodash@^1.1.0，则 ^1.1.0 为兼容版本。

而当 foo 依赖 lodash@^2.0.0，bar 依赖 lodash@^1.1.0，则依据 semver 的规则，二者不存在兼容版本。会将一个版本放在 node_modules 中，另一个仍保留在依赖树里。

举个例子，假设一个依赖树原本是这样：

```
node_modules
-- foo
---- lodash@version1

-- bar
---- lodash@version2
```

假设 version1 和 version2 是兼容版本，则经过 dedupe 会成为下面的形式：

```
node_modules
-- foo

-- bar

-- lodash（保留的版本为兼容版本）
```

假设 version1 和 version2 为非兼容版本，则后面的版本保留在依赖树中：

```
node_modules
-- foo
-- lodash@version1

-- bar
---- lodash@version2
```

##### 安装模块

这一步将会更新工程中的 node_modules，并执行模块中的生命周期函数（按照 preinstall、install、postinstall 的顺序）。

##### 执行工程自身生命周期

当前 npm 工程如果定义了钩子此时会被执行（按照 install、postinstall、prepublish、prepare 的顺序）。

最后一步是生成或更新版本描述文件，npm install 过程完成。



### ES5的继承和ES6的继承有什么区别？

ES5的继承时通过prototype或构造函数机制来实现。ES5的继承实质上是先创建子类的实例对象，然后再将父类的方法添加到this上（Parent.apply(this)）。

ES6的继承机制完全不同，实质上是先创建父类的实例对象this（所以必须先调用父类的super()方法），然后再用子类的构造函数修改this。

具体的：ES6通过class关键字定义类，里面有构造方法，类之间通过extends关键字实现继承。子类必须在constructor方法中调用super方法，否则新建实例报错。因为子类没有自己的this对象，而是继承了父类的this对象，然后对其进行加工。如果不调用super方法，子类得不到this对象。

ps：super关键字指代父类的实例，即父类的this对象。在子类构造函数中，调用super后，才可使用this关键字，否则报错。



### 定时器的执行顺序或机制？

因为js是单线程的，浏览器遇到setTimeout或者setInterval会先执行完当前的代码块，在此之前会把定时器推入浏览器的待执行事件队列里面，等到浏览器执行完当前代码之后会看一下事件队列里面有没有任务，有的话才执行定时器的代码。所以即使把定时器的时间设置为0还是会先执行当前的一些代码。

```
function test()\\{
    var aa = 0;
    var testSet = setInterval(function()\\{
        aa++;
        console.log(123);
        if(aa<10)\\{
            clearInterval(testSet);
        \\}
    \\},20);
  var testSet1 = setTimeout(function()\\{
    console.log(321)
  \\},1000);
  for(var i=0;i<10;i++)\\{
    console.log('test');
  \\}
\\}
test()
```


输出结果：

```
test //10次
undefined
123
321
```



### ['1','2','3'].map(parseInt) 输出什么,为什么?

输出：[1, NaN, NaN]

首先让我们回顾一下，map函数的第一个参数callback：
var new_array = arr.map(function callback(currentValue[, index[, array]]) \\{ // Return element for new_array \\}[, thisArg])
这个callback一共可以接收三个参数，其中第一个参数代表当前被处理的元素，而第二个参数代表该元素的索引。

而parseInt则是用来解析字符串的，使字符串成为指定基数的整数。
parseInt(string, radix)
接收两个参数，第一个表示被处理的值（字符串），第二个表示为解析时的基数。
了解这两个函数后，我们可以模拟一下运行情况
parseInt('1', 0) //radix为0时，且string参数不以“0x”和“0”开头时，按照10为基数处理。这个时候返回1
parseInt('2', 1) //基数为1（1进制）表示的数中，最大值小于2，所以无法解析，返回NaN
parseInt('3', 2) //基数为2（2进制）表示的数中，最大值小于3，所以无法解析，返回NaN
map函数返回的是一个数组，所以最后结果为[1, NaN, NaN]



### Doctype作用? 严格模式与混杂模式如何区分？它们有何意义?

Doctype声明于文档最前面，告诉浏览器以何种方式来渲染页面，这里有两种模式，严格模式和混杂模式。

严格模式的排版和 JS 运作模式是 以该浏览器支持的最高标准运行。
混杂模式，向后兼容，模拟老式浏览器，防止浏览器无法兼容页面。



### fetch发送2次请求的原因

fetch发送post请求的时候，总是发送2次，第一次状态码是204，第二次才成功？

原因很简单，因为你用fetch的post请求的时候，导致fetch 第一次发送了一个Options请求，询问服务器是否支持修改的请求头，如果服务器支持，则在第二次中发送真正的请求。



## http、浏览器对象

### HTTPS 握手过程中，客户端如何验证证书的合法性

#### 首先什么是HTTP协议?

http协议是超文本传输协议，位于tcp/ip四层模型中的应用层；通过请求/响应的方式在客户端和服务器之间进行通信；但是缺少安全性，http协议信息传输是通过明文的方式传输，不做任何加密，相当于在网络上裸奔；容易被中间人恶意篡改，这种行为叫做中间人攻击；

#### 加密通信：

为了安全性，双方可以使用对称加密的方式key进行信息交流，但是这种方式对称加密秘钥也会被拦截，也不够安全，进而还是存在被中间人攻击风险；
于是人们又想出来另外一种方式，使用非对称加密的方式；使用公钥/私钥加解密；通信方A发起通信并携带自己的公钥，接收方B通过公钥来加密对称秘钥；然后发送给发起方A；A通过私钥解密；双发接下来通过对称秘钥来进行加密通信；但是这种方式还是会存在一种安全性；中间人虽然不知道发起方A的私钥，但是可以做到偷天换日，将拦截发起方的公钥key;并将自己生成的一对公/私钥的公钥发送给B；接收方B并不知道公钥已经被偷偷换过；按照之前的流程，B通过公钥加密自己生成的对称加密秘钥key2;发送给A；
这次通信再次被中间人拦截，尽管后面的通信，两者还是用key2通信，但是中间人已经掌握了Key2;可以进行轻松的加解密；还是存在被中间人攻击风险；

#### 解决困境：权威的证书颁发机构CA来解决；

制作证书：作为服务端的A，首先把自己的公钥key1发给证书颁发机构，向证书颁发机构进行申请证书；证书颁发机构有一套自己的公私钥，CA通过自己的私钥来加密key1,并且通过服务端网址等信息生成一个证书签名，证书签名同样使用机构的私钥进行加密；制作完成后，机构将证书发给A；
校验证书真伪：当B向服务端A发起请求通信的时候，A不再直接返回自己的公钥，而是返回一个证书；
说明：各大浏览器和操作系统已经维护了所有的权威证书机构的名称和公钥。B只需要知道是哪个权威机构发的证书，使用对应的机构公钥，就可以解密出证书签名；接下来，B使用同样的规则，生成自己的证书签名，如果两个签名是一致的，说明证书是有效的；
签名验证成功后，B就可以再次利用机构的公钥，解密出A的公钥key1;接下来的操作，就是和之前一样的流程了；

#### 中间人是否会拦截发送假证书到B呢？

因为证书的签名是由服务器端网址等信息生成的，并且通过第三方机构的私钥加密中间人无法篡改； 所以最关键的问题是证书签名的真伪；

https主要的思想是在http基础上增加了ssl安全层，即以上认证过程；



### TCP三次握手和四次挥手

三次握手之所以是三次是保证client和server均让对方知道自己的接收和发送能力没问题而保证的最小次数。

第一次client => server 只能server判断出client具备发送能力
第二次 server => client client就可以判断出server具备发送和接受能力。此时client还需让server知道自己接收能力没问题于是就有了第三次
第三次 client => server 双方均保证了自己的接收和发送能力没有问题

其中，为了保证后续的握手是为了应答上一个握手，每次握手都会带一个标识 seq，后续的ACK都会对这个seq进行加一来进行确认。



### img iframe script来发送跨域请求有什么优缺点？

iframe
优点：跨域完毕之后DOM操作和互相之间的JavaScript调用都是没有问题的

缺点：1.若结果要以URL参数传递，这就意味着在结果数据量很大的时候需要分割传递，巨烦。2.还有一个是iframe本身带来的，母页面和iframe本身的交互本身就有安全性限制。

script
优点：可以直接返回json格式的数据，方便处理

缺点：只接受GET请求方式

图片ping
优点：可以访问任何url，一般用来进行点击追踪，做页面分析常用的方法

缺点：不能访问响应文本，只能监听是否响应



### http和https的区别？

http传输的数据都是未加密的，也就是明文的，网景公司设置了SSL协议来对http协议传输的数据进行加密处理，简单来说https协议是由http和ssl协议构建的可进行加密传输和身份认证的网络协议，比http协议的安全性更高。 主要的区别如下：

Https协议需要ca证书，费用较高。
http是超文本传输协议，信息是明文传输，https则是具有安全性的ssl加密传输协议。
使用不同的链接方式，端口也不同，一般而言，http协议的端口为80，https的端口为443
http的连接很简单，是无状态的；HTTPS协议是由SSL+HTTP协议构建的可进行加密传输、身份认证的网络协议，比http协议安全。



### Cookie、sessionStorage、localStorage的区别

共同点：都是保存在浏览器端，并且是同源的

#### Cookie：

cookie数据始终在同源的http请求中携带（即使不需要），即cookie在浏览器和服务器间来回传递。而sessionStorage和localStorage不会自动把数据发给服务器，仅在本地保存。cookie数据还有路径（path）的概念，可以限制cookie只属于某个路径下,存储的大小很小只有4K左右。 （key：可以在浏览器和服务器端来回传递，存储容量小，只有大约4K左右）

#### sessionStorage：

仅在当前浏览器窗口关闭前有效，自然也就不可能持久保持，localStorage：始终有效，窗口或浏览器关闭也一直保存，因此用作持久数据；cookie只在设置的cookie过期时间之前一直有效，即使窗口或浏览器关闭。（key：本身就是一个回话过程，关闭浏览器后消失，session为一个回话，当页面不同即使是同一页面打开两次，也被视为同一次回话）

#### localStorage：

localStorage 在所有同源窗口中都是共享的；cookie也是在所有同源窗口中都是共享的。（key：同源窗口都会共享，并且不会失效，不管窗口或者浏览器关闭与否都会始终生效）

#### 补充说明一下cookie的作用：

保存用户登录状态。例如将用户id存储于一个cookie内，这样当用户下次访问该页面时就不需要重新登录了，现在很多论坛和社区都提供这样的功能。 cookie还可以设置过期时间，当超过时间期限后，cookie就会自动消失。因此，系统往往可以提示用户保持登录状态的时间：常见选项有一个月、三个 月、一年等。
跟踪用户行为。例如一个天气预报网站，能够根据用户选择的地区显示当地的天气情况。如果每次都需要选择所在地是烦琐的，当利用了 cookie后就会显得很人性化了，系统能够记住上一次访问的地区，当下次再打开该页面时，它就会自动显示上次用户所在地区的天气情况。因为一切都是在后 台完成，所以这样的页面就像为某个用户所定制的一样，使用起来非常方便
定制页面。如果网站提供了换肤或更换布局的功能，那么可以使用cookie来记录用户的选项，例如：背景色、分辨率等。当用户下次访问时，仍然可以保存上一次访问的界面风格。



### Cookie如何防范XSS攻击

XSS（跨站脚本攻击）是指攻击者在返回的HTML中嵌入javascript脚本，为了减轻这些攻击，需要在HTTP头部配上，set-cookie：

httponly-这个属性可以防止XSS,它会禁止javascript脚本来访问cookie。
secure - 这个属性告诉浏览器仅在请求为https的时候发送cookie。
结果应该是这样的：Set-Cookie=.....



### 浏览器和 Node 事件循环的区别？

其中一个主要的区别在于浏览器的event loop 和nodejs的event loop 在处理异步事件的顺序是不同的,nodejs中有micro event;其中Promise属于micro event 该异步事件的处理顺序就和浏览器不同.nodejs V11.0以上 这两者之间的顺序就相同了.

```
function test () \\{
   console.log('start')
    setTimeout(() => \\{
        console.log('children2')
        Promise.resolve().then(() => \\{console.log('children2-1')\\})
    \\}, 0)
    setTimeout(() => \\{
        console.log('children3')
        Promise.resolve().then(() => \\{console.log('children3-1')\\})
    \\}, 0)
    Promise.resolve().then(() => \\{console.log('children1')\\})
    console.log('end') 
\\}

test()
```

// 以上代码在node11以下版本的执行结果(先执行所有的宏任务，再执行微任务)
// start
// end
// children1
// children2
// children3
// children2-1
// children3-1

// 以上代码在node11及浏览器的执行结果(顺序执行宏任务和微任务)
// start
// end
// children1
// children2
// children2-1
// children3
// children3-1



### 简述HTTPS中间人攻击

https协议由 http + ssl 协议构成，具体的链接过程可参考SSL或TLS握手的概述

#### 中间人攻击过程如下：

服务器向客户端发送公钥。
攻击者截获公钥，保留在自己手上。
然后攻击者自己生成一个【伪造的】公钥，发给客户端。
客户端收到伪造的公钥后，生成加密hash值发给服务器。
攻击者获得加密hash值，用自己的私钥解密获得真秘钥。
同时生成假的加密hash值，发给服务器。
服务器用私钥解密获得假秘钥。
服务器用加秘钥加密传输信息

#### 防范方法：

服务端在发送浏览器的公钥中加入CA证书，浏览器可以验证CA证书的有效性



### 说几条web前端优化策略

(1). 减少HTTP请求数

这条策略基本上所有前端人都知道，而且也是最重要最有效的。都说要减少HTTP请求，那请求多了到底会怎么样呢？首先，每个请求都是有成本的，既包 含时间成本也包含资源成本。一个完整的请求都需要经过DNS寻址、与服务器建立连接、发送数据、等待服务器响应、接收数据这样一个“漫长”而复杂的过程。 时间成本就是用户需要看到或者“感受”到这个资源是必须要等待这个过程结束的，资源上由于每个请求都需要携带数据，因此每个请求都需要占用带宽。

另外，由于浏览器进行并发请求的请求数是有上限的，因此请求数多了以后，浏览器需要分批进行请求，因此会增加用户的等待时间，会给 用户造成站点速度慢这样一个印象，即使可能用户能看到的第一屏的资源都已经请求完了，但是浏览器的进度条会一直存在。减少HTTP请求数的主要途径包括：

(2). 从设计实现层面简化页面

如果你的页面像百度首页一样简单，那么接下来的规则基本上都用不着了。保持页面简洁、减少资源的使用时最直接的。如果不是这样，你的页面需要华丽的皮肤，则继续阅读下面的内容。

(3). 合理设置HTTP缓存

缓存的力量是强大的，恰当的缓存设置可以大大的减少HTTP请求。以有啊首页为例，当浏览器没有缓存的时候访问一共会发出78个请求，共600多K 数据（如图1.1），而当第二次访问即浏览器已缓存之后访问则仅有10个请求，共20多K数据（如图1.2）。（这里需要说明的是，如果直接F5刷新页面 的话效果是不一样的，这种情况下请求数还是一样，不过被缓存资源的请求服务器是304响应，只有Header没有Body，可以节省带宽）

怎样才算合理设置？原则很简单，能缓存越多越好，能缓存越久越好。例如，很少变化的图片资源可以直接通过HTTP Header中的Expires设置一个很长的过期头；变化不频繁而又可能会变的资源可以使用Last-Modifed来做请求验证。尽可能的让资源能够 在缓存中待得更久。

(4). 资源合并与压缩

如果可以的话，尽可能的将外部的脚本、样式进行合并，多个合为一个。另外，CSS、Javascript、Image都可以用相应的工具进行压缩，压缩后往往能省下不少空间。

(5). CSS Sprites

合并CSS图片，减少请求数的又一个好办法。

(6). Inline Images

使用data: URL scheme的方式将图片嵌入到页面或CSS中，如果不考虑资源管理上的问题的话，不失为一个好办法。如果是嵌入页面的话换来的是增大了页面的体积，而且无法利用浏览器缓存。使用在CSS中的图片则更为理想一些。

(7). Lazy Load Images

这条策略实际上并不一定能减少HTTP请求数，但是却能在某些条件下或者页面刚加载时减少HTTP请求数。对于图片而言，在页面刚加载的时候可以只 加载第一屏，当用户继续往后滚屏的时候才加载后续的图片。这样一来，假如用户只对第一屏的内容感兴趣时，那剩余的图片请求就都节省了。有啊首页曾经的做法 是在加载的时候把第一屏之后的图片地址缓存在Textarea标签中，待用户往下滚屏的时候才“惰性”加载。



### 你了解的浏览器的重绘和回流导致的性能问题

重绘（Repaint）和回流（Reflow）

重绘和回流是渲染步骤中的一小节，但是这两个步骤对于性能影响很大。

重绘是当节点需要更改外观而不会影响布局的，比如改变 color就叫称为重绘
回流是布局或者几何属性需要改变就称为回流。
回流必定会发生重绘，重绘不一定会引发回流。回流所需的成本比重绘高的多，改变深层次的节点很可能导致父节点的一系列回流。

所以以下几个动作可能会导致性能问题：

- 改变 window 大小
- 改变字体
- 添加或删除样式
- 文字改变
- 定位或者浮动
- 盒模型

很多人不知道的是，重绘和回流其实和 Event loop 有关。

当 Event loop 执行完 Microtasks 后，会判断 document 是否需要更新。因为浏览器是 60Hz 的刷新率，每 16ms 才会更新一次。
然后判断是否有 resize或者 scroll，有的话会去触发事件，所以 resize和 scroll事件也是至少 16ms 才会触发一次，并且自带节流功能。
判断是否触发了 media query
更新动画并且发送事件
判断是否有全屏操作事件
执行 requestAnimationFrame回调
执行 IntersectionObserver回调，该方法用于判断元素是否可见，可以用于懒加载上，但是兼容性不好
更新界面
以上就是一帧中可能会做的事情。如果在一帧中有空闲时间，就会去执行 requestIdleCallback回调。
减少重绘和回流

使用 translate 替代 top

```
<div class="test"></div>
<style>
    .test \\{
        position: absolute;
        top: 10px;
        width: 100px;
        height: 100px;
        background: red;
    \\}
</style>
<script>
    setTimeout(() => \\{
        // 引起回流
        document.querySelector('.test').style.top = '100px'
    \\}, 1000)
</script>
```

使用 visibility替换 display: none，因为前者只会引起重绘，后者会引发回流（改变了布局）

把 DOM 离线后修改，比如：先把 DOM 给 display:none(有一次 Reflow)，然后你修改100次，然后再把它显示出来

不要把 DOM 结点的属性值放在一个循环里当成循环里的变量

```
for(let i = 0; i < 1000; i++) \\{
    // 获取 offsetTop 会导致回流，因为需要去获取正确的值
    console.log(document.querySelector('.test').style.offsetTop)
\\}
```

不要使用 table 布局，可能很小的一个小改动会造成整个 table 的重新布局
动画实现的速度的选择，动画速度越快，回流次数越多，也可以选择使用 requestAnimationFrame
CSS 选择符从右往左匹配查找，避免 DOM 深度过深
将频繁运行的动画变为图层，图层能够阻止该节点回流影响别的元素。比如对于 video标签，浏览器会自动将该节点变为图层。



## react、Vue

### 写 React / Vue 项目时为什么要在列表组件中写 key，其作用是什么？

vue和react都是采用diff算法来对比新旧虚拟节点，从而更新节点。在vue的diff函数中（建议先了解一下diff算法过程）。
在交叉对比中，当新节点跟旧节点头尾交叉对比没有结果时，会根据新节点的key去对比旧节点数组中的key，从而找到相应旧节点（这里对应的是一个key => index 的map映射）。如果没找到就认为是一个新增节点。而如果没有key，那么就会采用遍历查找的方式去找到对应的旧节点。一种一个map映射，另一种是遍历查找。相比而言。map映射的速度更快。
vue部分源码如下：

```
// vue项目  src/core/vdom/patch.js  -488行
// 以下是为了阅读性进行格式化后的代码

// oldCh 是一个旧虚拟节点数组
if (isUndef(oldKeyToIdx)) \\{
  oldKeyToIdx = createKeyToOldIdx(oldCh, oldStartIdx, oldEndIdx)
\\}
if(isDef(newStartVnode.key)) \\{
  // map 方式获取
  idxInOld = oldKeyToIdx[newStartVnode.key]
\\} else \\{
  // 遍历方式获取
  idxInOld = findIdxInOld(newStartVnode, oldCh, oldStartIdx, oldEndIdx)
\\}
创建map函数

function createKeyToOldIdx (children, beginIdx, endIdx) \\{
  let i, key
  const map = \\{\\}
  for (i = beginIdx; i <= endIdx; ++i) \\{
    key = children[i].key
    if (isDef(key)) map[key] = i
  \\}
  return map
\\}
遍历寻找

// sameVnode 是对比新旧节点是否相同的函数
 function findIdxInOld (node, oldCh, start, end) \\{
    for (let i = start; i < end; i++) \\{
      const c = oldCh[i]
      if (isDef(c) && sameVnode(node, c)) return i
    \\}

  \\}
```



### React 中 setState 什么时候是同步的，什么时候是异步的？

在React中，如果是由React引发的事件处理（比如通过onClick引发的事件处理），调用setState不会同步更新this.state，除此之外的setState调用会同步执行this.state。所谓“除此之外”，指的是绕过React通过addEventListener直接添加的事件处理函数，还有通过setTimeout/setInterval产生的异步调用。

原因：在React的setState函数实现中，会根据一个变量isBatchingUpdates判断是直接更新this.state还是放到队列中回头再说，而isBatchingUpdates默认是false，也就表示setState会同步更新this.state，但是，有一个函数batchedUpdates，这个函数会把isBatchingUpdates修改为true，而当React在调用事件处理函数之前就会调用这个batchedUpdates，造成的后果，就是由React控制的事件处理过程setState不会同步更新this.state。



### 下面输出什么

```
class Example extends React.Component \\{
  constructor() \\{
    super();
    this.state = \\{
      val: 0
    \\};
  \\}

  componentDidMount() \\{
    this.setState(\\{val: this.state.val + 1\\});
    console.log(this.state.val);    // 第 1 次 log

    this.setState(\\{val: this.state.val + 1\\});
    console.log(this.state.val);    // 第 2 次 log

    setTimeout(() => \\{
      this.setState(\\{val: this.state.val + 1\\});
      console.log(this.state.val);  // 第 3 次 log

      this.setState(\\{val: this.state.val + 1\\});
      console.log(this.state.val);  // 第 4 次 log
    \\}, 0);

  \\}

  render() \\{
    return null;
  \\}
\\};
```


1、第一次和第二次都是在 react 自身生命周期内，触发时 isBatchingUpdates 为 true，所以并不会直接执行更新 state，而是加入了 dirtyComponents，所以打印时获取的都是更新前的状态 0。

2、两次 setState 时，获取到 this.state.val 都是 0，所以执行时都是将 0 设置成 1，在 react 内部会被合并掉，只执行一次。设置完成后 state.val 值为 1。

3、setTimeout 中的代码，触发时 isBatchingUpdates 为 false，所以能够直接进行更新，所以连着输出 2，3。

输出： 0 0 2 3



### 为什么虚拟dom会提高性能?

虚拟dom相当于在js和真实dom中间加了一个缓存，利用dom diff算法避免了没有必要的dom操作，从而提高性能。

具体实现步骤如下：

用 JavaScript 对象结构表示 DOM 树的结构；然后用这个树构建一个真正的 DOM 树，插到文档当中

当状态变更的时候，重新构造一棵新的对象树。然后用新的树和旧的树进行比较，记录两棵树差异

把2所记录的差异应用到步骤1所构建的真正的DOM树上，视图就更新了。



## css

### 分析比较 opacity: 0、visibility: hidden、display: none 优劣和适用场景

结构：
display:none: 会让元素完全从渲染树中消失，渲染的时候不占据任何空间, 不能点击，
visibility: hidden:不会让元素从渲染树消失，渲染元素继续占据空间，只是内容不可见，不能点击
opacity: 0: 不会让元素从渲染树消失，渲染元素继续占据空间，只是内容不可见，可以点击

继承：
display: none和opacity: 0：是非继承属性，子孙节点消失由于元素从渲染树消失造成，通过修改子孙节点属性无法显示。
visibility: hidden：是继承属性，子孙节点消失由于继承了hidden，通过设置visibility: visible;可以让子孙节点显式。

性能：
displaynone : 修改元素会造成文档回流,读屏器不会读取display: none元素内容，性能消耗较大
visibility:hidden: 修改元素只会造成本元素的重绘,性能消耗较少读屏器读取visibility: hidden元素内容
opacity: 0 ： 修改元素会造成重绘，性能消耗较少

联系：它们都能让元素不可见



### 清除浮动的方式有哪些?比较好的是哪一种?

常用的一般为三种.clearfix, clear:both,overflow:hidden;

比较好是 .clearfix,伪元素万金油版本,后两者有局限性.

```
.clearfix:after \\{
  visibility: hidden;
  display: block;
  font-size: 0;
  content: " ";
  clear: both;
  height: 0;
\\}

<!--
为毛没有 zoom ,_height 这些,IE6,7这类需要 csshack 不再我们考虑之内了
.clearfix 还有另外一种写法,
-->

.clearfix:before, .clearfix:after \\{
    content:"";
    display:table;
\\}
.clearfix:after\\{
    clear:both;
    overflow:hidden;
\\}
.clearfix\\{
    zoom:1;
\\}

<!--
用display:table 是为了避免外边距margin重叠导致的margin塌陷,
内部元素默认会成为 table-cell 单元格的形式
-->
```

clear:both:若是用在同一个容器内相邻元素上,那是贼好的,有时候在容器外就有些问题了, 比如相邻容器的包裹层元素塌陷

overflow:hidden:这种若是用在同个容器内,可以形成 BFC避免浮动造成的元素塌陷



### css sprite 是什么,有什么优缺点

概念：

将多个小图片拼接到一个图片中。通过 background-position 和元素尺寸调节需要显示的背景图案。

优点：

减少 HTTP 请求数，极大地提高页面加载速度
增加图片信息重复度，提高压缩比，减少图片大小
更换风格方便，只需在一张或几张图片上修改颜色或样式即可实现

缺点：

图片合并麻烦
维护麻烦，修改一个图片可能需要重新布局整个图片，样式



### link与@import的区别

link是 HTML 方式， @import是 CSS 方式
link最大限度支持并行下载，@import过多嵌套导致串行下载，出现FOUC
link可以通过rel="alternate stylesheet"指定候选样式
浏览器对link支持早于@import，可以使用@import对老浏览器隐藏样式
@import必须在样式规则之前，可以在 css 文件中引用其他文件
总体来说：link 优于@import



### display: block;和display: inline;的区别

#### block元素特点：

1.处于常规流中时，如果width没有设置，会自动填充满父容器

2.可以应用margin/padding

3.在没有设置高度的情况下会扩展高度以包含常规流中的子元素

4.处于常规流中时布局时在前后元素位置之间（独占一个水平空间）

5.忽略vertical-align

#### inline元素特点

1.水平方向上根据direction依次布局

2.不会在元素前后进行换行

3.受white-space控制

4.margin/padding在竖直方向上无效，水平方向上有效

5.width/height属性对非替换行内元素无效，宽度由元素内容决定

6.非替换行内元素的行框高由line-height确定，替换行内元素的行框高由height,margin,padding,border决定 

7.浮动或绝对定位时会转换为block 

8.vertical-align属性生效



### 容器包含若干浮动元素时如何清理浮动

容器元素闭合标签前添加额外元素并设置clear: both
父元素触发块级格式化上下文(见块级可视化上下文部分)
设置容器元素伪元素进行清理推荐的清理浮动方法

```
/**
* 在标准浏览器下使用
* 1 content内容为空格用于修复opera下文档中出现
* contenteditable属性时在清理浮动元素上下的空白
* 2 使用display使用table而不是block：可以防止容器和
* 子元素top-margin折叠,这样能使清理效果与BFC，IE6/7
* zoom: 1;一致
**/

.clearfix:before,
.clearfix:after \\{
    content: " "; /* 1 */
    display: table; /* 2 */
\\}

.clearfix:after \\{
    clear: both;
\\}

/**
IE 6/7下使用
通过触发hasLayout实现包含浮动
**/
.clearfix \\{
  *zoom: 1;
\\}
```



### PNG,GIF,JPG 的区别及如何选

#### GIF:

8 位像素，256 色
无损压缩
支持简单动画
支持 boolean 透明
适合简单动画

#### JPEG：

颜色限于 256
有损压缩
可控制压缩质量
不支持透明
适合照片

#### PNG：

有 PNG8 和 truecolor PNG
PNG8 类似 GIF 颜色上限为 256，文件小，支持 alpha 透明度，无动画
适合图标、背景、按钮



### display,float,position 的关系

如果display为 none，那么 position 和 float 都不起作用，这种情况下元素不产生框
否则，如果 position 值为 absolute 或者 fixed，框就是绝对定位的，float 的计算值为 none，display 根据下面的表格进行调整。
否则，如果 float 不是 none，框是浮动的，display 根据下表进行调整
否则，如果元素是根元素，display 根据下表进行调整
其他情况下 display 的值为指定值 总结起来：绝对定位、浮动、根元素都需要调整display



### 如何水平居中一个元素

如果需要居中的元素为常规流中 inline 元素，为父元素设置text-align: center;即可实现
如果需要居中的元素为常规流中 block 元素，1）为元素设置宽度，2）设置左右 margin 为 auto。3）IE6 下需在父元素上设置text-align: center;,再给子元素恢复需要的值


    <body>
        <div class="content">
        aaaaaa aaaaaa a a a a a a a a
        </div>
    </body>
        
    <style>
        body \\{
            background: #DDD;
            text-align: center; /* 3 */
        \\}
        .content \\{
            width: 500px;      /* 1 */
            text-align: left;  /* 3 */
            margin: 0 auto;    /* 2 */
        	background: purple;
    	\\}
    </style>

如果需要居中的元素为浮动元素，1）为元素设置宽度，2）position: relative;，3）浮动方向偏移量（left 或者 right）设置为 50\\%，4）浮动方向上的 margin 设置为元素宽度一半乘以-1


    <body>
        <div class="content">
        aaaaaa aaaaaa a a a a a a a a
        </div>
    </body>
    
    <style>
        body \\{
            background: #DDD;
        \\}
        .content \\{
            width: 500px;         /* 1 */
            float: left;
            position: relative;   /* 2 */
            left: 50\\%;            /* 3 */
            margin-left: -250px;  /* 4 */
            background-color: purple;
        \\}
    </style>
如果需要居中的元素为绝对定位元素，1）为元素设置宽度，2）偏移量设置为 50\\%，3）偏移方向外边距设置为元素宽度一半乘以-1

```
<body>
    <div class="content">
    aaaaaa aaaaaa a a a a a a a a
    </div>
</body>

<style>
    body \\{
        background: #DDD;
        position: relative;
    \\}
    .content \\{
        width: 800px;
        position: absolute;
        left: 50\\%;
        margin-left: -400px;
        background-color: purple;
    \\}
</style>
```


如果需要居中的元素为绝对定位元素，1）为元素设置宽度，2）设置左右偏移量都为 0,3）设置左右外边距都为 auto


    <body>
        <div class="content">
        aaaaaa aaaaaa a a a a a a a a
        </div>
    </body>
    
    <style>
        body \\{
            background: #DDD;
            position: relative;
        \\}
        .content \\{
            width: 800px;
            position: absolute;
            margin: 0 auto;
            left: 0;
            right: 0;
            background-color: purple;
        \\}
    </style>


### Promise 构造函数是同步执行还是异步执行，那么 then 方法呢？

```
const promise = new Promise((resolve, reject) => \\{
  console.log(1)
  resolve()
  console.log(2)
\\})

promise.then(() => \\{
  console.log(3)
\\})

console.log(4)
```


输出结果是：

1
2
4
3
promise构造函数是同步执行的，then方法是异步执行的
Promise new的时候会立即执行里面的代码

then是微任务 会在本次任务执行完的时候执行

setTimeout是宏任务 会在下次任务执行的时候执行



### JS的四种设计模式

#### 工厂模式

简单的工厂模式可以理解为解决多个相似的问题;

```
function CreatePerson(name,age,sex) \\{
    var obj = new Object();
    obj.name = name;
    obj.age = age;
    obj.sex = sex;
    obj.sayName = function()\\{
        return this.name;
    \\}
    return obj;
\\}
var p1 = new CreatePerson("longen",'28','男');
var p2 = new CreatePerson("tugenhua",'27','女');
console.log(p1.name); // longen
console.log(p1.age);  // 28
console.log(p1.sex);  // 男
console.log(p1.sayName()); // longen

console.log(p2.name);  // tugenhua
console.log(p2.age);   // 27
console.log(p2.sex);   // 女
console.log(p2.sayName()); // tugenhua  
```

#### 单例模式

只能被实例化(构造函数给实例添加属性与方法)一次

```
// 单体模式
var Singleton = function(name)\\{
    this.name = name;
\\};
Singleton.prototype.getName = function()\\{
    return this.name;
\\}
// 获取实例对象
var getInstance = (function() \\{
    var instance = null;
    return function(name) \\{
        if(!instance) \\{//相当于一个一次性阀门,只能实例化一次
            instance = new Singleton(name);
        \\}
        return instance;
    \\}
\\})();
// 测试单体模式的实例,所以a===b
var a = getInstance("aa");
var b = getInstance("bb");  
```

#### 沙箱模式

将一些函数放到自执行函数里面,但要用闭包暴露接口,用变量接收暴露的接口,再调用里面的值,否则无法使用里面的值

```
let sandboxModel=(function()\\{
    function sayName()\\{\\};
    function sayAge()\\{\\};
    return\\{
        sayName:sayName,
        sayAge:sayAge
    \\}
\\})()
```

#### 发布者订阅模式

就例如如我们关注了某一个公众号,然后他对应的有新的消息就会给你推送,

    //发布者与订阅模式
    var shoeObj = \\{\\}; // 定义发布者
    shoeObj.list = []; // 缓存列表 存放订阅者回调函数
    
    // 增加订阅者
    shoeObj.listen = function(fn) \\{
        shoeObj.list.push(fn); // 订阅消息添加到缓存列表
    \\}
     
    // 发布消息
    shoeObj.trigger = function() \\{
        for (var i = 0, fn; fn = this.list[i++];) \\{
        	fn.apply(this, arguments);//第一个参数只是改变fn的this,
        \\}
    \\}
     // 小红订阅如下消息
    shoeObj.listen(function(color, size) \\{
        console.log("颜色是：" + color);
        console.log("尺码是：" + size);
    \\});
     
    // 小花订阅如下消息
    shoeObj.listen(function(color, size) \\{
        console.log("再次打印颜色是：" + color);
        console.log("再次打印尺码是：" + size);
    \\});
    shoeObj.trigger("红色", 40);
    shoeObj.trigger("黑色", 42);  
代码实现逻辑是用数组存贮订阅者, 发布者回调函数里面通知的方式是遍历订阅者数组,并将发布者内容传入订阅者数组



### 列举出集中创建实例的方法

1.字面量

```
let obj=\\{'name':'张三'\\}
```


2.Object构造函数创建

```
let Obj=new Object()
Obj.name='张三'
```


3.使用工厂模式创建对象

```
function createPerson(name)\\{
 var o = new Object();
 o.name = name;
 \\};
 return o; 
\\}
var person1 = createPerson('张三');
```


4.使用构造函数创建对象

```
function Person(name)\\{
 this.name = name;
\\}
var person1 = new Person('张三');
```



### 简述一下前端事件流

HTML中与javascript交互是通过事件驱动来实现的，例如鼠标点击事件onclick、页面的滚动事件onscroll等等，可以向文档或者文档中的元素添加事件侦听器来预订事件。想要知道这些事件是在什么时候进行调用的，就需要了解一下“事件流”的概念。

什么是事件流：事件流描述的是从页面中接收事件的顺序,DOM2级事件流包括下面几个阶段。

事件捕获阶段
处于目标阶段
事件冒泡阶段
addEventListener：addEventListener是DOM2 级事件新增的指定事件处理程序的操作，这个方法接收3个参数：要处理的事件名、作为事件处理程序的函数和一个布尔值。最后这个布尔值参数如果是true，表示在捕获阶段调用事件处理程序；如果是false，表示在冒泡阶段调用事件处理程序。

IE只支持事件冒泡。



### Function._proto_(getPrototypeOf)是什么？

获取一个对象的原型，在chrome中可以通过__proto__的形式，或者在ES6中可以通过Object.getPrototypeOf的形式。

那么Function.proto是什么么？也就是说Function由什么对象继承而来，我们来做如下判别。

```
Function.__proto__==Object.prototype //false
Function.__proto__==Function.prototype//true
```


我们发现Function的原型也是Function。

我们用图可以来明确这个关系：



### 简述一下原型 / 构造函数 / 实例

原型(prototype): 一个简单的对象，用于实现对象的 属性继承。可以简单的理解成对象的爹。在 Firefox 和 Chrome 中，每个JavaScript对象中都包含一个__proto__(非标准)的属性指向它爹(该对象的原型)，可obj.__proto__进行访问。
构造函数: 可以通过new来 新建一个对象的函数。
实例: 通过构造函数和new创建出来的对象，便是实例。 实例通过__proto__指向原型，通过constructor指向构造函数。
这里来举个栗子，以Object为例，我们常用的Object便是一个构造函数，因此我们可以通过它构建实例。

```
// 实例
const instance = new Object()
```


则此时， 实例为instance, 构造函数为Object，我们知道，构造函数拥有一个prototype的属性指向原型，因此原型为:

```
// 原型
const prototype = Object.prototype
```


这里我们可以来看出三者的关系:

实例.__proto__ === 原型

原型.constructor === 构造函数

构造函数.prototype === 原型

```
// 这条线其实是是基于原型进行获取的，可以理解成一条基于原型的映射线
// 例如: 
// const o = new Object()
// o.constructor === Object   --> true
// o.__proto__ = null;
// o.constructor === Object   --> false
```

实例.constructor === 构造函数



### 简述一下JS继承，并举例

在 JS 中，继承通常指的便是 原型链继承，也就是通过指定原型，并可以通过原型链继承原型上的属性或者方法。

最优化: 圣杯模式

```
var inherit = (function(c,p)\\{
    var F = function()\\{\\};
    return function(c,p)\\{
        F.prototype = p.prototype;
        c.prototype = new F();
        c.uber = p.prototype;
        c.prototype.constructor = c;
    \\}
\\})();
```

使用 ES6 的语法糖 class / extends



### 函数柯里化

在函数式编程中，函数是一等公民。那么函数柯里化是怎样的呢？

函数柯里化指的是将能够接收多个参数的函数转化为接收单一参数的函数，并且返回接收余下参数且返回结果的新函数的技术。

函数柯里化的主要作用和特点就是参数复用、提前返回和延迟执行。

在一个函数中，首先填充几个参数，然后再返回一个新的函数的技术，称为函数的柯里化。通常可用于在不侵入函数的前提下，为函数 预置通用参数，供多次重复调用。

```
const add = function add(x) \\{
    return function (y) \\{
        return x + y
    \\}
\\}

const add1 = add(1)

add1(2) === 3
add1(20) === 21
```



### 说说bind、call、apply 区别？

call 和 apply 都是为了解决改变 this 的指向。作用都是相同的，只是传参的方式不同。

除了第一个参数外，call 可以接收一个参数列表，apply 只接受一个参数数组。

```
let a = \\{
    value: 1
\\}
function getValue(name, age) \\{
    console.log(name)
    console.log(age)
    console.log(this.value)
\\}
getValue.call(a, 'yck', '24')
getValue.apply(a, ['yck', '24'])
```


bind和其他两个方法作用也是一致的，只是该方法会返回一个函数。并且我们可以通过 bind实现柯里化。

（下面是对这三个方法的扩展介绍）

如何实现一个 bind 函数

对于实现以下几个函数，可以从几个方面思考

不传入第一个参数，那么默认为 window
改变了 this 指向，让新的对象可以执行该函数。那么思路是否可以变成给新的对象添加一个函数，然后在执行完以后删除？

```
Function.prototype.myBind = function (context) \\{
  if (typeof this !== 'function') \\{
    throw new TypeError('Error')
  \\}
  var _this = this
  var args = [...arguments].slice(1)
  // 返回一个函数
  return function F() \\{
    // 因为返回了一个函数，我们可以 new F()，所以需要判断
    if (this instanceof F) \\{
      return new _this(...args, ...arguments)
    \\}
    return _this.apply(context, args.concat(...arguments))
  \\}
\\}
```

如何实现一个call函数

```
Function.prototype.myCall = function (context) \\{
  var context = context || window
  // 给 context 添加一个属性
  // getValue.call(a, 'yck', '24') => a.fn = getValue
  context.fn = this
  // 将 context 后面的参数取出来
  var args = [...arguments].slice(1)
  // getValue.call(a, 'yck', '24') => a.fn('yck', '24')
  var result = context.fn(...args)
  // 删除 fn
  delete context.fn
  return result
\\}
```


如何实现一个apply函数

```
Function.prototype.myApply = function (context) \\{
  var context = context || window
  context.fn = this

  var result
  // 需要判断是否存储第二个参数
  // 如果存在，就将第二个参数展开
  if (arguments[1]) \\{
    result = context.fn(...arguments[1])
  \\} else \\{
    result = context.fn()
  \\}

  delete context.fn
  return result
\\}
```



### 箭头函数的特点

```
function a() \\{
    return () => \\{
        return () => \\{
            console.log(this)
        \\}
    \\}
\\}
console.log(a()()())
```

箭头函数其实是没有 this的，这个函数中的 this只取决于他外面的第一个不是箭头函数的函数的 this。

在这个例子中，因为调用a符合前面代码中的第一个情况，所以 this是 window。并且 this一旦绑定了上下文，就不会被任何代码改变。



### 谈谈你对 dns-prefetch 的理解

DNS 是什么-- Domain Name System，域名系统，作为域名和IP地址相互映射的一个分布式数据库。

#### DNS Prefetching

浏览器根据自定义的规则，提前去解析后面可能用到的域名，来加速网站的访问速度。简单来讲就是提前解析域名，以免延迟。

#### 使用方式

```
<link rel="dns-prefetch" href="//wq.test.com">
```

这个功能有个默认加载条件，所有的a标签的href都会自动去启用DNS Prefetching，也就是说，你网页的a标签href带的域名，是不需要在head里面加上link手动设置的。但a标签的默认启动在HTTPS不起作用。

这时要使用 meta里面http-equiv来强制启动功能。

```
<meta http-equiv="x-dns-prefetch-control" content="on">
```

#### 总结一下

1. DNS Prefetching是提前加载域名解析的，省去了解析时间。a标签的href是可以在chrome。firefox包括高版本的IE，但是在HTTPS下面不起作用，需要meta来强制开启功能
2. 这是DNS的提前解析，并不是css，js之类的文件缓存，大家不要混淆了两个不同的概念。
3. 如果直接做了js的重定向，或者在服务端做了重定向，没有在link里面手动设置，是不起作用的。
4. 这个对于什么样的网站更有作用呢，类似taobao这种网站，你的网页引用了大量很多其他域名的资源，如果你的网站，基本所有的资源都在你本域名下，那么这个基本没有什么作用。因为DNS Chrome在访问你的网站就帮你缓存了。

#### 拓展知识学习

- web下的性能优化1(网络方向)



### get/post请求传参长度有什么特点

我们经常说get请求参数的大小存在限制，而post请求的参数大小是无限制的。这是一个错误的说法，实际上HTTP 协议从未规定 GET/POST 的请求长度限制是多少。对get请求参数的限制是来源与浏览器或web服务器，浏览器或web服务器限制了url的长度。为了明确这个概念，我们必须再次强调下面几点:

1. HTTP 协议 未规定 GET 和POST的长度限制
2. GET的最大长度显示是因为 浏览器和 web服务器限制了 URI的长度
3. 不同的浏览器和WEB服务器，限制的最大长度不一样
4. 要支持IE，则最大长度为2083byte，若只支持Chrome，则最大长度 8182byte



### 前端需要注意哪些 SEO

1. 合理的 title、description、keywords：搜索对着三项的权重逐个减小，title 值强调重点即可，重要关键词出现不要超过 2 次，而且要靠前，不同页面 title 要有所不同；description 把页面内容高度概括，长度合适，不可过分堆砌关键词，不同页面 description 有所不同；keywords 列举出重要关键词即可
2. 语义化的 HTML 代码，符合 W3C 规范：语义化代码让搜索引擎容易理解网页
3. 重要内容 HTML 代码放在最前：搜索引擎抓取 HTML 顺序是从上到下，有的搜索引擎对抓取长度有限制，保证重要内容一定会被抓取
4. 重要内容不要用 js 输出：爬虫不会执行 js 获取内容
5. 少用 iframe(搜索引擎不会抓取 iframe 中的内容)
6. 非装饰性图片必须加 alt
7. 提高网站速度(网站速度是搜索引擎排序的一个重要指标)



### 实现一个页面操作不会整页刷新的网站，并且能在浏览器前进、后 退时正确响应。给出你的技术实现方案？

第一步，通过使用 pushState + ajax 实现浏览器无刷新前进后退，当一次 ajax 调用成功后我们将一 条 state 记录加入到 history 对象中。

第二步，一条 state 记录包含了 url、title 和 content 属性，在 popstate 事件中可以 获取到这个 state 对象，我们可 以使用 content 来传递数据。第三步，我们通过对 window.onpopstate 事件监听来响应浏览器 的前进后退操作。

使用 pushState 来实现有两个问题，一个是打开首页时没有记录，我们可以使用 replaceState 来将首页的记录替换，另一个问 题是当一个页面刷新的时候，仍然会向服务器端请求数据，因此如果请求的 url 需要后端的配 合将其重定向到一个页面。

更多参考：http://blog.chenxu.me/post/detail?id=ed4f0732-897f-48e4-9d4f-821e82f17fad



### 如何优化SPA应用的首屏加载速度慢的问题？

- 将公用的JS库通过script标签外部引入，减小app.bundel的大小，让浏览器并行下载资源文件，提高下载速度；
- 在配置 路由时，页面和组件使用懒加载的方式引入，进一步缩小 app.bundel 的体积，在调用某个组件时再加载对应的js文件；
- root中插入loading 或者 骨架屏 prerender-spa-plugin，提升用户体验；
- 如果在webview中的页面，可以进行页面预加载
- 独立打包异步组件公共 Bundle，以提高复用性&缓存命中率
- 静态文件本地缓存，有两种方式分别为HTTP缓存，设置Cache-Control，Last-Modified，Etag等响应头和Service Worker离线缓存
- 配合 PWA 使用
- SSR
- root中插入loading 或者 骨架屏 prerender-spa-plugin
- 使用 Tree Shaking 减少业务代码体积 更多参考：https://github.com/LuckyWinty/fe-weekly-questions/issues/69



### Reflect 对象创建目的？

1. 将 Object 对 象 的 一 些 明 显 属 于 语 言 内 部 的 方 法 （ 比 如 Object.defineProperty，放到 Reflect 对象上。
2. 修改某些 Object 方法的返回结果，让其变得更合理。
3. 让 Object 操作都变成函数行为。
4. Reflect 对象的方法与 Proxy 对象的方法一一对应，只要是 Proxy 对象 的方法，就能在 Reflect 对象上找到对应的方法。这就让 Proxy 对象可 以方便地调用对应的 Reflect 方法，完成默认行为，作为修改行为的基础。

也就是说，不管 Proxy 怎么修改默认行为，你总可以在 Reflect 上获取 默认行为。



### 内部属性 [[Class]] 是什么？

所有 typeof 返回值为 "object" 的对象（如数组）都包含一个内部属性 [[Class]]（我 们可以把它看作一个内部的分类，而非传统的面向对象意义上的类）。这个属性无法直接访问， 一般通过 Object.prototype.toString(..) 来查看。例如：

```
Object.prototype.toString.call( [1,2,3] );  // "[object Array]" 
Object.prototype.toString.call( /regex-literal/i ); //"[object RegExp]"
```

多数情况下，对象的内部[[class]]属性和创建该对象的内建原生构造函数相对应，不过也不总是这样。2.基本类型值的[[class]]属性

虽然Null()和Undefined()这样的原生构造函数并不存在，但是内部[[class]]属性仍然是“Null”和“Undefined”。

```
console.log(Object.prototype.toString.call(null)); //[object Null]

console.log(Object.prototype.toString.call(undefined)); //[object Undefined]
```

其他基本类型值的情况有所不同：

```
console.log(Object.prototype.toString.call("abc")); //[object String]

console.log(Object.prototype.toString.call(42));  //[object Number]

console.log(Object.prototype.toString.call(true)); //[object Boolean]
```

基本类型值被各自的封装对象自动包装，所以他们的内部[[class]]属性分别为“String”，“Number”和“Boolean”。3.封装对象

由于基本类型值没有.length和.toString()这样的属性和方法，需要通过封装对象才能访问，此时Javascript引擎会自动为基本类型值包装一个封装对象。

```
//封装对象包装

var b = 'abc';
console.log(b.length);
console.log(b.toUpperCase());
​```js
一般不直接使用封装对象（即通过new操作创建基本类型值），优先考虑使用“abc”和“42”这样的基本类型值，而不是new String("abc") 和 new Number(42)。4.拆封

如果想要得到封装对象中的基本类型值，可以使用valueOf()函数。 
​```js
//封装对象的拆封
var s = new String( "abc" );
var n = new Number( 42 );
var b = new Boolean( true );

console.log(s.valueOf());
console.log(n.valueOf());
console.log(b.valueOf());
```



### 什么是堆？什么是栈？它们之间有什么区别和联系？

堆和栈的概念存在于数据结构中和操作系统内存中。在数据结构中，栈中数据的存取方式为 先进后出。而堆是一个优先队列，是按优先级来进行排序的，优先级可以按照大小来规定。完全 二叉树是堆的一种实现方式。在操作系统中，内存被分为栈区和堆区。栈区内存由编译器自动分 配释放，存放函数的参数值，局部变量的值等。其操作方式类似于数据结构中的栈。堆区内存一 般由程序员分配释放，若程序员不释放，程序结束时可能由垃圾回收机制回收。

详细资料可以参考：《什么是堆？什么是栈？他们之间有什么区别和联系？》



### isNaN 和 Number.isNaN 函数的区别？

函数 isNaN 接收参数后，会尝试将这个参数转换为数值，任何不能被转换为数值的的值都会返 回 true，因此非数字值传入也会返回 true ，会影响 NaN 的判断。

函数 Number.isNaN 会首先判断传入参数是否为数字，如果是数字再继续判断是否为 NaN ，这种方法对于 NaN 的判断更为准确。



### 什么情况下会发生布尔值的隐式强制类型转换？

（1） if (..) 语句中的条件判断表达式。

（2） for ( .. ; .. ; .. ) 语句中的条件判断表达式（第二个）。

（3） while (..) 和 do..while(..) 循环中的条件判断表达式。

（4） ? : 中的条件判断表达式。

（5） 逻辑运算符 ||（逻辑或）和 &&（逻辑与）左边的操作数（作为条件判断表达式）。



### undefined 与 undeclared 的区别？

已在作用域中声明但还没有赋值的变量，是 undefined 的。相反，还没有在作用域中声明 过的变量，是 undeclared 的。对于 undeclared 变量的引用，浏览器会报引用错误，如 ReferenceError: b is not defined 。但是我们可以使用 typeof 的安全防范机制来避免 报错，因为对于 undeclared（或者 not defined ）变量，typeof 会返回 "undefined"。



### 如何封装一个 javascript 的类型判断函数？

```
function getType(value) \\{ 
  // 判断数据是 null 的情况 
  if (value === null) \\{ 
      return value + ""; 
  \\}
  // 判断数据是引用类型的情况 
  if (typeof value === "object") \\{ 
    let valueClass = Object.prototype.toString.call(value), 
    type = valueClass.split(" ")[1].split(""); 
    type.pop(); 
    return type.join("").toLowerCase();
  \\} else \\{ 
    // 判断数据是基本数据类型的情况和函数的情况 
    return typeof value
  \\}
\\}
```



### 小程序和公众号用什么来区分同一个用户

在微信生态中，小程序和公众号可以通过微信的 openid 和 unionid 来区分同一个用户。

 openid 是同一个应用（App、公众号、小程序）的同一个用户的唯一标识。即，一个用户在一个小程序或公众号中有唯一的 openid ，但在不同的小程序或公众号中， openid 可能不同。

 unionid 是一个用户对于同主体微信小程序、公众号、APP的标识，开发者需要在微信开放平台下绑定相同账号的主体。 unionid 在正常情况下是用户身份的唯一标识，但在业务涉及不同主体时，不一定唯一。



### 渲染函数和jsx介绍和区别

在 Vue 中，渲染函数和 JSX 都是用于构建 Vue 组件的工具。它们提供了一种编写组件的不同方式，通常用于编写更复杂、更灵活的组件。渲染函数是用 JavaScript 编写的函数，它接收一个上下文对象作为参数，然后返回一个 Vue VNode 节点。VNode 节点表示了组件的结构，包括 HTML 标记、属性、事件、样式等等。通过递归地构建 VNode 树，Vue 渲染函数可以生成最终的 DOM 树，并将其插入到文档中。渲染函数可以用于构建任何类型的组件，包括功能组件和状态组件。它通常用于编写高级别的抽象组件，例如基于数据结构的树形控件、动态表单生成器等等。渲染函数的语法相对于 JSX 较为灵活，但同时也更加复杂。

JSX 是一种在 JavaScript 中编写 HTML 标记的语法。它是 React 中广泛使用的语法，但也可以与 Vue 一起使用。JSX 允许开发者使用类似 HTML 的语法来编写组件，然后使用 Babel 等工具将其转换为常规的 JavaScript 代码。在 Vue 中使用 JSX 需要安装相应的插件，并进行配置。JSX 的语法更加简洁直观，因此更容易上手。它的表达能力也非常强，可以轻松地实现组件的复杂嵌套和逻辑控制。同时，由于 JSX 本质上是一种 JavaScript 语法扩展，因此也可以使用 JavaScript 的语言特性，例如变量、条件语句、循环等等。

总的来说，渲染函数和 JSX 在 Vue 中都有其独特的用途和优势。选择使用哪种方式取决于具体的需求和场景。



### 最近两年有什么前端新技术

近两年前端领域出现了许多新技术，其中一些比较重要的包括：

- HTML6：构建交互优良用户界面的基础技术。
- TypeScript：一种由微软开发的编程语言，具有静态类型检查功能，可以提高代码的可读性和可维护性。
- WebAssembly：一种新的二进制格式，用于在浏览器中运行高性能的代码，如视频编解码、图形渲染等。
- 渐进式 WEB 应用（PWA）：一种可以提高网站性能和用户体验的技术，允许网站在离线状态下继续运行，并提供类似于原生应用程序的功能。
- 微前端：一种软件架构，可以将前端应用拆解成一些更小的、能够独立开发部署的微型应用，然后再将这些微应用进行组合，使其成为整体应用的架构模式。

这些技术都在不同程度上推动了前端开发的发展，为用户提供了更好的体验。



### 翻书效果css使用哪个方法

你可以使用 CSS 的 rotateY 方法来实现翻书效果。该方法可以定义沿 Y 轴的 3D 旋转，从而实现翻书的效果。以下是一个示例代码：

```
.book \\{
    perspective: 800px;
    transform-style: preserve-3d;
    animation: flip 10s linear infinite;
\\}

@keyframes flip \\{
    0\\% \\{
        transform: rotateY(0deg);
    \\}
    100\\% \\{
        transform: rotateY(180deg);
    \\}
\\}
```


在上述代码中，首先使用 perspective 属性设置视距，让元素具有 3D 效果，值越大，元素距离屏幕越远，视觉效果上就显得更小，这里设置为 800px 。然后使用 transform-style:preserve-3d; 开启 3D 空间。最后，使用 rotateY 方法结合 animation 属性来实现翻书效果， rotateY(0deg) 表示初始状态下页面是闭合的， rotateY(180deg) 表示页面完全翻开的状态， 10s 是翻书效果的时长， linear 是动画效果的速度曲线， infinite 是指动画效果无限循环。

实际应用中，你可以根据需要对代码进行调整，例如修改翻书效果的速度、方向和时长等。



### script标签的哪个属性可以实现html解析完成执行

在 <script> 标签中， defer 属性可以实现 HTML 解析完成后执行脚本。

 defer 属性的作用是延迟脚本的执行，直到页面完全加载（包括 HTML、CSS 和其他资源）完成后再执行。

使用 defer 属性的优点包括：

1. 提高页面加载速度：避免阻塞页面的其他内容加载。
2. 确保脚本在 HTML 解析完成后执行：可以访问已解析的 DOM。

示例如下：

```
<script defer src="script.js"></script>
```

在上述示例中，指定了 defer 属性，该脚本将在页面加载完成后执行。

需要注意的是， defer 属性只适用于外部脚本文件。如果脚本代码直接嵌入在 <script> 标签内部，则无法使用 defer 属性。



### js最准确的判断数组方法

在 JavaScript 中，有多种方法可以判断一个变量是否为数组，以下是几种常用的方法：

- instanceof 运算符：该方法通过检查变量的原型链中是否存在 Array 构造函数来判断一个变量是否为数组。如果存在，则返回 true，否则返回 false。但是，这种方法的准确性可能会受到原型链修改的影响。
- Array.isArray()方法：这是 ECMAScript 5 引入的方法，用于判断一个值是否为数组。它的使用非常简单，直接调用该方法并传入待判断的值即可。如果返回值为 true，则表示该值是一个数组；如果返回值为 false，则表示该值不是数组。
- Object.prototype.toString.call()方法：该方法会返回一个表示对象类型的字符串，对于数组来说，返回的字符串应该是"(object Array)"。这种方法可以准确地判断数组的类型，但代码相对复杂。

总的来说，以上方法都可以用于判断一个变量是否为数组，具体选择哪种方法，取决于你的需求和代码结构。



```
for (let i = 0; i < 3; i++) \\{
setTimeout(() => \\{
console.log(i);
\\}, 1000);
```


\\}这段JavaScript代码的功能是，每隔一秒（1000毫秒）在控制台打印变量i的值，一共打印三次。但是，你可能不会得到预期的连续打印0、1、2的结果，而是三次都打印3。

这是因为setTimeout函数是一个异步操作，它并不会立即执行，而是会等待指定的延迟时间后再执行。而在这段代码中，循环会先完成三次迭代，然后再依次执行setTimeout中的回调函数。由于let声明的变量i在循环外仍然是可访问的，所以每次执行回调函数时，它都会访问到当前的i值，即3。

如果你想让每次打印的都是循环时的i值，你需要使用闭包来捕获每次循环时的i值。你可以通过立即执行的函数表达式（IIFE）或者Array.prototype.forEach来实现这一点。

下面是使用IIFE的修改后的代码：

```
for (let i = 0; i < 3; i++) \\{
  (function(i) \\{
    setTimeout(() => \\{
      console.log(i);
    \\}, 1000);
  \\})(i);
\\}
```


在这个修改后的代码中，每次循环都会创建一个新的函数作用域，并将当前的i值作为参数传递给这个作用域。这样，在setTimeout的回调函数中，我们就可以访问到这个被捕获的i值，而不是循环结束后的i值。

同样的，你也可以使用Array.prototype.forEach来实现相同的效果：

```
[0, 1, 2].forEach((i) => \\{
  setTimeout(() => \\{
    console.log(i);
  \\}, 1000);
\\});
```

在这个例子中，我们创建了一个包含三个元素的数组，并使用forEach方法遍历这个数组。每次遍历都会将当前的元素值（即i）作为参数传递给回调函数，这样我们就可以在回调函数中直接访问到这个值，而无需担心循环结束后的变量值变化。



### css选择器和优先级

CSS选择器是用于选择你想要样式化的HTML元素的模式。这些选择器可以是元素选择器、类选择器、ID选择器、属性选择器、伪类选择器等。每种选择器都有其特定的用途和优先级。

CSS选择器种类：

元素选择器：基于HTML元素名称来选择元素，如 p、div 等。
类选择器：使用 . 开头的类名来选择元素，如 .myClass。
ID选择器：使用 # 开头的ID来选择元素，如 #myID。
属性选择器：基于元素的属性和属性值来选择元素，如 [type="text"]。
伪类选择器：用于选择HTML元素的特定状态，如 :hover、:active、:first-child 等。

CSS选择器优先级：

当多个选择器应用于同一个元素时，CSS有一套规则来确定哪个样式应该被应用。这就是所谓的“特异性”（specificity）或“优先级”。以下是确定优先级的一般规则：

内联样式：在HTML元素内部使用style属性定义的样式具有最高的优先级。
ID选择器：具有比类选择器、属性选择器和伪类选择器更高的优先级。
类选择器、属性选择器和伪类选择器：它们的优先级相同，并低于ID选择器，但高于元素选择器。
元素选择器：具有最低的优先级。
!important规则：如果样式声明后面带有!important，那么该声明将具有最高的优先级，无论其特异性如何。
继承：如果元素没有指定的样式，那么它会从其父元素继承样式。继承的样式具有最低的优先级。

如果两个选择器具有相同的特异性，那么后出现的规则会覆盖先出现的规则（这被称为“源顺序”或“后者优先”规则）。

为了编写高效且易于维护的CSS代码，建议尽量避免使用!important，并尽量保持选择器的特异性尽可能低。同时，合理地组织CSS规则，使它们易于理解和修改。



### 0.1+0.2为什么不等于0.3

在js中在 JavaScript 中，0.1 + 0.2 不等于 0.3 的原因在于浮点数在计算机中的表示和计算。这是由于计算机内部使用二进制表示法来存储浮点数，而很多十进制小数无法精确地用二进制小数来表示。

当你尝试将 0.1 和 0.2 相加时，这两个数在计算机内部实际上是以一种近似值的形式存在的。这种近似值是由一系列二进制位表示的，可能并不完全等同于十进制数中的 0.1 或 0.2。因此，当你将它们相加时，得到的结果可能是一个稍微偏离 0.3 的值。

这种问题不仅限于 JavaScript，它是浮点数运算中普遍存在的。如果你需要精确的小数运算，可能需要使用特殊的库或方法来处理。但在大多数日常编程任务中，这种微小的精度损失是可以接受的。

为了查看实际的计算结果，你可以尝试在 JavaScript 控制台中运行以下代码：

```
console.log(0.1 + 0.2);
```


你可能会看到类似 0.30000000000000004 这样的输出，这证明了计算结果并不完全等于 0.3。

如果你需要处理金融计算或其他需要高精度小数运算的场景，建议使用专门的库，如 decimal.js 或 big.js，这些库提供了更高精度的浮点数运算支持。



### 设置过期时间的localstory实现

你的问题可能是关于如何在JavaScript中实现一个具有过期时间的localStorage。在标准的localStorage API中，并没有直接提供设置过期时间的功能。但是，我们可以通过一些额外的逻辑来实现这一功能。

以下是一个简单的示例，演示了如何在localStorage中存储一个键值对，并为该键值对设置一个过期时间：

    class ExpiringLocalStorage \\{
        constructor() \\{
            this.prefix = 'expiring_';
        \\}
    set(key, value, ttl) \\{
        const now = new Date().getTime();
        const expiry = now + ttl;
        const data = \\{
            value: value,
            expiry: expiry
        \\};
    
        localStorage.setItem(this.prefix + key, JSON.stringify(data));
    \\}
    
    get(key) \\{
        const item = localStorage.getItem(this.prefix + key);
        if (!item) \\{
            return null;
        \\}
    
        const data = JSON.parse(item);
        const now = new Date().getTime();
    
        if (now > data.expiry) \\{
            // 如果数据已过期，则删除并从localStorage中返回null
            this.remove(key);
            return null;
        \\}
    
        return data.value;
    \\}
    
    remove(key) \\{
        localStorage.removeItem(this.prefix + key);
    \\}
    \\}
    
    // 使用示例：
    const expiringStorage = new ExpiringLocalStorage();
    expiringStorage.set('myKey', 'myValue', 1000 * 60 * 60); // 设置一个键为'myKey'，值为'myValue'，过期时间为1小时
    console.log(expiringStorage.get('myKey')); // 在过期前，应返回'myValue'

在这个示例中，我们创建了一个名为ExpiringLocalStorage的类，它封装了localStorage的基本功能，并添加了过期时间的概念。当调用set方法时，除了存储键值对外，还会存储一个过期时间（以毫秒为单位）。当调用get方法时，会检查数据是否已过期。如果已过期，则会从localStorage中删除该数据并返回null。如果未过期，则返回数据的值。

请注意，这个实现并不会自动删除过期的数据。你需要通过调用get方法来检查并删除过期的数据。如果你需要定期清理过期的数据，你可能需要设置一个定时器或使用其他方法来定期调用清理逻辑。

此外，由于localStorage的大小有限，并且所有的浏览器都可能有不同的限制，因此在使用localStorage时需要注意不要存储过多的数据。



### 分别解释请求头参数，host，cookie，method，accept，content-length

当然可以，以下是这些请求头参数的解释：

Host：

Host 请求头字段用于指定请求所发送的目标域名的地址。在HTTP/1.1中，每个请求都应包含一个Host头，因为网络地址（如IP地址）可能对应多个域名。
示例：Host: www.example.com

Cookie：

Cookie 请求头字段用于发送之前由服务器通过Set-Cookie头发送到浏览器的cookie。当浏览器发送请求到服务器时，它会包含所有相关的cookie，以便服务器能够识别用户会话和其他状态信息。
示例：Cookie: session_id=12345; user_id=john

Method：

Method 或 HTTP-Method 指的是HTTP请求的类型或动作。它告诉服务器你想要对请求的资源执行什么操作。常见的HTTP方法包括GET（获取资源）、POST（提交数据）、PUT（更新资源）、DELETE（删除资源）等。
注意：虽然Method不是请求头的一部分，但它是HTTP请求的一个重要组成部分，通常与请求头一起发送。

Accept：

Accept 请求头字段用于告诉服务器客户端可以处理哪些类型的响应内容。这通常用于指定客户端可以理解的媒体类型，如text/html、application/json等。
示例：Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8

Content-Length：

Content-Length 请求头字段表示请求体的长度（以字节为单位）。这对于那些包含请求体的请求方法（如POST和PUT）来说是非常重要的，因为它允许服务器知道要读取多少数据。
示例：Content-Length: 15

这些请求头字段在HTTP通信中起着关键作用，帮助客户端和服务器之间进行交互并理解彼此的请求和响应。不同的字段提供了关于请求的各种信息，使服务器能够更准确地响应客户端的需求。



### js数组里的数组，展开为一维数组去重升序

好的，了解你的需求啦！你想把一个包含数组的数组（二维数组）展开成一维数组，并且进行去重和升序排序，对吧？这个任务可以用JavaScript的几种方法来实现呢~

首先，我们可以使用Array.prototype.flat()方法将二维数组展开成一维数组，然后用Set数据结构进行去重，最后使用Array.prototype.sort()方法进行升序排序。下面是一个示例代码：

```
let nestedArray = [[1, 2, 3], [3, 4, 5], [5, 6, 1]];

// 使用 flat 方法将二维数组展开成一维数组
let flattenedArray = nestedArray.flat();

// 使用 Set 数据结构进行去重
let uniqueArray = [...new Set(flattenedArray)];

// 使用 sort 方法进行升序排序
let sortedArray = uniqueArray.sort((a, b) => a - b);

console.log(sortedArray); // 输出: [1, 2, 3, 4, 5, 6]
```


上面的代码首先使用flat()方法将二维数组nestedArray展开成一维数组flattenedArray。然后，我们利用Set的特性，将数组转换为Set，自动去除了重复的元素，再通过展开运算符...将Set转回数组uniqueArray。最后，我们使用sort()方法，通过传入一个比较函数，将数组uniqueArray进行升序排序，得到最终的排序数组sortedArray。

这个方法是不是很方便呢？希望对你有帮助哦~ (｡♥‿♥｡)



### cavas怎么局部渲染

在Canvas中，局部渲染通常指的是只更新或重绘Canvas的某一部分，而不是整个画布。这可以提高性能，尤其是在处理大型或复杂的Canvas应用时。以下是几种实现局部渲染的常见方法：

使用clearRect清除特定区域：

在重绘之前，你可以使用clearRect方法来清除Canvas上的特定区域。然后，只在该区域内进行绘制。

```
const canvas = document.getElementById('myCanvas');
const ctx = canvas.getContext('2d');

// 清除特定区域
ctx.clear
```



### 什么是js闭包和原型链

**JS闭包**

在JavaScript中，闭包是一个强大的概念，它指的是一个有权访问另一个函数作用域中的变量的函数。换句话说，一个函数内部定义的函数（称为内嵌函数）可以访问其父级函数的变量，甚至在父级函数执行完毕后，这些变量依然可以被内嵌函数访问。这就是因为闭包可以维持一个到其外部作用域的引用。

例如：

```javascript
function outerFunction() \\{  
    var outerVariable = 'I am from outer function!';  
  
    function innerFunction() \\{  
        console.log(outerVariable);  
    \\}  
  
    return innerFunction;  
\\}  
  
var inner = outerFunction();  
inner(); // 输出：I am from outer function!
```

在这个例子中，`innerFunction` 是一个闭包，因为它可以访问 `outerFunction` 的作用域中的 `outerVariable`。

**原型链**

原型链是JavaScript中对象继承的主要方式。每个JavaScript对象都有一个内部链接到另一个对象。这个链接被称为该对象的原型。当试图访问一个对象的属性时，如果该对象自身没有这个属性，那么JavaScript就会在该对象的原型上寻找这个属性，以此类推，一直通过原型链向上查找，直到找到属性或者到达原型链的末尾（`null`）。

每个构造函数都有一个 `prototype` 属性，这个属性是一个指针，指向一个对象，这个对象的用途是包含可以由特定类型的所有实例共享的属性和方法。当我们试图访问一个对象的某个属性时，JavaScript引擎首先会在对象本身的属性中查找，如果没有找到，就会到它的原型（也就是构造函数的 `prototype` 属性所指向的那个对象）中查找，如果再没有找到，就会到原型的原型中查找，依此类推，一直查到 `Object.prototype` 对象。如果还没有找到，就会返回 `undefined`。这种通过原型链接起来的链式结构，就叫做原型链。

例如：

```javascript
function Person(name) \\{  
    this.name = name;  
\\}  
  
Person.prototype.sayHello = function() \\{  
    console.log('Hello, my name is ' + this.name);  
\\}  
  
var person1 = new Person('Alice');  
person1.sayHello(); // 输出：Hello, my name is Alice
```

在这个例子中，`person1` 是一个 `Person` 的实例，它继承了 `Person.prototype` 上的 `sayHello` 方法。当我们调用 `person1.sayHello()` 时，实际上是通过原型链找到了 `Person.prototype` 上的 `sayHello` 方法。



### vue2升级vue3具体怎么做

Vue2升级到Vue3是一个涉及多个步骤的过程，下面是一个详细的步骤说明：

1. **创建一个新的Vue3项目**：
   使用Vue CLI工具创建一个新的Vue3项目。可以通过在命令行中运行`vue create projectName`命令并按照提示进行操作来完成这一步。
2. **安装依赖**：
   在新创建的Vue3项目中，需要安装必要的依赖。首先，将原Vue2项目中的`package.json`文件下的`dependencies`节点中的`vue`、`element-ui`、`vuex`等内容删除，并将这些依赖项追加到新项目的`package.json`中。然后，安装`element-plus`和`pinia`这两个Vue3的对应库，可以通过`npm install element-plus pinia`或`yarn add element-plus pinia`命令进行安装。最后，继续安装剩余的其他依赖项，通过执行`npm install`或`yarn install`命令完成。
3. **整理代码**：
   将原Vue2项目的`src`目录中的代码拷贝到新创建的Vue3项目中，但注意不要直接复制`main.js`文件。然后，根据代码的具体情况修改`main.js`文件。这一步可能涉及到对Vue2和Vue3之间API差异的处理。
4. **重写组件逻辑**：
   Vue 3引入了Composition API作为官方提供的组合式API，取代了Vue 2中的Options API。因此，在升级过程中，需要重写现有的组件逻辑，改为基于Composition API编写。这涉及到对组件内部状态、生命周期钩子、方法等的重新组织和实现。
5. **修改生命周期钩子**：
   Vue 3对生命周期钩子进行了调整，一些在Vue 2中存在的钩子（如`beforeCreate`、`created`等）被删除或替换。同时，Vue 3引入了新的生命周期钩子，如`setup()`函数作为新的入口点，以及`onBeforeMount`、`onMounted`等。因此，在升级过程中，需要根据Vue 3的文档说明修改相应的生命周期钩子名称和用法。
6. **处理其他差异**：
   在升级过程中，还需要注意Vue 2和Vue 3之间可能存在的其他差异，如指令的注册方式、全局API的变化等。这些差异可能需要根据具体的项目代码和Vue 3的文档进行逐一处理。
7. **测试与调试**：
   完成上述步骤后，需要对升级后的Vue3项目进行测试和调试，确保所有功能都正常工作，没有出现错误或异常。这可能涉及到对项目的各个部分进行详细的检查和验证。

请注意，Vue2升级到Vue3是一个复杂的过程，可能涉及到大量的代码修改和重构。在进行升级之前，建议详细阅读Vue 3的官方文档，了解Vue 3的新特性和与Vue 2的差异，以便更好地进行升级工作。同时，也建议备份好原Vue2项目的代码，以防万一出现不可预期的问题。



### setter怎么通知它的订阅者

在Vue中，setter可以通过 dep.notify() 方法来通知它的订阅者。其具体流程如下：

1. 创建一个 Observer 对象作为数据监听器，用来监听所有属性的变化。
2. 使用 Object.defineProperty() 方法，递归遍历所有属性，为每个属性添加 setter 和 getter 。
3. 当给对象的某个属性赋值时，会触发 setter ，从而监听到数据的变化。
4.  setter 触发 Dep 的 notify 方法，该方法会调用所有订阅者的 update 方法，以通知它们数据的变化。

通过这种方式，setter可以及时通知它的订阅者，从而实现数据的双向绑定和动态更新。



### 有一个20g的tar包，需要前端上传，如何做技术架构

对于20GB的tar包，前端上传确实需要一些特殊的技术架构来处理大文件上传的问题。以下是一个建议的技术架构：

#### 前端处理

文件分片：
将20GB的tar包切分成多个较小的文件分片。每个分片的大小可以根据网络条件和服务器配置来决定，通常可以选择几MB到几十MB不等。

分片上传：
使用JavaScript中的File API和FormData对象，逐个上传这些分片。可以使用如axios或fetch等HTTP客户端库来发送分片上传的请求。

进度追踪与展示：
通过监听每个分片的上传进度事件，实时更新并展示上传进度给用户，以便他们了解上传的进度和剩余时间。

断点续传：
如果上传过程中发生网络中断或其他错误，前端需要能够记录已经上传的分片信息，并在恢复上传时跳过这些已上传的分片，从断点处继续上传。

错误处理与重试机制：
对于上传失败的分片，前端应该实现重试机制，尝试重新上传失败的分片，直到成功为止。

#### 后端处理

接收分片：
后端需要提供一个API接口，用于接收前端发送的文件分片。可以使用Node.js、Java、Python等后端技术栈来实现。

分片存储：
后端接收到分片后，需要将其存储到临时目录中，以便后续合并成完整的tar包。可以使用文件系统、云存储服务（如Amazon S3、阿里云OSS等）或其他存储解决方案来存储分片。

合并分片：
当所有分片都上传完成后，后端需要将这些分片合并成一个完整的tar包。可以使用文件操作API或相关库来完成分片的合并。

文件完整性校验：
后端在合并完成后，应该计算整个tar包的哈希值，并与前端提供的哈希值进行比对，以确保文件的完整性。

删除临时分片：
合并完成后，后端需要删除存储的临时分片，以释放存储空间。

#### 其他考虑

安全性：
确保上传过程的安全性，例如使用HTTPS进行通信，验证用户身份，防止恶意文件上传等。

上传速度优化：
根据网络条件和服务器性能，可以考虑使用多线程上传、并行上传等技术来加快上传速度。

用户体验：
优化前端界面和交互，提供友好的上传体验，如拖拽上传、批量上传等功能。

综上所述，处理20GB的tar包上传需要前端和后端的紧密配合，通过文件分片、断点续传、错误处理等技术手段来确保上传的可靠性和效率。同时，还需要考虑安全性和用户体验等方面的问题。



### js设计模式

在 JavaScript 中，设计模式是解决软件开发某些特定问题而提出的一些解决方案，也可以理解成解决问题的一些思路。通过设计模式可以帮助开发者增强代码的可重用性、可扩充性、可维护性、灵活性。以下是几种常见的 JavaScript 设计模式：

- 单例模式：单例模式是一种只允许实例化一次的对象创建模式。它保证一个类只有一个实例，并且提供一个访问该实例的全局点。在 JavaScript 中，可以通过闭包来实现单例模式。
- 原型模式：原型模式是基于原型继承的。在这种模式中，被创建的对象充当其他对象的原型。实际上，原型（prototype）是被创建的每个对象构造函数的蓝图。
- 模块设计模式：模块设计模式对原型模式做了一些改进。模块模式设置了不同类型的修饰符（私有和公共）。你可以创建相似的函数或属性而不会发生冲突。这个设计模式的一个缺陷是无法覆盖（override）外部环境中创建的函数。
- 构造函数设计模式：这是一种特殊的方法，用于在分配内存后初始化新创建的对象。由于 JavaScript 一般来说是面向对象的，所以它打交道最多的就是对象。于是深入研究对象构造函数。在 JavaScript 中创建新对象有三种方法可用。

如果你还想了解更多关于 JavaScript 设计模式的内容，请继续向我提问。



### vue2迁移vue3，具体怎么处理

将 Vue 2 项目迁移到 Vue 3 可以按照以下步骤进行处理：

1. 升级 Vue 版本：在项目中安装 Vue 3。
2. 组件重构：根据 Vue 3 的语法和特性，重构组件。
3. 使用 Composition API：利用 Composition API 来管理状态和逻辑。
4. 模板语法调整：适应 Vue 3 的模板语法变化。
5. 处理生命周期钩子：了解 Vue 3 中生命周期钩子的改动。
6. 适配插件和依赖：确保使用的插件和依赖与 Vue 3 兼容。
7. 测试和调试：进行全面的测试以确保项目的正常运行。

在迁移过程中，可能会遇到一些问题，需要仔细检查和调试。同时，参考 Vue 3 的官方文档和相关教程可以帮助你更好地完成迁移。



### 前端工程师在项目中遇到什么难题，你是怎么解决它？

前端工程师在项目中可能会遇到以下一些难题：

1. 浏览器兼容性问题：不同浏览器对 HTML、CSS 和 JavaScript 的实现可能存在差异。
解决方法：进行广泛的浏览器测试，使用特定的兼容解决方案。
2. 性能优化：确保页面加载速度快，用户体验良好。
解决方法：压缩资源、优化代码、使用缓存等。
3. 复杂的用户界面设计：创建具有复杂交互和视觉效果的界面。
解决方法：选择合适的前端框架和工具，进行合理的架构设计。
4. 与后端集成：确保前端与后端之间的数据传输和通信顺畅。
解决方法：使用合适的 API 设计和通信协议。
5. 移动端适配：使页面在各种移动设备上良好显示。
解决方法：采用响应式设计或特定的移动端解决方案。
6. 安全和权限问题：保护用户数据和系统安全。
解决方法：实施安全策略，进行漏洞测试。
7. 团队协作和代码管理：与其他开发者协同工作。
解决方法：使用版本控制系统，进行有效的沟通和协作。
8. 不断变化的技术和需求：跟上行业的发展和用户需求的变化。
解决方法：持续学习，灵活调整项目架构。

解决这些难题通常需要以下步骤：

1. 分析问题：确定问题的本质和范围。
2. 研究和学习：查找相关的知识和解决方案。
3. 尝试不同方法：进行实验和测试。
4. 与团队成员沟通：分享想法和经验。
5. 优化和改进：不断完善解决方案。
6. 记录和总结：以便在未来的项目中参考。



### 程序题

let str='aabcd'
计算每个字母出现的次数
将重复字母移出字符串

在 JavaScript 中，可以通过遍历字符串来计算每个字母出现的次数，并使用数组来存储每个字母及其出现的次数。然后遍历数组，将重复的字母从字符串中移除。以下是示例代码：

```
let str = 'aabcd';
let charCount = \\{\\};
for (let i = 0; i < str.length; i++) \\{
  if (charCount[str[i]]) \\{
    charCount[str[i]]++;
  \\} else \\{
    charCount[str[i]] = 1;
  \\}
\\}
let newStr = '';
for (let key in charCount) \\{
  if (charCount[key] === 1) \\{
    newStr += key;
  \\}
\\}
console.log(newStr);
```

在上述代码中，首先定义了字符串`str`，然后遍历字符串，通过`charCount`对象来记录每个字母及其出现的次数。接着创建一个新的字符串`newStr`，遍历`charCount`对象，将出现次数为 1 的字母添加到`newStr`中。最后打印输出处理后的字符串。 

