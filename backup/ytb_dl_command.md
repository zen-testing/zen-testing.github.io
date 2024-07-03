---
title: 'youtube-dl常用命令'
date: 2022-09-26 21:26:14
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---
# 指定视频尺寸下载

```shell
/usr/local/bin/youtube-dl --proxy 127.0.0.1:1086 -f 'bestvideo[height=1080]+bestaudio/best[height<=480]' <url>
```

# 下载最高分辨率(不适用于YouTube视频)

```shell
sudo /usr/local/bin/youtube-dl --proxy 127.0.0.1:1080 -f bestvideo+bestaudio <url>
```

# 同时下载全部可用字幕

```shell
/usr/local/bin/youtube-dl --proxy 127.0.0.1:1080 --write-sub --all-subs -i -f bestvideo+bestaudio <url>
```

# 直接下载

```shell
/usr/local/bin/youtube-dl <url>
```

# 不检查证书

```shell
youtube-dl --no-check-certificate --proxy 127.0.0.1:8889 -f bestvideo+bestaudio <url>
```

# 查看可用格式

```shell
$ youtube-dl --proxy 127.0.0.1:8889 -F https://www.youtube.com/watch?v=s_NpfL0iXWE
format code  extension  resolution note
249          webm       audio only tiny   54k , opus @ 50k (48000Hz), 13.41MiB
250          webm       audio only tiny   67k , opus @ 70k (48000Hz), 16.62MiB
251          webm       audio only tiny  120k , opus @160k (48000Hz), 30.22MiB
140          m4a        audio only tiny  132k , m4a_dash container, mp4a.40.2@128k (44100Hz), 38.33MiB
394          mp4        256x144    144p   95k , av01.0.00M.08, 25fps, video only, 21.74MiB
278          webm       256x144    144p  146k , webm container, vp9, 25fps, video only, 30.09MiB
160          mp4        256x144    144p  157k , avc1.4d400c, 25fps, video only, 23.08MiB
395          mp4        426x240    240p  209k , av01.0.00M.08, 25fps, video only, 43.44MiB
242          webm       426x240    240p  224k , vp9, 25fps, video only, 47.62MiB
133          mp4        426x240    240p  296k , avc1.4d4015, 25fps, video only, 34.48MiB
396          mp4        640x360    360p  374k , av01.0.01M.08, 25fps, video only, 78.61MiB
243          webm       640x360    360p  410k , vp9, 25fps, video only, 85.73MiB
134          mp4        640x360    360p  626k , avc1.4d401e, 25fps, video only, 63.03MiB
397          mp4        854x480    480p  648k , av01.0.04M.08, 25fps, video only, 138.33MiB
244          webm       854x480    480p  762k , vp9, 25fps, video only, 134.39MiB
135          mp4        854x480    480p  995k , avc1.4d401e, 25fps, video only, 97.44MiB
398          mp4        1280x720   720p 1315k , av01.0.05M.08, 25fps, video only, 285.05MiB
247          webm       1280x720   720p 1544k , vp9, 25fps, video only, 235.05MiB
136          mp4        1280x720   720p 1599k , avc1.4d401f, 25fps, video only, 162.52MiB
399          mp4        1920x1080  1080p 2444k , av01.0.08M.08, 25fps, video only, 527.64MiB
248          webm       1920x1080  1080p 2705k , vp9, 25fps, video only, 650.58MiB
137          mp4        1920x1080  1080p 4339k , avc1.640028, 25fps, video only, 583.48MiB
18           mp4        640x360    360p  568k , avc1.42001E, 25fps, mp4a.40.2@ 96k (44100Hz), 168.39MiB
22           mp4        1280x720   720p  678k , avc1.64001F, 25fps, mp4a.40.2@192k (44100Hz) (best)
$ youtube-dl --proxy 127.0.0.1:8889 -f 248+140 https://www.youtube.com/watch?v=s_NpfL0iXWE
```