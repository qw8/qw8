---
title: JavaScript数组
date: 2020-02-06 21:10:40
categories: 
- 前端知识
tags:
- JavaScript
- 数组
---

### 数组方法

- Array.length：数组的大小

- join()：用指定的分隔符将数组每一项拼接为字符串

- push() ：向数组的末尾添加新元素，返回值为添加完后的数组的长度

- pop()：删除数组的最后一项，返回值是删除的元素

- shift()：删除数组的第一项， 返回值是删除的元素

- unshift()：向数组首位添加新元素，返回值是添加完后的数组的长度

- slice()：按照条件查找出其中的部分元素

- splice()：对数组进行增删改

- fill(): 方法能使用特定值填充数组中的一个或多个元素

- filter():“过滤”功能

- concat()：用于连接两个或多个数组

- indexOf()：检测当前值在数组中第一次出现的位置索引

- lastIndexOf()：检测当前值在数组中最后一次出现的位置索引

- every()：判断数组中每一项都是否满足条件

- some()：判断数组中是否存在满足条件的项

- includes()：判断一个数组是否包含一个指定的值

- sort()：对数组的元素进行排序

- reverse()：对数组进行倒序

- forEach()：ES5 及以下循环遍历数组每一项

- map()：ES6 循环遍历数组每一项

- copyWithin():用于从数组的指定位置拷贝元素到数组的另一个指定位置中

- find():返回匹配的值

- findIndex():返回匹配位置的索引

- Array.toLocaleString()：把数组转换成局部字符串

- Array.toString()：将数组转换成一个字符串

- flat()、flatMap()：扁平化数组

- entries() 、keys() 、values():遍历数组 

  [22个超详细的 JS 数组方法](https://www.bilibili.com/read/cv9715493)



### 数组对象有哪些原生方法，列举一下

pop、push、shift、unshift、splice、reverse、sort、concat、join、slice、toString、indexOf、lastIndexOf、reduce、reduceRight
forEach、map、filter、every、some



### 数组的常用方法

#### 1.Array.map()

此方法是将数组中的每个元素调用一个提供的函数，结果作为一个新的数组返回，并没有改变原来的数组。

- map() 方法返回一个新数组，数组中的元素为原始数组元素调用函数处理后的值。
- map() 方法按照原始数组元素顺序依次处理元素。
- 注意： map() 不会对空数组进行检测。
- 注意： map() 不会改变原始数组。

##### 字符串数组转数字数组 .map(Number)

```
var strArr = ['1','2','3'];
var newArr = strArr.map(Number);
console.log(newArr);
// 控制台打印结果   [1,2,3]
```

##### 数字数组转字符串数组 .map(String)

```
var numberArr = [1,2,3];
var newArr = numberArr.map(String);
console.log(newArr);
// 控制台打印结果   ['1','2','3']
```

##### map内部函数更改数组内部数据

```
// 将数组中每个元素乘2返回一个新的数组
let arr = [1, 2, 3, 4, 5];
let newArr = arr.map(x => x * 2);
// arr= [1, 2, 3, 4, 5]   原数组保持不变
// newArr = [2, 4, 6, 8, 10] 返回新数组
```



#### 2.Array.forEach()

此方法是将数组中的每个元素执行传进提供的函数，没有返回值，直接改变原数组，注意和 map 方法区分

```js
let arr = [1, 2, 3, 4, 5];
num.forEach(x => x * 2);
// arr = [2, 4, 6, 8, 10]  数组改变,注意和map区分
```

#### 3.Array.filter()

此方法是将所有元素进行判断，将满足条件的元素作为一个新的数组返回

```js
let arr = [1, 2, 3, 4, 5]
    const isBigEnough => value => value >= 3
    let newArr = arr.filter(isBigEnough )
    //newNum = [3, 4, 5] 满足条件的元素返回为一个新的数组
```

#### 4.Array.every()

此方法是将所有元素进行判断返回一个布尔值，如果所有元素都满足判断条件，则返回 true，否则为 false：

```js
	let arr = [1, 2, 3, 4, 5]
    const isLessThan4 => value => value < 4
    const isLessThan6 => value => value < 6
    arr.every(isLessThan4 ) //false
    arr.every(isLessThan6 ) //true
```

##### 语法:array.every( function ( item, index,arr) \\{\\} )

- 第一个参数: item,必须,当前元素的值
- 第二个参数 : index,可选,当前元素在数组中的索引值
- 第三个参数 : arr,当前元素所处的数组对象

##### every方法特点

(1)循环次数 !== 数组长度

(2)函数内部的return

- return true : 循环继续 当前元素满足条件,继续判断,如果循环执行完毕还是true,则every的返回值就是true

- return false : 循环结束,当前元素不满足条件,every的返回值也是false


(3)every方法的返回值

- return true : 全部元素都满足条件

- return false : 有元素不满足条件


##### 注意点:

- every()方法不会对空数组进行检测
- every()方法不会改变原始数组


##### 应用场景 : 开关思想,购物车全选



#### 5.Array.some()

此方法是将所有元素进行判断返回一个布尔值，如果存在元素都满足判断条件，则返回 true，若所有元素都不满足判断条件，则返回 false：

```js
	let arr= [1, 2, 3, 4, 5]
    const isLessThan4 => value => value < 4
    const isLessThan6 => value => value > 6
    arr.some(isLessThan4 ) //true
    arr.some(isLessThan6 ) //false
```

groupList.value=[\\{name:'xx',name:'']怎么判断有一个name为空？

```
	// 使用some()方法检查是否至少有一个对象的name属性为空
    let isEmpty = groupList.value.some((item) => item.name === '')
    console.log(isEmpty)
    if (isEmpty) \\{
      showToast('请先输入上一个分组名称')
      return
    \\}
```



#### 6.Array.reduce()

此方法是所有元素调用返回函数，返回值为最后结果,传入的值必须是函数类型：

```js
let arr = [1, 2, 3, 4, 5];
const add = (a, b) => a + b;
let sum = arr.reduce(add);
//sum = 15  相当于累加的效果
```

与之相对应的还有一个 Array.reduceRight() 方法，区别是这个是从右向左操作的



#### 7.Array.push()

此方法是在数组的后面添加新加元素，此方法改变了数组的长度：

#### 8.Array.pop()

此方法在数组后面删除最后一个元素，并返回数组，此方法改变了数组的长度：

```js
let arr = [1, 2, 3, 4, 5];
arr.pop();
console.log(arr); //[1, 2, 3, 4]
console.log(arr.length); //4
```

#### 9.Array.shift()

此方法在数组后面删除第一个元素，并返回数组，此方法改变了数组的长度：

```js
let arr = [1, 2, 3, 4, 5];
arr.shift();
console.log(arr); //[2, 3, 4, 5]
console.log(arr.length); //4

```

#### 10.Array.unshift()

此方法是将一个或多个元素添加到数组的开头，并返回新数组的长度：

```js
let arr = [1, 2, 3, 4, 5];
arr.unshift(6, 7);
console.log(arr); //[6, 7, 2, 3, 4, 5]
console.log(arr.length); //7

```

#### 11.Array.isArray()

判断一个对象是不是数组，返回的是布尔值

#### 12.Array.concat()

此方法是一个可以将多个数组拼接成一个数组：

```js
let arr1 = [1, 2, 3]
      arr2 = [4, 5]
  let arr = arr1.concat(arr2)
  console.log(arr)//[1, 2, 3, 4, 5]

```

#### 13.Array.toString()

 此方法将数组转化为字符串：

```js
let arr = [1, 2, 3, 4, 5];
   let str = arr.toString()
   console.log(str)// 1,2,3,4,5

```

#### 14.Array.join()

此方法也是将数组转化为字符串：

```js
let arr = [1, 2, 3, 4, 5];
   let str1 = arr.toString()
   let str2 = arr.toString(',')
   let str3 = arr.toString('##')
   console.log(str1)// 12345
   console.log(str2)// 1,2,3,4,5
   console.log(str3)// 1##2##3##4##5
```

通过例子可以看出和 toString 的区别，可以设置元素之间的间隔~

#### 15.Array.splice(开始位置， 删除的个数，元素)

万能方法，可以实现增删改：

```js
let arr = [1, 2, 3, 4, 5];
     let arr1 = arr.splice(2, 0 'haha')
     let arr2 = arr.splice(2, 3)
     let arr1 = arr.splice(2, 1 'haha')
     console.log(arr1) //[1, 2, 'haha', 3, 4, 5]新增一个元素
     console.log(arr2) //[1, 2] 删除三个元素
     console.log(arr3) //[1, 2, 'haha', 4, 5] 替换一个元素
```



### 一、变异方法（会改变原始数组）

1.push

向数组的末尾增加一个元素或多个元素，并返回新的长度

```
let arr = [0,1,2]
console.log(arr.push(3)) //返回新的数组长度 4
console.log(arr) //[0,1,2,3]
```

2.pop

删除并返回数组的最后一个元素

```
let arr = [0,1,2]
console.log(arr.pop()) //删除并返回数组最后一个元素 2
console.log(arr) //[0,1]
```

3.shift

删除并返回数组的第一个元素

```
let arr = [0,1,2]
console.log(arr.shift()) //删除并返回数组第一个元素 0
console.log(arr) //[1,2]
```

4.unshift

向数组的开头增加一个或多个元素，并返回新的长度

```
let arr = [0,1,2]
console.log(arr.unshift(-2,-1)) //返回新的数组长度 5
console.log(arr) //[-2, -1, 0, 1, 2]
```

5.splice

对数组的内容进行删除，增加，替换。

```
arr.splice(index,howmany,item1,item2...)
```

index是执行操作的位置，必须

howmany是删除的个数，为0时就是不删除只增加

```
let arr = ["方案1", "方案2", "方案3", "方案4", "方案5"];

for (let i = 0, len = arr.length; i < len; i++) \\{
    if (
        arr[i] === "方案1" ||
        arr[i] === "方案2" ||
        arr[i] === "方案3"
    ) \\{
        arr.splice(i, 1);
        i--; //因为删除后，数组长度会减1，所以 i 也要减1，才能对应新的数组
    \\}
\\}
console.log(arr)//["方案4", "方案5"]
```

6.sort

对数组排序

```
let array = [1, 2, 10, 18, 3, 95, 2, 5];
//升序
array.sort((a,b)=>a-b); 
//降序
array.sort((a,b)=>b-a);
```

7.reverse

颠倒数组中的元素

```
let arr = [1,2,3]
arr.reverse()
console.log(arr) //[3,2,1]
```



### 二、非变异方法（不会改变原始数组）

1. map

返回一个新数组，新数组的元素为原始数组元素调用函数处理后的值

```
let arr = [1,2,3]
let newArr = arr.map((item,index)=>item+1)
console.log(newArr) //[2, 3, 4]
```

2. reduce

reduce方法接收一个函数作为累加器，数组中的每个值（从左到右）开始缩减，最终计算的得到一个值

```
array.reduce(function(total, currentValue, currentIndex), initialValue)
```

（1）累加器

```
let arry = [1, 25, 85, 36];
let totalValue = arry.reduce((total, currentValue)=> total * currentValue);
console.log(totalValue);//76500
```

（2）访问嵌套对象

```
<script>
    let obj = \\{
        a: \\{
            b: \\{
                c: 666
            \\}
        \\}
    \\}

    var str = 'a.b.c';

    let newArr = str.split('.').reduce(function (total, current) \\{
        return total[current]
    \\}, obj)
    
    console.log(newArr)
</script>
```

3. filter

返回符合条件的项组成的数组

```
let array = [1, 2, 5, 6];
let arrayNew = array.filter(item => item > 2); 
console.log(arrayNew) //[5,6]
```

4. concat

用于连接两个或者多个数组，相同的值不会被覆盖

```
let arr = [1, 2, 3];
let newArr = a.concat(3,4, 5);
console.log(newArr) //[1,2,3,3,4,5]
```

5. slice

从已有的数组中返回选定的元素

```
array.slice(start,end)
```

start：规定从何处开始选取

end：规定何处结束

如果都没有指定，array.slice()则将拷贝整个数组

```
let arr = [1, 2, 3];
let newArr = arr.slice(1,3) 
console.log(newArr) //[2,3]
```

6. join

array.join(separator) // separator= "." 分隔符，默认为,

将所有数组元素拼接成字符串

```
const arr = [1,2,3,4,5];
console.log(arr.join("")) // 12345
```

7. toString

将数组作为字符串返回

注意：使用toString()方法将数组转为字符串时，只能转化数值数组或字符串数组。不能用在对象数组上

```
const arr = [1, 2, 3, 4, 5];
let str = arr.toString()
console.log(str) // 1,2,3,4,5

const arr2 = [\\{name:'张三'\\},\\{age:24\\}];
console.log(arr2.toString())  // [object Object],[object Object]
```



### 三、对数组的检测

#### 1.every

对数组中的每一项运行给定函数，全部满足条件则返回true

```
let arr = array.every(value => value > 18)
```

#### 2.some

对数组中的每一项运行给定函数，如果有一项满足条件则返回true

#### 3.indexOf

返回第一个与给定参数相等的数组元素的索引，没有的话返回-1

例子：

```
let arr = [1,2,3,56,57]
arr.indexOf(1)
```

#### 4.lastIndexOf

返回最后一个与给定参数相等的数组元素的索引，没有的话返回-1

#### 5.includes

检测数组是否包含某个数

```
[5,6,7,8,24,25,26,27,28,29,30,31,32,33].includes(val)
```

存在返回true，不存在返回false

#### 6.find

找出第一个符合条件的数组成员，如果没有符合条件的则返回undefined

```
[1, 4, -5, 10].find((n) => n < 0)
```

#### 7.findIndex

返回第一个符合条件的数组成员的位置，如果没有符合条件的，则返回-1

方法返回数组中通过测试的第一个元素的索引（作为函数提供）。

findIndex() 方法对数组中存在的每个元素执行一次函数：

如果找到函数返回 true 值的数组元素，则 findIndex() 返回该数组元素的索引（并且不检查剩余值）
否则返回 -1

注释：findIndex() 不会为没有值的数组元素执行函数。

注释：findIndex() 不会改变原始数组。

```
var ages = [3, 10, 18, 20];
 
function checkAdult(age) \\{
    return age >= 18;
\\}

ages.findIndex(checkAdult)
```

##### 定义和用法：

findIndex() 方法返回传入一个测试条件（函数）符合条件的数组第一个元素位置。
有两点要注意：

1.当数组中的元素在测试条件时返回 true 时, findIndex() 返回符合条件的元素的索引位置，之后的值不会再调用执行函数。例子2就是一个很好的说明，即使后面的666和66大于50，但是它只找到99，就不会执行后面的循环了。
2.如果没有符合条件的元素返回 -1

```
var arr = ['a','b','c','d'];
   var flag = arr.findIndex(item => \\{
        return item === 'c';
    \\})
    console.log(flag) // 得到： 2

var arr2 = [1,18,2,99,666,44,66];
    var flag2 = arr2.findIndex(item => \\{
        return item > 50;
    \\});
    console.log(flag2)   // 得到： 3

var arr3 = ['red','pink','green'];
    var flag3 = arr3.findIndex(item => item === 'yellow')
    console.log(flag3)  // 得到：-1
```







### JavaScript 类数组对象的定义？

一个拥有 length 属性和若干索引属性的对象就可以被称为类数组对象，类数组对象和数组类似，但是不能调用数组的方法。

常见的类数组对象有 arguments 和 DOM 方法的返回结果，还有一个函数也可以被看作是类数组对象，因为它含有 length属性值，代表可接收的参数个数。

常见的类数组转换为数组的方法有这样几种：

（1）通过 call 调用数组的 slice 方法来实现转换

```js
Array.prototype.slice.call(arrayLike);
```

（2）通过 call 调用数组的 splice 方法来实现转换

```js
Array.prototype.splice.call(arrayLike, 0);
```

（3）通过 apply 调用数组的 concat 方法来实现转换

```js
Array.prototype.concat.apply([], arrayLike);
```

（4）通过 Array.from 方法来实现转换

```js
Array.from(arrayLike);
```

详细的资料可以参考：
[《JavaScript 深入之类数组对象与 arguments》](https://github.com/mqyqingfeng/Blog/issues/14)
[《javascript 类数组》](https://segmentfault.com/a/1190000000415572)
[《深入理解 JavaScript 类数组》](https://blog.lxxyx.cn/2016/05/07/\\%E6\\%B7\\%B1\\%E5\\%85\\%A5\\%E7\\%90\\%86\\%E8\\%A7\\%A3JavaScript\\%E7\\%B1\\%BB\\%E6\\%95\\%B0\\%E7\\%BB\\%84/)



### 数组和对象有哪些原生方法，列举一下？

数组和字符串的转换方法：toString()、toLocalString()、join() 其中 join() 方法可以指定转换为字符串时的分隔符。

数组尾部操作的方法 pop() 和 push()，push 方法可以传入多个参数。

数组首部操作的方法 shift() 和 unshift() 重排序的方法 reverse() 和 sort()，sort() 方法可以传入一个函数来进行比较，传入前后两个值，如果返回值为正数，则交换两个参数的位置。

数组连接的方法 concat() ，返回的是拼接好的数组，不影响原数组。

数组截取办法 slice()，用于截取数组中的一部分返回，不影响原数组。

数组插入方法 splice()，影响原数组查找特定项的索引的方法，indexOf() 和 lastIndexOf() 迭代方法 every()、some()、filter()、map() 和 forEach() 方法

数组归并方法 reduce() 和 reduceRight() 方法

详细资料可以参考：
[《JavaScript 深入理解之 Array 类型详解》](http://cavszhouyou.top/JavaScript\\%E6\\%B7\\%B1\\%E5\\%85\\%A5\\%E7\\%90\\%86\\%E8\\%A7\\%A3\\%E4\\%B9\\%8BArray\\%E8\\%AF\\%A6\\%E8\\%A7\\%A3.html)



### 数组的 fill 方法？

fill() 方法用一个固定值填充一个数组中从起始索引到终止索引内的全部元素。不包括终止索引。
fill 方法接受三个参数 value，start 以及 end，start 和 end 参数是可选的，其默认值分别为 0 和 this 对象的 length 属性值。

详细资料可以参考：
[《Array.prototype.fill()》](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/fill)



### map、filter、reduce相关

参考链接：

https://atendesigngroup.com/blog/array-map-filter-and-reduce-js

http://zerosoul.github.io/2016/12/06/array-filter-map-reduce-in-js



### 分别阐述join()、split()、slice()、splice()

- join()

  用于把数组中的所有元素通过指定的分隔符进行分隔放入一个字符串。所带的参数为分割字符串的分隔符，默认是以逗号分开。归属于 Array

- split()

  用于把一个字符串通过指定的分隔符进行分隔成数组

- slice() 方法可从已有的数组中返回选定的元素。该方法并不会修改数组，而是返回一个子数组。如果想删除数组中的一段元素，应该使用方法 Array.splice()

- splice() 方法向/从数组中添加/删除项目，然后返回被删除的项目。返回的是含有被删除的元素的数组。



### join() 方法将数组作为字符串返回

join() 方法用于把数组中的所有元素放入一个字符串。

元素是通过指定的分隔符进行分隔的。 arrayObject.join(*separator*)， 默认为使用逗号分隔

```
var arr = ['a','b','c','d','e','f'];
arr.join() // a,b,c,d,e,f
arr.join("-") // a-b-c-d-e-f
```

```
<!DOCTYPE html>
<html>
<body>
<h1>JavaScript 数组</h1>
<p>join() 方法将数组作为字符串返回。</p>
<p id="demo"></p>
<script>
const fruits = ["Banana", "Orange", "Apple", "Mango"];
document.getElementById("demo").innerHTML = fruits.join("+");
</script>
</body>
</html>
```

结果

```
Banana+Orange+Apple+Mango
```

#### vue3模板中使用

info.clientStaffs为["马振东", "建小投", "李垒垒", "邓雪 (主服务)"]，转成、分隔字符串，vue3 

```
 <span class="value">\\\{\\\{ info.clientStaffs||'--' \\\}\\\}</span>
```

在Vue3中，可以使用数组的`join`方法结合逻辑判断实现，以下是实现代码：

```
<span class="value">\\\{\\\{ info.clientStaffs?.length ? info.clientStaffs.join('、') : '--' \\\}\\\}</span>
```

**效果说明**：

- 当数组有元素时：显示`马振东、建小投、李垒垒、邓雪 (主服务)`
- 当数组为空或未定义时：显示`--`

**代码解析**：

1. `?.` 可选链操作符：安全访问可能为`null/undefined`的数组
2. `length`判断：过滤空数组的情况
3. `join('、')`：用中文顿号连接数组元素
4. 三元表达式：满足条件时返回处理后的字符串，否则返回占位符

如果环境不支持可选链操作符，可以用以下兼容写法：

```
<span class="value">\\\{\\\{ info.clientStaffs && info.clientStaffs.length ? info.clientStaffs.join('、') : '--' \\\}\\\}</span>
```



### js中split字符串分割

String.split() 执行的操作与 [Array.join](http://www.w3school.com.cn/jsref/jsref_join.asp) 执行的操作是相反的。

split() 方法用于把一个字符串分割成字符串数组。stringObject.split(separator,howmany)  separator：必需。字符串或正则表达式，从该参数指定的地方分割 stringObject。 howmany： 可选。该参数可指定返回的数组的最大长度。如果设置了该参数，返回的子串不会多于这个参数指定的数组。 如果没有设置该参数，整个字符串都会被分割，不考虑它的长度。 

```
var str="Do you want to have a holiday?"
str.split(" ")  //  Do,you,want,to,have,a,holiday?
str.split(/\s+/)  //  Do,you,want,to,have,a,holiday? 正则表达式分割
str.split("") // D,o, ,y,o,u, ,w,a,n,t, ,t,o, ,h,a,v,e, ,a, ,h,o,l,i,d,a,y,?
str.split(" ",3) //  Do,you,want  3表示返回长度为3的数组

var str="Do-you-want-to-have-a-holiday?"
str.split("-") //  Do,you,want,to,have,a,holiday?
```

#### 1.通过单一字符将字符串切割成多字符

```
var data= "烈日当头已数月有余，天气高温，汗流浃背，不知所言。";
var str = data.split(',');
结果：
str[0] //烈日当头已数月有余
str[1] //天气高温
str[2] //汗流浃背
str[3] //不知所言。
```

#### 2.通过多字符将字符串切割成多字符串

```
var data= "外面在下雨，天气真冷，你现在到哪里了呀，我们待会一起吃饭吧。";
var str = data.split(/在,/);
结果：
str[0] //外面
str[1] //下雨
str[2] //天气真冷
str[3] //你现
str[4] //到哪里了呀
str[5] //我们待会一起吃饭吧。
```

####  3.通过字符串将字符串切割成多字符串

```
var data = "abbcaaflajbbcafdfbbcioerfadef";
var str = data.split('bbc');
结果：
str[0] //a
str[1] //aaflaj
str[2] //afdf
str[3] //ioerfadef
```



### 求数组的最大值

Math.max.apply(null, 数组)

```js
var a = [1, 2, 3, 5];
alert(Math.max.apply(null, a)); //最大值
alert(Math.min.apply(null, a)); //最小值
```



### Array.slice() 与 Array.splice() 的区别？

slice -- “读取”数组指定的元素，不会对原数组进行修改

- 语法：arr.slice(start, end)
- start 指定选取开始位置（含）
- end 指定选取结束位置（不含）

splice

- “操作”数组指定的元素，会修改原数组，返回被删除的元素
- 语法：arr.splice(index, count, [insert Elements])
- index 是操作的起始位置
- count = 0 插入元素，count > 0 删除元素
- [insert Elements] 向数组新插入的元素



### js删除数组中的元素

在JavaScript中，可以通过以下几种方法删除数组中的元素：

#### 使用splice()方法：

```
let arr = [1, 2, 3, 4, 5];
let index = 2;  // 要删除的元素的索引
arr.splice(index, 1);
console.log(arr);  // 输出: [1, 2, 4, 5]
```

使用splice()方法，可以指定要删除的元素的索引和数量。在上面的例子中，我们删除了索引为2的元素。

#### 使用delete关键字：

```
let arr = [1, 2, 3, 4, 5];
let index = 2;  // 要删除的元素的索引
delete arr[index];
console.log(arr);  // 输出: [1, 2, empty, 4, 5]
```

使用delete关键字可以删除指定索引处的元素，但是会将该位置的元素设置为undefined，并且不会改变数组的长度。

#### 使用filter()方法：

```
let arr = [1, 2, 3, 4, 5];
let index = 2;  // 要删除的元素的索引
arr = arr.filter((value, idx) => idx !== index);
console.log(arr);  // 输出: [1, 2, 4, 5]
```

使用filter()方法，可以通过筛选出不需要删除的元素，重新生成一个新的数组来删除指定索引处的元素。

#### 使用pop()或shift()方法：

```js
let arr = [1, 2, 3, 4, 5];
let index = 2;  // 要删除的元素的索引
if (index === 0) \\{
  arr.shift();
\\} else if (index === arr.length - 1) \\{
  arr.pop();
\\} else \\{
  arr = arr.slice(0, index).concat(arr.slice(index + 1));
\\}
console.log(arr);  // 输出: [1, 2, 4, 5]
```

在上面的例子中，如果要删除的元素处于数组的首位，我们使用shift()方法删除该元素；如果要删除的元素处于数组的末尾，我们使用pop()方法删除该元素；否则，我们使用slice()方法删除指定索引处的元素，并将前半部分和后半部分重新拼接成一个新的数组。

请注意，以上代码只是展示了如何删除数组中的元素，实际应用中需要考虑到数组的长度变化以及是否需要保留原数组等因素。



### 使用splice删除数组元素

> 使用 splice 而不是 delete, 它会删除对象属性，但不会重新索引数组或更新其长度

```
  let myArray = ["a", "b", "c", "d"] 
  // 错误
  delete myArray[2]

  // 更优
  myArray.splice(0, 2) ["a", "b"]
```



### 删除重复值

> 忘记for循环

```js
  const array  = [5,4,7,8,9,2,7,5];
  // 普通
  array.filter((item,idx,arr) => arr.indexOf(item) === idx);

  // 简写
  const nonUnique = [...new Set(array)];
```



### 根据属性删除数组中的一个对象

```js
 // 根据属性删除数组中的对象,利用filter进行过滤数组中id相同的项
 const initial = [ \\{id: 1, score: 1\\}, \\{id: 2, score: 2\\}, \\{id: 3, score: 4\\}];
 const removeId = 3;
 const without3 = initial.filter(x => x.id !== removeId);
 console.log(without3) // => [ \\{ id: 1, score: 1 \\}, \\{ id: 2, score: 2 \\} ]
```



### JS删除数组中某个元素的几种方式

#### 第一种：删除最后一个元素

pop

- **优点**：简单、直接，修改原数组。
- **缺点**：会改变原数组，如果你需要保留原数组不变，这可能不是最好的选择。
- **适用场景**：当你不需要保留原数组，并且希望操作简洁时。

```
var arr = [1,2,3,4,5]
arr.pop()
// arr => [1,2,3,4]
```

slice

- **优点**：不改变原数组，返回一个新的数组。
- **缺点**：创建了一个新的数组，可能会占用更多内存。
- **适用场景**：当你需要保留原数组不变，并且创建一个新数组没有问题时。

```js
var arr = [1,2,3,4,5]
var new_arr = arr.slice(0, -1)
// arr => [1,2,3,4,5]
// new_arr => [1,2,3,4]

var arr = [1,2,3,4,5]
var new_arr = arr.slice(0, arr.length - 1)
// arr => [1,2,3,4,5]
// new_arr => [1,2,3,4]
```

splice

- **优点**：可以同时删除并获取被删除的元素，修改原数组。
- **缺点**：会改变原数组，如果只是想删除元素而不关心被删除的元素，那么这个方法显得有些多余。
- **适用场景**：当你需要删除元素并且还需要知道被删除的是什么时。

```js
var arr = [1,2,3,4,5]
var new_arr = arr.splice(-1)
// arr => [1,2,3,4]
// new_arr => [5]

var arr = [1,2,3,4,5]
var new_arr = arr.splice(-1, 1)
// arr => [1,2,3,4]
// new_arr => [5]

var arr = [1,2,3,4,5]
var new_arr = arr.splice(arr.length - 1)
// arr => [1,2,3,4]
// new_arr => [5]

var arr = [1,2,3,4,5]
var new_arr = arr.splice(arr.length - 1, 1)
// arr => [1,2,3,4]
// new_arr => [5]
```

for

- **优点**：灵活，可以进行更复杂的逻辑处理。
- **缺点**：代码较长，可读性较低，性能上不如内置方法。
- **适用场景**：当你需要执行额外的操作或有特殊条件时。

```js
var arr = [1,2,3,4,5]
var new_arr = []
for (let i = 0, len = arr.length; i < len; i++) \\{
    if (i < len - 1) \\{
        new_arr.push(arr[i])
    \\}
\\}
// arr => [1,2,3,4,5]
// new_arr => [1,2,3,4]
```

length

- **优点**：非常高效，直接截断数组。
- **缺点**：会改变原数组，而且这种用法不够直观，可能会影响代码的可读性。
- **适用场景**：当你追求极致性能，并且确定要修改原数组时。

```
var arr = [1,2,3,4,5]
arr.length = arr.length - 1
// arr => [1,2,3,4]
```

##### 总结

选择哪种方法来删除数组的最后一个元素取决于具体的应用场景和需求。每种方法都有其优缺点

- 如果你需要保留原数组不变，使用 `slice()`。
- 如果你需要删除元素并且想要得到被删除的元素，使用 `splice()`。
- 如果你不在乎保留原数组，并且追求简洁，使用 `pop()`。
- 如果你需要执行额外的逻辑或者有特殊的条件，使用 `for` 循环。
- 如果你追求极致性能，并且确定要修改原数组，可以考虑设置 `length` 属性。

在大多数情况下，`pop()` 和 `slice()` 是最常用的两种方法，因为它们简单易懂，分别适用于修改原数组和保持原数组不变的情况。对于你的具体情况，如果没有特别的需求，通常推荐使用 `pop()` 或 `slice()`。

#### 第二种: 删除第一个元素

shift 删除

```
var arr = [1,2,3,4,5]
arr.shift()
// arr => [2,3,4,5]
```

slice 删除

```
var arr = [1,2,3,4,5]
var new_arr = arr.slice(1)
// arr => [1,2,3,4,5]
// new_arr => [2,3,4,5]
```

splice 删除

```
var arr = [1,2,3,4,5]
var new_arr = arr.splice(0, 1)
// arr => [2,3,4,5]
// new_arr => [1]
```

#### 第三种：删除数组中某个指定下标的元素

splice 删除

```
var delete_index = 2
var arr = [1,2,3,4,5]
// arr => [1,2,3,4,5]
var new_arr = arr.splice(delete_index, 1)
// new_arr => [3]
// arr => [1,2,4,5]
```

for 删除

```js
var delete_index = 2,
    arr = [1,2,3,4,5],
    new_arr = []

for (let i = 0, len = arr.length; i < len; i++) \\{
    if (i != delete_index) \\{
        new_arr.push(arr[i])
    \\}
\\}

// arr => [1,2,3,4,5]
// new_arr => [1,2,4,5]
```

注意：

1. 不可以使用 delete 方式删除数组中某个元素，此操作会造成稀疏数组，被删除的元素的为位置依然存在为empty，且数组的长度不变

2. 不可以使用 forEach 方法比对数组下标值，因为 forEach 在循环的时候是无序的

#### 第四种：删除数组中某个指定元素的元素

splice 删除

```
var element = 2,
    arr = [1,2,3,4,5]

arr.splice(arr.indexOf(2), 1)
// arr => [1,3,4,5]
```

filter 删除

```
var arr = [1,2,3,4,5],
    element = 2

arr = arr.filter(item => item != element)
// arr => [1,3,4,5]
```

forEach、map、for 删除

```js
var arr = [1,2,3,4,5],
    element = 2,
    new_arr = []
arr.forEach(item => (item != element && new_arr.push(item)))
// new_arr => [1,3,4,5]

// map 同理

var arr = [1,2,3,4,5],
    element = 2,
    new_arr = []

for (let i = 0; i < arr.length; i++) \\{
    arr[i] != element && new_arr.push(arr[i])
\\}
// new_arr => [1,3,4,5]
```

Set 删除

```
var arr = [1,2,3,4,5],
    element = 2
var new_set = new Set(arr)
new_set.delete(element)
var new_arr = [...new_set]
// new_arr => [1,3,4,5]
```

原文链接：https://blog.csdn.net/Li_dengke/article/details/105249837



###  数组去重的方法（[参考链接](https://github.com/mqyqingfeng/Blog/issues/27)）

1、先将原数组进行排序，使重复元素在相邻位置，创建新数组，并赋值元数组的第一项，检查原数组中的第i个元素与新数组中的最后一个元素是否相同，如果不相同，则将该元素存入新数组中。

```js
function unique(arr)\\{ 
    arr.sort(); //先排序 ，这里不需要参数
    var res = [arr[0]];  
    for (var i = 1; i < arr.length; i++) \\{  
        if (arr[i] !== res[res.length - 1]) \\{   
        	res.push(this[i]); 
      	\\} 
   \\} 
   return res;
\\}
```

2、创建一个空对象和一个空数组，将数组的数值以对象属性的形式保存，并赋值1，push到新数组中，后续遍历数组时通过数组的值以属性的方式访问对象，从而达到验证重复的目的。（较推荐）

```
function unique(arr) \\{ 
var res = [];
var hash = \\{\\};
for (var i = 0; i < arr.length; i++) \\{  
    if (!hash[arr[i]]) \\{   
       res.push(arr[i]);  
       hash[arr[i]] = 1; 
      \\} 
   \\} 
   return res;
\\}
```

3.扩展运算符和 Set 结构相结合，就可以去除数组的重复成员

```js
// 去除数组的重复成员
[...new Set([1, 2, 2, 3, 4, 5, 5])];
// [1, 2, 3, 4, 5]

```

4.使用set去重

```
function removeRepeatArr(arr) \\{
    return Array.from(new Set(arr));
\\}

const arr = [1, 2, 1, 2, 3, 3, 4, 5];

console.log(removeRepeatArr(arr));
// [ 1, 2, 3, 4, 5   ]
```

5.ES5

```js
function unique(arry) \\{
  const temp = [];
  arry.forEach(e => \\{
    if (temp.indexOf(e) == -1) \\{
      temp.push(e);
    \\}
  \\});
  return temp;
\\}
```

6.ES6

```js
function unique(arr) \\{
  return Array.from(new Set(arr));
\\}
```

7.双重for循环依次比较

将结果函数中的元素与原数组中的元素依次比较，重复的元素舍弃，不重复的元素添加仅结果函数。

```
function removeRepeatArr(arr) \\{
    const result = [];
    for (let i = 0, len = arr.length; i < len; i++) \\{
        let isRepeat = false;
        for (let j = 0, _len = result.length; j < _len; j++) \\{
            if (result[j] === arr[i]) \\{
                isRepeat = true;
                break;
            \\}
        \\}
        if (!isRepeat) \\{
            result.push(arr[i]);
        \\}
    \\}

    return result;
\\}

const arr = [1, 2, 1, 2, 3, 3, 4, 5];

console.log(removeRepeatArr(arr));
// [ 1, 2, 3, 4, 5  ]
```

8.使用hashtable

使用for循环创建hash表

```
function removeRepeatArr(arr) \\{
    const result = [];
    const hash = \\{\\};
    for (let i = 0, len = arr.length; i < len; i++) \\{
        if (!hash[arr[i]]) \\{
            hash[arr[i]] = true;
            result.push(arr[i]);
        \\}
    \\}

    return result;
\\}

const arr = [1, 2, 1, 2, 3, 3, 4, 5];

console.log(removeRepeatArr(arr));
// [ 1, 2, 3, 4, 5 ]
```

当然也可以用forEach代替for循环

```
function removeRepeatArr(arr) \\{
    const result = [];
    const hash = \\{\\};
    arr.forEach((item) => \\{
        if (!hash[item]) \\{
            result.push(item);
            hash[item] = true;
        \\}
    \\});
    
    return result;
\\}

const arr = [1, 2, 1, 2, 3, 3, 4, 5];

console.log(removeRepeatArr(arr));
// [ 1, 2, 3, 4, 5 ]
```



**方法一：**

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

**方法二：利用splice直接在原数组进行操作**

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

**方法三：利用对象的属性不能相同的特点进行去重**

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

**方法四：数组递归去重**

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

**方法五：利用indexOf以及forEach**

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

**方法六：利用ES6的set**

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

**下面给大家补充介绍合并数组并去重的方法**

**一、concat()方法**

思路：concat() 方法将传入的数组或非数组值与原数组合并,组成一个新的数组并返回。该方法会产生一个新的数组。

```
function concatArr(arr1, arr2)\\{
  var arr = arr1.concat(arr2);
  arr = unique1(arr);//再引用上面的任意一个去重方法
  return arr;
\\}
```

**二、Array.prototype.push.apply()**

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



### sort 排序原理

冒泡排序法

解析：

冒泡排序法的原理：

- 比较相邻的元素。如果第一个比第二个大，就交换他们两个。
- 对每一对相邻元素做同样的工作，从开始第一对到结尾的最后一对。在这一点，最后的元素应该会是最大的数。
- 针对所有的元素重复以上的步骤，除了最后一个。
- 持续每次对越来越少的元素重复上面的步骤，直到没有任何一对数字需要比较。

示例：

```js
var arr = [1, 5, 4, 2];
// sort()方法的比较逻辑为：
// 第一轮：1和5比，1和4比，1和2比
// 第二轮：5和4比，5和2比
// 第三轮：4和2比
```

```js
// 一.sort排序规则 return大于0则交换数组相邻2个元素的位置
// 二.arr.sort(function (a,b) \\{\\})中
//         a -->代表每一次执行匿名函时候，找到的数组中的当前项；
//         b -->代表当前项的后一项；

// 1.升序
var apple = [45, 42, 10, 147, 7, 65, -74];
// ①默认法,缺点:只根据首位排序
console.log(apple.sort());
// ②指定排序规则法,return可返回任何值
console.log(
  apple.sort(function(a, b) \\{
    return a - b; //若return返回值大于0(即a＞b),则a,b交换位置
  \\})
);

//2.降序
var arr = [45, 42, 10, 111, 7, 65, -74];
console.log(
  apple.sort(function(a, b) \\{
    return b - a; //若return返回值大于零(即b＞a),则a,b交换位置
  \\})
);
```

原文：https://blog.csdn.net/soraru/article/details/82255616
https://www.cnblogs.com/huoxiao/p/10239284.html



### 数组方法的 32 场演唱会

> 摘抄自 @大转转 FE

来跟我一起唱 判断是不是数组，isArray最靠谱。 按照条件来判断，every/some给答案
是否包含此元素，includes最快速。 find/findIndex很相似，按条件给第一个值。
indexOf/lastIndexOf也很强，有没有来在哪忙。 from和of，都能用来生数组。
concat当红娘，数组结婚她帮忙。 filter瘦身有一套，不想要的都不要。
map整容有实力，改头换面出新意。 slice就像买切糕，想切哪来就下刀。
自力更生很重要，copyWithin自己搞。 fill就像填大坑，想往哪扔往哪扔。
搬山摸金四兄弟，pop、push、shift、unshift不难记。
造反其实很容易，reverse一下看好戏。 sort排序有技巧，能小大来能大小。
splice要认识，能插能删有本事。 forEach最熟悉，有人说它是万能滴。
keys、values、entries，遍历数组新方式。
算总账，不要慌，reduce、reduceRight帮你忙。
toString，join变字符，toLocaleString不常用。
当里个当，当里个当，数组32方法，猥琐发育不要浪，嘿！不要浪！



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



### filter对数组和对象的过滤

1，对数组的过滤

```
      let arr = ['1', '2', '3']
      let b = arr.filter(val => val === '2')
      console.log(b) // ['2]
```

2，对象的过滤

```
      let objArr = [
        \\{id: 1, label: '影视'\\},
        \\{id: 2, label: '动漫'\\},
        \\{id: 3, label: '音乐'\\}
      ]
      let c = objArr.filter(val => \\{
        return val.label === '音乐'
      \\})
      console.log(c) // \\{id: 3, label: "音乐"\\}
```



### js循环遍历数组（对象）

#### 1，for循环

对于循环应该是最常用的一种遍历方式了，通常用来遍历数组结构。

```
let arr = [a,b,d];
for (let i=0; i<arr.length; i++)\\{
	console.log(i,arr[i]);
\\}
```

#### 2，for...in循环

for...in语句用于对数组或者对象的属性进行循环操作。

for...in循环中的代码每执行一次，就会对数组或者对象的属性进行一次操作。

```
let obj=\\{'name':'programmer','age':'22','height':'180'\\};
for(let i in obj)\\{
	console.log(i,obj[i])
\\}
```

#### 3，while循环

while用于循环作用基本一致，通常用来循环数组

```
cars=["BMW","Volvo","Saab","Ford"];
var i=0;
while (cars[i])\\{
	console.log(cars[i] + "<br>")
	i++;
\\};
```

#### 4，do while循环

do while 是while的一个亲戚，它在循环开始前先执行一次操作，然后才进行判断，true就继续执行，false就结束循环。

```
let i = 3;
do\\{
	console.log(i)
	i--;
\\}
while(i>0);
```

#### 5，forEach循环

forEach方法用于调用数组的每个元素，并将元素传递给回调函数。对于空数组不会执行回调函数。

```
let arr = [1,2,3];
arr.forEach(function(i,index)\\{
	console.log(i,index)
\\})
// 1 0
// 2 1
// 3 2
```

#### 6，map方法

map返回一个新数组，数组中的元素为原始数组元素调用函数处理后的值。

```
let arr = [1,2,3];
let tt = arr.map(function(i)\\{
	console.log(i)
	return i*2;
\\})
// [2,4,6] tt
```

#### 7，for...of循环

因为是es6引入到新特性中的，借鉴c ++，java，c＃和python语言，引入for...of循环，作为遍历所有数据结构的统一方法。

```
var arr = ['a', 'b', 'c', 'd'];
for (let a of arr) \\{
	console.log(a); // a b c d
\\}
```



### js数组遍历、对象遍历、字符串遍历

#### 数组遍历

- **for** --使用变量将数组长度缓存起来，在数组较长时性能优化效果明显

```go
for(var i=0,len=arr.length;i<len;i++)\\{
	console.log("元素："+arr[i]);
\\}
```

- **forEach** --ES5语法，对数组的每个元素执行一次提供的函数，不能使用break、return

```javascript
arr.forEach(function(item,index,arr)\\{
	console.log("元素："+item+" 索引："+index+" 整个数组："+arr);
\\})
```

- **map** --ES5语法，创建一个新数组，其结果是该数组中的每个元素都调用一个提供的函数后返回的结果

```kotlin
arr.map(function(val,index)\\{
	console.log("元素："+val+" 索引："+index);
	return val*val;
\\})
```

- **for...of** --ES6语法，可以遍历Array、Set、Map、String、TypedArray、arguments等可迭代对象，可以使用break、continue

```javascript
for(let item of arr)\\{
	console.log("元素："+item);
\\}
```

#### 对象遍历

- **for...in** --以任意顺序遍历一个对象自有的、继承的、可枚举的、非Symbol的属性，对于每个不同的属性，语句都会被执行

```javascript
for(var key in obj)\\{
	console.log("属性："+key+" 值："+obj[key]);
\\}
```

- **Object.keys()** --返回一个由一个给定对象的自身可枚举**属性**组成的数组，数组中属性名的排列顺序和使用for...in循环遍历该对象时返回的顺序一致

```javascript
Object.keys(obj);
```

- **Object.values()** --返回一个给定对象自身的所有可枚举**属性值**的数组，值的顺序与使用for...in循环的顺序相同(区别在于 for-in 循环枚举原型链中的属性)

```javascript
Object.values(obj);
```

- **Object.getOwnPropertyNames()** --返回一个由指定对象的所有自身属性的属性名（包括不可枚举属性但不包括Symbol值作为名称的**属性**）组成的数组

```javascript
Object.getOwnPropertyNames(obj);
```

#### 字符串遍历

- **for...of** --ES6语法，可以遍历Array、Set、Map、String、TypedArray、arguments等可迭代对象，可以使用break、continue

```csharp
for(let char of string)\\{
	console.log("字符："+char);
\\}
```



### 把一个数组添加到另一个数组里

#### 一、使用concat方法 

```
//用concat方法
//concat()把两个或者多个数组链接在一起，但是不改变已经存在的数组
//而是返回一个链接之后的新数组
var a = [1, 2, 3];
a.concat([4, 5]);
console.log(a);
//此处输出为 [1, 2, 3]

var a = [1, 2, 3];
a = a.concat([4, 5]);
console.log(a);//此处输出为 [1, 2, 3 ,4 ,5]
```

#### 二、使用push方法

```
var arr1 = [1,2,3];
var arr2 = [4,5];
//或者 改变原数组
arr1.push(arr2)
```

#### 三、重新定义数组

```
var arr1 = [1,2,3];
var arr2 = [4,5];
var arr3 = [...arr1, ...arr2]; //此处输出为 [0, 1, 2, 3 ,4 ,5]
```



### js中的数组对象排序

#### 一、普通数组排序　　

　　js中用方法sort()为数组排序。sort()方法有一个可选参数，是用来确定元素顺序的函数。如果这个参数被省略，那么数组中的元素将按照ASCII字符顺序进行排序。如：

```
var arr = ["a", "b", "A", "B"];
arr.sort();
console.log(arr);//["A", "B", "a", "b"]
```

因为字母A、B的ASCII值分别为65、66，而a、b的值分别为97、98，所以上面输出的结果是 ["A", "B", "a", "b"] 。

　　如果数组元素是数字呢，结果会是怎样？

```
var arr = [15, 8, 25, 3];
arr.sort();
console.log(arr);//[15, 25, 3, 8]
```

结果是 [15, 25, 3, 8] 。其实，sort方法会调用每个数组项的toString()方法，得到字符串，然后再对得到的字符串进行排序。虽然数值15比3大，但在进行字符串比较时"15"则排在"3"前面。显然，这种结果不是我们想要的，这时，sort()方法的参数就起到了作用，我们把这个参数叫做比较函数。

　　比较函数接收两个参数，如果第一个参数应该位于第二个之前则返回一个负数，如果两个参数相等则返回0，如果第一个参数应该位于第二个之后则返回一个正数。例子：

```
var arr = [23, 9, 4, 78, 3];
var compare = function (x, y) \\{//比较函数
    if (x < y) \\{
        return -1;
    \\} else if (x > y) \\{
        return 1;
    \\} else \\{
        return 0;
    \\}
\\}
console.log(arr.sort(compare));        
```

结果为 [3, 4, 9, 23, 78] ，返回了我们想要的结果。如果要按降序排序，比较函数写成这样即可：

```
var compare = function (x, y) \\{
    if (x < y) \\{
        return 1;
    \\} else if (x > y) \\{
        return -1;
    \\} else \\{
        return 0;
    \\}
\\}
```

　　我们并不能用比较函数比较一个不能转化为数字的字符串与数字的顺序：

```
var arr = ["b", 5];
console.log(arr.sort(compare))
```

结果是 ["b", 5] 。因为比较函数在比较时，会把先把字符串转化为数字，然后再比较，字符串b不能转化为数字，所以就不能比较大小。然而，当不用比较函数时，会比较ASCII值，所以结果是 [5, "b"] 。

#### 二、数组对象排序

　　如果数组项是对象，我们需要根据数组项的某个属性对数组进行排序，要怎么办呢？其实和前面的比较函数也差不多：

```
var arr = [\\{name: "zlw", age: 24\\}, \\{name: "wlz", age: 25\\}];
var compare = function (obj1, obj2) \\{
    var val1 = obj1.name;
    var val2 = obj2.name;
    if (val1 < val2) \\{
        return -1;
    \\} else if (val1 > val2) \\{
        return 1;
    \\} else \\{
        return 0;
    \\}            
\\} 
console.log(arr.sort(compare));
```

　　输出结果为 [Object \\{ name="wlz", age=25\\}, Object \\{ name="zlw", age=24\\}] ，可以看到数组已经按照 name 属性进行了排序。我们可以对上面的比较函数再改造一下：

```
var compare = function (prop) \\{
    return function (obj1, obj2) \\{
        var val1 = obj1[prop];
        var val2 = obj2[prop];
        if (val1 < val2) \\{
            return -1;
        \\} else if (val1 > val2) \\{
            return 1;
        \\} else \\{
            return 0;
        \\}            
    \\} 
\\}
```

如果想按照 age 进行排序， arr.sort(compare("age")) 即可。

　　但是对age属性进行排序时需要注意了，如果age属性的值是数字，那么排序结果会是我们想要的。但很多时候我们从服务器传回来的数据中，属性值通常是字符串。现在我把上面的数组改为：

```
var arr = [\\{name: "zlw", age: "24"\\}, \\{name: "wlz", age: "5"\\}];
```

可以看到，我把 age 属性由数字改为了字符串，第二个数组项的 age 值改为了 "5" 。再次调用 arr.sort(compare("age")) 后，结果为：

```
[Object \\{ name="zlw", age="24"\\}, Object \\{ name="wlz", age="5"\\}]
```

我们的期望是5排在25前面，但是结果不是。这是因为当两个数字字符串比较大小时，**会比较它们的ASCII值大小**

比较规则是：从第一个字符开始，顺次向后直到出现不同的字符为止，然后以第一个不同的字符的ASCII值确定大小。所以"24"与"5"比较大小时，先比较”2“与"5"的ASCII值，显然”2“的ASCII值比"5"小，即确定排序顺序。

　　现在，我们需要对比较函数再做一些修改：

```
var compare = function (prop) \\{
    return function (obj1, obj2) \\{
        var val1 = obj1[prop];
        var val2 = obj2[prop];
        if (!isNaN(Number(val1)) && !isNaN(Number(val2))) \\{
            val1 = Number(val1);
            val2 = Number(val2);
        \\}
        if (val1 < val2) \\{
            return -1;
        \\} else if (val1 > val2) \\{
            return 1;
        \\} else \\{
            return 0;
        \\}            
    \\} 
\\}
```

在比较函数中，先把比较属性值转化为数字 Number(val1) 再通过 !isNaN(Number(val1)) 判断转化后的值是不是数字(有可能是NaN)，转化后的值如果是数字，则比较转换后的值，这样就可以得到我们想要的结果了， 调用 arr.sort(compare("age")) 得到：

```
[Object \\{ name="wlz", age="5"\\}, Object \\{ name="zlw", age="24"\\}]
```

可以看到，确实是按正确的方式排序了。

但是在火狐浏览器有问题，比较数字用下面代码没问题啦



### 根据对象数组中的数字来排序

```
compare(key)\\{
	return function(value1,value2)\\{
		var val1=value1[key];
		var val2=value2[key];
		return val2-val1;//从大到小排序
	\\}
\\}
arr.sort(compare("count"));
```

```
//数组对象按count从大到小排序
    listNew.sort((a, b) => \\{
      if (a.count < b.count) \\{
        return 1;
      \\} else if (a.count > b.count) \\{
        return -1;
      \\} else \\{
        return 0;
      \\}
    \\});
```



### 根据对象数组中的时间来排序

第一种也可以比较字符串

```
compare(prop) \\{
				//数组对象排序
				return function (obj1, obj2) \\{
					var val1 = obj1[prop];
					var val2 = obj2[prop];
					if (val1 > val2) \\{
						return -1;
					\\} else if (val1 < val2) \\{
						return 1;
					\\} else \\{
						return 0;
					\\}
				\\}
			\\},
arr.sort(compare("time"));
```

另一种只比较时间

```
sortKey(array, key) \\{
	return array.sort(function(a, b) \\{
		var x = a[key];
		var y = b[key];
			return x > y ? -1 : x < y ? 1 : 0;
		\\});
\\}
arr=sortKey(arr,"time");//传入数组、时间字段
```

```
list.sort(function(a, b) \\{
	return b.createTime < a.createTime ? -1 : 1
\\})
```



### 数组对象某元素求和

类似于这种格式数据求和var array=[\\{'id':80,'price':50.,\\{'id':20,'price':30\\}]

```
var total=array.reduce((total, item) => total+item.count,0);
```

```
var arry = [\\{'id': 80, 'price': 50\\}, \\{'id': 20, 'price': 30\\}, \\{'id': 20, 'price': 300\\}];
var strarr = [];
for (let i in arry) \\{
    strarr.push(arry[i]['price'])
\\};
console.log(eval(strarr.join('+'))) //结果
```



## 判断是否是一个数组

在 JavaScript 中，判断一个变量是否为数组有多种方法。以下是**最可靠和推荐**的解决方案：

### 1. 使用 `Array.isArray()`（ES5+ 标准方法，首选）

```
const arr = [1, 2, 3];
console.log(Array.isArray(arr)); // true

const notArr = \\{ key: 'value' \\};
console.log(Array.isArray(notArr)); // false
```

### 2. 兼容旧环境的替代方案（如 IE8-）

```
// 通过 Object.prototype.toString 判断
function isArray(obj) \\{
  return Object.prototype.toString.call(obj) === '[object Array]';
\\}

const arr = [];
console.log(isArray(arr)); // true
```

### ❌ 不推荐的方法（存在缺陷）

[].constructor

使用 instanceof 操作符。

```
// 方法 1：typeof 无法识别数组（返回 'object'）
console.log(typeof []); // "object" （不适用）

// 方法 2：instanceof 在跨 frame 时会失效
const iframe = document.createElement('iframe');
document.body.appendChild(iframe);
const frameArray = window.frames[0].Array;
const frameArr = new frameArray();
console.log(frameArr instanceof Array); // false （跨 frame 不可靠）
```

------

### 总结

| **方法**                    | 可靠性   | 跨执行环境 | 支持版本 |
| --------------------------- | -------- | ---------- | -------- |
| `Array.isArray()`           | ✅ 可靠   | ✅ 安全     | ES5+     |
| `Object.prototype.toString` | ✅ 可靠   | ✅ 安全     | 全兼容   |
| `instanceof Array`          | ⚠️ 有条件 | ❌ 失效     | 所有版本 |
| `typeof`                    | ❌ 无效   | -          | 所有版本 |

**强烈建议始终使用 `Array.isArray()`**，这是现代 JavaScript 的标准做法。



### JS判断是否是数组的四种做法

判断对象是否是数组的几种方式

#### 1.通过instanceof判断

instanceof运算符用于检验构造函数的prototype属性是否出现在对象的原型链中的任何位置，返回一个布尔值。

```
let a = [];
a instanceof Array; //true
let b = \\{\\};
b instanceof Array; //false
```

在上方代码中，instanceof运算符检测Array.prototype属性是否存在于变量a的原型链上，显然a是一个数组，拥有Array.prototype属性，所以为true。

**存在问题：**

需要注意的是，prototype属性是可以修改的，所以并不是最初判断为true就一定永远为真。

其次，当我们的脚本拥有多个全局环境，例如html中拥有多个iframe对象，instanceof的验证结果可能不会符合预期，例如：

```
//为body创建并添加一个iframe对象
var iframe = document.createElement('iframe');
document.body.appendChild(iframe);
//取得iframe对象的构造数组方法
xArray = window.frames[0].Array;
//通过构造函数获取一个实例
var arr = new xArray(1,2,3); 
arr instanceof Array;//false
```

导致这种问题是因为iframe会产生新的全局环境，它也会拥有自己的Array.prototype属性，让不同环境下的属性相同很明显是不安全的做法，所以Array.prototype !== window.frames[0].Array.prototype，想要arr instanceof Array为true，你得保证arr是由原始Array构造函数创建时才可行。

#### 2.通过constructor判断

我们知道，实例的构造函数属性constructor指向构造函数，那么通过constructor属性也可以判断是否为一个数组。

```
let a = [1,3,4];
a.constructor === Array;//true
```

同样，这种判断也会存在多个全局环境的问题，导致的问题与instanceof相同。

```
//为body创建并添加一个iframe标签
var iframe = document.createElement('iframe');
document.body.appendChild(iframe);
//取得iframe对象的构造数组方法
xArray = window.frames[window.frames.length-1].Array;
//通过构造函数获取一个实例
var arr = new xArray(1,2,3); 
arr.constructor === Array;//false
```

#### 3.通过Object.prototype.toString.call()判断

 Object.prototype.toString().call()可以获取到对象的不同类型，例如

```
let a = [1,2,3]
Object.prototype.toString.call(a) === '[object Array]';//true
```

它强大的地方在于不仅仅可以检验是否为数组，比如是否是一个函数，是否是数字等等

```
//检验是否是函数
let a = function () \\{\\};
Object.prototype.toString.call(a) === '[object Function]';//true
//检验是否是数字
let b = 1;
Object.prototype.toString.call(a) === '[object Number]';//true
```

甚至对于多全局环境时， Object.prototype.toString().call()也能符合预期处理判断。

```
//为body创建并添加一个iframe标签
var iframe = document.createElement('iframe');
document.body.appendChild(iframe);
//取得iframe对象的构造数组方法
xArray = window.frames[window.frames.length-1].Array;
//通过构造函数获取一个实例
var arr = new xArray(1,2,3); 
console.log(Object.prototype.toString.call(arr) === '[object Array]');//true
```

#### 4.通过Array.isArray()判断

Array.isArray() 用于确定传递的值是否是一个数组，返回一个布尔值。

```
let a = [1,2,3]
Array.isArray(a);//true
```

简单好用，而且对于多全局环境，Array.isArray() 同样能准确判断，但有个问题，Array.isArray() 是在ES5中提出，也就是说在ES5之前可能会存在不支持此方法的情况。怎么解决呢？

#### 判断数组方法的最终推荐

 当然还是用**Array.isArray()**，从ES5新增isArray()方法正是为了提供一个稳定可用的数组判断方法，不可能专门为此提出的好东西不用，而对于ES5之前不支持此方法的问题，我们其实可以做好兼容进行自行封装，像这样：

```
if (!Array.isArray) \\{
  Array.isArray = function(arg) \\{
    return Object.prototype.toString.call(arg) === '[object Array]';
  \\};
\\}
```



### JS中的Map对象

1.js创建map对象

```
var map = new Map();
```

2.将键值对放入map对象

```
map.set("key",value)
map.set("key1",value1)
map.set("key2",value2)
```

3.根据key获取map值

```
map.get(key)
```

4.删除map指定对象

```
delete map[key]
或
map.delete(key)
```

5.循环遍历map

```
map.forEach(function(key)\\{
　　console.log("key",key) //输出的是map中的value值
\\})
```



### map()方法遍历数组

这里的map不是地图的意思，而是“映射”。

map的使用方法和forEach类似。

和forEach不同的是，map有返回值。

在工作中如果需要**根据条件重组数组**，用map会很方便。

map() 方法返回一个新数组，数组中的元素为原始数组元素**调用函数处理后的值**。

map() 方法**按照原始数组元素顺序依次处理**元素。

**注意：** 

map() 不会对空数组进行检测。

map() 不会改变原始数组。

详细写法

```php
array.map(function(currentValue,index,arr),thisValue)
```

- **currentValue：**【必填】数组中正在处理的当前元素。
- **index：**【可选】数组中正在处理的当前元素的索引。
- **arr：**【可选】方法被调用的数组。也就是当前元素属于的数组对象。
- **thisValue：**【可选】执行回调函数时使用的this值。

`map` 方法会给原数组中的每个元素都按顺序调用一次  `callback` 函数。`callback` 每次执行后的返回值（包括 `undefined`）组合起来形成一个新数组。 `callback` 函数只会在有值的索引上被调用；那些从来没被赋过值或者使用 `delete` 删除的索引则不会被调用。

`callback` 函数会被自动传入三个参数：**数组元素，元素索引，原数组本身**。

如果 `thisArg` 参数有值，则每次 `callback` 函数被调用的时候，`this` 都会指向 `thisArg` 参数上的这个对象。如果省略了 `thisArg ``参数,``或者赋值为 null` 或 `undefined`，则 this 指向全局对象 。

`map`不修改调用它的原数组本身（当然可以在 `callback` 执行时改变原数组）。

使用 map 方法处理数组时，数组元素的范围是在 callback 方法第一次调用之前就已经确定了。在 map 方法执行的过程中：原数组中新增加的元素将不会被 callback 访问到；若已经存在的元素被改变或删除了，则它们的传递到 callback 的值是 map 方法遍历到它们的那一时刻的值；而被删除的元素将不会被访问到。



map() 方法创建一个新数组，其结果是该数组中的每个元素都调用一个提供的函数后返回的结果。

并举了个例子：

```
var array1 = [1,4,9,16];
const map1 = array1.map(x => x *2);
console.log(map1);
```

打印结果为：

> Array [2,8,18,32]
> 而我这样写时：

```
var array1 = [1, 4, 9, 16];

const map1 = array1.map(x => \\{
    if (x == 4) \\{
        return x * 2;
    \\}
\\});

console.log(map1);
```

打印结果为：

> Array [undefined, 8, undefined, undefined]
> 为什么会出现三个undefined呢？而不是我预期的[1,8,9,16]。

这样写只是增加了一个条件，即x的值为4时才乘以2，之所以会出现undefined，是因为map()方法创建了一个新数组，但新数组并不是在遍历完array1后才被赋值的，而是每遍历一次就得到一个值。所以，下面这样修改后就正确了：

```
var array1 = [1, 4, 9, 16];

const map1 = array1.map(x => \\{
    if (x == 4) \\{
        return x * 2;
    \\}
    return x;
\\});
```

这里注意箭头函数有两种格式：
1.只包含一个表达式，这时花括号和return都省略了。
2.包含多条语句，这时花括号和return都不能省略。



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







# map、forEach、filter和reduce方法比较

在JS算法和Web前端开发中，map、forEach、filter是比较常用的对数组进行操作的方法，reduce则是比较少见的高阶函数。但由于它们语法相似，初学者在学习过程中经常会混淆这四者，对其概念和用法比较模糊。在总结过去学习成果时，我也顺便对这四个函数进行比较全面的对比分析。

**语法**

```javascript
//map方法
array.map(function(currentValue,index,arr), thisValue)

//forEach方法
array.forEach(function(currentValue, index, arr), thisValue)

//filter方法
array.filter(function(currentValue,index,arr), thisValue)

//reduce方法
array.reduce(function(total, Value, index, arr), initialValue)
```

| 必须参数     | 描述                             | 可选参数     | 描述                                                         |
| ------------ | -------------------------------- | ------------ | ------------------------------------------------------------ |
| currentValue | 当前元素的值                     | thisValue    | 对象作为该执行回调时使用，传递给函数，用作 "this" 的值。 如果省略了 thisValue ，"this" 的值为 "undefined" |
| index        | 当前元素的索引值                 | initialValue | 传递给函数的初始值（total）                                  |
| arr          | 当前元素属于的数组对象           |              |                                                              |
| total        | 初始值, 或者计算结束后的返回值。 |              |                                                              |

#### map

```js
// map
//作用：对数组进行遍历
//返回值：新的数组
//是否改变：否
var arr = [2, 5, 3, 4];
var ret = arr.map(function(value) \\{
  return value + 1;
\\});
console.log(ret); //[3,6,4,5]
console.log(arr); //[2,5,3,4]
```

#### forEach

```js
// forEach 方法
// 作用：遍历数组的每一项
// 返回值：undefined
// 是否改变：否
var arr = [2, 5, 3, 4];
var ret = arr.forEach(function(value) \\{
  console.log(value); // 2, 5, 3, 4
\\});
console.log(ret); //undefined
console.log(arr); //[2,5,3,4]
```

#### filter

```js
// filter 过滤
// 作用： 筛选一部分元素
// 返回值： 一个满足筛选条件的新数组
// 是否改变原有数组：不会

var arr = [2, 5, 3, 4];
var ret = arr.filter(function(value) \\{
  return value > 3;
\\});
console.log(ret); //[5,4]
console.log(arr); //[2,5,3,4]
```

#### reduce

```js
// reduce 方法
// 作用：对数组进行迭代，然后两两进行操作，最后返回一个值
// 返回值：return出来的结果
// 是否改变：不会
var arr = [1, 2, 3, 4];
var ret = arr.reduce(function(a, b) \\{
  return a * b;
\\});
console.log(ret); // 24
console.log(arr); // [1, 2, 3, 4]
```



## 1、map函数

### 1-1、定义和用法

map() 方法返回一个新数组，数组中的元素为原始数组元素调用函数处理后的值。 map() 方法按照原始数组元素顺序依次处理元素。

### 1-2、方法特性

 是否对空数组进行检测：否

### 1-3、用例

#### 1-3-1、构造数组

```js
[...Array(10000).keys()].map((v, i) => i + 1);
```

#### 1-3-2、数组元素值翻倍

```js
const double = numbers.map(function (num) \\{
    return num * 2;
\\})
```

#### 1-3-3、获取列表里的object信息

```js
const msg = error.details.map(el => el.message).join(',')
```

#### 1-3-4、构造对象数组

```js
newCamp.images = req.files.map(f => (\\{ url: f.path, filename: f.filename \\}))
```

## 2、forEach函数

### 2-1、定义和用法

 forEach() 方法用于调用数组的每个元素，并将元素传递给回调函数。 

### 2-2、方法特性

 是否对空数组进行检测：否

### 2-3、用例

#### 2-3-1、遍历输出

```js
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20];

function print(element) \\{
    console.log(element);
\\}
numbers.forEach(print)
```

#### 2-3-2、计算数组所有元素相加的总和

```js
<button onclick="numbers.forEach(myFunction)">点我</button>
<p>数组元素总和：<span id="demo"></span></p> 
<script> 
var sum = 0; 
var numbers = [65, 44, 12, 4]; 
function myFunction(item) \\{ 
    sum += item; 
    demo.innerHTML = sum; 
\\} 
</script>
```

## 3、filter函数

### 3-1、定义和用法

 filter() 方法创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素。 

### 3-2、方法特性

 是否对空数组进行检测：否

### 3-3、用例

#### 3-3-1、筛选数组

```js
var ages = [32, 33, 16, 40];
function checkAdult(age) \\{
    return age >= 18;
\\}
document.getElementById("demo").innerHTML = ages.filter(checkAdult);\\}
```

#### 3-3-2、筛选数组（反向筛选）

```js
comments = comments.filter(c => c.id != id);
```

#### 3-3-3、filter与map方法结合的链式操作

```js
const movies = [
    \\{
        title: 'Amadeus',
        score: 99
    \\},
    \\{
        title: 'Stand By Me',
        score: 85
    \\},
    \\{
        title: 'Parasite',
        score: 95
    \\},
    \\{
        title: 'Alien',
        score: 90
    \\}
]
const goodMovies = movies.filter(m => m.score > 80)
const goodTitles = goodMovies.map(m => m.title)

movies.filter(m => m.score > 80).map(m => m.title);
```

## 4、reduce函数

### 4-1、定义和用法

 reduce() 方法接收一个函数作为累加器，数组中的每个值（从左到右）开始缩减，最终计算为一个值。 reduce() 可以作为一个高阶函数，用于函数的 compose。 

### 4-2、方法特性

 reduce() 是数组的归并方法，与forEach()、map()、filter()等迭代方法一样都会对数组每一项进行遍历，但是reduce() 可同时将前面数组项遍历产生的结果与当前遍历项进行运算，这一点是其他迭代方法无法企及的 

是否对空数组进行检测：否
 是否能改变原始数组：否
 是否返回数据：是
 返回数组长度能否改变：是

### 4-3、用例

#### 4-3-1、数组元素累加

```js
const prices = [9.99, 1.50, 19.99, 49.99, 30.50];
const total = prices.reduce((total, price) => \\{
    return total + price
\\})
```

#### 4-3-2、条件筛选

```js
const prices = [9.99, 1.50, 19.99, 49.99, 30.50];
const minPrice = prices.reduce((min, price) => \\{
    if (price < min) \\{
        return price;
    \\}
    return min;
\\})
```

#### 4-3-3、求数组项最大值

```js
var arr = [3,9,4,3,6,0,9];
var max = arr.reduce(function (prev, cur) \\{
    return Math.max(prev,cur);
\\});
```

#### 4-3-4、扁平一个二维数组

```js
var arr = [[1, 2, 8], [3, 4, 9], [5, 6, 10]];
var res = arr.reduce((x, y) => x.concat(y), []);
```

## 5、参考资料

[reduce() 方法](https://link.juejin.cn?target=https\\%3A\\%2F\\%2Fwww.runoob.com\\%2Fjsref\\%2Fjsref-reduce.html)

[filter() 方法](https://link.juejin.cn?target=https\\%3A\\%2F\\%2Fwww.runoob.com\\%2Fjsref\\%2Fjsref-filter.html)

[forEach() 方法](https://link.juejin.cn?target=https\\%3A\\%2F\\%2Fm.runoob.com\\%2Fjsref\\%2Fjsref-foreach.html)

[map() 方法](https://link.juejin.cn?target=https\\%3A\\%2F\\%2Fwww.runoob.com\\%2Fjsref\\%2Fjsref-map.html)

[颠覆者——JS中reduce() 的用法](https://link.juejin.cn?target=https\\%3A\\%2F\\%2Fwww.cnblogs.com\\%2Famujoe\\%2Fp\\%2F11376940.html)


原文链接：https://juejin.cn/post/7082271376307912711

