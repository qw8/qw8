---
title: sass
date: 2019-10-29 19:45:42
categories: 
- 前端知识
tags:
- sass
---

### 选择器

">"代表子选择器，可以选择某个元素中所有的子元素

"+"代表相邻元素选择器，选择紧挨着某个元素的元素



### scss 使用 /deep/ 穿透写法

当 <style> 标签有 scoped 属性时，它的 CSS 只作用于当前组件中的元素。这类似于 Shadow DOM 中的样式封装。它通过使用 PostCSS 来实现以下转换：

```
<template>
  <div class="example" data-v-f3f3eg9>hi</div>
</template>
```

```
<style>
.example[data-v-f3f3eg9] \\{
  color: red;
\\}
</style>
```

PostCSS 给一个组件中的所有 DOM 添加了一个独一无二的动态属性，然后给 CSS 选择器额外添加一个对应的属性选择器来选择该组件中 DOM，这种做法使得样式只作用于含有该属性的 DOM——组件内部 DOM。

问题描述：当我们需要修改 element-ui 内部组件的样式时，我们通常将内部组件的样式放在一个 class 作用域下，同时使用全局作用域的样式去修改默认 ui 样式，代码如下：

```
<style lang="scss">
  .button-box\\{
    .el-button\\{
      padding: 13px 50px;
    \\}
  \\}
</style>
```

混用本地和全局样式
你可以在一个组件中同时使用有 scoped 和非 scoped 样式：

```
<style>
/* 全局样式 */
</style>
```

```
<style scoped>
/* 本地样式 */
</style>
```

如果我们依然使用当前组件的 scoped 属性，那我们如何去修改 element-ui 内部的样式呢？引用了第三方组件，需要在组件中局部修改第三方组件的样式，而又不想去除 scoped 属性造成组件之间的样式污染。此时只能通过特殊的方式，穿透 scoped。下面我们就会介绍这个深度作用选择器。



### 深度作用选择器

如果你希望 scoped 样式中的一个选择器能够作用得“更深”，例如影响子组件，你可以使用 >>> 操作符：

```
<style scoped>
.a >>> .b \\{ /* ... */ \\}
</style>
```

上述代码将会编译成：

```
.a[data-v-f3f3eg9] .b \\{ /* ... */ \\}
```

有些像 Sass 之类的预处理器无法正确解析 >>>。这种情况下你可以使用 /deep/ 或 ::v-deep 操作符取而代之——两者都是 >>> 的别名，同样可以正常工作。

```
<style lang="scss" scoped>
  .button-box\\{
    /deep/ .el-button\\{
      padding: 13px 50px;
    \\}
  \\}
</style>
```

更多详情，请查看 Vue-loader 官网之 Scoped CSS。



### Sass和less的区别是什么？用哪个好

#### 什么是Sass和Less？

   Sass和Less都属于CSS预处理器，**那什么是 CSS 预处理器呢？**

​    **CSS 预处理器定义了一种新的语言，其基本思想是，用一种专门的编程语言，为 CSS 增加了一些编程的特性，将 CSS 作为目标生成文件，然后开发者就只要使用这种语言进行CSS的编码工作。**

​    转化成通俗易懂的话来说就是“**用一种专门的编程语言，进行 Web 页面样式设计，再通过编译器转化为正常的 CSS 文件，以供项目使用**”。

#### 为什么要使用CSS预处理器？

   作为前端开发人员，大家都知道，Js中可以自定义变量，而CSS仅仅是一个标记语言，不是编程语言，因此不可以自定义变量，不可以引用等等。

​    **CSS有具体以下几个缺点：**

- **语法不够强大，比如无法嵌套书写，导致模块化开发中需要书写很多重复的选择器；**
- **没有变量和合理的样式复用机制，使得逻辑上相关的属性值必须以字面量的形式重复输出，导致难以维护。**

​    这就导致了我们在工作中无端增加了许多工作量。而使用CSS预处理器，**提供 CSS 缺失的样式层复用机制、减少冗余代码，提高样式代码的可维护性。**大大提高了我们的开发效率。

​    但是，CSS预处理器也不是万金油，CSS的好处在于简便、随时随地被使用和调试。预编译CSS步骤的加入，让我们开发工作流中多了一个环节，调试也变得更麻烦了。更大的问题在于，预编译很容易造成后代选择器的滥用。

​    所以我们在实际项目中衡量预编译方案时，还是得想想，比起带来的额外维护开销，CSS预处理器有没有解决更大的麻烦。

#### Sass和Less的比较

**不同之处**

**1、Less环境较Sass简单**

Sass的安装需要安装Ruby环境，Less基于JavaScript，是需要引入Less.js来处理代码输出css到浏览器，也可以在开发环节使用Less，然后编译成css文件，直接放在项目中，有less.app、SimpleLess、CodeKit.app这样的工具，也有在线编辑地址。
**2、Less使用较Sass简单**

LESS 并没有裁剪 CSS 原有的特性，而是在现有 CSS 语法的基础上，为 CSS 加入程序式语言的特性。只要你了解 CSS 基础就可以很容易上手。
**3、从功能出发，Sass较Less略强大一些**

①sass有变量和作用域。
\- $variable，like php；
\- #｛$variable｝like ruby；
\- 变量有全局和局部之分，并且有优先级。
②sass有函数的概念；
\- @function和@return以及函数参数（还有不定参）可以让你像js开发那样封装你想要的逻辑。
-@mixin类似function但缺少像function的编程逻辑，更多的是提高css代码段的复用性和模块化，这个用的人也是最多的。
-ruby提供了非常丰富的内置原生api。

③进程控制：
-条件：@if @else；
-循环遍历：@for @each @while
-继承：@extend
-引用：@import

④数据结构：
-$list类型=数组；
-$map类型=object；
其余的也有string、number、function等类型

#### 4、Less与Sass处理机制不一样

前者是通过客户端处理的，后者是通过服务端处理，相比较之下前者解析会比后者慢一点

#### 5、关于变量在Less和Sass中的唯一区别就是Less用@，Sass用$。

 **相同之处**

Less和Sass在语法上有些共性，比如下面这些：

1、混入(Mixins)——class中的class；
2、参数混入——可以传递参数的class，就像函数一样；
3、嵌套规则——Class中嵌套class，从而减少重复的代码；
4、运算——CSS中用上数学；
5、颜色功能——可以编辑颜色；
6、名字空间(namespace)——分组样式，从而可以被调用；
7、作用域——局部修改样式；
8、JavaScript 赋值——在CSS中使用JavaScript表达式赋值。

 

### 为什么选择使用Sass而不是Less？

1、Sass在市面上有一些成熟的框架，比如说Compass，而且有很多框架也在使用Sass，比如说Foundation。

2、就国外讨论的热度来说，Sass绝对优于LESS。
3、就学习教程来说，Sass的教程要优于LESS。在国内LESS集中的教程是LESS中文官网，而Sass的中文教程，慢慢在国内也较为普遍。

4、Sass也是成熟的CSS预处理器之一，而且有一个稳定，强大的团队在维护。

5、同时还有Scss对sass语法进行了改良，Sass 3就变成了Scss(sassy css)。与原来的语法兼容，只是用\\{\\}取代了原来的缩进。

6、bootstrap（Web框架）最新推出的版本4，使用的就是Sass。