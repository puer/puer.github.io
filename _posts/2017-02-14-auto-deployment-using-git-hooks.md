---
layout: post
title: "使用 git hooks 自动部署"
description: ""
category: IT
tags: ["hexo", "blog", "git", "hook"]
---
{% include JB/setup %}
### 使用 git hooks 自动部署

下面是一个 `hooks/post-receive` 文件的例子, 在收到 git 推送后自动 build 静态 html.
<!-- more -->

```
#!/bin/sh
#
# An example hook script to prepare a packed repository for use over
# dumb transports.
#
# To enable this hook, rename this file to "post-update".

git push --all origin

unset GIT_DIR

# GIT_REPO=$HOME/git/note.git
GIT_WORKING_DIR=$HOME/note

cd $GIT_WORKING_DIR
git add . -A
git stash
git co master
git pull origin
export PATH=$PATH:$HOME/node/bin
hexo generate

exit 
```
