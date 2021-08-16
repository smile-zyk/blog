# C#的构成元素
- 关键字(Keyword)
- 操作符(Operator)
- 标识符(Identifier)
- 标点符号
- 文本
- 注释和空白

## 关键字
- 普通关键字
![微信截图_20201020134531.png](https://i.loli.net/2020/10/20/IfAMdEBnW1jXTQZ.png)
- 上下文关键字
![微信截图_20201020134705.png](https://i.loli.net/2020/10/20/B1UK9a5FRQXczCx.png)
- MSDN文档：[C#关键字|MSDN](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/
)

## 操作符
![微信截图_20201020135430.png](https://i.loli.net/2020/10/20/HjSg65BCmwDqVfi.png)
MSDN文档：[C# 运算符和表达式|MSDN](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/operators/)
## 标识符
- 命名规范  
（1）不能是C#关键字(如果非要用关键字可以在前面加一个@)。  
（2）由字母、数组、下划线构成。  
（3）第一个字符必须是字母或下划线。  
（4）不要太长，一般不超过31个字符为宜。  
（5）变量名最好不要与库函数、类名相同。  
与C/C++ 类似，与C/C++ 一样C#是大小写敏感的。  

## 标点符号
如分号( ; )，大括号({})，小括号()，起到分隔语句的作用。

## 文本(字面值)
[词法结构|MSDN（从"文字"单元开始看，随便吐槽一下机翻）](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/language-specification/lexical-structure#tokens)
### 整数字面值
- 如果字面值以0X或者0x开头则字面值为16进制
- 如果字面值没有后缀，则其值可以表示为以下类型的第一个类型：int、uint、long 和 ulong 。
- 如果字面值的后缀为 U 或 u 则它具有以下类型中可以表示其值的第一个类型：uint、ulong 。
- 如果字面值的后缀为 L 或 l 则它具有以下类型中可以表示其值的第一个类型： long、ulong。
- 如果字面值的后缀为 UL、Ul、uL、ul、LU、Lu、lU 或 lu  ，则它属于类型ulong。

### 实数字面值
- 如果未指定实数字面值后缀 ，则真实字面值的类型为 double 。 否则，实数类型后缀将确定真实文本的类型，如下所示：
- 用F或f作为后缀的实数字面值的类型为 float 。例如，字面值1f、1.5f、1e10f和 123.456F都是类型 float 。
- 用 D 或 d 作为后缀的实数字面值的类型为 double 。 例如，字面值1d 、1.5d 、1e10d 、和 123.456D 、都是类型 double 。
- 用 M 或作为后缀的实数字面值 m 的类型为 decimal 。 例如，字面值1m 1.5m 1e10m 和 123.456M 都是类型 decimal 。 通过采用精确值将此字面值转换为一个 decimal 值，并在必要时使用银行家舍入（decimal 类型）舍入为最接近的可表示值。 除非值舍入或值为零（在这种情况下，正负号为0），否则字面值中的任何小数位数都将保留。 因此， 2.900m 将分析文本，以形成带有符号 0 、系数 2900 和刻度的小数 3 。
> 关于decimal类型  
[Decimal类型|MSDN](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/language-specification/types#the-decimal-type)

### 其他详见MSDN(字符字面值，字符串字面值等等。。。)

## 注释和空白
同C/C++ ，不赘述。