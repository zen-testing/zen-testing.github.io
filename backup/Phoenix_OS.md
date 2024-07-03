---
title: 'Phoenix OS安装方法'
date: 2022-09-26 15:21:33
tags: [Androidx86]
published: true
hideInList: false
feature: 
isTop: false
---

这里介绍四种方法,原文在凤凰论坛的帮助,但是不太好找,只有在中文网站才能在特定网站找到,这里整理一下
因为每种方法在虚拟机里实现一遍太浪费时间,所以这次依然没有截图,按照步骤做不需要截图

----

## Macintosh下安装
#### 安装之前
1. 下载最新版的Phoenix OS ISO版安装镜像,并刻录到U盘.
2. 使用磁盘工具将磁盘分出至少6GB的空余空间

#### 开始安装
1. 重启机器,在启动过程中按"option",进入启动选择界面,在启动选项中选择U盘启动;选择"Installation Phoenix OS to Harddisk"
2. 选择安装磁盘
安装程序会检测磁盘的信息,选择"Create/Modify partitions",一般会有机器的硬盘和U盘两个选项,我们选择Harddisk;
3. 启动会询问是否使用GPT分区,因为Mac一般使用UEFI引导方式,选择"Yes"
4. 此时会进入到分区工具界面,因为Mac中已经包含分区信息,不要修改苹果系统的分区信息,上下键移动到最后一个新建分区处,左右键选择"Delete"删除;
5. 上下键移动到"free space"处,左右方向键选择"New",首先需要新建一个EFI分区;
6. 选择起始位置:直接"Enter";选择分区大小:这里填"100M";选择分区类型,这里填写"ef00",为EFI分区;填写分区名称:这里可以填入"EFI";
7. 创建好EFI分区后,上下键选择剩余分区的位置,按照上述方式新建一个数据分区(起始位置默认;大小默认;分区格式默认(ext),名字为PhoenixOS);
8. 左右方向键选择"Write",保存我们的修改,分区工具会询问是否确定保存,输入"yes"确认;
9. 左右方向键选择"Quit",退出分区工具;
10. 退出后可以在分区选择列表中看到我们新分的sda4/5,选择sda5安装Phoenix OS;
11. 是否格式化磁盘
Phoenix OS支持安装在EXT4\FAT32和NTFS分区上,本教程选择EXT4分区并确认格式化.区别: A.EXT4分区:无需定义凤凰系统存储空间大小,可以使用磁盘的剩余空间作为凤凰系统存储空间;B.FAT32分区:需要定义凤凰系统存储空间大小,但由分区特性决定,单个文件最大不能超过4GB;C.NTFS分区:单个文件没有大小限制,其余与FAT32特性相同;
12. 是否安装EFI引导项:选择"Yes";
13. 选择EFI分区的位置:选择/dev/sda4并格式化
EFI分区是否格式化:这里因为我们新建分区,选择格式化,如果已经有EFI分区,选择不格式化,这里选"Yes";
14. 是否安装Grub:选择"Skip";
15. 正在安装;
16. 创建data.img
在FAT32和NTFS分区上使用data.img 存放数据,这里一般创建4GB以上的空间,EXT4分区上则会跳过此步骤;
17. 安装完成,重启电脑;
18. 启动并进入Phoenix OS
拔出U盘重新启动设备,按住"option",选择新的引导项,进入Grub菜单中看到Phoenix OS选项,选择此选项即可进入Phoenix OS.

## Linux下安装
#### 安装之前
1. 下载最新版的Phoenix OS ISO版安装镜像,并刻录到U盘;(命令:`sudo dd if=~/Downloads/PhoenixOSInstall-1.0.7.iso of=/dev/sdb && sync`
2.打开gparted查看磁盘使用情况,选择要安装Phoenix OS的磁盘目录并记下来;
Phoenix OS支持安装在EXT4\FAT32和NTFS分区上,本教程选择安装在/dev/sda5;分区格式选择EXT4.区别: A.EXT4分区:无需定义凤凰系统存储空间大小,可以使用磁盘的剩余空间作为凤凰系统存储空间;B.FAT32分区:需要定义凤凰系统存储空间大小,但由分区特性决定,单个文件最大不能超过4GB;C.NTFS分区:单个文件没有大小限制,其余与FAT32特性相同;

#### 开始安装
1. 重启机器,在启动项中选择U盘启动;选择"Installation Phoenix OS to Harddisk";
2. 选择安装磁盘
安装程序会检测磁盘的信息并列出,本教程选择安装在/dev/sda5;
3. 是否格式化磁盘
一般情况下磁盘已经在使用中,所以不需要格式化,选择"Do not format";(格式化会清空数据请谨慎选择)
4. 是否安装EFI引导项:选择跳过,我们使用Ubuntu的引导项;
5. 是否安装Grub:同样选择跳过;
6. 正在安装
7. 创建data.img:
在FAT32和NTFS分区上使用data.img 存放数据,这里一般创建4GB以上的空间,EXT4分区上则可以跳过此步骤;
8. 安装完成重启电脑;

#### 添加Phoenix OS启动项
1. 重启进入到Ubuntu中,为Phoenix OS添加Grub的引导项,首先修改/etc/grub.d/40-custom文件,填入下列内容,并保存:menuentry ‘Phoenix OS’ --class android-x86 {search --set=root --file /PhoenixOS/kernellinux /PhoenixOS/kernel quiet root=/dev/ram0 SRC=/PhoenixOS vga=autoinitrd /PhoenixOS/initrd.img}


2. 修改/etc/default/grub文件,注释下列两行(在两行前加#),并保存;

  `#GRUB_HIDDEN_TIMEOUT=0`

  `#GRUB_HIDDEN_TIMEOUT_QUIET=TRUE`

3. 生成新的Grub菜单;
通过下列命令行生成新的Grub菜单:
sudo grub-mkconfig -o /boot/grub/grub.cfg
#### 进入Phoenix OS
重启电脑在引导菜单界面选择凤凰系统引导

## Windows的UEFI安装
说明:

1. 本教程会清空磁盘数据,请提前做好备份工作

2. 本教程适用于Legacy引导的设备,点击查看如何确认引导方式
#### 安装之前
下载最新版的Phoenix OS ISO版安装镜像,并刻录到U盘
#### 开始安装
1. 重启机器,在启动选项中选择U盘启动;选择"Installation Phoenix OS to Harddisk"

2. 选择安装磁盘
安装程序会检测磁盘的信息并列出.选择"Create/Modify partitions"新建分区表;

3. 这时会询问是否使用GPT分区,因为这里使用UEFI引导方式,选择"Yes"

4. 此时会进入到分区工具界面,左右方向键选择"New",首先需要新建一个EFI分区;

5. 选择起始位置:直接"Enter";

6. 选择分区大小,这里我们填"100M"

7. 选择分区类型,这里填写"ef00",为EFI分区;

8. 填写分区名称:这里可以填入"EFI";

9. 创建数据分区
创建好EFI分区后,上下键选择剩余分区的位置,按照上述方式新建一个数据分区(起始位置默认;大小默认;分区格式默认(ext),名字为PhoenixOS);

10. 左右方向键选择"Write",保存我们的修改,分区工具会询问是否确定保存,输入"yes"确认;

11. 左右方向键选择"Quit",退出分区工具;

12. 退出后可以在分区选择列表中看到我们新分的sda1/2,选择sda2安装Phoenix OS;

13. 格式化磁盘
Phoenix OS支持安装在EXT4\FAT32和NTFS分区上,本教程选择EXT4分区并确认格式化.区别: A.EXT4分区:无需定义凤凰系统存储空间大小,可以使用磁盘的剩余空间作为凤凰系统存储空间;B.FAT32分区:需要定义凤凰系统存储空间大小,但由分区特性决定,单个文件最大不能超过4GB;C.NTFS分区:单个文件没有大小限制,其余与FAT32特性相同;


14. 是否安装EFI引导项:选择"Yes";

15. 选择EFI分区的位置:选择/dev/sda1;

16. 格式化EFI分区
这里选"Yes";因为我们新建分区,所以选择格式化.如果已经有EFI分区,请选择"No"

17. 是否安装Grub:选择"Skip";

18. 正在安装

19. 创建data.img
在FAT32和NTFS分区上使用data.img 存放数据,这里一般创建4GB以上的空间,EXT4分区上则会跳过此步骤;

20. 安装完成重启电脑

21. 启动Phoenix OS
重启可以在Grub菜单中看到Phoenix OS选项,选择此选项即可进入Phoenix OS.

## Windows的Legacy安装
说明:

1. 本教程会清空磁盘数据,请提前做好备份工作

2. 本教程适用于Legacy引导的设备,点击查看如何确认引导方式
#### 安装之前
下载最新版的Phoenix OS ISO版安装镜像,并刻录到U盘
#### 开始安装

1. 重启机器,在启动选项中选择U盘启动,选择"Installation Phoenix OS to Harddisk"

2. 选择安装磁盘
安装程序会检测磁盘的信息并列出.我们选择"Create/Modify partitions"新建分区表;

3. 创建完成会询问是否使用GPT分区.这里使用Legacy引导方式,我们选择"No"

4. 此时会进入到分区工具界面:左右方向键选择"New",新建一个分区;

5. 选择"Primary"新建一个主分区

6. 选择分区大小,这里我们把所有剩余大小都分给这个分区,所以不用修改直接按"Enter";

7. 左右方向键选择"Bootable",把这个分区设置为可以引导的分区;

8. 左右方向键选择"Write",保存我们的修改;

9. 分区工具会询问是否确定保存,输入"yes"确认;

10. 左右方向键选择"Quit",退出分区工具;

11. 退出后可以在分区选择列表中看到我们新分的sda1,选择它安装Phoenix OS;

12. 格式化磁盘
Phoenix OS支持安装在EXT/4\FAT32和NTFS分区上,本教程选择EXT4分区并确认格式化. 区别: A.EXT4分区:无需定义凤凰系统存储空间大小,可以使用磁盘的剩余空间作为凤凰系统存储空间; B.FAT32分区:需要定义凤凰系统存储空间大小,但由分区特性决定,单个文件最大不能超过4GB; C.NTFS分区:单个文件没有大小限制,其余与FAT32特性相同;

13. 是否安装EFI引导项:选择跳过

14. 是否安装Grub:选择"Yes"

15. 正在安装

16. 创建data.img:
在FAT32和NTFS分区上使用data.img 存放数据,这里一般创建4GB以上的空间,EXT4分区上则会跳过此步骤;

17. 安装完成,重启电脑

18. 进入Phoenix OS
重启可以在引导菜单中看到Phoenix OS选项,选择此选项即可进入Phoenix OS
