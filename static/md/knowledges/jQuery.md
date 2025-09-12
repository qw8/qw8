---
title: JQuery
date: 2019-12-22 18:22:11
categories: 
- 前端知识
tags:
- JQuery
- jQuery UI
- Zepto
---
### jquery的一些基本用法

[jquery的一些基本用法](https://blog.csdn.net/qq719365064/article/details/52925155)

[jQuery的详细解析以及用法](https://blog.csdn.net/liuyingv8/article/details/79758403)



### jQuery隐藏和显示

```
	// 左侧栏隐藏
    $(".close").click(function () \\{
        $(".ask").hide();
        $(".ask-hidden").show();
    \\});
    // 左侧栏显示
    $(".ask-hidden").click(function () \\{
        $(".ask").show();
        $(".ask-hidden").hide();
    \\});
```



### jQuery实现不同按钮的切换选中效果

```
	function tagClick(value) \\{
      $(".tag").click(function () \\{
        $(".tag").removeClass("active"); // 清除已经选中了的按钮的样式
        $(this).addClass("active"); // 重新给新选中的按钮添加选中样式
      \\});
    \\}
```

或者

```
    $(this).addClass('selected').siblings().removeClass('selected');
```



### 回车键按下触发搜索

```
	  // 回车键按下触发搜索
      $(document).keydown(function (event) \\{
        if (event.keyCode == 13) \\{
          filter();
        \\}
      \\});
```



### 给动态添加的html绑定点击事件

第一种是在动态添加的html代码中添加oclick事件，然后传递一个唯一的参数来判断点击的是哪个，然后做相应的操作。 

```
		var timestamp = parseInt((new Date()).valueOf()); //唯一的标识
        console.log(timestamp);
        document.getElementById("joblist").innerhtml +=
            `<div id="job` + timestamp + `" class="job">
            <input name="CompanyName" type="text" value="公司` + timestamp + `" />
            <button onclick="DelJob(` + timestamp + `)">删除</button>
            </div>`;
        \\}
        // 删除工作经历
        function DelJob(timestamp) \\{
          document.getElementById("job" + timestamp).remove();
        \\}
```

第二种是通过事件委托的原理进行处理，事件委托将一个 事件监听器实际上绑定到整个容器，然后每个列表项被点击就可以访问，这样效率更高。



### jQuery怎么根据不同条件动态加载js文件

要根据不同条件动态加载js文件，可以使用jQuery的`$.getScript()`方法。该方法可以通过异步加载外部的js文件并执行。

以下是根据不同条件动态加载js文件的示例代码：

```
if (condition1) \\{
  $.getScript("script1.js", function() \\{
    // script1.js文件加载完成后执行的回调函数
    // 在这里可以编写需要执行的代码
  \\});
\\} else if (condition2) \\{
  $.getScript("script2.js", function() \\{
    // script2.js文件加载完成后执行的回调函数
    // 在这里可以编写需要执行的代码
  \\});
\\} else \\{
  $.getScript("defaultScript.js", function() \\{
    // defaultScript.js文件加载完成后执行的回调函数
    // 在这里可以编写需要执行的代码
  \\});
\\}
```



### 根据不同域名加载js

```
		var hostname = window.location.hostname
        // 测试数据
        // hostname = 'www.sxjayu.cn'
        // hostname = 'xiuchuan.52dingfang.cn'
        // hostname = 'car-test.xiuchuan.com'
        // hostname = 'carxiuchuan.manshang.com'
        var arr1 = hostname.split('.');
        arr1.shift();
        domain1 = arr1.join('.');
        // 除这两个域名都用智齿
        if (domain1 === 'sxjayu.cn' || domain1 === '52dingfang.cn') \\{
            document.write("<script src='https://scripts.easyliao.com/js/easyliao.js'><\/script>");
            document.write("<script src='https://scripts.easyliao.com/34415/112627.js'><\/script>");
        \\} else \\{
            // 初始化智齿客服
            initZhichi()
        \\}
```





### 如何使用jQuery清空Input的值

#### 一、从jQuery获取Input的输入值

要清空Input的值，首先需要获取当前Input中的值。可以使用jQuery的.val()函数获取输入框的值。例如：

```
    $('input:text').val();
```

代码中，通过选择器选中所有的Input输入框，然后使用.val()函数获取其值。这个函数对于所有类型的Input都适用：text, password, checkbox, radio, 等等。

#### 二、jQuery如何修改Input的value值

如果需要修改一个Input的值，可以通过.val()函数设置新的值。例如：

```
    $('input:text').val('新的值');
```

代码中，使用val()函数设置新值“新的值”到所有被选中的文本Input中。

#### 三、jQuery取Input的值

与.val()函数相反，如果需要获取Input的value值，可以使用jQuery的.attr()函数。例如：

```
    $('input:text').attr('value');
```

代码中，通过选择器选中所有文本Input，然后用.attr()函数获取它们的值。这个函数的快捷方式是使用.val()函数，但是在一些情况下（例如，checkbox或radio）使用.attr()函数可以获得更准确的值。

#### 四、jQuery获取Input的value值

如果要获取所有选中的Input的值，可以使用jQuery的serialize()函数。这个函数可以通过序列化表单值的方式将它们组成一个字符串。例如：

```
    $('form').serialize();
```

代码中，通过选择器选中所有的form元素，然后使用.serialize()函数获取值。

#### 五、jQuery设置Input的值

如果要为所有被选中的Input元素设置相同的值，可以使用如下代码：

```
    $('input:text').val('新值');
```

代码中，使用.val()函数替换所有文本Input元素的值为“新值”。

#### 六、jQuery通过name获取Input的值

如果不想使用选择器，可以通过给Input元素设置name属性获取它的值。例如：

```
    $('form input[name="username"]').val();
```

代码中，通过选择器选中form元素中name属性为“username”的Input元素，然后使用.val()函数获取它的值。

#### 七、jQuery获取Input输入框的值

要获取一个Input输入框的值，可以使用如下代码：

```
    $('input:text').val();
```

代码中，使用选择器选取所有文本Input，然后使用.val()函数获取它们的值。

#### 八、JS怎么清空Input的值

如果不想使用jQuery库，可以使用JavaScript直接清空一个Input元素的值。例如：

```
    document.getElementById("myInput").value = "";
```

代码中，使用JavaScript的原生方法获取Input元素，然后将它的值设置为空字符串即可清除它的值。

#### 九、jQuery清空文本框的值

使用jQuery清空文本框的值非常简单。只需要给文本框的value属性设置为空字符串即可。例如：

```
    $('input:text').val('');
```

代码中，使用选择器选取所有文本Input，然后使用.val()函数将它们的值设置为空字符串。这样即可清空文本框中的值。







### jQuery 的实现原理？

- `(function(window, undefined) \\{\\})(window);`
- jQuery 利用 JS 函数作用域的特性，采用立即调用表达式包裹了自身，解决命名空间和变量污染问题

- `window.jQuery = window.$ = jQuery;`
- 在闭包当中将 jQuery 和 $ 绑定到 window 上，从而将 jQuery 和 $ 暴露为全局变量



### 你觉得jQuery或zepto源码有哪些写的好的地方

- jquery源码封装在一个匿名函数的自执行环境中，有助于防止变量的全局污染，然后通过传入window对象参数，可以使window对象作为局部变量使用，好处是当jquery中访问window对象的时候，就不用将作用域链退回到顶层作用域了，从而可以更快的访问window对象。同样，传入undefined参数，可以缩短查找undefined时的作用域链

```
 (function( window, undefined ) \\{

         //用一个函数域包起来，就是所谓的沙箱

         //在这里边var定义的变量，属于这个函数域内的局部变量，避免污染全局

         //把当前沙箱需要的外部变量通过函数参数引入进来

         //只要保证参数对内提供的接口的一致性，你还可以随意替换传进来的这个参数

        window.jQuery = window.$ = jQuery;

    \\})( window );
```

- jquery将一些原型属性和方法封装在了jquery.prototype中，为了缩短名称，又赋值给了jquery.fn，这是很形象的写法
- 有一些数组或对象的方法经常能使用到，jQuery将其保存为局部变量以提高访问速度
- jquery实现的链式调用可以节约代码，所返回的都是同一个对象，可以提高代码效率



### jQuery 和 Zepto 的区别？ 各自的使用场景？


* jQuery 主要目标是PC的网页中，兼容全部主流浏览器。在移动设备方面，单独推出 jQuery Mobile
* Zepto 从一开始就定位移动设备，相对更轻量级。它的 API 基本兼容 jQuery，但对PC浏览器兼容不理想



### jquery.extend 与 jquery.fn.extend的区别？

- jquery.extend 为jquery类添加类方法，可以理解为添加静态方法
- jquery.fn.extend:源码中jquery.fn = jquery.prototype，所以对jquery.fn的扩展，就是为jquery类添加成员函数
  使用：
- jquery.extend扩展，需要通过jquery类来调用，而jquery.fn.extend扩展，所有jquery实例都可以直接调用



### jQuery UI 如何自定义组件？

- 通过向 $.widget() 传递组件名称和一个原型对象来完成
- `$.widget("ns.widgetName", [baseWidget], widgetPrototype);`



### jQuery 与 jQuery UI、jQuery Mobile 区别？

* jQuery 是 JS 库，兼容各种PC浏览器，主要用作更方便地处理 DOM、事件、动画、AJAX，主要提供的功能是选择器，属性修改和事件绑定等等

* jQuery UI 是建立在 jQuery 库上，利用jQuery的扩展性设计的插件，一组用户界面交互、特效、小部件及主题。供了一些常用的界面元素，诸如对话框、拖动行为、改变大小行为等等

* jQuery Mobile 以 jQuery 为基础，用于创建“移动Web应用”的框架



### jQuery 一个对象可以同时绑定多个事件，这是如何实现的？

jQuery可以给一个对象同时绑定多个事件，低层实现方式是使用addEventListner或attachEvent兼容不同的浏览器实现事件的绑定，这样可以给同一个对象注册多个事件。



### jQuery 的 slideUp 动画，当鼠标快速连续触发, 动画会滞后反复执行，该如何处理呢?

* 在触发元素上的事件设置为延迟处理：使用 JS 原生 setTimeout 方法
* 在触发元素的事件时预先停止所有的动画，再执行相应的动画事件：$('.tab').stop().slideUp();



### 如何判断当前脚本运行在浏览器还是node环境中？（阿里）

- this === window ? 'browser' : 'node';
- 通过判断Global对象是否为window，如果不为window，当前脚本没有运行在浏览器中



### jQuery 的 slideUp动画 ，如果目标元素是被外部事件驱动, 当鼠标快速地连续触发外部元素事件, 动画会滞后的反复执行，该如何处理呢?

- jquery stop(): 如：$("#div").stop().animate(\\{width:"100px"\\},100);



### 那些操作会造成内存泄漏？

- 内存泄漏指任何对象在您不再拥有或需要它之后仍然存在
- 垃圾回收器定期扫描对象，并计算引用了每个对象的其他对象的数量。如果一个对象的引用数量为 0（没有其他对象引用过该对象），或对该对象的惟一引用是循环的，那么该对象的内存即可回收
- setTimeout 的第一个参数使用字符串而非函数的话，会引发内存泄漏。
  闭包、控制台日志、循环（在两个对象彼此引用且彼此保留时，就会产生一个循环)



### JQuery一个对象可以同时绑定多个事件，这是如何实现的？

- 多个事件同一个函数：`$("div").on("click mouseover", function()\\{\\});`
- 多个事件不同函数

```
$("div").on(\\{
	click: function()\\{\\},
	mouseover: function()\\{\\}
\\});
```

```javascript
  $("#btn").on("mouseover mouseout", func);

  $("#btn").on(\\{
      mouseover: func1,
      mouseout: func2,
      click: func3
  \\});
```



### jQuery.fn 的 init 方法返回的 this 指的是什么对象？ 为什么要返回 this？

* jQuery.fn 的 init 方法 返回的 this 就是 jQuery 对象
* 用户使用 jQuery() 或 $() 即可初始化 jQuery 对象，不需要动态的去调用 init 方法



### jQuery 的属性拷贝(extend)的实现原理是什么，如何实现深拷贝？

- 浅拷贝（只复制一份原始对象的引用）
`var newObject = $.extend(\\{\\}, oldObject);`

- 深拷贝（对原始对象属性所引用的对象进行进行递归拷贝）
`var newObject = $.extend(true, \\{\\}, oldObject);`



### jQuery 中的 bind(), live(), delegate(), on()的区别？


* bind 直接绑定在目标元素上
* live 通过冒泡传播事件，默认document上，支持动态数据
* delegate 更精确的小范围使用事件代理，性能优于 live
* on 是最新的1.9版本整合了之前的三种方式的新事件绑定机制



### 是否知道自定义事件？ jQuery 里的 fire 函数是什么意思，什么时候用？

* 事件即“发布/订阅”模式，自定义事件即“消息发布”，事件的监听即“订阅订阅”
* JS 原生支持自定义事件，示例：

```javascript
  document.createEvent(type); // 创建事件
  event.initEvent(eventType, canBubble, prevent); // 初始化事件
  target.addEventListener('dataavailable', handler, false); // 监听事件
  target.dispatchEvent(e);  // 触发事件
```

- jQuery 里的 fire 函数用于调用 jQuery 自定义事件列表中的事件



### jQuery 通过哪个方法和 Sizzle 选择器结合的？


* Sizzle 选择器采取 Right To Left 的匹配模式，先搜寻所有匹配标签，再判断它的父节点
* jQuery 通过 $(selecter).find(selecter); 和 Sizzle 选择器结合



### jQuery 中如何将数组转化为 JSON 字符串，然后再转化回来？

```javascript
// 通过原生 JSON.stringify/JSON.parse 扩展 jQuery 实现
 $.array2json = function(array) \\{
    return JSON.stringify(array);
 \\}

 $.json2array = function(array) \\{
    // $.parseJSON(array); // 3.0 开始，已过时
    return JSON.parse(array);
 \\}

 // 调用
 var json = $.array2json(['a', 'b', 'c']);
 var array = $.json2array(json);
```



### 谈一下 Jquery 中的 bind(),live(),delegate(),on()的区别？

- bind： 绑定事件，对新添加的事件不起作用，方法用于将一个处理程序附加到每个匹配元素的事件上并返回 jQuery 对象。
- live： 方法将一个事件处理程序附加到与当前选择器匹配的所有元素（包含现有的或将来添加的）的指定事件上并返回 jQuery 对象。
- delegate： 方法基于一组特定的根元素将处理程序附加到匹配选择器的所有元素（现有的或将来的）的一个或多个事件上。



### jQuery.extend 与 jQuery.fn.extend 的区别？

* $.fn.extend() 和 $.extend() 是 jQuery 为扩展插件提拱了两个方法
* $.extend(object); // 为jQuery添加“静态方法”（工具方法）

```
$.extend(\\{
　　min: function(a, b) \\{ return a < b ? a : b; \\},
　　max: function(a, b) \\{ return a > b ? a : b; \\}
\\});
$.min(2,3); //  2
$.max(4,5); //  5
```

 * $.extend([true,] targetObject, object1[, object2]); // 对targt对象进行扩展

 ```
var settings = \\{validate:false, limit:5\\};
var options = \\{validate:true, name:"bar"\\};
$.extend(settings, options);  // 注意：不支持第一个参数传 false
// settings == \\{validate:true, limit:5, name:"bar"\\}
 ```

* $.fn.extend(json); // 为jQuery添加“成员函数”（实例方法）

```
$.fn.extend(\\{
   alertValue: function() \\{
      $(this).click(function()\\{
        alert($(this).val());
      \\});
   \\}
\\});

$("#email").alertValue();
```



### jQuery 的队列是如何实现的？队列可以用在哪些地方？

* jQuery 核心中有一组队列控制方法，由 queue()/dequeue()/clearQueue() 三个方法组成。
* 主要应用于 animate()，ajax，其他要按时间顺序执行的事件中

```javascript
var func1 = function()\\{alert('事件1');\\}
var func2 = function()\\{alert('事件2');\\}
var func3 = function()\\{alert('事件3');\\}
var func4 = function()\\{alert('事件4');\\}

// 入栈队列事件
$('#box').queue("queue1", func1);  // push func1 to queue1
$('#box').queue("queue1", func2);  // push func2 to queue1

// 替换队列事件
$('#box').queue("queue1", []);  // delete queue1 with empty array
$('#box').queue("queue1", [func3, func4]);  // replace queue1

// 获取队列事件（返回一个函数数组）
$('#box').queue("queue1");  // [func3(), func4()]

// 出栈队列事件并执行
$('#box').dequeue("queue1"); // return func3 and do func3
$('#box').dequeue("queue1"); // return func4 and do func4

// 清空整个队列
$('#box').clearQueue("queue1"); // delete queue1 with clearQueue
```



### jquery 中如何将数组转化为json字符串，然后再转化回来？

- jQuery中没有提供这个功能，所以你需要先编写两个jQuery的扩展：

```
$.fn.stringifyArray = function(array) \\{
    return JSON.stringify(array)
\\}

$.fn.parseArray = function(array) \\{
    return JSON.parse(array)
\\}

然后调用：
$("").stringifyArray(array)
```



### 针对 jQuery 的优化方法？

- 尽量使用id选择器代替class选择器。基于Class的选择性的性能相对于Id选择器开销很大，因为需遍历所有DOM元素。

- 频繁操作的DOM，先缓存起来再操作。用Jquery的链式调用更好

  比如：var str=$("a").attr("href");

- for (var i = size; i < arr.length; i++) \\{\\}

  for 循环每一次循环都查找了数组 (arr) 的.length 属性，在开始循环的时候设置一个变量来存储这个数字，可以让循环跑得更快：

  for (var i = size, length = arr.length; i < length; i++) \\{\\}

* 总是从#id选择器来继承
* 尽量使用链式操作
* 使用时间委托 on 绑定事件
* 采用jQuery的内部函数data()来存储数据
* 使用最新版本的 jQuery
