---
title: Kali扫描工具
tags:
  - Linux
  - Kali
  - 扫描
  - nmap
categories:
  - Linux
  - Kali
  - 工具
keywords:
  - Linux
  - Kali
  - 工具
cover: >-
  https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fimage.3001.net%2Fimages%2F20151123%2F14482473953522.png
abbrlink: 294380fb
---



# Kali扫描工具

### Nmap扫描基础

```
扫描全部端口
nmap -p- IP

扫描存活主机（ping）
nmap -sP IP/24

不ping式扫描主机
nmap -Pn IP/24
nmap -P0 IP/24

半开放扫描
nmap -sS IP/24

扫描端口服务版本
nmap -sV IP/24

扫描外部文件
nmap -iL ip.txt

综合性扫描
nmap -A IP/24

扫描操作系统指纹信息
nmap -O IP/24

RPC扫描
nmap -sR IP/24

ACK和ICMP并型扫描
nmap -PB IP/24

导出全部格式的扫描结果
nmap -oA 文件名 IP

导出XML格式的扫描结果
nmpa -oX x.xml IP

导出标准格式的扫描结果
nmap -oN 文件名 IP

扫描等级
nmap -T4 IP		//有T1~T5

注：
IP/24是扫描所有IP0~255
IP是电脑IP
```



### arping

```
arping -c 5 IP	//指定发包数量
```



### fping扫描

```
普通扫描
fping Ip

扫描网段或指定范围
fping -g IP/24
fping -g IP1 IP2

回显存活主机
fping -a IP

回显不存活主机
fping -u IP

扫描外部文件
fping -f ip.txt

循环ping
fping -l IP

统计扫描结果
fping -s IP
```



### dirrsearch 扫描

```
注：需下载

dirrsearch -u "网站" -e *		扫描所有目录
```

