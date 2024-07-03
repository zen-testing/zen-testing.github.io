---
title: '压缩相关命令'
date: 2022-09-26 15:26:27
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---
# 解压tar分卷

```shell
$ cat 华为matebookE2022版售后原装系统.tar.* | tar xv
```

# xz

```shell
$ xz -9ek -T 12  release.tar
```

# 解压zip到指定目录

```shell
$ unzip 华为matebookE2022版原装系统.zip -d iso
```

# bzip2

```shell
# 解压1:
$ bzip2 -d FileName.bz2
# 解压2:
$ bunzip2 FileName.bz2
# 压缩:
$ bzip2 -z FileName
```

# tar.bzip2

```shell
# 解压:
$ tar jxvf FileName.tar.bz2#显示解压详细过程 或tar --bzip xvf FileName.tar.bz2 #不显示解压详细过程
# 压缩:
$ tar jcvf FileName.tar.bz2 DirName
```