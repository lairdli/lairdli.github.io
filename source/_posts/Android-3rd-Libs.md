---
title: Android 3rd Libs
date: 2019-02-25 10:00:00
tags: [Android,Libs]
categories: Android
---

总结个人Android开发过程中常用的（经典的）第三方库。

方便技术选型，记忆回顾。持续 更新中......

##  Mind Mapping

对应如下思维导图所描述，第三方库按功能分，大致可以分为如下几类：

> - **UI**
> - **WebView**
> - **网络请求-Net Requst**
> - **数据解析-Data Parse**
> - **数据库    -DataBase**
> - **图片加载-Image Load**
> - **缓存框架-Cache**
> - **依赖注册-Dependency Injection**
> - **响应式  -Reactive**
> - **事件总线-Event Bus**
> - **权限适配-Permissions**
> - **架构组件--Componentization** 

![android-3rd-libs](/images/android-3rd-libs.png)

<!--more-->

[点我看大图](https://lairdli.top/images/android-3rd-libs.png)

## UI

>- [CircleImageView] (https://github.com/hdodenhof/CircleImageView) 提供Android圆角图片库
>- [PhotoView](https://github.com/chrisbanes/PhotoView) 通过各种触摸手势实现支持缩放的Android Image View
>
>- [Fragmentation](https://github.com/YoKeyword/Fragmentation) 一个功能强大的库用于管理Android-Fragment！
>- [MaterialDrawer](https://github.com/mikepenz/MaterialDrawer) 适用于Android项目的灵活，易用，一体化抽屉库
>- [material-dialogs](https://github.com/afollestad/material-dialogs) 适用于Kotlin和Android的漂亮流畅的对话框API
>- [BaseRecyclerViewAdapterHelper](https://github.com/CymChad/BaseRecyclerViewAdapterHelper) 功能强大且灵活的RecyclerAdapter
>
>- [FastAdapter](https://github.com/mikepenz/FastAdapter) 快速且易用的适配器库
>
>- [zxing](https://github.com/zxing/zxing) ZXing（“Zebra Crossing”）用于Java，Android的条形码扫描库
>- [Lottie](https://github.com/airbnb/lottie-android) 在Android和iOS，Web和React Native上渲染After Effects动画库

## WebView

> - [AgentWeb](https://github.com/Justson/AgentWeb) AgentWeb是一个基于Android WebView的强大库
> - [Crosswalk](https://crosswalk-project.org/index_zh.html) 采用了 `Chromenium` 内核，是一款开源的 `web` 引擎
>
> - [X5](https://x5.tencent.com/) X5内核是腾讯基于优秀开源Webkit [1]  深度优化的浏览器渲染引擎
>
> - [AndroidChromium](https://github.com/JackyAndroid/AndroidChromium)  google开源的Android版本的Chormium浏览器源码

## Net Requst

>- [Volley](https://github.com/google/volley)  google开源HTTP库，它使Android应用程序的网络更容易，最重要的是，更快
>- [AndroidAsync](https://github.com/koush/AndroidAsync) 一个底层网络协议库，更多解锁功能可以结合[Ion](https://github.com/koush/ion) 使用。
>- [OkHttp](https://github.com/square/okhttp) square出品，适用于Android和Java应用程序的HTTP + HTTP / 2客户端。
>- [Retrofit](https://github.com/square/retrofit) square出品，适用于Android和Java的类型安全的HTTP客户端。
>- [paho.mqtt.android](https://github.com/eclipse/paho.mqtt.android)  适用于MQTT 
>- [ksoap2-android](https://github.com/karlmdavis/ksoap2-android) 适用于Android平台的轻量级高效SOAP库。
>- [nanohttpd](https://github.com/NanoHttpd/nanohttpd)  适用于Android-Java中的小巧，易于嵌入的HTTP服务器
>
>除以上开源第三方库外，Android还自带以下网络请求模块
>
>- HttpUrlConnection 适用于Android 2.3及以上版本，api简单，易扩展升级
>- HttpClient 可兼容Android 2.3一下版本，api数量多，不易扩展
>- AsyncTask Android封装好的轻量级异步类，使用时需实现子类

## Data Parse

>- [Gson/Json](https://github.com/google/gson) google出品，一个Java序列化/反序列化库，用于将Java对象转换为JSON并返回
>
>- [JackSon/Json ](https://github.com/FasterXML/jackson) 用于处理JSON和XML格式化的类库
>
>- [FastJson/Json](https://github.com/alibaba/fastjson) alibaba出品，用于Java的快速JSON解析器/生成器
>
>- [Jsoup/Html](https://github.com/jhy/jsoup) 用于Java解析HTML
>
>- [dom4j](https://github.com/dom4j/dom4j) 用于Xml解析
>
>除此之外，Android还自带XMl解析，主要分三类
>
>- SAX(Simple API for XML)
>- DOM
>- POll ([XmlPull](http://xmlpull.org/))

## DataBase

>- [LitePal](https://github.com/LitePalFramework/LitePal)  郭林大神开源的一款基于ORM模式的SQLite数据库框架
>
>- [GreenDao](https://github.com/greenrobot/greenDAO) 一款轻松快速的Android ORM解决方案，可将对象映射到SQLite数据库
>
>- [Object-Box](https://github.com/objectbox/objectbox-java)ObjectBox是一个用于对象的超快速轻量级数据库
>
>- [SQLBrite](https://github.com/square/sqlbrite) 对 Android 系统的`SQLiteOpenHelper`和 `ContentResolver` 的轻量级封装,配合Rxjava使用
>
>- [Realm](https://github.com/realm/realm-java) 是一个移动数据库：SQLite和ORM的替代品
>
>  除此之外，[Android Jetpack](https://developer.android.google.cn/jetpack)架构组件中自带的[Room](https://developer.android.google.cn/topic/libraries/architecture/room)组件，也是基于ORM的SQlite数据库框架

## Image Load

>- [Android-Universal-Image-Loader](https://github.com/nostra13/Android-Universal-Image-Loader)老牌图片加载，显示，缓存库
>- [Glide](https://github.com/bumptech/glide) google推荐的图片加载，显示，缓存库
>- [Picasso](https://github.com/square/picasso) 适用于Android的强大图像下载和缓存库
>- [Fresco](https://github.com/facebook/fresco) facebook出品，用于管理图像及其使用内存的Android库

## Cache

>- [DiskLruCache](https://github.com/JakeWharton/DiskLruCache)基于磁盘的LRU缓存的Java实现，专门针对Android兼容性

## Dependency Injection

>- [ButterKnife](https://github.com/JakeWharton/butterknife) 将Android视图和回调绑定到字段和方法,省去findviewbyid
>- [Dagger](https://github.com/square/dagger) 适用于Android和Java的快速依赖注入器,Ioc,依赖解耦，控制反转，建议MVP架构搭配适用 

## Reactive 

>- [RxJava](https://github.com/ReactiveX/RxJava) JVM的Reactive Extensions - 一个使用Java VM的可观察序列组成异步和基于事件的程序的库
>- [RxAndroid 
>- ](https://github.com/ReactiveX/RxAndroid)适用于Android的RxJava绑定
>- [RxBinding](https://github.com/JakeWharton/RxBinding) 用于Android UI小部件的RxJava绑定API。
>- [Agera](https://github.com/google/agera) Android的反应式编程，Agera是一组类和接口，用于帮助编写Android的功能，异步和响应式应用程序

## Event Bus

>- [EventBus ](https://github.com/greenrobot/EventBus) 适用于Android和Java的事件总线，可简化活动，碎片，线程，服务等之间的通信。减少代码，提高质量。
>- [Otto](https://github.com/square/otto) 基于Guava的事件总线的Android支持库，组件化通讯，减低耦合性

## Permissions

>- [PermissionsDispatcher](https://github.com/permissions-dispatcher/PermissionsDispatcher) 基于简单注释的API，用于处理Android运行时权限
>- [RxPermissions](https://github.com/tbruyelle/RxPermissions) 能配合RxJava与新的Android M权限模型一起使用，用于处理Android运行时权限
>
>- [SettingsCompat](https://github.com/czy1121/settingscompat) 特殊权限(Special Permissions)兼容库，悬浮窗权限(SYSTEM_ALERT_WINDOW)与系统设置修改权限(WRITE_SETTINGS)

## Componentization 

>- [ARouter](https://github.com/alibaba/ARouter)  alibaba出品，帮助 Android App 进行组件化改造的路由框架
>- [WMRouter](https://github.com/meituan/WMRouter) 美团出品，是一款Android路由框架，基于组件化的设计思路，有功能灵活、使用简单的特点

## Utlis

>- [Logger](https://github.com/orhanobut/logger) 一款简易，精致，功能强大的Android日志库
>- [timber](https://github.com/JakeWharton/timber) 一款小型可扩展API的日志类，可在Android的普通Log类之上提供实用程序，易集成扩展
>
>- [AboutLibraries](https://github.com/mikepenz/AboutLibraries) 显示第三方库信息的库，一般在开源项目类引用。

## End

其他扩展可参考

> - [Android 开源项目及库汇总](https://www.jianshu.com/p/383468f58fe1)
> - [Awesome-Third-Library-Source-Analysis](https://github.com/JsonChao/Awesome-Third-Library-Source-Analysis)
> - [Android Store](https://mindorks.com/android/store)

优秀的开源库数不胜数，以上总结Android常用框架，不要求全部掌握，但至少保证如下几点：

> 1. 不必重复造梯子，善用[google](https://www.google.com.hk/)，[github](/github.com)等，以便技术选型。
> 2. 对照着官网,能会使用，跟进实际项目需求能对比选择合适3RD-Lib。
> 3. 经典的，使用频率比较高的开源框架，需理解其设计思想。

好记性不如烂笔头，所用即所知，所思即所得。

共勉学习之。
