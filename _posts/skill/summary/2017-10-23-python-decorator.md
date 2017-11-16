---
layout: post
title: "python装饰器"
date: 2017-09-27 18:00:00 +0800 
categories: 酱油人生
tag: python decorator
---
* content
{:toc}

### 什么是装饰器
[装饰器](http://python.jobbole.com/81683/)

> 装饰器是对函数的封装，然后通过@语法简化操作。继承是算面向对象，所以两者不同。打个比方，我希望每个函数在执行的时候打印个日志信息，常规做法是定义个logging函数，然后logging(func())，使用装饰器就是在func()上面直接使用@logging。

### 装饰器常用场景：
* 引入日志
* 增加计时逻辑来检测性能
* 给函数加入事物能力。

### 使用方法举例说明

```python
	from django.contrib.auth.decorators 
	import login_required

    @login_required
	def view_db2(request):
	    lists = Db2Database.objects.all()
	    return render(request, 'database/db2.html', {'lists': lists, 'DSM_URL': DSM_URL})

```
以上这个实例事我们事先定义权限认证函数login_required，这里在调用view_db2(request）的时候会自动调用login_required函数执行权限认证。

```python

    class MyClass(obj):
    @staticmethod
    def staticFoo():
    	...

```
这里的staticmethod也是我们事先定义好的一个函数，实现将函数转换为静态函数，然后调用声明staticFoo()为静态方法

## decorator的应用
1. 建立日志跟踪记录日志及错误日志

``` python
#coding=utf-8
@author: sunying
@file: exception_logger.py
@time: 2017/11/16 15:43
@description: 
    Creates a logging object and returns it
@param logger: The logging path to store the log info
import logging
def create_logger(log_path,lable):

    logger = logging.getLogger(lable)
    logger.setLevel(logging.INFO)
 
    # create the logging file handler
    fh = logging.FileHandler(log_path)
 
    fmt = '%(asctime)s - %(name)s - %(levelname)s - %(message)s'
    formatter = logging.Formatter(fmt)
    fh.setFormatter(formatter)

    # add handler to logger object
    logger.addHandler(fh)
    return logger
```
```python

@author: sunying
@file: exception_dector.py
@time: 2017/11/16 18:43
@description: 
    A decorator that wraps the passed in function and logs 
    exceptions should one occur
@param logger: The logging object
 
import functools
 
def exception(logger):
    def decorator(func):
 
        def wrapper(*args, **kwargs):
            try:
                # print "Noerror",func.__name__
                info = "Sucess"+func.__name__
                info += "%s,%s"%(args,kwargs)
                logger.info(info)
                return func(*args, **kwargs)             
            except:
                # log the exception
                err = "There was an exception in  "
                err += func.__name__
                logger.exception(err)
            # re-raise the exception
            raise
        return wrapper
    return decorator
```
``` pythons

#test.py
from  uniontools import exception_decor 
from  uniontools import exception_logger

log_path = './test.log'
lable = "IndexTrade"

logger = exception_logger.create_logger(log_path,lable)
exception = exception_decor.exception
@exception(logger)
def zero_divide(a,b,c):
    float(a) / float(b)

if __name__ == '__main__':
    zero_divide(1,2,3)
```