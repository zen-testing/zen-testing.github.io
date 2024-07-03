---
title: 'error while loading shared libraries错误解决办法'
date: 2022-09-26 17:19:51
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---

默认情况下,编译器只会使用`/lib`和`/usr/lib`这两个目录下的库文件,通常通过源码包进行安装时,如果不指定`--prefix`,会将库安装在`/usr/local/lib`目录下;当运行程序需要链接动态库时,提示找不到相关的`.so`库,会报错.也就是说,`/usr/local/lib`目录不在系统默认的库搜索目录中,需要将目录加进去.

1. 首先打开`/etc/ld.so.conf`文件
2. 加入动态库文件所在的目录执行`sudo nano /etc/ld.so.conf`,在`include ld.so.conf.d/*.conf`下方增加`/usr/local/lib`
3. 保存后,在命令行终端执行`/sbin/ldconfig -v`其作用是将文件`/etc/ld.so.conf`列出的路径下的库文件缓存到`/etc/ld.so.cache`以供使用,因此当安装完一些库文件,或者修改`/etc/ld.so.conf`增加了库的新搜索路径,需要运行一下`ldconfig`使所有的库文件都被缓存到文件`/etc/ld.so.cache`中,如果没做,可能会找不到刚安装的库.

经过以上三个步骤`error while loading shared libraries`的问题通常情况下就可以解决了.

如果运行应用程序时,还是提示以上错误,那就得确认一下是不是当前用户在库目录下是不是没有可读的权限.像我遇到的问题就是,从别的机子拷贝了一些`.so`动态库,然后用`root`权限放到了`/usr/local/lib`中(普通用户没有对该目录的写权限),然后切换用户运行程序时,始终提示找不到`.so`库,一直以为是我配置有问题,结果是因为权限原因,那些我用`root`权限增加到`/usr/local/lib`中的`.so`文件对于普通用户而言,是没有访问权限的,所以以普通用户运行程序,当需要链接`.so`库时,在`/usr/local/lib`中是查找不到的.

其实,对于由普通用户自己编译生成的`.so`库文件,比较好的做法是将这些`.so`库文件的路径用`export`指令加入到`~/.bash_profile`中的`LD_LIBRARY_PATH`变量中,`LD_LIBRARY_PATH`是程序运行需要链接`.so`库时会去查找的一个目录,`~/.bash_profile`是登陆或打开`shell`时会读取的文件,这样,每次用户登录时,都会把这些`.so`库文件的路径写入`LD_LIBRARY_PATH`,这样就可以正常地使用这些`.so`库文件了.
