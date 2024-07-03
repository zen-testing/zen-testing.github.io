---
title: 'homebrew常用参数'
date: 2023-04-24 14:16:58
tags: [HomeBrew]
published: true
hideInList: false
feature: 
isTop: false
---
```bash
export LDFLAGS="-L/opt/homebrew/opt/curl/lib"
export CPPFLAGS="-I/opt/homebrew/opt/curl/include"
export PATH="/opt/homebrew/opt/curl/bin:$PATH"
# 忽略curl错误
export HOMEBREW_FORCE_BREWED_CURL=1
# 禁止自动更新
export HOMEBREW_NO_AUTO_UPDATE=1
# 禁止自动清理
export HOMEBREW_NO_INSTALL_CLEANUP=1
```