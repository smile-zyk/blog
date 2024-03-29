# 容器概念
容器是Python中的重要概念，分为有序与无序。  
有序容器也称为序列类型容器，如：字符串、列表。  
# 序列容器
## 通用序列容器操作  
### 容器连接+
加号可以把两个序列连接成一个更大的容器，相加后两个序列的值并不改变
```python
>>> s1='abc'
>>> s2='def'
>>> s3=s1+s2
>>> s3
'abcdef'
>>> s1
'abc'
>>> s2
'def'
>>> l1=[1,2,3]
>>> l2=[4,5,6]
>>> l3=l1+l2
>>> l3
[1, 2, 3, 4, 5, 6]
>>> l1
[1, 2, 3]
>>> l2
[4, 5, 6]
```
### 数乘
一个序列容器乘以一个整数，把序列重复整数遍。相乘后原序列依然不发生变化。    
```python
>>> s1='ab'
>>> s2=s1*3
>>> s2
'ababab'
>>> l1=[1,2]
>>> l2=l1*3
>>> l2
[1, 2, 1, 2, 1, 2]
```
### in与not in
in判断一个元素是否在序列容器中，not in判断是否不再序列容器中，返回值为布尔类型。  
```python
>>> s1='abc'
>>> 'a'in s1
True
>>> 'ab'in s1
True
>>> 'd' in s1
False
>>> l1=[1,2,3]
>>> 1 in l1
True
>>> [1,2] in l1#错误因为[1,2]不在[1,2]中
False`
>>> [1,2] in [[1,2],3]#正确
True
```
### 索引[]
取单个元素，从0开始计数。  
我们一个称第一个元素为第一个，第零号。  
最大下标为长度减一，超过此范围会报错。  
我们也可以倒着数，最后一个元素为-1，第一个元素为长度的负数。  
列表的索引支持重新赋值，字符串不支持    
```python
>>> l=[1,2,3]
>>> l[1]=3
>>> l
[1, 3, 3]
>>> s="abc"
>>> s[1]="c"
Traceback (most recent call last):
  File "<pyshell#4>", line 1, in <module>
    s[1]="c"
TypeError: 'str' object does not support item assignment
```
### 切片[]
在一个序列容器l中，有l[a:b]其中a<b，（若a>b，l[a:b]为空串）  
l[a:b]=l[a]+l[a+1]+......+l[b-1]。（若a=0，a可以省略）  
在切片中依然可以只用负数索引，并且有时可以做到一些直接索引不好做的操作。  
如，我们要把一个数字+一个字符的串中的最后一个字符去掉，直接使用切片似乎不太好处理，因为我们无法确定数字的长度。  
这时我们可以使用[0:-1]，我们切刀的第一个元素到倒数第二个元素。巧妙地解决了这个问题。  
```python
>>> s="25c"
>>> s[:-1]
'25'
```
(注意，如果序列容器中，我们可以在切片中使用长度（这似乎看上去并不合理），这是为了解决无法切片得到最后一个元素的问题，但我们通常不推荐这么做，我们通常使用省略最后一个切片范围的方法来使得切片取到最后一个字符)  
## 通用序列容器函数
### len函数
获得序列容器的长度。  
### min函数
获得序列容器中最小的元素。  
### max函数
获得序列容器中的最大元素。
### sort函数
排序函数，按照ASC码顺序排序。  
## 字符串
### 字符串中的引号与转义
如果需要在字符串中使用单引号，我们可以使用双引号包裹。  
如果需要在字符串中使用双引号，我们可以使用单引号包裹。  
```python
>>> a="'a'+'b'"
>>> a
"'a'+'b'"
>>> a='"a"+"b"'
>>> a
'"a"+"b"'
```
也可以使用反斜杠（左上到右下）做转义。  
```python
>>> a="\'a\'+\'b\'"
>>> a
"'a'+'b'"
```
三个单引号或者三个双引号，可以使字符串保留回车。  
```python
>>> """
a
cacad
casdw
,
"""
'\na\ncacad\ncasdw\n,\n'
```
如果想在输出时在多行书写，但同时最后的结果不会换行，可以在行末加反斜杠。  
```python
>>> s="adad\
vasd\
avasddaw\
,\
"
>>> print(s)
adadvasdavasddaw,
```
如果想使输入时的字符，不被识别成转义字符，我们可以在引号前面加一个r。  
```python
>>> s=r'a\ndjwaid\tdad'
>>> s
'a\\ndjwaid\\tdad'
>>> print(s)
a\ndjwaid\tdad
```
### 字符串特有函数（方法）
#### lower和upper
把大写变成小写，不会改变原来字符串
```python
>>> s="ADADWDADS"
>>> s.lower()
'adadwdads'
>>> s
'ADADWDADS'
```
upper是把小写变成大写，使用方法与lower一致。  
#### find
find("s",a,b)从左往右数第一次在字符串的[a,b-1]范围中出现的位置。  
如果找不到则返回-1  
```python
>>> s.find("p",0,2)
-1
>>> s.find("p",0,3)
2
```
#### count
count('s')计算s在字符串中出现的次数。  
```python
>>> s="hello,world"
>>> s.count('l')
3
```
#### strip、lstrip、rstrip
strip去掉左右两边空格，lstrip去掉左边空格，rstrip去掉右边空格。  
```python
>>> s=' hello world    '
>>> s.strip()
'hello world'
>>> s.lstrip()
'hello world    '
>>> s.rstrip()
' hello world'
```
#### replace
replace('s1','s2')把字符串中的's1'替换成's2'  
```python
>>> s=' hello world '
>>> s.replace(' ','-')
'-hello-world-'
```
#### format
str.format()  
```python
>>> x=3.14159
>>> y=2*x*3
>>> print("{0:.2f} {1:.2f}".format(x,y))
3.14 18.85
```
0和1表示format函数中的第一和第二个参数  
.2f表示小数部分保留两位，四舍五入。  
格式化的方法与C/C++一致。  
#### %
字符串的格式化，类似于C/C++中，不同的是后面也要用%，如`print("%d+%f"%(1,1.2))`，这里略。  
## 列表
列表中的元素由中括号构成包裹
### list函数
list()可以将其他类型转换成列表
```python
>>> s="this is a string"
>>> list(s)
['t', 'h', 'i', 's', ' ', 'i', 's', ' ', 'a', ' ', 's', 't', 'r', 'i', 'n', 'g']
```
### 列表的特性
#### 1.列表的字面是可以是表达式
```python
>>> a=6
>>> b=8
>>> [a,b]
[6, 8]
>>> [a+2,b-a]
[8, 2]
```

#### 2.如果列表的元素还是一个列表，就形成了广义表
```python
>>> t=[[1,2,3],[4,5,6],[7,8,9]]
>>> len(t)
3
>>> t[0]
[1, 2, 3]
>>> t[0][0]
1
```
#### 3.列表的赋值并不重分配空间
列表的赋值并不重分配空间，只是把新变量的指针也指向原来的变量指向的地址。这导致了，改变被赋值的变量会导致原变量被修改，这与其他变量的赋值不同。  
```python
>>> t=[1,2,3]
>>> t[0]
1
>>> l=t
>>> l[0]
1
>>> l[0]=2
>>> l
[2, 2, 3]
>>> t
[2, 2, 3]
```
如图：
![TIM截图20191024145718.png](https://i.loli.net/2019/10/24/WFH7GebsiBSTjvR.png)
##### 列表切片的其他应用
为了解决上面的问题，我们可以使用切片
如果想要重新分配一个空间来让新变量拥有可以使用切片的方法。  
```python
>>> t1=[1,2,3]
>>> t2=t1[:]#省略开头结尾，表示从0开始一直到结束
>>> t2[0]=0
>>> t1
[1, 2, 3]
>>> t2
[0, 2, 3]
```
如图：  
![TIM截图20191024150113.png](https://i.loli.net/2019/10/24/F84zUpxXSDMmjrk.png)
使用切片时，如果切片在赋值号右边，那么它会给左边的变量分配新的空间，  
如果在左边，那么它指向的是原来的空间，所以可以通过改变切片的值来改变原来的空间。   
```python
>>> t=[1,2,3,4,5,6,7,8,9,10]
>>> ts=t[2:4]
>>> t[2:4]=[10,20]
>>> ts
[3, 4]
>>> t
[1, 2, 10, 20, 5, 6, 7, 8, 9, 10]
```
如图：  
![TIM截图20191024151451.png](https://i.loli.net/2019/10/24/frTKWokxj6mIulc.png)  
甚至可以赋与切片中元素个数不同的列表。  
```python
>>> t[2:4]=[10,20,30]
>>> t
[1, 2, 10, 20, 30, 5, 6, 7, 8, 9, 10]
```
我们也可以利用这一特性来删除元素
```python
>>> t[2:4]=[]#删除第二个第三个元素。  
>>> t
[1, 2, 30, 5, 6, 7, 8, 9, 10]
```
#### del运算符
在del后面加上要删除的元素，即可在列表中删除这一元素。  
如果要删除整个列表，可以直接del+列表名即可。  
```python
>>> t=[1,2,3,4,5,6]
>>> del t[2]
>>> t
[1, 2, 4, 5, 6]
>>> del t
>>> t
Traceback (most recent call last):
  File "<pyshell#16>", line 1, in <module>
    t
NameError: name 't' is not defined
```
### 列表的特有函数
#### append
相当于C++中STL的push_back，把一个新的元素添加的列表的最后。  
#### extend
相当容器连接运算符+，把两个列表连接起来。  
（注意：append与extend看似内容相似，实际上功能上还是有着很大的差异，append是添加元素，它的参数应该为一个字面量或者表达式，而extend的作用是扩展列表，连接两个列表，后面的参数必须也是一个列表）  
```
>>> t=[1,2,3,4,5,6,7,8]
>>> t.append(10)
>>> t
[1, 2, 3, 4, 5, 6, 7, 8, 10]
>>> t.extend([1,2,3])
>>> t
[1, 2, 3, 4, 5, 6, 7, 8, 10, 1, 2, 3]
>>> t.append([1,2,3])#这是正确的因为列表也是一个字面量
>>> t
[1, 2, 3, 4, 5, 6, 7, 8, 10, 1, 2, 3, [1, 2, 3]]
>>> t.extend(1)#下面报错，因为参数不为列表
Traceback (most recent call last):
  File "<pyshell#25>", line 1, in <module>
    t.extend(1)
TypeError: 'int' object is not iterable
```
#### insert函数
insert函数有两个参数，第一个参数指定在哪个元素前面插入(0~INF)，第二个元素指定要插入的元素（字面量或者表达式）  
```python
>>> t=[1,2,3,4,5,6,7]
>>> t.insert(0,0)
>>> t
[0, 1, 2, 3, 4, 5, 6, 7]
>>> t.insert(0,[1,2])
>>> t
[[1, 2], 0, 1, 2, 3, 4, 5, 6, 7]
```
当insert的第一个参数超过了列表的最大下标时，我们会把元素添加到列表尾部。  
```python  
>>> t=[1,2,3,4,5,6]
>>> t.insert(100,1)
>>> t
[1, 2, 3, 4, 5, 6, 1]
```
#### remove函数
删除元素，与del运算符不同的是，del是删除指定位置的元素，remove是删除指定值(第一个)的元素。
如果有很多指定值，那么删除第一个。  
```python
>>> t=[1,2,3,4,5,6,2]
>>> t.remove(2)
>>> t
[1, 3, 4, 5, 6, 2]
```
#### pop函数
与数据结构中堆栈的pop一致，即弹出最后一个元素，函数的返回值为该元素的值。  
如果该函数带有参数，那么弹出的值为该位置元素的值。  
```python
>>> t=[1,2,3,4,5,6,7,8]
>>> t.pop()
8
>>> t.pop(2)
3
>>> t
[1, 2, 4, 5, 6, 7]
```
#### reverse函数
翻转列表，没有什么好说的。  
```python
>>> t=[1,2,3]
>>> t.reverse()
>>> t
[3, 2, 1]
```
#### index函数
与字符串的find函数一致，返回指定元素在列表中的位置，如果有多个就返回第一个。  
与find函数基本一致
```python
>>> t=[1,3,4,5,7,3,4,24]
>>> t.index(4,3,9)
6
>>> t.index(4)
2
>>> t.index(4,3)
6
```
### 列表推导式
列表推导式（又称列表解析式）提供了一种简明扼要的方法来创建列表。  
它可以将循环和条件判断结合，从而避免语法冗长的代码，同时提高程序性能。  
基本格式：  
`[expression for item in iterable]`  
如，我们要产生2,4,6,8,10的列表可以使用  
`n1=[2*n for n in [1,2,3,4,5]]`  
#### 带条件的列表解析  
`[expression for item in iterable if condition]`  
`[expression if condition else expression for item in iterable]`  
```python
>>> l=[n for n in range(1,8) if n%2==1]
>>> l
[1, 3, 5, 7]
```
例如：求1-1/2+...-1/20之和  
```python
>>> a=sum([1/i if i%2==1 else -1/i for i in range(1,21)])
>>> a
0.6687714031754279
```
## 列表与字符串的转换
### split函数
字符串的成员函数，默认无参时把字符串按空格分隔成列表。  
```python
>>> s="this is a string"
>>> s.split()
['this', 'is', 'a', 'string']
```
带参数时按照参数分隔。  
```python
>>> s="12:35"
>>> s.split(":")
['12', '35']
```
### join函数
字符串的成员函数把一个列表按照某个字符串来作为连接，格式为s.join(l)，其中s为连接的字符串，l为列表。  
```python
>>> l=["hello","world"]
>>> "-".join(l)
'hello-world'
```
## 元组
与列表基本一样，但是元组是用圆括号包裹的。并且元组中的元素不能被改变（可以看出C/C++中的const string)!  
元组与字符串一致都不支持元素的重新赋值。  
元组可以使用除了修改元素的所有的列表的函数。  
一般不加括号的容器默认为元组。  
```python
>>> a,b=3,4
>>> a
3
>>> b
4
>>> p=3,4
>>> p
(3, 4)
```
### tuple函数
可以用tuple函数把其他容器转化为元组。  

# 非序列容器(无序容器)
非序列容器不支持索引、切片等等上面所提到的序列容器操作。  
主要包括有字典、集合。  
非序列容器的无序并不是指容器中的元素完全没有顺序，而是指容器中元素的顺序完全不能由程序员指定。

## 集合
在python中集合被大括号所包裹。
同时,和数学中的集合一样,集合中具有元素唯一性，确定性，无序性。
```python
>>> s={1,2,2,3,4}
>>> s
{1, 2, 3, 4}
```


# 随机库random
使用随机函数前需要`import random`。  
## 设置随机数种子
`seed(int a)`
相同种子获得的随机数是相同的，可以借此来完成一些特殊的任务。
## shuffle函数
`random.shuffle(t)`
把容器t随机打乱。  
```python
>>> import random
>>> t=["zyk","zjc","ysy","xhm"]
>>> random.shuffle(t)
>>> t
['ysy', 'xhm', 'zyk', 'zjc']
>>> random.shuffle(t)
>>> t
['xhm', 'zjc', 'zyk', 'ysy']
```
其他函数详见:[python--随机函数（random,uniform,randint,randrange,shuffle,sample）](https://www.cnblogs.com/LoongitArt/p/9885595.html#commentform
)  