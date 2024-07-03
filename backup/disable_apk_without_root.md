---
title: '免root禁用系统预装应用'
date: 2022-09-26 16:07:15
tags: [adb]
published: true
hideInList: false
feature: 
isTop: false
---
# 插播

健康使用手机/学生模式只能卸载不能禁用
----
有时候华为推送的新版本并不能适合所有人的使用需求,这就会导致某些用户希望停留在较低版本(包括我),但是每次连接wifi都会跳出升级提示,比较不方便.

此命令针对 Android 6.0及以下版本并未做尝试,如有基友尝试成功请在issue中告知

停用输入的命令`adb shell pm disable-user 包名`

有停用就有启用

打开输入的命令`adb shell pm enable 包名`

如果你不知道你要删除的软件包名

`adb shell pm list package` 列出所有应用

`adb shell pm list package -3` 列出第三方应用

`adb shell pm list instrumentation` 列出所有测试包

`adb shell pm dump 包名` 查看包详细信息

# pm命令详解

`list packages`列出设备中已经安装的所有应用包(包括系统应用和用户应用)

`list features`列出所有硬件相关信息

`list libraries `列出当前设备支持的libs

`list users`列出系统上所有的users

`list permissions`列出所有已知的权限

`list ‘pkgname’`列出指定包名的associated文件(APK存档文件)所在

`path ‘pkgname’`查询package的安装位置

`install [-lrtsfd] [PATH]`安装命令
```
`** -l` 锁定应用程序
`** -r`重新安装应用,且保留应用数据
`** -i`指定安装包的包名
`** -s`安装到sd卡
`** -f`安装到系统内置存储中(默认安装位置)
`** -g`授予应用程序清单中列出的所有权限(只有6.0系统可用)
```

`uninstall [options] pkgname`’卸载命令
```
`** -k`卸载应用且保留数据与缓存(如果不加-k则全部删除)
`clear ‘pkgname’` 对指定的package删除所有数据
```
`enable ‘pkgname’` 使package或component可用.(如pm enable "package/class")

`disable ‘pkgname’ `使package或component不可用.(如pm disable "package/class")

`grant ‘pkgname’`授权给应用

`revoke ‘pkgname’`撤销权限

`set-install-location ‘location’`设置默认的安装位置.
```
其中`0`让系统自动选择最佳的安装位置.`1`安装到内部的设备存储空间.`2`安装到外部的设备存储空间
```
`get-install-location` 返回当前的安装位置.返回结果同上

`create-user ‘USER_NAME’` 增加一个新的USER

`remove-user ‘USER_ID’` 删除一个USER
# 已知包名

##### 小米系:
```
com.miui.virtualsim 全球上网
com.android.email 电子邮件
com.miui.backup 备份
com.miui.notes 便签
com.miui.hybrid 快应用
com.miui.hybrid.accessory 快应用服务
com.xiaomi.scanner 扫一扫
com.android.quicksearchbox 搜索
com.miui.voiceassist 小爱同学
com.miui.player 音乐
com.miui.video 视频
com.miui.backup 备份
com.miui.cloudbackup 桌面备份
com.miui.bugreport 用户反馈
com.miui.touchassistant 悬浮球
com.android.printspooler 打印处理服务
com.android.bips 默认打印服务
com.xiaomi.gamecenter 游戏
com.xiaomi.gamecenter.sdk.service 游戏服务
com.miui.userguide 用户手册
com.miui.cloudservice 小米云服务
com.android.midrive 小米云盘
com.miui.yellowpage 生活黄页
com.miui.screenrecorder 屏幕录制
com.android.browser 浏览器
com.miui.contentextension 传送门
com.android.providers.userdictionary 用户字典
com.xiaomi.payment 米币支付
com.xiaomi.drivemode 驾车模式
com.android.stk USIM卡应用
com.xiaomi.simactivate.service 小米SIM卡激活服务
com.sohu.inputmethod.sogou.xiaomi 搜狗输入法小米版
com.miui.personalassistant 智能助理
com.android.calllogbackup 小米云服务中备份通话记录的
com.miui.systemAdSolution msa小米广告推送服务
com.xiaomi.scanner 扫一扫
com.miui.analytics Analytics(未知)
com.dsi.ant.server ANT HAL Service(未知)
com.svox.pico Pico TTS 语音识别系统
com.android.thememanager 个性主题
com.miui.compass 指南针
```

##### 华为系:
```
adb shell pm disable-user com.huawei.android.hwouc  系统更新
adb shell pm disable-user com.huawei.powergenie     省电精灵
adb shell pm disable-user com.huawei.android.hsf  (华为框架服务)
adb shell pm disable-user com.android.mediacenter  (音乐)听音乐我不用它
adb shell pm disable-user com.huawei.health  (运动健康)会要求开启华为移动服务,会要求关注微信公众号
adb shell pm disable-user com.huawei.intelligent  (情景智能)  这个是第三方应用,不是华为自己的
adb shell pm disable-user com.huawei.vdrive  (驾驶模式)无法停用,但在空间管理的预置应用能删的奇怪应用
adb shell pm disable-user com.huawei.phoneservice  (会员服务)停用
adb shell pm disable-user com.huawei.phoneservice  (华为钱包) 用不到,停用
adb shell pm disable-user com.huawei.KoBackup  (备份)删
adb shell pm disable-user com.huawei.hwvplayer.youku  (华为视频优酷版)删
adb shell pm disable-user com.stupeflix.replay  (Quik)删
adb shell pm disable-user com.google.android.marvin.talkback  (TalkBack)删
adb shell pm disable-user com.huawei.android.karaoke  k歌音效
adb shell pm disable-user com.google.android.gms(停用谷歌的代码
adb shell pm disable-user com.android.nfc  (NFC服务)停用
adb shell pm disable-user com.huawei.parentcontrol (学生模式)用不上,但不给停用
adb shell pm disable-user com.baidu.input_huawei  (百度输入法华为版)找到替代的可删
adb shell pm disable-user com.ifeng.news2  (凤凰新闻)删
adb shell pm disable-user com.huawei.gamebox  (华为游戏中心)删
adb shell pm disable-user com.huawei.android.hwouc  (系统更新)删\一连wifi就跳出来烦
adb shell pm disable-user com.huawei.skytone  (天际通数据服务)删\出国才可能有机会用到
adb shell pm disable-user com.huawei.hiskytone  (天际通)删\出国才可能有机会用到
adb shell pm disable-user com.huawei.powergenie  (省电精灵)
adb shell pm disable-user com.android.hwmirror  (镜子
adb shell pm disable-user com.android.email  (电子邮件)删
adb shell pm disable-user com.huawei.decision   决策系统
adb shell pm disable-user com.huawei.phoneservice   会员服务
adb shell pm disable-user com.android.packageinstaller  (打包安装程序)自测不能停
adb shell pm disable-user com.huawei.android.hwpay  (华为钱包安全支付)停用
adb shell pm disable-user com.vmall.client  (华为商城)删
adb shell pm disable-user com.huawei.android.findmyphone   找回手机
adb shell pm disable-user com.huawei.watch.sync   手表同步
adb shell pm disable-user com.huawei.camera  (相机)
adb shell pm disable-user com.huawei.hidisk  (文件管理)不用的时候能停用
adb shell pm disable-user com.huawei.bluetooth  (通过蓝牙导入)
adb shell pm disable-user com.android.providers.media  (媒体存储)
adb shell pm disable-user com.huawei.android.thememanager  (主题)
adb shell pm disable-user com.huawei.android.chr  (HwChrService)
adb shell pm disable-user com.google.android.ext.shared  (Android Shared Library)
adb shell pm disable-user com.android.wallpapercropper  (壁纸裁剪器)
adb shell pm disable-user com.huawei.android.FloatTasks  (悬浮导航)
adb shell pm disable-user com.huawei.motionservice  (手势服务)
org.simalliance.openmobileapi.service  (SmartcardService)
adb shell pm disable-user com.huawei.appmarket  (华为应用市场)连接助手就会强制更新的应用
adb shell pm disable-user com.huawei.secime  (华为安全输入法)
adb shell pm disable-user com.android.documentsui (文件)
adb shell pm disable-user com.android.externalstorage  (外部存储设备)
adb shell pm disable-user com.android.htmlviewer  (HTML查看器)
adb shell pm disable-user com.iflytek.speechsuite  (讯飞语音引擎)停用也能微信语音
adb shell pm disable-user com.android.mms.service
adb shell pm disable-user com.huawei.android.totemweather  (天气)
adb shell pm disable-user com.android.providers.downloads  (下载管理器)
adb shell pm disable-user com.dianping.v1  (大众点评)删
adb shell pm disable-user com.nuance.swype.EMUI  (华为Swype输入法)删
adb shell pm disable-user com.huawei.locationsharing  (位置共享)
adb shell pm disable-user com.huawei.cryptosms.service  (短信加密
adb shell pm disable-user com.realvnc.android.remote  (VNC远程控制)
adb shell pm disable-user com.huawei.screenrecorder  (屏幕录制)
adb shell pm disable-user com.huawei.videoeditor  (视频编辑)
adb shell pm disable-user com.huawei.securitymgr  (隐私空间)
adb shell pm disable-user com.android.browser  (浏览器)
adb shell pm disable-user com.android.soundrecorder  (录音机)
adb shell pm disable-user com.huawei.iconnect
adb shell pm disable-user com.huawei.android.AutoRegSms
adb shell pm disable-user com.android.defcontainer  (软件包访问帮助程序)
adb shell pm disable-user com.android.providers.downloads.ui  (下载内容)
adb shell pm disable-user com.android.pacprocessor
adb shell pm disable-user com.hisi.mapcon
adb shell pm disable-user com.huawei.logupload
adb shell pm disable-user com.android.certinstaller  (证书安装器)
adb shell pm disable-user com.android.carrierconfig
adb shell pm disable-user com.huawei.imonitor
adb shell pm disable-user com.huawei.fans  (花粉俱乐部)删
adb shell pm disable-user com.huawei.hwid  (华为移动服务)停用
adb shell pm disable-user com.huawei.remoteassistant (远程协助)停用
adb shell pm disable-user com.android.contacts  (联系人)
adb shell pm disable-user com.android.mms  (信息)
adb shell pm disable-user com.android.mtp  (MTP服务)
adb shell pm disable-user com.android.stk  (SIM卡应用)
adb shell pm disable-user com.android.backupconfirm
adb shell pm disable-user com.huawei.android.instantshare  (Huawei Share)
adb shell pm disable-user com.huawei.indexsearch.observer
adb shell pm disable-user com.huawei.trustagent  (智能解锁)
adb shell pm disable-user com.huawei.trustspace  (支付保护中心)停用
adb shell pm disable-user com.android.statementservice  (Intent Filter Verification Services)
adb shell pm disable-user com.huawei.indexsearch
adb shell pm disable-user com.huawei.android.internal.app  (Huawei Share)
adb shell pm disable-user com.huawei.hwasm
=adb shell pm disable-user com.huawei.lives
adb shell pm disable-user com.android.calendar  (日历)
adb shell pm disable-user com.huawei.wifiprobqeservice
adb shell pm disable-user com.android.providers.settings
adb shell pm disable-user com.android.sharedstoragebackup
adb shell pm disable-user com.android.printspooler  (打印处理服务)停用
adb shell pm disable-user com.android.frameworkres.overlay
adb shell pm disable-user com.android.dreams.basic  (基本互动屏保)停用
adb shell pm disable-user com.android.incallui  (拨号)
adb shell pm disable-user com.huawei.systemmanager  (手机管家)虽然半残,但停用将影响服务 自测不能停
adb shell pm disable-user com.android.inputdevices  (输入设备)
adb shell pm disable-user com.huawei.yellowpage  (在线黄页)深度集成在通讯录内
adb shell pm disable-user com.android.supl
adb shell pm disable-user com.huawei.hilink.framework
adb shell pm disable-user com.google.android.webview
adb shell pm disable-user com.huawei.HwMultiScreenShot  (滚动截屏)
adb shell pm disable-user com.android.onetimeinitializer
adb shell pm disable-user com.huawei.vassistant  (语音助手)停用
adb shell pm disable-user com.android.server.teleadb shell pm disable-user com  (通话管理)
adb shell pm disable-user com.example.android.notepad  (备忘录)
adb shell pm disable-user com.android.keychain  (密钥链)
adb shell pm disable-user com.android.keyguard  (华为杂志锁屏)删
adb shell pm disable-user com.android.gallery3d  (图库)
adb shell pm disable-user com.huawei.watch.sync  (手表应用同步)没表的删
adb shell pm disable-user com.huawei.hwstartupguide  (安装向导)
adb shell pm disable-user com.huawei.fido.uafclient
adb shell pm disable-user com.svox.pico  (Pico TTS)删
adb shell pm disable-user com.huawei.hwireader  (华为阅读)删
adb shell pm disable-user com.android.proxyhandler
adb shell pm disable-user com.huawei.android.mirrorshare  (无线分享)
adb shell pm disable-user com.huawei.phonediagnose
adb shell pm disable-user com.android.inputmethod.latin  (AOSP输入法)删\一打字就现身通知栏
adb shell pm disable-user com.huawei.contactscamcard  (名片全能王)删\深度集成在通讯录
adb shell pm disable-user com.google.android.printservice.readb shell pm disable-user commendation
adb shell pm disable-user com.android.managedprovisioning  (工作资料设置)
adb shell pm disable-user com.huawei.hiboard  (负一屏)  这个是第三方应用,不是华为自己的
adb shell pm disable-user com.huawei.himovie  (华为视频)删
adb shell pm disable-user com.huawei.adb shell pm disable-user compass  (指南针)停用
adb shell pm disable-user com.android.dreams.phototable  (图片屏保程序)停用
adb shell pm disable-user com.huawei.android.dsdscardmanager  (双卡管理)
adb shell pm disable-user com.huawei.android.hwaps
adb shell pm disable-user com.huawei.android.wfdft  (WLAN直连)
adb shell pm disable-user com.android.wallpaper.livepicker  (动态壁纸)停用
adb shell pm disable-user com.amap.android.ams  (高德位置服务)
adb shell pm disable-user com.huawei.mmitest
adb shell pm disable-user com.android.apps.tag  (标记)停用
adb shell pm disable-user com.qeexo.smartshot  (智能截屏)
adb shell pm disable-user com.android.settings
adb shell pm disable-user com.android.calculator2  (计算器)
adb shell pm disable-user com.autonavi.minimap  (高德地图)删
adb shell pm disable-user com.huawei.android.projectmenu  (工程菜单)
adb shell pm disable-user com.android.cts.ctsshim
adb shell pm disable-user com.huawei.android.pushagent  (推送服务)停用
adb shell pm disable-user com.huawei.geofence  (地理围栏)
adb shell pm disable-user com.android.vpndialogs  (VPN设置)
adb shell pm disable-user com.huawei.ihealth  (华为健康)删
adb shell pm disable-user com.huawei.android.location.activityrecognition  (行为识别)
adb shell pm disable-user com.sina.weibo  (新浪微博)删
adb shell pm disable-user com.android.phone  (拨号)
adb shell pm disable-user com.android.shell
adb shell pm disable-user com.android.providers.blockednumber  (存储已屏蔽的号码)
adb shell pm disable-user com.android.providers.userdictionary  (用户词典)
adb shell pm disable-user com.android.emergency  (个人紧急信息)
adb shell pm disable-user com.huawei.scanner  (扫一扫)停用
adb shell pm disable-user com.android.location.fused  (融合定位)
adb shell pm disable-user com.android.deskclock  (时钟)
adb shell pm disable-user com.android.systemui  (系统界面)
adb shell pm disable-user com.android.exchange  (Exchange服务)
adb shell pm disable-user com.android.bluetoothmidiservice
adb shell pm disable-user com.huawei.hwdetectrepair  (智能检测)
adb shell pm disable-user com.huawei.bd  (HwUE)
adb shell pm disable-user com.huawei.ca  (CAServices)
adb shell pm disable-user com.huawei.ims
adb shell pm disable-user com.huawei.lbs  (HwLBSService)
adb shell pm disable-user com.android.bluetooth  (蓝牙)
adb shell pm disable-user com.android.providers.contacts  (联系人存储)
adb shell pm disable-user com.android.captiveportallogin
adb shell pm disable-user com.huawei.android.airsharing (多屏互动)停用
adb shell pm disable-user com.huawei.himovie (华为视频)
adb shell pm disable-user com.huawei.browser (华为浏览器)
adb shell pm disable-user com.huawei.health (运动健康)
adb shell pm disable-user com.android.mediacenter (音乐播放器)
adb shell pm disable-user com.huawei.android.thememanager (华为主题)
adb shell pm disable-user com.huawei.hwireader (华为阅读)
adb shell pm disable-user com.huawei.hifolder (精品推荐)
adb shell pm disable-user com.huawei.android.findmyphone (查找手机)
adb shell pm disable-user com.android.stk (sim卡应用)
adb shell pm disable-user com.huawei.search (下拉搜索)
```
