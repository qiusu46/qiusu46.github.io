---
title: FTP笑脸漏洞
tags:
  - Kali
  - 渗透
categories:
  - Linux
  - Kali
  - 渗透
keywords:
  - 渗透
  - 笑脸
  - FTP
cover: >-
  https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fb-ssl.duitang.com%2Fuploads%2Fitem%2F201605%2F27%2F20160527231830_8SmRK.thumb.700_0.jpeg&refer=http%3A%2F%2Fb-ssl.duitang.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1638848394&t=1a77f6341d90774798f6775965449817
abbrlink: 3e9895be
---





## 准备工作

靶机：Metasploitable2

攻击机：Kali



## 查看IP

首先我们查看一下Metasploitable2的IP还有我们的Kali的IP

![](https://www.helloimg.com/images/2021/11/07/Ch5X3v.png)

![](https://www.helloimg.com/images/2021/11/07/Ch5eME.png)



## 扫描FTP端口

好了，既然我们知道靶机的IP就扫描他的21端口的版本号

![](https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fimg.wxcha.com%2Ffile%2F201905%2F17%2F2ec4142728.jpg&refer=http%3A%2F%2Fimg.wxcha.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1638846992&t=4e380c43a4a50e162987f927a948d681)

![](https://www.helloimg.com/images/2021/11/07/Ch5EZ9.png)

现在我们知道他的版本号是2.3.4了

接着我们扫描全部端口

![](https://img1.baidu.com/it/u=1860989660,31265886&fm=253&fmt=auto&app=138&f=PNG?w=174&h=164)

![](https://www.helloimg.com/images/2021/11/07/Ch5q6Y.png)

注意！他现在是没有6200端口的

这时就需要我们去开启他了

![](https://img2.baidu.com/it/u=3843003660,1206078383&fm=26&fmt=auto)



## 开启6200端口

打开我们的CMD窗口

输入ftp 172.16.1.107

![](https://www.helloimg.com/images/2021/11/07/Ch5act.png)

输入用户名root:)

密码随便输

![](https://www.helloimg.com/images/2021/11/07/Ch5JSX.png)

看见没用户名是个歪着的笑脸

![](https://img2.baidu.com/it/u=1490811348,3819277822&fm=26&fmt=auto)

输完就和图片一样不用去管

接着我们回到Kali重新扫描他的所有端口

![](https://www.helloimg.com/images/2021/11/07/Ch5mQg.png)

然后你就发现多了个6200的端口

![](https://img0.baidu.com/it/u=3058060533,726879872&fm=26&fmt=auto)

## 连接

当开启6200端口后我们就可以使用nc命令连接了

![](https://www.helloimg.com/images/2021/11/07/Ch5syM.png)

然后我们使用命令看看能不能使用

![](https://www.helloimg.com/images/2021/11/07/Ch54mP.png)

呦吼，可以使用（Linux和CMD命令都可以使用）

![](https://img1.baidu.com/it/u=2229101157,1940665360&fm=26&fmt=auto)

最后记住他只能连接一次，退出去就进不了了

![](https://www.helloimg.com/images/2021/11/07/Ch5Ac6.png)

![](https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fc-ssl.duitang.com%2Fuploads%2Fitem%2F202004%2F11%2F20200411012317_xLZGk.thumb.400_0.gif&refer=http%3A%2F%2Fc-ssl.duitang.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1638847887&t=e1a8051ce0e2ca2d16f62373fb0f8f4e)