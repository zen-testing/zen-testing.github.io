---
title: '使用adb命令查看电池电量信息'
date: 2022-09-26 15:09:25
tags: [adb,Android]
published: true
hideInList: false
feature: 
isTop: false
---
命令
`adb shell dumpsys battery`
返回值
```
Current Battery Service state:
  AC powered: false #交流电充电
  USB powered: false #USB充电
  Wireless powered: true #无线充电
  Max charging current: 0 #最大充电电流
  Max charging voltage: 0 #最大充电电压
  Charge counter: 44000 # 充电计数
  status: 5 #电池状态:2:充电状态 ,其他数字为非充电状态
  health: 2 #电池健康状态:只有数字2表示good
  present: true #电池是否安装在机身
  level: 100 #电量: 百分比
  scale: 100
  voltage: 4399 #电池电压
  temperature: 350 #电池温度,单位是0.1摄氏度
  technology: Li-poly #电池种类
```