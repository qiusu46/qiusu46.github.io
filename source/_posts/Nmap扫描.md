---
title: Nmap扫描题目解析
tags:
  - Linux
  - Kali
  - Nmap
categories:
  - Linux
  -	Kali
  - 工具
keywords:
  - Linux
  - Nmap
cover: https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fc-ssl.duitang.com%2Fuploads%2Fitem%2F201903%2F30%2F20190330192531_jKAKG.jpeg&refer=http%3A%2F%2Fc-ssl.duitang.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1639138038&t=8e40943f2911288ff5ccef410c9fa257
abbrlink: 'jstrn'
---






## Nmap扫描

例题：

​	使用nmap工具对靶机进行扫描

1. 将扫描到的回显信息中22端口开放状态作为flag提交

flag: 

2. 使用不ping扫描方式对主机进行扫描，将必要参数作为flag提交

flag:

3. 扫描主机操作系统，将回显信息中的OS details:一行作为flag提交

flag:

4. 对靶机进行服务版本号扫描，将必要参数作为flag提交

Flag:

5. 扫描主机22端口的服务版本，并将服务版本号作为flag提交

flag:

6. 将扫描到的数据以xml的格式导出，并将必要的参数作为flag提交

flag:

7. 对主机进行综合扫描，并将MAC Address:一行的MAC地址作为flag提交

flag:

8. 使用arping工具向靶机发送5个数据包，并将必要参数作为flag提交

flag:

9. 扫描存活主机，将必要参数作为flag提交

Flag:

10. 使用半开放式扫描，将必要参数作为flag提交

Flag:

11. 对靶机进行扫描，将445端口对应的服务名称作为flag提交

Flag:

首先我这的靶机是Metasploitable2，IP是172.16.1.103

然后开始做题

![](https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fbqbimg.yuexw.com%2Farticle%2F228%2F2_xxlmw__.jpg&refer=http%3A%2F%2Fbqbimg.yuexw.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1639134523&t=db916e9157e9b29719b89355b91f8d27)

### 第一题

将扫描到的回显信息中22端口开放状态作为flag提交



我们看到题目的时候记得先看清楚题目要求，这道题的要求是提交22端口的开放状态，所以我们直接扫描22端口

```
nmap -p 22 172.16.1.103			//-p是指定一个端口，端口后面是IP
```

![](/img/Nmap/1.png)

从图上可以看到PORT，STATE，SERVICE三个参数

POST对应端口，STATE对应开放状态，SERVICE对应服务

所以这道题的flag为**open**

![](https://img0.baidu.com/it/u=647578192,1820478163&fm=26&fmt=auto)



### 第二题

使用不ping扫描方式对主机进行扫描，将必要参数作为flag提交



还是一样，注意看题，题目要求不ping式扫描

我们要知道不ping式扫描时nmap -Pn IP或者nmap -P0 IP

但是题目要求的是必要参数，所以这道题不需要去扫描直接填写参数-Pn或者-P0

所以这道题的flag为：**-Pn** 或 **-P0**



是不是很简单

![](https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fww4.sinaimg.cn%2Flarge%2F9150e4e5ly1fkirjpkr0dj202s02sjr7.jpg&refer=http%3A%2F%2Fwww.sina.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1639136402&t=84d7324463b7c6e63a829efd5cbd4d06)



### 第三题

扫描主机操作系统，将回显信息中的OS details:一行作为flag提交



一样，分析题目要求

题目要求扫描主机操作系统，所以他是用nmap -O IP指令

然后题目要求提交OS details：后面的内容

前往kali扫描靶机

```
nmap -O 172.16.1.103
```

![](/img/Nmap/2.png)

所以这道题的flag为：**Linux 2.6.9 - 2.6.33**



### 第四题

对靶机进行服务版本号扫描，将必要参数作为flag提交



分析题目，要求版本号扫描，提交必要参数

简直就是白给

![](https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fc-ssl.duitang.com%2Fuploads%2Fitem%2F201812%2F17%2F20181217092442_gayyq.thumb.100_100_c.jpg&refer=http%3A%2F%2Fc-ssl.duitang.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1639136723&t=874a520624ef79a07247652724a58c18)

我们要知道扫描版本号的指令是nmap -sV IP

所以flag为：**-sV**



### 第五题

扫描主机22端口的服务版本，并将服务版本号作为flag提交



这道题一样是白给，从上题的题目知道了扫描版本号的指令，你可以直接扫描IP找到22端口的的版本号

或者加-p 22 只扫描22端口

```
nmap -sV -p 22 172.16.1.103
```

![](/img/Nmap/3.png)

从图中可以看VERSION，这个就是版本号

我们找到22端口对应的版本号

所以flag为：**OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)**

![](https://img0.baidu.com/it/u=3036192872,1274237577&fm=26&fmt=auto)



### 第六题

将扫描到的数据以xml的格式导出，并将必要的参数作为flag提交



白给题目

![](https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fimage.110go.com%2Fupload%2Ftpk3%2F105185353.jpg&refer=http%3A%2F%2Fimage.110go.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1639137041&t=a64ffbf942295ef0d77d4267463e01bf)

首先要知道nmap以xml格式导出的指令

```
nmap -oX xx.xml IP
```

题目要求的室必要参数

注意是必要参数

所以flag为：**-oX**



### 第七题

对主机进行综合扫描，并将MAC Address:一行的MAC地址作为flag提交



综合扫描的命令为namp -A IP

根据题目要求去扫描找到MAC Address

```
nmap -A 172.16.1.103
```

![](/img/Nmap/4.png)

找到题目需求的

所以flag为：**00:0C:29:22:FE:50**



### 第八题

使用arping工具向靶机发送5个数据包，并将必要参数作为flag提交



这道题没什么难度的，存粹靠记arping命令

```
arping -c 5 IP
```

-c后面的5为发送数据包的数量

题目要求必要参数，所以5也要加进去

所以flag为：**-c 5**



### 第九题

扫描存活主机，将必要参数作为flag提交



一样，必要参数，扫描存活主机的命令是

```
nmap -sP IP
```

所以flag为：**-sP**



### 第十题

使用半开放式扫描，将必要参数作为flag提交



还是一样，必要参数，半开放式扫描的命令式

```
nmap -sS IP
```

所以flag为：**-sS**



### 第十一题

对靶机进行扫描，将445端口对应的服务名称作为flag提交



根据题目要求直接扫描445端口

```
nmap -p 445 172.16.1.103
```

![](/img/Nmap/5.png)

所以flag为：**microsoft-ds**



不清楚Nmap指令的点击：[Nmap基础命令](http://www.suqu46.cn/fengye/294380fb.html)



![](https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fc-ssl.duitang.com%2Fuploads%2Fitem%2F202003%2F21%2F20200321131210_fsumr.thumb.1000_0.gif&refer=http%3A%2F%2Fc-ssl.duitang.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1639137883&t=d520f6a1b94d84758cc24971fbfae8ba)
