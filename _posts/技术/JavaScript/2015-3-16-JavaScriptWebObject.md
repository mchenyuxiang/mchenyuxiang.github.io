---
layout: post
title: JavaScript浏览器对象
category: 技术
tags: JavaScript
keywords: JavaScript,脚本语言
description: JavaScript学习
---
@(Javascript)

## Window对象
1. window对象：
	window对象是BOM的核心，window对象指当前的浏览器窗口
	所有JavaScript全局对象、函数以及变量均自动成为window对象的成员
	全局变量是window对象的属性
	全局函数是window对象的方法
	甚至HTML DOM的document也是window对象的属性之一
2. window尺寸：
	window.innerHeight - 浏览器窗口的内部高度
	window.innerWidth - 浏览器窗口的内部宽度

## History对象
history.back() - 与浏览器后退按钮相同
history.foward() - 与浏览器向前按钮相同
history.go() - 进入历史的某个页面