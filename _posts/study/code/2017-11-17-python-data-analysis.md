---
layout: post
title: "python数据分析"
date: 2018-07-23 18:00:00 +0800 
categories: 酱油人生
tag: python
---
* content
{:toc}

<!-- more -->
# python正态分布计算

1.求正太分布逆分布：scipy.stats.invgauss

# python数学计算包：

**numpy**:一个定义了数值数组和矩阵类型和它们的基本运算的语言扩展，numpy的优势是矩阵运算,纯数学，计算速度快，存储和处理大型矩阵，是基础扩展。
**[scipy](https://docs.scipy.org/doc/)**:一种使用NumPy，科学计算库，来做高等数学、信号处理、优化、统计和许多其它科学任务的语言扩展。
**[pandas](http://pandas.pydata.org/pandas-docs/stable/10min.html)**:基于NymPy的一种工具，为了解决数据分析任务而创建的，其中纳入了大量的库和标准的数据类型，提供高效操作大数据集所需的工具，最具有统计意味的工具包，某些方面优于R软件。**数据结构**有一维的Series，二维的DataFrame(类似于Excel或者SQL中的表，如果深入学习，会发现Pandas和SQL相似的地方很多，例如merge函数)， 三维的Panel。
**matplotlib**:python中最著名的绘图系统.很多其他的绘图例如seaborn（针对pandas绘图而来）也是由其封装而成。这个绘图系统操作起来很复杂，和R的ggplot,lattice绘图相比显得望而却步，这也是为什么我个人不丢弃R的原因. 但是matplotlib的复杂给其带来了很强的定制性

# 容易混淆/出错的地方：

生成0-N数列的函数：在python中是range(N+1)，但是在numpy中是arange(N+1)

数组切片：

numpy的零矩阵 np.zeros((3,3))  3维零矩阵，对于矩阵，形参必须是带括号（）的，即tuple类型

改变多维数组维数 np.reshape((dim1,dim2)) 必须是（）的tuple类型



