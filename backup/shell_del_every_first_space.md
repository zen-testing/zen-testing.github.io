---
title: 'shell 实现遍历指定文件夹下每一个扩展名为txt的文件 并删除每行第一个多余的空格'
date: 2024-04-01 19:26:30
tags: [AI,shell]
published: true
hideInList: false
feature: 
isTop: false
---
```shell
#!/bin/bash

# 指定要遍历的文件夹路径
folder_path="/path/to/folder"

# 遍历文件夹下所有扩展名为txt的文件
for file in "$folder_path"/*.txt; do
    # 使用sed命令删除每行第一个多余的空格
    sed 's/^[[:space:]]\+//' "$file" > "${file}_temp"
    # 用处理后的文件替换原文件
    mv "${file}_temp" "$file"
done
```