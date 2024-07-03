---
title: '按照过期操作教程的危害'
date: 2022-09-26 15:33:25
tags: [knowledge]
published: true
hideInList: false
feature: 
isTop: false
---

单位服务器是CentOS6.8

安装之后第一步就是更换为国内源

按照镜像站的教程

直接wget

设置完后下载什么都报错404

再去国内任何一个程序员网站

CSDN 博客园什么的

都是一模一样的操作

最后还是在stack overflow上看到了正解

>centos6已经被废弃,官方已经不提供软件源,国内这些镜像站无脑复制直接一并变成空白,repo为空自然下载什么都404
>>解决方法是使用centos7的安装源

# 更换为阿里源报错类似
```shell
http://mirrors.aliyun.com/centos/6/os/x86_64/repodata/repomd.xml: [Errno 14] PYCURL ERROR 22 - "The requested URL returned error: 404 Not Found"
Trying other mirror.
http://mirrors.aliyuncs.com/centos/6/os/x86_64/repodata/repomd.xml: [Errno 14] PYCURL ERROR 7 - "couldn’t connect to host"
Trying other mirror.
http://mirrors.cloud.aliyuncs.com/centos/6/os/x86_64/repodata/repomd.xml: [Errno 14] PYCURL ERROR 6 - "Couldn’t resolve host ‘mirrors.cloud.aliyuncs.com’"
Trying other mirror.
Error: Cannot retrieve repository metadata (repomd.xml) for repository: base. Please verify its path and try again
```
# 解决方案
```shell
cd /etc/yum.repos.d
vi CentOS-Base.repo
:%s/$releasever/7/g #将文件中$releasever全部改成7
yum clean all && yum makecache #清除和缓存
```

国内这些所谓的教程网站能不能顺便发一下教程的发布时间?
