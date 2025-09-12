---
title: vant
date: 2022-05-23 23:40:25
categories: 
- 前端问题
tags:
- vue
---

### uni-app 或 微信小程序，使用vant组件

1.下载vant组件

[vant的GitHub下载地址](https://github.com/youzan/vant-weapp/releases)下载完成后解压，然后在项目根目录下创建文件夹`wxcomponents`，注意这里的`wxcomponents`目录级别和`pages`在同一级别，回到刚才解压的vant目录，找到`dist`文件夹，重命名为vant，把它复制到`wxcomponents`目录下。

2.首先在`app.vue`文件内添加

```scss
@import "/wxcomponents/vant/common/index.wxss";
```

3.在pages.json文件内添加组件引用

你可以选择在一个页面的配置文件style里面配置，但是只能在这个页面内使用

你也可以选择在globalStyle里面配置，是所有页面都可以直接使用

```css
"usingComponents":\\{
	"van-button": "/wxcomponents/vant/button/index",
    "van-cell": "/wxcomponents/vant/cell/index",
    "van-cell-group": "/wxcomponents/vant/cell-group/index",
    "van-icon": "/wxcomponents/vant/icon/index",
    "van-image": "/wxcomponents/vant/image/index",
    "van-row": "/wxcomponents/vant/row/index",
    "van-col": "/wxcomponents/vant/col/index",
    "van-popup": "/wxcomponents/vant/popup/index",
    "van-dialog": "/wxcomponents/vant/dialog/index",
    "van-toast": "/wxcomponents/vant/toast/index"
\\}
```

4.在你要使用的页面内添加你要使用的组件就可以了

```
<van-button type="default">默认按钮</van-button>
```

##### 注意事项：上述配置完成后，记得关闭微信开发者 工具，然后重新用Hbuilder启动微信开发者工具，才能看到效果，需要重加载包文件。

https://vant-contrib.gitee.io/vant-weapp/#/



### uniapp-H5，使用vant组件

1.安装

```
// Vue 2 项目，安装 Vant 2：
npm i vant@latest-v2 -S
```

2.App.vue在style里面全局引入vant的样式 

```
@import 'vant/lib/index.css';
```

3.在页面中

```
<dropdown-menu></dropdown-menu>

import \\{ DropdownMenu, DropdownItem, TreeSelect \\} from 'vant'
components: \\{
    DropdownMenu,
    DropdownItem,
    TreeSelect
\\},
```

https://vant-contrib.gitee.io/vant/v2/#/zh-CN/



### vant组件库在微信小程序和H5同时使用

1.下载/安装步骤同上

2.App.vue在style里面全局引入vant的样式 

```
<style lang="scss">
// #ifdef MP-WEIXIN
@import '/wxcomponents/vant/common/index.wxss';
// #endif
// #ifdef H5
@import 'vant/lib/index.css';
// #endif
</style>
```

3.在pages.json中

```
\\{
			"path": "pages/index/index",
			"style": \\{
				"navigationBarTitleText": "首页",
				"navigationStyle": "custom",
				"enablePullDownRefresh": true,
				"backgroundColor": "#F5F7F9",
				"usingComponents": \\{
					// #ifdef MP-WEIXIN
					"dropdown-menu": "/wxcomponents/vant/dropdown-menu/index",
					"dropdown-item": "/wxcomponents/vant/dropdown-item/index",
					"tree-select": "/wxcomponents/vant/tree-select/index"
					// #endif
				\\}
			\\}
		\\},
```

4.在页面中

```
<dropdown-menu></dropdown-menu>

// #ifdef H5
import \\{ DropdownMenu, DropdownItem, TreeSelect \\} from 'vant'
// #endif

export default \\{
    // #ifdef H5
    components: \\{
        DropdownMenu,
        DropdownItem,
        TreeSelect
    \\},
    // #endif
\\}
```



### 开关正确用法

```
<van-switch :checked="checked" @change="switchSignIn" active-color="#ee0a24" inactive-color="#dcdee0" />
```

```
// 签到提醒
switchSignIn() \\{
	this.checked = !this.checked;
\\}
```



### uni-app 编译H5报错，编译小程序没问题

```
SyntaxError
10:12:34.675 (1:5774) Unclosed bracket
```

如果是icon/index.wxss文件报错, 全局搜索("woff2"),和("woff"),逗号后加个空格就可以了

```
src:url(https://img01.yzcdn.cn/vant/vant-icon-f463a9.woff2) format("woff2"), url(https://img01.yzcdn.cn/vant/vant-icon-f463a9.woff) format("woff"),
```



### uniapp 引入vant后 运行h5页面报错 Cannot read property 'split' of undefined

在version.js找到compareVersion方法，对里面的v1和v2参数 做一个处理

```
复制代码v1 = v1?v1.split('.'):[];  
v2 = v2?v2.split('.'):[];
```



### Vant 步进器 van-stepper 阻止事件冒泡

 一般情况下

> Vue 阻止事件冒泡用 .**stop** 即可解决
>
> Vue 阻止事件默认行为用 **.prevent** 解决

今天这里是介绍 **Vant** 框架里写购物车，需求是购物车中的商品点击也可以进入到商品详情，于是在 card 标签加了 click 事件，就导致点击步进器 **van-stepper** 增加减少也会触发 card 的 click ，用原生事件 **event.stopPropagation()** 即可完美解决

```html
<van-stepper 
  v-model="val.quantity" 
  @plus="plusNum(val.id)" 
  @minus="minusNum(val.id)" 
  min="1" 
  disable-input 
/>
plusNum(id) \\{
  event.stopPropagation();  // 阻止事件冒泡
  console.log(id);
\\},
minusNum(id) \\{
  event.stopPropagation();  // 阻止事件冒泡
  console.log(id);
\\},
```

catchtap=“onChange” 依然能触发change函数，也完美的阻止了事件冒泡行为。



### vant骨架屏

在`app.json`或`index.json`中引入组件

```
"usingComponents": \\{
  "van-skeleton": "@vant/weapp/skeleton/index"
\\}
```

在页面中

```
<template>
	<van-skeleton title avatar animate :row="2" :row-width="['50\\%','80\\%']" :loading="loading">
		<view>内容</view>
	</van-skeleton>
</template>

data中
loading: true, //开启骨架屏

methods中加载完数据后
this.loading = false; // 关闭骨架屏

```



### 时间选择器

wxml

```
<!-- vant时间选择器在安卓上抖动 -->
  <van-popup show="\\\{\\\{ isShowTime1\\\}\\\} }}" round position="bottom" custom-style="height: 40\\%" bind:close="onClose1">
    <van-datetime-picker type="datetime" value="\\\{\\\{ currentDate1\\\}\\\} }}" min-date="\\\{\\\{ minDate\\\}\\\} }}" max-date="\\\{\\\{ maxDate\\\}\\\} }}" formatter="\\\{\\\{formatte\\\}\\\}r}}" bind:change="onChange1" bind:confirm="onClose1" bind:cancel="onClose1" />
  </van-popup>
  <van-popup show="\\\{\\\{ isShowTime2\\\}\\\} }}" round position="bottom" custom-style="height: 40\\%" bind:close="onClose2">
    <van-datetime-picker type="datetime" value="\\\{\\\{ currentDate2\\\}\\\} }}" min-date="\\\{\\\{ currentDate1\\\}\\\} }}" max-date="\\\{\\\{ maxDate\\\}\\\} }}" formatter="\\\{\\\{formatte\\\}\\\}r}}" bind:change="onChange2" bind:confirm="onClose2" bind:cancel="onClose2" />
  </van-popup>
```

js-data

```
maxDate: new Date(2023, 11, 31, 23, 59, 59).getTime(),
    // 用车开始时间
    isShowTime1: false,
    currentDate1: new Date().getTime(),
    minDate: new Date(2021, 00, 01, 00, 00, 00).getTime(),
    // 用车结束时间
    isShowTime2: false,
    currentDate2: new Date().getTime(),
    // 处理控件显示的时间格式
    formatter(type, value) \\{
      // 格式化选择器日期
      if (type === "year") \\{
        return `$\\{value\\}年`;
      \\} else if (type === "month") \\{
        return `$\\{value\\}月`;
      \\} else if (type === "day") \\{
        return `$\\{value\\}日`;
      \\} else if (type === "hour") \\{
        return `$\\{value\\}时`;
      \\} else if (type === "minute") \\{
        return `$\\{value\\}分`;
      \\}
      return value;
    \\}
```

js方法

```
// 显示时间弹窗
  showTime1() \\{
    this.setData(\\{
      isShowTime1: true
    \\})
  \\},
  showTime2() \\{
    this.setData(\\{
      isShowTime2: true
    \\})
  \\},
  // 关闭时间弹窗
  onClose1() \\{
    this.setData(\\{
      isShowTime1: false
    \\})
  \\},
  onClose2() \\{
    this.setData(\\{
      isShowTime2: false
    \\})
  \\},
  // 改变时间
  onInput1(event) \\{
    // @input在Android手机上会有抖动问题，所以用change
    this.setData(\\{
      currentDate1: event.detail,
      "formModel.use_start": this.formatTime(event.detail)
    \\});
  \\},
  onChange1(event) \\{
    // let value = event.detail.getColumnValue(0) + ':' + event.detail.getColumnValue(1)//获取每列进行拼接
    let temp = event.detail.getValues();
    if (temp) \\{
      for (let i = 0; i < temp.length; i++) \\{
        // 在字符串中抽取从 start 下标开始的指定数目的字符
        temp[i] = temp[i].substr(0, temp[i].length - 1);
      \\}
      temp = temp.join('-') + '-00'
      let date = temp.substr(0, 10)
      let time = temp.substr(11, 8).replace(/-/g, ':')
      temp = date + ' ' + time // 所需时间格式
      var date1 = new Date(temp.replace(/-/g, '/'));
      time1 = date1.getTime(); // 组件所需时间戳
      // console.log(temp, date1, time1, this.data)
      this.setData(\\{
        "formModel.use_start": temp,
        currentDate1: time1
      \\});
    \\}
  \\},
  onChange2(event) \\{
    let temp = event.detail.getValues();
    for (let i = 0; i < temp.length; i++) \\{
      // 在字符串中抽取从 start 下标开始的指定数目的字符
      temp[i] = temp[i].substr(0, temp[i].length - 1);
    \\}
    temp = temp.join('-') + '-00'
    let date = temp.substr(0, 10)
    let time = temp.substr(11, 8).replace(/-/g, ':')
    temp = date + ' ' + time // 所需时间格式
    var date1 = new Date(temp.replace(/-/g, '/'));
    time1 = date1.getTime(); // 组件所需时间戳
    this.setData(\\{
      "formModel.use_end": temp,
      currentDate2: time1
    \\});
    // console.log(temp, date, time, this.data)
  \\},
```

json

```
"van-popup": "@vant/weapp/popup/index",
"van-datetime-picker": "@vant/weapp/datetime-picker/index"
```



### 当 `<van-popover> `激活时改变 .drop-down 的颜色

```
<van-popover v-model:show="isShowCate"
:actions="actions"
@select="cateSelect">
    <template #reference>
        <div class="sort-item drop-down"
            :class="\\{ 'active': isShowCate \\}">
            <span>全部分类</span>
        </div>
    </template>
</van-popover>

// 是否显示全部分类
const isShowCate = ref(false)
// 选择全部分类某项
const cateSelect = (action) => \\{
  searchType.value = action.text
  isShowCate.value = false
\\}

.drop-down \\{
    position: relative;
    &::after \\{
        content: '';
        border: 5px solid transparent;
        border-top-color: #8692a6;
        position: absolute;
        top: 9px;
        right: -18px;
    \\}
    // 激活时改变颜色
    &.active::after \\{
        border-top-color: #267ef0;
    \\}
\\}
```



### 懒加载

```
import \\{ Lazyload \\} from 'vant'
instance.use(Lazyload)
```

Vant 的 `Lazyload` 组件除了以组件形式使用外，还支持通过自定义指令的方式来实现懒加载。这种方式可以让你更灵活地应用懒加载逻辑到不同的元素上，而不仅仅是 `<img>` 标签。以下是使用 `v-lazy` 指令的示例：

1. 首先确保你已经安装并引入了 Vant 的 `Lazyload`。

2. 注册 `Lazyload` 并开启指令模式：

```javascript
import \\{ createApp \\} from 'vue';
import App from './App.vue';
import \\{ Lazyload \\} from 'vant';

const app = createApp(App);
app.use(Lazyload); // 注册懒加载插件
app.mount('#app');
```

3. 使用 `v-lazy` 指令在模板中：

```html
<img v-lazy="src" />
```

这里 `src` 是一个包含图片路径的数据属性，例如：

```javascript
data() \\{
  return \\{
    src: 'https://example.com/image.png'
  \\};
\\}
```

4. (可选) 设置默认占位图：

如果你想要为所有使用 `v-lazy` 指令的图片设置一个默认的加载中或错误状态下的占位图，你可以这样配置：

```javascript
Vue.use(Lazyload, \\{
  loading: 'https://example.com/loading.png', // 加载中的占位图
  error: 'https://example.com/error.png',     // 加载失败的占位图
\\});
```

5. (可选) 对于背景图片的懒加载：

对于 CSS 背景图片，你可以使用 `v-lazy` 指令来指定一个对象，其中包含 `background` 属性和对应的 URL：

```html
<div v-lazy="\\{ background: 'https://example.com/background.jpg' \\}"></div>
<div class="bg"
     v-lazy:background-image="item.imageUrl"></div>
```

6. (可选) 自定义选项：

你可以传递更多选项给 `Lazyload` 插件，比如调整监听的事件、根元素等。详情请参阅 [Vant 官方文档](https://youzan.github.io/vant/)。

7. 更新懒加载：

如果动态添加了新的需要懒加载的节点，或者页面结构发生了变化，你可以调用 `this.$Lazyload.update()` 来手动触发懒加载检查。

以上就是使用 `v-lazy` 指令来实现懒加载的方式。根据 Vant 版本的不同，API 可能会有所变化，请参考官方文档获取最新的信息。



### .van-checkbox选中文字颜色

```
		:deep(.van-checkbox) \\{
            height: 50px;
            line-height: 20px;
            padding-left: 15px;
            border-radius: 6px;
            font-size: 15px;
            color: #2b3341;
            box-shadow: 0px 1px 2px 0px rgba(0, 0, 0, 0.08);
            .van-checkbox__icon--checked + .van-checkbox__label \\{
              /* 选中的文字颜色 */
              color: #267ef0;
            \\}
          \\}
```



### 怎么把onSelect改成类似于

@click="handleIndexChange(event.type, eventIndex, item)"，其中item相当于onSelect的默认参数

```
			<van-popover v-if="event.indexList?.length>4"
                :actions="event.indexList"
                placement="bottom-start"
                @select="onSelect">
                <template #reference>
                  <div class="drop-item align-center">
                    <span>\\\{\\\{ cardStates[eventIndex]?.btnName\\\}\\\} }}</span>
                    <img src="@/assets/images/customer/drop@2x.png"
                      alt="">
                  </div>
                </template>
             </van-popover>
```

要将 `@select` 事件处理改为传递 `event.type`、`eventIndex` 和默认参数 `item`，你可以使用箭头函数直接捕获参数。修改后的代码如下：

```html
<van-popover 
  v-if="event.indexList?.length>4"
  :actions="event.indexList"
  placement="bottom-start"
  @select="(item) => handleIndexChange(event.type, eventIndex, item)">
  <template #reference>
    <div class="drop-item align-center">
      <span>\\\{\\\{ cardStates[eventIndex]?.btnName\\\}\\\} }}</span>
      <img src="@/assets/images/customer/drop@2x.png" alt="">
    </div>
  </template>
</van-popover>
```

解释：
1. `@select` 事件绑定：通过 `(item) => handleIndexChange(...)` 箭头函数，将 `@select` 默认返回的 `item` 作为第三个参数传递。
2. 参数传递：`event.type` 和 `eventIndex` 直接来自当前作用域（如 `v-for` 循环中的变量），`item` 由 `@select` 事件自动提供。
3. 确保作用域正确：确保 `event` 和 `eventIndex` 在模板中可访问（如循环中的变量定义）。

这样即可在 `handleIndexChange` 方法中同时获取这三个参数。



### 在vue3中怎么动态修改placement根据页面的高度决定显示在上方还是下方

```
<!-- 分类下拉 -->
              <van-popover v-if="event.indexList?.length>4"
                :actions="event.indexList"
                :offset="[0, -6]"
                placement="top"
                @select="(item) => handleIndexChange(item, event.type, eventIndex)">
                <template #reference>
                  <div class="drop-item align-center">
                    <span>\\\{\\\{ cardStates[eventIndex]?.btnName\\\}\\\} }}</span>
                    <img src="@/assets/images/customer/drop@2x.png"
  						alt="">
                  </div>
                </template>
              </van-popover>
```

在 Vue 3 中，你可以根据页面高度动态修改 `van-popover` 的 `placement` 属性。以下是实现方法：

#### 方法一：使用计算属性动态判断，不行

```html
<template>
  <van-popover 
    v-if="event.indexList?.length>4"
    :actions="event.indexList"
    :offset="[0, -6]"
    :placement="getPopoverPlacement(eventIndex)"
    @select="(item) => handleIndexChange(item, event.type, eventIndex)">
    <!-- 其他内容 -->
  </van-popover>
</template>

<script setup>
import \\{ ref, computed, onMounted \\} from 'vue';

// 假设这是你的组件数据
const cardStates = ref([]);

// 计算每个popover的位置
const getPopoverPlacement = (index) => \\{
  // 获取元素位置
  const element = document.querySelectorAll('.drop-item')[index];
  if (!element) return 'top'; // 默认值
  
  const rect = element.getBoundingClientRect();
  const viewportHeight = window.innerHeight;
  
  // 如果元素靠近底部，就显示在上方，否则显示在下方
  return rect.bottom > viewportHeight / 2 ? 'top' : 'bottom';
\\};
</script>
```

#### 方法二：使用 Intersection Observer API（更现代的方法），没试过

```html
<script setup>
import \\{ ref, onMounted \\} from 'vue';

// 存储每个popover的位置
const placements = ref([]);

onMounted(() => \\{
  const observer = new IntersectionObserver((entries) => \\{
    entries.forEach(entry => \\{
      const index = parseInt(entry.target.dataset.index);
      const isNearBottom = entry.boundingClientRect.bottom > window.innerHeight / 2;
      placements.value[index] = isNearBottom ? 'top' : 'bottom';
    \\});
  \\}, \\{
    threshold: 1.0
  \\});

  // 观察所有drop-item元素
  document.querySelectorAll('.drop-item').forEach((el, index) => \\{
    el.dataset.index = index;
    observer.observe(el);
  \\});
\\});

const getPlacement = (index) => \\{
  return placements.value[index] || 'top'; // 默认值
\\};
</script>

<template>
  <van-popover 
    :placement="getPlacement(eventIndex)"
    <!-- 其他属性 -->
  >
    <!-- 内容 -->
  </van-popover>
</template>
```

#### 方法三：响应式监听滚动和窗口大小变化，可以

```html
<script setup>
import \\{ ref, onMounted, onUnmounted \\} from 'vue';
import \\{ throttle \\} from 'lodash-es';

// 存储每个popover的位置状态，使用对象存储，响应性更好
const placements = ref(\\{\\});
/**
 * 更新所有drop-item元素的位置状态
 * 根据元素在视口中的位置决定popover显示在上方还是下方
 */
const updatePlacements = () => \\{
  // 获取所有drop-item元素
  const dropItems = document.querySelectorAll('.drop-item');
  const newPlacements = \\{...placements.value\\};
  
  dropItems.forEach((el, index) => \\{
    // 获取元素位置信息
    const rect = el.getBoundingClientRect();
    const viewportHeight = window.innerHeight;
    // 如果元素位于视口下半部分，则popover显示在上方，否则显示在下方
    newPlacements[index] = rect.bottom > viewportHeight / 2 ? 'top' : 'bottom';
  \\});
  
  placements.value = newPlacements;
\\};

// 创建节流版本的更新函数，300ms内最多执行一次
const throttledUpdate = throttle(updatePlacements, 300);

onMounted(() => \\{
  // 初始更新
  updatePlacements();
  
  // 添加滚动和窗口大小变化监听（使用节流函数）
  window.addEventListener('scroll', throttledUpdate);
  window.addEventListener('resize', throttledUpdate);
\\});

onUnmounted(() => \\{
  // 组件卸载时移除事件监听
  window.removeEventListener('scroll', throttledUpdate);
  window.removeEventListener('resize', throttledUpdate);
  
  // 取消节流函数中待执行的调用
  throttledUpdate.cancel();
\\});
</script>

<template>
  <van-popover 
    v-if="event.indexList?.length>4"
    :actions="event.indexList"
    :offset="[0, -6]"
    :placement="placements[eventIndex] || 'top'"
    @select="(item) => handleIndexChange(item, event.type, eventIndex)">
    <template #reference>
        <div class="drop-item align-center">
            <span>\\\{\\\{ cardStates[eventIndex]?.btnName\\\}\\\} }}</span>
            <img src="@/assets/images/customer/drop@2x.png"
                 alt="">
        </div>
      </template>
  </van-popover>
</template>
```

#### 注意事项

1. 确保在组件挂载后(`onMounted`)再访问DOM元素
2. 对于大量元素，Intersection Observer API性能更好
3. 记得在组件卸载时清理事件监听器
4. 你可能需要根据实际情况调整判断逻辑(如使用不同的阈值)

以上方法都可以实现根据页面高度动态调整popover显示位置的功能，选择最适合你项目需求的一种即可。



### 全局封装的错误拦截提示方法

```
function showFrontToast(msg) \\{
  let tips = msg || '网络异常，请重试！'
  if (tips.length > 40) \\{
    showDialog(\\{
      width: '320px',
      title: '请确认',
      messageAlign: 'left',
      message: tips,
      confirmButtonColor: '#0052D9',
      confirmButtonText: '知道了',
    \\}).then(() => \\{\\})
  \\} else \\{
    showToast(\\{
      type: 'fail',
      message: tips,
      duration: 5000,
    \\})
  \\}
\\}
报错后，点击知道了没反应；移动端滑动不了，pc滚动条也动不了
原因是：页面中成功了才closeToast()
showLoadingToast(\\{
    duration: 0, // 持续展示 toast
    forbidClick: true,
    message: '加载中'
  \\})
const \\{ success, data \\} = await getEvaluateLink()
if (success) \\{
closeToast()
但改成
closeToast()
if (success) \\{
也会有问题，全局toast提示被立马清除了，提示时间过短
```

**问题根本原因分析：**

1. 加载中Toast未正确关闭导致界面锁死
2. 成功/失败提示与加载中Toast存在时序冲突

```
/* 注意：页面中成功再清除，如：if(success)\\{closeToast()\\}
失败无需清除，会导致全局报错toast提示被立马清除了，提示时间过短 */
function showFrontToast(msg) \\{
  // 先关闭可能存在的其他提示，防止页面中forbidClick:true导致点击'知道了'没反应
  closeToast()
  let tips = msg || '网络异常，请重试！'
  if (tips.length > 40) \\{
    showDialog(\\{
      width: '320px',
      title: '请确认',
      messageAlign: 'left',
      message: tips,
      confirmButtonColor: '#0052D9',
      confirmButtonText: '知道了',
    \\}).then(() => \\{\\})
  \\} else \\{
    showToast(\\{
      type: 'fail',
      message: tips,
      duration: 5000,
    \\})
  \\}
\\}
```



### vant showImagePreview在qiankun有兼容性问题，图片显示宽度过小，是细长条状，不是全屏

```
import \\{ showImagePreview \\} from 'vant'
// 图片预览
const showImg = (codeUrl: string) => \\{
  showImagePreview(\\{
    teleport: '.page',
    images: [codeUrl],
    showIndex: false,
    closeable: true
  \\})
\\}
```

可能是函数式组件还没加载好，有问题

函数调用存在兼容性问题，改用组件形式手动控制显隐

```vue
<template>
  <van-image-preview
    v-model:show="showPreview"
    :images="[codeUrl]"
    :show-index="false"
    closeable
  />
</template>

<script setup>
import \\{ ref \\} from 'vue';
// 图片预览，函数调用存在兼容性问题，改用组件形式
const showPreview = ref(false);
const codeUrl = ref('');
const showImg = (url) => \\{
  codeUrl.value = url;
  showPreview.value = true;
\\};
</script>
```



### van-sticky组件问题

#### pc端正常 移动端：初始tab显示正常，点击进入详情页（其他子应用），返回列表页，上滑页面，tab的style宽高会变成无穷大

请分析可能的原因并解决

```
<div class="van-sticky van-sticky--fixed" style="width: 5.00069e+06px; height: 586216px; top: 0px;"> 
```

解决：

```
.page \\{
  // 修复：进入详情页，返回列表页，上滑页面，tab的style宽高会变成无穷大
  > div:first-child \\{
    width: 100\\% !important;
    max-width: 740px;
    height: auto !important;
  \\}
  :deep(.van-sticky--fixed) \\{
    width: 100\\% !important;
    max-width: 740px;
    height: auto !important;
  \\}
\\}
```

#### 在安卓、pc正常，在ios吸顶时会一直向右偏移一半，一直滑动一直闪烁

```
<!-- 标签切换 -->
<template>
  <van-sticky>
    <van-tabs v-model:active="activeTab">
      <!-- 标签内容 -->
    </van-tabs>
  </van-sticky>
</template>

// 吸顶时水平居中
:deep(.van-sticky--fixed) \\{
  left: 50\\%;
  transform: translateX(-50\\%);
\\}
```

要解决iOS上吸顶标签页闪烁并向右偏移的问题，可以通过以下方案修复：

##### 原因分析：

iOS Safari对粘性定位（sticky）+ 动态变换（transform）的组合存在渲染问题，导致元素在固定定位时坐标计算错误。

##### 解决方案：

通过自动外边距居中

```
<style scoped>
// 吸顶时水平居中，兼容ios
:deep(.van-sticky--fixed) \\{
  width: 100\\%;
  max-width: 740px;
  left: 0;
  right: 0;
  margin: 0 auto;
  /* 修复iOS滑动时的闪烁问题 */
  -webkit-overflow-scrolling: auto;
\\}
</style>
```

##### 关键修改说明：

1. **替代居中方式**
   - 移除 `left: 50\\%` 和 `transform`
   - 使用 `left:0 + right:0 + margin:auto` 实现居中
2. **iOS滑动优化**
    `-webkit-overflow-scrolling: auto` 禁用弹性滚动（可能导致问题的根源）
3. **宽度约束**
    `max-width: 100vw` 防止元素超出屏幕宽度



### <van-swipe计算有误

第二屏内容右边超出了背景5px左右，请解决

```
<div class="card-bg">
    <van-swipe 
        ref="swipeRef"
        :loop="false"
        :show-indicators="false"
        @change="onSwipeChange">
            <!-- 第一屏 -->
            <van-swipe-item>
            	<div class="info-group"></div>
            </van-swipe-item>
            <!-- 第二屏 -->
            <van-swipe-item>
            	<div class="info-group"></div>
            </van-swipe-item>
    </van-swipe>
</div>

.card-bg \\{
    padding: 8px 10px;
    margin-bottom: 8px;
    border-radius: 6px;
    background: rgba(38, 126, 240, 0.06);
\\}
.info-group \\{
    display: flex;
    flex-direction: column;
    gap: 6px; /* 行间距 */
\\}
```

还是不行
渲染后card-bg和van-swipe都是292
但van-swipe-item是307
这可能是vant的bug？
请重新考虑修复



这个好像有点用

```
.van-swipe-item \\{
    width: calc(50\\% - 15px) !important;
    padding: 8px 10px;
    margin-right: 15px;
\\}
```

