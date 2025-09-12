---
title: Redux
date: 2019-11-17 17:11:07
categories: 
- 前端知识
tags:
- React
---

### Store

就是把它们联系到一起的对象。Store 有以下职责：

- 维持应用的 state；
- 提供 [`getState()`](http://cn.redux.js.org/docs/api/Store.html#getState) 方法获取 state；
- 提供 [`dispatch(action)`](http://cn.redux.js.org/docs/api/Store.html#dispatch) 方法更新 state；
- 通过 [`subscribe(listener)`](http://cn.redux.js.org/docs/api/Store.html#subscribe) 注册监听器;
- 通过 [`subscribe(listener)`](http://cn.redux.js.org/docs/api/Store.html#subscribe) 返回的函数注销监听器。

再次强调一下 Redux 应用只有一个单一的 store。当需要拆分数据处理逻辑时，你应该使用 [reducer 组合](http://cn.redux.js.org/docs/basics/Reducers.html#splitting-reducers)而不是创建多个 store。



### 1、基本用法：

- Redux中存在几个概念：state, action, dispatch

  **state:** 依旧是组件的内部的状态
   **action:** 组件动作，相应的改变组件内部的状态值
   **dispatch:** 发出相应的动作

  Redux中提供createStore方法用于生成一个store对象，这个函数接受一个初始值state值和一个reducer函数。当用户发出相应的action时，利用传入的reducer函数计算出一个新的state值，并返回。

- 使用**Redux**，我们只获取一次数据并将其存储在一个中心位置，称为 **store**。然后，任何组件都可以随时使用这些数据。这就像附近有一家超市，我们的厨师可以在那里买到所有的食材。这家超市派卡车从农场大批运回蔬菜和肉类。这比让个别厨师亲自去农场效率高得多。

- **store** 还是唯一的数据源。组件通常从 `store` 中获取数据，而不是其他地方。这使得 UI 保持高度统一。

- store对象中包括getState方法(获取目前的state)，subscribe方法(指定监听函数，当state变化时调用)，dispatch方法(分发action)。

- 在使用过程中，需要将store作为参数传递给子组件。

```jsx
// reducer
function counter(state = 0, action) \\{
  switch (action.type) \\{
    case 'ADD':
      return state + 1;
    case 'SUB':
      return state - 1;
    default:
      return 10;
  \\}
\\}

// 创建Store
let store = createStore(counter);
console.log(store.getState()); // 10

// 监听器
function listener() \\{
  console.log(store.getState()) // 先输出11，在输出10
\\}

// 订阅事件监听
store.subscribe(listener);

// 分发事件
store.dispatch(\\{ type: 'ADD' \\});

store.dispatch(\\{ type: 'SUB' \\});
```

- 多个reducer

  当存在多个reducer，分别管理不同方面的state，需要将其合并成一个reducer，redux中提供了combineReducers函数，完成该项功能。

```cpp
combineReducers(\\{ reducer1,reducer2 \\}) //返回合并后的reducer
```



### 2、redux的不足：

- **陡峭的学习曲线**

  Redux　的学习曲线比较陡峭。 理解，记忆并习惯其模式需要时间。 如果你完全不会 Redux 和 React ，不推荐你两者同时学习。

- **“样板” 代码**

  在许多情况下，使用Redux意味着编写更多代码。通常需要接触多个文件才能使一个简单的功能正常工作。人们一直在抱怨他们必须用 Redux 编写的样板代码。

  我知道，这听起来很矛盾。 我不是说 Redux 能够用最少的代码实现功能吗？ 这有点像使用洗碗机。 首先，你得花时间仔细地排列盘子。 在此之前，你将看到洗碗机的好处：节省实际清洁餐具的时间，消毒餐具等。你必须决定准备时间是否值得。

- **性能损耗**

  由于其强制执行的限制，Redux 也可能对性能产生影响。 每当数据发生变化时，它会增加一点开销。 在大多数情况下，这不是什么大问题，而且放缓并不明显。 仍然，当存储中存在大量数据并且当数据频繁改变时（例如，当用户在移动设备上快速键入时），UI 可能因此变得缓慢。



### 3、Redux 不只是为 React 而生

- 一个常见的误解是 Redux 仅用于 React。 听起来Redux在没有React的情况下无法做任何事情。 事实上，正如我们之前所讨论的，Redux在几个重要方面补充了React。 React 是最最常见的 Redux 用例。
- 然而，事实上，Redux可以使用任何前端框架，如Angular、Ember.js 甚至jQuery 或者 普通的JavaScript。试着谷歌一下，你会发现这个，这个，这个甚至这个。Redux 的一般思想适用于任何地方
- 只要你明智地使用 Redux，你可以在很多情况下得到它的好处，而不仅仅是在React应用中。



### react-redux

- react-redux是为了方便开发，提供了一个Provider组件，以及connect方法。Provider组件作为做上层组件，需要将store作为参数注入组件中，此后在子组件中都可以访问到store这个对象；connect方法接受两个参数：mapStateToProps，actionCreators，并返回处理后的组件，其中mapStateToProps可以将对应的state作为prop注入对应的子组件，actionCreator可以将对应的actioncreator作为prop注入对应的子组件。

```dart
// 定义Connect,将对应的数据注入
const mapStateToProps = (state) => \\{
  return \\{ num: state \\}// 必须返回一个对象
\\};
const actionCreator = \\{ addAction, subAction, addActionAsync \\}

App = connect(mapStateToProps, actionCreator)(App)
```

- **装饰器写法：**

```dart
@connect(
  (state) => (\\{ num: state.counter \\}),
  \\{ addAction, subAction, addActionAsync \\}
)
```

- 使用上述写法，需要安装babel插件babel-plugin-transform-decorators-legacy，并且在babelrc中添加相应的配置

```undefined
 npm install --save-dev babel-plugin-transform-decorators-legacy
```

```bash
 "plugins": [
   "transform-decorators-legacy"
]
```



### React-router

- react-router提供了web和Native两个版本，当在浏览器中使用时，需要安装react-router-dom

```undefined
npm install --save react-router-dom
```

- react-router-dom中提供了BrowserRouter, Link, Route, Switch，Redirect。

  其中：
   1、 BrowserRouter包裹所有需要路由控制的内容，在使用redux时，需要放置在Provider组件中；
   2、 Link组件用于链接某个路径下，用户点击跳转；

  3、 Route组件用于路由到这个组件；
   4、Switch组件用于在内部Route组件中选一个；

  5、 Redirect组件用于重定向到某个路径下；

```xml
<Provider store=\\{store\\}>
    <BrowserRouter>
      <Switch>
        <Route path="/" exact component=\\{Dashboard\\}></Route>
        <Route path="/login" component=\\{Auto\\}></Route>
        <Route path="/dashboard" component=\\{Dashboard\\}></Route>
        <!-- <Redirect to="/dashboard"></Redirect>     -->
        <!-- <Link to="/dashboard"></Link> -->
      </Switch>
    </BrowserRouter>
  </Provider>,
```



### react组件中的通信

react推崇的是单向数据流，自上而下进行数据的传递，但是由下而上或者不在一条数据流上的组件之间的通信就会变的复杂。解决通信问题的方法很多，如果只是父子级关系，父级可以将一个回调函数当作属性传递给子级，子级可以直接调用函数从而和父级通信。

组件层级嵌套到比较深，可以使用上下文getChildContext来传递信息，这样在不需要将函数一层层往下传，任何一层的子级都可以通过this.context直接访问。

兄弟关系的组件之间无法直接通信，它们只能利用同一层的上级作为中转站。而如果兄弟组件都是最高层的组件，为了能够让它们进行通信，必须在它们外层再套一层组件，这个外层的组件起着保存数据，传递信息的作用，这其实就是redux所做的事情。

组件之间的信息还可以通过全局事件来传递。不同页面可以通过参数传递数据，下个页面可以用location.param来获取。其实react本身很简单，难的在于如何优雅高效的实现组件之间数据的交流。



### redux的用途和用法

首先，redux并不是必须的，它的作用相当于在顶层组件之上又加了一个组件，作用是进行逻辑运算、储存数据和实现组件尤其是顶层组件的通信。如果组件之间的交流不多，逻辑不复杂，只是单纯的进行视图的渲染，这时候用回调，context就行，没必要用redux，用了反而影响开发速度。但是如果组件交流特别频繁，逻辑很复杂，那redux的优势就特别明显了。我第一次做react项目的时候并没有用redux，所有的逻辑都是在组件内部实现，当时为了实现一个逻辑比较复杂的购物车，洋洋洒洒居然写了800多行代码，回头一看我自己都不知道写的是啥，画面太感人。

先简单说一下redux和react是怎么配合的。react-redux提供了connect和Provider两个好基友，它们一个将组件与redux关联起来，一个将store传给组件。组件通过dispatch发出action，store根据action的type属性调用对应的reducer并传入state和这个action，reducer对state进行处理并返回一个新的state放入store，connect监听到store发生变化，调用setState更新组件，此时组件的props也就跟着变化。



### redux的流程

值得注意的是connect，Provider，mapStateToProps,mapDispatchToProps是react-redux提供的，redux本身和react没有半毛钱关系，它只是数据处理中心，没有和react产生任何耦合，是react-redux让它们联系在一起。

接下来具体分析一下，redux以及react-redux到底是怎么实现的。

先说说redux：
redux主要由三部分组成：store，reducer，action。

store是一个对象，它有四个主要的方法：

#### 1、dispatch:

用于action的分发——在createStore中可以用middleware中间件对dispatch进行改造，比如当action传入dispatch会立即触发reducer，有些时候我们不希望它立即触发，而是等待异步操作完成之后再触发，这时候用redux-thunk对dispatch进行改造，以前只能传入一个对象，改造完成后可以传入一个函数，在这个函数里我们手动dispatch一个action对象，这个过程是可控的，就实现了异步。

#### 2、subscribe：

监听state的变化——这个函数在store调用dispatch时会注册一个listener监听state变化，当我们需要知道state是否变化时可以调用，它返回一个函数，调用这个返回的函数可以注销监听。 let unsubscribe = store.subscribe(() => \\{console.log('state发生了变化')\\})

#### 3、getState：

获取store中的state——当我们用action触发reducer改变了state时，需要再拿到新的state里的数据，毕竟数据才是我们想要的。getState主要在两个地方需要用到，一是在dispatch拿到action后store需要用它来获取state里的数据，并把这个数据传给reducer，这个过程是自动执行的，二是在我们利用subscribe监听到state发生变化后调用它来获取新的state数据，如果做到这一步，说明我们已经成功了。

#### 4、replaceReducer:

替换reducer，改变state修改的逻辑。

store可以通过createStore()方法创建，接受三个参数，经过combineReducers合并的reducer和state的初始状态以及改变dispatch的中间件，后两个参数并不是必须的。store的主要作用是将action和reducer联系起来并改变state。

#### action:

action是一个对象，其中type属性是必须的，同时可以传入一些数据。action可以用actionCreactor进行创造。dispatch就是把action对象发送出去。

#### reducer:

reducer是一个函数，它接受一个state和一个action，根据action的type返回一个新的state。根据业务逻辑可以分为很多个reducer，然后通过combineReducers将它们合并，state树中有很多对象，每个state对象对应一个reducer，state对象的名字可以在合并时定义。

像这个样子：

```
const reducer = combineReducers(\\{
     a: doSomethingWithA,
     b: processB,
     c: c
\\})
```

#### combineReducers:

其实它也是一个reducer，它接受整个state和一个action，然后将整个state拆分发送给对应的reducer进行处理，所有的reducer会收到相同的action，不过它们会根据action的type进行判断，有这个type就进行处理然后返回新的state，没有就返回默认值，然后这些分散的state又会整合在一起返回一个新的state树。

接下来分析一下整体的流程，首先调用store.dispatch将action作为参数传入，同时用getState获取当前的状态树state并注册subscribe的listener监听state变化，再调用combineReducers并将获取的state和action传入。combineReducers会将传入的state和action传给所有reducer，并根据action的type返回新的state，触发state树的更新，我们调用subscribe监听到state发生变化后用getState获取新的state数据。

redux的state和react的state两者完全没有关系，除了名字一样。

上面分析了redux的主要功能，那么react-redux到底做了什么？



### React-Redux

如果只使用redux，那么流程是这样的：

```
component --> dispatch(action) --> reducer --> subscribe --> getState --> component
```

用了react-redux之后流程是这样的：

```
component --> actionCreator(data) --> reducer --> component
```

store的三大功能：dispatch，subscribe，getState都不需要手动来写了。react-redux帮我们做了这些，同时它提供了两个好基友Provider和connect。

Provider是一个组件，它接受store作为props,然后通过context往下传，这样react中任何组件都可以通过context获取store.也就意味着我们可以在任意一个组件里利用dispatch(action)来触发readucer改变state,并用subscribe监听state的变化，然后用getState获取变化后的值。但是并不推荐这样做，它会让数据流变的混乱，过度的耦合也会影响组件的复用，维护起来也更麻烦。

connect --connect(mapStateToProps, mapDispatchToProps, mergeProps, options) 是一个函数，它接受四个参数并且再返回一个函数--wrapWithConnect，wrapWithConnect接受一个组件作为参数wrapWithConnect(component)，它内部定义一个新组件Connect(容器组件)并将传入的组件(ui组件)作为Connect的子组件然后return出去。

所以它的完整写法是这样的：connect(mapStateToProps, mapDispatchToProps, mergeProps, options)(component)

#### mapStateToProps(state, [ownProps])：

mapStateToProps 接受两个参数，store的state和自定义的props，并返回一个新的对象，这个对象会作为props的一部分传入ui组件。我们可以根据组件所需要的数据自定义返回一个对象。ownProps的变化也会触发mapStateToProps

```
function mapStateToProps(state) \\{
   return \\{ todos: state.todos \\};
\\}
```

#### mapDispatchToProps(dispatch, [ownProps])：

mapDispatchToProps如果是对象，那么会和store绑定作为props的一部分传入ui组件。如果是个函数，它接受两个参数，bindActionCreators会将action和dispatch绑定并返回一个对象，这个对象会和ownProps一起作为props的一部分传入ui组件。所以不论mapDispatchToProps是对象还是函数，它最终都会返回一个对象，如果是函数，这个对象的key值是可以自定义的

```
function mapDispatchToProps(dispatch) \\{
   return \\{
      todoActions: bindActionCreators(todoActionCreators, dispatch),
      counterActions: bindActionCreators(counterActionCreators, dispatch)
   \\};
\\}
```

mapDispatchToProps返回的对象其属性其实就是一个个actionCreator，因为已经和dispatch绑定，所以当调用actionCreator时会立即发送action，而不用手动dispatch。ownProps的变化也会触发mapDispatchToProps。

#### mergeProps(stateProps, dispatchProps, ownProps)：

将mapStateToProps() 与 mapDispatchToProps()返回的对象和组件自身的props合并成新的props并传入组件。默认返回 Object.assign(\\{\\}, ownProps, stateProps, dispatchProps) 的结果。

options：

pure = true 表示Connect容器组件将在shouldComponentUpdate中对store的state和ownProps进行浅对比，判断是否发生变化，优化性能。为false则不对比。

其实connect函数并没有做什么，大部分的逻辑都是在它返回的wrapWithConnect函数内实现的，确切的说是在wrapWithConnect内定义的Connect组件里实现的。



### 下面是一个完整的 react --> redux --> react 流程：

一、Provider组件接受redux的store作为props，然后通过context往下传。

二、connect函数在初始化的时候会将mapDispatchToProps对象绑定到store，如果mapDispatchToProps是函数则在Connect组件获得store后，根据传入的store.dispatch和action通过bindActionCreators进行绑定，再将返回的对象绑定到store，connect函数会返回一个wrapWithConnect函数，同时wrapWithConnect会被调用且传入一个ui组件，wrapWithConnect内部使用class Connect extends Component定义了一个Connect组件，传入的ui组件就是Connect的子组件，然后Connect组件会通过context获得store，并通过store.getState获得完整的state对象，将state传入mapStateToProps返回stateProps对象、mapDispatchToProps对象或mapDispatchToProps函数会返回一个dispatchProps对象，stateProps、dispatchProps以及Connect组件的props三者通过Object.assign()，或者mergeProps合并为props传入ui组件。然后在ComponentDidMount中调用store.subscribe，注册了一个回调函数handleChange监听state的变化。

三、此时ui组件就可以在props中找到actionCreator，当我们调用actionCreator时会自动调用dispatch，在dispatch中会调用getState获取整个state，同时注册一个listener监听state的变化，store将获得的state和action传给combineReducers，combineReducers会将state依据state的key值分别传给子reducer，并将action传给全部子reducer，reducer会被依次执行进行action.type的判断，如果有则返回一个新的state，如果没有则返回默认。combineReducers再次将子reducer返回的单个state进行合并成一个新的完整的state。此时state发生了变化。dispatch在state返回新的值之后会调用所有注册的listener函数其中包括handleChange函数，handleChange函数内部首先调用getState获取新的state值并对新旧两个state进行浅对比，如果相同直接return，如果不同则调用mapStateToProps获取stateProps并将新旧两个stateProps进行浅对比，如果相同，直接return结束，不进行后续操作。如果不相同则调用this.setState()触发Connect组件的更新，传入ui组件，触发ui组件的更新，此时ui组件获得新的props，react --> redux --> react 的一次流程结束。

上面的有点复杂，简化版的流程是：

一、Provider组件接受redux的store作为props，然后通过context往下传。

二、connect函数收到Provider传出的store，然后接受三个参数mapStateToProps，mapDispatchToProps和组件，并将state和actionCreator以props传入组件，这时组件就可以调用actionCreator函数来触发reducer函数返回新的state，connect监听到state变化调用setState更新组件并将新的state传入组件。

connect可以写的非常简洁，mapStateToProps，mapDispatchToProps只不过是传入的回调函数，connect函数在必要的时候会调用它们，名字不是固定的，甚至可以不写名字。

简化版本：

connect(state => state, action)(Component);



### 项目搭建

上面说了react，react-router和redux的知识点。但是怎么把它们整合起来，搭建一个完整的项目。

1.首先引用react.js，redux，react-router等基本文件，建议用npm安装，直接在文件中引用。

2.从react.js，redux，react-router 中引入所需要的对象和方法。

```
import React, \\{ Componet, PropTypes\\} from 'react';
import ReactDOM, \\{render\\} from 'react-dom';
import \\{Provider, connect\\} from 'react-redux';
import \\{createStore, combineReducers, applyMiddleware\\} from 'redux';
import \\{ Router, Route, Redirect, IndexRoute, browerHistory, hashHistory \\} from 'react-router'
```

3,根据需求创建顶层UI组件，每个顶层ui组件对应一个页面。

4.创建actionCreators和reducers,并用combineReducers将所有的reducer合并成一个大的reducer。利用createStore创建store并引入combineReducers和applyMiddleware.

5.利用connect将actionCreator, reducer和顶层的ui组件进行关联并返回一个新的组件。

6.利用connect返回新的组件配合react-router进行路由的部署，返回一个路由组件Router.

7.将Route放入顶层组件Provider,引入store作为Provider的属性。

8.调用render渲染Provider组件且放入页面的标签中。

可以看到顶层的ui组件其实被套用了四层组件，Provider, Router, Route, Connect,这四个组件并不会在视图改变react,他们只是功能性的。

通常我们在顶层的ui组件打印props时可以看到一堆属性：

顶层的UI组件属性总共有18个，如果刚刚接触react,可能对这些属性怎么来的感到困惑，其实这些属性来自五个地方：

组件自定义属性1个，actionCreator返回的对象6个，reducer返回的state 4个，Connect组件属性0 个，以及Router注入的属性7个。



### redux中state不能直接修改

redux中不能直接修改state原因：

 redux会通过引用来判断前后两次state有没有变化

```
直接修改了state对象，然后返回的还是原来的state对象（被修改过的）复制代码
return原来的state的话redux会认为你的state没有变化,从而无法记录时光旅行，快照，历史等。
那么react组件就认为state无变化则不更新组件复制代码
```

解决方案：创建新的对象，改变引用（创建新的引用）,新建了一个副本。

```
   Object.assign(\\{\\}, state, \\{
        visibilityFilter: action.filter
   \\})
```

  或者

```
  \\{...state, visibilityFilter: action.filter\\} 
```

