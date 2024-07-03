---
title: '用启动盘安装 Windows 10'
date: 2022-09-26 19:42:38
tags: [Windows]
published: true
hideInList: false
feature: 
isTop: false
---
首先声明,这是不带任何推广软件和广告的原版系统,不要认为那些一键装系统的软件真的好心让你免费一键装系统,基本上的套路都是捆绑主页,你打开一次他挣两分钱,各种流氓管家卸不掉,各种必要的运行库和系统功能精简掉,如果你真觉得这些你都不在乎,可以线下来问问我还有什么,因为这是大部分人的利益,说出来断了大家财路.
安装原版系统自然会比盗版系统花费的时间长,这也是为什么电脑店的奸商不给你装正版的原因

言归正传,进入正题
要制作一个可启动的U盘,制作方法在[另一篇blog](https://zhangyiming748.github.io/post/make_bootable_disk/)

制作好启动盘之后,以下是单项选择题,三个启动U盘的方法你选择其中一个:
1. 可以通过电脑上的快捷启动按键来启动你的U盘.(常见F12)
(就是在按下电源键的时候一直敲敲敲敲,一直敲敲敲就可以出现可启动设备的选项,然后选择U盘来启动)
你的u盘名字带有uefi前缀就是用uefi方式启动
没有前缀就是legacy

主板启动方式|应该选择的分区类型|应该选择的目标系统类型
---|:--:|---
UEFI|GPT|UEFI(非CSM)
Legacy|MBR|BIOS(或UEFI-CSM)

2. 通过在BIOS设置,把U盘设为第一启动设备,插上U盘开机的话会自动启动你的U盘而不是电脑上的硬盘.
{由于不同主板的快捷启动按键不一样,BIOS的设置也不一样,没有办法一个个主板说,具体启动方法根据你的主板型号去百度查(如果觉得百度太麻烦,可以根据电脑品牌去官网找客服问快捷启动按键或者BIOS设置方法,客服就是用来麻烦的)
3. 按住shift键重启电脑,会出现启动USB的选项,然后选择USB启动

----
当你成功启动U盘的时候,会出现操作系统的安装界面,就可以开始安装你的操作系统了

![1](https://s1.ax1x.com/2022/09/05/vT6LHP.png)


![2](https://s1.ax1x.com/2022/09/04/vTVShR.png)

![3](https://s1.ax1x.com/2022/09/04/vTEj74.png)

![4](https://s1.ax1x.com/2022/09/04/vTEXBF.png)

![5](https://s1.ax1x.com/2022/09/04/vTExAJ.png)

![6](https://s1.ax1x.com/2022/09/05/vT6qBt.png)

关于磁盘分区的弊端,以前的blog应该有,自己去看,而且不论你多么想分区,都不要在这里分区,进系统之后再分

![7](https://s1.ax1x.com/2022/09/04/vTEzN9.png)

如果shift+F10不好使就试试Fn+shift+F10,有些主板默认Fn反转

![8](https://s1.ax1x.com/2022/09/05/vT6XAf.png)

然后关掉黑色这个窗口,点刷新,然后选中你要装系统的那个磁盘,点下一步
就会开始安装操作系统了

![9](https://s1.ax1x.com/2022/09/04/vTEOnU.png)

现在不拔也行,重启之前拔掉就行
然后电脑会自动重启,然后会出现很多设置,自己选择自己喜欢的设置,然后就安装完成了!

补发,安装过程中添加硬盘驱动的方法(常见于第一代nvme固态)

<iframe width="560" height="315" src="https://www.youtube.com/embed/dkQ8UHk_f5I" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>