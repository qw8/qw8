---
title: uniapp
date: 2023-04-25 18:03:10
categories: 
- 前端知识
tags:
- uniapp
- 小程序
---

### 小技巧

右击“新建页面“可以直接创建xx文件夹和xx.vue并配置好pages.json，可以自定义模板如下：

```
<template>
    <view>

    </view>
</template>

<script>
export default \\{
    data() \\{
        return \\{\\};
    \\},
    components: \\{\\},
    onLoad(options) \\{\\},
    onShow() \\{\\},
    methods: \\{\\},
\\};
</script>

<style lang="scss" scoped>

</style>
```



### 小问题

- uniapp登录并不会执行App.vue中的onlunch，因为onlunch是进入小程序执行一次，onlunch后才能看到登录页

- switch、delete等是关键词，不能用作方法名，不然打死也找不到为什么报错o(╥﹏╥)o

- 在小程序中尽量避免使用cursor: pointer;会导致点击时会出现淡蓝色背景，打死找不到原因o(╥﹏╥)o

- 刚配置完pages.json里的页面后跳转该页不显示？在Hbuilder中重新运行一下项目就好了

- 固定尺寸图标不能只设置宽度用mode="widthFix"，这样真机首次进入会闪烁（高度拉伸），只能同时设置宽高

- 微信小程序底部tabBar一般通过switchTab进行跳转，但该api无法传参； 可以使用reLaunch进行跳转，它也可以跳转到tabBar，且可以传参，当然注意它会关闭其他页面

- iPhoneX等机型安全区高度都是34

  ```
  :style="\\{ 'padding-bottom': systemInfo.safeAreaInsets.bottom + 'px'\\}"
  ```

- 缺少平台 h5 插件（一定要cnpm安装）

  ```
  cnpm install @dcloudio/uni-h5 --save
  ```

- :style 不支持模板字符串如 `top:$\\{headerHeight\\}px` 的语法

```
单字符如top可写为
:style="\\{ top: headerHeight + 'px' \\}
双字符padding-bottom不加引号会报错，可写为
:style="\\{ 'padding-bottom': safeAreaHeight + 'px', height: calc(100\\% - navHeight+'px') \\}"
:style="\\{'padding-top':160+systemInfo.statusBarHeight+'px','padding-bottom':envType===4?'60px':'0'\\}"
```



### uniapp创建步骤

1.新建-项目-选择模板-创建

2.manifest.json中

基础配置-填写名称、描述

web配置-基础路径填“./”，部署H5到相对路径（本地可以打开）

微信小程序配置-填写appid、勾选样式补全和自动压缩



### uniapp运行步骤

1. 项目拖动到HBuilderX打开
2. HBuilderX插件市场安装sass、less
3. 打开微信开发者工具扫码登录（微信开发者平台需要加入项目组），在左上角选择设置 > 安全设置， 开启服务端口即可
4. HBuilderX打开首页代码，点击“运行”--“运行到小程序模拟器”--“微信开发者工具”
5. 等待微信开发者工具启动，点击项目，等待加载完成即可看到页面
6. h5：点击“运行”--“运行到浏览器”--“chome”
7. h5打包：点击“发行”--“网站-PC”



### uniapp公共图片路径封装及使用

config.js

```
imgUrl: 'https://xxx.xxx.com/xxx/images/', // 服务器图片路径
```

#### 方法1.使用Vue.prototype，每个页改动代码较少，推荐使用

main.js

```
// 返回公共图片路径
Vue.prototype.getSrc = function (img) \\{
  return Config.imgUrl + img;
\\}
```

页面中

```
<image :src="getSrc('account_checked@2x.png')" />
```

#### 方法2.只使用config，缺点：每个页改动代码较多

```
<image :src="imgUrl+'login-bg@2x.png'"></image>

import Config from '@/config'

data() \\{
        return \\{
            imgUrl: Config.imgUrl, // 图片地址
        \\}
    \\},
```



### success内部不写_this简化代码

官网示例

```
uni.removeStorage(\\{
	key: 'storage_key',
	success: function (res) \\{
		console.log('success');
	\\}
\\});
```

实际使用因为success函数内部无法获取this.historicalLocation报错，只能let _this = this

```
			let _this = this
            uni.removeStorage(\\{
                key: 'historicalLocation',
                success(res) \\{
                    _this.historicalLocation = []
                \\}
            \\})
```

优化：将success函数改为箭头函数，就不需要再let _this = this了

```
			uni.removeStorage(\\{
                key: 'historicalLocation',
                success: (res) => \\{
                    this.historicalLocation = []
                \\}
            \\})
```

很简单，但很实用！官网所有success的函数都可以这样使用。



### await可以获取函数返回值

```
async function echo(arg) \\{  
	return arg;
\\}
async function getValue() \\{
	const res = await echo(5);
    console.log(res);
\\}

getValue();
```




### uniapp中使用calc计算的坑

错误写法：

```
height: calc(100vh-100rpx)
```

正确写法:

```
height: calc(100vh - 100rpx)
```

睁大眼睛找不同，有没有发现在calc中“100vh”和“100rpx”与中间“-”加了个空格，对，就是这么坑，我之前以为uniapp不支持calc计算不同单位呢，后来才发现这个坑。



### uni-app 部署 H5 到相对路径（含file协议打开）

自 HBuilderX 2.6.6 版本开始，uni-app 支持部署 H5 到相对路径，部署到服务端或在本地（使用file协议）打开均可。

#### 使用方式

配置 manifest.json 配置 h5->router->base 值为 "./" 部署到相对路径

#### 注意事项

按相对路径发行时路由模式强制为hash模式，不支持history模式（两者相悖）。



### uniapp阻止遮罩滚动穿透

```
<view class="mask" @touchmove.stop.prevent="moveHandle">

methods:\\{
    moveHandle()\\{
		return
	\\},
\\}
```



### 填入字符不能包含<>/（防止xss攻击）

```
//main.js中
Vue.prototype.inputFilter = function(text) \\{
	// 规则对象(reg)
	let reg = new RegExp("[<>/]")
	if (reg.test(text)) \\{
		uni.showToast(\\{
			icon: 'none',
			duration: 3000,
			title: '填入字符不能包含<>/'
		\\})
		return true;
	\\}
	return false;
\\}

// 页面中函数内使用
// 填入字符不能包含<>/
if (this.inputFilter(this.value)) \\{
	return false
\\}
//如果要验证数组对象中多个值
let flag = false
bodyList.forEach(item => \\{
	if (this.inputFilter(item.memo)) \\{
		flag = true
	\\}
\\})
if (flag) \\{
	return
\\}
```



### 全屏播放视频

```
<video id="myVideo" class="home_video" loop autoplay show-center-play-btn :src="articleData.content"
			:controls="false" :object-fit="fit" @loadedmetadata="getSize"></video>

data中
fit: 'fill', // 默认竖屏播放（填充）

// 获取视频宽高时长
getSize(e) \\{
	const \\{ width, height, duration \\} = e.detail
	// 如果宽大于高，横屏播放（包含）
	if (width > height) \\{
		this.fit = 'contain'
	\\}
	// console.log(width, height, duration, this.fit)
\\},
```



###  每日登录领红包

父组件中

```
<!-- 签到弹窗组件 -->
<popup v-if="signIn" :isShowDialog="isShowDialog" :operation="operation" @sonClose="close" @sonReceive="receive"></popup>
```

弹窗组件中

```
methods: \\{
			// 关闭弹窗后今日不再提醒
			dialogClose() \\{
				this.$emit("sonClose", false); //其中function为父组件定义函数，param为需要传递参数
				try \\{
					uni.setStorageSync('signInDate', new Date().toLocaleDateString());
				\\} catch (e) \\{
					console.log(e)
				\\}
			\\},
			// 登录领取福利
			async receive() \\{
				const \\{ data \\} = await signInRedPacket()
				try \\{
					uni.setStorageSync('signInDate', new Date().toLocaleDateString());
				\\} catch (e) \\{
					console.log(e)
				\\}
				console.log(data)
				if (data) \\{
					this.credit = data.credit;
					setTimeout(() => \\{
						this.operation = 2;
						this.$emit("sonReceive", this.operation); //其中function为父组件定义函数，param为需要传递参数
					\\}, 100);
				\\}
			\\},
		\\},
```

在App.vue中onLaunch生命周期函数中

```
			// 每日签到判断
			everydaySignIn() \\{
				try \\{
					const signInDate = uni.getStorageSync('signInDate');
					if (signInDate) \\{
						const today = new Date().toLocaleDateString()
						if (today <= signInDate) \\{
							console.log(signInDate, today, "不可以签到");
							this.$store.commit('everydaySignIn', false)
						\\}
					\\}
				\\} catch (e) \\{
					console.log(e)
				\\}
			\\}
```



### 防止多次提交或点击

```
if (this.noClick) \\{
	// 第一次点击
    this.noClick = false;
    console.log(this.noClick)
    const res = await saveReceiver(this.form)
    if (res.code === 0) \\{
    	uni.navigateBack()
    \\} else \\{
        uni.showToast(\\{
            icon: 'none',
            title: '添加失败'
    	\\})
	\\}
    setTimeout(() => \\{
        this.noClick = true;
        console.log(this.noClick)
    \\}, 2000)
\\}
```



### 返回顶部按钮

```
<template>
   <view class="toTop" @tap="toTop" :style="\\{'display':(flag? 'block':'none')\\}">
			<image src="../../static/icon/toTop.png" mode="widthFix"></image>
		</view>
</template>

<script>
    export default \\{
        data() \\{
            return \\{
                flag: false // 是否显示回顶按钮
            \\}
        \\},
        methods: \\{
           // 返回顶部
			toTop() \\{
				uni.pageScrollTo(\\{
					scrollTop: 0
				\\});
			\\},
			// 当距离大于800时显示回到顶部按钮
			onPageScroll(e) \\{
				if (e.scrollTop > 800) \\{
					this.flag = true
				\\} else \\{
					this.flag = false
				\\}
			\\}
        \\}
    \\}
</script>

<style>
    .toTop \\{
		position: fixed;
		z-index: 999;
		right: 20rpx;
		bottom: 200rpx;
		transition: transform 0.8s ease-in;

		image \\{
			width: 80rpx;
		\\}
	\\}
</style>
```



### 跳转页面传对象

```
// 传递
goSystemNotice(content) \\{
	uni.navigateTo(\\{
		url: `/pages/message/systemNotice?content=$\\{JSON.stringify(content)\\}`
	\\})
\\}
// 接收
onLoad(option) \\{
	this.content = JSON.parse(option.content)
\\}
```



### uniapp保存网络图片

```
// 预览长按保存到相册
			preview(pic) \\{
				uni.previewImage(\\{
					urls: [pic],
					// 长按图片显示操作菜单
					longPressActions: \\{
						itemList: ['保存图片'],
						success: (data) => \\{
							//先下载到本地获取临时路径
							uni.downloadFile(\\{
								url: pic,
								success: (res) => \\{
									console.log('下载成功', res.tempFilePath)
									//将临时路径保存到相册，即可在相册中查看图片
									uni.saveImageToPhotosAlbum(\\{
										filePath: res.tempFilePath, //不支持网络地址
										success: function() \\{
											uni.showToast(\\{
												title: '保存图片到相册成功',
												position: 'bottom'
											\\});
										\\}
									\\});
								\\},
								fail: (err) => \\{
									console.log('下载失败', err)
								\\}
							\\})
						\\},
						fail: function(err) \\{
							console.log(err.errMsg);
						\\}
					\\}
				\\})
			\\}
```



### .gitignore文件忽略提交unpackage包到github仓库（uni-app）

pull代码下来，然而unpackage文件一直说有东西重复了，让我删除掉先，应该是同事提交了unpackage包上去了，所以我们就来解决这个问题。

1、要怎么样把远程分支上的unpackage包给删除掉？

```
git rm -r --cached unpackage
```

（本地的目录还在，直接关闭软件删除unpackage目录）

2、要怎么要每次提交都忽略unpackage等文件？

根目录新建.gitignore文件

然后记事本打开，复制粘贴以下内容进去就完事了

```
node_modules/
.project
unpackage/
.DS_Store
```

3、git提交，push一下即可。



### uni-app把canvas的px像素使用rpx表示

小程序，移动端在设置canvas的位置的时候，因为cnavas默认是px像素，对于位置的设置很不方便，所以要把px转换为用rpx表示

1、获取设备宽度

```
const system = uni.getSystemInfoSync()
```

2、单位换算，算出1rpx = 多少px

```
const w = system.windowWidth / 750
```

3、使用

比如我要设置30rpx，则可以表为 30*w



### canvas绘制多行文本自动换行

```js
/**
	 * 绘制多行文本自动换行
	 * ctx canvas对象
	 * text 文本内容
	 * leftWidth 距离左侧的距离
	 * initHeight 距离顶部的距离
	 * textWidth 文本的宽度
	 */
	drawText (text, leftWidth, initHeight, ctx, textWidth) \\{
	    let lineWidth = 0;
	    let lastSubStrIndex = 0; //每次开始截取的字符串的索引
		const rpx = this.windowWidth / 750;
	    for (let i = 0; i < text.length; i++) \\{
	        lineWidth += ctx.measureText(text[i]).width;
	        //16是一个中文宽度，为了解决偶尔夹有数字或英文时，文字长度超出设置宽度的bug
	        if (lineWidth > textWidth - 16) \\{
	            ctx.fillText(text.substring(lastSubStrIndex, i + 1), leftWidth, initHeight); //绘制截取部分
	            initHeight += 48 * rpx;
	            lineWidth = 0;
	            lastSubStrIndex = i + 1;
	        \\}
	        if (i === text.length - 1) \\{
	            ctx.fillText(text.substring(lastSubStrIndex, i + 1), leftWidth, initHeight); //绘制剩余部分
	        \\}
	    \\}
		ctx.fillText("谢谢。", 40 * rpx, initHeight + 48 * rpx);
	\\},
```




### canvas设置字间距（真机不生效）、文字加粗

```
<canvas
        class="my-canvas"
        canvas-id="myCanvas"
        @click="saveSharePic('canvas')"
></canvas>

context.font = "bold 16px PingFangSC-Medium, PingFang SC";

.my-canvas \\{
	letter-spacing: 2rpx;
\\}
```



### 文字地址使用微信内置地图查看位置 

```
	import Config from "@/config.js";
	import QQMapWX from "@/utils/qqmap-wx-jssdk.min.js"

	//点击查看地址
    viewAddress(address) \\{
		// 实例化腾讯地图API核心类
		const tMap = new QQMapWX(\\{
			key: Config.mapKey // 开发者密钥
		\\});
		// 调用地址解析接口
		tMap.geocoder(\\{
			address, //地址参数，例：address: '北京市海淀区彩和坊路海淀西大街74号'
			success: function(res) \\{
				// console.log(res);
				uni.openLocation(\\{
					latitude: res.result.location.lat, // 纬度，范围为-90~90，负数表示南纬
					longitude: res.result.location.lng, // 经度，范围为-180~180，负数表示西经
					name: res.result.title, // 位置名
					address, // 地址的详细说明
					scale: 17, // 缩放比例，范围5~18，默认为18
					success: function(res)\\{
						// success
					\\},
					fail: function() \\{
						// fail
					\\},
				\\})
			\\},
			fail: function(res) \\{
				// console.log(res);
				uni.showToast(\\{
					title: "该地址无法定位",
					icon: "none",
					duration: 2000
				\\});
			\\}
		\\});
    \\},
```

在manifest.json中添加以下代码，并在小程序后台申请getLocation权限（审核1-2天）

```
"mp-weixin" : \\{
        "permission" : \\{
            "scope.userLocation" : \\{
                "desc" : "将获取您的位置信息，用于查看地址功能"
            \\}
        \\},
		"requiredPrivateInfos" : [ "getLocation" ]
    \\},
```



### 开启小程序在前后台时均可接收位置消息

开发工具需要清除全部缓存，重新编译，才能获取权限

真机需要到小程序设置中位置信息选择“使用小程序时和离开后”

```
		"requiredBackgroundModes": [
            "location"
        ],
        "requiredPrivateInfos": [
            "getLocation",
            "onLocationChange",
            "startLocationUpdate",
            "startLocationUpdateBackground"
        ]
```



### js计算两个经纬度点之间距离

```
		// 计算两点之间直线距离
        algorithm(point1, point2) \\{
            let \\{ latitude: x1, longitude: y1 \\} = point1
            let \\{ latitude: x2, longitude: y2 \\} = point2
            console.log(x1, y1, x2, y2)
            // 纬度
            let Lat1 = this.rad(x1)
            let Lat2 = this.rad(x2)
            let a = Lat1 - Lat2 // 两点纬度之差
            let b = this.rad(y1) - this.rad(y2) // 经度之差
            let s =
                2 *
                Math.asin(
                    Math.sqrt(
                        Math.pow(Math.sin(a / 2), 2) +
                            Math.cos(Lat1) *
                                Math.cos(Lat2) *
                                Math.pow(Math.sin(b / 2), 2)
                    )
                )
            // 计算两点距离的公式
            // 弧长等于弧度乘地球半径（半径为米）
            s = s * 6378137.0
            // 精确距离的数值
            s = Math.round(s * 10000) / 10000
            return s
        \\},
        // 角度转换成弧度
        rad(d) \\{
            return (d * Math.PI) / 180.0
        \\},
```

自己与腾讯地图分别计算两点距离，8km，自己计算比腾讯多了10m



### js计算多个经纬度点之间距离

```
		// 计算实时路径总距离
        calculateDistance() \\{
            let sum = 0,
                points = this.points
            // let points = [
            //     \\{ latitude: 40.040452, longitude: 116.273486 \\},
            //     \\{ latitude: 40.00654, longitude: 116.303695 \\},
            //     \\{ latitude: 39.8664564344618, longitude: 116.3070187717014 \\}
            // ]
            if (points.length >= 2) \\{
                for (let i = 0; i < points.length - 1; i++) \\{
                    sum += this.algorithm(points[i], points[i + 1])
                \\}
            \\}
            this.sum = sum
        \\},
```



### 小程序地图画路线测试结果

北京到深圳2000km，最多10w个点的话，可以设置20m一个点
距离：都可以计算，7w多km
真机本地存储：最多15185个，石家庄站到喀什站-2次
画图，10w个耗时10秒左右，不过存在有性能问题-8次
14w个可以画图-12次
17w个可以画图-14次
（n次表示漠河站到喀什站路径规划，返回值push的循环次数）

比例尺是根据图上距离*比例尺计算实际距离，图上距离和比例尺都无法获取，无法计算实际距离
比例尺1:1000000，图上的距离是12.5厘米
实际距离12.5cm x 1000000 = 12500000cm = 125000m = 125km

开发工具57980个，setData数据传输长度为 8322KB，8.12MB，存在有性能问题！-5次
漠河站到喀什站5898002/3=1966000个数组，腾讯23611个，距离误差15km
北京到吕梁672178/3=224059个数组，腾讯3860个



### 小程序其他样式需覆盖地图

根据实际情况，使用position的三个属性。（使用z-index不生效）

```
position: relative;
position: absolute;
position: fixed;
```



### 地图选点

```
        <map id="myMap"
            :latitude="location.latitude"
            :longitude="location.longitude"
            scale="17"
            show-location
            @regionchange="regionchange">
        </map>
            
        // 视野发生变化
        regionchange(e) \\{
            console.log('视野发生变化', e)
            if (e.type === 'end') \\{
                this.mapCtx.getCenterLocation(\\{
                    success: (res) => \\{
                        console.log('地图中心的经纬度', res)
                        this.getAddress(res.latitude, res.longitude)
                    \\},
                    fail: (err) => \\{
                        console.log(err)
                    \\}
                \\})
            \\}
        \\},
```



### 地图高度动态调整

```
			<!-- 地图 -->
            <map id="myMap"
                :latitude="latitude"
                :longitude="longitude"
                :markers="markers"
                :polyline="polyline"
                scale="17"
                show-location
                style="width: 100\\%;"
                :style="\\{ height: mapHeight + 'px' \\}">
            </map>

		<view :class="envType === 4?'operation operation-web':'operation operation-mp'"
                v-else
                id="operation">
                <view class="back"
                    @click="goBack">
                    <image class="back-img"
                        src="/static/images/index_icon12.png" />
                </view>
                <view class="input-area">
                    <view class="button"
                        @click="reverse">
                        <image src="/static/images/index_icon1.png" />
                    </view>
                    <view class="input-content">
                        <view class="input-item"
                            v-for="(item, index) in tripList"
                            :key="index">
                            <view class="prefix"
                                v-if="index === 0">
                                <view class="kong"></view>
                                <view class="cricle start"></view>
                                <view class="line"></view>
                            </view>
                            <view class="prefix"
                                v-else-if="index === tripList.length - 1">
                                <view class="line"></view>
                                <view class="cricle end"></view>
                                <view class="kong"></view>
                            </view>
                            <view class="prefix"
                                v-else>
                                <view class="line"></view>
                                <view class="index">\\\{\\\{ index\\\}\\\} }}</view>
                                <view class="line"></view>
                            </view>
                            <view :class="item ? 'input' : 'input placeholder'"
                                @click="onClick"
                                v-if="index === 0">
                                \\\{\\\{ item?item: "请输入起点" \\\}\\\}</view>
                            <view :class="item ? 'input' : 'input placeholder'"
                                @click="onClick"
                                v-else-if="index === tripList.length - 1">\\\{\\\{ item?item: "请输入终点" \\\}\\\}</view>
                            <view :class="item ? 'input' : 'input placeholder'"
                                @click="onClick"
                                v-else>\\\{\\\{ item?item: "请输入途径点" \\\}\\\}
                            </view>
                        </view>
                    </view>
                    <view class="button"
                        @click="onClick(1)">
                        <image src="/static/images/index_icon2.png" />
                    </view>
                </view>
                <view class="add-trip"
                    @click="onClick">添加行程</view>
            </view>


        mapHeight: 400, // 地图高度响应式

        // 设置地图高度
        this.setMapHeight()
		// 设置地图高度
        setMapHeight() \\{
            if (this.token && this.userInfo.travel_type !== 0) \\{
                // 设备模式/仪表盘模式/手机GPS模式
                this.mapHeight = this.systemInfo.windowHeight
            \\} else \\{
                const query = uni.createSelectorQuery()
                query.select('#operation').boundingClientRect()
                query.selectViewport().scrollOffset()
                query.exec((res) => \\{
                    console.log('操作区dom', res)
                    if (res[0]) \\{
                        // 防止切换到设备模式没有操作区dom报错
                        if (this.envType === 3) \\{
                            // 钉钉无法隐藏地图水印
                            this.mapHeight =
                                this.systemInfo.windowHeight - res[0].height
                        \\} else \\{
                            // 地图高度=可使用窗口高度-输入框区域高度+地图水印高度
                            this.mapHeight =
                                this.systemInfo.windowHeight -
                                res[0].height +
                                22
                        \\}
                        console.log(
                            this.systemInfo.windowHeight,
                            res[0].height,
                            this.mapHeight
                        )
                    \\}
                \\})
            \\}
        \\},
        // 数组反转
        reverse() \\{
            this.tripList = this.tripList.reverse()
            this.$store.commit('setAddTripList', this.tripList)
            console.log(this.tripList)
        \\},
        // 点击添加行程
        onClick: Utils.throttle(function (isAdd) \\{
            console.log('点击事件随机值' + Math.random())
            this.addTrip(isAdd)
        \\}, 2000),
        // 添加行程
        async addTrip(isAdd) \\{
        		// 如果点击+号，添加一个途经点
                const url =
                    isAdd === 1
                        ? `/sub_trip/trip/SetTrip?isAdd=$\\{isAdd\\}`
                        : '/sub_trip/trip/SetTrip'
                uni.navigateTo(\\{
                    url
                \\})
        \\},


// pc样式
.pc \\{
    .operation \\{
        .add-trip \\{
            width: calc(100\\% - 16px);
        \\}
        .input-area \\{
            .input-content \\{
                width: 100\\%;
                .input-item .input \\{
                    width: 100\\%;
                \\}
            \\}
        \\}
    \\}
\\}
.operation-web \\{
    bottom: 50px;
\\}
.operation-mp \\{
    bottom: 0;
\\}
.operation \\{
    width: 100\\%;
    min-height: 222rpx;
    padding: 32rpx;
    box-sizing: border-box;
    position: absolute;
    background: #f5f7fa;
    box-shadow: 0 0 80rpx 0 rgba(0, 0, 0, 0.08);
    border-radius: 24rpx 24rpx 0 0;

    .input-area \\{
        border-radius: 16rpx;
        display: flex;
        align-items: center;
        background: #fff;

        // 扩大点击热区
        .button \\{
            width: 88rpx;
            min-height: 88rpx;
            padding: 0 16rpx;
            box-sizing: border-box;
            display: flex;
            align-items: center;
            image \\{
                width: 40rpx;
                height: 40rpx;
            \\}
        \\}

        .input-content \\{
            width: 558rpx;
            padding: 0 8rpx;
            box-sizing: border-box;
            display: flex;
            flex-direction: column;

            .input-item \\{
                height: 90rpx;
                display: flex;
                align-items: center;

                .input \\{
                    width: 486rpx;
                    height: 88rpx;
                    line-height: 88rpx;
                    border-bottom: solid 2rpx #f0f2f5;
                    white-space: nowrap;
                    overflow: hidden;
                    text-overflow: ellipsis;
                \\}
            \\}
            .kong \\{
                width: 2rpx;
                height: 37rpx;
            \\}

            .line \\{
                height: 37rpx;
                border-left: dashed 2rpx #e6e8eb;
                box-shadow: 0 0 80rpx 0 rgba(0, 0, 0, 0.08);
            \\}

            .index \\{
                width: 24rpx;
                height: 24rpx;
                line-height: 24rpx;
                font-size: 18rpx;
                border-radius: 50\\%;
                text-align: center;
                color: #fff;
                background: #c9ccd1;
                box-shadow: 0 0 80rpx 0 rgba(0, 0, 0, 0.08);
            \\}
        \\}
    \\}

    .back \\{
        /* 去掉水印高度 */
        top: -104rpx;
    \\}
    .add-trip \\{
        width: 686rpx;
        margin-top: 32rpx;
    \\}
\\}
```



### 小程序拖拽排序

页面

```
					<view class="trip-list">
                        <!-- 克隆当前拖拽的项 -->
                        <view class="trip-item kelong"
                            v-if="showkelong"
                            :style="\\{ top: top + 'px' \\}">
                            <view class="trip-input-area">
                                <view class="cricle channel"></view>
                                <input v-model="kelong"
                                    placeholder="请输入地点" />
                                <image class="small img"
                                    src="/static/images/index_icon3.png"></image>
                            </view>
                        </view>
                        <!-- 原来各项 -->
                        <view class="trip-item"
                            v-for="(item, index) in tripList"
                            :key="index">
                            <view class="trip-input-area">
                                <view v-if="index === 0"
                                    class="cricle start"></view>
                                <view v-else-if="index === tripList.length - 1"
                                    class="cricle end"></view>
                                <view v-else
                                    class="cricle channel"></view>
                                <input v-if="index === 0"
                                    :value="item"
                                    @input="getsuggest"
                                    @focus="focus(index)"
                                    placeholder="请输入起点"
                                    maxlength="32"
                                    :auto-focus="autoFocus[0]" />
                                <input v-else-if="index === tripList.length - 1"
                                    :value="item"
                                    @input="getsuggest"
                                    @focus="focus(index)"
                                    placeholder="请输入终点"
                                    maxlength="32"
                                    :auto-focus="autoFocus[1]" />
                                <input v-else
                                    :value="item"
                                    @input="getsuggest"
                                    @focus="focus(index)"
                                    placeholder="请输入途径点"
                                    maxlength="32" />
                                <!-- 拖拽节点 -->
                                <view class="drag"
                                    :id="index"
                                    @touchstart='dragStart'
                                    @touchmove='dragMove'
                                    @touchend='dragEnd'>
                                    <image class="small img"
                                        src="/static/images/index_icon3.png"></image>
                                </view>
                            </view>
                            <view class="del"
                                v-if="tripList.length > 2"
                                @click="delSpot(index)">
                                <image class="small "
                                    src="/static/images/index_icon4.png"></image>
                            </view>
                        </view>
                    </view>
```

js

```
        kelong: '', // 当前拖拽项的克隆
        mkelong: \\{\\}, // 当前拖拽项的克隆(标记点)
        startTop: 0, //拖拽开始时克隆项距离class=tripList节点顶部边界的值
        top: 0, // 当前拖拽项的top
        selectedIndex: -1, //被选择拖拽的项的index
        showkelong: false, //是否显示克隆项
            
		// 拖拽开始
        dragStart(e) \\{
            // 当前拖拽项的索引index
            let index = e.currentTarget.id
            // 把当前拖拽项的内容复制给kelong
            this.kelong = this.tripList[index]
            this.mkelong = this.markers[index]
            this.selectedIndex = index
            this.showkelong = true
            console.log('拖拽开始index=', index, 'kelong=', this.kelong, e)
            let query = uni.createSelectorQuery() // 创建节点查询器 quer
            //选择class=tripList的节点，获取节点位置信息的查询请求
            query
                .select('.trip-list')
                .boundingClientRect((rect) => \\{
                    console.log(rect)
                    this.top = e.changedTouches[0].clientY - rect.top - 22
                    this.startTop = this.top
                \\})
                .exec()
        \\},
        // 拖拽移动
        dragMove(e) \\{
            // console.log("拖拽移动", e);
            let query = uni.createSelectorQuery()
            let top = this.top
            query
                .select('.trip-list')
                .boundingClientRect((rect) => \\{
                    top = e.changedTouches[0].clientY - rect.top - 22
                    if (top < 0) \\{
                        // 顶部边界控制：控制克隆项不会拖拽出class=tripList节点的顶部边界
                        top = 0
                    \\}
                    this.top = top
                \\})
                .exec()
        \\},
        // 拖拽结束
        dragEnd(e) \\{
            console.log('拖拽结束', e)
            let i = e.currentTarget.id
            let query = uni.createSelectorQuery()
            let kelong = this.kelong
            let mkelong = this.mkelong
            let tripList = this.tripList
            let markers = this.markers
            query
                .select('.trip-list')
                .boundingClientRect((rect) => \\{
                    let top = e.changedTouches[0].clientY - rect.top - 22
                    if (top > rect.height) \\{
                        // 底部边界控制：控制克隆项拖拽结束时不会出class=tripList节点的底部边界
                        top = rect.height - 44
                    \\} else if (top < 0) \\{
                        // 顶部边界控制：控制克隆项拖拽结束时不会出class=tripList节点的顶部边界
                        top = 0
                    \\}
                    this.top = top
                    let target = parseInt(top / 44)
                    let list = [] //用于备份数据
                    let mlist = [] //用于备份数据
                    if (this.startTop > top) \\{
                        //  往上方位置拖拽
                        for (let k = 0; k <= i - target; k++) \\{
                            //  备份插入位置target开始的下方数据，除了拖拽数据项
                            if (tripList[target + k] != kelong) \\{
                                list.push(tripList[target + k])
                            \\}
                            if (markers[target + k] != mkelong) \\{
                                mlist.push(markers[target + k])
                            \\}
                        \\}
                        console.log('往上拖拽 list=======', list)
                        if (list.lenghth != 0) \\{
                            tripList[target] = kelong
                            markers[target] = mkelong
                            for (
                                let m = target + 1, n = 0;
                                n < list.length;
                                m++, n++
                            ) \\{
                                tripList[m] = list[n]
                                markers[m] = mlist[n]
                            \\}
                        \\}
                    \\} else \\{
                        // 往下边位置拖拽
                        for (let k = 1; k <= target - i; k++) \\{
                            //  备份插入位置target开始的上方数据，除了拖拽数据项
                            if (tripList[i + k] != kelong) \\{
                                list.push(tripList[i + k])
                            \\}
                            if (markers[i + k] != mkelong) \\{
                                mlist.push(markers[i + k])
                            \\}
                        \\}
                        console.log('往下拖拽 list=======', list)
                        if (list.length != 0) \\{
                            tripList[target] = kelong
                            markers[target] = mkelong
                            for (let m = i, n = 0; n < list.length; m++, n++) \\{
                                tripList[m] = list[n]
                                markers[m] = mlist[n]
                            \\}
                        \\}
                    \\}
                    console.log(tripList, markers)
                    this.tripList = tripList
                    this.markers = markers
                    this.selectedIndex = -1
                    this.showkelong = false
                \\})
                .exec()
        \\}
```

css

```
.trip-list \\{
    position: relative;
    .trip-item \\{
        margin: 0rpx auto;
        width: 100\\%;
        /* height: 60px; */
        height: 44px;
        background-color: #fff;
        position: relative;
        display: flex;
        align-items: center;
        .trip-input-area \\{
            width: 526rpx;
            height: 80rpx;
            padding-left: 16rpx;
            margin: 4rpx 0;
            box-sizing: border-box;
            border-radius: 8rpx;
            display: flex;
            align-items: center;
            position: relative;
            background: #f5f7fa;
            border: solid 1rpx #f0f2f5;
            .cricle \\{
                width: 16rpx;
                height: 16rpx;
                margin-right: 16rpx;
                border-radius: 50\\%;
                box-shadow: 0 0 80rpx 0 rgba(0, 0, 0, 0.08);
            \\}
            .start \\{
                background: #00cc88;
                border: solid 2rpx #00cc88;
            \\}
            .channel \\{
                background: #c9ccd1;
                border: solid 2rpx #c9ccd1;
            \\}
            .end \\{
                background: #f25041;
                border: solid 2rpx #f25041;
            \\}
            input \\{
                width: 420rpx;
                background: #f5f7fa;
            \\}
            .drag \\{
                width: 40rpx;
                height: 56rpx;
                /* 为了扩大可拖拽区域 */
                padding: 16rpx 16rpx 16rpx 0;
            \\}
            .small \\{
                width: 24rpx;
                height: 24rpx;
            \\}
            .img \\{
                position: absolute;
                right: 16rpx;
                top: 28rpx;
                z-index: 2;
            \\}
        \\}
        // 扩大点击热区
        .del \\{
            height: 44px;
            padding-left: 24rpx;
            display: flex;
            align-items: center;
        \\}
    \\}
    .kelong \\{
        width: 526rpx;
        height: 80rpx;
        background: #f5f7fa;
        z-index: 99;
        position: absolute;
        box-shadow: 1px 1px 5px #ccc;
        .trip-input-area \\{
            border: 0;
        \\}
    \\}
\\}
```



### uniapp小程序用deep重写组件样式不生效

deep只在h5中生效，但是在小程序中不生效

解决办法：在method同级下添加：

		methods: \\{
		\\},
		options: \\{
			styleIsolation: 'shared'
		\\}
然后再使用deep就可以了，如：

	/deep/ .u-modal__title \\{
		color: red
	\\}



### 去掉按钮默认边框

```
button::after \\{
  border: none;
  outline: none;
\\}
```



### input组件样式问题

- input组件placeholder-class样式未生效，

```
/deep/.placeholder \\{
	color: #b0b3b8 !important;
\\}
/deep/.err \\{
	color: #f25041 !important;
\\}
```

- input字体大小及样式修改（直接在input里写font-size不生效）

```
<view class="alert">
	<input v-model="formData.imei"
		placeholder-class="placeholder"
		placeholder="请输入设备号" />
</view>

.alert \\{
    font-size: 28rpx;
    input \\{
        padding: 16rpx;
        border-radius: 8rpx;
        background: #f5f7fa;
    \\}
    /deep/ .placeholder \\{
        font-size: 28rpx !important;
    \\}
\\}
```



### v-for循环将index带入class属性中

使用绑定数组写法 

```
<view :class="['item', `img$\\{index + 1\\}`]" v-for="(item,index) in list" :key="item" @click="previewImage(index)">
	<image :src="item" mode="widthFix"></image>
</view>
```



### 自定义导航

优点：样式和功能可以自定义，文字可居中（官方居左）

```
		// 页面级别使用
		\\{
			"path": "file_detail/file_detail",
			"style": \\{
				"navigationBarTitleText": "文件详情",
				"navigationBarTextStyle": "black",
				"navigationBarBackgroundColor": "#ffffff",
				"navigationStyle": "custom"
			\\}
		\\}
		// 全局使用
		"globalStyle": \\{
            "navigationBarTextStyle": "white",
            "navigationBarTitleText": "首页",
            "navigationBarBackgroundColor": "#287eff",
            "backgroundColor": "#F8F8F8",
            "navigationStyle": "custom" //导航栏样式，仅支持 default/custom。
		\\},
```

官方原生的效果肯定比较好好，全局使用自定义导航不太好

比如：页面多了的话，每个页面都需要写导航组件，代码重复；滚动条通顶；塌陷的高度还需要额外处理等缺点。



### getSavedFileList返回fileList为空

wx.getSavedFileList() 是获取【缓存文件】，而 saveFile 存文件操作的是【用户文件】，这是两个不同的文件区划。

https://developers.weixin.qq.com/miniprogram/dev/framework/ability/file-system.html

![img](http://mmbiz.qpic.cn/mmbiz_png/qThSw5b3h8S0fFsh9jB0JFA938QfMrQx5DLNdau88XJCaGc2LMWJemF4DQxKWelbPsFcwASxN2e7yKaaDRACtw/0?wx_fmt=png)

所以应该访问【用户文件】

```
let fs = wx.getFileSystemManager()
fs.readdir(wx.env.USER_DATA_PATH)
```



### 小程序使用downloadFile和saveFile()保存文件在本机找不到文件？

downloadFile和saveFile调用成功后返回的地址都是以wxfile://开头的，这是微信自己的内部存储空间。但是android是可以在本地查询到的：

```
内部存储/Android/data/com.tencent.mm/MicroMsg/wxanewfiles/***/文件名，
```

中间那个***·是个长字符串，不知道是什么规则生成的；ios是无法查询到具体的文件的。



### 文件下载

```
<view class="item" @click="download" v-if="!isDownload">
    <image src="/static/img/icon_download@3x.png" mode="widthFix"></image>
    <text>下载</text>
</view>
<view class="item" @click="viewFile" v-if="isDownload">
    <image src="/static/img/icon_downloaded@3x.png" mode="widthFix"></image>
    <text>已下载</text>
</view>
            
data() \\{
        return \\{
            fs: null, // 文件管理器
            filePath: `$\\{wx.env.USER_DATA_PATH\\}/my/2021_PDF.pdf`, // 文件存放路径
            isDownload: false, // 该文件是否已下载
        \\};
    \\},
    
onLoad(options) \\{
        console.log(options);
        // 获取FileSystemManger的全局唯一文件管理器
        this.fs = uni.getFileSystemManager();
        this.judgeDownload();
    \\},
    
		// 判断文件是否已下载
        judgeDownload() \\{
            const _this = this;
            // 检查本地文件夹是否存在
            this.fs.access(\\{
                path: `$\\{wx.env.USER_DATA_PATH\\}/my`,
                success(res) \\{
                    console.log("有my文件夹", res);
                    // 检查本地该文件是否存在
                    _this.fs.access(\\{
                        path: _this.filePath,
                        success(res) \\{
                            console.log("有该文件", res);
                            _this.isDownload = true;
                        \\},
                        fail(err) \\{
                            console.log("没有该文件", err);
                        \\},
                    \\});
                    // 文件列表中可以用这个判断
                    // _this.fs.readdir(\\{
                    //     dirPath: `$\\{wx.env.USER_DATA_PATH\\}/my`,
                    //     success(res) \\{
                    //         console.log(res, "用户本地my目录文件列表");
                    //     \\},
                    //     fail(res) \\{
                    //         console.error(res);
                    //     \\},
                    // \\});
                \\},
                fail(err) \\{
                    console.log("没my有文件夹", err);
                    // 不存在执行创建文件夹，便于后续下载
                    _this.mkdir();
                \\},
            \\});
            console.log(wx.env.USER_DATA_PATH);
        \\},
        // 创建文件夹，便于区分本小程序下载的文件
        mkdir() \\{
            this.fs.mkdir(\\{
                dirPath: `$\\{wx.env.USER_DATA_PATH\\}/my`,
                success(res) \\{
                    console.log("创建文件夹成功", res);
                \\},
                fail(err) \\{
                    console.log("创建文件夹失败", err);
                \\},
            \\});
        \\},
        
		// 下载文件
        download() \\{
            const downloadTask = uni.downloadFile(\\{
                url: "http://www.gov.cn/zhengce/pdfFile/2021_PDF.pdf",
                success: (res) => \\{
                    console.log(res);
                    if (res.statusCode === 200) \\{
                        uni.showToast(\\{
                            title: "下载成功",
                            icon: "none",
                        \\});
                        console.log(res.tempFilePath);
                        // res.filePath和res.tempFilePath路径一致，这样做是为了防止IOS中报错：No tempFilePath
                        const tempFilePath = res.tempFilePath || res.filePath;
                        this.fs.saveFile(\\{
                            tempFilePath,
                            // 临时文件保存到用户本地并且重命名，不加文件名的话会导致下载的文件没有后缀打不开
                            filePath: this.filePath,
                            success: (res) => \\{
                                console.log(res, "本地路径");
                                this.isDownload = true;
                                // 下载后跳转查看
                                this.viewFile();
                            \\},
                            fail: (res) => \\{
                                console.log(res);
                            \\},
                        \\});
                    \\}
                \\},
                fail: (res) => \\{
                    uni.showToast(\\{
                        title: "下载失败，请重试",
                        icon: "none",
                        duration: 2000,
                    \\});
                    console.log(res);
                \\},
                // 接口调用结束
                complete: () => \\{
                    // 关闭进度提示
                    uni.hideLoading();
                    // 取消监听加载进度
                    downloadTask.offProgressUpdate();
                \\},
            \\});
            downloadTask.onProgressUpdate((res) => \\{
                console.log("下载进度" + res.progress);
                uni.showLoading(\\{
                    mask: true, // 显示透明蒙层，防止触摸穿透
                    title: "下载中..." + res.progress + "\\%",
                \\});
                // console.log("已经下载的数据长度" + res.totalBytesWritten);
                // console.log(
                //     "预期需要下载的数据总长度" + res.totalBytesExpectedToWrite
                // );
            \\});
        \\},
        // 查看原文件
        viewFile() \\{
            uni.openDocument(\\{
                filePath: this.filePath,
                showMenu: true,
                success: (res) => \\{
                    console.log("打开文档成功", res);
                \\},
            \\});
        \\},
```

小bug：

文件下载名称不能过长，官方会提示太长导致下载失败；不超过80字可以正常下载，90字就下载失败了

关闭console调试下载失败问题：需要在小程序后台配置downloadFile合法域名（测试、正式两个地址）



### vue3微信小程序预览文件

临时文件名

```
const instructions = () => \\{
  uni.downloadFile(\\{
    url: getFileUrl('front-files/risk-assessment/instructions.docx'),
    success: function (res) \\{
      const filePath = res.tempFilePath
      uni.openDocument(\\{
        filePath,
        showMenu: true,
        success: function (res) \\{
          console.log('打开文档成功')
        \\}
      \\})
    \\}
  \\})
\\}
```

自定义文件名

```
// 风险测评须知，文件预览
const instructions = () => \\{
  uni.downloadFile(\\{
    url: getFileUrl('front-files/risk-assessment/instructions.docx'),
    // 保存到用户本地并且重命名，不加文件名的话会导致下载的文件没有后缀打不开
    filePath: `$\\{wx.env.USER_DATA_PATH\\}/风险测评须知.docx`,
    success: function (res) \\{
      console.log('downloadFile', res)
      if (res.statusCode === 200) \\{
        // 成功
        uni.openDocument(\\{
          filePath: res.filePath, // 要打开的文件路径
          showMenu: true, // 是否显示右上角菜单
          success(res) \\{
            console.log('打开成功', res)
          \\},
          fail(res) \\{
            console.log('打开失败', res)
            uni.showToast(\\{
              title: '打开文件失败',
              icon: 'none'
            \\})
          \\}
        \\})
      \\} else \\{
        // 失败
        uni.showToast(\\{
          title: '获取文件失败',
          icon: 'none'
        \\})
      \\}
    \\}
  \\})
\\}
```



### vue2微信小程序预览文件

```
		// 微信小程序预览文件
        openDocument(url) \\{
            uni.downloadFile(\\{
                url, // 要预览的PDF的地址
                // 保存到用户本地并且重命名，不加文件名的话会导致下载的文件没有后缀打不开
                filePath: `$\\{wx.env.USER_DATA_PATH\\}/$\\{this.protoName\\}.pdf`, // 文件存放路径
                success(res) \\{
                    console.log(res)
                    if (res.statusCode === 200) \\{
                        // 成功
                        uni.openDocument(\\{
                            filePath: res.filePath, // 要打开的文件路径
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
                    console.log(res) //失败
                \\}
            \\})
        \\},
```



### uniapp 子组件监听页面onShow

uniapp 开发的时候，需要子组件监听onShow事件，但是子组件没有办法直接监听onShow，我们可以通过页面监听，当页面监听到以后发送通知，子组件监听通知，收到通知后触发事件就可以了。

页面代码 

```
onShow() \\{
    // 触发全局的自定义事件，用于子组件监听onShow
	uni.$emit('onShow', 1);
\\},
//触底监听
onReachBottom() \\{
	uni.$emit('onReachBottom', 1);
\\},
```

子组件监听

```
mounted() \\{
	// 监听主页面onShow事件
	uni.$on('onShow', function(data) \\{
		console.log(data);
	\\});
	uni.$on('onReachBottom', function(data) \\{
		console.log(data);
	\\});
\\}
// 为了避免重复监听，在组件销毁前，关闭监听
beforeDestroy()\\{
	uni.$off('onReachBottom')
	uni.$off('onShow')
\\},
```



### 组件中从本地目录文件判断列表文件是否已下载

```
		mounted() \\{
			// 获取FileSystemManger的全局唯一文件管理器
			this.fs = uni.getFileSystemManager();
			// 首次监听不到onShow，所以需调用一次
			this.readdir()
			const _that = this;
			// 监听主页面onShow事件
			uni.$on('onShow', function(data) \\{
				console.log(data);
				// 如果用户切换到文件管理去删除文件或目录，也能实时判断
				_that.readdir()
			\\});
		\\}
		beforeDestroy()\\{
			// 为了避免重复监听，在组件销毁前，关闭监听
			uni.$off('onShow')
		\\},
		
		// 读取本地目录内文件列表
			readdir()\\{
				const _this = this
				this.fs.readdir(\\{
					dirPath: `$\\{wx.env.USER_DATA_PATH\\}/my`,
					success(res) \\{
						console.log(res, "用户本地my目录文件列表");
						_this.downloadFiles = res.files
						_this.judgeDownload()
					\\},
					fail(res) \\{
						console.error(res);
					\\},
				\\});
			\\},
			// 判断文件是否已下载(首次data为空不影响，第一次获取到数据，查看更多时只判断新加载的数据，onShow触发时重新实时判断)
        	judgeDownload(data = this.profileList) \\{
        		data.forEach(item => \\{
					let res = this.downloadFiles.find( it => it === item.title)
					console.log(res)
					if(res)\\{
						item.isDown = true
					\\} else \\{
						// 避免本地删除后不更新状态
						item.isDown = false
					\\}
				\\});
				// 下面这种看似正常，但在else时存在问题，记录一下（有bug禁用）
				this.downloadFiles.forEach(item => \\{
					data.forEach(it => \\{
						if(item === it.title)\\{
							it.isDown = true
						\\} else \\{
							// 避免本地删除后不更新状态
							it.isDown = false
						\\}
					\\});
				\\});
			\\},
```



### JS中find方法

- find() 方法返回通过测试（函数内判断）的数组的第一个元素的值。
- 如果没有符合条件的元素返回 undefined
- find() 对于空数组，函数是不会执行的。
- find() 并没有改变数组的原始值。
- array.find(function(currentValue, index, arr),thisValue)，其中currentValue为当前项，index为当前索引，arr为当前数组

```
let test = [1, 2, 3, 4, 5];
let a = test.find(item => item > 3);
console.log(a); //4
 
let b = test.find(item => item == 0);
console.log(b); //undefined
```



### 小程序onShareTimeline()分享朋友圈

只写onShareTimeline不生效，有点坑，有两种方法：

1.onLoad或者onReady中使用wx.showShareMenu，必须两个菜单都写上朋友圈才生效

2.写个onShareAppMessage空函数里面啥也不写也行

```
	data:\\{
	\\},
	// 生命周期函数--监听页面加载
    onLoad: function(options) \\{
    	// 要先在这里设置menus的两个参数,才可以分享朋友圈
    	wx.showShareMenu(\\{
	      withShareTicket: true,
	      menus: ['shareAppMessage', 'shareTimeline']
	    \\})
    \\},
	// 用户点击右上角分享给好友
	onShareAppMessage: function() \\{
		
	\\},
	// 用户点击右上角分享朋友圈
	onShareTimeline: function () \\{
		return \\{
	      title: '',
	      query: \\{
	        key: value
	      \\},
	      imageUrl: ''
	    \\}
	\\},
\\})
```



### 无法通过自己的按钮触发“分享到朋友圈”和“收藏”

转发到朋友圈、收藏到微信收藏 只能通过点击右上角三个点操作，无法通过自己写的按钮触发，可以用类似于分享到企微的引导弹窗实现

不过可以监听右上角菜单“分享到朋友圈”、“收藏”按钮的点击行为，并可以自定义标题和图片
https://developers.weixin.qq.com/community/develop/doc/0002c42d65c4401925cef764c58c00



### 标签切换

常规写法：

```
<view class="tags-list">
            <view :class="item.checked?'active tags-item':'tags-item'" v-for="(item,index) in tagsList" :key="item.name" @click="switchTags(index)">\\\{\\\{ item.name\\\}\\\} }}
            </view>
        </view>
        
				tagsList: [
                    \\{
                        name: "全部",
                        checked: true,
                    \\},
                    \\{
                        name: "分类1",
                        checked: false,
                    \\},
                    \\{
                        name: "分类2",
                        checked: false,
                    \\},
                    \\{
                        name: "分类3",
                        checked: false,
                    \\},
            	],
            	
		// 切换分类
        switchTags(ind) \\{
            // 重新判断是否选中
            this.tagsList.forEach((item, index) => \\{
                item.checked = false;
                if (ind === index) \\{
                    item.checked = true;
                \\}
            \\});
            if (ind === 0) \\{
                console.log(ind);
            \\}
        \\},
        
 	.active \\{
        font-weight: bold;
        position: relative;
        transition: all 0.2s;
    \\}
    .active::after \\{
        content: "";
        width: 62.5\\%;
        height: 6rpx;
        border-radius: 3rpx;
        position: absolute;
        left: 18.75\\%; // 50-62.5/2
        bottom: 0;
        background: #247bff;
    \\}
```

通过selectedIndex来控制选中项更加简单：

```
<view class="tags-list">
            <view :class="checked===index?'active tags-item':'tags-item'" v-for="(item,index) in tagsList" :key="item.name" @click="switchTags(index)">\\\{\\\{ item.name\\\}\\\} }}
            </view>
        </view>
        
			// 分类列表
            tagsList: [
                \\{
                    name: "全部",
                \\},
                \\{
                    name: "分类1",
                \\},
                \\{
                    name: "分类2",
                \\},
                \\{
                    name: "分类3",
                \\},
            ],
            checked: 0, // 选中项
            
            // 切换分类
        switchTags(index) \\{
            this.checked = index; // 选中当前项
            if (index === 0) \\{
                console.log(index);
            \\}
        \\},
```



### 搜索历史保存

```
		// 点击完成按钮时触发
        confirm() \\{
            console.log(this.value, this.historicalFiles);
            // 如果缓存中有此记录，就先删除再加入
            this.historicalFiles.forEach((item, index) => \\{
                if (item === this.value) \\{
                    this.historicalFiles.splice(index, 1);
                \\}
            \\});
            this.historicalFiles.unshift(this.value);
            if (this.historicalFiles.length >= 15) \\{
                this.historicalFiles.length = 15; // 限制数组长度
            \\}
            this.$store.commit("setHistoricalFiles", this.historicalFiles);
        \\},
```



### 图片懒加载

我们在用 `uni-app` 开发微信小程序时，一般都离不开图片组件 `image`，如果图片多的时候，为了提升用户体验，都会做懒加载处理。那么，我们应该如何实现图片懒加载呢？

通过查看 [uni-app 相关文档](https://uniapp.dcloud.io/component/image.html) 和 [微信小程序相关文档](https://developers.weixin.qq.com/miniprogram/dev/component/image.html)，有如下属性：

| 属性名    | 类型    | 默认值 | 说明                                                   |
| :-------- | :------ | :----- | :----------------------------------------------------- |
| lazy-load | Boolean | false  | 图片懒加载，在即将进入一定范围（上下三屏）时才开始加载 |

因此，我们只需在 `image` 属性中增加该属性就可以了，具体如下：

```
<image lazy-load :src="item.pic" />
```

小伙伴们可能会感觉加入 `lazy-load` 属性后，好像懒加载没有生效。其实这只是个错觉，因为按文档所述，小程序会提前加载上下三屏的图片，导致无法感知懒加载的存在。其实 `image` 组件还有个如下隐藏的属性，官方文档里面没有标出来（可以在开发文档搜索“[image 组件支持设置预加载屏数](https://developers.weixin.qq.com/community/develop/doc/000a4ce83905e06823589c90651414)”查看）

默认情况下， image 组件 lazy-load 的阈值是 2 屏，也就是当图片距当前屏幕边界为 2 屏之外，图片会马上加载。不同场景可能对该阈值有不同要求，因此计划新增一个属性可以设置该阈值。文档没更新，但是可以使用了。

lazy-load-margin 值指代阈值，如lazy-load-margin="0.5"，是距离视口0.5屏时再开始加载资源

| 属性名           | 类型   | 默认值 | 说明                                               |
| :--------------- | :----- | :----- | :------------------------------------------------- |
| lazy-load-margin | Number | —      | 图片懒加载屏数阈值，在即将进入设置的屏数才开始加载 |

为了能更清楚的确认懒加载是否生效，我们通过将 `lazy-load-margin` 设置为 `0`，再看效果，代码如下：

```
<image :src="item" mode="widthFix" lazy-load="true" lazy-load-margin="0" @load="load"></image>

// 只需查看本事件触发即可知道image的加载情况
load(e) \\{
	console.log(e);
\\},
```

通过设置 `lazy-load-margin`，并结合 `微信开发者工具` 调试器中的 `Network`，我们可以很清楚的观察到懒加载的效果了。

另外，可以通过 `lazy-load-margin` 灵活设置懒加载屏数阈值。

**注意：**图片懒加载只针对 `page` 与 `scroll-view` 下的 `image` 有效。

所有的**注册页面**讲道理都在page 之下，注意这个是**注册页面**，而不是组件等。不过通常情况下组件也会在页面上被使用，里面的image自然也会在page之下



### 关键词精准匹配高亮

```
/**
 * 关键词精准匹配高亮
 * @param \\{String\\} keyword 关键词
 * @param \\{String\\} target 原数据
 * */
utils.highLight = (keyword, target) => \\{
    const reg1 = new RegExp("-", "gi");
    const keywords = keyword.replace(reg1, "\\-")
    const reg = new RegExp(keywords, "gi");
    // 对原数据中的每一项都做正则匹配，得到高亮之后的字符串
    const hLight = target.replace(
        reg,
        (val) => `<span style="color:#FEAA00">$\\{val\\}</span>`
    )
    return hLight
\\}

computed: \\{
        // 精准匹配
        highLight() \\{
            return (data) => \\{
                return utils.highLight(this.keyword, data);
            \\};
        \\},
    \\},
   
<view class="name" v-html="highLight(item.title)"></view>
```



### uniapp获取元素高度

在页面渲染完成OnReady回调，获取元素高度时，如果不加定时器，获取的元素的高度还是**没渲染完异步数据**前的高度。故需要加定时器 

```
<view class="list">
            <view :class="['item', `img$\\{index\\}`]" v-for="(item,index) in list" :key="item" @click="previewImage(index)">
                <image :src="item" mode="widthFix" lazy-load="true" lazy-load-margin="1" @load="load"></image>
            </view>
        </view>
		
		// 初始化数据
        init() \\{
        	// 获取数据后再调用
            this.getImageHeight();
        \\},
        // 获取第一个图片所在元素的高度，用于页码计算
        getImageHeight() \\{
            // 加延时才能获取到实际的高度
            setTimeout(() => \\{
                const query = uni.createSelectorQuery();
                query
                    .select(".img0")
                    .boundingClientRect((res) => \\{
                        this.imageHeight = res.height;
                        console.log(res, "第一个图片");
                    \\})
                    .exec();
            \\}, 500);
        \\},
```



### 滚动到指定元素

```
		// 点击目录将页面滚动到对应位置
        pageScrollTo(index) \\{
            this.isShowCatalogue = false;
            uni.pageScrollTo(\\{
                selector: ".img" + index,
                // 状态栏+导航栏+头部固定区域的高度为偏移量
                offsetTop: -this.headerHeight - 80,
            \\});
        \\},
```



### 监听用户滑动页面事件，判断当前页码

第一种：整页所有图片高度一样可以使用

```
	// 监听用户滑动页面事件，判断当前页码
    onPageScroll(e) \\{
        if (e.scrollTop > 0) \\{
            // 小数向上取整 + this.headerHeight + 80
            this.currentPage = Math.ceil((e.scrollTop + 80) / this.imageHeight);
        \\}
        console.log(e, this.imageHeight, this.currentPage);
    \\},
```

Math.ceil() 函数总是四舍五入并返回大于等于给定数字的最小整数。

```
console.log(Math.ceil(.95));
// expected output: 1

console.log(Math.ceil(4));
// expected output: 4

console.log(Math.ceil(7.004));
// expected output: 8

console.log(Math.ceil(-7.004));
// expected output: -7
```

第二种：尝试用循环获取元素高度，因为图片并没有都加载完，后面获取到的高度都一样，以失败告终

```
        // 加延时才能获取到实际的高度
        setTimeout(() => \\{
        	this.getImageHeight();
        \\}, 500);
            
        // 获取第一个图片所在元素的高度，用于页码计算
        async getImageHeight() \\{
            for (let i = 0; i < this.list.length; i++) \\{
                const query = uni.createSelectorQuery();
                let start, end;
                await query
                    .select(".img" + i)
                    .boundingClientRect(async (res) => \\{
                        start = i > 0 ? this.imageHeight[i - 1].end : 0;
                        end = res.height;
                        this.imageHeight.push(\\{ start, end \\});
                        console.log(res, "图片高度" + i, this.imageHeight);
                    \\})
                    .exec();
            \\}
        \\},
```

最终版：通过load触发（思路：循环获取图片每一个top(可用load)，存一个数组里，依次精确计算当前页码。）

```
        screenWidth: getApp().globalData.screenWidth, // 屏幕实际宽度
        list: [],
        imageHeight: [], // 图片高度
        scrollTop: 0,

        computed: \\{
            // 当前页码
            currentPage() \\{
                let page;
                this.imageHeight.forEach((item, index) => \\{
                    if (
                        this.scrollTop >= item.start &&
                        this.scrollTop <= item.end
                    ) \\{
                        page = index + 1;
                    \\}
                \\});
                return page;
            \\},
        \\},
    
        // 监听用户滑动页面事件，判断当前页码
        onPageScroll(e) \\{
            this.scrollTop = e.scrollTop;
            console.log(e, this.currentPage);
        \\},
    
    	// 只需查看本事件触发即可知道image的加载情况
        load(e) \\{
            console.log(e);
            // 宽高比=宽/高=屏幕宽/实际高
            const height =
                this.screenWidth / (e.detail.width / e.detail.height);
            let start, end;
            if (this.imageHeight.length === 0) \\{
                start = 0;
                end = height;
            \\} else \\{
                start = this.imageHeight[this.imageHeight.length - 1].end;
                end = start + height;
            \\}
            this.imageHeight.push(\\{ start, end \\});
            console.log("图片高度" + height, start, end, this.imageHeight);
        \\},
```



### 微信小程序单独设置右上角胶囊颜色

```
\\{
    "path": "index/index",
    "style": \\{
        "navigationBarTitleText": "首页",
        "navigationBarTextStyle": "black" // white默认透明色、black白色
    \\}
\\}
```



### 判断是在朋友圈打开

场景值1154：朋友圈内打开“单页模式” 

https://blog.csdn.net/aa2528877987/article/details/123127466



### 小程序自动更新

```
	getUpdateInfo() \\{
			// 小程序自动更新
			if (uni.canIUse('getUpdateManager')) \\{
				const updateManager = uni.getUpdateManager()
				updateManager.onCheckForUpdate(function (res) \\{
					// 请求完新版本信息的回调
					if (res.hasUpdate) \\{
						updateManager.onUpdateReady(function () \\{
							uni.showModal(\\{
								title: '更新提示',
								content: '新版本已经准备好，是否重启应用？',
								showCancel: false,
								success: function (res) \\{
									if (res.confirm) \\{
										// 新的版本已经下载好，调用 applyUpdate 应用新版本并重启
										updateManager.applyUpdate()
									\\}
								\\}
							\\})
						\\})
						updateManager.onUpdateFailed(function () \\{
							// 新的版本下载失败
							uni.showModal(\\{
								title: '已经有新版本了哟~',
								content:
									'新版本已经上线啦~，请您删除当前小程序，重新搜索打开哟~'
							\\})
						\\})
					\\}
				\\})
			\\}
		\\},
```



### uniapp request中post传递数组值的时候，数组没有正确的被传递

问题：前端传数组，后端接收到是字符串

```
uni.request(\\{
  method: 'POST',
  header: \\{
    'content-type': 'application/x-www-form-urlencoded',
  \\},
  dataType: 'json',
  url: 'http://api.cn', 
  data: \\{
    a: [1,2]
  \\}
\\})
```

'content-type'换成 application/json即可解决



### 自定义导航栏透明渐变色

pages.json设置自定义custom

```
	   \\{
			"path": "pages/index/index",
			"style": \\{
				"navigationBarTitleText": "秀企车",
				"navigationStyle": "custom"
			\\}
		\\}
```

首页

```
<!-- 自定义导航栏 -->
<view class="navbar" v-if="envType !== 3" :style="\\{ 'padding-top': systemInfo.statusBarHeight + 13 + 'px' \\}">首页自定义标题</view>

.page \\{
    width: 100vw;
    height: 100vh;
    position: relative;
\\}
.navbar \\{
    width: 100\\%;
    padding: 26rpx 0;
    position: absolute;
    top: 0;
    left: 0;
    z-index: 999;
    text-align: center;
    background-image: linear-gradient(#ffffff, transparent); // 白->透明（上到下）
\\}

// 透明->白（上到下）
background: linear-gradient(
    180deg,
    rgba(255, 255, 255, 0) 0\\%,
    #ffffff 100\\%
);
```



### 页面最小高度各平台保持一致

由于在H5中，页面区域是标题栏下方部分，设置为100vh会导致页面滚动，所以应该区分设置。

```
.page \\{
  // #ifdef H5
  height: 100\\%;
  // #endif
  // #ifndef H5
  min-height: 100vh;
  // #endif
  background: #fff;
\\}
```



### 节流函数（防止重复提交）

```
// 节流
const throttle = (fn, wait) => \\{
  let delay = wait || 500 // 不传默认500毫秒
  let timer = +new Date()  // 声明初始时间
  return function (...arg) \\{ // 获取参数
    let newTimer = +new Date()  // 获取触发事件的时间
    console.log(timer, newTimer)
    if (newTimer - timer >= delay) \\{  // 时间判断,是否满足条件
      fn.apply(this, arg)  // 调用需要执行的函数,修改this值,并且传入参数
      timer = +new Date() // 重置初始时间
    \\}
  \\}
\\}
// 类似上一种
const throttle1 = function (func, delay) \\{
  var prev = Date.now()
  return function () \\{
    var context = this;
    var args = arguments;
    var now = Date.now();
    console.log(prev, now)
    if (now - prev >= delay) \\{
      func.apply(context, args);
      prev = Date.now();
    \\}
  \\}
\\}

module.exports = \\{
  throttle
\\}
```

页面中使用

```
		import Utils from "@/utils/index";

		// 调用不成功示例
        onClick1() \\{
            Utils.throttle(this.submit1(), 1000)
        \\},
        submit1() \\{
            console.log("点击事件随机值" + Math.random())
        \\},
        // 点击提交按钮（成功示例）
        onClick: Utils.throttle(function () \\{
            console.log("点击事件随机值" + Math.random())
            this.submit()
        \\}, 2000),
        // 提交数据
        async submit() \\{
        	...
        	const res = await $http.addTripApi(this.formModel)
        	...
        \\}
```

##### 思路2. 前端：不允许二次或多次点击

1.例如使用：wx.showToast，wx.showLoading

弹出提示框，提示框显示xx秒，提示框显示期间无法再操作

通俗讲，就是弹出屏蔽层，防止用户第二次点击

2.例如使用：hidden 或者 disable 或者 wx:if

点击一次后，立即禁用或隐藏按钮

此方法可能存在的问题：在弹出提示框前已经点击了多次



### uniapp弹窗蒙层禁止滚动穿透滚动底层页面

```
// 弹窗蒙层
<view class="alert-bg"
        v-if="isShow"
        catchtouchmove='true'>
        // 弹窗内容
        ...
</view>
```



### setInterval

window.setInterval(调用函数，延时时间);

与setTimeout区别：

setTimeout是延时时间到了就去调用这个回调函数，只调用了一次 就结束了这个定时器。

setInterval是 每隔这个延迟时间 就去调用这个回调函数 会调用很多次 重复调用这个函数。

清除定时器 clearInterval()

```
	onLoad(options) \\{
        // 不是微信环境且当前页面出现在屏幕上时执行轮询
        if (this.envType !== 1 && this.isPolling) \\{
            // 3秒刷新一次
            this.timer = setInterval(() => \\{
                this.getState()
            \\}, 3000)
        \\}
    \\},
    onShow() \\{
        this.isPolling = true
    \\},
    onHide() \\{
        this.isPolling = false
    \\},
    // 监听页面卸载
    onUnload() \\{
        clearInterval(this.timer)
    \\},
```



### 小程序首页onUnload中无法请求接口

小程序首页的onUnload生命周期函数是在页面被关闭或隐藏时触发的，而请求接口需要在页面可见的状态下才能发送。因此，在onUnload中无法直接请求接口。

如果你想在小程序首页关闭或隐藏时发送接口请求，可以考虑使用其他生命周期函数或事件来实现。以下是一些可能的解决方案：

1. 在页面的onHide生命周期函数中发送接口请求：onHide会在小程序页面隐藏时触发，这样可以确保页面仍然是可见状态，可以发送请求。但需要注意，如果用户频繁在首页和其他页面之间切换，可能会频繁触发该生命周期函数并发送多个接口请求，导致性能问题。
2. 使用App全局对象的onHide生命周期函数：将请求接口的逻辑放在App全局对象的onHide生命周期函数中。这样无论哪个页面被关闭或隐藏，都能够在一处统一处理接口请求。
3. 使用其他触发条件：根据具体需求，可以考虑使用其他触发条件来发送接口请求，例如点击按钮、进入其他页面等。你可以在合适的时机，结合业务场景，选择合适的触发条件来发送接口请求。



### 原生微信小程序转uniapp每个页面修改步骤

```
this.data换成this

/images换成/static/images

bindtap和catchtap换成@click

wx.改成uni.

var改成let

that改成_this

bind改成@

wx:if改成v-if去掉大括号

wx:elif改成v-else-if去掉大括号

wx:else改成v-else

wx:for改成v-for看着改

this.setData看着改

data-改成函数传参

style=和="\\\{\\\{看着改

引用接口，改.then

解决报错
```



### vue移动端转uniapp每个页面修改步骤

- div和<p标签改成view
- span改成text
- ../../static改成/static/images
- img改成image
- alt=""改成/
- api.改成$http.
- res.data改成res
- 修改Toast、Dialog
- lang="scss"



### uniapp使用toast提示进行表单校验

```
		showToast() \\{
            this.formData.name = 'ww'
            const arr = [
                \\{ key: 'name', title: '请输入姓名' \\\}\}},
                \\{
                    key: 'index',
                    title: '请选择xxx',
                    fun: (p) => \\{
                        return p === 0
                    \\}
                \\},
                \\{ key: 'xxx', title: '请输入xxx' \\}
            ]
            let key, title, fun
            for (let i = 0; i < arr.length; i++) \\{
                key = arr[i].key
                title = arr[i].title
                fun = arr[i].fun
                console.log(key, title, fun, this.formData[key])
                if ((fun && fun(this[key])) || (!fun && !this.formData[key])) \\{
                    // 如果不满足条件或者为空就提示
                    uni.showToast(\\{
                        title,
                        icon: 'none'
                    \\})
                    return
                \\}
            \\}
        \\},
```

this[key]和this.formData[key]根据实际data数据进行修改

封装一个通用的验证方法来简化代码 

```
<template>
  <div>
    <form @submit.prevent="submitForm">
      <input v-model="name" type="text" placeholder="Name">
      
      <input v-model="email" type="email" placeholder="Email">

      <!-- Add more input fields -->

      <button type="submit">Submit</button>
    </form>
  </div>
</template>

<script>
export default \\{
  data() \\{
    return \\{
      name: '',
      email: ''
    \\}
  \\},
  methods: \\{
    submitForm() \\{
      const validationResult = this.validateForm();
      if (validationResult.isValid) \\{
        // Submit the form
      \\} else \\{
        this.$toast.error(validationResult.errorMessage);
      \\}
    \\},
    validateForm() \\{
      const requiredFields = [
        \\{ fieldName: 'name', label: 'Name' \\},
        \\{ fieldName: 'email', label: 'Email' \\},
        // Add more input fields
      ];

      for (const field of requiredFields) \\{
        if (!this[field.fieldName]) \\{
          return \\{
            isValid: false,
            errorMessage: `$\\{field.label\\} is required.`
          \\}
        \\}
      \\}

      // Add more custom validation rules

      return \\{
        isValid: true,
        errorMessage: ''
      \\};
    \\},
  \\},
\\};
</script>
```



### 控制输入框是否自动聚焦

```
<input v-model="formData.code"
                        type="number"
                        maxlength="4"
                        class="idCard-formItem-input"
                        placeholder="请输入短信验证码"
                        placeholder-class="placeholder"
                        :focus="autoFocus"
                        @blur="handleBlur"
                        @keydown.enter.native="phoneLogin" />
                    <view class="code"
                        @click="getCode"
                        v-if="!codeData.status">获取验证码</view>
                        
		getCode() \\{
            this.autoFocus = true
            this.timerInterval = setInterval(() => \\{
                if (this.codeData.count > 0) \\{
                    this.codeData.count = this.codeData.count - 1
                \\} else \\{
                    this.codeData.count = 30
                    this.codeData.status = false
                    this.dxToken = ''
                    clearInterval(this.timerInterval)
                \\}
            \\}, 1000)
        \\},
```



### 输入框聚焦页面置顶

切记:adjust-position="false"，不然ios会自动上推页面导致有问题

.focus为输入框外层容器类名

```
		<input :placeholder-class="isCheck&&!formData.title?'err':'placeholder'"
                            v-model="formData.title"
                            :adjust-position="false"
                            maxlength="32"
                            placeholder="请输入发票抬头（可检索）"
                            @focus="focusTitle"
                            @blur="blurTitle"
                            @input="inputTitle" />
                            
		// 发票抬头聚焦
        focusTitle() \\{
            this.$refs.dropRef.show()
            // 输入框聚焦置顶
            this.isFocus = true
            const offsetTop = -this.systemInfo.statusBarHeight - 44 - 45
            console.log(offsetTop)
            // 状态栏+导航栏+头部固定区域的高度为偏移量
            this.$nextTick(() => \\{
                // 防止键盘遮挡下拉框
                uni.pageScrollTo(\\{
                    selector: '.focus',
                    offsetTop
                \\})
            \\})
        \\},
```



### 使用JSON.stringify遇到特殊字符如：& 会报错

[Vue warn]: Error in onLoad hook: "SyntaxError: Unexpected end of JSON input"
SyntaxError: Unterminated string in JSON at position 90

```
			[\\{
                latitude: this.latitude,
                longitude: this.longitude,
                title: '四创科技有限公司(星网锐捷科技园·一期&二期西南)',
                // title: res.formatted_addresses.recommend,
                address: res.address,
                id: 0,
                width: 44,
                height: 60,
                iconPath: '/static/images/spot_start.png', // 图标路径
                clock_state: 0,
                time: ''
            \\}]
```

解决方案：

#### 1.通过编码解码的方式处理

```
let markers = encodeURIComponent(JSON.stringify(this.markers))
                console.log(markers)
                uni.navigateTo(\\{
                    url: `/sub_trip/trip/SetTrip?isAdd=$\\{isAdd\\}&tripList=$\\{JSON.stringify(
                        this.tripList
                    )\\}&markers=$\\{markers\\}`
                \\})
```

接收页

```
onLoad(options) \\{
        console.log(options)
        if (options.tripList) \\{
            this.tripList = JSON.parse(options.tripList)
            this.markers = JSON.parse(decodeURIComponent(options.markers))
        \\}
        console.log(this.tripList, this.markers)
\\}
```

#### 2.使用vuex，不容易出问题

因为这个字段过长，路由传参最多300多字符



### 数组深拷贝

```
				let [...markers] = this.markers // 数组深拷贝
                markers.reverse() // 数组反转
                // 处理markers数据
                markers.forEach((item, index) => \\{
                    item.id = index
                    item.width = 44
                    item.height = 60
                    item.clock_state = 0
                    item.time = ''
                    if (index === 0) \\{
                        item.iconPath = '/static/images/spot_start.png'
                    \\} else if (index === this.markers.length - 1) \\{
                        item.iconPath = '/static/images/spot_end.png'
                    \\} else \\{
                        item.iconPath = `/static/images/spot$\\{index\\}.png`
                    \\}
                \\})
                this.markers = markers
                console.log(this.markers)
```



### 微信小程序textarea组件 输入字数 ＞ 限制字数 的bug

当你需要给textarea组件添加一个统计输入字数的功能时

如果在手机上通过复制粘贴达到最大限制字数，这时候继续使用手机上的小键盘输入内容，就会出现输入字数大于限制字数的bug，而多出来的字数就是你小键盘上当前输入的内容长度。

或者超过最大限制字数，复制超字数会被统计出来

例如feedback.length可能会显示134、165，但文本框内实际有100个字符，实际问题只是显示字数不对

```
				<textarea v-model="feedback"
                    placeholder='请输入反馈内容'
                    maxlength="100"
                    @blur="handleBlur">
                </textarea>
                <text class="count">
                    <text class="black">\\\{\\\{feedback.lengt\\\}\\\}h}}</text>/100
                </text>
```

解决办法：

如果value的长度大于限制长度，则取限制长度展示

```
<text class="black">\\\{\\\{ feedback.length>100 ? 100 : feedback.length\\\}\\\} }}</text>/100
```



### 套div防止图片被挤压变形

```
<view class="search">
    <view class="icon">
    	<image :src="getSrc('search@2x.png')" />
    </view>
    <input v-model="formData.keyword"
        disabled
        @click="openPopup"
        placeholder="任务名称、任务编号"
        placeholder-class="placeholder" />
</view>
	
	.search \\{
        width: 646rpx;
        height: 60rpx;
        padding: 0 16rpx;
        margin-top: 20rpx;
        border-radius: 32rpx;
        box-sizing: border-box;
        display: flex;
        align-items: center;
        background: #fff;
        .icon \\{
            // 套div防止图片被挤压
            height: 42rpx;
            image \\{
                width: 40rpx;
                height: 42rpx;
                margin-right: 16rpx;
            \\}
        \\}
        input \\{
            width: 100\\%;
            height: 100\\%;
            font-size: 32rpx;
            letter-spacing: 2rpx;
            text-align: left;
            color: #464c5b;
        \\}
    \\}
```



### 小程序不支持table标签

```
		<view class="table">
            <!-- 表头(即第一行) -->
            <view class="tr">
                <view class="th">插件名称</view>
                <view class="th">插件提供方名称</view>
                <view class="th">使用场景</view>
                <view class="th">共享个人信息内容</view>
            </view>
            <!-- 表格第二行 -->
            <view class="tr">
                <view class="td">OCR身份证识别SDK</view>
                <view class="td">北京市商汤科技开发有限公司</view>
                <view class="td">实名认证</view>
                <view class="td">身份证照片识别</view>
            </view>
            <!-- 表格第三行 -->
            <view class="tr">
                <view class="td">顶象验证SDK</view>
                <view class="td">北京顶象技术有限公司</view>
                <view class="td">验证码防刷</view>
                <view class="td">设备信息、网络信息、IP地址、用户行为</view>
            </view>
            <!-- 表格第四行 -->
            <view class="tr">
                <view class="td">神策SDK</view>
                <view class="td">神策网络科技（北京）有限公司</view>
                <view class="td">用户行为分析</view>
                <view class="td">手机IMEI、操作信息、设备型号、手机操作系统</view>
            </view>
            <!-- 表格第五行 -->
            <view class="tr">
                <view class="td">微信SDK</view>
                <view class="td">深圳市腾讯计算机系统有限公司</view>
                <view class="td">微信登录、分享</view>
                <view class="td">微信信息（头像、昵称、地区、性别）</view>
            </view>
        </view>

.table \\{
    display: flex;
    flex-direction: column;
    border-top: 2rpx solid #dadada; /* 单元格上线框 */
    border-left: 2rpx solid #dadada; /* 单元格左线框 */
    .tr \\{
        display: flex;
        flex-direction: row;
    \\}
    .th,
    .td \\{
        width: 25\\%; /* 4个25\\%相加刚好100\\% */
        padding: 2rpx;
        display: flex;
        flex-direction: row;
        flex-wrap: wrap; /* 自动换行 */
        text-align: center; /* 文本居中 */
        justify-content: center; /* 主轴居中 */
        align-items: center; /* 交叉轴居中 */
        border-bottom: 2rpx solid #dadada; /* 单元格下线框 */
        border-right: 2rpx solid #dadada; /* 单元格右线框 */
    \\}
    .th \\{
        font-weight: bold;
    \\}
\\}
```



### uniapp中的textarea文本框设置长度限制

在uniapp 的项目中要使用编辑文本域的功能，但是文本框的长度是不做限制的，虽然在不写maxlength的情况下是可以的。但是在测试的时候你会发现文本框输入文字的时候添加140个文字以后就不能再添加文字了（没有效果了）。
我是在做uniapp的项目的时候，测试出这个问题的，后来发现，在不设置maxlength的情况下，uniapp中默认textarea中的最大字数限制为140。
即 在不写maxlength的时候，会在审查元素的时候，会自动生成 maxlength=“140”

解决办法：

在textarea标签中添加**maxlength=’’-1’’**属性

```
<textarea  maxlength="-1" />
```



### 打开另一个小程序 

```
		// 打开另一个小程序
        navigateToMiniProgram() \\{
            uni.navigateToMiniProgram(\\{
                appId: 'wx3f3b615216e7cfbe',
                path: 'pages/my/My',
                extraData: \\{
                    sign_mch_id: 'WgrpwNplS8rL',
                    phone: '18734131475'
                \\},
                envVersion: 'trial', // 要打开的小程序版本
                success(res) \\{
                    // 打开成功
                    console.log('打开成功')
                \\}
            \\})
        \\},
```

envVersion： 要打开的小程序版本，有效值： develop（开发版），trial（体验版），release（正式版）。仅在当前小程序为开发版或体验版时此参数有效。如果当前小程序是正式版，则打开的小程序必定是正式版。 

#### 跳转回上一个小程序

只有当另一个小程序跳转到当前小程序时才会能调用成功。 

```
		// 返回第三方小程序
        goBack() \\{
            // 跳转回上一个小程序，只有当另一个小程序跳转到当前小程序时才会能调用成功
            uni.navigateBackMiniProgram(\\{
                extraData: \\{
                    msg: '签约成功'
                \\},
                success(res) \\{
                    // 返回成功
                \\}
            \\})
        \\}
```



### 跳转到E证通小程序进行人脸识别

```
import $http from '@/api/http'
import \\{ mapState \\} from 'vuex'
import \\{ initEid, startEid \\} from '@/mp_ecard_sdk/main'

export default \\{
    data() \\{
        return \\{
        \\};
    \\},
    computed: \\{
        ...mapState(\\{
            userInfo: (state) => state.login.userInfo
        \\})
    \\},
    onLoad(option) \\{
        // 初始化E证通
        initEid()
    \\},
    methods: \\{
        // 跳转到E证通小程序进行人脸识别
        async faceEid() \\{
            uni.showLoading(\\{
                title: '加载中'
            \\})
            // 获取E证通EidToken
            const token = await $http.eidToken()
            uni.hideLoading()
            const param = \\{
                data: \\{
                    token
                \\},
                // 核身完成的回调
                verifyDoneCallback: async (res) => \\{
                    console.log('收到核身完成的res', res)
                    const \\{ token, verifyDone \\} = res
                    console.log('核身验证成功的token是:', token)
                    console.log('是否完成核身:', verifyDone)
                    if (verifyDone) \\{
                        uni.showLoading(\\{
                            title: '核验中'
                        \\})
                        const data = await $http.checkEidToken(res)
                        // name、phone、id_card
                        console.log(data)
                        if (data.name || this.userInfo.state === 1) \\{
                            // 认证成功 或者 已实名补录人脸的情况
                            console.log('认证成功')
                            // 刷新缓存
                            await this.getUserInfo()
                            uni.hideLoading()
                            // 如果在我的页用reLaunch，核验完回来onShow刷新一次，等待上面核验接口执行完又reLaunch，页面感觉会刷新两次
                            uni.switchTab(\\{
                                url: '/pages/my/My'
                            \\})
                        \\} else \\{
                            // 认证失败
                            uni.hideLoading()
                        \\}
                    \\}
                \\}
            \\}
            // 有token就进⼊E证通实名认证⻚
            token && startEid(param)
        \\},
    \\}
\\}
```



### 常用返回值记录

#### uniapp视频选择uni.chooseVideo返回值

```
// 微信小程序视频选择真机返回值
duration: 2
errMsg: "chooseVideo:ok"
height: 656
size: 176181
tempFilePath: "wxfile://tmp_326eae5820787184e4351b9eb86e131c9b376dc6263e5304.mp4"
width: 296

// web视频选择返回值
duration: 8.9
errMsg: "chooseVideo:ok"
height: 960
name: "iphone底部按钮问题.mp4"
size: 1201520
width: 442
tempFilePath: "blob:http://localhost:8080/e339462f-8f8a-4025-955a-e2a53760efba"
tempFile:
\\{
    lastModified: 1669347671458
    lastModifiedDate: Fri Nov 25 2022 11:41:11 GMT+0800 (中国标准时间) \\{\\}
    name: "iphone底部按钮问题.mp4"
    size: 1201520
    type: "video/mp4"
    webkitRelativePath: ""
\\}
```

#### uniapp监听实时地理位置变化事件uni.onLocationChange返回值

```
// 真机
accuracy: 35
altitude: 0
direction: 0
horizontalAccuracy: 35
indoorLocationType: -1
latitude: 39.866444498697916
longitude: 116.30702663845486
provider: "network"
speed: 0
steps: 0
type: "gcj02"
verticalAccuracy: 0
```



### 小程序如何展示md技术文档

在小程序中展示Markdown（MD）格式的技术文档，可以通过以下几种方法实现：

#### 1. 使用第三方库转换Markdown为HTML
- **选择合适的库**：可以使用如 `markdown-it` 或 `marked` 这样的JavaScript库来将Markdown文本转换成HTML格式。
- **集成到小程序**：将选中的库集成到小程序的前端代码中。由于微信小程序等平台对npm包的支持有限，可能需要手动引入库文件或通过其他方式安装。
- **调用转换函数**：在小程序中读取Markdown文档的内容，然后使用库提供的API将其转换为HTML字符串。
- **显示HTML内容**：将生成的HTML字符串通过`<rich-text>`组件在小程序页面上显示出来。

#### 2. 服务器端渲染
- **后端处理**：如果文档较多或更新频繁，可以在服务器端使用Markdown解析器（如Python的`mistune`，Node.js的`marked`等）将Markdown文件转换为HTML。
- **接口提供**：通过API接口向小程序提供转换后的HTML内容。
- **前端请求**：小程序通过HTTP请求获取这些HTML内容，并使用`<rich-text>`组件显示。

#### 3. 预先转换并存储
- **批量转换**：对于静态的Markdown文档，可以在部署前使用工具批量转换为HTML文件。
- **存储与访问**：将转换后的HTML文件存储在云存储服务中，或者直接打包进小程序资源里。
- **加载显示**：小程序加载这些HTML文件并通过`<rich-text>`组件展示给用户。

#### 注意事项
- **安全性**：无论是客户端还是服务器端渲染，都需要确保Markdown内容的安全性，避免XSS攻击。可以使用相关库的安全选项或自定义解析规则来过滤潜在危险的标签和属性。
- **样式支持**：虽然`<rich-text>`组件可以显示基本的HTML结构，但对于复杂的CSS样式支持有限。因此，在设计文档样式时需要注意兼容性。
- **性能考虑**：对于大体积的文档，应考虑分页加载或懒加载策略，以优化用户体验。

选择合适的方法取决于具体的应用场景和技术栈，例如文档的更新频率、文档大小、以及开发团队的技术偏好等因素。



### uniapp使用第三方库将Markdown文件转为页面

在UniApp中使用第三方库将Markdown文件转换为页面，可以通过以下几个步骤来实现。这里以流行的Markdown解析库`marked`为例，说明如何在UniApp项目中集成并使用它。

#### 步骤 1: 安装依赖

首先，你需要安装`marked`库。打开命令行工具，进入你的UniApp项目的根目录，执行以下命令：

```bash
npm install marked --save
```

#### 步骤 2: 创建一个Markdown组件

为了更好地组织代码，你可以创建一个新的Vue组件来专门处理Markdown文件的加载和渲染。假设我们创建一个名为`MarkdownViewer.vue`的组件。

##### MarkdownViewer.vue

```vue
<template>
  <view class="markdown-viewer">
    <rich-text :nodes="htmlContent"></rich-text>
  </view>
</template>

<script>
import marked from 'marked';

export default \\{
  data() \\{
    return \\{
      markdownContent: '',
      htmlContent: ''
    \\};
  \\},
  methods: \\{
    async fetchMarkdown() \\{
      // 这里可以根据实际情况从服务器获取Markdown内容
      const response = await uni.request(\\{
        url: '/path/to/your/markdown/file.md', // 替换为实际的Markdown文件路径
        method: 'GET'
      \\});
      
      this.markdownContent = response[1].data;
      this.convertMarkdownToHtml();
    \\},
    convertMarkdownToHtml() \\{
      this.htmlContent = marked(this.markdownContent);
    \\}
  \\},
  mounted() \\{
    this.fetchMarkdown();
  \\}
\\};
</script>

<style scoped>
.markdown-viewer \\{
  padding: 20px;
\\}
</style>
```

#### 步骤 3: 在页面中使用Markdown组件

接下来，你可以在任何页面中引入并使用这个`MarkdownViewer`组件。例如，在`pages/index/index.vue`中使用它：

##### pages/index/index.vue

```vue
<template>
  <view class="content">
    <MarkdownViewer />
  </view>
</template>

<script>
import MarkdownViewer from '@/components/MarkdownViewer.vue';

export default \\{
  components: \\{
    MarkdownViewer
  \\}
\\};
</script>

<style>
.content \\{
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
\\}
</style>
```

#### 注意事项

1. **安全性**：确保Markdown内容是安全的，避免XSS攻击。可以配置`marked`库的安全设置或自定义解析规则。
2. **样式**：`<rich-text>`组件支持的基本HTML标签样式，对于复杂的样式需求，可能需要额外的CSS支持。
3. **性能**：对于较大的Markdown文件，考虑分页加载或按需加载以提高性能。
4. **跨平台兼容性**：测试不同平台（如H5、iOS、Android）上的表现，确保一致性和兼容性。

通过上述步骤，你就可以在UniApp中成功地使用第三方库将Markdown文件转换为页面了。



### uniapp通过小程序二维码跳转到某个页面怎么获取参数options.scene

在 UniApp 中，通过小程序二维码跳转到指定页面时，获取 `scene` 参数（即二维码的场景值）需要通过小程序的启动参数或页面路径参数来解析。具体步骤如下：

---

1. 生成带参数的二维码
生成小程序二维码时，需要将参数编码到 `scene` 字段中。例如：
```javascript
// 假设你的参数是 \\{ id: 123 \\}
const scene = 'id=123'; // 将参数拼接成字符串
```

---

2. 在 App.vue 的 onLaunch 中获取场景值
当用户扫码进入小程序时，场景值 `scene` 会通过 启动参数 传递。在 `App.vue` 的 `onLaunch` 生命周期中获取：
```javascript
// App.vue
export default \\{
  onLaunch(options) \\{
    // 微信小程序中，场景值在 options.scene
    // 如果需要解析 scene 中的参数，例如 scene=id=123
    if (options.scene) \\{
      const sceneParams = decodeURIComponent(options.scene); // 解码参数
      console.log('场景值参数:', sceneParams); // 输出：id=123

      // 如果需要将参数传递给具体页面，可以存到全局或 Vuex
      uni.setStorageSync('sceneParams', sceneParams);
    \\}

    // 如果是其他平台（如支付宝），可能需要从 options.query 中获取
  \\}
\\}
```

---

3. 在目标页面解析参数
如果二维码的路径直接指向某个页面（例如 `pages/index/index`），并且 `scene` 参数是通过路径传递的（如 `?scene=id=123`），则在目标页面的 `onLoad` 中获取：
```javascript
// pages/index/index.vue
export default \\{
  onLoad(options) \\{
    // 如果 scene 参数通过 URL 传递（如 ?scene=id=123）
    if (options.scene) \\{
      const sceneParams = decodeURIComponent(options.scene);
      console.log('页面接收的场景值:', sceneParams); // 输出：id=123
    \\}
  \\}
\\}
```

---

4. 处理编码问题（关键！）
微信小程序会自动对 `scene` 参数进行 URL 编码，因此必须使用 `decodeURIComponent` 解码：
```javascript
const sceneParams = decodeURIComponent(sceneStr);
```

---

完整流程示例
1. 生成二维码：将参数 `id=123` 拼接到 `scene` 字段。
2. App.vue 中获取：
    ```javascript
    onLaunch(options) \\{
      if (options.scene) \\{
        const sceneParams = decodeURIComponent(options.scene);
        uni.setStorageSync('id', sceneParams.split('=')[1]); // 存储 id=123
      \\}
    \\}
    ```
3. 目标页面使用：
    ```javascript
    onLoad() \\{
      const id = uni.getStorageSync('id'); // 读取 id=123
    \\}
    ```

---

调试技巧
• 本地开发：在微信开发者工具中，通过点击“编译模式”下拉菜单，选择“场景值”模拟扫码场景。

• 真机测试：使用微信生成的二维码进行测试，确保参数传递正确。


通过以上步骤，你可以正确获取并解析小程序二维码中的 `scene` 参数。