---
title: Git
date: 2020-08-31 22:30:10
categories: 
- 前端知识
tags:
- Git
---

### Git是什么

Git是目前世界上最先进的分布式版本控制系统（没有之一）

#### 版本控制

版本控制（Version Control）的作用是追踪文件的变化。为什么需要版本控制？简单说，就是当你出错了，可以很容易地回到没出错时的状态。

#### 为什么使用GIT

Git有很多优势，其中之一就是远程操作非常简便，以及速度快。



### 删除分支

为了帮助您有效管理Git分支，以下是删除分支的规范化操作指南：

一、删除本地和远程分支（两者均存在）

1. 切换到非目标分支

```bash
git checkout main  # 切换到主分支或其他安全分支
```

2. 删除本地分支

```bash
git branch -d feature/test1  # 安全删除已合并分支
git branch -D feature/test1  # 强制删除未合并分支
```

3. 删除远程分支

```bash
git push origin --delete feature/test1  # 标准删除命令
# 或等效简写
git push origin :feature/test1
```

**常用示例：**

```
git branch -D dc-uat
git push origin -d dc-uat
```

二、清理远程已删除分支的本地缓存

1. 查看远程分支状态

```bash
git remote show origin  # 显示带(stale)标记的过期分支
```

2. 同步远程分支信息

```bash
git fetch --prune  # 推荐方式：获取更新同时清理缓存
# 或单独清理
git remote prune origin
```

三、操作验证

```bash
# 查看本地分支
git branch

# 查看所有远程分支（实时状态）
git ls-remote --heads origin

# 查看本地缓存的远程分支
git branch -a
```

四、注意事项

1. 分支删除不可逆，建议先创建tag备份重要代码
2. 团队协作分支删除前需确认所有成员已完成同步
3. 推荐使用图形化工具查看分支拓扑：

```bash
git log --oneline --graph --all
```

五、高效操作技巧

1. 组合命令（删除本地+远程）

```bash
git branch -d feature/test1 && git push origin :feature/test1
```

2. 配置自动清理（全局生效）

```bash
git config --global fetch.prune true  # 每次fetch自动清理过期分支
```

通过以上标准化流程，您可以安全高效地管理Git分支生命周期。当遇到分支删除冲突时，建议优先使用`git fetch --all -p`更新所有远程引用后再进行操作。



### 冲突解决

自己基于主分支的开发分支，gitlab面板合并到测试分支时和别人代码有冲突，怎么处理（我的开发分支不能拉取测试分支，我的分支就不干净了，到时候上线时把别人代码也上线了）

在使用GitLab进行合并时遇到冲突，尤其是你在开发分支（比如feature分支）合并到测试分支（比如test分支）时发生冲突，解决方案如下：

#### 1. 理解问题
- 你不能直接将测试分支拉到你的开发分支，这会导致你的开发分支变得不干净（包含其他人的提交）。
- 你希望将你的开发分支合并到测试分支，确保冲突解决后，测试分支保持清晰，避免把别人的代码带到上线环节。

#### 2. 正确的操作流程

##### 步骤一：切换到测试分支（本地）
```bash
git checkout test
```

##### 步骤二：拉取最新的测试分支代码（确保你本地的测试分支是最新的）
```bash
git pull origin test
```

##### 步骤三：合并你的开发分支到测试分支
如果你的开发分支是`feature-branch`，执行：
```bash
git merge feature-branch
```
此时，如果出现冲突，Git会提示你哪些文件有冲突。

##### 步骤四：解决冲突
1. 打开冲突的文件，手动编辑，保留你想要的代码，删除冲突标记（<<<<<<<、=======、>>>>>>>）。
2. 一旦解决完所有冲突，标记文件为已解决：
```bash
git add <冲突文件>
```

##### 步骤五：完成合并
```bash
git commit
```
（如果冲突解决后没有自动提交的话）

##### 步骤六：推送到远程测试分支

```bash
git push origin test
```

#### 3. 小技巧和建议
- **不要直接从测试分支拉到你的开发分支**，因为这样会让你的开发分支变得不干净，也容易引入其他人的变更到你的开发分支，影响后续开发。
- 建议经常从`test`分支拉取最新改动到你的开发分支，保持同步：
  ```bash
  git checkout feature-branch
  git pull origin test
  ```
  然后解决冲突，提交后再推送到你的远程开发分支。

#### 4. 最后注意
- 在合并前确保你理解冲突的内容，不要盲目接受全部冲突解决方案。
- **上线前**，一般会由CI/CD流程（自动测试）验证，确保合并后的代码不会引入其他问题。

如果你愿意，也可以考虑用【rebase】方式整理提交历史，但操作相对复杂，推荐在熟悉后使用。

---

如果还有具体冲突的文件内容或操作疑问，可发我详细信息，我可以帮你指导如何解决！







### 使用

#### 安装GIT软件

推荐使用Github的客户端 [windows 版下载](https://windows.github.com/)。

####  常用命令

* 检出仓库 `git clone /path/to/repository`
* 获取更新，并与本地代码进行合并 `git pull`
* 将文件添加到版本控制系统 `git add filePath`
  * `git add .` 添加当前目录下的所有文件
  * `git add -A` 添加当前目录下的所有文件，如有重命名的文件，会对重命名前的文件进行删除。`git add .`不会
* 提交改动代码 `git commit -m filePath "注释"` 注意:注释是必填的
* 提交所有改动代码 `git commit -am "注释"`
* 查看当前项目代码的状态 `git status`
* 将改动推送到服务器 `git push`
* 将文件的内容替换成上次提交时候的内容 `git checkout filePath`
* 将还没提交的内容保存起来，所有的文件内容变成上次提交时的样子 `git stash`
* 回复上次`git stash`的内容，并与当前代码进行合并 `git stash pop`
* 分支操作
  * 切换到某分支 `git checkout branchName`
  * 创建并切换到某分支 `git checkout -b branchName`
  * 将某分支的改动推送到服务器 `git push origin branchName`
* 发生冲突时，文件中会用 `>>>>` 和 `<<<<` 来标明冲突的地方。合并好后，`git add 这个冲突的文件`。 然后再commit,push



### 怎么提交代码

在命令行提交代码到Git仓库，你需要遵循几个基本步骤。以下是提交代码的基本命令流程：

1. **检查当前状态**：
   首先，使用 `git status` 命令查看哪些文件已被修改或者尚未被Git跟踪。

2. **添加文件**：
   使用 `git add` 命令将你想要提交的文件添加到暂存区。你可以添加单个文件，如 `git add myfile.txt`，也可以添加所有修改过的文件，使用 `git add .`。

3. **提交更改**：
   使用 `git commit` 命令提交暂存区的更改。你应该附上一条有意义的提交信息来描述这次提交做了什么变动。例如：`git commit -m "添加了新功能和修复了小错误"`。

4. **推送到远程仓库**：
   如果你正在与他人协作或者想在云端保存代码，还需要将提交推送到远程仓库。首先确认你的远程仓库名称（通常是 `origin`），然后使用 `git push` 命令。常见的形式是 `git push origin 分支名`，比如 `git push origin main` 或 `git push origin develop`，具体取决于你要推送的分支。

注意：如果你的仓库启用了 `commitlint`（如你在提问中提到的），确保你的提交信息遵循项目的提交规范，否则在执行 `git commit` 时可能会遇到错误提示，需要按照规范调整提交信息后重新提交。

此外，如果你在提交时遇到了诸如权限问题、身份验证失败等问题，可能需要配置SSH密钥或使用HTTPS凭据进行身份验证。



### .gitignore

如果项目想让某些文件的版本不受Git管理，可以在项目的根路径创建个文件，名称为 `.gitignore`。内容为不受Git管理的文件名。 如

```
.idea
Desktop.ini
*.log
# 开头表示注释，如果相匹配 #，可以在前面加一个反斜杠，即 \#
```

一些`.gitignore`的模板 https://github.com/github/gitignore

[用对 gitignore](http://www.barretlee.com/blog/2015/09/06/set-gitignore-after-add-file/)。[更多gitignore规则](https://git-scm.com/docs/gitignore)



### git在一个分支开发一半，不想产生提交记录，怎么暂存，切换到别的分支

当你在一个 Git 分支上开发但还没有准备好提交你的更改，并且你想要切换到另一个分支进行其他工作时，你可以使用 `git stash` 命令来暂存当前的工作。这将保存你未完成的更改，允许你干净地切换分支。

以下是具体步骤：

1. 确保你在想要暂存更改的分支上。
2. 使用以下命令来暂存更改：
   ```bash
   git stash save "描述信息"
   ```
   或者更简洁的方式（Git 1.8.4 及以上版本）：
   ```bash
   git stash push -m "描述信息"
   ```

   描述信息是可选的，但它有助于你记住这些更改的目的或内容。

3. 暂存后，你可以查看所有暂存的状态：
   ```bash
   git stash list
   ```

4. 现在你可以切换到其他的分支：
   ```bash
   git checkout 其他分支名
   ```
   或者如果你使用的是 Git 2.23.0 或更新版本，推荐使用：
   ```bash
   git switch 其他分支名
   ```

当你回到原来的分支并准备恢复暂存的工作时，可以使用以下命令：

```bash
git stash pop
```

这会将最近一次暂存的更改应用回工作目录，并从 stash 列表中移除它。如果有冲突，你需要解决这些冲突。如果你只是想查看或应用某个特定的 stash 而不移除它，你可以使用 `git stash apply` 加上 stash 的名称（例如 `stash@\\{0\\}`）。

请记得，`git stash` 是一个本地操作，stash 中的内容不会被推送到远程仓库。因此，它们只存在于你自己的计算机上。

#### 在 TortoiseGit 汉化版中

您可以使用以下步骤在不产生提交记录的情况下暂存当前的工作，并切换到其他分支：

1.暂存当前工作：


2.在您正在开发的分支上，右键点击工作目录（文件夹）并选择 TortoiseGit -&gt; Stash Save（中文界面中可能显示为“存储变更”）。
3.在弹出的窗口中，您可以为当前的暂存操作输入描述（如果需要），然后点击“确定”。
4.这样，当前的工作目录中的更改（包括未提交的内容）就会被存储起来，而不会影响版本历史。


5.切换到其他分支：


6.右键点击工作目录，选择 TortoiseGit -&gt; Switch/Checkout...（中文界面中可能显示为“切换/检出…”）。
7.在弹出的对话框中，选择您想切换到的分支，然后点击“确定”。
8.TortoiseGit 会切换到指定的分支，并确保您的工作目录处于干净状态。


9.恢复暂存的工作：


10.如果您想恢复之前暂存的工作，右键点击工作目录，选择 TortoiseGit -&gt; Stash Pop（中文界面中可能显示为“恢复变更”）。
11.这样，之前存储的变更会被恢复到当前的工作目录中。

通过上述步骤，您可以在不产生提交记录的情况下暂存您的更改，并切换到其他分支继续工作。



### 创建分支的时候跟踪有什么用

在 Git 中，跟踪分支（Tracking Branch）的主要作用是让本地分支与远程分支（或其他分支）自动建立关联。这种关联可以简化日常操作，并提供更直观的状态提示。以下是跟踪分支的具体用途：

---

1. **简化命令操作**
当本地分支跟踪了远程分支后，以下操作不再需要手动指定远程分支名：
• `git pull`: 直接拉取远程分支的最新代码到本地分支。

• `git push`: 直接推送本地分支的提交到对应的远程分支。


例如：
```bash
# 创建并跟踪远程分支 origin/feature
git checkout -b feature origin/feature

# 后续操作无需指定远程分支名
git pull  # 自动从 origin/feature 拉取
git push  # 自动推送到 origin/feature
```

---

2. **自动同步状态**
• `git status` 提示差异：Git 会显示本地分支与跟踪分支之间的提交差异（领先或落后多少提交）。

  ```
  Your branch is ahead of 'origin/feature' by 2 commits.
  Your branch is behind 'origin/main' by 3 commits.
  ```
• `git branch -vv`：查看所有本地分支及其跟踪的远程分支状态。

---

3. **避免手动指定参数**
• 无需重复输入远程分支名：如果没有跟踪分支，每次操作都需要手动指定远程分支：

  ```bash
  git push origin feature  # 不跟踪时需要手动指定
  git pull origin feature  # 同上
  ```

---

4. **`git rebase` 或 `git merge` 的默认目标**
如果本地分支跟踪了另一个分支（如主分支），某些操作会自动基于跟踪分支进行：
```bash
# 假设当前分支跟踪 origin/main
git rebase  # 默认会对 origin/main 执行 rebase
```

---

5. **应用场景示例**
• 场景 1：协作开发  

  多人协作时，本地分支跟踪远程的 `feature` 分支，能快速同步他人提交的代码。
• 场景 2：持续集成  

  本地开发分支跟踪远程的 `dev` 分支，确保本地代码始终与团队最新版本保持一致。

---

如何设置跟踪分支？
• 创建时直接跟踪：

  ```bash
  git checkout -b <本地分支名> <远程分支名>
  # 示例
  git checkout -b feature origin/feature
  ```
• 推送时设置跟踪：

  ```bash
  git push -u origin <分支名>  # -u 表示设置跟踪
  ```
• 修改现有分支的跟踪关系：

  ```bash
  git branch -u origin/<远程分支名>  # 为当前分支设置跟踪
  ```

---

总结
跟踪分支的核心作用是让 Git 自动关联本地和远程分支，减少手动操作，提高效率，同时通过状态提示帮助开发者更清晰地了解代码同步情况。对于频繁与远程仓库交互的场景（如团队协作），跟踪分支几乎是必备的实践。



### 基于主分支创建并且跟踪了开发分支，导致不小心就推送到主分支了

你在使用 Git 时可能遇到了 分支跟踪关系错误 导致意外推送的问题。以下是具体分析和解决方案：

---

⚠️ **问题根源**
1. 分支跟踪关系错误  
   • 假设你基于 `main` 分支创建了本地分支 `dev`，但错误地将 `dev` 分支的跟踪目标设置为 `origin/main`（而非 `origin/dev`）。

   • 此时执行 `git push` 会默认推送代码到 `origin/main`，覆盖主分支内容。


2. 验证跟踪关系  
   运行以下命令查看分支跟踪状态：
   ```bash
   git branch -vv
   ```
   如果输出类似：
   ```
   * dev   a1b2c3d [origin/main] Commit message
     main  e4f5g6h [origin/main] Another commit
   ```
   说明 `dev` 分支跟踪的是 `origin/main`，而非预期的 `origin/dev`。

---

🔧 **解决方案**
**1. 修正分支跟踪关系**
• 重新设置跟踪分支  

  将本地 `dev` 分支的跟踪目标改为正确的远程分支（如 `origin/dev`）：
  ```bash
  git branch -u origin/dev dev
  ```
  或切换到 `dev` 分支后直接设置：
  ```bash
  git checkout dev
  git branch -u origin/dev
  ```

• 验证修改结果  

  再次运行 `git branch -vv`，确认跟踪关系已更新：
  ```
  * dev   a1b2c3d [origin/dev] Commit message
    main  e4f5g6h [origin/main] Another commit
  ```

---

**2. 推送时明确指定分支**
即使跟踪关系正确，重要分支（如 `main`） 的推送建议显式指定分支名，避免误操作：
```bash
# 推送 dev 分支到远程 dev
git push origin dev

# 推送 main 分支时格外谨慎（需权限）
git push origin main
```

---

**3. 恢复主分支状态（若已误推送）**
如果已经误推送代码到 `origin/main`，按以下步骤恢复：
1. 本地回滚到正确提交  
   ```bash
   git checkout main
   git reset --hard <正确提交的哈希值>
   ```

2. 强制推送到远程  
   ```bash
   git push -f origin main
   ```
   > ⚠️ 强制推送会覆盖远程分支，需确保团队成员知晓此操作。

---

**4. 预防措施**
• 分支保护规则  

  在 Git 平台（如 GitHub/GitLab）中为 `main` 分支设置保护规则：
  • 禁止直接推送，仅允许通过 Pull Request 合并。

  • 要求代码审查和 CI 通过。


• 别名和脚本  

  将常用命令封装为别名，避免手动输入分支名：
  ```bash
  # 示例：推送当前分支到同名远程分支
  git config --global alias.publish 'push -u origin HEAD'
  ```

• 推送前检查  

  养成推送前检查的习惯：
  ```bash
  git status          # 查看当前分支和修改状态
  git remote -v       # 确认远程仓库地址
  git branch -vv      # 确认跟踪关系
  ```

---

📝 **总结**
• 根本原因：分支跟踪关系错误导致 `git push` 默认推送到主分支。

• 修复步骤：修正跟踪关系 → 显式推送 → 必要时恢复主分支。

• 长期预防：分支保护 + 推送前检查 + 明确指定分支名。

建议定期通过 `git branch -vv` 检查跟踪关系，尤其在协作开发中，避免因配置错误导致代码丢失或覆盖。



### 配置别名

```
git config --global alias.st status
git config --global alias.pl pull
git config --global alias.aa 'add -A'
git config --global alias.ci commit
git config --global alias.ca 'commit -am'
git config --global alias.ph push
```



### Github表情符

在Github中可以在 Pull Requests, Issues, 提交消息, Markdown 文件里加入表情符。使用方法 :name_of_emoji:

如输入

```
:smile: :flushed: :sleeping:
:sunny: :snowman: :full_moon:
:ghost: :camera: :calendar:
```

输出    
:smile: :flushed: :sleeping:    
:sunny: :snowman: :full_moon:    
:ghost: :camera: :calendar:    



### 提交说明

* [Commit message 和 Change log 编写指南](http://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html)



### Git 贡献提交规范

- `feat` 增加新功能
- `fix` 修复问题/BUG
- `style` 代码风格相关无影响运行结果的
- `perf` 优化/性能提升
- `refactor` 重构
- `revert` 撤销修改
- `test` 测试相关
- `docs` 文档/注释
- `chore` 依赖更新/脚手架配置修改等
- `workflow` 工作流改进
- `ci` 持续集成
- `types` 类型定义文件更改
- `wip` 开发中

规范 git 提交信息，请使用 commitlint

> [git commit 提交规范 & 规范校验](https://blog.csdn.net/y491887095/article/details/80594043)
> [如何写好 Git commit messages](https://www.cnblogs.com/cpselvis/p/6423874.html)
> [git commit 规范指南](https://www.jianshu.com/p/201bd81e7dc9?utm_source=oschina-app)

```text
用于说明 commit 的类别，只允许使用下面7个标识。
    feat：新功能（feature）
    fix：修补bug
    docs：文档（documentation）
    style： 格式（不影响代码运行的变动）
    refactor：重构（即不是新增功能，也不是修改bug的代码变动）
    test：增加测试
    chore：构建过程或辅助工具的变动
如果type为feat和fix，则该 commit 将肯定出现在 Change log 之中。
```



### 常见问题

#### 如何配置Git支持对文件名的大小写敏感

方案一是设置Git大小写敏感

```
git config core.ignorecase false
```



### <a name="practice">练习</a>

1. 安装[Github](https://github.com/)的客户端 [windows 版下载](https://windows.github.com/)
1. 注册Github的账号
1. 创建一个名为`front-end-learn` 的项目
1. 在该项目中创建一个`README.md` 提交代码,流程如下
   1. 检出仓库
   1. 将README.md文件添加到版本控制系统
   1. 提交README.md
   1. 将改动推送到服务器
1. 修改`README.md`的内容 提交代码,流程如下
   1. 提交README.md
   1. 将改动推送到服务器

注：Github的客户端包含图形界面和命令行（Git Shell）界面。虽然他们都包含一样的功能，但推荐使用命令行来完成上面的工作。



### 实战

* [githug](https://github.com/Gazler/githug) 闯过 55 个关卡，你就掌握 Git 啦~ [介绍](http://segmentfault.com/a/1190000004222489)



### 拓展阅读

* [猴子都能懂的Git入门](http://backlogtool.com/git-guide/cn/)
* [git-recipes](https://github.com/geeeeeeeeek/git-recipes/wiki) 高质量的Git中文教程
* [Git 及托管商 Github 的使用](https://github.com/xirong/my-git)
* [版本控制入门插图教程](http://www.ruanyifeng.com/blog/2008/12/a_visual_guide_to_version_control.html)
* [git - 简明指南](http://rogerdudler.github.io/git-guide/index.zh.html)
* [史上最浅显易懂的Git教程！](http://rogerdudler.github.io/git-guide/index.zh.html)
* [GitHub秘籍](https://github.com/tiimgreen/github-cheat-sheet/blob/master/README.zh-cn.md)
* [《Git in Practice》作者访谈：关于Git的八个问题](http://www.infoq.com/cn/articles/interview-Mike-McQuaid-git-practice)
* [Linus Torvalds 传记 By 池建强](http://www.chenjunlu.com/2014/07/linus-torvalds-biography/)



### git 与 svn 的区别在哪里？

   ```
   git 和 svn 最大的区别在于 git 是分布式的，而 svn 是集中式的。因此我们不能再离线的情况下使用 svn。如果服务器
   出现问题，我们就没有办法使用 svn 来提交我们的代码。

   svn 中的分支是整个版本库的复制的一份完整目录，而 git 的分支是指针指向某次提交，因此 git 的分支创建更加开销更小
   并且分支上的变化不会影响到其他人。svn 的分支变化会影响到所有的人。

   svn 的指令相对于 git 来说要简单一些，比 git 更容易上手。
   ```

   详细资料可以参考：
   [《常见工作流比较》](https://github.com/geeeeeeeeek/git-recipes/wiki/3.5-\\%E5\\%B8\\%B8\\%E8\\%A7\\%81\\%E5\\%B7\\%A5\\%E4\\%BD\\%9C\\%E6\\%B5\\%81\\%E6\\%AF\\%94\\%E8\\%BE\\%83)
   [《对比 Git 与 SVN，这篇讲的很易懂》](https://juejin.im/post/5bd95bf4f265da392c5307eb)
   [《GIT 与 SVN 世纪大战》](https://blog.csdn.net/github_33304260/article/details/80171456)
   [《Git 学习小记之分支原理》](https://www.jianshu.com/p/e8ad60710017)



### 经常使用的 git 命令？

   ```
git init                     // 新建 git 代码库
git add                      // 添加指定文件到暂存区
git rm                       // 删除工作区文件，并且将这次删除放入暂存区
git commit -m [message]      // 提交暂存区到仓库区
git branch                   // 列出所有分支
git checkout -b [branch]     // 新建一个分支，并切换到该分支
git status                   // 显示有变更的文件
   ```

如：
git checkout -b develop
git pull origin develop
git switch test
git merge develop

详细资料可以参考：
   [《常用 Git 命令清单》](http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html)



### git pull 和 git fetch 的区别 

   ```
   git fetch 只是将远程仓库的变化下载下来，并没有和本地分支合并。
   git pull 会将远程仓库的变化下载下来，并和当前分支合并。
   ```

   [《详解 git pull 和 git fetch 的区别》](https://blog.csdn.net/weixin_41975655/article/details/82887273)



### git rebase 和 git merge 的区别

   ```
   git merge 和 git rebase 都是用于分支合并，关键在 commit 记录的处理上不同。
   git merge 会新建一个新的 commit 对象，然后两个分支以前的 commit 记录都指向这个新 commit 记录。这种方法会
   保留之前每个分支的 commit 历史。
   git rebase 会先找到两个分支的第一个共同的 commit 祖先记录，然后将提取当前分支这之后的所有 commit 记录，然后
   将这个 commit 记录添加到目标分支的最新提交后面。经过这个合并后，两个分支合并后的 commit 记录就变为了线性的记
   录了。
   ```

   [《git rebase 和 git merge 的区别》](https://www.jianshu.com/p/f23f72251abc)
   [《git merge 与 git rebase 的区别》](https://blog.csdn.net/liuxiaoheng1992/article/details/79108233)



### vscode-git中的U,M和D文件标记含义

- M modified
  你已经在github中添加过该文件，然后你对这个文件进行了修改，就会文件后标记M
- U untracked
  你在本地新建了这个文件，还未提交到github上，就会标记U
- D delete
  你删除了这个文件，vscode-git会记录下这个状态
- 6,U
  表示有6个错误且untracked
  这些标记可以很清晰地帮助你查看工作区每个文件的git状态



### git修改文件大小写

使用git的时候，有时我们需要修改文件名的大小写，但是默认情况下，git是会忽略文件名大小写的，如果我们要修改文件名称大小写，可以使用试下方法：

首先，我们将 index.js 这个文件修改为 aindex.js，然后使用 git add . 将其贮存。

接着我们将其修改为 Index.js，再次使用 git add . 进行贮存，可以通过 git status 看到这个文件名的变化，是从 index.js 重命名为 Index.js，中间那个 aindex.js 只是用来桥接的，并不会产生真正的提交记录，只有最后那个会产生一条 rename 的记录。并且通过这种方式修改的文件名，切换分支也不会出现之前那种红色提示了。

总结
虽然这种方式操作时会略显繁琐，但是在后续的切换分支等方面，会省心很多，所以我比较推荐这种方式。



### 线上bug修复流程：

网页在master创建分支
本地直接切换到该分支
修改代码推到该分支
该分支合并代码到release产品验收
该分支合并代码到master发布上线
该分支合到develop
切换到自己原来的测试分支
测试分支拉取develop代码



### Git提交代码的注释type

feat: 新特性
fix: 修复bug
build: 构建或者外部依赖的变更
refactor: 代码重构，既不是feat也不是fix的代码变更
docs: 文档变更
style: 风格，不会影响代码代码运行的变动（空格，分号，格式等等）
perf: 性能优化
revert: 回退
chore: 其他更新



### Git全局设置重定向地址

Git全局重定向拉取服务器是指在使用Git进行代码拉取时，将默认的代码源站重定向到其他服务器。更新源站是指更新代码源站的地址。

在Git中，可以通过修改全局配置文件来实现重定向拉取服务器和更新源站。

#### git配置http和git协议自动转换

```
git config --global url."http://gitlab.xxx.io/".insteadOf git@gitlab.xxx.io:
```

这条命令的作用是将所有使用git://协议的仓库地址替换为https://协议的地址。

#### 简单命令处理：

可以选择一种自己习惯的

Clone with SSH 

```
git config --global url."http://gitlab.dustess.net/".insteadOf git@gitlab.boundless-tech.com.cn:
```

Clone with HTTP（好像不太行）

```
git config --global url."http://gitlab.dustess.net/".insteadOf "http://gitlab.boundless-tech.com.cn":
```

#### 复杂一点的具体步骤如下：

1. 打开终端或命令行工具，输入以下命令进入全局配置文件编辑模式：git config --global --edit
2. 在打开的配置文件中，找到名为`[url]`的节（如果没有则手动添加），在该节下添加以下内容：insteadOf = <原始源站地址> <重定向的服务器地址>其中，`<原始源站地址>`是你想要重定向的代码源站地址，`<重定向的服务器地址>`是你希望将代码拉取到的服务器地址。

   例如，如果想将原始源站地址`https://github.com`重定向到服务器地址`https://git.example.com`，则配置文件内容如下：

```
insteadOf = https://github.com https://git.example.com
```

保存并关闭配置文件。

配置完成后，当你使用Git命令从原始源站拉取代码时，Git会自动将源站地址重定向到指定的服务器地址。

需要注意的是，更新源站是指更新代码源站的地址，即将原始源站地址更新为新的地址。如果源站地址发生变化，你需要手动修改全局配置文件中的重定向配置，将重定向的服务器地址更新为新的地址。



### git的最佳分支管理流程

![img](https://images2018.cnblogs.com/blog/1287300/201804/1287300-20180420093948272-181557850.png)

　　再简单复习各个分支：

- master: 主分支，主要用来版本发布。
- develop：日常开发分支，该分支正常保存了开发的最新代码。
- feature：具体的功能开发分支，只与 develop 分支交互。
- release：release 分支可以认为是 master 分支的未测试版。比如说某一期的功能全部开发完成，那么就将 develop 分支合并到 release 分支，测试没有问题并且到了发布日期就合并到 master 分支，进行发布。
- hotfix：线上 bug 修复分支。

　　首先介绍企业的一般流程，就是版本发布（假设为V3R2）和开发新版本（假设新版本为V3R3）的问题，其实一条时间线同时存在这两个版本，一个是稳定的已发布版本，另一个是正在开发的未来需要发布的版本。那么为什么要开发新版本呢？因为软件是要演进的，要适应变化和需求，一段时间迭代后发布的软件比喻V3R2也会不断暴露出问题，这类问题也需要在新版本中变得可用。因为V3R3的都是新特征新变化

　　**feature：**
　　只与develop交互，因为feature就是新版本开发为了升级和演进需要用的，里面的所有代码只能在发布新版本且经过测试的时候才合进去master，然后在master打tag表明所有新功能开发完毕，一次性合并。同时我们开发一般是不同的人开发不同的功能，因此各自都应该有自己的feature，然后断断续续并进develop所以，保证develop是个新功能持续集成的版本。

　　**hotfix：**

　　这个分支用来修复主线master的BUG，但是要注意的是，在旧版本的BUG，新版本也是存在的，因此develop分支也存在该BUG，具体来说就是V3R2和V3R3都有该BUG，因此，修复的时候必须要提交两个分支master和develo否则，后面需要rebase就麻烦了。



### 代码pr是什么意思

代码PR（Pull Request）是软件开发协作流程中的一个重要概念，特别是在使用Git版本控制系统和代码托管平台（如GitHub、GitLab或Bitbucket）的项目中。PR表示一个开发者向项目的主要代码库（往往是上游仓库或者主分支）提出合并其代码更改的请求。这个过程涉及以下几个关键步骤：

1. **分叉（Fork）或克隆（Clone）**: 开发者通常会从原始项目仓库分叉一份到自己的账户下，或者直接克隆到本地，以便在不影响原仓库的情况下独立工作。

2. **修改与提交**: 在自己的分支上进行代码修改、增加新功能、修复bug或进行其他改进，并提交这些更改到自己的仓库。

3. **发起Pull Request**: 当开发者认为自己的改动已经完成并且准备好了让项目维护者或团队成员审查时，会在代码托管平台上向原项目发起一个PR。这个请求会展示出所有更改的差异（diffs），通常会附带描述改动原因、目的以及如何测试这些更改的注释。

4. **代码审查（Code Review）**: 项目维护者或团队其他成员会对PR进行审查，可能会提出问题、建议或要求进一步的修改。

5. **讨论与迭代**: 根据审查反馈，开发者可能需要进一步修改代码，并且这些更新会实时反映在PR中，直到团队达成共识。

6. **合并（Merge）**: 当PR经过审查并被认为满足项目标准和要求后，会被合并到主分支或目标分支中，成为项目的一部分。

PR机制鼓励开放源代码项目中的协作，提高了代码质量，并促进了知识共享。它也是分布式团队合作中不可或缺的工具。



### git 出现 The requested URL returned error: 403

**问题：**

cch:requsetDatas leo$ git push origin master

remote: Permission to bbb/requsetDatas.git denied to aaa.

fatal: unable to access 'https://github.com/bbb/requsetDatas.git/': The requested URL returned error: 403

**解决方法：**

1：终端输入：vim .git/config 就是打开git的config配置文件。

2：找到下面一句

```
[remote "origin"]
url = https://github.com/bbb/example.git
```

修改为：

```
[remote "origin"]
url = https://bbb@github.com/bbb/example.git
```

保存并退出。(注意颜色字体)

3：再次git push origin master，提示输入密码，OK。



### 提交代码报错error Command "husky-run" not found.

删除.git/hooks文件夹，重新提交

step1:

```
rm -rf .git/hooks
```

step2：重新提交即可



## mac怎么全局安装npm install husky@4.2.5 -g在哪个目录运行这个命令

在 macOS 系统中，全局安装 `husky@4.2.5` 的命令 `npm install husky@4.2.5 -g` **可以在任意目录下运行**，因为 `-g`（全局安装）会忽略当前工作目录，直接将包安装到系统的全局 `node_modules` 目录中。以下是具体说明和注意事项：

------

### ⚙️ 1. **全局安装路径**

默认情况下，macOS 的 npm 全局安装路径为 **`/usr/local/lib/node_modules/`**：

- 执行 `npm root -g` 可查看当前全局安装路径。
- 安装后，`husky` 的可执行文件会链接到 **`/usr/local/bin/`** 目录下。

------

### 🔒 2. **权限问题与解决方案**

全局安装需系统目录写入权限，可能因权限不足报错（`EACCES`）：

- 推荐方案：使用 sudo 提权：

  ```
  sudo npm install husky@4.2.5 -g
  ```

- 替代方案（避免 sudo）：修改 npm 全局路径到用户目录：

  ```
  # 创建用户目录下的全局安装路径
  mkdir ~/.npm-global
  # 配置 npm 使用新路径
  npm config set prefix '~/.npm-global'
  # 更新环境变量（添加到 ~/.bashrc 或 ~/.zshrc）
  echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.zshrc
  source ~/.zshrc
  # 重新安装（无需 sudo）
  npm install husky@4.2.5 -g
  ```

------

### 🔍 3. **验证安装**

安装后通过以下命令确认：

```
# 查看安装路径
npm list -g --depth=0 | grep husky
# 检查可执行文件位置
which husky
```

------

### 💎 4. **注意事项**

- **Node 版本管理工具（如 nvm）**：
   若使用 `nvm`，全局路径为 `~/.nvm/versions/node/<版本>/lib/node_modules`，同样支持任意目录安装。
- **Husky 版本兼容性**：
   `husky@4.2.5` 是旧版（新版为 `husky@8+`），需确保项目兼容性。
- **全局命令的使用**：
   安装后可直接在终端运行 `husky` 命令（例如 `husky install`）。

------

### 📌 **总结**

- **运行目录**：任意终端目录均可执行 `npm install husky@4.2.5 -g`。
- 安装位置：
  - 默认路径：`/usr/local/lib/node_modules/husky`（需 `sudo`）；
  - 自定义路径：`~/.npm-global/lib/node_modules/husky`（无需 `sudo`）。
- **权限问题**：优先通过 `sudo` 或修改全局路径解决。







# Git规范

### Git提交规范

- validate-commit-msg检查提交信息是否规范
- conventional-changelog生成 Change log

### Git提交书写格式

------

**简单示例：git commit -m "feat(commit): 添加验证提交信息功能"**

- commit message包含三部分：Header，Body，Footer，其中Header是必需的，Body、Footer可忽略。格式为：

```text
<type>(<scope>): <subject>
// 空一行
<body>
// 空一行
<footer>
```

- 通常使用提交 `(): `
- Header包含 type，scope（可选），subject

### Type 类型 （feat、fix、docs、style、refactor、test、chore）

为此次内容变更的类型，只能为下面的标识： - feat: 新特性 - fix: 修复bug - build: 构建或者外部依赖的变更~~ - refactor: 代码重构，既不是feat也不是fix的代码变更 - docs: 文档变更 - style: 风格，不会影响代码代码运行的变动（空格，分号，格式等等） - perf: 性能优化 - revert: 回退 - chore: 其他更新

### Scope 范围

当前内容变更影响的范围，如当前变更内容的文件的目录，或者当前变更内容功能名称 比如组件名(dialog)、功能名(user)、插件名(rabbit)

### Subject 简述

对当前变更做的简短描述，比如新增、修改、删除、重新、测试、添加等 - 用动词开头，比如用"change"而不是"changed"或者"changes" - ~~第一个字母小写~~ - 结尾不需要加句号

### Body 详述

当前变更的详细描述，可以分为多行，说明为什么要变更，以及之前的行为对比

### Footer

footer包含不兼容变更、变更解决的对应issue id

```text
1. feat(mock): 新增数据模拟
2. fix: 修复个人中心上传头像bug
3. build(scripts): 修改入口文件引入方式
   引入方式修改为glob全局引入，不需要在手动export

4. chore: 删除插件打包脚本多余注释
```

出现下面错误执行 rm -rf .git/hooks然后重新安装下husky

### 常用拉取项目

```text
1、git clone [url]: 项目仓库地址
  例：git clone http://192.168.10.117/wangxu/rabbit-framework-web-practice.git （常用方式）
2、git init与 git remote
  在本地工作目录中先执行git init，然后执行 git remote add origin [url]
```

### 常用拉取

```text
git pull
```

### 常用提交

```text
1. git add .
2. git commit -m "[commit message]"
3. git push
注：commit message 书写方式参照下列方式，例："fix(page):修复page组件页面高度计算方式"
```

### 拉取固定分支

```text
git clone -b [url]
例：git clone -b dev-v1.0.8 http://192.168.10.117/wangxu/rabbit-framework-web-practice.git
```

### 拉取项目同时更改项目名称

```text
git clone [url] [name]: 项目新名称
例：git clone http://192.168.10.117/wangxu/rabbit-framework-web-practice.git rabbit-1.0.8
```

### 修改远程地址

```text
方法1：
git remote set-url origin [地址](http://192.168.10.117/framework/rabbit-web.git)
方法2：
git remote rm origin
git remote add origin [地址](http://192.168.10.117/framework/rabbit-web.git)
```

### git 获取其他分支commit内容

```text
1. git reflog 查看所有分支变动信息并获取提交短号
2. git cherry-pick [短号/b602289] 将提交内容拉取下来
```

------

### GIT常用命令操作

```text
拉取远程项目到本地：git clone git://github.com/schacon/grit.git
查看工作状态：git status
添加所有改动到暂存区：git add .
添加指定文件到暂存区 git indexgit add [file name]
提交暂存区并添加注释: git commit -m "your message"
提交暂存区所有改变文件：git commit -a
比较commit文件差异：git commit -v
绕过husky代码检测：git commit --no-verify -m "提交信息"

修改本仓库修改文件大小写敏感(默认为true)：git config core.ignorecase false
推送到远程仓库对应分支: git push origin [branch]
拉取最新代码到本地：git pull origin [branch]
合并分支内容到当前分支：git merge [branch]
查看本地所有分支：git branch
查看所有的分支：git branch -a
查看远程所有分支：git branch -r
切换分支：git checkout [branch]
切换并新建本地分支：git checkout -b [branch]
删除本地指定分支：git branch -D [branch]

查看提交日志: git log
查看变化内容：git diff
查看尚未提交变化内容：git diff --cached
看所有用户：git config --list
查看config 用户名：git config user.name
查看config 邮箱：git config user.email

添加远程分支地址：git remote add [name] [http]
显示远程库地址列表：git remote -v
查看远程库：git remote show
删除暂存区和工作区中指定文件：git rm [file]
强制删除暂存区和工作区中指定文件：git rm -f [file]
删除暂存区中指定文件：git rm --cached [file]
查看提交文件列表：git ls-files
推送文件到临时空间：git stash push
获取临时空间文件：git stash pop
```

### git命令速查表

### git常用命令

| 命令                   | 简要说明                                 | 命令                | 简要说明                        |
| ---------------------- | ---------------------------------------- | ------------------- | ------------------------------- |
| git add                | 添加至暂存区                             | git add–interactive | 交互式添加                      |
| git branch             | 分支管理                                 | git checkout        | 检出到工作区、切换或创建分支    |
| git cherry-pick        | 提交拣选                                 | git clean           | 清除工作区未跟踪文件            |
| git clone              | 克隆版本库                               | git commit          | 提交                            |
| git config             | 查询和修改配置                           | git describe        | 通过里程碑直观地显示提交ID      |
| git diff               | 差异比较                                 | git difftool        | 调用图形化差异比较工具          |
| git fetch              | 获取远程版本库的提交                     | git log             | 显示提交日志                    |
| git init               | 版本库初始化                             | git init-db*        | 同义词，等同于 git init         |
| git merge              | 分支合并                                 | git mergetool       | 图形化冲突解决                  |
| git mv                 | 重命名                                   | git rebase          | 分支变基                        |
| git pull               | 拉回远程版本库的提交                     | git push            | 推送至远程版本库                |
| git rebase–interactive | 交互式分支变基                           | git reflog          | 分支等引用变更记录管理          |
| git remote             | 远程版本库管理                           | git repo-config*    | 同义词，等同于 git config       |
| git reset              | 重置改变分支“游标”指向                   | git rev-parse       | 将各种引用表示法转换为哈希值等  |
| git revert             | 反转提交                                 | git rm              | 删除文件                        |
| git show               | 显示各种类型的对象                       | git stage*          | 同义词，等同于 git add          |
| git stash              | 保存和恢复进度                           | git status          | 显示工作区文件状态              |
| git tag                | 里程碑管理                               | git help            | 帮助                            |
| git annotate           | 同义词，等同于git blame                  | git archive         | 文件归档打包                    |
| git bisect             | 二分查找                                 | git blame           | 文件逐行追溯                    |
| git cat-file           | 版本库对象研究工具                       | git citool          | 图形化提交，相当于 git gui 命令 |
| git format-patch       | 创建邮件格式的补丁文件。参见 git am 命令 | git grep            | 文件内容搜索定位工具            |
| git gui                | 基于Tcl/Tk的图形化工具，侧重提交等操作   |                     |                                 |

### 协议相关命令

| 命令                   | 简要说明                                  | 命令               | 简要说明                                    |
| ---------------------- | ----------------------------------------- | ------------------ | ------------------------------------------- |
| git daemon             | 实现Git协议                               | git http-backend   | 实现HTTP协议的CGI程序，支持智能HTTP协议     |
| git instaweb           | 即时启动浏览器通过 gitweb 浏览当前版本库  | git shell          | 受限制的shell，提供仅执行Git命令的SSH访问   |
| git update-server-info | 更新哑协议需要的辅助文件                  | git http-fetch     | 通过HTTP协议获取版本库                      |
| git http-push          | 通过HTTP/DAV协议推送                      | git remote-ext     | 由Git命令调用，通过外部命令提供扩展协议支持 |
| git remote-fd          | 由Git命令调用，使用文件描述符作为协议接口 | git remote-ftp     | 由Git命令调用，提供对FTP协议的支持          |
| git remote-ftps        | 由Git命令调用，提供对FTPS协议的支持       | git remote-http    | 由Git命令调用，提供对HTTP协议的支持         |
| git remote-https       | 由Git命令调用，提供对HTTPS协议的支持      | git remote-testgit | 协议扩展示例脚本                            |

### 合并相关的辅助命令

| 命令                | 简要说明                                                     |
| ------------------- | ------------------------------------------------------------ |
| git merge-base      | 供其他脚本调用，找到两个或多个提交最近的共同祖先             |
| git merge-file      | 针对文件的两个不同版本执行三向文件合并                       |
| git merge-index     | 对index中的冲突文件调用指定的冲突解决工具                    |
| git merge-octopus   | 合并两个以上分支。参见 git merge 的octopus合并策略           |
| git merge-one-file  | 由 git merge-index 调用的标准辅助程序                        |
| git merge-ours      | 合并使用本地版本，抛弃他人版本。参见 git merge 的ours合并策略 |
| git merge-recursive | 针对两个分支的三向合并。参见 git merge 的recursive合并策略   |
| git merge-resolve   | 针对两个分支的三向合并。参见 git merge 的resolve合并策略     |
| git merge-subtree   | 子树合并。参见 git merge 的 subtree 合并策略                 |
| git merge-tree      | 显式三向合并结果，不改变暂存区                               |
| git fmt-merge-msg   | 供执行合并操作的脚本调用，用于创建一个合并提交说明           |
| git rerere          | 重用所记录的冲突解决方案                                     |

### 版本库管理相关命令

| 命令               | 简要说明                             | 命令               | 简要说明                               |
| ------------------ | ------------------------------------ | ------------------ | -------------------------------------- |
| git count-objects  | 显示松散对象的数量和磁盘占用         | git filter-branch  | 版本库重构                             |
| git fsck           | 对象库完整性检查                     | git fsck-objects*  | 同义词，等同于 git fsck                |
| git gc             | 版本库存储优化                       | git index-pack     | 从打包文件创建对应的索引文件           |
| git pack-objects   | 从标准输入读入对象ID，打包到文件     | git pack-redundant | 查找多余的 pack 文件                   |
| git pack-refs      | 将引用打包到 .git/packed-refs 文件中 | git prune          | 从对象库删除过期对象                   |
| git prune-packed   | 将已经打包的松散对象删除             | git relink         | 为本地版本库中相同的对象建立硬连接     |
| git repack         | 将版本库未打包的松散对象打包         | git show-index     | 读取包的索引文件，显示打包文件中的内容 |
| git unpack-objects | 从打包文件释放文件                   | git verify-pack    | 校验对象库打包文件                     |



### 配置commitlint

1.我们commit代码时，如果想要有统一规范的，要让每个人都按照统一的标准来执行，我们可以利用commitlint来实现。

2.安装包：pnpm add @commitlint/config-conventional @commitlint/cli -D
添加配置文件，新建commitlint.config.cjs(注意是cjs)，然后添加下面的代码

```
module.exports = \\{
  extends: ['@commitlint/config-conventional'],
  // 校验规则
  rules: \\{
    'type-enum': [
      2,
      'always',
      [
        'feat',
        'fix',
        'docs',
        'style',
        'refactor',
        'perf',
        'test',
        'chore',
        'revert',
        'build',
      ],
    ],
    'type-case': [0],
    'type-empty': [0],
    'scope-empty': [0],
    'scope-case': [0],
    'subject-full-stop': [0, 'never'],
    'subject-case': [0, 'never'],
    'header-max-length': [0, 'always', 72],
  \\},
\\}
```

 3.在`package.json`中配置scripts命令

```javascript
\\{
  "scripts": \\{
    "commitlint": "commitlint --config commitlint.config.cjs -e -V"
  \\}
\\}
```

 4.配置结束，现在当我们填写`commit`信息的时候，前面就需要带着下面的`subject` 

```
'feat',//新特性、新功能
'fix',//修改bug
'docs',//文档修改
'style',//代码格式修改, 注意不是 css 修改
'refactor',//代码重构
'perf',//优化相关，比如提升性能、体验
'test',//测试用例修改
'chore',//其他修改, 比如改变构建流程、或者增加依赖库、工具等
'revert',//回滚到上一个版本
'build',//编译相关的修改，例如发布版本、对项目构建或者依赖的改动
```

 5.配置husy

```
npx husky add .husky/commit-msg
```

 6.在生成的commit-msg文件中添加下面的命令

```
. "$(dirname -- "$0")/_/husky.sh"
pnpm commitlint
```

这样配好后，每次[git](https://so.csdn.net/so/search?q=git&spm=1001.2101.3001.7020) commit -m ""就不能再随意写了，必须是 git commit -m 'fix: xxx' 符合类型的才可以，**需要注意的是类型的后面需要用英文的 :，并且冒号后面是需要空一格的，这个是不能省略的**



### gitee个人版仓库总容量

根据 Gitee 官方说明，个人版（社区版）的仓库总容量限制如下：

1. **总仓库容量**
    个人用户及其创建的组织下所有仓库总容量上限为 ​**​5GB​**​，该容量包含 Git 仓库和 SVN 仓库的总体积。
2. **单仓库限制**

- Git 单仓库容量上限为 **500MB**，SVN 单仓库上限为 **400MB**
- 单个文件最大 **50MB**（若企业版套餐则可能提升至 100MB 或更高）

1. **附件容量**

- 单个附件文件最大 **100MB**
- 每个仓库的附件总容量上限为 **1GB**

1. **其他限制**

- 私有仓库协作人数上限为 **5人**，公有仓库不限人数
- 若仓库体积超标，可通过历史改写瘦身工具（如 `git-repo-clean`）或升级企业版套餐解决。

建议开发者避免在仓库中直接存储大文件，可通过 Git LFS（大文件存储）管理二进制文件，以节省仓库容量。若需更高配额，可参考企业版的套餐标准（单仓库最高 3GB，总容量 100GB+）。



## github所有常用功能详细介绍，如watch、fork、starred

GitHub 作为广泛使用的代码托管和协作平台，提供了丰富的功能。以下是对常用功能的详细介绍，分类整理以帮助用户全面理解：

---

### **一、仓库管理基础**
1. **Star（星标）**
   - **作用**：收藏感兴趣的项目，支持开发者并提升项目曝光度。
   - **使用**：点击仓库右上角的 **Star** 按钮。
   - **场景**：快速访问常用项目；热门项目会进入 [GitHub Trending](https://github.com/trending) 榜单。
   - **技巧**：在个人资料页的 **Stars** 中可分类管理（需手动添加标签）。

2. **Fork（分叉）**
   - **作用**：复制他人仓库到自己的账号，独立修改而不影响原项目。
   - **使用**：点击仓库右上角的 **Fork** 按钮，选择目标账号。
   - **同步更新**：通过 `git remote add upstream 原仓库URL` 添加原仓库为上游，定期 `git fetch upstream` 并合并到本地分支。
   - **场景**：贡献代码（通过 Pull Request）或基于现有项目二次开发。

3. **Clone（克隆）**
   - **作用**：将远程仓库下载到本地。
   - **命令**：`git clone 仓库URL`。
   - **场景**：本地开发或查看代码。

---

### **二、协作与贡献**
4. **Pull Request（PR，拉取请求）**
   - **作用**：请求将你的代码变更合并到原仓库。
   - **流程**：
     1. Fork 仓库 → 本地修改 → 推送至自己的仓库。
     2. 在 GitHub 点击 **New Pull Request**，选择分支并提交。
   - **场景**：开源贡献、团队内代码审核。

5. **Issues（问题追踪）**
   - **作用**：报告 Bug、提议新功能或讨论任务。
   - **使用**：仓库内 **Issues** 标签页 → **New Issue**。
   - **技巧**：使用模板、标签（如 `bug`、`enhancement`）、指派负责人和项目看板关联。

6. **Discussions（讨论区）**
   - **作用**：开放式讨论（非问题追踪），如设计决策或使用帮助。
   - **启用**：仓库设置中手动开启。
   - **场景**：社区交流、Q&A。

---

### **三、通知与关注**
7. **Watch（关注）**
   - **作用**：控制接收仓库活动的通知。
   - **选项**：
     - **Not watching**：仅手动关注时通知（如被@提及）。
     - **Releases only**：仅新版本发布时通知。
     - **Watching**：所有活动（Issue、PR、提交等）均通知。
   - **设置**：仓库右上角点击 **Watch** 下拉菜单选择。

8. **Follow（关注用户）**
   - **作用**：关注其他用户的动态，显示在个人动态流中。
   - **操作**：进入用户主页 → 点击 **Follow**。

---

### **四、项目管理**
9. **Projects（项目看板）**
   - **作用**：类似看板墙，管理任务进度（如待办、进行中、已完成）。
   - **类型**：仓库级项目（仅限当前仓库）或组织级项目。
   - **集成**：与 Issues、PR 联动，自动化卡片生成。

10. **Wiki**
    - **作用**：托管项目文档，支持 Markdown。
    - **启用**：仓库设置中开启，通过 **Wiki** 标签页编辑。

11. **Milestones（里程碑）**
    - **作用**：为 Issues 或 PR 设定完成目标（如版本发布）。
    - **使用**：在 Issues/PR 中关联 Milestone，跟踪进度。

---

### **五、自动化与集成**
12. **GitHub Actions**
    - **作用**：自动化 CI/CD（测试、构建、部署）。
    - **配置**：在 `.github/workflows/` 下创建 YAML 文件定义工作流。
    - **场景**：自动运行测试、部署到服务器或发布包。

13. **GitHub Pages**
    - **作用**：托管静态网站（如文档、博客）。
    - **启用**：仓库设置 → Pages → 选择分支（如 `gh-pages` 或 `main` 下的 `/docs`）。

14. **Packages（包管理）**
    - **作用**：发布 npm、Docker 等软件包。
    - **集成**：与 Actions 配合自动化发布。

---

### **六、社交与发现**
15. **Explore（探索）**
    - **作用**：发现热门仓库、主题和趋势项目。
    - **入口**：顶部导航栏的 **Explore**。

16. **Trending（趋势榜）**
    - **作用**：查看每日/周/月热门项目（按语言、时间筛选）。
    - **访问**：[github.com/trending](https://github.com/trending)。

---

### **七、高级功能**
17. **Branch Protection（分支保护）**
    - **作用**：防止主分支被直接推送，要求 PR 审核和状态检查。
    - **设置**：仓库设置 → **Branches** → **Add rule**。

18. **Code Review（代码审查）**
    - **功能**：在 PR 中评论代码、建议修改、批准合并。
    - **工具**：行内评论、差异对比（Diff View）。

19. **Templates（模板）**
    - **作用**：标准化 Issues、PR 和仓库结构。
    - **配置**：在仓库中添加 `.github/ISSUE_TEMPLATE.md` 等文件。

---

### **八、用户与组织管理**
20. **Organizations（组织）**
    - **作用**：管理团队项目，设置角色权限（Owner、Member等）。
    - **场景**：企业或开源团队协作。

21. **Gists（代码片段）**
    - **作用**：分享单文件或代码片段，支持匿名创建。
    - **访问**：[gist.github.com](https://gist.github.com)。

---

### **操作示例**
- **同步 Fork 的仓库**：
  ```bash
  git remote add upstream https://github.com/原仓库/项目.git
  git fetch upstream
  git checkout main
  git merge upstream/main
  git push origin main
  ```

- **创建 Pull Request**：
  1. 在 Fork 的仓库页面点击 **Contribute → Open Pull Request**。
  2. 选择你的分支与原仓库的目标分支。
  3. 填写标题和描述，提交后等待审核。

---

通过合理利用这些功能，可以高效管理代码、参与协作并提升项目可见性。建议根据实际需求逐步探索，例如从 Star/Fork 开始，逐步尝试 Issues 和 PR，最终掌握 Actions 等高级工具。



### 有一个文件夹，里面有好多个项目，怎么让git忽略其下所有子文件夹没用的dist或者node_modules，请写出.git忽略文件

要忽略所有子文件夹中的 `dist` 和 `node_modules` 目录，只需在项目根目录的 `.gitignore` 文件中添加以下规则：

```
# 忽略所有名为 dist 的目录（递归匹配）
**/dist/

# 忽略所有名为 node_modules 的目录（递归匹配）
**/node_modules/
```

### 完整 `.gitignore` 示例：

```
### 全局忽略规则 ###
**/dist/
**/node_modules/

### 其他常见忽略项（可选） ###
# 系统文件
.DS_Store
Thumbs.db

# 编辑器设置
.idea/
.vscode/
*.suo
*.ntvs*
*.njsproj
*.sln

# 日志文件
*.log
npm-debug.log*

# 依赖目录（已单独处理，此处可省略）
# node_modules/  # 已被 **/node_modules/ 覆盖

# 构建产物
*.exe
*.out
*.app

# 环境变量文件
.env
.env.local
```

### 关键说明：

1. `**/` 表示**递归匹配所有层级的子目录**
2. 结尾的 `/` 确保只匹配**目录**（不会误伤同名文件）
3. 即使根目录下有同名文件夹也会被忽略（符合常见需求）

### 验证方法：

```
# 检查忽略规则是否生效
git check-ignore -v your_project/node_modules/some_file
git check-ignore -v subfolder/dist/index.html
```

> 此配置适用于所有主流 Git 版本（Git 2.0+）。对于大型项目，忽略 `node_modules` 可显著减少 `git status` 的扫描时间。



## 不想提交代码，怎么切换分支，使用sourcetree或者vscode面板

在不提交代码的情况下切换分支，可以通过**储藏（Stash）**功能临时保存工作目录的修改。以下是详细步骤：

------

### **方法 1：使用 VS Code**

1. **储藏当前修改**：
   - 打开 VS Code 左侧的 **源代码管理面板**（Git 图标）。
   - 在顶部输入框旁点击 **···**（更多操作） → 选择 **储藏** → **全部储藏**。
   - 输入储藏名称（可选）并确认。
2. **切换分支**：
   - 点击 VS Code 左下角的当前分支名（如 `main`）。
   - 在弹出的分支列表中，选择目标分支（如 `dev`）。
3. **恢复储藏内容**：
   - 切换成功后，回到源代码管理面板。
   - 点击 **···** → **储藏** → 选择 **应用最新的储藏**（或其他指定储藏）。

------

### **方法 2：使用 SourceTree**

1. **储藏当前修改**：
   - 打开 SourceTree，选择仓库。
   - 点击顶部工具栏的 **储藏** 按钮（盒子图标）。
   - 勾选 **包含未跟踪文件**（如果需要），输入描述 → 点击 **储藏**。
2. **切换分支**：
   - 在左侧 **分支** 列表中，双击目标分支（如 `dev`）。
3. **恢复储藏内容**：
   - 切换分支后，点击顶部工具栏的 **储藏** 按钮。
   - 选中刚刚创建的储藏 → 点击 **恢复**（恢复后储藏保留）或 **删除**（恢复后删除储藏）。

------

### **注意事项**

1. 冲突风险：
   - 如果目标分支和储藏的修改有冲突，恢复时需手动解决冲突（VS Code/SourceTree 会提示）。
2. 未跟踪文件：
   - 新建的文件默认不会储藏（除非勾选 **包含未跟踪文件**）。
3. 临时跳过储藏：
   - 在 VS Code 切换分支时，弹出警告框可直接选择 **储藏并切换**（一步完成储藏+切换）。
   - 在 SourceTree 切换分支时，若未储藏，会提示选择 **强行检出**（丢弃修改，**慎用**）。

------

### **总结**

- **推荐流程**：`储藏修改 → 切换分支 → 恢复储藏`。
- 避免使用 `git checkout -f` 或 `git switch -f`（强制切换），这会**丢失未提交的修改**。

通过以上步骤，无需提交代码即可安全切换分支，并保留所有工作目录更改。