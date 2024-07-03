---
title: 'find命令详解'
date: 2022-09-26 16:24:29
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---

# 从文件内容查找匹配指定字符串的行

`$ grep "被查找的字符串" 文件名`

例子:在当前目录里第一级文件夹中寻找包含指定字符串的.in文件

`$ grep "hermcontact" *.in`

# 从文件内容查找与正则表达式匹配的行:

`$ grep –e "正则表达式" 文件名`

# 查找时不区分大小写

`$ grep –i "被查找的字符串" 文件名`

# 查找匹配的行数

`$ grep -c "被查找的字符串" 文件名`

# 从文件内容查找不匹配指定字符串的行

`$ grep –v "被查找的字符串"文件名`

从根目录开始查找所有扩展名为.log的文本文件,并找出包含"ERROR"的行
find / -type f -name "*.log" | xargs grep "ERROR"
例子:从当前目录开始查找所有扩展名为.in的文本文件,并找出包含"thermcontact"的行
find . -name "*.in" | xargs grep "thermcontact"

# 批量删除macOS读取外部驱动器产生的4k挂载点文件

`find ./ -size 4k -exec rm -f {} \;`

# 批量删除macOS自动建立的`.DS_Store`文件

`find ./ -name ".DS_Store" -depth -exec rm {} \;`

# 查找并显示文件

`find ./ -name '*.txt' -print`

# 查找指定范围文件

`find . -type f -mtime -1 -size +100k`

# 查找空文件

`find -type d -empty`

# 查询出所有的空文件夹

`find -type d -empty`

# 查询所有/root/下的空文件夹

`find /root -type d -empty`

# 列出搜索到的文件/删除文件

`find . -name "shuaige.txt" -exec ls {} ;`

# 批量删除搜索到的文件

`find . -name "shuaige.txt" -exec rm -f {} ;`

# 删除前有提示

`find . -name "shuaige.txt" -ok rm -rf {} ;`

# 删除当前目录下面所有 test 文件夹下面的文件

`find . -name "test" -type d -exec rm -rf {} ;`

# 删除文件夹下面的所有的.svn文件

`find . -name '.svn' -exec rm -rf {} ;`

1. {}和之间有一个空格 注:
2. find . -name 之间也有空格 
3. exec 是一个后续的命令,{}内的内容代表前面查找出来的文件
