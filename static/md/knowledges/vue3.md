---
title: vue3
date: 2024-03-08 21:02:08
categories: 
- 前端知识
tags:
- vue
---

## 一、Vue3 里 `script` 的三种写法

首先，Vue3 新增了一个叫做组合式 api 的东西，英文名叫 Composition API。因此 Vue3 的 `script` 现在支持三种写法，

### **1、最基本的 Vue2 写法**

```html
<template>
  <div>\\\{\\\{ count\\\}\\\} }}</div>
  <button @click="onClick">
    增加 1
  </button>
</template>

<script>
export default \\{
  data() \\{
    return \\{
      count: 1,
    \\};
  \\},
  methods: \\{
    onClick() \\{
      this.count += 1;
    \\},
  \\},
\\}
</script>
```

### **2、setup() 属性**

```xml
<template>
  <div>\\\{\\\{ count\\\}\\\} }}</div>
  <button @click="onClick">
    增加 1
  </button>
</template>

<script>
import \\{ ref \\} from 'vue';
export default \\{

  // 注意这部分
  setup() \\{
    let count = ref(1);
    const onClick = () => \\{
      count.value += 1;
    \\};
    return \\{
      count,
      onClick,
    \\};
  \\},
  
\\}
</script>
```

### 3、`script setup`

```xml
<template>
  <div>\\\{\\\{ count\\\}\\\} }}</div>
  <button @click="onClick">
    增加 1
  </button>
</template>

<script setup>
import \\{ ref \\} from 'vue';

const count = ref(1);
const onClick = () => \\{
  count.value += 1;
\\};
</script>
```

正如你看到的那样，无论是代码行数，还是代码的精简度，`script setup` 的方式是最简单的形式。

**如果你对 Vue 很熟悉，那么，我推荐你使用**`script setup`**的方式。**

这种写法，让 Vue3 成了我最喜欢的前端框架。

**如果你还是前端新人，那么，我推荐你先学习第一种写法。**

因为第一种写法的学习负担更小，先学第一种方式，掌握最基本的 Vue 用法，然后再根据我这篇文章，快速掌握 Vue3 里最需要关心的内容。

第一种写法，跟过去 Vue2 的写法是一样的，所以我们不过多介绍。

第二种写法，所有的对象和方法都需要 `return` 才能使用，太啰嗦。除了旧项目，可以用这种方式体验 Vue3 的新特性以外，我个人不建议了解这种方式。反正我自己暂时不打算精进这部分。

所以，接下来，我们主要介绍的，也就是`script setup` ，这种写法里需要了解的内容。

**注意：**`script setup`本质上是第二种写法的语法糖，掌握了这种写法，其实第二种写法也基本上就会了。（又多了一个不学第二种写法的理由）。



## 二、如何使用`script setup`编写组件

**学习 Vue3 并不代表你需要新学习一个技术，Vue3 的底层开发思想，跟 Vue2 是没有差别的。**

**V3 和 V2 的区别就像是，你用不同的语言或者方言说同一句话。**

所以我们需要关心的，就是 Vue2 里的内容，怎么用 Vue3 的方式写出来。

### 1、`data`——唯一需要注意的地方

整个 `data` 这一部分的内容，你只需要记住下面这一点。

**以前在** **`data`** **中创建的属性，现在全都用** **`ref()`** **声明。**

**在** **`template`** **中直接用，在** **`script`** **中记得加** **`.value`** **。**

在开头，我就已经写了一个简单的例子，我们直接拿过来做对比。

#### **1）写法对比**

```xml
 // Vue2 的写法

<template>
  <div>\\\{\\\{ count\\\}\\\} }}</div>
  <button @click="onClick">
    增加 1
  </button>
</template>

<script>
export default \\{
  data() \\{
    return \\{
      count: 1,
    \\};
  \\},
  methods: \\{
    onClick() \\{
      this.count += 1;
    \\},
  \\},
\\}
</script>
 // Vue3 的写法

<template>
  <div>\\\{\\\{ count\\\}\\\} }}</div>
  <button @click="onClick">
    增加 1
  </button>
</template>

<script setup>
import \\{ ref \\} from 'vue';

 // 用这种方式声明
const count = ref(1);

const onClick = () => \\{
   // 使用的时候记得 .value
  count.value += 1;
\\};
</script>
```

#### **2）注意事项——组合式** **api** **的心智负担**

##### **a、ref 和 reactive**

Vue3 里，还提供了一个叫做 `reactive` 的 `api`。

但是我的建议是，你不需要关心它。绝大多数场景下，`ref` 都够用了。

##### **b、什么时候用** **`ref()`** **包裹，什么时候不用。**

要不要用ref，就看你的这个变量的值改变了以后，页面要不要跟着变。

当然，你可以完全不需要关心这一点，跟过去写 `data` 一样就行。

只不过这样做，你在使用的时候，需要一直 `.value`。

##### **c、不要解构使用**

在使用时，不要像下面这样去写，会**丢失响应性。**

**也就是会出现更新了值，但是页面没有更新的情况**

```xml
// Vue3 的写法
<template>
  <div>\\\{\\\{ count\\\}\\\} }}</div>
  <button @click="onClick">
    增加 1
  </button>
</template>

<script setup>
import \\{ ref \\} from 'vue';

const count = ref(1);
const onClick = () => \\{
  // 不要这样写！！
  const \\{ value \\} = count;
  value += 1;
\\};
</script>
```

**注意：** 学习 Vue3 就需要考虑像这样的内容，徒增了学习成本。实际上这些心智负担，在学习的过程中，是可以完全不需要考虑的。

**这也是为什么我推荐新人先学习 Vue2 的写法。**



### 2、methods

声明事件方法，我们只需要在 `script` 标签里，创建一个方法对象即可。

剩下的在 Vue2 里是怎么写的，Vue3 是同样的写法。

```xml
// Vue2 的写法
<template>
  <div @click="onClick">
    这是一个div
  </div>
</template>

<script>
export default \\{
  methods: \\{
    onClick() \\{
      console.log('clicked')
    \\},
  \\},
\\}
</script>
// Vue3 的写法
<template>
  <div @click="onClick">
    这是一个div
  </div>
</template>

<script setup>

// 注意这部分
const onClick = () => \\{
  console.log('clicked')
\\}

</script>
```



### 3、props

声明 `props` 我们可以用 `defineProps()`，具体写法，我们看代码。

#### **1）写法对比**

```xml
// Vue2 的写法
<template>
  <div>\\\{\\\{ foo\\\}\\\} }}</div>
</template>

<script>
export default \\{
  props: \\{
    foo: String,
  \\},
  created() \\{
    console.log(this.foo);
  \\},
\\}
</script>
// Vue3 的写法
<template>
  <div>\\\{\\\{ foo\\\}\\\} }}</div>
</template>

<script setup>

// 注意这里
const props = defineProps(\\{
  foo: String
\\})

// 在 script 标签里使用
console.log(props.foo)
</script>
```

#### **2）注意事项——组合式** **api** **的心智负担**

使用 props 时，同样注意不要使用解构的方式。

```xml
<script setup>
const props = defineProps(\\{
  foo: String
\\})
// 或者
const props = defineProps(\\{
    info:\\{
        type:String,//接受的数据类型
        default:'默认参数',//接受默认数据
    \\},
    money:\\{
        type:Number,
        default:0
    \\}
\\})

 // 不要这样写
const \\{ foo \\} = props;
console.log(foo)
</script>
```



### 4、emits 事件

在 `  <script setup>  ` 中 声明 `emit` ，必须使用 `defineEmits` API，这是一个宏命令，不需要导入，直接可在 `  <script setup>  ` 使用且只能在 `  <script setup>  ` 中使用 

与 `props` 相同，声明 `emits` 我们可以用 `defineEmits()`，具体写法，我们看代码。

```xml
// Vue2 的写法
<template>
  <div @click="onClick">
    这是一个div
  </div>
</template>

<script>
export default \\{

  emits: ['click'], // 注意这里
  methods: \\{
    onClick() \\{
      this.$emit('click'); // 注意这里
    \\},
  \\},
 
\\}
</script>
// Vue3 的写法
<template>
  <div @click="onClick">
    这是一个div
  </div>
</template>

<script setup>

// 注意这里
const emit = defineEmits(['click']);

const onClick = () => \\{
  emit('click') // 注意这里
\\}

</script>
```

1. 运行时声明

```ts
ts复制代码// 父组件
<Info @parentClick="parentClick" @parentChang="parentChang"></Info>

<script setup>
    // 这样是没有任何的类型检查的 不管是什么值都可以传递过来
    const parentClick = (data: number) => \\{ alert('子组件触发了此事件,传递的值是' + data) \\}
    const parentChang = () => \\{ alert('子组件触发了此事件') \\}
</script>

// 子组件
<button @click="handClick">点击触发handClick事件</button>
<input type="checkbox" @change="handChang">

<script setup>
    const emits = defineEmits(['parentClick','parentChang']) // 语法糖
    
    const handClick = () => \\{
        emits('parentClick',2) // 使用方式和 vue2 this.$emit 一样
    \\}
    const handChang = () => \\{
        emits('parentChang') // 使用方式和 vue2 this.$emit 一样
    \\}
</script>
```

2 . 类型声明式

```ts
ts复制代码   // 子组件
   <script setup>
    const emits = defineEmits<\\{
        (e: 'parentClick', data: number): void // 函数类型 当传递的值的类型不是number时会报错
        (e: 'parentChang'): void // 函数类型
    \\}>();
    
    const handClick = () => \\{
        emits('parentClick',2) // 使用方式和 vue2 this.$emit 一样
    \\}
    const handChang = () => \\{
        emits('parentChang') // 使用方式和 vue2 this.$emit 一样
    \\}
</script>
```

运行时声明和类型声明式同样不可同时使用



### 5、computed

直接上写法对比。

```xml
// Vue2 的写法
<template>
  <div>
    <span>\\\{\\\{ value\\\}\\\} }}</span>
    <span>\\\{\\\{ reversedValue\\\}\\\} }}</span>
  </div>
</template>

<script>
export default \\{
  data() \\{
    return \\{
      value: 'this is a value',
    \\};
  \\},
  computed: \\{
    reversedValue() \\{
      return value
        .split('').reverse().join('');
    \\},
  \\},
\\}
</script>
// Vue3 的写法
<template>
  <div>
    <span>\\\{\\\{ value\\\}\\\} }}</span>
    <span>\\\{\\\{ reversedValue\\\}\\\} }}</span>
  </div>
</template>

<script setup>
import \\{ref, computed\\} from 'vue'
const value = ref('this is a value')

// 注意这里
const reversedValue = computed(() => \\{
  // 使用 ref 需要 .value
  return value.value
    .split('').reverse().join('');
\\})

</script>
```



### 6、watch

这一部分，我们需要注意一下了，Vue3 中，watch 有两种写法。一种是直接使用 `watch`，还有一种是使用 `watchEffect`。

两种写法的区别是：

- `watch` 需要你明确指定依赖的变量，才能做到监听效果。
- 而 `watchEffect` 会根据你使用的变量，自动的实现监听效果。

#### 1）直接使用 `watch`

```xml
// Vue2 的写法
<template>
  <div>\\\{\\\{ count\\\}\\\} }}</div>
  <div>\\\{\\\{ anotherCount\\\}\\\} }}</div>
  <button @click="onClick">
    增加 1
  </button>
</template>

<script>
export default \\{
  data() \\{
    return \\{  
      count: 1,
      anotherCount: 0,
    \\};
  \\},
  methods: \\{
    onClick() \\{
      this.count += 1;
    \\},
  \\},
  watch: \\{
    count(newValue) \\{
      this.anotherCount = newValue - 1;
    \\},
  \\},
\\}
</script>

// Vue3 的写法
<template>
  <div>\\\{\\\{ count\\\}\\\} }}</div>
  <div>\\\{\\\{ anotherCount\\\}\\\} }}</div>
  <button @click="onClick">
    增加 1
  </button>
</template>

<script setup>
import \\{ ref, watch \\} from 'vue';

const count = ref(1);
const onClick = () => \\{
  count.value += 1;
\\};

const anotherCount = ref(0);

// 注意这里
// 需要在这里，明确指定依赖的是 count 这个变量
watch(count, (newValue) => \\{
  anotherCount.value = newValue - 1;
\\})

</script>
```

##### vue3中watch子组件中的props

子组件监听父组件传入的值

```
const props = defineProps(\\{
  contentId: \\{
    type: String || Number, 
    required: true,
  \\},
\\});
 
// 整体监听
watch(props,(newValue, oldValue)=>\\{
  // 
\\})
 
// 监听contentId
watch(
	()=>props.contentId,
	(newVal, oldVal)=>\\{
    	console.log(newVal, oldVal)
	\\},
	\\{ immediate: true \\}
)
// 监听contentlist的变化
watch(
  () => props.contentlist,
  (newVal, oldVal) => \\{
    console.log('contentlist', newVal)
    if (props.listMode === 'horizontal') \\{
      listData.value = props.contentlist
    \\}
  \\},
  \\{ immediate: true, deep: true \\}
)

// 还可以使用watchEffect监听
watchEffect(()=>\\{
    let id=props.contentId
   //
\\})
```



#### 2）使用 `watchEffect`

```xml
// Vue2 的写法
<template>
  <div>\\\{\\\{ count\\\}\\\} }}</div>
  <div>\\\{\\\{ anotherCount\\\}\\\} }}</div>
  <button @click="onClick">
    增加 1
  </button>
</template>

<script>
export default \\{
  data() \\{
    return \\{  
      count: 1,
      anotherCount: 0,
    \\};
  \\},
  methods: \\{
    onClick() \\{
      this.count += 1;
    \\},
  \\},
  watch: \\{
    count(newValue) \\{
      this.anotherCount = newValue - 1;
    \\},
  \\},
\\}
</script>
// Vue3 的写法
<template>
  <div>\\\{\\\{ count\\\}\\\} }}</div>
  <div>\\\{\\\{ anotherCount\\\}\\\} }}</div>
  <button @click="onClick">
    增加 1
  </button>
</template>

<script setup>
import \\{ ref, watchEffect \\} from 'vue';

const count = ref(1);
const onClick = () => \\{
  count.value += 1;
\\};

const anotherCount = ref(0);

// 注意这里
watchEffect(() => \\{
  // 会自动根据 count.value 的变化，
  // 触发下面的操作
  anotherCount.value = count.value - 1;
\\})

</script>
```



### 7、生命周期

Vue3 里，除了将两个 `destroy` 相关的钩子，改成了 `unmount`，剩下的需要注意的，就是在 `script` 中，不能使用 `beforeCreate` 和 `created` 两个钩子。

如果你熟悉相关的生命周期，只需要记得在 `setup` 里，用 `on` 开头，加上大写首字母就行。

```xml
// 选项式 api 写法
<template>
  <div></div>
</template>

<script>
export default \\{
  beforeCreate() \\{\\},
  created() \\{\\},
  
  beforeMount() \\{\\},
  mounted() \\{\\},
  
  beforeUpdate() \\{\\},
  updated() \\{\\},
  
  // Vue2 里叫 beforeDestroy
  beforeUnmount() \\{\\},
  // Vue2 里叫 destroyed
  unmounted() \\{\\},
  
  // 其他钩子不常用，所以不列了。
\\}
</script>

// 组合式 api 写法
<template>
  <div></div>
</template>

<script setup>
import \\{
  onBeforeMount,
  onMounted,

  onBeforeUpdate,
  onUpdated,

  onBeforeUnmount,
  onUnmounted,
\\} from 'vue'

onBeforeMount(() => \\{
	console.log('DOM即将挂载')
\\})
onMounted(() => \\{
	console.log('DOM挂载完毕')
\\})

onBeforeUpdate(() => \\{
    console.log('DOM即将更新')
\\})
onUpdated(() => \\{
    console.log('DOM更新完毕')
\\})

onBeforeUnmount(() => \\{
    console.log('即将销毁')
\\})
onUnmounted(() => \\{
    console.log('销毁完毕')
\\})

// 组件被缓存后，重新激活
onActivated(() => \\{
  console.log('onActivated')
\\})
// 失去激活状态
onDeactivated(() => \\{
  console.log('onDeactivated')
\\})
</script>
```

如果你的 setup() 包含异步操作，确保所有生命周期钩子都在await之前定义。



## 三、结语

好了，对于快速上手 Vue3 来说，以上内容基本已经足够了。

如果觉得这篇文章不错，有帮你节省时间的话，还想听我说哪些内容，欢迎评论区里告诉我。

这篇文章本身不能做到帮你理解所有 Vue3 的内容，但是能帮你快速掌握 Vue3 的写法。

如果想做到对 Vue3 的整个内容心里有数，还需要你自己多看看 Vue3 的官方文档。

原文链接：https://juejin.cn/post/7225267685763907621







# vue3快速查阅📒

**Vue 3 相对于 Vue 2 有许多改进和新功能，其中一些主要的变化包括：**

1. `使用 Composition API`：Vue 3 引入了 Composition API，这是一种新的、更灵活的组件编写方式，允许更好地组织和复用代码。
2. `改进的性能`：Vue 3 在性能方面进行了许多改进，包括更快的渲染速度、更小的捆绑体积和更好的内存管理。
3. `更好的 TypeScript 支持`：Vue 3 提供了更好的 TypeScript 支持，包括类型推断和类型注解。
4. `新的路由器和状态管理库`：Vue 3 引入了新的路由器和状态管理库，称为 Vue Router 和 Vuex 4。
5. `更好的 tree-shaking 支持`：Vue 3 更好地支持 tree-shaking，这意味着在生产环境中，只打包实际使用的代码，从而减少应用程序的大小。

### setup

在 Vue 3 中，`setup` 是一个新的组件选项，用于定义组件的逻辑和状态。通过使用 setup，可以更清晰地组织组件的逻辑和状态，并使其更易于测试和维护。`也可以直接把setup写在script标签上哦`。

```html
<template>
  <div>
    \\\{\\\{ count\\\}\\\} }}
  </div>
</template>

<script>
export default \\{
  name: 'MyComponent',
  setup() \\{
    const count = ref(0);
    const increment = () => \\{
      count.value++;
    \\};

    return \\{
      count,
      increment
    \\};
  \\}
\\};
</script>
```

### 响应式数据

使用`reactive`创建对象类型响应式数据，如果给reactive重新分配一个对象，会失去响应式，可以使用`Object.assign()`去整体替换。使用ref创建基本类型响应数据

> ref也可以创建对象类型的响应数据。若层级较深，建议reactive

```html
<script setup>
  import \\{ reactive , ref \\} from 'vue';
  let obj=reactive(\\{
    a:1,
    b:\\{
      c:3
      d:4
    \\}
  \\})
  let str=ref('hi')
  const fnc=()=>\\{
    str.value = 'hello!'//记得加.value
  \\}
</script>
```

### 解构响应式对象

`toRefs`可用来解构，该对象的每个属性都是独立的 ref 对象，并保持响应式

```js
import \\{ reactive, toRefs \\} from 'vue';
let info = reactive(\\{
  name: 'Echo',
  age: 26,
  gender: 'Male',
\\})

let \\{ name, age, gender \\} = toRefs(info);//解构数据，并保持响应式
```

### 如何监听多个数据？

监听多个数据，第一个参数需用数组包起来；如果监听非对象类型，需写成函数形式，若监听 reactive 定义的对象类型，就默认开启深度监听。

开启immediate ：上来就调用监听里的内容，类似react中的useEffect(()=>\\{\\},[])

```js
import \\{ watch \\} from 'vue';
//监听active、type
watch([() => props.active, ()=> props.type],(nv, ov) => \\{
  // nv代表最新数据，ov是老数据
  console.log(nv)
  //开启deep代表深度监听
\\},\\{ deep:true, immediate: true \\})
```

### 解放双手，自动检测变化

`watchEffect`可以自动检测到属性的变化，无需手动指定要监听的属性。

与传统的 watch 不同，watchEffect 会在属性变化时自动执行副作用函数，并且可以返回一个清理函数，用于在组件卸载时清理副作用。

```js
import \\{ watchEffect \\} from 'vue';

//只要temp.val跟json.val发生变更，就会自动执行watchEffect内的副作用函数
watchEffect(()=>\\{
  if(temp.val>60||json.val>60)\\{
    console.log('发送请求')
  \\}
\\})
```

### 接收props

父子组件传值，需要使用`defineProps`接收props，案例如下：

```html
<script setup>
  import \\{ defineProps \\} from 'vue';
  //子组件接收props
  const props = defineProps(\\{
    language: \\{
      type: Object,
      //也可以使用withDefaults设置默认值
      default: () => (\\{\\}),
    \\},
    cookieCountry: \\{
      type: String,
      default: ''
    \\}
  \\})
</script>
```

### Ref属性（父子交互）

通过 `Ref 属性`，可以从父组件中访问子组件的属性和方法，或者直接操作 DOM 元素。

```html
<template>
  <div ref="myDiv">Hello, World!</div>
</template>

<script>
import \\{ ref, onMounted \\} from 'vue';

export default \\{
  setup() \\{
    const myDiv = ref(null);
		//mounted是生命周期，代表挂载完毕
    onMounted(() => \\{
      myDiv.value.style.color = 'red';//将myDiv的颜色改成红色
    \\});

    return \\{
      myDiv
    \\};
  \\}
\\};
</script>
```

> 如果父组件想访问子组件的内容，子组件需使用defineExpose将内容导出。

defineExpose将组件中的属性或方法暴露给外部环境，以便在其他组件或模板中使用。

```html
<template>
   <card-num 
    ref="cardNumRef"
   />
</template>

<script setup>
  import \\{ ref \\} from 'vue';
  const resetAllRefData = () => \\{
    console.log(cardNumRef.value.cardNo)//获取子组件中的cardNo值
  \\}
</script>
```

cardNum组件：

```html
<script setup>
  import \\{ defineExpose \\} from 'vue';
  const resetData = () => \\{
    cardNo.value = ''
    cardNum.value = ''
  \\}
  //暴露
  defineExpose(\\{
    resetData
  \\})
</script>
```

### 自定义事件

`defineEmits` 是 Vue 3 中的一个新特性，它允许你在组件中自定义事件。在父组件中，可以使用 v-on 指令来监听自定义事件。

```html
<template>
  <!-- 自定义一个叫update的事件 -->
  <Child @update="onUpdate"/>
</template>

<script setup>
  import Child from '/Child.vue'
  
  const onUpdate = (value)=>\\{
    console.log(value)//666
  \\}
</script>
```

Child组件：

```html
<template>
  <!-- 点击button，将666传给父，emits 触发事件 -->
  <button @click="emits('update',666)"/>
</template>

<script setup>
  import \\{ defineEmits,onMounted \\} from 'vue'
  
  // 定义 emits
  const emits = defineEmits(['update'])//接收事件名update
</script>
```

### vue3 生命周期

```html
<script setup>
  import \\{ onMounted,onBeforeMount,onUpdated,unmounted \\} from 'vue';
  //挂载前
  onBeforeMount(()=>\\{\\})
  //挂载完毕
  onMounted(()=>\\{\\})
  //更新完毕
  onUpdated(()=>\\{\\})
  //卸载完毕
  onUnmounted(()=>\\{\\})
</script>
```

`beforeCreate`: 在实例初始化之后。

`created`: 在实例创建完成后被立即调用。

`beforeUpdate`: 数据更新时。

`beforeUnmount`: 实例销毁之前。

以此类推...

### 作用域插槽

作用域插槽，它允许你在一个组件中定义具有局部作用域的插槽。通过作用域插槽，可以将组件的属性传递给插槽内容，从而使插槽内容能够根据组件的状态进行动态渲染。
 作用域插槽使用 `v-slot` 指令来定义，它可以接受一个参数，该参数指定了要传递给插槽的属性名。
 下面是具名插槽+作用域插槽的例子：

> 如果不写名字就是默认插槽

```html
 <!-- <template #ScopedSlot="\\{list\\}"></template> -->
<template>
  <SlotComponent>
    <!-- ScopedSlot是插槽名，params子组件传的是参数 -->
    <template v-slot:ScopedSlot='params'>
      <ul>
        <li v-for='d in params.list' :key="d.id">
        \\\{\\\{d.nam\\\}\\\}e}}
        </li>
      </ul>
    </template>
  </SlotComponent>
</template>

<script>
import SlotComponent from './SlotComponent.vue';

export default \\{
  components: \\{
    SlotComponent,
  \\},
\\};
</script>
```

子组件SlotComponent：

```html
<template>
  <div>
    <slot name="ScopedSlot" :list="list" />
  </div>
</template>

<script setup>
	import \\{reactive\\} from 'vue'
  let list=reactive([
    \\{id:'001',name:'test-01'\\},
    \\{id:'002',name:'test-02'\\}
  ])
</script>
```

### 提高性能-浅层次响应

`shallowRef()`与`ref()`类似，但它不支持深度响应性，是浅层次响应。

对嵌套对象的属性或数组元素的修改不会触发响应性。这在需要优化性能并避免不必要的深度响应性跟踪时非常有用。这样使用浅的响应式提高性能，只有最外一层是响应式。

> shallowReactive同理

### 响应式对象-》原始对象

`toRaw()` 是用于将响应式对象转换为原始对象。以便在需要时进行操作。转换后的对象不再具有响应性，对其进行的更改不会触发 Vue 的更新机制。

```js
import \\{ reactive, toRaw \\} from 'vue';

const obj = reactive(\\{ name: 'John', age: 24 \\});

const rawObj = toRaw(obj);

console.log(rawObj); 
// 输出：\\{ name: 'John', age: 24 \\}

rawObj.name = 'Alice';

console.log(obj.name); 
// 输出：'John'
```

### 创建自定义的ref

`customRef` 是 Vue 3 中引入的一个新特性，用于创建自定义的ref，让用户来决定什么时候收集和执行依赖，从而更好地控制行为和逻辑。customRef 接受 track 和 trigger 两个函数作为参数，并返回一个带有 get 和 set 方法的对象。

track用于追踪数据，trigger 用于触发响应，更新视图。一般 track 方法放在 get 中，trigger 方法放在 set 中。

```js
import \\{ customRef \\} from 'vue';

const myCustomRef = customRef((track, trigger) => \\{
  // 在这里编写自定义的逻辑
  return\\{
    get()\\{
      track()//跟踪
    \\},
    set(value)\\{
      trigger()//触发
    \\}
  \\}
\\});

// 在组件中使用自定义的 ref
const myComponent = \\{
  template: `<div ref="myCustomRef"></div>`,
  setup() \\{
    const myCustomRef = myCustomRef();

    console.log(myCustomRef.value); 
    // 获取当前的引用值
  \\}
\\};
```

### 获取未在 props 中声明的属性

`$attrs` 可以用于获取父组件传递的属性值，或者在组件内部未在 props 中声明的属性。

注意：$attrs 中的属性是只读的，不能直接修改。如果需要在组件内部处理未在 props 中声明的属性，可以使用 v-bind 指令或动态组件来实现。

```html
<!-- 传值给子组件 -->
<child-component :id="id" :style="style" some-other-attribute="value"></child-component>
export default \\{
  props: ['id', 'style'],//props只接收了id跟style
  created() \\{
    console.log(this.$attrs); //$attrs能实现全部获取
    // 输出：\\{ id: "id", style: "style", someOtherAttribute: "value" \\}
  \\}
\\};
```



### 组件间通信

$parent和refs 是用于组件间通信和访问的属性。需要配合`defineExpose`一起使用

- refs 可以用于在模板中访问子组件或 DOM 元素。在模板中的元素或组件上使用 ref 属性来定义一个引用名称，然后在组件的 JavaScript 代码中通过 `$refs` 访问到这个元素或组件。
- parent 指向当前组件的父组件实例。通过 `$parent`，可以访问父组件的属性、方法和事件等。

父组件 $refs示例代码：

```html
<template>
  <div>
    <button @click="myButton($refs)">点击我</button>
    <!-- 子组件 -->
    <ChildComponent1 />
    <ChildComponent2 />
  </div>
</template>

<script setup>
  import ChildComponent1 from '/ChildComponent1.vue'
  import ChildComponent2 from '/ChildComponent2.vue'
  import \\{ ref,defineExpose \\} from 'vue';
  
  let value=ref('666')
	function myButton(refs)\\{
    // refs是子组件的集合
    for(let key in refs)\\{
      refs[key].val=+1//操作每个子组件的val+1
    \\}
  \\}
  defineExpose(\\{value\\})
</script>
```

子组件 $parent示例代码：

```html
<template>
  <div>
    <button @click="parentMethod($parent)">点击我</button>
  </div>
</template>

<script>
  import \\{ ref \\} from 'vue';
  let value=ref('888')
  function myButton(parent)\\{
    parent.value-=1//子操作父的value
  \\}
  defineExpose(\\{value\\})
</script>
```



### 隔代通信

`provide` 是一个用于提供依赖注入的选项。可用于隔代通信；它允许父组件向其后代组件提供共享的数据或功能。在子组件中可以通过 inject 选项来接收父组件提供的属性。

```html
<template>
  <div>
    <Child />
  </div>
</template>

<script setup>
  import Child from './Child.vue';
  import \\{ ref,provide \\} from 'vue';
  
  let value=ref(\\{
    name:'sam',
    age:18
  \\})
  //provide向后代提供数据
  provide('val',value)
</script>
```

子组件Child：

```html
<template>
  <div>
    <!-- sam -->
    姓名:\\\{\\\{data.nam\\\}\\\}e}}
    <!-- 18 -->
    年龄:\\\{\\\{data.ag\\\}\\\}e}}
  </div>
</template>

<script setup>
  import \\{ inject \\} from 'vue';
  //inject接收数据
  let data=inject('val',\\{//第二个参数是默认值
    name:'未知',
    age:0
  \\})
</script>
```

原文链接：https://juejin.cn/post/7332435905925890098



### vue3祖孙组件通信举例

在Vue 3中，如果想要孙组件触发祖先组件的事件，可以结合使用`provide`/`inject`和一个事件总线（Event Bus）或者通过祖先组件提供的回调函数来实现。这里我们主要介绍使用祖先组件提供的回调函数的方法，因为它更为直接且易于理解。

#### 方法：使用祖先组件提供的回调函数

这种方法涉及到祖先组件提供一个方法（通常是更新状态或执行特定操作的方法），然后通过`provide`将其暴露给子孙组件。子孙组件则可以通过`inject`获取这个方法，并在适当的时候调用它以触发祖先组件中的逻辑。

##### 祖先组件 (GrandParent.vue)

```vue
<template>
  <div>
    <h1>我是爷爷组件</h1>
    <p>共享数据：\\\{\\\{ sharedData\\\}\\\} }}</p>
    <!-- 父组件 -->
    <Parent />
  </div>
</template>

<script>
import \\{ provide, ref \\} from 'vue';
import Parent from './Parent.vue';

export default \\{
  components: \\{
    Parent
  \\},
  setup() \\{
    const sharedData = ref('初始共享数据');

    // 定义一个方法，供后代组件调用
    const updateSharedData = (newData) => \\{
      sharedData.value = newData;
    \\};

    // 使用provide将sharedData和updateSharedData暴露给后代组件
    provide('sharedInfo', \\{
      sharedData,
      updateSharedData
    \\});

    return \\{
      sharedData
    \\}
  \\}
\\}
</script>
```

##### 子组件 (Child.vue)

```vue
<template>
  <div>
    <h3>我是孙子组件</h3>
    <button @click="handleClick">点击我来更新爷爷组件的数据</button>
  </div>
</template>

<script>
import \\{ inject \\} from 'vue';

export default \\{
  setup() \\{
    const sharedInfo = inject('sharedInfo');

    const handleClick = () => \\{
      if(sharedInfo.updateSharedData)\\{
        sharedInfo.updateSharedData('孙子组件更新了这条信息');
      \\}
    \\};

    return \\{
      handleClick
    \\}
  \\}
\\}
</script>
```

在这个例子中，祖父组件不仅提供了共享的数据，还提供了一个用于更新这些数据的方法`updateSharedData`。孙子组件通过`inject`获取到这个方法，并在按钮被点击时调用它，从而实现了从孙组件触发祖先组件的行为的目的。这种方式非常灵活，可以根据需要传递任何类型的回调函数或数据。



### vue3中provide/inject传参，使用组合式和函数式两种写法举例

在 Vue 3 中，`provide` 和 `inject` 提供了一种机制，使得祖先组件可以向其所有子孙组件传递数据。下面分别使用组合式 API（Composition API）和选项式 API（Options API）来展示如何使用 `provide` 和 `inject` 进行参数传递。

#### 使用组合式 API (Composition API)

**提供数据（父组件）：**

```javascript
<template>
  <div>
    <child-component></child-component>
  </div>
</template>

<script>
import \\{ provide, ref \\} from 'vue';
import ChildComponent from './ChildComponent.vue';

export default \\{
  components: \\{ ChildComponent \\},
  setup() \\{
    const message = ref('Hello from Parent');
    provide('message', message);
  \\}
\\}
</script>
```

**注入数据（子组件）：**

```javascript
<template>
  <div>\\\{\\\{ injectedMessage\\\}\\\} }}</div>
</template>

<script>
import \\{ inject \\} from 'vue';

export default \\{
  setup() \\{
    const injectedMessage = inject('message');
    return \\{ injectedMessage \\};
  \\}
\\}
</script>
```

#### 使用选项式 API (Options API)

**提供数据（父组件）：**

```javascript
<template>
  <div>
    <child-component></child-component>
  </div>
</template>

<script>
export default \\{
  data() \\{
    return \\{
      message: 'Hello from Parent'
    \\}
  \\},
  provide() \\{
    return \\{
      message: this.message
    \\}
  \\}
\\}
</script>
```

**注入数据（子组件）：**

```javascript
<template>
  <div>\\\{\\\{ message\\\}\\\} }}</div>
</template>

<script>
export default \\{
  inject: ['message']
\\}
</script>
```

请注意，虽然这里没有直接提及“函数式写法”，但Vue确实支持函数式组件，并且可以与`provide`/`inject`一起使用。然而，在Vue 3中，由于引入了Teleport、Suspense等新特性以及对组合式API的强化，通常推荐使用组合式API进行更灵活的数据处理和逻辑复用。对于函数式组件来说，它们更多地关注于渲染性能优化，而`provide`和`inject`主要用于跨层级组件间的状态管理。因此，在函数式组件中应用`provide`/`inject`并不常见，通常还是采用上述两种方式之一。



### vue3孙组件如何触发祖先组件的事件，祖孙组件通信举例

在 Vue3 中，实现祖孙组件通信主要有以下几种方式，以下给出两种常用方案的示例：

---

#### 方案 1：使用 `provide` + `inject` + 函数传递
通过祖先组件提供方法，后代组件注入调用

```vue
<!-- 祖先组件 Grandparent.vue -->
<script setup>
import \\{ provide \\} from 'vue'

// 提供一个方法给后代组件使用（放在后面会报错）
const handleGrandchildEvent = (message) => \\{
  console.log('收到来自孙组件的信息:', message)
\\}
provide('grandparentMethod', handleGrandchildEvent)
    

const message = ref('等待孙组件更新...');
// 提供一个方法给后代组件使用（放在后面会报错）
provide('updateMessage', (newMessage) => \\{
	message.value = newMessage;
\\});
</script>

<template>
  <ParentComponent />
</template>
```

```html
<!-- 中间父组件 Parent.vue -->
<template>
  <ChildComponent />
</template>
```

```html
<!-- 孙组件 Child.vue -->
<script setup>
import \\{ inject \\} from 'vue'

// 注入祖先提供的方法
const triggerGrandparent = inject('grandparentMethod')
const sendMessage = () => \\{
  triggerGrandparent('Hello 祖先!') // 触发祖先方法
\\}

// 注入祖先组件提供的方法
const updateMessage = inject('updateMessage');
const updateAncestorMessage = () => \\{
	updateMessage('这是由孙组件更新的消息！');
\\};
</script>

<template>
  <button @click="sendMessage">触发祖先事件</button>
</template>
```

---

#### 方案 2：使用事件链 + `$attrs`
通过逐层传递事件实现（需要中间组件配合透传）

```html
<!-- 祖先组件 Grandparent.vue -->
<template>
  <Parent @custom-event="handleEvent" />
</template>

<script setup>
const handleEvent = (msg) => \\{
  console.log('收到事件:', msg)
\\}
</script>
```

```html
<!-- 中间父组件 Parent.vue -->
<template>
  <!-- 透传所有事件 -->
  <Child v-bind="$attrs" />
</template>
```

```html
<!-- 孙组件 Child.vue -->
<script setup>
const emit = defineEmits(['custom-event'])

const trigger = () => \\{
  emit('custom-event', '来自孙组件的数据')
\\}
</script>

<template>
  <button @click="trigger">触发事件</button>
</template>
```

---

#### 方案对比：
| 方案                     | 优点                             | 缺点                                        |
| ------------------------ | -------------------------------- | ------------------------------------------- |
| provide/inject           | 跨层级直接访问，中间组件无需参与 | 组件层级关系不直观                          |
| 事件链透传               | 符合标准事件流，适合简单层级     | 需要中间组件手动透传，层级深时较繁琐        |
| 全局状态管理（如 Pinia） | 适合大型应用，解耦组件           | 需要引入额外库，小型项目可能过度设计        |
| 事件总线（如 mitt）      | 完全解耦组件                     | 需要手动管理事件监听/移除，Vue3不再内置支持 |

---

**推荐使用 `provide/inject`** 方案，这是 Vue3 官方推荐的跨层级通信方式，能直接实现祖孙间逻辑交互，代码也更清晰。



### 为什么报错injection "updateDetail" not found. 

```
祖先组件
// 提供一个方法给后代组件使用
provide('updateDetail', (id) => \\{
  params.id = id
  getContentDetail()
\\})

孙组件
// 注入祖先组件提供的方法
const updateDetail = inject('updateDetail')
// 跳转详情页面
const goDetail = (item) => \\{
  if (props.source === 'collect' && !item.isOnShelves) \\{
    // 收藏列表 已下架
    showToast('素材已下架')
    return
  \\}
  if (props.source === 'detail') \\{
    updateDetail(item.id)
  \\} else \\{
    goPage('Detail', \\{ id: item.id \\})
  \\}
\\}
```

报错 `"updateDetail" not found` 通常意味着在尝试使用 `inject` 函数获取名为 `updateDetail` 的依赖项时，Vue 无法找到该依赖项。这种情况可能由几个原因引起：

1. **祖先组件未正确提供依赖**：确保祖先组件确实通过 `provide` 方法提供了 `updateDetail`。这意味着 `provide` 应该被放置在一个能覆盖到孙组件的父组件内部。如果孙组件和提供者之间有多个层级，而其中任何一个中间组件没有正确传递下来，也会导致这个问题。

2. **注入发生在提供之前**：确保孙组件的 `inject` 调用是在对应的祖先组件已经挂载并且调用了 `provide` 提供了 `updateDetail` 方法之后发生的。Vue 的依赖注入是基于组件树的，因此需要确保顺序正确。

3. **命名错误或拼写错误**：检查 `provide` 和 `inject` 中使用的字符串 `'updateDetail'` 是否完全一致，包括大小写等细节。任何不匹配都会导致 Vue 无法找到相应的注入。

4. **使用 Vue 版本问题**：如果你正在使用的是 Vue 2，确保你使用的是正确的语法和方法。对于 Vue 3，依赖注入机制有所改进，但同样需要注意上述几点。确保你的 Vue 版本与你使用的 API 兼容。

5. **组件异步加载问题**：如果你的应用中涉及到异步组件或者动态导入，确保这些不会影响到依赖项的提供和注入。例如，如果孙组件在祖先组件准备好提供 `updateDetail` 之前就已经尝试注入它，那么这也会导致错误。

解决步骤可以包括：

- 确认祖先组件中的 `provide` 方法是否正确无误，并且在孙组件试图 `inject` 之前已经被执行。
- 检查整个组件树，确保从祖先组件到孙组件之间没有中断依赖链的地方。
- 查看是否有任何拼写错误或大小写不匹配的情况。
- 如果可能的话，尝试简化你的组件结构，以隔离问题所在，确认是否是由于组件层次结构复杂性导致的问题。

根据你提供的代码片段，看起来逻辑上是正确的，因此你需要仔细检查上述提到的可能原因。



### 某些祖先组件不需要这个updateDetail，怎么避免报错

如果你有一些祖先组件不需要提供 `updateDetail` 方法，但你仍然希望孙组件能够安全地尝试注入并使用它而不报错，有几种方法可以解决这个问题：

#### 1. 默认值
在调用 `inject` 的时候，你可以提供一个默认值。如果祖先组件没有提供相应的依赖项，那么就会使用这个默认值。这对于避免因缺少依赖项而导致的错误非常有用。

```javascript
const updateDetail = inject('updateDetail', (id) => \\{
  // 默认实现或空实现
  console.log("updateDetail not provided, using default behavior.");
\\});
```

这样，即使某些祖先组件没有提供 `updateDetail`，你的孙组件也不会因为找不到注入而报错，并且可以根据需要定义默认行为。

#### 2. 条件性注入检查
另一种方法是在使用 `updateDetail` 前检查其是否存在，以避免直接调用未定义的方法导致的错误。

```javascript
const goDetail = (item) => \\{
  if (props.source === 'collect' && !item.isOnShelves) \\{
    showToast('素材已下架');
    return;
  \\}
  if (props.source === 'detail') \\{
    if(typeof updateDetail === 'function') \\{
      updateDetail(item.id);
    \\} else \\{
      console.warn('updateDetail function is not available.');
      // 可选：在这里处理updateDetail不可用的情况
    \\}
  \\} else \\{
    goPage('Detail', \\{ id: item.id \\});
  \\}
\\}
```

#### 3. 使用 Symbol 或唯一字符串作为键
确保你在 `provide` 和 `inject` 中使用的键是唯一的（例如通过使用 Symbol），以避免命名冲突和意外覆盖。这虽然不能直接解决缺少提供者的问题，但有助于保持代码清晰和减少错误的可能性。

#### 总结
最简单直接的方法是为 `inject` 提供一个默认值，这样即使某些祖先组件没有提供 `updateDetail`，你的应用也不会崩溃，并且可以在这些情况下执行一些默认行为或者显示警告信息。这种方法提高了代码的健壮性和灵活性，使得组件间的依赖更加松散耦合。







# 知识点

### vue3项目中通过globalProperties定义与使用全局数据

vue3项目中有一个全局的字典文件dic.js，里面定义的都是一些公共字段映射值，如： 

```
dic.js
export default \\{
	typeMap:\\{
		1:'自动',
		2:'手动'
	\\},
	...
\\}
```

**main.js中：**

1. 首先引入这个文件
2. 通过createApp()创建组件实例app
3. 将dic暴露出来的数据对象挂载到 app.config.globalProperties 的一个$dic 属性上

```
main.js

import \\{ createApp \\} from 'vue'
import dic from './dicFolder/dic.js'

const app = createApp(App)
app.config.globalProperties.$dic = dic
```

在需要使用 dic 中的字典数据的vue文件中：

1. 引入 getCurrentInstance
2. 调用 getCurrentInstance，并从结果中解析出proxy（必须用proxy），再从proxy解析到自己定义的 $dic ，这样就可以在js中或模板中直接使用dic里面定义的数据了

```
test.vue

import \\{ getCurrentInstance \\} from 'vue'
const \\{ proxy: \\{ $dic \\} \\} = getCurrentInstance()

console.log($dic.typeMap)
```



### vue3定义函数的方法有几种？有什么利弊 

在Vue 3中，有三种常见的定义函数的方法：普通函数、箭头函数和组件方法。每种方法都有自己的特点和用途。

#### 普通函数：

- 定义方式：使用普通的function关键字来定义函数，例如：

  ```javascript
  function myFunction() \\{
    // 函数体
  \\}
  ```

- 利与弊：

  - 优点：函数体内的this指向调用该函数的对象，可以正常使用this关键字来引用当前对象。
  - 缺点：会创建一个新的函数实例，可能会带来一些性能上的开销。

#### 箭头函数：

- 定义方式：使用箭头函数的语法来定义函数，例如：

  ```javascript
  const myFunction = () => \\{
    // 函数体
  \\}
  ```

- 利与弊：

  - 优点：箭头函数没有自己的this值，内部的this是词法上绑定的。这意味着箭头函数内部的this指向是外层第一个普通函数的this，可以更好地解决this指向的问题。
  - 缺点：无法通过call、apply、bind等方法改变this指向。

#### 组件方法：

- 定义方式：在Vue组件的methods选项中定义函数，例如：

  ```javascript
  export default \\{
    data() \\{
      return \\{
        // ...
      \\}
    \\},
    methods: \\{
      myMethod() \\{
        // 方法体
      \\}
    \\}
  \\}
  ```

- 利与弊：

  - 优点：组件方法将函数绑定到Vue组件实例上，可以在模板中直接调用该方法。而且组件的生命周期钩子函数也都是使用这种方式定义的。
  - 缺点：只能在组件内使用，无法在组件外部直接调用。

根据具体的需求和场景，选择适合的函数定义方法可以提高代码的可读性和维护性。



### vue3和typescript项目自动导入api和components

#### 安装自动导入api插件unplugin-auto-import

```cpp
yarn add unplugin-auto-import -D
```

修改vite.config.ts配置,重启项目会在 `src`目录下生成一个 `auto-import.d.ts` 文件

```javascript
import AutoImport from 'unplugin-auto-import/vite' //注意后面有个/vite
export default defineConfig((\\{ mode \\}: ConfigEnv): UserConfig => \\{
  const root = process.cwd()
  const env = loadEnv(mode, root)
  return \\{
    plugins: [
      AutoImport(\\{
        imports: ['vue', 'vue-router'],
        // 可以选择auto-import.d.ts生成的位置，使用ts建议设置为'src/auto-import.d.ts'
        dts: 'src/auto-import.d.ts'
      \\}),
    ]
  \\}
\\})
```

#### 安装自动导入组件插件unplugin-vue-components

```javascript
yarn add unplugin-vue-components -D
```

修改vite.config.ts配置,重启项目会在 `src`目录下生成一个 `components.d.ts` 文件

```javascript
import Components from 'unplugin-vue-components/vite' //注意后面有个/vite
export default defineConfig((\\{ mode \\}: ConfigEnv): UserConfig => \\{
  const root = process.cwd()
  const env = loadEnv(mode, root)
  return \\{
    plugins: [
      Components(\\{
        dirs: ['src/components'],
        extensions: ['vue', 'tsx'],
        // 配置文件生成位置
        dts: 'src/components.d.ts'
      \\})
    ]
  \\}
\\})
```

#### vue3项目中components.d.ts是什么

在Vue 3项目中，`components.d.ts` 是一个TypeScript类型声明文件，用于全局注册组件并提供类型定义，以便于在项目中使用这些组件时获得代码智能提示和类型检查。通过这种方式，Vue应用程序可以利用TypeScript的静态类型特性来提高开发效率和代码质量。

当你在一个大型项目中使用很多自定义组件，并且希望在任何地方都能直接使用这些组件而不需要每次都导入它们时，你可以在`components.d.ts`中全局声明这些组件。这通常与Vue的自动导入插件（如`unplugin-vue-components`）结合使用，该插件会根据配置自动生成或更新这个文件。

文件内容一般会像这样定义组件的类型：

```typescript
// src/components.d.ts
import Vue from 'vue';
import MButton from '@/components/global/MButton.vue';
import MInput from '@/components/global/MInput.vue';
import MCheckbox from '@/components/MCheckbox.vue';

declare module 'vue' \\{
  export interface GlobalComponents \\{
    MButton: typeof MButton;
    MInput: typeof MInput;
    MCheckbox: typeof MCheckbox;
    ElDrawer: typeof import('element-plus/es')['ElDrawer']
    VanImagePreview: typeof import('vant/es')['ImagePreview']
  \\}
\\}

export \\{\\};

// 这段代码告诉Vue的类型系统关于这些全局组件的信息，
// 使得在模板和Vue文件中使用这些组件时能够得到正确的类型提示。
```

通过上述声明，你就可以在整个项目中直接使用`<MButton>`、`<MInput>` 和 `<MCheckbox>` 等组件，而IDE将会提供准确的类型检查和自动完成建议。



### defineProps() 和 defineEmits()

为了在声明 `props` 和 `emits` 选项时获得完整的类型推导支持，我们可以使用 `defineProps` 和 `defineEmits` API，它们将自动地在 `  <script setup>  ` 中可用：

- `defineProps` 和 `defineEmits` 都是只能在 `  <script setup>  ` 中使用的**编译器宏**。他们**不需要导入**，且会随着 `  <script setup>  ` 的处理过程一同被编译掉。
- `defineProps` 接收与 `props` 选项相同的值，`defineEmits` 接收与 `emits` 选项相同的值。
- `defineProps` 和 `defineEmits` 在选项传入后，会提供恰当的类型推导。
- 传入到 `defineProps` 和 `defineEmits` 的选项会从 setup 中提升到模块的作用域。因此，传入的选项不能引用在 setup 作用域中声明的局部变量。这样做会引起编译错误。但是，它*可以*引用导入的绑定，因为它们也在模块作用域内。

https://cn.vuejs.org/api/sfc-script-setup.html#defineprops-defineemits



### defineExpose 、defineProps、defineEmits

是vue3的写法并且是一个仅 <script setup> 中可用的编译宏命令，并不需要显式地导入；

defineExpose 来显式指定在 <script setup> 组件中要暴露出去的属性。 defineProps、defineEmits在vue3的非语法糖setup和在vue2中的写法是 props,emit 

#### defineExpose   子传父 

（用在子组件，暴露想传递的值或方法，父组件通过ref属性获取子组件暴露的）

1. 作用
defineExpose定义：用于组件通信中父级组件调用操作子组建方法和响应式属性参数能力，即子组件将值和方法传给父组件。

2. 原理
使用 <script setup> 的组件是默认关闭的——即通过模板引用或者 $parent 链获取到的组件的公开实例，不会暴露任何在 <script setup> 中声明的绑定。

那么，通过 defineExpose 编译器宏来显式指定在 <script setup> 组件中要暴露出去的属性

然后，父组件通过ref属性访问子组件

3. 实例
 父组件：


    <Index ref="childeRef"></Index>
     
    <script setup>
        import Index from "./index.vue";
     
        const childeRef = ref();
     
        function test() \\{
            console.log(childeRef.value.msg) // Hello World
        \\}
     
        onMounted(() => \\{
          let flag:boolean = true;
          let value:number= 5;
          childeRef.value.childFn(flag,value) // 调用子组件函数, 输出 6
        \\})
     
    </script>

子组件：


    <script setup>
        import \\{ref\\} from "vue";
     
        function childFn(type：boolean, data：number) \\{
            console.log('我是子组件');
            if(data)\\{
               let value = data + 1;   
               return value;
            \\}
        \\}
        
        const msg = 'Hello World';
        const num = ref(0);
        
        defineExpose(\\{ //暴露想要传递的值或方法
            msg,
            childFn,
        \\});
    </script>
#### defineProps  父传子 

（用在子组件，接收父组件的传值，用来声明props）

1. 作用
它可以帮助我们在组件中自定义 props,并定义它们的数据类型和默认值。使用这个新特性,可以更加方便地管理组件的 Props 数据

2. 原理
defineProps() 宏中的参数不可以访问 <script setup>中定义的其他变量，因为在编译时整个表达式都会被移到外部的函数中，即必须在<script setup>的顶层使用，不可以在<script setup>的局部变量中引用；

3. 实例
父组件：


    <templte>
       <sub-task-detail
          v-model:open="subTaskDetailVisible"
          :task-info="task"
          :sub-task-id="subTaskId"
          :tab="tabIndex"
        />
    </templte>
     
    <script setup>
        
        const subTaskDetailVisible = ref(false)
        
        const handleDetail = (row) => \\{
          subTaskDetailVisible.value = true
          subTaskId.value = row.id
          tabIndex.value = 1
        \\}
     
    </script>

子组件：

```
<script setup>
import \\{ ref, watch, onMounted, onBeforeUnmount, h \\} from 'vue'
import \\{ subTaskDetail, downloadLog \\} from '@/api/detail'
import BigDataList from './BigDataList.vue'
import dayjs from 'dayjs'
import \\{ useI18n \\} from 'vue-i18n'
import \\{ MIGRATION_MODE, SUB_TASK_STATUS \\} from '@/utils/constants'
 
const \\{ t \\} = useI18n()
 
const props = defineProps(\\{
  open: Boolean,
  taskInfo: Object,
  subTaskId: [String, Number],
  tab: [String, Number]
\\})
//也可以let props = defineProps(['open','taskInfo','subTaskId','tab']);
 
onMounted(() => \\{
  visible.value = props.open
\\})
 
</script>
```

#### defineEmits  子传父 

（用在子组件，将子组件的方法传递给父组件，用来声明emits）


1. 作用
用于在setup中注册自定义事件，方便开发者监听和绑定事件。是一个宏函数，使用时无需导入

2. 原理
不可以访问 <script setup>中定义的其他变量，因为在编译时整个表达式都会被移到外部的函数中，即defineEmits必须放在全局，否则报错。

3. 实例
父组件：

```
<template>
 
 <add-jdbc ref="addJdbcRef" @finish="finishAddJdbc" />
 
</template>
 
<script setup>
import \\{ reactive, ref, computed, watch, onMounted, toRaw, h, compile \\} from 'vue'
import AddJdbc from '../components/AddJdbc.vue'
import \\{ sourceClusters, targetClusters, sourceClusterDbsData, targetClusterDbsData \\} from '@/api/task'
 
const finishAddJdbc = (type) => \\{
  if (type === 'ORACLE'||type === 'MYSQL') \\{
    getSourceClustersData()
  \\} else \\{
    getTargetClustersData()
  \\}
\\}
</script>
```

子组件：

    <script setup>
    //defineEmits接受一个数组，元素为自定义事件名
    //返回一个触发器，用于触发事件，第一个参数是具体事件名，第二个是传递的值
     
     emits = defineEmits([`finish`])
     
     const submit = () => \\{
        // save
        data.loading = true
     
        const param = \\{
          clusterName: data.form.name,
          dbType: data.form.dbType,
          deployType: data.form.nodes.length > 1 ? 'CLUSTER' : 'SINGLE_NODE',
          nodes: []
        \\}
     
        addJdbc(param).then((res) => \\{
          data.loading = false
          if (Number(res.code) === 200) \\{
            Message.success(\\{ content: `Create success` \\})
            emits(`finish`, data.form.dbType)
          \\}
          close()
        \\})
    \\}
原文链接：https://blog.csdn.net/Realizee/article/details/131131134



### defineProps，defineEmits，defineExpose去掉

`defineProps` is a compiler macro and no longer needs to be imported.

`defineExpose` is a compiler macro and no longer needs to be imported.

这个错误信息意味着你在使用Vue 3的新 Composition API，并且你错误地尝试导入了 `defineProps`。在Vue 3中，`defineProps` 和 `defineEmits` 是编译器宏（compiler macros），它们不需要像普通函数那样被显式导入。当你在 `<script setup>` 语法或者使用Vue的Composition API时，可以直接使用这些宏来定义组件的props和emits。

#### 如何修正

如果你的代码是这样的：

```javascript
import \\{ defineProps \\} from 'vue';

export default \\{
  setup() \\{
    const props = defineProps(\\{
      // props定义
    \\});
    // ...
  \\},
\\};
```

你应该改为使用 `<script setup>` 语法，直接使用 `defineProps`，无需导入：

```html
<script setup>
const props = defineProps(\\{
  // props定义
\\});
// ...
</script>
```

或者，如果你的项目配置支持但没有使用 `<script setup>`，直接在普通的 `setup` 函数中使用，也不需要导入：

```javascript
export default \\{
  setup() \\{
    const props = defineProps(\\{
      // props定义
    \\});
    // ...
  \\},
\\};
```

确保你的Vue版本是3或以上，并且Vue CLI或构建配置支持Vue 3的Composition API特性。这样修改后，该警告就应该会消失。



### :v-deep弃用

`:v-deep usage as a combinator has been deprecated. Use :deep(<inner-selector>) instead of ::v-deep <inner-selector>.`

如果你在使用Vue.js并收到关于`:v-deep`作为组合器已被弃用的警告，提示你使用`:deep(<inner-selector>)`替代`::v-deep <inner-selector>`，这意味着你的代码需要进行相应的更新以遵循新的最佳实践。

#### 如何修正

假设你有如下代码，使用了已弃用的`:v-deep`：

```html
<style scoped>
.parent \\{
  ::v-deep .child \\{
    color: red;
  \\}
\\}
</style>
```

你应该按照警告提示修改为使用`:deep()`：

```html
<style scoped>
.parent \\{
  :deep(.child) \\{
    color: red;
  \\}
\\}
</style>
```

#### 注意事项

- **兼容性**: 这一改变是为了更好的标准兼容性和未来的Vue.js版本。`:deep()`是Vue为了兼容Web Components的Shadow DOM样式穿透而引入的，它在Vue 2.x中通过插件支持，在Vue 3中则原生支持。
  
- **更新依赖**: 如果你是在Vue CLI创建的项目或是使用了如Vue Loader等工具，确保它们也是最新版本或至少支持`:deep()`语法。有时，过时的构建工具可能是导致新语法不工作的原因。

- **逐步迁移**: 如果项目中有大量使用到`:v-deep`的情况，可以考虑逐步迁移，每次修改一部分，特别是当你计划升级Vue版本或优化代码库时。

总之，根据警告的指导，将`:v-deep`替换为`:deep()`是一个向前兼容的改动，有助于保持代码的现代性和可维护性。



### vue3父组件调用子组件方法

在 Vue 3 中，父组件调用子组件的方法通常涉及到使用 `ref` 和 `defineExpose`。下面是一些关键步骤和示例代码：

#### 步骤 1: 在子组件中定义需要暴露的方法

在子组件中，你需要使用 `defineExpose` 函数来明确指定哪些方法应该对外公开，这样父组件才能访问这些方法。

```javascript
// 子组件 Child.vue
<script setup>
import \\{ defineExpose \\} from 'vue';

// 定义子组件中的方法
const doSomething = () => \\{
  console.log('子组件中的方法被调用了');
\\};

// 使用 defineExpose 明确暴露哪些方法
defineExpose(\\{ doSomething \\});
</script>
```

#### 步骤 2: 在父组件中使用 `ref` 引用子组件

在父组件中，你需要给子组件的标签添加一个 `ref` 属性，并在父组件的 `setup` 函数中声明这个 `ref`。

```javascript
// 父组件 Parent.vue
<template>
  <child-component ref="childRef" />
</template>

<script setup>
import ChildComponent from './ChildComponent.vue';

const childRef = ref(null); // 声明 ref
</script>
```

#### 步骤 3: 调用子组件的方法

现在，你可以在父组件的任何地方通过 `childRef.value.doSomething()` 来调用子组件的 `doSomething` 方法。

```javascript
// 父组件 Parent.vue
<script setup>
import ChildComponent from './ChildComponent.vue';
import \\{ ref \\} from 'vue';

const childRef = ref(null);

// 在父组件中调用子组件的方法
const callChildMethod = () => \\{
  if (childRef.value) \\{
    childRef.value.doSomething();
  \\}
\\};
</script>
```

#### 步骤 4: 在父组件中使用方法

你可以在父组件的任何事件处理器、计算属性或生命周期钩子中调用 `callChildMethod` 函数。

```html
<!-- 父组件 Parent.vue -->
<template>
  <button @click="callChildMethod">调用子组件方法</button>
  <child-component ref="childRef" />
</template>
```

#### 总结

使用这种方式，你可以有效地从父组件中调用子组件的方法，这在很多场景下都非常有用，比如初始化子组件的状态、触发子组件的某些动作或者获取子组件的数据等。记住，`ref` 必须在 DOM 更新完成后才能访问到子组件实例，因此在组件挂载之后或响应式数据变化后调用这些方法才是安全的。

如果父组件需要修改子组件变量，使用 Props 和 Events 是更推荐的做法，因为它遵循了 Vue 的单向数据流原则。 



### vue3中使用vue2的写法，子组件更新父组件的值

子组件

```
this.$emit('update:selectId', selectedValues)
```

父组件

```
<PopupSelect v-model:selectId="selectId"/>
```



### 简化版：父组件的修改可以传递到子组件，子组件方便的更新父组件的值

子组件方法中怎么实现props.areaParams.pageIndex++

这两个数据

```
// 专区列表请求参数
const areaParams = reactive(\\{
  areaId: 1,
  areaGroupId: null, // 不传查所有，传 -1 查未分组
  areaMaterialName: '',
  pageIndex: 1,
  pageSize: 20,
\\})// 是否全部加载完成
const finished = ref(false)
```

父组件reactive的数据类型，传递给子组件没有更新，怎么解决

**reactive换成ref即可**，真的坑

#### 父组件示例

```vue
<template>
  <div>
    <h3>Parent Component</h3>
    <p>Current Page Index: \\\{\\\{ areaParams.pageIndex\\\}\\\} }}</p>
    <child-component :areaParams="areaParams" @update:areaParams="areaParams = $event" />
  </div>
</template>

<script setup>
import \\{ reactive \\} from 'vue';
import ChildComponent from './ChildComponent.vue';

const areaParams = ref(\\{
  areaId: 1,
  areaGroupId: null, // 不传查所有，传 -1 查未分组
  areaMaterialName: '',
  pageIndex: 1,
  pageSize: 20,
\\});
</script>
```

#### 子组件示例

```vue
<template>
  <button @click="loadMore">Load More</button>
</template>

<script setup>
const props = defineProps(\\{
  areaParams: \\{
    type: Object,
    required: true,
  \\},
\\});

const emit = defineEmits(['update:areaParams']);

const loadMore = () => \\{
  // 更新pageIndex并通知父组件
  emit('update:areaParams', \\{ ...props.areaParams, pageIndex: props.areaParams.pageIndex + 1 \\});
\\};
</script>
```

在这两个示例中：
- 父组件通过`areaParams`属性传递给子组件一个对象。
- 子组件有一个`loadMore`按钮，当点击时会增加`pageIndex`的值，并通过`update:areaParams`事件通知父组件更新`areaParams`对象。
- 父组件监听`update:areaParams`事件，并通过事件参数（$event）更新`areaParams`。

这样，子组件就可以方便地更新父组件的数据了。如果你还需要处理`finished`的状态，可以按照类似的方式在子组件中通过`update:finished`事件来通知父组件。



### 复杂版：v-model可以实现父传子，并且子也可以修改父组件传递过来的数据。那多个值怎么办，子组件方法中怎么实现props.areaParams.pageIndex++ 

使用 `v-model` 来实现父组件向子组件传递多个数据，并允许子组件修改这些数据，你可以创建一个包含所有需要双向绑定的属性的对象，并通过 `v-model` 来绑定这个对象。

对于多个值的情况，你可以创建一个包含所有需要双向绑定的属性的对象，并通过 `v-model` 来绑定这个对象。然后，在子组件中，你可以通过触发自定义事件来更新父组件中的数据。

下面是一个具体的示例，演示了如何使用 `v-model` 和自定义事件来实现这一功能：

#### 父组件 (Parent.vue)

```vue
<template>
  <div>
    <h2>Parent Component</h2>
    <pre>\\\{\\\{ JSON.stringify(areaParams, null, 2)\\\}\\\} }}</pre>
    <child-component v-model:area-params="areaParams" :finished="finished" @update-finished="updateFinished"></child-component>
  </div>
</template>

<script setup>
import \\{ reactive, toRefs \\} from 'vue';
import ChildComponent from './Child.vue';

const areaParams = ref(\\{
  areaId: 4,
  areaGroupId: null, // 不传查所有，传 -1 查未分组
  areaMaterialName: '',
  pageIndex: 1,
  pageSize: 20,
\\});
// 使用 toRefs 将响应式对象解构为单独的响应式属性
const \\{ areaParams: areaParamsRef \\} = toRefs(areaParams);

// 是否全部加载完成
const finished = ref(false)
// 更新finished状态
const updateFinished = (newFinished) => \\{
  finished.value = newFinished
\\}
</script>
```

#### 子组件 (Child.vue)

```vue
<template>
  <div>
    <h3>Child Component</h3>
    <button @click="incrementPageIndex">Increment Page Index</button>
  </div>
</template>

<script setup>
import \\{ onMounted, watchEffect \\} from 'vue';

const props = defineProps(\\{
  areaParams: \\{
    type: Object,
    required: true
  \\},
  finished: Boolean
\\});

const emit = defineEmits(['update:area-params', 'update-finished']);

// 当内部状态改变时，通过 emit 通知父组件
function incrementPageIndex() \\{
  const newPageIndex = props.areaParams.pageIndex + 1;
  emit('update:area-params', \\{ ...props.areaParams, pageIndex: newPageIndex \\});
\\}
// 当内部状态改变时，通过 emit 通知父组件
function finishProcess() \\{
  emit('update-finished', true);
\\}
</script>
```

#### 解释

1. **父组件**:
   - 定义了一个响应式的 `areaParams` 对象。
   - 使用 `toRefs` 将 `areaParams` 对象解构成单独的响应式属性。
   - 将 `areaParams` 通过 `v-model:area-params` 传递给子组件。

2. **子组件**:
   - 接收 `areaParams` 作为 prop。
   - 定义了一个 `incrementPageIndex` 方法，该方法会在按钮点击时触发。
   - 当点击按钮时，`incrementPageIndex` 方法会增加 `areaParams.pageIndex` 的值，并通过 `emit` 发出 `update:area-params` 事件，传递新的参数值。

#### 注意事项

- 确保子组件中 `areaParams` 的类型与父组件传递的数据类型相匹配。
- 在子组件中使用 `v-model` 时，需要使用正确的事件名称格式，例如 `v-model:area-params`，其中 `area-params` 需要与父组件传递的 prop 名称一致。
- 当子组件中的数据发生变化时，通过 `emit` 发送 `update:area-params` 事件，并传递新的值。

这种方法提供了一种简单的方式来实现双向数据绑定，并保持代码的简洁和可维护性。同时，它确保了 `props` 的只读特性不会被破坏。



### \\{ ...props.areaParams, pageIndex: newPageIndex \\}这个是什么意思

在 JavaScript 中，表达式 `\\{ ...props.areaParams, pageIndex: newPageIndex \\}` 是用来创建一个新对象的，这个新对象包含了原对象 `props.areaParams` 的所有属性和值，同时还覆盖了 `pageIndex` 属性的新值 `newPageIndex`。

让我们详细解释一下这个表达式的组成部分：

1. **扩展运算符 (`...`)**:
   - 扩展运算符可以用于将一个数组的元素展开为单独的元素，或者将一个对象的属性展开为单独的键值对。
   - 在这个上下文中，`...props.areaParams` 表示将 `props.areaParams` 对象的所有属性和值展开。
2. **对象字面量 (`\\{\\}`)**:
   - `\\{ ...props.areaParams \\}` 创建了一个新对象，该对象包含了来自 `props.areaParams` 的所有属性。
   - `pageIndex: newPageIndex` 是一个键值对，表示新对象的 `pageIndex` 属性应具有值 `newPageIndex`。
3. **合并结果**:
   - 当你将 `\\{ ...props.areaParams \\}` 和 `pageIndex: newPageIndex` 放在一起时，JavaScript 会创建一个新对象，该对象首先包含 `props.areaParams` 的所有属性，然后用 `pageIndex: newPageIndex` 覆盖 `pageIndex` 的值。



# vue3为什么同时需要Ref和Reactive？

**前言**

Vue 3 引入了两个新的响应式 API：`ref` 和 `reactive`。这两个 API 都可以用于创建响应式数据，但它们在使用场景和实现方式上有一些显著的区别。本文将详细探讨 Vue 3 为什么需要同时引入 `ref` 和 `reactive`，并通过代码示例来展示它们各自的优势和适用场景。![图片](https://mmbiz.qpic.cn/mmbiz_png/4db5hNb7fBAvD240juYRIJdia0XZw0XZKWMYGibicrNh0HwSqWXLxiaXicuHTdlYpPAmNgPMga5y3KibG1w09SR6vrHg/640?&random=0.8406257866180358&random=0.29900129741161896&random=0.21939590800556963&wxfrom=13&tp=wxpic)

## Ref 和 Reactive 的介绍

### 什么是 Ref？

`ref` 是一个函数，用于创建一个包含单一值的响应式对象。它可以包装任意类型的值，包括基本类型和对象类型。当 `ref` 包装的值发生变化时，Vue 会自动追踪并触发相应的更新。

```
import \\{ ref \\} from 'vue';

const count = ref(0);

console.log(count.value); // 输出：0

count.value = 1;
console.log(count.value); // 输出：1
```

![图片](https://mmbiz.qpic.cn/mmbiz_svg/UDa9R1yl9Ub4qlLE2gdnrJ4H8YBTDcP2fF5bWVFPiabmb8rKIKUkHekcibgFycjUprqEm0cIXQPnJsmuJDOVG5QJsxI9taORZT/640?wx_fmt=svg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

### 什么是 Reactive？

`reactive` 是一个函数，用于创建一个深层响应式的对象。当对象的任何属性发生变化时，Vue 都会自动追踪并触发更新。`reactive` 只能用于对象，而不能用于基本类型。

```
import \\{ reactive \\} from 'vue';

const state = reactive(\\{
  count: 0,
  user: \\{
    name: 'Alice',
    age: 25
  \\}
\\});

console.log(state.count); // 输出：0

state.count++;
console.log(state.count); // 输出：1
```

![图片](https://mmbiz.qpic.cn/sz_mmbiz_jpg/Ric3gNzlqMkt9jsdVicQDpibgCOtumQrGic54enL0CEhdrmKU5WYmicXxIr9SfoJ1SEQCkLgY2m0jUYw88ibahqicOGCA/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

## Ref 和 Reactive 的区别

### 数据类型

- `ref` 可以包装任意类型的数据，包括基本类型和对象。
- `reactive` 只能用于创建对象的深层响应式状态。

### API 设计

- `ref` 返回一个包含 `value` 属性的对象，使用时需要通过 `value` 访问和修改实际数据。
- `reactive` 返回的是一个代理对象，直接通过对象的属性访问和修改数据。

### 使用场景

- `ref` 适用于处理基本类型的数据或希望在使用对象时保持 API 一致性。
- `reactive` 适用于处理复杂的对象状态，并希望自动处理嵌套的响应式属性。

## 为什么需要同时使用 Ref 和 Reactive？

### 灵活性

在实际开发中，我们会遇到各种不同的数据结构和使用场景。`ref` 和 `reactive` 的引入，为开发者提供了更多的选择和灵活性。我们可以根据具体需求选择最合适的响应式 API。

### 性能优化

`ref` 和 `reactive` 在实现机制上有所不同。在某些场景下，使用 `ref` 可以带来更好的性能。例如，对于频繁变更的基本类型数据，使用 `ref` 会更高效。

### 代码可读性和一致性

在一些场景中，使用 `ref` 可以使代码更加简洁和易读。特别是当我们希望保持 API 一致性时，`ref` 是一个很好的选择。例如，当我们使用组合式 API 组合多个响应式状态时，使用 `ref` 可以保持访问方式的一致性。

## 实际使用示例

### 基本示例

#### 使用 Ref

```
<template>
  <div>
    <p>Count: \\\{\\\{ count.value\\\}\\\} }}</p>
    <button @click="increment">Increment</button>
  </div>
</template>

<script>
import \\{ ref \\} from 'vue';

export default \\{
  setup() \\{
    const count = ref(0);

    const increment = () => \\{
      count.value++;
    \\};

    return \\{
      count,
      increment
    \\};
  \\}
\\};
</script>
```

#### 使用 Reactive

```
<template>
  <div>
    <p>Count: \\\{\\\{ state.count\\\}\\\} }}</p>
    <button @click="increment">Increment</button>
  </div>
</template>

<script>
import \\{ reactive \\} from 'vue';

export default \\{
  setup() \\{
    const state = reactive(\\{
      count: 0
    \\});

    const increment = () => \\{
      state.count++;
    \\};

    return \\{
      state,
      increment
    \\};
  \\}
\\};
</script>
```

### 复杂示例

#### 混合使用 Ref 和 Reactive

在实际应用中，我们经常需要同时使用 `ref` 和 `reactive` 来处理不同类型的数据。例如：

```
<template>
  <div>
    <p>Message: \\\{\\\{ message.value\\\}\\\} }}</p>
    <p>Count: \\\{\\\{ state.count\\\}\\\} }}</p>
    <p>User: \\\{\\\{ state.user.name\\\}\\\} }} (\\\{\\\{ state.user.age\\\}\\\} }} years old)</p>
    <button @click="updateMessage">Update Message</button>
    <button @click="incrementCount">Increment Count</button>
    <button @click="updateUser">Update User</button>
  </div>
</template>

<script>
import \\{ ref, reactive \\} from 'vue';

export default \\{
  setup() \\{
    const message = ref('Hello, Vue 3!');
    const state = reactive(\\{
      count: 0,
      user: \\{
        name: 'Alice',
        age: 25
      \\}
    \\});

    const updateMessage = () => \\{
      message.value = 'Hello, World!';
    \\};

    const incrementCount = () => \\{
      state.count++;
    \\};

    const updateUser = () => \\{
      state.user.name = 'Bob';
      state.user.age = 30;
    \\};

    return \\{
      message,
      state,
      updateMessage,
      incrementCount,
      updateUser
    \\};
  \\}
\\};
</script>
```

## 结论

在 Vue 3 中，`ref` 和 `reactive` 是两个核心的响应式 API，它们各自解决了不同的问题，提供了更大的灵活性和更好的性能。在实际开发中，我们可以根据具体需求选择最合适的响应式 API，从而编写出更加简洁、高效和易于维护的代码。

- `ref`：适用于处理基本类型的数据，或者希望在使用对象时保持 API 一致性。
- `reactive`：适用于处理复杂的对象状态，并希望自动处理嵌套的响应式属性。

通过合理使用这两个 API，我们可以充分利用 Vue 3 的响应式系统，提高开发效率和应用性能。







# vue3请求封装

#### 安装

```
npm install axios
npm install js-cookie
```

#### 在utils文件夹封装js

request.js

```
import axios from 'axios'
import cache from '@/utils/cache'
import errorCode from '@/utils/errorCode'
import Config from '@/config';
import \\{ ElNotification, ElMessageBox, ElMessage, ElLoading \\} from 'element-plus'
import \\{ getToken \\} from '@/utils/auth'
import \\{ tansParams, blobValidate \\} from '@/utils/index'
// import \\{ saveAs \\} from 'file-saver'
// import useUserStore from '@/store/modules/user'

let downloadLoadingInstance;
// 是否显示重新登录
export let isRelogin = \\{ show: false \\};

axios.defaults.headers['Content-Type'] = 'application/json;charset=utf-8'
// 创建axios实例
const service = axios.create(\\{
    // axios中请求配置有baseURL选项，表示请求URL公共部分
    baseURL: Config.server.url + Config.server.prefix,
    // 超时
    timeout: 55000
\\})

// request拦截器
service.interceptors.request.use(config => \\{
    console.log(config);
    // 是否需要设置 token
    const isToken = (config.headers || \\{\\}).isToken === false
    // 是否需要防止数据重复提交
    const isRepeatSubmit = (config.headers || \\{\\}).repeatSubmit === false
    if (getToken() && !isToken) \\{
        config.headers['Authorization'] = 'Bearer ' + getToken() // 让每个请求携带自定义token 请根据实际情况自行修改
    \\}
    // get请求映射params参数
    if (config.method === 'get' && config.data) \\{
        let url = config.url + '?' + tansParams(config.data);
        url = url.slice(0, -1);
        config.data = \\{\\};
        config.url = url;
    \\}
    if (!isRepeatSubmit && (config.method === 'post' || config.method === 'put')) \\{
        const requestObj = \\{
            url: config.url,
            data: typeof config.data === 'object' ? JSON.stringify(config.data) : config.data,
            time: new Date().getTime()
        \\}
        const requestSize = Object.keys(JSON.stringify(requestObj)).length; // 请求数据大小
        const limitSize = 5 * 1024 * 1024; // 限制存放数据5M
        if (requestSize >= limitSize) \\{
            console.warn(`[$\\{config.url\\}]: ` + '请求数据大小超出允许的5M限制，无法进行防重复提交验证。')
            return config;
        \\}
        const sessionObj = cache.session.getJSON('sessionObj')
        if (sessionObj === undefined || sessionObj === null || sessionObj === '') \\{
            cache.session.setJSON('sessionObj', requestObj)
        \\} else \\{
            const s_url = sessionObj.url;                // 请求地址
            const s_data = sessionObj.data;              // 请求数据
            const s_time = sessionObj.time;              // 请求时间
            const interval = 1000;                       // 间隔时间(ms)，小于此时间视为重复提交
            if (s_data === requestObj.data && requestObj.time - s_time < interval && s_url === requestObj.url) \\{
                const message = '数据正在处理，请勿重复提交';
                console.warn(`[$\\{s_url\\}]: ` + message)
                return Promise.reject(new Error(message))
            \\} else \\{
                cache.session.setJSON('sessionObj', requestObj)
            \\}
        \\}
    \\}
    return config
\\}, error => \\{
    console.log(error)
    Promise.reject(error)
\\})

// 响应拦截器
service.interceptors.response.use(res => \\{
    // 未设置状态码则默认成功状态
    const code = res.data.code || 200;
    // 获取错误信息
    const msg = errorCode[code] || res.data.msg || errorCode['default']
    // 二进制数据则直接返回
    if (res.request.responseType === 'blob' || res.request.responseType === 'arraybuffer') \\{
        return res.data
    \\}
    if (code === 401) \\{
        if (!isRelogin.show) \\{
            isRelogin.show = true;
            ElMessageBox.confirm('登录状态已过期，您可以继续留在该页面，或者重新登录', '系统提示', \\{ confirmButtonText: '重新登录', cancelButtonText: '取消', type: 'warning' \\}).then(() => \\{
                isRelogin.show = false;
                // useUserStore().logOut().then(() => \\{
                //   location.href = '/index';
                // \\})
            \\}).catch(() => \\{
                isRelogin.show = false;
            \\});
        \\}
        return Promise.reject('无效的会话，或者会话已过期，请重新登录。')
    \\} else if (code === 500) \\{
        ElMessage(\\{ message: msg, type: 'error' \\})
        return Promise.reject(new Error(msg))
    \\} else if (code === 601) \\{
        ElMessage(\\{ message: msg, type: 'warning' \\})
        return Promise.reject(new Error(msg))
    \\} else if (code !== 200) \\{
        ElNotification.error(\\{ title: msg \\})
        return Promise.reject('error')
    \\} else \\{
        return Promise.resolve(res.data)
    \\}
\\},
    error => \\{
        console.log('err' + error)
        let \\{ message \\} = error;
        if (message == "Network Error") \\{
            message = "后端接口连接异常";
        \\} else if (message.includes("timeout")) \\{
            message = "系统接口请求超时";
        \\} else if (message.includes("Request failed with status code")) \\{
            message = "系统接口" + message.substr(message.length - 3) + "异常";
        \\}
        ElMessage(\\{ message: message, type: 'error', duration: 5 * 1000 \\})
        return Promise.reject(error)
    \\}
)

// 通用下载方法
export function download(url, params, filename, config) \\{
    downloadLoadingInstance = ElLoading.service(\\{ text: "正在下载数据，请稍候", background: "rgba(0, 0, 0, 0.7)", \\})
    return service.post(url, params, \\{
        transformRequest: [(params) => \\{ return tansParams(params) \\}],
        headers: \\{ 'Content-Type': 'application/x-www-form-urlencoded' \\},
        responseType: 'blob',
        ...config
    \\}).then(async (data) => \\{
        const isBlob = blobValidate(data);
        if (isBlob) \\{
            const blob = new Blob([data])
            saveAs(blob, filename)
        \\} else \\{
            const resText = await data.text();
            const rspObj = JSON.parse(resText);
            const errMsg = errorCode[rspObj.code] || rspObj.msg || errorCode['default']
            ElMessage.error(errMsg);
        \\}
        downloadLoadingInstance.close();
    \\}).catch((r) => \\{
        console.error(r)
        ElMessage.error('下载文件出现错误，请联系管理员！')
        downloadLoadingInstance.close();
    \\})
\\}

export default service
```

auth.js

```
import Cookies from 'js-cookie'

const TokenKey = 'token'

export function getToken() \\{
    return Cookies.get(TokenKey)
\\}

export function setToken(token) \\{
    return Cookies.set(TokenKey, token)
\\}

export function removeToken() \\{
    return Cookies.remove(TokenKey)
\\}
```

cache.js

```
const sessionCache = \\{
    set(key, value) \\{
        if (!sessionStorage) \\{
            return
        \\}
        if (key != null && value != null) \\{
            sessionStorage.setItem(key, value)
        \\}
    \\},
    get(key) \\{
        if (!sessionStorage) \\{
            return null
        \\}
        if (key == null) \\{
            return null
        \\}
        return sessionStorage.getItem(key)
    \\},
    setJSON(key, jsonValue) \\{
        if (jsonValue != null) \\{
            this.set(key, JSON.stringify(jsonValue))
        \\}
    \\},
    getJSON(key) \\{
        const value = this.get(key)
        if (value != null) \\{
            return JSON.parse(value)
        \\}
    \\},
    remove(key) \\{
        sessionStorage.removeItem(key);
    \\}
\\}
const localCache = \\{
    set(key, value) \\{
        if (!localStorage) \\{
            return
        \\}
        if (key != null && value != null) \\{
            localStorage.setItem(key, value)
        \\}
    \\},
    get(key) \\{
        if (!localStorage) \\{
            return null
        \\}
        if (key == null) \\{
            return null
        \\}
        return localStorage.getItem(key)
    \\},
    setJSON(key, jsonValue) \\{
        if (jsonValue != null) \\{
            this.set(key, JSON.stringify(jsonValue))
        \\}
    \\},
    getJSON(key) \\{
        const value = this.get(key)
        if (value != null) \\{
            return JSON.parse(value)
        \\}
    \\},
    remove(key) \\{
        localStorage.removeItem(key);
    \\}
\\}

export default \\{
    /**
     * 会话级缓存
     */
    session: sessionCache,
    /**
     * 本地缓存
     */
    local: localCache
\\}
```

errorCode.js

```
export default \\{
    '401': '认证失败，无法访问系统资源',
    '403': '当前操作没有权限',
    '404': '访问资源不存在',
    'default': '系统未知错误，请反馈给管理员'
\\}
```

index.js

```
/**
* 参数处理
* @param \\{*\\} params  参数
*/
export function tansParams(params) \\{
    let result = ''
    for (const propName of Object.keys(params)) \\{
        const value = params[propName];
        var part = encodeURIComponent(propName) + "=";
        if (value !== null && value !== "" && typeof (value) !== "undefined") \\{
            if (typeof value === 'object') \\{
                for (const key of Object.keys(value)) \\{
                    if (value[key] !== null && value[key] !== "" && typeof (value[key]) !== 'undefined') \\{
                        let params = propName + '[' + key + ']';
                        var subPart = encodeURIComponent(params) + "=";
                        result += subPart + encodeURIComponent(value[key]) + "&";
                    \\}
                \\}
            \\} else \\{
                result += part + encodeURIComponent(value) + "&";
            \\}
        \\}
    \\}
    return result
\\}

// 验证是否为blob格式
export function blobValidate(data) \\{
    return data.type !== 'application/json'
\\}
```

#### 在api文件夹封装js

http.js

```
import common from '@/api/common';

const $http = Object.assign(
    \\{\\},
    common,
);

export default $http;
```

common.js

```
// 接口调用封装
import $api from '@/utils/request'

const $http = \\{\\};

// 获取注册验证码
$http.getRegisterCode = (data) => $api(\\{
    url: "/auth/register/code",
    data,
    method: "post"
\\})

// 行程记录列表
$http.travelRecord = (data) => $api(\\{
    url: '/travel-record',
    data,
    method: "get"
\\})

export default $http;
```

#### 在vue文件夹使用

```
		import $http from '@/api/http'

		// 打开抽屉
        show() \\{
            this.drawer = true
            $http.getRegisterCode(\\{
                phone: '187341314xx',
                captcha: '123'
            \\})
            $http.travelRecord(\\{
                page: 1,
                limit: 15,
                car_num: '',
                name: ''
            \\})
        \\},
```

参考文档

https://www.axios-http.cn/docs/intro



### token放在cookie和localstorage的区别

#### Cookie和LocalStorage都是用于在浏览器端存储数据的技术，但它们有以下几个主要的区别：

存储容量：Cookie存储的数据大小有限制，一般为4KB左右；而LocalStorage可以存储更大的数据，一般为5MB或者更多。

存储位置：Cookie数据会随着每次HTTP请求自动发送到服务器端，而LocalStorage的数据只存在于浏览器端。

过期时间：Cookie可以设置过期时间，一旦过期就会被浏览器删除，而LocalStorage存储的数据不会过期，除非手动清除。

安全性：由于Cookie会被发送到服务器端，所以它们的数据可能被拦截和篡改，存在一定的安全风险；而LocalStorage数据只存储在浏览器端，相对来说更加安全。

访问权限：Cookie可以设置访问路径和访问域名，以控制哪些页面可以访问Cookie；而LocalStorage存储的数据可以被同一域名下的所有页面访问。

根据具体的业务需求和安全要求，可以选择合适的数据存储方式。一般来说，如果需要存储较小的数据，或者需要将数据发送给服务器进行处理，可以选择使用Cookie；如果需要存储较大的数据，或者需要在客户端进行快速读写操作，可以选择使用LocalStorage。

#### token存在cookie和localstorage的区别：

在前端中，将token存储在cookie或者localStorage中都有各自的优缺点，需要根据实际情况进行选择。

将token存储在cookie中的优点是：

安全性更高：cookie在传输过程中会被加密，避免了敏感数据在传输过程中被篡改或者被截获。

可以设置过期时间：cookie可以设置过期时间，这样可以控制token的有效期，减少token被滥用的风险。

对于一些后端框架，比如Spring Security，需要在cookie中存储token才能进行认证。

将token存储在localStorage中的优点是：

容易访问：localStorage的API简单易用，可以方便地获取和修改存储的数据。

便于多个标签页之间的数据共享。

跨域请求时可以携带localStorage，而不能携带cookie。

#### localstorage有可能被类似chrome中的插件所获取

将token存储在localStorage中也存在一些风险，因为localStorage的数据存储在本地，如果用户的电脑被恶意软件攻击，也有可能被窃取。另外，localStorage的API也比cookie的API更容易受到类似Chrome插件的攻击，但这些风险可以通过使用https协议来减轻。

综上所述，将token存储在cookie中或localStorage中都有其优缺点，需要根据实际情况进行选择。如果需要多个标签页之间共享token或者需要在跨域请求时携带token，可以考虑使用localStorage；如果需要更高的安全性和可控制的过期时间，可以考虑使用cookie。

#### cookie的传输过程

当浏览器向服务器发送HTTP请求时，如果请求头中包含Cookie信息，那么这些Cookie数据会被自动加密，并在传输过程中使用HTTPS或SSL/TLS等协议进行加密传输，以确保在传输过程中不会被恶意程序窃取或篡改。

在服务器收到加密的Cookie信息后，会自动解密这些数据，并将其还原成原始的Cookie值，以便服务器能够读取和使用这些Cookie信息。服务器可以使用这些Cookie信息来进行用户认证、记录用户的登录状态等。

需要注意的是，如果使用非加密的HTTP协议传输Cookie信息，那么Cookie信息就会以明文的形式在网络中传输，容易被黑客攻击者窃取或篡改，因此一般情况下，我们建议使用HTTPS或SSL/TLS等安全的协议来保护Cookie信息的安全性。

一般情况下，当服务器向浏览器发送HTTP响应时，响应头中包含的Set-Cookie信息不会被加密，因为这些信息只是服务器发送给浏览器的一组数据，用于告诉浏览器如何设置和管理Cookie。这些数据通常不包含敏感信息，因此不需要进行加密传输。

当浏览器接收到服务器发送的Set-Cookie信息时，浏览器会根据这些信息自动设置和管理Cookie。如果这些Cookie包含敏感信息，例如用户的认证信息等，那么服务器通常会要求使用HTTPS或SSL/TLS等加密协议来传输HTTP响应，以确保Cookie信息在传输过程中不会被窃取或篡改。

需要注意的是，如果在使用HTTP协议传输HTTP响应时，服务器返回的Set-Cookie信息将会以明文的形式在网络中传输，容易被黑客攻击者窃取或篡改。因此，为了保护Cookie信息的安全性，我们建议在使用Cookie时，使用HTTPS或SSL/TLS等安全的协议来保护HTTP请求和响应的安全性。

#### Token 可以存放在 Cookie 和 Local Storage 中，它们各有不同的用途和安全考虑：

1. Cookie：
   - 优点：每次请求都会携带，不需要额外的HTTP请求头。
   - 缺点：不能跨域（即从一个域名到另一个域名的请求）。
   - 安全措施：可以使用 `httponly` 来防止JavaScript读取；可以使用 `secure` 来确保只有HTTPS连接才能传输数据。
   - 可能的安全风险：容易受到CSRF（Cross Site Request Forgery）攻击，因为Token可能被用于未经授权的操作。
2. Local Storage：
   - 优点：持久化存储，不会随着浏览器窗口的关闭而消失。
   - 缺点：每次请求都需要重新获取，需要额外的HTTP请求头。
   - 安全措施：虽然不容易受到XSS（Cross Site Scripting）攻击，但如果多个第三方JS库被恶意利用，仍然存在一定的安全隐患。

综上所述，选择将Token存放在Cookie还是Local Storage取决于具体的应用场景和对安全性的需求。如果需要在不跨域的情况下快速传递Token，那么Cookie可能是更好的选择；如果需要持久化的存储并且不介意每次请求都带上一些额外开销，那么Local Storage可能更适合。同时，为了提高安全性，应该结合使用`httponly`和`secure`属性以及适当的加密技术来保护Token



### Object.assign把所有api方法都放在一个对象，vue页面引用，可能有什么问题

#### chatGPT

将所有的 API 方法都放在一个对象中，然后在 Vue 页面中引用可能会引发一些问题。以下是其中几个可能的问题：

1. 命名冲突：如果多个 API 方法具有相同的名称，在引入时可能会导致命名冲突并出现不可预料的结果。

2. 组件重复渲染：如果每个组件都引入了完整的 API 对象，而不仅仅是所需的方法，可能会导致组件重复渲染，从而影响性能。

3. 难以维护和扩展：当所有的 API 方法都放在一个对象中时，代码的组织和维护可能会变得困难。此外，当需要添加新的 API 方法时，也是一个挑战，因为需要修改该对象。

为了解决这些潜在问题，可以考虑以下几点：

1. 模块化：将不同的 API 方法分别封装到独立的模块中，并根据功能和业务逻辑进行合理的组织。这样可以避免命名冲突，并允许按需引入和使用。

2. Mixin：通过使用 Vue 的 Mixin 功能，可以将 API 方法适当地混入不同的组件中，以提供所需的功能。这样可以避免引入未使用的方法和组件重复渲染的问题。

3. 插件：如果有多个 Vue 页面需要使用相同的 API 方法，可以将这些方法封装为一个插件，并在需要的地方进行安装。这样可以避免重复的代码和维护繁琐的更新。

总的来说，将所有的 API 方法都放在一个对象中并不是一个推荐的做法。最好的方式是根据实际需求进行合理的模块化和组织，以提高代码的可读性、可维护性和扩展性。

#### 文心一言

`Object.assign()` 是 JavaScript 中的一个方法，用于将所有可枚举属性的值从一个或多个源对象复制到目标对象。它会返回目标对象。

如果你将所有的 API 方法都放在一个对象上，然后在 Vue 页面中引用这个对象，可能会出现以下问题：

1. **命名冲突**：如果你的 API 方法名称与其他库或组件的名称冲突，可能会导致运行时错误或不可预测的行为。
2. **可维护性**：随着 API 的增长，整个对象会变得越来越庞大和复杂，这使得代码更难维护和理解。
3. **作用域问题**：如果所有的 API 方法都在同一个对象上，那么它们的作用域将是共享的。这可能会导致意想不到的副作用或覆盖其他方法的行为。
4. **性能问题**：每次使用 `Object.assign()` 时，它都会遍历源对象的所有属性并将其复制到目标对象上。这在性能上可能是一个瓶颈，尤其是在处理大型对象或频繁执行此操作时。
5. **缺乏模块化**：在现代 JavaScript 和 Vue 开发中，通常推荐使用模块化方法来组织代码，这样可以更好地隔离不同部分的功能，提高代码的可重用性和可维护性。
6. **不易于测试**：如果所有的 API 方法都放在一个对象上，那么对单个方法的单元测试会变得更加困难，因为你需要测试整个对象的状态和行为。
7. **不支持链式调用**：如果 API 设计为链式调用（例如 `api.method1().method2()`），那么将所有方法放在一个对象上可能会导致这种设计变得不切实际或难以实现。

为了解决上述问题，更好的做法是将每个 API 方法放在单独的模块或组件中，这样可以更好地组织代码、提高可维护性和可测试性。



### 每个组件引用了一个api文件，该api文件引用了很多对象，使用Object.assign()把其他对象综合为一个对象，有什么性能问题

#### chatGPT

使用 Object.assign() 将多个对象合并为一个对象可能会引发一些性能问题。以下是其中几个可能的问题：

1. 遍历和复制：Object.assign() 在合并对象时需要遍历每个属性，并将其复制到目标对象中。如果合并的对象很大或者嵌套层级较深，这个过程可能会消耗较多的时间和内存。

2. 对象创建：合并对象可能会导致新的对象的创建，特别是在合并的对象数量较多时。这会增加内存的使用和垃圾回收的工作量。

3. 响应式更新：如果合并的对象用于 Vue 组件的 data 或 computed 属性，每次合并都会触发组件的响应式更新机制，可能导致不必要的重绘和性能损耗。

为了解决这些潜在的性能问题，可以考虑以下几点：

1. 只合并必要的对象：仅将必要的对象属性合并到目标对象中，避免合并大量无用的属性，以减少遍历、复制和对象创建的成本。

2. 缓存合并结果：如果合并的对象是不变的，可以将合并结果缓存起来，避免重复的合并操作，提高性能。

3. 惰性加载或异步加载：如果合并的对象是在组件使用时才需要的，可以考虑将其惰性加载或者异步加载，以减少初始加载时的性能开销。

总的来说，使用 Object.assign() 合并多个对象可能会引发一些性能问题，特别是对象数量较多或者合并的对象比较复杂时。在实际使用中，需要注意合并的对象是否必要、是否会频繁变动，以及合并操作对性能的影响，从而采取相应的优化策略。

#### 文心一言

使用 `Object.assign()` 将多个对象合并为一个对象可能会导致以下性能问题：

1. **深度复制**：`Object.assign()` 执行的是浅复制，而不是深复制。这意味着如果源对象的属性值是引用类型（例如对象或数组），那么合并后的对象将共享这些属性值的引用，而不是创建新的副本。这可能导致意外的行为和难以调试的问题，特别是在处理复杂对象或深层嵌套的对象时。
2. **性能开销**：`Object.assign()` 需要遍历源对象的所有属性并将其复制到目标对象上。如果源对象包含大量的属性或深层嵌套的对象，这可能会导致性能瓶颈。在处理大量数据或频繁执行此操作时，这种性能开销可能会变得显著。
3. **内存占用**：如果使用 `Object.assign()` 将大量对象合并为一个对象，可能会导致内存占用增加。这可能会影响应用程序的性能和响应能力。
4. **不可预测的行为**：由于 `Object.assign()` 是浅复制，因此它不会处理源对象的原型链或其他继承关系。这可能导致合并后的对象具有不可预测的行为，特别是当涉及到原型链和继承时。

为了解决这些问题，你可以考虑使用其他方法来组织和引用 API 对象，例如使用模块化模式或构造函数。这些方法可以更好地控制对象的创建和引用，并提供更好的性能和可预测的行为。
