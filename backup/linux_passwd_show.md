---
title: 'sudo 输入密码的时候显示 * '
date: 2023-09-29 20:18:52
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---
```shell
sed -i 's/env_reset/pwfeedback/g' /etc/sudoers
```

## 对于国产个别封闭系统慎用