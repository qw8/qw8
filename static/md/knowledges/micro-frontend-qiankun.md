---
title: 微前端qiankun
date: 2024-04-19 17:22:46
categories: 
- 前端知识
tags:
- 微前端
- qiankun
---

### qiankun微前端框架详细介绍

#### **一、概述**

qiankun是一个基于single-spa的微前端实现库，它旨在解决在构建大型、复杂前端应用时遇到的技术挑战。通过qiankun，开发者可以构建出高内聚、低耦合的微前端架构系统，使得每个微应用都能独立开发、独立部署，并且能够在主应用中无缝集成。

#### **二、核心特性**

1. **技术栈无关**：qiankun支持任意技术栈的应用接入，无论是React、Vue还是其他前端框架，都可以作为子应用轻松集成到主应用中。这使得不同团队可以独立选择适合自己的技术栈进行开发，提高了开发效率和团队协作的灵活性。
2. **沙箱隔离**：qiankun为每个子应用提供了JS沙箱环境，确保子应用之间的全局变量、样式等不会相互污染。这使得不同微应用可以在同一个页面中运行，而不会发生冲突或相互影响。
3. **动态加载与卸载**：qiankun支持动态加载和卸载子应用，根据路由的变化动态地挂载或卸载相应的子应用。这使得主应用可以根据需要灵活地加载所需的微应用，提高了应用的性能和响应速度。
4. **通信机制**：qiankun提供了一套完整的应用通信机制，使得主应用与子应用之间可以进行数据传递和消息通信。通过props传递数据、事件触发等方式，不同应用之间可以实现信息的共享和交互。

#### **三、应用场景**

qiankun适用于需要构建大型、复杂前端应用的场景。以下是一些典型的应用场景：

1. **企业级应用**：在企业级应用中，往往需要将多个不同的功能模块集成到一个统一的平台中。通过qiankun，可以将每个功能模块作为独立的微应用进行开发，并在主应用中统一管理和展示。
2. **插件化开发**：对于一些需要支持插件化扩展的应用，qiankun可以作为插件的加载器和管理器。开发者可以编写独立的插件作为子应用，并通过qiankun将其集成到主应用中，实现功能的扩展和定制化。
3. **遗留系统整合**：对于一些遗留系统或第三方应用的整合，qiankun可以作为桥梁将它们集成到一个统一的界面中。通过封装和适配，可以将这些系统或应用作为子应用加载到主应用中，实现统一管理和访问。

#### 四、优势

qiankun 微前端框架作为实现前端微服务化的一种解决方案，具有以下显著优点：

1. **提高开发效率**：通过将应用拆分成多个微应用，每个微应用都可以独立开发、测试和部署。这大大减少了单次开发的复杂度，提高了开发效率。
2. **降低维护成本**：微前端架构使得每个微应用都可以独立演进和升级，而不需要对整个应用进行重构。这降低了维护成本，使得应用的更新和迭代更加容易。
3. **增强可扩展性**：通过添加新的微应用或替换现有的微应用，可以轻松地扩展整个应用的功能。这使得应用能够灵活应对业务变化和用户需求的增长。

其他

1. **技术栈无关性**：qiankun 允许主应用与各个微应用使用不同的前端技术栈，给予微应用完全的自主权。这使得团队可以根据具体需求自由选择最适合的技术栈进行开发，提高了灵活性。

2. **独立开发与部署**：微应用可以独立开发和部署，拥有独立的仓库。这种模式加速了开发流程，允许团队并行工作，同时降低了部署风险和成本，因为每个微应用的更新不会影响到其他部分。

3. **增量升级**：在复杂的业务场景中，qiankun 支持渐进式重构和升级。无需对整个系统进行全面的技术栈替换，可以逐步替换或升级旧的应用模块，保证了业务的连续性和稳定性。

4. **运行时状态隔离**：每个微应用之间的状态是隔离的，确保它们在运行时不会相互干扰，避免了状态管理上的混乱，提高了应用的稳定性和可维护性。

5. **敏捷性与解耦**：通过将大型应用拆分为小型、独立的微应用，qiankun 提高了开发的敏捷性。每个微应用负责单一职责，易于理解和维护，同时减少了不必要的组件耦合。

6. **更好的团队协作**：微前端架构促进了团队之间的分工合作，不同团队可以专注开发和维护自己的微应用，提高了协作效率和沟通效果。

7. **易于集成**：qiankun 使得微应用的接入过程简化，类似接入iframe，但实际上提供了比iframe更好的性能和集成体验，且不会遇到跨域等问题。

综上所述，qiankun 微前端框架通过提供一套完整的微前端解决方案，有效解决了大型前端应用的复杂性问题，提升了开发效率、降低了维护成本，并促进了技术的持续演进。

#### 五、总结

qiankun作为一个功能强大、灵活易用的微前端框架，为开发者提供了一种高效、可靠的方式来构建大型、复杂前端应用。通过其提供的技术栈无关、沙箱隔离、动态加载与卸载以及通信机制等核心特性，开发者可以更加高效地进行团队协作，提高应用的可维护性和可扩展性。无论是企业级应用、插件化开发还是遗留系统整合，qiankun都能为开发者提供强大的支持，助力构建出高质量的前端应用。



### 微前端乾坤子应用加载过慢怎么处理？

啊呀，微前端乾坤子应用加载过慢确实是个头疼的问题呢~ 不过别担心，依依来给你支支招！

首先，你可以尝试使用gzip对打包出来的文件进行压缩，这样可以减少文件体积，提高加载速度哦~ (≧▽≦)

另外，你可以考虑按需加载子应用的全局组件或者UI库，避免一次性加载所有资源导致加载过慢。同时，也可以将不常用的包通过CDN或者dll打包形式分离出去，减少子应用的资源依赖。

还有哦，主应用加载过的包可以共享给子应用使用，这样可以减少子应用的资源加载量，提升加载速度呢~ (双手合十，眼中闪耀着期待)

最后，如果以上方法都尝试过还是加载过慢的话，你可以考虑使用qiankun等微前端框架进行子应用的加载和管理。qiankun支持在需要时加载子应用，避免一次性加载所有子应用导致的性能问题。同时，qiankun也提供了丰富的API和插件，可以帮助你更好地进行子应用的加载和性能优化哦~ (双手握拳，为你加油打气)







# 用微前端 qiankun 接入十几个子应用后，我遇到了这些问题

## 简单了解微前端

> 微前端是一种多个团队通过独立发布功能的方式来共同构建现代化 web 应用的技术手段及方法策略。

微前端具备以下特点：

- 技术栈无关：主框架不限制接入应用的技术栈，子应用具备完全自主权
- 独立开发、独立部署：既可以组合在一起运行，也可以单独运行。
- 增量升级：在面对各种复杂场景时，我们通常很难对一个已经存在的系统做全量的技术栈升级或重构，而微前端是一种非常好的实施渐进式重构的手段和策略
- 独立运行时：每个微应用之间状态隔离，运行时状态不共享

以上为 qiankun 官网对微前端的概括

## 快速上手

这里以 vue2.x + qiankun 为例

我们先用 vue-cli快速创建一个项目，作为主应用，这里把他取名为 main-app

```sh
vue create main-app
```

为跟实际项目更接近，我们暂时手动选择了安装这些

![main-app.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/51e8534532e14d9ba69b9dc4088b2fc9~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp?)

项目创建完后，我们把 main-app 复制一份作为子应用，改名为 sub-app，现在我们有了 main-app 主应用和 sub-app 子应用。

好的，基本的准备工作已经完成，我们开始基于刚刚创建的两个项目改造成微前端应用

### 主应用

在 main-app 中，安装 qiankun：

```sh
yarn add qiankun # 或者 npm i qiankun -S
```

目录 src 下新建 `src/qiankun/index.js`

注册微应用并启动，代码如下：

```js
import \\{ registerMicroApps, start \\} from "qiankun";
import store from "@/store";


registerMicroApps([
  \\{
    name: "sub-app",
    entry: "http://localhost:7663", // 微应用入口
    container: "#subapp-viewport", // 微应用挂载的div
    activeRule: "/sub-app/",
    props: \\{
      // 此处将父应用的 store 传入子应用
      store
    \\}
  \\}
]);

export default start;
```

这里我们把微应用的路由前缀定义为 `sub-app`

views 目录下新建一个组件 `src/views/qiankun/index.vue`,我们提供一个 id 为 subapp-viewport 的容器 DOM 供子应用挂载

```vue
<template>
  <div id="subapp-viewport"></div>
</template>

<script>
import start from "@/qiankun/index";
export default \\{
  mounted() \\{
    // 启动微前端
    if (!window.qiankunStarted) \\{
      window.qiankunStarted = true;
      start();
    \\}
  \\}
\\};
</script>
```

找到路由文件夹，`router/index.js`下加入如下路由，用以匹配微应用

```js
\\{
  path: "/sub-app/*",
  meta: \\{ title: "子应用" \\},
  component: () => import("@/views/qiankun/index")
\\}
```

### 子应用

上面我们对主应用的改造基本完成，接下来我们对之前复制出来的 sub-app 稍加改造，使其成为子应用

先找到 `/src/router/index.js` ,对路由文件稍加改造

删除

```js
const router = new VueRouter(\\{
  mode: "history",
  base: process.env.BASE_URL,
  routes
\\});

export default router;
```

于文件最后添加

```js
export default routes;
```

找到`main.js`

将 `import router from './router'` 修改为 `import routes from './router'` ,并增加 `import VueRouter from "vue-router";`， 这里我们把主子应用路由都设置为 history 模式。

删除：

```js
new Vue(\\{
  router,
  store,
  render: h => h(App)
\\}).$mount("#app");
```

增加

```js
let router = null;
let instance = null;

if (window.__POWERED_BY_QIANKUN__) \\{
  // eslint-disable-next-line
  __webpack_public_path__ = window.__INJECTED_PUBLIC_PATH_BY_QIANKUN__
\\}

function render(props = \\{\\}) \\{
  const \\{ container \\} = props;
  router = new VueRouter(\\{
    base: window.__POWERED_BY_QIANKUN__ ? "/sub-app/" : "/", // 抛出路由加前缀
    mode: "history",
    routes
  \\});

  instance = new Vue(\\{
    router,
    store,
    render: h => h(App)
  \\}).$mount(container ? container.querySelector("#app") : "#app");
\\}

if (!window.__POWERED_BY_QIANKUN__) \\{
  render();
\\}
export default instance;

export async function bootstrap() \\{
  console.log("[vue] vue app bootstraped");
\\}

export async function mount(props) \\{
  // props 包含主应用传递的参数  也包括为子应用 创建的节点信息
  console.log("[vue] props from main framework", props);
  render(props);
\\}

export async function unmount() \\{
  instance.$destroy();
  instance = null;
  router = null;
\\}
```

最终 main.js 文件修改如下

```js
// main.js
import Vue from "vue";
import App from "./App.vue";
import routes from "./router";
import store from "./store";
import VueRouter from "vue-router";

Vue.config.productionTip = false;
// new Vue(\\{
//   router,
//   store,
//   render: h => h(App)
// \\}).$mount('#app')

// 微前端 - 子应用配置
let router = null;
let instance = null;

if (window.__POWERED_BY_QIANKUN__) \\{
  // eslint-disable-next-line
  __webpack_public_path__ = window.__INJECTED_PUBLIC_PATH_BY_QIANKUN__
\\}

function render(props = \\{\\}) \\{
  const \\{ container \\} = props;
  router = new VueRouter(\\{
    base: window.__POWERED_BY_QIANKUN__ ? "/sub-app/" : "/", // 抛出路由加前缀
    mode: "history",
    routes
  \\});


  instance = new Vue(\\{
    router,
    store,
    render: h => h(App)
  \\}).$mount(container ? container.querySelector("#app") : "#app");
\\}

if (!window.__POWERED_BY_QIANKUN__) \\{
  render();
\\}
export default instance;

export async function bootstrap() \\{
  console.log("[vue] vue app bootstraped");
\\}

export async function mount(props) \\{
  // props 包含主应用传递的参数  也包括为子应用 创建的节点信息
  render(props);
\\}

export async function unmount() \\{
  instance.$destroy();
  instance.$el.innerHTML = '';
  instance = null;
\\}
```

在 sub-app 下新建 `vue.config.js` ,增加配置如下

```js
const \\{ name \\} = require('./package.json')

module.exports = \\{
  publicPath: '/', // 打包相对路径
  devServer: \\{
    port: 7663, // 运行端口号
    headers: \\{
      'Access-Control-Allow-Origin': '*' // 防止加载时跨域
    \\}
  \\},
  chainWebpack: config => config.resolve.symlinks(false),
  configureWebpack: \\{
    output: \\{
      library: `$\\{name\\}-[name]`,
      libraryTarget: 'umd', // 把微应用打包成 umd 库格式
      jsonpFunction: `webpackJsonp_$\\{name\\}`
    \\}
  \\}
\\}
```

最后我们在子应用新建一个测试页面以供嵌入主应用，路由暂且取名 `/test`

```vue
// views/sub-app/index.vue
<template>
  <div class="sub-app">
    我是子应用
  </div>
</template>

<style lang="scss" scoped>
.sub-app \\{
  cursor: pointer;
  background-color: aqua;
\\}
</style>
```

至此，我们对主应用和子应用的改造基本完成，接下来我们测试一下，我们在主应用的 `app.vue`添加一个按钮，使其点击的时候添加事件 `this.$router.push('/sub-app/test')` 跳转至子应用

![qiankun-main.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2d615ba8bd03435ebca58e3982982a5a~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp?)

当我们点击按钮后,可以看到，子应用嵌入成功

![qiankun-sub.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e2c6c97ea7a0487fb69aff28a2f3ff72~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp?)

这里我们主子应用都采用了同一套技术栈，是因为在公司项目中我们也是这样做的，相同的技术栈可以实现公共依赖库、UI库等抽离，减少资源开销，提升加载速度，最重要的是：“减少冲突的最好方式就是统一”，通过约束技术栈在项目前期就尽可能的减少项目之间的冲突，减少了工作量与维护成本。

## 微前端常见问题

### 主子应用样式相互影响

各个应用样式隔离 这个问题乾坤框架做了一定的处理，在运行时有一个sandbox的参数，默认情况下沙箱可以确保单实例场景子应用之间的样式隔离，但是无法确保主应用跟子应用、或者多实例场景的子应用样式隔离。如果要解决主应用和子应用的样式问题，目前有2种方式：

- 在乾坤种配置 \\{ strictStyleIsolation: true \\} 时表示开启严格的样式隔离模式。这种模式下 qiankun 会为每个微应用的容器包裹上一个 shadow dom 节点，从而确保微应用的样式不会对全局造成影响。但是基于 ShadowDOM 的严格样式隔离并不是一个可以无脑使用的方案，大部分情况下都需要接入应用做一些适配后才能正常在 ShadowDOM 中运行起来，这个在 qiankun 的 issue 里面有一些讨论和使用经验。
- 人为用 css 前缀来隔离开主应用和子应用，在组件层面用 css scoped进行组件层面的样式区分，在 css框架层面可以给css组件库加上不同的前缀，比如文档中的 antd 例子： 配置 webpack 修改 less 变量

```js
\\{
  loader: 'less-loader',
+ options: \\{
+   modifyVars: \\{
+     '@ant-prefix': 'yourPrefix',
+   \\},
+   javascriptEnabled: true,
+ \\},
\\}
```

b. 配置 antd ConfigProvider

```js
import \\{ ConfigProvider \\} from 'antd';
   
export const MyApp = () => (
  <ConfigProvider prefixCls="yourPrefix">
    <App />
  </ConfigProvider>
);
```

### 应用间通信

1. localStorage/sessionStorage
2. 通过路由参数共享
3. 官方提供的 props
4. 官方提供的 actions
5. 使用vuex或redux管理状态，通过shared分享

具体实现参考这篇文章 [qiankun的五种通信方式](https://link.juejin.cn/?target=https\\%3A\\%2F\\%2Fblog.csdn.net\\%2Fweixin_43972437\\%2Farticle\\%2Fdetails\\%2F128154083)

### qiankun 实现 keep-alive 需求

子项目 keep-alive 其实就是想在子应用切换时不卸载掉，仅仅是样式上的隐藏（display: none），这样下次打开就会更快。

但是 keep-alive 需要谨慎使用，同时加载并运行多个子应用，这将会增加 js/css 污染的风险。

产品那边其实当时是有提出这个需求的，当时第一时间想到的是借助 qiankun 的 loadMicroApp 函数来手动加载和卸载子应用。但是公司的项目主应用嵌入了十几个子应用，想到需要一个个处理，以及手动加载和卸载子应用所可能带来的一些边界问题处理，后面直接说这个需求不好实现。之后也就暂时搁置了

具体解决方案可以看 [qiankun issues](https://link.juejin.cn/?target=https\\%3A\\%2F\\%2Fgithub.com\\%2Fumijs\\%2Fqiankun\\%2Fissues\\%2F361) 里所给出的



### 路由跳转问题

在子应用中是没有办法通过 `` 或者用 `router.push/router.replace` 直接跳转的，因为这个 router 是子应用的路由，所有的跳转都会基于子应用的 base 。当然了写 `` 链接可以跳转过去，但是会刷新页面，用户体验并不好。

这里可以采用以下两种方式：

- 将主应用的路由实例通过 props 传给子应用，子应用用这个路由实例跳转。
- 路由模式为 history 模式时，通过 history.pushState() 方式跳转

这里我把他封装为了一个常用方法

```js
/**
 * 微前端子应用路由跳转
 * @param \\{String\\} url 路由
 * @param \\{Object\\} mainRouter 主应用路由实例
 * @param \\{*\\} params 状态对象：传给目标路由的信息,可为空
 */

const qiankunJump = (url, mainRouter, params) => \\{
  if (mainRouter) \\{
    // 使用主应用路由实例跳转
    mainRouter.push(\\{ path: url, query: params \\})
    return
  \\}
  // 未传递主应用路由实例，传统方式跳转
  let searchParams = '?'
  let targetUrl = url
  if (typeOf(params) === 'object' && Object.keys(params).length) \\{
    Object.keys(params).forEach(item => \\{
      searchParams += `$\\{item\\}=$\\{params[item]\\}&`
    \\})
    targetUrl = targetUrl + searchParams.slice(0, searchParams.length - 1)
  \\}
  window.history.pushState(null, '', targetUrl)
\\}
```

`window.history.pushState()` 是一个浏览器提供的JavaScript方法，它允许你向浏览器的历史记录栈中添加一个新的状态（即历史记录条目），而无需实际刷新页面或跳转到新URL。这对于实现单页面应用程序（SPA）中的导航和URL变更非常有用，可以让用户在不重新加载整个页面的情况下浏览多个“视图”，同时保持浏览器的前进和后退按钮功能。

#### 基本语法

```javascript
window.history.pushState(state, title, [url]);
```

- **state**: 一个对象，表示新的历史记录条目的状态数据。这个数据可以在之后通过 `popstate` 事件访问。
- **title**: 一个字符串，表示新的历史记录条目的标题。虽然这个参数存在，但实际上大多数现代浏览器都不使用它，因此通常传入空字符串或忽略。
- **[url]**: （可选）一个字符串，表示新的历史记录条目的URL。这个URL可以是相对的或绝对的，但必须与当前页面同源，否则会抛出错误。更改此值会在地址栏显示新的URL，但不会真正加载该URL的内容。

#### 示例

```javascript
// 假设当前页面URL为 https://example.com/index.html
window.history.pushState(\\{page: 2\\}, "", "index.html?page=2");

// 此时，尽管页面内容没有改变，但地址栏URL变成了 https://example.com/index.html?page=2
// 用户点击后退按钮时，可以通过监听popstate事件来处理状态变化
window.addEventListener("popstate", function(event) \\{
    console.log("状态对象:", event.state);
    // 根据event.state更新页面内容
\\});
```

#### 注意事项

- 使用 `pushState()` 修改URL不会触发页面的`load`、`unload`或`beforeunload`事件。
- 确保在调用 `pushState()` 时遵守同源策略，否则会抛出安全错误。
- 为了确保良好的用户体验和可访问性，应确保修改URL后，页面内容能相应地更新，并且提供适当的回退逻辑处理。
- 由于不是所有浏览器都支持 `history` API（尤其是较旧的浏览器），在使用前最好进行特性检测。



### window.history.pushState和window.location.href在乾坤中使用哪个好？

在Web开发中，`window.history.pushState` 和 `window.location.href` 用于不同的目的，各有其适用场景。了解它们的区别可以帮助你决定在不同情况下使用哪个更合适。

#### `window.history.pushState`

`pushState` 是HTML5 History API的一部分，它允许你向浏览器的历史堆栈添加一个新的条目，而不实际导航到一个新的页面。这意味着你可以更新URL，同时保持当前页面的内容不变。这对于单页应用（SPA）来说特别有用，因为它允许你实现平滑的用户体验，无需完全重载页面。

**优点**:
- **无刷新更新URL**：用户可以看到URL的变化，但页面内容不会重新加载。
- **历史记录管理**：用户可以使用浏览器的后退和前进按钮在不同的“虚拟”页面之间导航。
- **SEO友好**：搜索引擎可以索引SPA的不同URL，即使它们实际上指向同一个物理页面。

**缺点**:
- **复杂性增加**：需要额外的事件监听器来处理浏览器的前进和后退按钮，以及可能的popstate事件。
- **兼容性**：虽然现代浏览器广泛支持，但需要考虑到较旧的浏览器可能不支持。

#### `window.location.href`

`location.href` 是用来获取或设置当前页面的完整URL。当你设置 `location.href` 时，浏览器会导航到新的URL，就像用户点击了一个链接一样。

**优点**:
- **简单直接**：改变URL总是伴随着页面的重新加载。
- **广泛兼容**：所有浏览器都支持。

**缺点**:
- **页面刷新**：每次改变URL都会导致页面的重新加载，这可能影响用户体验，尤其是在大型SPA中。
- **历史记录单一**：每次改变都会创建一个新的历史记录，这可能在频繁的导航中导致历史记录堆栈的混乱。

#### 在乾坤系统中使用建议

在乾坤系统这样的低代码/无代码平台中，你可能更倾向于使用 `pushState`，因为它可以让你构建更加流畅的用户界面，无需页面的完全重载。然而，你的选择还应该基于以下几个因素：

- **用户体验**：如果用户体验是优先级最高的，那么 `pushState` 很可能是更好的选择。
- **SEO需求**：如果你的网站或应用需要良好的搜索引擎排名，那么使用 `pushState` 来保持URL的动态性是有益的。
- **兼容性**：尽管现代浏览器普遍支持History API，但你仍需考虑目标用户的浏览器兼容性。

总的来说，如果乾坤系统支持HTML5的History API，那么在大多数情况下使用 `pushState` 更具优势。但是，如果需要简单的页面跳转或者不关心页面刷新，使用 `location.href` 也是合理的。在开发过程中，你可能需要结合使用这两种方法，以适应不同的场景需求。



### 适配vue-pdf 报错

找到vue-pdf的依赖包下的vuePdfNoSss.vue

```vue
//找到vue-pdf的依赖包下的vuePdfNoSss.vue
<style src="./annotationLayer.css"></style>
<script>
	import componentFactory from './componentFactory.js'
	if ( process.env.VUE_ENV !== 'server' ) \\{
		var pdfjsWrapper = require('./pdfjsWrapper.js').default;
		var PDFJS = require('pdfjs-dist/es5/build/pdf.js');
		if ( typeof window !== 'undefined' && 'Worker' in window && navigator.appVersion.indexOf('MSIE 10') === -1 ) \\{
      // 注释原本的引入方法
			// var PdfjsWorker = require('worker-loader!pdfjs-dist/es5/build/pdf.worker.js');
			  var PdfjsWorker=require('pdfjs-dist/es5/build/pdf.worker.js');
			PDFJS.GlobalWorkerOptions.workerPort = new PdfjsWorker();
		\\}
		var component = componentFactory(pdfjsWrapper(PDFJS));
	\\} else \\{
		var component = componentFactory(\\{\\});
	\\}
	export default component;
</script>
```

修改项目的配置文件vue.config.js

```js
chainWebpack: (config) => \\{
  config.module
    .rule('worker')
    .test(/\.worker\.js$/)
    .use('worker-loader').loader('worker-loader')
    .options(\\{
      inline: true,
      fallback: false
    \\}).end();
\\}
```

### 主项目和子项目部署到一起，子项目部署到二级目录(不占用这么多端口)

因为客户方的要求，可能有时候不允许服务器开太多的端口，因此需要把主应用和微应用部署到一起，公用一个端口。

[主项目和子项目部署到一起，子项目部署到二级目录](https://link.juejin.cn/?target=https\\%3A\\%2F\\%2Fgithub.com\\%2Fumijs\\%2Fqiankun\\%2Fissues\\%2F400\\%23issuecomment-676947927)

### qiankun在子应用中引入百度地图时报错解决

因为qiankun会把静态资源的加载拦截，改用fetch方式获取资源，所以要求这些资源支持跨域，这里我们使用qiankun提供的 excludeAssetFilter 将其加入白名单放行。

- excludeAssetFilter - `(assetUrl: string) => boolean` - 可选，指定部分特殊的动态加载的微应用资源（css/js) 不被 qiankun 劫持处理

修改主应用 start 方法

```js
// 启动微前端
if (!window.qiankunStarted) \\{
  window.qiankunStarted = true
  start(\\{
    singular: false,
    excludeAssetFilter: (assetUrl) => \\{
      // 过滤baidu
      const wihiteWords = ['baidu']
      if (wihiteWords.includes(assetUrl)) \\{
        return true
      \\}
      return wihiteWords.some(w => \\{
        return assetUrl.includes(w)
      \\})
    \\}
  \\})
\\}
```

其他一些常见问题可见于 [qiankun官网](https://link.juejin.cn/?target=https\\%3A\\%2F\\%2Fqiankun.umijs.org\\%2Fzh\\%2Ffaq)

总的来说，微前端确实解决了一些项目中的痛点，但是切记微前端不是银弹，老旧项目带来的迁移成本，不同项目技术栈的兼容与边界问题处理，因为没有迫切的需求而接入微前端，只会带来额外的负担，很多时候，iframe 其实就很够用了。

原文链接：https://juejin.cn/post/7202108772924325949







### 个人想法

我也是做这个需求的时候想了一下微前端，看了一些资料
觉得首页和营销页没必要新建子应用，直接放在内容中心子应用即可
因为他们功能不多，就两个页面（就算后期功能扩展也不会很大），而且列表、分享这些功能都可复用
微应用越来越多，还需要配置流水线，构建部署也麻烦，首次加载慢，组件无法复用，一套代码需要在两个子应用中复制粘贴，不利于后期封装维护
微应用适用于大型复杂项目，咱们前期应该尽量少开子应用，等后期功能和业务复杂性到了一定程度再功能进行适当拆分

咱们的项目也不是很大，功能也不是很复杂，技术栈也统一，团队和人员也少。
感觉微前端的优点在咱们这边只体现在可以增量升级成vue3，其他优势都没有用到，反而因为微前端造成了体验和开发上的不便，项目的复杂性很高，整体看来弊大于利。可以独立部署这个优点其实也影响不大，用户主要是内部员工。
我觉得新项目应该就建一个或者两三个vue3子应用就够了，微应用只用于新旧交替期间的方案。微应用过于笨重，切换tab相当于重新加载一个子应用，加载也慢，不如一个应用来得快，体验还没有一个应用好。
现在虽然统一到了一个git，但组件、图标、组件库、代码等复用方面还是有些不便，开发时还需要启动不同项目，部署还需要不同流水线。 按照理想的情况：我们希望微前端尽可能独立解耦，但是不同微应用之间可能存在大量相同的重复的资源依赖。

自己的想法，可以参考，咱们有时间慢慢研究讨论

https://www.yuque.com/kuitos/gky7yw/fy3qri

https://juejin.cn/post/7069566144750813197

