---
title: uniapp安卓IOS
date: 2023-04-27 17:03:10
categories: 
- 前端知识
tags:
- uniapp
---

### uniapp---app开发(nvue)

1. 如果view包括文字，需要再文字外层包括text

2. 不能使用百分比控制宽高，vh，vw也不支持

3. 仅支持css写法

4. nvue 页面只能使用`flex`布局，nvue 页面的布局排列方向默认为竖排（`column`）

5. 文字内容，必须、只能在`<text>`组件下。不能在`<div>`、`<view>`的`text`区域里直接写文字。否则即使渲染了，也无法绑定js里的变量

6. 只有`text`标签可以设置字体大小，字体颜色。

7. 布局不能使用百分比、没有媒体查询。

8. padding不生效

9. 小程序和app-vue中，`<map>` 组件是由引擎创建的原生组件，它的层级是最高的，不能通过 z-index 控制层级。在`<map>`上绘制内容，可使用组件自带的`marker、controls`等属性，也可以使用`<cover-view>`组件。App端还可以使用plus.nativeObj.view 或 subNVue 绘制原生内容，[参考](https://uniapp.dcloud.net.cn/component/native-component)。另外App端nvue文件不存在层级问题。从微信基础库2.8.3开始，支持map组件的同层渲染，不再有层级问题。

10. App端nvue文件的map和小程序拉齐度更高。vue里的map则与plus.map功能一致，和小程序的地图略有差异。App端使用map推荐使用nvue。

11. App 端使用地图组件需要**向高德或百度等三方服务商申请SDK资质，获取AppKey，打包时需要在manifest文件中勾选相应模块，在SDK配置中填写Appkey。注意申请包名和打包时的包名需匹配一致，证书信息匹配**。在manifest可视化界面有详细申请指南。

12. ios nvue Color 不支持 ARGB 十六进制，使用 rgba(r,g,b,a) 代替

13. 小程序和App的vue页面，主体是webview渲染的。为了提升性能，小程序和App的vue页面下部分ui元素，比如导航栏、tabbar、video、map使用了原生控件。这种方式被称为混合渲染。

14. 部分CSS样式无法应用于原生组件，例如：
    - 无法对原生组件设置 CSS 动画；
    - 无法定义原生组件为 position: fixed；
    - 不能在父级节点使用 overflow: hidden 来裁剪原生组件的显示区域。
    

在小程序端真机上，原生组件会遮挡 vConsole 弹出的调试面板。
    
15. nvue页面，map地图的include-points属性，怎么设置缩放的左右间距

16. nvue页面如果使用组件，组件也需要改成nvue的写法



### cover-view(开发注意)

1. 只支持基本的定位、布局、文本样式。不支持设置单边的`border`、`background-image`、`shadow`、`overflow: visible`等。
2. 自定义组件嵌套 `cover-view` 时，自定义组件的 `slot` 及其父节点暂不支持通过 `wx:if` 控制显隐，否则会导致 `cover-view` 不显示。
3. css不支持标签选择器
4. flex布局默认为column，期望是行排列的话，需要手动改成row
5. cover-view里面放文本不能直接放需要在文本外嵌套webview
6. 只支持基本的定位、布局、文本样式。不支持设置单边的`border`、`background-image`、`shadow`、`overflow: visible`等。单边border不支持



### map组件polyline实时更新

this.polyline.push或者$set()在安卓上面没效果，需要把整个polyline对象通过解构赋值 

```
this.polyline = [...this.route.polyline]
```

