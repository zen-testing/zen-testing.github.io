---
title: 'crf and bitrate'
date: 2024-04-05 09:28:48
tags: [ffmpeg]
published: true
hideInList: false
feature: 
isTop: false
---
|编码|分辨率|crf|qp|bitrate|
|:---:|:---:|:---:|:---:|:---:|
|libx265|2160p|20||12000k@30Hz<br>18000@60Hz|
|libx265|1440p|21||6000k@30Hz<br>9000@60Hz|
|libx265|1080p|22||3000k@30Hz<br>6000k@60Hz|
|libx265|720p|23||1500k@30Hz<br>2000k@60Hz|
|libx265|480p|24||512k@30Hz|
|SVT AV1|2160p||24|12000k@30Hz<br>18000k@60Hz|
|SVT AV1|1440p||24|6000k@30Hz<br>9000k@60Hz|
|SVT AV1|1080p||24|1800k@30Hz<br>3000k@60Hz|
|SVT AV1|720p||24|1024k@30Hz<br>1800k@60Hz|
|SVT AV1|480p||24|512k@30Hz|
|libvpx-vp9|2160p|15||12000k@30Hz<br>18000k@60Hz|
|libvpx-vp|1440p|24||6000k@30Hz<br>9000k@60Hz|
|libvpx-vp|1080p|31||1800k@30Hz<br>3000k@60Hz|
|libvpx-vp|720p|32||1024k@30Hz<br>1800k@60Hz|
|libvpx-vp|480p|33||512k@30Hz|