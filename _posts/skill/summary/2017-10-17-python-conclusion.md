---
layout: post
title: "Python技巧总结"
date: 2017-12-14 11:00:00 +0800 
categories: 酱油人生
tag: Python connector
---
* content
{:toc}


## 技巧

1.列表巧用
``` python 

$ python

data = DataFrame(np.arange(15).reshape(3,5),index=['one','two','three'],columns=['a','b','c','d','e'])
print(data)
result = [price for tup in data[['a','b']].values for price in tup ]
print(data[['a','b']].values)
print(result)

```

2.生成NaN矩阵
``` python 

$ python

DataFrame(np.empty([_dummy_row,_dummy_col])*np.nan)
```
3.正态分布的逆分布


4.巧用与或非
``` python 

import pandas as pd
data1 = {"column1": ["A", "B", "C", "D", "E", "F", "G", ...],
         "column2": [338, 519, 871, 1731, 2693, 2963, 3379, ...],
         "column3": [5, 1, 8, 3, 731, 189, 9, ...], 
         "columnA" : [5, 0, 75, 150, 0, 0, 0, ...], 
         "columnB" : [0, 32, 0, 96, 0, 51, 0, ...], 
         "columnC" : [0, 42, 0, 42, 0, 42, 42, ...]}

df = pd.DataFrame(data1)

df['newcolumn'] = 0
print('df',df)
cond_A = df.columnA == 0
cond_B = df.columnB == 0
cond_C = df.columnC!=0
print(cond_A)
print(cond_C)
print(cond_A&cond_C)
df.loc[cond_A&cond_B&cond_C,'newcolumn'] = 1

```
5.dataframe之 apply

``` python 
import pandas as pd
data1 = {"column1": ["A", "B", "C", "D", "E", "F", "G", ...],
         "column2": [338, 519, 871, 1731, 2693, 2963, 3379, ...],
         "column3": [5, 1, 8, 3, 731, 189, 9, ...], 
         "columnA" : [5, 0, 75, 150, 0, 0, 0, ...], 
         "columnB" : [0, 32, 0, 96, 0, 51, 0, np.nan], 
         "columnC" : [0, 42, 0, 6, 0, 42, 42, 34]}

df = pd.DataFrame(data1)

print(df)
# print(df.columnC ==0)

# print(df.columnB[(df.columnC >= 1)&(df.columnC<=40)])
def f(x):
	print((df.columnC > x)&(df.columnC< x+40))
	ser = df.columnB[(df.columnC > x)&(df.columnC< x+40)]
	# print(ser)
	return ser.sum()
df['result'] = df.columnC.apply(f)
print(df)

```
行操作：
> f=lambda x:x.max()-x.min()

> #默认对每一列应用
> dataframe.apply(f)

> #如果需要对每一行分组应用
> dataframe.apply(f,axis=1)

6.逐行操作：
> DataFrame.pct_change(periods=1, fill_method='pad', limit=None, freq=None, **kwds) 
> DataFrame.shift()
> freq 是在Index为Timestamp的情况下，可设为'M'或BDay()等

7.[pandas](http://blog.csdn.net/suzyu12345/article/details/50733932)
8. python [rolling包](http://blog.csdn.net/xxzhangx/article/details/76938053?locationNum=2)
9.list操作 
9.1 求交、并、差集
> # intersection
> intersection = list(set(a).intersection(set(b)))
> # union
> union = list(set(a).union(set(b)))
> # difference
> difference = list(set(a).difference(set(b)))

10.numpy
1) np.func.accumulate(array),从第一个逐两个求func
2) comprod累乘，comsum累加
3）multiply函数得到的结果是对应位置上面的元素进行相乘。x1=[1,2,3];x2=[4,5,6] ;print multiply(x1,x2)



11.作图
   matplotlib:
   1) ax2 = twinx()添加一个坐标轴
   2) ax2.set_ylim() 坐标范围，ax2.fill_between(index,0,np.array(),color=,alpha = 1)
   3) ax2.set_title()
   4) ax2.set_yticklabels([str(x*100)+'0%' for x in ax1.get_yticks()], fontproperties=font, fontsize=14)
   Seaborn:
   其实是在matplotlib的基础上进行了更高级的API封装，从而使得作图更加容易，在大多数情况下使用seaborn就能做出很具有吸引力的图。
   1) distplot( )为hist加强版，kdeplot( )为密度曲线图 
   三维作图：
   # plotting a 3D scatter plot
   from mpl_toolkits.mplot3d import Axes3D
   fig = plt.figure(figsize=(12,9))
   ax = fig.add_subplot(111, projection = '3d')
   ax.scatter(X['width'], X['height'], X['mass'], c = y, marker = 'o', s=100)
   ax.set_xlabel('width')
   ax.set_ylabel('height')
   ax.set_zlabel('mass')
   plt.show()

12.pandas
   1) df.ix:它允许我们混合使用下标和名称进行选取。 可以说它涵盖了前面所有的用法。基本上把前面的都换成df.ix 都能成功，但是有一点，就是df.ix [ [ ..1.. ], [..2..] ],  1框内必须统一，必须同时是下标或者名称，2框也一样。 BTW， 1框是用来指定row，2框是指定column， 当然上面所有的取数方法都是这个规则。
   2) df['列名'][index]


13.量化指标
   1) pretreat_data.ix[dt_str1] = pd.Series(standardize(neutralize(winsorize(factor_df.ix[dt_str1].to_dict())))) 标准化，中性化，去极值


14.[较好的文章推荐](https://uqer.io/community/share/5987d4a7bce0050108892cfc)
[期权文章](https://xueqiu.com/5557079529/79821083)
