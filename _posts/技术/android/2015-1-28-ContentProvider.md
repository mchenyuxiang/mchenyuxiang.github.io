---
layout: post
title: Android四大组件学习-ContentProvider
category: 技术
tags: Android
keywords: android,移动开发
description: 安卓service学习
---
## Android四大组件学习-ContentProvider
@(android)

### 概述
ContentProvider是android提供用于在应用程序中相互共享数据。必须指定一个uri。这里主要说明如何使用ContentProvider读取应用程序的数据，后期博客将对其进行更详细的讲解。

### 用法（以读取联系人数据为例子）
下面只是一个简单的掩饰读取联系人名称的例子。
得到联系人的数据，可以直接调用getContentResolver()的query查询方法来实现，```getContentResolver().query(uri, projection, selection, selectionArgs, sortOrder)```。在uri中我们需要填写电话本的查询uri，ContactsContract.Contacts.CONTENT_URI，其余的暂时都填写null。我们把得到的数据都放入一个游标中，由游标来循环读取每一行的电话本记录。
另外，如果需要读取通讯录，需要在AndroidManifest.xml中来进行权限的设置，设置```"android.permission.READ_CONTACTS" ```。这样就能读取电话中的记录信息了。
部分代码如下：
```java

Cursor c = getContentResolver().query(ContactsContract.Contacts.CONTENT_URI, null, null, null, null);
        
while(c.moveToNext()){
   System.out.println(">>>>>>" + c.getString(c.getColumnIndex(ContactsContract.Contacts.DISPLAY_NAME)));
        }
```

此节代码为查看：[L005ReadContact](https://github.com/mchenyuxiang/studyAndroid/tree/master/L005ReadContact)