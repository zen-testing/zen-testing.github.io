---
title: 'macOS重建聚焦搜索'
date: 2023-10-28 02:03:06
tags: [macOS]
published: true
hideInList: false
feature: 
isTop: false
---
macOS每次大版本更新聚焦搜索都会崩掉,Sonoma之后甚至每次小升级聚焦搜索都会崩掉

<!-- more -->
```bash
sudo -i
# 删除并重建索引
mdutil -Ea
# 关闭索引
mdutil -ai off
# 开启索引
mdutil -ai on
```