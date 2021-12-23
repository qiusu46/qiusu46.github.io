---
title: CentOS6.5 ftp安装
tags:
  - Linux
  - FTP
  - 搭建
categories:
  - Linux
  - 搭建
keywprds:
  - Linux
  - 搭建
cover: >-
  https://img0.baidu.com/it/u=4293397279,3592153418&fm=26&fmt=auto
abbrlink: c6d92ee6
---





### 安装vsftpd

检查是否已安装vsftpd

```
rpm -qa | grep vsftpd
```

![](https://www.helloimg.com/images/2021/11/07/ChFEWC.png)

好，我没有安装

![](https://img1.baidu.com/it/u=517018669,4200314082&fm=26&fmt=auto)

如果没有安装就安装，并设置开机启动

```
yum -y install vsftpd
chkconfig vsftpd on
```

![](https://www.helloimg.com/images/2021/11/07/ChFJUQ.png)

如果安装不了参考 [点这个](https://blog.51cto.com/u_12922638/2412603) 或者 [点这个](https://www.xmpan.com/944.html)

接下卡添加一个防火墙

![](https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fimg.adoutu.com%2Farticle%2F1592910059810.gif&refer=http%3A%2F%2Fimg.adoutu.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1638861972&t=22dba43b48c44e2f201df4e00a0091c4)

```
vim /etc/sysconfig/iptables
```

![](https://www.helloimg.com/images/2021/11/07/ChFXwo.png)

添加

```
-A INPUT -m state --state NEW -m tcp -p tcp --dport 21 -j ACCEPT
```

![](https://www.helloimg.com/images/2021/11/07/ChFxqS.png)



重启防火墙

```
service iptables restart
```

![](https://www.helloimg.com/images/2021/11/07/ChFefD.png)



开启vsftpd

```
service vsftpd start
```

![](https://www.helloimg.com/images/2021/11/07/ChFtnu.png)



开启21端口

```
iptables -I INPUT -p tcp --dport 21 -j ACCEPT
service iptables start
service iptables save
service iptables restart
```



一些其他基本命令

```
service vsftpd status	查看状态
service vsftpd start	启动
service vsftpd restart	重启
service vsftpd stop		停止
```

![](https://img0.baidu.com/it/u=3981365252,242824101&fm=26&fmt=auto)

### 配置

配置文件在 /etc/vsftpd/vsftpd.conf

用户权限配置说明：

|                        |                    chroot_local_user=YES                     |                     chroot_local_user=NO                     |
| :--------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
| chroot_list_enable=YES | 1.所有用户都被限制在目录下<br />2.使用chroot_list_file指定的用户列表，这些用户作为“例外”，不受限制 | 1.所有用户都不被限制其主目录下<br />2.使用chroot_list_file指定的用户列表，这些用户作为“例外”受到限制 |
| chroot_list_enable=NO  | 1.所有用户都被限制在其主目录下 <br />2.不使用chroot_list_file指定的用户列表，没有任何“例外”用户 | 1.所有用户都不被限制其主目录下<br />2.不使用chroot_list_file指定的用户列表，没有任何“例外”用户 |

结束！欢迎下次光临。

![](https://img1.baidu.com/it/u=4261116483,563439624&fm=253&fmt=auto&app=120&f=JPEG?w=156&h=92)