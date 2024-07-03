---
title: 'linux mount命令详解'
date: 2023-09-29 18:16:32
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---
### linux [mount命令]

**功能**:加载指定的文件系统.

**语法**

```bash
mount \[-afFhnrvVw\] \[-L<标签>\] \[-o<选项>\] \[-t<文件系统类型>\] \[设备名\] \[加载点\]
```

用法说明:mount可将指定设备中指定的文件系统加载到Linux目录下(也就是装载点).可将经常使用的设备写入文件/etc/fastab,以使系统在每次启动时自动加载.mount加载设备的信息记录在/etc/fstab文件中.使用umount命令卸载设备时,记录将被清除.

#### 参数说明

|参数|说明|
|:---:|:---:|
|-a|加载文件/etc/fstab中设置的所有设备|
|-f|不实际加载设备 可与-v等参数同时使用以查看mount的执行过程|
|-F|需与-a参数同时使用,所有在/etc/fstab中设置的设备会被同时加载,可加快执行速度|
|-h|显示在线帮助信息|
|-L<标签>|加载文件系统标签为<标签>的设备|
|-n|不将加载信息记录在/etc/mtab文件中|
|-o <选项>|指定加载文件系统时的选项.有些选项也可在/etc/fstab中使用.这些选项包括<br>`async`以非同步的方式执行文件系统的输入输出动作<br>`atime`每次存取都更新inode的存取时间,默认设置,取消选项为`noatime`<br>`auto`必须在/etc/fstab文件中指定此选项.执行-a参数时,会加载设置为auto的设备,取消选取为`noauto`<br>`defaults`使用默认的选项.默认选项为rw\suid\dev\exec\anto nouser与async<br>`dev`可读文件系统上的字符或块设备,取消选项为`nodev`<br>`exec`可执行二进制文件,取消选项为`noexec`<br>`noatime` 每次存取时不更新inode的存取时间<br>`nodiratime` 每次存取时不更新所在目录的atime<br>`noauto` 无法使用-a参数来加载<br>`nodev` 不读文件系统上的字符或块设备<br>`noexec` 无法执行二进制文件<br>`nosuid` 关闭set-user-identifier(设置用户ID)与set-group-identifer(设置组ID)设置位<br>`nouser` 使一位用户无法执行加载操作,默认设置<br>`remount` 重新加载设备.通常用于改变设备的设置状态<br>`ro`以只读模式加载<br>`rw`以可读写模式加载<br>`suid`启动set-user-identifier(设置用户ID)与set-group-identifer(设置组ID)设置位,取消选项为nosuid<br>`sync`以同步方式执行文件系统的输入输出动作<br>`user`可以让一般用户加载设备|
|-r|以只读方式加载设备|
|-t <文件系统类型>|指定设备的文件系统类型.常用的选项说明有<br>`minixLinux`最早使用的文件系统<br>`ext2`Linux目前的常用文件系统<br>`msdos`MS-DOS 的 FAT<br>`vfat`Win85/98 的 VFAT<br>`nfs` 网络文件系统<br>`iso9660`CD-ROM光盘的标准文件系统<br>`ntfs`Windows NT的文件系统<br>`hpfs`OS/2文件系统 Windows NT 3.51之前版本的文件系统<br>`auto`自动检测文件系统|
|-v|执行时显示详细的信息|
|-V|显示版本信息|
|-w|以可读写模式加载设备,默认设置|
