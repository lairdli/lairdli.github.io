---
title: Android Material Design
date: 2019-06-29 20:26:08
updated: 2019-06-29 20:26:08
categories: Android
tags: [Android,Design]
---

## Android Material Design

Material Design（质感设计）是google在Android 5.0提出的一种全新的设计理论，旨在为手机，平板，TV，电脑 等平台提供一致的设计与体验。

### 导图

开局一张图，直接上脑图

![android-material-design](https://lairdli.top/images/android-material-design.png)

<!--more-->

### 概述

#### 设计思想

Material Design的设计思想是为了保持跨平台设计的一致性，将物理世界的体验带入屏幕，去掉物理世界的杂质，再加上虚拟世界的灵活特效，带给用户最接近现实的体验。

#### 材质与空间

魔法纸片是Material Design的重要信息载体，引入z轴概率，z坐标值越大，投影越重。

#### 动画

响应式交互，转场动画，细节动画等

#### 样式

色彩，字体，字体排版等约定

#### 图标

桌面图标，小图标等

#### 图像

图像布局，图片色彩设计等

### 控件

#### ToolBar

可代替ActionBar，具备Material效果，应用三部曲

- 更改application主题，改为非ActionBar主题
- 布局文件layout，引入v7包Toolbar,作为根布局
- 代码文件，findviewbyid->setSupportActionBar
#### TabLayout

Desin Support库中提供，可实现动态滑动标题栏效果，需配合其他组件使用

- 布局文件layout 引入AppBarLayout,AppBarLayout包裹ToolBar ,TabLayout，ViewPager

- 代码文件设置 

  ```
  toolbar.setSupportActionBar(...)；
  tabLayout.addTab(...);
  viewPager.setAdapter(...);
  tabLayout.setupWithViewPager(...);
  tabLayout.setTabsFromPagerAdapter(...);
  ```

#### 滑动菜单

##### DrawerLayout

v4包中提供，可配合toolbar添加导航呼出，应用步骤

- 布局文件layout,引入v4-DrawerLayout作为根布局，子布局放入两个控件，，一个是主屏幕中显示内容，一个是滑动菜单显示的内容。第一个控件可引入toolbar，特别注意第二个控件的layout_gravity属性必须制定，一般为start

- 代码文件，获取actionBar，设置导航

- 代码文件，响应导航onOptionsItemSelected,触发左侧滑动控件显示drawerLayout.openDrawer(GravityCompat.START)

##### NavigationView

Desin Support库中提供的滑动页面控件，配合DrawerLayout使用。使用步骤如下：

- 基本步骤同DrawerLayout使用
- 布局文件第二个控件滑动控件使用NavigationView。
- 准备NavigationView的app:menu布局文件,可使用子菜单
- 准备NavigationView的app:headerlayout布局文件
- 代码文件，findviewbyid找到NavigationView，设置默认checked，navView.setCheckedItem(..)设置item选中监听，navView.setNavigationItemSelectedListener(..)
#### 悬浮按钮和交互提示

##### FloatActionButton 

Desin Support库中提供，悬浮按钮使用步骤：

- 布局文件layout中引入FloatActionButton控件

- 代码文件，findviewbyid找到FloatActionButton，设置监听事件fab.setOnclickListener(...)

##### SnackBar

类似Toast的提示，不过带了交互功能，调用方式也和Toast类似：
```java
Snackbar.make(view,“Data deleted”,Snackbar.LENGTH_SHORT)
  .setAction("Undo",new View.OnClickListener(){
    @override
    public void onClick(View v){
      Toast.makeText(context,"Data restored",Toast.LENGTH_SHORT)
        .show();
    }
  })
  .show();
```

##### CoordinatorLayout

Desin Support库中提供，加强版FrameLayout,CoordinatorLayout可以监听其所有子控件各种事件，自动做出合并的响应，比如FloatActionButton+SnackBar的操作场景-如果SnackBar的弹出覆盖了FloatActionButton，如何换成CoordinatorLayout，FloatActionButton会自动向上偏移。

CoordinatorLayout中最经典的设计就是Behavior,我们也可以自定义Behavior实现组件的交互与滑动。

自定义Behavior需继承CoordinatorLayout.Behavior<View>,分两种情况：

- 自定义View监听CoordinatorLayout里面的滑动状态，注意onStartNestedScroll()和onNestedPreScoll()
- 自定义View监听其他View的变化，如大小，位置，显示状态等。注意layoutDependsOn()(),onDependentViewChanged().

##### TextInputLayout

Desin Support库中提供，TextInputLayout是一个容器，跟ScrollView一样，只接受一个子元素，并且这个子元素为EditText,使用步骤：

- 布局文件layout 引入TextInputLayout包裹EditText

- 设置EditText的hit属性，就会看到不一样的输入提示

- 代码文件，findviewbyid找到TextInputLayout，还可以设置错误提示

  ```java
  tl.setErrorEnable(true);
  tl.setError("error message tips!");
  ```
  
- 样式文件，改变主题的colorAccent，可改变hit提示颜色

##### BottomSheetBehavior

Android Support 库23.2中引入，可轻松实现底部动作条功能，步骤：

- 布局中加入app:layout_behavior属性

- 将布局作为CoordinatorLayout子布局

- 代码设置回调监听 

  ```java
  behavior = ottomSheetBehavior.from(bottomview) ;
  behavior.setBottomSheetCallBack(...)
  ```

#### 卡片式布局

##### CardView 

v7包提供，实际上CardView也是一个FrameLayout,只是额外添加了圆角，阴影等效果，使用步骤同FrameLayout一样，只需在布局文件layout中引入CardView，设置圆角，阴影等属性配置即可。

##### AppBarLayout

Desin Support库中提供,AppBarLayout实质是一个垂直方向的LinearLayout,在内部做了些滚动的封装，并应用了Material Design的设计理念。

可解决RecyclerView + Toolbar+CoordinatorLayout经典场景中的遮挡问题，解决步骤：

- 布局文件layout中将Toolbar嵌套到AppbarLayout中
- 给RecyclerView设置一个布局行为app:layout_behavior="..."

#### 下拉刷新

##### SwipeRefreshLayout

v4包提供，SwipeRefreshLayout是用于实现下拉刷新的核心库。使用步骤：

- 布局文件layout 中引入SwipeRefreshLayout包裹RecyclerView

- 代码文件设置刷新逻辑swipeRefresh.setOnRefreshListener(...)

#### 可折叠式标题栏

##### CollapsingToolbarLayout

Desin Support库提供，CollapsingToolbarLayout是一个作用于其他组件上的控件，需配合其他组件使用。使用步骤：

- 布局文件layout ,CoordinatorLayout包裹AppBarLayout,AppBarLayout包裹CollapsingToolbarLayout。

- CollapsingToolbarLayout包裹ToolBar+其他子控件（图片等）

- CoordinatorLayout包裹NestedScollView(v4包提供，可嵌套响应滚动)，NestedScollView包裹LinearLayout,

  LinearLayout可包裹显示长文字的CardView-TextView.或者CoordinatorLayout包裹RecyclerView。

#### 沉浸式标题栏

-	实现背景图和系统标题栏融合，需借助android:fitsSystemWindows这个属性：
- 控件设置android:fitsSystemWindows属性为true
- 主题中的android:statusBarColor设置为透明。由于android:statusBarColor是从5.0系统才有，需进行系统差异化处理。建立values-v21主题配置。

### 参考

- [《Android进阶之光》](<https://book.douban.com/subject/27080694/>)第2章
- [《第一行代码-第二版》](https://book.douban.com/subject/26915433/)第12章
- [Android Developers Design](https://developer.android.google.cn/design/)
- [Android沉浸式(透明)状态栏适配](https://www.jianshu.com/p/a44c119d6ef7)
- [Android状态栏微技巧](https://blog.csdn.net/guolin_blog/article/details/51763825)

### 推荐阅读

- [Android 学习书籍推荐](<https://lairdli.top/2018/05/25/Android-Book-Recomendations/>)
- [Android 常用第三方库整理](<https://lairdli.top/2019/02/25/Android-3rd-Libs/>)
- [Android 知识点脑图整理](<https://lairdli.top/2019/01/30/Android-Journey/>)
- [Android 路线图](<https://lairdli.top/2019/05/19/Android-RoadMap/>)
- [Android NDK知识脑图整理](<https://lairdli.top/2019/06/01/Android-NDK-RoadMap/>)
- [Andorid C知识脑图整理](<https://lairdli.top/2019/06/09/Android-C-RoadMap/>)
- [Android Helper 软件开发工具集](<https://lairdli.top/2019/06/18/Android-Helper/>)












