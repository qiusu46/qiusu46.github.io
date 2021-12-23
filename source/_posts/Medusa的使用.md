---
title: Medusa工具使用
tags:
  - Kali
  - 爆破
categories:
  - Linux
  -	Kali
  - 工具
keywords:
  - Kali
  - 爆破
  - Medusa
cover: https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fhbimg.b0.upaiyun.com%2F5776bb61a68cf1371ff18d327a6f7bc3f111cdce29ec9-NmVwkJ_fw658&refer=http%3A%2F%2Fhbimg.b0.upaiyun.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1640398444&t=b3900207d8c2ce27c867901c0681c04c
abbrlink: 'Medusha'
---




## 科普

​    Medusa是支持AFP, CVS, FTP, HTTP, IMAP, MS-SQL, MySQL, NCP (NetWare),    NNTP, PcAnywhere, POP3, PostgreSQL, rexec, rlogin, rsh, SMB, SMTP    (AUTH/VRFY), SNMP, SSHv2, SVN, Telnet, VmAuthd, VNC的密码爆破工具。 最近搞一个项目,需要爆破postgres这个数据库的账号密码.想弄个全球的工具. 

## 基本使用

使用语法：

```
medusa -h IP -u 用户名 -P 密码字典 -M 模块执行名称
```

其他参数：

```
-h [TEXT]      目标IP
-H [FILE]      目标主机文件
-u [TEXT]      用户名
-U [FILE]      用户名文件
-p [TEXT]      密码
-P [FILE]      密码文件
-C [FILE]      组合条目文件
-O [FILE]      文件日志信息
-e [n/s/ns]    N意为空密码，S意为密码与用户名相同
-M [TEXT]      模块执行名称
-m [TEXT]      传递参数到模块
-d             显示所有的模块名称
-n [NUM]       使用非默认端口
-s             启用SSL
-r [NUM]       重试间隔时间，默认为3秒
-t [NUM]       设定线程数量
-L             并行化，每个用户使用一个线程
-f             在任何主机上找到第一个账号/密码后，停止破解
-q             显示模块的使用信息
-v [NUM]       详细级别（0-6）
-w [NUM]       错误调试级别（0-10）
-V             显示版本
-Z [TEXT]      继续扫描上一次
```

