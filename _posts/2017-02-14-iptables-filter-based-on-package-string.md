---
layout: post
title: "iptables过滤客户端的非法请求导致的一个问题"
description: ""
category: IT
tags: ["httpd", "iptables", "security"]
---
{% include JB/setup %}
使用iptables的string模块可以根据请求的URL把某些不希望访问的http请求过滤掉.
```
iptables -I INPUT -p tcp --dport 80 -m string --string "GET /lujie.php" --algo bm --from 64 --to 500 -j DROP
iptables -I INPUT -p tcp --dport 80 -m string --string "/ClassLogo/2013-3-8-1.jpg" --algo bm --from 64 --to 500 -j DROP
```
但是这种方式会造成httpd prefork产生大量的进程. 我猜测原因可能是 客户端发起tcp连接后, 开始http会话, 而http请求的url地址由于触发防火墙DROP规则, 没有到达httpd, httpd 就会一直等待客户端发起http请求. 在有新的请求到达时,原来在等待客户端的httpd进程被认为"忙", httpd主控只好swap新的httpd进程服务新的请求.
