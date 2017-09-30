---
layout: post
title: "股票市场基本知识"
date: 2017-09-29 18:00:00 +0800 
categories: 诗和远方
tag: Algorithms
---
* content
{:toc}


<!-- more -->
 ## 1 股票市场
完整意义上的现代股票市场包括了三个层次，分别是股票一级发行市场、二级交易市场和三级风险管理市场，其中三级风险管理市场主要是指股指期货、期权市场。
>- 一级市场，指股票的初级市场也即发行市场，在这个市场上投资者可以认购公司发行的股票，成为公司股东。投资银行（investment bank）是一级市场上协助证券首次售出的重要金融机构。投资银行的做法是承销（underwriting）证券，即它们确保公司证券能够按照某一价格销售出去，之后再向公众推销这些证券。
>- 二级市场，是交易市场。保证有价证券的流通。
>- 三级市场，由非交易所会员对在全国性交易所上市的普通股进行的场外交易的一种股票交易市场。包括退市的股票和因历史遗留问题而未能上市交易的股票交易的市场。

## 2 现货 & 期货
>- 现货市场：股票现货市场交易对象是上市公司股票，一笔交易完成后，股票从卖方账户划转至买方账户。股票现货市场持仓总量始终与股票流通总量相等，也不存在空头持仓的概念。
>- 股指期货：


## 3 额外收益率
基于CAPM模型，证券投资的额外收益率可以看做两部分之和。第一部分是和整个市场无关的，叫**阿尔法**；第二部分是整个市场的平均收益率乘以一个贝塔系数。贝塔可以称为这个投资组合的**系统风险**。
市场收益是m,基金收益是f，做个线性回归：f=alpha+beta*m+e，这就是alpha的定义，一般指相对市场的超额收益。阿尔法体现的是管理人的能力，贝特反应的是股票市场的系统性风险。

### 3.1 贝特收益
> 整个市场的涨跌对各个投资组合提供的收益率却可能不 同。这就是贝塔系数，它取决于这个投资组合和市场的相关性以及投资组合相比市场的风险大小。一般的投资组合的贝塔系数通常是正的，股票指数基金的贝塔系数一般在1左右。
> 只要通过调节投资组合中的现金和股票指数基金(或者股指期货)的比率，就可以很容易地改变贝塔系数，即投资组合中来 自整个市场部分的收益
> 指数基金(Index Fund)和交易型开放式指数基金(ETF，Exchange Traded Fund)是购买纯贝塔的工具


### 3.2 阿尔法收益
+ alpha是与大盘无关的部分的收益，是一个基金核心价值体现。一般主动型公募基金阿尔法收益和贝特收益，对冲基金卖的就是纯阿尔法收益，试图获得纯阿尔法的，又不像私募股权投资基金那样投资于非公开上市交易股权的基金，就是**对冲基金**。
+ alpha是超额收益，组合收益扣除市场、行业、size等这些广义beta之后的残差项，也就是说不是靠系统性的上涨而获取的收益；
+ 以股票市场为例，我们就可以通过寻找能够获取alpha的驱动因子来构建组合，由于组合的涨跌我们是不知道的，我们能够确保的是组合与基准的收益差在不断扩大，那么持有组合，做空基准，对冲获取稳定的差额收益（alpha收益）,这就是传说中的市场中性策略(**股票多空头**，**股指多空头**)。
![box-model]({{ '/styles/images/study/defineOfAlpha.jpg' | prepend: site.baseurl }})

>推荐书籍《quantitive equity portfolio》《主动投资组合管理》《finding alphas》。
 
### 3.3 寻找阿尔法

优矿已经提供了海量的基础因子，可见[优矿因子周报](https://uqer.io/community/share/57425e58228e5b86a71fd0c3)；同时实现了Worldquant的websim中可以玩的工具并且把封闭的websim变成了开放的平台, 可以详见[如何用Quartz Signal快速实现Worldquant 101 Alpha](https://uqer.io/community/share/56e7d803228e5b887de50afe)。
例如 [文章](http://papers.ssrn.com/sol3/Papers.cfm?abstract_id=2701346) 中描述的alpha 53为例，其原始表达式为:
> (−1*delta((((close−low)−(high−close))/(close−low)),9))
--[知乎](https://www.zhihu.com/question/23543972/answer/102596255)

在优矿中测试alpha有效性的方法：

``` python

import numpy as np
start = '2012-01-01'                       # 回测起始时间
end = '2016-01-01'                         # 回测结束时间
benchmark = 'HS300'                        # 策略参考标准
universe = set_universe("HS300", end)  # 证券池，支持股票和基金
capital_base = 100000                      # 起始资金
freq = 'd'                                 # 策略类型，'d'表示日间策略使用日线回测，'m'表示日内策略使用分钟线回测
refresh_rate = 5                           # 调仓频率，表示执行handle_data的时间间隔，若freq = 'd'时间间隔的单位为交易日，若freq = 'm'时间间隔为分钟

def foo(data, dependencies=['closePrice', 'highPrice', 'lowPrice'], max_window=9):
    today = (2*data['closePrice'].ix[-1]-data['lowPrice'].ix[-1]-data['highPrice'].ix[-1])/(data['closePrice'].ix[-1]-data['lowPrice'].ix[-1])
    day_9 = (2*data['closePrice'].ix[-9]-data['lowPrice'].ix[-9]-data['highPrice'].ix[-9])/(data['closePrice'].ix[-9]-data['lowPrice'].ix[-9])
    return day_9 - today
    
def initialize(account):                   # 初始化虚拟账户状态
    a = Signal("worldquant_53", foo)
    account.signal_generator = SignalGenerator(a)
    
def handle_data(account):                  # 每个交易日的买入卖出指令
    weight = account.signal_result['worldquant_53']
    weight = weight[weight>0]
    weight = weight.replace([np.inf, -np.inf], np.nan).dropna()
    weight = weight/weight.sum()
    
    buy_list = weight.index
    sell_list = account.valid_secpos
    for stk in sell_list:
        if stk not in buy_list:
            order_to(stk, 0)
        
    total_money = account.referencePortfolioValue
    prices = account.referencePrice 
    for stk in buy_list:
        if stk not in prices:
            continue
        if np.isnan(prices[stk]) or prices[stk] == 0:  # 停牌或是还没有上市等原因不能交易
            continue
        order_num = int(total_money * weight[stk] / prices[stk] /100)*100
        if order_num < 100:
            order_num = 100
        order_to(stk, order_num)
```

### 4. 另类投资
另类投资有许多种。如果投资于非上市股权，或者上市公司非公开交易股权，就叫做**私募股权投资**(Private Equity，简称PE)。广义的私募股权投资涵盖了企业首次公开发行前各阶段的权益投资，包括大家可能熟悉的**创业投资**(Venture Capital，简称VC、创投)等


---

编辑备注：

+ 2017-09-28第一次编辑
+ 2017-09-30第二次编辑