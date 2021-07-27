# python中的语句
python语句包括赋值语句，分支语句，循环语句等。  
语句通常是一行一条，如果需要一行多条的话需要在语句末尾加分号。  
如果一条语句过长我们也可以使用续行符来`\`跨行表示。  
需要注意的是，**python中的语句是严格注意缩进的！**(解决C/C++中的悬空else问题)。  
## 赋值语句
基本形式是“变量=值”的形式。  
```python
>>> x=1
>>> y=2
>>> k=x+y
>>> x
1
>>> y
2
>>> k
3
```
### 序列赋值
```python
>>> x,y=4,8
>>> x
4
>>> y
8
>>> a,b="34"
>>> a
'3'
>>> b
'4'
```  
> 关于序列赋值：
> 序列赋值的本质是等号右边给一个序列容器,使得序列左边的变量和右边的变量一一对应赋值。
> `x,y=4,8`实际上是把4,8看作了(4,8),即一个元组。
> 我们也可以写成`x,y=[4,8]`,效果是一样的
> 注意序列赋值时，两边序列容器中的元素个数必须一致否则会报错。  
```python
>>> i,j=[1,2,3]
Traceback (most recent call last):
  File "<pyshell#18>", line 1, in <module>
    i,j=[1,2,3]
ValueError: too many values to unpack (expected 2)
```  

>小技巧：在python中可以使用序列赋值来进行swap  
```python
>>> a=4;b=8
>>> a,b=b,a
>>> a
8
>>> b
4
```  
  

### 多变量赋值（即连等）  
```python
>>> a=b=c=5
>>> print(a,b,c)
5 5 5
```
## 分支语句  
```python
if 逻辑表达式:
	语句块1
else:
	语句块2  
```
多分支用elif代替else if。  
这个没啥好说的。  
**这里要再次强调一下Python要严格注意缩进问题!**
## 循环语句
### while语句
```python
while(BOOL):
    语句块
```
while语句可以使用break退出，continue重新开始。
例如
```python
while(True):
    x=int(input())
    if(x!=-1):
        sum+=x
    elif(x==0):
        continue
    else:
        break
```
### for语句
```python
for variable in 序列:
	语句块
```
例如:  
```python
>>> s="hello,world"
>>> for i in s:
	print(i,end='')	
hello,world
```
有时为了方便产生序列我们引入range函数
#### range函数  
`range(start,stop,step)`  
- start:计数从start开始。默认是从0开始。  
例如:range(5)等价于range(0,5)
- stop:计数到stop结束，但不包括stop。  
例如:list(range(0,5))是[0,1,2,3,4]没有5  
- step:步长，默认为1。  
例如:range(0,5)等价于range(0,5,1)  

注意range的返回值并不为序列，而是iterable，（具体是什么我暂时也不是很清楚，只知道可以在for循环中迭代使用，其他情况下只有变成列表才管用），如果想当成list使用，需要用list()强制转换。  
```python
>>> list(range(10))
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> list(range(1,10))
[1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> list(range(1,10,4))
[1, 5, 9]
>>> list(range(0,-10,-1))
[0, -1, -2, -3, -4, -5, -6, -7, -8, -9]
```
#### for-else语句
python中提供了判断程序是用break跳出还是正常退出的语句。  
如果程序正常退出则执行else。  
break,return退出循环，则不执行else语句。  
```python
x=int(input())
for i in range(1,10):
    if(i>x):
        break
else:
        print("x>9")
```
## 异常处理语句
```python
try:
    语句块1
except 异常类型1:
    语句块2
except 异常类型2:
....
except:
    语句块3
else:
    语句块4
finally:
    语句块5
```
- 如果try里的语句块发生了异常就根据异常执行相应except中的语句。  
- 如果except后面没有异常类型则包含所有异常类型。  
- 如果没有异常就执行else。  
- 无论有没有异常都指向finally。  
### 异常类型
异常名称|描述
--|--
BaseException|所有异常的基类
SystemExit|解释器请求退出
KeyboardInterrupt|用户中断执行(通常是输入^C)
Exception|常规错误的基类
StopIteration|迭代器没有更多的值
GeneratorExit|生成器(generator)发生异常来通知退出
StandardError|所有的内建标准异常的基类
ArithmeticError|所有数值计算错误的基类
FloatingPointError|浮点计算错误
OverflowError|数值运算超出最大限制
ZeroDivisionError|除(或取模)零 (所有数据类型)
AssertionError|断言语句失败
AttributeError|对象没有这个属性
EOFError|没有内建输入,到达EOF 标记
EnvironmentError|操作系统错误的基类
IOError|输入/输出操作失败
OSError|操作系统错误
WindowsError|系统调用失败
ImportError|导入模块/对象失败
LookupError|无效数据查询的基类
IndexError|序列中没有此索引(index)
KeyError|映射中没有这个键
MemoryError|内存溢出错误(对于Python 解释器不是致命的)
NameError|未声明/初始化对象 (没有属性)
UnboundLocalError|访问未初始化的本地变量
ReferenceError|弱引用(Weak reference)试图访问已经垃圾回收了的对象
RuntimeError|一般的运行时错误
NotImplementedError|尚未实现的方法
SyntaxError|Python 语法错误
IndentationError|缩进错误
TabError|Tab 和空格混用
SystemError|一般的解释器系统错误
TypeError|对类型无效的操作
ValueError|传入无效的参数
UnicodeError|Unicode 相关的错误
UnicodeDecodeError|Unicode 解码时的错误
UnicodeEncodeError|Unicode 编码时错误
UnicodeTranslateError|Unicode 转换时错误
Warning|警告的基类
DeprecationWarning|关于被弃用的特征的警告
FutureWarning|关于构造将来语义会有改变的警告
OverflowWarning|旧的关于自动提升为长整型(long)的警告
PendingDeprecationWarning|关于特性将会被废弃的警告
RuntimeWarning|可疑的运行时行为(runtime behavior)的警告
SyntaxWarning|可疑的语法的警告
UserWarning|用户代码生成的警告