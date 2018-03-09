---
layout: post
title: "Python安装汇总"
date: 2017-12-21 11:00:00 +0800 
categories: 酱油人生
tag: Python install
---
* content
{:toc}

1.[ARIMA](http://blog.csdn.net/u010414589/article/details/49622625)
[ARIMA详述](https://www.cnblogs.com/foley/p/5582358.html)
2.[基于R语言的时间序列建模完整教程](https://www.analyticsvidhya.com/blog/2015/12/complete-tutorial-time-series-modeling/)


> 数据stationary的要求: https://stackoverflow.com/questions/42453381/why-i-got-the-computed-initial-ar-coefficients-are-not-stationary-while-using

缺点：
> 1.要求时序数据是稳定的（stationary），或者是通过差分化(differencing)后是稳定的。
> 2.本质上只能捕捉线性关系，而不能捕捉非线性关系。
注意，采用ARIMA模型预测时序数据，必须是稳定的，如果不稳定的数据，是无法捕捉到规律的。比如股票数据用ARIMA无法预测的原因就是股票数据是非稳定的，常常受政策和新闻的影响而波动。

判断时序是否稳定：
> 平稳性的含义：时间序列的统计性质关于时间平移的不变性。时间序列的统计性质关于时间平移的不变性
> 1.稳定的数据是没有趋势(trend)，没有周期性(seasonality)的; 它的均值，在时间轴上拥有常量的振幅，并且它的方差，在时间轴上是趋于同一个稳定的值的。
> 2.可以使用Dickey-Fuller Test进行假设检验。（）
> 3.德宾-沃森（Durbin-Watson）检验。德宾-沃森检验,简称D-W检验，是目前检验自相关性最常用的方法，但它只使用于检验一阶自相关性。

Arima的参数与数学形式
> ARIMA模型有三个参数:p,d,q。
> p--代表预测模型中采用的时序数据本身的滞后数(lags) ,也叫做AR/Auto-Regressive项
> d--代表时序数据需要进行几阶差分化，才是稳定的，也叫Integrated项。
> q--代表预测模型中采用的预测误差的滞后数(lags)，也叫做MA/Moving Average项

[Arima预测模型表示](https://www.cnblogs.com/bradleon/p/6827109.html)
> Y的预测值 = 常量c and/or 一个或多个最近时间的Y的加权和 and/or 一个或多个最近时间的预测误差
## 金融数据的时间序列特征
金融数据带漂移项的布朗运动，金融资产的价格随机游走，这说明我们不能基于金融资产价格进行预测，为了获得平稳的序列，即统计规律不发生大的变化的序列，我们通常查分求金融资产的对数收益率。收益率序列一般是通过平稳性检验的，统计特性的规律性较强（入尖峰肥尾，负偏，波动集聚）
2.GARCH模型
GARCH模型是用来预测时间序列方差的模型，方差可以衡量风险，所以ARCH、GARCH模型在金融领域倍受重视。GARCH模型可以（1）估计方差，衡量风险（2）可以计算均值方差中变量的置信区间（3）对条件异方差正确估计可以使估计参数更准确。我们时间序列跟投资在一个学期开，把GARCH-M跟CAPM模型一对比，恍然大悟啊。至于用什么软件做，一般的统计软件都可以的，上课讲的时候用的是EViews，像R、SAS这些软件都可以做的。再给你一个张晓桐老师的课件做参考吧。

3.[Garch和ARIMA的结合](http://www.dataguru.cn/thread-477226-1-1.html)
2.[Python包汇总](https://www.cnblogs.com/SandyKid/p/6142610.html)

6.[贝叶斯](http://www.statsmodels.org/stable/genindex.html)