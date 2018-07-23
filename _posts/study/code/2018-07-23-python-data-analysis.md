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

# Numpy处理速度快的原因：

1. NumPy的数组类(被用来实现矩阵类的基础)是考虑速度的实现，所以存取NumPy数组比存取Python列表速度更快。此外，NumPy实现一种数组语言，以致于不需要大多数循环。
2. NumPy的导入都比普通Python中的循环更快。为什么？Python是一种动态类型的解释语言，这意味着在每次循环迭代时它都必须检查运算对象a和b的类型来选则+正确的意义。(在python中+被用到许多地方，比如连接字符串、可以有不同元素类型的列表)当’+’的操作对象之一是一个NumPy数组时，NumPy的add函数将被Python自动选择，仅仅检测一次类型。然后它通过编译C函数执行”真正的”加法循环。这和普通python中的解释循环相比是非常快的。



