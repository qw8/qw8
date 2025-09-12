---
title: vue实践
date: 2024-03-11 21:02:08
categories: 
- 前端知识
tags:
- vue
---

### vue几种传值方式

1 :v-bind  $mit 
2 回调函数(callback)
3 parent + $children
4 provide + inject
5 $attrs + $ilsteners
6 ref refs



### vue中的activated和deactivated

当keepalive页面缓存下来的时候，只会调用一次created这个钩子函数，因为已经被缓存下来了，所以我们在created中获取按钮权限的话，tab栏再次进入的话就不会触发created钩子了，而代之的是使用我们的activated钩子函数。

keep-alive是Vue内置的一个组件，可以是被包含的组件保留状态，或避免重新渲染当页面被keep-alive缓存下来的时候，vuet提供两个钩子函数

- activated被 keep-alive 缓存的组件激活时调用。
- deactivated被 keep-alive 缓存的组件失活时调用。

当keepalive页面缓存，有activated钩子和created钩子函数时，这两个函数会被同时触发，此时应该使用activated代替created，因为created只会触发一次

页面被缓存下来的时候，就不会触发destroyed生命钩子，取而代之触发的是deactivated钩子

然后引出我们keep-alive里边的两个属性

- include 字符串或正则表达,只有匹配的组件会被缓存
- exclude 字符串或正则表达式 ，任何匹配的组件都不会被缓存



### 具名插槽

　　需要多个插槽的情况，slot 元素有一个特殊的属性：name，用来定义额外的插槽。一个不带 name 的 <slot> 出口会带有隐含的名字“default”。

　　在向具名插槽提供内容的时候，我们可以在一个 <template> 元素上使用 v-slot 指令，并以 v-slot 的参数的形式提供其名称:

```
<template v-slot:footer>
  <p>展示</p>
</template>
```

代码

```
//父组件
<template>
  <div>
    <About>
      <template v-slot:header="slotProps">
        <h1>\\\{\\\{slotProps.header + ' ' + msg\\\}\\\}</h1>
      </template>
      <p>这是没有命名的slot</p>
      <p>这是没有命名的slot2</p>
      <template v-slot:footer>
        <p>v-slot:footer</p>
      </template>
    </About>
  </div>
</template>

<script>
import About from './About.vue'
export default \\{
	data() \\{
    	return \\{
      		msg: '这是根组件的消息msg'
    	\\}
  	\\},
	components: \\{
		About
	\\}
\\}
</script>
```

```
//子组件
<template>
  <div>
    <header>
      <slot name="header" :header="header"></slot>  //header是要传入父组件插槽中的值
    </header>
    <slot></slot>
    <footer>
      <slot name="footer"></slot>
    </footer>
  </div>
</template>

<script>
export default \\{
	data() \\{
    return \\{
      	header: '来自子组件的头部消息header'
    \\}
  \\}
\\}
</script>
```

渲染结果如下

### 总结

1、组件中可以使用template标签，加v-slot指令制定具名插槽，当没有指定插槽name时，默认出口会带有隐含的名字“default”。 

2、根组件可以利用 `v-slot:header="slotProps"`接受组件中的消息，组件中只需要在

`<slot name="header" :header="header"></slot>`就可以了

3、如果被提供的内容只有一个默认插槽时，组件的标签可以直接被当做插槽的模板来使用 `<about v-slot="slotProps">` 

4、动态参数也可是使用到插槽当中，例如： `pro: 'header'`， `<template v-slot:[pro]='solt'>nihao \\\{\\\{solt.heade\\\}\\\}r}}</template>`，代表name属性是header的插槽

5、v-slot的缩写是#，但是如果使用#的话，必须始终使用具插槽来代替

```
<about #default="slotProps">
```



### vue自定义通用函数（全局函数）

1、我们可以在src目录下新建一个通用的js来存放全局函数，比如我这里是建了util.js,你们也可以取名tool.js之类的，随你们高兴。因为可能会用到其他通用的js，为了代码的规范，我都将他们放到utils的文件夹里了，这些都是自定义的，命名没有强制要求

然后怎么在util.js里面定义全局函数呢，如下：

```
/*
 *首先是相互调用，接收的地方用import，输出的地方用export
 *比如这里面需要用到cookie.js中的方法，那么就要先把cookie引用进来，这个思想跟后面的引用是一致的
 */
import cookie from './cookie';

/*
 *接下来是定义全局函数
 *因为全局函数是要给外部使用的，所以需要将函数用export告知外部即可
 *比如我们在这里定义了日期的格式，供后面组件统一改变
 */
//Date对象转化为yyyy-MM-dd格式
export function dateFormat(dateObj)\\{
  var year = dateObj.getFullYear();
  var month = ("0" + (dateObj.getMonth() + 1)).slice(-2);
  var day = ("0" + dateObj.getDate()).slice(-2);
  return year + "-" + month + "-" + day;
\\}
```

2、如何调用全局函数，就跟上面提到的一样，那里需要用到就在那个组件的script开始的地方import进util.js的文件，然后调用util里面的函数就行了，如下：

```
<script>
    import * as util from '../../../utils/util'
    export default \\{
        data() \\{
          return \\{
              //这里调用了util的dateFormat()函数
              outputStartDate: util.dateFormat(new Date()),
          \\}
        \\}
    \\}
</script>
```

**import * as xxx from ‘xxx’: 会将若干export导出的内容组合成一个对象返回；**

```
import * as obj from 'xx'  这种写法是把所有的输出包裹到obj对象里

xxx里中：
export function test()\\{
    return '返回是test 内容';
\\}
export function login()\\{
    return '返回login 内容';
\\}
调用test 函数，即obj.test();
调用login 函数，即obj.login();
```

**import xxx from ‘xxx’：（export default Din）只会导出这个默认的对象作为一个对象**



### watch用法

watch的作用可以监控一个值的变换，并调用因为变化需要执行的方法。可以通过watch动态改变关联的状态。

```
 data:\\{
     a:1,
     b:\\{
         c:1
     \\}
 \\},
 watch:\\{
     a(val, oldVal)\\{//普通的watch监听
         console.log("a: "+val, oldVal);
     \\},
     b:\\{//深度监听，可监听到对象、数组的变化
         handler(val, oldVal)\\{
             console.log("b.c: "+val.c, oldVal.c);
         \\},
         deep:true //true 深度监听
     \\}
 \\}
```



### vue请求数据放在哪个生命周期？

异步请求在哪个阶段都可以调用，因为会先执行完生命周期的钩子函数之后，才会执行异步函数，但如果考虑用户体验方面的话，在**created中调用异步请求最佳**，用户就越早感知页面的已加载，毕竟越早获取数据，在mounted实例挂载的时候就越及时。

在created 钩子函数触发时，组件的 data 数据、通过路由注入的数据已经具备，此时可以使用这些数据发送 ajax 请求。

在 mounted 钩子函数中发起也可以，但是相对比 created 稍微迟了一些。

如果不需要依赖任何数据发起 ajax 请求，那么在 beforeCreate 发起也可以。

最好的还是放在created中，created时，data中的数据已经通过Object.defineProperty方法劫持、添加观察者模式。此时的数据已经支持双向绑定。从生命周期来看，created会在mounted之前调用，如果fetch接口响应数据时间相同的话，**放在created中， 能更快的获取并渲染视图，体验会更好~**

mounted()以及created()两个钩子函数都可以，但一般我会在created的时候去请求数据，习惯了。

在mounted()和created()请求数据好像并没有太大的不同，但好像多数人都是在created()阶段请求数据



### vue 中的@、@/和./的区别

@：表示vue语法中v-on的简写；绑定事件的专用格式。当事件触发的时候，函数才会来调用。

使用格式，在标签内部添加v-on:事件名="事件"

注意：Vue实例中所有的函数必须放在methods对象中，否则利用v-on绑定的事件，系统会报找不到该事件的错误

@ /：表示 src目录下；

. /：表示当前目录下；



### Vue中的字符串模板的使用

1、HTML模板和字符串模板

HTML模板：直接在HTML页面挂载的模板。（即非字符串模板）

非字符串模板：在单文件里用 <template></template> 指定的模板，换句话说，写在 html 中的就是非字符串模板。

字符串模板：在js字符串中定义的模板。

2、Props属性：HTML 特性是不区分大小写的。所以，当使用的不是字符串模板时，camelCase (驼峰式命名) 的 props属性需要转换为相对应的 kebab-case (短横线分隔式命名)：

（1）、HTML模板：

```
Vue.component(``'child'``, \\{``// 在 JavaScript 中使用 camelCase``props: [``'myMessage'``],``template: ``'<span>\\\{\\\{ myMessage\\\}\\\} }}</span>'``\\})
```

（2）、字符串模板：

```
<!-- 在 HTML 中使用kebab-case -->``<``child` `my-message``=``"hello!"``></``child``>
```

3、组件名大小写：

注意：当直接在 DOM 中使用一个组件 (而不是在字符串模板或单文件组件) 的时候，我们强烈推荐遵循 W3C 规范中的自定义组件名 (字母全小写且必须包含一个连字符)。这会帮助你避免和当前以及未来的 HTML 元素相冲突。

(1)、使用 kebab-case:

```
Vue.component(``'my-component-name'``, \\{ ``/* ... */` `\\});
```

当使用 kebab-case (短横线分隔命名) 定义一个组件时，你也必须在引用这个自定义元素时使用 kebab-case，例如 <my-component-name>。

(2)、使用 PascalCase:

```
Vue.component(``'MyComponentName'``, \\{ ``/* ... */` `\\})
```

当使用 PascalCase (驼峰式命名) 定义一个组件时，你在引用这个自定义元素时两种命名法都可以使用。也就是说 <my-component-name> 和 <MyComponentName> 都是可接受的。注意，尽管如此，直接在 DOM (即非字符串的模板，如：在单个组件的<template></template>中 或者 index.html中直接CDN引入vue.js的<div id="app"></div>中) 使用时只有 kebab-case 是有效的，使用驼峰式，是不会渲染的。

#### 传统的JavaScript语言，输出模板通常是这样的写的。

```
$('#result').append(
   'There are <b>' + basket.count + '</b> ' +
   'items in your basket, ' +
   '<em>' + basket.onSale +
   '</em> are on sale!'
 );
```

上面这种写法相当繁琐不方便，ES6 引入了模板字符串解决这个问题。

```
$('#result').append(`
   There are <b>$\\{basket.count\\}</b> items
    in your basket, <em>$\\{basket.onSale\\}</em>
   are on sale!
 `);
```

模板字符串（template string）是增强版的字符串，用反引号（`）标识。它可以当作普通字符串使用，也可以用来定义多行字符串，或者在字符串中嵌入变量

```
// 普通字符串
`In JavaScript '\n' is a line-feed.`
 
// 多行字符串
`In JavaScript this is
 not legal.`
 
console.log(`string text line 1
string text line 2`);
 
// 字符串中嵌入变量
let name = "Bob", time = "today";
`Hello $\\{name\\}, how are you $\\{time\\}?
```

上面代码中的模板字符串，都是用反引号表示。如果在模板字符串中需要使用反引号，则前面要用反斜杠转义。

```
let greeting ``=` ``\`Yo\` World!`;
```

输入结果：`Yo` World!

如果使用模板字符串表示多行字符串，所有的空格和缩进都会被保留在输出之中。

```
$('#list').html(`
<ul>
  <li>first</li>
  <li>second</li>
</ul>
`);　
```



### vue-cli-service build 不同环境配置

#### 背景

在项目部署时，我们需要在测试环境和生产环境使用不同的变量。
`vue-cli`提供了`vue-cli-service build`打包命令，然而`vue-cli-service build`默认的环境变量值则为`production`。那我们通过`npm run build`打包构建，想要实现不同环境使用不同变量，暂时不能实现。

#### vue-cli-service介绍

[vue-cli-service介绍](https://cli.vuejs.org/zh/guide/cli-service.html#使用命令)
vue-cli生成项目时，在`package.json`中会设置：

```
  "scripts": \\{
    "serve": "vue-cli-service serve",
    "build": "vue-cli-service build"
\\}
```

`vue-cli-service serve` 命令会启动一个开发服务器，默认指定的环境模式为`development`。
`vue-cli-service build` 会在 dist/ 目录产生一个可用于生产环境的包，带有 `JS/CSS/HTML` 的压缩，和为更好的缓存而做的自动的` vendor chunk splitting`。

#### 环境变量和模式

在项目的根目录下我们可以创建不同模式的文件：

```
.env                # 在所有的环境中被载入
.env.local          # 在所有的环境中被载入，但会被 git 忽略
.env.[mode]         # 只在指定的模式中被载入
.env.[mode].local   # 只在指定的模式中被载入，但会被 git 忽略
```

一般来说，我们会存在`本地环境`、`测试环境`、`线上环境`，那我们就需要创建三个模式文件。

- `.env.development`开发环境模式

```
// 环境变量
NODE_ENV=development
// 以 VUE_APP_ 开头的变量会被 webpack.DefinePlugin 静态嵌入到客户端侧的包中
VUE_APP_ENV = 'development'
```

- `.env.test`测试环境模式

```
// 环境变量（这里的环境变量是跟打包有关的，production则会进行压缩代码等，真正跟每个环境有关的变量是下面以VUE_APP开头的变量）
NODE_ENV=production
// 以 VUE_APP_ 开头的变量会被 webpack.DefinePlugin 静态嵌入到客户端侧的包中
VUE_APP_ENV = 'test'
```

- `.env.production`线上环境模式

```
// 环境变量
NODE_ENV=production
// 以 VUE_APP_ 开头的变量会被 webpack.DefinePlugin 静态嵌入到客户端侧的包中
VUE_APP_ENV = 'production'
```

#### 配置不同模式

部署时，构建打包执行`npm run build`，则会执行`vue-cli-service build`，默认模式为`production`，对应`.env.production`文件，取此文件中的环境变量。

想要配置测试环境，需要在scripts下增加脚本：

```
"scripts": \\{
    "serve": "vue-cli-service serve",
    "build": "vue-cli-service build",
    "build-test": "vue-cli-service build --mode test"
\\}
```

测试环境打包构建时，执行`npm run build-test`即可。

#### index.html使用环境变量

在`index.html`中可通过`<\\%= process.env.VUE_APP_xxx \\%>`的方式获取不同模式下配置的环境变量。

#### 验证

可通过不同模式下对应的环境变量，判断是否为对应的环境



### vue-cli3.0有两个放置静态资源的目录分别是public和assets。

public放不会变动的文件（相当于vue-cli2.x中的static）
public/ 目录下的文件并不会被Webpack处理：它们会直接被复制到最终的打包目录（默认是dist/static）下。必须使用绝对路径引用这些文件，这个取决于你vue.config.js中publicPath的配置，默认的是/。
assets放可能会变动的文件
assets目录中的文件会被webpack处理解析为模块依赖，只支持相对路径形式。
简单来说就是就是public放别人家js文件（也就是不会变动），assets放自己写的js文件（需要改动的文件）



### 导出函数

```
export function copy (dom) \\{\\}//普通函数
export const share = (id,name) => \\{\\}//箭头函数
```



### v-for（：key）绑定index、id、key的区别

使用v-for渲染元素时，使用元素自身的id属性去指定渲染元素的key值有利于单个元素的重新渲染，若采用其他如v-for提供的index, key等值，在改变渲染出来的DOM结构时，会触发所有元素的**重新渲染**，当数据过大时，可能会造成性能负担。

**当我们在使用v-for进行渲染时，尽可能使用渲染元素自身属性的id给渲染的元素绑定一个key值，这样在当前渲染元素的DOM结构发生变化时，能够单独响应该元素而不触发所有元素的渲染。**



### vue.nextTick()方法的使用详解

#### 什么是Vue.nextTick()？

更新数据后立即操作dom

定义：

在下次 DOM 更新循环结束之后执行延迟回调。在修改数据之后立即使用这个方法，获取更新后的 DOM。

所以就衍生出了这个获取更新后的DOM的Vue方法。所以放在Vue.nextTick()回调函数中的执行的应该是会对DOM进行操作的 js代码；

理解：

nextTick()，是将回调函数延迟在下一次dom更新数据后调用，简单的理解是：当数据更新了，在dom中渲染后，自动执行该函数。

```
<template>
  <div class="hello">
    <div>
      <button id="firstBtn" @click="testClick()" ref="aa">\\\{\\\{testMs\\\}\\\}g}}</button>
    </div>
  </div>
</template>

<script>
export default \\{
  name: 'HelloWorld',
  data () \\{
    return \\{
      testMsg:"原始值",
    \\}
  \\},
  methods:\\{
    testClick:function()\\{
      let that=this;
      that.testMsg="修改后的值";
      console.log(that.$refs.aa.innerText);   //that.$refs.aa获取指定DOM，输出：原始值
    \\}
  \\}
\\}
</script>
```


使用this.$nextTick()

```
methods:\\{
    testClick:function()\\{
      let that=this;
      that.testMsg="修改后的值";
      that.$nextTick(function()\\{
        console.log(that.$refs.aa.innerText);  //输出：修改后的值
      \\});
    \\}
  \\}
```

注意：Vue 实现响应式并不是数据发生变化之后 DOM 立即变化，而是按一定的策略进行 DOM 的更新。$nextTick 是在下次 DOM 更新循环结束之后执行延迟回调，在修改数据之后使用 $nextTick，则可以在回调中获取更新后的 DOM，

#### 什么时候需要用的Vue.nextTick()？

1、Vue生命周期的created()钩子函数进行的DOM操作一定要放在Vue.nextTick()的回调函数中，原因是在created()钩子函数执行的时候DOM 其实并未进行任何渲染，而此时进行DOM操作无异于徒劳，所以此处一定要将DOM操作的js代码放进Vue.nextTick()的回调函数中。与之对应的就是mounted钩子函数，因为该钩子函数执行时所有的DOM挂载已完成。

```
created()\\{
    let that=this;
    that.$nextTick(function()\\{  //不使用this.$nextTick()方法会报错
        that.$refs.aa.innerHTML="created中更改了按钮内容";  //写入到DOM元素
    \\});
  \\},
```


2、当项目中你想在改变DOM元素的数据后基于新的dom做点什么，对新DOM一系列的js操作都需要放进Vue.nextTick()的回调函数中；通俗的理解是：更改数据后当你想立即使用js操作新的视图的时候需要使用它

```
<template>
  <div class="hello">
    <h3 id="h">\\\{\\\{testMs\\\}\\\}g}}</h3>
  </div>
</template>

<script>
export default \\{
  name: 'HelloWorld',
  data () \\{
    return \\{
      testMsg:"原始值",
    \\}
  \\},
  methods:\\{
    changeTxt:function()\\{
      let that=this;
      that.testMsg="修改后的文本值";  //vue数据改变，改变dom结构
      let domTxt=document.getElementById('h').innerText;  //后续js对dom的操作
      console.log(domTxt);  //输出可以看到vue数据修改后DOM并没有立即更新，后续的dom都不是最新的
      if(domTxt==="原始值")\\{
        console.log("文本data被修改后dom内容没立即更新");
      \\}else \\{
        console.log("文本data被修改后dom内容被马上更新了");
      \\}
    \\},
  \\}
\\}
</script
```

正确的用法是：vue改变dom元素结构后使用vue.$nextTick()方法来实现dom数据更新后延迟执行后续代码

    changeTxt:function()\\{
      let that=this;
      that.testMsg="修改后的文本值";  //修改dom结构
       
      that.$nextTick(function()\\{  //使用vue.$nextTick()方法可以dom数据更新后延迟执行
        let domTxt=document.getElementById('h').innerText; 
        console.log(domTxt);  //输出可以看到vue数据修改后并没有DOM没有立即更新，
        if(domTxt==="原始值")\\{
          console.log("文本data被修改后dom内容没立即更新");
        \\}else \\{
          console.log("文本data被修改后dom内容被马上更新了");
        \\}
      \\});
    \\},

3、在使用某个第三方插件时 ，希望在vue生成的某些dom动态发生变化时重新应用该插件，也会用到该方法，这时候就需要在 $nextTick 的回调函数中执行重新应用插件的方法。

待完善？？？

#### Vue.nextTick(callback) 使用原理：

原因是，Vue是异步执行dom更新的，一旦观察到数据变化，Vue就会开启一个队列，然后把在同一个事件循环 (event loop) 当中观察到数据变化的 watcher 推送进这个队列。如果这个watcher被触发多次，只会被推送到队列一次。这种缓冲行为可以有效的去掉重复数据造成的不必要的计算和DOm操作。而在下一个事件循环时，Vue会清空队列，并进行必要的DOM更新。
当你设置 vm.someData = 'new value'，DOM 并不会马上更新，而是在异步队列被清除，也就是下一个事件循环开始时执行更新时才会进行必要的DOM更新。如果此时你想要根据更新的 DOM 状态去做某些事情，就会出现问题。。为了在数据变化之后等待 Vue 完成更新 DOM ，可以在数据变化之后立即使用 Vue.nextTick(callback) 。这样回调函数在 DOM 更新完成后就会调用。

#### vue中this.$refs可以拿到,但是里面的属性undefind的问题

1.和vue的生命周期有关,必须要在从mounted开始拿,才能拿得到里面的Dom元素

2.想在element ui 对话框打开后取dom时，应该使用`$nextTick`，而不是直接使用`this.$refs. imgLocal2`：

```
        console.log('this.$refs.imgLocal2外面', this.$refs.imgLocal2);
        setTimeout(() => \\{
          console.log('this.$refs.imgLocal2 setTimeout', this.$refs.imgLocal2);
        \\}, 500);  // 不推荐
        this.$nextTick(() => \\{
          console.log('this.$refs.imgLocal2 $nextTick', this.$refs.imgLocal2);
        \\});
```

#### 说说nextTick的用处？

我举个例子，在vue中：

```
    this.name = "十年"
    this.age = 18
    this.gender = "男"
```

我们修改了三个变量，那问题来了，是每修改一次，DOM就更新一次吗？不是的，Vue采用的是异步更新的策略，通俗点说就是，同一事件循环内多次修改，会统一进行一次视图更新，这样才能节省性能嘛

看懂了上面，那你应该也看得懂下面的例子了吧：

```
    <div ref=testDiv>\\\{\\\{nam\\\}\\\}e}}</div>

    name: "十年"
    this.name = "十一年"
    console.log(this.$refs.testDiv.innerHTML) // 这里是啥呢

```

答案是“十年”，前面说了，Vue是异步更新，所以数据一更新，视图却还没更新，所以拿到的还是上一次的旧视图数据，那么想要拿到最新视图数据怎么办呢？

```
    this.name = "十一年"
    this.$nextTick(() => \\{
        console.log(this.$refs.testDiv.innerHTML) // 十一年
    \\})

```



### 组件注册使用命名

#### 组件名大小写

定义组件名的方式有两种：

#### 使用 kebab-case

```
Vue.component('my-component-name', \\{ /* ... */ \\})
```

当使用 kebab-case (短横线分隔命名) 定义一个组件时，你也必须在引用这个自定义元素时使用 kebab-case，例如 `<my-component-name>`。

#### 使用 PascalCase

```
Vue.component('MyComponentName', \\{ /* ... */ \\})
```

当使用 PascalCase (首字母大写命名) 定义一个组件时，你在引用这个自定义元素时两种命名法都可以使用。也就是说 `<my-component-name>` 和 `<MyComponentName>` 都是可接受的。注意，尽管如此，直接在 DOM (即非字符串的模板) 中使用时只有 kebab-case 是有效的。

```
<dia-logo v-if="dialogVisible" :dialog="dialogVisible" @toParent="getMag" />
<announ-cements :announcements="announcements" @toParent="getAnnounCements" />
    
import dialogo from './dialog'
import announCements from './AnnounCements'

export default \\{
  components: \\{
    "dia-logo": dialogo,
    announCements: AnnounCements
  \\}
\\}
```



### 命名可遵循以下规则：

1、有意义的名词、简短、具有可读性
2、以小写开头，采用短横线分割命名
3、基础组件名以Base、App 或 V开头
4、文件夹命名主要以功能模块代表命名
  以后开发一定要注意命名规范，减少不必要的问题，且容易维护。



### Vue组件中的方法书写顺序

```
    - name
    - components   
    - props    
    - data     
    - created
    - mounted
    - activited
    - update
    - beforeRouteUpdate
    - methods   
    - filter
    - computed
    - watch
```



### 获取个位十位百位千位数字

```
// var num1=1234
//prompt是可输入的弹出框
var num1=parseInt(prompt(“请输入一个四位数”))//将输入的数据（string类型）转换成number类型
var a //个位数
var b //十位数
var c //百位数
var d //千位数
//parseInt：将浮点数保留整数位
d=parseInt(num1/1000);
c=parseInt(num1/100)\\%10;
b=parseInt(num1/10)\\%10;
a=num1\\%10;
alert(“千位数：”+d+"，百位数："+c+"，十位数："+b+"，个位数"+a);
```

或者使用以下简单方法



### vue遍历数字或者字符串方法

```
<text :class="item==='.'?'point':'font'" v-for="item in couponBalance" :key="item">\\\{\\\{ite\\\}\\\}m}}</text>
```

数据处理

```
this.couponBalance = data.couponBalance.toFixed(2).toString()
```



### vue阻止点击事件向上传递

1.阻止向下冒泡

```
<div class="content" @click.self="cancelFunc"></div>
```

2.阻止向上冒泡

```
<div class="item" @click.stop="function">
```



### Transition

```
.fade-move,
    .fade-enter-active,
    .fade-leave-active \\{
      transition: all 0.5s cubic-bezier(0.55, 0, 0.1, 1);
    \\}
    .fade-enter-from,
    .fade-leave-to \\{
      opacity: 0;
      transform: scaleY(0.01) translate(30px, 0);
    \\}
    .fade-leave-active \\{
      position: absolute;
    \\}
```

这段代码是 Vue.js 中用于定义 CSS 过渡效果的样式。它通常与 Vue 的 ` <transition> ` 组件一起使用，以实现元素在插入、更新或移除时的动画效果。下面我会详细解释这段代码：

1. **过渡效果定义**:
   - `.fade-move, .fade-enter-active, .fade-leave-active`: 这些类选择器定义了过渡效果的公共属性。
   - `transition: all 0.5s cubic-bezier(0.55, 0, 0.1, 1);`: 这里定义了一个 CSS 过渡效果，该效果应用于所有可动画的属性（由 `all` 指定），持续时间为 0.5 秒，并使用了一个贝塞尔曲线函数 `cubic-bezier(0.55, 0, 0.1, 1)` 来定义过渡的速度曲线。
2. **进入过渡的起始状态**:
   - `.fade-enter-from`: 当元素开始插入时，它将具有这个类的样式。
   - `opacity: 0;`: 元素是完全透明的。
   - `transform: scaleY(0.01) translate(30px, 0);`: 元素在垂直方向上被压缩到几乎不可见（scaleY(0.01)），并向右移动了 30 像素。
3. **离开过渡的结束状态**:
   - `.fade-leave-to`: 当元素开始离开（即被移除）时，它将最终变为这个类的样式。
   - `opacity: 0;`: 同样，元素是完全透明的。
   - `transform: scaleY(0.01) translate(30px, 0);`: 与进入过渡的起始状态相同，元素在垂直方向上被压缩并向右移动。
4. **离开过渡的活跃状态**:
   - `.fade-leave-active`: 当元素正在离开时，它将具有这个类的样式。
   - `position: absolute;`: 这意味着正在离开的元素将脱离正常的文档流，并可能与其他元素重叠。这通常是为了确保在动画期间，正在离开的元素不会影响到其他元素的位置。

**总结**:

- 当一个元素开始插入时，它将从透明、垂直压缩并向右移动的状态开始，然后平滑地过渡到其正常状态。
- 当一个元素开始离开时，它首先会平滑地过渡到透明、垂直压缩并向右移动的状态，然后从这个状态消失。

注意：虽然 `.fade-move` 在这段代码中定义了过渡效果，但在给出的样式中并没有为它指定任何特定的动画属性。它可能是为了与 Vue 的 ` <transition> ` 组件的 `name` 属性一起使用，以便在需要时可以定义与移动相关的过渡效果。



### table样式

```
			<table>
                <thead>
                    <th></th>
                    <th>平台数据</th>
                    <th>TIS数据</th>
                </thead>
                <tbody>
                    <tr v-if="tableData.tis.type">
                        <td>合同类型</td>
                        <td>\\\{\\\{tableData.xiuchuan.typ\\\}\\\}e}}</td>
                        <td>\\\{\\\{tableData.tis.typ\\\}\\\}e}}</td>
                    </tr>
                    <tr v-if="tableData.tis.channel_ids">
                        <td>签约通道</td>
                        <td>
                            <div v-for="(item,index) in tableData.xiuchuan.channel_ids"
                                :key="index">\\\{\\\{ite\\\}\\\}m}}</div>
                        </td>
                        <td>
                            <div v-for="(item,index) in tableData.tis.channel_ids"
                                :key="index">\\\{\\\{ite\\\}\\\}m}}</div>
                        </td>
                    </tr>
                </tbody>
            </table>
            
// 表格
table \\{
    margin-top: 16px;
    thead \\{
        background: #e6f6fe;
    \\}
    th,
    tr \\{
        height: 48px;
    \\}
    th,
    td \\{
        padding: 4px 8px;
        text-align: left;
        vertical-align: middle;
    \\}
    /* 设置第1列 */
    th:nth-child(1),
    td:nth-child(1) \\{
        width: 76px;
        background: #e6f6fe;
    \\}
\\}
```

