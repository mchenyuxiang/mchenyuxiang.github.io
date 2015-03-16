---
layout: post
title: JavaScript事件流
category: 技术
tags: JavaScript
keywords: JavaScript,脚本语言
description: JavaScript学习
---
@(Javascript)

## 事件流
1. 事件流：描述的是在页面中接受事件的顺序。
2. 事件冒泡：由最具体的元素接收，然后逐级向上传播至最不具体的元素的节点（文档）。
3. 事件捕获：最不具体的节点先接收时间，而最具体的节点应该是最后接收时间。

## 事件处理
1. HTML事件处理：直接添加到HTML结构中
2. DOM0级事件处理
	把一个函数赋值给一个事件处理程序属性

```
    <div id="div">
        <button id="btn1">按钮</button>
    </div>
    <script>
        var btn1 = document.getElementById("btn1");
        btn1.onclick = function(){alert("hello dom0级事件处理程序")}
    </script>
```
弊端：多个事件，则会被覆盖，只显示最后一个事件。
3. DOM2级事件处理
	addEventListener("事件名","事件处理函数","布尔值");
	true: 事件捕获
	false: 事件冒泡
	removeEventListener();
	
DOM2级事件不覆盖，是依次执行。

```
<body>
    <!--创建对象-->
    <div id="div">
        <button id="btn1">按钮</button>
    </div>
    <script>
        var btn1 = document.getElementById("btn1");
        btn1.addEventListener("click",demo1);
        btn1.addEventListener("click",demo2);
        function demo1(){
            alert("Dom2级事件处理程序1");
        }
        function demo2(){
            alert("Dom2级事件处理程序2");
        }
        btn1.removeEventListener("click",demo2);
    </script>
</body>
```
4. IE事件处理程序
	attachEvent
	detachEvent

```
<body>
    <!--创建对象-->
    <div id="div">
        <button id="btn1">按钮</button>
    </div>
    <script>
        var btn1 = document.getElementById("btn1");
        if(bt1.addEventListener){
            btn1.addEventListener("click",demo);
        }else if(btn1.attachEvent){
            btn1.attachEvent("onclick"),demo);
        }else{
            btn1.onclick = demo();
        }
        function demo(){
            alert("hello");
        }
    </script>
</body>
```

## 事件对象
事件对象event：
type:获取事件类型
target:获取事件目标
stopPropagation():阻止事件冒泡
preventDefault():阻止事件默认行为

```
<body>
    <!--创建对象-->
    <div id="div">
        <button id="btn1">按钮</button>
        <a id="aid" href="http://www.playdba.com">playdba</a>
    </div>
    <script>
        document.getElementById("btn1").addEventListener("click",demo);
        document.getElementById("div").addEventListener("click",showDiv);
        document.getElementById("aid").addEventListener("click",showA);
        function demo(event){
//            alert(event.type);
            alert(event.target);
            event.stopPropagation();//阻止事件冒泡
        }
        function showDive(){
            alert("div");
        }
        function showA(event){
            event.stopPropagation();
            event.preventDefault();//阻止a标签的默认跳转行为
        }
    </script>
</body>
```