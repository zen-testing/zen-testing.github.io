---
title: 'Ventoy配置文件'
date: 2022-09-26 20:17:14
tags: [ventoy]
published: true
hideInList: false
feature: 
isTop: false
---
如果你使用的是Linux系统,完全可以通过VentoyPlugson傻瓜化图形界面操作获得和码农一样的个性化定制
![VentoyPlugson.sh](https://www.ventoy.net/static/img/ventoyplugson_cn.png)

# 其中最关键的配置文件写法示例

```json
{
    "control":[
        { "VTOY_WIN11_BYPASS_CHECK": "1" },
        { "VTOY_HELP_TXT_LANGUAGE": "zh_CN" },// 主界面使用的语言
        { "VTOY_DEFAULT_SEARCH_ROOT": "/iso" }// 查找镜像启示的目录,避免全盘搜索不必要的文件,加快速度
    ],
    "theme":{
        "file": "/ventoy/theme/bigsur/theme.txt",// 使用的主题文件
        "gfxmode": "1920x1080"// 第一个界面使用的分辨率,如果你有设置壁纸的话,最好这里设置一下
    },
    "menu_alias":[
        {
            "image": "/iso/en_windows_thin_pc_x86_697681.iso",// 镜像所在位置
            "alias": "Windows Thin PC"// 镜像在启动选择菜单中显示的名称
        },
        {
            "image": "/iso/cn_windows_10_enterprise_ltsc_2019_x64_dvd_d17070a8.iso",
            "alias": "Windows 10 LTSC"
        },
        {
            "image": "/iso/gparted-live-1.4.0-1-amd64.iso",
            "alias": "Gparted"
        },
        {
            "image": "/iso/uniontechos-desktop-21.3-home-amd64.iso",
            "alias": "UOS家庭版"
        },
        {
            "image": "/iso/Hikari_PE_X64_V8.2_SC.iso",
            "alias": "Hikari PE"
        },
        {
            "image": "/iso/ubuntu-22.04-desktop-amd64.iso",
            "alias": "Ubuntu 22.04"
        },
        {
            "image": "/iso/openEuler-22.03-LTS-x86_64-dvd.iso",
            "alias": "openEuler 22.03"
        },
        {
            "image": "/iso/uos-livetools-desktop-20220425_amd.iso",
            "alias": "UOS-Tools"
        },
        {
            "image": "/iso/19044.1288.211006-0501.21h2_release_svc_refresh_CLIENT_LTSC_EVAL_x64FRE_zh-cn.iso",
            "alias": "Windows LTSC 2021"
        }
    ]
}
```

# 比较大的数据分区目录结构

```shell
.
├── Edgeless
│         ├── Nes_Inport.7z
│         ├── Resource
│         │         ├── ATI_25.10.1.39_泉水叮咚.7z
│         │         ├── HDTunePro_5.7.5.0_0.0.7z
│         │         ├── LLFTool低格工具_4.40.0.0_Cno.7z
│         │         ├── WindowsGame_1.0.0.0_可爱の萌新酱.7z
│         │         ├── 鲁大师_6.1022.3255.120_Horatio+Shaw.7z
│         │         ├── 芯片精灵_1.0.0.0_Brzh.7z
│         │         ├── 火绒安全_5.0.69.5_Cno(bot).7z
│         │         ├── 搜狗拼音_8.4.0.1039_Cno.7z
│         │         ├── 无线网卡驱动_1.0.0.0_光卡.7z
│         │         ├── 网卡增强驱动_1.1.0_Fir.7z
│         │         ├── 植物大战僵尸beta版_6.25.4.1_Cno.7z
│         │         ├── 一键启用所有插件.cmd
│         │         ├── 一键禁用所有插件.cmd
│         │         └── 硬盘整数分区计算器_1.2_System3206.7z
│         ├── version.txt
│         └── wp.jpg  
├── Edgeless_4-1-0.wim
├── System Volume Information
│         ├── EDP
│         │         └── Recovery
│         ├── IndexerVolumeGuid
│         └── WPSettings.dat
├── fonts
│         ├── ttf
│         │         ├── JetBrainsMono-Bold.ttf
│         │         ├── JetBrainsMono-BoldItalic.ttf
│         │         ├── JetBrainsMono-ExtraBold.ttf
│         │         ├── JetBrainsMono-ExtraBoldItalic.ttf
│         │         ├── JetBrainsMono-ExtraLight.ttf
│         │         ├── JetBrainsMono-ExtraLightItalic.ttf
│         │         ├── JetBrainsMono-Italic.ttf
│         │         ├── JetBrainsMono-Light.ttf
│         │         ├── JetBrainsMono-LightItalic.ttf
│         │         ├── JetBrainsMono-Medium.ttf
│         │         ├── JetBrainsMono-MediumItalic.ttf
│         │         ├── JetBrainsMono-Regular.ttf
│         │         ├── JetBrainsMono-SemiBold.ttf
│         │         ├── JetBrainsMono-SemiBoldItalic.ttf
│         │         ├── JetBrainsMono-Thin.ttf
│         │         ├── JetBrainsMono-ThinItalic.ttf
│         │         ├── JetBrainsMonoNL-Bold.ttf
│         │         ├── JetBrainsMonoNL-BoldItalic.ttf
│         │         ├── JetBrainsMonoNL-ExtraBold.ttf
│         │         ├── JetBrainsMonoNL-ExtraBoldItalic.ttf
│         │         ├── JetBrainsMonoNL-ExtraLight.ttf
│         │         ├── JetBrainsMonoNL-ExtraLightItalic.ttf
│         │         ├── JetBrainsMonoNL-Italic.ttf
│         │         ├── JetBrainsMonoNL-Light.ttf
│         │         ├── JetBrainsMonoNL-LightItalic.ttf
│         │         ├── JetBrainsMonoNL-Medium.ttf
│         │         ├── JetBrainsMonoNL-MediumItalic.ttf
│         │         ├── JetBrainsMonoNL-Regular.ttf
│         │         ├── JetBrainsMonoNL-SemiBold.ttf
│         │         ├── JetBrainsMonoNL-SemiBoldItalic.ttf
│         │         ├── JetBrainsMonoNL-Thin.ttf
│         │         └── JetBrainsMonoNL-ThinItalic.ttf
│         ├── variable
│         │         ├── JetBrainsMono-Italic[wght].ttf
│         │         └── JetBrainsMono[wght].ttf
│         └── webfonts
│             ├── JetBrainsMono-Bold.woff2
│             ├── JetBrainsMono-BoldItalic.woff2
│             ├── JetBrainsMono-ExtraBold.woff2
│             ├── JetBrainsMono-ExtraBoldItalic.woff2
│             ├── JetBrainsMono-ExtraLight.woff2
│             ├── JetBrainsMono-ExtraLightItalic.woff2
│             ├── JetBrainsMono-Italic.woff2
│             ├── JetBrainsMono-Light.woff2
│             ├── JetBrainsMono-LightItalic.woff2
│             ├── JetBrainsMono-Medium.woff2
│             ├── JetBrainsMono-MediumItalic.woff2
│             ├── JetBrainsMono-Regular.woff2
│             ├── JetBrainsMono-SemiBold.woff2
│             ├── JetBrainsMono-SemiBoldItalic.woff2
│             ├── JetBrainsMono-Thin.woff2
│             └── JetBrainsMono-ThinItalic.woff2
├── iso
│         ├── 19044.1288.211006-0501.21h2_release_svc_refresh_CLIENT_LTSC_EVAL_x64FRE_zh-cn.iso
│         ├── Hikari_PE_X64_V8.2_SC.iso
│         ├── Kylin-Server-10-SP2-x86-Release-Build09-20210524.iso
│         ├── cn_windows_10_enterprise_ltsc_2019_x64_dvd_d17070a8.iso
│         ├── en_windows_thin_pc_x86_697681.iso
│         ├── gparted-live-1.4.0-1-amd64.iso
│         ├── gparted-live-1.4.0-5-amd64.iso
│         ├── openEuler-22.03-LTS-x86_64-dvd.iso
│         ├── openKylin-0.7.5-x86_64.iso
│         ├── ubuntu-22.04-desktop-amd64.iso
│         ├── ubuntu-22.04.1-live-server-amd64.iso
│         ├── uniontechos-desktop-21.3-home-amd64.iso
│         ├── uos-livetools-desktop-20220425_amd.iso
│         └── zh-cn_windows_11_business_editions_version_21h2_updated_july_2022_x64_dvd_b53f45ba.iso
├── tools
│         ├── Debian
│         │         └── icalingua_2.6.4_amd64.deb
│         ├── Universal
│         │         ├── Dism++10.1.1002.1.zip
│         │         ├── Gamesys_V1.1-Gamersky.rar
│         │         ├── Intel-Driver-and-Support-Assistant-Installer.exe
│         │         ├── LTSB-Add-MicrosoftStore-master.zip
│         │         ├── MicrosoftCorporationII.WindowsSubsystemForAndroid_2205.40000.14.0_neutral___8wekyb3d8bbwe.Msixbundle
│         │         ├── MicrosoftCorporationII.WindowsSubsystemForLinux_0.61.8.0_neutral___8wekyb3d8bbwe.Msixbundle
│         │         ├── OneDriveSetup.exe
│         │         ├── Tools.zip
│         │         ├── VMware-tools-windows-11.0.0-14549434.iso
│         │         ├── VMware-workstation-16.2.3-19376536.exe
│         │         ├── Win7经典游戏和组件.zip
│         │         ├── Windows Media Center For Win11.zip
│         │         ├── Windows7Games_for_Windows_11_10_8.zip
│         │         ├── balena-etcher-electron_1.7.9_amd64.deb
│         │         ├── rufus-3.19p.exe
│         │         ├── ventoy-1.0.78-linux.tar.gz
│         │         └── windowsdesktop-runtime-6.0.4-win-x64.exe
│         ├── Windows 10
│         │         ├── 7z2107-x64.exe
│         │         ├── WindowsDefenderControl.zip
│         │         └── 数字权利激活工具.zip
│         ├── Windows thin PC
│         │         ├── WindowsThinPC功能包.zip
│         │         ├── lp.cab
│         │         └── 证书和语言包.zip
│         └── openEuler
│             └── readme.openEuler
├── ventoy
│         ├── theme
│         │         └── bigsur
│         │             ├── DejaVuSans-48.pf2
│         │             ├── DejaVuSans-Regular-14.pf2
│         │             ├── background.png
│         │             ├── boot_menu_c.png
│         │             ├── boot_menu_e.png
│         │             ├── boot_menu_n.png
│         │             ├── boot_menu_ne.png
│         │             ├── boot_menu_nw.png
│         │             ├── boot_menu_s.png
│         │             ├── boot_menu_se.png
│         │             ├── boot_menu_sw.png
│         │             ├── boot_menu_w.png
│         │             ├── icons
│         │             │         ├── Manjaro.i686.png
│         │             │         ├── Manjaro.x86_64.png
│         │             │         ├── antergos.png
│         │             │         ├── arch.png
│         │             │         ├── archlinux.png
│         │             │         ├── arcolinux.png
│         │             │         ├── bsd.png
│         │             │         ├── cancel.png
│         │             │         ├── chakra.png
│         │             │         ├── crunchbang.png
│         │             │         ├── debian.png
│         │             │         ├── deepin.png
│         │             │         ├── devuan.png
│         │             │         ├── driver.png
│         │             │         ├── edit.png
│         │             │         ├── edubuntu.png
│         │             │         ├── efi.png
│         │             │         ├── elementary.png
│         │             │         ├── endeavouros.png
│         │             │         ├── fedora.png
│         │             │         ├── find.efi.png
│         │             │         ├── find.none.png
│         │             │         ├── frugalware.png
│         │             │         ├── gentoo.png
│         │             │         ├── gnu-linux.png
│         │             │         ├── help.png
│         │             │         ├── iso.png
│         │             │         ├── kali.png
│         │             │         ├── kaos.png
│         │             │         ├── kbd.png
│         │             │         ├── korora.png
│         │             │         ├── kubuntu.png
│         │             │         ├── lang.png
│         │             │         ├── lfs.png
│         │             │         ├── linux.png
│         │             │         ├── linuxmint.png
│         │             │         ├── lubuntu.png
│         │             │         ├── macosx.png
│         │             │         ├── mageia.png
│         │             │         ├── manjaro.png
│         │             │         ├── memtest.png
│         │             │         ├── opensuse.png
│         │             │         ├── pop-os.png
│         │             │         ├── recovery.png
│         │             │         ├── restart.png
│         │             │         ├── sabayon.png
│         │             │         ├── shutdown.png
│         │             │         ├── siduction.png
│         │             │         ├── solus.png
│         │             │         ├── steamos.png
│         │             │         ├── type.png
│         │             │         ├── tz.png
│         │             │         ├── ubuntu.png
│         │             │         ├── unknown.png
│         │             │         ├── unset.png
│         │             │         ├── void.png
│         │             │         ├── windows.png
│         │             │         ├── xubuntu.png
│         │             │         └── zorin-os.png
│         │             ├── item_c.png
│         │             ├── item_e.png
│         │             ├── item_n.png
│         │             ├── item_ne.png
│         │             ├── item_nw.png
│         │             ├── item_s.png
│         │             ├── item_se.png
│         │             ├── item_sw.png
│         │             ├── item_w.png
│         │             ├── password_field.png
│         │             ├── select_c.png
│         │             ├── select_e.png
│         │             ├── select_n.png
│         │             ├── select_ne.png
│         │             ├── select_nw.png
│         │             ├── select_s.png
│         │             ├── select_se.png
│         │             ├── select_sw.png
│         │             ├── select_w.png
│         │             ├── slider_c.png
│         │             ├── slider_n.png
│         │             ├── slider_s.png
│         │             ├── terminal_c.png
│         │             ├── terminal_e.png
│         │             ├── terminal_n.png
│         │             ├── terminal_ne.png
│         │             ├── terminal_nw.png
│         │             ├── terminal_s.png
│         │             ├── terminal_se.png
│         │             ├── terminal_sw.png
│         │             ├── terminal_w.png
│         │             ├── terminus-12.pf2
│         │             ├── terminus-14.pf2
│         │             ├── terminus-16.pf2
│         │             └── theme.txt
│         ├── ventoy.json
│         ├── ventoy_backup.json
│         └── ventoy_wimboot.img
├── wallpaper
│         ├── (2).jpg
│         └── (9).jpg
└── wim
    └── install.wim

22 directories, 221 files
```

# 比较小的启动分区目录结构

```shell
.
├── EFI
│         └── BOOT
│             ├── BOOTAA64.EFI
│             ├── BOOTIA32.EFI
│             ├── BOOTMIPS.EFI
│             └── BOOTX64.EFI
├── grub
│         ├── arm64-efi
│         │         ├── adler32.mod
│         │         ├── affs.mod
│         │         ├── afs.mod
│         │         ├── archelp.mod
│         │         ├── bfs.mod
│         │         ├── blscfg.mod
│         │         ├── bswap_test.mod
│         │         ├── btrfs.mod
│         │         ├── cbfs.mod
│         │         ├── cmdline_cat_test.mod
│         │         ├── cmp.mod
│         │         ├── cmp_test.mod
│         │         ├── command.lst
│         │         ├── cpio.mod
│         │         ├── cpio_be.mod
│         │         ├── crc64.mod
│         │         ├── crypto.lst
│         │         ├── cryptodisk.mod
│         │         ├── ctz_test.mod
│         │         ├── date.mod
│         │         ├── datehook.mod
│         │         ├── disk.mod
│         │         ├── div.mod
│         │         ├── div_test.mod
│         │         ├── dm_nv.mod
│         │         ├── efinet.mod
│         │         ├── elf.mod
│         │         ├── eval.mod
│         │         ├── exfctest.mod
│         │         ├── f2fs.mod
│         │         ├── fdt.lst
│         │         ├── fdt.mod
│         │         ├── fs.lst
│         │         ├── functional_test.mod
│         │         ├── fwload.mod
│         │         ├── gcry_arcfour.mod
│         │         ├── gcry_blowfish.mod
│         │         ├── gcry_camellia.mod
│         │         ├── gcry_cast5.mod
│         │         ├── gcry_crc.mod
│         │         ├── gcry_des.mod
│         │         ├── gcry_dsa.mod
│         │         ├── gcry_idea.mod
│         │         ├── gcry_md4.mod
│         │         ├── gcry_rfc2268.mod
│         │         ├── gcry_rijndael.mod
│         │         ├── gcry_rmd160.mod
│         │         ├── gcry_rsa.mod
│         │         ├── gcry_seed.mod
│         │         ├── gcry_serpent.mod
│         │         ├── gcry_sha1.mod
│         │         ├── gcry_sha256.mod
│         │         ├── gcry_tiger.mod
│         │         ├── gcry_twofish.mod
│         │         ├── gcry_whirlpool.mod
│         │         ├── geli.mod
│         │         ├── gfxterm_menu.mod
│         │         ├── gptsync.mod
│         │         ├── hello.mod
│         │         ├── help.mod
│         │         ├── hexdump.mod
│         │         ├── hfs.mod
│         │         ├── hfspluscomp.mod
│         │         ├── jfs.mod
│         │         ├── keystatus.mod
│         │         ├── ldm.mod
│         │         ├── loadenv.mod
│         │         ├── lsacpi.mod
│         │         ├── lsefi.mod
│         │         ├── lsefimmap.mod
│         │         ├── lsefisystab.mod
│         │         ├── lsmmap.mod
│         │         ├── lssal.mod
│         │         ├── luks.mod
│         │         ├── lvm.mod
│         │         ├── macbless.mod
│         │         ├── macho.mod
│         │         ├── mdraid09.mod
│         │         ├── mdraid09_be.mod
│         │         ├── mdraid1x.mod
│         │         ├── memdisk.mod
│         │         ├── memrw.mod
│         │         ├── minix.mod
│         │         ├── minix2.mod
│         │         ├── minix2_be.mod
│         │         ├── minix3.mod
│         │         ├── minix3_be.mod
│         │         ├── minix_be.mod
│         │         ├── moddep.lst
│         │         ├── mouse.mod
│         │         ├── mpi.mod
│         │         ├── msdospart.mod
│         │         ├── mul_test.mod
│         │         ├── nilfs2.mod
│         │         ├── normal.mod
│         │         ├── ntfscomp.mod
│         │         ├── odc.mod
│         │         ├── offsetio.mod
│         │         ├── part_acorn.mod
│         │         ├── part_amiga.mod
│         │         ├── part_bsd.mod
│         │         ├── part_dfly.mod
│         │         ├── part_dvh.mod
│         │         ├── part_plan.mod
│         │         ├── part_sun.mod
│         │         ├── part_sunpc.mod
│         │         ├── partmap.lst
│         │         ├── parttool.lst
│         │         ├── parttool.mod
│         │         ├── password.mod
│         │         ├── pbkdf2_test.mod
│         │         ├── pgp.mod
│         │         ├── probe.mod
│         │         ├── procfs.mod
│         │         ├── progress.mod
│         │         ├── raid5rec.mod
│         │         ├── raid6rec.mod
│         │         ├── reiserfs.mod
│         │         ├── romfs.mod
│         │         ├── scsi.mod
│         │         ├── search_fs_file.mod
│         │         ├── search_fs_uuid.mod
│         │         ├── search_label.mod
│         │         ├── setjmp.mod
│         │         ├── setjmp_test.mod
│         │         ├── sfs.mod
│         │         ├── shift_test.mod
│         │         ├── signature_test.mod
│         │         ├── sleep_test.mod
│         │         ├── smbios.mod
│         │         ├── strtoull_test.mod
│         │         ├── syslinuxcfg.mod
│         │         ├── terminal.lst
│         │         ├── test_blockarg.mod
│         │         ├── testload.mod
│         │         ├── testspeed.mod
│         │         ├── tga.mod
│         │         ├── time.mod
│         │         ├── tr.mod
│         │         ├── ufs1.mod
│         │         ├── ufs1_be.mod
│         │         ├── ufs2.mod
│         │         ├── verifiers.mod
│         │         ├── video.lst
│         │         ├── videoinfo.mod
│         │         ├── videotest.mod
│         │         ├── videotest_checksum.mod
│         │         ├── xen_boot.mod
│         │         ├── xnu_uuid.mod
│         │         ├── xnu_uuid_test.mod
│         │         ├── zfs.mod
│         │         ├── zfscrypt.mod
│         │         ├── zfsinfo.mod
│         │         └── zstd.mod
│         ├── checksum.cfg
│         ├── debug.cfg
│         ├── fonts
│         │         ├── ascii.pf2
│         │         └── unicode.pf2
│         ├── grub.cfg
│         ├── help.tar.gz
│         ├── hwinfo.cfg
│         ├── i386-efi
│         │         ├── adler32.mod
│         │         ├── affs.mod
│         │         ├── afs.mod
│         │         ├── ahci.mod
│         │         ├── aout.mod
│         │         ├── appleldr.mod
│         │         ├── archelp.mod
│         │         ├── ata.mod
│         │         ├── backtrace.mod
│         │         ├── bfs.mod
│         │         ├── blscfg.mod
│         │         ├── bsd.mod
│         │         ├── bswap_test.mod
│         │         ├── btrfs.mod
│         │         ├── cbfs.mod
│         │         ├── cbls.mod
│         │         ├── cbmemc.mod
│         │         ├── cbtable.mod
│         │         ├── cbtime.mod
│         │         ├── cmdline_cat_test.mod
│         │         ├── cmp.mod
│         │         ├── cmp_test.mod
│         │         ├── command.lst
│         │         ├── cpio.mod
│         │         ├── cpio_be.mod
│         │         ├── cpuid.mod
│         │         ├── crc64.mod
│         │         ├── crypto.lst
│         │         ├── cryptodisk.mod
│         │         ├── cs5536.mod
│         │         ├── ctz_test.mod
│         │         ├── date.mod
│         │         ├── datehook.mod
│         │         ├── disk.mod
│         │         ├── div.mod
│         │         ├── div_test.mod
│         │         ├── dm_nv.mod
│         │         ├── efinet.mod
│         │         ├── ehci.mod
│         │         ├── elf.mod
│         │         ├── eval.mod
│         │         ├── exfctest.mod
│         │         ├── f2fs.mod
│         │         ├── fdt.lst
│         │         ├── fixvideo.mod
│         │         ├── fs.lst
│         │         ├── functional_test.mod
│         │         ├── gcry_arcfour.mod
│         │         ├── gcry_blowfish.mod
│         │         ├── gcry_camellia.mod
│         │         ├── gcry_cast5.mod
│         │         ├── gcry_crc.mod
│         │         ├── gcry_des.mod
│         │         ├── gcry_dsa.mod
│         │         ├── gcry_idea.mod
│         │         ├── gcry_md4.mod
│         │         ├── gcry_rfc2268.mod
│         │         ├── gcry_rijndael.mod
│         │         ├── gcry_rmd160.mod
│         │         ├── gcry_rsa.mod
│         │         ├── gcry_seed.mod
│         │         ├── gcry_serpent.mod
│         │         ├── gcry_sha1.mod
│         │         ├── gcry_sha256.mod
│         │         ├── gcry_tiger.mod
│         │         ├── gcry_twofish.mod
│         │         ├── gcry_whirlpool.mod
│         │         ├── gdb.mod
│         │         ├── geli.mod
│         │         ├── gptsync.mod
│         │         ├── hdparm.mod
│         │         ├── hello.mod
│         │         ├── help.mod
│         │         ├── hexdump.mod
│         │         ├── hfs.mod
│         │         ├── hfspluscomp.mod
│         │         ├── iorw.mod
│         │         ├── jfs.mod
│         │         ├── keylayouts.mod
│         │         ├── keystatus.mod
│         │         ├── ldm.mod
│         │         ├── legacy_password_test.mod
│         │         ├── legacycfg.mod
│         │         ├── linux16.mod
│         │         ├── loadbios.mod
│         │         ├── loadenv.mod
│         │         ├── lsacpi.mod
│         │         ├── lsefi.mod
│         │         ├── lsefimmap.mod
│         │         ├── lsefisystab.mod
│         │         ├── lsmmap.mod
│         │         ├── lspci.mod
│         │         ├── lssal.mod
│         │         ├── luks.mod
│         │         ├── lvm.mod
│         │         ├── macbless.mod
│         │         ├── macho.mod
│         │         ├── mdraid09.mod
│         │         ├── mdraid09_be.mod
│         │         ├── mdraid1x.mod
│         │         ├── memdisk.mod
│         │         ├── memrw.mod
│         │         ├── minix.mod
│         │         ├── minix2.mod
│         │         ├── minix2_be.mod
│         │         ├── minix3.mod
│         │         ├── minix3_be.mod
│         │         ├── minix_be.mod
│         │         ├── moddep.lst
│         │         ├── morse.mod
│         │         ├── mpi.mod
│         │         ├── msdospart.mod
│         │         ├── mul_test.mod
│         │         ├── multiboot.mod
│         │         ├── multiboot2.mod
│         │         ├── nativedisk.mod
│         │         ├── nilfs2.mod
│         │         ├── normal.mod
│         │         ├── ntfscomp.mod
│         │         ├── odc.mod
│         │         ├── offsetio.mod
│         │         ├── ohci.mod
│         │         ├── part_acorn.mod
│         │         ├── part_amiga.mod
│         │         ├── part_bsd.mod
│         │         ├── part_dfly.mod
│         │         ├── part_dvh.mod
│         │         ├── part_plan.mod
│         │         ├── part_sun.mod
│         │         ├── part_sunpc.mod
│         │         ├── partmap.lst
│         │         ├── parttool.lst
│         │         ├── parttool.mod
│         │         ├── password.mod
│         │         ├── pata.mod
│         │         ├── pbkdf2_test.mod
│         │         ├── pcidump.mod
│         │         ├── pgp.mod
│         │         ├── play.mod
│         │         ├── probe.mod
│         │         ├── procfs.mod
│         │         ├── progress.mod
│         │         ├── raid5rec.mod
│         │         ├── raid6rec.mod
│         │         ├── random.mod
│         │         ├── rdmsr.mod
│         │         ├── reiserfs.mod
│         │         ├── romfs.mod
│         │         ├── scsi.mod
│         │         ├── search_fs_file.mod
│         │         ├── search_fs_uuid.mod
│         │         ├── search_label.mod
│         │         ├── setjmp.mod
│         │         ├── setjmp_test.mod
│         │         ├── setpci.mod
│         │         ├── sfs.mod
│         │         ├── shift_test.mod
│         │         ├── signature_test.mod
│         │         ├── sleep_test.mod
│         │         ├── smbios.mod
│         │         ├── spkmodem.mod
│         │         ├── strtoull_test.mod
│         │         ├── syslinuxcfg.mod
│         │         ├── terminal.lst
│         │         ├── test_blockarg.mod
│         │         ├── testload.mod
│         │         ├── testspeed.mod
│         │         ├── tga.mod
│         │         ├── time.mod
│         │         ├── tr.mod
│         │         ├── ufs1.mod
│         │         ├── ufs1_be.mod
│         │         ├── ufs2.mod
│         │         ├── uhci.mod
│         │         ├── usb.mod
│         │         ├── usbms.mod
│         │         ├── usbserial_common.mod
│         │         ├── usbserial_ftdi.mod
│         │         ├── usbserial_pl2303.mod
│         │         ├── usbserial_usbdebug.mod
│         │         ├── usbtest.mod
│         │         ├── verifiers.mod
│         │         ├── video.lst
│         │         ├── videoinfo.mod
│         │         ├── videotest.mod
│         │         ├── videotest_checksum.mod
│         │         ├── wrmsr.mod
│         │         ├── xnu.mod
│         │         ├── xnu_uuid.mod
│         │         ├── xnu_uuid_test.mod
│         │         ├── zfs.mod
│         │         ├── zfscrypt.mod
│         │         ├── zfsinfo.mod
│         │         └── zstd.mod
│         ├── i386-pc
│         │         ├── acpi.mod
│         │         ├── adler32.mod
│         │         ├── affs.mod
│         │         ├── afs.mod
│         │         ├── ahci.mod
│         │         ├── aout.mod
│         │         ├── archelp.mod
│         │         ├── ata.mod
│         │         ├── backtrace.mod
│         │         ├── bfs.mod
│         │         ├── bitmap.mod
│         │         ├── bitmap_scale.mod
│         │         ├── blscfg.mod
│         │         ├── bsd.mod
│         │         ├── bswap_test.mod
│         │         ├── btrfs.mod
│         │         ├── bufio.mod
│         │         ├── cat.mod
│         │         ├── cbfs.mod
│         │         ├── cbls.mod
│         │         ├── cbmemc.mod
│         │         ├── cbtable.mod
│         │         ├── cbtime.mod
│         │         ├── cmdline_cat_test.mod
│         │         ├── cmosdump.mod
│         │         ├── cmostest.mod
│         │         ├── cmp.mod
│         │         ├── cmp_test.mod
│         │         ├── command.lst
│         │         ├── cpio.mod
│         │         ├── cpio_be.mod
│         │         ├── cpuid.mod
│         │         ├── crc64.mod
│         │         ├── crypto.lst
│         │         ├── crypto.mod
│         │         ├── cryptodisk.mod
│         │         ├── cs5536.mod
│         │         ├── ctz_test.mod
│         │         ├── datehook.mod
│         │         ├── datetime.mod
│         │         ├── diskfilter.mod
│         │         ├── div.mod
│         │         ├── div_test.mod
│         │         ├── dm_nv.mod
│         │         ├── efiemu.mod
│         │         ├── ehci.mod
│         │         ├── elf.mod
│         │         ├── eval.mod
│         │         ├── exfctest.mod
│         │         ├── f2fs.mod
│         │         ├── fdt.lst
│         │         ├── file.mod
│         │         ├── freedos.mod
│         │         ├── fs.lst
│         │         ├── fshelp.mod
│         │         ├── functional_test.mod
│         │         ├── gcry_arcfour.mod
│         │         ├── gcry_blowfish.mod
│         │         ├── gcry_camellia.mod
│         │         ├── gcry_cast5.mod
│         │         ├── gcry_crc.mod
│         │         ├── gcry_des.mod
│         │         ├── gcry_dsa.mod
│         │         ├── gcry_idea.mod
│         │         ├── gcry_md4.mod
│         │         ├── gcry_rfc2268.mod
│         │         ├── gcry_rijndael.mod
│         │         ├── gcry_rmd160.mod
│         │         ├── gcry_rsa.mod
│         │         ├── gcry_seed.mod
│         │         ├── gcry_serpent.mod
│         │         ├── gcry_sha1.mod
│         │         ├── gcry_sha256.mod
│         │         ├── gcry_sha512.mod
│         │         ├── gcry_tiger.mod
│         │         ├── gcry_twofish.mod
│         │         ├── gcry_whirlpool.mod
│         │         ├── gdb.mod
│         │         ├── geli.mod
│         │         ├── gfxterm_menu.mod
│         │         ├── gptsync.mod
│         │         ├── hdparm.mod
│         │         ├── hello.mod
│         │         ├── hexdump.mod
│         │         ├── hfs.mod
│         │         ├── hfsplus.mod
│         │         ├── hfspluscomp.mod
│         │         ├── iorw.mod
│         │         ├── jfs.mod
│         │         ├── keylayouts.mod
│         │         ├── keystatus.mod
│         │         ├── ldm.mod
│         │         ├── legacy_password_test.mod
│         │         ├── legacycfg.mod
│         │         ├── loadenv.mod
│         │         ├── lsacpi.mod
│         │         ├── lsapm.mod
│         │         ├── lsmmap.mod
│         │         ├── luks.mod
│         │         ├── lvm.mod
│         │         ├── macbless.mod
│         │         ├── macho.mod
│         │         ├── mda_text.mod
│         │         ├── mdraid09.mod
│         │         ├── mdraid09_be.mod
│         │         ├── mdraid1x.mod
│         │         ├── memdisk.mod
│         │         ├── memrw.mod
│         │         ├── minix.mod
│         │         ├── minix2.mod
│         │         ├── minix2_be.mod
│         │         ├── minix3.mod
│         │         ├── minix3_be.mod
│         │         ├── minix_be.mod
│         │         ├── mmap.mod
│         │         ├── moddep.lst
│         │         ├── morse.mod
│         │         ├── mpi.mod
│         │         ├── msdospart.mod
│         │         ├── mul_test.mod
│         │         ├── multiboot.mod
│         │         ├── multiboot2.mod
│         │         ├── nativedisk.mod
│         │         ├── net.mod
│         │         ├── newc.mod
│         │         ├── nilfs2.mod
│         │         ├── ntfscomp.mod
│         │         ├── odc.mod
│         │         ├── offsetio.mod
│         │         ├── ohci.mod
│         │         ├── part_acorn.mod
│         │         ├── part_amiga.mod
│         │         ├── part_apple.mod
│         │         ├── part_bsd.mod
│         │         ├── part_dfly.mod
│         │         ├── part_dvh.mod
│         │         ├── part_plan.mod
│         │         ├── part_sun.mod
│         │         ├── part_sunpc.mod
│         │         ├── partmap.lst
│         │         ├── parttool.lst
│         │         ├── parttool.mod
│         │         ├── password.mod
│         │         ├── pata.mod
│         │         ├── pbkdf2.mod
│         │         ├── pbkdf2_test.mod
│         │         ├── pcidump.mod
│         │         ├── pgp.mod
│         │         ├── plan9.mod
│         │         ├── play.mod
│         │         ├── priority_queue.mod
│         │         ├── probe.mod
│         │         ├── procfs.mod
│         │         ├── progress.mod
│         │         ├── pxe.mod
│         │         ├── pxechain.mod
│         │         ├── raid5rec.mod
│         │         ├── raid6rec.mod
│         │         ├── random.mod
│         │         ├── rdmsr.mod
│         │         ├── regexp.mod
│         │         ├── reiserfs.mod
│         │         ├── relocator.mod
│         │         ├── romfs.mod
│         │         ├── scsi.mod
│         │         ├── search_fs_file.mod
│         │         ├── search_fs_uuid.mod
│         │         ├── search_label.mod
│         │         ├── sendkey.mod
│         │         ├── serial.mod
│         │         ├── setjmp.mod
│         │         ├── setjmp_test.mod
│         │         ├── setpci.mod
│         │         ├── sfs.mod
│         │         ├── shift_test.mod
│         │         ├── signature_test.mod
│         │         ├── sleep_test.mod
│         │         ├── smbios.mod
│         │         ├── spkmodem.mod
│         │         ├── strtoull_test.mod
│         │         ├── syslinuxcfg.mod
│         │         ├── terminal.lst
│         │         ├── terminfo.mod
│         │         ├── test_blockarg.mod
│         │         ├── testload.mod
│         │         ├── testspeed.mod
│         │         ├── tga.mod
│         │         ├── time.mod
│         │         ├── truecrypt.mod
│         │         ├── ufs1.mod
│         │         ├── ufs1_be.mod
│         │         ├── ufs2.mod
│         │         ├── uhci.mod
│         │         ├── usb.mod
│         │         ├── usbms.mod
│         │         ├── usbserial_common.mod
│         │         ├── usbserial_ftdi.mod
│         │         ├── usbserial_pl2303.mod
│         │         ├── usbserial_usbdebug.mod
│         │         ├── usbtest.mod
│         │         ├── verifiers.mod
│         │         ├── video.lst
│         │         ├── wrmsr.mod
│         │         ├── xnu.mod
│         │         ├── xnu_uuid.mod
│         │         ├── xnu_uuid_test.mod
│         │         ├── zfs.mod
│         │         ├── zfscrypt.mod
│         │         ├── zfsinfo.mod
│         │         └── zstd.mod
│         ├── keyboard.cfg
│         ├── localboot.cfg
│         ├── mips64el-efi
│         │         ├── adler32.mod
│         │         ├── affs.mod
│         │         ├── afs.mod
│         │         ├── archelp.mod
│         │         ├── bfs.mod
│         │         ├── blscfg.mod
│         │         ├── bswap_test.mod
│         │         ├── btrfs.mod
│         │         ├── cbfs.mod
│         │         ├── cmdline_cat_test.mod
│         │         ├── cmp.mod
│         │         ├── cmp_test.mod
│         │         ├── command.lst
│         │         ├── cpio.mod
│         │         ├── cpio_be.mod
│         │         ├── crc64.mod
│         │         ├── crypto.lst
│         │         ├── cryptodisk.mod
│         │         ├── ctz_test.mod
│         │         ├── date.mod
│         │         ├── datehook.mod
│         │         ├── disk.mod
│         │         ├── div.mod
│         │         ├── div_test.mod
│         │         ├── dm_nv.mod
│         │         ├── efinet.mod
│         │         ├── elf.mod
│         │         ├── eval.mod
│         │         ├── exfctest.mod
│         │         ├── f2fs.mod
│         │         ├── fdt.lst
│         │         ├── fs.lst
│         │         ├── functional_test.mod
│         │         ├── fwload.mod
│         │         ├── gcry_arcfour.mod
│         │         ├── gcry_blowfish.mod
│         │         ├── gcry_camellia.mod
│         │         ├── gcry_cast5.mod
│         │         ├── gcry_crc.mod
│         │         ├── gcry_des.mod
│         │         ├── gcry_dsa.mod
│         │         ├── gcry_idea.mod
│         │         ├── gcry_md4.mod
│         │         ├── gcry_rfc2268.mod
│         │         ├── gcry_rijndael.mod
│         │         ├── gcry_rmd160.mod
│         │         ├── gcry_rsa.mod
│         │         ├── gcry_seed.mod
│         │         ├── gcry_serpent.mod
│         │         ├── gcry_sha1.mod
│         │         ├── gcry_sha256.mod
│         │         ├── gcry_tiger.mod
│         │         ├── gcry_twofish.mod
│         │         ├── gcry_whirlpool.mod
│         │         ├── geli.mod
│         │         ├── gfxterm_menu.mod
│         │         ├── gptsync.mod
│         │         ├── hello.mod
│         │         ├── help.mod
│         │         ├── hexdump.mod
│         │         ├── hfs.mod
│         │         ├── hfspluscomp.mod
│         │         ├── jfs.mod
│         │         ├── keystatus.mod
│         │         ├── ldm.mod
│         │         ├── loadenv.mod
│         │         ├── lsacpi.mod
│         │         ├── lsefi.mod
│         │         ├── lsefimmap.mod
│         │         ├── lsefisystab.mod
│         │         ├── lsmmap.mod
│         │         ├── lssal.mod
│         │         ├── luks.mod
│         │         ├── lvm.mod
│         │         ├── macbless.mod
│         │         ├── macho.mod
│         │         ├── mdraid09.mod
│         │         ├── mdraid09_be.mod
│         │         ├── mdraid1x.mod
│         │         ├── memdisk.mod
│         │         ├── memrw.mod
│         │         ├── minix.mod
│         │         ├── minix2.mod
│         │         ├── minix2_be.mod
│         │         ├── minix3.mod
│         │         ├── minix3_be.mod
│         │         ├── minix_be.mod
│         │         ├── moddep.lst
│         │         ├── mouse.mod
│         │         ├── mpi.mod
│         │         ├── msdospart.mod
│         │         ├── mul_test.mod
│         │         ├── nilfs2.mod
│         │         ├── normal.mod
│         │         ├── ntfscomp.mod
│         │         ├── odc.mod
│         │         ├── offsetio.mod
│         │         ├── part_acorn.mod
│         │         ├── part_amiga.mod
│         │         ├── part_bsd.mod
│         │         ├── part_dfly.mod
│         │         ├── part_dvh.mod
│         │         ├── part_plan.mod
│         │         ├── part_sun.mod
│         │         ├── part_sunpc.mod
│         │         ├── partmap.lst
│         │         ├── parttool.lst
│         │         ├── parttool.mod
│         │         ├── password.mod
│         │         ├── pbkdf2_test.mod
│         │         ├── pgp.mod
│         │         ├── probe.mod
│         │         ├── procfs.mod
│         │         ├── progress.mod
│         │         ├── raid5rec.mod
│         │         ├── raid6rec.mod
│         │         ├── reiserfs.mod
│         │         ├── relocator.mod
│         │         ├── romfs.mod
│         │         ├── scsi.mod
│         │         ├── search_fs_file.mod
│         │         ├── search_fs_uuid.mod
│         │         ├── search_label.mod
│         │         ├── setjmp.mod
│         │         ├── setjmp_test.mod
│         │         ├── sfs.mod
│         │         ├── shift_test.mod
│         │         ├── signature_test.mod
│         │         ├── sleep_test.mod
│         │         ├── smbios.mod
│         │         ├── strtoull_test.mod
│         │         ├── syslinuxcfg.mod
│         │         ├── terminal.lst
│         │         ├── test_blockarg.mod
│         │         ├── testload.mod
│         │         ├── testspeed.mod
│         │         ├── tga.mod
│         │         ├── time.mod
│         │         ├── tr.mod
│         │         ├── ufs1.mod
│         │         ├── ufs1_be.mod
│         │         ├── ufs2.mod
│         │         ├── verifiers.mod
│         │         ├── video.lst
│         │         ├── videoinfo.mod
│         │         ├── videotest.mod
│         │         ├── videotest_checksum.mod
│         │         ├── xnu_uuid.mod
│         │         ├── xnu_uuid_test.mod
│         │         ├── zfs.mod
│         │         ├── zfscrypt.mod
│         │         ├── zfsinfo.mod
│         │         └── zstd.mod
│         ├── power.cfg
│         ├── themes
│         │         └── ventoy
│         │             ├── background.png
│         │             ├── menu_c.png
│         │             ├── menu_e.png
│         │             ├── menu_n.png
│         │             ├── menu_ne.png
│         │             ├── menu_nw.png
│         │             ├── menu_s.png
│         │             ├── menu_se.png
│         │             ├── menu_sw.png
│         │             ├── menu_w.png
│         │             ├── select_c.png
│         │             ├── slider_c.png
│         │             ├── slider_n.png
│         │             ├── slider_s.png
│         │             ├── terminal_box_c.png
│         │             ├── terminal_box_e.png
│         │             ├── terminal_box_n.png
│         │             ├── terminal_box_ne.png
│         │             ├── terminal_box_nw.png
│         │             ├── terminal_box_s.png
│         │             ├── terminal_box_se.png
│         │             ├── terminal_box_sw.png
│         │             ├── terminal_box_w.png
│         │             └── theme.txt
│         └── x86_64-efi
│             ├── adler32.mod
│             ├── affs.mod
│             ├── afs.mod
│             ├── ahci.mod
│             ├── aout.mod
│             ├── appleldr.mod
│             ├── archelp.mod
│             ├── ata.mod
│             ├── backtrace.mod
│             ├── bfs.mod
│             ├── blscfg.mod
│             ├── bsd.mod
│             ├── bswap_test.mod
│             ├── btrfs.mod
│             ├── cbfs.mod
│             ├── cbls.mod
│             ├── cbmemc.mod
│             ├── cbtable.mod
│             ├── cbtime.mod
│             ├── cmdline_cat_test.mod
│             ├── cmp.mod
│             ├── cmp_test.mod
│             ├── command.lst
│             ├── cpio.mod
│             ├── cpio_be.mod
│             ├── cpuid.mod
│             ├── crc64.mod
│             ├── crypto.lst
│             ├── cryptodisk.mod
│             ├── cs5536.mod
│             ├── ctz_test.mod
│             ├── date.mod
│             ├── datehook.mod
│             ├── disk.mod
│             ├── div.mod
│             ├── div_test.mod
│             ├── dm_nv.mod
│             ├── efinet.mod
│             ├── ehci.mod
│             ├── elf.mod
│             ├── eval.mod
│             ├── exfctest.mod
│             ├── f2fs.mod
│             ├── fdt.lst
│             ├── fixvideo.mod
│             ├── fs.lst
│             ├── functional_test.mod
│             ├── gcry_arcfour.mod
│             ├── gcry_blowfish.mod
│             ├── gcry_camellia.mod
│             ├── gcry_cast5.mod
│             ├── gcry_crc.mod
│             ├── gcry_des.mod
│             ├── gcry_dsa.mod
│             ├── gcry_idea.mod
│             ├── gcry_md4.mod
│             ├── gcry_rfc2268.mod
│             ├── gcry_rijndael.mod
│             ├── gcry_rmd160.mod
│             ├── gcry_rsa.mod
│             ├── gcry_seed.mod
│             ├── gcry_serpent.mod
│             ├── gcry_sha1.mod
│             ├── gcry_sha256.mod
│             ├── gcry_tiger.mod
│             ├── gcry_twofish.mod
│             ├── gcry_whirlpool.mod
│             ├── geli.mod
│             ├── gptsync.mod
│             ├── hdparm.mod
│             ├── hello.mod
│             ├── help.mod
│             ├── hexdump.mod
│             ├── hfs.mod
│             ├── hfspluscomp.mod
│             ├── iorw.mod
│             ├── jfs.mod
│             ├── keylayouts.mod
│             ├── keystatus.mod
│             ├── ldm.mod
│             ├── legacy_password_test.mod
│             ├── legacycfg.mod
│             ├── linux16.mod
│             ├── loadbios.mod
│             ├── loadenv.mod
│             ├── lsacpi.mod
│             ├── lsefi.mod
│             ├── lsefimmap.mod
│             ├── lsefisystab.mod
│             ├── lsmmap.mod
│             ├── lspci.mod
│             ├── lssal.mod
│             ├── luks.mod
│             ├── lvm.mod
│             ├── macbless.mod
│             ├── macho.mod
│             ├── mdraid09.mod
│             ├── mdraid09_be.mod
│             ├── mdraid1x.mod
│             ├── memdisk.mod
│             ├── memrw.mod
│             ├── minix.mod
│             ├── minix2.mod
│             ├── minix2_be.mod
│             ├── minix3.mod
│             ├── minix3_be.mod
│             ├── minix_be.mod
│             ├── moddep.lst
│             ├── morse.mod
│             ├── mpi.mod
│             ├── msdospart.mod
│             ├── mul_test.mod
│             ├── multiboot.mod
│             ├── multiboot2.mod
│             ├── nativedisk.mod
│             ├── nilfs2.mod
│             ├── normal.mod
│             ├── ntfscomp.mod
│             ├── odc.mod
│             ├── offsetio.mod
│             ├── ohci.mod
│             ├── part_acorn.mod
│             ├── part_amiga.mod
│             ├── part_bsd.mod
│             ├── part_dfly.mod
│             ├── part_dvh.mod
│             ├── part_plan.mod
│             ├── part_sun.mod
│             ├── part_sunpc.mod
│             ├── partmap.lst
│             ├── parttool.lst
│             ├── parttool.mod
│             ├── password.mod
│             ├── pata.mod
│             ├── pbkdf2_test.mod
│             ├── pcidump.mod
│             ├── pgp.mod
│             ├── play.mod
│             ├── probe.mod
│             ├── procfs.mod
│             ├── progress.mod
│             ├── raid5rec.mod
│             ├── raid6rec.mod
│             ├── random.mod
│             ├── rdmsr.mod
│             ├── reiserfs.mod
│             ├── romfs.mod
│             ├── scsi.mod
│             ├── search_fs_file.mod
│             ├── search_fs_uuid.mod
│             ├── search_label.mod
│             ├── setjmp.mod
│             ├── setjmp_test.mod
│             ├── setpci.mod
│             ├── sfs.mod
│             ├── shift_test.mod
│             ├── shim_lock.mod
│             ├── signature_test.mod
│             ├── sleep_test.mod
│             ├── smbios.mod
│             ├── spkmodem.mod
│             ├── strtoull_test.mod
│             ├── syslinuxcfg.mod
│             ├── terminal.lst
│             ├── test_blockarg.mod
│             ├── testload.mod
│             ├── testspeed.mod
│             ├── tga.mod
│             ├── time.mod
│             ├── tpm.mod
│             ├── tr.mod
│             ├── ufs1.mod
│             ├── ufs1_be.mod
│             ├── ufs2.mod
│             ├── uhci.mod
│             ├── usb.mod
│             ├── usbms.mod
│             ├── usbserial_common.mod
│             ├── usbserial_ftdi.mod
│             ├── usbserial_pl2303.mod
│             ├── usbserial_usbdebug.mod
│             ├── usbtest.mod
│             ├── verifiers.mod
│             ├── video.lst
│             ├── videoinfo.mod
│             ├── videotest.mod
│             ├── videotest_checksum.mod
│             ├── wrmsr.mod
│             ├── xnu.mod
│             ├── xnu_uuid.mod
│             ├── xnu_uuid_test.mod
│             ├── zfs.mod
│             ├── zfscrypt.mod
│             ├── zfsinfo.mod
│             └── zstd.mod
├── tool
│         ├── mount.exfat-fuse_aarch64
│         ├── mount.exfat-fuse_i386
│         └── mount.exfat-fuse_x86_64
└── ventoy
    ├── 7z
    │         ├── 32
    │         │         └── 7za.xz
    │         └── 64
    │             └── 7za.xz
    ├── dragonfly.mfs.xz
    ├── imdisk
    │         ├── 32
    │         │         ├── imdisk.cpl
    │         │         ├── imdisk.exe
    │         │         └── imdisk.sys
    │         └── 64
    │             ├── imdisk.cpl
    │             ├── imdisk.exe
    │             └── imdisk.sys
    ├── ipxe.krn
    ├── iso9660_aa64.efi
    ├── iso9660_ia32.efi
    ├── iso9660_x64.efi
    ├── memdisk
    ├── udf_aa64.efi
    ├── udf_ia32.efi
    ├── udf_x64.efi
    ├── ventoy.cpio
    ├── ventoy_aa64.efi
    ├── ventoy_arm64.cpio
    ├── ventoy_efiboot.img.xz
    ├── ventoy_ia32.efi
    ├── ventoy_mips64.cpio
    ├── ventoy_unix.cpio
    ├── ventoy_x64.efi
    ├── ventoy_x86.cpio
    ├── vtloopex.cpio
    ├── vtoyjump32.exe
    ├── vtoyjump64.exe
    ├── vtoyutil_aa64.efi
    ├── vtoyutil_ia32.efi
    ├── vtoyutil_x64.efi
    ├── wimboot.i386.efi.xz
    └── wimboot.x86_64.xz

19 directories, 981 files
```