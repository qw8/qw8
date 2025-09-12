---
title: JavaScript面试题
date: 2020-06-15 10:24:57
categories: 
- 前端面试
tags:
- JavaScript
- DOM
- BOM
---

### 1.undefined 和 null 有什么区别？

在理解`undefined`和`null`之间的差异之前，我们先来看看它们的相似类。

**它们属于 JavaScript 的 7 种基本类型。**

```
let primitiveTypes = ['string','number','null','undefined','boolean','symbol', 'bigint'];
```

它们是属于虚值，可以使用`Boolean(value)`或`!!value`将其转换为布尔值时，值为`false`。

```
console.log(!!null); // false
console.log(!!undefined); // false

console.log(Boolean(null)); // false
console.log(Boolean(undefined)); // false
```

接着来看看它们的区别。

`undefined`是未指定特定值的变量的默认值，或者没有显式返回值的函数，如：`console.log(1)`，还包括对象中不存在的属性，这些 JS 引擎都会为其分配 `undefined` 值。

```
let _thisIsUndefined;
const doNothing = () => \\{\\};
const someObj = \\{
  a : "ay",
  b : "bee",
  c : "si"
\\};

console.log(_thisIsUndefined); // undefined
console.log(doNothing()); // undefined
console.log(someObj["d"]); // undefined
```

`null`是**“不代表任何值的值”**。`null`是已明确定义给变量的值。在此示例中，当`fs.readFile`方法未引发错误时，我们将获得`null`值。

```
fs.readFile('path/to/file', (e,data) => \\{
   console.log(e); // 当没有错误发生时，打印 null
   if(e)\\{
     console.log(e);
   \\}
   console.log(data);
 \\});
```

在比较`null`和`undefined`时，我们使用`==`时得到`true`，使用`===`时得到`false`:

```
 console.log(null == undefined); // true
 console.log(null === undefined); // false
```



### 2. && 运算符能做什么

`&&` 也可以叫**逻辑与**，在其操作数中找到第一个虚值表达式并返回它，如果没有找到任何虚值表达式，则返回最后一个真值表达式。它采用短路来防止不必要的工作。

```
console.log(false && 1 && []); // false
console.log(" " && true && 5); // 5
```

**使用`if`语句**

```
const router: Router = Router();

router.get('/endpoint', (req: Request, res: Response) => \\{
   let conMobile: PoolConnection;
   try \\{
      //do some db operations
   \\} catch (e) \\{
   if (conMobile) \\{
    conMobile.release();
   \\}
  \\}
\\});
```

**使用`&&`操作符**

```
const router: Router = Router();

router.get('/endpoint', (req: Request, res: Response) => \\{
  let conMobile: PoolConnection;
  try \\{
     //do some db operations
  \\} catch (e) \\{
    conMobile && conMobile.release()
  \\}
\\});
```



### 3. || 运算符能做什么

`||`也叫或`逻辑或`，在其操作数中找到第一个真值表达式并返回它。这也使用了短路来防止不必要的工作。在支持 ES6 默认函数参数之前，它用于初始化函数中的默认参数值。

```
console.log(null || 1 || undefined); // 1

function logName(name) \\{
  var n = name || "Mark";
  console.log(n);
\\}

logName(); // "Mark"
```



### 4. 使用 + 或一元加运算符是将字符串转换为数字的最快方法吗？

根据MDN文档，`+`是将字符串转换为数字的最快方法，因为如果值已经是数字，它不会执行任何操作。



### 5. DOM 是什么？

**DOM** 代表**文档对象模型**，是 HTML 和 XML 文档的接口(API)。当浏览器第一次读取(解析)HTML文档时，它会创建一个大对象，一个基于 HTM L文档的非常大的对象，这就是**DOM**。它是一个从 HTML 文档中建模的树状结构。DOM 用于交互和修改DOM结构或特定元素或节点。

假设我们有这样的 HTML 结构：

```
<!DOCTYPE html>
<html lang="en">

<head>
   <meta charset="UTF-8">
   <meta name="viewport" content="width=device-width, initial-scale=1.0">
   <meta http-equiv="X-UA-Compatible" content="ie=edge">
   <title>Document Object Model</title>
</head>

<body>
   <div>
      <p>
         <span></span>
      </p>
      <label></label>
      <input>
   </div>
</body>

</html>
```

等价的**DOM**是这样的：

![图片](https://mmbiz.qpic.cn/mmbiz_png/LDPLltmNy57ianicNyt0G9GEGibARafiazZKV0Y332hOUmFjQYBIYcXTm37FgzYBmsCFpKKjqnY9fm9r6NMvQSib0rw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)![图片](https://mmbiz.qpic.cn/mmbiz_png/LDPLltmNy57ianicNyt0G9GEGibARafiazZKV0Y332hOUmFjQYBIYcXTm37FgzYBmsCFpKKjqnY9fm9r6NMvQSib0rw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

JS 中的`document`对象表示DOM。它为我们提供了许多方法，我们可以使用这些方法来选择元素来更新元素内容，等等。



### 6. 什么是事件传播?

当**事件**发生在**DOM**元素上时，该**事件**并不完全发生在那个元素上。在**“冒泡阶段”**中，事件冒泡或向上传播至父级，祖父母，祖父母或父级，直到到达`window`为止；而在**“捕获阶段”**中，事件从`window`开始向下触发元素 事件或`event.target`。

事件传播有三个阶段：

1. **捕获阶段**–事件从 `window` 开始，然后向下到每个元素，直到到达目标元素。
2. **目标阶段**–事件已达到目标元素。
3. **冒泡阶段**–事件从目标元素冒泡，然后上升到每个元素，直到到达 `window`。

![图片](https://mmbiz.qpic.cn/mmbiz_png/LDPLltmNy57ianicNyt0G9GEGibARafiazZKYwkJmmSmticQRSmsI0k78CTiaG6Ccia6eNRKS9usV3bO154uCLPep1DUQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)



### 7. 什么是事件冒泡？

当**事件**发生在**DOM**元素上时，该**事件**并不完全发生在那个元素上。在冒泡阶段，事件冒泡，或者事件发生在它的父代，祖父母，祖父母的父代，直到到达`window`为止。

假设有如下的 HTML 结构：

```
<div class="grandparent">
  <div class="parent">
    <div class="child">1</div>
  </div>
</div>
```

对应的 JS 代码:

```
function addEvent(el, event, callback, isCapture = false) \\{
  if (!el || !event || !callback || typeof callback !== 'function') return;
  if (typeof el === 'string') \\{
    el = document.querySelector(el);
  \\};
  el.addEventListener(event, callback, isCapture);
\\}

addEvent(document, 'DOMContentLoaded', () => \\{
  const child = document.querySelector('.child');
  const parent = document.querySelector('.parent');
  const grandparent = document.querySelector('.grandparent');

  addEvent(child, 'click', function (e) \\{
    console.log('child');
  \\});

  addEvent(parent, 'click', function (e) \\{
    console.log('parent');
  \\});

  addEvent(grandparent, 'click', function (e) \\{
    console.log('grandparent');
  \\});

  addEvent(document, 'click', function (e) \\{
    console.log('document');
  \\});

  addEvent('html', 'click', function (e) \\{
    console.log('html');
  \\})

  addEvent(window, 'click', function (e) \\{
    console.log('window');
  \\})

\\});
```

`addEventListener`方法具有第三个可选参数`useCapture`，其默认值为`false`，事件将在冒泡阶段中发生，如果为`true`，则事件将在捕获阶段中发生。如果单击`child`元素，它将分别在控制台上记录`child`，`parent`，`grandparent`，`html`，`document`和`window`，这就是事件冒泡。



### 8. 什么是事件捕获？

当事件发生在 **DOM** 元素上时，该事件并不完全发生在那个元素上。在捕获阶段，事件从`window`开始，一直到触发事件的元素。

假设有如下的 HTML 结构：

```
<div class="grandparent">
  <div class="parent">
    <div class="child">1</div>
  </div>
</div>
```

对应的 JS 代码:

```
function addEvent(el, event, callback, isCapture = false) \\{
  if (!el || !event || !callback || typeof callback !== 'function') return;
  if (typeof el === 'string') \\{
    el = document.querySelector(el);
  \\};
  el.addEventListener(event, callback, isCapture);
\\}

addEvent(document, 'DOMContentLoaded', () => \\{
  const child = document.querySelector('.child');
  const parent = document.querySelector('.parent');
  const grandparent = document.querySelector('.grandparent');

  addEvent(child, 'click', function (e) \\{
    console.log('child');
  \\});

  addEvent(parent, 'click', function (e) \\{
    console.log('parent');
  \\});

  addEvent(grandparent, 'click', function (e) \\{
    console.log('grandparent');
  \\});

  addEvent(document, 'click', function (e) \\{
    console.log('document');
  \\});

  addEvent('html', 'click', function (e) \\{
    console.log('html');
  \\})

  addEvent(window, 'click', function (e) \\{
    console.log('window');
  \\})

\\});
```

`addEventListener`方法具有第三个可选参数`useCapture`，其默认值为`false`，事件将在冒泡阶段中发生，如果为`true`，则事件将在捕获阶段中发生。如果单击`child`元素，它将分别在控制台上打印`window`，`document`，`html`，`grandparent`和`parent`，这就是**事件捕获**。



### 9. event.preventDefault() 和 event.stopPropagation()方法之间有什么区别？

`event.preventDefault()` 方法可防止元素的默认行为。如果在表单元素中使用，它将阻止其提交。如果在锚元素中使用，它将阻止其导航。如果在上下文菜单中使用，它将阻止其显示或显示。`event.stopPropagation()`方法用于阻止捕获和冒泡阶段中当前事件的进一步传播。



### 10. 如何知道是否在元素中使用了`event.preventDefault()`方法？

我们可以在事件对象中使用`event.defaultPrevented`属性。它返回一个布尔值用来表明是否在特定元素中调用了`event.preventDefault()`。



### 11. 为什么此代码 `obj.someprop.x` 会引发错误?

```
const obj = \\{\\};
console.log(obj.someprop.x);
```

显然，由于我们尝试访问`someprop`属性中的`x`属性，而 someprop 并没有在对象中，所以值为 `undefined`。记住对象本身不存在的属性，并且其原型的默认值为`undefined`。因为`undefined`没有属性`x`，所以试图访问将会报错。



### 12. 什么是 event.target ？

简单来说，`event.target`是发生事件的元素或触发事件的元素。

假设有如下的 HTML 结构：

```
<div onclick="clickFunc(event)" style="text-align: center;margin:15px;
border:1px solid red;border-radius:3px;">
    <div style="margin: 25px; border:1px solid royalblue;border-radius:3px;">
        <div style="margin:25px;border:1px solid skyblue;border-radius:3px;">
          <button style="margin:10px">
             Button
          </button>
        </div>
    </div>
 </div>
```

JS 代码如下：

```
function clickFunc(event) \\{
  console.log(event.target);
\\}
```

如果单击 `button`，即使我们将事件附加在最外面的`div`上，它也将打印 `button` 标签，因此我们可以得出结论`event.target`是触发事件的元素。



### 13. 什么是 event.currentTarget？？

`event.currentTarget`是我们在其上显式附加事件处理程序的元素。

假设有如下的 HTML 结构：

```
<div onclick="clickFunc(event)" style="text-align: center;margin:15px;
border:1px solid red;border-radius:3px;">
    <div style="margin: 25px; border:1px solid royalblue;border-radius:3px;">
        <div style="margin:25px;border:1px solid skyblue;border-radius:3px;">
          <button style="margin:10px">
             Button
          </button>
        </div>
    </div>
 </div>
```

JS 代码如下：

```
function clickFunc(event) \\{
  console.log(event.currentTarget);
\\}
```

如果单击 `button`，即使我们单击该 `button`，它也会打印最外面的`div`标签。在此示例中，我们可以得出结论，`event.currentTarget`是附加事件处理程序的元素。



### 14. == 和 === 有什么区别？

`==`用于一般比较，`===`用于严格比较，`==`在比较的时候可以转换数据类型`，===`严格比较，只要类型不匹配就返回`flase`。

先来看看 `==` 这兄弟：

强制是将值转换为另一种类型的过程。在这种情况下，`==`会执行隐式强制。在比较两个值之前，`==`需要执行一些规则。

假设我们要比较`x == y`的值。

1. 如果`x`和`y`的类型相同，则 JS 会换成`===`操作符进行比较。
2. 如果`x`为`null`, `y`为`undefined`，则返回`true`。
3. 如果`x`为`undefined`且`y`为`null`，则返回`true`。
4. 如果`x`的类型是`number`, `y`的类型是`string`，那么返回`x == toNumber(y)`。
5. 如果`x`的类型是`string`, `y`的类型是`number`，那么返回`toNumber(x) == y`。
6. 如果`x`为类型是`boolean`，则返回`toNumber(x)== y`。
7. 如果`y`为类型是`boolean`，则返回`x == toNumber(y)`。
8. 如果`x`是`string`、`symbol`或`number`，而`y`是`object`类型，则返回`x == toPrimitive(y)`。
9. 如果`x`是`object`，`y`是`string`，`symbol`则返回`toPrimitive(x) == y`。
10. 剩下的 返回 `false`

注意：`toPrimitive`首先在对象中使用`valueOf`方法，然后使用`toString`方法来获取该对象的原始值。

举个例子。

| x                 | y         | x == y |
| :---------------- | :-------- | :----- |
| 5                 | 5         | true   |
| 1                 | '1'       | true   |
| null              | undefined | true   |
| 0                 | false     | true   |
| '1,2'             | [1,2]     | true   |
| '[object Object]' | \\{\\}        | true   |

这些例子都返回`true`。

第一个示例符合`条件1`，因为`x`和`y`具有相同的类型和值。

第二个示例符合`条件4`，在比较之前将`y`转换为数字。

第三个例子符合`条件2`。

第四个例子符合`条件7`，因为`y`是`boolean`类型。

第五个示例符合`条件8`。使用`toString()`方法将数组转换为字符串，该方法返回`1,2`。

最后一个示例符合`条件8`。使用`toString()`方法将对象转换为字符串，该方法返回`[object Object]`。

| x                 | y         | x === y |
| :---------------- | :-------- | :------ |
| 5                 | 5         | true    |
| 1                 | '1'       | false   |
| null              | undefined | false   |
| 0                 | false     | false   |
| '1,2'             | [1,2]     | false   |
| '[object Object]' | \\{\\}        | false   |

如果使用`===`运算符，则第一个示例以外的所有比较将返回`false`，因为它们的类型不同，而第一个示例将返回`true`，因为两者的类型和值相同。

具体更多规则可以对参考我之前的文章：

我对 JS 中相等和全等操作符转化过程一直很迷惑，直到有了这份算法



### 15. 为什么在 JS 中比较两个相似的对象时返回 false？

先看下面的例子：

```
let a = \\{ a: 1 \\};
let b = \\{ a: 1 \\};
let c = a;

console.log(a === b); // 打印 false，即使它们有相同的属性
console.log(a === c); // true
```

JS 以不同的方式比较对象和基本类型。在基本类型中，JS 通过值对它们进行比较，而在对象中，JS 通过引用或存储变量的内存中的地址对它们进行比较。这就是为什么第一个`console.log`语句返回`false`，而第二个`console.log`语句返回`true`。`a`和`c`有相同的引用地址，而`a`和`b`没有。



### 16. !! 运算符能做什么？

`!!`运算符可以将右侧的值强制转换为布尔值，这也是将值转换为布尔值的一种简单方法。

```
console.log(!!null); // false
console.log(!!undefined); // false
console.log(!!''); // false
console.log(!!0); // false
console.log(!!NaN); // false
console.log(!!' '); // true
console.log(!!\\{\\}); // true
console.log(!![]); // true
console.log(!!1); // true
console.log(!![].length); // false
```



### 17. 如何在一行中计算多个表达式的值？

可以使用`逗号`运算符在一行中计算多个表达式。它从左到右求值，并返回右边最后一个项目或最后一个操作数的值。

```
let x = 5;

x = (x++ , x = addFive(x), x *= 2, x -= 5, x += 10);

function addFive(num) \\{
  return num + 5;
\\}
```

上面的结果最后得到`x`的值为`27`。首先，我们将`x`的值增加到`6`，然后调用函数`addFive(6)`并将`6`作为参数传递并将结果重新分配给`x`，此时`x`的值为`11`。之后，将`x`的当前值乘以`2`并将其分配给`x`，`x`的更新值为`22`。然后，将`x`的当前值减去`5`并将结果分配给`x` `x`更新后的值为`17`。最后，我们将`x`的值增加`10`，然后将更新的值分配给`x`，最终`x`的值为`27`。



### 18. 什么是提升？

**提升**是用来描述变量和函数移动到其(全局或函数)作用域顶部的术语。

为了理解提升，需要来了解一下**执行上下文**。**执行上下文**是当前正在执行的**“代码环境”**。执行上下文有两个阶段:`编译`和`执行`。

**编译**-在此阶段，JS 引荐获取所有**函数声明**并将其**提升**到其作用域的顶部，以便我们稍后可以引用它们并获取所有变量声明（使用`var`关键字进行声明），还会为它们提供默认值：`undefined`。

**执行**——在这个阶段中，它将值赋给之前提升的变量，并执行或调用函数(对象中的方法)。

**注意:**只有使用`var`声明的变量，或者函数声明才会被提升，相反，函数表达式或箭头函数，`let`和`const`声明的变量，这些都不会被提升。

假设在全局使用域，有如下的代码：

```
console.log(y);
y = 1;
console.log(y);
console.log(greet("Mark"));

function greet(name)\\{
  return 'Hello ' + name + '!';
\\}

var y;
```

上面分别打印：`undefined`,`1`, `Hello Mark!`。

上面代码在编译阶段其实是这样的：

```
function greet(name) \\{
  return 'Hello ' + name + '!';
\\}

var y; // 默认值 undefined

// 等待“编译”阶段完成，然后开始“执行”阶段

/*
console.log(y);
y = 1;
console.log(y);
console.log(greet("Mark"));
*/
```

编译阶段完成后，它将启动执行阶段调用方法，并将值分配给变量。

```
function greet(name) \\{
  return 'Hello ' + name + '!';
\\}

var y;

//start "execution" phase

console.log(y);
y = 1;
console.log(y);
console.log(greet("Mark"));
```



### 19. 什么是作用域？

JavaScript 中的作用域是我们可以有效访问变量或函数的区域。JS 有三种类型的作用域：**全局作用域**、**函数作用域**和**块作用域(ES6)**。

- **全局作用域**——在全局命名空间中声明的变量或函数位于全局作用域中，因此在代码中的任何地方都可以访问它们。

```
//global namespace
var g = "global";

function globalFunc()\\{
  function innerFunc()\\{
    console.log(g); // can access "g" because "g" is a global variable
  \\}
 innerFunc();
\\}  
```

- **函数作用域**——在函数中声明的变量、函数和参数可以在函数内部访问，但不能在函数外部访问。

```
function myFavoriteFunc(a) \\{
  if (true) \\{
    var b = "Hello " + a;
  \\}
  return b;
\\}

myFavoriteFunc("World");

console.log(a); // Throws a ReferenceError "a" is not defined
console.log(b); // does not continue here 
```

- **块作用域**-在块`\\{\\}`中声明的变量（`let，const`）只能在其中访问。

```
 function testBlock()\\{
   if(true)\\{
     let z = 5;
   \\}
   return z; 
 \\}

 testBlock(); // Throws a ReferenceError "z" is not defined
```

作用域也是一组用于查找变量的规则。如果变量在当前作用域中不存在，它将向外部作用域中查找并搜索，如果该变量不存在，它将再次查找直到到达全局作用域，如果找到，则可以使用它，否则引发错误，这种查找过程也称为**作用域链**。

```
   /* 作用域链

     内部作用域->外部作用域-> 全局作用域
  */

  // 全局作用域
  var variable1 = "Comrades";   
  var variable2 = "Sayonara";

  function outer()\\{
  // 外部作用域
    var variable1 = "World";
    function inner()\\{
    // 内部作用域
      var variable2 = "Hello";
      console.log(variable2 + " " + variable1);
    \\}
    inner();
  \\}  
  outer(); // Hello World
```



![图片](https://mmbiz.qpic.cn/mmbiz_png/LDPLltmNy57ianicNyt0G9GEGibARafiazZKZygCFTnJzqJUDenZbJd5iaNb4JdmPlNichcClS3DHIK6C3F1iaicueicBIA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)





### 20. 什么是闭包？

这可能是所有问题中最难的一个问题，因为闭包是一个有争议的话题，这里从个人角度来谈谈，如果不妥，多多海涵。

**闭包**就是一个函数在声明时能够记住当前作用域、父函数作用域、及父函数作用域上的变量和参数的引用，直至通过作用域链上全局作用域，基本上闭包是在声明函数时创建的作用域。

看看小例子：

```
   // 全局作用域
   var globalVar = "abc";

   function a()\\{
     console.log(globalVar);
   \\}

   a(); // "abc" 
```

在此示例中，当我们声明`a`函数时，全局作用域是`a`闭包的一部分。

![图片](https://mmbiz.qpic.cn/mmbiz_png/LDPLltmNy57ianicNyt0G9GEGibARafiazZKGgUN6iannKmoHFEkT9qSDLXFy2UdceBhTc0jTPhHVMII9VQotMBVEicw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)



变量`globalVar`在图中没有值的原因是该变量的值可以根据调用函数`a`的位置和时间而改变。但是在上面的示例中，`globalVar`变量的值为`abc`。

来看一个更复杂的例子：

```
var globalVar = "global";
var outerVar = "outer"

function outerFunc(outerParam) \\{
  function innerFunc(innerParam) \\{
    console.log(globalVar, outerParam, innerParam);
  \\}
  return innerFunc;
\\}

const x = outerFunc(outerVar);
outerVar = "outer-2";
globalVar = "guess"
x("inner");
```



![图片](https://mmbiz.qpic.cn/mmbiz_png/LDPLltmNy57ianicNyt0G9GEGibARafiazZKzKopRTZNRpghHkyZrkzDN6T3hPKNfaTgqibvWXAj31jurfSLstX7MGg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

上面打印结果是  `guess outer inner`。

当我们调用`outerFunc`函数并将返回值`innerFunc`函数分配给变量`x`时，即使我们为`outerVar`变量分配了新值`outer-2`，`outerParam`也继续保留`outer`值，因为重新分配是在调用`outerFunc`之后发生的，并且当我们调用`outerFunc`函数时，它会在作用域链中查找`outerVar`的值，此时的`outerVar`的值将为 `"outer"`。

现在，当我们调用引用了`innerFunc`的`x`变量时，`innerParam`将具有一个`inner`值，因为这是我们在调用中传递的值，而`globalVar`变量值为`guess`，因为在调用`x`变量之前，我们将一个新值分配给`globalVar`。

下面这个示例演示没有理解好闭包所犯的错误：

```
const arrFuncs = [];
for(var i = 0; i < 5; i++)\\{
  arrFuncs.push(function ()\\{
    return i;
  \\});
\\}
console.log(i); // i is 5

for (let i = 0; i < arrFuncs.length; i++) \\{
  console.log(arrFuncs[i]()); // 都打印 5
\\}
```

由于闭包，此代码无法正常运行。`var`关键字创建一个全局变量，当我们 push 一个函数时，这里返回的全局变量`i`。因此，当我们在循环后在该数组中调用其中一个函数时，它会打印`5`，因为我们得到`i`的当前值为`5`，我们可以访问它，因为它是全局变量。

因为闭包在创建变量时会保留该变量的引用而不是其值。我们可以使用**IIFES**或使用 `let` 来代替 `var` 的声明。



### 21. JavaScript 中的虚值是什么？

```
 const falsyValues = ['', 0, null, undefined, NaN, false];
```

简单的来说虚值就是是在转换为布尔值时变为 `false` 的值。



### 22. 如何检查值是否虚值？

使用 `Boolean` 函数或者 `!!` 运算符。



### 23. 'use strict' 是干嘛用的？

`"use strict"` 是 **ES5** 特性，它使我们的代码在函数或整个脚本中处于**严格模式**。**严格模式**帮助我们在代码的早期避免 bug，并为其添加限制。

**严格模式**的一些限制：

1. 变量必须声明后再使用
2. 函数的参数不能有同名属性，否则报错
3. 不能使用`with`语句
4. 不能对只读属性赋值，否则报错
5. 不能使用前缀 0 表示八进制数，否则报错
6. 不能删除不可删除的属性，否则报错
7. 不能删除变量`delete prop`，会报错，只能删除属性`delete global[prop]`
8. `eval`不能在它的外层作用域引入变量
9. `eval`和`arguments`不能被重新赋值
10. `arguments`不会自动反映函数参数的变化
11. 不能使用`arguments.callee`
12. 不能使用`arguments.caller`
13. 禁止`this`指向全局对象
14. 不能使用`fn.caller`和`fn.arguments`获取函数调用的堆栈
15. 增加了保留字（比如`protected`、`static`和`interface`）

设立”严格模式”的目的，主要有以下几个：

1. 消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为;
2. 消除代码运行的一些不安全之处，保证代码运行的安全；
3. 提高编译器效率，增加运行速度；
4. 为未来新版本的Javascript做好铺垫。



### 24. JavaScript 中 `this` 值是什么？

基本上，`this`指的是当前正在执行或调用该函数的对象的值。`this`值的变化取决于我们使用它的上下文和我们在哪里使用它。

```
const carDetails = \\{
  name: "Ford Mustang",
  yearBought: 2005,
  getName()\\{
    return this.name;
  \\},
  isRegistered: true
\\};

console.log(carDetails.getName()); // Ford Mustang
```

这通常是我们期望结果的，因为在`getName`方法中我们返回`this.name`，在此上下文中，`this`指向的是`carDetails`对象，该对象当前是执行函数的“所有者”对象。

接下我们做些奇怪的事情：

```
var name = "Ford Ranger";
var getCarName = carDetails.getName;

console.log(getCarName()); // Ford Ranger
```

上面打印`Ford Ranger`，这很奇怪，因为在第一个`console.log`语句中打印的是`Ford Mustang`。这样做的原因是`getCarName`方法有一个不同的“所有者”对象，即`window`对象。在全局作用域中使用`var`关键字声明变量会在`window`对象中附加与变量名称相同的属性。请记住，当没有使用`“use strict”`时，在全局作用域中`this`指的是`window`对象。

```
console.log(getCarName === window.getCarName); // true
console.log(getCarName === this.getCarName); // true
```

本例中的`this`和`window`引用同一个对象。

解决这个问题的一种方法是在函数中使用`apply`和`call`方法。

```
console.log(getCarName.apply(carDetails)); // Ford Mustang
console.log(getCarName.call(carDetails));  // Ford Mustang
```

`apply`和`call`方法期望第一个参数是一个对象，该对象是函数内部`this`的值。

`IIFE`或**立即执行的函数表达式**，在全局作用域内声明的函数，对象内部方法中的匿名函数和内部函数的`this`具有默认值，该值指向`window`对象。

```
   (function ()\\{
     console.log(this);
   \\})(); // 打印 "window" 对象

   function iHateThis()\\{
      console.log(this);
   \\}

   iHateThis(); // 打印 "window" 对象

   const myFavoriteObj = \\{
     guessThis()\\{
        function getName()\\{
          console.log(this.name);
        \\}
        getName();
     \\},
     name: 'Marko Polo',
     thisIsAnnoying(callback)\\{
       callback();
     \\}
   \\};


   myFavoriteObj.guessThis(); // 打印 "window" 对象
   myFavoriteObj.thisIsAnnoying(function ()\\{
     console.log(this); // 打印 "window" 对象
   \\});
```

如果我们要获取`myFavoriteObj`对象中的`name`属性（即**Marko Polo**）的值，则有两种方法可以解决此问题。

一种是将 `this` 值保存在变量中。

```
const myFavoriteObj = \\{
 guessThis()\\{
  const self = this; // 把 this 值保存在 self 变量中
  function getName()\\{
    console.log(self.name);
  \\}
  getName();
 \\},
 name: 'Marko Polo',
 thisIsAnnoying(callback)\\{
   callback();
  \\}
\\};
```

第二种方式是使用箭头函数

```
const myFavoriteObj = \\{
  guessThis()\\{
     const getName = () => \\{ 
       console.log(this.name);
     \\}
     getName();
  \\},
  name: 'Marko Polo',
  thisIsAnnoying(callback)\\{
   callback();
  \\}
\\};
```

箭头函数没有自己的 `this`。它复制了这个封闭的词法作用域中`this`值，在这个例子中，`this`值在`getName`内部函数之外，也就是`myFavoriteObj`对象。



### 25. 对象的 prototype(原型) 是什么？

简单地说，原型就是对象的蓝图。如果它存在当前对象中，则将其用作属性和方法的回退。它是在对象之间共享属性和功能的方法，这也是JavaScript实现继承的核心。

```
const o = \\{\\};
console.log(o.toString()); // logs [object Object] 
```

即使`o`对象中不存在`o.toString`方法，它也不会引发错误，而是返回字符串`[object Object]`。当对象中不存在属性时，它将查看其原型，如果仍然不存在，则将其查找到原型的原型，依此类推，直到在原型链中找到具有相同属性的属性为止。原型链的末尾是`Object.prototype`。

```
console.log(o.toString === Object.prototype.toString); // logs true
```



### 26. 什么是 IIFE，它的用途是什么？

**IIFE**或立即调用的函数表达式是在创建或声明后将被调用或执行的函数。创建**IIFE的**语法是，将`function ()\\{\\}`包裹在在括号`()`内，然后再用另一个括号`()`调用它，如：`(function()\\{\\})()`

```
(function()\\{
  ...
\\} ());

(function () \\{
  ...
\\})();

(function named(params) \\{
  ...
\\})();

(() => \\{

\\});

(function (global) \\{
  ...
\\})(window);

const utility = (function () \\{
  return \\{
    ...
  \\}
\\})
```

这些示例都是有效的**IIFE**。倒数第二个表明我们可以将参数传递给**IIFE**函数。最后一个示例表明，我们可以将`IIFE`的结果保存到变量中，以便稍后使用。

**IIFE**的一个主要作用是避免与全局作用域内的其他变量命名冲突或污染全局命名空间，来个例子。

```
<script src="https://cdnurl.com/somelibrary.js"></script>
```

假设我们引入了一个`omelibr.js`的链接，它提供了一些我们在代码中使用的全局函数，但是这个库有两个方法我们没有使用：`createGraph`和`drawGraph`，因为这些方法都有`bug`。我们想实现自己的`createGraph`和`drawGraph`方法。

解决此问题的一种方法是直接覆盖：

```
<script src="https://cdnurl.com/somelibrary.js"></script>
<script>
   function createGraph() \\{
      // createGraph logic here
   \\}
   function drawGraph() \\{
      // drawGraph logic here
   \\}
</script>
```

当我们使用这个解决方案时，我们覆盖了库提供给我们的那两个方法。

另一种方式是我们自己改名称：

```
<script src="https://cdnurl.com/somelibrary.js"></script>
<script>
   function myCreateGraph() \\{
      // createGraph logic here
   \\}
   function myDrawGraph() \\{
      // drawGraph logic here
   \\}
</script>
```

当我们使用这个解决方案时，我们把那些函数调用更改为新的函数名。

还有一种方法就是使用**IIFE**：

```
<script src="https://cdnurl.com/somelibrary.js"></script>
<script>
   const graphUtility = (function () \\{
      function createGraph() \\{
         // createGraph logic here
      \\}
      function drawGraph() \\{
         // drawGraph logic here
      \\}
      return \\{
         createGraph,
         drawGraph
      \\}
   \\})
</script>
```

在此解决方案中，我们要声明了`graphUtility` 变量，用来保存**IIFE**执行的结果，该函数返回一个包含两个方法`createGraph`和`drawGraph`的对象。

**IIFE** 还可以用来解决一个常见的面试题：

```
var li = document.querySelectorAll('.list-group > li');
for (var i = 0, len = li.length; i < len; i++) \\{
   li[i].addEventListener('click', function (e) \\{
      console.log(i);
   \\})
```

假设我们有一个带有`list-group`类的`ul`元素，它有`5`个`li`子元素。当我们单击单个`li`元素时，打印对应的下标值。但在此外上述代码不起作用，这里每次点击 `li` 打印 `i` 的值都是`5`，这是由于闭包的原因。

**闭包**只是函数记住其当前作用域，父函数作用域和全局作用域的变量引用的能力。当我们在全局作用域内使用`var`关键字声明变量时，就创建全局变量`i`。因此，当我们单击`li`元素时，它将打印`5`，因为这是稍后在回调函数中引用它时`i`的值。

使用 **IIFE** 可以解决此问题：

```
var li = document.querySelectorAll('.list-group > li');
for (var i = 0, len = li.length; i < len; i++) \\{
   (function (currentIndex) \\{
      li[currentIndex].addEventListener('click', function (e) \\{
         console.log(currentIndex);
      \\})
   \\})(i);
\\}
```

该解决方案之所以行的通，是因为**IIFE**会为每次迭代创建一个新的作用域，我们捕获`i`的值并将其传递给`currentIndex`参数，因此调用**IIFE**时，每次迭代的`currentIndex`值都是不同的。



### 27. Function.prototype.apply 方法的用途是什么？

`apply()` 方法调用一个具有给定this值的函数，以及作为一个数组（或类似数组对象）提供的参数。

```
const details = \\{
  message: 'Hello World!'
\\};

function getMessage()\\{
  return this.message;
\\}

getMessage.apply(details); // 'Hello World!'
```

> `call()`方法的作用和 `apply()` 方法类似，区别就是`call()`方法接受的是参数列表，而`apply()`方法接受的是一个参数数组。

```
const person = \\{
  name: "Marko Polo"
\\};

function greeting(greetingMessage) \\{
  return `$\\{greetingMessage\\} $\\{this.name\\}`;
\\}

greeting.apply(person, ['Hello']); // "Hello Marko Polo!"
```



### 28. `Function.prototype.call` 方法的用途是什么？

`call()` 方法使用一个指定的 `this` 值和单独给出的一个或多个参数来调用一个函数。

```
const details = \\{
  message: 'Hello World!'
\\};

function getMessage()\\{
  return this.message;
\\}

getMessage.call(details); // 'Hello World!'
```

注意：该方法的语法和作用与 `apply()` 方法类似，只有一个区别，就是 `call()` 方法接受的是一个参数列表，而 `apply()` 方法接受的是一个包含多个参数的数组。

```
const person = \\{
  name: "Marko Polo"
\\};

function greeting(greetingMessage) \\{
  return `$\\{greetingMessage\\} $\\{this.name\\}`;
\\}

greeting.call(person, 'Hello'); // "Hello Marko Polo!"
```



### 29. Function.prototype.apply 和 Function.prototype.call 之间有什么区别？

`apply()`方法可以在使用一个指定的 `this` 值和一个参数数组（或类数组对象）的前提下调用某个函数或方法。`call()`方法类似于`apply()`，不同之处仅仅是`call()`接受的参数是参数列表。

```
const obj1 = \\{
 result:0
\\};

const obj2 = \\{
 result:0
\\};

function reduceAdd()\\{
   let result = 0;
   for(let i = 0, len = arguments.length; i < len; i++)\\{
     result += arguments[i];
   \\}
   this.result = result;
\\}

reduceAdd.apply(obj1, [1, 2, 3, 4, 5]); // 15
reduceAdd.call(obj2, 1, 2, 3, 4, 5); // 15
```



### 30. Function.prototype.bind 的用途是什么？

`bind()` 方法创建一个新的函数，在 `bind()` 被调用时，这个新函数的 `this` 被指定为 `bind()` 的第一个参数，而其余参数将作为新函数的参数，供调用时使用。

```
import React from 'react';

class MyComponent extends React.Component \\{
     constructor(props)\\{
          super(props); 
          this.state = \\{
             value : ""
          \\}  
          this.handleChange = this.handleChange.bind(this); 
          // 将 “handleChange” 方法绑定到 “MyComponent” 组件
     \\}

     handleChange(e)\\{
       //do something amazing here
     \\}

     render()\\{
        return (
              <>
                <input type=\\{this.props.type\\}
                        value=\\{this.state.value\\}
                     onChange=\\{this.handleChange\\}                      
                  />
              </>
        )
     \\}
\\}
```



### 31. 什么是函数式编程? JavaScript 的哪些特性使其成为函数式语言的候选语言？

函数式编程（通常缩写为FP）是通过编写纯函数，避免共享状态、可变数据、副作用 来构建软件的过程。数式编程是声明式 的而不是命令式 的，应用程序的状态是通过纯函数流动的。与面向对象编程形成对比，面向对象中应用程序的状态通常与对象中的方法共享和共处。

函数式编程是一种编程范式 ，这意味着它是一种基于一些基本的定义原则（如上所列）思考软件构建的方式。当然，编程范式的其他示例也包括面向对象编程和过程编程。

函数式的代码往往比命令式或面向对象的代码更简洁，更可预测，更容易测试 - 但如果不熟悉它以及与之相关的常见模式，函数式的代码也可能看起来更密集杂乱，并且 相关文献对新人来说是不好理解的。

**JavaScript支持闭包和高阶函数是函数式编程语言的特点。**



### 32. 什么是高阶函数？

**高阶函数只是将函数作为参数或返回值的函数。**

```
function higherOrderFunction(param,callback)\\{
    return callback(param);
\\}
```



### 33. 为什么函数被称为一等公民？

在JavaScript中，函数不仅拥有一切传统函数的使用方式（声明和调用），而且可以做到像简单值一样赋值`（var func = function()\\{\\}）`、传参`(function func(x,callback)\\{callback();\\})`、返回`(function()\\{return function()\\{}})`，这样的函数也称之为**第一级函数（First-class Function）**。不仅如此，JavaScript中的函数还充当了类的构造函数的作用，同时又是一个`Function`类的实例(instance)。这样的多重身份让JavaScript的函数变得非常重要。



### 34. 手动实现 `Array.prototype.map 方法`

`map()` 方法创建一个新数组，其结果是该数组中的每个元素都调用一个提供的函数后返回的结果。

```
function map(arr, mapCallback) \\{
  // 首先，检查传递的参数是否正确。
  if (!Array.isArray(arr) || !arr.length || typeof mapCallback !== 'function') \\{ 
    return [];
  \\} else \\{
    let result = [];
    // 每次调用此函数时，我们都会创建一个 result 数组
    // 因为我们不想改变原始数组。
    for (let i = 0, len = arr.length; i < len; i++) \\{
      result.push(mapCallback(arr[i], i, arr)); 
      // 将 mapCallback 返回的结果 push 到 result 数组中
    \\}
    return result;
  \\}
\\}
```



### 35. 手动实现`Array.prototype.filter`方法

`filter()` 方法创建一个新数组, 其包含通过所提供函数实现的测试的所有元素。

```
function filter(arr, filterCallback) \\{
  // 首先，检查传递的参数是否正确。
  if (!Array.isArray(arr) || !arr.length || typeof filterCallback !== 'function') 
  \\{
    return [];
  \\} else \\{
    let result = [];
     // 每次调用此函数时，我们都会创建一个 result 数组
     // 因为我们不想改变原始数组。
    for (let i = 0, len = arr.length; i < len; i++) \\{
      // 检查 filterCallback 的返回值是否是真值
      if (filterCallback(arr[i], i, arr)) \\{ 
      // 如果条件为真，则将数组元素 push 到 result 中
        result.push(arr[i]);
      \\}
    \\}
    return result; // return the result array
  \\}
\\}
```



### 36. 手动实现`Array.prototype.reduce`方法

`reduce()` 方法对数组中的每个元素执行一个由您提供的`reducer`函数(升序执行)，将其结果汇总为单个返回值。

```
function reduce(arr, reduceCallback, initialValue) \\{
  // 首先，检查传递的参数是否正确。
  if (!Array.isArray(arr) || !arr.length || typeof reduceCallback !== 'function') 
  \\{
    return [];
  \\} else \\{
    // 如果没有将initialValue传递给该函数，我们将使用第一个数组项作为initialValue
    let hasInitialValue = initialValue !== undefined;
    let value = hasInitialValue ? initialValue : arr[0];
   、

    // 如果有传递 initialValue，则索引从 1 开始，否则从 0 开始
    for (let i = hasInitialValue ? 0 : 1, len = arr.length; i < len; i++) \\{
      value = reduceCallback(value, arr[i], i, arr); 
    \\}
    return value;
  \\}
\\}
```



### 37. arguments 的对象是什么？

`arguments`对象是函数中传递的参数值的集合。它是一个类似数组的对象，因为它有一个length属性，我们可以使用数组索引表示法`arguments[1]`来访问单个值，但它没有数组中的内置方法，如：`forEach`、`reduce`、`filter`和`map`。

我们可以使用`Array.prototype.slice`将`arguments`对象转换成一个数组。

```
function one() \\{
  return Array.prototype.slice.call(arguments);
\\}
```

**注意:箭头函数中没有`arguments`对象。**

```
function one() \\{
  return arguments;
\\}
const two = function () \\{
  return arguments;
\\}
const three = function three() \\{
  return arguments;
\\}

const four = () => arguments;

four(); // Throws an error  - arguments is not defined
```

当我们调用函数`four`时，它会抛出一个`ReferenceError: arguments is not defined error`。使用`rest`语法，可以解决这个问题。

```
const four = (...args) => args;
```

这会自动将所有参数值放入数组中。



### 38. 如何创建一个没有 prototype(原型)的对象？

我们可以使用`Object.create`方法创建没有原型的对象。

```
const o1 = \\{\\};
console.log(o1.toString()); // [object Object]

const o2 = Object.create(null);
console.log(o2.toString());
// throws an error o2.toString is not a function 
```



### 39. 为什么在调用这个函数时，代码中的`b`会变成一个全局变量?

```
function myFunc() \\{
  let a = b = 0;
\\}

myFunc();
```

原因是赋值运算符是从右到左的求值的。这意味着当多个赋值运算符出现在一个表达式中时，它们是从右向左求值的。所以上面代码变成了这样：

```
function myFunc() \\{
  let a = (b = 0);
\\}

myFunc();
```

首先，表达式`b = 0`求值，在本例中`b`没有声明。因此，JS引擎在这个函数外创建了一个全局变量`b`，之后表达式`b = 0`的返回值为`0`，并赋给新的局部变量`a`。

我们可以通过在赋值之前先声明变量来解决这个问题。

```
function myFunc() \\{
  let a,b;
  a = b = 0;
\\}
myFunc();
```



### 40. ECMAScript 是什么？

ECMAScript 是编写脚本语言的标准，这意味着JavaScript遵循ECMAScript标准中的规范变化，因为它是JavaScript的蓝图。

ECMAScript 和 Javascript，本质上都跟一门语言有关，一个是语言本身的名字，一个是语言的约束条件
只不过发明JavaScript的那个人（Netscape公司），把东西交给了ECMA（European Computer Manufacturers Association），这个人规定一下他的标准，因为当时有java语言了，又想强调这个东西是让ECMA这个人定的规则，所以就这样一个神奇的东西诞生了，这个东西的名称就叫做ECMAScript。

javaScript = ECMAScript + DOM + BOM（自认为是一种广义的JavaScript）

ECMAScript说什么JavaScript就得做什么！

JavaScript（狭义的JavaScript）做什么都要问问ECMAScript我能不能这样干！如果不能我就错了！能我就是对的！

——突然感觉JavaScript好没有尊严，为啥要搞个人出来约束自己，

那个人被创造出来也好委屈，自己被创造出来完全是因为要约束JavaScript。



### 41. ES6或ECMAScript 2015有哪些新特性？

- 箭头函数
- 类
- 模板字符串
- 加强的对象字面量
- 对象解构
- Promise
- 生成器
- 模块
- Symbol
- 代理
- Set
- 函数默认参数
- rest 和展开
- 块作用域



### 42. `var`,`let`和`const`的区别是什么？

**`var`声明的变量会挂载在`window`上，而`let`和`const`声明的变量不会：**

```
var a = 100;
console.log(a,window.a);    // 100 100

let b = 10;
console.log(b,window.b);    // 10 undefined

const c = 1;
console.log(c,window.c);    // 1 undefined
```

**`var`声明变量存在变量提升，`let`和`const`不存在变量提升:**

```
console.log(a); // undefined  ===>  a已声明还没赋值，默认得到undefined值
var a = 100;

console.log(b); // 报错：b is not defined  ===> 找不到b这个变量
let b = 10;

console.log(c); // 报错：c is not defined  ===> 找不到c这个变量
const c = 10;
```

**`let`和`const`声明形成块作用域**

```
if(1)\\{
  var a = 100;
  let b = 10;
\\}

console.log(a); // 100
console.log(b)  // 报错：b is not defined  ===> 找不到b这个变量

-------------------------------------------------------------

if(1)\\{
  var a = 100;
  const c = 1;
\\}
console.log(a); // 100
console.log(c)  // 报错：c is not defined  ===> 找不到c这个变量
```

**同一作用域下`let`和`const`不能声明同名变量，而`var`可以**

```
var a = 100;
console.log(a); // 100

var a = 10;
console.log(a); // 10
-------------------------------------
let a = 100;
let a = 10;

//  控制台报错：Identifier 'a' has already been declared  ===> 标识符a已经被声明了。
```

**暂存死区**

```
var a = 100;

if(1)\\{
    a = 10;
    //在当前块作用域中存在a使用let/const声明的情况下，给a赋值10时，只会在当前作用域找变量a，
    // 而这时，还未到声明时候，所以控制台Error:a is not defined
    let a = 1;
\\}
```

**const**

```
/*
* 　　1、一旦声明必须赋值,不能使用null占位。
*
* 　　2、声明后不能再修改
*
* 　　3、如果声明的是复合类型数据，可以修改其属性
*
* */

const a = 100; 

const list = [];
list[0] = 10;
console.log(list);　　// [10]

const obj = \\{a:100\\};
obj.name = 'apple';
obj.a = 10000;
console.log(obj);　　// \\{a:10000,name:'apple'\\}
```



### 43. 什么是箭头函数？

箭头函数表达式的语法比函数表达式更简洁，并且没有自己的`this`，`arguments`，`super`或`new.target`。箭头函数表达式更适用于那些本来需要匿名函数的地方，并且它不能用作构造函数。

```
//ES5 Version
var getCurrentDate = function ()\\{
  return new Date();
\\}

//ES6 Version
const getCurrentDate = () => new Date();
```

在本例中，ES5 版本中有`function()\\{\\}`声明和`return`关键字，这两个关键字分别是创建函数和返回值所需要的。在箭头函数版本中，我们只需要`()`括号，不需要 `return` 语句，因为如果我们只有一个表达式或值需要返回，箭头函数就会有一个隐式的返回。

```
//ES5 Version
function greet(name) \\{
  return 'Hello ' + name + '!';
\\}

//ES6 Version
const greet = (name) => `Hello $\\{name\\}`;
const greet2 = name => `Hello $\\{name\\}`;
```

我们还可以在箭头函数中使用与函数表达式和函数声明相同的参数。如果我们在一个箭头函数中有一个参数，则可以省略括号。

```
const getArgs = () => arguments

const getArgs2 = (...rest) => rest
```

箭头函数不能访问`arguments`对象。所以调用第一个`getArgs`函数会抛出一个错误。相反，我们可以使用**rest**参数来获得在箭头函数中传递的所有参数。

```
const data = \\{
  result: 0,
  nums: [1, 2, 3, 4, 5],
  computeResult() \\{
    // 这里的“this”指的是“data”对象
    const addAll = () => \\{
      return this.nums.reduce((total, cur) => total + cur, 0)
    \\};
    this.result = addAll();
  \\}
\\};
```

箭头函数没有自己的`this`值。它捕获词法作用域函数的`this`值，在此示例中，`addAll`函数将复制`computeResult` 方法中的`this`值，如果我们在全局作用域声明箭头函数，则`this`值为 `window` 对象。



### 44. 什么是类？

`类(class)`是在 JS 中编写构造函数的新方法。它是使用构造函数的语法糖，在底层中使用仍然是原型和基于原型的继承。

```
   //ES5 Version
   function Person(firstName, lastName, age, address)\\{
      this.firstName = firstName;
      this.lastName = lastName;
      this.age = age;
      this.address = address;
   \\}

   Person.self = function()\\{
     return this;
   \\}

   Person.prototype.toString = function()\\{
     return "[object Person]";
   \\}

   Person.prototype.getFullName = function ()\\{
     return this.firstName + " " + this.lastName;
   \\}  

   //ES6 Version
   class Person \\{
        constructor(firstName, lastName, age, address)\\{
            this.lastName = lastName;
            this.firstName = firstName;
            this.age = age;
            this.address = address;
        \\}

        static self() \\{
           return this;
        \\}

        toString()\\{
           return "[object Person]";
        \\}

        getFullName()\\{
           return `$\\{this.firstName\\} $\\{this.lastName\\}`;
        \\}
   \\}
```

重写方法并从另一个类继承。

```
//ES5 Version
Employee.prototype = Object.create(Person.prototype);

function Employee(firstName, lastName, age, address, jobTitle, yearStarted) \\{
  Person.call(this, firstName, lastName, age, address);
  this.jobTitle = jobTitle;
  this.yearStarted = yearStarted;
\\}

Employee.prototype.describe = function () \\{
  return `I am $\\{this.getFullName()\\} and I have a position of $\\{this.jobTitle\\} and I started at $\\{this.yearStarted\\}`;
\\}

Employee.prototype.toString = function () \\{
  return "[object Employee]";
\\}

//ES6 Version
class Employee extends Person \\{ //Inherits from "Person" class
  constructor(firstName, lastName, age, address, jobTitle, yearStarted) \\{
    super(firstName, lastName, age, address);
    this.jobTitle = jobTitle;
    this.yearStarted = yearStarted;
  \\}

  describe() \\{
    return `I am $\\{this.getFullName()\\} and I have a position of $\\{this.jobTitle\\} and I started at $\\{this.yearStarted\\}`;
  \\}

  toString() \\{ // Overriding the "toString" method of "Person"
    return "[object Employee]";
  \\}
\\}
```

**所以我们要怎么知道它在内部使用原型？**

```
class Something \\{

\\}

function AnotherSomething()\\{

\\}
const as = new AnotherSomething();
const s = new Something();

console.log(typeof Something); // "function"
console.log(typeof AnotherSomething); // "function"
console.log(as.toString()); // "[object Object]"
console.log(as.toString()); // "[object Object]"
console.log(as.toString === Object.prototype.toString); // true
console.log(s.toString === Object.prototype.toString); // true
```



### 46. 什么是对象解构？

**对象析构**是从对象或数组中获取或提取值的一种新的、更简洁的方法。假设有如下的对象：

```
const employee = \\{
  firstName: "Marko",
  lastName: "Polo",
  position: "Software Developer",
  yearHired: 2017
\\};
```

从对象获取属性，早期方法是创建一个与对象属性同名的变量。这种方法很麻烦，因为我们要为每个属性创建一个新变量。假设我们有一个大对象，它有很多属性和方法，用这种方法提取属性会很麻烦。

```
var firstName = employee.firstName;
var lastName = employee.lastName;
var position = employee.position;
var yearHired = employee.yearHired;
```

使用解构方式语法就变得简洁多了：

```
\\{ firstName, lastName, position, yearHired \\} = employee;
```

我们还可以为属性取别名：

```
let \\{ firstName: fName, lastName: lName, position, yearHired \\} = employee;
```

当然如果属性值为 `undefined` 时，我们还可以指定默认值：

```
let \\{ firstName = "Mark", lastName: lName, position, yearHired \\} = employee;
```



### 47. 什么是 ES6 模块？

**模块**使我们能够将代码基础分割成多个文件，以获得更高的可维护性，并且避免将所有代码放在一个大文件中。在 ES6 支持模块之前，有两个流行的模块。

- **CommonJS-Node.js**
- AMD（异步模块定义）-**浏览器**

基本上，使用模块的方式很简单，`import`用于从另一个文件中获取功能或几个功能或值，同时`export`用于从文件中公开功能或几个功能或值。

**导出**

使用 ES5 (CommonJS)

```
// 使用 ES5 CommonJS - helpers.js
exports.isNull = function (val) \\{
  return val === null;
\\}

exports.isUndefined = function (val) \\{
  return val === undefined;
\\}

exports.isNullOrUndefined = function (val) \\{
  return exports.isNull(val) || exports.isUndefined(val);
\\}
```

使用 ES6 模块

```
// 使用 ES6 Modules - helpers.js
export function isNull(val)\\{
  return val === null;
\\}

export function isUndefined(val) \\{
  return val === undefined;
\\}

export function isNullOrUndefined(val) \\{
  return isNull(val) || isUndefined(val);
\\}
```

在另一个文件中导入函数

```
// 使用 ES5 (CommonJS) - index.js
const helpers = require('./helpers.js'); // helpers is an object
const isNull = helpers.isNull;
const isUndefined = helpers.isUndefined;
const isNullOrUndefined = helpers.isNullOrUndefined;

// or if your environment supports Destructuring
const \\{ isNull, isUndefined, isNullOrUndefined \\} = require('./helpers.js');
-------------------------------------------------------

// ES6 Modules - index.js
import * as helpers from './helpers.js'; // helpers is an object

// or 

import \\{ isNull, isUndefined, isNullOrUndefined as isValid \\} from './helpers.js';

// using "as" for renaming named exports
```

**在文件中导出单个功能或默认导出**

使用 ES5 (CommonJS)

```
// 使用 ES5 (CommonJS) - index.js
class Helpers \\{
  static isNull(val) \\{
    return val === null;
  \\}

  static isUndefined(val) \\{
    return val === undefined;
  \\}

  static isNullOrUndefined(val) \\{
    return this.isNull(val) || this.isUndefined(val);
  \\}
\\}


module.exports = Helpers;
```

使用ES6 Modules

```
// 使用 ES6 Modules - helpers.js
class Helpers \\{
  static isNull(val) \\{
    return val === null;
  \\}

  static isUndefined(val) \\{
    return val === undefined;
  \\}

  static isNullOrUndefined(val) \\{
    return this.isNull(val) || this.isUndefined(val);
  \\}
\\}

export default Helpers
```

从另一个文件导入单个功能

使用ES5 (CommonJS)

```
// 使用 ES5 (CommonJS) - index.js
const Helpers = require('./helpers.js'); 
console.log(Helpers.isNull(null));
```

使用 ES6 Modules

```
import Helpers from '.helpers.js'
console.log(Helpers.isNull(null));          
```



### 48. 什么是`Set`对象，它是如何工作的？

**Set** 对象允许你存储任何类型的唯一值，无论是原始值或者是对象引用。

我们可以使用`Set`构造函数创建`Set`实例。

```
const set1 = new Set();
const set2 = new Set(["a","b","c","d","d","e"]);
```

我们可以使用`add`方法向`Set`实例中添加一个新值，因为`add`方法返回`Set`对象，所以我们可以以链式的方式再次使用`add`。如果一个值已经存在于`Set`对象中，那么它将不再被添加。

```
set2.add("f");
set2.add("g").add("h").add("i").add("j").add("k").add("k");
// 后一个“k”不会被添加到set对象中，因为它已经存在了
```

我们可以使用`has`方法检查`Set`实例中是否存在特定的值。

```
set2.has("a") // true
set2.has("z") // true
```

我们可以使用`size`属性获得`Set`实例的长度。

```
set2.size // returns 10
```

可以使用`clear`方法删除 `Set` 中的数据。

```
set2.clear();
```

我们可以使用`Set`对象来删除数组中重复的元素。

```
const numbers = [1, 2, 3, 4, 5, 6, 6, 7, 8, 8, 5];
const uniqueNums = [...new Set(numbers)]; // [1,2,3,4,5,6,7,8]
```



### 49. 什么是回调函数？

**回调函数**是一段可执行的代码段，它作为一个参数传递给其他的代码，其作用是在需要的时候方便调用这段（回调函数）代码。

在JavaScript中函数也是对象的一种，同样对象可以作为参数传递给函数，因此函数也可以作为参数传递给另外一个函数，这个作为参数的函数就是回调函数。

```
const btnAdd = document.getElementById('btnAdd');

btnAdd.addEventListener('click', function clickCallback(e) \\{
    // do something useless
\\});
```

在本例中，我们等待`id`为`btnAdd`的元素中的`click`事件，如果它被单击，则执行`clickCallback`函数。回调函数向某些数据或事件添加一些功能。

数组中的`reduce`、`filter`和`map`方法需要一个回调作为参数。回调的一个很好的类比是，当你打电话给某人，如果他们不接，你留下一条消息，你期待他们回调。调用某人或留下消息的行为是事件或数据，回调是你希望稍后发生的操作。



### 50. Promise 是什么？

**Promise** 是异步编程的一种解决方案：从语法上讲，`promise`是一个对象，从它可以获取异步操作的消息；从本意上讲，它是承诺，承诺它过一段时间会给你一个结果。`promise`有三种状态：`pending(等待态)`，`fulfiled(成功态)`，`rejected(失败态)`；状态一旦改变，就不会再变。创造`promise`实例后，它会立即执行。

```
fs.readFile('somefile.txt', function (e, data) \\{
  if (e) \\{
    console.log(e);
  \\}
  console.log(data);
\\});
```

如果我们在回调内部有另一个异步操作，则此方法存在问题。我们将有一个混乱且不可读的代码。此代码称为**“回调地狱”**。

```
// 回调地狱
fs.readFile('somefile.txt', function (e, data) \\{
  //your code here
  fs.readdir('directory', function (e, files) \\{
    //your code here
    fs.mkdir('directory', function (e) \\{
      //your code here
    \\})
  \\})
\\})
```

如果我们在这段代码中使用`promise`，它将更易于阅读、理解和维护。

```
promReadFile('file/path')
  .then(data => \\{
    return promReaddir('directory');
  \\})
  .then(data => \\{
    return promMkdir('directory');
  \\})
  .catch(e => \\{
    console.log(e);
  \\})
```

`promise`有三种不同的状态：

- pending：初始状态，完成或失败状态的前一个状态
- fulfilled：操作成功完成
- rejected：操作失败

`pending` 状态的 `Promise` 对象会触发 `fulfilled/rejected` 状态，在其状态处理方法中可以传入参数/失败信息。当操作成功完成时，**Promise** 对象的 `then` 方法就会被调用；否则就会触发 `catch`。如：

```
const myFirstPromise = new Promise((resolve, reject) => \\{
    setTimeout(function()\\{
        resolve("成功!"); 
    \\}, 250);
\\});

myFirstPromise.then((data) => \\{
    console.log("Yay! " + data);
\\}).catch((e) => \\{...\\});
```



### 51. 什么是 `async/await` 及其如何工作？

`async/await`是 JS 中编写异步或非阻塞代码的新方法。它建立在**Promises**之上，让异步代码的可读性和简洁度都更高。

`async/await`是 JS 中编写异步或非阻塞代码的新方法。它建立在`Promises`之上，相对于 Promise 和回调，它的可读性和简洁度都更高。但是，在使用此功能之前，我们必须先学习`Promises`的基础知识，因为正如我之前所说，它是基于`Promise`构建的，这意味着幕后使用仍然是**Promise**。

**使用 Promise**

```
function callApi() \\{
  return fetch("url/to/api/endpoint")
    .then(resp => resp.json())
    .then(data => \\{
      //do something with "data"
    \\}).catch(err => \\{
      //do something with "err"
    \\});
\\}
```

**使用async/await**

在`async/await`，我们使用 tru/catch 语法来捕获异常。

```
async function callApi() \\{
  try \\{
    const resp = await fetch("url/to/api/endpoint");
    const data = await resp.json();
    //do something with "data"
  \\} catch (e) \\{
    //do something with "err"
  \\}
\\}
```

**注意**:使用 `async`关键声明函数会隐式返回一个**Promise**。

```
const giveMeOne = async () => 1;

giveMeOne()
  .then((num) => \\{
    console.log(num); // logs 1
  \\});
```

**注意:**`await`关键字只能在`async function`中使用。在任何非**async function**的函数中使用`await`关键字都会抛出错误。`await`关键字在执行下一行代码之前等待右侧表达式(可能是一个**Promise**)返回。

```
const giveMeOne = async () => 1;

function getOne() \\{
  try \\{
    const num = await giveMeOne();
    console.log(num);
  \\} catch (e) \\{
    console.log(e);
  \\}
\\}

// Uncaught SyntaxError: await is only valid in async function

async function getTwo() \\{
  try \\{
    const num1 = await giveMeOne(); // 这行会等待右侧表达式执行完成
    const num2 = await giveMeOne(); 
    return num1 + num2;
  \\} catch (e) \\{
    console.log(e);
  \\}
\\}

await getTwo(); // 2
```



### 52. 展开(spread )运算符和 剩余(Rest) 运算符有什么区别？

展开运算符(spread)是三个点(`...`)，可以将一个数组转为用逗号分隔的参数序列。说的通俗易懂点，有点像化骨绵掌，把一个大元素给打散成一个个单独的小元素。

剩余运算符也是用三个点(`...`)表示，它的样子看起来和展开操作符一样，但是它是用于解构数组和对象。在某种程度上，剩余元素和展开元素相反，展开元素会“展开”数组变成多个元素，剩余元素会收集多个元素和“压缩”成一个单一的元素。

```
function add(a, b) \\{
  return a + b;
\\};

const nums = [5, 6];
const sum = add(...nums);
console.log(sum);
```

在本例中，我们在调用`add`函数时使用了展开操作符，对`nums`数组进行展开。所以参数`a`的值是`5` ，`b`的值是`6`，所以`sum` 是`11`。

```
function add(...rest) \\{
  return rest.reduce((total,current) => total + current);
\\};

console.log(add(1, 2)); // 3
console.log(add(1, 2, 3, 4, 5)); // 15
```

在本例中，我们有一个`add`函数，它接受任意数量的参数，并将它们全部相加，然后返回总数。

```
const [first, ...others] = [1, 2, 3, 4, 5];
console.log(first); // 1
console.log(others); // [2,3,4,5]
```

这里，我们使用剩余操作符提取所有剩余的数组值，并将它们放入除第一项之外的其他数组中。



### 53. 什么是默认参数？

默认参数是在 JS 中定义默认变量的一种新方法，它在ES6或ECMAScript 2015版本中可用。

```
//ES5 Version
function add(a,b)\\{
  a = a || 0;
  b = b || 0;
  return a + b;
\\}

//ES6 Version
function add(a = 0, b = 0)\\{
  return a + b;
\\}
add(1); // returns 1 
```

我们还可以在默认参数中使用解构。

```
function getFirst([first, ...rest] = [0, 1]) \\{
  return first;
\\}

getFirst();  // 0
getFirst([10,20,30]);  // 10

function getArr(\\{ nums \\} = \\{ nums: [1, 2, 3, 4] \\})\\{
    return nums;
\\}

getArr(); // [1, 2, 3, 4]
getArr(\\{nums:[5,4,3,2,1]\\}); // [5,4,3,2,1]
```

我们还可以使用先定义的参数再定义它们之后的参数。

```
function doSomethingWithValue(value = "Hello World", callback = () => \\{ console.log(value) \\}) \\{
  callback();
\\}
doSomethingWithValue(); //"Hello World"
```



### 54. 什么是包装对象（wrapper object）？

我们现在复习一下JS的数据类型，JS数据类型被分为两大类，**基本类型**和**引用类型**。

基本类型：`Undefined`,`Null`,`Boolean`,`Number`,`String`,`Symbol`,`BigInt`

引用类型：`Object`,`Array`,`Date`,`RegExp`等，说白了就是对象。

其中引用类型有方法和属性，但是基本类型是没有的，但我们经常会看到下面的代码：

```
let name = "marko";

console.log(typeof name); // "string"
console.log(name.toUpperCase()); // "MARKO"
```

`name`类型是 `string`，属于基本类型，所以它没有属性和方法，但是在这个例子中，我们调用了一个`toUpperCase()`方法，它不会抛出错误，还返回了对象的变量值。

原因是基本类型的值被临时转换或强制转换为**对象**，因此`name`变量的行为类似于**对象**。除`null`和`undefined`之外的每个基本类型都有自己**包装对象**。也就是：`String`，`Number`，`Boolean`，`Symbol`和`BigInt`。在这种情况下，`name.toUpperCase()`在幕后看起来如下：

```
console.log(new String(name).toUpperCase()); // "MARKO"
```

在完成访问属性或调用方法之后，新创建的对象将立即被丢弃。



### 55. 隐式和显式转换有什么区别）？

隐式强制转换是一种将值转换为另一种类型的方法，这个过程是自动完成的，无需我们手动操作。

假设我们下面有一个例子。

```
console.log(1 + '6'); // 16
console.log(false + true); // 1
console.log(6 * '2'); // 12
```

第一个`console.log`语句结果为`16`。在其他语言中，这会抛出编译时错误，但在 JS 中，`1`被转换成字符串，然后与`+运`算符连接。我们没有做任何事情，它是由 JS 自动完成。

第二个`console.log`语句结果为`1`，JS 将`false`转换为`boolean` 值为 `0`，,`true`为`1`，因此结果为`1`。

第三个`console.log`语句结果`12`，它将`'2'`转换为一个数字，然后乘以`6 * 2`，结果是12。

而显式强制是将值转换为另一种类型的方法，我们需要手动转换。

```
console.log(1 + parseInt('6'));
```

在本例中，我们使用`parseInt`函数将`'6'`转换为`number` ，然后使用`+`运算符将`1`和`6`相加。



### 57. 如何判断值是否为数组？

我们可以使用`Array.isArray`方法来检查值是否为**数组**。当传递给它的参数是数组时，它返回`true`，否则返回`false`。

```
console.log(Array.isArray(5));  // false
console.log(Array.isArray("")); // false
console.log(Array.isArray()); // false
console.log(Array.isArray(null)); // false
console.log(Array.isArray(\\{ length: 5 \\})); // false

console.log(Array.isArray([])); // true
```

如果环境不支持此方法，则可以使用`polyfill`实现。

```
function isArray(value)\\{
 return Object.prototype.toString.call(value) === "[object Array]"
\\}
```

当然还可以使用传统的方法：

```
let a = []
if (a instanceof Array) \\{
  console.log('是数组')
\\} else \\{
  console.log('非数组')
\\}
```



### 58. 如何在不使用`\\%`模运算符的情况下检查一个数字是否是偶数？

我们可以对这个问题使用按位`&`运算符，`&`对其操作数进行运算，并将其视为二进制值，然后执行与运算。

```
function isEven(num) \\{
  if (num & 1) \\{
    return false
  \\} else \\{
    return true
  \\}
\\}
0` 二进制数是 `000`
`1` 二进制数是 `001`
`2` 二进制数是 `010`
`3` 二进制数是 `011`
`4` 二进制数是 `100`
`5` 二进制数是 `101`
`6` 二进制数是 `110`
`7` 二进制数是 `111
```

以此类推…

与运算的规则如下：

| a    | b    | a & b |
| :--- | :--- | :---- |
| 0    | 0    | 0     |
| 0    | 1    | 0     |
| 1    | 1    | 1     |

因此，当我们执行`console.log(5&1)`这个表达式时，结果为`1`。首先，`&`运算符将两个数字都转换为二进制，因此`5`变为`101`，`1`变为`001`。

然后，它使用按位怀运算符比较每个位（`0`和`1`）。`101&001`，从表中可以看出，如果`a & b`为`1`，所以`5&1`结果为`1`。

| 101 & 001 |
| :-------: |
|    101    |
|    001    |
|    001    |

- 首先我们比较最左边的`1&0`，结果是`0`。

- 然后我们比较中间的`0&0`，结果是`0`。

- 然后我们比较最后`1&1`，结果是`1`。

- 最后，得到一个二进制数`001`，对应的十进制数，即`1`。

  由此我们也可以算出`console.log(4 & 1)` 结果为`0`。知道`4`的最后一位是`0`，而`0 & 1` 将是`0`。如果你很难理解这一点，我们可以使用递归函数来解决此问题。

  ```
  function isEven(num) \\{  
      if (num < 0 || num === 1) return false;  
      if (num == 0) return true;  
      return isEven(num - 2);
  \\}
  ```




### 59. 如何检查对象中是否存在某个属性？

检查对象中是否存在属性有三种方法。

第一种使用 `in` 操作符号：

```
const o = \\{ 
  "prop" : "bwahahah",
  "prop2" : "hweasa"
\\};

console.log("prop" in o); // true
console.log("prop1" in o); // false
```

第二种使用 `hasOwnProperty` 方法，`hasOwnProperty()` 方法会返回一个布尔值，指示对象自身属性中是否具有指定的属性（也就是，是否有指定的键）。

```
console.log(o.hasOwnProperty("prop2")); // true
console.log(o.hasOwnProperty("prop1")); // false
```

第三种使用括号符号`obj["prop"]`。如果属性存在，它将返回该属性的值，否则将返回`undefined`。

```
console.log(o["prop"]); // "bwahahah"
console.log(o["prop1"]); // undefined
```



### 60. AJAX 是什么？

即异步的 **JavaScript 和 XML**，是一种用于创建快速动态网页的技术，传统的网页（不使用 AJAX）如果需要更新内容，必需重载整个网页面。使用**AJAX**则不需要加载更新整个网页，实现部分内容更新

用到AJAX的技术：

- **HTML** - 网页结构
- **CSS** - 网页的样式
- **JavaScript** - 操作网页的行为和更新DOM
- **XMLHttpRequest API** - 用于从服务器发送和获取数据
- **PHP，Python，Nodejs** - 某些服务器端语言



### 61. 如何在 JS 中创建对象？

**使用对象字面量：**

```
const o = \\{
  name: "前端小智",
  greeting() \\{
    return `Hi, 我是$\\{this.name\\}`;
  \\}
\\};

o.greeting(); // "Hi, 我是前端小智"
```

**使用构造函数：**

```
function Person(name) \\{
   this.name = name;
\\}

Person.prototype.greeting = function () \\{
   return `Hi, 我是$\\{this.name\\}`;
\\}

const mark = new Person("前端小智");

mark.greeting(); // "Hi, 我是前端小智"
```

**使用 Object.create 方法：**

```
const n = \\{
   greeting() \\{
      return `Hi, 我是$\\{this.name\\}`;
   \\}
\\};

const o = Object.create(n); 
o.name = "前端小智";
```



### 62. Object.seal 和 Object.freeze 方法之间有什么区别？

**Object.freeze()**

`Object.freeze()` 方法可以冻结一个对象。一个被冻结的对象再也不能被修改；冻结了一个对象则不能向这个对象添加新的属性，不能删除已有属性，不能修改该对象已有属性的可枚举性、可配置性、可写性，以及不能修改已有属性的值。此外，冻结一个对象后该对象的原型也不能被修改`。freeze()` 返回和传入的参数相同的对象。

**Object.seal()**

```
Object.seal()方法封闭一个对象，阻止添加新属性并将所有现有属性标记为不可配置。当前属性的值只要可写就可以改变。
```

方法的相同点：

1. ES5新增。
2. 对象不可能扩展，也就是不能再添加新的属性或者方法。
3. 对象已有属性不允许被删除。
4. 对象属性特性不可以重新配置。

方法不同点：

- `Object.seal`方法生成的密封对象，如果属性是可写的，那么可以修改属性值。
  `* Object.freeze`方法生成的冻结对象，属性都是不可写的，也就是属性值无法更改。



### 63. `in` 运算符和 `Object.hasOwnProperty` 方法有什么区别？

**hasOwnPropert方法**

`hasOwnPropert()`方法返回值是一个布尔值，指示对象自身属性中是否具有指定的属性，因此这个方法会忽略掉那些从原型链上继承到的属性。

看下面的例子：

```
Object.prototype.phone= '15345025546';

let obj = \\{
    name: '前端小智',
    age: '28'
\\}
console.log(obj.hasOwnProperty('phone')) // false
console.log(obj.hasOwnProperty('name')) // true
```

可以看到，如果在函数原型上定义一个变量`phone`，`hasOwnProperty`方法会直接忽略掉。

**in 运算符**

如果指定的属性在指定的对象或其原型链中，则`in` 运算符返回`true`。

还是用上面的例子来演示：

```
console.log('phone' in obj) // true
```

可以看到`in`运算符会检查它或者其原型链是否包含具有指定名称的属性。



### 64. 有哪些方法可以处理 JS 中的异步代码？

- 回调
- Promise
- async/await
- 还有一些库：async.js, bluebird, q, co



### 65. 函数表达式和函数声明之间有什么区别？

看下面的例子：

```
hoistedFunc();
notHoistedFunc();

function hoistedFunc()\\{
  console.log("注意：我会被提升");
\\}

var notHoistedFunc = function()\\{
  console.log("注意：我没有被提升");
\\}
```

`notHoistedFunc`调用抛出异常：`Uncaught TypeError: notHoistedFunc is not a function`，而`hoistedFunc`调用不会，因为`hoistedFunc`会被提升到作用域的顶部，而`notHoistedFunc` 不会。



### 66. 调用函数，可以使用哪些方法？

在 JS 中有4种方法可以调用函数。

**作为函数调用**——如果一个函数没有作为方法、构造函数、`apply`、`call` 调用时，此时 `this` 指向的是 `window` 对象（非严格模式）

```
  //Global Scope

  function add(a,b)\\{
    console.log(this);
    return a + b;
  \\}  

  add(1,5); // 打印 "window" 对象和 6

  const o = \\{
    method(callback)\\{
      callback();
    \\}
  \\}

  o.method(function ()\\{
      console.log(this); // 打印 "window" 对象
  \\});
```

**作为方法调用**——如果一个对象的属性有一个函数的值，我们就称它为**方法**。调用该方法时，该方法的`this`值指向该对象。

```
const details = \\{
  name : "Marko",
  getName()\\{
    return this.name;
  \\}
\\}

details.getName(); // Marko
```

**作为构造函数的调用**-如果在函数之前使用`new`关键字调用了函数，则该函数称为`构造函数`。构造函数里面会默认创建一个空对象，并将`this`指向该对象。

```
function Employee(name, position, yearHired) \\{
  // 创建一个空对象 \\{\\}
  // 然后将空对象分配给“this”关键字
  // this = \\{\\};
  this.name = name;
  this.position = position;
  this.yearHired = yearHired;
  // 如果没有指定 return ,这里会默认返回 this
\\};

const emp = new Employee("Marko Polo", "Software Developer", 2017);
```

**使用`apply`和`call`方法调用**——如果我们想显式地指定一个函数的`this`值，我们可以使用这些方法，这些方法对所有函数都可用。

```
const obj1 = \\{
 result:0
\\};

const obj2 = \\{
 result:0
\\};


function reduceAdd()\\{
   let result = 0;
   for(let i = 0, len = arguments.length; i < len; i++)\\{
     result += arguments[i];
   \\}
   this.result = result;
\\}


reduceAdd.apply(obj1, [1, 2, 3, 4, 5]);  // reduceAdd 函数中的 this 对象将是 obj1
reduceAdd.call(obj2, 1, 2, 3, 4, 5); // reduceAdd 函数中的 this 对象将是 obj2
```



### 67. 什么是缓存及它有什么作用？

缓存是建立一个函数的过程，这个函数能够记住之前计算的结果或值。使用缓存函数是为了避免在最后一次使用相同参数的计算中已经执行的函数的计算。这节省了时间，但也有不利的一面，即我们将消耗更多的内存来保存以前的结果。



### 68. 手动实现缓存方法

```
function memoize(fn) \\{
  const cache = \\{\\};
  return function (param) \\{
    if (cache[param]) \\{
      console.log('cached');
      return cache[param];
    \\} else \\{
      let result = fn(param);
      cache[param] = result;
      console.log(`not cached`);
      return result;
    \\}
  \\}
\\}

const toUpper = (str ="")=> str.toUpperCase();

const toUpperMemoized = memoize(toUpper);

toUpperMemoized("abcdef");
toUpperMemoized("abcdef");
```

这个缓存函数适用于接受一个参数。我们需要改变下，让它接受多个参数。

```
const slice = Array.prototype.slice;
function memoize(fn) \\{
  const cache = \\{\\};
  return (...args) => \\{
    const params = slice.call(args);
    console.log(params);
    if (cache[params]) \\{
      console.log('cached');
      return cache[params];
    \\} else \\{
      let result = fn(...args);
      cache[params] = result;
      console.log(`not cached`);
      return result;
    \\}
  \\}
\\}
const makeFullName = (fName, lName) => `$\\{fName\\} $\\{lName\\}`;
const reduceAdd = (numbers, startingValue = 0) => numbers.reduce((total, cur) => total + cur, startingValue);

const memoizedMakeFullName = memoize(makeFullName);
const memoizedReduceAdd = memoize(reduceAdd);

memoizedMakeFullName("Marko", "Polo");
memoizedMakeFullName("Marko", "Polo");

memoizedReduceAdd([1, 2, 3, 4, 5], 5);
memoizedReduceAdd([1, 2, 3, 4, 5], 5);
```



### 69. 为什么typeof null 返回 object？如何检查一个值是否为 null？

`typeof null == 'object'`总是返回`true`，因为这是自 JS 诞生以来`null`的实现。曾经有人提出将`typeof null == 'object'`修改为`typeof null == 'null'`，但是被拒绝了，因为这将导致更多的**bug**。

我们可以使用严格相等运算符`===`来检查值是否为`null`。

```
function isNull(value)\\{
  return value === null;
\\}
```



### 70. new 关键字有什么作用？

`new`关键字与构造函数一起使用以创建对象:

```
function Employee(name, position, yearHired) \\{
  this.name = name;
  this.position = position;
  this.yearHired = yearHired;
\\};

const emp = new Employee("Marko Polo", "Software Developer", 2017);
```

`new`关键字做了`4`件事:

- 创建空对象 `\\{\\}`
- 将空对象分配给 `this` 值
- 将空对象的`**proto**`指向构造函数的`prototype`
- 如果没有使用显式`return`语句，则返回`this`

看下面事例：

function Person() \\{
 this.name = '前端小智'
\\}

根据上面描述的，`new Person()`做了：

- 创建一个空对象：`var obj = \\{\\}`
- 将空对象分配给 `this` 值：this = obj
- 将空对象的`**proto__`指向构造函数的`prototype`:`this.__proto** = Person().prototype`
- 返回`this`:`return this`



### 71. 什么时候不使用箭头函数? 说出三个或更多的例子？

不应该使用箭头函数一些情况：

- 当想要函数被提升时(箭头函数是匿名的)
- 要在函数中使用`this/arguments`时，由于箭头函数本身不具有`this/arguments`，因此它们取决于外部上下文
- 使用命名函数(箭头函数是匿名的)
- 使用函数作为构造函数时(箭头函数没有构造函数)
- 当想在对象字面是以将函数作为属性添加并在其中使用对象时，因为咱们无法访问 `this` 即对象本身。



### 72. Object.freeze() 和 const 的区别是什么？]

`const`和`Object.freeze`是两个完全不同的概念。

`const` 声明一个只读的变量，一旦声明，常量的值就不可改变：

```
const person = \\{
    name: "Leonardo"
\\};
let animal = \\{
    species: "snake"
\\};
person = animal; // ERROR "person" is read-only    
```

`Object.freeze`适用于值，更具体地说，适用于对象值，它使对象不可变，即不能更改其属性。

```
let person = \\{
    name: "Leonardo"
\\};
let animal = \\{
    species: "snake"
\\};
Object.freeze(person);
person.name = "Lima"; //TypeError: Cannot assign to read only property 'name' of object
console.log(person); 
```



### 73. 如何在 JS 中“深冻结”对象？

如果咱们想要确保对象被深冻结，就必须创建一个递归函数来冻结对象类型的每个属性：

**没有深冻结**

```
let person = \\{
    name: "Leonardo",
    profession: \\{
        name: "developer"
    \\}
\\};
Object.freeze(person); 
person.profession.name = "doctor";
console.log(person); //output \\{ name: 'Leonardo', profession: \\{ name: 'doctor' \\} \\}
```

**深冻结**

```
function deepFreeze(object) \\{
    let propNames = Object.getOwnPropertyNames(object);
    for (let name of propNames) \\{
        let value = object[name];
        object[name] = value && typeof value === "object" ?
            deepFreeze(value) : value;
    \\}
    return Object.freeze(object);
\\}
let person = \\{
    name: "Leonardo",
    profession: \\{
        name: "developer"
    \\}
\\};
deepFreeze(person);
person.profession.name = "doctor"; // TypeError: Cannot assign to read only property 'name' of object
```



### 74. `Iterator`是什么，有什么作用？

遍历器（Iterator）就是这样一种机制。它是一种接口，为各种不同的数据结构提供统一的访问机制。任何数据结构只要部署Iterator接口，就可以完成遍历操作（即依次处理该数据结构的所有成员）。

`Iterator` 的作用有三个：

1. 为各种数据结构，提供一个统一的、简便的访问接口；
2. 使得数据结构的成员能够按某种次序排列；
3. ES6 创造了一种新的遍历命令`for…of`循环，Iterator 接口主要供`for…of`消费。

遍历过程：

1. 创建一个指针对象，指向当前数据结构的起始位置。也就是说，遍历器对象本质上，就是一个指针对象。
2. 第一次调用指针对象的next方法，可以将指针指向数据结构的第一个成员。
3. 第二次调用指针对象的next方法，指针就指向数据结构的第二个成员。
4. 不断调用指针对象的next方法，直到它指向数据结构的结束位置。

每一次调用`next`方法，都会返回数据结构的当前成员的信息。具体来说，就是返回一个包含`value`和`done`两个属性的对象。其中，`value`属性是当前成员的值，`done`属性是一个布尔值，表示遍历是否结束。

```
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



### 75. `Generator` 函数是什么，有什么作用？

如果说 JavaScrip 是 ECMAScript 标准的一种具体实现、`Iterator`遍历器是`Iterator`的具体实现，那么`Generator`函数可以说是`Iterator`接口的具体实现方式。

执行`Generator`函数会返回一个遍历器对象，每一次`Generator`函数里面的yield都相当一次遍历器对象的`next()`方法，并且可以通过`next(value)`方法传入自定义的`value`,来改变`Generator`函数的行为。

`Generator`函数可以通过配合Thunk 函数更轻松更优雅的实现异步编程和控制流管理。







### 1. new的实现原理是什么？

`new` 的实现原理:

1. 创建一个空对象，构造函数中的this指向这个空对象
2. 这个新对象被执行 [[原型]] 连接
3. 执行构造函数方法，属性和方法被添加到this引用的对象中
4. 如果构造函数中没有返回其它对象，那么返回this，即创建的这个的新对象，否则，返回构造函数中返回的对象。

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn54G2UhXFsbjtnWZ3u08jwuRnxeOQ2Yd57fvwSw2yYImx5bDjltTwu7w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)



### 2. 如何正确判断this的指向？

如果用一句话说明 this 的指向，那么即是: 谁调用它，this 就指向谁。

但是仅通过这句话，我们很多时候并不能准确判断 this 的指向。因此我们需要借助一些规则去帮助自己：

this 的指向可以按照以下顺序判断:

#### 全局环境中的 this

浏览器环境：无论是否在严格模式下，在全局执行环境中（在任何函数体外部）this 都指向全局对象 `window`;

node 环境：无论是否在严格模式下，在全局执行环境中（在任何函数体外部），this 都是空对象 `\\{\\}`;

#### 是否是 `new` 绑定

如果是 `new` 绑定，并且构造函数中没有返回 function 或者是 object，那么 this 指向这个新对象。如下:

> 构造函数返回值不是 function 或 object。 `newSuper()` 返回的是 this 对象。

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn54iaqYAbPr4NoM3clCdUbh5CT8cqS9VwjlHw8NHib7LHUfiaKy6tIK9Sfg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

> 构造函数返回值是 function 或 object， `newSuper()`是返回的是Super种返回的对象。

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5wlqjj2UkfFcAsUzCQcK7P4ibnyuXCaXG01w3B2ToMM0Pwqyic22YHJeg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

#### 函数是否通过 call,apply 调用，或者使用了 bind 绑定，如果是，那么this绑定的就是指定的对象【归结为显式绑定】。

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5ibm3yrI4oUSJHSGWeic0iadporic1R8f9cuDSmiap1NalzmzbYDp246R9xQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这里同样需要注意一种**特殊**情况，如果 call,apply 或者 bind 传入的第一个参数值是 `undefined`或者 `null`，严格模式下 this 的值为传入的值 null /undefined。非严格模式下，实际应用的默认绑定规则，this 指向全局对象(node环境为global，浏览器环境为window)

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5Lw9PYrfb71iafia6jBwaEIBiaFj1Xo2MZkibobD1QFK0EIXibtB7tGEguOQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

#### 隐式绑定，函数的调用是在某个对象上触发的，即调用位置上存在上下文对象。典型的隐式调用为: `xxx.fn()`

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5qCVwK4KbA3GGvR3EeFokrr6KhGnj4qTox3fp6aZr78zq3J7WgUuxfQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

#### 默认绑定，在不能应用其它绑定规则时使用的默认规则，通常是独立函数调用。

非严格模式：node环境，执行全局对象 global，浏览器环境，执行全局对象 window。

严格模式：执行 undefined

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5ibzF4ZTbXvUWE2Cr2xgZP3CG0phjaY6jN0lpibKQgKQppO7VibgicagRSg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

#### 箭头函数的情况：

箭头函数没有自己的this，继承外层上下文绑定的this。

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn50JCNTZLdicc1CS9v23RGIop9jwviaw0tRyT6ZzPPusPvxeaI1zRb0UlA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)



### 3. 深拷贝和浅拷贝的区别是什么？实现一个深拷贝

深拷贝和浅拷贝是针对复杂数据类型来说的，浅拷贝只拷贝一层，而深拷贝是层层拷贝。

#### 深拷贝

> 深拷贝复制变量值，对于非基本类型的变量，则递归至基本类型变量后，再复制。深拷贝后的对象与原来的对象是完全隔离的，互不影响，对一个对象的修改并不会影响另一个对象。

#### 浅拷贝

> 浅拷贝是会将对象的每个属性进行依次复制，但是当对象的属性值是引用类型时，实质复制的是其引用，当引用指向的值改变时也会跟着变化。

可以使用 `forin`、 `Object.assign`、 扩展运算符 `...` 、 `Array.prototype.slice()`、 `Array.prototype.concat()` 等，例如:

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5Y4icrlYnl1IdcKpHvO69ou18D0F8PCTHmfvWofHVgtUJpWHvrMj4uXg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

可以看出浅拷贝只最第一层属性进行了拷贝，当第一层的属性值是基本数据类型时，新的对象和原对象互不影响，但是如果第一层的属性值是复杂数据类型，那么新对象和原对象的属性值其指向的是同一块内存地址。

#### 深拷贝实现

> 1.深拷贝最简单的实现是: `JSON.parse(JSON.stringify(obj))`

`JSON.parse(JSON.stringify(obj))` 是最简单的实现方式，但是有一些缺陷：

1. 对象的属性值是函数时，无法拷贝。
2. 原型链上的属性无法拷贝
3. 不能正确的处理 Date 类型的数据
4. 不能处理 RegExp
5. 会忽略 symbol
6. 会忽略 undefined

> 2.实现一个 deepClone 函数

1. 如果是基本数据类型，直接返回
2. 如果是 `RegExp` 或者 `Date` 类型，返回对应类型
3. 如果是复杂数据类型，递归。
4. 考虑循环引用的问题

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn51FTQY2ZeZn1MtMkVKpXbM13bZuGAicnia6sdYCo8uHUqt8bbicYrSv2fw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)



### 4. call/apply 的实现原理是什么？

`call` 和 `apply` 的功能相同，都是改变 `this` 的执行，并立即执行函数。区别在于传参方式不同。



- `func.call(thisArg,arg1,arg2,...)`：第一个参数是 `this` 指向的对象，其它参数依次传入。



- `func.apply(thisArg,[argsArray])`：第一个参数是 `this` 指向的对象，第二个参数是数组或类数组。

一起思考一下，如何模拟实现 `call` ？

首先，我们知道，函数都可以调用 `call`，说明 `call` 是函数原型上的方法，所有的实例都可以调用。即: `Function.prototype.call`。

- 在 `call` 方法中获取调用 `call()`函数
- 如果第一个参数没有传入，那么默认指向 `window/global`(非严格模式)
- 传入 `call` 的第一个参数是 this 指向的对象，根据隐式绑定的规则，我们知道 `obj.foo()`, `foo()` 中的 `this` 指向 `obj`;因此我们可以这样调用函数 `thisArgs.func(...args)`
- 返回执行结果

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5SYKMXefJWOPsop82xTBM1adriaVmUmsrHQCoibViaEYfH50vSUxJcn1qg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

`apply` 的实现思路和 `call` 一致，仅参数处理略有差别。如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn55neqb9WzibkmJA43DS8js9ZqSFw04MlYKLZWpdicZx3KxDCtibopFGCMg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)



### 5. 柯里化函数实现

在开始之前，我们首先需要搞清楚函数柯里化的概念。

函数柯里化是把接受多个参数的函数变换成接受一个单一参数（最初函数的第一个参数）的函数，并且返回接受余下的参数而且返回结果的新函数的技术。

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5nRnE2g5YKGhe5CJVvx7lLicibiaQEGBfAIZhOK5ibGLibzVovwyfEsJ3ZSA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn56GGcKxicqbtHQNAprARD7nXpCCibagWCksnmXT7Td5Q0nkCplIFPR2ibw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

> 函数柯里化的主要作用：

- 参数复用
- 提前返回 – 返回接受余下的参数且返回结果的新函数
- 延迟执行 – 返回新函数，等待执行



### 6. 如何让 (a == 1 && a == 2 && a == 3) 的值为true？

> 1. 利用隐式类型转换

`==` 操作符在左右数据类型不一致时，会先进行隐式转换。

`a==1&&a==2&&a==3` 的值意味着其不可能是基本数据类型。因为如果 a 是 null 或者是 undefined bool类型，都不可能返回true。

因此可以推测 a 是复杂数据类型，JS 中复杂数据类型只有 `object`，回忆一下，Object 转换为原始类型会调用什么方法？



- 如果部署了 `[Symbol.toPrimitive]` 接口，那么调用此接口，若返回的不是基本数据类型，抛出错误。

- 如果没有部署 `[Symbol.toPrimitive]` 接口，那么根据要转换的类型，先调用 `valueOf` / `toString`

- 1. 非Date类型对象， `hint` 是 `default` 时，调用顺序为： `valueOf` >>> `toString`，即 `valueOf` 返回的不是基本数据类型，才会继续调用 `valueOf`，如果 `toString` 返回的还不是基本数据类型，那么抛出错误。
  2. 如果 `hint` 是 `string`(Date对象的hint默认是string) ，调用顺序为： `toString` >>> `valueOf`，即 `toString` 返回的不是基本数据类型，才会继续调用 `valueOf`，如果 `valueOf` 返回的还不是基本数据类型，那么抛出错误。
  3. 如果 `hint` 是 `number`，调用顺序为： `valueOf` >>> `toString`

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5V2sCHBbIibaveibXomzNl4n7DmNXPUich7gLRRgYVnkMp6mD27CqJjHDw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

> 1. 利用数据劫持(Proxy/Object.definedProperty)

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5Eia3ibFu8nLABlTOAWmbGBoWC9g4FqjQzY9p4DichctQbXvu2k5Y4GTyg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

> 1. 数组的 `toString` 接口默认调用数组的 `join` 方法，重新 `join` 方法

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5eEflnyfscRRcZ5JHKNL7vMeibicZ9Qx4xVav2AehxSIV94ZGPTvRmicvA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)



### 7. 什么是BFC？BFC的布局规则是什么？如何创建BFC？

Box 是 CSS 布局的对象和基本单位，页面是由若干个Box组成的。

元素的类型 和 `display` 属性，决定了这个 Box 的类型。不同类型的 Box 会参与不同的 Formatting Context。

> Formatting Context

Formatting Context 是页面的一块渲染区域，并且有一套渲染规则，决定了其子元素将如何定位，以及和其它元素的关系和相互作用。

Formatting Context 有 BFC (Block formatting context)，IFC (Inline formatting context)，FFC (Flex formatting context) 和 GFC (Grid formatting context)。FFC 和 GFC 为 CC3 中新增。

> BFC布局规则

- BFC内，盒子依次垂直排列。
- BFC内，两个盒子的垂直距离由 `margin` 属性决定。属于同一个BFC的两个相邻Box的margin会发生重叠【符合合并原则的margin合并后是使用大的margin】
- BFC内，每个盒子的左外边缘接触内部盒子的左边缘（对于从右到左的格式，右边缘接触）。即使在存在浮动的情况下也是如此。除非创建新的BFC。
- BFC的区域不会与float box重叠。
- BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。
- 计算BFC的高度时，浮动元素也参与计算。

> 如何创建BFC

- 根元素
- 浮动元素（float 属性不为 none）
- position 为 absolute 或 fixed
- overflow 不为 visible 的块元素
- display 为 inline-block, table-cell, table-caption

> BFC 的应用

1. 防止 margin 重叠 (同一个BFC内的两个两个相邻Box的 `margin` 会发生重叠，触发生成两个BFC，即不会重叠)
2. 清除内部浮动 (创建一个新的 BFC，因为根据 BFC 的规则，计算 BFC 的高度时，浮动元素也参与计算)
3. 自适应多栏布局 (BFC的区域不会与float box重叠。因此，可以触发生成一个新的BFC)



### 8. 异步加载JS脚本的方式有哪些？

<script> 标签中增加 async(html5) 或者 defer(html4) 属性,脚本就会异步加载。

```
<scriptsrc="../XXX.js"defer></script>
```

`defer` 和 `async` 的区别在于：

- `defer` 要等到整个页面在内存中正常渲染结束（DOM 结构完全生成，以及其他脚本执行完成），在window.onload 之前执行；
- `async` 一旦下载完，渲染引擎就会中断渲染，执行这个脚本以后，再继续渲染。
- 如果有多个 `defer` 脚本，会按照它们在页面出现的顺序加载
- 多个 `async` 脚本不能保证加载顺序

> 动态创建 `script` 标签

动态创建的 `script` ，设置 `src` 并不会开始下载，而是要添加到文档中，JS文件才会开始下载。

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5ibThWoFSzEqhcZL9JBfphU4KoHgC75jZX4SwL4Yd2QJxzMvd5gCFKqg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

> XHR 异步加载JS

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5Q0Qvasibkz3UeatXIZm2APZnwrpFmSh1rJJx7nw7dazk3iaK37HW7wSQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)



### 9. ES5有几种方式可以实现继承？分别有哪些优缺点？

ES5 有 6 种方式可以实现继承，分别为：

##### 1. 原型链继承

原型链继承的基本思想是利用原型让一个引用类型继承另一个引用类型的属性和方法。

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5nzTvsaZibnvY9744nayJGRv1bicxKo25nPa3c4ibcnfhzkNvkttlUltHQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

> 缺点：

1. 通过原型来实现继承时，原型会变成另一个类型的实例，原先的实例属性变成了现在的原型属性，该原型的引用类型属性会被所有的实例共享。
2. 在创建子类型的实例时，没有办法在不影响所有对象实例的情况下给超类型的构造函数中传递参数。

##### 2. 借用构造函数

**借用构造函数**的技术，其基本思想为:

在子类型的构造函数中调用超类型构造函数。

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5aCXn8MobqGXRvg90hDg7n8ic2IyuvwE4aibgcApciaxhgxnzzaorU3x2A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

> 优点:

1. 可以向超类传递参数
2. 解决了原型中包含引用类型值被所有实例共享的问题

> 缺点:

1. 方法都在构造函数中定义，函数复用无从谈起，另外超类型原型中定义的方法对于子类型而言都是不可见的。

##### 3. 组合继承(原型链 + 借用构造函数)

组合继承指的是将原型链和借用构造函数技术组合到一块，从而发挥二者之长的一种继承模式。基本思路：

使用原型链实现对原型属性和方法的继承，通过借用构造函数来实现对实例属性的继承，既通过在原型上定义方法来实现了函数复用，又保证了每个实例都有自己的属性。

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5V1ZrDbx8s8bnOwq9ZqKAXEjArM3xPmicz43KZGbkDydiaR2EU07icBaHQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

> 缺点:

- 无论什么情况下，都会调用两次超类型构造函数：一次是在创建子类型原型的时候，另一次是在子类型构造函数内部。

> 优点:

- 可以向超类传递参数
- 每个实例都有自己的属性
- 实现了函数复用

##### 4. 原型式继承

原型继承的基本思想：

借助原型可以基于已有的对象创建新对象，同时还不必因此创建自定义类型。

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5O5Oc6xuNqfYBomN7fic979nMOicl5pBpKgxMEgoXR9qPfmscXMU819jw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在 `object()` 函数内部，先穿甲一个临时性的构造函数，然后将传入的对象作为这个构造函数的原型，最后返回了这个临时类型的一个新实例，从本质上讲， `object()` 对传入的对象执行了一次浅拷贝。

ECMAScript5通过新增 `Object.create()`方法规范了原型式继承。这个方法接收两个参数：一个用作新对象原型的对象和（可选的）一个为新对象定义额外属性的对象(可以覆盖原型对象上的同名属性)，在传入一个参数的情况下， `Object.create()` 和 `object()` 方法的行为相同。

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5w5xjuwSNcwNxibl5v5eI18VraG9B6xHDCM4nibm2M2E2Ebue7RIVmAgw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在没有必要创建构造函数，仅让一个对象与另一个对象保持相似的情况下，原型式继承是可以胜任的。

> 缺点:

同原型链实现继承一样，包含引用类型值的属性会被所有实例共享。

##### 5. 寄生式继承

寄生式继承是与原型式继承紧密相关的一种思路。寄生式继承的思路与寄生构造函数和工厂模式类似，即创建一个仅用于封装继承过程的函数，该函数在内部已某种方式来增强对象，最后再像真地是它做了所有工作一样返回对象。

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5zCxKia3ehuVbHl38GSlUPPibAyRXV3ylZxZuMAF57z2EhjeDcaq5mhxA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

基于 `person` 返回了一个新对象 -—— `person2`，新对象不仅具有 `person` 的所有属性和方法，而且还有自己的 `sayHi()` 方法。在考虑对象而不是自定义类型和构造函数的情况下，寄生式继承也是一种有用的模式。

> 缺点：

- 使用寄生式继承来为对象添加函数，会由于不能做到函数复用而效率低下。
- 同原型链实现继承一样，包含引用类型值的属性会被所有实例共享。

##### 6. 寄生组合式继承

所谓寄生组合式继承，即通过借用构造函数来继承属性，通过原型链的混成形式来继承方法，基本思路：

不必为了指定子类型的原型而调用超类型的构造函数，我们需要的仅是超类型原型的一个副本，本质上就是使用寄生式继承来继承超类型的原型，然后再将结果指定给子类型的原型。寄生组合式继承的基本模式如下所示：

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn59eJo9qQWjQQAiauRvo7ezc2ILiayI7uUTj4rLxYBz989k42Lj87pqRdg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

- 第一步：创建超类型原型的一个副本
- 第二步：为创建的副本添加 `constructor` 属性
- 第三步：将新创建的对象赋值给子类型的原型

至此，我们就可以通过调用 `inheritPrototype` 来替换为子类型原型赋值的语句：

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5G4zK1DvgwSiaO6hl7TDmslABvXPhVhLrg4qWYbl9lm5uVSC5MQ7LayQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

> 优点:

只调用了一次超类构造函数，效率更高。避免在 `SuberType.prototype`上面创建不必要的、多余的属性，与其同时，原型链还能保持不变。

因此寄生组合继承是引用类型最理性的继承范式。



### 10. 隐藏页面中的某个元素的方法有哪些？

> 隐藏类型

屏幕并不是唯一的输出机制，比如说屏幕上看不见的元素（隐藏的元素），其中一些依然能够被读屏软件阅读出来（因为读屏软件依赖于可访问性树来阐述）。为了消除它们之间的歧义，我们将其归为三大类：

- 完全隐藏：元素从渲染树中消失，不占据空间。
- 视觉上的隐藏：屏幕中不可见，占据空间。
- 语义上的隐藏：读屏软件不可读，但正常占据空。

> 完全隐藏

##### 1. `display` 属性

```
display: none;
```

##### 2.hidden 属性

HTML5 新增属性，相当于 `display:none`

```
<div hidden></div>
```

> 视觉上的隐藏

##### 1.利用 `position` 和 盒模型 将元素移出可视区范围

1. 设置 `posoition` 为 `absolute` 或 `fixed`，通过设置 `top`、 `left` 等值，将其移出可视区域。

```
position:absolute;left: -99999px;
```

1. 设置 `position` 为 `relative`，通过设置 `top`、 `left` 等值，将其移出可视区域。

```
position: relative;left: -99999px;height: 0
```

1. 设置 margin 值，将其移出可视区域范围（可视区域占位）。

```
margin-left: -99999px;height: 0;
```

##### 2.利用 transfrom

1. 缩放

```
transform: scale(0);height: 0;
```

1. 移动 `translateX`, `translateY`

```
transform: translateX(-99999px);height: 0
```

1. 旋转 `rotate`

```
transform: rotateY(90deg);

```

##### 3.设置其大小为0

1. 宽高为0，字体大小为0：

```
height: 0;width: 0;font-size: 0;

```

1. 宽高为0，超出隐藏:

```
height: 0;width: 0;overflow: hidden;

```

##### 4.设置透明度为0

```
opacity: 0;

```

##### 5. `visibility`属性

```
visibility: hidden;

```

##### 6.层级覆盖， `z-index` 属性

```
position: relative;z-index: -999;

```

再设置一个层级较高的元素覆盖在此元素上。

##### 7.clip-path 裁剪

```
clip-path: polygon(0 0, 0 0, 0 0, 0 0);

```

> 语义上的隐藏

##### aria-hidden 属性

读屏软件不可读，占据空间，可见。

```
<div aria-hidden="true"></div>

```



### 11. let、const、var 的区别有哪些？

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5BmicUT2v1GPibejOmE8XEuomTXTAem3kVvVc5CA517TiaL2YzmPtDzopg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

1.let/const 定义的变量不会出现变量提升，而 var 定义的变量会提升。

2.相同作用域中，let 和 const 不允许重复声明，var 允许重复声明。

3.const 声明变量时必须设置初始值

4.const 声明一个只读的常量，这个常量不可改变。

这里有一个非常重要的点即是：在JS中，复杂数据类型，存储在栈中的是堆内存的地址，存在栈中的这个地址是不变的，但是存在堆中的值是可以变得。有没有相当常量指针/指针常量~

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5TMicHEJds6MerDXXDtqVaWiagtDCaIujkGIVZvOqr5wuicRbict3GiaibIKA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

一图胜万言，如下图所示，不变的是栈内存中 a 存储的 20，和 b 中存储的 0x0012ff21（瞎编的一个数字）。而 \\{age: 18, star: 200\\} 是可变的。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5rFPgUAmqvHia5657AsW9icopcB6Jx5ibboGAvsxImhTVwyU6fDNldO7kg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)



### 12. 说一说你对JS执行上下文栈和作用域链的理解？

在开始说明JS上下文栈和作用域之前，我们先说明下JS上下文以及作用域的概念。

#### JS执行上下文

执行上下文就是当前 JavaScript 代码被解析和执行时所在环境的抽象概念， JavaScript 中运行任何的代码都是在执行上下文中运行。

> 执行上下文类型分为：

- 全局执行上下文
- 函数执行上下文

执行上下文创建过程中，需要做以下几件事:

1. 创建变量对象：首先初始化函数的参数arguments，提升函数声明和变量声明。
2. 创建作用域链（Scope Chain）：在执行期上下文的创建阶段，作用域链是在变量对象之后创建的。
3. 确定this的值，即 ResolveThisBinding

#### 作用域

**作用域**负责收集和维护由所有声明的标识符（变量）组成的一系列查询，并实施一套非常严格的规则，确定当前执行的代码对这些标识符的访问权限。—— 摘录自《你不知道的JavaScript》(上卷)

作用域有两种工作模型：词法作用域和动态作用域，JS采用的是**词法作用域**工作模型，词法作用域意味着作用域是由书写代码时变量和函数声明的位置决定的。( `with` 和 `eval` 能够修改词法作用域，但是不推荐使用，对此不做特别说明)

> 作用域分为：

- 全局作用域
- 函数作用域
- 块级作用域

#### JS执行上下文栈(后面简称执行栈)

执行栈，也叫做调用栈，具有 **LIFO** (后进先出) 结构，用于存储在代码执行期间创建的所有执行上下文。

> 规则如下：

- 首次运行JavaScript代码的时候,会创建一个全局执行的上下文并Push到当前的执行栈中，每当发生函数调用，引擎都会为该函数创建一个新的函数执行上下文并Push当前执行栈的栈顶。
- 当栈顶的函数运行完成后，其对应的函数执行上下文将会从执行栈中Pop出，上下文的控制权将移动到当前执行栈的下一个执行上下文。

以一段代码具体说明：

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5yr7jLqeDaxEQTsSib18458DP1ZtCiaVib2oHcwbmzmhV5UtRI3lRyZHTQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

`GlobalExecutionContext` (即全局执行上下文)首先入栈，过程如下：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn504lVksJpOtvTG5IYCceOX5nLMK75jib1q2BJvlPteRqt7FXysNODDtw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

伪代码:

```
//全局执行上下文首先入栈ECStack.push(globalContext);
//执行fun1();ECStack.push(<fun1> functionContext);
//fun1中又调用了fun2;ECStack.push(<fun2> functionContext);
//fun2中又调用了fun3;ECStack.push(<fun3> functionContext);
//fun3执行完毕ECStack.pop();
//fun2执行完毕ECStack.pop();
//fun1执行完毕ECStack.pop();
//javascript继续顺序执行下面的代码，但ECStack底部始终有一个 全局上下文（globalContext）;

```

#### 作用域链

作用域链就是从当前作用域开始一层一层向上寻找某个变量，直到找到全局作用域还是没找到，就宣布放弃。这种一层一层的关系，就是作用域链。

如：

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5Qp3STjLricd5KZS9kcbp4ZEKIt0dNEk05nN3gUMomsTSUxQNNhXo8Vw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

fn2作用域链 = [fn2作用域, fn1作用域，全局作用域]

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn55AUHBR4xIcP8MKoJpxFPjhFZvccE0gb06WichbkHlf8CSEPVy9nQdeA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)



### 15. 什么是闭包？闭包的作用是什么？

##### 闭包的定义

《JavaScript高级程序设计》:

> 闭包是指有权访问另一个函数作用域中的变量的函数

《JavaScript权威指南》：

> 从技术的角度讲，所有的JavaScript函数都是闭包：它们都是对象，它们都关联到作用域链。

《你不知道的JavaScript》

> 当函数可以记住并访问所在的词法作用域时，就产生了闭包，即使函数是在当前词法作用域之外执行。

##### 创建一个闭包

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5rGwyvmzMVXPr3AmRqU8zibL27gO2ugAr2Hyls1LPEoTexvic435MCmrw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

闭包使得函数可以继续访问定义时的词法作用域。拜 fn 所赐，在 foo() 执行后，foo 内部作用域不会被销毁。

##### 闭包的作用

- 能够访问函数定义时所在的词法作用域(阻止其被回收)。
- 私有化变量

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5mdovgJdp40a68pUdnKDRXJ5txnoqeWWFn9hOe5YGAeFvk4K5t9H9icg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

- 模拟块级作用域

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5aUa3w6LMz6lO3mNJvVBq1BIaZVC0AvUfmVHicaPW0V2kWOEiazKCfGAA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

- 创建模块

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5vRJ9urEFXpkz3ZBOR9IC2QKaqhYycZficGPxoApBib4GyFZdu648ztYg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

模块模式具有两个必备的条件(来自《你不知道的JavaScript》)

- 必须有外部的封闭函数，该函数必须至少被调用一次(每次调用都会创建一个新的模块实例)
- 封闭函数必须返回至少**一个**内部函数，这样内部函数才能在私有作用域中形成闭包，并且可以访问或者修改私有的状态。



### 16. 实现 Promise.all 方法

在实现 Promise.all 方法之前，我们首先要知道 Promise.all 的功能和特点，因为在清楚了 Promise.all 功能和特点的情况下，我们才能进一步去写实现。

> Promise.all 功能

`Promise.all(iterable)` 返回一个新的 Promise 实例。此实例在 `iterable` 参数内所有的 `promise` 都 `fulfilled` 或者参数中不包含 `promise` 时，状态变成 `fulfilled`；如果参数中 `promise` 有一个失败 `rejected`，此实例回调失败，失败原因的是第一个失败 `promise` 的返回结果。

```
let p = Promise.all([p1, p2, p3]);

```

p的状态由 p1,p2,p3决定，分成以下；两种情况：

（1）只有p1、p2、p3的状态都变成 `fulfilled`，p的状态才会变成 `fulfilled`，此时p1、p2、p3的返回值组成一个数组，传递给p的回调函数。

（2）只要p1、p2、p3之中有一个被 `rejected`，p的状态就变成 `rejected`，此时第一个被reject的实例的返回值，会传递给p的回调函数。

> Promise.all 的特点

Promise.all 的返回值是一个 promise 实例

- 如果传入的参数为空的可迭代对象， `Promise.all` 会 **同步** 返回一个已完成状态的 `promise`
- 如果传入的参数中不包含任何 promise, `Promise.all` 会 **异步** 返回一个已完成状态的 `promise`
- 其它情况下， `Promise.all` 返回一个 **处理中（pending）** 状态的 `promise`.

> Promise.all 返回的 promise 的状态

- 如果传入的参数中的 promise 都变成完成状态， `Promise.all` 返回的 `promise` 异步地变为完成。
- 如果传入的参数中，有一个 `promise` 失败， `Promise.all` 异步地将失败的那个结果给失败状态的回调函数，而不管其它 `promise` 是否完成
- 在任何情况下， `Promise.all` 返回的 `promise` 的完成状态的结果都是一个数组

> Promise.all 实现

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5F3OQOAFicggwrrWTHRTUEPIjES9VlwEzYlEwhtia52TlDl8G1yUaIXxw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)



### 17. 请实现一个 flattenDeep 函数，把嵌套的数组扁平化

例如:

```
flattenDeep([1, [2, [3, [4]], 5]]); //[1, 2, 3, 4, 5]

```

> 利用 Array.prototype.flat

ES6 为数组实例新增了 `flat` 方法，用于将嵌套的数组“拉平”，变成一维的数组。该方法返回一个新数组，对原数组没有影响。

`flat` 默认只会 “拉平” 一层，如果想要 “拉平” 多层的嵌套数组，需要给 `flat` 传递一个整数，表示想要拉平的层数。

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5JiaAMibmh3vC4D9qYOibQprBUOyHYhiaceBlT2ZgXvmWCib63ic5D4I5qf3g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

当传递的整数大于数组嵌套的层数时，会将数组拉平为一维数组，JS能表示的最大数字为 `Math.pow(2,53)-1`，因此我们可以这样定义 `flattenDeep` 函数

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn55onORazW72kUX52iae7JiaYlDVbvRqDrtWw3eB6I82Lo764koRfHWhzw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

> 利用 reduce 和 concat

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5sliashHBgmfwaeAkYrneSdsxFzYczfRYj825iaicAQjV0A8DgbSQ9H4tA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

> 使用 stack 无限反嵌套多层嵌套数组

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5HfwkKCAN9IytV7gDu324PYTKQ8IjWyr1ibdEyshSOrv6Y67U3Jq49Yw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)



### 18. 请实现一个 uniq 函数，实现数组去重

例如:

```
uniq([1, 2, 3, 5, 3, 2]);//[1, 2, 3, 5]

```

> 法1: 利用ES6新增数据类型 `Set`

`Set`类似于数组，但是成员的值都是唯一的，没有重复的值。

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5O1Z4oSibhO3SpSE11xFAqAhTg0QdbVEU6GJzEfQr0FbTWZEQD9ddSfg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

> 法2: 利用 `indexOf`

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5wgGA7d2iaouBq9sBYESJGUXqF23KOIF6fuxCc3aL5wrSVw4z8VoFuYQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

> 法3: 利用 `includes`

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn50xB0gqX80lhqbdNJfib3hC7SClT8zd232zWHubiaNjFGFCibunpg7N5Xw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

> 法4：利用 `reduce`

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5kEKcpn37JQmUeH1XVR9sqHrIaeJpn0Axd1AVYKiaXvL1oicVibuN8cQUw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

> 法5：利用 `Map`

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5PwKVnSyibzD3b2NEpFGWEOOOVDia16qpOpZW1tnIiaK6tZbLmrlBzQjibA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)



### 19. 可迭代对象有哪些特点

ES6 规定，默认的 `Iterator` 接口部署在数据结构的 `Symbol.iterator` 属性，换个角度，也可以认为，一个数据结构只要具有 `Symbol.iterator` 属性( `Symbol.iterator` 方法对应的是遍历器生成函数，返回的是一个遍历器对象)，那么就可以其认为是可迭代的。

#### 可迭代对象的特点

- 具有 `Symbol.iterator` 属性， `Symbol.iterator()` 返回的是一个遍历器对象
- 可以使用 `for...of` 进行循环
- 通过被 `Array.from` 转换为数组

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5IQHY73dTYsQKiaeFWBbyqN6C34lkfCqMjp7LRVnwcAyL2gD5IMVFOzg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

#### 原生具有 `Iterator` 接口的数据结构：

- Array
- Map
- Set
- String
- TypedArray
- 函数的 arguments 对象
- NodeList 对象



### 20. JSONP 的原理是什么？

尽管浏览器有同源策略，但是 `<script>` 标签的 `src` 属性不会被同源策略所约束，可以获取任意服务器上的脚本并执行。 `jsonp` 通过插入 `script` 标签的方式来实现跨域，参数只能通过 `url` 传入，仅能支持 `get` 请求。

> 实现原理:

- Step1: 创建 callback 方法
- Step2: 插入 script 标签
- Step3: 后台接受到请求，解析前端传过去的 callback 方法，返回该方法的调用，并且数据作为参数传入该方法
- Step4: 前端执行服务端返回的方法调用

> jsonp源码实现

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5BGLJ0MNPYzqES2HrphOVZuP8pB6Dmouxibc54SaR42lw9T7IpU9tNfg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

> 使用:

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5aygIZBnpfWuribuM23iac7oFvFXiaErdXx4BkYuwv6v25OwWCJpfzyX6A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

> 服务端代码(node):

![图片](https://mmbiz.qpic.cn/mmbiz_png/nnic7Ckj9Nq0zXqZ0Q1e2sUkKsRLQcwn5DY7hQ98xRfA8ria5MribAuFacLHxYVGJP5Qay94b6TlpLyCC84T6HnHg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)