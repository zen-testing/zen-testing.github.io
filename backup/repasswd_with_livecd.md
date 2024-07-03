---
title: 'UOS使用liveCD覆盖修改密码'
date: 2022-09-26 19:41:29
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---
1. [进入livecd模式](https://zhangyiming748.github.io/post/uos-wei-hu-mo-shi/#LiveCD%E6%A8%A1%E5%BC%8F)
2. 使用命令修改密码
```shell
# passwd $USER
```
3. 修改成功后执行命令
```shell
# rm /home/uos/.local/share/keyrings/login.keyring
```