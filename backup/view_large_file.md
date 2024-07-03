---
title: '5分钟定位Linux的大文件夹'
date: 2023-11-23 17:21:41
tags: [五分钟已经很棒了]
published: true
hideInList: false
feature: 
isTop: false
---
# du(disk usage)

-s 只看总量
-h 可读性
-d 1 / --max-depth=1 显示的文件夹深度
`du -d 1 -h | sort -h | tail -n 5`

```bash
# 最大的五个文件
485M    ./sdk
1.4G    ./.local
72G     ./disk1
921G    ./disk2
995G    .
```

或
`du -d 1 -h | sort -hr | head -n 5`

```bash
995G    .
921G    ./disk2
72G     ./disk1
1.2G    ./.local
485M    ./sdk
```

# 查询目录下的大文件

`du -a -h | sort -hr | head -n 5`

```bash
995G    .
921G    ./disk2/share
921G    ./disk2
287G    ./disk2/share/BaiduNetdisk
159G    ./disk2/share/music
```

**不过我还是喜欢用ncdu**
