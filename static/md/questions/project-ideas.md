---
title: 项目思路
date: 2022-05-22 22:40:25
categories: 
- 前端问题
tags:
- vue
- 前端
---

### 域名1获取到token，跳转到域名2实现自动登录，写出思路和完整代码 

要实现域名1获取到token，然后跳转到域名2实现自动登录，可以使用以下思路和代码实现：

1. 在域名1上，用户登录成功后生成一个包含token的URL，并将该URL传递给域名2。
2. 在域名2上，接收到包含token的URL后，提取出token的值。
3. 在域名2上，发送一个POST请求到域名1的某个登录验证接口，将token作为参数，并且将withCredentials设置为true以允许跨域携带凭证（例如cookies）。
4. 在域名1的登录验证接口上，验证token的合法性，并通过设置response header的Access-Control-Allow-Origin为域名2，允许来自域名2的跨域请求。
5. 在域名2上，根据返回的响应结果进行相应的操作，例如登录成功则跳转到用户页面，登录失败则返回错误提示。

下面是一个可能的代码示例：

在域名1上的页面：
```javascript
// 用户登录成功后生成包含token的URL
var token = 'abc123'; // 假设已经获取到了token
var redirectURL = 'http://domain2.com/login?token=' + token;

// 域名1跳转到域名2
window.location.href = redirectURL;
```

在域名2上的登录页面：

vue

```
		// 带token跳转过来自动登录
        async tokenLogin() \\{
            console.log(this.$route.query)
            let access_token = this.$route.query.access_token
            if (access_token) \\{
                utils.saveLogin(\\{ access_token \\})
                await this.dispathAuthorCode()
                this.$router.push(\\{
                    name: 'app'
                \\})
            \\}
        \\}
```

HTML

```javascript
// 提取URL中的token值
var tokenIndex = location.href.indexOf('?token=') + '?token='.length;
var token = location.href.substring(tokenIndex);

// 发送跨域POST请求到域名1的登录验证接口
var xhr = new XMLHttpRequest();
xhr.withCredentials = true;
xhr.open('POST', 'http://domain1.com/login-verify', true);
xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
xhr.onreadystatechange = function() \\{
    if (xhr.readyState === 4 && xhr.status === 200) \\{
        var response = JSON.parse(xhr.responseText);
        // 根据响应结果进行相应的操作，例如登录成功则跳转到用户页面
        if (response.status === 'success') \\{
            window.location.href = 'http://domain2.com/user'; // 假设用户页面URL为http://domain2.com/user
        \\} else \\{
            alert('登录失败：' + response.message);
        \\}
    \\}
\\};

// 发送POST请求，将token作为参数
xhr.send('token=' + token);
```

在域名1的登录验证接口上，根据具体的后端语言和框架来实现验证token合法性的逻辑，并设置response header的Access-Control-Allow-Origin为域名2。例如，在PHP中可以这样实现：

```php
<?php
header('Access-Control-Allow-Origin: http://domain2.com');
$response = array();
$token = $_POST['token'];

// 验证token的合法性，在此处根据具体需求编写验证
```



### file_type是数组[1,2]，代表选中两个按钮，这两个按钮可以多选，请用vue写出按钮点击公用事件（两个按钮最少选中一个，只剩下一个选中按钮时禁止取消） 

好的，下面是根据您的要求使用 Vue 来实现按钮点击公用事件的代码：

```html
<template>
  <div>
    <button v-for="button in buttons" :key="button" @click="buttonClick(button)" :class="\\{ active: selectedButtons.includes(button) \\}">
      Button \\\{\\\{ button\\\}\\\} }}
    </button>
  </div>
</template>

<script>
export default \\{
  data() \\{
    return \\{
      buttons: [1, 2], // 可选按钮列表
      selectedButtons: [] // 当前选中的按钮列表
    \\}
  \\},
  methods: \\{
    buttonClick(button) \\{
      // 判断按钮是否已选中
      const selectedIndex = this.selectedButtons.indexOf(button);
      if (selectedIndex > -1) \\{
        // 如果按钮已选中
        if (this.selectedButtons.length === 1) \\{
          // 如果只剩下一个选中按钮，则禁止取消选中
          return;
        \\}
        // 取消选中按钮
        this.selectedButtons.splice(selectedIndex, 1);
      \\} else \\{
        // 如果按钮未选中
        // 添加选中按钮
        this.selectedButtons.push(button);
      \\}
    \\}
  \\},
  mounted() \\{
    // 默认选中第一个按钮
    this.selectedButtons.push(this.buttons[0]);
  \\}
\\}
</script>
```

在上述代码中，我使用了 `v-for` 指令来循环渲染按钮，通过 给每个按钮绑定 `@click` 事件监听点击事件。

在 `buttonClick` 方法内部，首先判断按钮是否已选中。如果已选中，再判断是否只剩下一个选中按钮，如果是，则禁止取消选中。如果按钮未选中，则将其添加到 `selectedButtons` 中。

启动后，默认选中了第一个按钮。

这样，就实现了通过公用事件控制多个按钮的选中状态，并满足了最少选中一个按钮、只剩下一个选中按钮时禁止取消的需求。



### 有个key每天有一定使用额度次数，因为是不同用户在使用，无法计数，只能通过接口报错知道key用完了，需要用另一个key来替换，请用vue实现这个逻辑。 

```
// 腾讯地图接口失败处理
		tMapFail(err) \\{
			// 模拟失败的测试数据
			// err.status = 121
			// err.message = '此key每日调用量已达到上限'
			// err.request_id = err.request_id

			console.log('腾讯地图接口失败', err);
			if (err.status === 121) \\{
				uni.showToast(\\{
					title: '地图key每日上限，请退出此页面重试',
					icon: 'none',
					duration: 2500
				\\})
				const setTime = Utils.formatDate(new Date())
				console.log(setTime);
				// 如果接口报错达到上限，启用备用的key（下次onLaunch，如果超过一天，会使用原始的key）
				this.$store.commit('setMap', \\{
					key: Config.backupMapKey,
					keyName: Config.mapKeyName,
					setTime
				\\})
				this.newMap()
			\\}
		\\}
```

onLaunch重置

```
// 设置地图信息
		setMapInfo(context) \\{
			const setTime = Utils.getDateFromTimeString(this.state.login.map.setTime)
			const time = new Date()
			let day = (time - setTime) / (1000 * 60 * 60 * 24)
			console.log(setTime, time, day)
			// 如果第一次进入 或者 超过一天，使用原始的key
			if (!setTime || day > 1) \\{
				// 保存腾讯地图信息
				context.commit('setMap', \\{
					key: Config.mapKey,
					keyName: Config.mapKeyName,
					setTime: Utils.formatDate(time)
				\\});
			\\}
		\\},
```



### groupListEdit是一个数组列表，点击向下箭头，当前元素移到下一位vue3

在Vue 3中，如果你想实现一个功能，即当用户点击一个元素的向下箭头时，这个元素会与它下面的一个元素交换位置，你可以使用`ref`和`reactive`来创建响应式数据，并且使用方法来处理列表元素的移动。下面是一个示例代码，展示了如何实现这个功能：

```html
<template>
  <div>
    <ul>
      <li v-for="(item, index) in groupListEdit" :key="index" @click="moveDown(index)">
        \\\{\\\{ item\\\}\\\} }} 
        <span class="arrow-down">⬇️</span>
      </li>
    </ul>
  </div>
</template>

<script setup>
import \\{ ref, reactive \\} from 'vue';

// 假设这是你的初始列表
const groupListEdit = reactive(['Item 1', 'Item 2', 'Item 3', 'Item 4']);

// 移动元素到下一个位置的方法
const moveDown = (index) => \\{
  if (index < groupListEdit.length - 1) \\{ // 确保不是最后一个元素
    // 保存当前元素
    const temp = groupListEdit[index];
    // 将当前元素与下一个元素交换位置
    groupListEdit[index] = groupListEdit[index + 1];
    groupListEdit[index + 1] = temp;
  \\}
\\};
</script>

<style scoped>
.arrow-down \\{
  cursor: pointer;
\\}
</style>
```

在这个例子中，`v-for`循环遍历`groupListEdit`数组并为每个元素创建一个列表项。当列表项被点击时，`moveDown`函数会被调用，该函数检查元素是否是数组中的最后一个元素，如果不是，则与下一个元素进行位置交换。

请注意，你可能需要根据你的具体需求调整代码，比如添加边界条件、错误处理或者更复杂的样式和交互。



### 请在app.vue中显示骨架屏

```
<template>
  <!-- 添加路由组件 -->
  <router-view v-slot="\\{ Component \\}">
    <keep-alive include="ClueListFilter">
      <component :is="Component" />
    </keep-alive>
  </router-view>
</template>
```

在 `App.vue` 中显示骨架屏，可以通过条件渲染来实现。你可以添加一个数据属性来控制骨架屏的显示与隐藏，并在 Vue 应用初始化完成之后更新这个属性以移除骨架屏。

下面是一个示例代码，展示如何在 `App.vue` 中加入 `<van-skeleton>` 骨架屏组件，并在应用加载完成后隐藏它：

1. **安装 Vant UI 框架**（如果你还没有安装的话）：
   ```bash
   npm install vant
   ```

2. **在 `main.js` 中引入 Vant 的样式文件**：
   ```javascript
   import 'vant/lib/index.css';
   ```

3. **修改 `App.vue` 文件**，加入骨架屏并使用一个布尔值来控制其显示：

```vue
<template>
  <div id="app">
    <!-- 条件渲染骨架屏 -->
    <van-skeleton title :row="3" v-if="showSkeleton"></van-skeleton>

    <!-- 添加路由组件 -->
    <router-view v-slot="\\{ Component \\}">
      <keep-alive include="ClueListFilter">
        <component :is="Component" />
      </keep-alive>
    </router-view>
  </div>
</template>

<script>
export default \\{
  name: 'App',
  data() \\{
    return \\{
      showSkeleton: true, // 控制骨架屏显示的标志
    \\};
  \\},
  mounted() \\{
    // 当应用挂载后，可以设置一个定时器或监听某个事件来关闭骨架屏
    this.$nextTick(() => \\{
      setTimeout(() => \\{
        this.showSkeleton = false; // 假设异步操作需要1秒
      \\}, 1000); // 这里只是一个示例，实际中可以根据你的逻辑来决定何时关闭骨架屏
    \\});
  \\},
\\};
</script>

<style>
/* 你的样式 */
</style>
```

4. **确保在 `main.js` 中正确创建和挂载应用**：
   ```javascript
   import \\{ createApp \\} from 'vue';
   import App from './App.vue';
   import router from './router'; // 确保你已经配置了路由
   import store from './store'; // 如果有 Vuex 存储

   const app = createApp(App);
   app.use(router);
   app.use(store);
   app.mount('#app');
   ```

在这个例子中，当 `App.vue` 组件被挂载时，`mounted` 生命周期钩子会触发，并且在下一个 DOM 更新周期后通过 `setTimeout` 函数模拟了一个异步操作。一旦该操作完成，`showSkeleton` 就会被设置为 `false`，从而隐藏骨架屏。在实际情况中，你可以根据你的异步操作（比如数据获取、初始化等）来决定何时隐藏骨架屏。



### vue3项目使用vue2写法

在vue3项目中的main.js中

```
instance.config.globalProperties.$isHas = (code) => \\{
    const list = instance.config.globalProperties.$permission || []
    const target = list.find((method) => \\{
      return method.powers === code
    \\})
    return (target && target.select) || false
  \\}
```

这个$isHas在页面中怎么使用，该页面使用了vue2写法（vue3项目）

在 Vue 3 项目中，如果你需要在一个使用了 Vue 2 语法的页面或组件中使用通过 `instance.config.globalProperties` 定义的 `$isHas` 方法，你可以直接像在 Vue 2 中一样访问这个全局属性。Vue 3 的 `config.globalProperties` 使得所有组件实例都可以访问到这些属性，因此你可以在任何组件中直接使用 `this.$isHas`。

可以在你的组件（即使是使用了 Vue 2 语法的组件）中这样使用 `$isHas` 方法：

```vue
<template>
  <div v-if="hasPermission('view')">
    <!-- 只有当用户有查看权限时才显示的内容 -->
  </div>
</template>

<script>
export default \\{
  name: 'YourComponent',
  data() \\{
    return \\{
      // 你的数据
    \\};
  \\},
  computed: \\{
    hasPermission() \\{
      // 使用 this.$isHas 来检查权限
      return (code) => this.$isHas(code);
    \\}
  \\},
  methods: \\{
    someMethod() \\{
      if (this.hasPermission('edit')) \\{
        // 执行某些操作
      \\}
    \\}
  \\}
\\};
</script>
```

在这个例子中，`hasPermission` 是一个计算属性，它返回一个函数，该函数接受一个权限代码作为参数并调用 `this.$isHas` 来检查权限。这种方式可以让你在模板和方法中方便地使用权限检查逻辑。

请注意，尽管你可以使用类似 Vue 2 的写法来编写组件，但最好遵循 Vue 3 的最佳实践，例如使用 Composition API 或 `<script setup>` 等新特性。这将有助于保持代码的一致性和可维护性。



### 点击全选，可能会请求到五千条数据，导致页面非常卡顿，请分析原因并且优化

```
<van-checkbox-group v-model="curSelectList"
        ref="checkRef"
        direction="horizontal"
        @change="onCheckChange">
        <van-checkbox v-for="(item, index) in filterCustomerList"
          :key="item.customerId"
          :name="item.customerId">
          <div :class="[
              'radio-item',
              index === filterCustomerList.length - 1 ? 'no-border' : '',
            ]">
            <van-image width="32"
              height="32"
              :src="getAssets(`components/avatar.png`)"
              lazy-load />
            <div class="customer-name">\\\{\\\{ item.name ||  item.custName || item.nickname\\\}\\\} }}</div>
          </div>
        </van-checkbox>
      </van-checkbox-group>
```

点击全选时，如果请求到五千条数据，会导致页面非常卡顿的原因主要有以下几点：

1. **DOM 元素过多**：五千个 `` 元素同时渲染，会导致浏览器需要处理大量的 DOM 节点，从而引起性能瓶颈。
2. **事件绑定过多**：每个 `` 都绑定了 `@change` 事件，五千个事件监听器会消耗大量内存和 CPU 资源。
3. **图片加载**：即使使用了懒加载，五千张图片的元数据仍然需要加载，这也会增加页面的负担。

### 优化方案

#### 1. 使用虚拟滚动

虚拟滚动是一种常见的优化技术，它只渲染当前视口内的数据项，大大减少了 DOM 元素的数量。

```
bashnpm install vue-virtual-scroller --save
```

然后在组件中引入并使用：

```
vue<template>
  <RecycleScroller
    class="scroller"
    :items="filterCustomerList"
    :item-size="50"
    key-field="customerId"
    v-slot="\\{ item \\}"
  >
    <van-checkbox
      :key="item.customerId"
      :name="item.customerId"
      @change="onCheckChange"
    >
      <div :class="['radio-item', \\{ 'no-border': isLastItem(item) \\}]">
        <van-image width="32" height="32" :src="getAssets(`components/avatar.png`)" lazy-load />
        <div class="customer-name">\\\{\\\{ item.name || item.custName || item.nickname\\\}\\\} }}</div>
      </div>
    </van-checkbox>
  </RecycleScroller>
</template>

<script>
import \\{ RecycleScroller \\} from 'vue-virtual-scroller';
import 'vue-virtual-scroller/dist/vue-virtual-scroller.css';

export default \\{
  components: \\{
    RecycleScroller,
  \\},
  methods: \\{
    isLastItem(item) \\{
      return this.filterCustomerList[this.filterCustomerList.length - 1].customerId === item.customerId;
    \\},
    onCheckChange(value) \\{
      // 处理选中变化的逻辑
    \\},
    getAssets(path) \\{
      // 获取资源路径的逻辑
    \\},
  \\},
\\};
</script>

<style scoped>
.scroller \\{
  height: 300px; /* 根据实际需求调整高度 */
\\}
.radio-item \\{
  display: flex;
  align-items: center;
\\}
.no-border \\{
  border-bottom: none;
\\}
</style>
```

#### 2. 分页加载

将数据分页显示，每次只加载部分数据，减少一次性渲染的数据量。

```
vue<template>
  <div>
    <van-checkbox-group v-model="curSelectList" @change="onCheckChange">
      <van-checkbox v-for="(item, index) in paginatedCustomerList" :key="item.customerId" :name="item.customerId">
        <div :class="['radio-item', \\{ 'no-border': isLastItem(index) \\}]">
          <van-image width="32" height="32" :src="getAssets(`components/avatar.png`)" lazy-load />
          <div class="customer-name">\\\{\\\{ item.name || item.custName || item.nickname\\\}\\\} }}</div>
        </div>
      </van-checkbox>
    </van-checkbox-group>
    <button @click="loadMore">加载更多</button>
  </div>
</template>

<script>
export default \\{
  data() \\{
    return \\{
      curSelectList: [],
      filterCustomerList: [], // 假设这是你的数据源
      pageSize: 100,
      currentPage: 1,
    \\};
  \\},
  computed: \\{
    paginatedCustomerList() \\{
      const start = (this.currentPage - 1) * this.pageSize;
      const end = start + this.pageSize;
      return this.filterCustomerList.slice(start, end);
    \\},
  \\},
  methods: \\{
    isLastItem(index) \\{
      return index === this.paginatedCustomerList.length - 1;
    \\},
    onCheckChange(value) \\{
      // 处理选中变化的逻辑
    \\},
    getAssets(path) \\{
      // 获取资源路径的逻辑
    \\},
    loadMore() \\{
      this.currentPage++;
    \\},
  \\},
\\};
</script>

<style scoped>
.radio-item \\{
  display: flex;
  align-items: center;
\\}
.no-border \\{
  border-bottom: none;
\\}
</style>
```

#### 3. 懒加载图片

确保图片使用懒加载，减少初始加载时的资源消耗。

```
vue<van-image width="32" height="32" :src="getAssets(`components/avatar.png`)" lazy-load />
```

#### 4. 优化事件处理

减少不必要的事件绑定，可以考虑使用事件委托或其他优化手段。

### 总结

通过使用虚拟滚动、分页加载、懒加载图片和优化事件处理，可以显著提升页面的性能，避免因大量数据渲染导致的卡顿问题。希望这些优化建议对你有帮助！



### 减少查找时间

```
let list = []
        dataList.forEach((el) => \\{
          let item = this.filterCustomerList.find(
            (k) => k.customerId === el.customerId
          )
          if (!item) \\{
            list.push(el)
          \\}
        \\})
        this.filterCustomerList = [...this.filterCustomerList, ...list]
```

#### 解释

这段代码的功能是从 `dataList` 中找出那些不在 `this.filterCustomerList` 中的元素，然后将这些元素添加到 `this.filterCustomerList` 中。具体解释如下：

1. 首先初始化了一个空数组 `list`，用于临时存储需要添加的新元素。

2. 然后遍历 `dataList` 数组，对于每一个元素 `el`，它会尝试在 `this.filterCustomerList` 中查找是否存在一个对象，其 `customerId` 属性与 `el` 的 `customerId` 属性相匹配。

3. 如果没有找到匹配项（即 `item` 为 `false` 或 `undefined`），说明 `el` 是一个新的客户信息，不包含在当前的 `this.filterCustomerList` 中，因此将 `el` 添加到 `list` 数组中。

4. 最后，将 `list` 中的所有新元素合并到 `this.filterCustomerList` 中。这里使用了扩展运算符 (`...`) 来解构 `list` 和 `this.filterCustomerList`，并将它们合并成一个新的数组赋值给 `this.filterCustomerList`。

这段代码可能会有性能问题，特别是在 `dataList` 和 `this.filterCustomerList` 都非常大的时候，因为每次迭代都可能涉及对 `this.filterCustomerList` 的线性搜索。如果 `customerId` 是唯一的，并且你经常需要进行这样的查找操作，可以考虑使用 Map 或者 Set 来优化查找效率，例如通过 `customerId` 作为键来快速查找对应的客户信息。

#### 优化

为了优化这段代码，我们可以采用更高效的数据结构来减少查找时间。考虑到 `customerId` 的唯一性，可以使用 JavaScript 的 `Map` 对象来存储 `filterCustomerList`，这样可以将查找的时间复杂度从 O(n) 降低到 O(1)。

以下是优化后的代码：

```javascript
// 将 this.filterCustomerList 转换为 Map，以 customerId 作为键
const customerMap = new Map();
this.filterCustomerList.forEach(item => \\{
  customerMap.set(item.customerId, item);
\\});

// 遍历 dataList，对于每一个不在 customerMap 中的元素添加到 map 中
dataList.forEach(el => \\{
  if (!customerMap.has(el.customerId)) \\{
    customerMap.set(el.customerId, el);
  \\}
\\});

// 将更新后的 Map 转换回数组，并赋值给 this.filterCustomerList
this.filterCustomerList = Array.from(customerMap.values());
```

这种做法有几个优点：

- **查找效率高**：通过 `Map` 来存储客户信息，利用 `Map` 的 `has` 方法可以在常数时间内检查一个 `customerId` 是否已经存在。
- **避免重复**：由于 `Map` 的键是唯一的，所以自然就避免了 `filterCustomerList` 中出现重复的 `customerId`。
- **性能提升**：在处理大数据集时，性能会显著优于原代码，因为减少了对 `filterCustomerList` 数组的线性搜索次数。

此外，如果 `filterCustomerList` 和 `dataList` 都是大型数据集，那么这种优化可能会带来明显的性能改善。如果 `customerId` 是字符串或者数字类型的话，这个方法尤为适用。



#### 解释一下这两个customerMap.set区别

在这段代码中，`customerMap.set` 方法被调用了两次，但它们的目的和上下文有所不同：

### 第一次调用 `customerMap.set(item.customerId, item);`

这是在初始化 `customerMap` 的阶段。遍历 `this.filterCustomerList` 数组，将每一个客户对象 `item` 添加到 `customerMap` 中，以 `customerId` 作为键，`item` 客户对象本身作为值。

```javascript
this.filterCustomerList.forEach(item => \\{
  customerMap.set(item.customerId, item);
\\});
```

**目的：**
- 构建一个基于 `customerId` 的查找表（即 `Map`），以便后续能够快速判断某个 `customerId` 是否已经存在于 `filterCustomerList` 中。
- 这样做的好处是可以将查找时间复杂度从 O(n) 降低到 O(1)，极大地提高了效率，特别是当 `filterCustomerList` 非常大时。

### 第二次调用 `customerMap.set(el.customerId, el);`

这是在处理 `dataList` 的阶段。对于 `dataList` 中的每一个元素 `el`，如果它不在 `customerMap` 中（即它的 `customerId` 没有在 `customerMap` 中找到），那么就将这个新客户添加到 `customerMap` 中。

```javascript
if (!customerMap.has(el.customerId)) \\{
  customerMap.set(el.customerId, el);
\\}
```

**目的：**
- 将 `dataList` 中的新客户信息添加到 `customerMap` 中，确保最终的 `customerMap` 包含了所有需要保留的客户信息，同时避免了重复添加相同的客户（通过 `customerId` 判断）。
- 确保 `filterCustomerList` 最终包含的是无重复且更新后的客户列表。

### 总结

两个 `set` 调用的区别在于它们操作的数据源不同：

- **第一个** `set` 是用来填充初始的 `customerMap`，使用的是现有的 `filterCustomerList` 数据。
- **第二个** `set` 是用来更新 `customerMap`，根据 `dataList` 中的数据进行增补，只添加那些之前不存在的客户。

这样做可以有效地管理客户列表，既保证了数据的完整性，又提升了操作的效率。



#### Array.from(customerMap.values());解释

`Array.from(customerMap.values())` 是将 `Map` 对象中的所有值转换为一个数组。让我们来详细解释一下这个操作：

### Map.values()

- `customerMap.values()` 返回一个新的 Iterator 对象，该对象包含了 `Map` 中每个元素的值（即客户对象），按照插入顺序排列。
- 这个 Iterator 可以用于遍历 `Map` 的所有值，但它本身并不是一个数组，因此不能直接使用数组的方法。

### Array.from()

- `Array.from()` 方法可以从类似数组的对象或可迭代对象（如 `Map` 的 values iterator）创建一个真正的数组。
- 它接受三个参数，但在这个例子中我们只使用了第一个参数：
  - 第一个参数是要转换成数组的可迭代对象或类数组对象。
  - 后面两个参数是可选的，可以用来指定映射函数和作为 `this` 值的对象，在这里不适用。

### 组合使用

```javascript
this.filterCustomerList = Array.from(customerMap.values());
```

这行代码的作用是：

1. 使用 `customerMap.values()` 获取一个包含所有客户对象的 Iterator。
2. 使用 `Array.from()` 将这个 Iterator 转换为一个真实的数组。
3. 最后，将这个新的数组赋值给 `this.filterCustomerList`，更新其内容为 `customerMap` 中所有客户的最新集合。

### 为什么这么做？

这样做有几个好处：

- **类型转换**：确保 `this.filterCustomerList` 是一个真正的数组，而不是其他类型的可迭代对象，这样可以使用数组的所有方法。
- **数据同步**：通过这种方式，你可以确保 `this.filterCustomerList` 包含的是最新的、无重复的客户信息，并且这些信息是以数组的形式存储的，方便后续处理或展示。

总之，`Array.from(customerMap.values())` 是一种简洁有效的方式，用来从 `Map` 中提取所有的值并转换为数组，特别适用于需要将键值对结构的数据转换为简单的列表形式的情况。



### 这段代码比原来提升了多少

评估代码优化带来的性能提升百分比通常需要进行具体的性能测试，因为实际的性能增益取决于多个因素，包括但不限于数据集的大小、执行环境（如浏览器或Node.js版本）、硬件性能等。不过，我们可以基于理论分析给出一个大致的预期。

### 原始代码的时间复杂度

原始代码中，对于 `dataList` 中的每一个元素，都会遍历一次 `this.filterCustomerList` 来查找是否存在匹配的 `customerId`。如果 `dataList` 的长度为 m，`this.filterCustomerList` 的长度为 n，则时间复杂度为 O(m * n)。当 m 和 n 较大时，这种操作可能会非常耗时。

### 优化后的代码时间复杂度

优化后的代码使用了 `Map` 来存储客户信息，并通过 `Map` 的 `has` 方法在常数时间内检查 `customerId` 是否存在。因此，对于 `dataList` 中的每个元素，查找和插入操作的时间复杂度都降为了 O(1)，而初始化 `customerMap` 的时间复杂度为 O(n)。整体来看，优化后的代码的时间复杂度为 O(m + n)，其中 m 是 `dataList` 的长度，n 是 `this.filterCustomerList` 的长度。

### 性能提升估算

理论上讲，从 O(m * n) 到 O(m + n) 的转变可以带来显著的性能提升，特别是在 m 和 n 都很大的情况下。具体提升的百分比很难直接计算，因为它依赖于 m 和 n 的具体值。然而，我们可以用一个简化的方式估计：

- 如果 `m` 和 `n` 都是 1000，那么原始代码的总操作次数大约是 1,000,000 次（即 1000 * 1000），而优化后的代码大约只需要 2000 次（即 1000 + 1000）。
- 这意味着，在这个特定的例子中，性能提升了约 (1,000,000 - 2000) / 1,000,000 = 99.8\\%。

请注意，这只是一个理论上的估算。实际性能提升会因实际情况而异。为了得到准确的性能提升百分比，建议在实际运行环境中对原始代码和优化后的代码进行基准测试（benchmarking），并记录它们各自的执行时间来进行比较。



### 优化代码，逻辑不变，注释尽量保留

```
if (this.isPreset) \\{
        if (this.selectTags && this.selectTags.length) \\{
          // mot-标签过滤
          this.filterCustomerList = []
          for (let i = 0; i < this.presetRangeList.length; i++) \\{
            const customerItem = this.presetRangeList[i]
            // 是否符合标签
            let isFit = true
            this.selectTags.find((item) => \\{
              // 该标签customers中的wxworkId，是否和当前循环的客户匹配
              let subFit = false
             for (let j = 0; j < item.customers.length; j++) \\{
                const subItem = item.customers[j]
                if (subItem.wxworkId === customerItem.wxworkId) \\{
                  subFit = true
                  break
                \\}
              \\}
              if (!subFit) \\{
                isFit = false
              \\}
            \\})
            if (isFit) \\{
              // 符合标签，列表显示该客户
              this.filterCustomerList.push(customerItem)
            \\} else \\{
              // 不符合标签，列表不显示该客户，清除之前勾选
              this.checkInfoMap.set(customerItem.customerId, false)
            \\}
          \\}
        \\} else \\{
          // 没有标签
          this.filterCustomerList = this.presetRangeList
        \\}
        console.log(this.filterCustomerList, this.presetRangeList)
        this.totalNum = this.filterCustomerList.length
        return
      \\}
```

为了优化这段代码，我们可以采取一些措施来提高其可读性和性能。例如，可以使用更简洁的语法（如`forEach`、`some`等），同时减少不必要的循环次数。以下是优化后的代码：

```javascript
if (this.isPreset) \\{
  if (this.selectTags && this.selectTags.length) \\{
    // mot-标签过滤
    this.filterCustomerList = this.presetRangeList.filter(customerItem => \\{
      // 是否符合所有选中的标签
      let isFit = this.selectTags.every(tag => 
        // 检查当前客户是否在标签的客户列表中
        tag.customers.some(subItem => subItem.wxworkId === customerItem.wxworkId)
      );
      
      if (!isFit) \\{
        // 不符合标签，列表不显示该客户，清除之前勾选
        this.checkInfoMap.set(customerItem.customerId, false);
      \\}
      
      return isFit;
    \\});
  \\} else \\{
    // 没有标签
    this.filterCustomerList = this.presetRangeList;
  \\}

  console.log(this.filterCustomerList, this.presetRangeList);
  this.totalNum = this.filterCustomerList.length;
  return
\\}
```

这里做了如下改进：
1. 使用`filter`方法代替了for循环和手动添加到`filterCustomerList`数组。
2. 使用`every`结合`some`来检查每个客户是否匹配所有选中的标签，这简化了内部逻辑并提高了代码的可读性。
3. 直接在`filter`回调中处理不符合条件的客户，即设置`checkInfoMap`值为`false`。

这些改动不会改变原有逻辑，但会使代码更加简洁和易于理解。

#### 再加入名称过滤逻辑

```
if (this.isPreset) \\{
        // 预设已选列表搜索
        const resultList = []
        this.custName = this.custName.trim()
        if (this.custName) \\{
          this.presetRangeList.forEach((item) => \\{
            if (item.custName && item.custName.indexOf(this.custName) > -1) \\{
              resultList.push(item)
            \\}
          \\})
        \\}
        this.searchCustomerList = resultList
        return
      \\}
```

为了将名称过滤逻辑整合到现有的预设筛选逻辑中，同时保持代码的清晰和高效，我们可以对两个逻辑进行合并。这不仅减少了重复代码，还确保了在应用标签过滤的同时也考虑到了名称过滤。下面是优化后的代码：

```javascript
if (this.isPreset) \\{
  // 预设已选列表搜索与标签过滤

  // 处理客户名称输入框的值
  this.custName = this.custName.trim();

  // 定义一个过滤函数，用于同时处理标签和名称过滤
  const filterFunc = (customerItem) => \\{
    let isFit = true;

    // 如果有选中的标签，则检查客户是否符合所有选中的标签
    if (this.selectTags && this.selectTags.length) \\{
      isFit = this.selectTags.every(tag =>
        tag.customers.some(subItem => subItem.wxworkId === customerItem.wxworkId)
      );
    \\}

    // 如果提供了客户名称，则检查客户名称是否包含搜索字符串
    if (this.custName && isFit) \\{
      isFit = customerItem.custName && customerItem.custName.indexOf(this.custName) > -1;
    \\}

    return isFit;
  \\};

  // 应用过滤函数
  this.filterCustomerList = this.presetRangeList.filter(filterFunc);

  // 创建一个Set来存储符合条件的客户的ID
  const filteredCustomerIds = new Set(this.filterCustomerList.map(item => item.customerId));

  // 更新checkInfoMap：对于不在filterCustomerList中且之前选中的客户，清除勾选状态
  this.presetRangeList.forEach(customerItem => \\{
    if (!filteredCustomerIds.has(customerItem.customerId) && this.checkInfoMap.get(customerItem.customerId)) \\{
      this.checkInfoMap.set(customerItem.customerId, false);
    \\}
  \\});

  console.log(this.filterCustomerList, this.presetRangeList);
  this.totalNum = this.filterCustomerList.length;

  // 更新搜索结果列表（如果需要单独的搜索结果列表）
  this.searchCustomerList = this.custName ? this.filterCustomerList : [];

  return;
\\}
```

在这个版本中：
- 我们定义了一个`filterFunc`函数来同时处理标签过滤和名称过滤。
- 使用这个函数来创建`filterCustomerList`，并且也用来更新`checkInfoMap`。
- `searchCustomerList`只在提供了客户名称时才被更新为`filterCustomerList`，否则它将为空数组。

这样做可以确保无论是否有客户名称过滤条件，代码都能正确地应用标签过滤，并且不会出现不必要的重复操作。



### $listeners在vue3中报错

```
父组件<Upload ref="uploadImage"
      @oversize="oversize('图片需小于等于10M')"
      result-type="file"
      :max-size="10 * 1024 * 1024"
      accept=".png,.jpg"
      file-type="uploadImage"
      @after-read="afterRead"></Upload>
    <Upload ref="uploadVideo"
      @oversize="oversize('视频需小于等于10M')"
      result-type="file"
      :max-size="10 * 1024 * 1024"
      accept="video/mp4"
      file-type="uploadVideo"
      @after-read="afterRead"></Upload>子组件<template>
  <van-uploader
    ref="upload"
    :after-read="afterRead"
    v-show="false"
    style="pointer-events: none; position: absolute"
    v-bind="$attrs"
    v-on="$listeners"
  />
</template>应该怎么修改
```

在子组件中直接去掉 `v-on="$listeners"` 这一行是可以的，但前提是你要确保所有需要监听的事件已经在父组件中通过显式的 `v-on` 绑定到了子组件。如果你移除了 `v-on="$listeners"` 并且没有为这些事件提供显式的绑定，那么原本依赖于 `$listeners` 传递下来的事件将不再被触发。

### 分析你的场景

根据你提供的代码：

#### 父组件
```vue
<Upload ref="uploadImage"
  @oversize="oversize('图片需小于等于10M')"
  result-type="file"
  :max-size="10 * 1024 * 1024"
  accept=".png,.jpg"
  file-type="uploadImage"
  @after-read="afterRead">
</Upload>
<Upload ref="uploadVideo"
  @oversize="oversize('视频需小于等于10M')"
  result-type="file"
  :max-size="10 * 1024 * 1024"
  accept="video/mp4"
  file-type="uploadVideo"
  @after-read="afterRead">
</Upload>
```

#### 子组件 (Upload.vue)
```vue
<template>
  <van-uploader
    ref="upload"
    v-show="false"
    style="pointer-events: none; position: absolute"
    v-bind="$attrs"
    v-on="$listeners" <!-- 这一行 -->
  />
</template>
```

### 解决方案

由于你在父组件中已经明确绑定了 `@oversize` 和 `@after-read` 事件，你可以安全地移除子组件中的 `v-on="$listeners"`，因为这些事件已经被显式定义了。接下来，你需要确保这些事件能够正确传递和处理。

### 修改后的子组件代码

```vue
<template>
  <van-uploader
    ref="upload"
    v-show="false"
    style="pointer-events: none; position: absolute"
    v-bind="$attrs"
    @oversize="emitOversize"
    @after-read="handleAfterRead"
  />
</template>

<script setup>
import \\{ useAttrs, defineEmits \\} from 'vue';

const attrs = useAttrs();
const emit = defineEmits(['oversize', 'after-read']);

function emitOversize(event) \\{
  emit('oversize', event);
\\}

function handleAfterRead(file) \\{
  emit('after-read', file);
\\}
</script>
```

### 注意事项

- **移除 `v-on="$listeners"`**：因为你已经在父组件中显式地绑定了所有需要的事件（如 `@oversize` 和 `@after-read`），所以不需要再使用 `v-on="$listeners"`。
- **保持 `v-bind="$attrs"`**：这行代码仍然保留，因为它会把所有非 prop 属性（例如 `result-type`, `max-size`, `accept`, `file-type`）从父组件传递给子组件。
- **确保事件处理逻辑**：确认所有必要的事件都在父组件和子组件之间正确绑定，并且子组件中有相应的处理逻辑来发射这些事件。

### 总结

是的，你可以直接移除 `v-on="$listeners"`，并且这样做可以使代码更清晰，因为所有的事件监听都是显式定义的。确保你已经为每个需要监听的事件提供了显式的 `v-on` 绑定，并且在子组件中正确处理这些事件。如果将来添加新的事件监听器，记得相应地更新子组件中的事件绑定。
