---
layout: post
title: 笨办法学python第二天
category: 技术
tags: Python
keywords: python,脚本语言
description: python学习
---
@(python)

#  笨办法学python第二天
昨天学习了一些基本的python的语法以及用法，学到了函数的建立以及调用，文件的读取和写入。

##  复习函数

```python
#--coding:utf-8--
def break_words(stuff):
    """This function will break up words for us."""
    words = stuff.split(' ')
    return words

def sort_words(words):
    """Sorts the words."""
    return sorted(words)

def print_first_word(words):
    """Prints the first word after popping it off."""
    word = words.pop(0)
    print word

def print_last_word(words):
    """Prints the last word after popping it off."""
    word = words.pop(-1)
    print word

def sort_sentence(sentence):
    """Takes in a full sentence and returns the sorted words."""
    words = break_words(sentence)
    return sort_words(words)

def print_first_and_last(sentence):
    """Prints the first and last words of the sentence."""
    words = break_words(sentence)
    print_first_word(words)
    print_last_word(words)

def print_first_and_last_sorted(sentence):
    """Sorts the words then prints the first and last one."""
    words = sort_sentence(sentence)
    print_first_word(words)
    print_last_word(words)
```

使用时，需要用import先导入文件，然后再直接使用函数。`split`函数是将字符串按照指定分隔符进行分割。`pop`是删除字符串

## 逻辑


+ `and` 与
+ `or` 或
+ `not` 非
+ `!=` (not equal) 不等于
+ `==` (equal) 等于
+ `>=` (greater-than-equal) 大于等于
+ `<=` (less-than-equal) 小于等于
+ `True` 真
+ `False` 假


## IF与ELSE

python分支语句为`if...elif..else`结构

```python
#--coding:utf-8--
people = 30
cars = 40
trucks = 15

if cars > people:
    print "We should take the cars."
elif cars < people:
    print "We should not take the cars."
else:
    print "We can't decide."

if trucks > cars:
    print "That's too many trucks."
elif trucks < cars:
    print "Maybe we could take the trucks."
else:
    print "We still can't decide."

if people > trucks:
    print "Alright, let's just take the trucks."
else:
    print "Fine,let's stay home then"
```


## 循环和列表

`for`循环定义循环时应该以`:`作为结尾。`range`关键字不包括结尾的数字

```python
the_count = [1, 2, 3, 4, 5]
fruits = ['apples', 'oranges', 'pears', 'apricots']
change = [1, 'pennies', 2, 'dimes', 3, 'quarters']

# this first kind of for-loop goes through a list
for number in the_count:
    print "This is count %d" % number

# same as above
for fruit in fruits:
    print "A fruit of type: %s" % fruit

# also we can go through mixed lists too
# notice we have to use %r since we don't know what's in it
for i in change:
    print "I got %r" % i

# we can also build lists, first start with an empty one
elements = []

# then use the range function to do 0 to 5 counts
for i in range(0, 6):
    print "Adding %d to the list." % i
    # append is a function that lists understand
    elements.append(i)

# now we can print them out too
for i in elements:
    print "Element was: %d" % i
```

while循环每次做完一次将判断是否退出条件，如果不满足将执行下一次循环。

```python
i = 0
numbers = []

while i < 6:
    print "At the top i is %d" % i
    numbers.append(i)

    i = i + 1
    print "Numbers now: ", numbers
    print "At the bottom i is %d" % i

print "The numbers: "

for num in numbers:
    print num
```

**IF语句规则**

1. 每一个“if 语句”必须包含一个 else.
2. 如果这个else永远都不应该被执行到，因为它本身没有任何意义，那你必须在else语句后面使用一个叫做die的函数，让它打印出错误信息,这和上一节的习题类似，这样你可以找到很多的错误。
3. “if 语句”的嵌套不要超过 2 层，最好尽量保持只有 1 层。
4. 将“if 语句”当做段落来对待，其中的每一个if-elif-else 组合就跟一个段落的句子一样。在这种组合的最前面和最后面留一个空行以作区分。
5. 你的布尔测试应该很简单，如果它们很复杂的话，你需要将它们的运算事先放到一个 变量里，并且为变量取一个好名字。

**完成一个软件的最好方式是把它们拆解为像下面这样的小块**：

1. 在纸上写下你完成这个软件所需要做的所有任务。这就是你的待办事项列表。
2. 先找到你列表中最容易的事情。
3. 在你的源代码中增加注释，作为你完成这项任务的指南。
4. 在这些注释下面，开始编码。
5. 然后立即运行你的代码，看它是否正常工作。
6. 循环的进行代码编写，测试运行，以及代码修正，直到代码正常运行。
7. 在你的列表中划掉刚完成的任务，然后再挑选下一个最容易完成的任务，重复进行以上步骤。


## 模块, 类和对象

模块就像字典。使用时我可以导入模块，要用什么时通过在模块中定义的标识符直接使用就好。

类的作用是组织一系列的函数和数据并将它们放在一个容器里，这样你可以通过`.`操作符访问到它们。

使用类而不是仅有模块的原因：你可以使用一个类，还可以用它来创建更多个对象，而他们之间也不会互相冲突。当你导入一个模块时，你的整个项目也就只有一个这个模块。

**类和对象与模块是有区别的**：
+ 类是用来创建迷你模块的蓝本或定义
+ 实例化是如何创建这些小模块，并在同一时间将其导入。实例化仅仅是指通过类创建一个对象。
+ 由此产生的迷你模块被称为对象，你可以将其分配给一个变量，让它开始运行