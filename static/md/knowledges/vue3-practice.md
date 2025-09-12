---
title: vue3实践
date: 2024-03-09 00:02:08
categories: 
- 前端知识
tags:
- vue3
---

# 自定义Hooks

**简介：** 自定义 Hooks 在 Vue3 中的应用和重要性

👀 你有没有遇到过这样的问题：在不同的组件中重复编写相似的逻辑？是否觉得维护这些代码既费时又乏味？

**如果你的回答是肯定的，那么自定义Hooks无疑是你的救星！**

![img](https://ucc.alicdn.com/pic/developer-ecology/tib3bzkxpvagq_0f7db4216dcf4eafa8b19a4d89baaeff.png?x-oss-process=image\\%2Fresize\\%2Cw_1400\\%2Fformat\\%2Cwebp)



## 概述

自定义Hooks是Vue3提供的一种将可复用逻辑提取到独立函数中的方式。这不仅可以减少代码的重复，还能让你的代码更加清晰易读，维护起来也更加方便。

在这篇文章中，我将通过详细的步骤和实例，带你深入了解如何在Vue3中使用自定义Hooks，以及它们在实际项目中的应用和重要性。



## 应用场景

### 1. 状态管理

在大型应用中，状态管理无疑是一个重要的部分。尽管Vuex可以解决很多问题，但有时候我们只需要在局部组件中共享一些状态。这时候，自定义Hooks就派上了用场。

### 2. 业务逻辑复用

有些业务逻辑可能会在多个组件中重复使用，比如表单校验、数据获取等。通过自定义Hooks，我们可以将这些逻辑提取出来，避免重复代码。

### 3. 生命周期管理

Vue3引入了组合式API，使得我们可以更灵活地管理组件的生命周期。自定义Hooks让我们可以将与生命周期相关的逻辑独立出来，更加模块化和可复用。



## 重要性

### 提高代码复用性

通过将通用逻辑提取到自定义Hooks中，我们可以在多个组件中复用这些逻辑，极大地减少代码重复。

### 增强代码可读性

将复杂的逻辑封装到Hooks中，使得组件代码更加简洁，逻辑更加清晰，提升代码的可读性。

### 方便测试

自定义Hooks将逻辑独立出来，便于单独测试这些逻辑，提高测试的覆盖率和代码的可靠性。

### 模块化开发

通过Hooks将逻辑模块化，使得开发过程更加清晰，易于维护和扩展。



## 使用方法

### 创建自定义Hook

首先，我们来看一下如何创建一个简单的自定义Hook。在Vue3中，自定义Hook本质上就是一个返回特定功能的函数。让我们从一个简单的计数器例子开始。

```
// useCounter.js
import \\{ ref \\} from'vue';
export function useCounter()\\{
const count =ref(0);
const increment=()=>\\{
    count.value++;
\\};
const decrement=()=>\\{
    count.value--;
\\};
return\\{
    count,
    increment,
    decrement
\\};
\\}
```

这个 `useCounter` Hook 提供了一个计数器功能，包含了 `count` 状态和 `increment`、`decrement` 方法。

### 使用自定义Hook

接下来，我们在组件中使用这个自定义Hook。

```
<template>
  <div>
    <p>Count: \\\{\\\{ count\\\}\\\} }}</p>
    <button @click="increment">Increment</button>
    <button @click="decrement">Decrement</button>
  </div>
</template>
<script setup>
import \\{ useCounter \\} from './useCounter';
const \\{ count, increment, decrement \\} = useCounter();
</script>
```

通过这种方式，我们可以在多个组件中使用相同的计数器逻辑，而无需重复代码。

### 高级用法：组合多个Hooks

有时候，我们需要组合多个Hooks来实现更复杂的功能。比如，我们可以创建一个 `useFetch` Hook 来处理数据获取，然后将其与 `useCounter` 组合起来。

```
// useFetch.js
import\\{ ref \\}from'vue';
export function useFetch(url)\\{
const data =ref(null);
const error =ref(null);
const fetchData=async()=>\\{
try\\{
const response =await fetch(url);
      data.value=await response.json();
\\}catch(err)\\{
      error.value= err;
\\}
\\};
return\\{
    data,
    error,
    fetchData
\\};
\\}
<template>
  <div>
    <p>Count:\\\{\\\{ count\\\}\\\} }}</p>
<button @click="increment">Increment</button>
<button @click="decrement">Decrement</button>
<button @click="fetchData">FetchData</button>
<pre v-if="data">\\\{\\\{ data\\\}\\\} }}</pre>
<p v-if="error">Error:\\\{\\\{ error\\\}\\\} }}</p>
  </div>
</template>
<script setup>
import \\{ useCounter \\}from'./useCounter';
import\\{ useFetch \\}from'./useFetch';
const\\{ count, increment, decrement \\}=useCounter();
const\\{ data, error, fetchData \\}=useFetch('https://api.example.com/data');
</script>
```

通过这种组合方式，我们可以轻松地将不同的逻辑模块化并复用。



## 实践案例

### 案例一：表单校验

表单校验是前端开发中非常常见的需求。我们可以创建一个 `useFormValidation` Hook 来简化表单校验逻辑。

```
// useFormValidation.js
import \\{ ref \\} from 'vue';
export function useFormValidation()\\{
const errors =ref(\\{\\});
const validate=(field, value)=>\\{
if(field ==='email')\\{
      errors.value.email=!/^\S+@\S+\.\S+$/.test(value)?'Invalid email':'';
\\}elseif(field ==='password')\\{
      errors.value.password= value.length<6?'Password too short':'';
\\}
\\};
return\\{
    errors,
    validate
\\};
\\}
<template>
  <form @submit.prevent="submit">
    <div>
<label for="email">Email:</label>
<input id="email" v-model="email" @blur="validate('email', email)" />
<p v-if="errors.email">\\\{\\\{ errors.email\\\}\\\} }}</p>
</div>
<div>
<label for="password">Password:</label>
<input id="password" type="password" v-model="password" @blur="validate('password', password)" />
<p v-if="errors.password">\\\{\\\{ errors.password\\\}\\\} }}</p>
</div>
<button type="submit">Submit</button>
  </form>
</template>
<script setup>
import \\{ ref \\} from 'vue';
import \\{ useFormValidation \\} from'./useFormValidation';
const email =ref('');
const password =ref('');
const \\{ errors, validate \\}=useFormValidation();
const submit=()=>\\{
validate('email', email.value);
validate('password', password.value);
if(!errors.value.email&&!errors.value.password)\\{
// 表单提交逻辑
\\}
\\};
</script>
```

### 案例二：响应式数据获取

在大型应用中，响应式数据获取是非常常见的需求。我们可以创建一个 `useReactiveFetch` Hook 来处理这个需求。

```
// useReactiveFetch.js
import\\{ ref, watch \\}from'vue';
export function useReactiveFetch(url)\\{
const data =ref(null);
const error =ref(null);
const fetchData=async()=>\\{
try\\{
const response =await fetch(url.value);
      data.value=await response.json();
\\}catch(err)\\{
      error.value= err;
\\}
\\};
watch(url, fetchData);
return\\{
    data,
    error
\\};
\\}
<template>
  <div>
    <input v-model="url" placeholder="Enter URL" />
    <pre v-if="data">\\\{\\\{ data\\\}\\\} }}</pre>
    <p v-if="error">Error: \\\{\\\{ error\\\}\\\} }}</p>
  </div>
</template>
<script setup>
import \\{ ref \\} from 'vue';
import\\{ useReactiveFetch \\}from'./useReactiveFetch';
const url =ref('https://api.example.com/data');
const \\{ data, error \\}=useReactiveFetch(url);
</script>
```



## 总结

自定义Hooks不仅提高了代码的复用性和可读性，还增强了代码的模块化和可维护性。

原文链接：https://developer.aliyun.com/article/1581003







# vite + vue3 + setup + pinia + ts 项目实战

## 介绍

一个使用 vite + vue3 + pinia + ant-design-vue + typescript 完整技术路线开发的项目，秒级开发更新启动、新的vue3 composition api 结合 setup纵享丝滑般的开发体验、全新的 pinia状态管理器和优秀的设计体验（1k的size）、antd无障碍过渡使用UI组件库 ant-design-vue、安全高效的 typescript类型支持、代码规范验证、多级别的权限管理~



## 前言

前两天接到了一个需求，就是把原来的一个项目的主要功能模块和用户模块权限系统抽出来做一个新后台项目，并迭代新增一些新功能，看起来好像也没啥东西

拿到源码看了下项目，好家伙，原项目是个微应用项目，主应用用户模块是react技术栈，子应用模块是vue2技术栈，这直接 CV大法看样子是不行了👀，我这要做的毕竟是个单页面应用，确定一个技术路线即可，具体看下代码逻辑并跑起来看看

跑起来试了下，两个项目基本都是1分钟左右启动，看代码vue项目整个业务逻辑代码都拧在一块写了

想到之前问老大要源码的时候，说那个是老项目了，重新搭一个写应该会快点

这话没毛病啊，话不多说，直接开整，这次直接上 vite + vue3



## 特性

✨脚手架工具：高效、快速的 Vite
🔥前端框架：眼下最时髦的 Vue3
🍍状态管理器：vue3新秀 Pinia，犹如 react zustand般的体验，友好的api和异步处理
🏆开发语言：政治正确 TypeScript
🎉UI组件：antd开发者无障碍过渡使用 ant-design-vue，熟悉的配方熟悉的味道
🎨css样式：less 、postcss
📖代码规范：Eslint、Prettier、Commitlint
🔒权限管理：页面级、菜单级、按钮级、接口级
✊依赖按需加载：unplugin-auto-import，可自动导入使用到的vue、vue-router等依赖
💪组件按需导入：unplugin-vue-components，无论是第三方UI组件还是自定义组件都可实现自动按需导入以及TS语法提示



## 项目目录

```
├── .husky                              // husky git hooks配置目录
    ├── _                               // husky 脚本生成的目录文件
    ├── commit-msg                      // commit-msg钩子，用于验证 message格式
    ├── pre-commit                      // pre-commit钩子，主要是和eslint配合
├── config                              // 全局配置文件
    ├── vite                            // vite 相关配置
    ├── constant.ts                     // 项目配置
    ├── themeConfig.ts                  // 主题配置
├── dist                                // 默认的 build 输出目录
├── mock                                // 前端数据mock
├── public                              // vite项目下的静态目录
└── src                                 // 源码目录
    ├── api                             // 接口相关
    ├── assets                          // 公共的文件（如image、css、font等）
    ├── components                      // 项目组件
    ├── directives                      // 自定义 指令
    ├── enums                           // 自定义 常量（枚举写法）
    ├── hooks                           // 自定义 hooks
    ├── layout                          // 全局布局
    ├── router                          // 路由
    ├── store                           // 状态管理器
    ├── utils                           // 工具库
    ├── views                           // 页面模块目录
        ├── login                       // login页面模块
        ├── ...
    ├── App.vue                         // vue顶层文件
    ├── auto-imports.d.ts               // unplugin-auto-import 插件生成
    ├── components.d.d.ts               // unplugin-vue-components 插件生成
    ├── main.ts                         // 项目入口文件
    ├── shimes-vue.d.ts                 // vite默认ts类型文件
    ├── types                           // 项目type类型定义文件夹
├── .editorconfig                       // IDE格式规范
├── .env                                // 环境变量
├── .eslintignore                       // eslint忽略
├── .eslintrc                           // eslint配置文件
├── .gitignore                          // git忽略
├── .npmrc                              // npm配置文件
├── .prettierignore                     // prettierc忽略
├── .prettierrc                         // prettierc配置文件
├── index.html                          // 入口文件
├── LICENSE.md                          // LICENSE
├── package.json                        // package
├── pnpm-lock.yaml                      // pnpm-lock
├── postcss.config.js                   // postcss
├── README.md                           // README
├── tsconfig.json                       // typescript配置文件
└── vite.config.ts                      // vite
```



## 开发

### 项目初始化

如果使用vscode编辑器开发vue3，请务必安装Volar插件与vue3配合使用更佳（与原本的Vetur不兼容）

开发
项目初始化
如果使用vscode编辑器开发vue3，请务必安装Volar插件与vue3配合使用更佳（与原本的Vetur不兼容）

使用 vite cli 快速创建项目

```
yarn create vite project-name --template vue-ts
```

### 安装相关依赖

推荐使用新一代 pnpm 包管理工具，性能和速度以及 node_modules依赖管理都很优秀

建议配合 .npmrc 配置使用

```
# 提升一些依赖包至 node_modules
# 解决部分包模块not found的问题
# 用于配合 pnpm
shamefully-hoist = true

# node-sass 下载问题
# sass_binary_site="https://npm.taobao.org/mirrors/node-sass/"
```

### 代码规范

工具：husky、eslint、prettier

具体使用方式，网上很多，我在之前另一篇文章也有说过，这里不再赘述~

[a Vite2 + Typescript + React + Antd + Less + Eslint + Prettier + Precommit template](https://juejin.cn/post/6986169708722520072)

主要就是自动化的概念，在一个合适的时机完成规定的事

- 结合VsCode编辑器（保存时自动执行格式化：editor.formatOnSave: true）
- 配合Git hooks钩子（commit前或提交前执行：pre-commit => npm run lint:lint-staged）

注意：针对不同系统 commitlint安装方式有所不同 commitlint，安装错误可能会无效哦~

```
# Install commitlint cli and conventional config
npm install --save-dev @commitlint/\\{config-conventional,cli\\}
# For Windows:
npm install --save-dev @commitlint/config-conventional @commitlint/cli
```



## 功能

### vue能力支持

模板语法配合jsx语法，使用起来非常方便、灵活~

一些必须的插件

```
\\{
    // "@vitejs/plugin-legacy": "^1.6.2", // 低版本浏览器兼容
    "@vitejs/plugin-vue": "^1.9.3", // vue 支持
    "@vitejs/plugin-vue-jsx": "^1.2.0", // jsx 支持
\\}
```



### 状态管理器 Pinia

vue新一代状态管理器，用过 react zustand的同学应该会有很熟悉的感觉

状态管理器 Pinia
vue新一代状态管理器，用过 react zustand的同学应该会有很熟悉的感觉

> Pinia是一个围绕Vue 3 Composition API的封装器。因此，你不必把它作为一个插件来初始化，除非你需要Vue devtools支持、SSR支持和webpack代码分割的情况
>

- 非常轻量化，仅有 1 KB
- 直观的API使用，符合直觉，易于学习
- 模块化设计，便于拆分状态
- 全面的TS支持

```
// ... 引入相关依赖

interface IUserInfoProps\\{
  name: string;
  avatar: string;
  mobile: number;
  auths: string[]
\\}

interface UserState \\{
  userInfo: Nullable<IUserInfoProps>;
\\}

// 创建 store
export const useUserStore = defineStore(\\{
  id: 'app-user', // 唯一 ID，可以配合 Vue devtools 使用
  state: (): UserState => (\\{
    // userInfo
    userInfo: null,
  \\}),
  getters: \\{
    getUserInfo(): Nullable<IUserInfoProps> \\{
      return this.userInfo || null;
    \\},
  \\},
  actions: \\{
    setUserInfo(info: Nullable<IUserInfoProps>) \\{
      this.userInfo = info ?? null;
    \\},
    resetState() \\{
      this.userInfo = null;
    \\},

    /**
     * @description: fetchUserInfo
     */
    async fetchUserInfo(params: ReqParams) \\{
      const res = await fetchApi.userInfo(params);
      if (res) \\{
        this.setUserInfo(res);
      \\}
    \\},
  \\},
\\})
```

组件中使用

```
// TS 类型推断、异步函数使用都很方便
import \\{ useHomeStore \\} from '/@/store/modules/home';

const store = useHomeStore();
const userInfo = computed(() => store.getUserInfo);

onMounted(async () => \\{
  await store.fetchInfo(); // 异步函数
  // ...
\\});
```



### UI组件按需加载、自动导入

了解基本概念：vite 自带按需加载（针对js），我们这里主要针对样式做按需加载处理

UI组件按需加载、自动导入
了解基本概念：vite 自带按需加载（针对js），我们这里主要针对样式做按需加载处理

#### 方案一：vite-plugin-style-import

```
import styleImport from 'vite-plugin-style-import'

// 
plugins:[
  styleImport(\\{
    libs: [
      \\{
        libraryName: 'ant-design-vue',
        esModule: true,
        resolveStyle: (name) => \\{
          return `ant-design-vue/es/$\\{name\\}/style/index`
        \\},
      \\}
    ]
  \\})
]
```

#### 方案二：unplugin-vue-components

推荐使用 [unplugin-vue-components](https://github.com/antfu/unplugin-vue-components) 插件

方案二：unplugin-vue-components
推荐使用 unplugin-vue-components 插件

该插件只需在 vite plugin中添加对应 AntDesignVueResolver 即可，也支持自定义的 components 自动注册，很方便

```
import \\{ AntDesignVueResolver \\} from 'unplugin-vue-components/resolvers';
import Components from 'unplugin-vue-components/vite';

// vite.config.ts plugins 添加如下配置
export default defineConfig(\\{
  plugins: [
    Components(\\{
      resolvers: [
        AntDesignVueResolver(), // ant-design-vue
        // ElementPlusResolver(), // Element Plus
        // VantResolver(), // Vant
      ]
    \\})
  ]
\\})
```

当然这里如果没有你使用的对应的UI框架的 Resolver加载器，也没关系，也支持自定义配置

当然这里如果没有你使用的对应的UI框架的 Resolver加载器，也没关系，也支持自定义配置

```
Components(\\{
  resolvers: [
    // example of importing Vant
    (name) => \\{
      // where `name` is always CapitalCase
      if (name.startsWith('Van'))
        return \\{ importName: name.slice(3), path: 'vant' \\}
    \\}
  ]
\\})
```

另一强悍功能：该插件不仅支持UI框架组件的按需导入，也支持项目组件的自动按需导入

另一强悍功能：该插件不仅支持UI框架组件的按需导入，也支持项目组件的自动按需导入

> 具体表现就是：如我们使用 ant-design-vue的 Card组件或我们自己定义的 components/Icon 等其他组件时，我们不用导入，直接用即可，插件会为我们自动按需导入，结合 TS语法提示，开发效率杠杠的~
>

配置如下:

```
Components(\\{
  // allow auto load markdown components under `./src/components/`
  extensions: ['vue'],

  // allow auto import and register components
  include: [/\.vue$/, /\.vue\?vue/],

  dts: 'src/components.d.ts',
\\})
```

需要在src目录下添加 components.d.ts文件配合使用，该文件会被插件自动更新

需要在src目录下添加 components.d.ts文件配合使用，该文件会被插件自动更新

###### components.d.ts 作用

直接的作用是：在项目下生成对应.d.tstype类型文件，用于语法提示与类型检测通过

注意

```
"unplugin-vue-components": "^0.17.2"
```

###### 当前版本已知问题：[issues 174](https://github.com/antfu/unplugin-vue-components/issues/174)

对于 ant-design-vue 的 notification / message 组件，当在 js中使用时，该插件不会执行自动导入能力（样式不会被导入）

最终效果是：message.success('xx')可以创建 DOM元素，但是没有相关样式代码

因为该插件的设计原理是根据 vue template 模板中的组件使用进行处理的，函数式调用时插件查询不到

解决方案：

- 改用vite-plugin-style-import 插件
- 手动全局引入 message组件样式，import 'ant-design-vue/es/message/style'
- 在vue组件的 template中手动添加 <a-message /> 供插件索引依赖时使用



### 依赖按需自动导入

unplugin-auto-import
vue相关 defineComponent 、computed 、watch等模块依赖根据使用，插件自动导入，你无需关心 import，直接使用即可

该插件默认支持：

- vue
- vue-router
- vue-i18n
- @vueuse/head
- @vueuse/core
- …

当然你也可以自定义配置 [unplugin-auto-import](https://github.com/antfu/unplugin-auto-import#readme)

用法如下：

```
import AutoImport from 'unplugin-auto-import/vite'

export default defineConfig(\\{
  // ...
  plugins: [
    AutoImport(\\{
      imports: [
        'vue',
        'vue-router',
        'vue-i18n',
        '@vueuse/head',
        '@vueuse/core',
      ],
      dts: 'src/auto-imports.d.ts',
    \\})
  ]
\\})
```

需要在src目录下添加 auto-imports.d.ts文件配合使用，该文件会被插件自动更新

需要在src目录下添加 auto-imports.d.ts文件配合使用，该文件会被插件自动更新

最终效果为：

如 ref方法我们可以直接使用并有相应的TS语法提示，而不需要手动的去 import \\{ ref \\} from 'vue'



### 自定义主题

自定义主题设置参考官方文档配置即可，两种常规方式

1. 按需加载配合 webpack/vite loader属性修改变量
2. 全量引入，配合 variables.less自定义样式覆盖框架主题样式

这里我们采用第一种方法通过loader配置配合按需加载食用

vite项目下，请手动安装 less

```
pnpm add less -D
```

```
css: \\{
  preprocessorOptions: \\{
    less: \\{
      modifyVars: \\{ 'primary-color': 'red' \\},
      javascriptEnabled: true, // 这是必须的
    \\},
  \\},
\\}
```

注意：在使用了 unplugin-vue-components进行按需加载配置后，相关 less变量设置需要同步开启 importStyle: 'less'，[unplugin-vue-components issues 160](https://github.com/antfu/unplugin-vue-components/issues/160)

注意：在使用了 unplugin-vue-components进行按需加载配置后，相关 less变量设置需要同步开启 importStyle: 'less'，unplugin-vue-components issues 160

```
AntDesignVueResolver(\\{ importStyle: 'less' \\}) // 这里很重要
```



### mock数据

vite-plugin-mock 插件
vite plugin配置

```
viteMockServe(\\{
  ignore: /^\_/,
  mockPath: 'mock',
  localEnabled: true,
  prodEnabled: false,
  // 开发环境无需关心
  // injectCode 只受prodEnabled影响
  // https://github.com/anncwb/vite-plugin-mock/issues/9
  // 下面这段代码会被注入 main.ts
  injectCode: `
      import \\{ setupProdMockServer \\} from '../mock/_createProductionServer';

      setupProdMockServer();
      `,
\\})
```

根目录下创建 _createProductionServer.ts文件

```
import \\{ createProdMockServer \\} from 'vite-plugin-mock/es/createProdMockServer';

// 批量加载
const modules = import.meta.globEager('./**/*.ts');

const mockModules: any[] = [];
Object.keys(modules).forEach((key) => \\{
  if (key.includes('/_')) \\{
    return;
  \\}
  mockModules.push(...modules[key].default);
\\});

/**
 * Used in a production environment. Need to manually import all modules
 */
export function setupProdMockServer() \\{
  createProdMockServer(mockModules);
\\}
```

这样mock目录下的非 _开头文件都会被自动加载成mock文件

如：

```
import Mock from 'mockjs';

const data = Mock.mock(\\{
  'items|30': [
    \\{
      id: '@id',
      title: '@sentence(10, 20)',
      account: '@phone',
      true_name: '@name',
      created_at: '@datetime',
      role_name: '@name',
    \\},
  ],
\\});

export default [
  \\{
    url: '/table/list',
    method: 'get',
    response: () => \\{
      const items = data.items;
      return \\{
        code: 0,
        result: \\{
          total: items.length,
          list: items,
        \\},
      \\};
    \\},
  \\},
];
```

配置好代理直接请求 /api/table/list 就可以得到数据了

配置好代理直接请求 /api/table/list 就可以得到数据了



### Proxy代理

```
import proxy from './config/vite/proxy';

export default defineConfig(\\{
  // server
  server: \\{
    hmr: \\{ overlay: false \\}, // 禁用或配置 HMR 连接 设置 server.hmr.overlay 为 false 可以禁用服务器错误遮罩层
    // 服务配置
    port: VITE_PORT, // 类型： number 指定服务器端口;
    open: false, // 类型： boolean | string在服务器启动时自动在浏览器中打开应用程序；
    cors: false, // 类型： boolean | CorsOptions 为开发服务器配置 CORS。默认启用并允许任何源
    host: '0.0.0.0', // 支持从IP启动访问
    proxy,
  \\},
\\})
```

 proxy 如下 

```
import \\{
  API_BASE_URL,
  API_TARGET_URL,
\\} from '../../config/constant';
import \\{ ProxyOptions \\} from 'vite';

type ProxyTargetList = Record<string, ProxyOptions>;

const ret: ProxyTargetList = \\{
  // test
  [API_BASE_URL]: \\{
    target: API_TARGET_URL,
    changeOrigin: true,
    rewrite: (path) => path.replace(new RegExp(`^$\\{API_BASE_URL\\}`), ''),
  \\},
  // mock
  // [MOCK_API_BASE_URL]: \\{
  //   target: MOCK_API_TARGET_URL,
  //   changeOrigin: true,
  //   rewrite: (path) => path.replace(new RegExp(`^$\\{MOCK_API_BASE_URL\\}`), '/api'),
  // \\},
\\};

export default ret;

```



### 环境变量 .env

我这边是把系统配置放到 config/constant.ts 管理了

为了方便管理不同环境的接口和参数配置，可以使用环境变量 .env，如 .env、.env.local、.env.development、.env.production

配合 dotenv库 使用还是很方便的



### 包依赖分析可视化

插件：rollup-plugin-visualizer

```
import visualizer from 'rollup-plugin-visualizer';

visualizer(\\{
  filename: './node_modules/.cache/visualizer/stats.html',
  open: true,
  gzipSize: true,
  brotliSize: true,
\\})
```



### 代码压缩

插件：vite-plugin-compression

代码压缩
插件：vite-plugin-compression

```
import compressPlugin from 'vite-plugin-compression';

compressPlugin(\\{
  ext: '.gz',
  deleteOriginFile: false,
\\})
```



### Chunk 拆包

如果想把类似 ant-design-vue这样的包依赖单独拆分出来，也可以手动配置 manualChunks属性

Chunk 拆包
如果想把类似 ant-design-vue这样的包依赖单独拆分出来，也可以手动配置 manualChunks属性

```
// vite.config.ts
build: \\{
  rollupOptions: \\{
    output: \\{
      manualChunks: configManualChunk
    \\}
  \\}
\\}
```

```
// optimizer.ts
const vendorLibs: \\{ match: string[]; output: string \\}[] = [
  \\{
    match: ['ant-design-vue'],
    output: 'antdv',
  \\},
  \\{
    match: ['echarts'],
    output: 'echarts',
  \\},
];

export const configManualChunk = (id: string) => \\{
  if (/[\\/]node_modules[\\/]/.test(id)) \\{
    const matchItem = vendorLibs.find((item) => \\{
      const reg = new RegExp(`[\\/]node_modules[\\/]_?($\\{item.match.join('|')\\})(.*)`, 'ig');
      return reg.test(id);
    \\});
    return matchItem ? matchItem.output : null;
  \\}
\\};
```



### 兼容处理

插件：@vitejs/plugin-legacy


兼容处理
插件：@vitejs/plugin-legacy

兼容不支持 `<script type="module">`特性的浏览器，或 IE浏览器

```
// Native ESM
legacy(\\{
  targets: ['defaults', 'not IE 11']
\\})

// IE11
// 需要 regenerator-runtime
legacy(\\{
  targets: ['ie >= 11'],
  additionalLegacyPolyfills: ['regenerator-runtime/runtime']
\\})
```



### 路由和布局

```
// router/index.ts
import \\{ createRouter, createWebHashHistory \\} from 'vue-router'
import routes from './router.config'

const router = createRouter(\\{
  history: createWebHashHistory(), //
  routes,
\\})

// main.ts
app.use(router); // 挂载后可全局使用实列，如模板中 <div @click="$router.push('xx')"></div>
```

用法如下：

```
// router.config.ts
import BasicLayout from '/@/layouts/BasicLayout/index.vue'; // 基本布局
import BlankLayout from '/@/layouts/BlankLayout.vue'; // 空布局
import type \\{ RouteRecordRaw \\} from 'vue-router';

const routerMap: RouteRecordRaw[] = [
  \\{
    path: '/app',
    name: 'index',
    component: BasicLayout,
    redirect: '/app/home',
    meta: \\{ title: '首页' \\},
    children: [
      \\{
        path: '/app/home',
        component: () => import('/@/views/home/index.vue'),
        name: 'home',
        meta: \\{
          title: '首页',
          icon: 'liulanqi',
          auth: ['home'],
        \\},
      \\},
      \\{
        path: '/app/others',
        name: 'others',
        component: BlankLayout,
        redirect: '/app/others/about',
        meta: \\{
          title: '其他菜单',
          icon: 'xitongrizhi',
          auth: ['others'],
        \\},
        children: [
          \\{
            path: '/app/others/about',
            name: 'about',
            component: () => import('/@/views/others/about/index.vue'),
            meta: \\{ title: '关于', keepAlive: true, hiddenWrap: true \\},
          \\},
          \\{
            path: '/app/others/antdv',
            name: 'antdv',
            component: () => import('/@/views/others/antdv/index.vue'),
            meta: \\{ title: '组件', keepAlive: true, breadcrumb: true \\},
          \\},
        ],
      \\},
    ]
  \\}
  ...
]
```



### 权限

- 支持页面和菜单级别的权限管理、路由管理
- 支持按钮级别的权限管理
- 支持接口级别的权限管理

几个关键词：router.addRoutes动态路由、v-auth指令、axios拦截

权限
支持页面和菜单级别的权限管理、路由管理
支持按钮级别的权限管理
支持接口级别的权限管理
几个关键词：router.addRoutes动态路由、v-auth指令、axios拦截

使用 router.beforeEach 全局路由钩子

核心逻辑如下，详情见仓库代码 router/permission.ts

```
// 没有获取，请求数据
await permissioStore.fetchAuths();
// 过滤权限路由
const routes = await permissioStore.buildRoutesAction();
// 404 路由一定要放在 权限路由后面
routes.forEach((route) => \\{
  router.addRoute(route);
\\});
// hack 方法
// 不使用 next() 是因为，在执行完 router.addRoute 后，
// 原本的路由表内还没有添加进去的路由，会 No match
// replace 使路由从新进入一遍，进行匹配即可
next(\\{ ...to, replace: true \\});
```


使用v-auth指令控制按钮级别的权限

```
function isAuth(el: Element, binding: any) \\{
  const \\{ hasPermission \\} = usePermission();

  const value = binding.value;
  if (!value) return;
  if (!hasPermission(value)) \\{
    el.parentNode?.removeChild(el);
  \\}
\\}
```



### axios拦截

在 axios请求拦截器 interceptors.request.use 添加

```
// 接口权限拦截
const store = usePermissioStoreWithOut();
const \\{ url = '' \\} = config;
if (!WhiteList.includes(url) && store.getIsAdmin === 0) \\{
  if (!store.getAuths.includes(url)) \\{
    return Promise.reject('没有操作权限');
  \\}
\\}
```



## 总结

在开始使用 vite + vue3的时候，也是边踩坑边学习开发的过程，好在现在社区比较活跃，很多问题都有对应的解决方案，配合文档和github issue一起食用基本ok，该项目也是参考了 vue-vben-admin的一些实现和代码管理，本文作为 vue3使用学习记录~

总结
在开始使用 vite + vue3的时候，也是边踩坑边学习开发的过程，好在现在社区比较活跃，很多问题都有对应的解决方案，配合文档和github issue一起食用基本ok，该项目也是参考了 vue-vben-admin的一些实现和代码管理，本文作为 vue3使用学习记录~

使用过之后会发现 vue3和 vue2有着完全不同的开发体验，现在的 vue3对 TS有着极好的支持，开发效率和质量上上升了一个层次啊，而且也支持 JSX语法，类似 React的形式开发也是可行的，当然，配合 vue模板使用时，也有着极大的灵活性，可自行根据场景定制自己的代码，在结合目前的 script setup开发，直接爽到起飞呀~

在使用 vue3的 composition api开发模式时，一定要摒弃之前的 options api的开发逻辑，配和 hooks可以自由组合拆分代码，灵活性极高，方便维护管理，不会再出现 vue2时代的整个代码都拧在一起的情况

一句话：vite + vue3 + setup + ts + vscode volar 插件，谁用谁知道，爽的一批~

仓库地址：https://github.com/JS-banana/vite-vue3-ts



## 参考

- [vue3](https://v3.vuejs.org/)
- [Pinia](https://pinia.esm.dev/)
- [Vue Router](https://next.router.vuejs.org/)
- [vue-vben-admin](https://github.com/anncwb/vue-vben-admin)
- [一个简单的Vue按钮级权限方案](https://juejin.cn/post/6844904001012514823)
- [手摸手，带你用vue撸后台 系列二(登录权限篇)](https://juejin.cn/post/6844903478880370701)
- [前后端分离下前端权限处理](https://juejin.cn/post/6844904003831070727)

原文链接：https://blog.csdn.net/weixin_44777255/article/details/122540697







# 【Vue3】如何封装一个超级好用的 Hook

本文将通过介绍什么是 Hook、如何在 Vue 使用 Hook，以及在实践场景中如何封装自己的 Vue Hook，带你走进 Hook 的世界，写出更优雅的代码。如果你觉得这篇文章写的不错，可以点赞支持一下，如果文章中存在不足（代码量多，难免出现 bug，咳咳），欢迎在评论区指出！

## 什么是 Hook

Vue3 官方文档是这样定义组合式函数的。`A "composable" is a function that leverages Vue's Composition API to encapsulate and reuse stateful logic.`，一个利用 Vue 的组合式 API 来封装和复用具有状态逻辑的函数。

这个概念借鉴自 React 的 Hook。在 16.8 的版本中，React 引入了 React Hook。这是一项特别强大的技术，通过封装有状态的函数，极大提高了组件的编写效率和维护性。在下文中也是使用 Hook 来替代“组合式函数”进行叙述。

在开发中，我们经常会发现一些可以重复利用的代码段，于是我们将其封装成函数以供调用。这类函数包括工具函数，但是又不止工具函数，因为我们可能也会封装一些重复的业务逻辑。以往，在前端原生开发中，我们封装的这些函数都是“无状态”的。为了建立数据与视图之间的联系，基于 MVC 架构的 React 框架和基于 MVVM 的 Vue 框架都引入了“状态”这一概念，状态是特殊的 JavaScript 变量，它的变化会引起视图的变化。在这类框架中，如果一个变量的变化不会引起视图的变化，那么它就是普通变量，如果一个变量已经被框架注册为状态，那么这个变量的变化就会引发视图的变化，我们称之为响应式变量。如果一个函数包含了状态（响应式变量），那么它就是一个 Hook 函数。

在具备“状态”的框架的基础上，才有 Hook 这一说。Hook 函数与普通函数的本质区别在于是否具备“状态”。

比如，在一个 Vue 项目中，我们可能同时引入了 lodash 库和 VueUse 库，这两个库都是提供一些方便的工具函数。工具函数库只引入一个不行吗，不会重复吗？或许不行，因为 lodash 的函数是无状态的，用来处理普通变量或者响应式变量中的数据部分，而 VueUse 提供的 api 都是 Hook。如果你的项目中既有普通变量又有响应式变量，你或许就会在同一个项目中同时接触到这两个库。

React 官方为我们提供了一些非常方便的 Hook 函数，比如 useState、useEffect（我们通常使用 use 作为前缀来标识 Hook 函数），但是这远远不够，或者说，它们足够通用但是不够具体。为了在具体业务下复用某些逻辑，我们往往会封装自己的 Hook，即自定义 Hook。为什么这里会反复提到 React 中呢？因为提到 Hook，就不可能避开 React。Hook 是 React 发扬光大的，使用 Hook 已经是 React 社区的主流。然而，只要框架具备“状态”这一概念，都可以使用 Hook 技术！下面文章将会介绍如何将 Hook 应用到 Vue 当中。

## 在 Vue 中使用Hook

下面我们来看一个简单的自定义 Hook（来自 Vue 官方文档）：

需求：在页面实时显示鼠标的坐标。 实现：没有使用 Hook。

```html
<script setup>
import \\{ ref, onMounted, onUnmounted \\} from 'vue'

const x = ref(0)
const y = ref(0)

function update(event) \\{
  x.value = event.pageX
  y.value = event.pageY
\\}

onMounted(() => window.addEventListener('mousemove', update))
onUnmounted(() => window.removeEventListener('mousemove', update))
</script>

<template>Mouse position is at: \\\{\\\{ x\\\}\\\} }}, \\\{\\\{ y\\\}\\\} }}</template>
```

在没有封装的情况下，如果我们在另一个页面也需要这个功能，我们需要将代码复制过去。另外，可以看出，它声明了两个变量，并且在生命周期钩子 `onMounted` 和 `onUnmounted` 中书写了一些代码，如果这个页面需要更多的功能，那么会出现代码中存在很多变量、生命周期中存在很多逻辑写在一起的现象，使得这些逻辑混杂在一起，而使用 Hook 可以将其分隔开来（这也是为什么会有很多人使用 Hook 的原因，分离代码，提高可维护性！）

使用 Hook：

```html
<script setup>
import \\{ useMouse \\} from './mouse.js'

const \\{ x, y \\} = useMouse()
</script>

<template>Mouse position is at: \\\{\\\{ x\\\}\\\} }}, \\\{\\\{ y\\\}\\\} }}</template>
```

可以发现，比原来的代码更加简洁，这时如果加入其它功能的变量，也不会觉得眼花缭乱了。

当然，我们需要在外部定义这个 Hook：

```js
// mouse.js
import \\{ ref, onMounted, onUnmounted \\} from 'vue'

// 按照惯例，组合式函数名以“use”开头
export function useMouse() \\{
  // 被组合式函数封装和管理的状态
  const x = ref(0)
  const y = ref(0)

  // 组合式函数可以随时更改其状态。
  function update(event) \\{
    x.value = event.pageX
    y.value = event.pageY
  \\}

  // 一个组合式函数也可以挂靠在所属组件的生命周期上
  // 来启动和卸载副作用
  onMounted(() => window.addEventListener('mousemove', update))
  onUnmounted(() => window.removeEventListener('mousemove', update))

  // 通过返回值暴露所管理的状态
  return \\{ x, y \\}
\\}
```

或许，你可以试着去 VueUse 库找到别人封装好的 useMouse！

```js
import \\{ useMouse \\} from 'VueUse'
```

恭喜你，掌握了 VueUse 库的使用方法。如果需要其它 Hook，你可以先试着去官方文档（[VueUse](https://vueuse.org/)）查找，使用现成的函数，而不是自己去封装。

## 封装一（入门级的表格 Hook）

在前面，我们介绍完了 Hook 的概念，完成了一个简单的自定义 Hook，还学会了使用社区提供的大量现成的 Hook 函数（VueUse 库），接下来，我们将结合实际业务，完成我们自己的 Hook 函数！

### 场景分析

首先定义一个表格：

```vue
<template>
  <el-table :data="tableData" style="width: 100\\%">
    <el-table-column prop="date" label="Date" width="180" />
    <el-table-column prop="name" label="Name" width="180" />
    <el-table-column prop="address" label="Address" />
  </el-table>
  <button @click="refresh">refresh</button>
</template>
```

表格的数据通过 api 获取（一般写法）：

```vue
<script lang="ts" setup>
import \\{ onMounted, ref \\} from "vue";
import \\{ getTableDataApi \\} from "./api.ts";

const tableData = ref([]);
const refresh=async () => \\{
  const data = await getTableDataApi();
  tableData.value = data;
\\}

onMounted(refresh);
</script>
```

模拟 api：

```JavaScript
// api.ts
export const getTableDataApi = () => \\{
  const data = [
    \\{
      date: '2016-05-03',
      name: 'Tom',
      address: 'No. 189, Grove St, Los Angeles',
    \\},
    \\{
      date: '2016-05-02',
      name: 'Tom',
      address: 'No. 189, Grove St, Los Angeles',
    \\},
    \\{
      date: '2016-05-04',
      name: 'Tom',
      address: 'No. 189, Grove St, Los Angeles',
    \\},
    \\{
      date: '2016-05-01',
      name: 'Tom',
      address: 'No. 189, Grove St, Los Angeles',
    \\},
  ]
  return new Promise(resolve => \\{
    setTimeout(() => \\{
      resolve(data)
    \\}, 100);
  \\})
\\}
```

如果存在多个表格，我们的 js 代码会变得比较复杂：

```vue
<script lang="ts" setup>
import \\{ onMounted, ref \\} from "vue";
import \\{ getTableDataApi1, getTableDataApi2, getTableDataApi3 \\} from "./api.ts";

const tableData1 = ref([]);
const refresh1=async () => \\{
  const data = await getTableDataApi1();
  tableData1.value = data;
\\}

const tableData2 = ref([]);
const refresh2=async () => \\{
  const data = await getTableDataApi2();
  tableData2.value = data;
\\}

const tableData3 = ref([]);
const refresh3=async () => \\{
  const data = await getTableDataApi3();
  tableData3.value = data;
\\}

onMounted(refresh1);
</script>
```

### 封装实例

封装我们的 useTable：

```js
// useTable.ts
import \\{ ref \\} from 'vue'
export function useTable(api) \\{
  const data = ref([])
  const refresh = () => \\{ api().then(res => data.value = res) \\};
  refresh()
  return [data, refresh]
\\}
```

改造代码：

```vue
<script lang="ts" setup>
import \\{ onMounted, ref \\} from "vue";
import \\{ getTableDataApi1, getTableDataApi2, getTableDataApi3 \\} from "./api.ts";
import \\{ useTable \\} from './useTable.ts'

const [tableData1, refresh1] = useTable(getTableDataApi1);
const [tableData2, refresh2] = useTable(getTableDataApi2);
const [tableData3, refresh3] = useTable(getTableDataApi3);

onMounted(refresh1);
</script>
```

### 封装技巧 - Hook 返回值

1. 一般自定义 Hook 有返回数组的，也有返回对象的，上面 useTable 使用了返回数组的写法，useMouse 使用了返回对象的写法。数组是对应位置命名的，可以方便重命名，对象对于类型和语法提示更加友好。两种写法都是可以替换的。
2. 因为 Hook 返回对象或者数组，那么它一定是一个非 async 函数（async 函数一定返回 Promise），所以在 Hook 中，一般使用 then 而不是 await 来处理异步请求。
3. 返回值如果是对象，一般在函数中通过 reactive 创建一个对象，最后通过 toRefs 导出，这样做的原因是可以产生批量的可以解构的 Ref 对象，以免在解构返回值时丢失响应性。

```javascript
// 使用 reactive 和 toRefs 可以快速创建多个ref对象，并在解构后使用时不丢失其响应性和与原先数据的关联性
function usePaginaion()\\{
	const pagination = reactive(\\{
		current: 1,
		total: 0,
		sizeOption,
		size: sizeOption[0]
	\\})
	...
	return \\{...toRefs(pagination)\\}
\\}

const \\{ current,total \\} = usePagination()
```

## 封装二（支持分页查询）

### 需求分析

上面我们封装了一个简单的 hook，但是实际应用中并不会如此简单，下面我列出一个比较完整的 useTable 在实践中应该具备的功能，并在后续的文章部分完成它。

封装表格组件逻辑：

1. 维护 api 的调用和刷新（已完成）
2. 支持分页查询（页数、总条数、每页大小等）
3. 支持 api 参数。
4. 增加辅助功能（loading、立即执行等）

下面我们将对 useTable 进行改造，使其支持分页器。

先改造一些我们的 api，使其支持分页查询：

```js
export const getTableDataApi = (page, limit) => \\{
  const data = [
    \\{
      date: '2016-05-03',
      name: 'Tom',
      address: 'No. 189, Grove St, Los Angeles',
    \\},
    \\{
      date: '2016-05-02',
      name: 'Tom',
      address: 'No. 189, Grove St, Los Angeles',
    \\},
    \\{
      date: '2016-05-04',
      name: 'Tom',
      address: 'No. 189, Grove St, Los Angeles',
    \\},
    \\{
      date: '2016-05-01',
      name: 'Tom',
      address: 'No. 189, Grove St, Los Angeles',
    \\},
    \\{
      date: '2017-05-03',
      name: 'Tom',
      address: 'No. 189, Grove St, Los Angeles',
    \\},
    \\{
      date: '2017-05-02',
      name: 'Tom',
      address: 'No. 189, Grove St, Los Angeles',
    \\},
    \\{
      date: '2017-05-04',
      name: 'Tom',
      address: 'No. 189, Grove St, Los Angeles',
    \\},
    \\{
      date: '2017-05-01',
      name: 'Tom',
      address: 'No. 189, Grove St, Los Angeles',
    \\},
  ]
  return new Promise(resolve => \\{
    setTimeout(() => \\{
      resolve(\\{
        total: data.length,
        data: data.slice((page - 1) * limit, (page - 1) * limit + limit)
      \\})
    \\}, 100);
  \\})
\\}
```

如果没有使用 Hook，我们的 vue 文件应该是这样的：

```vue
<template>
  <el-table :data="tableData" style="width: 100\\%">
    <el-table-column prop="date" label="Date" width="180" />
    <el-table-column prop="name" label="Name" width="180" />
    <el-table-column prop="address" label="Address" />
  </el-table>
  <button @click="refresh">refresh</button>
  <!-- 分页器 -->
  <el-pagination
    v-model:current-page="current"
    :page-size="size"
    layout="total, prev, pager, next"
    :page-sizes="sizeOption"
    :total="total"
    @size-change="handleSizeChange"
    @current-change="handleCurrentChange"
  />
</template>

<script lang="ts" setup>
import \\{ onMounted, ref \\} from "vue";
import \\{ getTableDataApi \\} from "./api.ts";

const tableData = ref([]); // 表格数据
const current = ref(1); // 当前页数
const sizeOption = [10, 20, 50, 100, 200]; // 每页大小选项
const size = ref(sizeOption[0]); //每页大小
const total = ref(0); // 总条数

// 每页大小变化
const handleSizeChange = (size: number) => \\{
  size.value = size;
  current.value = 1;
  // total.value = 0;
  refresh();
\\};

// 页数变化
const handleCurrentChange = (page: number) => \\{
  current.value = page;
  // total.value = 0;
  refresh();
\\};

const refresh = async () => \\{
  const result = await getTableDataApi(\\{
    page: current.value,
    limit: size.value,
  \\});
  tableData.value = result.data || [];
  total.value = result.total || 0;
\\};

onMounted(refresh);
</script>
```

可以看出，如果存在多个表格，会创建很多套变量和重复的代码。

### 封装实例

先写个 usePagination：该钩子接受一个回调函数，当页数改变时就会调用该函数。

```javascript
import \\{ reactive \\} from "vue";
export function usePagination(
  cb: any,
  sizeOption: Array<number> = [10, 20, 50, 100, 200]
): any \\{
  const pagination = reactive(\\{
    current: 1,
    total: 0,
    sizeOption,
    size: sizeOption[0],
    // 维护page和size（一般是主动触发）
    onPageChange: (page: number) => \\{
      pagination.current = page;
      return cb();
    \\},
    onSizeChange: (size: number) => \\{
      pagination.current = 1;
      pagination.size = size;
      return cb();
    \\},
    // 一般调用cb后会还会修改total（一般是被动触发）
    setTotal: (total: number) => \\{
      pagination.total = total;
    \\},
    reset() \\{
      pagination.current = 1;
      pagination.total = 0;
      pagination.size = pagination.sizeOption[0];
    \\},
  \\});

  return [
    pagination,
    pagination.onPageChange,
    pagination.onSizeChange,
    pagination.setTotal,
  ];
\\}
```

与 useTable 结合：代码非常简单，在调用 api 时传入参数，并在接受返回值时更新 data 和 total。这里我们的 refresh 函数是一个返回 Promise 的函数，能够支持在调用 refresh 处再链接 then 进行下一层处理。

```javascript
export function useTable(api: (params: any) => Promise<T>) \\{
  const [pagination, , , setTotal] = usePagination(() => refresh());
  const data = ref([]);

  const refresh = () => \\{
    return api(\\{ page: pagination.current, limit: pagination.size \\}).then(
      (res) => \\{
        data.value = res.data;
        setTotal(res.total);
      \\}
    );
  \\};
  return [data, refresh, pagination];
\\}
```

注：我们新建一个文件 `customHooks.js` 并将 usePagination 和 useTable 放在里面。

使用 useTable：

```vue
<template>
  <el-table :data="tableData" style="width: 100\\%">
    <el-table-column prop="date" label="Date" width="180" />
    <el-table-column prop="name" label="Name" width="180" />
    <el-table-column prop="address" label="Address" />
  </el-table>
  <button @click="refresh">refresh</button>
  <!-- 分页器 -->
  <el-pagination
    v-model:current-page="pagination.current"
    :page-size="pagination.size"
    layout="total, prev, pager, next"
    :page-sizes="pagination.sizeOption"
    :total="pagination.total"
    @size-change="pagination.onSizeChange"
    @current-change="pagination.onCurrentChange"
  />
</template>

<script lang="ts" setup>
import \\{ onMounted, ref \\} from "vue";
import \\{ getTableDataApi \\} from "./api.ts";
import \\{ useTable \\} from './customHooks.ts'

const [tableData, refresh, pagination] = useTable(getTableDataApi);

onMounted(refresh);
</script>
```

## 封装三（支持不同接口字段）

### 封装分析

上面我们封装了一个“看起来”比较使用的 useTable 函数，但实际上，你会发现很多问题：

1. 每次都要写 onMounted 来初始化数据。
2. 接口接受的格式可能不一样，比如，页数的字段为"currentPage"，而不是“page”。
3. 接口返回的格式可能不一样，比如，返回的 data 并不在 refresh 方法定义的“data”上。

### 封装实例

接下来，我们通过增加 useTable 函数的参数，来解决上面所有问题！

```JavaScript
import \\{ get, has, defaults \\} from "lodash-es";
type keyPath = Array<string> | string;
export function useTable<T>(
  api: (params: any) => Promise<T>,
  options?: \\{
    path?: \\{ data?: keyPath; total?: keyPath; page?: string; size?: string \\};
    immediate?: boolean;
  \\}
) \\{
  // 参数处理
  defaults(options, \\{
    path: \\{ data: "data", total: "total", page: "page", size: "size" \\},
    immediate: false,
  \\});

  const [pagination, , , setTotal] = () => refresh();
  const data = ref([]);
  const loading = ref(false)

  const refresh = () => \\{
	loading.value = true
    return api(\\{ [options?.path?.page]: pagination.current, [options?.path?.size]: pagination.size \\}).then(
      (res) => \\{
        data.value = get(res, options!.path?.data, []);
        setTotal(get(res, options!.path?.total, 0));
        // 友好提示
        if (!has(res, options!.path?.data) || !has(res, options!.path?.total)) \\{
          console.warn("useTable：响应数据缺少所需字段");
        \\}
      \\}.finally(() => \\{
        loading.value = false
      \\})
    );
  \\};
 // 立即执行
  options!.immediate && refresh();
  return [data, refresh, loading, pagination];
\\}
```

这里引入了 lodash 库中的三个工具函数来辅助处理对象：

- defaults，将后面参数的属性，赋值到第一个对象的值为 undefined 的属性上，用于初始化函数参数。
- get，获取对象属性，如果为 undefined，使用第三个参数的值。
- has，判断对象属性。

具体用法可以查看官方文档（[Lodash 简介 | Lodash中文文档 | Lodash中文网](https://link.juejin.cn?target=https\\%3A\\%2F\\%2Fwww.lodashjs.com\\%2F)） 此外，还新增了 loading，可以挂载到 el-table 的 v-loading 上，展示数据加载中的效果。

```html
<el-table v-loding="loading" ...>...</el-table>
```

改造后：不管接口接受的格式还是响应的格式字段是什么样的，都可以正常接收。设置 immediate 为 true，调用 useTable 时立即执行一遍 api，onMounted 都不用写了。

```javascript
<script lang="ts" setup>
import \\{ onMounted, ref \\} from "vue";
import \\{ getTableDataApi \\} from "./api.ts";
import \\{ useTable \\} from './customHooks.ts'

const [tableData, refresh, loading, pagination] = useTable(getTableDataApi, \\{
  path: \\{
    data: 'data',
    total: 'total',
    page: 'page',
    size: 'limit'
  \\},
  immediate: true
\\});

// onMounted(refresh);
</script>
```

### JavaScript 函数传参技巧

1. 一般函数定义参数越少越好，最好不要超过两个，所以这里我只定义了两个参数 api 和options。
2. 在函数头上可以给参数定义默认值，但是如果参数是一个对象，只要传入一个属性，就不会使用默认值，比如：

```JavaScript
export function useTable<T>(
  api: (params: any) => Promise<T>,
  options: \\{
    path?: \\{ data?: keyPath; total?: keyPath; page?: string; size?: string \\};
    immediate?: boolean;
  \\} = \\{
    path: \\{ data: "data", total: "total", page: "page", size: "size" \\},
    immediate: false,
  \\}
)\\{...函数体\\} 

useTable(xxxApi,\\{immediate:false\\})
```

只要该位置的值非 undefined，那么 options 将不会使用默认值，这意味着，此时 options 的值为 `\\{immediate:false\\}`，其它地方的默认值不会生效，`\\{path:undefined,\\}`。 所以对于函数参数为对象的，我们往往通过在函数体内赋默认值，比如：

```JavaScript
保证options只传入一个值，其它位置也会有默认值
\\{
  options.path = options.path || \\{\\}
  options.path.data = options.path.data || 'data'
  options.path.total = options.path.total || 'total'
  options.path.page = options.path.page || 'page'
  options.path.size = options.path.size || 'size'
  options.immediate = options.immediate ?? false
\\}
```

需要注意元素的层次，在不存在 path 时，给 path. data 赋值会出现错误，需要先保证 path 有值，才能给 path 的下一层赋值。

使用 defaults 可以快速给整个对象赋默认值：

```javascript
  defaults(options, \\{
    path: \\{ data: "data", total: "total", page: "page", size: "size" \\},
    immediate: false,
  \\});
```

## 封装四（接口传参-定义时）

### 封装分析

现在，我们的 useTable 趋近完整了：

1. 维护 api 的调用和刷新（已完成）
2. 支持分页查询（已完成）
3. 支持 api 参数。
4. 增加辅助功能 loading、立即执行等。（已完成）

我们还可以让我们的 api 接受参数。但是如何实现？还需要考虑一下。

首先我们想一想那里可以接受 api 的参数？

```JavaScript
const params = \\{
	id:2
\\}

// api本身
getTableDataApi(\\{limit:3,page:2,...params\\})

// useTable也可以接受参数
const [data,refresh]=useTable(getTableDataApi,params,api)

// refresh也可以接受参数
refresh(params)
```

从使用上看，我们在 refresh 上接受参数，和我们在 getTableDataApi 的使用上感觉是最相似的，因为 refresh 本来就是在 api 的基础上增加 then 维护了页数而已。但是我们还是先从 useTable 传参开始讲起，最后我们两种方式都可以接受！

方案一：在调用 useTable 的时候就接受参数，在 useTable 内部将这个参数传给 refresh。 存在问题：如果我们传入的是值类型，那么这个值会被拷贝过去，并传给 refresh，后续调用 refresh，都是不变的参数。只适合需要传参但参数之后都不会变的接口，比如接受当前用户的 id。如果参数会变，这种方法是不行的。

```javascript
function useTable(api,id,options)\\{
	...
	const refresh=()=>api(id).then(res=>data=res)
	return [data,refresh]
\\}

const [data,refresh]=useTable(api,id)
refresh()
refresh() // 都是id=2
```

如果我们传入的是引用类型，那么在后续调用中，我们可以通过改变对象的属性值来改变 refresh 的参数（但是需要一些技巧，因为我们需要和分页参数进行结合）。

```JavaScript
const params = \\{ id:12 \\}
function useTable(api,params,options)\\{
	...
	// 错误，使用解构会丢失与原来对象的联系，导致原来的对象params更改，但这里仍使用旧值。
	const refresh=()=>api(\\{[options.path.size]:pagination.size,[options.path.page]:pagination.page,...params\\}).then(res=>data=res)
	// 正确，可以保持与外部params的联系。
	const refresh=()=>api(Object.assign(params,\\{[options.path.size]:pagination.size,[options.path.page]:pagination.page\\})).then(res=>data=res)
	return [data,refresh]
\\}

const [data,refresh]=useTable(api,params)
refresh() // id=12
params.id = 10
refresh() // id=10
```

这样，我们就实现了 api 参数的传递，而且如果 params 的属性 id 是响应式的，还可以与页面结合，实现搜索功能！然而，使用同一个引用 params，可以解决传参问题，但是还是存在一些问题：在 refresh 中，Object. assign 会给原来的对象 params 增加两个属性，要注意避免在 params 中与这两个属性发生冲突。另外，我们可以看到这里的参数间存在了一种优先级，就是如果我们在 param 中也传入了分页参数，会在 refresh 中被 pagination 的分页参数覆盖调，pagination 的分页参数比 params 中的分页参数优先级更高，这样好吗？

第一个问题，在 refresh 中每次都会被 pagination 的属性覆盖，所以并不会出现什么问题，除非你在 params 上保存相同属性名的数据，这将被覆盖掉。第二个问题和第一个问题本质是一样的，就是覆盖问题。根本原因就是都是引用同一个对象。如果我们能够额外创建一个对象，就不会改变原来的对象，但是如何保持新创建对象能够动态变化呢？

方案二：试试 useTable 接受传入函数 params 如何？

```javascript
const params=\\{id:12\\}
const paramsFn =()=>\\{ id: params.id \\}
function useTable(api,paramsFn(),options)\\{
	...
	const refresh=()=>api(Object.assign(paramsFn(),\\{[options.path.size]:pagination.size,[options.path.page]:pagination.page\\})).then(res=>data=res)
	return [data,refresh]
\\}

const [data,refresh]=useTable(api,paramsFn)
refresh() // id=12
params.id = 10
refresh() // id=10
```

完美解决。

最后，兼容一下两种参数，让传入 useTable 的 api 参数既可以是函数，又可以是对象：

```javascript
export function useTable<T>(
  api: (params: any) => Promise<T>,
  params?: object | (() => object),
  options?: \\{
    path?: \\{ data?: keyPath; total?: keyPath; page?: string; size?: string \\}
    immediate?: boolean
  \\},
) \\{
  // 参数处理
  defaults(options, \\{
    path: \\{ data: 'data', total: 'total', page: 'page', size: 'size' \\},
    immediate: false,
  \\})

  const [pagination, , , setTotal] = usePagination(() =>refresh())
  const loading = ref(false)
  const data = ref([])

  const refresh = (extraData?: object | (() => object)) => \\{
    const requestData = \\{
      [options?.path?.page as string]: pagination.current,
      [options?.path?.size as string]: pagination.size,
    \\}
    if (params) \\{
      if (typeof params === 'function') \\{
        Object.assign(requestData, params())
      \\} else \\{
        Object.assign(requestData, params)
      \\}
    \\}
    loading.value = true
    return api(requestData)
      .then((res) => \\{
        data.value = get(res, options!.path?.data, [])
        setTotal(get(res, options!.path?.total, 0))
        if (!has(res, options!.path?.data) || !has(res, options!.path?.total)) \\{
          console.warn('useTable：响应数据缺少所需字段')
        \\}
      \\})
      .finally(() => \\{
        loading.value = false
      \\})
  \\}

  options!.immediate && refresh()

  return [data as T, refresh, loading, pagination]
\\}
```

这里代码主要新增了三处改变：

1. 如果 params 是对象，直接使用，如果是函数，则读取其返回值。
2. 优先级调整：paginaiton 的参数可以被 params 的同名属性覆盖，适用于开发者自己维护分页参数。
3. 定义了返回值的类型。

### 使用示例

试想一个常见，点击列表的某一项，就展示列表对应 id 的表格，如何实现？

```html
<template>
	<ul>
		// 自定义组件，点击时emit发送onClick事件并传入item的id
		<Item v-for="item in list" :key="item.key" :label="item.label" @on-click="handleClick">
		...
	</ul>
</template>

<script>
...
// 这里接受item的id
const handleClick=(id:number)=>\\{
	params.id=number;
	refresh()
\\}
...
</script>
```

## 封装五（接口传参-调用时）

最后，来让 refresh 函数也能接受我们的传参。 先看效果：

```html
<script>
...
// 这里接受item的id
const handleClick=(id:number)=>\\{
	refresh(\\{id\\})
\\}
...
</script>
```

可以省去 params 和 paramsFn 的定义了！

实现代码：在定义 refresh 时允许加入参数。

```javascript
export function useTable<T>(
  api: (params: any) => Promise<T>,
  params?: object | (() => object),
  options?: \\{
    path?: \\{ data?: keyPath; total?: keyPath; page?: string; size?: string \\}
    immediate?: boolean
  \\},
) \\{
  defaults(options, \\{
    path: \\{ data: 'data', total: 'total', page: 'page', size: 'size' \\},
    immediate: false,
  \\})

  // 使用()=>fn()而不是fn()区别在于后者只是一个值且立即执行
  const [pagination, , , setTotal] = usePagination((extraData?: object) =>
    extraData ? refresh(extraData) : refresh(),
  )
  const loading = ref(false)
  const data = ref([])

  const refresh = (extraData?: object | (() => object)) => \\{
    const requestData = \\{
      [options?.path?.page as string]: pagination.current,
      [options?.path?.size as string]: pagination.size,
    \\}
    if (extraData) \\{
      if (typeof extraData === 'function') \\{
        Object.assign(requestData, extraData())
      \\} else \\{
        Object.assign(requestData, extraData)
      \\}
    \\}
    if (params) \\{
      if (typeof params === 'function') \\{
        Object.assign(requestData, params())
      \\} else \\{
        Object.assign(requestData, params)
      \\}
    \\}
    loading.value = true
    return api(requestData)
      .then((res) => \\{
        // TODO 检查响应状态码
        data.value = get(res, options!.path?.data, [])
        setTotal(get(res, options!.path?.total, 0))
        // 友好提示
        if (!has(res, options!.path?.data) || !has(res, options!.path?.total)) \\{
          console.warn('useTable：响应数据缺少所需字段')
        \\}
      \\})
      .finally(() => \\{
        loading.value = false
      \\})
  \\}

	return[data,refresh,paginaiton,loading]
\\}
```

需要注意的是，usePagination 处接受的回调函数也要适当修改。当然，pagination 也是要修改的了（增加回调函数有参数的情况，之前回调是没有参数的）。这里还额外新增了一个 reset 方法，用于重置分页器状态，这或许会有用！

```javascript
export function usePagination(
  cb: any,
  sizeOption: Array<number> = [10, 20, 50, 100, 200],
): any \\{
  const pagination = reactive(\\{
    current: 1,
    total: 0,
    size: sizeOption[0],
    sizeOption,
    onPageChange: (page: number, extraData?: object) => \\{
      pagination.current = page
      return extraData ? cb(extraData) : cb()
    \\},
    onSizeChange: (size: number, extraData?: object) => \\{
      pagination.current = 1
      pagination.size = size
      return extraData ? cb(extraData) : cb()
    \\},
    setTotal: (total: number) => \\{
      pagination.total = total
    \\},
    reset() \\{
      pagination.current = 1
      pagination.total = 0
      pagination.size = pagination.sizeOption[0]
    \\},
  \\})

  return [
    pagination,
    pagination.onPageChange,
    pagination.onSizeChange,
    pagination.setTotal,
  ]
\\}
```

使用：

```html
  <!-- 分页器 -->
  <el-pagination
    v-model:current-page="current"
    :page-size="size"
    layout="total, prev, pager, next"
    :page-sizes="sizeOption"
    :total="total"
    @size-change="(size)=>handleSizeChange(size,params.id)"
    @current-change="(page)=>handleCurrentChange(page,params.id)"
  />
```

在此之前，需要保存 item. id 作为全局变量以供读取。

```javascript
const handleClick=(id:number)=>\\{
	params.id=id;
\\}
```

这样，我们就完成了一个功能相对完善的 Hook 函数。

## 总结

本文通过介绍 Hook 的概念和使用方法，并在实践的过程中封装了一个功能相对完善的 Hook 函数，但是它还有很多可以拓展的地方，比如 useTable 中可以再导出一个 clear 函数，用来将 data 赋值为空数组，以及对 data 数据的每一项进行查找、删除，或者新增一个 showData，用来过滤 data 并展示在视图上，总之，我们打开了 Hook 世界的大门，看到了 Hook 这项技术的强大之处：状态复用！

因为本文主要讲解 Hook 封装，所以比较少提及组件封装。如果代码需要复用，首先考虑组件封装，因为它可以对 html、css 和 javacript 代码进行复用，而 Hook 只是复用 JavaScript 代码。如果将二者结合，能够高效地提高你的开发效率，以及项目的可维护性，帮助你写出优雅的代码。

原文链接：https://juejin.cn/post/7299849645206781963