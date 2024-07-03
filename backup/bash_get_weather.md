---
title: 'Linux里查询天气'
date: 2022-09-26 19:12:29
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---

**从实用性的角度来讲,用Bash查询天气肯定是不如直接打开APP或者浏览器查询方便,你在Bash里得到的天气信息也当然不如APP里展示的丰富,不过,用来drum(zhuang)the(ge)beat是再好不过了,有些时候,我们大概不能绝对地用"它是否实用"来衡量一件事物的价值,重要的是,它能为你带来多少乐趣.**

<!-- more -->

文中的演示是在Win10的Linux子系统(WSL)中进行的,在其他的Linux发行版上,这种方法同样适用.下面我们开始.

### 首先打开Bash(如果不会开启Linux子系统在下方留言,有时间的话我会写教程)

![0](https://raw.githubusercontent.com/zhangyiming748/zhangyiming748.github.io/master/img/searchweather/0.webp)

### 以中文查询当前IP所在地的天气

`curl wttr.in?lang=zh`

![1](https://raw.githubusercontent.com/zhangyiming748/zhangyiming748.github.io/master/img/searchweather/1.webp)

### 查询某个城市的天气

`curl wttr.in/Daqing?lang=zh`

![2](https://raw.githubusercontent.com/zhangyiming748/zhangyiming748.github.io/master/img/searchweather/2.webp)

### 查询指定国家某个城市的天气

`curl wttr.in/Daqing`

### 查询某个城市某个区域的天气

`curl wttr.in/~Harbin+Xuefulu?lang=zh`

### 查询某个机场的天气(参数为机场代号)

`curl wttr.in/HRB?lang=zh`

### 查询某个坐标的天气(参数为北纬东京)

`curl wttr.in/41.80,123.43`

### 查询当天大概天气

`curl wttr.in/Daqing?0`

### 查询当天详细天气

`curl wttr.in/Daqing?1`

### 查询今明两天天气

`curl wttr.in/Daqing?1`

### 查询正午和晚间的天气

`curl wttr.in/Daqing?n`

### 只用黑白颜色显示

`curl wttr.in/Qingdao?T`

### 查看当前月相

`curl wttr.in/Moon?lang=zh`

### 查看指定日期月相

`curl wttr.in/Moon@2019-12-12`