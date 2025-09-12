---
title: vue递归组件
date: 2024-03-09 08:02:08
categories: 
- 前端知识
tags:
- vue
---

# 递归组件

对于一些有规律的DOM结构，如果我们再一遍遍的编写同样的代码，显然代码是比较繁琐和不科学的，而且自己的工作量会大大增加。

那么有没有一种方法来解决这个问题呢？

答案是肯定的，我们可以通过 递归 方式来生成这个结构，我们可以在 Vue 的组件中调用自己本身，这样就能达到目的。

### 递归组件是什么？

字面理解为层层递进最后归并到一起， 简单来说就是在组件中内使用组件本身，它的特点就是层级分明。
例如饿了么和iview组件库的“树组件”就是一个递归。

https://element.eleme.cn/#/zh-CN/component/tree

http://v4.iviewui.com/components/tree 

### 递归条件

- 该组件一定要有 name 属性

  如果没有 name 这个属性会造成控件自身不能调用自身，而且调用的时候最好绑定一个 key 值，因为这个 key 值是唯一的标识

- 要确保递归的调用有终止条件，防止内存溢出

### Vue实现递归的核心思路

1、循环出一级类别
2、判断如果有多级，再调用自身。

父组件传过来的树形数据结构到子组件后，我们需要拿到数据并做遍历，然后再下一行加入核心逻辑：if 发现我们有子数据，那么我们直接调用自身组件，也就是直接使用name值做组件声明。最关键的是要把子数据结构再传入我们自身组件，那么我们就成功的实现了数据的层层遍历。 

### 代码实现

首先我们先创建一个 List 的递归组件 

```
<template>
    <div>
        <div class="list-item" v-for="(item, index) in list" :key="index">
            <div class="item-name">
                <span>\\\{\\\{item.nam\\\}\\\}e}}</span>
            </div>
            <div v-if="item.children" class="children-item">
                <list :list="item.children"></list>
            </div>
        </div>
    </div>
</template>
<script>
export default \\{
  name: "List",
  props: \\{
    list: Array
  \\}
\\};
</script>
```

注意上面的代码中我们使用了 List 组件本身，完成这些之后，我们在外部父级组件中使用 List 组件时，不管我们的数据有多少层嵌套关系，都可以完美的自适应加载，我们再也不用通过嵌套嵌套在嵌套了。 

```
<template>
    <div class="list-detail">
      <list :list="list"></list>
    </div>
</template>
<script>
import List from "./components/List";
export default \\{
  name: "Parent",
  components: \\{ List \\},
  data() \\{
    return \\{
      list: [\\{
          name: "经济",
          children: [\\{
              name: "如家",
              children: [\\{
                  name: "上江路-如家"
                \\},
                \\{
                  name: "望江路-如家"
                \\}]
            \\},\\{
              name: "7天",
              children: [\\{
                  name: "长江路-7天"
                \\},
                \\{
                  name: "望江路-7天"
                \\}]
            \\}]
        \\}]
    \\}
  \\}
\\}
</script>
```



### vue中递归调用自身的组件如何向父组件传值

目前写了一个递归的树形目录，通过调用自己的name的方式来循环的调用自身，但是问题来了，这个是一个子组件，这样循环调用后，无法向它的父组件传值了，这种该怎么办呢（就第一层可以传，后面的子层都不行，因为它后面的子层父组件就是自己本身） 

到这里我们看似完成了这个数据结构。如果只是展示性质的递归组件，到这里我们就ok了。可是我们的需求是组件还可以操作，有数据的交互，添加删除数据。那么我们就该想，递归组件该怎么来通知我修改了谁的数据？
走到这里我们可能就要考虑数据该放哪儿？该在哪儿去修改数据最为合适？怎么通知数据，我是谁，我修改了谁？既然递归组件，大家都一样，这该通知谁呢？我又是递归的第几层修改的数据呢？ 

#### 组件间数据传递

确定一点，我们是递归组件，不知道层级。也就是说这不是简单的父子之间的传值，也不是兄弟组件的传值

- 一般的prop传值：适合层次清楚且少的传值,父子组件
- this.$children/parent：适合父子组件
- this.$ref: 适合父子组件
- $sttrs/listeners：适合层次清楚的多组件间传值
- Vuex： 状态管理，我们这儿只涉及组件，用vuex就大材小用了（但也可以）。适合大型项目
- event bus: 事件总线。注册/监听事件，传递数据。很符合我的需求。





# EventBus

### EventBus的简介

`EventBus` 又称为事件总线。在Vue中可以使用 `EventBus` 来作为沟通桥梁的概念，就像是所有组件共用相同的事件中心，可以向该中心注册发送事件或接收事件，所以组件都可以上下平行地通知其他组件。

但也就是太方便所以若使用不慎，就会造成难以维护的“灾难”，因此才需要更完善的Vuex作为状态管理中心，将通知的概念上升到共享状态层次。



### 如何使用EventBus

#### 一、初始化

首先需要创建事件总线并将其导出，以便其它模块可以使用或者监听它。我们可以通过两种方式来处理。先来看第一种，新创建一个 .js 文件，比如 `event-bus.js`

```text
// event-bus.js
// 方式一
import Vue from 'vue'
export const EventBus = new Vue()
```

实质上`EventBus`是一个不具备 `DOM` 的组件，它具有的仅仅只是它实例方法而已，因此它非常的轻便。

另外一种方式，可以直接在项目中的 `main.js` 初始化 `EventBus` :

全局定义，可以将eventBus绑定到vue实例的原型上,也可以直接绑定到window对象上 

```text
//main.js
// 方式二
Vue.prototype.$EventBus = new Vue();
// 方式三
window.eventBus = new Vue();
```

注意，这种方式初始化的`EventBus`是一个`全局的事件总线`。

现在我们已经创建了 `EventBus` ，接下来你需要做到的就是在你的组件中加载它，并且调用同一个方法，就如你在父子组件中互相传递消息一样。

#### 二、发送事件

假设你有两个Vue页面需要通信： A 和 B ，A页面 在按钮上面绑定了点击事件，发送一则消息，想=通知 B页面。

```text
// 方式一
<!-- A.vue -->
<template>
    <button @click="sendMsg()">-</button>
</template>

<script> 
import \\{ EventBus \\} from "../event-bus.js";
export default \\{
  methods: \\{
    sendMsg() \\{
      EventBus.$emit("aMsg", '来自A页面的消息');
    \\}
  \\}
\\}; 
</script>
```

```
// 方式二
this.$EventBus.$emit('eventName', param1,param2,...)
// 方式三
EventBus.$emit('eventName', param1,param2,...)
```

接下来，我们需要在 B页面 中接收这则消息。

#### 三、接收事件

```text
// 方式一
<!-- IncrementCount.vue -->
<template>
  <p>\\\{\\\{ms\\\}\\\}g}}</p>
</template>

<script> 
import \\{ 
  EventBus 
\\} from "../event-bus.js";
export default \\{
  data()\\{
    return \\{
      msg: ''
    \\}
  \\},
  mounted() \\{
    EventBus.$on("aMsg", (msg) => \\{
      // A发送来的消息
      this.msg = msg;
    \\});
  \\}
\\};
</script>
```

```
created() \\{
    // 方式二
    this.$EventBus.$on('eventName', (param1,param2,...)=>\\{
        //需要执行的代码
        this.xxx(param1,param2,...)
    \\})
    // 方式三
    EventBus.$on('eventName', (param1,param2,...)=>\\{
        //需要执行的代码
        this.xxx(param1,param2,...)
    \\})
\\}
```

同理我们也可以在 B页面 向 A页面 发送消息。这里主要用到的两个方法：

```text
// 发送消息
EventBus.$emit(channel: string, callback(payload1,…))
// 监听接收消息
EventBus.$on(channel: string, callback(payload1,…))
```

#### 四、移除事件监听者

原因：

​    ① 为了避免在监听时，事件被反复触发

​    ② 由于[热更新](https://so.csdn.net/so/search?q=热更新&spm=1001.2101.3001.7020)，事件可能会被多次绑定监听，这时也需要移除事件监听

​    ③ 未及时移除的 eventBus 会导致内存泄漏

你也可以使用 `EventBus.$off('aMsg')` 来移除应用内所有对此某个事件的监听。

或者直接调用 `EventBus.$off()` 来移除所有事件频道，不需要添加任何参数 。

如果想移除事件的监听，可以像下面这样操作：

```text
// 方式一
import \\{ 
  eventBus 
\\} from './event-bus.js'
EventBus.$off('aMsg', \\{\\})
```

```
// 为了避免在监听时，事件被反复触发，通常需要在页面销毁时移除事件监听
beforeDestroy() \\{
    // 方式二
    this.$EventBus.$off('eventName');
    // 方式三
    EventBus.$off('eventName');
\\},
```







# 递归函数

> 在函数体内调用本函数叫递归函数

### 递归思想

> 递归是一种编程模式，在一个任务可以自然地拆分成多个相同类型但更简单的任务的情况下非常有用。
>
> 或者，在一个任务可以简化为一个简单的行为加上该任务的一个更简单的变体的时候可以使用。
>
> 或者，就像我们很快会看到的那样，处理某些数据结构。当一个函数解决一个任务时，在解决的过程中它可以调用很多其它函数。在部分情况下，函数会调用 **自身**。这就是所谓的 **递归**。

说的有点抽象，我们举个例子就比较清晰。比如我们要计算1到10的和，使用递归来来计算就特别的简单。

现在我们使用两种方法来实现这个例子：使用循环语句和使用递归。

使用for循环我们可以累加1至10的和：

```js
function add(n) \\{
    let result = 0;
    for(let i = 0; i <= n; i++)\\{
        result += i;
    \\}
    return result;
\\}
console.log(add(10));//55

//n是个自定义值，我们也可以利用这个函数计算其他数值

console.log(add(20));//210
```

下面我们使用递归来实现一下上面的功能：

```js
function adds(n) \\{
    if(n == 1)\\{
        return n;
    \\}
    return n+adds(n-1);
\\}

console.log(adds(10));//55
console.log(adds(20));//210
```

> 递归的原理是一个自上而下函数调用自己的执行过程，执行到一个自定义值就让这个函数递归执行。递归将函数调用简化为一个更简单的函数调用，然后再将其简化为一个更简单的函数，以此类推，直到结果变得显而易见。最重要的一点是，递归一定要设置一个跳出自调用的值，而且这个值是可控的，受制于JS引擎的影响，一般10000以内的递归都是可执行的。

> 正如上面的例子，循环和递归都可以计算和。实际上，任何递归函数都可以被重写为循环形式。有时这是在优化代码时需要做的。但对于大多数任务来说，递归方法足够快，并且容易编写和维护。

### 递归的应用场景

在我们实际学习工作中，递归算法一般用于解决三类问题：

- 问题的定义是按递归定义的（Fibonacci函数，阶乘，…）；
- 问题的解法是递归的（有些问题只能使用递归方法来解决，例如，汉诺塔问题，…）；
- 数据结构是递归的（链表、树等的操作，包括树的遍历，树的深度，…）。

### 

> 递归函数必须有一个终止条件，否则会造成堆栈溢出。

1.递归函数必须接受参数。（比如我要递归谁？）

2.在递归函数的定义初始，应该有一个判断条件，当参数满足这个条件的时候，函数停止执行，并返回值。（指定退出条件，否则就会死循环）

3.每次递归函数执行自己的时候，都需要把当前参数做某种修改，然后传入下一次递归。（每次循环在调用自己一次并传参）

4.当参数被累积修改到符合初始判断条件了，递归就停止了。（最后满足条件就退出）

简单的说**递归函数就是在函数体内调用n次本函数。**

```js
function ji(num)\\{
  if(num==1)\\{
    return num;
  \\}else \\{
    return num*ji(num-1);
  \\}
\\}
alert(ji(5))
// 执行步骤：5*（4*（3*（2*（1））））
```

### 递归校验所有名称是否为空

```
		isPassed: true, // 所有名称是否校验通过

		// 校验姓名
        verifyName(list) \\{
            console.log(list)
            for (let i = 0; i < list.length; i++) \\{
                console.log(list[i].name)
                if (list[i].name) \\{
                    if (list[i].child.length && this.isPassed) \\{
                        // 如果有子节点 且 还没找到为空的，递归判断子节点
                        this.verifyName(list[i].child)
                    \\}
                \\} else \\{
                    this.isPassed = false
                    // 找到为空的就跳出本次循环
                    break
                \\}
            \\}
        \\},
        // 保存
        async handleSave() \\{
            this.isPassed = true
            this.verifyName(this.organizationData)
            if (this.isPassed) \\{
            	// 保存接口
            	...
            \\} else \\{
                this.$Message.error(\\{
                    content: '名称不能为空',
                    duration: 2
                \\})
            \\}
        \\}
```

