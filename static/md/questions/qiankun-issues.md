---
title: qiankun问题
date: 2022-05-20 20:45:42
categories: 
- 前端问题
tags:
- qiankun
- 前端
---

## 有一个乾坤项目目录，里面有很多子应用的目录，怎么一键启动五个常用子应用platform、home...等，命令都是yarn dev

要实现一键启动五个子应用（如 `platform`、`home` 等），您可以使用 **并行执行工具** 结合 **脚本定制**。以下是具体步骤：

------

### 方法 1：使用 `concurrently`（推荐）

1. **在项目根目录安装工具**：

   ```
   yarn add -D concurrently
   ```

2. **在根目录的 `package.json` 中添加启动脚本**：

   ```
   \\{
     "scripts": \\{
       "start:all": "concurrently -n platform,home,app1,app2,app3 \"yarn --cwd platform dev\" \"yarn --cwd home dev\" \"yarn --cwd app1 dev\" \"yarn --cwd app2 dev\" \"yarn --cwd app3 dev\""
     \\}
   \\}
   ```

   - 替换 `app1,app2,app3` 为您的其他子应用目录名。
   - `-n` 参数为每个命令设置标签（方便日志区分）。
   - `--cwd [目录名]` 指定子应用的工作目录。

3. **运行命令**：

   ```
   yarn start:all
   ```

------

### 方法 2：使用 `npm-run-all`

1. **安装工具**：

   ```
   yarn add -D npm-run-all
   ```

2. **在 `package.json` 中配置**：

   ```
   \\{
     "scripts": \\{
       "dev:platform": "yarn --cwd platform dev",
       "dev:home": "yarn --cwd home dev",
       "dev:app1": "yarn --cwd app1 dev",
       "dev:app2": "yarn --cwd app2 dev",
       "dev:app3": "yarn --cwd app3 dev",
       "start:all": "run-p dev:*"
     \\}
   \\}
   ```

   - 为每个子应用创建独立脚本（如 `dev:platform`）。
   - `run-p dev:*` 并行执行所有以 `dev:` 开头的脚本。

3. **运行命令**：

   ```
   yarn start:all
   ```

------

### 方法 3：原生脚本（跨平台）

1. **在项目根目录创建脚本文件**：

   - Windows：创建start.cmd：

     ```
     @echo off
     start "platform" yarn --cwd platform dev
     start "home" yarn --cwd home dev
     start "app1" yarn --cwd app1 dev
     start "app2" yarn --cwd app2 dev
     start "app3" yarn --cwd app3 dev
     ```

   - Linux/macOS：创建start.sh：

     ```
     #!/bin/bash
     # Mac电脑在h5-scrm-suite根目录运行以下命令，即可一键启动乾坤
     # chmod +x start.sh && ./start.sh
     
     # 设置一个醒目的标题
     echo "🚀Starting qiankun applications...🚀"
     
     # 使用 () & 的方式让每个命令在子 shell 中后台运行
     (cd platform && yarn dev) &
     (cd home && yarn dev) &
     (cd msg-flow && yarn dev) &
     (cd content-hub && yarn dev) &
     (cd marketing && yarn dev) &
     (cd customer && yarn dev)
     
     # wait 命令会等待所有后台任务结束
     # 当你按下 Ctrl+C 时，它会捕获信号并终止所有子进程
     wait
     ```

> **命令解析**:
>
> - `#!/bin/bash`：指定脚本由 bash 解释器执行。
> - `(command) &`：`&` 符号让命令在后台运行，这样脚本就不会被第一个 `yarn dev` 阻塞。将命令放在 `()` 中可以确保 `cd` 只在子 shell 中生效，不会影响下一个命令。
> - `wait`：让主脚本等待所有后台任务完成。这有一个额外的好处是，当你在终端按下 `Ctrl+C` 时，所有由这个脚本启动的后台进程会一并被终止。

**如何使用**:

1. **添加执行权限**: `chmod +x start.sh`
2. **运行脚本**: `./start.sh`

#### 运行脚本

- Windows：双击 `start.cmd` 或在终端中执行。

- Linux/macOS：

  ```
  chmod +x start.sh && ./start.sh
  ```

------

### 关键注意事项

1. **子应用目录**：确保脚本中的目录名（如 `platform`）与您项目的实际目录匹配。
2. **依赖安装**：首次运行前，请在每个子应用中执行 `yarn install` 安装依赖。
3. **端口冲突**：检查各子应用的 `dev` 命令是否监听相同端口（如有冲突需手动修改配置）。
4. **日志混合问题**：`concurrently` 和 `npm-run-all` 会聚合日志，建议用 `-n` 参数标记来源（如 `-n platform,home,...`）。

按需选择方案，推荐使用 **`concurrently`** 或 **`npm-run-all`**，灵活简洁且跨平台兼容。

### 总结与建议

| 方法               | 优点                                                         | 缺点                                                         | 推荐场景                                                     |
| ------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **`concurrently`** | 1. **跨平台**，无需关心操作系统差异。 2. **日志聚合**在一个终端，带颜色和前缀，方便查看。 3. **集成在 `package.json`** 中，是前端工程化的标准做法。<br>4. 终止时（`Ctrl+C`）能干净地关闭所有进程。 | 需要额外安装一个开发依赖。                                   | **绝大多数情况下的首选方案**。特别是对于团队协作项目，这是一个清晰、统一的解决方案。 |
| **Shell 脚本**     | 1. 无需额外依赖。 2. 对于熟悉 Shell 的开发者非常灵活。       | 1. **不跨平台**，需要为 Windows 和 macOS/Linux 分别编写。 2. 日志分散在不同进程或窗口，不易于统一管理。 | 个人开发，或者团队成员都使用同一种操作系统，并且不想引入新依赖时。 |

### mac命令最终版版

```
#!/bin/bash
# Mac电脑在h5-scrm-suite根目录运行以下命令，即可一键启动乾坤
# 首次启动命令chmod +x start.sh && ./start.sh
# 后续启动命令./start.sh

# 设置一个醒目的标题
echo "🚀Starting qiankun applications...🚀"

# 配置应用列表（✅表示启动，❌表示跳过）
APPS=(
  "platform"
  "home"
  "msg-flow"
  "content-hub"
  "marketing"
  "customer"
)

printf '\\%s\n' "📋 应用列表:"
for app in "$\\{APPS[@]\\}"; do
  if [ -d "$app" ]; then
    echo "  ✅ $app"
    # 启动应用并后台运行
    (cd "$app" && yarn dev) &
  else
    echo "  ❌ $app (目录不存在)"
  fi
done

echo ""
echo "✅ 所有应用已启动! 按下 Ctrl+C 停止应用..."

# 等待所有后台任务，支持Ctrl+C终止
wait
```



### chmod +x start.sh && ./start.sh这个命令是什么意思，每次都需要执行吗，第二次能不能简化

这个命令由两部分组成，其含义和简化方法如下：

### 命令分解：

1. **`chmod +x start.sh`**
   - **作用**：给 `start.sh` 文件添加可执行权限（`+x`）。
   - **必要性**：仅当文件**首次创建或失去执行权限时**需要运行（权限修改是永久性的）。
2. **`./start.sh`**
   - **作用**：执行当前目录下的 `start.sh` 脚本文件（需要文件已有执行权限）。
3. **`&&`**
   - 表示只有前一条命令成功（即权限添加成功）后，才会执行后续命令。

------

### 是否每次都需要执行？

- 不需要

  。这是一个一次性操作和启动的组合命令：

  - `chmod +x` 只需在**第一次**运行时执行（或文件权限丢失时），后续无需重复。
  - `./start.sh` 是实际启动脚本的命令，后续每次只需运行这一部分。

------

### ✅ 第二次及以后的简化方式：

直接运行脚本（无需重复添加权限）：

```
./start.sh
```

------

### 常见问题解答：

1. **为什么第一次需要 `chmod +x`？**
    Linux 中新建文件默认无执行权限，`chmod +x` 赋予权限后才能通过 `./` 执行。
2. **如何判断是否需要 `chmod +x`？**
    运行 `ls -l start.sh`，如果输出包含 `-rw-r--r--`（无 `x`），则需添加权限。若有 `-rwxr-xr-x` 则已有权限。
3. **其他简化建议**：
   - 如果脚本路径已加入 `PATH` 环境变量，可直接通过 `start.sh` 调用（需配置，不推荐临时使用）。
   - 通过绝对路径执行（如 `/home/user/app/start.sh`），避免进入目录的步骤。

> **总结**：
>  ​**​首次运行​**​：`chmod +x start.sh && ./start.sh`
>  ​**​后续运行​**​：只需 `./start.sh`（高效无冗余）。



### 乾坤微应用，重新进入子应用，vue组件怎么监听

在乾坤微前端框架中，当重新进入子应用时，Vue组件想要监听这个事件，可以采取以下策略：

#### 使用 QianKun 生命周期钩子

乾坤微前端为子应用提供了特定的生命周期钩子，可以在这些钩子中触发自定义的监听逻辑。对于Vue组件来说，通常需要在子应用的入口文件（通常是`main.js`或类似文件）中利用这些钩子，然后通过Vue的事件总线、Vuex状态管理或props等方式将事件传递到需要监听的组件中。

#### 具体步骤：

1.在子应用入口文件中监听：
利用QianKun提供的生命周期函数，如`mount`，在这个阶段可以认为是子应用被激活或重新进入的时候。
在`mount`钩子中触发一个自定义事件或者更新全局状态（如Vuex）。

```
// 子应用入口文件
import \\{ mount \\} from '@qiankun/mount';

export async function bootstrap() \\{
 console.log('子应用：bootstrap');
\\}

export async function mount(props) \\{
 console.log('子应用：mount');
 // 触发全局事件或状态更新
 window.dispatchEvent(new Event('subAppReentered'));
 // 或者使用Vuex来更新状态
 store.commit('setSubAppStatus', 'reentered');
\\}

export async function unmount() \\{
 console.log('子应用：unmount');
\\}
```

2.Vue组件内监听：
  \- 在需要监听的Vue组件内部，你可以根据上面选择的通信方式来监听变化。
  \- 如果是全局事件，使用`mounted`钩子绑定事件监听器，并在`beforeDestroy`或`unmounted`钩子中移除。
  \- 如果是Vuex状态，使用`computed`属性结合`watch`来监听状态变化。

```
<template>
 <!-- 组件内容 -->
</template>

<script>
export default \\{
 name: 'YourComponent',
 computed: \\{
  subAppState() \\{
   return this.$store.state.subAppState;
  \\},
 \\},
 watch: \\{
  subAppState(newValue) \\{
   if (newValue === 'reentered') \\{
    console.log('子应用被重新进入');
    // 执行你的逻辑
   \\}
  \\},
 \\},
 mounted() \\{
  // 监听全局事件示例（如果使用了这种方式）
  window.addEventListener('subAppReentered', this.handleReentry);
 \\},
 beforeDestroy() \\{
  // 清理事件监听器
  window.removeEventListener('subAppReentered', this.handleReentry);
 \\},
 methods: \\{
  handleReentry() \\{
   console.log('子应用被重新进入');
   // 执行你的逻辑
  \\},
 \\},
\\};
</script>
```

这样，当子应用被重新进入时，相关组件就能通过上述机制监听到并作出响应。 



### 离开子应用后重新进入，不会触发mouted钩子，怎么解决

在Vue中，特别是使用了QianKun微前端框架的情况下，如果你发现离开子应用后重新进入时，组件的`mounted`钩子没有被触发，这可能是因为Vue为了性能考虑复用了已经创建的组件实例，而不是重新创建它们。此时，你可以利用Vue的`activated`钩子来处理这种情况。

#### 解决方案：

Vue提供了`keep-alive`组件来缓存组件实例，以避免重复渲染和优化性能。在QianKun框架中，当子应用被切换时，实际上是在管理这些缓存的组件。因此，你应该在组件内使用`activated`和`deactivated`这两个生命周期钩子来替代或补充原本的`mounted`和`destroyed`。

\- **activated**: 当组件被激活（即从不可见变为可见）时调用，这发生在组件被缓存后重新进入时。
\- **deactivated**: 当组件被停用（即从可见变为不可见）时调用。

示例代码：

```
<template>
 <div>
  <!-- 组件内容 -->
 </div>
</template>

<script>
export default \\{
 name: 'YourComponent',
 mounted() \\{
  // 首次加载时的初始化逻辑依然可以放在这里
  console.log('组件首次挂载');
 \\},
 activated() \\{
  // 当组件从非活跃状态变为活跃状态时调用，类似重新进入
  console.log('组件重新激活');
  // 在这里执行你需要在重新进入时运行的逻辑
 \\},
 deactivated() \\{
  // 当组件从活跃状态变为非活跃状态时调用，类似离开
  console.log('组件失去焦点');
  // 可以在这里清理一些资源，例如取消未完成的请求
 \\},
\\};
</script>
```

确保在你的主应用中，对于需要缓存的子应用路由或组件，使用了`<keep-alive>`包裹`<router-view>`，这样Vue才会在路由切换时复用组件实例，并触发`activated`和`deactivated`钩子。

注意事项：

\- 如果你发现即使使用了`activated`依然没有达到预期效果，请检查是否有正确配置`<keep-alive>`，以及是否所有相关的路由切换逻辑都支持这种模式。
\- 对于需要在每次进入时都执行某些初始化逻辑的情况，`activated`是最佳选择。而对于只需在第一次加载时执行的逻辑，则应继续使用`mounted`。 



### window.history.pushState页面跳转问题

http://localhost:8086/front/h5-content-hub/detail?id=2535&agentId=1000138&appId=wxee4c15650f2ab0db&browser=true&code=fV8rDIGl0JZgWP_9_CXa9aLWTge0dtc-bSbdlnIetak&state=redirect

http://localhost:8080/front/scrm/content-hub/detail?id=2535

这两个链接都同一个详情页，都使用代码

```
const toUrl=`/front/scrm/msg-flow/group-send/create?source=contentHub&id=$\\{shareItem.value.id\\}`
navigateTo(toUrl)\\{
window.history.pushState(
          \\{\\},
          '',
          url
        )
\\}
```

跳转，但第一个跳转不成功，为什么，怎么通过代码解决
改造navigateTo方法可以通过当前页面链接中/front/scrm判断，如果是，toUrl就使用window.history.pushState跳转，如果不是就使用window.location.href跳转

#### 回答

由于 `window.history.pushState` 只在同源策略下有效，即协议、域名和端口必须相同，当尝试从 `http://localhost:8086` 跳转到 `http://localhost:8080` 时，尽管都在 `localhost` 上，但不同的端口被视为不同的源，因此 `pushState` 无法实现页面跳转。对于第一个链接来说，尝试使用 `pushState` 跳转到第二个链接是无效的，因为它试图跨域修改历史记录。

要解决这个问题，你可以根据当前页面的路径前缀来决定使用 `pushState` 还是 `location.href`。

```
function navigateTo(toUrl) \\{
  // 创建URL对象，以便解析和比较
  const currentUrl = new URL(window.location.href)
  const targetUrl = new URL(toUrl, currentUrl)
  console.log('工作台通用跳转', currentUrl, targetUrl)
  if (targetUrl.origin === currentUrl.origin) \\{
    // 如果目标URL和当前URL的源相同
    // 当前页面路径是否以'/front/scrm/'开始（是否工作台）
    const isScrmPath = currentUrl.pathname.startsWith('/front/scrm/')

    if (isScrmPath) \\{
      // 工作台
      window.history.pushState(\\{\\}, '', targetUrl.href)
    \\} else \\{
      // 单体页，进行完全重定向
      window.location.href = targetUrl.href
    \\}
  \\} else \\{
    // 如果目标URL和当前URL的源不同，进行完全重定向
    window.location.href = targetUrl.href
  \\}
\\}
```



### ElMessage在qiankun框架中不显示 

`<el-config-provider :locale="zhCn" namespace="csc">`导致

在 qiankun 微前端框架中使用 `ElConfigProvider` 可能会影响到 `ElMessage` 的显示，这是因为 `ElMessage` 作为一个全局组件，其样式和行为可能受到配置提供者的影响，尤其是在不同微应用间共享全局状态时。

`ElConfigProvider` 的主要作用是提供 Element UI 的配置项，包括但不限于主题、国际化设置等。当你在微应用中使用 `ElConfigProvider` 时，它可能会覆盖主应用或其他微应用的配置，导致样式或行为不一致。

若 `ElMessage` 在 qiankun 中不显示，可以尝试以下几种解决方案：

1. **将 `ElConfigProvider` 移至主应用中**:
   将 `ElConfigProvider` 的配置移到主应用中，确保所有微应用共享同一套配置。这样可以避免配置冲突，并确保 `ElMessage` 的显示不受微应用边界的影响。

   主应用中使用 `ElConfigProvider` 的示例：

   ```html
   <template>
     <el-config-provider :locale="zhCn" namespace="csc">
       <!-- 主应用的其他内容 -->
       <router-view></router-view>
     </el-config-provider>
   </template>
   
   <script>
   import zhCn from 'element-plus/lib/locale/lang/zh-cn';
   export default \\{
     data() \\{
       return \\{
         zhCn,
       \\};
     \\},
   \\};
   </script>
   ```

2. **使用微应用级别的 `ElMessage` 配置**:
   如果你需要在每个微应用中都有不同的配置，你可以在微应用中局部地使用 `ElConfigProvider`，但要确保 `ElMessage` 的根节点位于微应用的容器之外，或者在微应用的生命周期中正确处理 `ElMessage` 的显示和销毁。

3. **利用 qiankun 的通信机制**:
   利用 qiankun 提供的通信机制（如事件总线），在微应用中触发主应用中的 `ElMessage`。这样可以避免样式和配置的冲突，同时确保消息提示的显示不受微应用边界的限制。

   微应用中触发主应用 `ElMessage` 的示例：

   ```javascript
   window.microApp.dispatch('showMessage', message);
   ```

   主应用中监听并显示 `ElMessage` 的示例：

   ```javascript
   window.microApp.on('showMessage', message => \\{
     this.$message(\\{
       message,
       type: 'success',
     \\});
   \\});
   ```

请根据你的项目结构和具体需求选择合适的解决方案。如果问题仍未解决，建议检查 qiankun 和 Element UI 的官方文档，或者在相关社区和论坛寻求帮助。



### element-plus 自定义命名空间 el-config-provider namespace 不起作用，html 的class值改变了，但是样式不对

今天按照文档，对elemen plus + vite 的项目，进行qiankun嵌套，发现子应用的element和主应用的element plus样式冲突，所以决定用element plus 的自定义命名空间处理下。
使用方法，按照文档来
第一步：vue文件内部添加自定义命名空间标签，自定义命名 ep

```
<template>
  <el-config-provider namespace="ep">
    <!-- ... -->
  </el-config-provider>
</template>
```


第二步：修改 namespace的变量值，将下面的代码，添加到你的文件内部

```
@forward 'element-plus/theme-chalk/src/mixins/config.scss' with (
  $namespace: 'ep'
);
```


第三步：将sass文件引入

```
import \\{ defineConfig \\} from 'vite'
// https://vitejs.dev/config/
export default defineConfig(\\{
  // ...
  css: \\{
    preprocessorOptions: \\{
      scss: \\{
        additionalData: `@use "~/styles/element/index.scss" as *;`,
      \\},
    \\},
  \\},
  // ...
\\})
```

文档到此结束。就是个大坑，结果就是，html变了，但是element css 的文件还是el-开头的，
所以还需要：替换element css 文件引入路径，我是再main.ts内引入的。

文档到此结束。就是个大坑，结果就是，html变了，但是element css 的文件还是el-开头的，
所以还需要：替换element css 文件引入路径，我是再main.ts内引入的。

```
import 'element-plus/theme-chalk/src/index.scss'
```

到此，算是成功了。
如果报错，math.div之类的，那就是sass版本太低了，更新下，升级下就好了。

原文链接：https://blog.csdn.net/qq_34164814/article/details/139329167



### 乾坤两个子应用怎么方便传递数据

在乾坤（qiankun）微前端框架中，两个子应用之间传递数据有几种常用的方式。以下是几种推荐的方法：

1. **全局状态管理**：
   - 使用`initGlobalState`创建一个全局状态容器，通过`setGlobalState`方法来设置全局状态，并且子应用可以通过`onGlobalStateChange`监听全局状态的变化。
   - 这种方式非常适合需要共享和同步的数据，比如用户登录信息、主题配置等。

2. **props 传递**：
   - 在注册子应用时，可以通过`registerMicroApps`的`props`参数给子应用传递数据。
   - 这个方法适合于主应用向子应用传递启动时所需的配置或参数。

3. **PostMessage API**：
   - qiankun 支持使用浏览器原生的`postMessage`API进行跨窗口通信。这对于子应用之间的直接通信特别有用。
   - 子应用可以使用`window.parent.postMessage()`发送消息到主应用或其他子应用，接收方可以通过监听`window.addEventListener('message', callback)`来获取这些消息。

4. **事件总线（Event Bus）**：
   - 创建一个简单的事件发布/订阅系统，或者使用现有的库如`mitt`或`tiny-emitter`。
   - 主应用和子应用都可以订阅感兴趣的事件，并在需要时发布事件通知其他应用。

5. **LocalStorage/SessionStorage**：
   - 虽然不是最优雅的解决方案，但在某些情况下可以考虑使用`localStorage`或`sessionStorage`存储共享数据。
   - 注意这种方式不适合敏感数据，并且需要处理好数据的一致性和更新问题。

6. **URL 参数**：
   - 如果数据量不大，也可以考虑通过URL参数来传递数据。
   - 当用户导航到特定页面时，可以在URL中附加查询参数，子应用加载时解析这些参数。

7. **自定义 API 或服务**：
   - 构建一套RESTful API或GraphQL服务，让子应用通过HTTP请求相互交换数据。
   - 这种方法适用于更复杂的应用场景，特别是当数据需要持久化或涉及到后端逻辑时。

根据你的具体需求选择合适的数据传递方式。对于两个子应用之间的实时通信，`postMessage`和全局状态管理可能是最方便的选择；而对于启动时的一次性配置，则可以考虑使用`props`传递。

#### 使用`sessionStorage`

来在子应用之间传递数据是可行的，特别是在你只需要在浏览器会话期间保持数据并且不介意这些数据对用户可见的情况下。不过需要注意的是，`sessionStorage`有其局限性，比如它不适合处理大型对象或敏感信息，并且当页面刷新或关闭时数据会被清除。

下面是一个简单的封装方法，可以帮助你在子应用之间通过`sessionStorage`安全地存储和读取业务数据：

##### 封装 `sessionStorage` 的工具函数

```javascript
class SessionStorageHelper \\{
  constructor(namespace = 'default') \\{
    this.namespace = namespace;
  \\}

  /**
   * 设置数据到 sessionStorage 中
   * @param \\{string\\} key - 数据键名
   * @param \\{*\\} value - 要存储的数据值
   */
  setItem(key, value) \\{
    try \\{
      const stringifiedValue = JSON.stringify(value);
      sessionStorage.setItem(`$\\{this.namespace\\}:$\\{key\\}`, stringifiedValue);
    \\} catch (error) \\{
      console.error('Failed to set item in sessionStorage:', error);
    \\}
  \\}

  /**
   * 从 sessionStorage 中获取数据
   * @param \\{string\\} key - 数据键名
   * @returns \\{*\\} 存储的数据值
   */
  getItem(key) \\{
    try \\{
      const item = sessionStorage.getItem(`$\\{this.namespace\\}:$\\{key\\}`);
      return item ? JSON.parse(item) : null;
    \\} catch (error) \\{
      console.error('Failed to get item from sessionStorage:', error);
      return null;
    \\}
  \\}

  /**
   * 移除指定键名的数据
   * @param \\{string\\} key - 数据键名
   */
  removeItem(key) \\{
    sessionStorage.removeItem(`$\\{this.namespace\\}:$\\{key\\}`);
  \\}

  /**
   * 清空所有以命名空间为前缀的数据
   */
  clearNamespace() \\{
    Object.keys(sessionStorage)
      .filter(key => key.startsWith(`$\\{this.namespace\\}:`))
      .forEach(key => sessionStorage.removeItem(key));
  \\}
\\}

// 使用示例
const storageHelper = new SessionStorageHelper('productInfo');

// 设置产品信息
storageHelper.setItem('currentProduct', \\{
  productName: item.prdName,
  productCode: item.prdCode,
  productType: item.prdType
\\});

// 获取产品信息
const productInfo = storageHelper.getItem('currentProduct');
console.log(productInfo);

// 在跳转之前确保清理不再需要的数据
// storageHelper.clearNamespace();
```

### 注意事项

1. **命名空间**：为了避免不同部分的代码之间的键冲突，建议为每个数据类别定义一个唯一的命名空间（如上例中的`'productInfo'`）。
2. **序列化/反序列化**：因为`sessionStorage`只能存储字符串，所以我们使用`JSON.stringify`和`JSON.parse`来处理复杂的数据类型。
3. **错误处理**：考虑到可能发生的异常情况，比如超过存储限制或浏览器禁用`sessionStorage`，我们在设置和获取数据时加入了基本的错误捕捉。
4. **安全性**：不要将敏感信息存入`sessionStorage`，因为它可以通过JavaScript访问，存在被恶意脚本读取的风险。
5. **生命周期**：记住`sessionStorage`的数据会在浏览器标签页关闭后丢失。如果你需要更持久的存储，请考虑使用`localStorage`，但要注意`localStorage`也有自己的限制和风险。

这个封装后的工具类可以简化你在项目中使用`sessionStorage`的方式，同时提供了一些额外的功能来确保代码的健壮性和可维护性。



### 获取后移除session

```
// 获取后移除session
export const getOnceSession = (key) => \\{
  const data = sessionStorage.getItem(key)
  if (data) \\{
    sessionStorage.removeItem(key)
    return JSON.parse(data)
  \\}
  return null
\\}
```

