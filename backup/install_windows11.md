---
title: '安装Windows11的技巧'
date: 2022-09-26 19:18:58
tags: [Windows]
published: true
hideInList: false
feature: 
isTop: false
---

# 在不受支持的硬件上全新安装

1. 按 `Shift+F10` 打开命令提示符键入 `regedit.exe` 启动注册表编辑器
2. 导航到 `HKEY_LOCAL_MACHINE\SYSTEM\Setup`
3. 右侧右键选择新建一个项并命名为 `LabConfig`
4. 新建五个DWORD类型的值 `BypassTPMCheck` `BypassSecureBootCheck` `BypassRAMCheck` `BypassStorageCheck` `BypassCPUCheck` 并且编辑数值为 `1`
5. 导航到`HKEY_LOCAL_MACHINE\SYSTEM\Setup`
6. 新建项`MoSetup`
7. 在`MoSetup`下新建DWORD值`AllowUpgradesWithUnsupportedTPMOrCPU`编辑数值为`1`
8. 关闭注册表编辑器和命令提示符
9. 继续安装

# 在不受支持的硬件上升级安装

打开记事本粘贴如下内容

```regedit
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SYSTEM\Setup\LabConfig]
"BypassTPMCheck"=dword:00000001
"BypassSecureBootCheck"=dword:00000001
"BypassRAMCheck"=dword:00000001
"BypassStorageCheck"=dword:00000001
"BypassCPUCheck"=dword:00000001
;以上部分这五个键根据自己情况选择就好,一般老电脑只是TPM和CPU不达标,只要跳过这两个就好,不用全部写上
[HKEY_LOCAL_MACHINE\SYSTEM\Setup\MoSetup]
"AllowUpgradesWithUnsupportedTPMOrCPU"=dword:00000001
```

另存为`Bypass.reg`
类型选择全部文件

然后双击打开这个文件导入注册表

# OOBE阶段强行跳过联网

1. 按 `Shift+F10` 打开命令提示符键入 `OOBE\BYPASSNRO`
![](https://i3g4v6w8.stackpathcdn.com/wp-content/uploads/2022/02/oobe-bypassnro-wndows-11-no-internet-install.webp)
2. 电脑重启后多出一个`我没有互联网连接的选项`
![](https://i3g4v6w8.stackpathcdn.com/wp-content/uploads/2022/02/windows-11-oobe-dont-have-internet.webp)
3. 单击`继续有限设置`
![](https://i3g4v6w8.stackpathcdn.com/wp-content/uploads/2022/02/continue-limited-setup-windows-11.webp)