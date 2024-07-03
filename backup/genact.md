---
title: 'genact用法'
date: 2022-10-29 10:41:36
tags: [Linux,macOS,跨平台]
published: true
hideInList: false
feature: 
isTop: false
---
摸鱼使我快乐

<!-- more -->
# 用法
```shell
A nonsense activity generator

Usage: genact [OPTIONS]

Options:
  -l, --list-modules
          List available modules
  -m, --modules <MODULES>
          Run only these modules [possible values: composer, cargo, bootlog, download, mkinitcpio,
          rkhunter, bruteforce, julia, cryptomining, docker_build, cc, simcity, botnet,
          kernel_compile, weblog, docker_image_rm, ansible, memdump]
  -s, --speed-factor <SPEED_FACTOR>
          Global speed factor [default: 1]
      --exit-after-time <EXIT_AFTER_TIME>
          Exit after running for this long (format example: 2h10min)
      --exit-after-modules <EXIT_AFTER_MODULES>
          Exit after running this many modules
      --print-completions <shell>
          Generate completion file for a shell [possible values: bash, elvish, fish, powershell,
          zsh]
      --print-manpage
          Generate man page
  -h, --help
          Print help information
  -V, --version
          Print version information
```

# 可选modules

|名称|效果|
|:---:|:---:|
|docker_build|![docker_build](https://s1.ax1x.com/2022/10/29/x4XU1O.png)|
|botnet|![botnet](https://s1.ax1x.com/2022/10/29/x4XJtx.png)|
|weblog|![weblog](https://s1.ax1x.com/2022/10/29/x4X1B9.png)|
|cargo|![cargo](https://s1.ax1x.com/2022/10/29/x4XKcF.png)|
|cc|![cc](https://s1.ax1x.com/2022/10/29/x4Owoq.png)|
|composer|![composer](https://s1.ax1x.com/2022/10/29/x4OJSS.png)|
|docker_image_rm|![docker_image_rm](https://s1.ax1x.com/2022/10/29/x4OeQe.png)|
|cryptomining|![cryptomining](https://s1.ax1x.com/2022/10/29/x4OAJK.png)|
|bootlog|![bootlog](https://s1.ax1x.com/2022/10/29/x4OiIx.png)|
|bruteforce|![bruteforce](https://s1.ax1x.com/2022/10/29/x4OpL9.png)|
|julia|![julia](https://s1.ax1x.com/2022/10/29/x4LyqA.png)|
|mkinitcpio|![mkinitcpio](https://s1.ax1x.com/2022/10/29/x4L02D.png)|
|rkhunter|![rkhunter](https://s1.ax1x.com/2022/10/29/x4LNUx.png)|
|memdump|![memdump](https://s1.ax1x.com/2022/10/29/x4Ll2F.png)|
|kernel_compile|![kernel_compile](https://s1.ax1x.com/2022/10/29/x4LnU0.png)|
|download|![download](https://s1.ax1x.com/2022/10/29/x4qxHI.png)|
|ansible|![ansible](https://s1.ax1x.com/2022/10/29/x4qb9O.png)|
|simcity|![simcity](https://s1.ax1x.com/2022/10/29/x4qhu9.png)|