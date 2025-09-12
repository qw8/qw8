---
title: yarn
date: 2020-08-27 19:21:17
categories: 
- 前端知识
tags:
- yarn
---

### 什么是 yarn

Yarn 是 facebook 发布的一款取代 npm 的包管理工具。



### yarn 的特点

速度超快。
Yarn 缓存了每个下载过的包, 所以再次使用时无需重复下载。 同时利用并行下载以最大化资源利用率, 因此安装速度更快。

超级安全。
在执行代码之前, Yarn 会通过算法校验每个安装包的完整性。

超级可靠。
使用详细、简洁的锁文件格式和明确的安装算法, Yarn 能够保证在不同系统上无差异的工作。



### Yarn的优点

- 速度快 。速度快主要来自以下两个方面：

1. 并行安装：无论 npm 还是 Yarn 在执行包的安装时，都会执行一系列任务。npm 是按照队列执行每个 package，也就是说必须要等到当前 package 安装完成之后，才能继续后面的安装。而 Yarn 是同步执行所有任务，提高了性能。
2. 离线模式：如果之前已经安装过一个软件包，用Yarn再次安装时之间从缓存中获取，就不用像npm那样再从网络下载了。

- 安装版本统一：为了防止拉取到不同的版本，Yarn 有一个锁定文件 (lock file) 记录了被确切安装上的模块的版本号。每次只要新增了一个模块，Yarn 就会创建（或更新）yarn.lock 这个文件。这么做就保证了，每一次拉取同一个项目依赖时，使用的都是一样的模块版本。npm 其实也有办法实现处处使用相同版本的 packages，但需要开发者执行 npm shrinkwrap 命令。这个命令将会生成一个锁定文件，在执行 npm install 的时候，该锁定文件会先被读取，和 Yarn 读取 yarn.lock 文件一个道理。npm 和 Yarn 两者的不同之处在于，Yarn 默认会生成这样的锁定文件，而 npm 要通过 shrinkwrap 命令生成 npm-shrinkwrap.json 文件，只有当这个文件存在的时候，packages 版本信息才会被记录和更新。
- 更简洁的输出：npm 的输出信息比较冗长。在执行 npm install <package> 的时候，命令行里会不断地打印出所有被安装上的依赖。相比之下，Yarn 简洁太多：默认情况下，结合了 emoji直观且直接地打印出必要的信息，也提供了一些命令供开发者查询额外的安装信息。
- 多注册来源处理：所有的依赖包，不管他被不同的库间接关联引用多少次，安装这个包时，只会从一个注册来源去装，要么是 npm 要么是 bower, 防止出现混乱不一致。
- 更好的语义化： yarn改变了一些npm命令的名称，比如 yarn add/remove，感觉上比 npm 原本的 install/uninstall 要更清晰。



### 为什么会出现 yarn

npm 存在一些历史遗留问题, npm 很多依赖不会指定版本号, 默认会安装最新的版本, 这样就会出现问题: 当新版本无法兼容之前的项目, 原项目可能会出现 bug。

yarn 为了解决这个问题推出了 yarn.lock 的机制, 把依赖模块的版本号全部锁定, 当你执行 yarn install 的时候, yarn 会读取这个文件获得依赖的版本号, 然后依照这个版本号去安装对应的依赖模块, 这样依赖就会被锁定, 以后再也不用担心版本号的问题了。其他人或者其他环境下使用的时候, 把这个 yarn.lock 拷贝到相应的环境项目下再安装即可。
注意: 这个文件不要手动修改它, 当你使用一些操作如 yarn add 时, yarn 会自动更新 yarn.lock。



### yarn 的安装

下载 node.js, 使用 npm 安装

```
npm install -g yarn
```

查看版本: yarn --version

Yarn 淘宝源安装, 分别复制粘贴以下代码行到黑窗口运行即可

```
yarn config set registry https://registry.npm.taobao.org -g
yarn config set sass_binary_site http://cdn.npm.taobao.org/dist/node-sass -g
```



### yarn 的常用命令

#### 1.5.1. 初始化项目

```
yarn init // 同 npm init, 执行输入信息后, 会生成 package.json 文件
```

#### 1.5.2. yarn 的配置项

```
yarn config list // 显示所有配置项
yarn config get <key> // 显示某配置项
yarn config delete <key> // 删除某配置项
yarn config set <key> <value> [-g|--global] // 设置配置项
```

#### 1.5.3. 安装包

```
yarn // 等同于运行yarn install
yarn install // 安装 package.json 里所有包, 并将包及它的所有依赖项保存进 yarn.lock
yarn install --flat // 安装一个包的单一版本
yarn install --force // 强制重新下载所有包
yarn install --production // 只安装 dependencies 里的包
yarn install --no-lockfile // 不读取或生成 yarn.lock
yarn install --pure-lockfile // 不生成 yarn.lock
```

##### yarn install具体作用

1. **安装依赖**
   如果项目根目录下有 `package.json` 文件，Yarn 会解析该文件中的 `dependencies`、`devDependencies` 等字段，并根据 `yarn.lock`（或 `package-lock.json`，但优先使用 `yarn.lock`）的精确版本信息，安装所有缺失的依赖项到 `node_modules` 目录。
2. **检查依赖完整性**
   Yarn 会验证 `node_modules` 中的依赖是否与 `yarn.lock` 中的记录一致。如果不一致（例如手动修改了 `node_modules` 或 `package.json`），Yarn 会自动修复或更新依赖。
3. **生成/更新 `yarn.lock`**
   如果 `yarn.lock` 不存在，Yarn 会根据 `package.json` 生成它；如果 `package.json` 的依赖版本范围允许更新（例如 `^1.0.0`），Yarn 可能会更新 `yarn.lock` 中的版本（具体行为取决于配置）。

#### 1.5.4. 添加包 (会更新 package.json 和 yarn.lock)

```
yarn add [package] // 在当前的项目中添加一个依赖包, 会自动更新到 package.json 和 yarn.lock 文件中
yarn add [package]@[version] // 安装指定版本, 这里指的是主要版本, 如果需要精确到小版本, 使用 - E 参数
yarn add [package]@[tag] // 安装某个 tag(比如 beta,next 或者 latest)
```

默认安装包的主要版本里的最新版本, 下面两个命令可以指定版本:

```
yarn add --exact/-E // 安装包的精确版本。例如 yarn add foo@1.2.3 会接受 1.9.1 版, 但是 yarn add foo@1.2.3 --exact 只会接受 1.2.3 版
yarn add --tilde/-T // 安装包的次要版本里的最新版。例如 yarn add foo@1.2.3 --tilde 会接受 1.2.9, 但不接受 1.3.0
```

#### 1.5.5. 发布包

```
yarn publish
```

#### 1.5.6. 移除一个包

yarn remove <packageName>: 移除一个包, 会自动更新 package.json 和 yarn.lock

#### 1.5.7. 更新一个依赖

yarn upgrade用于更新包到基于规范范围的最新版本

更新到特定版本，可以指定版本号 

```
yarn upgrade vue@2.7.16
```

#### 1.5.8. 运行脚本

yarn run 用来执行在 package.json 中 scripts 属性下定义的脚本

#### 1.5.9. 显示某个包的信息

yarn info <packageName> 可以用来查看某个模块的最新版本信息

#### 1.5.10. 缓存

yarn cache
yarn cache list # 列出已缓存的每个包

yarn cache dir # 返回 全局缓存位置

yarn cache clean # 清除缓存



### yarn cache clean

是 Yarn 包管理器的一个命令，用于清理本地的缓存。Yarn 会将下载的包存储在一个全局缓存目录中，以便在未来的安装过程中可以重用这些包，从而加速安装过程。然而，在某些情况下，你可能想要清除这个缓存，比如：

1. 解决依赖问题：如果你遇到了由于缓存中的包损坏或不兼容导致的问题，清理缓存可以帮助你从远程源重新下载最新的包。
2. 释放磁盘空间：随着时间的推移，缓存可能会变得非常大，占用大量的磁盘空间。使用 `yarn cache clean` 可以帮助你回收这部分空间。
3. 更新依赖：当你想确保所有的依赖都是最新的版本时，清理缓存并重新安装可以达到这个目的。

执行 `yarn cache clean` 命令后，下一次运行 `yarn install` 或其他需要获取依赖的操作时，Yarn 将会从注册表（如 npm registry）重新下载所有需要的包。

请注意，清理缓存不会影响已经安装到项目 `node_modules` 目录下的包。它仅仅清除了 Yarn 的全局缓存，这意味着下次你需要某个包的时候，Yarn 必须再次从网络上下载它。



### 使用 yrm 工具管理一些 npm 源

1.7.1. 安装

```
yarn global add yrm
```

1.7.2. 查看可用源

```
yrm ls
```

1.7.3. 选择源

```
yrm use yarn
```



### 快速删除 node_modules

手动删除真的很慢:

```
安装: npm install rimraf -g
使用: rimraf node_modules
```

rimraf 是 node 的一个包, 可以快速删除 node_modules, 再也不用等半天了。



### Yarn docs

Yarn 1 (Classic): https://classic.yarnpkg.com/en/docs/cli/run
Yarn 2+: https://yarnpkg.com/getting-started/migration



### yarn与npm区别

Yarn和npm都是JavaScript的包管理工具，用于在项目中安装、更新、删除和管理依赖关系。

以下是Yarn和npm之间的一些区别：

1. 性能：Yarn在性能方面通常比npm更快。Yarn使用并行和缓存机制来加快包的下载和安装速度。
2. 离线模式：Yarn可以离线运行，因为它会缓存所有已安装过的包。这使得在没有网络连接或网络不稳定的情况下，能够继续安装依赖项。
3. 安全性：Yarn通过使用哈希算法验证每个下载的包的完整性，以提供更高的安全性。
4. 依赖关系解析：Yarn使用锁定文件 (yarn.lock) 来确保在不同设备上的开发者之间共享相同的依赖版本。这可以防止由于环境差异而引起的构建问题。
5. 脚本执行：npm允许在项目中运行自定义脚本（例如npm run build），而Yarn则需要使用yarn run命令来运行类似的脚本。

不论选择使用Yarn还是npm，都要根据项目的需求和团队的偏好来决定。

#### Yarn的优点？

- 速度快 。速度快主要来自以下两个方面：

1. 并行安装：无论 npm 还是 Yarn 在执行包的安装时，都会执行一系列任务。npm 是按照队列执行每个 package，也就是说必须要等到当前 package 安装完成之后，才能继续后面的安装。而 Yarn 是同步执行所有任务，提高了性能。
2. 离线模式：如果之前已经安装过一个软件包，用Yarn再次安装时之间从缓存中获取，就不用像npm那样再从网络下载了。

- 安装版本统一：为了防止拉取到不同的版本，Yarn 有一个锁定文件 (lock file) 记录了被确切安装上的模块的版本号。每次只要新增了一个模块，Yarn 就会创建（或更新）yarn.lock 这个文件。这么做就保证了，每一次拉取同一个项目依赖时，使用的都是一样的模块版本。npm 其实也有办法实现处处使用相同版本的 packages，但需要开发者执行 npm shrinkwrap 命令。这个命令将会生成一个锁定文件，在执行 npm install 的时候，该锁定文件会先被读取，和 Yarn 读取 yarn.lock 文件一个道理。npm 和 Yarn 两者的不同之处在于，Yarn 默认会生成这样的锁定文件，而 npm 要通过 shrinkwrap 命令生成 npm-shrinkwrap.json 文件，只有当这个文件存在的时候，packages 版本信息才会被记录和更新。
- 更简洁的输出：npm 的输出信息比较冗长。在执行 npm install <package> 的时候，命令行里会不断地打印出所有被安装上的依赖。相比之下，Yarn 简洁太多：默认情况下，结合了 emoji直观且直接地打印出必要的信息，也提供了一些命令供开发者查询额外的安装信息。
- 多注册来源处理：所有的依赖包，不管他被不同的库间接关联引用多少次，安装这个包时，只会从一个注册来源去装，要么是 npm 要么是 bower, 防止出现混乱不一致。
- 更好的语义化： yarn改变了一些npm命令的名称，比如 yarn add/remove，感觉上比 npm 原本的 install/uninstall 要更清晰。

#### npm 与 yarn 命令比较


| NPM                           | YARN                      | 说明                                         |
| ----------------------------- | ------------------------- | -------------------------------------------- |
| npm init                      | yarn init                 | 初始化某个项目                               |
| npm install/link              | yarn install/link         | 默认的安装依赖操作                           |
| npm install taco --save       | yarn add taco             | 安装某个依赖, 并且默认保存到 package         |
| npm uninstall taco --save     | yarn remove taco          | 移除某个依赖项目                             |
| npm install taco --save --dev | yarn add taco --dev       | 安装某个开发时依赖项目                       |
| npm update taco --save        | yarn upgrade taco         | 更新某个依赖项目                             |
| npm update --save             | yarn upgrade              |                                              |
| npm install taco --global     | yarn global add taco      | 安装某个全局依赖项目                         |
| npm publish/login/logout      | yarn publish/login/logout | 发布 / 登录 / 登出, 一系列 NPM Registry 操作 |
| npm run/test                  | yarn run/test             | 运行某个命令                                 |



```
1、查看版本
yarn --version
npm -version(或者 node -v)

2、安装淘宝镜像
yarn config set registry 'https://registry.npm.taobao.org'
npm install -g cnpm --registry=http://registry.npm.taobao.org

3、初始化某个项目
yarn init                                   
npm init

4、默认安装项目依赖
yarn install
cnpm install

5、安装某个依赖，并且默认保存到package
yarn add xxx
cnpm install xxx --save

6、卸载某个项目依赖
yarn remove xxx
cnpm uninstall xxx --save

7、更新某个项目依赖
yarn upgrade xxx
cnpm update xxx --save

8、安装某个全局的项目依赖
yarn global add xxx
cnpm install xxx -g

9、安装某个特定版本号的项目依赖
yarn add xxx@
cnpm install xxx@1.2.33 --save

10、发布/登录/登出，一系列NPM Registry操作
yarn publish/login/logout
npm publish/login/logout

11、运行某个命令
yarn run/test
npm run/test
```



### yarn使用报错系统上禁止运行脚本

#### yarn使用报错信息

yarn : 无法加载文件 C:\Users\Administrator\AppData\Roaming\npm\ya
rn.ps1，因为在此系统上禁止运行脚本。有关详细信息

#### 解决方法

要解决这个问题，可以通过以下步骤打开 PowerShell 的管理权限窗口，修改 PowerShell 执行策略即可：

1.以管理员身份运行 PowerShell 终端。方法是：在开始菜单中找到“Windows PowerShell”，右键点击它并选择“以管理员身份运行”。

2.运行以下命令：Get-ExecutionPolicy -List

3.查看目前 PowerShell 的执行策略。输出结果应该类似于下面这样：

```
 Scope    ExecutionPolicy
 -----    ---------------
```

MachinePolicy Undefined
UserPolicy Undefined
Process RemoteSigned
CurrentUser Restricted
LocalMachine Undefined
4.把当前用户的执行策略改为 RemoteSigned 或者更为宽松的 Unrestricted，方法是运行以下命令：

```
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser 或者 Set-ExecutionPolicy Unrestricted -Scope CurrentUser
```

5.输入 Y 并按回车确认更改。然后再次输入以下命令验证更改是否生效：

```
Get-ExecutionPolicy -List
```

6.输出应该会显示类似如下所示的结果：

```
 Scope    ExecutionPolicy
 -----    ---------------
```

MachinePolicy Undefined
UserPolicy Undefined
Process Undefined
CurrentUser RemoteSigned
LocalMachine Undefined

#### 再次尝试

现在再尝试使用 yarn 进行安装，应该就能正常执行了。完成之后，如果担心安全问题可以把 PowerShell 的执行策略修改回 Restricted 阻止运行脚本。



### 怎么更新yarn.lock文件

要更新`yarn.lock`文件，你可以遵循以下步骤：

1. **安装或更新依赖包**：
   - 添加新依赖：使用命令`yarn add [package_name]`来添加一个新的依赖包到项目中。这将自动更新`yarn.lock`文件以包含新包及其依赖的精确版本。
   - 更新依赖包：要更新一个已存在的依赖到最新版本，可以使用`yarn upgrade [package_name]`。如果想更新到特定版本，可以指定版本号，如`yarn upgrade [package_name]@[version]`。此操作同样会更新`yarn.lock`文件。
   - 删除依赖：使用`yarn remove [package_name]`来移除不再需要的依赖，这也会相应地更新`yarn.lock`文件。

2. **整体更新所有依赖**：
   - 要将所有依赖更新到它们各自的最新版本（符合`package.json`中的版本范围），可以运行`yarn upgrade`或`yarn upgrade-interactive`。后者提供了一个交互式的界面，让你可以选择要更新的包。

3. **解决冲突或不一致**：
   - 在团队协作中，如果`yarn.lock`文件存在合并冲突或需要与远程分支同步，首先解决冲突，然后运行`yarn install`以确保本地环境与`yarn.lock`文件匹配，这也会解决任何潜在的依赖不一致问题。

记住，**不要直接手动编辑`yarn.lock`文件**，除非你非常清楚自己在做什么，因为手动更改容易引入错误，导致依赖不一致。始终让Yarn工具自动管理这个文件，以保证依赖的确定性和项目环境的一致性。



### yarn更新最新版element-plus

**查看最新版本**（可选）：
在升级前，建议先查看最新版本号：

```bash
yarn info element-plus version
```

要使用 `yarn` 更新到最新版的 `element-plus`，你可以执行以下命令：

```sh
yarn add element-plus@latest
```

这将会更新你的项目中的 `element-plus` 到最新版本，并自动处理相关的依赖关系。

在更新完成后，你可能需要检查项目的兼容性，因为新版本可能会包含破坏性的变更（Breaking Changes）。查看 `element-plus` 的官方 [GitHub releases page](https://github.com/element-plus/element-plus/releases) 或者 [更新日志](https://element-plus.org/#/zh-CN/changelog)，以获取有关新版本的信息和任何必要的迁移指南。

如果你遇到任何问题或者需要按需引入组件而不是全局引入，请确保你的构建配置支持 Tree Shaking 并正确配置了相关插件，例如 `babel-plugin-component`。如果你是按需引入，记得更新 `.babelrc` 或 `babel.config.js` 文件中的插件设置以匹配最新版 `element-plus` 的要求。

#### 升级了运行报错，怎么恢复到原来的版本

如果你在升级 `element-plus` 后遇到了错误，并希望回退到之前的版本，可以通过以下步骤来恢复：

1. **确认你想要回退的版本号**：如果你之前有记录所使用的 `element-plus` 版本号，可以直接使用。如果没有，可以检查项目的 `yarn.lock` 文件或者你的 `package.json` 备份来找回旧版的版本号。

2. **卸载当前版本的 `element-plus`**：
    ```sh
    yarn remove element-plus
    ```

3. **安装特定版本的 `element-plus`**：用你之前确认好的版本号替换下面命令中的 `x.x.x`。
    ```sh
    yarn add element-plus@x.x.x
    ```

例如，如果要安装版本 1.2.0，你应该运行：
```sh
yarn add element-plus@1.2.0
```

4. **验证安装**：确保项目依赖正确更新，并尝试重新运行你的项目以确认问题是否解决。
    ```sh
    yarn run serve # 或者其它你用来启动项目的命令
    ```

5. **（可选）锁定版本**：为了防止意外再次升级，可以在 `package.json` 中明确指定 `element-plus` 的版本号，这样即使执行 `yarn upgrade` 命令也不会轻易改变这个依赖的版本。

如果遇到任何问题或需要进一步的帮助，请参考 `element-plus` 的官方文档或社区支持。同时，建议在进行任何重大改动前备份你的项目，以便于回滚更改。

