# c#的类和名称空间
- 类是构成程序的主体
- 名称空间(namespace)以树型结构组织类(和其他类型)。  
> 例如:Button和Path类

## 从Hello,World开始认识类和名称空间
```cs
using System;

namespace ConsoleApp
{
    class Program
        {
            Console.WriteLine("Hello,World");
        }
    }
}
```
- `using System;`的作用是引用名称空间,引用后可以直接使用名称空间中的类而不用在前面加上名称空间。如果不加名称空间的引用要想使用Console类必须得使用`System.Console.WriteLine("Hello,World")

- `namespace ConsoleApp{class Program{....`为什么要把Main函数写在类里？这是因为C#是完全面向对象的语言，要使用Main函数，也要把它写在类里才可以。(这里也可以不使用名称空间，使用名称空间的目的是为了便于后续的管理和维护)。
- `static void Main(string[] args)`static函数即静态方法(函数)，与C++ 一样，静态方法可以不用具体的对象来进行使用，只要在前面加上类名即可(这里的WriteLine方法也是一个static方法)。C#中的main函数首字母需要大写(区别与C/C++)
- 注意:名称空间的引用并不是越多越好，如果两个名称空间里有名字一样的类，那么这两个名称空间里的同名类将都不可以使用。

## 类库(Assembly)
不管是使用类还是名称空间，我们都需要引用其所在的类库(Assembly)，即.dll(Dynamic Link Library)文件。  
在VS2019中我们可以点击"解决方案资源管理器"中对应项目的"引用(References)"来查看该程序引用了那些类库。双击该类库可以进入"对象浏览器"查看该类库中包含的类和名称空间以及每个类的方法和字段。  
![微信截图_20201017170346.png](https://i.loli.net/2020/10/17/V78rS6dKDsiZ2v1.png)  
![微信截图_20201017170453.png](https://i.loli.net/2020/10/17/x3EFBKnGmPVvzlf.png)
## 类库的引用
- 类库引用是使用名称空间的物理基础
> 不同技术类型的项目会默认引用不同的类库。
- DLL引用(黑盒引用，无源代码)
- 项目引用(白盒引用，有源代码)

### DLL引用
在"解决方案资源管理器"中右击"引用"选择"添加引用"进入引用管理器，选择浏览添加.dll文件即可添加新的DLL文件并在程序中使用该类库中的函数。  
![QQ图片20201018171058.png](https://i.loli.net/2020/10/18/YWjUhb4cgrq9ISn.png)
DLL引用的缺点是如果代码中有错误，并不能直接修改，只能联系类库的编写者修改后重新编译。  
### 项目引用
首先把项目添加到解决方案中，右击"解决方案资源管理器"选择添加"现有项目"将要引用的项目添加到解决方案中。  
![QQ截图20201018182403.png](https://i.loli.net/2020/10/18/zLo8mapgnXQe1Mi.png)
接着在"解决方案资源管理器"中右击"引用"选择"添加引用"，在引用管理器左侧选择项目，并点击刚刚添加的新项目，选择确定。
![QQ截图20201018182611.png](https://i.loli.net/2020/10/18/Pz5NBaY7u2tCUqn.png)
这时就可以在程序中使用刚刚添加项目里的类和名称空间。
### 自己编写类库
新建项目时选择类库(class library)即可。  
![QQ截图20201018183416.png](https://i.loli.net/2020/10/18/SfYupin8XTeRCl6.png)

## 依赖关系
- 类(或对象)之间的耦合关系
- 优秀的程序追求"高内聚，低耦合"
- UML(通用建模语言)类图。  