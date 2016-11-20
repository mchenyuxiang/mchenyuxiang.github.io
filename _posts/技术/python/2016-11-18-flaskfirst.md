---
layout: post
title: Flask学习web第一天
category: 技术
tags: Python
keywords: python,脚本语言
description: python学习
---
@(python)
#Flask web学习第一天
##安装
Flask 依赖两个外部库：Werkzeug 和 Jinja2 。

```
sudo pip install Werkzeug
sudo pip install Jinja2
sudo pip install Flask
```
##Hello World

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello World!'

if __name__ == '__main__':
    app.run()
```

1. route() 装饰器告诉 Flask 什么样的URL 能触发我们的函数
2.  run() 函数来让应用运行在本地服务器上。 其中 if ```__name__ == '__main__': ```确保服务器只会在该脚本被 Python 解释器直接执行的时候才会运行，而不是作为模块导入的时候。

如果你运行了这个服务器，你会发现它只能从你自己的计算机上访问，网络中其它任何的地方都不能访问。在调试模式下，用户可以在你的计算机上执行任意 Python 代码。因此，这个行为是默认的。

如果你禁用了 debug 或信任你所在网络的用户，你可以简单修改调用 run() 的方法使你的服务器公开可用，如下:
```
app.run(host='0.0.0.0')
```
这会让操作系统监听所有公网 IP。

###调试模式

虽然 run() 方法适用于启动本地的开发服务器，但是你每次修改代码后都要手动重启它。这样并不够优雅，而且 Flask 可以做到更好。如果你启用了调试支持，服务器会在代码修改后自动重新载入，并在发生错误时提供一个相当有用的调试器。

有两种途径来启用调试模式。一种是直接在应用对象上设置:
```
app.debug = True
app.run()
```
另一种是作为 run 方法的一个参数传入:
```
app.run(debug=True)
```
两种方法的效果完全相同。

##路由
现代 Web 应用的 URL 十分优雅，易于人们辨识记忆，这一点对于那些面向使用低速网络连接移动设备访问的应用特别有用。如果可以不访问索引页，而是直接访问想要的那个页面，他们多半会笑逐颜开而再度光顾。

如上所见， route() 装饰器把一个函数绑定到对应的 URL 上。

这里是一些基本的例子:
```python
@app.route('/')
def index():
    return 'Index Page'

@app.route('/hello')
def hello():
    return 'Hello World'
```
但是，不仅如此！你可以构造含有动态部分的 URL，也可以在一个函数上附着多个规则。

##HTTP方法
HTTP （与 Web 应用会话的协议）有许多不同的访问 URL 方法。默认情况下，路由只回应 GET 请求，但是通过 route() 装饰器传递 methods 参数可以改变这个行为。这里有一些例子:
```python
@app.route('/login', methods=['GET', 'POST'])
def login():
    if request.method == 'POST':
        do_the_login()
    else:
        show_the_login_form()
```

##重定向和错误
你可以用 redirect() 函数把用户重定向到其它地方。放弃请求并返回错误代码，用 abort() 函数。这里是一个它们如何使用的例子:
```python
from flask import abort, redirect, url_for

@app.route('/')
def index():
    return redirect(url_for('login'))

@app.route('/login')
def login():
    abort(401)
    this_is_never_executed()
```
这是一个相当无意义的例子因为用户会从主页重定向到一个不能访问的页面 （401 意味着禁止访问），但是它展示了重定向是如何工作的。

默认情况下，错误代码会显示一个黑白的错误页面。如果你要定制错误页面， 可以使用 errorhandler() 装饰器:
```python
from flask import render_template

@app.errorhandler(404)
def page_not_found(error):
    return render_template('page_not_found.html'), 404
```
注意 render_template() 调用之后的 404 。这告诉 Flask，该页的错误代码是 404 ，即没有找到。默认为 200，也就是一切正常。

