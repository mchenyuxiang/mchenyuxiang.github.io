---
layout: post
title: JavaScript内置对象
category: 技术
tags: JavaScript
keywords: JavaScript,脚本语言
description: JavaScript学习
---
@(Javascript)

## 什么是对象
在JS中所有事物都是对象：字符串、数值、数组、函数……。
每个对象带有属性和方法。
JS允许自定义对象

```
<body>
    <!--创建对象-->
    <button onclick="demo()">按钮</button>
    <script>
        people = new Object();
        people.name = "xiaochen";
        people.age = "26";
        document.write("name:"+people.name+",age:"+people.age);
    </script>
</body>
```

```
    <script>

        people = {name:"xiaochen",age:"26"};      document.write("name:"+people.name+",age:"+people.age);
    </script>
```

```
<body>
    <!--创建对象-->
    <button onclick="demo()">按钮</button>
    <script>
        function people(name,age){
            this.name=name;
            this.age=age;
        }
        son = new people("xiaochen","26");
        document.write("name:"+son.name+",age:"+son.age)
    </script>
</body>
```


## String字符串对象
用于处理已有的字符串
字符串可以使用双引号或单引号

查找字符串：indexOf();有则返回字符串开始位置，否则返回-1。注意大小写敏感。
```
    <script>
        var str = "Hello World";
        document.write(str.indexOf("World"));
    </script>
```

内容匹配：match(),如果字符串存在则打印出字符串，否则返回null。注意大小写敏感。
```
    <script>
        var str = "Hello World";
        document.write(str.match("World"));
    </script>
```

替换内容：replace()
```
    <script>
        var str = "Hello World";
        document.write(str.replace("World","xiaochen"));
    </script>
```

字符串大小写转换：toUpperCase() / toLowerCase()
```
    <script>
        var str = "Hello World";
        document.write(str.toUpperCase());
    </script>
```

字符串转为数组：strong>split()
```
<script>
    var str1 = "Hello,xiao,chen";
    var s = str1.split(",");
    document.write(s[1]);
</script>
```

## Date日期对象
用于处理日期和时间

获取当前日期：
```
    <script>
        var date = new Date();
        document.write(date);
    </script>
```

常用方法：
getFullYear():获取年份
···
    <script>
        var date = new Date();
        document.write(date.getFullYear());
    </script>
···
getTime():获取毫秒，时间戳到现在的毫秒数
```
    <script>
        var date = new Date();
        document.write(date.getTime());
    </script>
```
setFullYear():设置具体的日期
```
    <script>
        var date = new Date();
        date.setFullYear(2010,1,1);
        document.write(date);
    </script>
```
getDay():获取星期


时钟实例：实现每一秒自动刷新一次网页，并显示时间
```
<body onload="startTime()">
    <!--创建对象-->
    <script>
        function startTime(){
            var today = new Date();
            var h = today.getHours();
            var m = today.getMinutes();
            var s = today.getSeconds();
            m = checkTime(m);
            s = checkTime(s);
            document.getElementById("timetxt").innerHTML = h+":"+m+":"+s;
            t = setTimeout(function(){
                startTime();
            },1000);
        }

        function checkTime(i){
            if(i<10){
                i = "0" + i;
            }
            return i;
        }
    </script>
    <div id="timetxt"></div>
</body>
```

## Array数组对象
使用单独的变量名来存储一系列的值

元素合并
```
    <script>
        var a = ["hello","world"];
        var b = ["xiao","chen"];
        var c = a.concat(b);
        document.write(c);
    </script>
```

排序
```
    <script>
        var a = ["a","c","e","k","r","z","o"]
        document.write(a.sort());
    </script>
```

## Math对象
执行常用算数任务

round():四舍五入
random():返回0—1之间的随机数
max():返回最高值
min():返回最低值
abs():返回绝对值