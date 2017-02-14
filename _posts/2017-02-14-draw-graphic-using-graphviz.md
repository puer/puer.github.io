---
layout: post
title: "graphviz画流程图"
description: ""
category: IT
tags: ["graph", "flowchart", "graphviz"]
---
{% include JB/setup %}
Graphviz 或 Graph Visualization 是由 AT&T 开发的一个开源的图形可视化工具。它提供了多种画图能力，但是我们重点关注的是它使用 Dot 语言直连图的能力。在本文中，我们将简单介绍如何使用 Dot 来创建一个图形，并展示如何将分析数据转换成 Graphviz 可以使用的规范。（请参阅 参考资料 一节，以获得有关下载这个开源软件的信息。）

#### Dot 使用的图形规范

使用 Dot 语言，您可以指定三种对象：图、节点和边。为了让您理解这些对象的含义，我们将构建一个例子来展示这些元素的用法。
```
digraph sms {
    size = "8,8";
    edge [fontname="Microsoft YaHei"];
    node [shape=box, fontname="Microsoft YaHei" size="20,20"];

    1[label="sendid, phoneno, smid, \nsmcontent任何一个为空?"]
    2[label="tm_t_replymessage中\n已经存在相同sendid, phoneno,\nsmid的记录"];
    3[label="是否有对\n应的已发送短信\n(tm_t_sendmessage)"];
    4[label="create tm_t_replymessage record"];
    
    5[label="根据回复的\n短息查找相应的Rule\n(platformNumber+ ActivityInstruction)"];

    1 -> 2 -> 3 -> 4 -> 5;
    1 -> end [label="Y"];
    2 -> end [label="Y"];
    3 -> end [label="N"];

}
```

![sms](http://wx3.sinaimg.cn/mw690/6392f3f7ly1fcpucxu4vyj20e90fgwf5.jpg)

下面是一个复相对复杂的例子
```
digraph sms {
    size = "5,5";
    edge [fontname="Microsoft YaHei"];
    node [shape=box, fontname="Microsoft YaHei" size="20,20"];
    1[label="发生销售需求时"];
    2[label="编辑订单"];
    3[label="审批"];
    4[label="是否为电子契约"];
    3, 4 [shape=diamond];
    5[label="发送到分销系统"];
    6[label="分销系统是否同意"];
    3 -> 1[label="否", tailport=e];
    3 -> 4[label="通过", tailport=s];
    4 -> 5[label="是"];
    6 -> 1[label="拒绝"];
    11[label="产品出库处理"];
    22[label="发货"];
    33[label="到货回单"];
    44[label="销售单类型"];
    55[label="应收处理"];
    66[label="借欠处理"];
    4 -> 11[label="否"];
    6 -> 11[label="同意"];
    44 -> 55[label="销售单"];
    44 -> 66[label="结出单"];
    start -> 1 -> 2 -> 3;
  5 -> 6;
    11 -> 22 -> 33 -> 44;
    {55; 66} -> end;
    {rank=same;2;11;}
    {rank=same;3;22;}
    {rank=same;4;33;}
    {rank=same;5;44;}
    {rank=same;6;55;66;}
}
```
