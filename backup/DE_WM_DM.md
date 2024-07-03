---
title: '桌面环境(DE)窗口管理器(WM)主屏幕管理员(DM)'
date: 2022-09-26 16:05:04
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---

[原文地址](https://blog.desdelinux.net/display-manager-gestores-inicio-sesion-linux/)

# Linux操作系统的要素

### 桌面环境(DE)

桌面环境只不过是为特定操作系统的所有用户提供视觉友好和舒适的交互形式所必需的一组软件.换句话说,它是一种图形用户界面 (GUI) 实现,旨在提供访问和配置工具,例如工具栏和应用程序之间的集成,以及拖放等功能.[在这里查看更多](https://blog.desdelinux.net/gnome-que-es-instalacion-debian10-mxlinux19/)

### 窗口管理器(WM)
它是控制窗户位置和外观的一块拼图.这需要X Windows工作,但不是桌面环境,这是强制性的.根据官方 ArchLinux Wiki,在其" Windows 管理器"部分中,它们分为 3 种类型,分别是:堆叠,平铺和动态.[在这里查看更多](https://blog.desdelinux.net/gestores-ventanas-interfaces-graficas-usuario-gnu-linux/)

### 主屏幕管理员(DM)

它是在引导过程结束时显示的图形界面,而不是默认的 shell.有各种类型的显示管理器,就像有不同类型的窗口管理器和桌面环境一样.这些管理器通常会为每个管理器提供一定程度的定制和主题可用性.[在这里查看更多](https://wiki.archlinux.org/index.php/Display_manager_(Espa%C3%B1ol))

+ [GNOME显示管理器(GDM)](https://wiki.gnome.org/Projects/GDM):在其官方网站上被描述为管理图形显示服务器并管理图形用户登录的程序. 来自GNOME.

+ [KDE显示管理器(KDM)](https://es.wikipedia.org/wiki/KDE_Display_Manager):这是旧的DM 从KDE4,它基于XDM,因此它共享了许多配置选项. 这些选项大多数都在kdmrc中定义.

+ [简单桌面显示管理器(SDDM)](https://github.com/sddm/sddm):这是X11和Wayland的现代DM,其目标是快速,简单和美观. 当前,它已被DE KDE Plasma广泛使用,主要是因为它使用了诸如QtQuick之类的现代技术,这反过来又使设计人员能够创建流畅且生动的用户界面.

+ [灯光显示管理器(LightDM)](https://github.com/canonical/lightdm) :非常轻巧且简单的DM,它用作守护程序(服务),可以在许多事情中执行,包括必要时的屏幕服务器(例如X)和登录管理器,以允许用户选择要使用的帐户用户和会话类型.

+ [简单登录管理器(SliM)](https://github.com/iwamatsu/slim):DM是一种过时的,过时的,但是轻巧的,易于配置的方法,它需要最小的依赖性,并且独立于桌面环境.

+ [LX显示管理器(LXDM)](https://sourceforge.net/projects/lxdm/):专为LXDE设计的简单DM,但可以独立使用.

+ 还有很多,尤其是旧的,过时的或很少散布的或被称为: XDM,WDM MDM和Qingy.
