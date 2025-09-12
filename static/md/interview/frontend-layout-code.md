---
title: 前端布局代码
date: 2021-01-18 18:36:27
categories: 
- 前端面试
tags:
- HTML
- CSS
- 页面布局
---

### 左右居中

- 行内元素: `text-align: center`
- 定宽块状元素: 左右 `margin` 值为 `auto`
- 不定宽块状元素: `table`布局，`position + transform`

```css
/* 方案1 */
.wrap \\{
  text-align: center
\\}
.center \\{
  display: inline;
  /* or */
  /* display: inline-block; */
\\}
/* 方案2 */
.center \\{
  width: 100px;
  margin: 0 auto;
\\}
/* 方案2 */
.wrap \\{
  position: relative;
\\}
.center \\{
  position: absulote;
  left: 50\\%;
  transform: translateX(-50\\%);
\\}
```



###  上下垂直居中

- 定高：`margin`，`position + margin`(负值)
- 不定高：`position` + `transform`，`flex`，`IFC + vertical-align:middle`

```css
/* 定高方案1 */
.center \\{
  height: 100px;
  margin: 50px 0;   
\\}
/* 定高方案2 */
.center \\{
  height: 100px;
  position: absolute;
  top: 50\\%;
  margin-top: -25px;
\\}
/* 不定高方案1 */
.center \\{
  position: absolute;
  top: 50\\%;
  transform: translateY(-50\\%);
\\}
/* 不定高方案2 */
.wrap \\{
  display: flex;
  align-items: center;
\\}
.center \\{
  width: 100\\%;
\\}
/* 不定高方案3 */
/* 设置 inline-block 则会在外层产生 IFC，高度设为 100\\% 撑开 wrap 的高度 */
.wrap::before \\{
  content: '';
  height: 100\\%;
  display: inline-block;
  vertical-align: middle;
\\}
.wrap \\{
  text-align: center;
\\}
.center \\{
  display: inline-block;  
  vertical-align: middle;
\\}
```



### 如何居中div？如何居中一个浮动元素？如何让绝对定位的div居中？

- 给`div`设置一个宽度，然后添加`margin:0 auto`属性

```
div\\{
    width:200px;
    margin:0 auto;
 \\}
```

- 居中一个浮动元素

```
//确定容器的宽高 宽500 高 300 的层
//设置层的外边距

 .div \\{
      width:500px ; height:300px;//高度可以不设
      margin: -150px 0 0 -250px;
      position:relative;         //相对定位
      background-color:pink;     //方便看效果
      left:50\\%;
      top:50\\%;
 \\}
```

- 让绝对定位的div居中

```
  position: absolute;
  width: 1200px;
  background: none;
  margin: 0 auto;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
```



### 垂直居中一个浮动元素？

已知高度：

```
.son\\{
background-color:#ff0000;
width:200px;
height:200px;
position:absolute;
top:50\\%;
left:50\\%;
margin-left:-100px;
margin-top:-100px;
\\}
```

未知高度：

```
.son\\{
width: 200px;
height: 200px;
background-color: #ff0000;
margin:auto;
position: absolute;
left: 0;
top: 0;
right: 0;
bottom: 0;
\\}
```

css3方法未知宽高

```
.father\\{
display:flex;
justify-content:center;
align-items:center;
\\}
```

(详解c3div水平垂直居中：[http://www.cnblogs.com/shenxiaolin/p/5387623.html](https://link.jianshu.com/?t=http://www.cnblogs.com/shenxiaolin/p/5387623.html))

```css
    如何垂直居中一个<img>？
    第一种：
    .father\\{
            display:table-cell;                
            text-align:center;
            vertical-align:middle;
    \\}
    第二种：
    .father\\{
            height: 1000px;
            width: 1000px;
            text-align: center;
            margin: 0 auto;
            line-height: 1000px;
    \\}
    .img\\{
            vertical-align: middle;
    \\}

```



### 如何垂直居中一个元素？

方法一：绝对定位居中（原始版之已知元素的高宽）

```css
.content \\{
  width: 200px;
  height: 200px;
  background-color: #6699ff;
  position: absolute; /*父元素需要相对定位*/
  top: 50\\%;
  left: 50\\%;
  margin-top: -100px; /*设为高度的1/2*/
  margin-left: -100px; /*设为宽度的1/2*/
\\}
```

方法二：绝对定位居中（改进版之一未知元素的高宽）

```css
.content \\{
  width: 200px;
  height: 200px;
  background-color: #6699ff;
  position: absolute; /*父元素需要相对定位*/
  top: 50\\%;
  left: 50\\%;
  transform: translate(-50\\%, -50\\%); /*在水平和垂直方向上各偏移-50\\%*/
\\}
```

方法三：绝对定位居中（改进版之二未知元素的高宽）

```css
.content \\{
  width: 200px;
  height: 200px;
  background-color: #6699ff;
  margin: auto; /*很关键的一步*/
  position: absolute; /*父元素需要相对定位*/
  left: 0;
  top: 0;
  right: 0;
  bottom: 0; /*让四个定位属性都为0*/
\\}
```

方法四：flex 布局居中

```css
body \\{
  display: flex; /*设置外层盒子display为flex*/
  align-items: center; /*设置内层盒子的垂直居中*/
  justify-content: center; /*设置内层盒子的水平居中*/
  .content \\{
    width: 200px;
    height: 200px;
    background-color: #6699ff;
  \\}
\\}
```

那么问题来了，如何垂直居中一个 img（用更简便的方法。）

```css
.content \\{
  //img的容器设置如下
  display: table-cell;
  text-align: center;
  vertical-align: middle;
\\}
```



### 如何居中div？

- 水平居中：给div设置一个宽度，然后添加margin:0 auto属性

```
div\\{
	width:200px;
	margin:0 auto;
 \\}
```

- 让绝对定位的div居中

```
div \\{
	position: absolute;
	width: 300px;
	height: 300px;
	margin: auto;
	top: 0;
	left: 0;
	bottom: 0;
	right: 0;
	background-color: pink;	/* 方便看效果 */
\\}
```

- 水平垂直居中一
  - 确定容器的宽高 宽500 高 300 的层
  - 设置层的外边距

```
div \\{
	position: relative;		/* 相对定位或绝对定位均可 */
	width:500px;
	height:300px;
	top: 50\\%;
	left: 50\\%;
	margin: -150px 0 0 -250px;     	/* 外边距为自身宽高的一半 */
	background-color: pink;	 	/* 方便看效果 */

 \\}
```

- 水平垂直居中二
  - 未知容器的宽高，利用 `transform` 属性

```
div \\{
	position: absolute;		/* 相对定位或绝对定位均可 */
	width:500px;
	height:300px;
	top: 50\\%;
	left: 50\\%;
	transform: translate(-50\\%, -50\\%);
	background-color: pink;	 	/* 方便看效果 */

\\}
```

- 水平垂直居中三
  - 利用 flex 布局
  - 实际使用时应考虑兼容性

```
.container \\{
	display: flex;
	align-items: center; 		/* 垂直居中 */
	justify-content: center;	/* 水平居中 */

\\}
.container div \\{
	width: 100px;
	height: 100px;
	background-color: pink;		/* 方便看效果 */
\\}  

```



### css垂直居中的方法有哪些？

- 如果是单行文本, line-height 设置成和 height 值

```
.vertical \\{
      height: 100px;
      line-height: 100px;
    \\}

```

- 已知高度的块级子元素，采用绝对定位和负边距

```
.container \\{
  position: relative;
\\}
.vertical \\{
  height: 300px;  /*子元素高度*/
  position: absolute;
  top:50\\%;  /*父元素高度50\\%*/
  margin-top: -150px; /*自身高度一半*/
\\}

```

- 未知高度的块级父子元素居中，模拟表格布局
- 缺点：IE67不兼容，父级 overflow：hidden 失效

```
.container \\{
      display: table;
    \\}
    .content \\{
      display: table-cell;
      vertical-align: middle;
    \\}


```

- 新增 inline-block 兄弟元素，设置 vertical-align
  - 缺点：需要增加额外标签，IE67不兼容

```
.container \\{
  height: 100\\%;/*定义父级高度，作为参考*/
\\}
.extra .vertical\\{
  display: inline-block;  /*行内块显示*/
  vertical-align: middle; /*垂直居中*/
\\}
.extra \\{
  height: 100\\%; /*设置新增元素高度为100\\%*/
\\}

```

- 绝对定位配合 CSS3 位移

```
.vertical \\{
  position: absolute;
  top:50\\%;  /*父元素高度50\\%*/
  transform:translateY(-50\\%, -50\\%);
\\}

```

- CSS3弹性盒模型

```
.container \\{
  display:flex;
  justify-content: center; /*子元素水平居中*/
  align-items: center; /*子元素垂直居中*/
\\}

```



### 圣杯布局的实现原理？

- 要求：三列布局；中间主体内容前置，且宽度自适应；两边内容定宽
  - 好处：重要的内容放在文档流前面可以优先渲染
  - 原理：利用相对定位、浮动、负边距布局，而不添加额外标签

```css
  .container \\{
      padding-left: 150px;
      padding-right: 190px;
  \\}
  .main \\{
      float: left;
      width: 100\\%;
  \\}
  .left \\{
      float: left;
      width: 190px;
      margin-left: -100\\%;
      position: relative;
      left: -150px;
  \\}
  .right \\{
      float: left;
      width: 190px;
      margin-left: -190px;
      position: relative;
      right: -190px;
  \\}

```



### 什么是双飞翼布局？实现原理？

- 双飞翼布局：对圣杯布局（使用相对定位，对以后布局有局限性）的改进，消除相对定位布局
- 原理：主体元素上设置左右边距，预留两翼位置。左右两栏使用浮动和负边距归位，消除相对定位。

```css
.container \\{
    /*padding-left:150px;*/
    /*padding-right:190px;*/
\\}
.main-wrap \\{
    width: 100\\%;
    float: left;
\\}
.main \\{
    margin-left: 150px;
    margin-right: 190px;
\\}
.left \\{
    float: left;
    width: 150px;
    margin-left: -100\\%;
    /*position: relative;*/
    /*left:-150px;*/
\\}
.right \\{
    float: left;
    width: 190px;
    margin-left: -190px;
    /*position:relative;*/
    /*right:-190px;*/
\\}

```



### 左边定宽，右边自适应方案：float + margin，float + calc

```css
/* 方案1 */ 
.left \\{
  width: 120px;
  float: left;
\\}
.right \\{
  margin-left: 120px;
\\}
/* 方案2 */ 
.left \\{
  width: 120px;
  float: left;
\\}
.right \\{
  width: calc(100\\% - 120px);
  float: left;
\\}

```



### 左右两边定宽，中间自适应：float，float + calc, 圣杯布局（设置BFC，margin负值法），flex

```css
.wrap \\{
  width: 100\\%;
  height: 200px;
\\}
.wrap > div \\{
  height: 100\\%;
\\}
/* 方案1 */
.left \\{
  width: 120px;
  float: left;
\\}
.right \\{
  float: right;
  width: 120px;
\\}
.center \\{
  margin: 0 120px; 
\\}
/* 方案2 */
.left \\{
  width: 120px;
  float: left;
\\}
.right \\{
  float: right;
  width: 120px;
\\}
.center \\{
  width: calc(100\\% - 240px);
  margin-left: 120px;
\\}
/* 方案3 */
.wrap \\{
  display: flex;
\\}
.left \\{
  width: 120px;
\\}
.right \\{
  width: 120px;
\\}
.center \\{
  flex: 1;
\\}

```



### 一边固定宽度一边宽度自适应

可以使用 flex 布局 复制下面的 HTML 和 CSS 代码 用浏览器打开可以看到效果

```
<div class="wrap">
  <div class="div1"></div>
  <div class="div2"></div>
</div>

.wrap \\{
  display: flex;
  justify-content: space-between;
\\}
.div1 \\{
  min-width: 200px;
\\}
.div2 \\{
  width: 100\\%;
  background: #e6e6e6;
\\}
html,
body,
div \\{
  height: 100\\%;
  margin: 0;
\\}

```



### 描述下 CSS3 里实现元素动画的方法

1. 创建动画：@keyframes 规则

方式一：from\\{属性：值;\\} to\\{属性：值;\\}

```css
@keyframes myflash \\{
  from \\{
    width: 200px;
    height: 200px;
  \\}
  to \\{
    position: relative;
    left: 50px;
    transform: rotate(360deg);
  \\}
\\}

```

方式二：0\\%\\{属性：值;\\} 100\\%\\{属性：值;\\}
0\\% 是动画的开始，100\\% 是动画的完成。可以在二者之间加入 25\\%，50\\%等

```css
@keyframes myflash \\{
  0\\% \\{
    background: red;
  \\}
  50\\% \\{
    background: yellow;
  \\}
  75\\% \\{
    background: green;
  \\}
  100\\% \\{
    background: blue;
  \\}
\\}

```

2. 将动画绑定到选择器

在样式中，设置动画属性 animation，自定义动画名称和时长。

animation：动画名 时长；

此时就可以完成一个简单的动画了，要进行更多设置还需要其他属性。

```css
#first \\{
  animation: myflash 10s;
  animation-delay: 2s;
  animation-iteration-count: 2;
  animation-timing-function: ease-in;
\\}

```



### 如何用css实现瀑布流布局

利用column-count和break-inside这两个CSS3属性即可，复制如下代码即可察看效果

```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <style>
        body \\{
            margin: 0;
        \\}
        .waterfall-container \\{
            /*分几列*/
            column-count: 2;
            width: 100\\%;
            /* 列间距 */
            column-gap: 10px;
        \\}

        .waterfall-item \\{
            break-inside: avoid;
            width: 100\\%;
            height: 100px;
            margin-bottom: 10px;
            background: #ddd;
            column-gap: 0;
            text-align: center;
            color: #fff;
            font-size: 40px;
        \\}
    </style>
</head>
<body>
    <div class="waterfall-container">
        <div class="waterfall-item" style="height: 100px">1</div>
        <div class="waterfall-item" style="height: 300px">2</div>
        <div class="waterfall-item" style="height: 400px">3</div>
        <div class="waterfall-item" style="height: 100px">4</div>
        <div class="waterfall-item" style="height: 300px">5</div>
        <div class="waterfall-item" style="height: 600px">6</div>
        <div class="waterfall-item" style="height: 400px">7</div>
        <div class="waterfall-item" style="height: 300px">8</div>
        <div class="waterfall-item" style="height: 700px">9</div>
        <div class="waterfall-item" style="height: 100px">10</div>
    </div>
</body>
</html>

```



### 已知父级盒子的宽高，子级img宽高未知，想让img铺满父级盒子且图片不能变形

需要用到`css`的`object-fit`属性

```css
div \\{
    width: 200px;
    height: 200px;
\\}
img \\{
    object-fit: cover;
    width: 100\\%;
    height: 100\\%;
\\}

```



### 页面布局：假设高度默认`100px` ，请写出三栏布局，其中左栏、右栏各为`300px`，中间自适应。

![](http://img.smyhvae.com/20180305_1520.png)

分析：

初学者想到的答案有两种：

- 方法1：浮动
- 方法2：绝对定位

> 但要求你能至少写出三四种方法，才算及格。剩下的方法如下：

- 方法3：`flexbox`。移动开发里经常用到。
- 方法4：表格布局` table`。虽然已经淘汰了，但也应该了解。
- 方法5：网格布局 `grid`

**方法1、浮动：**

> 左侧设置左浮动，右侧设置右浮动即可，中间会自动地自适应。

**方法2、绝对定位：**

> 左侧设置为绝对定位， ` left：0px`。右侧设置为绝对定位， `right：0px`。中间设置为绝对定位，`left `和`right` 都为`300px`，即可。中间的宽度会自适应。

> 使用`article`标签作为容器，包裹左、中、右三个部分。

> 方法1 和方法2 的代码如下：

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        html * \\{
            padding: 0px;
            margin: 0px;
        \\}

        .layout \\{
            margin-bottom: 150px;
        \\}


        .layout article div \\{ /*注意，这里是设置每个小块儿的高度为100px，而不是设置大容器的高度。大容器的高度要符合响应式*/
            height: 100px;
        \\}

        /* 方法一 start */

        .layout.float .left \\{
            float: left;
            width: 300px;
            background: red;
        \\}

        .layout.float .right \\{
            float: right;
            width: 300px;
            background: blue;
        \\}

        .layout.float .center \\{
            background: green;

        \\}

        /* 方法一 end */


        /* 方法二 start */
        .layout.absolute .left-center-right \\{
            position: relative;
        \\}

        .layout.absolute .left \\{
            position: absolute;
            left: 0;
            width: 300px;
            background: red;
        \\}

        /* 【重要】中间的区域，左侧定位300px，右侧定位为300px，即可完成。宽度会自使用 */
        .layout.absolute .center \\{
            position: absolute;
            left: 300px;
            right: 300px;
            background: green;
        \\}

        .layout.absolute .right \\{
            position: absolute;
            right: 0;
            width: 300px;
            background: blue;
        \\}


        /* 方法二 end */
    </style>
</head>

<body>

    <!-- 方法一：浮动 start -->
    <!-- 输入 section.layout.float，即可生成  -->
    <section class="layout float">
        <!-- 用  article 标签包裹左、中、右三个部分 -->
        <article class="left-right-center">
            <!-- 输入 div.left+div.right+div.center，即可生成 -->
            <div class="left">
                我是 left
            </div>
            <div class="right">
                我是 right
            </div>
            <div class="center">
                浮动解决方案
                我是 center
            </div>

        </article>

    </section>
    <!-- 方法一：浮动 end -->

    <section class="layout absolute">
        <article class="left-center-right">
            <div class="left">
                我是 left
            </div>
            <div class="right">
                我是 right
            </div>
            <div class="center">
                <h1>绝对定位解决方案</h1>
                我是 center
            </div>
        </article>
    </section>
</body>
</html>

```

效果如下：

![](http://img.smyhvae.com/20180305_1640.gif)

**方法3、flexbox布局**

> 将左中右所在的容器设置为`display: flex`，设置两侧的宽度后，然后让中间的`flex = 1`，即可。

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        html * \\{
            padding: 0;
            margin: 0;
        \\}

        .layout article div \\{
            height: 100px;
        \\}

        .left-center-right \\{
            display: flex;
        \\}

        .layout.flex .left \\{
            width: 300px;
            background: red;
        \\}

        .layout.flex .center \\{
            flex: 1;
            background: green;
        \\}

        .layout.flex .right \\{
            width: 300px;
            background: blue;
        \\}
    </style>

</head>

<body>
    <section class="layout flex">
        <article class="left-center-right-">
            <div class="left">
                我是 left
            </div>
            <div class="center">
                <h1>flex布局解决方案</h1>
                我是 center
            </div>
            <div class="right">
                我是 right
            </div>

        </article>
    </section>

</body>

</html>


```

效果如下：

![](http://img.smyhvae.com/20180305_1700.gif)



**方法4、表格布局 table**

> 设置整个容器的宽度为`100\\%`，设置三个部分均为表格，然后左边的单元格为 `300px`，右边的单元格为 `300px`，即可。中间的单元格会自适应。

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        html * \\{
            padding: 0;
            margin: 0;
        \\}

        .layout.table div \\{
            height: 100px;
        \\}

        /* 重要：设置容器为表格布局，宽度为100\\% */
        .layout.table .left-center-right \\{
            width: 100\\%;
            display: table;
            height: 100px;

        \\}

        .layout.table .left-center-right div \\{
            display: table-cell; /* 重要：设置三个模块为表格里的单元*/
        \\}

        .layout.table .left \\{
            width: 300px;
            background: red;
        \\}

        .layout.table .center \\{
            background: green;
        \\}

        .layout.table .right \\{
            width: 300px;
            background: blue;
        \\}
    </style>

</head>

<body>
    <section class="layout table">
        <article class="left-center-right">
            <div class="left">
                我是 left
            </div>
            <div class="center">
                <h1>表格布局解决方案</h1>
                我是 center
            </div>
            <div class="right">
                我是 right
            </div>

        </article>
    </section>

</body>

</html>

```

![](http://img.smyhvae.com/20180305_1855.gif)

**方法5、网格布局 grid**

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        html * \\{
            padding: 0;
            margin: 0;
        \\}

        /* 重要：设置容器为网格布局，宽度为100\\% */
        .layout.grid .left-center-right \\{
            display: grid;
            width: 100\\%;
            grid-template-rows: 100px;
            grid-template-columns: 300px auto 300px;  /* 重要：设置网格为三列，并设置每列的宽度。即可。*/

        \\}

        .layout.grid .left \\{
            background: red;
        \\}

        .layout.grid .center \\{
            background: green;
        \\}

        .layout.grid .right \\{
            background: blue;
        \\}
    </style>

</head>

<body>
    <section class="layout grid">
        <article class="left-center-right">
            <div class="left">
                我是 left
            </div>
            <div class="center">
                <h1>网格布局解决方案</h1>
                我是 center
            </div>
            <div class="right">
                我是 right
            </div>

        </article>
    </section>

</body>

</html>
```

效果：

![](http://img.smyhvae.com/20180305_1920.gif)

**延伸：五种方法的对比**

> 五种方法的优缺点

- 考虑中间模块的高度问题
- 兼容性问题：实际开发中，哪个最实用？

方法1：浮动：

- 优点：兼容性好。
- 缺点：浮动会脱离标准文档流，因此要清除浮动。我们解决好这个问题即可。

方法:2：绝对定位

- 优点：快捷。
- 缺点：导致子元素也脱离了标准文档流，可实用性差。

方法3：flex 布局（CSS3中出现的）

- 优点：解决上面两个方法的不足，flex布局比较完美。移动端基本用 flex布局。

方法4：表格布局

- 优点：表格布局在很多场景中很实用，兼容性非常好。因为IE8不支持 flex，此时可以尝试表格布局
- 缺点：因为三个部分都当成了**单元格**来对待，此时，如果中间的部分变高了，其会部分也会被迫调整高度。但是，在很多场景下，我们并不需要两侧的高度增高。

> 什么时候用 `flex `布局 or 表格布局，看具体的场景。二者没有绝对的优势，也没有绝对的不足。

方法5：网格布局

- CSS3中引入的布局，很好用。代码量简化了很多。

> PS：面试提到网格布局，说明我们对新技术是有追求的。

**延伸：如果题目中去掉高度已知**

> 问题：题目中，如果去掉高度已知，我们往中间的模块里塞很多内容，让中间的模块撑开。会发生什么变化？哪个布局就不能用了？

分析：其实可以这样理解，我们回去看上面的动画效果，当中间的模块变得很挤时，会发生什么效果？就是我们想要的答案。

> 答案是：**flex 布局和表格布局可以通用**，其他三个布局都不能用了。



**总结**

> 涉及到的知识点：

- 语义化掌握到位：每个区域用`section`、`article`代表容器、`div`代表块儿。如果通篇都用 div，那就是语义化没掌握好。
- 页面布局理解深刻。
- `CSS`基础知识扎实。
- 思维灵活且积极上进。题目中可以通过`网格布局`来体现。
- 代码书写规范。注意命名。上面的代码中，没有一行代码是多的。



### 六个元素分三行，右边长一点

 `.info-box`中的六个`.item`元素就会分成三行，其中偶数位置的`.item`占据54\\%的宽度，而奇数位置的`.item`占据46\\%的宽度。 

```
<div class="info-box">
  <div class="item">Odd Item 1</div>
  <div class="item">Even Item 1</div>
  <div class="item">Odd Item 2</div>
  <div class="item">Even Item 2</div>
  <div class="item">Odd Item 3</div>
  <div class="item">Even Item 3</div>
</div>
```

```
.info-box \\{
  display: grid; // 启用CSS Grid布局
  grid-template-columns: 46\\% 54\\%; // 定义两列的宽度
  gap: 1rem; // 添加间距

  .item \\{
    // 每个.item占据一个单元格
    // 其他样式
  \\}
\\}
```

