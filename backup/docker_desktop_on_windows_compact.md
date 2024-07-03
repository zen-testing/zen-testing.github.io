---
title: 'Windows下Docker Desktop占用过大空间解决方法'
date: 2024-05-03 17:12:51
tags: [Docker,Windows]
published: true
hideInList: false
feature: 
isTop: false
---
[![pkkvC6S.png](https://s21.ax1x.com/2024/05/03/pkkvC6S.png)](https://imgse.com/i/pkkvC6S)

<!-- more -->
# 起因
很多同学拉取镜像使用一段时间后发现 C 盘快满了，把之前用过的镜像和容器删除,发现 WSL 挂载目录的虚拟磁盘大小没有变化,非常的奇怪
其实,不同于 WSL1
WSL2 本质上是虚拟机,所以 Windows 会自动创建 vhdx 后缀的虚拟磁盘文件作为存储.这个 vhdx 后缀的虚拟磁盘文件特点是可以自动扩容,但是一般不会自动缩容.一旦有很多文件把它"撑大"即使把这些文件删除它也不会自动"缩小"
所以删除文件后还需要我们手动进行压缩才能释放磁盘空间.
# 解决
### 找到要压缩的虚拟磁盘文件
如果你不是个大聪明如果你没更改挂载磁盘的位置，那他位置在 `%userprofile%\AppData\Local\Docker\wsl\data\ext4.vhdx` 
### 关闭 Docker Desktop
在任务栏右下角右键单击 Docker Desktop 图标关闭 Docker 桌面，选择退出 Docker 桌面，等一会 Docker 图标没了之后，就证明 Docker 完全关闭了，然后，打开命令提示符：
```powershell
wsl --list -v
```
[![pkkvMXF.png](https://s21.ax1x.com/2024/05/03/pkkvMXF.png)](https://imgse.com/i/pkkvMXF)
### 压缩虚拟磁盘文件
在 PowerShell 中执行:
```powershell
# 关闭 WSL2 中的 linux distributions
wsl --shutdown
# 运行管理计算机的驱动器的 DiskPart 命令
diskpart
在新打开的 DiskPart 命令窗口中执行：
# 选择虚拟磁盘文件
select vdisk file="就是步骤2.1虚拟磁盘文件的路径"
# 压缩文件
compact vdisk
# 压缩完毕后卸载磁盘
detach vdisk
``` 
上述操作执行完毕,WSL2 删除文件后空出来的磁盘空间就被释放了,可以去虚拟磁盘文件的路径看到 ext4.vhdx 文件大小已经减小.最后打开 Docker Desktop 可以看到原来镜像还在,成功解决问题。

# 捷径
保存以下文件为compress.ps1
管理员权限运行
相同的效果
```powershell
# 关闭 WSL2 中的 linux distributions
wsl --shutdown

# 运行管理计算机的驱动器的 DiskPart 命令
$diskpartScript = @"
select vdisk file=%userprofile%\AppData\Local\Docker\wsl\data\ext4.vhdx
compact vdisk
detach vdisk
"@

$diskpartScript | diskpart
```
