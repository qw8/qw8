---
title: nvm
date: 2019-12-09 19:25:55
categories: 
- 前端知识
tags:
- Node
---

### 1、nvm是什么

  nvm全名node.js version management，顾名思义是一个nodejs的版本管理工具。通过它可以安装和切换不同版本的nodejs。下面列出下载、安装及使用方法。



### 2、下载

  可在[点此在github](https://github.com/coreybutler/nvm-windows/releases)上下载最新版本,本次下载安装的是windows版本。打开网址我们可以看到有两个版本：

- nvm-noinstall.zip：绿色免安装版，但使用时需进行配置。
- nvm-setup.zip：安装版，推荐使用



### 3、安装

  本次演示的是安装版。

  1、双击安装文件 nvm-setup.exe

  ![img](https://img2018.cnblogs.com/blog/775046/201904/775046-20190411160657751-1529010875.png)

  2、选择nvm安装路径

  ![img](https://img2018.cnblogs.com/blog/775046/201904/775046-20190411160816834-99504468.png)

  例如：E:\Software\nvm

  3、选择nodejs路径

  ![img](https://img2018.cnblogs.com/blog/775046/201904/775046-20190411161045308-1947410693.png)

  例如：E:\Software\nvm\nodejs

  4、确认安装即可

   ![img](https://img2018.cnblogs.com/blog/775046/201904/775046-20190411171705646-891139870.png)

  5、安装完确认

  打开CMD，输入命令 nvm ，安装成功则如下显示。可以看到里面列出了各种命令，本节最后会列出这些命令的中文示意。

![img](https://img2018.cnblogs.com/blog/775046/201904/775046-20190411172641876-1326770838.png)



### 4、安装/管理nodejs

以 **管理员身份** 打开 PowerShell 后再执行安装命令。 

1、查看本地安装的所有版本；有可选参数available，显示所有可下载的版本。

```
nvm list available
```

2、安装，命令中的版本号可自定义，具体参考命令1查询出来的列表

```
nvm install 18.17.0
```

安装最新版本

```
nvm install node
```

3、使用特定版本

```
nvm use 18.17.0
```

4、卸载指定版本

```
nvm uninstall 18.17.0
```



### 5、命令提示

1. nvm arch ：显示node是运行在32位还是64位。
2. nvm install <version> [arch] ：安装node， version是特定版本也可以是最新稳定版本latest。可选参数arch指定安装32位还是64位版本，默认是系统位数。可以添加--insecure绕过远程服务器的SSL。
3. nvm list [available] ：显示已安装的列表。可选参数available，显示可安装的所有版本。list可简化为ls。
4. nvm on ：开启node.js版本管理。
5. nvm off ：关闭node.js版本管理。
6. nvm proxy [url] ：设置下载代理。不加可选参数url，显示当前代理。将url设置为none则移除代理。
7. nvm node_mirror [url] ：设置node镜像。默认是https://nodejs.org/dist/。如果不写url，则使用默认url。设置后可至安装目录settings.txt文件查看，也可直接在该文件操作。
8. nvm npm_mirror [url] ：设置npm镜像。https://github.com/npm/cli/archive/。如果不写url，则使用默认url。设置后可至安装目录settings.txt文件查看，也可直接在该文件操作。
9. nvm uninstall <version> ：卸载指定版本node。
10. nvm use [version] [arch] ：使用制定版本node。可指定32/64位。
11. nvm root [path] ：设置存储不同版本node的目录。如果未设置，默认使用当前目录。
12. nvm version ：显示nvm版本。version可简化为v。

- 查看远程版本

```undefined
nvm ls-remote
```

- 查看安装版本

```undefined
nvm ls
```

- 设置Node默认版本

```csharp
nvm alias default x.x.x
```

- 设置别名

```css
nvm alias 别名 x.x.x
```

- 删除别名

```css
nvm unbalias 别名 x.x.x
```

- 恢复Path

```undefined
nvm deactivate
```

#### 删除 nvm

- 卸载 nvm

```undefined
nvm unload
```

- 手动卸载

```bash
$ rm -rf "$NVM_DIR"
```

编辑 `~/.bashrc` 并删除以下行：

```bash
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
[[ -r $NVM_DIR/bash_completion ]] && \. $NVM_DIR/bash_completion
```



### 6、总结

本节列出node.js版本管理工具nvm的安装及使用，需要注意的是安装路径最好不要出现中文和空格。



### 7、补充

#### 1、配置nvm镜像

在安装目录下settings文件中新增如下两行

```
node_mirror: https://npm.taobao.org/mirrors/node/ 
npm_mirror: https://npm.taobao.org/mirrors/npm/
```

#### 2、安装yarn

```
npm install -g yarn
```

如果设置过npm安装路径，需要从npm安装路径手动拷贝yarn相关文件和node_modules下yarn文件夹到对应版本或者node.js目录。最终目录如下：

![img](https://img2023.cnblogs.com/blog/775046/202212/775046-20221204171059766-1926423572.png)

#### 3、配置npm、yarn

##### 3.1、配置npm全局包路径、缓存路径、镜像

nvm安装目录下nodejs文件夹新建npm_global、npm_cache目录

```
npm config set prefix "E:\Software\nvm\nodejs\npm_global"
npm config set cache "E:\Software\nvm\nodejs\npm_cache"
npm config set registry https://registry.npm.taobao.org/
```

##### 3.2、配置yarn全局包路径、缓存路径、镜像

nvm安装目录下nodejs文件夹新建yarn-global、yarn_cache目录

```
yarn config set global-folder "E:\Software\nvm\nodejs\yarn-global"
yarn config set cache-folder "E:\Software\nvm\nodejs\yarn_cache"
yarn config set registry https://registry.npm.taobao.org/
```

 

### 8、问题及处理

#### 1、提示npm不能识别

网络或者其他原因导致npm没有正常被下载安装，可手动下载安装。

##### 1.1、node版本和npm版本对应查询

[点击查看](https://nodejs.org/zh-cn/download/releases/)

##### 1.2、下载对应版本的npm

[点击此处并选择对应版本下载](https://npm.taobao.org/mirrors/npm/)

下载解压后重命名为npm，粘贴到nvm安装的node目录下的\node_modules文件夹，目录如下

![img](https://img2022.cnblogs.com/blog/775046/202204/775046-20220412200207640-1196504984.png)

把bin下的npm、npmx相关文件拷贝到node路径下

![img](https://img2022.cnblogs.com/blog/775046/202204/775046-20220412200221840-490056859.png)

然后 npm -v 即可

#### 2、Cannot find module '@npmcli/config' 或者 npm vx.x.x is known not to run on Node.js vx.x.x.

nodejs和npm版本对应关系不对，可手动安装或者更新nvm至最新版本后重新安装对应版本nodejs

原文链接：https://www.cnblogs.com/gaozejie/p/10689742.html

#### 3.Error extracting from Node archive: open C:\Program Files\nvm\v18.17.0\node-v18.17.0-win-x64\corepack.cmd: Access is denied.

Could not download node.js v18.17.0 64-bit executable.

访问被拒绝的问题，这通常发生在尝试访问没有足够权限的目录或文件时。 

以管理员身份运行安装程序或命令提示符。右键点击安装程序或命令提示符图标，然后选择“**以管理员身份运行**”。 