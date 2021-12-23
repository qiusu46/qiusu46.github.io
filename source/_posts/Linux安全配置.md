---
title: Linux安全配置
tags:
  - Linux
  - 安全加固
categories:
  - Linux
  -	安全加固
keywords:
  -	kali
  - 加固
  - 安全
cover: https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fs5.51cto.com%2Foss%2F201904%2F25%2F8cd99b614865af53acdae87f0e9117ac.jpg-wh_651x-s_2310818553.jpg&refer=http%3A%2F%2Fs5.51cto.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1639569653&t=2349fa98d9a83b8ed54282591fc9d84c
abbrlink: 'Linuxanquanpeizhi'
---











# 用户和组的管理

## 密码及账户安全

启动ContOS6.5

打开终端修改配置文件/etc/login.defs来让用户只能设置强密码与定期更换密码的规则。

```
vim /etc/login.defs
```

![](/img/Linuxaqpz/1.png)



修改配置

```
PASS_MAX_DAYS 60   //要求用户每60天修改一次密码
PASS_MIN_DAYS 0		//0为允许用户修改密码
PASS_MIN_LEN 8		//密码长度必须为8位数
PASS_WARN_AGE 7		//在密码失效前7天提醒用户修改密码
```

![](/img/Linuxaqpz/2.png)

修改完成后按Esc退出编辑，按住shift+：输入wq保存退出，修改过后的配置文件立即生效，但是只对修改后创建的用户生效



修改完配置后，新建用户test，并使用命令chage -l来查看用户账户的基本信息

添加通过修改配置文件，能对之后新建用户起作用，而且前系统已经存在的用户，则直接用chage来配置

```
chage 选项 用户名
-m	密码可更改的最小天数，为零时代表任何时候都可以更改密码
-M	密码保持有效的最大天数	99999为永不过期
-d	上次更改的日期
-E	帐号到期的日期，过了这天，此帐号将不可用
-w	用户密码到期前，提前收到警告信息的天数
```



总结：通过修改Linux账户密码复杂程度、长度、过期时间等相关安全策略，可实现对账户的基本保护。



## 配置PAM认证模块

​	Linux—PAM（Linux可插入认证模块）是一套共享库，使本地系统管理员可以随意选择程序的认证方式。换句话说，不用（重新编写）重新编译一个包含PAM功能的应用程序，就可以改变它使用的认证机制。这种方式下，就算升级本地认证机制，也不用修改程序。

​	当一个服务器请求PAM模块的时候，PAM本身是不提供服务验证的，它是调用其它的一群模块来进行服务器请求验证，这样的文件全放在了/lib/security中。具体到哪一个服务使用哪一种具体的模块，这是由具体PAM服务文件定义的（/etc/pam.d）



启动CentOS6.5

打开终端进入PAM配置文件 /etc/pam.d

```
vim /etc/pam.d
```

![](/img/Linuxaqpz/3.png)



编辑system-auth配置文件

```
vim system-auth
```

![](/img/Linuxaqpz/4.png)



禁止使用旧密码——找到同时有“password”和“pam_unix.so”字段，在其后加上字段“remeber=5”（表示禁止使用最近用过的5个密码）

![](/img/Linuxaqpz/5.png)



设置最短密码长度——找到同时有“password”和”pam_cracklib.so“的位置，将其修改为：password requisite pam_cracklib.so retry=3 difok=3 minlen=10，修改完成后Esc退出编辑模式，按shift+：后输入wq保存退出。

​	difok=3，默认值为10。这个参数设置允许的新、旧密码相同字符的个数，即允许相同字符的个数为3，retry=3改变输入密码的次数，默认值是1。就是说，用户输入的密码强度不够可重试三次；minlen=10，指密码最小长度为10.

```
password    requisite     pam_cracklib.so try_first_pass retry=3 difok=3 minlen=10
```

![](/img/Linuxaqpz/6.png)



设置密码复杂度——在pam_cracklib.so的参数后面附加：ucredit=-1 lcredit=-2 dcredit=-1 ocredit=-1

它表示密码必须至少包含一个大写字母（ucredit），两个小写字母（lcredit），一个数字（dcredit），一个标点符号（ocredit）

```
password    requisite     pam_cracklib.so try_first_pass retry=3 difok=3 minlen=10 ucredit=-1 lcredit=-2 dcredit=-1 ocredit=-1
```

![](/img/Linuxaqpz/7.png)



编辑/etc/pam.d/login 文件，配置pam锁定多次登陆失败的用户，在第一行下即#%PAM-1.0的下面添加：

```
vim /etc/pam.d/login

auth       required     pam_tally2.so deny=3 unlock_time=600 even_deny_root root_unlock_time=120
```

![](/img/Linuxaqpz/8.png)

![](/img/Linuxaqpz/9.png)

3为超过3次，120为锁定2分钟



验证：

​	创建用户test，并赋予密码

​	输入init 3 切换至终端画面，登录用户test进行测试（密码输入错误的，尝试登录3次，账户将被锁定）

​	

​	登录root用户，输入init 5 切换到图形化界面，在root用户下输入pam_tally2 -u test 可查看登录信息



总结：

​	通过修改账户密码最短长度、密码复杂程度、登录认证次数等相关策略，禁止使用前5次设置过的密码防止社会工程学攻击，设置登录3次失败锁定用户防止暴力破解。可实现对账户的进一步保护。



## 配置用户权限

​	变更文件或目录的权限。在UNIX系统家族里，文件或目录权限的控制分别以读取，写入，执行3种一般权限来区分，另有3种特殊权限可供运用，在搭配拥有者与所属群组管理权限范围。您可以使用chmod指令去变更文件与目录的权限，设置方式采用文字或数字代号皆可。符号连接的权限无法变更，如果您对符号连接修改权限，其改变会作用在被连接的原始文件。权限范围的表示法如下：

​		u：User，即文件或目录的拥有者

​		g：Group。即文件或目录的所属群组。

​		o：Other，除了文件或目录拥有者或所属群组之外，其他用户皆属于这个范围。

​		a：All，即全部的用户，包含拥有者，所属群组以及其他用户。

​		r：读取权限，数字代号为”4“

​		w：写入权限，数字代号为”2“

​		x：执行或切换权限，数字代号为”1“。

​		-：不具任何权限，数字代号为”0“。

​		s：特殊?b>功能说明：变更文件或目录的权限。

​		语法：

​			chmod [-cfRv] [--help] [--version] [<权限范围>+/-/=<权限设置...>] [文件或目录...]

​			chmod [-cfRv] [--help] [--version] [数字代号] [文件目录...]

​			chmod [-cfRv] [--help] [--reference=<参考文件或目录>] [--version] [文件或目录...] 选项说明	-c或--changes效果类似”-v“参数，但仅回报更改的部分。

​			-f 或 --quiet 或 --silent 不显示错误信息

​			-R 或 --recursive 递归处理，将指定目录下的所有文件及子目录一并处理。

​			-v 或 --verbose 显示指令执行过程

​			--help	在线帮助。

​			--reference=<参考文件或目录>把指定文件或目录的权限全部设成参考文件或目录的权限相同。

​			--version	显示版本信息。

​			<权限范围>+<权限设置>开启权限范围的文件或目录的该项权限设置。

​			<权限范围>-<权限设置>关闭权限范围的文件或目录的该权限设置。

​			<权限范围>=<权限设置>指定权限范围的文件或目录的该项权限设置。



启动CentOS6.5

打开终端

用户管理——使用命令useradd创建用户user1，user2并通过passwd设置密码：123456，并通过id命令来查看用户。

```
useradd user1
passwd user1
id user1

useradd user2
passwd user2
id user2
```

![](/img/Linuxaqpz/10.png)

![](/img/Linuxaqpz/11.png)

创建用户useradd的几个参数：

​	-c		描述

​	-d		家目录

​	-u		uid号

​	-g		私有组

​	-G		把这个用户附加到其他组中去

​	-s		shell环境变量 /bin/bash /sbin/nologin 它无法登录到本地，远程用户可以。



使用cat命令查看配置文件/etc/passwd，里面记载这所有用户的信息

```
cat /etc/passwd
```

![](/img/Linuxaqpz/12.png)

在/etc/passwd 下，有三种用户：

​	第一种：超级管理员root，uid为0

​	第二种：系统服务用户，uid为1~999

​	第三种：（CentOS7）普通（本地）用户，uid为1000往后

​	CentOS6系统服务用户uid是1-499



使用命令groupadd创建一个test组，并使用gpasswd对这个组设置密码：123456

```
groupadd test
gpasswd test
```

![](/img/Linuxaqpz/13.png)



使用su命令去换到普通用户user1上，把user1加入到test组中。

```
su user1
newgrp test
```

![](/img/Linuxaqpz/14.png)



尝试通过命令ls来查看/root管理员目录，然后通过touch命令在/root目录下创建文件user1，发现user1用户的权限不够，无法打开目录/root。

```
ls /root
ls -ld /root		//-l以详细格式列表 d 仅列目录
touch /root/user1
```

![](/img/Linuxaqpz/15.png)



切换用户root并使用chmod命令/bin/ls、/bin/touch给这两个程序的所有者以suid权限，允许普通用户以root身份暂时执行该程序，并在执行结束后再恢复身份。

```
su root
chmod u+s /bin/ls
chmod u+s /bin/touch
ll /bin/ls
ll /bin/touch

注：ll是ls -l 的别名
```

![](/img/Linuxaqpz/16.png)



切换user1用户使用命令ls、touch再次进行测试，发现可以进行查看和文件写入的操作了。

```
su user1
ls /root
touch /root/test1
ll /root
```

![](/img/Linuxaqpz/17.png)

SUID权限仅仅只对可执行文件（命令文件）有效，对普通文件无意义，只出现在第三位，如果一个可执行文件有SUID权限，那么其它用户在执行这个可执行文件过程时会临时拥有这个可执行文件的所有者权限。



查看/home 目录，发现里面有user2，切换user2用户，然后使用useradd命令创建test2用户提示权限拒绝。

```
ls /home
su user2
useradd test2
```

![](/img/Linuxaqpz/18.png)



通过修改/etc/sudoers 文件，使得user2用户有执行useradd命令的权限，并查看sudoers文件内容。

使用vim命令编辑/etc/sudoers文件，在root ALL=（ALL）ALL一行下面添加user2 ALL=(ALL)，/usr/sbin/useradd，委派user2用户有执行useradd命令的权限，保存并退出（wq!）

```
vim /etc/sudoers
注：记得切换为root用户
```

![](/img/Linuxaqpz/19.png)



修改了/etc/sudoers 文件，赋予了user2有执行useradd命令的权限，我们再来通过用户user2创建新的用户test2，再次提示权限不够。

```
useradd test2
```

![](/img/Linuxaqpz/20.png)



权限委派在执行的时候前面一定要加一个sudo命令，否则是无效的，再前面加上sodu命令来创建。

```
sudo useradd test2
cat /etc/passwd | grep test2
```

![](/img/Linuxaqpz/21.png)

创建用户test2成功，成功委派了用户user2有创建用户的权限。



总结：

​	通过修改用户的读、写、执行等权限，可避免账户权限过高被黑客利用。



# Samba服务的安全配置

## 设置用户账户映射

​	Samba是在Linux和UNIX系统上实现SMB协议的一个免费软件，由服务器及客服端程序构成。SMB（Server Messages Block，信息服务块）是一种在局域网上共享文件和打印机的一种通信协议，它为局域网内的不用计算机之间提供文件及打印机等资源的共享服务。使用虚拟账号登录可以确保LInux用户名不会暴露。



打开CentOS6.5

打开终端输入useradd smbuser 创建一个用户，之后输入smbpasswd -a smbuser 将这个用户加入到samba中

```
useradd smbuser
smbpasswd -a smbuser
```

![](/img/Linuxaqpz/22.png)



在终端输入cd /etc/samba/ 进入到文件夹samba中，输入vim smb.conf对samba配置文件进行编辑

```
cd /etc/samba/
vim smb.conf
```

![](/img/Linuxaqpz/23.png)



在smb.conf文件中添加”user map=/etc/samba/smbusers“开启账户映射后写入并退出。

![](/img/Linuxaqpz/24.png)



对smbuser文件进行编辑，创建用户账户映射”smbuser = test1 test2“，写入并退出
![](/img/Linuxaqpz/25.png)



在终端输入service smb restart 将smb服务重启

```
service smb restart
```

![](/img/Linuxaqpz/26.png)



查看终端IP

![](/img/Linuxaqpz/27.png)



在终端输入smbclient -L 172.16.1.9 -U smbueser%123456，使用本地账户，对smb服务器进行登录测试（账号%密码）

```
smbclient -L 172.16.1.9 -U smbuser%123456
```

![](/img/Linuxaqpz/28.png)



在终端输入smbclient -L 172.16.1.9 -U test1%123456,使用虚拟账户，对smb服务器进行登录测试

```
smbclient -L 172.16.1.9 -U test1%123456
```

![](/img/Linuxaqpz/29.png)

在终端输入smbclient //172.16.1.9/smbuser -U smbuser%123456，使用虚拟账号，对smb服务器进行登录后，输入pwd查看虚拟账号下的本地文件夹路径

```
smbclient //172.16.1.9/smbuser -U smbuser%123456
pwd
```

![](/img/Linuxaqpz/30.png)



总结：

​	通过设置Samba用户账号映射，使用虚拟账号访问服务端。避免服务器用户名的暴露，可实现对Samba服务器的保护。



## 设置主机访问控制

​	针对某些特定用户使用共享资源权限的控制的方法不止一种，主要是对主机进行控制。例如，可以使用IPTables以及PAM。不过Samba服务自身也提供主机访问控制功能。Samba的访问控制通过hosts allow（配置允许访问的客户端）、hosts deny（配置拒绝访问的客户端）两个参数实现。



打开CentOS6.5

打开终端输入ifconfig查看IP

```/
ifconfig
```

![](/img/Linuxaqpz/31.png)



在终端输入vim /etc/samba/smb.conf 进行编辑smb服务器配置

```
vim /etc/samba/smb.conf
```

![](/img/Linuxaqpz/32.png)



在配置界面最低端添加如下，保存并退出。

![](/img/Linuxaqpz/33.png)



在根目录下创建文件夹public，在文件夹中创建文件hello

```
mkdir /public
touch /public/hello.txt
ls /public/
```

![](/img/Linuxaqpz/34.png)



创建一个smb认证用户

```
smbpasswd -a test
注：记得创建用户test
```

![](/img/Linuxaqpz/35.png)



在终端输入service smb restart 将smb服务重启

```
service smb restart
```

![](/img/Linuxaqpz/36.png)



在终端输入smbclient //172.16.1.9/public -U test%123456 登录到smb服务器中，输入ls看目录下文件（账号%密码）

```
smbclient //172.16.1.9/public -U test%123456
```

![](/img/Linuxaqpz/37.png)

如果提示NT_STATUS_ACCESS_DENIED listing \* 那就是被SELIUNX阻挡了

解决方法

输入：

```
setenforce 0
```



在终端输入vim /etc/samba/smb.conf 进行编辑smb服务器配置。

```
vim /etc/samba/smb.conf
```



将hosts allow = 172.16.1.9 删除，保存并退出

![](/img/Linuxaqpz/38.png)



在终端输入service smb restart将smb服务重启

```
service smb restart
```

![](/img/Linuxaqpz/39.png)



在终端输入smbclient //172.16.1.9/public -U test%123456 无法登录

```
smbclient //172.16.1.9/public -U test%123456
```

![](/img/Linuxaqpz/40.png)



总结：

​	使用Samba服务自带的主机访问控制，通过hosts allow（配置允许访问的客户端）、hosts deny（配置拒绝访问的客户端）两个参数。可实现仅部分主机访问Sabma服务的目的。



## 用PAM实现用户和主机访问控制

​	Samba服务器使用完全独立于系统之外的用户认证，这样的好处是可以提高安全性，但同样也带来了一些麻烦，比如修改用户密码时既要修改该用户登录系统的密码，又要修改登录Samba服务器的密码。但通过PAM模块所提供的功能可以有效实现系统用户密码与Samba服务器密码的自动同步。



启动CentOS6.5



创建文件夹myshare，进入smb服务配置文件

![](/img/Linuxaqpz/41.png)



找到[global]添加obey pam restrictions=yes 使主配置文件支持pam认证

![](/img/Linuxaqpz/42.png)



在配置文件最低处添加如图

![](/img/Linuxaqpz/43.png)



在samba认证文件/etc/pam.d/samba中添加Account required pam_access.so accessfile=/etc/mysmblogin保存并退出.

```
vim /etc/pam.d/samba
添加：
account    required     pam_access.so accessfile=/etc/mysmblogin
```

![](/img/Linuxaqpz/44.png)



编辑smb用户登录文件，输入vim /etc/mysmblogin，允许test1在172.16.1.0/24网段访问myshare文件夹，禁止test2在172.16.1.0/24网段访问myshare文件夹。

```
vim /etc/mysmblogin
```

![](/img/Linuxaqpz/45.png)



创建用户test1和test2，并将用户加入共享登陆中。

```
useradd test1
useradd test2
smbpasswd -a test1
smbpasswd -a test2
```

![](/img/Linuxaqpz/46.png)



重启smb服务器及关闭防火墙

```
service smb restart
service iptables stop
```

![](/img/Linuxaqpz/47.png)



查看本机IP

![](/img/Linuxaqpz/48.png)



查看Win7IP

![](/img/Linuxaqpz/49.png)



打开cmd输入\\\172.16.1.9，访问CentOS6.5IP，使用test1和test2测试访问情况

test1正常访问

test2无法访问



总结：

​	Sabma服务可以通过hosts allow、hosts deny对访问的客服端进行控制，也可以使用valid users对访问用户进行控制，但如果希望对特定用户在特定客户端进行控制就必须使用PAM模块。



