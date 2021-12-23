---
title: CentOS6.5 Telnet安装
tags:
  - telnet
  - 搭建
  - Linux
categories:
  - Linux
  - 搭建
keywords: 
  - 搭建
  - Telnet
cover: >-
  https://img0.baidu.com/it/u=4293397279,3592153418&fm=26&fmt=auto
abbrlink: 7b6a2bcc
---





### 安装Telnet

查看是否安装

```
rpm -qa telnet-server
```

安装

```
yum -y install telnet-server
```

![](https://www.helloimg.com/images/2021/11/07/Chev0T.png)

接下来就重新启动xinetd并把telnet添加到开机启动

```
service xinetd resart
chkconfig telnet on
```

![](https://www.helloimg.com/images/2021/11/07/ChecGq.png)

![](https://www.helloimg.com/images/2021/11/07/CheWHh.png)

添加23端口

![](https://img0.baidu.com/it/u=125088234,459388324&fm=26&fmt=auto)

```
iptables -I INPUT -p tcp --dport 23 -j ACCEPT		添加23端口
service iptables save 		保存
service iptablse restart	重启
```

![](https://www.helloimg.com/images/2021/11/07/Che9Dc.png)

最后一步

![](https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fimage.110go.com%2Fupload%2Ftpk3%2F105185353.jpg&refer=http%3A%2F%2Fimage.110go.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1638868549&t=1327c4bad0dbf3cf63b9e842bfeb336a)

打开Kali扫描CentOS6.5的端口

![](https://www.helloimg.com/images/2021/11/07/Ched4r.png)



结束！

![](https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fnimg.ws.126.net%2F%3Furl%3Dhttp%3A%2F%2Fdingyue.ws.126.net%2F2021%2F0517%2F3952871fj00qt8ed30006d2005i0053g005i0053.jpg%26thumbnail%3D650x2147483647%26quality%3D80%26type%3Djpg&refer=http%3A%2F%2Fnimg.ws.126.net&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1638868617&t=3df9ead09bc432e369fce576c23c3b88)