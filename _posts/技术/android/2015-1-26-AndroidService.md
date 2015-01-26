---
layout: post
title: Android四大组件学习-service
category: 技术
tags: Android
keywords: android,移动开发
description: 安卓service学习
---

## Android四大组件学习-service
@(android)

Service是后台运行的，是不可见的程序，对用户来说是透明的。

### Service两种状态，onCreate()和onDestroy()
1. 创建service
- 创建类EchoService，继承自service。
- 在androidManifest.xml中注册service。```
<service android:name="EchoService"></service>
```
- 我直接在MainActivity中来启动服务，我们需要在MainActivity中实现OnClickListener接口中的onClick方法。定义不同的事件。
- 我们在EchoService中重写Service的两个方法，Service生命周期只有两种状态，onCreate和onDestroy。我们重写只是简单的打印出状态信息。创建服务后，关闭activity服务进程也同样存在，只有在关闭服务后，服务进程才结束。

### 绑定服务
- 操作系统中一个service只有一个实例，在service已经oncreate的时候，bind service时，不会重复创建service。
- 如果同时启动且绑定service，如果想要destroy，必须同时执行stop和unbind，service才能被关闭掉。
-  通过start service启动服务时，把当前的activity销毁时，你的服务不会被停掉；如果是用bind service启动服务时，当activity销毁时，服务也将被停掉。
-   如果需要与服务进行通信时，必须同某个服务进行绑定。
