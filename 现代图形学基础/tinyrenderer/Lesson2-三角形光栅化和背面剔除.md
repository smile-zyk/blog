## 三角形填充
嗨,大伙.这是我.
![](https://raw.githubusercontent.com/ssloy/tinyrenderer/gh-pages/img/02-triangle/cfa0f3a9d9.png)  
更准确的说,这是一个我脸部的模型,它使用我们将在接下来的一两个小时编写的程序渲染.上次我们画出了一个三维模型的线框图,这一次,我们将填充多边形,准确的说是三角形.实际上,OpenGL几乎可以三角化任何多边形,所以不需要考虑复杂的情况.

> 注意,这一系列文章的目的是为了让你自己手把手地编程.当我说你可以在两个小时内渲染出类似上面的图像,我的意思并不是在两个小时内阅读我的代码.
而是在两个小时内从头开始创建你的代码.这里提供的代码纯粹是为了让你用我的代码和你(正在运行的)程序作对比.我是一个糟糕的程序员,很有可能你的代码比我写的要好.不要简单地复制粘贴我的代码.欢迎任何意见和问题.

## 经典方法-扫描线算法
我们目前的任务是画出二维的三角形.对于对此感兴趣的学生来说,这通常需要几个小时,即使他是一个糟糕的程序员.上一次我们了解了Bresenham的画线算法.今天的任务是绘制出被填充的三角形.有趣的是,这个任务并不轻松.我并不知道为什么,但是我知道这是真实存在的.我的大多数学生都很难完成这个简单的任务.所以,初始的代码看起来是这样的.
```cpp
void triangle(Vec2i t0, Vec2i t1, Vec2i t2, TGAImage &image, TGAColor color) { 
    line(t0, t1, image, color); 
    line(t1, t2, image, color); 
    line(t2, t0, image, color); 
}

// ...

Vec2i t0[3] = {Vec2i(10, 70),   Vec2i(50, 160),  Vec2i(70, 80)}; 
Vec2i t1[3] = {Vec2i(180, 50),  Vec2i(150, 1),   Vec2i(70, 180)}; 
Vec2i t2[3] = {Vec2i(180, 150), Vec2i(120, 160), Vec2i(130, 180)}; 
triangle(t0[0], t0[1], t0[2], image, red); 
triangle(t1[0], t1[1], t1[2], image, white); 
triangle(t2[0], t2[1], t2[2], image, green);
```
![](https://raw.githubusercontent.com/ssloy/tinyrenderer/gh-pages/img/02-triangle/41060d3251.png)  

和往常一样,这段代码可以在GitHub上找到相应的[提交](https://github.com/ssloy/tinyrenderer/tree/7e46cc57fa3f5a41129d6b6fefe4e77f77b8aa84).这段代码很简单:我为代码的初始调试提供了三个三角形.如果我们在`triangle`函数中调用了`line()`,我们将会得到三角形的轮廓.如何绘制一个被填充的三角形呢?  
一个绘制三角形的好方法必须具有以下的特点:
- 它应该(非常)简单和高效
- 它应该是对称的:绘制的图像应该不依赖于传递给绘图函数的顶点顺序.
- 如果两个三角形有两个相同的顶点,由于光栅化的舍入(rounding),它们之间应该没有缝隙.
- 我们可以添加更多的需求,但让我们先着眼于上面这几点.  
  
传统的扫描线算法流程为:
1. 根据三角形顶点的y轴坐标来对顶点进行排序
2. 同时光栅化三角形的左右两侧.
3. 绘制一条在左右边界点之间的水平线段.

哪一段是左,哪一段是右?我的学生们在这一点上开始失去了合理的根据.此外,在一个三角形中有三条线段...通常,在介绍完这些之后,我会离开我的学生们大约一个小时:再一次重申,相比先自己实现,然后把实现的代码和我的代码比较,仅仅阅读我的代码你获得的收获将会少很多!

[一个小时过去了...]

我是如何绘制三角形的呢?再次重申,如果你有一个更好的方法,我很乐意采纳它.我们假定我们有三角形的三个点:t0,t1,t2,他们按照y轴坐标升序排序.接着,边界A在t0和t2之间,边界B在t0与t1,t1和t2之间.
```
void triangle(Vec2i t0, Vec2i t1, Vec2i t2, TGAImage &image, TGAColor color) { 
    // sort the vertices, t0, t1, t2 lower−to−upper (bubblesort yay!) 
    if (t0.y>t1.y) std::swap(t0, t1); 
    if (t0.y>t2.y) std::swap(t0, t2); 
    if (t1.y>t2.y) std::swap(t1, t2); 
    line(t0, t1, image, green); 
    line(t1, t2, image, green); 
    line(t2, t0, image, red); 
}
```
这里边界A用红色表示,边界B用绿色表示.
![](https://raw.githubusercontent.com/ssloy/tinyrenderer/gh-pages/img/02-triangle/3a5643f513.png)  
不幸地是,边界B由两部分构成.让我们通过水平裁剪,先渲染出三角形的下半部分.
```cpp
void triangle(Vec2i t0, Vec2i t1, Vec2i t2, TGAImage &image, TGAColor color) { 
    // sort the vertices, t0, t1, t2 lower−to−upper (bubblesort yay!) 
    if (t0.y>t1.y) std::swap(t0, t1); 
    if (t0.y>t2.y) std::swap(t0, t2); 
    if (t1.y>t2.y) std::swap(t1, t2); 
    int total_height = t2.y-t0.y; 
    for (int y=t0.y; y<=t1.y; y++) { 
        int segment_height = t1.y-t0.y+1; 
        float alpha = (float)(y-t0.y)/total_height; 
        float beta  = (float)(y-t0.y)/segment_height; // be careful with divisions by zero 
        Vec2i A = t0 + (t2-t0)*alpha; 
        Vec2i B = t0 + (t1-t0)*beta; 
        image.set(A.x, y, red); 
        image.set(B.x, y, green); 
    } 
}
```
![](https://raw.githubusercontent.com/ssloy/tinyrenderer/gh-pages/img/02-triangle/d8e0575a00.png)
注意,有一些线段是不连续的.上次画直线的时候我们努力地得到了连续的线段,但这里我没有麻烦地旋转图像(还记得当时我们把x与y进行交换吗?).为什么呢?我们接下来将要填充的三角形就是原因.如果我们通过水平线连接对应的点,缝隙就会消失:
![](https://raw.githubusercontent.com/ssloy/tinyrenderer/gh-pages/img/02-triangle/c1f95127ad.png)  
现在,让我们绘制出三角形的第二部分(上半部分).我们可以通过添加一个循环来完成这一步:
```cpp
void triangle(Vec2i t0, Vec2i t1, Vec2i t2, TGAImage &image, TGAColor color) { 
    // sort the vertices, t0, t1, t2 lower−to−upper (bubblesort yay!) 
    if (t0.y>t1.y) std::swap(t0, t1); 
    if (t0.y>t2.y) std::swap(t0, t2); 
    if (t1.y>t2.y) std::swap(t1, t2); 
    int total_height = t2.y-t0.y; 
    for (int y=t0.y; y<=t1.y; y++) { 
        int segment_height = t1.y-t0.y+1; 
        float alpha = (float)(y-t0.y)/total_height; 
        float beta  = (float)(y-t0.y)/segment_height; // be careful with divisions by zero 
        Vec2i A = t0 + (t2-t0)*alpha; 
        Vec2i B = t0 + (t1-t0)*beta; 
        if (A.x>B.x) std::swap(A, B); 
        for (int j=A.x; j<=B.x; j++) { 
            image.set(j, y, color); // attention, due to int casts t0.y+i != A.y 
        } 
    } 
    for (int y=t1.y; y<=t2.y; y++) { 
        int segment_height =  t2.y-t1.y+1; 
        float alpha = (float)(y-t0.y)/total_height; 
        float beta  = (float)(y-t1.y)/segment_height; // be careful with divisions by zero 
        Vec2i A = t0 + (t2-t0)*alpha; 
        Vec2i B = t1 + (t2-t1)*beta; 
        if (A.x>B.x) std::swap(A, B); 
        for (int j=A.x; j<=B.x; j++) { 
            image.set(j, y, color); // attention, due to int casts t0.y+i != A.y 
        } 
    } 
}
```
![](https://raw.githubusercontent.com/ssloy/tinyrenderer/gh-pages/img/02-triangle/b1a0fce5f1.png)  
这可能已经足够了,但是我不喜欢看到同样的代码两次.这是我将其变得些许难读的原因,但是它变得更加便于修改和维护.
```cpp
void triangle(Vec2i t0, Vec2i t1, Vec2i t2, TGAImage &image, TGAColor color) { 
    if (t0.y==t1.y && t0.y==t2.y) return; // I dont care about degenerate triangles 
    // sort the vertices, t0, t1, t2 lower−to−upper (bubblesort yay!) 
    if (t0.y>t1.y) std::swap(t0, t1); 
    if (t0.y>t2.y) std::swap(t0, t2); 
    if (t1.y>t2.y) std::swap(t1, t2); 
    int total_height = t2.y-t0.y; 
    for (int i=0; i<total_height; i++) { 
        bool second_half = i>t1.y-t0.y || t1.y==t0.y; 
        int segment_height = second_half ? t2.y-t1.y : t1.y-t0.y; 
        float alpha = (float)i/total_height; 
        float beta  = (float)(i-(second_half ? t1.y-t0.y : 0))/segment_height; // be careful: with above conditions no division by zero here 
        Vec2i A =               t0 + (t2-t0)*alpha; 
        Vec2i B = second_half ? t1 + (t2-t1)*beta : t0 + (t1-t0)*beta; 
        if (A.x>B.x) std::swap(A, B); 
        for (int j=A.x; j<=B.x; j++) { 
            image.set(j, t0.y+i, color); // attention, due to int casts t0.y+i != A.y 
        } 
    } 
}
```
绘制2D三角形的代码可以在[这里](https://github.com/ssloy/tinyrenderer/tree/024ad4619b824f9179c86dc144145e2b8b155f52)得到.
## 我在实际代码中使用的方法
尽管不是很复杂,但是行扫描算法的源代码确实有点混乱.此外,行扫描算法实际上是一个为单线程CPU编程设计的老式算法.让我们看一看下面这一段伪代码:
```
triangle(vec2 points[3]) { 
    vec2 bbox[2] = find_bounding_box(points); 
    for (each pixel in the bounding box) { 
        if (inside(points, pixel)) { 
            put_pixel(pixel); 
        } 
    } 
}
```
很容易找到一个包围盒,检查一个点是否在一个2D三角形(或者其他凸多边形)实际上也没有问题.
(一段作者的人生感悟,略)  
好,让我们开始吧!首先我们需要知道为什么是[重心坐标](https://en.wikipedia.org/wiki/Barycentric_coordinate_system).给定一个2D的三角形ABC和一个点P,

