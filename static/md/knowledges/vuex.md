---
title: vuex
date: 2022-07-28 21:02:08
categories: 
- 前端知识
tags:
- vue
- vuex
---

### 什么是vuex？

vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。



### Vuex是什么？怎么使用？

Vuex是实现组件全局状态（数据）管理的一种机制，可以方便实现组件数据之间的共享；Vuex集中管理共享的数据，易于开发和后期维护；能够高效的实现组件之间的数据共享，提高开发效率；存储在Vuex的数据是响应式的，能够实时保持页面和数据的同步；
Vuex重要核心属性包括：state,mutations,action,getters,modules.

state
Vuex 使用单一状态树,即每个应用将仅仅包含一个store 实例，但单一状态树和模块化并不冲突。存放的数据状态，不可以直接修改里面的数据。

mutations
mutations定义的方法动态修改Vuex 的 store 中的状态或数据。

action
actions可以理解为通过将mutations里面处里数据的方法变成可异步的处理数据的方法，简单的说就是异步操作数据。view 层通过 store.dispath 来分发 action。

getters
类似vue的计算属性，主要用来过滤一些数据。

modules
项目特别复杂的时候，可以让每一个模块拥有自己的state、mutation、action、getters,使得结构非常清晰，方便管理。
ps:详细使用和对其各属性的理解可以参考以下文章！

[一文吃透Vuex3的状态管理](https://blog.csdn.net/qq_44182284/article/details/125460217?spm=1001.2014.3001.5501)



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



### vuex 工作原理详解 

vuex 整体思想诞生于 flux,可其的实现方式完完全全的使用了 vue 自身的响应式设计，依赖监听、依赖收集都属于 vue 对对象 Property set get 方法的代理劫持。最后一句话结束 vuex 工作原理，vuex 中的 store 本质就是没有 template 的隐藏着的 vue 组件；

解析：vuex的原理其实非常简单，它为什么能实现所有的组件共享同一份数据？
因为vuex生成了一个store实例，并且把这个实例挂在了所有的组件上，所有的组件引用的都是同一个store实例。
store实例上有数据，有方法，方法改变的都是store实例上的数据。由于其他组件引用的是同样的实例，所以一个组件改变了store上的数据， 导致另一个组件上的数据也会改变，就像是一个对象的引用。



### vuex 是什么？怎么使用？哪种功能场景使用它？

vue 框架中状态管理。在 main.js 引入 store，注入。新建一个目录 store，….. export 。场景有：单页应用中，组件之间的状态。音乐播放、登录状态、加入购物车

main.js:

```
import store from './store'


new Vue(\\{
el:'#app',
store
\\})
```



### vuex 有哪几种属性？

有五种，分别是 State、 Getter、Mutation 、Action、 Module

```
vuex的State特性
A、Vuex就是一个仓库，仓库里面放了很多对象。其中state就是数据源存放地，对应于一般Vue对象里面的data
B、state里面存放的数据是响应式的，Vue组件从store中读取数据，若是store中的数据发生改变，依赖这个数据的组件也会发生更新
C、它通过mapState把全局的 state 和 getters 映射到当前组件的 computed 计算属性中

· vuex的Getter特性
A、getters 可以对State进行计算操作，它就是Store的计算属性
B、 虽然在组件内也可以做计算属性，但是getters 可以在多组件之间复用
C、 如果一个状态只在一个组件内使用，是可以不用getters

·  vuex的Mutation特性
Action 类似于 mutation，不同在于：Action 提交的是 mutation，而不是直接变更状态；Action 可以包含任意异步操作。
```



### vuex是什么？怎么使用？哪种功能场景使用它？

> 是什么：vue框架中状态管理:有五种，分别是 State、 Getter、Mutation 、Action、 Module
> 使用：新建一个目录store，
> 场景：单页应用中，组件之间的状态。音乐播放、登录状态、加入购物车

```js
vuex的State特性
A、Vuex就是一个仓库，仓库里面放了很多对象。其中state就是数据源存放地，对应于一般Vue对象里面的data
B、state里面存放的数据是响应式的，Vue组件从store中读取数据，若是store中的数据发生改变，依赖这个数据的组件也会发生更新
C、它通过mapState把全局的 state 和 getters 映射到当前组件的 computed 计算属性中

vuex的Getter特性
A、getters 可以对State进行计算操作，它就是Store的计算属性
B、 虽然在组件内也可以做计算属性，但是getters 可以在多组件之间复用
C、 如果一个状态只在一个组件内使用，是可以不用getters

vuex的Mutation特性
改变store中state状态的唯一方法就是提交mutation，就很类似事件。
每个mutation都有一个字符串类型的事件类型和一个回调函数，我们需要改变state的值就要在回调函数中改变。
我们要执行这个回调函数，那么我们需要执行一个相应的调用方法：store.commit。

Action 类似于 mutation，不同在于：Action 提交的是 mutation，而不是直接变更状态；
Action 可以包含任意异步操作，Action 函数接受一个与 store 实例具有相同方法和属性的 context 对象，
因此你可以调用 context.commit 提交一个 mutation，
或者通过 context.state 和 context.getters 来获取 state 和 getters。
Action 通过 store.dispatch 方法触发：eg。
store.dispatch('increment')

vuex的module特性
Module其实只是解决了当state中很复杂臃肿的时候，module可以将store分割成模块，
每个模块中拥有自己的state、mutation、action和getter
```



### vuex mutations或actions使用state中储存的数据

在控制台中输出this，发现这里this指代的是store。输出this.state.a和this.state.b，显示的是需要的数据。

总结：在vuex的index,js中，this指代的是store，因此如果要在actions和mutations中使用state中的数据，需要写成this.state.xxx，而不是this.xxx



### 不用 Vuex 会带来什么问题？

可维护性会下降，想修改数据要维护三个地方；

可读性会下降，因为一个组件里的数据，根本就看不出来是从哪来的；

增加耦合，大量的上传派发，会让耦合性大大增加，本来 Vue 用 Component 就是为了减少耦合，现在这么用，和组件化的初衷相背。



### vuex的原理

参考链接：[到底vuex是什么](https://segmentfault.com/a/1190000007516967?hmsr=toutiao.io&utm_medium=toutiao.io&utm_source=toutiao.io)



### vuex的action和mutation的异步操作和同步操作问题

参考链接：[vuex2.0 基本使用(2) --- mutation 和 action](https://www.cnblogs.com/SamWeb/p/6543931.html)



### 什么情况下使用 Vuex？

如果应用够简单，最好不要使用 Vuex，一个简单的 store 模式即可；
需要构建一个中大型单页应用时，使用Vuex能更好地在组件外部管理状态；



### Vuex和单纯的全局对象有什么区别？

Vuex 的状态存储是响应式的。当 Vue 组件从 store 中读取状态的时候，若 store 中的状态发生变化，那么相应的组件也会相应地得到高效更新。
不能直接改变 store 中的状态。改变 store 中的状态的唯一途径就是显式地提交 (commit) mutation。这样使得我们可以方便地跟踪每一个状态的变化，从而让我们能够实现一些工具帮助我们更好地了解我们的应用。



### vuex使用

1.安装

```
cnpm install vuex -S
```

2.浏览器安装扩展程序Vue.js devtools

3.在src文件夹下创建一个store.js文件

```
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex);

//要设置的全局访问的state对象
const state = \\{
    count: 0
\\};

const mutations = \\{
//自定义改变state初始值的方法，这里面的参数除了state之外还可以再传额外的参数(变量或对象);
    mutationsAddCount(state, n = 0) \\{
        return (state.count += n)
    \\},
    mutationsReduceCount(state, n = 0) \\{
        return (state.count -= n)
    \\}
\\}

export default new Vuex.Store(\\{
    state,
    mutations
\\})
```

4.在main.js中引入

```
import store from "./store";//引入vuex

new Vue(\\{
  el: '#app',
  router,
  store,
  components: \\{ App \\},
  template: '<App/>'
\\});
```

5.在组件中引用

```
<h3>\\\{\\\{$store.state.coun\\\}\\\}t}}</h3>
```

总结日期：2019.12.3



### vuex的使用 ：

首先下载 vuex

```
cnpm install vuex --save
```

在src目录中，新建一个store的文件夹来存放index.js

```
//导入vue和vuex的包 在导出store

import Vue from "vue";
import vuex from "vuex";
Vue.use(vuex);
var store=new vuex.Store(\\{
    state:\\{
    //    变量
    \\},
    mutations:\\{
    //    方法
    \\},
    getters:\\{
    //    计算
    \\},
    actions:\\{
    //    异步
    \\}
\\})
export default store
```

在main.js中引入store

```
// The Vue build version to load with the `import` command
// (runtime-only or standalone) has been set in webpack.base.conf with an alias.
import Vue from 'vue'
import App from './App'
import router from './router'
import '@vant/touch-emulator';//--- rem ---
import "./rem"
import store from "./store/index"//store
//引入vant开始
import Vant from 'vant';
import 'vant/lib/index.css';
//引入vant结束
Vue.config.productionTip = false
Vue.use(Vant);//--- Vant ---
/* eslint-disable no-new */
new Vue(\\{
  el: '#app',
  router,
  store,//store
  components: \\{ App \\},
  template: '<App/>'
\\})
```

看注释为 //store 的配置



### vuex核心概念

state 仓库 在组件中this.$store.state.参数名
mutations 直接操作state中的数据的方法 在组件中调用 this.$stote.commit("方法名",参数列表)
getter 类似于计算属性 来对state中的数据进行加工 在组件调用 this.$store.getters.方法名
actions 实现异步操作数据 在actions中调用mutations的方法 在组件中调用 this.$store.dispatch("方法名")



### vuex的运行机制：

在组件中通过this.$store.dispatch来调用actions中的方法，在action中通过commit来调用mutations中的方法，在mutations的方法中操作state中的数据，数据只要更新就会立即响应到组件上



### vuex好处：

集中存储管理程序组件的状态，避免了组件通信的麻烦
场景：适用于中大型的单页面应用
（不是说所有的地方都要用到 vuex 如果说是父传子子传父的地方使用vuex反而麻烦，对于复杂的组件通信时在使用vuex）



### vuex是什么？怎么使用？哪种功能场景使用它？

Vuex 是一个专为 Vue.js 应用程序开发的**状态管理插件**。（公共数据库）

在main.js引入store，注入。新建了一个目录`store`，….. `export`

当项目遇到以下两种场景时

1. 多个组件依赖于同一状态时。
2. 来自不同组件的行为需要变更同一状态。

解决的问题：多个视图依赖同一个状态，来自不同视图的行为需要变更同一状态，适用于中大型的单页面应用。

> 场景有：单页应用中，组件之间的状态。音乐播放、登录状态、加入购物车



### vuex有哪几种属性？

有五种，分别是 State、 Getter、Mutation 、Action、 Module

state：存放公共数据的地方；

getter：获取根据业务场景处理返回的数据；

mutations：唯一修改state的方法，修改过程是同步的；

action：异步处理，通过分发操作触发mutation；

module：将store模块分割，减少代码臃肿；



### Vue.js中ajax请求代码应该写在组件的methods中还是vuex的actions中？

如果请求来的数据是不是要被其他组件公用，仅仅在请求的组件内使用，就不需要放入vuex 的state里。

如果被其他地方复用，这个很大几率上是需要的，如果需要，请将请求放入action里，方便复用。



### 为什么 Vuex 的 mutation 中不能做异步操作？

每个mutation执行完成后都会对应到一个新的状态变更，这样devtools就可以打个快照存下来，然后就可以实现 time-travel 了。如果mutation支持异步操作，就没有办法知道状态是何时更新的，无法很好的进行状态的追踪，给调试带来困难。



### 使用vuex的优势是什么？

其实vuex中的所有功能都能够通过其他的方式进行实现，只不过vuex对这些方法进行了整合处理，使用起来更加便捷，同时也便于维护。



### Vuex中状态储存在哪里，怎么改变它？

存储在state中，改变Vuex中的状态的唯一途径就是显式地提交 (commit) mutation。



### Vuex中状态是对象时，使用时要注意什么？

因为对象是引用类型，复制后改变属性还是会影响原始数据，这样会改变state里面的状态，是不允许的，所以先用深度克隆复制对象，再修改。



### 怎么在组件中批量使用Vuex的state状态？

使用mapState辅助函数, 利用对象展开运算符将state混入computed对象中

```
import \\{mapState\\} from 'vuex'
export default\\{
    computed:\\{
        ...mapState(['price','number'])
    \\}
\\}
```



### Vuex中要从state派发一些状态出来，且多个组件使用它，该怎么做？

使用getter属性，相当Vue中的计算属性computed，只有原状态改变派生状态才会改变。

getter接收两个参数，第一个是state，第二个是getters(可以用来访问其他getter)。

```
const store = new Vuex.Store(\\{
    state: \\{
        price: 10,
        number: 10,
        discount: 0.7,
    \\},
    getters: \\{
        total: state => \\{
            return state.price * state.number
        \\},
        discountTotal: (state, getters) => \\{
            return state.discount * getters.total
        \\}
    \\},
\\});
```

然后在组件中可以用计算属性computed通过this.$store.getters.total这样来访问这些派发状态。

然后在组件中可以用计算属性computed通过this.$store.getters.total这样来访问这些派发状态。

```
computed: \\{
    total() \\{
        return this.$store.getters.total
    \\},
    discountTotal() \\{
        return this.$store.getters.discountTotal
    \\}
\\}
```




### vuex中 划分模块的好处

state 更为 容易管理 保证了store完整的状态数 又避免了相互之间的state冲突



### vuex的store特性

vuex 就是一个仓库 仓库里放了很多对象 其中state就是数据源存放地

state里面存放的数据是 响应式的 vue组件从store读取数据 若是 store中的数据发生改变 依赖这项数据的组件 也会发生更新

通过 mapState 把全局的state 和 getters 映射到当前组件的 computed中



### vuex怎么知道state是通过mutation修改还是外部直接修改的？

通过$watch监听mutation的commit函数中_committing是否为true



### Vuex中action和mutation有什么相同点？

第二参数都可以接收外部提交时传来的参数。
this.$store.dispatch('ACTION_NAME',data)和this.$store.commit('SET_NUMBER',10)



### Vuex中action通常是异步的，那么如何知道action什么时候结束呢？

在action函数中返回Promise，然后再提交时候用then处理

```
actions:\\{
    SET_NUMBER_A(\\{commit\\},data)\\{
        return new Promise((resolve,reject) =>\\{
            setTimeout(() =>\\{
                commit('SET_NUMBER',10);
                resolve();
            \\},2000)
        \\})
    \\}
\\}
this.$store.dispatch('SET_NUMBER_A').then(() => \\{
  // ...
\\})
```




### Vuex中有两个action，分别是actionA和actionB，其内都是异步操作，在actionB要提交actionA，需在actionA处理结束再处理其它操作，怎么实现？

利用ES6的async和await来实现。

```
actions:\\{
    async actionA(\\{commit\\})\\{
        //...
    \\},
    async actionB(\\{dispatch\\})\\{
        await dispatch ('actionA')//等待actionA完成
        // ... 
    \\}
\\}
```



### 在模块中，getter和mutation接收的第一个参数state，是全局的还是模块的？

第一个参数state是模块的state，也就是局部的state。



### 在v-model上怎么用Vuex中state的值？

需要通过computed计算属性来转换。

```
<input v-model="message">
// ...
computed: \\{
    message: \\{
        get () \\{
            return this.$store.state.message
        \\},
        set (value) \\{
            this.$store.commit('updateMessage', value)
        \\}
    \\}
\\}
```




### Vuex的严格模式是什么,有什么作用,怎么开启？

在严格模式下，无论何时发生了状态变更且不是由 mutation函数引起的，将会抛出错误。这能保证所有的状态变更都能被调试工具跟踪到。

在Vuex.Store 构造器选项中开启,如下：

```
const store = new Vuex.Store(\\{
    strict:true,
\\})
```



### vuex dispatch和commit的区别

dispatch：异步操作
commit ：同步操作

#### 为什么dispatch是异步而commit是同步呢？

首先，dispatch是去分发一个action的。而commit则是去调用mutations的，那这两个玩意儿又有啥区别呢

action： 用于调用mutations去变更state。
自身会返回一个promise
支持异步操作

mutations：修改数据，不支持异步，只是一个单纯的函数。

#### 为什么action支持异步而mutations不支持异步呢？

因为如果mutations支持异步的话，那数据将会变得难以跟踪。因为异步存在着很多不确定性。你不知道数据啥时候返回，不知道成功与否。所以这也注定了mutations必须是个同步操作。
但是当我们需要用到异步去获取数据提交数据的时候又该怎么办呢，action的出现就完美的解决了这些问题。所以action不能直接操作数据，他必须通过mutations去操作数据。但是他支持异步操作。所以这俩兄弟是相辅相成的。

回到上一个问题。正因为action支持异步，所以分发他的api dispatch也就是一个异步操作，而commit也就是一个同步操作了。



### router.push参数，vue3

在 Vue 3 中，`router.push` 方法用于导航到不同的路由。它可以通过多种方式传递参数，包括路径、命名路由、查询参数以及哈希等。以下是一些常见的使用方式：

1. **基本跳转**：
   ```javascript
   router.push('/path')
   ```
   直接通过路径进行跳转。

2. **命名路由**：
   如果你为路由配置了名称，可以使用 `name` 属性来指定要跳转的路由。
   ```javascript
   router.push(\\{ name: 'namedRoute' \\})
   ```

3. **传递参数**：
   如果你的路由定义中包含参数（例如 `/user/:id`），你可以这样传递参数：
   ```javascript
   router.push(\\{ path: '/user', params: \\{ id: 123 }})
   ```
   不过需要注意的是，如果你是用 `path` 来指定目标路由的话，不能同时使用 `params`，应该直接将参数嵌入到 `path` 字符串中，比如：`'/user/123'`。对于命名路由则可以使用 `params`。

4. **查询参数**：
   可以通过 `query` 属性添加查询参数，类似于 URL 中的 `?key=value`。
   ```javascript
   router.push(\\{ path: '/search', query: \\{ q: 'vue' }})
   ```
   这将会导航到类似 `/search?q=vue` 的地址。

5. **哈希定位**：
   使用 `hash` 可以指定页面加载时滚动到哪个位置。
   ```javascript
   router.push(\\{ path: '/page', hash: '#section1' \\})
   ```

6. **替换当前历史记录**：
   默认情况下，`router.push` 会向浏览器的历史记录栈中添加一条新记录。如果你想替换当前的历史记录条目而不是添加新的，可以使用 `router.replace()`。

7. **编程式导航的回调**：
   `router.push` 方法返回一个 Promise，因此你可以使用 `.then()` 或者 `async/await` 来处理异步逻辑。
   ```javascript
   router.push('/path').then(() => \\{
     // 导航完成后执行
   \\})
   ```

确保在调用 `router.push` 时已经正确设置了 Vue Router 并且可以在组件内部通过 this.$router 访问到它，或者在其他地方通过导入的方式获取路由器实例。



### vue3想传10条分组数组到下一页（不是父子组件），怎么处理比较简单、合适

选择使用 Vuex 还是重新通过接口请求数据，取决于具体的应用场景和需求。以下是两种方法的优缺点对比，帮助您决定哪种更适合您的情况：

#### 使用 Vuex

**优点**:

1. **性能优化**：如果您已经从API获取了数据并存储在Vuex中，再次切换页面时无需重新请求，减少了网络请求次数，提高了用户体验。
2. **状态集中管理**：Vuex提供了一个集中式存储管理应用的所有组件的状态，使得状态变更更加可预测和易于维护。
3. **响应式更新**：Vue组件可以订阅Vuex中的状态变化，当状态更新时，相关组件会自动重新渲染，简化了数据流动的管理。

**缺点**:

1. **内存占用**：如果数据量较大，长期存储在Vuex中可能会增加内存占用。
2. **数据一致性**：需要确保数据的一致性，尤其是在多用户或多页面同时操作同一份数据时，管理起来可能更复杂。

#### 重新通过接口请求数据

**优点**:

1. **数据实时性**：每次页面加载时都从服务器获取最新数据，保证了数据的实时性和准确性。
2. **减轻前端负担**：特别是对于大型或复杂应用，让服务器承担更多的数据处理和计算任务，前端专注于展示逻辑。
3. **简化状态管理**：避免了状态管理的复杂度，特别是对于不需要跨页面共享或短期使用的数据。

**缺点**:

1. **性能开销**：频繁的网络请求可能导致延迟和性能下降，尤其是对于移动设备或网络状况不佳的用户。
2. **额外的服务器负载**：每个页面加载都需要服务器响应，可能增加服务器资源消耗。

#### 结论

- 如果数据量不大，且需要在多个页面间共享或频繁切换时保持状态，使用 Vuex 更合适。
- 如果数据实时性要求高，或者数据量过大不适合存储在前端，每次进入页面时重新请求数据可能更合理。
- 考虑到您的场景是要传递10条分组数组到下一页，这通常意味着数据量不会太大，且可能需要快速切换且保持数据一致，因此使用 Vuex 可能是一个既简单又合适的选择，特别是如果这10条数据已经从某个地方获取过，避免了不必要的重复请求。但最终决定应基于整个应用程序的设计和性能考量。



## 在 Vue 3 中使用 Vuex 传递10条分组数组到下一页

可以通过以下步骤实现：

### 1. 安装并配置 Vuex

首先确保已经安装了 Vuex，并配置好基本的 store。

```bash
npm install vuex
```

### 2. 创建 Vuex Store

在 `store/index.js` 中定义状态（state）、突变（mutation）和动作（action）来处理数组数据。

```javascript
// store/index.js
import \\{ createStore \\} from 'vuex';

export default createStore(\\{
  state: \\{
    groupedArray: [],
  \\},
  mutations: \\{
    setGroupedArray(state, payload) \\{
      state.groupedArray = payload;
    \\},
  \\},
  actions: \\{
    updateGroupedArray(\\{ commit \\}, data) \\{
      commit('setGroupedArray', data);
    \\},
  \\},
\\});
```

### 3. 在当前页面设置分组数组

在当前页面（例如，`PageA.vue`），将分好的10条数据提交到 Vuex store。

```javascript
// PageA.vue
import \\{ useStore \\} from 'vuex';

export default \\{
  setup() \\{
    const store = useStore();

    // 假设这是已经分好的10条数据的数组
    const groupedData = yourGroupingFunction(yourArray, 10);

    // 提交到Vuex
    // 如果有异步操作
    store.dispatch('updateGroupedArray', groupedData);
    // 同步简单一点，actions里不用写updateGroupedArray
    store.commit('setGroupedArray', groupedData)

    // 导航到下一页
    navigateToNextPage();
  \\},
\\};
```

### 4. 在下一页获取分组数组

在目标页面（例如，`PageB.vue`），从 Vuex store 中获取分组好的数组。

```javascript
// PageB.vue
import \\{ useStore \\} from 'vuex';

export default \\{
  setup() \\{
    const store = useStore();
    const groupedArray = computed(() => store.state.groupedArray);

    // ... 使用 groupedArray 进行后续操作
  \\},
\\};
```

#### 这两种写法有什么区别

```
const detail = store.state.editDetail
const groupedArray = computed(() => store.state.groupedArray)
```

在 Vue 3 中，使用响应式状态管理时，`detail = store.state.editDetail` 和 `groupedArray = computed(() => store.state.groupedArray)` 这两种获取状态的方式存在显著的区别，主要体现在响应式行为和计算优化上。

##### 1. 直接访问 store.state

```javascript
const detail = store.state.editDetail
```

这种方式直接从 Vuex store 的 state 中读取数据。`detail` 变量将直接引用 `store.state.editDetail` 的值。这种方式简单直接，但是它不会触发任何依赖追踪，也就是说，如果 `editDetail` 发生变化，`detail` 不会被认为是依赖于 `editDetail` 的响应式引用，因此不会自动更新。这意味着如果你在组件中使用 `detail`，组件可能不会对 `editDetail` 的变化做出响应。

##### 2. 使用 computed 属性

```javascript
const groupedArray = computed(() => store.state.groupedArray)
```

这种方式使用 Vue 的 `computed` 功能来创建一个计算属性。`groupedArray` 将成为组件中的一个响应式计算属性，它依赖于 `store.state.groupedArray`。当 `groupedArray` 在 Vuex store 中发生变化时，由于 `computed` 属性会自动追踪依赖并缓存结果，所以 `groupedArray` 会自动更新，进而触发使用了这个计算属性的任何模板或计算属性的重新渲染。

##### 总结

- **直接访问**：简单，但不会自动触发响应式更新，适合于不需要响应式行为的场景，或者你计划手动处理更新逻辑的情况。
- **使用 computed**：能够自动追踪依赖并触发更新，适合于需要响应式行为的场景，特别是当数据变化需要立即反映在界面上时。

在现代 Vue 应用中，特别是在使用 Vuex 时，推荐使用 `computed` 属性来访问 store 中的状态，因为它可以更好地利用 Vue 的响应式系统，简化代码并提高可维护性。

### 注意事项

- 确保在 Vue 应用中已经注册了 Vuex store，通常在 `main.js` 或 `app.js` 文件中通过 `app.use(store)` 完成。
- 根据实际情况调整分组逻辑，这里假设你已经有了一个 `yourGroupingFunction` 来对数组进行分组。
- 导航函数 `navigateToNextPage()` 需要根据你的路由配置来实现，可能是 `this.$router.push(\\{ name: 'PageB' \\})` 或其他导航方式。

这样，你就能够利用 Vuex 在不同页面间共享和传递分组后的数组数据了。



### 页面刷新后vuex的state数据丢失怎么解决？

就是放在localStorage 或者就是sessionStorage ，或者借用辅助插vuex-persistedstate。



### 刷新容易丢失，直接使用sessionStorage好？还是vuex结合sessionStorage好？ 

在 Vue 3 中，决定使用哪种方式（Vuex、sessionStorage 或两者的组合）来存储和传递数据主要取决于你的具体需求，包括数据的持久性、应用的复杂度以及性能考虑。

#### 1. 使用 Vuex

Vuex 是 Vue.js 官方的状态管理库，它提供了集中式的数据管理方案，使得组件之间的状态共享变得简单。如果你的应用有多个组件需要访问这些数据，或者数据的更改涉及到复杂的逻辑，那么 Vuex 可能是一个更好的选择。

然而，Vuex 管理的状态默认情况下在页面刷新时会丢失。为了在页面刷新时保持状态，可以使用插件如 [vuex-persistedstate](https://github.com/robinvdvleuten/vuex-persistedstate) 来自动将 Vuex 的状态存储到 localStorage 或 sessionStorage 中。

#### 2. 直接使用 sessionStorage

如果你只需要在特定的页面之间传递数据，并且不需要在多个组件或页面之间共享这个数据，直接使用 sessionStorage 可以是一个更轻量级的解决方案。sessionStorage 的好处是它会在用户关闭浏览器窗口或标签页时自动清除数据，这有助于避免不必要的数据积累。

#### 3. Vuex 结合 sessionStorage

结合使用 Vuex 和 sessionStorage 可以提供一种平衡解决方案，既可以利用 Vuex 的状态管理能力，又可以确保状态在页面刷新时不丢失。你可以在 Vuex 的 mutation 或 action 中手动处理数据的持久化，例如，在状态发生改变时更新 sessionStorage。

#### 实际应用建议

- **如果数据只在少数页面间传递，且不涉及复杂的业务逻辑**，直接使用 sessionStorage 可能就足够了。
- **如果数据需要在多个组件或页面间共享，或者数据更改涉及复杂逻辑**，推荐使用 Vuex，并考虑使用 vuex-persistedstate 或自定义的持久化机制来保证数据的持久性。

无论选择哪种方法，都应该考虑到数据的安全性和隐私问题，尤其是当涉及到敏感信息时，应当采取适当的加密措施。



### 数据页面刷新丢失问题解决方案

用Vue做项目开发很久了，对于vuex能用、会用，但是因为状态脱离页面和刷新丢失两个原因，一直都有种抵触，特别是一些简单的数据都是通过query或者本地存储就解决了，然而对于一些复杂内容，不可避免的还是要使用Vuex去处理(真香)，但是刷新丢失的问题，的确叫人头大。最近闲下来，我们来研究下怎么干掉这个问题～

------

不大了解Vuex的同学，可以[先去官网溜溜](https://vuex.vuejs.org/zh/)

------

由于Vuex的数据是存储在内存中的，相当于memory cache，当页面刷新的时候内存被清空重载新内容，原来的数据就丢了，为了解决这个我们可以借助浏览器的本地存储来解决，此时我们有两个选择

- localStorage 真·持久存储
- sessionStorage 会话期存储

相比之下localStorage太持久了，不主动清除都会一直在，而sessionStorage更符合Vuex会话期状态管理的设计初衷。因此下文中统一使用sessionStorage来做补充，解决问题。

有了补充对象之后，我们要做的只有两点
1、每次在mutation中set state的时候，同步的塞到sessionStorage一份
2、状态初始化的时候，从sessionStorage中读取相应内容并作为默认值(存在的话)

看起来很简单，于是第一版方案有了，

```javascript
export default new Vuex.Store(\\{
    state: \\{
        userLevel: sessionStorage.getItem('userLevel') || ''
    \\},
    mutations: \\{
        SET_USERLEVEL(state, userLevel) \\{
            sessionStorage.setItem('userLevel', userLevel)
            state.userLevel = userLevel
        \\}
    \\},
    modules: \\{
    \\}
\\})
```

这个是解决问题了，但是每个mutation都要sessionStorage.setItem一下实在有点麻烦，而且初始化还要都getItem一遍，我很懒不想写。。。于是我们改进了第二版

```javascript
const storeMaker = (state) => \\{
    // 初始化
    Object.keys(state).map((key) => \\{
        // 判断类型获取本地存储数据
        if (typeof state[key] === 'object') \\{
            if (sessionStorage.getItem(key) && JSON.parse(sessionStorage.getItem(key))) \\{
                state[key] = JSON.parse(sessionStorage.getItem(key))
            \\}
        \\} else if (typeof state[key] === 'number') \\{
            if (sessionStorage.getItem(key) && parseInt(sessionStorage.getItem(key))) \\{
                state[key] = parseInt(sessionStorage.getItem(key))
            \\}
        \\} else \\{
            if (sessionStorage.getItem(key)) \\{
                state[key] = sessionStorage.getItem(key)
            \\}
        \\}
    \\})

    // 重写set处理
    return new Proxy(state, \\{
        set: function(target, key, value) \\{
            let temp = value
            if (typeof temp === 'object') \\{
                temp = JSON.stringify(temp)
            \\}

            sessionStorage.setItem(key, temp)
            return Reflect.set(target, key, value)
        \\}
    \\})
\\}

export default new Vuex.Store(\\{
    state: storeMaker(\\{
        userLevel: ''
    \\}),
    mutations: \\{
        SET_USERLEVEL(state, userLevel) \\{
            state.userLevel = userLevel
        \\}
    \\},
    modules: \\{
    \\}
\\})
```

内容不多，主要定义了一个storeMaker的函数实现了两个功能
1、对传入的state初始值判断类型，并尝试从sessionStorage中读取数据替换默认值
2、通过Proxy重置state的set逻辑，添加同步保存到sessionStorage的逻辑

其实本来可以通过Proxy重置get逻辑处理取值的问题，但是由于vuex本身通过defineProperty函数重置了get逻辑，在这里使用proxy覆盖会有冲突，因此在初始化的时候直接读取sessionStorage。

同时也存在一些问题：
1、目前只处理了一级属性，二级以下属性没处理，对于初始化会有偏差。对于这点处理层级也不宜过深，因为过深的结构设计本来就并不合理，两层基本也足够了。基本处理就是对于state的每个key再去遍历一遍，如果是object(非null非数组非空对象)就重新proxy一下
2、可以尝试打包成npm包，或者写成Vuex的插件形式，方便使用
3、等等

～状态不好，先写到这，大家有兴趣一起来讨论，清清脑子再来补充～

联想到的一些点：
1、memory cache和disk cache？内存怎么清理？js垃圾回收机制？
2、SessionStorage怎么做到会话期缓存？
3、session机制怎么回事？
4、http的无状态？状态保持？客户端保持？服务端保持？
5、等等等等
发散开看看，一个地方真的能学到很多东西。

原文链接：https://www.cnblogs.com/heioray/p/10284268.html



### 封装vuex，使其结合缓存持久化，并且在组件中方便使用

#### chatGPT

    在使用Vuex时结合缓存持久化，可以通过以下几个步骤来封装：

1. 安装依赖：安装vuex和localforage（或其他合适的缓存库）。

```bash
npm install vuex localforage
```

2. 创建一个新的store.js文件，用于封装Vuex。

```javascript
import Vue from 'vue';
import Vuex from 'vuex';
import localforage from 'localforage';

Vue.use(Vuex);

// 初始化缓存库
localforage.config(\\{
  driver: localforage.LOCALSTORAGE, // 在本地存储中使用localStorage作为驱动程序
  name: 'myApp' // 设置缓存库名称，可以根据你的应用名称进行设置
\\});

// 创建并导出store实例
export default new Vuex.Store(\\{
  state: \\{
    // 初始化state
    // ...
  \\},
  mutations: \\{
    // 定义mutations
    // ...
  \\},
  actions: \\{
    // 定义actions
    // ...
  \\},
  plugins: [
    store => \\{
      // 在刷新时从缓存中恢复state
      localforage.getItem('vuex').then(value => \\{
        if (value) \\{
          store.replaceState(value);
        \\}
      \\});

      // 在每次mutation后将state缓存起来
      store.subscribe((mutation, state) => \\{
        localforage.setItem('vuex', state);
      \\});
    \\}
  ]
\\});
```

在上面的代码中，我们使用了localforage作为缓存库，并且在每次mutation后将state缓存起来，在刷新时从缓存中恢复state。

3. 在主应用文件（如main.js）中引入store.js并挂载到Vue实例上。

```javascript
import Vue from 'vue';
import App from './App.vue';
import store from './store';

new Vue(\\{
  store,
  render: h => h(App)
\\}).$mount('#app');
```

现在，我们已经将Vuex结合缓存持久化封装好了。

在组件中，你可以像正常使用Vuex一样使用它：

```javascript
// 使用mapState和mapActions辅助函数获取state和actions
import \\{ mapState, mapActions \\} from 'vuex';

export default \\{
  computed: \\{
    ...mapState(['count'])
  \\},
  methods: \\{
    ...mapActions(['increment'])
  \\}
\\};
```

这样，你就可以在组件中通过this.count访问state，并且通过this.increment()来调用increment action。所有的状态更新都会被自动地缓存到本地存储中，以确保在刷新页面后能够重新加载。

需要注意的是，由于缓存是异步的，所以在应用初始化加载时，可能会出现短暂的闪屏情况。如果需要避免这种情况，可以在应用启动之前显示一个加载提示，然后在缓存加载完成后隐藏加载提示。



### 在vue3中vuex使用vuex-persistedstate实现持久化

在 Vue 3 中使用 Vuex 结合 `vuex-persistedstate` 插件实现状态持久化，主要涉及以下几个步骤：

1. **安装 Vuex 和 Vuex Persisted State**

   如果你还没有安装 Vuex 和 `vuex-persistedstate`，可以通过 npm 或 yarn 安装它们：

   ```bash
   npm install vuex @vueuse/core
   npm install vuex-persistedstate
   ```

   或者使用 yarn：

   ```bash
   yarn add vuex @vueuse/core
   yarn add vuex-persistedstate
   ```

   注意：`@vueuse/core` 不是必需的，它是用于提供一些额外的组合式 API 实用工具的，但与持久化状态无关。

2. **配置 Vuex Store**

   在你的 Vuex store 配置中，你需要引入并使用 `vuex-persistedstate` 插件。在你的 `store/index.js` 文件中，这样做：

   ```javascript
   // store/index.js
   import \\{ createStore \\} from 'vuex';
   import createPersistedState from 'vuex-persistedstate';

   export default createStore(\\{
     state: \\{
       count: 0,
       user: null
     \\},
     mutations: \\{
       increment(state) \\{
         state.count++;
       \\},
       setUser(state, user) \\{
         state.user = user;
       \\}
     \\},
     plugins: [
       createPersistedState(\\{
         // 配置项
         key: 'your-storage-key', // 自定义存储的 key
         storage: window.localStorage, // 或 sessionStorage, 或其他自定义的存储
         reducer: state => (\\{ // 只保存部分状态
           count: state.count,
           user: state.user
         \\}),
         paths: ['count', 'user'] // 或者指定要保存哪些状态路径
       \\})
     ]
   \\});
   ```

   在上面的配置中，`createPersistedState` 插件接收一个对象作为配置，你可以自定义存储的 key、使用的存储类型（如 `localStorage` 或 `sessionStorage`）、以及要持久化的状态字段。

3. **在主应用中使用 Vuex Store**

   然后，在你的 `main.js` 或 `main.ts` 文件中，引入 store 并使用它：

   ```javascript
   // main.js
   import \\{ createApp \\} from 'vue';
   import App from './App.vue';
   import store from './store';

   const app = createApp(App);
   app.use(store);
   app.mount('#app');
   ```

4. **测试持久化**

   现在，每次你在 Vuex store 中更改状态，这些更改都会被保存到你选择的存储中（例如 localStorage）。当应用程序重新加载时，这些状态会被自动恢复。

   你可以通过浏览器的开发者工具检查 localStorage，确认是否已经保存了对应的数据。

以上就是在 Vue 3 中使用 Vuex 和 `vuex-persistedstate` 实现状态持久化的基本流程。根据实际需求，你可能还需要对插件的配置进行更多的定制。

在 `vuex-persistedstate` 插件中，`reducer` 是一个可选配置项，它允许你定义一个函数来决定哪些状态会被持久化到存储（如 `localStorage` 或 `sessionStorage`）中。这个函数接收 Vuex store 的当前状态作为参数，并返回一个新的对象，该对象包含了你希望保存的状态片段。



### reducer解释

### Reducer 的作用

- **选择性持久化**：通过 `reducer` 函数，你可以精确控制哪些状态需要被持久化。这对于大型应用尤其有用，因为并不是所有状态都需要被保存下来。
  
- **减少存储负担**：只保存必要的状态可以减少浏览器的存储使用，提高性能。

- **数据清理**：可以在返回的对象中对状态进行一些预处理或清理工作，比如移除敏感信息等。

### 使用示例

假设你有一个 Vuex store 的状态如下：

```javascript
const state = \\{
  user: \\{ name: 'John', age: 30 \\},
  settings: \\{ theme: 'dark', language: 'en' \\},
  tempData: \\{\\} // 不想持久化的临时数据
\\};
```

如果你只想持久化 `user.name` 和 `settings.theme`，你可以这样定义 `reducer`：

```javascript
import createPersistedState from 'vuex-persistedstate';

const persistedState = createPersistedState(\\{
  reducer(state) \\{
    return \\{
      userName: state.user.name,
      theme: state.settings.theme
    \\};
  \\}
\\});
```

在这个例子中，只有 `user.name` 和 `settings.theme` 这两个属性会被持久化到存储中。其他状态（例如 `tempData` 和 `user.age`）将不会被保存。

### 注意事项

- 如果同时指定了 `paths` 和 `reducer`，那么 `reducer` 的优先级更高，即 `reducer` 中指定的状态会覆盖 `paths` 中的配置。
  
- 在某些情况下，`reducer` 可能比 `paths` 提供更灵活的选择逻辑，特别是当你要根据复杂的条件来决定哪些状态应该被持久化时。

总之，`reducer` 是一种强大的工具，可以帮助你更好地管理哪些状态需要被持久化以及如何组织这些状态，确保你的应用程序在用户刷新页面或者重新打开浏览器时能够恢复到之前的状态。

#### 解释一下paths: ['count', 'user']

在 `vuex-persistedstate` 的配置中，`paths` 选项是一个数组，它指定了你想要持久化的 Vuex store 中的具体状态路径。这是一个非常有用的特性，特别是当你不想将整个 store 状态都保存到本地存储时。

当你设置 `paths: ['count', 'user']`，这意味着：

- **'count'**：表示你希望将名为 `count` 的状态属性值保存到本地存储中。这通常意味着在你的 Vuex store 的 `state` 对象中存在一个名为 `count` 的属性。
  
- **'user'**：同样地，这表示你希望将名为 `user` 的状态属性值保存到本地存储中。

这种配置方式允许你精细控制哪些状态需要被持久化。例如，假设你的 store 状态如下：

```javascript
state: \\{
  count: 0,
  user: null,
  sensitiveData: 'some-secret'
\\}
```

你可能不希望 `sensitiveData` 这样的敏感信息被保存到本地存储中，因为它可能包含用户密码或其他重要数据。在这种情况下，你只需要在 `paths` 数组中列出你希望持久化的状态路径，比如 `['count', 'user']`。

这样做有几个好处：

1. **安全性**：通过排除敏感数据，你增加了应用的安全性，避免了在本地存储中留下潜在的安全隐患。

2. **性能**：只保存必要的状态可以减少读写本地存储的频率和数据量，从而提高应用性能。

3. **灵活性**：你可以根据需要动态调整哪些状态需要持久化，而不必修改其他代码。

总之，`paths` 选项提供了对 Vuex store 状态持久化过程的细粒度控制，使你能够根据具体的应用需求来优化数据存储策略。



### 在vue2中vuex使用vuex-persistedstate实现持久化

封装 Vuex 以结合缓存持久化并在组件中方便使用，你可以遵循以下步骤来实现：

#### 步骤 1: 安装必要的库

首先，你需要安装 `vuex` 和一个用于缓存持久化的库，比如 `vuex-persistedstate`。你可以使用 npm 或 yarn 进行安装：

```bash
npm install vuex vuex-persistedstate --save  
# 或者  
yarn add vuex vuex-persistedstate
```

#### 步骤 2: 创建 Vuex Store

在 Vue 项目中，创建一个新的文件（例如 `store.js`）来定义你的 Vuex store。在这个文件中，导入 Vuex 和 `vuex-persistedstate` 插件，并定义你的 store：

```javascript
import Vue from 'vue';  
import Vuex from 'vuex';  
import createPersistedState from 'vuex-persistedstate';  
  
Vue.use(Vuex);  
  
const store = new Vuex.Store(\\{  
  state: \\{  
    // 定义你的状态  
  \\},  
  mutations: \\{  
    // 定义你的 mutations  
  \\},  
  actions: \\{  
    // 定义你的 actions  
  \\},  
  modules: \\{  
    // 定义你的模块（如果有的话）  
  \\},  
  plugins: [  
    createPersistedState(\\{  
      // 配置选项，例如存储位置（localStorage 或 sessionStorage）  
    \\})  
  ]  
\\});  
  
export default store;
```

#### 步骤 3: 在 Vue 实例中使用 Vuex Store

在你的 Vue 实例中，导入并使用刚才创建的 Vuex store：

```javascript
import Vue from 'vue';  
import App from './App.vue';  
import store from './store';  
  
new Vue(\\{  
  store,  
  render: h => h(App)  
\\}).$mount('#app');
```

#### 步骤 4: 在组件中使用 Vuex

现在，你可以在你的 Vue 组件中通过 `this.$store` 访问 Vuex store。为了更方便地使用 Vuex，你可以使用 `mapState`、`mapMutations` 和 `mapActions` 辅助函数来映射 state、mutations 和 actions 到组件的计算属性和方法上。

例如，在你的组件中：

```javascript
<template>  
  <div>  
    <p>\\\{\\\{ count\\\}\\\} }}</p>  
    <button @click="incrementCount">Increment</button>  
  </div>  
</template>  
  
<script>  
import \\{ mapState, mapMutations \\} from 'vuex';  
  
export default \\{  
  computed: \\{  
    ...mapState(['count']) // 映射 state 中的 count 到组件的计算属性上  
  \\},  
  methods: \\{  
    ...mapMutations(['incrementCount']) // 映射 mutations 中的 incrementCount 到组件的方法上 
  \\}
\\};
</script>
```

#### 步骤 5: 测试缓存持久化

现在，当你更改 Vuex store 中的状态时，这些更改应该会被持久化到浏览器的 localStorage 或 sessionStorage 中（取决于你在 `vuex-persistedstate` 插件中的配置）。你可以尝试刷新页面，看看状态是否仍然保持不变。

这样，你就成功地封装了 Vuex 以结合缓存持久化，并在组件中方便地使用 Vuex 了。



### vuex使用vuex-persistedstate缓存在qiankun中怎么封装

支持有的状态使用sessionStorage，有的状态使用localStorage
数据还需要在每个子应用中，或者主应用中，都可以更新，都可以获取，举例说明使用方法
使得每个子应用分类清晰，代码统一，方便管理维护

```
// 一个子应用
createPersistedState(\\{
      // 配置项
      key: 'vuex', // 自定义存储的 key
      storage: window.localStorage, // 或 sessionStorage, 或其他自定义的存储
      reducer: (state) => (\\{
        // 只保存部分状态
        isPC: state.isPC,
        isList: state.isList,
        groupedArray: state.groupedArray,
        editDetail: state.editDetail,
      \\}),
      paths: ['isPC', 'isList', 'groupedArray', 'editDetail'], // 或者指定要保存哪些状态路径
    \\}),

// 另一个子应用
createPersistedState(\\{
      // 配置项
      key: 'vuex', // 自定义存储的 key
      storage: window.sessionStorage, // 或 sessionStorage, 或其他自定义的存储
      reducer: (state) => (\\{
        // 只保存部分状态
        curProduct: state.curProduct,
        curCustomer: state.curCustomer,
      \\}),
    \\}),
```

在 Qiankun 的微前端架构中，子应用之间的状态管理和数据共享可以通过 `vuex` 配合 `vuex-persistedstate` 插件来实现。为了实现不同子应用使用不同的存储方式（`localStorage` 或 `sessionStorage`），同时保证状态的隔离性、清晰性，并且能够在每个子应用之间或主应用中进行更新和获取，可以通过以下步骤封装。

### 1. **封装 `vuex-persistedstate` 配置**

首先，我们需要为每个子应用创建一个独立的 `vuex-persistedstate` 配置，确保不同的存储方式和状态保存需求清晰分离。

### 2. **配置多个存储**

- 对于某些子应用，我们使用 `localStorage` 来持久化状态（适合需要长期保留的数据）。
- 对于其他子应用，使用 `sessionStorage`（适合需要在会话结束后清除的数据）。

### 3. **封装管理配置**

我们可以为每个子应用封装一个 `createPersistedState` 的配置方法，这样方便统一管理和维护。

#### 示例：主应用和子应用 `vuex-persistedstate` 配置封装

首先，为每个子应用创建不同的 `vuex` 配置，设置不同的 `storage` 和 `reducer`。

```
javascript// src/utils/vuex-persistedstate.js

import createPersistedState from 'vuex-persistedstate';

// 配置1：子应用A
export const persistedStateAppA = createPersistedState(\\{
  key: 'vuex-app-a',  // 为每个子应用定义不同的 key，避免冲突
  storage: window.localStorage,  // 使用 localStorage
  reducer: (state) => (\\{
    isPC: state.isPC,
    isList: state.isList,
    groupedArray: state.groupedArray,
    editDetail: state.editDetail,
  \\}),
  paths: ['isPC', 'isList', 'groupedArray', 'editDetail'],  // 要持久化的状态路径
\\});

// 配置2：子应用B
export const persistedStateAppB = createPersistedState(\\{
  key: 'vuex-app-b',
  storage: window.sessionStorage,  // 使用 sessionStorage
  reducer: (state) => (\\{
    curProduct: state.curProduct,
    curCustomer: state.curCustomer,
  \\}),
  paths: ['curProduct', 'curCustomer'],
\\});

// 在主应用中共享配置
export const sharedPersistedState = createPersistedState(\\{
  key: 'vuex-main',  // 主应用的持久化配置
  storage: window.localStorage,  // 可以根据需要使用不同的存储方式
  reducer: (state) => (\\{
    mainState1: state.mainState1,
    mainState2: state.mainState2,
  \\}),
  paths: ['mainState1', 'mainState2'],
\\});
```

#### 4. **在每个子应用中引入并使用 `vuex-persistedstate`**

在每个子应用的 `store` 中使用不同的配置。

##### 子应用A的 `store` 配置：

```
javascript// 子应用A store.js
import Vue from 'vue';
import Vuex from 'vuex';
import \\{ persistedStateAppA \\} from './utils/vuex-persistedstate';

Vue.use(Vuex);

export default new Vuex.Store(\\{
  state: \\{
    isPC: true,
    isList: false,
    groupedArray: [],
    editDetail: \\{\\},
  \\},
  mutations: \\{
    setPC(state, value) \\{
      state.isPC = value;
    \\},
    setList(state, value) \\{
      state.isList = value;
    \\},
    setGroupedArray(state, array) \\{
      state.groupedArray = array;
    \\},
    setEditDetail(state, detail) \\{
      state.editDetail = detail;
    \\},
  \\},
  plugins: [persistedStateAppA],  // 使用子应用A的持久化配置
\\});
```

##### 子应用B的 `store` 配置：

```
javascript// 子应用B store.js
import Vue from 'vue';
import Vuex from 'vuex';
import \\{ persistedStateAppB \\} from './utils/vuex-persistedstate';

Vue.use(Vuex);

export default new Vuex.Store(\\{
  state: \\{
    curProduct: \\{\\},
    curCustomer: \\{\\},
  \\},
  mutations: \\{
    setCurProduct(state, product) \\{
      state.curProduct = product;
    \\},
    setCurCustomer(state, customer) \\{
      state.curCustomer = customer;
    \\},
  \\},
  plugins: [persistedStateAppB],  // 使用子应用B的持久化配置
\\});
```

### 5. **数据共享与更新**

为了让数据在主应用和各个子应用之间共享，可以通过以下方式进行更新和获取：

- **主应用管理共享状态**：主应用可以通过 `Vuex` 中的共享状态和 `vuex-persistedstate` 保持跨子应用的数据同步。主应用也可以通过 `window.localStorage` 或 `window.sessionStorage` 管理这些状态。
- **子应用间状态共享**：子应用可以通过事件总线或者 `window.localStorage`、`window.sessionStorage` 等方式进行通信，或者通过将某些状态放入 `vuex` 中，并通过跨应用的通信机制（如广播）来共享状态。

例如：

```
javascript// 在主应用中获取子应用A的持久化数据
const appAData = JSON.parse(window.localStorage.getItem('vuex-app-a'));

// 在主应用中设置数据
window.localStorage.setItem('vuex-app-a', JSON.stringify(\\{ isPC: true, isList: true \\}));
```

### 6. **注意事项**

- **避免 key 冲突**：每个子应用的 `key` 应该是唯一的，这样才能保证每个子应用的 `vuex` 状态能够单独持久化，而不会发生冲突。
- **跨子应用通信**：如果子应用间需要共享状态，除了持久化存储，还可以考虑使用 `window` 对象来实现跨应用通信。例如，在子应用A中更新状态后，可以通过 `window.dispatchEvent` 触发事件，通知其他子应用更新。
- **性能考虑**：存储方式选择 `localStorage` 和 `sessionStorage` 时，要注意它们的存储大小限制以及存储的生命周期（`sessionStorage` 会在页面会话结束后清除）。

### 总结

通过上述封装方法，我们可以在 Qiankun 微前端架构中实现每个子应用根据需要选择不同的持久化存储方式，同时保证代码清晰、易于管理和维护。每个子应用可以拥有独立的存储配置，而主应用和子应用之间的数据共享和更新也变得灵活且高效。



### 子应用c中既需要persistedStateAppA 又需要persistedStateAppB 

在 Qiankun 微前端架构中，如果子应用 C 既需要 `persistedStateAppA` 配置（使用 `localStorage`）又需要 `persistedStateAppB` 配置（使用 `sessionStorage`），我们可以通过组合多个 `vuex-persistedstate` 配置来满足这个需求。

### 解决方案

1. **多个插件组合**： 可以在子应用 C 的 `store` 中同时使用多个 `vuex-persistedstate` 插件，每个插件有不同的存储方式和不同的状态路径。这样，子应用 C 可以同时使用 `localStorage` 和 `sessionStorage` 存储不同的状态。

### 实现步骤

#### 1. **创建多个 `vuex-persistedstate` 配置**

我们已经有了 `persistedStateAppA` 和 `persistedStateAppB` 配置，接下来需要在子应用 C 的 `store` 中引入这两个配置。

```
javascript// src/utils/vuex-persistedstate.js

import createPersistedState from 'vuex-persistedstate';

// 配置1：子应用A使用 localStorage
export const persistedStateAppA = createPersistedState(\\{
  key: 'vuex-app-a',  // 为每个子应用定义不同的 key，避免冲突
  storage: window.localStorage,  // 使用 localStorage
  reducer: (state) => (\\{
    isPC: state.isPC,
    isList: state.isList,
    groupedArray: state.groupedArray,
    editDetail: state.editDetail,
  \\}),
  paths: ['isPC', 'isList', 'groupedArray', 'editDetail'],  // 要持久化的状态路径
\\});

// 配置2：子应用B使用 sessionStorage
export const persistedStateAppB = createPersistedState(\\{
  key: 'vuex-app-b',
  storage: window.sessionStorage,  // 使用 sessionStorage
  reducer: (state) => (\\{
    curProduct: state.curProduct,
    curCustomer: state.curCustomer,
  \\}),
  paths: ['curProduct', 'curCustomer'],
\\});
```

#### 2. **在子应用 C 的 `store` 中同时使用多个 `vuex-persistedstate` 配置**

在子应用 C 中，我们需要将 `persistedStateAppA` 和 `persistedStateAppB` 插件都加入到 `Vuex` 的插件中。这样，子应用 C 就可以同时使用 `localStorage` 和 `sessionStorage`。

```
javascript// 子应用C store.js
import Vue from 'vue';
import Vuex from 'vuex';
import \\{ persistedStateAppA, persistedStateAppB \\} from './utils/vuex-persistedstate';

Vue.use(Vuex);

export default new Vuex.Store(\\{
  state: \\{
    isPC: true,
    isList: false,
    groupedArray: [],
    editDetail: \\{\\},
    curProduct: \\{\\},
    curCustomer: \\{\\},
  \\},
  mutations: \\{
    setPC(state, value) \\{
      state.isPC = value;
    \\},
    setList(state, value) \\{
      state.isList = value;
    \\},
    setGroupedArray(state, array) \\{
      state.groupedArray = array;
    \\},
    setEditDetail(state, detail) \\{
      state.editDetail = detail;
    \\},
    setCurProduct(state, product) \\{
      state.curProduct = product;
    \\},
    setCurCustomer(state, customer) \\{
      state.curCustomer = customer;
    \\},
  \\},
  plugins: [
    persistedStateAppA,  // 使用 persistStateAppA 配置（localStorage）
    persistedStateAppB   // 使用 persistStateAppB 配置（sessionStorage）
  ],
\\});
```

#### 3. **如何管理和访问不同存储的数据**

- **子应用 C 中的数据访问**：

  - 对于

     

    ```
    localStorage
    ```

     

    存储的数据，可以通过

     

    ```
    window.localStorage
    ```

     

    获取：

    ```
    javascriptconst appAState = JSON.parse(window.localStorage.getItem('vuex-app-a'));
    ```

  - 对于

     

    ```
    sessionStorage
    ```

     

    存储的数据，可以通过

     

    ```
    window.sessionStorage
    ```

     

    获取：

    ```
    javascriptconst appBState = JSON.parse(window.sessionStorage.getItem('vuex-app-b'));
    ```

- **子应用 C 中的状态更新**： 在子应用 C 中，您可以直接通过 `Vuex` 的 `mutations` 来更新状态：

  ```
  javascript// 更新子应用C的状态
  this.$store.commit('setPC', true);
  this.$store.commit('setCurProduct', product);
  ```

#### 4. **跨子应用的通信和同步**

如果主应用或者其他子应用需要与子应用 C 共享或更新这些状态，您可以通过以下方式进行通信：

- **通过 `window.localStorage` 或 `window.sessionStorage` 实现跨子应用通信**：在一个子应用中更新状态后，其他子应用可以监听这些存储的变化，或者通过事件机制（`window.dispatchEvent`）进行同步。

  例如，在子应用 A 中更新某些状态后，其他子应用可以监听 `localStorage` 或 `sessionStorage` 的变化：

  ```
  javascript// 子应用A中更新localStorage
  window.localStorage.setItem('vuex-app-a', JSON.stringify(newState));
  
  // 子应用C监听更新
  window.addEventListener('storage', (event) => \\{
    if (event.key === 'vuex-app-a') \\{
      const updatedState = JSON.parse(event.newValue);
      // 更新store状态
      this.$store.commit('setPC', updatedState.isPC);
    \\}
  \\});
  ```

#### 5. **其他注意事项**

- **性能**：多个 `vuex-persistedstate` 插件同时存在时，确保每个插件配置的 `key` 唯一，以避免冲突。每个子应用的状态应该分别存储，保证数据的隔离。
- **数据同步**：如果你需要跨子应用共享数据，确保每个子应用在初始化时能够根据需要同步其他子应用的数据。例如，使用 `localStorage` 来持久化存储一些公共数据，其他子应用可以通过监听 `storage` 事件来获取更新。
- **清理数据**：对于一些只在当前会话中需要的数据，可以使用 `sessionStorage`。当会话结束时，数据会自动清除。对于长期需要存储的数据，使用 `localStorage` 更为合适。

### 总结

在子应用 C 中同时使用 `persistedStateAppA` 和 `persistedStateAppB` 是完全可行的，只需将两个插件组合在一起即可。通过这种方式，可以根据需求选择不同的存储方式（如 `localStorage` 或 `sessionStorage`）来持久化不同的状态，并且保持子应用的状态清晰和独立。



### 项目代码

persistedstate.js

```
import createPersistedState from 'vuex-persistedstate'

/*参数说明
  key：为每个子应用定义不同的 key，避免冲突
  storage：存储方式
  reducer：精确控制哪些状态需要被持久化
*/

// 全部子应用，共享使用localStorage
export const vuexLocal = createPersistedState(\\{
  key: 'vuex',
  storage: window.localStorage,
  reducer: (state) => (\\{
    isPC: state.isPC,
    isList: state.isList,
  \\}),
\\})

// 全部子应用，共享使用sessionStorage
export const vuexSession = createPersistedState(\\{
  key: 'vuex',
  storage: window.sessionStorage,
  reducer: (state) => (\\{
    curProduct: state.curProduct,
  \\}),
\\})

// content-hub子应用，使用sessionStorage
export const contentSession = createPersistedState(\\{
  key: 'content',
  storage: window.sessionStorage,
  reducer: (state) => (\\{
    groupedArray: state.groupedArray,
    editDetail: state.editDetail,
  \\}),
\\})

// marketing子应用，使用sessionStorage
export const marketingSession = createPersistedState(\\{
  key: 'marketing',
  storage: window.sessionStorage,
  reducer: (state) => (\\{
    curCustomer: state.curCustomer,
  \\}),
\\})
```

index.js

```
import \\{ createStore \\} from 'vuex'
import \\{ vuexLocal, contentSession \\} from './persistedstate'

export const store = createStore(\\{
  state: \\{
    isPC: false, // 是否为PC端
    isList: false, // 是否为列表模式
    groupedArray: [], // 分区的分组数组
    editDetail: \\{\\}, // 分区的编辑回显数据
  \\},
  getters: \\{\\},
  mutations: \\{
    // 更新是否为PC端
    setIsPC(state, payload) \\{
      state.isPC = payload
    \\},
    // 更新列表模式
    setIsList(state, payload) \\{
      state.isList = payload
    \\},
    // 更新分区的分组数组
    setGroupedArray(state, payload) \\{
      state.groupedArray = payload
    \\},
    // 更新分区的编辑回显数据
    setEditDetail(state, payload) \\{
      state.editDetail = payload
    \\},
  \\},
  actions: \\{\\},
  modules: \\{\\},
  plugins: [vuexLocal, contentSession],
\\})
```

子应用在每次加载时，检查并使用最新的各个缓存数据来初始化state，请在补充恢复方法initializeStore，使得plugins: [vuexLocal, contentSession],中的所有数据都更新

参考代码

main.js中

```
instance.use(store)
// 初始化 store
store.dispatch('initializeStore')
```

index.js中

```
mutations: \\{
  setIsPC(state, payload) \\{
    state.isPC = payload;
  \\},
  setIsList(state, payload) \\{
    state.isList = payload;
  \\},
  initializeState(state, persistedData) \\{
    // 检查 persistedData 是否存在，并通过直接触发 mutations 更新 state
    if (persistedData) \\{
      // 调用 mutations 来修改 state
      state.isPC = persistedData.isPC;
      state.isList = persistedData.isList;
    \\}
  \\}
\\},
actions: \\{
  initializeStore(\\{ commit \\}) \\{
    const persistedData = JSON.parse(window.localStorage.getItem('vuex'));
    
    // 通过 commit 来触发 mutations
    commit('initializeState', persistedData);
  \\}
\\}
```

#### 解决方法1

根据您提供的代码，`vuex-persistedstate` 插件已经被配置为自动保存和恢复 Vuex store 的状态。通常情况下，当插件被正确配置并添加到 Vuex store 中时，它会在页面加载或应用启动时自动从存储（如 `localStorage` 或 `sessionStorage`）中读取数据，并将这些数据合并到 Vuex store 的初始状态中。

但是，如果您希望确保在每次应用加载时明确地初始化 store 状态，可以创建一个 `initializeStore` action 来手动处理这个过程。然而，由于 `vuex-persistedstate` 会自动处理状态的持久化，您需要确保不与插件的行为冲突。下面是一个调整后的 `index.js` 版本，包括了 `initializeStore` action：

```javascript
import \\{ createStore \\} from 'vuex'
import \\{ vuexLocal, contentSession \\} from './persistedstate'

export const store = createStore(\\{
  state: \\{
    isPC: false, // 是否为PC端
    isList: false, // 是否为列表模式
    groupedArray: [], // 分区的分组数组
    editDetail: \\{\\}, // 分区的编辑回显数据
  \\},
  getters: \\{\\},
  mutations: \\{
    setIsPC(state, payload) \\{
      state.isPC = payload;
    \\},
    setIsList(state, payload) \\{
      state.isList = payload;
    \\},
    setGroupedArray(state, payload) \\{
      state.groupedArray = payload;
    \\},
    setEditDetail(state, payload) \\{
      state.editDetail = payload;
    \\},
    initializeState(state, persistedData) \\{
      if (persistedData) \\{
        Object.keys(persistedData).forEach(key => \\{
          if (state.hasOwnProperty(key)) \\{
            state[key] = persistedData[key];
          \\}
        \\});
      \\}
    \\}
  \\},
  actions: \\{
    initializeStore(\\{ commit \\}) \\{
      // 获取由 vuexLocal 和 contentSession 插件持久化的所有数据
      const localPersistedData = JSON.parse(window.localStorage.getItem('vuex')) || \\{\\};
      const sessionPersistedData = JSON.parse(window.sessionStorage.getItem('content')) || \\{\\};

      // 合并两个来源的数据
      const allPersistedData = \\{ ...localPersistedData, ...sessionPersistedData \\};

      // 提交 mutation 来初始化状态
      commit('initializeState', allPersistedData);
    \\}
  \\},
  modules: \\{\\},
  plugins: [vuexLocal, contentSession],
\\})
```

请注意，上面的 `initializeStore` action 试图获取由 `vuexLocal` 和 `contentSession` 插件所管理的所有持久化数据，并将其合并。这是因为您有两个不同的持久化插件实例，每个实例都可能有自己的 key 和 storage 机制。

此外，考虑到 `vuex-persistedstate` 默认行为是在 store 创建时自动恢复状态，上述 `initializeStore` action 可能是多余的。除非您有特定的需求，例如需要在某些条件下控制初始化逻辑，否则不需要额外实现这样的功能。如果您确实需要这样的初始化逻辑，请确保在应用生命周期的适当时间点调用 `store.dispatch('initializeStore')`，比如在 main.js 中的应用启动时。

#### 解释

1. `createApp(App)`：创建 Vue 应用实例。
2. `app.use(store)`：将 Vuex store 注入到 Vue 应用实例中。
3. `store.dispatch('initializeStore')`：触发 `initializeStore` action，调用 Vuex 中的 `initializeState` mutation 来根据存储的数据初始化状态。

#### `initializeStore` 和 `initializeState` 的作用

- `initializeStore` 是一个 action，它会在应用启动时被触发。它的作用是调用 `initializeState` mutation，来根据本地存储（`localStorage` 或 `sessionStorage`）中的数据来初始化 Vuex 的 state。
- `initializeState` mutation 会检查 `localStorage` 或 `sessionStorage` 中是否有相关的数据。如果有，它会更新 Vuex 的状态；如果没有，则使用默认值。



### Do not access Object.prototype method 'hasOwnProperty' from target object (no-prototype-builtins) at src\store\index.js:17:21 

```
	// 初始化数据
    initializeState(state, persistedData) \\{
      if (persistedData) \\{
        Object.keys(persistedData).forEach((key) => \\{
          if (state.hasOwnProperty(key)) \\{
            state[key] = persistedData[key]
          \\}
        \\})
      \\}
    \\},
```

你遇到的这个错误是由ESLint规则`no-prototype-builtins`触发的。该规则建议不要直接使用`Object.prototype`上的方法，如`hasOwnProperty`，因为这可能会导致意外的行为，特别是在处理可能覆盖这些方法的对象时。

为了解决这个问题，你可以使用`Object.prototype.hasOwnProperty.call`或者更现代的方法是使用`Reflect.has`。以下是两种解决办法：

#### 使用 `Object.prototype.hasOwnProperty.call`

```javascript
if (Object.prototype.hasOwnProperty.call(state, key)) \\{
  state[key] = persistedData[key];
\\}
```

#### 使用 `Reflect.has`

```javascript
if (Reflect.has(state, key)) \\{
  state[key] = persistedData[key];
\\}
```

这两种方法都可以避免直接访问`Object.prototype`的方法，并且不会被对象自身的属性所覆盖。

在你的代码中，可以这样修改：

```javascript
if (persistedData) \\{
  Object.keys(persistedData).forEach((key) => \\{
    if (Object.prototype.hasOwnProperty.call(state, key)) \\{ // 或者使用 Reflect.has(state, key)
      state[key] = persistedData[key];
    \\}
  \\});
\\}
```

请根据你的项目需求选择合适的方法进行修改。如果你的项目需要支持较老的JavaScript环境，那么`Object.prototype.hasOwnProperty.call`可能是更好的选择。如果只关注现代浏览器和环境，`Reflect.has`则更为简洁。



### 其他

在qiankun中，每个子应用实例化不同的store，一个子应用1更新了setIsList，localStorage数据已经改变为isList: false；

首次跳转到另一个子应用2，isList: false正常，子应用2更新setIsList，localStorage数据已经改变为isList: true

返回原来子应用1，state的数据还是之前的false，vuex-persistedstate又把localStorage恢复为false了

怎么解决，请仔细思考， 能否在返回子应用1的时候，重新根据缓存来初始化store 

两个子应用，怎么在重新加载app.vue时，重新从缓存初始化store，避免之前的store干扰

### 解决方法2，未解决

我们需要确保在调用 `restoreStatesFromStorage` 函数时，传入的持久化插件配置对象包含有效的 `storage` 属性。具体来说，应该确保每个持久化插件对象都有一个 `plugin` 属性，并且这个 `plugin` 包含了 `storage` 和 `key` 属性。

#### 修改 `persistedstate.js`

确保每个持久化插件对象都正确地包含了 `plugin` 和 `storage` 属性。我们可以在创建持久化插件时直接将 `storage` 和 `key` 作为属性添加到返回的对象中，而不是仅仅通过 `createPersistedState` 创建的插件。

```javascript
import createPersistedState from 'vuex-persistedstate';

// 定义持久化插件并返回带有名称标识符和存储的对象
function createPersistedPlugin(key, storage, reducer, name) \\{
  const persistedPlugin = createPersistedState(\\{
    key,
    storage,
    reducer,
  \\});

  return \\{
    plugin: persistedPlugin,
    storage, // 直接保存 storage
    key,     // 直接保存 key
    name: name || key // 默认使用 key 作为名称标识符
  \\};
\\}

// 共享状态持久化插件
export const vuexLocal = createPersistedPlugin(
  'vuex',
  window.localStorage,
  (state) => (\\{
    isPC: state.isPC,
    isList: state.isList,
  \\}),
  'vuex'
);

// content-hub 子应用专用持久化插件
export const contentSession = createPersistedPlugin(
  'content',
  window.sessionStorage,
  (state) => (\\{
    groupedArray: state.groupedArray,
    editDetail: state.editDetail,
  \\}),
  'content'
);

// marketing 子应用专用持久化插件
export const marketingSession = createPersistedPlugin(
  'marketing',
  window.sessionStorage,
  (state) => (\\{
    curProduct: state.curProduct,
    curCustomer: state.curCustomer,
  \\}),
  'marketing'
);

// 创建一个通用的恢复状态方法
export function restoreStatesFromStorage(store, persistedPlugins) \\{
  persistedPlugins.forEach((\\{ storage, key \\}) => \\{
    if (!storage || !storage.getItem) \\{
      console.error(`Invalid storage for key $\\{key\\}`);
      return;
    \\}

    const savedState = JSON.parse(storage.getItem(key)) || \\{\\};
    
    // 更新 store 状态
    Object.keys(savedState).forEach((key) => \\{
      if (store.state[key] !== undefined) \\{
        // 假设 mutations 遵循 set<Key> 的命名规则
        store.commit(`set$\\{key.charAt(0).toUpperCase() + key.slice(1)\\}`, savedState[key]);
      \\}
    \\});

    console.log(`Restored state for $\\{key\\} from $\\{storage === window.localStorage ? 'localStorage' : 'sessionStorage'\\}`);
  \\});
\\}
```

### 修改 `index.js`

确保在创建 store 后立即调用 `restoreStatesFromStorage` 函数来主动恢复状态。为此，我们需要导入所有相关的持久化插件，并将它们传递给恢复函数。

```javascript
import \\{ createStore \\} from 'vuex';
import \\{ vuexLocal, contentSession, restoreStatesFromStorage \\} from './persistedstate';

const store = createStore(\\{
  state: \\{
    isPC: false, // 是否为PC端
    isList: false, // 是否为列表模式
    groupedArray: [], // 分区的分组数组
    editDetail: \\{\\}, // 分区的编辑回显数据
  \\},
  getters: \\{\\},
  mutations: \\{
    setIsPC(state, payload) \\{
      state.isPC = payload;
    \\},
    setIsList(state, payload) \\{
      state.isList = payload;
    \\},
    setGroupedArray(state, payload) \\{
      state.groupedArray = payload;
    \\},
    setEditDetail(state, payload) \\{
      state.editDetail = payload;
    \\},
  \\},
  actions: \\{\\},
  modules: \\{\\},
  plugins: [vuexLocal.plugin, contentSession.plugin], // 注意这里只传入插件部分
\\});

// 主动恢复缓存数据
restoreStatesFromStorage(store, [vuexLocal, contentSession]);

export default store;
```

### 关键点解释

- **持久化插件对象**：现在每个持久化插件对象不仅包含 `plugin`，还直接包含了 `storage` 和 `key` 属性。这确保了在恢复状态时可以直接访问这些属性。
  
- **错误处理**：在 `restoreStatesFromStorage` 函数中添加了对无效 `storage` 的检查，以防止尝试从 `undefined` 调用 `getItem` 方法导致的错误。

通过这种方式，我们可以确保即使每个子应用拥有自己的 store 实例，它们也能主动从持久化存储中恢复最新的状态，从而保持一致性和同步性。此外，这种方法更具扩展性，未来如果有更多的持久化需求，只需添加新的持久化插件配置即可。