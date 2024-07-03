---
title: ' 小米平板6pro 通用Root教程'
date: 2024-05-03 17:26:46
tags: [xiaomi,Magisk]
published: true
hideInList: false
feature: 
isTop: false
---
> 首发冲的小米平板6pro等了7天后终于可以解锁了，这意味这可以安装Magisk来获取Root权限了。解bootloader锁 安装Magisk最重要的就是使用Fastboot刷入Magisk修补后的Boot文件这和Magisk的工作原理有关，感兴趣可以去百度看看。 这意味这我们首先需要拿到Boot文件才能使用Magisk修补，寻找官方Boot文件的方法一般是去下载小米的官方Room，这里我推荐  [这个网站](XiaomiROM.com)，以小米平板6pro为例，搜索《小米平板6》，点击小米平板6pro

    首发冲的小米平板6pro等了7天后终于可以解锁了，这意味这可以安装Magisk来获取Root权限了。

![](https://i0.hdslb.com/bfs/article/51e32934c54416f9ce0ee6adcc1e6bd39039563e.png@1256w_858h_!web-article-pic.avif)

解bootloader锁

    安装Magisk最重要的就是使用Fastboot刷入Magisk修补后的Boot文件这和Magisk的工作原理有关，感兴趣可以去百度看看。

    这意味这我们首先需要拿到Boot文件才能使用Magisk修补，寻找官方Boot文件的方法一般是去下载小米的官方Room，这里我推荐 XiaomiROM.com  这个网站，以小米平板6pro为例，

搜索`小米平板6`，点击小米平板6pro

从这里可以看出小米平板6pro目前公开发布的Rom数量，如果手机当前MIUI版本是稳定版，选择Fastboot线刷包，**下载与手机版本对应的Rom**即可。  
下载完成后使用解压软件解压两遍，这里我使用《7z》解压软件示例。  
我们只需要images文件夹里面的boot.img文件就行  

boot.img

把他复制出来，我这边是改了个名字，做个标记。

在需要刷入Magisk的设备上安装Magisk App（Magisk apk下载地址可以去Magisk作者topjohnwu Github的Magisk仓库的[Release页面](https://github.com/topjohnwu/Magisk/releases)下载最新

手机用数据线连接电脑，手机上开启传输文件模式，把下面的Magisk apk文件和上面提到的boot.img放到手机根目录下的Download文件夹里面（方便查找）。

Magisk App apk

接下来视角转到安装了Magisk App的设备，打开文件管理，点击`内部存储`，找到点击Download文件夹，点击Magisk.apk进行安装，打开应该是这样子的：

Magisk App首页

    接下来我们点击安装，点击选择并修补一个文件，在这里点击最左上角的三条杠，点击下载内容，在这里我们可以看到之前上传的boot.img，点击这个文件，再点击开始，Magisk就会修补boot，在输出日志中，我们需要记住Output file也就是输出文的路径，下面是gif，

![](https://i0.hdslb.com/bfs/article/091c91930f3147da6bbdd3a3f17646a725675e0c.jpg@1256w_2010h_!web-article-pic.avif)
`fastboot flash boot_ab `
然后在`boot_ab`后面敲一个空格，然后找到从手机上复制出来的Magisk修补后的boot文件，右键复制，回到powershell窗口，粘贴，然后敲击回车，等待一会出现如下图就说明刷入成功。
输入
`fastboot reboot`
敲击回车，等待手机重启到系统，打开Magisk，在Magisk下面出现《当前 26.1(26100)》则说明手机成功刷入Magisk，成功获得Root权限，接下来就可以去删温控或者玩Magisk模块了。
**小米13要修补的文件是init_boot**