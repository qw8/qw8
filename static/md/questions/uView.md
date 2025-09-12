---
title: uView
date: 2022-05-21 23:40:25
categories: 
- 前端问题
tags:
- vue
---

### 空白页可以这样写

```
<u-empty v-else icon="/static/img/none@3x.png" text="暂无企业文件"></u-empty>

// methods同级
options: \\{
        styleIsolation: "shared",
    \\},

/deep/.u-empty \\{
    height: 85vh;
    .u-empty__text \\{
        margin-top: 32rpx !important;
    \\}
\\}
```



### Tabs标签栏实现对齐（实现不了）

```
.first \\{
    width: 100\\%;
    height: 108rpx;
    // 外部设置边距保证了滑动时也对齐
    padding: 0 32rpx;
    box-sizing: border-box;

    /deep/.u-tabs \\{
      max-width: 606rpx;
      // 第一个标签去掉左边距实现刚进去对齐，但是会导致底部蓝色滑块不居中
      .u-tabs__wrapper__nav__item-0 \\{
        padding-left: 0;
      \\}
    \\}
  \\}
```

