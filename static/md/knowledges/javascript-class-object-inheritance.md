---
title: JavaScript类、对象和继承
date: 2020-03-25 21:10:40
categories: 
- 前端知识
tags:
- JavaScript
- 继承
---
### Javascript如何实现继承？

继承的本质就是原型链。（这些问题必问的，其实就是考察你对原型链的掌握程度。）

- 构造函数绑定：使用 call 或 apply 方法，将父对象的构造函数绑定在子对象上

```javascript   　
function Cat(name,color)\\{
 　Animal.apply(this, arguments);
 　this.name = name;
 　this.color = color;
\\}
```

- 实例继承：将子对象的 prototype 指向父对象的一个实例     

```javascript
Cat.prototype = new Animal();
Cat.prototype.constructor = Cat;
```

- 拷贝继承：如果把父对象的所有属性和方法，拷贝进子对象

```javascript         　　
    function extend(Child, Parent) \\{
  　　　var p = Parent.prototype;
  　　　var c = Child.prototype;
  　　　for (var i in p) \\{
  　　　   c[i] = p[i];
  　　　\\}
  　　　c.uber = p;
  　 \\}
```

- 原型继承：将子对象的 prototype 指向父对象的 prototype      

```javascript
    function extend(Child, Parent) \\{
        var F = function()\\{\\};
      　F.prototype = Parent.prototype;
      　Child.prototype = new F();
      　Child.prototype.constructor = Child;
      　Child.uber = Parent.prototype;
    \\}
```

- ES6 语法糖 extends：class ColorPoint extends Point \\{\\}

```javascript
    class ColorPoint extends Point \\{
       constructor(x, y, color) \\{
          super(x, y); // 调用父类的constructor(x, y)
          this.color = color;
       \\}
       toString() \\{
          return this.color + ' ' + super.toString(); // 调用父类的toString()
       \\}
    \\}
```

- 原型prototype机制或apply和call方法去实现较简单，建议使用构造函数与原型混合方式

```
 function Parent()\\{
        this.name = 'wang';
    \\}

    function Child()\\{
        this.age = 28;
    \\}
    Child.prototype = new Parent();//继承了Parent，通过原型

    var demo = new Child();
    alert(demo.age);
    alert(demo.name);//得到被继承的属性
  \\}
```



### 类和继承（es5实现方法 + es6实现方法）

[继承机制](http://www.ruanyifeng.com/blog/2011/06/designing_ideas_of_inheritance_mechanism_in_javascript.html)

[ES6创建类的基本语法和继承实现原理](https://juejin.im/post/5ab31129f265da2378402cb3)

[ES5和ES6中对于继承的实现方法](https://www.jianshu.com/p/342966fdf816)



### JavaScript 继承方式和优缺点

#### 原型链继承

```js
function Parent () \\{
    this.name = 'kevin';
\\}

Parent.prototype.getName = function () \\{
    console.log(this.name);
\\}

function Child () \\{

\\}

Child.prototype = new Parent();

var child1 = new Child();

console.log(child1.getName()) // kevin
```

缺点：

1.引用类型的属性被所有实例共享，举个例子：

```js
function Parent () \\{
    this.names = ['kevin', 'daisy'];
\\}

function Child () \\{

\\}

Child.prototype = new Parent();

var child1 = new Child();

child1.names.push('yayu');

console.log(child1.names); // ["kevin", "daisy", "yayu"]

var child2 = new Child();

console.log(child2.names); // ["kevin", "daisy", "yayu"]
```

2.在创建 Child 的实例时，不能向Parent传参

3.字面量重写原型会中断关系，使用引用类型的原型

#### 借用构造函数(经典继承)

```js
function Parent () \\{
    this.names = ['kevin', 'daisy'];
\\}

function Child () \\{
    Parent.call(this);
\\}

var child1 = new Child();

child1.names.push('yayu');

console.log(child1.names); // ["kevin", "daisy", "yayu"]

var child2 = new Child();

console.log(child2.names); // ["kevin", "daisy"]
```

优点：

1.避免了引用类型的属性被所有实例共享

2.可以在 Child 中向 Parent 传参

举个例子：

```js
function Parent (name) \\{
    this.name = name;
\\}

function Child (name) \\{
    Parent.call(this, name);
\\}

var child1 = new Child('kevin');

console.log(child1.name); // kevin

var child2 = new Child('daisy');

console.log(child2.name); // daisy
```

缺点：

方法都在构造函数中定义，每次创建实例都会创建一遍方法。

没有原型，则复用无从谈起。

#### 组合继承

原型链继承和经典继承双剑合璧。

```js
function Parent (name) \\{
    this.name = name;
    this.colors = ['red', 'blue', 'green'];
\\}

Parent.prototype.getName = function () \\{
    console.log(this.name)
\\}

function Child (name, age) \\{

    Parent.call(this, name);
    
    this.age = age;

\\}

Child.prototype = new Parent();

var child1 = new Child('kevin', '18');

child1.colors.push('black');

console.log(child1.name); // kevin
console.log(child1.age); // 18
console.log(child1.colors); // ["red", "blue", "green", "black"]

var child2 = new Child('daisy', '20');

console.log(child2.name); // daisy
console.log(child2.age); // 20
console.log(child2.colors); // ["red", "blue", "green"]
```

优点：融合原型链继承和构造函数的优点，是 JavaScript 中最常用的继承模式。

其背后的思路是使用原型链实现对原型属性和方法的继承，而通过借用构造函数来实现对实例属性的继承。这样，既通过在原型上定义方法实现了函数复用，又保证每个实例都有它自己的属性。

#### 原型式继承

```js
function createObj(o) \\{
    function F()\\{\\}
    F.prototype = o;
    return new F();
\\}
```

就是 ES5 Object.create 的模拟实现，将传入的对象作为创建的对象的原型。

缺点：

包含引用类型的属性值始终都会共享相应的值，这点跟原型链继承一样。

```js
var person = \\{
    name: 'kevin',
    friends: ['daisy', 'kelly']
\\}

var person1 = createObj(person);
var person2 = createObj(person);

person1.name = 'person1';
console.log(person2.name); // kevin

person1.firends.push('taylor');
console.log(person2.friends); // ["daisy", "kelly", "taylor"]
```

注意：修改`person1.name`的值，`person2.name`的值并未发生改变，并不是因为`person1`和`person2`有独立的 name 值，而是因为`person1.name = 'person1'`，给`person1`添加了 name 值，并非修改了原型上的 name 值。

#### 寄生式继承

创建一个仅用于封装继承过程的函数，该函数在内部以某种形式来做增强对象，最后返回对象。

```js
function createObj (o) \\{
    var clone = object.create(o);
    clone.sayName = function () \\{
        console.log('hi');
    \\}
    return clone;
\\}
```

缺点：跟借用构造函数模式一样，每次创建对象都会创建一遍方法。

#### 寄生组合式继承

为了方便大家阅读，在这里重复一下组合继承的代码：

```js
function Parent (name) \\{
    this.name = name;
    this.colors = ['red', 'blue', 'green'];
\\}

Parent.prototype.getName = function () \\{
    console.log(this.name)
\\}

function Child (name, age) \\{
    Parent.call(this, name);
    this.age = age;
\\}

Child.prototype = new Parent();

var child1 = new Child('kevin', '18');

console.log(child1)
```

组合继承最大的缺点是会调用两次父构造函数。

一次是设置子类型实例的原型的时候：

```js
Child.prototype = new Parent();
```

一次在创建子类型实例的时候：

```js
var child1 = new Child('kevin', '18');

```

回想下 new 的模拟实现，其实在这句中，我们会执行：

```js
Parent.call(this, name);
```

在这里，我们又会调用了一次 Parent 构造函数。

所以，在这个例子中，如果我们打印 child1 对象，我们会发现 Child.prototype 和 child1 都有一个属性为`colors`，属性值为`['red', 'blue', 'green']`。

那么我们该如何精益求精，避免这一次重复调用呢？

如果我们不使用 Child.prototype = new Parent() ，而是间接的让 Child.prototype 访问到 Parent.prototype 呢？

看看如何实现：

```js
function Parent (name) \\{
    this.name = name;
    this.colors = ['red', 'blue', 'green'];
\\}

Parent.prototype.getName = function () \\{
    console.log(this.name)
\\}

function Child (name, age) \\{
    Parent.call(this, name);
    this.age = age;
\\}

// 关键的三步
var F = function () \\{\\};

F.prototype = Parent.prototype;

Child.prototype = new F();


var child1 = new Child('kevin', '18');

console.log(child1);
```

最后我们封装一下这个继承方法：

```js
function object(o) \\{
    function F() \\{\\}
    F.prototype = o;
    return new F();
\\}

function prototype(child, parent) \\{
    var prototype = object(parent.prototype);
    prototype.constructor = child;
    child.prototype = prototype;
\\}

// 当我们使用的时候：
prototype(Child, Parent);
```

优点：引用《JavaScript高级程序设计》中对寄生组合式继承的夸赞就是：

1.这种方式的高效率体现它只调用了一次 Parent 构造函数，并且因此避免了在 Parent.prototype 上面创建不必要的、多余的属性。

2.与此同时，原型链还能保持不变；

3.因此，还能够正常使用 instanceof 和 isPrototypeOf。

开发人员普遍认为寄生组合式继承是引用类型最理想的继承范式。



### class 类constructor的理解

​    1.类中的构造器不是必须写的，要对实例进行一些初始化的操作，如添加指定属性时才写
​    2.如果A类继承了B类，且A类中写了构造器，那么A类构造器中的super是必须要调用的。
​    3.类中所定义的方法，都是放在了类的原型对象上，供实例去使用
​    4.类的方法 放在了类的原型对象上，供实例使用



### 如何避免原型链上面的对象共享

避免对象共享可以参考经典的 extend()函数，很多前端框架都有封装的，就是用一个空函数当做中间变量



### javascript 中 this 的指向问题

- 全局环境、普通函数（非严格模式）指向 window
- 普通函数（严格模式）指向 undefined
- 函数作为对象方法及原型链指向的就是上一级的对象
- 构造函数指向构造的对象
- DOM 事件中指向触发事件的元素
- 箭头函数...

#### 1、全局环境

全局环境下，this 始终指向全局对象（window），无论是否严格模式；

```js
// 在浏览器中，全局对象为 window 对象：
console.log(this === window); // true

this.a = 37;
console.log(window.a); // 37

```

#### 2、函数上下文调用

2.1 普通函数

普通函数内部的 this 分两种情况，严格模式和非严格模式。

（1）非严格模式下，没有被上一级的对象所调用,this 默认指向全局对象 window。

```js
function f1() \\{
  return this;
\\}
f1() === window; // true
```

（2）严格模式下，this 指向 undefined。

```js
function f2() \\{
  "use strict"; // 这里是严格模式
  return this;
\\}
f2() === undefined; // true
```

2.2 函数作为对象的方法

（1）函数有被上一级的对象所调用，那么 this 指向的就是上一级的对象。

（2）多层嵌套的对象，内部方法的 this 指向离被调用函数最近的对象（window 也是对象，其内部对象调用方法的 this 指向内部对象， 而非 window）。

```js
//方式1
var o = \\{
  prop: 37,
  f: function() \\{
    return this.prop;
  \\}
\\};
//当 o.f()被调用时，函数内的this将绑定到o对象。
console.log(o.f()); // logs 37

//方式2
var o = \\{ prop: 37 \\};
function independent() \\{
  return this.prop;
\\}
//函数f作为o的成员方法调用
o.f = independent;
console.log(o.f()); // logs 37

//方式3
//this 的绑定只受最靠近的成员引用的影响
o.b = \\{ g: independent, prop: 42 \\};
console.log(o.b.g()); // 42
```

特殊例子

```js
// 例子1
var o = \\{
  a: 10,
  b: \\{
    // a:12,
    fn: function() \\{
      console.log(this.a); //undefined
      console.log(this); //\\{fn: ƒ\\}
    \\}
  \\}
\\};
o.b.fn();
// 例子2
var o = \\{
  a: 10,
  b: \\{
    a: 12,
    fn: function() \\{
      console.log(this.a); //undefined
      console.log(this); //window
    \\}
  \\}
\\};
var j = o.b.fn;
j();
// this永远指向的是最后调用它的对象，也就是看它执行的时候是谁调用的，例子2中虽然函数fn是被对象b所引用，但是在将fn赋值给变量j的时候并没有执行所以最终指向的是window，这和例子1是不一样的，例子1是直接执行了fn

```

2.3 原型链中的 this

（1）如果该方法存在于一个对象的原型链上，那么 this 指向的是调用这个方法的对象，就像该方法在对象上一样。

```js
var o = \\{
  f: function() \\{
    return this.a + this.b;
  \\}
\\};
var p = Object.create(o);
p.a = 1;
p.b = 4;

console.log(p.f()); // 5

```

上述例子中，对象 p 没有属于它自己的 f 属性，它的 f 属性继承自它的原型。当执行 p.f()时，会查找 p 的原型链，找到 f 函数并执行。因为 f 是作为 p 的方法调用的，所以函数中的 this 指向 p。

（2）相同的概念也适用于当函数在一个 getter 或者 setter 中被调用。用作 getter 或 setter 的函数都会把 this 绑定到设置或获取属性的对象。

（3）call()和 apply()方法：当函数通过 Function 对象的原型中继承的方法 call() 和 apply() 方法调用时， 其函数内部的 this 值可绑定到 call() & apply() 方法指定的第一个对象上， 如果第一个参数不是对象，JavaScript 内部会尝试将其转换成对象然后指向它。

```js
function add(c, d) \\{
  return this.a + this.b + c + d;
\\}
var o = \\{ a: 1, b: 3 \\};

add.call(o, 5, 7); // 1 + 3 + 5 + 7 = 16
add.apply(o, [10, 20]); // 1 + 3 + 10 + 20 = 34

function tt() \\{
  console.log(this);
\\}
// 第一个参数不是对象，JavaScript内部会尝试将其转换成对象然后指向它。
tt.call(5); // 内部转成 Number \\{[[PrimitiveValue]]: 5\\}
tt.call("asd"); // 内部转成 String \\{0: "a", 1: "s", 2: "d", length: 3, [[PrimitiveValue]]: "asd"\\}

```

（4）bind()方法：由 ES5 引入， 在 Function 的原型链上， Function.prototype.bind。通过 bind 方法绑定后， 函数将被永远绑定在其第一个参数对象上， 而无论其在什么情况下被调用。

```js
function f() \\{
  return this.a;
\\}

var g = f.bind(\\{ a: "azerty" \\});
console.log(g()); // azerty

var o = \\{ a: 37, f: f, g: g \\};
console.log(o.f(), o.g()); // 37, azerty

```

2.4 构造函数中的 this

当一个函数用作构造函数时（使用 new 关键字），它的 this 被绑定到正在构造的新对象。

构造器返回的默认值是 this 所指的那个对象，也可以手动返回其他的对象。

```js
function C() \\{
  this.a = 37;
\\}

var o = new C();
console.log(o.a); // 37
// 为什么this会指向o？首先new关键字会创建一个空的对象，然后会自动调用一个函数apply方法，将this指向这个空对象，这样的话函数内部的this就会被这个空的对象替代。

function C2() \\{
  this.a = 37;
  return \\{ a: 38 \\}; // 手动设置返回\\{a:38\\}对象
\\}

o = new C2();
console.log(o.a); // 38

```

特殊例子

当 this 碰到 return 时

```js
// 例子1
function fn() \\{
  this.user = "追梦子";
  return \\{\\};
\\}
var a = new fn();
console.log(a.user); //undefined
// 例子2
function fn() \\{
  this.user = "追梦子";
  return function() \\{\\};
\\}
var a = new fn();
console.log(a.user); //undefined
// 例子3
function fn() \\{
  this.user = "追梦子";
  return 1;
\\}
var a = new fn();
console.log(a.user); //追梦子
// 例子4
function fn() \\{
  this.user = "追梦子";
  return undefined;
\\}
var a = new fn();
console.log(a.user); //追梦子
// 例子5
function fn() \\{
  this.user = "追梦子";
  return undefined;
\\}
var a = new fn();
console.log(a); //fn \\{user: "追梦子"\\}
// 例子6
// 虽然null也是对象，但是在这里this还是指向那个函数的实例，因为null比较特殊
function fn() \\{
  this.user = "追梦子";
  return null;
\\}
var a = new fn();
console.log(a.user); //追梦子
// 总结：如果返回值是一个对象，那么this指向的就是那个返回的对象，如果返回值不是一个对象那么this还是指向函数的实例。

```

2.5 setTimeout & setInterval

（1）对于延时函数内部的回调函数的 this 指向全局对象 window；

（2）可以通过 bind()方法改变内部函数 this 指向。

```js
//默认情况下代码
function Person() \\{
  this.age = 0;
  setTimeout(function() \\{
    console.log(this);
  \\}, 3000);
\\}

var p = new Person(); //3秒后返回 window 对象
//通过bind绑定
function Person() \\{
  this.age = 0;
  setTimeout(
    function() \\{
      console.log(this);
    \\}.bind(this),
    3000
  );
\\}
var p = new Person(); //3秒后返回构造函数新生成的对象 Person\\{...\\}
```

#### 3、在 DOM 事件中

3.1 作为一个 DOM 事件处理函数

当函数被用作事件处理函数时，它的 this 指向触发事件的元素（针对 addEventListener 事件）。

```js
// 被调用时，将关联的元素变成蓝色
function bluify(e) \\{
  //this指向所点击元素
  console.log("this === e.currentTarget", this === e.currentTarget); // 总是 true
  // 当 currentTarget 和 target 是同一个对象时为 true
  console.log("this === e.target", this === e.target);
  this.style.backgroundColor = "#A5D9F3";
\\}

// 获取文档中的所有元素的列表
var elements = document.getElementsByTagName("*");

// 将bluify作为元素的点击监听函数，当元素被点击时，就会变成蓝色
for (var i = 0; i < elements.length; i++) \\{
  elements[i].addEventListener("click", bluify, false);
\\}
```

3.2 作为一个内联事件处理函数

（1）当代码被内联处理函数调用时，它的 this 指向监听器所在的 DOM 元素；

（2）当代码被包括在函数内部执行时，其 this 指向等同于 普通函数直接调用的情况，即在非严格模式指向全局对象 window，在严格模式指向 undefined：

```html
<button onclick="console.log(this)">show me</button>
<button onclick="(function () \\{console.log(this)\\})()">show inner this</button>
<button onclick="(function () \\{'use strict'; console.log(this)\\})()">
  use strict
</button>
```

```
// 控制台打印
<button onclick="console.log(this)">show me</button>
Window \\{postMessage: ƒ, blur: ƒ, focus: ƒ, close: ƒ, parent: Window, …\\}
undefined
```

#### 4.1 全局环境中

在全局代码中，箭头函数被设置为全局对象：

```js
var globalObject = this;
var foo = () => this;
console.log(foo() === globalObject); // true

```

4.2 this 捕获上下文

箭头函数没有自己的 this，而是使用箭头函数所在的作用域的 this，即指向箭头函数定义时（而不是运行时）所在的作用域。

```js
//1、箭头函数在函数内部，以非方法的方法使用
function Person() \\{
  this.age = 0;
  setInterval(() => \\{
    this.age++;
  \\}, 3000);
\\}
var p = new Person(); //Person\\{age: 0\\}

//普通函数作为内部函数
function Person() \\{
  this.age = 0;
  setInterval(function() \\{
    console.log(this);
    this.age++;
  \\}, 3000);
\\}
var p = new Person(); //Window\\{...\\}

```

4.2 this 捕获上下文

箭头函数没有自己的 this，而是使用箭头函数所在的作用域的 this，即指向箭头函数定义时（而不是运行时）所在的作用域。

```js
//1、箭头函数在函数内部，以非方法的方法使用
function Person() \\{
  this.age = 0;
  setInterval(() => \\{
    console.log(this);
    this.age++;
  \\}, 3000);
\\}
var p = new Person(); //Person\\{age: 0\\}

//普通函数作为内部函数
function Person() \\{
  this.age = 0;
  setInterval(function() \\{
    console.log(this);
    this.age++;
  \\}, 3000);
\\}
var p = new Person(); //Window\\{...\\}

```

在 setTimeout 中的 this 指向了构造函数新生成的对象，而普通函数指向了全局 window 对象。

4.3 箭头函数作为对象的方法使用

箭头函数作为对象的方法使用，指向全局 window 对象；而普通函数作为对象的方法使用，则指向调用的对象。

```js
var obj = \\{
  i: 10,
  b: () => console.log(this.i, this),
  c: function() \\{
    console.log(this.i, this);
  \\}
\\};
obj.b(); // undefined window\\{...\\}
obj.c(); // 10 Object \\{...\\}

```

4.4 箭头函数中，call()、apply()、bind()方法无效

```js
var adder = \\{
  base: 1,
  //对象的方法内部定义箭头函数，this是箭头函数所在的作用域的this，
  //而方法add的this指向adder对象，所以箭头函数的this也指向adder对象。
  add: function(a) \\{
    var f = v => v + this.base;
    return f(a);
  \\},
  //普通函数f1的this指向window
  add1: function() \\{
    var f1 = function() \\{
      console.log(this);
    \\};
    return f1();
  \\},
  addThruCall: function inFun(a) \\{
    var f = v => v + this.base;
    var b = \\{
      base: 2
    \\};

    return f.call(b, a);
  \\}
\\};

console.log(adder.add(1)); // 输出 2
adder.add1(); //输出全局对象 window\\{...\\}
console.log(adder.addThruCall(1)); // 仍然输出 2（而不是3，其内部的this并没有因为call() 而改变，其this值仍然为函数inFun的this值，指向对象adder

```

4.5 this 指向固定化

箭头函数可以让 this 指向固定化，这种特性很有利于封装回调函数

```js
var handler = \\{
  id: "123456",

  init: function() \\{
    document.addEventListener(
      "click",
      event => this.doSomething(event.type),
      false
    );
  \\},

  doSomething: function(type) \\{
    console.log("Handling " + type + " for " + this.id);
  \\}
\\};

```

上面代码的 init 方法中，使用了箭头函数，这导致这个箭头函数里面的 this，总是指向 handler 对象。如果不使用箭头函数则指向全局 document 对象。

4.6 箭头函数不适用场景

（1）箭头函数不适合定义对象的方法（方法内有 this），因为此时指向 window；

（2）需要动态 this 的时候，也不应使用箭头函数。

```js
//例1，this指向定义箭头函数所在的作用域，它位于对象cat内，但cat不能构成一个作用域，所以指向全局window，改成普通函数后this指向cat对象。
const cat = \\{
  lives: 9,
  jumps: () => \\{
    this.lives--;
  \\}
\\};

//例2，此时this也是指向window，不能动态监听button，改成普通函数后this指向按钮对象。
var button = document.getElementById("press");
button.addEventListener("click", () => \\{
  this.classList.toggle("on");
\\});
```

