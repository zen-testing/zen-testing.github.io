---
title: 'openEuler安装xfce桌面环境'
date: 2022-09-26 18:13:33
tags: [openEuler,Linux,xfce]
published: true
hideInList: false
feature: 
isTop: false
---

````shell
#!/usr/bin/env bash

echo "install Xfce"
sudo dnf update 

echo "Run"
sudo dnf install dejavu-fonts liberation-fonts gnu-*-fonts google-*-fonts

echo "install Xorg"
sudo dnf install xorg-*

echo "install Xfce"
sudo dnf install xfwm4 xfdesktop xfce4-* xfce4-*-plugin *fonts

echo "install the login manager"
sudo dnf install lightdm

echo "start Xfce using the login manager"
sudo systemctl start lightdm

echo "set the GUI to start upon system boot"
sudo systemctl enable lightdm
sudo systemctl set-default graphical.target

echo "Restart the server"
sudo reboot
```