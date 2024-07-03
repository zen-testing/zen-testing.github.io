---
title: '使用uupdump获取原版Windows镜像'
date: 2022-09-26 19:27:30
tags: [Windows]
published: true
hideInList: false
feature: 
isTop: false
---

[网站地址](https://uupdump.net/)

+ 0x01
搜索你要下载的版本,或者直接在下方点击
![1](https://s1.ax1x.com/2022/09/05/vT6Nmq.png)
+ 0x02
比如这里我们搜索`Windows 10 21H2`(这个网站的分词器好像有问题)
![2](https://s1.ax1x.com/2022/09/05/vT6U00.png)
+ 0x03
找到你需要的版本和架构,点进去
![3](https://s1.ax1x.com/2022/09/05/vT6YXn.png)
+ 0x04
选择你需要的版本,点击下一步
![4](https://s1.ax1x.com/2022/09/05/vT6J6s.png)
+ 0x05
下载方式选择下载并转换,转换选项都不要选,然后点击创建下载包,解压并打开
![5](https://s1.ax1x.com/2022/09/05/vT6Glj.png)
+ 0x06
右键用你喜欢的编辑器打开下载程序(只编辑当前系统版本对应的文件就行),在16行附近有`set "all_proxy="`字样可以添加你喜欢的代理服务加速下载进程
![6](https://s1.ax1x.com/2022/09/05/vT68pQ.png)
+ 0x07
开始下载
```shell
Windows:双击运行批处理文件
Linux:chmod +x uup_download_linux.sh && ./uup_download_linux.sh
Darwin:chmod +x uup_download_macos.sh && ./uup_download_macos.sh
```
![7](https://s1.ax1x.com/2022/09/05/vT61fg.png)
+ 0x08
下载成功后按0退出
![8](https://s1.ax1x.com/2022/09/05/vT6Qk8.png)
+ 0x09
下载好的ISO文件保存在当前目录下
![9](https://s1.ax1x.com/2022/09/05/vT61fg.png)