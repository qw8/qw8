---
title: pnpm
date: 2019-12-10 19:25:55
categories: 
- 前端知识
tags:
- pnpm
---

现在越来越多的公司或开源项目开始使用 `pnpm` 作为包管理工具，这篇文章主要想分享一下这个优秀的包管理器的用法和原理，以及为什么我们应该使用它来代替 `npm` 和 `yarn`。



## pnpm 是什么？

根据[官方文档](https://link.juejin.cn?target=https\\%3A\\%2F\\%2Fpnpm.io\\%2Fzh\\%2F)的描述，我们可以知道 `pnpm` 是一个**快速的**，**节省磁盘空间**的包管理工具，同时它还对 `monorepos` 有良好的支持。

它的用处与 `npm`  和 `yarn` 并没有什么本质区别，甚至连用法都十分相似。

并且它的安装也非常简单：`npm i pnpm -g`



## pnpm的优势是什么？

### 1. 速度快

这里直接放上官方文档中的 [benchmark](https://link.juejin.cn?target=https\\%3A\\%2F\\%2Fpnpm.io\\%2Fzh\\%2Fbenchmarks) 对比：

![Graph of the alotta-files results](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/bcdebc603f1c459c9e4bd4f9ac65ab02~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

我们可以清晰地看到在大多数的情况下，`pnpm` 的安装速度都要优于 `npm/yarn`。

### 2. 节省磁盘空间

`pnpm` 内部使用**基于内容寻址存储（CAS - Content-addressable store）**的方式来存储依赖，它是一种存储信息的方式，根据内容而不是位置进行检索信息的存储方式，被用于高速存储和检索的固定内容.。它的优点在于:

- 不会重复安装同一个包。用 `npm/yarn` 的时候，如果 100 个项目都依赖 `lodash`，那么 `lodash` 很可能就被安装了 100 次。但使用 `pnpm` 则只会安装一次，磁盘中只有一个地方写入，后面再次使用都会直接使用 `hardlink`（硬链接）。
- 即使一个包的不同版本，`pnpm` 也会极大程度地复用之前版本的代码。举个例子，比如 `lodash` 有 100 个文件，更新版本之后多了一个文件，那么磁盘当中并不会重新写入 101 个文件，而是保留原来的 100 个文件的 `hardlink`，**仅仅写入那一个新增的文件**。

### 3. 支持 monorepo

关于 `monorepo` 可以看[这篇文章](https://link.juejin.cn?target=https\\%3A\\%2F\\%2Fwww.perforce.com\\%2Fblog\\%2Fvcs\\%2Fwhat-monorepo)的介绍。

`pnpm` 对 `monorepo` 的支持体现在各个子命令的功能上，比如在根目录下 `pnpm add A -r`, 那么所有的 package 中都会被添加 A 这个依赖。

### 4. 安全性高

如果使用 `npm/yarn` 进行包管理，由于 `node_module` 的扁平结构，如果 A 依赖 B， B 依赖 C，那么 A 当中是可以直接使用 C 的，但问题是 A 当中并没有声明 C 这个依赖（幽灵依赖）。因此会出现这种非法访问的情况。但 `pnpm` 自创了一套依赖管理方式，很好地解决了这个问题，保证了安全性。



## 依赖管理方式对比

### npm/yarn 的原理

当执行 `npm/yarn install` 命令之后，首先会构建依赖树，然后针对每个节点下的包会经历以下四个步骤：

1. 将依赖包的版本区间解析为某个具体的版本号
2. 下载对应版本依赖的 tar 包到本地离线镜像
3. 将依赖从离线镜像解压到本地缓存
4. 将依赖从缓存拷贝到当前目录的 node_modules 目录

之后对应包就会到达项目中的 `node_modules` 文件夹下。

**在 `npm` 3.0 版本之前**，项目的 `node_modules` 会呈现出嵌套结构：

```js
js复制代码node_modules
└─ foo
   ├─ index.js
   ├─ package.json
   └─ node_modules
      └─ bar
         ├─ index.js
         └─ package.json
└─ zoo
   ├─ index.js
   ├─ package.json
   └─ node_modules
      └─ bar
         ├─ index.js
         └─ package.json
```

这种嵌套依赖树设计存在几个严重的问题：

1. 依赖层级太深，这会导致文件的路径过长的问题，毕竟 windows 系统的文件路径默认最多支持 256 个字符。
2. 会出现很多包被重复安装的情况，导致项目体积暴涨。比如上面 `foo` 和 `bar` 都依赖于 `bar`，那么 `bar` 就会在两者的 `node_modules` 中被安装两次。
3. 模块实例不能共享。比如 React 有一些内部变量，在两个不同包引入的 React 不是同一个模块实例，因此无法共享内部变量，导致一些不可预知的 bug。

后来 `yarn` 横空出世，解决了上面的几个问题，并且 `npm` 也在 3.0 版本中沿用了 `yarn` 的解决方案，这个解决方案就是**扁平化依赖**。

所谓的**扁平化依赖**就是将所有依赖铺平，放到同一级目录下。这时的 `node_modules` 结构类似这样：

```js
js复制代码node_modules
├─ foo
|  ├─ index.js
|  └─ package.json
└─ bar
|  ├─ index.js
|  └─ package.json
└─ zoo
   ├─ index.js
   └─ package.json
```

在这种扁平化管理下，`node_modules` 目录下不会再有很深层次的嵌套关系，这样在安装新的包时，根据 node require 机制，会不停往上级的 `node_modules` 当中去找，如果找到相同版本的包就不会重新安装，解决了包重复安装的问题。

虽然之前的问题得到了解决，但同时这种扁平化的处理方式自身也存在许多问题，其中最为明显的问题就是”**幽灵依赖**“。

所谓的幽灵依赖是指我们明明没有在 `package.json` 的 dependencies 里声明某个依赖，但在代码里却可以 import 进来。原因很简单，因为项目依赖被铺平了，那么依赖的依赖自然也是可以被引入到项目中。

幽灵依赖带来的弊端很明显：我们显式依赖了A，A又依赖了B，这时候我们在项目中直接使用B是可以的，但如果某一天A不再依赖于B，那么我们项目中使用B的地方就会报错。

那么如何解决幽灵依赖问题呢？这就要提到 `pnpm` 了。

### 硬链接和软链接

在探索 `pnpm` 的原理之前，我们必须要知道两个重要概念：**硬链接**和**软链接**。

首先说一下两种概念的定义，这里我直接贴出 wiki 上的定义。

- **硬链接**（hard link）是计算机文件系统中的**多个文件**平等地共享**同一个文件存储单元**。
- **符号链接**（**软链接、Symbolic link**）是一类**特殊的文件**，其包含有一条以绝对路径或者相对路径的形式**指向其它文件或者目录的引用**。

![image-20230206155912289](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ce1d944081f744d7919cb6850e86d756~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

软链接其实很好理解，它就相当于 windows 系统中的快捷方式。一个符号链接文件仅包含有一个文本字符串，其被操作系统解释为一条指向另一个文件或者目录的路径。它是一个**独立文件**，其存在并不依赖于目标文件。如果删除一个符号链接，它指向的目标文件**不受影响**。如果目标文件被移动、重命名或者删除，任何指向它的符号链接仍然存在，但是它们将**会指向一个不复存在的文件**。

![image-20230206153319348](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/834f073660b64e16b0bcdeb8bd35d04e~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

那么什么是硬链接呢？我简单画了一幅图来解释它的概念：

![image-20230206155004217](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/478c1710d17440baa3b9204bf478e28f~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

举一个不那么恰当的例子，我们可以把硬链接想象成 JavaScript 中的对象引用：

```js
js复制代码const foo = \\{
  age: 23
\\}
const bar = foo
bar.age = 24
console.log(foo.age) // 24
```

理解了硬链接和软链接后，我们就可以开始了解 `pnpm` 的原理了。

### pnpm的原理

我们可以在两个项目中分别用 `npm` 和 `pnpm` 来安装 `express` ，看一下两者的 `node_modules` 有什么不同。

首先是 `npm` :

![image-20230206151328605](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0f4c278c828641ecae2a7396216ac7bd~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

然后是 `pnpm`:

![image-20230206151347503](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a3313b775e184ee8bf44bb87120746b0~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

通过简单的两个图的对比，我们可以明显感觉到 `pnpm` 的目录结构更加合理，因为我们的项目只依赖了 `express`，那么 `node_modules` 中就应该只存在 `express` 的文件。但问题在于 `express` 的依赖被放到哪里了呢？

其实这里的 `express` 仅仅只是一个**软链接**（注意截图中 express 文件夹右侧的小箭头），里面并不存在 `node_modules`。它的真正位置其实位于同级目录下的 `.pnpm` 文件夹中，展开 `.pnpm` 文件夹，我们可以找到其真正的位置，也就是 `.pnpm/express@4.17.1/node_modules/express`。

![image-20230206152045398](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b4455e3cc1b44b28bb491746b58512ef~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

这也代表了 `pnpm` 中的依赖规律，也是 `@version/node_modules/` 这种目录结构。并且 `express` 的依赖都在 `.pnpm/express@4.17.1/node_modules` 下面，并且这些依赖也全都是**软链接**。

也就是说，所有的依赖都是从全局 store **硬链接**到了 `node_modules/.pnpm` 下，然后之间通过**软链接**来相互依赖。

[官方文档](https://link.juejin.cn?target=https\\%3A\\%2F\\%2Fpnpm.io\\%2Fzh\\%2Fmotivation)中给出了这么一张图，可以很清晰地明白其中的原理。

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/15beb5c1b288452c94f6156d8c990b70~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp?)

将`包本身`和`依赖`放在同一个`node_module`下面，与原生 Node 完全兼容，又能将 package 与相关的依赖很好地组织到一起，不得不说 `pnpm` 的设计十分精妙。

总结：`pnpm` 使用软链接来创建依赖项的嵌套结构，将项目的直接依赖符号链接到`node_modules`的根目录，直接依赖的实际位置在`.pnpm/@/node_modules/`，依赖包中的每个文件再硬链接到`.pnpm store`。



### 为什么不是 yarn ？

事实上 yarn 只是对 npm 的一个小改进。尽管它使安装速度更快并且具有一些不错的新功能，但它却使用了和 npm 相同的扁平化 node_modules 结构。

扁平化的 node_modules 结构带来了很多问题：

1.模块可以访问它们不依赖（没有进行声明）的包 （这极其不合理！）
2.扁平化依赖的算法非常复杂
3.一些包必须复制到一个项目的 node_modules 文件夹中（太浪费空间了！）

截至目前，pnpm 具有 yarn 优于 npm 的所有优点（是的,是所有）：

1.安全： 与 Yarn 一样，pnpm 有一个特殊文件，其中包含所有已安装包的校验和，用于在执行其代码之前验证每个已安装包的完整性。
2.离线模式： pnpm 将所有下载的包 tarball 保存在本地注册表镜像中。当包在本地可用时，它从不发出请求。使用该--offline参数，可以完全



## pnpm的基本使用

`pnpm` 的使用成本非常低，因为它的基础命令和 `npm/yarn` 基本相似。

### pnpm install

跟 `npm install` 类似，安装项目下所有的依赖。但对于 `monorepo` 项目，会安装 workspace 下面所有 packages 的所有依赖。不过可以通过 `--filter` 参数来指定 package，只对满足条件的 package 进行依赖安装。

```js
js复制代码// 安装 lodash
pnpm install lodash
// 添加至 devDependencies
pnpm install lodash -D
// 添加至 dependencies
pnpm install lodash -S
```

### pnpm update

根据指定的范围将包更新到最新版本，`monorepo` 项目中可以通过 `--filter` 来指定 package。

### pnpm uninstall

在 `node_modules` 和 `package.json` 中移除指定的依赖。`monorepo` 项目同上。

### pnpm run

运行一个在 `package.json` 中定义的脚本

```js
js复制代码"scripts": \\{
    "watch": "webpack --watch"
\\}

pnpm run watch
// 或者简写为 pnpm watch （仅适用于那些不与已有的pnpm 命令相同名字的脚本）
```



## 结论

综合来看，`pnpm` 是一个相比 `npm/yarn` 更为优秀的包管理方案，推荐在新项目中使用。

原文链接：https://juejin.cn/post/7231742100844724280
