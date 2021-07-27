# python�е����
python��������ֵ��䣬��֧��䣬ѭ�����ȡ�  
���ͨ����һ��һ���������Ҫһ�ж����Ļ���Ҫ�����ĩβ�ӷֺš�  
���һ������������Ҳ����ʹ�����з���`\`���б�ʾ��  
��Ҫע����ǣ�**python�е�������ϸ�ע�������ģ�**(���C/C++�е�����else����)��  
## ��ֵ���
������ʽ�ǡ�����=ֵ������ʽ��  
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
### ���и�ֵ
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
> �������и�ֵ��
> ���и�ֵ�ı����ǵȺ��ұ߸�һ����������,ʹ��������ߵı������ұߵı���һһ��Ӧ��ֵ��
> `x,y=4,8`ʵ�����ǰ�4,8������(4,8),��һ��Ԫ�顣
> ����Ҳ����д��`x,y=[4,8]`,Ч����һ����
> ע�����и�ֵʱ���������������е�Ԫ�ظ�������һ�·���ᱨ��  
```python
>>> i,j=[1,2,3]
Traceback (most recent call last):
  File "<pyshell#18>", line 1, in <module>
    i,j=[1,2,3]
ValueError: too many values to unpack (expected 2)
```  

>С���ɣ���python�п���ʹ�����и�ֵ������swap  
```python
>>> a=4;b=8
>>> a,b=b,a
>>> a
8
>>> b
4
```  
  

### �������ֵ�������ȣ�  
```python
>>> a=b=c=5
>>> print(a,b,c)
5 5 5
```
## ��֧���  
```python
if �߼����ʽ:
	����1
else:
	����2  
```
���֧��elif����else if��  
���ûɶ��˵�ġ�  
**����Ҫ�ٴ�ǿ��һ��PythonҪ�ϸ�ע����������!**
## ѭ�����
### while���
```python
while(BOOL):
    ����
```
while������ʹ��break�˳���continue���¿�ʼ��
����
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
### for���
```python
for variable in ����:
	����
```
����:  
```python
>>> s="hello,world"
>>> for i in s:
	print(i,end='')	
hello,world
```
��ʱΪ�˷������������������range����
#### range����  
`range(start,stop,step)`  
- start:������start��ʼ��Ĭ���Ǵ�0��ʼ��  
����:range(5)�ȼ���range(0,5)
- stop:������stop��������������stop��  
����:list(range(0,5))��[0,1,2,3,4]û��5  
- step:������Ĭ��Ϊ1��  
����:range(0,5)�ȼ���range(0,5,1)  

ע��range�ķ���ֵ����Ϊ���У�����iterable����������ʲô����ʱҲ���Ǻ������ֻ֪��������forѭ���е���ʹ�ã����������ֻ�б���б�Ź��ã�������뵱��listʹ�ã���Ҫ��list()ǿ��ת����  
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
#### for-else���
python���ṩ���жϳ�������break�������������˳�����䡣  
������������˳���ִ��else��  
break,return�˳�ѭ������ִ��else��䡣  
```python
x=int(input())
for i in range(1,10):
    if(i>x):
        break
else:
        print("x>9")
```
## �쳣�������
```python
try:
    ����1
except �쳣����1:
    ����2
except �쳣����2:
....
except:
    ����3
else:
    ����4
finally:
    ����5
```
- ���try������鷢�����쳣�͸����쳣ִ����Ӧexcept�е���䡣  
- ���except����û���쳣��������������쳣���͡�  
- ���û���쳣��ִ��else��  
- ������û���쳣��ָ��finally��  
### �쳣����
�쳣����|����
--|--
BaseException|�����쳣�Ļ���
SystemExit|�����������˳�
KeyboardInterrupt|�û��ж�ִ��(ͨ��������^C)
Exception|�������Ļ���
StopIteration|������û�и����ֵ
GeneratorExit|������(generator)�����쳣��֪ͨ�˳�
StandardError|���е��ڽ���׼�쳣�Ļ���
ArithmeticError|������ֵ�������Ļ���
FloatingPointError|����������
OverflowError|��ֵ���㳬���������
ZeroDivisionError|��(��ȡģ)�� (������������)
AssertionError|�������ʧ��
AttributeError|����û���������
EOFError|û���ڽ�����,����EOF ���
EnvironmentError|����ϵͳ����Ļ���
IOError|����/�������ʧ��
OSError|����ϵͳ����
WindowsError|ϵͳ����ʧ��
ImportError|����ģ��/����ʧ��
LookupError|��Ч���ݲ�ѯ�Ļ���
IndexError|������û�д�����(index)
KeyError|ӳ����û�������
MemoryError|�ڴ��������(����Python ����������������)
NameError|δ����/��ʼ������ (û������)
UnboundLocalError|����δ��ʼ���ı��ر���
ReferenceError|������(Weak reference)��ͼ�����Ѿ����������˵Ķ���
RuntimeError|һ�������ʱ����
NotImplementedError|��δʵ�ֵķ���
SyntaxError|Python �﷨����
IndentationError|��������
TabError|Tab �Ϳո����
SystemError|һ��Ľ�����ϵͳ����
TypeError|��������Ч�Ĳ���
ValueError|������Ч�Ĳ���
UnicodeError|Unicode ��صĴ���
UnicodeDecodeError|Unicode ����ʱ�Ĵ���
UnicodeEncodeError|Unicode ����ʱ����
UnicodeTranslateError|Unicode ת��ʱ����
Warning|����Ļ���
DeprecationWarning|���ڱ����õ������ľ���
FutureWarning|���ڹ��콫��������иı�ľ���
OverflowWarning|�ɵĹ����Զ�����Ϊ������(long)�ľ���
PendingDeprecationWarning|�������Խ��ᱻ�����ľ���
RuntimeWarning|���ɵ�����ʱ��Ϊ(runtime behavior)�ľ���
SyntaxWarning|���ɵ��﷨�ľ���
UserWarning|�û��������ɵľ���