---
title: python
date: 2024-02-26 09:44:06
categories: 
- 其他
tags:
- python
---

### 兴趣

扒站
Python爬取网站
仿站工具
网站克隆
扒网站



# 知识

### 安装Python

你可以从Python官方网站（https://www.python.org/downloads/）下载并安装Python。确保下载适合你操作系统的版本。如 [Windows installer (64-bit)](https://www.python.org/ftp/python/3.12.2/python-3.12.2-amd64.exe) 

特别要注意勾上 Add Python 3.5 to PATH，然后“lnstall Now”即可完成安装，默认会安装到 C：\Python35 目录下。

安装完成后， 打开命令提示符窗口（方法是点击“开始”-“运行”-输入：“cmd”），敲入 Python 后，会出现“Python 3.11.0”等内容。



## python包管理工具pip

### 一、什么是 pypi

![pip 官网.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/283000f79197495ab840e910fe12ae0b~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=1378&h=813&s=100086&e=png&b=006faf)

> The Python Package Index 是 python 软件包的存储库。在这里可以找到社区中你需要的 python 软件包。

pipy 中有 50+ 多万个项目，500+ 万加的释放，以及 76+ 万的用户。python 生态庞大，值得拥抱。

### 二、什么是 pip

![pip 包.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f2725c984b994612a34074e2ffa160a3~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=1107&h=225&s=19559&e=png&b=006cab)

> The Python Package Installer python 的包管理工具

### 三、资源

- [pip 官网](https://link.juejin.cn?target=https\\%3A\\%2F\\%2Fpypi.org\\%2Fproject\\%2Fpip\\%2F)
- [pip 包管理库](https://link.juejin.cn?target=https\\%3A\\%2F\\%2Fgithub.com\\%2Fpypa\\%2Fpip)

### 四、自带 pip 的 python

> 🚨🚨🚨注意：Python 2.7.9 + 或 Python 3.4+ 以上版本都自带 pip 工具。

### 五、安装 pip

如果你还没有 pip 可以安装，带有 pip 的 python 版本。

- `py -m ensurepip --upgrade` ensurepip 确认模块
- 使用 [get-pip](https://link.juejin.cn?target=https\\%3A\\%2F\\%2Fbootstrap.pypa.io\\%2Fget-pip.py) 引导安装

### 六、pip 命令详解

> pip --help 获取所有 pip 命令提示

- 升级pip： `pip install -U pip`
- 安装

```sh
sh 代码解读复制代码pip install pkg              # 最新版本
pip install pkg==1.0.4       # 指定版本
pip install 'pkg>=1.0.4'     # 最小版本

pip install tmuxp # 安装 tmuxp 示例
```

- 升级包`：pip install --upgrade pkg`
- 搜索包: `pip search pkg`
- 显示包信息：`pip show/pip show -f pkg`
- 显示所有已经安装的包：`pip list`(`pip list -o` 可升级)

### 七、pip 镜像站

- [清华开源镜像站](https://link.juejin.cn?target=https\\%3A\\%2F\\%2Fmirrors.tuna.tsinghua.edu.cn\\%2Fhelp\\%2Fpypi\\%2F)
- [阿里云镜像站](https://link.juejin.cn?target=https\\%3A\\%2F\\%2Fmirrors.aliyun.com\\%2Fpypi\\%2F)
- [豆瓣镜像站](https://link.juejin.cn?target=http\\%3A\\%2F\\%2Fpypi.douban.com\\%2Fsimple\\%2F)
- [中科大进镜像站](https://link.juejin.cn?target=https\\%3A\\%2F\\%2Fpypi.mirrors.ustc.edu.cn\\%2Fsimple\\%2F)

### 八、requirements.txt 记录python包管理工具

#### 8.1）什么是 requirements.txt

requirements.txt 是 python 在不同的环境中对依赖包的一种约定，用于列出 Python 项目中所有的依赖包以及对应版本号的文本文件。一般在项目的在工程目录下。

#### 8.2）requirements.txt 格式

```sh
sh 代码解读复制代码pkg==version 等于版本
pkg>version 大于版本
pkg<version 小于版本
pkg>=version 大于等于版本
pkg<=version 小于等于版本
pkg~=version 大于版本
pkg >= 1.0, <=2.0 容版本，使用任何大于或等于指定版本，但不大于当前发行系列的版本，
```

#### 8.3）一个简单的示例

```txt
txt 代码解读复制代码touch requirements.txt

# 输入
requests==2.26.0
numpy>=1.21.4
pandas<=1.3.5
```

#### 8.4）pip 安装 requirements.txt 中的包

```sh
sh 代码解读复制代码pip install -r requirements.txt
```

#### 8.5）更新 requirements.txt 中的包

```sh
sh 代码解读复制代码pip freeze > requirements.txt
```

### 九、python 中常用包推荐

| 领域               | 库名称                | 描述                                                         |
| ------------------ | --------------------- | ------------------------------------------------------------ |
| 数据处理与科学计算 | NumPy                 | 用于数值计算，提供高效的多维数组对象和操作。                 |
|                    | Pandas                | 用于数据处理和分析，提供了数据结构和工具。                   |
|                    | SciPy                 | 提供了许多科学计算的工具包，包括数值积分、优化、信号处理等。 |
|                    | matplotlib            | 用于绘制图表和数据可视化。                                   |
| 机器学习与人工智能 | Scikit-learn          | 提供了各种机器学习算法和工具。                               |
|                    | TensorFlow 或 PyTorch | 用于深度学习和神经网络。                                     |
|                    | Keras                 | 用于构建和训练神经网络的高级 API。                           |
| Web 开发           | Flask 或 Django       | Web 应用程序框架，用于构建 Web 应用。                        |
|                    | requests              | 用于 HTTP 请求和访问 Web 数据。                              |
| 自然语言处理       | NLTK                  | 用于自然语言处理的库，包含了丰富的语料库和算法。             |
|                    | spaCy                 | 提供了高效的自然语言处理工具。                               |
| 测试               | unittest              | Python 内置的单元测试框架。                                  |
|                    | pytest                | 简化测试的库，支持更多的测试特性。                           |
| 图像处理           | Pillow                | 用于图像处理的库，支持图像格式的处理和基本图像操作。         |
| 数据库             | SQLAlchemy            | 用于数据库操作的库，提供了高层的 SQL 工具。                  |
|                    | pymongo               | 用于 MongoDB 数据库的 Python 客户端库。                      |
| 加密与安全         | cryptography          | 提供了加密工具和算法。                                       |
| 请求相关           | Requests              | 简单易用的 HTTP 请求库，用于发送各种类型的 HTTP 请求。       |
| HTML 解析相关      | Beautiful Soup        | 用于解析 HTML 和 XML 文档，功能强大且灵活。                  |
| 游戏开发           | Pygame                | 用于创建 2D 游戏的库，提供了图形、声音和输入的支持。         |
|                    | Pyglet                | 用于开发游戏和多媒体应用程序的库，支持 OpenGL。              |
|                    | Ren'Py                | 用于创建视觉小说和交互式故事的框架。                         |
|                    | Arcade                | 适用于初学者的 2D 游戏开发库，旨在简化游戏开发过程。         |
|                    | PyOpenGL              | Python 的 OpenGL 实现，允许直接访问 OpenGL API。             |

### 十、小结

本文主要关注 pip 包管理工具以及使用方法，pip 已经在内置到了新版的 python 中，使用 pip 可方便的管理 python 的第三方依赖。同时 pip 可以通过 requirements.txt 来配置当前项目的依赖以及版本，可以很好的管理自不同环境中包的依赖问题，最后推荐了一些 python 生态中常用的包，希望能够帮助到你。

原文链接：https://juejin.cn/post/7313758022486409255







# 项目

### Python经典入门开源项目及链接

对于想要通过实际项目来学习Python编程的朋友来说，参与开源项目是一个非常好的方式。这不仅能帮助你提高编程技能，还能让你了解软件开发的流程、版本控制等重要概念。下面列出了一些适合初学者参与的Python开源项目，以及它们的GitHub链接。请注意，项目的活跃程度和社区支持可能会随时间变化，请访问相应网站查看最新情况。

1. **Flask** - 一个轻量级的Web应用框架。
   - GitHub: [https://github.com/pallets/flask](https://github.com/pallets/flask)

2. **Django** - 一个高级的Web框架，鼓励快速开发和干净、实用的设计。
   - GitHub: [https://github.com/django/django](https://github.com/django/django)

3. **Scrapy** - 用于网络爬虫和数据抓取的强大框架。
   - GitHub: [https://github.com/scrapy/scrapy](https://github.com/scrapy/scrapy)

4. **Pandas** - 提供高性能的数据结构和数据分析工具。
   - GitHub: [https://github.com/pandas-dev/pandas](https://github.com/pandas-dev/pandas)

5. **NumPy** - 支持大量维度数组与矩阵运算，并针对数组操作提供大量的数学函数库。
   - GitHub: [https://github.com/numpy/numpy](https://github.com/numpy/numpy)

6. **Requests** - 用Python发起HTTP请求变得简单。
   - GitHub: [https://github.com/psf/requests](https://github.com/psf/requests)

7. **Beautiful Soup** - 用于解析HTML和XML文档的库。
   - GitHub: [https://github.com/bkjones/beautiful-soup-4](https://github.com/bkjones/beautiful-soup-4) (注意：这个链接指向的是BeautifulSoup 4的一个分支；官方文档通常会指导到正确的位置)

8. **TensorFlow** - 由Google开发的开源机器学习库。
   - GitHub: [https://github.com/tensorflow/tensorflow](https://github.com/tensorflow/tensorflow)

9. **PyTorch** - Facebook的人工智能研究小组FAIR开发的深度学习库。
   - GitHub: [https://github.com/pytorch/pytorch](https://github.com/pytorch/pytorch)

10. **OpenCV-Python** - 计算机视觉库。
    - GitHub: [https://github.com/opencv/opencv/tree/master/samples/python](https://github.com/opencv/opencv/tree/master/samples/python) (这里列出了使用Python的例子)

除了直接贡献代码之外，很多项目也欢迎非代码贡献，比如改进文档、报告错误或提出新功能建议。选择适合自己兴趣和技术水平的项目开始吧！记得在参与之前先阅读该项目的贡献指南。
