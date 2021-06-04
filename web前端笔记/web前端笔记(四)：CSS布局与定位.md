# CSS布局
## 概述
网页通常的布局如图所示：
![TIM截图20191209152844.png](https://i.loli.net/2019/12/09/3AyYBHWw6QFuKd2.png)
由此我们可以大概可以将CSS布局分为两个内容:
<dl>
	<dt>盒子模型</dt>
	<dd>页面元素的大小</dd>
	<dd>边框</dd>
    <dd>与其他元素的距离</dd>
	<dt>定位机制</dt>
	<dd>文档流</dd>
	<dd>浮动定位</dd>
	<dd>层定位</dd>
</dl>

## 盒子模型
页面上的区域、图片、导航、列表、段落，都可以是盒子
### 组成
- content内容
- height高度
- width宽度
- border边框
- padding内边距
- margin外边距  

![TIM截图20191209154711.png](https://i.loli.net/2019/12/09/bwP2SQm8e4rAWIk.png)  
盒子模型的属性是可以分方向的，如border-top代表上边框，具体如下图:  
![TIM截图20191209154925.png](https://i.loli.net/2019/12/09/OHT7ZpVDdezjnAF.png)  

一个盒子的实际宽度、高度：content+padding+border+margin：  
![TIM截图20191209155237.png](https://i.loli.net/2019/12/09/QlIS4qkVmA3wgKn.png)  
### overflow属性
超出盒子模型的部分我们用overflow属性来进行设置：
- hidden：超出部分不可见
- scroll：显示滚动条
- auto：如果有超出部分，显示滚动条  

### border属性
- border-width:..px、thin、medium、thick
- border-style:dashed(横线)、dotted(点线)、solid(实线)、double(双实线)
- border-color:颜色
- border:width style color  
  
可以利用border属性来制作样式多样的水平分割线
```css
.line{
    height:1px;
    width:500px;
    border-top:1px solid #e5e5e5;
}
```
### margin和padding属性
每个浏览器会个margin和padding一个默认值
首先要对margin和padding属性清零,使用*标记来对所有标签的margin和padding进行初始化。
```
*{
    margin:0;
    padding:0;
}
```
取值：px，%(外层盒子的宽度和高度)  
如果只赋一个margin值说明四个方向全为该值，如果有四个值则为上右下左(顺时针方向)，如果是两个或者三个值，则根据上下一致，左右一致的原则缺省：
![TIM截图20191209165353.png](https://i.loli.net/2019/12/09/BjmAyKdipXbFJYl.png)  
![TIM截图20191209165501.png](https://i.loli.net/2019/12/09/AZyl3bJGhfBMTwW.png)  
margin属性的上下边框会有合并的效果：  
![TIM截图20191209170857.png](https://i.loli.net/2019/12/09/8CmKoRZWHgQz3eO.png)
#### 如何将盒子内容水平居中？
`margin:0(上下边框的宽度) auto(左右宽度设为auto将会自动根据外部盒子和div内容的宽度自动设置为居中)` 
# CSS定位机制
CSS的定位方法主要分三种：
- 文档流定位
- 浮动定位
- 层定位

## 文档流定位
文档流定位主要靠display属性来进行。  
display属性主要分为三种：block、inline、inline-block。  

### block类型元素
特点：
- 独占一行
- 元素的height、width、margin、padding都可以设置  
常见的block元素有：
div,p,h1...h6,ol,ul,table,form....  
非block类型的元素可以通过将其display属性设置为block，使其具有block属性特点。  

### inline类型元素
特点：  
- 不单独占用一行
- width、height不可设置
- width就是它包含的文字或图片的宽度，不可修改
  
常见的inline元素有：span,a
同样的，我们也可以通过设置非inline属性的display为inline来将其变为inline类型元素。  
注意：inline类型元素直接排列会中间会有间隙。

### inline-block类型元素
同时具有inline元素和block元素的特点：
- 不单独占用一行。  
- 元素的height、width、margin、padding都可以设置
  
常见的元素有:img。  
同样可通过设置`display:inline-block`来将其他类型元素设置为inline-block.   

## 浮动定位
### float属性
可以设置三种不同情况：left(左浮动)、right(右浮动)、none(不浮动)。  
使用float属性之后，元素脱离了文档流原来的位置，根据设置的属性进行浮动。原有的位置空出。  
如果浮动时当前行宽度不够，则另起一行。  
### clear属性
可以设置四种不同的值：
- both，清除左右两边的浮动
- left和right只能清除一个方向的浮动
- none是默认值，只在需要移除已指定的清除值时用到。  
clear的意思虽然是清除然而这个属性在实际使用时并不是清除左侧或右侧的元素，而是一行一行找左侧或右侧没有元素的地方。  

## 层定位
这个部分内容细节很多，详见一个大佬整理的博客:[CSS属性：定位属性（图文详解） ](https://www.cnblogs.com/qianguyihao/p/8296748.html)
