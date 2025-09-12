---
title: CSS动效
date: 2020-08-30 22:30:10
categories: 
- 前端知识
tags:
- CSS
---

### Web 动画

**综合学习:**

* [Web 动画的历史](https://www.codeschool.com/courses/adventures-in-web-animations) [watch][$]
* [Snap.svg 动画](https://webdesign.tutsplus.com/courses/animating-with-snapsvg) [watch][$]
* [CSS3 和 HTML5 动画](https://frontendmasters.com/courses/animation-storytelling-html5-css3/) [watch][$]
* [真实世界中的 CSS 动画](https://webdesign.tutsplus.com/courses/css-animation-in-the-real-world) [watch][$]
* [HTML5+JavaScript 动画基础](http://www.amazon.cn/HTML5-JavaScript\\%E5\\%8A\\%A8\\%E7\\%94\\%BB\\%E5\\%9F\\%BA\\%E7\\%A1\\%80-\\%E5\\%85\\%B0\\%E8\\%B4\\%9D\\%E5\\%A1\\%94/dp/B00D69IJKA/ref=sr_1_2?ie=UTF8&qid=1446346650&sr=8-2) [read][RMB]
* [Web Animation using JavaScript: Develop &amp; Design (Develop and Design)](http://www.amazon.com/Web-Animation-using-JavaScript-Develop-ebook/dp/B00UNKXVDU/ref=sr_1_1) [read][$]
* [2014: 动画发展现状](http://www.smashingmagazine.com/2014/11/the-state-of-animation-2014/) [read]
* [学会用 CSS 创建动画](http://www.kirupa.com/css_animations/index.htm) [read & watch]
* [学会用 JavaScript 创建动画](http://www.kirupa.com/javascript_animations/index.htm) [read & watch]

**标准/规范**

* [Web 动画](https://w3c.github.io/web-animations/)

**译者补充:**

* [Pro CSS3 Animation](http://apress.jensimmons.com/v5/pro-css3-animation/ch2.html)

其他

1. https://www.cnblogs.com/coco1s/p/6829372.html https://codepen.io/comehope/pen/GBwvxw 两个比较炫酷的 css 特效源码
2. https://www.zhangxinxu.com/wordpress/2011/04/\\%E5\\%B0\\%8Ftipcss3\\%E4\\%B8\\%8B\\%E7\\%9A\\%84\\%E6\\%B8\\%90\\%E5\\%8F\\%98\\%E6\\%96\\%87\\%E5\\%AD\\%97\\%E6\\%95\\%88\\%E6\\%9E\\%9C\\%E5\\%AE\\%9E\\%E7\\%8E\\%B0/ CSS3 下的渐变文字效果实现
3. https://www.zhangxinxu.com/wordpress/2012/09/css3-3d-transform-perspective-animate-transition/ css3 3d 理解 来自张鑫旭



### transition和animation的区别

#### transition过渡

可以在一定的时间内实现元素的状态过渡为最终状态，用于模拟以一种过渡动画效果，但是功能有限，只能用于制作简单的动画效果而动画属性

#### animation动画

可以制作类似 Flash 动画，通过关键帧控制动画的每一步，控制更为精确，从而可以制作更为复杂的动画。

transition关注的是CSS property的变化，property值和时间的关系是一个三次贝塞尔曲线。

animation作用于元素本身而不是样式属性，可以使用关键帧的概念，应该说可以实现更自由的动画效果。

详细资料可以参考：
[《CSSanimation 与 CSStransition 有何区别？》](https://www.zhihu.com/question/19749045)
[《CSS3Transition 和 Animation 区别及比较》](https://blog.csdn.net/cddcj/article/details/53582334)
[《CSS 动画简介》](http://www.ruanyifeng.com/blog/2014/02/css_transition_and_animation.html)
[《CSS 动画：animation、transition、transform、translate》](https://juejin.im/post/5b137e6e51882513ac201dfb)



### transition、translate分别是什么？

transition： 当前元素只要有“属性”发生变化时，可以平滑的进行过渡。通过 transtion-propety 设置过渡属性；

transtion-duration 设置过渡时间；

trantion-timing-function 设置过渡速度；

trantion-delay 设置过渡延时

translate：通过移动改变元素的位置；有 x、y、z 三个属性



### 全屏滚动的原理是什么？用到了 CSS 的哪些属性？（待深入实践）

原理：有点类似于轮播，整体的元素一直排列下去，假设有5个需要展示的全屏页面，那么高度是500\\%，只是展示100\\%，容器及容
器内的页面取当前可视区高度，同时容器的父级元素overflow属性值设为hidden，通过更改容器可视区的位置来实现全
屏滚动效果。主要是响应鼠标事件，页面通过CSS的动画效果，进行移动。

```
overflow：hidden；transition：all 1000 ms ease；
```

详细资料可以参考：
[《js 实现网页全屏切换（平滑过渡），鼠标滚动切换》](https://blog.csdn.net/liona_koukou/article/details/52680409)
[《用 ES6 写全屏滚动插件》](https://juejin.im/post/5aeef41cf265da0ba0630de0)



### transition过渡动画的自述

Hi,大家好！我是`transition`，经常有小伙伴把我和隔壁`animation`搞混，下面我就好好的介绍一下自己，让大家能明白我到底是干啥的。

#### 看看我身上的属性吧：

大家总是叫我`transition`，其实我有四个重要的部分组成，下面一一听我介绍：

1. `transition-property`:需要参与过渡的属性，例如：width、height、background...
2. `transition-duration`:过渡动画的持续时间，单位秒s或毫秒ms
3. `transition-delay`：延迟过渡的时间，单位秒s或毫秒ms
4. `transition-timing-function`：动画过渡的动画类型

我可以以属性的形式被定义

```css
div\\{
  width:100px;
  height:100px;
  background:blue;
  transition-property: width;/* 需要参与过渡的属性 */
  transition-duration: 1s;/* 过渡动画的持续时间 */
  transition-delay: 1s;/* 延迟过渡的时间，单位秒s或毫秒ms */
  transition-timing-function: ease-out;/* 动画过渡的动画类型 */
\\}
div:hover\\{
  width:300px; 
\\}
```

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6d996d316c2c453b83fdf7b34d9766e7~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

效果图出来了我是不是很厉害？可是上面的我由于属性太多有点不招新手同学待见 o(╥﹏╥)o

其实平时的我是下面这种形式出现在代码中的：

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/baa2de23374d48f59279de5334bafe37~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

这样瘦身的我是不是就很可爱了呢？ (*╹▽╹*)

下面这样写，效果一样哟

```css
div\\{
  width:100px;
  height:100px;
  background:blue;
  transition:width 1s 1s ease-out ;
\\}

div:hover\\{
  width:300px;
\\}
```

我还可以更厉害呢！ ୧(๑•̀◡•́๑)૭

通常情况下，我会让一些元素在变化时产生动画效果，但是我得和好搭档`hover`（鼠标悬停）一起干活，先来看一段代码：

```css
div\\{
    width:100px;
    height:500px;
    background:teal;
    /* 而且我还能多个属性逐个显示过渡动画效果哦~~*/
    transition:width .5s linear,height .5s ease .5s,background 1s ease-in 1s;
\\}
/* 鼠标悬停，改变div的样式 */
div:hover\\{
    width:500px;
    height:100px;
    background:hotpink;
\\}
```

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9db99e320c3343f89210b04f02836b3f~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

那大家明白这种写法吗？[试一试?](https://link.juejin.cn/?target=https\\%3A\\%2F\\%2Fwww.runoob.com\\%2Ftry\\%2Ftry.php\\%3Ffilename\\%3Dtrycss3_transition)

这里就是应用过渡动画实现的效果，多个属性是依次执行动画效果的，其实就是巧妙应用了过渡延迟属性，让上一个属性执行完了再接着下面一个,是不是很有趣鸭。

#### 看我的绝技 transition-timing-function

`transition-timing-function`是动画运动的曲线，它一共有6个值。

- `ease` - 指定一个缓慢开始，然后快速，然后慢慢结束的过渡效果(这是默认值)
- `linear` - 指定从开始到结束以相同速度的转换效果
- `ease-in` - 指定缓慢启动的过渡效果
- `ease-out` - 指定一个缓慢结束的过渡效果
- `ease-in-out` - 指定开始和结束缓慢的过渡效果
- `cubic-bezier(n,n,n,n)` - 在一个三次贝塞尔函数中定义您自己的值

```css
#div1 \\{transition-timing-function: linear;\\}
#div2 \\{transition-timing-function: ease;\\}
#div3 \\{transition-timing-function: ease-in;\\}
#div4 \\{transition-timing-function: ease-out;\\}
#div5 \\{transition-timing-function: ease-in-out;\\}
```

#### 看看我都能干什么吧！ヾ(◍°∇°◍)ﾉﾞ 复杂一点的例子

下面我们再来做一个更好看的效果，类似于弹钢琴的效果，代码如下：

html:

```html
<ul>
    <li><a href="">首页</a><span></span></li>
    <li><a href="">首页</a><span></span></li>
    <li><a href="">首页</a><span></span></li>
    <li><a href="">首页</a><span></span></li>
</ul>
```

css

```css
<style>
    ul \\{
        list-style: none;
        width: 600px;
        height: 60px;
        background: skyblue;
    \\}

    li \\{
        float: left;
        /* 参照物 */
        position: relative;
    \\}

    a \\{
        display: block;
        width: 150px;
        height: 60px;
        line-height: 60px;
        text-align: center;
        color: #333;
        text-decoration: none;
        /* 提升层级，解决被span遮住 */
        position: relative;
        z-index: 1;
    \\}

    span \\{
        position: absolute;
        bottom: 0;
        width: 150px;
        height: 4px;
        background: pink;
        /* 过渡 */
        transition: height .5s linear;
    \\}

    li:hover span \\{
        height: 60px;
    \\}
</style>
```

请看效果图：

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c400025d20f0468bae8e60432dfea758~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

这个效果还不错吧，运用了过渡动画结合了定位相关的综合应用。最后再次提醒，你想要用我做过渡动画，一定要结合事件触发哦，最常用的方式就是鼠标的hover。

原文链接：https://juejin.cn/post/6909646228301021191



### css图片放大功能，且不溢出包裹盒子

```
<div class="item">
    <div class="img">
    	<img src="./images/solve1@2x.png" alt="" />
    </div>
    <div class="sub-title">xxx</div>
    <div class="desc">xxxxxx</div>
</div>

.solve .item \\{
    width: 285px;
    height: 254px;
    margin-bottom: 20px;
    border-radius: 8px;
    display: flex;
    flex-direction: column;
    align-items: center;
    background: #FFF;
    box-shadow: 0px 4px 12px 0px rgba(0, 0, 0, 0.04);
    /* 防止图片放大后圆角处溢出 */
    overflow: hidden;
\\}

.solve .item:hover img \\{
    transform: scale(1.2);
\\}

.solve .img \\{
    height: 168px;
    /* 防止图片放大后溢出 */
    overflow: hidden;
\\}

.solve img \\{
    width: 100\\%;
    height: 168px;
    /* 定义过渡动画效果 */
    transition: transform 0.5s ease-out;
\\}
```



### 纯css hover放大图片

 hover效果css代码: 

```
<div> <img src="1.jpg" /> </div>

div \\{
    width: 555px;
    height: 489px;
    border: #000 solid 1px;
    margin: 50px auto;
    overflow: hidden;
\\}
div img \\{
    cursor: pointer;
    webkit-transition: all 1s ease 0s;
	transition: all 1s ease 0s;
\\}
div img:hover \\{
    transform: scale(1.3);
\\}
```

**属性解释**

transition: all 0.6s;表示所有的属性变化在0.6s的时间段内完成。

transform: scale(1.4);表示在鼠标放到图片上的时候图片按比例放大1.4倍

不过这个transform 的属性只支持到ie9

总结日期：2020.10.27



### hover图片放大效果

先给图片一个属性：

```
transition: all 0.6s cubic-bezier(0.23, 1, 0.320, 1);
```

再给hover一个属性：

```
transform: scale3d(1.2, 1.2, 1);
```



### 请用 CSS 实现：一个矩形内容，有投影，有圆角，hover 状态慢慢变透明

```html
<div class="test"></div>
```

```css
.test \\{
  width: 200px;
  height: 100px;
  border-radius: 10px;
  box-shadow: 10px 10px 5px #888888;
  background-color: green;
  transition: 0.7s;
\\}
.test:hover \\{
  opacity: 0;
\\}
```



### 列表项hover效果

```
.day-item \\{
    border-radius: 7px;
    margin-bottom: 10px;
    transition: all 0.3s ease;
    background: #fff;
    &:hover \\{
      transform: translateY(-2px);
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    \\}
\\}
```



### 传统a链接跳转的网页也可以加过渡动画的

具体动画看你怎么加喽 体验也很棒

```html
<head>
  <style>
    .content \\{
      opacity: 0;
      transition: opacity 0.5s;
    \\}
    .content.active \\{
      opacity: 1;
    \\}
  </style>
</head>
<body>
  <nav>
    <ul>
      <li><a href="/">首页</a></li>
      <li><a href="/my">我的</a></li>
      <li><a href="/you">你的</a></li>
    </ul>
  </nav>
  <div class="content">内容</div>
  <script>
    var content = document.querySelector(".content");
    content.classList.add("active"); // 这个 classList IE10才行
  </script>
</body>
```



### less主题色切换

```
<div :class="theme==='dark'?'dark':'light'">侧边栏<div>
<Tooltip :content="theme==='dark'?'点击切换为浅色导航':'点击切换为深色导航'">
   <div class="head-icon theme-icon" @click="changeTheme">
   	<img v-if="theme==='dark'" src="../../assets/images/theme2@2x.png" alt="">
   	<img v-else src="../../assets/images/theme1@2x.png" alt="">
   </div>
</Tooltip>

data() \\{
    return \\{
      theme:'dark' // 当前主题色
    \\};
\\},
created()\\{
    // 获取缓存中的主题色
    this.theme = localStorage.getItem("theme")||'dark';
\\}
methods: \\{
// 切换主题色并设置缓存
    changeTheme()\\{
        if(this.theme === 'dark')\\{
            this.theme = 'light'
            localStorage.setItem("theme", this.theme);
        \\}else\\{
            this.theme = 'dark'
            localStorage.setItem("theme", this.theme);
        \\}
    \\},
\\}

<style lang="less">
// 侧边栏主题切换样式
/* 更改dark类名下变量的取值 */
.dark\\{
    --background: #122036;
    transition: all .2s ease-in-out;
\\}
/* 更改light类名下变量的取值 */
.light\\{
    --background: #ffffff;
    transition: all .2s ease-in-out;
\\}
@background: var(--background);

// logo区域背景色
.ivu-layout-sider \\{
    width: 216px;
    overflow-y: auto;
    background: @background;
\\}
// 菜单整体背景色
.ivu-menu-dark \\{
    background: @background;
\\}
</style>
```



### 单页面过渡动画过渡过程要设置absolute还要有位置，这样才不会抖动

```css
.ht-filter-enter-active,
.ht-filter-leave-active \\{
  position: absolute;
  left: 0;
  top: 0;
  bottom: 0;
  right: 0;
  transform: translate3d(0, 0, 0);
  transition: opacity 0.5s, filter 0.5s;
\\}
.ht-filter-enter,
.ht-filter-leave-to \\{
  position: absolute;
  left: 0;
  top: 0;
  bottom: 0;
  right: 0;
  transform: translate3d(0, 0, 0);
  filter: blur(8px);
  opacity: 0;
\\}
```



### transition动画过程中多个子重叠优先级问题（鼠标右移和左移显示效果不一样）

大概就是这样一个场景 一个列表 五个 li 然后鼠标放上去放大 放大后的要遮住旁边的 li 鼠标从左往右的时候，即将开始动画的在即将结束动画的 DOM 结构之上，而从右往左，是结束的在上面 开始的在下面，于是利用 z-index 的方案来解决了这个问题

```css
li \\{
  position: relative;
  z-index: 1;
  display: inline-block;
  width: 227px;
  height: 290px;
  text-align: center;
  margin-right: 24px;
  background: linear-gradient(
    180deg,
    rgba(83, 77, 51, 1),
    rgba(198, 184, 119, 1)
  );
  border-radius: 8px;
  transition: transform 0.4s linear, box-shadow 0.4s linear;
  &:hover \\{
    transform: scale(1.3);
    box-shadow: 0 0 60px #000;
    z-index: 2;
  \\}
\\}
```



### 消除 transition 闪屏

```
.css\\{
    /*设置内嵌的元素在 3D 空间如何呈现：保留 3D*/
    -webkit-transform-style: preserve-3d;
    /*（设置进行转换的元素的背面在面对用户时是否可见：隐藏）*/
    -webkit-backface-visibility: hidden;
\\}
```

#### 开启硬件加速

· 解决页面闪白

· 保证动画流畅

```
.css \\{
    -webkit-transform: translate3d(0, 0, 0);
    -moz-transform: translate3d(0, 0, 0);
    -ms-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
\\}
```



### 设计高性能CSS3动画的几个要素

- 尽可能地使用合成属性transform和opacity来设计CSS3动画
- 不使用position的left和top来定位
- 利用translate3D开启GPU加速



### transform导致文字模糊

> 这是因为transform变换会在浏览器上单独创建一个绘画层并重新进行渲染，rotate渲染的时候，由于图层渲染的时候也处理了周围的文字，如果高度为奇数的文字可能会存在半个像素的计算量，浏览器对这半个像素会进行优化渲染，所以边缘会出现模糊的情况。

后来尝试过下面三种方法

1. 将元素的高度设置为偶数可解决；
2. 将transform: translate(x\\%, y\\%)中的y轴单位改成px也可以解决
3. 改成transform: translate(-50\\%, -52\\%)也可以解决（如果52\\%不行的话，可以从51\\%一个一个1\\%试试）

一、不使用transform
模糊的原因跟 transform:translate(X,Y) 偏移有关系，我们就看看能否使用其他法子

法一：定位方式
translate偏移无非就是想居中定位（如果不是居中定位的话，那就没必要使用偏移了，直接通过top,left等定出你需要的位置），这种方式需要给定元素宽高，然后定位top,left,right,bottom四个值设为0在加上margin为auto即可~

```
 .popup-box\\{
	 position: fixed;
	 top: 0;
	 right: 0;
	 left: 0;
	 bottom: 0;
	 z-index: 999;
	 background-color: #fff;
	 width: 540px;
	 height: 20rem;
	 margin: auto;
 \\}
```

法二：css计算属性calc
如果对于垂直方向上的偏移没过多要求的话，直接使用百分比或者rem适应性单位定位即可，而水平方向一般都要求屏幕中间的话，可以在left值上使用计算属性，50\\%减去元素宽度的一半，因此这边需要给定元素一个宽度值

```
.popup-box\\{
  position: fixed;
  top: 25\\%;
  left: calc(50\\% - 260px);
  z-index: 999;
  width: 520px;
  padding: 46px 0 40px;
  background-color: #fff;
\\}
```

法三：给字体加多一个父级
原本字体的父级为列子中的popup-box，我们可以看到该父级是参与定位偏移的，所以才会影响到里面的字体，因此我们让字体套多一层父级即可

```
<div class="popup-box">
  <div class="popup-text">xxxx...</div>
</div>
```

```
.popup-box\\{
  position: fixed;
  top: 50\\%;
  left: 50\\%;
  z-index: 999;
  width: 520px;
  background-color: #fff;
  transform: translate(-50\\%,-50\\%);
\\}
.popup-text\\{
  display: flex;
  align-items: center;
\\}
```

二、仍使用transform
如果还是要用 transform：translate来偏移的话，那可以这样写：

法一：元素宽高值设为偶数
当字体的父级元素盒子宽高给定偶数时，此时是不会出现模糊的，若其一为奇数则出现模糊的情况

```
.popup-box\\{
   position: fixed;
   top: 50\\%;
   left: 50\\%;
   z-index: 999;
   width: 520px;
   height: 300px;
   padding: 46px 0 40px;
   background-color: #fff;
   transform: translate(-50\\%,-50\\%);
\\}
```

法二：给translate的Y值偏移设为绝对单位
直接给translate的Y轴偏移设为绝对单位，此时也是不会模糊的，此时不管你元素高度是奇数还是偶数

```
.popup-box\\{
    position: fixed;
    top: 50\\%;
    left: 50\\%;
    z-index: 999;
    width: 520px;
    /* height: 300px; */
    background-color: #fff;
    border-radius: 8px;
    padding: 46px 0 40px;
    transform: translate(-50\\%,-201px);
 \\}
```

我们可以搞个demo多试一试，会发现参与百分比translate偏移的轴，对应的元素宽/高得给个偶数值绝对单位，而如果当前元素宽/高不能为偶数时，对应的translate可以设置为绝对单位的偏移即可，亦或者不参与偏移；

元素宽(W)高(H)						translate偏移值
W：500px ；H: 500px		transform: translate(-50\\%,-50\\%)
W：501px ；H: 500px		transform: translate(-200px,-50\\%)
W：500px ；H: 501px		transform: translate(-50\\%,-200px)
W：501px ；H: 500px		transform: translateY(-50\\%)
W：500px ；H: 501px		transform: translateX(-50\\%)

方法1：
如果是固定的宽高，你可以把宽高各加0.5或者1px,让它变成偶数就不会模糊！

方法2：
在父元素上改成flex布局，让他水平垂直居中，这种方法简单粗暴（推荐！）

```
.ngdialog.ngdialog-theme-default \\{
    padding-bottom: 0;
    padding-top: 0;
    display: flex;
    justify-content: center;//水平居中
    align-items: center;//垂直居中
\\}
```

方法3：
在translate XY方法各加0.5px,用calc函数去计算！

```
.ngdialog.ngdialog-theme-default .ngdialog-content \\{
    position: absolute;
    top: 50\\%;
    left: 50\\%;
    transfrom:translate(calc(-50\\% + 0.5px),calc(-50\\% + 0.5px));
\\}
```

