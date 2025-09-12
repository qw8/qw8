---
title: vue
date: 2024-03-07 21:02:08
categories: 
- 前端知识
tags:
- vue
- MVVM
---

### Vue基础介绍

`Vue.js`是一套构建用户界面的渐进式框架。
 它提供了`MVVM` [数据绑定]()和一个可组合的[组件]()系统。
 在Vue中，一个核心的概念，就是让用户不再操作DOM元素。

- **响应的数据绑定**
   当数据发生改变时，自动更新视图。
   是利用Object.defineProperty中的getter和setter代理数据。
   Vue监控的数据变化就是监控的getter和setter得变化。变化就去重新渲染。

- **视图组件**
   UI页面映射出一个组件树
   组件可重用，可维护性好。
   Vue封装了大量的组件,可以直接使用,简便而而美,省去了大量的Js代码.(有字体\主题\各种表单,表格,图标,按钮,提示框,导航栏等等)
   

  ![img](https:////upload-images.jianshu.io/upload_images/23481186-715b00cd0ec0e684.png?imageMogr2/auto-orient/strip|imageView2/2/w/752/format/webp)

  映射出一个组件树

  

- **虚拟DOM**
   要改变一个DOM节点，才能把视图重新渲染出来。但这样会发生重排重绘，十分耗费性能。
   虚拟DOM就是使用js去模拟一个节点。把js封装出来，变为一个真实的DOM。（使用js对象的嵌套形式模仿出一个html文档），通过底层的算法可以让重排重绘只发生在局部。优化页面。
   ①：真实DOM和其解析流程
   

  ![img](https:////upload-images.jianshu.io/upload_images/23481186-997223c56268abdb.png?imageMogr2/auto-orient/strip|imageView2/2/w/713/format/webp)

  真实DOM和其解析流程

   ②：JS操作真实DOM的代价

   用我们传统的开发模式，原生JS或JQ操作DOM时，浏览器会从构建DOM树开始从头到尾执行一遍流程。在一次操作中，我需要更新10个DOM节点，浏览器收到第一个DOM请求后并不知道还有9次更新操作，因此会马上执行流程，最终执行10次。

   ③：为什么需要虚拟DOM，它有什么好处

   Web界面由DOM树(树的意思是数据结构)来构建，当其中一部分发生变化时，其实就是对应某个DOM节点发生了变化， 虚拟DOM就是为了解决浏览器性能问题而被设计出来的。如前，若一次操作中有10次更新DOM的动作，虚拟DOM不会立即操作DOM，而是将这10次更新的diff内容保存到本地一个JS对象中，最终将这个JS对象一次性attch到DOM树上，再进行后续操作，避免大量无谓的计算量。所以，用JS对象模拟DOM节点的好处是，页面的更新可以先全部反映在JS对象(虚拟DOM)上，操作内存中的JS对象的速度显然要更快，等更新完成后，再将最终的JS对象映射成真实的DOM，交由浏览器去绘制。

  

- **MVVM**
   MVVM（Model-View-ViewModel）是对 MVC（Model-View-Control）的进一步改进。
   『View』：视图层（UI 用户界面）
   『ViewModel』：业务逻辑层（一切 js 可视为业务逻辑）
   『Model』：数据层（存储数据及对数据的处理如增删改查）
   MVVM 将数据[双向绑定（data-binding）]()作为核心思想，View 和 Model 之间没有联系，它们通过 ViewModel 这个桥梁进行交互。
   Model 和 ViewModel 之间的交互是双向的，因此 View 的变化会自动同步到 Model，而 Model 的变化也会立即反映到 View 上显示。
   当用户操作 View，ViewModel 感知到变化，然后通知 Model 发生相应改变；反之当 Model 发生改变，ViewModel 也能感知到变化，使 View 作出相应更新。
   前端页面中使用MVVM的思想，主要是为了让我们开发MVVM提供了数据的双向绑定，双向绑定是由VM提供的
   

  ![img](https:////upload-images.jianshu.io/upload_images/23481186-88ec25d4edd0f08b.png?imageMogr2/auto-orient/strip|imageView2/2/w/562/format/webp)




### VUE的第一个demo

```xml
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <!-- 1. 导入Vue的包 -->
  <script src="./lib/vue-2.4.0.js"></script>
</head>

<body>
  <!-- 将来 new 的Vue实例，会控制这个 元素中的所有内容 -->
  <!-- 3. Vue 实例所控制的这个元素区域，就是我们的 V  -->
  <div id="app">
    <p>\\\{\\\{ msg\\\}\\\} }}</p>
  </div>

  <script>
    // 2. 创建一个Vue的实例
    // 当我们导入包之后，在浏览器的内存中，就多了一个 Vue 构造函数
    //  注意：我们 new 出来的这个 vm 对象，就是我们 MVVM中的 VM调度者
    var vm = new Vue(\\{
      el: '#app',  // 表示，当前我们 new 的这个 Vue 实例，要控制页面上的哪个区域
      // 这里的 data 就是 MVVM中的 M，专门用来保存 每个页面的数据的
      data: \\{ // data 属性中，存放的是 el 中要用到的数据
      msg: '欢迎学习Vue' // 通过 Vue 提供的指令，很方便的就能把数据渲染到页面上，程序员不再手动操作DOM元素了【前端的Vue之类的框架，不提倡我们去手动操作DOM元素了】
      \\}
    \\})
  </script>
</body>

</html>
```



### 常用指令

> Vue中不允许直接操作dom
>  指令是用来操作dom，将数据和dom做关联，当表达式的值改变时，响应式地作用在视图
>  指令是用一个 v-xxx 表示

#### v-bind

 功能：绑定变量， 将一个数据绑定在一个dom的属性上，及时对页面的数据进行更改，可缩写成 ":"

```ruby
<div :id="text"></div>
```

代码说明：将text变量绑定到id属性

#### v-text

 功能：绑定标签内显示内容。将数据解析为纯文本，不能输出真正的html，与花括号的区别是在页面加载时不显示\\\{\\\{\\\}\\\}【加载闪烁问题】
 和插值差不多，也可以从vue对象中获取信息，v-text默认是没有闪烁问题的，但是会覆盖掉原有的内容，但是 插值表达式 只会替换自己的这个占位符，不会把 整个元素的内容清空

```xml
<div v-text="text"></div>
```

代码说明：指定了标签内的文字内容，相当于`innerText`


![img](https:////upload-images.jianshu.io/upload_images/23481186-b54a726f0299e721.png?imageMogr2/auto-orient/strip|imageView2/2/w/381/format/webp)

加载闪烁问题



#### v-html

 功能：以html形式渲染变量内容

```xml
<div v-html="html"></div>
```

代码说明：将html变量以html的形式添加到标签内，相当于`innerHTMl`

如果你在 `  <style>  ` 标签中使用了 `scoped` 属性，那么样式只会应用到当前组件内部。如果你的 HTML 是通过 `v-html` 动态生成的，那么这些元素可能不在当前组件的作用范围内，所以 `scoped` 样式不会生效。

解决方案:

##### 1.使用外部类名

对于动态生成的 HTML，可以为其添加外部类名，然后在全局样式表中定义这些类名的样式（移除 `  <style>  ` 标签中的 `scoped` 属性）。

示例：

```
<template>
  <div v-html="htmlContent"></div>
</template>

<script setup>
import \\{ ref \\} from 'vue';

const htmlContent = ref('<p class="dynamic-text">Hello, World!</p>');
</script>

<!-- 在全局样式文件中 -->
<style>
.dynamic-text \\{
  color: blue;
\\}
</style>
```

##### 2.使用内联样式

对于某些情况，可以直接在 HTML 字符串中使用内联样式。

示例：

```
<template>
  <div v-html="htmlContent"></div>
</template>

<script setup>
import \\{ ref \\} from 'vue';

const htmlContent = ref('<p style="color: red;">Hello, World!</p>');
</script>
```



#### v-show

 功能：可以控制一个dom的显示隐藏（ 这个指令操作的是dom的display属性 ）

```xml
<div v-show="flase"></div>
```

代码说明：相当于`display：none`，虽然不进行节点渲染，但是dom对象一直存在，适用于频繁切换的场景

#### v-if

 功能：可以控制一个dom的存在与否（ 创建 和 销毁 ）

```xml
<div v-if="true"></div>
```

代码说明：相当于`appendChild`，`removeChild`，直接将dom对象添加或者删除，适用于不频繁切换的场景，与v-if配合使用的有，v-else，v-if-else

#### v-for

 功能：循环产生同一个组件

```xml
<ul>
<li v-for="item in items" :key="item">\\\{\\\{item.nam\\\}\\\}e}}</li>
</ul>
```

代码说明：items是一个数组或者对象，将其中每一项都渲染出一个li，值得注意的是每一个li都需要一个独一无二的key，这样才能保证每次重新渲染的时候，只会更改key产生变化的节点，减少了开销，而且不能使用数组的index作为key，因为数组每一项对应的index会产生变化。

#### v-on

 功能：为节点绑定事件，可简写成@

```css
<div @click="open"></div>
```

代码说明：为div绑定了点击事件，点击事件触发open这个函数

#### v-model

 功能：为input提供双向绑定功能

```bash
<inpurt type="text" v-model="value"/>
```

代码说明：直接将value与input进行双向绑定，input的输入会修改value的值，要注意
 v-model与单选框和多选框的配合使用

```bash
<inpurt type="text" v-model.number="value"/>
```

代码说明：.number修饰符将输入变成数值型，.trim则是帮助去除首尾空格

```bash
 <inpurt type="text" v-model.lazy="value"/>
```

代码说明：.lazy修饰符将v-model的绑定事件从input变成onchange事件



### 7.v-show与v-if的区别

v-show是css切换，v-if是完整的销毁和重新创建
使用频繁切换时用v-show,运行时较少改变时用v-if
V-if=’false’v-if是条件渲染，当false的时候不会渲染
使用v-if的时候，如果值为false，那么页面将不会有这个html标签生成
v-show则是不管值是为true还是false，html元素都会存在，只是css中的display显示或隐藏
v-show 仅仅控制元素的显示方式，将 display 属性在 block 和 none 来回切换；而v-if会控制这个 DOM 节点的存在与否。

**当我们需要经常切换某个元素的显示/隐藏时，使用v-show会更加节省性能上的开销；**

**当只需要一次显示或隐藏时，使用v-if更加合理。**



### 8.开发中常用的指令有哪些?

v-model:一般用在表达输入，很轻松的实现表单控件和数据的双向绑定
v-html：更新元素的innerHTML
v-show与v-if：条件渲染，注意二者区别
v-on:click:可以简写为@click,@绑定一个事件。如果事件触发了，就可以指定事件的处理函数
v-for：基于源数据多次渲染元素或模板
v-bind:当表达式的值改变时，将其产生的连带影响，响应式地作用于DOM语法
v-bind:title=”msg”简写 :title="msg"



### Class 与 Style 如何动态绑定？

#### Class可以通过对象语法和数组语法进行动态绑定：

- 对象语法：

```
<div v-bind:class="\\{ active: isActive, 'text-danger': hasError \\}"></div>

data: \\{
  isActive: true,
  hasError: false
\\}
```

- 数组语法：

```
<div v-bind:class="[isActive ? activeClass : '', errorClass]"></div>

data: \\{
  activeClass: 'active',
  errorClass: 'text-danger'
\\}
```

##### 绑定class的数组用法

```js
1.对象方法v-bind:class="\\{'orange':isRipe, 'green':isNotRipe\\}”
2.数组方法v-bind:class="[class1,class2]"
3.行内v-bind:style="\\{color:color,fontSize:fontSize+'px'\\}”
```

#### Style也可以通过对象语法和数组语法进行动态绑定：

- 对象语法：

```
<div v-bind:style="\\{ color: activeColor, fontSize: fontSize + 'px' \\}"></div>

data: \\{
  activeColor: 'red',
  fontSize: 30
\\}
```

- 数组语法：

```
<div v-bind:style="[styleColor, styleSize]"></div>

data: \\{
  styleColor: \\{
     color: 'red'
   \\},
  styleSize:\\{
     fontSize:'23px'
  \\}
\\}
```



### vue 绑定class的几种方式

#### 对象语法

给v-bind:class 设置一个对象，可以动态地切换class，如下

```
<div id="app">
    <div :class="\\{'active':isActive\\}"></div>
</div>
<script>
var app = new Vue(\\{
    el:'#app',
    data:\\{
        isActive:true
    \\}
\\})
</script>
```

类名active依赖于数据isActive,当其为true时候，div会拥有类名active,为false时则没

2.对象中也可以传入多个属性，来动态切换class,另外，:class可以与普通class共存

```
<div id="app">
    <div :class="\\{'active':isActive,'error':isError\\}"></div>
</div>
<script>
var app = new Vue(\\{
    el:'#app',
    data:\\{
        isActive:true,
        isError:false
    \\}
\\})
</script>
最终渲染结果为：<div class="active"></div>
```

当isError为true时，对应的类名更新，如

```
<div class="active error"></div
```

当class的表达式过长或者逻辑复杂时候，还可以绑定一个计算属性，这是一种友好和常见的用法，一般当条件多于两个时，都可以使用data或者computed,例如

```
<div id="app">
    <div :class="classes"></div>
</div>

<script>
var app = new Vue(\\{
    el:'#app',
    data:\\{
        isActive:true,
        isError:null
    \\},
    computed:\\{
        classes()\\{
            return \\{
                active:this.isActive && !this.error,
                'text-fail':this.error && this.error.type ==='fail'
            \\}
        \\}
    \\}
\\})
</script>
```

除了计算属性，也可以直接绑定一个Object类型的数据，或者使用类似计算属性的methods.

#### 数组方法

当需要应用多个class，可以使用数组语法，给:class 绑定一个数组，应用一个class列表

```
<div id="app">
    <div :class="[atvieCls,errorCls]"></div>
</div>
<script>
var app = new Vue(\\{
    el:'#app',
    data:\\{
        atvieCls:'active',
        errorCls:'error'
    \\}
\\})
</script>

最终渲染结果为：<div class="active error"></div>
```

也可以使用三元表达式来根据条件切换class,如：

```
<div id="app">
    <div :class="[isActive ? activeCls : '',errorCls]"></div>
</div>
<script>
var app = new Vue(\\{
    el:'#app',
    data:\\{
        isActive:true,
        atvieCls:'active',
        errorCls:'error'
    \\}
\\})
</script>
```

样式error会始终应用，当数据isActive为真时，样式active才会被应用。class有多个条件时候，这样写较为反锁，可以在数组语法中使用对象语法

```
<div id="app">
    <div :class="[\\{'active':isActive\\},errorCls]"></div>
</div>
<script>
var app = new Vue(\\{
    el:'#app',
    data:\\{
        isActive:true,
        errorCls:'error'
    \\}
\\})
</script>
```

```
:class="['page', \\{ dd: envType===3 \\}, \\{ pc: isPC \\}]"
:class="\\{'tag-item':true, active:index===activeIndex\\}"
```

当与对象语法一样时候，也可以使用data,computed和methods三种方法

#### 在组件上使用 

如果直接在自定义组件上使用class或者:class，样式规则会直接应用到这个组件的根元素上，例如声明一个简单组件

```
Vue.component('my-component',\\{
    template:'<p class="article">test</p>'
\\})
```

在调用这个组件时，应用上面介绍的对象语法或者数组语法绑定class，以对象语法为例

```
<div id="app">
    <my-content :class="\\{'active':isActive\\}"></my-content>
</div>
<script>
var app = new Vue(\\{
    el:'#app',
    data:\\{
        isActive:true
    \\}
\\})
</script>

渲染结果：
<p class="article active">test</p>
```

这种用法仅仅使用于自定义组件的最外层的一个根元素，否则无效，当不满足这种条件或需要给具体的子元素设置类名时候，应当使用组件的props来传递



### 10.路由跳转方式

1.router-link标签会渲染为标签，咋填template中的跳转都是这种；
2.另一种是编辑是导航，也就是通过js跳转比如router.push('/home')



### 11.MVVM

M-model，model代表数据模型，也可以在model中定义数据修改和操作的业务逻辑

V-view,view代表UI组件，它负责将数据模型转化为UI展现出来

VM-viewmodel,viewmodel监听模型数据的改变和控制视图行为、处理用户交互，简单理解就是一个同步view和model的对象，连接model和view



### 13.**vue组件的scoped属性的作用**

在style标签上添加scoped属性，以表示它的样式作用于当下的模块，很好的实现了样式私有化的目的；
但是也得慎用：样式不易（可）修改，而很多时候，我们是需要对公共组件的样式做微调的；

**解决办法：**

①：使用混合型的css样式：（混合使用全局跟本地的样式） 

```
<style> /* 全局样式 */ </style>
<style scoped> /* 本地样式 */ </style>
```

②：深度作用选择器（>>>）如果你希望 scoped 样式中的一个选择器能够作用得“更深”，例如影响子组件，你可以使用 >>> 操作符：

```
<style scoped> .a >>> .b \\{ /* ... */ \\} </style>
```



### 14.vue是渐进式的框架的理解：(**主张最少,没有多做职责之外的事**)

Vue的核心的功能，是一个视图模板引擎，但这不是说Vue就不能成为一个框架。如下图所示，这里包含了Vue的所有部件，在声明式渲染（视图模板引擎）的基础上，我们可以通过添加组件系统、客户端路由、大规模状态管理来构建一个完整的框架。更重要的是，这些功能相互独立，你可以在核心功能的基础上任意选用其他的部件，不一定要全部整合在一起。可以看到，所说的“渐进式”，其实就是Vue的使用方式，同时也体现了Vue的设计的理念 
在我看来，渐进式代表的含义是：主张最少。视图模板引擎
每个框架都不可避免会有自己的一些特点，从而会对使用者有一定的要求，这些要求就是主张，主张有强有弱，它的强势程度会影响在业务开发中的使用方式。
比如说，Angular，它两个版本都是强主张的，如果你用它，必须接受以下东西：
必须使用它的模块机制- 必须使用它的依赖注入- 必须使用它的特殊形式定义组件（这一点每个视图框架都有，难以避免）
所以Angular是带有比较强的排它性的，如果你的应用不是从头开始，而是要不断考虑是否跟其他东西集成，这些主张会带来一些困扰。
Vue可能有些方面是不如React，不如Angular，但它是渐进的，没有强主张，你可以在原有大系统的上面，把一两个组件改用它实现，当jQuery用；也可以整个用它全家桶开发，当Angular用；还可以用它的视图，搭配你自己设计的整个下层用。也可以函数式，都可以，它只是个轻量视图而已，只做了自己该做的事，没有做不该做的事，仅此而已。
**渐进式的含义，我的理解是：没有多做职责之外的事。**



### 15.vue.js的两个核心是什么(数据驱动、组件系统。)

数据驱动:Object.defineProperty和存储器属性: getter和setter（所以只兼容IE9及以上版本），可称为基于依赖收集的观测机制,核心是VM，即ViewModel，保证数据和视图的一致性。
组件系统:[点此查看](https://link.zhihu.com/?target=https\\%3A//blog.csdn.net/tangxiujiang/article/details/79620542\\%23commentBox)



### 16.vue常用修饰符

**修饰符分为：一般修饰符，事件修饰符，按键、系统**

#### ①一般修饰符：

.lazy：v-model 在每次 input 事件触发后将输入框的值与数据进行同步 。你可以添加 lazy 修饰符，从而转变为使用 change 事件进行同步

```js
<input v-model.lazy="msg" >  
```

**.number**

```js
<input v-model.number="age" type="number">
```

**.trim**

自动过滤用户输入的首尾空白字符

```js
<input v-model.trim='trim'>
```



#### ② 事件修饰符

.prevent: 提交事件不再重载页面
.stop: 阻止单击事件冒泡
.self: 当事件发生在该元素本身而不是子元素的时候会触发

```js
<a v-on:click.stop="doThis"></a><!-- 阻止单击事件继续传播 -->

<form v-on:submit.prevent="onSubmit"></form> <!-- 提交事件不再重载页面 -->

<a v-on:click.stop.prevent="doThat"></a> <!-- 修饰符可以串联 -->

<form v-on:submit.prevent></form>   <!-- 只有修饰符 -->

<div v-on:click.capture="doThis">...</div>   <!-- 添加事件监听器时使用事件捕获模式 --> <!-- 即元素自身触发的事件先在此处处理，然后才交由内部元素进行处理 -->

<div v-on:click.self="doThat">...</div>  <!-- 只当在 event.target 是当前元素自身时触发处理函数 --> <!-- 即事件不是从内部元素触发的 -->

<a v-on:click.once="doThis"></a> <!-- 点击事件将只会触发一次 -->
```

##### vue click.stop阻止点击事件继续传播

这个修饰符等同于调用 `event.stopPropagation()`，可以防止事件向上冒泡到父元素。 

```
<div id="app">
		//将会先弹出“noclick”,再弹出“dodo”。
        <div v-on:click="dodo">
            <button v-on:click="doThis">单击事件继续传播</button>
        </div>
        //只弹出“noclick”
         <div v-on:click="dodo">
            <button v-on:click.stop="doThis">阻止单击事件继续传播</button>
        </div>
    </div>

    <script>
        var app = new Vue(\\{
            el: "#app",
            data: \\{
                name: "Vue.js"
            \\},
            methods: \\{
                doThis: function () \\{
                    alert("noclick");
                \\},
                dodo: function () \\{
                    alert("dodo");
                \\}
            \\}
        \\});
    </script>
```



#### ③按键修饰符

全部的按键别名:

```js
.enter
.tab
.delete (捕获“删除”和“退格”键)
.esc
.space
.up
.down
.left
.right
.ctrl
.alt
.shift
.meta
```

```vue
<input v-on:keyup.enter="submit">
或者
<input @keyup.enter="submit">
```



#### ④系统修饰键 （可以用如下修饰符来实现仅在按下相应按键时才触发鼠标或键盘事件的监听器。）

```js
.ctrl
.alt
.shift
.meta
```

```js
<input @keyup.alt.67="clear"> 或者 <div @click.ctrl="doSomething">Do something</div><!-- Ctrl + Click -->
```



### 17.**v-on可以监听多个方法吗？（可以的）**

一个元素绑定多个事件的两种写法，一个事件绑定多个函数的两种写法，修饰符的使用。

```js
<a style="cursor:default" v-on='\\{click:DoSomething,mouseleave:MouseLeave\\}'>doSomething</a>
```

在method方法里面分别写两个时事件；

```js
<button @click="a(),b()">点我ab</button>
```



### 18.**vue事件中如何使用event对象**

```js
<button @click="Event($event)">事件对象</button>
```



### 19.**比如你想让一个dom元素显示**，然后下一步去获取这个元素的offsetWidth，最后你获取到的会是0。

因为你改变数据把show变成true,元素并不会立即显示，理所当然也不会获取到动态宽度。
正确的做法是先把元素show出来，在$nextTick去执行获取宽度的操作，不知道这样说会不会好理解一点。

```js
openSubmenu() \\{
	this.show = true //获取不到宽度
	this.$nextTick(() => //这里才可以 let w = this.$refs.submenu.offsetWidth;
	\\})
\\}
```



### 20.Vue 组件中 data 为什么必须是函数

vue组件中data值不能为对象，**因为对象是引用类型，组件可能会被多个实例同时引用**。
如果data值为对象，将导致多个实例共享一个对象，其中一个组件改变data属性值，其它实例也会受到影响。



### 21.vue中子组件调用父组件的方法

第一种方法是直接在子组件中通过this.$parent.event来调用父组件的方法
第二种方法是在子组件里用$emit向父组件触发一个事件，父组件监听这个事件就行了。
第三种都可以实现子组件调用父组件的方法，

```js
<template>
  <div>
    <button @click="childMethod()">点击</button>
  </div>
</template>
<script>
  export default \\{
    props: \\{
      fatherMethod: \\{
        type: Function,
        default: null
      \\}
    \\},
    methods: \\{
      childMethod() \\{
        if (this.fatherMethod) \\{
          this.fatherMethod();
        \\}
      \\}
    \\}
  \\};
</script>
```



### 22.vue中 keep-alive 组件的作用

keep-alive 是 Vue 内置的一个组件，可以使被包含的组件保留状态，或避免重新渲染。

```js
<keep-alive>
  <component>
    <!-- 该组件将被缓存！ -->
  </component>
</keep-alive>
如果只想 router-view 里面某个组件被缓存

export default [
  \\{
    path: '/',
    name: 'home',
    component: Home,
    meta: \\{
      keepAlive: true // 需要被缓存
    \\}
  \\}, \\{
    path: '/:id',
    name: 'edit',
    component: Edit,
    meta: \\{
      keepAlive: false // 不需要被缓存
    \\}
  \\}
]
<keep-alive>
    <router-view v-if="$route.meta.keepAlive">
        <!-- 这里是会被缓存的视图组件，比如 Home！ -->
    </router-view>
</keep-alive>
 
<router-view v-if="!$route.meta.keepAlive">
    <!-- 这里是不被缓存的视图组件，比如 Edit！ -->
</router-view>
```



### 23.vue中如何编写可复用的组件？

https://blog.csdn.net/qq_38563845/article/details/77524934

①创建组件页面eg Toast.vue；
②用Vue.extend()扩展一个组件构造器,再通过实例化组件构造器,就可创造出可复用的组件
③将toast组件挂载到新创建的div上；
④把toast组件的dom添加到body里；
⑤修改优化达到动态控制页面显示文字跟显示时间；

```js
import Vue from 'vue'; 
import Toast from '@/components/Toast';     //引入组件
let ToastConstructor  = Vue.extend(Toast) // 返回一个“扩展实例构造器”
 
let myToast = (text,duration)=>\\{
    let toastDom = new ToastConstructor(\\{
        el:document.createElement('div')    //将toast组件挂载到新创建的div上
    \\})
    document.body.appendChild( toastDom.$el )   //把toast组件的dom添加到body里
    
    toastDom.text = text;
    toastDom.duration = duration;
 
    // 在指定 duration 之后让 toast消失
    setTimeout(()=>\\{
        toastDom.isShow = false;  
    \\}, toastDom.duration);
\\}
export default myToast;
```



### 26.webpack的作用

①、依赖管理：方便引用第三方模块、让模块更容易复用，避免全局注入导致的冲突、避免重复加载或者加载不需要的模块。会一层一层的读取依赖的模块，添加不同的入口；同时，不会重复打包依赖的模块。
②、合并代码：把各个分散的模块集中打包成大文件，减少HTTP的请求链接数，配合UglifyJS（压缩代码）可以减少、优化代码的体积。
③、各路插件：统一处理引入的插件，babel编译ES6文件，TypeScript,eslint 可以检查编译期的错误。
**一句话总结：**webpack 的作用就是处理依赖，模块化，打包压缩文件，管理插件。
一切皆为模块，由于webpack只支持js文件，所以需要用loader 转换为webpack支持的模块，其中plugin 用于扩张webpack 的功能，在webpack构建生命周期的过程中，在合适的时机做了合适的事情。



### webpack怎么工作的过程

①解析配置参数，合并从shell(npm install 类似的命令)和webpack.config.js文件的配置信息，输出最终的配置信息；
②注册配置中的插件,让插件监听webpack构建生命周期中的事件节点，做出对应的反应；
③解析配置文件中的entry入口文件，并找出每个文件依赖的文件，递归下去；
④在递归每个文件的过程中，根据文件类型和配置文件中的loader找出对应的loader对文件进行转换；
⑤递归结束后得到每个文件最终的结果，根据entry 配置生成代码chunk(打包之后的名字)；
⑥输出所以chunk 到文件系统。



### 27.vue等单页面应用及其优缺点

**缺点：**

> 不支持低版本的浏览器，最低只支持到IE9；
> 不利于SEO的优化（如果要支持SEO，建议通过服务端来进行渲染组件）；
> 第一次加载首页耗时相对长一些；
> 不可以使用浏览器的导航按钮需要自行实现前进、后退。

**优点：**

> 无刷新体验,提升了用户体验；
> 前端开发不再以页面为单位，更多地采用组件化的思想，代码结构和组织方式更加规范化，便于修改和调整；
> API 共享，同一套后端程序代码不用修改就可以用于Web界面、手机、平板等多种客户端
> 用户体验好、快，内容的改变不需要重新加载整个页面。



### 28.什么是vue的计算属性computed

计算属性是需要复杂的逻辑，可以用方法method代替

```js
computed:\\{
    totalPrice()\\{
      return (this.good.price*this.good.count)*this.discount+this.deliver;
    \\}
  \\}
```



### 29.vue-cli提供的几种脚手架模板

> vue-cli 的脚手架项目模板有browserify 和 webpack；



### 30.组件中传递数据？

```js
props：export default \\{
props: \\{
	message: String //定义传值的类型<br>
\\},

//或者props:["message"]
data: \\{\\}
父组件调用子组件的方法：父组件   this.$refs.yeluosen.childMethod()
子组件向父组件传值并调用方法 $emit
组件之间：bus==$emit+$on
```



### 32.vue-router 的导航钩子,主要用来作用是拦截导航,让他完成跳转或取消。

> **全局的:**前置守卫、后置钩子（beforeEach，afterEach）beforeResolve
> **单个路由独享的:**beforeEnter
> **组件级的:** beforeRouteEnter（不能获取组件实例 this）、beforeRouteUpdate、beforeRouteLeave
> 这是因为在执行路由钩子函数beforRouteEnter时候，组件还没有被创建出来；
> 先执行beforRouteEnter，再执行组件周期钩子函数beforeCreate，可以通过 next 获取组件的实例对象，如：next( (vm)=>\\{\\} )，参数vm就是组件的实例化对象。



### 33.完整的 vue-router 导航解析流程

> 1.导航被触发；
> 2.在失活的组件里调用beforeRouteLeave守卫；
> 3.调用全局beforeEach守卫；
> 4.在复用组件里调用beforeRouteUpdate守卫；
> 5.调用路由配置里的beforeEnter守卫；
> 6.解析异步路由组件；
> 7.在被激活的组件里调用beforeRouteEnter守卫；
> 8.调用全局beforeResolve守卫；
> 9.导航被确认；
> 10..调用全局的afterEach钩子；
> 11.DOM更新；
> 12.用创建好的实例调用beforeRouteEnter守卫中传给next的回调函数。



### 34.vue-router如何响应 路由参数 的变化？

**原来的组件实例会被复用。这也意味着组件的生命周期钩子不会再被调用。你可以简单地 watch (监测变化) $route 对象：**

```js
const User = \\{
  template: '...',
  watch: \\{
    '$route' (to, from) \\{
      // 对路由变化作出响应...
    \\}
  \\}
\\}


const User = \\{
  template: '...',
  watch: \\{
    '$route' (to, from) \\{
      // 对路由变化作出响应...
    \\}
  \\}
\\}
```



### 35.vue-router的几种实例方法以及参数传递

> name传递
> to来传递
> 采用url传参



### 36.is的用法（用于动态组件且基于 DOM 内模板的限制来工作。）

is用来动态切换组件，DOM模板解析

```js
<table> <tr is="my-row"></tr> </table>
```



### [动态组件](https://v2.cn.vuejs.org/v2/guide/components.html#动态组件)

有的时候，在不同组件之间进行动态切换是非常有用的，比如在一个多标签的界面里： 

上述内容可以通过 Vue 的 ` <component> ` 元素加一个特殊的 `is` attribute 来实现： 

```
<!-- 组件会在 `currentTabComponent` 改变时改变 -->
<component v-bind:is="currentTabComponent"></component>
```

在上述示例中，`currentTabComponent` 可以包括

- 已注册组件的名字，或
- 一个组件的选项对象

 请留意，这个 attribute 可以用于常规 HTML 元素，但这些元素将被视为组件，这意味着所有的 attribute **都会作为 DOM attribute 被绑定**。对于像 `value` 这样的 property，若想让其如预期般工作，你需要使用 [`.prop` 修饰器](https://v2.cn.vuejs.org/v2/api/#v-bind)。 



### 说说你对 SPA 单页面的理解，它的优缺点分别是什么？

SPA（ single-page application ）仅在 Web 页面初始化时加载相应的 HTML、JavaScript 和 CSS。一旦页面加载完成，SPA 不会因为用户的操作而进行页面的重新加载或跳转；取而代之的是利用路由机制实现 HTML 内容的变换，UI 与用户的交互，避免页面的重新加载。

优点：

- 用户体验好、快，内容的改变不需要重新加载整个页面，避免了不必要的跳转和重复渲染；
- 基于上面一点，SPA 相对对服务器压力小；
- 前后端职责分离，架构清晰，前端进行交互逻辑，后端负责数据处理；

缺点：

- 初次加载耗时多：为实现单页 Web 应用功能及显示效果，需要在加载页面的时候将 JavaScript、CSS 统一加载，部分页面按需加载；
- 前进后退路由管理：由于单页应用在一个页面中显示所有的内容，所以不能使用浏览器的前进后退功能，所有的页面切换需要自己建立堆栈管理；
- SEO 难度较大：由于所有的内容都在一个页面中动态替换显示，所以在 SEO 上其有着天然的弱势。



### v-show 与 v-if 有什么区别？

v-if 是真正的条件渲染，因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建；也是惰性的：如果在初始渲染时条件为假，则什么也不做——直到条件第一次变为真时，才会开始渲染条件块。

v-show 就简单得多——不管初始条件是什么，元素总是会被渲染，并且只是简单地基于 CSS 的 “display” 属性进行切换。

所以，v-if 适用于在运行时很少改变条件，不需要频繁切换条件的场景；v-show 则适用于需要非常频繁切换条件的场景。



### Class 与 Style 如何动态绑定？

Class 可以通过对象语法和数组语法进行动态绑定：

- 对象语法：

```jsx
<div v-bind:class="\\{ active: isActive, 'text-danger': hasError \\}"></div>
```

- 数组语法：

```jsx
<div v-bind:class="[isActive ? activeClass : '', errorClass]"></div>
```

Style 也可以通过对象语法和数组语法进行动态绑定：

- 对象语法：

```xml
<div v-bind:style="\\{ color: activeColor, fontSize: fontSize + 'px' \\}"></div>
```

- 数组语法：

```xml
<div v-bind:style="[styleColor, styleSize]"></div>
```



### 怎样理解 Vue 的单向数据流？

所有的 prop 都使得其父子 prop 之间形成了一个单向下行绑定：父级 prop 的更新会向下流动到子组件中，但是反过来则不行。

这样会防止从子组件意外改变父级组件的状态，从而导致你的应用的数据流向难以理解。

额外的，每次父级组件发生更新时，子组件中所有的 prop 都将会刷新为最新的值。这意味着你不应该在一个子组件内部改变 prop。如果你这样做了，Vue 会在浏览器的控制台中发出警告。

子组件想修改时，只能通过 $emit 派发一个自定义事件，父组件接收到后，由父组件修改。

有两种常见的试图改变一个 prop 的情形 :

- 这个 prop 用来传递一个初始值；这个子组件接下来希望将其作为一个本地的 prop 数据来使用。 在这种情况下，最好定义一个本地的 data 属性并将这个 prop 用作其初始值：

```bash
props: ['initialCounter'],
```

- 这个 prop 以一种原始的值传入且需要进行转换。 在这种情况下，最好使用这个 prop 的值来定义一个计算属性

```bash
props: ['size'],
```



### computed 和 watch 的区别和运用的场景？

computed： 是计算属性，依赖其它属性值，并且 computed 的值有缓存，只有它依赖的属性值发生改变，下一次获取 computed 的值时才会重新计算 computed 的值；

watch： 更多的是「观察」的作用，类似于某些数据的监听回调 ，每当监听的数据变化时都会执行回调进行后续操作；

运用场景：

- 当我们需要进行数值计算，并且依赖于其它数据时，应该使用 computed，因为可以利用 computed 的缓存特性，避免每次获取值时，都要重新计算；
- 当我们需要在数据变化时执行异步或开销较大的操作时，应该使用 watch，使用 watch 选项允许我们执行异步操作 ( 访问一个 API )，限制我们执行该操作的频率，并在我们得到最终结果前，设置中间状态。这些都是计算属性无法做到的。



### 直接给一个数组项赋值，Vue 能检测到变化吗？

由于 JavaScript 的限制，Vue 不能检测到以下数组的变动：

- 当你利用索引直接设置一个数组项时，例如：vm.items[indexOfItem] = newValue
- 当你修改数组的长度时，例如：vm.items.length = newLength

为了解决第一个问题，Vue 提供了以下操作方法：

```cpp
// Vue.set
```

为了解决第二个问题，Vue 提供了以下操作方法：

```cpp
// Array.prototype.splice
```



### 谈谈你对 Vue 生命周期的理解？

#### （1）生命周期是什么？

Vue 实例有一个完整的生命周期，也就是从开始创建、初始化数据、编译模版、挂载 Dom -> 渲染、更新 -> 渲染、卸载等一系列过程，我们称这是 Vue 的生命周期。

#### （2）各个生命周期的作用

| 生命周期      | 描述                                                         |
| ------------- | ------------------------------------------------------------ |
| beforeCreate  | 组件实例被创建之初，组件的属性生效之前                       |
| created       | 组件实例已经完全创建，属性也绑定，但真实 dom 还没有生成，$el 还不可用 |
| beforeMount   | 在挂载开始之前被调用：相关的 render 函数首次被调用           |
| mounted       | el 被新创建的 vm.$el 替换，并挂载到实例上去之后调用该钩子    |
| beforeUpdate  | 组件数据更新之前调用，发生在虚拟 DOM 打补丁之前              |
| update        | 组件数据更新之后                                             |
| activited     | keep-alive 专属，组件被激活时调用                            |
| deactivated   | keep-alive 专属，组件被销毁时调用                            |
| beforeDestory | 组件销毁前调用                                               |
| destoryed     | 组件销毁后调用                                               |

#### （3）生命周期示意图

![img](https:////upload-images.jianshu.io/upload_images/12842279-43f8b23ff3bd3a30?imageMogr2/auto-orient/strip|imageView2/2/w/640/format/webp)



### Vue 的父组件和子组件生命周期钩子函数执行顺序？

Vue 的父组件和子组件生命周期钩子函数执行顺序可以归类为以下 4 部分：

- 加载渲染过程

  父 beforeCreate -> 父 created -> 父 beforeMount -> 子 beforeCreate -> 子 created -> 子 beforeMount -> 子 mounted -> 父 mounted

- 子组件更新过程

  父 beforeUpdate -> 子 beforeUpdate -> 子 updated -> 父 updated

- 父组件更新过程

  父 beforeUpdate -> 父 updated

- 销毁过程

  父 beforeDestroy -> 子 beforeDestroy -> 子 destroyed -> 父 destroyed



### 在哪个生命周期内调用异步请求？

可以在钩子函数 created、beforeMount、mounted 中进行调用，因为在这三个钩子函数中，data 已经创建，可以将服务端端返回的数据进行赋值。但是本人推荐在 created 钩子函数中调用异步请求，因为在 created 钩子函数中调用异步请求有以下优点：

- 能更快获取到服务端数据，减少页面 loading 时间；
- ssr 不支持 beforeMount 、mounted 钩子函数，所以放在 created 中有助于一致性；



### 在什么阶段才能访问操作DOM？

在钩子函数 mounted 被调用前，Vue 已经将编译好的模板挂载到页面上，所以在 mounted 中可以访问操作 DOM。vue 具体的生命周期示意图可以参见如下，理解了整个生命周期各个阶段的操作，关于生命周期相关的面试题就难不倒你了。

![img](https:////upload-images.jianshu.io/upload_images/12842279-f01c5f655dd3628a?imageMogr2/auto-orient/strip|imageView2/2/w/640/format/webp)

### 父组件可以监听到子组件的生命周期吗？

比如有父组件 Parent 和子组件 Child，如果父组件监听到子组件挂载 mounted 就做一些逻辑处理，可以通过以下写法实现：

```cpp
// Parent.vue
```

以上需要手动通过 $emit 触发父组件的事件，更简单的方式可以在父组件引用子组件时通过 @hook 来监听即可，如下所示：

```cpp
//  Parent.vue
```

当然 @hook 方法不仅仅是可以监听 mounted，其它的生命周期事件，例如：created，updated 等都可以监听。



### 谈谈你对 keep-alive 的了解？

keep-alive 是 Vue 内置的一个组件，可以使被包含的组件保留状态，避免重新渲染 ，其有以下特性：

- 一般结合路由和动态组件一起使用，用于缓存组件；
- 提供 include 和 exclude 属性，两者都支持字符串或正则表达式， include 表示只有名称匹配的组件会被缓存，exclude 表示任何名称匹配的组件都不会被缓存 ，其中 exclude 的优先级比 include 高；
- 对应两个钩子函数 activated 和 deactivated ，当组件被激活时，触发钩子函数 activated，当组件被移除时，触发钩子函数 deactivated。



### 组件中 data 为什么是一个函数？

为什么组件中的 data 必须是一个函数，然后 return 一个对象，而 new Vue 实例里，data 可以直接是一个对象？

```cpp
// data
```

因为组件是用来复用的，且 JS 里对象是引用关系，如果组件中 data 是一个对象，那么这样作用域没有隔离，子组件中的 data 属性值会相互影响，如果组件中 data 选项是一个函数，那么每个实例可以维护一份被返回对象的独立的拷贝，组件实例之间的 data 属性值不会互相影响；而 new Vue 的实例，是不会被复用的，因此不存在引用对象的问题。



### v-model 的原理？

我们在 vue 项目中主要使用 v-model 指令在表单 input、textarea、select 等元素上创建双向数据绑定，我们知道 v-model 本质上不过是语法糖，v-model 在内部为不同的输入元素使用不同的属性并抛出不同的事件：

- text 和 textarea 元素使用 value 属性和 input 事件；
- checkbox 和 radio 使用 checked 属性和 change 事件；
- select 字段将 value 作为 prop 并将 change 作为事件。

以 input 表单元素为例：

```xml
<input v-model='something'>
```

如果在自定义组件中，v-model 默认会利用名为 value 的 prop 和名为 input 的事件，如下所示：

```undefined
父组件：
```



### Vue 组件间通信有哪几种方式？

Vue 组件间通信是面试常考的知识点之一，这题有点类似于开放题，你回答出越多方法当然越加分，表明你对 Vue 掌握的越熟练。Vue 组件间通信只要指以下 3 类通信：父子组件通信、隔代组件通信、兄弟组件通信，下面我们分别介绍每种通信方式且会说明此种方法可适用于哪类组件间通信。

**（1）props / $emit 适用 父子组件通信**

这种方法是 Vue 组件的基础，相信大部分同学耳闻能详，所以此处就不举例展开介绍。

**（2）ref 与 ![parent /](https://math.jianshu.com/math?formula=parent\\%20\\%2F)children 适用 父子组件通信**

- ref：如果在普通的 DOM 元素上使用，引用指向的就是 DOM 元素；如果用在子组件上，引用就指向组件实例
- ![parent /](https://math.jianshu.com/math?formula=parent\\%20\\%2F)children：访问父 / 子实例

**（3）EventBus （![emit /](https://math.jianshu.com/math?formula=emit\\%20\\%2F)on） 适用于 父子、隔代、兄弟组件通信**

这种方法通过一个空的 Vue 实例作为中央事件总线（事件中心），用它来触发事件和监听事件，从而实现任何组件间的通信，包括父子、隔代、兄弟组件。

**（4）![attrs/](https://math.jianshu.com/math?formula=attrs\\%2F)listeners 适用于 隔代组件通信**

- ![attrs：包含了父作用域中不被 prop 所识别 (且获取) 的特性绑定 ( class 和 style 除外 )。当一个组件没有声明任何 prop 时，这里会包含所有父作用域的绑定 ( class 和 style 除外 )，并且可以通过 v-bind="](https://math.jianshu.com/math?formula=attrs\\%EF\\%BC\\%9A\\%E5\\%8C\\%85\\%E5\\%90\\%AB\\%E4\\%BA\\%86\\%E7\\%88\\%B6\\%E4\\%BD\\%9C\\%E7\\%94\\%A8\\%E5\\%9F\\%9F\\%E4\\%B8\\%AD\\%E4\\%B8\\%8D\\%E8\\%A2\\%AB\\%20prop\\%20\\%E6\\%89\\%80\\%E8\\%AF\\%86\\%E5\\%88\\%AB\\%20(\\%E4\\%B8\\%94\\%E8\\%8E\\%B7\\%E5\\%8F\\%96)\\%20\\%E7\\%9A\\%84\\%E7\\%89\\%B9\\%E6\\%80\\%A7\\%E7\\%BB\\%91\\%E5\\%AE\\%9A\\%20(\\%20class\\%20\\%E5\\%92\\%8C\\%20style\\%20\\%E9\\%99\\%A4\\%E5\\%A4\\%96\\%20)\\%E3\\%80\\%82\\%E5\\%BD\\%93\\%E4\\%B8\\%80\\%E4\\%B8\\%AA\\%E7\\%BB\\%84\\%E4\\%BB\\%B6\\%E6\\%B2\\%A1\\%E6\\%9C\\%89\\%E5\\%A3\\%B0\\%E6\\%98\\%8E\\%E4\\%BB\\%BB\\%E4\\%BD\\%95\\%20prop\\%20\\%E6\\%97\\%B6\\%EF\\%BC\\%8C\\%E8\\%BF\\%99\\%E9\\%87\\%8C\\%E4\\%BC\\%9A\\%E5\\%8C\\%85\\%E5\\%90\\%AB\\%E6\\%89\\%80\\%E6\\%9C\\%89\\%E7\\%88\\%B6\\%E4\\%BD\\%9C\\%E7\\%94\\%A8\\%E5\\%9F\\%9F\\%E7\\%9A\\%84\\%E7\\%BB\\%91\\%E5\\%AE\\%9A\\%20(\\%20class\\%20\\%E5\\%92\\%8C\\%20style\\%20\\%E9\\%99\\%A4\\%E5\\%A4\\%96\\%20)\\%EF\\%BC\\%8C\\%E5\\%B9\\%B6\\%E4\\%B8\\%94\\%E5\\%8F\\%AF\\%E4\\%BB\\%A5\\%E9\\%80\\%9A\\%E8\\%BF\\%87\\%20v-bind\\%3D\\%22)attrs" 传入内部组件。通常配合 inheritAttrs 选项一起使用。
- ![listeners：包含了父作用域中的 (不含 .native 修饰器的) v-on 事件监听器。它可以通过 v-on="](https://math.jianshu.com/math?formula=listeners\\%EF\\%BC\\%9A\\%E5\\%8C\\%85\\%E5\\%90\\%AB\\%E4\\%BA\\%86\\%E7\\%88\\%B6\\%E4\\%BD\\%9C\\%E7\\%94\\%A8\\%E5\\%9F\\%9F\\%E4\\%B8\\%AD\\%E7\\%9A\\%84\\%20(\\%E4\\%B8\\%8D\\%E5\\%90\\%AB\\%20.native\\%20\\%E4\\%BF\\%AE\\%E9\\%A5\\%B0\\%E5\\%99\\%A8\\%E7\\%9A\\%84)\\%20v-on\\%20\\%E4\\%BA\\%8B\\%E4\\%BB\\%B6\\%E7\\%9B\\%91\\%E5\\%90\\%AC\\%E5\\%99\\%A8\\%E3\\%80\\%82\\%E5\\%AE\\%83\\%E5\\%8F\\%AF\\%E4\\%BB\\%A5\\%E9\\%80\\%9A\\%E8\\%BF\\%87\\%20v-on\\%3D\\%22)listeners" 传入内部组件

**（5）provide / inject 适用于 隔代组件通信**

祖先组件中通过 provider 来提供变量，然后在子孙组件中通过 inject 来注入变量。provide / inject API 主要解决了跨级组件间的通信问题，不过它的使用场景，主要是子组件获取上级组件的状态，跨级组件间建立了一种主动提供与依赖注入的关系。

**（6）Vuex 适用于 父子、隔代、兄弟组件通信**

Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。每一个 Vuex 应用的核心就是 store（仓库）。“store” 基本上就是一个容器，它包含着你的应用中大部分的状态 ( state )。

- Vuex 的状态存储是响应式的。当 Vue 组件从 store 中读取状态的时候，若 store 中的状态发生变化，那么相应的组件也会相应地得到高效更新。
- 改变 store 中的状态的唯一途径就是显式地提交 (commit) mutation。这样使得我们可以方便地跟踪每一个状态的变化。

#### 父传子

##### props

```vue
//child
props: \\{
  msg: String;
\\}

// parent
<HelloWorld msg="Welcome to Your Vue.js App" />;
```

##### refs

```vue
// parent
<HelloWorld ref="hw" />

this.$refs.hw.xx
```


#### 子传父

``` vue
// child
this.$emit('add', good)

// parent
<div @add="cartAdd($event)"></div>
```

#### .sync 传参绑定

.sync 其实也是事件传参的语法糖，父组件 以这样的形式@update:msg="changeEmit" 子组件 this.$emit('update:msg',this.msg)进行触发 而sync是可以进行简写的

```vue 
// 父组件
<template>
    <div class="hello">
        \\\{\\\{ms\\\}\\\}g}}
        <son @update:msg="changeEmit"></son>
        // 这下面是上面的语法糖，可以简写成这样
        <son :msg.sync="msg"></son>
    </div>
</template>
<script>
    import son from './son.vue'
    export default \\{
        components:\\{
            son
        \\},
        data()\\{
            return\\{
                msg:"我是父亲"
            \\}
        \\},
        methods:\\{
            changeEmit(value)\\{
                this.msg = value
            \\}
        \\}
    \\}
</script>
// 子组件
<template>
     <div>\\\{\\\{ms\\\}\\\}g}}</div>
</template>
<script>
    export default \\{
        data()\\{
             return\\{
                  msg:"我是儿子emit"
             \\}
        \\},
         mounted() \\{
              this.$emit('update:msg',this.msg)
         \\}
    \\}
</script>

```

#### 兄弟组件：通过共同祖辈组件

通过共同的祖辈组件搭桥，$parent或$root。

```javascript
// brother1
this.$parent.$on("foo", handle);
// brother2
this.$parent.$emit("foo");
```

#### EventBus

EventBus 又称为事件总线。在Vue中可以使用 EventBus 来作为沟通桥梁的概念， 就像是所有组件共用相同的事件中心，可以向该中心注册发送事件或接收事件， 所以组件都可以上下平行地通知其他组件，但也就是太方便所以若使用不慎， 就会造成难以维护的灾难，因此才需要更完善的Vuex作为状态管理中心，将通知的概念上升到共享状态层次。

平常我们采用更多的是父传子，子传父，当遇到兄弟之间的组件通信的时候 就可以使用EventBus
如下例 Vue.prototype.$EventBus = new Vue() 这句话的意思是 因为Vue的原型上有$on $emit 方法 继承自vue原型上的方法，实现一个发布订阅模式

```vue
// main.js
//这句话的意思是 因为Vue的原型上有$on $emit 方法 继承自vue原型上的方法，实现一个发布订阅模式
Vue.prototype.$EventBus = new Vue()
// 父组件-----------------
<template>
    <div class="hello">
        \\\{\\\{ms\\\}\\\}g}}
        <son></son>
        <son1></son1>
    </div>
</template>
<script>
    import son from './son.vue'
    import son1 from './son1.vue'
    export default \\{
        components:\\{
            son,
            son1
        \\},
        data()\\{
            return\\{
                msg:"我是父亲"
            \\}
        \\},

    \\}
</script>

// 子组件son------------------------
<template>
     <div>
          <span>\\\{\\\{sonValu\\\}\\\}e}}</span>
     </div>
</template>
<script>
    export default \\{
        data()\\{
          return\\{
               sonValue:"我是son1"
          \\}
        \\},
         mounted() \\{
             this.$EventBus.$on('son1',(val)=>\\{
                  this.sonValue = val
             \\})
         \\}
    \\}
</script>

// 子组件son1----------------
<template>
     <div>
          <span>\\\{\\\{sonValu\\\}\\\}e}}</span>
          <button @click="btn">在son1里面改变son的值</button>
     </div>
</template>
<script>
    export default \\{
        data()\\{
          return\\{
               sonValue:"我是son2"
          \\}
        \\},
         methods:\\{
             btn()\\{
                  this.$EventBus.$emit('son1','在son1里面改变son的值')
             \\}
         \\}
    \\}
</script>
​``` -->

### 祖先和后代之间

provide/inject：能够实现祖先给后代传值

​```javascript
// ancestor
provide() \\{    
    return \\{foo: 'foo'\\}
\\}

// descendant
inject: ['foo']
```

#### dispatch：后代给祖先传值

``` javascript
//定义一个dispatch方法，指定要派发事件名称和数据
function dispatch(eventName, data) \\{
  let parent = this.$parent;
  // 只要还存在父元素就继续往上查找
  while (parent) \\{
    // 父元素用$emit触发
    parent.$emit(eventName, data);
    // 递归查找父元素
    parent = parent.$parent;
  \\}
\\}

// 使用，HelloWorld.vue
<h1 @click="dispatch('hello', 'hello,world')">\\\{\\\{ msg\\\}\\\} }}</h1>

// App.vue
this.$on('hello', this.sayHello)
```

#### 任意两个组件之间：事件总线 或 vuex

事件总线：创建一个 Bus 类负责事件派发、监听和回调管理

```javascript
// Bus：事件派发、监听和回调管理
class Bus \\{
  constructor() \\{
    // \\{
    //   eventName1:[fn1,fn2],
    //   eventName2:[fn3,fn4],
    // \\}
    this.callbacks = \\{\\};
  \\}
  $on(name, fn) \\{
    this.callbacks[name] = this.callbacks[name] || [];
    this.callbacks[name].push(fn);
  \\}
  $emit(name, args) \\{
    if (this.callbacks[name]) \\{
      this.callbacks[name].forEach(cb => cb(args));
    \\}
  \\}
\\}

// main.js
Vue.prototype.$bus = new Bus()

// child1 
this.$bus.$on('foo', handle) 
// child2 
this.$bus.$emit('foo')
```

vuex：创建唯一的全局数据管理者 store，通过它管理数据并通知组件状态变更



### .sync修饰符

#### 1.作用

可以实现子组件与父组件数据的双向绑定，简化代码

简单理解:子组件可以修改父组件传过来的props值

#### 2.场景

封装弹框类的基础组件， visible属性true显示false隐藏

特点:prop属性名，可以自定义，非固定为value

#### 3.本质

.sync修饰符就是:属性名和@update:属性名合写

.sync(有语义)

:属性.sync='数据' 相当于

：属性=“数据“ + @update：属性="数据=$event"

```
<base-select :selectId="selectId"@update:selectId="selectId = $event" >
```

相当于

```
<base-select :selectId.sync="selectId"/>
```

v-model中的value不具有语义，要使其有语义写成 **：属性名=" 数据" @update:属性名=" 数据"**

来替换原来的 **：属性名="数据" @input="数据"**

#### 4.案例一

App.vue

```
<template>
  <div>
    <h1>大标题</h1>
    <!-- <header-comp :projectId="selectId" @changeId="selectId=$event"></header-comp> -->
<header-comp :selectId="selectId" @update:selectId="selectId=$event"></header-comp>
  </div>
</template>
 
<script>
import HeaderComp from './components/HeaderComp.vue'
 
export default \\{
  components: \\{
    HeaderComp
  \\},
  data () \\{
    return \\{
      selectId: '2'
 
    \\}
  \\}
 
\\}
</script>
 
<style>
 
</style>
```

HeaderComp.vue

```
<template>
  <div class="fa">
    <h2>h2文章二级标题</h2>
<select name="" id="" :value="selectId"  @change="handleChange">
  <option value="1">html</option>
  <option value="2">css</option>
  <option value="3">js</option>
</select>
  </div>
</template>
 
<script>
 
export default \\{
  props: \\{
    selectId: String
  \\},
  methods: \\{
    handleChange (e) \\{
      console.log(e.target.value)
      this.$emit('update:selectId', e.target.value)
    \\}
  \\}
 
\\}
</script>
 
<style>
 
</style>
```

用.sync修饰符简化，只需将App.vue中的子组件标签写成

```
<header-comp :selectId.sync="selectId"></header-comp>
```

#### 5.案例二

father.vue

```
<template>
 <div class="hello">
 <input type="text" v-model="wrd">
 <box :wrd.sync="wrd"></box>
 </div>
</template>
<script>
import box from './box'
export default \\{
 name: 'HelloWorld',
 data() \\{
 return \\{
  wrd: ''
 \\}
 \\},
 methods: \\{
 boxIncremend(e) \\{
  this.wrd = e
 \\}
 \\},
 components: \\{
 box
 \\}
\\}
</script>
```

child.vue

```
<template>
 <div class="hello">
  <input type="text" v-model="str">
 <h2>\\\{\\\{ word\\\}\\\} }}</h2>
 </div>
</template>
<script>
export default \\{
 name: 'box',
 props: \\{
 word: ''
 \\},
 watch: \\{
 str: function(newword) \\{
  //往父级发射incre事件
  this.$emit('update:word', newword)
 \\}
 \\},
\\}
</script>
```

父组件中的子组件，少写了一个自定义事件属性，子组件中$emit直接出发父组件中数据的更新，清新明了。使用中需要注意的是，update和后面对应的数据名不能写错。 



### 你使用过 Vuex 吗？

Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。每一个 Vuex 应用的核心就是 store（仓库）。“store” 基本上就是一个容器，它包含着你的应用中大部分的状态 ( state )。

（1）Vuex 的状态存储是响应式的。当 Vue 组件从 store 中读取状态的时候，若 store 中的状态发生变化，那么相应的组件也会相应地得到高效更新。

（2）改变 store 中的状态的唯一途径就是显式地提交 (commit) mutation。这样使得我们可以方便地跟踪每一个状态的变化。

主要包括以下几个模块：

- State：定义了应用状态的数据结构，可以在这里设置默认的初始状态。
- Getter：允许组件从 Store 中获取数据，mapGetters 辅助函数仅仅是将 store 中的 getter 映射到局部计算属性。
- Mutation：是唯一更改 store 中状态的方法，且必须是同步函数。
- Action：用于提交 mutation，而不是直接变更状态，可以包含任意异步操作。
- Module：允许将单一的 Store 拆分为多个 store 且同时保存在单一的状态树中。



### 使用过 Vue SSR 吗？说说 SSR？

> Vue.js 是构建客户端应用程序的框架。默认情况下，可以在浏览器中输出 Vue 组件，进行生成 DOM 和操作 DOM。然而，也可以将同一个组件渲染为服务端的 HTML 字符串，将它们直接发送到浏览器，最后将这些静态标记"激活"为客户端上完全可交互的应用程序。
>
> 即：SSR大致的意思就是vue在客户端将标签渲染成的整个 html 片段的工作在服务端完成，服务端形成的html 片段直接返回给客户端这个过程就叫做服务端渲染。



### 服务端渲染 SSR 的优缺点如下：

（1）服务端渲染的优点：

- 更好的 SEO：因为 SPA 页面的内容是通过 Ajax 获取，而搜索引擎爬取工具并不会等待 Ajax 异步完成后再抓取页面内容，所以在 SPA 中是抓取不到页面通过 Ajax 获取到的内容；而 SSR 是直接由服务端返回已经渲染好的页面（数据已经包含在页面中），所以搜索引擎爬取工具可以抓取渲染好的页面；
- 更快的内容到达时间（首屏加载更快）：SPA 会等待所有 Vue 编译后的 js 文件都下载完成后，才开始进行页面的渲染，文件下载等需要一定的时间等，所以首屏渲染需要一定的时间；SSR 直接由服务端渲染好页面直接返回显示，无需等待下载 js 文件及再去渲染等，所以 SSR 有更快的内容到达时间；

（2) 服务端渲染的缺点：

- 更多的开发条件限制：例如服务端渲染只支持 beforCreate 和 created 两个钩子函数，这会导致一些外部扩展库需要特殊处理，才能在服务端渲染应用程序中运行；并且与可以部署在任何静态文件服务器上的完全静态单页面应用程序 SPA 不同，服务端渲染应用程序，需要处于 Node.js server 运行环境；
- 更多的服务器负载：在 Node.js 中渲染完整的应用程序，显然会比仅仅提供静态文件的 server 更加大量占用CPU 资源 (CPU-intensive - CPU 密集)，因此如果你预料在高流量环境 ( high traffic ) 下使用，请准备相应的服务器负载，并明智地采用缓存策略。

如果没有 SSR 开发经验的同学，可以参考本文作者的另一篇 SSR 的实践文章《Vue SSR 踩坑之旅》，里面 SSR 项目搭建以及附有项目源码。



### vue-router 路由模式有几种？

vue-router 有 3 种路由模式：hash、history、abstract，对应的源码如下所示：

```cpp
switch (mode) \\{
```

其中，3 种路由模式的说明如下：

- hash: 使用 URL hash 值来作路由。支持所有浏览器，包括不支持 HTML5 History Api 的浏览器；
- history : 依赖 HTML5 History API 和服务器配置。具体可以查看 HTML5 History 模式；
- abstract : 支持所有 JavaScript 运行环境，如 Node.js 服务器端。如果发现没有浏览器的 API，路由会自动强制进入这个模式.



### 能说下 vue-router 中常用的 hash 和 history 路由模式实现原理吗？

#### （1）hash 模式的实现原理

早期的前端路由的实现就是基于 location.hash 来实现的。其实现原理很简单，location.hash 的值就是 URL 中 # 后面的内容。比如下面这个网站，它的 location.hash 的值为 '#search'：

```bash
https://www.word.com#search
```

hash 路由模式的实现主要是基于下面几个特性：

- URL 中 hash 值只是客户端的一种状态，也就是说当向服务器端发出请求时，hash 部分不会被发送；
- hash 值的改变，都会在浏览器的访问历史中增加一个记录。因此我们能通过浏览器的回退、前进按钮控制hash 的切换；
- 可以通过 a 标签，并设置 href 属性，当用户点击这个标签后，URL 的 hash 值会发生改变；或者使用 JavaScript 来对 loaction.hash 进行赋值，改变 URL 的 hash 值；
- 我们可以使用 hashchange 事件来监听 hash 值的变化，从而对页面进行跳转（渲染）。

#### （2）history 模式的实现原理

HTML5 提供了 History API 来实现 URL 的变化。其中做最主要的 API 有以下两个：history.pushState() 和 history.repalceState()。这两个 API 可以在不进行刷新的情况下，操作浏览器的历史纪录。唯一不同的是，前者是新增一个历史记录，后者是直接替换当前的历史记录，如下所示：

```dart
window.history.pushState(null, null, path);
```

history 路由模式的实现主要基于存在下面几个特性：

- pushState 和 repalceState 两个 API 来操作实现 URL 的变化 ；
- 我们可以使用 popstate 事件来监听 url 的变化，从而对页面进行跳转（渲染）；
- history.pushState() 或 history.replaceState() 不会触发 popstate 事件，这时我们需要手动触发页面跳转（渲染）。



### 什么是 MVVM？

Model–View–ViewModel （MVVM） 是一个软件架构设计模式，由微软 WPF 和 Silverlight 的架构师 Ken Cooper 和 Ted Peters 开发，是一种简化用户界面的事件驱动编程方式。由 John Gossman（同样也是 WPF 和 Silverlight 的架构师）于2005年在他的博客上发表

MVVM 源自于经典的 Model–View–Controller（MVC）模式 ，MVVM 的出现促进了前端开发与后端业务逻辑的分离，极大地提高了前端开发效率，MVVM 的核心是 ViewModel 层，它就像是一个中转站（value converter），负责转换 Model 中的数据对象来让数据变得更容易管理和使用，该层向上与视图层进行双向数据绑定，向下与 Model 层通过接口请求进行数据交互，起呈上启下作用。如下图所示：

![img](https:////upload-images.jianshu.io/upload_images/12842279-5af933c42fa81a9e?imageMogr2/auto-orient/strip|imageView2/2/w/640/format/webp)

#### （1）View 层

View 是视图层，也就是用户界面。前端主要由 HTML 和 CSS 来构建 。

#### （2）Model 层

Model 是指数据模型，泛指后端进行的各种业务逻辑处理和数据操控，对于前端来说就是后端提供的 api 接口。

#### （3）ViewModel 层

ViewModel 是由前端开发人员组织生成和维护的视图数据层。在这一层，前端开发者对从后端获取的 Model 数据进行转换处理，做二次封装，以生成符合 View 层使用预期的视图数据模型。

需要注意的是 ViewModel 所封装出来的数据模型包括视图的状态和行为两部分，而 Model 层的数据模型是只包含状态的，比如页面的这一块展示什么，而页面加载进来时发生什么，点击这一块发生什么，这一块滚动时发生什么这些都属于视图行为（交互），视图状态和行为都封装在了 ViewModel 里。这样的封装使得 ViewModel 可以完整地去描述 View 层。

MVVM 框架实现了双向绑定，这样 ViewModel 的内容会实时展现在 View 层，前端开发者再也不必低效又麻烦地通过操纵 DOM 去更新视图，MVVM 框架已经把最脏最累的一块做好了，我们开发者只需要处理和维护 ViewModel，更新数据视图就会自动得到相应更新。

这样 View 层展现的不是 Model 层的数据，而是 ViewModel 的数据，由 ViewModel 负责与 Model 层交互，这就完全解耦了 View 层和 Model 层，这个解耦是至关重要的，它是前后端分离方案实施的重要一环。

我们以下通过一个 Vue 实例来说明 MVVM 的具体实现，有 Vue 开发经验的同学应该一目了然：

（1）View 层

```objectivec
<div id="app">
```

（2）ViewModel 层

```csharp
var app = new Vue(\\{
```

（3） Model 层

```undefined
\\{
```



### Vue 是如何实现数据双向绑定的？

Vue 数据双向绑定主要是指：数据变化更新视图，视图变化更新数据，如下图所示：

![img](https:////upload-images.jianshu.io/upload_images/12842279-965e38fb3e4c6774?imageMogr2/auto-orient/strip|imageView2/2/w/492/format/webp)

即：

- 输入框内容变化时，Data 中的数据同步变化。即 View => Data 的变化。
- Data 中的数据变化时，文本节点的内容同步变化。即 Data => View 的变化。

其中，View 变化更新 Data ，可以通过事件监听的方式来实现，所以 Vue 的数据双向绑定的工作主要是如何根据 Data 变化更新 View。

Vue 主要通过以下 4 个步骤来实现数据双向绑定的：

实现一个监听器 Observer：对数据对象进行遍历，包括子属性对象的属性，利用 Object.defineProperty() 对属性都加上 setter 和 getter。这样的话，给这个对象的某个值赋值，就会触发 setter，那么就能监听到了数据变化。

实现一个解析器 Compile：解析 Vue 模板指令，将模板中的变量都替换成数据，然后初始化渲染页面视图，并将每个指令对应的节点绑定更新函数，添加监听数据的订阅者，一旦数据有变动，收到通知，调用更新函数进行数据更新。

实现一个订阅者 Watcher：Watcher 订阅者是 Observer 和 Compile 之间通信的桥梁 ，主要的任务是订阅 Observer 中的属性值变化的消息，当收到属性值变化的消息时，触发解析器 Compile 中对应的更新函数。

实现一个订阅器 Dep：订阅器采用 发布-订阅 设计模式，用来收集订阅者 Watcher，对监听器 Observer 和 订阅者 Watcher 进行统一管理。

以上四个步骤的流程图表示如下，如果有同学理解不大清晰的，可以查看作者专门介绍数据双向绑定的文章《0 到 1 掌握：Vue 核心之数据双向绑定》，有进行详细的讲解、以及代码 demo 示例。

![img](https:////upload-images.jianshu.io/upload_images/12842279-fd64627956b167e5?imageMogr2/auto-orient/strip|imageView2/2/w/640/format/webp)



### Vue 框架怎么实现对象和数组的监听？

如果被问到 Vue 怎么实现数据双向绑定，大家肯定都会回答 通过 Object.defineProperty() 对数据进行劫持，但是 Object.defineProperty() 只能对属性进行数据劫持，不能对整个对象进行劫持，同理无法对数组进行劫持，但是我们在使用 Vue 框架中都知道，Vue 能检测到对象和数组（部分方法的操作）的变化，那它是怎么实现的呢？我们查看相关代码如下：

```undefined
 /**
```

通过以上 Vue 源码部分查看，我们就能知道 Vue 框架是通过遍历数组 和递归遍历对象，从而达到利用 Object.defineProperty() 也能对对象和数组（部分方法的操作）进行监听。



### Proxy 与 Object.defineProperty 优劣对比

Proxy 的优势如下:

- Proxy 可以直接监听对象而非属性；
- Proxy 可以直接监听数组的变化；
- Proxy 有多达 13 种拦截方法,不限于 apply、ownKeys、deleteProperty、has 等等是 Object.defineProperty 不具备的；
- Proxy 返回的是一个新对象,我们可以只操作新的对象达到目的,而 Object.defineProperty 只能遍历对象属性直接修改；
- Proxy 作为新标准将受到浏览器厂商重点持续的性能优化，也就是传说中的新标准的性能红利；

Object.defineProperty 的优势如下:

- 兼容性好，支持 IE9，而 Proxy 的存在浏览器兼容性问题,而且无法用 polyfill 磨平，因此 Vue 的作者才声明需要等到下个大版本( 3.0 )才能用 Proxy 重写。



### vue中this.$set的用法

当你发现你给对象加了一个属性，在控制台能打印出来，但是却没有更新到视图上时，也许这个时候就需要用到this.$set（）这个方法了，简单来说this.$set的功能就是解决这个问题的啦。

官方解释：向响应式对象中添加一个属性，并确保这个新属性同样是响应式的，且触发视图更新。它必须用于向响应式对象上添加新属性，因为 Vue 无法探测普通的新增属性 (比如 this.myObject.newProperty = 'hi')

调用方法：this.$set( target, key, value )

🌹 target：要更改的数据源(可以是对象或者数组)

🌹 key：要更改的具体数据

🌹 value ：重新赋的值

```
// 不能动态修改值
item2.price = 0
this.arr[2] = 0
this.$set(item, 'price', 0)	// 对象给item设置新属性price，值为0，可以动态修改
this.$set(this.arr, 2, 0) // 数组给第三个元素赋值为0
```



### vue更新数组时触发视图更新的方法

1.Vue.set 可以设置对象或数组的值，通过 key 或数组索引，可以触发视图更新

```
数组修改
Vue.set(array, indexOfItem, newValue)
this.array.$set(indexOfItem, newValue)

对象修改
Vue.set(obj, keyOfItem, newValue)
this.obj.$set(keyOfItem, newValue)
```

2.Vue.delete 删除对象或数组中元素，通过 key 或数组索引，可以触发视图更新

```
数组修改
Vue.delete(array, indexOfItem)
this.array.$delete(indexOfItem)

对象修改
Vue.delete(obj, keyOfItem)
this.obj.$delete(keyOfItem)
```

3.数组对象直接修改属性，可以触发视图更新

```
this.array[0].show = true;
this.array.forEach(function(item)\\{
    item.show = true;
\\});
```

4.splice 方法修改数组，可以触发视图更新

```
this.array.splice(indexOfItem, 1, newElement)
```

5.数组整体修改，可以触发视图更新

```
var tempArray = this.array;
tempArray[0].show = true;
this.array = tempArray;
```

6.用 Object.assign 或 lodash.assign 可以为对象添加响应式属性，可以触发视图更新

```
//Object.assign的单层的覆盖前面的属性，不会递归的合并属性
this.obj = Object.assign(\\{\\},this.obj,\\{a:1, b:2\\})

//assign与Object.assign一样
this.obj = _.assign(\\{\\},this.obj,\\{a:1, b:2\\})

//merge会递归的合并属性
this.obj = _.merge(\\{\\},this.obj,\\{a:1, b:2\\})
```

7.Vue 提供了如下的数组的变异方法，可以触发视图更新

```
push()
pop()
shift()
unshift()
splice()
sort()
reverse()
```



### 直接给一个数组项赋值，Vue 能检测到变化吗？

由于 JavaScript 的限制，Vue 不能检测到以下数组的变动：

- 当你利用索引直接设置一个数组项时，例如：`vm.items[indexOfItem] = newValue`
- 当你修改数组的长度时，例如：`vm.items.length = newLength`

为了解决第一个问题，Vue 提供了以下操作方法：

```
// Vue.set
Vue.set(vm.items, indexOfItem, newValue)
// vm.$set，Vue.set的一个别名
vm.$set(vm.items, indexOfItem, newValue)
// Array.prototype.splice
vm.items.splice(indexOfItem, 1, newValue)
```

为了解决第二个问题，Vue 提供了以下操作方法：

```
// Array.prototype.splice
vm.items.splice(newLength)
```



### vue更新数组时触发视图更新的方法

```js
Vue.set    ==========Vue.set(target,key,value)这个方法主要是用于避开vue不能检测属性被添加的限制
Vue.set(array, indexOfItem, newValue)//indexOfItem指的索引
this.array.$set(indexOfItem, newValue)
Vue.set(obj, keyOfItem, newValue)
this.obj.$set(keyOfItem, newValue)
Vue.delete   这个方法主要用于避开vue不能检测到属性被删除；

Vue.delete(array, indexOfItem)
this.array.$delete(indexOfItem)
Vue.delete(obj, keyOfItem)
this.obj.$delete(keyOfItem)
```



### vue的数据是响应式的，请问什么时候是非响应式的并如何解决

#### 数组数据：

问题1：通过改变长度，利用索引直接设置跟项

解决：Vue.set(数组对象, key, value)            |         vm|this.$set(数组对象, key, value)

问题2：对数组使用了非变异 (non-mutating method) 方法（返回的了新数组）

解决：对象合并

#### 对象数据变化：

问题：问题：data:\\{a:1\\}；a 数据是响应式的；vm.b='qq'; b 属性不是响应式的

解决：Vue.set(对象, key, value)              |              vm|this.$set(对象, key, value)

总结：数据一开始就应该出现在data里，数组里面永远不要放置简单性数据



### vm.$set(obj, key, val) 做了什么？

由于 Vue 无法探测对象新增属性或者通过索引为数组新增一个元素，所以这才有了 vm.set ， 它 是 Vue.set 的 别 名 。 vm.set，它是 Vue.set 的别名。 vm.set，它是Vue.set的别名。vm.set 用于向响应式对象添加一个新的 property，并确保这个新的 property 同样是响应式的，并触发视图更新。

为对象添加一个新的响应式数据：调用 defineReactive 方法为对象增加响应式数据，然后执行 dep.notify 进行依赖通知，更新视图
为数组添加一个新的响应式数据：通过 splice 方法实现



### Vue 怎么用 vm.$set() 解决对象新增属性不能响应的问题 ？

受现代 JavaScript 的限制 ，Vue 无法检测到对象属性的添加或删除。由于 Vue 会在初始化实例时对属性执行 getter/setter 转化，所以属性必须在 data 对象上存在才能让 Vue 将它转换为响应式的。

但是 Vue 提供了`Vue.set (object, propertyName, value) / vm.$set (object, propertyName, value)` 来实现为对象添加响应式属性，那框架本身是如何实现的呢？

我们查看对应的 Vue 源码：`vue/src/core/instance/index.js`

```
export function set (target: Array<any> | Object, key: any, val: any): any \\{
  // target 为数组  
  if (Array.isArray(target) && isValidArrayIndex(key)) \\{
    // 修改数组的长度, 避免索引>数组长度导致splcie()执行有误
    target.length = Math.max(target.length, key)
    // 利用数组的splice变异方法触发响应式  
    target.splice(key, 1, val)
    return val
  \\}
  // key 已经存在，直接修改属性值  
  if (key in target && !(key in Object.prototype)) \\{
    target[key] = val
    return val
  \\}
  const ob = (target: any).__ob__
  // target 本身就不是响应式数据, 直接赋值
  if (!ob) \\{
    target[key] = val
    return val
  \\}
  // 对属性进行响应式处理
  defineReactive(ob.value, key, val)
  ob.dep.notify()
  return val
\\}
```

我们阅读以上源码可知，vm.$set 的实现原理是：

- 如果目标是数组，直接使用数组的 splice 方法触发相应式；
- 如果目标是对象，会先判读属性是否存在、对象是否是响应式，最终如果要对属性进行响应式处理，则是通过调用   defineReactive 方法进行响应式处理（ defineReactive 方法就是  Vue 在初始化对象时，给对象属性采用 Object.defineProperty 动态添加 getter 和 setter 的功能所调用的方法）



### 虚拟 DOM 的优缺点？

优点：

- 保证性能下限： 框架的虚拟 DOM 需要适配任何上层 API 可能产生的操作，它的一些 DOM 操作的实现必须是普适的，所以它的性能并不是最优的；但是比起粗暴的 DOM 操作性能要好很多，因此框架的虚拟 DOM 至少可以保证在你不需要手动优化的情况下，依然可以提供还不错的性能，即保证性能的下限；
- 无需手动操作 DOM： 我们不再需要手动去操作 DOM，只需要写好 View-Model 的代码逻辑，框架会根据虚拟 DOM 和 数据双向绑定，帮我们以可预期的方式更新视图，极大提高我们的开发效率；
- 跨平台： 虚拟 DOM 本质上是 JavaScript 对象,而 DOM 与平台强相关，相比之下虚拟 DOM 可以进行更方便地跨平台操作，例如服务器渲染、weex 开发等等。

缺点:

- 无法进行极致优化： 虽然虚拟 DOM + 合理的优化，足以应对绝大部分应用的性能需求，但在一些性能要求极高的应用中虚拟 DOM 无法进行针对性的极致优化。



### 虚拟 DOM 实现原理？

虚拟 DOM 的实现原理主要包括以下 3 部分：

- 用 JavaScript 对象模拟真实 DOM 树，对真实 DOM 进行抽象；
- diff 算法 — 比较两棵虚拟 DOM 树的差异；
- pach 算法 — 将两个虚拟 DOM 对象的差异应用到真正的 DOM 树。

如果对以上 3 个部分还不是很了解的同学，可以查看本文作者写的另一篇详解虚拟 DOM 的文章《深入剖析：Vue核心之虚拟DOM》



### 你有对 Vue 项目进行哪些优化？

如果没有对 Vue 项目没有进行过优化总结的同学，可以参考本文作者的另一篇文章《 Vue 项目性能优化 — 实践指南 》，文章主要介绍从 3 个大方面，22 个小方面详细讲解如何进行 Vue 项目的优化。

#### （1）代码层面的优化

- v-if 和 v-show 区分使用场景
- computed 和 watch 区分使用场景
- v-for 遍历必须为 item 添加 key，且避免同时使用 v-if
- 长列表性能优化
- 事件的销毁
- 图片资源懒加载
- 路由懒加载
- 第三方插件的按需引入
- 优化无限列表性能
- 服务端渲染 SSR or 预渲染

#### （2）Webpack 层面的优化

- Webpack 对图片进行压缩
- 减少 ES6 转为 ES5 的冗余代码
- 提取公共代码
- 模板预编译
- 提取组件的 CSS
- 优化 SourceMap
- 构建结果输出分析
- Vue 项目的编译优化

#### （3）基础的 Web 技术的优化

- 开启 gzip 压缩
- 浏览器缓存
- CDN 的使用
- 使用 Chrome Performance 查找性能瓶颈



### vue路由组件动态引入

在Vue中，可以使用动态组件和Vue Router结合来实现路由组件的动态引入。以下是一个简单的例子：

安装Vue Router：

```
npm install vue-router
```

设置Vue Router，并使用动态导入来懒加载组件：

```
// router.js
import Vue from 'vue';
import Router from 'vue-router';

Vue.use(Router);

function loadView(view) \\{
  return () => import(`@/views/$\\{view\\}.vue`);
\\}

const router = new Router(\\{
  mode: 'history',
  routes: [
    \\{
      path: '/',
      name: 'home',
      component: loadView('Home') // 动态引入Home组件
    \\},
    \\{
      path: '/about',
      name: 'about',
      component: loadView('About') // 动态引入About组件
    \\},
    // 更多路由...
  ]
\\});

export default router;
```

在Vue实例中使用router：

```
// main.js
import Vue from 'vue';
import App from './App.vue';
import router from './router';

new Vue(\\{
  router,
  render: h => h(App)
\\}).$mount('#app');
```

在上述代码中，loadView函数负责根据视图名称动态创建组件加载函数。当Vue Router匹配到相应路由时，会调用这个加载函数来懒加载对应的组件文件。这样可以实现按需加载，提高应用的初始化速度和性能。



### 对于即将到来的 vue3.0 特性你有什么了解的吗？

Vue 3.0 正走在发布的路上，Vue 3.0 的目标是让 Vue 核心变得更小、更快、更强大，因此 Vue 3.0 增加以下这些新特性：

#### （1）监测机制的改变

3.0 将带来基于代理 Proxy 的 observer 实现，提供全语言覆盖的反应性跟踪。这消除了 Vue 2 当中基于 Object.defineProperty 的实现所存在的很多限制：

- 只能监测属性，不能监测对象
- 检测属性的添加和删除；
- 检测数组索引和长度的变更；
- 支持 Map、Set、WeakMap 和 WeakSet。

新的 observer 还提供了以下特性：

- 用于创建 observable 的公开 API。这为中小规模场景提供了简单轻量级的跨组件状态管理解决方案。
- 默认采用惰性观察。在 2.x 中，不管反应式数据有多大，都会在启动时被观察到。如果你的数据集很大，这可能会在应用启动时带来明显的开销。在 3.x 中，只观察用于渲染应用程序最初可见部分的数据。
- 更精确的变更通知。在 2.x 中，通过 Vue.set 强制添加新属性将导致依赖于该对象的 watcher 收到变更通知。在 3.x 中，只有依赖于特定属性的 watcher 才会收到通知。
- 不可变的 observable：我们可以创建值的“不可变”版本（即使是嵌套属性），除非系统在内部暂时将其“解禁”。这个机制可用于冻结 prop 传递或 Vuex 状态树以外的变化。
- 更好的调试功能：我们可以使用新的 renderTracked 和 renderTriggered 钩子精确地跟踪组件在什么时候以及为什么重新渲染。

#### （2）模板

模板方面没有大的变更，只改了作用域插槽，2.x 的机制导致作用域插槽变了，父组件会重新渲染，而 3.0 把作用域插槽改成了函数的方式，这样只会影响子组件的重新渲染，提升了渲染的性能。

同时，对于 render 函数的方面，vue3.0 也会进行一系列更改来方便习惯直接使用 api 来生成 vdom 。

#### （3）对象式的组件声明方式

vue2.x 中的组件是通过声明的方式传入一系列 option，和 TypeScript 的结合需要通过一些装饰器的方式来做，虽然能实现功能，但是比较麻烦。

3.0 修改了组件的声明方式，改成了类式的写法，这样使得和 TypeScript 的结合变得很容易。

此外，vue 的源码也改用了 TypeScript 来写。其实当代码的功能复杂之后，必须有一个静态类型系统来做一些辅助管理。

现在 vue3.0 也全面改用 TypeScript 来重写了，更是使得对外暴露的 api 更容易结合 TypeScript。静态类型系统对于复杂代码的维护确实很有必要。

#### （4）其它方面的更改

vue3.0 的改变是全面的，上面只涉及到主要的 3 个方面，还有一些其他的更改：

- 支持自定义渲染器，从而使得 weex 可以通过自定义渲染器的方式来扩展，而不是直接 fork 源码来改的方式。
- 支持 Fragment（多个根节点）和 Protal（在 dom 其他部分渲染组建内容）组件，针对一些特殊的场景做了处理。
- 基于 treeshaking 优化，提供了更多的内置功能。



## 说说你使用 Vue 框架踩过最大的坑是什么？怎么解决的？

本题为开放题目，Vue框架部分我们会涉及一些高频且有一定探讨价值的面试题,我们不会涉及一些非常初级的在官方文档就能查看的纯记忆性质的面试题,比如:

- vue常用的修饰符?
- vue-cli 工程常用的 npm 命令有哪些？
- vue中 keep-alive 组件的作用?

首先,上述类型的面试题在文档中可查,没有比官方文档更权威的答案了,其次这种问题没有太大价值,除了考察候选人的记忆力,最后,这种面试题只要用过vue的都知道,没有必要占用我们的篇幅.

我们的问题并不多,但是难度可能会高一些,如果你真的搞懂了这些问题,在绝大多数情况下会有举一反三的效果,可以说基本能拿下Vue相关的所有重要知识点了.



### MVVM是什么?

MVVM 模式，顾名思义即 Model-View-ViewModel 模式。它萌芽于2005年微软推出的基于 Windows 的用户界面框架 WPF ，前端最早的 MVVM 框架 knockout 在2010年发布。

Model 层: 对应数据层的域模型，它主要做域模型的同步。通过 Ajax/fetch 等 API 完成客户端和服务端业务 Model 的同步。在层间关系里，它主要用于抽象出 ViewModel 中视图的 Model。

View 层:作为视图模板存在，在 MVVM 里，整个 View 是一个动态模板。除了定义结构、布局外，它展示的是 ViewModel 层的数据和状态。View 层不负责处理状态，View 层做的是 数据绑定的声明、 指令的声明、 事件绑定的声明。

ViewModel 层:把 View 需要的层数据暴露，并对 View 层的 数据绑定声明、 指令声明、 事件绑定声明 负责，也就是处理 View 层的具体业务逻辑。ViewModel 底层会做好绑定属性的监听。当 ViewModel 中数据变化，View 层会得到更新；而当 View 中声明了数据的双向绑定（通常是表单元素），框架也会监听 View 层（表单）值的变化。一旦值变化，View 层绑定的 ViewModel 中的数据也会得到自动更新。



### MVVM的优缺点?

优点:

1. 分离视图（View）和模型（Model）,降低代码耦合，提高视图或者逻辑的重用性: 比如视图（View）可以独立于Model变化和修改，一个ViewModel可以绑定不同的"View"上，当View变化的时候Model不可以不变，当Model变化的时候View也可以不变。你可以把一些视图逻辑放在一个ViewModel里面，让很多view重用这段视图逻辑
2. 提高可测试性: ViewModel的存在可以帮助开发者更好地编写测试代码
3. 自动更新dom: 利用双向绑定,数据更新后视图自动更新,让开发者从繁琐的手动dom中解放

缺点:

1. Bug很难被调试: 因为使用双向绑定的模式，当你看到界面异常了，有可能是你View的代码有Bug，也可能是Model的代码有问题。数据绑定使得一个位置的Bug被快速传递到别的位置，要定位原始出问题的地方就变得不那么容易了。另外，数据绑定的声明是指令式地写在View的模版当中的，这些内容是没办法去打断点debug的
2. 一个大的模块中model也会很大，虽然使用方便了也很容易保证了数据的一致性，当时长期持有，不释放内存就造成了花费更多的内存
3. 对于大型的图形应用程序，视图状态较多，ViewModel的构建和维护的成本都会比较高



### 异步请求适合在哪个生命周期调用？

官方实例的异步请求是在mounted生命周期中调用的，而实际上也可以在created生命周期中调用。



### Vue组件如何通信？

Vue组件通信的方法如下:

- `props` `$emit+v-on`: 通过props将数据自上而下传递，而通过`$emit`和`v-on`来向上传递信息。
- EventBus: 通过EventBus进行信息的发布与订阅
- vuex: 是全局数据管理库，可以通过vuex管理全局的数据流
- `$attrs` `$listeners`: Vue2.4中加入的`$attrs/$listeners`可以进行跨级的组件通信
- `provide/inject`：以允许一个祖先组件向其所有子孙后代注入一个依赖，不论组件层次有多深，并在起上下游关系成立的时间里始终生效，这成为了跨组件通信的基础

还有一些用solt插槽或者ref实例进行通信的，使用场景过于有限就不赘述了。



### Vue是如何实现双向绑定的?

利用`Object.defineProperty`劫持对象的访问器,在属性值发生变化时我们可以获取变化,然后根据变化进行后续响应,在vue3.0中通过Proxy代理对象进行类似的操作。

```js
// 这是将要被劫持的对象
const data = \\{
    name: '',
\\};

function say(name) \\{
    if (name === '古天乐') \\{
    console.log('给大家推荐一款超好玩的游戏');
    \\} else if (name === '渣渣辉') \\{
    console.log('戏我演过很多,可游戏我只玩贪玩懒月');
    \\} else \\{
    console.log('来做我的兄弟');
    \\}
\\}

// 遍历对象,对其属性值进行劫持
Object.keys(data).forEach(function(key) \\{
    Object.defineProperty(data, key, \\{
    enumerable: true,
    configurable: true,
    get: function() \\{
        console.log('get');
    \\},
    set: function(newVal) \\{
        // 当属性值发生变化时我们可以进行额外操作
        console.log(`大家好,我系$\\{newVal\\}`);
        say(newVal);
    \\},
    \\});
\\});

data.name = '渣渣辉';
//大家好,我系渣渣辉
//戏我演过很多,可游戏我只玩贪玩懒月
```

> 详细实现见[Proxy比defineproperty优劣对比?](http://mp.weixin.qq.com/s?__biz=MzI3NjM1OTI3Mw==&mid=2247483695&idx=1&sn=8f4d74b58f4102eced8089bcaac4c443&chksm=eb77f029dc00793f502d4a39819e488d560e6bf7d268f3e987a03d43d71a07a2edab59d8d78f&scene=21#wechat_redirect)



### Proxy与Object.defineProperty的优劣对比?

Proxy的优势如下:

- Proxy可以直接监听对象而非属性
- Proxy可以直接监听数组的变化
- Proxy有多达13种拦截方法,不限于apply、ownKeys、deleteProperty、has等等是`Object.defineProperty`不具备的
- Proxy返回的是一个新对象,我们可以只操作新的对象达到目的,而`Object.defineProperty`只能遍历对象属性直接修改
- Proxy作为新标准将受到浏览器厂商重点持续的性能优化，也就是传说中的新标准的性能红利

Object.defineProperty的优势如下:

- 兼容性好,支持IE9

> 详细实现见[Proxy比defineproperty优劣对比](http://mp.weixin.qq.com/s?__biz=MzI3NjM1OTI3Mw==&mid=2247483695&idx=1&sn=8f4d74b58f4102eced8089bcaac4c443&chksm=eb77f029dc00793f502d4a39819e488d560e6bf7d268f3e987a03d43d71a07a2edab59d8d78f&scene=21#wechat_redirect)?



### 你是如何理解Vue的响应式系统的?

响应式系统简述:

- 任何一个 Vue Component 都有一个与之对应的 Watcher 实例。
- Vue 的 data 上的属性会被添加 getter 和 setter 属性。
- 当 Vue Component render 函数被执行的时候, data 上会被 触碰(touch), 即被读, getter 方法会被调用, 此时 Vue 会去记录此 Vue component 所依赖的所有 data。(这一过程被称为依赖收集)
- data 被改动时（主要是用户操作）, 即被写, setter 方法会被调用, 此时 Vue 会去通知所有依赖于此 data 的组件去调用他们的 render 函数进行更新。



### 虚拟DOM的优劣如何?

优点:

- 保证性能下限: 虚拟DOM可以经过diff找出最小差异,然后批量进行patch,这种操作虽然比不上手动优化,但是比起粗暴的DOM操作性能要好很多,因此虚拟DOM可以保证性能下限
- 无需手动操作DOM: 虚拟DOM的diff和patch都是在一次更新中自动进行的,我们无需手动操作DOM,极大提高开发效率
- 跨平台: 虚拟DOM本质上是JavaScript对象,而DOM与平台强相关,相比之下虚拟DOM可以进行更方便地跨平台操作,例如服务器渲染、移动端开发等等

缺点:

- 无法进行极致优化: 在一些性能要求极高的应用中虚拟DOM无法进行针对性的极致优化,比如VScode采用直接手动操作DOM的方式进行极端的性能优化



### 虚拟DOM实现原理?

- 虚拟DOM本质上是JavaScript对象,是对真实DOM的抽象
- 状态变更时，记录新树和旧树的差异
- 最后把差异更新到真正的dom中

> 详细实现见[虚拟DOM原理](http://mp.weixin.qq.com/s?__biz=MzI3NjM1OTI3Mw==&mid=2247483738&idx=1&sn=3f38e3ad9dddfa9740c9f3f4eb8b412c&chksm=eb77f05cdc00794a8b87f46b5bef4d854227b800c0a3b71178f8cc1624ecafa049c8339981ae&scene=21#wechat_redirect)?



### 既然Vue通过数据劫持可以精准探测数据变化,为什么还需要虚拟DOM进行diff检测差异?

考点: Vue的变化侦测原理

前置知识: 依赖收集、虚拟DOM、响应式系统

现代前端框架有两种方式侦测变化,一种是pull一种是push

pull: 其代表为React,我们可以回忆一下React是如何侦测到变化的,我们通常会用`setState`API显式更新,然后React会进行一层层的Virtual Dom Diff操作找出差异,然后Patch到DOM上,React从一开始就不知道到底是哪发生了变化,只是知道「有变化了」,然后再进行比较暴力的Diff操作查找「哪发生变化了」，另外一个代表就是Angular的脏检查操作。

push: Vue的响应式系统则是push的代表,当Vue程序初始化的时候就会对数据data进行依赖的收集,一但数据发生变化,响应式系统就会立刻得知,因此Vue是一开始就知道是「在哪发生变化了」,但是这又会产生一个问题,如果你熟悉Vue的响应式系统就知道,通常一个绑定一个数据就需要一个Watcher,一但我们的绑定细粒度过高就会产生大量的Watcher,这会带来内存以及依赖追踪的开销,而细粒度过低会无法精准侦测变化,因此Vue的设计是选择中等细粒度的方案,在组件级别进行push侦测的方式,也就是那套响应式系统,通常我们会第一时间侦测到发生变化的组件,然后在组件内部进行Virtual Dom Diff获取更加具体的差异,而Virtual Dom Diff则是pull操作,Vue是push+pull结合的方式进行变化侦测的.



### Vue为什么没有类似于React中shouldComponentUpdate的生命周期？

考点: Vue的变化侦测原理

前置知识: 依赖收集、虚拟DOM、响应式系统

根本原因是Vue与React的变化侦测方式有所不同

React是pull的方式侦测变化,当React知道发生变化后,会使用Virtual Dom Diff进行差异检测,但是很多组件实际上是肯定不会发生变化的,这个时候需要用shouldComponentUpdate进行手动操作来减少diff,从而提高程序整体的性能.

Vue是pull+push的方式侦测变化的,在一开始就知道那个组件发生了变化,因此在push的阶段并不需要手动控制diff,而组件内部采用的diff方式实际上是可以引入类似于shouldComponentUpdate相关生命周期的,但是通常合理大小的组件不会有过量的diff,手动优化的价值有限,因此目前Vue并没有考虑引入shouldComponentUpdate这种手动优化的生命周期.



### Vue中的key到底有什么用？

`key`是为Vue中的vnode标记的唯一id,通过这个key,我们的diff操作可以更准确、更快速

diff算法的过程中,先会进行新旧节点的首尾交叉对比,当无法匹配的时候会用新节点的`key`与旧节点进行比对,然后超出差异.

> diff程可以概括为：oldCh和newCh各有两个头尾的变量StartIdx和EndIdx，它们的2个变量相互比较，一共有4种比较方式。如果4种比较都没匹配，如果设置了key，就会用key进行比较，在比较的过程中，变量会往中间靠，一旦StartIdx>EndIdx表明oldCh和newCh至少有一个已经遍历完了，就会结束比较,这四种比较方式就是首、尾、旧尾新头、旧头新尾.

- 准确: 如果不加`key`,那么vue会选择复用节点(Vue的就地更新策略),导致之前节点的状态被保留下来,会产生一系列的bug.
- 快速: key的唯一性可以被Map数据结构充分利用,相比于遍历查找的时间复杂度O(n),Map的时间复杂度仅仅为O(1).

在这个地方，模板不再是简单的声明式逻辑。你必须看一段时间才能意识到，这里是想要显示变量 message 的翻转字符串。当你想要在模板中多次引用此处的翻转字符串时，就会更加难以处理。

所以，对于任何复杂逻辑，你都应当使用计算属性。



### vue-cli提供了几种脚手架模板

六种

https://github.com/vuejs/vue-cli/tree/v2#vue-cli--



### computed、methods的区别

两种方式的最终结果确实是完全相同的。然而，不同的是计算属性是基于它们的依赖进行缓存的。只在相关依赖发生改变时它们才会重新求值。这就意味着只要值还没有发生改变，多次访问 定义的计算属性会立即返回之前的计算结果，而不必再次执行函数。

相比之下，每当触发重新渲染时，调用方法(methods)将总会再次执行函数。

我们为什么需要缓存？假设我们有一个性能开销比较大的计算属性 A，它需要遍历一个巨大的数组并做大量的计算。然后我们可能有其他的计算属性依赖于 A 。如果没有缓存，我们将不可避免的多次执行 A 的 getter！如果你不希望有缓存，请用方法来替代。



### 什么是自定义指令，有哪些钩子函数及自定义指令的使用场景

有的情况下，你仍然需要对普通 DOM 元素进行底层操作，这时候就会用到自定义指令。

一个指令定义对象可以提供如下几个钩子函数 (均为可选)：

bind：只调用一次，指令第一次绑定到元素时调用。在这里可以进行一次性的初始化设置。

inserted：被绑定元素插入父节点时调用 (仅保证父节点存在，但不一定已被插入文档中)。

update：所在组件的 VNode 更新时调用，但是可能发生在其子 VNode 更新之前。指令的值可能发生了改变，也可能没有。但是你可以通过比较更新前后的值来忽略不必要的模板更新 (详细的钩子函数参数见下)。

componentUpdated：指令所在组件的 VNode 及其子 VNode 全部更新后调用。

unbind：只调用一次，指令与元素解绑时调用。



### 父组件获取异步动态数据传递给子组件

在父组件中使用axios获取异步数据传给子组件，但是发现子组件在渲染的时候并没有数据，在created里面打印也是空的，结果发现一开始子组件绑定的数据是空的，在请求数据没有返回数据时，子组件就已经加载了，并且他绑定的值也是空的，问题找到了，怎么解决呢？

> 开始的时候让子组件隐藏,然后等数据返回的时候，让子组件显示
>
> 通过v-if，也就是判断数据是否为空，为空就不渲染，也能解决了
>
> 为不能读取的属性添加一个默认值，就可以很好的解决了



### vue-router实现原理

这里指的路由并不是指我们平时所说的硬件路由器，这里的路由就是SPA（单页应用）的路径管理器。 换句话说，vue-router就是WebApp的链接路径管理系统。

vue-router是Vue.js官方的路由插件，它和vue.js是深度集成的，适合用于构建单页面应用。

#### 那与传统的页面跳转有什么区别呢？

1.vue的单页面应用是基于路由和组件的，路由用于设定访问路径，并将路径和组件映射起来。

2.传统的页面应用，是用一些超链接来实现页面切换和跳转的。

在vue-router单页面应用中，则是路径之间的切换，也就是组件的切换。路由模块的本质 就是建立起url和页面之间的映射关系。

至于为啥不能用a标签，这是因为用Vue做的都是单页应用，就相当于只有一个主的index.html页面，所以你写的标签是不起作用的，必须使用vue-router来进行管理。

SPA(single page application):单一页面应用程序，有且只有一个完整的页面；当它在加载页面的时候，不会加载整个页面的内容，而只更新某个指定的容器中内容。

单页面应用(SPA)的核心之一是:

更新视图而不重新请求页面;

vue-router在实现单页面前端路由时，提供了三种方式：Hash模式、History模式、abstract模式，根据mode参数来决定采用哪一种方式。



### 路由模式

vue-router 提供了三种运行模式：

● hash: 使用 URL hash 值来作路由。默认模式。

● history: 依赖 HTML5 History API 和服务器配置。查看 HTML5 History 模式。

● abstract: 支持所有 JavaScript 运行环境，如 Node.js 服务器端。

#### Hash模式

vue-router 默认模式是 hash 模式 —— 使用 URL 的 hash 来模拟一个完整的 URL，当 URL 改变时，页面不会去重新加载。

hash（#）是URL 的锚点，代表的是网页中的一个位置，单单改变#后的部分（/#/…），浏览器只会加载相应位置的内容，不会重新加载网页，也就是说 #是用来指导浏览器动作的，对服务器端完全无用，HTTP请求中不包括#；同时每一次改变#后的部分，都会在浏览器的访问历史中增加一个记录，使用”后退”按钮，就可以回到上一个位置；所以说Hash模式通过锚点值的改变，根据不同的值，渲染指定DOM位置的不同数据。

JavaScript实现SPA路由hash模式详解

#### History模式

HTML5 History API提供了一种功能，能让开发人员在不刷新整个页面的情况下修改站点的URL，就是利用 history.pushState API 来完成 URL 跳转而无须重新加载页面；

由于hash模式会在url中自带#，如果不想要很丑的 hash，我们可以用路由的 history 模式，只需要在配置路由规则时，加入"mode: ‘history’",这种模式充分利用 history.pushState API 来完成 URL 跳转而无须重新加载页面。

[//main.js文件中](https://main.xn--js-ry2cx4aj93f/)

```
const router = new VueRouter(\\{
	mode: ‘history’,
	routes: […]
\\})
```

当使用 history 模式时，URL 就像正常的 url，例如 [yoursite.com/user/id，比较好…](http://yoursite.com/user/id，比较好…) 不过这种模式有点问题，还需要后台配置支持。你要在服务端增加一个覆盖所有情况的候选资源：如果 URL 匹配不到任何静态资源，则应该返回同一个 index.html 页面，这个页面就是你 app 依赖的页面，如果不这么做，直接访问页面空白



### 配置Apache

第一步：新建：.htaccess文件放在服务器根目录下 （命令type null>.htaccess）

```
<IfModule mod_rewrite.c>
	RewriteEngine On
	RewriteBase /
	RewriteRule ^index.html$ - [L]
	RewriteCond \\%\\{REQUEST_FILENAME\\} !-f
	RewriteCond \\%\\{REQUEST_FILENAME\\} !-d
	RewriteRule . /index.html [L]
</IfModule>
```

除了 mod_rewrite，你也可以使用 FallbackResource。

第二步： src/router/index.js

mode: ‘history’,

base: ‘/dist/’,

第三步：访问：地址进行测试

abstract模式

abstract模式是使用一个不依赖于浏览器的浏览历史虚拟管理后端。

根据平台差异可以看出，在 Weex 环境中只支持使用 abstract 模式。 不过，vue-router 自身会对环境做校验，如果发现没有浏览器的 API，vue-router 会自动强制进入 abstract 模式，所以 在使用 vue-router 时只要不写 mode 配置即可，默认会在浏览器环境中使用 hash 模式，在移动端原生环境中使用 abstract 模式。 （当然，你也可以明确指定在所有情况下都使用 abstract 模式）



### Vuex

用户在组件中发起动作，然后从API中拿数据，就会牵扯到异步操作，所以我们通过dispatch来提交一个action，在action里面发起ajax请求，拿到数据以后我们只需要通过commit提交mutations改变我的state状态就可以了，状态改变后视图就会改变因为Vuex是响应式的，这就是Vuex的运作流程机制



### vuex中如何异步修改数据

Action 类似于 mutation，不同在于：

Action 提交的是 mutation，而不是直接变更状态。

Action 可以包含任意异步操作。



![图片](https://mmbiz.qpic.cn/mmbiz_jpg/yphVQAwjncvicxKz1nicIOUh3ibEd24MWW1C0sVQ35DYJe5rPDTzZ8WeCPib3DibZ0uTc1Zfs9SGyDWoVu0cdgRNR8g/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

## 荣耀黄金

### 1. Vue的优点？Vue的缺点？

优点：渐进式，组件化，轻量级，虚拟dom，响应式，单页面路由，数据与视图分开

缺点：单页面不利于seo，不支持IE8以下，首屏加载时间长



### 2. 为什么说Vue是一个渐进式框架？

渐进式：通俗点讲就是，你想用啥你就用啥，咱也不强求你。你想用component就用，不用也行，你想用vuex就用，不用也可以

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/gMvNo9rxo40PPicD3fczxSYXZxxV3D2ORicibhZDdbZtm29mjvafm5unOBmia0s7iaSwolhVk6Ny4Aqe2Vbncoe4alw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)image.png



### 3. Vue跟React的异同点？

相同点：

- 1.都使用了虚拟dom
- 2.组件化开发
- 3.都是单向数据流(父子组件之间，不建议子修改父传下来的数据)
- 4.都支持服务端渲染

不同点：

- 1.React的JSX，Vue的template
- 2.数据变化，React手动(setState)，Vue自动(初始化已响应式处理，Object.defineProperty)
- 3.React单向绑定，Vue双向绑定
- 4.React的Redux，Vue的Vuex



### 4. MVVM是什么？和MVC有何区别呢？

MVC

- Model(模型)：负责从数据库中取数据
- View(视图)：负责展示数据的地方
- Controller(控制器)：用户交互的地方，例如点击事件等等
- 思想：Controller将Model的数据展示在View上

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/gMvNo9rxo40PPicD3fczxSYXZxxV3D2ORCeyFh1MjM6kv9Msc0jue4OfHGLlIUQhQXgbwJkngNsGlXO39AoIUog/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)image.png

MVVM

- VM：也就是View-Model，做了两件事达到了数据的双向绑定 一是将【模型】转化成【视图】，即将后端传递的数据转化成所看到的页面。实现的方式是：数据绑定。二是将【视图】转化成【模型】，即将所看到的页面转化成后端的数据。实现的方式是：DOM 事件监听。
- 思想：实现了 View 和 Model 的自动同步，也就是当 Model 的属性改变时，我们不用再自己手动操作 Dom 元素，来改变 View 的显示，而是改变属性后该属性对应 View 层显示会自动改变（对应Vue数据驱动的思想）

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/gMvNo9rxo40PPicD3fczxSYXZxxV3D2ORickpt9vKH462r7e4Qia14ar4icQPk9IfZcFO81GB8AUCsh8Z2icRUzLIIw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)image.png

区别

整体看来，MVVM 比 MVC 精简很多，不仅简化了业务与界面的依赖，还解决了数据频繁更新的问题，不用再用选择器操作 DOM 元素。因为在 MVVM 中，View 不知道 Model 的存在，Model 和 ViewModel 也观察不到 View，这种低耦合模式提高代码的可重用性

Vue是不是MVVM框架？

Vue是MVVM框架，但是不是严格符合MVVM，因为MVVM规定Model和View不能直接通信，而Vue的`ref`可以做到这点



### 5. Vue和JQuery的区别在哪？为什么放弃JQuery用Vue？

- 1.jQuery是直接操作DOM，Vue不直接操作DOM，Vue的数据与视图是分开的，Vue只需要操作数据即可
- 2.jQuery的操作DOM行为是频繁的，而Vue利用虚拟DOM的技术，大大提高了更新DOM时的性能
- 3.Vue中不倡导直接操作DOM，开发者只需要把大部分精力放在数据层面上
- 4.Vue集成的一些库，大大提高开发效率，比如Vuex，Router等



### 6. Vue的作者是谁？大声说出它的名字！！！

他的名字就是：鱿鱼西



## 永恒钻石

### 7. 为什么data是个函数并且返回一个对象呢？

`data`之所以只一个函数，是因为一个组件可能会多处调用，而每一次调用就会执行`data函数`并返回新的数据对象，这样，可以避免多处调用之间的`数据污染`。



### 8. 使用过哪些Vue的修饰符呢？

可以看我这篇文章**「百毒不侵」面试官最喜欢问的13种Vue修饰符**[1]

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/gMvNo9rxo40PPicD3fczxSYXZxxV3D2OR4V4kawxZ0rNQDgwzWh52f3btQ3sic8LA7DHayibYGicSUuNLo53gPxfCA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)截屏2021-07-11 下午9.56.53.png



### 9. 使用过哪些Vue的内部指令呢？

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/gMvNo9rxo40PPicD3fczxSYXZxxV3D2OReXR4ibmUb9kh4xNDO8cbmDiauq8cZ3mrbDd6VYk3bSblp3re6Xyd4jBA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)image.png



### 10. 组件之间的传值方式有哪些？

- 父组件传值给子组件，子组件使用`props`进行接收
- 子组件传值给父组件，子组件使用`$emit+事件`对父组件进行传值
- 组件中可以使用`$parent`和`$children`获取到父组件实例和子组件实例，进而获取数据
- 使用`$attrs`和`$listeners`，在对一些组件进行二次封装时可以方便传值，例如A->B->C
- 使用`$refs`获取组件实例，进而获取数据
- 使用`Vuex`进行状态管理
- 使用`eventBus`进行跨组件触发事件，进而传递数据
- 使用`provide`和`inject`，官方建议我们不要用这个，我在看`ElementUI`源码时发现大量使用
- 使用浏览器本地缓存，例如`localStorage`



### 11. 路由有哪些模式呢？又有什么不同呢？

- hash模式：通过`#号`后面的内容的更改，触发`hashchange`事件，实现路由切换
- history模式：通过`pushState`和`replaceState`切换url，触发`popstate`事件，实现路由切换，需要后端配合



### 12. 如何设置动态class，动态style？

- 动态class对象：`<div :class=\\{ 'is-active': true, 'red': isRed \\}></div>`
- 动态class数组：`<div :class=['is-active', isRed ? 'red' : '' ]></div>`
- 动态style对象：`<div :style=\\{ color: textColor, fontSize: '18px' \\}></div>`
- 动态style数组：`<div :style=[\\{ color: textColor, fontSize: '18px' \\}, \\{ fontWeight: '300' \\}]></div>`



### 13. v-if和v-show有何区别？

- 1.`v-if`是通过控制dom元素的删除和生成来实现显隐，每一次显隐都会使组件重新跑一遍生命周期，因为显隐决定了组件的生成和销毁
- 2.`v-show`是通过控制dom元素的css样式来实现显隐，不会销毁
- 3.频繁或者大数量显隐使用`v-show`，否则使用`v-if`



### 15. Vue的生命周期，讲一讲？

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/gMvNo9rxo40PPicD3fczxSYXZxxV3D2ORibreS1NicHBvGjhAwC5pkSMeaOVSrS1gl1DwbxxU5LQnhjc4z2AoD3BA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)



### 16. 为什么v-if和v-for不建议用在同一标签？

在Vue2中，`v-for`优先级是高于`v-if`的，咱们来看例子

```
<div v-for=item in [1, 2, 3, 4, 5, 6, 7] v-if=item !== 3>
    \\\{\\\{ite\\\}\\\}m}}
</div>
```

上面的写法是`v-for`和`v-if`同时存在，会先把7个元素都遍历出来，然后再一个个判断是否为3，并把3给隐藏掉，这样的坏处就是，渲染了无用的3节点，增加无用的dom操作，建议使用computed来解决这个问题：

```
<div v-for=item in list>
    \\\{\\\{ite\\\}\\\}m}}
</div>

computed() \\{
    list() \\{
        return [1, 2, 3, 4, 5, 6, 7].filter(item => item !== 3)
    \\}
  \\}
```



### 17. vuex的有哪些属性？用处是什么？

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/gMvNo9rxo40PPicD3fczxSYXZxxV3D2ORaSZPoXANK5XTKiaYUKGPDZPjFx61fg7DNxeXctJxT08ibz9IagIXTmrA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)image.png

- State：定义了应用状态的数据结构，可以在这里设置默认的初始状态。
- Getter：允许组件从 Store 中获取数据，mapGetters 辅助函数仅仅是将 store 中的 getter 映射到局部计算属性。
- Mutation：是唯一更改 store 中状态的方法，且必须是同步函数。
- Action：用于提交 mutation，而不是直接变更状态，可以包含任意异步操作。
- Module：允许将单一的 Store 拆分为多个 store 且同时保存在单一的状态树中。



## 至尊星耀

### 18. 不需要响应式的数据应该怎么处理？

在我们的Vue开发中，会有一些数据，从始至终都`未曾改变过`，这种`死数据`，既然`不改变`，那也就`不需要对他做响应式处理`了，不然只会做一些无用功消耗性能，比如一些写死的下拉框，写死的表格数据，这些数据量大的`死数据`，如果都进行响应式处理，那会消耗大量性能。

```
// 方法一：将数据定义在data之外
data () \\{
    this.list1 = \\{ xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx \\}
    this.list2 = \\{ xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx \\}
    this.list3 = \\{ xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx \\}
    this.list4 = \\{ xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx \\}
    this.list5 = \\{ xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx \\}
    return \\{\\}
 \\}
    
// 方法二：Object.freeze()
data () \\{
    return \\{
        list1: Object.freeze(\\{xxxxxxxxxxxxxxxxxxxxxxxx\\}),
        list2: Object.freeze(\\{xxxxxxxxxxxxxxxxxxxxxxxx\\}),
        list3: Object.freeze(\\{xxxxxxxxxxxxxxxxxxxxxxxx\\}),
        list4: Object.freeze(\\{xxxxxxxxxxxxxxxxxxxxxxxx\\}),
        list5: Object.freeze(\\{xxxxxxxxxxxxxxxxxxxxxxxx\\}),
    \\}
 \\}
```



### 19. watch有哪些属性，分别有什么用？

当我们监听一个基本数据类型时：

```
watch: \\{
    value () \\{
        // do something
    \\}
\\}
```

当我们监听一个引用数据类型时：

```
watch: \\{
    obj: \\{
       handler () \\{ // 执行回调
           // do something
       \\},
       deep: true, // 是否进行深度监听
       immediate: true // 是否初始执行handler函数
    \\}
\\}
```



### 20. 父子组件生命周期顺序

父beforeCreate -> 父created -> 父beforeMount -> 子beforeCreate -> 子created -> 子beforeMount -> 子mounted -> 父mounted



### 21. 对象新属性无法更新视图，删除属性无法更新视图，为什么？怎么办？

- 原因：`Object.defineProperty`没有对对象的新属性进行属性劫持
- 对象新属性无法更新视图：使用`Vue.$set(obj, key, value)`，组件中`this.$set(obj, key, value)`
- 删除属性无法更新视图：使用`Vue.$delete(obj, key)`，组件中`this.$delete(obj, key)`



### 22. 直接arr[index] = xxx无法更新视图怎么办？为什么？怎么办？

- 原因：Vue没有对数组进行`Object.defineProperty`的属性劫持，所以直接arr[index] = xxx是无法更新视图的
- 使用数组的splice方法，`arr.splice(index, 1, item)`
- 使用`Vue.$set(arr, index, value)`



### 24. 插槽的使用以及原理？

建议看我这篇文章**「Vue源码学习」你真的知道插槽Slot是怎么“插”的吗**[3]



### 25. 为什么不建议用index做key，为什么不建议用随机数做key？

举个例子：

```
<div v-for=(item, index) in list :key=index>\\\{\\\{item.nam\\\}\\\}e}}</div>

list: [
    \\{ name: '小明', id: '123' \\},
    \\{ name: '小红', id: '124' \\},
    \\{ name: '小花', id: '125' \\}
]

渲染为
<div key=0>小明</div>
<div key=1>小红</div>
<div key=2>小花</div>

现在我执行 list.unshift(\\{ name: '小林', id: '122' \\})

渲染为
<div key=0>小林</div>
<div key=1>小明</div>
<div key=2>小红</div>
<div key=3>小花</div>


新旧对比

<div key=0>小明</div>  <div key=0>小林</div>
<div key=1>小红</div>  <div key=1>小明</div>
<div key=2>小花</div>  <div key=2>小红</div>
                         <div key=3>小花</div>

可以看出，如果用index做key的话，其实是更新了原有的三项，并新增了小花，虽然达到了渲染目的，但是损耗性能

现在我们使用id来做key，渲染为

<div key=123>小明</div>
<div key=124>小红</div>
<div key=125>小花</div>

现在我执行 list.unshift(\\{ name: '小林', id: '122' \\})，渲染为

<div key=122>小林</div>
<div key=123>小明</div>
<div key=124>小红</div>
<div key=125>小花</div>

新旧对比

                           <div key=122>小林</div>
<div key=123>小明</div>  <div key=123>小明</div>
<div key=124>小红</div>  <div key=124>小红</div>
<div key=125>小花</div>  <div key=125>小花</div>

可以看出，原有的三项都不变，只是新增了小林这个人，这才是最理想的结果
```

用`index`和用`随机数`都是同理，`随机数`每次都在变，做不到专一性，很`渣男`，也很消耗性能，所以，拒绝`渣男`，选择`老实人`



### 26. 说说nextTick的用处？

我举个例子，在vue中：

```
this.name = '公众号：前端印象'
this.age = 18
this.gender = '男'
```

我们修改了三个变量，那问题来了，是每修改一次，DOM就更新一次吗？不是的，Vue采用的是`异步更新`的策略，通俗点说就是，`同一事件循环内`多次修改，会`统一`进行一次`视图更新`，这样才能节省性能嘛

看懂了上面，那你应该也看得懂下面的例子了吧：

```
<div ref=testDiv>\\\{\\\{nam\\\}\\\}e}}</div>

name: '小林'

this.name = '公众号：前端印象'
console.log(this.$refs.testDiv.innerHTML) // 这里是啥呢
```

答案是“小林”，前面说了，Vue是`异步更新`，所以数据一更新，视图却还没更新，所以拿到的还是上一次的旧视图数据，那么想要拿到最新视图数据怎么办呢？

```
this.name = '公众号：前端印象'
this.$nextTick(() => \\{
    console.log(this.$refs.testDiv.innerHTML) // 公众号：前端印象
\\})
```



### 27. Vue的SSR是什么？有什么好处？

- `SSR`就是服务端渲染
- 基于`nodejs serve`服务环境开发，所有`html`代码在服务端渲染
- 数据返回给前端，然后前端进行“激活”，即可成为浏览器识别的html代码
- `SSR`首次加载更快，有更好的用户体验，有更好的seo优化，因为爬虫能看到整个页面的内容，如果是vue项目，由于数据还要经过解析，这就造成爬虫并不会等待你的数据加载完成，所以其实Vue项目的seo体验并不是很好



## 最强王者

### 28. Vue响应式是怎么实现的？

整体思路是数据劫持+观察者模式

对象内部通过`defineReactive` 方法，使用 `Object.defineProperty` 将属性进行劫持（只会劫持已经存在的属性），数组则是通过重写数组方法来实现。当页面使用对应属性时，每个属性都拥有自己的`dep`属性，存放他所依赖的`watcher`（依赖收集），当属性变化后会通知自己对应的`watcher` 去更新(派发更新)。

想详细了解过程，建议阅读我的**Vue源码解析系列**[4]

```
const \\{ arrayMethods \\} = require('./array')

class Observer \\{
    constructor(value) \\{
        Object.defineProperty(value, '__ob__', \\{
            value: this,
            enumerable: false,
            writable: true,
            configurable: true
        \\})
        if(Array.isArray(value)) \\{
            value.__proto__ = arrayMethods
            this.observeArray(value)
        \\} else \\{
            this.walk(value)
        \\}
    \\}

    walk(data) \\{
        let keys = Object.keys(data)
        for(let i = 0; i < keys.length; i++) \\{
            const key = keys[i]
            const value = data[key]
            defineReactive(data, key, value)
        \\}
    \\}

    observeArray(items) \\{
        for(let i = 0; i < items.length; i++) \\{
            observe(items[i])
        \\}
    \\}
\\}

function defineReactive(data, key, value) \\{
    const childOb = observe(value)

    const dep = new Dep()

    Object.defineProperty(data, key, \\{
        get() \\{
            console.log('获取值')
            if (Dep.target) \\{
                dep.depend()

                if (childOb) \\{
                    childOb.dep.depend()

                    if (Array.isArray(value)) \\{
                        dependArray(value)
                    \\}
                \\}
            \\}
            return value
        \\},
        set(newVal) \\{
            if (newVal === value) return
            observe(newVal)
            value = newVal
            dep.notify()
        \\}
    \\})
\\}

function observe(value) \\{
    if (Object.prototype.toString.call(value) === '[object Object]' || Array.isArray(value)) \\{
        return new Observer(value)
    \\}
\\}

function dependArray(value) \\{
    for(let e, i = 0, l = value.length; i < l; i++) \\{
        e = value[i]

        e && e.__ob__ && e.__ob__.dep.depend()

        if (Array.isArray(e)) \\{
            dependArray(e)
        \\}
    \\}
\\}

// array.js
const arrayProto = Array.prototype

const arrayMethods = Object.create(arrayProto)

const methodsToPatch = [
    'push',
    'pop',
    'shift',
    'unshift',
    'splice',
    'reverse',
    'sort'
]

methodsToPatch.forEach(method => \\{
    arrayMethods[method] = function (...args) \\{
        const result = arrayProto[method].apply(this, args)

        const ob = this.__ob__

        var inserted

        switch (method) \\{
            case 'push':
            case 'unshift':
                inserted = args
                break;
            case 'splice':
                inserted = args.slice(2)
            default:
                break;
        \\}

        if (inserted) ob.observeArray(inserted)

        ob.dep.notify()

        return result
    \\}
\\})
```



### 29. 为什么只对对象劫持，而要对数组进行方法重写？

因为对象最多也就几十个属性，拦截起来数量不多，但是数组可能会有几百几千项，拦截起来非常耗性能，所以直接重写数组原型上的方法，是比较节省性能的方案



### 30. Vue的模板编译原理？

因为这个问题讲起来可能比较长，所以：

建议看我这篇**「Vue源码学习(二)」你不知道的-模板编译原理**[5]



### 32. Vue.set方法的原理？

```
function set(target, key, val) \\{
    // 判断是否是数组
    if (Array.isArray(target)) \\{
        // 判断谁大谁小
        target.length = Math.max(target.length, key)
        // 执行splice
        target.splice(key, 1, val)
        return val
    \\}

    const ob = target.__ob__

    // 如果此对象没有不是响应式对象，直接设置并返回
    if (key in target && !(key in target.prototype) || !ob) \\{
        target[key] = val
        return val
    \\}

    // 否则，新增属性，并响应式处理
    defineReactive(target, key, val)
    return val
\\}
```



### 33. Vue.delete方法的原理？

```
function del (target, key) \\{
    // 判断是否为数组
    if (Array.isArray(target)) \\{
        // 执行splice
        target.splice(key, 1)
        return
    \\}

    const ob = target.__ob__

    // 对象本身就没有这个属性，直接返回
    if (!(key in target)) return


    // 否则，删除这个属性
    delete target[key]

    // 判断是否是响应式对象，不是的话，直接返回
    if (!ob) return
    // 是的话，删除后要通知视图更新
    ob.dep.notify()
\\}
```



### 34. nextTick的原理？

```
let callbacks = []; //回调函数
let pending = false;
function flushCallbacks() \\{
  pending = false; //把标志还原为false
  // 依次执行回调
  for (let i = 0; i < callbacks.length; i++) \\{
    callbacks[i]( i);
  \\}
\\}
let timerFunc; //先采用微任务并按照优先级优雅降级的方式实现异步刷新
if (typeof Promise !== undefined) \\{
  // 如果支持promise
  const p = Promise.resolve();
  timerFunc = () => \\{
    p.then(flushCallbacks);
  \\};
\\} else if (typeof MutationObserver !== undefined) \\{
  // MutationObserver 主要是监听dom变化 也是一个异步方法
  let counter = 1;
  const observer = new MutationObserver(flushCallbacks);
  const textNode = document.createTextNode(String(counter));
  observer.observe(textNode, \\{
    characterData: true,
  \\});
  timerFunc = () => \\{
    counter = (counter + 1) \\% 2;
    textNode.data = String(counter);
  \\};
\\} else if (typeof setImmediate !== undefined) \\{
  // 如果前面都不支持 判断setImmediate
  timerFunc = () => \\{
    setImmediate(flushCallbacks);
  \\};
\\} else \\{
  // 最后降级采用setTimeout
  timerFunc = () => \\{
    setTimeout(flushCallbacks, 0);
  \\};
\\}

export function nextTick(cb) \\{
  callbacks.push(cb);
  if (!pending) \\{
    pending = true;
    timerFunc();
  \\}
\\}
```



## 冷门的知识点

### 36. 如果子组件改变props里的数据会发生什么

props可以修改对象的属性值，不能直接改其他类型的值

- 改变的props数据是基本类型

> 如果修改的是基本类型，则会报错

```
props: \\{
    num: Number,
  \\}
created() \\{
    this.num = 999
  \\}
```

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/gMvNo9rxo40PPicD3fczxSYXZxxV3D2ORlUNlxTKRMrIBzJ1XonRXojcVYdg8fsMpncY9eHxxYJDp6rYngeL9Rw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)0458e2ff1538ee85d42953cec9a94ca.png

- 改变的props数据是引用类型

```
props: \\{
    item: \\{
      default: () => \\{\\},
    \\}
  \\}
created() \\{
    // 不报错，并且父级数据会跟着变
    this.item.name = 'sanxin';
    
    // 会报错，跟基础类型报错一样
    this.item = 'sss'
  \\},
```



### 37. props怎么自定义验证

```
props: \\{
    num: \\{
      default: 1,
      validator: function (value) \\{
          // 返回值为true则验证不通过，报错
          return [
            1, 2, 3, 4, 5
          ].indexOf(value) !== -1
    \\}
    \\}
  \\}
```



### 38. watch的immediate属性有什么用？

> 比如平时created时要请求一次数据，并且当搜索值改变，也要请求数据，我们会这么写：

```
created()\\{
  this.getList()
\\},
watch: \\{
  searchInputValue()\\{
    this.getList()
  \\}
\\}
```

> 使用`immediate`完全可以这么写，当它为`true`时，会初始执行一次

```
watch: \\{
  searchInputValue:\\{
    handler: 'getList',
    immediate: true
  \\}
\\}
```



### 39. watch监听一个对象时，如何排除某些属性的监听

> 下面代码是，params发生改变就重新请求数据，无论是a，b，c，d属性改变

```
data() \\{
    return \\{
      params: \\{
        a: 1,
        b: 2,
        c: 3,
        d: 4
      \\},
    \\};
  \\},
watch: \\{
    params: \\{
      deep: true,
      handler() \\{
        this.getList;
      \\},
    \\},
  \\}
```

> 但是如果我只想要a，b改变时重新请求，c，d改变时不重新请求呢？

```
mounted() \\{
    Object.keys(this.params)
      .filter((_) => ![c, d].includes(_)) // 排除对c，d属性的监听
      .forEach((_) => \\{
        this.$watch((vm) => vm.params[_], handler, \\{
          deep: true,
        \\});
      \\});
  \\},
data() \\{
    return \\{
      params: \\{
        a: 1,
        b: 2,
        c: 3,
        d: 4
      \\},
    \\};
  \\},
watch: \\{
    params: \\{
      deep: true,
      handler() \\{
        this.getList;
      \\},
    \\},
  \\}
```

> 欢迎关注公众号：`前端印象`，每日精选好文推送



### 40. 审查元素时发现data-v-xxxxx，这是啥？

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/gMvNo9rxo40PPicD3fczxSYXZxxV3D2ORqNJn2TO6WXVPh7NTpsSY4HHffjia9A4uiceWZfablgNoqAL5Kx9Rzsdg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)image.png

> 这是在标记vue文件中css时使用scoped标记产生的，因为要保证各文件中的css不相互影响，给每个component都做了唯一的标记，所以每引入一个component就会出现一个新的'data-v-xxx'标记



### 41. computed如何实现传参？

```
// html
<div>\\\{\\\{ total(3)\\\}\\\} }}

// js
computed: \\{
    total() \\{
      return function(n) \\{
          return n * this.num
         \\}
    \\},
  \\}
```



### 42. vue的hook的使用

- 同一组件中使用

> 这是我们常用的使用定时器的方式

```
export default\\{
  data()\\{
    timer:null  
  \\},
  mounted()\\{
      this.timer = setInterval(()=>\\{
      //具体执行内容
      console.log('1');
    \\},1000);
  \\}
  beforeDestory()\\{
    clearInterval(this.timer);
    this.timer = null;
  \\}
\\}
```

> 上面做法不好的地方在于：得全局多定义一个timer变量，可以使用hook这么做：

```
export default\\{
  methods:\\{
    fn()\\{
      const timer = setInterval(()=>\\{
        //具体执行代码
        console.log('1');
      \\},1000);
      this.$once('hook:beforeDestroy',()=>\\{
        clearInterval(timer);
        timer = null;
      \\})
    \\}
  \\}
\\}
```

- 7.2 父子组件使用

> 如果子组件需要在mounted时触发父组件的某一个函数，平时都会这么写：

```
//父组件
<rl-child @childMounted=childMountedHandle
/>
method () \\{
  childMountedHandle() \\{
  // do something...
  \\}
\\},

// 子组件
mounted () \\{
  this.$emit('childMounted')
\\},
```

> 使用hook的话可以更方便：

```
//父组件
<rl-child @hook:mounted=childMountedHandle
/>
method () \\{
  childMountedHandle() \\{
  // do something...
  \\}
\\},
```



### 43. provide和inject是响应式的吗？

```
// 祖先组件
provide()\\{
    return \\{
   // keyName: \\{ name: this.name \\}, // value 是对象才能实现响应式，也就是引用类型
      keyName: this.changeValue // 通过函数的方式也可以[注意，这里是把函数作为value，而不是this.changeValue()]
   // keyName: 'test' value 如果是基本类型，就无法实现响应式
    \\}
  \\},
data()\\{
  return \\{
 name:'张三'
\\}
  \\},
  methods: \\{
   changeValue()\\{
    this.name = '改变后的名字-李四'
   \\}
  \\}  
  
  // 后代组件
  inject:['keyName']
  create()\\{
 console.log(this.keyName) // 改变后的名字-李四
\\}
```



### 44.Vue的el属性和 $mount优先级？

> 比如下面这种情况，Vue会渲染到哪个节点上

```
new Vue(\\{
  router,
  store,
  el: '#app',
  render: h => h(App)
\\}).$mount('#ggg')
```

> 这是官方的一张图，可以看出`el`和`$mount`同时存在时，`el优先级` > `$mount`

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/gMvNo9rxo40PPicD3fczxSYXZxxV3D2ORib744Hzu19Rsf5HIpFjAeakRVBgeMf7sic9O8hvfs8gu9JMTntut1tjQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)image.png



### 45. 动态指令和参数使用过吗？

```
<template>
    ...
    <aButton @[someEvent]=handleSomeEvent() :[someProps]=1000 />...
</template>
<script>
  ...
  data()\\{
    return\\{
      ...
      someEvent: someCondition ? click : dbclick,
      someProps: someCondition ? num : price
    \\}
  \\},
  methods: \\{
    handleSomeEvent()\\{
      // handle some event
    \\}
  \\}  
</script>
```



### 46. 相同的路由组件如何重新渲染？

> 开发人员经常遇到的情况是，多个路由解析为同一个Vue组件。问题是，Vue出于性能原因，默认情况下共享组件将不会重新渲染，如果你尝试在使用相同组件的路由之间进行切换，则不会发生任何变化。

```
const routes = [
  \\{
    path: /a,
    component: MyComponent
  \\},
  \\{
    path: /b,
    component: MyComponent
  \\},
];
```

> 如果依然想重新渲染，怎么办呢？可以使用`key`

```
<template>
    <router-view :key=$route.path></router-view>
</template>
```



### 47. 自定义v-model

> 默认情况下，v-model 是 @input 事件侦听器和 :value 属性上的语法糖。但是，你可以在你的Vue组件中指定一个模型属性来定义使用什么事件和value属性——非常棒！

```
export default: \\{
  model: \\{
    event: 'change',
    prop: 'checked'  
  \\}
\\}
```



### 48. 如何将获取data中某一个数据的初始状态？

> 在开发中，有时候需要拿初始状态去计算。例如

```
data() \\{
    return \\{
      num: 10
  \\},
mounted() \\{
    this.num = 1000
  \\},
methods: \\{
    howMuch() \\{
        // 计算出num增加了多少，那就是1000 - 初始值
        // 可以通过this.$options.data().xxx来获取初始值
        console.log(1000 - this.$options.data().num)
    \\}
  \\}
```



### 49.为什么不建议v-for和v-if同时存在

```
<div v-for=item in [1, 2, 3, 4, 5, 6, 7] v-if=item !== 3>
    \\\{\\\{ite\\\}\\\}m}}
</div>
```

> 上面的写法是v-for和v-if同时存在，会先把7个元素都遍历出来，然后再一个个判断是否为3，并把3给隐藏掉，这样的坏处就是，渲染了无用的3节点，增加无用的dom操作，建议使用computed来解决这个问题：

```
<div v-for=item in list>
    \\\{\\\{ite\\\}\\\}m}}
</div>

computed() \\{
    list() \\{
        return [1, 2, 3, 4, 5, 6, 7].filter(item => item !== 3)
    \\}
  \\}
```
