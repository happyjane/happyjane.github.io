---
layout: post
title: "价值投资&量化投资"
date: 2017-10-30 18:00:00 +0800 
categories: 诗和远方
tag: Quant Learning
---
* content
{:toc}

我以前有个同事曾经在价值投资中使用量化分析，就是统计5年内所有A股上市公司在发布业绩预增公告之后，在一个月内股价相对大盘的强弱，结论是业绩预增的公司股票走势有较大概率强于大盘
[价值投资与量化](https://www.zhihu.com/question/39994649)
[数据源](http://www.waditu.cn/reference.html#id5)
[决策树可视化](http://blog.csdn.net/u012845311/article/details/77294973)
[spark.mlib](http://www.cnblogs.com/LT-blogs/p/6228805.html)

### 市场中性策略
市场中性策略基金同时持有多头和空头仓位，以对冲市场风险。一般来说市场中性策略分为货币等额市场中性和 Beta 
市场中性。货币等额市场中性：买入股票的多头头寸和卖空的空头头寸的货币价值数额相等。但货币等额市场中性，并不意味着组合的 Beta 为 0，并非真正的市场中性。Beta 市场中性：调整买入和卖空的头寸，使得整体组合的 Beta 值等于0，即理论上不受市场大盘涨跌的影响。
市场中性策略通过定量或定性的方法来选择股票，选择回报率高于市场平均水平的股票作为多头头寸，选择回报率低于市场平均水平的股票作为空头头寸。市场中性策略也可进一步拓展为行业中性策略和因素中性策略，即通过同时持有某一行业或某一因素相关的股票的多头和空头仓位，来对冲这一行业或这一因素的风险，使组合不受行业或因素变化的影响。
这种策略的优点是：可以通过同时持有多头和空头仓位的资产配置，达到对冲市场风险的目的，或者实现对某一因素的局部风险免疫；与市场大盘走势相关度小，Beta 值为 0，由 CAPM 模型可知，投资人对它的期望回报率要求较低，可能接近无风险利率；适合养老基金、捐赠基金、保险资金等大资金进行资产大类的配置，以分散风险；如果选股正确，将可以同时在多头和空头仓位获利。
缺点是：因为股票的股价和 Beta 值都是在不断的变化中，要完全对冲市场风险，必须随时动态调整多头和空头的仓位，否则将不能保证组合的 Beta 值始终为 0，即组合仍然会受到市场大盘涨跌的影响；如果选股错误，将同时在多头和空头仓位遭受损失

