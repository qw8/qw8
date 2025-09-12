---
title: vite
date: 2024-03-06 21:02:08
categories: 
- 前端知识
tags:
- vue
- vite
---

### vue3的vite中图片的动态加载

#### 将图片资源放入public目录下

```
let myIcon = new BMap.Icon("/map_pin_red.png", new BMap.Size(21, 30));
```


我们看到实际上我们不希望资源文件被vite编译可以把图片放到public 目录会更省事，不管是开发环境还是生产环境，可以始终以根目录保持图片路径的一致。

> public 目录# 如果你有下列这些资源： 不会被源码引用（例如 robots.txt） 必须保持原有文件名（没有经过 hash） ...或者你压根不想引入该资源，只是想得到其 URL。 那么你可以将该资源放在指定的 public 目录中，它应位于你的项目根目录。该目录中的资源在开发时能直接通过 / 根路径访问到，并且打包时会被完整复制到目标目录的根目录下。 目录默认是 <root>/public，但可以通过 publicDir 选项 来配置。 请注意： 引入 public 中的资源永远应该使用根绝对路径 —— 举个例子，public/icon.png 应该在源码中被引用为 /icon.png。 public 中的资源不应该被 JavaScript 文件引用。
>

```
/**
 * @description: 动态加载图片 （注意：将图片放到public目录下）
 * @param \\{*\\} imgUrl public目录下图片的地址：eg: /public/imgs/a.png, 则imgUrl为 ./imgs/a.png
 * @return \\{*\\} 返回图片的绝对路径
 */
const loadPicture = (imgUrl) => \\{
	let pathnameArr = location.pathname.split("/");
	let realPathArr = []
	pathnameArr.forEach(item =>\\{
		if( item && item.slice(-5) !== '.html')\\{
			realPathArr.push(item)
		\\}
	\\})
	let realPath = location.origin + "/"
	if(realPathArr.length > 0)\\{
		realPath = realPath + realPathArr.join('/') + "/"
	\\}
	return new URL(imgUrl, realPath).href;
\\}
```

#### 将图片放入assets目录下

##### 第一种方式（适用于处理单个链接的资源文件）

```javascript
import homeIcon from '@/assets/images/home/home_icon.png'

<img :src="homeIcon" />
```

##### 第二种方式----- 图片在src目录下（适用于处理多个链接的资源文件）

[vite官网的静态资源引入参考地址](https://cn.vitejs.dev/guide/assets.html)
`new URL() + import.meta.url`

@/utils/index.js中

```javascript
// 获取assets静态资源路径
export const getAssets = (url) => \\{
  return new URL(`../assets/images/$\\{url\\}`, import.meta.url).href
\\}
```

注意：这里只能通过 …/…/ 这种方式去获取路径，无法通过@/assets

页面中

```
import \\{ getAssets \\} from '@/utils/index'

<img :src="getAssets(`home/cover$\\{activeIndex\\}@2x.png`)" alt="">
```

##### 补充：如果是背景图片引入的方式（一定要使用相对路径）

```
.imgText \\{
	background-image: url('../../assets/images/1462466500644.jpg');
\\}
```

生产环境会自动加上hash，并且路径正确

![img](https://img.jbzj.com/file_images/article/202303/2023032009564213.png)

以下错误用法，使用绝对路径在开发环境能够正常显示，但将导致打包后的路径不正确

```
.imgText \\{
	background-image: url('src/assets/images/1462466500644.jpg');
\\}
```

生产环境资源404：

![img](https://img.jbzj.com/file_images/article/202303/2023032009564214.png)



### 优缺点

在 Vite 项目中，推荐优先使用方法一（直接路径引用），这是更符合 Vite 官方推荐的静态资源处理方式。以下是具体分析：

------

**方法一优势（推荐）**

```html
<img src="@/assets/images/components/share1@2x.png" alt="">
```

1. 构建时优化
    Vite 会自动识别这种静态引用，在构建时会：
    • 生成带哈希的文件名（长期缓存）

   • 对图片进行压缩（当配置 build.assetsInlineLimit）

   • 自动处理路径别名转换

2. 开发体验更好
    支持 HMR 热更新（修改图片后自动刷新）

3. 代码更简洁
    直观的路径声明，无需额外工具函数

------

**方法二适用场景**

```html
<img :src="getAssets('employee/mask@2x.png')" alt />
```

仅在以下情况使用这种动态路径：

1. 需要拼接动态路径（如根据变量生成路径） 

   ```
   const imagePath = ref('a.png')
   getAssets(`categories/$\\{imagePath.value\\}`)
   ```

2. 处理非标准目录结构
    当资源不在 Vite 默认识别的 `assets` 目录时

------

**两者的本质区别**

| 特性         | 方法一（直接引用） | 方法二（new URL） |
| ------------ | ------------------ | ----------------- |
| 构建处理     | ✅ 预优化/压缩      | ❌ 仅路径转换      |
| 路径解析时机 | 构建时             | 运行时            |
| 热更新支持   | ✅                  | ❌                 |
| 动态路径能力 | ❌                  | ✅                 |

------

**最终建议**
 • 对于固定路径的图片资源，坚持使用方法一

• 仅当需要动态拼接路径时，才使用工具函数方法二

• 如果使用 TypeScript，可以为 `getAssets` 添加类型声明：

```ts
declare const getAssets: (url: string) => string;
```

------

**补充：Vite 静态资源规范**
 Vite 官方推荐将需要优化的资源放在：

1. `src/assets` - 通过路径别名直接引用
2. `public/` - 通过绝对路径 `/icon.png` 引用（原样复制，不优化）

应根据资源类型选择合适的目录存放。



## vite项目加载图片失败

在Vite项目中图片加载失败通常与**资源路径处理**或**构建配置**有关。以下是常见原因及解决方案：

------

### 1. **静态资源引用方式错误（最常见）**

Vite要求使用**ES模块导入**或**绝对路径**引用资源：

#### ✅ 正确方式（JavaScript/TS中）：

```
// 方式1：显式导入（推荐）
import logo from '@/assets/images/logo.png'; // 使用别名

// 方式2：动态URL（适用于变量路径）
const imgUrl = new URL('./assets/image.png', import.meta.url).href;

// 在模板中使用
<img :src="logo" /> 或 <img :src="imgUrl" />
```

#### ✅ CSS/SCSS中：

```
/* 相对路径会自动处理 */
.bg \\{
  background: url(../assets/bg.jpg);
\\}
```

#### ❌ 错误方式：

```
<!-- 直接使用字符串路径（除非在public目录） -->
<img src="@/assets/image.png" /> <!-- 编译后路径可能失效 -->
```

------

### 2. **未配置路径别名**

若使用了`@/assets`等别名，需确认`vite.config.js`已设置：

```
// vite.config.js
import \\{ defineConfig \\} from 'vite';
import path from 'path';

export default defineConfig(\\{
  resolve: \\{
    alias: \\{
      '@': path.resolve(__dirname, './src'), // 确保路径正确
    \\},
  \\},
\\});
```

------

### 3. **文件路径大小写问题**

Linux系统**区分大小写**，确认路径与文件名大小写完全匹配：

```
assets/Image.png  ➜ 引用时写成 assets/image.png 会失败
```

------

### 4. **图片未放对位置**

- **`src/assets`**：需通过import引用的资源

- `public/`

  ：直接通过绝对路径访问（不会经过构建处理） 

  ```
  <!-- public/images/logo.png -->
  <img src="/images/logo.png" />
  ```

------

### 5. **构建后路径错误**

生产环境部署到子路径时需配置`base`选项：

```
// vite.config.js
export default defineConfig(\\{
  base: '/your-subpath/', // 若部署到域名子目录
\\});
```

------

### 6. 检查网络请求路径

在浏览器DevTools的**Network标签**中查看：

- 图片请求是否返回404？

- 实际请求路径与预期是否一致？ 

  ```
  Expected: /src/assets/logo.png
  Actual:   /assets/logo.03d8ff.png  <!-- 构建后哈希路径正常 -->
  ```

------

### 完整示例：动态加载图片

```
<script setup>
// 静态导入
import staticImage from '@/assets/static.png';

// 动态路径（根据变量加载）
const getImage = (name) => \\{
  return new URL(`./assets/$\\{name\\}.png`, import.meta.url).href;
\\};
</script>

<template>
  <!-- 方式1: 静态导入 -->
  <img :src="staticImage" />
  
  <!-- 方式2: 动态生成URL -->
  <img :src="getImage('banner')" />
</template>
```

------

通过以上步骤排查，90\\%的图片加载问题可解决。重点检查**资源引用方式**和**构建路径配置**。