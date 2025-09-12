---
title: npm
date: 2019-11-24 11:10:20
categories: 
- 前端知识
tags:
- npm
- node
---

### NPM介绍

NPM是随同NodeJS一起安装的包管理工具，能解决NodeJS代码部署上的很多问题，常见的使用场景有以下几种：

+ 允许用户从NPM服务器下载别人编写的第三方包到本地使用。
+ 允许用户从NPM服务器下载并安装别人编写的命令行程序到本地使用。
+ 允许用户将自己编写的包或命令行程序上传到NPM服务器供别人使用。



### 常用命令

```
// 检测是否安装及版本
npm -v

// 使用npm命令安装模块
npm install <Module Name>
// 缩写
npm i <Module Name>

// 生成package.json文件
npm init
```

package.json用来描述项目中用到的模块和其他信息

#### 安装模块

```
npm install # 安装package.json定义好的模块，简写 npm i

# 安装包指定模块
npm i <ModuleName>

# 全局安装
npm i <ModuleName> -g 

# 安装包的同时，将信息写入到package.json中的 dependencies 配置中
npm i <ModuleName> --save

# 安装包的同时，将信息写入到package.json中的 devDependencies 配置中
npm i <ModuleName> --save-dev

# 安装多模块
npm i <ModuleName1> <ModuleName2>

# 安装方式参数：
-save # 简写-S，加入到生产依赖中
-save-dev # 简写-D，加入到开发依赖中
-g # 全局安装 将安装包放在 /usr/local 下或者你 node 的安装目录
```

#### 查看

```
# 查看所有全局安装的包
npm ls -g

# 查看本地项目中安装的包
npm ls

# 查看包的 package.json文件
npm view <ModuleName>

# 查看包的依赖关系
npm view <ModuleName> dependencies

# 查看包的源文件地址
npm view <ModuleName> repository.url

# 查看包所依赖的node版本
npm view <ModuleName> engines

# 查看帮助
npm help
```

#### 更新模块

```
# 更新本地模块
npm update <ModuleName>

# 更新全局模块
npm update -g <ModuleName> # 更新全局软件包。
npm update -g # 更新所有的全局软件包。
npm outdated -g --depth=0 # 找出需要更新的包。
```

#### 卸载模块

```
# 卸载本地模块
npm uninstall <ModuleName>

# 卸载全局模块
npm uninstall -g <ModuleName> # 卸载全局软件包。
```

#### 清空缓存

```
# 清空npm缓存
npm cache clear
```

#### 使用淘宝镜像

```
# 使用淘宝镜像
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

#### 其他

```
# 更改包内容后进行重建
npm rebuild <ModuleName>

# 检查包是否已经过时，此命令会列出所有已经过时的包，可以及时进行包的更新
npm outdated

# 访问npm的json文件，此命令将会打开一个网页
npm help json

# 发布一个包的时候，需要检验某个包名是否存在
npm search <ModuleName>

# 撤销自己发布过的某个版本代码
npm unpublish <package> <version>
```

#### 使用技巧

多次安装不成功尝试先清除缓存

```
npm cache clean -f
```

查看已安装的依赖包版本号

```
npm ls <ModuleName>
```

注意：用此方法才能准确的知道项目使用的版本号，查看package.json时，有“^" 符号表示大于此版本



### nrm的作用与使用

#### nrm是什么？

nrm(npm registry manager )是npm的镜像源管理工具，有时候国外资源太慢，使用这个就可以快速地在 npm 源间切换

#### nrm的安装

```
npm install -g nrm
```

#### nrm命令

```
nrm ls　#查看可用的源（有*号的表示当前所使用的源,以下<registry>表示源的名称）
nrm use <registry> # 将npm下载源切换成指定的源
nrm add <registry> <url> # 添加源，url为源的路径
nrm del <registry> # 删除源
nrm test <registry> # 测试源的响应时间，可以作为使用哪个源的参考

nrm help　# 查看nrm帮助
nrm home <registry>　# 跳转到指定源的官网
```

#### nrm使用

如果在你的网络不太理想或者受到其他网络限制导致不能使用npm原本的源进行下载时，nrm就非常有用了，你只需要：

nrm使用
如果在你的网络不太理想或者受到其他网络限制导致不能使用npm原本的源进行下载时，nrm就非常有用了，你只需要：

```
nrm ls # 查看可用的源
nrm use <registry>　# 切换到指定源
```



### 全局安装与本地安装

```
npm i koa      //本地安装
```

+ 将安装包放在 ./node_modules 下（运行 npm 命令时所在的目录），如果没有 node_modules 目录，会在当前执行 npm 命令的目录下生成 node_modules 目录。
+ 可以通过 require() 来引入本地安装的包。

```
npm i koa -g   //全局安装
```

+ 将安装包放在 /usr/local 下或者你 node 的安装目录。
+ 可以直接在命令行里使用。

npm install -save moduleName # -save 的意思是将模块安装到项目目录下，并在package文件的dependencies节点写入依赖。

npm install -save-dev moduleName # -save-dev 的意思是将模块安装到项目目录下，并在package文件的devDependencies节点写入依赖。

#### 查看安装信息

查看所有全局安装的模块

```
npm list -g
```

如果要查看某个模块的版本号，可以使用命令如下：

```
npm list koa -g
```

#### 使用 package.json

package.json 位于模块的目录下，用于定义包的属性。

Package.json 属性说明

+ name - 包名。
+ version - 包的版本号。
+ description - 包的描述。
+ homepage - 包的官网 url 。
+ author - 包的作者姓名。
+ contributors - 包的其他贡献者姓名。
+ dependencies - 依赖包列表。如果依赖包没有安装，npm 会自动将依赖包安装在 node_module 目录下。
+ repository - 包代码存放的地方的类型，可以是 git 或 svn，git 可在 Github 上。
+ main - main 字段指定了程序的主入口文件，require('moduleName') 就会加载这个文件。这个字段的默认值是模块根目录下面的 index.js。
+ keywords - 关键字

#### 卸载模块

我们可以使用以下命令来卸载 Node.js 模块。

```
npm uninstall koa
```

卸载后，你可以到 /node_modules/ 目录下查看包是否还存在，或者使用以下命令查看：

```
npm ls
```

#### 更新模块

```
npm update koa
```

#### 搜索模块

```
npm search express
```

#### 创建模块

创建模块，package.json 文件是必不可少的。我们可以使用 NPM 生成 package.json 文件，生成的文件包含了基本的结果。

```
npm init
快速创建
npm init -y
```

#### 在 npm 资源库中注册用户（使用邮箱注册）：

```
npm adduser

Username: "用户名"
Password: "密码"
Email: (this IS public) "邮箱"
```

#### 发布模块

```
npm publish
```

#### npm发布包教程

https://segmentfault.com/a/1190000017461666

#### 容易混乱的几个安装

<!-- 原文地址：https://www.cnblogs.com/limitcode/p/7906447.html -->

```
npm install moduleName 命令
1. 安装模块到项目node_modules目录下。
2. 不会将模块依赖写入devDependencies或dependencies 节点。
3. 运行 npm install 初始化项目时不会下载模块。

npm install -g moduleName 命令
1. 安装模块到全局，不会在项目node_modules目录中保存模块包。
2. 不会将模块依赖写入devDependencies或dependencies 节点。
3. 运行 npm install 初始化项目时不会下载模块。

npm install -save moduleName 命令
1. 安装模块到项目node_modules目录下。
2. 会将模块依赖写入dependencies 节点。
3. 运行 npm install 初始化项目时，会将模块下载到项目目录下。
4. 运行npm install --production或者注明NODE_ENV变量值为production时，会自动下载模块到node_modules目录中。

npm install -save-dev moduleName 命令
1. 安装模块到项目node_modules目录下。
2. 会将模块依赖写入devDependencies 节点。
3. 运行 npm install 初始化项目时，会将模块下载到项目目录下。
4. 运行npm install --production或者注明NODE_ENV变量值为production时，不会自动下载模块到node_modules目录中。
```

#### 总结

devDependencies 节点下的模块是我们在开发时需要用的，比如项目中使用的 gulp ，压缩css、js的模块。这些模块在我们的项目部署后是不需要的，所以我们可以使用 -save-dev 的形式安装。像 express 这些模块是项目运行必备的，应该安装在 dependencies 节点下，所以我们应该使用 -save 的形式安装。



### npm的镜像源

npm镜像源是npm软件包管理器的服务器地址，用于下载和安装npm包。常见的npm镜像源有以下几种：

- 官方源

  npm官方提供的默认源，地址是https://registry.npmjs.org/，但由于位于国外，速度较慢。

- npm中国镜像站地址

  https://registry.npmmirror.com

- cnpm源

  另一个由淘宝团队提供的镜像源，地址是http://r.cnpmjs.org/，同样是国内服务器，速度较快。

- 阿里源

  由阿里巴巴提供的镜像源，地址是https://npm.aliyun.com/，同样是国内服务器，速度较快。

- 腾讯云 NPM 镜像：

  https://mirrors.cloud.tencent.com/npm/

- 淘宝源（日前已禁用）

  由淘宝团队提供的镜像源，地址是https://registry.npm.taobao.org/，是国内服务器，因此速度较快。

#### npm查看镜像源

在npm中查看配置的镜像源（registry），可以使用以下命令：

```
npm get registry
```

这将输出当前配置的npm包仓库地址。

如果想要查看所有的npm配置，可以使用：

```
npm config list
```

这将列出npm的所有配置信息，包括镜像源。

#### 切换镜像源

使用镜像源可以加快npm包的下载和安装速度，尤其是在国内网络环境下。你可以通过设置npm的配置来切换镜像源。例如，要使用淘宝源，可以执行以下命令：

npm config set registry https://registry.npm.taobao.org/

切换镜像源后，再使用npm安装包时，npm将会从对应的镜像源下载和安装包。

#### 特定包使用特定源

```
yarn add vue-draggable-plus --registry https://registry.npmjs.org
```

#### 缓存问题

如果你之前使用过其他的镜像源，并且现在想要切换到另一个，可能需要先清除 yarn 的缓存。

你可以使用yarn cache clean命令来做到这一点。







### 问题

#### 不同包使用不同源

##### 临时更改

你可以在运行 npm 命令时指定 `--registry` 标志来临时更改 registry。例如：

```bash
npm install vue-draggable-plus --registry https://registry.npmjs.org
```

这条命令会告诉 npm 使用 `https://registry.npmjs.org` 来安装 `vue-draggable-plus`。

##### 永久更改

如果你想永久更改 registry，你可以更新 `.npmrc` 文件。你可以按照以下步骤进行：

1. 找到你的 `.npmrc` 文件。这个文件通常位于你的用户主目录下，或者在项目的根目录中（如果你在项目级别设置了 registry）。

2. 使用文本编辑器打开 `.npmrc` 文件。

3. 修改或添加 `registry` 行来指向 `https://registry.npmjs.org`。例如：

   ```
   registry=https://registry.npmjs.org/
   ```

4. 保存文件并关闭文本编辑器。

5. 现在，当你运行 `npm install` 命令时，npm 将默认使用新的 registry。

##### 项目级别的 `.npmrc`

如果你只想在特定的项目中更改 registry，而不是全局地更改，你可以在该项目的根目录中创建一个 `.npmrc` 文件，并只在该文件中指定 registry。这样，当你在该项目的上下文中运行 npm 命令时，它会使用这个 `.npmrc` 文件中的设置。

##### 注意事项

- 更改 registry 后，确保你的网络可以访问新的 registry，并且该 registry 包含了你要安装的软件包。
- 如果你正在使用一个公司或组织的私有 registry，请确保更改 registry 后不会影响你的其他依赖项的安装。
- 在切换回原来的 registry 之前，请确保你已经记录了原始的 registry 地址，以便日后需要时可以恢复。

通过以上方法，你应该能够灵活地管理 npm 的 registry，从而使用不同的源来安装你的依赖项。

##### 不影响自动化构建

目前项目的.npmrc文件指定了registry=http://npm.boundless-tech.com.cn/
如果我想使用https://registry.npmjs.org这个源来安装vue-draggable-plus
且不影响自动化构建时其他包的安装，我应该怎么处理

如果你希望在不修改全局 `.npmrc` 文件的情况下，仅为 `vue-draggable-plus` 这个包使用 `https://registry.npmjs.org` 这个源，你可以通过在执行安装命令时指定 `--registry` 参数来实现。这样做不会影响自动化构建时其他包的安装，因为其他包仍然会使用 `.npmrc` 文件中指定的源。

具体做法如下：

```bash
npm install vue-draggable-plus --registry=https://registry.npmjs.org
```

这条命令会只针对 `vue-draggable-plus` 这个包使用 `https://registry.npmjs.org` 这个源，而不会影响其他包的安装源。

在自动化构建脚本中，你可以确保只有安装 `vue-draggable-plus` 的命令包含了 `--registry` 参数，其他包的安装命令则保持原样，这样就可以确保只有 `vue-draggable-plus` 会从 `https://registry.npmjs.org` 安装，而其他包仍然从 `.npmrc` 文件中指定的源安装。

例如，如果你的自动化构建脚本中原本有类似这样的命令：

```bash
npm install
```

你可以修改为：

```bash
npm install --ignore-scripts  # 首先安装其他所有依赖，忽略可能的脚本执行  
npm install vue-draggable-plus --registry=https://registry.npmjs.org  # 然后单独安装 vue-draggable-plus
```

注意：`--ignore-scripts` 参数是可选的，用于防止在全局安装依赖时执行任何 npm 脚本，这通常是为了提高构建速度和安全性。如果你的构建过程不需要执行这些脚本，那么可以加上这个参数。如果你的项目依赖于某些安装脚本（如 `postinstall` 脚本），则不应使用此参数。

#### 同时使用两个源地址

删了yarn.lock文件，然后命令行运行下面这两个代码
yarn
yarn add vue-draggable-plus --registry https://registry.npmjs.org 



### npm全局安装与本地安装、开发依赖和生产依赖

**npm(Node Package Manager)是 JavaScript 世界的包管理工具,并且是 Node.js 平台的默认包管理工具。通过 npm 可以安装、共享、分发代码,管理项目依赖关系。**（与其有同样功能的另一个包管理工具yarn，速度用体验比旧版本的npm好，但npm最近的新版本也做出很大努力，与yarn速度和体验差距越来越小，有兴趣可以了解下）。

npm这几年可以说是前端猿日常离不开的工具了，刚开始学习使用node、npm来进行前端项目构建的时候，有很多概念需要理解，**各种命令行、各种新js语法、各种环境依赖**...就问你怕吗？：

![图片描述](https://segmentfault.com/img/bVbmGs5?w=663&h=183)

**讲真，刚开学时我怕。**废话不多扯，现在我们进入主题，聊聊**npm 全局安装与本地安装、开发依赖和生产依赖**，先抛几个常见疑惑：

1. **什么是全局安装、什么是本地安装(或叫局部安装，下文统一叫本地安装) ？**
2. **为什么要全局安装？为什么又要本地安装？全局安装和本地安装有什么区别？**
3. **什么叫开发依赖、生产依赖？什么又是开发环境、生产环境？**



### 全局安装与本地安装

#### 一、全局安装：

```awk
npm install <pageName> -g//（这里-g是-global的简写）
```

通过上面的命令行（带-g修饰符）安装某个包，就叫全局安装。通常全局包安装在node目录下的node_modules文件夹。可以通过执行下面几条命令查看node、npm的安装目录和全局包的安装目录。

```awk
which node   // 查看node的安装目录
which npm   // 查看npm的安装目录
npm root -g // 查看全局包的安装目录
npm list -g --depth 0 //查看全局安装过的包
```

#### 二、本地安装:

```q
npm install <pageName> (后面可以加几种修饰符，主要有两种--save-dev和--save)
```

通过上面的命令行安装某个包，就叫本地安装。包安装在你当前项目文件夹下的node_modules文件夹中。

#### 三、全局安装的作用:

**全局安装的包可提供直接执行的命令**(例：gulp -h可以查看gulp定义了什么命令)。 比如gulp全局安装后，可以在命令行上直接执行gulp -v、gulp -h等（原理：全局安装的gulp会将其package.json中的bin命令注入到了全局环境，使得你可以全局执行：gulp xxx命令，这另一个话题了，不深入）。**倘若只在本地安装了gulp，未在全局安装gulp，直接执行这些命令会报错**。你想要执行相应的命令则可能需要例如：node ./node_modules/gulp/bin/gulp.js -v(查看版本) 这样用一大串命令来执行。**因此全局安装就发挥到他的好处了**，一个gulp -v就搞定

当然，不是每个包都必须要全局安装的，**一般在项目中需要用到该包定义的命令才需要全局安装**。比如gulp <taskName>执行gulp任务...等，所以是否需要全局安装取决于我们如何使用这个包。**全局安装的就像全局变量有点粗糙，但在某些情况下也是必要的，全局包很重要，但如果不需要，最好避免使用。**

#### 四、可以全局安装，那么直接全局安装到处使用就行了，干嘛还需要本地安装？

1. 如果只是全局安装了而没本地安装，就得require('<pagePath>') 例：引入一个全局的包可能就是requirt('/usr/local/....')通过全局包的路径引入，这样显然十分的不灵活。如果安装了本地包，那么就**可以直接require('<pageName>')引入使用**。
2. 一个包通常会在不同的项目上会重复用到，如果只全局安装，那么当某个项目需要该包更新版本时，更新后可能就会影响到其他同样引用该包的项目，**因此本地安装可以更灵活地在不同的项目使用不同版本的包，并避免全局包污染的问题，**

**一个经验法则：要用到该包的命令执行任务的就需要全局安装，要通过require引入使用的就需要本地安装**（ 但实际开发过程中，我们也不怎么需要考虑某个包是全局安装还是本地安装，因为这一点在该包的官网上一般会明确指出，以上是为了理解全局安装和本地安装）



### 开发依赖和生产依赖

顺着上面讲到的本地安装，本地安装有两种主要的安装方式：

1. 保存到开发依赖(devDependencies): npm install <pageName> --save-dev
2. 保存到生产依赖(dependencies): npm install <pageName> --save

"**开发依赖"顾名思义在开发环境中用到的依赖，"生产依赖"在生产环境中用到的依赖**。那么这里又延伸出个问题什么是开发环境、什么是生产环境？

#### 一、开发环境和生产环境

【开发环境】：指的是你的项目尚且在编码阶段时的环境。你在代码可能还有各种console.log()、注释、格式化等。
【生产环境】：指的是你的项目已经完成编码，并发布上线可供用户浏览的阶段时的环境。代码可能经过了压缩、优化等处理。

**这些概念其实并没有一个很明确的定义，接下来我们举例个场景，将"开发环境"、"生产环境"和上面的"开发依赖"、"生产依赖"联系起来就会比较容易理解的了**。假如我们在开发过程中使用jQuery。在以往，可能就是把jQuery这个插件下载的本地，再通<script>引入html中。但这有个不方便的地方，我们每次进行一个项目的时候就得手动复制这个jQuery文件到我们的项目中，如果想要换个版本又得官网上下载、随着项目越来越多。用到的插件、库也随之越繁杂...这样会造成自家用的插件管理繁琐的问题。因此就出现了npm(包管理工具)你需要用到什么，直接通过一条命令行就可以将想要的插件下载下来，并直接引入到项目中，目前几乎所有的js插件都能在npm上直接下载。

#### 二、生产依赖

回到环境和依赖话题，**我们下载的jQuery，在开发时参与源码编写，在发布上线的生产环境中也是需要它的。不仅在开发环境编写代码时要依赖它、线上环境也要依赖它，因此将它归类为"生产依赖"**，安装时执行npm install jquery --save，它就会被记录在package.json的dependencies。当进行代码打包时，会将这里的jQuery打包入我们的项目代码中。

#### 三、开发依赖

接着，假如我们用gulp对html进行压缩，我们通常会用到一个插件gulp-htmlmin。**我们只希望它把html压缩完就ok了，并不希望它融入我们的项目代码中，即只存在于开发环境，因此把他归类为"开发依赖"**。安装时执行npm install gulp-htmlmin --save-dev它就会被记录在package.json的devependencies下，当进行代码打包时，不会将这里的gulp-htmlmin插件源码打包入我们的项目代码中

**devDependencies只会在开发环境下使用，生产环境不会被打入包内；而dependencies不仅在开发环境中要使用，生产环境也需要使用到**。根据以上规则，我们就很容易区分哪些插件是用--save-dev模式安装，哪些用--save模式安装。



### NPM语义版本号

在 [npm 的官方文档](https://docs.npmjs.com/about-semantic-versioning)中建议库的版本号的发布规则如下 ：


| 场景               | 阶段       | 规则                                    | 例子  |
| ------------------ | ---------- | --------------------------------------- | ----- |
| 首次发布           | 新产品     | 从 1.0.0 开始                           | 1.0.0 |
| 向后兼容的bug修复  | 发布补丁   | 第三位数字值递增                        | 1.0.1 |
| 向后兼容的新特性   | 小版本更新 | 第二位数字递增且将第三位数字重置为0     | 1.1.0 |
| 破坏向后兼容的修改 | 大版本更新 | 第一位数字递增且将第二、三为数字重置为0 | 2.0.0 |

#### 你想使用什么版本？

回看文章开头我使用 create-react-app 新建的项目里 package.json 里的

```text
"react-scripts": "4.0.1"
```

这边非常明确地指定了使用 react-scripts 的 4.0.1 版本。

所有依赖库都使用这样明确的版本声明不好吗？—— 是的，这可能不是最佳的做法。

设想，你的项目里依赖的某个库有个性能问题，作者最近发布了修复补丁，如果你不是经常关注该库的 changelog，你可能根本不知道，你的项目也享受不到这个性能提升了。

再设想，你的项目里依赖的某个库最近被作者更新了，提供了几个十分有用的小功能，同样的，使用精确的版本号不能让你及时体验到这些新特性。

那么有办法设置一个模糊的版本号范围吗？ —— 有的！下面使用例子来更好地说明

1） 及时帮我安装最新补丁

例子1：

```text
"some-lib": "1.0"   
或   
"some-lib": "1.0.x"
```

说明1： npm install 的时候，请帮我安装 1.0 的小版本以及最新的补丁版本，如 1.0.2 , 1.0.6 等

例子2:

```text
"some-lib"： ”~1.0.4“
```

说明2: npm install 的时候，请帮我安装 1.0 的小版本 以及 **1.0.4 以上**的最新补丁版本， 如 1.0.6 等（但不会安装 1.0.2 因为它低于 1.0.4 ）

2）及时帮我安装最新小版本和最新补丁

例子3:

```text
"some-lib": "1"   
或   
"some-lib": "1.x"
```

说明3: npm install 的时候，请帮我安装 1 的大版本以及最新的小版本以及补丁版本，如 1.0.6 , 1.1.6 , 1.2.3 , 1.3.0 等

例子4:

```text
"some-lib": "^1.1.4"
```

说明4: npm install 的时候，请帮我安装 1 的大版本以及 **1.1.4 以上** 最新的小版本以及补丁版本，如 1.1.6 , 1.2.3 , 1.3.0 等 （但不会安装 1.0.6 因为它低于 1.1.4 ）

3) 及时帮我安装最新的版本

例子5:

```text
"some-lib": "*"   
或   
"some-lib": "x"
```

说明5: npm install 的时候, **都给我安装最最最新的版本！我不在乎兼容性！项目上线崩盘了我也无所谓！** —— 这是最浮夸的一种写法，当然也是基本不可能出现在实际生产环境代码中的写法。

（以上都是以项目中没有 package-lock.json 为前提假设，后面的章节会谈到 package-lock.json）

官方提供了一个实验平台网站可以尝试以上这些写法 [npm semantic version calculator](https://semver.npmjs.com/)



### package-lock.json

#### 作用

其实用一句话来概括很简单，就是锁定安装时的包的版本号，并且需要上传到git，以保证其他人在npm install时大家的依赖能保证一致。

引用知乎@周载南的回答

> 根据官方文档，这个package-lock.json 是在 `npm install`时候生成一份文件，用以记录当前状态下实际安装的各个npm package的具体来源和版本号。
>
> 它有什么用呢？因为npm是一个用于管理package之间依赖关系的管理器，它允许开发者在pacakge.json中间标出自己项目对npm各库包的依赖。你可以选择以如下方式来标明自己所需要库包的版本
>
> 这里举个例子：
>
> "dependencies": \\{
> "@types/node": "**^**8.0.33",
> \\},
>
> 这里面的 向上标号**^**是定义了**向后（新）兼容依赖**，指如果 types/node的版本是超过8.0.33，并在大版本号（8）上相同，就允许下载最新版本的 types/node库包，例如实际上可能运行npm install时候下载的具体版本是8.0.35。波浪号
>
> 大多数情况这种向新兼容依赖下载最新库包的时候都没有问题，可是因为npm是开源世界，各库包的版本语义可能并不相同，有的库包开发者并不遵守严格这一原则：相同大版本号的同一个库包，其接口符合兼容要求。这时候用户就很头疼了：在完全相同的一个nodejs的代码库，在不同时间或者不同npm下载源之下，下到的各依赖库包版本可能有所不同，因此其依赖库包行为特征也不同有时候甚至完全不兼容。
>
> 因此npm最新的版本就开始提供自动生成package-lock.json功能，为的是让开发者知道只要你保存了源文件，到一个新的机器上、或者新的下载源，只要按照这个package-lock.json所标示的具体版本下载依赖库包，就能确保所有库包与你上次安装的完全一样。

原来package.json文件只能锁定大版本，也就是版本号的第一位，并不能锁定后面的小版本，你每次npm install都是拉取的该大版本下的最新的版本，为了稳定性考虑我们几乎是不敢随意升级依赖包的，这将导致多出来很多工作量，测试/适配等，所以package-lock.json文件出来了，当你每次安装一个依赖的时候就锁定在你安装的这个版本。

那如果我们安装时的包有bug，后面需要更新怎么办？

在以前可能就是直接改package.json里面的版本，然后再npm install了，但是5版本后就不支持这样做了，因为版本已经锁定在package-lock.json里了，所以我们只能npm install xxx@x.x.x  这样去更新我们的依赖，然后package-lock.json也能随之更新。

假如我已经安装了jquery 2.1.4这个版本，从git更新了package.json和package-lock.json，我npm install能覆盖掉node_modules里面的依赖吗?

其实我也有这个疑问，所以做了测试，在直接更新package.json和package-loc.json这两个文件后，npm install是可以直接覆盖掉原先的版本的，所以在协作开发时，这两个文件如果有更新，你的开发环境应该npm install一下才对。

### package-lock.json 放进版本控制系统（以Git为例）的目的和好处

package.json 里声明的版本支持以上的模糊写法，那么在 npm install 的时候，我怎么知道到底安装了具体哪个版本呢？

答案就在 package-lock.json 里

package-lock.json 还有一个很重要的作用 —— 当 npm install 时发现本地有 package-lock.json，就会严格按照 package-lock.json 的版本来安装。

- package-lock.json 完整描述了当前项目的依赖树，保证了其他地方运行npm install 时都能安装一模一样的依赖库版本
- 无需把 node_modules 上传到Git就能达到上面第一点提到的效果
- 如果package-lock.json更新并上传新版本到 Git，利用 Git 的 Diff 功能可以清楚地了解发生了哪些变化
- 可以让 Npm install 时跳过对一些依赖库的元数据的请求，优化了性能
- 从 npm v7 版本开始，package-lock.json 的信息已经包含了 package.json 关于依赖树的的所有内容，因此无需再解析 package.json，大大提高了性能



### 发布一个UI组件库

1.在本地创建项目目录

2.在 GitHub 上创建仓库，并在本地关联远程仓库，用于保存项目。

3.添加开源许可证 - 如何选择开源许可证？


在 GitHub 对应的仓库根目录下新增文件，输入 LICENSE ，出现增加许可证的选项，点击后选择对应许可证即可：

4.本地项目目录下运行 npm init - 创建 package.json

5.本地项目目录下运行 npm i vue - 添加 vue

6.写自己的组件。。。。略

7.设置入口文件

在 package.json 中添加入口文件 "main": "index.js",，在入口文件中引入并导出需要打包发布的组件：

```
import Button from './src/Button.vue'
import ButtonGroup from './src/buttonGroup.vue'
import Icon from './src/Icon.vue'

export \\{Button,ButtonGroup,Icon\\}
```

8.发布到npm

在 npmjs注册一个账号并在邮箱中确认注册信息
在项目根目录的命令行中输入 npm adduser，根据提示填入账号密码邮箱
使用命令 npm publish 发布
注意：如果错误提示里面含有 https://registry.npm.taobao.org 则说明你的 npm 源目前为淘宝源，需要更换为 npm 官方源

可以直接安装 nrm 对 npm源 进行管理: npm install -g nrm

输入 nrm ls 可以看到目前的 npm 源；输入 nrm use npm 切换到 npm 源。

参考

[参考element-ui源码](https://github.com/ElemeFE/element/blob/dev/packages/alert/index.js)



1， 首先是安装命令

```
 //全局安装
 npm install 模块名 -g
 //本地安装
 npm install 模块名
 //一次性安装多个
 npm install 模块1 模块2 模块3 
 //安装开发时依赖包
 npm install 模块名 --save-dev
 //安装运行时依赖包
 npm install 模块名 --save
```

2， 查看安装的目录

```
 //查看项目中模块所在的目录
 npm root
 //查看全局安装的模块所在目录
 npm root -g
```

3， 查看npm的所有命令命令

```
 npm help
```

4，查看某个包的各种属性

```
//查看某个包对于各种包的依赖关系
 npm view 模块名 dependencies
```

5，查看包的源文件地址

```
 //查看包的源文件地址
 npm view 模块名 repository.url
```

6

- 查看当前模块依赖的node最低版本号

```
 npm view 模块名 engines
```

- 查看模块的当前版本号

```
 npm view 模块名 version
 //需要注意的是查看到的模块版本是该模块再远程仓库的版本号，并不是当前项目中所依赖的版本号。
 //查看当前项目中应用的某个模块的版本号的命令为
 npm list 模块名 version
```

- 查看模块的历史版本和当前版本

```
 npm view 模块名 versions
```

- 查看一个模块的所有信息

```
 npm view 模块名
```

7，查看npm使用的所有文件夹

```
 npm help folders
```

8，用于更改包内容后进行重建

```
 npm rebuild 模块名
```

9，检查包是否已经过时

```
 //此命令会列出所有已经过时的包，可以及时进行包的更新
 npm outdated
```

10，更新node模块

```
 npm update 模块名
 //当然你也可以update 该模块到指定版本
 npm update 模块名 @版本号
 //如果安装到最新版本可以使用以下命令
 npm install 模块名@latest 
 
 //如果当前的版本号为2.5.1，是没办法进行npm update 模块名 @2.3.1 将模块版本号变为2.3.1的，当然，你可以先uninstall，然后进行install @2.3.1
```

11，卸载node模块

```
 npm uninstall 模块名
```

12，访问package.json的字段文档

```
 npm help json
```

13，发布一个npm包的时候，需要检验某个包名是否已经存在

```
 npm search 模块名
```

14，npm init：引导你创建一个package.json文件，包括名称、版本、作者这些信息

- 清除npm的缓存

```
 npm cache clean
 //慎重使用改命令
```

15, npm root 查看当前包的安装路径，
npm root -g 查看全局的包的安装路径

16，npm -v 查看npm的版本

17，查看某个模块的bugs列表界面

```
 npm bugs 模块名
 //例如运行npm bugs chai则会打开vue仓库的issue，效果如下图
```

![npm bugs](http://blogpic.blackgan.cn/npmBugs2.PNG)

18，打开某个模块的仓库界面

```
 npm repo 模块名
 //例如运行npm repo vue则会打开vue线上仓库，效果如下图
```

![npm bugs](http://blogpic.blackgan.cn/npmRepo.PNG)

- 打开某个模块的文档

```
 npm docs 模块名
 //例如运行npm docs vue则会打开vue的readme.md文档
```

- 打开某个模块的主页

```
 npm home 模块名
 //例如运行npm home vue则会打开vue模块的主页
```

- 查看当前已经安装的模块

```
 npm list
 //当然我们也可以限制输入的模块层级，例如
 npm list --depth=0
```

![npm list](http://blogpic.blackgan.cn/npmList.PNG)

- 清除未被使用到的模块

```
 //有时在我们使用npm list的时候，可能会碰到一些问题，就是有些模块并没有被项目引用使用，我们还是安装了这些模块，那么我们可以一键清除这些没有使用到的模块
 npm prune
```

#### 版本控制

我们使用node开发时，经常需要依赖一些模块，我们进行了下载之后，便一直在该版本的模块环境下进行开发，但是线上的服务器一般都是根据依赖来配置文件，重新下载各个模块，但是保不齐某个模块的版本已经更新了，这时线上的包会更新到最新的版本，但你的代码还是依据老版本来写的，这时可能会产生一些不知名的Bug,

首先看npm包的版本号的格式X.Y.Z,版本好的格式遵循semver 2.0规范，其中X为主版本号，只有更新了不向下兼容的API时进行修改主版本号，Y为次版本号，当模块增加了向下兼容的功能时进行修改，Z为修订版本号，当模块进行了向下兼容的bug修改后进行修改,这就是“语义化的版本控制”。

> > 默认情况下，当用--save或者--save-dev安装一个模块时，npm通过脱字符(^)来限定所安装模块的主版本号，而该脱字符对于不同的版本号有不同的更新机制
> >
> > - ^1.2.1 代表的更新版本范围为 >=1.2.1 && < 2.0.0
> > - ^0.2.1 代表的更新版本范围为 >=0.2.1 && < 0.3.0
> > - ^0.0.2 代表的更新版本范围为 0.0.2（相当于锁定为了0.0.2版本）

## ##### 对于上述字符的版本控制，我们可以来进行一个尝试:

首先可以看到package.json中对于vuex的版本依赖为^2.3.1

![version1](http://blogpic.blackgan.cn/version1.PNG)

然后查看以下项目中安装的vuex模块的版本号

![version2](http://blogpic.blackgan.cn/version2.PNG)

果然没错，改版本号为2.3.1，接下来我们看一下vuex的历史版本（npm view vuex versions）

![version3](http://blogpic.blackgan.cn/version3.PNG)

可以看到2.3.1-2.5.0之后到了3.0.0，接下来运行npm update vuex,查看以下更新后的版本

![version3](http://blogpic.blackgan.cn/version4.PNG)

现在我们看到更新后的vuex版本号为2.5.0 < 3.0.0,可以验证第一条规范。

我们再来验证下主版本号为0的版本控制情况，先将当前项目依赖的vuex版本改为@0.6.1版本.

```
npm uninstall vuex
//卸载vuex成功
npm install vuex@0.6.1 --save
//安装vuex0.6.1版本成功
```

![version5](http://blogpic.blackgan.cn/version5.PNG)

然后更新当前项目中的vuex版本，执行代码 npm update vuex

![version5](http://blogpic.blackgan.cn/version6.PNG)

可以通过npm view vuex versions看到vuex的版本历程，在0.6.3之上为0.7.0，所以当使用脱字符(^)来控制版本号时，当主版本号为0，即代表该模块在快速构建中时，更新项目时的版本范围只能更新修订版本号Z。

对于第三种情况，当主版本和此版本都为0时，代表着该模块处于一个极其不稳定的状态，在执行update时并不会进行版本更新。

------

> > 波浪号(~)是限定模块的次要版本，（以下规则测试方法同上，便不一 一测试）
> >
> > - ~1.5.1允许安装版本号大于1.5.1但小于1.6.0版本的模块
> > - ~0.5.1允许安装版本号为0.6.0

------

> > 当主版本号/次版本号/修订版本号为X or x or *时，那么update或install是会下载该分支最新的版本号
> >
> > - (*)跟新或安装模块时会安装>=0.0.0的最新版本
> > - 1.x 表示的更新范围为>=1.0.0&&< 2.0.0
> > - 1.2.x 表示的更新范围为>=1.2.0&&< 1.3.0

[更多版本规范](https://github.com/npm/npm/blob/latest/doc/misc/semver.md)

1，当然我们也可以把项目依赖的包固定在某一个版本，强制大家安装相同的依赖树，如下所示：

```
 npm install react --save -E
 //此命令会将react的版本号进行固定，但是该方式只能控制项目中直接依赖的包的版本，无法控制项目模块中依赖的包的版本号，所以这种方式也无法让不同的使用者得到相同的依赖树。
```

2，此外我们还可以使用npm shrinkwrap,可以将项目中的模块版本进行精确锁定：

这时候只需要运行命令 npm shrinkwrap,便会产生一个npm-shrinkwrap.json文件，这个文件保存了所有当前使用的依赖模块的版本：把该文件提交到git仓库中，这样其他人在clone你的项目的时候，执行npm install命令时，npm检测到该文件中的信息会完整的还原出完全相同的依赖树，具体的使用方法如下：

```
npm install --save-dev react //安装react
npm prune    //清除未被使用的模块
npm shrinkwrap
```

> 但是使用这种方法，安装一个模块包的方式比较繁琐。

3，使用yarn我们也可以得到模块包精确控制的结果

yarn是一个与npm兼容的node包管理器，使用它安装npm包，会自动在项目目录创建一个yarn.lock文件，该文件包含了当前项目中所安装的依赖包的版本信息，其他人在使用yarn安装项目的依赖包时就可以通过该文件创建一个完全相同的依赖环境。

使用方法如下：

```
 yarn init  //使用yarn创建一个项目
 yarn add 模块名  //使用yarn 安装一个包
 //还有很多yarn命令
```

> 此外，yarn除了可以自动帮我们锁定依赖包的版本，yarn还在本地缓存已经安装过的包，当再次安装时，直接从本地读取即可。安装速度得到大大提升。但yarn的使用需要整个团队都去使用，还是有一定的成本的。

综上所述，目前大多数项目中较为简单的使用规范，在项目中依赖各个模块时，对于主版本号和次版本号都为0的不稳定的项目，我们可以使用精确版本（exact）,对于主版本号为0次版本号不为0的模块和主版本号不为0的模块，使用caret Range即脱字符(^)来控制版本。当然，我们也可以对项目依赖模块的版本进行精确锁定。

#### SemVer(Semantic Versioning) 2.0.0

SemVer是一个对npm包版本进行规范的模块，它对于npm包的版本号有着一系列的规则，以下为摘抄自SemVer 2.0.0中的规则：

1. 在版本控制环节我们已经说过了，模块的版本号采用X.Y.Z的格式，且都必须为非负的正整数，依次为主版本号、次版本号，修改版本号。
2. 当规定版本的模块进行发布之后，对于该模块的任何修改，都必须发布新版本。
3. 主版本号为0.X.Y的模块处于开发阶段，模块并不稳定。
4. 主版本号在有不向下兼容的API发布时必须修改，在主版本号递增时，次版本号和修订版本号必须重新归零。
5. 次版本号再有向下兼容的API发布时进行递增修改，在模块中有API被弃用时也必须递增次版本号，当此版本号递增改变时，修订版本号Z必须归零。
6. 版本的优先级就是各个版本的排序规则，判断版本优先级时，必须把版本号从左至右分为主版本号、此版本号、修订版本号、以及先行版本号来进行比较

