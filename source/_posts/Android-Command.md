---
title: Android Command
date: 2019-08-13 21:22:52
updated: 2019-08-13 21:22:52
categories: Android
tags: [Android,Command]
---

 

众所周知 Android系统是基于linux内核的，因而linux上的一些命令行基本上Android上也能适用，有时候有些有些阉割的命令也可以通过busybox这个命令工具做补充。本文总结Android开发常用的一些的命令行操作，带你走进不一样的空间体验。命令太多，建议收藏，有需要时搜索就行。

![android-command](https://lairdli.top/images/android-command.jpg)

<!--more-->

# Adb常用命令

  ### adb connect ip:port
  连接指定设备
  ```shell
    Laird-MacBook-Pro:~ laird$ adb connect 192.168.3.43:5555
    already connected to 192.168.3.43:5555
    Laird-MacBook-Pro:~ laird$
  ```
 ### adb disconnect
  断开指定设备
  ```shell
    Laird-MacBook-Pro:~ laird$ adb disconnect
    disconnected everything
    Laird-MacBook-Pro:~ laird$
  ```

 ### adb devices
  列出已连接设备
  ```shell
    Laird-MacBook-Pro:~ laird$ adb devices
    List of devices attached
    192.168.3.43:5555	device
    Laird-MacBook-Pro:~ laird$
  ```

 ### adb kill-server
  adb 关闭服务
  ```shell
    Laird-MacBook-Pro:~ laird$ adb kill-server
    Laird-MacBook-Pro:~ laird$
  ```
 ### adb start-server
  adb 启动服务
  ```shell
    Laird-MacBook-Pro:~ laird$ adb start-server
    Laird-MacBook-Pro:~ laird$
  ```
 ### adb install
  安装应用 adb install -r -t apk路径
  >-r,-t,-d 选填
  >-r表示替换掉原来的apk；如果没有-r，否则会提示apk已经存在
  >-t表示可安装测试debug版本的apk,否则会提示TEST_ONLY
  >-d表示可以降级安装，否则会提示apk版本太低

  ```shell
    Laird-MacBook-Pro:~ laird$ adb install -r -t -d /Users/laird/git/AndroidTVappTutorial/app/build/outputs/apk/debug/app-debug.apk
    Performing Push Install
    /Users/laird/Work/05workspace/git/AndroidTV... pushed. 1.3 MB/s (2777025 bytes in 1.994s)
        pkg: /data/local/tmp/app-debug.apk
    Success
    Laird-MacBook-Pro:~ laird$
  ```
 ### adb uninstall
  卸载应用，后面指定应用包名
  ```shell
    Laird-MacBook-Pro:~ laird$ adb uninstall com.example.android.tvleanback
    Success
    Laird-MacBook-Pro:~ laird$
  ```
 ### adb logcat
  抓取系统日志，建议带上时间戳，并写入文件
  ```shell
    Laird-MacBook-Pro:~ laird$ adb logcat -vtime > android.log

  ```
  如需结束，按下^C
  ```shell
    Laird-MacBook-Pro:~ laird$ adb logcat -vtime > android.log
    ^C
    Laird-MacBook-Pro:~ laird$
  ```
 ### adb root
  获取root权限
  ```shell
    Laird-MacBook-Pro:~ laird$ adb root
    restarting adbd as root
    Laird-MacBook-Pro:~ laird$
  ```
 ### adb remount
  挂载系统
  ```shell
    Laird-MacBook-Pro:~ laird$ adb remount
    remount succeeded
    Laird-MacBook-Pro:~ laird$
  ```
 ### adb reboot
  重启系统
  ```shell
    Laird-MacBook-Pro:~ laird$ adb reboot 
    Laird-MacBook-Pro:~ laird$
  ```
 ### adb shell
  进入命令行模式
  ```shell
    Laird-MacBook-Pro:~ laird$ adb shell
    shell@pineapple:/ $
  ```

 ### adb -s ...
  如果有adb连接有多台设备，可用-s指定设备识别号后，再后面再加命令
  识别号可通过adb devices查看
  ```shell
    Laird-MacBook-Pro:~ laird$ adb devices
    List of devices attached
    192.168.3.183:5555	device
    192.168.3.18:5555	offline
    192.168.3.43:5555	device
  ```
```
  操作指定的设备
  ```shell
    Laird-MacBook-Pro:~ laird$ adb -s 192.168.3.183:5555 root
    adbd is already running as root
    Laird-MacBook-Pro:~ laird$
    Laird-MacBook-Pro:~ laird$ adb -s 192.168.3.43:5555 shell
    shell@pineapple:/ $
```

# Android-Linux 常用命令


## 系统信息

 ### busybox uname -m 
  显示机器的处理器架构(2) 
  ```shell
    shell@pineapple:/ $ busybox uname -m
    armv7l
    shell@pineapple:/ $
  ```

 ### busybox uname -r 
  显示正在使用的内核版本
  ```shell
    shell@pineapple:/ $ busybox uname -r
    3.10.40
    shell@pineapple:/ $
  ```

 ### cat /proc/cpuinfo 
  显示CPU info的信息 
  ```shell
    shell@pineapple:/ $  cat /proc/cpuinfo
    processor	: 0
    model name	: ARMv7 Processor rev 4 (v7l)
    BogoMIPS	: 1377.06
    ......
    shell@pineapple:/ $
  ```

 ### cat /proc/meminfo 

  查看内存使用 

  ```shell
    shell@pineapple:/ $ cat /proc/meminfo
    MemTotal:         921624 kB
    MemFree:           58280 kB
    Buffers:           13696 kB
    Cached:           295604 kB
    SwapCached:          116 kB
    Active:           334472 kB
    Inactive:         310756 kB
    Active(anon):     172492 kB
    Inactive(anon):   172312 kB
    Active(file):     161980 kB
  ......
    shell@pineapple:/ $
  ```

 ### cat /proc/version 
  显示内核的版本 
  ```shell
    shell@pineapple:/ $ cat /proc/version
    Linux version 3.10.40 (root@ubuntukaifa) (gcc version 4.7.2 (Sourcery CodeBench Lite 2012.09-64) ) #148 SMP PREEMPT Wed Jul 10 17:36:30 CST 2019
    shell@pineapple:/ $
  ```

 ### cat /proc/net/dev 

  显示网络适配器及统计 
  ```shell
    Inter-|   Receive                                                |  Transmit
    face |bytes    packets errs drop fifo frame compressed multicast|bytes    packets errs drop fifo colls carrier compressed
       sit0:       0       0    0    0    0     0          0         0        0       0    0    0    0     0       0          0
         lo:   33251      32    0    0    0     0          0         0    33251      32    0    0    0     0       0          0
      eth0: 23879158  130231    0   10    0     0          0     92837 11739459   41693    0    0    0     0       0          0
    ip6tnl0:       0       0    0    0    0     0          0         0        0       0    0    0    0     0       0          0
    shell@pineapple:/ $
  ```

 ### cat /proc/mounts
   显示已加载的文件系统 
   ```shell
   shell@pineapple:/ $ cat /proc/mounts
    rootfs / rootfs ro,relatime 0 0
    tmpfs /dev tmpfs rw,nosuid,relatime,mode=755 0 0
    devpts /dev/pts devpts rw,relatime,mode=600 0 0
    ......
    /dev/block/platform/mstar_mci.0/by-name/system /system ext4 ro,relatime,data=ordered 0 0
    /dev/block/platform/mstar_mci.0/by-name/cache /cache ext4 rw,nosuid,nodev,noatime,data=ordered 0 0
    /dev/block/platform/mstar_mci.0/by-name/userdata /data ext4 rw,nosuid,......

   ```

 ### busybox cal 2019 
  显示2019年的日历表
  ```shell
    shell@pineapple:/ $ busybox cal 2019
                                2019

        January               February               March
    Su Mo Tu We Th Fr Sa  Su Mo Tu We Th Fr Sa  Su Mo Tu We Th Fr Sa
        1  2  3  4  5                  1  2                  1  2
    6  7  8  9 10 11 12   3  4  5  6  7  8  9   3  4  5  6  7  8  9
    13 14 15 16 17 18 19  10 11 12 13 14 15 16  10 11 12 13 14 15 16
    20 21 22 23 24 25 26  17 18 19 20 21 22 23  17 18 19 20 21 22 23
    27 28 29 30 31        24 25 26 27 28        24 25 26 27 28 29 30
                                                31
    ......

    shell@pineapple:/ $
  ```

 ### date
  显示系统日期 
  ```shell
    127|shell@pineapple:/ $ date
    Mon Aug 12 16:50:24 CST 2019
    shell@pineapple:/ $
  ```

 ### date -s "yyyymmdd.hhmmss"
  设置日期和时间 
  ```shell
    shell@pineapple:/ # date -s "20190823.172522"
    Fri Aug 23 17:25:22 CST 2019
    shell@pineapple:/ # date
    Fri Aug 23 17:25:24 CST 2019
    shell@pineapple:/ #
  ```

 ### getprop
  查看系统属性
  ```shell
    shell@pineapple:/ # getprop
    [bluetooth.sco_over_btmic]: [1]
    [chrome.tv.hole_threshold]: [0]
    [config.disable_bluetooth]: [0]
    [dalvik.vm.dex2oat-Xms]: [64m]
    [dalvik.vm.dex2oat-Xmx]: [512m]
    [dalvik.vm.dexopt-flags]: [m=y]
    [dalvik.vm.heapgrowthlimit]: [128m]
    [dalvik.vm.heapmaxfree]: [8m]
    [dalvik.vm.heapminfree]: [512k]
    [dalvik.vm.heapsize]: [256m]
    ......
  ```
  也可以过滤字段 getprop | grep 过滤字符
  ```shell
    shell@pineapple:/ # getprop | grep "version"
    [mstar.primary.audioHAL.version]: [Primary audioHAL version 3.0.04]
    [ro.build.version.all_codenames]: [REL]
    [ro.build.version.base_os]: []
    [ro.build.version.codename]: [REL]
    [ro.build.version.incremental]: [GD__-18.03.100.20.11.C2P]
    [ro.build.version.release]: [5.1.1]
    [ro.build.version.sdk]: [22]
    [ro.build.version.security_patch]: [2016-03-01]
    [ro.opengles.version]: [131072]
    shell@pineapple:/ #
  ```
  也也可指定属性 getprop 属性名
  ```shell
    shell@pineapple:/ # getprop persist.sys.timezone
    Asia/Shanghai
    shell@pineapple:/ #
  ```

 ### setprop
  设置系统属性,注意有些系统属性设置后重启可能会失效
  ```shell
    shell@pineapple:/ # setprop persist.sys.test testvalue
    shell@pineapple:/ # getprop persist.sys.test
    testvalue
    shell@pineapple:/ #
  ```

 ### dumpsys
  dump系统所有的信息，由于信息量太大，建议会写入文件
  ```shell
    shell@pineapple:/ #   dumpsys > dumpsys.log
  ```

 ### dumpsys package
  dump应用信息，一般可以指定包名，查看应用信息
  ```shell
    shell@pineapple:/ # dumpsys package tv.lairdli.top
    Activity Resolver Table:
    Non-Data Actions:
        android.intent.action.MAIN:
            c015d7f tv.lairdli.top/.androidtvapptutorial.MainTvActivity

    Key Set Manager:
    [tv.lairdli.top]
        Signing KeySets: 139

    Packages:
    Package [tv.lairdli.top] (164bb14c):
    ......
  ```

 ### dumpsys meminfo
  查看内存信息，可指定应用包名或者进程pid
  ```shell
  127|shell@pineapple:/ $ dumpsys meminfo com.example.android.persistence
    Applications Memory Usage (kB):
    Uptime: 8640528 Realtime: 8640528

    ** MEMINFO in pid 5534 [com.example.android.persistence] **
                    Pss  Private  Private  Swapped     Heap     Heap     Heap
                    Total    Dirty    Clean    Dirty     Size    Alloc     Free
                    ------   ------   ------   ------   ------   ------   ------
    Native Heap     3882     3852        0      284    12288     5183     7104
    Dalvik Heap     7002     6952        0        0    11564     7325     4239
    Dalvik Other     8618     8604        0        0
            Stack      312      312        0        0
        Other dev       20        0       20        0
        .so mmap      924      100      196      188
        .apk mmap      396        0       92        0
        .ttf mmap       59        0       48        0
        .dex mmap       96        0       92        0
        .oat mmap     1462        0      516        0
        .art mmap      862      636        0        8
    ......

    shell@pineapple:/ $
  ```

 ### ps
  查看当前系统运行应用进程，可配合grep使用
  ```shell
    shell@pineapple:/ $ ps | grep example
    u0_a95    5534  1189  1034160 52728 ffffffff 00000000 S com.example.android.persistence
    shell@pineapple:/ $
  ```
```
  
 ### top
  查看当前活跃的进程可加参数-m 显示个数
  ```shell
    shell@pineapple:/ $ top -m 3

    User 20%, System 9%, IOW 0%, IRQ 0%
    User 116 + Nice 1 + Sys 52 + Idle 401 + IOW 0 + IRQ 0 + SIRQ 1 = 571

    PID PR CPU% S  #THR     VSS     RSS PCY UID      Name
    6160  3  15% S    31 1024760K  38488K  bg u0_a57   com.dangbeimarket:bdservice_v1
    2231  2   4% S    68 1071148K  56480K  bg u0_a60   com.douyu.xl.douyutv
    1183  0   2% S    73 386908K   7020K  fg root     /applications/bin/MiSysSrv
    ^C
    130|shell@pineapple:/ $
```

 ### logcat 
  查看日志，建议加上时间戳 ，TAG等
  ```shell
    130|shell@pineapple:/ $ logcat -vtime -s TAG AndroidRuntime DEBUG
    --------- beginning of main
    --------- beginning of system
    08-23 18:30:53.294 I/TAG     ( 5940): registerNewOutGoingCallReceiver mIsNewOutGoingCallRegistered false

  ```

 ### &
  一个神奇的指令，命令行+& ，能将命令置于后台，不影响前台输出

  ```shell
    shell@pineapple:/ $ top -m 2 &
    [2] 6583
    shell@pineapple:/ $

    User 18%, System 7%, IOW 0%, IRQ 0%
    User 55 + Nice 1 + Sys 24 + Idle 228 + IOW 0 + IRQ 0 + SIRQ 1 = 309

    PID PR CPU% S  #THR     VSS     RSS PCY UID      Name
    1164  1   7% S     7  28496K  10012K  bg logd     /system/bin/logd
    5940  0   6% S    76 1089524K  69544K  bg u0_a61   com.duowan.kiwitv

    shell@pineapple:/ $
  ```

### busybox killall system-server
重启服务，可模拟快速重启，硬件不重启

  ```
  shell
  shell@pineapple: $ su
  shell@pineapple: $  busybox killall system_server
  shell@pineapple: $ 
  Laird-MacBook-Pro:Documents laird$
  ```


## 文件路径

 ### cd -
  切换到上一次路径
  ```shell
    shell@Hi3751V551:/ $ cd /data
    shell@Hi3751V551:/data $ cd /system
    shell@Hi3751V551:/system $ cd -
    /data
    shell@Hi3751V551:/data $
  ```
 ### ll -a
  列出目录文件，含权限信息,-a 包含隐藏文件
  ```shell
    shell@Hi3751V551:/ $ ll
    lrwxrwxrwx root     root              1970-01-01 08:00 Customer -> /tvcustomer/Customer
    lrwxrwxrwx root     root              1970-01-01 08:00 Database -> /tvdatabase/Database
    lrwxrwxrwx root     root              1970-01-01 08:00 DatabaseBackup -> /tvdatabase/DatabaseBackup
    dr-xr-xr-x root     root              1970-01-01 08:00 acct
    lrwxrwxrwx root     root              1970-01-01 08:00 applications -> /tvservice/applications
    drwxr-xr-x root     root              2017-01-01 08:01 atv
    drwxrwx--- system   cache             2018-11-03 20:10 cache
    ......
  ```
 ### mkdir dir
  创建文件夹
  ```shell
    root@generic_x86:/sdcard # mkdir testDir
    root@generic_x86:/sdcard # ll
    ...
    drwxrwx--- root     sdcard_r          2019-03-23 06:00 Ringtones
    drwxrwx--- root     sdcard_r          2019-08-12 22:54 testDir
    root@generic_x86:/sdcard #
  ```
 ### rm -rf dir
  删除文件夹
  ```shell
    root@generic_x86:/sdcard # rm -rf testDir/
    root@generic_x86:/sdcard # ll test*
    test*: No such file or directory
    1|root@generic_x86:/sdcard #
  ```
 ### ln file link
  创建硬链接，拷贝+同步
  硬链接不能指向自身文件系统外的文件，即不能跨硬盘分区(软链接可以)。
  硬链接不能指向目录。
 ### ln -s file link
  创建软链接，软链接可以类比Windows上的快捷方式

 ### df
  显示系统挂载盘
  ```shell
    root@generic_x86:/ # df
    Filesystem               Size     Used     Free   Blksize
    /dev                   757.7M    52.0K   757.6M   4096
    /mnt/asec              757.7M     0.0K   757.7M   4096
    /mnt/obb               757.7M     0.0K   757.7M   4096
    /system                823.3M   594.9M   228.4M   4096
    /cache                  61.0M    60.0K    60.9M   4096
    /data                  779.3M   299.2M   480.1M   4096
    /mnt/media_rw/sdcard   510.0M    54.0K   509.9M   2048
    /mnt/secure/asec       510.0M    54.0K   509.9M   2048
    /storage/sdcard        510.0M    54.0K   509.9M   2048
    root@generic_x86:/ #
  ```
 ### du -sh *
  显示当前文件夹下子项大小
  ```shell
    root@generic_x86:/sdcard # du -sh *
    2.0K	Alarms
    22K	Android
    2.0K	DCIM
    2.0K	Download
    2.0K	LOST.DIR
    2.0K	Movies
    2.0K	Music
    2.0K	Notifications
    2.0K	Pictures
    2.0K	Podcasts
    2.0K	Ringtones
    2.0K	test
    6.0K	testDir
    root@generic_x86:/sdcard #
  ```
 ### du -sh ./
  显示当前文件夹总大小
  ```shell
    root@generic_x86:/sdcard # du -sh ./
    52K	./
    1|root@generic_x86:/sdcard #
  ```
 ### touch
  touch命令用于修改文件或者目录的时间属性，包括存取时间和更改时间。
  若文件不存在，系统会建立一个新的文件。
  ls -l 可以显示档案的时间记录。
  ```shell
    root@generic_x86:/sdcard/testDir # ll -l
    root@generic_x86:/sdcard/testDir # touch testfile
    root@generic_x86:/sdcard/testDir # ll -l
    -rwxrwx--- root     sdcard_r        0 2019-08-12 23:11 testfile
    root@generic_x86:/sdcard/testDir # touch testfile
    root@generic_x86:/sdcard/testDir # ll -l
    -rwxrwx--- root     sdcard_r        0 2019-08-12 23:12 testfile
    root@generic_x86:/sdcard/testDir #
  ```
 ### chmod 777 file/dir
  修改文件/文件夹读写权限
  ```shell
    root@generic_x86:/data # touch testFile
    root@generic_x86:/data # ll testFile
    -rw-rw-rw- root     root            0 2019-08-12 23:14 testFile
    root@generic_x86:/data # chmod 777 testFile
    root@generic_x86:/data # ll testFile
    -rwxrwxrwx root     root            0 2019-08-12 23:14 testFile
    root@generic_x86:/data #
  ```
### tar  

  - tar -cvf archive.tar file1 
    压缩
  ```shell
    shell@pineapple:/sdcard # ll test/
    -rw-rw---- root     sdcard_r       15 2019-08-13 09:35 testfile
    -rw-rw---- root     sdcard_r       15 2019-08-13 11:52 testfileRemote
    shell@pineapple:/sdcard # busybox tar -cvf test.tar test
    test/
    test/testfile
    test/testfileRemote
    shell@pineapple:/sdcard # ll test.tar
    -rw-rw---- root     sdcard_r     3584 2019-08-13 16:07 test.tar
    shell@pineapple:/sdcard #
  ```

  - tar -xvf archive.tar 
    解压
  ```shell
    shell@pineapple:/sdcard # rm -rf test/
    shell@pineapple:/sdcard # ll test*
    -rw-rw---- root     sdcard_r     3584 2019-08-13 16:07 test.tar
    shell@pineapple:/sdcard # busybox tar -xvf test.tar
    test/
    test/testfile
    test/testfileRemote
    shell@pineapple:/sdcard # ll test/
    -rw-rw---- root     sdcard_r       15 2019-08-13 09:35 testfile
    -rw-rw---- root     sdcard_r       15 2019-08-13 11:52 testfileRemote
    shell@pineapple:/sdcard #
  ```


### busybox find
  - busybox find -name tmp 
      从当前目录搜索文件和目录,指定名称
      ```shell
        shell@pineapple:/ # busybox find . -name default
        ./sys/devices/virtual/bdi/default
        ./sys/class/bdi/default
        ./sys/kernel/debug/bdi/default
        ./proc/sys/net/ipv4/conf/default
        ./proc/sys/net/ipv4/neigh/default
        ./proc/sys/net/ipv6/conf/default
        ./proc/sys/net/ipv6/neigh/default
        shell@pineapple:/ #
      ```

  - busybox find -name *prop 
      从当前目录搜索后缀为.prop的文件
      ```shell
        shell@pineapple:/ # busybox find -name "*.prop"
        ./system/build.prop
        find: ./proc/1167/task/1378/fd/67: No such file or directory
        find: ./proc/1167/task/1399/fd/48: No such file or directory
        find: ./proc/5691/fdinfo/34: No such file or directory
        ./default.prop
        shell@pineapple:/ #
      ```
  - busybox find -name '*.prop' |  grep 'build' 
    从当前搜索文件名含字符build
    ```shell
      shell@pineapple:/ # busybox find -name "*.prop" | grep "build"
      ./system/build.prop
      shell@pineapple:/ #
    ```
  - busybox find -name '*.prop' | busybox xargs grep 'version' 
    从当前搜索文件名为.prop后缀，且文件内容包含version的文件
    ```shell
      shell@pineapple:/ #busybox find -name '*.prop' | busybox xargs grep 'version'                         
      find: ./proc/1167/task/1368/fd/59: No such file or directory
      find: ./proc/1167/task/1375/fd/22: No such file or directory
      ...
      ./system/build.prop:ro.build.version.incremental=GD__-18.03.100.20.11.C2P
      ./system/build.prop:ro.build.version.sdk=22
      ./system/build.prop:ro.build.version.codename=REL
      ./system/build.prop:ro.build.version.all_codenames=REL
      ./system/build.prop:ro.build.version.release=5.1.1
      ./system/build.prop:ro.build.version.security_patch=2016-03-01
      ./system/build.prop:ro.build.version.base_os=
      ./system/build.prop:ro.opengles.version=131072
      shell@pineapple:/ #
    ```

 ### busybox which su 
  显示一个二进制文件或可执行文件的完整路径 
  ```shell
  
  shell@pineapple:/ $   busybox which su
    /system/xbin/su
    shell@pineapple:/ $
  ```
 ### pwd 显示当前文件夹路径全路
  ```shell
    root@generic_x86:/sdcard/testDir # pwd
    /sdcard/testDir
    root@generic_x86:/sdcard/testDir #
  ```


 ### cat file1 
  从第一个字节开始正向查看文件的内容 
  ```shell
    shell@pineapple:/system # ll build.prop
    -rw-r--r-- root     root         3489 2019-07-10 17:23 build.prop
    shell@pineapple:/system # cat build.prop

    # begin build properties
    # autogenerated by buildinfo.sh
    ro.build.id=LMY47V
    ......

  ```
 ### busybox tac file1 
  从最后一行开始反向查看一个文件的内容 
  ```shell
    shell@pineapple:/system # ll build.prop
    -rw-r--r-- root     root         3489 2019-07-10 17:23 build.prop
    shell@pineapple:/system # busybox tac build.prop
    dalvik.vm.stack-trace-file=/data/anr/traces.txt
    net.bt.name=Android
    ......
    ro.build.version.incremental=GD__-18.03.100.20.11.C2P
    ro.build.display.id=aosp_pineapple-userdebug 5.1.1 LMY47V GD__-18.03.100.20.11.C2P test-keys
    ro.build.id=LMY47V
    # autogenerated by buildinfo.sh
    # begin build properties

    shell@pineapple:/system #
  ```
  ### busybox more file1 
   查看一个长文件的内容 
   ```shell
    shell@pineapple:/system # busybox more build.prop

    # begin build properties
    # autogenerated by buildinfo.sh
    ro.build.id=LMY47V
    ro.build.version.incremental=GD__-18.03.100.20.11.C2P
    ro.build.version.sdk=22
    ro.build.version.codename=REL
    ro.build.version.all_codenames=REL
    ......
    ro.build.flavor=aosp_pineapple-userdebug
    ro.product.model=MStar Android TV
    ro.product.brand=MStar
    ro.product.name=aosp_pineapple
    --More-- (21% of 3489 bytes)

   ```

 ### busybox head -2 file1 
  查看一个文件的前两行 
  ```shell
    shell@pineapple:/system # busybox head -2 build.prop

    # begin build properties
    shell@pineapple:/system #
  ```
 ### busybox tail -2 file1 
  查看一个文件的最后两行 
  ```shell
    shell@pineapple:/system # busybox tail -2 build.prop
    net.bt.name=Android
    dalvik.vm.stack-trace-file=/data/anr/traces.txt
    shell@pineapple:/system #
  ```
 ### busybox tail -f /data/anr/traces.txt 
  实时查看被添加到一个文件中的内容 
  ```shell
    shell@pineapple:/ $ busybox tail -f /data/anr/traces.txt
      | sysTid=4182 nice=0 cgrp=default
      | state=S schedstat=( 0 0 0 ) utm=0 stm=0 core=0 HZ=100
      kernel: (couldn't read /proc/self/task/4182/stack)

    "[HY]YCMedia" prio=5 (not attached)
      | sysTid=4183 nice=0 cgrp=default
      | state=S schedstat=( 0 0 0 ) utm=0 stm=0 core=0 HZ=100
      kernel: (couldn't read /proc/self/task/4183/stack)

    ----- end 3932 -----
  ```

 ### echo aaaaa > file
   写入文件内容，覆盖
   ```shell
      shell@pineapple:/sdcard/test $ echo aaaa > testfile
      shell@pineapple:/sdcard/test $ cat testfile
      aaaa
      shell@pineapple:/sdcard/test $
   ```

 ### echo bbbb > file 
  写入文件内容，追加
  ```shell
    shell@pineapple:/sdcard/test $ echo aaaa > testfile
    shell@pineapple:/sdcard/test $ cat testfile
    aaaa
    shell@pineapple:/sdcard/test $ echo bbbb >> testfile
    shell@pineapple:/sdcard/test $ cat testfile
    aaaa
    bbbb
    shell@pineapple:/sdcard/test $
  ```

 ### busybox vi files 
  修改文件内容
  ```shell
    shell@pineapple:/sdcard/test $ busybox vi testfile
    aaaa
    bbbb
    cccc
    ~
    ~
    ~
    ~
    ~
    shell@pineapple:/sdcard/test $ cat testfile
    aaaa
    bbbb
    cccc
    shell@pineapple:/sdcard/test $
  ```


## 网络信息
 ### busybox ifconfig
  ````shell
    shell@pineapple:/ # busybox ifconfig
    eth0      Link encap:Ethernet  HWaddr 00:30:1B:BA:02:DB
              inet addr:192.168.3.43  Bcast:192.168.3.255  Mask:255.255.255.0
              inet6 addr: fe80::230:1bff:feba:2db/64 Scope:Link
              UP BROADCAST RUNNING ALLMULTI MULTICAST  MTU:1500  Metric:1
              RX packets:65386 errors:0 dropped:7 overruns:0 frame:0
              TX packets:30638 errors:0 dropped:0 overruns:0 carrier:0
              collisions:0 txqueuelen:1000
              RX bytes:12742381 (12.1 MiB)  TX bytes:7053946 (6.7 MiB)
              Interrupt:209 Base address:0x4000

    lo        Link encap:Local Loopback
              inet addr:127.0.0.1  Mask:255.0.0.0
              inet6 addr: ::1/128 Scope:Host
              UP LOOPBACK RUNNING  MTU:65536  Metric:1
              RX packets:33 errors:0 dropped:0 overruns:0 frame:0
              TX packets:33 errors:0 dropped:0 overruns:0 carrier:0
              collisions:0 txqueuelen:0
              RX bytes:33303 (32.5 KiB)  TX bytes:33303 (32.5 KiB)

    shell@pineapple:/ #
  ````
 ### ping
  ```shell
    shell@pineapple:/ # ping -c 5 8.8.8.8
    PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
    64 bytes from 8.8.8.8: icmp_seq=2 ttl=51 time=27.8 ms
    64 bytes from 8.8.8.8: icmp_seq=3 ttl=51 time=28.3 ms
    64 bytes from 8.8.8.8: icmp_seq=4 ttl=51 time=27.9 ms
    64 bytes from 8.8.8.8: icmp_seq=5 ttl=51 time=26.8 ms

    --- 8.8.8.8 ping statistics ---
    5 packets transmitted, 4 received, 20% packet loss, time 4004ms
    rtt min/avg/max/mdev = 26.832/27.766/28.399/0.574 ms
    shell@pineapple:/ #
  ```
 ### busybox traceroute ip
  ```shell
    shell@pineapple:/ # busybox traceroute 8.8.8.8
    traceroute to 8.8.8.8 (8.8.8.8), 30 hops max, 38 byte packets
    1  192.168.3.1 (192.168.3.1)  2.652 ms  2.069 ms  2.478 ms
    2  192.168.1.1 (192.168.1.1)  2.649 ms  2.428 ms  2.709 ms
    3  219.140.116.1 (219.140.116.1)  4.015 ms  3.311 ms  8.269 ms
    4  111.175.212.21 (111.175.212.21)  7.947 ms  111.175.212.61 (111.175.212.61)  12.815 ms  111.175.209.205 (111.175.209.205)  8.140 ms
    5  111.175.209.49 (111.175.209.49)  7.436 ms  7.424 ms  111.175.210.225 (111.175.210.225)  8.159 ms
    6  202.97.67.53 (202.97.67.53)  22.661 ms  23.562 ms  25.208 ms
    7  202.97.94.138 (202.97.94.138)  19.972 ms  28.593 ms  202.97.94.134 (202.97.94.134)  23.313 ms
    8  202.97.94.94 (202.97.94.94)  37.283 ms  202.97.94.90 (202.97.94.90)  43.247 ms  38.987 ms
    9  202.97.89.54 (202.97.89.54)  31.696 ms  32.007 ms  31.233 ms
    10  202.97.62.214 (202.97.62.214)  30.404 ms  28.171 ms  27.565 ms
    11  108.170.241.33 (108.170.241.33)  28.638 ms  108.170.241.1 (108.170.241.1)  28.890 ms  108.170.241.97 (108.170.241.97)  29.114 ms
    12  209.85.243.249 (209.85.243.249)  26.962 ms  72.14.239.95 (72.14.239.95)  27.257 ms  72.14.233.169 (72.14.233.169)  24.176 ms
    13  8.8.8.8 (8.8.8.8)  27.501 ms  29.182 ms  26.884 ms
    shell@pineapple:/ #
  ```
 ### tcpdump -i eht0  -w file.cap
   监听网卡的网络包，并保存到文件，之后可以用wireshark等软件分析
  ```shell
    shell@pineapple:/sdcard # tcpdum -i eth0 -w eth0.cap
    sh: tcpdum: not found
    127|shell@pineapple:/sdcard # tcpdump -i eth0 -w eth0.cap
    tcpdump: listening on eth0, link-type EN10MB (Ethernet), capture size 65535 bytes
    ^C375 packets captured
    399 packets received by filter
    0 packets dropped by kernel
    shell@pineapple:/sdcard # ll eth0.cap
    -rw-rw---- root     sdcard_r    54574 2019-08-13 09:40 eth0.cap
    shell@pineapple:/sdcard #
  ```

 ### busybox tftp
  文件传输
  mac建议安装[TFTP Server](http://ww2.unime.it/flr/tftpserver/)
  windows建议安装 [Tftp32](http://tftpd32.jounin.net/tftpd32_download.html)
  上传文件 busybox tftp -pl remoteip
  ```shell
    shell@pineapple:/sdcard/test $ busybox tftp -pl testfile 192.168.3.41
    testfile             100% |*******************************|    15   0:00:00 ETA
    shell@pineapple:/sdcard/test $
  ```
  下载文件
  ```shell
    shell@pineapple:/sdcard/test $ busybox tftp -gr testfileRemote 192.168.3.41
    testfileRemote       100% |*******************************|    15   0:00:00 ETA
    shell@pineapple:/sdcard/test $ ll
    -rw-rw---- root     sdcard_r       15 2019-08-13 09:35 testfile
    -rw-rw---- root     sdcard_r       15 2019-08-13 11:52 testfileRemote
    shell@pineapple:/sdcard/test $
  ```

 ### busybox wget
  下载网络文件
  ```shell
    shell@pineapple:/sdcard $ busybox wget http://192.168.3.5/index.html.en
    Connecting to 192.168.3.5 (192.168.3.5:80)
    index.html.en        100% |*******************************|    45   0:00:00 ETA
    shell@pineapple:/sdcard $ ll index.html.en
    -rw-rw---- root     sdcard_r       45 2019-08-13 10:40 index.html.en
    shell@pineapple:/sdcard $
  ```
 ### busybox md5sum
  查看文件md5值
  ```shell
    shell@pineapple:/sdcard $ busybox md5sum index.html.en
    5388f60d7695cb57b87c799ee62d20b2  index.html.en
    shell@pineapple:/sdcard $
  ```
# 签名
 ### 生成普通签名文件
  ```shell
    Laird-MacBook-Pro:Work laird$ keytool -genkey -alias test -keypass 123456 -keyalg RSA -keysize 2048 -validity 36500 -keystore test.keystore -storepass 123456
    您的名字与姓氏是什么?
      [Unknown]:  laird.li
    您的组织单位名称是什么?
      [Unknown]:  laird.li
    您的组织名称是什么?
      [Unknown]:  lairdli.top
    您所在的城市或区域名称是什么?
      [Unknown]:  wh
    您所在的省/市/自治区名称是什么?
      [Unknown]:  hb
    该单位的双字母国家/地区代码是什么?
      [Unknown]:  ch
    CN=laird.li, OU=laird.li, O=lairdli.top, L=wh, ST=hb, C=ch是否正确?
      [否]:  y

    Warning:
    JKS 密钥库使用专用格式。建议使用 "keytool -importkeystore -srckeystore test.keystore -destkeystore test.keystore -deststoretype pkcs12" 迁移到行业标准格式 PKCS12。
    Laird-MacBook-Pro:Work laird$ ll tes*
    -rw-r--r--  1 laird  staff  2226  8 12 23:51 test.keystore
    Laird-MacBook-Pro:Work laird$
  ```
 ### 查看签名文件信息
  ```shell
  Laird-MacBook-Pro:Work laird$ keytool -list -v -keystore test.keystore -storepass 123456
  密钥库类型: jks
  密钥库提供方: SUN

  您的密钥库包含 1 个条目

  别名: test
  创建日期: 2019-8-12
  条目类型: PrivateKeyEntry
  证书链长度: 1
  证书[1]:
  所有者: CN=laird.li, OU=laird.li, O=lairdli.top, L=wh, ST=hb, C=ch
  发布者: CN=laird.li, OU=laird.li, O=lairdli.top, L=wh, ST=hb, C=ch
  序列号: 457b2631
  有效期为 Mon Aug 12 23:51:21 CST 2019 至 Wed Jul 19 23:51:21 CST 2119
  证书指纹:
    MD5:  DD:9B:06:2B:EE:25:44:22:97:75:99:C0:DC:A6:24:67
    SHA1: 93:C5:28:01:EA:43:2C:5E:21:5B:4B:E6:A8:31:C9:5B:03:CC:20:82
  ......

  Warning:
  JKS 密钥库使用专用格式。建议使用 "keytool -importkeystore -srckeystore test.keystore -destkeystore test.keystore -deststoretype pkcs12" 迁移到行业标准格式 PKCS12。
  Laird-MacBook-Pro:Work laird$
  ```

 ### 查看apk签名信息
  ```shell
    Laird-MacBook-Pro:debug laird$ keytool -list -printcert -jarfile app-debug.apk
    签名者 #1:

    签名:

    所有者: C=US, O=Android, CN=Android Debug
    发布者: C=US, O=Android, CN=Android Debug
    序列号: 1
    有效期为 Mon Mar 18 22:00:17 CST 2019 至 Wed Mar 10 22:00:17 CST 2049
    证书指纹:
      MD5:  91:AB:FF:E4:5B:C4:7B:D1:4F:CC:B9:5D:44:A6:73:DD
      SHA1: CD:30:F3:C9:07:CE:AE:77:71:52:24:3F:65:20:FA:51:7D:85:2E:75
      SHA256: F9:D2:32:1C:00:0C:59:F4:43:20:27:1F:F7:C2:9A:12:F6:0C:C5:02:C4:B6:49:B6:0D:42:85:7B:80:A4:19:4B
    签名算法名称: SHA1withRSA
    主体公共密钥算法: 1024 位 RSA 密钥
    版本: 1

    Laird-MacBook-Pro:debug laird$
  ```

 ### 生成系统签名文件
  Android系统签名证书的目录是“build/target/product/security”
  找到系统的 platform.pk8 和 platform.x509.pem 放在 keytool-importkeypair目录下执行

  ```shell
  Laird-MacBook-Pro:~ laird$ keytool-importkeypair -k platform.keystore -p android -pk8 platform.pk8 -cert platform.x509.pem -alias platform
  ```
  然后在androidstudio 编译脚本引用
  ```shell
    signingConfigs {
      releaseConfig {
          keyAlias 'platform'
          keyPassword 'android'
          storeFile file("${rootDir}"+'/platform.keystore')
          storePassword 'android'
        }
     }
  ```
# web调试
 ### mac下apache服务
   1. 启动或者关闭服务
       ```shell
        Laird-MacBook-Pro:~ laird$ sudo apachectl start
        Password:
        /System/Library/LaunchDaemons/org.apache.httpd.plist: service already loaded
        Laird-MacBook-Pro:~ laird$ sudo apachectl stop
        Laird-MacBook-Pro:~ laird$
       ```
   2. 默认网站目录
       Mac下apache默认的网站路径是/Library/WebServer/Documents
       
       ```shell
        Laird-MacBook-Pro:~ laird$ cd /Library/WebServer/Documents
        Laird-MacBook-Pro:Documents laird$ pwd
        /Library/WebServer/Documents
        Laird-MacBook-Pro:Documents laird$
       ```
 ### windows下web服务
     建议下载轻量级web服务[Abyss Web Serve](https://aprelium.com/)或者[Tomcat](https://tomcat.apache.org/)
# 工具推荐
本文涉及到的工具软件整理如下：
- mac推荐命令行终端-[iterm](https://www.iterm2.com/) 
- windows推荐命令行终端-[cmder](https://cmder.net/)
- adb工具 sdk目录下sdk/platform-tools/adb 或者单独下载-[adbshell](http://adbshell.com/downloads/)
- 平台签名转换工具-[keytool-importkeypair](https://github.com/lairdli/keytool-importkeypair) 
- 网络包分析-[WireShark](https://www.wireshark.org/)
