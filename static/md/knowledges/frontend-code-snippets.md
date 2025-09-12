---
title: 前端代码片段
date: 2021-11-25 15:26:47
categories: 
- 前端知识
tags:
- 前端
---

在日常的开发过程中，我们都会有一些常用的代码片段，这些代码片段可以直接复制到各个项目中使用，非常方便。如果你有接手过别人的项目，就可以很明显感受到几个项目一般都会有一些相同的工具类方法，这些方法就是之前开发者的常用代码片段。

现在前端社区相当完善，有许多好用质量又有保证的库，如 lodash、dayjs、classnames、js-cookie 等，这些库基本能满足你开发中对数组、日期、类名、cookie 等的处理。

所以本文会尽量不重复介绍那些很常见的代码片段。



### 1. 检测元素之外的点击

在实现隐藏弹窗或收起下拉框时，如果你还在一层层判断是否点击了某个元素之外的区域，赶紧试试使用 `contains` 方法来实现。

```
document.addEventListener('click', function (evt) \\{
    // isClickedOutside 为 true 如果点击的元素在 ele 之外
    const isClickedOutside = !ele.contains(evt.target);
\\});
```



### 2. 快速打开官网

当你想查看第三方库的主页和代码仓库时，你可以使用一下命令快速打开：

```
// 打开主页
npm home PACKAGE_NAME
npm home react

// 打开代码仓库
npm repo PACKAGE_NAME
npm repo react
```

![图片](https://mmbiz.qpic.cn/sz_mmbiz_gif/lLBsScfW7cV8PVyFqWxLrHE8EjLSxdYWrh4M8pjuoHibYPyuhic7PlnCL38KtoBzdRa8Rg05wphw47q1jN4ibwVRw/640?wx_fmt=gif&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



### 3. 一次性的事件监听

除了在监听的事件函数中移除当前的监听外，也可以使用 `once` 参数。

```
const handler = function (e) \\{\\};
ele.addEventListener('event-name', handler, \\{ once: true \\});
```



### 4. 格式化时分秒

在展示音视频时长之类的场景时，需要把时长秒数格式为 HH:mm:ss 的格式。

```
const formatSeconds = (s) =>
  [parseInt(s / 60 / 60), parseInt((s / 60) \\% 60), parseInt(s \\% 60)]
    .join(':')
    .replace(/\b(\d)\b/g, '0$1')
```

如果你想显示“刚刚”、“5分钟前”之类的内容，可以尝试 timeago.js 库。



### 5. URL 参数转化为对象

获取 url 参数有个热门的库 query-string，如果不想使用的话，可以通过 `URLSearchParams` API 实现。

```
const getUrlParams = (query) =>
  Array.from(new URLSearchParams(query)).reduce(
    (p, [k, v]) =>
      Object.assign(\\{\\}, p, \\{ [k]: p[k] ? (Array.isArray(p[k]) ? p[k] : [p[k]]).concat(v) : v \\}),
    \\{\\}
  )
  
// 获取 query 参数
getUrlParams(location.query)
// \\{ a: ['1', '4'], b: '2', c: '3' \\}
getUrlParams('?a=1&b=2&c=3&a=4')

// 获取 hash 参数
getUrlParams(location.hash.split('?')[1])
```



### 6. 打开新页签

看似平平无奇的打开页签，但是需要关注下 `rel`，如果要打开外链，建议设置为 `noopener noreferrer`，避免一些恶意网站通过 `window.opener.location` 重定向你的网站地址。`window.open` 方法同理。

```
// 高版本浏览器 rel 默认为 noopener，不过建议显示设置，兼容低版本。
<a target="_blank" rel="noopener noreferrer">...</a>
// window.open rel 默认为 opener，需要自己设置
window.open('https://baidu.com', 'baidu', 'noopener,noreferrer')
```

以下有安全漏洞，打开的新页签可以通过 window.opener.location 重定向你的网站

```
<a target="_blank" rel="opener">...</a>
window.opener.location = 'http://fake.website.here';
```



### 7. 显示上传的图片

通过 `fileReader` API 的 `readAsDataURL` 方法来显示上传图片。

```
function readImage() \\{
  const fileReader = new FileReader()
  const file = document.getElementById('uploaded-file').files[0]

  if (file) \\{
    fileReader.readAsDataURL(file)
  \\}

  fileReader.addEventListener(
    'load',
    () => \\{
      const result = fileReader.result
      const resultContainer = document.getElementById('result')
      const img = document.createElement('img')
      img.src = result
      resultContainer.append(img)
    \\},
    \\{ once: true \\}
  )
\\}
```



### 8. 文件下载

使用 `a` 标签的 `download` 属性，同源才能触发下载，IE 不支持，移动端兼容性也不太好。

```
<a href="/path/to/file" download>Download</a>
// 或者 js 临时生成 a
function download(url) \\{
  const link = document.createElement('a')
  link.download = 'file name'
  link.href = 'url'

  document.body.appendChild(link)
  link.click()
  document.body.removeChild(link)
\\}
```

静态资源服务器设置响应头也能触发浏览器下载。

```
Content-Disposition: attachment; filename="filename.jpg"
```

除了在线文件下载，你还可以创建一个 text 或 json 文件，并下载，主要用到了 `Blob` 对象和 `createObjectURL` 方法。

```
const data = JSON.stringify(\\{ 'message': 'Hello Word' \\});

const blob = new Blob([data], \\{ type: 'application/json' \\});

// 创建一个 URL
const url = window.URL.createObjectURL(blob);

// 用上面的 download 方法下载这个 url
...

// 释放创建的 URL
window.URL.revokeObjectURL(url);
```



### 9. 缓存结果

缓存函数的结果，当计算比较复杂时可以使用。

```
const memoize = (fn) =>
  (
    (cache = Object.create(null)) =>
    (arg) =>
      cache[arg] || (cache[arg] = fn(arg))
  )()
```



### 10. 多行省略号

单行或多行截断显示省略号，很常用的 CSS 片段。

```
.truncate \\{
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
\\}

.truncate \\{
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 2;
  overflow: hidden;
\\}
```



### 11. 选中最后几个元素

```
// 前三个
li:nth-child(-n + 3) \\{
  text-decoration: underline;
\\}

// 选中 2-5 的列表项
li:nth-child(n + 2):nth-child(-n + 5) \\{
  color: #2563eb;
\\}

// 倒数两个
li:nth-last-child(-n + 2) \\{
  text-decoration-line: line-through;
\\}
```

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/lLBsScfW7cV8PVyFqWxLrHE8EjLSxdYWK3ZQHAsy6ic3dKnPsia1EIns2m91CS6QsjDJSVkkwjlLIUx2nliaciakPA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



### 12. 滚动条样式

自定义滚动条样式也是很常见的需求，除了通过样式，也可以通过第三方库（如 better-scroll 等）来实现自定义滚动条样式。

```
/*定义滚动条高宽及背景 高宽分别对应横竖滚动条的尺寸*/
::-webkit-scrollbar \\{
  width: 8px;
  height: 8px;
\\}

/*定义滚动条轨道 内阴影+圆角*/
::-webkit-scrollbar-track \\{
  border-radius: 10px;
  background-color: #fafafa;
\\}

/*定义滑块 内阴影+圆角*/
::-webkit-scrollbar-thumb \\{
  border-radius: 10px;
  background: rgb(191, 191, 191);
\\}

/*较新的 API*/
body \\{
  scrollbar-width: thin;
  scrollbar-color: #718096 #edf2f7;
\\}
```



### 13. 百分比计算 - 最大余额法

计算百分比时，由于四舍五入，各个比例相加可能不等于 1，通过最大余额法可以保证总数为 1。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/lLBsScfW7cV8PVyFqWxLrHE8EjLSxdYWViaXq92nr6JsvMADC2bZqJMl1zJ8NQBibfuLlw9ibrpicJynzKO7UyOj6g/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

```
// 输出 ['32.56\\%', '6.97\\%', '27.91\\%', '32.56\\%']
getPercentWithPrecision([56, 12, 48, 56], 2)

// 具体最大余额法算法可以网上搜索查看
function getPercentWithPrecision(valueList, precision) \\{
  // 根据保留的小数位做对应的放大
  const digits = Math.pow(10, precision)
  const sum = valueList.reduce((total, cur) => total + cur, 0)
  
  // 计算每项占比，并做放大，保证整数部分就是当前获得的席位，小数部分就是余额
  const votesPerQuota = valueList.map((val) => \\{
      return val / sum * 100 * digits
  \\})
  // 整数部分就是每项首次分配的席位
  const seats = votesPerQuota.map((val) => \\{
    return Math.floor(val);
  \\});
  // 计算各项的余额
  const remainder = votesPerQuota.map((val) => \\{
    return val - Math.floor(val)
  \\})
    
  // 总席位
  const totalSeats = 100 * digits
  // 当前已经分配出去的席位总数
  let currentSeats = votesPerQuota.reduce((total, cur) => total + Math.floor(cur), 0)
    
  // 按最大余额法分配
  while(totalSeats - currentSeats > 0) \\{
    let maxIdx = -1 // 余数最大的 id
    let maxValue = Number.NEGATIVE_INFINITY // 最大余额, 初始重置为无穷小

    // 选出这组余额数据中最大值
    for(var i = 0; i < remainder.length; i++) \\{
      if (maxValue < remainder[i]) \\{
        maxValue = remainder[i]
        maxIdx = i
      \\}
    \\}
        
    // 对应的项席位加 1，余额清零，当前分配席位加 1
    seats[maxIdx]++
    remainder[maxIdx] = 0
    currentSeats++
  \\}
    
  return seats.map((val) => `$\\{val / totalSeats * 100\\}\\%`)
\\}
```



### 14. 限制并发

当有大量请求需要发起时，往往需求限制并发数量保证其他请求能优先返回。

```
async function asyncPool(poolLimit, iterable, iteratorFn) \\{
  // 用于保存所有异步请求
  const ret = [];
  // 用户保存正在进行的请求
  const executing = new Set();
  for (const item of iterable) \\{
    // 构造出请求 Promise
    const p = Promise.resolve().then(() => iteratorFn(item, iterable));
    ret.push(p);
    executing.add(p);
    // 请求执行结束后从正在进行的数组中移除
    const clean = () => executing.delete(p);
    p.then(clean).catch(clean);
    // 如果正在执行的请求数大于并发数，就使用 Promise.race 等待一个最快执行完的请求
    if (executing.size >= poolLimit) \\{
      await Promise.race(executing);
    \\}
  \\}
  // 返回所有结果
  return Promise.all(ret);
\\}

// 使用方法
const timeout = i => new Promise(resolve => setTimeout(() => resolve(i), i));
asyncPool(2, [1000, 5000, 3000, 2000], timeout).then(results => \\{
  console.log(results)
\\})
```



### 15. uuid

生成 uuid 的代码片段

```
const uuid = (a) =>
  a
    ? (a ^ ((Math.random() * 16) >> (a / 4))).toString(16)
    : ([1e7] + -1e3 + -4e3 + -8e3 + -1e11).replace(/[018]/g, uuid)
```



### 16. 打开 Modal 时禁止 body 滚动

打开弹窗的时候，会发现背后的内容还是可以滚动，我们需要在弹窗出现时禁用滚动，在弹窗消失时恢复。

```
// 打开 Modal 时，禁止 body 滚动
document.body.style.overflow = 'hidden';

// 恢复滚动
document.body.style.removeProperty('overflow');
```



### 使用URLSearchParams获取URL的搜索参数

这应该是一个非常常见的操作，之前经常会使用 正则来完成，现在有了更简单的方式：

```
const getQueryByName = (name) => \\{
  const query = new URLSearchParams(location.search)
  return decodeURIComponent(query.get(name))
\\}
// url: https://sunday.com/?name=fatfish&age=100
const name = getQueryByName('name') // fatfish
const age = getQueryByName('age') // 100
const gender = getQueryByName('gender') // null
```



### 平滑滚动至页面顶部

```
const scrollToTop = () => \\{
  const c = document.documentElement.scrollTop || document.body.scrollTop
  
  if (c > 0) \\{
    window.requestAnimationFrame(scrollToTop)
    window.scrollTo(0, c - c / 8)
  \\}
\\}
```



### 获取当前页面滚动距离

```
const getScrollPosition = (el = window) => (\\{
  x: el.pageXOffset !== undefined ? el.pageXOffset : el.scrollLeft,
  y: el.pageYOffset !== undefined ? el.pageYOffset : el.scrollTop,
\\})

getScrollPosition() // \\{ x: 0, y: 215 \\}
```



### 判断当前设备是Andoird还是iOS

```
function getOSType() \\{
  let u = navigator.userAgent,
    app = navigator.appVersion
  let isAndroid = u.indexOf("Android") > -1 || u.indexOf("Linux") > -1
  let isIOS = !!u.match(/\(i[^]+( U)? CPU.+Mac OS X/)
  
  if (isIOS) \\{
    return 0
  \\} else if (isAndroid) \\{
    return 1
  \\} else \\{
    return 2
  \\}
\\}

getOSType() // 0
```



### 格式化货币

```
const formatMoney = (money) => \\{
  return money.toLocaleString()
\\}

formatMoney(123456789) // '123,456,789'
formatMoney(123456789.123) // '123,456,789.123'
formatMoney(123) // '123'
```



### 进入和退出全屏

```
// 进入全屏
function fullScreen() \\{
  let el = document.documentElement
  let rfs = el.requestFullScreen || el.webkitRequestFullScreen || el.mozRequestFullScreen || el.msRequestFullScreen
  //typeof rfs != "undefined" && rfs
  if (rfs) \\{
    rfs.call(el)
  \\} else if (typeof window.ActiveXObject !== "undefined") \\{
    let wscript = new ActiveXObject("WScript.Shell")
    if (wscript != null) \\{
      wscript.SendKeys("\\{F11\\}")
    \\}
  \\}
\\}
// 退出全屏
function exitScreen() \\{
  let el = document
  let cfs = el.cancelFullScreen || el.webkitCancelFullScreen || el.mozCancelFullScreen || el.exitFullScreen
  //typeof cfs != "undefined" && cfs
  if (cfs) \\{
    cfs.call(el)
  \\} else if (typeof window.ActiveXObject !== "undefined") \\{
    let wscript = new ActiveXObject("WScript.Shell")
    if (wscript != null) \\{
      wscript.SendKeys("\\{F11\\}")
    \\}
  \\}
\\}
```