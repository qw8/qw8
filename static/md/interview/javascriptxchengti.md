---
title: JavaScript编程题
date: 2020-05-28 10:41:39
categories: 
- 前端面试
tags:
- JavaScript
- 算法
- 编程题
---

## 常考代码题

### 防抖和节流区别

防抖（Debouncing）和节流（Throttling）是前端开发中用来优化性能的两种常见技术，主要用于控制函数调用的频率。它们通常用于处理那些可能在短时间内被频繁触发的事件，如窗口调整大小、滚动、输入框内容变化等。

#### 防抖（Debouncing）

防抖的原理是：当某个事件被触发时，并不立即执行对应的函数，而是等待一段时间（即设定的延迟时间），如果在这段时间内没有再次触发该事件，则执行函数；如果在这段时间内再次触发了事件，则重新计时。

**应用场景：**

- 搜索框中的实时搜索功能。
- 窗口调整大小后，确保所有调整操作完成后才进行布局调整或重绘。
- 提交表单前的验证，防止用户快速多次点击提交按钮。

#### 节流（Throttling）

节流的原理是：不管事件触发了多少次，在设定的时间间隔内只允许执行一次函数。换句话说，它会保证函数在一定时间内最多被执行一次，即使事件触发得非常频繁。

**应用场景：**

- 滚动事件监听，比如无限滚动加载更多内容。
- 缩放事件监听，以限制布局计算的频率。
- 游戏中的按键响应，避免玩家过快地重复按键。

#### 区别

- **触发时机不同**：防抖是当最后一次事件触发后的指定时间内如果没有新的触发才会执行，而节流是在每次事件触发时都会检查是否达到了执行的时间间隔。
- **使用场景不同**：防抖适用于需要等到一系列连续动作结束后再执行的场景，例如输入完成后再查询；节流则适用于需要控制操作频率的场景，例如每滚动一段距离就加载新内容。

通过合理使用防抖和节流，可以有效减少不必要的计算资源浪费，提高用户体验和页面性能。



### 手写防抖函数

```
const debounce = (fn = \\{\\}, wait = 50, immediate) => \\{
  let timer;
  return function() \\{
    if (immediate) \\{
      fn.apply(this, arguments);
    \\}
    if (timer) \\{
      clearTimeout(timer);
      timer = null;
    \\}
    timer = setTimeout(() => \\{
      fn.apply(this, arguments);
    \\}, wait);
  \\};
\\};

```



### 手写节流函数

```
var throttle = (fn = \\{\\}, wait = 0) => \\{
  let prev = new Date();
  return function() \\{
    const args = arguments;
    const now = new Date();
    if (now - prev > wait) \\{
      fn.apply(this, args);
      prev = new Date();
    \\}
  \\};
\\};
```



### 什么是防抖和节流？有什么区别？如何实现？

1、防抖(debounce)：触发高频事件后 n 秒内函数只会执行一次，如果 n 秒内高频事件再次被触发，则重新计算时间

举例：就好像在百度搜索时，每次输入之后都有联想词弹出，这个控制联想词的方法就不可能是输入框内容一改变就触发的，他一定是当你结束输入一段时间之后才会触发。

节流(thorttle)：高频事件触发，但在 n 秒内只会执行一次，所以节流会稀释函数的执行频率

举例：预定一个函数只有在大于等于执行周期时才执行，周期内调用不执行。就好像你在淘宝抢购某一件限量热卖商品时，你不断点刷新点购买，可是总有一段时间你点上是没有效果，这里就用到了节流，就是怕点的太快导致系统出现bug。

2、区别：防抖动是将多次执行变为最后一次执行，节流是将多次执行变成每隔一段时间执行。

公司：挖财

解析：[第 3 题](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/5)



### 什么是防抖和节流？有什么区别？如何实现？

#### 防抖

触发高频事件后n秒内函数只会执行一次，如果n秒内高频事件再次被触发，则重新计算时间
思路：
每次触发事件时都取消之前的延时调用方法

```
function debounce(fn) \\{
      let timeout = null; // 创建一个标记用来存放定时器的返回值
      return function () \\{
        clearTimeout(timeout); // 每当用户输入的时候把前一个 setTimeout clear 掉
        timeout = setTimeout(() => \\{ // 然后又创建一个新的 setTimeout, 这样就能保证输入字符后的 interval 间隔内如果还有字符输入的话，就不会执行 fn 函数
          fn.apply(this, arguments);
        \\}, 500);
      \\};
    \\}
    function sayHi() \\{
      console.log('防抖成功');
    \\}
```

    var inp = document.getElementById('inp');
    inp.addEventListener('input', debounce(sayHi)); // 防抖

#### 节流

高频事件触发，但在n秒内只会执行一次，所以节流会稀释函数的执行频率
思路：
每次触发事件时都判断当前是否有等待执行的延时函数

```
function throttle(fn) \\{
      let canRun = true; // 通过闭包保存一个标记
      return function () \\{
        if (!canRun) return; // 在函数开头判断标记是否为true，不为true则return
        canRun = false; // 立即设置为false
        setTimeout(() => \\{ // 将外部传入的函数的执行放在setTimeout中
          fn.apply(this, arguments);
          // 最后在setTimeout执行完毕后再把标记设置为true(关键)表示可以执行下一次循环了。当定时器没有执行的时候标记永远是false，在开头被return掉
          canRun = true;
        \\}, 500);
      \\};
    \\}
    function sayHi(e) \\{
      console.log(e.target.innerWidth, e.target.innerHeight);
    \\}
    window.addEventListener('resize', throttle(sayHi));
```



### 介绍一下 js 的节流与防抖？

函数防抖： 在事件被触发 n 秒后再执行回调，如果在这 n 秒内事件又被触发，则重新计时。

函数节流： 规定一个单位时间，在这个单位时间内，只能有一次触发事件的回调函数执行，如果在同一个单位时间内某事件被触发多次，只有一次能生效。

```js
// 函数防抖的实现
function debounce(fn, wait) \\{
  var timer = null;

  return function() \\{
    var context = this,
      args = arguments;

    // 如果此时存在定时器的话，则取消之前的定时器重新记时
    if (timer) \\{
      clearTimeout(timer);
      timer = null;
    \\}

    // 设置定时器，使事件间隔指定事件后执行
    timer = setTimeout(() => \\{
      fn.apply(context, args);
    \\}, wait);
  \\};
\\}

// 函数节流的实现;
function throttle(fn, delay) \\{
  var preTime = Date.now();

  return function() \\{
    var context = this,
      args = arguments,
      nowTime = Date.now();

    // 如果两次时间间隔超过了指定时间，则执行函数。
    if (nowTime - preTime >= delay) \\{
      preTime = Date.now();
      return fn.apply(context, args);
    \\}
  \\};
\\}
```

回答：

函数防抖是指在事件被触发 n 秒后再执行回调，如果在这 n 秒内事件又被触发，则重新计时。这可以使用在一些点击请求的事件上，避免因为用户的多次点击向后端发送多次请求。

函数节流是指规定一个单位时间，在这个单位时间内，只能有一次触发事件的回调函数执行，如果在同一个单位时间内某事件被触发多次，只有一次能生效。节流可以使用在 scroll 函数的事件监听上，通过事件节流来降低事件调用的频率。

详细资料可以参考：
[《轻松理解 JS 函数节流和函数防抖》](https://juejin.im/post/5a35ed25f265da431d3cc1b1)
[《JavaScript 事件节流和事件防抖》](https://juejin.im/post/5aa60b0e518825556b6c6d1a)
[《JS 的防抖与节流》](https://juejin.im/entry/5b1d2d54f265da6e2545bfa4)



### 防抖函数的作用是什么？请实现一个防抖函数

> 防抖函数的作用

防抖函数的作用就是控制函数在一定时间内的执行次数。防抖意味着N秒内函数只会被执行一次，如果N秒内再次被触发，则**重新**计算延迟时间。

**举例说明：** 小思最近在减肥，但是她非常吃吃零食。为此，与其男朋友约定好，如果10天不吃零食，就可以购买一个包(不要问为什么是包，因为**包治百病**)。但是如果中间吃了一次零食，那么就要重新计算时间，直到小思坚持10天没有吃零食，才能购买一个包。所以，管不住嘴的小思，没有机会买包(悲伤的故事)... 这就是 **防抖**。

> 防抖函数实现

1. 事件第一次触发时， `timer` 是 `null`，调用 `later()`，若 `immediate` 为 `true`，那么立即调用 `func.apply(this,params)`；如果 `immediate` 为 `false`，那么过 `wait` 之后，调用 `func.apply(this,params)`
2. 事件第二次触发时，如果 `timer` 已经重置为 `null`(即 `setTimeout` 的倒计时结束)，那么流程与第一次触发时一样，若 `timer` 不为 `null`(即 setTimeout 的倒计时未结束)，那么清空定时器，重新开始计时。

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5r1nYvEW7KljZ2HUYWmiaVDmUR2Ot0G96D0YcIDZbeRa9KiaXjdL61PzQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

`immediate` 为 true 时，表示函数在每个等待时延的开始被调用。 `immediate` 为 false 时，表示函数在每个等待时延的结束被调用。

> 防抖的应用场景

1. 搜索框输入查询，如果用户一直在输入中，没有必要不停地调用去请求服务端接口，等用户停止输入的时候，再调用，设置一个合适的时间间隔，有效减轻服务端压力。
2. 表单验证
3. 按钮提交事件。
4. 浏览器窗口缩放，resize事件(如窗口停止改变大小之后重新计算布局)等。



### 节流函数的作用是什么？有哪些应用场景，请实现一个节流函数

> 节流函数的作用

节流函数的作用是规定一个单位时间，在这个单位时间内最多只能触发一次函数执行，如果这个单位时间内多次触发函数，只能有一次生效。

> 节流函数实现

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5ZAg1icic6UibTQA8VKtwREjxo88BoH0XFoNXUZvAU0icST8tLCJXV39HCA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

禁用第一次首先执行，传递 `\\{leading:false\\}` ；想禁用最后一次执行，传递 `\\{trailing:false\\}`

> 节流的应用场景

1. 按钮点击事件
2. 拖拽事件
3. onScoll
4. 计算鼠标移动的距离(mousemove)





### new操作符

```
var New = function(Fn) \\{
  var obj = \\{\\}; // 创建空对象
  var arg = Array.prototype.slice.call(arguments, 1);
  obj.__proto__ = Fn.prototype; // 将obj的原型链__proto__指向构造函数的原型prototype
  obj.__proto__.constructor = Fn; // 在原型链 __proto__上设置构造函数的构造器constructor，为了实例化Fn
  Fn.apply(obj, arg); // 执行Fn，并将构造函数Fn执行obj
  return obj; // 返回结果
\\};

```



### 深拷贝

```
const getType = data => \\{
  // 获取数据类型
  const baseType = Object.prototype.toString
    .call(data)
    .replace(/^\[object\s(.+)\]$/g, "$1")
    .toLowerCase();
  const type = data instanceof Element ? "element" : baseType;
  return type;
\\};
const isPrimitive = data => \\{
  // 判断是否是基本数据类型
  const primitiveType = "undefined,null,boolean,string,symbol,number,bigint,map,set,weakmap,weakset".split(
    ","
  ); // 其实还有很多类型
  return primitiveType.includes(getType(data));
\\};
const isObject = data => getType(data) === "object";
const isArray = data => getType(data) === "array";
const deepClone = data => \\{
  let cache = \\{\\}; // 缓存值，防止循环引用
  const baseClone = _data => \\{
    let res;
    if (isPrimitive(_data)) \\{
      return data;
    \\} else if (isObject(_data)) \\{
      res = \\{ ..._data \\};
    \\} else if (isArray(_data)) \\{
      res = [..._data];
    \\}
    // 判断是否有复杂类型的数据，有就递归
    Reflect.ownKeys(res).forEach(key => \\{
      if (res[key] && getType(res[key]) === "object") \\{
        // 用cache来记录已经被复制过的引用地址。用来解决循环引用的问题
        if (cache[res[key]]) \\{
          res[key] = cache[res[key]];
        \\} else \\{
          cache[res[key]] = res[key];
          res[key] = baseClone(res[key]);
        \\}
      \\}
    \\});
    return res;
  \\};
  return baseClone(data);
\\};
```



### 手写bind

```
Function.prototype.bind2 = function(context) \\{
  if (typeof this !== "function") \\{
    throw new Error("...");
  \\}
  var that = this;
  var args1 = Array.prototype.slice.call(arguments, 1);
  var bindFn = function() \\{
    var args2 = Array.prototype.slice.call(arguments);
    var that2 = this instanceof bindFn ? this : context; // 如果当前函数的this指向的是构造函数中的this 则判定为new 操作。如果this是构造函数bindFn new出来的实例，那么此处的this一定是该实例本身。
    return that.apply(that2, args1.concat(args2));
  \\};
  var Fn = function() \\{\\}; // 连接原型链用Fn
  // 原型赋值
  Fn.prototype = this.prototype; // bindFn的prototype指向和this的prototype一样，指向同一个原型对象
  bindFn.prototype = new Fn();
  return bindFn;
\\};
```



### 手写函数柯里化

```
const curry = fn => \\{
  if (typeof fn !== "function") \\{
    throw Error("No function provided");
  \\}
  return function curriedFn(...args) \\{
    if (args.length < fn.length) \\{
      return function() \\{
        return curriedFn.apply(null, args.concat([].slice.call(arguments)));
      \\};
    \\}
    return fn.apply(null, args);
  \\};
\\};
```



### 手写 Promise

```
// 来源于 https://github.com/bailnl/promise/blob/master/src/promise.js
const PENDING = 0;
const FULFILLED = 1;
const REJECTED = 2;

const isFunction = fn => typeof fn === "function";
const isObject = obj => obj !== null && typeof obj === "object";
const noop = () => \\{\\};

const nextTick = fn => setTimeout(fn, 0);

const resolve = (promise, x) => \\{
  if (promise === x) \\{
    reject(promise, new TypeError("You cannot resolve a promise with itself"));
  \\} else if (x && x.constructor === Promise) \\{
    if (x._stauts === PENDING) \\{
      const handler = statusHandler => value => statusHandler(promise, value);
      x.then(handler(resolve), handler(reject));
    \\} else if (x._stauts === FULFILLED) \\{
      fulfill(promise, x._value);
    \\} else if (x._stauts === REJECTED) \\{
      reject(promise, x._value);
    \\}
  \\} else if (isFunction(x) || isObject(x)) \\{
    let isCalled = false;
    try \\{
      const then = x.then;
      if (isFunction(then)) \\{
        const handler = statusHandler => value => \\{
          if (!isCalled) \\{
            statusHandler(promise, value);
          \\}
          isCalled = true;
        \\};
        then.call(x, handler(resolve), handler(reject));
      \\} else \\{
        fulfill(promise, x);
      \\}
    \\} catch (e) \\{
      if (!isCalled) \\{
        reject(promise, e);
      \\}
    \\}
  \\} else \\{
    fulfill(promise, x);
  \\}
\\};

const reject = (promise, reason) => \\{
  if (promise._stauts !== PENDING) \\{
    return;
  \\}
  promise._stauts = REJECTED;
  promise._value = reason;
  invokeCallback(promise);
\\};

const fulfill = (promise, value) => \\{
  if (promise._stauts !== PENDING) \\{
    return;
  \\}
  promise._stauts = FULFILLED;
  promise._value = value;
  invokeCallback(promise);
\\};

const invokeCallback = promise => \\{
  if (promise._stauts === PENDING) \\{
    return;
  \\}
  nextTick(() => \\{
    while (promise._callbacks.length) \\{
      const \\{
        onFulfilled = value => value,
        onRejected = reason => \\{
          throw reason;
        \\},
        thenPromise
      \\} = promise._callbacks.shift();
      let value;
      try \\{
        value = (promise._stauts === FULFILLED ? onFulfilled : onRejected)(
          promise._value
        );
      \\} catch (e) \\{
        reject(thenPromise, e);
        continue;
      \\}
      resolve(thenPromise, value);
    \\}
  \\});
\\};

class Promise \\{
  static resolve(value) \\{
    return new Promise((resolve, reject) => resolve(value));
  \\}
  static reject(reason) \\{
    return new Promise((resolve, reject) => reject(reason));
  \\}
  constructor(resolver) \\{
    if (!(this instanceof Promise)) \\{
      throw new TypeError(
        `Class constructor Promise cannot be invoked without 'new'`
      );
    \\}

    if (!isFunction(resolver)) \\{
      throw new TypeError(`Promise resolver $\\{resolver\\} is not a function`);
    \\}

    this._stauts = PENDING;
    this._value = undefined;
    this._callbacks = [];

    try \\{
      resolver(value => resolve(this, value), reason => reject(this, reason));
    \\} catch (e) \\{
      reject(this, e);
    \\}
  \\}

  then(onFulfilled, onRejected) \\{
    const thenPromise = new this.constructor(noop);
    this._callbacks = this._callbacks.concat([
      \\{
        onFulfilled: isFunction(onFulfilled) ? onFulfilled : void 0,
        onRejected: isFunction(onRejected) ? onRejected : void 0,
        thenPromise
      \\}
    ]);
    invokeCallback(this);
    return thenPromise;
  \\}
  catch(onRejected) \\{
    return this.then(void 0, onRejected);
  \\}
\\}
```



### 手写 instanceOf

```
const instanceOf = (left, right) => \\{
  let proto = left.__proto__;
  let prototype = right.prototype;
  while (true) \\{
    if (proto === null) \\{
      return false;
    \\} else if (proto === prototype) \\{
      return true;
    \\}
    proto = proto.__proto__;
  \\}
\\};
```



### 简单实现 Function.bind 函数？

```javascript
  if (!Function.prototype.bind) \\{
    Function.prototype.bind = function(that) \\{
      var func = this, args = arguments;
      return function() \\{
        return func.apply(that, Array.prototype.slice.call(args, 1));
      \\}
    \\}
  \\}
  // 只支持 bind 阶段的默认参数：
  func.bind(that, arg1, arg2)();

  // 不支持以下调用阶段传入的参数：
  func.bind(that)(arg1, arg2);
```



### 实现一个 Function.bind

```js
Function.prototype.bind2 = function(context) \\{
  if (typeof this !== "function") \\{
    throw new Error(
      "Function.prototype.bind - what is trying to be bound is not callable"
    );
  \\}
  var self = this;
  var args = Array.prototype.slice.call(arguments, 1);
  var fNOP = function() \\{\\};
  var fbound = function() \\{
    self.apply(
      this instanceof self ? this : context,
      args.concat(Array.prototype.slice.call(arguments))
    );
  \\};
  fNOP.prototype = this.prototype;
  fbound.prototype = new fNOP();
  return fbound;
\\};
```



### 手写一个 promise

```js
var promise = new Promise((resolve, reject) => \\{
  if (success) \\{
    // 操作成功
    resolve(value);
  \\} else \\{
    reject(error);
  \\}
\\});

promise
  .then(res => console.log(res))
  .catch(err => \\{
    console.log(err);
  \\});
```



### 手写一个 Promise(中高级必考)

```js
function myPromise(constructor) \\{
  let self = this;
  self.status = "pending";
  //定义状态改变前的初始状态
  self.value = undefined;
  //定义状态为resolved的时候的状态
  self.reason = undefined;
  //定义状态为rejected的时候的状态
  function resolve(value) \\{
    //两个==="pending"，保证了状态的改变是不可逆的
    if (self.status === "pending") \\{
      self.value = value;
      self.status = "resolved";
    \\}
  \\}
  function reject(reason) \\{
    //两个==="pending"，保证了状态的改变是不可逆的
    if (self.status === "pending") \\{
      self.reason = reason;
      self.status = "rejected";
    \\}
  \\}
  //捕获构造异常
  try \\{
    constructor(resolve, reject);
  \\} catch (e) \\{
    reject(e);
  \\}
\\}

//同时，需要在 myPromise的原型上定义链式调用的 then方法：
myPromise.prototype.then = function(onFullfilled, onRejected) \\{
  let self = this;
  switch (self.status) \\{
    case "resolved":
      onFullfilled(self.value);
      break;
    case "rejected":
      onRejected(self.reason);
      break;
    default:
  \\}
\\};

//测试一下：
var p = new myPromise(function(resolve, reject) \\{
  resolve(1);
\\});
p.then(function(x) \\{
  console.log(x);
\\});
```



### 用 js 实现一个标准的排序算法

#### 一.冒泡排序

```
var bubble = function(arr)\\{
    var maxIndex = arr.length - 1, temp, flag;
    for (var i = maxIndex; i > 0; i--) \\{
        flag = true
        for (var j = 0; j < i; j++) \\{
            if (arr[j] > arr[j + 1]) \\{
                temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
                flag = false;
            \\}
        \\}
        if(! flag)\\{
            break;
        \\}
    \\}
    return arr;
\\}
// 调用
var arr = bubble([13, 69, 28, 93, 55, 75, 34]);
```

```js
function BubbleSort(arr) \\{
  for (var i = arr.length - 1; i > 0; i--) \\{
    //用于缩小范围
    for (var j = 0; j < i; j++) \\{
      //在范围内进行冒泡，在此范围内最大的一个将冒到最后面
      if (arr[j] > arr[j + 1]) \\{//从小到大
        var temp = arr[j];
        arr[j] = arr[j + 1];
        arr[j + 1] = temp;
      \\}
    \\}
    console.log(arr);
  \\}
  return arr;
\\}

var arr = [10, 9, 8, 7,6, 5,4, 3];
var result = BubbleSort(arr);
console.log(result);
/*
代码实际输出：
[ 9, 8, 7, 6, 5, 4, 3, 10 ]
[ 8, 7, 6, 5, 4, 3, 9, 10 ]
[ 7, 6, 5, 4, 3, 8, 9, 10 ]
[ 6, 5, 4, 3, 7, 8, 9, 10 ]
[ 5, 4, 3, 6, 7, 8, 9, 10 ]
[ 4, 3, 5, 6, 7, 8, 9, 10 ]
[ 3, 4, 5, 6, 7, 8, 9, 10 ]
[ 3, 4, 5, 6, 7, 8, 9, 10 ]
*/
```

```
// 冒泡排序
var bubbleSort = function( arr) \\{
    var len = arr.length;
    for( var i = 0; i < len; i ++)\\{
        for( var j = 0; i < len - 1 - i; i ++)\\{
            if(arr[j] > arr[j + 1]) \\{ //相邻元素两两对比
                var temp = arr[j + 1]; //元素交换
                arr[j + 1] = arr[j];
                arr[j] = temp;
            \\}
        \\}
    \\}
    return arr;
\\}
```

#### 二.选择排序

```js
function SelectionSort(array) \\{
  var length = array.length;
  for (var i = 0; i < length; i++) \\{
    //缩小选择的范围
    var min = array[i]; //假定范围内第一个为最小值
    var index = i; //记录最小值的下标
    for (var j = i + 1; j < length; j++) \\{
      //在范围内选取最小值
      if (array[j] < min) \\{
        min = array[j];
        index = j;
      \\}
    \\}
    if (index != i) \\{
      //把范围内最小值交换到范围内第一个
      var temp = array[i];
      array[i] = array[index];
      array[index] = temp;
    \\}
    console.log(array);
    console.log("---------------------");
  \\}
  return array;
\\}

var arr = [1, 10, 100, 90, 65, 5, 4, 10, 2, 4];
var result = SelectionSort(arr);
console.log(result);
/*
[ 1, 10, 100, 90, 65, 5, 4, 10, 2, 4 ]
---------------------
[ 1, 2, 100, 90, 65, 5, 4, 10, 10, 4 ]
---------------------
[ 1, 2, 4, 90, 65, 5, 100, 10, 10, 4 ]
---------------------
[ 1, 2, 4, 4, 65, 5, 100, 10, 10, 90 ]
---------------------
[ 1, 2, 4, 4, 5, 65, 100, 10, 10, 90 ]
---------------------
[ 1, 2, 4, 4, 5, 10, 100, 65, 10, 90 ]
---------------------
[ 1, 2, 4, 4, 5, 10, 10, 65, 100, 90 ]
---------------------
[ 1, 2, 4, 4, 5, 10, 10, 65, 100, 90 ]
---------------------
[ 1, 2, 4, 4, 5, 10, 10, 65, 90, 100 ]
---------------------
[ 1, 2, 4, 4, 5, 10, 10, 65, 90, 100 ]
---------------------
[ 1, 2, 4, 4, 5, 10, 10, 65, 90, 100 ]
*/
```

#### 三.插入排序

```js
function InsertionSort(array) \\{
  var length = array.length;
  for (var i = 0; i < length - 1; i++) \\{
    //i代表已经排序好的序列最后一项下标
    var insert = array[i + 1];
    var index = i + 1; //记录要被插入的下标
    for (var j = i; j >= 0; j--) \\{
      if (insert < array[j]) \\{
        //要插入的项比它小，往后移动
        array[j + 1] = array[j];
        index = j;
      \\}
    \\}
    array[index] = insert;
    console.log(array);
    console.log("-----------------------");
  \\}
  return array;
\\}

var arr = [100, 90, 80, 62, 80, 8, 1, 2, 39];
var result = InsertionSort(arr);
console.log(result);
/*
[ 90, 100, 80, 62, 80, 8, 1, 2, 39 ]
-----------------------
[ 80, 90, 100, 62, 80, 8, 1, 2, 39 ]
-----------------------
[ 62, 80, 90, 100, 80, 8, 1, 2, 39 ]
-----------------------
[ 62, 80, 80, 90, 100, 8, 1, 2, 39 ]
-----------------------
[ 8, 62, 80, 80, 90, 100, 1, 2, 39 ]
-----------------------
[ 1, 8, 62, 80, 80, 90, 100, 2, 39 ]
-----------------------
[ 1, 2, 8, 62, 80, 80, 90, 100, 39 ]
-----------------------
[ 1, 2, 8, 39, 62, 80, 80, 90, 100 ]
-----------------------
[ 1, 2, 8, 39, 62, 80, 80, 90, 100 ]
*/
```

```
// 插入排序
var insertSort = function( arr) \\{
    var len = arr.length;
    var preIndex, current;
    for( var i = 1; i < len; i ++)\\{
        preIndex = i - 1;
        current = arr[i];
        while(preIndex >= 0 && arr[preIndex] > current)\\{
            arr[preIndex + 1] = arr[preIndex];
            preIndex --;
        \\}
        arr[preIndex + 1] = current;
    \\}
    return arr;
\\}
```

#### 四.希尔排序

#### 五.归并排序

#### 六.快速排序

```
var quickSort = function( arr) \\{
    if(arr.length < 1) \\{ //如果数组就是一项，那么可以直接返回
        return arr;
    \\}
    var centerIndex = Math. floor(arr.length / 2); //获取数组中间的索引
    var centerValue = arr[centerIndex]; //获取数组中间项
    var left = [], right = [];
    for( var i = 0; i < arr.lenght; i ++)\\{
        if(arr[i] < centerValue)\\{
            left. push(arr[i]);
        \\} else\\{
            right. push(arr[i]);
        \\}
    \\}
    return quickSort(left). contanct([centerValue], quickSort(right)); //递归调用
\\}
```



### 手写数组快速排序

```JavaScript
var quickSort = function(arr) \\{
    if (arr.length <= 1) \\{ return arr; \\}
    var pivotIndex = Math.floor(arr.length / 2);
    var pivot = arr.splice(pivotIndex, 1)[0];
    var left = [];
    var right = [];
    for (var i = 0, len = arr.length; i < len; i++)\\{
        if (arr[i] < pivot) \\{
          left.push(arr[i]);
        \\} else \\{
          right.push(arr[i]);
        \\}
    \\}
    return quickSort(left).concat([pivot], quickSort(right));
\\};

// 调用
quickSort([9, 4, 2, 8, 1, 5, 3, 7]);
```



### 如何实现数组的随机排序？

- 方法一：

```javascript
var arr = [1,2,3,4,5,6,7,8,9,10];
function randSort1(arr)\\{
	for(var i = 0,len = arr.length;i < len; i++ )\\{
		var rand = parseInt(Math.random()*len);
		var temp = arr[rand];
		arr[rand] = arr[i];
		arr[i] = temp;
	\\}
	return arr;
\\}
console.log(randSort1(arr));

```

- 方法二：


```javascript
var arr = [1,2,3,4,5,6,7,8,9,10];
function randSort2(arr)\\{
	var mixedArray = [];
	while(arr.length > 0)\\{
		var randomIndex = parseInt(Math.random()*arr.length);
		mixedArray.push(arr[randomIndex]);
		arr.splice(randomIndex, 1);
	\\}
	return mixedArray;
\\}
console.log(randSort2(arr));

```

- 方法三：


```javascript
var arr = [1,2,3,4,5,6,7,8,9,10];
arr.sort(function()\\{
	return Math.random() - 0.5;
\\})
console.log(arr);
```



### 用 js 实现随机选取 10–100 之间的 10 个数字，存入一个数组，并排序。

```js
var iArray = [];
funtion getRandom(istart, iend)\\{
var iChoice = istart - iend +1;
return Math.floor(Math.random() * iChoice + istart;
\\}
for(var i=0; i<10; i++)\\{
iArray.push(getRandom(10,100));
\\}
iArray.sort();
```



### 手写防抖(Debouncing)和节流(Throttling)

```js
// 防抖函数
function debounce(fn, wait) \\{
  let timer;
  return function() \\{
    if (timer) clearTimeout(timer);
    timer = setTimeout(() => \\{
      fn.apply(this, arguments);
    \\}, wait);
  \\};
\\}
```

```js
// 节流函数
function throttle(fn, wait) \\{
  let prev = new Date();
  return function() \\{
    const args = arguments;
    const now = new Date();
    if (now - prev > wait) \\{
      fn.apply(this, args);
      prev = new Date();
    \\}
  \\};
\\}
```



### 实现防抖函数（debounce）

防抖函数原理：在事件被触发n秒后再执行回调，如果在这n秒内又被触发，则重新计时。

那么与节流函数的区别直接看这个动画实现即可。

手写简化版:

```
// 防抖函数
const debounce = (fn, delay) => \\{
  let timer = null;
  return (...args) => \\{
    clearTimeout(timer);
    timer = setTimeout(() => \\{
      fn.apply(this, args);
    \\}, delay);
  \\};
\\};
```

适用场景：

- 按钮提交场景：防止多次提交按钮，只执行最后提交的一次
- 服务端验证场景：表单验证需要服务端配合，只执行一段连续的输入事件的最后一次，还有搜索联想词功能类似

生存环境请用lodash.debounce



### 实现节流函数（throttle）

防抖函数原理:规定在一个单位时间内，只能触发一次函数。如果这个单位时间内触发多次函数，只有一次生效。

// 手写简化版

```
// 节流函数
const throttle = (fn, delay = 500) => \\{
  let flag = true;
  return (...args) => \\{
    if (!flag) return;
    flag = false;
    setTimeout(() => \\{
      fn.apply(this, args);
      flag = true;
    \\}, delay);
  \\};
\\};
```

适用场景：

- 拖拽场景：固定时间内只执行一次，防止超高频次触发位置变动
- 缩放场景：监控浏览器resize
- 动画场景：避免短时间内多次触发动画引起性能问题



### 手写一个 JS 深拷贝

```js
function deepCopy(obj) \\{
  //判断是否是简单数据类型，
  if (typeof obj == "object") \\{
    //复杂数据类型
    var result = obj.constructor == Array ? [] : \\{\\};
    for (let i in obj) \\{
      result[i] = typeof obj[i] == "object" ? deepCopy(obj[i]) : obj[i];
    \\}
  \\} else \\{
    //简单数据类型 直接 == 赋值
    var result = obj;
  \\}
  return result;
\\}
```

```js
let o1 = \\{
  a: \\{
    b: 1
  \\}
\\};
let o2 = JSON.parse(JSON.stringify(o1));
```

另一种方法

```js
function deepCopy(s) \\{
  const d = \\{\\};
  for (let k in s) \\{
    if (typeof s[k] == "object") \\{
      d[k] = deepCopy(s[k]);
    \\} else \\{
      d[k] = s[k];
    \\}
  \\}
  return d;
\\}
```



### 如何封装一个 javascript 的类型判断函数？

```js
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
    return typeof value;
  \\}
\\}
```

详细资料可以参考：
[《JavaScript 专题之类型判断(上)》](https://github.com/mqyqingfeng/Blog/issues/28)



### 如何判断一个对象是否为空对象？

```js
function checkNullObj(obj) \\{
  return Object.keys(obj).length === 0 && Object.getOwnPropertySymbols(obj).length === 0;
\\}
```

详细资料可以参考：
[《js 判断一个 object 对象是否为空》](https://blog.csdn.net/FungLeo/article/details/78113661)



### 使用闭包实现每隔一秒打印 1,2,3,4

```js
// 使用闭包实现
for (var i = 0; i < 5; i++) \\{
  (function(i) \\{
    setTimeout(function() \\{
      console.log(i);
    \\}, i * 1000);
  \\})(i);
\\}

// 使用 let 块级作用域

for (let i = 0; i < 5; i++) \\{
  setTimeout(function() \\{
    console.log(i);
  \\}, i * 1000);
\\}
```



### 手写一个 jsonp

```js
function jsonp(url, params, callback) \\{
  // 判断是否含有参数
  let queryString = url.indexOf("?") === -1 ? "?" : "&";

  // 添加参数
  for (var k in params) \\{
    if (params.hasOwnProperty(k)) \\{
      queryString += k + "=" + params[k] + "&";
    \\}
  \\}

  // 处理回调函数名
  let random = Math.random()
      .toString()
      .replace(".", ""),
    callbackName = "myJsonp" + random;

  // 添加回调函数
  queryString += "callback=" + callbackName;

  // 构建请求
  let scriptNode = document.createElement("script");
  scriptNode.src = url + queryString;

  window[callbackName] = function() \\{
    // 调用回调函数
    callback(...arguments);

    // 删除这个引入的脚本
    document.getElementsByTagName("head")[0].removeChild(scriptNode);
  \\};

  // 发起请求
  document.getElementsByTagName("head")[0].appendChild(scriptNode);
\\}
```

详细资料可以参考：
[《原生 jsonp 具体实现》](https://www.cnblogs.com/zzc5464/p/jsonp.html)
[《jsonp 的原理与实现》](https://segmentfault.com/a/1190000007665361#articleHeader1)



### 手写一个观察者模式？

```js
var events = (function() \\{
  var topics = \\{\\};

  return \\{
    // 注册监听函数
    subscribe: function(topic, handler) \\{
      if (!topics.hasOwnProperty(topic)) \\{
        topics[topic] = [];
      \\}
      topics[topic].push(handler);
    \\},

    // 发布事件，触发观察者回调事件
    publish: function(topic, info) \\{
      if (topics.hasOwnProperty(topic)) \\{
        topics[topic].forEach(function(handler) \\{
          handler(info);
        \\});
      \\}
    \\},

    // 移除主题的一个观察者的回调事件
    remove: function(topic, handler) \\{
      if (!topics.hasOwnProperty(topic)) return;

      var handlerIndex = -1;
      topics[topic].forEach(function(item, index) \\{
        if (item === handler) \\{
          handlerIndex = index;
        \\}
      \\});

      if (handlerIndex >= 0) \\{
        topics[topic].splice(handlerIndex, 1);
      \\}
    \\},

    // 移除主题的所有观察者的回调事件
    removeAll: function(topic) \\{
      if (topics.hasOwnProperty(topic)) \\{
        topics[topic] = [];
      \\}
    \\}
  \\};
\\})();
```

详细资料可以参考：
[《JS 事件模型》](https://segmentfault.com/a/1190000006934031#articleHeader1)



### EventEmitter 实现

```js
class EventEmitter \\{
  constructor() \\{
    this.events = \\{\\};
  \\}

  on(event, callback) \\{
    let callbacks = this.events[event] || [];
    callbacks.push(callback);
    this.events[event] = callbacks;

    return this;
  \\}

  off(event, callback) \\{
    let callbacks = this.events[event];
    this.events[event] = callbacks && callbacks.filter(fn => fn !== callback);

    return this;
  \\}

  emit(event, ...args) \\{
    let callbacks = this.events[event];
    callbacks.forEach(fn => \\{
      fn(...args);
    \\});

    return this;
  \\}

  once(event, callback) \\{
    let wrapFun = (...args) => \\{
      callback(...args);

      this.off(event, wrapFun);
    \\};
    this.on(event, wrapFun);

    return this;
  \\}
\\}
```



### 一道常被人轻视的前端 JS 面试题

```js
function Foo() \\{
  getName = function() \\{
    alert(1);
  \\};
  return this;
\\}
Foo.getName = function() \\{
  alert(2);
\\};
Foo.prototype.getName = function() \\{
  alert(3);
\\};
var getName = function() \\{
  alert(4);
\\};
function getName() \\{
  alert(5);
\\}

//请写出以下输出结果：
Foo.getName(); // 2
getName(); // 4
Foo().getName(); // 1
getName(); // 1
new Foo.getName(); // 2
new Foo().getName(); // 3
new new Foo().getName(); // 3
```

详细资料可以参考：
[《前端程序员经常忽视的一个 JavaScript 面试题》](https://github.com/Wscats/Good-text-Share/issues/85)
[《一道考察运算符优先级的 JavaScript 面试题》](https://segmentfault.com/q/1010000008430170)
[《一道常被人轻视的前端 JS 面试题》](https://www.cnblogs.com/xxcanghai/p/5189353.html)



### 如何查找一篇英文文章中出现频率最高的单词？

```js
function findMostWord(article) \\{
  // 合法性判断
  if (!article) return;

  // 参数处理
  article = article.trim().toLowerCase();

  let wordList = article.match(/[a-z]+/g),
    visited = [],
    maxNum = 0,
    maxWord = "";

  article = " " + wordList.join("  ") + " ";

  // 遍历判断单词出现次数
  wordList.forEach(function(item) \\{
    if (visited.indexOf(item) < 0) \\{

      // 加入 visited 
      visited.push(item);

      let word = new RegExp(" " + item + " ", "g"),
        num = article.match(word).length;

      if (num > maxNum) \\{
        maxNum = num;
        maxWord = item;
      \\}
    \\}
  \\});

  return maxWord + "  " + maxNum;
\\}
```



### 用最简单的方式，求一个数组中最大的元素，例如 arr=[5,7,9,42,18,29]

```js
var a = [1, 2, 3, 5];
alert(Math.max.apply(null, a)); //最大值
alert(Math.min.apply(null, a)); //最小值
```



### 如何解决数组塌陷问题

```js
// 1 使用i--
for (var i = 0; i < arr.length; i++) \\{
  if (arr[i] === 4) \\{
    arr.splice(i, 1);
    i--;
  \\}
\\}
console.log(arr);

// 2 从数组的末尾一项开始遍历
for (var i = arr.length; i >= 0; i--) \\{
  if (arr[i] === 4) \\{
    arr.splice(i, 1);
  \\}
\\}
console.log(arr);
```



### 已知 id 的 input 输入框，希望获取这个输入框的输入值，怎么做？（不使用第三方框架）

```js
document.getElementById("id").value;
```



### 获取到页面中所有的 checkbox 怎么做？（不使用第三方框架）

```js
var domList = document.getElementsByTagName("input");
var ckList = []; // 返回的所有的 checkbox
var len = domList.length;
for (var i = 0; i < len; i++) \\{
  if (domList[i].type == "checkbox") \\{
    ckList.push(domList[i]);
  \\}
\\}
```



### 设置一个已知 id 的 div 的 html 内容为 xxxx，字体颜色设置为黑色（不使用第三方框架）

```js
var dom = document.getElementById("id");
dom.innerHTML = "xxxx";
dom.style.color = "#000"; // 'black'
```



### 已知有字符串 foo=“get-element-by-id”,写一个 function 将其转化为驼峰表示法“getElementById”

```js
var string = "get-element-by-id";

function combo(msg) \\{
  var arr = msg.split("-"); //split("-")以-为分隔符截取字符串，返回数组
  for (var i = 1; i < arr.length; i++) \\{
    arr[i] = arr[i].charAt(0).toUpperCase() + arr[i].slice(1);
  \\}
  msg = arr.join(""); //join()返回字符串
  return msg;
\\}
console.log(combo(string));
```



### 写一个 function，清除字符串前后的空格（兼容所有的浏览器）

```js
//重写trim方法
if (!String.prototype.trim) \\{
  String.prototype.trim = function() \\{
    return this.replace(/^\s+/, "").replace(/\s+$/, "");
  \\};
\\}
```



### 运算符面试题

```js
var a = 10,
  b = 20,
  c = 30;
++a;
a++;
e = ++a + ++b + c++ + a++;
console.log(e); // 77
```



### 判断相等

2 == true
[] == false
[] == ![]



### 闭包

```js
for (var i = 1; i <= 3; i++) \\{
  setTimeout(
    (() => \\{
      var j = i;
      return function() \\{
        console.log(j);
      \\};
    \\})(),
    0
  );
\\}
```



### 实现一个 new 操作符

```js
function New(func) \\{
  var res = \\{\\};
  if (func.prototype !== null) \\{
    res.__proto__ = func.prototype;
  \\}
  var ret = func.apply(res, Array.prototype.slice.call(arguments, 1));
  if ((typeof ret === "object" || typeof ret === "function") && ret !== null) \\{
    return;
    ret;
  \\}
  return;
  res;
\\}
var obj = New(A, 1, 2);
// equals to
var obj = new A(1, 2);
```



### 实现一个 call 或 apply

答案：
call

```js
Function.prototype.call2 = function(context) \\{
  var context = context || window;
  context.fn = this;

  var args = [];
  for (var i = 1, len = arguments.length; i < len; i++) \\{
    args.push("arguments[" + i + "]");
  \\}

  var result = eval("context.fn(" + args + ")");

  delete context.fn;
  return result;
\\};
```

apply

```js
Function.prototype.apply2 = function(context, arr) \\{
  var context = Object(context) || window;
  context.fn = this;

  var result;
  if (!arr) \\{
    result = context.fn();
  \\} else \\{
    var args = [];
    for (var i = 0, len = arr.length; i < len; i++) \\{
      args.push("arr[" + i + "]");
    \\}
    result = eval("context.fn(" + args + ")");
  \\}

  delete context.fn;
  return result;
\\};
```



### 原型链面试题

```js
// 1
function A() \\{\\}
function B() \\{\\}
B.prototype = new A();
var a = new A();
B.prototype = a;
var b = new B();
console.log(b.constructor); // 构造函数A

//2

console.log(Function.constructor === Function);
// Function 是一个构造函数
console.log(Function.__proto__.constructor === Function);

// 默认原型上面的constructor属性指向了原型所在的构造函数。

console.log(Object.constructor === Function);
// Object本身没有constructor这个属性，那么就到它的原型链上去查找，
Object.__proto__ === Function.prototype;

console.log(Function.__proto__.__proto__ === Object.prototype);
Function.__proto__ === Function.prototype;
Function.prototype.__proto__ === Object.prototype;
```



```js
var o = new Object();
function foo(obj) \\{
  obj.name = "腐女";
  obj = new Object();
  obj.name = "屌丝"; //这是另一个新对象的name
\\}
foo(o);
console.log(o.name); //想要的是原来对象的name，所以输出腐女
```



### 实现一个继承

```js
function Parent(name) \\{
  this.name = name;
\\}

Parent.prototype.sayName = function() \\{
  console.log("parent name:", this.name);
\\};

function Child(name, parentName) \\{
  Parent.call(this, parentName);
  this.name = name;
\\}

function create(proto) \\{
  function F() \\{\\}
  F.prototype = proto;
  return new F();
\\}
Child.prototype = create(Parent.prototype);
Child.prototype.sayName = function() \\{
  console.log("child name:", this.name);
\\};

Child.prototype.constructor = Child;
var parent = new Parent("汪某");
parent.sayName(); // parent name: 汪某
var child = new Child("son", "汪某");
```



### 编写一个方法 求一个字符串的字节长度

假设：一个英文字符占用一个字节，一个中文字符占用两个字节    

```
function GetBytes(str)\\{
        var len = str.length;
        var bytes = len;
        for(var i=0; i<len; i++)\\{
            if (str.charCodeAt(i) > 255) bytes++;
        \\}
        return bytes;
    \\}
alert(GetBytes("你好,as"));
```



### 写一个通用的事件侦听器函数

```
 // event(事件)工具集，来源：github.com/markyun
    markyun.Event = \\{
        // 页面加载完成后
        readyEvent : function(fn) \\{
            if (fn==null) \\{
                fn=document;
            \\}
            var oldonload = window.onload;
            if (typeof window.onload != 'function') \\{
                window.onload = fn;
            \\} else \\{
                window.onload = function() \\{
                    oldonload();
                    fn();
                \\};
            \\}
        \\},
        // 视能力分别使用dom0||dom2||IE方式 来绑定事件
        // 参数： 操作的元素,事件名称 ,事件处理程序
        addEvent : function(element, type, handler) \\{
            if (element.addEventListener) \\{
                //事件类型、需要执行的函数、是否捕捉
                element.addEventListener(type, handler, false);
            \\} else if (element.attachEvent) \\{
                element.attachEvent('on' + type, function() \\{
                    handler.call(element);
                \\});
            \\} else \\{
                element['on' + type] = handler;
            \\}
        \\},
        // 移除事件
        removeEvent : function(element, type, handler) \\{
            if (element.removeEventListener) \\{
                element.removeEventListener(type, handler, false);
            \\} else if (element.datachEvent) \\{
                element.detachEvent('on' + type, handler);
            \\} else \\{
                element['on' + type] = null;
            \\}
        \\},
        // 阻止事件 (主要是事件冒泡，因为IE不支持事件捕获)
        stopPropagation : function(ev) \\{
            if (ev.stopPropagation) \\{
                ev.stopPropagation();
            \\} else \\{
                ev.cancelBubble = true;
            \\}
        \\},
        // 取消事件的默认行为
        preventDefault : function(event) \\{
            if (event.preventDefault) \\{
                event.preventDefault();
            \\} else \\{
                event.returnValue = false;
            \\}
        \\},
        // 获取事件目标
        getTarget : function(event) \\{
            return event.target || event.srcElement;
        \\},
        // 获取event对象的引用，取到事件的所有信息，确保随时能使用event；
        getEvent : function(e) \\{
            var ev = e || window.event;
            if (!ev) \\{
                var c = this.getEvent.caller;
                while (c) \\{
                    ev = c.arguments[0];
                    if (ev && Event == ev.constructor) \\{
                        break;
                    \\}
                    c = c.caller;
                \\}
            \\}
            return ev;
        \\}
    \\};
```



### 写一个通用的事件侦听器函数

```js
// event(事件)工具集，来源：https://github.com/markyun
markyun.Event = \\{
  // 页面加载完成后
  readyEvent: function(fn) \\{
    if (fn == null) \\{
      fn = document;
    \\}
    var oldonload = window.onload;
    if (typeof window.onload != "function") \\{
      window.onload = fn;
    \\} else \\{
      window.onload = function() \\{
        oldonload();
        fn();
      \\};
    \\}
  \\},
  // 视能力分别使用dom0||dom2||IE方式 来绑定事件
  // 参数： 操作的元素,事件名称 ,事件处理程序
  addEvent: function(element, type, handler) \\{
    if (element.addEventListener) \\{
      //事件类型、需要执行的函数、是否捕捉
      element.addEventListener(type, handler, false);
    \\} else if (element.attachEvent) \\{
      element.attachEvent("on" + type, function() \\{
        handler.call(element);
      \\});
    \\} else \\{
      element["on" + type] = handler;
    \\}
  \\},
  // 移除事件
  removeEvent: function(element, type, handler) \\{
    if (element.removeEnentListener) \\{
      element.removeEnentListener(type, handler, false);
    \\} else if (element.datachEvent) \\{
      element.detachEvent("on" + type, handler);
    \\} else \\{
      element["on" + type] = null;
    \\}
  \\},
  // 阻止事件 (主要是事件冒泡，因为IE不支持事件捕获)
  stopPropagation: function(ev) \\{
    if (ev.stopPropagation) \\{
      ev.stopPropagation();
    \\} else \\{
      ev.cancelBubble = true;
    \\}
  \\},
  // 取消事件的默认行为
  preventDefault: function(event) \\{
    if (event.preventDefault) \\{
      event.preventDefault();
    \\} else \\{
      event.returnValue = false;
    \\}
  \\},
  // 获取事件目标
  getTarget: function(event) \\{
    return event.target || event.srcElement;
  \\},
  // 获取event对象的引用，取到事件的所有信息，确保随时能使用event；
  getEvent: function(e) \\{
    var ev = e || window.event;
    if (!ev) \\{
      var c = this.getEvent.caller;
      while (c) \\{
        ev = c.arguments[0];
        if (ev && Event == ev.constructor) \\{
          break;
        \\}
        c = c.caller;
      \\}
    \\}
    return ev;
  \\}
\\};
```



### 手写事件侦听器，并要求兼容浏览器

```JavaScript
var eventUtil = \\{
  getEvent: function(event) \\{
      return event || window.event;
  \\},

  getTarget: function(event) \\{
      return event.target || event.srcElement;
  \\},

  addListener: function(element, type, hander) \\{
      if (element.addEventListener) \\{
          element.addEventListener(type, hander, false);
      \\} else if (element.attachEvent) \\{
          element.attachEvent('on' + type, hander);
      \\} else \\{
          element['on' + type] = hander;
      \\}
  \\},

  removeListener: function(element, type, hander) \\{
      if (element.removeEventListener) \\{
          element.removeEventListener(type, hander, false);
      \\} else if (element.deattachEvent) \\{
          element.detachEvent(type, hander);
      \\} else \\{
          element['on' + type] = null;
      \\}
  \\},

  preventDefault: function(event) \\{
      if (event.preventDefault) \\{
          event.preventDefault();
      \\} else \\{
          event.returnValue = false;
      \\}
  \\},

  stopPropagation: function(event) \\{
      if (event.stopPropagation) \\{
          event.stopPropagation();
      \\} else \\{
          event.cancelBubble = true;
      \\}
  \\}
\\};

// 调用
(function() \\{
  var btn = document.getElementById("btn");
  var link = document.getElementsByTagName("a")[0];

  eventUtil.addListener(btn, "click", function(event) \\{
      var event = eventUtil.getEvent(event);
      var target = eventUtil.getTarget(event);
      alert(event.type);
      alert(target);
      eventUtil.stopPropagation(event);
  \\});

  eventUtil.addListener(link, "click", function(event) \\{
      alert("prevent default event");
      var event = eventUtil.getEvent(event);
      eventUtil.preventDefault(event);
  \\});

  eventUtil.addListener(document.body, "click", function() \\{
      alert("click body");
  \\});
\\})();
```



### 写一个通用的事件侦听器函数。

```
// event(事件)工具集，来源：github.com/markyun
markyun.Event = \\{
	// 页面加载完成后
	readyEvent : function(fn) \\{
		if (fn==null) \\{
			fn=document;
		\\}
		var oldonload = window.onload;
		if (typeof window.onload != 'function') \\{
			window.onload = fn;
		\\} else \\{
			window.onload = function() \\{
				oldonload();
				fn();
			\\};
		\\}
	\\},
	// 视能力分别使用dom0||dom2||IE方式 来绑定事件
	// 参数： 操作的元素,事件名称 ,事件处理程序
	addEvent : function(element, type, handler) \\{
		if (element.addEventListener) \\{
			//事件类型、需要执行的函数、是否捕捉
			element.addEventListener(type, handler, false);
		\\} else if (element.attachEvent) \\{
			element.attachEvent('on' + type, function() \\{
				handler.call(element);
			\\});
		\\} else \\{
			element['on' + type] = handler;
		\\}
	\\},
	// 移除事件
	removeEvent : function(element, type, handler) \\{
		if (element.removeEventListener) \\{
			element.removeEventListener(type, handler, false);
		\\} else if (element.datachEvent) \\{
			element.detachEvent('on' + type, handler);
		\\} else \\{
			element['on' + type] = null;
		\\}
	\\},
	// 阻止事件 (主要是事件冒泡，因为IE不支持事件捕获)
	stopPropagation : function(ev) \\{
		if (ev.stopPropagation) \\{
			ev.stopPropagation();
		\\} else \\{
			ev.cancelBubble = true;
		\\}
	\\},
	// 取消事件的默认行为
	preventDefault : function(event) \\{
		if (event.preventDefault) \\{
			event.preventDefault();
		\\} else \\{
			event.returnValue = false;
		\\}
	\\},
	// 获取事件目标
	getTarget : function(event) \\{
		return event.target || event.srcElement;
	\\},
	// 获取event对象的引用，取到事件的所有信息，确保随时能使用event；
	getEvent : function(e) \\{
		var ev = e || window.event;
		if (!ev) \\{
			var c = this.getEvent.caller;
			while (c) \\{
				ev = c.arguments[0];
				if (ev && Event == ev.constructor) \\{
					break;
				\\}
				c = c.caller;
			\\}
		\\}
		return ev;
	\\}
\\};
```



### 手写事件模型

```JavaScript
var Event = (function () \\{
    var list = \\{\\}, bind, trigger, remove;
    bind = function (key, fn) \\{
        if (!list[key]) \\{
            list[key] = [];
        \\}
        list[key].push(fn);
    \\};
    trigger = function () \\{
        var key = Array.prototype.shift.call(arguments);
        var fns = list[key];
        if (!fns || fns.length === 0) \\{
            return false;
        \\}
        for (var i = 0, fn; fn = fns[i++];) \\{
            fn.apply(this, arguments);
        \\}
    \\};
    remove = function (key, fn) \\{
        var fns = list[key];
        if (!fns) \\{
            return false;
        \\}
        if (!fn) \\{
            fns & (fns.length = 0);
        \\} else \\{
            for (var i = fns.length - 1; i >= 0; i--) \\{
                var _fn = fns[i];
                if (_fn === fn) \\{
                    fns.splice(i, 1);
                \\}
            \\}
        \\}
    \\};
    return \\{
        bind: bind,
        trigger: trigger,
        remove: remove
    \\}
\\})();

// 调用
Event.bind('Hit', function()\\{ console.log('bind event'); \\}); // 绑定事件
Event.trigger("Hit", function()\\{ console.log('trigger event'); \\}); // 触发事件
```



### 手写事件代理，并要求兼容浏览器

```JavaScript
function delegateEvent(parentEl, selector, type, fn) \\{
    var handler = function(e)\\{
          var e = e || window.event;
          var target = e.target || e.srcElement;
          if (matchSelector(target, selector)) \\{
              if(fn) \\{
                  fn.call(target, e);
              \\}
          \\}
    \\};
    if(parentEl.addEventListener)\\{
        parentEl.addEventListener(type, handler);
    \\}else\\{
        parentEl.attachEvent("on" + type, handler);
    \\}
\\}
/**
 * support #id, tagName, .className
 */
function matchSelector(ele, selector) \\{
    // if use id
    if (selector.charAt(0) === "#") \\{
        return ele.id === selector.slice(1);
    \\}
    // if use class
    if (selector.charAt(0) === ".") \\{
        return (" " + ele.className + " ").indexOf(" " + selector.slice(1) + " ") != -1;
    \\}
    // if use tagName
    return ele.tagName.toLowerCase() === selector.toLowerCase();
\\}

// 调用
var box = document.getElementById("box");
delegateEvent(box, "a", "click", function()\\{
    console.log(this.href);
\\})
```



### 手写事件触发器，并要求兼容浏览器

```JavaScript
var fireEvent = function(element, event)\\{
    if (document.createEventObject)\\{
        var mockEvent = document.createEventObject();
        return element.fireEvent('on' + event, mockEvent)
    \\}else\\{
        var mockEvent = document.createEvent('HTMLEvents');
        mockEvent.initEvent(event, true, true);
        return element.dispatchEvent(mockEvent);
    \\}
\\}
```



### 手写 Function.bind 函数

```JavaScript
if (!Function.prototype.bind) \\{
  Function.prototype.bind = function (oThis) \\{
    if (typeof this !== "function") \\{
      throw new TypeError("'this' is not function");
    \\}

    // bind's default arguments, array without first element
    // first part arguments for the function
    var aBindArgs = Array.prototype.slice.call(arguments, 1);
    var fToBind = this; // the function will be binding
    var fNOP = function () \\{\\};
    var fBound = function () \\{
          // target this will be binding
          var oThis = this instanceof fNOP ? this : oThis || this;
          // last part arguments for the function
          var aCallArgs = Array.prototype.slice.call(arguments);
          // complete arguments for the function
          var aFuncArgs = aBindArgs.concat(aCallArgs);
          return fToBind.apply(oThis, aFuncArgs);
        \\};

    // fBound extends fToBind
    fNOP.prototype = this.prototype;
    fBound.prototype = new fNOP();

    return fBound;
  \\};
\\}

// 调用
var add = function(a, b, c)\\{ return a + b + c;\\};
var newAdd = add.bind(null, 1, 2);
var result = newAdd(3);
```



### JS实现数组去重方法总结(六种方法)

#### 方法一：

双层循环，外层循环元素，内层循环时比较值

如果有相同的值则跳过，不相同则push进数组

```
Array.prototype.distinct = function()\\{
 var arr = this,
  result = [],
  i,
  j,
  len = arr.length;
 for(i = 0; i < len; i++)\\{
  for(j = i + 1; j < len; j++)\\{
   if(arr[i] === arr[j])\\{
    j = ++i;
   \\}
  \\}
  result.push(arr[i]);
 \\}
 return result;
\\}
var arra = [1,2,3,4,4,1,1,2,1,1,1];
arra.distinct();    //返回[3,4,2,1]
```

#### 方法二：利用splice直接在原数组进行操作

双层循环，外层循环元素，内层循环时比较值

值相同时，则删去这个值

注意点:删除元素之后，需要将数组的长度也减1.

```
Array.prototype.distinct = function ()\\{
 var arr = this,
  i,
  j,
  len = arr.length;
 for(i = 0; i < len; i++)\\{
  for(j = i + 1; j < len; j++)\\{
   if(arr[i] == arr[j])\\{
    arr.splice(j,1);
    len--;
    j--;
   \\}
  \\}
 \\}
 return arr;
\\};
var a = [1,2,3,4,5,6,5,3,2,4,56,4,1,2,1,1,1,1,1,1,];
var b = a.distinct();
console.log(b.toString()); //1,2,3,4,5,6,56
```

优点：简单易懂

缺点：占用内存高，速度慢

#### 方法三：利用对象的属性不能相同的特点进行去重

```
Array.prototype.distinct = function ()\\{
 var arr = this,
  i,
  obj = \\{\\},
  result = [],
  len = arr.length;
 for(i = 0; i< arr.length; i++)\\{
  if(!obj[arr[i]])\\{ //如果能查找到，证明数组元素重复了
   obj[arr[i]] = 1;
   result.push(arr[i]);
  \\}
 \\}
 return result;
\\};
var a = [1,2,3,4,5,6,5,3,2,4,56,4,1,2,1,1,1,1,1,1,];
var b = a.distinct();
console.log(b.toString()); //1,2,3,4,5,6,56
```

#### 方法四：数组递归去重

运用递归的思想

先排序，然后从最后开始比较，遇到相同，则删除

```
Array.prototype.distinct = function ()\\{
 var arr = this,
  len = arr.length;
 arr.sort(function(a,b)\\{  //对数组进行排序才能方便比较
  return a - b;
 \\})
 function loop(index)\\{
  if(index >= 1)\\{
   if(arr[index] === arr[index-1])\\{
    arr.splice(index,1);
   \\}
   loop(index - 1); //递归loop函数进行去重
  \\}
 \\}
 loop(len-1);
 return arr;
\\};
var a = [1,2,3,4,5,6,5,3,2,4,56,4,1,2,1,1,1,1,1,1,56,45,56];
var b = a.distinct();
console.log(b.toString());  //1,2,3,4,5,6,45,56
```

#### 方法五：利用indexOf以及forEach

```
Array.prototype.distinct = function ()\\{
 var arr = this,
  result = [],
  len = arr.length;
 arr.forEach(function(v, i ,arr)\\{  //这里利用map，filter方法也可以实现
  var bool = arr.indexOf(v,i+1);  //从传入参数的下一个索引值开始寻找是否存在重复
  if(bool === -1)\\{
   result.push(v);
  \\}
 \\})
 return result;
\\};
var a = [1,1,1,1,1,1,1,1,1,2,2,2,2,2,2,3,3,3,3,3,3,3,2,3,3,2,2,1,23,1,23,2,3,2,3,2,3];
var b = a.distinct();
console.log(b.toString()); //1,23,2,3
```

#### 方法六：利用ES6的set

Set数据结构，它类似于数组，其成员的值都是唯一的。

利用Array.from将Set结构转换成数组

```
function dedupe(array)\\{
 return Array.from(new Set(array));
\\}
dedupe([1,1,2,3]) //[1,2,3]
```

拓展运算符(...)内部使用for...of循环

```
let arr = [1,2,3,3];
let resultarr = [...new Set(arr)]; 
console.log(resultarr); //[1,2,3]
```



### 合并数组并去重的方法

#### 一、concat()方法

思路：concat() 方法将传入的数组或非数组值与原数组合并,组成一个新的数组并返回。该方法会产生一个新的数组。

```
function concatArr(arr1, arr2)\\{
  var arr = arr1.concat(arr2);
  arr = unique1(arr);//再引用上面的任意一个去重方法
  return arr;
\\}
```

#### 二、Array.prototype.push.apply()

思路：该方法优点是不会产生一个新的数组。

```
 var a = [1, 2, 3];
 var b = [4, 5, 6];
 Array.prototype.push.apply(a, b);//a=[1,2,3,4,5,6]
 //等效于:a.push.apply(a, b);
 //也等效于[].push.apply(a, b); 
 function concatArray(arr1,arr2)\\{
   Array.prototype.push.apply(arr1, arr2);
   arr1 = unique1(arr1);
   return arr1;
 \\}
```



### 手写数组去重

```
var arr = [1, 2, 3, 3, 4, 4, 5, 5, 6, 1, 9, 3, 25, 4];
function deRepeat() \\{
  var newArr = [];
  var obj = \\{\\};
  var index = 0;
  var l = arr.length;
  for (var i = 0; i < l; i++) \\{
    if (obj[arr[i]] == undefined) \\{
      obj[arr[i]] = 1;
      newArr[index++] = arr[i];
    \\} else if (obj[arr[i]] == 1) continue;
  \\}
  return newArr;
\\}
var newArr2 = deRepeat(arr);
alert(newArr2); //输出1,2,3,4,5,6,9,25
```

```JavaScript
Array.prototype.unique = function() \\{ return [...new Set(this)];\\};
// 调用
[1, 2, 3, 3, 2, 1].unique();

function unique1(arr)\\{
    var hash = \\{\\}, result = [];
    for(var i=0, len=arr.length; i<len; i++)\\{
        if(! hash[arr[i]])\\{
          result.push(arr[i]);
          hash[arr[i]] = true;
        \\}
    \\}
    return result;
\\}
// 调用
unique1([1, 2, 3, 3, 2, 1]);

Array.prototype.unique2 = function()\\{
    this.sort();
    var result = [this[0]];
    var len = this.length;
    for(var i = 0; i < len; i++)\\{
        if(this[i] !== result[result.length - 1])\\{
          result.push(this[i]);
        \\}
    \\}
    return result;
\\}
// 调用
[1, 2, 3, 3, 2, 1].unique2();

function unique3(arr)\\{
    var result = [];
    for(var i=0; i<arr.length; i++)\\{
        if(result.indexOf(arr[i]) == -1)\\{
          result.push(arr[i]);
        \\}
    \\}
    return result;
\\}

// 调用
unique3([1, 2, 3, 3, 2, 1]);
```

```
//数组去重:
Array.prototype. myUnique = function myUnique()\\{
    //this是当前要操作的数组
    var obj = \\{\\};
    for( var i = 0; i < this.length; i ++)\\{
        var cur = this[i];
        if (obj[cur] == cur)\\{
            this[i] = this[ this.length - 1];
            this.length --;
            i --; //防止数组塌陷
            continue;
        \\}
        obj[cur] = cur;
    \\}
    obj = null;
    return this; //为了实现链式写法
\\};
```



### 将url的查询参数解析成字典对象

```JavaScript
function parseQuery(url) \\{
  url = url == null ? window.location.href : url;
  var search = url.substring(url.lastIndexOf("?") + 1);
  var hash = \\{\\};
  var reg = /([^?&=]+)=([^?&=]*)/g;
  search.replace(reg, function (match, $1, $2) \\{
      var name = decodeURIComponent($1);
      var val = decodeURIComponent($2);
      hash[name] = String(val);
      return match;
  \\});
  return hash;
\\}
```



### 封装函数节流函数

```JavaScript
var throttle = function(fn, delay, mustRunDelay)\\{
  var timer = null;
  var t_start;
  return function()\\{
    var context = this, args = arguments, t_curr = +new Date();
    clearTimeout(timer);
    if(!t_start)\\{
      t_start = t_curr;
    \\}
    if(t_curr - t_start >= mustRunDelay)\\{
      fn.apply(context, args);
      t_start = t_curr;
    \\} else \\{
      timer = setTimeout(function()\\{
        fn.apply(context, args);
      \\}, delay);
    \\}
  \\};
\\};

// 调用（两次间隔50ms内连续触发不执行，但每累计100ms至少执行一次
window.onresize = throttle(myFunc, 50, 100);
```



### 用JS实现千位分隔符

```JavaScript
function test1(num)\\{
  var str = (+ num) + '';
  var len = str.length;
  if(len <= 3) return str;
  num = '';
  while(len > 3)\\{
      len -= 3;
      num = ',' + str.substr(len, 3) + num;
  \\}
  return str.substr(0, len) + num;
\\}

function test2(num)\\{
  // ?= 正向匹配:匹配位置
  // ?! 正向不匹配:排除位置
  var str = (+num).toString();
  var reg = /(?=(?!\b)(\d\\{3\\})+$)/g;
  return str.replace(reg, ',');
\\}
```



### 深克隆（deepclone）

简单版：

```
const newObj = JSON.parse(JSON.stringify(oldObj));
```

局限性：

1. 他无法实现对函数 、RegExp等特殊对象的克隆
2. 会抛弃对象的constructor,所有的构造函数会指向Object
3. 对象有循环引用,会报错

面试版:

```
/**
 * deep clone
 * @param  \\{[type]\\} parent object 需要进行克隆的对象
 * @return \\{[type]\\}        深克隆后的对象
 */
const clone = parent => \\{
  // 判断类型
  const isType = (obj, type) => \\{
    if (typeof obj !== "object") return false;
    const typeString = Object.prototype.toString.call(obj);
    let flag;
    switch (type) \\{
      case "Array":
        flag = typeString === "[object Array]";
        break;
      case "Date":
        flag = typeString === "[object Date]";
        break;
      case "RegExp":
        flag = typeString === "[object RegExp]";
        break;
      default:
        flag = false;
    \\}
    return flag;
  \\};

  // 处理正则
  const getRegExp = re => \\{
    var flags = "";
    if (re.global) flags += "g";
    if (re.ignoreCase) flags += "i";
    if (re.multiline) flags += "m";
    return flags;
  \\};
  // 维护两个储存循环引用的数组
  const parents = [];
  const children = [];

  const _clone = parent => \\{
    if (parent === null) return null;
    if (typeof parent !== "object") return parent;

    let child, proto;

    if (isType(parent, "Array")) \\{
      // 对数组做特殊处理
      child = [];
    \\} else if (isType(parent, "RegExp")) \\{
      // 对正则对象做特殊处理
      child = new RegExp(parent.source, getRegExp(parent));
      if (parent.lastIndex) child.lastIndex = parent.lastIndex;
    \\} else if (isType(parent, "Date")) \\{
      // 对Date对象做特殊处理
      child = new Date(parent.getTime());
    \\} else \\{
      // 处理对象原型
      proto = Object.getPrototypeOf(parent);
      // 利用Object.create切断原型链
      child = Object.create(proto);
    \\}

    // 处理循环引用
    const index = parents.indexOf(parent);

    if (index != -1) \\{
      // 如果父数组存在本对象,说明之前已经被引用过,直接返回此对象
      return children[index];
    \\}
    parents.push(parent);
    children.push(child);

    for (let i in parent) \\{
      // 递归
      child[i] = _clone(parent[i]);
    \\}

    return child;
  \\};
  return _clone(parent);
\\};
```

局限性:

1. 一些特殊情况没有处理: 例如Buffer对象、Promise、Set、Map
2. 另外对于确保没有循环引用的对象，我们可以省去对循环引用的特殊处理，因为这很消耗时间

> 原理详解[实现深克隆](http://mp.weixin.qq.com/s?__biz=MzI3NjM1OTI3Mw==&mid=2247483692&idx=1&sn=ab072f6e9bf145cda31b19b96131faf7&chksm=eb77f02adc00793c60966183ae6ef692d3f5c8518ea04fe5491e2de70183e8637ec7dd843ab2&scene=21#wechat_redirect)



### 实现Event(event bus)

event bus既是node中各个模块的基石，又是前端组件通信的依赖手段之一，同时涉及了订阅-发布设计模式，是非常重要的基础。

简单版：

```
class EventEmeitter \\{
  constructor() \\{
    this._events = this._events || new Map(); // 储存事件/回调键值对
    this._maxListeners = this._maxListeners || 10; // 设立监听上限
  \\}
\\}


// 触发名为type的事件
EventEmeitter.prototype.emit = function(type, ...args) \\{
  let handler;
  // 从储存事件键值对的this._events中获取对应事件回调函数
  handler = this._events.get(type);
  if (args.length > 0) \\{
    handler.apply(this, args);
  \\} else \\{
    handler.call(this);
  \\}
  return true;
\\};

// 监听名为type的事件
EventEmeitter.prototype.addListener = function(type, fn) \\{
  // 将type事件以及对应的fn函数放入this._events中储存
  if (!this._events.get(type)) \\{
    this._events.set(type, fn);
  \\}
\\};
```

面试版：

```
class EventEmeitter \\{
  constructor() \\{
    this._events = this._events || new Map(); // 储存事件/回调键值对
    this._maxListeners = this._maxListeners || 10; // 设立监听上限
  \\}
\\}

// 触发名为type的事件
EventEmeitter.prototype.emit = function(type, ...args) \\{
  let handler;
  // 从储存事件键值对的this._events中获取对应事件回调函数
  handler = this._events.get(type);
  if (args.length > 0) \\{
    handler.apply(this, args);
  \\} else \\{
    handler.call(this);
  \\}
  return true;
\\};

// 监听名为type的事件
EventEmeitter.prototype.addListener = function(type, fn) \\{
  // 将type事件以及对应的fn函数放入this._events中储存
  if (!this._events.get(type)) \\{
    this._events.set(type, fn);
  \\}
\\};

// 触发名为type的事件
EventEmeitter.prototype.emit = function(type, ...args) \\{
  let handler;
  handler = this._events.get(type);
  if (Array.isArray(handler)) \\{
    // 如果是一个数组说明有多个监听者,需要依次此触发里面的函数
    for (let i = 0; i < handler.length; i++) \\{
      if (args.length > 0) \\{
        handler[i].apply(this, args);
      \\} else \\{
        handler[i].call(this);
      \\}
    \\}
  \\} else \\{
    // 单个函数的情况我们直接触发即可
    if (args.length > 0) \\{
      handler.apply(this, args);
    \\} else \\{
      handler.call(this);
    \\}
  \\}

  return true;
\\};

// 监听名为type的事件
EventEmeitter.prototype.addListener = function(type, fn) \\{
  const handler = this._events.get(type); // 获取对应事件名称的函数清单
  if (!handler) \\{
    this._events.set(type, fn);
  \\} else if (handler && typeof handler === "function") \\{
    // 如果handler是函数说明只有一个监听者
    this._events.set(type, [handler, fn]); // 多个监听者我们需要用数组储存
  \\} else \\{
    handler.push(fn); // 已经有多个监听者,那么直接往数组里push函数即可
  \\}
\\};

EventEmeitter.prototype.removeListener = function(type, fn) \\{
  const handler = this._events.get(type); // 获取对应事件名称的函数清单

  // 如果是函数,说明只被监听了一次
  if (handler && typeof handler === "function") \\{
    this._events.delete(type, fn);
  \\} else \\{
    let postion;
    // 如果handler是数组,说明被监听多次要找到对应的函数
    for (let i = 0; i < handler.length; i++) \\{
      if (handler[i] === fn) \\{
        postion = i;
      \\} else \\{
        postion = -1;
      \\}
    \\}
    // 如果找到匹配的函数,从数组中清除
    if (postion !== -1) \\{
      // 找到数组对应的位置,直接清除此回调
      handler.splice(postion, 1);
      // 如果清除后只有一个函数,那么取消数组,以函数形式保存
      if (handler.length === 1) \\{
        this._events.set(type, handler[0]);
      \\}
    \\} else \\{
      return this;
    \\}
  \\}
\\};
```



### 实现instanceOf

```
// 模拟 instanceof
function instance_of(L, R) \\{
  //L 表示左表达式，R 表示右表达式
  var O = R.prototype; // 取 R 的显示原型
  L = L.__proto__; // 取 L 的隐式原型
  while (true) \\{
    if (L === null) return false;
    if (O === L)
      // 这里重点：当 O 严格等于 L 时，返回 true
      return true;
    L = L.__proto__;
  \\}
\\}
```



### 实现一个call

call做了什么:

- 将函数设为对象的属性
- 执行&删除这个函数
- 指定this到函数并传入给定参数执行函数
- 如果不传入参数，默认指向为 window

```
// 模拟 call bar.mycall(null);
//实现一个call方法：
Function.prototype.myCall = function(context) \\{
  //此处没有考虑context非object情况
  context.fn = this;
  let args = [];
  for (let i = 1, len = arguments.length; i < len; i++) \\{
    args.push(arguments[i]);
  \\}
  context.fn(...args);
  let result = context.fn(...args);
  delete context.fn;
  return result;
\\};
```

> 具体实现参考JavaScript深入之call和apply的模拟实现



### 实现apply方法

apply原理与call很相似，不多赘述

```
// 模拟 apply
Function.prototype.myapply = function(context, arr) \\{
  var context = Object(context) || window;
  context.fn = this;

  var result;
  if (!arr) \\{
    result = context.fn();
  \\} else \\{
    var args = [];
    for (var i = 0, len = arr.length; i < len; i++) \\{
      args.push("arr[" + i + "]");
    \\}
    result = eval("context.fn(" + args + ")");
  \\}

  delete context.fn;
  return result;
\\};
```



### 实现bind

实现bind要做什么

- 返回一个函数，绑定this，传递预置参数
- bind返回的函数可以作为构造函数使用。故作为构造函数时应使得this失效，但是传入的参数依然有效

```
// mdn的实现
if (!Function.prototype.bind) \\{
  Function.prototype.bind = function(oThis) \\{
    if (typeof this !== 'function') \\{
      // closest thing possible to the ECMAScript 5
      // internal IsCallable function
      throw new TypeError('Function.prototype.bind - what is trying to be bound is not callable');
    \\}

    var aArgs   = Array.prototype.slice.call(arguments, 1),
        fToBind = this,
        fNOP    = function() \\{\\},
        fBound  = function() \\{
          // this instanceof fBound === true时,说明返回的fBound被当做new的构造函数调用
          return fToBind.apply(this instanceof fBound
                 ? this
                 : oThis,
                 // 获取调用时(fBound)的传参.bind 返回的函数入参往往是这么传递的
                 aArgs.concat(Array.prototype.slice.call(arguments)));
        \\};

    // 维护原型关系
    if (this.prototype) \\{
      // Function.prototype doesn't have a prototype property
      fNOP.prototype = this.prototype; 
    \\}
    // 下行的代码使fBound.prototype是fNOP的实例,因此
    // 返回的fBound若作为new的构造函数,new生成的新对象作为this传入fBound,新对象的__proto__就是fNOP的实例
    fBound.prototype = new fNOP();

    return fBound;
  \\};
\\}
```

> 详解请移步JavaScript深入之bind的模拟实现 #12



### 模拟Object.create

Object.create()方法创建一个新对象，使用现有的对象来提供新创建的对象的**proto**。

```
// 模拟 Object.create

function create(proto) \\{
  function F() \\{\\}
  F.prototype = proto;

  return new F();
\\}
```



### 实现类的继承

类的继承在几年前是重点内容，有n种继承方式各有优劣，es6普及后越来越不重要，那么多种写法有点『回字有四样写法』的意思，如果还想深入理解的去看红宝书即可，我们目前只实现一种最理想的继承方式。

```
function Parent(name) \\{
    this.parent = name
\\}
Parent.prototype.say = function() \\{
    console.log(`$\\{this.parent\\}: 你打篮球的样子像kunkun`)
\\}
function Child(name, parent) \\{
    // 将父类的构造函数绑定在子类上
    Parent.call(this, parent)
    this.child = name
\\}

/** 
 1. 这一步不用Child.prototype =Parent.prototype的原因是怕共享内存，修改父类原型对象就会影响子类
 2. 不用Child.prototype = new Parent()的原因是会调用2次父类的构造方法（另一次是call），会存在一份多余的父类实例属性
3. Object.create是创建了父类原型的副本，与父类原型完全隔离
*/
Child.prototype = Object.create(Parent.prototype);
Child.prototype.say = function() \\{
    console.log(`$\\{this.parent\\}好，我是练习时长两年半的$\\{this.child\\}`);
\\}

// 注意记得把子类的构造指向子类本身
Child.prototype.constructor = Child;

var parent = new Parent('father');
parent.say() // father: 你打篮球的样子像kunkun

var child = new Child('cxk', 'father');
child.say() // father好，我是练习时长两年半的cxk
```



### 实现JSON.parse

```
var json = '\\{"name":"cxk", "age":25\\}';
var obj = eval("(" + json + ")");
```

此方法属于黑魔法，极易容易被xss攻击，还有一种`new Function`大同小异。

简单的教程看这个半小时实现一个 JSON 解析器



### 实现Promise

> 我很早之前实现过一版，而且注释很多，但是居然找不到了,这是在网络上找了一版带注释的，目测没有大问题，具体过程可以看这篇史上最易读懂的 Promise/A+ 完全实现

```
var PromisePolyfill = (function () \\{
  // 和reject不同的是resolve需要尝试展开thenable对象
  function tryToResolve (value) \\{
    if (this === value) \\{
    // 主要是防止下面这种情况
    // let y = new Promise(res => setTimeout(res(y)))
      throw TypeError('Chaining cycle detected for promise!')
    \\}

    // 根据规范2.32以及2.33 对对象或者函数尝试展开
    // 保证S6之前的 polyfill 也能和ES6的原生promise混用
    if (value !== null &&
      (typeof value === 'object' || typeof value === 'function')) \\{
      try \\{
      // 这里记录这次then的值同时要被try包裹
      // 主要原因是 then 可能是一个getter, 也也就是说
      //   1. value.then可能报错
      //   2. value.then可能产生副作用(例如多次执行可能结果不同)
        var then = value.then

        // 另一方面, 由于无法保证 then 确实会像预期的那样只调用一个onFullfilled / onRejected
        // 所以增加了一个flag来防止resolveOrReject被多次调用
        var thenAlreadyCalledOrThrow = false
        if (typeof then === 'function') \\{
        // 是thenable 那么尝试展开
        // 并且在该thenable状态改变之前this对象的状态不变
          then.bind(value)(
          // onFullfilled
            function (value2) \\{
              if (thenAlreadyCalledOrThrow) return
              thenAlreadyCalledOrThrow = true
              tryToResolve.bind(this, value2)()
            \\}.bind(this),

            // onRejected
            function (reason2) \\{
              if (thenAlreadyCalledOrThrow) return
              thenAlreadyCalledOrThrow = true
              resolveOrReject.bind(this, 'rejected', reason2)()
            \\}.bind(this)
          )
        \\} else \\{
        // 拥有then 但是then不是一个函数 所以也不是thenable
          resolveOrReject.bind(this, 'resolved', value)()
        \\}
      \\} catch (e) \\{
        if (thenAlreadyCalledOrThrow) return
        thenAlreadyCalledOrThrow = true
        resolveOrReject.bind(this, 'rejected', e)()
      \\}
    \\} else \\{
    // 基本类型 直接返回
      resolveOrReject.bind(this, 'resolved', value)()
    \\}
  \\}

  function resolveOrReject (status, data) \\{
    if (this.status !== 'pending') return
    this.status = status
    this.data = data
    if (status === 'resolved') \\{
      for (var i = 0; i < this.resolveList.length; ++i) \\{
        this.resolveList[i]()
      \\}
    \\} else \\{
      for (i = 0; i < this.rejectList.length; ++i) \\{
        this.rejectList[i]()
      \\}
    \\}
  \\}

  function Promise (executor) \\{
    if (!(this instanceof Promise)) \\{
      throw Error('Promise can not be called without new !')
    \\}

    if (typeof executor !== 'function') \\{
    // 非标准 但与Chrome谷歌保持一致
      throw TypeError('Promise resolver ' + executor + ' is not a function')
    \\}

    this.status = 'pending'
    this.resolveList = []
    this.rejectList = []

    try \\{
      executor(tryToResolve.bind(this), resolveOrReject.bind(this, 'rejected'))
    \\} catch (e) \\{
      resolveOrReject.bind(this, 'rejected', e)()
    \\}
  \\}

  Promise.prototype.then = function (onFullfilled, onRejected) \\{
  // 返回值穿透以及错误穿透, 注意错误穿透用的是throw而不是return，否则的话
  // 这个then返回的promise状态将变成resolved即接下来的then中的onFullfilled
  // 会被调用, 然而我们想要调用的是onRejected
    if (typeof onFullfilled !== 'function') \\{
      onFullfilled = function (data) \\{
        return data
      \\}
    \\}
    if (typeof onRejected !== 'function') \\{
      onRejected = function (reason) \\{
        throw reason
      \\}
    \\}

    var executor = function (resolve, reject) \\{
      setTimeout(function () \\{
        try \\{
        // 拿到对应的handle函数处理this.data
        // 并以此为依据解析这个新的Promise
          var value = this.status === 'resolved'
            ? onFullfilled(this.data)
            : onRejected(this.data)
          resolve(value)
        \\} catch (e) \\{
          reject(e)
        \\}
      \\}.bind(this))
    \\}

    // then 接受两个函数返回一个新的Promise
    // then 自身的执行永远异步与onFullfilled/onRejected的执行
    if (this.status !== 'pending') \\{
      return new Promise(executor.bind(this))
    \\} else \\{
    // pending
      return new Promise(function (resolve, reject) \\{
        this.resolveList.push(executor.bind(this, resolve, reject))
        this.rejectList.push(executor.bind(this, resolve, reject))
      \\}.bind(this))
    \\}
  \\}

  // for prmise A+ test
  Promise.deferred = Promise.defer = function () \\{
    var dfd = \\{\\}
    dfd.promise = new Promise(function (resolve, reject) \\{
      dfd.resolve = resolve
      dfd.reject = reject
    \\})
    return dfd
  \\}

  // for prmise A+ test
  if (typeof module !== 'undefined') \\{
    module.exports = Promise
  \\}

  return Promise
\\})()

PromisePolyfill.all = function (promises) \\{
  return new Promise((resolve, reject) => \\{
    const result = []
    let cnt = 0
    for (let i = 0; i < promises.length; ++i) \\{
      promises[i].then(value => \\{
        cnt++
        result[i] = value
        if (cnt === promises.length) resolve(result)
      \\}, reject)
    \\}
  \\})
\\}

PromisePolyfill.race = function (promises) \\{
  return new Promise((resolve, reject) => \\{
    for (let i = 0; i < promises.length; ++i) \\{
      promises[i].then(resolve, reject)
    \\}
  \\})
\\}
```



### 解析 URL Params 为对象

```
let url = 'http://www.domain.com/?user=anonymous&id=123&id=456&city=\\%E5\\%8C\\%97\\%E4\\%BA\\%AC&enabled';
parseParam(url)
/* 结果
\\{ user: 'anonymous',
  id: [ 123, 456 ], // 重复出现的 key 要组装成数组，能被转成数字的就转成数字类型
  city: '北京', // 中文需解码
  enabled: true, // 未指定值得 key 约定为 true
\\}
*/
function parseParam(url) \\{
  const paramsStr = /.+\?(.+)$/.exec(url)[1]; // 将 ? 后面的字符串取出来
  const paramsArr = paramsStr.split('&'); // 将字符串以 & 分割后存到数组中
  let paramsObj = \\{\\};
  // 将 params 存到对象中
  paramsArr.forEach(param => \\{
    if (/=/.test(param)) \\{ // 处理有 value 的参数
      let [key, val] = param.split('='); // 分割 key 和 value
      val = decodeURIComponent(val); // 解码
      val = /^\d+$/.test(val) ? parseFloat(val) : val; // 判断是否转为数字

      if (paramsObj.hasOwnProperty(key)) \\{ // 如果对象有 key，则添加一个值
        paramsObj[key] = [].concat(paramsObj[key], val);
      \\} else \\{ // 如果对象没有这个 key，创建 key 并设置值
        paramsObj[key] = val;
      \\}
    \\} else \\{ // 处理没有 value 的参数
      paramsObj[param] = true;
    \\}
  \\})

  return paramsObj;
\\}
```



### 模板引擎实现

```
let template = '我是\\\{\\\{nam\\\}\\\}e}}，年龄\\\{\\\{ag\\\}\\\}e}}，性别\\\{\\\{se\\\}\\\}x}}';
let data = \\{
  name: '姓名',
  age: 18
\\}
render(template, data); // 我是姓名，年龄18，性别undefined
function render(template, data) \\{
  const reg = /\\\{\\\{(\w+)\\\}\\\}/; // 模板字符串正则
  if (reg.test(template)) \\{ // 判断模板里是否有模板字符串
    const name = reg.exec(template)[1]; // 查找当前模板里第一个模板字符串的字段
    template = template.replace(reg, data[name]); // 将第一个模板字符串渲染
    return render(template, data); // 递归的渲染并返回渲染后的结构
  \\}
  return template; // 如果模板没有模板字符串直接返回
\\}
```



### 转化为驼峰命名

```
var s1 = "get-element-by-id"

// 转化为 getElementById
var f = function(s) \\{
    return s.replace(/-\w/g, function(x) \\{
        return x.slice(1).toUpperCase();
    \\})
\\}
```



### 查找字符串中出现最多的字符和个数

例: abbcccddddd -> 字符最多的是d，出现了5次

```
let str = "abcabcabcbbccccc";
let num = 0;
let char = '';

 // 使其按照一定的次序排列
str = str.split('').sort().join('');
// "aaabbbbbcccccccc"

// 定义正则表达式
let re = /(\w)\1+/g;
str.replace(re,($0,$1) => \\{
    if(num < $0.length)\\{
        num = $0.length;
        char = $1;        
    \\}
\\});
console.log(`字符最多的是$\\{char\\}，出现了$\\{num\\}次`);
```



### 字符串查找

请使用最基本的遍历来实现判断字符串 a 是否被包含在字符串 b 中，并返回第一次出现的位置（找不到返回 -1）。

```
a='34';b='1234567'; // 返回 2
a='35';b='1234567'; // 返回 -1
a='355';b='12354355'; // 返回 5
isContain(a,b);
function isContain(a, b) \\{
  for (let i in b) \\{
    if (a[0] === b[i]) \\{
      let tmp = true;
      for (let j in a) \\{
        if (a[j] !== b[~~i + ~~j]) \\{
          tmp = false;
        \\}
      \\}
      if (tmp) \\{
        return i;
      \\}
    \\}
  \\}
  return -1;
\\}
```



### 实现千位分隔符

```
// 保留三位小数
parseToMoney(1234.56); // return '1,234.56'
parseToMoney(123456789); // return '123,456,789'
parseToMoney(1087654.321); // return '1,087,654.321'
function parseToMoney(num) \\{
  num = parseFloat(num.toFixed(3));
  let [integer, decimal] = String.prototype.split.call(num, '.');
  integer = integer.replace(/\d(?=(\d\\{3\\})+$)/g, '$&,');
  return integer + '.' + (decimal ? decimal : '');
\\}
```

正则表达式(运用了正则的前向声明和反前向声明):

```
function parseToMoney(str)\\{
    // 仅仅对位置进行匹配
    let re = /(?=(?!\b)(\d\\{3\\})+$)/g; 
   return str.replace(re,','); 
\\}
```







## ES6

### 箭头函数问题

答案：

第 1 题

在使用=>定义函数的时候，this 的指向是定义时所在的对象，而不是使用时所在的对象；

```js
class Animal \\{
  constructor() \\{
    this.type = "animal";
  \\}
  say(val) \\{
    setTimeout(function() \\{
      console.log(this); //window
      console.log(this.type + " says " + val);
    \\}, 1000);
  \\}
\\}
var animal = new Animal();
animal.say("hi"); //undefined says hi
```

```js
class Animal \\{
  constructor() \\{
    this.type = "animal";
  \\}
  say(val) \\{
    setTimeout(() => \\{
      console.log(this); //Animal
      console.log(this.type + " says " + val);
    \\}, 1000);
  \\}
\\}
var animal = new Animal();
animal.say("hi"); //animal says hi
```

第二题：

箭头函数里面根本没有自己的 this，而是引用外层的 this

```js
// ES6
function foo() \\{
  setTimeout(() => \\{
    console.log("id:", this.id);
  \\}, 100);
\\}

// 转成ES5
function foo() \\{
  var _this = this;

  setTimeout(function() \\{
    console.log("id:", _this.id);
  \\}, 100);
\\}
```



### this 面试题

```
 this指向了谁？
 看函数在执行的时候是如何调用的，
 1 如果这个函数是用普通函数调用模式来进行调用，它内部的this指向了window
 2如果一个函数在调用的时候是通过对象方法模式来进行调用，则它内部的this就是我们的对象
 3 如果一个函数在调用的时候通过构造函数模式调用，则它内部的this指向了生成的实例
 4 如果这个函数是通过方法借用模式调用，则这个函数内部的this就是我们手动指定this。
```

```js
//第1题
function Fn() \\{
  console.log(this);
\\}
Fn(); //window 普通函数调用模式
new Fn(); //\\{\\}  构造函数调用模式
Fn.apply(Fn); // Fn的函数体   方法借用模式

//第2题
var o = \\{
  f: function() \\{
    console.log(this);
  \\},
  2: function() \\{
    console.log(this);
    console.log(this.__proto__ === o[2].prototype);
  \\}
\\};
o.f(); //o   对象调用模式
o[2](); //o  对象调用模式
new o[2](); //存疑，存在着优先级的问题 \\{\\}  通过构造函数模式进行调用
o.f.call([1, 2]); //[1,2]   call方法进行方法借用。
o[2].call([1, 2, 3, 4]); // [1,2,3,4]  call方法进行方法借用

//第3题
var name = "out";
var obj = \\{
  name: "in",
  prop: \\{
    name: "inside",
    getName: function() \\{
      return this.name;
    \\}
  \\}
\\};

console.log(obj.prop.getName()); //对象调用模式来进行调用  obj.prop.name  'inside'
var test = obj.prop.getName; // 把test这个变量指向了obj.prop.getName所在的内存地址。
console.log(test()); //普通函数模式来进行调用  window 'out'
console.log(obj.prop.getName.apply(window)); //方法借用模式  'out'
console.log(obj.prop.getName.apply(this)); //方法借用模式  'out'
console.log(this === window); //true

//第4题
var length = 10;
function fn() \\{
  console.log(this.length);
\\}
var obj = \\{
  length: 5,
  method: function(f) \\{
    console.log(this);
    f(); // f在调用的时候是什么调用模式？普通函数调用模式  window.length  10
    arguments[0](); // 通过什么模式来进行调用的。执行之前有[]和.就是对象调用模式。
    //arguments是一个类数组，也就是一个对象，就是通过arguments来进行调用的
    //arguments.length实参的数量。实参长度是1
    //通过arguments对象进行调用，因此函数内部的this是  arguments
    // 如果一个函数在调用的时候它前面有call和apply那么就肯定是方法借用模式调用
    arguments[0].call(this);
    // 调用method方法是通过obj.method 因此在这里的this就是 obj
    //通过call方法把fn内的this指向了obj
    // 输出obj.length  5
  \\}
\\};
obj.method(fn);

//第5题
function Foo() \\{
  getName = function() \\{
    console.log(1);
  \\};
  return this;
\\}
Foo.getName = function() \\{
  console.log(2);
\\};
Foo.prototype.getName = function() \\{
  console.log(3);
\\};
var getName = function() \\{
  console.log(4);
\\};
function getName() \\{
  console.log(5);
\\}
//请写出以下输出结果：
Foo.getName(); //2
getName(); //4
Foo().getName(); //1
getName(); //1
new Foo.getName(); //2
new Foo().getName(); //3
new new Foo().getName(); //3
// new Foo()创建了一个构造函数，然后这个函数再去访问getName这个函数，
//对它进行调用
/*console.log(new Foo().getName)*/
/*var o = new new Foo().getName(); //
    console.log(o.__proto__===Foo.prototype.getName.prototype)*/
//用new Foo创建出来了一个实例，然后这个实例去访问 (new Foo().getName)

/*console.log(new new Foo().getName())

    console.log(new Foo().getName())*/

/*function Foo() \\{
        getName = function () \\{
            console.log(1);
        \\};
        return this;
    \\}
    var getName;
    Foo.getName = function () \\{
        console.log(2);
    \\};
    Foo.prototype.getName = function () \\{
        console.log(3);
    \\};
    getName = function () \\{
        console.log(4);
    \\};
    //请写出以下输出结果：
    Foo.getName();// 2
    getName();//4
/!*    Foo().getName();//!*!/
    window.getName()//1
    getName();//1
  /!*  var o = new Foo.getName();//2
    console.log(o);// \\{\\}
    console.log(o.__proto__===Foo.getName.prototype)//true*!/
    new Foo.getName();// 2
    new Foo().getName();//
    new new Foo().getName();*/

//第6题
var obj = \\{
  fn: function() \\{
    console.log(this);
  \\}
\\};
obj.fn(); //obj
var f = obj.fn;
f(); //window
console.log(f === obj.fn); // true

// f和obj.fn是同一个函数，但是他们在调用的时候使用的函数调用模式不同，因此，它们内部的this指向也就不同。

// #7题
var arr = [
  function() \\{
    console.log(this);
  \\}
];
arr[0](); //数组本身
//数组也是一个复杂数据类型，也是一个对象，那用数组去调用函数，使用的模式就是对象方法调用模式。
function f() \\{
  console.log(this);
\\}
function fn() \\{
  console.log(arguments); // 类数组，也是就一个对象    [0:function f()\\{\\}]
  console.log(this); // window
  arguments[0]();
  console.log(arguments[0]); //内部的this就是arguments
  // 通过arguments对f这个方法进行调用，使用的是对象方法调用模式。
\\}
fn(f);

// #8题
function SuperClass() \\{
  this.name = "women";
  this.bra = ["a", "b"];
\\}

SuperClass.prototype.sayWhat = function() \\{
  console.log("hello");
\\};

function SubClass() \\{
  this.subname = "you sister";
  SuperClass.call(this);
\\}

var sub = new SubClass();
console.log(sub.sayWhat());
```



### 把以下代码使用两种方法，依次输出 0-9

答案：

```js
var funcs = [];
for (var i = 0; i < 10; i++) \\{
  funcs.push(function() \\{
    console.log(i);
  \\});
\\}
funcs.forEach(function(func) \\{
  func(); //输出十个10
\\});
```

解决办法：

方法一：使用立即执行函数

```js
var funcs = [];
for (var i = 0; i < 10; i++) \\{
  funcs.push(
    (function(value) \\{
      return function() \\{
        console.log(value);
      \\};
    \\})(i)
  );
\\}
funcs.forEach(function(func) \\{
  func(); //依次输出0-9
\\});
```

方法二：使用闭包

```js
function show(i) \\{
  return function() \\{
    console.log(i);
  \\};
\\}
var funcs = [];
for (var i = 0; i < 10; i++) \\{
  funcs.push(show(i));
\\}
funcs.forEach(function(func) \\{
  func(); //0 1 2 3 4 5 6 7 8 9
\\});
```

方法三：使用 let

```js
var funcs = [];
for (let i = 0; i < 10; i++) \\{
  funcs.push(function() \\{
    console.log(i);
  \\});
\\}
funcs.forEach(function(func) \\{
  func(); //依次输出0-9
\\});
```



### 怎么解决回调函数里面回调另一个函数，另一个函数的参数需要依赖这个回调函数。需要被解决的代码如下：

```js
$http.get(url).success(function (res) \\{
  if (success != undefined) \\{
    success(res);
  \\}
\\}).error(function (res) \\{
  if (error != undefined) \\{
    error(res);
  \\}
\\});

function success(data) \\{
  if（ data.id != 0） \\{
    var url = "getdata/data?id=" + data.id + "";
    $http.get(url).success(function (res) \\{
      showData(res);
    \\}).error(function (res) \\{
      if (error != undefined) \\{
        error(res);
      \\}
    \\});
  \\}
\\}
```

答案：使用 Promise/async/await 解决

解析：

```js
function awaitMethod(num) \\{
  return new Promise((resolve, reject) => \\{
    setTimeout(() => \\{
      resolve(2 * num); // 此处模拟接口的请求
    \\}, 2000);
  \\});
\\}
// 打个比方，await是学生，async是校车，必须等人齐了再开车
async function test() \\{
  let result = await awaitMethod(30); // await 这个关键字只能在使用async定义的函数里面使用
  console.log(result); // 2秒钟之后控制台输出60 ; 后面利用 result 继续调用函数
  let next = await awaitMethod(result);
  console.log(next); // 4秒钟之后控制台输出120
  return next;
\\}
// 在async里，必须要将结果return回来，不然的话.then .catch获取不到值
test()
  .then(success => console.log("成功", success))
  .catch(error => console.log("失败", error));
```



### jQuery 的 ajax 返回的是 promise 对象吗？

jquery 的 ajax 返回的是 deferred 对象，通过 promise 的 resolve()方法将其转换为 promise 对象。

var jsPromise = Promise.resolve(\$.ajax('/whatever.json'));



### promise 只有 2 个状态，成功和失败，怎么让一个函数无论成功还是失败都能被调用？

```
使用promise.all()

Promise.all方法用于将多个Promise实例，包装成一个新的Promise实例。

Promise.all方法接受一个数组作为参数，数组里的元素都是Promise对象的实例，如果不是，就会先调用下面讲到的Promise.resolve方法，将参数转为Promise实例，再进一步处理。（Promise.all方法的参数可以不是数组，但必须具有Iterator接口，且返回的每个成员都是Promise实例。）

示例：
var p =Promise.all([p1,p2,p3]);
p的状态由p1、p2、p3决定，分为两种情况。
当该数组里的所有Promise实例都进入Fulfilled状态：Promise.all**返回的实例才会变成Fulfilled状态。并将Promise实例数组的所有返回值组成一个数组，传递给Promise.all返回实例的回调函数**。

当该数组里的某个Promise实例都进入Rejected状态：Promise.all返回的实例会立即变成Rejected状态。并将第一个rejected的实例返回值传递给Promise.all返回实例的回调函数。
```



### 以下代码依次输出的内容是？

```js
setTimeout(function() \\{
  console.log(1);
\\}, 0);
new Promise(function executor(resolve) \\{
  console.log(2);
  for (var i = 0; i < 10000; i++) \\{
    i == 9999 && resolve();
  \\}
  console.log(3);
\\}).then(function() \\{
  console.log(4);
\\});
console.log(5);
```

答案：打印顺序 2 3 5 4 1

解析：

首先先碰到一个 setTimeout，于是会先设置一个定时，在定时结束后将传递这个函数放到任务队列里面，因此开始肯定不会输出 1 。

然后是一个 Promise，里面的函数是直接执行的，因此应该直接输出 2 3 。

然后，Promise 的 then 应当会放到当前 tick 的最后，但是还是在当前 tick 中。

因此，应当先输出 5，然后再输出 4 ， 最后在到下一个 tick，就是 1 。

[参考](https://juejin.im/post/5b1ffff96fb9a01e345ba704)



### Promise 编程题

答案：

第 1 题

```js
const promise = new Promise((resolve, reject) => \\{
  console.log(1);
  resolve();
  console.log(2);
\\});
promise.then(() => \\{
  console.log(3);
\\});
console.log(4);
```

```
运行结果及原因

运行结果：
1 2 4 3

原因：
Promise 构造函数是同步执行的，promise.then 中的函数是异步执行的。
```

第 2 题

```js
const promise1 = new Promise((resolve, reject) => \\{
  setTimeout(() => \\{
    resolve("success");
  \\}, 1000);
\\});
const promise2 = promise1.then(() => \\{
  throw new Error("error!!!");
\\});

console.log("promise1", promise1);
console.log("promise2", promise2);

setTimeout(() => \\{
  console.log("promise1", promise1);
  console.log("promise2", promise2);
\\}, 2000);
```

运行结果及原因

```
运行结果：
promise1 Promise \\{ <pending> \\}
promise2 Promise \\{ <pending> \\}
Uncaught (in promise) Error: error!!!
promise1 Promise \\{ 'success' \\}
promise2 Promise \\{
  <rejected> Error: error!!!
    at promise.then (...)
    at <anonymous> \\}


原因：
promise 有 3 种状态：pending（进行中）、fulfilled（已完成，又称为Resolved） 或 rejected（已失败）。状态改变只能是 pending->fulfilled 或者 pending->rejected，状态一旦改变则不能再变。上面 promise2 并不是 promise1，而是返回的一个新的 Promise 实例。
```

第 3 题

```js
const promise = new Promise((resolve, reject) => \\{
  resolve("success1");
  reject("error");
  resolve("success2");
\\});

promise
  .then(res => \\{
    console.log("then: ", res);
  \\})
  .catch(err => \\{
    console.log("catch: ", err);
  \\});
```

```
运行结果及原因

运行结果：
then：success1

原因：
构造函数中的 resolve 或 reject 只有第一次执行有效，多次调用没有任何作用，呼应代码二结论：promise 状态一旦改变则不能再变。
```

第 4 题

```js
Promise.resolve(1)
  .then(res => \\{
    console.log(res); // 打印1
    return 2;
  \\})
  .catch(err => \\{
    return 3;
  \\})
  .then(res => \\{
    console.log(res); // 打印2
  \\});
```

运行结果：
1 2

原因：
promise 可以链式调用。提起链式调用我们通常会想到通过 return this 实现，不过 Promise 并不是这样实现的。promise 每次调用 .then 或者 .catch 都会返回一个新的 promise，从而实现了链式调用。

第 5 题

```js
Promise.resolve()
  .then(() => \\{
    return new Error("error!!!");
  \\})
  .then(res => \\{
    console.log("then: ", res);
  \\})
  .catch(err => \\{
    console.log("catch: ", err);
  \\});
```

```
运行结果
then: Error: error!!!
    at Promise.resolve.then (...)
    at ...

原因
.then 或者 .catch 中 return 一个 error 对象并不会抛出错误，所以不会被后续的 .catch 捕获，需要改成其中一种：
return Promise.reject(new Error('error!!!'))
throw new Error('error!!!')

因为返回任意一个非 promise 的值都会被包裹成 promise 对象，即 return new Error('error!!!') 等价于 return Promise.resolve(new Error('error!!!'))。
```

第 6 题

```js
const promise = new Promise((resolve, reject) => \\{
  setTimeout(() => \\{
    console.log("once");
    resolve("success");
  \\}, 1000);
\\});

const start = Date.now();
promise.then(res => \\{
  console.log(res, Date.now() - start);
\\});
promise.then(res => \\{
  console.log(res, Date.now() - start);
\\});
```

```
运行结果：
once
success 1001
success 1001
注：1001不是准确数值，也可能是998、999、1000、1002 等

原因：
promise 的 .then 或者 .catch 可以被调用多次，但这里 Promise 构造函数只执行一次。或者说 promise 内部状态一经改变，并且有了一个值，那么后续每次调用 .then 或者 .catch 都会直接拿到该值。
```

第 7 题

```js
const promise = Promise.resolve().then(() => \\{
  return promise;
\\});
promise.catch(console.error);
```

```
运行结果
TypeError: Chaining cycle detected for promise #<Promise>...

原因
.then 或 .catch 返回的值不能是 promise 本身，否则会造成死循环。
```

第 8 题

```js
Promise.resolve(1)
  .then(2)
  .then(Promise.resolve(3))
  .then(console.log);
```

```
运行结果
1

原因
.then 或者 .catch 的参数期望是函数，传入非函数则会发生值穿透。
```

第 9 题

```js
Promise.resolve()
  .then(
    function success(res) \\{
      throw new Error("error");
    \\},
    function fail1(e) \\{
      console.error("fail1: ", e);
    \\}
  )
  .catch(function fail2(e) \\{
    console.error("fail2: ", e);
  \\});
```

```
运行结果
fail2: Error: error
    at success (...)
    at ...

原因
.then 可以接收两个参数，第一个是处理成功的函数，第二个是处理错误的函数。.catch 是 .then 第二个参数的简便写法，但是它们用法上有一点需要注意：.then 的第二个处理错误的函数捕获不了第一个处理成功的函数抛出的错误，而后续的 .catch 可以捕获之前的错误。
```

第 10 题

```js
process.nextTick(() => \\{
  console.log("nextTick");
\\});
Promise.resolve().then(() => \\{
  console.log("then");
\\});
setImmediate(() => \\{
  console.log("setImmediate");
\\});
console.log("end");
```

```
运行结果
end
nextTick
then
setImmediate

原因
process.nextTick 和 promise.then 都属于 microtask，而 setImmediate 属于 macrotask，在事件循环的 check 阶段执行。事件循环的每个阶段（macrotask）之间都会执行 microtask，事件循环的开始会先执行一次 microtask。
```







## 不常考代码题

### 变量提升

```js
// 1
console.log(tt);
tt = "dd";
console.log(tt);
// 变量提升之后的代码：
var tt;
console.log(tt); //undefined
tt = "dd";
console.log(tt); //'dd'
```

```js
// 2
if (!a) \\{
  var a = 2;
\\}
console.log(a);
// 变量提升之后的代码：
var a; //undefined
if (!a) \\{
  //true
  a = 2;
\\}
console.log(a); //2
```



### 函数提升

```js
// 1
if (false) \\{
  function fn() \\{
    console.log(1);
  \\}
\\}
console.log(fn);
fn();
// 变量提升之后的代码：
var fn; //undefined
if (false) \\{
  function fn() \\{
    console.log(1);
  \\}
\\}
console.log(fn); //undefined
fn(); // fn is not a function
```

```js
// 2
function fn() \\{
  foo();
  return;
  function foo() \\{\\}
\\}
fn();
// 变量提升之后的代码：
function fn() \\{
  function foo() \\{\\}
  foo(); // 没有输出也不会报一个错误，因为foo是一个函数
  return;
\\}
fn();
```

```js
// 3
function bar() \\{
  console.log(foo);
  return;
  var foo = function() \\{\\};
\\}
bar();
// 变量提升之后的代码：
function bar() \\{
  var foo;
  console.log(foo); // undefined
  return; // 函数return之后的代码依旧会发生变量提升
  foo = function() \\{\\};
\\}
bar();
```

```js
// 4
console.log(f1);
console.log(f2);
function f1() \\{\\}
var f2 = function() \\{\\};
// 变量提升之后的代码：
function f1() \\{\\} // 函数提升，整个代码块提升到文件的最开始
var f2;
console.log(f1); // function f1() \\{\\}
console.log(f2); // undefined
f2 = function() \\{\\};
```



### 函数和变量同时提升

```js
// 1
console.log(fn);
var fn = function() \\{
  console.log(1);
\\};
console.log(fn);
function fn() \\{
  console.log(2);
\\}
console.log(fn);
// 变量提升之后的代码：
var fn;
function fn() \\{
  console.log(2);
\\}
console.log(fn); // 2
fn = function() \\{
  console.log(1);
\\};
console.log(fn); // 1
console.log(fn); // 1
```

```js
// 2
console.log(f1());
console.log(f2);
function f1() \\{
  console.log("aa");
\\}
var f2 = function() \\{\\};
// 变量提升之后的代码：
var f2
function f1() \\{
  console.log("aa"); // "aa"
\\}
f2 = function() \\{\\};
console.log(f1()); // undefined
console.log(f2); // ƒ () \\{\\}
```

```js
// 3
(function() \\{
  console.log(a);
  a = "aaa";
  var a = "bbb";
  console.log(a);
\\})();
// 变量提升之后的代码：
```

```js
// 4
console.log(a);
var a = 1;
console.log(a);
function a() \\{\\}
console.log(a);
// 变量提升之后的代码： 函数的提升后的位置是在变量提升后的位置之后的
var a;
function a() \\{\\}
console.log(a); // a()
a = 1;
console.log(a); // 1
console.log(a); // 1
```

```js
// 5
console.log(a);
var a = 1;
console.log(a);
function a() \\{\\}
console.log(a);
console.log(b);
var b = 2;
console.log(b);
function b() \\{\\}
console.log(b);
// 变量提升之后的代码：
var a;
var b;
function a() \\{\\}
function b() \\{\\}
console.log(a); // a()
a = 1;
console.log(a); // 1
console.log(a); // 1
console.log(b); // b()
b = 2;
console.log(b); // 2
console.log(b); // 2
```

```js
// 6
console.log(a);
console.log(b); // 报错 隐式全局变量不会提升
b = "aaa";
var a = "bbb";
console.log(a);
console.log(b);
```



### 你如何获取浏览器 URL 中查询字符串中的参数？

答案：

方法一：(基础版)

```js
function getQueryString() \\{
  var sHref = window.location.href;
  var args = sHref.split("?");
  if (args[0] == sHref) \\{
    // 没有参数，直接返回空即可
    return "";
  \\}
  var arr = args[1].split("&");
  var obj = \\{\\};
  for (var i = 0; i < arr.length; i++) \\{
    var arg = arr[i].split("=");
    obj[arg[0]] = arg[1];
  \\}
  return obj;
\\}
var href = getQueryString();
console.log(href["categoryId"]);
```

方法二：(正则版,URL 存在#则不适用)

```js
function getQueryString(name) \\{
  var reg = new RegExp("(^|&)" + name + "=([^&]*)(&|$)");
  var r = window.location.search.substr(1).match(reg);
  if (r != null) return unescape(r[2]);
  return null;
\\}
console.log(getQueryString("categoryId"));
```

方法三：(正则升级版)

```js
function getQueryString(name) \\{
  // 未传参，返回空
  if (!name) return null;
  // 查询参数：先通过search取值，如果取不到就通过hash来取
  var after = window.location.search;
  after = after.substr(1) || window.location.hash.split("?")[1];
  // 地址栏URL没有查询参数，返回空
  if (!after) return null;
  // 如果查询参数中没有"name"，返回空
  if (after.indexOf(name) === -1) return null;
  var reg = new RegExp("(^|&)" + name + "=([^&]*)(&|$)");
  // 当地址栏参数存在中文时，需要解码，不然会乱码
  var r = decodeURI(after).match(reg);
  // 如果url中"name"没有值，返回空
  if (!r) return null;
  return r[2];
\\}
console.log(getQueryString("categoryId"));
```



### js 实现一个打点计时器

1、从 start 到 end（包含 start 和 end），每隔 100 毫秒 console.log 一个数字，每次数字增幅 1
2、返回的对象中需要包含一个 cancel 方法，用于停止定时操作
3、第一个数需要立即输出

```js
// 实现法一（setTimeout()方法）：

function count(start, end) \\{
  if (start <= end) \\{
    console.log(start++);
    st = setTimeout(function() \\{
      count(start, end);
    \\}, 100);
  \\}
  return \\{
    cancel: function() \\{
      clearTimeout(st);
    \\}
  \\};
\\}
count(1, 10);

// 实现法二（setInterval()方法）：

function count(start, end) \\{
  console.log(start++);
  var timer = setInterval(function() \\{
    if (start <= end) \\{
      console.log(start++);
    \\}
  \\}, 100);
  return \\{
    cancel: function() \\{
      clearInterval(timer);
    \\}
  \\};
\\}
count(1, 10);
```

知识点：
setTimeout()方法用于在指定的毫秒数后调用函数或计算表达式。
语法：setTimeout(code, millisec)
注意：setTimeout() 只执行 code 一次。如果要多次调用，请使用 setInterval() 或者让 code 自身再次调用 setTimeout()。

setInterval() 方法可按照指定的周期（以毫秒计）来调用函数或计算表达式。
语法：setInterval(code ,millisec[,"lang"])
setInterval() 方法会不停地调用函数，直到 clearInterval() 被调用或窗口被关闭。由 setInterval() 返回的 ID 值可用作 clearInterval() 方法的参数。



###  正则表达式，验证手机号码，验证规则：11 位数字，以 1 位开头

```js
checkphonenumber(number) \\{
	if (number == null || number.length != 11) \\{
		return false
	\\} else \\{
		// 移动号段正则表达式
		var pat1 = '^((13[4-9])|(147)|(15[0-2,7-9])|(178)|(18[2-4,7-8]))\\d\\{8\\}|(1705)\\d\\{7\\}$';
		// 联通号段正则表达式
		var pat2 = '^((13[0-2])|(145)|(15[5-6])|(176)|(18[5,6]))\\d\\{8\\}|(1709)\\d\\{7\\}$';
		// 电信号段正则表达式
		var pat3 = '^((133)|(153)|(177)|(18[0,1,9])|(149))\\d\\{8\\}$';
		// 虚拟运营商正则表达式
		var pat4 = '^((170))\\d\\{8\\}|(1718)|(1719)\\d\\{7\\}$';
		if (!part1.test(number)) \\{
			return false
		\\}
		if (!part2.test(number)) \\{
			return false
		\\}
		if (!part3.test(number)) \\{
			return false
		\\}
		if (!part4.test(number)) \\{
			return false
		\\}
	\\}
	return true
\\}
```



### 请给 Array 本地对象增加一个原型方法，他的用途是删除数组中重复的条目并按升序排序，最后返回新数组。

```js
Array.prototype.distinct = function() \\{
  var ret = [];
  for (var i = 0; i < this.length; i++) \\{
    for (var j = i + 1; j < this.length; ) \\{
      if (this[i] === this[j]) \\{
        ret.push(this.splice(j, 1)[0]);
      \\} else \\{
        j++;
      \\}
    \\}
  \\}
  return ret;
\\};
console.log(["a", "b", "c", "d", "b", "a", "e"].distinct()); // ["a", "b"]
```



### 为字符串扩展一个 rewrite 函数，接收一个正则 pattern 和一个字符串 result,如果该字符串符合 pattern， 则以 result 对结果进行转义输出。 

```js
"/foo".rewrite(/^\/foo/, "/bar");
"u1234".rewrite(/^\/u(\d+)/, "/user/$1");
"/i".rewrite(/^\o/, "/ooo");
```



### 实现一个 js 对象序列化函数，将 js 对象序列化为可反序列化的代码，要求 1.尽量和 json 兼容，2.支持不可序列化的值，如 undefined/NaN/Infinify-Infinity，3. 支持特殊对象，如正则、Date 等

```js
serialize(\\{\\});
serialize(\\{ a: "b" \\});
serialize(\\{ a: 0 / 0 \\});
serialize(\\{ a: /foo/ \\});
```



设计一道 JavaScript 的 range 算法如下：

range(1, 10, 3) 返回 [1, 4, 7, 10];
range('A', 'F', 2) 返回 ['A', 'C', 'E']
// 请使用 JavaScript 语言实现该功能（可以使用 ES6）



### 头条的视频网站上支持了弹幕，假设一个视频有很多弹幕，弹幕的数据是一个数组，格式定义如下：

```

[
    \\{
        time: Number,
        content: String
    \\},
    \\{
        time: Number,
        content: String
    \\}...
]
(其中 time 表示时间，content表示弹幕内容)，那么如何快速定位到某个时间点的弹幕，请编码实现（不使用数组的 sort 方法）

```



### 尝试实现注释部分的 JavaScript 代码， 可在其他任何地方添加更多代码。

```
var Obj = function(msg) \\{
    this.msg = msg;
    this.shout = function () \\{
        alert(this.msg)
    \\}
    this.waitAndShout = function() \\{
        // 隔五秒钟后执行上面的 shout 方法
    \\}
\\}
```



### 请编写一个 JavaScript 函数 parseQuerySting, 它的用途是把 URL 参数解析为一个对象

```
var url = "http://www.58.com/index.aspx?key0=0&key1=1&key2=2..."
var obj = parseQuerySting(url);
alert(obj.key0) // 输出 0
```



### 判断一个字符串中出现次数最多的字符，统计这个次数

```js
var str = "asdfssaaasasasasaa";
var json = \\{\\};
for (var i = 0; i < str.length; i++) \\{
  if (!json[str.charAt(i)]) \\{
    json[str.charAt(i)] = 1;
  \\} else \\{
    json[str.charAt(i)]++;
  \\}
\\}
var iMax = 0;
var iIndex = "";
for (var i in json) \\{
  if (json[i] > iMax) \\{
    iMax = json[i];
    iIndex = i;
  \\}
\\}
alert("出现次数最多的是:" + iIndex + "出现" + iMax + "次");
```



### 写一个获取非行间样式的函数

```js
function getStyle(obj, attr, value) \\{
  if (!value) \\{
    if (obj.currentStyle) \\{
      return obj.currentStyle(attr);
    \\} else \\{
      obj.getComputedStyle(attr, false);
    \\}
  \\} else \\{
    obj.style[attr] = value;
  \\}
\\}
```



### 字符串反转，如将 '12345678' 变成 '87654321'

```js
//思路：先将字符串转换为数组 split()，利用数组的反序函数 reverse()颠倒数组，再利用 jion() 转换为字符串
var str = "12345678";
str = str
  .split("")
  .reverse()
  .join("");
```



### 将数字 12345678 转化成 RMB 形式 如： 12,345,678

```js
//个人方法；
//思路：先将数字转为字符， str= str + '' ;
//利用反转函数，每三位字符加一个 ','最后一位不加； re()是自定义的反转函数，最后再反转回去！
for (var i = 1; i <= re(str).length; i++) \\{
  tmp += re(str)[i - 1];
  if (i \\% 3 == 0 && i != re(str).length) \\{
    tmp += ",";
  \\}
\\}
```



### 生成 5 个不同的随机数

```js
//思路：5个不同的数，每生成一次就和前面的所有数字相比较，如果有相同的，则放弃当前生成的数字！
var num1 = [];
for (var i = 0; i < 5; i++) \\{
  num1[i] = Math.floor(Math.random() * 10) + 1; //范围是 [1, 10]
  for (var j = 0; j < i; j++) \\{
    if (num1[i] == num1[j]) \\{
      i--;
    \\}
  \\}
\\}
```



### 去掉数组中重复的数字

方法一

```js
//思路：每遍历一次就和之前的所有做比较，不相等则放入新的数组中！
//这里用的原型 个人做法；
Array.prototype.unique = function() \\{
  var len = this.length,
    newArr = [],
    flag = 1;
  for (var i = 0; i < len; i++, flag = 1) \\{
    for (var j = 0; j < i; j++) \\{
      if (this[i] == this[j]) \\{
        flag = 0; //找到相同的数字后，不执行添加数据
      \\}
    \\}
    flag ? newArr.push(this[i]) : "";
  \\}
  return newArr;
\\};
```

方法二

```js
(function(arr) \\{
  var len = arr.length,
    newArr = [],
    flag;
  for (var i = 0; i < len; i += 1, flag = 1) \\{
    for (var j = 0; j < i; j++) \\{
      if (arr[i] == arr[j]) \\{
        flag = 0;
      \\}
    \\}
    flag ? newArr.push(arr[i]) : "";
  \\}
  alert(newArr);
\\})([1, 1, 22, 3, 4, 55, 66]);
```



### 阶乘函数

```js
//原型方法
Number.prototype.N = function() \\{
  var re = 1;
  for (var i = 1; i <= this; i++) \\{
    re *= i;
  \\}
  return re;
\\};
var num = 5;
alert(num.N());
```



### 看题做答

```js
	function f1()\\{
    var tmp = 1;
    this.x = 3;
    console.log(tmp);    //A
    console.log(this.x)；     //B
\\}
var obj = new f1(); //1
console.log(obj.x)     //2
console.log(f1());        //3
```

解析：   
     这道题让我重新认识了对象和函数，首先看代码（1），这里实例话化了 f1 这个类。相当于执行了 f1 函数。所以这个时候 A 会输出 1， 而 B 这个时候的 this 代表的是 实例化的当前对象 obj B 输出 3.。 代码（2）毋庸置疑会输出 3， 重点 代码（3）首先这里将不再是一个类，它只是一个函数。那么 A 输出 1， B 呢？这里的 this 代表的其实就是 window 对象，那么 this.x 就是一个全局变量 相当于在外部 的一个全局变量。所以 B 输出 3。最后代码由于 f 没有返回值那么一个函数如果没返回值的话，将会返回 underfined ，所以答案就是 ： 1， 3， 3， 1， 3， underfined 。



### 下面输出多少？

```js
var o1 = new Object();
var o2 = o1;
o2.name = "CSSer";
console.log(o1.name);
```

解析：

如果不看答案，你回答真确了的话，那么说明你对 javascript 的数据类型了解的还是比较清楚了。js 中有两种数据类型，分别是：基本数据类型和引用数据类型（object Array）。对于保存基本类型值的变量，变量是按值访问的，因为我们操作的是变量实际保存的值。对于保存引用类型值的变量，变量是按引用访问的，我们操作的是变量值所引用（指向）的对象。答案就清楚了：  //CSSer;



### 下面输出多少？

```js
function changeObjectProperty(o) \\{
  o.siteUrl = "http://www.csser.com/";
  o = new Object();
  o.siteUrl = "http://www.popcg.com/";
\\}
var CSSer = new Object();
changeObjectProperty(CSSer);
console.log(CSSer.siteUrl); //
```

解析：

如果 CSSer 参数是按引用传递的，那么结果应该是"http://www.popcg.com/"，但实际结果却仍是"http://www.csser.com/"。事实是这样的：在函数内部修改了引用类型值的参数，该参数值的原始引用保持不变。我们可以把参数想象成局部变量，当参数被重写时，这个变量引用的就是一个局部变量，局部变量的生存期仅限于函数执行的过程中，函数执行完毕，局部变量即被销毁以释放内存。    
    （补充：内部环境可以通过作用域链访问所有的外部环境中的变量对象，但外部环境无法访问内部环境。每个环境都可以向上搜索作用域链，以查询变量和函数名，反之向下则不能。）



### 输出多少？

```js
var a = 6;
setTimeout(function() \\{
  var a = 666;
  alert(a); // 输出666，
\\}, 1000);
a = 66;
```

因为 var a = 666;定义了局部变量 a，并且赋值为 666，根据变量作用域链，
全局变量处在作用域末端，优先访问了局部变量，从而覆盖了全局变量 。

```js
var a = 6;
setTimeout(function() \\{
  alert(a); // 输出undefined
  var a = 666;
\\}, 1000);
a = 66;
```

因为 var a = 666;定义了局部变量 a，同样覆盖了全局变量，但是在 alert(a);之前
a 并未赋值，所以输出 undefined。

```js
var a = 6;
setTimeout(function() \\{
  alert(a);
  var a = 66;
\\}, 1000);
a = 666;
alert(a);
// 666, undefined;
```

记住： 异步处理，一切 OK 声明提前



### JS 的继承性？

```js
window.color = "red";
var o = \\{ color: "blue" \\};
function sayColor() \\{
  alert(this.color);
\\}
sayColor(); //red
sayColor.call(this); //red this-window对象
sayColor.call(window); //red
sayColor.call(o); //blue
```



### 精度问题: JS 精度不能精确到 0.1 所以  。。。。同时存在于值和差值中

```js
var n = 0.3,
  m = 0.2,
  i = 0.2,
  j = 0.1;
alert(n - m == i - j); //false
alert(n - m == 0.1); //false
alert(i - j == 0.1); //true
```



### 加减运算

```js
alert("5" + 3); //53 string
alert("5" + "3"); //53 string
alert("5" - 3); //2 number
alert("5" - "3"); //2 number
```



### 结果是什么？

```js
function foo() \\{
  foo.a = function() \\{
    alert(1);
  \\};
  this.a = function() \\{
    alert(2);
  \\};
  a = function() \\{
    alert(3);
  \\};
  var a = function() \\{
    alert(4);
  \\};
\\}
foo.prototype.a = function() \\{
  alert(5);
\\};
foo.a = function() \\{
  alert(6);
\\};
foo.a(); //6
var obj = new foo();
obj.a(); //2
foo.a(); //1
```



### 输出结果

```js
var a = 5;
function test() \\{
  a = 0;
  alert(a);
  alert(this.a); //没有定义 a这个属性
  var a;
  alert(a);
\\}
test(); // 0, 5, 0
new test(); // 0, undefined, 0 //由于类它自身没有属性a， 所以是undefined
```



### 计算字符串字节数

```js
new (function(s) \\{
  if (!arguments.length || !s) return null;
  if ("" == s) return 0;
  var l = 0;
  for (var i = 0; i < s.length; i++) \\{
    if (s.charCodeAt(i) > 255) l += 2;
    else l += 1; //charCodeAt()得到的是unCode码
  \\} //汉字的unCode码大于 255bit 就是两个字节
  alert(l);
\\})("hello world!");
```



### 结果是

var bool = !!2; alert(bool)；//true;
双向非操作可以把字符串和数字转换为布尔值



### 声明对象，添加属性，输出属性

```js
var obj = \\{
  name: "leipeng",
  showName: function() \\{
    alert(this.name);
  \\}
\\};
obj.showName();
```



### 匹配输入的字符：第一个必须是字母或下划线开头，长度 5-20

```js
var reg = /^[a-zA-Z][a-zA-Z0-9_]\\{5,20\\}/,
  name1 = "leipeng",
  name2 = "0leipeng",
  name3 = "你好leipeng",
  name4 = "hi";
alert(reg.test(name1));
alert(reg.test(name2));
alert(reg.test(name3));
alert(reg.test(name4));
```



### 检测变量类型

```js
function checkStr(str) \\{
  typeof str == "string" ? alert("true") : alert("false");
\\}
checkStr("leipeng");
```



### 如何在 HTML 中添加事件，几种方法？

```
1、标签之中直接添加 onclick="fun()";
2、JS 添加 Eobj.onclick = method;
3、现代事件  IE： obj.attachEvent('onclick', method)；
            FF: obj.addEventListener('click', method, false);
```



### 请问代码实现 outerHTML

```js
//说明：outerHTML其实就是innerHTML再加上本身；
Object.prototype.outerHTML = function() \\{
  var innerCon = this.innerHTML, //获得里面的内容
    outerCon = this.appendChild(innerCon); //添加到里面
  alert(outerCon);
\\};
```

演示代码：

```html     
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Document</title>
  </head>
  <body>
    <div id="outer">
      hello
    </div>
    <script>
      Object.prototype.outerHTML = function() \\{
        var innerCon = this.innerHTML, //获得里面的内容
          outerCon = this.appendChild(innerCon); //添加到里面
        alert(outerCon);
      \\};
      function $(id) \\{
        return document.getElementById(id);
      \\}
      alert($("outer").innerHTML);
      alert($("outer").outerHTML);
    </script>
  </body>
</html>
```



### JS 中的简单继承 call 方法！

```js
//顶一个父母类，注意：类名都是首字母大写的哦！
function Parent(name, money) \\{
  this.name = name;
  this.money = money;
  this.info = function() \\{
    alert("姓名： " + this.name + " 钱： " + this.money);
  \\};
\\} //定义孩子类
function Children(name) \\{
  Parent.call(this, name); //继承 姓名属性，不要钱。
  this.info = function() \\{
    alert("姓名： " + this.name);
  \\};
\\} //实例化类
var per = new Parent("parent", 800000000000);
var chi = new Children("child");
per.info();
chi.info();
```



### 解析 URL 成一个对象？

```js
String.prototype.urlQueryString = function() \\{
  var url = this.split("?")[1].split("&"),
    len = url.length;
  this.url = \\{\\};
  for (var i = 0; i < len; i += 1) \\{
    var cell = url[i].split("="),
      key = cell[0],
      val = cell[1];
    this.url["" + key + ""] = val;
  \\}
  return this.url;
\\};
var url = "?name=12&age=23";
console.log(url.urlQueryString().age);
```



### 看下列代码输出什么？

```js
var foo = "11" + 2 - "1";
console.log(foo);
console.log(typeof foo);
// 执行完后foo的值为111，foo的类型为Number。
```



### 看下列代码,输出什么？

```js
var a = new Object();
a.value = 1;
b = a;
b.value = 2;
alert(a.value);
// 执行完后输出结果为2
```



### 已知数组 var stringArray = ["This”, "is”, "Baidu”, "Campus”]，Alert 出”This is Baidu Campus”。

alert(stringArray.join(""))



### 请描述出下列代码运行的结果

```js
function d() \\{
  console.log(this);
\\}
d();
```



### 需要将变量 e 的值修改为“a+b+c+d”,请写出对应的代码

var e=”abcd”;



### 下面这个 ul，如何点击每一列的时候 alert 其 index?（闭包）

```html
<ul id="”test”">
  <li>这是第一条</li>
  <li>这是第二条</li>
  <li>这是第三条</li>
</ul>
```

答案：

```js
// 方法一：
var lis = document.getElementById("2223").getElementsByTagName("li");
for (var i = 0; i < 3; i++) \\{
  lis[i].index = i;
  lis[i].onclick = function() \\{
    alert(this.index);
  \\};
\\}
//方法二：
var lis = document.getElementById("2223").getElementsByTagName("li");
for (var i = 0; i < 3; i++) \\{
  lis[i].index = i;
  lis[i].onclick = (function(a) \\{
    return function() \\{
      alert(a);
    \\};
  \\})(i);
\\}
```



### 小贤是一条可爱的小狗(Dog)，它的叫声很好听(wow)，每次看到主人的时候就会乖乖叫一声(yelp)。从这段描述可以得到以下对象：

```js
	function Dog() \\{
      this.wow = function() \\{
               alert(’Wow’);
      \\}
      this.yelp = function() \\{
              this.wow();
      \\}
\\}
```

小芒和小贤一样，原来也是一条可爱的小狗，可是突然有一天疯了(MadDog)，一看到人就会每隔半秒叫一声(wow)地不停叫唤(yelp)。请根据描述，按示例的形式用代码来实。（继承，原型，setInterval）

```js
function MadDog() \\{
  this.yelp = function() \\{
    var self = this;
    setInterval(function() \\{
      self.wow();
    \\}, 500);
  \\};
\\}
MadDog.prototype = new Dog();
//for test
var dog = new Dog();
dog.yelp();
var madDog = new MadDog();
madDog.yelp();
```



### 实现一个函数 clone，可以对 JavaScript 中的 5 种主要的数据类型（包括 Number、String、Object、Array、Boolean）进行值复制

- 考察点 1：对于基本数据类型和引用数据类型在内存中存放的是值还是指针这一区别是否清楚
- 考察点 2：是否知道如何判断一个变量是什么类型的
- 考察点 3：递归算法的设计

```js
// 方法一：
Object.prototype.clone = function() \\{
  var o = this.constructor === Array ? [] : \\{\\};
  for (var e in this) \\{
    o[e] = typeof this[e] === "object" ? this[e].clone() : this[e];
  \\}
  return o;
\\};
/**
 * 克隆一个对象
 * @param Obj
 * @returns
 */
//方法二：
function clone(Obj) \\{
  var buf;
  if (Obj instanceof Array) \\{
    buf = []; //创建一个空的数组
    var i = Obj.length;
    while (i--) \\{
      buf[i] = clone(Obj[i]);
    \\}
    return buf;
  \\} else if (Obj instanceof Object) \\{
    buf = \\{\\}; //创建一个空对象
    for (var k in Obj) \\{
      //为这个对象添加新的属性
      buf[k] = clone(Obj[k]);
    \\}
    return buf;
  \\} else \\{
    //普通变量直接赋值
    return Obj;
  \\}
\\}
```



### 输出今天的日期，以 YYYY-MM-DD 的方式，比如今天是 2014 年 9 月 26 日，则输出 2014-09-26

```js
var d = new Date();
// 获取年，getFullYear()返回4位的数字
var year = d.getFullYear();
// 获取月，月份比较特殊，0是1月，11是12月
var month = d.getMonth() + 1;
// 变成两位
month = month < 10 ? "0" + month : month;
// 获取日
var day = d.getDate();
day = day < 10 ? "0" + day : day;
alert(year + "-" + month + "-" + day);
```



### 写出函数 DateDemo 的返回结果，系统时间假定为今天

```js
function DateDemo() \\{
  var d,
    s = "今天日期是：";
  d = new Date();
  s += d.getMonth() + "/";
  s += d.getDate() + "/";
  s += d.getYear();
  return s;
\\}
```

答案：今天日期是：7/17/2010



### 只允许使用 + - _ / 和 Math._ ，求一个函数 y = f(x, a, b);当 x > 100 时返回 a 的值，否则返回 b 的值，不能使用 if else 等条件语句，也不能使用|,?:,数组。

```js
function f(x, a, b) \\{
  var temp = Math.ceil(Math.min(Math.max(x - 100, 0), 1));
  return a * temp + b * (1 - temp);
\\}
console.log(f(-10, 1, 2));
```







## 看代码，写结果

### 看题算结果

```js
var tasks = []; // 这里存放异步操作的 Promise
var output = i =>
  new Promise(resolve => \\{
    setTimeout(() => \\{
      console.log(new Date(), i);
      resolve();
    \\}, 1000 * i);
  \\});

// 生成全部的异步操作
for (var i = 0; i < 5; i++) \\{
  tasks.push(output(i));
\\}

console.log(new Date, i);
```

答案：

```
Mon Aug 12 2019 09:37:36 GMT+0800 (中国标准时间) 5
Mon Aug 12 2019 09:33:55 GMT+0800 (中国标准时间) 0
然后每隔1s打印
Mon Aug 12 2019 09:33:56 GMT+0800 (中国标准时间) 1
Mon Aug 12 2019 09:33:57 GMT+0800 (中国标准时间) 2
Mon Aug 12 2019 09:33:58 GMT+0800 (中国标准时间) 3
Mon Aug 12 2019 09:33:59 GMT+0800 (中国标准时间) 4
```

解析：[参考](https://www.cnblogs.com/adouwt/p/6481479.html)



### 看题算结果

```js
// 模拟其他语言中的 sleep，实际上可以是任何异步操作
const sleep = timeountMS =>
  new Promise(resolve => \\{
    setTimeout(resolve, timeountMS);
  \\});

(async () => \\{
  // 声明即执行的 async 函数表达式
  for (var i = 0; i < 5; i++) \\{
    await sleep(1000);
    console.log(new Date(), i);
  \\}

  await sleep(1000);
  console.log(new Date(), i);
\\})();
```

答案：每隔1s打印

```
Mon Aug 12 2019 09:39:02 GMT+0800 (中国标准时间) 0
Mon Aug 12 2019 09:39:03 GMT+0800 (中国标准时间) 1
Mon Aug 12 2019 09:39:04 GMT+0800 (中国标准时间) 2
Mon Aug 12 2019 09:39:05 GMT+0800 (中国标准时间) 3
Mon Aug 12 2019 09:39:06 GMT+0800 (中国标准时间) 4
Mon Aug 12 2019 09:39:07 GMT+0800 (中国标准时间) 5
```

解析：[参考](https://www.cnblogs.com/adouwt/p/6481479.html)



### 请写出以下代码的执行结果

```
(function() \\{
    fn();
    var fn = function() \\{
        alert(1);
    \\}
    fn();
    function fn() \\{
        alert(2)
    \\}
\\})()
```



###  请说明以下各种情况的执行结果，并注明产生对应结果的理由

```
function doSomething() \\{
    alert(this);
\\}

a) element.onclick = doSomething, 点击 element 元素后
b) element.onclick = function() doSomething()\\{\\}, 点击 element 元素后
c) 直接执行 doSomething()
```



###  请写出以下代码的执行结果

```
var obj = \\{\\};
var events = \\{ m1: "clicked", m2: "changed"\\};
for(e in events) \\{
    obj[e] = function() \\{
        alert(events[e])
    \\}
\\}

alert(obj.m1 == obj.m2);
obj.m1();
obj.m2();
```



###  以下代码输出多少

```js
var name = "world";
(function () \\{
    if (typeof name === "undefined") \\{
        var name = "jack";
        console.log("Hi!" + name);
    \\} else \\{
        console.log("Hello," + name)
    \\}
\\})()

==> Hi!jack

var name = "world";
(function (name) \\{
    if (typeof name === "undefined") \\{
        var name = "jack";
        console.log("Hi!" + name);
    \\} else \\{
        console.log("Hello," + name)
    \\}
\\})(name)

==> Hello,world
```



### 计算打印结果

```js
function fun(n, o) \\{
  console.log(o);
  return \\{
    fun: function(m) \\{
      return fun(m, n);
    \\}
  \\};
\\}
//    var a = fun(0);
//    a.fun(1)
//    a.fun(2)
//    a.fun(3)

// 打印
// undefined 0 0 0

//    var b = fun(0).fun(1).fun(2).fun(3)
// 打印 undefined 0 1 2

var c = fun(0).fun(1);
c.fun(2);
c.fun(3);
// 打印
// undefined 0 1 1
```



### 看下面代码，给出输出结果

```js
for (var i = 1; i <= 3; i++) \\{
  console.log(i);
\\}
// 1 2 3
```

但是

```js
for (var i = 1; i <= 3; i++) \\{
  setTimeout(() => \\{
    // setTimout在for里面是异步执行的，在延迟输出的时候，i的值已经是4了
    console.log(i);
  \\}, 0);
\\}
// 4 4 4
```

如何输出 1 2 3

答案：

立即执行函数

```js
for (var i = 1; i <= 3; i++) \\{
  setTimeout(
    (i => \\{
      console.log(i);
    \\})(i),
    0
  );
\\}
```



### 看下面代码，给出输出结果(考察闭包及++运算符)

```js
function Foo() \\{
  var i = 0;
  return function() \\{
    console.log(i++);
  \\};
\\}
var f1 = Foo(),
  f2 = Foo();

f1(); // 0
f1(); // 1
f2(); // 0
```

```js
function fn() \\{
  var a = 1;
  return function() \\{
    a++;
    console.log(a);
  \\};
\\}
var b = fn();
console.log(b());
// 2
```

```js
function fn() \\{
  var a = 1;
  return function() \\{
    console.log(a++);
  \\};
\\}
var b = fn();
console.log(b());
// 1
```



### 看下面代码，给出输出结果(考察时间戳)

```js
//总结：第一个setTimeout，时间间隔<1000的话，输出1000多，>1000的话，输出间隔值多
//     第二个setTimeout，是1000+时间间隔
var dateNum = new Date();
setTimeout(function() \\{
  console.log(new Date() - dateNum);
\\}, 1200); //1200多
while (new Date() - dateNum < 1000) \\{
  var a = 1;
\\}
setTimeout(function() \\{
  console.log(new Date() - dateNum);
\\}, 1500); // 2500左右
```



### 看题写结果

```js
var output = function(i) \\{
  setTimeout(function() \\{
    console.log(i);
  \\}, 1000);
\\};

for (var i = 0; i < 5; i++) \\{
  output(i); // 这里传过去的 i 值被复制了
\\}

console.log(i);
```

答案：

5
0
1
2
3
4

解析：[参考](https://www.cnblogs.com/adouwt/p/6481479.html)



第 16 题

```js
function test() \\{
  console.log("test函数");
\\}
setTimeout(function() \\{
  console.log("定时器回调函数");
\\}, 0);
test();
function foo() \\{
  var name = "hello";
\\}
```



### 下列 JavaScript 代码执行后，依次 alert 的结果是

```js
var obj = \\{ proto: \\{ a: 1, b: 2 \\} \\};
function F() \\{\\}
F.prototype = obj.proto;
var f = new F();
obj.proto.c = 3;
obj.proto = \\{ a: -1, b: -2 \\};
alert(f.a);
alert(f.c);
delete F.prototype["a"];
alert(f.a);
alert(obj.proto.a);

```



### 下列 JavaScript 代码执行后，运行的结果是

```html
<button id="btn">点击我</button>
```

```js
var btn = document.getElementById("btn");
var handler = \\{
  id: "_eventHandler",
  exec: function() \\{
    alert(this.id);
  \\}
\\};
btn.addEventListener("click", handler.exec.false);
```



### 输出结果是多少？

1）

```js
var a; // undefined
var b = a * 0; // NaN
if (b == b) \\{
  // false
  console.log(b * 2 + "2" - 0 + 4);
\\} else \\{
  console.log(!b * 2 + "2" - 0 + 4); // 22 + 4 = 26
\\}
```

答案：26

2）

```js
<script>
    var a = 1;
</script>
<script>
var a;
var b = a * 0;
if (b == b) \\{ // true
       console.log(b * 2 + "2" - 0 + 4); // 6
\\} else \\{
       console.log(!b * 2 + "2" - 0 + 4);
\\}
</script>
```

答案：6

3）

```js
var t = 10;
function test(t) \\{
  var t = t++;
\\}
test(t);
console.log(t); // 外部不能访问函数内的变量
```

答案：10

4）

```js
var t = 10;
function test(test) \\{
  var t = test++;
\\}
test(t);
console.log(t);
```

答案：10

6）

```js
var t = 10;
function test(test) \\{
  t = test++;
  console.log(t);
\\}
test(t);
console.log(t);
```

答案：10

7）

```js
var t = 10;
function test(test) \\{
  t = t + test;
  console.log(t);
  var t = 3;
\\}
test(t);
console.log(t);
```

答案：NaN 10

8）

```js
var a;
var b = a / 0;
if (b == b) \\{
  console.log(b * 2 + "2" - 0 + 4);
\\} else \\{
  console.log(!b * 2 + "2" - 0 + 4);
\\}
```

答案：26

9）

```js
<script>
     var a = 1;
</script>
<script>
   var a;
   var b = a / 0;
   if (b == b) \\{
       console.log(b * 2 + "2" + 4);
   \\} else \\{
       console.log(!b * 2 + "2" + 4);
   \\}
</script>
```

答案：Infinity24



### 下列 JavaScript 代码执行后，iNum 的值是

```js
var iNum = 0;
for (var i = 1; i < 10; i++) \\{
  if (i \\% 5 == 0) \\{
    continue;
  \\}
  iNum++;
\\}
console.log(iNum);
```

答案：8



### 下列 JavaScript 代码执行后，依次打印的结果是

```js
(function test() \\{
  var a = (b = 5);
  console.log(typeof a);
  console.log(typeof b);
\\})();
console.log(typeof a);
console.log(typeof b);
```

答案：

```
number
number
undefined
number
```



### console.log( 8 | 1 ); 输出值是多少？

9



### 请写出三种以上的 Firefox 有但 InternetExplorer 没有的属性和函数

1、在 IE 下可通过`document.frames["id"];`得到该 IFRAME 对象，

而在火狐下则是通过`document.getElementById("content_panel_if").contentWindow;`

2、IE 的写法： `_tbody=_table.childNodes[0]`
在 FF 中，firefox 会在子节点中包含空白则第一个子节点为空白""， 而 ie 不会返回空白
可以通过`if("" != node.nodeName)`过滤掉空白子对象

3、模拟点击事件

```js
if (document.all) \\{
  //ie下
  document.getElementById("a3").click();
\\} else \\{
  //非IE
  var evt = document.createEvent("MouseEvents");
  evt.initEvent("click", true, true);
  document.getElementById("a3").dispatchEvent(evt);
\\}
```

4、事件注册

```js
if (isIE) \\{
  window.attachEvent("onload", init);
\\} else \\{
  window.addEventListener("load", init, false);
\\}
```



### 编写一个快速方法将 html 的 sup 提取转换为一个数组

```js
// 编写一个快速方法将html的sup提取转换为一个数组，如：
let str = "气量(10<sup>8</sup>m<sup>3</sup>)";
// 输出结果
// ['气量(10',8,'m',3,')']
```

答案：

```js
// 方法1
str.split(/\<\/?sup\>/);
// 方法2
str.split(/<[^>]+>/);
```



### 求 num 的值

```js
//   面试题1
var num = 123;
function f1() \\{
  console.log(num); // 123
\\}
function f2() \\{
  var num = 456;
  f1();
\\}
f2();

//面试题1 变式
var num = 123;
function f1(num) \\{
  console.log(num); // 456
\\}
function f2() \\{
  var num = 456;
  f1(num);
\\}
f2();

//面试题1  变式
var num = 123;
function f1() \\{
  console.log(num); // 456
\\}
f2();
function f2() \\{
  num = 456; //这里是全局变量
  f1();
\\}
console.log(num); // 456
```



### 有一个函数，参数是一个函数，返回值也是一个函数，返回的函数功能和入参的函数相似，但这个函数只能执行 3 次，再次执行无效，如何实现

这个题目是考察闭包的使用

答案：

```js
function sayHi() \\{
  console.log("hi");
\\}

function threeTimes(fn) \\{
  let times = 0;
  return () => \\{
    if (times++ < 3) \\{
      fn();
    \\}
  \\};
\\}

const newFn = threeTimes(sayHi);
newFn();
newFn();
newFn();
newFn();
newFn(); // 后面两次执行都无任何反应
```

通过闭包变量 `times` 来控制函数的执行



### 实现 add 函数,让 add(a)(b)和 add(a,b)两种调用结果相同

```js
function add(a, b) \\{
  if (b === undefined) \\{
    return function(x) \\{
      return a + x;
    \\};
  \\}

  return a + b;
\\}
```



### 格式化金钱，每千分位加逗号

```js
function format(str) \\{
  let s = "";
  let count = 0;
  for (let i = str.length - 1; i >= 0; i--) \\{
    s = str[i] + s;
    count++;
    if (count \\% 3 == 0 && i != 0) \\{
      s = "," + s;
    \\}
  \\}
  return s;
\\}
```

```js
function format(str) \\{
  return str.replace(/(\d)(?=(?:\d\\{3\\})+$)/g, "$1,");
\\}
```



### 反转数组

**要求**

**input**: I am a student <br>
**output**: student a am I <br>
输入是数组 输出也是数组<br>
不允许用 `split` `splice` `reverse`<br>

答案：

**解法一**

```js
function reverseArry(arry) \\{
  const str = arry.join(" ");
  const result = [];
  let word = "";
  for (let i = 0, len = str.length; i < len; i++) \\{
    if (str[i] != " ") \\{
      word += str[i];
    \\} else \\{
      result.unshift(word);
      word = "";
    \\}
  \\}

  result.unshift(word);
  return result;
\\}

console.log(reverseArry(["I", "am", "a", "student"]));
// ["student", "a", "am", "I"]
```

**解法二**

```js
function reverseArry(arry) \\{
  const result = [];
  const distance = arry.length - 1;
  for (let i = distance; i >= 0; i--) \\{
    result[distance - i] = arry[i];
  \\}

  return result;
\\}
```



### 说出以下函数的作用是？空白区域应该填写什么？

```js
//define
(function(window) \\{
  function fn(str) \\{
    this.str = str;
  \\}
  fn.prototype.format = function() \\{
    var arg = ______;
    return this.str.replace(_____, function(a, b) \\{
      return arg[b] || "";
    \\});
  \\};
  window.fn = fn;
\\})(window);
//use
(function() \\{
  var t = new fn('<p><a href="\\{0\\}">\\{1\\}</a><span>\\{2\\}</span></p>');
  console.log(t.format("http://www.alibaba.com", "Alibaba", "Welcome"));
\\})();
```

答案：访函数的作用是使用 format 函数将函数的参数替换掉\\{0\\}这样的内容，返回一个格式化后的结果：
第一个空是：arguments
第二个空是：/\\\{(\d+)\\\}/ig



### 原生 JS 的 window.onload 与 Jquery 的\$(document).ready(function()\\{\\})有什么不同？如何用原生 JS 实现 Jq 的 ready 方法？

window.onload()方法是必须等到页面内包括图片的所有元素加载完毕后才能执行。
\$(document).ready()是 DOM 结构绘制完毕后就执行，不必等到加载完毕。

```js
/*
 * 传递函数给whenReady()
 * 当文档解析完毕且为操作准备就绪时，函数作为document的方法调用
 */
var whenReady = (function() \\{
  //这个函数返回whenReady()函数
  var funcs = []; //当获得事件时，要运行的函数
  var ready = false; //当触发事件处理程序时,切换为true //当文档就绪时,调用事件处理程序
  function handler(e) \\{
    if (ready) return; //确保事件处理程序只完整运行一次 //如果发生onreadystatechange事件，但其状态不是complete的话,那么文档尚未准备好
    if (e.type === "onreadystatechange" && document.readyState !== "complete") \\{
      return;
    \\} //运行所有注册函数 //注意每次都要计算funcs.length //以防这些函数的调用可能会导致注册更多的函数
    for (var i = 0; i < funcs.length; i++) \\{
      funcs[i].call(document);
    \\} //事件处理函数完整执行,切换ready状态, 并移除所有函数
    ready = true;
    funcs = null;
  \\} //为接收到的任何事件注册处理程序
  if (document.addEventListener) \\{
    document.addEventListener("DOMContentLoaded", handler, false);
    document.addEventListener("readystatechange", handler, false); //IE9+
    window.addEventListener("load", handler, false);
  \\} else if (document.attachEvent) \\{
    document.attachEvent("onreadystatechange", handler);
    window.attachEvent("onload", handler);
  \\} //返回whenReady()函数
  return function whenReady(fn) \\{
    if (ready) \\{
      fn.call(document);
    \\} else \\{
      funcs.push(fn);
    \\}
  \\};
\\})();
```

如果上述代码十分难懂，下面这个简化版：

```js
function ready(fn) \\{
  if (document.addEventListener) \\{
    //标准浏览器
    document.addEventListener(
      "DOMContentLoaded",
      function() \\{
        //注销事件, 避免反复触发
        document.removeEventListener(
          "DOMContentLoaded",
          arguments.callee,
          false
        );
        fn(); //执行函数
      \\},
      false
    );
  \\} else if (document.attachEvent) \\{
    //IE
    document.attachEvent("onreadystatechange", function() \\{
      if (document.readyState == "complete") \\{
        document.detachEvent("onreadystatechange", arguments.callee);
        fn(); //函数执行
      \\}
    \\});
  \\}
\\}
```



### 对作用域上下文和 this 的理解，看下列代码：

```js
var User = \\{
  count: 1,
  getCount: function() \\{
    return this.count;
  \\}
\\};
console.log(User.getCount()); // what?
var func = User.getCount;
console.log(func()); // what?
```

问两处 console 输出什么？为什么？

答案：1 和 undefined。func 是在 winodw 的上下文中被执行的，所以会访问不到 count 属性。

解析：

继续追问，那么如何确保 Uesr 总是能访问到 func 的上下文，即正确返回 1。正确的方法是使用 Function.prototype.bind。兼容各个浏览器完整代码如下：

```js
Function.prototype.bind =
  Function.prototype.bind ||
  function(context) \\{
    var self = this;
    return function() \\{
      return self.apply(context, arguments);
    \\};
  \\};
var func = User.getCount.bind(User);
console.log(func());
```



### 在 Javascript 中什么是伪数组？如何将伪数组转化为标准数组？

伪数组（类数组）：无法直接调用数组方法或期望 length 属性有什么特殊的行为，但仍可以对真正数组遍历方法来遍历它们。典型的是函数的 argument 参数，还有像调用 getElementsByTagName,document.childNodes 之类的,它们都返回 NodeList 对象都属于伪数组。可以使用 Array.prototype.slice.call(fakeArray)将数组转化为真正的 Array 对象。

假设我们要给每个 log 方法添加一个”(app)”前缀，比如’hello world!’ ->’(app)hello world!’。方法如下：

```js
function log() \\{
  var args = Array.prototype.slice.call(arguments); //为了使用unshift数组方法，将argument转化为真正的数组
  args.unshift("(app)");
  console.log.apply(console, args);
\\}
```



### 定义一个 log 方法，让它可以代理 console.log 的方法。

可行的方法一：

```js
function log(msg) \\{
  console.log(msg);
\\}
log("hello world!"); // hello world!
```

如果要传入多个参数呢？显然上面的方法不能满足要求，所以更好的方法是：

```js
function log() \\{
  console.log.apply(console, arguments);
\\}
```

到此，追问 apply 和 call 方法的异同。

对于 apply 和 call 两者在作用上是相同的，即是调用一个对象的一个方法，以另一个对象替换当前对象。将一个函数的对象上下文从初始的上下文改变为由 thisObj 指定的新对象。

但两者在参数上有区别的。对于第一个参数意义都一样，但对第二个参数： apply 传入的是一个参数数组，也就是将多个参数组合成为一个数组传入，而 call 则作为 call 的参数传入（从第二个参数开始）。  如 func.call(func1,var1,var2,var3)对应的 apply 写法为：func.apply(func1,[var1,var2,var3]) 。



### 给 String 对象添加一个方法，传入一个 string 类型的参数，然后将 string 的每个字符间价格空格返回，例如：addSpace(“hello world”) // -> ‘h e l l o  w o r l d’

```js
String.prototype.spacify = function() \\{
  return this.split("").join(" ");
\\};
```

接着上述问题答案提问，1）直接在对象的原型上添加方法是否安全？尤其是在 Object 对象上。(这个我没能答出？希望知道的说一下。)　 2）函数声明与函数表达式的区别？
答案：在 js 中，解析器在向执行环境中加载数据时，对函数声明和函数表达式并非是一视同仁的，解析器会率先读取函数声明，并使其在执行任何代码之前可用（可以访问），至于函数表达式，则必须等到解析器执行到它所在的代码行，才会真正被解析执行。



### 请评价以下代码并给出改进意见

```js
if (window.addEventListener) \\{
  var addListener = function(el, type, listener, useCapture) \\{
    el.addEventListener(type, listener, useCapture);
  \\};
\\} else if (document.all) \\{
  addListener = function(el, type, listener) \\{
    el.attachEvent("on" + type, function() \\{
      listener.apply(el);
    \\});
  \\};
\\}
```

- 不应该在 if 和 else 语句中声明 addListener 函数，应该先声明；
- 不需要使用 window.addEventListener 或 document.all 来进行检测浏览器，应该使用能力检测； \*　由于 attachEvent 在 IE 中有 this 指向问题，所以调用它时需要处理一下

改进如下：

```js
function addEvent(elem, type, handler) \\{
  if (elem.addEventListener) \\{
    elem.addEventListener(type, handler, false);
  \\} else if (elem.attachEvent) \\{
    elem["temp" + type + handler] = handler;
    elem[type + handler] = function() \\{
      elem["temp" + type + handler].apply(elem);
    \\};
    elem.attachEvent("on" + type, elem[type + handler]);
  \\} else \\{
    elem["on" + type] = handler;
  \\}
\\}
```



### 编写一个 JavaScript 函数，输入指定类型的选择器(仅需支持 id，class，tagName 三种简单 CSS 选择器，无需兼容组合选择器)可以返回匹配的 DOM 节点，需考虑浏览器兼容性和性能。

```js
/*** @param selector \\{String\\} 传入的CSS选择器。* @return \\{Array\\}*/
var query = function(selector) \\{
  var reg = /^(#)?(\.)?(\w+)$/gim;
  var regResult = reg.exec(selector);
  var result = [];
  //如果是id选择器
  if (regResult[1]) \\{
    if (regResult[3]) \\{
      if (typeof document.querySelector === "function") \\{
        result.push(document.querySelector(regResult[3]));
      \\} else \\{
        result.push(document.getElementById(regResult[3]));
      \\}
    \\}
  \\} //如果是class选择器
  else if (regResult[2]) \\{
    if (regResult[3]) \\{
      if (typeof document.getElementsByClassName === "function") \\{
        var doms = document.getElementsByClassName(regResult[3]);
        if (doms) \\{
          result = converToArray(doms);
        \\}
      \\} //如果不支持getElementsByClassName函数
      else \\{
        var allDoms = document.getElementsByTagName("*");
        for (var i = 0, len = allDoms.length; i < len; i++) \\{
          if (allDoms[i].className.search(new RegExp(regResult[2])) > -1) \\{
            result.push(allDoms[i]);
          \\}
        \\}
      \\}
    \\}
  \\} //如果是标签选择器
  else if (regResult[3]) \\{
    var doms = document.getElementsByTagName(regResult[3].toLowerCase());
    if (doms) \\{
      result = converToArray(doms);
    \\}
  \\}
  return result;
\\};
function converToArray(nodes) \\{
  var array = null;
  try \\{
    array = Array.prototype.slice.call(nodes, 0); //针对非IE浏览器
  \\} catch (ex) \\{
    array = new Array();
    for (var i = 0, len = nodes.length; i < len; i++) \\{
      array.push(nodes[i]);
    \\}
  \\}
  return array;
\\}
```



### 下列控制台都输出什么

第 1 题：

```js
function setName() \\{
  name = "张三";
\\}
setName();
console.log(name);
```

答案："张三"

第 2 题：

```js
//考点：1、变量声明提升 2、变量搜索机制
var a = 1;
function test() \\{
  console.log(a);
  var a = 1;
\\}
test();
```

答案：undefined

第 3 题：

```js
var b = 2;
function test2() \\{
  window.b = 3;
  console.log(b);
\\}
test2();
```

答案：3

第 4 题：

```js
c = 5; //声明一个全局变量c
function test3() \\{
  window.c = 3;
  console.log(c); //答案：undefined，原因：由于此时的c是一个局部变量c，并且没有被赋值
  var c;
  console.log(window.c); //答案：3，原因：这里的c就是一个全局变量c
\\}
test3();
```

第 5 题：

```js
var arr = [];
arr[0] = "a";
arr[1] = "b";
arr[10] = "c";
alert(arr.length); //答案：11
console.log(arr[5]); //答案：undefined
```

第 6 题：

```js
var a = 1;
console.log(a++); //答案：1
console.log(++a); //答案：3
```

第 7 题：

```js
console.log(null == undefined); //答案：true
console.log("1" == 1); //答案：true，因为会将数字1先转换为字符串1
console.log("1" === 1); //答案：false，因为数据类型不一致
```

第 8 题：

```js
typeof 1;
("number");
typeof "hello";
("string");
typeof /[0-9]/;
("object");
typeof \\{\\};
("object");
typeof null;
("object");
typeof undefined;
("undefined");
typeof [1, 2, 3];
("object");
typeof function() \\{\\}; //"function"
```

第 9 题：

```js
parseInt(3.14); //3
parseFloat("3asdf"); //3
parseInt("1.23abc456");
parseInt(true); //"true" NaN
```

第 10 题：

```js
//考点：函数声明提前
function bar() \\{
  return foo;
  foo = 10;
  function foo() \\{\\}
  //var foo = 11;
\\}
alert(typeof bar()); //"function"
```

第 11 题：考点：函数声明提前

```js
var foo = 1;
function bar() \\{
  foo = 10;
  return;
  function foo() \\{\\}
\\}
bar();
alert(foo); //答案：1
```

第 12 题：

```js
console.log(a); //是一个函数
var a = 3;
function a() \\{\\}
console.log(a); ////3
```

第 13 题：

```js
//考点：对arguments的操作
function foo(a) \\{
    arguments[0] = 2;
    alert(a);//答案：2，因为：a、arguments是对实参的访问，b、通过arguments[i]可以修改指定实参的值
\\}
foo(1);
265、第14题：
function foo(a) \\{
    alert(arguments.length);//答案：3，因为arguments是对实参的访问
\\}
foo(1, 2, 3);
```

第 15 题

```js
bar(); //报错
var foo = function bar(name) \\{
  console.log("hello" + name);
  console.log(bar);
\\};
//alert(typeof bar);
foo("world"); //"hello"
console.log(bar); //undefined
console.log(foo.toString());
bar(); //报错
```



### 下面程序输出的结果是什么？

```
function sayHi() \\{
  console.log(name);
  console.log(age);
  var name = "Lydia";
  let age = 21;
\\}

sayHi();
A: Lydia 和 undefined
B: Lydia 和 ReferenceError
C: ReferenceError 和 21
D: undefined 和 ReferenceError
```

参考答案

在函数中，我们首先使用var关键字声明了name变量。 这意味着变量在创建阶段会被提升（JavaScript会在创建变量创建阶段为其分配内存空间），默认值为undefined，直到我们实际执行到使用该变量的行。 我们还没有为name变量赋值，所以它仍然保持undefined的值。

使用let关键字（和const）声明的变量也会存在变量提升，但与var不同，初始化没有被提升。 在我们声明（初始化）它们之前，它们是不可访问的。 这被称为“暂时死区”。 当我们在声明变量之前尝试访问变量时，JavaScript会抛出一个ReferenceError。

关于let的是否存在变量提升，我们何以用下面的例子来验证：

```
let name = 'ConardLi'
\\{
  console.log(name) // Uncaught ReferenceError: name is not defined
  let name = 'code秘密花园'
\\}
```


let变量如果不存在变量提升，console.log(name)就会输出ConardLi，结果却抛出了ReferenceError，那么这很好的说明了，let也存在变量提升，但是它存在一个“暂时死区”，在变量未初始化或赋值前不允许访问。

变量的赋值可以分为三个阶段：

创建变量，在内存中开辟空间
初始化变量，将变量初始化为undefined
真正赋值
关于let、var和function：

let的「创建」过程被提升了，但是初始化没有提升。
var的「创建」和「初始化」都被提升了。
function的「创建」「初始化」和「赋值」都被提升了。



### 下面代码输出什么

```
var a = 10;
(function () \\{
    console.log(a)
    a = 5
    console.log(window.a)
    var a = 20;
    console.log(a)
\\})()
```


依次输出：undefined -> 10 -> 20

在立即执行函数中，var a = 20; 语句定义了一个局部变量 a，由于js的变量声明提升机制，局部变量a的声明会被提升至立即执行函数的函数体最上方，且由于这样的提升并不包括赋值，因此第一条打印语句会打印undefined，最后一条语句会打印20。

由于变量声明提升，a = 5; 这条语句执行时，局部的变量a已经声明，因此它产生的效果是对局部的变量a赋值，此时window.a 依旧是最开始赋值的10，



### 下面的输出结果是什么？

```
class Chameleon \\{
  static colorChange(newColor) \\{
    this.newColor = newColor;
  \\}

  constructor(\\{ newColor = "green" \\} = \\{\\}) \\{
    this.newColor = newColor;
  \\}
\\}

const freddie = new Chameleon(\\{ newColor: "purple" \\});
freddie.colorChange("orange");
```


A: orange
B: purple
C: green
D: TypeError
答案: D

colorChange方法是静态的。 静态方法仅在创建它们的构造函数中存在，并且不能传递给任何子级。 由于freddie是一个子级对象，函数不会传递，所以在freddie实例上不存在freddie方法：抛出TypeError。



### 下面代码中什么时候会输出1？

```
var a = ?;
if(a == 1 && a == 2 && a == 3)\\{
     conso.log(1);
\\}
```

因为==会进行隐式类型转换 所以我们重写toString方法就可以了

```
var a = \\{
  i: 1,
  toString() \\{
    return a.i++;
  \\}
\\}

if( a == 1 && a == 2 && a == 3 ) \\{
  console.log(1);
\\}
```



### 下面的输出结果是什么？

```
var obj = \\{
    '2': 3,
    '3': 4,
    'length': 2,
    'splice': Array.prototype.splice,
    'push': Array.prototype.push
\\}
obj.push(1)
obj.push(2)
console.log(obj)
```


参考答案

1.使用第一次push，obj对象的push方法设置 obj[2]=1;obj.length+=1
2.使用第二次push，obj对象的push方法设置 obj[3]=2;obj.length+=1
3.使用console.log输出的时候，因为obj具有 length 属性和 splice 方法，故将其作为数组进行打印
4.打印时因为数组未设置下标为 0 1 处的值，故打印为empty，主动 obj[0] 获取为 undefined



### 下面代码输出的结果是什么？

```
var a = \\{n: 1\\};
var b = a;
a.x = a = \\{n: 2\\};

console.log(a.x)     
console.log(b.x)
```

参考答案

undefined
\\{n:2\\}

首先，a和b同时引用了\\{n:2\\}对象，接着执行到a.x = a = \\{n：2\\}语句，尽管赋值是从右到左的没错，但是.的优先级比=要高，所以这里首先执行a.x，相当于为a（或者b）所指向的\\{n:1\\}对象新增了一个属性x，即此时对象将变为\\{n:1;x:undefined\\}。之后按正常情况，从右到左进行赋值，此时执行a =\\{n:2\\}的时候，a的引用改变，指向了新对象\\{n：2\\},而b依然指向的是旧对象。之后执行a.x = \\{n：2\\}的时候，并不会重新解析一遍a，而是沿用最初解析a.x时候的a，也即旧对象，故此时旧对象的x的值为\\{n：2\\}，旧对象为 \\{n:1;x:\\{n：2}}，它被b引用着。
后面输出a.x的时候，又要解析a了，此时的a是指向新对象的a，而这个新对象是没有x属性的，故访问时输出undefined；而访问b.x的时候，将输出旧对象的x的值，即\\{n:2\\}。



### 下面代码的输出是什么?

```
function checkAge(data) \\{
  if (data === \\{ age: 18 \\}) \\{
    console.log("You are an adult!");
  \\} else if (data == \\{ age: 18 \\}) \\{
    console.log("You are still an adult.");
  \\} else \\{
    console.log(`Hmm.. You don't have an age I guess`);
  \\}
\\}

checkAge(\\{ age: 18 \\});
```

参考答案

Hmm.. You don't have an age I guess
在比较相等性，原始类型通过它们的值进行比较，而对象通过它们的引用进行比较。JavaScript检查对象是否具有对内存中相同位置的引用。

我们作为参数传递的对象和我们用于检查相等性的对象在内存中位于不同位置，所以它们的引用是不同的。

这就是为什么\\{ age: 18 \\} === \\{ age: 18 \\}和 \\{ age: 18 \\} == \\{ age: 18 \\}返回 false的原因。



### 下面代码的输出是什么?

```
const obj = \\{ 1: "a", 2: "b", 3: "c" \\};
const set = new Set([1, 2, 3, 4, 5]);

obj.hasOwnProperty("1");
obj.hasOwnProperty(1);
set.has("1");
set.has(1);
```


参考答案

true  true  false  true
所有对象键（不包括Symbols）都会被存储为字符串，即使你没有给定字符串类型的键。 这就是为什么obj.hasOwnProperty（'1'）也返回true。

上面的说法不适用于Set。 在我们的Set中没有“1”：set.has（'1'）返回false。 它有数字类型1，set.has（1）返回true。



### 下面代码的输出是什么?

```
// example 1
var a=\\{\\}, b='123', c=123;  
a[b]='b';
a[c]='c';  
console.log(a[b]);

// example 2
var a=\\{\\}, b=Symbol('123'), c=Symbol('123');  
a[b]='b';
a[c]='c';  
console.log(a[b]);

// example 3
var a=\\{\\}, b=\\{key:'123'\\}, c=\\{key:'456'\\};  
a[b]='b';
a[c]='c';  
console.log(a[b]);
```


参考答案

这题考察的是对象的键名的转换。

对象的键名只能是字符串和 Symbol 类型。
其他类型的键名会被转换成字符串类型。
对象转字符串默认会调用 toString 方法。

```
// example 1
var a=\\{\\}, b='123', c=123;
a[b]='b';
// c 的键名会被转换成字符串'123'，这里会把 b 覆盖掉。
a[c]='c';  
// 输出 c
console.log(a[b]);


// example 2
var a=\\{\\}, b=Symbol('123'), c=Symbol('123');  
// b 是 Symbol 类型，不需要转换。
a[b]='b';
// c 是 Symbol 类型，不需要转换。任何一个 Symbol 类型的值都是不相等的，所以不会覆盖掉 b。
a[c]='c';
// 输出 b
console.log(a[b]);

// example 3
var a=\\{\\}, b=\\{key:'123'\\}, c=\\{key:'456'\\};  
// b 不是字符串也不是 Symbol 类型，需要转换成字符串。
// 对象类型会调用 toString 方法转换成字符串 [object Object]。
a[b]='b';
// c 不是字符串也不是 Symbol 类型，需要转换成字符串。
// 对象类型会调用 toString 方法转换成字符串 [object Object]。这里会把 b 覆盖掉。
a[c]='c';  
// 输出 c
console.log(a[b]);
```



### 下面代码的输出是什么?

```
(() => \\{
  let x, y;
  try \\{
    throw new Error();
  \\} catch (x) \\{
    (x = 1), (y = 2);
    console.log(x);
  \\}
  console.log(x);
  console.log(y);
\\})();
```


参考答案

1  undefined  2
catch块接收参数x。当我们传递参数时，这与变量的x不同。这个变量x是属于catch作用域的。

之后，我们将这个块级作用域的变量设置为1，并设置变量y的值。 现在，我们打印块级作用域的变量x，它等于1。

在catch块之外，x仍然是undefined，而y是2。 当我们想在catch块之外的console.log(x)时，它返回undefined，而y返回2。



### 下面代码的输出结果是什么？

```
function Foo() \\{
    Foo.a = function() \\{
        console.log(1)
    \\}
    this.a = function() \\{
        console.log(2)
    \\}
\\}
Foo.prototype.a = function() \\{
    console.log(3)
\\}
Foo.a = function() \\{
    console.log(4)
\\}
Foo.a();
let obj = new Foo();
obj.a();
Foo.a();
```


参考答案

输出顺序是 4 2 1

```
function Foo() \\{
    Foo.a = function() \\{
        console.log(1)
    \\}
    this.a = function() \\{
        console.log(2)
    \\}
\\}
// 以上只是 Foo 的构建方法，没有产生实例，此刻也没有执行

Foo.prototype.a = function() \\{
    console.log(3)
\\}
// 现在在 Foo 上挂载了原型方法 a ，方法输出值为 3

Foo.a = function() \\{
    console.log(4)
\\}
// 现在在 Foo 上挂载了直接方法 a ，输出值为 4

Foo.a();
// 立刻执行了 Foo 上的 a 方法，也就是刚刚定义的，所以
// # 输出 4
```

原文链接：https://blog.csdn.net/sinat_37903468/article/details/100887223







### 笔试经验

**面试中的写代码的过程,一定不能紧张,要沉住气慢慢来**.只要不是系统自动检查结果,只要是面试官看着你写,就有很大的表现的机会,哪怕最后做不出来。

可以肯定的是,**面试官不会只根据是否能运行成功来评价应聘者**.

所以,**只需要顺着正确思路稳稳地做就好了,不要怕最后运行不成功**.

**如果实在做不出,也一定要和面试官说清你当前的进展和思路**,而不是一句"我不会"就想结束问题.

> 关于这篇文章,有几点我想先说清楚,方便读者更顺利的学习.
>
> - 这篇文章**不适合前端小白阅读**,需要对`JS`和`ES6`有一定了解,否则遇到一些写法可能不太看得懂
>
> - 因为精力有限,我只加了较为粗略但足以帮助读者理解的注释,因为多数题也只有几行代码而已.
>
> 如果遇到还**不懂的地方**,我认为读者完全可以**自己去查询文档来了解为什么这么做**,为什么使用这个函数.
>
> 或者,**先查询该问题通常的解决思路,再回来参考我的实现**
>
> - 代码**大量使用了`ES6`的语法**
>
> - 学习手撕代码,不只是理解的过程,更是**实践**的过程
>
> 我在完全掌握(可以默写出每段代码,并讲清楚每一行的作用)以下代码的过程中,做了以下几件事
>
> - - 参考别人的实现,结合自己的思路,写出一个自己的版本
>
>   - **不断对代码进行优化**
>
>  当你尝试去优化一段代码的时候,对它的理解和记忆会异常深刻
>
>   - 不看之前的实现,重新自己实现一次
>
>  再和之前的实现做对比,检查错误
>
>   - **反复阅读和默写**,直到可以完全正确的默写为之
>
> - **作为一个专业的程序员,除了工作中的编码,额外的无实际产出的练习(反复练习解决一个问题,反复默写同一段代码),也是必不可少的.**
>
> 这就像歌手不可能到了舞台上才去练习自己的声音.他一定会在平时大量去练声.
>
> 这就是我强调要反复敲代码的原因.别想着平时只要理解,工作中再去熟能生巧.
>
> **工作不是给你练习的地方,工作是你的舞台.**
>
> - 下文中几乎每一段代码,都是我反复优化后的结果,希望可以带给读者新的启发.
>
> - 我把代码大致分成了几个专题,一共包含了大致**30个问题的解决方案**
>
> - 除了文章中的问题,还有些**我没有提到的,都是频率较低的问题**
>
> 关于**算法题,除了排序和查找我也基本没有写**.因为算法问题千变万化,需要的是解决问题的思维,而不是固定的实现
>
> - 重要性与顺序无关
>

### 目录

#### DOM

- 事件代理

#### 数组 对象

- 扁平化

- 去重 - `unique()`

- 拷贝

- - 浅拷贝
  - 深拷贝（`copy()`函数实现、`JSON.stringify`）

#### 字符串

- 去除空格 - `trim()`

- 字符串全排列

- - 广度优先实现
  - 深度优先实现

#### 排序和查找

- 插入排序
- 归并排序
- 快速排序
- 二分查找
- 找出出现次数最多的元素 - `getMostItem()`

#### 功能函数实现

- `setTimeout`实现`setInterval`
- 函数柯里化
- 防抖 节流

#### 数据结构

- 单链表

#### 设计模式

- 发布订阅模式

#### JS原生API实现

- `bind()` `call()` `apply()`
- `InstanceOf`
- `new`
- `reduce()` `forEach()`
- `Promise`

#### HTTP请求

- AJAX封装
- JSONP

## DOM

### 事件代理

```
document.getElementById("father-id").onclick=function(event)\\{
    event=event||window.event
    let target=event.target||event.srcElement
    //可以自己打印一下event.target.nodeName,看看是什么
    if (target.nodeName.toLowerCase()==='xxx')\\{
        //事件内容
    \\}
\\}
```

## 数组 对象

### 扁平化

```
function flatten(arr) \\{
 let result=[]
 for (let i=0,len=arr.length;i<len;i++) \\{
  if (Array.isArray(arr[i])) \\{
   result=result.concat(flatten(arr[i]))
  \\} else \\{
   result.push(arr[i])
  \\}
 \\}
 return result
\\}
```

### 去重 - `unique()`

```
function unique(arr) \\{
    let appeard=new Set()
    return arr.filter(item=>\\{
        //创建一个可以唯一标识对象的字符串id
        let id=item+JSON.stringify(item)
        if (appeard.has(id)) \\{
            return false
        \\} else \\{
            appeard.add(id)
            return true
        \\}
    \\})
\\}
```

### 拷贝

#### 浅拷贝

```
function copy(obj) \\{
 let result=Array.isArray(obj)?[]:\\{\\}
 Object.keys(obj).forEach(key=>result[key]=obj[key])
 return result
\\}
otherStar=\\{...star\\}
Object.assign(\\{\\},star)
```

#### 深拷贝

##### `copy()`函数实现

处理了**循环引用**和**key为symbol类型的情况**

```
function copy(obj,appeard=new Map()) \\{
 if (!(obj instanceof Object)) return obj//如果是原始数据类型
    if (appeard.has(obj)) return appeard.get(obj)//如果已经出现过

    let result=Array.isArray(obj)?[]:\\{\\}
    appeard.set(obj,result)//将新对象放入map

    //遍历所有属性进行递归拷贝
    ;[...Object.keys(obj),...Object.getOwnPropertySymbols(obj)]
     .forEach(key=>result[key]=copy(obj[key],appeard))

    return result
\\}
```

##### `JSON.stringify`

- 只能处理纯JSON数据
- 有几种情况会发生错误
- 包含不能转成 JSON 格式的数据
- 循环引用
- undefined,NaN, -Infinity, Infinity 都会被转化成null
- **RegExp/函数**不会拷贝
- new Date()会被转成字符串

```
new=JSON.parse(JSON.stringify(old))
```

## 字符串

### 去除空格 - `trim()`

```
function myTrim(str) \\{
 return str.replace(/(^\s+)|(\s+$)/g,'')//将前空格和后空格替换为空
\\}
function myTrim(str) \\{//记录前后空格的个数,最后对字符串进行截取
 let first=0,last=str.length
 for (let i in str) \\{
  if (str[i]===' ') \\{
   first++
  \\} else \\{
   break
  \\}
 \\}
 for (let i=last;i>first;i--) \\{
  if (str[i]===' ') \\{
   last--
  \\} else \\{
   break
  \\}
 \\}
 return str.substr(first,last-first)
\\}
```

### 字符串全排列

#### 广度优先实现

```
function combine(str) \\{//抽出一个字符s,对其余的进行排列,将s放在每种排列开头
 if (str.length===1) return [str]
 let results=[]
 for (let i in str) \\{
  for (let s of combine(str.slice(0,i)+str.slice(1+(+i)))) \\{
   results.push(str[i]+s)
  \\}
 \\}
    //可能会出现类似"aa"=>[aa,aa,aa,aa]的情况,需要去重
 return [...new Set(results)]
\\}
```

#### 深度优先实现

```
function combine(str) \\{//记录已经使用过的字符,深度优先访问所有方案
 let result=[]
 ;(function _combine(str,path='')\\{
  if (str.length===0) return result.push(path)
  for (let i in str) \\{
   _combine(str.slice(0,i)+str.slice((+i)+1,str.length),path+str[i])
  \\}
 \\})(str)
    //可能会出现类似"aa"=>[aa,aa,aa,aa]的情况,需要去重
 return [...new Set(result)]
\\}
```

## 排序和查找

### 插入排序

```
function sort(arr) \\{//原地
 for (let i in arr) \\{//选一个元素
  while (i>0&&arr[i]<arr[i-1]) \\{//向前移动到合适的位置
   [arr[i],arr[i-1]]=[arr[i-1],arr[i]]
   i--
  \\}
 \\}
\\}
```

### 归并排序

```
function sort(arr) \\{
 if (arr.length===1) return arr

 //分成两部分
 let mid=Math.floor(arr.length/2)
 let [part1,part2]=[sort(arr.slice(0,mid)),sort(arr.slice(mid))]

 //对比+合并
 let result=[]
 while (part1.length>0&&part2.length>0)
  result.push((part1[0]<part2[0]?part1:part2).shift())
 return [...result,...part1,...part2]
\\}
```

### 快速排序

```
function sort(arr) \\{
 if (arr.length<=1) return arr

    //选基准值
 let mid_pos=arr.length>>1
 let mid=arr.splice(mid_pos,1)[0]

 let left=[],right=[]

    //和基准值比较,分别插入left,right数组
 arr.forEach(item=>(item<=mid?left:right).push(item))

 return [...sort(left),mid,...sort(right)]//递归调用排序
\\}
```

### 二分查找

```
function search(arr,target) \\{//循环写法,不断移动左右指针,缩小范围
 let left=0,right=arr.length-1

 while (left<=right) \\{
  const mid_pos=Math.floor((left+right)/2)
  const mid_val=arr[mid_pos]

  if (target===mid_val) \\{
   return mid_pos
  \\} else if (target>mid_val) \\{
   left=mid_pos+1
  \\} else \\{
   right=mid_pos-1
  \\}
 \\}
 return -1
\\}
```

### 找出出现次数最多的元素 - `getMostItem()`

```
function getMost(arr) \\{
 //计数
 let map=new Map()
 arr.forEach(item=>\\{
  if (map.has(item)) \\{
   map.set(item,map.get(item)+1)
  \\} else \\{
   map.set(item,1)
  \\}
 \\})

 //找出出现最多
 let [max_vals,max_num]=[[arr[0]],map.get(arr[0])]
 map.forEach((count,item)=>\\{
  if (count>max_num)\\{
   max_vals=[item]
   max_num=count
  \\} else \\{
   max_vals.push(item)
  \\} 
 \\})
 return max_vals
\\}

console.log(getMost(['1', '2', '3', '3', '55', '3', '55', '55']))
```

## 功能函数实现

### `setTimeout`实现`setInterval`

```
function myInterval(fn,interval,...args) \\{
 let context=this
 setTimeout(()=>\\{
  fn.apply(context,args)
  myInterval(fn,interval,...args)//别忘了为它传入参数
 \\},interval)
\\}


myInterval((num)=>console.log(num),500,10)
```

### 函数柯里化

```
function sum(...args1)\\{
    return function (...args2) \\{
        return [...args1,...args2].reduce((p,n)=>p+n)
    \\}
\\}
console.log(sum(1, 2, 2)(7))
```

### 防抖 节流

实现了两个**加工方法**,返回一个加工后的防抖/节流函数

#### 防抖

```
function debounce(fn,delay) \\{
 let timer=null
 return function ()\\{
  if (timer) clearTimeout(timer)
  timer=setTimeout(()=>fn.call(...arguments),delay)//别忘了为它传入参数
 \\}
\\}
```

#### 节流

```
function throttle(fn,delay) \\{
 let flag=true
 return function() \\{
  if (!flag) return

  flag=false
  setTimeout(()=>\\{
   fn(...arguments)//别忘了为它传入参数
   flag=true
  \\},delay)
 \\}
\\}
```

## 数据结构

### 单链表

```
function Node(element) \\{//结点类
 [this.element,this.next]=[element,null]
\\}

class LinkList \\{//链表类
 constructor() \\{
  this.length=0
  this.head=new Node()
  this.tail=new Node()
  this.head.next=this.tail
 \\}
 get_all() \\{
  let result=[]
  let now=this.head
  while (now.next!==this.tail) \\{
   now=now.next
   result.push(now.element)
  \\}
  return result
 \\}
 unshift(element) \\{//开头添加
  let node=new Node(element)
  node.next=this.head.next
  this.head.next=node
 \\}
 shift()\\{//开头删除
  let node=this.head.next
  this.head.next=this.head.next.next
  return node.element
 \\}
\\}
let list=new LinkList()
list.unshift(15)
list.unshift(16)
list.unshift(17)
console.log(list.shift())//17
console.log(list.get_all())//[ 16, 15 ]
```

## 设计模式

### 发布订阅模式

```
class Observer \\{
 constructor() \\{
  this.events=\\{\\}//事件中心
 \\}
 publish(eventName,...args) \\{//发布=>调用事件中心中对应的函数
  if (this.events[eventName])
   this.events[eventName].forEach(cb=>cb.apply(this,args))
 \\}
 subscribe(eventName,callback) \\{//订阅=>向事件中心中添加事件
  if (this.events[eventName]) \\{
   this.events[eventName].push(callback)
  \\} else \\{
   this.events[eventName]=[callback]
  \\}
 \\}
 unSubscribe(eventName,callback) \\{//取消订阅
  if (events[eventName])
   events[eventName]=events[eventName].filter(cb=>cb!==callback)
 \\}
\\}
```

## JS原生API实现

### `bind()` `call()` `apply()`

#### `apply()`

```
Function.prototype.myApply=function(context,args) \\{
 context.fn=this//为context设置函数属性
 let result=context.fn(...args)//调用函数
 delete context.fn//删除context的函数属性
 return result
\\}
```

#### `call()`

```
//除了...args
//和apply都一样
Function.prototype.myCall=function(context,...args) \\{
 context.fn=this
 let result=context.fn(...args)
 delete context.fn
 return result
\\}
```

#### `bind()`

```
Function.prototype.myBind=function(context,args1) \\{//使用[闭包+apply]实现
 return (...args2)=>this.apply(context,[...args1,...args2]);
\\}
```

### `InstanceOf`

```
function myInstanceOf(son,father) \\{//沿着父亲的原型链向上查找是否有儿子的原型
 while (true) \\{
  son=son.__proto__
  if (!son) return false
  if (son===father.prototype) return true
 \\}
\\}

myInstanceOf([], Array)  // true
```

### `new`

```
function myNew(constructor_fn,...args) \\{
 //构造新的空对象
 let new_obj=\\{\\}
 new_obj.__proto__=constructor_fn.prototype

 let result=constructor_fn.apply(new_obj,args)
 //如果构造函数没有返回一个对象,则返回新创建的对象
 //如果构造函数返回了一个对象,则返回那个对象
 //如果构造函数返回原始值,则当作没有返回对象
 return result instanceof Object?result:new_obj
\\}



function Animal(name) \\{
  this.name = name;
\\}

let animal = myNew(Animal, 'dog');
console.log(animal.name)  // dog
```

### `reduce()` `forEach()`

#### `reduce()`

api用法:

```
arr.reduce(function(prev, cur, index, arr)\\{\\}, initialValue)
```

实现:

```
Array.prototype.myReduce=function(fn,init_val)\\{
 let [val,idx]=init_val?[init_val,0]:[this[0],1]//设置初始值
 for (let i=idx,len=this.length;i<len;i++) \\{
  val=fn(val,this[i],i,this)//循环并迭代结果
 \\}
 return val
\\}

console.log([1,2,3,4,5].reduce((pre,item)=>pre+item,0)) // 15
```

#### `forEach()`

api用法:

```
[1,3,5,7,9].myForEach(function(item,index,arr) \\{
    console.log(this)
\\},15)
```

实现:

```
Array.prototype.myForEach=function(fn,temp_this) \\{
    for (let i=0,len=this.length;i<len;i++)\\{
        fn.call(temp_this,this[i],i,this)//循环数组元素,为回调函数传入参数
    \\}
\\}
```

### `Promise`

#### `Promise.all()`

```
Promise.prototype.all=function(promiseList) \\{
    return new Promise((resolve,reject)=>\\{
        if (promiseList.length===0) return resolve([])
        let result=[],count=0

        promiseList.forEach((promise,index)=>\\{
            Promise.resolve(promise).then(value=>\\{
                result[index]=value
                if (++count===promiseList.length) resolve(result)
            \\},reason=>reject(reason))
        \\})
    \\})
\\}
```

#### ES6所有API完整实现

通过Promise/A+ test测试

实现细节过多,还请参照Promise/A+规范阅读

也可以直接参考我关于promise的笔记

> 深入理解promise
>
> https://blog.csdn.net/weixin_43758603/article/details/109641486

```
class Promise \\{
 constructor(task) \\{
  this.status="pending"
  this.value=undefined
  this.reason=undefined
  this.fulfilled_callbacks=[]
  this.rejected_callbacks=[]

  try \\{
   task(this._resolve,this._reject)
  \\} catch (error) \\{
   this._reject(error)
  \\}
 \\}
 then(onFulfilled,onRejected)\\{
  if (this.status==='fulfilled') \\{
   let promise2=new Promise((resolve,reject)=>\\{
    setTimeout(()=>\\{
     try \\{
      if (!this._isFunction(onFulfilled)) \\{
       resolve(this.value)
      \\} else \\{
       this._resolvePromise(promise2,onFulfilled(this.value))
      \\}
     \\} catch (error) \\{
      reject(error)
     \\}
    \\},0)
   \\})
   return promise2
  \\} else if (this.status==='rejected') \\{
   let promise2=new Promise((resolve,reject)=>\\{
    setTimeout(()=>\\{
     try \\{
      if (!this._isFunction(onRejected)) \\{
       reject(this.reason)
      \\} else \\{
       this._resolvePromise(promise2,onRejected(this.reason))
      \\}
     \\} catch (error) \\{
      reject(error)
     \\}
    \\},0)
   \\})
   return promise2
  \\} else if (this.status==='pending')  \\{
   let promise2=new Promise((resolve,reject)=>\\{
    this.fulfilled_callbacks.push(()=>\\{
     try \\{
      if (!this._isFunction(onFulfilled)) \\{
       resolve(this.value)
      \\} else \\{
       this._resolvePromise(promise2,onFulfilled(this.value))
      \\}
     \\} catch (error) \\{
      reject(error)
     \\}
    \\})
    this.rejected_callbacks.push(()=>\\{
     try \\{
      if (!this._isFunction(onRejected)) \\{
       reject(this.reason)
      \\} else \\{
       this._resolvePromise(promise2,onRejected(this.reason))
      \\}
     \\} catch (error) \\{
      reject(error)
     \\}
    \\})
   \\})
   return promise2
  \\}
 \\}
 catch=onRejected=>this.then(null,onRejected)

 finally=onFinished=>this.then(onFinished,onFinished)

 static deferred()\\{
  let deferred=\\{\\}
  deferred.promise=new Promise((resolve,reject)=>\\{
   deferred.resolve=resolve
   deferred.reject=reject
  \\})
  return deferred
 \\}
 static resolve(value) \\{
  if (value instanceof Promise) return value
  return new Promise(resolve=>resolve(value))
 \\}
 static reject=reason=>\\{return new Promise((resolve, reject)=>reject(reason))\\}

 static all(promiseList) \\{
  return new Promise((resolve,reject)=>\\{
   if (promiseList.length===0) return resolve([])
   let result=[],count=0

   promiseList.forEach((promise,index)=>\\{
    Promise.resolve(promise).then(value=>\\{
     result[index]=value
     if (++count===promiseList.length) resolve(result)
    \\},reason=>reject(reason))
   \\})
  \\})
 \\}
 static race(promiseList) \\{
  return new Promise((resolve,reject)=>\\{
   if (promiseList.length===0) return resolve()
   promiseList.forEach(promise=>\\{
    Promise.resolve(promise)
     .then(value=>resolve(value),reason=>reject(reason))
   \\})
  \\})
 \\}
 static allSettled(promiseList) \\{
  return new Promise(resolve=>\\{
   let result=[],count=0
   if (len===0) return resolve(result)

   promiseList.forEach((promise,i)=>\\{
    Promise.resolve(promise).then(value=>\\{
     result[i]=\\{
      status:'fulfilled',
      value:value
     \\}
     if (++count===promiseList.length) resolve(result)
    \\},reason=>\\{
     result[i]=\\{
      status:'rejected',
      reason:reason
     \\}
     if (++count===promiseList.length) resolve(result)
    \\})
   \\})
  \\})
 \\}
 _resolve=value=>\\{
  if (this.status!=='pending') return
  setTimeout(()=>\\{
   this.status ='fulfilled'
   this.value = value
   this.fulfilled_callbacks.forEach(cb=>cb(this.value))
  \\},0)
 \\}
 _reject=reason=>\\{
  if (this.status!=='pending') return
  setTimeout(()=>\\{
   this.reason = reason
   this.status ='rejected'
   this.rejected_callbacks.forEach(cb=>cb(this.reason))
  \\},0)
 \\}
 _isFunction=f=>Object.prototype.toString.call(f).toLocaleLowerCase()==='[object function]'
 
 _isObject=o=>Object.prototype.toString.call(o).toLocaleLowerCase()==='[object object]'

 _resolvePromise(promise,x)\\{
  if (promise===x) \\{
      promise._reject(new TypeError('cant be the same'))
      return
  \\}
  if (x instanceof Promise) \\{
   if (x.status==='fulfilled') \\{
    promise._resolve(x.value)
   \\} else if (x.status==='rejected') \\{
    promise._reject(x.reason)
   \\} else if (x.status==='pending') \\{
    x.then(value=>\\{
     this._resolvePromise(promise,value)
    \\},reason=>\\{
     promise._reject(reason)
    \\})
   \\}
   return
  \\}
  if (this._isObject(x)||this._isFunction(x)) \\{
   let then
   try \\{
    then=x.then
   \\} catch (error) \\{
    promise._reject(error)
    return
   \\}
   if (this._isFunction(then)) \\{
    let called=false
    try \\{
     then.call(x,value=>\\{
      if (called) return
      called=true
      this._resolvePromise(promise,value)
     \\},reason=>\\{
      if (called) return
      called=true
      promise._reject(reason)
     \\})
    \\} catch (error) \\{
     if (called) return
     promise._reject(error)
    \\}
   \\} else \\{
    promise._resolve(x)
   \\}
  \\} else \\{
   promise._resolve(x)
  \\}
 \\}
\\}
module.exports = Promise
```

## HTTP请求

### AJAX封装

```
function ajax(method,url,params,callback) \\{
 //对参数进行处理
 method=method.toUpperCase()
 let post_params=null
 let get_params=''
 
 if (method==='GET') \\{
  if (typeof params==='object') \\{
   let tempArr=[]
   for (let key in params) \\{
    tempArr.push(`$\\{key\\}=$\\{params[key]\\}`)
   \\}
   params=tempArr.join('&')
  \\}
  get_params=`?$\\{params\\}`
 \\} else \\{
  post_params=params
 \\}

 //发请求
 let xhr=new XMLHttpRequest()

 xhr.onreadystatechange=function()\\{
  if (xhr.readyState!==4) return
  callback(xhr.responseText)
 \\}

 xhr.open(method,url+get_params,false)
 if (method==='POST')
  xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded')

 xhr.send(post_params) 
\\}

ajax('get','https://www.baidu.com',\\{id:15\\},data=>console.log(data))
```

### JSONP

```
function jsonp(url, params_obj, callback) \\{
 //创建一个供后端返回数据调用的函数名
 let funcName = 'jsonp_' + Data.now() + Math.random().toString().substr(2, 5)

 //将参数拼接成字符串
 if (typeof params==='object') \\{
  let temp=[]
  for (let key in params) \\{
   temp.push(`$\\{key\\}=$\\{params[key]\\}`)
  \\}
  params=temp.join('&')
 \\}

 //在html中插入<script>资源请求标签
 let script=document.createElement('script')
 script.src=`$\\{url\\}?$\\{params\\}&callback=$\\{funcName\\}`
 document.body.appendChild(script)

 //在本地设置供后端返回数据时调用的函数
 window[funcName]=data=>\\{
  callback(data)

  delete window[funcName]
  document.body.removeChild(script)
 \\}
\\}

//使用方法
jsonp('http://xxxxxxxx',\\{id:123\\},data=>\\{
 //获取数据后的操作
\\})
```

js插入html中标签的内容

```
<script src="https://www.liuzhuocheng.com?callback=funcName"></script>
```

后端返回的`<script>`资源的内容

```
<script src="https://www.liuzhuocheng.com?callback=funcName">
 funcName('datadatadatadatadatadatadatadata')
</script>
```



### 面试代码题解释

```
var a = 10;
(function () \\{
    console.log(a)
    a = 5
    console.log(window.a)
    var a = 20;
    console.log(a)
\\})()
```


这段代码的输出结果为：

- 第一个  console.log(a)  输出  10 ，因为在外部定义了变量  a  并赋值为  10 。
- 第二个  console.log(window.a)  输出  10 ，这里通过  window.a  访问全局变量  a ，其值仍为  10 。
- 第三个  console.log(a)  输出  20 ，这是在函数内部重新声明的局部变量  a  的值。

这段代码主要考察了以下几个方面：

- 作用域：展示了全局作用域和函数内部作用域的区别。
- 变量声明：不同位置声明变量的可见性和生命周期。

在函数内部重新声明了变量  a ，这会形成一个局部作用域，覆盖了外部的全局变量  a 。在函数内部对  a  进行赋值操作只会影响局部变量，而不会改变全局变量的值。



```
const p = Promise.resolve();
(async () => \\{
    await p;
    console.log('await end');
\\})();
p.then(() => \\{
    console.log('then 1');
\\}).then(() => \\{
    console.log('then 2');
\\});
```

好的，下面是一个更通俗易懂的解释：

首先， Promise.resolve()  创建了一个已经完成的 Promise 对象  p 。

然后，在  async  函数中使用  await p ，这意味着程序会在这里暂停，等待  p  完成。

由于  p  已经完成了，所以  await p  不会阻塞，会直接继续执行后面的代码，输出  await end 。

而  p.then()  里的回调函数，它们会在  p  完成后被调用。但在这个例子中，程序在  await p  后就已经继续执行了，不会再回到  then  里的回调函数。

所以，最后只会输出  await end 。



```
['2.1.2', '0.402.1', '3.20.1', '0.1.8', '5.1.2', '1.3.4.5']
```


你可以使用 JavaScript 的 sort() 方法对数组进行排序，以下是一个示例代码：

```
const arr = ['2.1.2', '0.402.1', '3.20.1', '0.1.8', '5.1.2', '1.3.4.5'];
arr.sort();
console.log(arr);
```


执行上面的代码后，将会对数组进行排序，并将排序后的结果输出到控制台。