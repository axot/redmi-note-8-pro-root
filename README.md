# The manual for getting root of Redmi Note 8 Pro MIUI 12.5.6

1. extract boot.img from https://miuiver.com/tag/begonia-stable-rom/
2. generate magisk patched boot.img(the name of `magisk_patched-25100_5MyUS.img` in following step)
   1. check the steps from https://topjohnwu.github.io/Magisk/install.html
3. (optional) flash a custom recovery partition.
   1. I was using this, https://pan.baidu.com/s/15lHG5eibrZ3nsS8CM_JVqg#list/path=%2Fsharelink1542921633-770875344366009%2F小米%2F红米Note8Pro%2F11系统专用-请勿乱刷&parentPath=%2Fsharelink1542921633-770875344366009
   2. password pc5n
   3. flash
      ```
      fastboot flash recovery twrp.img
      ```
4. flash vbmeta
   ```
   fastboot --disable-verity --disable-verification flash vbmeta ./begonia_images_V12.5.6.0.RGGCNXM_20220602.0000.00_11.0_cn/images/vbmeta.img
   ```
5. flash magisk patched boot partition
   ```
    fastboot --disable-verity --disable-verification flash boot ./magisk_patched-25100_5MyUS.img
   ```

# useful commands
## rollback to original boot secion
```
fastboot flash boot ./begonia_images_V12.5.6.0.RGGCNXM_20220602.0000.00_11.0_cn/images/boot.img
```

## reboot from fastboot
```
fastboot reboot
fastboot reboot-recovery
```

## reboot from MIUI
```
adb reboot bootloader
```

# adb shell as root
```
adb shell
su
```

## remount ro as rw, don't do this with magisk, if you modificated filses in /system, the OS will get stuck
mount -o rw,remount /

# Magisk Modules
1. Gapps
    1. install gapps from source: https://github.com/LSPosed/MagiskOnWSA
    2. i was using a prebuild version fro MIUI 12.5 from https://drive.google.com/file/d/13Rdy36ppLHVwI4O9cn_BTckTjheqVygs/view
    3. then install the lasted google play store app from apk mirror
2. Uperf
   1. source from: https://github.com/yc9559/uperf/releases
   2. install both sfanalysis-magisk-22.06.05.zip and uperf-dev-22.07.09.zip