---
title: MySQL基本语句
tags:
  - MySQL
categories:
  - MySQL
keywords:
  - MySQL
cover: https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fpic.16pic.com%2F00%2F13%2F46%2F16pic_1346579_b.jpg&refer=http%3A%2F%2Fpic.16pic.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1640745298&t=d82f7a7c6653dd081875b7175382d1cd
abbrlink: 1
---







## 简介

PHP 在开发 Web 站点或一些管理系统时，需要对大量的数据进行保存，虽然 XML 文件或者文本文件也可以作为数据的载体，但不易进行管理和对大量数据的存储，所以在项目开发时，数据库就显得非常重要。

PHP 可以连接的数据库种类较多，其中 MySQL 数据库与其兼容较好，在 PHP 数据库开发中被广泛地应用。



## MySQL特点

下面总结了一下 MySQL 具备的特点。

#### 1) 功能强大

MySQL 中提供了多种数据库存储引擎，各引擎各有所长，适用于不同的应用场合，用户可以选择最合适的引擎以得到最高性能，可以处理每天访问量超过数亿的高强度的搜索 Web 站点。MySQL5 支持事务、视图、存储过程、触发器等。

#### 2) 支持跨平台

MySQL 支持至少 20 种以上的开发平台，包括 Linux、Windows、FreeBSD 、IBMAIX、AIX、FreeBSD 等。这使得在任何平台下编写的程序都可以进行移植，而不需要对程序做任何的修改。

#### 3) 运行速度快

高速是 MySQL 的显著特性。在 MySQL 中，使用了极快的 B 树磁盘表（MyISAM）和索引压缩；通过使用优化的单扫描多连接，能够极快地实现连接；SQL 函数使用高度优化的类库实现，运行速度极快。

#### 4) 支持面向对象

PHP 支持混合编程方式。编程方式可分为纯粹面向对象、纯粹面向过程、面句对象与面向过程混合 3 种方式。

#### 5) 安全性高

灵活和安全的权限与密码系统，允许基本主机的验证。连接到服务器时，所有的密码传输均采用加密形式，从而保证了密码的安全。

#### 6) 成本低

MySQL 数据库是一种完全免费的产品，用户可以直接通过网络下载。

#### 7) 支持各种开发语言

MySQL 为各种流行的程序设计语言提供支持，为它们提供了很多的 API 函数，包括 PHP、ASP.NET、Java、Eiffel、Python、Ruby、Tcl、C、C++、Perl 语言等。

#### 8) 数据库存储容量大

MySQL 数据库的最大有效表尺寸通常是由操作系统对文件大小的限制决定的，而不是由 MySQL 内部限制决定的。InnoDB 存储引擎将 InnoDB 表保存在一个表空间内，该表空间可由数个文件创建，表空间的最大容量为 64TB，可以轻松处理拥有上千万条记录的大型数据库。

#### 9) 支持强大的内置函数

PHP 中提供了大量内置函数，几乎涵盖了 Web 应用开发中的所有功能。它内置了数据库连接、文件上传等功能，MySQL 支持大量的扩展库，如 MySQLi 等，可以为快速开发 Web 应用提供便利。




## MySQL基本语句

```
service mysqld start		启动mysql
service mysqld stop			停止mysql
service mysqld restart		重启mysql
mysql -h IP -u 用户名 -p密码			连接数据库
select version();			查看mysql版本号
create database 库名;			创建数据库
show databases;				查看所有数据库
show create database 库名;		查看指定数据库
use 数据库名;				 使用数据库
drop database 数据库;		删除数据库
create table 表名(列名 数据类型[not null] [primary key],列名 数据类型[not null],...)
show tables;				查看所有表
rename table 旧表明 to 新表名;	修改表名
select * from 表名		进入表

create user 用户名 identified by '密码';		添加用户
update user set user='新用户' where user='旧用户';		修改用户
update user set password=password('新密码') where user='用户名';		修改密码
update user set password=md5(password) where user='用户名';		使用md5加密密码
drop user '用户'@'host';		删除用户
show grants for '用户';		查看用户权限
select * from 数据库.user where user='用户名'\G;		查看用户权限
flush privileges;			刷新SQL
grant 权限 on 数据库名.表名 to '用户'@'host';		添加或修改权限
revoke privilege on 数据库名.表名 from '用户名'@'host';		撤销权限
select host,user from user;			查看用户
select password from user where user='用户名';			查看密码
update user set host='%' where user='用户名';		修改用户host

Mysql5.7及以上没有password字段，应替换成authentication_string
select authentication_string from user where user='用户名';		查看密码
```



## 一些实例演示

```
//查看版本号
select version();
```

![](https://www.helloimg.com/images/2021/11/29/GPtGph.png)



```
//查看所有数据库
show databases;
```

![](https://www.helloimg.com/images/2021/11/29/GPtXKb.png)





```
//查看指定数据库
show create database dvwa;
```

![](https://www.helloimg.com/images/2021/11/29/GPtLev.png)



```
//创建数据库
create database test;
```

![](https://www.helloimg.com/images/2021/11/29/GPtWv6.png)



```
//删除数据库
drop database test;
```

![](https://www.helloimg.com/images/2021/11/29/GPt9fn.png)



```
//查看表
show tables;
```

![](https://www.helloimg.com/images/2021/11/29/GPt0P5.png)



```
//进入表
select * from users;
```

![](https://www.helloimg.com/images/2021/11/29/GPtNn0.png)



```
//创建用户名、查看用户
create user test identified by '123456';
select user from user;
```

![](https://www.helloimg.com/images/2021/11/29/GPt7tc.png)



```
//修改用户名
update user set user='test1' where user='test';
```

![](https://www.helloimg.com/images/2021/11/29/GP4BWv.png)



```
//查看密码、修改密码
select password from user where user='test1';			#查看用户密码
update user set password=('test') where user='test1';		#不使用md5加密
update user set password=md5(password) where user='test1';		#使用md5加密
注：mysql5.7以上版本password要换成authentication_string
```

![](https://www.helloimg.com/images/2021/11/29/GP4OAS.png)





```
//添加用户权限
select * from user where user='test1'\G;		#查看权限
grant select,update on *.* to 'test1';		#添加权限，*.*表示所有数据库和表
```

![](https://www.helloimg.com/images/2021/11/29/GP48NM.png)

![](https://www.helloimg.com/images/2021/11/29/GP4kOn.png)



```
//删除用户
drop user test1;
```

![](https://www.helloimg.com/images/2021/11/29/GPAlmP.png)



![](https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fc-ssl.duitang.com%2Fuploads%2Fitem%2F202003%2F10%2F20200310161151_jensw.thumb.400_0.gif&refer=http%3A%2F%2Fc-ssl.duitang.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1640744936&t=92c7f08864d0a6edf6979216fae11bc3)
