---
title: 'ffmpeg嵌入字幕'
date: 2022-11-15 21:01:38
tags: [ffmpeg]
published: true
hideInList: false
feature: 
isTop: false
---
# mkv+ass软字幕

```bash
ffmpeg -i input.mkv -i input.ass -c copy -c:s ass output.mkv
```

# 嵌入字幕

用ffmpeg去`嵌入字幕`=`写入字幕`=`合并字幕`=`烧录字幕`

分2类:

## 软字幕=内挂字幕

* 别称:`软字幕`=`soft subs`=`soft subtitles`
* ffmpeg处理逻辑:`stream copy`**流拷贝**模式
* 举例:
    ```bash
    ffmpeg -i input.mkv -i subtitles.ass -codec copy -map 0 -map 1 output.mkv

    ffmpeg -i infile.mp4 -f srt -i infile.srt -c:v copy -c:a copy -c:s mov_text outfile.mp4
    ```

## 硬字幕=内嵌字幕

* 别称:`硬字幕`=`hardsubs`=`hard subs`=`hard subtitles`=`burn in subtitles`
* ffmpeg处理逻辑:用`-vf`加上**字幕文件**
* 前提:ffmpeg支持ass
  * 即:ffmpeg编译参数中包含:`--enable-libass`
    * 举例
        ```bash
        # ffmpeg -version
        ffmpeg version 4.2-tessus  https://evermeet.cx/ffmpeg/  Copyright (c) 2000-2019 the FFmpeg developers
        built with Apple LLVM version 10.0.1 (clang-1001.0.46.4)
        configuration: --cc=/usr/bin/clang --prefix=/opt/ffmpeg ... --enable-libass  ...
        ```
* 举例
  1. 嵌入srt字幕
    ```bash
    ffmpeg -i input.mp4 -vf "subtitles=subtitle.srt" output.mp4
    ```
    * 注
      * (1)-vf后面参数,可以不加双引号:
        ```bash
        ffmpeg -i input.mp4 -vf subtitles=subtitle.srt output.mp4
        ```
        * 不过为了区别后续其他参数,最好像上面一样加上双引号,比较容易和其他参数区别开
      * (2)如果srt字幕内在在视频文件中
        * 比如视频是mkv的容器,内挂有srt字幕,则可以:
            ```bash
            ffmpeg -i input.mkv -vf subtitles=input.mkv output.mp4
            ```
  2. 嵌入ass字幕
    ```bash
    ffmpeg -i input.mp4 -vf "ass=subtitle.ass" output.mp4
    ```
    * 举例
      ```bash
      ffmpeg -i CTT_Folge_01_CH_Subs_DefaultZhcnButNotShow.mp4 -vf ass=subtitle_fontLarggerBackgroundAlpha-4.ass fontPingFangSC20HalfTransparent.mp4
      ```
    * 特殊
      * 另外ffmpeg也支持:`Picture-based subtitles`=基于图片的字幕
        * 命令举例:
            ```bash
            ffmpeg -i input.mkv -filter_complex "[0:v][0:s]overlay[v]" -map "[v]" -map 0:a <output options> output.mkv
            ```
        * 参数说明:
          * 如果是多个stream流,可以把`[0:s]`换成对应的`[0:s:0]`或`[0:s:1]`
    * 注意:
      * (1)当视频有多个音频流,此种方式可能会破坏编码,则用下面方式去修复:
        ```bash
        ffmpeg -i input.ts -filter_complex "[0:v][0:s]overlay[v]" -map "[v]" -map 0:a:0 <output options> output.mkv
        ```
      * (2)Windows环境:注意设置字体的路径
# 高级用法

# 指定字幕文字属性

此处介绍嵌入字幕时,指定字幕文字的各种属性,比如`字体大小`\`字体类型`\`颜色`\`透明度`等

* srt字幕:加force_style参数
    ```bash
    ffmpeg -i video.mp4 -vf "subtitles=subs.srt:force_style='Fontsize=24,PrimaryColour=&H0000ff&'" -c:a copy output.mp4
    ```
* ass字幕:在ass字幕中设置参数
    ```bash
    Fontname, Fontsize, PrimaryColour, SecondaryColour, OutlineColour, BackColour, Bold, Italic, Underline, StrikeOut, ScaleX, ScaleY, Spacing, Angle, BorderStyle, Outline, Shadow
    ```

具体设置成什么值,以及效果如何,可借助于软件Aegisub去设置和预览

### 举例1

```bash
Style: Transparent,PingFang SC,20,&H00FFFFFF,&H000000FF,&HBC5E5E5E,&H8B000000,0,0,0,0,100,100,0,0,3,0,1,2,10,10,10,134
```

实现了字幕效果:

* 字体:PingFang SC
* 字体大小:20
* 字幕的背景半透明效果:后面很多参数组合的效果

如图:

![subtitle_set_attribute_effect](../../assets/img/subtitle_set_attribute_effect.png)

### 举例2:ass设置半透明的背景

```bash
Style: Default,Arial,16,&H00FFFFFF,&H000000FF,&H80000000,&H80000000,-1,0,0,0,100,100,0,0,4,0,0,2,10,10,10,1
```

即可达到要的字幕有个半透明的背景色了.

其中`16`指的是`字体大小`,可以根据需要更改为自己要的值.

# 指定字幕位置

* 最简单但常见的需求:无需操心字幕的具体位置,只需要保证字幕在视频底部
  * 则可以直接嵌入字幕,其中字幕文件是srt或ass均可
    ```bash
    ffmpeg -i input.mp4 -vf subtitles=input.srt output.mp4
    ffmpeg -i input.mp4 -vf ass=subtitle.ass output.mp4
    ```
* 高级需求:指定字幕的具体的位置(不同区域,具体边距等)
  * 前提:必须是ass文件(才能用参数指定字幕位置),srt无法指定字幕位置
    * 如果是srt文件,则需要先去转换成ass文件
        ```bash
        ffmpeg -i input.srt output.ass
        ```

## 嵌入ass字幕到视频中

```bash
ffmpeg -i input.mp4 -vf "ass=input.ass" output.mp4
```

* 其中:
  * ass字幕文件input.ass中,有对应的位置的参数配置
    ```ini
    [V4+ Styles]
    Format: Name, Fontname, Fontsize, PrimaryColour, SecondaryColour, OutlineColour, BackColour, Bold, Italic, Underline, StrikeOut, ScaleX, ScaleY, Spacing, Angle, BorderStyle, Outline, Shadow, Alignment, MarginL, MarginR, MarginV, Encoding

    Style: Default,Arial,16,&Hffffff,&Hffffff,&H0,&H0,0,0,0,0,100,100,0,0,1,1,0,2,10,10,10,0
    ```
    * 其中:
      * `Alignment`:默认为`2` = 底部居中
        * 就满足了我们希望的:字幕在底部居中的位置

### 微调左右间距和底部间距

* 再去微调左右间距和底部间距时
  * 再去改动:
    * `MarginL, MarginR, MarginV`
  * 比如:
    ```ini
    MarginL, MarginR, MarginV
    20,20,10
    ```
  * 即可实现:
    * `MarginL`=`MarginR`:左右间距`20`
    * `MarginV`:底部向上间距`10`

## 嵌入ass字幕举例

* 字幕文件:`input/5d41d82f52247ce73d40475b_cfgPosition.ass`
  * ass文件中相关参数
    ```ini
    Format: Name, Fontname, Fontsize, PrimaryColour, SecondaryColour, OutlineColour, BackColour, Bold, Italic, Underline, StrikeOut, ScaleX, ScaleY, Spacing, Angle, BorderStyle, Outline, Shadow, Alignment, MarginL, MarginR, MarginV, Encoding

    Style: Default,Arial,16,&Hffffff,&Hffffff,&H0,&H0,0,0,0,0,100,100,0,0,1,1,0,2,20,20,10,0
    ```
    * 参数说明
      * 字幕位置主要影响因素
        * 字幕主体所在区域
          * `Alignment`
            * 默认为`2` = 底部居中
            * 其中值: `1-9`
              * 逻辑:和键盘中数字的排布一致
              * 见图:
                * ![subtitle_ass_aligment](../../assets/img/subtitle_ass_aligment.png)
      * 字幕位置次要影响因素
        * 字幕的边距
          * (字幕距离)左右的边距:`MarginL`和`MarginR`:`20`
          * (字幕距离)底部的边距:`10`
* 命令
  ```bash
  ffmpeg -i input/5d41d82f52247ce73d40475b_extendedAll.mp4 -vf "ass=input/5d41d82f52247ce73d40475b_cfgPosition.ass" output/5d41d82f52247ce73d40475b_addedAss_marginV10LR20.mp4
  ```
* 效果
  * ![embed_ass_effect_demo](../../assets/img/embed_ass_effect_demo.png)
