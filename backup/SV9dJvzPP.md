---
title: '强行加入Windows insider Dev channel'
date: 2022-09-26 16:32:31
tags: [Windows]
published: true
hideInList: false
feature: 
isTop: false
---
对于 6 月 24 日之前没有加入 DEV 通道却又想测试 Win11 的小伙伴,我们这里提供一种方法,不过修改注册表有一定风险,该方法仅供参考,后果自负

<!-- more -->

首先,加入 Insider 计划并选择 Release Preview,毕竟你也没有其他选择.

重启,然后打开注册表编辑器.

在左侧导航中找到:
`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsSelfHost\UI\Selection`
![1](https://z3.ax1x.com/2021/07/04/RfmjM9.jpg)
1. 将 UIBranch 中的值更改为 Dev
2. 将 ContentType 中的值更改为 Mainline
3. 将 Ring 中的文本更改为 External

然后导航到:
`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsSelfHost\Applicability`
![2](https://z3.ax1x.com/2021/07/04/RfmOxJ.jpg)
1. 将 BranchName 中的值更改为 Dev
2. 将 ContentType 中的值更改为 Mainline
3. 将 Ring 中的值更改为 External
4. 退出注册表编辑器,重启.

OK,若你重启之后发现现在变成了 DEV 通道那么恭喜你,现在只需耐心等待微软准时推送测试版即可;万一操作失败的话则建议放弃电脑
