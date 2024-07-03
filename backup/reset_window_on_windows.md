---
title: '重置 Windows 的窗口大小和位置'
date: 2023-08-18 13:51:01
tags: [Windows]
published: true
hideInList: false
feature: 
isTop: false
---
注册表编辑器中定位到

```reg
HKEY_CURRENT_USER\SOFTWARE\Classes\Local Settings\Software\Microsoft\Windows\Shell\Bags\AllFolders\Shell
```

在打开的项中,删除所有以WinPos和MaxPos开头的键,关闭注册表编辑器后重启 Windows 资源管理器即可