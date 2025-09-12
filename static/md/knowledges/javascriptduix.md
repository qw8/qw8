---
title: JavaScript对象
date: 2020-04-18 22:10:40
categories: 
- 前端知识
tags:
- JavaScript
- 类
- 对象
---

### 操作对象

1.Object.assign()

用于拼接，或者创建一个新对象

拼接：相同字段后面会覆盖前面的

```
let obj = \\{
    name:'张三',
    sex:'男'
\\}
Object.assign(obj,\\{name:'李四',age:20\\})
console.log(obj)//\\{name: "李四", sex: "男", age: 20\\}
```

创建新对象：

```
let obj = \\{
    name:'张三',
    sex:'男'
\\}
let newObj = Object.assign(\\{\\},obj,\\{name:'李四',age:20\\})
console.log(newObj)//\\{name: "李四", sex: "男", age: 20\\}
```

2.delete

删除对象某个属性

```
delete a.age;
```

3.Object.keys()

返回对象可枚举属性（返回一个数组）

```
let obj = \\{
    name:'张三',
    sex:'男'
\\}
let newArr = Object.keys(obj)
console.log(newArr)//["name", "sex"]
```

4.Object.values()

返回对象可枚举的值（返回一个数组）

```
let obj = \\{
    name:'张三',
    sex:'男'
\\}
let newArr = Object.values(obj)
console.log(newArr)//["张三", "男"]
```

5.Object.entries()

返回键值对 [[key, value],[key, value]] 数组

```
let obj = \\{
    name:'张三',
    sex:'男'
\\}
let newArr = Object.entries(obj)
console.log(newArr)//[["name":"张三"],["sex":"男"]]
```

6.Object.fromEntries()

Object.fromEntries()方法是Object.entries()的逆操作，用于将键值对数组转为对象

```
Object.fromEntries([
  ['foo', 'bar'],
  ['baz', 42]
])
// \\{ foo: "bar", baz: 42 \\}
```



### 对对象的检测

1. name in obj

检测对象中是否有某个属性

```
var person = \\{
    name:'张三'
\\}
console.log('name' in person) //true
```

2. 判断对象是否为空

（1）JSON方式

将对象转化为json字符串，再判断字符串是否为" \\{\\} "

```
let data = \\{\\};
let b = (JSON.Stringify(data) == "\\{\\}")  

//注意：这里双括号外面要有双引号,因为JSON数据括号外面有双引号
```

（2）使用Object.keys()

```
let data = \\{\\};
let arr = Object.keys(data);
console.log(arr.length == 0); //true
```



### 删除JS 对象属性（元素）

```
var a=\\{"id":1,"name":"danlis"\\};
//添加属性
a.age=18;
console.log(a);
//结果：Object \\{ id: 1, name: "danlis", age: 18 \\}
//修改属性
a.age="我怎么知道";
//结果：Object \\{ id: 1, name: "danlis", age: "我怎么知道" \\}
 
delete a.age;
//结果：Object \\{ id: 1, name: "danlis" \\}
```



### Js判断对象是否为空

#### 1.for (... in ...)

```
for(var i in obj)\\{
    return true;    //如果不为空，返回true
\\}
return false;    //如果为空，返回false
```

#### 2.JSON.stringify()

```
if(JSON.stringify(data) === '\\{\\}')\\{
    return false;    //如果为空，返回false
\\}
return true;    //如果不为空，返回true
```

#### 3.ES6新增方法Object.keys()

```
if(Object.keys(object).length === 0)\\{
    return false;    //如果为空，返回false
\\}
return true;    //如果不为空，返回true
```



### 判断对象属性eventTag不为undefined（或者是否数组）且长度大于0

```
selectValue.eventTag && selectValue.eventTag.length > 0
```

```
if (Array.isArray(zone.AlarmInfoSublist) && zone.AlarmInfoSublist.length > 0) 
```



使用hook导入外部数据需要深拷贝，不然是只读无法修改

### 手写一个深拷贝（深克隆）

#### 1. 首先使用JSON.parse来实现一个深拷贝

最简单且兼容性较好的方式是使用`JSON.parse`和`JSON.stringify`方法。但是这种方法不适用于包含函数、循环引用或特殊类型（如`Date`和`RegExp`）的对象。对于简单的数据结构，这应该足够了。

```js
let test = \\{
	x : 1,
	y : 2,
	z : \\{
		a : 4,
		b : 5
	\\}
\\}
// 深拷贝
let result = JSON.parse(JSON.stringify(test));
// 改变拷贝后的值
result.z.a = 40;
console.log(test);
console.log(result);
```

#### 2. 手写实现深拷贝

```text
function deepClone(obj)\\{
    let cloneObj;
    // 判断当输入的数据是简单数据类型时，直接复制
    if(obj && typeof obj !== 'object')\\{
        cloneObj = obj;
    \\}
    // 当输入的数据是对象或者数组时
    else if(obj && typeof obj === 'object')\\{
        // 检测输入的数据是数组还是对象
        cloneObj = Array.isArray(obj) ? [] : \\{\\};

        // 变量数据对象
        for(let key in obj)\\{
            // 判断对象是否存在key属性
            if(obj.hasOwnProperty(key))\\{
                if(obj[key] && typeof obj[key] === 'object')\\{
                    // 若当前元素类型为对象时，递归调用
                    cloneObj[key] = deepClone(obj[key]);
                \\}
                // 若当前元素类型为基本数据类型
                else\\{
                    cloneObj[key] = obj[key];
                \\}
            \\}
        \\}
    \\}
    return cloneObj;
\\}

// 测试用例
deepClone(\\{
  x: 1,
  y: [ 5, 6, 7 ],
  z: \\{
    a: 0,
    b: 1
  \\}
\\})
```



### JS中如何进行对象的深拷贝

在JS中，一般的=号传递的都是对象/数组的引用，并没有真正地拷贝一个对象，那如何进行对象的深度拷贝呢？如果你对此也有疑问，这篇文章或许能够帮助到你

#### 一、对象引用、浅层拷贝与深层拷贝的区别

js的对象引用传递理解起来很简单，参考如下代码：

```javascript
var a = \\{name:'wanger'\\}
var b = a ;
a===b // true
b.name = 'zhangsan'
a.name //'zhangan'
```

上述代码中，使用了`=`进行赋值，于是b指向了a所指向的栈的对象，也就是a与b指向了同一个栈对象，所以在对b.name赋值时，a.name也发生了变化。为了避免上面的情况，可以对对象进行拷贝，代码如下：

```javascript
var a = \\{name:'wanger'\\}
var b = Object.assign(\\{\\}, a)
a===b // false
b.name = 'zhangsan'
a.name //'wanger'
```

上面代码将原始对象拷贝到一个空对象，就得到了原始对象的克隆，这时候a与b指向的是不同的栈对象，所以对b.name重新复制也不会影响到a.name。**但是如果a.name是一个对象的引用，而不是一个字符串，那么上面的代码也会遇到一些问题**，参考如下代码：

```javascript
var a = \\{name:\\{firstName:'wang',lastName:'er'}}
var b = Object.assign(\\{\\}, a)
a===b // false
b.name.firstName = 'zhang'
a.name.firstName //'zhang'
```

b.name.firstName又影响到了a.name.firstName，这是因为Object.assign()方法只是浅层拷贝，a.name是一个栈对象的引用，赋值给b时，b.name也同样是这个栈对象的引用，很多时候，我们不想让这种事情发生，所以我们就需要用到对象的深拷贝。

#### 二、使用JSON.parse（）与JSON.stringify（）对对象进行拷贝

通常情况下，我们可以使用JSON.parse（）与 JSON.stringify（）实现对象的深克隆，如下：

```javascript
var clone = function (obj) \\{
    return JSON.parse(JSON.stringify(obj));
\\}
```

这种方法只适用于**纯数据json对象的深度克隆**，因为有些时候，这种方法也有缺陷，参考如下代码：

```javascript
var clone = function (obj) \\{
    return JSON.parse(JSON.stringify(obj));
\\}
var a = \\{a:function()\\{console.log('hello world')\\},b:\\{c:1\\},c:[1,2,3],d:"wanger",e:new Date(),f:null,g:undefined\\}
var b = clone(a)
```

我们发现，上述的方法会忽略值为function以及undefied的字段，而且对date类型的支持也不太友好。

更要紧的是，上述方法只能克隆原始对象自身的值，不能克隆它继承的值，参考如下代码：

```javascript
function Person (name) \\{
    this.name = name
\\}
var wanger = new Person('王二')
var newwanger = clone(wanger)
wanger.constructor === Person // true
newwanger.constructor === Object // true
```

我们发现，克隆的对象的构造函数已经变成了Object,而原来的对象的构造是Person。

#### 三、目前没有发现bug的对象深拷贝方法

王二在网上参考了不少文章，方法都不尽完美，于是在前人基础上改造了一下，方法如下，目前没有发现有什么bug：

```javascript
var clone = function (obj) \\{ 
    if(obj === null) return null 
    if(typeof obj !== 'object') return obj;
    if(obj.constructor===Date) return new Date(obj); 
    var newObj = new obj.constructor ();  //保持继承链
    for (var key in obj) \\{
        if (obj.hasOwnProperty(key)) \\{   //不遍历其原型链上的属性
            var val = obj[key];
            newObj[key] = typeof val === 'object' ? arguments.callee(val) : val; // 使用arguments.callee解除与函数名的耦合
        \\}
    \\}  
    return newObj;  
\\}; 
```

这里有三点需要注意：
1、用`new obj.constructor ()`构造函数新建一个空的对象，而不是使用`\\{\\}`或者`[]`,这样可以保持原形链的继承；
2、用`obj.hasOwnProperty(key)`来判断属性是否来自原型链上，因为`for..in..`也会遍历其原型链上的可枚举属性。
3、上面的函数用到递归算法，在函数有名字，而且名字以后也不会变的情况下，这样定义没有问题。但问题是这个函数的执行与函数名 factorial 紧紧耦合在了一起。为了消除这种紧密耦合的现象，需要使用 `arguments.callee`。

------

2017-10-03添加，之前没有考虑正则对象的问题，这里再做一下修改：

```javascript
var clone = function (obj) \\{ 
    if(obj === null) return null 
    if(typeof obj !== 'object') return obj;
    if(obj.constructor===Date) return new Date(obj); 
    if(obj.constructor === RegExp) return new RegExp(obj);
    var newObj = new obj.constructor ();  //保持继承链
    for (var key in obj) \\{
        if (obj.hasOwnProperty(key)) \\{   //不遍历其原型链上的属性
            var val = obj[key];
            newObj[key] = typeof val === 'object' ? arguments.callee(val) : val; // 使用arguments.callee解除与函数名的耦合
        \\}
    \\}  
    return newObj;  
\\}; 
```



### js对象中的get和set方法的实现

对象中有get和set方法，在读取和设定值的时候触发。vue中的数据绑定就是通过这个来实现的。

#### 1. 直接在对象内使用

- **get用法**

```jsx
var user = \\{
    info: \\{
        name: "张三"
    \\},
    get name()\\{
        return this.info.name;
    \\}
\\}
    console.log(user.info.name) // '张三'
    console.log(user.name) // '张三'
```

*作用：*
(1). 在对象内属性嵌套层级过多时，可以直接在对象下读取到对应属性，简化调用；
(2). 在get时可以任意设置属性名，可以不暴露组件内部属性名。

- **set用法**

```jsx
var user = \\{
    info: \\{
        name: "张三"
    \\},
    set name(val)\\{
        console.log('我改名了');
        this.info.name = val;
    \\}
\\}
    console.log(user.name) // '张三'

    user.set = '李四'; // '我改名了'
    console.log(user.name) // '李四'
```

*作用：*
(1). 在对象内属性嵌套层级过多时，可以直接在对象下设置到对应属性，简化层级；
(2). set方法内的逻辑在赋值时会自动执行，可以监听属性值的改变

#### 2. 使用Object.defineProperty()

```jsx
var user = \\{
    name: '张三'
\\}

Object.defineProperty(user, name, \\{
    get()\\{
        return user.name
    \\},
    set(val)\\{
        console.log('我改名了');
        user.name = val
    \\}

\\})

console.log(user.name) // '张三'
user.name = '王二'; // '我改名了'

console.log(user.name) // '王二'
```

*作用：*
set方法可以监听对应属性值的改变，vue的数据动态绑定就是通过这个方法实现的，监听到vue实例中的data属性发生改变时，在set方法中触发模版重新渲染逻辑。

#### 3. 使用Object.defineProperties()

```jsx
var user = \\{
    name: '张三'
\\}

Object.defineProperties(user, \\{
    nameGet: \\{
        value: function() \\{
            console.log('读取');
            return this.name;
        \\}
    \\},
    nameSet: \\{
        value: function(name) \\{
            console.log('设置');
            this.name = name;
        \\}
    \\}
 

\\})

console.log(user.nameGet) // '读取'  '张三'
user.nameSet = '王二'; // '设置'

console.log(user.nameSet) // '王二'
```

*作用：*
和方法1直接在对象中设置效果和原理相似

#### 4.对象初始化之后可以这样添加属性

```
var obj=\\{
    a: 1,
    b: 2    
\\};

obj.__defineGetter__('c', function()\\{return c\\});
obj.__defineSetter__('c', function(x)\\{c = x\\});
```



### Object.assign()

Object.assign() 方法用于将所有可枚举属性的值从一个或多个源对象复制到目标对象。它将返回目标对象。

简单来说，就是Object.assign()是对象的静态方法，可以用来复制对象的可枚举属性到目标对象，利用这个特性可以实现对象属性的合并。

#### 用法：

```js
 Object.assign(target, ...sources)
```

参数：

target--->目标对象
source--->源对象

返回值：target，即目标对象

#### 使用示例：

##### 1、目标对象和源对象无重名属性

```js
var target=\\{name:'guxin', age:25\\};
var source=\\{state:'single'\\}
var result=Object.assign(target,source);
console.log(target,target==result);
// \\{name:'guxin', age:25, state:'single'\\} true
```

我们可以看到source上的state属性合并到了target对象上。如果只是想将两个或多个对象的属性合并到一起，不改变原有对象的属性，可以用一个空的对象作为target对象。像下面这样：

```js
var result=Object.assign(\\{\\},target,source);
```

##### 2、目标对象和源对象有重名属性

上面的示例目标对象和源对象是没有重名属性的，那么如果他们有重名属性又会怎样呢？是后面的属性覆盖前面的还是前面的属性覆盖后面的呢？我们接下来看下一个例子：

```js
var target=\\{name:'guxin', age:18\\}
var source=\\{state:'signle', age:22\\}
var result=Object.assign(target,source)
console.log(target)
// \\{name:'guxin, age:22, state:'single'\\}
```

可以看到如果有同名属性的话，后面的属性值会覆盖前面的属性值。

##### 3、有多个源对象

前面的示例都是只有一个源对象，那么如果有多个源对象情况会不会不同呢？我们继续看下面的例子：

```js
var target=\\{name:'guxin', age:18\\}
var source1=\\{state:'signle', age:22\\}
var source2=\\{mood:'happy', age:25\\}
var result=Object.assign(target,source1,source2)
console.log(target)
// \\{name:'guxin, age:25, state:'single', mood:'happy'\\}
```

可以看到有多个源对象情况也是和一个源对象一样的。没有同名的属性会直接复制到目标对象上，同名的属性后面的属性值会覆盖前面的同名属性值。

#### 注意事项：

1、Object.assign 方法只会拷贝源对象自身的并且可枚举的属性到目标对象，继承属性和不可枚举属性是不能拷贝的。

2、针对深拷贝，需要使用其他办法，因为 Object.assign()拷贝的是属性值。假如源对象的属性值是一个对象的引用，那么它也只指向那个引用。

3、目标对象自身也会改变

4、异常会打断后续拷贝任务

#### 兼容性

目前IE浏览器不兼容Object.assign()，如果需要兼容IE的话最好不要直接使用这个方法。

#### 六、与$.extend()的比较

我们通过一个简单的示例来比较两者有什么不同，

```js
    var target=\\{name:'guxin',age:18\\}
    var source1=\\{state:'signle',age:22\\}
    var source2=\\{mood:'happy',age:25\\}
    var result=Object.assign(target,source1,source2)
    console.log(target)
    
    var targetObj=\\{name:'guxin',age:18\\}
    var sourceObj1=\\{state:'signle',age:22\\}
    var sourceObj2=\\{mood:'happy',age:25\\}
    var result=$.extend(targetObj,sourceObj1,sourceObj2)
    console.log(targetObj)
    
    // 结果都是\\{name:'guxin, age:25, state:'single', mood:'happy'\\}
```
可以看到两者得到的结果是一样的。所以，我认为这两个方法，除了兼容性应该是一样的。

原文链接：https://blog.csdn.net/weixin_43290151/article/details/124715850



### Object.assign 和 Object.create 的一些理解

- assign 不继承原型 浅拷贝的**proto**是 Object 而 Object.create 的 proto 指向它继承来的那个对象 从而让整个原型链串起来
- assign 可以合并 浅拷贝俩对象 而 create 就是继承

#### 文章

- :book: [Object.create —— MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/create)
- :book: [Object.assign —— MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)
- :book: [Object.create vs Object.assign —— 慕课网手记](https://www.imooc.com/article/17591)
- :book: [JS 中的 Object.assign()、Object.create()、Object.defineProperty() —— CSDN](https://blog.csdn.net/DeepLies/article/details/52915143)
- :book: [es6 中 object.create()和 object.assign() —— 风信子博客](http://www.onlyfordream.cn/2018/03/19/es6\\%E4\\%B8\\%ADobject-create\\%E5\\%92\\%8Cobject-assign/)
- :book: [Object-Assign-Deep —— github](https://github.com/saikojosh/Object-Assign-Deep)



### js合并多个对象并且去重

#### 方法一：

```javascript
let o1 = \\{ a: 1, b: 2 \\};
let o2 = \\{ c: 4, d: 5 \\};
let o3 = \\{...o1, ...o2\\};//\\{ a: 1, b: 2, c: 4, d: 5\\}
```

如果有重复的`key`，则后面的会将前面的值覆盖掉

```javascript
let o1 = \\{ a: 1, b: 2 \\};
let o2 = \\{ c: 4, b: 5 \\};
let o3 = \\{...o1, ...o2\\};//\\{ a: 1, b: 5, c: 4\\}
```

#### 方法二：

`Object.assign`方法用于对象的合并，将源对象`（source）`的所有可枚举属性，复制到目标对象`（target）`。

```javascript
const target = \\{ a: 1 \\};

const source1 = \\{ b: 2 \\};
const source2 = \\{ c: 3 \\};

Object.assign(target, source1, source2);
target // \\{a:1, b:2, c:3\\}
```

`Object.assign`方法的第一个参数是目标对象，后面的参数都是源对象。

> 注意，如果目标对象与源对象有同名属性，或多个源对象有同名属性，则后面的属性会覆盖前面的属性。

```javascript
const target = \\{ a: 1, b: 1 \\};

const source1 = \\{ b: 2, c: 2 \\};
const source2 = \\{ c: 3 \\};

Object.assign(target, source1, source2);
target // \\{a:1, b:2, c:3\\}
```



### JavaScript如何实现一个类（类的定义），怎么实例化这个类？

#### 构造函数法（this + prototype） -- 用 new 关键字 生成实例对象

缺点：用到了 this 和 prototype，编写复杂，可读性差

```javascript
  function Mobile(name, price)\\{
     this.name = name;//通过this，表明这是一个构造函数
     this.price = price;
   \\}
   Mobile.prototype.sell = function()\\{
      alert(this.name + "，售价 $" + this.price);
   \\}
   var iPhone7 = new Mobile("iPhone7", 1000);
   iPhone7.sell();
```

#### Object.create 法 -- 用 Object.create() 生成实例对象

缺点：不能实现私有属性和私有方法，实例对象之间也不能共享数据

```javascript
 var Person = \\{
     firstname: "Mark",
     lastname: "Yun",
     age: 25,
     introduce: function()\\{
         alert('I am ' + Person.firstname + ' ' + Person.lastname);
     \\}
 \\};

 var person = Object.create(Person);
 person.introduce();

 // Object.create 要求 IE9+，低版本浏览器可以自行部署：
 if (!Object.create) \\{
　   Object.create = function (o) \\{
　　　 function F() \\{\\}
　　　 F.prototype = o;
　　　 return new F();
　　\\};
　\\}
```

#### 极简主义法（消除 this 和 prototype） -- 调用 createNew() 得到实例对象

优点：容易理解，结构清晰优雅，符合传统的"面向对象编程"的构造

```javascript
 var Cat = \\{
   age: 3, // 共享数据 -- 定义在类对象内，createNew() 外
   createNew: function () \\{
     var cat = \\{\\};
     // var cat = Animal.createNew(); // 继承 Animal 类
     cat.name = "小咪";
     var sound = "喵喵喵"; // 私有属性--定义在 createNew() 内，输出对象外
     cat.makeSound = function () \\{
       alert(sound);  // 暴露私有属性
     \\};
     cat.changeAge = function(num)\\{
       Cat.age = num; // 修改共享数据
     \\};
     return cat; // 输出对象
   \\}
 \\};

 var cat = Cat.createNew();
 cat.makeSound();
```

#### ES6 语法糖 class -- 用 new 关键字 生成实例对象

类的实例化很简单，直接 `new` 出来即可。函数可以作为构造函数来使用，通过 new 来实例化，其实函数本身也是一个对象。

```javascript
     class Point \\{
       constructor(x, y) \\{
         this.x = x;//可以在构造函数里写属性
         this.y = y;
       \\}
       toString() \\{
         return '(' + this.x + ', ' + this.y + ')';
       \\}
     \\}

  var point = new Point(2, 3);
```



### 谈谈This对象的理解

- this总是指向函数的直接调用者（而非间接调用者），指向调用上下文；
- 如果有new关键字，this指向new出来的那个对象；
- 在事件中，this指向触发这个事件的对象，特殊的是，IE中的attachEvent（触发事件）中的this总是指向全局对象Window



### this相关(注意箭头函数的this指向问题)

ES6中箭头函数的this问题：

ES6 允许使用“箭头”（=>）定义函数， 函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象。

this对象的指向是可变的，但是在箭头函数中，它是固定的，**箭头函数根本没有自己的this，导致内部的this就是外层代码块的this。**

所以箭头函数不能做构造函数， 也不能用call()、apply()、bind()这些方法去改变this的指向。



## 对象

> 对象是引用数据类型，是属性的无序集合
>
> 对象的组成：属性和方法

### 创建对象

* 隐式创建

  ```js 
  var obj = \\{
    ：
  \\}
  ```

* 实例化构造函数

  ```js
  var obj = new Object(\\{
    ：
  \\});
  ```

  

* 实例化自定义函数

  ```js
  function Animal()\\{
    this .
  \\}
  var obj = new Animal()
  ```

* 实例化类

  ```
  class Ani\\{
    this.
  \\}
  var obj = new Ani\\{\\};
  ```


### 对象的增删改查

* 增

  * 声明的同时赋值

  ```js
  //1.隐式
  var cup=\\{
       color:'red',
       size:'1000ml',
       price:588
   \\}
   console.log(cup);
  
  //2.实例化构造函数
  var cat = new Object(\\{
      age:2,
      weight:'10kg',
  \\})
  console.log(cat); 
  //3.实例化自定义构造函数
  function Person()\\{
      this.name='常博';
      this.sex='男';
      this.age=25;
      this.eat = (function()\\{
          return 'bread'
      \\})()
  \\}
  var $chang = new Person();
  console.log($chang);
  
  
  
  ```

* 先声明后赋值

```js
 //对象.属性名=方法
//1.隐式
var flower =\\{\\};
flower.color="red";
flower.type='玫瑰';
flower.price='1元'
console.log(flower);
flower.total=function()\\{
    return 999;
\\}
console.log(flower);
```

* 查

  * 访问属性

    ```js
    //对象的访问
    // 对象.属性名
    console.log(flower.type);
    //对象["属性名"]
    console.log(flower['type']);
    ```

  * 访问方法

  ```js
  //属性名.方法()
  console.log(flower.total());
  //属性名["方法"]()
  console.log(flower['total']());
  ```

* 改

  * 修改属性

    ```js
    // 对象.属性名=新的属性值
    flower.color="pink";
    flower['price'] = "2元"
    
    console.log(flower.color);
    console.log(flower['price']);
    
    console.log(flower);
    ```

  * 修改方法

    ```js
    //对象.方法=新的方法
    flower.total=function()\\{
        return 10
    \\}
    console.log(flower.total());
    
    flower['total'] = function()\\{
        return 99
    \\}
    console.log(flower["total"]());
    ```

* 删

  * 删除属性

    ```js
    delete flower.type;
    delete flower['price'];
    console.log(flower);
    ```

  * 删除方法

    ```js
    delete flower.total;
    console.log(flower);
    ```

  * 销毁对象

    ```js
    flower =null;
    console.log(flower);
    ```

### 对象遍历

* for ... in

  ```js
  // Object.keys(obj) 返回一个给定对象自身可枚举属性组成的数组。
  Object.keys(obj).length
  
  
  var changbo = \\{
      name:"常博",
      age:"3岁",
      sex:"未知",
      eat:"面",
      play : function()\\{
          return "王者"
      \\}
  \\}
  for ( var i in changbo)\\{
      console.log(changbo[i]);
  
  \\}
  ```

### 对象拷贝

* 浅拷贝：直接拷贝对象的内存地址，如果原地址中的对象被改变，浅拷贝拷贝出来的对象会相应改变

  只是增加了一个指针指向已存在的内存地址；

  * 直接赋值
  * `Object.assign(obj)`

* 深拷贝：在内存中新开辟一块内存，将对象中的所有属性值全部赋值，深拷贝出来的对象不会影响之前的对象

  增加了一个指针并且申请了一个新的内存，使这个指向新的内存。

  * `Object.assign(\\{\\}，obj)`   不兼容低版本   ES6的内容只有 一层的时候就是深拷贝  如果第二层有引用类型的话则是浅拷贝 

  * `JSON.stringify()` 将对象转换为字符串然后采用      `JSON.parse`转换成对象

    **注意：如果对象中存在函数/方法，那么该方法会丢失**

    ```js
    var obj=\\{
      name:"张三"
    \\}
    var obj2=JSON.parse(JSON.stringify(obj)) ;
    ```

  * 采用递归遍历，逐层拷贝

  ```js
function fun(o)\\{
      let s;
    	//检测是否是一个数组
    	//o instanceof Array
    	//Array.isArray(o)
      if(o instanceof Array)\\{
        s = [];
      \\}else if(typeof o == 'object')\\{
        s =\\{\\}
      \\}else\\{
        return o;
      \\}
    //遍历 判断是否对象中存在对象  有对象就递归函数 没有就直接赋值
      for(var i in o)\\{
        if(typeof o[i] == 'object')\\{
          debugger  //调试
          s[i] = fun(o[i])
        \\}else\\{
          console.log(7789);
          s[i] = o[i];
        \\}
      \\}
      return s   
    \\}
  console.log(fun(chang));
  ```
  
  

补充：

* `let str =  JSON.stringify(obj)`将对象转换成字符串
* `let obj=JSON.parse(str)`  将字符串转换成对象

### 对象特性

### 封装

* 工厂函数（不建议使用）

  ```js
  //工厂函数  不建议使用
  function person()\\{
    var obj=\\{
      name:"张三",
      age:'50岁',
      play:function()\\{
        return  1
      \\}
    \\}
    return obj   
  \\}
  console.log(person());
  ```

* 构造函数

  ```js	
  //构造函数  大写
  function Fruit()\\{
    this.name='西瓜';
    this.size='15斤';
    this.price='15块'
  \\}
  var watermelon = new Fruit();
  console.log(watermelon); 
  ```

### 继承

> 在一个对象的基础上，创建一个新的对象，并且这个新对象可以访问原对象的属性和方法，这就是继承

#### 继承方式

构造函数构造的对象  new Child()

对象  的原型链__proto__指向构造函数的原型prototype

__proto__是对象的属性

prototype原型：函数

* 原型继承

  ```js
  function Father()\\{
    this.lastName="雷";
  \\}
  function Daughter()\\{
    this.name="婷"
  \\}
  //Daughter继承Father 同时实例化Father
  Daughter.prototype=new Father();
  
  let $daughter=new Daughter();
  console.log($daughter);
  console.log($daughter.lastName+$daughter.name);
  ```

* `call()`继承  立即执行

  ```js
  //继承的方式有两种
  //1.继承的单个方法（继承的是实例化之后的），参数是一逗号隔开
  实例化被继承的对象.方法.call(谁来继承实例化之后的对象，参数1，参数2....)
  
  
  //2.继承整个构造函数（继承的是构造函数）
  被继承的构造函数.call（谁来继承实例化之后的对象）
  
  
  this的指向：
  call：里面是谁来继承this就指向谁
  ```

  ```js
  function Father()\\{
    this.lastName="老王";
    this.work=function(num)\\{
      console.log('军人');
      console.log(num);
      return '999'
    \\}
  \\}
  function Son()\\{
    this.name="小白"
  \\}
  //实例化Father Son
  let $father = new Father();
  let $son = new Son()
  //继承单个方法   //call()会立即执行 并且输出
  $father.work.call($son,995);
  //继承整个 对象
  Father.call($son)
  console.log($son.work(995));
  console.log($son.lastName);
  ```

* `apply()` 继承 立即执行

  ```js
  //继承的方式有两种
  //1.继承的单个方法（继承的是实例化之后的），参数是一逗号隔开
  实例化被继承的对象.方法.apply(谁来继承实例化之后的对象，[参数1，参数2....])
  
  
  //2.继承整个构造函数（继承的是构造函数）
  被继承的构造函数.apply（谁来继承实例化之后的对象）
  
  
  this的指向：
  apply：里面是谁来继承this就指向谁
  ```

  ```js
  function Father()\\{
    this.lastName="老王";
    this.work=function(num)\\{
      console.log('军人');
      console.log(num);
      return '999'
  
    \\}
  \\}
  function Son()\\{
    this.name="小白"
  \\}
  //实例化Father Son
  let $father = new Father();
  let $son = new Son()
  //继承单个方法   //apply()会立即执行 并且输出
  $father.work.apply($son,[995]);
  //继承整个 对象
  Father.apply($son)
  console.log($son.work(995));
  console.log($son.lastName); 
  ```

* `bind()` 继承 不会立即执行 需要手动调用

  * 如果要立即输出在后面加个括号bind(谁来继承实例化之后的对象，参数1，参数2....)();

  ```js
  //继承的方式有两种
  //1.继承的单个方法（继承的是实例化之后的），参数是一逗号隔开
  实例化被继承的对象.方法.bind(谁来继承实例化之后的对象，参数1，参数2....)()
  
  
  //2.继承整个构造函数（继承的是构造函数）
  被继承的构造函数.bind（谁来继承：实例化之后的对象）()
  
  
  this的指向：
  bind：里面是谁来继承this就指向谁
  ```

  ```js
  function Father()\\{
    this.lastName="老王";
    this.work=function(num)\\{
      console.log('军人');
      console.log(num);
      return '999'
  
    \\}
  \\}
  function Son()\\{
    this.name="小白"
  \\}
  
  //实例化Father Son
  let $father = new Father();
  let $son = new Son()
  //继承单个方法   //bind()会立即执行 并且输出
  // $father.work.bind($son,995)();
  //继承整个 对象  切记括号
  Father.bind($son)();
  console.log($son.work(995));
  console.log($son.lastName);  
  ```

Function上的方法  函数原型上的方法   函数名.call()

函数原型的方法 call() apply()  bind()  所有的函数都有这三个方法

函数原型上的方法  

修改上下文   修改this  指向 

**call()和apply()的区别**    面试问题

```js
call传递参数是通过逗号隔开依次跟在后面
apply传参数是将所有参数放在一个数组中，哪怕只有一个参数
call和apply继承的方法都是立即执行
```

**call()和bind()的区别**   面试问题

```js
call是立即执行函数。bind会将方法先继承，需要的时候在调用
```

* ES6类继承：通过`extends`关键字实现类与类之间的继承，然后实例化子类，来实现继承

### 应用

——修改函数中  this 指向

——JavaScript中某些方法

Math.min.apply(null,arr)

### 原型

> 当我们在创建对象的时候会发现一些对象有一些共享的方法和属性，这些方法在每次创建的时候都会在内存进行保存，内存浪费非常严重，为了解决这个问题，我们使用原型，所谓原型，就是用于存储公共属性和方法的对象

**javaScript规定，每个函数都有一个`prototype`属性，指向一个对象**

### 原型链

> 当访问对象的属性或方法，该属性或方法会在对象本身调用，对象本身没有，那么去对象本身的构造函数调用 ，本身构造函数没有，那么去父类的构造函数调用、父类的原型...以此类推，直到寻找到Object、以及Object的原型null.最后属性不存在时会得到`undefined`,方法不存在会报错。



### this

> 被自动定义在所有函数的作用域，总是会指向一个对象

**this的指向在函数定义的时候确定不了，只有函数执行的时候才能确定this到底指向谁，实际上this 的最终执行的是那个调用它的对象**

* 在事件中，this指向事件源
* 在构造函数中this指向构造函数的实例对象
* 在js里面this指向window
* 如果在事件中调用另一个函数，那么另一个函数this指向的是window,因为另一个函数是定义在window下面的
* 如果事件直接等于另一个函数，则另一个函数里面的this指向的是该事件的事件源
* es6箭头函数this指向不会改变

定时器可以阻断this的传播

可以使用  let  that=this；

**this绑定方式**

* call():谁来继承this就指向谁；
* apply():谁来继承this就指向谁；
* bind():谁来继承this就指向谁；



### null，undefined 的区别？

#### null

- 表示一个对象是“没有值”的值，也就是值为“空”；
- null的类型(typeof)是object；
- Javascript从来不会将变量设为null。它是用来让程序员表明某个用var声明的变量时没有值的

#### undefined

- 表示一个变量声明了没有初始化(赋值)；
- undefined不是一个有效的JSON，而null是；
- undefined的类型(typeof)是undefined；
- Javascript将未赋值的变量默认值设为undefined；

#### typeof undefined

- 是一个表示"无"的原始值或者说表示"缺少值"，就是此处应该有一个值，但是还没有定义。当尝试读取时会返回 undefined；
- 例如变量被声明了，但没有赋值时，就等于undefined

#### typeof null //"object"

- null : 是一个对象(空对象, 没有任何属性和方法)；
- 例如作为函数的参数，表示该函数的参数不是对象；

#### 注意：

在验证null时，一定要使用　=== ，因为 == 无法分别 null 和undefined

- null == undefined // true
- null === undefined // false



### 介绍js有哪些内置对象？

- Object 是 JavaScript 中所有对象的父对象
- 数据封装类对象：Object、Array、Boolean、Number 和 String
- 其他对象：Function、Arguments、Math、Date、RegExp、Error
- ES6新增对象：Symbol、Map、Set、Promises、Proxy、Reflect



### 列举一下JavaScript对象有哪些原生方法？

-  object.hasOwnProperty(prop);     
-  object.propertyIsEnumerable(prop);
-  object.valueOf();                 
-  object.toString();                
-  object.toLocaleString();          
-  Class.prototype.isPropertyOf(object);  
- Object.hasOwnProperty( ) 检查属性是否被继承
- Object.isPrototypeOf( ) 一个对象是否是另一个对象的原型
- Object.propertyIsEnumerable( ) 是否可以通过 for/in 循环看到属性
- Object.toLocaleString( ) 返回对象的本地字符串表示
- Object.toString( ) 定义一个对象的字符串表示
- Object.valueOf( ) 指定对象的原始值



### 对象浅拷贝和深拷贝有什么区别

在 `JS` 中，除了基本数据类型，还存在对象、数组这种引用类型。
基本数据类型，拷贝是直接拷贝变量的值，而引用类型拷贝的其实是变量的地址。

```
let o1 = \\{a: 1\\}
let o2 = o1
```

在这种情况下，如果改变 `o1` 或 `o2` 其中一个值的话，另一个也会变，因为它们都指向同一个地址。

```
o2.a = 3
console.log(o1.a) // 3
```

而浅拷贝和深拷贝就是在这个基础之上做的区分

如果在拷贝这个对象的时候，只对基本数据类型进行了拷贝，而对引用数据类型只是进行了引用的传递，而没有重新创建一个新的对象，则认为是**浅拷贝**。

反之，在对引用数据类型进行拷贝的时候，创建了一个新的对象，并且复制其内的成员变量，则认为是**深拷贝**。



### 如何判断一个对象是否属于某个类？

```
// 使用instanceof （待完善）
   if(a instanceof Person)\\{
       alert('yes');
   \\}
```



### javascript 的本地对象，内置对象和宿主对象

- **本地对象**
  ECMA-262 把本地对象（native object）定义为“独立于宿主环境的 ECMAScript 实现提供的对象"。简单来说，本地对象就是 ECMA-262 定义的类（引用类型）。它们包括：Object、Function、Array、String、Boolean、Number、Date、RegExp、Error、EvalError、RangeError、ReferenceError、SyntaxError、TypeError、URIError
- **内置对象**
  JS中内置了17个对象，常用的是Array对象、Date对象、正则表达式对象、string对象、Global对象
- **宿主对象**
  由ECMAScript实现的宿主环境提供的对象，可以理解为：浏览器提供的对象。所有的BOM和DOM都是宿主对象。



### 原型的`constructor`属性

**问题：**已知A继承了B，B继承了C。怎么判断 a 是由A**直接生成**的实例，还是B直接生成的实例呢？还是C直接生成的实例呢？

> 分析：这就要用到原型的`constructor`属性了。

- `foo.__proto__.constructor === M`的结果为`true`，但是 `foo.__proto__.constructor === Object`的结果为`false`。
- 所以，用 `consturctor`判断就比用 `instanceof`判断，更为严谨。



###  对象的几种创建方式

> javascript创建对象简单的说,无非就是用内置对象或各种自定义对象，当然还可以用JSON；但写法有很多种，也能混合使用

#### 第一种：内置对象Object 创建

```
var wcDog =new Object();
     wcDog.name="旺财";
     wcDog.age=3;
     wcDog.work=function()\\{
       alert("我是"+wcDog.name+",汪汪汪......");
     \\}
     wcDog.work();
```

```js
var Person = new Object();
Person.name = "Nike";
Person.age = 29;
```

这行代码创建了 Object 引用类型的一个新实例，然后把实例保存在变量 Person 中。

#### 第二种：使用对象字面量表示法

```js
var Person = \\{\\}; //相当于 var Person = new Object();
var Person = \\{
	name: 'Nike';
	age: 29;
\\}
```

对象字面量是对象定义的一种简写形式，目的在于简化创建包含大量属性的对象的过程。也就是说，第一种和第二种方式创建对象的方法其实都是一样的，只是写法上的区别不同

在介绍第三种的创建方法之前，我们应该要明白为什么还要用别的方法来创建对象，也就是第一种，第二种方法的缺点所在：它们都是用了同一个接口创建很多对象，会产生大量的重复代码，就是如果你有 100 个对象，那你要输入 100 次很多相同的代码。那我们有什么方法来避免过多的重复代码呢，就是把创建对象的过程封装在函数体内，通过函数的调用直接生成对象。

#### 第三种：使用工厂模式创建对象

```js
function createPerson(name, age, job) \\{
  var o = new Object();
  o.name = name;
  o.age = age;
  o.job = job;
  o.sayName = function() \\{
    alert(this.name);
  \\};
  return o;
\\}
var person1 = createPerson("Nike", 29, "teacher");
var person2 = createPerson("Arvin", 20, "student");
```

在使用工厂模式创建对象的时候，我们都可以注意到，在 createPerson 函数中，返回的是一个对象。那么我们就无法判断返回的对象究竟是一个什么样的类型。于是就出现了第四种创建对象的模式。

#### 第四种:使用构造函数创建对象

```js
function Person(name, age, job) \\{
  this.name = name;
  this.age = age;
  this.job = job;
  this.sayName = function() \\{
    alert(this.name);
  \\};
\\}
var person1 = new Person("Nike", 29, "teacher");
var person2 = new Person("Arvin", 20, "student");
```

对比工厂模式，我们可以发现以下区别：

1.没有显示地创建对象

2.直接将属性和方法赋给了 this 对象

3.没有 return 语句

4.终于可以识别的对象的类型。对于检测对象类型，我们应该使用 instanceof 操作符，我们来进行自主检测：

```js
alert(person1 instanceof Object); //ture

alert(person1 instanceof Person); //ture

alert(person2 instanceof Object); //ture

alert(person2 instanceof Object); //ture
```

同时我们也应该明白，按照惯例，构造函数始终要应该以一个大写字母开头，而非构造函数则应该以一个小写字母开头。

那么构造函数确实挺好用的，但是它也有它的缺点：

就是每个方法都要在每个实例上重新创建一遍，方法指的就是我们在对象里面定义的函数。如果方法的数量很多，就会占用很多不必要的内存。于是出现了第五种创建对象的方法

#### 第五种：原型创建对象模式

```
function Dog()\\{\\}
Dog.prototype.name="旺财";
Dog.prototype.eat=function()\\{
	alert(this.name+"是个吃货");
\\}
var wangcai =new Dog();
wangcai.eat();
```

```js
function Person() \\{\\}
Person.prototype.name = "Nike";
Person.prototype.age = 20;
Person.prototype.jbo = "teacher";
Person.prototype.sayName = function() \\{
  alert(this.name);
\\};
var person1 = new Person();
person1.sayName();
```

使用原型创建对象的方式，可以让所有对象实例共享它所包含的属性和方法。

如果是使用原型创建对象模式，请看下面代码：

```js
function Person() \\{\\}
Person.prototype.name = "Nike";
Person.prototype.age = 20;
Person.prototype.jbo = "teacher";
Person.prototype.sayName = function() \\{
  alert(this.name);
\\};
var person1 = new Person();
var person2 = new Person();
person1.name = "Greg";
alert(person1.name); //'Greg' --来自实例
alert(person2.name); //'Nike' --来自原型
```

当为对象实例添加一个属性时，这个属性就会屏蔽原型对象中保存的同名属性。

这时候我们就可以使用构造函数模式与原型模式结合的方式，构造函数模式用于定义实例属性，而原型模式用于定义方法和共享的属性

#### 第六种：组合使用构造函数模式和原型模式

```js
function Person(name, age, job) \\{
	this.name = name;
	this.age = age;
	this.job = job;
\\}
Person.prototype = \\{
	constructor: Person,
	sayName: function() \\{
		alert(this.name);
	\\};
\\}
var person1 = new Person('Nike', 20, 'teacher');
```

```
 function Car(name,price)\\{
      this.name=name;
      this.price=price; 
    \\}
     Car.prototype.sell=function()\\{
       alert("我是"+this.name+"，我现在卖"+this.price+"万元");
      \\}
    var camry =new Car("凯美瑞",27);
    camry.sell(); 
```

- #### 用function来模拟无参的构造函数

```
 function Person()\\{\\}
 //定义一个function，如果使用new"实例化",该function可以看作是一个Class
    var person=new Person();
        person.name="Mark";
        person.age="25";
        person.work=function()\\{
        alert(person.name+" hello...");
    \\}
person.work();
```

- #### 用function来模拟参构造函数来实现（用this关键字定义构造的上下文属性）

```
function Pet(name,age,hobby)\\{
       this.name=name;//this作用域：当前对象
       this.age=age;
       this.hobby=hobby;
       this.eat=function()\\{
          alert("我叫"+this.name+",我喜欢"+this.hobby+",是个程序员");
       \\}
    \\}
    var maidou =new Pet("麦兜",25,"coding");//实例化、创建对象
    maidou.eat();//调用eat方法
```



### javascript创建对象的几种方式？

javascript创建对象简单的说,无非就是使用内置对象或各种自定义对象，当然还可以用JSON；但写法有很多种，也能混合使用

1、对象字面量的方式

- `person=\\{firstname:"Mark",lastname:"Yun",age:25,eyecolor:"black"\\};`

2、用function来模拟无参的构造函数

```
function Person()\\{\\}
//定义一个function，如果使用new"实例化",该function可以看作是一个Class
person.name="Mark";
var person=new Person();
person.age="25";
person.work=function()\\{
alert(person.name+" hello...");
\\}
person.work();
```

3、用function来模拟参构造函数来实现（用this关键字定义构造的上下文属性）

```
function Pet(name,age,hobby)\\{
   this.name=name;//this作用域：当前对象
   this.age=age;
   this.hobby=hobby;
   this.eat=function()\\{
      alert("我叫"+this.name+",我喜欢"+this.hobby+",是个程序员");
   \\}
\\}
var maidou =new Pet("麦兜",25,"coding");//实例化、创建对象
maidou.eat();//调用eat方法
```

4、用工厂方式来创建（内置对象）

```
var wcDog =new Object();
 wcDog.name="旺财";
 wcDog.age=3;
 wcDog.work=function()\\{
   alert("我是"+wcDog.name+",汪汪汪......");
 \\}
 wcDog.work();
```

5、用原型方式来创建

```
function Dog()\\{

 \\}
 Dog.prototype.name="旺财";
 Dog.prototype.eat=function()\\{
 	alert(this.name+"是个吃货");
 \\}
 var wangcai =new Dog();
 wangcai.eat();
```

6、用混合方式来创建

```
function Car(name,price)\\{
  this.name=name;
  this.price=price;
\\}
 Car.prototype.sell=function()\\{
   alert("我是"+this.name+"，我现在卖"+this.price+"万元");
  \\}
var camry =new Car("凯美瑞",27);
camry.sell();
```



### JavaScript Object对象的方法总结( ES5 与 ES6 )

### ES5中的方法

### Object 对象的静态方法

所谓“静态方法”，是指部署在`Object`对象自身的方法  ---（此句话摘自 阮一峰博客）

Object.keys()方法与Object.getOwnPropertyNames方法很相似，一般用来遍历对象的（属性名，索引），并返回一个数组，该数组成员都是对象自身的（不是继承的），区别在于Object.keys方法只返回可枚举的属性，Object.getOwnPropertyNames方法还能返回不可枚举的属性名

**1.Object.keys**

```
// 定义一个 Array 对象
let arr = ["a", "b", "c"];

// 定义一个 Object 对象
let obj = \\{ foo: "bar", baz: 42 \\}；

// 定义一个  类数组 对象 
let ArrayLike = \\{ 0 : "a", 1 : "b", 2 : "c"\\};

// 类数组 对象, 随机 key 排序 
let anObj = \\{ 100: 'a', 2: 'b', 7: 'c' \\}; 

/* getFoo 是个不可枚举的属性 */ 
var my_obj = Object.create(\\{\\}, \\{
     getFoo : \\{ value : function () \\{ return this.foo \\} \\}
 \\}
);
my_obj.foo = 1;

// 打印结果
console.log(Object.keys(arr));       // ['0', '1', '2']
console.log(Object.keys(obj));       // ["foo","baz"]
console.log(Object.keys(ArrayLike));     // ['0', '1', '2']
console.log(Object.keys(anObj));   // ['2', '7', '100']
console.log(Object.keys(my_obj)); // ['foo']
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

返回数组中的排序与for..in是一致的，区别在于for..in循环还可以枚举原型链上的属性

``**2.Object.getOwnPropertyNames**

```
// 定义一个数组
var arr = ["a", "b", "c"];

// 定义一个 类数组对象
var obj = \\{ 0: "a", 1: "b", 2: "c"\\};

//定义一个 不可枚举属性
var my_obj = Object.create(\\{\\}, \\{
  getFoo: \\{
    value: function() \\{ return this.foo; \\},
    enumerable: false
  \\}
\\});
my_obj.foo = 1;

// 打印结果
console.log(Object.getOwnPropertyNames(arr).sort()); // ["0", "1", "2", "length"]
console.log(Object.getOwnPropertyNames(obj).sort()); // ["0", "1", "2"]
console.log(Object.getOwnPropertyNames(my_obj).sort()); // ["foo", "getFoo"]
```

**3.对象属性相关的方法**

```
// 看此方法之前，我觉得应该先了解一下，对象的属性分为哪两种，插句题外话，O(∩_∩)O哈哈~
```

　　对象里目前存在的属性描述符有两种主要形式：***数据描述符*** 和 ***存取描述符\***。

　　　　数据描述符: 是一个具有值的属性，该值可能是可写的，也可能不是可写的。

　　　　访问器描述符: 是由getter-setter函数对描述的属性。描述符必须是这两种形式之一；不能同时是两者。

　　数据描述符和存取描述符均具有以下可选键值：

　　　　configurable: 当且仅当该属性的 configurable 为 true 时，该属性`描述符`才能够被改变，同时该属性也能从对应的对象上被删除。默认为 false。

　　　　enumerable: 当且仅当该属性的`enumerable`为`true`时，该属性才能够出现在对象的枚举属性中。默认为 false。

　　　　value: 该属性对应的值。可以是任何有效的 JavaScript 值（数值，对象，函数等）。默认为 undefined。

　　　　writable: 当且仅当该属性的`writable`为`true`时，`value`才能被赋值运算符改变。默认为 false。

　　　　getter: 一个给属性提供 getter 的方法，如果没有 getter 则为 `undefined`。该方法返回值被用作属性值。默认为 undefined。

　　　　setter: 一个给属性提供 setter 的方法，如果没有 setter 则为 `undefined`。该方法将接受唯一参数，并将该参数的新值分配给该属性。默认为 undefined。

- 　　　　注意：如果一个描述符同时设置value,writable,get和set关键字，它将被认为是一个数据描述符。如果一个描述符同时有value或writable和get或set关键字，将产生异常。

　　　　记住，这些选项不一定是自身属性，如果是继承来的也要考虑。为了确认保留这些默认值，你可能要在这之前冻结 [`Object.prototype`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/prototype)，明确指定所有的选项，或者将　[`__proto__`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/__proto__)属性指向[`null`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/null)。

　　**a).Object.getOwnPropertyDescriptor( obj, prop) 返回一个指定对象上的自有属性对应的属性描述 （自由属性指，直接赋值的属性，不需要从原型上查找的属性）**

　　　参数:

　　　　obj 需要查找的目标对象

　　　　prop 目标对象内的属性名称

```
let o = \\{ get foo() \\{ return 17; \\} \\};
let d = Object.getOwnPropertyDescriptor(o, "foo");

let o1 = \\{ bar: 42 \\};
let d1 = Object.getOwnPropertyDescriptor(o1, "bar");

let o2 = \\{\\};
Object.defineProperty(o2, "baz", \\{
    value: 8675309,
    writable: false,
    enumerable: false
\\});
let d2 = Object.getOwnPropertyDescriptor(o2, "baz");
console.log(d)// \\{configurable: true, enumerable: true, get: [Function: get foo],set: undefined\\}
console.log(d1)//\\{configurable: true, enumerable: true, value: 42, writable: true\\}
console.log(d2)// \\{value: 8675309, writable: false, enumerable: false, configurable: false\\}
```

注意事项：ES5第一个参数不是对象，就会产生TypeError, ES2015第一个参数不是对象的话，就会被强制转换成对象

　　**b).Object.defineProperty( obj, prop, decriptor) 直接在一个对象上定义一个新属性，或修改一个对象的现有属性，并返回这个对象，默认情况下使用此方法添加的属性值是不能被修改的**

　　参数：

　　　　obj 要在其上定义属性的对象

　　　　prop 要定义或修改的属性名称

　　　　decriptor 将被定义或修改的属性描述符

```
var o = \\{\\}; // 创建一个新对象

// 在对象中添加一个属性与数据描述符的示例
Object.defineProperty(o, "a", \\{
    value : 37,
    writable : true,
    enumerable : true,
    configurable : true
\\});
// 对象o拥有了属性a，值为37

// 在对象中添加一个属性与存取描述符的示例
var bValue;
Object.defineProperty(o, "b", \\{
    get : function()\\{
        return bValue;
    \\},
    set : function(newValue)\\{
        bValue = newValue;
    \\},
    enumerable : true,
    configurable : true
\\});
o.b = 38;
// 对象o拥有了属性b，值为38

// o.b的值现在总是与bValue相同，除非重新定义o.b

// 数据描述符和存取描述符不能混合使用
Object.defineProperty(o, "conflict", \\{
    value: 0x9f91102,
    get: function() \\{
        return 0xdeadbeef;
    \\}
\\});
// TypeError: Invalid property descriptor. Cannot both specify accessors and a value or writable attribute(无效的属性描述符,不能同时指定访问器和值或可写属性)
```

　　c).Object.defineProperties()

　　d).Object.getOwnPropertyNames()

**4.控制对象状态的方法**

　　a).Object.preventExtensions() 防止对象扩展

　　b).Object.isExtensible() 判断对象是否可扩展

　　c).Object.seal() 禁止对象配置

　　d).Object.isSealed() 判断一个对象是否可配置

　　e).Object.freeze() 冻结一个对象

　　f).Object.isFrozen() 判断一个对象是否被冻结

**5.原型链相关方法**

　　a).Object.creat() 可以指定原型对象和属性，返回一个新的对象

　　b).Object.getPrototypeOf() 获取对的的Prototype对象



### Object对象的实例方法

除了`Object`对象本身的方法，还有不少方法是部署在`Object.prototype`对象上的，所有`Object`的实例对象都继承了这些方法。`Object`实例对象的方法，主要有以下六个。（此句摘自 --阮一峰 博客）

　　a). `valueOf()`返回当前对象对应的值

　　b). `toString()`返回当前对象对应的字符串形式,用来判断一个值的类型

　　c). `toLocaleString()`返回当前对象对应的本地字符串形式

　　d). `hasOwnProperty()`判断某个属性是否为当前对象自身的属性，还是继承自原型对象的属性

　　e). `isPrototypeOf()`判断当前对象是否为另一个对象的原型

　　f). `propertyIsEnumerable()`判断某个属性是否可枚举



###  ES6新增方法

(摘自 阮一峰ECMAScript 6 入门 )

**1.属性的简洁写法**

　　ES6 允许在对象之中，直接写变量。这时，属性名为变量名, 属性值为变量的值。

　　属性简写

```
function f(x, y) \\{
  return \\{x, y\\};
\\}
// 等同于
function f(x, y) \\{
  return \\{x: x, y: y\\};
\\}
f(1, 2) // Object \\{x: 1, y: 2\\}
```

　　方法名简写

```
const o = \\{
  method() \\{
    return "Hello!";
  \\}
\\};
// 等同于
const o = \\{
  method: function() \\{
    return "Hello!";
  \\}
\\};
```

　　属性简写与方法名简写，例：

```
let birth = '2000/01/01';
const Person = \\{
  name: '张三',
  //等同于birth: birth
  birth,
  // 等同于hello: function ()...
  hello() \\{ console.log('我的名字是', this.name); \\}
\\};
```

　　CommonJS 模块输出一组变量，就非常合适使用简洁写法

```
let ms = \\{\\};
function getItem (key) \\{
  return key in ms ? ms[key] : null;
\\}
function setItem (key, value) \\{
  ms[key] = value;
\\}
module.exports = \\{ getItem, setItem \\};
// 等同于
module.exports = \\{
  getItem: getItem,
  setItem: setItem
\\};
```

　　属性的赋值器（setter）和取值器（getter），事实上也是采用这种写法

```
const cart = \\{
  _wheels: 4,
  get wheels () \\{
    return this._wheels;
  \\},
  set wheels (value) \\{
    if (value < this._wheels) \\{
      throw new Error('数值太小了！');
    \\}
    this._wheels = value;
  \\}
\\}
```

**2.属性名表达式**

　　方法一，是直接用标识符作为属性名

　　方法二，是用表达式作为属性名，这时要将表达式放在方括号之内。

```
// 方法一
obj.foo = true;
// 方法二
obj['a' + 'bc'] = 123;
```

　　表达式还可以用做方法名

```
let obj = \\{
  ['h' + 'ello']() \\{
    return 'hi';
  \\}
\\};
obj.hello() // hi
```

　　注意，属性名表达式与简洁表示法，不能同时使用，会报错。

```
// 报错
const foo = 'bar';
const bar = 'abc';
const baz = \\{ [foo] \\};

// 正确
const foo = 'bar';
const baz = \\{ [foo]: 'abc'\\};
```

　　注意，属性名表达式如果是一个对象，默认情况下会自动将对象转为字符串`[object Object]`，这一点要特别小心。

```
const keyA = \\{a: 1\\};
const keyB = \\{b: 2\\};

const myObject = \\{
  [keyA]: 'valueA',
  [keyB]: 'valueB'
\\};

myObject // Object \\{[object Object]: "valueB"\\}
```

　　上面代码中，`[keyA]`和`[keyB]`得到的都是`[object Object]`，所以`[keyB]`会把`[keyA]`覆盖掉，而`myObject`最后只有一个`[object Object]`属性。

**3.方法的 name 属性**

　　如果对象的方法使用了取值函数（`getter`）和存值函数（`setter`），则`name`属性不是在该方法上面，而是该方法的属性的描述对象的`get`和`set`属性上面，返回值是方法名前加上`get`和`set`。

**4.Object.is() 它用来比较两个值是否严格相等，与严格比较运算符（===）的行为基本一致**

　　ES5 比较两个值是否相等，只有两个运算符：相等运算符（`==`）和严格相等运算符（`===`）。它们都有缺点，前者会自动转换数据类型，后者的`NaN`不等于自身，以及`+0`等于`-0`。JavaScript 缺乏一种运算，在所有环境中，只要两个值是一样的，它们就应该相等。

```
Object.is('foo', 'foo')
// true
Object.is(\\{\\}, \\{\\})
// false
```

　　不同之处只有两个：一是`+0`不等于`-0`，二是`NaN`等于自身。

```
+0 === -0 //true
NaN === NaN // false

Object.is(+0, -0) // false
Object.is(NaN, NaN) // true
```

　　ES5 可以通过下面的代码，部署`Object.is`。

```
Object.defineProperty(Object, 'is', \\{
  value: function(x, y) \\{
    if (x === y) \\{
      // 针对+0 不等于 -0的情况
      return x !== 0 || 1 / x === 1 / y;
    \\}
    // 针对NaN的情况
    return x !== x && y !== y;
  \\},
  configurable: true,
  enumerable: false,
  writable: true
\\});
```

5.Object.assign( target, source, source1 ) 方法用于对象的合并，将源对象（source）的所有可枚举属性，复制到目标对象（target）。拷贝的属性是有限制的，只拷贝源对象的自身属性（不拷贝继承属性），也不拷贝不可枚举的属性（`enumerable: false`）

　　参数

　　　　target 目标对象

　　　　source 源对象

```
const target = \\{ a: 1, b: 1 \\};

const source1 = \\{ b: 2, c: 2 \\};
const source2 = \\{ c: 3 \\};

Object.assign(target, source1, source2);
target // \\{a:1, b:2, c:3\\}
```

　　注意，如果目标对象与源对象有同名属性，或多个源对象有同名属性，则后面的属性会覆盖前面的属性。

```
let obj = \\{a: 1\\};
Object.assign(obj, undefined) === obj // true
Object.assign(obj, null) === obj /
```

　　如果非对象参数出现在源对象的位置（即非首参数），那么处理规则有所不同。首先，这些参数都会转成对象，如果无法转成对象，就会跳过。这意味着，如果`undefined`和`null`不在首参数，就不会报错。

**注意：**

`　　**a). Object.assign**`**方法实行的是浅拷贝，而不是深拷贝。也就是说，如果源对象某个属性的值是对象，那么目标对象拷贝得到的是这个对象的引用。**

```
const obj1 = \\{a: \\{b: 1}};
const obj2 = Object.assign(\\{\\}, obj1);

obj1.a.b = 2;
console.log(obj2.a.b) //2
obj2.a.b = 3
console.log(obj1.a.b) //3
```

　　上面代码中，源对象`obj1`的`a`属性的值是一个对象，`Object.assign`拷贝得到的是这个对象的引用。这个对象的任何变化，都会反映到目标对象上面。

 　**b). 数组的处理**

```
Object.assign([1, 2, 3], [4, 5])// [4, 5, 3]
```

　　上面代码中，`Object.assign`把数组视为属性名为 0、1、2 的对象，因此源数组的 0 号属性`4`覆盖了目标数组的 0 号属性`1`。

**常见用途**

　　**a). 为对象添加属性**

```
class Point \\{
  constructor(x, y) \\{
    Object.assign(this, \\{x, y\\});
  \\}
\\}
```

　　上面方法通过`Object.assign`方法，将`x`属性和`y`属性添加到`Point`类的对象实例。　

　　**b). 为对象添加方法**

```
Object.assign(SomeClass.prototype, \\{
  someMethod(arg1, arg2) \\{
    ···
  \\},
  anotherMethod() \\{
    ···
  \\}
\\});

// 等同于下面的写法
SomeClass.prototype.someMethod = function (arg1, arg2) \\{
  ···
\\};
SomeClass.prototype.anotherMethod = function () \\{
  ···
\\};
```

　　上面代码使用了对象属性的简洁表示法，直接将两个函数放在大括号中，再使用`assign`方法添加到`SomeClass.prototype`之中。

　　**c). 克隆对象**

```
function clone(origin) \\{
  return Object.assign(\\{\\}, origin);
\\}
```

　　上面代码将原始对象拷贝到一个空对象，就得到了原始对象的克隆。

　　不过，采用这种方法克隆，只能克隆原始对象自身的值，不能克隆它继承的值。如果想要保持继承链，可以采用下面的代码。

```
function clone(origin) \\{
  let originProto = Object.getPrototypeOf(origin);
  return Object.assign(Object.create(originProto), origin);
\\}
```

　　**d). 合并多个对象，将多个对象合并到某个对象。**

```
const merge = (target, ...sources) => Object.assign(target,...sources);

//如果希望合并后返回一个新对象，可以改写上面函数，对一个空对象合并。

const merge =(...sources) => Object.assign(\\{\\}, ...sources);
```

　　**e). 为属性指定默认值**

**6.属性的可枚举和可遍历**

　　可枚举性

　　对象的每个属性都有一个描述对象（Descriptor），用来控制该属性的行为。

　　a). `Object.getOwnPropertyDescriptor`方法可以获取该属性的描述对象。

```
let obj = \\{ foo: 123 \\};
Object.getOwnPropertyDescriptor(obj, 'foo')
//  \\{ value: 123, writable: true, enumerable: true, configurable: true \\}
```

　　目前，有四个操作会忽略`enumerable`为`false`的属性。

　　　　`for...in`循环：只遍历对象自身的和继承的可枚举的属性。

　　　　`Object.keys()`：返回对象自身的所有可枚举的属性的键名。

　　　　`JSON.stringify()`：只串行化对象自身的可枚举的属性。

　　　　`Object.assign()`： 忽略`enumerable`为`false`的属性，只拷贝对象自身的可枚举的属性。

　　**ES6 规定，所有 Class 的原型的方法都是不可枚举的。**

　　属性的遍历一共有5种：

　　　　`for...in`循环遍历对象自身的和继承的可枚举属性（不含 Symbol 属性）。

`　　　　Object.keys`返回一个数组，包括对象自身的（不含继承的）所有可枚举属性（不含 Symbol 属性）的键名。

`　　　　Object.getOwnPropertyNames`返回一个数组，包含对象自身的所有属性（不含 Symbol 属性，但是包括不可枚举属性）的键名。

`　　　　Object.getOwnPropertySymbols`返回一个数组，包含对象自身的所有 Symbol 属性的键名。

`　　　　Reflect.ownKeys`返回一个数组，包含对象自身的所有键名，不管键名是 Symbol 或字符串，也不管是否可枚举。





### JS操作对象属性（获取、添加、删除、修改对象属性）

属性也称为名值对，包括属性名和属性值。属性名可以是包含空字符串在内的任意字符串，一个对象中不能存在两个同名的属性。属性值可以是任意类型的数据。

### 定义属性

#### 1. 直接量定义

在对象直接量中，属性名与属性值之间通过冒号分隔，冒号左侧是属性名，右侧是属性值，名值对（属性）之间通过逗号分隔。

#### 示例1

在下面示例中，使用直接量方法定义对象 obj，然后添加了两个成员，一个是属性，另一个是方法。

```
var obj = \\{
    x : 1,
    y : function () \\{
        return this.x + this.x;
    \\}
\\}
```

#### 2. 点语法定义

#### 示例2

通过点语法，可以在构造函数内或者对象外添加属性。

```
var obj = \\{\\};
obj.x = 1;
obj.y = function () \\{
    return this.x + this.x;
\\}
```

#### 3. 使用 Object.defineProperty

使用 Object.defineProperty() 函数可以为对象添加属性，或者修改现有属性。如果指定的属性名在对象中不存在，则执行添加操作；如果在对象中存在同名属性，则执行修改操作。

具体用法如下：

Object.defineProperty(object, propertyname, descriptor);

参数说明如下：

- object：指定要添加或修改属性的对象，可以是 [JavaScript](http://c.biancheng.net/js/) 对象或者 DOM 对象。
- propertyname：表示属性名的字符串。
- descriptor：定义属性的描述符，包括对数据属性或访问器属性。


Object.defineProperty 返回值为已修改的对象。

#### 示例3

下面示例先定义一个对象直接量 obj，然后使用 Object.defineProperty() 函数为 obj 对象定义属性，属性名为 x，值为 1，可写、可枚举、可修改特性。

```
var obj = \\{\\};
Object.defineProperty(obj, "x", \\{
    value : 1,
    writable : true,
    enumerable : true,
    configurable : true
\\});
console.log(obj.x);  //1
```

#### 4. 使用 Object.defineProperties

使用 Object.defineProperties() 函数可以一次定义多个属性。具体用法如下：

object.defineProperties(object, descriptors);

参数说明如下：

- object：对其添加或修改属性的对象，可以是本地对象或 DOM 对象。
- descriptors：包含一个或多个描述符对象，每个描述符对象描述一个数据属性或访问器属性。

#### 示例4

在下面示例中，使用 Object.defineProperties() 函数将数据属性和访问器属性添加到对象 obj 上。

```
var obj = \\{\\};
Object.defineProperties(obj, \\{
    x : \\{  //定义属性x
        value : 1,
        writable : true,  //可写
    \\},
    y : \\{  //定义属性y
        set : function (x) \\{  //设置访问器属性
            this.x = x;  //改写obj对象的x属性的值
        \\},
        get : function () \\{  //设置访问器
            return this.x;
        \\},
    \\}
\\});
obj.y = 10;
console.log(obj.x);  //10
```



### 读写属性

#### 1. 使用点语法

使用点语法可以快速读写对象属性，点语法左侧是引用对象的变量，右侧是属性名。

#### 示例1

下面示例定义对象 obj，包含属性 x，然后使用点语法读取属性 x 的值。

```
var obj = \\{  //定义对象
    x : 1
\\}
console.log(obj.x);  //访问对象属性x，返回1
obj.x = 2;  //重写属性值
console.log(obj.x);  //访问对象属性x，返回2
```

#### 2. 使用中括号语法

从结构上分析，对象与数组相似，因此可以使用中括号来读写对象属性。

#### 示例2

针对上面示例，可以使用中括号来读写对象属性。

```
console.log(obj["x"]);  //2
obj["x"] = 3;  //重写属性值
console.log(obj["x"]);  //3
```

#### 【注意事项】

- 在中括号语法中，必须以字符串形式指定属性名，不能使用标识符。
- 中括号内可以使用字符串，也可以使用字符型表达式，即只要表达式的值为字符串即可。

#### 示例3

下面示例使用 for/in 遍历对象的可枚举属性，并读取它们的值，然后重写属性值。

```
for (var i in obj) \\{
    console.log(obj[i]);
    obj[i] = obj[i] + obj[i];
    console.log(obj[i]);
\\}
```

在上面代码中，中括号中的表达式 i 是一个变量，其返回值为 for/in 遍历对象时枚举的每个属性名。

#### 3. 使用 Object.getOwnPropertyNames

使用 Object.getOwnPropertyNames() 函数能够返回指定对象私有属性的名称。私有属性是指用户在本地定义的属性，而不是继承的原型属性。具体用法如下：

Object.getOwnPropertyNames(object);

参数 object 表示一个对象，返回值为一个数组，其中包含所有私有属性的名称。其中包括可枚举的和不可枚举的属性和方法的名称。如果仅返回可枚举的属性和方法的名称，应该使用 Object.keys() 函数。

#### 示例4

在下面示例中定义一个对象，该对象包含三个属性，然后使用 getOwnPropertyNames 获取该对象的私有属性名称。

```
var obj = \\{x : 1, y : 2, z : 3\\};
var arr = Object.getOwnPropertyNames(obj);
console.log(arr);  //返回属性名：x,yz
```

#### 4. 使用 Object.keys

使用 Object.keys() 函数仅能获取可枚举的私有属性名称。具体用法如下：

Object.keys(object);

参数 object 表示指定的对象，可以是 [Java](http://c.biancheng.net/java/)Script 对象或 DOM 对象。返回值是一个数组，其中包含对象的可枚举属性名称。

#### 5. Object.getOwnPropertyDescriptor

使用 Object.getOwnPropertyDescriptor() 函数能够获取对象属性的描述符。具体用法如下：

Object.getOwnPropertyDescriptor(object, propertyname);

参数 object 表示指定的对象，propertyname 表示属性的名称。返回值为属性的描述符对象。

#### 示例5

在下面示例中定义一个对象 obj，包含 3 个属性，然后使用 Object.getOwnPropertyDescriptor() 函数获取属性 x 的数据属性描述符，并使用该描述符将属性 x 设置为只读。最后，调用 Object.defineProperty() 函数，使用数据属性描述符修改属性 x 的特性。遍历修改后的对象，可以发现只读属性 writable 为 false。

```
var obj = \\{x : 1, y : 2, z : 3\\};  //定义对象
var des = Object.getOwnPropertyDescriptor(obj, "x");  //获取属性x的数据属性描述符
for (var prop in des) \\{  //遍历属性描述符对象
    console.log(prop + ':' + des[prop]);  //显示特性值
\\}
des.writable = false;  //重写特性，不允许修改属性
des.value = 100;  //重写属性值
Object.defineProperty(obj, "x", des);  //使用修改后的数据属性描述符覆盖属性x
var des = Object.getOwnPropertyDescriptor(obj, "x");  //重新获取属性x的数据属性描述符
for (var prop in des) \\{  //遍历属性描述符对象
    console.log(prop + ':' + des[prop]);  //显示特性值
\\}
```

一旦为未命名的属性赋值后，对象就会自动定义该属性的名称，在任何时候和位置为该属性赋值，都不需要定义属性，而只会重新设置它的值。如果读取未定义的属性，则返回值都是 undefined。



### 删除属性

使用 delete 运算符可以删除对象的属性。

#### 示例

下面示例使用 delete 运算符删除指定属性。

```
var obj = \\{x : 1\\};  //定义对象
delete obj.x;  //删除对象的属性x
console.log(obj.x);  //返回undefined
```

当删除对象属性之后，不是将该属性值设置为 undefined，而是从对象中彻底清除属性。如果使用 for/in 语句枚举对象属性，只能枚举属性值为 undefined 的属性，但不会枚举已删除属性。

### 使用方法

方法也是函数，当函数被赋值给对象的属性，就被称为方法。方法的使用与函数是相同的，唯一的不同点是在方法内常用 this 引用调用对象，其实在普通函数内也有 this，只不过不常用。

使用点语法或中括号可以访问方法，使用小括号可以激活方法。

#### 示例1

与普通函数用法一样，可以在调用方法时传递参数，也可以设计返回值。

```
var obj = \\{\\};
obj.f = function (n) \\{  //定义对象的方法
    return 10 * n;
\\}
var n = obj.f(5);  //调用方法，设置参数为5
console.log(n);  //返回值50
```

#### 示例2

在方法内 this 总是指向当前调用对象。在下面示例中，当在不同运行环境中调用对象 obj 的方法 f() 时，该方法的 this 指向时不同的。

```
var obj = \\{  //定义对象
    f : function () \\{  //定义对象的方法
        console.log(this);  //访问当前对象
    \\}
\\}
obj.f();  //此时this指向对象obj
var f1 = obj.f;  //引用对象obj的方法f
f1();  //此时this指向对象window
```



### JavaScript中?. 和??分别是什么详解

在项目中我们往往要做很多很多的空值判断进行容错处理,往往伴随着三目运算、与或、if else来使用,下面这篇文章主要给大家介绍了关于JavaScript中?. 和??分别是什么 

`?. `和 `??` 是 JavaScript 中的两个新操作符，分别是可选链操作符（optional chaining operator）和空值合并操作符（nullish coalescing operator）。

#### ?. 操作符（可选链运算符）

 ?.   表示：可选链操作符( ?. )允许读取位于连接对象链深处的属性的值，而不必明确验证链中的每 个引用是否有效。操作符的功能类似于 . 链式操作符，不同之处在于，在引用为空(null 或者 undefined) 的情况下不会引起错误，该表达式短路返回值

判断对象的某个属性是否存在，如果存在那么就返回整个属性的值，否则返回undefined

 在javascript中如果一个值为null、undefined，直接访问下面的属性，会报 Uncaught TypeError: Cannot read properties of undefined 异常错误。

`?.` 可选链操作符用于访问可能为空或未定义的属性或方法，它允许我们安全地访问嵌套对象的属性，如果中间的属性为空或未定义，则不会抛出错误，而是返回 undefined。例如：

```
`const obj = \\{`` ``foo: \\{``  ``bar: 123`` ``\\}``\\};` `// 普通访问属性的方式``const x = obj.foo.bar; ``// x = 123` `// 使用可选链操作符``const y = obj?.foo?.bar; ``// y = 123` `// 如果对象未定义，则返回 undefined``const z = undefined?.foo?.bar; ``// z = undefined`
```

#### ?? 操作符（空值合并运算符）

??表示：只有左侧的值为 null 或 undefined 的时候才返回右侧的值 

?? 双问号后面是默认值（可常量、可变量）。

在 ?? 前面没有值的时候会默认 ?? 后边的值（类似于三目运算符中的:后面赋值）

![img](https://img-blog.csdnimg.cn/c6a7c7ecc4b34fbba34a9a3be576ae63.png)

`??` 空值合并操作符用于检查一个变量是否为 null 或 undefined，如果是，则返回一个默认值，否则返回该变量的值。与传统的逻辑运算符 `||` 不同，`??` 只会在左侧的值为 null 或 undefined 时返回右侧的默认值，对于其他假值（如空字符串、0、false 等）并不会返回默认值，而是会返回它本身。例如：

```
`const x = undefined ?? ``'default'``; ``// x = 'default'``const y = ``null` `?? ``'default'``; ``// y = 'default'``const z = ``'value'` `?? ``'default'``; ``// z = 'value'``const a = ``''` `?? ``'default'``; ``// a = ''``const b = ``''` `|| ``'default'``; ``// b = 'default'`
```

需要注意的是，`??` 操作符需要在 ES11 及以上的版本才能使用。

**和||运算符的区别：**

1. || 只会在左边的值为假值时返回右边的值 (0, '', undefined, null, false 等都为假值)

2. ?? 是在左边的值为undefined或者null时才会返回右边的值

![img](https://img.jbzj.com/file_images/article/202302/202322095947477.jpg?20231201007)

#### ??=（空值赋值运算符）

意思是只有当??=左侧的值为undefined、null时，才会把右侧的值赋给左侧，否则左侧不会被赋值

```
let a;
let b = '123';
let c = 'qwer'
a ??= b;// '123'
b ??= c;// '123'
```

举个🌰: 

 (1)这个时候存在detail然后去detail下查找cat属性，因为obj定义了cat所以返回huahua 

```
const obj = \\{
      name: 'ceshi',
      detail: \\{\\}
\\}
const name = obj.dog ?. name;
console.log(name) // undefined
const cat = obj.detail ?. cat ?? 'default name'
console.log(cat) // default name
```


(2)查找obj中detail属性下面name属性，但是对象中没有定义所以值是undefined，这个时候？？左侧是undefied那么久使用右侧的数据所以最终返回default name  

```
const obj = \\{
      name: 'ceshi',
      detail: \\{
        cat: 'huahua'
      \\}
    \\}
const name = obj.dog ?. name;
console.log(name) // undefined
const cat = obj.detail ?. cat ?? 'default name'
console.log(cat) // huahua
```



### 对象accountInfo: \\{\\}怎么判断为空vue3

在 Vue 3 中，如果你想要判断一个对象（例如 `accountInfo`）是否为空，你可以使用几种不同的方法。这里假设 `accountInfo` 是响应式数据的一部分，比如它是在 `setup()` 函数中通过 `ref` 或 `reactive` 定义的。

#### 使用 JavaScript 的原生方法

最直接的方法是使用 JavaScript 的原生方法来检查对象是否为空：

```javascript
// 假设 accountInfo 是通过 ref 定义的
const accountInfo = ref(\\{\\});

// 检查 accountInfo.value 是否为空
if (Object.keys(accountInfo.value).length === 0) \\{
  console.log('accountInfo is empty');
\\} else \\{
  console.log('accountInfo is not empty');
\\}

// 如果 accountInfo 是通过 reactive 定义的
const accountInfo = reactive(\\{\\});

// 检查 accountInfo 是否为空
if (Object.keys(accountInfo).length === 0) \\{
  console.log('accountInfo is empty');
\\} else \\{
  console.log('accountInfo is not empty');
\\}
```

#### 使用 lodash 库

如果你已经在项目中使用了 lodash 库，可以利用它的 `_.isEmpty` 方法来简化代码：

首先确保你已经安装了 lodash:

```bash
npm install lodash
```

然后可以在你的组件或逻辑中这样使用：

```javascript
import \\{ isEmpty \\} from 'lodash';

// 假设 accountInfo 是通过 ref 定义的
const accountInfo = ref(\\{\\});

// 检查 accountInfo.value 是否为空
if (isEmpty(accountInfo.value)) \\{
  console.log('accountInfo is empty');
\\} else \\{
  console.log('accountInfo is not empty');
\\}

// 如果 accountInfo 是通过 reactive 定义的
const accountInfo = reactive(\\{\\});

// 检查 accountInfo 是否为空
if (isEmpty(accountInfo)) \\{
  console.log('accountInfo is empty');
\\} else \\{
  console.log('accountInfo is not empty');
\\}
```

#### 在模板中使用

如果你想在 Vue 模板中根据 `accountInfo` 是否为空来显示不同的内容，可以直接使用 `v-if` 指令结合计算属性或者直接用内联表达式进行判断：

```vue
<template>
  <div v-if="isAccountInfoEmpty">
    Account Info is empty.
  </div>
  <div v-else>
    Account Info is not empty.
  </div>
</template>

<script setup>
import \\{ computed, ref \\} from 'vue';

const accountInfo = ref(\\{\\});
const isAccountInfoEmpty = computed(() => Object.keys(accountInfo.value).length === 0);
</script>
```

以上就是在 Vue 3 中判断一个对象是否为空的一些常见方式。选择哪种方式取决于你的具体需求和项目的依赖情况。