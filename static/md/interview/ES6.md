---
title: ES6
date: 2020-08-13 11:42:39
categories: 
- 前端面试
tags:
- JavaScript
- ES6
---

# ES6（2015）

### ES6 中的一些新特性

ES6 即 ECMAScript 2015，是 JavaScript 的新一代标准。

- 块级作用域：使用 let 和 const 关键字声明块级作用域的变量和常量，避免变量污染和重复定义。
- 箭头函数：可以更简洁地定义函数，并且它的 this 值绑定在定义时的环境中，而不是执行时的环境。
- 模板字符串：可以方便地拼接字符串和变量，避免了繁琐的字符串拼接和转义。
- 解构赋值：可以方便地提取对象和数组中的值并赋值给变量，使得代码更加简洁易懂。
- Rest 参数：将函数参数作为数组来处理，避免了需要使用 arguments 对象的情况。
- Spread 操作符：可以将数组或对象展开成独立的元素，方便地进行数组合并、对象合并等操作。
- Class 类：更方便地定义对象和继承，使得面向对象编程更加规范和易懂。
- Promise 异步编程：可以更好地处理异步操作，避免了回调地狱的问题。
- Promise.all 方法：可以同时执行多个 Promise 对象，并在所有 Promise 对象都执行完毕后返回结果。
- 模块化：引入了模块化的概念，可以更好地组织和管理代码，避免了全局变量的污染。

如你想了解更多关于 ES6 的新特性，可点击web前端tips:ES6部分常用新特性介绍查看。



### 1. 类（class）

```bash
class Man \\{
  constructor(name) \\{
    this.name = '小豪';
  \\}
  console() \\{
    console.log(this.name);
  \\}
\\}
const man = new Man('小豪');
man.console(); // 小豪
```



### 2. 模块化(ES Module)

```bash
// 模块 A 导出一个方法
export const sub = (a, b) => a + b;
// 模块 B 导入使用
import \\{ sub \\} from './A';
console.log(sub(1, 2)); // 3
```



### 3. 箭头（Arrow）函数

```bash
const func = (a, b) => a + b;
func(1, 2); // 3
```



### 4. 函数参数默认值

```bash
function foo(age = 25,)\\{ // ...\\}
```



### 5. 模板字符串

```bash
const name = '小豪';
const str = `Your name is $\\{name\\}`;
```



### 6. 解构赋值

```bash
let a = 1, b= 2;
[a, b] = [b, a]; // a 2  b 1
```



### 7. 延展操作符

```bash
let a = [...'hello world']; // ["h", "e", "l", "l", "o", " ", "w", "o", "r", "l", "d"]
```



### 8. 对象属性简写

```bash
const name='小豪',
const obj = \\{ name \\};
```



### 9. Promise

```bash
Promise.resolve().then(() => \\{ console.log(2); \\});
console.log(1);
// 先打印 1 ，再打印 2
```



### 10. let和const

```bash
let name = '小豪'；
const arr = [];
```







# ES7（2016）

### 1. Array.prototype.includes()

```bash
[1].includes(1); // true
```



### 2. 指数操作符

```bash
2**10; // 1024
```







# ES8（2017）

### 1. async/await

异步终极解决方案

```bash
async getData()\\{
    const res = await api.getTableData(); // await 异步任务
    // do something    
\\}
```



### 2. Object.values()

```bash
Object.values(\\{a: 1, b: 2, c: 3\\}); // [1, 2, 3]
```



### 3. Object.entries()

```bash
Object.entries(\\{a: 1, b: 2, c: 3\\}); // [["a", 1], ["b", 2], ["c", 3]]
```



### 4. String padding

```bash
// padStart
'hello'.padStart(10); // "     hello"
// padEnd
'hello'.padEnd(10) "hello     "
```



### 5. 函数参数列表结尾允许逗号



### 6. Object.getOwnPropertyDescriptors()

> 获取一个对象的所有自身属性的描述符,如果没有任何自身属性，则返回空对象。



### 7. SharedArrayBuffer对象

> SharedArrayBuffer 对象用来表示一个通用的，固定长度的原始二进制数据缓冲区，

```bash
/**
 * 
 * @param \\{*\\} length 所创建的数组缓冲区的大小，以字节(byte)为单位。  
 * @returns \\{SharedArrayBuffer\\} 一个大小指定的新 SharedArrayBuffer 对象。其内容被初始化为 0。
 */
new SharedArrayBuffer(10)
```



### 8. Atomics对象

> Atomics 对象提供了一组静态方法用来对 SharedArrayBuffer 对象进行原子操作。







# ES9（2018）

### 1. 异步迭代

await可以和for...of循环一起使用，以串行的方式运行异步操作

```bash
async function process(array) \\{
  for await (let i of array) \\{
    // doSomething(i);
  \\}
\\}
```



### 2. Promise.finally()

```bash
Promise.resolve().then().catch(e => e).finally();
```



### 3. Rest/Spread 属性

```bash
const values = [1, 2, 3, 5, 6];
console.log( Math.max(...values) ); // 6
```



### 4. 正则表达式命名捕获组

```bash
const reg = /(?<year>[0-9]\\{4\\})-(?<month>[0-9]\\{2\\})-(?<day>[0-9]\\{2\\})/;
const match = reg.exec('2021-02-23');
```

![img](https://segmentfault.com/img/remote/1460000039272643)



### 5. 正则表达式反向断言

```bash
(?=p)、(?<=p)  p 前面(位置)、p 后面(位置)
(?!p)、(?<!p>) 除了 p 前面(位置)、除了 p 后面(位置)
(?<=w)
```

![img](https://segmentfault.com/img/remote/1460000039272644)

`(?

![img](https://segmentfault.com/img/remote/1460000039272648)



### 6. 正则表达式dotAll模式

> 正则表达式中点.匹配除回车外的任何单字符，标记s改变这种行为，允许行终止符的出现

```bash
/hello.world/.test('hello\nworld');  // false
```

![img](https://segmentfault.com/img/remote/1460000039272649)







# ES10（2019）

### 1. Array.flat()和Array.flatMap()

flat()

```bash
[1, 2, [3, 4]].flat(Infinity); // [1, 2, 3, 4]
```

flatMap()

```bash
[1, 2, 3, 4].flatMap(a => [a**2]); // [1, 4, 9, 16]
```



### 2. String.trimStart()和String.trimEnd()

去除字符串首尾空白字符



### 3. String.prototype.matchAll

> matchAll（）为所有匹配的匹配对象返回一个迭代器

```bash
const raw_arr = 'test1  test2  test3'.matchAll((/t(e)(st(\d?))/g));
const arr = [...raw_arr];
```

![img](https://segmentfault.com/img/remote/1460000039272646)



### 4. Symbol.prototype.description

> 只读属性，回 Symbol 对象的可选描述的字符串。

```bash
Symbol('description').description; // 'description'
```



### 5. Object.fromEntries()

> 返回一个给定对象自身可枚举属性的键值对数组

```bash
// 通过 Object.fromEntries， 可以将 Map 转化为 Object:
const map = new Map([ ['foo', 'bar'], ['baz', 42] ]);
console.log(Object.fromEntries(map)); // \\{ foo: "bar", baz: 42 \\}
```



### 6. 可选 Catch







# ES11（2020）

### 1. Nullish coalescing Operator(空值处理)

表达式在 ?? 的左侧 运算符求值为undefined或null，返回其右侧。

```bash
let user = \\{
    u1: 0,
    u2: false,
    u3: null,
    u4: undefined
    u5: '',
\\}
let u2 = user.u2 ?? '用户2'  // false
let u3 = user.u3 ?? '用户3'  // 用户3
let u4 = user.u4 ?? '用户4'  // 用户4
let u5 = user.u5 ?? '用户5'  // ''
```



### 2. Optional chaining（可选链）

?.用户检测不确定的中间节点

```bash
let user = \\{\\}
let u1 = user.childer.name // TypeError: Cannot read property 'name' of undefined
let u1 = user.childer?.name // undefined
```



### 3. Promise.allSettled

> 返回一个在所有给定的promise已被决议或被拒绝后决议的promise，并带有一个对象数组，每个对象表示对应的promise结果

```bash
const promise1 = Promise.resolve(3);
const promise2 = 42;
const promise3 = new Promise((resolve, reject) => reject('我是失败的Promise_1'));
const promise4 = new Promise((resolve, reject) => reject('我是失败的Promise_2'));
const promiseList = [promise1,promise2,promise3, promise4]
Promise.allSettled(promiseList)
.then(values=>\\{
  console.log(values)
\\});
```

![img](https://segmentfault.com/img/remote/1460000039272647)



### 4. import()

按需导入



### 5. 新基本数据类型BigInt

> 任意精度的整数



### 6. globalThis

- 浏览器：window
- worker：self
- node：global







# ES12（2021）

### 1. replaceAll

> 返回一个全新的字符串，所有符合匹配规则的字符都将被替换掉

```bash
const str = 'hello world';
str.replaceAll('l', ''); // "heo word"
```



### 2. Promise.any

> Promise.any() 接收一个Promise可迭代对象，只要其中的一个 promise 成功，就返回那个已经成功的 promise 。如果可迭代对象中没有一个 promise 成功（即所有的 promises 都失败/拒绝），就返回一个失败的 promise

```bash
const promise1 = new Promise((resolve, reject) => reject('我是失败的Promise_1'));
const promise2 = new Promise((resolve, reject) => reject('我是失败的Promise_2'));
const promiseList = [promise1, promise2];
Promise.any(promiseList)
.then(values=>\\{
  console.log(values);
\\})
.catch(e=>\\{
  console.log(e);
\\});
```

![img](https://segmentfault.com/img/remote/1460000039272645)



### 3. WeakRefs

> 使用WeakRefs的Class类创建对对象的弱引用(对对象的弱引用是指当该对象应该被GC回收时不会阻止GC的回收行为)



### 4. 逻辑运算符和赋值表达式

> 逻辑运算符和赋值表达式，新特性结合了逻辑运算符（&&，||，??）和赋值表达式而JavaScript已存在的 复合赋值运算符有：

```bash
a ||= b
//等价于
a = a || (a = b)

a &&= b
//等价于
a = a && (a = b)

a ??= b
//等价于
a = a ?? (a = b)
```



### 5. 数字分隔符

> 数字分隔符，可以在数字之间创建可视化分隔符，通过_下划线来分割数字，使数字更具可读性

```bash
const money = 1_000_000_000;
//等价于
const money = 1000000000;

1_000_000_000 === 1000000000; // true
```

![img](https://segmentfault.com/img/remote/1460000039272650)

以上内容来自https://segmentfault.com/a/1190000039272641



### 箭头函数

一、ES6标准新增加了一种新的匿名函数定义方法:箭头函数(Arrow Function)。箭头函数并没有替代以前定义匿名函数的方法，只是新增的一种定义匿名函数的方式！

```
// 正常函数
function name(形参列表)\\{代码块\\}

// ES6之前的匿名函数
function(形参列表)\\{代码块\\}
function(x,y)\\{return x+y\\}

// ES6新特性箭头函数
(形参列表)=>\\{代码块\\}
x => x+1 ; // 只有一个形参省略括号
x => (\\{foo: x\\}); // 返回对象字面量表达式
(x,y) => x+y;
(x,y) => \\{return x+y\\}
```


二、箭头函数没有定义this绑定。

箭头函数最大的好处是解决了匿名函数的this指向问题，有利于封装回调函数。箭头函数体内的this对象，就是定义该函数时所在的作用域指向的对象，而不是使用时所在的作用域指向的对象。（简述：箭头函数的this是继承所在作用域的this）。

```
var obj = \\{
  msg: "你好",
  fn1: function () \\{
    //  你好
    console.log(this.msg);
    // undefined （this指向该当前对象）
    setTimeout(function () \\{
      console.log(this.msg);
    \\}, 500);
    // 你好 （this指向定义该箭头函数时所在的作用域）
    setTimeout(() => \\{
      console.log(this.msg);
    \\}, 500);
  \\},
  fn2: () => \\{
    // undefined （this指向window）
    console.log(this.msg);
  \\},
\\};
```


三、箭头函数不绑定Arguments 对象，不能用作构造器，没有prototype属性，yield关键字通常不能在箭头函数中使用。

```
var fn1 = function (x) \\{
  // arguments数组
  console.log(arguments);
\\};
var fn2 = (x) => \\{
  // ReferenceError
  console.log(arguments);
\\};
fn2.prototype; // undefined
let fn3 = new fn2(); // ReferenceError
```


四、其他

```
// 三元运算
var simple = a => a > 10 ? 15 : a;
simple(18); // 15
simple(8); // 8

// 递归
var mult = (x) => ( x==0 ?  1 : x*mult(x-1) );
mult(5); // 120

// 标准的闭包函数
function fn1() \\{
  var i = 0;
  return function fn2() \\{ return ++i; \\};
\\}
fn1()(); // 1
var v = fn1();
v(); //1 
v(); //2

//箭头函数体的闭包（ i=0 是默认参数）
var Add = (i = 0) => \\{
  return () => ++i;
\\};
//因为仅有一个返回，return 及括号（）也可以省略
var Add = (i = 0) => () => ++i;

var q = Add ();
q(); //1 
q(); //2

// 箭头函数内定义的变量及其作用域

// 常规写法 函数体内var let定义的变量是局部变量
var whatTime = () => \\{
  let now = new Date();
  // var now = new Date();
  return now.getHours() > 17 ? "晚上好" : "日安";
\\};
whatTime(); // "晚上好"
console.log(now); // ReferenceError: now is not defined

// 参数括号内定义的变量是局部变量（默认参数）
var whatTime = (now = new Date()) => (now.getHours() > 17 ? "晚上好" : "日安");
whatTime(); // "晚上好"
console.log(now); // ReferenceError: now is not defined

// 对比：函数体内\\{\\}不使用var定义的变量是全局变量
var whatTime = () => \\{
  now = new Date();
  return now.getHours() > 17 ? "晚上好" : "日安";
\\};
whatTime(); // "晚上好"
console.log(now); // Thu Oct 14 2021 18:21:21 GMT+0800 (中国标准时间)
```

原文链接：https://blog.csdn.net/lusy258/article/details/120767707



### ES5、ES6和ES2015有什么区别?

> `ES2015`特指在`2015`年发布的新一代`JS`语言标准，`ES6`泛指下一代JS语言标准，包含`ES2015`、`ES2016`、`ES2017`、`ES2018`等。现阶段在绝大部分场景下，`ES2015`默认等同`ES6`。`ES5`泛指上一代语言标准。`ES2015`可以理解为`ES5`和`ES6`的时间分界线



### ES6的了解

es6 是一个新的标准，它包含了许多新的语言特性和库，是 JS 最实质性的一次升级。
比如'箭头函数'、'字符串模板'、'generators(生成器)'、'async/await'、'解构赋值'、'class'等等，还有就是引入 module 模块的概念。

- 增加了块级作用域。let命令实际上就增加了块级作用域。ES6规定，var命令和function命令声明的全局变量，属于全局对象的属性；let命令、const命令、class命令声明的全局变量，不属于全局对象的属性。

  块级作用域let a = 1;`可定义常量 `const PI = 3.141592654;`

- ES6将promise对象纳入规范，提供了原生的Promise对象。增加了let和const命令，用来声明变量。

  ` var promise = new Promise(func);`

- 箭头函数（操作符左边为输入的参数，而右边则是进行的操作以及返回的值Inputs=>outputs。）
- 新增模板字符串（为JavaScript提供了简单的字符串插值功能，字符串的扩展） ` var sum = `$\\{a + b\\}`;`
- arguments对象可被不定参数和默认参数完美代替。
- ES6新的语法糖，类，module模块化等新特性

解析：[参考](https://www.cnblogs.com/heweijain/p/7073553.html)



### 谈一谈你了解ECMAScript6的新特性？

* 变量解构赋值              `var [a, b, c] = [1, 2, 3];`
* 数组的扩展(转换数组类型)   `Array.from($('li'));`
* 函数的扩展(扩展运算符)     `[1, 2].push(...[3, 4, 5]);`
* 对象的扩展(同值相等算法)   ` Object.is(NaN, NaN);`
* 新增数据类型(Symbol)      `let uid = Symbol('uid');`
* 新增数据结构(Map)        ` let set = new Set([1, 2, 2, 3]);`
* for...of循环（用来遍历数据—例如数组中的值。）            `for(let val of arr)\\{\\};`
* Promise对象        
* Generator函数          ` function* foo(x)\\{yield x; return x*x;\\}`
* 引入Class(类)          ` class Foo \\{\\}`
* 引入模块体系            ` export default func;`
* 引入async函数[ES7]    

```js
async function asyncPrint(value, ms) \\{
      await timeout(ms);
      console.log(value)
     \\}
```



### 日常前端代码开发中，有哪些值得用ES6去改进的编程优化或者规范？

- 常用箭头函数来取代`var self = this`;的做法。
- 常用`let`取代`var`命令。
- 常用数组/对象的结构赋值来命名变量，结构更清晰，语义更明确，可读性更好。
- 在长字符串多变量组合场合，用模板字符串来取代字符串累加，能取得更好地效果和阅读体验。
- 用`Class`类取代传统的构造函数，来生成实例化对象。
- 在大型应用开发中，要保持`module`模块化开发思维，分清模块之间的关系，常用`import`、`export`方法。



### var、let、const 的区别

- var 定义的变量，没有块的概念，可以跨块访问, 不能跨函数访问。
- let 定义的变量，只能在块作用域里访问，不能跨块访问，也不能跨函数访问。（通常配合 `for` 循环或者 `\\{\\}` 进行使用产生块级作用域）
- const 用来定义常量，使用时必须初始化(即必须赋值)，只能在块作用域里访问，而且不能修改（内存地址不变）。
- 同一个变量只能使用一种方式声明，不然会报错

[参考链接](http://es6.ruanyifeng.com/#docs/let)



### let有什么用，有了var为什么还要用let？

> 在`ES6`之前，声明变量只能用`var`，`var`方式声明变量其实是很不合理的，准确的说，是因为`ES5`里面没有块级作用域是很不合理的。没有块级作用域回来带很多难以理解的问题，比如`for`循环`var`变量泄露，变量覆盖等问题。`let`声明的变量拥有自己的块级作用域，且修复了`var`声明变量带来的变量提升问题。

```js
<script type="text/javascript">
	// 块作用域
	\\{
		var a = 1;
		let b = 2;
		const c = 3;
		// c = 4; // 报错

		// let a = 'a';	// 报错  注：是上面 var a = 1; 那行报错
		// var b = 'b';	// 报错：本行报错
		// const a = 'a1';	// 报错  注：是上面 var a = 1; 那行报错
		// let c = 'c';	// 报错：本行报错

		var aa;
		let bb;
		// const cc; // 报错
		console.log(a); // 1
		console.log(b); // 2
		console.log(c); // 3
		console.log(aa); // undefined
		console.log(bb); // undefined
	\\}
	console.log(a); // 1
	// console.log(b); // 报错
	// console.log(c); // 报错

	// 函数作用域
	(function A() \\{
		var d = 5;
		let e = 6;
		const f = 7;
		console.log(d); // 5
		console.log(e); // 6  (在同一个\\{ \\}中,也属于同一个块，可以正常访问到)
		console.log(f); // 7  (在同一个\\{ \\}中,也属于同一个块，可以正常访问到)
	\\})();
	// console.log(d); // 报错
	// console.log(e); // 报错
	// console.log(f); // 报错
</script>
```



###  JS 块级作用域、变量提升

**块级作用域**

JS 中作用域有：全局作用域、函数作用域。没有块作用域的概念。ECMAScript 6(简称 ES6)中新增了块级作用域。块作用域由 \\{ \\} 包括，if 语句和 for 语句里面的\\{ \\}也属于块作用域。

**变量提升**

- 如果变量声明在函数里面，则将变量声明提升到函数的开头
- 如果变量声明是一个全局变量，则将变量声明提升到全局作用域的开头

解析：

```js
<script type="text/javascript">
	\\{
		var a = 1;
		console.log(a); // 1
	\\}
	console.log(a); // 1
	// 可见，通过var定义的变量可以跨块作用域访问到。

	(function A() \\{
		var b = 2;
		console.log(b); // 2
	\\})();
	// console.log(b); // 报错，
	// 可见，通过var定义的变量不能跨函数作用域访问到

	if(true) \\{
		var c = 3;
	\\}
	console.log(c); // 3
	for(var i = 0; i < 4; i++) \\{
		var d = 5;
	\\};
	console.log(i);	// 4   (循环结束i已经是4，所以此处i为4)
	console.log(d); // 5
	// if语句和for语句中用var定义的变量可以在外面访问到，
	// 可见，if语句和for语句属于块作用域，不属于函数作用域。

	\\{
		var a = 1;
		let b = 2;
		const c = 3;

		\\{
			console.log(a);		// 1	子作用域可以访问到父作用域的变量
			console.log(b);		// 2	子作用域可以访问到父作用域的变量
			console.log(c);		// 3	子作用域可以访问到父作用域的变量

			var aa = 11;
			let bb = 22;
			const cc = 33;
		\\}

		console.log(aa);	// 11	// 可以跨块访问到子 块作用域 的变量
		// console.log(bb);	// 报错	bb is not defined
		// console.log(cc);	// 报错	cc is not defined
	\\}
</script>
```



### var let 在 for 循环中的区别

解析：[参考](https://blog.csdn.net/zoelinjf/article/details/79618688)



### 如何避免回调函数嵌套？

使用 Promises 将回调写成单独的函数



### Promise是什么，有什么作用？

> 这里你谈 `promise`的时候，除了将他解决的痛点以及常用的 `API` 之外，最好进行拓展把 `eventloop` 带进来好好讲一下，`microtask`(微任务)、`macrotask`(任务) 的执行顺序；
>
> 如果看过 `promise` 源码，最好可以谈一谈 原生 `Promise` 是如何实现的。`Promise` 的关键点在于`callback` 的两个参数，一个是 `resovle`，一个是 `reject`。还有就是 `Promise` 的链式调用（`Promise.then()`，每一个 `then` 都是一个责任人）

`Promise`是`ES6`引入的一个新的对象，他的主要作用是用来**解决JS异步机制里，回调机制产生的“回调地狱”。**从语法上说，Promise 是一个对象，从它可以获取异步操作的消息。它并不是什么突破性的`API`，只是**封装了异步回调形式，使得异步回调可以写的更加优雅，可读性更高，而且可以链式调用。**

Promise 是异步编程的一种解决方案，比传统的解决方案——回调函数和事件监听——更合理和更强大。简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。Promise 提供统一的 API，各种异步操作都可以用同样的方法进行处理。

- Promise 就是一个对象，用来表示并传递异步操作的最终结果
- Promise 最主要的交互方式：将回调函数传入 then 方法来获得最终结果或出错原因
- Promise 代码书写上的表现：以“链式调用”代替回调函数层层嵌套（回调地狱）

**有两个特点:**

1. 对象的状态不受外界影响，Promise 对象代表一个异步操作，有三种状态：Pending（进行中）、Resolved（已完成，又称 Fulfilled）和 Rejected（已失败）
2. 一旦状态改变，就不会再变，任何时候都可以得到这个结果。

依照 Promise/A+ 的定义，Promise 有四种状态：

- pending: 初始状态, 非 fulfilled 或 rejected.

- fulfilled: 成功的操作.

- rejected: 失败的操作.

- settled: Promise已被fulfilled或rejected，且不是pending

另外， fulfilled 与 rejected 一起合称 settled

Promise 对象用来进行延迟(deferred) 和异步(asynchronous ) 计算

解析：[参考](https://www.cnblogs.com/heweijain/p/7073553.html)、[参考链接](http://es6.ruanyifeng.com/#docs/promise)



### Promise 的构造函数

构造一个 Promise，最基本的用法如下：

```js
var promise = new Promise(function(resolve, reject) \\{
        if (...) \\{  // succeed
            resolve(result);
        \\} else \\{   // fails
            reject(Error(errMessage));
        \\}
    \\});
```

Promise 实例拥有 then 方法（具有 then 方法的对象，通常被称为thenable）。它的使用方法如下：

```
promise.then(onFulfilled, onRejected)
```

接收两个函数作为参数，一个在 fulfilled 的时候被调用，一个在rejected的时候被调用，接收参数就是 future，onFulfilled 对应 resolve, onRejected 对应 reject



### async函数是什么，有什么作用？

`async`函数可以理解为**内置自动执行器的`Generator`函数语法糖**，它配合`ES6`的`Promise`近乎完美的实现了异步编程解决方案。



### async、await

async/await 是写异步代码的新方式，以前的方法有回调函数和 Promise。

async/await 是基于 Promise 实现的，它不能用于普通的回调函数。async/await 与 Promise 一样，是非阻塞的。

async/await 使得异步代码看起来像同步代码，这正是它的魔力所在。

> `Generator` 函数的语法糖。有更好的语义、更好的适用性、返回值是 `Promise`。

- `async => *`
- `await => yield`

```js
// 基本用法

async function timeout (ms) \\{
  await new Promise((resolve) => \\{
    setTimeout(resolve, ms)    
  \\})
\\}
async function asyncConsole (value, ms) \\{
  await timeout(ms)
  console.log(value)
\\}
asyncConsole('hello async and await', 1000)
```

> 注：最好把2，3，4 连到一起讲



### 箭头函数和普通函数有什么区别

箭头函数可以让 this 指向固定化，这种特性很有利于封装回调函数

- 函数体内的`this`对象，就是定义时所在的对象，而不是使用时所在的对象，用`call` `apply` `bind`也不能改变`this`指向
- 不可以当作构造函数，也就是说，不可以使用`new`命令，否则会抛出一个错误。
- 不可以使用`arguments`对象，该对象在函数体内不存在。如果要用，可以用 `rest` 参数代替。
- 不可以使用`yield`命令，因此箭头函数不能用作 `Generator` 函数。
- 箭头函数没有原型对象`prototype`

第一点尤其值得注意。this 对象的指向是可变的，但是在箭头函数中，它是固定的。

```js
function foo() \\{
  setTimeout(() => \\{
    console.log("id:", this.id);
  \\}, 100);
\\}

var id = 21;

foo.call(\\{ id: 42 \\});
// id: 42
```

解析：[参考](https://www.jianshu.com/p/bc28e4f67ef9)



### 举一些ES6对Function函数类型做的常用升级优化?

**优化部分**

> 箭头函数(核心)。箭头函数是ES6核心的升级项之一，箭头函数里**没有自己的this**,这改变了以往JS函数中最让人难以理解的this运行机制。主要优化点

- 箭头函数内的this指向的是**函数定义时所在的对象**，而不是函数执行时所在的对象。ES5函数里的this总是指向函数执行时所在的对象，这使得在很多情况下`this`的指向变得很难理解，尤其是非严格模式情况下，`this`有时候会指向全局对象，这甚至也可以归结为语言层面的bug之一。ES6的箭头函数优化了这一点，**它的内部没有自己的`this`,这也就导致了`this`总是指向上一层的`this`，如果上一层还是箭头函数，则继续向上指，直到指向到有自己`this`的函数为止，并作为自己的`this`**
- 箭头函数不能用作构造函数，因为它没有自己的`this`，无法实例化
- 也是因为箭头函数没有自己的this,所以箭头函数 内也不存在`arguments`对象。（可以用扩展运算符代替）
- 函数默认赋值。`ES6`之前，函数的形参是无法给默认值得，只能在函数内部通过变通方法实现。`ES6`以更简洁更明确的方式进行函数默认赋值

```js
function es6Fuc (x, y = 'default') \\{
    console.log(x, y);
\\}
es6Fuc(4) // 4, default
```

**升级部分**

> ES6新增了双冒号运算符，用来取代以往的`bind`，`call`,和`apply`。(浏览器暂不支持，`Babel`已经支持转码)

```js
foo::bar;
// 等同于
bar.bind(foo);

foo::bar(...arguments);
// 等同于
bar.apply(foo, arguments);
```



### 模板字符串

就是这种形式$\\{varible\\},在以往的时候我们在连接字符串和变量的时候需要使用这种方式'string' + varible + 'string'但是有了模版语言后我们可以使用string$\\{varible\\}string 这种进行连接。基本用途有如下：

1、基本的字符串格式化，将表达式嵌入字符串中进行拼接，用\$\\{\\}来界定。

```js
//es5
var name = "lux";
console.log("hello" + name);
//es6
const name = "lux";
console.log(`hello $\\{name\\}`); //hello lux
```

2、在 ES5 时我们通过反斜杠(\)来做多行字符串或者字符串一行行拼接，ES6 反引号(``)直接搞定。

```js
//ES5
var template =
  "hello \
world";
console.log(template); //hello world

//ES6
const template = `hello
world`;
console.log(template); //hello 空行 world
```



### module、export、import是什么，有什么作用？

- `module`、`export`、`import`是`ES6`用来统一前端模块化方案的设计思路和实现方案。`export`、`import`的出现统一了前端模块化的实现方案，整合规范了浏览器/服务端的模块化方法，用来取代传统的`AMD/CMD`、`requireJS`、`seaJS`、`commondJS`等等一系列前端模块不同的实现方案，使前端模块化更加统一规范，`JS`也能更加能实现大型的应用程序开发。
- `import`引入的模块是静态加载（编译阶段加载）而不是动态加载（运行时加载）。
- `import`引入`export`导出的接口值是动态绑定关系，即通过该接口，可以取到模块内部实时的值



### ES6 如何动态加载 import

```js
import("lodash").then(_ => \\{
  // Do something with lodash (a.k.a '_')...
\\});
```

解析：[参考](https://webpack.js.org/api/module-methods/#import)



### 什么是 Babel 

`babel`是一个 `ES6` 转码器，可以将 `ES6` 代码转为 `ES5` 代码，以便兼容那些还没支持`ES6`的平台

* Babel 是一个 JS 编译器，自带一组 ES6 语法转化器，用于转化 JS 代码。
  这些转化器让开发者提前使用最新的 JS语法(ES6/ES7)，而不用等浏览器全部兼容。
* Babel 默认只转换新的 JS 句法(syntax)，而不转换新的API。



### Object.is() 与原来的比较操作符“ ===”、“ ==”的区别？

- == 相等运算符，比较时会自动进行数据类型转换

- === 严格相等运算符，比较时不进行隐式类型转换（类型不同则会返回false）；

- Object.is 在三等号判等的基础上特别处理了 NaN 、-0 和 +0 ，保证 -0 和 +0 不再相同，但 Object.is(NaN, NaN) 会返回 true

  ```
  //Object.is 同值相等算法，在 === 基础上对 0 和 NaN 特别处理
  +0 === -0 //true
  NaN === NaN // false
  
  Object.is(+0, -0) // false
  Object.is(NaN, NaN) // true
  ```

- Object.is 应被认为有其特殊的用途，而不能用它认为它比其它的相等对比更宽松或严格。









### for...in 和for...of有什么区别？

> 如果看到问题十六，那么就很好回答。问题十六提到了ES6统一了遍历标准，制定了可遍历对象，那么用什么方法去遍历呢？答案就是用`for...of`。ES6规定，有所部署了载了`Iterator`接口的对象(可遍历对象)都可以通过`for...of`去遍历，而`for..in`仅仅可以遍历对象

这也就意味着，数组也可以用`for...of`遍历，这极大地方便了数组的取值，且避免了很多程序用`for..in`去遍历数组的恶习



### Symbol是什么，有什么作用？

> `Symbol`是`ES6`引入的第七种原始数据类型（说法不准确，应该是第七种数据类型，Object不是原始数据类型之一，已更正），所有Symbol()生成的值都是独一无二的，可以从根本上解决对象属性太多导致属性名冲突覆盖的问题。对象中`Symbol()`属性不能被`for...in`遍历，但是也不是私有属性



### Set是什么，有什么作用？

> `Set`是`ES6`引入的一种类似`Array`的新的数据结构，`Set`实例的成员类似于数组`item`成员。
>
> 区别是`Set`实例的成员都是唯一，不重复的。这个特性可以轻松地实现数组去重

**Set 数据结构**

- es6 方法,Set 本身是一个构造函数，它类似于数组，但是成员值都是唯一的。

```js
const set = new Set([1, 2, 3, 4, 4]);
console.log([...set]); // [1,2,3,4]
console.log(Array.from(new Set([2, 3, 3, 5, 6]))); //[2,3,5,6]
```



### Map是什么，有什么作用？

> `Map`是`ES6`引入的一种类似`Object`的新的数据结构，`Map`可以理解为是`Object`的超集，打破了以传统键值对形式定义对象，对象的`key`不再局限于字符串，也可以是`Object`。可以更加全面的描述对象的属性



### Proxy是什么，有什么作用？

> `Proxy`是`ES6`新增的一个构造函数，可以理解为JS语言的一个代理，用来改变JS默认的一些语言行为，包括拦截默认的`get/set`等底层方法，使得JS的使用自由度更高，可以最大限度的满足开发者的需求。比如通过拦截对象的`get/set`方法，可以轻松地定制自己想要的`key`或者`value`。下面的例子可以看到，随便定义一个`myOwnObj`的`key`,都可以变成自己想要的函数`

```js
function createMyOwnObj() \\{
	//想把所有的key都变成函数，或者Promise,或者anything
	return new Proxy(\\{\\}, \\{
		get(target, propKey, receiver) \\{
			return new Promise((resolve, reject) => \\{
				setTimeout(() => \\{
					let randomBoolean = Math.random() > 0.5;
					let Message;
					if (randomBoolean) \\{
						Message = `你的$\\{propKey\\}运气不错，成功了`;
						resolve(Message);
					\\} else \\{
						Message = `你的$\\{propKey\\}运气不行，失败了`;
						reject(Message);
					\\}
				\\}, 1000);
			\\});
		\\}
	\\});
\\}

let myOwnObj = createMyOwnObj();

myOwnObj.hahaha.then(result => \\{
	console.log(result) //你的hahaha运气不错，成功了
\\}).catch(error => \\{
	console.log(error) //你的hahaha运气不行，失败了
\\})

myOwnObj.wuwuwu.then(result => \\{
	console.log(result) //你的wuwuwu运气不错，成功了
\\}).catch(error => \\{
	console.log(error) //你的wuwuwu运气不行，失败了
\\})
```



### Reflect是什么，有什么作用？

> `Reflect`是`ES6`引入的一个新的对象，他的主要作用有两点，一是将原生的一些零散分布在`Object`、`Function`或者全局函数里的方法(如`apply`、`delete`、`get`、`set`等等)，统一整合到`Reflect`上，这样可以更加方便更加统一的管理一些原生`API`。其次就是因为`Proxy`可以改写默认的原生API，如果一旦原生`API`别改写可能就找不到了，所以`Reflect`也可以起到备份原生API的作用，使得即使原生`API`被改写了之后，也可以在被改写之后的`API`用上默认的`API`



### 举一些ES6对String字符串类型做的常用升级优化?

**优化部分**

> `ES6`新增了字符串模板，在拼接大段字符串时，用反斜杠`(`)`取代以往的字符串相加的形式，能保留所有空格和换行，使得字符串拼接看起来更加直观，更加优雅

**升级部分**

> `ES6`在`String`原型上新增了`includes()`方法，用于取代传统的只能用`indexOf`查找包含字符的方法(`indexOf`返回`-1`表示没查到不如`includes`方法返回`false`更明确，语义更清晰), 此外还新增了`startsWith()`, `endsWith(),` `padStart()`,`padEnd()`,`repeat()`等方法，可方便的用于查找，补全字符串



### 举一些ES6对Array数组类型做的常用升级优化

**优化部分**

- 数组解构赋值。`ES6`可以直接以`let [a,b,c] = [1,2,3]`形式进行变量赋值，在声明较多变量时，不用再写很多`let(var),`且映射关系清晰，且支持赋默认值
- 扩展运算符。`ES6`新增的扩展运算符(`...`)(重要),可以轻松的实现数组和松散序列的相互转化，可以取代`arguments`对象和`apply`方法，轻松获取未知参数个数情况下的参数集合。（尤其是在`ES5`中，`arguments`并不是一个真正的数组，而是一个类数组的对象，但是扩展运算符的逆运算却可以返回一个真正的数组）。扩展运算符还可以轻松方便的实现数组的复制和解构赋值（`let a = [2,3,4]`; `let b = [...a]`）

**升级部分**

> `ES6`在`Array`原型上新增了`find()`方法，用于取代传统的只能用`indexOf`查找包含数组项目的方法,且修复了`indexOf`查找不到`NaN的bug([NaN].indexOf(NaN) === -1)`.此外还新增了`copyWithin()`,` includes()`, `fill()`,`flat()`等方法，可方便的用于字符串的查找，补全,转换等



### 举一些ES6对Number数字类型做的常用升级优化

**优化部分**

> ES6在`Number`原型上新增了`isFinite()`, `isNaN()`方法，用来取代传统的全局`isFinite(),` `isNaN()`方法检测数值是否有限、是否是`NaN`。`ES5`的`isFinite()`, `isNaN()`方法都会先将非数值类型的参数转化为`Number`类型再做判断，这其实是不合理的，最造成i`sNaN('NaN') === true`的奇怪行为`--'NaN'`是一个字符串，但是`isNaN`却说这就是`NaN`。而`Number.isFinite()`和`Number.isNaN()`则不会有此类问题(`Number.isNaN('NaN') === false`)。（`isFinite()`同上）

**升级部分**

> `ES6`在`Math`对象上新增了`Math.cbrt()`，`trunc()`，`hypot()`等等较多的科学计数法运算方法，可以更加全面的进行立方根、求和立方根等等科学计算



### 举一些ES6对Object类型做的常用升级优化?(重要)

**优化部分**

> 对象属性变量式声明。`ES6`可以直接以变量形式声明对象属性或者方法，。比传统的键值对形式声明更加简洁，更加方便，语义更加清晰

```js
let [apple, orange] = ['red appe', 'yellow orange'];
let myFruits = \\{apple, orange\\};    // let myFruits = \\{apple: 'red appe', orange: 'yellow orange'\\};
```

> 尤其在对象解构赋值(见优化部分b.)或者模块输出变量时，这种写法的好处体现的最为明显

```js
let \\{keys, values, entries\\} = Object;
let MyOwnMethods = \\{keys, values, entries\\}; // let MyOwnMethods = \\{keys: keys, values: values, entries: entries\\}
```

可以看到属性变量式声明属性看起来更加简洁明了。方法也可以采用简洁写法

```js
let es5Fun = \\{
    method: function()\\{\\}
\\}; 
let es6Fun = \\{
    method()\\{\\}
\\}
```

> 对象的解构赋值。 `ES6`对象也可以像数组解构赋值那样，进行变量的解构赋值

```js
let \\{apple, orange\\} = \\{apple: 'red appe', orange: 'yellow orange'\\};
```

> 对象的扩展运算符(`...`)。 ES6对象的扩展运算符和数组扩展运算符用法本质上差别不大，毕竟数组也就是特殊的对象。对象的扩展运算符一个最常用也最好用的用处就在于可以轻松的取出一个目标对象内部全部或者部分的可遍历属性，从而进行对象的合并和分解

```js
let \\{apple, orange, ...otherFruits\\} = \\{apple: 'red apple', orange: 'yellow orange', grape: 'purple grape', peach: 'sweet peach'\\}; 
// otherFruits  \\{grape: 'purple grape', peach: 'sweet peach'\\}
// 注意: 对象的扩展运算符用在解构赋值时，扩展运算符只能用在最有一个参数(otherFruits后面不能再跟其他参数)
let moreFruits = \\{watermelon: 'nice watermelon'\\};
let allFruits = \\{apple, orange, ...otherFruits, ...moreFruits\\};
```

> `super` 关键字。`ES6`在`Class`类里新增了类似`this`的关键字`super`。同`this`总是指向当前函数所在的对象不同，`super`关键字总是指向当前函数所在对象的原型对象

**升级部分**

> `ES6`在`Object`原型上新增了`is()`方法，做两个目标对象的相等比较，用来完善`'==='`方法。`'==='`方法中`NaN === NaN //false`其实是不合理的，`Object.is`修复了这个小`bug`。`(Object.is(NaN, NaN) // true)`

> `ES6`在`Object`原型上新增了`assign()`方法，用于对象新增属性或者多个对象合并

```js
const target = \\{ a: 1 \\};
const source1 = \\{ b: 2 \\};
const source2 = \\{ c: 3 \\};
Object.assign(target, source1, source2);
target // \\{a:1, b:2, c:3\\}
```

> **注意**: `assign`合并的对象`target`只能合并`source1`、s`ource2`中的自身属性，并不会合并`source1`、`source2`中的继承属性，也不会合并不可枚举的属性，且无法正确复制get和set属性（会直接执行`get/set`函数，取`return`的值）

- `ES6`在`Object`原型上新增了`getOwnPropertyDescriptors()`方法，此方法增强了`ES5`中`getOwnPropertyDescriptor()`方法，可以获取指定对象所有自身属性的描述对象。结合`defineProperties()`方法，可以完美复制对象，包括复制`get`和`set`属性
- `ES6`在`Object`原型上新增了`getPrototypeOf()`和`setPrototypeOf()`方法，用来获取或设置当前对象的`prototype`对象。这个方法存在的意义在于，`ES5`中获取设置`prototype`对像是通过`__proto__`属性来实现的，然而`__proto__`属性并不是ES规范中的明文规定的属性，只是浏览器各大产商“私自”加上去的属性，只不过因为适用范围广而被默认使用了，再非浏览器环境中并不一定就可以使用，所以为了稳妥起见，获取或设置当前对象的`prototype`对象时，都应该采用ES6新增的标准用法
- `ES6`在`Object`原型上还新增了`Object.keys()`，`Object.values()`，`Object.entries()`方法，用来获取对象的所有键、所有值和所有键值对数组



### ES6 都有什么 Iterator 遍历器

答案：Set、Map

1、遍历器（Iterator）是一种接口，为各种不同的数据结构提供统一的访问机制。任何数据结构只要部署 Iterator 接口，就可以完成遍历操作（即依次处理该数据结构的所有成员）

2、Iterator 的作用有三个：

- 一是为各种数据结构，提供一个统一的、简便的访问接口；
- 二是使得数据结构的成员能够按某种次序排列；
- 三是 ES6 创造了一种新的遍历命令 for...of 循环，Iterator 接口主要供 for...of 消费。

3、默认部署了 Iterator 的数据有 Array、Map、Set、String、TypedArray、arguments、NodeList 对象，ES6 中有的是 Set、Map、



### Iterator是什么，有什么作用？(重要)

- `Iterator`是`ES6`中一个很重要概念，它并不是对象，也不是任何一种数据类型。因为`ES6`新增了`Set`、`Map`类型，他们和`Array`、`Object`类型很像，`Array`、`Object`都是可以遍历的，但是`Set`、`Map`都不能用for循环遍历，解决这个问题有两种方案，一种是为`Set`、`Map`单独新增一个用来遍历的`API`，另一种是为`Set`、`Map`、`Array`、`Object`新增一个统一的遍历`API`，显然，第二种更好，`ES6`也就顺其自然的需要一种设计标准，来统一所有可遍历类型的遍历方式。`Iterator`正是这样一种标准。或者说是一种规范理念
- 就好像`JavaScript`是`ECMAScript`标准的一种具体实现一样，`Iterator`标准的具体实现是`Iterator`遍历器。`Iterator`标准规定，所有部署了`key`值为`[Symbol.iterator]`，且`[Symbol.iterator]`的`value`是标准的`Iterator`接口函数(标准的`Iterator`接口函数: 该函数必须返回一个对象，且对象中包含`next`方法，且执行`next()`能返回包含`value/done`属性的`Iterator`对象)的对象，都称之为可遍历对象，`next()`后返回的`Iterator`对象也就是`Iterator`遍历器

```js
//obj就是可遍历的，因为它遵循了Iterator标准，且包含[Symbol.iterator]方法，方法函数也符合标准的Iterator接口规范。
//obj.[Symbol.iterator]() 就是Iterator遍历器
let obj = \\{
  data: [ 'hello', 'world' ],
  [Symbol.iterator]() \\{
    const self = this;
    let index = 0;
    return \\{
      next() \\{
        if (index < self.data.length) \\{
          return \\{
            value: self.data[index++],
            done: false
          \\};
        \\} else \\{
          return \\{ value: undefined, done: true \\};
        \\}
      \\}
    \\};
  \\}
\\};
```

> `ES6`给`Set`、`Map`、`Array`、`String`都加上了`[Symbol.iterator]`方法，且`[Symbol.iterator]`方法函数也符合标准的`Iterator`接口规范，所以`Set`、`Map`、`Array`、`String`默认都是可以遍历的

```js
//Array
let array = ['red', 'green', 'blue'];
array[Symbol.iterator]() //Iterator遍历器
array[Symbol.iterator]().next() //\\{value: "red", done: false\\}

//String
let string = '1122334455';
string[Symbol.iterator]() //Iterator遍历器
string[Symbol.iterator]().next() //\\{value: "1", done: false\\}

//set
let set = new Set(['red', 'green', 'blue']);
set[Symbol.iterator]() //Iterator遍历器
set[Symbol.iterator]().next() //\\{value: "red", done: false\\}

//Map
let map = new Map();
let obj= \\{map: 'map'\\};
map.set(obj, 'mapValue');
map[Symbol.iterator]().next()  \\{value: Array(2), done: false\\}

```



### Generator函数是什么，有什么作用？

- 如果说`JavaScript`是`ECMAScript`标准的一种具体实现、`Iterator`遍历器是`Iterator`的具体实现，那么`Generator`函数可以说是`Iterator`接口的具体实现方式。
- 执行`Generator`函数会返回一个遍历器对象，每一次`Generator`函数里面的`yield`都相当一次遍历器对象的`next()`方法，并且可以通过`next(value)`方法传入自定义的value,来改变`Generator`函数的行为。
- `Generator`函数可以通过配合`Thunk` 函数更轻松更优雅的实现异步编程和控制流管理。



### Generator

> 遍历器对象生成函数，最大的特点是可以交出函数的执行权

- `function` 关键字与函数名之间有一个星号；
- 函数体内部使用 `yield`表达式，定义不同的内部状态；
- `next `指针移向下一个状态

> 这里你可以说说 `Generator`的异步编程，以及它的语法糖 `async` 和 `awiat`，传统的异步编程。`ES6` 之前，异步编程大致如下

- 回调函数
- 事件监听
- 发布/订阅

> 传统异步编程方案之一：协程，多个线程互相协作，完成异步任务。



### Class、extends是什么，有什么作用？

> `ES6` 的`class`可以看作只是一个`ES5`生成实例对象的构造函数的语法糖。它参考了`java`语言，定义了一个类的概念，让对象原型写法更加清晰，对象实例化更像是一种面向对象编程。`Class`类可以通过`extends`实现继承。它和ES5构造函数的不同点

类的内部定义的所有方法，都是不可枚举的

```js
///ES5
function ES5Fun (x, y) \\{
	this.x = x;
	this.y = y;
\\}
ES5Fun.prototype.toString = function () \\{
	 return '(' + this.x + ', ' + this.y + ')';
\\}
var p = new ES5Fun(1, 3);
p.toString();
Object.keys(ES5Fun.prototype); //['toString']

//ES6
class ES6Fun \\{
	constructor (x, y) \\{
		this.x = x;
		this.y = y;
	\\}
	toString () \\{
		return '(' + this.x + ', ' + this.y + ')';
	\\}
\\}

Object.keys(ES6Fun.prototype); //[]
```

- `ES6`的`class`类必须用`new`命令操作，而`ES5`的构造函数不用`new`也可以执行。
- `ES6`的`class`类不存在变量提升，必须先定义`class`之后才能实例化，不像`ES5`中可以将构造函数写在实例化之后。
- `ES5` 的继承，实质是先创造子类的实例对象`this`，然后再将父类的方法添加到`this`上面。`ES6` 的继承机制完全不同，实质是先将父类实例对象的属性和方法，加到`this`上面（所以必须先调用`super`方法），然后再用子类的构造函数修改`this`。



### AMD，CMD，CommonJs，ES6 Module：解决原始无模块化的痛点

- **AMD**：`requirejs` 在推广过程中对模块定义的规范化产出，提前执行，推崇依赖前置
- **CMD**：`seajs` 在推广过程中对模块定义的规范化产出，延迟执行，推崇依赖就近
- **CommonJs**：模块输出的是一个值的 `copy`，运行时加载，加载的是一个对象（`module.exports` 属性），该对象只有在脚本运行完才会生成
- **ES6 Module**：模块输出的是一个值的引用，编译时输出接口，`ES6`模块不是对象，它对外接口只是一种静态定义，在代码静态解析阶段就会生成。



### Class 的讲解

class 语法相对原型、构造函数、继承更接近传统语法，它的写法能够让对象原型的写法更加清晰、面向对象编程的语法更加通俗
这是 class 的具体用法。

解析：[参考](https://www.cnblogs.com/fengxiongZz/p/8191503.html)



### ECMAScript6 怎么写class么，为什么会出现class这种东西?

```js
class Point \\{
  constructor(x, y) \\{
    this.x = x;
    this.y = y;
  \\}
  toString() \\{
     return '('+this.x+', '+this.y+')';
  \\}
\\}
```
