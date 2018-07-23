---
layout: post
title: "python代码规范"
date: 2017-11-15 18:00:00 +0800 
categories: 酱油人生
tag: python
---
* content
{:toc}

<!-- more -->

---
## 关于python中带下划线的变量和函数的意义
[参考](http://blog.csdn.net/AI_S_YE/article/details/44685139?ref=myread)

### 1. 变量
**常量** : 大写加下划线 : USER_CONSTANT 对于不会发生改变的全局变量，使用大写加下划线。

**私有变量** : 小写和一个前导下划线 :_private_value
Python 中不存在私有变量一说，若是遇到需要保护的变量，使用小写和一个前导下划线。但这只是程序员之间的一个约定，用于警告说明这是一个私有变量，外部类不要去访问它。但实际上，外部类还是可以访问到这个变量。
**内置变量** : 小写，两个前导下划线和两个后置下划线: __class__两个前导下划线会导致变量在解释期间被更名。这是为了避免内置变量和其他变量产生冲突。用户定义的变量要严格避免这种风格。以免导致混乱。

### 2. 函数和方法
总体而言应该使用，小写和下划线。但有些比较老的库使用的是混合大小写，即首单词小写，之后每个单词第一个字母大写，其余小写。但现在，小写和下划线已成为规范。

**私有方法** ： 小写和一个前导下划线
``` python
def _secrete(self):
    print "don't test me."
```
这里和私有变量一样，并不是真正的私有访问权限。同时也应该注意一般函数不要使用两个前导下划线(当遇到两个前导下划线时，Python 的名称改编特性将发挥作用)。特殊函数后面会提及。

**特殊方法** ： 小写和两个前导下划线，两个后置下划线
``` python
def __add__(self, other):
    return int.__add__(other)
```
这种风格只应用于特殊函数，比如操作符重载等。

**函数参数** : 小写和下划线，缺省值等号两边无空格
``` python
def connect(self, user=None):
    self._user = user
``` 

python默认的成员函数和成员变量都是公开的，并且没有类似别的语言的public,private等关键词来修饰。 在python中定义私有变量只需要在变量名或函数名前加上 "__"两个下划线，那么这个函数或变量就会为私有的了。 在内部，python使用一种 name mangling 技术，将 __membername替换成 _classname__membername，所以你在外部使用原来的私有成员的名字时，会提示找不到。 比如：

``` python
class Person:

   def __init__(self):
       self.__name = 'haha'#私有属性
       self.age = 22

   def __get_name(self):##私有方法
       return self.__name

   def get_age(self):
       return self.age

person = Person()
print person.get_age()
print person.__get_name()

```
我们这里定义的__name是私有属性，__get_name()是私有方法。在 Python 中没有什么是真正私有的；在内部，私有方法和属性的名字被忽然改变和恢复，以致于使得它们看上去用它们给定的名字是无法使用的

## 3.类的命名
类总是使用驼峰格式命名，即所有单词首字母大写其余字母小写。类名应该简明，精确，并足以从中理解类所完成的工作。常见的一个方法是使用表示其类型或者特性的后缀，例如:
> SQLEngine
> MimeTypes

对于基类而言，可以使用一个 Base 或者 Abstract 前缀
> BaseCookie
> AbstractGroup

``` python
class UserProfile(object):
    def __init__(self, profile):
        return self._profile = profile

    def profile(self):
     
        return self._profile
``` 

## 4.模块和包
除特殊模块 __init__ 之外，模块名称都使用不带下划线的小写字母。
若是它们实现一个协议，那么通常使用lib为后缀，例如:

``` python
import smtplib
import os
import sys
``` 
## 5.关于参数
1. 不要用断言来实现静态类型检测
断言可以用于检查参数，但不应仅仅是进行静态类型检测。 Python 是动态类型语言，静态类型检测违背了其设计思想。断言应该用于避免函数不被毫无意义的调用。

2. 不要滥用 *args 和 **kwargs
*args 和 **kwargs 参数可能会破坏函数的健壮性。它们使签名变得模糊，而且代码常常开始在不应该的地方构建小的参数解析器。

## 6.一些数字
**一行列数** : PEP 8 规定为 79 列，这有些苛刻了。根据自己的情况，比如不要超过满屏时编辑器的显示列数。这样就可以在不动水平游标的情况下，方便的查看代码。

**一个函数** : 不要超过 30 行代码, 即可显示在一个屏幕类，可以不使用垂直游标即可看到整个函数。

**一个类** : 不要超过 200 行代码，不要有超过 10 个方法。
一个模块 不要超过 500 行。
## 7.其他
1. 使用 has 或 is 前缀命名布尔元素
     is_connect = True
     has_member = False

2. 用复数形式命名序列
     members = ['user_1', 'user_2']
3. 用显式名称命名字典
     person_address = {'user_1':'10 road WD', 'user_2' : '20 street huafu'}
4. 避免通用名称
     诸如 list, dict, sequence 或者 element 这样的名称应该避免。
5. 避免现有名称
     诸如 os, sys 这种系统已经存在的名称应该避免。

## 8.验证脚本
可以安装一个 pep8 脚本用于验证你的代码风格是否符合 PEP8。

     easy_install pep8
     pep8 -r --ignoire E501 Test.py

这个命令行的意思是，重复打出错误，并且忽略 501 错误(代码超过 79 行)。


## 9.函数调用时带括号和不带括号的区别：
1. 不带括号时，调用的是这个函数本身 

2. 带括号（此时必须传入需要的参数），调用的是函数的return结果

## 10.类中的__dict__学习笔记
dict: 类与对象的所有成员； 
类输出的是全局的函数，变量等信息。 
对象输出的只是对象拥有的普通变量而已[关于对象](http://python.jobbole.com/83747/)

``` python
class Province:
    country = 'China'

    def __init__(self, name, count):
        self.name = name
        self.count = count

    def func(self, *args, **kwargs):
        print 'func'

print Province.__dict__
obj1 = Province('HeBei', 10000)
print obj1.__dict__
obj2 = Province('HeNan', 3888)
print obj2.__dict__
```
结果：
> {'country': 'China', '__module__': '__main__', 'func': <function func at 0x1074191b8>, '__init__': <function __init__ at 0x1074190c8>, '__doc__': None}
> {'count': 10000, 'name': 'HeBei'}
> {'count': 3888, 'name': 'HeNan'}

## 11.python 模块
在一个文件夹下建立的模块在另一个文件夹下的文件引入，在源文件夹下要建立__init__.py的构造文件初始化该文件夹中的模块