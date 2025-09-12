---
title: ElementUI
date: 2024-04-28 11:11:11
categories: 
- 前端问题
tags:
- 组件库
- element
---

### element-ui封装Loading公共方法

注册到vue实例上，全屏或者局部页面都可以使用，项目文件引用方便一点

要将 `Loading` 功能封装成公共方法并注册到 Vue 实例上，这样可以在任何组件中通过 `this.$loading.show()` 和 `this.$loading.hide()` 来方便地调用。以下是具体实现步骤：

#### 步骤 1: 创建公共方法

首先，在你的项目中创建一个工具文件夹（如果还没有的话），比如叫做 `utils`，然后在这个文件夹下创建一个名为 `loading.js` 的文件。

```javascript
import \\{ Loading \\} from 'element-ui';

let loadingInstance = null; // 用于存储全局loading实例
let timeoutId = null; // 用于存储定时器ID

const showLoading = (options) => \\{
  if (loadingInstance) return; // 如果已经有loading实例，则不再创建新的
  const defaultOptions = \\{
    lock: true,
    text: '拼命加载中...',
    spinner: 'el-icon-loading',
    background: 'rgba(0, 0, 0, 0.7)',
    ...options, // 允许传递自定义选项覆盖默认值
  \\};

  loadingInstance = Loading.service(defaultOptions);

  // 设置30秒后自动关闭加载提示
  timeoutId = setTimeout(() => \\{
    hideLoading();
  \\}, 30000); // 30000毫秒 = 30秒
\\};

const hideLoading = () => \\{
  if (loadingInstance) \\{
    loadingInstance.close();
    loadingInstance = null;
  \\}

  // 清除定时器
  if (timeoutId) \\{
    clearTimeout(timeoutId);
    timeoutId = null;
  \\}
\\};

export default \\{
  show: showLoading,
  hide: hideLoading
\\};
```

这段代码定义了一个对象，其中包含 `show` 和 `hide` 方法，分别用于显示和隐藏加载动画。

#### 步骤 2: 注册到 Vue 实例

接下来，你需要在 Vue 应用的入口文件（通常是 `main.js` 或 `app.js`）中导入这个模块，并将其挂载到 Vue 的原型上，以便在所有组件中都可以访问。

```javascript
// main.js 或 app.js
import Vue from 'vue';
import App from './App.vue';
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';
import loading from '@/utils/loading'; // 调整路径以匹配你的项目结构

Vue.use(ElementUI);

// 将loading方法挂载到Vue原型上
Vue.prototype.$loading = loading;

new Vue(\\{
  render: h => h(App),
\\}).$mount('#app');
```

#### 步骤 3: 在组件中使用

现在你可以在任何 Vue 组件中直接使用 `this.$loading.show()` 和 `this.$loading.hide()` 来控制加载状态了。

##### 示例：全屏加载

```vue
<template>
  <div>
    <button @click="startLoading">开始加载</button>
    <button @click="endLoading">结束加载</button>
  </div>
</template>

<script>
export default \\{
  methods: \\{
    startLoading() \\{
      this.$loading.show();  // 显示全屏loading
    \\},
    endLoading() \\{
      this.$loading.hide();  // 隐藏loading
    \\}
  \\}
\\}
</script>
```

##### 示例：局部加载

```vue
<template>
  <div>
    <div ref="content">
      <!-- 这里是内容 -->
    </div>
    <button @click="startLocalLoading">开始局部加载</button>
    <button @click="endLocalLoading">结束局部加载</button>
  </div>
</template>

<script>
export default \\{
  methods: \\{
    startLocalLoading() \\{
      // 显示局部loading
      this.$loading.show(\\{ target: this.$refs.content \\});
      this.$loading.show(\\{ target: '.groupForm' \\});
    \\},
    endLocalLoading() \\{
      this.$loading.hide();  // 隐藏loading
    \\}
  \\}
\\}
</script>
```

通过这种方式，你可以非常方便地在整个项目中管理和使用加载效果，无论是全屏还是局部页面。这种方法不仅提高了代码的可维护性，也使得加载功能的调用更加简洁和一致。



### 当前使用的vue2.7的`<script lang="ts" setup>`写法，组件中怎么使用

是的，你可以使用解构赋值来简化代码，直接从 `getCurrentInstance` 返回的对象中提取 `proxy` 的 `$loading` 方法。这样可以使代码更加简洁和易读。以下是修改后的示例：

#### 组件代码

```vue
<template>
  <div>
    <button @click="startLoading">开始加载</button>
    <button @click="endLoading">结束加载</button>

    <div ref="content">
      <!-- 这里是内容 -->
    </div>
    <button @click="startLocalLoading">开始局部加载</button>
    <button @click="endLocalLoading">结束局部加载</button>
  </div>
</template>

<script lang="ts">
import \\{ defineComponent, ref, onMounted, getCurrentInstance \\} from '@vue/composition-api';

export default defineComponent(\\{
  name: 'MyComponent',
  setup() \\{
    const content = ref(null);
    
    // 使用解构赋值直接获取 $loading
    const \\{ proxy: \\{ $loading \\} \\} = getCurrentInstance();

    const startLoading = () => \\{
      $loading.show();  // 显示全屏loading
    \\};

    const endLoading = () => \\{
      $loading.hide();  // 隐藏loading
    \\};

    const startLocalLoading = () => \\{
      // 显示局部loading
      $loading.show(\\{ target: content.value \\});
      $loading.show(\\{ target: '.xxxx' \\});
    \\};

    const endLocalLoading = () => \\{
      $loading.hide();  // 隐藏loading
    \\};

    return \\{
      content,
      startLoading,
      endLoading,
      startLocalLoading,
      endLocalLoading
    \\};
  \\}
\\});
</script>
```

#### 解释

- **`getCurrentInstance`**: 获取当前组件的实例。
- **解构赋值**: 通过解构赋值直接从 `getCurrentInstance` 返回的对象中提取 `proxy` 的 `$loading` 方法。

这种方式不仅使代码更加简洁，而且避免了重复访问 `proxy` 对象。你可以在 `setup` 函数中直接使用 `$loading` 方法，而不需要每次都通过 `proxy` 来访问。

这种方法既简单又直接，同时保持了代码的可读性和类型安全性。希望这能满足你的需求！如果还有其他问题或需要进一步的帮助，请告诉我。

#### 其他方法

```
<template>
  <div>
    <button @click="startLoading">开始加载</button>
    <button @click="endLoading">结束加载</button>

    <div ref="content">
      <!-- 这里是内容 -->
    </div>
    <button @click="startLocalLoading">开始局部加载</button>
    <button @click="endLocalLoading">结束局部加载</button>
  </div>
</template>

<script lang="ts">
import \\{ defineComponent, ref, onMounted \\} from '@vue/composition-api';

export default defineComponent(\\{
  name: 'MyComponent',
  setup() \\{
    const content = ref(null);

    const startLoading = () => \\{
      (this as any).$loading.show();  // 显示全屏loading
    \\};

    const endLoading = () => \\{
      (this as any).$loading.hide();  // 隐藏loading
    \\};

    const startLocalLoading = () => \\{
      (this as any).$loading.show(\\{ target: content.value \\});  // 显示局部loading
    \\};

    const endLocalLoading = () => \\{
      (this as any).$loading.hide();  // 隐藏loading
    \\};

    return \\{
      content,
      startLoading,
      endLoading,
      startLocalLoading,
      endLocalLoading
    \\};
  \\}
\\});
</script>
```

- **`defineComponent`**: 用于定义一个 Vue 组件。
- **`ref`**: 用于创建一个响应式的引用，这里用来绑定到模板中的 DOM 元素。
- **`(this as any).$loading`**: 由于 `setup` 函数内部没有 `this` 上下文，我们需要通过类型断言来访问 Vue 实例上的 `$loading` 方法。

这种方法允许你在 Vue 2.7 中使用 Composition API，并且可以方便地调用全局的 `$loading` 方法。这样做的好处是代码更加模块化和可复用。





### 嵌套的 Dialog

如果需要在一个 Dialog 内部嵌套另一个 Dialog，需要使用 `append-to-body` 属性。

**不使用的话有遮罩bug，需要多点击一次。**

点击打开外层 Dialog

正常情况下，我们不建议使用嵌套的 Dialog，如果需要在页面上同时显示多个 Dialog，可以将它们平级放置。对于确实需要嵌套 Dialog 的场景，我们提供了`append-to-body`属性。将内层 Dialog 的该属性设置为 true，它就会插入至 body 元素上，从而保证内外层 Dialog 和遮罩层级关系的正确。

```
<template>
  <el-button type="text" @click="outerVisible = true">点击打开外层 Dialog</el-button>
  
  <el-dialog title="外层 Dialog" :visible.sync="outerVisible">
    <el-dialog
      width="30\\%"
      title="内层 Dialog"
      :visible.sync="innerVisible"
      append-to-body>
    </el-dialog>
    <div slot="footer" class="dialog-footer">
      <el-button @click="outerVisible = false">取 消</el-button>
      <el-button type="primary" @click="innerVisible = true">打开内层 Dialog</el-button>
    </div>
  </el-dialog>
</template>

<script>
  export default \\{
    data() \\{
      return \\{
        outerVisible: false,
        innerVisible: false
      \\};
    \\}
  \\}
</script>
```



### el-cascader组件宽度限制

element里面的`el-cascader`组件宽度会根据里面的数据自动延伸，也就导致了一些超出屏幕的情况

```
<style lang="scss">
// 限制级联选择器最大宽度
.el-cascader-menu \\{
  max-width: 180px;
\\}
</style>
```

不能写在scoped里面，会失效

有部分内容被遮挡，这个时候就需要我们的另一个组件上场了——`el-tooltip`
咱们使用`el-cascader`里面的插槽，对文本直接进行处理，限制长度大于12就有内容提示。 

```
<el-cascader
 v-model="value"
 :options="list">
   <template slot-scope="\\{ data \\}">
     <el-tooltip
       :disabled="data.label.length < 12"
       class="item"
       effect="dark"
       :content="data.label"
       placement="right"
     >
      <span>\\\{\\\{ data.label\\\}\\\} }}</span>
    </el-tooltip>
  </template>
</el-cascader>
```

注意：有时候会导致提示组件定位不准确，需要手动调整！ 



### Element-UI Popconfirm组件的确认事件

文档事件名有误：confirm应为onConfirm

```
<el-popconfirm title="您确定需要取消活动吗？" @onConfirm="cancelProductCoupon(scope.row.pid)">
	<el-link slot="reference" type="danger">取消活动</el-link>
</el-popconfirm>
```



### 输入框随字数变化宽度及输入字符超出提示

```
<el-input :style="\\{width:inputAuto(sanInputValue)\\}" v-model="sanInputValue"></el-input>
computed: \\{
			// 输入框随字数变化宽度
			inputAuto() \\{
				return function(value) \\{
					if (value) \\{
						return String(value).length * 12 + 50 + 'px'
					\\} else \\{
						return '50px'
					\\}
				\\}
			\\}
		\\},
watch: \\{
	// 输入字符超出提示
	sanInputValue: function(newVal) \\{
				if (newVal.length > 15) \\{
					this.sanInputValue = this.sanInputValue.slice(0, 15)
					this.$message.warning('子规格字符不能超过15个')
				\\}
			\\},
\\},
```



### 提交按钮禁用

```
<el-button :disabled="!followText.trim()"
          type="primary"
          @click="submit">确 定</el-button>
```



### element-ui预览大图的点击方法

```
// 保证ref唯一
<el-image :src="scope.row.img" :preview-src-list="[scope.row.img]" :ref="'img'+scope.row.index"></el-image>

<span @click="handlePreview(scope.row.index)">
	<i class="el-icon-zoom-in"></i>
</span>

// 关键点在于模拟点击事件的this.$refs.preview.clickHandler()该方法执行，在官网没写出来这个方法
handlePreview(index) \\{
	// console.log(this.$refs['img' + index])
	this.$refs['img' + index].clickHandler()
\\},
```



### 响应式布局项目修改el-header与el-footer的高度值

```
.el-footer \\{
	height: auto !important;
\\}
```



### element-ui表头居中header-align设置了不生效

建议使用css控制

```
// 表头
::v-deep .el-table__header tr,
  .el-table__header th \\{
    text-align: left;
  \\}
```

也可以使用style

```
:header-cell-style="\\{textAlign: 'center'\\}"  //表头居中
```



### vue给按钮或者输入框添加回车事件

#### 按钮

```vue
<Button type="primary" @click="handleSearch" @keyup.enter="enterSearch">搜索</Button>

created () \\{
    //    一定要在create里面执行一下写的回车事件enterSearch(),否则会执行不了
       this.enterSearch()
   \\},
   methods: \\{
        //条件搜索
        handleSearch() \\{
            this.pageNumber = 1;
            this.getList()
        \\},
        //回车搜索
        enterSearch()\\{
            document.onkeydown = e =>\\{
                //13表示回车键，baseURI是当前页面的地址，为了更严谨，也可以加别的，可以打印e看一下
                if (e.keyCode === 13 && e.target.baseURI.match(/freshmanage/)) \\{
                //回车后执行搜索方法
                    this.handleSearch()
                \\}
            \\}
        \\}
    \\}
```

#### 输入框

按下回车时触发搜索功能，你可以给 组件添加 `@keyup.enter.native` 事件监听。

```vue
<el-form :inline="true" @submit.native.prevent>
    <el-form-item>
        <el-input 
            v-model.trim="keywords" 
            size="small" 
            style="width: 300px" 
            placeholder="请输入模板key、内容或描述"
            clearable
            @keyup.enter.native="search" <!-- 添加回车事件监听 -->
        ></el-input>
    </el-form-item>
    <el-form-item style="margin-top: 5px;">
        <el-button type="primary" size="small" @click="search()">查询</el-button>
    </el-form-item>
    <el-button type="primary" icon="el-icon-plus" size="small" @click="addShow()">添加</el-button>
</el-form>
```

**关键改动说明：**

1. `@keyup.enter.native="search"`
   - 当用户按下回车键时，直接调用 `search` 方法。
   - `.native` 是必要的，因为需要监听原生 DOM 事件（Element UI 组件封装了原生输入框）。

**说明：**

- 输入框的键盘事件通过键修饰符 `.enter` 确保仅在按下回车时触发。
- `.native` 确保监听原生事件（关键步骤，避免因组件封装导致事件失效）。

这种方法无需改动表单或其他按钮逻辑，仅需在输入框绑定回车事件即可实现搜索功能。



### ElementUI、iview中input回车触发页面刷新问题及其解决方法

在日常的开发过程中，你可能会遇到一个问题：在ElementUI的el-form表单中，如果只存在一个el-input输入框，当你输入值后按下回车，页面会发生刷新。

这是因为当form元素中只有一个输入框时，按下回车将触发表单的默认提交事件，这是W3C标准的规定。form表单提交的时候会刷新页面。

### 解决方案：

1. 在form表单里禁止自动提交
2. 在页面全局禁止键盘按下enter事件
3. input禁止键盘按下enter事件
4. vue项目中可在form标签上加上@submit.native.prevent
5. 直接去除掉form表单，当然这是最简单粗暴的方法。
6. 如果一个input会自动提交，那么比较容易想到的是再加一个input。值得注意的是 这里的input不能设置type为hidden，这样一样是不生效的，form一样会认为只有一个input。

#### 解决方法：

ElementUI也给出了解决方法。如果你希望阻止这一默认行为，可以**在<el-form>标签上添加@submit.native.prevent**

例如：

```
<el-form 
  :model="form" 
  ref="form" 
  label-width="200px" 
  class="form" 
  @submit.native.prevent
>
  <el-form-item
    label="姓名"
    prop="name"
  >
    <el-input v-model.number="form.name"></el-input>
  </el-form-item>
  <el-form-item>
    <el-button type="primary" @click="submit('form')">提交</el-button>
    <el-button @click="reset('form')">重置</el-button>
  </el-form-item>
</el-form>
```

 然而，上述方法只是阻止了默认行为，如果你仍需要回车来提交表单，你可以通过以下方式解决： 

```
<el-form 
  :model="form" 
  ref="form" 
  label-width="200px" 
  class="form" 
  @submit.native.prevent="() => submit('form')"
>
  <el-form-item
    label="姓名"
    prop="name"
  >
    <el-input v-model.number="form.name"></el-input>
  </el-form-item>
  <el-form-item>
    <el-button type="primary" native-type="submit">提交</el-button>
    <el-button @click="reset('form')">重置</el-button>
  </el-form-item>
</el-form>
```

请注意以下几点：

- 确保使用 @submit.native.prevent 阻止原生事件，执行方法为搜索按钮按click事件
- 搜索按钮需要被包裹在 el-form 中
- 移除搜索按钮的click事件
- 确保增加 native-type="submit" 属性

此外，原生的form表单的单input和form包裹el-input回车刷新的问题也可以解决，有以下几种方法：

1. 在form表单内再增加一个隐藏的input框，可以通过hidden定义隐藏的输入字段，或者通过CSS样式进行隐藏。

2. 去掉输入框的回车事件（根据需求来定，有的需要回车事件提交表单来查询或者执行其他操作则该方法不适用）。

3. 阻止表单默认提交事件。例如，使用onsubmit句柄返回false来阻止原生form内的input的默认提交事件。



### el-input的自动填充密码怎么禁止？

在 Vue 项目中，如果你想要禁用 `el-input` 组件的密码自动填充功能，可以通过修改输入框的一些属性来实现。Element UI 的 `el-input` 组件本身并没有直接提供禁用自动填充的选项，但是你可以通过设置 HTML 的原生属性来达到这个目的。

以下是一个简单的示例，展示如何在 Vue 2 中使用 Element UI 的 `el-input` 组件，并禁用密码自动填充：

```html
<template>
  <el-input
    type="password"
    v-model="password"
    :autofill="false"
    placeholder="请输入密码">
  </el-input>
</template>

<script>
export default \\{
  data() \\{
    return \\{
      password: ''
    \\}
  \\}
\\}
</script>
```

这里需要注意的是，`:autofill="false"` 这样的写法实际上并不会生效，因为 `autofill` 不是 `el-input` 组件的有效属性。你需要使用 HTML5 的 `autocomplete` 属性来控制浏览器的自动填充行为。

正确的做法是在 `el-input` 的标签上添加 `autocomplete` 属性，并将其值设置为 `"off"` 或者 `"new-password"`（如果这是一个注册表单中的密码字段）。

```html
<template>
  <el-input
    type="password"
    v-model="password"
    :autocomplete="false"  <!-- 注意这里 -->
    placeholder="请输入密码">
  </el-input>
</template>

<script>
export default \\{
  data() \\{
    return \\{
      password: ''
    \\}
  \\}
\\}
</script>
```

更好的做法是使用 `autocomplete="new-password"`，这样浏览器会知道这是一个新的密码字段，不应该从历史记录中填充。

```html
<template>
  <el-input
    type="password"
    v-model="password"
    autocomplete="new-password"
    placeholder="请输入密码">
  </el-input>
</template>

<script>
export default \\{
  data() \\{
    return \\{
      password: ''
    \\}
  \\}
\\}
</script>
```

这样做可以确保浏览器不会尝试自动填充该密码字段。



### 日期范围选择器禁用

src\mixins\pickerOptions.js

```js
export default \\{
  data() \\{
    return \\{
      startDate: null, // 已选择的开始时间
      // 一个月范围（没有禁用今天之后的）
      pickerOptions: \\{
        onPick: (\\{ maxDate, minDate \\}) => \\{
          this.startDate = minDate.getTime()
          if (maxDate) \\{
            this.startDate = null
          \\}
        \\},
        disabledDate: (time) => \\{
          const choiceDateTime = new Date(this.startDate).getTime()
          const minTime = new Date(choiceDateTime).setMonth(
            new Date(choiceDateTime).getMonth() - 1
          )
          const maxTime = new Date(choiceDateTime).setMonth(
            new Date(choiceDateTime).getMonth() + 1
          )
          const min = minTime
          const newDate = new Date(new Date().toLocaleDateString()).getTime()
          const max = newDate < maxTime ? newDate : maxTime
          // 如果已经选中一个日期 则 返回可选日期为 【当前日期一个月前～当前日期一个月后】和【当前日期以前日期】的交集时间范围
          if (this.startDate) \\{
            return time.getTime() < min || time.getTime() > maxTime
          \\}

          // return time.getTime() > Date.now()
        \\},
      \\},
      // 只能选择今天及之前的六个月范围
      preSixMonths: \\{
        onPick: (\\{ maxDate, minDate \\}) => \\{
          this.startDate = minDate.getTime()
          if (maxDate) \\{
            // 清除开始时间记录
            this.startDate = null
          \\}
        \\},
        disabledDate: (time) => \\{
          const today = new Date()
          if (this.startDate) \\{
            const choiceDate = new Date(this.startDate)
            const minTime = new Date(
              choiceDate.getFullYear(),
              choiceDate.getMonth() - 6,
              choiceDate.getDate()
            )
            const maxTime = new Date(
              choiceDate.getFullYear(),
              choiceDate.getMonth() + 6,
              choiceDate.getDate()
            )

            // 禁止选择：前后六个月范围之外 和 今天之后的日期
             return (
              time.getTime() < minTime.getTime() ||
              time.getTime() > maxTime.getTime() ||
              time.getTime() > today.getTime()
            )
          \\} else \\{
            // 如果没有选择开始时间，禁止选择今天之后的日期
            return time.getTime() > today.getTime()
          \\}
        \\},
      \\},
    \\}
  \\},
\\}
```

src\mixins\index.js

```js
import pickerOptions from './pickerOptions'

export \\{
  pickerOptions // 日期选择器配置项
\\}
```

组件js使用

```
import \\{ pickerOptions \\} from '@/mixins/index'

mixins: [pickerOptions],

created() \\{
    // 此时混入数据已可用
    this.searchOption.list[0].pickerOptions = this.preSixMonths
\\},
```

组件html使用

```
<el-date-picker v-model="form.dateArr1"
    value-format="yyyy-MM-dd"
    type="daterange"
    size="small"
    range-separator="至"
    start-placeholder="触发开始时间"
    end-placeholder="触发结束时间"
    :picker-options="preSixMonths"
    :editable="false"
    unlink-panels
    class="date-picker-w280">
</el-date-picker>

import \\{ pickerOptions \\} from '@/mixins/index'

mixins: [pickerOptions],
```



### 混入引用问题

在data中写了pickerOptions: this.preSixMonths,

已经正确引用了import \\{ pickerOptions \\} from '@/mixins/index'中的data:preSixMonths

可以打印出来this.preSixMonths，为什么pickerOptions还是undefined？

出现该问题的原因可能如下：

1. **混入未正确应用**：确保组件中通过 `mixins: [pickerOptions]` 引入混入对象。若未在组件选项中添加，`preSixMonths` 将不存在于实例中。

2. **初始化时机问题**：在组件的 `data()` 函数中直接访问 `this.preSixMonths` 时，混入的 `data` 可能尚未合并到当前实例。Vue 的合并策略会导致混入的 `data` 先于组件自身 `data` 初始化，但在组件 `data` 函数中通过 `this` 访问仍可能为 `undefined`。

3. **混入导出格式错误**：确保混入对象包含 `data` 函数返回 `preSixMonths`，例如：

   ```js
   // @/mixins/index.js
   export const pickerOptions = \\{
     data() \\{
       return \\{
         preSixMonths: \\{ /* 配置数据 */ \\}
       \\};
     \\}
   \\};
   ```

**解决方案**：

1. **在组件中正确应用混入**：

   ```js
   import \\{ pickerOptions \\} from '@/mixins/index';
   export default \\{
     mixins: [pickerOptions], // 确保混入被添加到数组
     // 其他选项...
   \\};
   ```

2. **避免在 `data` 中引用混入属性**，改用 **计算属性** 或 **生命周期钩子**：

   ```js
   // 使用计算属性
   computed: \\{
     pickerOptions() \\{
       return this.preSixMonths; // 响应式获取混入数据
     \\}
   \\}
   
   // 或在 created 中赋值
   data() \\{
     return \\{
       pickerOptions: null
     \\};
   \\},
   created() \\{
     // 此时混入数据已可用
     this.pickerOptions = this.preSixMonths;
   \\}
   ```

3. **验证混入数据是否正确**：在 `created` 钩子中打印 `this.preSixMonths`，确保其存在且正确。

**总结**：问题源于在组件 `data` 初始化阶段过早访问混入数据。通过调整赋值时机或使用计算属性可确保正确引用。同时检查混入是否正确应用及导出格式。