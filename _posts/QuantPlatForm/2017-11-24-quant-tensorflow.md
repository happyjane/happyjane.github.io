---
layout: post
title: "GPU版tensorflow安装步骤"
date: 2017-09-27 18:00:00 +0800 
categories: 诗和远方
tag: Tensorflow
---
* content
{:toc}

## 系统环境
我的电脑是英伟达集成显卡，首先到官网安装最新版的显卡驱动，安装的时候会提示检测java环境是否是最新版，如果不是更新到最新版，这里要用Ie浏览器，用谷歌浏览器总是报错。

## python
安装的是Python 3.5版本，自带pip

## 安装TensorFlow
以管理员身份运行CMD，然后输入一下命令来自动安装：
> pip3 install --upgrade https://storage.googleapis.com/tensorflow/windows/gpu/tensorflow_gpu-0.12.0-cp35-cp35m-win_amd64.whl
或者：
> pip3 install tensorflow-gpu

## 注意： 我自己在安装的过程完成后，导入tensorflow时总是提示如下问题：
Error importing tensorflow. Unless you are using bazel.
you should not try to import tensorflow from its source directory;
please exit teh tensorflow source tree, and relaunch your python interpreter from there.

解决方法： 下载Windows 的 Microsoft Visual C++ 2015 redistributable update 3 64bit 安装即可
下载路径：https://www.microsoft.com/zh-cn/download/confirmation.aspx?id=53840

## 测试脚本

``` python 

$ python

>>> import tensorflow as tf
>>> hello = tf.constant('Hello, TensorFlow!')
>>> sess = tf.Session()
>>> print(sess.run(hello))
Hello, TensorFlow!
>>> a = tf.constant(10)
>>> b = tf.constant(32)
>>> print(sess.run(a + b))

```