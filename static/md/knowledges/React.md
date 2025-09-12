---
title: React
date: 2019-11-15 17:11:07
categories: 
- 前端知识
tags:
- React
- redux
- 组件
---
### React 是什么？

React 不是 MV* 框架，用于构建用户界面的 JavaScript 库，侧重于 View 层

React 主要的原理：

- 虚拟 DOM + diff 算法 -> 不直接操作 DOM 对象
- Components 组件 -> Virtual DOM 的节点
- State 触发视图的渲染 -> 单向数据绑定
- React 解决方案：React + Redux + react-router + Fetch + webpack



### React 组件生命周期

组件的生命周期可分成三个状态：

- Mounting(挂载)：已插入真实 DOM
- Updating(更新)：正在被重新渲染
- Unmounting(卸载)：已移出真实 DOM

#### 挂载

当组件实例被创建并插入 DOM 中时，其生命周期调用顺序如下：

- `constructor()`: 在 React 组件挂载之前，会调用它的构造函数。
- `getDerivedStateFromProps()`: 在调用 render 方法之前调用，并且在初始挂载及后续更新时都会被调用。
- `render()`: render() 方法是 class 组件中唯一必须实现的方法。
- `componentDidMount()`: 在组件挂载后（插入 DOM 树中）立即调用。

render() 方法是 class 组件中唯一必须实现的方法，其他方法可以根据自己的需要来实现。

#### 更新

每当组件的 state 或 props 发生变化时，组件就会更新。

当组件的 props 或 state 发生变化时会触发更新。组件更新的生命周期调用顺序如下：

- `getDerivedStateFromProps()`: 在调用 render 方法之前调用，并且在初始挂载及后续更新时都会被调用。根据 shouldComponentUpdate() 的返回值，判断 React 组件的输出是否受当前 state 或 props 更改的影响。
- `shouldComponentUpdate()`:当 props 或 state 发生变化时，shouldComponentUpdate() 会在渲染执行之前被调用。
- `render()`: render() 方法是 class 组件中唯一必须实现的方法。
- `getSnapshotBeforeUpdate()`: 在最近一次渲染输出（提交到 DOM 节点）之前调用。
- `componentDidUpdate()`: 在更新后会被立即调用。

render() 方法是 class 组件中唯一必须实现的方法，其他方法可以根据自己的需要来实现。

#### 卸载

当组件从 DOM 中移除时会调用如下方法：

- `componentWillUnmount()`: 在组件卸载及销毁之前直接调用。



### 为啥要用Hook

#### 1.Hook是React16.8的新增特性，它可以让我们在不编写class的情况下使用state以及其他的React特性（比如生命周期）。

#### 2.class相比函数式组件的优势：

class组件内部可以定义自己的state，用来保存组件自己内部的状态；函数式组件不可以，因为函数每次调用都会产生新的临时变量。
class组件有自己的生命周期，可以在对应的生命周期中完成自己的逻辑；比如在componentDidMount中发送网络请求，并且该生命周期函数只会执行一次；函数式组件在学习hooks之前，如果在函数中发送网络请求，意味着每次重新渲染都会重新发送一次网络请求。
class组件可以在状态改变时只重新执行render函数以及我们希望重新调用的生命周期函数componentDidUpdate等；函数式组件在重新渲染时，整个函数都会被执行，似乎没有什么地方可以只让它们调用一次；
在Hook之前，以上情况通常都用class。

#### 3.Class组件存在的问题：

复杂组件变得难以理解： 最初编写class组件时，往往逻辑比较简单，但是业务增多，class组件就会越来越复杂；
比如componentDidMount中，可能就会有大量逻辑代码，包括网络请求，一些事件的监听（还需要在componentWillUnmount中移除）；
而对于这样的class实际上很难拆分，因为这些逻辑往往混在一起，强行拆分反而会造成过度设计，增加代码的复杂度。
难以理解的class： ES6中class相当于React的一个障碍；
在class中，我们必须搞清楚this的指向到底是谁，所以需要花很多的精力去学习this； 虽然掌握this是必要，但是处理起来依然很麻烦
组件复用状态很难： 在之前为了一些状态的复用，我们需要通过高阶组件或render props；
像redux中connect或者react-route中的withRouter，这些高阶组件设计的目的就是为了状态的复用。
或者类似于Provider，Consumer来共享一些状态，但是多次使用Consumer时，就会有很多嵌套；



### Hook优点

可以让我们在不编写class的情况下使用state以及其他的React特性；也可以延伸很多用法解决上述问题。

Hook使用场景： Hook的出现基本可以替代class组件（除了个别场景）；
若项目比较旧，并不需要直接将所有代码重构为Hooks，因为它完全向下兼容，可以渐进式地来使用；
Hook只能在函数组件中使用，不能在类组件，或者函数组件之外的地方使用；



### React 中setState更新state何时同步何时异步？

React中constructor是唯一可以初始化state的地方，也可以把它理解成一个钩子函数，该函数最先执行且只执行一次。

更新状态不要直接修改this.state。虽然状态可以改变，但不会触发组件的更新。

应当使用this.setState()，该方法接收两种参数：对象或函数。

1. 对象：即想要修改的state
2. 函数：接收两个函数，第一个函数接受两个参数，第一个是当前state，第二个是当前props，该函数返回一个对象，和直接传递对象参数是一样的，就是要修改的state；第二个函数参数是state改变后触发的回调。

回到主题，setState可能是异步的。对此官方有这样一段描述：setState() does not always immediately update the component. It may batch or defer the update until later. This makes reading this.state right after calling setState()a potential pitfall.

关键词：batch、defer、may。

#### 要探究setState为什么可能是异步的，先了解setState执行后会发生什么？

事实上setState内部执行过程是很复杂的，大致过程包括更新state，创建新的VNode，再经过diff算法比对差异，决定渲染哪一部分以及怎么渲染，最终形成最新的UI。这一过程包含组件的四个生命周期函数。

- shouleComponentUpdate
- componentWillUpdate
- render
- componentDidUpdate

需要注意的是如果子组件的数据依赖于父组件，还会执行一个钩子函数`componentWillReceiveProps`。

假如setState是同步更新的，每更新一次，这个过程都要完整执行一次，无疑会造成性能问题。事实上这些生命周期为纯函数，对性能还好，但是diff比较、更新DOM总消耗时间和性能吧。

此外为了批次和效能，多个setState有可能在执行过程中还会被合并，所以setState延时异步更新是很合理的。

#### setState何时同步何时异步？

**由React控制的事件处理程序，以及生命周期函数调用setState不会同步更新state** 。

**React控制之外的事件中调用setState是同步更新的。比如原生js绑定的事件，setTimeout/setInterval等**。

大部分开发中用到的都是React封装的事件，比如onChange、onClick、onTouchMove等，这些事件处理程序中的setState都是异步处理的。

看以下case：

```js
constructor() \\{
  this.state = \\{
    count: 10
  \\}

  this.handleClickOne = this.handleClickOne.bind(this)
  this.handleClickTwo = this.handleClickTwo.bind(this)
\\}

render() \\{
  return (
    <button onClick=\\{this.hanldeClickOne\\}>clickOne</button>
    <button onClick=\\{this.hanldeClickTwo\\}>clickTwo</button>
    <button id="btn">clickTwo</button>
  )
\\}

handleClickOne() \\{
  this.setState(\\{ count: this.state.count + 1\\})
  console.log(this.state.count)
\\}
```

输出：10

由此可以看出该事件处理程序中的setState是异步更新state的。

```js
componentDidMount() \\{
  document.getElementById('btn').addEventListener('clcik', () => \\{
    this.setState(\\{ count: this.state.count + 1\\})
    console.log(this.state.count)
  \\})
\\}
```

输出： 11

```js
handleClickTwo() \\{
  setTimeout(() => \\{
    this.setState(\\{ count: this.state.count + 1\\})
    console.log(this.state.count)
  \\}, 10)  
\\}
```

输出： 11

以上两种方式绕过React，通过js的事件绑定程序 addEventListener 和使用setTimeout/setInterval 等 React 无法掌控的 APIs情况下，setState是同步更新state。

#### React是怎样控制异步和同步的呢？

在 React 的 setState 函数实现中，会根据一个变量 isBatchingUpdates 判断是直接更新 this.state 还是放到队列中延时更新，而 isBatchingUpdates 默认是 false，表示 setState 会同步更新 this.state；但是，有一个函数 batchedUpdates，该函数会把 isBatchingUpdates 修改为 true，而当 React 在调用事件处理函数之前就会先调用这个 batchedUpdates将isBatchingUpdates修改为true，这样由 React 控制的事件处理过程 setState 不会同步更新 this.state。

![img](https://upload-images.jianshu.io/upload_images/5256541-992ce78e70151b57.jpg?imageMogr2/auto-orient/strip|imageView2/2/w/720/format/webp)

#### 多个setState调用会合并处理

```js
render() \\{
  console.log('render')
\\}
hanldeClick() \\{
  this.setState(\\{ name: 'jack' \\})
  this.setState(\\{ age: 12 \\})
\\}
```

在hanldeClick处理程序中调用了两次setState，但是render只执行了一次。因为React会将多个this.setState产生的修改放在一个队列里进行批延时处理。

#### 参数为函数的setState用法

先看以下case：

```js
handleClick() \\{
  this.setState(\\{
    count: this.state.count + 1
  \\})
\\}
```

以上操作存在潜在的陷阱，不应该依靠它们的值来计算下一个状态。

```js
handleClick() \\{
  this.setState(\\{
    count: this.state.count + 1
  \\})
  this.setState(\\{
    count: this.state.count + 1
  \\})
  this.setState(\\{
    count: this.state.count + 1
  \\})
\\}
```

最终的结果只加了1

因为调用this.setState时，并没有立即更改this.state，所以this.setState只是在反复设置同一个值而已，上面的代码等同于这样

```js
handleClick() \\{
  const count = this.state.count

  this.setState(\\{
    count: count + 1
  \\})
  this.setState(\\{
    count: count + 1
  \\})
  this.setState(\\{
    count: count + 1
  \\})
\\}
```

count相当于一个快照，所以不管重复多少次，结果都是加1。

此外假如setState更新state后我希望做一些事情，而setState可能是异步的，那我怎么知道它什么时候执行完成。所以setState提供了函数式用法，接收两个函数参数，第一个函数调用更新state，第二个函数是更新完之后的回调。

第一个函数接收先前的状态作为第一个参数，将此次更新被应用时的props做为第二个参数。

```js
increment(state, props) \\{
  return \\{
    count: state.count + 1
  \\}
\\}

handleClick() \\{
  this.setState(this.increment)
  this.setState(this.increment)
  this.setState(this.increment)
\\}
```

结果: 13

对于多次调用函数式setState的情况，React会保证调用每次increment时，state都已经合并了之前的状态修改结果。

也就是说，第一次调用this.setState(increment)，传给increment的state参数的count是10，第二调用是11，第三次调用是12，最终handleClick执行完成后的结果就是this.state.count变成了13。

值得注意的是：在increment函数被调用时，this.state并没有被改变，依然要等到render函数被重新执行时（或者shouldComponentUpdate函数返回false之后）才被改变，因为render只执行一次。

让setState接受一个函数的API的设计是相当棒的！不仅符合函数式编程的思想，让开发者写出没有副作用的函数，而且我们并不去修改组件状态，只是把要改变的状态和结果返回给React，维护状态的活完全交给React去做。正是把流程的控制权交给了React，所以React才能协调多个setState调用的关系。

#### 在同一个事件处理程序中不要混用

case:

```js
increment(state, props) \\{
  return \\{
    count: state.count + 1
  \\}
\\}

handleClick() \\{
  this.setState(this.increment)
  this.setState(\\{ count: this.state.count + 1 \\})
  this.setState(this.increment)
\\}
```

结果： 12

第一次执行setState，count为11，第二次执行，this.state仍然是没有更新的状态，所以this.state.count又打回了原形为10，加1以后变成11，最后再执行setState，所以最终count的结果是12。（render依然只执行一次）

setState的第二个回调参数会在更新state，重新触发render后执行。



### react-router 路由系统的实现原理？

- 实现原理：location 与 components 之间的同步

* 路由的职责是保证 UI 和 URL 的同步
* 在 react-router 中，URL 对应 Location 对象，UI 由 react components 决定
* 因此，路由在 react-router 中就转变成 location 与 components 之间的同步



### React 中 keys 的作用是什么？

> Keys 是 React 用于追踪哪些列表中元素被修改、被添加或者被移除的辅助标识

- 在开发过程中，我们需要保证某个元素的 key 在其同级元素中具有唯一性。在 React Diff 算法中 React 会借助元素的 Key 值来判断该元素是新近创建的还是被移动而来的元素，从而减少不必要的元素重渲染。此外，React 还需要借助 Key 值来判断元素与本地状态的关联关系，因此我们绝不可忽视转换函数中 Key 的重要性



### 传入 setState 函数的第二个参数的作用是什么？

> 该函数会在setState函数调用完成并且组件开始重渲染的时候被调用，我们可以用该函数来监听渲染是否完成：

```
this.setState(
  \\{ username: 'tylermcginnis33' \\},
  () => console.log('setState has finished and the component has re-rendered.')
)
```

```
this.setState((prevState, props) => \\{
  return \\{
    streak: prevState.streak + props.count
  \\}
\\})
```



### React 中 refs 的作用是什么

- Refs 是 React 提供给我们的安全访问 DOM 元素或者某个组件实例的句柄
- 可以为元素添加ref属性然后在回调函数中接受该元素在 DOM 树中的句柄，该值会作为回调函数的第一个参数返回



### 在生命周期中的哪一步你应该发起 AJAX 请求

> 我们应当将AJAX 请求放到 `componentDidMount` 函数中执行，主要原因有下

- React 下一代调和算法 Fiber 会通过开始或停止渲染的方式优化应用性能，其会影响到 componentWillMount 的触发次数。对于 componentWillMount 这个生命周期函数的调用次数会变得不确定，React 可能会多次频繁调用 componentWillMount。如果我们将 AJAX 请求放到 componentWillMount 函数中，那么显而易见其会被触发多次，自然也就不是好的选择。
- 如果我们将 AJAX 请求放置在生命周期的其他函数中，我们并不能保证请求仅在组件挂载完毕后才会要求响应。如果我们的数据请求在组件挂载之前就完成，并且调用了setState函数将数据添加到组件状态中，对于未挂载的组件则会报错。而在 componentDidMount 函数中进行 AJAX 请求则能有效避免这个问题



### shouldComponentUpdate 的作用

> shouldComponentUpdate 允许我们手动地判断是否要进行组件更新，根据组件的应用场景设置函数的合理返回值能够帮我们避免不必要的更新



### 如何告诉 React 它应该编译生产环境版

> 通常情况下我们会使用 Webpack 的 DefinePlugin 方法来将 NODE_ENV 变量值设置为 production。编译版本中 React 会忽略 propType 验证以及其他的告警信息，同时还会降低代码库的大小，React 使用了 Uglify 插件来移除生产环境下不必要的注释等信息



### 概述下 React 中的事件处理逻辑

> 为了解决跨浏览器兼容性问题，React 会将浏览器原生事件（Browser Native Event）封装为合成事件（SyntheticEvent）传入设置的事件处理器中。这里的合成事件提供了与原生事件相同的接口，不过它们屏蔽了底层浏览器的细节差异，保证了行为的一致性。另外有意思的是，React 并没有直接将事件附着到子元素上，而是以单一事件监听器的方式将所有的事件发送到顶层进行处理。这样 React 在更新 DOM 的时候就不需要考虑如何去处理附着在 DOM 上的事件监听器，最终达到优化性能的目的



### createElement 与 cloneElement 的区别是什么

> createElement 函数是 JSX 编译之后使用的创建 React Element 的函数，而 cloneElement 则是用于复制某个元素并传入新的 Props



### redux中间件

> 中间件提供第三方插件的模式，自定义拦截 action -> reducer 的过程。变为 action -> middlewares -> reducer 。这种机制可以让我们改变数据流，实现如异步 action ，action 过滤，日志输出，异常报告等功能

- `redux-logger`：提供日志输出
- `redux-thunk`：处理异步操作
- `redux-promise`：处理异步操作，`actionCreator`的返回值是`promise`



### redux有什么缺点

- 一个组件所需要的数据，必须由父组件传过来，而不能像flux中直接从store取。
- 当一个组件相关数据更新时，即使父组件不需要用到这个组件，父组件还是会重新render，可能会有效率影响，或者需要写复杂的`shouldComponentUpdate`进行判断。



### react组件的划分业务组件技术组件？

- 根据组件的职责通常把组件分为UI组件和容器组件。
- UI 组件负责 UI 的呈现，容器组件负责管理数据和逻辑。
- 两者通过`React-Redux` 提供`connect`方法联系起来



### react生命周期函数

**初始化阶段**

- `getDefaultProp`s:获取实例的默认属性
- `getInitialState`:获取每个实例的初始化状态
- `componentWillMount`：组件即将被装载、渲染到页面上
- `render`:组件在这里生成虚拟的DOM节点
- `omponentDidMount`:组件真正在被装载之后

**运行中状态**

- `componentWillReceiveProps`:组件将要接收到属性的时候调用
- `shouldComponentUpdate`:组件接受到新属性或者新状态的时候（可以返回false，接收数据后不更新，阻止`render`调用，后面的函数不会被继续执行了）
- `componentWillUpdate`:组件即将更新不能修改属性和状态
- `render`:组件重新描绘
- `componentDidUpdate`:组件已经更新

**销毁阶段**

- `componentWillUnmount`:组件即将销毁



### react性能优化是哪个周期函数

> shouldComponentUpdate 这个方法用来判断是否需要调用render方法重新描绘dom。因为dom的描绘非常消耗性能，如果我们能在shouldComponentUpdate方法中能够写出更优化的dom diff算法，可以极大的提高性能



### 为什么虚拟dom会提高性能

> 虚拟dom相当于在js和真实dom中间加了一个缓存，利用dom diff算法避免了没有必要的dom操作，从而提高性能

**具体实现步骤如下**

- 用 JavaScript 对象结构表示 DOM 树的结构；然后用这个树构建一个真正的 DOM 树，插到文档当中
- 当状态变更的时候，重新构造一棵新的对象树。然后用新的树和旧的树进行比较，记录两棵树差异
- 把2所记录的差异应用到步骤1所构建的真正的DOM树上，视图就更新



### diff算法?

- 把树形结构按照层级分解，只比较同级元素。
- 给列表结构的每个单元添加唯一的key属性，方便比较。
- React 只会匹配相同 class 的 component（这里面的class指的是组件的名字）
- 合并操作，调用 component 的 setState 方法的时候, React 将其标记为 - dirty.到每一个事件循环结束, React 检查所有标记 dirty 的 component 重新绘制.
- 选择性子树渲染。开发人员可以重写shouldComponentUpdate提高diff的性能



### react性能优化方案

- 重写`shouldComponentUpdate`来避免不必要的dom操作
- 使用 production 版本的react.js
- 使用key来帮助React识别列表中所有子组件的最小变化



### 当你调用 setState 的时候，发生了什么事？

将传递给 setState 的对象合并到组件的当前状态，这将启动一个和解的过程，构建一个新的 react 元素树，与上一个元素树进行对比（ diff ），从而进行最小化的重渲染。



### React 项目用过什么脚手架（本题是开放性题目）

creat-react-app Yeoman 等



### 什么时候在功能组件( Class Component )上使用类组件( Functional Component )？

如果您的组件具有状态( state ) 或 生命周期方法，请使用 Class 组件。否则，使用功能组件



### React 中 keys 的作用是什么？

Keys 是 React 用于追踪哪些列表中元素被修改、被添加或者被移除的辅助标识。

```js
render () \\{
  return (
    <ul>
      \\{this.state.todoItems.map((\\{item, key\\}) => \\{
        return <li key=\\{key\\}>\\{item\\}</li>
      \\})\\}
    </ul>
  )
\\}
```

在开发过程中，我们需要保证某个元素的 key 在其同级元素中具有唯一性。在 React Diff 算法中 React 会借助元素的 Key 值来判断该元素是新近创建的还是被移动而来的元素，从而减少不必要的元素重渲染。此外，React 还需要借助 Key 值来判断元素与本地状态的关联关系，因此我们绝不可忽视转换函数中 Key 的重要性。



### React 优势

1、React 速度很快：它并不直接对 DOM 进行操作，引入了一个叫做虚拟 DOM 的概念，安插在 javascript 逻辑和实际的 DOM 之间，性能好。

2、跨浏览器兼容：虚拟 DOM 帮助我们解决了跨浏览器问题，它为我们提供了标准化的 API，甚至在 IE8 中都是没问题的。

3、一切都是 component：代码更加模块化，重用代码更容易，可维护性高。

4、单向数据流：Flux 是一个用于在 JavaScript 应用中创建单向数据层的架构，它随着 React 视图库的开发而被 Facebook 概念化。

5、同构、纯粹的 javascript：因为搜索引擎的爬虫程序依赖的是服务端响应而不是 JavaScript 的执行，预渲染你的应用有助于搜索引擎优化。

6、兼容性好：比如使用 RequireJS 来加载和打包，而 Browserify 和 Webpack 适用于构建大型应用。它们使得那些艰难的任务不再让人望而生畏。



### react diff 原理（常考，大厂必考）

把树形结构按照层级分解，只比较同级元素。

给列表结构的每个单元添加唯一的 key 属性，方便比较。

React 只会匹配相同 class 的 component（这里面的 class 指的是组件的名字）
合并操作，调用 component 的 setState 方法的时候, React 将其标记为 dirty.到每一个事件循环结束, React 检查所有标记 dirty 的 component 重新绘制.

选择性子树渲染。开发人员可以重写 shouldComponentUpdate 提高 diff 的性能。



### react 生命周期函数

- 初始化阶段：
  - getDefaultProps:获取实例的默认属性
  - getInitialState:获取每个实例的初始化状态
  - componentWillMount：组件即将被装载、渲染到页面上
  - render:组件在这里生成虚拟的 DOM 节点
  - componentDidMount:组件真正在被装载之后
- 运行中状态：
  - componentWillReceiveProps:组件将要接收到属性的时候调用
  - shouldComponentUpdate:组件接受到新属性或者新状态的时候（可以返回 false，接收数据后不更新，阻止 render 调用，后面的函数不会被继续执行了）
  - componentWillUpdate:组件即将更新不能修改属性和状态
  - render:组件重新描绘
  - componentDidUpdate:组件已经更新
- 销毁阶段：
  - componentWillUnmount:组件即将销毁

解析：有三大阶段，每阶段的细分 5-5-1



### shouldComponentUpdate 是做什么的？（react 性能优化是哪个周期函数？）

shouldComponentUpdate 这个方法用来判断是否需要调用 render 方法重新描绘 dom。因为 dom 的描绘非常消耗性能，如果我们能在 shouldComponentUpdate 方法中能够写出更优化的 dom diff 算法，可以极大的提高性能。



### 为什么虚拟 dom 会提高性能?(必考)

虚拟 dom 相当于在 js 和真实 dom 中间加了一个缓存，利用 dom diff 算法避免了没有必要的 dom 操作，从而提高性能。

用 JavaScript 对象结构表示 DOM 树的结构；然后用这个树构建一个真正的 DOM 树，插到文档当中当状态变更的时候，重新构造一棵新的对象树。然后用新的树和旧的树进行比较，记录两棵树差异把 2 所记录的差异应用到步骤 1 所构建的真正的 DOM 树上，视图就更新了。



### React 中 refs 的作用是什么？

Refs 是 React 提供给我们的安全访问 DOM 元素或者某个组件实例的句柄。我们可以为元素添加 ref 属性然后在回调函数中接受该元素在 DOM 树中的句柄，该值会作为回调函数的第一个参数返回：

```js
class CustomForm extends Component \\{
  handleSubmit = () => \\{
    console.log("Input Value: ", this.input.value);
  \\};
  render() \\{
    return (
      <form onSubmit=\\{this.handleSubmit\\}>
        <input type="text" ref=\\{input => (this.input = input)\\} />
        <button type="submit">Submit</button>
      </form>
    );
  \\}
\\}
```

上述代码中的 input 域包含了一个 ref 属性，该属性声明的回调函数会接收 input 对应的 DOM 元素，我们将其绑定到 this 指针以便在其他的类函数中使用。另外值得一提的是，refs 并不是类组件的专属，函数式组件同样能够利用闭包暂存其值：

```js
function CustomForm(\\{ handleSubmit \\}) \\{
  let inputElement;
  return (
    <form onSubmit=\\{() => handleSubmit(inputElement.value)\\}>
      <input type="text" ref=\\{input => (inputElement = input)\\} />
      <button type="submit">Submit</button>
    </form>
  );
\\}
```



### redux 有什么缺点

- 一个组件所需要的数据，必须由父组件传过来，而不能像 flux 中直接从 store 取。
- 当一个组件相关数据更新时，即使父组件不需要用到这个组件，父组件还是会重新 render，可能会有效率影响，或者需要写复杂的 shouldComponentUpdate 进行判断。



### 简述 flux 思想

Flux 的最大特点，就是数据的"单向流动"。

1. 用户访问 View
2. View 发出用户的 Action
3. Dispatcher 收到 Action，要求 Store 进行相应的更新
4. Store 更新后，发出一个"change"事件
5. View 收到"change"事件后，更新页面



### 了解 redux 么，说一下 redux 吧

- redux 是一个应用数据流框架，主要是解决了组件间状态共享的问题，原理是集中式管理，主要有三个核心方法，action，store，reducer，工作流程是 view 调用 store 的 dispatch 接收 action 传入 store，reducer 进行 state 操作，view 通过 store 提供的 getState 获取最新的数据，flux 也是用来进行数据操作的，有四个组成部分 action，dispatch，view，store，工作流程是 view 发出一个 action，派发器接收 action，让 store 进行数据更新，更新完成以后 store 发出 change，view 接受 change 更新视图。Redux 和 Flux 很像。主要区别在于 Flux 有多个可以改变应用状态的 store，在 Flux 中 dispatcher 被用来传递数据到注册的回调事件，但是在 redux 中只能定义一个可更新状态的 store，redux 把 store 和 Dispatcher 合并,结构更加简单清晰
- 新增 state,对状态的管理更加明确，通过 redux，流程更加规范了，减少手动编码量，提高了编码效率，同时缺点时当数据更新时有时候组件不需要，但是也要重新绘制，有些影响效率。一般情况下，我们在构建多交互，多数据流的复杂项目应用时才会使用它们



### React 中有三种构建组件的方式

React.createClass()、ES6 class 和无状态函数。



### react 组件的划分业务组件技术组件？

- 根据组件的职责通常把组件分为 UI 组件和容器组件。
- UI 组件负责 UI 的呈现，容器组件负责管理数据和逻辑。
- 两者通过 React-Redux 提供 connect 方法联系起来。



### 描述事件在 React 中的处理方式

为了解决跨浏览器兼容性问题，您的 React 中的事件处理程序将传递 SyntheticEvent 的实例，它是 React 的浏览器本机事件的跨浏览器包装器。

这些 SyntheticEvent 与您习惯的原生事件具有相同的接口，除了它们在所有浏览器中都兼容。有趣的是，React 实际上并没有将事件附加到子节点本身。React 将使用单个事件监听器监听顶层的所有事件。这对于性能是有好处的，这也意味着在更新 DOM 时，React 不需要担心跟踪事件监听器。



### 应该在 React 组件的何处发起 Ajax 请求

在 React 组件中，应该在 componentDidMount 中发起网络请求。这个方法会在组件第一次“挂载”(被添加到 DOM)时执行，在组件的生命周期中仅会执行一次。更重要的是，你不能保证在组件挂载之前 Ajax 请求已经完成，如果是这样，也就意味着你将尝试在一个未挂载的组件上调用 setState，这将不起作用。在 componentDidMount 中发起网络请求将保证这有一个组件可以更新了。



### (在构造函数中)调用 super(props) 的目的是什么

在 super() 被调用之前，子类是不能使用 this 的，在 ES2015 中，子类必须在 constructor 中调用 super()。传递 props 给 super() 的原因则是便于(在子类中)能在 constructor 访问 this.props。



### 除了在构造函数中绑定 this，还有其它方式吗

你可以使用属性初始值设定项(property initializers)来正确绑定回调，create-react-app 也是默认支持的。在回调中你可以使用箭头函数，但问题是每次组件渲染时都会创建一个新的回调。



### 为什么建议传递给 setState 的参数是一个 callback 而不是一个对象

因为 this.props 和 this.state 的更新可能是异步的，不能依赖它们的值去计算下一个 state。



### 何为高阶组件(higher order component)

高阶组件是一个以组件为参数并返回一个新组件的函数。HOC 运行你重用代码、逻辑和引导抽象。最常见的可能是 Redux 的 connect 函数。除了简单分享工具库和简单的组合，HOC 最好的方式是共享 React 组件之间的行为。如果你发现你在不同的地方写了大量代码来做同一件事时，就应该考虑将代码重构为可重用的 HOC。



### 何为受控组件(controlled component)

在 HTML 中，类似 `<input>`, `<textarea>` 和 `<select>` 这样的表单元素会维护自身的状态，并基于用户的输入来更新。当用户提交表单时，前面提到的元素的值将随表单一起被发送。但在 React 中会有些不同，包含表单元素的组件将会在 state 中追踪输入的值，并且每次调用回调函数时，如 onChange 会更新 state，重新渲染组件。一个输入表单元素，它的值通过 React 的这种方式来控制，这样的元素就被称为"受控元素"。



### 在 React 当中 Element 和 Component 有何区别？

React Element 是描述屏幕上所见内容的数据结构，是对于 UI 的对象表述。典型的 React Element 就是利用 JSX 构建的声明式代码片然后被转化为 createElement 的调用组合。

React Component 是一个函数或一个类，可以接收参数输入，并且返回某个 React Element



### (组件的)状态(state)和属性(props)之间有何区别

- State 是一种数据结构，用于组件挂载时所需数据的默认值。State 可能会随着时间的推移而发生突变，但多数时候是作为用户事件行为的结果。
- Props(properties 的简写)则是组件的配置。props 由父组件传递给子组件，并且就子组件而言，props 是不可变的(immutable)。组件不能改变自身的 props，但是可以把其子组件的 props 放在一起(统一管理)。Props 也不仅仅是数据--回调函数也可以通过 props 传递。



### 展示组件(Presentational component)和容器组件(Container component)之间有何区别？

- 展示组件关心组件看起来是什么。展示专门通过 props 接受数据和回调，并且几乎不会有自身的状态，但当展示组件拥有自身的状态时，通常也只关心 UI 状态而不是数据的状态。
- 容器组件则更关心组件是如何运作的。容器组件会为展示组件或者其它容器组件提供数据和行为(behavior)，它们会调用 Flux actions，并将其作为回调提供给展示组件。容器组件经常是有状态的，因为它们是(其它组件的)数据源。



### 类组件(Class component)和 函数式组件(Functional component)之间有何区别？

1. 函数式组件比类组件操作简单，只是简单的调取和返回 JSX；而类组件可以使用生命周期函数来操作业务

2. 函数式组件可以理解为静态组件（组件中的内容调取的时候已经固定了，很难再修改），而类组件，可以基于组件内部的状态来动态更新渲染的内容

- 类组件不仅允许你使用更多额外的功能，如组件自身的状态和生命周期钩子，也能使组件直接访问 store 并维持状态
- 当组件仅是接收 props，并将组件自身渲染到页面时，该组件就是一个 '无状态组件(stateless component)'，可以使用一个纯函数来创建这样的组件。这种组件也被称为哑组件(dumb components)或展示组件



### createElement 和 cloneElement 有什么区别？

传入的第一个参数不同

React.createElement():JSX 语法就是用 React.createElement()来构建 React 元素的。它接受三个参数，第一个参数可以是一个标签名。如 div、span，或者 React 组件。第二个参数为传入的属性。第三个以及之后的参数，皆作为组件的子组件。

```js
React.createElement(type, [props], [...children]);
```

React.cloneElement()与 React.createElement()相似，不同的是它传入的第一个参数是一个 React 元素，而不是标签名或组件。新添加的属性会并入原有的属性，传入到返回的新元素中，而旧的子元素将被替换。将保留原始元素的键和引用。

```js
React.cloneElement(element, [props], [...children]);
```



### setState 和 replaceState 的区别

setState 是修改其中的部分状态，相当于 Object.assign，只是覆盖，不会减少原来的状态

replaceState 是完全替换原来的状态，相当于赋值，将原来的 state 替换为另一个对象，如果新状态属性减少，那么 state 中就没有这个状态了



### 创建项目

使用命令行窗口打开一个想要存放项目的文件夹

```
npx create-react-app my-app
cd my-app
npm start
```

当你准备好部署到生产环境时，执行 

```
npm run build
```

会在 `build` 文件夹内生成你应用的优化版本



### React 父子组件通信

通讯是单向的，数据必须是由一方传到另一方。

#### 1.父组件与子组件间的通信。

在 React 中，**父组件可以向子组件通过传 props 的方式，向子组件进行通讯。**

 **父组件 App.js**

```jsx
import React, \\{ Component \\} from 'react';
import './App.css';
import Child from './child'

class App extends Component \\{
    constructor(props)\\{
        super(props);
        this.state=\\{
            msg:'父类的消息',
            name:'秦始皇',
            age:40
        \\}
    \\}

    callback=(msg,name,age)=>\\{
        // setState方法,分别修改msg、name、age的值,值是由child里面传过来的
        this.setState(\\{msg\\});
        this.setState(\\{name\\});
        this.setState(\\{age\\});
    \\}

	render() \\{
		return (
			<div className="father">
				<p> Message: &nbsp;&nbsp;\\{this.state.msg\\}</p>
				<Child callback=\\{this.callback\\} age=\\{this.state.age\\} name=\\{this.state.name\\}></Child>
			</div>
		);
	\\}
\\}

export default App;
```

父组件中，**state**里面有三个属性，分别是**msg**，**name**和**age**，在子组件child中，如果想拿到父组件里面的属性，就需要通过props传递。

在 <Child></Child> 标签里面添加

```kotlin
age=\\{this.state.age\\} name=\\{this.state.name\\}  
写成 
<Child age=\\{this.state.age\\} name=\\{this.state.name\\}></Child>
```

**name**和**age**分别是你要传递的属性。

**子组件  Child**

```jsx
import React from "react";

class Child extends React.Component\\{
    constructor(props)\\{
        super(props);
        this.state=\\{
            name:'Andy',
            age:31,
            msg:"来自子类的消息"
        \\}
    \\}

    change=()=>\\{
        this.props.callback(this.state.msg,this.state.name,this.state.age);
    \\}

    render()\\{
        return(
            <div>
                <div>\\{this.props.name\\}</div>
                <div>\\{this.props.age\\}</div>
                <button onClick=\\{this.change\\}>点击</button>
            </div>
        )
    \\}
\\}

export default Child;
```

在子组件中,通过 **\\{this.props.name\\}**  **\\{this.props.age\\}**就能拿到父组件里面的数据。

![img](https:////upload-images.jianshu.io/upload_images/6177839-882baa5378ab8f4b.jpg?imageMogr2/auto-orient/strip|imageView2/2/w/246/format/webp)

呈现在页面上的就是这个样子。

**其中 John,99均来自于父组件App.js**



#### 2.子组件向父组件通信

子组件向父组件通讯，同样也需要**父组件向子组件传递 props 进行通讯**

只是父组件传递的，是作用域为父组件自身的函数；**子组件调用该函数，将子组件想要传递的信息，作为参数，传递到父组件的作用域中。**

上面例子中，在子组件**Child**中绑定了onClick事件。 调用this.change方法。

> 注意change函数采用了箭头函数的写法 change=()=>\\{\\}，目的是**为了改变this的指向，使得在函数单独调用的时候，函数内部的this依然指向child组件**
>
> 如果不使用**箭头函数**，而是采用普通的写法
> **change()\\{
> \\}**
> 则需要在 constructor中绑定this,
> **this.change=this.change.bind(this)**
>
> 或者在onClick方法中绑定this,
> **onClick=\\{this.change=this.change.bind(this)\\}**

在**change**方法中，通过**props**发送出去一个方法，比如说叫**callback**方法，父组件中去接收这个方法，**callback=\\{this.callback\\}**，然后在自身的callback函数中进行一些列操作。

本例中，函数**callback**中就是通过调用 **setState**方法来改变值。

点击按钮后页面显示:

![img](https:////upload-images.jianshu.io/upload_images/6177839-78d8d0166789aa61.jpg?imageMogr2/auto-orient/strip|imageView2/2/w/289/format/webp)

 可以看到，我们既实现了通过props将父组件里面的数据传递给子组件的效果，也实现了通过子组件按钮点击事件，将子组件里面的数据发送给父组件



### React严格模式-React.StrictMode

严格模式在官网中这样介绍：

> **StrictMode** 是一个用以标记出应用中潜在问题的工具。就像 **Fragment** ，**StrictMode** 不会渲染任何真实的UI。它为其后代元素触发额外的检查和警告。

**注意: 严格模式检查只在开发模式下运行，不会与生产模式冲突。**

你可以在代码的任何地方启用严格模式。例如：

```jsx
// 文件入口
React.render(
    <React.StrictMode>
        <App />
    </React.StrictMode>,
    document.getElementById("root")
)

// 单个组件中
import React from "react";

function Home() \\{
    return (
        <div className="home">
            <React.StrictMode>
                <ComponentTable />
                <ComponentDialog />
            </React.StrictMode>
            <CommonInfo />
        </div>
    )
\\}
```

上述栗子🌰中，在`文件入口`中使用，会对它的所有后代元素都进行检查；在`单个组件`中使用，会对`ComponentTable`和`ComponentDialog`以及他们的所有后代元素进行检查，不会对`CommonInfo`组件运行严格模式。

#### 使用`StrictMode`的优点：

- 识别不安全的生命周期组件
- 有关旧式字符串ref用法的警告
- 关于使用废弃的 findDOMNode 方法的警告
- 检测意外的副作用
- 检测过时的 context API



### 引入 public 文件夹下的图片

```html
<img src="/images/03.png"/>
```

这是因为用 create-react-app搭建的 react 项目会以 public 文件夹为根目录



### react中常用标签

```
<br/>//换行
<hr/>//分割线
```



### REACT操作DOM元素的两种方式

#### 一：使用选择器：

1、引入react-dom

```
import ReactDom from 'react-dom'
```

2、给react节点设置id或类名等标识

```
 <span id='tip'></span>
```

3、定义变量保存dom元素

```
var span = document.getElementById('tip')
```

4、通过ReactDom的findDOMNode()方法修改dom的属性

```
ReactDom.findDOMNode(span).style.color = 'red'
```

#### 二：使用ref属性

1、给指定标签设置ref属性

```
<span ref='tip'></span>
```

2、通过this.refs.ref属性值来修改标签的属性

```
this.refs.tip.style.color = "red"
```



### React点击事件的两种写法

#### 1.bind绑定（推荐）

第一个参数指向this，第二个参数开始才是事件函数接收到的参数，事件对象`event`默认是最后一个参数。

```csharp
clicked(param,event)\\{
    console.log(param) //hello world
    console.log(event.target.value) //按钮
\\}

render()\\{
    return (
        <React.Fragment>
            <button value="按钮" onClick=\\{this.clicked.bind(this,"hello world")\\}>点击</button>
        </React.Fragment>
    )
\\}
```

这里的话绑定`this`可以统一写，这样代码看起来整洁点。

```jsx
constructor(props)\\{
    super(props);
    this.state = \\{\\};
    this.checkMenu = this.checkMenu.bind(this);
\\}

clicked = (param)=>\\{
    return (event)=>\\{
        console.log(event.target.value); // 按钮
        console.log(param); // hello
    \\}
\\}

render()\\{
    return (
        <React.Fragment>
            <button value="按钮" onClick=\\{this.clicked('hello')\\}>点击</button>
        </React.Fragment>
    )
\\}
```

#### 2.箭头函数

箭头函数若要传事件对象`event`的话，需要在箭头函数中把`event`作为参数传递给触发的事件。

```csharp
clicked(param,event)\\{
    console.log(param) //hello world
    console.log(event.target.value) //按钮
\\}

render()\\{
    return (
        <React.Fragment>
            <button value="按钮" onClick=\\{(event)=>this.clicked("hello world",event)\\}>点击</button>
        </React.Fragment>
    )
\\}
```



### react方法传参的两种方式

#### 1.使用bind

```
import React, \\{ Component \\} from 'react'
class App extends Component\\{
  constructor(props)\\{
    super(props)
    this.state = \\{
      test:"哈哈"
    \\}
  \\}
  render()\\{
    return(
      <div>
        <button onClick=\\{this.getValue.bind(this,this.state.test)\\}>确定</button>
      </div>
    )
  \\}
  getValue(val)\\{
    console.log(val);
  \\}
\\}
export default App ;
```

#### 2.使用箭头函数

```
import React, \\{ Component \\} from 'react'
class App extends Component \\{
  constructor(props) \\{
    super(props)
    this.state = \\{
      test: "哈哈"
    \\}
  \\}
  render() \\{
    return (
      <div>
        <button onClick=\\{() => this.getVal(this.state.test)\\}>确定</button>
      </div>
    )
  \\}

  getVal = (val) => \\{
    console.log(val);
  \\}
\\}
export default App;
```



### 前端React注释方法

#### jsx注释

使用react在jsx里加注释时，应使用大括号包裹注释行，例如：

```
var content = (
    <Nav>
      \\{/* child comment, put \\{\\} around ,使用大括号包裹标签内的注释行*/\\}
      <Person
        /* multi
           line
           comment js本身注释方法*/
        name=\\{window.isLoggedIn ? window.name : ''\\} // end of line comment
      />
    </Nav>
  );
```

#### html注释

<!--...--> 注释标签用来在源文档中插入注释。注释不会在浏览器中显示。

```
<!--这是一个注释，注释在浏览器中不会显示-->
```

#### css注释

/* */风格的注释语法可以用作单行注释,也可以用作多行注释。在外部独立的CSS文件中,再没有其他注释CSS代码的方法了.不过,如果CSS代码写在了<style>标签中,则在某些旧版浏览器中,你还可以使用<!-- -->来注释CSS代码,虽然这样做是不推荐的,因为在其他大部分语言中,都支持/* */这样的语法来进行注释.需要注意的是,这种风格的注释无法嵌套,也就是说,一旦遇到第一个*/记号,就一定会结束注释。

```
/* 这是一行单行注释 */

/*
这个注释分散
在了多个物理
行上面
*/
```



### react中引用本地图片

#### 第一种导入图片路径

```jsx
import Img from "./images/1.png"
<img src=\\{Img\\} alt=""/>
```

#### 第二种直接获取图片

```jsx
<img src=\\{require("./images/1.png")\\} alt=""/>
```

#### 如果是背景图的话操作style

```jsx
style=\\{\\{background:\`url($\\{require("./images/1.png")\\})\`\\}\\}
```

> $\\\{\\\} 为字符串模板,要用反引号``

#### 背景图片引入

1 第一种就是常规的 新建一个css文件，然后就可以直接写css语法了

```
.img \\{
   background: url('../images/picture.png') 0 0 no-repeat;
\\}
```

2 第二种就是在react组件中通过变量的方式引入,然后直接将变量赋值给img标签

// 引入图片文件
import bg from '../images/bg.png'

```
// 通过字符串拼接的方式定义一个样式对象
const imgStyle = \\{
  width: '100\\%',
  height: '500px',
  backgroundImage: 'url(' + bg + ')',
  backgroundPosition: 'center 0',
  backgroundSize: '2045px 472px',
  backgroundRepeat: 'no-repeat'
\\}
class Home extends Component \\{
	constructor () \\{
		super (props)
	\\}
	render() \\{
		// 最后直接将变量赋值给标签

		<div style="imgStyle">
			...
		</div>
	\\}
\\}
```

#### 选项1：`import`将图像导入组件

将图像文件放在`src`文件夹下的某个位置。仅此一项将不会自动使其可用，因此您必须将图像导入到使用它的React组件中。

```
import companyLogo from './path/to/logo.jpg';
```

然后，您可以通过该变量名称来引用它。名称可以是您想要的任何名称，不必与图像匹配或任何其他名称。

无论您要在哪里显示图像，请渲染`img`标签并将该变量作为传递`src`：

```
function Home() \\{
  return (
    <div>
      <img src=\\{companyLogo\\} alt="BigCo Inc. logo"/>
    </div>
  );\\}
```

请注意，我正在使用，`src=\\{companyLogo\\}`而不是`src="companyLogo"`！如果使用带引号的字符串`"companyLogo"`，它将尝试在处获取文件，`/companyLogo`这将失败。如果您使用的是导入的图像，请确保使用花括号。花括号是将JS变量作为道具传递的方式。

#### 选项2：将图片放在`public`目录中

您可以将图像文件放在`public`文件夹中（或者如果不是Create React App…，那么将被复制到服务器的任何文件夹）。

然后，假设您的服务器将公用文件夹视为“根”目录（`/`），则您的图像将相对于该目录可用-就像纯HTML一样。

因此，如果您在拥有一张图片`public/images/thing.jpg`，则可以通过以下方式显示该图片：

```
function Home() \\{
  return (
    <div>
      <img src="images/logo.jpg" alt="BigCo Inc. logo"/>
    </div>
  );\\}
```

由于此方法使图像可以在Web服务器上作为常规文件使用，因此您可以通过`http://localhost:3000/images/logo.jpg`在浏览器中打开（或在部署后知道您的实际域名！）对其进行测试。

#### 导入的图像如何在React中工作

首先，要知道`import`s根本不是由React处理的-它们是由您的捆绑程序（可能是Webpack）处理的。（如果您使用的是Create React App，则肯定是Webpack）

Webpack，Rollup，Parcel和其他`import`捆绑器在概念上都以相同的方式工作：当您使用静态文件（例如图像或CSS文件）时，捆绑器实际上不会将该文件粘贴到该`import`位置。相反，它指出此特定JS文件取决于此特定图像/ CSS文件/所有内容。

然后，打包程序将使用生成的唯一名称（如`a5c8d3f89cad.jpg`）将映像复制到输出目录，然后在后台将其替换`<img src=\\{yourName\\}/>`为`<img src="a5c8d3f89cad.jpg"/>`。

如果图像特别小，Webpack甚至可能决定将其内联到JS捆绑软件中，作为一种优化。

这一切都无需担心。

#### img在React中使用标签的最佳方法？

对于与当前组件相关的一次性图像，我喜欢将其导入。导入的图像还有一个好处，就是如果缺少该文件，构建将失败，您会很快发现！因此，如果要使用图像，我倾向于导入图像。

对于整个站点范围内的通用图像，或手动导入它们会很烦人的地方，我将其公开发布。当React应用仅占整个站点的一小部分，并且React和其他非React页面都应使用相同的图像时，这尤其有用。在这种情况下，我宁愿避免复制图像（可能会导致副本不同步）。



### 循环/动态样式

```
titles.map((item, index) => \\{
            return (
              <div className="tab-item" onClick=\\{e => this.itemClick(index)\\}>
                <span className=\\{"title " + (index === currentIndex ? "active": "")\\}>\\{item\\}</span>
              </div>
            )
          \\})
```



### react 点击列表某一项，当前项 active ，其他项恢复默认； 单选效果，多选效果

开发中经常会遇到这样得场景

点击列表中得某一项，当前项激活，其他项恢复默认 ( 单选样式 )
点击列表中得某一项，当前项激活，再次点击，当前项目恢复默认，不影响其他项 ( 多选样式 )
上代码

test.js

```
import React from 'react'
import './test.scss'
 
class Test extends React.Component \\{
    constructor(props) \\{
        super(props)
        this.state = \\{
            dataList: [
                \\{ name: '这是1111', checked: false, \\},
                \\{ name: '这是2222', checked: false, \\},
                \\{ name: '这是3333', checked: false, \\},
                \\{ name: '这是4444', checked: false, \\}
            ]
        \\}
    \\}
    itemClick(item,index)\\{
        let list = this.state.dataList;
        list.forEach(item=>\\{
            item.checked = false;
        \\})
        list[index].checked = true;
        this.setState(\\{
            dataList:list
        \\})
    \\}
    render() \\{
        return (
            <div className="Test">
                \\{
                    this.state.dataList.map((item, index) => \\{
                        return (
                            <div className=\\{item.checked ? 'item item-active' : 'item'\\} key=\\{index\\} onClick=\\{this.itemClick.bind(this,item,index)\\}>
                                \\{item.name\\}
                            </div>
                        )
                    \\})
                \\}
            </div>
        )
    \\}
\\}
export default Test
```

test.scss

```
.Test \\{

    .item \\{
        line-height: 30px;
    \\}
     
    .item-active \\{
        color: red
    \\}

\\}
```

完成单选效果，主要靠得就是 itemClick 函数

如果需要得是多选效果，将 itemClick 函数 修改为如下即可

```
 itemClick(item,index)\\{
        let list = this.state.dataList;
        list[index].checked = !list[index].checked;
        this.setState(\\{
            dataList:list
        \\})
    \\}
```



### react中三种函数调用方法

#### 方式一：内联调用法

```
import React, \\{ Component \\} from 'react';

class func extends Component\\{
    constructor(porps)\\{
        super(props);
    \\}
    funcOne()\\{
        console.log('内联调用法')
    \\}
    render()\\{
        return (
            <button onClick=\\{this.funcOne.bind(this)\\}></button>
        )
    \\}
\\}
```

#### 方式二：配置中调用法

```
import React, \\{ Component \\} from 'react';

class func extends Component\\{
    constructor(porps)\\{
        super(props);
        this.funcTwo = this.funcTwo.bind(this)
    \\}
    funcTwo()\\{
        console.log('配置中调用法')
    \\}
    render()\\{
        return (
            <button onClick=\\{this.funcTwo\\}></button>
        )
    \\}
\\}
```

#### 方式三：箭头函数调用法（最推荐）

```
import React, \\{ Component \\} from 'react';

class func extends Component\\{
    constructor(porps)\\{
        super(props);
    \\}
    funcThree:() => \\{
        console.log('箭头函数调用法')
    \\}
    render()\\{
        return (
            <button onClick=\\{this.funcThree\\}></button>
        )
    \\}
\\}
```



### React组件绑定this的四种方式

用react进行开发组件时，我们需要关注一下组件内部方法this的指向，react定义组件的方式有两种，一种为函数组件，一种为类组件，类组件内部可以定义一些方法，这些方法的this需要绑定到组件实例上，小编这里总结了一下，一共有四种方案：

#### 第一种方案，在构造函数内部使用bind绑定this，这样做的好处是，避免每次渲染时都要重新绑定

```
import React, \\{Component\\} from 'react'

class Test extends React.Component \\{
    constructor (props) \\{
        super(props)
        this.state = \\{message: 'Allo!'\\}
        this.handleClick = this.handleClick.bind(this)
    \\}

    handleClick (e) \\{
        console.log(this.state.message)
    \\}
    
    render () \\{
        return (
            <div>
                <button onClick=\\{ this.handleClick \\}>Say Hello</button>
            </div>
        )
    \\}

\\}
```

#### 第二种方案同样是用bind，但是这次不再构造函数内部使用，而是在render函数内绑定，但是这样每次渲染都需要重新绑定

```
import React, \\{Component\\} from 'react'

class Test extends React.Component \\{
    constructor (props) \\{
        super(props)
        this.state = \\{message: 'hello!'\\}
    \\}

    handleClick (name, e) \\{
        console.log(this.state.message + name)
    \\}
    
    render () \\{
        return (
            <div>
                <button onClick=\\{ this.handleClick.bind(this, '赵四') \\}>Say Hello</button>
            </div>
        )
    \\}
\\}
```

#### 第三种方案是在render函数中，调用方法的位置包裹一层箭头函数

因为箭头函数的this指向箭头函数定义的时候其所处作用域的this，而箭头函数在render函数中定义，render函数this始终指向组件实例，所以箭头函数的this也指向组件实例，代码如下：

    class Test extends React.Component \\{
        constructor (props) \\{
            super(props)
            this.state = \\{message: 'Allo!'\\}
        \\}
    	handleClick (e) \\{
        	console.log(this.state.message)
    	\\}
    
    	render () \\{
        	return (
            	<div>
                	<button onClick=\\{ ()=>\\{ this.handleClick() \\} \\}>Say Hello</button>
            	</div>
        	)
    	\\}


以上这种方式有个小问题，因为箭头函数总是匿名的，如果你打算移除监听事件，是做不到的，那么怎么做才可以移除呢？看下一种方案。

#### 第四种方案，代码如下：

```
class Test extends React.Component \\{
    constructor (props) \\{
        super(props)
        this.state = \\{message: 'Allo!'\\}
    \\}

    handleClick = (e) => \\{
        console.log(this.state.message)
    \\}
     
    render () \\{
        return (
            <div>
                <button onClick=\\{ this.handleClick \\}>Say Hello</button>
            </div>
        )
    \\}

\\}
```


不过，在Classes中直接赋值是ES7的写法，ES6并不支持，你有两种选择，一种是配置你的开发环境支持ES7，一种使采用如下方式，下面这种方式是第四种方案的另外一种写法，代码如下：

```
class Test extends React.Component \\{
    constructor (props) \\{
        super(props)
        this.state = \\{message: 'Allo!'\\}
        this.handleClick = (e) => \\{
            console.log(this.state.message)
        \\}
    \\}

    render () \\{
        return (
            <div>
                <button onClick=\\{ this.handleClick \\}>Say Hello</button>
            </div>
        )
    \\}
```



### mobx和redux的区别

可以先从共同点，每一个的具体用法，区别进行回答。

#### 1.共同点：

- 两者都是为了解决状态不好管理，无法有效同步的问题而产生的工具。
- 都是用来统一管理应用状态的工具
- 某一个状态只有一个可靠的数据来源
- 操作更新的方式是统一的，并且是可控的
- 都支持store与react组件，如react-redux,mobx-react;

#### Redux

是一个JavaScript库，通过action（一个对象，包含type，和payload属性）中的type判断需要处理的数据是什么，通过payload进行数据负载，Reducer是一个纯函数，用来通过对应每一个action中的type去进行对应的store中的数据进行操作，有两个参数，第一个是store的初始值，第二个是action。

store提供三个功能，1.getstate()获取数据，2.dispatch(action)监听action的分发进行数据更新，3.支持订阅store的变更（subscribe(listenner)）当数据，

总而言之，当组件中使用store，可以通过getstate()获取到数据，通过dispatch(action)进行数据的更新，通过subscribe监听到数据，当对应的store中的数据也被修改时，组件中的数据也会相应改变。
在redux中纯在异步流，由于Redux对所有的store数据的变更，都应该通过action触发，异步任务（通常是业务或者是获取数据任务）也不例外，而为了不将业务或数据相关的任务混入react组件中，就需要使用其它框架配合管理异步流程，如redux-thunk,和redux-saga等。

#### Mobx

Mobx是一个透明函数响应式编程的状态管理库（Transparently Functional Reactive Programming,TFPR）,它使得状态管理简单可压缩：
-Mobx在action中定义改变状态的动作函数，包括如何变更状态。
-Mobx在store中集中管理状态(state)和动作(action)

#### Mobx和Redux的对比总结

1.redux将数据保存在单一的store中，而mobx将数据保存在分散的多个store中
2.redux使用plain object保存数据，需要手动处理变化后的操作，mobx使用observable保存数据，数据变化后自动处理响应的操作。
3.redux使用的是不可变状态，意味着状态只是只读的，不能直接去修改它，而是应该返回一个新的状态，同时使用纯函数；mobx中的状态是可变的，可以直接对其进行修改。
4.mobx相对来说比较简单，在其中有很多的抽象，mobx使用的更多的是面向对象的思维，redux会比较复杂，因为其中的函数式编程思想掌握起来不是那么容易，同时需要借助一系列的中间件来处理异步和副作用。
5.mobx中有更多的抽象和封装，所以调试起来会更加复杂，同时结果也更难以预测，而redux提供可以进行时间回溯的开发工具，同时其纯函数以及更少的抽象，让调试变得更加容易。

#### 关键词：

**mobx:面向对象思维、多个store、observable自动响应变化操作、mobx状态可变，直接修改、更多的抽象和封装，调试复杂，结果难以预测。**

**redux:函数式编程思想、单一store，plan object保存数据，手动处理变化后的操作、使用不可变状态，意味着状态只读，使用纯函数修改，返回的是一个新的状态、提供时间回溯的开发工具。**



### prop-types

```
npm install prop-types
```

propTypes能用来检测全部数据类型的变量，包括基本类型的的字符串，布尔值，数字，以及引用类型的对象，数组，函数，甚至还有ES6新增的符号类型

```
Son.propTypes = \\{
     optionalArray: PropTypes.array,//检测数组类型
     optionalBool: PropTypes.bool,//检测布尔类型
     optionalFunc: PropTypes.func,//检测函数（Function类型）
     optionalNumber: PropTypes.number,//检测数字
     optionalObject: PropTypes.object,//检测对象
     optionalString: PropTypes.string,//检测字符串
     optionalSymbol: PropTypes.symbol,//ES6新增的symbol类型
\\}
```



### 条件判断的几种形式

解决的办法有以下几种：

使用三目运算符

设置一个变量，并在属性中引用它
讲逻辑信息封装到函数中
使用 && 运算符

#### 三目运算符

```
var IvanIf = React.createClass(\\{
    getInitialState:function () \\{
        return \\{ isComplete:true \\};
    \\},
    render: function () \\{
        return(
            <div className=\\{ this.state.isComplete ? 'is-complete' : '' \\}> Hello Ivan .</div>
        );
    \\}
\\});
```

虽然以上的三目运算符可以正常运行，但如果你想要在其他情况下很好的应用React Component时，可能就显得笨重又麻烦了，所以此方法是不做推荐使用的。

#### 使用变量

```
var IvanIf = React.createClass(\\{
    getInitialState:function () \\{
        return \\{ isComplete:true \\};
    \\},
    getIsComplete:function()\\{
      return this.state.isComplete ? 'is-complete' : '' ;
    \\},
    render: function () \\{
        var isComplete = this.getIsComplete();
        return(
            <div className=\\{ isComplete \\}> Hello Ivan .</div>
        );
    \\}
\\});
```

其实就是将条件判断单独的抽离出去，在render中使用函数调用的形式来获取条件结果。

#### 使用函数

```
var IvanIf = React.createClass(\\{
    getInitialState:function () \\{
        return \\{ isComplete:false \\};
    \\},
    getIsComplete:function()\\{
      return this.state.isComplete ? 'is-complete' : '' ;
    \\},
    render: function () \\{
        return(
            <div className=\\{ this.getIsComplete() \\}> Hello Ivan .</div>
        );
    \\}
\\});
```

有种然并卵的赶脚

#### 使用逻辑与(&&)运算符

```
var IvanIf = React.createClass(\\{
    getInitialState:function () \\{
        return \\{ isComplete:false \\};
    \\},
    render: function () \\{
        return(
            <div className=\\{ this.state.isComplete && 'is-complete' \\}> Hello Ivan .</div>
        );
    \\}
\\});
```

由于对于null 或 false 值，React不会输出任何内容，因此可以使用一个后面跟随了期望字符串的boolean值来实现条件判断。 
如果这个boolean值为true，那么后续的字符串会被使用，反之，则不会被使用



### react 父组件如何调用子组件的方法

父组件

```
 bindRef (ref) \\{
    this.child = ref
  \\}
  clickMethod = () => \\{
    this.child.childMethod()
  \\}
  render () \\{
    return (
      <div className='wrapper'>
        <p onClick=\\{this.clickMethod\\}>这是一个click事件</p>
        <child onRef=\\{this.bindRef.bind(this)\\}></child>
      </div>
    )
  \\}
```

子组件

```
 childMethod () \\{
    console.log('我是子组件的方法')
  \\}
  componentDidMount () \\{
    this.props.onRef(this)
  \\}
```



### React页面嵌套

些组件使用一个特殊的 `children` prop 来将他们的子组件传递到渲染结果中：

```
function FancyBorder(props) \\{
  return (
    <div className=\\{'FancyBorder FancyBorder-' + props.color\\}>
      \\{props.children\\}//或者\\{this.props.children\\}
    </div>
  );
\\}
```

这使得别的组件可以通过 JSX 嵌套，将任意组件作为子组件传递给它们。

```
function WelcomeDialog() \\{
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">
        Welcome
      </h1>
      <p className="Dialog-message">
        Thank you for visiting our spacecraft!
      </p>
    </FancyBorder>
  );
\\}
```

`<FancyBorder>` JSX 标签中的所有内容都会作为一个 `children` prop 传递给 `FancyBorder` 组件。因为 `FancyBorder` 将 `\\{props.children\\}` 渲染在一个 `<div>` 中，被传递的这些子组件最终都会出现在输出结果中。



### React中props和state的区别

需要理解的是，props是一个**父组件传递给子组件的数据流**，这个数据流可以一直传递到子孙组件。而state代表的是**一个组件内部自身的状态**（可以是父组件、子孙组件）。改变一个组件自身状态，从语义上来说，就是这个组件内部已经发生变化，有可能需要对此组件以及组件所包含的子孙组件进行重渲染。而props是父组件传递的参数，可以被用于显示内容，或者用于此组件自身状态的设置（部分props可以用来设置组件的state），不仅仅是组件内部state改变才会导致重渲染，父组件传递的props发生变化，也会执行。既然两者的变化都有可能导致组件重渲染，所以只有理解pros与state的意义，才能很好地决定到底什么时候用props或state。

官方指导有说，props放初始化数据，一直不变的，state就是放要变的。

State应该包括那些可能被组件的事件处理器改变并触发用户界面更新的数据,因为组件本身不能修改自己的 props。

props是我们给组件的数据，而state是组件本地或者私有的数据容器，其他的组件时不能访问这个组件的state的，它完全**只能在组件内被访问**。
另外，**props是只读的，我们不能在组件内部改变组件的输入数据。**

props和state都是用于描述component状态的，并且这个状态应该是与显示相关的。
1.State（由内部改变的）

如果component的某些状态需要被改变，并且会影响到component的render，那么这些状态就应该用state表示。
例如：一个购物车的component，会根据用户在购物车中添加的产品和产品数量，显示不同的价格，那么“总价”这个状态，就应该用state表示。

2.Props（由外部传送的）

如果component的某些状态由外部所决定，并且会影响到component的render，那么这些状态就应该用props表示。
例如：一个下拉菜单的component，有哪些菜单项，是由这个component的使用者和使用场景决定的，那么“菜单项”这个状态，就应该用props表示，并且由外部传入。



### JSX基本语法中关于react如何写css样式主要有三种方法

#### 1、基于class --（className）

基于className ,通过className在style中给该class名的DOM元素添加样式

```
 1 <style>
 2 .title\\{
 3     color:blue;
 4 \\}
 5 </style>
 6 
 7 
 8 <div id='app'></div>
 9 //创建一个叫App类，继承（extends)了react中创建组件的方法(component)
10 class App extends React.Component\\{
11     constructor(props)\\{  
12         super(peops)
13     \\}
14     render()\\{   //类里面负责构建HTML的位置，render渲染
15         return(  //返回HTML结构
16         <div  className="title">高版本</div>
17         
18         )
19     \\}
20 \\}
21 
22 //将虚拟DOM以组件标签的形式渲染到id为'app'的真实DOM之间
23 ReactDOM.render(<App/>,document.getElementById('app'))
```

#### 2、基于inner css （facebook 主张的方式） 行间样式(json)

Facebook主张的是行间样式，直接给对应的DOM元素添加style属性，遵循react的规则，写在\\{ \\}当中。

#### 3、原型链和全局变量

可以通过定义全局变量的方法来定义一个css样式，适用该样式的DOM元素可直接调用。

原型链中需要注意添加样式的位置，调用时通过this，this指向该组件

```
<div id='app'></div>
//全局样式方法
var color=\\{color:'red'\\}

class App extends React.Component\\{
    constructor(props)\\{  
        super(peops)
    \\}
    render()\\{   
        return( 
         <div style=\\{color\\}>react全局行间样式</div>
         //this 指向组件本身
         <div style=\\{this.col\\}>原型样式</div>
        )
    \\}
\\}
//原型链样式的写法，在创建完以及渲染中间的位置添加原型上的样式
App.prototype.col=\\{
    color:pink  
\\}

//将虚拟DOM以组件标签的形式渲染到id为'app'的真实DOM之间
ReactDOM.render(<App/>,document.getElementById('app'))
```



### react使用style和select

```
<select>
	<option value="volvo" style=\\\{\\\{ display: "none" \\\}\\\}>报警标签</option>
	<option value="">天气原因</option>
	<option value="">未知事物</option>
	<option value="">垃圾触碰</option>
	<option value="">施工</option>
	<option value="">飞机尾气</option>
	<option value="">守卫测试</option>
	<option value="">动物</option>
	<option value="">工作人员</option>
	<option value="">外围人员</option>
	<option value="">入侵</option>
</select>
```
