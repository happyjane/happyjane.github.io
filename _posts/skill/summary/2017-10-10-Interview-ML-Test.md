---
layout: post
title: "机器学习笔试题"
date: 2017-09-27 18:00:00 +0800 
categories: 酱油人生
tag: Machine Learning
---
* content
{:toc}

#### 1.	SVM经常使用的核函数有：
	(1)线性核函数(2)多项式核(3)径向基核（RBF）(4)傅里叶核(5)样条核(6)Sigmoid核函数
#### 2.	特征选择方法（填空）：


#### 3.	请尽可能列举python列表的成员方法，并给出一下列表操作的答案：
a=[1, 2, 3, 4, 5], a[::2]=______, a[-2:] = __________
#### 4.	List = [-2, 1, 3, -6]，如何实现以绝对值大小从小到大将 List 中内容排序。

#### 5.	数据清理中，处理缺失值的方法有哪些?
数据清理中，处理缺失值的方法有两种：
+ 删除法：1）删除观察样本
       2）删除变量：当某个变量缺失值较多且对研究目标影响不大时，可以将整个变量整体删除
       3）使用完整原始数据分析：当数据存在较多缺失而其原始数据完整时，可以使用原始数据替代现有数据进行分析
       4）改变权重：当删除缺失数据会改变数据结构时，通过对完整数据按照不同的权重进行加权，可以降低删除缺失数据带来的偏差
+ 查补法：均值插补、回归插补、抽样填补等
成对删除与改变权重为一类，估算与查补法为一类

#### 6.	KNN和K-Means的区别有哪些
<table>
<tr>
  <th width 50%,bgcolor = yellow>KNN</th>
  <th width 50%,bgcolor = yellow>K-Means</th>
</tr>
<tr>
  <td> use a long listing format  </td>
  <td>  1.KNN是分类算法 
		2.监督学习 
		3.喂给它的数据集是带label的数据，已经是完全正确的数据</td>
  <td>  1.K-Means是聚类算法 
        2.非监督学习 
        3.喂给它的数据集是无label的数据，是杂乱无章的，经过聚类后才变得有点顺序，先无序，后有序
        </td>
</tr>
<tr>
  <td> 没有明显的前期训练过程，属于memory-based learning </td>
  <td> 有明显的前期训练过程 </td>
</tr>
<tr>
  <td> K的含义：来了一个样本x，要给它分类，即求出它的y，就从数据集中，在x附近找离它最近的K个数据点，这K个数据点，类别c占的个数最多，就把x的label设为c</td>
  <td> K的含义：K是人工固定好的数字，假设数据集合可以分为K个簇，由于是依靠人工定好，需要一点先验知识 </td>
</tr>

#### 7.	下列哪个不属于CRF模型对于HMM和MEMM模型的优势（B）
 A. 特征灵活  B. 速度快  C. 可容纳较多上下文信息  D. 全局最优
#### 8.	以下哪个是常见的时间序列算法模型（B）
 A. RSIB. MACDC. ARMAD. KDJ
#### 9.	一道SQL语句面试题，关于group by表内容：
info 表
date result
2005-05-09 win
2005-05-09 lose
2005-05-09 lose
2005-05-09 lose
2005-05-10 win
2005-05-10 lose
2005-05-10 lose
如果要生成下列结果, 该如何写sql语句?
      win lose
2005-05-09 2 2
2005-05-10 1 2

(1) select date, sum(case when result = "win" then 1 else 0 end) as "win", sum(case when result = "lose" then 1 else 0 end) as "lose" from info group by date;
(2) select a.date, a.result as win, b.result as lose
　　from
　　(select date, count(result) as result from info where result = "win" group by date) as a
　　join
　　(select date, count(result) as result from info where result = "lose" group by date) as b
　　on a.date = b.date;

#### 10.	一种双核CPU的两个核能够同时的处理任务，现在有n个已知数据量的任务需要交给CPU处理，假设已知CPU的每个核1秒可以处理1kb，每个核同时只能处理一项任务。n个任务可以按照任意顺序放入CPU进行处理，现在需要设计一个方案让CPU处理完这批任务所需的时间最少，求这个最小的时间。 
输入描述:
输入包括两行：
第一行为整数n(1 ≤ n ≤ 50)
第二行为n个整数length[i](1024 ≤ length[i] ≤ 4194304)，表示每个任务的长度为length[i]kb，每个数均为1024的倍数。
输出描述:
输出一个整数，表示最少需要处理的时间
输入例子:
5
3072 3072 7168 3072 1024
输出例子:
9216
``` cpp
for (int i = 0; i < n; i++) 
    {
        for (int j = 1; j <= sum / 2; j++) 
        {
            dp[i + 1][j] = dp[i][j];
            if (j >= vec[i] && dp[i][j - vec[i]] + vec[i]>dp[i][j])
                dp[i + 1][j] = dp[i][j - vec[i]] + vec[i];
        }
    }
``` 
#### 11.	请举例说明map 和 lambda 的用法。

#### 12.	解释朴素贝叶斯算法里面的先验概率、似然估计和边际似然估计？

#### 13.	什么时候Ridge回归优于Lasso回归？
答：你可以引用ISLR的作者Hastie和Tibshirani的话，他们断言在对少量变量有中等或大尺度的影响的时候用lasso回归。在对多个变量只有小或中等尺度影响的时候，使用Ridge回归。
#### 14.	Gradient boosting算法（GBM）和随机森林都是基于树的算法，它们有什么区别？
答：最根本的区别是，随机森林算法使用bagging技术做出预测。 GBM采用boosting技术做预测。在bagging技术中，数据集用随机采样的方法被划分成使n个样本。然后，使用单一的学习算法，在所有样本上建模。接着利用投票或者求平均来组合所得到的预测。Bagging是平行进行的。而boosting是在第一轮的预测之后，算法将分类出错的预测加高权重，使得它们可以在后续一轮中得到校正。
这种给予分类出错的预测高权重的顺序过程持续进行，一直到达到停止标准为止。随机森林通过减少方差（主要方式）提高模型的精度。生成树之间是不相关的，以把方差的减少最大化。在另一方面，GBM提高了精度，同时减少了模型的偏差和方差。
#### 15.	哪些机器学习算法不需要做归一化处理？
概率模型不需要归一化，因为它们不关心变量的值，而是关心变量的分布和变量之间的条件概率，如决策树、rf。而像adaboost、gbdt、xgboost、svm、lr、KNN、KMeans之类的最优化问题就需要归一化。


