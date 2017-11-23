# python 错误的总结

* [错误和异常的概念](#错误和异常的概念)
* [python常见错误](#python常见错误)
* [try-except捕获异常](#try-except捕获异常)
* [raise语句和assert语句](#raise语句和assert语句)
* [标准异常和自定义异常](#标准异常和自定义异常)

## 错误和异常的概念
错误：  
1. 语法错误：代码不符合解释器或者编译器语法  
2. 逻辑错误：不完整或者不合法的输入或者计算出现问题  
异常：执行过程中出现问题导致程序无法执行  
1. 程序遇到逻辑或算法问题  
2. 运行过程中计算机错误（内存不够或IO错误）  

## python常见错误
1. NameError：变量没有定义直接引用  
2. SyntaxError：语法错误  
3. IOError：io错误
4. ZeroDivisionError：除0的错误  
5. ValueError：强制类型转换时可能出现  

## try-except捕获异常
使用try-except捕获异常  
```
try:
    代码块
except Exception, e:
    print '打印错误信息', e
```
try-except--else
```
try:
    代码块
except Exception, e:
    print '错误信息',e
else:
    print '没有异常'
```
try--finally
```
try:
    代码块
finally:
    print '无论是否有异常都执行'
```
try-except--else--finally
```
try:
    代码块
except:
    错误信息
else:
    没有抛出错误
finally:
    最后执行，无论是否发生错误
```
```
with context [as var]:  
    with_suit
``` 
1. 用来代替try-except--finally语句，使代码更加简介
2. context表达式返回的是一个对象，要支持上下文协议
3. var用来保存context返回的对象，单个返回值或元组
4. with_suit使用var变量来对context返回对象进行操作
```
with open('1.txt') as f:
    for line in f.readlines():
        print line
```
1. 打开1.txt文件
2. f变量接收打开文件返回的对象
3. with代码块中的代码执行完，关闭文件

with语句实质上是一个上下文管理：  
1. 上下文管理协议：包含方法__enter__()和__exit__()，支持该协议的对象要实现这两个方法  
2. 上下文管理器：定义执行with语句时要建立的运行时上下文，负责执行with语句上下文中的进入和退出操作  
3. 进入上下文管理器：调用管理器的__enter__方法，如果设置as var语句，var变量接收__enter__方法返回值  
4. 退出上下文管理器：调用管理器的__exit__方法  

with语句的操作场景：  
1. 文件操作
2. 进程线程之间的互斥对象，例如互斥锁
3. 支持上下文的其他对象

## raise语句和assert语句
raise语句：用于主动抛出异常  
raise [exception[,args]]  
exception:异常类  
args:描述异常信息的元组  
例如：
```
raise IOError, "File Not Exit"
```
assert语句：断言语句，用于检测表达式是否为真，如果为＋，引发AssertionError错误  
assert expression [, args]  
expression:表达式  
args:判断条件的描述信息  

## 标准异常和自定义异常
标准异常：python内建异常，程序执行前就已经存在  
BaseException  
    KeyboardInterrupt(用户中断，ctrl+c)  
    Exception(常见错误的基类)  
        SyntaxError,NameError,IOError,ImportError...  
    SystemExit(Python解释器退出)  
自定义异常：
1. python允许自定义异常，用于python中没有涉及到的异常情况  
2. 自定义异常必须继承Exception类  
3. 自定义异常只能主动触发  
