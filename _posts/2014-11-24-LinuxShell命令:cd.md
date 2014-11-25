---
layout: post
title:  LinuxShell命令详解:cd
date:   2014-11-25 09:15:21
categories: system
---

# 前言

平常一直都有使用Linux下**bash shell**一些常用命令,但是都没有很系统的去学它们.为了提高开发效率,减少出错,同时为**Shell脚本编程**打基础.现在开始准备一个一个的去详细学习.

----

# cd命令

`cd`命令大家再熟悉不过了,**bash shell**经常会被用到的切换目录命令.
接下来我们直接通过万能的`man`来了解`cd`命令.

>* 直接 `man cd` 是不行的,会显示 **No manual entry for cd** .`cd`命令是`bash`基本命令中的一种,所以应该是 `man bash`.
>* 关于**man**以及**man page**等相关内容会在以后的 **LinuxShell命令:man** 中详细介绍.

通过查找`man page`里可以看到`cd`的命令语法如下

      cd [-L|[-P [-e]] [-@]] [dir]

## 基本作用

cd命令的作用就是从当前目录跳转到**dir**处, 如果**dir**处留空的话就会跳转到**环境变量HOME**中设置的值.

## 附加内容

### 环境变量CDPATH

对于**环境变量CDPATH**,

* 如果没有设置**CDPATH**的话,每次`cd`查找的跳转目录都是以当前的目录为父目录.
* 若有设置**CDPATH**的话,每次`cd`查找的跳转目录就是以设置的目录为父目录来查找.

e.g. 假设当前有目录结构: ~/a/b/c 若没有设置CDPATH
{% highlight bash %}
luckyshq@localhost:~$ cd a
luckyshq@localhost:~/a$ cd c
bash: cd: c: No such file or directory
{% endhighlight %}

若将CDPATH设为`CDPATH=.:/home/luckyshq/a/b`的话
{% highlight bash %}
luckyshq@localhost:~$ cd a
luckyshq@localhost:~/a$ cd c
luckyshq@localhost:~/a/b/c$
{% endhighlight %}

将常用目录设置到**CDPATH**里就能有效提高`cd`的效率.

>* CDPATH中目录见用`:`隔开.
>* 若不加上`.`路径(即当前路径的话),以前默认的本目录作为父目录`cd`就不可用了.
>* 若**dir**处是以`/`开头(即是绝对路径)的话,CDPATH就失效了.

### cd -P, -e参数

进入到**快捷方式目录**的实际目录中.
e.g. 假设 ~ 目录下有a,b两个目录, 同时a下有一个连接到b的子目录b(这个b是快捷方式)
{% highlight bash %}
// 不加 -P 参数
luckyshq@localhost:~$ cd a
luckyshq@localhost:~/a$ cd b
luckyshq@localhost:~/a/b$

//加上 -P 参数
luckyshq@localhost:~$ cd a
luckyshq@localhost:~/a$ cd -P b
luckyshq@localhost:~/b$
{% endhighlight %}

若将一个文件夹自己的快捷方式放到文件夹里,这样写脚本的时候就有可能会出现无限循环,当前路径名就会变得无限长,但是加上了`-P`命令后就可以避免无线循环的情况.

如果在`-P`后面加上`-e`的话,若跳转前路径不存在对应物理路径的话(比如说夹杂着多个快捷方式为名称的路径)就会返回一个**失败的状态**.(-e具体的用法可能要到Shell编程时才能体会到.)

### cd -L参数

`-L`参数和`-P`相反(两者不能同时出现,即 `-L|-P`),是跳转到链接目录中,类似于不带参数的`cd`.(加不加`-L`具体有什么区别还没弄清=,=)

### ..

**dir**中如果出现了`..`,

>* 若`..`后有路径,则吞掉路径中第一个目录元素(例如 `cd ../a/b/c` 等价 `cd b/c`).
>* 若`..`后没路径,则退回到当前路径的父目录中.

### -@参数

原文解释如下:(貌似我系统不支持,用不了-@参数)

On systems that support it, the -@ option presents the extended  attributes  associated  with  a file  as  a directory.  An argument of - is converted to $OLDPWD before the directory change is attempted.  If a non-empty directory  name  from  CDPATH is used, or if - is the first argument, and the directory change is successful, the absolute pathname of the  new  working  directory  is written to the standard output. The return value is  true  if  the  directory  was  successfully changed; false otherwise.
