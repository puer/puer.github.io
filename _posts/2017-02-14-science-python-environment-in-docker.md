---
layout: post
title: "图像分析和科学计算的docker环境"
description: ""
category: 
tags: []
---
{% include JB/setup %}
图像分析和科学计算使用python的opencv和numpy是最方便和最主流的方法. 如果想要所见即所得的效果可以使用ipython来获得. 最近ipython将前端展示分离到jupyter项目. 

> IPython is a growing project, with increasingly language-agnostic components. IPython 3.x was the last monolithic release of IPython, containing the notebook server, qtconsole, etc. As of IPython 4.0, the language-agnostic parts of the project: the notebook format, message protocol, qtconsole, notebook web application, etc. have moved to new projects under the name Jupyter. IPython itself is focused on interactive Python, part of which is providing a Python kernel for Jupyter.

正好最近某个项目需要使用这些库, 就顺便做了一个docker环境, 方便管理和使用. 下面是伪Dockerfile, 供参考

```
FROM python:2.7

COPY sources.list /etc/apt/sources.list
RUN apt-get update && \
    pip install numpy Pillow jupyter
RUN apt-get install -y cmake libgtk2.0-dev libavcodec-dev libavformat-dev libswscale-dev python-dev python-numpy

## 获得opencv包 并解压
cd  opencv
mkdir build
cd build
cmake -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=/usr/local -D PYTHON2_EXECUTABLE=/usr/bin/python -D PYTHON_INCLUDE_DIR=/usr/include/python2.7 -
D PYTHON_INCLUDE_DIR2=/usr/include/x86_64-linux-gnu/python2.7 -D PYTHON_LIBRARY=/usr/lib/x86_64-linux-gnu/libpython2.7.so -D PYTHON2_NUMPY_INCLUDE_DIRS=/
usr/lib/python2.7/dist-packages/numpy/core/include/ ..
make install
```

环境启动之后, 就可以在浏览器访问192.168.171.130:8888进行使用了.
```
docker run -d -v /home/dots/work/sci:/sci -p 192.168.171.130:8888:8888 jupyter sh -c "jupyter notebook --notebook-dir=/sci --port=8888 --ip=0.0.0.0 --no-browser"
```


![jupyterpreview](http://wx1.sinaimg.cn/mw690/6392f3f7ly1fcpw5lhui2j20sa0k1k01.jpg)


#### 或者是使用dataquestio已经搭好的环境
[https://github.com/dataquestio/ds-containers](https://github.com/dataquestio/ds-containers)

[https://www.dataquest.io/blog/data-science-quickstart-with-docker/](https://www.dataquest.io/blog/data-science-quickstart-with-docker/)

dataquestio/python3-starter                 5
dataquestio/python2-starter                 0
dataquestio/ubuntu-base                     0
