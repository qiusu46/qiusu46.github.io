---
title: CMD基础命令
tags:
  - Windows
  - CMD
  - 基础
categories:
  - Windows
  - 基础
keywords:
  - CMD
  - 基础
  - Windows
cover: 'https://img2.baidu.com/it/u=152309329,2781784674&fm=26&fmt=auto'
abbrlink: 91f9f04
---



# Windows CMD基础命令

```
win键+R开启运行，输入cmd进入命令窗口

//进入某个盘
D:		进入D盘

//查看目录文件
dir

//创建目录
md 目录名（文件夹）

//删除目录
rd 目录名（文件夹）

//清除屏幕
cls

//复制文件
copy 路径\文件名 路径\文件名		把一个文件拷贝到另一个地方

//移动文件
move 路径\文件名\ 路径\文件名		把一个文件移动到另一个地方

//删除文件
del 文件名（不能删除目录）

//用来测试网络是否畅通
ping ip(主机名)

//重命名
ren 源文件名 新文件名

//查看文本文件内容
type 文本文件

//创建用户
net user 用户名 密码 /add		密码复杂度需要满足要求

//查看用户
net user		//查看所有用户
net user test1	//查看指定用户 如test1

//删除用户
net user 用户名 /del

//重置用户密码
net user 用户名 新密码

//给用户添加管理员权限
net localgroup administrators 用户 /add

//查看IP
ipconfig
ipconfig /all		显示详细
ipconfig /release	释放ip地址
ipconfig /renew		重新获取ip地址
ipconfig /flushdns	刷新DNS缓存
```

