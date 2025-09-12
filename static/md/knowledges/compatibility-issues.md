---
title: 兼容性问题
date: 2021-03-21 15:11:22
categories: 
- 前端知识
tags:
- 浏览器兼容
- 移动端兼容
---
### 浏览器内核

市场上浏览器种类很多，不同浏览器的内核也不尽相同，所以各个浏览器对网页的解析存在一定的差异。

主要分成两部分：渲染引擎(`layout engineer`或`Rendering Engine`)和`JS`引擎，最开始渲染引擎和JS引擎并没有区分的很明确，后来JS引擎越来越独立，内核就倾向于只指**渲染引擎**。

- 渲染引擎：负责取得网页的内容（HTML、XML、图像等等）、整理讯息（例如加入CSS等），以及计算网页的显示方式，然后会输出至显示器或打印机。浏览器的内核的不同对于网页的语法解释会有不同，所以渲染的效果也不相同。所有网页浏览器、电子邮件客户端以及其它需要编辑、显示网络内容的应用程序都需要内核
- JS引擎则：解析和执行javascript来实现网页的动态效果



### 常见的浏览器内核有哪些？

- `Trident`内核：`IE,MaxThon,TT,The World,360`,搜狗浏览器等国产浏览器。[又称MSHTML]
- `Gecko`内核：`Netscape6`及以上版本，`FF,MozillaSuite/SeaMonkey`等
- `Presto`内核：`Opera7`及以上。      [`Opera`内核原为：Presto，现为：`Blink`;]
- `Webkit`内核：`Safari,Chrome`等。   [ `Chrome`的`Blink`（`WebKit`的分支）]
- Blink内核：新版 Chrome、新版 Opera

> 常见的浏览器内核可以分四种：**Trident、Gecko、Blink、Webkit**
> IE浏览器			  Trident内核，也称为IE内核
> Chrome浏览器  Webkit内核，现在是Blink内核
> Firefox浏览器	Gecko内核，俗称Firefox内核
> Safari浏览器	  Webkit内核
> Opera浏览器	 最初是自己的Presto内核，后来加入谷歌大军，从Webkit又到了Blink内核；
> 360浏览器	     IE+Chrome双内核
> 猎豹浏览器	    IE+Chrome双内核
> 百度浏览器	    IE内核
> QQ浏览器	     Trident（兼容模式）+Webkit（高速模式）



### 为何会出现浏览器兼容问题

- 同一产品，版本越老 bug 越多
- 同一产品，版本越新，功能越多
- 不同产品，不同标准，不同实现方式



### 处理兼容问题的思路

**1.要不要做**

- 产品的角度（产品的受众、受众的浏览器比例、效果优先还是基本功能优先）
- 成本的角度 (有无必要做某件事)
- 不同浏览器的解析器实现不同

**2.做到什么程度**

​        让哪些浏览器支持哪些效果

**3.如何做**

- 根据兼容需求选择技术框架/库(jquery)
- 根据兼容需求选择兼容工具(html5shiv.js、respond.js、css reset、normalize.css、Modernizr)
- 条件注释、CSS Hack、js 能力检测做一些修补
- **渐进增强**(progressive enhancement): 针对低版本浏览器进行构建页面，保证最基本的功能，然后再针对高级浏览器进行效果、交互等改进和追加功能达到更好的用户体验
- **优雅降级** (graceful degradation): 一开始就构建完整的功能，然后再针对低版本浏览器进行兼容。



### 渐进增强和优雅降级定义、不同

#### 渐进增强progressive enhancement

针对低版本浏览器进行构建页面，保证最基本的功能，然后再针对高级浏览器进行效果、交互等改进和追加功能达到更好的用户体验。

（一开始保证最基本的功能，再改进和追加功能）

#### 优雅降级graceful degradation

一开始就根据高版本浏览器构建完整的功能，然后再针对低版本浏览器进行兼容。

区别：优雅降级是从复杂的现状开始，并试图减少用户体验的供给，而渐进增强则是从一个非常基础的，能够起作用的版本开始，并不断扩充，以适应未来环境的需要。降级（功能衰减）意味着往回看；而渐进增强则意味着朝前看，同时保证其根基处于安全地带。



### 什么叫优雅降级和渐进增强？

- 优雅降级：

  Web站点在所有新式浏览器中都能正常工作，如果用户使用的是老式浏览器，则代码会针对旧版本的IE进行降级处理了，使之在旧式浏览器上以某种形式降级体验却不至于完全不能用。

  Web站点在所有新式浏览器中都能正常工作，如果用户使用的是老式浏览器，则代码会检查以确认它们是否能正常工作。由于IE独特的盒模型布局问题，针对不同版本的IE的hack实践过优雅降级了，为那些无法支持功能的浏览器增加候选方案，使之在旧式浏览器上以某种形式降级体验却不至于完全失效。

- 渐进增强：

  从被所有浏览器支持的基本功能开始，逐步地添加那些只有新版本浏览器才支持的功能，向页面增加不影响基础浏览器的额外样式和功能的。当浏览器支持时，它们会自动地呈现出来并发挥作用。

  如：默认使用flash上传，但如果浏览器支持 HTML5 的文件上传功能，则使用HTML5实现更好的体验

详见：[css学习归纳总结（一）](http://segmentfault.com/blog/trigkit4/1190000000800711#articleHeader30)







# IE兼容性问题

### 如何不让ie跳转到edge

设置ie浏览器不跳转到edge浏览器需要进入IE浏览器的Internet选项，关闭启用第三方浏览器扩展即可。 

1.点击设置符号

打开IE浏览器，点击右上角的菜单中的设置符号。

![如何不让ie跳转到edge](https://exp-picture.cdn.bcebos.com/d2001d7de137c9763c63307244672b5fd4462b7a.jpg?x-bce-process=image\\%2Fresize\\%2Cm_lfit\\%2Cw_500\\%2Climit_1\\%2Fformat\\%2Cf_auto\\%2Fquality\\%2Cq_80)

2.点击高级

在弹出菜单中点击Internet选项，在弹出的Internet 选项窗口中点击高级。

![如何不让ie跳转到edge](https://exp-picture.cdn.bcebos.com/023cff37c97622bc621a82d0a05fd5460496287a.jpg?x-bce-process=image\\%2Fresize\\%2Cm_lfit\\%2Cw_500\\%2Climit_1\\%2Fformat\\%2Cf_auto\\%2Fquality\\%2Cq_80)

3.关闭启用第三方浏览器

在高级项下的设置里面滚动滑动，找到浏览，把勾选的启动第三方浏览器取消勾选即可。

![如何不让ie跳转到edge](https://exp-picture.cdn.bcebos.com/32fbcd41037de137d4a96f0bf6c5cf672a5f2a7a.jpg?x-bce-process=image\\%2Fresize\\%2Cm_lfit\\%2Cw_500\\%2Climit_1\\%2Fformat\\%2Cf_auto\\%2Fquality\\%2Cq_80)

4.重启电脑才生效



### IE设置background: rgb(0, 21, 51, .7);无效

分开写就可以了

```
background: #001533;
opacity: .7;
```



### IE不支持ES6语法，如模板字符串``、箭头函数

- 将模板字符串改为字符串拼接 
- 使用转换工具babel


```
<script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
<script type="text/babel">
const getMessage = () => `Hello World`;
document.getElementById('output').innerHTML = getMessage();
</script>
```



### 子元素超出父元素宽度

需单独设置子元素宽度，或者设置为100\\%



### Jquery + CSS 简易解决文字溢出省略问题（兼容IE）

原理很简单，就是计算行高，然后与当前的元素判断，大于的话就截取，后面替换再拼接 ···，因为此处计算的是行高，需要有一个固定的行高。

```
		/*
        * 兼容IE省略多行
        * @param \\{number\\} lines-行数
        * @param \\{string\\} jDom-选择器
        */
        function ellipsis(lines, jDom) \\{
            jDom.each(function () \\{
                var lineHeight = Math.ceil($(this).css("lineHeight").slice(0, -2));
                var maxHeight = lineHeight * lines;
                while ($(this).height() > maxHeight) \\{
                    $(this).text($(this).text().slice(0, -4) + "...");
                \\}
            \\});
        \\}
        ellipsis(2, $('.list .desc'))
```



### CSS-hover替换图片

原来这种写法在ie没有hover效果，其他浏览器正常

```
   .arrow \\{
      width: 22px;
      height: 22px;
    \\}
    // 左箭头
   .arrow:first-of-type:hover \\{
      content: url("http://xxxxx")
    \\}
```

```
	.txlhover:hover \\{ 
      .imgText img \\{
        content: url(/static/img/txl.png);
      \\}
    \\}
```

兼容ie

```
.news .btn \\{
    width: 58px;
    height: 58px;
\\}
.news .left\\{
    background: url('../../images/left1@2x.png') no-repeat;
    background-size: cover;
\\}
.left:hover \\{
    background: url('../../images/left1-hover@2x.png') no-repeat;
    background-size: cover;
\\}
```



### placeholder样式兼容各浏览器

写法：input::placeholder\\{你想要修改的样式\\}

因为placeholder是 HTML5 中新增加的属性，需要注意浏览器的兼容性。 

```
<input type="text" id="input" placeholder="请输入用户名" />

/* 使用webkit内核的浏览器 */
input::-webkit-input-placeholder\\{\\}
/* Firefox版本4-18 */
input:-moz-placeholder\\{\\}
/* Firefox版本19+ */
input::-moz-placeholder\\{\\}
/* IE浏览器 */
input:-ms-input-placeholder\\{\\}
```



# 其他兼容性问题

### flex布局兼容性写法

#### 1.容器写法

```css
display: -webkit-box; /* Chrome 4+, Safari 3.1, iOS Safari 3.2+ */  
display: -moz-box; /* Firefox 17- */  
display: -webkit-flex; /* Chrome 21+, Safari 6.1+, iOS Safari 7+, Opera 15/16 */  
display: -moz-flex; /* Firefox 18+ */  
display: -ms-flexbox; /* IE 10 */  
display: flex; /* Chrome 29+, Firefox 22+, IE 11+, Opera 12.1/17/18, Android 4.4+ */  
```

##### 2.其他

```css
/*display*/
.display_flex\\{
    display: -webkit-box;
    display: -ms-flexbox;
    display: -webkit-flex;
    display: flex;
\\}
.display_flex > *\\{
    display: block;
\\}
.display_inline-flex\\{
    display: -webkit-inline-box;
    display: -ms-inline-flexbox;
    display: -webkit-inline-flex;
    display: inline-flex;    
\\}
.display_inline-flex > *\\{
    display: block;
\\}
/*伸缩流方向*/
.flex-direction_column\\{
    -webkit-box-orient: vertical;
    -ms-flex-direction: column;
    -webkit-flex-direction: column;
    flex-direction: column;
\\}
/*主轴对齐*/
.justify-content_flex-center\\{
    -webkit-box-pack: center;
    -ms-flex-pack: center;
    -webkit-justify-content: center;
    justify-content: center;
\\}
.justify-content_flex-end\\{
    -webkit-box-pack: end;
    -ms-flex-pack: end;
    -webkit-justify-content: flex-end;
    justify-content: flex-end;
\\}
.justify-content_flex-justify\\{
    -webkit-box-pack: justify;
    -ms-flex-pack: justify;
    -webkit-justify-content: space-between;
    justify-content: space-between;
\\}
/*侧轴对齐*/
.align-items_flex-start\\{
    -webkit-box-align: start;
    -ms-flex-align: start;
    -webkit-align-items: flex-start;
    align-items: flex-start;
\\}
.align-items_flex-end\\{
    -webkit-box-align: end;
    -ms-flex-align: end;
    -webkit-align-items: flex-end;
    align-items: flex-end;
\\}
.align-items_center\\{
    -webkit-box-align: center;
    -ms-flex-align: center;
    -webkit-align-items: center;
    align-items: center;
\\}
.align-items_baseline\\{
    -webkit-box-align: baseline;
    -ms-flex-align: baseline;
    -webkit-align-items: baseline;
    align-items: baseline;
\\}
/*伸缩性*/
.flex_auto\\{
    -webkit-box-flex: 1;
    -ms-flex: auto;
    -webkit-flex: auto;
    flex: auto;
\\}
.flex_1\\{
    width: 0;
    -webkit-box-flex: 1;
    -ms-flex: 1;
    -webkit-flex: 1;
    flex: 1;    
\\}
/*显示顺序*/
.order_2\\{
    -webkit-box-ordinal-group: 2;
    -ms-flex-order: 2;
    -webkit-order: 2;
    order: 2;
\\}
.order_3\\{
    -webkit-box-ordinal-group: 3;
    -ms-flex-order: 3;
    -webkit-order: 3;
    order: 3;
\\}
```

总结日期：2019.11.27



### Vue.js浏览器兼容性问题

#### IE兼容性问题

- IE11不识别 data()\\{\\}定义的方法

```kotlin
    data()\\{
        return \\{\\}
    \\}
```

- 仅识别如下形式:

```jsx
    data: function () \\{
        return \\{\\}
    \\}
```

- IE10不识别let标识符
- Vue不支持IE8, 因为Vue使用了IE8无法模拟的ECMAScript 5 特性, 但它支持所有**兼容ECMAScript 5** 的浏览器
- IE8不识别 vue.js 中的: var extendsFrom = child.extends;  // 报错缺少标识符
- 腾讯、淘宝已经不支持IE8
- xp系统最高只支持IE8

#### Microsoft Edge

- 均支持 let和data()\\{\\}定义的方法

#### 360

- 均支持 let和data()\\{\\}定义的方法



vue-cli2：兼容ie9及其以上；
flex：兼容ie10及其以上；
vue-cli3：兼容ie11及其以上



1、首先，安装babel-polyfill，在main.js文件的开头引入。
2、再次，使用IE11打开页面，看控制台的报错，然后都解决了。
3、这时候，你的应用基本上就可以用手机打开了，就正常了。

以上思路是通过解决IE的兼容性，顺便就兼容了手机端。是不是很厉害啊？

总结日期：2019.11.27



> 定义：浏览器兼容性又叫网页或者网站的兼容性问题，是指不同的浏览器**（内核）**对同一段代码有不同的解析，造成页面显示不一样的情况
>
> 所以需要考虑到：内核，客户端屏幕尺寸&分辨率，操作系统，不同终端

### 什么时候需要做浏览器兼容性测试？

大型的，用户群体多的网站都需要做浏览器兼容性测试，需要测试主流的浏览器（除特定要求的浏览器以外）

测试的内容：

- 一般是页面的排版，页面格式，字体，颜色，下拉菜单，复选框等测试（UI：CSS，HML，Js在不同浏览器下的表现）
- 再就是对功能进行检查

四个主流浏览器 

- IE8以上，360极速/ 安全浏览器、搜狗（Trident内核）
- 火狐（Gecko内核）
- google（Blink内核）
- 苹果、遨游浏览器（Gecko内核）

| 谷歌Chrome  | Blink，Webkit                      | 体积小浏览速度快，本身安全性较高                             |
| ----------- | ---------------------------------- | ------------------------------------------------------------ |
| 火狐Firefox | Gecko                              | 跨多个平台，最大的特色就是兼容，速度比较快                   |
| ie          | Trident                            | 使用用户越来越少，逐渐被其他浏览器取代                       |
| 360         | Blink（Webkit）-极速，Trident-兼容 | 现在主流浏览器，会将不能识别的软件作为病毒处理掉，会将它认为不安全的浏览器重新命名等 |
| 搜狗/QQ     | Webkit-极速，Trident-兼容          |                                                              |
| safari      | Webkit                             | 是苹果计算机的操作系统Mac OS中的浏览器                       |
| Opera       | Blink                              | 跨多个平台，快速、小巧和比其他浏览器更佳的标准兼容性         |

 

### 会对不同版本的浏览器进行测试吗？例如：兼容IE8~IE11

- 按照需求，做到一定程度上的向下兼容
- 用户手册、用户引导中，写推荐使用的浏览器（版本和内核）

 

### 小众浏览器需不需要做兼容性测试？用户反馈再小众浏览器上有问题？怎么处理？

- 一般来说都需要做兼容性测试，保证我们在小众浏览器上也不会出现错位问题 ，但是具体怎么做要看用户的要求（eg：用户说是需要在谷歌浏览器上加宣传彩页，视觉效果最好，我们就得调查分析 市面上大多数用户使用的分辨率及谷歌浏览器多少分辨率视觉效果才是最好的）。
- 可以与用户沟通，看这个小众浏览器上的客户群体占比例情况能不能放弃，主推大众浏览器，如果不行，可以联系开发修改代码保证小众浏览器的兼容性

 

### 如果一个网站分为前台、后台是否都需要做浏览器兼容性测试？

前台测试一般都会做兼容性测试，但是如果我的网站后台只有自己进行管理，一般不需要做兼容性测试，如果我们后台会分一部分权限对外，就得需要做兼容性测试，还是得根据用户的需求来定。

 

### 面试：你们做的项目是什么架构？

BS：
- Browser/server
- 浏览器的兼容：IE，Firefox…..一般就是最新版本/稳定版本就可以了。是不是可以使用，展示是不是OK

CS：
- Client/server
- CS客户端的兼容：在不同系统是不是兼容。可以安装就好



### 测试手段

- 手工测试：安装不同的浏览器，逐一进行测试（可能考虑高低版本，eg：IE工具ietester [ie8-ie11]）；
  - 目标浏览器（高低版本）：1.需要和产品沟通好，以需求为准；2.或者参考行业领头的标准
  - 主要环境已经明确，用例要进行全覆盖。侧重：主业务流程
- 云测试：wetest，Testin，人手不足的付费测试
- 测试环境需求：设备，正常网络，弱网，断网

总结日期：2019.12.2



### 常见的浏览器兼容性问题

#### 1、不同浏览器的**标签默认的margin和padding不同**

解决方案：全局的 css文件 里增加通配符 * \\{ margin: 0; padding: 0; \\}

#### 2、IE6双边距问题

在 IE6中设置了float , 同时又设置margin就会出现边距问题（如：元素向左浮动并且设置了左侧的外边距、元素向右浮动并且设置右边距；同一行如果有多个浮动元素，第一个浮动元素会出现这个双边距bug，其它的浮动元素则不会）。
解决方案：给浮动元素加上display:inline;

#### 3.margin-top，margin-bottom的bug

父元素的第一个子元素设置了margin-top,会作用于父元素（值为父元素的margin-top与该margin-top两者中的最大值)，而子元素和父元素的边距则没有发生变化。

#### 4、图片默认有间距

解决方案：使用float为img 布局

#### 5、IE9以下浏览器不能使用opacity

解决方案：

```
opacity: 0.5;
filter: alpha(opacity = 50);
filter: progid:DXImageTransform.Microsoft.Alpha(style = 0, opacity = 50);
```

#### 6、cursor

hand 显示手型在safari 上不支持
解决方案：统一使用 cursor:pointer

####  7、两个块级元素，父元素设置了overflow:auto；子元素设置了position:relative ;且高度大于父元素，在IE6、IE7**会被隐藏而不是溢出**；

解决方案：父级元素设置position:relative

#### 8、不同浏览器都会带有自己的浏览器默认样式，一般我们需要把这些浏览器默认自带的样式给清除，一般我们借助reset.css来清楚浏览器默认样式。

简单

```
* \\{
    margin: 0;
    padding: 0;
    list-style: none;
    outline: none;
    font-weight: normal;
    box-sizing: border-box;
    font-family: PingFang, Microsoft Yahei, sans-serif;
\\}

html,
body \\{
    text-rendering: optimizeLegibility;
    text-size-adjust: 100\\%;
    -webkit-font-smoothing: antialiased;
\\}
```



```
//解决不同浏览器页面样视不统一问题
@charset "utf-8";html\\{background-color:#fff;color:#000;font-size:12px\\}
body,ul,ol,dl,dd,h1,h2,h3,h4,h5,h6,figure,form,fieldset,legend,input,textarea,button,p,blockquote,th,td,pre,xmp\\{margin:0;padding:0\\}
body,input,textarea,button,select,pre,xmp,tt,code,kbd,samp\\{line-height:1.5;font-family:tahoma,arial,"Hiragino Sans GB",simsun,sans-serif\\}
h1,h2,h3,h4,h5,h6,small,big,input,textarea,button,select\\{font-size:100\\%\\}
h1,h2,h3,h4,h5,h6\\{font-family:tahoma,arial,"Hiragino Sans GB","微软雅黑",simsun,sans-serif\\}
h1,h2,h3,h4,h5,h6,b,strong\\{font-weight:normal\\}
address,cite,dfn,em,i,optgroup,var\\{font-style:normal\\}
table\\{border-collapse:collapse;border-spacing:0;text-align:left\\}
caption,th\\{text-align:inherit\\}
ul,ol,menu\\{list-style:none\\}
fieldset,img\\{border:0\\}
img,object,input,textarea,button,select\\{vertical-align:middle\\}
article,aside,footer,header,section,nav,figure,figcaption,hgroup,details,menu\\{display:block\\}
audio,canvas,video\\{display:inline-block;*display:inline;*zoom:1\\}
blockquote:before,blockquote:after,q:before,q:after\\{content:"\0020"\\}
textarea\\{overflow:auto;resize:vertical\\}
input,textarea,button,select,a\\{outline:0 none;border: none;\\}
button::-moz-focus-inner,input::-moz-focus-inner\\{padding:0;border:0\\}
mark\\{background-color:transparent\\}
a,ins,s,u,del\\{text-decoration:none\\}
sup,sub\\{vertical-align:baseline\\}
html \\{overflow-x: hidden;height: 100\\%;font-size: 50px;-webkit-tap-highlight-color: transparent;\\}
body \\{font-family: Arial, "Microsoft Yahei", "Helvetica Neue", Helvetica, sans-serif;color: #333;font-size: .28em;line-height: 1;-webkit-text-size-adjust: none;\\}
hr \\{height: .02rem;margin: .1rem 0;border: medium none;border-top: .02rem solid #cacaca;\\}
a \\{color: #25a4bb;text-decoration: none;\\}
```

```
/**
 * Eric Meyer's Reset CSS v2.0 (http://meyerweb.com/eric/tools/css/reset/)
 * http://cssreset.com
 */
 
html, body, div, span, applet, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
a, abbr, acronym, address, big, cite, code,
del, dfn, em, img, ins, kbd, q, s, samp,
small, strike, strong, sub, sup, tt, var,
b, u, i, center,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, embed, 
figure, figcaption, footer, header, hgroup, 
menu, nav, output, ruby, section, summary,
time, mark, audio, video\\{
  margin: 0;
  padding: 0;
  border: 0;
  font-size: 100\\%;
  font: inherit;
  font-weight: normal;
  vertical-align: baseline;
\\}
/* HTML5 display-role reset for older browsers */
article, aside, details, figcaption, figure, 
footer, header, hgroup, menu, nav, section\\{
  display: block;
\\}
ol, ul, li\\{
  list-style: none;
\\}
blockquote, q\\{
  quotes: none;
\\}
blockquote:before, blockquote:after,
q:before, q:after\\{
  content: '';
  content: none;
\\}
table\\{
  border-collapse: collapse;
  border-spacing: 0;
\\}
 
/* custom */
a\\{
  color: #7e8c8d;
  text-decoration: none;
  -webkit-backface-visibility: hidden;
\\}
::-webkit-scrollbar\\{
  width: 5px;
  height: 5px;
\\}
::-webkit-scrollbar-track-piece\\{
  background-color: rgba(0, 0, 0, 0.2);
  -webkit-border-radius: 6px;
\\}
::-webkit-scrollbar-thumb:vertical\\{
  height: 5px;
  background-color: rgba(125, 125, 125, 0.7);
  -webkit-border-radius: 6px;
\\}
::-webkit-scrollbar-thumb:horizontal\\{
  width: 5px;
  background-color: rgba(125, 125, 125, 0.7);
  -webkit-border-radius: 6px;
\\}
html, body\\{
  width: 100\\%;
  font-family: "Arial", "Microsoft YaHei", "黑体", "宋体", "微软雅黑", sans-serif;
\\}
body\\{
  line-height: 1;
  -webkit-text-size-adjust: none;
  -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
\\}
html\\{
  overflow-y: scroll;
\\}
 
/*清除浮动*/
.clearfix:before,
.clearfix:after\\{
  content: " ";
  display: inline-block;
  height: 0;
  clear: both;
  visibility: hidden;
\\}
.clearfix\\{
  *zoom: 1;
\\}
 
/*隐藏*/
.dn\\{
  display: none;
\\}
```



#### **9、display:inline-block（IE7及以下不支持）**

需要对低版本IE特殊处理：

```
\\{
	display:inline-block;
	display:inline;
	zoom:1;
\\}
```

#### 10、display:inline-block 什么时候会显示间隙？怎样消除间隙？

父元素font-size设置成0，子元素重新设置font-size
display:inline-block滥用容易出现布局方面的问题，尤其在左中右、左右等布局方面的问题尤为突出。因此如果是左右布局的话，尽量都用浮动来代替。

#### **11、z-index**

z-index在IE7及以下版本的话，有时会发现不是谁z-index设置的越高谁就显示在最上面。碰到这种问题需要设置父元素有相对定位属性元素的z-index。先比较父元素的z-index再比较子元素的

#### **12、IE8-(IE8及以下)rgba模式不兼容的解决方案**

IE8以及以下用滤镜， filter:Alpha(opacity=20);

#### 13、当标签的高度设置小于10px，在IE6、IE7中会超出自己设置的高度

解决方案：超出高度的标签设置overflow:hidden，或者设置line-height的值小于你的设置高度

#### 14、png24位的图片在iE6浏览器上出现背景

解决方案：是做成PNG8.

#### 15、获取自定义属性

IE下,可以使用获取常规属性的方法来获取自定义属性,也可以使用getAttribute()获取自定义属性;Firefox下,只能使用getAttribute()获取自定义属性。

**解决方法：**统一通过getAttribute()获取自定义属性

#### 16、IE下,even对象有x,y属性,但是没有pageX,pageY属性；Firefox下,event对象有pageX,pageY属性,但是没有x,y属性

**解决方法：**使用 mX(mX = event.x ? event.x : event.pageX;)来代替 IE 下的 event.x 或者 Firefox 下的 event.pageX.



### IE6 遇到什么 bug？解决办法是？

一、IE6 双倍边距 bug

当页面上的元素使用 float 浮动时，不管是向左还是向右浮动;只要该元素带有 margin 像素都会使该值乘以 2，例如“margin-left:10px” 在 IE6 中，该值就会被解析为 20px。想要解决这个 BUG 就需要在该元素中加入 display:inline 或 display:block 明确其元素类型即可解决双倍边距的 BUG

二、IE6 中 3 像素问题及解决办法

当元素使用 float 浮动后，元素与相邻的元素之间会产生 3px 的间隙。诡异的是如果右侧的容器没设置高度时 3px 的间隙在相邻容器的内部，当设定高度后又跑到容器的相反侧了。要解决这类 BUG 的话，需要使布局在同一行的元素都加上 float 浮动。

三、IE6 中奇数宽高的 BUG

IE6 中奇数的高宽显示大小与偶数高宽显示大小存在一定的不同。其中要问题是出在奇数高宽上。要解决此类问题，只需要尽量将外部定位的 div 高宽写成偶数即可。

四、IE6 中图片链接的下方有间隙

IE6 中图片的下方会存在一定的间隙，尤其在图片垂直挨着图片的时候，即可看到这样的间隙。要解决此类问题，需要将 img 标签定义为 display:block 或定义 vertical-align 对应的属性。也可以为 img 对应的样式写入 font-size:0

五、IE6 下空元素的高度 BUG

如果一个元素中没有任何内容，当在样式中为这个元素设置了 0-19px 之间的高度时。此元素的高度始终为 19px。

解决的方法有四种:

1.在元素的 css 中加入：overflow:hidden

2.在元素中插入 html 注释：

3.在元素中插入 html 的空白符：

4.在元素的 css 中加入：font-size:0

六、重复文字的 BUG

在某些比较复杂的排版中，有时候浮动元素的最后一些字符会出现在 clear 清除元素的下面。

解决方法如下：

1.确保元素都带有 display:inline

2.在最后一个元素上使用“margin-right:-3px

3.为浮动元素的最后一个条目加上条件注释，xxx

4.在容器的最后元素使用一个空白的 div，为这个 div 指定不超过容器的宽度。

七、IE6 中 z-index 失效

具体 BUG 为，元素的父级元素设置的 z-index 为 1，那么其子级元素再设置 z-index 时会失效，其层级会继承父级元素的设置，造成某些层级调整上的 BUG。

写在最后：实际上 IE6 中，很多 BUG 的解决方法都可以使用 display:inline、font-size:0、float 解决。因此我们在书写代码时要记住，一旦使用了 float 浮动，就为元素增加一个 display:inline 样式，可以有效的避免浮动造成的样式错乱问题。使用空 DIV 时，为了避免其高度影响布局美观，也可以为其加上 font-size:0 这样就很容易避免一些兼容上的问题。

解析：[参考](https://www.cnblogs.com/rightzhao/p/3474162.html)



### IE 和标准下有哪些兼容性的写法

```js
var ev = ev || window.event;
document.documentElement.clientWidth || document.body.clientWidth;
var target = ev.srcElement || ev.target;
```



### 为什么不能定义 1px 左右的 div 容器？

IE6 下这个问题是因为默认的行高造成的，解决的方法也有很多，例如：
overflow:hidden | zoom:0.08 | line-height:1px



### 为什么要初始化CSS样式？

因为浏览器的兼容问题，不同浏览器对有些标签的默认值是不同的，如果没对CSS初始化往往会出现浏览器之间的页面显示差异。



### 什么是CSS hack？

由于不同厂商的流览器或某浏览器的不同版本（如IE6-IE11,Firefox/Safari/Opera/Chrome等），对CSS的支持、解析不一样，导致在不同浏览器的环境中呈现出不一致的页面展现效果。这时，我们为了获得统一的页面效果，就需要针对不同的浏览器或不同版本写特定的CSS样式，我们把这个针对不同的浏览器/不同版本写相应的CSS code的过程，叫做CSS hack!



### CSS hack的原理

由于不同的浏览器和浏览器各版本对CSS的支持及解析结果不一样，以及**CSS优先级对浏览器展现效果的影响**，我们可以据此针对不同的浏览器情景来应用不同的CSS。



### CSS hack分类

科普
lte：就是Less than or equal to的简写，也就是小于或等于的意思。
lt ：就是Less than的简写，也就是小于的意思。
gte：就是Greater than or equal to的简写，也就是大于或等于的意思。
gt ：就是Greater than的简写，也就是大于的意思。
! ：就是不等于的意思，跟javascript里的不等于判断符相同
**CSS Hack大致有3种表现形式**

CSS属性前缀法、选择器前缀法以及IE条件注释法（即HTML头部引用if IE）Hack，实际项目中CSS Hack大部分是针对IE浏览器不同版本之间的表现差异而引入的。

#### 属性前缀法(即类内部Hack)

例如 IE6能识别下划线""和星号" * "，IE7能识别星号" * "，但不能识别下划线""，IE6~IE10都认识"\9"，但firefox前述三个都不能认识

```
.all IE\\{property:value\9;\\}
.gte IE 8\\{property:value\0;\\}
.lte IE 7\\{*property:value;\\}
.IE 8/9\\{property:value\0;\\}
.IE 9\\{property:value\9\0;\\}
.IE 7\\{+property:value;\\}
.IE 6\\{_property:value;\\}
.not IE\\{property//:value;\\}
```

#### 选择器前缀法

(即选择器Hack)：例如 IE6能识别html .class\\{\\}，IE7能识别+html .class\\{\\}或者*:first-child+html .class\\{\\}。

#### IE条件注释法(即HTML条件注释Hack)

针对所有IE(注：IE10+已经不再支持条件注释)： ，针对IE6及以下版本： 。

这类Hack不仅对CSS生效，对写在判断语句里面的所有代码都会生效。



### 有一个导航栏在chrome 里面样式完好？在 IE 里文字都聚到一起了，是哪个兼容性问题？

 用了 display：flex 属性，在 ie10 以下都是无效的。



### 兼容各种浏览器版本的事件绑定

```js
/*
兼容低版本IE，ele为需要绑定事件的元素，
eventName为事件名（保持addEventListener语法，去掉on），fun为事件响应函数
*/
function addEvent(ele, eventName, fun) \\{
  if (ele.addEventListener) \\{
    ele.addEventListener(eventName, fun, false);
  \\} else \\{
    ele.attachEvent("on" + eventNme, fun);
  \\}
\\}
```



### const 问题

Firefox 下,可以使用 const 关键字或 var 关键字来定义常量;
IE 下,不能使用 const 关键字，只能使用 var 关键字来定义常量.
解决方法：统一使用 var 关键字来定义常量.



###  关于高度问题

如果是动态地添加内容，高度最好不要定义。

浏览器可以自动伸缩，然而如果是静态的内容，高度最好定好。

如果设定了高度，内容过多时，ie6 下会自动增加高度、其他浏览器会超出边框。

解决： 

1.设置 overflow:hidden;

2.高度自增 height:auto!important;height:100px;



### 为什么无法定义 1px 左右高度的容器

IE6 下这个问题是因为默认的行高造成的,解决的技巧也有很多：

例如:overflow:hidden 　 zoom:0.08 　 line-height:1px



### 页面的最小宽度

如上一个问题，IE 不识别 min，要实现最小宽度，可用下面的方法：

#container\\{ min-width: 600px; width:expression(document.body.clientWidth ＜ 600? "600px": "auto" );\\}

第一个 min-width 是正常的；但第 2 行的 width 使用了 Javascript，这只有 IE 才认得，这也会让你的 HTML 文档不太正规。它实际上通过 Javascript 的判断来实现最小宽度。



### 默认的内外边距不同

问题：

各个浏览器默认的内外边距不同

解决方案：

\*\\{margin:0;padding:0;\\}



### 水平居中的问题

问题：

- 设置 text-align: center
- ie6-7 文本居中，嵌套的块元素也会居中
- ff /opera /safari /ie8 文本会居中，嵌套块不会居中
  解决：
- 块元素设置
- 1、margin-left:auto;margin-right:auto
- 2、margin:0 auto;
- 3、<div align="center"></div>



### 垂直居中的问题

问题：
在浏览器中想要垂直居中，设置 vertical-align:middle; 不起作用。例如：ie6 下文本与文本输入框对不齐，需设置 vertical-align:middle，但是文本框的内容不会垂直居中

解决：
给容器设置一个与其高度相同的行高
line-height:与容器的 height 一样



### 除去滚动条的问题

问题：
隐藏滚动条
解决：
1、只有 ie6-7 支持<body scroll="no">
2、除 ie6-7 不支持 body\\{overflow:hidden\\}
3、所有浏览器 html\\{overflow:hidden\\}



### 子容器宽度大于父容器宽度时，内容超出

问题：
子 DIV 的宽度和父 DIV 的宽度都已经定义，在 IE6 中如果其子 DIV 的宽度大于父 DIV 的宽度，父 DIV 的宽度将会被扩展，在其他浏览器中父 DIV 的宽度将不会扩展，子 DIV 将超出父 DIV
解决：
设置 overflow:hidden，子 DIV 将不会超出父 DIV。



### HTML 对象获取问题

FireFox：document.getElementById("idName");
ie:document.idname 或者 document.getElementById("idName").
解决办法：统一使用 document.getElementById("idName");



### window.location.href 问题

说明:IE 或者 Firefox2.0.x 下,可以使用 window.location 或 window.location.href;
Firefox1.5.x 下,只能使用 window.location.

解决方法：使用 window.location 来代替 window.location.href.



### frame 问题

以下面的 frame 为例：

```html
<frame src="xxx.html" id="frameId" name="frameName" />
```

(1)访问 frame 对象:
IE:使用 window.frameId 或者 window.frameName 来访问这个 frame 对象. frameId 和 frameName 可以同名。
Firefox:只能使用 window.frameName 来访问这个 frame 对象.
另外，在 IE 和 Firefox 中都可以使用 window.document.getElementById("frameId")来访问这个 frame 对象.
(2)切换 frame 内容:
在 IE 和 Firefox 中都可以使用 window.document.getElementById("testFrame").src = "xxx.html"或 window.frameName.location = "xxx.html"来切换 frame 的内容.
如果需要将 frame 中的参数传回父窗口(注意不是 opener,而是 parent frame)，可以在 frame 中使用 parent 来访问父窗口。例如：parent.document.form1.filename.value="Aqing";



### 模态和非模态窗口问题

说明:IE 下,可以通过 showModalDialog 和 showModelessDialog 打开模态和非模态窗口;Firefox 下则不能.
解决方法：直接使用 window.open(pageURL,name,parameters)方式打开新窗口。
如果需要将子窗口中的参数传递回父窗口,可以在子窗口中使用 window.opener 来访问父窗口.
例如：var parWin = window.opener; parWin.document.getElementById("Aqing").value = "Aqing";



### firefox 与 IE 的父元素(parentElement)的区别

IE：obj.parentElement
firefox：obj.parentNode
解决方法: 因为 firefox 与 IE 都支持 DOM,因此使用 obj.parentNode 是不错选择.



### document.formName.item(”itemName”) 问题

问题说明：IE 下，可以使用 document.formName.item(”itemName”) 或 document.formName.elements ["elementName"]；Firefox 下，只能使用 document.formName.elements["elementName"]。
解决方法：统一使用 document.formName.elements["elementName"]。



### 集合类对象问题

问题说明：IE 下，可以使用 () 或 [] 获取集合类对象；Firefox 下，只能使用 [ ]获取集合类对象。
解决方法：统一使用 [] 获取集合类对象。



### 自定义属性问题

问题说明：IE 下，可以使用获取常规属性的方法来获取自定义属性，也可以使用 getAttribute() 获取自定义属性；Firefox 下，只能使用 getAttribute() 获取自定义属性。
解决方法：统一通过 getAttribute() 获取自定义属性。



### input.type 属性问题

问题说明：IE 下 input.type 属性为只读；但是 Firefox 下 input.type 属性为读写。
解决办法：不修改 input.type 属性。如果必须要修改，可以先隐藏原来的 input，然后在同样的位置再插入一个新的 input 元素。>



### event.srcElement 问题

问题说明：IE 下，even 对象有 srcElement 属性，但是没有 target 属性；Firefox 下，even 对象有 target 属性，但是没有 srcElement 属性。
解决方法：使用 srcObj = event.srcElement ?event.srcElement : event.target;
如果考虑第 8 条问题，就改用 myEvent 代替 event 即可。



### body 载入问题

问题说明：Firefox 的 body 对象在 body 标签没有被浏览器完全读入之前就存在；而 IE 的 body 对象则必须在 body 标签被浏览器完全读入之后才存在。
[注] 这个问题尚未实际验证，待验证后再来修改。
[注] 经验证，IE6、Opera9 以及 FireFox2 中不存在上述问题，单纯的 JS 脚本可以访问在脚本之前已经载入的所有对象和元素，即使这个元素还没有载入完成。



### 事件委托方法

问题说明：IE 下，使用 document.body.onload = inject; 其中 function inject()在这之前已被实现；在 Firefox 下，使用 document.body.onload = inject();
解决方法：统一使用 document.body.onload=new Function(’inject()’); 或者 document.body.onload = function()\\{\\}
[注意] Function 和 function 的区别。



### Table 操作问题

问题说明：ie、firefox 以及其它浏览器对于 table 标签的操作都各不相同，在 ie 中不允许对 table 和 tr 的 innerHTML 赋值，使用 js 增加一个 tr 时，使用 appendChild 方法也不管用。
解决方法：//向 table 追加一个空行：
var row = otable.insertRow(-1);var cell = document.createElement("td");cell.innerHTML = "";cell.className = "XXXX";row.appendChild(cell);[注] 由于俺很少使用 JS 直接操作表格，这个问题没有遇见过。建议使用 JS 框架集来操作 table，如 JQuery。



### 对象宽高赋值问题

问题说明：FireFox 中类似 obj.style.height = imgObj.height 的语句无效。

Ø CSS

1. cursor:hand VS cursor:pointer
   firefox 不支持 hand，但 ie 支持 pointer
   解决方法: 统一使用 pointer



### innerText 在 IE 中能正常工作，但在 FireFox 中却不行

需用 textContent。
解决方法:

```
if(navigator.appName.indexOf("Explorer") > -1)\\{
	document.getElementById('element').innerText = "my text";
\\}else\\{
	document.getElementById('element').textContent = "my text";
\\}
```



### CSS 透明

IE：filter:progid:DXImageTransform.Microsoft.Alpha(style=0,opacity=60)。
FF：opacity:0.6。
opacity 透明，子元素会继承透明属性。解决方式：

1、使用 background:rgba(0,0,0,.6) //IE8 及以下无效果。 

2、使用定位，背景色与子元素处于同级关系。



### css 中的 width 和 padding

在 IE7 和 FF 中 width 宽度不包括 padding，在 Ie6 中包括 padding.



### FF 和 IEBOX 模型解释不一致导致相差 2px

box.style\\{width:100;border 1px;\\}
ie 理解为 box.width = 100
ff 理解为 box.width = 100 + 1\*2 = 102 //加上边框 2px

解决方法：div\\{margin:30px!important;margin:28px;\\}
注意这两个 margin 的顺序一定不能写反， IE 不能识别!important 这个属性，但别的浏览器可以识别。所以在 IE 下其实解释成这样：div\\{maring:30px;margin:28px\\}
重复定义的话按照最后一个来执行，所以不可以只写 margin:XXpx!important;



### IE5 和 IE6 的 BOX 解释不一致

IE5 下 div\\{width:300px;margin:0 10px 0 10px;\\}
div 的宽度会被解释为 300px-10px(右填充)-10px(左填充)，最终 div 的宽度为 280px，而在 IE6 和其他浏览器上宽度则是以 300px+10px(右填充)+10px(左填充)=320px 来计算的。这时我们可以做如下修改 div\\{width:300px!important;width :340px;margin:0 10px 0 10px\\}



### ul 和 ol 列表缩进问题

消除 ul、ol 等列表的缩进时，样式应写成：list-style:none;margin:0px;padding:0px;
经验证，在 IE 中，设置 margin:0px 可以去除列表的上下左右缩进、空白以及列表编号或圆点，设置 padding 对样式没有影响；在 Firefox 中，设置 margin:0px 仅仅可以去除上下的空白，设置 padding:0px 后仅仅可以去掉左右缩进，还必须设置 list- style:none 才能去除列表编号或圆点。也就是说，在 IE 中仅仅设置 margin:0px 即可达到最终效果，而在 Firefox 中必须同时设置 margin:0px、 padding:0px 以及 list-style:none 三项才能达到最终效果。



### 元素水平居中问题

FF: margin:0 auto;

IE: 父级\\{ text-align:center; \\}



### Div 的垂直居中问题

vertical-align:middle; 将行距增加到和整个 DIV 一样高：line-height:200px; 然后插入文字，就垂直居中了。

缺点是要控制内容不要换行。



### margin 加倍的问题

设置为 float 的 div 在 ie 下设置的 margin 会加倍。这是一个 ie6 都存在的 bug。解决方案是在这个 div 里面加上 display:inline;

例如：

```htm1
<div id=”imfloat”>
相应的css为
#imfloat\\{
float:left;
margin:5px;
display:inline;\\}
```



### IE 与宽度和高度的问题

IE 不认得 min-这个定义，但实际上它把正常的 width 和 height 当作有 min 的情况来使。这样问题就大了，如果只用宽度和高度，正常的浏览器里这两个值就不会变，如果只用 min-width 和 min-height 的话，IE 下面根本等于没有设置宽度和高度。

比如要设置背景图片，这个宽度是比较重要的。要解决这个问题，可以这样：

#box\\{ width: 80px; height: 35px;\\}html>body #box\\{ width: auto; height: auto; min-width: 80px; min-height: 35px;\\}



### DIV 浮动 IE 文本产生 3 像素的 bug

左边对象浮动，右边采用外补丁的左边距来定位，右边对象内的文本会离左边有 3px 的间距.

#box\\{ float:left; width:800px;\\}
#left\\{ float:left; width:50\\%;\\}
#right\\{ width:50\\%;\\}
\*html #left\\{ margin-right:-3px; //这句是关键\\}

```
<div id="box">
<div id="left">＜/div>
<div id="right">＜/div>
```



### IE 捉迷藏的问题

当 div 应用复杂的时候每个栏中又有一些链接，DIV 等这个时候容易发生捉迷藏的问题。

有些内容显示不出来，当鼠标选择这个区域是发现内容确实在页面。

解决办法：对#layout 使用 line-height 属性或者给#layout 使用固定高和宽。页面结构尽量简单。



### float 的 div 闭合;清除浮动;自适应高度

① 例如：＜ div id=”floatA”>＜ div id=”floatB”>＜ div id=”NOTfloatC”>

这里的 NOTfloatC 并不希望继续平移，而是希望往下排。(其中 floatA、floatB 的属性已经设置为 float:left;)

这段代码在 IE 中毫无问题，问题出在 FF。原因是 NOTfloatC 并非 float 标签，必须将 float 标签闭合。在＜ div class=”floatB”>＜ div class=”NOTfloatC”>之间加上＜ div class=”clear”>这个 div 一定要注意位置，而且必须与两个具有 float 属性的 div 同级，之间不能存在嵌套关系，否则会产生异常。并且将 clear 这种样式定义为为如下即可：.clear\\{clear:both;\\}

② 作为外部 wrapper 的 div 不要定死高度,为了让高度能自适应，要在 wrapper 里面加上 overflow:hidden; 当包含 float 的 box 的时候，高度自适应在 IE 下无效，这时候应该触发 IE 的 layout 私有属性(万恶的 IE 啊！)用 zoom:1;可以做到，这样就达到了兼容。
例如某一个 wrapper 如下定义：

.colwrapper\\{overflow:hidden; zoom:1; margin:5px auto;\\}

③ 对于排版,我们用得最多的 css 描述可能就是 float:left.有的时候我们需要在 n 栏的 float div 后面做一个统一的背景,譬如:

```
<div id=”page”>
    <div id=”left”>＜/div>
	<div id=”center”>＜/div>
	<div id=”right”>＜/div>
</div>
```

比如我们要将 page 的背景设置成蓝色,以达到所有三栏的背景颜色是蓝色的目的,但是我们会发现随着 left center right 的向下拉长,而 page 居然保存高度不变,问题来了,原因在于 page 不是 float 属性,而我们的 page 由于要居中,不能设置成 float,所以我们应该这样解决：

```
<div id=”page”>
	<div id=”bg” style=”float:left;width:100\\%”>
		<div id=”left”>＜/div>
		<div id=”center”>＜/div>
		<div id=”right”>＜/div>
	</div>
</div>
```

再嵌入一个 float left 而宽度是 100\\%的 DIV 解决之。

或者另一种方法：用选择器（：after）在 page 之后插入一个空标签,并清除浮动

.page:after \\{ content: ""; display: table; clear: both; \\}

④ 万能 float 闭合(非常重要!)

关于 clear float 的原理可参见 [How To Clear Floats Without Structural Markup],将以下代码加入 Global CSS 中,给需要闭合的 div 加上 class="clearfix" 即可,屡试不爽。

```
.clearfix:after \\{ content:"."; display:block; height:0; clear:both; visibility:hidden; \\}
.clearfix \\{ display:inline-block; \\}

.clearfix \\{display:block;\\}
```

或者这样设置：.hackbox\\{ display:table; //将对象作为块元素级的表格显示\\}



### 高度不适应

高度不适应是当内层对象的高度发生变化时外层高度不能自动进行调节，特别是当内层对象使用 margin 或 padding 时。

例：

```
#box \\{ \\}
#box p \\{margin-top: 20px;margin-bottom: 20px; text-align:center; \\}
<div id="box">
<p>p对象中的内容＜/p>
</div>

解决技巧：在P对象上下各加2个空的div对象CSS代码\\{height:0px;overflow:hidden;\\}或者为DIV加上border属性。
</details>

<b><details><summary>32. IE6下图片下有空隙产生</summary></b>


解决这个BUG的技巧有很多,可以是改变html的排版,或者设置img为display:block或者设置vertical-align属性为vertical-align:top/bottom/middle/text-bottom 都可以解决.
</details>

<b><details><summary>33. 对齐文本与文本输入框</summary></b>


加上vertical-align:middle;

<style type="text/css">
<!--
input \\{
width:200px;
height:30px;
border:1px solid red;
vertical-align:middle;
\\}
-->
</style>

经验证，在IE下任一版本都不适用，而ff、opera、safari、chrome均OK！
```



### LI 中内容超过长度后以省略号显示

此技巧适用与 IE、Opera、safari、chrom 浏览器，FF 暂不支持。

```
<style type="text/css">
	li \\{
		width:200px;
		white-space:nowrap;
		text-overflow:ellipsis;
		-o-text-overflow:ellipsis;
		overflow: hidden;
	\\}
</style>
```



### 为什么 web 标准中 IE 无法设置滚动条颜色了

```
解决办法是将body换成html

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<meta http-equiv="Content-Type" content="text/html; charset=gb2312" />
<style type="text/css">
<!--
html \\{
scrollbar-face-color:#f6f6f6;
scrollbar-highlight-color:#fff;
scrollbar-shadow-color:#eeeeee;
scrollbar-3dlight-color:#eeeeee;
scrollbar-arrow-color:#000;
scrollbar-track-color:#fff;
scrollbar-darkshadow-color:#fff;
\\}
-->
＜/style>
```



### 怎么样才能让层显示在 FLASH 之上呢

```
解决的办法是给FLASH设置透明
<param name="wmode" value="transparent" />
```



### 链接(a 标签)的边框与背景

a 链接加边框和背景色，需设置 display: block, 同时设置 float: left 保证不换行。参照 menubar, 给 a 和 menubar 设置高度是为了避免底边显示错位, 若不设 height, 可以在 menubar 中插入一个空格。



### 超链接访问过后 hover 样式就不出现的问题

```
被点击访问过的超链接样式不在具有hover和active了,很多人应该都遇到过这个问题,解决技巧是改变CSS属性的排列顺序: L-V-H-A

Code:

<style type="text/css">
<!--
a:link \\{\\}
a:visited \\{\\}
a:hover \\{\\}
a:active \\{\\}
-->
</style>
```



### FORM 标签

这个标签在 IE 中,将会自动 margin 一些边距,而在 FF 中 margin 则是 0,因此,如果想显示一致,所以最好在 css 中指定 margin 和 padding,针对上面两个问题,我的 css 中一般首先都使用这样的样式 ul,form\\{margin:0;padding:0;\\}。



### 属性选择器(这个不能算是兼容,是隐藏 css 的一个 bug)

p[id]\\{\\}div[id]\\{\\}

这个对于 IE6.0 和 IE6.0 以下的版本都隐藏,FF 和 OPera 作用.属性选择器和子选择器还是有区别的,子选择器的范围从形式来说缩小了,属性选择器的范围比较大,如 p[id]中,所有 p 标签中有 id 的都是同样式的.



### 为什么 FF 下文本无法撑开容器的高度

标准浏览器中固定高度值的容器是不会象 IE6 里那样被撑开的,那我又想固定高度,又想能被撑开需要怎样设置呢？办法就是去掉 height 设置 min-height:200px; 这里为了照顾不认识 min-height 的 IE6 可以这样定义:

```
\\{
	height:auto!important;
	height:200px;
	min-height:200px;
\\}
```



### IE 和 FireFox 对空格的尺寸解释不同，FireFox 为 4px,IE 为 8px;

FireFox 对 div 与 div 之间的空格是忽略的，但是 IE 是处理的。因此在两个相邻 div 之间不要有空格跟回车，否则可能造成不同浏览间之间格式不正确，比如著名的 3px 偏差（多个 img 标签连着，然后定义 float: left;结果在 firefox 里面正常，而 IE 里面显示的每个 img 都相隔了 3px。我把标签之间的空格都删除都没有作用。解决方法是在 img 外面套 li，并且对 li 定义 margin: 0; 避免方式：在必要的时候不要无视 list 标签）而且原因难以查明。



### 条件注释

```
<link rel="stylesheet" type="text/css" href="css.css" />

<!--[if IE 7]>
<link rel="stylesheet" type="text/css" href="ie7.css" />
<![endif]-->

<!--[if lte IE 6]>
<link rel="stylesheet" type="text/css" href="ie.css" />
<![endif]-->

lte -- 小于等于
lt  -- 小于
gte --  大于等于
gt  --  大于
！ --  不等于
```



### 强制渲染

```
<meta http-equiv=X-UA-Compatible content=IE=EmulateIE7>    //这句话的意思是强制使用IE7模式来解析网页代码！

<meta http-equiv=“X-UA-Compatible” content=“IE=8″>

<meta http-equiv=“X-UA-Compatible” content=“chrome=1″ />    //Google Chrome Frame也可以让IE用上Chrome的引擎

<meta http-equiv=“X-UA-Compatible” content=“IE=EmulateIE7″><!– IE7 mode –> 或者 <meta http-equiv=“X-UA-Compatible” content=“IE=7″><!– IE7 mode –>       //强制IE8使用IE7模式来解析

<meta http-equiv=“X-UA-Compatible” content=“IE=6″><!– IE6 mode –>   <meta http-equiv=“X-UA-Compatible” content=“IE=5″><!– IE5 mode –>   //强制IE8使用IE6或IE5模式来解析

<meta http-equiv=“X-UA-Compatible” content=“IE=5; IE=8″ />   //一个特定版本的IE支持所要求的兼容性模式多于一种
```



### js 兼容文件

```
使IE5,IE6兼容到IE7模式（推荐）

<!–[if lt IE 7]>
<script src=”http://ie7-js.googlecode.com/svn/version/2.0(beta)/IE7.js” type=”text/javascript”></script>
<![endif]–>
使IE5,IE6,IE7兼容到IE8模式

<!–[if lt IE 8]>
<script src=”http://ie7-js.googlecode.com/svn/version/2.0(beta)/IE8.js” type=”text/javascript”></script>
<![endif]–>
使IE5,IE6,IE7,IE8兼容到IE9模式

<!–[if lt IE 9]>
<script src=”http://ie7-js.googlecode.com/svn/version/2.1(beta4)/IE9.js”></script>
<![endif]–>
```



### 浏览器识别符

```
p\\{ \_color:red; \\} IE6 专用
*html p\\{ color:#red; \\} IE6 专用
p\\{ +color:red; \\} IE6,7 专用
p\\{ *color:red; \\} IE6,7 专用
_html p\\{ color:red; \\} IE6,7 专用
p\\{_+color: red;\\} IE7 专用
Body> p\\{ color: red; \\} 屏蔽 IE6
p\\{ color:red\9; \\} IE8

Firefox: -moz-
Safari: -webkit-
Opera: -o-
IE: -ms-
```







## 移动端兼容

### 添加到主屏后的标题（IOS）

```html
<meta name="apple-mobile-web-app-title" content="标题" />
```



### 启用 WebApp

```
全屏模式（IOS）
当网站添加到主屏幕后再点击进行启动时，可隐藏地址栏（从浏览器跳转或输入链接进入并没有此效果）

<meta name="apple-mobile-web-app-capable" content="yes" />

<meta name="apple-touch-fullscreen" content="yes" />
```



### 百度禁止转码

```
通过百度手机打开网页时，百度可能会对你的网页进行转码，往你页面贴上它的广告，非常之恶心。不过我们可以通过这个meta标签来禁止它：

<meta http-equiv="Cache-Control" content="no-siteapp" />

百度SiteApp转码声明：http://t.cn/R28wSBl
```



### 设置状态栏的背景颜色（IOS）

```
设置状态栏的背景颜色，只有在"apple-mobile-web-app-capable" content="yes"时生效

<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />

content 参数：

· default ：状态栏背景是白色。

· black ：状态栏背景是黑色。

· black-translucent ：状态栏背景是半透明。 如果设置为 default 或 black ,网页内容从状态栏底部开始。
如果设置为 black-translucent ,网页内容充满整个屏幕，顶部会被状态栏遮挡。
```



### 移动端手机号码识别（IOS）

```

在 iOS Safari （其他浏览器和Android均不会）上会对那些看起来像是电话号码的数字处理为电话链接，比如：

· 7位数字，形如：1234567

· 带括号及加号的数字，形如：(+86)123456789

· 双连接线的数字，形如：00-00-00111

· 11位数字，形如：13800138000

可能还有其他类型的数字也会被识别。我们可以通过如下的meta来关闭电话号码的自动识别：

<meta name="format-detection" content="telephone=no" />

开启电话功能

<a href="tel:123456">123456</a>

开启短信功能：

<a href="sms:123456">123456</a>
```



### 移动端邮箱识别（Android）

```
与电话号码的识别一样，在安卓上会对符合邮箱格式的字符串进行识别，我们可以通过如下的meta来管别邮箱的自动识别：

<meta content="email=no" name="format-detection" />

同样地，我们也可以通过标签属性来开启长按邮箱地址弹出邮件发送的功能：

<a mailto:dooyoe@gmail.com">dooyoe@gmail.com</a>
```



### 添加智能 App

```
广告条 Smart App Banner（IOS 6+ Safari）
<meta name="apple-itunes-app" content="app-id=myAppStoreID, affiliate-data=myAffiliateData, app-argument=myURL">
```



### IOS Web app 启动动画

```
由于iPad 的启动画面是不包括状态栏区域的。所以启动图片需要减去状态栏区域所对应的方向上的20px大小，相应地在retina设备上要减去40px的大小。

<link href="apple-touch-startup-image-320×460.png" media="(device-width: 320px)" rel="apple-touch-startup-image">

<link href="apple-touch-startup-image-640×960.png" media="(device-width: 320px) and (-webkit-device-pixel-ratio: 2)" rel="apple-touch-startup-image">

<link href="apple-touch-startup-image-768×1004.png" media="(device-width: 768px) and (orientation: portrait)" rel="apple-touch-startup-image">

<link href="apple-touch-startup-image-748×1024.png" media="(device-width: 768px) and (orientation: landscape)" rel="apple-touch-startup-image">

<link href="apple-touch-startup-image-1536×2008.png" media="(device-width: 1536px) and (orientation: portrait) and (-webkit-device-pixel-ratio: 2)" rel="apple-touch-startup-image">

<link href="apple-touch-startup-image-2048×1496.png" media="(device-width: 1536px)  and (orientation: landscape) and (-webkit-device-pixel-ratio: 2)" rel="apple-touch-startup-image">

（landscape：横屏 | portrait：竖屏）
```



### 添加到主屏后的 APP 图标

```
指定web app添加到主屏后的图标路径，有两种略微不同的方式：

<!– 设计原图 –>

<link href="short_cut_114x114.png" rel="apple-touch-icon-precomposed">

<!– 添加高光效果 –>

<link href="short_cut_114x114.png" rel="apple-touch-icon">

· apple-touch-icon：在IOS6及以下的版本会自动为图标添加一层高光效果（IOS7开始已使用扁平化的设计风格）

· apple-touch-icon-precomposed：使用“设计原图图标”

效果：



图标尺寸：

可通过指定size属性来为不同的设备提供不同的图标（但通常来说，我们只需提供一个114 x 114 pixels大小的图标即可 ）

官方说明如下：

Create different sizes of your app icon for different devices. If you’re creating a universal app, you need to supply app

icons in all four sizes.

For iPhone and iPod touch both of these sizes are required:

57 x 57 pixels

114 x 114 pixels (high resolution)

For iPad, both of these sizes are required:

72 x 72 pixels

144 x 144 (high resolution)
```



### 优先使用最新版本 IE 和 Chrome

```
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
```



### viewport 模板

```
<html>

<head>
<meta charset="utf-8">
<meta content="width=device-width,initial-scale=1.0,maximum-scale=1.0,user-scalable=no" name="viewport">
<meta content="yes" name="apple-mobile-web-app-capable">
<meta content="black" name="apple-mobile-web-app-status-bar-style">
<meta content="telephone=no" name="format-detection">
<meta content="email=no" name="format-detection">
<title>标题</title>
<link rel="stylesheet" href="index.css">
</head>

<body>
这里开始内容
</body>

</html>
```



### 移动端如何定义字体 font-family

```
三大手机系统的字体：

iOS 系统
· 默认中文字体是Heiti SC
· 默认英文字体是Helvetica
· 默认数字字体是HelveticaNeue
· 无微软雅黑字体

Android 系统
· 默认中文字体是Droidsansfallback
· 默认英文和数字字体是Droid Sans
· 无微软雅黑字体

Winphone 系统
· 默认中文字体是Dengxian(方正等线体)
· 默认英文和数字字体是Segoe
· 无微软雅黑字体

各个手机系统有自己的默认字体，且都不支持微软雅黑，如无特殊需求，手机端无需定义中文字体，使用系统默认英文字体和数字字体可使用 Helvetica ，三种系统都支持。

* 移动端定义字体的代码 */

body\\{font-family:Helvetica;\\}
```



### 移动端字体单位 font-size 选择 px 还是 rem

```
· 对于只需要适配手机设备，使用px即可

· 对于需要适配各种移动设备，使用rem，例如只需要适配iPhone和iPad等分辨率差别比较挺大的设备

rem配置参考：
html \\{font-size:10px\\}
@media screen and (min-width:480px) and (max-width:639px) \\{
    html \\{
        font-size: 15px
    \\}
\\}

@media screen and (min-width:640px) and (max-width:719px) \\{
    html \\{
        font-size: 20px
    \\}
\\}

@media screen and (min-width:720px) and (max-width:749px) \\{
    html \\{
        font-size: 22.5px
    \\}
\\}

@media screen and (min-width:750px) and (max-width:799px) \\{
    html \\{
        font-size: 23.5px
    \\}
\\}

@media screen and (min-width:800px) and (max-width:959px) \\{
    html \\{
        font-size: 25px
    \\}
\\}

@media screen and (min-width:960px) and (max-width:1079px) \\{
    html \\{
        font-size: 30px
    \\}
\\}

@media screen and (min-width:1080px) \\{
    html \\{
        font-size: 32px
    \\}
\\}
```



### 移动端 touch 事件(区分 webkit 和 winphone)

当用户手指放在移动设备在屏幕上滑动会触发的touch事件

以下支持webkit

· touchstart——当手指触碰屏幕时候发生。不管当前有多少只手指

· touchmove——当手指在屏幕上滑动时连续触发。通常我们再滑屏页面，会调用event的preventDefault()可以阻止默认情况的发生：阻止页面滚动

· touchend——当手指离开屏幕时触发

· touchcancel——系统停止跟踪触摸时候会触发。例如在触摸过程中突然页面alert()一个提示框，此时会触发该事件，这个事件比较少用

以下支持winphone 8

· MSPointerDown——当手指触碰屏幕时候发生。不管当前有多少只手指

· MSPointerMove——当手指在屏幕上滑动时连续触发。通常我们再滑屏页面，会调用css的html\\{-ms-touch-action:
none;\\}可以阻止默认情况的发生：阻止页面滚动

· MSPointerUp——当手指离开屏幕时触发



### 移动端 click 屏幕产生 200-300 ms 的延迟响应

移动设备上的web网页是有300ms延迟的，玩玩会造成按钮点击延迟甚至是点击失效。

以下是历史原因：

2007年苹果发布首款iphone上IOS系统搭载的safari为了将适用于PC端上大屏幕的网页能比较好的展示在手机端上，使用了双击缩放 (double tap to zoom)的方案，比如你在手机上用浏览器打开一个PC上的网页，你可能在看到页面内容虽然可以撑满整个屏幕，但是字体、图片都很小看不清，此时可以快速 双击屏幕上的某一部分，你就能看清该部分放大后的内容，再次双击后能回到原始状态。

双击缩放是指用手指在屏幕上快速点击两次，iOS 自带的 Safari 浏览器会将网页缩放至原始比例。

原因就出在浏览器需要如何判断快速点击上，当用户在屏幕上单击某一个元素时候，例如跳转链接，此处浏览器会先捕获该次单击，但浏览器不能决定用户是
单纯要点击链接还是要双击该部分区域进行缩放操作，所以，捕获第一次单击后，浏览器会先Hold一段时间t，如果在t时间区间里用户未进行下一次点击，则 浏览器会做单击跳转链接的处理，如果t时间里用户进行了第二次单击操作，则浏览器会禁止跳转，转而进行对该部分区域页面的缩放操作。那么这个时间区间t有 多少呢？在IOS safari下，大概为300毫秒。这就是延迟的由来。造成的后果用户纯粹单击页面，页面需要过一段时间才响应，给用户慢体验感觉，对于web开发者来说
是，页面js捕获click事件的回调函数处理，需要300ms后才生效，也就间接导致影响其他业务逻辑的处理。

解决方案：

· fastclick可以解决在手机上点击事件的300ms延迟

· zepto的touch模块，tap事件也是为了解决在click的延迟问题

触摸事件的响应顺序

1、ontouchstart

2、ontouchmove

3、ontouchend

4、onclick

解决300ms延迟的问题，也可以通过绑定ontouchstart事件，加快对事件的响应。



### 什么是 Retina

```
显示屏，带来了什么问题
retina：一种具备超高像素密度的液晶屏，同样大小的屏幕上显示的像素点由1个变为多个，如在同样带下的屏幕上，苹果设备的retina显示屏中，像素点1个变为4个

在高清显示屏中的位图被放大，图片会变得模糊，因此移动端的视觉稿通常会设计为传统PC的2倍。

那么，前端的应对方案是：

设计稿切出来的图片长宽保证为偶数，并使用backgroud-size把图片缩小为原来的1/2

//例如图片宽高为：200px*200px，那么写法如下

.css\\{width:100px;height:100px;background-size:100px 100px;\\}

其它元素的取值为原来的1/2，例如视觉稿40px的字体，使用样式的写法为20px

.css\\{font-size:20px\\}
```



### ios 系统中元素被触摸时产生的半透明灰色遮罩怎么去掉

```
ios用户点击一个链接，会出现一个半透明灰色遮罩, 如果想要禁用，可设置-webkit-tap-highlight-color的alpha值为0，也就是属性值的最后一位设置为0就可以去除半透明灰色遮罩。

a,button,input,textarea\\{-webkit-tap-highlight-color: rgba(0,0,0,0;)\\}
```



### 部分 android 系统中元素被点击时产生的边框怎么去掉

```
android用户点击一个链接，会出现一个边框或者半透明灰色遮罩, 不同生产商定义出来额效果不一样，可设置-webkit-tap-highlight-color的alpha值为0去除部分机器自带的效果。
a,button,input,textarea\\{
    -webkit-tap-highlight-color: rgba(0,0,0,0;)
    -webkit-user-modify:read-write-plaintext-only;
\\}
-webkit-user-modify有个副作用，就是输入法不再能够输入多个字符。
另外，有些机型去除不了，如小米2
对于按钮类还有个办法，不使用a或者input标签，直接用div标签
```



### winphone 系统 a、input 标签被点击时产生的半透明灰色背景怎么去掉

```
<meta name="msapplication-tap-highlight" content="no">
```



### webkit 表单元素的默认外观怎么重置

```
.css\\{-webkit-appearance:none;\\}
```



### webkit 表单输入框 placeholder 的颜色值能改变么

```
input::-webkit-input-placeholder\\{color:#AAAAAA;\\}
input:focus::-webkit-input-placeholder\\{color:#E
```



### webkit 表单输入框 placeholder 的文字能换行么

```
iOS可以，Android不行~
1. 关闭iOS键盘首字母自动大写
在iOS中，默认情况下键盘是开启首字母大写的功能的，如果启用这个功能，可以这样：
<input type="text" autocapitalize="off" />
```



### 关闭 iOS 输入自动修正

```
和英文输入默认自动首字母大写那样，IOS还做了一个功能，默认输入法会开启自动修正输入内容，这样的话，用户经常要操作两次。如果不希望开启此功能，我们可以通过input标签属性来关闭掉：
<input type="text" autocorrect="off" />
```



### 禁止文本缩放

```
当移动设备横竖屏切换时，文本的大小会重新计算，进行相应的缩放，当我们不需要这种情况时，可以选择禁止：
html \\{
       -webkit-text-size-adjust: 100\\%;
\\}
需要注意的是，PC端的该属性已经被移除，该属性在移动端要生效，必须设置 meta viewport。
```



### 移动端如何清除输入框内阴影

```
在iOS上，输入框默认有内部阴影，但无法使用 box-shadow 来清除，如果不需要阴影，可以这样关闭：
input,
textarea \\{
border: 0; /* 方法1 */
-webkit-appearance: none; /* 方法2 */
\\}
```



### 移动端取消 touch 高亮效果

在做移动端页面时，会发现所有 a 标签在触发点击时或者所有设置了伪类 :active 的元素，默认都会在激活状态时，显示高亮框，如果不想要这个高亮，那么你可以通过 css 以下方法来进行全局的禁止：

html \\{

    -webkit-tap-highlight-color: rgba(0, 0, 0, 0);

\\}

但这个方法在三星的机子上无效，有一种妥协的方法是把页面非真实跳转链接的 a 标签换成其它标签，可以解决这个问题。



### 如何禁止保存或拷贝图像（IOS）

通常当你在手机或者 pad 上长按图像 img ，会弹出选项存储图像 或者拷贝图像，如果你不想让用户这么操作，那么你可以通过以下方法来禁止：

img \\{ -webkit-touch-callout: none; \\}



### 模拟按钮 hover 效果

```
移动端触摸按钮的效果，可明示用户有些事情正要发生，是一个比较好体验，但是移动设备中并没有鼠标指针，使用css的hover并不能满足我们的需求，还好国外有个激活css的active效果，代码如下，

<html>
<head>

<meta charset="utf-8">
<meta content="width=device-width,initial-scale=1.0,maximum-scale=1.0,user-scalable=no" name="viewport">
<meta content="yes" name="apple-mobile-web-app-capable">
<meta content="black" name="apple-mobile-web-app-status-bar-style">
<meta content="telephone=no" name="format-detection">
<meta content="email=no" name="format-detection">

<style type="text/css">
a\\{-webkit-tap-highlight-color: rgba(0,0,0,0);\\}
.btn-blue\\{display:block;height:42px;line-height:42px;text-align:center;border-radius:4px;font-size:18px;color:#FFFFFF;background-color: #4185F3;\\}
.btn-blue:active\\{background-color: #357AE8;\\}
</style>

</head>
<body>

<div class="btn-blue">按钮</div>

<script type="text/javascript">
document.addEventListener("touchstart", function()\\{\\}, true)
</script>
</body>
</html>

兼容性ios5+、部分android 4+、winphone 8

要做到全兼容的办法，可通过绑定ontouchstart和ontouchend来控制按钮的类名。

<html>
<head>

<meta charset="utf-8">
<meta content="width=device-width,initial-scale=1.0,maximum-scale=1.0,user-scalable=no" name="viewport">
<meta content="yes" name="apple-mobile-web-app-capable">
<meta content="black" name="apple-mobile-web-app-status-bar-style">
<meta content="telephone=no" name="format-detection">
<meta content="email=no" name="format-detection">

<style type="text/css">
a\\{-webkit-tap-highlight-color: rgba(0,0,0,0);\\}
.btn-blue\\{display:block;height:42px;line-height:42px;text-align:center;border-radius:4px;font-size:18px;color:#FFFFFF;background-color: #4185F3;\\}
.btn-blue-on\\{background-color: #357AE8;\\}
</style>

</head>

<body>
<div class="btn-blue">按钮</div>

<script type="text/javascript">
var btnBlue = document.querySelector(".btn-blue");
btnBlue.ontouchstart = function()\\{
    this.className = "btn-blue btn-blue-on"
\\}
btnBlue.ontouchend = function()\\{
    this.className = "btn-blue"
\\}
</script>

</body>
</html>
```



### 屏幕旋转的事件和样式事件

```
window.orientation，取值：正负90表示横屏模式、0和180表现为竖屏模式；
window.onorientationchange = function()\\{
            switch(window.orientation)\\{
                case -90:
                case 90:
                alert("横屏:" + window.orientation);
                case 0:
                case 180:
                alert("竖屏:" + window.orientation);
                break;
          \\}
\\}

样式
//竖屏时使用的样式
@media all and (orientation:portrait) \\{
    .css\\{\\}
\\}

//横屏时使用的样式
@media all and (orientation:landscape) \\{
    .css\\{\\}
\\}
```



### audio 元素和 video 元素在 ios 和 andriod 中无法自动播放

应对方案：触屏即播

```
$(‘html’).one(‘touchstart’,function()\\{
audio.play()
\\})
```



### 摇一摇功能

HTML5 deviceMotion：封装了运动传感器数据的事件，可以获取手机运动状态下的运动加速度等数据。



### 手机拍照和上传图片

```
<input type="file">的accept 属性

<!– 选择照片 –>
<input type=file accept="image/*">

<!– 选择视频 –>
<input type=file accept="video/*">

使用总结：
· iOS有拍照、录像、选取本地图片功能
· 部分android只有选取本地图片功能
· winphone不支持
· input控件默认外观丑陋
```







## 不常用

### android 上去掉语音输入按钮

input::-webkit-input-speech-button \\{display: none\\}



### 不同浏览器的标签默认外补丁 margin 和内补丁 padding 不同

发生概率：100\\%

解决方案：使用 CSS 通配符\*，设置内外补丁为 0

\*\\{ margin: 0; padding: 0;\\}



### 块属性标签 float 之后，又有横向的 margin 值，在 IE6 中显示会比设置的大（IE6 双边距 bug）

解决方案：在 float 标签样式控制中加入 display:inline;



### 设置较小的高度标签（一般小于 10px），在 IE6，IE7，遨游中超出自己设置的高度

发生概率：60\\%

解决方案：给超出高度的标签设置 overflow:hidden;或者设置行高 line-height 小于你设置的高度。



### 行内标签设置 display:block;后又采用 float 布局，再设置横向 margin 值时，在 IE6 中显示会比设置的大（IE6 双边距 bug）

发生概率：20\\%

解决方案：在 display:block;后面加上 display:inline;display:table;



### 图片默认有间距

发生概率：20\\%

解决方案：使用 float 为 img 布局



### 标签最低高度设置 min-height 不兼容

发生概率：5\\%

解决方案：例如要设置一个标签的最小高度为 200px

\\{ min-height: 200px;

height: auto!important;

height: 200px;

overflow: visible;\\}



### 透明度兼容设置

发生概率：主要看你要写的东西设不设透明度

解决方案：一句话

    transparent_class \\{
    	filter:alpha(opacity=50);
    
       -moz-opacity:0.5;
    
       -khtml-opacity: 0.5;
    
       opacity: 0.5;
    \\}

opacity:0.5; This is the “most important” one because it is the currentstandard in CSS. This will work in most versions of Firefox, Safari, andOpera.This would be all you need if all browsers supported current standards. Which,of course, they don’t.

filter:alpha(opacity=50); This one you need for IE.

-moz-opacity:0.5; You need this one to support way old school versions of theMozilla browsers like Netscape Navigator.

-khtml-opacity:0.5; This is for way old versions of Safari (1.x) when therendering engine it was using was still referred to as KTHML, asopposed to thecurrent WebKit .



### Box Model 的 bug

描述：给一个元素设置了高度和宽度的同时，还为其设置 margin 和 padding 的值，会改变该元素的实际大小。

解决办法：在需要加 margin 和 padding 的 div 内部加一个 div,在这个 div 里设置 margin 和 padding 值。



### IE6 中的列表 li 楼梯状 bug

描述：通常在 li 中的元素（比如 a）设置了浮动 float，但 li 本身不浮动。

解决办法：

ul li\\{float:left;\\}

或 ul li\\{display:inline;\\}



### li 空白间距

描述：在 IE 下，会增加 li 和 li 之间的垂直间距

解决办法：给 li 里的 a 显式的添加宽度或者高度

li a\\{width:20px;\\}

或者

li a\\{display:block;float:left;clear:left;\\}

或者

li \\{display:inline;\\}

li a\\{display:block;\\}

或者

在每个列表 li 上设置一个实线的底边，颜色和 li 的背景色相同



### overflow：auto;和 position:relative 的碰撞

描述：此 bug 只出现在 IE6 和 IE7 中，有两个块级元素，父元素设置了 overflow：auto;子元素设置了 position:relative;且高度大于父元素，在 IE6-7 中子元素不会被隐藏而是溢出。

解决方案：给父元素也设置 position:relative;



### 浮动层的错位

描述：当内容超出外包容器定义的宽度时会导致浮动层错位问题。在 Firefox、IE7、IE8 及其他标准浏览器里,超出的内容仅仅只是超出边缘;但在 IE6 中容器会忽视定义的 width 值,宽度会错误地随内容宽度增长而增长。如果在这个浮动元素之后还跟着一个浮动元素,那么就会导致错位问题。

解决方案：overflow：hidden;



### IE6 克隆文本的 bug

描述：若你的代码结构如下

```
<!--这是注释-->

    <div>
    
       ……

   </div>

<!--这是注释-->
```

很有可能在 IE6 网页上出现一段空白文本

解决方案：

使用条件注释

删除所有注释

在注释前面的那个浮动元素加上 display：inline；



### IE 的图片缩放

描述：图片在 IE 下缩放有时会影响其质量

解决方案：img\\{ -mg-interpolation-mode:bicubic;\\}



### IE6 下 png 图片的透明 bug

描述：使用透明图片,使用 png24 或 png32 图片在 IE6 下面显示图片会有一层淡蓝色的背景。

解决方案：

```css
.img\\{

background:url('http://shenmo.wanmei.com/images/logo/sm_logo_202x104.png');

_background:0;

_filter:progid:DXImageTransform.Microsoft.AlphaImageLoader(src='http://shenmo.wanmei.com/images/logo/sm_logo_202x104.png',sizingMethod='scale');

\\}

img\\{filter:progid:DXImageTransform.Microsoft.AlphaImageLoader(src='http://shenmo.wanmei.com/images/logo/sm_logo_202x104.png',sizingMethod='scale');\\}

或

<imgsrc="test.png" width="247" height="216"style="filter:progid:DXImageTransform.Microsoft.AlphaImageLoader(src='http://shenmo.wanmei.com/images/logo/sm_logo_202x104.png',sizingMethod='scale');" alt="" />
```



### `<iframe>`透明背景 bug

描述：在 IE 浏览器中，<iframe>框架不会自动把背景设为透明

解决方案：

<iframesrc="content.html"allowTransparency="true"></iframe>

在 iframe 调用的 content.html 页面中设置

body\\{background-color: transparent;\\}



### 禁用 IE 默认的垂直滚动条

解决方案：

html\\{

overflow:auto;

\\}



### IE6 默认的 div 高度

问题：
ie6 默认 div 高度为一个字体显示的高度，所在 ie6 下 div 的高度大于等于一个字的高度，因此在 ie6 下定义高度为 1px 的容器，显示的是一个字体的高度
解决：
为这个容器设置下列属性之一
1、设置 overflow:hidden;
2、设置 line-height:1px;
3、设置 zoom:0.08



### IE6 最小高度(宽度)的问题

问题：
ie6 不支持 min-height、min-width 属性，默认 height 是最小高度，width 是最小宽度。
解决：
使用 ie6 不支持但其余浏览器支持的属性!important。
设置属性 min-height:200px; height:auto !important; height:200px;

 

### td 高度的问题

问题：
table 中 td 的宽度都不包含 border 的宽度，但是 oprea 和 ff 中 td 的高度包含了 border 的高度
解决：
设置 line-height 和 height 一样。在 ie 中如果 td 中的没有内容，那么 border 将不会显示



### div 嵌套 p 时，出现空白行

问题：
div 中显示<p>文本</p>，ff、oprea、Chrome：top 和 bottom 都会出现空白行，但是在 ie 下不会出现空白行。
解决：
设置 p 的 margin:0px，再设置 div 的 padding-top 和 padding-bottom



### IE6-7 图片下面有空隙的问题

问题：
块元素中含有图片时，ie6-7 中会出现图片下有空隙
解决：
1、在源代码中让</div>和<img>在同一行
2、将图片转换为块级对象 display:block;
3、设置图片的垂直对齐方式 vertical-align:top/middle/bottom
4、改变父对象的属性，如果父对象的宽、高固定，图片大小随父对象而定，那么可以对父元素设置： overflow:hidden;
5、设置图片的浮动属性 float:left;



### IE6 双倍边距的问题

    问题：
    ie6 中设置浮动，同时又设置 margin 时，会出现双倍边距的问题
    例 float:left;width:100px;margin:0 100px;
    解决：
    设置 display:inline;



### IE6 width 为奇数，右边多出 1px 的问题

    问题：
    父级元素采用相对定位，且宽度设置为奇数时，子元素采用绝对定位，在 ie6 中会出现右侧多出 1 像素
    解决：
    将宽度的奇数值改成偶数



### IE6 两个层之间 3px 的问题

    问题：
    左边层采用浮动，右边没有采用浮动，这时在 ie6 中两层之间就会产生 3 像素的间距
    解决：
    1、右边层也采用浮动 float
    2、左边层添加属性 margin-right:-3px;



### IE6 子元素绝对定位的问题

    问题：
    父级元素使用 padding 后，子元素使用绝对定位，不能精确定位
    解决：
    在子元素中设置 \_left:-20px; \_top:-1px;



### 显示手型 cursor:hand

    问题：
    ie6/7/8、opera 都支持
     但是 safari 、 ff 不支持
    解决：
    写成 cursor:pointer; (所有浏览器都能识别)



### IE6-7 line-height 失效的问题

    问题：
    在 ie 中 img 与文字放一起时， line-height 不起作用
    解决：
    都设置成 float



### td 自动换行的问题

    问题：
    Table 宽度固定，td 自动换行
    解决：
    设置 Table 的 table-layout:fixed，td 的 word-wrap:break-word



### 子容器浮动后，父容器扩展问题

    问题：
    子容器都 float 以后，父容器没有设定高度,父容器将不会扩展
    解决：
    只需要添加一个 clear:both 的 div，代码如下：

```html
<div style="border:1px solid#333;width:204px">
    <divstyle="width:100px;border:1px solid #333; float:left; ">子容器a</div>
    <divstyle="width:100px;border:1px solid #333; float:left;">子容器b</div>
    <divstyle="clear:both"></div>
</div>
```



### 透明 png 图片会带背景色

    问题：
    在 ie6 下透明的 png 图片会带一个背景色
    解决：
    background-image: url(icon_home.png);
    background-repeat: no-repeat;
    \_filter:progid:DXImageTransform.Microsoft.AlphaImageLoader(src='icon_home.png');
    \_background-image: none;



### list-style-position 默认值的问题

    问题：
    ie 下 list-style-position 默认为 inside, firefox 默认为 outside
    解决：
    css 中指定为 outside 即可解决兼容性问题



### list-style-image 准确定位的问题

    问题：
    li 前设置图片时，图片与其后的文字对齐问题
    解决：
    1、采用背景定位 和 字符缩进的方法
    background:url() no-repeat left center;text-index:16px;
    2、采用相对定位方法
    li 设置 list-style:url();
    li 的子元素 position:relative;top:-5px;



### ul 标签默认值的问题

    问题：
    ul 标签在 ff 中默认是有 padding 值的,而在 ie 中只有 margin 有值
    解决：
    定义 ul\\{margin:0;padding:0;\\}就能解决大部分问题



### IE 中 li 指定高度后，出现排版错误

    问题：
    在 ie 下如果为 li 指定高度可能会出现排版错位
    解决：
    设置 line-height



### ul 或 li 浮动后，显示在 div 外

    问题：
    div 中的 ul 或 li 设置 float 以后，都不在 div 中
    解决：
    必须在 ul 标签后加<div style="clear:both"></div>来闭合外层 div



### ul 浮动后，margin 变大

    问题：
    ul 设置 float 后，在 ie 中 margin 将变大
    解决：
    设置 ul 的 display:inline，li 的 list-style-position:outside



### li 浮动后，margin 变大

    问题：
    li 设置 float 后，在 ie 中 margin 将变大
    解决：
    设置 li 的 display:inline



### 嵌套使用 ul、li 的问题

    问题：
    ie 的 bug，嵌套使用 ul、li 时，里层的 li 设置 float 以后，外层 li 不设置 float, 里面的 ul 顶部和它外面的 li 总是有一段间距
    解决：
    设置里面的 ul 的 zoom:1



### IE6-7 li 底部有 3px 的问题

    问题：
    这个 bug 产生的充要条件是 li 的子元素浮动并且 li 设置了以下 CSS 属性之一：width、height、zoom、padding-top、padding-bottom、margin-top、margin-bottom。
    解决：
    1、div 设置 clear:left|both，这时 li 不能设置 width、height、zoom。
    2、li 设置 float:left，这时 li 可以设置 width、height、zoom。
    3、li 设置 clear:left|both，这时 li 不能设置 width、height、zoom。
    4、IE6/IE7 的这个 Bug 可以通过给 li 中的 div 设置 vertical-align:top|middle|bottom 解决。



### IE6 垂直列表间隙的问题

    问题：
    li 中有 a 且设置 display:block 时，ie6 中列表间会出现空隙
    解决：
    1、li 中加 display:inline;
    2、li 使用 float 然后 clear:both;
    3、给包含的文本末尾添加一个空格
    4、设置 width



###  IE6 列表背景颜色失效的问题

    问题：
    当父元素设置 position:relative;时，在 ie6 中第一个 ul、ol、dl 的背景颜色失效
    解决：
    ul、ol、dl 都设置为 position:relative;



### IE6-7 列表背景颜色失效的问题

    问题：
    做横向导航栏时，ul 设置为 float 且有背景色，li 设置为 float。ie6-7 背景颜色失效
    解决：
    很多 ie 的 bug 都可以通过触发 layout 来解决 ul 添加属性
    1、height:1\\%;
    2、float:left;
    3、zoom:1;



### 列表不能换行的问题

    问题：
    li 设置为浮动，后面的 li 紧随其后，不能换行
    解决：
    1、为这个 ul 定义合适的宽高
    2、给包含这个 ul 的父 div 定义合适的宽高。



### li 中的内容以省略号显示

    问题：
    li 中内容超过长度时，想以省略号显示， 此方法适用于 ie6-7-8、opera、safari 浏览器
    ff 浏览器不支持
    解决：
    li\\{width:200px;white-space:nowrap;text-overflow:ellipsis;
    -o-text-overflow:ellipsis; overflow:hidden; \\}



### 超链接访问过后 hover 样式不出现的问题

    问题：
    点击超链接后，hover、active 样式没有效果
    解决：
    改变 CSS 属性的排列顺序: L-V-H-A



### 禁用中文输入法的问题

    问题：
    不能在输入框中输入汉字
    解决：
    只在 ie 系列和 ff 中有效
    ime-mode:disabled (但可以粘贴)
    禁用粘贴：
    onpaste="return false"



### 让层显示在 FLASH 之上

    问题：
    想让层的内容显示在 flash 上
    解决：
    把 FLASH 设置透明
    1、<param name=" wmode " value="transparent" />
    2、<param name="wmode" value="opaque"/>



### 去除链接虚线边框的问题

    问题：
    当点击超链接后，ie6/7/8 ff 会出现虚线边框 ,而 opera、safari 没有虚线边框
    解决：
    ie6/7 中 设置为 a \\{blr:expression_r(this.onFocus=this.blur()) \\}
    ie8 和 ff 都不支持 expression 在 ie8 、ff 中设置为 :focus \\{ outline: none; \\}



### css 滤镜的问题

    问题：
    css 滤镜只在 ie 中有效，Firefox, Safari(WebKit), Opera 只能够设置透明，它们不支持滤镜 filter，无法实现图片切换中间变换的效果，只能通过透明度来设置。
    解决：
    ff 中设置透明度 -moz-opacity:0.10; opacity:0.6;
    ie 中只设置 filter:alpha(opacity=50);时，ie6-7 失效，还要设置
    1、zoom:1; 2、width:100\\%;



### IE6 背景闪烁的问题

    问题：
    链接、按钮用 CSS sprites 作为背景，在 ie6 下会有背景图闪烁的现象。原因是:IE6 没有将背景图缓存，每次触发 hover 的时候都会重新加载
    解决：
    可以用 JavaScript 设置 ie6 缓存这些图片：
    document.execCommand("BackgroundImageCache",false,true);



### 出现重复文字的问题

    问题：
    <div style="width:400px">
      <div style="float:left"></div>
      <!– _ –>
      <div style="float:right;width:400px">↓这就是多出来的那只猪</div>
    </div>
    解决：
    1、  改变结构，不出现【一个容器包含2两个具有“float”样式的子容器】的结构。
    2、减小第二个容器的宽度，使父容器宽度减去第二个容器宽度的值大于3
    3、去掉所有的注释。
    4、修正注释的写法。<!--[if!IE]>这里是注释内容<![endif]-->
    5、在第二个容器后面加一个或者多个<divstyle="clear"></div>来解决。



###  ff、chrome 绝对定位无效

    问题：
    在 IE 给 td 设置 position:relative，然后给它包含的一个容器使用 position:absolute 进行定位是有效的，但在 FF 和 Chrome 下却不可以。
    解决：
    设置 td 的 display:block。



### IE6 绝对定位的问题

    问题：
    <div style="position:relative;border:1px solid orange;text-align:center;">
    <div style="position:absolute;top:0;left:0;
    background:#CCC;">dovapour</div>
    <a href="#" title="vapour的blog">内容</a>
    </div>
    解决：
    left的定位错误问题
    1、给父层设置zoom:1触发layout。
    2、给父层设置宽度width



### bottom 的定位错误问题

1、给父层设置 zoom:1 触发 layout。
2、给父层设置高度 height



### float 的 div 闭合的问题

    问题：
    例如：<div id=”floatA” ><div id=”floatB” ><div id=”NOTfloatC” >这里的 NOTfloatC 并不希望继续平移，而是希望往下排。(其中 floatA、floatB 的属性已经设置为 float:left;)
    这段代码在 IE 中毫无问题，问题出在其他浏览器中。原因是 NOTfloatC 并非 float 标签，必须将 float 标签闭合。
    解决：
    在 <#div class=”floatB”> <#div class=”NOTfloatC”>之间加上 <#div class=”clear”>这个 div 一定要注意位置，而且必须与两个具有 float 属性的 div 同级，之间不能存在嵌套关系，否则会产生异常。并且将 clear 这种样式定义为为如下即可：.clear\\{ clear:both;\\}



### 单选框、复选框与后面的文字对不齐

    问题：
    单选框、复选框与后面的文字对不齐。
    解决：
    .align\\{font-size:12px;\\}
    .align input\\{ display:block; float:left;\\}
    .align label\\{ display:block; float:left;padding-top:3px; \*padding-top:5px;\\}

需注意的问题：

1. 设置 padding 后高度和宽带都会增加
   说明：
   除了 ie5.5，其他所有浏览器中，设置 padding 以后高度和宽带都会增加
2. 使用 XHTML 1.0Transitional 后，div 宽度
   说明：
   在使用 XHTML 1.0Transitional 以后 div 宽度都不包含 border 的宽度了，设置宽度的时候需要注意下。
3. 外层相对定位，内层绝对定位
   说明：
   ie6 下，外层 div 的 postion:relative，并设置 text-align，内层 div 的 postion: absolute，这时内层的位置是相对于 text-align 而言的
   例如：

```html
<div style="position:relative;border:1px solid orange;text-align:center;zoom:1">
  position:relative
  <div style="position:absolute;top:0;left:0;background:#CCC;">
    position:absolute
  </div>
</div>
```



###  `&nbsp;` 显示的大小不一致

默认字本显示问题，导致&nbsp;显示的大小不一致，在 ie 下比较小一点，其他的浏览器都一致，当你使用了&nbsp;造成问题时请注意。



### 边框重叠说明

说明：
为 table、td 都指定了边框后，然后使用 border-collapse:collapse 让边框重叠，可以看出在发生重叠时，Firefox 是用 td 覆盖 table 的，而 IE 是用 table 覆盖 td 的。使用时候需要注意。



### 设置 td padding 的说明

说明：
设置 td 的 padding 以后高度和宽带都会增加,padding-left 和 padding-right 的效果都一样增加了 td 的宽带，但是 padding-top 和 padding-bottom 的效果不一样。最好不要使用 td 的 padding-top 和 padding-bottom



### ul 设置的说明

说明：
ul 一般设置：list-style-type:none;margin:0px;padding:0px；li 一般设置：list-style-type:none;list-style-position:outside



### 使一个层垂直居中于浏览器中

说明：
使用百分比绝对定位,与外补丁负值的技巧,负值的大小为其自身宽度高度除以二
div \\{
position:absolute; top:50\\%; lef:50\\%; margin:-100px 0 0 -100px;
width:200px; height:200px; border:1px solidred;
\\}



### 触发 layout

说明：
IE6 中很多 Bug 都可以通过触发 layout 得到解决.下列的 CSS 属性或取值会让一个元素获得 layout：
position:absolute 绝对定位元素的包含区块(containingblock)就会经常在这一方面出问题
float:left|right 由于 layout 元素的特性，浮动模型会有很多怪异的表现
display:inline-block 当一个内联级别的元素需要 layout 的时候就往往符用到它，这也可能也是这个 CSS 属性的唯一效果----让某个元素有 layout
width: 除 auto 外的任何值
height: 除 auto 外的任何值
zoom: 除 auto 外的任何值



### 如何使连续长字段自动换行

ff 最新版本 word-wrap:break-word;就可以了
ff 旧版本 还要使用 javascript 完成文字换行

```
<style type="text/css">
div \\{
      width:300px;
      word-wrap:break-word;
      border:1px solid red;
       \\}
</style>

<scripttype="text/javascript">
function toBreakWord(intLen)\\{
varobj=document.getElementByIdx_x("ff");
var strContent=obj.innerHTML;
var strTemp="";
while(strContent.length>intLen)\\{
strTemp+=strContent.substr(0,intLen)+"&#10;";
strContent=strContent.substr(intLen,strContent.length);
\\}
strTemp+="&#10;"+strContent;
obj.innerHTML=strTemp;
\\}
if(document.getElementByIdx_x &&  !document.all)  toBreakWord(37)
```



### 设置滚动条颜色 只对 ie 系列有效 在 html 中 而不是设置 body

```
<style type="text/css">
html \\{
      scrollbar-face-color:#f6f6f6;
      scrollbar-highlight-color:#fff;
      scrollbar-shadow-color:#eeeeee;
      scrollbar-3dlight-color:#eeeeee;
      scrollbar-arrow-color:#000;
      scrollbar-track-color:#fff;
      scrollbar-darkshadow-color:#fff;
       \\}
</style>
```

IE 不支持 float：inherit overflow:hidden 有 2 个用法，一个是隐藏溢出，另一个是清除浮动。

```
<div>, <p>, <h1>,<form>, <ul> 和 <li>是块元素的例子
<span>, <a>, <label>,<input>, <img>, <strong> 和<em>是inline元素
<body oncontextmenu="returnfalse" ondragstart="return false"  tstart="returnfalse"  scroll="auto">
这行代码放在body中，去掉了页面鼠标右键快捷菜单，达到防止图片另存为的目的。
```



### document.form.item 问题

问题：
代码中存在 document.formName.item("itemName") 这样的语句，不能在 FF 下运行
解决方法：
改用 document.formName.elements["elementName"]



### 集合类对象问题

问题：
代码中许多集合类对象取用时使用()，IE 能接受，FF 不能
解决方法：
改用 [] 作为下标运算，例：
document.getElementsByName("inputName")(1) 改为 document.getElementsByName("inputName")[1]



### window.event

问题：
使用 window.event 无法在 FF 上运行
解决方法：
FF 的 event 只能在事件发生的现场使用，此问题暂无法解决。可以把 event 传到函数里变通解决：

```
onMouseMove = "functionName(event)"
function functionName (e) \\{
	e = e || window.event;
	......
\\}
```



### HTML 对象的 id 作为对象名的问题

在 IE 中，HTML 对象的 ID 可以作为 document 的下属对象变量名直接使用，在 FF 中不能
解决方法：
使用对象变量时全部用标准的 getElementById("idName")



### 用 idName 字符串取得对象的问题

问题：
在 IE 中，利用 eval_r("idName") 可以取得 id 为 idName 的 HTML 对象，在 FF 中不能
解决方法：
用 getElementById("idName") 代替 eval_r("idName")



### 变量名与某 HTML 对象 id 相同的问题

问题：
在 FF 中，因为对象 id 不作为 HTML 对象的名称，所以可以使用与 HTML 对象 id 相同的变量名，IE 中不能
解决方法：
在声明变量时，一律加上 var ，以避免歧义，这样在 IE 中亦可正常运行
最好不要取与 HTML 对象 id 相同的变量名，以减少错误



### event.x 与 event.y 问题

问题：
在 IE 中，event 对象有 x,y 属性，FF 中没有
解决方法：
在 FF 中，与 event.x 等效的是 event.pageX ，但 event.pageX IE 中没有
故采用 event.clientX 代替 event.x ，在 IE 中也有这个变量
event.clientX 与 event.pageX 有微妙的差别，就是滚动条
要完全一样，可以这样：
mX = event.x ? event.x : event.pageX;
然后用 mX 代替 event.x



### 关于 frame

问题：
在 IE 中可以用 window.testFrame 取得该 frame，FF 中不行
解决方法：
window.top.document.getElementByIdx_x("testFrame").src = 'xx.htm'
window.top.frameName.location = 'xx.htm'



### 取得元素的属性

在 FF 中，自己定义的属性必须 getAttribute() 取得



### 在 FF 中没有 parentElement，parement.children 而用 parentNode，parentNode.childNodes

    问题：
    childNodes 的下标的含义在 IE 和 FF 中不同，FF 的 childNodes 中会插入空白文本节点
    解决方法：
    可以通过 node.getElementsByTagName_r() 来回避这个问题
    问题：
    当 html 中节点缺失时，IE 和 FF 对 parentNode 的解释不同，例如：
    <form>
    	<table>
    		<input/>
    	</table>
    </form>
    FF中 input.parentNode 的值为form，而IE中 input.parentNode 的值为空节点
    问题：
    FF中节点自己没有 removeNode 方法
    解决方法：
    必须使用如下方法 node.parentNode.removeChild(node)



### body 对象

    FF 的 body 在 body 标签没有被浏览器完全读入之前就存在，而 IE 则必须在 body 完全被读入之后才存在
    这会产生在 IE 下，文档没有载入完时，在 body 上 appendChild 会出现空白页面的问题
    解决方法：
    一切在 body 上插入节点的动作，全部在 onload 后进行



### url encoding

    问题：
    一般 FF 无法识别 js 中的&
    解决方法：
    在 js 中如果书写 url 就直接写&不要写&



### nodeName 和 tagName 问题

    问题：
    在 FF 中，所有节点均有 nodeName 值，但 textNode 没有 tagName 值，在 IE 中，nodeName 的使用有问题
    解决方法：
    使用 tagName，但应检测其是否为空



### 元素属性

    IE 下 input.type 属性为只读，但是 FF 下可以修改



### document.getElementsByName() 和 document.all[name] 的问题

    问题：
    在 IE 中，getElementsByName()、document.all[name] 均不能用来取得 div 元素
    是否还有其它不能取的元素还不知道（这个问题还有争议，还在研究中）



### 调用子框架或者其它框架中的元素的问题

    在 IE 中，可以用如下方法来取得子元素中的值
    document.getElementByIdx_x("frameName").(document.)elementName
    window.frames["frameName"].elementName
    在 FF 中则需要改成如下形式来执行，与 IE 兼容：
    window.frames["frameName"].contentWindow.document.elementName
    window.frames["frameName"].document.elementName



### 对象宽高赋值问题

    问题：
    FireFox 中类似 obj.style.height = imgObj.height 的语句无效
    解决方法：
    统一使用 obj.style.height = imgObj.height + "px";



### innerText 的问题

    问题：
    innerText 在 IE 中能正常工作，但是 innerText 在 FireFox 中却不行
    解决方法：
    在非 IE 浏览器中使用 textContent 代替 innerText



### event.srcElement 和 event.toElement 问题

    问题：
    IE 下，even 对象有 srcElement 属性，但是没有 target 属性；Firefox 下，even 对象有 target 属性，但是没有 srcElement 属性
    解决方法：
    var source = e.target || e.srcElement;
    var target = e.relatedTarget || e.toElement;



### 禁止选取网页内容

    问题：
    FF 需要用 CSS 禁止，IE 用 JS 禁止
    解决方法：
    IE: obj.onselectstart = function() \\{return false;\\}
    FF: -moz-user-select:none;



### 捕获事件

```js
问题：
FF 没有 setCapture()、releaseCapture()方法
解决方法：
IE:
obj.setCapture();
obj.releaseCapture();
FF:
window.captureEvents(Event.MOUSEMOVE|Event.MOUSEUP);
window.releaseEvents(Event.MOUSEMOVE|Event.MOUSEUP);
if (!window.captureEvents) \\{
	o.setCapture();
\\}else \\{
	window.captureEvents(Event.MOUSEMOVE|Event.MOUSEUP);
\\}
if (!window.captureEvents) \\{
	o.releaseCapture();
\\}else \\{
	window.releaseEvents(Event.MOUSEMOVE|Event.MOUSEUP);
\\}
```



### 常见浏览器bug及处理


#### <a name="double-margin">双边距</a>

IE6下,一个div盒子如果设置了margin和浮动，便会产生双边距问题。    
解决方案：给该div设置样式`_display:inline`。

#### <a name="overflow-hidden-bug">`overflow:hidden`失效</a>

IE6，7下，当父元素的子元素的样式拥有`position:relative`时，父元素的`overflow:hidden`属性就会失效。 

解决方案：父元素也设置`position:relative`

#### <a name="scroll-hidden-bug">滚动条bug</a>

IE6，7下，当固定了一个元素的宽高，纵向溢出（overflow-y）为滚动（scroll）或者自动（auto）时，当其子元素有`position:relative`时，子元素不会随滚动条滚动    
解决方案: 给该元素也设置`position:relative`

#### <a name="repaint">浏览器未重绘导致的问题</a>

解决方式,用js,让其隐藏再显示

```
$elem.hide().show();
```

#### <a name="float-li-3px">li底部3px的Bug</a>

IE6，7下，当li的子元素浮动（float），并且li设置了以下CSS属性之一：`width、height、zoom、padding-top、padding-bottom、margin-top、margin-bottom`，li会产生3px空隙。    
解决方案:给li的浮动的子元素上设置`vertical-align:top|middle|bottom`


#### <a name="repeat-text">IE6注释bug</a>

IE6下，满足以下条件

* 一个容器包含2两个具有“float”样式的子容器。
* 容器的宽度大于父容器的宽度，或者父容器宽度减去第二个容器宽度的值小于3
* 在第二个容器前存在注释

会出现重复的字符内容
解决方案： 破坏其中一个触发条件。最简单方式：删除注释。


#### <a name="over-flow-y">body上设置overflow-y:hidden的问题</a>

在ie6，7中，设置在body元素上`overflow-y:hidden`不能隐藏滚动条。    
解决方案：在html元素上也设置`overflow-y:hidden`

#### <a name="text-v-center">Firefox下input button内文字不垂直居中</a>

解决方案：

```
input[type="reset"]::-moz-focus-inner,
input[type="button"]::-moz-focus-inner,
input[type="submit"]::-moz-focus-inner,
input[type="file"] > input[type="button"]::-moz-focus-inner\\{
border:none;padding:0;
\\}
```
