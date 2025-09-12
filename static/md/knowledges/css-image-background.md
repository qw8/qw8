---
title: CSS图片背景
date: 2020-08-31 22:30:10
categories: 
- 前端知识
tags:
- CSS
---

### 解决img标签下边距的问题

> 问题描述：如果img标签下跟一个块级标签，那么两者之间会出现一条缝隙。
>
> 原因：原因是行级标签具有自身的定位，图片默认的垂直对齐方式是基线(vertical-align: baseline)

解决方案1：

将图片转成块级元素即可(display: block)。

解决方案2：

更改图片的对齐方式为top

```
vertical-align: top;
```



### 图片元素的垂直对齐方式

对于 inline 元素和 table-cell 元素，标准模式下 vertical-align 属性默认取值是 baseline

在怪异模式下，table 单元格中的图片的 vertical-align 属性默认取值是 bottom。

因此在图片底部会有及像素的空间。



### img标签自动裁剪

```
.image-container \\{
  width: 200px; /* 容器宽度 */
  height: 200px; /* 容器高度 */
  overflow: hidden; /* 隐藏超出容器的图片部分 */
\\}

.image-container img \\{
  width: 100\\%; /* 图片宽度为容器宽度的100\\% */
  height: 100\\%; /* 图片高度为容器高度的100\\% */
  object-fit: cover; /* 自动裁剪图片以填充容器 */
  object-position: center; /* 图片居中显示 */
\\}
```

在这个例子中，图片将被裁剪以适应 `.image-container` 的尺寸，同时保持图片的中心区域可见。`overflow: hidden;` 确保超出容器的图片部分被隐藏，不会出现滚动条。

通过调整 `object-position` 的值，你可以控制图片的哪一部分被显示在容器中。例如，使用 `object-position: 0\\% 50\\%;` 将显示图片的顶部中间部分。

[object-fit](https://developer.mozilla.org/zh-CN/docs/Web/CSS/object-fit) 属性由下列的值中的单独一个关键字来指定。

- `contain`

  被替换的内容将被缩放，以在填充元素的内容框时保持其宽高比。整个对象在填充盒子的同时保留其长宽比，因此如果宽高比与框的宽高比不匹配，该对象将被添加“[黑边](https://zh.wikipedia.org/wiki/黑邊)”。

- `cover`

  被替换的内容在保持其宽高比的同时填充元素的整个内容框。如果对象的宽高比与内容框不相匹配，该对象将被剪裁以适应内容框。

- `fill`

  被替换的内容正好填充元素的内容框。整个对象将完全填充此框。如果对象的宽高比与内容框不相匹配，那么该对象将被拉伸以适应内容框。

- `none`

  被替换的内容将保持其原有的尺寸。

- `scale-down`

  内容的尺寸与 `none` 或 `contain` 中的一个相同，取决于它们两个之间谁得到的对象尺寸会更小一些。

#### 确保图片的上部总是可见

如果你想要在使用 `object-fit: cover;` 的同时确保图片的上部总是可见，你可以结合使用 `object-position` 属性。`object-position` 允许你控制背景图像或替换元素（如 `<img>` 或 `<video>`）在容器内的定位。

要使图片的上部总是显示，你可以将 `object-position` 设置为 `0\\%`，这会将图片的顶部对齐到容器的顶部。这是一个示例 CSS：

```css
img \\{
  width: 100\\%; /* 或者设置你需要的宽度 */
  height: auto; /* 或者设置一个固定的高 */
  object-fit: cover; /* 自动裁剪图片以填充容器 */
  object-position: 0\\% 0\\%; /* 确保图片的上部总是可见 */
\\}
```

##### 优先展示图片的左上部分

```css
object-position: 0\\% 0\\%;
```

- `0\\% 0\\%` 表示水平和垂直方向上的起始位置。具体来说，`0\\%` 水平偏移意味着图片的左边缘将与容器的左边缘对齐；`0\\%` 垂直偏移意味着图片的顶部边缘将与容器的顶部边缘对齐。
- 因此，`object-position: 0\\% 0\\%;` 确保了图片的上部（即顶部）总是可见，并且从容器的左上角开始显示图片的内容。

简单来说，这行代码确保无论图片如何缩放（基于 `object-fit` 的值），图片的最顶部和最左边的部分总是可见的，并且图片相对于容器的左上角对齐。

例如，如果有一个宽高比不同于其容器的图片，设置 `object-fit: cover;` 和 `object-position: 0\\% 0\\%;` 将会使图片在保持比例的同时覆盖整个容器，但优先展示图片的左上部分。这样即使图片被裁剪，它的顶部也是始终可见的。

在 HTML 中，你可以这样使用：

```html
<img src="your-image.jpg" alt="Your Image">
```

这样设置后，无论图片的宽高比如何，图片的上部都会始终与容器的顶部对齐，而图片的其他部分可能会被裁剪以保持 `cover` 的效果。

如果你想要更多的控制，你可以使用百分比值来微调 `object-position`，例如 `object-position: 0\\% 50\\%;` 会使图片的上部居中。

##### 水平居中

```css
/* 图片的上部可见，水平居中 */
object-position: 50\\% 0\\%;
```

`object-position: 50\\% 0\\%;` 的设置改变了图片在其容器中的对齐方式。这里，`50\\%` 指的是水平方向上的中心位置，而 `0\\%` 则指的是垂直方向上的顶部位置。

具体来说：

- **水平方向（50\\%）**：表示图片在容器中水平居中显示。也就是说，图片的中心点将与容器的中心点对齐。如果图片的宽度大于容器的宽度，则超出部分将在两边均匀裁剪；如果图片的宽度小于容器宽度，则图片两边会有等量的空间。
  
- **垂直方向（0\\%）**：意味着图片的顶部边缘会与容器的顶部边缘对齐。在这种情况下，无论图片的高度如何调整，其顶部总是与容器顶部对齐，可能会导致图片的底部被裁剪或者容器底部有多余空间。

这种设置通常用于确保图片在适应容器大小的同时，保持一定的视觉焦点。例如，在一个宽高比不同的容器中，使用 `object-fit: cover;` 和 `object-position: 50\\% 0\\%;` 可以让图片从顶部开始显示，并且水平居中，这样即使图片被裁剪，其顶部和中部的重要内容仍能尽量展示出来。

举个例子，如果你有一个风景照片作为背景图，但是你希望确保地平线（假设它位于图片的上半部分）始终可见并且水平居中，那么 `object-position: 50\\% 0\\%;` 就是一个合适的选择。这样可以保证图片的关键区域不会因为适配不同尺寸的屏幕而丢失。

##### 使用背景也可以实现

```html
<div class="bg"
v-lazy:background-image="item.attachments[0].imageUrl"
v-if="item.contentType === 'image'"></div>

.bg \\{
        width: 100\\%;
        height: 100\\%;
        // 将一个背景图像设置为不重复，并且定位在元素内部的左上角，同时保证图像的宽度完全填充元素的宽度，而图像的高度则根据宽度按比例调整。
        background-repeat: no-repeat;
        background-position: left 0px;
        background-size: 100\\% auto;
\\}
```



### 怎么固定图片宽度或者高度，让它按原图比例显示

要保持图片按原比例显示并固定宽度或高度，您需要只设置其中一个属性（宽或高），另一个设为`auto`，这样浏览器会自动按比例调整。以下是具体解决方案：

#### 方案1：固定宽度，高度自适应（常用）

```
img \\{
  width: 20px;    /* 固定宽度 */
  height: auto;   /* 高度自动按比例计算 */
\\}
```

#### 方案2：固定高度，宽度自适应

```
img \\{
  height: 14px;   /* 固定高度 */
  width: auto;    /* 宽度自动按比例计算 */
\\}
```

#### 避免同时固定宽高（防止变形）：

```
- 错误做法（破坏比例）：
img \\{
  width: 20px;
  height: 14px; /* 同时设置会强制拉伸图片 */
\\}

+ 正确做法（任选其一）：
img \\{ width: 20px; height: auto; \\} 
/* 或 */
img \\{ height: 14px; width: auto; \\}
```

#### 效果说明：

- 当只固定宽度时，图片会按原比例计算高度
- 当只固定高度时，图片会按原比例计算宽度
- 使用`object-fit: contain;`可额外适配容器（可选）

> 提示：实际开发中优先选择固定宽度（适应布局流），特殊场景（如固定高度的轮播图）再固定高度。

**不写auto是有效的**：当你只设置宽度（未设置高度）时，高度默认行为是`auto`；反之亦然。



### vue项目中加入图片和背景图：img、background-image

一、背景图

第一种方式：推荐使用

```
<div class="bgimg"></div>

.bgimg\\{
    width: 150px;
    height: 60px;

    /*以下两种路径方式都可以*/
    /*background-image: url('../../../../assets/images/logo.png');*/
    background-image: url('~@/assets/images/logo.png');
    background-size: cover
\\}
```

第二种方式：

```
<div :style="\\{backgroundImage: 'url(' + require('@/assets/images/logo.png') + ')' \\}"></div>
```

第三种方式：

```
<div :style="\\{backgroundImage: 'url(' + imgData + ')' \\}"></div>

<script>
import logo from '@/assets/images/logo.png'
export default \\{
    data() \\{
        return \\{
            imgData: logo
        \\}
    \\}
\\}
</script>
```

二、img直接引入图片

第一种方式：

```
<img src="~@/assets/images/logo.png" alt="">
<img src="../../../../assets/images/logo.png" alt="">
```

第二种方式：

```
<img :src="imgData" alt="">
```

第三种方式：

```
<img :src="require('../../../../assets/images/logo.png')" alt="">
```

原文链接：https://blog.csdn.net/m0_72822997/article/details/136215100







# 背景图

### background属性

background一共有8个属性，css2.1中5个，css3中加了3个。

##### 一、background版本属性

##### css 2.1

- background-color: 背景颜色
- background-image: 背景图片
- background-repeat: 重复背景图片
- background-attachment: 是否固定或者随着页面的其余部分滚动
- background-position: 背景图片的位置

##### css 3

- background-size: 背景的尺寸
- background-origin: 背景图片定位区域
- background-clip: 背景图片绘制区域

background的可以简写为 :

```css
.bg\\{
    background : [background-color] [background-image] [background-repeat] [background-attachment] [background-position] / [background-size] [background-origin] [background-clip]
\\}
```

##### 二、属性详情

##### 1. background-color

背景颜色 支持多种类型

- color_name    规定颜色值为颜色名称的背景颜色（比如 red）。
- hex_number    规定颜色值为十六进制值的背景颜色（比如 #ff0000）。
- rgb_number    规定颜色值为 rgb 代码的背景颜色（比如 rgb(255,0,0)）。
- transparent   默认值。背景颜色为透明。
- inherit   规定应该从父元素继承背景颜色。

```css
.div1\\{
    background-color:blue;
  \\}
.div2\\{
    background-color:#0000ff;
  \\}
.div3\\{
    background-color:rgb(0,0,255);
  \\}
```

##### 2. background-image

背景图片 尽量用引号包起来

```css
.div1\\{
    /** 能识别 **/ 
    background-image: url(http://xxxxxxxxx123.jpg);

    /** 识别不了 **/
    background-image: url(http://xxxxxxxxx-(1)-600x600.jpg);

    /** 加了引号 能识别 **/
    background-image: url('http://xxxxxxxxx-(1)-600x600.jpg');
\\}
```

##### 3. background-repeat

重复图片

- repeat    默认。背景图像将在垂直方向和水平方向重复。
- repeat-x  背景图像将在水平方向重复。
- repeat-y  背景图像将在垂直方向重复。
- no-repeat 背景图像将仅显示一次。
- inherit   规定应该从父元素继承 `background-repeat` 属性的设置。

```css
.div1\\{
  background-repeat: repeat|repeat-x|repeat-y|no-repeat|inherit;
\\}
```

##### 4. background-attachment

滚动或者固定背景

- scroll    默认值。背景图像会随着页面其余部分的滚动而移动。
- fixed 当页面的其余部分滚动时，背景图像不会移动。
- inherit   规定应该从父元素继承 `background-attachment`属性的设置。

```css
.div1\\{
  background-attachment:scroll|fixed|inherit;
\\}
```

##### 5. background-position

图片位置 支持3中类型: 百分比，单位，英文关键字。三种类型能混合着写
 默认值为 0\\% 0\\%;

###### 5.1 百分比

第一个值是水平位置，第二个值是垂直位置。
 左上角是 0\\% 0\\%。右下角是 100\\% 100\\%。
 如果仅定义一个值，另外一个为50\\%。

```css
.div1\\{
  background-position:50\\%;
\\}
```

###### 5.2 单位

可以是px或其他单位。
 第一个值是水平位置，第二个值是垂直位置。
 左上角是 0 0。
 如果仅定义一个值，另外一个为50\\%。

```css
.div1\\{
  background-position:10px 20px;
\\}
```

###### 5.3 英文关键字

如果仅定义了一个关键字，另外一个为center
 值: center top bottom left right

```css
.div1\\{
  background-position: center|top|bottom|left|right center|top|bottom|left|right;
\\}
```

如顶部居中

```
.report-list \\{
  background: url('@/assets/images/customer/header-bg.png') no-repeat center top;
  /* 或分开写： */
  /* background-image: url('@/assets/images/customer/header-bg.png'); */
  /* background-repeat: no-repeat; */
  /* background-position: center top; */
\\}
```

##### 6. background-size

背景大小 有四种类型

```css
.div1\\{
  background-size: auto auto|100\\% 100\\%|contain|cover;
\\}
```

###### 6.1 值

设置背景图像的高度和宽度。
 第一个值设置宽度，第二个值设置高度。
 如果只设置一个值，则第二个值会被设置为 "auto"。

###### 6.2 百分比

以父元素的百分比来设置背景图像的宽度和高度。
 第一个值设置宽度，第二个值设置高度。
 如果只设置一个值，则第二个值会被设置为 "auto"。

###### 6.3 cover

把背景图像扩展至足够大，以使背景图像完全覆盖背景区域。
 背景图像的某些部分也许无法显示在背景定位区域中。

###### 6.4 contain

把图像图像扩展至最大尺寸，以使其宽度和高度完全适应内容区域。

##### 7. background-origin

背景的相对定位
 背景图像的 `background-attachment`属性为 `fixed`，则该属性没有效果。

- padding-box   背景图像相对于内边距框来定位。
- border-box    背景图像相对于边框盒来定位。
- content-box   背景图像相对于内容框来定位。

```css
div1\\{
  background-origin: padding-box|border-box|content-box;
\\}
```

##### 8. background-clip

规定背景的绘制区域

- border-box    背景被裁剪到边框盒。
- padding-box   背景被裁剪到内边距框。
- content-box   背景被裁剪到内容框。

```css
div1\\{
  background-clip:padding-box|border-box|content-box;
\\}
```

原文链接：https://www.jianshu.com/p/7cc41d38f192



### background-size属性详解

background-size 指定背景图像大小，以象素或百分比显示，当指定为百分比时，大小会由所在区域的宽度、高度以及 background-origin（图片的起始位置） 的位置决定，还可以通过 cover 和 contain 来对图片进行伸缩。

1、定义：

background-size用来调整背景图像的尺寸大小。

2、语法：

以下为引用内容：

```
background-size : contain | cover | 100px 100px | 50\\% 100\\%;
```

3、参数：

```
background-size：contain; // 缩小图片来适应元素的尺寸（保持像素的长宽比），是图片宽高最长的那个边覆盖元素一边即可；
background-size ：cover; // 扩展图片来填满元素（保持像素的长宽比），是图片宽高最短的那个边覆盖元素一边即可；
background-size ：100px 100px; // 调整图片到指定大小；
background-size ：50\\% 100\\%; // 调整图片到指定大小，百分比相对于包含元素的尺寸（并且并不需要包含元素显示设置宽高）
```



### 常用宽高相同

```css
background: url('../../assets/images/home/area-bg2@2x.png') center center
        no-repeat;
background-size: 100\\% 100\\%;
```

简写：

```css
background: url('../../assets/images/home/area-bg2@2x.png') no-repeat center / cover;
```

这里的样式解释如下：

- `url('../../assets/images/home/area-bg2@2x.png')`: 指定背景图片的路径。
- `no-repeat`: 设置背景图片不重复。
- `center`: 设置背景图片的位置居中。
- `/ cover`: 设置背景图片的大小覆盖整个容器，同时保持图片的宽高比不变。

这是将所有背景相关的属性合并到一行的简洁写法。这种方式在CSS中被称为“复合属性”写法，可以让你在一个声明中设置多个背景相关的属性。

请注意，如果你的样式表用于生产环境，你可能需要考虑压缩和最小化CSS以减少加载时间。在这种情况下，你可能会进一步压缩上面的代码，例如：

```css
background:url('../../assets/images/home/area-bg2@2x.png')no-repeat center/cover;
```

不过，通常我们还是推荐保持一定的可读性，特别是在开发阶段。



### 顶部背景图宽度很长适配

参考美团商企通网站

```
height: 608px;
background: url(https://p1.meituan.net/travelcube/7b14905a9bac3d7af33710715d26d35f439352.png) no-repeat;
background-position: 50\\%;
background-size: cover;
```



### 固定高度，确保背景图片在PC和移动端均能居中并自适应，同时保持清晰且不失真

为了让图片保持原始比例、不变形，并且能自动填充整个背景区域，最佳实践是使用 `background-size: cover;`。

**`background-size: cover;` 的作用是：**

- 将图片等比例缩放，直到其宽度和高度都**大于或等于**容器的尺寸。
- 这样可以完全覆盖住背景区域，不会留白。
- 图片多余的部分会被裁剪掉（这通常是可接受的）。
- 结合 `background-position: center center;`，可以确保图片的核心部分（中心区域）始终可见。

```
.header-bg \\{
  height: 102px; /* 保持容器高度 */
  padding: 26px 20px 20px;

  /* 背景图片设置 */
  background-image: url('@/assets/images/manage/header-bg@2x.png');
  background-position: center center; /* 水平和垂直居中 */
  background-size: cover;             /* 等比例缩放，完全覆盖容器，不变形 */
  background-repeat: no-repeat;       /* 防止图片平铺 */
\\}
```



### 区分设备时拆分写法才生效

合并写就会被background覆盖，不生效

```css
.pc \\{
  .header \\{
    background-position: center -140px;
    background-size: 100\\% 520px;
  \\}
\\}
.mobile \\{
  .header \\{
    background-position: center -40px;
    background-size: 100\\% 260px;
  \\}
\\}

.header \\{
    height: 260px;
    background-image: url('@/assets/images/customer/detail-bg@2x.png');
    background-repeat: no-repeat;
    // background: url('@/assets/images/customer/detail-bg@2x.png') no-repeat;
\\}
```
