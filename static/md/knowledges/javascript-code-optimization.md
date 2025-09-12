---
title: JavaScript代码优化
date: 2020-06-10 20:50:00
categories: 
- 前端知识
tags:
- JavaScript
- 代码优化
---

# JavaScript小技巧

### 多个字符串检查

通常，如果我们需要检查**字符串是否等于多个值中的一个**，往往很快会觉得疲惫不堪。幸运的是，JavaScript有一个内置的方法来帮助你解决这个问题。

```
// 普通写法
const isVowel = (letter) => \\{
  if (
    letter === "a" ||
    letter === "e" ||
    letter === "i" ||
    letter === "o" ||
    letter === "u"
  ) \\{
    return true;
  \\}
  return false;
\\};

// 简写方法
const isVowel = (letter) =>
  ["a", "e", "i", "o", "u"].includes(letter);
```



### For-of和For-in循环

`For-of`和`For-in`循环是迭代`array`或`object`的好方法，因为无需手动跟踪`object`键的索引。

#### For-of

```
const arr = [1, 2, 3, 4, 5];

// 普通写法
for (let i = 0; i < arr.length; i++) \\{
  const element = arr[i];
  // ...
\\}

// 简写方法
for (const element of arr) \\{
  // ...
\\}
```

### For-in

```
const obj = \\{
  a: 1,
  b: 2,
  c: 3,
\\};

// 普通写法
const keys = Object.keys(obj);
for (let i = 0; i < keys.length; i++) \\{
  const key = keys[i];
  const value = obj[key];
  // ...
\\}

// 简写方法
for (const key in obj) \\{
  const value = obj[key];
  // ...
\\}
```



### Falsey（假值）检查

如果要检查变量是`null`、`undefined`、`0`、`false`、`NaN`还是空`string`，可以使用逻辑非 (`!`)运算符一次检查所有变量，而无需编写多个条件。这使得检查变量是否包含有效数据变得相对容易多了。

```
// 普通写法
const isFalsey = (value) => \\{
  if (
    value === null ||
    value === undefined ||
    value === 0 ||
    value === false ||
    value === NaN ||
    value === ""
  ) \\{
    return true;
  \\}
  return false;
\\};

// 简写方法
const isFalsey = (value) => !value;
```



### 三元运算符

作为JavaScript开发人员，你一定遇到过三元运算符。这是编写简洁`if-else`语句的好方法。但是，也可用来编写简洁的代码，甚至将它们链接起来来检查多个条件。

```
// 普通写法
let info;
if (value < minValue) \\{
  info = "Value is too small";
\\} else if (value > maxValue) \\{
  info = "Value is too large";
\\} else \\{
  info = "Value is in range";
\\}

// 简写方法
const info =
  value < minValue
    ? "Value is too small"
    : value > maxValue ? "Value is too large" : "Value is in range";
```



### 函数调用

在三元运算符的帮助下，你还可以根据条件确定要调用哪个函数。

> 注：函数的`call signature`必须相同，否则可能会遇到错误。

```
function f1() \\{
  // ...
\\}
function f2() \\{
  // ...
\\}

// 普通写法
if (condition) \\{
  f1();
\\} else \\{
  f2();
\\}

// 简写方法
(condition ? f1 : f2)();
```



### Switch简写

通常我们可以使用以键作为`switch`条件并将值作为返回值的对象来优化长`switch`语句。

```
const dayNumber = new Date().getDay();

// 普通写法
let day;
switch (dayNumber) \\{
  case 0:
    day = "Sunday";
    break;
  case 1:
    day = "Monday";
    break;
  case 2:
    day = "Tuesday";
    break;
  case 3:
    day = "Wednesday";
    break;
  case 4:
    day = "Thursday";
    break;
  case 5:
    day = "Friday";
    break;
  case 6:
    day = "Saturday";
\\}

// 简写方法
const days = \\{
  0: "Sunday",
  1: "Monday",
  2: "Tuesday",
  3: "Wednesday",
  4: "Thursday",
  5: "Friday",
  6: "Saturday",
\\};
const day = days[dayNumber];
```



### 默认值

`||`运算符可以为变量设置默认值。

```
// 普通写法
let name;
if (user?.name) \\{
  name = user.name;
\\} else \\{
  name = "Anonymous";
\\}

// 简写方法
const name = user?.name || "Anonymous";
```



### 用 && 替换 if true 语句

```
  // 普通
  if (callback) \\{ callback() \\}

  // 简写
  callback && callback()
```



### 使用数组解构交换值

> 交换值从未如此简单

```
  let a = 5, b = 8;
  // 普通
  let c = a, a = b, b = c;

  // 简写
  [a, b] = [b, a]
```



### 消除小数点

> 使用“~~”来消除值的小数，有助于提高性能

```
  // 普通
  math.round(math.random * 100)

  // 简单
  ~~ (math.random * 100)
```



### 逗号运算符

> 逗号运算符 (,) 从左到右并返回最后一个操作数的值

```
  for(let i = 0, j = 0; i < 10, j < 6; i++, j++) \\{
    console.log(i + j) 
  \\}
```



### 合并数组

> Array.concat() 函数会在创建单独的新数组时消耗大量内存

```
  var array1 = [1, 2, 3],
      array2 = [4, 5, 6];

  // 普通
  array1.concat(array2)

  // 更优
  Array.push.apply(arr1, arr2)
```

#### 这两种方式，哪个更好 

```
listData.value = listData.value.concat(dataist)
listData.value.push(...dataist)
```

当你需要将 `dataist` 数组的元素追加到 `listData.value` 数组时，可以使用 `concat()` 方法或者 `push(...dataist)` 方法。这两种方法各有优缺点，具体取决于你的需求。

##### 1. `listData.value = listData.value.concat(dataist)`

这种方法不会直接修改 `listData.value`，而是创建了一个新的数组，并将这个新数组赋值给 `listData.value`。这样做的好处是，原始数组 `listData.value` 不会被改变，因此这种方法适用于需要保持原始数组不变的情况。

```javascript
listData.value = listData.value.concat(dataist);
```

##### 2. `listData.value.push(...dataist)`

这种方法直接在 `listData.value` 上进行操作，将 `dataist` 中的所有元素追加到 `listData.value` 的末尾。这种方法会修改 `listData.value`，但通常效率更高，因为不需要创建新的数组。

```javascript
listData.value.push(...dataist);
```

##### 性能和内存影响

- **内存使用**: `concat()` 方法会产生一个新的数组对象，这意味着需要额外的内存空间来存储这个新数组。而 `push(...dataist)` 只是在现有的数组上进行操作，没有额外的内存开销。
- **执行速度**: `push(...dataist)` 通常比 `concat()` 快，因为 `push` 是就地操作，而 `concat` 需要创建新数组并复制元素。

##### 适用场景

- 如果你不需要保留原始数组 `listData.value` 的状态，并且希望提高性能，那么使用 `push(...dataist)` 更好。常用于移动端下拉加载新数据
- 如果你需要保留原始数组 `listData.value` 的状态，并且不介意额外的内存开销，那么使用 `concat()` 更合适。

##### 示例代码

假设 `listData.value` 是一个可变状态，我们可以通过以下方式更新它：

```javascript
let listData = \\{ value: [1, 2, 3] \\};
let dataist = [4, 5, 6];

// 使用 concat
listData.value = listData.value.concat(dataist);
console.log(listData.value); // 输出: [1, 2, 3, 4, 5, 6]

// 使用 push
listData.value = [1, 2, 3]; // 重置回初始状态
listData.value.push(...dataist);
console.log(listData.value); // 输出: [1, 2, 3, 4, 5, 6]
```

综上所述，如果你可以修改 `listData.value` 并且希望提高性能，建议使用 `push(...dataist)`；如果你需要保持 `listData.value` 的原始状态，可以选择 `listData.value = listData.value.concat(dataist)`。



### 获取数组中的最后一项

> slice是跟聪明的选择

```
  let  array = [1, 2, 3, 4, 5, 6]; 

  // 普通
   array[array.length - 1]

  // 简写
  array.slice(-1)
```



### 数组进行排序

> 内置的方法sort()是个不错的解决方案

- 排序字符串数组

  ```
    const stringArr = ["Joe", "Kapil", "Steve", "Musk"]
    stringArr.sort();
    // log: ["Joe", "Kapil", "Musk", "Steve"]
  ```

- 排序数字数组

  ```
    const array  = [40, 100, 1, 5, 25, 10];
    array.sort((a,b) => a-b);
    // log: [1, 5, 10, 25, 40, 100]
  
    array.sort((a,b) => b-a);
    // log: [100, 40, 25, 10, 5, 1]
  ```

- 排序对象数组

  ```
    const objectArr = [ 
      \\{ first_name: 'Lazslo', last_name: 'Jamf'     \\},
      \\{ first_name: 'Pig',    last_name: 'Bodine'   \\},
      \\{ first_name: 'Pirate', last_name: 'Prentice' \\}
    ];
    objectArr.sort((a, b) => a.last_name.localeCompare(b.last_name));
  
    // log: [\\{…\\}, \\{…\\}, \\{…\\}]
    0: \\{first_name: "Pig", last_name: "Bodine"\\}
    1: \\{first_name: "Lazslo", last_name: "Jamf"\\}
    2: \\{first_name: "Pirate", last_name: "Prentice"\\}
    length: 3
  ```







# if-else优化小技巧

### 短路运算💻

Javascript 的逻辑或 `||` 的短路运算有时候可以用来代替一些比较简单的 `if else`

- 逻辑或 `||` 的短路运算：**若左边能转成true**，返回左边式子的值，反之返回右边式子的值。

给一个变量分配的值是通过判断其值是否为null或undefined 

下面用一个简单的案例来表述

```
let c
if(a)\\{
    c = a
\\} else \\{
    c = b
\\}
```

可以用短路运算去简化我们的代码🙂。

```
let c = a || b
```

这样看起来是不是就简洁了很多😕。



### 三元运算符🎶

三元运算符我觉得大家应该都很熟悉吧，很多时候简单的一些判断我们都可以使用三元运算符去替代 `if else`，这里只推荐 **一层** 三元运算符，因为多层嵌套的三元运算符也不具备良好的可读性。

例子：条件为 true 时返回1，反之返回0：

```
const fn = (nBoolean) \\{
    if (nBoolean) \\{
        return 1
    \\} else \\{
        return 0
    \\}
    
\\}

// 使用三元运算符
const fn = (nBoolean) \\{
    return nBoolean ? 1 : 0
\\}
```

三元运算符使用的地方也比较多，比如：条件赋值，递归...

```
// num值在nBoolean为true时为10，否则为5
let num = nBoolean ? 10 : 5

// 求0-n之间的整数的和
let sum = 0;
function add(n)\\{
    sum += n
    return n >= 2 ? add(n - 1) : result;
\\};
let num = add(10);//55
```



### switch case🖥️

上述的两种方式：短路运算跟三元运算虽然很好用，代码也很简洁，不过都只能用于简单的判断，遇到多重条件判断就不能使用了😭。

对于 `switch case`，虽然它的可读性确实比 `else if` 更高，但是我想大家应该都觉得它写起来比较麻烦吧😣（反正我觉得很麻烦😺）。

例：有A、B、C、D四种种类型，在A、B的时候输出1，C输出2、D输出3，默认输出0。

```
let type = 'A'

//if else if
if (type === 'A' || type === 'B') \\{
    console.log(1);
\\} else if (type === 'C') \\{
    console.log(2);
\\} else if(type === 'D') \\{
    console.log(3);
\\} else \\{
    console.log(0)
\\}

//switch case
switch (type) \\{
    case 'A':
    case 'B':
        console.log(1)
        break
    case 'C':
        console.log(2)
        break
    case 'D':
        console.log(3);
        break;
    default:
        console.log(0)
\\}
```



### 对象配置/策略模式📑

对象配置看起来跟 `策略模式` 差不多，都是根据不同得参数使用不同得数据/算法/函数。😺

策略模式就是将一系列算法封装起来，并使它们相互之间可以替换。被封装起来的算法具有独立性，外部不可改变其特性。

接下来我们用对象配置的方法实现一下上述的例子

```
let type = 'A'

let tactics = \\{
    'A': 1,
    'B': 1,
    'C': 2,
    'D': 3,
    default: 0
\\}
console.log(tactics[type]) // 1
```

接下来用几个例子让大家更加熟悉一点。

#### 案例1 商场促销价🙋

根据不同的用户使用不同的折扣，如：普通用户不打折，普通会员用户9折，年费会员8.5折，超级会员8折。

使用`if else`实现😢

```
// 获取折扣 --- 使用if else
const getDiscount = (userKey) => \\{
    if (userKey === '普通会员') \\{
        return 0.9
    \\} else if (userKey === '年费会员') \\{
        return 0.85
    \\} else if (userKey === '超级会员') \\{
        return 0.8
    \\} else \\{
        return 1
    \\}
\\}
console.log(getDiscount('普通会员')) // 0.9
```

使用对象配置/策略模式实现🙂

```
// 获取折扣 -- 使用对象配置/策略模式
const getDiscount = (userKey) => \\{
    // 我们可以根据用户类型来生成我们的折扣对象
    let discounts = \\{
        '普通会员': 0.9,
        '年费会员': 0.85,
        '超级会员': 0.8,
        'default': 1
    \\}
    return discounts[userKey] || discounts['default']
\\}
console.log(getDiscount('普通会员')) // 0.9
```

从上面的案列中可以明显看得出来，使用对象配置比使用if else可读性更高，后续如果需要添加用户折扣也只需要修改折扣对象就行👍。

对象配置不一定非要使用对象去管理我们键值对，还可以使用 `Map`去管理🦋，如：

```
// 获取折扣 -- 使用对象配置/策略模式
const getDiscount = (userKey) => \\{
    // 我们可以根据用户类型来生成我们的折扣对象
    let discounts = new Map([
        ['普通会员', 0.9],
        ['年费会员', 0.85],
        ['超级会员', 0.8],
        ['default', 1]
    ])
    return discounts.get(userKey) || discounts.get('default')
\\}
console.log(getDiscount('普通会员')) // 0.9
```

#### 案例2 年终奖🏆

公司的年终奖根据员工的工资基数和绩效等级来发放的。例如，绩效为A的人年终奖有4倍工资，绩效为B的有3倍，绩效为C的只有2倍。

假如财务部要求我们提供一段代码来实现这个核算逻辑，我们要怎么实现呢？

这不是很简单嘛，一个函数就搞定了。

```
const calculateBonus = (performanceLevel, salary) => \\{ 
    if (performanceLevel === 'A')\\{
        return salary * 4
    \\}
    if (performanceLevel === 'B')\\{
        return salary * 3
    \\}
    if (performanceLevel === 'C')\\{
        return salary * 2
    \\}
\\}
calculateBonus( 'B', 20000 ) // 输出：60000
```

可以发现，这段代码十分简单，但是 `calculateBonus`函数比较庞大，所有的逻辑分支都包含在`if else`语句中，如果增加了一种新的绩效等级D，或者把A等级的倍数改成5，那我们必须阅读所有代码才能去做修改🙇‍♂️。

所以我们可以用对象配置/策略模式去简化这个函数😺

```
let strategies = new Map([
    ['A', 4],
    ['B', 3],
    ['C', 2]
])
const calculateBonus = (performanceLevel, salary) => \\{ 
    return strategies.get(performanceLevel) * salary
\\}
calculateBonus( 'B', 20000 ) // 输出：60000
```

至此，这个需求做完了，然后产品经理说要加上一个部门区分，假设公司有两个部门D和F，D部门的业绩较好，所以年终奖翻1.2倍😄，F部门的业绩较差，年终奖打9折😭。

改造以上代码，把状态值拼接，然后存入Map中

```
// 以绩效_部门的方式拼接键值存入
let strategies = new Map([
    ['A_D', 4 * 1.2],
    ['B_D', 3 * 1.2],
    ['C_D', 2 * 1.2],
    ['A_F', 4 * 0.9],
    ['B_F', 3 * 0.9],
    ['C_F', 2 * 0.9]
])
const calculateBonus = (performanceLevel, salary, department) => \\{ 
    return strategies.get(`$\\{performanceLevel\\}_$\\{department\\}`) * salary
\\}
calculateBonus( 'B', 20000, 'D' ) // 输出：72000
```

[原文](https://mp.weixin.qq.com/s/yOH5leewrH8zBY-2MFVxIw)

#### 案例3 v-if在视图优化

原版代码

```
<view class="title" v-if="item.type===1">业务</view>
<view class="title" v-else-if="item.type===2">差旅</view>
<view class="title" v-else-if="item.type===3">外出</view>
<view class="title" v-else-if="item.type===4">接送</view>
<view class="title" v-else="\\\{\\\{item.type===\\\}\\\}5}}">其他</view>
```

优化后

```
<view class="title">\\\{\\\{typeList[item.type\\\}\\\}]}}</view>

typeList: [
    "",
    "业务",
    "差旅",
    "外出",
    "接送",
    "其他",
],
```







# 34种JS优化技巧

### 1、 带有多个条件的 if 语句

把多个值放在一个[数组](https://so.csdn.net/so/search?q=数组&spm=1001.2101.3001.7020)中，然后调用数组的 includes 方法。

```js
//longhand
if (x === 'abc' || x === 'def' || x === 'ghi' || x ==='jkl') \\{
    //logic
\\}
//shorthand
if (['abc', 'def', 'ghi', 'jkl'].includes(x)) \\{
   //logic
\\}
```

```
// 原版
if (userInfo.saas_state === 2 && (name !== "home-page" && name !== "staff-list" && name !== "staff-car-list" && name !== "travel-record" && name !== "add-travel-record" && name !== "my-export-page")) \\{
          this.isShow = true
        \\} else \\{
          this.isShow = false
        \\}
        
// 简写
        if (userInfo.saas_state === 2 && !['home-page', 'staff-list', 'staff-car-list', 'travel-record', 'add-travel-record', "my-export-page"].includes(name)) \\{
          this.isShow = true
        \\} else \\{
          this.isShow = false
        \\}
```



### 2、简化 if true…else

对于不包含大逻辑的 if-else 条件，可以使用下面的快捷写法。我们可以简单地使用三元运算符来实现这种简化。

```js
// Longhand
let test: boolean;
if (x > 100) \\{
    test = true;
\\} else \\{
    test = false;
\\}
// Shorthand
let test = (x > 10) ? true : false;
//或者我们也可以直接用
let test = x > 10;
console.log(test);
```

如果有嵌套的条件，可以这么做。

```js
let x = 300,
test2 = (x > 100) ? 'greater than 100' : (x < 50) ? 'less 50' : 'between 50 and 100';
console.log(test2); // "greater than 100"
```



### 3、声明变量

当我们想要声明两个具有相同的值或相同类型的变量时，可以使用这种简写。

```js
//Longhand 
let test1;
let test2 = 1;
//Shorthand 
let test1, test2 = 1;
```



### 4、null、undefined 和空值检查

当我们创建了新变量，有时候想要检查引用的变量是不是为非 null 或 undefined。

JavaScript 确实有一个很好的快捷方式来实现这种检查。

```js
// Longhand
if (test1 !== null || test1 !== undefined || test1 !== '') \\{
    let test2 = test1;
\\}
// Shorthand
let test2 = test1 || '';
```



### 5、null 检查和默认赋值

```js
let test1 = null,
    test2 = test1 || '';
console.log("null check", test2); // 输出 ""
```



### 6、undefined 检查和默认赋值

```js
let test1 = undefined,
    test2 = test1 || '';
console.log("undefined check", test2); // 输出 ""
```

一般值检查

```js
let test1 = 'test',
    test2 = test1 || '';
console.log(test2); // 输出: 'test'
```

另外，对于上述的 4、5、6 点，都可以使用?? 操作符。

如果左边值为 null 或 undefined，就返回右边的值。默认情况下，它将返回左边的值。

```js
const test= null ?? 'default';
console.log(test);
// 输出结果: "default"
const test1 = 0 ?? 2;
console.log(test1);
// 输出结果: 0
```



### 7、给多个变量赋值

当我们想给多个不同的变量赋值时，这种技巧非常有用。

```js
//Longhand 
let test1, test2, test3;
test1 = 1;
test2 = 2;
test3 = 3;
//Shorthand 
let [test1, test2, test3] = [1, 2, 3];
```



### 8、简便的赋值操作符

在编程过程中，我们要处理大量的算术运算符。这是 JavaScript 变量赋值操作符的有用技巧之一。

```js
// Longhand
test1 = test1 + 1;
test2 = test2 - 1;
test3 = test3 * 20;
// Shorthand
test1++;
test2--;
test3 *= 20;
```



### 9、 if 判断值是否存在

这是我们都在使用的一种常用的简便技巧，在这里仍然值得再提一下。

```js
// Longhand
if (test1 === true) or if (test1 !== "") or if (test1 !== null)
// Shorthand //检查空字符串、null或者undefined
if (test1)
```

注意：如果 test1 有值，将执行 if 之后的逻辑，这个操作符主要用于 null 或 undefinded 检查。



### 10、 用于多个条件判断的 && 操作符

如果只在变量为 true 时才调用函数，可以使用 && 操作符。

```js
//Longhand 
if (test1) \\{
 callMethod(); 
\\} 
//Shorthand 
test1 && callMethod();
```



### 11、for each 循环

这是一种常见的循环简化技巧。

```js
// Longhand
for (var i = 0; i < testData.length; i++)
// Shorthand
for (let i in testData) or  for (let i of testData)
```

遍历数组的每一个变量。

```js
function testData(element, index, array) \\{
  console.log('test[' + index + '] = ' + element);
\\}
[11, 24, 32].forEach(testData);
// logs: test[0] = 11, test[1] = 24, test[2] = 32
```



### 12、比较后返回

我们也可以在 return 语句中使用比较，它可以将 5 行代码减少到 1 行。

```js
// Longhand
let test;
function checkReturn() \\{
    if (!(test === undefined)) \\{
        return test;
    \\} else \\{
        return callMe('test');
    \\}
\\}
var data = checkReturn();
console.log(data); //output test
function callMe(val) \\{
    console.log(val);
\\}
// Shorthand
function checkReturn() \\{
    return test || callMe('test');
\\}
```



### 13、 箭头函数

```js
//Longhand 
function add(a, b) \\{ 
   return a + b; 
\\} 
//Shorthand 
const add = (a, b) => a + b;
```

**更多例子：**

```js
function callMe(name) \\{
  console.log('Hello', name);
\\}
callMe = name => console.log('Hello', name)
```



### 14、简短的函数调用

我们可以使用三元操作符来实现多个函数调用。

```js
// Longhand
function test1() \\{
  console.log('test1');
\\};
function test2() \\{
  console.log('test2');
\\};
var test3 = 1;
if (test3 == 1) \\{
  test1();
\\} else \\{
  test2();
\\}
// Shorthand
(test3 === 1? test1:test2)();
```

```
const x = 20;
let answer;
if (x > 10) \\{
    answer = 'is greater';
\\} else \\{
    answer = 'is lesser';
\\}

// 简写
const answer = x > 10 ? 'is greater' : 'is lesser';
```



### 15、switch 简化

我们可以将条件保存在键值对象中，并根据条件来调用它们。

```js
// Longhand
switch (data) \\{
  case 1:
    test1();
  break;
  case 2:
    test2();
  break;
  case 3:
    test();
  break;
  // ...
\\}
// Shorthand
var data = \\{
  1: test1,
  2: test2,
  3: test
\\};
data[something] && data[something]();
```



### 16、隐式返回

通过使用箭头函数，我们可以直接返回值，不需要 return 语句。

```js
//longhand
function calculate(diameter) \\{
  return Math.PI * diameter
\\}
//shorthand
calculate = diameter => (
  Math.PI * diameter;
)
```



### 17、 指数表示法

```js
/// Longhand
for (var i = 0; i < 10000; i++) \\{ ... \\}
// Shorthand
for (var i = 0; i < 1e4; i++) \\{
```



### 18、默认参数值

```js
//Longhand
function add(test1, test2) \\{
  if (test1 === undefined)
    test1 = 1;
  if (test2 === undefined)
    test2 = 2;
  return test1 + test2;
\\}
//shorthand
add = (test1 = 1, test2 = 2) => (test1 + test2);
add() //输出结果: 3
```



### 19、延展操作符简化

```js
//longhand
// 使用concat连接数组
const data = [1, 2, 3];
const test = [4 ,5 , 6].concat(data);
//shorthand
// 连接数组
const data = [1, 2, 3];
const test = [4 ,5 , 6, ...data];
console.log(test); // [ 4, 5, 6, 1, 2, 3]
```

我们也可以使用延展操作符进行克隆。

```js
//longhand
// 克隆数组
const test1 = [1, 2, 3];
const test2 = test1.slice()
//shorthand
//克隆数组
const test1 = [1, 2, 3];
const test2 = [...test1];
```



### 20. 模板字面量

如果你厌倦了使用 + 将多个变量连接成一个字符串，那么这个简化技巧将让你不再头痛。

```js
//longhand
const welcome = 'Hi ' + test1 + ' ' + test2 + '.'
//shorthand
const welcome = `Hi $\\{test1\\} $\\{test2\\}`;
```



### 21. 跨行字符串

当我们在代码中处理跨行字符串时，可以这样做。

```js
//longhand
const data = 'abc abc abc abc abc abc\n\t'
    + 'test test,test test test test\n\t'
//shorthand
const data = `abc abc abc abc abc abc
         test test,test test test test`
```



### 22. 对象属性赋值

```js
let test1 = 'a'; 
let test2 = 'b';
//Longhand 
let obj = \\{
    test1: test1, 
    test2: test2
\\}; 
//Shorthand 
let obj = \\{
    test1, 
    test2
\\};
```



### 23. 将字符串转成数字

```js
//Longhand 
let test1 = parseInt('123'); 
let test2 = parseFloat('12.3'); 
//Shorthand 
let test1 = +'123'; 
let test2 = +'12.3';
```



### 24. 解构赋值

解构赋值是一种表达式，用于从数组或对象中快速提取属性值，并赋给定义的变量。

在代码简写方面，解构赋值能达到很好的效果。

#### 案例1

**普通写法：**

在处理数组时，我们有时需要将数组“解包”成一堆变量，如下所示：

```ini
let apples = ['🍎', '🍏'];
let redApple = apples[0];
let greenApple = apples[1];

console.log( redApple );    //=> 🍎
console.log( greenApple );  //=> 🍏
```

**简写写法：**

我们可以通过解构赋值用一行代码实现相同的结果：

```ini
let apples = ['🍎', '🍏'];
let [redApple, greenApple] = apples;  // <-- here

console.log( redApple );    //=> 🍎
console.log( greenApple );  //=> 🍏
```

#### 案例2

普通：

```
const observable = require('mobx/observable');
const action = require('mobx/action');
const runInAction = require('mobx/runInAction');
const store = this.props.store;
const form = this.props.form;
const loading = this.props.loading;
const errors = this.props.errors;
const entity = this.props.entity;
```

简写为：

```
import \\{ observable, action, runInAction \\} from 'mobx';
const \\{ store, form, loading, errors, entity \\} = this.props;
```

甚至可以指定自己的变量名：

```
const \\{ store, form, loading, errors, entity:contact \\} = this.props;
```

#### 案例3

```js
//longhand
const test1 = this.data.test1;
const test2 = this.data.test2;
const test2 = this.data.test3;
//shorthand
const \\{ test1, test2, test3 \\} = this.data;
```

#### 对比

哪个写法更好

```
const detail = shareItem.value
  if (detail.productCode) \\{
    productInfo.contentId = detail.contentBaseId
    productInfo.productCode = detail.productCode
  \\}

const \\{contentBaseId,productCode\\} = shareItem.value
  if (detail.productCode) \\{
    productInfo.contentId = contentBaseId
    productInfo.productCode = productCode
  \\}
```

从性能的角度来看，两种写法的差异非常微小，几乎可以忽略不计。现代JavaScript引擎对这两种操作都进行了高度优化，因此在实际应用中，它们的执行效率是非常接近的。

##### 性能分析

1. **第一种写法**
   
   ```javascript
   const detail = shareItem.value;
   if (detail.productCode) \\{
     productInfo.contentId = detail.contentBaseId;
     productInfo.productCode = detail.productCode;
   \\}
   ```
```
   
2. **第二种写法**
   
   ```javascript
   const \\{ contentBaseId, productCode \\} = shareItem.value;
   if (productCode) \\{
     productInfo.contentId = contentBaseId;
     productInfo.productCode = productCode;
   \\}
```

###### 具体分析

- **内存分配**：
  - 第一种写法：创建了一个新的 `detail` 对象引用。
  - 第二种写法：直接解构赋值，没有创建新的对象引用。

- **访问属性**：
  - 第一种写法：需要两次访问 `detail` 对象的属性（`contentBaseId` 和 `productCode`）。
  - 第二种写法：直接解构赋值，只需要一次访问 `shareItem.value`。

- **执行步骤**：
  - 第一种写法：多了一步创建 `detail` 变量。
  - 第二种写法：直接解构赋值，减少了中间步骤。

##### 结论

虽然从理论上讲，第二种写法可能会稍微快一些，因为少了创建 `detail` 变量的步骤，但在实际应用中，这种性能差异几乎可以忽略不计。现代JavaScript引擎的优化能力很强，能够高效地处理这两种情况。

因此，从性能的角度来看，两种写法都可以接受，但从代码的可读性和简洁性考虑，推荐使用第二种写法。



### 25. 数组 find 简化

当我们有一个对象数组，并想根据对象属性找到特定对象，find 方法会非常有用。

```js
const data = [\\{
        type: 'test1',
        name: 'abc'
    \\},
    \\{
        type: 'test2',
        name: 'cde'
    \\},
    \\{
        type: 'test1',
        name: 'fgh'
    \\},
]
function findtest1(name) \\{
    for (let i = 0; i < data.length; ++i) \\{
        if (data[i].type === 'test1' && data[i].name === name) \\{
            return data[i];
        \\}
    \\}
\\}
//Shorthand
filteredData = data.find(data => data.type === 'test1' && data.name === 'fgh');
console.log(filteredData); // \\{ type: 'test1', name: 'fgh' \\}
```



### 26. 条件查找简化

如果我们要基于不同的类型调用不同的方法，可以使用多个 else if 语句或 switch，但有没有比这更好的简化技巧呢？

```js
// Longhand
if (type === 'test1') \\{
  test1();
\\}
else if (type === 'test2') \\{
  test2();
\\}
else if (type === 'test3') \\{
  test3();
\\}
else if (type === 'test4') \\{
  test4();
\\} else \\{
  throw new Error('Invalid value ' + type);
\\}
// Shorthand
var types = \\{
  test1: test1,
  test2: test2,
  test3: test3,
  test4: test4
\\};
var func = types[type];
(!func) && throw new Error('Invalid value ' + type); func();
```



### 27. indexOf 的按位操作简化

在查找数组的某个值时，我们可以使用 indexOf() 方法。但有一种更好的方法，让我们来看一下这个例子。

```js
//longhand
if(arr.indexOf(item) > -1) \\{ // item found 
\\}
if(arr.indexOf(item) === -1) \\{ // item not found
\\}
//shorthand
if(~arr.indexOf(item)) \\{ // item found
\\}
if(!~arr.indexOf(item)) \\{ // item not found
\\}
```

按位 ( ~ ) 运算符将返回 true（-1 除外），反向操作只需要!~。另外，也可以使用 include() 函数。

```js
if (arr.includes(item)) \\{ 
// 如果找到项目，则为true
\\}
```



### 28. Object.entries()

这个方法可以将对象转换为对象数组。

```js
const data = \\{ test1: 'abc', test2: 'cde', test3: 'efg' \\};
const arr = Object.entries(data);
console.log(arr);
/** Output:
[ [ 'test1', 'abc' ],
  [ 'test2', 'cde' ],
  [ 'test3', 'efg' ]
]
**/
```



### 29. Object.values()

这也是 ES8 中引入的一个新特性，它的功能类似于 Object.entries()，只是没有键。

```js
const data = \\{ test1: 'abc', test2: 'cde' \\};
const arr = Object.values(data);
console.log(arr);
/** Output:
[ 'abc', 'cde']
**/
```



### 30. 双重按位操作

```js
// Longhand
Math.floor(1.9) === 1 // true
// Shorthand
~~1.9 === 1 // true
```



### 31. 重复字符串多次

为了重复操作相同的字符，我们可以使用 for 循环，但其实还有一种简便的方法。

```js
//longhand 
let test = ''; 
for(let i = 0; i < 5; i ++) \\{ 
  test += 'test '; 
\\} 
console.log(str); // test test test test test 
//shorthand 
'test '.repeat(5);
```



### 32. 查找数组的最大值和最小值

```js
const arr = [1, 2, 3]; 
Math.max(…arr); // 3
Math.min(…arr); // 1
```



### 33. 获取字符串的字符

```js
let str = 'abc';
//Longhand 
str.charAt(2); // c
//Shorthand 
str[2]; // c
```



### 34. 指数幂简化

```js
//longhand
Math.pow(2,3); // 8
//shorthand
2**3 // 8
```

[原文](https://blog.csdn.net/weixin_42609002/article/details/124422277)







# JavaScript简写技巧

![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2017/10/30/f0d760dd019d1495146fae8bd9ce706b~tplv-t2oaga2asx-jj-mark:3024:0:0:0:q75.awebp)



> 原文出处： [Michael Wanyoike](https://www.sitepoint.com/shorthand-javascript-techniques/)   译文出处：[葡萄城控件](http://www.cnblogs.com/powertoolsteam/p/shorthand-javascript.html)

本文来源于多年的 JavaScript 编码技术经验，适合所有正在使用 JavaScript 编程的开发人员阅读。

本文的目的在于帮助大家更加熟练的运用 JavaScript 语言来进行开发工作。

文章将分成初级篇和高级篇两部分，分别进行介绍。

# 初级篇

## 1. 三目运算符

下面是一个很好的例子，将一个完整的 if 语句，简写为一行代码。

```
const x = 20;
let answer;
    if (x > 10) \\{
    answer = 'greater than 10';
\\} else \\{
    answer = 'less than 10';
\\}
```

简写为：

```
const answer = x > 10 ? 'greater than 10' : 'less than 10';
```

## 2. 循环语句

当使用纯 JavaScript（不依赖外部库，如 jQuery 或 lodash）时，下面的简写会非常有用。

```
for (let i = 0; i< allImgs.length; i++)
```

简写为：

```
for (let index of allImgs)
```

下面是遍历数组 forEach 的简写示例：

```
function logArrayElements(element, index, array) \\{
    console.log("a[" + index + "] = " + element);
\\}
[2, 5, 9].forEach(logArrayElements);
# logs:
    # a[0] = 2
    # a[1] = 5
    # a[2] = 9
```

## 3. 声明变量

在函数开始之前，对变量进行赋值是一种很好的习惯。在申明多个变量时：

```
let x;
let y;
let z = 3;
```

可以简写为：

let x, y, z=3;

## 4. if 语句

在使用 if 进行基本判断时，可以省略赋值运算符。

```
if (likeJavaScript === true)
```

简写为：

```
if (likeJavaScript)
```

## 5. 十进制数

可以使用科学计数法来代替较大的数据，如可以将 10000000 简写为 1e7。

```
for (let i = 0; i<10000000;i++)\\{\\}
```

简写为：

```
for (let i = 0; i<1e7; i++) \\{ \\}
```

## 6. 多行字符串

如果需要在代码中编写多行字符串，就像下面这样：

```
const lorem = 'Lorem ipsum dolor sit amet, consectetur\n\t'
    + 'adipisicing elit, sed do eiusmod tempor incididunt\n\t'
    + 'ut labore et dolore magna aliqua. Ut enim ad minim\n\t'
    + 'veniam, quis nostrud exercitation ullamco laboris\n\t'
    + 'nisi ut aliquip ex ea commodo consequat. Duis aute\n\t'
    + 'irure dolor in reprehenderit in voluptate velit esse.\n\t'
```

但是还有一个更简单的方法，只使用引号：

```
const lorem = `Lorem ipsum dolor sit amet, consectetur
    adipisicing elit, sed do eiusmod tempor incididunt
    ut labore et dolore magna aliqua. Ut enim ad minim
    veniam, quis nostrud exercitation ullamco laboris
    nisi ut aliquip ex ea commodo consequat. Duis aute
    irure dolor in reprehenderit in voluptate velit esse.`
```



# 高级篇

### 1. 变量赋值

当将一个变量的值赋给另一个变量时，首先需要确保原值不是 null、未定义的或空值。

可以通过编写一个包含多个条件的判断语句来实现：

```
if (variable1 !== null || variable1 !== undefined || variable1 !== '') \\{
    let variable2 = variable1;
\\}
```

或者简写为以下的形式：

```
const variable2 = variable1  || 'new';
```

可以将下面的代码粘贴到 es6console 中，自己测试：

```
let variable1;
let variable2 = variable1  || '';
console.log(variable2 === ''); // prints true
variable1 = 'foo';
variable2 = variable1  || '';
console.log(variable2); #  prints foo
```

## 2. 默认值赋值

如果预期参数是 null 或未定义，则不需要写六行代码来分配默认值。我们可以只使用一个简短的逻辑运算符，只用一行代码就能完成相同的操作。

```
let dbHost;
  if (process.env.DB_HOST) \\{
    dbHost = process.env.DB_HOST;
\\} else \\{
    dbHost = 'localhost';
\\}
```

简写为：

```
const dbHost = process.env.DB_HOST || 'localhost';
```

## 3. 对象属性

ES6 提供了一个很简单的办法，来分配属性的对象。如果属性名与 key 名相同，则可以使用简写。

```
const obj = \\{ x:x, y:y \\};
```

简写为：

```
const obj = \\{ x, y \\};
```

## 4. 箭头函数

经典函数很容易读写，但是如果把它们嵌套在其它函数中进行调用时，整个函数就会变得有些冗长和混乱。这时候可以使用箭头函数来简写：

```
function sayHello(name) \\{
    console.log('Hello', name);
\\}

setTimeout(function() \\{
    console.log('Loaded')
\\}, 2000);

list.forEach(function(item) \\{
    console.log(item);
\\});
```

简写为：

```
sayHello = name => console.log('Hello', name);
setTimeout(() => console.log('Loaded'), 2000);
list.forEach(item => console.log(item));
```

## 5. 隐式返回值

返回值是我们通常用来返回函数最终结果的关键字。

只有一个语句的箭头函数，可以隐式返回结果（函数必须省略括号（\\{ \\}），以便省略返回关键字）。

要返回多行语句（例如对象文本），需要使用（）而不是\\{ \\}来包裹函数体。这样可以确保代码以单个语句的形式进行求值。

```
function calcCircumference(diameter) \\{
    return Math.PI * diameter
\\}
```

简写为：

```
calcCircumference = diameter => (
    Math.PI * diameter;
)
```

## 6. 默认参数值

可以使用 if 语句来定义函数参数的默认值。ES6 中规定了可以在函数声明中定义默认值。

```
function volume(l, w, h) \\{
    if (w === undefined)
    w = 3;
if (h === undefined)
     h = 4;
return l * w * h;
```

\\}

简写为：

```
volume = (l, w = 3, h = 4 ) => (l * w * h);
volume(2) //output: 24
```

## 7. 模板字符串

过去我们习惯了使用“+”将多个变量转换为字符串，但是有没有更简单的方法呢？

ES6 提供了相应的方法，我们可以使用反引号和 $ \\{ \\} 将变量合成一个字符串。

```
const welcome = 'You have logged in as ' + first + ' ' + last + '.'
const db = 'http://' + host + ':' + port + '/' + database;
```

简写为：

```
const welcome = `You have logged in as $\\{first\\} $\\{last\\}`;
const db = `http://$\\{host\\}:$\\{port\\}/$\\{database\\}`;
```

## 9. 展开运算符

展开运算符是在 ES6 中引入的，使用展开运算符能够让 JavaScript 代码更加有效和有趣。

使用展开运算符可以替换某些数组函数。

```
# joining arrays
const odd = [1, 3, 5];
const nums = [2 ,4 , 6].concat(odd);

# cloning arrays
const arr = [1, 2, 3, 4];
const arr2 = arr.slice( )
```

简写为：

```
# joining arrays
const odd = [1, 3, 5 ];
const nums = [2 ,4 , 6, ...odd];
console.log(nums); // [ 2, 4, 6, 1, 3, 5 ]

# cloning arrays
const arr = [1, 2, 3, 4];
const arr2 = [...arr];
```

和 concat( ) 功能不同的是，用户可以使用扩展运算符在任何一个数组中插入另一个数组。

```
const odd = [1, 3, 5 ];
const nums = [2, ...odd, 4 , 6];
```

也可以将展开运算符和 ES6 解构符号结合使用：

```
const \\{ a, b, ...z \\} = \\{ a: 1, b: 2, c: 3, d: 4 \\};
console.log(a) // 1
console.log(b) // 2
console.log(z) // \\{ c: 3, d: 4 \\}
```

## 10. 强制参数

默认情况下，如果不向函数参数传值，那么 JavaScript 会将函数参数设置为未定义。其它一些语言则会发出警告或错误。要执行参数分配，可以使用if语句抛出未定义的错误，或者可以利用“强制参数”。

```
function foo(bar) \\{
    if(bar === undefined) \\{
    throw new Error('Missing parameter!');
\\}
return bar;
\\}
```

简写为：

```
mandatory = ( ) => \\{
    throw new Error('Missing parameter!');
\\}
foo = (bar = mandatory( )) => \\{
    return bar;
\\}
```

## 11. Array.find

如果你曾经编写过普通 JavaScript 中的 find 函数，那么你可能使用了 for 循环。在 ES6 中，介绍了一种名为 find（）的新数组函数，可以实现 for 循环的简写。

```
const pets = [
    \\{ type: 'Dog', name: 'Max'\\},
    \\{ type: 'Cat', name: 'Karl'\\},
    \\{ type: 'Dog', name: 'Tommy'\\},
]
function findDog(name) \\{
    for(let i = 0; ii) \\{
    if(pets[i].type === 'Dog' && pets[i].name === name) \\{
    return pets[i];
    \\}
\\}
\\}
```

简写为：

```
pet = pets.find(pet => pet.type ==='Dog' && pet.name === 'Tommy');
console.log(pet); // \\{ type: 'Dog', name: 'Tommy' \\}
```

## 12. Object [key]

虽然将 foo.bar 写成 foo [‘bar’] 是一种常见的做法，但是这种做法构成了编写可重用代码的基础。

请考虑下面这个验证函数的简化示例：

```
function validate(values) \\{
if(!values.first)
    return false;
if(!values.last)
    return false;
 return true;
\\}
console.log(validate(\\{first:'Bruce',last:'Wayne'\\})); // true
```

上面的函数完美的完成验证工作。但是当有很多表单，则需要应用验证，此时会有不同的字段和规则。如果可以构建一个在运行时配置的通用验证函数，会是一个好选择。

```
# object validation rules
const schema = \\{
first: \\{
    required:true
\\},
    last: \\{
    required:true
\\}
\\}
```

# universal validation function

```
const validate = (schema, values) => \\{
for(field in schema) \\{
    if(schema[field].required) \\{
    if(!values[field]) \\{
        return false;
    \\}
    \\}
\\}
return true;
\\}
console.log(validate(schema, \\{first:'Bruce'\\})); // false
console.log(validate(schema, \\{first:'Bruce',last:'Wayne'\\})); // true
```

现在有了这个验证函数，我们就可以在所有窗体中重用，而无需为每个窗体编写自定义验证函数。

## 13. 双位操作符

位操作符是 JavaScript 初级教程的基本知识点，但是我们却不常使用位操作符。因为在不处理二进制的情况下，没有人愿意使用 1 和 0。

但是双位操作符却有一个很实用的案例。你可以使用双位操作符来替代 Math.floor( )。双否定位操作符的优势在于它执行相同的操作运行速度更快。

```
Math.floor(4.9) === 4  //true
```

简写为：

```
~~4.9 === 4  //true
```

原文链接：https://juejin.cn/post/6844903507149979655







# 14 个 JavaScript 代码优化技巧

![14个 JavaScript 代码优化技巧](https://static001.infoq.cn/resource/image/c7/f7/c70568fc1e23038da0eacb27e0ba72f7.jpg)

**本文最初发布于 Medium 网站，经原作者授权由 InfoQ 中文站翻译并分享。**

JavaScript 已经成为有史以来最受欢迎的编程语言之一。根据 W3Tech 的数据，全世界将近 96％的网站都在使用它。关于 Web 有一个关键的事实是，你无法控制访问网站的用户所用设备的硬件规格。最终用户访问你的网站时，使用的可能是高端设备也可能是低端设备，网络连接条件也有好有差。这意味着你必须尽可能优化自己的网站，以满足任何用户的需求。

这篇文章列举了一些技巧，可帮助你写出更好的 JavaScript 代码，从而提高性能。

附带提一下，请共享和重用你的 JS 组件，以在高质量代码（写起来需要花费时间）和合理的交付时间之间保持适当的平衡。你可以使用 [Bit](https://github.com/teambit/bit)等流行工具将任何项目中的组件（普通 JS、TS、React、Vue 等）共享到 Bit 的组件中心，用不了多大功夫。



### 1、删除未使用的代码和功能

你的应用程序包含的代码越多，就需要将更多的数据传输到客户端。浏览器也需要更多时间来分析和解释代码。

有时，你可能打包了很多根本用不到的功能。最好只在开发环境中保留这些额外的代码，而不要将其推送到生产环境中，以免给客户端的浏览器增加负担。

要不断问自己，某个功能或代码段是否是必要的。

你可以手动移除未使用的代码，也可以使用 Uglify 或谷歌的 Closure Compiler 之类的工具删除它们。你甚至可以使用一种称为摇树优化的技术从应用程序中删除未使用的代码。Webpack 这类打包软件提供了这种技术，详情可以参考[这里](https://www.infoq.cn/article/dcKcJiT8aeEBNZbdotFF)。如果要删除未使用的 npm 软件包，可以使用命令 npm prune，详细信息参考[NPM文档](https://docs.npmjs.com/cli-commands/prune.html)。



### 2、尽可能缓存

缓存可以减少延迟和网络流量，从而减少了显示资源表示所需的时间，以提高网站的速度和性能。缓存可以借助 Cache API 或 HTTP caching 来实现。你可能想知道内容更改时会发生什么。当满足某些条件（例如发布新内容）时，上述缓存机制能够处理和重新生成缓存。



### 3、避免内存泄漏

作为一种高级语言，JS 会负责一些底层管理工作，例如内存管理。垃圾回收是大多数编程语言共有的过程。用外行术语来说，垃圾收集就是收集并释放已分配给对象，但目前尚未在程序的任何部分中使用的内存。在 C 这样的编程语言中，开发人员必须使用 malloc()和 dealloc()函数来处理内存分配和释放操作。

虽然在 JavaScript 中垃圾回收是自动执行的，但在某些情况下它也不是完美的。在 JavaScript ES6 中，引入了 Map 和 Set 及其“weaker”的同级对象。被称为 WeakMap 和 WeakSet 的“较弱”对应项持有对对象的“弱”引用。它们使未引用的值能够被垃圾回收，从而防止内存泄漏。你可以在此处阅读有关 WeakMaps 的[更多信息](https://blog.bitsrc.io/understanding-weakmaps-in-javascript-6e323d9eec81)。



### 4、尽早打破循环

超大循环肯定会消耗很多宝贵的时间，所以你应该尽早打破它们。你可以用 break 关键字和 continue 关键字来做这件事。编写最高效的代码是你的责任。

在下面的示例中，如果你没有从循环中 break，则你的代码将循环运行 1000000000 次，显然会过载的。

```
let arr = new Array(1000000000).fill('----');
arr[970] = 'found';
for (let i = 0; i < arr.length; i++) \\{
  if (arr[i] === 'found') \\{
        console.log("Found");
        break;
    \\}
\\}
```

在下面的示例中，如果你在循环不符合你的条件时没有 continue，则你仍将运行该函数 1000000000 次。我们仅在数组元素处于偶数位置时处理它。这将循环执行减少了近一半。

```
let arr = new Array(1000000000).fill('----');
arr[970] = 'found';
for (let i = 0; i < arr.length; i++) \\{
  if(i\\%2!=0)\\{
        continue;
    \\};
    process(arr[i]);
\\}
```

你可以在[此处](https://www.oreilly.com/library/view/high-performance-javascript/9781449382308/ch04.html)详细了解循环和性能的关系。



### 5、最小化变量计算的次数

为了减少计算变量的次数，可以使用闭包。通俗来说，JavaScript 中的闭包使你可以从内部函数访问外部函数作用域。每次创建函数（**不调用**）时都会创建闭包。内部函数将有权访问外部作用域的变量，即使在返回外部函数之后也是如此。

我们来看两个例子。这些示例均来自 Bret 的博客。

```
function findCustomerCity(name) \\{
  const texasCustomers = ['John', 'Ludwig', 'Kate']; 
  const californiaCustomers = ['Wade', 'Lucie','Kylie'];
  
  return texasCustomers.includes(name) ? 'Texas' : 
    californiaCustomers.includes(name) ? 'California' : 'Unknown';
\\};
```

如果你多次调用上面的函数，那么每次都会创建一个新对象。每次调用时，变量 texasCustomers 和 californiaCustomers 都会导致不必要的内存重分配。

```
function findCustomerCity() \\{
  const texasCustomers = ['John', 'Ludwig', 'Kate']; 
  const californiaCustomers = ['Wade', 'Lucie','Kylie'];
  
  return name => texasCustomers.includes(name) ? 'Texas' : 
    californiaCustomers.includes(name) ? 'California' : 'Unknown';
\\};
let cityOfCustomer = findCustomerCity();
cityOfCustomer('John');//Texas
cityOfCustomer('Wade');//California
cityOfCustomer('Max');//Unknown
```

在上面的示例中，借助于闭包，返回到变量 cityOfCustomer 的内部函数可以访问外部函数 findCustomerCity()的常量。而且，每当以传递的名称作为参数调用内部函数时，都无需再次实例化常量。要了解关于闭包的更多信息，建议你阅读 Prashant 的[博客文章](https://medium.com/@prashantramnyc/javascript-closures-simplified-d0d23fa06ba4)。



### 6、尽量减少 DOM 访问

与其他 JavaScript 语句相比，访问 DOM 的速度很慢。如果你对 DOM 进行更改，触发了布局的重新绘制，那么就得等好一阵子了。

为了减少访问 DOM 元素的次数，请先访问一次，然后将其用作局部变量。完成需求后，请一定将其设置为 null 来移除该变量的值。这将防止内存泄漏，因为这会触发垃圾回收过程。



### 7、压缩文件

通过压缩方法（例如 Gzip）可以减小 JavaScript 文件的大小。较小的文件会提升你的网站性能，因为浏览器只需下载较小的资产即可。

这类压缩手段最多可以减少 80％的文件大小。在此处阅读有关压缩的[更多信息](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/optimize-encoding-and-transfer#text_compression_with_gzip)。



### 8、缩小最终代码

有人认为缩小和压缩是相同的，其实不然。在压缩中，我们使用特殊算法来改变文件的输出大小；在缩小时，我们需要删除 JavaScript 文件中的注释和多余的空格。可以在网上找到许多工具和软件包来帮助完成这一过程。缩小已成为页面优化的标准做法，也是前端优化的主要步骤之一。

缩小可以让文件大小最多减少 60％。你可以在此处阅读有关缩小的[更多信息](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/optimize-encoding-and-transfer#minification_preprocessing_context-specific_optimizations)。



### 9、使用 Throttle（节流）和 Debounce（防抖）

我们可以使用这两种技术来严格控制代码需要处理事件的次数。

节流是指定函数可以超时的最大次数。例如，“每 1000 毫秒最多执行一次 onkeyup 事件函数”。也就是说哪怕你每秒敲 20 个键，该事件每秒也只会触发一次。这将减少代码的负担。

另一方面，防抖是指定自上次执行相同函数以来再次运行该函数的最短持续时间。换句话说，“上次调用函数后过最少 600 毫秒才执行此函数”。要了解有关节流和防抖的更多信息，这里有一篇[快速入门](https://css-tricks.com/the-difference-between-throttling-and-debouncing/)。

你可以实现自己的防抖和节流函数，也可以从 Lodash 和 Underscore 之类的库中导入它们。



### 10、避免使用 Delete 关键字

delete 关键字用于从对象中删除属性。这个关键字的性能表现不怎么好，预计它将在未来的更新中修复。

或者，你可以简单地将不需要的属性设置为 undefined。

```
const object = \\{name:"Jane Doe", age:43\\};
object.age = undefined;
```

你还可以使用 Map 对象，Bret 认为它的 delete 方法会更快。



### 11、使用异步代码防止线程阻塞

你应该知道 JavaScript 默认情况下是同步的和单线程的。但是在某些情况下，你的代码需要很大的计算量。代码本质上是同步的，意味着一段代码运行时将阻止其他代码语句运行，直到前者完成执行为止。这会降低整体性能。

但是我们可以通过异步代码来避免这种情况。异步代码以前以回调的形式编写，但是 ES6 引入了一种处理异步代码的新样式。这种新样式被称为 Promise。你可以在 MDN 的官方文档中了解有关回调和 Promise 的[更多信息](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Introducing)。

**可是等等……**

 JavaScript 默认情况下是同步的，并且也是单线程的。 

如何在单个线程上运行异步代码呢？这是很多人感到困惑的地方。做到这一点，主要依赖运行在浏览器后台的 JavaScript 引擎。JavaScript 引擎是执行 JavaScript 代码的计算机程序或解释器。JavaScript 引擎可以用多种语言编写。例如，支持 Chrome 浏览器的 V8 引擎是用 C++编写的，而支持 Firefox 浏览器的 SpiderMonkey 引擎是用 C 和 C++编写的。

这些 JavaScript 引擎可以在后台处理任务。根据 Brian 的说法，调用栈可以识别 Web API 的函数，并将其交给浏览器处理。浏览器完成这些任务后，它们将返回并作为回调被推上堆栈。

你可能想知道 Node.js 是怎么做这些工作的，毕竟它没有浏览器的帮助。实际上，支持 Chrome 的那个 V8 引擎也是 Node.js 背后的支撑。这里有 Salil 的一篇很棒的[博客文章](https://medium.com/better-programming/is-node-js-really-single-threaded-7ea59bcc8d64)，解释了 Node 生态系统中的这一过程。



### 12、使用代码拆分

如果你有使用 Google Light House 的经验，肯定会熟悉一种称为“first contentful paint”的指标。它是 Lighthouse 报告的 Performance 部分中跟踪的六个指标之一。

First Contentful Paint（FCP）衡量用户转到你的页面后浏览器渲染第一段 DOM 内容所花费的时间。页面上的图像、非白色``元素和 SVG 被视为 DOM 内容；iframe 内部不包含任何内容。

获得更高的 FCP 分数的最佳方法之一是使用代码拆分。代码拆分是一种在传输开始时仅将必要的模块发送给用户的技术。通过减小最初发送的载荷大小，这将极大地影响 FCP 分数。

流行的模块打包器（例如 webpack）可为你提供代码拆分功能。你还可以利用原生 ES 模块来单独加载各个模块。你可以在此处详细了解有关原生 ES 模块的[信息](https://blog.bitsrc.io/understanding-es-modules-in-javascript-a28fec420f73)。



### 13、使用 async 和 defer

在现代网站中，脚本比 HTML 更为密集，其大小更大且消耗更多的处理时间。默认情况下，浏览器必须等待脚本下载和执行完毕后，再处理页面的其余部分。

于是笨重的脚本可能会阻止网页的加载。为了避免这种情况，JavaScript 为我们提供了两种分别称为 async 和 defer 的技术。你只需将这些属性添加到``标记中即可。

Async 会让浏览器在不影响渲染的情况下加载脚本。换句话说，页面不会等待 async 脚本，而是先处理和显示内容。

Defer 是让浏览器在渲染完成后加载脚本。如果同时指定它们两者，则 async 在现代浏览器上更优先，而支持 defer 但不支持 async 的老式浏览器将回退为 defer。

这两个属性可以帮助你大幅减少页面加载时间。我强烈建议你阅读 Flavio 的这篇[博客文章](https://flaviocopes.com/javascript-async-defer/)。



### 14、使用 Web Workers 在后台运行 CPU 密集型任务

Web Worker 允许你在后台线程中运行脚本。如果你有一些高强度的任务，可以将它们分配给 Web Worker，这些 WebWorker 可以在不干扰用户界面的情况下运行它们。创建后，Web Worker 可以将消息发布到该代码指定的事件处理程序来与 JavaScript 代码通信，反之亦然。

要了解有关 Web Worker 的更多信息，建议你阅读[MDN文档](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers)。

原文链接：https://www.infoq.cn/article/MwyrfzDPdRpkzfbW7NwW







# 10 个超棒的 JavaScript 简写技巧

### 1.合并数组

**普通写法：**

我们通常使用`Array`中的`concat()`方法合并两个数组。用`concat()`方法来合并两个或多个数组，不会更改现有的数组，而是返回一个新的数组。请看一个简单的例子：

```css
let apples = ['🍎', '🍏'];
let fruits = ['🍉', '🍊', '🍇'].concat(apples);

console.log( fruits );
//=> ["🍉", "🍊", "🍇", "🍎", "🍏"]
```

**简写写法：**

我们可以通过使用ES6扩展运算符(`...`)来减少代码，如下所示：

```css
let apples = ['🍎', '🍏'];
let fruits = ['🍉', '🍊', '🍇', ...apples];  // <-- here

console.log( fruits );
//=> ["🍉", "🍊", "🍇", "🍎", "🍏"]
```



### 2.合并数组（在开头位置）

**普通写法：** 假设我们想将`apples`数组中的所有项添加到`Fruits`数组的开头，而不是像上一个示例中那样放在末尾。我们可以使用`Array.prototype.unshift()`来做到这一点：

```css
let apples = ['🍎', '🍏'];
let fruits = ['🥭', '🍌', '🍒'];

// Add all items from apples onto fruits at start
Array.prototype.unshift.apply(fruits, apples)

console.log( fruits );
//=> ["🍎", "🍏", "🥭", "🍌", "🍒"]
```

**简写写法：**

我们依然可以使用ES6扩展运算符(`...`)缩短这段长代码，如下所示：

```css
let apples = ['🍎', '🍏'];
let fruits = [...apples, '🥭', '🍌', '🍒'];  // <-- here

console.log( fruits );
//=> ["🍎", "🍏", "🥭", "🍌", "🍒"]
```



### 3.克隆数组

**普通写法：**

我们可以使用`Array`中的`slice()`方法轻松克隆数组，如下所示：

```ini
let fruits = ['🍉', '🍊', '🍇', '🍎'];
let cloneFruits = fruits.slice();

console.log( cloneFruits );
//=> ["🍉", "🍊", "🍇", "🍎"]
```

**简写写法：**

我们可以使用ES6扩展运算符(`...`)像这样克隆一个数组：

```ini
let fruits = ['🍉', '🍊', '🍇', '🍎'];
let cloneFruits = [...fruits];  // <-- here

console.log( cloneFruits );
//=> ["🍉", "🍊", "🍇", "🍎"]
```



### 5.模板字面量

**普通写法：**

通常，当我们必须向字符串添加表达式时，我们会这样做：

```javascript
// Display name in between two strings
let name = 'Palash';
console.log('Hello, ' + name + '!');
//=> Hello, Palash!

// Add & Subtract two numbers
let num1 = 20;
let num2 = 10;
console.log('Sum = ' + (num1 + num2) + ' and Subtract = ' + (num1 - num2));
//=> Sum = 30 and Subtract = 10
```

**简写写法：**

通过模板字面量，我们可以使用反引号`(``)，这样我们就可以将表达式包装在`$\\{…\\}`中，然后嵌入到字符串，如下所示：

```ini
// Display name in between two strings
let name = 'Palash';
console.log(`Hello, $\\{name\\}!`);  // <-- No need to use + var + anymore
//=> Hello, Palash!

// Add two numbers
let num1 = 20;
let num2 = 10;
console.log(`Sum = $\\{num1 + num2\\} and Subtract = $\\{num1 - num2\\}`);
//=> Sum = 30 and Subtract = 10
```



### 6.For循环

**普通写法：**

我们可以使用`for`循环像这样循环遍历一个数组：

```javascript
let fruits = ['🍉', '🍊', '🍇', '🍎'];

// Loop through each fruit
for (let index = 0; index < fruits.length; index++) \\{ 
  console.log( fruits[index] );  // <-- get the fruit at current index
\\}

//=> 🍉
//=> 🍊
//=> 🍇
//=> 🍎
```

**简写写法：**

我们可以使用`for...of`语句实现相同的结果，而代码要少得多，如下所示：

```javascript
let fruits = ['🍉', '🍊', '🍇', '🍎'];

// Using for...of statement 
for (let fruit of fruits) \\{
  console.log( fruit );
\\}

//=> 🍉
//=> 🍊
//=> 🍇
//=> 🍎
```



### 7.箭头函数

**普通写法：**

要遍历数组，我们还可以使用`Array`中的`forEach()`方法。但是需要写很多代码，虽然比最常见的`for`循环要少，但仍然比`for...of`语句多一点：

```javascript
let fruits = ['🍉', '🍊', '🍇', '🍎'];

// Using forEach method
fruits.forEach(function(fruit)\\{
  console.log( fruit );
\\});

//=> 🍉
//=> 🍊
//=> 🍇
//=> 🍎
```

**简写写法：**

但是使用箭头函数表达式，允许我们用一行编写完整的循环代码，如下所示：

```javascript
let fruits = ['🍉', '🍊', '🍇', '🍎'];
fruits.forEach(fruit => console.log( fruit ));  // <-- Magic ✨

//=> 🍉
//=> 🍊
//=> 🍇
//=> 🍎
```



### 8.在数组中查找对象

**普通写法：**

要通过其中一个属性从对象数组中查找对象的话，我们通常使用`for`循环：

```scss
slet inventory = [  \\{name: 'Bananas', quantity: 5\\},  \\{name: 'Apples', quantity: 10\\},  \\{name: 'Grapes', quantity: 2\\}];

// Get the object with the name `Apples` inside the array
function getApples(arr, value) \\{
  for (let index = 0; index < arr.length; index++) \\{

    // Check the value of this object property `name` is same as 'Apples'
    if (arr[index].name === 'Apples') \\{  //=> 🍎

      // A match was found, return this object
      return arr[index];
    \\}
  \\}
\\}

let result = getApples(inventory);
console.log( result )
//=> \\{ name: "Apples", quantity: 10 \\}
```

**简写写法：**

上面我们写了这么多代码来实现这个逻辑。但是使用`Array`中的`find()`方法和箭头函数`=>`，允许我们像这样一行搞定：

```javascript
// Get the object with the name `Apples` inside the array
function getApples(arr, value) \\{
  return arr.find(obj => obj.name === 'Apples');  // <-- here
\\}

let result = getApples(inventory);
console.log( result )
//=> \\{ name: "Apples", quantity: 10 \\}
```



### 9.将字符串转换为整数

**普通写法：**

`parseInt()`函数用于解析字符串并返回整数：

```javascript
let num = parseInt("10")

console.log( num )         //=> 10
console.log( typeof num )  //=> "number"
```

**简写写法：**

我们可以通过在字符串前添加`+`前缀来实现相同的结果，如下所示：

```javascript
let num = +"10";

console.log( num )           //=> 10
console.log( typeof num )    //=> "number"
console.log( +"10" === 10 )  //=> true
```



### 10.短路求值

**普通写法：**

如果我们必须根据另一个值来设置一个值不是falsy值，一般会使用`if-else`语句，就像这样：

```javascript
function getUserRole(role) \\{
  let userRole;

  // If role is not falsy value
  // set `userRole` as passed `role` value
  if (role) \\{
    userRole = role;
  \\} else \\{

    // else set the `userRole` as USER
    userRole = 'USER';
  \\}

  return userRole;
\\}

console.log( getUserRole() )         //=> "USER"
console.log( getUserRole('ADMIN') )  //=> "ADMIN"
```

**简写写法：**

但是使用短路求值(`||`)，我们可以用一行代码执行此操作，如下所示：

```javascript
function getUserRole(role) \\{
  return role || 'USER';  // <-- here
\\}

console.log( getUserRole() )         //=> "USER"
console.log( getUserRole('ADMIN') )  //=> "ADMIN"
```

#### 补充几点

**箭头函数：**

如果你不需要`this`上下文，则在使用箭头函数时代码还可以更短：

```ini
let fruits = ['🍉', '🍊', '🍇', '🍎'];
fruits.forEach(console.log);
```

**在数组中查找对象：**

你可以使用对象解构和箭头函数使代码更精简：

```javascript
// Get the object with the name `Apples` inside the array
const getApples = array => array.find((\\{ name \\}) => name === "Apples");

let result = getApples(inventory);
console.log(result);
//=> \\{ name: "Apples", quantity: 10 \\}
```

**短路求值替代方案：**

```ini
const getUserRole1 = (role = "USER") => role;
const getUserRole2 = role => role ?? "USER";
const getUserRole3 = role => role ? role : "USER";
```



### 编码习惯

最后我想说下编码习惯。代码规范比比皆是，但是很少有人严格遵守。究其原因，多是在代码规范制定之前，已经有自己的一套代码习惯，很难短时间改变自己的习惯。良好的编码习惯可以为后续的成长打好基础。下面，列举一下开发规范的几点好处，让大家明白代码规范的重要性：

- 规范的代码可以促进团队合作。
- 规范的代码可以减少 Bug 处理。
- 规范的代码可以降低维护成本。
- 规范的代码有助于代码审查。
- 养成代码规范的习惯，有助于程序员自身的成长。

原文链接：https://juejin.cn/post/7105967944613494792







# 实用JavaScript优雅小技巧🌟

### 减少if...else面条代码

- 一旦当我们写到超过两个`if...else`的函数的时候就该想想是否有更好的优化方法。
- 比如现在需要让我们根据名称计算出麦某劳的食品价格，你可能会这么做。

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e3653c009be944feb68b92bbdcae1b20~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

- 这样的写法会让函数体有很多的条件判断语句，而当我们想下次增加一个商品的时候就需要修改函数内的逻辑增加一个`if...else`语句，这一定程度上也违反了**开闭原则**,当我们需要增加一个逻辑的时候要尽量通过扩展软件实体来解决需求变化，而不是通过修改已有的代码来完成变化。
- 这是很经典的优化方式，我们可以使用一个类似`Map`结构的数据来保存所有商品，这里我们直接建立一个对象来存储。

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0e708ffb8ad248939e12ff62fedf1ccb~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

- 这样我们下次需要再增加一个商品时就不需要改动`getPrice`的逻辑了，当然了这里其实更多人喜欢直接在用的地方直接使用`foodMap`，我这里只是简单举了个例子表述这个思路。
- 那么这时候就有同学会问了，如果我不想`key`只用字符串呢，这时候你就可以用到`new Map`了，思路也是差不多的，额外扩展一个实体来存储变化。

### 管道操作取代冗余循环

- 有这么一个麦某劳食物列表

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a01ff53f65034e74a3ee30d30a6402ef~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

- 如果你想找出属于套餐1的食物，你会怎么找呢？
- 上面这种是我们以前经常使用的方法，显然我们替换成使用`filter`与`map`来取代`for`循环不仅可以使代码更精简，还可以使语义更加明确，这样我们一下就可以看出是先对数组`过滤`再`重组`。

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/950e2bf6ee75476b9f7da1f7e2a149a9~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

### find取代冗余循环

- 还是上面的例子，如果我们要在这个食品对象数组中按照属性值查找特定的食物时，`find`的用处就出来了。

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7ef9877f41554b5598c3684d0af476c1~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

### includes取代冗余循环

- 和上面两个细节类似的这些都是既有的函数也就是不用我们重新写的内置函数，巧用它会节省很多时间。
- 众所周知，一碗**康某傅老坛酸菜牛肉面**有**酸菜**，**面**，**牛肉粒**，**烟头**和**脚皮**组成，那我们想用函数证实这个面里面是否有脚皮我们怎么写会比较简洁呢？

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a6aed73a33be4e6a811446b479439099~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

- 同样的，不止是**康某傅的酸菜牛肉面**可以这样耍，所有类似的在数组里面找到特定元素的操作都可以使用`includes`函数来调用。

### result返回值

- 我们通常在写一些拥有返回值的函数的时候常常会以返回值变量命名而纠结，甚至对于一些长函数的时候还不使用变量而是直接`return`，这样的习惯其实是不好的，因为等我们下次再去参照这段代码的时候还需要重新捋清逻辑。
- 通常的，在一个小函数中，我们可以使用`result`作为返回值。

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/06bb38edd6b94e6ea2bbd0ce12f782a4~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

### 提前返回

- 然而上面用`result`作为返回值并不适用于所有情况，往往有些时候我们需要提前结束函数体来避免后面的同事阅读多余的程序。

- 如下的例子中当我们`selectedKey`不存在的时候应该立即`return`，这样就不用继续阅读下面的代码，否则面对更复杂的函数时会增加很多的阅读成本。

  ![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/91edb4b407e14bda81cbabc5cb328899~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

### 保持对象完整

- 经常在我们通过请求拿到后端返回的数据会根据其中一些属性进行处理，如果需要处理的属性少的时候很多同学会习惯使用第一种方法。
- 但其实这种习惯是不好的，因为当你无法确定这个函数以后还需不需要增加依赖属性的时候应该保持对象的完整，就像我上篇文章提到的，**学会拥抱变化**，假如`getDocDetail`不止要用到`icon`和`content`,可能以后还会有`title`，`date`等属性，所以我们不如直接将完整对象传入，不仅增加缩短参数列表还会让代码更易读。 ![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4947e6a9b7a6405a99ec02c4bdce1e20~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

### 巧用运算符

- 当我们需要创建新变量时, 有时需要检查为其值引用的变量是否为`null`或未定义时, 就可以使用简便写法。

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7251dfabea534d0f899881ee89c3d228~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

原文链接：https://juejin.cn/post/7079935342966472711







# 30个Javascript知识点

#### 一行代码完成结构加赋值

我们日常经常使用结构赋值，一般都是先结构，再赋值，当然我们也可以一行就完成解构加赋值操作，看起来非常简化，当然可读性你懂得！

```ini
let people = \\{ name: null, age: null \\};
let result = \\{ name: '张三',  age: 16 \\};

(\\{ name: people.name, age: people.age\\} = result);
console.log(people) // \\{"name":"张三","age":16\\}###
```

#### 对基础数据类型进行解构

日常中我们应该用不到这样的场景，但是实际上我们也可以对基础数据类型解构

```arduino
const \\{length : a\\} = '1234';
console.log(a) // 4
```

#### 对数组解构快速拿到最后一项值

实际上我们是可以对数组解构赋值拿到**length**属性的，通过这个特性也可以做更多的事情。

```ini
const arr = [1, 2, 3];
const \\{ 0: first, length, [length - 1]: last \\} = arr;
first; // 1
last; // 3
length; // 3
```

#### 将下标转为中文零一二三...

日常可能有的列表我们需要将对应的012345转为中文的一、二、三、四、五...，在老的项目看到还有通过自己手动定义很多行这样的写法，于是写了一个这样的方法转换

```typescript
export function transfromNumber(number)\\{
  const  INDEX_MAP = ['零'，'一'.....]
  if(!number) return
  if(number === 10) return INDEX_MAP[number]
  return [...number.toString()].reduce( (pre, cur) => pre  + INDEX_MAP[cur] , '' )
\\}
```

#### 判断整数的不同方法

```javascript
/* 1.任何整数都会被1整除，即余数是0。利用这个规则来判断是否是整数。但是对字符串不准确 */
function isInteger(obj) \\{
 return obj\\%1 === 0
\\}

/* 1. 添加一个是数字的判断 */
function isInteger(obj) \\{
 return typeof obj === 'number' && obj\\%1 === 0
\\}

/* 2. 使用Math.round、Math.ceil、Math.floor判断 整数取整后还是等于自己。利用这个特性来判断是否是整数*/
function isInteger(obj) \\{
 return Math.floor(obj) === obj
\\}

/* 3. 通过parseInt判断 某些场景不准确 */
function isInteger(obj) \\{
 return parseInt(obj, 10) === obj
\\}

/* 4. 通过位运算符*/
function isInteger(obj) \\{
 return (obj | 0) === obj
\\}

/* 5.ES6提供了Number.isInteger */
```

#### 通过css检测系统的主题色从而全局修改样式

**@media** 的属性 prefers-color-scheme就可以知道当前的系统主题，当然使用前需要查查兼容性

```scss
@media (prefers-color-scheme: dark) \\{ //... \\} 
@media (prefers-color-scheme: light) \\{ //... \\}
```

**javascript**也可以轻松做到

```csharp
window.addEventListener('theme-mode', event =>\\{ 
    if(event.mode == 'dark')\\{\\}
   if(event.mode == 'light')\\{\\} 
\\})

window.matchMedia('(prefers-color-scheme: dark)') .addEventListener('change', event => \\{ 
    if (event.matches) \\{\\} // dark mode
\\})
```

#### 数组随机打乱顺序

通过 0.5-Math.random() 得到一个随机数，再通过两次sort排序打乱的更彻底,但是这个方法实际上并不够随机，如果是企业级运用，建议使用第二种洗牌算法

```javascript
shuffle(arr) \\{
      return arr.sort(() => 0.5 - Math.random()). sort(() => 0.5 - Math.random());
 \\},
function shuffle(arr) \\{
  for (let i = arr.length - 1; i > 0; i--) \\{
    const randomIndex = Math.floor(Math.random() * (i + 1))
    ;[arr[i], arr[randomIndex]] = [arr[randomIndex], arr[i]]
  \\}
  return arr
\\}
```

#### 随机获取一个Boolean值

和上个原理相同，通过随机数获取，**Math.random()**的区间是0-0.99，用0.5在中间百分之五十的概率

```javascript
function randomBool() \\{
    return 0.5 - Math.random()
\\}
```

#### 把数组的第一项放到最后一项

```javascript
function (arr)\\{
    return arr.push(arr.shift());
\\}
```

#### 把数组最后一项移到第一项

```javascript
function(arr)\\{
  return arr.unshift(arr.pop());
\\}
```

#### 利用set数组去重

```javascript
function uniqueArr(arr)\\{
    return [...new Set(arr)]
\\}
```

#### 获取随机颜色

日常我们经常会需要获取一个随机颜色，通过随机数即可完成

```javascript
function getRandomColor()\\{
    return `#$\\{Math.floor(Math.random() * 0xffffff) .toString(16)\\}`;
\\}
```

#### 检测是否为空对象

通过使用Es6的Reflect静态方法判断他的长度就可以判断是否是空数组了，也可以通过**Object.keys()**来判断

```javascript
function isEmpty(obj)\\{
    return  Reflect.ownKeys(obj).length === 0 && obj.constructor === Object;
\\}
```

#### Boolean转换

一些场景下我们会将boolean值定义为场景，但是在js中非空的字符串都会被认为是true

```scss
function toBoolean(value, truthyValues = ['true'])\\{
  const normalizedValue = String(value).toLowerCase().trim();
  return truthyValues.includes(normalizedValue);
\\}
toBoolean('TRUE'); // true
toBoolean('FALSE'); // false
toBoolean('YES', ['yes']); // true
```

#### 各种数组克隆方法

数组克隆的方法其实特别多了，看看有没有你没见过的！

```ini
const clone = (arr) => arr.slice(0);
const clone = (arr) => [...arr];
const clone = (arr) => Array.from(arr);
const clone = (arr) => arr.map((x) => x);
const clone = (arr) => JSON.parse(JSON.stringify(arr));
const clone = (arr) => arr.concat([]);
const clone = (arr) => structuredClone(arr);
```

#### 比较两个时间大小

通过调用getTime获取时间戳比较就可以了

```vbscript
function compare(a, b)\\{
    return a.getTime() > b.getTime();
\\}
```

#### 计算两个时间之间的月份差异

```vbscript
function monthDiff(startDate, endDate)\\{
    return  Math.max(0, (endDate.getFullYear() - startDate.getFullYear()) * 12 - startDate.getMonth() + endDate.getMonth());
\\}
```

#### 一步从时间中提取年月日时分秒

时间格式化轻松解决，一步获取到年月日时分秒毫秒，由于toISOString会丢失时区，导致时间差八小时，所以在格式化之前我们加上八个小时时间即可

```sql
function extract(date)\\{
	const d = new Date(new Date(date).getTime() + 8*3600*1000);
	return new Date(d).toISOString().split(/[^0-9]/).slice(0, -1);
\\}
console.log(extract(new Date())) // ['2022', '09', '19', '18', '06', '11', '187']
```

#### 判断一个参数是不是函数

有时候我们的方法需要传入一个函数回调，但是需要检测其类型，我们可以通过Object

的原型方法去检测，当然这个方法可以准确检测任何类型。

```javascript
function isFunction(v)\\{
   return ['[object Function]', '[object GeneratorFunction]', '[object AsyncFunction]', '[object Promise]'].includes(Object.prototype.toString.call(v));
\\}
```

#### 计算两个坐标之间的距离

```lua
function distance(p1, p2)\\{
    return `Math.sqrt(Math.pow(p2.x - p1.x, 2) + Math.pow(p2.y - p1.y, 2));
\\}
```

#### 检测两个dom节点是否覆盖重叠

有些场景下我们需要判断dom是否发生碰撞了或者重叠了，我们可以通过**getBoundingClientRect**获取到dom的x1,y1,x2,y2坐标然后进行坐标比对即可判断出来

```css
function overlaps = (a, b) \\{
   return (a.x1 < b.x2 && b.x1 < a.x2) || (a.y1 < b.y2 && b.y1 < a.y2);
\\}
```

#### 判断是否是NodeJs环境

前端的日常开发是离不开nodeJs的，通过判断全局环境来检测是否是nodeJs环境

```csharp
function isNode()\\{
    return typeof process !== 'undefined' && process.versions != null && process.versions.node != null;
\\}
```

#### 参数求和

之前看到有通过函数柯理化形式来求和的，通过reduce一行即可

```javascript
function sum(...args)\\{
    return args.reduce((a, b) => a + b);
\\}
```

原文链接：https://juejin.cn/post/7145036326373425159







# JavaScript中几个优雅的运算符使用技巧

ECMAScript发展进程中，会有很多功能的更新，比如销毁，箭头功能，模块，它们极大的改变JavaScript编写方式，可能有些人喜欢，有些人不喜欢，但像每个新功能一样，我们最终会习惯它们。新版本的ECMAScript引入了三个新的逻辑赋值运算符：空运算符，AND和OR运算符，这些运算符的出现，也是希望让我们的代码更干净简洁，下面分享几个优雅的JavaScript运算符使用技巧。

### 一、可选链接运算符【？.】

**可选链接运算符（Optional Chaining Operator）** 处于ES2020提案的第4阶段，因此应将其添加到规范中。它改变了访问对象内部属性的方式，尤其是深层嵌套的属性。它也可以作为TypeScript 3.7+中的功能使用。

相信大部分开发前端的的小伙伴们都会遇到null和未定义的属性。JS语言的动态特性使其无法不碰到它们。特别是在处理嵌套对象时，以下代码很常见：

```js
if (data && data.children && data.children[0] && data.children[0].title) \\{
    // I have a title!
\\}
```

上面的代码用于API响应，我必须解析JSON以确保名称存在。但是，当对象具有可选属性或某些配置对象具有某些值的动态映射时，可能会遇到类似情况，需要检查很多边界条件。

这时候，如果我们使用可选链接运算符，一切就变得更加轻松了。它为我们检查嵌套属性，而不必显式搜索梯形图。我们所要做的就是使用“？” 要检查空值的属性之后的运算符。我们可以随意在表达式中多次使用该运算符，并且如果未定义任何项，它将尽早返回。

**对于静态属性**用法是：

```js
object?.property
```

**对于动态属性**将其更改为：

```js
object?.[expression] 
```

上面的代码可以简化为：

```js
let title = data?.children?.[0]?.title;
```

然后，如果我们有:

```js

let data;
console.log(data?.children?.[0]?.title) // undefined

data  = \\{children: [\\{title:'codercao'\\}]\\}
console.log(data?.children?.[0]?.title) // codercao
```

这样写是不是更加简单了呢？ 由于操作符一旦为空值就会终止，因此也可以使用它来有条件地调用方法或应用条件逻辑

```js

const conditionalProperty = null;
let index = 0;

console.log(conditionalProperty?.[index++]); // undefined
console.log(index);  // 0
```

**对于方法**的调用你可以这样写

```js
object.runsOnlyIfMethodExists?.()
```

例如下面的`parent`对象，如果我们直接调用`parent.getTitle()`,则会报`Uncaught TypeError: parent.getTitle is not a function`错误，`parent.getTitle?.()`则会终止不会执行

```js
let parent = \\{
    name: "parent",
    friends: ["p1", "p2", "p3"],
    getName: function() \\{
      console.log(this.name)
    \\}
  \\};
  
  parent.getName?.()   // parent
  parent.getTitle?.()  //不会执行
  
```

**与无效合并一起使用**

提供了一种方法来处理未定义或为空值和表达提供默认值。我们可以使用`??`运算符，为表达式提供默认值

```js
console.log(undefined ?? 'codercao'); // codercao
```

因此，如果属性不存在，则可以将无效的合并运算符与可选链接运算符结合使用以提供默认值。

```js
let title = data?.children?.[0]?.title ?? 'codercao';
console.log(title); // codercao
```



### 二、逻辑空分配（?? =）

```js
expr1 ??= expr2
```

逻辑空值运算符仅在nullish值（`null` 或者 `undefined`）时才将值分配给expr1，表达方式：

```js
x ??= y
```

可能看起来等效于：

```js
x = x ?? y;
```

但事实并非如此！有细微的差别。

空的合并运算符（??）从左到右操作，如果x不为**nullish值**则中表达式不执行。因此，如果x不为`null` 或者 `undefined`，则永远不会对表达式`y`进行求值。如果`y`是一个函数，它将根本不会被调用。因此，此逻辑赋值运算符等效于

```js
x ?? (x = y);
```



### 三、逻辑或分配（|| =）

此逻辑赋值运算符仅在左侧表达式为 **falsy值（虚值）** 时才赋值。Falsy值（虚值）与null有所不同，因为falsy值（虚值）可以是任何一种值：undefined，null，空字符串(双引号""、单引号’’、反引号``)，NaN，0。IE浏览器中的 document.all，也算是一个。

语法

```js
x ||= y
```

等同于

```js
x || (x = y)
```

在我们想要保留现有值（如果不存在）的情况下，这很有用，否则我们想为其分配默认值。例如，如果搜索请求中没有数据，我们希望将元素的内部HTML设置为默认值。否则，我们要显示现有列表。这样，我们避免了不必要的更新和任何副作用，例如解析，重新渲染，失去焦点等。我们可以简单地使用此运算符来使用JavaScript更新HTML：

```js
document.getElementById('search').innerHTML ||= '<i>No posts found matching this search.</i>'
```



### 四、逻辑与分配（&& =）

可能你已经猜到了，此逻辑赋值运算符仅在左侧为真时才赋值。因此：

```js
x &&= y
```

等同于

```js
x && (x = y)
```



### 最后

本次分享几个优雅的JavaScript运算符使用技巧，重点分享了可选链接运算符的使用，这样可以让我们不需要再编写大量我们例子中代码即可轻松访问嵌套属性。但是IE不支持它，因此，如果需要支持该版本或更旧版本的浏览器，则可能需要添加Babel插件。对于Node.js，需要为此升级到Node 14 LTS版本，因为12.x不支持该版本。

如果你也有优雅的优雅的JavaScript运算符使用技巧，请不要吝惜，在评论区一起交流~

原文链接：https://juejin.cn/post/6954902440915238920







# 其他

### 使用`Set`来检查元素是否存在通常比在数组中使用`includes`方法更高效

```
	  // 生成一个映射来快速查找editableGroupIds
      const editableGroupMap = new Set(editableGroupIds.value) 
      if (editableGroupMap.has(group.groupId)) \\{
        // 如果这个组是可编辑的，跳过
        return
      \\}
      if (editableGroupIds.value.includes(group.groupId)) \\{
        // 如果这个组是可编辑的，跳过
        return
      \\}
```

在JavaScript中，使用`Set`来检查元素是否存在通常比在数组中使用`includes`方法更高效，特别是在集合非常大的情况下。这是因为`Set`的平均查找时间复杂度是O(1)，而数组的`includes`方法的时间复杂度是O(n)，其中n是数组的长度。

所以，在你的代码中，使用`Set`来存储`editableGroupIds`并将查找操作替换为`has`方法会更加优化。

使用`Set`和`has`方法可以显著减少查找时间，尤其是在处理大量数据时。这使得代码更加高效，尤其是在频繁进行查找操作的情况下。因此，推荐使用`Set`和`has`方法来进行优化。



### customerInfo.tagInfoList && customerInfo.tagInfoList.length>0怎么优化

#### 使用可选链（?.）操作符

ES2020 引入了可选链操作符 `?.`，它允许我们安全地访问深层嵌套的对象属性，即使某个中间属性不存在也不会抛出错误。这可以用来简化原始的条件判断：

```
customerInfo.tagInfoList?.length > 0
```

这条语句首先会检查 `customerInfo.tagInfoList` 是否存在。如果存在，则继续检查其 `.length` 属性是否大于0；如果 `tagInfoList` 不存在或为 `null`，则整个表达式的结果为 `false`。

如果你确定 `customerInfo.tagInfoList` 要么是一个数组，要么是 `undefined` 或 `null`，那么直接使用 `customerInfo.tagInfoList?.length > 0` 是完全可以的，并且非常简洁。这种方式利用了可选链操作符 `?.`，可以有效地防止在 `tagInfoList` 不存在时抛出错误。

以下是一些情况说明：

1. **当 `tagInfoList` 是一个数组**：
   - 如果数组为空，`customerInfo.tagInfoList?.length` 将返回 `0`，所以 `customerInfo.tagInfoList?.length > 0` 为 `false`。
   - 如果数组不为空，`customerInfo.tagInfoList?.length` 将返回一个正整数，所以 `customerInfo.tagInfoList?.length > 0` 为 `true`。

2. **当 `tagInfoList` 不存在或为 `null` 或 `undefined`**：
   - `customerInfo.tagInfoList?.length` 将返回 `undefined`，而 `undefined > 0` 为 `false`。

因此，`customerInfo.tagInfoList?.length > 0` 这个表达式可以很好地处理这些情况，并且代码非常简洁。

#### 示例代码

```javascript
const customerInfo = \\{
    tagInfoList: [/* 可能为空或包含元素的数组 */]
\\};

if (customerInfo.tagInfoList?.length > 0) \\{
    console.log("tagInfoList 不为空");
\\} else \\{
    console.log("tagInfoList 为空或不存在");
\\}
```

#### 注意事项

- 如果 `tagInfoList` 可能是其他类型的值（例如字符串、数字等），建议先确保它是数组，以避免意外行为。在这种情况下，可以使用 `Array.isArray` 方法：

```javascript
if (Array.isArray(customerInfo.tagInfoList) && customerInfo.tagInfoList?.length > 0) \\{
    console.log("tagInfoList 是一个非空数组");
\\} else \\{
    console.log("tagInfoList 为空或不存在或不是数组");
\\}
```

综上所述，如果你确定 `tagInfoList` 要么是数组，要么是 `undefined` 或 `null`，那么 `customerInfo.tagInfoList?.length > 0` 是一个很好的选择。

- **Vue 2**：**需要手动配置 Babel** 来支持 ES2020+ 语法。
- **Vue 3**：默认支持 ES2020+ 语法，通常不需要额外配置。



### customerInfo.tagInfoList && customerInfo.tagInfoList.length>0在vue2中怎么优化，最简单，不使用Babel

在 Vue 2 中，如果不使用 Babel 来支持现代 JavaScript 语法，你可以通过一些简单的优化来使代码更加简洁和易读。以下是几种方法：

#### 1. 使用简化的条件判断
你可以将条件判断简化为一个表达式，使其更易读。

```html
<div v-if="customerInfo.tagInfoList && customerInfo.tagInfoList.length">
  <!-- 内容 -->
</div>
```

这里，`customerInfo.tagInfoList.length` 会自动转换为布尔值，如果 `length` 为 0，则表达式为 `false`，否则为 `true`。

#### 2. 使用计算属性
计算属性可以提高代码的可读性和复用性。你可以在 Vue 组件中定义一个计算属性来处理这个条件判断。

##### 定义计算属性
```javascript
export default \\{
  data() \\{
    return \\{
      customerInfo: \\{
        tagInfoList: [] // 初始化为空数组
      \\}
    \\};
  \\},
  computed: \\{
    hasTags() \\{
      return this.customerInfo.tagInfoList && this.customerInfo.tagInfoList.length > 0;
    \\}
  \\}
\\};
```

##### 在模板中使用计算属性
```html
<div v-if="hasTags">
  <!-- 内容 -->
</div>
```

#### 3. 使用方法
你也可以定义一个方法来处理这个条件判断，虽然这种方法不如计算属性常用，但在某些情况下也是可行的。

##### 定义方法
```javascript
export default \\{
  data() \\{
    return \\{
      customerInfo: \\{
        tagInfoList: [] // 初始化为空数组
      \\}
    \\};
  \\},
  methods: \\{
    hasTags() \\{
      return this.customerInfo.tagInfoList && this.customerInfo.tagInfoList.length > 0;
    \\}
  \\}
\\};
```

##### 在模板中使用方法
```html
<div v-if="hasTags()">
  <!-- 内容 -->
</div>
```

#### 总结
- **简化条件判断**：直接使用 `customerInfo.tagInfoList && customerInfo.tagInfoList.length`。
- **使用计算属性**：定义一个计算属性 `hasTags`，并在模板中使用。
- **使用方法**：定义一个方法 `hasTags`，并在模板中调用。

推荐使用计算属性，因为它不仅提高了代码的可读性，还使得逻辑更加清晰和易于复用。