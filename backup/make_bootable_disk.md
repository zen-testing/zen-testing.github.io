---
title: '用Rufus不费脑制作启动盘'
date: 2022-09-26 17:39:36
tags: [Windows]
published: true
hideInList: false
feature: 
isTop: false
---

<iframe width="560" height="315" src="https://www.youtube.com/embed/eWowF40_pDs" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

之前写过使用软碟通制作启动盘的教程,但毕竟那是个正版收费的软件,估计王涛也觉得自己很冤,又因为之前写的软碟通的教程只适用在Windows平台,如果想做Linux甚至Macos需要手动更改的地方太多,不是一种大众的等级,所以又写了这个用[Rufus](https://rufus.ie/)制作启动盘的教程

### 下载Rufus
在浏览器上搜索Rufus,如果用Google,第一个搜索结果就是,其它搜索引擎就不一定了

![1](https://s1.ax1x.com/2022/09/04/vTEDkd.png)

进入官网,这个官网外观很特别,外观不像的网站就是你找错了

![2](https://s1.ax1x.com/2022/09/04/vTE6pt.png)

找到下载的位置,前两个都可以,没啥区别

![3](https://s1.ax1x.com/2022/09/04/vTE2X8.png)

### 安装

下载完了直接双击打开就能用

![4](https://s1.ax1x.com/2022/09/04/vTE0TH.png)

如果是首次安装运行的话,会询问你是否联网更新,选`否`就行,大家都懂

![5](https://s1.ax1x.com/2022/09/04/vTEsfI.png)

### 设置参数

![6](https://s1.ax1x.com/2022/09/04/vTErtA.png)

**设备** 选择你的U盘/内存卡,总之选择你要制作为系统盘的磁盘

**引导类型** 选择你下载的系统镜像(镜像可以去[msdn.itellyou.cn](https://msdn.itellyou.cn)下载,**站长只是收集了微软官方的下载链接,然而有些人用了带广告的PE安装原装系统,反咬这位站长一口,真替他喊冤**)

**镜像选项** 只在你选择Windows10或Windows8.x的时候才会出现,选择标准安装就行,Windows To Go 是安装系统到U盘上运行的

**目标系统类型** 和 **分区类型** 的对应关系如下

主板启动方式|应该选择的分区类型|应该选择的目标系统类型
---|:--:|---:
UEFI|GPT|UEFI(非CSM)
Legacy|MBR|BIOS(或UEFI-CSM)

**剩下的参数不要动就**,有疑问私聊

### 制作

参数确定后点击`开始`就会开始制作

进度条跑完就制作完成了

![7](https://s1.ax1x.com/2022/09/04/vTEc1P.png)

----

看似三步,实际上手动操作的时间加起来也就喝口咖啡的时间.选择Rufus的另一个原因就是它可以在你安装小众Linux发行版的时候自动下载引导文件,不过既然你都会安装Linux了,这软件对你来说就太小儿科了

**以上内容同样适用于制作Linux的LiveCD,但是并不建议这么做**
