---
title: Web渗透-暴力破解篇
tags:
  - Web
  - 渗透
  - 暴力破解
categories:
  - Web渗透
  - 暴力破解
keywords:
  - Web
  - 渗透
  - 暴力破解
cover: >-
  https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fi0.hdslb.com%2Fbfs%2Farchive%2Fbfc8e28218391fd0ca664c39ebae4546ed4bf074.jpg&refer=http%3A%2F%2Fi0.hdslb.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1638786487&t=e863dcba2240b3835c788db80f551a50
abbrlink: 900417ac
---









# Web渗透-暴力破解

## 基于表单的暴力破解

使用工具：Burp

Burp使用教程：[Burp使用教程](https://blog.csdn.net/qq_41703976/article/details/111826950?ops_request_misc=&request_id=&biz_id=&utm_medium=distribute.pc_search_result.none-task-blog-2~all~es_rank~default-1-111826950.pc_search_all_es&utm_term=burp%E4%BD%BF%E7%94%A8%E6%95%99%E7%A8%8B&spm=1018.2226.3001.4187)

#### 第一步

开启火狐浏览器的代理

![](https://www.helloimg.com/images/2021/11/06/CfdwCP.png)



#### 第二步

打开Burp开启拦截

![](https://www.helloimg.com/images/2021/11/06/CfdNwn.png)



#### 第三步

在页面的Username和Password输入框中随便输入内容，回车

![](https://www.helloimg.com/images/2021/11/06/Cfdlfv.png)

![](https://www.helloimg.com/images/2021/11/06/Cfdd7M.png)



#### 第四步

右键点击 Send to Intruder

![](https://www.helloimg.com/images/2021/11/06/CfdWU9.png)



#### 第五步

选择username和password参数内容

![](https://www.helloimg.com/images/2021/11/06/CfdOPX.png)



#### 第六步

添加用户名和密码字典（网页用户名和密码为admin和123456，由于时间长我就直接把正确用户和密码都加在字典第一个）



用户字典选择username

![](https://www.helloimg.com/images/2021/11/06/Cfd2qE.md.png)



密码字典选择password

![](https://www.helloimg.com/images/2021/11/06/CfdTTY.png)



#### 第七步

执行，可以看到破解出来的Length会和用户密码错误的不一样

![](https://www.helloimg.com/images/2021/11/06/Cfdcng.png)



## 验证码绕过（on server）

#### 第一步

输入用户名、密码和验证码（验证码要输正确，记得拦截）

![https://www.helloimg.com/images/2021/11/06/Cfdk4q.png](https://www.helloimg.com/images/2021/11/06/Cfdk4q.png)

![](https://www.helloimg.com/images/2021/11/06/Cfdrwr.png)



#### 第二步

右键点击 Send to Intruder

![](https://www.helloimg.com/images/2021/11/06/CfdgCc.png)



#### 第三步

一样选择参数，然后执行

![https://www.helloimg.com/images/2021/11/06/CfdVhT.png](https://www.helloimg.com/images/2021/11/06/CfdVhT.png)

![](https://www.helloimg.com/images/2021/11/06/CfdK7h.png)



## 验证码绕过（on client）

和on server一样，不多BB了



## token防爆破

#### 第一步

一样输入用户和密码拦截

![](https://www.helloimg.com/images/2021/11/06/CfNebb.png)



#### 第二步

还是一样选择3个参数

![](https://www.helloimg.com/images/2021/11/06/CfNXaK.png)



#### 第三步

依次点击

![](https://www.helloimg.com/images/2021/11/06/CfNPxr.png)

![](https://www.helloimg.com/images/2021/11/06/CfNa9T.png)



点击OK，记得复制token

Redirections选择Always

![](https://www.helloimg.com/images/2021/11/06/CfNEGD.png)



#### 第四步

用户和密码一样添加字典，token参数在Payload type选择Recursive grep，在红框粘贴刚才复制的token

![](https://www.helloimg.com/images/2021/11/06/CfNqIo.png)



#### 第五步

设置线程为1，执行

![](https://www.helloimg.com/images/2021/11/06/CfNJAS.png)

![](https://www.helloimg.com/images/2021/11/06/CfN1k1.png)