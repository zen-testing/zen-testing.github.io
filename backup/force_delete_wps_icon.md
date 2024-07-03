---
title: '强制删除WPS绑架在此电脑窗口上的云服务图标'
date: 2022-09-26 16:31:10
tags: [Windows]
published: true
hideInList: false
feature: 
isTop: false
---

---
在安装WPS2019/2016后,会在"此电脑"中创建一个云同步的图标,与本地磁盘并列在一起

<!-- more -->

官方提供的取消逻辑是:

进入这个云服务
在右上角选择设置
取消显示在我的电脑

而这个很严重的漏洞在于:

取消显示这个操作是需要重启云服务的
但是重启的优先级是大于这个设置的
导致在没有更改过来设置之前就已经重启了

我不知道金山这么做是想留住用户还是把用户推向Microsoft office

我觉得接下来介绍的操作比起安装完整版office2016来会更难,如果不看教程的话

但是有多少人会迎难而上金山你们没考虑过吗?
或者不会这个技巧的人有没有可能直接卸载投入微软怀抱?

你不仁,别怪我不义
----


**方法如下**
 

1. 打开`计算机\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\MyComputer\NameSpace`这里面应该会有一些类似于这样`{2107F2C2-1AFA-1744-BCCA-59912CCCA6DC}`的UUID项
找到其中所有内容为`WPS`的项,记录下来(先别着急删)
 
2. 在`计算机\HKEY_LOCAL_MACHINE\SOFTWARE\Classes\CLSID\`中所搜您刚才记录下来的每一个UUID项,并将这些项删除(仔细搜搜,应该都有的)
 
3. 最后返回`HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\MyComputer\NameSpace`删除之前找到的所有内容为`WPS`的项
 
4. 刷新一下`此电脑`,快捷方式应该都消失了

**进阶方法**

直接第三步,每个UUID复制到记事本上,前面添加`shell:::`,如`shell:::{ED7BA470-8E54-465E-825C-99712043E01C}`

复制这个条目到`运行`中执行

打开了什么程序/文件夹那么这条UUID就代表了什么

这么做虽然很费力

但是也有好的方面

说不定就顺便打开了以前不知道的一些功能

比如`完全控制面板`

假设你在`运行`中执行了`shell:::{ED7BA470-8E54-465E-825C-99712043E01C}`后打开了完全控制面板觉得很好用要保留下来

那么只需要在你想运行的地方新建一个文件夹重命名为`文件名.{ED7BA470-8E54-465E-825C-99712043E01C}`就会有~~三百万个基佬向你冲过来~~新的图标产生

而且这种文件夹还有特殊的用途