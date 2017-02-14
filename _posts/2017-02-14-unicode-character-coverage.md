---
layout: post
title: "覆盖所有Unicode基本语言集的字体"
description: ""
category: 
tags: []
---
{% include JB/setup %}

并不是所有字体都覆盖了unicode的所有可打印字符. 我们常见到的问题是, 英文字体可以正常显示英文字符, 但是不能显示中文. 原因并不是中文编码有问题, 而是识别出的中文不知道怎么显示. 而中文字体就可以正常覆盖中文内容. 但是unicode标准定义了各种语言,韩文,老挝语,数学专用符号等. 这些字符, 中文的字体并不一定有定义.
为了解决这种问题, GNU Unifont制作了一个可以覆盖Unicode 8.0基本语言集的字体unifont

http://unifoundry.com/unifont.html

![unicode 8.0 chart](http://unifoundry.com/pub/unifont-9.0.06/unifont-9.0.06.bmp)
