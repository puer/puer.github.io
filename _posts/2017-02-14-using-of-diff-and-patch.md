---
layout: post
title: "用Diff和Patch工具维护源码"
description: ""
category: IT
tags: []
---
{% include JB/setup %}
在此仅举一个简单的例子来说明如何用diff/patch工具维护源码升级。
假设program-1.0目录中为老版，现开发完成的新版位于program-2.0目录中，将两个目录置于同一父目录下，然后在该父目录上执行：

    diff -Nur program-1.0 program-2.0 >program-2.0.patch

将生成一个program-2.0.patch的补丁文件，发布该补丁文件（当然可以先压缩成bzip2格式）。
假设拿到的是program-2.0.patch.bz2文件，则在program-1.0目录同级执行：
<!-- more -->

    bzcat program-2.0.patch.bz2 | patch -p0
    
如此即完成了从1.0到2.0的升级。
如果希望恢复到原版本，可以使用-R（--reverse）参数，但仅对上下文格式的diff文件有效。还有一个备份参数也可以使用，但简单应用中，整个目录备份可能更方便一些。