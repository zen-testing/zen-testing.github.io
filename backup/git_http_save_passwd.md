---
title: 'git http方式设置记住密码'
date: 2022-11-25 20:11:25
tags: [Git]
published: true
hideInList: false
feature: 
isTop: false
---
# 0x01

在服务器输入命令

```bash
git config --global credential.helper store
```

# 0x02

查看保存的密码

```bash
cat ~/.git-credentials
```

# 0x03

查看当前服务器的git密码配置方式

```bash
cat ~/.gitconfig
```