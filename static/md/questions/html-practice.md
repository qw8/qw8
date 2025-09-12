---
title: HTML实践
date: 2024-04-30 11:11:11
categories: 
- 前端问题
tags:
- HTML
---

### HTML map 标签使用详解

在图片中标注usemap：

```html
<img src=""img.jpg" usemap="im_map" /> 
```

定义map：

```html
<map id="im_map" name="im_map">  
    <area shape="rect" coords="0,0,100,100" href="url.html" />
    <area shape="circle" coords="129,161,10" onClick=\\{this.Up\\} alt="Mercury"/>//react中
</map>
```

map标签定义map，area标签定义可点击的热点，area属性：

shape：定义热点形状，可选参数 rect(矩形)、circle(圆形)、poligon(自定义形状)。

coords：定义形状路径：

当shape=rect时，四个数字依次为：起点X、起点Y、终点X、终点Y

当shape=circle时，三个数字依次为：中心点X、中心点Y、半径

当shape=poligon时，可定义多个路径点，依次为：起点X、起点Y、路径1X、路径1Y、路径2X、路径2Y......

href定义点击跳转的地址。

有时候需要动态的为coords属性赋值，在JS中控制coords，demo使用JQ写法：

```js
//使用js控制coords，绘制map热点
var mapStartX = 0;  
var mapStartY = 0;  
var mapEndX = 100;  
var mapEndY = 100;  
var mapFill = mapStartX + ','+ mapStartY + ','+ mapEndX + ','+ mapEndY;  
var im_map = $('#im_map').find('area');  
im_map.attr('coords',mapFill); 
```



### html点击不同模块传递不同参数代码

下面是一个简单的示例，展示了如何在HTML中点击不同的模块并传递不同的参数：

```html
<!DOCTYPE html>
<html>
<body>

<h1>点击不同模块传递不同参数</h1>

<div id="module1" onclick="handleClick('module1', '参数1')">模块1</div>
<div id="module2" onclick="handleClick('module2', '参数2')">模块2</div>
<div id="module3" onclick="handleClick('module3', '参数3')">模块3</div>

<script>
function handleClick(moduleId, parameter) \\{
  // 在这里可以处理点击事件，根据参数进行不同的操作
  console.log("被点击的模块ID：" + moduleId);
  console.log("传递的参数：" + parameter);
\\}
</script>

</body>
</html>
```

在这个示例中，有三个具有不同id的div元素，每个元素都带有一个`onclick`属性来调用`handleClick`函数。当用户点击某个模块时，将调用这个函数，并传递相应的参数。

函数`handleClick`接收两个参数：被点击模块的id和需要传递的参数。可以根据这些参数执行相应的操作，例如在控制台中打印出模块的id和传递的参数。

请注意，这只是一个简单的示例，你可以根据自己的需求进行更复杂的操作。



### 移动端禁止选中内容

如果你不想用户可以选中页面中的内容，那么你可以在css中禁掉：

```
// 禁止选中
.select-none \\{
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
\\}
```



### img标签设置draggable = false

```
<img src="image.jpg" draggable="false">
```

`draggable="false"` 属性用于指定图像元素不可被拖动。

在HTML5中，带有 `img`、`a` 标签的元素默认是可以拖动的（即用户可以点击这些元素并拖拽以创建书签或复制链接等）。但是，当你设置 `draggable="false"` 时，你就禁用了这种行为。

具体来说，在你的代码片段中，这个属性的作用是防止用户将图片拖出浏览器窗口或者开始一个拖放操作。这可能是出于用户体验考虑，比如避免用户意外地拖动图像，或者是为了确保某些交互功能正常工作，例如在一个需要触摸手势的应用中，你可能不希望图像响应拖动手势。

此外，如果你的应用逻辑依赖于点击事件或其他类型的交互，而不想触发默认的拖动行为，那么禁用拖动也是有益的。这样做可以避免当用户试图点击图片时，却无意间触发了浏览器的默认拖动行为。

dragable:

默认值为false,可以用于拖拽，但是一个虚拟的。

a标签，img标签默认自带拖拽，(只有chrome,safari可以使用，firefox不支持，ie不支持)

在HTML5中，`img`标签默认是可拖动的（至少在某些浏览器如Chrome和Safari中）。

当用户尝试拖动图片时，浏览器会根据其默认行为进行处理，例如可能会启动一个文件拖放操作或者执行某种内置的拖放功能。

为了防止这种默认行为，特别是当你不希望网页上的图片被用户意外或无意间拖动时，可以设置`draggable`属性为`false`。
这样，即使用户尝试拖动该图片，也不会有任何效果。

因此，在需要禁用图片拖拽的场景下，通常建议对页面中的每个不需要拖放功能的`img`标签明确设置`draggable="false"`。



### user-drag: none;这个有什么用

`user-drag: none;` 是一个非标准的 CSS 属性，主要用于控制用户是否可以通过鼠标拖动元素来选择文本或启动拖放操作。这个属性并不是 CSS 规范的一部分，因此它的支持在不同浏览器之间可能会有所不同，并且通常带有浏览器特定的前缀，如 `-webkit-user-drag` 用于 WebKit 和 Blink 浏览器（例如 Chrome 和 Safari）。

使用 `user-drag: none;` 的主要目的是防止用户通过鼠标拖动来选择文本或者图像等元素。它与 `user-select` 属性有些类似，但它们的作用并不完全相同：

- `user-drag: none;` 主要是为了阻止拖动行为本身，即当用户尝试用鼠标拖动某个元素时，不会触发默认的拖放操作。
- `user-select: none;` 则是用来控制文本和某些元素的选择行为，即用户无法通过鼠标选中这些元素中的文本内容。

需要注意的是，由于 `user-drag` 不是标准的 CSS 属性，所以其兼容性和实际效果可能因浏览器而异。对于跨浏览器的支持，你可能需要考虑使用其他方法或结合 JavaScript 来实现所需的行为控制。

例如，在 WebKit/Blink 浏览器中，你可以这样使用：

```css
img \\{
  -webkit-user-drag: none;
\\}
```

为了确保更广泛的兼容性，最好还是使用 HTML 的 `draggable="false"` 属性来禁用元素的拖动功能，因为这是标准做法，所有现代浏览器都支持。如果你还需要进一步定制用户体验，可以结合 `user-select` 或者 JavaScript 事件处理程序来实现。

