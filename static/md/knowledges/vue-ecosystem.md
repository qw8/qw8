---
title: vue全家桶
date: 2024-03-10 21:02:08
categories: 
- 前端知识
tags:
- vue
- vue-router
- vue-cli
---

## vue-router

### vue-router 有哪几种导航钩子（ 导航守卫 ）？

答案：三种

第一种是全局导航钩子：router.beforeEach(to,from,next)，作用：跳转前进行判断拦截。
第二种：组件内的钩子；
第三种：单独路由独享组件



### 怎么定义 vue-router 的动态路由？怎么获取传过来的动态参数？

答案：

答：在 router 目录下的 index.js 文件中，对 path 属性加上/:id。 使用 router 对象的 params.id



### vue路由实现原理?或 vue-router原理?

说简单点，vue-router的原理就是通过对URL地址变化的监听，继而对不同的组件进行渲染。
每当URL地址改变时，就对相应的组件进行渲染。原理是很简单，实现方式可能有点复杂，主要有hash模式和history模式。
如果想了解得详细点，建议百度或者阅读源码。



### vue-router获取自定义参数

传值**：**

```
> this.$router.push(name:"test",params:\\{data:"test"\\});

> this.$router.push(path:"/test",query:\\{data:"test"\\});
```

取值（与传值一一对应）：

> $route.params      类型: Object
>
> 一个 key/value 对象，包含了动态片段和全匹配片段，如果没有路由参数，就是一个空对象。
>
> this.$route.params.data  //"test"

> $route.query       类型: Object
>
> 一个 key/value 对象，表示 URL 查询参数。例如，对于路径 /foo?user=1，则有 $route.query.user == 1，如果没有查询参数，则是个空对象。
>
> this.$route.query.data  //"test"

​        

### vue-router 路由模式（url中#号的解析）

​    参考链接：[vueRouter - mode API](https://router.vuejs.org/zh/api/#mode)

​    1）Hash模式：使用 URL hash 值来作路由。支持所有浏览器，包括不支持 HTML5 History Api 的浏览器。（URL中带有#号）：

> http://localhost:8080/#/

​    2）History模式：依赖HTML5 History API 和服务器配置。[HTML5 History模式](https://router.vuejs.org/zh-cn/essentials/history-mode.html)，(URL中不带有#号）:

> export default new Router (\\{
>
> ​     mode: 'history',
>
> ​    routes: [ \\{
>
> ​        path: '/',
>
> ​        name: '/',
>
> ​        component: main
>
> ​    \\} ]
>
> \\})

​    3）Abstract模式：支持所有javascript运行模式，如 Node.js 服务器端。如果发现没有浏览器的API，路由会自动强制进入这个模式。



### vue-router的go相关

> router.go(n)：类似 window.history.go(n)，在 history 记录中向前或后退n步(n为int类型)
>
> router.push(location)：导航到不同的 URL，则使用 router.push 方法。这个方法会**向 history 栈添加一个新的记录**，所以，当用户点击浏览器后退按钮时，则回到之前的 URL。
>
> router.replace(location)：跟 router.push 很像，唯一的不同就是，它不会向 history 添加新记录，而是跟它的方法名一样 —— *替换掉当前的 history 记录*。







## vue-cli

### 构建的 vue-cli 工程都到了哪些技术，它们的作用分别是什么？

1、vue.js：vue-cli 工程的核心，主要特点是 双向数据绑定 和 组件系统。

2、vue-router：vue 官方推荐使用的路由框架。

3、vuex：专为 Vue.js 应用项目开发的状态管理器，主要用于维护 vue 组件间共用的一些 变量 和 方法。

4、axios（ 或者 fetch 、ajax ）：用于发起 GET 、或 POST 等 http 请求，基于 Promise 设计。

5、vux 等：一个专为 vue 设计的移动端 UI 组件库。

6、创建一个 emit.js 文件，用于 vue 事件机制的管理。

7、webpack：模块加载和 vue-cli 工程打包器。



### vue-cli 工程常用的 npm 命令有哪些？

 **答案：**npm install、npm run dev、npm run build --report等

**解析：**

- 下载 node_modules 资源包的命令：npm install
- 启动 vue-cli 开发环境的 npm 命令：npm run dev
- vue-cli 生成 生产环境部署资源 的 npm 命令：npm run build
- 用于查看 vue-cli 生产环境部署资源文件大小的 npm 命令：npm run build --report，此命令必答

在浏览器上自动弹出一个 展示 vue-cli 工程打包后 app.js、manifest.js、vendor.js 文件里面所包含代码的页面。可以具此优化 vue-cli 生产环境部署的静态资源，提升 页面 的加载速度。



###  请说出 vue-cli 工程中每个文件夹和文件的用处

**vue-cli目录解析：**

- build 文件夹：用于存放 webpack 相关配置和脚本。开发中仅 偶尔使用 到此文件夹下 webpack.base.conf.js 用于配置 less、sass等css预编译库，或者配置一下 UI 库。

- config 文件夹：主要存放配置文件，用于区分开发环境、线上环境的不同。 常用到此文件夹下 config.js 配置开发环境的 端口号、是否开启热加载 或者 设置生产环境的静态资源相对路径、是否开启gzip压缩、npm run build 命令打包生成静态资源的名称和路径等。

- dist 文件夹：默认 npm run build 命令打包生成的静态资源文件，用于生产部署。

- node_modules：存放npm命令下载的开发环境和生产环境的依赖包。

- src: 存放项目源码及需要引用的资源文件。

  src下assets：存放项目中需要用到的资源文件，css、js、images等。

  src下componets：存放vue开发中一些公共组件：header.vue、footer.vue等。

  src下emit：自己配置的vue集中式事件管理机制。

  src下router：vue-router vue路由的配置文件。

  src下service：自己配置的vue请求后台接口方法。

  src下page：存在vue页面组件的文件夹。

  src下util：存放vue开发过程中一些公共的.js方法。

  src下vuex：存放 vuex 为vue专门开发的状态管理器。

  src下app.vue：使用标签<route-view></router-view>渲染整个工程的.vue组件。

  src下main.js：vue-cli工程的入口文件。

- index.html：设置项目的一些meta头信息和提供<div id="app"></div>用于挂载 vue 节

- package.json：用于 node_modules资源部 和 启动、打包项目的 npm 命令管理。

  

### config 文件夹 下 index.js 的对于工程 开发环境 和 生产环境 的配置

```
build 对象下 对于 生产环境 的配置：

index：配置打包后入口.html文件的名称以及文件夹名称
assetsRoot：配置打包后生成的文件名称和路径
assetsPublicPath：配置 打包后 .html 引用静态资源的路径，一般要设置成 "./"
productionGzip：是否开发 gzip 压缩，以提升加载速度

dev 对象下 对于 开发环境 的配置：

port：设置端口号
autoOpenBrowser：启动工程时，自动打开浏览器
proxyTable：vue设置的代理，用以解决 跨域 问题
```



###  vue-cli 中常用到的加载器

1.安装 sass:

2.安装 axios:

3.安装 mock:

4.安装 lib-flexible: --实现移动端自适应

5.安装 sass-resourses-loader



### vue.cli 中怎样使用自定义的组件？有遇到过哪些问题吗？

第一步：在 components 目录新建你的组件文件（如：indexPage.vue），script 一定要 export default \\{\\}

第二步：在需要用的页面（组件）中导入：import indexPage from '@/components/indexPage.vue'

第三步：注入到 vue 的子组件的 components 属性上面,components:\\{indexPage\\}

第四步：在 template 视图 view 中使用

遇到的问题：
例如有 indexPage 命名，使用的时候则 index-page



### babel相关

​    参考链接：[Babel 从入门到插件开发](http://web.jobbole.com/91277/)   

​                       [Babel](http://web.jobbole.com/tag/babel/)



### lodash相关

​    参考链接：[官方文档](http://www.css88.com/doc/lodash/)



### webGL

​    参考链接：[webGL—MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/WebGL_API/Tutorial/Adding_2D_content_to_a_WebGL_context)