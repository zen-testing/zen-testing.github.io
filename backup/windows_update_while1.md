---
title: 'Windows更新死循环解决'
date: 2022-09-26 21:03:36
tags: [Windows]
published: true
hideInList: false
feature: 
isTop: false
---
我们都有不顺利的时候,正在撤销更改

<!-- more -->

在Win10更新或升级的过程中,有时进展可能不太顺利,尤其是反复出现更新失败提示"无法完成更新,正在撤销更改"时很让人失望.不过这个问题也能解决,而且也不难,一个命令就可以搞定.

进入WindowsRE环境
执行以下命令

`DISM /image:系统盘符:\ /cleanup-image /revertpendingactions`