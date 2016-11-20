---
layout: post
title: 笨办法学python第三天
category: 技术
tags: Python
keywords: python,脚本语言
description: python学习
---
@(python)

# python进阶

## 函数

### python中的map()函数
map()是 Python 内置的高阶函数，它接收一个函数 f 和一个 list，并通过把函数 f 依次作用在 list 的每个元素上，得到一个新的 list 并返回。

```python
#-*-coding:utf-8-*-

def format_name(s):
	return s[0].upper() + s[1:].lower()

print map(format_name,['adam','LISA','barT'])
```


**注意**：map()函数不改变原有的 list，而是返回一个新的 list。

### python中reduce()函数
reduce()函数也是Python内置的一个高阶函数。reduce()函数接收的参数和 map()类似，一个函数 f，一个list，但行为和 map()不同，reduce()传入的函数 f 必须接收两个参数，reduce()对list的每个元素反复调用函数f，并返回最终结果值。

例如，编写一个f函数，接收x和y，返回x和y的和：

```python
def f(x, y):
    return x + y
```

调用 reduce(f, [1, 3, 5, 7, 9])时，reduce函数将做如下计算：

```
先计算头两个元素：f(1, 3)，结果为4；
再把结果和第3个元素计算：f(4, 5)，结果为9；
再把结果和第4个元素计算：f(9, 7)，结果为16；
再把结果和第5个元素计算：f(16, 9)，结果为25；
由于没有更多的元素了，计算结束，返回结果25。
上述计算实际上是对 list 的所有元素求和。虽然Python内置了求和函数sum()，但是，利用reduce()求和也很简单。
```

reduce()还可以接收第3个可选参数，作为计算的初始值。如果把初始值设为100，计算：

```
reduce(f, [1, 3, 5, 7, 9], 100)
```

结果将变为125，因为第一轮计算是：

计算初始值和第一个元素：f(100, 1)，结果为101。


### python中filter()函数
filter()函数是 Python 内置的另一个有用的高阶函数，filter()函数接收一个函数 f 和一个list，这个函数 f 的作用是对每个元素进行判断，返回 True或 False，filter()根据判断结果自动过滤掉不符合条件的元素，返回由符合条件元素组成的新list。

```python
import math

def is_sqr(x):
    return int(math.sqrt(x))*int(math.sqrt(x)) == x

print filter(is_sqr, range(1, 101))
```
