---
layout: post
title:  LinuxShell命令详解:cat
date:   2014-11-28 09:42
categories: system
---

# cat命令

`cat`命令的主要作用是显示一个文件的内容,常与重定向符号`>`搭配使用.

## 主要使用方法

* `cat FILE` 在Terminal中显示文件的所有内容.
* `cat > FILE` 直接从Terminal中输入文件内容并创建文件.只能用于创建,不能修改已有文件.
* `cat FILE1 FILE2 > FILE` 将多个文件内容合并到一个文件里.

## 参数介绍

* `-v, --show-nonprinting` 除了`LFD`和`TAB`之外,使用`^`和`M-`标注.
* `-T, --show-tabs` 将`TAB`显示为`^I`.
* `-E, --show-ends` 每行的末尾显示`$`.
* `-A, --show-all` 等同于`-vET`.
* `-n, --number` 对所有行标行号输出.
* `-b, --numbernonblank` 对于不为空的行标行号显示,会覆盖`-n`.
* `-e` 等同于`-vE`.
* `-s, --squeeze-blank` 多个空行只显示为一个空行.
* `-t` 等同于`-vT`.
* `--help` 显示帮助信息.
* `--version` 显示版本信息.
