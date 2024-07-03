---
title: 'dd命令高级用法'
date: 2023-08-18 13:52:29
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---
# dd命令除了烧录启动盘还能做什么呢?

|参数|解释|
|:---:|:---:|
|if=文件名|输入文件名,缺省为标准输入.即指定源文件|
|of=文件名|输出文件名,缺省为标准输出.即指定目的文件|
|ibs=bytes|一次读入bytes个字节,即指定一个块大小为bytes个字节|
|obs=bytes|一次输出bytes个字节,即指定一个块大小为bytes个字节|
|bs=bytes|同时设置读入/输出的块大小为bytes个字节|
|cbs=bytes|一次转换bytes个字节,即指定转换缓冲区大小|
|skip=blocks|从输入文件开头跳过blocks个块后再开始复制|
|seek=blocks|从输出文件开头跳过blocks个块后再开始复制<br>通常只用当输出文件是磁盘或磁带时才有效,即备份到磁盘或磁带时才有效|
|count=blocks|仅拷贝blocks个块,块大小等于ibs指定的字节数|
|conv=conversion|用指定的参数转换文件|
|ascii|转换ebcdic为ascii|
|ebcdic|转换ascii为ebcdic|
|ibm|转换ascii为alternate ebcdic|

1. 创建空文件

```bash
dd if=/dev/zero of=/tmp/2M.txt bs=1M count=2记录了2+0 的读入记录了2+0 的写出2097152 bytes (2.1 MB, 2.0 MiB) copied, 0.00159757 s, 1.3 GB/s
```

2. 备份/dev/sdb全盘数据,并利用gzip工具进行压缩,保存到指定路径

```bash
dd if=/dev/sdb | gzip > /root/image.gz
```

3. 将压缩的备份文件恢复到指定盘

```bash
gzip -dc /root/image.gz | dd of=/dev/sdb
```
4. 备份与恢复MBR

```bash
# 备份磁盘开始的512个字节大小的MBR信息到指定文件
dd if=/dev/sda of=/root/image count=1 bs=512
# MBR大小为512字节.count=1指仅拷贝一个块;bs=512指块大小为512个字节
# 恢复
dd if=/root/image of=/dev/sda
# 将备份的MBR信息写到磁盘开始部分
```

5. 拷贝内存内容到硬盘
```bash
dd if=/dev/mem of=/root/mem.img bs=1024
```

6. 将本地的`/dev/sda`整盘备份到`/dev/sdb`

```bash
dd if=/dev/sda of=/dev/sdb
```

7. 将`/dev/sdb`全盘数据备份到指定路径的`backup.img`文件

```bash
dd if=/dev/sdb of=/root/backup.img
```

8. 将备份文件恢复到指定盘

```bash
dd if=/root/image of=/dev/sdb
```

9. 增加swap分区文件大小

```bash
# 创建一个大小为1G的文件:
dd if=/dev/zero of=/swapfile bs=1M count=1024
# 把这个文件变成swap文件:
mkswap /swapfile
# 启用这个swap文件:
swapon /swapfile
# 编辑/etc/fstab文件,使在每次开机时自动加载swap文件:
echo '/swapfile    swap    swap    default   0 0' >> /etc/fstab
```

10. 销毁磁盘数据

```bash
dd if=/dev/urandom of=/dev/sda1
# 利用随机的数据填充硬盘,在某些必要的场合可以用来销毁数据.执行上述命令后硬盘数据能被销毁,但利用某些特殊手段还是能还原出来,所以有必要应该多次写入随机数据,或是直接销毁硬盘.
```

11. 测试硬盘的读写速度

```bash
dd if=/dev/zero bs=2048 count=500000 of=/root/1Gb.file#dd if=/root/1Gb.file bs=2M | dd of=/dev/null
# 通过以上两个命令输出的命令执行时间,可以计算出硬盘的读\写速度.
```

12. 测试磁盘I/O性能

```bash
# dd 的direct I/O 测试方式,直接绕过文件系统缓存,测试磁盘的真实I/O 性能
dd if=/dev/zero of=out.file bs=512K count=2048 oflag=sync#dd if=/dev/zero of=out.file bs=512K count=2048 oflag=dsync#dd if=/dev/zero of=out.file bs=512K count=2048 conv=fsync
# oflag=sync,每个 I/O 写入,都需要直接落到 物理存储 的 元数据和 真实数据
# oflag=dsync,每个 I/O 写入,都需要直接落到 物理存储 的 真实数据
# conv=fsync,只要求在 dd 命令结束前,将所有数据落到物理存储中
```

13. 确定硬盘的最佳块大小

```bash
dd if=/dev/zero bs=1M count=1000 of=/root/1Gb.file#dd if=/dev/zero bs=2M count=500 of=/root/1Gb.file#dd if=/dev/zero bs=4M count=250 of=/root/1Gb.file#dd if=/dev/zero bs=8M count=125 of=/root/1Gb.file
# 通过比较以上命令输出中所显示的命令执行时间,即可确定系统最佳的块大小.
```
14. 修复硬盘

```bash
dd if=/dev/sda of=/dev/sda
# 当硬盘较长时间(一年以上)放置不使用后,磁盘会有消磁的可能,当磁头读到这些区域时会遇到困难,并可能导致I/O错误.当这种情况影响到硬盘的第一个扇区时,可能导致硬盘报废.上边的命令有可能使这些数据起死回生.并且这个过程是安全\高效的.
```