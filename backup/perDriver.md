---
title: 'WinToGO在mac电脑上首次配置'
date: 2022-09-26 21:08:03
tags: [Windows,macOS]
published: true
hideInList: false
feature: 
isTop: false
---
此教程不仅适用于Mac,也适用于其他需要预安装驱动的情况

<!-- more -->

# 为什么要预安装驱动?

2016款之后的Mac首次开机会出现屏幕分辨率异常(表现为界面和字都非常小)以及键盘触摸板不能用的情况,这时候就需要借助外置USB键鼠来实现首次设置,装好Boot Camp驱动后才能正常使用.

但如果你在本机用启动转换助理装双系统就会发现,并不需要外置USB键鼠,它会自动重启引导完成Windows的安装,首次设置屏幕分辨率键盘触摸板都是可以正常使用的,开机后再装一下Boot Camp就可以正常使用.

而在制作WTG时预安装驱动的目的就是为了实现和官方装本机双系统一样丝般顺滑的体验.

# 实现原理

使用 [DISM](https://technet.microsoft.com/zh-cn/library/hh825070.ASPX) 脱机添加和删除驱动程序

# 需要提前下载好的东西

Boot Camp驱动,具体如何下载可以看Apple支持社区的[这篇文章](https://support.apple.com/zh-cn/HT204923)

或者你也可以在[这里](https://www.applex.net/pages/bootcamp) 下载Boot Camp驱动

不过个人还是建议在本机macOS里下载,极限苹果那个驱动其实也是有人在本机macOS下载之后传上去的,从哪里下载都可以,但注意一定要是对应版本的.

[Windows To Go 辅助工具](https://bbs.luobotou.org/forum.php?mod=viewthread&tid=761&fromuid=17)


# 具体操作流程

Boot Camp驱动下载好之后就是一个名为`WindowsSupport`的文件夹

然后解压缩我们下载好的最新版WTGA,把刚才那个`WindowsSupport`文件夹里的名为`$WinPEDriver$`的文件夹里的内容全选并复制**注意要复制,不要剪切,因为后面进WTG系统后还要再装一遍完整驱动**

粘贴到到解压好的WTGA的`Drivers`文件夹内.

**苹果电脑请使用识别为本地磁盘的设备制作WTG,建议使用传统模式,勾选UEFI+GPT选项,其他选项默认不用动即可**

点击`部署`按钮,静待WTG制作完成.然后把整个`WindowsSupport`文件夹拷贝到制作好的WTG盘内.

到Mac开机按住⌥选择`EFI Boot`正常完成首次启动设置,进桌面后手动点击刚刚拷贝进去的`WindowsSupport`文件夹里的`BootCamp`文件夹里的`Setup.exe`,安装剩余驱动程序.

大功告成