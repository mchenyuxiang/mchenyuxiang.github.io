---
layout: post
title: Scrapy学习第一天
category: 技术
tags: Python
keywords: python,脚本语言
description: python学习
---
@(python)
#Scrapy学习爬虫第一天
最近在学完python后,想着用python来做一个爬虫,爬关键字在各个搜索引擎的排名情况.之前用beautifulsoap来做了一个单线程的,现在想尝试用scrapy的爬虫框架来做,来让爬虫更加完善.现在一步一步的把scrapy的手册看完,笔记中将记录看得觉得重要的一些点.
##总览
手册一开始是scrapy的总览,上个手册的例子

```python
import scrapy
class QuotesSpider(scrapy.Spider):
	name = "quotes"
	start_urls = [
		'http://quotes.toscrape.com/tag/humor/',
	]
	def parse(self, response):
		for quote in response.css('div.quote'):
			yield {
				'text': quote.css('span.text::text').extract_first(),
				'author': quote.xpath('span/small/text()').extract_first(),
			}
		next_page = response.css('li.next a::attr("href")').extract_first()
		if next_page is not None:
			next_page = response.urljoin(next_page)
			yield scrapy.Request(next_page, callback=self.parse)
```
下面先解释啊下以上代码:
` start_urls ` 代表的是抓取的网页的地址.parse是一个回调方法.在回调方法中,使用了CSS选择器,yield了一个python的字典,有text和author.然后会寻找下一个页面,并且调度另外一个reques来使用同样的parse方法,也是回调函数.

在这里,可以注意到Scrapy的一个主要的有事:request的调度和执行是异步的.也就是说,Scrapy不需要一直等到请求完成并且被执行成功,他可以在一个请求被执行的同时发送另外一个请求或者去做其他的事情.也就是说,request会一直有,甚至是当request失败或者有错误的时候.

##安装
###需要的包

	- lxml:最低版本 3.4
	- parsel
	- w3lib
	- twisted:最低版本 14.0
	- cryptography and pyOpenSSL:最低版本 0.14

### 推荐使用虚拟环境
这一段,因为没有使用过,而且目前没有考虑使用,所以暂时跳过,有需要再回头阅读

### 安装

```
pip install Scrapy
```

## Scrapy手册

下面我们将做以下几件事情:
1.	建立一个Scrapy的工程
2.	写一个爬虫并且提取数据
3.	通过命令行爬取数据
4.	通过链接来改变爬虫的地址
5.	使用爬虫参数

### 建立工程
通过一条命令即可创建一个Scrapy的工程.
```python
scrapy startproject tutorial
```
 
将会得到工程以及文件夹.要说明的是,自己的爬虫是写在spider文件夹下面的.

###第一个爬虫

爬取两个网页的信息,并且将其写入到文件中
```python
import scrapy

class QuotesSpider(scrapy.Spider):
    name = "quotes"

    def start_requests(self):
        urls = [
            'http://quotes.toscrape.com/page/1/',
            'http://quotes.toscrape.com/page/2/',
        ]
        for url in urls:
            yield scrapy.Request(url=url,callback=self.parse)

    def parse(self,response):
        page = response.url.split("/")[-2]
        filename = 'quote-%s.html' % page
        with open(filename,'wb') as f:
            f.write(response.body)

        self.log('Save file %s' % filename)
```

以上文件需要说明:
- name:是爬虫的名字,在整个项目中必须是唯一的.不能有同名的爬虫.
- start_requests():是一个迭代的Request.
- parse():是来处理response的下载文件的程序.

如何运行爬虫:
` scrapy srawl quotes`.这里的quotes为上面程序的name

###如何提取数据
最好的方法是首先执行scrapy shell来尝试提取数据

` scrapy shell 'http://quotes.toscrape.com/page/1/' `

然后会进入shell环境,就可以开始尝试css选择了

```
In [1]: response.css('title')
Out[1]: [<Selector xpath=u'descendant-or-self::title' data=u'<title>Quotes to Scrape</title>'>]

In [3]: response.css('title::text').extract()
Out[3]: [u'Quotes to Scrape']

```

这样我们就可以提取出title里面的文字.

###使用xpath
xpath我还没有看,但是我看到谷歌浏览器有xpath的插件,可以直接使用谷歌浏览器的xpath来进行抓取感觉也蛮方便的,目前我用的是beautifulsoap来进行的网页解析.有时间也看看xpath的,这里我只是按照文档进行使用.

```
In [4]: response.xpath('//title')
Out[4]: [<Selector xpath='//title' data=u'<title>Quotes to Scrape</title>'>]

In [5]: response.xpath('//title/text()').extract()
Out[5]: [u'Quotes to Scrape']

In [6]: response.xpath('//title/text()').extract_first()
Out[6]: u'Quotes to Scrape'

```

###通过页面链接抓取
这里抓取的通过[http://quotes.toscrape.com/](http://quotes.toscrape.com/)列表的内容,读取作者链接信息后进入作者主页,然后抓取作者相关信息

```python
import scrapy

class AuthorSpider(scrapy.Spider):
    name = 'author'

    start_urls = ['http://quotes.toscrape.com/']

    def parse(self, response):
        for href in response.css('.author+a::attr(href)').extract():
            yield scrapy.Request(response.urljoin(href),
                                 callback=self.parse_author)

        next_page = response.css('li.next a::attr(href)').extract_first()
        if next_page is not None:
            next_page = response.urljoin(next_page)
            yield scrapy.Request(next_page,callback=self.parse)

    def parse_author(self,response):
        def extract_with_css(query):
            return response.css(query).extract_first().strip()

        yield {
            'name':extract_with_css('h3.author-title::text'),
            'birthdate':extract_with_css('.author-born-date::text'),
            'bio':extract_with_css('.author-description::text'),
        }
```

上面有一点要说明`response.urljoin(href)`,由于在页面上,这里是抓取的是相对路径,所以要进入作者相关信息网页,必须是网址加上相对路径才能访问,`urljoin`从字面意思可以知道就是联合访问的意思.

