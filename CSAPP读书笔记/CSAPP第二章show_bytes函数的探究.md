CSAPP第二章中给出了一个帮助我们观察数据的位模式的函数--show_bytes函数，具体实现如下：
```C
#include<stdio.h>
typedef unsigned char *byte_pointer;

void show_bytes(byte_pointer start, size_t len)
{
    size_t i;
	for (i = 0; i < len; i++)
	{
		printf("%.2x", start[i]);
	}
	printf("\n");
}

void show_int(int x)
{
	show_bytes((byte_pointer)&x, sizeof(int));
}

void show_double(double x)
{
	show_bytes((byte_pointer)&x, sizeof(double));
}

void show_float(float x)
{
	show_bytes((byte_pointer)&x, sizeof(float));
}
```
函数是不难懂的，只要有C语言基础的应该都能看懂，所以在看懂函数后，我第一时间想自己实现一下，实现代码如下:
```C
#include<stdio.h>
typedef char *byte_pointer;

void show_bytes(byte_pointer start, size_t len)
{
	for (int i = 0; i < len; i++)
	{
		printf("%.2x", start[i]);
	}
	printf("\n");
}

void show_int(int x)
{
	show_bytes((byte_pointer)&x, sizeof(int));
}

void show_double(double x)
{
	show_bytes((byte_pointer)&x, sizeof(double));
}

void show_float(float x)
{
	show_bytes((byte_pointer)&x, sizeof(float));
}
```
写完后我立刻尝试跑了一下一个int类型的数字
```
int main(void)
{
    int x=1;
    show_int(x);
}
```
VS2017运行结果为：
![TIM截图20191119161542.png](https://i.loli.net/2019/11/19/ftuhYLXJieMzcsU.png)  
看上去是没什么问题的。于是我又试了一下浮点数的表示:
```
int main(void)
{
	float x = 1.0f;
	show_float(x);
}
```
VS2017运行结果为：
![TIM截图20191119162023.png](https://i.loli.net/2019/11/19/GncptSkRJIo47BQ.png)  
输出了14个十六进制数字，多输出了6个二进制数，即3个字节。  
这三个字节是怎么来的呢？  
通过对比发现我写的函数与书中的函数一个不同，书中的`byte_pointer`是`unsigned char*`，而我的是`char*`。  
这有什么问题呢，`char`与`unsigned char`都是一个字节，八位二进制，两位十六进制，为什么会发生多输出三个字节的情况呢。  
通过查阅，我发现问题正出在`char`与`unsigned char`中：[c语言中 char* 和 unsigned char* 的区别浅析](https://blog.csdn.net/guotianqing/article/details/77341657)。  
具体原因是这样的：  
C语言中虽然没有具体说明char有无符号，但是大多数机器上char都是有符号的，而printf中格式输出%.2x的过程为：先把char类型转换为int类型，这就涉及到了位的扩展，而有符号数的位扩展所遵循的是--‘符号扩展’具体见我的新博客~。  
所以在扩展时，如果char类型的位模式中第一位是1的话，扩展为int类型，需要在前面加三个字节24位的1，printf时实际精度超过了.2x，自然就在这个字节的前面加了六个f。  