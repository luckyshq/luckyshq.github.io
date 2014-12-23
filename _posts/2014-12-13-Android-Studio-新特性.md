---
layout: post
title:  Android Studio 1.0 新特性
date:   2014-12-13 11:14
categories: android
---

本文部分引用自: [*Android Developers Blog](http://android-developers.blogspot.com/2014/12/android-studio-10.html)

11月8日,对我们Android开发者来说算是一个大日子. 因为, 从13年五月Google放出0.1.x版本后, 整整经历了近一年半, Android Studio终于发布1.0版本了! 相对于之前一直在使用的0.8.x版本, 正式版除了增强软件健壮性之外, 还多了许多十分易用的新功能.

废话不多说, 让我们来看看1.0里面又有哪些新玩具吧~ >,<

(这里仅介绍几个关键新特性,想要看Android Studio的full feature, [*请点这里](http://developer.android.com/tools/studio/index.html))

---

## 一大波新特性在逼近

### 更好的启动体验

Android Studio在1.0版本中使用了全新的主题与图标,理所当然采用了更Material Design风格的样式.显得更加小清新.

* **初次启动引导** -- 现在在新版本的启动中,不仅仅会帮你进行开发环境的设置,同时还会 **安装合适的Android SDK 和 创建最优化的测试模拟器**(这个能不能拼过Genymotion,还没有亲身体验过=,=.大家可以自己尝试下).

![](http://2.bp.blogspot.com/-3dthvcHHOlo/VIKNNX0wLWI/AAAAAAAABD0/VX0vlOmkpL8/s800/first%2Brun%2Bwizard.png)

* **实例和模板导入** -- 新版本的Android Studio提供了更多的模板供开发者在初次创建工程时使用.同时支持直接导入Google官方的代码样例.

![](http://2.bp.blogspot.com/-2pfCClH_Vi0/VIKNNErRV3I/AAAAAAAABDs/8BQT1lQPUIM/s800/Sample%2BWizard.png)

---

### 更便捷的编辑工具

* **代码编辑** -- Android Studio继承了IntelliJ IDEA所有智能编码的优点.例如高级自动补全, 智能重构, 代码分析等.(相信用过之前版本的猿们都应该对这些印象很深)

![](http://2.bp.blogspot.com/-DHQYEdfFSE0/VIKNORx1X5I/AAAAAAAABEM/r7afXHZLbxs/s800/shadow_studio-hero-code_2x.png)

* **多国语言编辑器** -- 在一个窗口下管理字符串的翻译.(Android Studio1.0新出的一个超赞功能,不用像以前那样复制来复制去了TAT)

> 不过由于现在还是Preview版本,所以有点坑.它只能识别`strings.xml`这一个文件,如果你string是按文件分的话(类似strings_history.xml等)它就不能启动编辑器了TAT.跪求快点出正式版.

![](http://4.bp.blogspot.com/-ok0a_1dW9PY/VIKNOmy8-TI/AAAAAAAABEU/LTSy6ih6VY4/s800/translations.png)

* **UI设计工具** -- 通过即时渲染,让开发者能更便捷地在不同屏幕大小,语言环境,API版本中编辑并预览布局.(这一直是Android Studio的招牌技能>.<)

![](http://4.bp.blogspot.com/-DW220tDpMcM/VIKNNGEuDNI/AAAAAAAABD4/Afto70CzVOk/s800/Multi-Screen%2BPreview.png)

### 更直观的程序执行分析工具

* **内存占用监视器** -- 图形化实时观察app的内存占用信息, 帮助猿们直观地找到app需要进行优化的部分.(又一高能新特性, 这样又不用用各种log或者测试平台来看内存和性能消耗了TAT)

![](http://3.bp.blogspot.com/-rd40vumDg_Y/VIKNOMQHqqI/AAAAAAAABEE/8yXCDDEIsTk/s800/monitor.png)

### 直接对接Google云服务

* 新版的Android Studio通过一种简单易用的方式,能将Google云服务加入到app中.(不过这功能在国内估计会有点呵呵...)

![](http://1.bp.blogspot.com/-3J2n6iqIOPU/VIKNNGVCIpI/AAAAAAAABDw/MU9a0yr4cVc/s800/cloud%2Bbackend.png)
