---
title: 浏览器调试
date: 2021-03-13 10:10:10
categories: 
- 前端知识
tags:
- 浏览器
---

### 知道什么是 webkit 么? 知道怎么用浏览器的各种工具来调试和 debug 代码么?

Webkit 是浏览器引擎，包括 html 渲染和 js 解析功能，手机浏览器的主流内核，与之相对应的引擎有 Gecko（Mozilla Firefox 等使用）和 Trident（也称 MSHTML，IE 使用）。
对于浏览器的调试工具要熟练使用，主要是页面结构分析，后台请求信息查看，js 调试工具使用，熟练使用这些工具可以快速提高解决问题的效率



### 企业微信开启调试模式

启动后按快捷键 ctrl+alt+shift+D进入调试模式



# 浏览器调试技巧

### 开启Chrome Dev Tools

1. 打开方式
   1. `F12`
   2. 右键-检查



### 命令菜单

1. 打开方式
   1. windows快捷键：`Ctrl`+`Shift`+`P`
   2. mac快捷键：`Command`+`Shift`+`P`
2. 使用
   1. 截屏
      1. `Capture area screenshot`（区域截屏）
      2. `Capture full size screenshot`（全屏长图截屏）
      3. `Capture node screenshot`（node节点截屏）
      4. `Capture screenshot`(全屏截图)



### 常用的面板

### Element

1. css调试
   1. 查看元素：点击![image.png](https://cdn.nlark.com/yuque/0/2022/png/28267569/1669454695325-62ec8677-1a34-41d5-932a-004f498b9c01.png#averageHue=\\%23e9ebec&clientId=u9ef9bbfc-180d-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=19&id=u27b711c3&margin=\\%5Bobject\\%20Object\\%5D&name=image.png&originHeight=24&originWidth=27&originalType=binary&ratio=1&rotation=0&showTitle=false&size=439&status=done&style=none&taskId=ue1c198bd-0669-4211-a9cb-0458f45c349&title=&width=21.6)，选中元素后，蓝色代表本体，绿色代表`padding`, 橙色代表`margin`
   2. 查看页面在不同设备上的展示情况：点击![image.png](https://cdn.nlark.com/yuque/0/2022/png/28267569/1669454824373-2cf3f0b2-1628-47c6-88ed-2fca5c1d7668.png#averageHue=\\%23ebedee&clientId=u9ef9bbfc-180d-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=22&id=uf4863f95&margin=\\%5Bobject\\%20Object\\%5D&name=image.png&originHeight=28&originWidth=30&originalType=binary&ratio=1&rotation=0&showTitle=false&size=323&status=done&style=none&taskId=u734936b0-1d2e-45ec-821e-17fb1d4b6b3&title=&width=24)，可以选择不同设备型号，横屏竖屏等
2. 查询Dom树
   1. 打开方式：
      1. windows快捷键：`Ctrl`+`F`
      2. mac快捷键：`Command`+`F`
   2. 使用![image.png](https://cdn.nlark.com/yuque/0/2022/png/28267569/1669455688773-2730ce46-9a00-41c8-ab66-392e722e92e5.png#averageHue=\\%23f2f2f2&clientId=u9ef9bbfc-180d-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=22&id=ueda50bda&margin=\\%5Bobject\\%20Object\\%5D&name=image.png&originHeight=28&originWidth=226&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1889&status=done&style=none&taskId=u8d92a148-1aee-471e-bac2-393fc432e1e&title=&width=180.8)
      1. 文本查询：直接输入文本
      2. css选择器查询：例如查询用到了类card的元素：直接输入`.card`
      3. XPath

补充：在console面板下用`inspect(element)`方法也能快速定位元素
例如：`inspect(document.getElementById('card'))`

3. style(样式编辑)
   1. 选中元素后可直接给元素添加样式
   2. 让元素保持某些状态![image.png](https://cdn.nlark.com/yuque/0/2022/png/28267569/1669463735711-3c76b41e-a87c-4a97-a4ab-f57df121f4c0.png#averageHue=\\%23e6e9ed&clientId=u9ef9bbfc-180d-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=19&id=u0f199267&margin=\\%5Bobject\\%20Object\\%5D&name=image.png&originHeight=24&originWidth=45&originalType=binary&ratio=1&rotation=0&showTitle=false&size=649&status=done&style=none&taskId=udf18a67c-8bd5-4262-aa86-b1816f05d1f&title=&width=36)
   3. 让元素去除某些类![image.png](https://cdn.nlark.com/yuque/0/2022/png/28267569/1669463782681-ef39c65f-567a-4d30-9a5d-ad71e8a47808.png#averageHue=\\%23e4e7ea&clientId=u9ef9bbfc-180d-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=18&id=u8848ae48&margin=\\%5Bobject\\%20Object\\%5D&name=image.png&originHeight=22&originWidth=41&originalType=binary&ratio=1&rotation=0&showTitle=false&size=505&status=done&style=none&taskId=ua6a27e65-0388-4c86-a2ca-b0953dbe9fb&title=&width=32.8)
4. 颜色选择器![image.png](https://cdn.nlark.com/yuque/0/2022/png/28267569/1669546568408-2b34929c-65ce-42fa-9166-bd036cd0653e.png#averageHue=\\%23e3e3e3&clientId=u9ef9bbfc-180d-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=18&id=u3a60157c&margin=\\%5Bobject\\%20Object\\%5D&name=image.png&originHeight=22&originWidth=26&originalType=binary&ratio=1&rotation=0&showTitle=false&size=466&status=done&style=none&taskId=u7a1cb49c-a7de-4d79-8d48-27275ed573c&title=&width=20.8)
5. computed
   1. 快速定位到某些样式的使用元素的位置
6. Layout
   1. 观察grid和felx布局



### Console

1. 可以直接执行语句
2. `$_`返回上一条语句的执行结果
3. `$0`返回上一个选择的dom节点
4. `$`代替`document.querySelector`，querySelector() 方法返回指定 CSS 选择器的一个元素。
5. `$$`代替`document.querySelectorAll`，querySelectorAll() 方法返回指定 CSS 选择器的所有元素，返回 [NodeList](https://www.runoob.com/js/js-htmldom-nodelist.html) 对象。
6. console.log/error/warn/table/clear/group/time/assert/trace
```javascript
// 1.使用 \\{ 变量 \\} 来显示其名称和值
let num = 8;
console.log("num",num)
console.log(\\{num\\})

// 2.console区分信息类型进行打印
console.info('我是一条提示信息');
console.warn('我是一条警告信息');
console.error('我是一条错误信息');
console.debug('我是一条debug调试信息');

//3.console.table() 可以以更友好的格式输出对象值
//对象
const obj = \\{
    propA: 1,
    propB: 2,
    propC: 3
  \\};

console.table( obj );
//二维数组
const arr1 = [
    [ 1, 2, 3 ],
    [ 4, 5, 6 ],
    [ 7, 8, 9 ]
  ];

console.table( arr1 );

//对象数组
const arr2 = [
    \\{ a: 1, b: 2, c: 3 \\},
    \\{ a: 4, b: 5, c: 6 \\},
    \\{ a: 7, b: 8, c: 9 \\}
  ];

console.table( arr2 );

//4.性能计时器console.time
// start timer
console.time('looptimer');

for (let i = 999999999; i > 0; i--);

// show elapsed time
console.timeEnd('looptimer');
```

7. 打印筛选![image.png](https://cdn.nlark.com/yuque/0/2022/png/28267569/1669533759661-a42f61a8-bad4-4616-be34-7f9da8cfd248.png#averageHue=\\%23e2e4e6&clientId=u9ef9bbfc-180d-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=26&id=ub3bdf4e0&margin=\\%5Bobject\\%20Object\\%5D&name=image.png&originHeight=33&originWidth=126&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1063&status=done&style=none&taskId=ufbc5a38f-41b7-4cab-a746-21d0fa25fe1&title=&width=100.8)
8. 观察变量![image.png](https://cdn.nlark.com/yuque/0/2022/png/28267569/1669533890821-63bc2f7a-6ae8-4b0f-8b96-0c473b924ae3.png#averageHue=\\%23eceeef&clientId=u9ef9bbfc-180d-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=23&id=u2739017c&margin=\\%5Bobject\\%20Object\\%5D&name=image.png&originHeight=29&originWidth=48&originalType=binary&ratio=1&rotation=0&showTitle=false&size=747&status=done&style=none&taskId=ua201ae79-159c-4afc-b84a-c25f6c6f31c&title=&width=38.4)
9. 编辑页面`document.body.contentEditable="true"`



### console对象方法

| 属性    | 参数      | 返回值    | 功能                                              | 兼容性 |
| ------- | --------- | --------- | ------------------------------------------------- | ------ |
| log     | msg       | undefined | 向 Web 控制台输出一条消息                         | 全部   |
| **dir** | object    | undefined | **打印出对象的所有属性和属性值**                  | >ie8   |
| error   | msg       | undefined | 向 Web 控制台输出一条错误消息                     | >ie7   |
| warn    | msg       | undefined | 向 Web 控制台输出一条警告信息                     | >ie7   |
| time    | timerName | undefined | 启动一个计时器（timer）来跟踪某一个操作的占用时长 | >ie10  |
| timeEnd | timerName | undefined | 停止一个通过 `console.time()` 启动的计时器        | >ie10  |

`console` 对象并不属于 BOM (Browser Object Model)，而是属于 Web API 的一部分。BOM 是指浏览器对象模型，它提供了一些可以与浏览器窗口进行交互的对象，比如 `window`, `navigator`, `screen` 等等。

`console` 对象是 JavaScript 中用来访问浏览器的调试控制台的一个接口。它主要用于输出调试信息，比如使用 `console.log()` 来打印信息到控制台。虽然 `console` 通常在浏览器环境中可用，并且对前端开发者非常有用，但它并不是直接由 BOM 定义的，而是 Web APIs 中的一部分，这些API是由浏览器厂商实现并遵循Web标准来提供的。

Web APIs 包括了 DOM (Document Object Model)、BOM 和其他一些特定的功能接口，如 `fetch` API, `XMLHttpRequest`, `Web Storage` API, 以及 `console` API 等等。因此，当你在浏览器中使用 `console` 对象时，实际上是在利用 Web API 提供的功能。



### Source

1. 调试
   1. 对事件进行断点调试
      1. 如果普通代码可直接调试
      2. 如果代码用了框架，可以在![image.png](https://cdn.nlark.com/yuque/0/2022/png/28267569/1669535530587-d64288df-e4d2-471a-8d10-71d572591c8f.png#averageHue=\\%23e4e6e7&clientId=u9ef9bbfc-180d-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=20&id=uf0ec124d&margin=\\%5Bobject\\%20Object\\%5D&name=image.png&originHeight=25&originWidth=149&originalType=binary&ratio=1&rotation=0&showTitle=false&size=999&status=done&style=none&taskId=uf8633e2f-beeb-4c7e-bfc8-a5e7d08bff9&title=&width=119.2)中，右键点击，选择![image.png](https://cdn.nlark.com/yuque/0/2022/png/28267569/1669535591631-14b31053-0392-4b78-99fe-f6a590b1eac4.png#averageHue=\\%23fdfaf6&clientId=u9ef9bbfc-180d-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=21&id=uc0b9f8ef&margin=\\%5Bobject\\%20Object\\%5D&name=image.png&originHeight=26&originWidth=186&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1394&status=done&style=none&taskId=uc974304c-7757-4705-82bc-924d80ede7a&title=&width=148.8)去忽视框架，调试我们自己的代码
   2. 直接在代码中写上`debugger`
   3. 在代码中打断点
      1. ![image.png](https://cdn.nlark.com/yuque/0/2022/png/28267569/1669534581150-615a76c8-c76b-4e34-9c0e-5ff6c46aca03.png#averageHue=\\%23ebedee&clientId=u9ef9bbfc-180d-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=18&id=AbwwU&margin=\\%5Bobject\\%20Object\\%5D&name=image.png&originHeight=23&originWidth=256&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1452&status=done&style=none&taskId=u05e8171d-d893-4316-b74f-db502ee7851&title=&width=204.8)可以单独观察某个变量
   4. 按钮
      1. ![image.png](https://cdn.nlark.com/yuque/0/2022/png/28267569/1669963859236-a7af78b5-0711-458d-9f1e-4225d99821e3.png#averageHue=\\%23ccdcf1&clientId=u85a2b026-58ce-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=19&id=qvWWE&margin=\\%5Bobject\\%20Object\\%5D&name=image.png&originHeight=24&originWidth=27&originalType=binary&ratio=1&rotation=0&showTitle=false&size=346&status=done&style=none&taskId=u55070950-cf56-4151-ba72-1ed92f77bf2&title=&width=21.6)从一个断点跳转到另一个断点
      2. ![image.png](https://cdn.nlark.com/yuque/0/2022/png/28267569/1669963895458-de75618f-e323-411f-94da-0050b2622261.png#averageHue=\\%23cccecf&clientId=u85a2b026-58ce-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=19&id=ue99ff377&margin=\\%5Bobject\\%20Object\\%5D&name=image.png&originHeight=24&originWidth=27&originalType=binary&ratio=1&rotation=0&showTitle=false&size=620&status=done&style=none&taskId=u925cbe20-6fc9-40ee-9542-07fc8a5c3b3&title=&width=21.6)执行代码时跳过一些代码
      3. ![image.png](https://cdn.nlark.com/yuque/0/2022/png/28267569/1669963918674-f6a14dd2-ff67-415c-ba15-f04894e52424.png#averageHue=\\%23eceeef&clientId=u85a2b026-58ce-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=18&id=u674e498e&margin=\\%5Bobject\\%20Object\\%5D&name=image.png&originHeight=23&originWidth=28&originalType=binary&ratio=1&rotation=0&showTitle=false&size=365&status=done&style=none&taskId=u8cf480dc-f68c-4dab-8b7d-09269365f8f&title=&width=22.4)进入函数内部并进行调试
      4. ![image.png](https://cdn.nlark.com/yuque/0/2022/png/28267569/1669963941595-808fda79-b63d-451b-a8cb-7b83464e2081.png#averageHue=\\%23e9ebec&clientId=u85a2b026-58ce-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=18&id=u91c7ac92&margin=\\%5Bobject\\%20Object\\%5D&name=image.png&originHeight=23&originWidth=17&originalType=binary&ratio=1&rotation=0&showTitle=false&size=363&status=done&style=none&taskId=u235fb85c-60f8-4c4d-aa08-2ade17b20b4&title=&width=13.6)跳出函数内部
      5. ![image.png](https://cdn.nlark.com/yuque/0/2022/png/28267569/1669964327863-bc416b6e-f8d1-4345-9187-09364e4ea655.png#averageHue=\\%23eceeef&clientId=u85a2b026-58ce-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=14&id=u684f2e3f&margin=\\%5Bobject\\%20Object\\%5D&name=image.png&originHeight=18&originWidth=26&originalType=binary&ratio=1&rotation=0&showTitle=false&size=348&status=done&style=none&taskId=u9cceea58-ea09-4b90-9eb3-a8d51f821ff&title=&width=20.8)逐行执行，如果中途有函数调用，单步执行也会进入函数内部，逐行执行，然后退出
   5. ![image.png](https://cdn.nlark.com/yuque/0/2022/png/28267569/1669546363756-26e95a45-0ade-44d2-bbde-58bd85732ff3.png#averageHue=\\%23eceeef&clientId=u9ef9bbfc-180d-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=19&id=uf4e4fef5&margin=\\%5Bobject\\%20Object\\%5D&name=image.png&originHeight=24&originWidth=37&originalType=binary&ratio=1&rotation=0&showTitle=false&size=599&status=done&style=none&taskId=ub847758b-fffd-436d-9259-d8244ab469f&title=&width=29.6)代码格式化



### Network

1. 使用
   1. ![image.png](https://cdn.nlark.com/yuque/0/2022/png/28267569/1669535922189-c8e39209-aebf-4371-b1dd-6e86e88109d5.png#averageHue=\\%23e9b4b1&clientId=u9ef9bbfc-180d-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=21&id=u090345b4&margin=\\%5Bobject\\%20Object\\%5D&name=image.png&originHeight=26&originWidth=25&originalType=binary&ratio=1&rotation=0&showTitle=false&size=692&status=done&style=none&taskId=u5823bc4a-edc4-4003-8dc7-7936aba2738&title=&width=20)停止对请求的监控
   2. ![image.png](https://cdn.nlark.com/yuque/0/2022/png/28267569/1669535963564-63b3485d-0a16-4550-98a2-50c1cc515b05.png#averageHue=\\%23e9ebec&clientId=u9ef9bbfc-180d-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=22&id=u597a5f88&margin=\\%5Bobject\\%20Object\\%5D&name=image.png&originHeight=27&originWidth=28&originalType=binary&ratio=1&rotation=0&showTitle=false&size=523&status=done&style=none&taskId=ua843289c-56b6-473e-8743-0473bca4717&title=&width=22.4)清空列表
   3. ![image.png](https://cdn.nlark.com/yuque/0/2022/png/28267569/1669536095661-14366a7b-b80e-4fde-8da3-a30654aab7c8.png#averageHue=\\%23edd5d5&clientId=u9ef9bbfc-180d-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=19&id=ue7590dbc&margin=\\%5Bobject\\%20Object\\%5D&name=image.png&originHeight=24&originWidth=32&originalType=binary&ratio=1&rotation=0&showTitle=false&size=494&status=done&style=none&taskId=ufb9eb41a-d90e-45ad-82fb-08e30b43320&title=&width=25.6)筛选
   4. ![image.png](https://cdn.nlark.com/yuque/0/2022/png/28267569/1669536297629-816e090f-8369-4c1f-a250-4ea4eb89424a.png#averageHue=\\%23e8eaeb&clientId=u9ef9bbfc-180d-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=26&id=ubb88f153&margin=\\%5Bobject\\%20Object\\%5D&name=image.png&originHeight=32&originWidth=129&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1162&status=done&style=none&taskId=u451e4321-3514-4554-9ba3-554f6951810&title=&width=103.2)保持历史请求的打印
   5. ![image.png](https://cdn.nlark.com/yuque/0/2022/png/28267569/1669536419839-f759a479-2c01-4407-9310-1bc16e34f498.png#averageHue=\\%23d5d8dd&clientId=u9ef9bbfc-180d-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=22&id=u93dde90a&margin=\\%5Bobject\\%20Object\\%5D&name=image.png&originHeight=28&originWidth=131&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1101&status=done&style=none&taskId=u7ccfd52d-9e23-4cd1-b130-e9d27e8e986&title=&width=104.8)节流器，模拟不同网络下网页加载情况
   6. ![image.png](https://cdn.nlark.com/yuque/0/2022/png/28267569/1669536860677-fcf1f7b2-53c6-4bc0-9f99-6db6178e52c0.png#averageHue=\\%23d6d8da&clientId=u9ef9bbfc-180d-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=18&id=ufe64deed&margin=\\%5Bobject\\%20Object\\%5D&name=image.png&originHeight=23&originWidth=27&originalType=binary&ratio=1&rotation=0&showTitle=false&size=658&status=done&style=none&taskId=u8149495a-86d2-4f30-a715-d49143af54c&title=&width=21.6)比较常用来配置`user agent`
   7. ![image.png](https://cdn.nlark.com/yuque/0/2022/png/28267569/1669537124672-7ced5a42-dee5-4b10-a803-a6cfb26de68c.png#averageHue=\\%23eceeef&clientId=u9ef9bbfc-180d-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=22&id=u8bcfe3c5&margin=\\%5Bobject\\%20Object\\%5D&name=image.png&originHeight=28&originWidth=61&originalType=binary&ratio=1&rotation=0&showTitle=false&size=519&status=done&style=none&taskId=u599e9644-e3da-4bf0-9b28-d02dce9535f&title=&width=48.8)场景复现
   8. 联调或修BUG时，发送 XHR 请求，在请求上点击鼠标右键，选择![image.png](https://cdn.nlark.com/yuque/0/2022/png/28267569/1669548089035-758dd06a-a905-43cc-ba31-1e51452ab718.png#averageHue=\\%23fdfaf7&clientId=u9ef9bbfc-180d-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=21&id=u26061787&margin=\\%5Bobject\\%20Object\\%5D&name=image.png&originHeight=26&originWidth=125&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1047&status=done&style=none&taskId=u78ff8428-eafe-4028-916f-4bdaa1f3258&title=&width=100)
   9. 联调或修BUG时，针对同样的请求，有时候需要修改入参重新发起，在请求上点击鼠标右键，选择`Copy as fetch`，控制台粘贴代码，修改参数，回车搞定。







# 调试器（`debugger`）的详细介绍

以下是关于调试器（`debugger`）的详细介绍及其在 JavaScript 和 Vue3 中的具体使用指南，结合核心概念、实践方法和注意事项整理而成：

------

### 🔧 **一、`debugger` 的作用与原理**

1. **核心功能**
   - **暂停执行**：当代码执行到 `debugger` 语句时，浏览器会暂停运行（需打开开发者工具），进入调试模式。
   - **上下文检查**：可查看当前作用域的变量、闭包、调用栈（Call Stack）、事件监听器等。
   - **流程控制**：支持单步执行（Step Over/Into/Out）、断点跳转等操作。
2. **实现原理**
   - **浏览器引擎**（如 V8）：检测到 `debugger` 关键字时，通过调试协议（如 Chrome DevTools Protocol）与开发者工具通信，暂停脚本执行。
   - **依赖条件**：仅在开发者工具开启时生效，否则被忽略。

------

### ⚙️ **二、JavaScript 中的使用示例**

#### **场景 1：基础调试**

```
function calculateSum(a, b) \\{
  const sum = a + b;
  debugger; // 此处暂停
  return sum;
\\}
console.log(calculateSum(2, 3)); // 执行时触发断点
```

**操作步骤**：

1. 浏览器中按 `F12` → 打开 **Sources** 面板。
2. 刷新页面，代码暂停在 `debugger` 处。
3. 在 **Scope** 面板查看 `a`、`b`、`sum` 的值。

#### **场景 2：异步代码调试**

```
setTimeout(() => \\{
  const data = \\{ id: 1, name: "Test" \\};
  debugger; // 在回调中暂停
  console.log(data);
\\}, 1000);
```

**优势**：解决异步逻辑难以追踪的问题，直接进入回调上下文。

#### **场景 3：循环中的条件断点**

```
for (let i = 0; i < 10; i++) \\{
  if (i === 5) \\{
    debugger; // 仅当 i=5 时暂停
  \\}
\\}
```

------

### 🖥️ **三、Vue3 中的使用示例**

#### **场景 1：调试组件生命周期**

```
<script setup>
import \\{ onMounted \\} from 'vue';

onMounted(() => \\{
  const message = "组件已挂载";
  debugger; // 检查挂载后的状态
\\});
</script>
```

**检查内容**：

- 组件 `data`、`props` 的初始值。
- DOM 是否渲染完成（通过 **Elements** 面板验证）。

#### **场景 2：响应式数据更新**

```
<script setup>
import \\{ ref \\} from 'vue';

const count = ref(0);

const increment = () => \\{
  count.value++;
  debugger; // 检查更新后的 count 值
\\};
</script>
```

**关键操作**：

1. 在 **Vue Devtools** 中观察 `count` 的变化。
2. 在 **Sources** 面板查看响应式依赖是否触发。

#### **场景 3：事件处理逻辑**

```
<script setup>
const handleClick = (event) => \\{
  debugger; // 检查事件对象
  console.log(event.target);
\\};
</script>

<template>
  <button @click="handleClick">点击</button>
</template>
```

------

### 🛠️ **四、调试工具与进阶技巧**

1. **浏览器开发者工具**

   - 快捷键：
     - `F8`：继续执行。
     - `F10`：单步跳过（Step Over）。
     - `F11`：单步进入（Step Into）。
   - **条件断点**：右键点击行号 → 设置条件（如 `count > 5`）。

2. **VS Code 集成调试**
    ​**​配置 `.vscode/launch.json`​**​：

   ```
   \\{
     "type": "chrome",
     "request": "launch",
     "url": "http://localhost:5173", // Vue 开发服务器地址
     "webRoot": "$\\{workspaceFolder\\}",
     "sourceMapPathOverrides": \\{
       "webpack:///src/*": "$\\{workspaceFolder\\}/src/*" // 确保源码映射正确
     \\}
   \\}
   ```

   **操作**：按 `F5` 启动调试，直接关联源码断点。

3. **Vue Devtools**

   - 可视化检查组件树、状态、事件。
   - 时间旅行调试：回溯状态变化历史。

------

### ⚠️ **五、注意事项**

1. **生产环境必须移除**

   - **风险**：未移除的 `debugger` 会导致应用暂停，影响用户体验。

   - 解决方案：

     - 使用构建工具（如 Webpack）在打包时自动移除（配置 `TerserPlugin`）。

     - 通过环境变量控制：

       ```
       if (process.env.NODE_ENV === 'development') \\{
         debugger; // 仅开发环境生效
       \\}
       ```

2. **替代方案**

   - **浏览器原生断点**：在 **Sources** 面板直接设置断点（无需修改代码）。
   - **日志调试**：`console.log` 快速验证（但缺乏上下文跟踪能力）。

3. **调试异步代码**

   - 在 `Promise`/`async/await` 回调内部使用 `debugger`。
   - 使用 **XHR Breakpoints** 拦截特定网络请求（Chrome 的 **Sources** 面板）。

------

### 💡 **六、最佳实践**

- **精准定位**：在复杂逻辑（如递归函数、深层嵌套对象操作）中插入 `debugger`。
- 结合工具链：
  - 开发阶段：`debugger` + Vue Devtools + 浏览器断点。
  - 生产环境：使用 **Sentry** 等错误监控工具捕获异常。
- **性能优化**：避免在循环中频繁触发 `debugger`，改用条件断点。

------

### 📊 **七、常见问题解决**

| 问题                 | 解决方案                                                     |
| -------------------- | ------------------------------------------------------------ |
| 断点未生效           | 确保开发者工具已打开；禁用浏览器缓存。                       |
| 源码映射失败         | 在 `vue.config.js` 中配置 `devtool: 'source-map'`。          |
| Vue 响应式数据未更新 | 在 `debugger` 暂停时，检查依赖追踪是否丢失（通过 Vue Devtools）。 |

------

通过灵活运用 `debugger` 和调试工具，可快速定位代码逻辑错误、响应式更新问题及异步流程异常。重点在于结合上下文检查与单步执行，深入理解执行流程，提升调试效率。