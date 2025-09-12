---
title: uniapp网页H5
date: 2023-04-29 10:03:10
categories: 
- 前端知识
tags:
- uniapp
---

### uniapp动态引入script

```
		onLoad(options) \\{
            if (this.envType === 4) \\{
                this.loadScript()
            \\}
        \\}
		
		// 动态引入script
        loadScript() \\{
            const URL =
                'https://cdn.dingxiang-inc.com/ctu-group/captcha-ui/index.js'
            // 插入script脚本
            let scriptNode = document.createElement('script')
            scriptNode.setAttribute('type', 'text/javascript')
            scriptNode.setAttribute('src', URL)
            document.body.appendChild(scriptNode)
            setTimeout(() => \\{
                this.initDx()
            \\}, 1000)
        \\},
```



### uniapp的H5项目腾讯地图跨域问题

用uni-app开发，h5和小程序使用的都是腾讯地图-微信小程序sdk，但它是为小程序设计的，所以在vue的h5中使用会有跨域问题，所以结合vue-jsonp对这个sdk做了一下修改，可以直接放入h5中使用。此方法不止在uniapp中可以使用，在所有H5项目中都可以。

简单描述一句：就是把sdk内使用的wx对象重写，替换了里面的request方法，使用vue-jsonp完成跨域；H5和小程序不能兼容问题，可以用uniapp的条件编译来解决。

#### 1.在腾讯地图创建应用时，要把webserviceAPI勾选上，并配置H5的域名白名单

#### 2.安装vue-jsonp

```
npm i --save vue-jsonp
```

#### 3.main.js中添加

```
import \\{ VueJsonp \\} from "vue-jsonp"
Vue.use(VueJsonp)
```

如果在这个时候出现 install undefined的报错，需要先初始化npm
npm init -y
然后在执行第一步进行安装，就正常了

#### 4.qqmap-wx-jssdk.js中最上方添加以下代码

```
// #ifdef H5
// 条件编译：仅出现在 H5 平台下的代码（解决h5地图跨域问题）
import Vue from 'vue'
var vm = new Vue()
// wx对象里的request方法重写
var wx = \\{
	request(obj) \\{
		obj.data.output = 'jsonp'
		vm.$jsonp(obj.url, obj.data)
			.then(json => \\{
				if (json.status == 0) \\{
					obj.success(\\{ data: json \\})
				\\} else \\{
					obj.fail(json)
				\\}
			\\})
			.catch(err => \\{
				obj.fail(err)
			\\})
	\\}
\\}
// #endif
```

参考链接: https://blog.csdn.net/weixin_42390525/article/details/117596280

https://blog.csdn.net/qq_60485359/article/details/126482245

https://www.jianshu.com/p/4847480995c9



### uniapp中h5获取网络类型

```
		// 获取网络类型
        getNetworkType() \\{
            if (this.envType === 4) \\{
                // h5判断有无网络
                console.log(navigator.onLine);
                if (navigator.onLine) \\{
                    this.judge();
                \\} else \\{
                    this.tip = "网络异常";
                    this.state = 2;
                \\}
            \\} else \\{
                let _this = this;
                uni.getNetworkType(\\{
                    success(res) \\{
                        console.log("网络", res);
                        if (res.networkType === "none") \\{
                            _this.tip = "网络异常";
                            _this.state = 2;
                        \\} else \\{
                            _this.getSetting();
                        \\}
                    \\},
                \\});
            \\}
            console.log(this.tip);
        \\}
```



### 在网页端，实现监听窗口尺寸变化（同一页套娃效果）

App.vue

```
onLaunch() \\{
        console.log('App Launch')
        this.getSystemInfo()
        // 如果在网页端，实现监听窗口尺寸变化
        if (window) \\{
        	// PC隐藏tabbar
            if (this.systemInfo.windowWidth > 750) \\{
                uni.hideTabBar()
            \\}
            // 如果PC首次从其他路径进入，就跳到首页，不然没有PC样式
            if (
                this.systemInfo.windowWidth > 750 &&
                window.location.pathname !== '/'
            ) \\{
                window.location.href = '/'
            \\}
            // 高频率会让浏览器崩溃，解决这个问题可以用定时器对该函数进行节流
            let timer = null,
                num = 0 // 用来计数，如果只监听到一次，是由于uni.hideTabBar引起的，不需要跳转（没有这个会陷入跳转死循环）
            window.onresize = function () \\{
                console.log('实时屏幕宽度', document.body.clientWidth, num)
                num++
                clearTimeout(timer)
                timer = setTimeout(function () \\{
                    // 首页有PC相关代码
                    if (num > 1) \\{
                        window.location.href = '/'
                    \\}
                \\}, 1000)
            \\}
        \\}
\\}        
```

请求封装

```
if (res.data.code === 401 && windowWidth <= 750) \\{
    console.log("小程序登录失效")
    uni.reLaunch(\\{
    	url: "/pages/login/Login"
    \\})
\\}
```

首页

```
<view>
        <!-- PC -->
        <view class="ifram-box"
            v-if="systemInfo.windowWidth>750">
            <view class="ifram-wrapper">
                <img class="barcode-image"
                    src="/static/images/code-bg.png"
                    alt="">
                <view class="list">
                    <p class="list-cell">请使用手机浏览器，扫描上方二维码预览。</p>
                    <p class="list-cell">PC浏览器，请打开控制台并切换至手机模式后再次刷新浏览。</p>
                </view>
            </view>
            <view class="h5-viwer-box">
                <iframe frameborder="0"
                    scrolling="auto"
                    class="h5-viwer"
                    width="375"
                    height="812"
                    src="/pages/home/Home">
                </iframe>
            </view>
        </view>
        <!-- 手机 -->
        <view class="home-content"
            v-else>
        </view>
</view>

		async init() \\{
            // PC版只展示页面，不需要触发方法
            if (this.systemInfo.windowWidth > 750) \\{
                return
            \\}
            // 首次登录还没有token，主动跳转，避免登录失效提示
            if (this.systemInfo.windowWidth <= 750 && !this.token) \\{
                uni.reLaunch(\\{
                    url: '/pages/login/Login'
                \\})
                return
            \\}
            
            // 获取数据方法
            ...
        \\}
```



### uni-app使用uni.request获取的文件流图片转base64数据

网站开发中对于后端请求数据是必不可少的一个操作，而后端反馈的数据格式大致分为字符串、json、文件流等。

对于后端反馈的文件流格式图片，在前端开发中有时并不能被直接使用。这个时候就需要将文件流图片先转换base64格式的图片数据，再来进行展示效果。

```
			uni.request(\\{
                url: 'https://xxx.xxx.com/api/wechat-qrcode',
                method: 'POST',
                responseType: 'arraybuffer',
                success: (res) => \\{
                    this.qrcodeUrl =
                        'data:image/png;base64,' +
                        uni.arrayBufferToBase64(res.data)
                    console.log(this.qrcodeUrl)
                \\}
            \\})
```

参数解析：

1.responseType：设置响应的数据类型为arraybuffer。

2.uni.arrayBufferToBase64将ArrayBuffer对象转成 Base64 字符串

注：uni.arrayBufferToBase64支持平台分别为App、H5、微信小程序、快手小程序、京东小程序

代码逻辑基础说明：

使用uni.request获取服务端反馈的文件流数据（注这里的responseType必须设置为arraybuffer），使用uni.arrayBufferToBase64将获取的文件流转换成base64数据。

转换后的base64数据需要拼接文件头：`data:image/png;base64,`



### base64编码的图片数据在vue3中如何显示？

后端返回qrCode:"/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQ..."

在 Vue3 中显示 Base64 编码的图片数据，可以通过以下步骤实现：

1. **确认数据格式**
确保后端返回的 `qrCode` 是完整的 Base64 字符串（如 `data:image/png;base64,XXXX`）或纯 Base64 数据部分（如 `XXXX`）。根据你的示例 `/9j/4AAQSkZ...`，看起来像是 JPEG 图片的 Base64 数据部分，但需要补充 MIME 类型前缀。

---

2. **拼接完整的 Data URL**
如果 `qrCode` 是纯 Base64 数据（无前缀）：
• JPEG 图片：拼接 `data:image/jpeg;base64,` + Base64 数据。

• PNG 图片：拼接 `data:image/png;base64,` + Base64 数据。

---

3. **在 Vue3 模板中绑定**
直接在 `<img>` 标签的 `src` 属性中动态绑定完整的 Data URL：

```vue
<template>
  <img :src="imageSrc" alt="QR Code">
</template>

<script setup>
import \\{ computed \\} from 'vue';

const props = defineProps(\\{
  qrCode: String // 接收后端返回的 Base64 数据
\\});

// 自动根据图片类型拼接 Data URL
const imageSrc = computed(() => \\{
  // 假设是 JPEG 图片，如果是 PNG 则替换为 image/png
  return `data:image/jpeg;base64,$\\{props.qrCode\\}`;
\\});
</script>
```

---

4. **处理不同图片格式**
如果不确定图片类型，可以通过代码判断：
```javascript
// 根据 Base64 开头字符判断类型（示例）
const getMimeType = (base64) => \\{
  if (base64.startsWith('/9j/')) return 'image/jpeg';
  if (base64.startsWith('iVBORw')) return 'image/png';
  return 'image/png'; // 默认处理
\\};

const imageSrc = computed(() => \\{
  const mime = getMimeType(props.qrCode);
  return `data:$\\{mime\\};base64,$\\{props.qrCode\\}`;
\\});
```

---

5. **注意事项**
• 数据完整性：确保 Base64 数据没有多余的空格或换行符。

• 异步加载：如果 `qrCode` 来自异步请求，使用 `v-if` 避免渲染空值：

  ```vue
  <img v-if="qrCode" :src="imageSrc" alt="QR Code">
  ```

---

完整示例代码
```vue
<template>
  <div>
    <!-- 直接拼接在模板中 -->
    <img v-if="qrCode" :src="'data:image/jpeg;base64,' + qrCode" alt="QR Code">
  </div>
</template>

<script setup>
defineProps(\\{
  qrCode: String // 接收后端返回的 Base64 数据
\\});
</script>
```

---

通过以上方法，你可以直接在 Vue3 中正确显示 Base64 编码的图片。



### uniapp修改checkbox样式

第一个是H5，第二个是微信小程序

```
/deep/ checkbox,
    uni-checkbox \\{
        // checkbox样式
        .wx-checkbox-input,
        .uni-checkbox-input \\{
            width: 24rpx;
            height: 24rpx;
            padding: 2rpx;
            border-radius: 0;
            border: 2rpx solid #c8c9cc;
        \\}
        // checkbox选中后样式
        .wx-checkbox-input.wx-checkbox-input-checked,
        .uni-checkbox-input.uni-checkbox-input-checked \\{
            color: #fff !important;
            background: rgb(31, 108, 221);
            border: 2rpx solid rgb(31, 108, 221);
        \\}
        // checkbox选中后图标样式
        .wx-checkbox-input.wx-checkbox-input-checked::before \\{
            color: #fff;
        \\}
    \\}
```

参考链接：https://blog.csdn.net/weixin_43655896/article/details/122955576



### uniapp打包发布h5项目的缓存问题

uniapp 打包 H5 生成的`js`文件，默认情况下是不包含版本号以及时间戳后缀。这样会导致H5新版打包上线后，用户依旧使用的是浏览器中缓存的老版js文件，文件更新滞后等现象。

#### 第一种(推荐)

在根目录新建vue.config.js文件,粘贴以下代码

```
let filePath = ''
let Timestamp = ''
//编译环境判断,判断是否H5环境
if (process.env.UNI_PLATFORM === 'h5') \\{
    filePath = 'static/js/'; //打包文件存放文件夹路径
    Timestamp = '.' + new Date().getTime();//时间戳
\\}

module.exports = \\{
    configureWebpack: \\{ // webpack 配置 解决js缓存的问题
        output: \\{ // 输出重构  打包编译后的 文件目录 文件名称 【模块名称.时间戳】
            filename: `$\\{filePath\\}[name]$\\{Timestamp\\}.js`,
            chunkFilename: `$\\{filePath\\}[name]$\\{Timestamp\\}.js`
        \\}
    \\}
\\}
```

#### 第二个方法

在应用程序的入口文件（如 main.js 或 App.vue）uniapp项目 :h5template.html中添加时间戳。例如，您可以在 index.html 文件中添加以下代码：

```
 var script = document.createElement('script');
 script.src = '/js/app.js?' + new Date().getTime();
 document.getElementsByTagName('head')[0].appendChild(script);
```

注意:这个方法可以生效,但是在电脑端调试的时候会看到一个报错,但是不影响使用,有知道完美解决的可以留言一下哦,感谢.

#### 第三个方法

1.设置缓存 (未实践)

```
<meta http-equiv="Cache-Control" content="no-cache" />
```

手机页面通常在第一次加载后会进行缓存，然后每次刷新会使用缓存而不是去重新向服务器发送请求。如果不希望使用缓存可以设置no-cache。 

2.设置nginx禁止缓存

点击网站->站点设置->配置文件，放在这下面即可，把之前的允许js和css缓存删除掉，然后重启nginx或者重新载入nginx配置即可。 ![img](https://jihainet.com/static/uploads/images/2021/03/30/16170691796062847b6efba.png) 

```
location ~ \.(js|css|html)$ \\{
    add_header Cache-Control no-store;
\\}
```



### uniapp网页在微信调试时，控制台出现报错

Invalid Host/Origin header，[WDS] Disconnected!

manifest.json源码视图找到h5，在devServer: 添加 “disableHostCheck”: true

重新启动项目，报错就消失了

注意：只能在Hbuilder创建的项目使用，在cil创建的项目加这个会报错，options has an unknown property 'disableHostCheck'

```
"h5": \\{
		"devServer": \\{
			"disableHostCheck": true
			// "proxy": \\{
			// 	"/apis": \\{
			// 		"target": "",
			// 		"changeOrigin": true,
			// 		"secure": false,
			// 		"pathRewrite": \\{
			// 			"^/apis": "/"
			// 		\\}
			// 	\\}
			// \\}
		\\},
		"router": \\{
			"mode": "hash"
		\\},
		"template": "",
		"title": ""
	\\}
```



### 通过路径拼接传参时，参数中含有特殊符号（#），被截断造成传参错误

```
https://user-stage.xiuchuan.com/pages/login/H5Login?mch_id=JiCI1qzUKGP6&redirect_url=http://172.16.8.84:8080/#/myPages/my/inspect
```

将#变成\\%23，在onLoad即可正常接受参数



### 云之家引入js

```
if (window.location.origin === "miniapp://" || options.query.ticket) \\{
    // 金蝶小程序或者金蝶轻应用
    context.commit('setWebType', 4);
    context.dispatch('setScript',
    'https://static.yunzhijia.com/public/js/qing/latest/qing.js');
    // 发布时需要自己切换地址
    // context.dispatch('setApi', 2);
    context.dispatch('setApi', 3);
\\}

// 插入script脚本
setScript(context, src) \\{
    let scriptNode = document.createElement('script')
    scriptNode.setAttribute('type', 'text/javascript')
    scriptNode.setAttribute('src', src)
    document.body.appendChild(scriptNode)
    console.log('已插入脚本', src)
\\},
```



### 云之家个人信息

```
        personInfo: \\{\\}, // 云之家个人信息
		// 云之家获取个人信息
        getPersonInfo() \\{
            qing.call('getPersonInfo', \\{
                success: (res) => \\{
                    console.log('云之家获取个人信息', res)
                    this.personInfo = res
                    // this.$refs.alertRef.show(\\{
                    //     title: '云之家获取个人信息成功',
                    //     content: JSON.stringify(res)
                    // \\})
                \\},
                error: (res) => \\{
                    console.log('云之家获取个人信息失败', res)
                    this.personInfo = res
                \\}
            \\})
        \\},
        
        if (!this.formData.ticket) \\{
                // 没有ticket再验证（成功过一次就不用重复验证了）
                const res = await this.yunValidate()
                // \\{success:false, error:'用户取消验证', errorCode:13400\\}
                // \\{success:false, error:'密码验证错误', errorCode:13400\\}
                // \\{success:true, errorCode:1, data:\\{ticket:'APPURLWITHTICKETf3bb6035b335502d1387d6f7cad9249e'}}
                // this.$refs.alertRef.show(\\{
                //     title: '金蝶身份确认结果' + typeof res.success,
                //     content: JSON.stringify(res)
                // \\})
                if (res.success) \\{
                    // 输入正确的密码才能获取到ticket
                    this.formData.ticket = res.data.ticket
                \\} else \\{
                    uni.showToast(\\{
                        title: '请输入正确的密码',
                        icon: 'none',
                        duration: 2000
                    \\})
                    return
                \\}
            \\}
            
        // 金蝶身份确认
        yunValidate() \\{
            return new Promise((resolve, reject) => \\{
                qing.call('validate', \\{
                    type: 'password', // 验证方式
                    lightAppId: Config.lightAppId, // 轻应用id
                    prompt: '为正常使用', // 自定义提示语
                    ignoreYzjPwd: false, // 是否不做降级处理（false表示降级，使用登录密码验证）
                    success: (res) => \\{
                        console.log(res)
                        resolve(res)
                    \\},
                    error: (res) => \\{
                        console.log('金蝶身份确认失败', res)
                        // res.success = true
                        // resolve(res)
                        reject(res)
                    \\}
                \\})
            \\})
        \\},
```



### H5返回uniapp的webview

下载js文件放入public/static/uni.webview.1.5.4.js 

public/index.html

```
<!-- 为了返回第三方uniapp的webview -->
<script src="/static/uni.webview.1.5.4.js"></script>
```

在点击事件中

```
let pages = getCurrentPages()
console.log(pages);
// 返回上一页
uni.webView.navigateBack()
// 返回多少层级前的页面
uni.webView.redirectTo(\\{
	url:`/pages/my/index?level=$\\{getCurrentPages().length-1\\}`
\\})
```
