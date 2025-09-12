---
title: 原生常见问题
date: 2022-05-20 19:45:42
categories: 
- 前端问题
tags:
- JavaScript
- Css
- 前端
---

### JavaScript文件位置

在本网站（HTML5学堂）正式上线之前，统计工具针对本网站的SEO优化提出了一些建议，说是将JS文件放置在body标签之后会提升加载速度。不过最终我们还是放置在了head标签里。这里就涉及到一个JS文件位置的选择。到底JS文件的引入放置在头部好还是尾部好？一起来看看吧。

具体将引入的JS放在哪里与代码执行的顺序有关。网页文件的读取是从上到下的，如果将JavaScript文件放置在head当中，会先加载JS文件，之后再继续执行，那么此时，如果JS文件比较大，页面加载就会比较慢，导致空白。

那么，如果将JavaScript文件放置在底部，如果说，也是比较大型的JS文件的话，是不是就没有问题了呢？

其实，如果将JS文件放置在底部的话，可以让JS文件与图片几乎同时下载，使得页面当中的内容能够尽快的下载下来，但是，由于网页基本结构与样式均已经加载完成，那么此时负责交互的JS并没有下载下来，必然也会对用户的体验造成影响。

因此，整体来说，如果“交互性优先”，那么我们应当将JS放置在顶部。如果对于交互性要求没那么高的页面，我们将JS放置在底部。

**阻塞方式加载JS**

阻塞方式加载JS：JavaScript在头部会阻止其他元素并行加载(css,图片,网页)。目前绝大部分的浏览器都是采取阻塞方式(Scripts Block Downloads)进行JavaScript文件的加载的。

首先在HTML文件中js脚本是按顺序加载的。

假设你的js脚本是给页面上某个元素绑定了事件，如果你将js脚本放在尾部就会造成页面出来了，但是js脚本没加载出来的这段时间里对绑定事件了的元素进行操作是没有效果的。所以这种情况就适合放在头部。 

但是针对那些不是需要及时的交互js脚本可以选在这</body>之前即可。

此外比较中肯的意见是：将js脚本放在头部，但是需要采用一些方法来进行优化。比如采用JSLoader。

总结日期：2019.11.18



### jQuery版本区别

1.x	兼容ie678，使用最为广泛的，官方只做bug维护，功能不再新增。因此一般项目来说，使用1.x版本就可以了，最终版本：1.12.4

2.x	不兼容ie678，很少人使用，官方只做bug维护，功能不再新增。如果不考虑兼容版本低的浏览器可以使用2.x，最终版本：2.2.4

3.x	不兼容ie678，只支持最新的浏览器。除非特殊要求，一般不会使用3.x版本的，很多老的jQuery插件不支持这个版本。目前该版本是官方主要更新维护的版本。截至2018年6月13日，最新版本：3.3.1

**电脑端 推荐选择 jQuery 1.9 版本**，理由如下：

兼容IE8，在当下电脑端兼容IE8还是有需要的（管理系统除外）。

API与更高版本基本一致，又将低版本的不足之处进行了修复，比如：选择器的性能、方法名的不规范等等

在1.9版本中有jQuery1.7中引进的事件处理函数界的一哥 “.on()” 函数。

移动端 推荐选择 jQuery 3.x 版本，理由如下：

新的肯定更好啊，不好还需要更新吗？这里不需要理由。

不推荐使用的 jQuery 版本：

低于 jQuery 1.7 的版本：

1、与现在的高版本API相差比较大；

2、选择器等各方面性能不高。

2.x 版本：

1、存在的周期短（2.0.0版本开始 至 2.2.4结束）；

2、不如1.9版本能兼容IE8；

3、现如今 3.x也早以发布再使用 2.x 版本意义 不大。

知名网站选择jQuery1.9 ~ 1.11版本中的站点有：CSDN1.9.1，腾讯课堂，幕课网，百度1.10.2

**1.x 常用版本**

1.4.2：稳定性和兼容性都很出色，插件最多，但性能不如下面后面的几个版本。

1.7.2：性能提升，插件第二多，ajax和 attr 等 api有少许修改。

1.8.3：最后一个支持 IE6 的稳定版

1.9.1：开始移除了不少方法，事件绑定推荐使用on方法一个代替所有的

1.12.4：1.x 时代最后一个稳定版本，仅支持 IE8，不支持 IE6/7。

**3，2.x、3.x 版本**

除非有特殊要求（比如面向移动端），一般情况下这两大版本使用人的确很少：

2.x 最后一个稳定版本：2.2.4

3.x 最新版本：3.3.1

总结日期：2019.11.18



### js生成新标签不触发click事件

当我们使用js新创建了一个新标签时，点击事件并不会触发
例如：button 是我们生成的新标签

```
<button id="btn" type="button" >新生成的button</button>
```

平常根据id绑定点击事件，此方法在原来的标签中可以触发click事件，在新生成的标签中不触发click事件

```
$("#btn").click(function()\\{
	alert(1)
\\})
```

解决方案
方法一：使用on(“click”,function\\{\\})绑定点击事件

```
$("body").on("click","#btn",function()\\{
	alert(1)
\\})
```

方法二: 创建新标签的同时，添加一个onClick事件

```
//新生成的button标签
<button id="btn" type="button" onClick="btnClick()" >新生成的button</button>

//函数
function btnClick()\\{
	alert(1)
\\}
```

总结:当我们使用js生成未来标签时，未来标签不能直接使用click绑定事件，应该使用on(“click”,function\\{\\})函数绑定，或者在新生成未来标签的同时添加一个onClick函数

总结日期：2019.11.19



### jQuery on() 方法

向 <p> 元素添加 click 事件处理程序：

$(document).ready(function()\\{  $("p").on("click",function()\\{    alert("段落被点击了。");  \\}); \\});

**定义和用法**

on() 方法在被选元素及子元素上添加一个或多个事件处理程序。

自 jQuery 版本 1.7 起，on() 方法是 bind()、live() 和 delegate() 方法的新的替代品。该方法给 API 带来很多便利，我们推荐使用该方法，它简化了 jQuery 代码库。

**注意：**使用 on() 方法添加的事件处理程序适用于当前及未来的元素（比如由脚本创建的新元素）。

**提示：**如需移除事件处理程序，请使用 [off()](https://www.runoob.com/jquery/event-off.html) 方法。

**提示：**如需添加只运行一次的事件然后移除，请使用 [one()](https://www.runoob.com/jquery/event-one.html) 方法。

**语法：**$(*selector*).on(*event,childSelector,data,function*)

| 参数            | 描述                                                         |
| :-------------- | :----------------------------------------------------------- |
| *event*         | 必需。规定要从被选元素移除的一个或多个事件或命名空间。  由空格分隔多个事件值，也可以是数组。必须是有效的事件。 |
| *childSelector* | 可选。规定只能添加到指定的子元素上的事件处理程序（且不是选择器本身，比如已废弃的 delegate() 方法）。 |
| *data*          | 可选。规定传递到函数的额外数据。                             |
| *function*      | 可选。规定当事件发生时运行的函数。                           |

总结日期：2019.11.19



### html拼接及模板字符串引用变量

```
 let str=``
 str += `<div>内容</tr>`
```

```
var obj = \\{name:"秦伟",age:"23"\\};
var str = `$\\{obj.name\\}很厉害，才$\\{obj.age\\}岁`;
alert(str);
```

总结日期：2019.11.20



### 嵌套对象遍历

```
<script>
    <!--js处理多层嵌套的Object对象数据-->
    var studentData = \\{
        "1": \\{
            "id": 11503080201,
            "name": "张三",
            "college": "计算机科学与工程学院",
            "profession": "软件工程",
            "grade": 2015,
            "classes": 2,
            "age": 21,
            "schedule": [\\{
                "id": "147",
                "cid": "1",
                "uid": "70",
                "classsid": "62",
                "name": "\u82f1\u8bed\u8bfe\u7a0b",
                "addtime": "1550565334",
                "updatetime": "1568085126",
                "week": "\u5468\u56db",
                "index": "1",
                "ctid": "1"
            \\}, \\{
                "id": "154",
                "cid": "1",
                "uid": "70",
                "classsid": "14",
                "name": "\u8bed\u8a00\u6559\u80b2",
                "addtime": "1550565334",
                "updatetime": "1568085261",
                "week": "\u5468\u56db",
                "index": "3",
                "ctid": "1"
            \\}]
        \\},
        "2": \\{
            "id": 11503080201,
            "name": "李四",
            "college": "计算机科学与工程学院",
            "profession": "软件工程",
            "grade": 2015,
            "classes": 2,
            "age": 21,
            "schedule": [\\{
                "id": "147",
                "cid": "1",
                "uid": "70",
                "classsid": "62",
                "name": "\u82f1\u8bed\u8bfe\u7a0b",
                "addtime": "1550565334",
                "updatetime": "1568085126",
                "week": "\u5468\u56db",
                "index": "1",
                "ctid": "1"
            \\}, \\{
                "id": "154",
                "cid": "1",
                "uid": "70",
                "classsid": "14",
                "name": "\u8bed\u8a00\u6559\u80b2",
                "addtime": "1550565334",
                "updatetime": "1568085261",
                "week": "\u5468\u56db",
                "index": "3",
                "ctid": "1"
            \\}]
        \\}
    \\}
    //字符串需要加引号，获取单个属性的值很简单
    document.write(studentData[2].name);

    // for (let date in studentData)\\{
    //     console.log(date);
    // \\}

    //遍历有三种方法可以实现
    //     for in循环遍历当前的对象的内容是一种很常见的手段。其可以遍历对象中的所有的可枚举属性，包括当前对象的自有属性和继承属性。
    // Object.key()方法，枚举属性名称的函数，他返回的是一个数组，其中存在的是对象中的可枚举属性名称组成。
    // Object.getOwnPropertyNames()方法，其返回的也是数组，但是是所有的自有属性名称的数组。
    // 我们一般使用最常用的for in实现遍历，相对也比较简单
    // 使用for in 遍历对象时，通过判断下标k的值来确定遍历数量是，发现k是string类型，在进行数值判断是最好用parseInt()转换一下，不然容易出现不可预料的错误
    for (var k in studentData) \\{
        let schedule = studentData[k].schedule;
        console.log(schedule);
        console.log(schedule[0]);
        console.log(schedule[0].week);
        console.log(schedule[0]["week"]);
        // console.log(studentData[k].schedule.length);

        //返回一个满足你过滤条件的新数组
        // let newArr= schedule.filter((item,index,arr) =>\\{
        //     return item.id =147;
        // \\});
        // console.log(newArr);
        //newArr就是你想要的结果

//         function kcb() \\{
//             for (let i = 0; i < studentData[k].schedule.length; i++) \\{
//                 let arr = studentData[k].schedule[i]["id"];
//                 console.log(arr);
//                 let classes=[];
//                 classes.push(arr);
//                 console.log(classes);
//                 return classes;
//             \\}
//        \\}
        // kcb();
        document.write("<br>" + k + ":" + studentData[k].id + "," +
            studentData[k].name + "," +
            studentData[k].college + "," +
            studentData[k].profession + "," +
            studentData[k].grade + "," +
            studentData[k].classes + "," +
            studentData[k].age + "," +
            studentData[k].schedule[0]["id"]+
            "<br>");
    \\}
</script>
```

```
JS里面对象的多个属性是无序的，数组才是有序的，对象只能通过键来取值。
Object.keys( object)  //Object.keys返回js对象或者数组的索引
var obj = \\{'a': 'Beijing', 'b': 'Haidian'\\};
console.log(Object.keys(obj));  //['a', 'b']
console.log(Object.keys(obj).length-1);  //获取最后一个对象的序号
```

```
var obj=\\{"08":"me","09":"th","15":"ing","06":"so"\\};
console.log(obj[Object.keys(obj).sort((a, b) => a - b)[0]]);//结果为so
    /* Object.keys(obj): 输出 obj 里所有 key 组成的数组；
    /* .sort((a,b)=>a-b): 从小到大排序
    /* [0]: 输出第一个的值。
    // 以上操作找出 obj 中最小的 key 的值 (s)
    /* obj[s]: 取第一个 */
```

总结日期：2019.11.20



### JS函数常用写法

JavaScript 使用关键字 function 定义函数。函数可以通过声明定义，也可以是一个表达式。

记录下来以作参考。

函数声明：function functionName(parameters) \\{ 执行的代码 \\}

函数表达式：var x = function (a, b) \\{return a * b\\};

1、常规写法

```
function run (参数) \\{
    alert('常规写法');//这里是你函数的内容
\\}
// 调用
run();
```


2、匿名函数写法（可以想成给变量赋值一个函数）

```
var run = function()\\{
   alert('这是一种声明函数的方式，左边是一个变量，右边是一个函数的表达式');
\\}
// 调用  
run();
```


3、将方法作为一个对象

```
var Test = \\{
    run:function()\\{
      alert('这个必须放在一个对象内部，放在外边会出错！');//这里是你函数的内容
    \\}
\\}
//调用
Test.run();//调用第1个函数
```

4、构造函数中给对象添加方法

```
Function.prototype.way = function()\\{
    alert('这是在函数上的原始对象上加了一个way方法，构造函数中用到');
\\}
// 调用
Function.way();//调用对象属性
```

总结日期：2019.11.20



### JS中三种主要的遍历对象的方法

for in、Object.keys、Object.getOwnProperty

一、对非Array对象类型的遍历

1、for in

主要用于遍历对象的可枚举属性，包括自有属性、继承自原型的属性

```
var obj = \\{"name":"tom","sex":"male"\\}；
Object.defineProperty(obj, "age", \\{value:"18", enumerable:false\\});//增加不可枚举的属性age
Object.prototype.protoPer1 = function()\\{console.log("name is tom");\\};//通过原型链增加属性，为一个函数
Object.prototype.protoPer2 = 2;////通过原型链增加属性，为一个整型值2
console.log("For In : ");
for(var a in obj)
console.log(a);
```

总结：for in 主要用于遍历对象的可枚举属性，包括自有属性、继承自原型的属性，示例中的属性age为不可可枚举，所以没有输出。

2、Object.keys

此方法返回一个数组，元素均为对象自有可枚举的属性

```
var obj = \\{"name":"tom","sex":"male"\\}；
Object.defineProperty(obj, "age", \\{value:"18", enumerable:false\\});//增加不可枚举的属性age
Object.prototype.protoPer1 = function()\\{console.log("name is tom");\\};//通过原型链增加属性，为一个函数
Object.prototype.protoPer2 = 2;////通过原型链增加属性，为一个整型值2
console.log("Object.keys:")
console.log(Object.keys(obj));
```

总结：Object.keys主要用于遍历对象自有的可枚举属性，不包括继承自原型的属性和不可枚举的属性。

3、Object.getOwnProperty

此方法用于返回对象的自有属性，包括可枚举和不可枚举的属性

```
Object.defineProperty(obj, "age", \\{value:"18", enumerable:false\\});//增加不可枚举的属性age
Object.prototype.protoPer1 = function()\\{console.log("name is tom");\\};//通过原型链增加属性，为一个函数
Object.prototype.protoPer2 = 2;////通过原型链增加属性，为一个整型值2
console.log("Object.getOwnPropertyNames: ");
console.log(Object.getOwnPropertyNames(obj));
```

总结：Object.getOwnProperty主要用于返回对象的自有属性，包括可枚举和不可枚举的属性，不包括继承自原型的属性。

二、对Array对象类型的遍历

1、for in

```
var arr = [1,2,3,4,5,6];
for(var a in arr) console.log(a);
```

总结：输出为数组对象的index 值。

2、Object.keys

```
var arr = [1,2,3,4,5,6];
console.log(Object.keys(arr));
```

总结：输出为数组对象的index 值。

3、Object.getOwnProperty

```
var arr = [1,2,3,4,5,6];
console.log(Object.getOwnPropertyNames(arr));
```

总结日期：2019.11.20



### js获取元素索引值

```
<!--以ul下的li元素为例；获取li的索引，代码如下：-->
<ul id="list">
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
</ul>

<script>
    // 方法1：(自执行匿名函数法)
    var ul = document.getElementById("list");
    var list = ul.getElementsByTagName('li');
    for (var i = 0; i < list.length; i++) \\{
        !function (j) \\{	// 匿名函数表达式1(j为该匿名函数形参)
            // console.log(j); //0,1,2,3
            list[j].onclick = function () \\{	// 该匿名函数中 无参数！
                console.log(j); // 点哪个输出哪个
            \\};
        \\}(i);	// 传入实参i,调用匿名函数
    \\}

    // 方法2：(函数调用法)
    function acti(ind) \\{
        list[ind].onclick = function () \\{	// 该匿名函数中 无参数！
            console.log(ind); // 点哪个输出哪个
        \\};
    \\}
    for (var i = 0; i < list.length; i++) \\{
        acti(i);
    \\}

    // 方法3:(添加自定义属性index法)
    // 把每个li元素加上自定义属性index, 在li被点击时获取相应index属性即可
    var ul = document.getElementById("list");
    var list = ul.querySelectorAll('li');
    for (var i = 0; i < list.length; i++) \\{
        list[i].index = i;	// 为每个li添加自定义属性并相应赋值
    \\}
    ul.addEventListener('click', function (e) \\{	// 为整个ul添加click
        console.log(e.target.index);	// 输出click target(即被点击的li) 对应的index值
    \\})

    // 方法4：(数组indexOf元素索引定位法)
    // 获取ul下的所有li，找到被点击li在所有li中的位置
    ul.addEventListener('click', function (e) \\{
        var item = e.target;
        var listArr = Array.from(list);
        console.log(listArr.indexOf(item));
    \\})
</script>
```

总结日期：2019.11.21



### jquery获取元素索引值index()示例

jquery的index()方法 搜索匹配的元素，并返回相应元素的索引值，从0开始计数。 

- 如果不给 .index() 方法传递参数，那么返回值就是这个jQuery对象集合中第一个元素相对于其同辈元素的位置。 
- 如果参数是一组DOM元素或者jQuery对象，那么返回值就是传递的元素相对于原先集合的位置。 
  如果参数是一个选择器，那么返回值就是原先元素相对于选择器匹配元素中的位置。
- 如果找不到匹配的元素，则返回-1。 

```
<ul> 
	<li id="foo">foo</li> 
	<li id="bar">bar</li> 
	<li id="baz">baz</li> 
</ul> 

$('li').index(document.getElementById('bar')); //1，传递一个DOM对象，返回这个对象在原先集合中的索引位置 
$('li').index($('#bar')); //1，传递一个jQuery对象 
$('li').index($('li:gt(0)')); //1，传递一组jQuery对象，返回这个对象中第一个元素在原先集合中的索引位置 
$('#bar').index('li'); //1，传递一个选择器，返回#bar在所有li中的做引位置 
$('#bar').index(); //1，不传递参数，返回这个元素在同辈中的索引位置。  
```

jquery获取元素索引值index()示例 代码如下:

```
//用于二级或者三级联动 
<div id="nav"> 
	<a href="http://www.51xuediannao.com/">建站素材</a> 
	<a href="http://www.51xuediannao.com/">jquery特效</a> 
	<a href="http://www.51xuediannao.com/">懒人主机</a> 
	<a href="http://www.51xuediannao.com/qd63/">前端路上</a> 
</div> 

$("#nav a").click(function()\\{ 
	//四个经典的用法 
	var index1 = $("#nav a").index(this); 
	var index2 = $("#nav a").index($(this)); 
	var index3 = $(this).index() 
	var index3 = $(this).index("a") 
	alert(index3); 
	return false; 
\\});
```

总结日期：2019.11.21



### vieo标签

| [autoplay](https://www.w3school.com.cn/tags/att_video_autoplay.asp) | autoplay | 如果出现该属性，则视频在就绪后马上播放。                     |
| ------------------------------------------------------------ | -------- | ------------------------------------------------------------ |
| [controls](https://www.w3school.com.cn/tags/att_video_controls.asp) | controls | 如果出现该属性，则向用户显示控件，比如播放按钮。             |
| [height](https://www.w3school.com.cn/tags/att_video_height.asp) | *pixels* | 设置视频播放器的高度。                                       |
| [loop](https://www.w3school.com.cn/tags/att_video_loop.asp)  | loop     | 如果出现该属性，则当媒介文件完成播放后再次开始播放。         |
| [muted](https://www.w3school.com.cn/tags/att_video_muted.asp) | muted    | 规定视频的音频输出应该被静音。                               |
| [poster](https://www.w3school.com.cn/tags/att_video_poster.asp) | *URL*    | 规定视频下载时显示的图像，或者在用户点击播放按钮前显示的图像。 |
| [preload](https://www.w3school.com.cn/tags/att_video_preload.asp) | preload  | 如果出现该属性，则视频在页面加载时进行加载，并预备播放。如果使用 "autoplay"，则忽略该属性。 |
| [src](https://www.w3school.com.cn/tags/att_video_src.asp)    | *url*    | 要播放的视频的 URL。                                         |
| [width](https://www.w3school.com.cn/tags/att_video_width.asp) | *pixels* | 设置视频播放器的宽度。                                       |

总结日期：2019.11.21



### 视频实现显示预览图

标题方法1、截图后作为预览图，然后用poster属性（举例：poster=“图片地址” ）

```
<video poster="图片url" src="视频url" controls=""></video>
```

优点：
1、能用视频以外的图片；
2、容易截到好看的图片作为封面。

标题方法2、用video里的preload=“metadata”，再地址的后面+#t=1（1是1秒的意思）（举例：地址#t=1,1是1秒的意思）。

```
<video preload="metadata" src="视频地址#=1" controls=""></video>
```

优点：
1、不需截图，十分方便；
总结日期：2019.11.21



PHP模板会自动改变标签属性为小写字母，需要注意。

总结日期：2019.11.21



### 改变自定义data属性

 jquery中data() 方法向被选元素附加数据，或者从被选元素获取数据。  data(name,value)  可以很方便的在一个html标签中添加data-*这样的自定义属性。

data方法从元素中读取数据的语法：$(selector).data(name) name:可选。规定要取回的数据的名称。如果没有规定名称，则该方法将以对象的形式从元素中返回所有存储的数据。

data方法从元素中存储数据的语法：$(selector).data(name,value)；name:必需，规定要设置的数据的名称。value:必需，规定要设置的数据的值。当然，我们在这里，也可以把一个包含键/值对的对象，向被选元素添加数据。语法如下：$(selector).data(object)object:必需。规定包含名称/值对的对象。Html代码如下：data方法之读取数据:单个数据:data-name="lichaoqiang"存储json数据:\\{"user_id":20141111,"user_name":"lichaoqiang"\\}注意：在元素data-*属性中设置json数据时，需要注意单双引号，否则可能出现undefined的,获取不到数据。正确的做法是用双引号。data方法之存储数据:这是一个div标签 

```
<body>
	<h1 data-qw="秦伟"></h1>
</body>
<script src="./js/jquery.min.js"></script>
<script>
	alert($("h1").data("qw"));
	$("h1").data("qw","qw");//原来没有该data会添加，原来有会修改
	alert($("h1").data("qw"));
</script>
```

总结日期：2019.11.25



### text-indent:-9999px 字体隐藏问题

为什么要字体隐藏？

通常为了传达更好的视觉效果，我们常用图片替代掉字体。但是为了html语义化，常常要给内容模块加上一些标题来让页面更有意义，在抛开css裸奔的情况下也能很顺利的汲取到页面信息。为此我们需将图片上的字体隐藏。另外，建站过过程中朋友喜欢把网站名称用H1表示,但从美观考虑，要用logo图片来代替h1，这时需要隐藏h1内的这段文字，但又不能对搜索引擎不友好，否则就失去了定义h1标签的意义。

 1）一般来说，偏移掉字体的方式是使用：text-indent:-9999px; （注意：只能用于block，table cells和inline-block）

text-indent:-9999px；的具体使用方法：把h1作为一个块来显示（display:block;），指定长宽（和图片一样大小），然后指定h1的背景图片，也就是将我们需要的图片作为h1这个 标签的背景。而h1标签中插入的，仍然是作为字符形式出现的博客标题，然后用text-indent:-9999px;将文字甩到屏幕看不到的地 方。（9999px应该是足够了，谁的屏幕也没那么大吧）

```
<h1>
　　<a href=“http://www.baidu,com/”>百度</a>
</h1>
```

在CSS文件中：（注意：将h1转化成block的话，他身后的的元素就被他赶到下一行了。如果正好这个h1后面，是一个按钮，就要用float来浮动以使他身后再出现簇拥者）

```
h1 a\\{
　　height:30px;
　　width:165px;
　　float:left;
　　text-indent:-9999px;
　　background-image:url(images/logo.gif);
　　background-repeat:no-repeat;
　　display:block;
　　position:relative;
　　\\}
```

在h1使用上语义明确，符合语义化定义。text-indent就是首行缩进，大家都在中文段落，首行空两格用过它。这里通过负值缩进，使文字 超出可视区，而这时h1下的背景就显示出来了，h1中包含的<a>标签又不影响使用，对于隐藏文字“站点名称”应该是最佳方案了。但对于多段 文字的隐藏这个方法就不适合了。

另外，点击<h1><a>链接时，会产生一个虚线框，对于IE还好，没什么问题，虚线框只是在背影图片大小。但是Firefox就有些麻烦，它把缩进的文字范围也包含进来了，这样不是很美观。

于是需要屏掉点击时产生的虚线框，IE和FF屏虚线框方法不一样。IE采用的遍历方法(HTC,css表达式)有些耗系统资源，正好我们只需要隐藏FF下的虚线框就行了，IE就不管了，说一下Firefox如何去掉链接的虚线框的方法。

```
1）
a\\{
　　outline:none;
　\\}
outline是css3的一个属性，用的很少。声明，这是个不能兼容的css属性，在ie6、ie7、遨游浏览器都不兼容。只有ff,ie8在加了outline:none后会取消聚焦的虚线框。
2）使用overflow:hidden;完美隐藏background之上的字体line-height:0;
font-size:0;overflow:hidden;
或 (不大适合用在h1标签上）
.text-hidden \\{
　　display:block;
　　overflow:hidden;
　　width:0;
　　height:0;
　　\\}
```

3）还有另外2种方法，不推荐使用。

  1、display:none;

　　这个大家普遍说法是，搜索引擎可能认为被隐藏的文字属于垃圾信息而被忽略，不为隐藏的对象保留物理占位空间。GG也搜CSS文件？不过如果用这个方法，<h1>如何设计，也是难题。　　

　2、visibility:hidden;

　　和display:none;相对应，为隐藏的对象保留物理占位空间。

总结日期：2019.11.25



### sort排序

 sort() 方法用于对数组的元素进行排序。 

```
arrayObject.sort(sortby)
```

| 参数     | 描述                             |
| :------- | :------------------------------- |
| *sortby* | 可选。规定排序顺序。必须是函数。 |

返回值:对数组的引用。请注意，数组在原数组上进行排序，不生成副本。

1.sort()方法有一个可选参数，是用来确定元素顺序的函数。如果这个参数被省略，那么数组中的元素将按照ASCII字符顺序进行排序。例如：

```
　var arr = ["a", "b", "A", "B"];
　arr.sort();
　console.log(arr);
```

因为字母A、B的ASCII值分别为65、66，而a、b的值分别为97、98，所以上面输出的结果是 [“A”, “B”, “a”, “b”] 。

当我们对数字进行排序的时候

```
var arr = [15, 8, 25, 3];
arr.sort();
console.log(arr);
//结果是 [15, 25, 3, 8] 。
```

其实，sort方法会调用每个数组项的toString()方法，得到字符串，然后再对得到的字符串进行排序。虽然数值15比3大，但在进行字符串比较时”1”则排在”3”前面。显然，这种结果不是我们想要的，这时，sort()方法的参数就起到了作用，我们把这个参数叫做比较函数。

对数组数字排序用函数来改变，修改方法如下：

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
//结果为 [3, 4, 9, 23, 78] 
```

返回了我们想要的结果

如果要按降序排序，比较函数写成这样即可：　

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

我们还可以对上面的函数进行简化的写法：

```
var arr = [23, 9, 4, 78, 3];
//升序
arr.sort(function(a,b)\\{
　　retun a-b;
\\});
//降序
arr.sort(function(a,b)\\{
　　retun b-a;
\\});
```

2.如果想按照其他标准进行排序，就需要提供比较函数，该函数要比较两个值，然后返回一个用于说明这两个值的相对顺序的数字。比较函数应该具有两个参数 a 和 b，其返回值如下：

- 若 a 小于 b，在排序后的数组中 a 应该出现在 b 之前，则返回一个小于 0 的值。
- 若 a 等于 b，则返回 0。
- 若 a 大于 b，则返回一个大于 0 的值。

总结日期：2019.11.26



### translate()方法

在CSS3中，我们可以使用translate()方法将元素沿着水平方向（X轴）和垂直方向（Y轴）移动。

![translate()方法](http://www.lvyestudy.com/App_images/lesson/css3/9-2-1.png)

对于位移translate()方法，我们分为3种情况：

（1）translateX(x)：元素仅在水平方向移动（X轴移动）；

（2）translateY(y)：元素仅在垂直方向移动（Y轴移动）；

（3）transklate(x,y)：元素在水平方向和垂直方向同时移动（X轴和Y轴同时移动）；

举例：transform:translateX(x);

在CSS3中，所有变形方法都是属于transform属性，因此所有关于变形的方法前面都要加上“tranform:”，以表示“变形”处理。x表示元素在水平方向（X轴）的移动距离，单位为px、em或百分比等。

当x为正时，表示元素在水平方向向右移动（X轴正方向）；当x为负时，表示元素在水平方向向左移动（X轴负方向）。

总结日期：2019.11.27



### 面包屑导航使用方法和作用

面包屑导航是每一个网站必备的一个细节优化方面，坦率的说，如果一个网站没有面包屑导航，可以初步判断，改网站的模板设计并不是很理想，那么面包屑导航作用是什么呢，我们如何增加网站的面包屑导航呢？

![导航](https://www.ssffx.com/uploads/allimg/160527/2-16052FJTC96.png)

**面包屑导航是什么？**

如上图所示，面包屑导航即包含首页、栏目、二级栏目、文章的连接，通常情况下网站的面包屑导航都是设置在页面主体内容旁边，方便用户在阅读页面的时候可以返回，当然面包屑导航不仅仅用于返回，还可以告诉用户，用户目前所以网站的位置，方便用户根据位置选择对应栏目。

**面包屑导航有什么作用？**

面包屑导航主要是告诉用户所在位置和方便用户点击指定栏目，比如你目前查看的SEO内容文章，想查看同类的文章，但你无法判断这个内容是SEO内容，那么可以通过面包屑导航选择SEO栏目。

另外一个站在SEO的角度考虑，面包屑导航可以增加我们网站内链，提高网站传递权重，这也是我们在SEO优化的一个内链策略。

最后是网站用户的使用体验，因为长期以来，大多数的网站都有面包屑导航，所以增加网站面包屑导航可以方便用户使用，这样也可以改善网站用户体验。

总结日期：2019.11.29



### pre自动换行

```
pre\\{
    width:100px;
	white-space:pre-wrap;
	white-space:-moz-pre-wrap;
	white-space:-pre-wrap;
	white-space:-o-pre-wrap;
	word-wrap:break-word;
\\}
```

总结日期：2019.12.04



### JS删除String里某个字符的方法

分割成数组，再重新拼接成新的字符串。

```
var str = "abcdaabbssaaa";
var a = str.split("a").join("");
console.log(a);
```

总结日期：2019.12.05



### 使用babel后js跨域问题

问题描述：

www.xxx.com正常使用babel，但xxx.com报错

```
Access to XMLHttpRequest at 'https://www.xxx.com/static/js/abc.js?20230406001' from origin 'https://xxx.com' has been blocked by CORS policy: No 'Access-Control-Allow-Origin' header is present on the requested resource.
```

原因：

百度到：babel.min.js库通过遍历script标签，查询type=text/babel的标签，获取该标签的src值后，发送XMLHttpRequest，由于本地file协议打开html，内部发送ajax请求js文件，协议不同，所以跨域。

我们使用了数据库后台返回的资源地址https://www.xxx.com，域名不同，所以跨域。

```
<script
    type="text/babel"
    src="\\{$configs.resources_url\\}/static/js/abc.js?\\{$static_file_version\\}"
></script>
```

修改：使用相对路径，避免域名不同的问题

```
<script
      type="text/babel"
      src="/static/js/abc.js?\\{$static_file_version\\}"
></script>
```

总结日期：2023.04.10
