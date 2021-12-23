---
title: Pikachu靶场SQL-Inject（数字型-XX型注入）
tags:
  - 渗透
  - SQL注入
  - 注入
  - 靶场
categories:
  - Web渗透
  - SQL注入
keywords:
  -	渗透
  - SQL
  - 注入
  - SQL注入
  - 靶场
cover: >-
  https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fcdn.scratch.mit.edu%2Fstatic%2Fsite%2Fprojects%2Fthumbnails%2F2442%2F9239.png&refer=http%3A%2F%2Fcdn.scratch.mit.edu&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1638842520&t=11b98537860cb678e8c79da91d2b5b1b
abbrlink: cd80b560
---







# Pikachu靶场SQL-Inject

## 数字型注入（post）

打开网页，选择SQL-Inject（Post）

点击了解get和post的区别：[get和post区别](https://zhidao.baidu.com/question/87535798.html)

按F12键，选择Network，F5刷新

![](https://www.helloimg.com/images/2021/11/07/CfjkK5.png)



选择查询的值，例如1

![](https://www.helloimg.com/images/2021/11/07/CfjVo0.png)



当点击查询时会发现Network会被刷新，这是我们点击sqli_id.php查看post提交的值

![](https://www.helloimg.com/images/2021/11/07/Cfjj5c.png)



我们打开接口测试工具或者百度查找接口测试的在线网站都可以（建议火狐浏览器有插件可以直接看页面不用看源码）

选择Post，在提交数据输入id:1和submit:查询  

一个数据一行

![](https://www.helloimg.com/images/2021/11/07/Cfjusq.png)



接下来判断注入

不知道怎么判断点击：[MySQL注入](http://suqu46.cn/fengye/7d3b4823.html)

![](https://www.helloimg.com/images/2021/11/07/Cfjydr.png)

![](https://www.helloimg.com/images/2021/11/07/CfuG2K.png)



从上一步判断出页面存在数字型注入（这个是废话题目不写着吗）

![](https://img1.baidu.com/it/u=2361767060,2242395012&fm=26&fmt=auto)

由此我们可以继续下一步，判断他的字段

![](https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fpic3.zhimg.com%2F50%2Fv2-44b615cd5a141988fb81bd22e75478fc_hd.jpg&refer=http%3A%2F%2Fpic3.zhimg.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1638839272&t=b0e77ca9a434d645330dcf7b2922d339)

![](https://www.helloimg.com/images/2021/11/07/Cfu5YT.png)

![](https://www.helloimg.com/images/2021/11/07/CfuCe1.png)



从上图中得知有两个字段（好吧这个也是废话）

![](https://img2.baidu.com/it/u=3203424084,185363387&fm=26&fmt=auto)

接下来还是下一步，查询字段属性

![](https://www.helloimg.com/images/2021/11/07/CfuRKb.png)



解释一下这里为什么就变成鸭蛋了不是油条了

因为鸭蛋没有返回数据，油条有

从上图可以看到返回数据有个2，那么接下来就要用到2了

![](https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fc-ssl.duitang.com%2Fuploads%2Fitem%2F202003%2F27%2F20200327121610_urrfl.thumb.400_0.jpg&refer=http%3A%2F%2Fc-ssl.duitang.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1638839767&t=33bf0e79dde53577e572b3fd2145021e)

查看数据库

![](https://www.helloimg.com/images/2021/11/07/CfuoFo.png)



然后我们就知道了数据库为pikachu

下一步就查表和字段

![](https://www.helloimg.com/images/2021/11/07/CfuPzS.png)

![](https://www.helloimg.com/images/2021/11/07/CfuFiD.png)



最后是内容

![](https://www.helloimg.com/images/2021/11/07/Cfu3sQ.png)



你以为就这样结束了？

![](https://img0.baidu.com/it/u=2301824158,2209520009&fm=253&fmt=auto&app=138&f=JPEG?w=198&h=182)

![](https://www.helloimg.com/images/2021/11/07/Cfu1BC.png)

这才是最后的答案（其实我不能说我一开始就没做好，不过也都是一样就是比较麻烦）

```
1 or 1=1
```

or 是或

and 和

都是可以去判断是否注入的（其实是最后百度看了一下才知道做错了）



## 字符型注入（get）

好了，接下来是get方式

这个就简单了

![](https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fimg0.pconline.com.cn%2Fpconline%2F1409%2F16%2F5440758_4685585_301_thumb1_thumb.jpg&refer=http%3A%2F%2Fimg0.pconline.com.cn&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1638840476&t=38d30586eccbe367a797b88f6eb972d3)

根据题目我们知道他是一个字符型注入

所以直接上图片

![](https://www.helloimg.com/images/2021/11/07/Cfjg2A.png)

![](https://www.helloimg.com/images/2021/11/07/Cfjfph.png)

好了结束

and和or都自己试一下

点击链接字符型注入：[字符型注入](https://zhuanlan.zhihu.com/p/23899464)

```
1' or 1=1#
```



## 搜索型注入

看到这个题目其实我也不会的

![](https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fc-ssl.duitang.com%2Fuploads%2Fitem%2F202002%2F15%2F20200215020116_hH833.thumb.400_0.gif&refer=http%3A%2F%2Fc-ssl.duitang.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1638841010&t=9c238a8e93bc7e134760a940b93b0166)

所以我点了提示

提示是%%

所以猜测应该是‘%查询内容%’

构造语句

```
xxx%' or 1=1#
```

![](https://www.helloimg.com/images/2021/11/07/Cfuxev.png)



## XX型注入

一样点击提示

构造一个闭合

那就构造一个闭合

![](https://img0.baidu.com/it/u=2844394520,4017554188&fm=253&fmt=auto&app=138&f=JPEG?w=200&h=192)

构造语句

```
xx') or 1=1#
```

![](https://www.helloimg.com/images/2021/11/07/CfueYu.png)

然后就先结束吧，懒，等有时间在继续。

![](https://img2.baidu.com/it/u=1765999030,3540847987&fm=26&fmt=auto)

