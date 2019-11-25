---
title: Android C Journey
date: 2019-06-09 12:00:00
tags: [Android,C]
categories: C 
---

# Android C RoadMap

对于Android应用开发者而言，想必在大学C语言都是必修课，现在面对C估计熟悉又陌生，但掌握基础的C语言开发对于Android开发还是会锦上添花的，不管是源码的阅读，驱动开发，jni开发，都绕不开C.趁着前段时间开始JNI开发的经历，大概梳理了下C语言开发基础的脑图点，和重要的知识点。  

## Let’s become a better Android/C Developer

本文适用于

> 1. 任何想要学习C开发但不知道从哪里开始的人。
> 2. 已经学习Android/C开发，但想学习Android底层相关开发的人

本文的目标是提供适当C/C++ RoadMap（路线图)，方便知识Review，以使你成为更好的Android/C开发人员。

 *There is no better way to learn something than by doing.*

## **Getting started with the MindMap**

开局一张图，直接上脑图

![jni-c-journey](<https://lairdli.top/images/jni-c-journey.png>)

<!--more-->

## First comes  a strong core foundation 

>- 基础类型 ->常见类型的分类，有符号，无符号，占用字节数等。
>- 数组 -> 一位数组，二维数组
>- 结构体 ->实质就是一个变量仓储，留意初始化，成员变量访问等
>- 函数 ->尽量精简，避免代码冗余
>- 运算符 -> 加减乘除，三目操作，位运算等
>- 枚举 -> 枚举定义，访问等
>- 预编译/重定义  ->#define/typedef 前者是预编译，后者是运算时加载，相当于昵称别名

## Learning is endless, take it to the next advance level

>- 指针  ->  实质是内存地址索引，注意避免空指针，野指针
>- 链表  -> 实质是指针的串行，注意指针的指向
>- 线程管理 ->常用phread库，注意线程锁申请/释放，加锁/解锁 成对出现
>- 内存管理 -> 实际开发中养成良好的开发习惯，注意指针变量声明初始化，macloc,memset等

## Online Study Source

### Beginner Resource

> - [笨方法学C](https://www.gitbook.com/book/wizardforcel/lcthw/details)
> - [C 语言资源大全中文版](<https://github.com/jobbole/awesome-c-cn>)
> - [菜鸟教程——C 语言教程](https://link.zhihu.com/?target=http%3A//www.runoob.com/cprogramming/c-tutorial.html)
> - [实验楼——C语言入门教程 ](https://link.zhihu.com/?target=https%3A//www.shiyanlou.com/courses/57)
> - [慕课网——C语言入门 ](https://link.zhihu.com/?target=http%3A//www.imooc.com/learn/249)
> - [网易云课堂——C语言基础入门 ](https://link.zhihu.com/?target=http%3A//study.163.com/course/introduction/1003030021.htm%23/courseDetail)

### Other Resource

>- [C 语言中的指针和内存泄漏](https://link.zhihu.com/?target=http%3A//www.ibm.com/developerworks/cn/aix/library/au-toughgame/)
>- [如何写出优美的 C 代码](https://link.zhihu.com/?target=http%3A//www.ibm.com/developerworks/cn/linux/l-cn-cobject/index.html)
>- [C语言的整型溢出问题 | 酷 壳 - CoolShell.cn](https://link.zhihu.com/?target=http%3A//coolshell.cn/articles/11466.html)
>- [易被遗忘的C/C++要点总结](https://link.zhihu.com/?target=http%3A//www.jianshu.com/p/14e8c549600c)
>- [C/C++的mem函数和strcpy函数的区别和应用](https://link.zhihu.com/?target=http%3A//zcheng.ren/2016/08/15/memcpySeries/%3Fqqdrsign%3D005a4)
>- [C语言的变量作用域及头文件](https://link.zhihu.com/?target=http%3A//blog.csdn.net/ts_54eagle/article/details/4418627)
>- [C语言中线程管理](<https://www.cnblogs.com/dongsheng/p/4184153.html>)
>- [10个经典的C语言面试基础算法及代码](https://link.zhihu.com/?target=http%3A//www.codeceo.com/article/10-c-interview-algorithm.html)
>

## Recommended reading

>- [Android 学习书籍推荐](<https://lairdli.top/2018/05/25/Android-Book-Recomendations/>)
>- [Android 常用第三方库整理](<https://lairdli.top/2019/02/25/Android-3rd-Libs/>)
>- [Android 知识点脑图整理](<https://lairdli.top/2019/01/30/Android-Journey/>)
>- [Android 路线图](<https://lairdli.top/2019/05/19/Android-RoadMap/>)
>- [Android NDK知识脑图整理](<https://lairdli.top/2019/06/01/Android-NDK-RoadMap/>)
