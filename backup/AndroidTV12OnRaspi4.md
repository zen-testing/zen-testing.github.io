---
title: '树莓派4安装AndroidTV(LineageOS 19 Android 12L)'
date: 2023-01-10 23:19:53
tags: [Raspberry,AndroidTV]
published: true
hideInList: false
feature: 
isTop: false
---
[原文地址](https://konstakang.com/devices/rpi4/LineageOS19/)

<!-- more -->
# 安装

0. 使用官方镜像安装工具将[lineage-19.1-20220923-UNOFFICIAL-KonstaKANG-rpi4.img](https://drive.google.com/file/d/1YgEYOxQF7Artmu_W2czBPErKSvCAD6wp/view?usp=sharing)烧写到TF卡(8G及以上)或移动硬盘上(虽然U盘也可以但是建议不要长时间读写u盘)
1. 下载[lineage-19.1-20220923-UNOFFICIAL-KonstaKANG-rpi4.zip](https://drive.google.com/file/d/1e9OPcALV2E2s-cu-IaFqSCmRQ79kJk45/view?usp=sharing)保存到内部或外部储存器
2. 重启到TWRP
3. 安装lineage-19.1-20220923-UNOFFICIAL-KonstaKANG-rpi4.zip(在这里也可以顺便调整系统使用全部储存空间,同时刷入[lineage-19.1-rpi-resize.zip](https://drive.google.com/file/d/17NDWJaht7eu47A7O53MJJKREfGH7IE5A/view?usp=sharing)即可
4. 在这一次刷入[Magisk](https://drive.google.com/file/d/1_RubGllyC4lP7RUB2bJdC16S5b9K51yI/view?usp=sharing)或任何你喜欢的插件(之后不好回到这个recovery)
5. 重启到正常系统
6. 如果之前刷入了面具需要安装[前端管理程序](https://drive.google.com/file/d/1mgy1S8_QfAubFWz1ArQWu1CiRzT86npr/view?usp=sharing)
7. 如需刷入[Google apps](https://drive.google.com/file/d/1tyOMWJISjIlBA7zCx9uom2HwhXFi4RF1/view?usp=sharing)务必要选择`Wipe` -> `Factory reset`然后再退出到正常系统
# 快捷键

|按键|对应按钮
|:---:|:---:|
|F1|主页|
|F2|返回|
|F3|多任务|
|F4|菜单|
|F5|电源|
|F11|音量减|
|F12|音量加|