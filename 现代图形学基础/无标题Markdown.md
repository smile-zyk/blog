# 先导知识
## 线性代数(略)

## 非线性变换与齐次坐标(Homogeneous Coordinates)
为了解决非线性变换无法表示为与要变换向量维数一致的矩阵，我们引入了齐次坐标(Homogeneous Coordinates)。  
  
例如：对于二维空间中的向量:
- 添加一个第三维的坐标w。
- 2D point =(x,y,**1**)^T
- 2D vector =(x,y,**0**)^T
- 之所以把点的w坐标设置为1，向量的w坐标设置为0，是因为这样的话，点和点相减得到的就是向量。
- vector + vector = vector
- point - point = vector
- point + vector = point
- point + point = point ([x,y,w]是一个2D的点[x/w,y/w,1]其中w!=0)
```math
\left\{
 \begin{matrix}
   x^, \\
   y^, \\
   1
  \end{matrix} 
\right\}=
\left\{
 \begin{matrix}
   a&b&t_x\\
   c&d&t_y\\
   0&0&1
  \end{matrix}
\right\}\cdot
\left\{
 \begin{matrix}
   x \\
   y \\
   1
  \end{matrix} 
\right\}
```
显然，我们可以将此概念引入三维空间。
```math
\left\{
 \begin{matrix}
   x^, \\
   y^, \\
   z^, \\
   1
  \end{matrix} 
\right\}=
\left\{
 \begin{matrix}
   a&b&c&t_x\\
   d&e&f&t_y\\
   g&h&i&t_z\\
   0&0&0&1
  \end{matrix}
\right\}\cdot
\left\{
 \begin{matrix}
   x \\
   y \\
   z \\
   1
  \end{matrix} 
\right\}
```

# 将三维模型转换到二维平面
一个三维的图形想要显示到二维平面需要经历一系列变换，可以分为模型变换(Model  transformation)、视口变换(View  transformation)、投影变换(projection transformation)。
## 模型变换(Model transformation)
模型变换实际上就是模型本身的变换，与二维平面的变换一样，我们可以分为:放缩变换、平移变换、旋转变换
### 放缩变换(Scale transformation)
### 平移变换(Translation transmation)
### 旋转变换(Rotation transmation)
