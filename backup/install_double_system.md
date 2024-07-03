---
title: 'Windows 下安装双系统的教程'
date: 2022-09-26 17:13:34
tags: [双系统,Windows]
published: true
hideInList: false
feature: 
isTop: false
---

为了模拟真实的使用情况

这里先使用全部硬盘空间安装Windows系统

![1](https://raw.githubusercontent.com/zhangyiming748/blog_image/master/double_system/1.webp)

按照正常流程安装Windows

![2](https://raw.githubusercontent.com/zhangyiming748/blog_image/master/double_system/2.webp)

进入系统后右键开始按钮选择磁盘管理

![3](https://raw.githubusercontent.com/zhangyiming748/blog_image/master/double_system/3.webp)

右键Windows所在分区选择`压缩卷`

![4](https://raw.githubusercontent.com/zhangyiming748/blog_image/master/double_system/4.webp)

通常Linux系统最小需要20G空间用来保证正常运行

![5](https://raw.githubusercontent.com/zhangyiming748/blog_image/master/double_system/5.webp)

在上图填上你喜欢的数字,比如30000,然后会是这样

![6](https://raw.githubusercontent.com/zhangyiming748/blog_image/master/double_system/6.webp)

这时插入另一个Linux系统的安装盘,然后重启

### 小技巧

Windows下按住左边shift点击重启会直接进入Windows RE环境

![7](https://raw.githubusercontent.com/zhangyiming748/blog_image/master/double_system/7.webp)

进入界面后选择使用设备

![8](https://raw.githubusercontent.com/zhangyiming748/blog_image/master/double_system/8.webp)

设备选择你自己制作的系统盘

![9](https://raw.githubusercontent.com/zhangyiming748/blog_image/master/double_system/9.webp)

"国产系统"最近多如雨后春笋,至于都什么质量,大家心照不宣

我们先来看看比较正常的uos

进入第一个安装界面选择自定义安装

![10](https://raw.githubusercontent.com/zhangyiming748/blog_image/master/double_system/10.webp)

接下来选择手动安装

![11](https://raw.githubusercontent.com/zhangyiming748/blog_image/master/double_system/11.webp)

接下来全程对这个可用空间操作,不要动前面几个分区,前面都是和Windows有关的分区

鼠标悬停在可用空间,最右边会有个加号,点击新建分区

![12](https://raw.githubusercontent.com/zhangyiming748/blog_image/master/double_system/12.webp)

新建efi分区,参数如图

![13](https://raw.githubusercontent.com/zhangyiming748/blog_image/master/double_system/13.webp)

新建根分区,参数如图

![14](https://raw.githubusercontent.com/zhangyiming748/blog_image/master/double_system/14.webp)

然后点击下一步安装

![15](https://raw.githubusercontent.com/zhangyiming748/blog_image/master/double_system/15.webp)

如果你的电脑内存大于4G,就不需要建立交换分区,如果你的电脑内存小于等于4G,安装系统后再开启swap文件,这里直接无视警告下一步,继续安装

![16](https://raw.githubusercontent.com/zhangyiming748/blog_image/master/double_system/16.webp)

安装完成后正常重启进入UOS系统

![17](https://raw.githubusercontent.com/zhangyiming748/blog_image/master/double_system/17.webp)

进入OOBE配置阶段

![18](https://raw.githubusercontent.com/zhangyiming748/blog_image/master/double_system/18.webp)

进入桌面后最好打开终端运行`sudo update-grub`更新一次

![19](https://raw.githubusercontent.com/zhangyiming748/blog_image/master/double_system/19.webp)

我们可以看到这里我们刚才新建的300M的efi分区并没有用到,但是安装程序如果检测到第一个efi分区小于300M就会警告你无法安装,所以这里一定要建立一个,只要你确定了双系统都能正常使用,删掉这个分区,合并到Windows或者Linux,由你决定

![20](https://raw.githubusercontent.com/zhangyiming748/blog_image/master/double_system/20.webp)

再来试试比较奇葩的~~开放~~优麒麟

进入第一个buzybox界面选择直接安装(第二个选项)

![21](https://raw.githubusercontent.com/zhangyiming748/blog_image/master/double_system/21.webp)

设置语言时区之后进入分区界面

![22](https://raw.githubusercontent.com/zhangyiming748/blog_image/master/double_system/22.webp)

由于这个系统只认一个efi分区,所以只需要建立一个根分区

新建根分区参数如下

![23](https://raw.githubusercontent.com/zhangyiming748/blog_image/master/double_system/23.webp)

分区表应该是这样,然后下一步安装

![24](https://raw.githubusercontent.com/zhangyiming748/blog_image/master/double_system/24.webp)

![25](https://raw.githubusercontent.com/zhangyiming748/blog_image/master/double_system/25.webp)

尽量断网安装,因为客服说过,他们的服务器是严格按照965工作制使用的,严禁任何形式的加班,如果你遇到了安装失败的错误,断网安装或者在live CD中先改时区是唯二的办法

![26](https://raw.githubusercontent.com/zhangyiming748/blog_image/master/double_system/26.webp)

安装成功后重启

正常情况下已经能看到双系统的启动菜单了

![27](https://raw.githubusercontent.com/zhangyiming748/blog_image/master/double_system/27.webp)

如果不放心的话,也可以执行一次`sudo update-grub`

![28](https://raw.githubusercontent.com/zhangyiming748/bl