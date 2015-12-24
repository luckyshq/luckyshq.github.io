---
layout: post
title:  application 标签属性
date:   2015-12-22 14:05
categories: android
---

本文翻译自: [*developers.android.com](http://developer.android.com/guide/topics/manifest/application-element.html#hwaccel)

AndroidManifest中关于Application的标签属性多种多样，是否所有的你都了解呢？让我们一起来看看这些属性都代表了些什么。

## 语法
{% highlight xml%}
  <application android:allowTaskReparenting=["true" | "false"]
             android:allowBackup=["true" | "false"]
             android:backupAgent="string"
             android:banner="drawable resource"
             android:debuggable=["true" | "false"]
             android:description="string resource"
             android:enabled=["true" | "false"]
             android:hasCode=["true" | "false"]
             android:hardwareAccelerated=["true" | "false"]
             android:icon="drawable resource"
             android:isGame=["true" | "false"]
             android:killAfterRestore=["true" | "false"]
             android:largeHeap=["true" | "false"]
             android:label="string resource"
             android:logo="drawable resource"
             android:manageSpaceActivity="string"
             android:name="string"
             android:permission="string"
             android:persistent=["true" | "false"]
             android:process="string"
             android:restoreAnyVersion=["true" | "false"]
             android:requiredAccountType="string"
             android:restrictedAccountType="string"
             android:supportsRtl=["true" | "false"]
             android:taskAffinity="string"
             android:testOnly=["true" | "false"]
             android:theme="resource or theme"
             android:uiOptions=["none" | "splitActionBarWhenNarrow"]
             android:usesCleartextTraffic=["true" | "false"]
             android:vmSafeMode=["true" | "false"] >
    . . .
    </application>
{% endhighlight %}

## 父节点
* `<manifest>`

## 子节点

* `<activity>`
* `<activity-alias>`
* `<meta-data>`
* `<service>`
* `<receiver>`
* `<provider>`
* `<uses-library>`

## 描述

`<application>`的子节点描述了应用所包含的组件，它的属性会影响到它所有的子节点组件。**icon/lable/permission** 等 属性是给子节点组件设置一个默认值，可以被复写。而 **debuggable/enabled** 等 属性是作为整个application的全局属性，不能被复写。

## 属性

### android:allowTaskReparenting

作用对象为该Application里定义的所有Activity。`表示Activity在其他应用的Task被启动后，如果再启动Activity原生应用，是否能将该Activity从被启动的Task直接移动到Activity原生应用的Task里。`

Activity也有该属性，可以覆盖掉Application设置的属性值。

    e.g.,在A应用中打开了浏览器的Activity。
    true：则再打开浏览器应用时就会发现被打开的是刚才打开过的Activity；
    false：(默认)则再打开浏览器应用时就会重新打开一个新的Activity。

### android:allowBackup

`表示是否允许该Application被工具备份或者恢复。`

    true：(默认)允许应用被备份或恢复。
    false：不允许备份和恢复，就算是通过adb的全系统备份也不会备份该引用。

### android:backupAgent

`实现了当前Application备份代理（BackupAgent）的类名。`

    该值需要被完整定义。
    e.g.,”com.example.project.MyBackupAgent”
    或可以直接以点开始定义已有包名后面的部分。
    e.g.,”.MyBackupAgent"

该属性没有默认值，如需要的话必须自行指定属性值。

### android:banner

`Drawable资源，为相关联的元素提供一个图片横幅。`

    在<application>中表示为整个应用提供一个默认的横幅
    在<activity>中表示为该特定的activity提供横幅

该属性没有默认值。系统只在Android TV主屏用横幅来表示应用。由于横幅只会在Android TV的主屏显示，它应该只被指定为能处理 **CATEGORY_LEANBACK_LAUNCHER** intent的Activity。

### android:debuggable

`决定该应用是否能被调试。`

    true: 可以被调试
    false: (默认)不可以被调试

### android:description

`相比与label而言，对该应用更具描述性的用户可读文本。`

该属性没有默认值。必须为字串资源的引用，而不能像label一样可以直接使用字串。

### android:enabled

`定义Android系统是否能实例化该应用组件。`

    true: (默认)Application的每个子组件都适用于自己设置的enabled属性。
    false: 覆盖所有子组件设定的enabled属性，所有都为false。

### android:hasCode

`定义这个应用是否有任何代码。`

    true: (默认)有代码。
    false: 在启动时，系统不会去读取任何application代码。

如果一个application只是用内置的组件类，它自身就不应该有任何代码。（例如一个使用AliasActivity的Activity，比较罕见）

### android:hardwareAccelerated

`定义在该应用中，所有的Activity和View是否能使用硬件加速渲染。`

    true: (minSdkVersion或targetSdkVersion大于等于14时为默认)
    false: (minSdkVersion或targetSdkVersion小于14是为默认)

从 **Android 3.0(API level 11)** 开始，为了提升许多通用2D图片操作，应用可以使用硬件加速的 **OpenGL** 渲染。一旦硬件加速渲染被启用，大多数在`Canvas/Paint/Xfermode/ColorFilter/Shader/Camera`的操作都会被加速。表现在更流畅的动画，更流畅的滚动，和整体灵敏度的提升，即使应用没有明确使用 **OpenGL** 库，同样会有效果。

不过并不是所有的 **OpenGL 2D** 操作都被加速了。如果启用了硬件加速渲染，需要通过测试应用来保证它生效了，同时不会出现渲染错误。

### android:icon

`为整个应用提供一个通用的icon，该icon为该应用所有组件的默认icon。`

属性值必须为包含一个图片的drawable资源引用。没有默认值。

### android:isGame

`定义应用是否是一个游戏。`

系统可能会对标示为游戏的应用进行单独分类，或者与其他应用分开单独显示。

### android:killAfterRestore

`定义应用在全系统恢复中恢复了设置后，是否需要被停止。`

一个应用包恢复操作不会导致该应用的关闭。全系统恢复操作会在手机第一次被设置好时发生一次停止操作。第三方应用通常不需要用到这个属性。

    默认值为true。即在全系统恢复时，应用处理完自身的数据后就会被关闭。

### android:largeHeap

`定义应用在运行时是否需要创建一个更大的Dalvik堆。`

这个属性会应用到该应用所有的进程。它只会被应用到第一个被加入进程的应用。

大多数的应用不应该需要这个属性，而是应该专注在通过降低总体存储占用来提升性能。同时使用这个属性不能保证一定能增大可用存储，因为设备也受它们的总可用存储的限制。

### android:label

`定义用户可读的Application标签，同时它也是Application所有组件的默认标签。`

标签应该是一个字符串资源的引用，因此它应该能像其他字符串一样在用户交互界面被定位到。同时，为了方便开发标签同样能设置成原始字串（raw string）。

### android:logo

`定义应用整个的默认标识，同时它也是所有子Activitys的默认标识。`

该属性应该是一个包含图片的drawable资源引用。没有默认值，必须得设置。

### android:manageSpaceActivity

`让用户可以手动管理应用的数据目录的Activitiy全名。`

Activity名必须为应用的子Activity组件。

### android:name

`该属性为一个实现Application的子类全名。当应用进程启动时，该类会早于其他所有Application组件启动。`

该属性是可选的，大多数的应用不需要。如果没有设置该属性，Android系统会使用一个基本Application实例。

### android:permission

`该属性为客户需要跟该应用交互所需权限的名字。`

该属性可以方便的为所有应用组件设置权限，同时可以被应用组件的权限属性覆盖。

### android:persistent

`该属性定义应用是否能一直保持运行。`

    默认值为false。在一般情况下，应用不该设置该值，该模式主要是为特定的系统应用设计的。

### android:process

`该属性定义了所有应用组件运行的进程名。组件自身的process属性可以覆盖Application的属性。`

    默认情况下，当应用的第一个组件需要运行时，系统就会为应用创建一个默认进程。默认进程名就是在manifest中设置的包名。

将该进程名设为跟另一个应用一样时，你可以让两个应用的组件在同一个进程里面运行。（必须保证两个应用使用同一个userID且用同一个证书签名）

如果进程名以一个分号开头，一个专属于该应用的进程会在需要的时候被创建。如果进程名以小写字母开头，就会创建一个全局进程。全局进程可以与其他应用共享，从而减少资源开销。

### android:restoreAnyVersion

`该属性表示了该应用是否接受任何任何备份数据集的恢复，就算备份数据属于比当前版本更高的应用，也同样会恢复。`

    默认值为false。如果设为了true，将允许BackupManager恢复一个不匹配的版本，导致数据不兼容。要谨慎使用。

### android:requiredAccountType

`该属性指定了应用运行所需要的账号类型。`

如果你的应用需要一个账号，那么这个值必须与应用的账号认证类型相符。e.g.,”com.google”。

    默认值为null，表示应用运行不需要任何账号。

该属性在API 18被加入。

### android:restrictedAccountType

`该属性制定了应用所需要的账号类型，同时表明允许受限的用户访问机主的该账户。`

如果应用需要一个账号，同时能允许受限用户访问主账户，则这个值必须与应用的账号认证类型相符。e.g.,”com.google”。

    默认值为null，表示应用运行不需要任何账号。

该属性在API 18被加入。

### android:supportsRtl

`该属性定义了应用是否支持从右到左的布局。`

    true: targetSdkVersion设为了17或更高时，许多RTL API就会被激活，系统使用这些API来显示从右到左的布局。
    false: (默认)该值为false或targetSdkVersion设为了17以下，RTL API就会被无视或无效，同时应用会忽略掉跟布局相关的locale设置。（应用的布局永远都是从左向右）

该属性在API 17被加入。

### android:taskAffinity

`该属性指明了Application内所有Activity想要进入的task的名字。如果Activity没有设置该属性，则启动的Activity都会在Application定的Task中。`

### android:testOnly

`该属性指明了这个Application是否只是用来测试的。`

    例如，指定了该属性后，应用就能对外暴露某些数据或者接口。这样可能会造成安全漏洞，但对测试十分有用。

该属性为true的应用只能通过adb来安装。

### android:theme

`该属性为所有的应用中的Activity设定了一个默认的主题。`

它为一个style资源的引用，同时每个Activity可以通过设置该属性类覆盖Application中的默认设置。

### android:uiOptions

`该属性为应用中ActivityUI的额外设置。`

    必须设为以下的值：
    none: (默认)没有额外设置。
    splitActionBarWhenNarrow: 当在一个狭窄的屏幕运行启用split actionbar时，会在屏幕的底部出现一个action bar显示所有action item。而顶部主要显示导航相关的内容。确保有足够的空间来显示action item、导航栏和顶栏。

该属性在API 14被加入。

### android:usesCleartextTraffic

`该属性指定是否允许未被加密的网络流量。`

### android:vmSafeMode

`该属性指定该应用是否应该向虚拟机一样在安全模式中运行。`

    默认值为false。

该属性在API 8中被加入时，设置为true会禁用Dalvik的JIT编译器。
该属性在API22中，设置为true会禁用ATR的AOT编译器。
