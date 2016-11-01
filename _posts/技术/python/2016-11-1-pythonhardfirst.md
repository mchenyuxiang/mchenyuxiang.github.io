---
layout: post
title: 笨办法学python第一天
category: 技术
tags: Python
keywords: python,脚本语言
description: python学习
---
@(python)

# 笨办法学python第一天

## 运行python
```python
print "Hello World!"
print "Hello Again"
print "I like typing this."
print "This is fun."
print 'Yay! Printing.'
print "I'd much rather you 'not'."
print 'I "said" do not touch this.'
```

存成文件 ex1.py
运行 `python ex1.py`

可以看到

```
Hello World
Hello Again
I like typing this.
This is fun.
Yay! Printing.
I'd much rather you 'not'.
I "said" do not touch this.
```

在python中#为注释

## 数字和数学计算

+ `+` plus 加号
+ `-` minus 减号
+ `/` slash 斜杠，除
+ `*` asterisk 星号，乘
+ `%` percent 百分号，取余
+ `<` less-than 小于号
+ `>` greater-than 大于号
+ `<=` less-than-equal 小于等于号
+ `>= `greater-than-equal 大于等于号


编写文件 `ext3.py`

```python
print "I will now count my chickens:"

print "Hens", 25+30/6
print "Roosters", 100-25*3%4

print "Now I will count the eggs:"

print 3+2+2-5+4%2-1/4+6

print "Is it true that 3+2<5-7?"

print 3+2<5-7

print "What is 3+2?",3+2
print "What is 5-7?",5-7

print "Oh,that's why it's False."

print "How about some more."

print "Is it greater?",5>-2
print "Is it greater or equal?",5>=-2
print "Is it less or equal?",5<=-2
```

运行结果

```
I will now count my chickens:
Hens 30
Roosters 97
Now I will count the eggs:
8
Is it true that 3+2<5-7?
False
What is 3+2? 5
What is 5-7? -2
Oh,that's why it's False.
How about some more.
Is it greater? True
Is it greater or equal? True
Is it less or equal? False
```

从结果可以看出如下几点规律
1. 运算符进行计算时有优先级顺序,先乘除,后加减,最后再是比较运算符.是从左往右进行计算
2. 进行相除时,如果除数和被除数都是整数,则结果也是整数.
3. 比较运算符的出来的结果是True和False,即是布尔型的
4. 如果结果有小数,需要将除数或者被除数转成浮点数,最容易的办法是加0.即20.0为一个浮点数.



## 变量和命名
python中变量声明后可以直接使用,不需要对变量提前定义类型.使用变量时必须提前声明.在python中,可以用`.`来进行字符串的拼接以及变量的打印.

``` python
# -- coding:utf-8 --
my_name = 'Zed A. Shaw'
my_age = 35
my_height = 74
my_weight = 180
my_eyes = 'Blue'
my_teeth = 'White'
my_hair = 'Brown'

print "Let's talk about %s." % my_name
print "He's %d inches tall." % my_height
print "He's %d pounds heavy." % my_weight
print "Actually that's not too heavy."
print "He's got %s eyes and %s hair."%(my_eyes,my_hair)
print "His teeth are usually %s depending on the coffee."% my_teeth

print "If I add %d,%d, and %d I get %d."%(my_age,my_height,my_weight,my_age+my_height+my_weight)
```

格式化打印变量,类似c语言,后面用`%`显示变量,不要打`,`.如果是utf-8的编码的情况,需要在文件的最开始添加代码` # --coding: utf-8 --`.

字符串可以包含格式化字符 `%s`，这个你之前也见过的。你只要将格式化的变量放到字符串中，再紧跟着一个百分号 `%` (percent)，再紧跟着变量名即可。唯一要注意的地方，是如果你想要在字符串中通过格式化字符放入多个变量的时候，你需要将变量放到 `( )` 圆括号(parenthesis)中，而且变量之间用 `,` 逗号(comma)隔开。就像你逛商店说“我要买牛奶、面包、鸡蛋、八宝粥”一样，只不过程序员说的是”(milk, eggs, bread, soup)”。

python中如果想多行输出的话,方式如下

```python
print """
There's something going on here.
With the three double-qoutes.
We'll be able to type as much as we like.
Even 4 lines if we want, or 5,or 6.
"""
```

## 输入raw_input()

一般软件做的事情主要就是下面几条:
1. 接受人的输入.
2. 改变输入.
3. 打印出改变了的输入.


```python
# --coding:utf-8 --
print "How old are you?",
age = raw_input()
print "How tall are you?",
height = raw_input()
print "How much do you weight?",
weight = raw_input()

print "So,you're %r old,%r tall and %r heave."%(age,height,weight)
```

注意到我在每行 `print` 后面加了个逗号(comma) `,` 了吧？这样的话 `print`就不会输出新行符而结束这一行跑到下一行去了。

`raw_input()`函数是使得用户可以从键盘进行输入.


当你键入 `raw_input() `的时候，你需要键入` ( `和 `)` 也就是“括号(parenthesis)”。这和你格式化输出两个以上变量时的情况有点类似，比如说` "%s %s" % (x, y) `里边就有括号。对于` raw_input `而言，你还可以让它显示出一个提示，从而告诉别人应该输入什么东西。

```python
# -- coding:utf-8 --
age = raw_input("How old are you?")
height = raw_input("How tall are you?")
weight = raw_input("How much do you weight?")

print "So, you're %r old,%r tall and %r heavy."%(age,height,weight)
```

## import功能
从现在开始我们将把这些我们导入(import)进来的功能称作模组。你将看到类似这样的说法：“你需要把 sys 模组 `import `进来。”也有人将它们称作“`库(libraries)`”，不过我们还是叫它们`模组`吧。

```python
# -- coding:utf-8 --
from sys import argv

script,first,second,third = argv

print "The script is called:",script
print "Your first variable is:",first
print "Your second variable is:",second
print "Your third variable is:",third
```

`argv` 是所谓的“参数变量(argument variable)”，是一个非常标准的编程术语。在其他的编程语言里你也可以看到它。这个变量包含了你传递给 Python 的参数。

## 读取文件
读取文件需要先用`open`命令来打开文件,然后用`.read`来进行文件的读取


```python
#--coding:utf-8--
from sys import argv

script, filename = argv

txt = open(filename)

print "Here's your file %r:"%filename
print txt.read()

print "Type the filename again:"
file_again = raw_input("> ")

txt_again = open(file_again)

print txt_again.read()
```



操作文件命令
+ close – 关闭文件。跟你编辑器的 文件->保存.. 一个意思。
+ read – 读取文件内容。你可以把结果赋给一个变量。
+ readline – 读取文本文件中的一行。
+ truncate – 清空文件，请小心使用该命令。
+ write(stuff) – 将stuff写入文件。

```python
from sys import argv

script, filename = argv

print "We're going to erase %r." % filename
print "If you don't want that, hit CTRL-C (^C)."
print "If you do want that, hit RETURN."

raw_input("?")

print "Opening the file..."
target = open(filename, 'w')

print "Truncating the file.  Goodbye!"
target.truncate()

print "Now I'm going to ask you for three lines."

line1 = raw_input("line 1: ")
line2 = raw_input("line 2: ")
line3 = raw_input("line 3: ")

print "I'm going to write these to the file."

target.write(line1)
target.write("\n")
target.write(line2)
target.write("\n")
target.write(line3)
target.write("\n")

print "And finally, we close it."
target.close()
```

## 文件拷贝

```python
from sys import argv
from os.path import exists

script, from_file, to_file = argv

print "Copying from %s to %s" % (from_file, to_file)

# we could do these two on one line too, how?
input = open(from_file)
indata = input.read()

print "The input file is %d bytes long" % len(indata)

print "Does the output file exist? %r" % exists(to_file)
print "Ready, hit RETURN to continue, CTRL-C to abort."
raw_input()

output = open(to_file, 'w')
output.write(indata)

print "Alright, all done."

output.close()
input.close()
```

在此单中,`len()`是计算字符串的长度.`exists()`判断是否存在文件,如果存在则返回True,否则返回False


## 函数

```python
# this one is like your scripts with argv
def print_two(*args):
    arg1, arg2 = args
    print "arg1: %r, arg2: %r" % (arg1, arg2)

# ok, that *args is actually pointless, we can just do this
def print_two_again(arg1, arg2):
    print "arg1: %r, arg2: %r" % (arg1, arg2)

# this just takes one argument
def print_one(arg1):
    print "arg1: %r" % arg1

# this one takes no arguments
def print_none():
    print "I got nothin'."


print_two("Zed","Shaw")
print_two_again("Zed","Shaw")
print_one("First!")
print_none()
```

函数用def定义,后面接冒号.全部用缩进的方式来进行函数定义.
