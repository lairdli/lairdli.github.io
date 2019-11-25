---
title: Android Release
date: 2019-06-24 20:37:13
updated: 2019-06-24 20:37:13
categories: Android
tags: [Android,Adapter]
---
#### Android Release

Android版本目前最新已发布了Android 9.0 Q测试版，本文旨在总结目前Android各个Release版本的新特性，以供App开发时，进行更好的版本适配，新功能开发。

##### MindMap
开局一张图，直接上脑图
![Android Release](https://lairdli.top/images/android-release.png)
<!--more-->

##### Android 9 Pie

>- 显示屏缺口支持
>- 通知-短信通知支持图像
>- 渠道设置、广播和请勿打扰
>- 多摄像头支持和摄像头更新
>- 安全增强功能

##### Android 8.0 Oreo

>- 用户体验-通知渠道等
>- 自动填充框架
>- 画中画模式
>- 动态权限申请，后台广播管理更加严格

##### Android 7.0 Nougat

>- 多窗口支持
>- VR支持
>- 后台省电
>- Unicode9支持 全新的emoji表情符号
>- 支持JAVA8 Lambda

##### Android 6.0 Marshmallow 

>- 运行时检查和请求权限
>- 取消支持 Apache HTTP 客户端
>- WLAN 和网络连接变更

##### Android 5.0 Lollipop 

>- Android Runtime (ART)
>- Material Design 样式
>- 浮动通知
>- NDK支持64位
>- 禁止Intent隐式调用
>- 推出RecyclerView等

##### Android 4.4 KitKat

>- 通过主机卡模拟实现新的 NFC 功能
>- 内存使用率分析工具 adb shell dumpsys procstats /db shell dumpsys meminfo 

#### Android Adapter

各版本适配适配，从Android5.0开始有差异，需要特别注意以下几点

>- Android 5.0 开始禁止Intent隐式调用
>- Android 6.0 开始动态权限管理
>- Android 7.0中删除了三项隐式广播
>- Android 8.0 动态权限申请，后台广播管理更加严格
>- Android 9.0 挖孔屏适配

#### References

>- [《Android进阶之光》](<https://book.douban.com/subject/27080694/>)第一章
>- [Android开发者官网-Android-Developer]()
>- [谈谈Android 6.0 的动态权限管理](<https://blog.csdn.net/qq_17766199/article/details/52013501>)
>- [Android 7.0脱坑指南](<https://blog.csdn.net/qq_17766199/article/details/77404712>)
>- [Android 8.0适配指北](<https://blog.csdn.net/qq_17766199/article/details/80965631>)
>- [Android P 兼容与适配](<https://www.jianshu.com/p/9e9e902ea039>)
>- [推荐一种非常好用的Android屏幕适配](<https://www.jianshu.com/p/1302ad5a4b04>)
>- [Android 6.0-9.0适配](<https://www.jianshu.com/p/251ff4ee94d3>)
>- [Android5.0&6.0新特性](<https://www.jianshu.com/p/f4b3b6a9a5d6?utm_campaign=maleskine&utm_content=note&utm_medium=seo_notes&utm_source=recommendation>)

#### Recommended reading

> - [Android 学习书籍推荐](<https://lairdli.top/2018/05/25/Android-Book-Recomendations/>)
> - [Android 常用第三方库整理](<https://lairdli.top/2019/02/25/Android-3rd-Libs/>)
> - [Android 知识点脑图整理](<https://lairdli.top/2019/01/30/Android-Journey/>)
> - [Android 路线图](<https://lairdli.top/2019/05/19/Android-RoadMap/>)
> - [Android NDK知识脑图整理](<https://lairdli.top/2019/06/01/Android-NDK-RoadMap/>)
> - [Andorid C知识脑图整理](<https://lairdli.top/2019/06/09/Android-C-RoadMap/>)
> - [Android Helper 软件开发工具集](<https://lairdli.top/2019/06/18/Android-Helper/>)


  