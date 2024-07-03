---
title: '请求管理员权限的批处理文件'
date: 2022-09-26 15:35:50
tags: [Windows,bat]
published: true
hideInList: false
feature: 
isTop: false
---

>很多批处理文件在运行时都需要管理员权限,然而这些程序往往需要用户手动以管理员身份运行才能正常运作,这种"半自动化"设定事实上还是比较麻烦的,要是能够双击运行直接就带管理员权限岂不是更放心?其实这也不难,使用IT之家提供的代码就可以轻松实现自动获取权限的功能.Win7/Win8.1/Win10各版本均可使用.

把如下代码(分割线之间)复制到记事本中,并保存为 .bat 格式即可

```bat
@echo off
CLS
ECHO.
ECHO ================================
ECHO 获取批处理文件管理员权限
ECHO ================================
:init
setlocal DisableDelayedExpansion
set "batchPath=%~0"
for %%k in (%0) do set batchName=%%~nk
set "vbsGetPrivileges=%temp%\OEgetPriv_%batchName%.vbs"
setlocal EnableDelayedExpansion
NET FILE 1>NUL 2>NUL
if '%errorlevel%' == '0' ( goto gotPrivileges ) else ( goto getPrivileges )
:getPrivileges
if '%1'=='ELEV' (echo ELEV & shift /1 & goto gotPrivileges)
ECHO.
ECHO ********************************
ECHO 请求 UAC 权限批准……
ECHO ********************************
ECHO Set UAC = CreateObject^("Shell.Application"^) > "%vbsGetPrivileges%"
ECHO args = "ELEV " >> "%vbsGetPrivileges%"
ECHO For Each strArg in WScript.Arguments >> "%vbsGetPrivileges%"
ECHO args = args ^& strArg ^& " " >> "%vbsGetPrivileges%"
ECHO Next >> "%vbsGetPrivileges%"
ECHO UAC.ShellExecute "!batchPath!", args, "", "runas", 1 >> "%vbsGetPrivileges%"
"%SystemRoot%\System32\WScript.exe" "%vbsGetPrivileges%" %*
exit /B
:gotPrivileges
setlocal & pushd .
cd /d %~dp0
if '%1'=='ELEV' (del "%vbsGetPrivileges%" 1>nul 2>nul & shift /1)
:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
:: 以下为需要运行的批处理文件代码 ::
:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
rem 本行以下可修改为你需要的bat命令(从上面三行冒号开始到下面都可删改)
ECHO 欢迎使用Windows!
ECHO.
pause
```
