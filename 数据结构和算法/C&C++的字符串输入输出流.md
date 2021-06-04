### 问题引入
在一些题目中我们常常会遇到需要把字符串转换为数字或者把数字转换为字符串的操作，对于单个(要转化成一个整数的)字符串或者数字，我们通常使用to_string(数字转换为字符串)或者atoi(字符数组转换成数字)函数来实现。    
但是对于一些较为复杂的情况，比如：把一个字符串"01:02:03:04"中的数字(被:所分割)单独拿出来进行使用，似乎无法使用上面两个函数简单地解决。  
但是如果上面的数据在我们的console数据缓冲区(即在命令行窗口输入)似乎问题就变得简单了起来，只需要使用C中的scanf("")或者C++中的cin即可轻松解决。  
是否能把从字符串读入的情况转换为从键盘缓存区读入的情况呢？或者说我们能否把一个字符串或者字符数组看作一个输入流呢(就像文件读写那样)？  

## C中的字符串输入输出流
### sprintf(写入字符串)
把字符串想象成console的输出窗口，按照C语言的字符串格式化方法进行输入，与printf相比，只多了第一个参数(即要输出的字符串)。  
```cpp
#include<iostream>
#include<string>
using namespace std;

int main()
{
	int a = 1, b = 2;
	scanf("%d %d", &a, &b);
	char res[20];
	sprintf(res, "%d:%d", a, b);
	printf("%s", res);
}
```
程序输出
```
1:2
```
### sscanf(从字符串中读取)
把字符串想象成console的控制台缓冲区，从中按照scanf的规定格式读取，与sprintf一样，多了一个参数(即从哪个字符串读入)
```c
#include<iostream>
#include<string>
using namespace std;
int main()
{
	char in[25] ="0:1:2:3";
	int a, b, c, d;
	sscanf(in, "%d:%d:%d:%d", &a, &b, &c, &d);
	printf("%d %d %d %d", a, b, c, d);
}
```
程序输出
```
0 1 2 3
```
## C++中的字符串输入输出流
与C语言使用scanf和printf进行读入和输出不同，C++ 的读入和输出则依赖istream对象和ostream对象，并且在标准库中定义了标准输入流cin(即从键盘读入)，标准输出流cout(即打印到console窗口中)。  
因此C++的文件输入输出流和字符串输入输出流也延续了这一风格，使用istringstream来从字符串中读入，使用ostringstream来输出数据到字符串。  
这写字符串输出输出流对象包含在头文件sstream中，主要有istringstream，ostringstream和stringstream。其中stringstream包含istringstream和ostringstream的功能(istringstream只能读，ostringstream只能写，而stringstream既可以读也可以写)。因此我们这里只介绍stringstream的用法。  
### 成员函数
#### 构造函数
```
stringstream(string val)
```
初始化并把string作为stringstream的流内容。
```cpp
#include<iostream>
#include<sstream>
#include<string>
using namespace std;

int main()
{ 
	string a = "hello world 1 2";
	stringstream s(a);
	string b, c;
	int d, e;
	s >> b >> c >> d >> e;
	cout << b << " " << c << " " << d << " " << e;
}
```
程序输出
```
hello world 1 2
```
#### str函数
```
str(string val)
```
改变stringsteam中的流内容
```cpp
#include<iostream>
#include<sstream>
#include<string>
using namespace std;

int main()
{ 
	stringstream s;
	s.str("hello world 1 2");
	string b, c;
	int d, e;
	s >> b >> c >> d >> e;
	cout << b << " " << c << " " << d << " " << e;
}
```
程序输出
```
hello world 1 2
```
> 小技巧：可以使用str("")来清空流内容。  

#### clear函数
```
clear()
```
并不是把stringstream的流内容清空，而是把标志位清空。  
> 什么是标志位  
当我们从流中读取数据时，如果读取到流的结尾，流对象会自己添加一个eofbit的标记位，标志读取结束，这个时候我们如果继续在流中写入数据是不可以的。  

如果多次使用一个stringstream，反复进行operator>>和operator<<，那么必须在每次>>到stringstream的流结尾时候使用clear清空标志位。  
不使用clear连续读入读出
```
#include<iostream>
#include<sstream>
#include<string>
using namespace std;
int main()
{
	stringstream is;
	int a = 5;
	is << a;
	string b;
	is >> b;
	cout << b << endl;
	int c = 6;
	is << c;
	is >> b;
	cout << b << endl;
}
```
程序输出
```
5
5
```
使用clear
```
#include<iostream>
#include<sstream>
#include<string>
using namespace std;
int main()
{
	stringstream is;
	int a = 5;
	is << a;
	string b;
	is >> b;
	cout << b << endl;
	int c = 6;
	is.clear();
	is << c;
	is >> b;
	cout << b << endl;
}
```
程序输出
```
5
6
```