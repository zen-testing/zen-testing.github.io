---
title: '5分钟用wc命令统计代码行数'
date: 2023-11-23 17:24:18
tags: [五分钟已经很棒了]
published: true
hideInList: false
feature: 
isTop: false
---
全称 `word count`

# 参数
-l 统计行数
-w 统计字符串(单词)
-m 统计字符

# 统计代码

```bash
find ./your_program_path -type f -name "*.go" -o -name "*.sh" | xargs wc -l
```
