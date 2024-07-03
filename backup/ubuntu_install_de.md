---
title: 'UbuntuServer安装图形界面'
date: 2022-09-26 19:25:57
tags: [Linux,Ubuntu]
published: true
hideInList: false
feature: 
isTop: false
---

```shell
$ sudo apt get update
$ sudo apt-get dist-upgrade
$ sudo apt-get install vim nano net-tools
$ sudo dpkg-reconfigure tzdata (70)
[设置snap商店走代理](https://zhangyiming748.github.io/2022/02/08/snapd_set_proxy/#%E8%A6%86%E7%9B%96snapd%E7%9A%84%E7%8E%B0%E6%9C%89%E8%AE%BE%E7%BD%AE)
$ sudo snap install firefox
$ sudo apt-get install cinnamon-desktop-environment
$ sudo apt-get install slim
$ sudo systemctl status slim
$ sudo systemctl enable slim
$ sudo systemctl reboot
$ sudo apt-get purge lightdm
$ sudo snap install snap-store
$ sudo apt-get install fuse libfuse2
$ ./balenaEtcher-1.7.9-x64.AppImage  --disable-gpu-sandbox
```

```shell
$ sudo apt-get purge \
swell-foop \
hitori \
gnome-sudoku \
gnome-klotski \
gnome-nibbles \
aisleriot \
gnome-mines \
gnome-robots \
gnome-2048 \
gnome-mahjongg \
four-in-a-row \
gnome-tetravex \
five-or-more \
quadrapassel \
gnome-games \
tali \
gnome-chess \
gnome-taquin \
iagno \
lightsoff \
brasero-common \
gnome-sound-recorder \
rhythmbox-plugins \
brasero \
rhythmbox \
brasero-cdrkit \
nautilus-extension-brasero \
cheese \
rhythmbox-plugin-alternative-toolbar \
rhythmbox-plugin-cdrecorder \
rhythmbox-data \
sound-juicer \
libbrasero-media3-1 \
libreoffice-l10n-en-gb \
libreoffice-l10n-en-za \
libreoffice-calc \
libreoffice-gnome \
libreoffice-base-core \
libreoffice-core \
libreoffice-common \
libreoffice-draw \
libreoffice-impress \
libreoffice-help-zh-cn \
libreoffice-writer \
libreoffice-l10n-zh-cn \
libreoffice-help-common \
libreoffice-math \
libreoffice-gtk3 \
libreoffice-help-en-gb \
libreoffice-help-en-us \
libcmark0.30.2 \
hexchat-python3 \
remmina-plugin-rdp \
remmina-plugin-vnc \
thunderbird \
transmission-gtk \
evolution-plugins \
remmina-plugin-secret \
hexchat-lua \
hexchat-plugins \
remmina \
thunderbird-locale-zh-cn \
hexchat \
thunderbird-locale-en \
hexchat-perl \
thunderbird-locale-zh-hans \
transmission-common \
hexchat-common \
remmina-common \
thunderbird-locale-en-gb \
thunderbird-locale-en-us \
deja-dup \
```

```shell
$ sudu snap remove firefox
```

# 实用主义者

```shell
$ sudo apt-get install -y \
net-tools \
vim \
nano \
dialog \
whiptail \
xfce4 \
slim  \
language-pack-zh* \
chinese* \
fonts-arphic-ukai \
fonts-arphic-uming \
fonts-ipafont-mincho \
fonts-ipafont-gothic \
fonts-unfonts-core 
$ sudo dpkg-reconfigure locales
$ sudo systemctl reboot
```