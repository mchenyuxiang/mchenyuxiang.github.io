---
layout: post
title: JavaScript函数
category: 技术
tags: JavaScript
keywords: JavaScript,脚本语言
description: JavaScript学习
---

## 定义函数
1. 定义函数：
```JavaScript
		function 函数名(){
			函数体;（代码块）
		}
```

2. 注意：function必须小写，因为Javascript大小写敏感。函数通常以小写命名。

## 调用函数
1. 函数调用：
	函数在定义好后，不能自动执行，需要调用
2. 调用方式：
	- 在``` <script> ```标签内调用
	``` JavaScript
	    <script>
        function demo(){
            var a = 10;
            var b = 20;
            var sum = a + b;
            alert(sum)
        }
        demo(); //调用函数
	    </script>
	```
	
	- 在HTML文件内调用
	```JavaScript
	    <script>
        function demo(){
            var a = 10;
            var b = 20;
            var sum = a + b;
            alert(sum)
        }
    </script>
    <form>
        <input type="button" value="按钮" onclick="demo()" >
    </form>
	```
	
## 带参数的函数
1. 函数参数：
在函数的调用中，也可以传递值，这些值被称为参数。
例：demo(arg1,arg2)；
2. 参数的个数可以为任意多，每个参数通过“,"隔开。
3. 参数需要按照设定的顺序进行传递。

