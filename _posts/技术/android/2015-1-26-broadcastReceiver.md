---
layout: post
title: Android四大组件学习-broadcast receiver
category: 技术
tags: Android
keywords: android,移动开发
description: 安卓service学习
---

## Android四大组件学习-broadcast receiver
@(android)

### 概述
android提供的用于在组件与组件进行通信的机制，可以跨应用程序进行通信。操作系统广播能够侦听到，如：低电量，收到短信，操作启动完毕等一些广播应用。通信的数据不大，传递频率不高。broadcast运行效率比较低，通信很频繁的程序不易用此组件。

### 声明
- 首先需要创建一个类MyBC，继承自BroadcastReceiver，建立好后会自动创建一个onReceive的方法，这个方法是在得到广播消息时执行。
- 类创建完后需要在AndroidManifest.xml中注册receiver，一种是直接在application里面添加，另外一种是直接在xml代码中添加```<receiver android:name="MyBC"></receiver> ``` 
- 上面两步建立好后，我们为了实验，首先在main.xml中添加了按钮来实现方法，用点击按钮打印信息的方式来实现此方法。按钮建立好后，在MainActivity中调用sendBroadcast来执行广播方法。关键代码如下：
```
btnSendBroadcast.setOnClickListener(new View.OnClickListener() {
			
	@Override
	public void onClick(View v) {
				
	Intent i = new Intent(MainActivity.this,MyBC.class);
	i.putExtra("txt", "hello eoe");
				
	sendBroadcast(i);
	}
});
```
- 在MyBC中就可以得到hello eoe的消息。
```
public void onReceive(Context context, Intent intent) {
		System.out.println("onReceive,data="+intent.getStringExtra("txt"));
}
```
用以上方法可以得到广播的消息，但是，有些时候我们并不想得到某些消息，这样我们就必须将某些广播方法进行注册和注销。下面具体操作说明：
- 需要添加注册广播和取消注册的事件。如果用注册的方式，将不需要再AndroManifest.xml文件将receiver进行注册。
- 注册调用的是registerReceiver方法。recevier我们用刚才的MyBC类新建一个mybc对象，另外一个参数使用action来执行动作。action的命名规则为：包命.intent.action.名称。
- 取消调用的是unregisterReceiver方法。取消则直接添加MyBC类的对象mybc即可。
- 发送广播。定义Intent为```Intent i = new Intent(MyBC.ACTION); ```。

实现以上程序后，可以参考[studyandroid当中的l004UsingBC](https://github.com/mchenyuxiang/studyAndroid/tree/master/L004UsingBC) 来实践。