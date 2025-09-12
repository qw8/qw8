---
title: VuePress
date: 2022-04-29 09:02:08
categories: 
- 前端知识
tags:
- vue
---

### 从头搭建一个简单的 VuePress 文档

#### 1.创建并进入一个新目录（也可以手动右键新建）

```bash
mkdir project && cd project
```

#### 2.使用你喜欢的包管理器进行初始化

```bash
yarn init
npm init
```

#### 3.将 VuePress 安装为本地依赖

已经不再推荐全局安装 VuePress

```bash
yarn add -D vuepress
npm install -D vuepress
```

如果你的现有项目依赖了 webpack 3.x，推荐使用 [Yarn ](https://classic.yarnpkg.com/zh-Hans/)而不是 npm 来安装 VuePress。因为在这种情形下，npm 会生成错误的依赖树。

#### 4.在project的根目录下新建docs文件夹：

这个文档将作为项目文档的根目录来使用：

```arduino
mkdir docs
```

#### 5.在docs文件夹下创建`.vuepress`文件夹：

```arduino
mkdir .vuepress
```

所有 VuePress 相关的文件都将会被放在这里

#### 6.在`.vuepress`文件夹下面创建`config.js`:

```mipsasm
touch config.js
```

config.js是VuePress必要的配置文件，它导出一个javascript对象。

你可以先加入如下配置：

```java
module.exports = \\{
	title: '秦伟博客', // 网站标题
	description: '前端、全栈、SEO的知识点、面试题与学习链接的整理',
	// 注入到当前页面的 HTML <head> 中的标签
	head: [
		['link', \\{ rel: 'icon', href: '/qw.ico' \\}], // 自定义的 favicon(网页标签的图标)
	],
	base: '/blogs/', // 这是部署到github相关的配置
	markdown: \\{
		lineNumbers: true // 代码块显示行号
	\\},
	themeConfig: \\{
		sidebarDepth: 2, // e'b将同时提取markdown中h2 和 h3 标题，显示在侧边栏上。
		lastUpdated: 'Last Updated', // 文档更新时间：每个文件git最后提交的时间
		// 导航栏配置
		nav: [
			\\{ text: '前端算法', link: '/algorithm/' \\}, // 内部链接 以docs为根目录
			\\{ text: '秦伟博客', link: 'http://blog.seoqp.com/' \\}, // 外部链接
			// 下拉列表
			\\{
				text: '个人',
				items: [\\{
					text: '秦伟博客',
					link: 'http://blog.seoqp.com/'
				\\}, \\{
					text: 'GitHub',
					link: 'https://github.com/qw8'
				\\}]
			\\}
		],
		// 侧边栏配置
		sidebar: \\{
			// docs文件夹下面的accumulate文件夹 文档中md文件 书写的位置(命名随意)
			'/accumulate/': [
				'/accumulate/', // accumulate文件夹的README.md 不是下拉框形式
				\\{
					title: '侧边栏下拉框的标题1',
					children: [
						'/accumulate/JS/test', // 以docs为根目录来查找文件 
						// 上面地址查找的是：docs>accumulate>JS>test.md 文件
						// 自动加.md 每个子选项的标题 是该md文件中的第一个h1/h2/h3标题
					]
				\\}
			],
			// docs文件夹下面的algorithm文件夹 这是第二组侧边栏 跟第一组侧边栏没关系
			'/algorithm/': [
				'/algorithm/',
				\\{
					title: '第二组侧边栏下拉框的标题1',
					children: [
						'/algorithm/simple/test'
					]
				\\}
			]
		\\}
	\\}
\\}
```

#### 7.在`.vuepress`文件夹下面创建public文件夹:

```arduino
mkdir public
```

这个文件夹是用来放置静态资源的，打包出来之后会放在.vuepress/dist/的根目录。

#### 8.首页(像VuePress文档主页一样)

在docs文件夹下面创建一个`README.md`：

默认的主题提供了一个首页，像下面一样设置`home:true`即可，可以把下面的设置放入`README.md`中，待会儿你将会看到跟`VuePress`一样的主页。

```yaml
---
home: true
heroImage: /logo.jpg
actionText: 快速上手 →
actionLink: /zh/guide/
features:
- title: 简洁至上
  details: 以 Markdown 为中心的项目结构，以最少的配置帮助你专注于写作。
- title: Vue驱动
  details: 享受 Vue + webpack 的开发体验，在 Markdown 中使用 Vue 组件，同时可以使用 Vue 来开发自定义主题。
- title: 高性能
  details: VuePress 为每个页面预渲染生成静态的 HTML，同时在页面被加载的时候，将作为 SPA 运行。
footer: MIT Licensed | Copyright © 2018-present Evan You
---
```

ps：你需要放一张logo.jpg图片到public文件夹中。

我们的项目结构已经搭好了：

```stylus
project
├─── docs
│   ├── README.md
│   └── .vuepress
│       ├── public
│       └── config.js
└── package.json
```

#### 9.在 `package.json` 里添加两个启动命令:

```json
\\{
  "scripts": \\{
    "docs:dev": "vuepress dev docs",
    "docs:build": "vuepress build docs"
  \\}
\\}
```

#### 10.在本地启动服务器

```bash
yarn docs:dev
npm run docs:dev
```

VuePress 会在 [http://localhost:8080 ](http://localhost:8080/)启动一个热重载的开发服务器。



### 修改默认颜色

#### 新建styles/palette.styl文件，并做如下配置

```
$accentColor = #90C54A // 默认主题颜色
$textColor = #2c3e50 // 默认字体颜色
$borderColor = #eaecef // 默认边框颜色
$codeBgColor = #f6f6f6 // 默认背景颜色
```

#### 修改代码字体默认白色

> node_modules
>
> _@vuepress_theme-default@1.9.7@@vuepress
>
> theme-default
>
> styles
>
> code.styl
>

删除第24行代码**color #fff**和第77行代码**color rgba(255, 255, 255, 0.3)**即可

### 代码行右边框颜色淡化

第95行代码66\\%改成10\\%

border-right 1px solid rgba(0, 0, 0, 10\\%)