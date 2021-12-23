---
title: Python爬虫
tags:
  - Python
  - 爬虫
categories:
  - Python
  - 爬虫
keywords:
  - Python
  - 爬虫
cover: >-
  https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fpic4.zhimg.com%2Fv2-4fa87dc9dfba36319c7d85be442ed32b_1440w.jpg%3Fsource%3D172ae18b&refer=http%3A%2F%2Fpic4.zhimg.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1638754900&t=f7dcbdd7114d366ce07c5721460facc9
abbrlink: c386cf1b
---





# Python lxml etree爬虫

### 安装

打开cmd在终端利用pip命令安装

```
pip install lxml
```



### Xpath常用规则

表达式								描述

nodename						选取此节点的所有子节点

/		 								从根节点选取

//										从匹配选择的当前节点选择文档中的节点，而不考虑他们的的位置

.		  								选取当前节点

..		 								选取当前节点的父节点

@										选取属性

⁎  									   通配符，选择所有元素节点于元素名

@⁎									  选取所有属性

[@attrib]							选取具有给定属性的所有元素

[@attrib='value']			  选取给定属性具有给定值的元素

[tag]								   选取所有具有指定元素的直接字节点

[tag='text']						选取所有具有指定元素并且文本内容是text节点



### 实例化etree对象

```
etree.HTEML(源码数据)
```



### Xpath使用实例

x 属性定位：    #找到class属性值为song的div标签

​						    //div[@class="song"] 

层级&索引定位：    #找到class属性值为tang的div的直系子标签ul下的第二个子标签li下的直系子标签a

​							    //div[@class="tang"]/ul/li[2]/a

逻辑运算：    #找到href属性值为空且class属性值为du的a标签

​					    //a[@href="" and @class="du"]

模糊匹配：    //div[contains(@class, "ng")]

​					    //div[starts-with(@class, "ta")]

取文本：    # /表示获取某个标签下的文本内容

​					//表示获取某个标签下的文本内容和所有子标签下的文本内容

   				 //div[@class="song"]/p[1]/text() 

​				   //div[@class="tang"]//text()

取属性：    //div[@class="tang"]//li[2]/a/@href



### 使用实例-图片爬取下载

```
# 需求：解析下载图片数据 http://pic.netbian.com/4kbeijing/
import requests
from lxml import etree
import os
if __name__ == "__main__":
    url = 'http://pic.netbian.com/4kbeijing/'
    headers = {
        'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/73.0.3683.103 Safari/537.36'
    }
    response = requests.get(url=url, headers=headers)
    # 手动设定响应数据的编码格式
    # response.encoding = 'utf-8'
    page_text = response.text

    # 数据解析：src的属性值  alt属性
    tree = etree.HTML(page_text)
    li_list = tree.xpath('//div[@class="slist"]/ul/li')

    # 创建一个文件夹
    if not os.path.exists('./picLibs'):
        os.mkdir('./picLibs')

    for li in li_list:
        img_src = 'http://pic.netbian.com' + li.xpath('./a/img/@src')[0]
        img_name = li.xpath('./a/img/@alt')[0] + '.jpg'
        # 通用处理中文乱码的解决方案
        # encode('iso-8859-1')
        # 是将gbk编码编码成unicode编码
        # decode(‘gbk’) 是从unicode编码解码成gbk字符串
        img_name = img_name.encode('iso-8859-1').decode('gbk')

        # print(img_name,img_src)
        # 请求图片进行持久化存储
        img_data = requests.get(url=img_src, headers=headers).content
        img_path = 'picLibs/' + img_name
        with open(img_path, 'wb') as fp:
            fp.write(img_data)
            print(img_name, '下载成功！！！')
```



# Request

### 库方法

```
	requests.request()			构造一个请求，支撑一下各方法的基础方法
	requests.get()				获取HTML网页的主要方法，对应于HTML的GET
	requests.head()				获取HTML网页头信息的方法，对应于HTML的HEAD
	requests.post()				向HTML网页提交POST请求的方法，对应于HTTP的POST
	requests.put()				向HTML网页提交PUT请求的方法，对应于HTTP的PUT
	requests.patch()			向HTML网页提交局部修改请求，对应于HTTP的PATCH
	requests.delete()			向HTML页面提交删除请求，对应于HTTP的DELETE
	
```



### 对象属性

```
r.status_code					HTTP请求的返回状态，200表示成功，404表示失败
r.text							HTTP响应内容的字符串形式，即，url对应的页面内容
r.encoding						从HTTP header中猜测的响应内容编码方式
r.apparent_encoding				从内容分析出的响应内容编码方式（备选编码方式）
r.content()						HTTP响应内容的二进制形式
```



### 库的异常

```
requests.ConnectionError		网络连接错误异常，如DNS查询失败、拒绝连接等
requests.HTTPError				HTTP错误异常
requests.URLRequired			URL缺失异常
requests.TooMangRedirects		超过最大重定向次数，产生重定向异常
requests.ConnectTimeout			连接远程服务器超时异常
requests.Timeout				请求URL超时，产生超时异常
r.raise_for_status()			如果不是200，产生异常requests.HTTPError
```



### 各方法使用样式

```
requests.get(url, params=None, **kwargs)
url:拟获取页面url链接
params:url中的额外参数，字典或字节流格式，可选
**kwargs:12个控制访问的参数

requests.head(url, **kwargs)
url:拟获取页面的url链接
**kwargs:13个控制访问的参数

requests.post(url, data=None, json=None, **kwargs)
url:拟获取页面的url链接
data:字典、字节序列或文件，Request的内容
json:JSON格式的数据，Request的内容
**kwargs:11个控制访问参数

requests.put(url,data=None, **kwargs)
url:拟更新页面的url链接
data:字典、字节序列或文件，Request的内容
**kwargs:12个控制访问参数

requests.patch(url, data=None, **kwargs)
url:拟更新页面url链接
data:字典、字节序列或文件，Request的内容
**kwargs:12个控制访问参数

requests.delete(url, **kwargs)
url:拟删除页面的url链接
**kwargs:13个控制访问参数
```



### 基础入门

#### 导入模块

```
import requests
```



#### 简单使用

```
import requests

url = 'http://www.suqu46.cn'		#爬取的网站
header = {'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/84.0.4147.89 Safari/537.36 SLBrowser/7.0.0.9231 SLBChan/30'}		#请求头部信息
response = requests.get(url=url, headers=header)		#get方式
response.encoding = 'utf-8'				#编码
print(response.text)
print('\n\n')
print(response.content)
```

#response.text返回的是Unicode格式，通常需要转换为utf-8格式，否则就是乱码；response.content是二进制模式，可以下载视频之类的，如果想看的话需要decode成utf-8格式。
#不管是通过response.content.decode('utf-8')的方式还是通过response.encoding='utf-8'的方式都可以避免乱码的问题发生

复制代码去运行看text和content的区别



获取编码

![](https://www.helloimg.com/images/2021/11/06/CfMhot.png)



获取头部信息

![](https://www.helloimg.com/images/2021/11/06/CfMjSu.png)



#### 爬取文章标题

```
import requests
from lxml import etree

url = 'http://www.suqu46.cn/'
header = {'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/84.0.4147.89 Safari/537.36 SLBrowser/7.0.0.9231 SLBChan/30'}
response = requests.get(url=url, headers=header)
response.encoding = 'utf-8'

tree = etree.HTML(response.text)        #实例化对象
title = tree.xpath('//*[@id="recent-posts"]/div[1]/div[2]/a/text()')[0]     #写入文章标题的xpath（F12，定位到标题右击标题源码选择copy载选择copy xpath），/text()是获取文本，[0]是获取列表第一个。
print(title)
```

输出结果：
	MySQL注入

注：文章是会更新的，所以不一定是MySQL注入



#### 爬取页面所有文章标题

```
import requests
from lxml import etree

url = 'http://www.suqu46.cn/'
header = {'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/84.0.4147.89 Safari/537.36 SLBrowser/7.0.0.9231 SLBChan/30'}
response = requests.get(url=url, headers=header)
response.encoding = 'utf-8'

tree = etree.HTML(response.text)        #实例化对象
title = tree.xpath('//*[@id="recent-posts"]/div')

#//*[@id="recent-posts"]/div[1]/div[2]/a        第一个标题的xpath
#//*[@id="recent-posts"]/div[2]/div[2]/a        第二个标题的xpath，注意两个的区别

for TITLE in title:     #遍历所有标题
    Title = TITLE.xpath('./div[2]/a/text()')[0]
    print(Title)
    
```

输出结果：
	MySQL注入
	Kali Msfconsole工具SSH爆破
	Kali扫描工具
	CMD基础命令
	永恒之蓝
	Linux基础命令
	Hello World