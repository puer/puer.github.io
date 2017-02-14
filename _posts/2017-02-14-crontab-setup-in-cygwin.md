---
layout: post
title: "Crontab Setup in Cygwin"
description: ""
category: it
tags: ["cygwin", "crontab"]
---
{% include JB/setup %}
在从业务环境中获取数据的时候，不可避免的需要使用任务的调度。windows自带的计划任务不是很灵活，可以在windows下安装cygwin模拟unix环境，这样就可以方便使用crontab了

首先在cygwin的安装选项里要选上admin目录中的cron，安装完之后，需要运行

    cygrunsrv -I cron -p /usr/sbin/cron -a -n

来安装这个服务

`-I` 是安装

`cron`是服务名

`-p /usr/sbin/cron` 是指定服务程序的目录

`-a` 后跟运行服务时需要添加的参数，这里运行服务的命令是 `/usr/sbin/cron -n`

 
安装完服务之后，需要运行

`cygrunsrv -S cron` 来启动这个服务

 
我启动的时候一直遇到windows error 1062

在`/var/log/cron.log`里面发现是`/var/cron: Permission denied`

`/var/cron`权限不够

将这个目录`chmod 755` 就搞定了

cronevent