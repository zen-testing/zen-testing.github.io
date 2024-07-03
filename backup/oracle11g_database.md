---
title: 'Oracle11g安装手册'
date: 2023-05-24 20:41:57
tags: [oracle]
published: true
hideInList: false
feature: 
isTop: false
---
# Oracle 安装

## 0x01 检查Linux环境

1. 机器配置

Centos虚拟机
VirtualBox
仅启用root账户
[linux.x64_11gR2_database_1of2.zip](https://pan.baidu.com/s/1JfEphdhGgOMNAgVjZRmhaA?pwd=7izi)
[linux.x64_11gR2_database_2of2.zip](https://pan.baidu.com/s/1BoTvS6jSBVhyli0YQwkV0Q?pwd=tlmy)
[jdk-8u361-linux-x64.tar.gz](https://pan.baidu.com/s/12a-JlpUbh8rEoghJMADMKA?pwd=58gf)

2. 检查系统位数

```bash
uname -m
```

3. 检查内存

```bash
grep MemTotal /proc/meminfo
free
```

4. 查看交换空间大小

```bash
grep SwapTotal /proc/meminfo
# swap:如果1-2G物理内存,最好设置swap为1.5-2倍的物理内存大小
```

重新制作交换文件

```bash
dd if=/dev/zero of=/swap bs=1M count=10000
mkswap /swap
swapon /swap //挂载这个swap
swapon -s //查看swap分区
```

5. 查看tmp空间大小(不能小于1G)

```bash
df -h /tmp
```

6. 查看内核版本

```bash
# 最好是oracle推荐的linux版本,如果不是建议修改/etc/redhat-release的内容来伪装一下
cat /proc/version
vim /etc/redhat-release
修改为:redhat-7
```

7. 查看内核版本

```bash
uname –r
```

## 0x02 安装和配置JDK

1. 下载

```bash
wget https://download.oracle.com/otn/java/jdk/8u361-b09/0ae14417abb444ebb02b9815e2103550/jdk-8u361-linux-x64.tar.gz?AuthParam=1684482758_561d509ab30013462644b448056694d
```

2. 解压

```bash
tar xvf jdk-8u361-linux-x64.tar.gz -C /opt
```

3. 配置环境变量

```bash
echo -e 'JAVA_HOME=/opt/jdk1.8.0_361\nPATH=$JAVA_HOME/bin:$PATH\nCLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar\nexport PATH' >> /etc/environment
```

## 0x03 检查Oracle安装必须包

```shell
#!/bin/bash
rpm -q binutils-2.20.51.0.2-5.11.el6
rpm -q compat-libcap1-1.10-1
rpm -q compat-libstdc++-33-3.2.3-69.el6
rpm -q compat-libstdc++-33-3.2.3-69.el6.i686
rpm -q gcc-4.4.4-13.el6
rpm -q gcc-c++-4.4.4-13.el6
rpm -q glibc-2.12-1.7.el6
rpm -q glibc-2.12-1.7.el6
rpm -q glibc-devel-2.12-1.7.el6
rpm -q glibc-devel-2.12-1.7.el6.i686
rpm -q ksh
rpm -q libgcc-4.4.4-13.el6
rpm -q libgcc-4.4.4-13.el6
rpm -q libstdc++-4.4.4-13.el6
rpm -q libstdc++-4.4.4-13.el6.i686
rpm -q libstdc++-devel-4.4.4-13.el6
rpm -q libstdc++-devel-4.4.4-13.el6.i686
rpm -q libaio-0.3.107-10.el6
rpm -q libaio-0.3.107-10.el6.i686
rpm -q libaio-devel-0.3.107-10.el6
rpm -q libaio-devel-0.3.107-10.el6.i686
rpm -q make-3.81-19.el6
rpm -q sysstat-9.0.4-11.el6
```

安装命令

```bash
yum install epel-release
yum install \
libgcc.i686 \
libaio \
libstdc++ \
libgcc* \
libXtst* \
make* \
compat-libstdc++-33 \
elfutils-libelf \
glibc-devel.i686 \
libaio* \
glibc \
glibc-devel \
unixODBC \
unixODBC-devel \
ksh \
libstdc++.i686 \
ksh* \
gcc* \
binutils \
libaio-devel.i686 \
unixODBC-devel \
binutils* \
glibc* \
libstdc++* \
libXi* \
unixODBC* \
expat* \
pdksh*  \
gcc  \
compat-libcap*  \
elfutils-libelf-devel  \
libgcc \
sysstat \
gcc-c++ \
sysstat* \
glibc-common \
libstdc++-devel \
glibc.i686 \
glibc-headers \
libaio.i686 \
compat-libstdc++* \
libaio-devel \
compat-libstdc++-33.i686

yum -y install binutils compat-libcap1 compat-libstdc+±33 compat-libstdc+±33i686 compat-libstdc+±33.devel compat-libstdc+±33 compat-libstdc+±33*.devel gcc gcc-c++ glibc glibc*.i686 glibc-devel glibc-devel*.i686 ksh libaio libaio*.i686 libaio-devel libaio-devel*.devel libgcc libgcc*.i686 libstdc++ libstdc++.i686 libstdc+±devel libstdc+±devel.devel libXi libXi*.i686 libXtst libXtst*.i686 make sysstat unixODBC unixODBC*.i686 unixODBC-devel unixODBC-devel*.i686
```

## 0x04 添加用户和组

1. 添加用户组

```bash
groupadd -g 502 oinstall
groupadd -g 503 dba
groupadd -g 504 oper
groupadd -g 505 asmadmin
```

2. 添加用户

```bash
useradd -u 502 -g oinstall -G oinstall,dba,asmadmin,oper -s /bin/bash -m oracle
```

3. 设置密码

```bash
passwd oracle
```

## 0x05 修改系统配置参数

1. 修改`/etc/sysctl.conf`文件

```bash
echo -e 'fs.aio-max-nr = 1048576\nfs.file-max = 6815744\nkernel.shmall = 2097152\nkernel.shmmax = 536870912\nkernel.shmmni = 4096\nkernel.sem = 250 32000 100 128\nnet.ipv4.ip_local_port_range = 9000 65500\nnet.core.rmem_default = 262144\nnet.core.rmem_max = 4194304\nnet.core.wmem_default = 262144\nnet.core.wmem_max = 1048576' >> /etc/sysctl.conf
# 使命令生效
sysctl -p
# 或者
/sbin/sysctl –p
```

2. 修改`/etc/security/limits.conf`文件
```bash
echo -e "oracle soft nproc 2047\noracle hard nproc 16384\noracle soft nofile 1024\noracle hard nofile 65536\noracle soft stack  10240" >> /etc/security/limits.conf
```

3. 修改`/etc/pam.d/login`文件

```bash
echo -e "session  required   /lib64/security/pam_limits.so\nsession  required   pam_limits.so" >> /etc/pam.d/login
```

## 0x06 创建oracle11gR2安装目录

```bash
mkdir -p /oradata/soft/oracle11g
# 解压安装文件到oradata
unzip linux.x64_11gR2_database_1of2.zip
unzip linux.x64_11gR2_database_2of2.zip
```

## 0x07 修改oracle用户环境变量

```bash
su - oracle
echo -e 'export ORACLE_BASE=/oradata/soft/oracle11g\nexport ORACLE_HOME=$ORACLE_BASE/product/11.2.0.3/dbhome_1\nexport ORACLE_SID=prod\nexport NLS_LANG=.AL32UTF8\nexport PATH=${PATH}:${ORACLE_HOME}/bin:$ORACLE_HOME/lib64' >> /home/oracle/.bash_profile
source /home/oracle/.bash_profile
```

## 0x08 修改安装配置文件

切换oracle用户登录,编辑配置文件

```bash
# 拷贝安装文件到工作目录
cp /oradata/database/response/db_install.rsp /oradata
# 编辑配置文件
vim db_install.rsp
```

```vim
# 修改如下内容
oracle.install.option=INSTALL_DB_AND_CONFIG
ORACLE_HOSTNAME=192.168.78.142
UNIX_GROUP_NAME=oinstall
INVENTORY_LOCATION=/oradata/soft/oraInventory
SELECTED_LANGUAGES=en,zh_CN
ORACLE_HOME=/oradata/soft/oracle11g/product/11.2.0.3/dbhome_1
ORACLE_BASE=/oradata/soft/oracle11g
oracle.install.db.InstallEdition=EE
oracle.install.db.DBA_GROUP=dba
oracle.install.db.OPER_GROUP=oper
oracle.install.db.config.starterdb.type=GENERAL_PURPOSE
oracle.install.db.config.starterdb.globalDBName=prod
oracle.install.db.config.starterdb.SID=prod
oracle.install.db.config.starterdb.characterSet=AL32UTF8
oracle.install.db.config.starterdb.memoryOption=true
oracle.install.db.config.starterdb.memoryLimit=1024262 oracle.install.db.config.starterdb.password.ALL=oracle
oracle.install.db.config.starterdb.storageType=FILE_SYSTEM_STORAGE
oracle.install.db.config.starterdb.fileSystemStorage.dataLocation=/oradata/soft/oracle11g/data
oracle.install.db.config.starterdb.fileSystemStorage.recoveryLocation=/oradata/soft/oracle11g/fast_recovery_area
DECLINE_SECURITY_UPDATES=true
```

## 0x09 安装数据库

先将oracle文件夹下所有文件权限都属于oracle用户

```bash
# root用户下
chown -R oracle:oinstall /oradata/
```

切换Oracle账户运行

```bash
./runInstaller -silent -ignoreSysPrereqs -responseFile /oradata/db_install.rsp -ignorePrereq
```

等待安装完成提示,打开新终端执行屏幕上显示的两条命令

## 0x0a 验证安装

```bash
# oracle用户
sqlplus / as sysdba
```

![安装成功](https://s1.ax1x.com/2023/05/24/p97QfYt.png)