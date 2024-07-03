---
title: 'linux普通用户使用sudo免密'
date: 2023-11-23 17:28:18
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---
`visudo`

```bash# Allow members of group sudo to execute any command
%sudo   ALL=(ALL:ALL) ALL
zen     ALL=(ALL:ALL) NOPASSWD:ALL
```