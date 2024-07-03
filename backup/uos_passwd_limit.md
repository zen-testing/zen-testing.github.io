---
title: 'UOS破解错误密码倒计时'
date: 2023-09-29 18:12:34
tags: [UOS]
published: true
hideInList: false
feature: 
isTop: false
---
uos的专业版或者家庭版系统,会在一定次数输入错误密码导致倒计时,应该是和苹果手机学的,但是他们可能并没有注意到,这是个linux系统

<!-- more -->
按ctrl alt f2 进入tty,使用root账号和超级密码登录

```bash
cd /var/lib/deepin/authenticate/
rm limit-states.json
```

这个能破除登录时间限制