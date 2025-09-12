---
title: JavaScript代码片段
date: 2020-06-09 21:50:00
categories: 
- 前端知识
tags:
- JavaScript
---

> ❝ 本文翻译自 [19 Practical ES6 Snippets to Solve Common JS Problems](https://link.zhihu.com/?target=https\\%3A//madza.hashnode.dev/19-practical-es6-snippets-to-solve-common-js-problems)，作者： Madza， 略有删改。
> ❞

在实际工作中，开发者常面临一些需巧妙编程解决的挑战。有时几行代码就能迎刃而解。本文整理了一系列实用代码片段，助您轻松处理URL、DOM操作、事件处理、日期处理以及用户偏好设置等常见问题。

这些精选代码片段均源自“`30 seconds of code`”——一个卓越的编程资源库。我强烈推荐您查阅其完整代码，以获得更多灵感。

选择这些代码片段的首要准则是它们的实用性。希望您能在这里发现宝贵的资源，并将其应用于未来的项目中，以提升编程效率和质量。

### 1.如何获取base URL？

```text
const getBaseURL = url => url.replace(/[?#].*$/, '');

getBaseURL('http://url.com/page?name=Adam&surname=Smith');
// 'http://url.com/page'
```



### 2.如何检查URL是否是绝对的？

```text
const isAbsoluteURL = str => /^[a-z][a-z0-9+.-]*:/.test(str);

isAbsoluteURL('https://google.com'); // true
isAbsoluteURL('ftp://www.myserver.net'); // true
isAbsoluteURL('/foo/bar'); // false
```



### 前端获取URL参数的方法（可能有bug）

#### slice

```text
const getURLParameters = url =>
  (url.match(/([^?=&]+)(=([^&]*))/g) || []).reduce(
    (a, v) => (
      (a[v.slice(0, v.indexOf('='))] = v.slice(v.indexOf('=') + 1)), a
    ),
    \\{\\}
  );

getURLParameters('google.com'); // \\{\\}
getURLParameters('http://url.com/page?name=Adam&surname=Smith');
// \\{name: 'Adam', surname: 'Smith'\\}
```

#### 字符串 split 方法

因为一个 `url` 地址是字符串形式的，所以利用 `split` 方法将参数提取出来，`该方法比较常用`，而且容易理解（对于不太会使用正则的我来说，haha~）

```JavaScript
let URL = "http://www.baidu.com?name=张三&age=25&sex=男&wife=小红"
function getUrlParams(url) \\{
    // 通过 ? 分割获取后面的参数字符串
    let urlStr = url.split('?')[1]
    // 创建空对象存储参数
	let obj = \\{\\};
    // 再通过 & 将每一个参数单独分割出来
	let paramsArr = urlStr.split('&')
	for(let i = 0,len = paramsArr.length;i < len;i++)\\{
        // 再通过 = 将每一个参数分割为 key:value 的形式
		let arr = paramsArr[i].split('=')
		obj[arr[0]] = arr[1];
	\\}
	return obj
\\}
console.log(getUrlParams(URL))
```

![对象参数1.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a4bc9a802f2b4480bf34cd3dd990c559~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp?)

#### 利用 URLSearchParams 方法

在 MDN 中结合两种方法实现参数的获取：1. 使用 `new URLSearchParams(url)` 方法，返回一个 `URLSearchParams` 对象，再调用 `entries()` 方法返回一个可迭代对象（Iterator）；2. 使用 `Object.fromEntries(iterable)` 方法转化为普通对象

```JavaScript
let URL = "http://www.baidu.com?name=Jack&age=25&sex=men&wife=Lucy"
function getUrlParams2(url) \\{
	let urlStr = url.split('?')[1]
	const urlSearchParams = new URLSearchParams(urlStr)
	const result = Object.fromEntries(urlSearchParams.entries())
	return result
\\}
console.log(getUrlParams2(URL))
```

![对象参数2.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/fc358dda6893417ba3df215999dfe96b~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp?)

**特别的**：`URLSearchParams` 方法不仅可以获取参数，还可以将参数对象转为 字符串，详细用法可查看 MDN 中的介绍，并且该方法存在浏览器兼容性问题。

#### 利用正则匹配方法

正则匹配功能强大相信很多小伙伴都知道，不仅可以实现在登录注册时的账号、密码、邮箱、手机号等等的验证，还可以非常方便的处理一些字符串（校验、替换、提取等操作），难点在于对正则使用的熟练度，这里就是通过正则提取字符串中需要的字符

```JavaScript
let URL = "http://www.baidu.com?name=Tom&friend=Jerry"
// let URL = "http://www.baidu.com?name=张三&age=25&sex=男&wife=小红"
function getUrlParams3(url)\\{
	// \w+ 表示匹配至少一个(数字、字母及下划线), [\u4e00-\u9fa5]+ 表示匹配至少一个中文字符
        /*
            该正则匹配规则表示: 首先匹配的格式是 xxx = xxx
                               然后 (\w+|[\u4e00-\u9fa5]+) 表示至少匹配一个(字母、数字、下划线) 或者至少匹配一个中文字符
        */
	let pattern = /(\w+|[\u4e00-\u9fa5]+)=(\w+|[\u4e00-\u9fa5]+)/ig;
        
        /*
            该正则匹配规则表示: 首先匹配的格式是 xxx = xxx
                               然后[^?|&] 表示匹配的字符中不能含有 ? 或者 &，后面同理
        */ 
        // let pattern = /([^?|&]+)=([^&]+)/ig;
        
	let result = \\{\\};
	url.replace(pattern, ($, $1, $2)=>\\{
		result[$1] = $2;
	\\})
	return result
\\}
console.log(getUrlParams3(URL))
```

![参数对象3.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b7aa2000ba624a8c957336c1d2908873~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp?)

#### 使用第三方库 qs

使用第三方库 `qs` 也可以实现 `url` 中参数字符的提取，还能实现将参数对象转为 url 参数形式，需要注意的是浏览器 `cdn` 方式引入时是默认添加到全局对象 window 的 `Qs` 属性上的

```JavaScript
<script src="https://cdn.bootcdn.net/ajax/libs/qs/6.10.3/qs.min.js"></script>
<script>
let URL = "http://www.baidu.com?product='iPhone 13 Pro'&price=￥9999.00"
function getUrlParams4(url)\\{
	// 引入 qs 库时会默认挂在到全局 window 的 Qs 属性上
	// console.log(window)
	let urlStr = url.split('?')[1]
	let result = Qs.parse(urlStr)
	// 拼接额外参数
	let otherParams = \\{
		num:50,
		size:6.1
	\\}
	let str = Qs.stringify(otherParams)
	let newUrl = url + str
	return \\{result,newUrl\\}
\\}
console.log(getUrlParams4(URL))
</script>
```

![参数对象4.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9ff40106fc3245678726505ae7c9ad4d~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp?)

原文链接：https://juejin.cn/post/7082306920945549325



### 4.如何检查一个元素是否包含另一个元素？

```text
const elementContains = (parent, child) =>
  parent !== child && parent.contains(child);

elementContains(
  document.querySelector('head'),
  document.querySelector('title')
);
// true
elementContains(document.querySelector('body'), document.querySelector('body'));
// false
```



### 5.如何获取元素的所有祖先？

```text
const getAncestors = el => \\{
  let ancestors = [];
  while (el) \\{
    ancestors.unshift(el);
    el = el.parentNode;
  \\}
  return ancestors;
\\};

getAncestors(document.querySelector('nav'));
// [document, html, body, header, nav]
```



### 7.如何处理元素外部的单击？

```text
const onClickOutside = (element, callback) => \\{
  document.addEventListener('click', e => \\{
    if (!element.contains(e.target)) callback();
  \\});
\\};

onClickOutside('#my-element', () => console.log('Hello'));
// Will log 'Hello' whenever the user clicks outside of #my-element
```



### 8.如何生成UUID？

```text
const UUIDGeneratorBrowser = () =>
  ([1e7] + -1e3 + -4e3 + -8e3 + -1e11).replace(/[018]/g, c =>
    (
      c ^
      (crypto.getRandomValues(new Uint8Array(1))[0] & (15 >> (c / 4)))
    ).toString(16)
  );

UUIDGeneratorBrowser(); // '7982fcfe-5721-4632-bede-6000885be57d'
```



### 9.如何获取所选文本？

```text
const getSelectedText = () => window.getSelection().toString();

getSelectedText(); // 'Lorem ipsum'
```



### 11.如何为HTML元素添加样式？

```text
const addStyles = (el, styles) => Object.assign(el.style, styles);

addStyles(document.getElementById('my-element'), \\{
  background: 'red',
  color: '#ffff00',
  fontSize: '3rem'
\\});
```



### 12.如何切换全屏模式？

```text
const fullscreen = (mode = true, el = 'body') =>
  mode
    ? document.querySelector(el).requestFullscreen()
    : document.exitFullscreen();

fullscreen(); // Opens `body` in fullscreen mode
fullscreen(false); // Exits fullscreen mode
```



### 13.如何检测Caps Lock是否打开？

```text
<form>
  <label for="username">Username:</label>
  <input id="username" name="username">

  <label for="password">Password:</label>
  <input id="password" name="password" type="password">
  <span id="password-message" style="display: none">Caps Lock is on</span>
</form>

const el = document.getElementById('password');
const msg = document.getElementById('password-message');

el.addEventListener('keyup', e => \\{
  msg.style = e.getModifierState('CapsLock')
    ? 'display: block'
    : 'display: none';
\\});
```



### 14.如何检查日期是否有效？

```text
const isDateValid = (...val) => !Number.isNaN(new Date(...val).valueOf());

isDateValid('December 17, 1995 03:24:00'); // true
isDateValid('1995-12-17T03:24:00'); // true
isDateValid('1995-12-17 T03:24:00'); // false
isDateValid('Duck'); // false
isDateValid(1995, 11, 17); // true
isDateValid(1995, 11, 17, 'Duck'); // false
isDateValid(\\{\\}); // false
```



### 15.如何从日期中获取时分秒信息？

```text
const getColonTimeFromDate = date => date.toTimeString().slice(0, 8);

getColonTimeFromDate(new Date()); // '08:38:00'
```



### 16.如何从Date生成UNIX时间戳？

```text
const getTimestamp = (date = new Date()) => Math.floor(date.getTime() / 1000);

getTimestamp(); // 1602162242
```



### 17.如何查看当前用户的首选语言？

```text
const detectLanguage = (defaultLang = 'en-US') =>
  navigator.language ||
  (Array.isArray(navigator.languages) && navigator.languages[0]) ||
  defaultLang;

detectLanguage(); // 'nl-NL'
```



### 18.如何查看用户的首选配色方案？

```text
const prefersDarkColorScheme = () =>
  window &&
  window.matchMedia &&
  window.matchMedia('(prefers-color-scheme: dark)').matches;

prefersDarkColorScheme(); // true
```



### 19.如何检查设备是否支持触摸事件？

```text
const supportsTouchEvents = () =>
  window && 'ontouchstart' in window;

supportsTouchEvents(); // true
```

在这篇文章中，我们列举了一些精心挑选的代码片段来解决开发过程中的常见挑战。这些代码片段涵盖了处理URL、DOM操作、事件处理、日期处理和用户偏好设置等多个方面，旨在提供简洁而高效的解决方案。希望你能在日常工作中找到并应用这些有价值的代码片段，从而提升编程效率和质量。