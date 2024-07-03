---
title: 'win10无法使用内置管理员账户打开应用的临时解决办法'
date: 2022-09-26 20:42:54
tags: [Windows]
published: true
hideInList: false
feature: 
isTop: false
---
之所以说是临时解决办法,是因为这种错误只会发生你图一时之便安装了GHOST系统,既然是ghost,不稳定肯定不会只出现在这一个情境,在你真正需要用到电脑前建议还是装个原版系统,三种临时解决方案如下 **(不放图了,我怕视觉中国警告)**

----

## 注册表(适用于所有版本)

1. 按下"WIN+R"输入:regedit回车,进入注册表编辑器;

2. 在注册表左侧依次打开`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System`,在右边找到`FilterAdministratorToken`,双击后将数值数据改为`1`并`确定`
若没有`FilterAdministratorToken`则在空白处点击鼠标右键新建 `DWORD(32位)值`,并更名为`FilterAdministratorToken`双击将其数值数据改为`1`
3. 改完后,还要改另外一个,也是一样,依次展开`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\UIPI`,在右边有个`默认项`,双击将值改成`1`完成后重启.

## 组策略(适用于专业版/企业版)
1. 按下`WIN+R`输入`secpol.msc`回车进入`本地安全策略编辑器`

2. 在组策略中依次打开`安全设置`->`本地策略`->`安全选项`

3. 在右侧双击打开`用户帐户控制:用于内置管理员帐户的管理员批准模式`改为`已启用`确定并重启后生效.

## 无脑版(适用于阿尔茨海默症的人)

1. 在键盘上按下`WIN+X`或在开始菜单上单击右键,在弹出的菜单中点击`命令提示符(管理员)`

2. 在命令提示符中输入`net user 用户名 密码 /add`比如创建Zen用户密码为123456`net user Zen 123456 /add`

3. 创建账号后输入`net localgroup administrators 用户名 /add`例如`net localgroup administrators Zen /add`

4. 然后点击`开始菜单` - `用户头像`,之后切换到该账户即可正常使用应用,或者重启电脑,开机的时候选择新建的用户即可正常使用应用
