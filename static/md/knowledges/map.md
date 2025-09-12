---
title: 地图
date: 2021-03-21 15:11:22
categories: 
- 前端知识
tags:
- 前端
---

# 百度地图

### 点线绘制

在mixins中

```
export default \\{
    components: \\{
    \\},
    data() \\{
        return \\{
            mapKey: "X6byRrbcPuN5IDlwZ4PQYFAXbQjwju76", // 百度地图开发者密钥
            BMapGL: null, // 地图原型
            map: null, // 地图实例
        \\};
    \\},
    created() \\{
    \\},
    mounted() \\{

    \\},
    destroyed() \\{

    \\},
    methods: \\{
        // 设置地图
        async setMap() \\{
            this.BMapGL = await this.initMap();
            // console.log(this.BMapGL)
            // 位于BMapGL命名空间下的Map类表示地图，通过new操作符可以创建一个地图实例
            this.map = new this.BMapGL.Map("map");
            // 设置地图中心点坐标（为天安门坐标）
            let point = new this.BMapGL.Point(116.404, 39.915);
            // 地图初始化，同时设置地图展示级别
            this.map.centerAndZoom(point, 12);
            let scaleCtrl = new this.BMapGL.ScaleControl();  // 添加比例尺控件
            this.map.addControl(scaleCtrl);
            let zoomCtrl = new this.BMapGL.ZoomControl();  // 添加缩放控件
            this.map.addControl(zoomCtrl);
            this.setMarkers();
        \\},
        // 地图异步加载回调
        initMap() \\{
            const Map_URL =
                "https://api.map.baidu.com/api?v=1.0&&type=webgl&ak=" +
                this.mapKey +
                "&callback=onMapCallback";
            return new Promise((resolve, reject) => \\{
                // 如果已加载直接返回
                if (typeof BMapGL !== "undefined") \\{
                    resolve(BMapGL);
                    return true;
                \\}
                // 地图异步加载回调处理
                window.onMapCallback = function () \\{
                    resolve(BMapGL);
                \\};

                // 插入script脚本
                let scriptNode = document.createElement("script");
                scriptNode.setAttribute("type", "text/javascript");
                scriptNode.setAttribute("src", Map_URL);
                document.body.appendChild(scriptNode);
            \\});
        \\},
        // 设置点标记
        async setMarkers() \\{
            let point, myIcon, marker, src, markers = this.modalData.markers, url = "/static/images/spot/";
            for (let i = 0; i < markers.length; i++) \\{
                if (i === markers.length - 1) \\{
                    // 终点图标路径
                    src =
                        markers[i].clock_state === "2"
                            ? url + "clock6@2x.png"
                            : url + "spot6@2x.png";
                \\} else \\{
                    // 其他点图标路径
                    src =
                        markers[i].clock_state === "2"
                            ? url + `clock$\\{i\\}@2x.png`
                            : url + `spot$\\{i\\}@2x.png`;
                \\}
                // console.log("转换前", markers[i])
                const location = await this.translate(markers[i])
                // console.log("转换后", location)
                // point = new this.BMapGL.Point(116.404, 39.915);
                point = new this.BMapGL.Point(location.longitude, location.latitude);
                myIcon = new this.BMapGL.Icon(src, new this.BMapGL.Size(68, 102), \\{\\});
                // 创建标注对象并添加到地图  
                marker = new this.BMapGL.Marker(point, \\{ icon: myIcon \\});
                this.map.addOverlay(marker);
            \\}
            // 调整到最佳视野
            let startPoint = new this.BMapGL.Point(markers[0].longitude, markers[0].latitude)
            let endPoint = new this.BMapGL.Point(markers[markers.length - 1].longitude, markers[markers.length - 1].latitude)
            this.map.setViewport([startPoint, endPoint])
            // 路线规划（循环每两个点）
            for (let i = 0; i < this.modalData.markers.length - 1; i++) \\{
                this.getLine(
                    this.modalData.markers[i],
                    this.modalData.markers[i + 1]
                );
            \\}
        \\},
        // 将用户GCJ02坐标系的经纬度转换成bd09的坐标系
        translate(item) \\{
            return new Promise((resolve, reject) => \\{
                let ggPoint = new this.BMapGL.Point(item.longitude, item.latitude);
                // console.log(ggPoint, 'ggPoint');
                // 坐标转换完之后的回调函数
                function translateCallback(data) \\{
                    // console.log('translateCallback', data);
                    if (data.status === 0) \\{
                        // 修改原数据
                        item.longitude = data.points[0].lng.toFixed(6)
                        item.latitude = data.points[0].lat.toFixed(6)
                        // 返回新数据 
                        let location = \\{
                            longitude: data.points[0].lng.toFixed(6),
                            latitude: data.points[0].lat.toFixed(6)
                        \\};
                        // console.log(location, '修改后的坐标系');
                        resolve(location)
                    \\} else \\{
                        console.log("转换失败")
                        reject()
                    \\}
                \\}
                let convertor = new this.BMapGL.Convertor();
                let pointArr = [];
                pointArr.push(ggPoint);
                // console.log(pointArr, 'pointArr');
                convertor.translate(pointArr, 3, 5, translateCallback);
            \\})
        \\},
        // 路线规划
        getLine(from, to) \\{
            let _this = this
            let p1 = new this.BMapGL.Point(from.longitude, from.latitude);
            let p2 = new this.BMapGL.Point(to.longitude, to.latitude);
            let driving = new this.BMapGL.DrivingRoute(this.map,
                \\{
                    // 结果呈现设置
                    renderOptions: \\{
                        map: this.map,
                        // 地图大小自适应
                        autoViewport: false
                    \\},
                    // 标注添加完成后的回调函数
                    onMarkersSet: function (routes) \\{
                        _this.map.removeOverlay(routes[0].marker); // 删除起点
                        _this.map.removeOverlay(routes[1].marker); // 删除终点
                    \\},
                    // 折线添加完成后的回调函数
                    onPolylinesSet(routes) \\{
                        // 路线绘制
                        routes.forEach((Route) => \\{
                            let polyline = Route.getPolyline()
                            polyline.setStrokeColor('#04C96D')
                            polyline.setStrokeWeight(5)
                        \\})
                    \\}
                \\});
            driving.search(p1, p2);
        \\}
    \\},
\\};
```



### wgs84坐标系的经纬度转换成bd09的坐标系

通过wx.getLocation且type为wgs84获取用户的当前wgs84坐标系[经纬度](https://so.csdn.net/so/search?q=经纬度&spm=1001.2101.3001.7020)，然后通过百度地图的BMap.Convertor().translate()的api来将用户wgs84坐标系的经纬度转换成bd09的坐标系。 

```
wx.getLocation(\\{
    type: 'wgs84',
    success(res) \\{
      var ggPoint = new BMap.Point(res.longitude, res.latitude);
      function translateCallback(data) \\{
        console.log('translateCallback');
        if (data.status === 0) \\{
          let userLocation = \\{
            longitude: data.points[0].lng.toFixed(6),
            latitude: data.points[0].lat.toFixed(6)
          \\};
          console.log(userLocation, '修改后的坐标系');
          uni.setStorageSync('LYZH_location', userLocation);
        \\} else \\{
          uni.showToast(\\{
            title: '获取定位失败',
            icon: 'none'
          \\});
        \\}
      \\}
      var convertor = new BMap.Convertor();
      console.log(ggPoint, 'ggPoint');
      var pointArr = [];
      pointArr.push(ggPoint);
      console.log(pointArr, 'pointArr');
      convertor.translate(pointArr, 1, 5, translateCallback);
    \\},
    
  \\});
```



### 将用户GCJ02坐标系的经纬度转换成bd09的坐标系

```
		// 将用户GCJ02坐标系的经纬度转换成bd09的坐标系
        translate(item) \\{
            return new Promise((resolve, reject) => \\{
                let ggPoint = new this.BMapGL.Point(item.longitude, item.latitude);
                // console.log(ggPoint, 'ggPoint');
                // 坐标转换完之后的回调函数
                function translateCallback(data) \\{
                    // console.log('translateCallback', data);
                    if (data.status === 0) \\{
                        // 修改原数据
                        item.longitude = data.points[0].lng.toFixed(6)
                        item.latitude = data.points[0].lat.toFixed(6)
                        // 返回新数据 
                        let location = \\{
                            longitude: data.points[0].lng.toFixed(6),
                            latitude: data.points[0].lat.toFixed(6)
                        \\};
                        console.log(location, '修改后的坐标系');
                        resolve(location)
                    \\} else \\{
                        console.log("转换失败")
                        reject()
                    \\}
                \\}
                let convertor = new this.BMapGL.Convertor();
                let pointArr = [];
                pointArr.push(ggPoint);
                // console.log(pointArr, 'pointArr');
                convertor.translate(pointArr, 3, 5, translateCallback);
            \\})
        \\},
```



### 定位不准的问题

本人踩坑点，包括了每次加载都打乱了坐标点的信息，和定位不准问题。

解决如下：注意转换方法convertor.translate对应的参数（其中的1和5）是以下意思。我当时复制过来调用的3和5，所以定位不准，得看你是需要用哪种坐标转换哪种。

```
* 坐标常量说明：
* COORDINATES_WGS84 = 1, WGS84坐标
* COORDINATES_WGS84_MC = 2, WGS84的平面墨卡托坐标
* COORDINATES_GCJ02 = 3，GCJ02坐标
* COORDINATES_GCJ02_MC = 4, GCJ02的平面墨卡托坐标
* COORDINATES_BD09 = 5, 百度bd09经纬度坐标
* COORDINATES_BD09_MC = 6，百度bd09墨卡托坐标
* COORDINATES_MAPBAR = 7，mapbar地图坐标
* COORDINATES_51 = 8，51地图坐标
```





# 腾讯地图

### 点线绘制

调用方式

```
			<div id="map"
            class="map"></div>
			
			// 判断是否存在地图实例，已存在先销毁，避免重复创建
            if (this.tMap) \\{
                this.tMap.destroy();
            \\}
            this.$nextTick(() => \\{
                this.setMap();
            \\});
            
            .map \\{
                margin-top: 16px;
                width: 100\\%;
                height: 500px;
            \\}
```

在mixins中

```
export default \\{
    components: \\{
    \\},
    data() \\{
        return \\{
            mapKey: "X4TBZ-TG56O-6LAW4-S6TOO-3EPW6-ZRBHL", // 腾讯地图开发者密钥
            TMap: null, // 地图原型
            tMap: null, // 地图实例
        \\};
    \\},
    created() \\{
        // Vue的方法给原生调用，则需要把方法挂在Window下面
        window.cb = this.cb;
    \\},
    mounted() \\{

    \\},
    destroyed() \\{

    \\},
    methods: \\{
        // 设置地图
        async setMap() \\{
            const map = document.getElementById("map");
            this.TMap = await this.initMap();
            // 定义地图中心点坐标
            var center = new this.TMap.LatLng(39.866202, 116.307053);
            // 定义map变量，调用 TMap.Map() 构造函数创建地图
            this.tMap = new this.TMap.Map(map, \\{
                center: center, // 设置地图中心点坐标
                zoom: 12, // 设置地图缩放级别
            \\});

            this.fitBounds();
            this.setMarkers();
            for (let i = 0; i < this.modalData.markers.length - 1; i++) \\{
                this.reqPolyline(
                    this.modalData.markers[i],
                    this.modalData.markers[i + 1]
                );
            \\}
        \\},
        // 地图异步加载回调
        initMap() \\{
            const TMap_URL =
                "https://map.qq.com/api/gljs?v=1.exp&libraries=tools,service&key=" +
                this.mapKey +
                "&callback=onMapCallback";
            return new Promise((resolve, reject) => \\{
                // 如果已加载直接返回
                if (typeof TMap !== "undefined") \\{
                    resolve(TMap);
                    return true;
                \\}
                // 地图异步加载回调处理
                window.onMapCallback = function () \\{
                    resolve(TMap);
                \\};

                // 插入script脚本
                let scriptNode = document.createElement("script");
                scriptNode.setAttribute("type", "text/javascript");
                scriptNode.setAttribute("src", TMap_URL);
                document.body.appendChild(scriptNode);
            \\});
        \\},
        // 自动调整地图显示范围
        fitBounds() \\{
            // 有一组坐标点
            let coords = this.modalData.markers.map((item) => \\{
                return new this.TMap.LatLng(item.latitude, item.longitude);
            \\});
            // 创建LatLngBounds实例
            var latlngBounds = new this.TMap.LatLngBounds();
            // 将坐标逐一做为参数传入extend方法，latlngBounds会根据传入坐标自动扩展生成
            for (var i = 0; i < coords.length; i++) \\{
                latlngBounds.extend(coords[i]);
            \\}
            // 调用fitBounds自动调整地图显示范围
            this.tMap.fitBounds(latlngBounds, \\{ padding: 102 \\});
        \\},
        // 设置点标记
        setMarkers() \\{
            // 点标记数据数组
            let geometries = this.modalData.markers.map((item) => \\{
                return \\{
                    id: item.id, // 点标记唯一标识，后续如果有删除、修改位置等操作，都需要此id
                    styleId: "marker" + item.id, // 指定样式id
                    position: new this.TMap.LatLng(
                        item.latitude,
                        item.longitude
                    ), // 点标记坐标位置
                    properties: \\{
                        // 自定义属性
                        title: item.title,
                    \\},
                \\};
            \\});
            // 创建并初始化MultiMarker
            var markerLayer = new this.TMap.MultiMarker(\\{
                // 指定地图容器
                map: this.tMap,
                // 样式定义
                styles: this.setMarkImg(),
                geometries,
            \\});
        \\},
        // 为了设置点标记的图片
        setMarkImg() \\{
            let styleOption = \\{\\};
            let src,
                url = "../../../../static/images/spot/";
            // 遍历图标集合
            this.modalData.markers.map((item, index) => \\{
                if (index === this.modalData.markers.length - 1) \\{
                    src =
                        item.clock_state === "2"
                            ? url + "clock6@2x.png"
                            : url + "spot6@2x.png";
                \\} else \\{
                    src =
                        item.clock_state === "2"
                            ? url + `clock$\\{index\\}@2x.png`
                            : url + `spot$\\{index\\}@2x.png`;
                \\}
                // if (index === 0) \\{
                //     src = "../../../../static/images/spot_start@2x.png";
                // \\} else if (index === this.modalData.markers.length - 1) \\{
                //     src = "../../../../static/images/spot_end@2x.png";
                // \\} else \\{
                //     src = `../../../../static/images/spot$\\{index\\}@2x.png`;
                // \\}
                styleOption["marker" + item.id] = new this.TMap.MarkerStyle(\\{
                    cursor: "pointer",
                    width: 68, // 点标记样式宽度（像素）
                    height: 102, // 点标记样式高度（像素）
                    src,
                    // 部分老数据iconPath不一致，不能直接引用
                    // src: "../../../.." + item.iconPath,
                \\});
            \\});
            return styleOption;
        \\},
        // 路线规划请求
        reqPolyline(from, to) \\{
            // WebServiceAPI请求URL（驾车路线规划默认会参考实时路况进行计算）
            var url = "https://apis.map.qq.com/ws/direction/v1/driving/"; //请求路径
            url += `?from=$\\{from.latitude\\},$\\{from.longitude\\}`; //起点坐标
            url += `&to=$\\{to.latitude\\},$\\{to.longitude\\}`; //起点坐标
            url += "&output=jsonp&callback=cb"; //指定JSONP回调函数名，本例为cb
            url = url + "&key=" + this.mapKey; //开发key，可在控制台自助创建
            //发起JSONP请求，获取路线规划结果（浏览器调用WebServiceAPI需要通过Jsonp的方式）
            var script = document.createElement("script");
            script.src = url;
            document.body.appendChild(script);
        \\},
        // 定义请求回调函数
        cb(ret) \\{
            // 从结果中取出路线坐标串
            var coors = ret.result.routes[0].polyline,
                pl = [];
            // 坐标解压（返回的点串坐标，通过前向差分进行压缩，因此需要解压）
            var kr = 1000000;
            for (var i = 2; i < coors.length; i++) \\{
                coors[i] = Number(coors[i - 2]) + Number(coors[i]) / kr;
            \\}
            // 将解压后的坐标生成LatLng数组
            for (var i = 0; i < coors.length; i += 2) \\{
                pl.push(new TMap.LatLng(coors[i], coors[i + 1]));
            \\}
            this.displayPolyline(pl);
        \\},
        // 显示路线
        displayPolyline(pl) \\{
            //创建 MultiPolyline显示折线
            var polylineLayer = new TMap.MultiPolyline(\\{
                map: this.tMap, //绘制到目标地图
                //折线样式定义
                styles: \\{
                    style: new TMap.PolylineStyle(\\{
                        color: "#04C96D", //线填充色
                        width: 5, //折线宽度
                        borderWidth: 3, //边线宽度
                        borderColor: "#FFF", //边线颜色
                        lineCap: "round", //线端头方式
                    \\}),
                \\},
                //折线数据定义
                geometries: [
                    \\{
                        id: "pl1", //折线唯一标识，删除时使用
                        styleId: "style", //绑定样式名
                        paths: pl,
                    \\},
                ],
            \\});
        \\},
    \\},
\\};
```

待优化：鼠标放到地图不能滚动页面



### 高德地图

按 NPM 方式安装使用 Loader

```
npm i @amap/amap-jsapi-loader --save
```

封装mixins

```
import Config from '@/config'
import AMapLoader from "@amap/amap-jsapi-loader";

export default \\{
    components: \\{
    \\},
    data() \\{
        return \\{
            AMap: null, // 地图原型
            map: null, // 地图实例
        \\};
    \\},
    created() \\{
    \\},
    mounted() \\{

    \\},
    destroyed() \\{

    \\},
    methods: \\{
        // 设置地图
        async setMap() \\{
            this.AMap = await this.initMap();
            // console.log(this.AMap, this.AMap)
            // 位于AMap命名空间下的Map类表示地图，通过new操作符可以创建一个地图实例
            this.map = new this.AMap.Map("map", \\{
                zoom: 10,  //设置地图显示的缩放级别
                center: [116.397428, 39.90923],  //设置地图中心点坐标
                viewMode: '2D'  //设置地图模式
            \\});

            // 地图基础控件
            this.AMap.plugin([
                'AMap.ToolBar',
                'AMap.Scale'
            ], () => \\{
                // 在图面添加工具条控件，工具条控件集成了缩放、平移、定位等功能按钮在内的组合控件
                this.map.addControl(new this.AMap.ToolBar());
                // 在图面添加比例尺控件，展示地图在当前层级和纬度下的比例尺
                this.map.addControl(new this.AMap.Scale());
            \\});

            this.setMarkers();
        \\},
        // 地图异步加载回调
        initMap() \\{
            window._AMapSecurityConfig = \\{
                securityJsCode: Config.gdCode,
            \\};
            return new Promise((resolve, reject) => \\{
                AMapLoader.load(\\{
                    key: Config.gdKey, // 申请好的 Web 端开发者 Key，首次调用 load 时必填
                    version: "2.0", // 指定要加载的 JS API 的版本，缺省时默认为 1.4.15
                    plugins: ["AMap.Scale"], // 需要使用的的插件列表，如比例尺'AMap.Scale'，支持添加多个如：['AMap.Scale','...','...']
                \\})
                    .then((AMap) => \\{
                        resolve(AMap);
                    \\})
                    .catch((e) => \\{
                        console.log(e);
                    \\});
            \\});
        \\},

        // 设置点标记
        async setMarkers() \\{
            if (!this.modalData.markers.length) \\{
                return
            \\}
            let icon, marker, src, url = "/static/images/spot/";
            console.log('点标记', this.modalData.markers);
            let markers = JSON.parse(JSON.stringify(this.modalData.markers));
            const isLine = this.modalData.isLine
            if (isLine) \\{
                markers = []
                markers.push(this.modalData.markers[0])
                markers.push(this.modalData.markers[this.modalData.markers.length - 1])
            \\}
            for (let i = 0; i < markers.length; i++) \\{
                if (i === markers.length - 1) \\{
                    // 终点图标路径
                    src =
                        markers[i].clock_state === "2"
                            ? url + "clock6@2x.png"
                            : url + "spot6@2x.png";
                \\} else \\{
                    // 其他点图标路径
                    src =
                        markers[i].clock_state === "2"
                            ? url + `clock$\\{i\\}@2x.png`
                            : url + `spot$\\{i\\}@2x.png`;
                \\}

                // 创建 AMap.Icon 实例：
                icon = new this.AMap.Icon(\\{
                    size: new this.AMap.Size(68, 102), // 图标尺寸
                    image: src, // Icon 的图像
                    imageOffset: new this.AMap.Pixel(0, 0), // 图像相对展示区域的偏移量，适于雪碧图等
                    imageSize: new this.AMap.Size(68, 102), // 根据所设置的大小拉伸或压缩图片
                \\});
                // 将 Icon 实例添加到 marker 上:
                marker = new this.AMap.Marker(\\{
                    position: new this.AMap.LngLat(markers[i].longitude, markers[i].latitude),
                    offset: new AMap.Pixel(-34, -102), // 当偏移量为 (0, 0) 或缺省时，自定义内容默认以左上角为基准点
                    icon // 添加 Icon 实例
                \\});
                this.map.add(marker);
            \\}

            // 调整到最佳视野
            // 第一个参数为空，表明用图上所有覆盖物 setFitview
            // 第二个参数为false, 非立即执行
            // 第三个参数设置上左下右的空白
            this.map.setFitView(null, false, [102, 60, 60, 60]);

            // 路线绘制
            if (isLine) \\{
                this.setPolyline()
            \\} else \\{
                this.getLine()
            \\}
        \\},

        // 直接用点串绘制路线
        setPolyline() \\{
            let path = this.modalData.markers.map((item) => \\{
                return new this.AMap.LngLat(
                    item.longitude,
                    item.latitude
                )
            \\})
            let polyline = new this.AMap.Polyline(\\{
                path,
                strokeWeight: 8, // 轮廓线宽度,默认为:2
                borderWeight: 2, // 描边的宽度，默认为1
                strokeColor: '#04C96D', // 线条颜色
                lineJoin: 'round', // 折线拐点连接处样式
                showDir: true // 是否延路径显示白色方向箭头,默认false。建议折线宽度大于6时使用
            \\});
            this.map.add(polyline);
        \\},
        // 路线规划
        getLine() \\{
            this.AMap.plugin('AMap.Driving', () => \\{
                // 驾车路线规划服务
                let driving = new this.AMap.Driving(\\{
                    map: this.map,
                    // 驾车路线规划策略，AMap.DrivingPolicy.LEAST_TIME是最快捷模式
                    policy: this.AMap.DrivingPolicy.LEAST_TIME,
                    hideMarkers: true, // 是否隐藏路径规划的起始点图标，默认值为false
                \\})

                // 处理地点坐标
                let point, start, waypoints = [], end, markers = this.modalData.markers
                markers.forEach((item, index) => \\{
                    point = new this.AMap.LngLat(item.longitude, item.latitude)
                    if (index === 0) \\{
                        start = point
                    \\} else if (index === markers.length - 1) \\{
                        end = point
                    \\} else \\{
                        waypoints.push(point)
                    \\}
                \\});
                // console.log(start, waypoints, end);

                // 根据起点、终点和途经点（可选）坐标或名称，实现驾车路线规划，途经点通过opts设定
                driving.search(start, end, \\{ waypoints \\}, (status, result) => \\{
                    // 未出错时，result即是对应的路线规划方案
                    // console.log(status, result);
                    if (status === 'complete') \\{
                        // console.log('绘制驾车路线完成')
                    \\} else \\{
                        console.log('获取驾车数据失败：' + result)
                    \\}
                \\})
            \\})
        \\},

    \\},
\\};
```

