---
title: '被Windows编辑过的Linux文件恢复'
date: 2022-09-26 18:48:06
tags: [Windows,Linux]
published: true
hideInList: false
feature: 
isTop: false
---
错误文本:解释器错误:没有那个文件或目录

Windows下,默认的文件编译,每一行的结尾是`\n\r`但是在Linux下文件的结尾是`\n`
因此在Windows环境下编辑过的文件在Linux下打开看的时候每一行的结尾就会多出来一个字符`\r`
常规只是看看文件的情况下,一般没啥影响,但是执行命令解释器解析的时候,就会出现本文中的异常
解决方法 `sed -i 's/\r$//' build.sh`<br>
彻底解决方法:<br>
`dos2unix`是将Windows格式文件转换为Unix\Linux格式的实用命令.Windows格式文件的换行符为`\r\n` 而Unix&Linux文件的换行符为`\n`dos2unix命令其实就是将文件中的`\r\n` 转换为`\n`
而unix2dos则是和dos2unix互为孪生的一个命令,它是将Linux&Unix格式文件转换为Windows格式文件的命令
dos2unix 可以一次转换多个文件
`find -name "*.sh" -exec dos2unix {} \;`