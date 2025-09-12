---
title: JavaScript数据处理
date: 2020-02-14 18:24:00
categories: 
- 前端知识
tags:
- JavaScript
- 字符串
- 数组
- 对象
---

### js取整方法（四舍五入）总结

```
1. 四舍五入:
Math.round(1.23);  // 1
2. 只取整数:
Math.parseInt(1.23); // 1
3. 向上取整数:
Math.floor(1.23); // 1
4. 向下取整:
Math.ceil(1.23); // 2
5. 取绝对值:
Math.abs(-1.23); //1.23
6. 取两者较大值:
Math.max(1, 2); //2
7. 取两者较小值:
Math.min(1, 2);// 1
8. 随机数: 返回一个浮点,  伪随机数在范围[0, 1)
Math.random()
Math.random() 不能提供像密码一样安全的随机数字, 不能使用它们来处理有关安全的事情。使用Web Crypto API 来代替, 和更精确的window.crypto.getRandomValues() 方法.
```

#### 1.round()方法：

round（）方法把一个数字舍入为最接近的整数

例子：

	console.log(Math.round(1.52))//输出2
	console.log(Math.round(1.12))//输出1
	console.log(Math.round(1.94))//输出2
	console.log(Math.round(1.50))//输出2
	console.log(Math.round(1.49))//输出1

#### 2.floor()方法

floor()方法向下取整，速记：floor有地板、地面的意思

例子：

	console.log(Math.floor(1.94))//输出1
	console.log(Math.floor(1.12))//输出1
	console.log(Math.floor(1.50))//输出1
	console.log(Math.floor(1.01))//输出1

#### 3.ceil()方法

ceil（）方法向上取整，速记：ceil有装天花板的意思

	console.log(Math.ceil(1.12))//输出2
	console.log(Math.ceil(1.49))//输出2
	console.log(Math.ceil(1.50))//输出2
	console.log(Math.ceil(1.98))//输出2
	console.log(Math.ceil(1.02))//输出2

#### 4.toFixed()方法

roFixed()方法把数值Number类型四舍五入为指定小数位数（0到20位）的数字

例子：

	var num = 1.4927
	console.log(num.toFixed(0))//输出1
	console.log(num.toFixed(1))//输出1.5
	console.log(num.toFixed(2))//输出1.49
	console.log(num.toFixed(3))//输出1.493
	console.log(num.toFixed(4))//输出1.497
	var num1 = 1.5226
	console.log(num1.toFixed(0))//输出2



### toPrecision 和 toFixed 和 Math.round 的区别？

toPrecision 用于处理精度，精度是从左至右第一个不为 0 的数开始数起。
toFixed 是对小数点后指定位数取整，从小数点开始数起。
Math.round 是将一个数字四舍五入到一个整数。



### 字符串转换成对象

```
var obj = JSON.parse(data);
console.log(JSON.stringify(data.data));
```

说明：
①php中json_encode()转换返回给前端页面时，用“.”读取不到，是因为返回的是字符串格式，就是最外层带了引号的json数据格式，可以用`var obj = JSON.parse(data);`转换成对象，也可以用tp框架中的`$this->ajaxReturn()`;
②另外在vue中，有时候打印对象或者数组时，可能会出现看不懂其数据结构，可以用`console.log(JSON.stringify(data.data));`打印出来，再复制出来，格式化结构。



### 判断一个单词是否是回文

回文是指把相同的词汇或句子，在下文中调换位置或颠倒过来，产生首尾回环的情趣，叫做回文。例如 12345654321 abcdedbcba 等。

```
//利用reverse 进行字符串反转，然后和原字符串对比是否相等
function isPalindrom(str) \\{  
    return str == str.split('').reverse().join('');
\\}
```



### 统计一个字符串出现最多的字母

```
//统计每个字母出现的次数，然后存起来，然后进行比较function maxTimesChar(str) \\{  
  if(str.length == 1) \\{
    return str;
  \\}
  let charObj = \\{\\};
  for(let i=0;i<str.length;i++) \\{
    if(!charObj[str.charAt(i)]) \\{
      charObj[str.charAt(i)] = 1;
    \\}else\\{
      charObj[str.charAt(i)] += 1;
    \\}
  \\}
  let maxChar = '',
      maxValue = 1;
  for(var k in charObj) \\{
    if(charObj[k] >= maxValue) \\{
      maxChar = k;
      maxValue = charObj[k];
    \\}
  \\}
  return maxChar;
\\}
```



### 转义与反转义兼容写法

```
//反转义
function HTMLDecode(text) \\{
    var temp = document.createElement("div");
    temp.innerHTML = text;
    var output = temp.innerText || temp.textContent;
    temp = null;
    return output;
\\}
//转义
function HTMLEncode(html) \\{    
    var temp = document.createElement ("div");  
    (temp.textContent != null) ? (temp.textContent = html) : (temp.innerText = html);  
    var output = temp.innerHTML;  
    temp = null;  
    return output;
\\}
```

说明：前端相关朋友说这么写是兼容性写法，我这里就不深究了，亲测可用。



### js 判断一个 object 对象是否为空

```
if (JSON.stringify(data) === '\\{\\}') \\{
    return false // 如果为空,返回false，数组可以用同样的判断方式
\\}
if (Object.keys(object).length === 0) \\{
    return false // 如果为空,返回false，Object.keys(object)会返回一个空数组[]
\\}
```



### 数组中添加元素

代码：arr.push();
说明：
可以用arr.push()，在添加元素之前先确认变量arr是一个数组。可以自己定义var arr = []，并可以在数组中添加对象，例如arr.push(\\{"aa":"bb"\\})。



### 读取对象或这数组中的元素

```
var test = [\\{"a":"a"\\},\\{"b","b"\\}];
console.log(test[1].b);
console.log(test[1].['b']);  //不能用test.1.b
```


当键名是数字时，不能用“.”点拼接，只能用[]



### 当两个数组要根据各自某一个字段进行排序

举个例子，表格的表头和表中的值，分为了两个数组(如下)，表头和表中值要一一对应。另外，在Element的表格组件中，不用排序，其组件已做了排序的工作。

表头1	表头2	表头3
1	2	3
…	…	…
数组示例：数组1和数组2要根据key字段一一对应，可以根据这个字段先对两个数组进行排序，然后一一匹配，如冒泡排序等。

```
[
    \\{
        "tabelHeader":"表头1",
        "key":"1"
    \\},
    \\{
        "tabelHeader":"表头2",
        "key":"2"
    \\},
    \\{
        "tabelHeader":"表头3",
        "key":"3"
    \\}
]
[
    \\{
        "value":"2",
        "key":"2"
    \\},
    \\{
        "value":"1",
        "key":"1"
    \\},
    \\{
        "value":"3",
        "key":"3"
    \\}
]

//根据数组中某个键的值冒泡排序，还有其他更优排序方式，这里不一一示例，可以搜索相关算法排序方式。
function bubbleSort(arr,sortKey) \\{
    //console.time('2.快速排序耗时');
    var len = arr.length;
    for (var i = 0; i < len; i++) \\{
        for (var j = 0; j < len - 1 - i; j++) \\{
            if (arr[j][sortKey] > arr[j+1][sortKey] ) \\{ //相邻元素两两对比
                var temp = arr[j+1]; //元素交换
                arr[j+1] = arr[j];
                arr[j] = temp;
            \\}
        \\}
    \\}
    //console.timeEnd('222222.快速排序耗时');
    return arr;
\\}
```



### 转义与反转义兼容写法

6、转义与反转义兼容写法
代码：

```
//反转义
function HTMLDecode(text) \\{
    var temp = document.createElement("div");
    temp.innerHTML = text;
    var output = temp.innerText || temp.textContent;
    temp = null;
    return output;
\\}
//转义
function HTMLEncode(html) \\{    
    var temp = document.createElement ("div");  
    (temp.textContent != null) ? (temp.textContent = html) : (temp.innerText = html);  
    var output = temp.innerHTML;  
    temp = null;  
    return output;
\\}
```


说明：前端相关朋友说这么写是兼容性写法，我这里就不深究了，亲测可用。



### 剔除数组中的某些元素

目前只找到循环剔除，把需要的元素用push添加到新的数组中。使用splice在循环中有问题，个人猜测是键名原因，未做深究，但我个人觉得肯定有更好方式，因为参照其他语言，都有更为简单的方式，知道的朋友请告知下，谢谢。
–更新–今天看到前端人员剔除数组中一些元素时，用到了filter函数，挺好用的。



### 将数组中字符串转换成整型

```
var arr = ["1","2","3"];
arr = arr.map(function (data) \\{
    return +data;
\\});//此时arr变成[1,2,3]
map是个好方法，我个人对map理解不深，对其使用有些别扭。
```



### 判断对象或数组中元素是否存在

typeof data.archiveRecordPage !== undefined
一搬如果typeof后边是表达式，就要用括号括起来，否则不用括起来。另外一般要判断该层级之前的层级也要存在
----更新： hasOwnProperty也可以对象某对象是否存在



### 将时间戳转换为时间格式

在网上找的一个示例，如果是php写的接口，一般是需要在返回的时间戳字段上乘以1000的，java写的接口一般不需要，这个与精确度有关。一个是精确到秒，一个是精确到毫秒。当然，在框架VUE中另有其他写法，这里暂时不做深究。

```
formatDate(timestamp) \\{
    var date = new Date(timestamp);//时间戳为10位需*1000，时间戳为13位的话不需乘1000
    var Y = date.getFullYear() + '-';
    var M = (date.getMonth()+1 < 10 ? '0'+(date.getMonth()+1) : date.getMonth()+1) + '-';
    var D = (date.getDate() < 10 ? '0'+(date.getDate()) : date.getDate()) + ' ';
    var h = (date.getHours() < 10 ? '0'+(date.getHours()) : date.getHours()) + ':';
    var m = (date.getMinutes() < 10 ? '0'+(date.getMinutes()) : date.getMinutes()) + ':';
    var s = (date.getSeconds() < 10 ? '0'+(date.getSeconds()) : date.getSeconds());
    return Y+M+D+h+m+s;
\\}
```



### js判断数组中对象里的某一个值是否存在

11、js判断数组中对象里的某一个值是否存在

```
function isInArray(arr,value)\\{
    for(var i = 0; i < arr.length; i++)\\{
        if(value === arr[i]['id'])\\{
            return true;
        \\}
    \\}
    return false;
\\}
var arr = [\\{id: "ccjl1"\\},\\{id: "ccjl2"\\},\\{id: "ccjl3"\\}];
var test = isInArray(arr,'ccjl1');
console.log(test);
```



### 根据属性来更新一个数组中的对象

```
const arr = [ \\{id: 1, score: 1\\}, \\{id: 2, score: 2\\}, \\{id: 3, score: 4\\}];//更新的值const newValue = \\{id: 3, score: 3\\}
```

　　更新数组中id为3的score值。

　　Es6 装逼写法如下：

```
const result = initial.map(x => x.id === newValue.id ? newValue : x); //是不是很装B？？
console.log(updated) // => [ \\{ id: 1, score: 1 \\}, \\{ id: 2, score: 2 \\}, \\{ id: 3, score: 3 \\} ]
```

　　首先数组是利用数组map方法去遍历arr的每一个值，然后进行于newValue的id进行对比，不同返回原来的项，相同返回newValue.

　　不装逼清晰点写法：

```
const updated = arr.map(function(item)\\{
    return item.id == newValue.id ? newValue : item ;
\\});
console.log(updated) // => [ \\{ id: 1, score: 1 \\}, \\{ id: 2, score: 2 \\}, \\{ id: 3, score: 3 \\} ]
```



### 根据属性删除数组中的一个对象

```
 // 根据属性删除数组中的对象,利用filter进行过滤数组中id相同的项
 const initial = [ \\{id: 1, score: 1\\}, \\{id: 2, score: 2\\}, \\{id: 3, score: 4\\}];
 const removeId = 3;
 const without3 = initial.filter(x => x.id !== removeId);
 console.log(without3) // => [ \\{ id: 1, score: 1 \\}, \\{ id: 2, score: 2 \\} ]
```



### 删除一个对象上的属性（key）

```
//利用es6的 ...运算符将其他属性和ａ属性分开来，这波操作很亮眼 ！const obj = \\{a: 1, b: 2, c: 3\\};
const \\{a, ...newObj\\} = obj;
console.log(newObj) // => \\{b: 2, c: 3\\};
```



### 两个Set对象相减

```
//利用filter对s1进行过滤 ，去掉s2中存在的数字const s1 = [ 1, 2, 3, 4, 5 ];
 const s2 = [ 2, 4 ];
 const subtracted = s1.filter(x => s2.indexOf(x) < 0);
 console.log(subtracted);//[1,3,5]
```

 同理这样是可以去出一个数组中指定的元素

```
//去掉s3中的2和4
 const s3 = [ 1, 2, 3, 4, 5, 4, 5, 6, 2, 2, 4 ];
 const s2 = [ 2, 4 ];
 const subtracted1 = s3.filter(x => s2.indexOf(x) < 0);
 console.log(subtracted1); // [1, 3, 5, 5, 6]
```



### 判断一个单词是否是回文

回文是指把相同的词汇或句子，在下文中调换位置或颠倒过来，产生首尾回环的情趣，叫做回文。例如 12345654321 abcdedbcba 等。

```
//利用reverse 进行字符串反转，然后和原字符串对比是否相等
function isPalindrom(str) \\{  
    return str == str.split('').reverse().join('');
\\}
```



### 统计一个字符串出现最多的字母

```
//统计每个字母出现的次数，然后存起来，然后进行比较function maxTimesChar(str) \\{  
  if(str.length == 1) \\{
    return str;
  \\}
  let charObj = \\{\\};
  for(let i=0;i<str.length;i++) \\{
    if(!charObj[str.charAt(i)]) \\{
      charObj[str.charAt(i)] = 1;
    \\}else\\{
      charObj[str.charAt(i)] += 1;
    \\}
  \\}
  let maxChar = '',
      maxValue = 1;
  for(var k in charObj) \\{
    if(charObj[k] >= maxValue) \\{
      maxChar = k;
      maxValue = charObj[k];
    \\}
  \\}
  return maxChar;
\\}
```



### 数组中添加元素

代码：arr.push();
说明：
可以用arr.push()，在添加元素之前先确认变量arr是一个数组。可以自己定义var arr = []，并可以在数组中添加对象，例如arr.push(\\{"aa":"bb"\\})。



### 读取对象或这数组中的元素

```
var test = [\\{"a":"a"\\},\\{"b","b"\\}];
console.log(test[1].b);
console.log(test[1].['b']);  //不能用test.1.b
```


当键名是数字时，不能用“.”点拼接，只能用[]



### 当两个数组要根据各自某一个字段进行排序

举个例子，表格的表头和表中的值，分为了两个数组(如下)，表头和表中值要一一对应。另外，在Element的表格组件中，不用排序，其组件已做了排序的工作。

表头1	表头2	表头3
1	2	3
…	…	…
数组示例：数组1和数组2要根据key字段一一对应，可以根据这个字段先对两个数组进行排序，然后一一匹配，如冒泡排序等。

```
[
    \\{
        "tabelHeader":"表头1",
        "key":"1"
    \\},
    \\{
        "tabelHeader":"表头2",
        "key":"2"
    \\},
    \\{
        "tabelHeader":"表头3",
        "key":"3"
    \\}
]
[
    \\{
        "value":"2",
        "key":"2"
    \\},
    \\{
        "value":"1",
        "key":"1"
    \\},
    \\{
        "value":"3",
        "key":"3"
    \\}
]

//根据数组中某个键的值冒泡排序，还有其他更优排序方式，这里不一一示例，可以搜索相关算法排序方式。
function bubbleSort(arr,sortKey) \\{
    //console.time('2.快速排序耗时');
    var len = arr.length;
    for (var i = 0; i < len; i++) \\{
        for (var j = 0; j < len - 1 - i; j++) \\{
            if (arr[j][sortKey] > arr[j+1][sortKey] ) \\{ //相邻元素两两对比
                var temp = arr[j+1]; //元素交换
                arr[j+1] = arr[j];
                arr[j] = temp;
            \\}
        \\}
    \\}
    //console.timeEnd('222222.快速排序耗时');
    return arr;
\\}
```



### 剔除数组中的某些元素

目前只找到循环剔除，把需要的元素用push添加到新的数组中。使用splice在循环中有问题，个人猜测是键名原因，未做深究，但我个人觉得肯定有更好方式，因为参照其他语言，都有更为简单的方式，知道的朋友请告知下，谢谢。
–更新–今天看到前端人员剔除数组中一些元素时，用到了filter函数，挺好用的。



### 将数组中字符串转换成整型

```
var arr = ["1","2","3"];
arr = arr.map(function (data) \\{
    return +data;
\\});//此时arr变成[1,2,3]
map是个好方法，我个人对map理解不深，对其使用有些别扭。
```



### js判断数组中对象里的某一个值是否存在

```
function isInArray(arr,value)\\{
    for(var i = 0; i < arr.length; i++)\\{
        if(value === arr[i]['id'])\\{
            return true;
        \\}
    \\}
    return false;
\\}
var arr = [\\{id: "ccjl1"\\},\\{id: "ccjl2"\\},\\{id: "ccjl3"\\}];
var test = isInArray(arr,'ccjl1');
console.log(test);
```



### 根据属性来更新一个数组中的对象

```
const arr = [ \\{id: 1, score: 1\\}, \\{id: 2, score: 2\\}, \\{id: 3, score: 4\\}];//更新的值const newValue = \\{id: 3, score: 3\\}
```

　　更新数组中id为3的score值。

　　Es6 装逼写法如下：

```
const result = initial.map(x => x.id === newValue.id ? newValue : x); //是不是很装B？？
console.log(updated) // => [ \\{ id: 1, score: 1 \\}, \\{ id: 2, score: 2 \\}, \\{ id: 3, score: 3 \\} ]
```

　　首先数组是利用数组map方法去遍历arr的每一个值，然后进行于newValue的id进行对比，不同返回原来的项，相同返回newValue.

　　不装逼清晰点写法：

```
const updated = arr.map(function(item)\\{
    return item.id == newValue.id ? newValue : item ;
\\});
console.log(updated) // => [ \\{ id: 1, score: 1 \\}, \\{ id: 2, score: 2 \\}, \\{ id: 3, score: 3 \\} ]
```



### 数组去重

方案 A

```
// 遍历数组，建立新数组，利用indexOf判断是否存在于新数组中，不存在则push到新数组，最后返回新数组 
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

方案B

```
//遍历数组，利用object对象保存数组值，判断数组值是否已经保存在object中，未保存则push到新数组并用object[arrayItem]=1的方式记录保存,这个效率比A高
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

方案C

```
//ES6
const numbers = [1, 2, 1, 1, 2, 1, 3, 4, 1 ];
const uniq = [...new Set(numbers)] // => [ 1, 2, 3, 4 ];
const uniq2 = Array.from(new Set(numbers)) // => [ 1, 2, 3, 4 ];
```

方案D

```
//filter function unique (arr) \\{
     var res = arr.filter(function (item, index, array) \\{
            return array.indexOf(item) === index; //array.indexOf(item) === index 说明这个元素第一次出现，后面这个item再出现他的item肯定不是index了
\\}) return res; \\}
```



### 数组中是否存在某个值

**数组自带方法**

```
var arr = [1, 2, 4, 3, 5, 6]
console.log(arr.includes(4))
console.log(arr.some(item => item === 4))
console.log(arr.find(item => item === 4))
console.log(arr.findIndex(item => item === 4))
console.log(arr.indexOf(4) !== -1)
console.log(arr.filter(item => item === 4))
// for 循环，略
```

**其他各种"神奇"的算法**

- 先排序，然后二分法查找
- set 解法，利用 set 的唯一性，将目标值添加进 set，如果 set 长度没变的话，这个值就是存在的

```
var arr = [1,2,3,4,5,6]
var arrSet = new Set(arr)
let prevSetLen = arrSet.size
arrSet.add(5)
console.log(prevSetLen===arrSet.length)
```

- 利用数组的 join 方法，把所有数字用逗号拼起来，然后正则匹配，或是调 includes 方法



### 找出两个数组中的交集

**常规蠢办法**

- for 循环

```
var arr1 = [1, 2, 3]
var arr2 = [3, 4, 5, 6]

var commonArr = []
for (var i = 0; i < arr1.length; i++) \\{
  var _item = arr1[i]
  for (var j = 0; j < arr2.length; j++) \\{
    if (_item === arr2[j]) \\{
      commonArr.push(_item)
    \\}
  \\}
\\}
```

- ES6 的 filter 结合 includes 方法

```
var arr1 = [1, 2, 3]
var arr2 = [3, 4, 5, 6]

arr1.filter(item=>arr2.includes(item))
```

- 一个数组转对象，一个数组遍历看对象是否存在对应值

```
var arr1 = [1, 2, 3]
var arr2 = [3, 4, 5, 6]
var _obj = \\{\\}
let _tempArr = arr1.length > arr2.length ? arr2 : arr1
_tempArr.forEach(item => \\{
  _obj[item] = item
\\})
let commonArr = arr2.filter(item => _obj[item])
console.log(commonArr)
_obj = null
_tempArr = null
```

> 这里先判断数组长度，选一个短的数组，使得新创建的临时对象尽可能小。

- 如果不考虑单个数组里有重复项的话，可以先合并数组，然后再遍历合并后的数组，进行计次，大于2则是重叠的。

```
var arr1 = [1, 2, 3]
var arr2 = [3, 4, 5, 6]

var _tempArr = arr1.concat(arr2).sort()
var result = []
_tempArr.reduce((prev, now) => \\{
  if (prev === now) \\{
    result.push(now)
  \\}
  return now
\\})
```

- set 的使用，主要利用不可重复设置，判断长度是否有变化，而得出是否是重复了；或者直接用 has 方法

```
var arr1 = [1, 2, 3]
var arr2 = [3, 4, 5, 6]

var set = new Set(arr1)
var result = []
result = arr2.filter(item => arr1.has(item))
console.log(result)
```

**"神奇"的算法**

- 排序后，两个数组下标移动，两两比较

```
var arr1 = [1, 2, 8, 3 ]
var arr2 = [5, 6, 2, 3, 4]

arr1.sort() // [1,2,3]
arr2.sort() // [2,3,4,5,6]

var result = []
let arr1Index = 0
let arr2Index = 0
let runTimes = 0
while (arr1Index < arr1.length && arr2Index < arr2.length) \\{
  runTimes++
  let arr1Item = arr1[arr1Index]
  let arr2Item = arr2[arr2Index]
  if (arr1Item > arr2Item) \\{
    arr2Index++
  \\} else if (arr1Item < arr2Item) \\{
    arr1Index++
  \\} else \\{
    result.push(arr1Item)
    arr1Index++
    arr2Index++
  \\}
\\}
console.log(result)
console.log(runTimes) 
```



### 两个数组的并集

- set

```
var arr1 = [1, 2, 3]
var arr2 = [4, 5, 3, 6]
var result = [...new Set(arr1.concat(arr2))]
// var result = [...new Set([...arr1, ...arr2])]
```

- reduce

```
var arr1 = [1, 2, 3]
var arr2 = [4, 5, 3, 6]
var tempArr = [...arr1, ...arr2].sort()
var result = []
tempArr.reduce((prev, now) => \\{
  if (prev !== now) \\{
    result.push(now)
  \\}
  return now
\\}, null)
console.log(result)
```

- 转 json 对象

```
var arr1 = [1, 2, 3]
var arr2 = [4, 5, 3, 6]    
var obj = \\{\\}
arr1.forEach(item => (obj[item] = item))
arr2.forEach(item => (obj[item] = item))
var result = Object.values(obj)
console.log(result)
```



### 数组去重

效率上讲，转 obj 的方式 > set > reduce > includes/indexOf > 双重for循环

- 双重for循环

```
var arr1 = [1, 2, 3, 3, 4, 5, 6, 8]
var result = []
for (var i = 0; i < arr1.length; i++) \\{
  let _hasItem = false
  for (var j = 0; j < result.length; j++) \\{
    if (arr1[i] === result[j]) \\{
      _hasItem = true
      break
    \\}
  \\}
  if (!_hasItem) \\{
    result.push(arr1[i])
  \\}
\\}
console.log(result)
```

- includes/indexOf

```
var arr1 = [1, 2, 3, 3, 4, 5, 6, 8]
var result = []
arr1.forEach(item => \\{
  if (!result.includes(item)) \\{
    result.push(item)
  \\}
\\})
```

- reduce

```
var arr1 = [1, 2, 4, 5, 3, 3, 3, 6, 8]
arr1.sort()
var result = []
arr1.reduce((prev, now) => \\{
  if (now !== prev) \\{
    result.push(now)
  \\}
  return now
\\}, null)
```

- set

```
var arr1 = [1, 2, 4, 5, 3, 3, 3, 6, 8]
var result = [...new Set(arr1)]
```

- 转对象方式

```
var arr1 = [1, 2, 4, 5, 3, 3, 3, 6, 8]
var obj = \\{\\}
arr1.forEach(item => (obj[item] = item))
var result = Object.values(obj)
```



### 数组排序

**自带 sort**

```
var arr = [2,3,1,4,6]
arr.sort(); // [1,2,3,4,6]
arr.sort((a,b)=>a-b); // [1,2,3,4,6]
arr.sort((a,b)=>b-a); // [6,4,3,2,1]
```

**选择排序**

每一次选择遍历选择一个最小值，确定一个位置

```
var times = 0
function selectSort(arr) \\{
  // 没遍历一轮,将确定一个位置
  for (var i = 0; i < arr.length; i++) \\{
    // 假定当前项是剩余未排中最小的
    let minIndex = i
    // 从已经确定的位置之后一位开始遍历
    for (var j = i + 1; j < arr.length; j++) \\{
      // 假如找到比 min 还小的,更新最小值
      if (arr[j] < arr[minIndex]) \\{
        minIndex = j
      \\}
    \\}
    // 得到最小值,第i位确定
    let temp = arr[i]
    arr[i] = arr[minIndex]
    arr[minIndex] = temp
  \\}
\\}
```

**冒泡排序**

核心为两两按大小规则交换

```
function bubbSort(arr) \\{
  for (var i = 0; i < arr.length; i++) \\{
    // 74
    for (var j = i + 1; j < arr.length; j++) \\{
      // 如果后面一个大于前面一个,那么换位置
      if (arr[j] < arr[i]) \\{
        var temp = arr[j]
        arr[j] = arr[i]
        arr[i] = temp
      \\}
    \\}
  \\}
\\}
```

**快速排序**

1. 先随机选一个数(可选中间值)
2. 以这个数分组，小的放左边，大的放右边
3. 同理，在左边和右边的分组执行相同的操作，直到分组只剩一个元素

```
var arr = [74, 28, 60, 41, 29, 90, 52, 40]

function quickSort(arr)\\{
  // 递归出口
  if(arr.length<=1)\\{
    return arr
  \\}
  // 1. 选中值
  var basicNum = arr[Math.floor((arr.length - 1) / 2)]
  // 2. 左右分组
  var left = []
  var right = []
  arr.forEach(item=>\\{
    if(item>basicNum)\\{
      right.push(item)
        \\}
    else\\{
      left.push(item)
    \\}
  \\})
  // 3.递归执行左边和右边数组,并且合并结果
  return quickSort(left).concat(basicNum, quickSort(right))
\\}
```



### 数组方法

**charAt()方法可返回指定位置的字符   JavaScript String 对象**

例:stringObject.charAt(index)
index:表示字符串中某个位置的数字,即字符在字符串中的下标.

```
<script type="text/javascript">
   var str = "Hello worle!"
   document.write(str.charAt(1))   // e
</script>
```

**toUpperCase()方法用于把字符串转换成大写  JavaScript String 对象**
例:stringObjice.toUpperCase()

```
<script type="text/javascript">
  var str="Hello World!"
  document.write(str.toUpperCase())
</script>
```

**slice()方法可从已有的数组中返回选定的元素  JavaScript Array 对象**
arrayObject.slice(start,end)
start 必需，规定从何处开始选取。自己算
end   可选, 规定从何处结束选取。 结束不算

```
<script type="text/javascript">
    var arr = ["George","John","Thomas"]
    document.write(arr.slice(1,))  // John,Thomas  
    document.write(arr.slice(1,2)) // John
</script>
```

**toString()方法可把一个逻辑值转换为字符串,并返回结果。**
booleanObject.toString()

```
<script type="text/javascript">
     var boo = new Boolean(true)
     console.log(boo.toString())    // true
</script>
```

**delete 操作符用于删除对象的某个属性；返回值是 true,false**

```
 delete object.property     object 对象的名称 或计算结果为对象的表达式
  delete object['property']        property 要删除的属性
     var Employee = \\{
         age:28,
         name:'abc',
         designation:'developer'
     \\}
     console.log(delete Employee.age)
     console.log(Employee)
```







### js 判断一个 object 对象是否为空

```
if (JSON.stringify(data) === '\\{\\}') \\{
    return false // 如果为空,返回false，数组可以用同样的判断方式
\\}
if (Object.keys(object).length === 0) \\{
    return false // 如果为空,返回false，Object.keys(object)会返回一个空数组[]
\\}
```



### 判断对象或数组中元素是否存在

typeof data.archiveRecordPage !== undefined
一搬如果typeof后边是表达式，就要用括号括起来，否则不用括起来。另外一般要判断该层级之前的层级也要存在
----更新： hasOwnProperty也可以对象某对象是否存在



### 删除一个对象上的属性（key）

```
//利用es6的 ...运算符将其他属性和ａ属性分开来，这波操作很亮眼 ！const obj = \\{a: 1, b: 2, c: 3\\};
const \\{a, ...newObj\\} = obj;
console.log(newObj) // => \\{b: 2, c: 3\\};
```



### 两个Set对象相减

```
//利用filter对s1进行过滤 ，去掉s2中存在的数字const s1 = [ 1, 2, 3, 4, 5 ];
 const s2 = [ 2, 4 ];
 const subtracted = s1.filter(x => s2.indexOf(x) < 0);
 console.log(subtracted);//[1,3,5]
```

 同理这样是可以去出一个数组中指定的元素

```
//去掉s3中的2和4
 const s3 = [ 1, 2, 3, 4, 5, 4, 5, 6, 2, 2, 4 ];
 const s2 = [ 2, 4 ];
 const subtracted1 = s3.filter(x => s2.indexOf(x) < 0);
 console.log(subtracted1); // [1, 3, 5, 5, 6]
```







### 将时间戳转换为时间格式

在网上找的一个示例，如果是php写的接口，一般是需要在返回的时间戳字段上乘以1000的，java写的接口一般不需要，这个与精确度有关。一个是精确到秒，一个是精确到毫秒。当然，在框架VUE中另有其他写法，这里暂时不做深究。

```
formatDate(timestamp) \\{
    var date = new Date(timestamp);//时间戳为10位需*1000，时间戳为13位的话不需乘1000
    var Y = date.getFullYear() + '-';
    var M = (date.getMonth()+1 < 10 ? '0'+(date.getMonth()+1) : date.getMonth()+1) + '-';
    var D = (date.getDate() < 10 ? '0'+(date.getDate()) : date.getDate()) + ' ';
    var h = (date.getHours() < 10 ? '0'+(date.getHours()) : date.getHours()) + ':';
    var m = (date.getMinutes() < 10 ? '0'+(date.getMinutes()) : date.getMinutes()) + ':';
    var s = (date.getSeconds() < 10 ? '0'+(date.getSeconds()) : date.getSeconds());
    return Y+M+D+h+m+s;
\\}
```
