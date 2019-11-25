---
title: Android NDK RoadMap
date: 2019-06-01 12:00:00
tags: [Android,Jni]
categories: Android 
---

# Android NDK RoadMap

## Let’s become a better Android/NDK Developer

本文使用于

> 1. 任何想要学习JNI-NDK开发但不知道从哪里开始的人。
> 2. 已经学习Android开发，但想学习Android-NDK-JNI相关开发的人

本文的目标是提供适当Android-JNI-NDK RoadMap（路线图)，列出常见需要注意的点，方便知识Review，以使你成为更好的Android/NDK开发人员。本文不会详情的展示如何演示脑图所展示的知识点，展开来谈，一篇的篇幅远远不够，但文章末会列出相关学习资源，给认真学习上进的你。

 *There is no better way to learn something than by doing.*

## **Getting started with the MindMap**

开局一张图，直接上脑图

![jni-c-journey](https://lairdli.top/images/jni-ndk-roadmap.png)

<!--more-->

## First comes  a strong core foundation 

- 简介，下载，配置，集成，编译

  >- JNI可以理解层沟通应用层(java)与底层(c)之间的桥梁，可以相互通信，相互调用。
  >- 下载建议下载r14以前版本，高版本，as可能会编译时找不到对应的arm
  >- AS集成，配置有大体分两种种情况，一种是引用cmake.txt,一种是引用Android.mk,推荐后者，可单独ndk编译，也可放源码类编译，详情参考底部推荐资源
- 异常-调试

  >- 异常的引起大致是由于代码规范不够严谨到账，遇到异常不用慌，理性分析，google一下，你懂的！
  >- ndk的调试推荐Android官网介绍的[ndk-stack](<https://developer.android.google.cn/ndk/guides/ndk-stack?hl=zh_cn>)
  >

- makefile编写

  >makefile 文件实质是一个编译脚本，告诉编译器改索引哪些文件，编译哪些文件，依赖哪些库，编译输出格式等。
  >
  >建议项目分包按 src(源文件)，include(头文件)，libs(依赖库)，(test)(测试)分包设计，方便makefile索引文件
  >
  >具体编写语法参考Android官网介绍的[ndk-Android.mk](<https://developer.android.google.cn/ndk/guides/android_mk>)
  >
  >源文件或者头文件依赖比较多，建议索引文件目录
  ```makefile
  LOCAL_PATH:= $(call my-dir)
  include $(CLEAR_VARS)
  PROJECT_PATH = $(LOCAL_PATH)
  
  LOCAL_MODULE    := libmodule
  LOCAL_LDFLAGS += -shared
  
  #添加模块使用宏定义
  LOCAL_CFLAGS += -DMODULE_FLAG
  
  #添加需要包含的头文件路径，会依次遍历向下所有目录，
  MY_HEADER_PATH += $(PROJECT_PATH)
  
  #添加需要包含的头文件路径，不会向下遍历，最后一个不要加\号
  LOCAL_C_INCLUDES += $(PROJECT_PATH)../include
  
  LOCAL_C_INCLUDES += $(shell find $(MY_HEADER_PATH) -type d)                              
  $(warning "$(LOCAL_MODULE): LOCAL_C_INCLUDES =$(LOCAL_C_INCLUDES)")   
  
  # 扫描目录下的所有源文件，会向下依次遍历
  MY_FILES_PATH  := $(PROJECT_PATH)
  # 添加指定C/CPP文件，只添加某个
  LOCAL_SRC_FILES += $(LOCAL_PATH)/test.c
  
  MY_FILES_SUFFIX := %.cpp %.c %.cc
  My_All_Files := $(foreach src_path,$(MY_FILES_PATH), $(shell find "$(src_path)" -type f) ) 
  My_All_Files := $(My_All_Files:$(MY_CPP_PATH)/./%=$(MY_CPP_PATH)%)
  MY_SRC_LIST  := $(filter $(MY_FILES_SUFFIX),$(My_All_Files)) 
  MY_SRC_LIST  := $(MY_SRC_LIST:$(LOCAL_PATH)/%=%)
  LOCAL_SRC_FILES += $(MY_SRC_LIST)
  $(warning "$(LOCAL_MODULE): LOCAL_SRC_FILES =$(LOCAL_SRC_FILES)")   
  
  #添加需要链接的静态库
  LOCAL_STATIC_LIBRARIES  := 
  
  #添加需要链接的动态库
  LOCAL_SHARED_LIBRARIES  := 
  $(warning "$(LOCAL_MODULE): LOCAL_SHARED_LIBRARIES=$(LOCAL_SHARED_LIBRARIES)") 
  
  #添加需要链接的系统库，如ndk编译，需要链接的log/android等
  LOCAL_LDLIBS    += -llog -landroid -lc
  
  #指定编译目标，这边编译动态库
  include $(BUILD_SHARED_LIBRARY)
  ```

## Learning is endless, take it to the next advance level

- Jni-c-调用java

  >- 大致可以分为c调用java静态方法和类，实例方法和类这四类
  >
  >- 调用流程-大致如下：
  >
  >  环境变量->找到java类->找到静态方法或者变量->设置静态方法或者变量->释放变量
  >
  >  环境变量->找到java类->创建java实例或者变量->设置实例方法或者变量->释放变量
  >

- Jni-动态注册

  >- 动态注册的好处就是可以在c文件实现函数时可以自定义函数名，另外一个好处是 解决c语言不支持函数重载(c++除外)的问题。
  >
  >- 动态注册的大体流程是jni_onload注册本地函数，建立映射表
  >
  ```c++
  /**
  *native method map to java methods
  */
  static JNINativeMethod methods[] = {
  		{"Init", "()I", (void *)Init},
  		{"u java method name", "u java method sigal", u c/c++ method name},
  	};
  
  	/*
   * Register several native methods for one class.
  */
  	static int registerNativeMethods(JNIEnv *env, const char *className,
  									 JNINativeMethod *gMethods, int numMethods)
  	{
  		jclass clazz;
  		LOGI(TAG, "++++++++++%s in", __FUNCTION__);
  
  		clazz = env->FindClass(className);
  		if (clazz == NULL)
  		{
  			LOGE(TAG, "Native registration unable to find class '%s'", className);
  			return JNI_FALSE;
  		}
  
  		if (env->RegisterNatives(clazz, gMethods, numMethods) < 0)
  		{
  			LOGE(TAG, "RegisterNatives failed for '%s'", className);
  			return JNI_FALSE;
  		}
  
  		LOGI(TAG, "++++++++++%s out", __FUNCTION__);
  		return JNI_TRUE;
  	}
  
  	/*
   * Register native methods for all classes we know about.
  *
   * returns JNI_TRUE on success.
  */
  	static int registerNatives(JNIEnv *env)
  	{
  		LOGI(TAG, "++++++++++%s in", __FUNCTION__);
  
  		if (!registerNativeMethods(env, classPathName, methods, sizeof(methods) / sizeof(methods[0])))
  		{
  			LOGE(TAG, "%s err", __FUNCTION__);
  			return JNI_FALSE;
  		}
  
  		LOGI(TAG, "++++++++++%s out", __FUNCTION__);
  		return JNI_TRUE;
  	}
  
  	jint JNI_OnLoad(JavaVM *vm, void *reserved)
  	{
  		JNIEnv *env;
  		g_JavaVM = vm;
  		int result;
  		LOGI(TAG, "++++++++++%s in", __FUNCTION__);
  
  		if (vm->GetEnv((void **)&env, JNI_VERSION_1_4) != JNI_OK)
  		{
  			LOGE(TAG, "Failed to get the environment using GetEnv()");
  			return JNI_FALSE;
  		}
  
  		if (registerNatives(env) != JNI_TRUE)
  		{
  			LOGE(TAG, "ERROR: registerNatives failed");
  			return JNI_FALSE;
  		}
  
  		result = JNI_VERSION_1_4;
  		LOGI(TAG, "++++++++++%s out", __FUNCTION__);
  		return result;
  	}
  ```
- jni-线程处理

  >线程处理大致是线程加锁操作，特别注意注意锁申请，释放，加锁，解锁对称调用，以免出现内存泄漏，或者程序死锁，异常
  >

## Online Study Source

>- [Android-developers-ndk](<https://developer.android.google.cn/ndk/guides?hl=zh_cn>)
>- [Android-ndk-download](<https://developer.android.google.cn/ndk/downloads/index.html>)
>- [Android-JNI入门-菜鸟教程](<https://www.runoob.com/w3cnote/jni-getting-started-tutorials.html>)
>- [Android-JNI入门-慕课网](<http://www.imooc.com/learn/411>)
>- [Android-JNI进阶](<http://www.imooc.com/learn/918>)
>- [Android-JNI-pThreads](<https://www.cnblogs.com/dongsheng/p/4184153.html>)
>

## Recommended reading

>- [Android 学习书籍推荐](<https://lairdli.top/2018/05/25/Android-Book-Recomendations/>)
>- [Android 常用第三方库整理](<https://lairdli.top/2019/02/25/Android-3rd-Libs/>)
>- [Android 知识点脑图整理](<https://lairdli.top/2019/01/30/Android-Journey/>)
>- [Android RoadMap](<https://lairdli.top/2019/05/19/Android-RoadMap/>)


