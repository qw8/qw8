---
title: vue3
date: 2024-03-10 21:02:08
categories: 
- 前端面试
tags:
- vue3
---

### vue3的新特性

#### 1、响应系统的变动

由原来的Object.defineProperty 的getter和setter，改变成为了ES2015 Proxy 作为其观察机制。

Proxy的优势：消除了以前存在的警告，使速度加倍，并节省了一半的内存开销。

#### 2、虚拟DOM重写（Virtual DOM Rewrite）

虚拟 DOM 从头开始重写，我们可以期待更多的编译时提示来减少运行时开销。重写将包括更有效的代码来创建虚拟节点。

#### 3、组件渲染的优化（优化插槽生成）

Vue2当中在父组件渲染同时，子组件也会渲染。 Vue3就可以单独渲染父组件、子组件。

#### 4、静态树提升（Static Tree Hoisting）

使用静态树提升，这意味着 Vue3 的编译器将能够检测到什么是静态组件，然后将其提升，从而降低了渲染成本。它将能够跳过未整个树结构打补丁的过程。

#### 5、静态属性提升（Static Props Hoisting）

此外，我们可以期待静态属性提升，其中 Vue3将跳过不会改变节点的打补丁过程。

总体来说：1. 更快 2. 更小 3. 更容易维护 4. 更加友好 5. 更容易使用

 

### vue3对比vue2有哪些不同？

答： https://www.cnblogs.com/ygunoil/p/14463855.html



### Proxy 相比于 defineProperty 的优势

Object.defineProperty() 的问题主要有三个：

- 不能监听数组的变化
- 必须深层遍历嵌套的对象
- 必须遍历对象的每个属性

Proxy 在 ES2015 规范中被正式加入，它有以下几个特点：

- 针对对象：针对整个对象，而不是对象的某个属性，所以也就不需要对 keys 进行遍历。这解决了上述 Object.defineProperty() 第二个问题
- 支持数组：Proxy 不需要对数组的方法进行重载，省去了众多 hack，减少代码量等于减少了维护成本，而且标准的就是最好的。

除了上述两点之外，Proxy 还拥有以下优势：

- Proxy 的第二个参数可以有 13 种拦截方法，这比起 Object.defineProperty() 要更加丰富
- Proxy 作为新标准受到浏览器厂商的重点关注和性能优化，相比之下 Object.defineProperty() 是一个已有的老方法。



### vue2为什么不使用proxy？

 答： 兼容性



### vue3性能比vue2好的原因？

1.diff算法优化

2.静态提升hoistStatic

3.事件侦听器缓存cacheHandles

https://www.cnblogs.com/ygunoil/p/14463687.html



### Vue3.0 里为什么要用 Proxy API 替代 defineProperty API？

响应式优化**（高频，重点！！！）**

这是在面试中问的最多的一个问题，无论是大厂还是中小型公司，都喜欢问，也是Vue更新的重点。

1.defineProperty API 的局限性最大原因是**它只能针对单例属性做监听**。

Vue2.x中的响应式实现正是基于defineProperty中的descriptor，对 data 中的属性做了遍历 + 递归，为每个属性设置了 getter、setter。这也就是为什么 Vue 只能对 data 中预定义过的属性做出响应的原因，在Vue中使用下标的方式直接修改属性的值或者添加一个预先不存在的对象属性是无法做到setter监听的，这是defineProperty的局限性。

2.Proxy API的监听是针对一个对象的，那么对这个对象的所有操作会进入监听操作， 这就完全可以代理所有属性，将会带来很大的性能提升和更优的代码。

Proxy 可以理解成，在目标对象之前架设一层“拦截”，外界对该对象的访问，都必须先通过这层拦截，因此提供了一种机制，可以对外界的访问进行过滤和改写。

3.响应式是惰性的

在 Vue.js 2.x 中，对于一个深层属性嵌套的对象，要劫持它内部深层次的变化，就需要递归遍历这个对象，**执行 Object.defineProperty 把每一层对象数据都变成响应式的，这无疑会有很大的性能消耗**。在 Vue.js 3.0 中，使用 Proxy API 并不能监听到对象内部深层次的属性变化，因此它的处理方式是在 getter 中去递归响应式，这样的好处是**真正访问到的内部属性才会变成响应式，简单的可以说是按需实现响应式，减少性能消耗。**基础用法：

![img](https://pics7.baidu.com/feed/42166d224f4a20a4ac217837b8d32f25730ed088.jpeg?token=ab85fef62897b5de230005159580dbae&s=21F0632201FB2E210CE15E8F0200808A)



### Vue3.0 编译做了哪些优化？**（底层，源码）**

#### 生成 Block tree

Vue.js 2.x 的数据更新并触发重新渲染的粒度是组件级的，单个组件内部 需要遍历该组件的整个 vnode 树。**在2.0里，渲染效率的快慢与组件大小成正相关：组件越大，渲染效率越慢。****并且，对于一些静态节点，又无数据更新，这些遍历都是性能浪费。**Vue.js 3.0 做到了通过编译阶段对静态模板的分析，编译生成了 Block tree。 **Block tree****是一个将模版基于动态节点指令切割的嵌套区块**，每个 区块内部的节点结构是固定的，每个区块只需要追踪自身包含的动态节点。所以，**在3.0里，渲染效率不再与模板大小成正相关，而是与模板中动态节点的数量成正相关。

![img](https://pics7.baidu.com/feed/8cb1cb13495409230918b8cebad9660eb2de4992.jpeg?token=d8b708fbbfa88364be1301c26a826a6a&s=BAA2F54C1AE0AB7C5C6524030000E0C3)

#### slot 编译优化

Vue.js 2.x 中，如果有一个组件传入了slot，那么每次父组件更新的时候，会强制使子组件update，造成性能的浪费。Vue.js 3.0 优化了slot的生成，使得非动态slot中属性的更新只会触发子组件的更新。**动态slot指的是在slot上面使用v-if，v-for，动态slot名字等会导致slot产生运行时动态变化但是又无法被子组件track的操作。****c. diff算法优化**（此知识点进大厂可能会问到，由于篇幅较长，大家可以去官网看下）



#### Vue3.0新特性 —— Composition API 与 React.js 中 Hooks的异同点（难点问题）

#### React.js 中的 Hooks 基本使用

React Hooks 允许你 "勾入" 诸如组件状态和副作用处理等 React 功能中。Hooks 只能用在函数组件中，并允许我们在不需要创建类的情况下将状态、副作用处理和更多东西带入组件中。React 核心团队奉上的采纳策略是不反对类组件，所以你可以升级 React 版本、在新组件中开始尝试 Hooks，并保持既有组件不做任何更改。案例：

![img](https://pics0.baidu.com/feed/4bed2e738bd4b31cdb2c7638af5790789f2ff8ae.jpeg?token=227aa01d9da625df78e4629dab22e444&s=01F0E9264BAEB64D4C594F8E0200708A)

useState 和 useEffect 是 React Hooks 中的一些例子，使得函数组件中也能增加状态和运行副作用。我们也可以自定义一个Hooks，它打开了代码复用性和扩展性的新大门。

#### Vue Composition API 基本使用

Vue Composition API 围绕一个新的组件选项 setup 而创建。setup() 为 Vue 组件提供了状态、计算值、watcher 和生命周期钩子。并没有让原来的 API（Options-based API）消失。允许开发者 结合使用新旧两种 API（向下兼容）。

![img](https://pics5.baidu.com/feed/fcfaaf51f3deb48f5f457428d89e8d2e2cf578a5.jpeg?token=540b94be60198116f5a6803d43073660&s=09F1EB004BAEB64D0EFC85870200E08A)

#### 原理

React hook 底层是基于链表实现，调用的条件是每次组件被render的时候都会顺序执行所有的hooks。vue hook 只会被注册调用一次，vue 能避开这些麻烦的问题，原因在于它对数据的响应是基于proxy的，对数据直接代理观察。（这种场景下，只要任何一个更改data的地方，相关的function或者template都会被重新计算，因此避开了react可能遇到的性能上的问题）。react 中，数据更改的时候，会导致重新render，重新render又会重新把hooks重新注册一次，所以react复杂程度会高一些。



### Vue3.0是如何变得更快的？（底层，源码）

#### diff方法优化

Vue2.x 中的虚拟dom是进行全量的对比。Vue3.0 中新增了静态标记（PatchFlag）：在与上次虚拟结点进行对比的时候，值对比带有patch flag的节点，并且可以通过flag 的信息得知当前节点要对比的具体内容化。

#### hoistStatic 静态提升

Vue2.x : 无论元素是否参与更新，每次都会重新创建。Vue3.0 : 对不参与更新的元素，只会被创建一次，之后会在每次渲染时候被不停的复用。

#### cacheHandlers 事件侦听器缓存

默认情况下onClick会被视为动态绑定，所以每次都会去追踪它的变化但是因为是同一个函数，所以没有追踪变化，直接缓存起来复用即可。说在后面

其实很多小伙伴都存在这样一种情况：**Vue2.x都用了一年多了，官方文档都还没有去详细过一遍，遇到问题就百度，所以Vue3.0一出就惊慌失措。**

所以我建议正确的学习姿势应该是：

当我们去接触一门新技术的时候，首要任务就是看官方文档，先大致过一遍，知道有哪些东西。开发的时候遇到问题再去针对具体的知识点细看。遇到实在搞不定的，官方文档看不懂的，再行百度也不迟。



### Vue 3.0 性能提升主要是通过哪几方面体现的？

#### 响应式系统提升

vue2在初始化的时候，对data中的每个属性使用definepropery调用getter和setter使之变为响应式对象。如果属性值为对象，还会递归调用defineproperty使之变为响应式对象。
vue3使用proxy对象重写响应式。proxy的性能本来比defineproperty好，proxy可以拦截属性的访问、赋值、删除等操作，不需要初始化的时候遍历所有属性，另外有多层属性嵌套的话，只有访问某个属性的时候，才会递归处理下一级的属性。
优势：
可以监听动态新增的属性；
可以监听删除的属性 ；
可以监听数组的索引和 length 属性；

#### 编译优化

优化编译和重写虚拟dom，让首次渲染和更新dom性能有更大的提升
vue2 通过标记静态根节点,优化 diff 算法
vue3 标记和提升所有静态根节点,diff 的时候只比较动态节点内容

Fragments, 模板里面不用创建唯一根节点,可以直接放同级标签和文本内容

静态提升

patch flag, 跳过静态节点,直接对比动态节点

缓存事件处理函数

#### 源码体积的优化

vue3移除了一些不常用的api，例如：inline-template、filter等
使用tree-shaking



#### Vue 3.0 所采用的 Composition Api 与 Vue 2.x使用的Options Api 有什么区别？

#### Options Api

包含一个描述组件选项（data、methods、props等）的对象 options；
API开发复杂组件，同一个功能逻辑的代码被拆分到不同选项 ；
使用mixin重用公用代码，也有问题：命名冲突，数据来源不清晰；

#### composition Api

vue3 新增的一组 api，它是基于函数的 api，可以更灵活的组织组件的逻辑。
解决options api在大型项目中，options api不好拆分和重用的问题。



### Proxy 相对于 Object.defineProperty 有哪些优点？

proxy的性能本来比defineproperty好，proxy可以拦截属性的访问、赋值、删除等操作，不需要初始化的时候遍历所有属性，另外有多层属性嵌套的话，只有访问某个属性的时候，才会递归处理下一级的属性。

可以监听数组变化
可以劫持整个对象
操作时不是对原对象操作,是 new Proxy 返回的一个新对象
可以劫持的操作有 13 种



### Vue 3.0 在编译方面有哪些优化？

vue.js 3.x中标记和提升所有的静态节点，diff的时候只需要对比动态节点内容；
Fragments（升级vetur插件): template中不需要唯一根节点，可以直接放文本或者同级标签
静态提升(hoistStatic),当使用 hoistStatic 时,所有静态的节点都被提升到 render 方法之外.只会在应用启动的时候被创建一次,之后使用只需要应用提取的静态节点，随着每次的渲染被不停的复用。
patch flag, 在动态标签末尾加上相应的标记,只能带 patchFlag 的节点才被认为是动态的元素,会被追踪属性的修改,能快速的找到动态节点,而不用逐个逐层遍历，提高了虚拟dom diff的性能。
缓存事件处理函数cacheHandler,避免每次触发都要重新生成全新的function去更新之前的函数
tree shaking 通过摇树优化核心库体积,减少不必要的代码量



### Vue.js 3.0 响应式系统的实现原理？

#### reactive

设置对象为响应式对象。接收一个参数，判断这参数是否是对象。不是对象则直接返回这个参数，不做响应式处理。
创建拦截器handerler，设置get/set/deleteproperty。
get
收集依赖（track）；
如果当前 key 的值是对象，则为当前 key 的对象创建拦截器 handler, 设置 get/set/deleteProperty；
如果当前的 key 的值不是对象，则返回当前 key 的值。
set
设置的新值和老值不相等时，更新为新值，并触发更新（trigger）。
deleteProperty
当前对象有这个 key 的时候，删除这个 key 并触发更新（trigger）。

#### effect

接收一个函数作为参数。作用是：访问响应式对象属性时去收集依赖

#### track

接收两个参数：target 和 key
－如果没有 activeEffect，则说明没有创建 effect 依赖
－如果有 activeEffect，则去判断 WeakMap 集合中是否有 target 属性
－WeakMap 集合中没有 target 属性，则 set(target, (depsMap = new Map()))
－WeakMap 集合中有 target 属性，则判断 target 属性的 map 值的 depsMap 中是否有 key 属性
－depsMap 中没有 key 属性，则 set(key, (dep = new Set()))
－depsMap 中有 key 属性，则添加这个 activeEffect

#### trigger

判断 WeakMap 中是否有 target 属性，WeakMap 中有 target 属性，则判断 target 属性的 map 值中是否有 key 属性，有的话循环触发收集的 effect()。



昨晚做了一个梦，梦见自己到了一家大厂面试，面试官走近房间，坐了下来：是杨溜溜吧？国际惯例，先来个自我介绍吧。

于是我巴拉巴拉开始了长达两分钟的自我介绍，与此同时，面试官边听边看我的简历，边看边皱眉，结束后问：看你之前的项目经常用到vue，对Vue熟悉吗？

我嘴角一笑，心里暗喜：幸好有专门看Vue的面试题，看来这次稳了。于是谦虚又装逼的回答：还行吧，您随便问。

于是面试官看我口气那么大，心想：哟嚯，来了一个装逼的，劳资今天就只问Vue。

 

### 来，先介绍一下Vue的响应式系统

Vue为MVVM框架，当数据模型data变化时，页面视图会得到响应更新，其原理对data的getter/setter方法进行拦截（Object.defineProperty或者Proxy），利用发布订阅的设计模式，在getter方法中进行订阅，在setter方法中发布通知，让所有订阅者完成响应。

在响应式系统中，Vue会为数据模型data的每一个属性新建一个订阅中心作为发布者，而监听器watch、计算属性computed、视图渲染template/render三个角色同时作为订阅者，对于监听器watch，会直接订阅观察监听的属性，对于计算属性computed和视图渲染template/render，如果内部执行获取了data的某个属性，就会执行该属性的getter方法，然后自动完成对该属性的订阅，当属性被修改时，就会执行该属性的setter方法，从而完成该属性的发布通知，通知所有订阅者进行更新。

 

### computed与watch的区别

计算属性computed和监听器watch**都可以观察属性的变化从而做出响应**，不同的是：

计算属性computed更多是**作为缓存功能的观察者**，它可以将一个或者多个data的属性进行复杂的计算生成一个新的值，提供给渲染函数使用，当依赖的属性变化时，computed不会立即重新计算生成新的值，而是先标记为脏数据，当下次computed被获取时候，才会进行重新计算并返回。

而监听器watch**并不具备缓存性，监听器watch提供一个监听函数，当监听的属性发生变化时，会立即执行该函数。**

 

### 介绍一下Vue的生命周期

beforeCreate：是new Vue()之后触发的第一个钩子，在当前阶段data、methods、computed以及watch上的**数据和方法都不能被访问**。

created：在实例创建完成后发生，当前阶段已经完成了数据观测，也就是**可以使用数据，更改数据**，在这里更改数据不会触发updated函数。可以做一些初始数据的获取，在当前阶段**无法与Dom进行交互**，如果非要想，可以通过vm.$nextTick来访问Dom。

beforeMount：发生在挂载之前，在这之前template模板已导入渲染函数编译。而当前阶段虚拟Dom已经创建完成，即将开始渲染。在此时**也可以对数据进行更改，不会触发updated**。

mounted：在挂载完成后发生，在当前阶段，**真实的Dom挂载完毕，数据完成双向绑定，可以访问到Dom节点，使用$refs属性对Dom进行操作。**

beforeUpdate：发生在更新之前，也就是响应式数据发生更新，虚拟dom重新渲染之前被触发，你可以在当前阶段进行更改数据，不会造成重渲染。

updated：发生在更新完成之后，当前阶段组件Dom已完成更新。要注意的是避免在此期间更改数据，因为这可能会导致无限循环的更新。

beforeDestroy：发生在实例销毁之前，在当前阶段实例完全可以被使用，我们可以在这时进行善后收尾工作，比如清除计时器。

destroyed：发生在实例销毁之后，这个时候只剩下了dom空壳。组件已被拆解，数据绑定被卸除，监听被移出，子实例也统统被销毁。

 

### 为什么组件的data必须是一个函数

一个组件可能在很多地方使用，也就是会创建很多个实例，如果data是一个对象的话，对象是引用类型，一个实例修改了data会影响到其他实例，所以data必须使用函数，为每一个实例创建一个属于自己的data，使其同一个组件的不同实例互不影响。

 

### 组件之间是怎么通信的

父子组件通信
父组件 -> 子组件：prop

子组件 -> 父组件：$on/$emit

获取组件实例：使用$parent/$children，$refs.xxx，获取到实例后直接获取属性数据或调用组件方法

兄弟组件通信
Event Bus：每一个Vue实例都是一个Event Bus，都支持$on/$emit，可以为兄弟组件的实例之间new一个Vue实例，作为Event Bus进行通信。

Vuex：将状态和方法提取到Vuex，完成共享

跨级组件通信
使用provide/inject

Event Bus：同兄弟组件Event Bus通信

Vuex：将状态和方法提取到Vuex，完成共享

 

### Vue事件绑定原理说一下

每一个Vue实例都是一个Event Bus，当子组件被创建的时候，父组件将事件传递给子组件，子组件初始化的时候是有$on方法将事件注册到内部，在需要的时候使用$emit触发函数，而对于原生native事件，使用addEventListener绑定到真实的DOM元素上。

 

### slot是什么？有什么作用？原理是什么？

slot又名插槽，是Vue的内容分发机制，组件内部的模板引擎使用slot元素作为承载分发内容的出口。插槽slot是子组件的一个模板标签元素，而这一个标签元素是否显示，以及怎么显示是由父组件决定的。

slot又分三类，默认插槽，具名插槽和作用域插槽。

#### 默认插槽

又名匿名插槽，当slot没有指定name属性值的时候一个默认显示插槽，一个组件内只有有一个匿名插槽。

#### 具名插槽

带有具体名字的插槽，也就是带有name属性的slot，一个组件可以出现多个具名插槽。

#### 作用域插槽

默认插槽、具名插槽的一个变体，可以是匿名插槽，也可以是具名插槽，该插槽的不同点是在子组件渲染作用域插槽时，可以将子组件内部的数据传递给父组件，让父组件根据子组件的传递过来的数据决定如何渲染该插槽。
实现原理：当子组件vm实例化时，获取到父组件传入的slot标签的内容，存放在vm.$slot中，默认插槽为vm.$slot.default，具名插槽为vm.$slot.xxx，xxx 为插槽名，当组件执行渲染函数时候，遇到slot标签，使用$slot中的内容进行替换，此时可以为插槽传递数据，若存在数据，则可称该插槽为作用域插槽。

 

### Vue模板渲染的原理是什么？

vue中的模板template无法被浏览器解析并渲染，因为这不属于浏览器的标准，不是正确的html语法，所有需要将template转化成一个JavaScript函数，这样浏览器就可以执行这一个函数并渲染出对应的html元素，就可以让视图跑起来了，这一个转化的过程，就成为模板编译。

模板编译又分三个阶段，解析parse，优化optimize，生成generate，最终生成可执行函数render。

parse阶段：使用大量的正则表达式对template字符串进行解析，将标签、指令、属性等转化为抽象语法树AST。
optimize阶段：遍历AST，找到其中的一些静态节点并进行标记，方便在页面重渲染的时候进行diff比较时，直接跳过这一些静态节点，优化runtime的性能。
generate阶段：将最终的AST转化为render函数字符串。



### template预编译是什么？

对于 Vue 组件来说，模板编译只会在**组件实例化的时候编译一次**，生成渲染函数之后在也不会进行编译。因此，编译对组件的 runtime 是一种性能损耗。

而模板编译的目的仅仅是将template转化为render function，这个过程，正好可以在项目构建的过程中完成，这样可以让实际组件在 runtime 时直接跳过模板渲染，进而提升性能，这个在项目构建的编译template的过程，就是预编译。

 

### 那template和jsx的有什么分别？

对于 runtime 来说，只需要保证组件存在 render 函数即可，而我们有了预编译之后，我们只需要保证构建过程中生成 render 函数就可以。

在 webpack 中，我们使用vue-loader编译.vue文件，内部依赖的vue-template-compiler模块，在 webpack 构建过程中，将template预编译成 render 函数。

与 react 类似，在添加了jsx的语法糖解析器babel-plugin-transform-vue-jsx之后，就可以直接手写render函数。

所以，template和jsx的都是render的一种表现形式，不同的是：

JSX相对于template而言，具有更高的灵活性，在复杂的组件中，更具有优势，而 template 虽然显得有些呆滞。但是 template 在代码结构上更符合视图与逻辑分离的习惯，更简单、更直观、更好维护。

 

### 说一下什么是Virtual DOM

Virtual DOM 是 DOM 节点在 JavaScript 中的一种抽象数据结构，之所以需要虚拟DOM，是因为浏览器中操作DOM的代价比较昂贵，频繁操作DOM会产生性能问题。虚拟DOM的作用是在每一次响应式数据发生变化引起页面重渲染时，**Vue对比更新前后的虚拟DOM，匹配找出尽可能少的需要更新的真实DOM，从而达到提升性能的目的。**

 

### 介绍一下Vue中的Diff算法

在新老虚拟DOM对比时

首先，对比节点本身，判断是否为同一节点，如果不为相同节点，则删除该节点重新创建节点进行替换
如果为相同节点，进行patchVnode，判断如何对该节点的子节点进行处理，先判断一方有子节点一方没有子节点的情况(如果新的children没有子节点，将旧的子节点移除)
比较如果都有子节点，则进行updateChildren，判断如何对这些新老节点的子节点进行操作（diff核心）。
匹配时，找到相同的子节点，递归比较子节点
在diff中，只对同层的子节点进行比较，放弃跨级的节点比较，使得时间复杂从O(n^3)降低值O(n)，也就是说，只有当新旧children都为多个子节点时才需要用核心的Diff算法进行同层级比较。

 

### key属性的作用是什么

在对节点进行diff的过程中，判断是否为相同节点的一个很重要的条件是key是否相等，如果是相同节点，则会尽可能的复用原有的DOM节点。所以key属性是提供给框架在diff的时候使用的，而非开发者。

 

### 说说Vue2.0和Vue3.0有什么区别

重构响应式系统，使用Proxy替换Object.defineProperty，使用Proxy优势：
可直接监听数组类型的数据变化
监听的目标为对象本身，不需要像Object.defineProperty一样遍历每个属性，有一定的性能提升
可拦截apply、ownKeys、has等13种方法，而Object.defineProperty不行
直接实现对象属性的新增/删除
新增Composition API，更好的逻辑复用和代码组织
重构 Virtual DOM
模板编译时的优化，将一些静态节点编译成常量
slot优化，将slot编译为lazy函数，将slot的渲染的决定权交给子组件
模板中内联事件的提取并重用（原本每次渲染都重新生成内联函数）
代码结构调整，更便于Tree shaking，使得体积更小
使用Typescript替换Flow



### 为什么要新增Composition API，它能解决什么问题

Vue2.0中，随着功能的增加，组件变得越来越复杂，越来越难维护，而难以维护的根本原因是Vue的API设计迫使开发者使用watch，computed，methods选项组织代码，而不是实际的业务逻辑。

另外Vue2.0缺少一种较为简洁的低成本的机制来完成逻辑复用，虽然可以minxis完成逻辑复用，但是当mixin变多的时候，会使得难以找到对应的data、computed或者method来源于哪个mixin，使得类型推断难以进行。

所以Composition API的出现，主要是也是为了解决Option API带来的问题，第一个是代码组织问题，Compostion API可以让开发者根据业务逻辑组织自己的代码，让代码具备更好的可读性和可扩展性，也就是说当下一个开发者接触这一段不是他自己写的代码时，他可以更好的利用代码的组织反推出实际的业务逻辑，或者根据业务逻辑更好的理解代码。

第二个是实现代码的逻辑提取与复用，当然mixin也可以实现逻辑提取与复用，但是像前面所说的，多个mixin作用在同一个组件时，很难看出property是来源于哪个mixin，来源不清楚，另外，多个mixin的property存在变量命名冲突的风险。而Composition API刚好解决了这两个问题。

 

### 都说Composition API与React Hook很像，说说区别

从React Hook的实现角度看，React Hook是根据useState调用的顺序来确定下一次重渲染时的state是来源于哪个useState，所以出现了以下限制

不能在循环、条件、嵌套函数中调用Hook
必须确保总是在你的React函数的顶层调用Hook
useEffect、useMemo等函数必须手动确定依赖关系
而Composition API是基于Vue的响应式系统实现的，与React Hook的相比

声明在setup函数内，一次组件实例化只调用一次setup，而React Hook每次重渲染都需要调用Hook，使得React的GC比Vue更有压力，性能也相对于Vue来说也较慢
Compositon API的调用不需要顾虑调用顺序，也可以在循环、条件、嵌套函数中使用
响应式系统自动实现了依赖收集，进而组件的部分的性能优化由Vue内部自己完成，而React Hook需要手动传入依赖，而且必须必须保证依赖的顺序，让useEffect、useMemo等函数正确的捕获依赖变量，否则会由于依赖不正确使得组件性能下降。
虽然Compositon API看起来比React Hook好用，但是其设计思想也是借鉴React Hook的。

 

### SSR有了解吗？原理是什么？

在客户端请求服务器的时候，服务器到数据库中获取到相关的数据，并且**在服务器内部将Vue组件渲染成HTML**，并且将数据、HTML一并返回给客户端，这个在服务器将数据和组件转化为HTML的过程，叫做**服务端渲染SSR**。

而当客户端拿到服务器渲染的HTML和数据之后，由于数据已经有了，客户端不需要再一次请求数据，而只需要将数据同步到组件或者Vuex内部即可。除了数据以外，HTML也结构已经有了，客户端在渲染组件的时候，也只需要将HTML的DOM节点映射到Virtual DOM即可，不需要重新创建DOM节点，这个将数据和HTML同步的过程，又叫做**客户端激活**。



### 使用SSR的好处：

#### 有利于seo

其实就是有利于爬虫来爬你的页面，因为部分页面爬虫是不支持执行JavaScript的，这种不支持执行JavaScript的爬虫抓取到的非SSR的页面会是一个空的HTML页面，而有了SSR以后，这些爬虫就可以获取到完整的HTML结构的数据，进而收录到搜索引擎中。

#### 白屏时间更短

相对于客户端渲染，服务端渲染在浏览器请求URL之后已经得到了一个带有数据的HTML文本，**浏览器只需要解析HTML，直接构建DOM树就可以**。而客户端渲染，需要先得到一个空的HTML页面，这个时候页面已经进入白屏，之后还需要经过**加载并执行 JavaScript、请求后端服务器获取数据、JavaScript 渲染页面**几个过程才可以看到最后的页面。特别是在复杂应用中，由于需要加载 JavaScript 脚本，越是复杂的应用，需要加载的 JavaScript 脚本就越多、越大，这会导致应用的首屏加载时间非常长，进而降低了体验感。
