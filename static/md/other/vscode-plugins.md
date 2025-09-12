---
title: VSCode插件
date: 2024-06-09 11:58:08
categories: 
- 其他
tags:
- 电脑
---

VS Code 代码编辑器支持多种编程语言，并提供了丰富的插件生态系统，可以帮助开发人员自定义编辑器以满足需求。

工欲善其事，必先利其器，下面推荐一些VSCode插件，可以帮助开发者提高代码质量、加速开发速度、简化常见任务，并且易于安装和使用。

## 必备

#### Chinese (Simplified) (简体中文) 

编辑器使用简体中文

### GitHub Copilot

开发者强大的AI编程助手

#### TONGYI Lingma

[通义灵码](https://tongyi.aliyun.com/lingma)，是一款基于通义大模型的智能编码辅助工具，提供行级/函数级实时续写、自然语言生成代码、单元测试生成、代码注释生成、代码解释、研发智能问答、异常报错排查等能力，并针对阿里云 SDK/API 的使用场景调优，为开发者带来高效、流畅的编码体验。 

#### 腾讯云代码助手 CodeBuddy

由腾讯云自研的一款开发编程提效辅助工具，基于腾讯混元 + DeepSeek 双轮模型驱动，构建对开发者友好，好用易用的代码助手，为开发者提供AI技术问答、Craft软件编码智能体、智能代码补全、单元测试、智能评审、代码修复等Agent智能体拓展能力，兼容 MCP 开放生态，并可支持团队知识库管理、自定义智能体与指令管理、多模型接入、企业账号集成等功能，辅助开发者提升编码效率和质量，助力研发团队提质增效。

### Vue-Official

Vue-Official 是 Vue 官方推荐的 VSCode 扩展，提供了 Vue 单文件组件中的 TypeScript 支持，还伴有一些其他非常棒的特性。

它取代了之前为 Vue 2 提供的官方 VS Code 扩展 Vetur。如果你之前已经安装了 Vetur，请确保在 Vue 3 的项目中禁用它。 以下是 Vue-Official 的一些特点： 

1. **支持 Vue 3**：提供 Vue 3 的语言支持，包括语法高亮、智能感知、代码片段等。 

2. **TypeScript 支持**：与 TypeScript 完美结合，提供类型检查和提示。 

3. **拖拽导入组件**：支持通过鼠标拖拽来导入组件，提高开发效率。 

4. **全面支持 Vue 3.4 新语法特性**：例如支持属性同名简写的写法。 如果你习惯使用英文界面，这个插件不是必须的。

   ```
   <!-- 原写法 -->
   <List :data="data" />
   <!-- 新写法 -->
   <List :data />
   ```

支持通过`鼠标拖拽`来导入组件，告别手动引入！

操作步骤：按住鼠标左键，把组件拖拽到想要引入的地方，VSCode 会提示按住 shift 放入编辑器中，此时我们按 shift 并放开鼠标左键，即可自动导入组件。

#### Vetur

Vue多功能集成插件，包括：语法高亮，智能提示，emmet，错误提示，格式化，自动补全，debugger。vscode官方钦定Vue插件，Vue开发者必备。

#### Vue VSCode Snippets

VUE代码自动补全插件

这个插件的目的是通过预定义一系列的快捷码，帮助开发者在编写Vue代码时，能够更快速、更高效地生成常见的模板代码结构。这些代码片段涵盖了Vue组件、指令、过滤器等各个方面，只需简单地输入几个缩写，就能自动填充相应的代码结构。

使用Vue VSCode Snippets不仅可以减少手动输入，降低出错的可能性，还能提升代码的一致性和可读性。这对于提高开发效率，优化工作流程具有显著的效果。

请注意，在使用Vue VSCode Snippets时，确保当前打开的文件是一个.vue文件，这样插件才能正常工作。此外，如果需要自定义模板，可以修改插件的配置文件。

总的来说，Vue VSCode Snippets是一个强大的工具，可以极大地提高Vue.js开发者的开发效率和代码质量。

#### Vue Peek

点击组件名跳到文件处

#### AutoScssStruct4Vue

根据 `vue`文件的模板`template`结构，自动生成对应的 `scss`文件 

#### SCSS Formatter

格式化SCSS

#### Sass (.sass only)

缩进的Sass语法高亮显示，自动完成和格式化

#### HTML CSS Support

在VScode中提示CSS相关扩展，这是写CSS代码快捷神器

#### CSS Peek

内联加载css文件，并在那里进行快速编辑

直接跳转到css文件或在新的编辑器中打开它

#### CSS Navigation

跳转到样式的定义，按住Ctrl键同时点击样式类的名称、或者光标在类的名称上按F12键即可跳转到样式的定义。

#### JavaScript (ES6) code snippets

这个插件乃是写ES6语法的最佳神器，拥有补全ES6语法和检查的功效。 

此扩展包括**「循环、条件、函数等常见 JavaScript 概念的片段，以及箭头函数、模板文字和解构等」** ES6 特定功能。使用这些片段可以为开发人员节省大量时间，因为它无需手动为日常任务键入代码。 

#### ESLint

统一JavaScript代码风格的工具，不包含css、html等。

ESLint可以与VS Code集成，通过安装ESLint插件，可以获得实时的代码检查和建议，能够在代码编辑过程中即时发现和修复潜在的问题。实时反馈和代码检查功能可维护高质量的代码并防止常见错误，帮助开发人员保证代码的质量和一致性。 

#### Prettier - Code formatter

Prettier是一款流行的代码格式化工具，用于自动规范和美化代码的风格，可应用于团队成员之间保持代码风格一致性。Prettier支持多种语言，包括JavaScript、TypeScript、CSS、HTML等。

使用Prettier可以节省开发人员在手动调整代码格式上的时间和精力，减少团队之间关于代码样式的争议。

如果你还想使用 ESLint，那么还有个 Prettier – Eslint 插件，你可不要错过咯！

### Stylelint

Stylelint是一个强大且先进的CSS代码检查器（linter），主要用于规避CSS代码中的错误，并确保编码风格的一致性。它的作用与ESLint相似，不仅提供了一系列的代码检查规则供开发者选择性地开启或关闭，还支持CLI工具，在命令行中调用Stylelint来检查项目中的CSS文件。

Stylelint支持自定义规则，并允许开发者根据团队规范或个人喜好定制检查规则。此外，Stylelint还提供了对Sass、Less、PostCSS等CSS衍生语法的检查功能，同时可以与Gulp或Webpack等构建工具集成。

对于Webpack用户，Stylelint Webpack Plugin是一个集成在Webpack构建流程中的插件，它通过实时反馈在每次编译时运行Stylelint，提供关于代码风格和潜在错误的警告。这个插件支持Stylelint的所有配置，允许根据团队规范或个人喜好定制检查规则，并能与其他Webpack插件协同工作，无需改变现有构建流程，轻松实现对样式文件的精细化管理。如果检测到严重错误，Stylelint Webpack Plugin还可以阻止Webpack构建过程，确保应用质量。

在使用Stylelint时，用户通常会在项目根目录下创建一个`.stylelintrc.js`的配置文件，里面的配置选项内容与ESLint中的配置基本相同。

#### Auto Rename Tag

自动重命名配对的HTML/XML标签。当我们在编写代码时，如果需要修改一个标签的名称，该插件可以自动更新对应闭合标签的名称，无需手动一个个修改，从而提高了编码效率和准确性。 

#### Auto Close Tag

该插件主要用于自动关闭HTML、XML和JSX标签。在编写代码时，只需输入起始标签，插件便会自动插入对应的结束标签，并将光标定位在两个标签之间，方便我们继续编写内容。 

#### Path Intellisense

自动提示文件路径，支持各种快速引入文件

#### Live Server

 `Live Server` 插件是一个用于前端开发的扩展，它的主要作用是提供一个本地开发服务器，以便实时预览和调试网页应用程序。**「其最大特点在于`热重载`，即开发者可实时预览代码效果。」** 

因为`Live Server`允许开发者在浏览器中实时预览您正在编辑的网页。每当保存`HTML、CSS、JavaScript`文件时，该插件会自动刷新浏览器，以便开发者可以立即看到页面的更改效果。 

#### open in browser

vscode不像IDE一样能够直接在浏览器中打开html，而该插件支持快捷键与鼠标右键快速在浏览器中打开html文件，支持自定义打开指定的浏览器，包括：Firefox，Chrome，Opera，IE以及Safari。

#### vscode-icons

`VSCode Icons` 插件是`Visual Studio Code`中的一个扩展，其主要作用是为文件和文件夹添加图标，以增强编辑器的可视化效果和可识别性。其可以为不同的文件或文件件添加不同的图标，进而确保项目结构清晰，项目结构易于理解。 

#### Error Lens

Error Lens插件提供在编辑器中直观和即时显示错误和警告的功能。该插件通过在代码行上方或旁边添加标记或提示来突出显示代码中的错误、警告和其他问题。它能够帮助开发人员快速发现和解决问题，提高代码质量和开发效率。

#### GitLens — Git supercharged

安装后重启，然后将鼠标单击放在被修改的那一处，  鼠标后面和编辑器右下角第一个位置，这两处都会有修改人的名字和时间。 

GitLens插件提供了深入了解代码历史和作者的功能。它可以显示每行代码的Git提交信息，并提供代码镜头功能，让开发人员快速浏览和理解代码的演进历史。

此外，此插件还具有快速导航到文件的最后一次修改、查看指定行的Git提交历史以及比较不同版本之间的更改等功能。

GitLens能够提高开发人员的协作效率和故障排除能力。

#### Image preview

Image preview是一个支持实时预览图片的插件，该插件支持各种常见的图像格式，如JPG、JPEG、PNG、BMP、GIF和SVG等。

当你的鼠标"hover"在有图像路径的代码行上，该插件就会显示一个预览窗口，直接显示图像。

可以在引入图片左侧导航条显示图像预览。

#### Md Editor

md编辑器，本扩展支持预览和编辑markdown格式的文件，基本接近 Typora 的编辑体验。

- 支持即时渲染、分屏预览和所见即所得三种不同编辑模式
- 支持暗黑模式和明亮模式
- 支持粘贴图片并自动保存到当前路径的images文件夹中







## 其他

#### ChatGPT - 中文版

一个ChatGPT4.0的插件支持中文版免翻墙

#### Baidu Comate

由文心大模型 `ERNIE-Code` 提供技术支持，通过对百度多年积累的非涉密代码数据和 `GitHub` 头部公开代码数据进行训练，为您自动生成完整的、且更符合实际研发场景的代码行或整个代码块，帮助每一位开发者轻松完成研发任务。

#### SFTP

项目新建工作区，/项目目录/.vscode/下新建sftp.json

```
\\{
    "name": "qw",
    "host": "192.168.1.22",
    "protocol": "sftp",
    "port": 22,
    "username": "root",
    "password": "123",
    "remotePath": "/var/www/website/",
    "uploadOnSave": true,
    "useTempFile": false,
    "openSsh": false
\\}
```

在文件列表中就可以右击使用：远程到本地或者本地到远程



## 其他待发掘

1. background
2. Color info
3. glTF Tools
4. Import Cost
5. stylus
6. Syncing
7. Ysgrifennwr Theme

#### Vue Language Features (Volar)

vue3必备，该插件可以让`Vue`代码获得漂亮的语法高亮显示、错误检查和代码格式化。并且它还会对很多`Vue` 指令和事件处理程序，进行提示和建议。 

#### Vue 3 Support - All In One

vue语法高亮，大部分js代码补全和片段生成。

#### Code Spell Checker

该插件会帮我们检查编写代码过程中的英文单词拼写错误。例如，在快速的开发过程中，我们可能会因为打字速度过快而造成一些简单的单词拼写错误，如将"history"误写为"histor"，或者将"active"误写为"actived"等。 

不过对于老项目，开了这个一片报红就比较烦

#### wxml

小程序代码格式化及高亮组件

#### Visual Studio IntelliCode

此插件利用机器学习技术来提供智能的代码建议和自动补全功能，提高生产力。可获得与开发人员的编码风格相符的智能建议，根据代码历史和上下文，优先推荐最可能使用的代码片段和函数。

通过使用此插件，开发人员可以更快地编写代码，减少打字错误，并且在编码过程中接收到更准确和有用的建议。这提高了开发效率，减少了调试和修复错误的时间。

#### Tabnine

`Tabnine` 是一款强大的智能代码补全插件，可在`Visual Studio Code（VSCode）`中使用。其主要作用是提供高效和智能的代码建议，以加速代码编写和提高代码质量。具体来看，`Tabnine` 主要有如下功能：

1. **「智能代码建议」**：`Tabnine`使用机器学习和自然语言处理技术，分析您的代码并为您提供高质量的代码建议。这不仅包括常见的变量、函数和类名，还包括上下文感知的建议，可大大加速编码过程。
2. **「多语言支持」**：`Tabnine`支持多种编程语言，包括但不限于 `JavaScript、Python、Java、C++、Go`等。这使得它适用于不同类型的项目和开发任务。
3. **「实时建议」**：插件在您键入代码时实时提供建议，让您不必在每次需要时手动查找文档或库。这有助于减少拼写错误和代码语法问题。

#### JSDoc

这个工具真的很有趣！你不再需要手动添加一些虚拟的参数，比如参数、返回值、描述等，并将它们从虚拟状态更新为实际参数。现在，你只需选择函数定义，按下（command + Shift + p）打开命令面板（Mac），然后选择“添加JSDoc注释”，一个带有所选参数的注释部分将自动添加。

这个功能真的很酷，可以帮助我们快速生成JSDoc注释，提高代码的可读性和可维护性。通过这个注释生成器，你可以轻松地为函数添加必要的文档注释，包括参数、返回值、描述等。这样，其他开发人员就能更好地理解和使用你的代码了。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_gif/S8yWrB610Tg55w03IF4F3Mev5iatUdj3QYpP756wyZxS4MNjXaSpqX7qNUgkdbfC9n0biaicvB5CibEricXLTllEFXQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1&wx_co=1)

#### any-rule

any-rule一个正则库，大部分正则都可以从这里面找到。

#### CSS Triggers

这个插件可以帮助我们更智能地编写代码，并提供有关CSS属性的布局、绘制和组合的更多信息。

该扩展为CSS属性添加内联修饰来指示它们的成本。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/S8yWrB610Tg55w03IF4F3Mev5iatUdj3Q64xZKt4c4soeNiajL1NeqpAEHVzScdXfbV5B2rSykgpceTiaQPTEWn1Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

同时，我们还可以找到示例，了解在编写这些属性时通过改变给定CSS属性而触发的不同变化。这些变化因浏览器引擎而异，包括Blink、Gecko、WebKit、EdgeHTML。通过这个插件，我们可以更好地了解和优化CSS代码。

#### Compareit

这个扩展帮助我们比较两个文件，你可以从当前项目和计算机上的其他目录选择文件，甚至可以从剪贴板中选择文件进行比较。使用这个扩展，就不再需要其他在线文本比较工具或离线许可软件了。它提供了便捷的文件比较功能，让我们能够轻松地对比文件内容，提高工作效率。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_gif/S8yWrB610Tg55w03IF4F3Mev5iatUdj3QiczaMzuxwsPLLaWiaNLicN7QlujKAX9icLtL9xgXLpdiaib5jJmBpQpxxeicQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1&wx_co=1)

#### Live Share

Live Share提供实时协作编程的能力，使多个开发人员可以在同一项目中实时共享代码、编辑和调试。适用于远程团队、教育和代码协作等场景，让开发人员可以更紧密、更实时地协同工作。

#### Code Runner

Code Runner插件主要就是可以快速运⾏调试代码，⽆需配置繁杂的环境，直接通过此插件就可以直接运行对应语言的代码，非常适合学习或测试各种开发语言。

#### Console Ninja

Console Ninja插件，很好用的一个插件，可以直接在Vscode内部就看到log的东西。

但是有一点不好的就是，很多时候都会失效，这个具体原因也不是很清楚。

#### SonarLint

SonarLint可以集成到VS Code中，是一个静态代码分析工具，实时分析和检测代码质量问题，提供保持清洁和无错误代码的建议。通过自动化的代码质量检查，提高代码可维护性和可靠性。

#### Pieces

通过代码片段和模板提高生产力，加快开发速度，减少重复的编码任务。访问可重用代码片段库，并自定义自己的代码片段，实现快速开发。

#### Better Comments

Better Comments插件旨在提供更丰富和可视化的代码注释功能。通过添加不同的注释样式来改进代码文档和协作，以提高代码的可读性和沟通效果；利用有信息量的注释增强代码可读性和沟通能力，有助于改善团队协作和代码维护的效率。

#### Git History

Git History插件提供可视化的界面，用于查看和浏览 Git 仓库的历史记录。使用 Git History，开发人员可以轻松查看提交历史、分支、标签和合并请求等信息，以图形化的方式展示了提交记录的时间轴，并显示每个提交的详细信息，如作者、提交消息、修改的文件等。

#### Git Graph

 `Git Graph`插件用于可视化查看存储库的 `Git`操作，并从图形中轻松执行`Git`操作。类似于`SOurceTree`的可视化版本控制插件，可以更新、提交代码，查看提交记录，审视代码。 

#### Material Icon Theme

此插件为文件和文件夹图标提供美观和一致的材质设计风格。使用Material Design风格的图标美化文件资源管理器，更容易导航和识别不同文件类型。通过视觉上吸引人的图标，定制开发人员的工作区，增强文件组织能力。

#### DotENV

DotENV在编辑.env文件时添加了便捷的语法高亮显示功能

#### Polacode

Polacode可以让将代码片段生成为优美的图像。很适合分享代码至社交媒体，写博客或者展示你的代码。

#### Markdown Preview Github Styling

`Markdown Preview Github Styling` 的作用是改善和优化`Markdown`预览功能，使得开发者可以在`VsCode` 中实时预览`.md`文件的最终效果。除此外，其还具有如下特点：

1. `预览实时更新`：插件允许您在 `VSCode` 中编写`Markdown`文档，并实时预览渲染效果。每当您对文档进行更改并保存时，预览面板会自动更新，以便您可以立即查看您的编辑效果。
2. 提高可读性：通过应用`GitHub` 风格的样式，该插件可以使 `Markdown` 文档更易于阅读，特别是对于那些已经熟悉 `GitHub`的用户。这对于编写技术文档、文档说明、`README` 文件等非常有帮助。
3. 可配置性：插件允许您根据需要进行一些自定义配置，以适应不同的渲染需求。您可以根据自己的偏好设置不同的预览样式。

总之，`Markdown Preview Github Styling` 插件通过在`VSCode`中提供`GitHub`风格的 `Markdown`预览，提高了`Markdown`编辑和协作的效率。

#### TODO Highlight

`TODO Highlight`插件是一个用于帮助开发人员识别和管理代码中的待办事项的工具。该插件的主要作用是提供代码中注释中包含的待办事项的可视化标记，以便开发者更容易定位、跟踪和处理这些任务。

当使用`todo`或`fixme`标签后，可按下快捷键`f1`，然后选择`all`或者`todo`即可查看当前项目中声明的标签信息。

#### Todo Tree

很多人在处理问题时都有自己的方式，在代码中加入某种形式的注释，并承诺自己会回来重新审视这段代码。然而，实际上很少有人能够真正回来重新审视这些注释，结果我们经常发现这些被遗忘的代码片段。

为了解决这个问题，有一个插件可以帮助我们以不同的样式在注释部分编写ToDo，并且可以方便地在代码库中找到所有相同的ToDo。这样一来，就能更好地管理和跟踪我们的开发计划了。

Todo Tree是一款非常实用的VS Code插件，它可以帮助用户快速搜索工作空间中的特定注释标签，如TODO和FIXME等，并以树状视图的形式将这些信息显示在活动栏中。 

 ![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/S8yWrB610Tg55w03IF4F3Mev5iatUdj3QibIIg0Wic9ItXTfTvcFJVCAmKEbR1ofzPR48peXHZaAjEhq2r9ZLMicEg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

#### REST Client

这个工具是在VS Code中使用`curl`命令的快捷方式和现成解决方案。支持测试Rest API，包括任何Get/Post/Put/Delete（CRUD）操作，带有参数和请求头。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_gif/S8yWrB610Tg55w03IF4F3Mev5iatUdj3Q26RE1lXckJlkYQnWiboBoD30edrqJq8W0d8PS3sNOBhg1KoWqnyfKSQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1&wx_co=1)

#### 书签

当你处理大文件并且需要在文件中不断搜索代码片段时，这个插件非常有帮助。它可以帮助我们在文件中快速跳转到另一个位置，节省宝贵的时间。你可以在文件中设置书签，并通过简单的操作在书签之间切换。此外，还可以在左侧菜单中查看书签列表，方便地管理和导航到不同的书签位置。使用这个插件，我们能更高效地浏览和编辑大文件，提高工作效率。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_gif/S8yWrB610Tg55w03IF4F3Mev5iatUdj3QlvEicaX3WRv0yGp9JUhanvyiaLGldbW1gXnWdFSS7NgQPGZQf2B6ly3Q/640?wx_fmt=gif&wxfrom=5&wx_lazy=1&wx_co=1)

#### Docker

在VS Code中，Docker插件用于与Docker进行集成和管理容器化应用程序。通过Docker集成，简化容器化应用程序的开发，便于管理和部署容器化环境。可保证在VS Code工作区内无缝构建、运行和管理容器。

#### Remote — SSH

Remote - SSH插件提供通过 SSH 协议连接到远程服务器进行开发的功能。通过SSH连接到远程服务器，开发人员可直接在远程文件上工作，实现无缝开发。在远程服务器上开发和调试代码，无需进行本地设置。 



### 图标	插件	作用

​	Auto Import	在j\ts文件中，直接使用外部依赖包的变量名，此时，会自动写入导入语句
​	Bracket Pair Colorizer2	VS Code 已经内置
​	Chinese (Simplified) (简体中文)	汉化
​	Code Spell Checker	适用于代码和文档的基本拼写检查器。此拼写检查器的目标是帮助捕获常见的拼写错误，同时保持较低的误报数量。
​	Document This	一个可视化工作室代码扩展，可为类型脚本和脚本文件自动生成详细的 JSDoc 注释。
​	Epub Reader	支持在vscode中阅读epub电子书.
​	GitLens — Git supercharged	可视化操作git ，安装后，在左侧栏中 有按钮
​	Git Graph 提交记录线，更形象化	可视化操作git ，安装后，会在左下角状态栏中有Git Graph按钮，点击即可调出操作UI
​	Import Cost	在编辑器中以内联方式显示导入的包的大小
​	JavaScript (ES6) code snippets	包含用于 VS 代码编辑器的 ES6 语法的 JavaScript 代码段
​	Live Server	在html文件中，右击，选择go live server,即可， 它将启用实时更改，而无需保存文件。
​	Live Share	实时共享，可以与他人实时协作编辑和调试试
​	Markdown All in One	Markdown所需的一切（键盘快捷键，目录，自动预览等）
​	Markdown Preview Enhanced	Markdown预览
​	node-snippets	提供一些很棒的NodeJS片段
​	npm Intellisense	用于在导入语句中，自动完成 npm 模块名的联想
​	Path Intellisense	在html标签中,文件路径，自动联想下路径下的目录和文件名
​	Path Autocomplete	es6导入引来文件书写时，自动联想路径下的文件和目录
​	Tabnine AITabnine AI	通过 AI 代码块联想,更快地编写代码
​	Prettier - Code formatter	格式化代码
​	Project Manager	生成各个项目目录，可以轻松访问项目，无论它们位于何处
​	Settings Sync	把VSCode设置、配置数据同步到github，方便多台设备上的VSCode的配置实时同步
​	SVG	预览SVG图片
​	vscode-pdf	查看pdf文件
​	Vue 3 Snippets	基于最新的 Vue 2 及 Vue 3 的 API 添加了 代码片段
​	Vue Language Features (Volar)	使编辑器识别vue3语法
​	WakaTime	用于统计编程活动中自动生成的指标、见解和时间跟踪。
​	Bookmarks	它可以帮助您在代码中导航，轻松快速地在重要位置之间移动
​	CSS Peek	它可以帮助您预览CSS样式class定义的内容，便于修改样式
​	IntelliSense for CSS class names in HTML	它可以帮助您在html联想已声明的class样式名
​	Excel Viewer	预览 Excel文件



### vscode怎么完全卸载之前安装的公有云版本通义灵码

解决方案：之前安装过公有云版本灵码，除了卸载原有的灵码，还需看下本地~/.lingma/bin目录下的文件是否清空。如下图，2.0.5这个文件为公有云版本的版本号，还需要把2.0.5这个文件删掉。Windows系统这个目录在哪？ 

以下是针对Windows系统完全卸载公有云版通义灵码及残留文件的步骤指南：

---

#### **步骤 1：卸载通义灵码程序**
1. 打开 **控制面板** > **程序和功能**。
2. 在程序列表中找到 **通义灵码** 或 **Lingma**，右键选择 **卸载**。
3. 按照提示完成卸载流程。

---

#### **步骤 2：删除用户目录下的残留文件**
1. 打开文件资源管理器，输入以下路径（替换 `<用户名>` 为你的实际用户名）：  
   ```shell
   C:\Users\<用户名>\.lingma\bin
   如
   C:\Users\12472\.lingma\bin
   C:\Users\12472\AppData\Local\.lingma
   ```
   - 如果提示路径不存在，需开启 **显示隐藏的文件和文件夹**：  
     - 点击资源管理器顶部 **查看** > **显示** > 勾选 **隐藏的项目**。
2. 删除 `.lingma\bin` 目录下的所有文件（如 `2.0.5` 版本文件夹）。

---

#### **步骤 3：清理VS Code扩展残留**
1. **卸载扩展**：
   - 打开VS Code，进入扩展面板（`Ctrl+Shift+X`）。
   - 搜索 **通义灵码**，右键选择 **卸载**。
2. **手动删除扩展文件**：
   - 关闭VS Code，打开路径：  
     ```shell
     C:\Users\<用户名>\.vscode\extensions
     ```
   - 删除名称包含 `lingma` 或 `tongyi` 的文件夹（如 `alibaba-lingma-*`）。

---

#### **步骤 4：清理临时文件（可选）**
1. 按 `Win + R`，输入 `\\%temp\\%` 并回车，删除与 `lingma` 相关的临时文件。
2. 清空回收站以彻底移除文件。

---

#### **步骤 5：重启系统**
完成上述操作后重启电脑，确保残留进程彻底关闭。

---

#### **验证是否卸载干净**
1. 检查上述目录是否已无残留文件。
2. 重新打开VS Code，确认扩展列表中没有通义灵码。

---

通过以上步骤，可彻底移除公有云版通义灵码及其残留文件。若后续安装新版，建议从官方渠道获取最新安装包以确保兼容性。

/user/xx和/user/xx/appdata/local都放一下
.lingma目录删掉之后，结束灵码进程，重启ide看看