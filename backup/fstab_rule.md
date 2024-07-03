---
title: 'fstab详解'
date: 2022-09-26 16:35:08
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---
# /etc/fstab文件的作用

磁盘被手动挂载之后都必须把挂载信息写入/etc/fstab这个文件中,否则下次开机启动时仍然需要重新挂载.
系统开机时会主动读取/etc/fstab这个文件中的内容,根据文件里面的配置挂载磁盘.这样我们只需要将磁盘的挂载信息写入这个文件中我们就不需要每次开机启动之后手动进行挂载了.

# 挂载的限制

在说明这个文件的作用之前先强调一下挂载的限制.
1. 根目录是必须挂载的,而且一定要先于其他mount point被挂载.因为mount是所有目录的根目录,其他目录都是由根目录衍生出来的.
2. 挂载点必须是已经存在的目录.
3. 挂载点的指定可以任意,但必须遵守必要的系统目录架构原则
4. 所有挂载点在同一时间只能被挂载一次
5. 所有分区在同一时间只能挂在一次
6. 若进行卸载,必须将工作目录退出挂载点(及其子目录)之外

# /etc/fstab文件中的参数

如:
```
proc            /proc           proc    defaults          0       0
PARTUUID=79e70732-01  /boot           vfat    defaults          0       2
PARTUUID=79e70732-02  /               ext4    defaults,noatime  0       1
# PARTUUID=5b4b9250-01  /home/pi/safe/HardDisk  exfat   defaults        0       0
# /dev/sda1     /mnt    ext4    defaults        0       0
# a swapfile is not a swap partition, no line here
#   use  dphys-swapfile swap[on|off]  for that
```
以第三行为例
|PARTUUID=79e70732-02|/|ext4|defaults,noatime|0|1|
|:---:|:---:|:---:|:---:|:---:|:---:|
|Device:磁盘设备文件或者该设备的Label或者UUID|Mount point:设备的挂载点,就是你要挂载到哪个目录下.|filesystem:磁盘文件系统的格式,包括ext2\ext3\reiserfs\nfs\vfat等|parameters:文件系统的参数|能否被dump备份命令作用:dump是一个用来作为备份的命令.通常这个参数的值为0或者1|是否检验扇区:开机的过程中,系统默认会以fsck检验我们系统是否为完整(clean).|

### 查看分区的label和uuid

Label就是分区的标签,在最初安装系统时填写的挂载点就是标签的名字.可以通过查看一个分区的superblock中的信息找到UUID和Label name.
例如:我们要查看当前系统下外存的uuid和label name
`$ blkid`
返回类似
```
/dev/sda1: LABEL_FATBOOT="boot" LABEL="boot" UUID="F4F1-BC2C" TYPE="vfat" PARTUUID="79e70732-01"
/dev/sda2: LABEL="rootfs" UUID="163660a6-ad17-44fc-99c5-5c75e78ad815" TYPE="ext4" PARTUUID="79e70732-02"
```

### 使用设备名和label及uuid作为标识的不同

使用设备名称(/dev/sda)来挂载分区时是被固定死的,一旦磁盘的插槽顺序发生了变化,就会出现名称不对应的问题.因为这个名称是会改变的.
不过使用label挂载就不用担心插槽顺序方面的问题.不过要随时注意你的Label name.至于UUID,每个分区被格式化以后都会有一个UUID作为唯一的标识号.使用uuid挂载的话就不用担心会发生错乱的问题了

### 第四列可选参数

|parameter|说明|
|:---:|:---:|
|Async/sync|设置是否为同步方式运行,默认为async|
|auto/noauto|当执行mount -a 的命令时,此文件系统是否被主动挂载.默认为auto|
|rw/ro|是否以以只读或者读写模式挂载|
|exec/noexec|限制此文件系统内是否能够进行"执行"的操作|
|user/nouser|是否允许用户使用mount命令挂载|
|suid/nosuid|是否允许SUID的存在|
|Usrquota|启动文件系统支持磁盘配额模式|
|Grpquota|启动文件系统对群组磁盘配额模式的支持|
|Defaults|同时具有rw,suid,dev,exec,auto,nouser,async等默认参数的设置|

### 第五列可选参数

|parameter|说明|
|:---:|:---:|
|0|代表不要做dump备份|
|1|代表要每天进行dump的操作|
|2|代表不定日期的进行dump操作|

### 第六列可选参数

|parameter|说明|
|:---:|:---:|
|0|不要检验|
|1|最早检验(一般根目录会选择)|
|2|1级别检验完成之后进行检验|