---
title: qiankun项目搭建
date: 2024-04-28 10:02:08
categories: 
- 前端知识
tags:
- qiankun
- vue
---

### 基座配置

> 基座采用是的 Vue3 + vite + ts，只负责导航的渲染和登录态的下发，为子应用提供一个挂载的容器div
>
> qiankun这个库只需要在基座引入

```
npm i qiankun
```

在main.ts 中注册子应用，为了方便管理，我们将子应用的配置都放在：/utils/qiankun.ts下 

```
import \\{ registerMicroApps, addGlobalUncaughtErrorHandler, start \\} from 'qiankun';
import router from './router'
// 注册子应用
registerMicroApps([
  \\{
    // 子应用名称，name值必须与子应用vite.config.ts文件中plugins属性qiankun的第一个参数值一致
    name: 'subApp',
    // 默认会加载这个路径下的html，解析里面的js
    entry: '//localhost:5050/',
    // 加载的容器（微应用会显示到这个容器里面，一定要保证主应用中有这个容器）
    container: '#subAppContainerVue3',  // 和app.vue配置的节点一致
    // 匹配的路由
    activeRule: '/gosubsystem', // 访问：http://localhost:5174/juminronghe
    props: \\{
        mag: '我是主应用main', // 主应用向微应用传递参数
    \\},
  \\},
  \\{
    // 子应用名称，name值必须与子应用vite.config.ts文件中plugins属性qiankun的第一个参数值一致
    name: 'lmsApp',
    // 默认会加载这个路径下的html，解析里面的js
    entry: '//localhost:5000/',
    // 加载的容器（微应用会显示到这个容器里面，一定要保证主应用中有这个容器）
    container: '#subAppContainerVue3',  // 和app.vue配置的节点一致
    // 匹配的路由
    activeRule: '/lmsApp', 
    props: \\{
        mag: '我是主应用main', // 主应用向微应用传递参数
        router    // 主路由下发到子路由，子应用路由跳转使用主应用路由实例跳转（需要跳转的路由要在主应用里注册）
    \\},
  \\}
],
\\{
  beforeLoad: app => \\{
    console.log('before load app.name====>>>>>', app.name)
  \\},
  beforeMount: [
    app => \\{
      console.log('[LifeCycle] before mount \\%c\\%s', 'color: green;', app.name);
    \\},
  ],
  afterMount: [
    app => \\{
      console.log('[LifeCycle] after mount \\%c\\%s', 'color: green;', app.name);
    \\}
  ],
  afterUnmount: [
    app => \\{
      console.log('[LifeCycle] after unmount \\%c\\%s', 'color: green;', app.name);
    \\},
  ],
\\});
// 启动 qiankun
// start(\\{
//     prefetch:'all', // 预加载
//     sandbox: \\{
//         experimentalStyleIsolation: true, //   开启沙箱模式,实验性方案
//     \\},
// \\});
// 添加全局异常捕获
addGlobalUncaughtErrorHandler((event) => \\{
  // console.error(event);
  const \\{ message: msg \\} = event;
  // 加载失败时提示
  if (msg && msg.includes("died in status LOADING_SOURCE_CODE")) \\{
    // message.error("微应用加载失败，请检查应用是否可运行");
    console.log("微应用加载失败，请检查应用是否可运行-乾坤插件是否正常")
  \\}
\\});
```

然后在src/main.ts中引入 

```
import './utils/qiankun.ts'
```



### 如何在主应用的某个路由页面加载微应用

> 必须保证微应用加载时主应用这个路由页面也加载了
> 主应用注册这个路由时给 path 加一个 *，注意：如果这个路由有其他子路由，需要另外注册一个路由，仍然使用这个组件即可

```
 \\{
    path: '/portal/*',
    name: 'portal',
    component: () => import('../views/Portal.vue'),
  \\},
```

Portal.vue

```
<template>
 <div id="subAppContainerVue3"></div>
</template>
  
<script lang="ts" setup  name="merchantsRuquest">
// import start from "@/qiankun/index.js";
import \\{ start \\} from 'qiankun'
// import \\{ registerApps \\} from '@/qiankun/index.js'
onMounted(()=>\\{
    if (!window.qiankunStarted) \\{
            window.qiankunStarted = true
            // registerApps()
            start(\\{
                sandbox: \\{
                    experimentalStyleIsolation: true // 样式隔离
                \\}
            \\})
        \\}
\\})
// export default \\{
//     mounted() \\{
      
//     \\}
// \\}
</script>
```



### 主应用路由配置

```
 \\{
          path: '/lmsApp/*',   // 注意和registerMicroApps 注册子应用的activeRule匹配
          name: 'lmsApp',
          meta: \\{
            title: "子应用菜单管理",
            icon: "car-outlined",
            isFull: false,
            isKeepAlive: true,
            isHide: false
          \\},
          children: [
            \\{
              name: 'xxxxx',
              path: '/lmsApp/xxxx/xxxxx',
              component: () => import('@/views/portal.vue'),
              meta: \\{
                title: '子应用菜单下的二级菜单',
                icon: '',
                isKeepAlive: false
              \\}
            \\},
           
          ]
        \\},
```

> 这样，基座就算配置完成了。项目启动后，子应用将会挂载到主应用中



### 子应用配置

> 安装vite-plugin-qiankun

```
npm i vite-plugin-qiankun --save-dev
或者
yarn add vite-plugin-qiankun --dev
```

修改vite.config.ts

```
// 引入乾坤插件
import qiankun from 'vite-plugin-qiankun'
plugins: [ vue(), qiankun('subApp', \\{ useDevMode: true \\}) ], 
```

在子应用main.ts 里引用qiankun

```
import \\{
  renderWithQiankun,
  qiankunWindow,
  type QiankunProps
\\} from 'vite-plugin-qiankun/dist/helper'
let app: any

const render = (container?: any, routers?: any) => \\{
  app = createApp(App)
  Object.keys(Icons).forEach((key) => \\{
    app.component(key, Icons[key as keyof typeof Icons])
  \\})
  app.use(pinia)
  app.use(print)
  app.use(Antd)
  app.use(directives)
  app.config.globalProperties.$routers = routers
  app.use(router).mount(container ? container.querySelector('#app') : '#app')
\\}

const initQianKun = () => \\{
  renderWithQiankun(\\{
    mount(props) \\{
      // localStorage.lalal = 111111
      console.log(props.router, '获取主应用传递数据')
      sessionStorage.latoutStatus = false
      const \\{ container, router \\} = props

      render(container, router)
    \\},
    bootstrap() \\{ \\},
    unmount() \\{
      app.unmount()
    \\},
    update: function (props: QiankunProps): void | Promise<void> \\{
      throw new Error('Function not implemented.')
    \\}
  \\})
\\}
// console.log(qiankunWindow.__POWERED_BY_QIANKUN__, '90')
qiankunWindow.__POWERED_BY_QIANKUN__ ? initQianKun() : render()
```

由于路由模式为history，需要匹配子应用的入口规则，修改src/router/index 

```
import \\{ qiankunWindow \\} from 'vite-plugin-qiankun/dist/helper'
const router = createRouter(\\{
  history: createWebHistory(
    qiankunWindow.__POWERED_BY_QIANKUN__
      ? '/lmsApp/'
      : '/'
  ),
  routes
\\})
```

#### 报错There is already an app instance mounted on the host container. 

因为是vue应用，子应用也有个id="app"

全局搜索\#app，改成\#app1



### qiankun运行逻辑

将主应用与子应用都运行起来后，由于主应用的main.js配置了registerMicroApps这个，里面是个数组，数组中一个对象代码一个子应用， name不太重要，运行逻辑如下：当在浏览器地址栏输入主应用的对应路由地址，主应用发现与activeRule的路由匹配上之后，会将此activeRule下的entry下跑的子应用界面渲染到container容器里（此容器我们之前写在了App.vue）
简单点说就是
主应用监听发现路由地址变化 （例如地址最后输入/son1）
主应用从main.js 的 registerMicroApps之中寻找对应匹配的规则地址
将此条规则的entry（这里填写的就是子应用目前跑在的地址），渲染到 container 下的容器里

原文链接：https://blog.csdn.net/weixin_45653441/article/details/134877301