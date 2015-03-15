---
layout: post
title: JavaScript异常处理和事件处理
category: 技术
tags: JavaScript
keywords: JavaScript,脚本语言
description: JavaScript学习
---

## 异常捕获
1、异常：导致程序停止运行
2、 抛出：产生一个错误信息
3、 异常捕获：
try{
	发生异常的代码块;
}catch(err){
	错误信息处理;
}

4、Throw语句：
	通过throw语句创建一个自定义错误


```
    <script>
        function demo(){
            try{
                alert(str);
            }catch (err){
                alert(err);
            }
        }
        demo();
    </script>
```

## 事件
什么是事件：
事件是可以被JavaScript侦测到的行为
