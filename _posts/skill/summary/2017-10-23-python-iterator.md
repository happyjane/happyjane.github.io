---
layout: post
title: "python迭代器&生成器"
date: 2017-12-06 22:00:00 +0800 
categories: 酱油人生
tag: python 迭代器 & 生成器
---
* content
{:toc}

<!-- more -->

## 迭代器 [ iter()和__iter__ ]
> 所谓的迭代器就是具有next方法（这个方法调用不用参数）的对象。next方法返回他的下一个值。如果next方法被调用，迭代器没有值可以返回就会返回一个StopIteration异常。（python 3中next方法为__next__）

### 为什么用迭代器
> 迭代器比列表节省很多内存空间，在使用迭代器计算的时候计算一个值获取一个值，而列表则是一次性把所有值都获取到；
> 使用迭代器可以让代码更优雅；
> 可以迭代不是序列但表现出序列行为的对象。

### 迭代器怎么用？

``` python

#!/usr/bin/env python
#coding=utf-8
#斐波那契数列

class Fib(object):
  def __init__(self):
    self.a,self.b = 0,1
  def __iter__(self):
    return self #实例本身就是迭代对象，所以返回自己
  def next(self): # next 属性是迭代器必有的方法，但具体实现没有定义，所以在使用迭代器的过程中必须对其进行定义。迭代器所实现的不同功能就在于此next的定义方式的不同
    self.a,self.b = self.b,self.a+self.b#计算下一个值
  if self.a > 10:
    raise StopIteration();
  return self.a # 返回下一个值

if __name__ == '__main__':
  for n in Fib():
    print n

#倒序列排列

class Reverse:
    def __init__(self, data):
        self.data = data
        self.index = len(data)

    def __iter__(self):
        return self
        
    def next(self):       
        if self.index == 0:
            raise StopIteration
        self.index = self.index -1
        return self.data[self.index]
```
### 迭代器转序列
> 可以用list将迭代器显式的转化为列表。

## 生成器


> first edit 2017-12-07
