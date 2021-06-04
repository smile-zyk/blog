# python数据类型
## 数字类型
### 整数（int）
与数学中整数概念一致（数字大小没有限制，这和其他语言不同），整数可正可负，默认情况下，整数采用十进制。其他进制需要增加相应的引导符号。  
如果是二进制在前面加上0b或者0B即可，如果是八进制在前面加上0o或者0O即可，如果是十六进制在前面加上0x或者0X即可。  
### 浮点数（float）
与数学中的实数概念一致，取值范围与精度都有限制。  
表达方式：  
1.小数：1.23，3.14，-9.01  
2.科学计数法：1.23e9，1.2e-5  
浮点数运算存在不确定位数，有误差，这是由于计算机用二进制存储浮点数造成的。  
如果要消除位数可以使用round函数。  
该函数原型为：`round(number,ndigit=none)`  
### 复数（complex）
与数学中的复数概念一致。  
由实部和虚部组成，虚部用j表示。  
例如：2+3j，2为实部，3j为虚部。  
real方法取实部，imag方法取虚部。  
complex(real,imag)函数可以用于创建一个职位real+imag*j的复数。  
### 与数字有关的运算符  
python只支持加减乘除和幂运算。
与其他语言不同的是，python的整数除法与浮点数除法是分开的。其中：  
/为浮点数除法，结果为小数。  
//为整数除法，结果为整数，向下（左）取余。  
另外python提供了幂运算，符号为**，它的优先级高于乘除和加减。  
python不支持自增自减。
注意python中的--i与++i不是自增自减操作，详见：[python开发_++i,i += 1的区分](https://www.cnblogs.com/hongten/p/hongten_python_operate.html
)
### 数学库（math）
e 自然常数  
pi 圆周率  
log(x[,base=e]) 返回以base为底的对数，缺省为e  
pow(x,y) 返回x的y次方    
sqrt(x) 返回x的平方根    
fabs(x) 返回x的绝对值  
round(x[,n]) 返回浮点数x的四舍五入值，n代表舍入到小数点后的位数  
divmod(x,y) 返回x和y的商和余数  
## 字符串类型
python中没有字符类型，即使是一个字符也是字符串。  
字符串是以引号括起来的任意文本，是一个有序序列  
表示形式：  
单引号：'abc'  
双引号："hello"  
三引号："'hello  
	world'"  
关于这些引号的用法详见:[Python中单引号，双引号，3个单引号及3个双引号的区别](https://blog.csdn.net/woainishifu/article/details/76105667)  
转义字符：和C/C++基本一致
### 字符串运算符
+连接字符串 \>>>'hello'+'world'  
'helloworld'  
\* 复制字符串 \>>>'ab'*3  
'ababab'    
### 字符串切片  
字符串是一个有序序列，可以是正向递增，也可以是反向递减。  
索引：在[]中给出序号  
切片：在[]中给出切片序号  
例如：  
```python
>>> a='abcdefgh'
>>> a[0]
'a'
>>> a[-8]
'a'
>>> a[1]
'b'
>>> a[1:5]
'bcde'
```
## 布尔值与关系、逻辑运算
python中提供布尔值：True、False（注意首字母大写）。  
逻辑运算和关系运算的结果是布尔值。  
注意python3中不同类型的数据不可以在一起比较。  
另外python中支持连续的关系运算，如：
`>>>1<3<5 #等价于1<3 and 3<5`  
另外与C/C++ 中不同的是，逻辑运算符，与或非为and，or，not而非&&、||、!  
另外按位与，或，异或，翻转python是支持的。  
1.与运算：A与B值均为1时，A、B与的运算结果才为1，否则为0 （运算符：&）  
2.或运算：A或B值为1时，A、B或的运算结果才为1，否则为0  （运算符：|）  
3.异或运算：A与B不同为1时，A、B的预算结果才为1，否则为0  （运算符：^）  
4.按位翻转(按位取反)：将内存中表示数字的2进制数取反0取1，1取0 （运算符：~）  
运算符优先级与C/C++一致。  
## 内置转换函数
内置函数指不需要导入类的函数
如图：  
![_M0N_V1RW_0MG08MO`T3_YP.png](https://i.loli.net/2019/10/07/u1flysvHAX2N7Oa.png)  
类型转换函数实例：  
基本格式：int(x[,base])  
```python
>>> int() #不传入参数时，得到结果0.
0
>>> int("02") #去掉0
2
>>> int("   35    ") #去掉空格
35
>>> int("35",8) #八进制
29
```
# python中的语句
python语句包括赋值语句，分支语句，循环语句等。  
语句通常是一行一条，如果需要一行多条的话需要在语句末尾加分号。  
如果一条语句过长我们也可以使用续行符来`\`跨行表示。  
需要注意的是，**python中的语句是严格注意缩进的！**(我觉得这是为了C/C++中的悬空else问题)。  
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
也可以进行序列赋值
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
注意序列赋值时，两边序列容器中的元素个数必须一致否则会报错。  
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
  

还可以进行多变量赋值（即连等）  
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
range(start,stop,step)  
start:计数从start开始。默认是从0开始。  
例如range(5)等价于range(0,5)
stop:计数到stop结束，但不包括stop。  
例如：list(range(0,5))是[0,1,2,3,4]没有5  
step:步长，默认为1。  
例如：range(0,5)等价于range(0,5,1)  
注意range的返回值并不为序列，而是iterable，（具体是什么我暂时也不是很清楚，只知道可以在for循环中迭代使用，其他情况下只有变成列表才管用），需要用list()强制转换。  
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
#### 循环中的else语句
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
如果try里的语句块发生了异常就根据异常执行相应except中的语句。  
如果except后面没有异常类型则包含所有异常类型。  
如果没有异常就执行else。  
无论有没有异常都指向finally。  
###异常类型
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
# 格式化输出
## format函数
基本格式：str.format()  
```python
>>> x=3.14159
>>> y=2*x*3
>>> print("{0:.2f} {1:.2f}".format(x,y))
3.14 18.85
```
0和1表示format函数中的第一和第二个参数  
.2f表示小数部分保留两位，四舍五入。  
格式化的方法与C/C++一致。  
除了format函数实际上还有一种方式%可以将字符串格式化，用法基本与这个一致，下节会提一下。