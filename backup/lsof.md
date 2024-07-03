---
title: '5分钟用lsof定位端口和文件'
date: 2023-11-23 17:14:49
tags: [五分钟已经很棒了]
published: true
hideInList: false
feature: 
isTop: false
---
全称 list open files

`lsof | head -n 10`
返回类似
```bash
# 进程名称 进程ID 线程ID 任务命令 所属用户 在进程中的标识符 资源类型 设备号 大小和偏移量 节点名称 路径或名称
COMMAND      PID    TID TASKCMD               USER   FD      TYPE             DEVICE SIZE/OFF       NODE NAME
systemd        1                              root  cwd       DIR              179,2     4096          2 /
systemd        1                              root  rtd       DIR              179,2     4096          2 /
systemd        1                              root  txt       REG              179,2   133464      17120 /usr/lib/systemd/systemd
systemd        1                              root  mem       REG              179,2   198640       5730 /usr/lib/aarch64-linux-gnu/libgpg-error.so.0.33.1
systemd        1                              root  mem       REG              179,2   592440       5849 /usr/lib/aarch64-linux-gnu/libpcre2-8.so.0.11.2
systemd        1                              root  mem       REG              179,2    67504       5656 /usr/lib/aarch64-linux-gnu/libcap-ng.so.0.0.0
systemd        1                              root  mem       REG              179,2   591960       5786 /usr/lib/aarch64-linux-gnu/libm.so.6
systemd        1                              root  mem       REG              179,2   198584       5784 /usr/lib/aarch64-linux-gnu/liblzma.so.5.4.1
systemd        1                              root  mem       REG              179,2   657352       5943 /usr/lib/aarch64-linux-gnu/libzstd.so.1.5.4
```

# 检测端口占用
`lsof -i :3000`

```bash
COMMAND    PID USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
docker-pr 1294 root    4u  IPv4  15332      0t0  TCP *:3000 (LISTEN)
docker-pr 1302 root    4u  IPv6  18623      0t0  TCP *:3000 (LISTEN)
```
# 检测文件被哪个进程占用

`sudo lsof /home/zen/container/gitea/gitea/gitea.db `

```bash
COMMAND  PID USER   FD   TYPE DEVICE SIZE/OFF   NODE NAME
gitea   1540  zen   12u   REG  179,2  1961984 253114 ./gitea.db
```

# 检测特定用户都打开了哪些文件
`sudo lsof -u zen`
```bash
COMMAND      PID USER   FD      TYPE             DEVICE SIZE/OFF       NODE NAME
gitea       1540  zen  cwd       DIR               0,41     4096     389958 /app/gitea
gitea       1540  zen  rtd       DIR               0,41     4096     390033 /
gitea       1540  zen  txt       REG               0,41 96508104     389959 /app/gitea/gitea
gitea       1540  zen  mem       REG              179,2              390083 /app/gitea/gitea (stat: No such file or directory)
gitea       1540  zen  mem-W     REG              179,2              253141 /data/gitea/indexers/issues.bleve/store/root.bolt (stat: No such file or directory)
gitea       1540  zen  mem       REG              179,2              388309 /lib/ld-musl-aarch64.so.1 (stat: No such file or directory)
gitea       1540  zen    0u      CHR                1,3      0t0          5 /dev/null
gitea       1540  zen    1w     FIFO               0,12      0t0      19499 pipe
gitea       1540  zen    2w     FIFO               0,12      0t0      19500 pipe
gitea       1540  zen    3uW     REG              179,2        0     253130 /data/gitea/queues/common/LOCK
gitea       1540  zen    4u  a_inode               0,13        0       1061 [eventpoll:5,14]
gitea       1540  zen    5r     FIFO               0,12      0t0      17921 pipe
gitea       1540  zen    6w     FIFO               0,12      0t0      17921 pipe
gitea       1540  zen    7w      REG              179,2    37189     253131 /data/gitea/queues/common/LOG
gitea       1540  zen    8w      REG              179,2        0     251074 /data/gitea/queues/common/000140.log
gitea       1540  zen    9w      REG              179,2      456     294337 /data/gitea/queues/common/MANIFEST-000141
gitea       1540  zen   10r      REG              179,2      491     251073 /data/gitea/queues/common/000142.ldb
gitea       1540  zen   12u      REG              179,2  1961984     253114 /data/gitea/gitea.db
gitea       1540  zen   13uW     REG              179,2    65536     253141 /data/gitea/indexers/issues.bleve/store/root.bolt
gitea       1540  zen   14u     sock                0,8      0t0      16881 protocol: TCPv6
systemd   118689  zen  cwd       DIR              179,2     4096          2 /
systemd   118689  zen  rtd       DIR              179,2     4096          2 /
systemd   118689  zen  txt       REG              179,2   133464      17120 /usr/lib/systemd/systemd
systemd   118689  zen  mem       REG              179,2   198640       5730 /usr/lib/aarch64-linux-gnu/libgpg-error.so.0.33.1
systemd   118689  zen  mem       REG              179,2   592440       5849 /usr/lib/aarch64-linux-gnu/libpcre2-8.so.0.11.2
systemd   118689  zen  mem       REG              179,2    67504       5656 /usr/lib/aarch64-linux-gnu/libcap-ng.so.0.0.0
systemd   118689  zen  mem       REG              179,2   591960       5786 /usr/lib/aarch64-linux-gnu/libm.so.6
systemd   118689  zen  mem       REG              179,2   198584       5784 /usr/lib/aarch64-linux-gnu/liblzma.so.5.4.1
systemd   118689  zen  mem       REG              179,2   657352       5943 /usr/lib/aarch64-linux-gnu/libzstd.so.1.5.4
systemd   118689  zen  mem       REG              179,2  4466856       3947 /usr/lib/aarch64-linux-gnu/libcrypto.so.3
systemd   118689  zen  mem       REG              179,2   199056       5783 /usr/lib/aarch64-linux-gnu/liblz4.so.1.9.4
systemd   118689  zen  mem       REG              179,2    67960       5749 /usr/lib/aarch64-linux-gnu/libip4tc.so.2.0.0
systemd   118689  zen  mem       REG              179,2  1000296       5719 /usr/lib/aarch64-linux-gnu/libgcrypt.so.20.4.1
systemd   118689  zen  mem       REG              179,2   198584       5662 /usr/lib/aarch64-linux-gnu/libcrypt.so.1.1.0
systemd   118689  zen  mem       REG              179,2    67704       5657 /usr/lib/aarch64-linux-gnu/libcap.so.2.66
systemd   118689  zen  mem       REG              179,2   396248       5630 /usr/lib/aarch64-linux-gnu/libblkid.so.1.1.0
systemd   118689  zen  mem       REG              179,2    67432       5596 /usr/lib/aarch64-linux-gnu/libacl.so.1.1.2301
systemd   118689  zen  mem       REG              179,2   461432       5796 /usr/lib/aarch64-linux-gnu/libmount.so.1.1.0
systemd   118689  zen  mem       REG              179,2   198800       5882 /usr/lib/aarch64-linux-gnu/libselinux.so.1
systemd   118689  zen  mem       REG              179,2   133752       5600 /usr/lib/aarch64-linux-gnu/libapparmor.so.1.8.4
systemd   118689  zen  mem       REG              179,2   133176       5761 /usr/lib/aarch64-linux-gnu/libkmod.so.2.4.0
systemd   118689  zen  mem       REG              179,2   132984       5611 /usr/lib/aarch64-linux-gnu/libaudit.so.1.0.0
systemd   118689  zen  mem       REG              179,2    67512      21476 /usr/lib/aarch64-linux-gnu/libpam.so.0.85.1
systemd   118689  zen  mem       REG              179,2   133328       5881 /usr/lib/aarch64-linux-gnu/libseccomp.so.2.5.4
systemd   118689  zen  mem       REG              179,2  1651472       5650 /usr/lib/aarch64-linux-gnu/libc.so.6
systemd   118689  zen  mem       REG              179,2  3354288       8175 /usr/lib/aarch64-linux-gnu/systemd/libsystemd-shared-252.so
systemd   118689  zen  mem       REG              179,2  2035576       8174 /usr/lib/aarch64-linux-gnu/systemd/libsystemd-core-252.so
systemd   118689  zen  mem       REG              179,2   202904       5409 /usr/lib/aarch64-linux-gnu/ld-linux-aarch64.so.1
systemd   118689  zen    0r      CHR                1,3      0t0          5 /dev/null
systemd   118689  zen    1u     unix 0x00000000144761e2      0t0      90860 type=STREAM (CONNECTED)
systemd   118689  zen    2u     unix 0x00000000144761e2      0t0      90860 type=STREAM (CONNECTED)
systemd   118689  zen    3u     unix 0x000000007da37498      0t0      90880 type=DGRAM (CONNECTED)
systemd   118689  zen    4u  a_inode               0,13        0       1061 [eventpoll:5,6,8,9,11,14,15,16,17,19,20,21,26,27,28,29,30,31,32,34]
systemd   118689  zen    5u  a_inode               0,13        0       1061 [signalfd]
systemd   118689  zen    6r  a_inode               0,13        0       1061 inotify
systemd   118689  zen    7r      DIR               0,24        0       3187 /sys/fs/cgroup/user.slice/user-1000.slice/user@1000.service
systemd   118689  zen    8u  a_inode               0,13        0       1061 [timerfd]
systemd   118689  zen    9u  a_inode               0,13        0       1061 [eventpoll:10,13]
systemd   118689  zen   10r      REG               0,18        0      90885 /proc/118689/mountinfo
systemd   118689  zen   11r  a_inode               0,13        0       1061 inotify
systemd   118689  zen   12u     unix 0x0000000095287989      0t0      90904 /run/user/1000/bus type=STREAM (LISTEN)
systemd   118689  zen   13r  a_inode               0,13        0       1061 inotify
systemd   118689  zen   14r      REG               0,18        0 4026532094 /proc/swaps
systemd   118689  zen   15u  netlink                         0t0      90886 KOBJECT_UEVENT
systemd   118689  zen   16u     unix 0x00000000b80a85c0      0t0      90892 /run/user/1000/systemd/notify type=DGRAM (CONNECTED)
systemd   118689  zen   17u     unix 0x00000000f88e9f9b      0t0      90893 type=DGRAM (CONNECTED)
systemd   118689  zen   18u     unix 0x00000000d4be8383      0t0      90894 type=DGRAM (CONNECTED)
systemd   118689  zen   19u     unix 0x0000000078096042      0t0      90895 /run/user/1000/systemd/private type=STREAM (LISTEN)
systemd   118689  zen   20u     unix 0x00000000856f09ae      0t0      90897 type=STREAM (CONNECTED)
systemd   118689  zen   21u  a_inode               0,13        0       1061 [timerfd]
systemd   118689  zen   26u     unix 0x0000000012f4e32a      0t0      90906 /run/user/1000/gnupg/S.dirmngr type=STREAM (LISTEN)
systemd   118689  zen   27u     unix 0x000000005ce911b7      0t0      90908 /run/user/1000/drkonqi-coredump-launcher type=SEQPACKET (LISTEN)
systemd   118689  zen   28u     unix 0x00000000bf870e18      0t0      90910 /run/user/1000/gnupg/S.gpg-agent.browser type=STREAM (LISTEN)
systemd   118689  zen   29u     unix 0x00000000c43b2439      0t0      90912 /run/user/1000/gnupg/S.gpg-agent.extra type=STREAM (LISTEN)
systemd   118689  zen   30u     unix 0x000000003856619d      0t0      90914 /run/user/1000/gnupg/S.gpg-agent.ssh type=STREAM (LISTEN)
systemd   118689  zen   31u     unix 0x000000000ff1923d      0t0      90916 /run/user/1000/gnupg/S.gpg-agent type=STREAM (LISTEN)
systemd   118689  zen   32u     unix 0x00000000c5f2646d      0t0      90918 /run/user/1000/pk-debconf-socket type=STREAM (LISTEN)
systemd   118689  zen   33u     unix 0x00000000aa541606      0t0      90920 /run/user/1000/pulse/native type=STREAM (LISTEN)
systemd   118689  zen   34u     unix 0x000000009504b8cd      0t0      91434 type=STREAM (CONNECTED)
(sd-pam)  118692  zen  cwd       DIR              179,2     4096          2 /
(sd-pam)  118692  zen  rtd       DIR              179,2     4096          2 /
(sd-pam)  118692  zen  txt       REG              179,2   133464      17120 /usr/lib/systemd/systemd
(sd-pam)  118692  zen  mem       REG              179,2    67352      22608 /usr/lib/aarch64-linux-gnu/security/pam_chksshpwd.so
(sd-pam)  118692  zen  mem       REG              179,2    67616      21485 /usr/lib/aarch64-linux-gnu/libpam_misc.so.0.82.1
(sd-pam)  118692  zen  mem       REG              179,2   530352       8163 /usr/lib/aarch64-linux-gnu/security/pam_systemd.so
(sd-pam)  118692  zen  mem       REG              179,2    67512      21585 /usr/lib/aarch64-linux-gnu/security/pam_keyinit.so
(sd-pam)  118692  zen  mem       REG              179,2    67592      21589 /usr/lib/aarch64-linux-gnu/security/pam_limits.so
(sd-pam)  118692  zen  mem       REG              179,2    67512      21601 /usr/lib/aarch64-linux-gnu/security/pam_loginuid.so
(sd-pam)  118692  zen  mem       REG              179,2    67512      21638 /usr/lib/aarch64-linux-gnu/security/pam_selinux.so
(sd-pam)  118692  zen  mem       REG              179,2    67512      21628 /usr/lib/aarch64-linux-gnu/security/pam_permit.so
(sd-pam)  118692  zen  mem       REG              179,2    67288      21568 /usr/lib/aarch64-linux-gnu/security/pam_deny.so
(sd-pam)  118692  zen  mem       REG              179,2    67600      21672 /usr/lib/aarch64-linux-gnu/security/pam_unix.so
(sd-pam)  118692  zen  mem       REG              179,2   198640       5730 /usr/lib/aarch64-linux-gnu/libgpg-error.so.0.33.1
(sd-pam)  118692  zen  mem       REG              179,2   592440       5849 /usr/lib/aarch64-linux-gnu/libpcre2-8.so.0.11.2
(sd-pam)  118692  zen  mem       REG              179,2    67504       5656 /usr/lib/aarch64-linux-gnu/libcap-ng.so.0.0.0
(sd-pam)  118692  zen  mem       REG              179,2   591960       5786 /usr/lib/aarch64-linux-gnu/libm.so.6
(sd-pam)  118692  zen  mem       REG              179,2   198584       5784 /usr/lib/aarch64-linux-gnu/liblzma.so.5.4.1
(sd-pam)  118692  zen  mem       REG              179,2   657352       5943 /usr/lib/aarch64-linux-gnu/libzstd.so.1.5.4
(sd-pam)  118692  zen  mem       REG              179,2  4466856       3947 /usr/lib/aarch64-linux-gnu/libcrypto.so.3
(sd-pam)  118692  zen  mem       REG              179,2   199056       5783 /usr/lib/aarch64-linux-gnu/liblz4.so.1.9.4
(sd-pam)  118692  zen  mem       REG              179,2    67960       5749 /usr/lib/aarch64-linux-gnu/libip4tc.so.2.0.0
(sd-pam)  118692  zen  mem       REG              179,2  1000296       5719 /usr/lib/aarch64-linux-gnu/libgcrypt.so.20.4.1
(sd-pam)  118692  zen  mem       REG              179,2   198584       5662 /usr/lib/aarch64-linux-gnu/libcrypt.so.1.1.0
(sd-pam)  118692  zen  mem       REG              179,2    67704       5657 /usr/lib/aarch64-linux-gnu/libcap.so.2.66
(sd-pam)  118692  zen  mem       REG              179,2   396248       5630 /usr/lib/aarch64-linux-gnu/libblkid.so.1.1.0
(sd-pam)  118692  zen  mem       REG              179,2    67432       5596 /usr/lib/aarch64-linux-gnu/libacl.so.1.1.2301
(sd-pam)  118692  zen  mem       REG              179,2   461432       5796 /usr/lib/aarch64-linux-gnu/libmount.so.1.1.0
(sd-pam)  118692  zen  mem       REG              179,2   198800       5882 /usr/lib/aarch64-linux-gnu/libselinux.so.1
(sd-pam)  118692  zen  mem       REG              179,2   133752       5600 /usr/lib/aarch64-linux-gnu/libapparmor.so.1.8.4
(sd-pam)  118692  zen  mem       REG              179,2   133176       5761 /usr/lib/aarch64-linux-gnu/libkmod.so.2.4.0
(sd-pam)  118692  zen  mem       REG              179,2   132984       5611 /usr/lib/aarch64-linux-gnu/libaudit.so.1.0.0
(sd-pam)  118692  zen  mem       REG              179,2    67512      21476 /usr/lib/aarch64-linux-gnu/libpam.so.0.85.1
(sd-pam)  118692  zen  mem       REG              179,2   133328       5881 /usr/lib/aarch64-linux-gnu/libseccomp.so.2.5.4
(sd-pam)  118692  zen  mem       REG              179,2  1651472       5650 /usr/lib/aarch64-linux-gnu/libc.so.6
(sd-pam)  118692  zen  mem       REG              179,2  3354288       8175 /usr/lib/aarch64-linux-gnu/systemd/libsystemd-shared-252.so
(sd-pam)  118692  zen  mem       REG              179,2  2035576       8174 /usr/lib/aarch64-linux-gnu/systemd/libsystemd-core-252.so
(sd-pam)  118692  zen  mem       REG              179,2   202904       5409 /usr/lib/aarch64-linux-gnu/ld-linux-aarch64.so.1
(sd-pam)  118692  zen    0r      CHR                1,3      0t0          5 /dev/null
(sd-pam)  118692  zen    1u     unix 0x00000000144761e2      0t0      90860 type=STREAM (CONNECTED)
(sd-pam)  118692  zen    2u     unix 0x00000000144761e2      0t0      90860 type=STREAM (CONNECTED)
(sd-pam)  118692  zen    3u  a_inode               0,13        0       1061 [eventfd:13]
(sd-pam)  118692  zen    4u  a_inode               0,13        0       1061 [eventfd:14]
(sd-pam)  118692  zen    6w     FIFO               0,12      0t0      90864 pipe
(sd-pam)  118692  zen    7u     unix 0x000000008a6c850d      0t0      90870 type=DGRAM (CONNECTED)
rootlessk 118712  zen  cwd       DIR              179,2     4096        946 /home/zen
rootlessk 118712  zen  rtd       DIR              179,2     4096          2 /
rootlessk 118712  zen  txt       REG              179,2 11681880       9579 /usr/bin/rootlesskit
rootlessk 118712  zen  mem       REG              179,2  1651472       5650 /usr/lib/aarch64-linux-gnu/libc.so.6
rootlessk 118712  zen  mem       REG              179,2   202904       5409 /usr/lib/aarch64-linux-gnu/ld-linux-aarch64.so.1
rootlessk 118712  zen    0r      CHR                1,3      0t0          5 /dev/null
rootlessk 118712  zen    1u     unix 0x00000000e74ffb4b      0t0      89860 type=STREAM (CONNECTED)
rootlessk 118712  zen    2u     unix 0x00000000e74ffb4b      0t0      89860 type=STREAM (CONNECTED)
rootlessk 118712  zen    3rR     DIR              179,2     4096     509431 /tmp/rootlesskit1709315404
rootlessk 118712  zen    4u  a_inode               0,13        0       1061 [eventpoll:5,8,9,13]
rootlessk 118712  zen    5r     FIFO               0,12      0t0      91289 pipe
rootlessk 118712  zen    6w     FIFO               0,12      0t0      91289 pipe
rootlessk 118712  zen    7rW     REG              179,2        0     509436 /tmp/rootlesskit1709315404/lock
rootlessk 118712  zen    8r     FIFO               0,12      0t0      91293 pipe
rootlessk 118712  zen    9u     unix 0x00000000d8d92290      0t0      90985 /tmp/rootlesskit1709315404/api.sock type=STREAM (LISTEN)
rootlessk 118712  zen   13r     FIFO               0,12      0t0      90962 pipe
pulseaudi 118713  zen  cwd       DIR              179,2     4096          2 /
pulseaudi 118713  zen  rtd       DIR              179,2     4096          2 /
pulseaudi 118713  zen  txt       REG              179,2   133352      67126 /usr/bin/pulseaudio
pulseaudi 118713  zen  mem       REG              179,2    67592     290170 /usr/lib/pulse-16.1+dfsg1/modules/module-filter-apply.so
pulseaudi 118713  zen  mem       REG              179,2    67512     290171 /usr/lib/pulse-16.1+dfsg1/modules/module-filter-heuristics.so
pulseaudi 118713  zen  mem       REG              179,2    67592     290191 /usr/lib/pulse-16.1+dfsg1/modules/module-role-cork.so
pulseaudi 118713  zen  mem       REG              179,2    67512     290187 /usr/lib/pulse-16.1+dfsg1/modules/module-position-event-sounds.so
pulseaudi 118713  zen  mem       REG              179,2    67512     290204 /usr/lib/pulse-16.1+dfsg1/modules/module-systemd-login.so
pulseaudi 118713  zen  mem       REG              179,2    67592     290201 /usr/lib/pulse-16.1+dfsg1/modules/module-suspend-on-idle.so
pulseaudi 118713  zen  mem       REG              179,2    67592     290174 /usr/lib/pulse-16.1+dfsg1/modules/module-intended-roles.so
pulseaudi 118713  zen  mem       REG              179,2    67592     290155 /usr/lib/pulse-16.1+dfsg1/modules/module-always-sink.so
pulseaudi 118713  zen  mem       REG              179,2    67512     290165 /usr/lib/pulse-16.1+dfsg1/modules/module-default-device-restore.so
pulseaudi 118713  zen  mem       REG              179,2    67352     294051 /usr/lib/pulse-16.1+dfsg1/modules/module-gsettings.so
pulseaudi 118713  zen  mem       REG              179,2    67592     290181 /usr/lib/pulse-16.1+dfsg1/modules/module-native-protocol-unix.so
pulseaudi 118713  zen  mem       REG              179,2    70504       5647 /usr/lib/aarch64-linux-gnu/libbz2.so.1.0.4
pulseaudi 118713  zen  mem       REG              179,2   133624       5692 /usr/lib/aarch64-linux-gnu/libelf-0.188.so
pulseaudi 118713  zen  mem       REG              179,2   725520       5688 /usr/lib/aarch64-linux-gnu/libdw-0.188.so
pulseaudi 118713  zen  mem       REG              179,2    67976       5917 /usr/lib/aarch64-linux-gnu/libunwind.so.8.0.1
pulseaudi 118713  zen  mem       REG              179,2   529696      66928 /usr/lib/aarch64-linux-gnu/libgstbase-1.0.so.0.2200.0
pulseaudi 118713  zen  mem       REG              179,2   134504      66994 /usr/lib/aarch64-linux-gnu/libgstapp-1.0.so.0.2200.0
pulseaudi 118713  zen  mem       REG              179,2  1453120      66932 /usr/lib/aarch64-linux-gnu/libgstreamer-1.0.so.0.2200.0
pulseaudi 118713  zen  mem       REG              179,2    67432      29510 /usr/lib/aarch64-linux-gnu/libsbc.so.1.3.1
pulseaudi 118713  zen  mem       REG              179,2   205976       5632 /usr/lib/aarch64-linux-gnu/libbluetooth.so.3.19.8
pulseaudi 118713  zen  mem       REG              179,2   198728     294046 /usr/lib/pulse-16.1+dfsg1/modules/libbluez5-util.so
pulseaudi 118713  zen  mem       REG              179,2    67616     294050 /usr/lib/pulse-16.1+dfsg1/modules/module-bluez5-discover.so
pulseaudi 118713  zen  mem       REG              179,2    67528     294047 /usr/lib/pulse-16.1+dfsg1/modules/module-bluetooth-discover.so
pulseaudi 118713  zen  mem       REG              179,2    67608     294048 /usr/lib/pulse-16.1+dfsg1/modules/module-bluetooth-policy.so
pulseaudi 118713  zen  mem       REG              179,2    67432      61349 /usr/lib/aarch64-linux-gnu/libdatrie.so.1.4.0
pulseaudi 118713  zen  mem       REG              179,2   137328      61332 /usr/lib/aarch64-linux-gnu/libgraphite2.so.3.2.1
pulseaudi 118713  zen  mem       REG              179,2 31262336       5742 /usr/lib/aarch64-linux-gnu/libicudata.so.72.1
pulseaudi 118713  zen  mem       REG              179,2   396248       5630 /usr/lib/aarch64-linux-gnu/libblkid.so.1.1.0
pulseaudi 118713  zen  mem       REG              179,2   133232       5641 /usr/lib/aarch64-linux-gnu/libbrotlicommon.so.1.0.9
pulseaudi 118713  zen  mem       REG              179,2   198752       5695 /usr/lib/aarch64-linux-gnu/libexpat.so.1.8.10
pulseaudi 118713  zen  mem       REG              179,2    40880      61355 /usr/lib/aarch64-linux-gnu/libthai.so.0.3.1
pulseaudi 118713  zen  mem       REG              179,2   108720      61326 /usr/lib/aarch64-linux-gnu/libfribidi.so.0.4.0
pulseaudi 118713  zen  mem       REG              179,2  1052200      61339 /usr/lib/aarch64-linux-gnu/libharfbuzz.so.0.60000.0
pulseaudi 118713  zen  mem       REG              179,2   132888      61367 /usr/lib/aarch64-linux-gnu/libpangoft2-1.0.so.0.5000.12
pulseaudi 118713  zen  mem       REG              179,2  2099352       5747 /usr/lib/aarch64-linux-gnu/libicuuc.so.72.1
pulseaudi 118713  zen  mem       REG              179,2   198800       5882 /usr/lib/aarch64-linux-gnu/libselinux.so.1
pulseaudi 118713  zen  mem       REG              179,2   461432       5796 /usr/lib/aarch64-linux-gnu/libmount.so.1.1.0
pulseaudi 118713  zen  mem       REG              179,2   395264       5757 /usr/lib/aarch64-linux-gnu/libjpeg.so.62.3.0
pulseaudi 118713  zen  mem       REG              179,2    67584       5725 /usr/lib/aarch64-linux-gnu/libgmodule-2.0.so.0.7400.6
pulseaudi 118713  zen  mem       REG              179,2    67608      61600 /usr/lib/aarch64-linux-gnu/libxcb-dri3.so.0.1.0
pulseaudi 118713  zen  mem       REG              179,2    67640      61606 /usr/lib/aarch64-linux-gnu/libXfixes.so.3.1.0
pulseaudi 118713  zen  mem       REG              179,2    68656       5835 /usr/lib/aarch64-linux-gnu/libnuma.so.1.0.0
pulseaudi 118713  zen  mem       REG              179,2   406248      61062 /usr/lib/aarch64-linux-gnu/liblcms2.so.2.0.14
pulseaudi 118713  zen  mem       REG              179,2   591864       5645 /usr/lib/aarch64-linux-gnu/libbrotlienc.so.1.0.9
pulseaudi 118713  zen  mem       REG              179,2    67528      61166 /usr/lib/aarch64-linux-gnu/libhwy.so.1.0.3
pulseaudi 118713  zen  mem       REG              179,2    67688       5643 /usr/lib/aarch64-linux-gnu/libbrotlidec.so.1.0.9
pulseaudi 118713  zen  mem       REG              179,2  2174296       5897 /usr/lib/aarch64-linux-gnu/libstdc++.so.6.0.30
pulseaudi 118713  zen  mem       REG              179,2   134696       5529 /usr/lib/aarch64-linux-gnu/libXext.so.6.4.0
pulseaudi 118713  zen  mem       REG              179,2    43408      61142 /usr/lib/aarch64-linux-gnu/libXrender.so.1.3.0
pulseaudi 118713  zen  mem       REG              179,2    67784      61130 /usr/lib/aarch64-linux-gnu/libxcb-render.so.0.0.0
pulseaudi 118713  zen  mem       REG              179,2    67576      61136 /usr/lib/aarch64-linux-gnu/libxcb-shm.so.0.0.0
pulseaudi 118713  zen  mem       REG              179,2   264040       5858 /usr/lib/aarch64-linux-gnu/libpng16.so.16.39.0
pulseaudi 118713  zen  mem       REG              179,2   788568       5713 /usr/lib/aarch64-linux-gnu/libfreetype.so.6.18.3
pulseaudi 118713  zen  mem       REG              179,2   330656       5706 /usr/lib/aarch64-linux-gnu/libfontconfig.so.1.12.0
pulseaudi 118713  zen  mem       REG              179,2   657360      61123 /usr/lib/aarch64-linux-gnu/libpixman-1.so.0.42.2
pulseaudi 118713  zen  mem       REG              179,2   592440       5849 /usr/lib/aarch64-linux-gnu/libpcre2-8.so.0.11.2
pulseaudi 118713  zen  mem       REG              179,2    68000       5700 /usr/lib/aarch64-linux-gnu/libffi.so.8.1.2
pulseaudi 118713  zen  mem       REG              179,2   133448       5718 /usr/lib/aarch64-linux-gnu/libgcc_s.so.1
pulseaudi 118713  zen  mem       REG              179,2   462192      61361 /usr/lib/aarch64-linux-gnu/libpango-1.0.so.0.5000.12
pulseaudi 118713  zen  mem       REG              179,2    67472      61373 /usr/lib/aarch64-linux-gnu/libpangocairo-1.0.so.0.5000.12
pulseaudi 118713  zen  mem       REG              179,2  1708736       5936 /usr/lib/aarch64-linux-gnu/libxml2.so.2.9.14
pulseaudi 118713  zen  mem       REG              179,2  2100616       5723 /usr/lib/aarch64-linux-gnu/libgio-2.0.so.0.7400.6
pulseaudi 118713  zen  mem       REG              179,2   198760      61296 /usr/lib/aarch64-linux-gnu/libgdk_pixbuf-2.0.so.0.4200.10
pulseaudi 118713  zen  mem       REG              179,2    67272      61184 /usr/lib/aarch64-linux-gnu/libcairo-gobject.so.2.11600.0
pulseaudi 118713  zen  mem       REG              179,2    67528       5866 /usr/lib/aarch64-linux-gnu/libpthread.so.0
pulseaudi 118713  zen  mem       REG              179,2    67528       5681 /usr/lib/aarch64-linux-gnu/libdl.so.2
pulseaudi 118713  zen  mem       REG              179,2    69048      61626 /usr/lib/aarch64-linux-gnu/libOpenCL.so.1.0.0
pulseaudi 118713  zen  mem       REG              179,2   133896       5683 /usr/lib/aarch64-linux-gnu/libdrm.so.2.4.0
pulseaudi 118713  zen  mem       REG              179,2    67520      61619 /usr/lib/aarch64-linux-gnu/libvdpau.so.1.0.0
pulseaudi 118713  zen  mem       REG              179,2    68096      61612 /usr/lib/aarch64-linux-gnu/libva-x11.so.2.1700.0
pulseaudi 118713  zen  mem       REG              179,2    67672      61594 /usr/lib/aarch64-linux-gnu/libva-drm.so.2.1700.0
pulseaudi 118713  zen  mem       REG              179,2   199088      61588 /usr/lib/aarch64-linux-gnu/libva.so.2.1700.0
pulseaudi 118713  zen  mem       REG              179,2   453312      61731 /usr/lib/aarch64-linux-gnu/libxvidcore.so.4.3
pulseaudi 118713  zen  mem       REG              179,2  2828696       5934 /usr/lib/aarch64-linux-gnu/libx265.so.199
pulseaudi 118713  zen  mem       REG              179,2  1379576      61726 /usr/lib/aarch64-linux-gnu/libx264.so.164
pulseaudi 118713  zen  mem       REG              179,2   120680      61707 /usr/lib/aarch64-linux-gnu/libtwolame.so.0.0.0
pulseaudi 118713  zen  mem       REG              179,2   133200      61698 /usr/lib/aarch64-linux-gnu/libtheoradec.so.1.1.4
pulseaudi 118713  zen  mem       REG              179,2   198736      61699 /usr/lib/aarch64-linux-gnu/libtheoraenc.so.1.1.2
pulseaudi 118713  zen  mem       REG              179,2  3251568       5525 /usr/lib/aarch64-linux-gnu/libSvtAv1Enc.so.1.4.1
pulseaudi 118713  zen  mem       REG              179,2   132968      61678 /usr/lib/aarch64-linux-gnu/libspeex.so.1.5.2
pulseaudi 118713  zen  mem       REG              179,2  1902752       5872 /usr/lib/aarch64-linux-gnu/librav1e.so.0.5.1
pulseaudi 118713  zen  mem       REG              179,2 16833104      61643 /usr/lib/aarch64-linux-gnu/libcodec2.so.1.0
pulseaudi 118713  zen  mem       REG              179,2  3629312       5599 /usr/lib/aarch64-linux-gnu/libaom.so.3.6.0
pulseaudi 118713  zen  mem       REG              179,2  9903480      61379 /usr/lib/aarch64-linux-gnu/librsvg-2.so.2.48.0
pulseaudi 118713  zen  mem       REG              179,2 12591384      60831 /usr/lib/aarch64-linux-gnu/libavcodec.so.59.37.100
pulseaudi 118713  zen  mem       REG              179,2   129418      89534 /usr/share/locale/en_GB/LC_MESSAGES/glib20.mo
pulseaudi 118713  zen  mem       REG              179,2    38904      61666 /usr/lib/aarch64-linux-gnu/libshine.so.3.0.1
pulseaudi 118713  zen  mem       REG              179,2   395664      61074 /usr/lib/aarch64-linux-gnu/libopenjp2.so.2.5.0
pulseaudi 118713  zen  mem       REG              179,2    67776      61177 /usr/lib/aarch64-linux-gnu/libjxl_threads.so.0.7.0
pulseaudi 118713  zen  mem       REG              179,2  1641632      61176 /usr/lib/aarch64-linux-gnu/libjxl.so.0.7.0
pulseaudi 118713  zen  mem       REG              179,2    67504      61648 /usr/lib/aarch64-linux-gnu/libgsm.so.1.0.19
pulseaudi 118713  zen  mem       REG              179,2    67912      61672 /usr/lib/aarch64-linux-gnu/libsnappy.so.1.1.9
pulseaudi 118713  zen  mem       REG              179,2   133520       5942 /usr/lib/aarch64-linux-gnu/libz.so.1.2.13
pulseaudi 118713  zen  mem       REG              179,2   572496      61751 /usr/lib/aarch64-linux-gnu/libzvbi.so.0.13.2
pulseaudi 118713  zen  mem       REG              179,2  1183080      61148 /usr/lib/aarch64-linux-gnu/libcairo.so.2.11600.0
pulseaudi 118713  zen  mem       REG              179,2  1314544       5724 /usr/lib/aarch64-linux-gnu/libglib-2.0.so.0.7400.6
pulseaudi 118713  zen  mem       REG              179,2   462704       5728 /usr/lib/aarch64-linux-gnu/libgobject-2.0.so.0.7400.6
pulseaudi 118713  zen  mem       REG              179,2   724912       5670 /usr/lib/aarch64-linux-gnu/libdav1d.so.6.6.0
pulseaudi 118713  zen  mem       REG              179,2   395832       5932 /usr/lib/aarch64-linux-gnu/libwebp.so.7.1.5
pulseaudi 118713  zen  mem       REG              179,2    67792      61086 /usr/lib/aarch64-linux-gnu/libwebpmux.so.3.0.10
pulseaudi 118713  zen  mem       REG              179,2  2099296      61719 /usr/lib/aarch64-linux-gnu/libvpx.so.7.1.0
pulseaudi 118713  zen  mem       REG              179,2   133048      61690 /usr/lib/aarch64-linux-gnu/libswresample.so.4.7.100
pulseaudi 118713  zen  mem       REG              179,2   790208      61636 /usr/lib/aarch64-linux-gnu/libavutil.so.57.28.100
pulseaudi 118713  zen  mem       REG              179,2    67744     290095 /usr/lib/aarch64-linux-gnu/alsa-lib/libasound_module_pcm_a52.so
pulseaudi 118713  zen  mem       REG              179,2  1116648       5605 /usr/lib/aarch64-linux-gnu/libasound.so.2.0.0
pulseaudi 118713  zen  mem       REG              179,2   331640     290142 /usr/lib/pulse-16.1+dfsg1/modules/libalsa-util.so
pulseaudi 118713  zen  mem       REG              179,2    67592     290152 /usr/lib/pulse-16.1+dfsg1/modules/module-alsa-card.so
pulseaudi 118713  zen  mem       REG              179,2   199104       5911 /usr/lib/aarch64-linux-gnu/libudev.so.1.7.5
pulseaudi 118713  zen  mem       REG              179,2    67592     290209 /usr/lib/pulse-16.1+dfsg1/modules/module-udev-detect.so
pulseaudi 118713  zen  mem       REG              179,2    67512     290203 /usr/lib/pulse-16.1+dfsg1/modules/module-switch-on-port-available.so
pulseaudi 118713  zen  mem       REG              179,2    67736     290157 /usr/lib/pulse-16.1+dfsg1/modules/module-augment-properties.so
pulseaudi 118713  zen  mem       REG              179,2    67592     290158 /usr/lib/pulse-16.1+dfsg1/modules/module-card-restore.so
pulseaudi 118713  zen  mem       REG              179,2   134008     290200 /usr/lib/pulse-16.1+dfsg1/modules/module-stream-restore.so
pulseaudi 118713  zen  mem       REG              179,2   198664     290147 /usr/lib/pulse-16.1+dfsg1/modules/libprotocol-native.so
pulseaudi 118713  zen  mem       REG              179,2    67592     290168 /usr/lib/pulse-16.1+dfsg1/modules/module-device-restore.so
pulseaudi 118713  zen  DEL       REG                0,1                2056 /memfd:pulseaudio
pulseaudi 118713  zen  mem       REG              179,2  6209216       1752 /usr/lib/locale/locale-archive
pulseaudi 118713  zen  mem       REG              179,2    68232       5875 /usr/lib/aarch64-linux-gnu/libresolv.so.2
pulseaudi 118713  zen  mem       REG              179,2    67432       5760 /usr/lib/aarch64-linux-gnu/libkeyutils.so.1.10
pulseaudi 118713  zen  mem       REG              179,2    68576       5765 /usr/lib/aarch64-linux-gnu/libkrb5support.so.0.1
pulseaudi 118713  zen  mem       REG              179,2    67432       5660 /usr/lib/aarch64-linux-gnu/libcom_err.so.2.1
pulseaudi 118713  zen  mem       REG              179,2   199352       5759 /usr/lib/aarch64-linux-gnu/libk5crypto.so.3.1
pulseaudi 118713  zen  mem       REG              179,2   928736       5764 /usr/lib/aarch64-linux-gnu/libkrb5.so.3.3
pulseaudi 118713  zen  mem       REG              179,2   334904       5735 /usr/lib/aarch64-linux-gnu/libgssapi_krb5.so.2.2
pulseaudi 118713  zen  mem       REG              179,2    67704       5791 /usr/lib/aarch64-linux-gnu/libmd.so.0.0.5
pulseaudi 118713  zen  mem       REG              179,2   198960       5907 /usr/lib/aarch64-linux-gnu/libtirpc.so.3.0.0
pulseaudi 118713  zen  mem       REG              179,2   133944       5646 /usr/lib/aarch64-linux-gnu/libbsd.so.0.11.7
pulseaudi 118713  zen  mem       REG              179,2   198640       5730 /usr/lib/aarch64-linux-gnu/libgpg-error.so.0.33.1
pulseaudi 118713  zen  mem       REG              179,2    89376       5817 /usr/lib/aarch64-linux-gnu/libnsl.so.2.0.1
pulseaudi 118713  zen  mem       REG              179,2    22576       5528 /usr/lib/aarch64-linux-gnu/libXdmcp.so.6.0.0
pulseaudi 118713  zen  mem       REG              179,2    14416       5527 /usr/lib/aarch64-linux-gnu/libXau.so.6.0.0
pulseaudi 118713  zen  mem       REG              179,2   331264       5729 /usr/lib/aarch64-linux-gnu/libgomp.so.1.0.0
pulseaudi 118713  zen  mem       REG              179,2   329616      61654 /usr/lib/aarch64-linux-gnu/libmp3lame.so.0.0.0
pulseaudi 118713  zen  mem       REG              179,2   332024      61151 /usr/lib/aarch64-linux-gnu/libmpg123.so.0.47.0
pulseaudi 118713  zen  mem       REG              179,2    67352       5836 /usr/lib/aarch64-linux-gnu/libogg.so.0.8.5
pulseaudi 118713  zen  mem       REG              179,2   395672      61660 /usr/lib/aarch64-linux-gnu/libopus.so.0.8.0
pulseaudi 118713  zen  mem       REG              179,2   653216      61713 /usr/lib/aarch64-linux-gnu/libvorbisenc.so.2.0.12
pulseaudi 118713  zen  mem       REG              179,2   165736       5930 /usr/lib/aarch64-linux-gnu/libvorbis.so.0.4.9
pulseaudi 118713  zen  mem       REG              179,2   329592       5416 /usr/lib/aarch64-linux-gnu/libFLAC.so.12.0.0
pulseaudi 118713  zen  mem       REG              179,2   199056       5783 /usr/lib/aarch64-linux-gnu/liblz4.so.1.9.4
pulseaudi 118713  zen  mem       REG              179,2   657352       5943 /usr/lib/aarch64-linux-gnu/libzstd.so.1.5.4
pulseaudi 118713  zen  mem       REG              179,2   198584       5784 /usr/lib/aarch64-linux-gnu/liblzma.so.5.4.1
pulseaudi 118713  zen  mem       REG              179,2  1000296       5719 /usr/lib/aarch64-linux-gnu/libgcrypt.so.20.4.1
pulseaudi 118713  zen  mem       REG              179,2    67352      61712 /usr/lib/aarch64-linux-gnu/libasyncns.so.0.3.1
pulseaudi 118713  zen  mem       REG              179,2    68344       5933 /usr/lib/aarch64-linux-gnu/libwrap.so.0.7.6
pulseaudi 118713  zen  mem       REG              179,2   199544       5935 /usr/lib/aarch64-linux-gnu/libxcb.so.1.1.0
pulseaudi 118713  zen  mem       REG              179,2  1329712       5526 /usr/lib/aarch64-linux-gnu/libX11.so.6.4.0
pulseaudi 118713  zen  mem       REG              179,2    67216      61546 /usr/lib/aarch64-linux-gnu/libX11-xcb.so.1.0.0
pulseaudi 118713  zen  mem       REG              179,2    67432      67059 /usr/lib/aarch64-linux-gnu/libspeexdsp.so.1.5.2
pulseaudi 118713  zen  mem       REG              179,2   137552      61684 /usr/lib/aarch64-linux-gnu/libsoxr.so.0.1.2
pulseaudi 118713  zen  mem       REG              179,2   672504      66985 /usr/lib/aarch64-linux-gnu/liborc-0.4.so.0.33.0
pulseaudi 118713  zen  mem       REG              179,2   133064      61485 /usr/lib/aarch64-linux-gnu/libtdb.so.1.4.8
pulseaudi 118713  zen  mem       REG              179,2   595024      61725 /usr/lib/aarch64-linux-gnu/libsndfile.so.1.0.35
pulseaudi 118713  zen  mem       REG              179,2   591960       5786 /usr/lib/aarch64-linux-gnu/libm.so.6
pulseaudi 118713  zen  mem       REG              179,2  1651472       5650 /usr/lib/aarch64-linux-gnu/libc.so.6
pulseaudi 118713  zen  mem       REG              179,2   858152       5898 /usr/lib/aarch64-linux-gnu/libsystemd.so.0.35.0
pulseaudi 118713  zen  mem       REG              179,2   395336       5672 /usr/lib/aarch64-linux-gnu/libdbus-1.so.3.32.4
pulseaudi 118713  zen  mem       REG              179,2    67704       5657 /usr/lib/aarch64-linux-gnu/libcap.so.2.66
pulseaudi 118713  zen  mem       REG              179,2    68080      59564 /usr/lib/aarch64-linux-gnu/libltdl.so.7.3.2
pulseaudi 118713  zen  mem       REG              179,2   330728      61747 /usr/lib/aarch64-linux-gnu/libpulse.so.0.24.2
pulseaudi 118713  zen  mem       REG              179,2   526456     279648 /usr/lib/aarch64-linux-gnu/pulseaudio/libpulsecommon-16.1.so
pulseaudi 118713  zen  mem       REG              179,2    10839      66943 /usr/share/locale/en_GB/LC_MESSAGES/gstreamer-1.0.mo
pulseaudi 118713  zen  mem       REG              179,2    16384    1159182 /home/zen/.config/pulse/fe8858a86c914bd2b19ee54188e1245a-card-database.tdb
pulseaudi 118713  zen  mem       REG              179,2      696    1159177 /home/zen/.config/pulse/fe8858a86c914bd2b19ee54188e1245a-stream-volumes.tdb
pulseaudi 118713  zen  mem       REG              179,2   723672     290139 /usr/lib/aarch64-linux-gnu/pulseaudio/libpulsecore-16.1.so
pulseaudi 118713  zen  mem       REG              179,2    12288    1159176 /home/zen/.config/pulse/fe8858a86c914bd2b19ee54188e1245a-device-volumes.tdb
pulseaudi 118713  zen  mem       REG              179,2     1433      26733 /usr/share/locale/en_GB/LC_MESSAGES/libc.mo
pulseaudi 118713  zen  mem       REG              179,2    27028       6263 /usr/lib/aarch64-linux-gnu/gconv/gconv-modules.cache
pulseaudi 118713  zen  mem       REG              179,2   202904       5409 /usr/lib/aarch64-linux-gnu/ld-linux-aarch64.so.1
pulseaudi 118713  zen    0r      CHR                1,3      0t0          5 /dev/null
pulseaudi 118713  zen    1u     unix 0x0000000095ffce40      0t0      90930 type=STREAM (CONNECTED)
pulseaudi 118713  zen    2u     unix 0x0000000095ffce40      0t0      90930 type=STREAM (CONNECTED)
pulseaudi 118713  zen    3u     unix 0x00000000aa541606      0t0      90920 /run/user/1000/pulse/native type=STREAM (LISTEN)
pulseaudi 118713  zen    4r     FIFO               0,12      0t0      89942 pipe
pulseaudi 118713  zen    5w     FIFO               0,12      0t0      89942 pipe
pulseaudi 118713  zen    6u      REG                0,1 67108864       2056 /memfd:pulseaudio (deleted)
pulseaudi 118713  zen    7r     FIFO               0,12      0t0      89943 pipe
pulseaudi 118713  zen    8w     FIFO               0,12      0t0      89943 pipe
pulseaudi 118713  zen   10u      REG              179,2    12288    1159176 /home/zen/.config/pulse/fe8858a86c914bd2b19ee54188e1245a-device-volumes.tdb
pulseaudi 118713  zen   11u      REG              179,2      696    1159177 /home/zen/.config/pulse/fe8858a86c914bd2b19ee54188e1245a-stream-volumes.tdb
pulseaudi 118713  zen   12u      REG              179,2    16384    1159182 /home/zen/.config/pulse/fe8858a86c914bd2b19ee54188e1245a-card-database.tdb
pulseaudi 118713  zen   13r  a_inode               0,13        0       1061 inotify
pulseaudi 118713  zen   14u  netlink                         0t0      89944 KOBJECT_UEVENT
pulseaudi 118713  zen   15u     unix 0x00000000294196ad      0t0      89945 type=STREAM (CONNECTED)
pulseaudi 118713  zen   16u     unix 0x00000000ff80369a      0t0      88045 type=DGRAM (UNCONNECTED)
pulseaudi 118713  zen   17u  a_inode               0,13        0       1061 [eventfd:21]
pulseaudi 118713  zen   18u  a_inode               0,13        0       1061 [eventfd:22]
pulseaudi 118713  zen   19u  a_inode               0,13        0       1061 [eventfd:23]
pulseaudi 118713  zen   20u  a_inode               0,13        0       1061 [eventfd:24]
pulseaudi 118713  zen   21u      CHR              116,7      0t0        606 /dev/snd/controlC2
pulseaudi 118713  zen   24u     unix 0x0000000058ab08da      0t0      88051 type=STREAM (CONNECTED)
pulseaudi 118713  zen   25r     FIFO               0,12      0t0      88052 pipe
pulseaudi 118713  zen   26r  a_inode               0,13        0       1061 inotify
sshd      118727  zen  cwd       DIR              179,2     4096          2 /
sshd      118727  zen  rtd       DIR              179,2     4096          2 /
sshd      118727  zen  txt       REG              179,2  1314416      17930 /usr/sbin/sshd
sshd      118727  zen  mem       REG              179,2    67512      21570 /usr/lib/aarch64-linux-gnu/security/pam_env.so
sshd      118727  zen  mem       REG              179,2    67592      21589 /usr/lib/aarch64-linux-gnu/security/pam_limits.so
sshd      118727  zen  mem       REG              179,2    67512      21602 /usr/lib/aarch64-linux-gnu/security/pam_mail.so
sshd      118727  zen  mem       REG              179,2    67512      21613 /usr/lib/aarch64-linux-gnu/security/pam_motd.so
sshd      118727  zen  mem       REG              179,2    67352      22608 /usr/lib/aarch64-linux-gnu/security/pam_chksshpwd.so
sshd      118727  zen  mem       REG              179,2   591960       5786 /usr/lib/aarch64-linux-gnu/libm.so.6
sshd      118727  zen  mem       REG              179,2    67616      21485 /usr/lib/aarch64-linux-gnu/libpam_misc.so.0.82.1
sshd      118727  zen  mem       REG              179,2   530352       8163 /usr/lib/aarch64-linux-gnu/security/pam_systemd.so
sshd      118727  zen  mem       REG              179,2    67512      21585 /usr/lib/aarch64-linux-gnu/security/pam_keyinit.so
sshd      118727  zen  mem       REG              179,2    67512      21601 /usr/lib/aarch64-linux-gnu/security/pam_loginuid.so
sshd      118727  zen  mem       REG              179,2    67512      21638 /usr/lib/aarch64-linux-gnu/security/pam_selinux.so
sshd      118727  zen  mem       REG              179,2    67512      21627 /usr/lib/aarch64-linux-gnu/security/pam_nologin.so
sshd      118727  zen  mem       REG              179,2    67512      21628 /usr/lib/aarch64-linux-gnu/security/pam_permit.so
sshd      118727  zen  mem       REG              179,2    67288      21568 /usr/lib/aarch64-linux-gnu/security/pam_deny.so
sshd      118727  zen  mem       REG              179,2    67600      21672 /usr/lib/aarch64-linux-gnu/security/pam_unix.so
sshd      118727  zen  mem       REG              179,2   198640       5730 /usr/lib/aarch64-linux-gnu/libgpg-error.so.0.33.1
sshd      118727  zen  mem       REG              179,2   198960       5907 /usr/lib/aarch64-linux-gnu/libtirpc.so.3.0.0
sshd      118727  zen  mem       REG              179,2    68232       5875 /usr/lib/aarch64-linux-gnu/libresolv.so.2
sshd      118727  zen  mem       REG              179,2    67432       5760 /usr/lib/aarch64-linux-gnu/libkeyutils.so.1.10
sshd      118727  zen  mem       REG              179,2    68576       5765 /usr/lib/aarch64-linux-gnu/libkrb5support.so.0.1
sshd      118727  zen  mem       REG              179,2   199352       5759 /usr/lib/aarch64-linux-gnu/libk5crypto.so.3.1
sshd      118727  zen  mem       REG              179,2   592440       5849 /usr/lib/aarch64-linux-gnu/libpcre2-8.so.0.11.2
sshd      118727  zen  mem       REG              179,2   199056       5783 /usr/lib/aarch64-linux-gnu/liblz4.so.1.9.4
sshd      118727  zen  mem       REG              179,2   657352       5943 /usr/lib/aarch64-linux-gnu/libzstd.so.1.5.4
sshd      118727  zen  mem       REG              179,2   198584       5784 /usr/lib/aarch64-linux-gnu/liblzma.so.5.4.1
sshd      118727  zen  mem       REG              179,2  1000296       5719 /usr/lib/aarch64-linux-gnu/libgcrypt.so.20.4.1
sshd      118727  zen  mem       REG              179,2    67704       5657 /usr/lib/aarch64-linux-gnu/libcap.so.2.66
sshd      118727  zen  mem       REG              179,2    67504       5656 /usr/lib/aarch64-linux-gnu/libcap-ng.so.0.0.0
sshd      118727  zen  mem       REG              179,2    89376       5817 /usr/lib/aarch64-linux-gnu/libnsl.so.2.0.1
sshd      118727  zen  mem       REG              179,2  1651472       5650 /usr/lib/aarch64-linux-gnu/libc.so.6
sshd      118727  zen  mem       REG              179,2   133520       5942 /usr/lib/aarch64-linux-gnu/libz.so.1.2.13
sshd      118727  zen  mem       REG              179,2  4466856       3947 /usr/lib/aarch64-linux-gnu/libcrypto.so.3
sshd      118727  zen  mem       REG              179,2    67432       5660 /usr/lib/aarch64-linux-gnu/libcom_err.so.2.1
sshd      118727  zen  mem       REG              179,2   928736       5764 /usr/lib/aarch64-linux-gnu/libkrb5.so.3.3
sshd      118727  zen  mem       REG              179,2   334904       5735 /usr/lib/aarch64-linux-gnu/libgssapi_krb5.so.2.2
sshd      118727  zen  mem       REG              179,2   198800       5882 /usr/lib/aarch64-linux-gnu/libselinux.so.1
sshd      118727  zen  mem       REG              179,2   858152       5898 /usr/lib/aarch64-linux-gnu/libsystemd.so.0.35.0
sshd      118727  zen  mem       REG              179,2    67512      21476 /usr/lib/aarch64-linux-gnu/libpam.so.0.85.1
sshd      118727  zen  mem       REG              179,2   132984       5611 /usr/lib/aarch64-linux-gnu/libaudit.so.1.0.0
sshd      118727  zen  mem       REG              179,2    68344       5933 /usr/lib/aarch64-linux-gnu/libwrap.so.0.7.6
sshd      118727  zen  mem       REG              179,2   198584       5662 /usr/lib/aarch64-linux-gnu/libcrypt.so.1.1.0
sshd      118727  zen  mem       REG              179,2   202904       5409 /usr/lib/aarch64-linux-gnu/ld-linux-aarch64.so.1
sshd      118727  zen    0u      CHR                1,3      0t0          5 /dev/null
sshd      118727  zen    1u      CHR                1,3      0t0          5 /dev/null
sshd      118727  zen    2u      CHR                1,3      0t0          5 /dev/null
sshd      118727  zen    3u     unix 0x000000000210c67f      0t0      89819 type=DGRAM (CONNECTED)
sshd      118727  zen    4u     IPv4              90829      0t0        TCP 192.168.1.5:ssh->192.168.1.11:50927 (ESTABLISHED)
sshd      118727  zen    5u     unix 0x000000003c80b6fa      0t0      89871 type=STREAM (CONNECTED)
sshd      118727  zen    6u     unix 0x00000000f85bba98      0t0      89808 type=STREAM (CONNECTED)
sshd      118727  zen    7u      CHR                5,2      0t0         90 /dev/ptmx
sshd      118727  zen    8w     FIFO               0,20      0t0       1851 /run/systemd/sessions/7.ref
sshd      118727  zen   10u      CHR                5,2      0t0         90 /dev/ptmx
sshd      118727  zen   11u      CHR                5,2      0t0         90 /dev/ptmx
exe       118730  zen  cwd       DIR              179,2     4096        946 /home/zen
exe       118730  zen  rtd       DIR              179,2     4096          2 /
exe       118730  zen  txt       REG              179,2 11681880       9579 /usr/bin/rootlesskit
exe       118730  zen  mem       REG              179,2  1651472       5650 /usr/lib/aarch64-linux-gnu/libc.so.6
exe       118730  zen  mem       REG              179,2   202904       5409 /usr/lib/aarch64-linux-gnu/ld-linux-aarch64.so.1
exe       118730  zen    0r      CHR                1,3      0t0          5 /dev/null
exe       118730  zen    1u     unix 0x00000000e74ffb4b      0t0      89860 type=STREAM (CONNECTED)
exe       118730  zen    2u     unix 0x00000000e74ffb4b      0t0      89860 type=STREAM (CONNECTED)
exe       118730  zen    4u  a_inode               0,13        0       1061 [eventpoll:5,9]
exe       118730  zen    5r     FIFO               0,12      0t0      90967 pipe
exe       118730  zen    6w     FIFO               0,12      0t0      90967 pipe
exe       118730  zen    9u     sock                0,8      0t0      90979 protocol: UNIX-STREAM
bash      118744  zen  cwd       DIR              179,2     4096     253077 /home/zen/container/gitea/gitea
bash      118744  zen  rtd       DIR              179,2     4096          2 /
bash      118744  zen  txt       REG              179,2  1346480       1691 /usr/bin/bash
bash      118744  zen  mem       REG              179,2  6209216       1752 /usr/lib/locale/locale-archive
bash      118744  zen  mem       REG              179,2  1651472       5650 /usr/lib/aarch64-linux-gnu/libc.so.6
bash      118744  zen  mem       REG              179,2   199896       5905 /usr/lib/aarch64-linux-gnu/libtinfo.so.6.4
bash      118744  zen  mem       REG              179,2   202904       5409 /usr/lib/aarch64-linux-gnu/ld-linux-aarch64.so.1
bash      118744  zen  mem       REG              179,2    27028       6263 /usr/lib/aarch64-linux-gnu/gconv/gconv-modules.cache
bash      118744  zen    0u      CHR              136,0      0t0          3 /dev/pts/0
bash      118744  zen    1u      CHR              136,0      0t0          3 /dev/pts/0
bash      118744  zen    2u      CHR              136,0      0t0          3 /dev/pts/0
bash      118744  zen  255u      CHR              136,0      0t0          3 /dev/pts/0
slirp4net 118757  zen  cwd       DIR               0,40       80          1 /
slirp4net 118757  zen  rtd       DIR               0,40       80          1 /
slirp4net 118757  zen  txt       REG              179,2   134848      60180 /usr/bin/slirp4netns
slirp4net 118757  zen  mem       REG              179,2   591960       5786 /usr/lib/aarch64-linux-gnu/libm.so.6
slirp4net 118757  zen  mem       REG              179,2   592440       5849 /usr/lib/aarch64-linux-gnu/libpcre2-8.so.0.11.2
slirp4net 118757  zen  mem       REG              179,2  1651472       5650 /usr/lib/aarch64-linux-gnu/libc.so.6
slirp4net 118757  zen  mem       REG              179,2    67528       5866 /usr/lib/aarch64-linux-gnu/libpthread.so.0
slirp4net 118757  zen  mem       REG              179,2   133328       5881 /usr/lib/aarch64-linux-gnu/libseccomp.so.2.5.4
slirp4net 118757  zen  mem       REG              179,2   133040      59700 /usr/lib/aarch64-linux-gnu/libslirp.so.0.4.0
slirp4net 118757  zen  mem       REG              179,2  1314544       5724 /usr/lib/aarch64-linux-gnu/libglib-2.0.so.0.7400.6
slirp4net 118757  zen  mem       REG              179,2   202904       5409 /usr/lib/aarch64-linux-gnu/ld-linux-aarch64.so.1
slirp4net 118757  zen    0r      CHR                1,3      0t0          5 /dev/null
slirp4net 118757  zen    1w     FIFO               0,12      0t0      90962 pipe
slirp4net 118757  zen    2w     FIFO               0,12      0t0      90962 pipe
slirp4net 118757  zen    5u     unix 0x00000000e6941d2b      0t0      91333 type=STREAM (CONNECTED)
slirp4net 118757  zen    6u      CHR             10,200     0t70        451 /dev/net/tun
dockerd   118780  zen  cwd       DIR              179,2     4096        946 /home/zen
dockerd   118780  zen  rtd       DIR              179,2     4096          2 /
dockerd   118780  zen  txt       REG              179,2 65849424       9569 /usr/bin/dockerd
dockerd   118780  zen  mem       REG              179,2   592440       5849 /usr/lib/aarch64-linux-gnu/libpcre2-8.so.0.11.2
dockerd   118780  zen  mem       REG              179,2   198640       5730 /usr/lib/aarch64-linux-gnu/libgpg-error.so.0.33.1
dockerd   118780  zen  mem       REG              179,2   591960       5786 /usr/lib/aarch64-linux-gnu/libm.so.6
dockerd   118780  zen  mem       REG              179,2   199104       5911 /usr/lib/aarch64-linux-gnu/libudev.so.1.7.5
dockerd   118780  zen  mem       REG              179,2   198800       5882 /usr/lib/aarch64-linux-gnu/libselinux.so.1
dockerd   118780  zen  mem       REG              179,2   199056       5783 /usr/lib/aarch64-linux-gnu/liblz4.so.1.9.4
dockerd   118780  zen  mem       REG              179,2   657352       5943 /usr/lib/aarch64-linux-gnu/libzstd.so.1.5.4
dockerd   118780  zen  mem       REG              179,2   198584       5784 /usr/lib/aarch64-linux-gnu/liblzma.so.5.4.1
dockerd   118780  zen  mem-W     REG              179,2    16384     250957 /home/zen/.local/share/docker/buildkit/history.db
dockerd   118780  zen  mem       REG              179,2  1000296       5719 /usr/lib/aarch64-linux-gnu/libgcrypt.so.20.4.1
dockerd   118780  zen  mem-W     REG              179,2    32768     250956 /home/zen/.local/share/docker/buildkit/cache.db
dockerd   118780  zen  mem       REG              179,2    67704       5657 /usr/lib/aarch64-linux-gnu/libcap.so.2.66
dockerd   118780  zen  mem-W     REG              179,2    16384     250954 /home/zen/.local/share/docker/buildkit/metadata_v2.db
dockerd   118780  zen  mem       REG              179,2  1651472       5650 /usr/lib/aarch64-linux-gnu/libc.so.6
dockerd   118780  zen  mem       REG              179,2   471280       5679 /usr/lib/aarch64-linux-gnu/libdevmapper.so.1.02.1
dockerd   118780  zen  mem-W     REG              179,2    16384     250953 /home/zen/.local/share/docker/buildkit/snapshots.db
dockerd   118780  zen  mem       REG              179,2   858152       5898 /usr/lib/aarch64-linux-gnu/libsystemd.so.0.35.0
dockerd   118780  zen  mem-W     REG              179,2    16384     250952 /home/zen/.local/share/docker/buildkit/containerdmeta.db
dockerd   118780  zen  mem       REG              179,2   202904       5409 /usr/lib/aarch64-linux-gnu/ld-linux-aarch64.so.1
dockerd   118780  zen  mem-W     REG              179,2    32768     250931 /home/zen/.local/share/docker/volumes/metadata.db
dockerd   118780  zen    0r      CHR                1,3      0t0          5 /dev/null
dockerd   118780  zen    1u     unix 0x00000000e74ffb4b      0t0      89860 type=STREAM (CONNECTED)
dockerd   118780  zen    2u     unix 0x00000000e74ffb4b      0t0      89860 type=STREAM (CONNECTED)
dockerd   118780  zen    3u     sock                0,8      0t0      91410 protocol: UNIX-STREAM
dockerd   118780  zen    4u  a_inode               0,13        0       1061 [eventpoll:3,5,7,8,9,10,16]
dockerd   118780  zen    5r     FIFO               0,12      0t0      87999 pipe
dockerd   118780  zen    6w     FIFO               0,12      0t0      87999 pipe
dockerd   118780  zen    7u     sock                0,8      0t0      91008 protocol: UNIX-STREAM
dockerd   118780  zen    8u     sock                0,8      0t0      91427 protocol: UNIX-STREAM
dockerd   118780  zen    9u     sock                0,8      0t0      91429 protocol: UNIX-STREAM
dockerd   118780  zen   10u     sock                0,8      0t0      91009 protocol: UNIX-STREAM
dockerd   118780  zen   11uW     REG              179,2    32768     250931 /home/zen/.local/share/docker/volumes/metadata.db
dockerd   118780  zen   12r      REG                0,4        0 4026532753 net
dockerd   118780  zen   13u     sock                0,8      0t0      90023 protocol: NETLINK
dockerd   118780  zen   14u     sock                0,8      0t0      90024 protocol: NETLINK
dockerd   118780  zen   15u     sock                0,8      0t0      90025 protocol: NETLINK
dockerd   118780  zen   16u     sock                0,8      0t0      92213 protocol: UNIX-STREAM
dockerd   118780  zen   17uW     REG              179,2    16384     250952 /home/zen/.local/share/docker/buildkit/containerdmeta.db
dockerd   118780  zen   18uW     REG              179,2    16384     250953 /home/zen/.local/share/docker/buildkit/snapshots.db
dockerd   118780  zen   19uW     REG              179,2    16384     250954 /home/zen/.local/share/docker/buildkit/metadata_v2.db
dockerd   118780  zen   20uW     REG              179,2    32768     250956 /home/zen/.local/share/docker/buildkit/cache.db
dockerd   118780  zen   21uW     REG              179,2    16384     250957 /home/zen/.local/share/docker/buildkit/history.db
container 118815  zen  cwd       DIR              179,2     4096        946 /home/zen
container 118815  zen  rtd       DIR              179,2     4096          2 /
container 118815  zen  txt       REG              179,2 39243472       6634 /usr/bin/containerd
container 118815  zen  mem-W     REG              179,2   262144     250920 /home/zen/.local/share/docker/containerd/daemon/io.containerd.metadata.v1.bolt/meta.db
container 118815  zen  mem       REG              179,2  1651472       5650 /usr/lib/aarch64-linux-gnu/libc.so.6
container 118815  zen  mem       REG              179,2   202904       5409 /usr/lib/aarch64-linux-gnu/ld-linux-aarch64.so.1
container 118815  zen    0r      CHR                1,3      0t0          5 /dev/null
container 118815  zen    1u     unix 0x00000000e74ffb4b      0t0      89860 type=STREAM (CONNECTED)
container 118815  zen    2u     unix 0x00000000e74ffb4b      0t0      89860 type=STREAM (CONNECTED)
container 118815  zen    3uW     REG              179,2   262144     250920 /home/zen/.local/share/docker/containerd/daemon/io.containerd.metadata.v1.bolt/meta.db
container 118815  zen    4u  a_inode               0,13        0       1061 [eventpoll:5,7,8,9,10,11,12]
container 118815  zen    5r     FIFO               0,12      0t0      91413 pipe
container 118815  zen    6w     FIFO               0,12      0t0      91413 pipe
container 118815  zen    7u     sock                0,8      0t0      91005 protocol: UNIX-STREAM
container 118815  zen    8u     sock                0,8      0t0      91006 protocol: UNIX-STREAM
container 118815  zen    9u     sock                0,8      0t0      91007 protocol: UNIX-STREAM
container 118815  zen   10u     sock                0,8      0t0      88019 protocol: UNIX-STREAM
container 118815  zen   11u     sock                0,8      0t0      88021 protocol: UNIX-STREAM
container 118815  zen   12u     sock                0,8      0t0      89937 protocol: UNIX-STREAM
dbus-daem 118845  zen  cwd       DIR              179,2     4096        946 /home/zen
dbus-daem 118845  zen  rtd       DIR              179,2     4096          2 /
dbus-daem 118845  zen  txt       REG              179,2   264600       1759 /usr/bin/dbus-daemon
dbus-daem 118845  zen  mem       REG              179,2   198640       5730 /usr/lib/aarch64-linux-gnu/libgpg-error.so.0.33.1
dbus-daem 118845  zen  mem       REG              179,2   592440       5849 /usr/lib/aarch64-linux-gnu/libpcre2-8.so.0.11.2
dbus-daem 118845  zen  mem       REG              179,2   199056       5783 /usr/lib/aarch64-linux-gnu/liblz4.so.1.9.4
dbus-daem 118845  zen  mem       REG              179,2   657352       5943 /usr/lib/aarch64-linux-gnu/libzstd.so.1.5.4
dbus-daem 118845  zen  mem       REG              179,2   198584       5784 /usr/lib/aarch64-linux-gnu/liblzma.so.5.4.1
dbus-daem 118845  zen  mem       REG              179,2  1000296       5719 /usr/lib/aarch64-linux-gnu/libgcrypt.so.20.4.1
dbus-daem 118845  zen  mem       REG              179,2    67704       5657 /usr/lib/aarch64-linux-gnu/libcap.so.2.66
dbus-daem 118845  zen  mem       REG              179,2  1651472       5650 /usr/lib/aarch64-linux-gnu/libc.so.6
dbus-daem 118845  zen  mem       REG              179,2   133752       5600 /usr/lib/aarch64-linux-gnu/libapparmor.so.1.8.4
dbus-daem 118845  zen  mem       REG              179,2    67504       5656 /usr/lib/aarch64-linux-gnu/libcap-ng.so.0.0.0
dbus-daem 118845  zen  mem       REG              179,2   132984       5611 /usr/lib/aarch64-linux-gnu/libaudit.so.1.0.0
dbus-daem 118845  zen  mem       REG              179,2   198800       5882 /usr/lib/aarch64-linux-gnu/libselinux.so.1
dbus-daem 118845  zen  mem       REG              179,2   198752       5695 /usr/lib/aarch64-linux-gnu/libexpat.so.1.8.10
dbus-daem 118845  zen  mem       REG              179,2   858152       5898 /usr/lib/aarch64-linux-gnu/libsystemd.so.0.35.0
dbus-daem 118845  zen  mem       REG              179,2   395336       5672 /usr/lib/aarch64-linux-gnu/libdbus-1.so.3.32.4
dbus-daem 118845  zen  mem       REG              179,2   202904       5409 /usr/lib/aarch64-linux-gnu/ld-linux-aarch64.so.1
dbus-daem 118845  zen    0u      CHR                1,3      0t0          5 /dev/null
dbus-daem 118845  zen    1u     unix 0x000000007b50d8ec      0t0      91011 type=STREAM (CONNECTED)
dbus-daem 118845  zen    2u     unix 0x000000007b50d8ec      0t0      91011 type=STREAM (CONNECTED)
dbus-daem 118845  zen    3u     unix 0x0000000095287989      0t0      90904 /run/user/1000/bus type=STREAM (LISTEN)
dbus-daem 118845  zen    4u  a_inode               0,13        0       1061 [eventpoll:3,5,6,8,9,10]
dbus-daem 118845  zen    5r  a_inode               0,13        0       1061 inotify
dbus-daem 118845  zen    6u     unix 0x000000009cb1d5bb      0t0      91024 type=STREAM (CONNECTED)
dbus-daem 118845  zen    7u     unix 0x00000000079e02b0      0t0      91025 type=STREAM (CONNECTED)
dbus-daem 118845  zen    8u     unix 0x00000000430fb6e3      0t0      91027 /run/user/1000/bus type=STREAM (CONNECTED)
dbus-daem 118845  zen    9u     unix 0x00000000831b07e9      0t0      91028 /run/user/1000/bus type=STREAM (CONNECTED)
dbus-daem 118845  zen   10u     unix 0x00000000a4436d9a      0t0      91112 /run/user/1000/bus type=STREAM (CONNECTED)
gsettings 118906  zen  cwd       DIR              179,2     4096          2 /
gsettings 118906  zen  rtd       DIR              179,2     4096          2 /
gsettings 118906  zen  txt       REG              179,2    67688    1155150 /usr/libexec/pulse/gsettings-helper
gsettings 118906  zen  mem       REG              179,2   132968      67513 /usr/lib/aarch64-linux-gnu/gio/modules/libdconfsettings.so
gsettings 118906  zen  mem       REG              179,2    67704       5791 /usr/lib/aarch64-linux-gnu/libmd.so.0.0.5
gsettings 118906  zen  mem       REG              179,2   198640       5730 /usr/lib/aarch64-linux-gnu/libgpg-error.so.0.33.1
gsettings 118906  zen  mem       REG              179,2   133944       5646 /usr/lib/aarch64-linux-gnu/libbsd.so.0.11.7
gsettings 118906  zen  mem       REG              179,2   396248       5630 /usr/lib/aarch64-linux-gnu/libblkid.so.1.1.0
gsettings 118906  zen  mem       REG              179,2   199056       5783 /usr/lib/aarch64-linux-gnu/liblz4.so.1.9.4
gsettings 118906  zen  mem       REG              179,2   657352       5943 /usr/lib/aarch64-linux-gnu/libzstd.so.1.5.4
gsettings 118906  zen  mem       REG              179,2   198584       5784 /usr/lib/aarch64-linux-gnu/liblzma.so.5.4.1
gsettings 118906  zen  mem       REG              179,2  1000296       5719 /usr/lib/aarch64-linux-gnu/libgcrypt.so.20.4.1
gsettings 118906  zen  mem       REG              179,2    67704       5657 /usr/lib/aarch64-linux-gnu/libcap.so.2.66
gsettings 118906  zen  mem       REG              179,2    22576       5528 /usr/lib/aarch64-linux-gnu/libXdmcp.so.6.0.0
gsettings 118906  zen  mem       REG              179,2    14416       5527 /usr/lib/aarch64-linux-gnu/libXau.so.6.0.0
gsettings 118906  zen  mem       REG              179,2   329616      61654 /usr/lib/aarch64-linux-gnu/libmp3lame.so.0.0.0
gsettings 118906  zen  mem       REG              179,2   332024      61151 /usr/lib/aarch64-linux-gnu/libmpg123.so.0.47.0
gsettings 118906  zen  mem       REG              179,2    67352       5836 /usr/lib/aarch64-linux-gnu/libogg.so.0.8.5
gsettings 118906  zen  mem       REG              179,2   395672      61660 /usr/lib/aarch64-linux-gnu/libopus.so.0.8.0
gsettings 118906  zen  mem       REG              179,2   653216      61713 /usr/lib/aarch64-linux-gnu/libvorbisenc.so.2.0.12
gsettings 118906  zen  mem       REG              179,2   165736       5930 /usr/lib/aarch64-linux-gnu/libvorbis.so.0.4.9
gsettings 118906  zen  mem       REG              179,2   329592       5416 /usr/lib/aarch64-linux-gnu/libFLAC.so.12.0.0
gsettings 118906  zen  mem       REG              179,2   592440       5849 /usr/lib/aarch64-linux-gnu/libpcre2-8.so.0.11.2
gsettings 118906  zen  mem       REG              179,2    68000       5700 /usr/lib/aarch64-linux-gnu/libffi.so.8.1.2
gsettings 118906  zen  mem       REG              179,2   198800       5882 /usr/lib/aarch64-linux-gnu/libselinux.so.1
gsettings 118906  zen  mem       REG              179,2   461432       5796 /usr/lib/aarch64-linux-gnu/libmount.so.1.1.0
gsettings 118906  zen  mem       REG              179,2   133520       5942 /usr/lib/aarch64-linux-gnu/libz.so.1.2.13
gsettings 118906  zen  mem       REG              179,2    67584       5725 /usr/lib/aarch64-linux-gnu/libgmodule-2.0.so.0.7400.6
gsettings 118906  zen  mem       REG              179,2    67352      61712 /usr/lib/aarch64-linux-gnu/libasyncns.so.0.3.1
gsettings 118906  zen  mem       REG              179,2   858152       5898 /usr/lib/aarch64-linux-gnu/libsystemd.so.0.35.0
gsettings 118906  zen  mem       REG              179,2   199544       5935 /usr/lib/aarch64-linux-gnu/libxcb.so.1.1.0
gsettings 118906  zen  mem       REG              179,2  1329712       5526 /usr/lib/aarch64-linux-gnu/libX11.so.6.4.0
gsettings 118906  zen  mem       REG              179,2    67216      61546 /usr/lib/aarch64-linux-gnu/libX11-xcb.so.1.0.0
gsettings 118906  zen  mem       REG              179,2   395336       5672 /usr/lib/aarch64-linux-gnu/libdbus-1.so.3.32.4
gsettings 118906  zen  mem       REG              179,2   595024      61725 /usr/lib/aarch64-linux-gnu/libsndfile.so.1.0.35
gsettings 118906  zen  mem       REG              179,2   591960       5786 /usr/lib/aarch64-linux-gnu/libm.so.6
gsettings 118906  zen  mem       REG              179,2  1651472       5650 /usr/lib/aarch64-linux-gnu/libc.so.6
gsettings 118906  zen  mem       REG              179,2  1314544       5724 /usr/lib/aarch64-linux-gnu/libglib-2.0.so.0.7400.6
gsettings 118906  zen  mem       REG              179,2   462704       5728 /usr/lib/aarch64-linux-gnu/libgobject-2.0.so.0.7400.6
gsettings 118906  zen  mem       REG              179,2  2100616       5723 /usr/lib/aarch64-linux-gnu/libgio-2.0.so.0.7400.6
gsettings 118906  zen  mem       REG              179,2   330728      61747 /usr/lib/aarch64-linux-gnu/libpulse.so.0.24.2
gsettings 118906  zen  mem       REG              179,2    48048      93290 /usr/share/glib-2.0/schemas/gschemas.compiled
gsettings 118906  zen  mem       REG              179,2   526456     279648 /usr/lib/aarch64-linux-gnu/pulseaudio/libpulsecommon-16.1.so
gsettings 118906  zen  mem       REG              179,2    27028       6263 /usr/lib/aarch64-linux-gnu/gconv/gconv-modules.cache
gsettings 118906  zen  mem       REG              179,2   202904       5409 /usr/lib/aarch64-linux-gnu/ld-linux-aarch64.so.1
gsettings 118906  zen  mem       REG               0,39        2         62 /run/user/1000/dconf/user
gsettings 118906  zen    0r      CHR                1,3      0t0          5 /dev/null
gsettings 118906  zen    1w     FIFO               0,12      0t0      88052 pipe
gsettings 118906  zen    2w      CHR                1,3      0t0          5 /dev/null
gsettings 118906  zen    3u  a_inode               0,13        0       1061 [eventfd:25]
gsettings 118906  zen    4u  a_inode               0,13        0       1061 [eventfd:26]
gsettings 118906  zen    5u  a_inode               0,13        0       1061 [eventfd:27]
gsettings 118906  zen    6u     unix 0x00000000f5c246eb      0t0      91111 type=STREAM (CONNECTED)
gsettings 118906  zen    7u  a_inode               0,13        0       1061 [eventfd:28]
```
 
