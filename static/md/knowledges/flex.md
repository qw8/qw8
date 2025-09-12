---
title: flex
date: 2020-08-30 22:30:10
categories: 
- 前端知识
tags:
- CSS
- 选择器
- flex
---

# Flex 布局教程：语法篇

网页布局（layout）是 CSS 的一个重点应用。

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/69874e688dfe4f758a22e94ebd66a72d~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

布局的传统解决方案，基于[盒状模型](https://developer.mozilla.org/en-US/docs/Web/CSS/box_model)，依赖 [`display`](https://developer.mozilla.org/en-US/docs/Web/CSS/display) 属性 + [`position`](https://developer.mozilla.org/en-US/docs/Web/CSS/position)属性 + [`float`](https://link.juejin.cn?target=https\\%3A\\%2F\\%2Fdeveloper.mozilla.org\\%2Fen-US\\%2Fdocs\\%2FWeb\\%2FCSS\\%2Ffloat)属性。它对于那些特殊布局非常不方便，比如，[垂直居中](https://css-tricks.com/centering-css-complete-guide/)就不容易实现。

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/26c6c812f7e04a3fa0726b2ec0edaf65~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

2009年，W3C 提出了一种新的方案----Flex 布局，可以简便、完整、响应式地实现各种页面布局。目前，它已经得到了所有浏览器的支持，这意味着，现在就能很安全地使用这项功能。

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7b8a52baf13c407c9d88520693c9398c~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

Flex 布局将成为未来布局的首选方案。本文介绍它的语法，[下一篇文章](https://www.ruanyifeng.com/blog/2015/07/flex-examples.html)给出常见布局的 Flex 写法。网友 [JailBreak](http://vgee.cn/) 为本文的所有示例制作了 [Demo](http://static.vgee.cn/static/index.html)，也可以参考。

以下内容主要参考了下面两篇文章：[A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) 和 [A Visual Guide to CSS3 Flexbox Properties](https://scotch.io/tutorials/a-visual-guide-to-css3-flexbox-properties)。



## 一、Flex 布局是什么？

Flex 是 Flexible Box 的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性。

任何一个容器都可以指定为 Flex 布局。

```css
.box\\{
  display: flex;
\\}
```

行内元素也可以使用 Flex 布局。

```arduino
.box\\{
  display: inline-flex;
\\}
```

Webkit 内核的浏览器，必须加上`-webkit`前缀。

```css
.box\\{
  display: -webkit-flex; /* Safari */
  display: flex;
\\}
```

注意，设为 Flex 布局以后，子元素的`float`、`clear`和`vertical-align`属性将失效。



## 二、基本概念

采用 Flex 布局的元素，称为 Flex 容器（flex container），简称"容器"。它的所有子元素自动成为容器成员，称为 Flex 项目（flex item），简称"项目"。

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3c60279a874149ffa3717bf1eb8c3b00~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

容器默认存在两根轴：水平的主轴（main axis）和垂直的交叉轴（cross axis）。主轴的开始位置（与边框的交叉点）叫做`main start`，结束位置叫做`main end`；交叉轴的开始位置叫做`cross start`，结束位置叫做`cross end`。

项目默认沿主轴排列。单个项目占据的主轴空间叫做`main size`，占据的交叉轴空间叫做`cross size`。



## 三、容器的属性

以下6个属性设置在容器上。

- flex-direction
- flex-wrap
- flex-flow
- justify-content
- align-items
- align-content

### 3.1 flex-direction属性

`flex-direction`属性决定主轴的方向（即项目的排列方向）。

```sql
.box \\{
  flex-direction: row | row-reverse | column | column-reverse;
\\}
```

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2a40921a01be4341af18e23b6f43323b~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

它可能有4个值。

- `row`（默认值）：主轴为水平方向，起点在左端。
- `row-reverse`：主轴为水平方向，起点在右端。
- `column`：主轴为垂直方向，起点在上沿。
- `column-reverse`：主轴为垂直方向，起点在下沿。

### 3.2 flex-wrap属性

默认情况下，项目都排在一条线（又称"轴线"）上。`flex-wrap`属性定义，如果一条轴线排不下，如何换行。

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/eaeb78dd8d69487a9877d14a13dbe493~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

```lua
.box\\{
  flex-wrap: nowrap | wrap | wrap-reverse;
\\}
```

它可能取三个值。

（1）`nowrap`（默认）：不换行。

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0c2c67ba3ea8459d809b8702f5b7d490~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

（2）`wrap`：换行，第一行在上方。

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d7be2610e8c9422d90d7a69fbf5b907f~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

（3）`wrap-reverse`：换行，第一行在下方。

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0699e153d90a435cb2ef5df3a898c162~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

### 3.3 flex-flow

`flex-flow`属性是`flex-direction`属性和`flex-wrap`属性的简写形式，默认值为`row nowrap`。

```css
.box \\{
  flex-flow: <flex-direction> || <flex-wrap>;
\\}
```

### 3.4 justify-content属性

`justify-content`属性定义了项目在主轴上的对齐方式。

```sql
.box \\{
  justify-content: flex-start | flex-end | center | space-between | space-around;
\\}
```

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/95b68af1914a4d18b0ec3fdada743e61~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

它可能取5个值，具体对齐方式与轴的方向有关。下面假设主轴为从左到右。

- `flex-start`（默认值）：左对齐

- `flex-end`：右对齐

- `center`： 居中

- `space-between`：两端对齐，项目之间的间隔都相等。

  弹性盒子元素会平均地分布在行里。如果最左边的剩余空间是负数，或该行只有一个子元素，则该值等效于'flex-start'。在其它情况下，第一个元素的边界与行的主起始位置的边界对齐，同时最后一个元素的边界与行的主结束位置的边距对齐，而剩余的弹性盒项目则平均分布，并确保两两之间的空白空间相等。

- `space-around`：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。

  弹性盒子元素会平均地分布在行里，两端保留子元素与子元素之间间距大小的一半。如果最左边的剩余空间是负数，或该行只有一个弹性盒项目，则该值等效于'center'。在其它情况下，弹性盒项目则平均分布，并确保两两之间的空白空间相等，同时第一个元素前的空间以及最后一个元素后的空间为其他空白空间的一半。

### 3.5 align-items属性

`align-items`属性定义项目在交叉轴上如何对齐。

```css
.box \\{
  align-items: flex-start | flex-end | center | baseline | stretch;
\\}
```

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8f26a2d0f34b4278b85ffdcf105babfe~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

它可能取5个值。具体的对齐方式与交叉轴的方向有关，下面假设交叉轴从上到下。

- `flex-start`：交叉轴的起点对齐。
- `flex-end`：交叉轴的终点对齐。
- `center`：交叉轴的中点对齐。
- `baseline`: 项目的第一行文字的基线对齐。
- `stretch`（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。

### 3.6 align-content属性

`align-content`属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。

```sql
.box \\{
  align-content: flex-start | flex-end | center | space-between | space-around | stretch;
\\}
```

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5fa3abfabce54eab92182fce4bb5d548~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

该属性可能取6个值。

- `flex-start`：与交叉轴的起点对齐。
- `flex-end`：与交叉轴的终点对齐。
- `center`：与交叉轴的中点对齐。
- `space-between`：与交叉轴两端对齐，轴线之间的间隔平均分布。
- `space-around`：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
- `stretch`（默认值）：轴线占满整个交叉轴。



### 四、项目的属性

以下6个属性设置在项目上。

- `order`
- `flex-grow`
- `flex-shrink`
- `flex-basis`
- `flex`
- `align-self`

### 4.1 order属性

`order`属性定义项目的排列顺序。数值越小，排列越靠前，默认为0。

```css
.item \\{
  order: <integer>;
\\}
```

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0b91e731629c44e9b3a2c1e7a96c5970~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

### 4.2 flex-grow属性

`flex-grow`属性定义项目的放大比例，默认为`0`，即如果存在剩余空间，也不放大。

```css
.item \\{
  flex-grow: <number>; /* default 0 */
\\}
```

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b48cdff5897a4931b65daad535633982~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

如果所有项目的`flex-grow`属性都为1，则它们将等分剩余空间（如果有的话）。如果一个项目的`flex-grow`属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。

### 4.3 flex-shrink属性

`flex-shrink`属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。

```css
.item \\{
  flex-shrink: <number>; /* default 1 */
\\}
```

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f513b3ae80e54ee4a30431e3ef6c24ff~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

如果所有项目的`flex-shrink`属性都为1，当空间不足时，都将等比例缩小。如果一个项目的`flex-shrink`属性为0，其他项目都为1，则空间不足时，前者不缩小。

负值对该属性无效。

### 4.4 flex-basis属性

`flex-basis`属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为`auto`，即项目的本来大小。

```css
.item \\{
  flex-basis: <length> | auto; /* default auto */
\\}
```

它可以设为跟`width`或`height`属性一样的值（比如350px），则项目将占据固定空间。

### 4.5 flex属性

`flex`属性是`flex-grow`, `flex-shrink` 和 `flex-basis`的简写，默认值为`0 1 auto`。后两个属性可选。

```css
.item \\{
  flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
\\}
```

该属性有两个快捷值：`auto` (`1 1 auto`) 和 none (`0 0 auto`)。

建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。

### 4.6 align-self属性

`align-self`属性允许单个项目有与其他项目不一样的对齐方式，可覆盖`align-items`属性。默认值为`auto`，表示继承父元素的`align-items`属性，如果没有父元素，则等同于`stretch`。

```arduino
.item \\{
  align-self: auto | flex-start | flex-end | center | baseline | stretch;
\\}
```

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/631c5b521d354b6685c27764090d35c5~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

该属性可能取6个值，除了auto，其他都与align-items属性完全一致。

原文链接：https://www.ruanyifeng.com/blog/2015/07/flex-grammar.html







# 其他

### flex: 1 flex: auto flex: none flex: 0到底有什么区别 ？使用场景？

我们在日常使用flex布局的时候，经常会用到 flex 缩写。flex简写设置了项目如何增大或缩小以适应在容器中可用的空间。 flex简写属性在下面有三个值的定义 默认值为 `0 1 auto`;

- flex-grow :定义项目的放大比例，默认为`0`
- flex-shrink :定义项目的缩小比例,默认为 `1`
- flex-basis :定义项目在分配多余的空间之前，项目占据的主轴空间 默认为`auto`（item本来大小） 在了解了flex的基本值之后，我们会用一些用例来实验一下(没有特殊声明的话，用例代码都是以下的结构)

```html
html复制代码  <div class="wrapper ">
    <item class="inner">一一一一一一一一一一一一一一一一</item>
    <item class="inner">二二</item>
    <item class="inner">三三</item>
    <item class="inner">四四四四四四四四四四四四四四四四</item>
  </div>
```



### flex:1

```
flex:1` = `flex: 1 1 0\\%;
```

flex:1在父元素尺寸不足的时候，会**优先最小化内容尺寸**。

下面我们给用例设置样式看下这句话是什么意思

```CSS
CSS复制代码.wrapper\\{
    margin: 0 auto;
    width: 560px;
    height: 40px;
    border: black 1px solid;
    display: flex;
  \\}
  .wrapper > .inner\\{
    border: chartreuse 1px solid;
    flex:1;
  \\}
```

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/eeee2318f13e4e769112ac64782476ac~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

从例子我们可以看出 flex:1 ，在充分分配容器尺寸的前提下，会优先`牺牲自己`,填充父容器的尺寸

#### 使用场景

当我们希望元素可以**充分的利用剩余的空间，同时不会很多的占用其他同级元素的空间**的时候使用。

- 等分布局
- 等比例列表



### flex: 1;怎么覆盖

`flex: 1;` 是一种简写属性，它同时设置了 `flex-grow`, `flex-shrink`, 和 `flex-basis`。具体来说，默认情况下，`flex: 1;` 等价于：

- `flex-grow: 1;` — 允许项目增长并占据容器中未使用的空间。
- `flex-shrink: 1;` — 允许项目在必要时缩小。
- `flex-basis: 0;` — 项目的初始主尺寸设置为0，剩余空间根据`flex-grow`的值进行分配。

如果你想覆盖这个属性，你需要明确地指定新的值来覆盖原有的`flex`属性设置。例如，如果你只想让某个元素不增长也不缩小，并且固定宽度，你可以这样设置：

```css
.your-class \\{
    flex-grow: 0;
    flex-shrink: 0;
    flex-basis: auto; /* 或者指定一个具体的宽度如 '200px' */
\\}
```

或者使用`flex`简写形式来达到同样的效果：

```css
.your-class \\{
    flex: 0 0 auto; /* 或者 'flex: 0 0 200px;' */
\\}
```

确保你的覆盖样式在原始样式之后定义，或者通过提高CSS选择器的特异性（specificity）来确保你的样式能够正确覆盖原有的`flex`属性。如果这两个方法都不起作用，你还可以考虑使用`!important`来强制覆盖（虽然这通常不是最佳实践）：

```css
.your-class \\{
    flex: 0 0 auto !important;
\\}
```

请根据实际需要调整这些值。



### flex:auto

```
flex:auto` = `flex: 1 1 auto;
```

flex:auto在父元素尺寸不足的时候，会优先最大化内容尺寸。

```CSS
CSS复制代码.wrapper\\{
    margin: 0 auto;
    width: 560px;
    height: 40px;
    border: black 1px solid;
    display: flex;
  \\}
  .wrapper > .inner\\{
    border: chartreuse 1px solid;
    flex:auto;
  \\}
```

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7a447e2d34344cf18c00c9c34c096497~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

从例子我们可以看出 flex:auto ，在充分分配容器尺寸的前提下，会优先`扩展自己`,填充父容器的尺寸

#### 使用场景

当我们希望元素**充分的使用剩余的空间，各自元素按照各自内容进行分配**的时候使用

- 内容动态适配布局
- 自适应布局
- 子元素个数不确定时



### flex:0

```
flex:0` = `flex: 0 1 0\\%;
```

flex:0 :通常表现为`内容最小化宽度`

```css
css复制代码  .wrapper\\{
    margin: 0 auto;
    width: 560px;
    height: 40px;
    border: black 1px solid;
    display: flex;
    
  \\}
  .wrapper > .inner\\{
    border: chartreuse 1px solid;
    flex:0;
  \\}
```

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/882ab2c7579d493bbbcfdd25319cabe1~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

从以上的例子可以看出:flex:0的时候元素的内容`宽度`最小化，并没有充分的分配容器的尺寸。

#### 使用场景

当希望元素item占用最小化的内容宽度的时候



### flex:none

```
flex:none` = `flex:0 0 auto;
```

flex:none;表示元素的大小由内容决定，但是flex-grow，flex-shrink都是0，元素没有弹性，通常表现为`内容最大化宽度`

```css
css复制代码  .wrapper\\{
    margin: 0 auto;
    width: 560px;
    height: 40px;
    border: black 1px solid;
    display: flex;
    
  \\}
  .wrapper > .inner\\{
    border: chartreuse 1px solid;
    flex:none;
  \\}
```

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/63b9404b0d56472dbb8313044b54523f~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

从以上的例子可以看出:flex:none的时候元素的内容直接溢出容器，没有换行，表现为`最大内容宽度`

#### 使用场景：

元素的宽度就是内容的宽度，并且内容永远不会换行

- 按钮里面文字不换行处理



### 总结

- flex:1 & flex:auto 的区别主要体现在 =>在充分分配父元素宽度的情况下，子元素是优先扩展（auto）自己的尺寸还是优先减小（1）自己的尺寸
- flex:0 & flex: none 的区别主要体现在 =>不考略父元素宽度的情况下，最大化内容宽度（none）还是最小化内容宽度（0）
- 对于不同的使用场景，我们应该使用不同的flex。比如flex：1多用于等分布局中，flex：auto多用于内容动态适配中，flex：none多用于元素内容最大化处理 参考：

[阮一峰flex布局语法篇](https://link.juejin.cn?target=http\\%3A\\%2F\\%2Fwww.ruanyifeng.com\\%2Fblog\\%2F2015\\%2F07\\%2Fflex-grammar.html)

[张鑫旭博客](https://link.juejin.cn?target=https\\%3A\\%2F\\%2Fwww.zhangxinxu.com\\%2Fwordpress\\%2F2020\\%2F10\\%2Fcss-flex-0-1-none\\%2F)

原文链接：https://juejin.cn/post/6967177565458923557



### 一、flex弹性布局

弹性布局，可以让盒子并排显示，并且可以使行内元素转换为行内块级元素

通常在flex布局里，使用时要注意，自己的主轴和侧轴的位置，因为一般情况下，主轴默认为X轴方向，侧轴为Y轴方向



### 二、 flex容器（flex container）

 所有子元素自动成为flex项目(flex item) 简称项目

子元素可横向排列，也可纵向排列。原理:通过给父元素添加flex属性，来控制盒子的位置和排列方式



### 三、父元素的属性

1、flex-direction：设置主轴方向，默认为X轴方向，也可设置Y轴为主轴

| row            | (默认的值)  X轴        |
| -------------- | ---------------------- |
| column         | 垂直方向（Y轴）        |
| row-reverse    | 倒序排列               |
| column-reverse | 主轴沿垂直方向从下到上 |

2、justify-content：设置主轴上子元素的排列方式，使用前先确定好主轴方向

- flex-start	项目位于容器的顶部
- flex-end	项目位于容器的底部
- center	子元素水平居中
- space-around	 将剩余空间平均分配给子项目，剩余空间=父盒子的总宽度-子项目的总宽度
- space-between *	子项目两边贴合父元素，并平均分配。两端对齐，项目之间的间隔是相等的

3、flex-wrap:设置子元素是否换行，布局中默认不换行

- nowrap  	不换行（默认），所有的子项目会在一行显示出来，并平均分配父容器的宽度
- wrap	换行

4、align-items：设置侧轴上的子元素排列方式（单行——也就是不换行）
注意：只有在单行的情况下，才能使用align-items

- flex-start	项目位于容器的顶部
- flex-end	项目位于容器的底部
- center	和justify-content都一起设置center时，子项目就垂直水平居中
- stretch	使用时  子元素不能设置高度，使用较少。拉伸

5、align-content：设置侧轴上子元素排列方式（多行）
多行情况下，子项目对于侧轴的排列方式

- space-between	多行项目均匀分布在容器中，其中第一行分布在容器的顶部，最后一行分布在容器的底部
- space-around	多行项目均匀分布在容器中，其中第一行分布在容器的顶部，最后一行分布在容器的底部

6、flex-flow：复合型写法，同时设置 direction 和 wrap 的值

```
flex-flow: column wrap;
```



### 四、子元素的属性

flex	子项目占的分数，定义子项目分配剩余空间，用flex来表示占多少份； flex: 1;
align-self	控制子项目自己在侧轴的排列方式
order	定义子项的排列顺序（前后顺序），默认为0，数值越小 排列越靠前； order: -2;

原文链接：https://blog.csdn.net/keket1/article/details/125482491