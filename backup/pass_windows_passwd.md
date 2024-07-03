---
title: '用最朴实的工具绕过Windows密码'
date: 2022-09-26 15:53:59
tags: [Windows]
published: true
hideInList: false
feature: 
isTop: false
---

<iframe width="560" height="315" src="https://www.youtube.com/embed/A-lbY7jl354" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# 为暴躁老哥准备的文字版
1. 使用系统盘启动忘记密码的电脑
2. 按`Shift+F10`或`Fn+Shift+F10`打开命令提示符
3. 输入`regedit`打开注册表
4. 定位到`HKEY_LOCAL_MACHINE`(鼠标选中)
5. 选择`文件`➡️`加载配置单元`
6. 找到`系统盘:\Windows\System32\config\SYSTEM`(注意此时系统盘不一定是c 自己根据大小判断)
7. 选中`SYSTEM`后打开,需要自定义一个名称,比如`Mojave`
8. 定位到`HKEY_LOCAL_MACHINE\Mojave\Setup`
9. 在右边找到`cmdline`双击修改值为`cmd.exe`
10. 继续向下找到`SetupType`修改值为`2`
11. 左边选中`Mojave`然后选择`文件`➡️`卸载配置单元`
12. 弹出外部介质(光盘/u盘/软盘/磁带/打孔纸带什么的)退出重启电脑
13. 重启过程中会弹出命令提示符窗口(类似于Linux的单用户模式)
14. 新建用户`zhang`的命令为`net user zhang 000000`
15. 将用户`zhang`加入管理员组`net localgroup administrator zhang /add`
16. 输入`regedit`打开注册表
17. 定位到`HKEY_LOCAL_MACHINE\System\Setup`
18. 在右边找到`cmdline`清空数值
19. 向下找到`SetupType`恢复值为`0`
20. 关闭注册表,输入`shutdown -r -t 0`重启电脑
21. 开机后发现多出新建的管理员用户,可以为所欲为了
