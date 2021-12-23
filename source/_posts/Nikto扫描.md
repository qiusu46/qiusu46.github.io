---
title: Nikto扫描
tags:
  - Linux
  - 扫描
  - Nikto
categories:
  - Linux
  - Kali
  - 工具
keywords:
  - Nikto
cover: https://gimg2.baidu.com/image_search/src=http%3A%2F%2Finews.gtimg.com%2Fnewsapp_bt%2F0%2F12975410056%2F1000.jpg&refer=http%3A%2F%2Finews.gtimg.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1640693459&t=953035f4f8af3c9d7d1138960feffae5
abbrlink: 1
---
## Nikto简介

Nikto是一款著名的Web漏洞扫描神器，支持XSS、SQL注入、Web目录爬行、敏感信息、信息收集等常用的Web漏洞的扫描和发现。其特点扫描全面，速度快。



## Nikto常用命令

```
-upodate 	升级，更新插件
-host	扫描目标URL
-id username:password	http认证接口
-list-plugins	列出所有可用的插件
-evasion	IDS/IPS逃避技术（实例演示里有详细信息）
-port	指定端口（默认80）
-ssl	使用SSL
-useproxy	使用http代理
-vhost 域名	当一个IP拥有多个网站时使用
```



## Nikto交互参数（扫描过程中使用）

```
空格	报告当前扫描状态
v	显示详细信息
d	显示调试信息
e	显示http错误信息
p	显示扫描进度
r	显示重定向信息
c	显示cookie
a	显示身份认证过程
q	退出程序
N	扫描下一个目标
P	暂停扫描
```



## 实例演示

### 扫描单个地址

```
nikto -h http://172.16.1.106
```

![](https://www.helloimg.com/images/2021/11/28/GFuYOv.png)



### 扫描https网站

```
nikto -h www.baidu.com -ssl -p 443
```

![](https://www.helloimg.com/images/2021/11/28/GFyRu6.png)



### 扫描指定端口

```
nikto -h 172.16.1.106 -p 80
```

![](https://www.helloimg.com/images/2021/11/28/GFyMyQ.png)



### 扫描保存结果

```
nikto -h 172.16.1.106 -p 80 -o 1.html
```

![](https://www.helloimg.com/images/2021/11/28/GFyQpM.png)



### 指定目录扫描

```
nikto -h 172.16.1.106 -c /dvwa
```

![](https://www.helloimg.com/images/2021/11/28/GFyko0.png)



![](https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fc-ssl.duitang.com%2Fuploads%2Fitem%2F201912%2F13%2F20191213005906_hqhfn.thumb.400_0.jpg&refer=http%3A%2F%2Fc-ssl.duitang.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1640693265&t=d83d0bc7eb074b85db6e38bf244d9c15)