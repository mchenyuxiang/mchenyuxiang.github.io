---
layout: post
title: JavaScriptDom对象
category: 技术
tags: JavaScript
keywords: JavaScript,脚本语言
description: JavaScript学习
---

## DOM简介
HTML DOM：
 当网页被加载时，浏览器会创建页面的文档对象模型（Document Object Model)

DOM操作HTML:
- JavaScript 能够改变页面中的所有HTML元素
- JavaScript 能够改变页面中的所有HTML属性
- JavaScript 能够改变页面中的所有CSS样式
- JavaScript 能够对页面中的所有事件做出反应

## DOM操作HTML
1. 改变HTML输出流：
	```
	<script>
        document.write("hello");
    </script>
	```
	
	注意：绝对不要在文档加载完成之后使用document.write()。这会覆盖该文档
	```
	<body>
    <p>Hello</p>
    <button onclick="demo()">按钮</button>
    <script>
        function demo(){
            document.write("world");
        }
    </script>
</body>
	```
	 例子中，点击按钮将会讲hello清空。
2. 寻找元素：
	通过id找到HTML元素
	通过标签名找到HTML元素
3. 改变HTML内容：
	使用属性：innerHTML

通过id:
```JavaScript
<body>
    <p id="pid">Hello</p>
    <button onclick="demo()">按钮</button>
    <script>
        function demo(){
            var nv = document.getElementById("pid");
            nv.innerHTML = "world";
        }
    </script>
</body>
```

通过标签名：
```
<body>
    <p id="pid">Hello</p>
    <button onclick="demo()">按钮</button>
    <script>
        function demo(){
            var nv = document.getElementById("pid");
            document.getElementsByTagName("p") //如果有多个p元素，则会找到相同元素的第一个
        }
    </script>
</body>
```

4. 改变HTML属性：
	使用属性：attribute
	
	``` JavaScript
	
	<body>
    <a id="aid" href="http://www.baidu.com">hello</a>
    <button onclick="demo()">按钮</button>
    <script>
        function demo(){
            document.getElementById("aid").href="http://www.playdba.com"
        }
    </script>
</body>

	```
	上面实现功能，没点击按钮点击hello是跳转到百度。点击按钮后，再点击hello则跳转到[http://www.playdba.com](http://www.playdba.com)

## DOM操作CSS
通过DOM对象改变CSS
语法：document.getElementById(id).style.property=new style

```
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <link rel="stylesheet" type="text/css" href="style.css">
</head>
<body>
    <div id="div" class="div">
        Hello
    </div>
    <button onclick="demo()">按钮</button>
    <script>
        function demo(){
            document.getElementById("div").style.background = "red";
        }
    </script>
</body>
```

## DOM EventListener
1. DOM EventListener:
	方法：addEventListener();
		removeEventListener();
2. addEventListener():
	方法用于向指定元素添加事件句柄
3. removeEventListener():
	移除方法添加的事件句柄