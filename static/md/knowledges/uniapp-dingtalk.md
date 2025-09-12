---
title: uniapp钉钉
date: 2023-04-28 19:03:10
categories: 
- 前端知识
tags:
- uniapp
- 小程序
---

### 小问题

- 钉钉小程序后台添加完Webview安全域名需要重新发布应用（或者重新真机调试），并不是实时生效

- uni.getLocation放在onLoad偶尔获取不到位置，放在onReady可以避免这个问题

- 统一授权套件目前只能在H5与小程序使用，PC端暂不支持

  https://www.dingtalk.com/qidian/help-detail-1060979859.html



### 钉钉小程序如何判断其当前环境

```
// 获取系统信息
		getSystemInfo(context) \\{
			uni.getSystemInfo(\\{
				success(res) \\{
					console.log("设备信息", res)
					context.commit('setSystemInfo', res);
					if (res.uniPlatform === "mp-weixin") \\{
						console.log("微信/企微环境", __wxConfig);
						if (res.environment === "wxwork") \\{
							context.commit('setEnvType', 2);
						\\} else \\{
							context.commit('setEnvType', 1);
						\\}
						// 不同环境使用不同接口域名
						if (__wxConfig.envVersion === "release") \\{
							// 正式版
							context.commit('setApiUrl', Config.releaseUrl);
							context.commit('setProUrl', Config.releaseProUrl);
						\\} else if (__wxConfig.envVersion === "trial") \\{
							// 体验版
							context.commit('setApiUrl', Config.testUrl);
							context.commit('setProUrl', Config.testProUrl);
						\\} else \\{
							// 开发版
							context.commit('setApiUrl', Config.testUrl);
							context.commit('setProUrl', Config.testProUrl);
						\\}
					\\} else if (res.uniPlatform === "mp-alipay") \\{
						console.log("钉钉/支付宝环境", __appxStartupParams, dd.isIDE);
						dd.getRunScene(\\{
							success(res) \\{
								console.log("运行版本", res.envVersion)
							\\},
						\\})
						context.commit('setEnvType', 3);
						if (dd.isIDE || __appxStartupParams.isRemoteDebug || __appxStartupParams.source) \\{
							// IDE中开发（没有source），或者是远程调试，或者体验版有source
							console.log("测试接口")
							context.commit('setApiUrl', Config.testUrl);
							context.commit('setProUrl', Config.testProUrl);
						\\} else \\{
							// 正式环境没有source
							console.log("正式接口")
							context.commit('setApiUrl', Config.releaseUrl);
							context.commit('setProUrl', Config.releaseProUrl);
						\\}
					\\}
				\\}
			\\})
		\\},
```

参考链接：https://blog.csdn.net/keloneko/article/details/106044305



### 报错及解决

报错：corpId is required
开发者工具左上角：没有登录或没有选择类型/应用/体验组织
报错：\\{error: 1002, errorMessage: '企业无此微应用'\\}
工作台-部署与发布-版本管理与发布-设置体验组织并开通-设置体验人员-开发者工具左上角选择体验组织即可

报错：onLoad调用组件方法，报错未定义

在onReady中调用即可

```
	onLoad(options) \\{
        console.log(options);
        this.toastType = options.toastType
    \\},
    onReady() \\{
        // 首次登录成功提示（如果放在onLoad中钉钉小程序因为组件还没有渲染完成会报错）
        if (this.toastType) \\{
            this.$refs.toastRef.show(
                "success",
                "登录成功"
            );
        \\}
        // 创建 map 上下文 MapContext 对象
        this.mapCtx = uni.createMapContext("myMap");
    \\},
```

问题：钉钉输入框没有auto-focus



### uniapp引入 'dingtalk-jsapi';

在main.js中

```
import * as dd from 'dingtalk-jsapi';
Vue.prototype.dd = dd;
```

在页面中

```
import \\{ onAuthAppBack \\} from "dingtalk-design-libs/biz/openAuthMiniApp";
onAuthAppBack(options, (data) => \\{
            console.log(data, 123);
            // 这里可以对返回数据做二次处理，之后需要把数据返回到page.onShow
            dd.alert(\\{
                title: "app is onAppShow have data ：" + JSON.stringify(data),
            \\});
            return data;
        \\});
```



### 时间选择器

```
<view class="message-item">
                <text>用车开始时间</text>
                <view class="message-item-content" v-if="envType === 3" @click="ddStart">
                    <text>\\\{\\\{ formModel.use_start\\\}\\\} }}</text>
                    <image src="/static/images/index_icon5@2x.png"></image>
                </view>
                <date-time mode="dateminute" :value="formModel.use_start" @change="startChange" v-else>
                    <view class="message-item-content">
                        <text>\\\{\\\{ formModel.use_start\\\}\\\} }}</text>
                        <image src="/static/images/index_icon5@2x.png"></image>
                    </view>
                </date-time>
            </view>
```

```
// 用车开始时间，时分的事件方法，如果需要时分秒参考https://blog.csdn.net/Shids_/article/details/122084621
        startChange(dateTime) \\{
            this.formModel.use_start = dateTime + ":00";
        \\},
        // 钉钉小程序选择用车开始时间
        ddStart() \\{
            dd.datePicker(\\{
                format: "yyyy-MM-dd HH:mm",
                currentDate: this.formModel.use_start,
                success: (res) => \\{
                    console.log(res);
                    this.formModel.use_start = res.date + ":00";
                \\},
            \\});
        \\},
```

时间选择组件DateTime.vue见文档：uniapp组件



### 文件查看

1.关于文件查看，在钉钉里需要使用钉盘进行查看。

转存文件到钉盘：[`dd.saveFileToDingTalk`](https://open.dingtalk.com/document/orgapp-client/transfer-files-to-a-nail-drive)

钉盘文件预览：[`dd.previewFileInDingTalk`](https://open.dingtalk.com/document/orgapp-client/nail-plate-file-preview)

封装成mixins，便于每个文件引用

```
import \\{ mapState \\} from "vuex";

export default \\{
    data() \\{
        return \\{
        \\};
    \\},
    computed: \\{
        ...mapState(\\{
            envType: (state) => state.login.envType,
            proUrl: (state) => state.login.proUrl,
            protocol: (state) => state.login.protocol,
        \\}),
    \\},
    methods: \\{
        // 预览协议
        previewFile(type) \\{
            let url, fileName, obj
            if (type === 1) \\{
                url = this.proUrl + "/mp_source/register.pdf";
                fileName = "用户协议"
                obj = this.protocol.register
            \\} else if (type === 2) \\{
                url = this.proUrl + "/mp_source/private.pdf";
                fileName = "隐私条款"
                obj = this.protocol.private
            \\}
            if (this.envType === 3) \\{
                this.ddPreviewFile(type, url, fileName, obj)
            \\} else if (this.envType === 4) \\{
                // H5打开协议
                window.open(url, '_self');
            \\} else \\{
                this.openDocument(url);
            \\}
        \\},
        // 钉钉预览协议
        ddPreviewFile(type, url, fileName, obj) \\{
        	// 如果缓存中有记录就直接预览
            if (obj) \\{
                dd.previewFileInDingTalk(obj)
            \\} else \\{
                // 钉钉采用钉盘处理文件
                let _this = this
                dd.saveFileToDingTalk(\\{
                    url,  // 文件在第三方服务器地址
                    name: fileName,
                    success(res) \\{
                        if (type === 1) \\{
                            _this.protocol.register = res.data[0]
                        \\} else if (type === 2) \\{
                            _this.protocol.private = res.data[0]
                        \\}
                        _this.$store.commit("setProtocol", _this.protocol);
                        if (res.data.length) \\{
                            dd.confirm(\\{
                                title: '提示',
                                content: '文件已保存到钉盘中，是否需要现在查看？',
                                confirmButtonText: '确定',
                                cancelButtonText: '取消',
                                success: (result) => \\{
                                    if (result.confirm) \\{
                                        dd.previewFileInDingTalk(\\{
                                            spaceId: res.data[0].spaceId,
                                            fileId: res.data[0].fileId,
                                            fileName: fileName,
                                            fileType: "pdf",
                                        \\})
                                    \\}
                                \\},
                            \\});
                        \\}
                    \\},
                    fail(err) \\{
                        console.log(err)
                        dd.alert(\\{
                            content: JSON.stringify(err)
                        \\})
                    \\}
                \\})
            \\}
        \\},
        // 微信/企微预览协议
        openDocument(url) \\{
            uni.downloadFile(\\{
                url, // 要预览的PDF的地址
                success(res) \\{
                    // console.log(res);
                    if (res.statusCode === 200) \\{ // 成功
                        uni.openDocument(\\{
                            filePath: res.tempFilePath, // 要打开的文件路径
                            showMenu: true, // 是否显示右上角菜单
                            success(res) \\{
                                // console.log("打开成功");
                            \\},
                            fail(res) \\{
                                // console.log("打开失败");
                            \\}
                        \\})
                    \\}
                \\},
                fail(res) \\{
                    console.log(res); //失败
                \\}
            \\})
        \\}
    \\}
\\}
```

2.下载地址也可以直接使用web-view打开，安卓会跳转到浏览器下载，ios直接可以预览，需在后台配置安全域名。

```
url='https://resource-test.xiuchuan.com/mp_source/car/register.pdf'
// 直接打开下载地址
uni.navigateTo(\\{
	url: `/sub_my/WebView$\\{url\\}`
\\})
```

```
<web-view :src="url"></web-view>
```

3.拼接第三方在线预览链接，使用web-view打开，如：

```
https://previewpdf.mumudev.top/?file=https://resource-test.xiuchuan.com/mp_source/car/register.pdf
```



### 选择图片的坑

chooseImage去掉参数去掉sizeType，避免钉钉报错

utils中封装

```
import store from "@/store/index"

// 选择图片
const chooseImage = () => \\{
  /* 返回一个promise实例化对象 */
  return new Promise((resolve, reject) => \\{
    uni.chooseImage(\\{
      count: 1,
      sourceType: ["album", "camera"],
      success: (res) => \\{
        console.log(res, store.state.login.envType)
        let filePath, dealName
        // 钉钉且不是开发者工具中（预览、真机调试、体验版、正式版）
        if (store.state.login.envType === 3 && !dd.isIDE) \\{
          // 可以作为img标签的src属性显示图片
          filePath = res.files[0].path.slice(0, -5) + res.files[0].fileType
          dealName = filePath.replace("https://resource/", "").toLowerCase();
        \\} else if (store.state.login.envType === 4) \\{
          // 网页版
          filePath = res.tempFilePaths[0]
          dealName = res.tempFiles[0].name;
        \\} else \\{
          // 微信/企微/钉钉开发者工具
          filePath = res.tempFilePaths[0]
          dealName = filePath.replace("http://tmp/", "").toLowerCase();
        \\}
        console.log(filePath, dealName)
        resolve([filePath, dealName])
      \\},
      fail: (err) => \\{
        reject(err)
      \\}
    \\})
  \\})
\\}

module.exports = \\{
  chooseImage
\\}
```

页面中调用

```
		import Utils from "@/utils/index";

		// 上传oss
        async uploadOSS(index) \\{
            const [filePath, dealName] = await Utils.chooseImage();
            console.log(filePath, dealName)
            uni.showLoading(\\{
                title: "图片上传中",
            \\});
            const res = await $http.getUploadOSS(\\{
                name: dealName,
                type: 2,
            \\});
            const _this = this
            uni.uploadFile(\\{
                url: res.host,
                filePath,
                name: "file",
                // 钉钉多传两个参数
                fileType: "image",
                fileName: "file",
                formData: \\{
                    "x:source_name": res.source_name,
                    key: res.path + res.name,
                    OSSAccessKeyId: res.accessid,
                    signature: res.signature,
                    policy: res.policy,
                    callback: res.callback,
                \\},
                success(res) \\{
                    let data = JSON.parse(res.data);
                    _this.formModel.other_amount[index].file_id =
                        data.data.id;
                    _this.formModel.other_amount[index].url = filePath;
                \\},
                fail(err) \\{
                    console.log(err);
                \\},
                complete(res) \\{
                    console.log(res);
                    uni.hideLoading();
                \\},
            \\});
        \\},
```



###  js中使用Promise同步resolve返回多个参数的解决办法

```
resolve([filePath, dealName])

async uploadOSS(index) \\{
    const [filePath, dealName] = await Utils.chooseImage();
    console.log(filePath, dealName)
\\}
```



### 更新钉钉小程序

小程序更新机制

开发者在开发者后台发布新版本之后，并不是用户就会立即使用到最新版的小程序。针对小程序版本的更新，钉钉小程序提供了不同的更新机制。 

小程序每次**冷启动**时，都会检查是否有更新版本，如果发现有新版本，将会异步下载新版本的代码包，并同时用客户端本地的包进行启动，即新版本的小程序需要等下一次冷启动才会应用上。如果距离上一次更新版本超过 48 小时，则会等待新版本的代码包被下载后，直接使用新版本启动。 

#### 1.手动更新

钉钉小程序发布后，手机端在24小时内还会默认使用旧的版本，如果需要立即使用新版本，请使用以下方法手动更新：

1.通过钉钉工作台打开小程序，使用小程序关闭按钮关闭，重新进入小程序

2.可以退出钉钉登录账户,并杀掉钉钉进程,这样再进去后就是直接访问的最新版本了

3.我的-设置-通用-一键清理，重新进入小程序即可（管用）

#### 2.onLaunch中代码自动触发

```
		// 钉钉更新版本
		update() \\{
			const updateManager = dd.getUpdateManager()
			updateManager.onCheckForUpdate(function (res) \\{
				// 请求完新版本信息的回调
				console.log(res)
				if (res.hasUpdate) \\{
					// 如果有新版
					dd.showLoading(\\{
						content: '正在获取新版本中...',
					\\});
					updateManager.onUpdateReady(function (ret) \\{
						console.log(ret.version) // 更新版本号
						dd.hideLoading()
						dd.confirm(\\{
							title: '更新提示',
							content: '新版本已经准备好，是否重启应用？',
							success: function (res) \\{
								if (res.confirm) \\{
									// 新的版本已经下载好，调用 applyUpdate 应用新版本并重启
									updateManager.applyUpdate()
								\\}
							\\}
						\\})
					\\})
				\\}
			\\})
			updateManager.onUpdateFailed(function () \\{
				// 新版本下载失败
				dd.hideLoading()
				dd.alert(\\{
					title: '新版本下载失败，请重启钉钉后重试！',
					buttonText: '我知道了',
					success: () => \\{ \\},
				\\})
			\\})
		\\},
```

这代码写的没问题，问题是即使你有新版上线了，若非冷启动，onCheckForUpdate也检查不到新版本。若冷启动，钉钉又可以自动更新小程序，那还要这一大串代码干啥嘞![表情包](https://g.csdnimg.cn/static/face/emoji/010.png) （有的手机有效）

### 钉钉小程序禁止下拉

```
	// 部分页面可用下拉
	\\{
        "path": "pages/index/index",
        "style": \\{
            "navigationBarTitleText": "首页",
            "enablePullDownRefresh": true,
            "mp-alipay": \\{
            	"allowsBounceVertical": "YES"
            \\}
        \\}
    \\},
	// 全局禁用下拉
	"globalStyle": \\{
		"mp-alipay": \\{
			"allowsBounceVertical": "NO"
		\\}
	\\}
```



### 钉钉小程序checkbox大小不好调

```
// 兼容钉钉
checkbox \\{
    border-radius: 50\\%;
    transform: scale(0.8);
\\}
```



### 钉钉输入框默认会高一点，因为默认有padding

```
input \\{
    width: 100\\%;
    height: 100\\%;
    // 兼容钉钉
    padding: 0;
    margin-left: 8rpx;
    font-size: 28rpx;
    background: #f5f7fa;
\\}
```



### 钉钉为了让地图视野移动到指定地点

```
<map id="myMap"
    :latitude="location.latitude"
    :longitude="location.longitude"
    :include-points="points"
    scale="17"
    show-location
    @regionchange="regionchange">
</map>

// 其他平台自动移动视野
this.location = location
if (this.envType === 3) \\{
    // 钉钉为了让地图视野移动到该地点
    this.points = [location]
\\}
```

