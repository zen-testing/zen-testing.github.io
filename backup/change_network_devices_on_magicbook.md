---
title: '更换魔法书上扶不起来的网卡'
date: 2019-11-18 15:47:03
tags: [华为]
published: true
hideInList: false
feature: 
isTop: false
---

# 前言

魔法书Pro科技尝鲜版自带的是瑞昱8822CE蓝牙Wi-Fi二合一芯片,信号干扰严重,只要蓝牙处在广播状态网络丢包率徘徊80%, 蓝牙数据传输时丢包率直逼100%

所以~~我有一个大胆的想法~~

+ [ ] 瑞昱某个型号的问题,手动更换一款瑞昱更高等级的无线模块
+ [x] 如果这是瑞昱无线技术不过关的问题,手动更换一款Intel高大全的无线模块

我假装自己是一个消费者,询问了客服Intel版魔法书的网卡型号

华为商城客服的回答简单明了三个字`不知道`

至于为什么不去找华为官方客户服务中心,他们的各种[睿智操作](https://zhangyiming748.github.io/2019/11/04/Honor/)已经抵消了我对专业人员的信任

----
# 计划

按照维修思想,先从预期收益最大的方式入手

购买[IntelAX200NGW网卡](https://detail.tmall.com/item.htm?spm=a230r.1.14.19.743868c9qB44vR&id=602306932858&ns=1&abbucket=15&skuId=4221965037035)

购买[防静电设备](https://detail.tmall.com/item.htm?id=537354759539&spm=a1z09.2.0.0.6a4a2e8d83hKPI&_u=i2cc9fmub8f4)

购买[螺丝刀套装](https://item.jd.com/100005054710.html)

等待MagicBook Pro 过保

----

# 睿智客服

昨天我以消费者的身份致电华为客服,询问了一下intel版魔法书的网卡型号

答复居然是`由于涉及供应商的涉密信息,我们不能提供详细的硬件信息`

我自己开盖看就不涉密,你告诉我电脑里边装的啥就是泄密?

----

# 插播

没耐心,不等了

东西已经在路上了

到货之后找个黄道吉日就直接换了

----

# 转机

刚才接到了华为客服中心的电话

官方确认是Intel-AC9560

突然心里一沉

我买的是AX200

看下对比

||Intel® Wi-Fi 6 AX200 Module|Intel® Wireless-AC 9560|
|:---:|:---:|:---:|
|状态|Launched|Launched|
|发行日期 |Q2'19|Q4'17|
|重量(克)|2.8|2.8|
|操作温度范围|0°C to 80°C|0°C to 80°C|
|支持的操作系统|Windows 10, 64-bit*, Linux*, Chrome OS*|Windows 10, 64-bit*, Linux*, Chrome OS*|
|天线|2x2|2x2|
|TX/RX 流|2x2|2x2|
|频带|2.4Ghz, 5Ghz (160Mhz)|2.4Ghz, 5Ghz (160Mhz)|
|最高速度|2.4Gbps|1.73Gbps|
|Wi-Fi CERTIFIED*|WiFi 6 (802.11ax)|802.11ac|
|兼容性|FIPS, FISMA|FIPS, FISMA|
|集成蓝牙|是|是|
|主板板型|M.2 2230, M.2 1216|M.2 2230, M.2 1216|
|封装大小|22mm x 30mm x 2.4mm, 12mm x 16mm x 1.65mm|22mm x 30mm x 2.4mm, 12mm x 16mm x 1.57mm|
|系统接口类型|<font color="#FF0000">Wi-Fi(PCIe), BT(USB)</font>|<font color="#FF0000">M.2: CNVio</font>|

其中系统接口类型的差异让我看的夜不能寐

常识告诉我,PCIE通道的硬盘通常很贵,接口也很稀有,我买的电脑预装了廉价的小螃蟹芯片会是PCIE通道的吗?一切只有到货之后才知道,现在只能听天由命了

![包裹](https://s1.ax1x.com/2022/09/05/vT5LHH.png)<center>拜双十一所赐,龟速快递</center>

----

# 数据

更正,论坛上有人说之前的网卡是8822CE,但是在官网查询并没有这个型号,最接近的一款是[8821CE](https://www.realtek.com/zh-tw/products/communications-network-ics/item/rtl8821ce)

已知Intel9560AC由于需要Intel芯片组协同工作,所以理论上不支持锐龙版魔法书

另外还有

+ 8822BE
>802.11AC/ABGN PCIE WLAN WITH BLUETOOTH 4.2 SINGLE-CHIP CONTROLLER The Realtek RTL8822BE-CG is a highly integrated single-chip that supports 2-stream 802.11ac solutions with Multi-user MIMO (Multiple-Input, Multiple-Output) and Wireless LAN (WLAN) PCI Express network interface controller and integrated Bluetooth 2.1/3.0/4.2 USB interface controller. It combines a WLAN MAC, a 2T2R capable WLAN baseband, and RF in a single chip. The RTL8822BE-CG provides a complete solution for a high-performance integrated wireless and Bluetooth device.FeaturesGeneralTFBGA 6.5x6.5mm package802.11 ac/abgn802.11ac 2x2, Wave-2 compatible with MU-MIMOBluetooth 4.2 (Software only)Host interfacePCI Express 1.1 for WLAN controllerUSB2.0 for Bluetooth controllerApplicationsThe product is applicable for PC/NB, Set-top box applications
>>(机翻)带蓝牙4.2单片机的802.11AC/ABGN PCIE WLAN Realtek RTL8822BE-CG是一个高度集成的单片机,支持2流802.11ac解决方案,支持多用户MIMO(多输入\多输出)和无线局域网(WLAN) PCI Express网络接口控制器,以及集成的蓝牙2.1/3.0/4.2 USB接口控制器.它将一个WLAN MAC\一个支持2T2R的WLAN基带和射频集成在一个芯片中.RTL8822BE-CG为高性能集成无线和蓝牙设备提供了完整的解决方案.WLAN controllerUSB2.0蓝牙控制器应用本产品适用于PC/NB\机顶盒应用

+ RTL8822BEH-VR
>802.11AC/ABGN PCIE WLAN WITH BLUETOOTH 4.1 SINGLE-CHIP CONTROLLER The Realtek RTL8822BEH-VR-CG is a highly integrated single-chip that supports 2-stream 802.11ac solutions with Multi-user MIMO (Multiple-Input, Multiple-Output) and Wireless LAN (WLAN) PCI Express network interface controller with integrated Bluetooth 2.1/3.0/4.1 USB interface controller. It combines a WLAN MAC, a 2T2R capable WLAN baseband, and RF in a single chip. The RTL8822BEH-VR-CG provides a complete solution for a high-performance integrated wireless and Bluetooth device. TFBGA 6.5x6.5mm package 802.11 ac/abgn 802.11ac 2x2, Wave-2 compatible with MU-MIMO Bluetooth 4.1 Host interface PCI Express 1.1 for WLAN controller HS-UART for Bluetooth controller Applications The product is applicable for Set-top box and AP router application
>>(机翻)802.11AC/ABGN PCIE WLAN带蓝牙4.1单片机控制器 Realtek rtl8822behr - vr - cg是一个高度集成的单片机,支持2流802.11ac解决方案,支持多用户MIMO(多输入\多输出)和无线局域网(WLAN) PCI Express网络接口控制器,支持集成蓝牙2.1/3.0/4.1 USB接口控制器.它将一个WLAN MAC\一个支持2T2R的WLAN基带和射频集成在一个芯片中.rtl8822behr - vr - cg为高性能集成无线和蓝牙设备提供了完整的解决方案.TFBGA 6.5x6.5mm封装802.11ac /abgn 802.11ac 2x2, Wave-2兼容MU-MIMO蓝牙4.1主机接口

+ RTL8822BS
>802.11AC/ABGN SDIO WLAN WITH BLUETOOTH 4.1 SINGLE-CHIP CONTROLLER The Realtek RTL8822BS-CG is a highly integrated single-chip that supports 2-stream 802.11ac solutions with Multi-user MIMO (Multiple-Input, Multiple-Output) and Wireless LAN (WLAN) SDIO interface controller with integrated Bluetooth 2.1/3.0/4.1 HS-UART interface controller. It combines a WLAN MAC, a 2T2R capable WLAN baseband, and RF in a single chip. The RTL8822BS-CG provides a complete solution for a high-performance integrated wireless and Bluetooth device. TFBGA 6.5x6.5mm package 802.11 ac/abgn 802.11ac 2x2, Wave-2 compatible with MU-MIMO Bluetooth 4.1 system Host interface SDIO 1.1/2.0/3.0 for WLAN controller HS-UART for Bluetooth controller Applications The product is applicable for Set-top box, virtual reality, and LTE router application
>>(机翻)Realtek RTL8822BS-CG是一个高度集成的单片机,支持2流802.11AC解决方案,支持多用户MIMO(多输入\多输出)和无线局域网(WLAN) SDIO接口控制器,支持集成蓝牙2.1/3.0/4.1 HS-UART接口控制器.它将一个WLAN MAC\一个支持2T2R的WLAN基带和射频集成在一个芯片中.RTL8822BS-CG为高性能集成无线和蓝牙设备提供了完整的解决方案.TFBGA 6.5x6.5mm封装802.11ac /abgn 802.11ac 2x2, Wave-2兼容MU-MIMO蓝牙4.1系统主机接口SDIO 1.1/2.0/3.0 for WLAN controller HS-UART for Bluetooth controller Applications本产品适用于机顶盒\虚拟现实\LTE路由器应用

+ RTL8822BU
>802.11AC/ABGN USB WLAN WITH BLUETOOTH 4.1 SINGLE-CHIP CONTROLLER The Realtek RTL8822BU-CG is a highly integrated single-chip that supports 2-stream 802.11ac solutions with Multi-user MIMO (Multiple-Input, Multiple-Output) and Wireless LAN (WLAN) with integrated Bluetooth 2.1/3.0/4.1 USB-multi interface controller. It combines a WLAN MAC, a 2T2R capable WLAN baseband, and RF in a single chip. The RTL8822BU-CG provides a complete solution for a high-performance integrated wireless and Bluetooth device. TFBGA 6.5x6.5mm package 802.11 ac/abgn 802.11ac 2x2, Wave-2 compatible with MU-MIMO Bluetooth 4.1 system Host interface USB2.0 for WLAN and BT controller Applications The product is applicable for TV and Set-top box application
>>(机翻)Realtek RTL8822BU-CG是一个高度集成的单片机,支持2流802.11AC解决方案,多用户MIMO(多输入\多输出)和无线局域网(WLAN),集成了蓝牙2.1/3.0/4.1 USB-multi interface CONTROLLER.它将一个WLAN MAC\一个支持2T2R的WLAN基带和射频集成在一个芯片中.RTL8822BU-CG为高性能集成无线和蓝牙设备提供了完整的解决方案.TFBGA 6.5x6.5mm封装802.11ac /abgn 802.11ac 2x2, Wave-2兼容MU-MIMO蓝牙4.1系统主机接口USB2.0用于WLAN和BT控制器应用本产品适用于电视和机顶盒应用

<font size="18">看来具体型号有待确认,不如现在来有奖竞猜一下,评论区留下你的答案,猜对可获得群成员稀有ASMR,正确答案即将揭晓</font>

----
# 到货
![到货](https://raw.githubusercontent.com/zhangyiming748/zhangyiming748.github.io/master/img/Honor/item.webp)<center>如果换不成功,最坏的打算,USB无线网卡</center>

----
# 开工

在我打开电脑的那一刻我惊呆了,电源排线的防拆条完好如新,而我经历过两次拆机级别的"专业工程师"--华为官方客户服务中心的维修

![没有断电的专业维修](https://s1.ax1x.com/2022/09/05/vTIG5R.png)<center>专业的带电维修师傅</center>

旧网卡确实是 RTL8822CE 但是官网上却查不到这个型号实属蹊跷

D壳卸下螺丝后需要使用翘片撬开,最容易下手的部分在通风部分

![效果图](https://s1.ax1x.com/2019/11/27/Q986BQ.png)

拆机中的难点主要是在新网卡上接天线,手残搞不定,比如我用了半个小时

高清无码大图由于网络环境问题就不上传了

重要节点的图片做成了电子相册,自行观看


<iframe width="560" height="315" src="https://www.youtube.com/embed/sL-bWYtq4ss" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<b>注意</b>换网卡危险性高于加装硬盘,千万注意手部放电,尤其是干燥的冬天,硬盘位不包含主板部件网卡位不同

# 效果图

![最终效果](https://s1.ax1x.com/2022/09/05/vTIS8P.png)<center>英特尔WiFi6Bluetooth5.0</center>


# 见解

我理解华为想要扶持中国企业,但有的真的是扶不起来啊,扶瑞昱扶声卡\以太网卡\读卡器和分线器都是可以的,无线网卡还是算了吧

----

# 旧网卡的临终关怀

换下来的网卡不要扔,裹上鸡蛋液,粘上面包糠,下锅炸至金黄酥脆控油捞出,老人小孩都爱吃,隔壁小孩都馋哭了

----
# 善后

由于更换了网卡,而之前个人判断一碰传实质上是根据网卡MAC地址临时建立虚拟局域网进行数据交换,由此预见更换网卡后NFC标签中并没有记录新网卡的MAC地址,所以更换网卡后一碰传和多屏协同快速建立连接的功能失效,预先在淘宝上购买了[NFC贴片](https://item.taobao.com/item.htm?spm=a1z0d.7625083.1998302264.5.5c5f4e69mSrRIE&id=607304808177),按照各方教程,制作了一张

>接下来开始NFC标签的制作,把那个APK用手机安装了,然后查看下电脑蓝牙MAC地址,打开CMD
ipconfig /all
我的蓝牙地址是这个98-54-1B-2E-68-77
>>https://cli.im/text
>>>SN=5EKPM18320000397|MAC=680715939B02|MODELID=00000505
>>
把这个MAC改下,其他不动
SN=5EKPM18320000397|MAC=98541B2E6877|MODELID=00000505
生成二维码,然后手机用那个APP扫一下
按提示激活NFC标签,好了

其中,二维码的内容
>SN=5EKPM18320000397|MAC=680715939B02|MODELID=00000505

SN填机器的SN号
可以用这个命令查询`wmic bios get serialnumber`

已知部分MODELID如下

<center>MateBook系列</center>

|型号|值|
|:---:|:--:|
|MateBook|0500|
|Matebook|0501|
|Matebook X|0502|
|Matebook D|0503|
|Matebook E|0504|
|Matebook D(2018)|0505|
|Matebook X Pro|0506|
|Matebook 13|0507|
|Matebook 14|0508|
|Matebook 15|0509|
|Matebook E|0510|
|Matebook|0511|
|Matebook|0512|

<center>MagicBook系列</center>

|型号|值|
|:---:|:--:|
|MagicBook|0800|
|MagicBook 2019|0801|
|MagicBook|0802|
|MagicBook|0803|
|MagicBook Pro|0804|
|MagicBook|0805|
|MagicBook|0806|
|MagicBook|0807|
|MagicBook Pro|0808|
|MagicBook|0809|
|MagicBook|0810|

MAC填芯片的bluetooth地址而不是网卡地址,虽然这俩东西在一张PCB上

MODELID00000505是MateBook D的型号 ~~但是我无论如何也查不到MagicBook Pro的MODELID 希望能人异士找到后能告诉我一声~~
MagicBook Pro的MODELID是0804,人还是要靠自己
读取出来的NFC芯片信息如下,感谢`我是传奇snake`提供图片

|IC Info|Ndef|Extra|Full Scan|
|:--:|:--:|:--:|:--:|
|![IC Info](https://raw.githubusercontent.com/zhangyiming748/zhangyiming748.github.io/master/img/Honor/icInfo.webp)|![Ndef](https://raw.githubusercontent.com/zhangyiming748/zhangyiming748.github.io/master/img/Honor/ndef.webp)|![Extra](https://raw.githubusercontent.com/zhangyiming748/zhangyiming748.github.io/master/img/Honor/extra.webp)|![Full Scan](https://raw.githubusercontent.com/zhangyiming748/zhangyiming748.github.io/master/img/Honor/fullScan.webp)|

购买六张NFC标签制作一张还剩五张,剩下的就扔掉吗?

剩下的贴片不要扔,~~裹上鸡蛋液,粘上面包糠,下锅炸至金黄酥脆控油捞出,老人小孩都爱吃,隔壁小孩都馋哭了~~还可以复制门禁卡,电梯卡等(一种不能说的卡)

那就是后话了

# 鸣谢

一起奋战的小伙伴们(排名不分先后)

[我是传奇snake](https://club.huawei.com/space-uid-7719051.html)

[sing238](https://club.huawei.com/space-uid-16975468.html)

[妖夭柒](https://club.huawei.com/space-uid-145794107.html)

[huafen854571664](https://club.huawei.com/space-uid-137254691.html)

[雾海沧狐](https://club.huawei.com/space-uid-7274763.html)

[君羊主](https://club.huawei.com/space-uid-23722374.html)

[芥末绿](https://club.huawei.com/space-uid-98447634.html)

# 后记

最近总有人说自己更换完网卡之后会失去保修,事实上,拆电脑后盖已经是一种像开冰箱门一样的常规操作了,售后会因为你私自打开过冰箱门不给冰箱保修吗?电脑同理
换完这个网卡后,自己买的各种nfc卡贴都觉得不美观,利用一代魔法书免费加装nfc卡贴的政策(免物料费),和服务日政策(免手工费)白嫖了一张正版nfc贴纸,去的时候服务人员告诉我直接复制就行,我明确告知他我换了网卡,蓝牙地址改变他就给我重做了一张,等待的时候客服看到我的Mate30Pro手机主动提出免费贴膜,临走还送了我一个陶瓷水杯;后来又走售后流程拿到了一套硬盘线,虽然最后硬盘是我自己装的,总之开电脑后盖和保不保修没关系,再说也没人和电脑滴血认亲
