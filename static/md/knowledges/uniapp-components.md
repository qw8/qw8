---
title: uniapp组件
date: 2023-04-30 08:03:10
categories: 
- 前端知识
tags:
- uniapp
- 小程序
---

### 弹窗确认提示框组件Alert.vue

```
<template>
    <view class="alert-bg"
        v-if="isShow"
        catchtouchmove='true'>
        <view class="alert">
            <text class="title">\\\{\\\{titl\\\}\\\}e}}</text>
            <text class="content"
                v-if="content">\\\{\\\{conten\\\}\\\}t}}</text>
            <slot></slot>
            <view class="button-bg">
                <view class="left button"
                    v-if="showCancel"
                    @click="cancel">\\\{\\\{cancelTex\\\}\\\}t}}</view>
                <view :class="showCancel ? 'right button':'full button'"
                    :style="\\{color:confirmColor\\}"
                    @click="confirm">\\\{\\\{confirmTex\\\}\\\}t}}</view>
            </view>
        </view>
    </view>
</template>

<script>
export default \\{
    props: \\{\\},
    data() \\{
        return \\{
            isShow: false, // 是否显示
            title: '', // 标题
            content: '', // 内容
            cancelText: '取消', // 取消按钮文字
            confirmText: '确定', // 确定按钮文字
            confirmColor: '#247bff', // 确定按钮的文字颜色
            url: '', // 确定后需跳转页面路径
            showCancel: true ,// 是否显示取消按钮
			isNavigate: true // 是否navigateTo
        \\}
    \\},
    computed: \\{\\},
    created() \\{\\},
    methods: \\{
        // 显示弹框
        show(obj) \\{
            console.log(obj)
            this.isShow = true
            this.title = obj.title || ''
            this.content = obj.content || ''
            this.cancelText = obj.cancelText || '取消'
            this.confirmText = obj.confirmText || '确定'
            this.confirmColor = obj.confirmColor || '#247bff'
            this.url = obj.url || ''
            this.showCancel = obj.showCancel === false ? false : true
			this.isNavigate = obj.isNavigate === false ? false : true
        \\},
        // 取消：关闭弹框
        cancel() \\{
            this.isShow = false
        \\},
        // 确认：跳转对应页面
        confirm() \\{
            // 有url就跳转
            if (this.url) \\{
				if(this.isNavigate)\\{
					uni.navigateTo(\\{
					    url: this.url
					\\})
				\\} else \\{
					uni.switchTab(\\{
					    url: this.url
					\\})
				\\}
            \\} else if (this.showCancel) \\{
                // 如果有取消按钮，触发父组件回调事件
                this.$emit('confirm')
            \\}
            this.isShow = false
        \\}
    \\}
\\}
</script>

<style scoped lang="scss">
.alert-bg \\{
    position: fixed;
    top: 0;
    left: 0;
    width: 100\\%;
    height: 100\\%;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 999;
    .alert \\{
        width: calc(100\\% - 128rpx);
        display: flex;
        flex-direction: column;
        align-items: center;
        border-radius: 16rpx;
        z-index: 1000;
        background-color: #ffffff;
        .title \\{
            font-size: 32rpx;
            font-weight: 500;
            color: #33373d;
            line-height: 40rpx;
            margin: 48rpx 0 40rpx 0;
        \\}
        .content \\{
            font-size: 28rpx;
            color: #5e6166;
            line-height: 36rpx;
            margin: 0 48rpx;
            text-align: center;
        \\}
        .button-bg \\{
            width: 100\\%;
            margin-top: 48rpx;
            font-size: 32rpx;
            border-top: 1px solid #f0f2f5;
            display: flex;
            .button \\{
                text-align: center;
                padding: 24rpx 0;
            \\}
            .left \\{
                width: 50\\%;
                color: #33373d;
                border-right: 1px solid #f0f2f5;
            \\}
            .full \\{
                width: 100\\%;
            \\}
            .right \\{
                width: 50\\%;
            \\}
        \\}
    \\}
\\}
</style>
```

使用方式：

```
<!-- 自定义弹窗 -->
<Alert ref="alertRef"></Alert>

this.$refs.alertRef.show(\\{
    title: '请添加收款账户',
    content:
    '您还未添加收款账户信息，为了方便企业进行费用结算，请尽快前往添加收款账户信息',
    cancelText: '稍后',
    confirmText: '去添加',
    url: '/sub_my/account/AddAccount'
\\})
```



### 打卡弹窗组件ClockPopup.vue

```
<template>
    <view class="popup"
        v-if="isShow">
        <view class="content">
            <image class="bg-top"
                :src="imgUrl+'clock_top@2x.png'" />
            <image class="bg-bottom"
                :src="imgUrl+'clock_bottom@2x.png'" />
            <view class="inner">
                <view class="rotate"
                    v-if="state===0">
                    <image class="ring"
                        :src="imgUrl+'clock2@2x.png'" />
                    <image class="circle"
                        :src="imgUrl+'clock1@2x.png'" />
                    <text>打卡中...</text>
                </view>
                <image class="success"
                    :src="imgUrl+'clock5@2x.png'"
                    v-if="state===1" />
                <view class="success-text"
                    v-if="state===1">打卡成功</view>
                <view class="address"
                    v-if="state===0||state===1">
                    <image :src="imgUrl+'clock3@2x.png'" />
                    <view class="text">\\\{\\\{state===0?'当前':'打卡'\\\}\\\}位置：\\\{\\\{addres\\\}\\\}s}}</view>
                </view>
                <image class="fail"
                    src="/static/images/clock6.png"
                    mode="widthFix"
                    v-if="state===2" />
                <view class="fail-text"
                    v-if="state===2">打卡失败</view>
                <view class="address"
                    v-if="state===2">
                    <image src="/static/images/clock7.png" />
                    <view class="text">失败原因：\\\{\\\{ti\\\}\\\}p}}</view>
                </view>
                <view class="again"
                    v-if="state===2"
                    @click="setRecord">
                    <image src="/static/images/clock8.png" />
                    <text>重新打卡</text>
                </view>
            </view>
            <image class="close"
                src="/static/images/clock4.png"
                @click="close" />
        </view>
    </view>
</template>

<script>
import Config from '@/config'
import $http from '@/api/http'
import Utils from '@/utils/index'
import QQMapWX from '@/utils/qqmap-wx-jssdk.min.js'
import \\{ mapState \\} from 'vuex'

export default \\{
    props: \\{
        tripId: \\{
            type: Number,
            value: 0
        \\},
        markers: \\{
            type: Array,
            value: []
        \\},
        clock_radius: \\{
            type: Number,
            value: 1000
        \\}
    \\},
    data() \\{
        return \\{
            imgUrl: Config.imgUrl, // 图片地址
            isShow: false, // 是否显示弹窗
            tMap: null, // 腾讯地图实例
            location: \\{\\}, // 位置信息
            title: '', // 当前位置标题
            address: '', // 当前位置详情
            state: 0, // 0打卡中，1打卡成功，2打卡失败
            tip: '网络异常' // 失败原因
        \\}
    \\},
    computed: \\{
        ...mapState(\\{
            envType: (state) => state.login.envType,
            map: (state) => state.login.map
        \\})
    \\},
    created() \\{
        // 微信/企微
        if (this.envType === 1 || this.envType === 2) \\{
            // 同步获取位置改变
            this.getWxLocation()
        \\}
        // 钉钉
        if (this.envType === 3) \\{
            // 普通获取当前位置坐标
            this.getLocation()
        \\}
        // 实例化腾讯地图API核心类
        this.tMap = new QQMapWX(\\{
            key: this.map.key // 开发者密钥
        \\})
    \\},
    methods: \\{
        // 打开弹框
        open() \\{
            // 微信/企微
            if (this.envType === 1 || this.envType === 2) \\{
                // 同步获取位置改变
                this.getWxLocation()
            \\}
            // 钉钉
            if (this.envType === 3) \\{
                // 普通获取当前位置坐标
                this.getLocation()
            \\}
            this.isShow = true
            console.time('耗时')
            this.setRecord()
            console.timeEnd('耗时')
        \\},
        // 关闭弹框
        close() \\{
            this.isShow = false
        \\},

        // 同步获取位置改变
        getWxLocation() \\{
            return new Promise((resolve, reject) => \\{
                const _locationChangeFn = (res) => \\{
                    console.log('同步获取位置改变', res)
                    this.location = res
                    resolve(res)
                    // 坐标转文字（放在resolve后面不影响同步获取速度）
                    this.getLocationText()
                    uni.offLocationChange(_locationChangeFn)
                \\}
                uni.startLocationUpdate(\\{
                    success: (res) => \\{
                        uni.onLocationChange(_locationChangeFn)
                    \\},
                    fail: (err) => \\{
                        console.log('获取当前位置失败', err)
                        reject()
                    \\}
                \\})
            \\})
        \\},
        // 普通获取当前位置坐标
        getLocation() \\{
            let _this = this
            uni.getLocation(\\{
                // type: 'gcj02',
                isHighAccuracy: true,
                success(res) \\{
                    console.log('getLocation', res)
                    _this.location = res
                    // 坐标转文字
                    _this.getLocationText()
                \\},
                fail(err) \\{
                    console.log(err)
                \\}
            \\})
        \\},
        // 普通获取当前位置坐标（同步获取）
        getLocationSync() \\{
            return new Promise((resolve, reject) => \\{
                uni.getLocation(\\{
                    type: 'gcj02',
                    isHighAccuracy: true,
                    success: resolve,
                    fail: reject
                \\})
            \\})
        \\},
        // 根据当前经纬度获取所在位置的文字描述
        async getLocationText() \\{
            const \\{ result \\} = await this.getCurrentLocation(this.location)
            console.log('当前位置文字', result)
            this.address = result.address
        \\},
        getCurrentLocation(location) \\{
            return new Promise((resolve, reject) => \\{
                this.tMap.reverseGeocoder(\\{
                    location, //位置坐标，对象格式,不填默认当前位置(不填真机会报错)
                    success: resolve,
                    fail: reject
                \\})
            \\})
        \\},

        // 打卡
        setRecord() \\{
            // 显示打卡中
            this.state = 0
            setTimeout(() => \\{
                this.getNetworkType()
            \\}, 1500)
        \\},
        // 获取网络类型
        getNetworkType() \\{
            if (this.envType === 4) \\{
                // h5判断有无网络
                console.log(navigator.onLine)
                if (navigator.onLine) \\{
                    this.judge()
                \\} else \\{
                    this.tip = '网络异常'
                    this.state = 2
                \\}
            \\} else \\{
                let _this = this
                uni.getNetworkType(\\{
                    success(res) \\{
                        console.log('网络', res)
                        if (res.networkType === 'none') \\{
                            _this.tip = '网络异常'
                            _this.state = 2
                        \\} else \\{
                            _this.getSetting()
                        \\}
                    \\}
                \\})
            \\}
        \\},
        // 获取用户的当前设置
        getSetting() \\{
            let isAuthed = false // 是否授权了位置信息
            if (this.envType === 1) \\{
                // 微信
                uni.getSetting(\\{
                    success: (res) => \\{
                        console.log('权限', res)
                        if (res.authSetting['scope.userLocation']) \\{
                            isAuthed = true
                        \\}
                    \\}
                \\})
            \\}
            if (isAuthed || this.location.latitude) \\{
                // 微信授权了 或者 企微/钉钉/web有坐标
                this.judge()
            \\} else \\{
                this.tip = '获取定位失败'
                this.state = 2
                console.log(this.tip)
            \\}
        \\},

        // 打卡判断
        async judge() \\{
            // 如果还没有获取到位置就重新获取
            if (!this.location.latitude) \\{
                if (this.envType === 1 || this.envType === 2) \\{
                    this.location = await this.getWxLocation()
                \\} else if (this.envType === 3) \\{
                    this.location = await this.getLocationSync()
                \\}
                console.log('还没有获取到位置，同步获取', this.location)
            \\}
            let markers = this.markers
            let num = 0
            let maxTime = '',
                time = new Date(),
                minute
            console.log(markers, this.location)
            for (let i = 0; i < markers.length; i++) \\{
                if (markers[i].time === null) \\{
                    // 防止time提交时为null字符串，不能写到下面的循环，会导致提交时后面的还是null
                    markers[i].time = ''
                \\} else \\{
                    // 如果打过卡
                    if (maxTime) \\{
                        // 第二个及以后
                        if (markers[i].time > maxTime) \\{
                            // 如果比最大的大，就赋值为最大值
                            maxTime = markers[i].time
                        \\}
                    \\} else \\{
                        // 第一个
                        maxTime = markers[i].time
                    \\}
                \\}
            \\}
            console.log('最大时间', maxTime)
            if (maxTime) \\{
                // 如果以前打过卡
                maxTime = Utils.getDateFromTimeString(maxTime)
                minute = (time - maxTime) / (1000 * 60)
            \\} else \\{
                // 没打过卡，让满足打卡条件
                minute = 4
            \\}
            console.log('距离最大时间的分钟数', minute, maxTime, time)

            // 循环获取两点距离进行判断
            for (let i = 0; i < markers.length; i++) \\{
                const \\{ result \\} = await this.calculateDistance(
                    this.location,
                    markers[i]
                )
                const distance = result.elements[0].distance
                console.log(
                    '第' + i + '个距离',
                    distance,
                    '半径',
                    this.clock_radius
                )
                if (distance < this.clock_radius) \\{
                    // 如果有在打卡半径（默认1000）范围内的
                    if (markers[i].clock_state === '2') \\{
                        // 如果已经打卡，弹窗直接显示成功，不调用接口，防止第一次打卡时间被覆盖
                        this.state = 1
                        console.log('已经打卡，弹窗直接显示成功')
                    \\} else if (minute > 3) \\{
                        // 如果超过三分钟
                        markers[i].time = Utils.formatDate(new Date()) // 当前时间
                        markers[i].clock_state = '2' // 打卡成功状态，为了和以前小程序数据类型相同
                        this.clockTrip(markers)
                        // 有一个成功就改变条件，后续的点不满足条件就不打卡了
                        minute = 0
                    \\}
                \\} else \\{
                    num++
                \\}
                // 每次点击打卡时依次记录各个点的情况
                await $http.recordClockApi(\\{
                    id: this.tripId,
                    is_ok: distance < this.clock_radius,
                    radius: distance,
                    latitude: this.location.latitude,
                    longitude: this.location.longitude,
                    markers
                \\})
            \\}
            if (num === markers.length) \\{
                this.tip = '您未在所有地点的半径1000米范围内'
                this.state = 2
            \\}
        \\},
        // 计算一段路的距离
        calculateDistance(from, to) \\{
            // console.log(from, to, 111)
            return new Promise((resolve, reject) => \\{
                this.tMap.calculateDistance(\\{
                    mode: 'straight', // 可选值：'driving'（驾车）、'walking'（步行）、'straight'（直线），不填默认：'walking'
                    // 经纬度并设置from和to参数
                    from: from, // 若起点有数据则采用起点坐标，若为空默认当前地址
                    to: [to], // 终点坐标格式为数组或字符串
                    success: resolve,
                    fail: reject
                \\})
            \\})
        \\},
        // 打卡接口
        async clockTrip(markers) \\{
            console.log(markers)
            await $http.clockTripApi(\\{
                id: this.tripId,
                markers
            \\})
            this.state = 1
            // 刷新父页面数据
            this.$emit('refresh')
        \\}
    \\}
\\}
</script>

<style scoped lang="scss">
.popup \\{
    width: 100\\%;
    height: 100\\%;
    display: flex;
    justify-content: center;
    align-items: center;
    position: fixed;
    top: 0;
    left: 0;
    z-index: 999;
    background: rgba(0, 0, 0, 0.5);
\\}

.content \\{
    width: 622rpx;
    height: 812rpx;
    margin-bottom: 164rpx;
    border-radius: 24rpx;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    position: relative;
    background: #fff;
\\}

.bg-top \\{
    width: 100\\%;
    height: 580rpx;
    position: absolute;
    top: 0;
\\}

.bg-bottom \\{
    width: 100\\%;
    height: 196rpx;
    position: absolute;
    bottom: 0;
\\}

.inner \\{
    width: 100\\%;
    height: 100\\%;
    position: absolute;
    top: 0;
    left: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
\\}

.rotate \\{
    width: 440rpx;
    height: 440rpx;
    margin-bottom: 56rpx;
    position: relative;
\\}

.ring \\{
    width: 440rpx;
    height: 440rpx;
    /*旋转*/
    animation: circleRoate 5s infinite;
    animation-timing-function: linear;
\\}

.circle \\{
    width: 392rpx;
    height: 392rpx;
    position: absolute;
    top: 38rpx;
    left: 24rpx;
\\}

@keyframes circleRoate \\{
    from \\{
        transform: rotate(0deg);
    \\}

    to \\{
        transform: rotate(360deg);
    \\}
\\}

.rotate text \\{
    line-height: 64rpx;
    position: absolute;
    top: 200rpx;
    left: 124rpx;
    font-size: 48rpx;
    font-weight: 500;
    color: #fff;
\\}

.success \\{
    width: 516rpx;
    height: 360rpx;
\\}

.success-text \\{
    line-height: 100rpx;
    margin: 32rpx 0;
    font-size: 72rpx;
    font-weight: 600;
    color: #247bff;
\\}

.address \\{
    padding: 0 40rpx;
    display: flex;
\\}

.address image \\{
    width: 32rpx;
    height: 32rpx;
    margin-top: 4rpx;
\\}

.address .text \\{
    line-height: 40rpx;
    margin-left: 8rpx;
    font-size: 28rpx;
    flex: 1;
    text-align: center;
    color: #868a8f;
\\}

.fail \\{
    width: 380rpx;
\\}

.fail-text \\{
    line-height: 100rpx;
    margin: 32rpx 0;
    font-size: 72rpx;
    font-weight: 600;
    color: #e34950;
\\}

.again \\{
    margin-top: 32rpx;
    position: relative;
\\}

.again image \\{
    width: 264rpx;
    height: 264rpx;
\\}

.again text \\{
    line-height: 40rpx;
    font-size: 32rpx;
    word-wrap: nowrap;
    position: absolute;
    top: 96rpx;
    left: 68rpx;
    color: #fff;
\\}

.close \\{
    width: 96rpx;
    height: 96rpx;
    position: absolute;
    bottom: -144rpx;
    left: 264rpx;
\\}
</style>
```

使用方式：

```
<!-- 打卡弹窗 -->
<clock-popup ref="clockRef"
    :tripId="detail.id"
    :markers="detail.markers"
    :clock_radius="clock.clock_radius"
    @refresh="getDetail"></clock-popup>
    
// 打卡
onClick() \\{
	this.$refs.clockRef.open()
\\},
```



### 时间选择组件DateTime.vue

```
<template>
    <picker mode="multiSelector" :range="rangeList" :value="rangeValue" @change="selectChangeFn" @columnchange="selectColumnChangeFn">
        <slot></slot>
    </picker>
</template>

<script>
export default \\{
    props: \\{
        mode: \\{
            // 选择器类型
            type: String,
            required: true,
        \\},
        value: \\{
            // 回显的时间
            type: String,
            default: "",
        \\},
    \\},
    data() \\{
        return \\{
            rangeList: [],
            rangeValue: [],
            dateDetails: ["年", "月", "时", "分", "秒"],
        \\};
    \\},
    computed: \\{\\},
    created() \\{
        // 初始化时间选择器，延时是因为编辑需要获取后端数据
        setTimeout(() => \\{
            this._initDateTimePickerFn();
        \\}, 500);
    \\},
    methods: \\{
        //初始化时间选择器
        _initDateTimePickerFn() \\{
            try \\{
                if (this.mode != "dateminute" && this.mode != "datetime") \\{
                    uni.showToast(\\{
                        title: "请输入合法的时间选择器类型！",
                        icon: "none",
                        duration: 2000,
                    \\});
                \\}
                //获取到当前时间
                let showTimeValue = this._validateShowTime(
                    this.value,
                    this.mode
                );
                // 获取年份范围
                const currentYear = showTimeValue.substring(
                    0,
                    showTimeValue.indexOf("-")
                );
                const currentMouth = showTimeValue.split(" ")[0].split("-")[1];
                const yearList = this._gotDateTimeList(\\{
                    _start: Number(currentYear) - 1,
                    _end: Number(currentYear) + 1,
                    _type: 0,
                \\});
                // 获取月份
                const monthList = this._gotDateTimeList(\\{
                    _start: 1,
                    _end: 12,
                    _type: 1,
                \\});
                //获取天数
                const dayList = this._gotDayList(currentYear, currentMouth);
                // 获取小时
                const hourList = this._gotDateTimeList(\\{
                    _start: 0,
                    _end: 23,
                    _type: 2,
                \\});
                // 获取分钟
                const munithList = this._gotDateTimeList(\\{
                    _start: 0,
                    _end: 59,
                    _type: 3,
                \\});
                // 获取秒
                const secondList = this._gotDateTimeList(\\{
                    _start: 0,
                    _end: 59,
                    _type: 4,
                \\});
                let rangeList = new Array();
                rangeList.push(yearList);
                rangeList.push(monthList);
                rangeList.push(dayList);
                rangeList.push(hourList);
                rangeList.push(munithList);
                this.mode === "datetime" && rangeList.push(secondList);
                this.rangeList = rangeList;
                this._echoDateTime(showTimeValue); // 初始化时间显示
            \\} catch (err) \\{
                console.log(err);
            \\}
        \\},
        //验证显示的时间是否合法
        //@param \\{Number\\} _value 要验证的时间
        //@param \\{Number\\} _mode  选择器类型
        _validateShowTime(_value, _mode) \\{
            let currentTime = this.formatTime(new Date()).replace(/\//g, "-");
            let showTimeValue = _value.trim() || currentTime;
            const secondReg = /^\d\\{4\\}-\d\\{2\\}-\d\\{2\\}\s\d\\{2\\}:\d\\{2\\}:\d\\{2\\}$/;
            const munithReg = /^\d\\{4\\}-\d\\{2\\}-\d\\{2\\}\s\d\\{2\\}:\d\\{2\\}$/;
            if (_mode === "dateminute") \\{
                // yyyy-MM-dd HH:mm
                // 验证是否合法
                secondReg.test(showTimeValue) &&
                    (showTimeValue = showTimeValue.substring(
                        0,
                        showTimeValue.lastIndexOf(":")
                    ));
                munithReg.test(showTimeValue) ||
                    (showTimeValue = currentTime.substring(
                        0,
                        currentTime.lastIndexOf(":")
                    ));
            \\} else \\{
                // yyyy-MM-dd HH:mm:ss
                munithReg.test(showTimeValue) && (showTimeValue += ":00");
                secondReg.test(showTimeValue) || (showTimeValue = currentTime);
            \\}
            return showTimeValue;
        \\},
        //获取年份、月份、小时、分钟、秒
        //@param \\{Number\\} _start 开始值
        //@param \\{Number\\} _end   结束值
        //@param \\{Number\\} _type  类型
        _gotDateTimeList(\\{ _start, _end, _type \\}) \\{
            let resultDataList = new Array();
            for (let i = _start; i <= _end; i++) \\{
                resultDataList.push(this._addZore(i) + this.dateDetails[_type]);
            \\}
            return resultDataList;
        \\},
        //获取天数
        //@param \\{Number\\} _year  年份
        //@param \\{Number\\} _mouth  月份
        _gotDayList(_year, _mouth) \\{
            let now = new Date(_year, _mouth, 0);
            const dayLength = now.getDate();
            let dayList = new Array();
            for (let i = 1; i <= dayLength; i++) \\{
                dayList.push(this._addZore(i) + "日");
            \\}
            return dayList;
        \\},
        //补零
        //@param \\{Number\\} _num  数值
        _addZore(_num) \\{
            return _num < 10 ? "0" + _num : _num.toString();
        \\},
        //回显时间
        //@param \\{Number\\} _showTimeValue  初始化时要显示的时间
        _echoDateTime(_showTimeValue) \\{
            const rangeList = this.rangeList;
            let rangeValue = new Array();
            const list = _showTimeValue.split(/[\-|\:|\s]/);
            list.map((el, index) => \\{
                rangeList[index].map((item, itemIndex) => \\{
                    item.indexOf(el) !== -1 && rangeValue.push(itemIndex);
                \\});
            \\});
            this.rangeValue = rangeValue;
        \\},
        //点击确定时触发的回调函数
        //@param \\{Number\\} ev
        selectChangeFn(ev) \\{
            const selectValues = ev.detail.value;
            const rangeList = this.rangeList;
            let dateTime = "";
            selectValues.map((el, index) => \\{
                dateTime += rangeList[index][el].substring(
                    0,
                    rangeList[index][el].length - 1
                );
                if (index == 0 || index == 1) \\{
                    dateTime += "-";
                \\} else if (
                    index == 3 ||
                    (index == 4 && index != selectValues.length - 1)
                ) \\{
                    dateTime += ":";
                \\} else if (index == 2 && index != selectValues.length - 1) \\{
                    dateTime += " ";
                \\}
            \\});
            // 触发父组件把值传递给父组件
            this.$emit("change", dateTime);
            // this.triggerEvent("change", \\{ value: dateTime \\});
        \\},
        // 当具体的一项的值发生改变时触发
        // @param \\{Number\\} ev
        selectColumnChangeFn(ev) \\{
            const \\{ column, value \\} = ev.detail;
            let rangeList = this.rangeList;
            let rangeValue = this.rangeValue;
            let selectValue = Number(
                rangeList[column][value].substring(
                    0,
                    rangeList[column][value].length - 1
                )
            );
            if (column === 1) \\{
                // 改变月份
                const currentYear = Number(
                    rangeList[0][rangeValue[0]].substring(
                        0,
                        rangeList[0][rangeValue[0]].length - 1
                    )
                );
                const dayList = this._gotDayList(currentYear, selectValue);
                rangeList[column + 1] = dayList;
            \\}
            this.rangeList = rangeList;
        \\},
        // 格式化日期
        formatTime(date) \\{
            const year = date.getFullYear();
            const month = date.getMonth() + 1;
            const day = date.getDate();
            const hour = date.getHours();
            const minute = date.getMinutes();
            const second = date.getSeconds();
            return (
                [year, month, day].map(this.formatNumber).join("/") +
                " " +
                [hour, minute, second].map(this.formatNumber).join(":")
            );
        \\},
        formatNumber(n) \\{
            n = n.toString();
            return n[1] ? n : "0" + n;
        \\},
    \\},
\\};
</script>

<style scoped lang="scss">
.toast_content_box \\{
    display: flex;
    width: 100\\%;
    height: 100\\%;
    justify-content: center;
    align-items: center;
    position: fixed;
    z-index: 999;
    top: 0;
\\}
.toast_content \\{
    background: rgba(0, 0, 0, 0.8);
    border-radius: 16rpx;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    max-width: 284rpx;
    min-width: 256rpx;
    min-height: 236rpx;
\\}
.toast_content_image \\{
    margin: 48rpx 32rpx 0 32rpx;
    width: 80rpx;
    height: 80rpx;
\\}
.text \\{
    /* margin: 20rpx 32rpx 48rpx 32rpx; */
    text-align: center;
    font-size: 32rpx;
    font-family: PingFangSC-Regular, PingFang SC;
    font-weight: 400;
    color: #ffffff;
    line-height: 40rpx;
\\}
.img_magin \\{
    margin: 20rpx 32rpx 48rpx 32rpx;
\\}
.no_img \\{
    margin: 20rpx 32rpx 20rpx 32rpx;
\\}
</style>
```

使用方式：

```
<date-time mode="dateminute" :value="formModel.use_start" @change="startChange">
	<view class="msg">
        <text>\\\{\\\{ use_start\\\}\\\} }}</text>
        <image src="/static/images/index_icon5.png"></image>
    </view>
</date-time>

// 用车开始时间，时分的事件方法，如果需要时分秒参考https://blog.csdn.net/Shids_/article/details/122084621
startChange(dateTime) \\{
    this.formModel.use_start = dateTime + ':00'
    this.use_start = this.formModel.use_start.replace(/-/g, '/')
\\},
```



### 输入框下拉组件DropDown.vue

```
<template>
    <view class="drop-down"
        v-if="isShow&&list.length">
        <view class="drop-list"
            @touchstart='touch(1)'
            @touchmove='touch(2)'
            @touchend='touch(3)'>
            <view class="drop-item"
                v-for="(item,index) in list"
                :key="index"
                @click="change(item,index)"
                v-html="highLight(item[label])">
            </view>
        </view>
    </view>
</template>

<script>
import Utils from '@/utils/index'

export default \\{
    props: \\{
        // 列表数据
        list: \\{
            type: Array,
            default: []
        \\},
        // 搜索词
        keyword: \\{
            type: String,
            default: ''
        \\},
        // 显示字段
        label: \\{
            type: String,
            default: 'label'
        \\}
    \\},
    data() \\{
        return \\{
            isShow: false // 是否显示
        \\}
    \\},
    computed: \\{
        highLight() \\{
            return (data) => \\{
                return Utils.highLight(this.keyword, data, '#247bff')
            \\}
        \\}
    \\},
    created() \\{\\},
    methods: \\{
        // 打开
        show() \\{
            this.isShow = true
        \\},
        // 关闭
        close() \\{
            this.isShow = false
        \\},
        // 触摸事件
        touch(type) \\{
            console.log(type)
            this.$emit('touch', type)
        \\},
        // 选择
        change(item) \\{
            console.log(item)
            this.$emit('change', item)
            // this.close()
        \\}
    \\}
\\}
</script>

<style  lang="scss" scoped>
.drop-down \\{
    width: 686rpx;
    border-radius: 8rpx;
    position: absolute;
    top: 110rpx;
    left: 0;
    z-index: 10;
    background: #ffffff;
    color: #1d2126;
    box-shadow: 0rpx 4rpx 16rpx 0rpx rgba(0, 0, 0, 0.12);
    .drop-list \\{
        // 避免ios闪烁
        max-height: 368rpx;
        overflow-y: auto;
        .drop-item \\{
            line-height: 44rpx;
            padding: 24rpx;
            font-size: 28rpx;
        \\}
    \\}
\\}
</style>
```

使用方式：

```
<view class="page"
        @touchmove='touchmove'>
        
    		<input v-model="car_num"
                :adjust-position="false"
                maxlength="10"
                placeholder="搜索车牌号"
                @focus="focus"
                @input="input"
                @blur="blur" />
            <drop-down ref="dropRef"
                :list="carList"
                :keyword="car_num"
                @touch="touch"
                @change="change"></drop-down>
        
</view>


        touchType: 3, // 下拉框触摸事件类型，3为结束
        isFocus: false, // 是否聚焦


		// 输入框聚焦
        focus() \\{
            this.$refs.dropRef.show()
        \\},
        // 输入框失焦
        blur() \\{
            if (this.touchType === 3) \\{
                setTimeout(() => \\{
                    this.$refs.dropRef.close()
                    this.isFocus = false
                \\}, 200)
            \\}
        \\},
        // 选择车辆
        change(item) \\{
            this.car_num = item.label
            this.$refs.dropRef.close()
            this.isFocus = false
            this.close()
            if (this.car_num) \\{
                // 如果有车牌号，根据车牌号过滤
                this.markers = this.allMarkers.filter(
                    (item) => item.car_num === this.car_num
                )
                this.includePoints()
            \\}
        \\},
        // 输入
        input() \\{
            if (this.car_num) \\{
                // 如果有车牌号，根据车牌号过滤
                this.carList = this.allCarList.filter(
                    (item) => item.label.indexOf(this.car_num) !== -1
                )
            \\} else \\{
                // 清空输入框刷新
                this.markers = this.allMarkers
                this.carList = this.allCarList
                this.includePoints()
            \\}
        \\},
        // 下拉框触摸事件
        touch(type) \\{
            this.touchType = type
        \\},
        // 页面触摸移动事件
        touchmove() \\{
            if (this.isFocus) \\{
                this.blur()
            \\}
        \\},
```



### 菜单栏组件ListBar.vue

```
<template>
    <view class="list-bar"
        v-if="isShow"
        @click="click">
        <view class="left">
            <image :src="icon" />
            <text>\\\{\\\{ title\\\}\\\} }}</text>
        </view>
        <view class="right">
            <view class="circle"
                v-if="num">
                <text>\\\{\\\{ num\\\}\\\} }}</text>
            </view>
            <image class="arrow"
                src="/static/images/right_arrow.png" />
        </view>
    </view>
</template>

<script>
export default \\{
    props: \\{
        // 是否显示（默认不显示，防止用户看到后又消失）
        isShow: \\{
            type: Boolean,
            default: false
        \\},
        // 标题
        title: \\{
            type: String,
            default: ''
        \\},
        // 左侧的图标
        icon: \\{
            type: String,
            default: ''
        \\},
        // 跳转路由
        url: \\{
            type: String,
            default: ''
        \\},
        // 消息数
        num: \\{
            type: Number,
            default: 0
        \\}
    \\},
    data() \\{
        return \\{\\}
    \\},
    computed: \\{\\},
    created() \\{\\},
    methods: \\{
        // 点击事件
        click() \\{
            if (this.url) \\{
                // 有跳转路由
                uni.navigateTo(\\{
                    url: this.url
                \\})
            \\} else \\{
                this.$emit('click')
            \\}
        \\}
    \\}
\\}
</script>

<style scoped lang="scss">
.list-bar \\{
    position: relative;
    height: 108rpx;
    display: flex;
    justify-content: space-between;
    align-items: center;
    .left \\{
        font-size: 32rpx;
        display: flex;
        align-items: center;
        color: #33373d;
        image \\{
            width: 36rpx;
            height: 36rpx;
            margin-right: 20rpx;
        \\}
    \\}
    .right \\{
        display: flex;
        align-items: center;
        .circle \\{
            width: 32rpx;
            height: 32rpx;
            border-radius: 50\\%;
            font-size: 20rpx;
            display: flex;
            align-items: center;
            justify-content: center;
            color: #fff;
            background: red;
        \\}
    \\}
    .arrow \\{
        width: 40rpx;
        height: 40rpx;
    \\}
\\}
</style>
```

使用方式：

```
			<list-bar isShow
                title="车辆管理"
                icon="/static/images/icon_car.png"
                @click="carList"></list-bar>
            <list-bar :isShow="userInfo.role_type===2"
                title="车辆定位"
                icon="/static/images/my_position.png"
                url="/sub_my/car/CarPosition"></list-bar>
            <list-bar isShow
                title="消息通知"
                icon="/static/images/message.png"
                url="/sub_my/notice/Notices"
                :num="userInfo.notice_num"></list-bar>
```



### 弹窗组件Popup.vue

```
<template>
    <view class="overlay"
        v-if="isShow"
        @click="close">
        <!-- @click.stop=""防止点击弹窗标题触发关闭 -->
        <view :style="\\{'padding-bottom':bottom+'px'\\}"
            class="popup"
            @click.stop="">
            <slot></slot>
        </view>
    </view>
</template>

<script>
import \\{ mapState \\} from 'vuex'

export default \\{
    props: \\{
        // 是否需要兼容ios安全区
        isSafe: \\{
            type: Boolean,
            default: true
        \\}
    \\},
    data() \\{
        return \\{
            isShow: false, // 是否显示
            bottom: 34 // padding-bottom高度
        \\}
    \\},
    computed: \\{
        ...mapState(\\{
            systemInfo: (state) => state.login.systemInfo
        \\})
    \\},
    created() \\{
        if (this.isSafe) \\{
            this.bottom = this.systemInfo.safeAreaInsets.bottom
        \\} else \\{
            this.bottom = 0
        \\}
    \\},
    methods: \\{
        /**
         * 展示弹框
         */
        show() \\{
            this.isShow = true
        \\},
        /**
         * 隐藏弹框
         */
        close() \\{
            this.isShow = false
        \\}
    \\}
\\}
</script>

<style scoped lang="scss">
.overlay \\{
    width: 100\\%;
    height: 100\\%;
    position: fixed;
    left: 0;
    top: 0;
    z-index: 99;
    transition-duration: 300ms;
    background: rgba(0, 0, 0, 0.5);
\\}
.popup \\{
    width: 100\\%;
    position: fixed;
    bottom: 0;
    border-radius: 32rpx 32rpx 0 0;
    background: #ffffff;
\\}
</style>
```

使用方式：

```
		<!-- 选择用车类型弹窗 -->
        <popup ref="carRef">
            <view class="popup-list">
                
            </view>
        </popup>
        
        // 显示选择车辆弹窗
        showCar() \\{
            this.$refs.carRef.show()
        \\},
        // 关闭选择车辆弹窗
        closeCar() \\{
            this.$refs.carRef.close()
        \\},
```



### 弹窗选择器组件Select.vue

```
<template>
    <popup ref="popupRef">
        <view class="popup">
            <view class="popup-title">
                <image @click="close"
                    src="/static/images/icon1.png" />
                <view class="ellipsis-one">\\\{\\\{titl\\\}\\\}e}}</view>
            </view>
            <view class="popup-list">
                <view :class="item.disabled ? 'popup-item placeholder' : 'popup-item'"
                    v-for="(item, index) in list"
                    :key="index"
                    @click="change(item)">
                    <view class="ellipsis-tow"
                        v-if="labelSlot">
                        <text>\\\{\\\{ item[label]\\\}\\\} }} | \\\{\\\{ item[labelSlot]\\\}\\\} }}</text>
                        <view class="state state-orange"
                            v-if="item.travel_state">出行中</view>
                        <!-- <slot name="label"
                            :item="item"></slot> -->
                    </view>
                    <view class="ellipsis-tow"
                        v-else>
                        \\\{\\\{ item[label]\\\}\\\} }}
                    </view>
                    <image v-if="item[value] === selected"
                        src="/static/images/icon2.png" />
                </view>
            </view>
        </view>
    </popup>
</template>

<script>
import Popup from '@/components/Popup'

export default \\{
    components: \\{
        Popup
    \\},
    props: \\{
        // 标题
        title: \\{
            type: String,
            default: ''
        \\},
        // 列表数据
        list: \\{
            type: Array,
            default: []
        \\},
        // 显示字段
        label: \\{
            type: String,
            default: 'label'
        \\},
        // 自定义其余显示字段
        labelSlot: \\{
            type: String,
            default: ''
        \\},
        // 绑定字段（key是关键词，如果用了会和vue的key冲突）
        value: \\{
            type: String,
            default: 'key'
        \\},
        // 选中项（不需要定义类型和默认值）
        selected: \\{\\}
    \\},
    data() \\{
        return \\{\\}
    \\},
    computed: \\{\\},
    created() \\{\\},
    methods: \\{
        // 显示弹窗
        show() \\{
            this.$refs.popupRef.show()
        \\},
        // 关闭弹窗
        close() \\{
            this.$refs.popupRef.close()
        \\},
        // 选择
        change(item) \\{
            console.log(item)
            if (item.travel_state) \\{
                // 不能选择出行中的
                return
            \\}
            this.$emit('change', item)
            if (!item.disabled) \\{
                // 不是禁用，才能关闭
                this.close()
            \\}
        \\}
    \\}
\\}
</script>

<style lang="scss" scoped>
.popup \\{
    width: 100\\%;
    border-radius: 32rpx 32rpx 0 0;
    color: #1d2126;
    background: #ffffff;
    image \\{
        width: 40rpx;
        height: 40rpx;
    \\}
    .popup-title \\{
        padding: 34rpx 40rpx;
        font-size: 36rpx;
        font-weight: 500;
        display: flex;
        align-items: center;
        border-bottom: 1px solid #f5f7fa;
        .ellipsis-one \\{
            width: 590rpx;
            line-height: 52rpx;
            text-align: center;
        \\}
    \\}
    .popup-list \\{
        min-height: 224rpx;
        max-height: 70vh;
        overflow: auto;
        .popup-item \\{
            padding: 32rpx 40rpx;
            font-size: 32rpx;
            display: flex;
            align-items: center;
            justify-content: space-between;
            &:hover \\{
                // 置灰时如果点击不生效会有背景色，所以先注释掉
                // background: #f0f2f5;
            \\}
            .ellipsis-tow \\{
                max-width: 614rpx;
                line-height: 48rpx;
                display: flex;
                align-items: center;
                .state \\{
                    line-height: 36rpx;
                    padding: 2rpx 16rpx;
                    margin-left: 16rpx;
                    border-radius: 8rpx;
                    font-size: 24rpx;
                \\}
                .state-orange \\{
                    color: #ff9900;
                    background: #fff4e0;
                \\}
            \\}
        \\}
    \\}
\\}
</style>
```

使用方式：

```
		<Select ref="carRef"
            title="使用车辆"
            :list="carList"
            label="car_num"
            labelSlot="name"
            value="car_num"
            :selected="formModel.car_num"
            @change="carSelected">
            <!-- <template v-slot:label="\\{item\\}">
                \\\{\\\{ item.car_num\\\}\\\} }} | \\\{\\\{ item.name\\\}\\\} }}
            </template> -->
        </Select>
```



### 步骤条组件Step.vue

```
<template>
    <view class="step">
        <view class="item"
            v-for="(item,index) in list"
            :key="index">
            <view :class="['tag',\\{'tag-black':index<active,'tag-blue':index===active,'tag-grey':index>active\\}]">
                <view class="circle">\\\{\\\{index+\\\}\\\}1}}</view>
                <text>\\\{\\\{ite\\\}\\\}m}}</text>
            </view>
            <view :class="\\{'line1':list.length===2,'line2':list.length===3,'line3':list.length===4,'line-blue':index<active,'line-grey':index>=active,\\}"
                v-if="index<list.length-1"></view>
        </view>
    </view>
</template>

<script>
export default \\{
    props: \\{
        list: \\{
            type: Array,
            default: []
        \\},
        active: \\{
            type: Number,
            default: 0
        \\}
    \\},
    data() \\{
        return \\{\\}
    \\},
    computed: \\{\\},
    created() \\{\\},
    methods: \\{\\}
\\}
</script>

<style scoped lang="scss">
.step \\{
    width: 100\\%;
    display: flex;
    align-items: center;
    justify-content: space-between;
    color: #33373d;
    background: #fff;
    .item \\{
        display: flex;
        .tag \\{
            display: flex;
            flex-direction: column;
            align-items: center;
            font-size: 24rpx;
            .circle \\{
                width: 40rpx;
                height: 40rpx;
                line-height: 40rpx;
                border-radius: 50\\%;
                margin-bottom: 12rpx;
                text-align: center;
            \\}
            text \\{
                line-height: 34rpx;
                white-space: nowrap;
            \\}
        \\}
        .tag-black \\{
            .circle \\{
                color: #247bff;
                border: 2rpx solid #247bff;
            \\}
        \\}
        .tag-blue \\{
            .circle \\{
                color: #fff;
                background: #247dff;
            \\}
            text \\{
                font-weight: 500;
                color: #247bff;
            \\}
        \\}
        .tag-grey \\{
            .circle \\{
                color: rgba(0, 0, 0, 0.26);
                border: 2rpx solid #c5c5c5;
            \\}
            text \\{
                color: #b0b3b8;
            \\}
        \\}
        .line1 \\{
            width: 479rpx;
            height: 1rpx;
            margin-top: 20rpx;
        \\}
        .line2 \\{
            width: 190rpx;
            height: 1rpx;
            margin-top: 20rpx;
        \\}
        .line3 \\{
            width: 132rpx;
            height: 1rpx;
            margin-top: 20rpx;
        \\}
        .line-blue \\{
            background: #247bff;
        \\}
        .line-grey \\{
            background: #dcdcdc;
        \\}
    \\}
\\}
</style>
```

使用方式：

```
<!-- 自定义步骤条 -->
<Step :list="list" :active="active"></Step>

list: ['上传', '添加', '签署'],
active: 2
```



### 提示栏组件TipBar.vue

```
<template>
    <view :class="isRed?'tip-bar red':'tip-bar orange'"
        v-if="isShow"
        @click="go">
        <view class="flex-view">
            <image class="icon"
                :src="isRed?'/static/images/warn2.png':'/static/images/icon.png'" />
            <text>\\\{\\\{titl\\\}\\\}e}}</text>
        </view>
        <view class="flex-view">
            <text>\\\{\\\{operat\\\}\\\}e}}</text>
            <image class="next"
                :src="isRed?'/static/images/next_red.png':'/static/images/next_yellow.png'" />
        </view>
    </view>
</template>

<script>
export default \\{
    props: \\{
        // 是否显示
        isShow: \\{
            type: Boolean,
            default: false
        \\},
        // 是否为红色
        isRed: \\{
            type: Boolean,
            default: false
        \\},
        // 标题
        title: \\{
            type: String,
            default: ''
        \\},
        // 操作文案
        operate: \\{
            type: String,
            default: ''
        \\}
    \\},
    data() \\{
        return \\{\\}
    \\},
    computed: \\{\\},
    created() \\{\\},
    methods: \\{
        // 点击事件
        go() \\{
            this.$emit('go')
        \\}
    \\}
\\}
</script>

<style scoped lang="scss">
.tip-bar \\{
    height: 64rpx;
    line-height: 64rpx;
    padding: 0 20rpx 0 16rpx;
    margin-bottom: 32rpx;
    border-radius: 8rpx;
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-size: 24rpx;

    .flex-view \\{
        display: flex;
        align-items: center;
        .icon \\{
            width: 32rpx;
            height: 32rpx;
            margin-right: 8rpx;
        \\}
        .next \\{
            width: 24rpx;
            height: 24rpx;
        \\}
    \\}
\\}
.red \\{
    color: #ed4013;
    background: #ffefe6;
\\}
.orange \\{
    color: #ff9900;
    background: #fff4db;
\\}
</style>
```

使用方式：

```
<tip-bar :isShow="accountState"
    title="您还未添加收款账户信息，请立即前往"
    operate="去添加"
    @go="goAddAccount"></tip-bar>
```



### 自定义toast组件Toast.vue

```
<template>
    <view class="toast_content_box" v-if="isShow">
        <view class="toast_content">
            <image v-if="url" class="toast_content_image" :src="url"></image>
            <view :class="url ? 'text img_magin' : 'text no_img'">\\\{\\\{ text\\\}\\\} }}</view>
        </view>
    </view>
</template>

<script>
export default \\{
    props: \\{\\},
    data() \\{
        return \\{
            isShow: false, // 是否显示
            url: "", // 提示图片路径
            text: "", // 提示内容
        \\};
    \\},
    computed: \\{\\},
    created() \\{ \\},
    methods: \\{
        /**
         * 展示提示
         * @param \\{String\\} type 提示类型
         * @param \\{String\\} text 提示内容
         */
        show(type, text) \\{
            if (type === "success") \\{
                this.url = "/static/images/toast_success.png";
            \\} else if (type === "alert") \\{
                this.url = "/static/images/toast_alert.png";
            \\}
            this.text = text;
            this.isShow = true;
            let _this = this;
            // 定时关闭
            setTimeout(function () \\{
                _this.isShow = false;
            \\}, 1500);
        \\},
    \\},
\\};
</script>

<style scoped lang="scss">
.toast_content_box \\{
    display: flex;
    width: 100\\%;
    height: 100\\%;
    justify-content: center;
    align-items: center;
    position: fixed;
    z-index: 999;
    top: 0;
	left: 0;
\\}

.toast_content \\{
    background: rgba(0, 0, 0, 0.8);
    border-radius: 16rpx;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    max-width: 284rpx;
    min-width: 256rpx;
    min-height: 236rpx;
\\}

.toast_content_image \\{
    margin: 48rpx 32rpx 0 32rpx;
    width: 80rpx;
    height: 80rpx;
\\}

.text \\{
    /* margin: 20rpx 32rpx 48rpx 32rpx; */
    text-align: center;
    font-size: 32rpx;
    font-family: PingFangSC-Regular, PingFang SC;
    font-weight: 400;
    color: #ffffff;
    line-height: 40rpx;
\\}

.img_magin \\{
    margin: 20rpx 32rpx 48rpx 32rpx;
\\}

.no_img \\{
    margin: 20rpx 32rpx 20rpx 32rpx;
\\}
</style>
```

使用方式：

```
		<!-- 自定义提示 -->
        <Toast ref="toastRef"></Toast>
        
        this.$refs.toastRef.show('success', '添加成功')
```



### 图片上传列表组件Upload.vue

```
<template>
    <view>
        <!-- 单文件 -->
        <view class="list"
            v-if="isSingle">
            <view class="item"
                v-if="url">
                <image class="upload img-border"
                    mode="aspectFill"
                    :src="url"
                    @click="preview(url)" />
                <image class="close"
                    v-if="url&&isAdd"
                    @click="del"
                    src="/static/images/index_icon11.png" />
            </view>
            <view class="item"
                v-else>
                <view :class="isCheck&&!url?'upload upload-err':'upload'"
                    @click="upload">
                    <image v-if="isCheck&&!url"
                        src="/static/images/upload_err.png" />
                    <image v-else
                        src="/static/images/index_icon10.png" />
                </view>
            </view>
        </view>
        <!-- 多文件 -->
        <view :class="['list',\\{'show3':columns===3,'show4':columns===4\\}]"
            v-else>
            <view class="item mb"
                v-for="(item,index) in files"
                :key="index">
                <image class="upload img-border"
                    mode="aspectFill"
                    :src="item.url"
                    @click="preview(item)" />
                <image class="close"
                    v-if="item.url&&isAdd"
                    @click="del(index)"
                    src="/static/images/index_icon11.png" />
            </view>
            <view class="item"
                v-if="isAdd">
                <view :class="isCheck&&!files.length?'upload upload-err':'upload'"
                    @click="upload">
                    <image v-if="isCheck&&!files.length"
                        src="/static/images/upload_err.png" />
                    <image v-else
                        src="/static/images/index_icon10.png" />
                </view>
            </view>
            <!-- 一行有两个元素的时候再加一个元素 -->
            <view class="item"
                v-if="columns===4&&files.length\\%4===1">
            </view>
        </view>
    </view>
</template>

<script>
export default \\{
    props: \\{
        // 是否为单个
        isSingle: \\{
            type: Boolean,
            default: true
        \\},
        // 单个地址
        url: \\{
            type: String,
            default: ''
        \\},
        // 多个地址
        files: \\{
            type: Array,
            default: []
        \\},
        // 是否为添加/编辑
        isAdd: \\{
            type: Boolean,
            default: true
        \\},
        // 是否核验
        isCheck: \\{
            type: Boolean,
            default: false
        \\},
        // 列数
        columns: \\{
            type: Number,
            default: 4
        \\}
    \\},
    data() \\{
        return \\{\\}
    \\},
    computed: \\{\\},
    created() \\{\\},
    methods: \\{
        // 预览图片
        preview(item) \\{
            let urls,
                current = 0
            if (this.isSingle) \\{
                urls = [item]
            \\} else \\{
                // 需要预览的图片链接列表
                urls = this.files.map((it) => it.url)
                // 当前显示图片的链接/索引值
                current = urls.indexOf(item.url)
            \\}
            uni.previewImage(\\{
                urls,
                current
            \\})
        \\},
        // 删除
        del(index) \\{
            this.$emit('del', index)
        \\},
        // 上传
        upload() \\{
            this.$emit('upload')
        \\}
    \\}
\\}
</script>

<style  lang="scss" scoped>
.list \\{
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    .mb \\{
        margin-bottom: 20rpx;
    \\}
    .item \\{
        width: 144rpx;
        position: relative;
        .upload \\{
            width: 140rpx;
            height: 140rpx;
            border-radius: 10rpx;
            display: flex;
            align-items: center;
            justify-content: center;
            background: #f5f7fa;
            border: dashed 2rpx #e6e8eb;
            image \\{
                width: 56rpx;
                height: 56rpx;
            \\}
        \\}
        .img-border \\{
            border: solid 2rpx #e6e8eb;
        \\}
        .upload-err \\{
            background: #ffe7e6;
            border: dashed 2rpx #e34950;
        \\}
        .close \\{
            width: 28rpx;
            height: 28rpx;
            position: absolute;
            top: 8rpx;
            right: 8rpx;
            z-index: 1;
        \\}
    \\}
\\}
// 3列
.show3 \\{
    // 防止最后一排两个的时候分散在两边
    &::after \\{
        content: '';
        width: 144rpx;
    \\}
    .item \\{
        width: 144rpx;
        .upload \\{
            width: 140rpx;
            height: 140rpx;
        \\}
    \\}
\\}
// 4列
.show4 \\{
    // 防止最后一排两个的时候分散在两边
    &::after \\{
        content: '';
        width: 144rpx;
    \\}
    .item \\{
        width: 144rpx;
        .upload \\{
            width: 140rpx;
            height: 140rpx;
        \\}
    \\}
\\}
</style>
```

使用方式：

```
<!-- 单文件 -->
<Upload :url="formModel.startPic.url"
    :isCheck="isCheck"
    @upload="uploadDashboard"
    @del="delDashboard"></Upload>
<!-- 多文件 -->
<Upload :isSingle="false"
    :files="item.file"
    :isCheck="isCheck"
    @upload="uploadImg(index)"
    @del="(e)=>delVoucher(e,index)"></Upload>
```

