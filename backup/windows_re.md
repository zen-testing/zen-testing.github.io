---
title: 'Win10的重置原理和可行性分析'
date: 2022-09-26 20:41:22
tags: [Windows]
published: true
hideInList: false
feature: 
isTop: false
---
总有人保留着一种想法:win10电脑随便设置,实在不行就重置

----

这个观点是从win8.* 中继承过来的,但是这里要说的是,他们实质上的原理不一样

![](https://img-blog.csdnimg.cn/20181230110942665.png)

![](https://img-blog.csdnimg.cn/20181230111003247.png)

![](https://img-blog.csdnimg.cn/20181230111022479.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTE2ODIyODM=,size_16,color_FFFFFF,t_70)

以上是win8.* 相关设置
接下来是win10同样的设置

![](https://img-blog.csdnimg.cn/20181230111112277.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTE2ODIyODM=,size_16,color_FFFFFF,t_70)

![](https://img-blog.csdnimg.cn/20181230111043487.png)
如果你还看不出区别的话,接下来是文字结论

****

Win8.* 的重置的原理是保留一份超高压缩的原始系统映像,无论你对现在的系统做了什么(除非你删除相关映像,流氓软件非常喜欢这么做),只要你还能执行resetsystem命令,系统都会恢复为全新状态

到了win10(准确说是version1507之后)的时候,因为已经找不到映像位置,而且官方文档已经表明win10重置的原理实质是收集现有可用的文件资源,重新组成个可用的系统.只要能正常开机和联网,剩下的部分交给dism工具就行

打个比方:  某家失火了,烧得只剩墙砖,重置就相当于收集了足够剩下来的砖来盖房子,只要保证不倒就行,等有了足够的钱(网络),缺什么可以去买,把这个房子恢复如初.重置的最后一步就是检验系统关键组件(砖)的完整性.

**所以结论就是** :过度破坏的win10系统不可以通过重置功能来恢复,不知道是不是巧合,我遇到过不能重置的电脑上都不约而同地装上了流氓软件并且用户手动清理了垃圾
