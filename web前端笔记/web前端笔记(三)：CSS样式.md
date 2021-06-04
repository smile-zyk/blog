# CSS样式
## CSS概述
CSS--Cascading Style Shees层叠样式表  
HTML定义网页的内容，CSS定义内容的样式。  
内容和样式相互分离，便于修改样式。  
### CSS语法
```css
p{
	font-size:12px;/*字号*/
	color:bule;  /*文字颜色*/
	font-weight:bold;  /*加粗*/
}
```
注意：1.最后一条声明可以没有分号，但是为了以后修改方便，一般也加上分号。  
2.为了使用样式更加容易阅读，可以将每条代码写在一个新行内。  
## CSS添加方法
### CSS添加方法--行内  
直接把属性放在标签内部。  
`<p style="color:red;">`  
### CSS添加方法--内嵌样式
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<style type="text/css">
	p{
		color:red;
	}
	</style>
</head>
<body>
	<p>此时我是红色的</p>
</body>
</html>
```
注意：即使有公共CSS代码，也是每个页面都要定义的。  
适合文件很少，CSS代码也不多的情况。  
如果一个网站有很多页面，每个文件都会变大，后期维护难度也大。  
### CSS添加方法--单独文件  
外部式样式表文件style.css
```css
p{
	color:red;
}
```
网页文件：1.html  
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<link rel="stylesheet" href="css/style.css" />
</head>
<body>
	<p>此时我是红色的</p>
</body>
</html>
```
subtime扩展方法：link:csss
单独文件优点：  
页面结构HTML代码与样式CSS代码完全分离  
维护方便  
如果需要改变网站风格，只需要修改公共CSS文件。  
可以在同一个HTML文档中引用多个外部样式表。  
### CSS添加方法--优先级  
多重样式可以层叠，可以覆盖。  
样式的优先级按照“就近原则”。  
行内样式>内嵌样式>链接样式>浏览器默认样式。  
## CSS选择器  
CSS选择器类型：
### 标签选择器  
以标签为名字，如：
CSS:  
```css
<style type="text/css">
body{
	background:center;
	font-size:12px;
}
h1{font:"黑体";font-size:20px;}  
p{color:red;font-size:16px;}  
hr{width:200px}  
</style>
```
HTML：  
```html
<body>
	<h1>标题</h1>
	<hr>
	<p>正文的段落</p>
</body>
```
### 类别选择器
以类别为名字
如：  
CSS：  
```css
<style type="text/css">
	p{font-size:12px;}
	.one{font:"黑体";font-size:20px;}  
	.two{color:red;font-size:16px;}  
</style>
```
HTML：  
```html
<body>
	<p class="one">类别1</p>
	<p class="two">类别2</p>
	<p>正文的段落</p>
</body>
```
### ID选择器  
以ID为名字：  
如：  
CSS：  
```css
<style type="text/css">
	#one{font-size:12px;}
	#two{font:"黑体";font-size:20px;}  
</style>
```
HTML：
```html
<body>
	<p id="one">类别1</p>
	<p id="two">类别2</p>
</body>
```
ID与class 的区别：一个ID在当前文件中只可以被引用一次。  
### 嵌套声明
span标签的嵌套声明：  
CSS：  
```css
<style type="text/css">
	p span{font-size:12px;}
</style>
```
HTML：  
```html
<body>
	<p><span>正文的段落<span></p>
</body>
```
### 集体声明
选择器用，隔开可以声明进行集体声明  
CSS：  
```css
<style type="text/css">
	h1,p{font-size:12px;}
</style>
```
HTML：  
```html
<body>
	<h1>标题</h1>
	<p>正文的段落</p>
</body>
```
### 全局声明  
用*代表全局声明
CSS：  
```css
<style type="text/css">
	*{text-align:center;}
</style>
```
HTML：  
```html
<body>
	<h1>欢迎</h1>
	<p>正文的段落</p>
</body>
```  
### 混合  
多个class选择器混用，用空格分开  
`<div class="one yellow left">oneyellowleft</div>` 
id和class混用  
`<div id="my" class="one yellow left">myoneyellowleft`
id选择器不可以多个同时使用  
## CSS样式(1)文字样式
### CSS样式的常用单位  
1.px：像素  
2.em：1em-一个字符，2em-2个字符，自动适应用户所使用的字体。  
3.%：百分比  
百分比的相对值遵循DOM树的继承：  
![TIM截图20191015104206.png](https://i.loli.net/2019/10/15/AxI4FlvtBnOkbTL.png)  
### 颜色  
1.直接用颜色名字，如：red、blue、green 详见W3Cschool
2.rgb(x,x,x) RGB值，每个颜色分量取值0-255，如红色rgb(255,0,0).  
3.rgb(x%,x%,x%) RGB百分比值，如：红色rgb(100%,0%,0%)  
4.rgba(x,x,x,x) RGB值，透明度 a值：0.0(完全透明)与1.0(完全不透明)，如，红色半透明rgba(255,0,0,0.5,)  
5#rrggbb 十六进制数，如红色：#ff0000或#f00(去掉重复位)  
### 文本可设置样式  
1.color 文本颜色 如：red #f00 rgb(255,0,0)  
2.letter-spacing 字符间距 2px -3px 1em (如果像素为负数，则字符重叠) 
3.line-height 行高 14px 1.5em 120% （em相对于字号大小，我们一般利用行高进行垂直居中，把行高设为与元素高度相等，即可做到垂直居中）  
4.text-align 对齐 center left right justify(两端对齐)    
5.text-decoration 装饰线 none(一般用来去掉默认超链接的下划线) overline(上面有线) underline(下面有线) line-through(中间有线，删除线)  
6.text-indent 首行缩进 2em  
### 字体可设置样式  
1.font 在一个声明中设置所有的字体属性 如：font:bold 18px '幼圆'  
2.font-family 字体系列 如：font-family:"HiraginoSans GB","Micrsoft YaHei"（设置多个字体，第一个没有就用第二个，以此类推，如果字体名字中有空格，需要加引号，否则可以不加）    
3.font-size 字号 如：14px 5pt(榜值) 120%  
4.font-style 斜体 如：italic  
5.font-weight 粗体 如：bold  
当使用font一次性声明字体样式时有一定的顺序  
font:斜体 粗体 字号/行高 字体  
如：font:italic bold 16px/1.5em '宋体'；  
## CSS样式(2)背景与超链接
### 背景可设置样式
1.background-color:见上一节(注意：对于背景颜色和图片，如果标签内元素为空，需要先指定其标签的长宽才能显示出颜色或者图片)    
2.background-image:url("logo.jpg")（背景图片会覆盖背景颜色）      
3.background-repeat(表示背景图片的填充方式): repeat(双向填充),repeat-x(横向填充),repeat-y(纵向填充),no-repeat(只显示一次)    
4.background:颜色 图片 repeat  
### 链接的四种状态  
1.a:link - 普通的、未被访问的链接
2.a:visited - 用户已访问的链接
3.a:hover - 鼠标指针位于链接的上方悬停(必须位于a:link和a:visited之后)    
4.a:active - 链接被点击的时刻(必须位于a:hover 之后)    
我们把这类选择器名称为：伪类选择器。   
## CSS样式(3)列表、表格样式  
### 列表可设置样式
list-style 所有用于列表的属性，设置于一个声明中。  
list-style-image 为列表项标志设置图像 详见上一节背景图片。  
list-style-position 标志的位置 inside,outside（一个在里面，一个在外面）。    
list-style-type 标志类型：太多了，看图吧。  
![TIM截图20191015115355.png](https://i.loli.net/2019/10/15/bdG1CWZz7MAaevB.png)
### 表格可设置样式  
width,height 属性：宽、高。  
border 属性：边框宽度，（在后面盒子模型中和详细说，这里简单说）。  
border-collpase：表格合并  
### nth-child(odd|even)：奇偶选择器
一般用来设置表格隔行颜色不一样，方便用户浏览。如下图：  
![TIM截图20191015122111.png](https://i.loli.net/2019/10/15/X146YQeLt7orWZc.png)  
例如：tr:nth-child(odd|even)（注意括号里可以带数字，直接说明是第几个元组，亦可以用odd和even说明奇偶性）
{
	background-color:#EAF2D3;
}
注意：奇偶是从第一行表头开始数的。