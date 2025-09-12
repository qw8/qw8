---
title: VSCode
date: 2024-06-08 11:58:08
categories: 
- 其他
tags:
- 电脑
---

### 下载安装

https://code.visualstudio.com/



### vscode设置中文的方法

首先打开vscode ，并按快捷键“Ctrl+Shift+P”；

然后输入“configure language”，并回车；

最后选择简体中文安装即可。



### 快捷键设置

格式化文档，Ctrl+L

切换行注释，Ctrl+/

向下复制行，Ctrl+D



### vscode设置代码格式化缩进为4个空格

- 在设置中搜索“tabsize” ，将下图中两个地方都改为4

- 搜索:“detectindentation”，将前面的勾选去了
- 找到"Editor: Insert Spaces"选项，并确保其设置为"false"，表示要使用tab键插入tab而不是空格。 

有的时候设置了是4个空格，但是格式化代码仍然是两个空格。原因是代码在之前的电脑上被格式化过，之前的电脑设置的是两个空格。而现在使用自己的电脑虽然设置的是4个空格， 但是在vscode的设置中detectindentation没有去掉，导致打开的时候vscode会自动检查代码的空格风格，认为是2个空格，导致我们设置的4个空格的缩进失效。



### 怎么让电脑底部状态栏vscode图标显示两个

在Windows 10及更高版本中，任务栏可能会自动组合相似的应用程序图标。如果你希望每个VSCode实例都有自己的独立图标，你可能需要调整任务栏设置来禁用这种组合。这可以通过右键点击任务栏，选择“任务栏设置”，然后在“合并任务栏按钮”选项中选择“从不”来实现。



### VSCode如何让先前打开的文件不被自动关闭，一直保持在标签栏里（关闭预览模式）

第一次接触VSCode IDE编辑器，每次打开一个新的代码文件，旧的代码文件都会被自动关闭（现在才知道是因为文件默认是以预览模式打开展示的）。

那么如何才能让先前打开的文件一直保持在标签栏里呢？

我们需要去设置界面。
点击VSCode IDE左下角的齿轮，选择设置，进入设置页面：

![image.png](https://bbs-img.huaweicloud.com/blogs/img/20211228/1640671388695018963.png)

或则直接快捷键Ctrl+shift+p键 / F1键 打开搜索框，输入open workspace setting 进入设置界面：

![image.png](https://bbs-img.huaweicloud.com/blogs/img/20211228/1640671438166004799.png)

然后在设置界面里，搜索“workbench.editor.enable”，会显示下面这些选项，全都不要勾选（已勾选的取消掉）

![image.png](https://bbs-img.huaweicloud.com/blogs/img/20211228/1640671490294019996.png)

这样，我们打开的代码文件就不会被自动关闭了。

如果后期需要自动关闭，勾选第一个即可。



### VSCode比较两个文件的区别

 1、首先打开编辑器，先从左边点击选中一个要比较的文件。

![vscode怎么比较两个文件的区别? vscode比较两个文件方法](http://img3.downza.cn/xueyuan/202208/7a6b496403e89ad4eba58a9701c3958e.jpg)

   2、然后按着键盘上的ctrl键，点击选中另一个要比较的文件。

![vscode怎么比较两个文件的区别? vscode比较两个文件方法截图](http://img3.downza.cn/xueyuan/202208/03d87e0f3ebd168581a8778981512419.jpg)

   3、选中后，右键点击，然后点击右键菜单上的compare selected(比较所选文件)。

![vscode怎么比较两个文件的区别? vscode比较两个文件方法截图](http://img3.downza.cn/xueyuan/202208/08d952ab26ed3f181eb651dc9dc399cc.jpg)

   4、接着打开后，可以看到左右二个文件有哪些不同的地方了。VSCODE会将两个文件按左右分隔，不一样的地方会红色高亮显示，右侧的状态柱标红色的地方就表示为不同，可以直接点击红色的地方快速查看。

![vscode怎么比较两个文件的区别? vscode比较两个文件方法截图](http://img3.downza.cn/xueyuan/202208/1f81e4798d64e4ce0fbe36667e304464.jpg)

   5、如果差异的地方比较多，我们可以使用右上角的这里二个按钮，分别是跳到上一个/下一个有差异的地方。

![vscode怎么比较两个文件的区别? vscode比较两个文件方法截图](http://img3.downza.cn/xueyuan/202208/67f976110d6741077ab927edc7745ef7.jpg)

   6、最后在比较文件差异的同时，我们还可以实时更改二个文件的内容。

![vscode怎么比较两个文件的区别? vscode比较两个文件方法截图](http://img3.downza.cn/xueyuan/202208/46651b384b4e723d383efd23adf0c785.jpg)

### vscode卡顿问题解决办法

VSCode作为一款强大的编辑器，使用顺手的时候无比丝滑，但是也有让人发狂的问题，(⊙o⊙)…，比如卡顿。

原因分析：编辑代码的时候，IDE会分析代码，对于他而言就是遍历文件，较大的文件内存消耗随之而来，调整下配置文件，这个问题就可以解决了

项目根目录： .vscode/setting.json

添加以下配置

```
    "search.followSymlinks": false,
    "disable-hardware-acceleration": true,
```

丝滑的提示配置

```
	"files.associations": \\{
        "*.cjson": "jsonc",
        "*.wxss": "css",
        "*.wxs": "javascript",
        "*.vue": "vue",
    \\},
```

下面是对各配置项的简要说明：

#### 文件排除(`files.exclude`)

这一部分定义了编辑器应当忽略的文件和文件夹，有助于提高文件搜索、索引构建等操作的速度，以及保持工作区的整洁。

- `"node_modules": true`: 忽略`node_modules`文件夹，这是Node.js项目中存放依赖包的地方，通常包含大量文件，不直接参与编码工作。
- `"**/.hg": true`, `"**/CVS": true`, `"**/.DS_Store": true`, `"**/Thumbs.db": true`: 分别忽略Mercurial版本控制系统、CVS版本控制系统、Mac OS的.DS_Store隐藏文件和Windows的Thumbs.db缩略图缓存文件，这些都是通常不需要编辑或查看的系统或版本控制相关的文件。

#### 遵循符号链接(`search.followSymlinks`)

- `"search.followSymlinks": false`: 设置搜索时不遵循符号链接（symlinks）。这意味着当你在编辑器中进行搜索时，符号链接指向的文件或目录不会被纳入搜索范围。这可以减少搜索范围，加快搜索速度，尤其是在项目结构复杂时。

#### 禁用硬件加速(`disable-hardware-acceleration`)

- `"disable-hardware-acceleration": true`: 禁用编辑器的硬件加速功能。对于一些用户来说，禁用硬件加速可以解决图形显示问题或性能问题，尽管这通常是以牺牲一些图形性能为代价的。

#### 文件关联(`files.associations`)

这部分用于指定文件扩展名与语言模式的关联，使得编辑器能以正确的语法高亮和智能提示来处理文件。

- `"*.cjson": "jsonc"`: 将所有`.cjson`扩展名的文件识别为JSONC（JSON with Comments）格式。
- `"*.wxss": "css"`: 将`.wxss`（Weixin Style Sheets，微信小程序专用样式表）文件识别为CSS格式。
- `"*.wxs": "javascript"`: 将`.wxs`（Weixin Script，微信小程序中的脚本文件）识别为JavaScript格式。
- `"*.vue": "vue"`: 确保`.vue`文件被正确识别为Vue单文件组件格式，这样就可以获得Vue模板、script和style部分的语法高亮和智能提示。

通过这些配置，用户能够优化编辑器的工作环境，提升开发效率。



### vscode设置js文件使用单引号

是的，`.editorconfig` 文件可以用来配置代码风格，包括是否使用单引号。`EditorConfig` 是一种跨编辑器和 IDE 的文件格式，用于维护一致的编码风格。它可以应用于整个项目或单个文件，并且能够很好地与其他工具（如 ESLint 和 Prettier）协同工作。

#### 如何使用 `.editorconfig` 配置单引号

1. **创建或修改 `.editorconfig` 文件**：
   在项目根目录下创建或修改 `.editorconfig` 文件。如果文件不存在，可以创建一个。

2. **配置单引号**：
   在 `.editorconfig` 文件中添加或修改相关配置项。

#### 示例配置

以下是一个示例 `.editorconfig` 文件，用于配置单引号和其他一些编码风格：

```ini
# top-most EditorConfig file
root = true

[*]
charset = utf-8
indent_style = space
indent_size = 2
end_of_line = lf
trim_trailing_whitespace = true
insert_final_newline = true

[*.js]
quote_type = single

[*.ts]
quote_type = single

[*.vue]
quote_type = single
```

#### 解释配置项

- `charset = utf-8`：指定字符集为 UTF-8。
- `indent_style = space`：指定使用空格进行缩进。
- `indent_size = 2`：指定缩进大小为 2 个空格。
- `end_of_line = lf`：指定行结束符为 Linux 样式（换行符 `\n`）。
- `trim_trailing_whitespace = true`：指定在文件保存时移除尾随空白字符。
- `insert_final_newline = true`：指定在文件末尾插入一个新行。
- `[*.js]`：针对所有 `.js` 文件的配置。
- `[*.ts]`：针对所有 `.ts` 文件的配置。
- `[*.vue]`：针对所有 `.vue` 文件的配置。
- `quote_type = single`：指定使用单引号。

#### 配合 VSCode 使用

为了确保 `.editorconfig` 文件能够在 VSCode 中生效，你需要安装 `EditorConfig for VSCode` 扩展。这个扩展可以帮助 VSCode 遵循 `.editorconfig` 文件中的设置。

1. **安装 `EditorConfig for VSCode` 插件**：
   - 打开 VSCode 的 Extensions 面板（可以通过侧边栏的 Extensions 图标或按 `Ctrl + Shift + X` 打开）。
   - 搜索 `EditorConfig for VSCode` 并安装它。

2. **重启 VSCode**：
   - 重启 VSCode 以确保所有设置都能正确加载。

#### 确认效果

一旦安装了 `EditorConfig for VSCode` 插件并重启了编辑器，当你编辑 `.js`、`.ts` 或 `.vue` 文件时，应该会看到代码自动使用单引号进行格式化。

#### 注意事项

- 确保没有其他插件或配置文件（如 `.prettierrc` 或 `.eslintrc`）覆盖了 `.editorconfig` 的设置。
- 如果你在使用 Prettier 或 ESLint，确保它们的配置文件中没有与 `.editorconfig` 冲突的设置。

通过以上步骤，你应该可以在 VSCode 中通过 `.editorconfig` 文件配置单引号以及其他编码风格。如果还有问题，请确保所有相关配置文件都已正确设置，并且重启 VSCode 以确保所有更改生效。



### vscode格式化代码，js双引号变单引号，不要；

解决 vscode 格式化代码 去掉代码结尾的分号 与 使用单引号替代双引号 失效的问题

在某些项目里 prettier 单引号格式化 会失效

```
“prettier.semi”: true, //去掉代码结尾的分号
“prettier.singleQuote”: true, //使用带引号替代双引号
```

以上配置没有效果

prettier3.7以上会优先读取项目根目录下的editorconfig or prettier config，如果有，就不会使用vscode setting中的设置，所以最好每个项目都配置一个单独的 prettier 配置 文件。

并且在.editorconfig 中没法配置行末不加分号，所有，只能配置一个 prettier文件了。

在根目录下创建名为.prettierrc的文件

```
\\{
    “tabWidth”: 2,
    “useTabs”: false,
    “singleQuote”: true,
    “semi”: false
\\}
```



## prettier怎么设置属性换行vscode中

在 VS Code 中配置 Prettier 实现属性换行，主要通过 `singleAttributePerLine` 和 `printWidth` 两个核心选项控制。以下是详细设置步骤及示例：

------

### ⚙️ 1. **核心配置选项**

- `singleAttributePerLine`设置为 true时，强制每个 HTML/Vue/JSX 属性独占一行；

  false时则按长度自动换行。

  ```
  // .prettierrc 示例
  \\{
    "singleAttributePerLine": true, // 强制每行一个属性
    "printWidth": 80               // 行宽阈值，超长则换行
  \\}
  ```

- **`printWidth`**
   定义单行最大字符数（默认 80），超限时 Prettier 会自动将属性换行显示。

------

### 📁 2. **通过项目配置文件设置（推荐）**

在项目根目录创建 **`.prettierrc`** 或 **`.prettierrc.json`**，添加以下配置：

```
\\{
  "singleAttributePerLine": true, // 强制属性换行
  "printWidth": 100,              // 自定义行宽
  "htmlWhitespaceSensitivity": "ignore" // 忽略 HTML 空格敏感度
\\}
```

- 文件类型覆盖：针对特定文件（如 Vue）单独配置：

  ```
  \\{
    "overrides": [
      \\{
        "files": "*.vue",
        "options": \\{
          "singleAttributePerLine": true
        \\}
      \\}
    ]
  \\}
  ```

------

### ⚡ 3. **在 VS Code 中直接配置**

修改 **`settings.json`**（`Ctrl + ,` → 点击右上角 JSON 图标）：

```
\\{
  "editor.defaultFormatter": "esbenp.prettier-vscode", // 启用 Prettier
  "editor.formatOnSave": true,                         // 保存时自动格式化
  "prettier.singleAttributePerLine": true,             // 强制属性换行
  "prettier.printWidth": 120,                          // 自定义行宽
  "[vue]": \\{                                           // 针对 Vue 文件
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  \\}
\\}
```

------

### ⚠️ 4. **注意事项**

- **优先级问题**：
   VS Code 的 `settings.json` 配置会覆盖项目中的 `.prettierrc` 文件。

- 插件冲突：

  若同时使用 ESLint 或 Vetur，需确保配置兼容：

  - 在 ESLint 中禁用冲突规则（如 `newline-per-chained-call`）。
  - Vetur 需关闭自动格式化（`"vetur.format.enable": false`）。

- **重启生效**：
   修改配置后需重启 VS Code 以使设置生效。

------

### 💎 5. **完整配置示例**

```
// .prettierrc
\\{
  "singleAttributePerLine": true,
  "printWidth": 100,
  "tabWidth": 2,
  "useTabs": false,
  "semi": true,
  "singleQuote": true,
  "trailingComma": "all",
  "bracketSpacing": true,
  "htmlWhitespaceSensitivity": "ignore"
\\}
```

------

### 💎 总结

- **强制所有属性换行** → 设 `"singleAttributePerLine": true`。
- **按长度智能换行** → 仅设 `printWidth`（如 `120`），不启用 `singleAttributePerLine`。
- **避免工具冲突** → 统一团队配置，优先使用项目级 `.prettierrc` 文件。

> 配置后若未生效，检查 VS Code 底部状态栏是否已切换为 Prettier 格式化工具，或通过命令面板运行 `Format Document With...` 手动选择 Prettier。







# 快捷键

### 10个最常用的VSCode快捷键

使用VS Code快捷键可以提高编程速度，让你在使用这个工具时看起来像是一个专家。让我们逐个看一下每个快捷键。

![图片](https://mmbiz.qpic.cn/mmbiz/KEXUm19zKo5fSOichXs2eHVdr8BMl66UWs9z16aUR6yiaUzF00khCicTwVcvuTr7y9wGWOVNUI9Udy70QVOe3Pm1Q/640?wx_fmt=other&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

#### 1、打开命令面板

如果你是初次接触 VS Code 编辑器，那么这个快捷键可能是你学习的最重要的键盘组合之一。

命令面板提供了对 VS Code 中的所有功能、快捷键、命令和配置选项的访问。

你可以使用以下键盘组合调用命令面板：

> Windows — Ctrl + P
>
> Mac — Command + P

![图片](https://mmbiz.qpic.cn/mmbiz/KEXUm19zKo5fSOichXs2eHVdr8BMl66UWVN98icX94PHaNCCjicZctYiaFqqOEG6eMTamfLvLsS9hmkf40ZLJPiaY5Q/640?wx_fmt=other&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

#### 2、切换注释行

传统上，你必须将光标放置在一行代码的开头，然后键入/ /（双斜杠）将其转换为注释。

VS Code 提供了一个更简单的注释代码行的方法。使用此快捷键，可以在光标所在行的任何位置切换注释行。

下面是在 Windows 和 Mac 上切换代码行的快捷键。

> Windows — Ctrl + /
> Mac — Command + /

#### 3、切换终端

VS Code（Visual Studio Code）内置了终端，您可以在其中运行所有命令，例如启动服务器（后端），运行应用程序（前端），更改目录（cd），安装软件包等等。

当构建复杂的 Web 应用程序时，我总是保持终端打开，因为我经常安装软件包，并且还检查终端以查看我的正在运行的进程是否崩溃。

如果您也需要更多的工作空间，可以关闭终端。

以下是在 Windows 和 Mac 上切换到终端的键盘快捷键：

> Windows — Ctrl + `
> Mac — control + `

![图片](https://mmbiz.qpic.cn/mmbiz/KEXUm19zKo5fSOichXs2eHVdr8BMl66UW9c1mD1qU9iayKLZmTyFjjyyL3sb3qM2ydDEZ6ia169KiaafryjtJc04Lw/640?wx_fmt=other&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

#### 4、打开用户设置

通常，当你想要更改一些设置时，你会点击右下角的齿轮图标，或者通过导航到文件菜单- > 首选项 -> 设置进行设置。

与使用鼠标单击以到达设置所需的点击相比，更简单的选择是使用快捷键。

你可以使用以下快捷键打开设置并进行所需的配置。

在VS Code中，你可以在视觉编辑器设置或设置的JSON文件中更改设置。

假设你想增加字体大小以使字符更加清晰可见，你可以使用以下快捷键打开设置，然后搜索字体大小并将其更改为所需的数字，更改将立即生效。

> Windows - Ctrl +，
>
> Mac - Command +，

![图片](https://mmbiz.qpic.cn/mmbiz/KEXUm19zKo5fSOichXs2eHVdr8BMl66UWtAaSPzPiakL7qz0TAr8zeiaib6aVIppib9ICicWNQrXjYXxfP7GtyK6umgQ/640?wx_fmt=other&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

#### 5、上下移动代码行

通常当您想要将一行代码上下移动时，您会选择剪切和粘贴或复制和粘贴该行代码。

当您复制和粘贴一行代码时，您必须删除原始行。

我知道你通常会选择剪切和粘贴一行代码，因为那是更好的做法，但是移动代码行有更好、更快的方式。

您可以使用以下命令将代码行向下或向上移动，而不必复制和粘贴它然后再删除原始行。

> Windows: Alt + Up Arrow / Down Arrow
>
> Mac: OPTION + Up Arrow / Down Arrow

![图片](https://mmbiz.qpic.cn/mmbiz/KEXUm19zKo5fSOichXs2eHVdr8BMl66UWLF0jVkSDNknDS2JWny3adOOn1QX0IWKsiaiaPOWXrcsFdNXQEsd8FvLA/640?wx_fmt=other&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

#### 6、打开文件选项卡

如果你想快速地在不使用鼠标的情况下移动到另一个标签页，这个快捷键会非常有用。通常在创建应用程序时，你会打开多个文件并使用鼠标单击特定文件进行编辑。

VS Code 提供了一个更简单的方法在不使用鼠标的情况下在标签页之间进行切换。

以下是可以在不使用鼠标的情况下轻松从选项卡移动到另一个选项卡的命令。

> Windows — Ctrl + Tab
>
> Mac — control + Tab

![图片](https://mmbiz.qpic.cn/mmbiz/KEXUm19zKo5fSOichXs2eHVdr8BMl66UWPolzefffeFicTkyQ8u2ibsPKZtY1PDJaN41Dd2SC8KKN20uy3ibpM6ciag/640?wx_fmt=other&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

#### 7、移动文件到分割窗口

VS Code 允许在编辑文件时轻松地进行分割视图。

通常情况下，当您需要一个分割视图时，可以使用鼠标将文件拖到右侧以使用分割编辑器。

分割编辑器可以自定义为网格，当您需要同时比较和编辑多个文件时，这个功能非常有用。

以下是在 Windows 和 Mac 上使用分割编辑器的命令：

> Windows — Ctrl + \
>
> Mac — Command + \

![图片](https://mmbiz.qpic.cn/mmbiz/KEXUm19zKo5fSOichXs2eHVdr8BMl66UWpnUk3TFwmLJtxHHicEV97HDQAiauQwRIyIO7Cp0qceZg4NuPsiblibfkEw/640?wx_fmt=other&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

#### 8、复制行代码，进行上下移动

我们都有把一行代码复制粘贴来复制它的习惯。当你想要复制一行代码时，可以使用以下键盘组合来复制它。你只需要确保光标在一行代码上，然后使用以下命令向上或向下复制它。

> Windows - Shift + Alt + 上/下箭头
>
> Mac - Shift + OPTION + 上/下箭头

![图片](https://mmbiz.qpic.cn/mmbiz/KEXUm19zKo5fSOichXs2eHVdr8BMl66UWMv2nN9fJG1RdKeh4GqpsqcZCNCibLDFDJ6QHHSUKtTBNjwTDn0qtMwg/640?wx_fmt=other&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

#### 9、复制某段代码，进行上下移动

假设你想把一段选定的代码块向上或向下复制，你首先想到的可能是复制并粘贴该代码块。虽然这样做可行，但使用键盘有更好、更快的方法。要在 Windows 和 Mac 上向上或向下复制选定的代码块，请使用以下命令。

> Windows - ALT + SHIFT + 上箭头/下箭头
>
> Mac - OPTION + SHIFT + 上箭头/下箭头

![图片](https://mmbiz.qpic.cn/mmbiz/KEXUm19zKo5fSOichXs2eHVdr8BMl66UWkbicXL16WnM7uTAo3Akqc97F8CHYqw3CpxBCouLyTDDicVXJxbdN2k3Q/640?wx_fmt=other&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

#### 10、在多个位置放置光标进行编辑

VS Code的另一个有用的功能是在多个位置放置光标的能力。

假设您想在一些文本变量或值周围添加列表标记。您可以选择所有变量列表或文本，然后使用Alt + Shift + I，然后按Home键（在删除键旁边）将光标移到变量列表的开头。

这就是多个光标发挥作用的时候，您只需按住Alt + Shift + I即可一次性编辑长列表。

> Windows - Alt + Shift + I，然后按Home键
>
> Mac - Option + Shift + I，然后按Home键

![图片](https://mmbiz.qpic.cn/mmbiz/KEXUm19zKo5fSOichXs2eHVdr8BMl66UWatXc02MbWylCIhibrxbqic4Yb3n8YqDqthALGmrNGoqXIJNbQFJkGn3g/640?wx_fmt=other&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

#### 结束

当你掌握了这些在 VS Code 中使用的常用快捷键后，你将会更加高效地进行代码编辑和开发。这些快捷键可以帮助你快速定位和编辑代码，从而节省时间和提高工作效率。当你开始使用这些快捷键时，可能会感觉不太习惯，但是随着时间的推移，你会发现这些快捷键已经成为你的习惯，从而使你的工作更加顺畅和高效。让我们在 VS Code 中掌握这些快捷键，让我们的代码编辑工作变得更加轻松愉快吧！





### 快速打开指定文件

大多数前端开发，在找路由文件时可能时一级一级找，实际上在地址栏复制一下路由名称

按下`ctrl + e`，再输入路由名称即可打开。*IDEA*快捷键是双击 `shfit`

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/78773d198fdd48bd8b75bb801335659e~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=757&h=259&s=23218&e=png&b=222121)



### 快速打开项目

`ctrl + r`
 默认打开会覆盖当前窗口，按下 **ctrl** 则为多开

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/58a9f3b3c3f64be3a9b6752f8fe02e98~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=598&h=306&s=28306&e=png&b=1b1b1b)



### 全局符号搜索（函数、变量...)

ctrl + t

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/be28882773954c9eaa56c98ca125a978~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=601&h=216&s=17642&e=png&b=1c1b1b)



### 当前文件符号搜索（函数、变量...)

ctrl + shift + o

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d8e9ecebac1a4355bb3f2a5e333a7de2~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=777&h=259&s=38462&e=png&b=1e1d1b)



### 展开当前文件符号（函数、变量...)

ctrl + shift + .

![63a44d1660df77e099c5602dfe8b01a.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9c1937d9258b46cd805740cf50e4ada5~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=522&h=269&s=20089&e=png&b=151413)



### 查看引用

`alt + shift + f12`
 快速查看哪里用到了，你必须能被 VSCode 识别类型

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c0edc26fbb144ffd91cb6840ba341481~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=452&h=172&s=22603&e=png&b=191818)



### 快捷跳转

当你在看别人代码时，是不是经常 *ctrl + 鼠标左键* 进去看，然后回来要滑半天？

那你看看我怎么做，是不是瞬间回来

![1.gif](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/61fd9bcb33b848dba6af2279d5459b69~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=411&h=566&s=56406&e=gif&f=36&b=1a1816)

这个只需要设置一下快捷键即可，默认是没有的，如下图所示

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e99be25f14a847d28bc3ae68797be2d8~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=884&h=902&s=47446&e=png&b=1b1a18)



### 变量 | 文件重命名

![var.gif](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a6d2e0214388412589fe7f79a123b467~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=226&h=175&s=23099&e=gif&f=41&b=1a1816)

大家设置一下对应的快捷键即可，我下图标红的就是。我设置的和 *window* 快捷键一样， *IDEA* 默认是`shift + F6`

**如果你的 \*window\* 版本过高，那么`shift + F6`又会和微软输入法冲突**

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ce5af25dc0b74efda8b29ac343a953ca~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=696&h=480&s=37529&e=png&b=201f1d)

> 需要注意的是，变量重命名需要编辑器分析你的代码。所以如果你的代码写的很烂，那么 *VSCode* 也会被弄得神志不清
>  所以这项功能在一些 *JS* 项目可能没有作用



### 快捷复制

很多人复制当前行，可能是先选中，然后再 *CV*，实在是太慢了

*VSCode* 快捷键是 `alt + shfit + ↓`，*IDEA* 是`ctrl + d`

![8.gif](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ce80cc7b3e30450692ebdba6b211aa37~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=300&h=266&s=21029&e=gif&f=44&b=1a1816)



### 快速移动行

```
alt + ↓`，*IDEA* 为 `ctrl + shift + ↓
```

![PixPin_2024-02-11_11-17-12.gif](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c4ed9da2ff71449495a4f2debec71077~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=406&h=267&s=28430&e=gif&f=41&b=1b1917)



### 删除整行

快捷键是 `ctrl + shift + k`，这个也能提高很多效率，不用每次都手动删除一行的最后一个空格

![9.gif](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2d57f15d5a7442fe83355dbe63034a88~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=336&h=232&s=21318&e=gif&f=34&b=1a1816)



### 快速新开一行

假设你的鼠标不在行末，而在中间，如下图。那么你按下回车会破坏你的代码

此时你仅需按下 `ctrl + enter` 即可新开一行，*IDEA* 快捷键是 `shift + enter`

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/eb952dd495ca4731812e8652f6ffb890~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=267&h=122&s=2396&e=png&b=191816)



### 查看参数

在函数括号内，按下`ctrl + shift + space`，即可查看参数类型，以及当前参数的注释

**注意，微软输入法可能和这个快捷键冲突，你需要手动关闭微软输入法的快捷键，或者修改VSCode**

*IDEA* 快捷键为 `ctrl + p`

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2926f74142014b0ba70dd221e48e6d72~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=377&h=413&s=19016&e=png&b=1b1a17)



### 代码提示

这个在强类型语言上非常实用，以 *Typescript* 为例。按下 `ctrl + i` 这个字符串枚举就出来了

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1a78a5fb5a774c4dab6c833587e6770c~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=255&h=288&s=7013&e=png&b=1a1916)



### 收起/ 打开 (控制台 | 终端)

```
ctrl + j
```



## 快速滑动

按住 `alt` 再滚动滚轮，可以加快滚动速度。这个速度默认 5 倍速，可以在设置调整。
 搜索`editor.fastScrollSensitivity`



### 批量操作

假设我从某个地方复制很多变量，我需要批量修改。比如说把 *my* 改成 *test*，

此时你可能按下 *ctrl + f* 批量搜索，再批量修改，而这时我已经改完了

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6ed2a4785f244c9999436fb43a0cb673~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=206&h=204&s=3898&e=png&b=191816)

![2.gif](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7a896ead2a9c4a2badbbc91be71df3a1~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=189&h=183&s=29739&e=gif&f=64&b=1a1816)

在 *VSCode* 中，批量选中相同的快捷键是 `ctrl + shift + l`

我上面就是按下此快捷键批量修改的



### 批量大小写修改

不仅于此，我们再来发掘一下他的功能，比如批量修改大小写

这个需要手动配置，我用的是`ctrl + shift + alt + u`

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0124a08029684beb875bffca58267a40~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=834&h=219&s=12888&e=png&b=1e1d1b)

![3.gif](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4b07e51b91054efd971129f3a16df675~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=317&h=205&s=20987&e=gif&f=88&b=1a1816)



### 扩选范围

如果你需要复制某一段文字，你可能先按下鼠标左键，然后不松手慢慢拖动选中。

但是这种体验太差了，需要非常精确的操作，能不能根据代码自动扩选的呢？

答案是可以的，不过同样要手动设置快捷键，这里我设置的和 *IDEA* 一样

![4.gif](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6624f500080b4c4a99c7a3d71329d934~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=455&h=150&s=20171&e=gif&f=45&b=1a1816)

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1aa4a013fd964ac6ad57fcb95a4e5728~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=756&h=263&s=12996&e=png&b=1e1d1b)



### 双击分割

我敢说下面的双击全选，99.99\\% 的人的 *VSCode* 都做不到，而是会被 `-` 分开

![5.gif](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a354ae7dea474e55baaf4c8c9eb2c9e0~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=237&h=139&s=5069&e=gif&f=20&b=1a1816)

仅需设置一下配置即可，按下 *ctrl + ,* 打开配置 `editor.wordSeparators`，把不要的分隔符删掉即可

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3ab5525f87844bb9a15040d07201dc3f~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=802&h=236&s=17076&e=png&b=1e1d1b)



### 批量移动光标到指定位置

![6.gif](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5034d1cc574042239c53761e5d48b9cf~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=215&h=234&s=34890&e=gif&f=67&b=1a1816)

下面这一套丝滑小连招是怎么做的呢？

1. 先按住 *alt + shift*，即可开启列选择模式
2. 拖动鼠标选择
3. *ctrl + →*，可以快速跳到分隔位置，这里没有被分隔，所以直接到最后了
4. *ctl + shift + 左*，快速选中并跳转到分隔位置
5. 最后执行操作即可

基于上述操作，可以玩出花来，大家可以开动一下脑袋

**值得注意的是，`ctrl + [shift] + ←` 这些快捷键不是编辑器带来的，基本上哪里都能用**



### 快速选中整行

有时候你可能需要选中很长一行，比如打包后的代码，爬到的代码，如果有手拖动那可太折磨人了

于是你可以按下 *shift + end* 来选中，这个就不放动图，和上面差不多。*shift* 就是多选的意思

不过有的人的键盘可能没有 *end* 按键，这时候可以查一下官网，大多数都是配合 *FN* 键实现



### 选中指定行

![7.gif](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8df43a0a25474021a96db1379b83946e~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=247&h=242&s=30383&e=gif&f=72&b=1a1816)

按住 *alt* 不放，加上鼠标点击即可

而且你不必精确选中列的位置，可以用 *end | home* 回到开头或者结尾，再配合上面的技巧操作



### 批量修改正则指定内容

按下 *ctrl + f*，把最右边的 `.*` 勾选上，就是开启正则的意思

然后再输入表达式，`\d` 即所有数字，$1即匹配到的第一组

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9239407d22204aeda3d505645aceb3eb~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=553&h=414&s=25634&e=png&b=1c1b19)

按下最右边的全部修改，结果就会改成下图，所有数字都会加上 *test* 后缀

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/96cd077b297b4eb084d012c37a93ffb0~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=244&h=249&s=7863&e=png&b=191816)

不止于此，还能整个文件夹批量检索操作

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a9defc8f4ef84fcb9b11b458cd4bec2f~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=407&h=358&s=21025&e=png&b=1e1d1d)



### 路径操作

很多人可能苦于导入路径没有智能提示，那是因为你的工程没有配置路径别名
 比如 `@` = `/src`，那么你需要创建 *tsconfig.json* 或者 *jsconfig.json*
 并写入如下配置

```json
\\{
    "compilerOptions": \\{
        "baseUrl": ".",
        "paths": \\{
          "@/*": ["./src/*"]
        \\}
    \\}
\\}
```

最好下个插件 *Path Intellisense*，然后在配置文件 `setting.json` 写入

```json
"path-intellisense.mappings": \\{
    "@": "$\\{workspaceFolder\\}/src",
\\},
```



### JS 导入

当你需要导入模块时，仅需要输入前面几个字母，就有提示导入。
 **需要注意的是，你最好是具名导出，用默认导出它可能分析不了，因为没有名字**

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/88555020912c414bb49de10fdd0b409d~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=1387&h=436&s=51037&e=png&b=191815)



### TS 导入

强类型语言，则多一个修复选项，*VSCode* 按下 `ctrl + .`触发，*IDEA* 按下 `alt + enter`触发

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/35d413952d9f4bb3aae096b69b3a751b~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=438&h=320&s=18045&e=png&b=1d1c1b)



### 相对路径导入

很多人导入可能是手写 `import xxx from '@/...'`
 这样不仅容易错，还很麻烦，实际上可以用快捷键复制一下，如图

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/53392df1e8a545eeb0bd1ee9bf6fb90c~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=559&h=668&s=53444&e=png&b=1d1c1c)

如果你是 *window*，那么你的斜杠是反的，你需要配置一下`explorer.copyRelativePathSeparator`

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/705f08e6888a496ca9eb9a38f08d8640~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=587&h=538&s=54145&e=png&b=1d1c1b)

原文链接：https://juejin.cn/post/7333157879862149146







# VSCode深度配置 - settings.json

阅读6分钟

## 智能总结

本文介绍了 VSCode 的深度配置，包括安装注意事项（如镜像下载最新版）、各种实用配置（如打字流畅度、窗口美化、代码提示等）、不同项目的配置方式、代码自定义配色等，所有配置均放在文末 git 供读者自取。

看完本文，你将

- 让你的 VSCode 打字流畅度提升 114 倍
- 不同工程使用各自的项目配置、插件
- 更加美观的自定义窗口
- 更加智能代码提示、替换
- 更加清晰的代码块结构，能一目了然地看出嵌套关系
- 删掉那些标题党推荐的无用插件，使用 VSCode 自带的功能
- 自定义代码颜色，VSCode 主题

**所有配置，我都放在文末 git，大家自取即可**

## 现况概要

我每天逛各种社区，看到的关于 VSCode 的文章，99.999\\% 都是 **插件推荐**

而这些插件，说真的作用不大，很多都是 VSCode 内置的功能，而且同质化严重
他们也就知道那几个插件，没什么可说的

于是乎，我只能自己一点点的摸索 VSCode 最佳配置实践
今天有空就写一点吧

#### VSCode专栏系列：

[juejin.cn/column/7368…](https://juejin.cn/column/7368071052448022562)

## 安装

没错，这也要讲，不是我水，因为有些时候，你下载速度很慢
所以你要使用镜像下载

详细教程搜 **VSCode镜像下载**

注意，下载最新版的，因为我讲的配置，很多是新特性
目前我的版本是 `1.89.0`
像 VSCode 这种良心的应用，无脑装最新版即可

## 配置

第一步下载中文插件，这个大家应该都会，搜：**Chinese (Simplified) (简体中文)**

第二步，打开设置，快捷键 *Ctrl + ,*

第三步，打开 `setting.json`

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/19e9f64253114c089ccbde1ad60f3ad4~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=771&h=327&s=32307&e=png&b=1c1b19)

### 丝滑打字配置

这四行配置加入后，你马上会给我点赞
你将体会到如同潺潺流水，流过你手的感觉
这是全新的体验，是绝大多数编辑器不具备的体验

```json
\\{
    "editor.smoothScrolling": true,
    "editor.cursorBlinking": "expand",
    "editor.cursorSmoothCaretAnimation": "on",
    "workbench.list.smoothScrolling": true,
\\}
```

### 鼠标控制大小

直接上图，按下 *Ctrl + 鼠标滚轮*

![PixPin_2024-05-15_22-12-15.gif](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3027d25e4e2c49c1a0db79cdee04e985~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=571&h=428&s=319774&e=gif&f=29&b=181815)

```json
\\{
    "editor.mouseWheelZoom": true,
\\}
```

### 彩虹括号与作用域块线条提示

一堆插件推荐的文章，天天叫你装插件实现，明明自带的功能

```json
\\{
    "editor.guides.bracketPairs": true,
    "editor.bracketPairColorization.enabled": true,
\\}
```

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/cf040e417e444f269510b20850c5d41f~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=279&h=276&s=6394&e=png&b=171714)

### 更加智能的代码提示

```json
\\{
    // 控制活动代码段是否阻止快速建议
    "editor.suggest.snippetsPreventQuickSuggestions": false,
    // 除了 `Tab` 键以外， `Enter` 键是否同样可以接受建议
    // 这能减少“插入新行”和“接受建议”命令之间的歧义
    "editor.acceptSuggestionOnEnter": "smart",
    // 代码补全列表中，优先选择最近的建议
    "editor.suggestSelection": "recentlyUsedByPrefix",
\\}
```

有一种场景，比如你在写代码，写到一半，你突然想要代码补全
于是你调出建议，但是补全的代码会直接插入，不会覆盖你的输入
这时代码就会多一点内容出来，那么就报错了

这个也是可以配置的，下面是改为覆盖

```json
\\{
    "editor.suggest.insertMode": "replace",
\\}
```

### 自动补全括号、引号

```json
\\{
    "editor.autoClosingBrackets": "beforeWhitespace",
    "editor.autoClosingDelete": "always",
    "editor.autoClosingOvertype": "always",
    "editor.autoClosingQuotes": "beforeWhitespace",
\\}
```

### 关闭缩进猜测

如果你打开一个文件，他的缩进是 2，而你的配置是 4
那么你格式化时，他很可能不按你的配置来

```json
\\{
     // 关闭缩进猜测
    "editor.detectIndentation": false,
    "editor.tabSize": 4,
\\}
```

### 美化窗口

window 默认窗口如下，丑陋至极

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d8dbca3b53c54e71a9c8c959800ebbc3~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=675&h=442&s=52462&e=png&b=171714)

配置后使用 VSCode 自己的窗口

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6e094e428073461c881ad86419119108~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=776&h=424&s=44965&e=png&b=141312)

```json
\\{
    "window.dialogStyle": "custom",
\\}
```

### 自动换行和行高

设置了这个，就不用横向滚动了

```json
\\{
    "editor.wordWrap": "on",
    "editor.lineHeight": 1.5,
\\}
```

### 紧凑的文件夹模式

```json
\\{
    // 文件夹紧凑模式
    "explorer.compactFolders": true,
    "notebook.compactView": true,
\\}
```

设置后会把没用的东西折叠，利于啰嗦的 *Java* 项目

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3f7061e0117e4d96b19dd47112f44b84~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=465&h=358&s=21423&e=png&b=181818)

**还有一个 Tab栏 紧凑模式**

```json
\\{
    "window.density.editorTabHeight": "compact"
\\}
```

### 格式化自动删分号

无意义的分号，不加为妙。现代编程语言都可以不用分号

```json
\\{
    "javascript.format.semicolons": "remove",
    "typescript.format.semicolons": "remove",
\\}
```

### Typescript 语言设置中文

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/47f4bbe182264fb7a3d628572215ac2a~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=611&h=313&s=19630&e=png&b=1a1c1a)

```json
\\{
    "typescript.locale": "zh-CN",
\\}
```

### 枚举类型数值提示

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/07aef9731b7c44e0ba2fb4eb70f17ceb~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=186&h=128&s=2914&e=png&b=171714)

```json
\\{
    "typescript.inlayHints.enumMemberValues.enabled": true,
\\}
```

### JS 获得所有类型推导

如果你全开，那就满屏幕都是类型

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/193abd290627423589926800ad728a57~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=508&h=173&s=6063&e=png&b=171714)

在设置里搜 `inlayHints`即可，你自行选择
我的配置如下

```json
\\{
    // 类型提示
    "javascript.inlayHints.enumMemberValues.enabled": true,
    "javascript.inlayHints.functionLikeReturnTypes.enabled": false,
    "javascript.inlayHints.parameterNames.enabled": "none",
    "typescript.inlayHints.enumMemberValues.enabled": true,
    "typescript.preferences.preferTypeOnlyAutoImports": true,
    "typescript.updateImportsOnFileMove.enabled": "always",
    "typescript.preferences.includePackageJsonAutoImports": "on",
    "javascript.updateImportsOnFileMove.enabled": "always",
    "javascript.preferences.quoteStyle": "single",
    "typescript.preferences.quoteStyle": "single",
\\}
```

### TS 导入、重命名、补全自动更新相关引用

```json
\\{
    "typescript.preferences.preferTypeOnlyAutoImports": true,
    "typescript.preferences.includePackageJsonAutoImports": "on",
    "javascript.suggest.autoImports": true,
    "typescript.suggest.autoImports": true,
    "vue.updateImportsOnFileMove.enabled": true,
\\}
```

### Vue 自动补全 .value 和缺失属性提醒

```json
\\{
    "vue.inlayHints.missingProps": true,
    "vue.autoInsert.dotValue": true,
\\}
```

### 关闭开屏 VSCode 的亲切问候

```json
\\{
    "workbench.startupEditor": "none",
\\}
```

### 自动猜测文本编码

```json
\\{
    "files.autoGuessEncoding": true,
\\}
```

### 保存自动删除末尾空格

这个想开就开，我不开，因为影响 md 格式

```json
\\{
    "files.trimTrailingWhitespace": false,
\\}
```

### 搜索吸附目录

新版特性，你要更新噢

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7b4e48e676cb494ba83f1b96e2f263a4~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=405&h=330&s=27060&e=png&b=191919)

```json
\\{
     "search.searchEditor.singleClickBehaviour": "peekDefinition",
\\}
```

### 父级自动吸附置顶

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/be656f3e5e7442fa945f864cfc1df7b3~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=511&h=327&s=14851&e=png&b=171714)

```json
\\{
    "editor.stickyScroll.enabled": true,
\\}
```

### 终端代码补全

实验性配置

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6bb689b7057f41d2ac432d2b6be5c741~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=595&h=480&s=43807&e=png&b=1a1c1a)

```json
\\{
    "terminal.integrated.shellIntegration.suggestEnabled": true,
\\}
```

### 终端命令置顶

图我就不放了，就是吸顶

```json
\\{
    "terminal.integrated.stickyScroll.enabled": true
\\}
```

### 个人终端配置

> 看完再复制噢，这部分我没放到 git 里

注意 **terminal.integrated.defaultProfile.windows** 是配置你终端的路径
别乱写，否则你终端就用不了了

- **terminal.integrated.cursorBlinking** - 终端闪动光标
- **terminal.integrated.cursorWidth** - 光标宽度
- **terminal.integrated.rightClickBehavior** - 右键行为

我的终端里的美化效果（Git分支，历史记录...），是自己下载并且配置的，不属于 *VSCode* 的

```json
\\{
    // 终端配置
    "terminal.integrated.fontFamily": "BitstromWera Nerd Font Mono",
    "terminal.integrated.shellIntegration.suggestEnabled": true,
    "terminal.integrated.stickyScroll.enabled": true,
    "terminal.integrated.profiles.windows": \\{
        "PowerShell 7": \\{
            "path": "C:/Program Files/PowerShell/7/pwsh.exe"
        \\}
    \\},
    "terminal.integrated.defaultProfile.windows": "PowerShell 7",
    "terminal.integrated.cursorBlinking": true,
    "terminal.integrated.cursorWidth": 2,
    "terminal.integrated.cursorStyle": "line",
    "terminal.integrated.rightClickBehavior": "default",
    "terminal.integrated.gpuAcceleration": "on",
    "accessibility.signals.terminalCommandFailed": \\{
        "sound": "auto",
        "announcement": "auto"
    \\},
\\}
```

### index 替换成目录名

在打开很多文件时，能区分出是谁

```json
\\{
    // index 替换成 目录名
    "workbench.editor.customLabels.patterns": \\{
        "**/index.vue": "$\\{dirname\\}.vue",
        "**/index.js": "$\\{dirname\\}.js",
        "**/index.ts": "$\\{dirname\\}.ts",
        "**/index.jsx": "$\\{dirname\\}.jsx",
        "**/index.tsx": "$\\{dirname\\}.tsx"
    \\},
\\}
```

### 行内样式代码补全

比如你在写 style 字符串时，能有代码提示

```json
\\{
    // 行内样式代码补全
    "editor.quickSuggestions": \\{
        "other": true,
        "comments": true,
        "strings": true
    \\},
\\}
```

### 双击选中被截断字符

再也不用担心双击被下滑线截断了

```json
\\{
    "editor.wordSeparators": "`~!@\\%^&*()=+[\\{]\\}\\|;:'\",.<>/?（），。；：",
\\}
```

### 折行缩进策略和关闭右侧代码地图

关闭右侧代码地图大家自己选择，反正我觉得碍眼

```json
\\{
    "editor.minimap.enabled": false,
    "editor.foldingStrategy": "indentation",
\\}
```

### 关闭搜索中跟踪符号链接

提高搜索性能

```json
\\{
    "search.followSymlinks": false,
\\}
```

### 更新模式选择

我要手动的

```json
\\{
    "update.mode": "manual",
\\}
```

### 搜索排除目录

提高性能，需要重启生效

```json
\\{
    "search.exclude": \\{
        "**/node_modules": true,
        "**/pnpm-lock.yaml": true,
        "**/package-lock.json": true,
        "**/.DS_Store": true,
        "**/.git": true,
        "**/.gitignore": true,
        "**/.idea": true,
        "**/.svn": true,
        "**/.vscode": true,
        "**/build": true,
        "**/dist": true,
        "**/tmp": true,
        "**/yarn.lock": true
    \\},
\\}
```

### 文件关联

比如小程序中的 .wxss 这种文件，会把它作为css文件来处理
提供对应的 css 的语法提示 css 的格式化等
jsonc意思是能写注释的 JSON

```json
\\{
    "files.associations": \\{
        "*.wxss": "css",
        "*.wxml": "html",
        "*.svg": "html",
        "*.xml": "html",
        "*.wxs": "javascript",
        // json注释
        "*.cjson": "jsonc",
        "*.json": "jsonc"
    \\},
\\}
```

### window 相对路径复制使用 `/`

右键文件复制路径，当你导入东西时有用
默认 window 反斜杠

```json
\\{
    "explorer.copyRelativePathSeparator": "/",
\\}
```

## 不同项目使用不同配置

方式很多，我最推荐这个

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8c91041704b84b7f943ae0bb01025087~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=628&h=532&s=44965&e=png&b=181717)

## 代码自定义配色与全部配置

这个如果你有强烈需求，我建议你写插件
因为配置文件的颜色，在 VSCode 上，会时不时闪烁
非常影响体验，你必须输入文件才有效

------

**我自己写的主题插件**

Pretty Dark Theme

![image.png](https://p3-xtjj-sign.byteimg.com/tos-cn-i-73owjymdk6/270230aa165a41ffa790b3bf0fef8299~tplv-73owjymdk6-jj-mark-v1:0:0:0:0:5o6Y6YeR5oqA5pyv56S-5Yy6IEAg5a-F5pe256CB:q75.awebp?rk3s=f64ab15b&x-expires=1730952555&x-signature=CJyen2TU1d14RRAD\\%2BQ6QUXjrLKE\\%3D)

------

自定义配色的配置有很多，我放在上 git 上

上面的配置也有，我把个人用的配置删了
如果和你的配置冲突，自行检查

https://gitee.com/cjl2385/dig-for-gold/tree/master/VSCode

原文链接：https://juejin.cn/post/7369029201579343887



### VS Code优化settings.json，保证常用功能，使得编辑器不卡顿，高效。需要注释

以下是为优化 VS Code 性能设计的 `settings.json` 配置，附带详细注释说明每个配置项的作用：

```
\\{
    // ========== 核心性能优化 ==========
    // 禁用自动保存，减少频繁磁盘写入（若需自动保存可改为 "afterDelay"）
    "files.autoSave": "off",
    // 关闭未保存文件的预览模式，减少内存占用
    "workbench.editor.enablePreview": false,
    // 禁用文件缩略图渲染（适用于大文件项目）
    "explorer.decorations.badges": false,
    "explorer.decorations.colors": false,

    // ========== 界面渲染优化 ==========
    // 禁用动画效果提升响应速度
    "workbench.list.smoothScrolling": false,
    "window.titleBarStyle": "custom", // 使用轻量级标题栏
    // 禁用平滑滚动和光标动画
    "editor.smoothScrolling": false,
    "editor.cursorSmoothCaretAnimation": "off",

    // ========== 扩展功能控制 ==========
    // 禁用内置功能（按需启用）
    "git.enabled": true,          // Git基础功能保留
    "git.autorefresh": false,     // 禁用自动刷新状态
    "typescript.tsserver.log": "off", // 关闭TS服务器日志
    // 禁用实时错误检查（对低配设备有帮助）
    "javascript.validate.enable": false,
    "typescript.validate.enable": false,

    // ========== 搜索优化 ==========
    // 限制搜索文件大小和数量
    "search.maxResults": 20000,
    "search.followSymlinks": false,
    "search.useIgnoreFiles": true,

    // ========== 编辑器渲染优化 ==========
    // 禁用不必要的渲染效果
    "editor.hideCursorInOverviewRuler": true,
    "editor.minimap.enabled": false,    // 关闭缩略图
    "editor.renderLineHighlight": "none",
    // 关闭括号高亮匹配
    "editor.matchBrackets": "never",

    // ========== 内存控制 ==========
    // 配置TS/JS内存限制（单位MB）
    "typescript.tsserver.maxTsServerMemory": 4096,
    "javascript.tsserver.maxTsServerMemory": 4096,
    // 禁用大型文件特殊处理
    "files.maxMemoryForLargeFilesMB": 4096,

    // ========== 网络与更新 ==========
    // 禁用自动更新检查
    "update.mode": "none",
    // 关闭遥测数据收集
    "telemetry.telemetryLevel": "off",

    // ========== 高级优化 ==========
    // 启用实验性渲染优化（需VS Code 1.70+）
    "editor.experimental.asyncTokenization": true,
    "editor.experimental.useSandboxedRenderer": true,
    // 禁用工作区建议
    "extensions.ignoreRecommendations": true
\\}
```

### 使用建议：

1. **渐进式调整**：建议逐项启用/禁用配置，观察对工作流程的影响

2. 硬件加速：若使用独立显卡，可添加： 

   ```
   "disable-hardware-acceleration": false
   ```

3. 扩展管理：定期检查禁用非常用扩展，建议： 

   ```
   "extensions.autoCheckUpdates": false
   ```

4. 主题选择：使用纯色主题可提升渲染性能： 

   ```
   "workbench.colorTheme": "Default Dark Modern"
   ```

### 性能检测技巧：

1. 使用命令面板 `> Developer: Show Running Extensions` 监控扩展性能
2. 通过 `> Help: Process Explorer` 查看资源占用情况
3. 定期使用 `> Developer: Reload Window` 重启编辑器释放内存

根据实际硬件配置（特别是内存小于 8GB 的设备），建议适当降低内存限制数值。此配置在保持代码高亮、智能提示等核心功能的同时，最大限度降低了非必要资源消耗。



### setting.json中配置

个人：

```json
\\{
    // 工作台
    "workbench.colorTheme": "Default Light+", // 使用颜色主题
    "workbench.iconTheme": "vscode-icons", // 使用的文件图标主题
    "workbench.startupEditor": "none", // 在没有从上一会话中恢复出信息的情况下，控制启动时显示的编辑器
    "workbench.list.smoothScrolling": true, // 列表和树是否具有平滑滚动效果
    // 编辑器
    "editor.fontSize": 15, // 字体大小
    "editor.indentSize": "tabSize", // 用于缩进或 "tabSize" 的空格数
    "editor.tabSize": 2, // 一个制表符等于的空格数
    "editor.formatOnPaste": true, // 是否自动格式化粘贴的内容
    "editor.suggest.snippetsPreventQuickSuggestions": false, // 活动代码段是否阻止快速建议
    "editor.smoothScrolling": true, // 是否使用动画滚动
    "editor.cursorBlinking": "expand", // 光标的动画样式
    "editor.cursorSmoothCaretAnimation": "on", // 是否启用平滑插入动画
    "editor.guides.bracketPairs": true, // 启用括号对参考线
    "editor.bracketPairColorization.enabled": true, // 是否启用括号对着色
    // 不同语言
    "javascript.preferences.quoteStyle": "single", // 始终使用单引号
    "typescript.preferences.quoteStyle": "single", // 始终使用单引号
    "typescript.validate.enable": false, // 启用/禁用TypeScript验证
    // prettier插件
    "prettier.semi": false, // 是否加分号
    "prettier.singleQuote": true, // 是否用单引号
    // 其他
    "security.workspace.trust.untrustedFiles": "open", // 始终允许不受信任的文件引入受信任的工作区，而不显示提示
    "terminal.integrated.env.windows": \\{\\}, // 具有环境变量的对象，这些变量将添加到将由Windows上的终端使用的VS Code进程
    "diffEditor.hideUnchangedRegions.enabled": true, // 差异编辑器是否显示未更改的区域
    "[vue]": \\{
        // 指定vue文件的格式化工具
        "editor.defaultFormatter": "octref.vetur"
        // "editor.defaultFormatter": "esbenp.prettier-vscode"
    \\},
    "vetur.format.defaultFormatter.html": "js-beautify-html",
    "vetur.format.options.tabSize": 2,
    "vetur.format.options.useTabs": false,
    "vetur.validation.template": false,
    "vetur.format.defaultFormatterOptions": \\{
        "js-beautify-html": \\{
            // "wrap_line_length": 200, // 最多容纳多少个字符，开始换行
            "wrap_attributes": "force" // 属性换行，也可以force-aligned
            // "end_with_newline": false
        \\},
        "prettier": \\{
            "semi": false, // 是否加分号
            "singleQuote": true, // 是否用单引号
            "trailingComma": "none" // 是否末尾添加逗号
        \\}
    \\},
    "[html]": \\{
        "editor.defaultFormatter": "vscode.html-language-features"
        // "editor.defaultFormatter": "esbenp.prettier-vscode"
    \\},
    "[css]": \\{
        "editor.defaultFormatter": "vscode.css-language-features"
    \\},
    "[javascript]": \\{
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    \\},
    "[typescript]": \\{
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    \\},
    "[scss]": \\{
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    \\},
    "[json]": \\{
        "editor.defaultFormatter": "vscode.json-language-features"
    \\},
    "[jsonc]": \\{
        "editor.defaultFormatter": "vscode.json-language-features"
    \\},
    // 文件内容打开文件时是否自动检测editor.tabSize和editor.insertSpaces
    // "editor.detectIndentation": false,
    // 设置为"false"，表示要使用tab键插入tab而不是空格
    // "editor.insertSpaces": false,
    // 指定文件扩展名与语言模式的关联，使得编辑器能以正确的语法高亮和智能提示来处理文件
    "files.associations": \\{
        "*.cjson": "jsonc",
        "*.wxss": "css",
        "*.wxs": "javascript",
        "*.vue": "vue",
    \\},
    "search.followSymlinks": false, // 搜索时，符号链接指向的文件或目录不会被纳入搜索范围
    // 排除不需要监视的文件类型（显著降低文件系统负载）
    "files.watcherExclude": \\{
        "**/.git": true,
        "**/node_modules/**": true,
        "**/dist/**": true,
        "**/build/**": true,
        "**/*.log": true
    \\},
    // 较大的文件和不需要遍历的文件
    "files.exclude": \\{
        "**/node_modules": true,
        "**/*.log": true,
        "**/.hg": true,
        "**/CVS": true,
        "**/.DS_Store": true,
        "**/Thumbs.db": true
    \\},
    // 全文搜索和文件搜索中排除文件和文件夹
    "search.exclude": \\{
        "**/node_modules": true,
        "**/pnpm-lock.yaml": true,
        "**/package-lock.json": true,
        "**/.DS_Store": true,
        "**/.git": true,
        "**/.gitignore": true,
        "**/.idea": true,
        "**/.svn": true,
        "**/.vscode": true,
        "**/build": true,
        "**/dist": true,
        "**/tmp": true,
        "**/yarn.lock": true
    \\},
    "github.copilot.enable": \\{
        "*": true,
        "plaintext": false,
        "markdown": true,
        "javascript": true
    \\},
    "editor.inlineSuggest.enabled": true,
    "editor.inlineSuggest.showToolbar": "always",
    "git.confirmSync": false,
    "explorer.confirmDelete": false,
    "git.enableSmartCommit": true, // 控制是否在编辑器中自动显示内联建议
\\}
```

推荐：

```
\\{
  /*格式化文件对应插件：
   主要是两步，一步是用格式化插件格式化对应的文件；
   另一步让格式化后的代码能通过代码检验工具。
   prettyhtml格式化HTML；prettier格式化css/less/scss/postcss/ts；
   stylus-supremacy格式化stylus；
   vscode自带格式化插件格式化js；
   vetur格式化.vue文件；
   ESlint进行代码检验。
   */

  /*格式化思路和注意事项。
   注意格式化的代码能符合ESlint代码检验。
   1.用vetur设置默认格式化工具。格式化.vue文件
   2.用ESlint设置保存时修复ESlint错误的功能。
   3.用prettier格式化css；去除语法结尾的分号，使用单引号替换双引号。
   4.保存时自动格式化。
   */

  // 默认使用prettier格式化支持的文件
  "editor.defaultFormatter": "esbenp.prettier-vscode",

  "vetur.format.defaultFormatter.html": "prettyhtml",
  "vetur.format.defaultFormatter.css": "prettier",
  "vetur.format.defaultFormatter.postcss": "prettier",
  "vetur.format.defaultFormatter.scss": "prettier",
  "vetur.format.defaultFormatter.less": "prettier",
  "vetur.format.defaultFormatter.stylus": "stylus-supremacy",
  // "vetur.format.defaultFormatter.js": "prettier",
  "vetur.format.defaultFormatter.ts": "prettier",
  "vetur.format.defaultFormatter.sass": "sass-formatter",
  "open-in-browser.default": "Chrome",

  // 将vetur的js格式化工具指定为vscode自带的
  "vetur.format.defaultFormatter.js": "vscode-typescript",
  // 移除js语句的分号
  "javascript.format.semicolons": "remove",
  // 在函数名后面加上括号，类似这种形式 foo () \\{\\}
  "javascript.format.insertSpaceBeforeFunctionParenthesis": true,

  // eslint配置项，保存时自动修复错误。
  "editor.codeActionsOnSave": \\{
    "source.fixAll": true
  \\},

  // 指定 *.vue 文件的格式化工具为vetur
  "[vue]": \\{
    "editor.defaultFormatter": "octref.vetur"
  \\},
  // 指定 *.js 文件的格式化工具为vscode自带
  "[javascript]": \\{
    "editor.defaultFormatter": "vscode.typescript-language-features"
  \\},

  "vetur.format.defaultFormatterOptions": \\{
    "JS-beautify-HTML": \\{
      // JS-beautify-HTML的设置在这里
      "wrap_attributes": "force-aligned"
    \\},
    " prettyhtml": \\{
      "printWidth'": 100, // 每一行不超过100个字符
      "singleQuote": false, // 不用单引号
      "wrapAttributes": false,
      "sortAttributes": true
    \\},
    "prettier": \\{
      // 去掉代码结尾的分号
      "semi": false, //不加分号
      "singleQuote": true, //用单引号
      // #让prettier使用eslint的代码格式进行校验
      "eslintIntegration": true,
      "arrowParens": "always"
    \\}
  \\},

  // vscode默认启用了根据文件类型自动设置tabsize的选项
  "editor.detectIndentation": false,
  // 重新设定tabsize
  "editor.tabSize": 2,

  // 保存时自动格式化代码
  "editor.formatOnSave": true,

  //可选项。stylus的格式化配置以及sass格式化配置。
  // 格式化stylus, 需安装Manta's Stylus Supremacy插件
  "stylusSupremacy.insertBraces": false, // 是否插入大括号
  "stylusSupremacy.insertColons": false, // 是否插入冒号
  "stylusSupremacy.insertSemicolons": false, // 是否插入分号
  "stylusSupremacy.insertNewLineAroundImports": false, // import之后是否换行
  "stylusSupremacy.insertNewLineAroundBlocks": false,
  // 启用调试模式。
  "sass.format.debug": false,
  // 删除空格
  "sass.format.deleteEmptyRows": true,
  // 删除最后一个空格。
  "sass.format.deleteWhitespace": true,
  // 将 scss / css 转换为 sass。
  "sass.format.convert": true,
  // 如果 属性:值 为true,则始终设置为1.
  "sass.format.setPropertySpace": true,
  "git.confirmSync": false,
  "security.workspace.trust.untrustedFiles": "open"

  /*格式化插件：
   //vetur：代码高亮、emmet语法支持、语法错误校验检查、代码提醒、格式化vue。
   vetur集成了prettier，让.vue文件中不同的块使用不同的格式化方案，
   <template> 调用 html 格式化工具，
   <script> 调用 JavaScript 格式化工具，
   <style> 使用style格式化工具。
   
   //ESlint：新版的ESlint支持了对.vue文件的校验。
   
   //prettyhtml：为纯HTML模板等提供通用格式化的工具。
   //prettier：格式化工具，用于css/less/scss/postcss/ts
   //stylus-supremacy：用于格式化stylus文件的node.js模块。
   //js的格式化工具用vscode自带的。
   Prettier不支持在函数名后面加上括号。这点和ESlint冲突了。
   
   //EditorConfig：主要是用于让 vscode 支持.editorconfig 文件。
   .editorconfig 文件中的设置用于在基本代码库中维持一致的编码风格和设置，
   例如缩进样式、选项卡宽度、行尾字符以及编码等。
   EditorConfig 是让代码创建前保持规范，
   Prettier 是让代码保存后保持规范
   */
\\}
```

```
\\{
  /*格式化文件对应插件：
  主要是两步，一步是用格式化插件格式化对应的文件；
  另一步让格式化后的代码能通过代码检验工具。
  prettyhtml格式化HTML；prettier格式化css/less/scss/postcss/ts；
  stylus-supremacy格式化stylus；
  vscode自带格式化插件格式化js；
  vetur格式化.vue文件；
  ESlint进行代码检验。
  */
  /*格式化思路和注意事项。
  注意格式化的代码能符合ESlint代码检验。
  1.用vetur设置默认格式化工具。格式化.vue文件
  2.用ESlint设置保存时修复ESlint错误的功能。
  3.用prettier格式化css；去除语法结尾的分号，使用单引号替换双引号。
  4.保存时自动格式化。
  */
  // 默认使用prettier格式化支持的文件
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "vetur.format.defaultFormatter.html": "prettyhtml",
  "vetur.format.defaultFormatter.css": "prettier",
  "vetur.format.defaultFormatter.postcss": "prettier",
  "vetur.format.defaultFormatter.scss": "prettier",
  "vetur.format.defaultFormatter.less": "prettier",
  "vetur.format.defaultFormatter.stylus": "stylus-supremacy",
  // "vetur.format.defaultFormatter.js": "prettier",
  "vetur.format.defaultFormatter.ts": "prettier",
  "vetur.format.defaultFormatter.sass": "sass-formatter",
  "vetur.format.options.tabSize": 4,
  "open-in-browser.default": "Chrome",
  // 将vetur的js格式化工具指定为vscode自带的
  "vetur.format.defaultFormatter.js": "vscode-typescript",
  // 移除js语句的分号
  "javascript.format.semicolons": "remove",
  // 在函数名后面加上括号，类似这种形式 foo () \\{\\}
  // "javascript.format.insertSpaceBeforeFunctionParenthesis": true,
  // eslint配置项，保存时自动修复错误。
  "editor.codeActionsOnSave": \\{
    "source.fixAll": true
  \\},
  // 指定 *.vue 文件的格式化工具为vetur
  "[vue]": \\{
    "editor.defaultFormatter": "octref.vetur"
  \\},
  // 指定 *.js 文件的格式化工具为vscode自带
  "[javascript]": \\{
    "editor.defaultFormatter": "vscode.typescript-language-features"
  \\},
  "vetur.format.defaultFormatterOptions": \\{
    "js-beautify-html": \\{
      // "wrap_line_length": 200, // 最多容纳多少个字符，开始换行
      "wrap_attributes": "force" // 属性换行，也可以force-aligned
      // "end_with_newline": false
    \\},
    " prettyhtml": \\{
      "printWidth'": 100, // 每一行不超过100个字符
      "singleQuote": false, // 不用单引号
      "wrapAttributes": false,
      "sortAttributes": true
    \\},
    "prettier": \\{
      // 去掉代码结尾的分号
      "semi": false, //不加分号
      "singleQuote": true, //用单引号
      // #让prettier使用eslint的代码格式进行校验
      "eslintIntegration": true,
      "arrowParens": "always"
    \\}
  \\},
  // vscode默认启用了根据文件类型自动设置tabsize的选项
  "editor.detectIndentation": false,
  // 重新设定tabsize
  "editor.tabSize": 2,
  // 保存时自动格式化代码
  "editor.formatOnSave": false,
  //可选项。stylus的格式化配置以及sass格式化配置。
  // 格式化stylus, 需安装Manta's Stylus Supremacy插件
"stylusSupremacy.insertBraces": false, // 是否插入大括号
"stylusSupremacy.insertColons": false, // 是否插入冒号
"stylusSupremacy.insertSemicolons": false, // 是否插入分号
"stylusSupremacy.insertNewLineAroundImports": false, // import之后是否换行
"stylusSupremacy.insertNewLineAroundBlocks": false,
// 启用调试模式。
"sass.format.debug": false,
// 删除空格
"sass.format.deleteEmptyRows": true,
    // 删除最后一个空格。
    "sass.format.deleteWhitespace": true,
    // 将 scss / css 转换为 sass。
    "sass.format.convert": true,
    // 如果 属性:值 为true,则始终设置为1.
    "sass.format.setPropertySpace": true,
    "git.confirmSync": false,
    "security.workspace.trust.untrustedFiles": "open",
    "fileheader.Author": "caojianyong",
    "fileheader.LastModifiedBy": "caojianyong",
    "workbench.settings.applyToAllProfiles": [
        "fileheader.LastModifiedBy",
        "fileheader.Author"
    ]
    /*格式化插件：
   //vetur：代码高亮、emmet语法支持、语法错误校验检查、代码提醒、格式化vue。
   vetur集成了prettier，让.vue文件中不同的块使用不同的格式化方案，
   <template> 调用 html 格式化工具，
   <script> 调用 JavaScript 格式化工具，
   <style> 使用style格式化工具。

   //ESlint：新版的ESlint支持了对.vue文件的校验。

   //prettyhtml：为纯HTML模板等提供通用格式化的工具。
   //prettier：格式化工具，用于css/less/scss/postcss/ts
   //stylus-supremacy：用于格式化stylus文件的node.js模块。
   //js的格式化工具用vscode自带的。
   Prettier不支持在函数名后面加上括号。这点和ESlint冲突了。

   //EditorConfig：主要是用于让 vscode 支持.editorconfig 文件。
   .editorconfig 文件中的设置用于在基本代码库中维持一致的编码风格和设置，
   例如缩进样式、选项卡宽度、行尾字符以及编码等。
   EditorConfig 是让代码创建前保持规范，
   Prettier 是让代码保存后保持规范
   */
    // 在使用搜索功能时，将这些文件夹/文件排除在外
    // "search.exclude": \\{
    //   "**/node_modules": true,
    //   "**/bower_components": true,
    //   "**/target": true,
    //   "**/logs": true,
    // \\},
    // // 这些文件将不会显示在工作空间中
    // "files.exclude": \\{
    //   "**/.git": true,
    //   "**/.svn": true,
    //   "**/.hg": true,
    //   "**/CVS": true,
    //   "**/.DS_Store": true,
    //   "**/*.js": \\{
    //       "when": "$(basename).ts" //ts编译后生成的js文件将不会显示在工作空中
    //   \\},
    //   "**/node_modules": true
    // \\},
\\}
```

其他可以参考：

```
\\{
  "workbench.colorTheme": "Ysgrifennwr",
  "workbench.iconTheme": "vscode-icons",
  "search.followSymlinks": false,
  "prettier.tabWidth": 2,
  "editor.tabSize": 2,
  // 开启行数提示
  "editor.lineNumbers": "on",
  "editor.quickSuggestions": \\{
    // 开启自动显示建议
    "other": true,
    "comments": true,
    "strings": true
  \\},
  // 开启eslint
  "eslint.format.enable": true,
  // 每次保存自动格式化
  // "editor.formatOnSave": true,
  "editor.codeActionsOnSave": \\{
    "source.fixAll.eslint": true
  \\},
  // 格式化.vue中html
  "vetur.format.defaultFormatter.html": "js-beautify-html",
  // 让vue中的js按编辑器自带的ts格式进行格式化
  "vetur.format.defaultFormatter.js": "vscode-typescript",
  "vetur.format.defaultFormatterOptions": \\{
    "js-beautify-html": \\{
      "wrap_attributes": "force" //属性强制折行不一定对齐
    \\}
  \\},
  "eslint.validate": ["javascript", "vue", "html"],
  "[html]": \\{
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  \\},
  "[jsonc]": \\{
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  \\},
  "prettier.arrowParens": "avoid",
  "files.associations": \\{
  
  \\},
  "[javascript]": \\{
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  \\}
\\}
```

