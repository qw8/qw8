---
title: 秦伟博客
date: 2019-08-25 18:00:00
categories: 
- 其他
tags:
- 博客
- Hexo
---
### 博客介绍

Welcome to [QinWei‘s blog](http://qvchat.com/)!

本博客有以下分类：
- 前端知识
- 前端进阶
- 前端面试
- 前端文章
- 前端问题
- 链接
- SEO
- 其他

This is my first post.If you have any problems in using this website , you can contact me by QQ： <u>*124729081*</u> or  Wechat：<u>*qwqw75*</u>. 

<!--more-->

This website is built using[Hexo](https://hexo.io/zh-cn/), and here are some brief introduction.



### 文件夹目录

- node_modules: 依赖包
- public：存放生成的页面
- scaffolds：生成文章的一些模板
- source：用来存放你的文章
- themes：主题
- _config.yml: 博客的配置文件



### 博客运行部署

#### Create a new post（新建日志）

``` bash
$ hexo new "My New Post"
```

More info: [Writing](https://hexo.io/docs/writing.html)

#### Run server（运行服务）

``` bash
$ hexo server
```

使用ctrl+c可以把服务关掉。

More info: [Server](https://hexo.io/docs/server.html)

#### Generate static files（生成静态文件）

``` bash
$ hexo generate
```

More info: [Generating](https://hexo.io/docs/generating.html)

#### Deploy to remote sites（部署到远程站点）

``` bash
$ hexo deploy
```

More info: [Deployment](https://hexo.io/docs/deployment.html)



### 博客问题

#### 更改样式后网站没有生效

确认非缓存问题后，执行 `hexo clean` 再进行生成上传。

清理之前在public文件夹中生成的文件

#### hexo d生成HTML文件报错

错误代码：
FATAL Something's wrong. Maybe you can find the solution here: http://hexo.io/do cs/troubleshooting.html Template render error: (unknown path) [Line 1, Column 12] unexpected token: }}

问题原因：
看到其中有一句Template render error，模板渲染错误

看到渲染错误，我的md文档中不就有渲染的语法嘛，双大括号就是做渲染的语法，可能有冲突吧，有文章说有代码块包含就可以，那么我试试

```
// 有包含
\\\{\\\{\\\}\\\}
```


果然，hexo g试验了一下，果然是没有报错的，而我没有使用代码块包含双大括号的时候，就会报上面的错误代码

#### 如何在文章中使用图标

先到 [fontawesome](http://fontawesome.io/icons/) 找到你需要的图标名，比如：`book`，按以下格式使用：

```
<i class="icon icon-book"></i>
```

图标样式前缀均为 `icon`，此外还有 5 个图标大小调节类和 1 个间距类。

```
<!-- 1.3倍大小 -->
<i class="icon icon-book icon-lg"></i>
<!-- 2倍大小 -->
<i class="icon icon-book icon-2x"></i>
<!-- 3倍大小 -->
<i class="icon icon-book icon-3x"></i>
<!-- 4倍大小 -->
<i class="icon icon-book icon-4x"></i>
<!-- 5倍大小 -->
<i class="icon icon-book icon-5x"></i>
<!-- 5px右边距 -->
<i class="icon icon-book icon-pr"></i>
<!-- 5px左边距 -->
<i class="icon icon-book icon-pl"></i>
```

#### 个别图标无法显示

如果你的浏览器安装了 ADBlock，它会屏蔽 SNS 相关的内容，比如：Github。

解决办法：可配置 ADBlock 不在你的站点运行。

#### 本地ssh目录

```
C:\Users\tuitui\.ssh
```



### 主题添加字数统计和阅读时长功能

#### 1.安装 hexo-wordcount

在博客目录下打开Git Bash Here 输入命令

> npm i --save hexo-wordcount

#### 2.文件配置

```
// 单篇文章字数
<span class="post-count"><\\%= wordcount(post.content) \\%>字</span>
<span class="post-count"><\\%= min2read(post.content) \\%>分</span>
<span>本网站总字数：<\\%= totalcount(site) \\%></span>
```

在`theme\yilia\layout\_partial\post`下创建`word.ejs`文件：

```xml
<div style="margin-top:10px;">
    <span class="post-time">
      <span class="post-meta-item-icon">
        <i class="fa fa-keyboard-o"></i>
        <span class="post-meta-item-text">  字数统计: </span>
        <span class="post-count"><\\%= wordcount(post.content) \\%>字</span>
      </span>
    </span>

    <span class="post-time">
      &nbsp; | &nbsp;
      <span class="post-meta-item-icon">
        <i class="fa fa-hourglass-half"></i>
        <span class="post-meta-item-text">  阅读时长: </span>
        <span class="post-count"><\\%= min2read(post.content) \\%>分</span>
      </span>
    </span>
</div>
```

#### 3. 开启功能

在站点的`_config.yml`中添加下面代码

```php
# 是否开启字数统计
#不需要使用，直接设置值为false，或注释掉
word_count: true
```



### 中文链接转拼音

如果你的文章名称是中文的，那么 Hexo 默认生成的永久链接也会有中文，这样不利于 `SEO`，且 `gitment` 评论对中文链接也不支持。我们可以用 [hexo-permalink-pinyin](https://cloud.tencent.com/developer/tools/blog-entry?target=https\\%3A\\%2F\\%2Fgithub.com\\%2Fviko16\\%2Fhexo-permalink-pinyin&source=article&objectId=1952241) Hexo 插件使在生成文章时生成中文拼音的永久链接。 这里为可选安装，因为我希望使用`urlname`进行连接访问，中文链接转拼音由一个缺点就是当文章名字过长会显示十分臃肿。`urlname`的方式见下文。 安装命令如下：

```javascript
npm i hexo-permalink-pinyin --save
```

在 Hexo 根目录下的 `_config.yml` 文件中，新增以下的配置项：

```javascript
permalink_pinyin:
  enable: true
  separator: '-' # default: '-'
```

复制

>  **注**：除了此插件外，[hexo-abbrlink](https://cloud.tencent.com/developer/tools/blog-entry?target=https\\%3A\\%2F\\%2Fgithub.com\\%2Frozbo\\%2Fhexo-abbrlink&source=article&objectId=1952241) 插件也可以生成非中文的链接。



### 网站收录

为了使博客能被谷歌、bing、百度收录，最好生成 `sitemap` 方便爬取 

```
npm install hexo-generator-sitemap --save
```

_config.yml配置

```
# hexo-generator-sitemap为了使博客能被谷歌、bing、百度收录，最好生成 sitemap 方便爬取
# https://github.com/hexojs/hexo-generator-sitemap
sitemap:
  path: sitemap.xml
  # template: ./sitemap_template.xml
  rel: true
  tags: false
  categories: false
```







# 安装Hexo

所有必备的应用程序安装完成后，即可使用 npm 安装 Hexo。

```
$ npm install -g hexo-cli
```

### 进阶安装和使用

对于熟悉 npm 的进阶用户，可以仅局部安装 `hexo` 包。

```
$ npm install hexo
```

安装以后，可以使用以下两种方式执行 Hexo：

1. `npx hexo `
2. Linux 用户可以将 Hexo 所在的目录下的 `node_modules` 添加到环境变量之中即可直接使用 `hexo `：

```
echo 'PATH="$PATH:./node_modules/.bin"' >> ~/.profile
```

### Node.js版本限制

如果你坚持使用旧的 Node.js，你可以考虑安装 Hexo 的过去版本。

请注意，我们不提供对过去版本 Hexo 的错误修复。

我们强烈建议永远安装 [最新版本](https://www.npmjs.com/package/hexo?activeTab=versions) 的 Hexo，以及 [推荐的 Node.js 版本](https://hexo.io/zh-cn/docs/#安装前提)。

| Hexo 版本   | 最低版本 (Node.js 版本) | 最高版本 (Node.js 版本) |
| :---------- | :---------------------- | :---------------------- |
| 7.0+        | 14.0.0                  | latest                  |
| 6.2+        | 12.13.0                 | latest                  |
| 6.0+        | 12.13.0                 | 18.5.0                  |
| 5.0+        | 10.13.0                 | 12.0.0                  |
| 4.1 - 4.2   | 8.10                    | 10.0.0                  |
| 4.0         | 8.6                     | 8.10.0                  |
| 3.3 - 3.9   | 6.9                     | 8.0.0                   |
| 3.2 - 3.3   | 0.12                    | 未知                    |
| 3.0 - 3.1   | 0.10 或 iojs            | 未知                    |
| 0.0.1 - 2.8 | 0.10                    | 未知                    |



# 建站

安装 Hexo 完成后，请执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件。

```
$ hexo init <folder>
$ cd <folder>
$ npm install
```

新建完成后，指定文件夹的目录如下：

```
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```

### _config.yml

网站的 [配置](https://hexo.io/zh-cn/docs/configuration) 信息，您可以在此配置大部分的参数。

### package.json

应用程序的信息。[EJS](https://ejs.co/), [Stylus](http://learnboost.github.io/stylus/) 和 [Markdown](http://daringfireball.net/projects/markdown/) 渲染引擎 已默认安装，您可以自由移除。

```
\\{
  "name": "hexo-site",
  "version": "0.0.0",
  "private": true,
  "hexo": \\{
    "version": ""
  \\},
  "dependencies": \\{
    "hexo": "^7.0.0",
    "hexo-generator-archive": "^2.0.0",
    "hexo-generator-category": "^2.0.0",
    "hexo-generator-index": "^3.0.0",
    "hexo-generator-tag": "^2.0.0",
    "hexo-renderer-ejs": "^2.0.0",
    "hexo-renderer-stylus": "^3.0.0",
    "hexo-renderer-marked": "^6.0.0",
    "hexo-server": "^3.0.0",
    "hexo-theme-landscape": "^1.0.0"
  \\}
\\}
```

### scaffolds

[模版](https://hexo.io/zh-cn/docs/writing#模版（Scaffold）) 文件夹。当您新建文章时，Hexo 会根据 scaffold 来创建文件。

Hexo 的模板是指在新建的文章文件中默认填充的内容。例如，如果您修改 `scaffold/post.md` 中的 Front-matter 内容，那么每次新建一篇文章时都会包含这个修改。

### source

资源文件夹是存放用户资源的地方。除 `_posts` 文件夹之外，开头命名为 `_` (下划线)的文件 / 文件夹和隐藏的文件将会被忽略。Markdown 和 HTML 文件会被解析并放到 `public` 文件夹，而其他文件会被拷贝过去。

### themes

[主题](https://hexo.io/zh-cn/docs/themes) 文件夹。Hexo 会根据主题来生成静态页面。



# 配置

您可以在 `_config.yml` 或 [代替配置文件](https://hexo.io/zh-cn/docs/configuration#使用代替配置文件) 中修改大部分的配置。

## 网站

| 参数          | 描述                                                         |
| :------------ | :----------------------------------------------------------- |
| `title`       | 网站标题                                                     |
| `subtitle`    | 网站副标题                                                   |
| `description` | 网站描述                                                     |
| `keywords`    | 网站的关键词。支持多个关键词。                               |
| `author`      | 您的名字                                                     |
| `language`    | 网站使用的语言。对于简体中文用户来说，使用不同的主题可能需要设置成不同的值，请参考你的主题的文档自行设置，常见的有 `zh-Hans`和 `zh-CN`。 |
| `timezone`    | 网站时区。Hexo 默认使用您电脑的时区。请参考 [时区列表](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) 进行设置，如 `America/New_York`, `Japan`, 和 `UTC` 。一般的，对于中国大陆地区可以使用 `Asia/Shanghai`。 |

其中，`description` 主要用于SEO，告诉搜索引擎一个关于您站点的简单描述，通常建议在其中包含您网站的关键词。`author` 参数用于主题显示文章的作者。

## 网址

| 参数                         | 描述                                                         | 默认值                      |
| :--------------------------- | :----------------------------------------------------------- | :-------------------------- |
| `url`                        | 网址, 必须以 `http://` 或 `https://` 开头                    |                             |
| `root`                       | 网站根目录                                                   | `url's pathname`            |
| `permalink`                  | 文章的 [永久链接](https://hexo.io/zh-cn/docs/permalinks) 格式 | `:year/:month/:day/:title/` |
| `permalink_defaults`         | 永久链接中各部分的默认值                                     |                             |
| `pretty_urls`                | 改写 [`permalink`](https://hexo.io/zh-cn/docs/variables) 的值来美化 URL |                             |
| `pretty_urls.trailing_index` | 是否在永久链接中保留尾部的 `index.html`，设置为 `false` 时去除 | `true`                      |
| `pretty_urls.trailing_html`  | 是否在永久链接中保留尾部的 `.html`, 设置为 `false` 时去除 (*对尾部的 `index.html`无效*) | `true`                      |

> 网站存放在子目录
>
> 如果您的网站存放在子目录中，例如 `http://example.com/blog`，则请将您的 `url` 设为 `http://example.com/blog` 并把 `root` 设为 `/blog/`。

例如：

```
# 比如，一个页面的永久链接是 http://example.com/foo/bar/index.html
pretty_urls:
  trailing_index: false
# 此时页面的永久链接会变为 http://example.com/foo/bar/
```

## 目录

| 参数           | 描述                                                         | 默认值           |
| :------------- | :----------------------------------------------------------- | :--------------- |
| `source_dir`   | 资源文件夹，这个文件夹用来存放内容。                         | `source`         |
| `public_dir`   | 公共文件夹，这个文件夹用于存放生成的站点文件。               | `public`         |
| `tag_dir`      | 标签文件夹                                                   | `tags`           |
| `archive_dir`  | 归档文件夹                                                   | `archives`       |
| `category_dir` | 分类文件夹                                                   | `categories`     |
| `code_dir`     | Include code 文件夹，`source_dir` 下的子目录                 | `downloads/code` |
| `i18n_dir`     | 国际化（i18n）文件夹                                         | `:lang`          |
| `skip_render`  | 跳过指定文件的渲染。匹配到的文件将会被不做改动地复制到 `public` 目录中。您可使用 [glob 表达式](https://github.com/micromatch/micromatch#extended-globbing)来匹配路径。 |                  |

例如：

```
skip_render: "mypage/**/*"
# 将会直接将 `source/mypage/index.html` 和 `source/mypage/code.js` 不做改动地输出到 'public' 目录
# 你也可以用这种方法来跳过对指定文章文件的渲染
skip_render: "_posts/test-post.md"
# 这将会忽略对 'test-post.md' 的渲染
```

> 提示
>
> 如果您刚刚开始接触 Hexo，通常没有必要修改这一部分的值。

## 文章

| 参数                    | 描述                                                         | 默认值         |
| :---------------------- | :----------------------------------------------------------- | :------------- |
| `new_post_name`         | 新文章的文件名称                                             | `:title.md`    |
| `default_layout`        | 预设布局                                                     | `post`         |
| `auto_spacing`          | 在中文和英文之间加入空格                                     | `false`        |
| `titlecase`             | 把标题转换为 title case                                      | `false`        |
| `external_link`         | 在新标签中打开链接                                           | `true`         |
| `external_link.enable`  | 在新标签中打开链接                                           | `true`         |
| `external_link.field`   | 对整个网站（`site`）生效或仅对文章（`post`）生效             | `site`         |
| `external_link.exclude` | 需要排除的域名。主域名和子域名如 `www` 需分别配置            | `[]`           |
| `filename_case`         | 把文件名称转换为 (1) 小写或 (2) 大写                         | `0`            |
| `render_drafts`         | 显示草稿                                                     | `false`        |
| `post_asset_folder`     | 启用 [资源文件夹](https://hexo.io/zh-cn/docs/asset-folders)  | `false`        |
| `relative_link`         | 把链接改为与根目录的相对位址                                 | `false`        |
| `future`                | 显示未来的文章                                               | `true`         |
| `syntax_highlighter`    | 代码块的设置, 请参考 [代码高亮](https://hexo.io/zh-cn/docs/syntax-highlight) 进行设置 | `highlight.js` |
| `highlight`             | 代码块的设置, 请参考 [Highlight.js](https://hexo.io/zh-cn/docs/syntax-highlight#Highlight-js) 进行设置 |                |
| `prismjs`               | 代码块的设置, 请参考 [PrismJS](https://hexo.io/zh-cn/docs/syntax-highlight#PrismJS) 进行设置 |                |

> 相对地址
>
> 默认情况下，Hexo 生成的超链接都是绝对地址。例如，如果您的网站域名为 `example.com`，您有一篇文章名为 `hello`，那么绝对链接可能像这样：`http://example.com/hello.html`，它是**绝对**于域名的。相对链接像这样：`/hello.html`，也就是说，无论用什么域名访问该站点，都没有关系，这在进行反向代理时可能用到。通常情况下，建议使用绝对地址。

## 分类 & 标签

| 参数               | 描述     | 默认值          |
| :----------------- | :------- | :-------------- |
| `default_category` | 默认分类 | `uncategorized` |
| `category_map`     | 分类别名 |                 |
| `tag_map`          | 标签别名 |                 |

## 日期 / 时间格式

Hexo 使用 [Moment.js](http://momentjs.com/) 来解析和显示时间。

| 参数             | 描述                                                         | 默认值       |
| :--------------- | :----------------------------------------------------------- | :----------- |
| `date_format`    | 日期格式                                                     | `YYYY-MM-DD` |
| `time_format`    | 时间格式                                                     | `HH:mm:ss`   |
| `updated_option` | 当 Front Matter 中没有指定 [`updated`](https://hexo.io/zh-cn/docs/variables#页面变量) 时 `updated` 的取值 | `mtime`      |

> updated_option
>
> `updated_option` 控制了当 Front Matter 中没有指定 `updated` 时，`updated` 如何取值：
>
> - `mtime`: 使用文件的最后修改时间。这是从 Hexo 3.0.0 开始的默认行为。
> - `date`: 使用 `date` 作为 `updated` 的值。可被用于 Git 工作流之中，因为使用 Git 管理站点时，文件的最后修改日期常常会发生改变
> - `empty`: 直接删除 `updated`。使用这一选项可能会导致大部分主题和插件无法正常工作。
>
> `use_date_for_updated` 选项已经在 v7.0.0+ 中被移除。请改为使用 `updated_option: 'date'`。

## 分页

| 参数             | 描述                                | 默认值 |
| :--------------- | :---------------------------------- | :----- |
| `per_page`       | 每页显示的文章量 (0 = 关闭分页功能) | `10`   |
| `pagination_dir` | 分页目录                            | `page` |

例如：

```
pagination_dir: 'page'
# http://example.com/page/2

pagination_dir: 'awesome-page'
# http://example.com/awesome-page/2
```

## 扩展

| 参数             | 描述                                                         |
| :--------------- | :----------------------------------------------------------- |
| `theme`          | 当前主题名称。值为`false`时禁用主题                          |
| `theme_config`   | 主题的配置文件。在这里放置的配置会覆盖主题目录下的 `_config.yml` 中的配置 |
| `deploy`         | 部署部分的设置                                               |
| `meta_generator` | [Meta generator](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/meta#属性) 标签。 值为 `false` 时 Hexo 不会在头部插入该标签 |

### 包括或不包括目录和文件

在 Hexo 配置文件中，通过设置 include/exclude 可以让 Hexo 进行处理或忽略某些目录和文件夹。你可以使用 [glob 表达式](https://github.com/isaacs/minimatch) 对目录和文件进行匹配。

`include` 和 `exclude` 选项只会应用到 `source/` ，而 `ignore` 选项会应用到所有文件夹.

| 参数      | 描述                                                         |
| :-------- | :----------------------------------------------------------- |
| `include` | Hexo 默认会不包括 `source/` 下的文件和文件夹（包括名称以下划线和 `.` 开头的文件和文件夹，Hexo 的 `_posts` 和 `_data` 等目录除外）。通过设置此字段将使 Hexo 处理他们并将它们复制到 `source` 目录下。 |
| `exclude` | Hexo 不包括 `source/` 下的这些文件和目录                     |
| `ignore`  | Hexo 会忽略整个 Hexo 项目下的这些文件夹或文件                |

例如：

```
# 处理或不处理目录或文件
include:
  - ".nojekyll"
  # 处理 'source/css/_typing.css'
  - "css/_typing.css"
  # 处理 'source/_css/' 中的任何文件，但不包括子目录及其其中的文件。
  - "_css/*"
  # 处理 'source/_css/' 中的任何文件和子目录下的任何文件
  - "_css/**/*"

exclude:
  # 不处理 'source/js/test.js'
  - "js/test.js"
  # 不处理 'source/js/' 中的文件、但包括子目录下的所有目录和文件
  - "js/*"
  # 不处理 'source/js/' 中的文件和子目录下的任何文件
  - "js/**/*"
  # 不处理 'source/js/' 目录下的所有文件名以 'test' 开头的文件，但包括其它文件和子目录下的单文件
  - "js/test*"
  # 不处理 'source/js/' 及其子目录中任何以 'test' 开头的文件
  - "js/**/test*"
  # 不要用 exclude 来忽略 'source/_posts/' 中的文件。你应该使用 'skip_render'，或者在要忽略的文件的文件名之前加一个下划线 '_'
  # 在这里配置一个 - "_posts/hello-world.md" 是没有用的。

ignore:
  # 忽略任何一个名叫 'foo' 的文件夹
  - "**/foo"
  # 只忽略 'themes/' 下的 'foo' 文件夹
  - "**/themes/*/foo"
  # 对 'themes/' 目录下的每个文件夹中忽略名叫 'foo' 的子文件夹
  - "**/themes/**/foo"
```

列表中的每一项都必须用单引号或双引号包裹起来。

`include` 和 `exclude` 并不适用于 `themes/` 目录下的文件。如果需要忽略 `themes/` 目录下的部分文件或文件夹，可以使用 `ignore` 或在文件名之前添加下划线 `_`。

- `source/_posts` 文件夹是一个例外，但该文件夹下任何名称以 `_` 开头的文件或文件夹仍会被忽略。不建议在该文件夹中使用 `include` 规则。

### 使用代替配置文件

可以在 hexo-cli 中使用 `--config` 参数来指定自定义配置文件的路径。你可以使用一个 YAML 或 JSON 文件的路径，也可以使用逗号分隔（无空格）的多个 YAML 或 JSON 文件的路径。例如：

```
# 用 'custom.yml' 代替 '_config.yml'
$ hexo server --config custom.yml

# 使用 'custom.yml' 和 'custom2.json'，优先使用 'custom3.yml'，然后是 'custom2.json'
$ hexo generate --config custom.yml,custom2.json,custom3.yml
```

当你指定了多个配置文件以后，Hexo 会按顺序将这部分配置文件合并成一个 `_multiconfig.yml`。如果遇到重复的配置，排在后面的文件的配置会覆盖排在前面的文件的配置。这个原则适用于任意数量、任意深度的 YAML 和 JSON 文件。

例如，使用 `--config` 指定了两个自定义配置文件：

```
$ hexo generate --config custom.yml,custom2.json
```

如果 `custom.yml` 中指定了 `foo: bar`，在 custom2.json 中指定了 `"foo": "dinosaur"`，那么在 `_multiconfig.yml` 中你会得到 `foo: dinosaur`。

### 使用代替主题配置文件

通常情况下，Hexo 主题是一个独立的项目，并拥有一个独立的 `_config.yml` 配置文件。

除了自行维护独立的主题配置文件，你也可以在其它地方对主题进行配置。

**配置文件中的 `theme_config`**

> 该特性自 Hexo 2.8.2 起提供

```
# _config.yml
theme: "my-theme"
theme_config:
  bio: "My awesome bio"
  foo:
    bar: 'a'
```

```
# themes/my-theme/_config.yml
bio: "Some generic bio"
logo: "a-cool-image.png"
  foo:
    baz: 'b'
```

最终主题配置的输出是：

```
\\{
  bio: "My awesome bio",
  logo: "a-cool-image.png",
  foo: \\{
    bar: "a",
    baz: "b"
  \\}
\\}
```

**独立的 `_config.[theme].yml` 文件**

> 该特性自 Hexo 5.0.0 起提供

独立的主题配置文件应放置于站点根目录下，支持 `yml` 或 `json` 格式。需要配置站点 `_config.yml` 文件中的 `theme` 以供 Hexo 寻找 `_config.[theme].yml` 文件。

```
# _config.yml
theme: "my-theme"
```

```
# _config.my-theme.yml
bio: "My awesome bio"
foo:
  bar: 'a'
```

```
# themes/my-theme/_config.yml
bio: "Some generic bio"
logo: "a-cool-image.png"
  foo:
    baz: 'b'
```

最终主题配置的输出是：

```
\\{
  bio: "My awesome bio",
  logo: "a-cool-image.png",
  foo: \\{
    bar: "a",
    baz: "b"
  \\}
\\}
```

> 我们强烈建议你将所有的主题配置集中在一处。如果你不得不在多处配置你的主题，那么这些信息对你将会非常有用：Hexo 在合并主题配置时，Hexo 配置文件中的 `theme_config` 的优先级最高，其次是 `_config.[theme].yml` 文件，最后是位于主题目录下的 `_config.yml` 文件。



# 指令

### init

```
$ hexo init [folder]
```

新建一个网站。如果没有设置 `folder` ，Hexo 默认在目前的文件夹建立网站。

本命令相当于执行了以下几步：

1. Git clone [hexo-starter](https://github.com/hexojs/hexo-starter) 和 [hexo-theme-landscape](https://github.com/hexojs/hexo-theme-landscape) 主题到当前目录或指定目录。
2. 使用 [Yarn 1](https://classic.yarnpkg.com/lang/en/)、[pnpm](https://pnpm.io/zh/) 或 [npm](https://docs.npmjs.com/cli/install) 包管理器下载依赖（如有已安装多个，则列在前面的优先）。npm 默认随 [Node.js](https://hexo.io/zh-cn/docs/index.html#安装-Node-js) 安装。



### new

```
$ hexo new [layout] <title>
```

新建一篇文章。如果没有设置 `layout` 的话，默认使用 [_config.yml](https://hexo.io/zh-cn/docs/configuration) 中的 `default_layout` 参数代替。如果标题包含空格的话，请使用引号括起来。

```
$ hexo new "post title with whitespace"
```

| 参数              | 描述                                          |
| :---------------- | :-------------------------------------------- |
| `-p`, `--path`    | 自定义新文章的路径                            |
| `-r`, `--replace` | 如果存在同名文章，将其替换                    |
| `-s`, `--slug`    | 文章的 Slug，作为新文章的文件名和发布后的 URL |

默认情况下，Hexo 会使用文章的标题来决定文章文件的路径。对于独立页面来说，Hexo 会创建一个以标题为名字的目录，并在目录中放置一个 `index.md` 文件。你可以使用 `--path` 参数来覆盖上述行为、自行决定文件的目录：

```
hexo new page --path about/me "About me"
```

以上命令会创建一个 `source/about/me.md` 文件，同时 Front Matter 中的 title 为 `"About me"`

注意！title 是必须指定的！如果你这么做并不能达到你的目的：

```
hexo new page --path about/me
```

此时 Hexo 会创建 `source/_posts/about/me.md`，同时 `me.md` 的 Front Matter 中的 title 为 `"page"`。这是因为在上述命令中，hexo-cli 将 `page` 视为指定文章的标题、并采用默认的 `layout`。



### generate

```
$ hexo generate
```

生成静态文件。

| 选项                  | 描述                                                         |
| :-------------------- | :----------------------------------------------------------- |
| `-d`, `--deploy`      | 文件生成后立即部署网站                                       |
| `-w`, `--watch`       | 监视文件变动                                                 |
| `-b`, `--bail`        | 生成过程中如果发生任何未处理的异常则抛出异常                 |
| `-f`, `--force`       | 强制重新生成文件 Hexo 引入了差分机制，如果 `public` 目录存在，那么 `hexo g` 只会重新生成改动的文件。 使用该参数的效果接近 `hexo clean && hexo generate` |
| `-c`, `--concurrency` | 最大同时生成文件的数量，默认无限制                           |

该命令可以简写为

```
$ hexo g
```



### publish

```
$ hexo publish [layout] <filename>
```

发表草稿。



### server

```
$ hexo server
```

启动服务器。默认情况下，访问网址为： `http://localhost:4000/`。

| 选项             | 描述                           |
| :--------------- | :----------------------------- |
| `-p`, `--port`   | 重设端口                       |
| `-s`, `--static` | 只使用静态文件                 |
| `-l`, `--log`    | 启动日记记录，使用覆盖记录格式 |



### deploy

```
$ hexo deploy
```

部署网站。

| 参数               | 描述                     |
| :----------------- | :----------------------- |
| `-g`, `--generate` | 部署之前预先生成静态文件 |

该命令可以简写为：

```
$ hexo d
```



### render

```
$ hexo render <file1> [file2] ...
```

渲染文件。

| 参数             | 描述         |
| :--------------- | :----------- |
| `-o`, `--output` | 设置输出路径 |



### migrate

```
$ hexo migrate <type>
```

从其他博客系统 [迁移内容](https://hexo.io/zh-cn/docs/migration)。



### clean

```
$ hexo clean
```

清除缓存文件 (`db.json`) 和已生成的静态文件 (`public`)。

在某些情况（尤其是更换主题后），如果发现您对站点的更改无论如何也不生效，您可能需要运行该命令。



### list

```
$ hexo list <type>
```

列出网站数据。



### version

```
$ hexo version
```

显示 Hexo 版本。



### config

```
$ hexo config [key] [value]
```

列出网站的配置（`_config.yml`）。如果指定了 `key`，则只展示配置中对应 `key` 的值；如果同时指定了 `key` 和 `value`，则将配置中对应的 `key` 的值修改为 `value`。



## 选项

### 安全模式

```
$ hexo --safe
```

在安全模式下，不会加载插件和脚本。当您在安装新插件遭遇问题时，可以尝试以安全模式重新执行。

### 调试模式

```
$ hexo --debug
```

在终端中显示调试信息并记录到 `debug.log`。当您碰到问题时，可以尝试用调试模式重新执行一次，并 [提交调试信息到 GitHub](https://github.com/hexojs/hexo/issues/new?assignees=&labels=&projects=&template=bug_report.yml)。

### 简洁模式

```
$ hexo --silent
```

隐藏终端信息。

### 自定义配置文件的路径

```
# 使用 custom.yml 代替默认的 _config.yml
$ hexo server --config custom.yml

# 使用 custom.yml 和 custom2.json，其中 custom2.json 优先级更高
$ hexo generate --config custom.yml,custom2.json,custom3.yml
```

自定义配置文件的路径，指定这个参数后将不再使用默认的 `_config.yml`。
你可以使用一个 YAML 或 JSON 文件的路径，也可以使用逗号分隔（无空格）的多个 YAML 或 JSON 文件的路径。例如：

```
# 使用 custom.yml 代替默认的 _config.yml
$ hexo server --config custom.yml

# 使用 custom.yml, custom2.json 和 custom3.yml，其中 custom3.yml 优先级最高，其次是 custom2.json
$ hexo generate --config custom.yml,custom2.json,custom3.yml
```

当你指定了多个配置文件以后，Hexo 会按顺序将这部分配置文件合并成一个 `_multiconfig.yml`。如果遇到重复的配置，排在后面的文件的配置会覆盖排在前面的文件的配置。这个原则适用于任意数量、任意深度的 YAML 和 JSON 文件。

### 显示草稿

```
$ hexo --draft
```

显示 `source/_drafts` 文件夹中的草稿文章。

### 自定义 CWD

```
$ hexo --cwd /path/to/cwd
```

自定义当前工作目录（Current working directory）的路径。



### 主题

#### Solitude

https://solitude-docs.efu.me/

#### shoka

https://www.kaitaku.xyz/

yilia-plus

matery

3-hexo

#### Butterfly

https://blog.270916.xyz/

#### Cuteen

https://blog.moej.cn/



### 免费托管静态网页

GitHub 页面 - https://pages.github.com/

Vercel- https://vercel.com/

Netlify - https://www.netlify.com/

Heroku - https://www.heroku.com/

亚马逊 S3 - https://aws.amazon.com/s3/
Firebase 托管 - https://firebase.google.com/products/hosting/
激增 - https://surge.sh/
GitLab 页面 - https://docs.gitlab.com/ee/user/project/pages/
Bitbucket - https://bitbucket.org/product/features/pages
GitBook - https://www.gitbook.com/
渲染 - https://render.com/
谷歌云存储 - https://cloud.google.com/storage/
DigitalOcean 空间 - https://www.digitalocean.com/products/spaces/
Cloudflare 页面 - https://pages.cloudflare.com/
Azure 静态 Web 应用 -
https://azure.microsoft.com/en-us/services/app-service/static/
AWS Amplify - https://aws.amazon.com/amplify/