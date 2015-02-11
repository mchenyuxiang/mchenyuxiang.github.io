---
layout: post
title: Android用户布局
category: 技术
tags: Android
keywords: android,移动开发
description: 安卓Intent学习
---

##Android用户布局
@(android)

###布局说明

1、FrameLayout
没有位置的概念，所添加的子元素都是相对于FrameLayout的左上角对齐。如果有需要不调整位置的子元素可以用FrameLayout。运行速度快。

2、LinearLayout
线性布局，可以水平也可以垂直。

3、RelativeLayout
相对布局，子元素可以相对于RelativeLayout调整位置也可以相对于其他子元素来调整位置。

4、TableLayout
是水平方向的LinearLayout和垂直方向的LinearLayout的混合。

5、AbsouluteLayout
绝对布局，子元素可以相对于布局调整布局（RelativeLayout已经包括），已弃用


今天的代码是一个在src文件中添加布局按钮，然后实现点击一个移除一个的效果。[代码连接](https://github.com/mchenyuxiang/studyAndroid/tree/master/L009Layout)