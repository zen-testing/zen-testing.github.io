---
title: 'shell脚本实现 按行读取网址列表并处理'
date: 2024-04-01 18:50:32
tags: [AI,shell]
published: true
hideInList: false
feature: 
isTop: false
---
```bash
#!/bin/bash

# 读取网址列表文件
url_list="url_list.txt"

# 按行读取网址列表
while IFS= read -r url
do
  # 在这里处理每个网址，例如访问网址、下载内容等
  echo "处理网址： $url"
done < "$url_list"
```