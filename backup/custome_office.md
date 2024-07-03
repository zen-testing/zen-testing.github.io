---
title: '定制安装office'
date: 2022-09-26 16:02:02
tags: [office,Windows]
published: true
hideInList: false
feature: 
isTop: false
---
#office 2016
代码如下

configure.xml
```
<Configuration>
	<Add SourcePath="H:\" OfficeClientEdition="64" Branch="Current">
		<Product ID="O365ProPlusRetail">
			<Language ID="zh-CN" />
			<ExcludeApp ID="Access" />
			<ExcludeApp ID="Groove" />
			<ExcludeApp ID="InfoPath" />
			<ExcludeApp ID="Lync" />
			<ExcludeApp ID="Publisher" />
			<ExcludeApp ID="SharePointDesigner" />
			<ExcludeApp ID="OneNote" />
			<ExcludeApp ID="Outlook" />
		</Product>
		<Product ID="VisioProRetail">
			<Language ID="zh-CN" />
		</Product>
		<Product ID="proplusretail">
			<Language ID="zh-cn" />
			<ExcludeApp ID="Access" />
			<ExcludeApp ID="Groove" />
			<ExcludeApp ID="InfoPath" />
			<ExcludeApp ID="Lync" />
			<ExcludeApp ID="Publisher" />
			<ExcludeApp ID="SharePointDesigner" />
			<ExcludeApp ID="OneNote" />
			<ExcludeApp ID="Outlook" />
		</Product>
	</Add>
</Configuration>
```
其中
+ ExcludeApp表示不安装,相反IncludeApp表示安装
+ SourcePath="H:\"表示安装镜像挂载的位置,比如H:\
+ ProPlus2019Volume表示安装你常见的office组件
+ VisioPro2019Volume表示安装VISIO
+ 剩下的靠猜也能猜出来

# office 2019
代码如下

configure.xml
```
<?xml version="1.0"?>
-<Configuration>
	-<Add  SourcePath="H:\" ForceUpgrade="TRUE" AllowCdnFallback="TRUE" Channel="PerpetualVL2019" OfficeClientEdition="64">
		-<Product ID="ProPlus2019Volume">
			<Language ID="zh-cn"/>
			<Language ID="en-us"/>
			<ExcludeApp ID="Groove"/>
			<ExcludeApp ID="OneNote" />
			<ExcludeApp ID="Access" />
			<ExcludeApp ID="Lync" />
			<ExcludeApp ID="PowerPoint" />
			<ExcludeApp ID="Excel" />
			<ExcludeApp ID="OneDrive" />
			<ExcludeApp ID="Outlook" />
			<ExcludeApp ID="Publisher" />
			<ExcludeApp ID="Word" />
		</Product>
		-<Product ID="VisioPro2019Volume">
			<Language ID="zh-cn"/>
			<Language ID="en-us"/>
			<ExcludeApp ID="Groove"/>
		</Product>
		-<Product ID="ProjectPro2019Volume">
			<Language ID="zh-cn"/>
			<Language ID="en-us"/>
			<ExcludeApp ID="Groove"/>
		</Product>
	</Add>
	<Property Value="0" Name="SharedComputerLicensing"/>
	<Property Value="TRUE" Name="PinIconsToTaskbar"/>
	<Property Value="0" Name="SCLCacheOverride"/>
	<Updates Enabled="TRUE"/>
</Configuration>
```
其中
+ ExcludeApp表示不安装,相反IncludeApp表示安装
+ SourcePath="H:\"表示安装镜像挂载的位置,比如H:\
+ ProPlus2019Volume表示安装你常见的office组件
+ VisioPro2019Volume表示安装VISIO
+ ProjectPro2019Volume表示安装Project
+ 剩下的靠猜也能猜出来


<iframe width="560" height="315" src="https://www.youtube.com/embed/kewFfaHMfOc" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

2019同理