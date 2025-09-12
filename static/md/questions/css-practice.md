---
title: CSS实践
date: 2022-05-21 19:45:42
categories: 
- 前端问题
tags:
- CSS
---

### 常用公共css

```
// 超出1行省略
.ellipsis-one \\{
  /* 强制不换行 */
  white-space: nowrap;
  /* 超出一行文字自动隐藏 */
  overflow: hidden;
  /* 文字隐藏后添加省略号 */
  text-overflow: ellipsis;
\\}
// 超出2行省略
.ellipsis-tow \\{
  display: -webkit-box;
  overflow: hidden;
  text-overflow: -o-ellipsis-lastline;
  text-overflow: ellipsis;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
\\}
// 超出3行省略
.ellipsis-three \\{
  display: -webkit-box;
  overflow: hidden;
  text-overflow: -o-ellipsis-lastline;
  text-overflow: ellipsis;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
\\}
// 垂直居中
.align-center \\{
  display: flex;
  align-items: center;
\\}
// 弹窗限制宽度
.popup \\{
  max-width: 740px;
  left: 50\\%;
  transform: translateX(-50\\%);
\\}
// 蓝色文字
.blue-text \\{
  color: #267ef0;
\\}
// 蓝色按钮
.blue-btn \\{
  cursor: pointer;
  color: #267ef0;
\\}
// 鼠标手势
.pointer \\{
  cursor: pointer;
\\}
// 吸顶时水平居中，兼容ios
.van-sticky--fixed \\{
  width: 100\\%;
  max-width: 740px;
  left: 0;
  right: 0;
  margin: 0 auto;
\\}
```



### css控制文字显示几行

#### 一行

```css
// 超出1行省略
.ellipsis-one \\{
  /* 强制不换行 */
  white-space: nowrap;
  /* 超出一行文字自动隐藏 */
  overflow: hidden;
  /* 文字隐藏后添加省略号 */
  text-overflow: ellipsis;
\\}
```

如果文本中间有换行符，如果不设置高度就会失效，所以尽量设置高度。

问题： 父元素需要自适应宽度flex: 1;子元素期望超出一行省略

解决：父元素设置overflow: hidden;不然会被撑宽，困扰好久的问题

```
.parent \\{
  flex: 1;
  overflow: hidden;
\\}
```

#### 多行

```css
// 超出2行省略
.ellipsis-tow \\{
  display: -webkit-box;
  overflow: hidden;
  text-overflow: -o-ellipsis-lastline;
  text-overflow: ellipsis;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
\\}
```

-webkit-line-clamp 是一个 不规范的属性（unsupported WebKit property），它没有出现在 CSS 规范草案中。限制在一个块元素显示的文本的行数。 为了实现该效果，它需要组合其他外来的WebKit属性。常见结合属性：

```css
display:-webkit-box;
必须结合的属性 ，将对象作为弹性伸缩盒子模型显示 。
-webkit-box-orient
必须结合的属性 ，设置或检索伸缩盒对象的子元素的排列方式 。
text-overflow
确定如何向用户发出未显示的溢出内容信号.它可以被剪切，显示一个省略号（'...'）或显示一个自定义字符串；可以用来多行文本的情况下，用省略号“...”隐藏超出范围的文本 。
```



### font-weight 属性设置文本的粗细

该属性用于设置显示元素的文本中所用的字体加粗。数字值 400 相当于 关键字 normal，700 等价于 bold。

每个数字值对应的字体加粗必须至少与下一个最小数字一样细，而且至少与下一个最大数字一样粗。

适用于：所有元素
继承：是
百分比：（不适用）

```
font-weight: normal;  // 默认值。定义标准的字符。正常的字体，声明此值取消之前任何设置
font-weight: bold;    // 定义粗体字符，也相当于b标签的作用
font-weight: bolder;  // 定义更粗的字符。
font-weight: lighter; // 定义更细的字符。
font-weight: inherit; // 规定应该从父元素继承字体的粗细。
font-weight: 100;
font-weight: 200;
font-weight: 300;
font-weight: 400;
font-weight: 500;
font-weight: 600;
font-weight: 700;
font-weight: 800;
font-weight: 900;
```



### Regular、Normal、Medium、Light 对应的font-weight值

‘font-weight’属性执行字体中字形的重量，这取决于黑度等级或笔划粗细。其值的意义如下：
100至900，这些有序排列中的每个值，表示至少与其起身拥有相同黑度的重量。其大致符合下列通用重量名称：

```
100 - Thin
200 - Extra Light (Ultra Light)
300 - Light
400 - Regular (Normal、Book、Roman)
500 - Medium
600 - Semi Bold (Demi Bold)
700 - Bold
800 - Extra Bold (Ultra Bold)
900 - Black (Heavy)
```



### ios电脑字体过粗

```
/* 通用 */
* \\{
    box-sizing: border-box;
\\}

html,
body \\{
  	font-family: PingFang, PingFangSC-Regular, PingFang SC, Microsoft Yahei UI, Microsoft Yahei,微软雅黑,Segoe UI,Tahoma,Arial，宋体b8b体,SimSun,sans-serif;
    text-rendering: optimizeLegibility;
    text-size-adjust: 100\\%;
    -webkit-font-smoothing: antialiased;
    -webkit-text-size-adjust: 100\\%;
  	-ms-text-size-adjust: 100\\%;
\\}

.bold \\{
    font-weight: bold;
\\}
```



### cursor属性

ursor属性定义了鼠标指针放在一个元素边界范围内时所用的光标形状

| 默认值：          | auto                              |
| :---------------- | --------------------------------- |
| 继承：            | yes                               |
| 版本：            | CSS2                              |
| JavaScript 语法： | *object*.style.cursor="crosshair" |

属性值

| 值        | 描述                                                         |
| :-------- | :----------------------------------------------------------- |
| *url*     | 需使用的自定义光标的 URL。注释：请在此列表的末端始终定义一种普通的光标，以防没有由 URL 定义的可用光标。 |
| default   | 默认光标（通常是一个箭头）                                   |
| auto      | 默认。浏览器设置的光标。                                     |
| crosshair | 光标呈现为十字线。                                           |
| pointer   | 光标呈现为指示链接的指针（一只手）                           |
| move      | 此光标指示某对象可被移动。                                   |
| e-resize  | 此光标指示矩形框的边缘可被向右（东）移动。                   |
| ne-resize | 此光标指示矩形框的边缘可被向上及向右移动（北/东）。          |
| nw-resize | 此光标指示矩形框的边缘可被向上及向左移动（北/西）。          |
| n-resize  | 此光标指示矩形框的边缘可被向上（北）移动。                   |
| se-resize | 此光标指示矩形框的边缘可被向下及向右移动（南/东）。          |
| sw-resize | 此光标指示矩形框的边缘可被向下及向左移动（南/西）。          |
| s-resize  | 此光标指示矩形框的边缘可被向下移动（南）。                   |
| w-resize  | 此光标指示矩形框的边缘可被向左移动（西）。                   |
| text      | 此光标指示文本。                                             |
| wait      | 此光标指示程序正忙（通常是一只表或沙漏）。                   |
| help      | 此光标指示可用的帮助（通常是一个问号或一个气球）。           |



### css设置鼠标手形，且连续点击div不选中里面的字体

```
cursor:pointer; //鼠标手形
user-select:none; /*标准语法*/
-moz-user-select:none; /*火狐*/
-webkit-user-select:none; /*webkit浏览器*/
-ms-user-select:none; /*IE10*/
```

#### user-select属性值：

- `auto`：表示元素的内容可以被选中。

- `none`：表示元素的内容不能被选中。
- `text`：表示元素的文本内容可以被选中，但是其他内容不能被选中。
- all：当所有内容作为一个整体时可以被选择。如果双击或者在上下文上点击子元素，那么被选择的部分将是以该子元素向上回溯的最高祖先元素。
- lement：可以选择文本，但选择范围受元素边界的约束

#### 禁用选中样式

除了禁用选择功能，有时候我们还希望禁止元素被选中时的默认样式。这可以通过为元素添加`-webkit-tap-highlight-color`属性来实现，如下所示：

```css
div.example \\{
  -webkit-tap-highlight-color: rgba(0, 0, 0, 0); /* Safari/Chrome */
  tap-highlight-color: rgba(0, 0, 0, 0);
\\}
```

在这个例子中，具有`example`类名的`div`元素将没有选中时的高亮效果。



### CSS扩大可点击区域的2种方法

<button class="btn">点击</button>`<button class="btn">点击</button>`

一、使用 border/padding 属性扩大可点击区域

```
.btn \\{
    border: 20px solid transparent;
    background-clip: padding-box;
\\}
 
或者
.btn \\{
   padding: 20px;
\\}
```

 二、使用伪元素扩大可点击区域 

```
.btn \\{
    position: relative;
\\}
 
.btn::before \\{
    content: '';
    position: absolute;
    top: -20px;
    right: -20px;
    bottom: -20px;
    left: -20px;
\\}
```



### css设置滚动条

只设置水平滚动条：

```
<div style="width:100px;overflow-x:auto"></div>
```

只设置垂直滚动条：

```
<div style="height:300px;overflow-y:auto"></div>
```

水平与垂直都设置：

```
<div style="width:70px;height:300px;overflow-x:auto;overflow-y:auto"></div>
```

```
//或者直接
overflow: scroll;
```



### css实现横向滚动

要在CSS中实现横向滚动，你需要确保你的容器元素的宽度超过了其可视区域的宽度，并且设置了`overflow-x`属性为`auto`或`scroll`。

核心属性overflow-x、white-space、display

```css
<div class="scroll-container">  
    <div class="scroll-content">  
        <!-- 这里是你的内容，可以是多个div或其他元素 -->  
        <div>内容1</div>  
        <div>内容2</div>  
        <div>内容3</div>  
        <!-- ... 更多内容 ... -->  
    </div>  
</div>

.scroll-container \\{  
    width: 100\\%; /* 或者你可以设置一个固定的宽度，比如 500px */
    white-space: nowrap; /* 防止内容换行 */
    overflow-x: auto; /* 当内容超出容器宽度时，显示横向滚动条 */
    /* 以下代码用于隐藏滚动条，主要针对WebKit内核的浏览器 */
    &::-webkit-scrollbar \\{
      display: none;
    \\}
    box-sizing: border-box; /* 包括padding和border在width内 */  
    /* 可以添加一些样式，如边框、背景色等 */  
    border: 1px solid #ccc;  
    padding: 10px;  
\\}  
  
.scroll-content > div \\{  
    display: inline-block; /* 使内容并排显示 */  
    width: 200px; /* 设置每个内容的宽度 */  
    height: 100px; /* 设置每个内容的高度 */  
    margin-right: 10px; /* 每个内容之间的间距 */  
    /* 可以添加一些样式，如背景色、边框等 */  
    background-color: #f0f0f0;  
    border: 1px solid #ddd;  
\\}
```



### 一行展示，超出可以横向滚动或者滑动，适配移动端

为了确保 `.area-list` 在移动端可以一行展示，并且当内容超出容器宽度时能够横向滚动或滑动，您已经在 CSS 中设置了一些正确的属性。不过，为了让这个功能在所有设备上都能正常工作，还需要做一些额外的调整和优化。

以下是优化后的代码：

```css
.area-list \\{
  padding: 15px 0 16px 15px;
  display: flex;
  justify-content: space-between;
  display: flex;
  /* 确保内部元素不会换行 */
  flex-wrap: nowrap;
  /* 当内容超出容器宽度时，显示横向滚动条 */
  overflow-x: auto;
  /* 平滑滚动 */
  scroll-behavior: smooth;
  /* 隐藏滚动条，但仍然允许通过触摸滚动 */
  -ms-overflow-style: none;  /* IE and Edge */
  scrollbar-width: none;  /* Firefox */
  &::-webkit-scrollbar \\{
      display: none;
  \\}
\\}

.area-item \\{
    /* 使用min-width以确保每个item至少有这个宽度 */
  	min-width: 124px;
    height: 48px;
    line-height: 48px;
    padding: 0 10px 0 12px;
    margin-right: 15px;
    border-radius: 8px;
    display: flex;
    align-items: center;
    text-align: center;
    cursor: pointer;
    color: #222222;
    /* 如果需要每个项目点击交互，确保它有足够的触摸目标区域 */
    flex-shrink: 0; /* 防止缩小 */
    background: #fff;
    box-shadow: 0px 2px 4px 0px rgba(0, 0, 0, 0.09);
\\}
```

另外，考虑到移动设备上的用户体验，可能需要添加一些媒体查询来进一步优化布局，比如在小屏幕上减少内边距或者调整项目的尺寸等。

对于触摸设备来说，确保滚动是平滑的也很重要。如果使用的是现代浏览器，您可以尝试为`.area-list`添加`scroll-behavior: smooth;`来启用平滑滚动。

最后，确保您的HTML结构支持这种样式应用，例如：

```html
<div class="area-list">
  <div class="area-item">Item 1</div>
  <div class="area-item">Item 2</div>
  <!-- 更多 .area-item 元素 -->
</div>
```

请测试这些更改，看看它们是否满足您的需求。如果您使用的是框架（如React、Vue等），确保这些样式规则正确地应用于组件。

#### 在pc横向滚动条细一点，移动端隐藏

```
@media (min-width: 740px) \\{
  .horizontal \\{
    /* 针对Webkit内核浏览器（如Chrome和Safari）的滚动条样式 */
    &::-webkit-scrollbar \\{
      height: 6px; /* 设置滚动条的高度 */
    \\}
    &::-webkit-scrollbar-thumb \\{
      background-color: #f2f2f2; /* 滚动条颜色 */
      border-radius: 3px;
    \\}
    &::-webkit-scrollbar-track \\{
      background-color: transparent; /* 滚动条轨道颜色 */
    \\}
  \\}
\\}
@media (max-width: 739px) \\{
  // 移动端、中等尺寸屏幕
  .horizontal \\{
    /* 隐藏滚动条，但仍然允许通过触摸滚动 */
    -ms-overflow-style: none; /* IE and Edge */
    scrollbar-width: none; /* Firefox */
    &::-webkit-scrollbar \\{
      display: none;
    \\}
  \\}
\\}
```



### css隐藏滚动条的方法

#### 方法一：

纯CSS+div样式隐藏。

在需要滚动的元素外面再套一个div，给最外面的div设置样式overflow:hidden，宽度比需要滚动的元素小；

之后给需要滚动的元素设置样式overflow-x:hidden; overflow-y:scroll；

```
// uniapp去除页面滚动条
.page \\{
    min-height: 100vh;
    overflow: hidden;
    background:#F5F7FA;
\\}
.content\\{
    height: 100\\%;
    overflow-y: auto;
\\}
```

#### 方法二

给需要滚动的元素添加伪选择器，::-webkit-scrollbar\\{width:0;\\}，

将宽度设为0，滚动条就会隐藏。

```
/* 去除h5滚动条 */
::-webkit-scrollbar \\{
    display: none !important;
    width: 0 !important;
    height: 0 !important;
    -webkit-appearance: none;
    background: transparent;
\\}
```

#### 可以设置滚动条样式，使其美观。

```
/*滚动条宽 长,滚动条整体部分，其中的属性有width,height,background,border等。*/
.xxx::-webkit-scrollbar\\{
         width: 8px;
\\}
/*滚动条的滑轨背景颜色,可以用display:none让其不显示，也可以添加背景图片，颜色改变显示效果。*/
    ::-webkit-scrollbar-track\\{
       	background-color: rgba(0, 0, 0, 0.2);
		-webkit-box-shadow:  2px 2px 2px rgba(27, 158, 252, .5) inset,
		-2px -2px 2px rgba(27, 158, 252, .5) inset;
		border-radius: 5px;
	\\}
/* 滑块颜色 */
    ::-webkit-scrollbar-thumb\\{
        background-color: rgba(0, 200, 255, .3);
		border-radius: 5px;
    \\}

/*滚动条两端的按钮。可以用display:none让其不显示，也可以添加背景图片，颜色改变显示效果。*/
    ::-webkit-scrollbar-button\\{
        background-color: #eee;
        display: none;
   	\\}
/* 横向滚动条和纵向滚动条相交处尖角的颜色 */
	::-webkit-scrollbar-corner\\{
    	background-color: black;
	\\}
```

以上代码适用于谷歌，要使滚动条兼容火狐，在需要滚动的div盒子设置样式：

```
scrollbar-color: rgba(0, 200, 255, .4) rgba(0, 200, 255, 0.2); /* 滑块颜色  滚动条背景颜色 */
scrollbar-width: thin; /* 滚动条宽度有三种：thin、auto、none */
```



### rem与px的转换

`rem`是相对于根元素`<html>`，这样就意味着，我们只需要在根元素确定一个参考值，这个参考值设置为多少，完全可以根据您自己的需求来定。 我们知道，浏览器默认的字号`16px`，来看一些`px`单位与`rem`之间的转换关系：

```
|  px  |     rem       |
------------------------
|  10  | 10/16 = 0.625  |
|  12  | 12/16 = .75   |
|  14  | 14/16 = .875  |
|  16  | 16/16 = 1     |
|  18  | 18/16 = 1.125 |
|  20  | 20/16 = 1.25  |
|  24  | 24/16 = 1.5   |
|  26  | 26/16 = 1.625 |
|  28  | 28/16 = 1.75  |
|  30  | 30/16 = 1.875 |
|  36  | 36/16 = 2.25  |
|  42  | 42/16 = 2.625 |
|  48  | 48/16 = 3     |
-------------------------        
```

为了方便计算，时常将在`<html>`元素中设置`font-size`值为`62.5\\%`: 相当于在`<html>`中设置`font-size`为`10px`，此时，上面示例中所示的值将会改变：

```
|  px  |     rem        |
-------------------------
|  12  | 12/10 = 1.2    |
|  14  | 14/10 = 1.4    |
|  16  | 16/10 = 1.6    |
|  18  | 18/10 = 1.8    |
|  20  | 20/10 = 2.0    |
|  24  | 24/10 = 2.4    |
|  30  | 30/10 = 3.0    |
|  36  | 36/10 = 3.6    |
|  42  | 42/10 = 4.2    |
|  48  | 48/10 = 4.8    |
-------------------------        
```

`rem`在众多浏览器中都已得到很好的支持，如果您的项目不用考虑IE低版本的话，你就可以放心的使用了。 **1rem等于多少px呢？** 1rem等于html根元素设定的font-size的px值，假如我们在css里面设定下面的css。

```
html\\{font-size:14px\\}
```

那么后面的CSS里面的rem值则是以这个14来换算，例如设定一个div宽度为3rem,高度为2.5rem.则它换算成px为width:42px.height:35px，同理，假如一个设计稿为宽度42px,高度为35px，则换成成rem，则是42/14=3rem，35/14=2.5rem。 如果css里面没有设定html的font-size，则默认浏览器以1rem=16px来换算



### 子元素选择器

:nth-child(*n*) 选择器匹配属于其父元素的第 N 个子元素，不论元素的类型。

*n* 可以是数字、关键词或公式。

如**3的倍数元素选择器**

```
.tabs-content:nth-child(3n) \\{
	background: #ff0000;
\\}
//3n就是3的倍数都加这个样式*/
.list li:nth-child(3n)\\{ border-bottom:1px;\\} 
```



### CSS3 :nth-last-child() 选择器

规定属于其父元素的第二个子元素的每个 p 元素，从最后一个子元素开始计数：

```
p:nth-last-child(2)
\\{
	background:#ff0000;
\\}
```

:nth-last-child(*n*) 选择器匹配属于其元素的第 N 个子元素的每个元素，不论元素的类型，从最后一个子元素开始计数。

*n* 可以是数字、关键词或公式。

Odd 和 even 是可用于匹配下标是奇数或偶数的子元素的关键词（第一个子元素的下标是 1）。

在这里，我们为奇数和偶数 p 元素指定两种不同的背景色，从最后一个子元素开始计数：

```
p:nth-last-child(odd)
\\{
	background:#ff0000;
\\}
p:nth-last-child(even)
\\{
	background:#0000ff;
\\}
```

使用公式 (*an* + *b*)。描述：表示周期的长度，n 是计数器（从 0 开始），b 是偏移值。

在这里，我们指定了下标是 3 的倍数的所有 p 元素的背景色，从最后一个子元素开始计数：

```
p:nth-last-child(3n+0)
\\{
	background:#ff0000;
\\}
```



### 最后一个元素不想要某样式，如margin-right

```
.turnOn:nth-child(1)
\\{
  margin-right: 33px;
\\}
.turnOn:nth-child(2)
\\{
  margin-right: 33px;
\\}
.turnOn:nth-child(3)
\\{
  margin-right: 0px;
\\}
```

要使用CSS选择元素中除最后一个之外的所有子元素，可以使用使用:not和:last-child选择器

**:not(selector) 选择器**：用来匹配非指定元素/选择器的每个元素。

**:last-child选择器**：用来匹配父元素中最后一个子元素。

上面代码可以替换为（）

```
.turnOn:not(:last-child) \\{ 
  margin-right: 33px;
\\}
```



### 小程序不支持.turnOn(:last-child) 语法，可用下方代码

 为什么:last-child失效：因为.staffli下方还有同级元素，wx:for(.staffli)的外层包一层view就可以了。

el:last-child 匹配顺序：

第一，查找el 其父级的所有同级子元素（如jQuery的siblings）；

第二，在同级元素中找到最后一个元素；

第三，校验最后一个元素是否和el一致。

```
<view class="form">
    <view class="form-item">
    </view>
</view>

.form-item \\{
    border-bottom: 1rpx solid #f0f2f5;
    &:last-child \\{
        border-bottom: 0;
    \\}
\\}
```



### currentColor

只要是需要使用颜色的地方都可以用关键字`CurrentColor`替换，使其保持和当前元素`color`属性的值一致。

由于`color`属性可以被继承，所以有的时候只需要在祖元素设置好`color`属性，其子元素和孙元素都可以使用`currentcolor`来调用祖元素的颜色。

由以上所有文字我们可以总结出来几点。首先这货可以拿来装逼，其次这货能调用`color`的值，最后根据继承性的存在一旦在DOM节点设置`color`属性那么属于此节点的分支都可以用这货来调用`color`值。



### 右边右对齐布局

```
.parameter \\{
		width: 100\\%;
		padding: 40rpx;
		display: flex;
		justify-content: space-between;
		font-size: 28rpx;

		.title \\{
			width: 25\\%;
		\\}

		.content \\{
			max-width: 75\\%;//防止多行文字时文字右对齐
		\\}
	\\}
```



### CSS3盒子阴影语法

```css
box-shadow:水平阴影 垂直阴影 模糊距离（虚实） 阴影尺寸（影子大小） 阴影颜色 内/外阴影；
```

| 值       | 描述                                   |
| :------- | :------------------------------------- |
| h-shadow | 必需。水平阴景拍的位置。允许负值。     |
| v-shadow | 必需。垂直阴景拍的位置。允许负值。     |
| blur     | 可选。模糊距离。                       |
| spread   | 可选。阴景的尺寸。                     |
| color    | 可选。阴景的颜色。请参阅CSS颜色值。    |
| inset    | 可选。将外部阴影(outset)改为内部阴影。 |

前两个属性是必须写的。其余的可以省略。

外阴影(outset)是默认的，但是不能写，想要内阴影可以写 inset。

```css
div \\{
    box-shadow: 0 2rpx 6rpx 0 rgba(255, 255, 255, 0.5); // 外阴影
    box-shadow: -2rpx -4rpx 16rpx 0 rgba(36, 82, 255, 0.4) inset; // 内阴影
\\}
```

如果要完全禁用或覆盖一个组件上的`box-shadow`，使其不显示

```
.my-component \\{
  box-shadow: none;
\\}
```



### 好看的box-shadow样式

```
box-shadow: 0px -1px 0px 0px #ff0000, //上边阴影  红色
			-1px 0px 0px 0px #3bee17, //左边阴影  绿色
			1px 0px 0px 0px #2279ee, //右边阴影  蓝色
			0px 1px 0px 0px #eede15; //下边阴影  黄色
```



### 利用伪元素画圆形

```
span::before \\{
    content: '';
    width: 6px;
    height: 6px;
    border-radius: 50\\%;
    position: absolute;
    top: 9px;
    left: -12px;
    background: #D8DDE6;
\\}
```



### 利用伪元素画菱形

```
.sub-title::before \\{
    content: '';
    width: 6px;
    height: 6px;
    position: absolute;
    top: 11px;
    left: -19px;
    transform: rotate(45deg);
    background: rgba(255, 255, 255, .32);
\\}
```



### 清除浮动

#### 知道 css 有个 content 属性吗？有什么作用？有什么应用？

知道。css 的 content 属性专门应用在 before/after 伪元素上，用来插入生成内容。最常见的应用是利用伪类清除浮动。

after 伪元素通过 content 在元素的后面生成了内容为一个点的块级素，再利用 clear:both 清除浮动。

```css
.clearfix \\{
    zoom: 1;
    /*ie6清除浮动的方式 *号只有IE6-IE7执行，其他浏览器不执行*/
\\}

.clearfix:after \\{
    /*伪元素是行内元素 正常浏览器清除浮动方法*/
    content: '';
    display: block;
    height: 0;
    clear: both;
    visibility: hidden;
\\}
```



### CSS 设置页面缩放

为了设置页面缩放，可以使用以下 CSS 属性：

```
body \\{
  zoom: 80\\%; /* 缩放比例 */
\\}
```


或者使用以下 CSS 属性：

```
body \\{
  transform: scale(0.8); /* 缩放比例 */
  transform-origin: 0 0; /* 缩放的原点 */
\\}
```


请注意，缩放可能影响页面布局。因此，应谨慎使用该特性。

为特定设备（例如移动设备）设置不同的缩放，可以使用媒体查询。例如：

```
@media only screen and (max-width: 480px) \\{
  body \\{
    zoom: 60\\%;
  \\}
\\}
```


这意味着，当屏幕宽度不超过 480px 时，页面将以 60\\% 的比例缩放。

请注意，在某些情况下，使用缩放可能不是一种最佳选择。例如，如果希望以响应式方式设计您的页面，则应考虑使用流式布局和媒体查询，而不是缩放。

除了缩放外，还可以使用 CSS 布局和媒体查询调整页面样式，以适应不同大小的屏幕。例如，可以使用 @media 规则调整页面字体大小，改变行高，调整图像尺寸等。



### 网站变灰默哀

> 霍金去世了 很惋惜

```css
filter: grayscale(100\\%);
-webkit-filter: grayscale(100\\%);
-moz-filter: grayscale(100\\%);
-ms-filter: grayscale(100\\%);
-o-filter: grayscale(100\\%);
filter: progid:DXImageTransform.Microsoft.BasicImage(grayscale=1);
-webkit-filter: grayscale(1);
```



### 允许在西文单词中换行

可防止数字和英文不换行

```
/* 允许在西文单词中换行 */
word-break: break-all;
```

https://developer.mozilla.org/zh-CN/docs/Web/CSS/word-break



### 多行文字文字中间出现不对齐

```css
word-break: break-all;
text-align: left;
```



### 文本两行 多余`...`隐藏

> 效果不是很理想 如果文字不够两行的话 兼容火狐的效果还是会留在右下角 谷歌的是没问题的 而且兼容火狐的背景色也是个问题

```css
.text-line-clame-2 \\{
	max-height: 55px;
	line-height: 30px;
	margin-top: -4px;
	position: relative;
	overflow: hidden;
	display: -webkit-box;
	word-break: break-all;
	white-space: pre-wrap;
	text-overflow: ellipsis;
	-webkit-line-clamp: 2;
	-webkit-box-orient: vertical;
\\}
/*火狐兼容效果*/
@-moz-document url-prefix() \\{ 
	.text-line-clame-2:after \\{
		background: linear-gradient(to right, rgba(255, 255, 255, 0), #FFFFFF 50\\%) repeat scroll 0 0 rgba(0, 0, 0, 0);
		bottom: 0;
		content: "...";
		padding: 0 5px 1px 30px;
		position: absolute;
		right: 0;
	\\}
\\}
```



### 宽高相等间距相等的盒子 一般用来展示图片

```scss
.img-contain\\{
	overflow: hidden;
	padding: 0;
	.item\\{
		box-sizing: border-box;
		position: relative;
		display: block;
		float: left;
		width: 9.5\\%;
		height: 0;
		padding-bottom: 9.1\\%;
		margin: 0.25\\%;
		cursor: pointer;
		border: 2px solid #a3b0b7;
		&.delete img\\{
			display: block;
			position: absolute;
			bottom: 0;
			width: 100\\%;
			height: 100\\%;
		\\}
		.contain\\{
			box-sizing: border-box;
			width: 100\\%;
			height: 100\\%;
			padding-bottom: 100\\%;
		\\}
	\\}
\\}
```



### input输入框样式

```
input \\{
    font-size: 16px;
\\}
input::placeholder \\{
    font-size: 16px;
    color: #9ea7b4;
\\}
```



### css样式子元素相对父级元素定位

父级元素 样式设置：

```html
position:relative;
```

子元素样式：

```html
position: absolute;
```

这样就可以达到子元素相对父级元素定位了。



### CSS中class的"."连着写的含义

在使用css的class属性中，我们写的最多的就是一个class 后面有多个属性值连接在一起，然后映射到具体的样式中去，

例子：.btn .btn-one .btn-two  

解释：

       举例如下：
       <a class="btn btn-one btn-two">123</a>
       各自写各自的样式：
        .btn\\{...\\}
        .btn-one\\{....\\}
        .btn-two\\{....\\}
        理解如下：在a标签上有各自的样式，后面的样式覆盖前面的，各自也保留各自独特的样式
        口诀：求同存异－－同留异留－－后浪推前浪

但是还有一种情况是class单独写的时候全部连接在一起，这又是什么意思呢？

例子：.btn.btn-one.btn-two

解释：

       举例如下：
       <a class="btn btn-one btn-two">123</a>
       .btn.btn-one.btn-two\\{.....\\}
       满足这几个class都存在的，都作用在同一个标签上的时候使用这个样式。
       口诀：同生死共存亡，缺一不可。

```
<head>
	<style type="text/css">
		.c1
		\\{
			color:#ff0000;
		\\}
		.c2
		\\{
			font-style:italic;
		\\}
		.c1.c2
		\\{
			text-decoration:underline;
		\\}
	</style>
	</head><body>
	<p class="c1">这里是红色</p>
	<p class="c2">这里是斜体</p>
	<p class="c1 c2">这里是红色、斜体、下划线</p>
</body>
```

.c1.c2 表示如果一个标签中同时使用了这两个类（不论顺序、不论是否还有其他类），则响应此样式规则。



### &.是什么意思

```
.tips-count \\{
    &.checked \\{
    	color: $themeColor;
    \\}
\\}
```

在 CSS 或预处理器（如 Sass、Less）中，`&` 符号用于指代父选择器。当你在嵌套规则中使用 `&` 时，它会将当前的选择器与 `&` 后面的部分连接起来，形成一个新的选择器。

在你的例子中：

```css
.tips-count \\{
  &.checked \\{
    color: $themeColor;
  \\}
\\}
```

这里的 `&.checked` 意味着 `.tips-count.checked`。也就是说，这段代码会被编译成或解释为：

```css
.tips-count.checked \\{
  color: $themeColor;
\\}
```

这表示只有当一个元素同时具有类 `.tips-count` 和 `.checked` 时，该样式才会被应用。这种写法在处理复杂的样式规则时特别有用，因为它使得代码更加简洁和易于维护。

例如，如果你有以下 HTML 结构：

```html
<div class="tips-count checked">...</div>
```

那么上述的 CSS 规则将会把文本颜色设置为 `$themeColor` 所定义的颜色。如果 `$themeColor` 是一个变量（比如在 Sass 中），它的值会在编译时被替换为实际的颜色值。



### 列表在pc宽度740px显示4列，中等尺寸屏幕显示3列，移动端显示2列，写出样式布局

```
	// 内容列表
    @media (max-width: 559px) \\{
      // 移动端，每行两个元素
      .list-box \\{
        grid-template-columns: repeat(auto-fill, minmax(calc(50\\% - 15px), 1fr));
      \\}
    \\}
    @media (min-width: 560px) and (max-width: 739px) \\{
      // 中等尺寸屏幕，每行三个元素
      .list-box \\{
        grid-template-columns: repeat(3, 1fr);
      \\}
    \\}
    @media (min-width: 740px) \\{
      // PC端，每行四个元素
      .list-box \\{
        grid-template-columns: repeat(4, 1fr);
      \\}
    \\}
    .list-box \\{
      padding: 15px;
      display: grid;
      gap: 15px; // 设置每项之间的间距
      overflow: hidden;
      .list-item \\{
        border-radius: 10px;
        overflow: hidden;
 		cursor: pointer;
        box-shadow: 0px 2px 4px 0px rgba(0, 0, 0, 0.1);
      \\}
    \\}
```



### vant搜索组件图标偶尔乱码

Vant 是一套移动端的 Vue 组件库，它提供了一系列丰富的组件来帮助开发者快速构建移动应用。如果你遇到了 Vant 搜索组件图标偶尔乱码的问题，这可能是由以下几个常见原因导致的：

1. **字体图标文件加载问题**：
   - 确保你的项目正确引入了 Vant 的 CSS 文件，这些文件中包含了图标字体的路径。
   - 检查网络请求，确保没有 404 错误或者其他阻止图标字体文件加载的问题。

2. **缓存问题**：
   - 浏览器缓存可能会导致旧版本的 CSS 或者图标字体文件被使用。尝试清除浏览器缓存或进行无缓存刷新（通常是在刷新页面时按住 `Ctrl` 键和 `Shift` 键）。

3. **跨域问题**：
   - 如果图标字体文件是从不同的域名加载的，确保服务器端设置了正确的 CORS（跨源资源共享）头信息。

4. **字体图标编码问题**：
   - 确认网页使用的字符编码是 UTF-8，因为这是支持显示所有语言和符号的标准编码格式。

5. **CSS 样式冲突**：
   - 检查是否有其他 CSS 样式覆盖或者干扰了 Vant 图标的样式，比如 font-family 属性可能被更改，影响到图标字体的正常显示。

6. **Vue 版本或 Vant 版本兼容性**：
   - 确认你正在使用的 Vue 和 Vant 的版本是兼容的，并且是最新版本，以避免已知的 bug。

7. **浏览器兼容性**：
   - 某些较老的浏览器可能不完全支持某些特性。确认你的应用是否在最新的主流浏览器中测试过。

为了更准确地诊断问题，请提供更多的上下文信息，例如代码片段、错误日志或截图等。如果你可以给出更具体的细节，我将能够提供更加针对性的帮助。

#### outputStyle: 'expanded',为什么可以解决图标偶现乱码的情况 

在某些情况下，图标可能会出现乱码，这是由于 CSS 或字体文件的渲染问题引起的。`outputStyle: 'expanded'` 是 Sass 编译器中的一种配置选项，它决定了 CSS 文件的输出格式。具体来说，`expanded` 格式将生成更加冗长、详细的 CSS 文件，而不是默认的压缩格式。

这种设置可能间接解决图标偶现乱码的原因如下：

1. **增加了 CSS 可读性**：`expanded` 输出的 CSS 文件包含了更多的空格和注释，使得 CSS 规则更加清晰。这有助于在开发过程中更容易定位和解决潜在的渲染问题。
2. **改进了字体加载的顺序**：有时候，在压缩后的文件中，某些资源的加载顺序可能会出现问题，导致图标字体未能正确加载。通过使用 `expanded` 输出格式，可能会改善 CSS 文件的结构和资源的加载顺序，从而减少这种问题。
3. **防止 CSS 合并错误**：在压缩过程中，CSS 文件可能会被过度合并或优化，导致某些规则丢失或顺序出错。使用 `expanded` 输出格式时，这些合并优化减少，可能有效防止这类错误，尤其是在字体图标的应用上。

总的来说，`outputStyle: 'expanded'` 通过增加可读性和改善 CSS 文件的结构，可能帮助避免图标加载时出现的偶现乱码问题。



### 原先vite配置是这样的，加一个outputStyle: 'expanded',有什么影响？可以加吗

```
css: \\{
    preprocessorOptions: \\{
      scss: \\{
        additionalData: `@use "@/assets/styles/element/index.scss" as *;`,
      \\},
    \\},
  \\},
```

在你提供的 Vite 配置中，`additionalData` 用于在每个 SCSS 文件的开头自动注入共享的 SCSS 变量或样式文件，这对于模块化和全局样式的引用非常有用。你提到想要添加 `outputStyle: 'expanded'`，让我们看看加上这个配置后的影响和可行性。

#### 影响：

1. **SCSS 编译风格**： `outputStyle: 'expanded'` 是 Sass 编译器的选项，用来指定输出的 CSS 格式。`expanded` 代表生成未压缩的、可读性较强的 CSS，通常带有额外的换行和空格。相比之下，默认的 `compressed` 会生成一行代码的紧凑格式。
2. **影响开发模式和构建模式**：
   - 在开发模式下，`expanded` 输出格式通常可以帮助调试，因为生成的 CSS 文件更为清晰，容易查找和修改样式。
   - 在生产环境中，`expanded` 输出的 CSS 文件会更大，因此通常使用 `compressed` 格式以减少文件大小，提高加载性能。如果你将其设置为 `expanded`，这可能会影响到生产构建的性能和文件大小。
3. **文件体积增加**： 使用 `expanded` 输出格式时，CSS 文件中的每条规则将占用更多行和空格。对于大型项目，这可能会导致输出的 CSS 文件较大，增加加载时间，特别是在生产环境中。
4. **调试友好**： 对于开发时的调试，`expanded` 格式非常有帮助，因为它能使得你更容易追踪样式问题。但对于生产环境来说，通常更推荐使用 `compressed`，以保持较小的文件体积。

#### 是否可以加：

可以加 `outputStyle: 'expanded'`，但请注意它的作用是在 SCSS 文件编译时影响输出的 CSS 样式格式。如果你是在开发环境中使用这个设置，它应该不会有太大问题，但如果是生产环境，你可能会希望使用 `compressed` 来减小 CSS 文件的大小，从而提高页面加载速度。

总的来说，添加 `outputStyle: 'expanded'` 是可以的，只需要确保在合适的环境下使用，避免在生产环境中影响性能。



### 适配iphone底部安全区

```
 <!-- 底部固定栏 -->
 <div class="footer">
```

为了适配 iPhone 的底部安全区（特别是带有 Home Indicator 的机型，如 iPhone X 及更新的型号），你可以使用 CSS 和 Vue 3 来创建一个响应式的底部固定栏。以下是一个简单的实现方法：

1. **确保使用正确的视口设置**：在 HTML 文档的 `<head>` 中包含正确的 viewport 标签，以确保页面正确缩放。

```html
<meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
```

2. **利用 CSS 环境变量和常量**：现代浏览器（包括 Safari）提供了环境变量 `safe-area-inset-bottom`，它可以根据设备的安全区域自动调整值。

3. **编写 CSS 样式**：为你的 `.footer` 类添加样式，以保证它能适应 iPhone 的底部安全区。

```css
.footer \\{
    position: fixed;
    left: 0;
    bottom: 0;
    width: 100\\%;
    padding-bottom: constant(safe-area-inset-bottom); /* 兼容 iOS 11.0 - 11.2 */
    padding-bottom: env(safe-area-inset-bottom); /* 兼容 iOS 11.2+ */
    background-color: #f8f9fa; /* 设置背景颜色 */
    text-align: center; /* 根据需要调整 */
\\}
```

4. **Vue 组件**：如果你是用 Vue 3 创建组件，可以将上述 CSS 放置在组件的 `<style>` 标签中，或者作为一个全局样式文件的一部分。然后，在模板部分定义你的 footer 结构。

```vue
<template>
  <div class="footer">
    <!-- Footer 内容 -->
  </div>
</template>

<script setup>
// 这里可以放置脚本逻辑，如果有的话。
</script>

<style scoped>
/* 这里放置上面提到的 .footer CSS 样式 */
</style>
```

5. **测试和调整**：确保你在实际的 iPhone 设备或模拟器上测试你的网站，因为不同的屏幕尺寸和方向可能会影响最终的显示效果。

请记得，CSS 的 `constant()` 函数是为早期版本的 Safari 浏览器准备的，对于较新的版本应该使用 `env()` 函数。随着浏览器的更新，你可能只需要保留 `env()`。



### css卡片右上角加一个上底朝向右上角，两边和卡片对齐的等腰梯形hot角标

要在 CSS 卡片的右上角加一个等腰梯形的角标，可以使用 `::before` 或 `::after` 伪元素来实现。这里使用一个简单的例子来展示如何为卡片右上角添加一个上底朝向右上角的等腰梯形标志。

```
html<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>CSS Card with Hot Label</title>
  <style>
    .card \\{
      position: relative;
      width: 150px;
      height: 230px;
      background-color: #f1f1f1;
      border-radius: 10px;
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
      padding: 20px;
    \\}

    .card .hot-label \\{
      position: absolute;
      top: 15px;
      right: 15px;
      // width: 0;
      height: 0;
      border-left: 20px solid transparent;
      border-right: 20px solid transparent;
      border-bottom: 20px solid #ff3333; /* Hot color */
      content: 'HOT';
      color: white;
      font-weight: bold;
      font-size: 14px;
      text-align: center;
      line-height: 40px;
      transform: translate(50\\%, -50\\%) rotate(45deg);
      padding: 10px 16px;
    \\}
  </style>
</head>
<body>
  <div class="card">
    <div class="hot-label">HOT</div>
  </div>
</body>
</html>
```

### 解释：

1. `.card`：这是卡片的样式，设置了宽度、高度、背景色和边框圆角等。
2. `.hot-label`：这是右上角的标签，使用 `position: absolute` 将它定位在卡片的右上角。通过调整 `top` 和 `right` 为 `0` 将它放置在卡片的右上角。
3. 使用 `border-left` 和 `border-right` 来形成梯形的两边，`border-bottom` 用来创建梯形的底部部分。
4. `rotate(45deg)` 将文本旋转 45 度，使其呈现正确的方向。
5. 标签文字 `"HOT"` 使用了 `content` 属性和 `line-height` 来居中对齐。

通过这个代码，你可以在卡片的右上角看到一个等腰梯形的 `HOT` 角标。



### 颜色变量使用

```
<div class="tags"
  v-if="info.tags">
  <div class="tag"
	v-for="(item, index) in info.tags"
	:key="index"
	:style="\\{ '--color': item.color, '--bgColor':item.bgColor \\}">\\\{\\\{ item.content\\\}\\\} }}</div>
</div>

  // 标签
  .tags \\{
    padding: 0 15px 8px;
    display: flex;
    align-items: center;
    flex-wrap: wrap;
    .tag \\{
      line-height: 24px;
      padding: 0 11px;
      margin: 0 16px 12px 0;
      border-radius: 2px;
      font-size: 12px;
      color: var(--color);
      background: var(--bgColor);
    \\}
  \\}
```



### 每个按钮有两层颜色，下边颜色是底色， 上边还有一层黑白渐变是不透明度35\\%

```
	.confirm \\{
        color: #fff;
        background: linear-gradient(
            to bottom right,
            rgba(0, 0, 0, 0.03),
            rgba(255, 255, 255, 0.35)
          ),
          #267ef0;
      \\}
      .reset \\{
        color: #8692a6;
        background: linear-gradient(
            to bottom right,
            rgba(0, 0, 0, 0.03),
            rgba(255, 255, 255, 0.35)
          ),
          #ebecf0;
      \\}
```



### 两个vue3文件，都有一大段公共的css，但其中某些样式稍微不同，怎么复用

```
.list-card \\{
    // 卡片标题
    .card-title \\{
  .search \\{.select-list \\{
```

在处理两个Vue3组件中重复的CSS结构时，可以采用以下方法实现样式复用并允许差异化定制：

方法一：使用Sass/Less的Mixin（推荐）

1. 创建共享Mixin文件（如 `shared.scss`）：

   ```scss
   @mixin list-card-base \\{
     .list-card \\{
       .card-title \\{
         font-size: 16px;
         // 其他公共样式
       \\}
       .search \\{
         margin: 10px;
         .select-list \\{
           padding: 8px;
           border: 1px solid #ccc;
           // 其他公共样式
         \\}
       \\}
     \\}
   \\}
   ```

2. 在组件中引用并扩展：

   ```vue
   <!-- 组件A -->
   <style lang="scss" scoped>
   @import '@/styles/shared.scss';
   
   @include list-card-base;
   
   .search .select-list \\{
     background-color: red;
     width: 200px;
   \\}
   </style>
   ```

   ```vue
   <!-- 组件B -->
   <style lang="scss" scoped>
   @import '@/styles/shared.scss';
   
   @include list-card-base;
   
   .search .select-list \\{
     background-color: blue;
     width: 300px;
   \\}
   </style>
   ```

方法二：使用CSS变量（纯CSS方案）

1. 定义全局公共样式（如 `global.css`）：

   ```css
   .list-card \\{
     --select-list-bg: #fff; /* 默认值 */
     --select-list-width: 200px;
   
     .search .select-list \\{
       background: var(--select-list-bg);
       width: var(--select-list-width);
       padding: 8px;
       border: 1px solid #ccc;
     \\}
   \\}
   ```

2. 在组件中覆盖变量：

   ```vue
   <!-- 组件A -->
   <template>
     <div class="list-card">
       <!-- 内容 -->
     </div>
   </template>
   
   <style scoped>
   .list-card \\{
     --select-list-bg: red;
     --select-list-width: 250px;
   \\}
   </style>
   ```

   ```vue
   <!-- 组件B -->
   <style scoped>
   .list-card \\{
     --select-list-bg: blue;
     --select-list-width: 300px;
   \\}
   </style>
   ```

方案选择建议
• Sass/Less Mixin：适合复杂结构、多层级嵌套且有条件样式的场景，需预处理器支持。

• CSS变量：适合简单主题定制或尺寸调整，无需构建工具，浏览器原生支持。


两种方案均能有效复用样式并实现差异化，根据项目技术栈选择最合适的方式。
