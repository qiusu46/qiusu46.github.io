---
title: Linux基础命令
tags:
  - 基础命令
  - Linux
  - Kali
categories: 
  - Linux
  - 基础
keywords: 
  - 基础
  - Linux
  - Kali
cover: 'https://www.helloimg.com/images/2021/11/03/CYeHwK.jpg'
abbrlink: 60189
---



# Linux基础命令



### ls命令

```
ls		查看目录下所有文件
ls xxx	查看xxx下所有文件
ls -a	查看所有文件包括隐藏文件
ls -l	列出文件详细信息
```

### pwd命令

```
pwd		显示出用户当前所在目录
```

### cd命令

```
cd 目录名	改变工作目录
cd..		返回上级目录
cd~			返回家目录

注：
/			根目录
.			当前目录
..			返回上级目录

以/为开头的称为绝对路径
以.或...开头的称为相对路径
```

### touch命令

```
touch xxx.xx	新建一个文本或以.xx为后缀的文本
```

### mkdir命令

```
mkdir xxx		新建一个文件夹
```

### rm命令

```
rm xxx			删除xxx文件
rm -rf			删除目录下所有文件（-f即使为只读文件亦直接删除）
```

### cp命令

```
cp 源文件或目录 目标文件或目录			复制文件或目录
```

### mv命令

```
mv 源文件或目录 目标文件或目录			重命名
mv 移动的文件 目标路径				移动文件
```

### cat命令

```
cat xxx.xx		查看文件
```

### ifconfig命令

```
ifconfig		查看IP
```

### find命令

```
find 要查找的文件或目录		查找文件或目录
```

### gzip命令

```
gzip 文件名			压缩
gzip -d 压缩文件.gz		解压
```

### unzip命令

```
unzip 压缩文件.zip			解压
unzip -v 压缩文件.zip		查看压缩文件
```

### vim命令

```
vim xxx.xx		编辑文件

进入按i编辑，按esc退出编辑，shitf+: 输入wq保存退出，输入w保存，输入q退出不保存，输入q！强制退出
```

### 切换用户

```
su 用户名
```

### 创建用户

```
useradd 用户名
```

### 更改用户密码

```
passwd
```

