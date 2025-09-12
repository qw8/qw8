---
title: CSS
date: 2021-07-07 23:30:10
categories: 
- 前端面试
tags:
- CSS
- 选择器
- 代码题
---

### 如何居中 div？

-水平居中：给 div 设置一个宽度，然后添加 margin:0 auto 属性

```css
div \\{
  width: 200px;
  margin: 0 auto;
\\}
```

-水平居中，利用 text-align:center 实现

```css
.container \\{
  background: rgba(0, 0, 0, 0.5);
  text-align: center;
  font-size: 0;
\\}

.box \\{
  display: inline-block;
  width: 500px;
  height: 400px;
  background-color: pink;
\\}
```

-让绝对定位的 div 居中

```css
div \\{
  position: absolute;
  width: 300px;
  height: 300px;
  margin: auto;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  background-color: pink; /*方便看效果*/
\\}
```

-水平垂直居中一

```css
/*确定容器的宽高宽500高300的层设置层的外边距div\\{*/
position: absolute;/*绝对定位*/
width: 500px;
height: 300px;
top: 50\\%;
left: 50\\%;
margin: -150px00-250px;/*外边距为自身宽高的一半*/
background-color: pink;/*方便看效果*/
\\}
```

-水平垂直居中二

```css
/*未知容器的宽高，利用`transform`属性*/
div \\{
  position: absolute; /*相对定位或绝对定位均可*/
  width: 500px;
  height: 300px;
  top: 50\\%;
  left: 50\\%;
  transform: translate(-50\\%, -50\\%);
  background-color: pink; /*方便看效果*/
\\}
```

-水平垂直居中三

```css
/*利用flex布局实际使用时应考虑兼容性*/
.container \\{
  display: flex;
  align-items: center; /*垂直居中*/
  justify-content: center; /*水平居中*/
\\}
.containerdiv \\{
  width: 100px;
  height: 100px;
  background-color: pink; /*方便看效果*/
\\}
```

-水平垂直居中四

```css
/*利用text-align:center和vertical-align:middle属性*/
.container \\{
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  background: rgba(0, 0, 0, 0.5);
  text-align: center;
  font-size: 0;
  white-space: nowrap;
  overflow: auto;
\\}

.container::after \\{
  content: '';
  display: inline-block;
  height: 100\\%;
  vertical-align: middle;
\\}

.box \\{
  display: inline-block;
  width: 500px;
  height: 400px;
  background-color: pink;
  white-space: normal;
  vertical-align: middle;
\\}
```

回答：

```
一般常见的几种居中的方法有：

对于宽高固定的元素

（1）我们可以利用margin:0 auto来实现元素的水平居中。

（2）利用绝对定位，设置四个方向的值都为0，并将margin设置为auto，由于宽高固定，因此对应方向实现平分，可以实现水
平和垂直方向上的居中。

（3）利用绝对定位，先将元素的左上角通过top:50\\%和left:50\\%定位到页面的中心，然后再通过margin负值来调整元素
的中心点到页面的中心。

（4）利用绝对定位，先将元素的左上角通过top:50\\%和left:50\\%定位到页面的中心，然后再通过translate来调整元素
的中心点到页面的中心。

（5）使用flex布局，通过align-items:center和justify-content:center设置容器的垂直和水平方向上为居中对
齐，然后它的子元素也可以实现垂直和水平的居中。

对于宽高不定的元素，上面的后面两种方法，可以实现元素的垂直和水平的居中。
```



### 怎么让一个不定宽高的 DIV，垂直水平居中？

**1.使用 CSS方法：**

父盒子设置：

```
display：table-cell；
text-align：center；
vertical-align：middle；
```

Div 设置：

```
display：inline-block；
vertical-align：middle；
```

**2.使用 CSS3transform：**

父盒子设置：

```
display：relative
```

Div 设置：

```
transform：translate(-50\\%，-50\\%)；
position：absolute；
top：50\\%；
left：50\\%；
```

 

### 用纯 CSS 创建一个三角形的原理是什么？

采用的是相邻边框连接处的均分原理。

三角形的实现原理是利用了元素边框连接处的等分原理。

将元素的宽高设为0，只设置border，把任意三条边隐藏掉（颜色设为transparent），剩下的就是一个三角形。

```css
#demo \\{
  width: 0;
  height: 0;
  border-width: 20px;
  border-style: solid;
  // 把上、左、右三条边隐藏掉（颜色设为 transparent）
  border-color: transparent transparent red transparent;
\\}
```

或者

```css
span \\{
  width: 0;
  height: 0;
  border-top: 40px solid transparent;
  border-left: 40px solid transparent;
  border-right: 40px solid transparent;
  border-bottom: 40px solid #ff0000;
\\}
```

![css_001](C:/公司/typora/images/css001.jpg)

[《三角形 demo 展示》](http://cavszhouyou.top/Demo-Display/Triangle/index.html)



### 利用伪元素画三角形

左上方画蓝色三角形

```
.info-tab \\{
  position: relative;
  &::before \\{
      content: ''; /* 必须设置内容为空字符串 */
      position: absolute; /* 绝对定位 */
      left: 15px; /* 调整左边距以适应更大的三角形 */
      top: -20px; /* 调整顶边距以确保三角形完全显示 */
      border-width: 10px; /* 增大三角形大小 */
      border-style: solid;
      border-color: transparent transparent #f2f7fe transparent; /* 设置边框颜色，透明、底色、透明 */
  \\}
\\}
```

蓝色下拉三角形

```css
// 左边
.drop-down \\{
  position: relative;
  &::after \\{
      content: "";
      border: 4px solid transparent;
      border-top-color: #2c8ac2;
      position: absolute;
      top: 11px;
      left: -19px;
  \\}
\\}

// 右边
.drop-down \\{
    position: relative;
    &::after \\{
        content: '';
        border: 5px solid transparent;
        border-top-color: #2c8ac2;
        position: absolute;
        top: 9px;
        right: -18px;
    \\}
\\}
```



### 右边下拉三角形改为等边三角形

要将下拉箭头改为等边三角形，我们需要调整边框的宽度和位置。等边三角形的特点是三条边长度相等，三个角都是60度。在CSS中，我们可以通过调整边框宽度来实现更精确的三角形形状。

以下是修改后的代码：

```css
.drop-down \\{
  line-height: 14px;
  padding: 3px 20px 3px 6px;
  border-radius: 11px;
  font-size: 12px;
  cursor: pointer;
  position: relative;
  color: #2b3341;
  border: 1px solid #dbdbdb;
  
  &::after \\{
    content: '';
    width: 0;
    height: 0;
    border-left: 4px solid transparent;
    border-right: 4px solid transparent;
    border-top: 7px solid #acb3be; /* 高度是宽度的√3倍，近似等边三角形 */
    position: absolute;
    top: 8px; /* 调整位置使其居中 */
    right: 8px;
  \\}
\\}
```

关键修改点：
1. 使用 `width: 0; height: 0;` 创建纯CSS三角形
2. 左右边框设置为相同宽度（4px）
3. 上边框高度设置为约7px（4px × √3 ≈ 6.928px，四舍五入为7px）
4. 调整了 `top` 值使其在容器中垂直居中

这样创建的三角形更接近等边三角形的形状。如果需要更精确的比例，可以微调这些值。

#### 三角形蓝湖上width: 8px; height: 5px;

如果你想将下拉箭头改为 **蓝湖（蓝湖设计工具）** 上常见的 **8px × 5px** 的三角形样式，可以这样调整 CSS：  

##### **修改后的代码（8px × 5px 三角形）**
```css
.drop-down \\{
  line-height: 14px;
  padding: 3px 20px 3px 6px;
  border-radius: 11px;
  font-size: 12px;
  cursor: pointer;
  position: relative;
  color: #2b3341;
  border: 1px solid #dbdbdb;
  
  &::after \\{
    content: '';
    width: 0;
    height: 0;
    border-left: 4px solid transparent;  /* 8px / 2 = 4px */
    border-right: 4px solid transparent; /* 8px / 2 = 4px */
    border-top: 5px solid #acb3be;      /* 高度 5px */
    position: absolute;
    top: 8px; /* 调整垂直居中 */
    right: 8px;
  \\}
\\}
```

##### **关键调整**
1. **`border-left` 和 `border-right` 各 `4px`**（总宽度 `8px`）
2. **`border-top` 高度 `5px`**（蓝湖常见的下拉箭头尺寸）
3. **调整 `top` 值** 使其在容器中垂直居中

##### **效果**
• 三角形宽度：`8px`（左右各 `4px`）
• 三角形高度：`5px`
• 颜色：`#acb3be`（可替换为你的设计稿颜色）

这样就能匹配蓝湖设计稿上的 **8px × 5px** 三角形样式了！ 🎨



### 下方正中间画白色三角形

```
.title \\{
    line-height: 28px;
    margin-bottom: 26px;
    font-size: 20px;
    position: relative;
    &::after \\{
        content: '';
        border: 8px solid transparent;
        border-top-color: rgba(255, 255, 255, 0.7);
        position: absolute;
        left: 50\\%;
        transform: translateX(-50\\%);
        bottom: -22px;
    \\}
\\}
```



### 怎么合并边框线

```
border-top: 1px solid #f5f7f9;
border-bottom: 1px solid #f5f7f9;
```

要合并上下边框的样式，可以使用以下简洁写法：

```
border: solid #f5f7f9;
border-width: 1px 0;
```

#### 解释：

1. `border: solid #f5f7f9;`
    设置所有边框的​**​样式​**​和​**​颜色​**​（相当于全局设置）
2. `border-width: 1px 0;`
   - 第一个值 `1px` 表示 **上下** 边框宽度
   - 第二个值 `0` 表示 **左右** 边框宽度（隐藏左右边框）

#### 效果等同：

```
border-top: 1px solid #f5f7f9;
border-bottom: 1px solid #f5f7f9;
border-left: 0;
border-right: 0;
```

#### 优点：

- 减少重复代码
- 统一维护颜色/样式
- 明确表示左右无边框



### 为什么要初始化 CSS 样式？

因为浏览器的兼容问题，不同浏览器对有些标签的默认值是不同的，如果没对CSS初始化往往会出现浏览器之间的页面显示差异。

当然，初始化样式会对SEO有一定的影响，但鱼和熊掌不可兼得，但力求影响最小的情况下初始化。

```css
最简单的初始化方法：*\\{padding:0;margin:0;\\}（强烈不建议）

淘宝的样式初始化代码：
body,h1,h2,h3,h4,h5,h6,hr,p,blockquote,dl,dt,dd,ul,ol,li,pre,form,fieldset,legend
,button,input,textarea,th,td\\{margin:0;padding:0;\\}
body,button,input,select,textarea\\{font:12px/1.5tahoma,arial,\5b8b\4f53;\\}
h1,h2,h3,h4,h5,h6\\{font-size:100\\%;\\}
address,cite,dfn,em,var\\{font-style:normal;\\}
code,kbd,pre,samp\\{font-family:couriernew,courier,monospace;\\}
small\\{font-size:12px;\\}
ul,ol\\{list-style:none;\\}
a\\{text-decoration:none;\\}
a:hover\\{text-decoration:underline;\\}
sup\\{vertical-align:text-top;\\}
sub\\{vertical-align:text-bottom;\\}
legend\\{color:#000;\\}
fieldset,img\\{border:0;\\}
button,input,select,textarea\\{font-size:100\\%;\\}
table\\{border-collapse:collapse;border-spacing:0;\\}
```



### 如何实现单行／多行文本溢出的省略（...）？

```css
/*单行文本溢出*/
p \\{
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
\\}

/*多行文本溢出*/
p \\{
  position: relative;
  line-height: 1.5em;
  /*高度为需要显示的行数*行高，比如这里我们显示两行，则为3*/
  height: 3em;
  overflow: hidden;
\\}

p:after \\{
  content: '...';
  position: absolute;
  bottom: 0;
  right: 0;
  background-color: #fff;
\\}
```

详细资料可以参考：
[《【CSS/JS】如何实现单行／多行文本溢出的省略》](https://zhuanlan.zhihu.com/p/30707916)
[《CSS 多行文本溢出省略显示》](https://juejin.im/entry/587f453e1b69e60058555a5f)



### css 实现上下固定中间自适应布局？

```css
利用绝对定位实现body \\{
  padding: 0;
  margin: 0;
\\}

.header \\{
  position: absolute;
  top: 0;
  width: 100\\%;
  height: 100px;
  background: red;
\\}

.container \\{
  position: absolute;
  top: 100px;
  bottom: 100px;
  width: 100\\%;
  background: green;
\\}

.footer \\{
  position: absolute;
  bottom: 0;
  height: 100px;
  width: 100\\%;
  background: red;
\\}

利用flex布局实现html,
body \\{
  height: 100\\%;
\\}

body \\{
  display: flex;
  padding: 0;
  margin: 0;
  flex-direction: column;
\\}

.header \\{
  height: 100px;
  background: red;
\\}

.container \\{
  flex-grow: 1;
  background: green;
\\}

.footer \\{
  height: 100px;
  background: red;
\\}
```

详细资料可以参考：
[《css 实现上下固定中间自适应布局》](https://www.jianshu.com/p/30bc9751e3e8)



### css 两栏布局的实现？

相关资料：

```css
/*两栏布局一般指的是页面中一共两栏，左边固定，右边自适应的布局，一共有四种实现的方式。*/
/*以左边宽度固定为200px为例*/

/*（1）利用浮动，将左边元素宽度设置为200px，并且设置向左浮动。将右边元素的margin-left设置为200px，宽度设置为auto（默认为auto，撑满整个父元素）。*/
.outer \\{
  height: 100px;
\\}

.left \\{
  float: left;

  height: 100px;
  width: 200px;

  background: tomato;
\\}

.right \\{
  margin-left: 200px;

  width: auto;
  height: 100px;

  background: gold;
\\}

/*（2）第二种是利用flex布局，将左边元素的放大和缩小比例设置为0，基础大小设置为200px。将右边的元素的放大比例设置为1，缩小比例设置为1，基础大小设置为auto。*/
.outer \\{
  display: flex;

  height: 100px;
\\}

.left \\{
  flex-shrink: 0;
  flex-grow: 0;
  flex-basis: 200px;

  background: tomato;
\\}

.right \\{
  flex: auto;
  /*11auto*/

  background: gold;
\\}

/*（3）第三种是利用绝对定位布局的方式，将父级元素设置相对定位。左边元素设置为absolute定位，并且宽度设置为
200px。将右边元素的margin-left的值设置为200px。*/
.outer \\{
  position: relative;

  height: 100px;
\\}

.left \\{
  position: absolute;

  width: 200px;
  height: 100px;

  background: tomato;
\\}

.right \\{
  margin-left: 200px;
  height: 100px;

  background: gold;
\\}

/*（4）第四种还是利用绝对定位的方式，将父级元素设置为相对定位。左边元素宽度设置为200px，右边元素设置为绝对定位，左边定位为200px，其余方向定位为0。*/
.outer \\{
  position: relative;

  height: 100px;
\\}

.left \\{
  width: 200px;
  height: 100px;

  background: tomato;
\\}

.right \\{
  position: absolute;

  top: 0;
  right: 0;
  bottom: 0;
  left: 200px;

  background: gold;
\\}
```

[《两栏布局 demo 展示》](http://cavszhouyou.top/Demo-Display/TwoColumnLayout/index.html)

回答：

两栏布局一般指的是页面中一共两栏，左边固定，右边自适应的布局，一共有四种实现的方式。

以左边宽度固定为 200px 为例

-（1）利用浮动，将左边元素宽度设置为 200px，并且设置向左浮动。将右边元素的 margin-left 设置为 200px，宽度设置为 auto（默认为 auto，撑满整个父元素）。

-（2）第二种是利用 flex 布局，将左边元素的放大和缩小比例设置为 0，基础大小设置为 200px。将右边的元素的放大比例设置为 1，缩小比例设置为 1，基础大小设置为 auto。

-（3）第三种是利用绝对定位布局的方式，将父级元素设置相对定位。左边元素设置为 absolute 定位，并且宽度设置为 200px。将右边元素的 margin-left 的值设置为 200px。

-（4）第四种还是利用绝对定位的方式，将父级元素设置为相对定位。左边元素宽度设置为 200px，右边元素设置为绝对定位，左边定位为 200px，其余方向定位为 0。



### css 三栏布局的实现？

```css
/*三栏布局一般指的是页面中一共有三栏，左右两栏宽度固定，中间自适应的布局，一共有五种实现方式。
这里以左边宽度固定为100px，右边宽度固定为200px为例。*/

/*（1）利用绝对定位的方式，左右两栏设置为绝对定位，中间设置对应方向大小的margin的值。*/
.outer \\{
  position: relative;
  height: 100px;
\\}

.left \\{
  position: absolute;

  width: 100px;
  height: 100px;
  background: tomato;
\\}

.right \\{
  position: absolute;
  top: 0;
  right: 0;

  width: 200px;
  height: 100px;
  background: gold;
\\}

.center \\{
  margin-left: 100px;
  margin-right: 200px;
  height: 100px;
  background: lightgreen;
\\}

/*（2）利用flex布局的方式，左右两栏的放大和缩小比例都设置为0，基础大小设置为固定的大小，中间一栏设置为auto*/
.outer \\{
  display: flex;
  height: 100px;
\\}

.left \\{
  flex: 00100px;
  background: tomato;
\\}

.right \\{
  flex: 00200px;
  background: gold;
\\}

.center \\{
  flex: auto;
  background: lightgreen;
\\}

/*（3）利用浮动的方式，左右两栏设置固定大小，并设置对应方向的浮动。中间一栏设置左右两个方向的margin值，注意这种方式，中间一栏必须放到最后。*/
.outer \\{
  height: 100px;
\\}

.left \\{
  float: left;
  width: 100px;
  height: 100px;
  background: tomato;
\\}

.right \\{
  float: right;
  width: 200px;
  height: 100px;
  background: gold;
\\}

.center \\{
  height: 100px;
  margin-left: 100px;
  margin-right: 200px;
  background: lightgreen;
\\}

/*（4）圣杯布局，利用浮动和负边距来实现。父级元素设置左右的 padding，三列均设置向左浮动，中间一列放在最前面，宽度设置为父级元素的宽度，因此后面两列都被挤到了下一行，通过设置 margin 负值将其移动到上一行，再利用相对定位，定位到两边。*/
.outer \\{
  height: 100px;
  padding-left: 100px;
  padding-right: 200px;
\\}

.left \\{
  position: relative;
  left: -100px;

  float: left;
  margin-left: -100\\%;

  width: 100px;
  height: 100px;
  background: tomato;
\\}

.right \\{
  position: relative;
  left: 200px;

  float: right;
  margin-left: -200px;

  width: 200px;
  height: 100px;
  background: gold;
\\}

.center \\{
  float: left;

  width: 100\\%;
  height: 100px;
  background: lightgreen;
\\}

/*（5）双飞翼布局，双飞翼布局相对于圣杯布局来说，左右位置的保留是通过中间列的 margin 值来实现的，而不是通过父元
素的 padding 来实现的。本质上来说，也是通过浮动和外边距负值来实现的。*/

.outer \\{
  height: 100px;
\\}

.left \\{
  float: left;
  margin-left: -100\\%;

  width: 100px;
  height: 100px;
  background: tomato;
\\}

.right \\{
  float: left;
  margin-left: -200px;

  width: 200px;
  height: 100px;
  background: gold;
\\}

.wrapper \\{
  float: left;

  width: 100\\%;
  height: 100px;
  background: lightgreen;
\\}

.center \\{
  margin-left: 100px;
  margin-right: 200px;
  height: 100px;
\\}
```

[《三栏布局 demo 展示》](http://cavszhouyou.top/Demo-Display/ThreeColumnLayout/index.html)

回答：

```
三栏布局一般指的是页面中一共有三栏，左右两栏宽度固定，中间自适应的布局，一共有五种实现方式。

这里以左边宽度固定为100px，右边宽度固定为200px为例。

（1）利用绝对定位的方式，左右两栏设置为绝对定位，中间设置对应方向大小的margin的值。

（2）利用flex布局的方式，左右两栏的放大和缩小比例都设置为0，基础大小设置为固定的大小，中间一栏设置为auto。

（3）利用浮动的方式，左右两栏设置固定大小，并设置对应方向的浮动。中间一栏设置左右两个方向的margin值，注意这种方式，中间一栏必须放到最后。

（4）圣杯布局，利用浮动和负边距来实现。父级元素设置左右的padding，三列均设置向左浮动，中间一列放在最前面，宽度设置为父级元素的宽度，因此后面两列都被挤到了下一行，通过设置margin负值将其移动到上一行，再利用相对定位，定位到两边。圣杯布局中间列的宽度不能小于两边任意列的宽度，而双飞翼布局则不存在这个问题。

（5）双飞翼布局，双飞翼布局相对于圣杯布局来说，左右位置的保留是通过中间列的margin值来实现的，而不是通过父元素的padding来实现的。本质上来说，也是通过浮动和外边距负值来实现的。
```



### 实现一个宽高自适应的正方形

```css
/*1.第一种方式是利用vw来实现*/
.square \\{
  width: 10\\%;
  height: 10vw;
  background: tomato;
\\}

/*2.第二种方式是利用元素的margin/padding百分比是相对父元素width的性质来实现*/
.square \\{
  width: 20\\%;
  height: 0;
  padding-top: 20\\%;
  background: orange;
\\}

/*3.第三种方式是利用子元素的margin-top的值来实现的*/
.square \\{
  width: 30\\%;
  overflow: hidden;
  background: yellow;
\\}

.square::after \\{
  content: '';
  display: block;
  margin-top: 100\\%;
\\}
```

[《自适应正方形 demo 展示》](http://cavszhouyou.top/Demo-Display/AdaptiveSquare/index.html)



### 一个自适应矩形，水平垂直居中，且宽高比为 2:1

```css
/*实现原理参考自适应正方形和水平居中方式*/
.box \\{
  position: absolute;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
  margin: auto;

  width: 10\\%;
  height: 0;
  padding-top: 20\\%;
  background: tomato;
\\}
```



### 文本超出部分显示省略号

**单行**

```css
overflow: hidden;
text-overflow: ellipsis;
white-space: nowrap;
```

**多行**

```css
display: -webkit-box;
-webkit-box-orient: vertical;
-webkit-line-clamp: 3; // 最多显示几行
overflow: hidden;
```



### 什么是 Css Hack？ie6,7,8 的 hack 分别是什么？

针对不同的浏览器写不同的 CSS code 的过程，就是 CSS hack。

示例如下：

```css
#test\\{
    width:300px;
    height:300px;
    background-color:blue;      /_firefox_/
    background-color:red\9;      /_all ie_/
    background-color:yellow;    /_ie8_/
    +background-color:pink;        /_ie7_/
    \_background-color:orange;       /_ie6_/   
\\}

 :root #test \\{ background-color:purple\9; \\}  /*ie9*/

@media all and (min-width:0px)

     \\{ #test \\{background-color:black;\\} \\}  /*opera*/

@media screen and (-webkit-min-device-pixel-ratio:0)

\\{ #test \\{background-color:gray;\\} \\}       /*chrome and safari*/
```



### 实现不使用 border 画出 1px 高的线，在不同浏览器的标准模式与怪异模式下都能保持一致的效果。

```html
<div style="height:1px;overflow:hidden;background:red"></div>
```



### input [type=search] 搜索框右侧小图标如何美化？

```css
input[type="search"]::-webkit-search-cancel-button\\{
  -webkit-appearance: none;
  height: 15px;
  width: 15px;
  border-radius: 8px;
  background:url("images/searchicon.png") no-repeat 0 0;
  background-size: 15px 15px;
\\}
```



### 网站图片文件，如何点击下载？而非点击预览？

```
<a href="logo.jpg" download>下载</a>
<a href="logo.jpg" download="网站LOGO" >下载</a>
```



### iOS safari 如何阻止“橡皮筋效果”？

```javascript
  $(document).ready(function()\\{
      var stopScrolling = function(event) \\{
          event.preventDefault();
      \\}
      document.addEventListener('touchstart', stopScrolling, false);
      document.addEventListener('touchmove', stopScrolling, false);
  \\});
```



### 怎么让Chrome支持小于12px 的文字？

```css
  .shrink\\{
    -webkit-transform:scale(0.8);
    -o-transform:scale(1);
    display:inline-block;
  \\}
```

- 用图片：如果是内容固定不变情况下，使用将小于12px文字内容切出做图片，这样不影响兼容也不影响美观
- 使用12px及12px以上字体大小：为了兼容各大主流浏览器，建议设计美工图时候设置大于或等于12px的字体大小，如果是接单的这个时候就需要给客户讲解小于12px浏览器不兼容等事宜
- 继续使用小于12px字体大小样式设置：如果不考虑chrome可以不用考虑兼容，同时在设置小于12px对象设置-webkit-text-size-adjust:none，做到最大兼容考虑



### 让页面里的字体变清晰，变细用CSS怎么做？（IOS手机浏览器字体齿轮设置）

```css
-webkit-font-smoothing: antialiased;
```



### 一个高度自适应的div，里面有两个div，一个高度100px，希望另一个填满剩下的高度

```
- 方案1：
  .sub \\{ height: calc(100\\%-100px); \\}
- 方案2：
  .container \\{ position:relative; \\}
  .sub \\{ position: absolute; top: 100px; bottom: 0; \\}
- 方案3：
  .container \\{ display:flex; flex-direction:column; \\}
  .sub \\{ flex:1; \\}
```

