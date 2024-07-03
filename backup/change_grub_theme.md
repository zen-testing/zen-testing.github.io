---
title: 'UOS更换grub界面主题'
date: 2022-09-26 15:44:24
tags: [UOS,Linux]
published: true
hideInList: false
feature: 
isTop: false
---

>今天闲来无事翻了200页uos论坛(u粉俱乐部)发现挺多人在抱怨能不能跳过grub界面,实际上就是觉得这个界面不好看,但是没有直说

>在我个人看来,uos和deepin主题说的年轻时尚是一帮中年高层干部心目中认为的年轻时尚,而不是年轻人真正的想法,好在linux是开源的,既然不好看那就来改一下

# 0x01

1. 选一个你自己喜欢的GRUB主题
2. 下载到桌面备用 比如
```bash
wget https://codeload.github.com/Teraskull/bigsur-grub2-theme/zip/refs/heads/master
```

# 0x02

```bash
# 必须使用su用户复制
cp -r /home/zen/Desktop/grub-theme/bigsur-grub2-theme-master/bigsur/ /boot/grub/themes
```

# 0x03

安装`grub-customizer`并且按照下图设置参数

[![jleHAg.md.png](https://s1.ax1x.com/2022/07/01/jleHAg.md.png)](https://imgtu.com/i/jleHAg)

黑框设置完成后再点保存,下方会有正在更新的进度条,进度条走完就可以重启查看效果了

[![jlmi4J.md.jpg](https://s1.ax1x.com/2022/07/01/jlmi4J.md.jpg)](https://imgtu.com/i/jlmi4J)

**不要尝试耍小聪明直接修改grub.cfg**
