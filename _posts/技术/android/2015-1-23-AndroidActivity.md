---
layout: post
title: Android四大组件学习-activity
category: 技术
tags: Android
keywords: android,移动开发
description: 安卓activity学习
---

## Android四大组件学习-activity
@(android)

### Android四大基本组件
- Activity
- Service
- Broadcast Receiver
- Content Provider

### Activity 概念
- 是一个与用户进行交互的基本程序单元

### Activity三种状态
- 运行
- 停止
- 暂停

### Activity生命周期的七个方法
![安卓生命周期](/public/upload/android/1421802290497.png)

### Activity中的数据传递

创建Intent，并配置参数，说明数据是由哪个activity传给哪个activity。
有两种传递方法：
- 如果数据比较简单，属于常见的数据类型，可以用如下列子：
```
		Intent i = new Intent(MainActivity.this, Aty1.class);
		i.putExtra("txt", "Hello Aty1");
```

在i.putExtra(所传数据的名称，所传数据的值)。这样在MainActivity中系统Intent则可以将数据传递到Aty1中，现在我们来看如何在Aty1中接受数据。Aty1接受代码如下：
```
		tvOut = (TextView) findViewById(R.id.tvOut);
		tvOut.setText(getIntent().getStringExtra("txt"));
```
Aty1中用TextView来展示数据，通过在MaiActivity中对数据的命名来得到相对应的数据。

- 如果数据比较大时，可以用创建Bundle来传输数据。MainActivity中代码如下：
```
		Bundle data = new Bundle();
		data.putString("txt", "Hello Aty1");
		i.putExtras(data);
```
Aty1中接受代码如下：
```
		Bundle data = getIntent().getExtras();
		String txt = data.getString("txt");
		tvOut.setText(txt);
```


### 如何得到Activity中的返回结果值
我们是将Aty1中的值返回给MainActivity，需要在MainActivity中创建Intent，然后重写onActivityResult方法。
先在Aty1中创建返回值
```
		Intent i = new Intent();
		i.putExtra("result", "Hello MainActivity");
		setResult(0, i);
```
这里创建一个新的Intent，讲值“Hello MainActivity”命名为result，setResult中的0代表返回结果的代码。将i返回到resultCode为0的结果中。

MainActivity中：
```
startActivityForResult(i, 0);
```
在MainActivity中不用平常的startActivity来得到返回值，而用startActivityForResult来启动activity，i为定义的Intent，0为下面重写onActivityResult中的resultCode。

```
@Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    	
    	String result = data.getStringExtra("result");
    	tvOut.setText(result);
    	super.onActivityResult(requestCode, resultCode, data);
    }
```
代码中，result为在Aty1中定义的返回值。用TextView来展示结果。