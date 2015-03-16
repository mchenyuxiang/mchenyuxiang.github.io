---
layout: post
title: JavaScript DOM对象控制HTML元素详解
category: 技术
tags: JavaScript
keywords: JavaScript,脚本语言
description: JavaScript学习
---
@(Javascript)

## 方法
getElementsByName() -- 获取name
getElementsByTagName() -- 获取元素
getAttribute() -- 获取元素属性
setAttribute() -- 设置元素属性
childNodes() -- 访问子节点
parentNode() -- 访问父节点
createElement() -- 创建元素节点
createTextNode -- 创建文本节点
insertBefore() -- 插入节点
removeChild() -- 删除节点
offsetHeight -- 网页尺寸（不包含滚动条）
scrollHeight -- 网页尺寸（包含滚动条）

```
<body>
    <p name="pn">hello</p>
    <p name="pn">hello</p>
    <p name="pn">hello</p>
    <a id="aid" title="得到a标签的属性">hello</a>
    <a id="aid2">aid2</a>
    <ul>
        <l1>1</l1>
        <l1>2</l1>
        <l1>3</l1>
    </ul>
    <div id="div">
        <p id="pid">div的p元素</p>
    </div>
    <script>
        function getName(){
//            var count = document.getElementsByName("pn"); // 多个是通过集合来操作
//            var count = document.getElementsByTagName("p"); // 多个是通过集合来操作
            alert(count.length);
            var p=count[0];
            p.innerHTML = "world";
        }
//        getName();
        function getAttr(){
            var anode = document.getElementById("aid");
            var attr = anode.getAttribute("title");
            alert(attr);
        }
//        getAttr();
        function setAttr(){
            var anode = document.getElementById("aid2");
            anode.setAttribute("title","动态设置aid2的title属性");
            var attr = anode.getAttribute("title");
            alert(attr);
        }
//        setAttr();
        function getChildNode(){
            var childnode = document.getElementsByTagName("ul")[0].childNodes;//包含空白项
            alert(childnode.length);
        }
//        getChildNode();
        function getParentNode(){
            var div = document.getElementById("pid");
            alert(div.parentNode.nodeName);
        }
//        getParentNode();
        function createNode(){
            var body = document.body;
            var input = document.createElement("input");
            input.type = "button";
            input.value = "按钮";
            body.appendChild(input);
        }
//        createNode();
        function addNode(){
            var div = document.getElementById("div");
            var node = document.getElementById("pid");
            var newnode = document.createElement("p");
            newnode.innerHTML = "动态添加第一个p元素";
            div.insertBefore(newnode,node);
        }
//        addNode();
        function removeNode(){
            var div = document.getElementById("div");
            var p = div.removeChild(div.childNodes[1]);
        }
//        removeNode();
        function getSize(){
            var width = document.documentElement.offsetWidth || document.body.offsetWidth;
            var height = document.documentElement.offsetHeight || document.body.offsetHeight;
            alert(width + "," + height);
        }
        getSize();
    </script>
</body>
```
