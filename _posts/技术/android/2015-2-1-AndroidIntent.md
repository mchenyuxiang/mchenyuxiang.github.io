---
layout: post
title: Android应用核心-Intent
category: 技术
tags: Android
keywords: android,移动开发
description: 安卓Intent学习
---

## Android应用核心-Intent
@(android)

### Intent对象介绍以及IntentFilter概念
Intent用来指定需要启动的目标组件。IntentFilter用来描述应用的地址。

### 显式Intent和隐式Intent
由指定包命和类名来启动Intent，称为显式Intent；由在AndridManifest.xml中配置action，然后通过调用action来启动Intent，称为隐式Intent。

今天学习主要以实战为主，直接上[代码](https://github.com/mchenyuxiang/studyAndroid/tree/master/L008Intents)