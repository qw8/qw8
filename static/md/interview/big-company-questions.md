---
title: 大厂高频题
date: 2021-06-24 16:42:29
categories: 
- 前端面试
tags:
- JavaScript
- vue
---

[转载自 Advanced-Frontend/Daily-Interview-Question](https://github.com/Advanced-Frontend/Daily-Interview-Question)

### 第 1 题：写 React / Vue 项目时为什么要在列表组件中写 key，其作用是什么？

答案：key 是给每一个 vnode（虚拟节点）的唯一 id,可以依靠 key,更准确, 更快的拿到 oldVnode 中对应的 vnode 节点。

1. 更准确
   因为带 key 就不是就地复用了，在 sameNode 函数 a.key === b.key 对比中可以避免就地复用的情况。所以会更加准确。

2. 更快
   利用 key 的唯一性生成 map 对象来获取对应节点，比遍历方式更快。

公司：滴滴、饿了么

解析：[第 1 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/1)



### 第 2 题：`['1', '2', '3'].map(parseInt)` what & why ?

答案：[1, NaN, NaN]

- parseInt('1', 0) //radix 为 0 时，且 string 参数不以“0x”和“0”开头时，按照 10 为基数处理。这个时候返回 1
- parseInt('2', 1) //基数为 1（1 进制）表示的数中，最大值小于 2，所以无法解析，返回 NaN
- parseInt('3', 2) //基数为 2（2 进制）表示的数中，最大值小于 3，所以无法解析，返回 NaN

解析：[第 2 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/4)



### 第 4 题：介绍下 Set、Map、WeakSet 和 WeakMap 的区别？

答案：

1、Set

- 成员唯一、无序且不重复；
- [value, value]，键值与键名是一致的（或者说只有键值，没有键名）；
- 可以遍历，方法有：add、delete、has、clear、entries、forEach、keys、values
- Set 也能用来保存 NaN 和 undefined， 如果有重复的 NaN， Set 会认为就一个 NaN(实际上 NaN!=NaN);

2、Map

- 本质上是键值对的集合，类似集合；
- 可以遍历，方法很多，可以跟各种数据格式转换。

3、WeakSet

- 成员都是对象；
- 成员都是弱引用，可以被垃圾回收机制回收，可以用来保存 DOM 节点，不容易造成内存泄漏；
- 不能遍历，方法有 add、delete、has。

4、WeakMap

- 只接受对象作为键名（null 除外），不接受其他类型的值作为键名；
- 键名是弱引用，键值可以是任意的，键名所指向的对象可以被垃圾回收，此时键名是无效的；
- 不能遍历，方法有 get、set、has、delete。

解析：[第 4 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/6)



### 第 5 题：介绍下深度优先遍历和广度优先遍历，如何实现？

解析：[第 5 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/9)



### 第 6 题：请分别用深度优先思想和广度优先思想实现一个拷贝函数？

答案：

解析：[第 6 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/10)



### 第 7 题：ES5/ES6 的继承除了写法以外还有什么区别？

答案：

解析：[第 7 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/20)



### 第 8 题：setTimeout、Promise、Async/Await 的区别

答案：

解析：[第 8 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/33)



### 第 9 题：Async/Await 如何通过同步的方式实现异步

答案：

公司：头条、微医

解析：[第 9 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/156)



### 第 10 题：异步笔试题

答案：

> 请写出下面代码的运行结果

```js
async function async1() \\{
  console.log("async1 start");
  await async2();
  console.log("async1 end");
\\}
async function async2() \\{
  console.log("async2");
\\}
console.log("script start");
setTimeout(function() \\{
  console.log("setTimeout");
\\}, 0);
async1();
new Promise(function(resolve) \\{
  console.log("promise1");
  resolve();
\\}).then(function() \\{
  console.log("promise2");
\\});
console.log("script end");
```

公司：头条

答案：

```js
// script start
// async1 start
// async2
// promise1
// script end
// async1 end
// promise2
// undefined
// setTimeout
```

解析：[第 10 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/7)



### 第 11 题：算法手写题

答案：

> 已知如下数组：
>
> var arr = [ [1, 2, 2], [3, 4, 5, 5], [6, 7, 8, 9, [11, 12, [12, 13, [14] ] ] ], 10];
>
> 编写一个程序将数组扁平化去并除其中重复部分数据，最终得到一个升序且不重复的数组

公司：携程

答案：

```js
Array.from(new Set(arr.flat(Infinity))).sort((a, b) => \\{
  return a - b;
\\});
```

拆解：

```js
arr.flat(Infinity); // 1.所有元素放到同一数组
//  [1, 2, 2, 3, 4, 5, 5, 6, 7, 8, 9, 11, 12, 12, 13, 14, 10]
Array.from(new Set(arr.flat(Infinity))).sort((a, b) => \\{
  return a - b;
\\}); // 2.去重及排序
// [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14]
```

解析：[第 11 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/8)



### 第 12 题：JS 异步解决方案的发展历程以及优缺点。

答案：

公司：滴滴、挖财、微医、海康

解析：[第 12 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/11)



### 第 13 题：Promise 构造函数是同步执行还是异步执行，那么 then 方法呢？

答案：

公司：微医

解析：[第 13 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/19)



### 第 14 题：情人节福利题，如何实现一个 new

答案：

公司：兑吧

解析：[第 14 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/12)



### 第 15 题：简单讲解一下 http2 的多路复用

答案：

公司：网易

解析：[第 15 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/14)



### 第 16 题：谈谈你对 TCP 三次握手和四次挥手的理解

答案：

解析：[第 16 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/15)



### 第 17 题：A、B 机器正常连接后，B 机器突然重启，问 A 此时处于 TCP 什么状态

答案：

> 如果 A 与 B 建立了正常连接后，从未相互发过数据，这个时候 B 突然机器重启，问 A 此时处于 TCP 什么状态？如何消除服务器程序中的这个状态？（超纲题，了解即可）

解析：[第 17 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/21)



### 第 18 题：React 中 setState 什么时候是同步的，什么时候是异步的？

答案：
公司：微医

解析：[第 18 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/17)



### 第 19 题：React setState 笔试题，下面的代码输出什么？

答案：

```js
class Example extends React.Component \\{
  constructor() \\{
    super();
    this.state = \\{
      val: 0
    \\};
  \\}

  componentDidMount() \\{
    this.setState(\\{ val: this.state.val + 1 \\});
    console.log(this.state.val); // 第 1 次 log

    this.setState(\\{ val: this.state.val + 1 \\});
    console.log(this.state.val); // 第 2 次 log

    setTimeout(() => \\{
      this.setState(\\{ val: this.state.val + 1 \\});
      console.log(this.state.val); // 第 3 次 log

      this.setState(\\{ val: this.state.val + 1 \\});
      console.log(this.state.val); // 第 4 次 log
    \\}, 0);
  \\}

  render() \\{
    return null;
  \\}
\\}
```

解析：[第 19 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/18)



### 第 20 题：介绍下 npm 模块安装机制，为什么输入 npm install 就可以自动安装对应的模块？

答案：
解析：[第 20 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/22)



### 第 21 题：有以下 3 个判断数组的方法，请分别介绍它们之间的区别和优劣

答案：

> Object.prototype.toString.call() 、 instanceof 以及 Array.isArray()

解析：[第 21 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/23)



### 第 22 题：介绍下重绘和回流（Repaint & Reflow），以及如何进行优化

解析：[第 22 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/24)



### 第 23 题：介绍下观察者模式和订阅-发布模式的区别，各自适用于什么场景

答案：
解析：[第 23 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/25)



### 第 24 题：聊聊 Redux 和 Vuex 的设计思想

答案：
解析：[第 24 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/45)



### 第 25 题：说说浏览器和 Node 事件循环的区别

答案：
解析：[第 25 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/26)



### 第 26 题：介绍模块化发展历程

答案：

可从 IIFE、AMD、CMD、CommonJS、UMD、webpack(require.ensure)、ES Module、`<script type="module">` 这几个角度考虑。

解析：[第 26 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/28)



### 第 27 题：全局作用域中，用 const 和 let 声明的变量不在 window 上，那到底在哪里？如何去获取？

答案：

解析：[第 27 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/30)



### 第 28 题：cookie 和 token 都存放在 header 中，为什么不会劫持 token？

答案：
解析：[第 28 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/31)



### 第 29 题：聊聊 Vue 的双向数据绑定，Model 如何改变 View，View 又是如何改变 Model 的

答案：
解析：[第 29 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/34)



### 第 30 题：两个数组合并成一个数组

答案：
请把两个数组 ['A1', 'A2', 'B1', 'B2', 'C1', 'C2', 'D1', 'D2'] 和 ['A', 'B', 'C', 'D']，合并为 ['A1', 'A2', 'A', 'B1', 'B2', 'B', 'C1', 'C2', 'C', 'D1', 'D2', 'D']。

解析： [第 30 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/39)



### 第 31 题：改造下面的代码，使之输出 0 - 9，写出你能想到的所有解法。

答案：

```js
for (var i = 0; i < 10; i++) \\{
  setTimeout(() => \\{
    console.log(i);
  \\}, 1000);
\\}
```

解析：[第 31 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/43)



### 第 32 题：Virtual DOM 真的比操作原生 DOM 快吗？谈谈你的想法。

答案：
解析：[第 32 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/47)



### 第 33 题：下面的代码打印什么内容，为什么？

答案：

```js
var b = 10;
(function b() \\{
  b = 20;
  console.log(b);
\\})();
```

解析：[第 33 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/48)



### 第 34 题：简单改造下面的代码，使之分别打印 10 和 20。

答案：

```js
var b = 10;
(function b() \\{
  b = 20;
  console.log(b);
\\})();
```

解析：[第 34 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/51)



### 第 35 题：浏览器缓存读取规则

答案：

可以分成 Service Worker、Memory Cache、Disk Cache 和 Push Cache，那请求的时候 from memory cache 和 from disk cache 的依据是什么，哪些数据什么时候存放在 Memory Cache 和 Disk Cache 中？

解析：[第 35 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/53)



### 第 36 题：使用迭代的方式实现 flatten 函数。

答案：
解析：[第 36 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/54)



### 第 37 题：为什么 Vuex 的 mutation 和 Redux 的 reducer 中不能做异步操作？

答案：
解析：[第 37 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/65)



### 第 38 题：下面代码中 a 在什么情况下会打印 1？

答案：

```js
var a = ?;
if(a == 1 && a == 2 && a == 3)\\{
 	console.log(1);
\\}
```

解析：[第 38 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/57)

公司：京东



### 第 39 题：介绍下 BFC 及其应用

答案：
解析：[第 39 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/59)



### 第 40 题：在 Vue 中，子组件为何不可以修改父组件传递的 Prop

答案：
如果修改了，Vue 是如何监控到属性的修改并给出警告的。

解析：[第 40 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/60)



### 第 41 题：下面代码输出什么

答案：

```js
var a = 10;
(function() \\{
  console.log(a);
  a = 5;
  console.log(window.a);
  var a = 20;
  console.log(a);
\\})();
```

解析：[第 41 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/61)



### 第 42 题：实现一个 sleep 函数

答案：
比如 sleep(1000) 意味着等待 1000 毫秒，可从 Promise、Generator、Async/Await 等角度实现

解析：[第 42 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/63)



### 第 43 题：使用 sort() 对数组 [3, 15, 8, 29, 102, 22] 进行排序，输出结果

答案：
解析：[第 43 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/66)



### 第 44 题：介绍 HTTPS 握手过程

答案：
解析：[第 44 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/70)



### 第 45 题：HTTPS 握手过程中，客户端如何验证证书的合法性

答案：
解析：[第 45 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/74)



### 第 46 题：输出以下代码执行的结果并解释为什么

答案：

```js
var obj = \\{
  "2": 3,
  "3": 4,
  length: 2,
  splice: Array.prototype.splice,
  push: Array.prototype.push
\\};
obj.push(1);
obj.push(2);
console.log(obj);
```

解析：[第 46 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/76)



### 第 47 题：双向绑定和 vuex 是否冲突

答案：
解析：[第 47 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/81)



### 第 48 题：call 和 apply 的区别是什么，哪个性能更好一些

答案：
解析：[第 48 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/84)



### 第 49 题：为什么通常在发送数据埋点请求的时候使用的是 1x1 像素的透明 gif 图片？

答案：
解析：[第 49 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/87)



### 第 50 题：实现 (5).add(3).minus(2) 功能。

> 例： 5 + 3 - 2，结果为 6

解析：[第 50 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/88)

公司：百度



### 第 51 题：Vue 的响应式原理中 Object.defineProperty 有什么缺陷？

答案：
为什么在 Vue3.0 采用了 Proxy，抛弃了 Object.defineProperty？

解析：[第 51 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/90)



### 第 52 题：怎么让一个 div 水平垂直居中

答案：
解析：[第 52 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/92)



### 第 53 题：输出以下代码的执行结果并解释为什么

答案：

```js
var a = \\{ n: 1 \\};
var b = a;
a.x = a = \\{ n: 2 \\};

console.log(a.x);
console.log(b.x);
```

解析：[第 53 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/93)



### 第 54 题：冒泡排序如何实现，时间复杂度是多少， 还可以如何改进？

答案：
解析：[第 54 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/94)



### 第 55 题：某公司 1 到 12 月份的销售额存在一个对象里面

答案：
如下：\\{1:222, 2:123, 5:888\\}，请把数据处理为如下结构：[222, 123, null, null, 888, null, null, null, null, null, null, null]。

解析：[第 55 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/96)



### 第 56 题：要求设计 LazyMan 类，实现以下功能。

答案：

```js
LazyMan("Tony");
// Hi I am Tony

LazyMan("Tony")
  .sleep(10)
  .eat("lunch");
// Hi I am Tony
// 等待了10秒...
// I am eating lunch

LazyMan("Tony")
  .eat("lunch")
  .sleep(10)
  .eat("dinner");
// Hi I am Tony
// I am eating lunch
// 等待了10秒...
// I am eating diner

LazyMan("Tony")
  .eat("lunch")
  .eat("dinner")
  .sleepFirst(5)
  .sleep(10)
  .eat("junk food");
// Hi I am Tony
// 等待了5秒...
// I am eating lunch
// I am eating dinner
// 等待了10秒...
// I am eating junk food
```

解析：[第 56 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/98)



### 第 57 题：分析比较 opacity: 0、visibility: hidden、display: none 优劣和适用场景。

答案：
解析：[第 57 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/100)



### 第 58 题：箭头函数与普通函数（function）的区别是什么？构造函数（function）可以使用 new 生成实例，那么箭头函数可以吗？为什么？

答案：
解析：[第 58 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/101)



### 第 59 题：给定两个数组，写一个方法来计算它们的交集。

答案：

> 例如：给定 nums1 = [1, 2, 2, 1]，nums2 = [2, 2]，返回 [2, 2]。

解析：[第 59 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/102)



### 第 60 题：已知如下代码，如何修改才能让图片宽度为 300px ？注意下面代码不可修改。

> `<img src="1.jpg" style="width:480px!important;”>`

解析：[第 60 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/105)



### 第 61 题：介绍下如何实现 token 加密

答案：
解析：[第 61 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/106)



### 第 62 题：redux 为什么要把 reducer 设计成纯函数

答案：
解析：[第 62 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/107)



### 第 63 题：如何设计实现无缝轮播

答案：
解析：[第 63 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/108)



### 第 64 题：模拟实现一个 Promise.finally

答案：
解析：[第 64 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/109)



### 第 65 题： `a.b.c.d` 和 `a['b']['c']['d']`，哪个性能更高？

答案：
解析：[第 65 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/111)



### 第 66 题：ES6 代码转成 ES5 代码的实现思路是什么

答案：
解析：[第 66 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/112)



### 第 67 题：数组编程题

答案：
随机生成一个长度为 10 的整数类型的数组，例如 `[2, 10, 3, 4, 5, 11, 10, 11, 20]`，将其排列成一个新数组，要求新数组形式如下，例如 `[[2, 3, 4, 5], [10, 11], [20]]`。

解析：[第 67 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/113)



### 第 68 题： 如何解决移动端 Retina 屏 1px 像素问题

解析：[第 68 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/115)



### 第 69 题： 如何把一个字符串的大小写取反（大写变小写小写变大写），例如 ’AbC' 变成 'aBc' 。

答案：
解析：[第 69 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/116)



### 第 70 题： 介绍下 webpack 热更新原理，是如何做到在不刷新浏览器的前提下更新页面的

答案：
解析：[第 70 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/118)



### 第 71 题： 实现一个字符串匹配算法，从长度为 n 的字符串 S 中，查找是否存在字符串 T，T 的长度是 m，若存在返回所在位置。

答案：
解析：[第 71 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/119)



### 第 72 题： 为什么普通 `for` 循环的性能远远高于 `forEach` 的性能，请解释其中的原因。

答案：
![image-20190512225510941](https://ws2.sinaimg.cn/large/006tNc79gy1g2yxbg4ta8j31gh0u048h.jpg)

解析：[第 72 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/121)



### 第 73 题： 介绍下 BFC、IFC、GFC 和 FFC

答案：
解析：[第 73 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/122)



### 第 74 题： 使用 JavaScript Proxy 实现简单的数据绑定

答案：
解析：[第 74 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/123)



### 第 75 题：数组里面有 10 万个数据，取第一个元素和第 10 万个元素的时间相差多少

答案：
解析：[第 75 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/124)



### 第 76 题：输出以下代码运行结果

答案：

```js
// example 1
var a=\\{\\}, b='123', c=123;
a[b]='b';
a[c]='c';
console.log(a[b]);

---------------------
// example 2
var a=\\{\\}, b=Symbol('123'), c=Symbol('123');
a[b]='b';
a[c]='c';
console.log(a[b]);

---------------------
// example 3
var a=\\{\\}, b=\\{key:'123'\\}, c=\\{key:'456'\\};
a[b]='b';
a[c]='c';
console.log(a[b]);
```

解析：[第 76 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/125)



### 第 77 题：算法题「旋转数组」

答案：

> 给定一个数组，将数组中的元素向右移动 k 个位置，其中 k 是非负数。

示例 1：

```js
输入: [1, 2, 3, 4, 5, 6, 7] 和 k = 3
输出: [5, 6, 7, 1, 2, 3, 4]
解释:
向右旋转 1 步: [7, 1, 2, 3, 4, 5, 6]
向右旋转 2 步: [6, 7, 1, 2, 3, 4, 5]
向右旋转 3 步: [5, 6, 7, 1, 2, 3, 4]
```

示例 2：

```js
输入: [-1, -100, 3, 99] 和 k = 2
输出: [3, 99, -1, -100]
解释:
向右旋转 1 步: [99, -1, -100, 3]
向右旋转 2 步: [3, 99, -1, -100]
```

解析：[第 77 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/126)



### 第 78 题：Vue 的父组件和子组件生命周期钩子执行顺序是什么

答案：
解析：[第 78 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/128)



### 第 79 题：input 搜索如何防抖，如何处理中文输入

答案：
解析：[第 79 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/129)



### 第 80 题：介绍下 Promise.all 使用、原理实现及错误处理

答案：
解析：[第 80 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/130)



### 第 81 题：打印出 1 - 10000 之间的所有对称数

答案：

> 例如：121、1331 等

解析：[第 81 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/131)



### 第 82 题：周一算法题之「移动零」

答案：

> 给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。
>
> 示例:
>
> ```
> 输入: [0,1,0,3,12]
> 输出: [1,3,12,0,0]
> ```
>
> 说明:
>
> 1. 必须在原数组上操作，不能拷贝额外的数组。
>
> 1. 尽量减少操作次数。

解析：[第 82 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/132)



### 第 83 题：var、let 和 const 区别的实现原理是什么

答案：
解析：[第 83 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/133)



### 第 84 题：请实现一个 add 函数，满足以下功能。

答案：

> ```js
> add(1); 			// 1
> add(1)(2);  	// 3
> add(1)(2)(3)；// 6
> add(1)(2, 3); // 6
> add(1, 2)(3); // 6
> add(1, 2, 3); // 6
> ```

解析：[第 84 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/134)



### 第 85 题：react-router 里的 `<Link>` 标签和 `<a>` 标签有什么区别

答案：

> 如何禁掉 `<a>` 标签默认事件，禁掉之后如何实现跳转。

解析：[第 85 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/135)



### 第 86 题：周一算法题之「两数之和」

答案：
给定一个整数数组和一个目标值，找出数组中和为目标值的两个数。

你可以假设每个输入只对应一种答案，且同样的元素不能被重复利用。

示例：

```js
给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```

解析：[第 86 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/136)

公司：京东、快手



### 第 87 题：在输入框中如何判断输入的是一个正确的网址。

答案：
解析：[第 87 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/138)



### 第 88 题：实现 convert 方法，把原始 list 转换成树形结构，要求尽可能降低时间复杂度

答案：
以下数据结构中，id 代表部门编号，name 是部门名称，parentId 是父部门编号，为 0 代表一级部门，现在要求实现一个 convert 方法，把原始 list 转换成树形结构，parentId 为多少就挂载在该 id 的属性 children 数组下，结构如下：

```js
// 原始 list 如下
let list =[
    \\{id:1,name:'部门A',parentId:0\\},
    \\{id:2,name:'部门B',parentId:0\\},
    \\{id:3,name:'部门C',parentId:1\\},
    \\{id:4,name:'部门D',parentId:1\\},
    \\{id:5,name:'部门E',parentId:2\\},
    \\{id:6,name:'部门F',parentId:3\\},
    \\{id:7,name:'部门G',parentId:2\\},
    \\{id:8,name:'部门H',parentId:4\\}
];
const result = convert(list, ...);

// 转换后的结果如下
let result = [
    \\{
      id: 1,
      name: '部门A',
      parentId: 0,
      children: [
        \\{
          id: 3,
          name: '部门C',
          parentId: 1,
          children: [
            \\{
              id: 6,
              name: '部门F',
              parentId: 3
            \\}, \\{
              id: 16,
              name: '部门L',
              parentId: 3
            \\}
          ]
        \\},
        \\{
          id: 4,
          name: '部门D',
          parentId: 1,
          children: [
            \\{
              id: 8,
              name: '部门H',
              parentId: 4
            \\}
          ]
        \\}
      ]
    \\},
  ···
];
```

解析：[第 88 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/139)



### 第 89 题：设计并实现 Promise.race()

答案：
解析：[第 89 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/140)



### 第 90 题：实现模糊搜索结果的关键词高亮显示

答案：
<img src="https://ws3.sinaimg.cn/large/006tNc79ly1g43dykaccuj30u01hc49s.jpg" height="800"/>

解析：[第 90 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/141)



### 第 91 题：介绍下 HTTPS 中间人攻击

答案：
解析：[第 91 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/142)



### 第 92 题：已知数据格式，实现一个函数 fn 找出链条中所有的父级 id

答案：

> ```js
> const value = '112'
> const fn = (value) => \\{
> ...
> \\}
> fn(value) // 输出 [1， 11， 112]
> ```

<img src="https://ws1.sinaimg.cn/large/006tNc79gy1g45a04ntttj30k20wen01.jpg" height="800"/>

解析：[第 92 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/143)



### 第 93 题：给定两个大小为 m 和 n 的有序数组 nums1 和 nums2。请找出这两个有序数组的中位数。要求算法的时间复杂度为 O(log(m+n))。

答案：
示例 1：

```js
nums1 = [1, 3];
nums2 = [2];
```

中位数是 2.0

示例 2：

```js
nums1 = [1, 2];
nums2 = [3, 4];
```

中位数是(2 + 3) / 2 = 2.5

解析：[第 93 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/144)



### 第 94 题：vue 在 v-for 时给每项元素绑定事件需要用事件代理吗？为什么？

答案：
解析：[第 94 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/145)



### 第 95 题：模拟实现一个深拷贝，并考虑对象相互引用以及 Symbol 拷贝的情况

答案：
解析：[第 95 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/148)



### 第 96 题：介绍下前端加密的常见场景和方法

答案：
解析：[第 96 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/150)



### 第 97 题：React 和 Vue 的 diff 时间复杂度从 O(n^3) 优化到 O(n) ，那么 O(n^3) 和 O(n) 是如何计算出来的？

答案：
解析：[第 97 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/151)



### 第 98 题：写出如下代码的打印结果

```js
function changeObjProperty(o) \\{
  o.siteUrl = "http://www.baidu.com";
  o = new Object();
  o.siteUrl = "http://www.google.com";
\\}
let webSite = new Object();
changeObjProperty(webSite);
console.log(webSite.siteUrl);
```

公司：京东

解析：[第 98 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/152)



### 第 99 题：编程算法题

答案：

> 用 JavaScript 写一个函数，输入 int 型，返回整数逆序后的字符串。如：输入整型 1234，返回字符串“4321”。要求必须使用递归函数调用，不能用全局变量，输入函数必须只有一个参数传入，必须返回字符串。

公司：bilibili

解析：[第 99 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/153)
