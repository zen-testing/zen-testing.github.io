---
title: '仅复制文件目录'
date: 2022-09-26 18:49:29
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---
```shell
find ./1-1 -type d -exec mkdir ./des/{} \;
参数:
-type d : 表示只差早目录
-exec <命令> 空格\;  : 表示把前面查找的结果输入到命令中作为参数,{}会被替换成搜索结果,必须\;结尾
./1-1 : 目标目录,这里可以使绝对路径,可以写相对路径
./des/{} : 表示把结果拷贝到 "./des/....."中
```