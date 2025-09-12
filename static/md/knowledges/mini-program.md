---
title: 小程序
date: 2020-09-30 16:25:46
categories: 
- 前端知识
tags:
- 小程序
---

### px、em、rem、rpx 用法 与 区别

#### PX

px像素（Pixel）。相对长度单位。像素px是相对于显示器屏幕分辨率而言的。

PX特点

1. IE无法调整那些使用px作为单位的字体大小；
2. 国外的大部分网站能够调整的原因在于其使用了em或rem作为字体单位；
3. Firefox能够调整px和em，rem，但是96\\%以上的中国网民使用IE浏览器(或内核)。

#### EM

em是相对长度单位。相对于当前对象内文本的字体尺寸。如当前对行内文本的字体尺寸未被人为设置，则相对于浏览器的默认字体尺寸。

EM特点

1. em的值并不是固定的；
2. em会继承父级元素的字体大小。

注意：任意浏览器的默认字体高都是16px。所有未经调整的浏览器都符合: 1em=16px。那么12px=0.75em,10px=0.625em。为了简化font-size的换算，需要在css中的body选择器中声明Font-size=62.5\\%，这就使em值变为 16px*62.5\\%=10px, 这样12px=1.2em, 10px=1em, 也就是说只需要将你的原来的px数值除以10，然后换上em作为单位就行了。

所以我们在写CSS的时候，需要注意两点：

1. body选择器中声明Font-size=62.5\\%；
2. 将你的原来的px数值除以10，然后换上em作为单位；
3. 重新计算那些被放大的字体的em数值。避免字体大小的重复声明。
也就是避免1.2 * 1.2= 1.44的现象。比如说你在#content中声明了字体大小为1.2em，那么在声明p的字体大小时就只能是1em，而不是1.2em, 因为此em非彼em，它因继承#content的字体高而变为了1em=12px。

#### REM

rem是CSS3新增的一个相对单位（root em，根em），这个单位引起了广泛关注。这个单位与em有什么区别呢？区别在于使用rem为元素设定字体大小时，仍然是相对大小，但相对的只是HTML根元素。这个单位可谓集相对大小和绝对大小的优点于一身，通过它既可以做到只修改根元素就成比例地调整所有字体大小，又可以避免字体大小逐层复合的连锁反应。目前，除了IE8及更早版本外，所有浏览器均已支持rem。对于不支持它的浏览器，应对方法也很简单，就是多写一个绝对单位的声明。这些浏览器会忽略用rem设定的字体大小。下面就是一个例子：

p \\{font-size:14px; font-size:.875rem;\\}
注意： 选择使用什么字体单位主要由你的项目来决定，如果你的用户群都使用最新版的浏览器，那推荐使用rem，如果要考虑兼容性，那就使用px,或者两者同时使用。

#### px 与 rem 的选择？

对于只需要适配少部分手机设备，且分辨率对页面影响不大的，使用px即可 。

对于需要适配各种移动设备，使用rem，例如只需要适配iPhone和iPad等分辨率差别比较挺大的设备。

#### rpx

rpx 是微信小程序解决自适应屏幕尺寸的尺寸单位。微信小程序规定屏幕的宽度为750rpx。

无论是在iPhone6上面还是其他机型上面都是750rpx的屏幕宽度，拿iPhone6来讲，屏幕宽度为375px，把它分为750rpx后， 1rpx = 0.5px。

微信小程序同时也支持rem尺寸单位， rem 规定屏幕的宽度为20rem, 所以 1rem = (750/20)rpx = 37.5 rpx



### 微信小程序字体最小支持

和chrome一样最小支持12px。

想要更小，可以使用css3 缩放， transform:scale(0.5);



### 小程序登录

小程序可以通过微信官方提供的登录能力方便地获取微信提供的用户身份标识，快速建立小程序内的用户体系。

#### 登录流程时序

![img](https://res.wx.qq.com/wxdoc/dist/assets/img/api-login.2fcc9f35.jpg)

#### 说明

1. 调用 [wx.login()](https://developers.weixin.qq.com/miniprogram/dev/api/open-api/login/wx.login.html) 获取 **临时登录凭证code** ，并回传到开发者服务器。
2. 调用 [auth.code2Session](https://developers.weixin.qq.com/miniprogram/dev/api-backend/open-api/login/auth.code2Session.html) 接口，换取 **用户唯一标识 OpenID** 、 用户在微信开放平台帐号下的**唯一标识UnionID**（若当前小程序已绑定到微信开放平台帐号） 和 **会话密钥 session_key**。

之后开发者服务器可以根据用户标识来生成自定义登录态，用于后续业务逻辑中前后端交互时识别用户身份。

#### 注意事项

1. 会话密钥 `session_key` 是对用户数据进行 [加密签名](https://developers.weixin.qq.com/miniprogram/dev/framework/open-ability/signature.html) 的密钥。为了应用自身的数据安全，开发者服务器**不应该把会话密钥下发到小程序，也不应该对外提供这个密钥**。
2. 临时登录凭证 code 只能使用一次



### 微信小程序分享转发功能

组件分享的话，会调用父页面的onShareAppMessage

父组件（页面）

```
// 转发给朋友
		onShareAppMessage(res) \\{
			console.log("成功", res)
			return \\{
				title: '下载盘爱坊APP或进入小程序完成注册，立享88元购物劵',
				path: `/pages/index/index?invitationCode=$\\{this.invitationCode\\}`, // 配置分享的页面路径
				imageUrl: 'https://test.panaifang.com/pubapi/images/upload/wechat/resources/invitation.png'
				// 微信不再支持分享回调参数 success 、fail
				// success: function(res) \\{
				// 	console.log("成功", res)
				// 	this.isShowDialog4 = false
				// \\}
			\\}
		\\},
		// 朋友圈
		onShareTimeline(res) \\{
			return \\{
				title: "下载盘爱坊APP或进入小程序完成注册，立享88元购物劵",
				query: `invitationCode=$\\{this.invitationCode\\}`, // 需要携带的参数, 无法自定义路径，只能是当前的分享页
				imageUrl: 'https://test.panaifang.com/pubapi/images/upload/wechat/resources/invitation.png'
			\\}
		\\},
```

子组件（弹窗）

```
<button open-type="share">
	<image :src="getImgSrc('/resources/inviteNow.png')" mode="widthFix"></image>
</button>
```

https://developers.weixin.qq.com/community/develop/doc/0000447a5b431807af57249a551408



### wx.navigateBack（）返回上一页面如何传参数？

wx.navigateBack（）不能像其他导航一样通过url传参，因此只能使用其他方法：

先说两个可以实现但弊端很大的方法：

1、将数据存到app.globalData中，然后返回上一页面从全局数据中获取

​    弊端：数据为全局数据，必须谨慎维护，否则全局某处做出修改，牵一发而动全身

2、将数据存到本地缓存中（[localStorage](https://so.csdn.net/so/search?q=localStorage&spm=1001.2101.3001.7020)），然后从缓存中获取 

​    弊端：本地缓存空间大小存在限制，若空间不足会自动清除其中最久未使用的数据，同样可能会造成意想不到的影响

so？还有一个比较完美的方法，就是：

使用getCurrentPages()函数获取页面栈的实例，以数组形式按栈的顺序给出，第一个元素为首页，最后一个元素为当前页面。

官方文档参考：https://developers.weixin.qq.com/miniprogram/dev/framework/app-service/route.html?search-key=getCurrentPages

```
var pages = getCurrentPages();
var currPage = pages[pages.length - 1];   //当前页面
var prevPage = pages[pages.length - 2];  //上一个页面
 
//直接调用上一个页面对象的setData()方法，把数据存到上一个页面中去
prevPage.setData(\\{
  data：data
\\});
wx.navigateBack(\\{
	delta: 1
\\})
```



### 小程序打开文件

1.微信自带文件预览
支持doc格式、docx格式、xls格式、xlsx格式、ppt格式、pptx格式、pdf格式
从文件预览进去的分享、收藏、下载不能监测到，不过查看、分享、收藏、下载的是文件原来的格式，体验好
从文件列表分享的支持以小程序卡片形式分享，可自定义分享卡片的图片和标题，分享可以记录访客的查看次数，但收藏、下载次数无法统计

2.目录功能官方暂不支持
如确需要做，PPT或PDF只能由后端将其按页分割成图片进行显示（目录：缩略图，内容：高清图），这样才能实现点击对应目录跳转对应页码
优点：预览页面可以自定义，保证了UI的还原，产品功能的全部实现（下载的时候可以给他下载源文件格式）
缺点：复杂度较高，实现较难，图片加载较慢，兼容性、清晰度、排版等可能有问题，且预览 下载 收藏时不是文件原PPT或PDF格式，缩放滑动等体验较差

3.PDF或PPT转成长图
不支持目录功能，其他功能基本可以实现，页面可以自定义

4.其他
iframe：小程序内嵌其他页面会自动铺满整个页面，且每个页面只能有一个，它会覆盖其他组件。也就是说，没有办法实现小程序界面组件和页面混排的情况
pdf.js：通过web-view打开，问题同上，不如官方自带的
ppt，pdf转html格式：不太可行



### getPhoneNumber:fail no permission

因为小程序没有做微信认证。

打开小程序后台 -> 设置 -> 基本设置

认证时需要支付300元认证费用。大概需要1-3工作日。

也可以复用公众号资质快速认证，这里如果关联的公众号是认证的，那么可以直接复用。



### 企业微信小程序清除本地缓存

企业微信发布体验版的方式和小程序不一样，官网也有写。在开发者工具点击预览，然后企业微信扫一扫打开小程序后，点击右上角三个点，菜单中有一个配置体验版，然后点击更新版本，体验版就是目前发布的最新版了。

在清除缓存方面，也不需要什么重新登陆。体验版或者开发版的情况下，同样进入小程序点击右上角三个点，菜单往后面滑动，点击打开调试，然后自动重启多出一个vconsole，点开vconsole之后里面有一个wechat的菜单栏，然后点击，里面有个wx.clearStorage()，点击之后退出去重新进就好了。不过这个办法在企业微信小程序里面只针对于安卓。

如果是苹果手机啊，使用上面的方法，打开小程序点击三个点之后会发现没有”打开调试“的菜单，因此，最好的办法还是使用小程序提供的最好，那就是在app.js的onLaunch生命周期里面加一句代码就好了：

```
wx.setEnableDebug(\\{
   enableDebug: true,
   success:()=>\\{
    console.log(123123)
   \\}
\\})
```

这句代码加进去 无论是普通的小程序 还是企业微信打开的小程序，都能有vconsole，都能清除缓存。



### 小程序获取位置

```
 // 定义组件生命周期函数
  lifetimes: \\{
    attached: function () \\{
      // 在组件实例进入页面节点树时执行
      console.log("组件attached")
      // 同步获取位置改变
      this.getWxLocation()
      // 测试-实时可能请求转文本接口过多
      // this.startLocationUpdate()
      // 普通获取当前位置坐标
      // this.getLocation()
    \\},
    ready() \\{\\},
    detached: function () \\{
      // 在组件实例被从页面节点树移除时执行
      // 移除实时地理位置变化事件的监听函数
      wx.offLocationChange(this.locationChange)
    \\},
  \\},
  
  
  	// 同步获取位置改变
    getWxLocation() \\{
      return new Promise((resolve, reject) => \\{
        const _locationChangeFn = (res) => \\{
          console.log('同步获取位置改变', res)
          this.setData(\\{
            location: res
          \\})
          resolve(res);
          // 坐标转文字（放在resolve后面不影响同步获取速度）
          this.getLocationText()
          wx.offLocationChange(_locationChangeFn)
        \\}
        wx.startLocationUpdate(\\{
          success: (res) => \\{
            wx.onLocationChange(_locationChangeFn)
          \\},
          fail: (err) => \\{
            console.log('获取当前位置失败', err)
            reject()
          \\}
        \\})
      \\})
    \\},
  
    // 获取实时位置坐标信息
    startLocationUpdate() \\{
      const _this = this
      wx.startLocationUpdate(\\{
        success: (res) => \\{
          wx.onLocationChange(_this.locationChange)
        \\},
        fail: (err) => \\{
          console.log(err)
        \\}
      \\})
    \\},
    locationChange(res) \\{
      console.log('实时位置改变', res)
      // this.setData(\\{
      //   location: res
      // \\})
      // 坐标转文字
      // this.getLocationText()
    \\},
    
    // 普通获取当前位置坐标（备用）
    getLocation() \\{
      let that = this
      wx.getLocation(\\{
        type: 'gcj02',
        isHighAccuracy: true,
        success(res) \\{
          console.log('getLocation', res)
          that.setData(\\{
            location: res
          \\})
          // 坐标转文字
          that.getLocationText()
        \\},
        fail(err) \\{
          console.log(err)
        \\}
      \\})
    \\},
```

切记在app.json中设置