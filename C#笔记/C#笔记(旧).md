# C#笔记
# 基础知识
一个C#程序主要包括以下部分：  
命名空间声明（Namespace declaration）  
一个 class  
Class 方法  
Class 属性  
一个 Main 方法  
语句（Statements）& 表达式（Expressions）  
关于Main函数的一些注意事项：[C#中Main()函数为什么必须是静态的？](https://blog.csdn.net/ScapeD/article/details/79439291
)

# 数据类型、变量与常量
程序的基本任务是：对数据进行处理。  
数据分为变量（variable）与常量（literal）  
`int age=18;`  
变量的值可以改变，本质上是内存的空间，用来存储信息。   
常量的值是固定的，直接写出来，称字面常量（literal）
## 关于字面量、常量和变量有什么区别：
1. 在计算机科学中，字面量（literal）是用于表达源代码中一个固定值的表示法（notation）。几乎所有计算机编程语言都具有对基本值的字面量表示，诸如：整数、浮点数以及字符串；而有很多也对布尔类型和字符类型的值也支持字面量表示；还有一些甚至对枚举类型的元素以及像数组、记录和对象等复合类型的值也支持字面量表示法。  
2. “常量”在程序运行时，不会被修改的量。换言之，常量虽然是为了硬件、软件、编程语言服务，但是它并不是因为硬件、软件、编程语言而引入。
常量区分为不同的类型，如25、0、-8为整形常量，6.8、-7.89为实型常量，‘a’‘b’为字符常量。常量一般从其字面形式即可判断。这种常量称为字面常量或直接常量。  
3. 变量来源于数学，是计算机语言中能储存计算结果或能表示值抽象概念。变量可以通过变量名访问。在指令式语言中，变量通常是可变的；但在纯函数式语言（如Haskell）中，变量可能是不可变（immutable）的。在一些语言中，变量可能被明确为是能表示可变状态、具有存储空间的抽象（如在Java和Visual Basic中）；但另外一些语言可能使用其它概念（如C的对象）来指称这种抽象，而不严格地定义“变量”的准确外延。

## 变量命名（identifier，标识符）要遵守如下规则：  
（1）不能是C#关键字。  
（2）由字母、数组、下划线构成。  
（3）第一个字符必须是字母或下划线。  
（4）不要太长，一般不超过31个字符为宜。  
（5）变量名最好不要与库函数、类名相同。  
与C/C++ 类似，与C/C++ 一样C#是大小写敏感的。  
变量命名方法：[匈牙利命名法](https://baike.baidu.com/item/匈牙利命名法/7632397?fr=aladdin
)
## 数据类型
数据类型：本质上是数据存储方式及其能参与的运算的抽象。  
如图：    
![数据类型](https://i.loli.net/2019/10/06/jU8PQosFVvDaYcl.png)  
C#数据类型分两大类：  
1. 值类型（Value Type）  
2. 引用类型（Reference Type） 
  

前者如：int，double，Point，Size，DataTime。  
后者如：Button，Label，Book，Person。  
两者的区别在于类型是直接存储在对应的空间内，而引用类型则在对应的位置存储一个指针（或者叫引用），该指针指向对应的数据。  
任何变量都有类型。  
值类型包括：  
- 简单类型（Simple Type）  
- 结构类型（Struct Type）  
- 枚举类型（Enum Type）  

引用类型包括：
- 类类型（Class Type）  
- 接口类型（Interface Type）  
- 委托类型（Delegate）  
- 数组类型（Array Type）  
  

注意：每种简单类型都有一个关键词  
int相当于System.Int32  
double相当于System.Double  
bool相当于System.Boolean  
string相当于System.String  
（如果using System,则string相当于String）  
### 关于数据类型的一些细节  
整数类型又分为：  
- 有符号 sbyte short int long 和87L，0x1F（注：没有八进制写法）  
- 无符号 byte ushort uint ulong 如87UL  
- 字符类型 char 如'a' '\uA0B1'表示Unicode'\n'（回车）  

实数类型又分为：  
- float 如3.14F
- double 如3.14 1.5E-3 3.14D（后面这个D可以省略）
  
十进制类型  
- Decimal 如120.50M
  
布尔类型  
- bool 如true false（小写）不能用0和1代替（区别于C/C++）  

### 字符类型
char型数据用来表示通常意义上“字符”。  
字符变量是用单引号括起来的单个字符。  
`char c='A';`  
C#字符采用Unicode编码，每个字符占两个字节，因而可用十六进制编码形式表示  
`char c1='\u0061';`  
C#语言中还允许使用转义字符'\'来将后面的字符转变为其它的含义。  
`char c2='\n'; //代表换行符`  
转义字符与C语言中的类似，值得一提的是\r 与\n的不同，\r表示回车，\n表示换行。  
### 字符串类型  
是引用类型，但对字符串常量有特殊处理。  
字符串前可以使用@，加了@的字符串可以换行写，可以不进行\转义，可以换行，双引号则用两个双引号表示一个双引号。  
针对C++ 程序员来说，引用类型与值类型是由其类型定义的，而不是由其使用决定的（不存在*&这些符号类指定类型的类型）。  
### C#新版本中的特殊类型
1. 推断类型（C#3.0）  
`var a=1+2;` var表示其类型又编译器推断，而不是自己指定。  
2. Nullable类型（C#3.0）  
`int? a=32;`可以有值可以没有值，在数据库中常用。  
3. Dynamic（C#4.0）由DLR支持  
编译时不检查，运行时才确定，主要用于与COM组件或其他语言交互。

# 运算符与表达式
## 运算符
基本与C/C++类似，不赘述，多了一个字符串连接运算符：+。  
+运算符两侧的操作数中只要有一个是字符串（String）类型，系统会自动将另一个操作数转换为字符串然后在进行连接  
## 表达式
表达式是符合一定语法规则的运算符和操作数的序列。  
表达式有类型和值，对表达式中的操作数进行运算得到的结果称为表达式的值。该值的类型称为表达式的类型。  
赋值时的默认类型转换与C/C++ 的原则是一致的，值得一提的是C#中的强制类型转换：  
字符串转换成数值：  
double.Parse(s) int.Parse(s)  
数字转成字符串：  
10.ToString()  
使用方法ToString();
""+10; 使用字符连接运算符来把数字转换成字符串。  
使用Convert  
Convert.ToInt32(textbox1.Text)  
Convert.ToDouble("123.45")  
Convert.ToDateTime*("2019-10-01 14:00")  
## 流程控制语句
结构化的程序设计的三种基本流程：顺序、选择、循环。  
### 顺序语句
方法调用语句和赋值语句都为顺序语句（简单语句）
C#中没有表达式语句这一概念。  
### 分支语句
if-else与C语言的if-else一  致。
> 在VS中按Ctrl+E+D（格式文档）
按Ctrl+E+F（格式化选中部分）  

switch语句与C/C++ 不同的是，变量可以为字符串类型。  
另外如果在C#中switch语句不加break编译器会报错。  
###循环语句
循环五要素：  
初始化部分  
循环条件部分  
循环体部分  
迭代部分，我们称为“循环改变”  
结束后处理  
## C#中的数组（与C/C++大不相同）
C#中的数组是引用类型。  
以为数组的声明方式：
`int[] a1;`注意方括号写到变量名的前面  
C#中声明数组时不能指定其长度（数组中元素的个数），这与C/C++ 不一样。  
每个数组都有一个属性Length指明它的长度。  
foreach语句可以方便的处理数组、集合中的各元素。（不可以在foreach中改变数组的内容，只读式遍历）。[c#中for与foreach的使用 ](https://www.cnblogs.com/huangxuQaQ/p/10731693.html
)  
C#中的多维数组与交错数组是不同的概念，这与C/C++ 似乎不同，因为在C/C++ 中我们一般把多维数组看做数组的数组，然而在C#中只有交错数组才被看做数组的数组。  
多维数组和交错数组的区别详见:[C# 多维数组 交错数组的区别](https://www.cnblogs.com/whuanle/p/9936047.html
)  
# 面向对象的C#语言
## 类
类最基本的要素是  
字段(field)：变量  
方法(method)：函数
### 构造方法  
构造方法的主要作用是完成对象的初始化工作  
(1)构造方法的方法名与类名相同。  
(2)构造方法没有返回类型，也不能写void。  
(与C++ 类似)  
如果用户没有定义任何构造方法。  
则系统会自动产生一个默认的无参构造方法  
构造方法不能显式地直接调用，而是使用new来调用(这与C++不同)  
###析构方法  
由于C#自动进行对象的释放，所以用户一般不定义析构方法。  
### 方法的重载  
方法的签名：方法名及参数个数及类型构成（参数名不算）  
方法的重载要求方法的签名不同。  
### this
this指这个对象本身，常用于：  
（1）访问这个对象的字段及方法（VS会提示）  
（2）区分字段与局部变量  
（3）用于构造方法调用另一个构造方法，注意其位置  
## 属性（property）
存取字段的方法。（个人理解为，对get与set的封装）  
```c#
private string _name;  
public string Name
{
	get
	{
		return _name;
	}
	set
	{
		_name=value;
	}
}
```
在C#3以上中可以简写为  
`public string Name{set;get;}`  
可以对属性进行访问
`Person p=new Person();`  
`p.Name="Li Ming";`  
`Console.WriteLine(p.Name);`  
编译器实际上产生了两个方法set_Name与get_Name  
### 属性与字段的比较  
由于属性实际上是方法  
所以属性可以具有的优点为：  
1.可以只读或只写：只有get或set。  
2.可以进行有效性检查：if...  
3.可以是计算得到的数据  
4.可以定义抽象类  
## 索引
索引器(Indexer)  
```
修饰符 类型名 this[参数列表]  
{
	set
	{
	}
	get
	{
	}
}
```
类似于C++中[]运算符的重载。  
调用方法为：对象名[参数]  
## 类的继承  
父类baseclass、子类subclass  
C#中采用单继承  
所有的类都是通过直接或间接地继承object（即System.Object）得到的。  
```
class SubClass:BaseClass
{
}
```
子类自动地从父类那里继承所有的字段、方法、属性、索引器等成员作为自己的成员。  
除了继承父类的成员外，子类还可以：添加新的成员、隐藏或修改父类的成员。  
如果要在子类定义一个和父类同名的字段，那么我们需要在声明变量时加一个new。  
如果在子类中出现了和父类同名的方法：  
1. 同名、但参数列表（签名）与父类不同的方法，这称为对父类方法的重载(Overloading)  
2. 同名且参数列表也与父类相同的方法，这称为新添加一种方法，用new表示。  
3. 同名且参数列表也与父类相同的方法，而且父类的方法用了abstract或virtual进行了修饰，子类的同名方法用了override进行了修饰，这称为虚方法的覆盖（overriding）。  
在子类的方法中可以使用base访问父类的方法和字段。  
### 子类和父类的转换  
子类的对象可以赋值给父类的对象，反之不可以（除非进行强制类型转换）。  
```cs
Person p1= new Person();  
Person p2= new Student();  
Student s1=new Student();
Student s2=new Student();  
p1=s1;//可以，因为Person类型的变量可以引用Student对象  
s1=p1;//不行，因为会产生编译错误  
s2=(Student)p1;//编译时可以通过，运行时则会出现类型不能转换的异常  
s2=(student)p2;//正确，因为p2引用的正好是Student对象实例
```
### as运算符  
可以用as运算符来代替强制类型转换  
如果不能转换，值为null  
```C#
Student s3=p1 as Student;//结果s3为null  
Student s4=p2 as Studnt;//s4被赋值  
```
它与强制类型转换的区别为：  
as只能针对引用型变量  
如果不能转换，as运算不会引起异常，只是值为null。  
### is运算符  
`if(p is Person)`  
判断一个对象是不是某个类（及其子类）的实例 
##修饰符  
###访问控制符
如图：  

### static
static的字段、方法、属性是属于整个类的  
static方法中，不能访问实例变量  
调动static方法时，直接用类名访问  
`Console.Write(...);	Math.Sqrt(...);`
static变量可以用来表示“全局变量”。  
在C#2.0中类名也可以用static修饰（该类中所有方法必须都为static方法）  
static构造方法：详见[静态构造函数 ](https://www.cnblogs.com/wubianluomu/articles/9572269.html
)  
### const及readonly  
const相当于静态常量
readonly相当于不可改量，只能赋值一次  
如String.Empty。  
在构造方法中赋值，或者在声明时就赋值。  
注：  
const只能用于基本类型及string  
readonly只能修饰字段，而const还可以修饰局部变量。  
### sealed及abstract  
sealed类，不可继承（也有利于编译优化）  
如String Console Math Convert  
abstract类，不可实例化(new)  
如Array，RandomNumberGenerator  
abstract的方法体，不用{}，用；  
abstract 类型 方法名(参数列表);  
abstract 类型 属性名{get;set;}  
## 接口  
接口实际上是一个约定  
如：ICloneable，IComparable  
接口是抽象成员的集合  
ICloneable含有方法clone()  
IComparable含有方法compare()  
接口是一个引用类型，比抽象类更抽象。  