---
title: 'Windows 重命名个人文件夹'
date: 2022-09-26 18:31:37
tags: [Windows]
published: true
hideInList: false
feature: 
isTop: false
---

Windows10的个人文件夹命名策略很奇怪,在1809之前,中文用户名所在的个人文件夹直接使用中文命名,导致一些初学编程的人总是因为中文路径文字编码遇见一些不可思议的编译错误,好在1810之后微软也注意到了这个问题,如果用户在oobe阶段输入的是中文用户名,系统会自动设置用户输入第一个字的拼音作为个人文件夹名称,然而如果有人姓"庄",个人文件夹的名称就是"zhuan",因为微软只考虑到五个英文字符的拼音,那么如何在建立用户进入系统后再进行更改呢?手动直接改肯定是不行,因为这个文件夹不仅仅是一个普通的文件夹,与系统软件,环境变量等都有关系,以下是一种比较安全的更改方法

<!-- more -->

1. 启用Administrator账户
[![B7JPTx.png](https://s1.ax1x.com/2020/11/09/B7JPTx.png)](https://imgchr.com/i/B7JPTx)

2. 使用Administrator账户登录

[![B7JunA.png](https://s1.ax1x.com/2020/11/09/B7JunA.png)](https://imgchr.com/i/B7JunA)

3. 修改`c:\Users`下个人文件夹名称,比如我这里改为`zenZhang`
[![B7JZ1e.png](https://s1.ax1x.com/2020/11/09/B7JZ1e.png)](https://imgchr.com/i/B7JZ1e)

4. 打开注册表定位到`计算机\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\ProfileList`
[![B7JktK.png](https://s1.ax1x.com/2020/11/09/B7JktK.png)](https://imgchr.com/i/B7JktK)

5. 找到之前用户名对应的`ProfileImagePath`值
[![B7JAfO.png](https://s1.ax1x.com/2020/11/09/B7JAfO.png)](https://imgchr.com/i/B7JAfO)

6. 修改此值新的文件夹名`zenZhang`
[![B7Je6H.png](https://s1.ax1x.com/2020/11/09/B7Je6H.png)](https://imgchr.com/i/B7Je6H)

7. 注销后登陆原账户
[![B7J1tf.png](https://s1.ax1x.com/2020/11/09/B7J1tf.png)](https://imgchr.com/i/B7J1tf)

8. 恢复admin禁用状态,可以看到之前设置的DPI缩放并没有失效,由此可见,个人文件夹名被成功更改

[![B7JFk6.png](https://s1.ax1x.com/2020/11/09/B7JFk6.png)](https://imgchr.com/i/B7JFk6)
