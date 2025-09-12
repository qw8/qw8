---
title: 前端规范
date: 2022-11-25 15:26:47
categories: 
- 前端知识
tags:
- 前端
---

### 组件@returnPhone="returnPhone"和@return-phone="returnPhone"应该使用哪种写法

在Vue.js中，你可以使用两种方式来绑定事件处理器：驼峰式命名（camelCase）和短横线分隔式命名（kebab-case）。这两种写法在Vue中都是有效的，但是它们的使用场景略有不同。

1. **驼峰式命名**：`@returnPhone="returnPhone"`

   这是更常见的用法。当你直接在模板中定义内联事件处理器时，通常会使用这种形式。它与JavaScript方法名保持一致，因为JavaScript不支持变量名或函数名中包含短横线。

2. **短横线分隔式命名**：`@return-phone="returnPhone"`

   这种写法主要用于HTML属性，因为它遵循了HTML属性的标准命名规则。在Vue中，当你的事件处理器是在HTML标签上作为属性出现时，可以使用这种方式。Vue内部会自动将短横线分隔的名字转换为驼峰式命名的形式，因此你依然可以在方法中使用`returnPhone`这个名字。

#### 总结
- 如果你在`.vue`文件中的`<template>`部分写代码，推荐使用驼峰式命名`@returnPhone`，因为它看起来更像是JavaScript的一部分，并且与可能在`<script>`部分定义的方法名相匹配。
- 如果你需要确保兼容性或者出于某种原因必须使用纯HTML风格的语法，那么可以使用短横线分隔式命名`@return-phone`。

无论选择哪种方式，在Vue组件内部它们最终都会指向同一个方法`returnPhone`。选择主要取决于团队约定和个人偏好以及是否需要保持HTML标准样式的一致性。

