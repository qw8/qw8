---
title: ES6
date: 2020-06-08 20:50:00
categories: 
- 前端知识
tags:
- JavaScript
---

### async函数

ES2017 标准引入了 async 函数，使得异步操作变得更加方便。

async 函数是 Generator 函数的语法糖

> 什么是语法糖？
>
> 意指那些没有给计算机语言添加新功能，而只是对人类来说更“甜蜜”的语法。语法糖往往给程序员提供了更实用的编码方式，有益于更好的编码风格，更易读。不过其并没有给语言添加什么新东西

async函数使用时就是将 Generator 函数的星号（*）替换成async，将yield替换成await，仅此而已



### async函数对 Generator 函数的区别：

（1）内置执行器。

Generator 函数的执行必须靠执行器，而async函数自带执行器。也就是说，async函数的执行，与普通函数一模一样，只要一行。

（2）更好的语义。

async和await，比起星号和yield，语义更清楚了。async表示函数里有异步操作，await表示紧跟在后面的表达式需要等待结果。

（3）正常情况下，await命令后面是一个 Promise 对象。如果不是，会被转成一个立即resolve的 Promise 对象。

（4）返回值是 Promise。

async函数的返回值是 Promise 对象，这比 Generator 函数的返回值是 Iterator 对象方便多了。你可以用then方法指定下一步的操作。

**进一步说，async函数完全可以看作多个异步操作，包装成的一个 Promise 对象，而await命令就是内部then命令的语法糖。**

用法如下：

```javascript
let task1 = function()\\{
    return new Promise((res, rej)=>\\{
        setTimeout(() => \\{
            res("完成task1");
        \\}, 1000);
    \\});
\\}
let task2 = function(str)\\{
    return new Promise((res, rej)=>\\{
        setTimeout(() => \\{
            res(str+"完成task2");
        \\}, 2000);
    \\});
\\}
let task3 = function(str)\\{
    return new Promise((res, rej)=>\\{
        setTimeout(() => \\{
            res(str+"完成task3");
        \\}, 3000);
    \\});
\\}
async function f() \\{
    let t1 = await task1();  //在这里await返回的是promise中resolve方法的参数
    console.log(t1, typeof t1);  //完成task1 string
    let t2 = await task2(t1);
    console.log(t2);
    return task3(t2);  //最后用return，表示将结果作为返回的Promise对象的resolve的参数
\\}
f().then(data=>\\{console.log(data)\\});  //完成task1完成task2完成task3
```

#### 错误处理

如果await后面的异步操作出错，那么等同于async函数返回的 Promise 对象被reject。防止出错的方法，也是将其放在try...catch代码块之中。

```javascript
async function main() \\{
  try \\{
    const val1 = await firstStep();
    const val2 = await secondStep(val1);
    const val3 = await thirdStep(val1, val2);

    console.log('Final: ', val3);
  \\}
  catch (err) \\{
    console.error(err);
  \\}
\\}
```



### 解决for循环中异步处理（异步变同步）

```
function getMoney()\\{
    var money=[100,200,300]  
    for( let i=0; i<money.length; i++)\\{
        compute.exec().then(()=>\\{
            console.log(money[i])
            //alert(i)
        \\})
    \\}
\\}
//compute.exec()这是个异步方法,在里面处理一些实际业务//这时候打印出来的很可能就是300,300,300（因为异步for循环还没有等异步操作返回Promise对象过来i值已经改变）
```

正确处理思路

```
async function getMoney()\\{
    var money=[100,200,300]  
    for( let i=0; i<money.length; i++)\\{
        await compute.exec().then(()=>\\{
            console.log(money[i])
            //alert(i)
        \\})
    \\}
\\}
//关键字async/await  async告诉getMoney方法里面存在异步的操作，await放在具体异步操作（方法）前面，意思是等待该异步返回Promise才会继续后面的操作
```

另外还有一种递归的处理思路

```
function getMoney(i) \\{
　　var money=[100,200,300]
　　compute.exec().then(() => \\{
　　	if ( i < money.length ) \\{
　　		console.log(money[i]);
　　		i++;
      　　getMoney(i);
    　　\\}
  　\\});
\\}
getMoney(0);//开始调用
//用递归来实现自我循环（具体循环在then里面，可以确保前面的compute.exec()的异步操作完成）.then()是返回了Promise对象为resolve后才进行的（可以了解一下Promise对象）
```



### async/await处理多个异步请求常用

```
async function queryData()\\{
        	// 得到调用接口async1的结果
            const info = await axios.get('async1')
            // 上面的结果这里需要拼接到查询字符串里并调用async2接口
            const result = await axios.get('async2?info=' + info.data)
            return result.data
        \\}

        queryData().then((result)=>\\{
            console.log(result)
        \\})
```



### Module

ES6 的模块自动采用严格模式，不管你有没有在模块头部加上"use strict";。

模块功能主要由两个命令构成：export和import。

export命令用于规定模块的对外接口。

import命令用于输入其他模块提供的功能。



### export

一个模块就是一个独立的文件。该文件内部的所有变量，外部无法获取。如果你希望外部能够读取模块内部的某个变量，就必须使用export关键字输出该变量。

export输出遍历的写法一：

```javascript
// profile.js
export var firstName = 'Michael';
export var lastName = 'Jackson';
export var year = 1958;
```

写法二（推荐）:

```javascript
// profile.js
var firstName = 'Michael';
var lastName = 'Jackson';
var year = 1958;

export \\{firstName, lastName, year\\};
//跟上面写法等价，推荐这种写法。
```

可以使用as关键字重命名：

```javascript
function v1() \\{ ... \\}
function v2() \\{ ... \\}

//export 内部参数 as 外部调用名
export \\{
  v1 as streamV1,
  v2 as streamV2,
  v2 as streamLatestVersion
\\};
```

export语句输出的接口，与其对应的值是动态绑定关系，即通过该接口，可以取到模块内部实时的值。

```javascript
export var foo = 'bar';
setTimeout(() => foo = 'baz', 500);
//上面代码输出变量foo，值为bar，500 毫秒之后变成baz。
```

**export命令可以出现在模块的任何位置，只要处于模块顶层就可以。如果处于块级作用域内，就会报错，下面的import命令也是如此。**



### import

使用export命令定义了模块的对外接口以后，其他 JS 文件就可以通过import命令加载这个模块。

下面代码的import命令，用于加载profile.js文件，并从中输入变量。import命令接受一对大括号，里面指定要从其他模块导入的变量名。大括号里面的变量名，必须与被导入模块（profile.js）对外接口的名称相同。

```javascript
// main.js
import \\{firstName, lastName, year\\} from './profile';
```

如果想为输入的变量重新取一个名字，import命令要使用as关键字，将输入的变量重命名。

```javascript
//import 外部变量 as 内部参数
import \\{ lastName as surname \\} from './profile';
```

注意，import命令具有提升效果，会提升到整个模块的头部，首先执行。

```javascript
foo();

import \\{ foo \\} from 'my_module';
//import的执行早于foo的调用。这种行为的本质是，import命令是编译阶段执行的，在代码运行之前。
```

除了指定加载某个输出值，还可以使用整体加载，即用星号（*）指定一个对象，所有输出值都加载在这个对象上面。注意，模块整体加载所在的那个对象，不允许运行时改变。下面的写法都是不允许的。

```javascript
import * as circle from './circle';

// 下面两行都是不允许的
circle.foo = 'hello';
circle.area = function () \\{\\};
```



### export default

使用import命令的时候，用户需要知道所要加载的变量名或函数名，否则无法加载。

为了给用户提供方便，让他们不用阅读文档就能加载模块，就要用到export default命令，为模块指定默认输出。

```javascript
// export-default.js
export default function () \\{
  console.log('foo');
\\}
```

其他模块加载该模块时，import命令可以为该匿名函数**指定任意名字**。

```javascript
// import-default.js
import customName from './export-default';
customName(); // 'foo'
```

export default命令用在非匿名函数前，也是可以的。下面代码中，foo函数的函数名foo，在模块外部是无效的。加载的时候，视同匿名函数加载。

```javascript
// export-default.js
export default function foo() \\{
  console.log('foo');
\\}

// 或者写成
function foo() \\{
  console.log('foo');
\\}
export default foo;
```

export default命令用于指定模块的默认输出。显然，一个模块只能有一个默认输出，因此export default命令只能使用一次。所以，import命令后面才不用加大括号，因为只可能唯一对应export default命令。



### ES6 中类的定义

```js
// 1、类的基本定义
class Parent \\{
  constructor(name = "小白") \\{
    this.name = name;
  \\}
\\}
```

```js
// 2、生成一个实例
let g_parent = new Parent();
console.log(g_parent); //\\{name: "小白"\\}
let v_parent = new Parent("v"); // 'v'就是构造函数name属性 , 覆盖构造函数的name属性值
console.log(v_parent); // \\{name: "v"\\}
```

```js
// 3、继承
class Parent \\{
  //定义一个类
  constructor(name = "小白") \\{
    this.name = name;
  \\}
\\}

class Child extends Parent \\{\\}

console.log("继承", new Child()); // 继承 \\{name: "小白"\\}
```

```js
// 4、继承传递参数
class Parent \\{
  //定义一个类
  constructor(name = "小白") \\{
    this.name = name;
  \\}
\\}

class Child extends Parent \\{
  constructor(name = "child") \\{
    // 子类重写name属性值
    super(name); // 子类向父类修改 super一定放第一行
    this.type = "preson";
  \\}
\\}
console.log("继承", new Child("hello")); // 带参数覆盖默认值  继承\\{name: "hello", type: "preson"\\}
```

```js
// 5、ES6重新定义的ES5中的访问器属性
class Parent \\{
  //定义一个类
  constructor(name = "小白") \\{
    this.name = name;
  \\}

  get longName() \\{
    // 属性
    return "mk" + this.name;
  \\}

  set longName(value) \\{
    this.name = value;
  \\}
\\}

let v = new Parent();
console.log("getter", v.longName); // getter mk小白

v.longName = "hello";
console.log("setter", v.longName); // setter mkhello
```

```js
// 6、类的静态方法
class Parent \\{
  //定义一个类
  constructor(name = "小白") \\{
    this.name = name;
  \\}

  static tell() \\{
    // 静态方法:通过类去调用，而不是实例
    console.log("tell");
  \\}
\\}

Parent.tell(); // tell
```

```js
// 7、类的静态属性：

class Parent \\{
  //定义一个类
  constructor(name = "小白") \\{
    this.name = name;
  \\}

  static tell() \\{
    // 静态方法:通过类去调用，而不是实例
    console.log("tell"); // tell
  \\}
\\}

Parent.type = "test"; // 定义静态属性

console.log("静态属性", Parent.type); // 静态属性 test

let v_parent = new Parent();
console.log(v_parent); // \\{name: "小白"\\}  没有tell方法和type属性
```



### 解构赋值及其原理

解构赋值：其实就是分解出一个对象的解构，分成两个步骤：

1. 变量的声明
2. 变量的赋值

原理：ES6 变量的解构赋值本质上是“模式匹配”,只要等号两边的模式相同，左边的变量就会被赋予匹配的右边的值，如果匹配不成功变量的值就等于 undefined

解析：

一、 数组的解构赋值

```js
// 对于数组的解构赋值，其实就是获得数组的元素，而我们一般情况下获取数组元素的方法是通过下标获取，例如：
let arr = [1, 2, 3];
let a = arr[0];
let b = arr[1];
let c = arr[2];

// 而数组的解构赋值给我们提供了极其方便的获取方式，如下：
let [a, b, c] = [1, 2, 3];
console.log(a, b, c); //1,2,3
```

1. 模式匹配解构赋值

```js
let [foo, [[bar], baz]] = [1, [[2], 3]];
console.log(foo, bar, baz); //1,2,3
```

2. 省略解构赋值

```js
let [, , a, , b] = [1, 2, 3, 4, 5];
console.log(a, b); //3,5
```

3. 含剩余参数的解构赋值

```js
let [a, ...reset] = [1, 2, 3, 4, 5];
console.log(a, reset); //1,[2,3,4,5]
```

其转成 ES5 的原理如下：

```js
var a = 1,
  reset = [2, 3, 4, 5];
console.log(a, reset); //1,[2,3,4,5]
```

注意：如果剩余参数是对应的值为 undefined，则赋值为[]，因为找不到对应值的时候，是通过 slice 截取的，如下：

```js
let [a, ...reset] = [1];
console.log(a, reset); //1,[]
```

其转成 ES5 的原理如下：

```js
var _ref = [1],
  a = _ref[0],
  reset = _ref.slice(1);
console.log(a, reset); //1,[]
```

4. 非数组解构成数组(重点，难点)

一条原则：要解构成数组的前提：如果等号右边，不是数组(严格地说，不是可遍历的解构)，则直接报错，例如：

```js
let [foo] = 1; //报错
let [foo1] = false; //报错
let [foo2] = NaN; //报错
let [foo3] = undefined; //报错
let [foo4] = null; //报错
let [foo5] = \\{\\}; //报错
```

为什么？转成 ES5 看下原理就一清二楚了：

```js
var _ = 1,
  foo = _[0]; //报错
var _false = false,
  foo1 = _false[0]; //报错
var _NaN = NaN,
  foo2 = _NaN[0]; //报错
var _undefined = undefined,
  foo3 = _undefined[0]; //报错
var _ref = null;
foo4 = _ref[0]; //报错
var _ref2 = \\{\\},
  foo5 = _ref2[0]; //报错
```

5. Set 的解构赋值

先执行 new Set()去重，然后对得到的结果进行解构

```js
let [a, b, c] = new Set([1, 2, 2, 3]);
console.log(a, b, c); //1,2,3
```

6. 迭代器解构

```js
function* fibs() \\{
  let a = 0;
  let b = 1;
  while (true) \\{
    yield a;
    [a, b] = [b, a + b];
  \\}
\\}

let [first, second, third, fourth, fifth, sixth] = fibs();
sixth; // 5
```

**总结 1：只要某种数据结构具有 Iterator 接口，都可以采用数组形式的解构赋值。**

7. 解构赋值的默认值

当变量严格等于 undefined 的时候，会读取默认值，所谓的严格等于，就是“===”

```js
----------

let [a,b = 'default'] = [1];
console.log(a,b);//1,'default'

----------

let [c = 'default'] = [undefined];
console.log(c);//'default'

----------

function f() \\{
  console.log('aaa');
\\}

let [x = f()] = [1];
console.log(x);//1

----------

function f() \\{
  console.log('aaa');//'aaa'
\\}

let [a,x = f()] = [1];
console.log(a,x);//1,undefined
```

**总结 2：如果不使用默认值，则不会执行默认值的函数**

二、对象的解构赋值

1. 解构赋值的举例：

```js
let p1 = \\{
  name: "zhuangzhuang",
  age: 25
\\};
let \\{ name, age \\} = p1; //注意变量必须为属性名
console.log(name, age); //"zhuangzhuang",25
```

其转成 es5 的原理则为：

```js
var _p1 = p1,
  name = _p1.name,
  age = _p1.age;
console.log(name, age); //"zhuangzhuang",25
```

2. 解构赋值的别名

如果使用别名，则不允许再使用原有的解构出来的属性名，看以下举例则会明白：

```js
let p1 = \\{
  name: "zhuangzhuang",
  age: 25
\\};
let \\{ name: aliasName, age: aliasAge \\} = p1; //注意变量必须为属性名
console.log(aliasName, aliasAge); //"zhuangzhuang",25
console.log(name, age); //Uncaught ReferenceError: age is not defined
```

为何打印原有的属性名则会报错？让我们看看转成 es5 后的原理是如何实现的：

```js
var _p1 = p1,
  aliasName = _p1.name,
  aliasAge = _p1.age;
console.log(aliasName, aliasAge); //"zhuangzhuang",25
console.log(name, age); //所以打印name和age会报错——“Uncaught ReferenceError: age is not defined”，但是为何只报错age，不报错name呢？
```

只报错 age，不报错 name，这说明其实 name 是存在的，那么根据 js 的解析顺序，当在当前作用域 name 无法找到时，会向上找，直到找到 window 下的 name,而我们打印 window 可以发现，其下面确实有一个 name，值为“”，而其下面并没有属性叫做 age，所以在这里 name 不报错，只报 age 的错。类似 name 的属性还有很多，比如 length 等。

3. 解构赋值的默认值

有些情况下，我们解构出来的值并不存在，所以需要设定一个默认值，例如：

```js
let obj = \\{
  name: "zhuangzhuang"
\\};
let \\{ name, age \\} = obj;
console.log(name, age); //"zhuangzhuang",undefined
```

我们可以看到当 age 这个属性并不存在于 obj 的时候，解构出来的值为 undefined，那么为了避免这种尴尬的情况，我们常常会设置该属性的默认值，如下：

```js
let obj = \\{
  name: "zhuangzhuang"
\\};
let \\{ name, age = 18 \\} = obj;
console.log(name, age); //"zhuangzhuang",18
```

当我们取出来的值不存在，即为 undefined 的时候，则会取默认值(假设存在默认值)，ES6 的默认值是使用**“变量=默认值”**的方式。

注意：只有当为 undefined 的时候才会取默认值，null 等均不会取默认值

```js
let obj = \\{
  name: "zhuangzhuang",
  age: 27,
  gender: null, //假设未知使用null
  isFat: false
\\};
let \\{ name, age = 18, gender = "man", isFat = true, hobbies = "study" \\} = obj;
console.log(name, age, gender, isFat, hobbies); //"zhuangzhuang"，27，null，false，"study"
```

4. 解构赋值的省略赋值

当我们并不是需要取出所有的值的时候，其实可以省略一些变量，这就是省略赋值，如下

```js
let arr = [1, 2, 3];
let [, , c] = arr;
console.log(c); //3
```

注意：省略赋值并不存在与对象解构，因为对象解构，明确了需要的属性

```js
let obj = \\{
  name: "zhuangzhuang",
  age: 27,
  gender: "man"
\\};
let \\{ age \\} = obj;
console.log(age); //27
```

5. 解构赋值的嵌套赋值(易错点，重点，难点)

```js
let obj = \\{\\},
  arr = [];

(\\{ foo: obj.prop, bar: arr[0] \\} = \\{ foo: 123, bar: true \\});
console.log(obj, arr); //\\{prop:123\\},[true]
```

注意当解构出来是 undefined 的时候，如果再给子对象的属性，则会报错，如下

```js
let \\{
  foo: \\{ bar \\}
\\} = \\{ baz: "baz" \\};
//报错，原因很简单，看下原理即可，如下：
//原理:
let obj = \\{ baz: "baz" \\};
let foo = obj.foo; //foo为undefined
let bar = foo.bar; //undefined的bar，可定报错
```

6. \\{\\}是块还是对象？

当我们写解构赋值的时候，很容易犯一个错误——\\{\\}的作用是块还是对象混淆，举例如下：

```js
//举例一：
let \\{a\\} = \\{a:"a"\\};
console.loh(a);//'a',这个很简单
//很多人觉得，以下这种写法也是可以的：
let a;
\\{a\\} = \\{a:"a"\\};//直接报错，因为此时a已经声明过了，在语法解析的时候，会将这一行的\\{\\}看做块结构，而“块=对象”，显然是语法错误，所以正确的做法是不将大括号写在开头，如下：
let a;
(\\{a\\} = \\{a:"a"\\})
```

7. 空解构

按照之前写的，解构赋值，左边则为解构出来的属性名，当然，在这里，我们也可以不写任何属性名称，也不会又任何的语法错误，即便这样没有任何意义，如下：

```js
(\\{\\} = [true, false]);
(\\{\\} = "abc");
(\\{\\} = []);
```

8. 解构成对象的原则

如果解构成对象，右侧不是 null 或者 undefined 即可!
之前说过，要解构成数组，右侧必须是可迭代对象，但是如果解构成对象，右侧不是 null 活着 undefined 即可!

三、字符串的解构赋值

字符串也是可以解构赋值的

```js
const [a, b, c, d, e] = "hello";
console.log(a, b, c, d, e); //'h','e','l','l','o'
```

转成 es5 的原理如下:

```js
var _hello = "hello",
  a = _hello[0],
  b = _hello[1],
  c = _hello[2];

console.log(a, b, c);
```

注意：字符串有一个属性 length，也可以被解构出来，但是要注意，解构属性一定是对象解构

```js
let \\{ length \\} = "hello";
console.log(length); //5
```

4. 布尔值和数值的解构

布尔值和数值的解构，其实就是对其包装对象的解构，取的是包装对象的属性

```js
\\{toString:s\\} = 123;
console.log(s);//s === Number.prototype.toString

\\{toString:s\\} = true;
console.log(s);//s === Boolean.prototype.toString
```

### 总结：解构赋值的规则是：

> 1. 解构成对象，只要等号右边的值不是对象或数组，就先将其转为对象。由于 undefined 和 null 无法转为对象，所以对它们进行解构赋值，都会报错。
> 2. 解构成数组，等号右边必须为可迭代对象

[参考](https://blog.csdn.net/qq_17175013/article/details/81490923)



### Array.from() 与 Array.reduce()

Array.from()方法就是将一个类数组对象或者可遍历对象转换成一个真正的数组
Array.reduce()方法对累加器和数组中的每个元素 (从左到右)应用一个函数，将其减少为单个值。

解析：

**Array.from()**

```js
// 那么什么是类数组对象呢？所谓类数组对象，最基本的要求就是具有length属性的对象。

// 1、将类数组对象转换为真正数组：

let arrayLike = \\{
  0: "tom",
  1: "65",
  2: "男",
  3: ["jane", "john", "Mary"],
  length: 4
\\};
let arr = Array.from(arrayLike);
console.log(arr); // ['tom','65','男',['jane','john','Mary']]

// 那么，如果将上面代码中length属性去掉呢？实践证明，答案会是一个长度为0的空数组。

// 这里将代码再改一下，就是具有length属性，但是对象的属性名不再是数字类型的，而是其他字符串型的，代码如下：

let arrayLike = \\{
  name: "tom",
  age: "65",
  sex: "男",
  friends: ["jane", "john", "Mary"],
  length: 4
\\};
let arr = Array.from(arrayLike);
console.log(arr); // [ undefined, undefined, undefined, undefined ]

// 会发现结果是长度为4，元素均为undefined的数组

// 由此可见，要将一个类数组对象转换为一个真正的数组，必须具备以下条件：

// 1、该类数组对象必须具有length属性，用于指定数组的长度。如果没有length属性，那么转换后的数组是一个空数组。

// 2、该类数组对象的属性名必须为数值型或字符串型的数字

// ps: 该类数组对象的属性名可以加引号，也可以不加引号

// 2、将Set结构的数据转换为真正的数组：

let arr = [12, 45, 97, 9797, 564, 134, 45642];
let set = new Set(arr);
console.log(Array.from(set)); // [ 12, 45, 97, 9797, 564, 134, 45642 ]

// 　Array.from还可以接受第二个参数，作用类似于数组的map方法，用来对每个元素进行处理，将处理后的值放入返回的数组。如下：

let arr = [12, 45, 97, 9797, 564, 134, 45642];
let set = new Set(arr);
console.log(Array.from(set, item => item + 1)); // [ 13, 46, 98, 9798, 565, 135, 45643 ]

// 3、将字符串转换为数组：

let str = "hello world!";
console.log(Array.from(str)); // ["h", "e", "l", "l", "o", " ", "w", "o", "r", "l", "d", "!"]

// 4、Array.from参数是一个真正的数组：

console.log(Array.from([12, 45, 47, 56, 213, 4654, 154]));
// 像这种情况，Array.from会返回一个一模一样的新数组
```

[参考](https://www.cnblogs.com/jf-67/p/8440758.html)

**Array.reduce()**

```
语法：

array.reduce(function(accumulator, currentValue, currentIndex, array), initialValue)；

accumulator：累加器，即函数上一次调用的返回值。第一次的时候为 initialValue || arr[0]

currentValue：数组中函数正在处理的的值。第一次的时候initialValue || arr[1]

currentIndex：数据中正在处理的元素索引，如果提供了 initialValue ，从0开始；否则从1开始

array： 调用 reduce 的数组

initialValue：可选项，累加器的初始值。没有时，累加器第一次的值为currentValue；注意：在对没有设置初始值的空数组调用reduce方法时会报错。
```

```js
//无初始值
[1, 2, 3, 4].reduce(function(accumulator, currentValue, currentIndex, array) \\{
  return accumulator + currentValue;
\\}); // 10
```

| callback    | accumulator       | currentValue      | currentIndex    | array        | return value |
| ----------- | ----------------- | ----------------- | --------------- | ------------ | ------------ |
| first call  | 1(数组第一个元素) | 2(数组第二个元素) | 1(无初始值为 1) | [1, 2, 3, 4] | 3            |
| second call | 3                 | 3                 | 2               | [1, 2, 3, 4] | 6            |
| third call  | 6                 | 4                 | 3               | [1, 2, 3, 4] | 10           |

```js
//有初始值
[1, 2, 3, 4].reduce(function(accumulator, currentValue, currentIndex, array) \\{
  return accumulator + currentValue;
\\}, 10); // 20
```

| callback    | accumulator | currentValue      | currentIndex    | array        | return value |
| ----------- | ----------- | ----------------- | --------------- | ------------ | ------------ |
| first call  | 10(初始值)  | 1(数组第一个元素) | 0(有初始值为 0) | [1, 2, 3, 4] | 11           |
| second call | 11          | 2                 | 1               | [1, 2, 3, 4] | 13           |
| third call  | 13          | 3                 | 2               | [1, 2, 3, 4] | 16           |
| fourth call | 16          | 4                 | 3               | [1, 2, 3, 4] | 20           |

```js
//1.数组元素求和
[1, 2, 3, 4].reduce((a, b) => a + b); //10

//2.二维数组转化为一维数组
[[1, 2], [3, 4], [5, 6]]
  .reduce((a, b) => a.concat(b), []) //[1, 2, 3, 4, 5, 6]

  [
    //3.计算数组中元素出现的次数
    (1, 2, 3, 1, 2, 3, 4)
  ].reduce((items, item) => \\{
    if (item in items) \\{
      items[item]++;
    \\} else \\{
      items[item] = 1;
    \\}
    return items;
  \\}, \\{\\}) //\\{1: 2, 2: 2, 3: 2, 4: 1\\}

  [
    //数组去重①
    (1, 2, 3, 1, 2, 3, 4, 4, 5)
  ].reduce((init, current) => \\{
    if (init.length === 0 || init.indexOf(current) === -1) \\{
      init.push(current);
    \\}
    return init;
  \\}, []) //[1, 2, 3, 4, 5]
  [
    //数组去重②
    (1, 2, 3, 1, 2, 3, 4, 4, 5)
  ].sort()
  .reduce((init, current) => \\{
    if (init.length === 0 || init[init.length - 1] !== current) \\{
      init.push(current);
    \\}
    return init;
  \\}, []); //[1, 2, 3, 4, 5]
```

[参考](https://www.cnblogs.com/xuejiangjun/p/8523313.html)