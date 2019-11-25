---
title: Android Tv
date: 2019-07-09 22:20:18
updated: 2019-07-09 22:22:18
categories: Tv
tags: [Android,Tv,Tvos]
---

本文总结Android-TV开发过程中，常见的基础知识点，主要分为TV-UI,IPTV,OTT,DVB,TVOS,DEBUG等几大模块展开。适用于常见盒子，电视，投影仪等TV开发。

### MindMap

开局一张图，直接上脑图

![](https://lairdli.top/images/android-tv.png)

<!--more-->

### UI

Android TV 界面开发有别与传统的移动手机端开发，TV端的交互主要是有用户遥控器操作完成，因而在TV上按键和焦点的处理显得尤为重要，其次TV端的输出显示媒介主要是电视显示屏，不同的电视所能支持的输入显示分辨率也不一样，因而分辨率的适配也是TV界面开发需要考虑的一点，除此之外TV界面的设计也与手机上的小屏显示不一样，由于是大屏显示，对UI的设计需更加偏平话，便捷化。

>- 焦点  TV上焦点处理
>- 按键  可以了解下Android View事件分发流程，针对具体的业务进行事件分发，拦截处理
>- 屏幕适配  TV上屏幕适配只需适配常见的720p 1080p 常见的几种分辨率即可。
>- 播放器 TV上播放器一般分为硬件软件，如果定制开发，建议硬解，其他情况可以考虑ijkplayer等
>- UI组件 TV上常见的的控件ListView GridView RecycleView TabLayout ViewPager ScorllView等

### IPTV

IPTV概念的普及，国内主要靠电信，联通，移动，广电四大宽带运营商。IPTV主要特点如下：

>- 基于城域网传输
>- 主要面向电视等大屏终端输出
>- 内容来源主要为牌照商

### OTT

OTT的概率，国内主要靠互联网行业推动，类似小米/乐视电视，盒子，创维，康佳，海信等智能电视。OTT主要特点如下：

>- 基于互联网传送
>- 除了面向电视等终端输出外，还有手机，pad等，即所谓的“多屏互动”。
>- 内容主要来源于牌照商，视频网内容（有版权）+其他

### DVB

DVB的概念，存在时间最早，即传统的广电业务。DVB系统按照信号传播的顺序可以分成前端系统，传输系统和终端系统。其中前端系统一般位于节目生产部门（例如电视台等部门），而终端系统一般用户设备中（例如机顶盒）

#### 传输标准 

区别于传送方式的不同，DVB的通用国际标准又可以分为以下：

>DVB-S,数字卫星电视系统，即通常山区里面的“户户通”小锅。
>
>DVB-T,数字地面电视广播系统,即通常区域电视塔发射出来的信号，国内标准对应为DTMB
>
>DVB-C,数字有线电视系统，即通常通过Cable线传输信号

#### 分层结构

DVB标准中描述的系统根据所属的层次不同从上层到底层可以分为：音视频编码层，服务信息层，基带传输层，信道编码层，射频层。对于Android开发而言，主要涉及的为服务信息层。服务信息层主要分为：

>- PSI 节目引导信息
>- SI 业务信息

#### PSI

PSI信息由节目关联表PAT、条件接收表CAT、节目映射表PMT和网络信息表NIT组成，这些表会被插入到TS流中。 PSI信息是对单一TS流的描述，它是TS流的引导信息；PSI信息指定了如何从一个携带多个节目的传输流中找到指定的节目。 下面给出的是节目引导信息（或称节目特定信息，PSI）的四个表结构

>- PAT节目关联表   将节目号码和节目映射表PID相关联，是获取数据的开始
>- PMT节目映射表  指定一个或多个节目的PID
>- CAT条件接收表 将一个或多个专用EMM流分别与唯一的PID相关联
>- NIT网络信息表  描述整个网络，如多少个TS流、频点和调制方式等信息

#### SI

PSI只提供了单个TS流的信息，使接收机能够对单个TS流中的不同节目进行解码； 但是，它不能提供多个TS流的相关业务，也不能提供节目的类型、节目名称、开始时间、节目简介等信息。 因此，DVB对PSI进行了扩展，提供了其他不同类型的表，形成了SI。

SI定义的表，并不需要全部传输， 其中，SDT、EIT和TDT是必须传输的； 而又以SDT和EIT最为重要，利用这2个表可以构成功能不同的EPG， 如提供节目附加信息、节目分类、节目预定和家长分级控制等。

S 业务I信息表分为以下几类：

>- SDT业务描述表   SDT描述了业务内容及信息，连接了NIT、EIT和PMT（PSI）
>- BAT业务群关联表  BAT将网络中所有的业务分成了多个业务群，以此界定用户。
>- EIT事件信息表  EIT按时间顺序提供每一个业务所包含的事件信息
>- RST运行状态表
>- TDT事件信息表 TDT为时间和日期表（Time&Date Table），它仅传送UTC时间和日期信息。
>- TOT事件偏移表  TOT表提供了UTC时间和日期信息，以及和本地时间的时差
>- ST填充表
>- SIT选择信息表
>- DIT间断信息表

#### SEARCH

DVB的搜台从用户角度来说，一般可以分为自动搜台，全频点搜台，手动搜台。其中手动搜台实质是单频点搜台，自动搜台是检索到ts流里面的频点信息后，还是回到单频点搜台，全频点搜台一般是固定了频率的数组，依次扫描单频点。

机顶盒搜台的实质是从TS流中获取并存储每套节目的音视频PID值和构建出电子节目节目指南。

以下总结三种搜台实现流程：

>①：主频点锁频->NIT获取ServiceList ->获取SDT 
>
>机顶盒软件开发厂商会在机顶盒内设定一个初始频点（MainFrenquency）.或称主频点,机顶盒可以根据这个主频点的物理参数,如频点.符号率,和调制方式,去锁定此频点.如某机顶盒设置506MHZ作为数字节目的承载主频点，获取NIT（Network Information Table），NIT表由以下两个描述：1.Cable Delivery System Descriptor，这个描述主要包含了频点，符号率，调制参数等信息；2.ServiceList Descriptor，这个描述主要包含当前节目信息的描述，通过NIT表获取ServiceList，进而获得SDT（Service Descriptor Table）表，获取SDT.依靠SDT.机顶盒可以知道频道名,频道类型节目开始时间,节目名称,节目长度,节目分类等信息,通过系统的BAT（业务群关联表）过滤节目信息，可以构建出EPG应用的频道列表.将播放节目和业务名称关联起来显示于节目列表中，最后将新的节目信息写入E2PROM之类的非易失存储介质中，开机自动读取这个存储器中的数据。E2PROM之类的非易失存储介质中，开机自动读取这个存储器中的数据。至此机顶盒的节目搜索工作算是完成。
>
>②：主频点锁频->PAT获取->PMT获取
>
>机顶盒找到主频点获取PAT表。PAT(Program Association Table)表是不加密的。PAT是一个传输流所有节目的总入口点.每路TS流都有一个PAT和一个PMT,但是最后合成的TS流中只有一个PAT和与相对应的总的多个PMT(Program Map Table),通过这两个表的信息进而获取搜取的节目信息，并将节目信息写入写入E2PROM之类的非易失存储介质中，开机自动读取这个存储器中的数据。
>
>③：间隔跨频点锁频->获取频点的节目信息。
>
>全频点搜台方式：通过设置的最低频点和最高频点，机顶盒从最低频点，一般系统最低频点为几十MHz，然后每增长8M，依次搜台到最高频点，搜所到这一频点的节目信息，便写入某一特定的存储空间，最后写入E2PROM之类的非易失存储介质中，

#### PLAY

播放主要分为大屏播放以及画中画播放，一直搞不懂为啥还要有画中画这种业务场景的需求。画中画一般需要双demux支持。

dvb的播放流程与传统的播放器调用有所差别，一般需要底层，jni层封装单独的播放器接口调用。

dvb播放需传入频点信息，音视频pid,以及音视频类型等。

### TVOS 

先看下官方简介-NGB TVOS，全称Next Generation Broadcasting Network TVOS，是中华人民共和国国家新闻出版广电总局科技司带头研发的基于Linux和安卓系统的一套应用于网络电视的操作系统。其开发者自称“兼顾现有操作系统的技术，比如Linux、安卓”，并增加信息安全模块，加强用户的信息安全保障，是专门针对电视终端的操作系统。

根据以上描述，结合NGB相关规范，不难看出，TVOS其实还是基于Android系统开发改造，主要是通用规范了中间层接口规范，为硬件软件厂家集成通用接口。

一套完整的TVOS系统，基本集合了DVB+IPTV的业务功能。TVOS应用层面基本覆盖如下几个方面

>- 桌面   一般支持动态配置更新
>- 直播  分为DVB直播（需传统广电Cable线支持），IPTV直播（http或者udp）
>- 回看 目前主要是IPTV回看，走http
>- 时移 目前主要是IPTV时移，走http，也有部分rtsp
>- 点播 目前主要是IPTV回看，走http，也有部分rtsp
>- 多屏互动 主要通过DLNA,AIRLPAY等集成，也有部分通过局域网socket实现或者组播实现
>- 设置  定制化设置，主要包含网络设置，图像设置，系统设置，其他设置等
>- 本地媒体 主要提供外置usb或者sdcard多媒体文件浏览播放，或者apk安装等
>- 应用管理 主要提供本地应用管理以及远程应用推荐，升级等
>- 系统升级 主要提供系统ROM升级，分IP形式升级以及Cable形式升级
>- 消息管理 主要提供前端消息下发，终端消息分发，上报等
>- 广告管理 主要提供前端广告下发，终端广告分发等，包含IP双向广告，以及Cable单向广告
>- 终端管理 主要提供远程运维，远程升级等，一般采用tr069,mqtt,xmpp等协议
>- 数据采集 主要进行用户行为分析，需终端应用埋点集成上报数据，前端进行大数据分析，一般采用mqtt,xmpp等

### DEBUG

TV端的开发调试工作，与手机端也有些差异，TV端调试方式大致如下：

>- AndoroidStudio 调试 ，可以直接debug
>
>- adb命令行，Linux常用命令
>
>- 串口工具，需拆盒子
>
>- Tftp  文件传输
>
>- 系统签名 ，root ,remout等
>
>- stetho ,可在谷歌浏览器远程查看数据库，sp，文件等信息。
>
>- Android-Debug-Database ，浏览器在线插件数据库

### REF

> - [Android Developer TV](https://developer.android.google.cn/tv/)
> - [Android TV开源社区](https://gitee.com/kumei)
> - [Android TV开发探索-知乎专栏](https://zhuanlan.zhihu.com/fuqiang)
> - [DVB数字电视系统简介](https://blog.csdn.net/leixiaohua1020/article/details/43882921)
> - [DVB标准](https://www.dvb.org/standards)
> - [PSI/SI智库](https://www.onelib.biz/blog/stb)

#### 推荐阅读

> - [Android 学习书籍推荐](<https://lairdli.top/2018/05/25/Android-Book-Recomendations/>)
> - [Android 常用第三方库整理](<https://lairdli.top/2019/02/25/Android-3rd-Libs/>)
> - [Android 知识点脑图整理](<https://lairdli.top/2019/01/30/Android-Journey/>)
> - [Android 路线图](<https://lairdli.top/2019/05/19/Android-RoadMap/>)
> - [Android NDK知识脑图整理](<https://lairdli.top/2019/06/01/Android-NDK-RoadMap/>)
> - [Andorid C知识脑图整理](<https://lairdli.top/2019/06/09/Android-C-RoadMap/>)
> - [Android Helper 软件开发工具集](<https://lairdli.top/2019/06/18/Android-Helper/>)
