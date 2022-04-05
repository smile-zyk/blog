## 第一次尝试
第一次课程的目标是渲染线框.为此.我们要学会如何画出线段,我们可以简单的阅读一下什么是Bresenham算法,但我们首先应该尝试自己来实现.画一条从 $(x_0,x_0)$ 到 $(x_1,x_1)$ 的线的最简单的代码应该是什么样的?显然,大概是下面这种:
```cpp
void line(int x0, int y0, int x1, int y1, TGAImage &image, TGAColor color) { 
    for (float t=0.; t<1.; t+=.01) { 
        int x = x0 + (x1-x0)*t; 
        int y = y0 + (y1-y0)*t; 
        image.set(x, y, color); 
    } 
}
```
![](https://raw.githubusercontent.com/ssloy/tinyrenderer/gh-pages/img/01-bresenham/c3c2ea8819.png)
这段代码的快照可以在[这里](https://github.com/ssloy/tinyrenderer/tree/d0703acf18c48f2f7d00e552697d4797e0669ade)获得
## 第二次尝试
这段代码的问题(除了它的低效)是那个恒等于 $0.01$ 的常量的选择.如果我们让他等于 $0.1$,我们的线段将会是这样的:
![](https://raw.githubusercontent.com/ssloy/tinyrenderer/gh-pages/img/01-bresenham/62a16a5321.png)
我们可以轻易发现这个必要的步骤:确定需要绘制的像素的数量.最简单(但是错误)的代码如下:
```cpp
void line(int x0, int y0, int x1, int y1, TGAImage &image, TGAColor color) { 
    for (int x=x0; x<=x1; x++) { 
        float t = (x-x0)/(float)(x1-x0); 
        int y = y0*(1.-t) + y1*t; 
        image.set(x, y, color); 
    } 
}
```
小心!我的学生在这段代码的错误的第一个来源是整数除法,比如`(x-x0)/(x1-x0)`.接着,如果我们尝试用这段代码画出下面的几条线:
```cpp
line(13, 20, 80, 40, image, white); 
line(20, 13, 40, 80, image, red); 
line(80, 40, 13, 20, image, red);
```
![](https://raw.githubusercontent.com/ssloy/tinyrenderer/gh-pages/img/01-bresenham/097a691f9e.png)
最终的结果是一条线的效果很好,第二条线有缝隙,第三条线则完全没有.注意,第一条线和第三条线(在上面的代码里)画的是同一条线,但是使用了不同的颜色和方向(源点和目标点翻转了位置).我们已经看到了白色的那条,它画的很不错.我刚刚希望改变这条线的颜色,让他从白色变成红色,但是没有做到.这是一个对称性测试:线段绘制的结果应该不依赖于点的顺序:从a到b的线段应该和从b到a的线段完全相同.

## 第三次尝试
我们通过交换点的方式修复了缺失的红线,这样 $x_0$ 会一直小于 $x_1$ .
其中一条线段有很多缝隙的原因是它的高度大于了宽度.我的学生们通常建议我使用下面的修复方式:
```c
if (dx>dy) {for (int x)} else {for (int y)}
```
神圣的牛!(bushi
```cpp
void line(int x0, int y0, int x1, int y1, TGAImage &image, TGAColor color) { 
    bool steep = false; 
    if (std::abs(x0-x1)<std::abs(y0-y1)) { // if the line is steep, we transpose the image 
        std::swap(x0, y0); 
        std::swap(x1, y1); 
        steep = true; 
    } 
    if (x0>x1) { // make it left−to−right 
        std::swap(x0, x1); 
        std::swap(y0, y1); 
    } 
    for (int x=x0; x<=x1; x++) { 
        float t = (x-x0)/(float)(x1-x0); 
        int y = y0*(1.-t) + y1*t; 
        if (steep) { 
            image.set(y, x, color); // if transposed, de−transpose 
        } else { 
            image.set(x, y, color); 
        } 
    } 
}
```
![](https://raw.githubusercontent.com/ssloy/tinyrenderer/gh-pages/img/01-bresenham/3e8e5c7d26.png)

## 时间优化:第四次尝试
>注意:在编写高效率代码方面,编译器优化(g++ -O3)做的通常比你(还有我)做的更好.这个部分被放在这里有历史和文化原因

这段代码运行的非常棒.这正是我想在最终版本或者我们的渲染器中看到的效果.他显然是低效的(多次除法,和其他类似的问题),但它短小并且具有可读性.注意,他没有任何断言(assert)并且没有做边界检查,这是不好的.在这些文章中我不想重构这部分特定代码,因为他会被很多人阅读.同时,我想系统地提醒大家性能检查的必要性.
所以,前面的代码运行的很好,但是我们可以优化它,优化是一个危险的事情.我们应该清楚代码要在哪个平台上运行.为显卡或仅仅为CPU作代码优化是完全不同的事情.在优化进行之前和进行中,代码必须被剖析.让我们来猜一猜,哪一个操作是这里最耗费资源的操作.  
为了进行测试,我画了 $1,000,000$ 次我们之前画过的三条线.我的CPU是 Intel® Core(TM) i5-3450 CPU @ 3.10GHz.对于每个像素,这段代码调用`TGAColor`的复制构造器.而一共有大约 $1,000,000*3*50$ 个像素(每条线段大约有 $50$ 个像素) .调用属实有点多?我们该从哪里优化呢?分析器(gprof)会告诉我们.  
我使用`g++ -ggdb -g -pg -O0`来编译这段代码,然后我们运行 gprof:
```
%   cumulative   self              self     total 
 time   seconds   seconds    calls  ms/call  ms/call  name 
 69.16      2.95     2.95  3000000     0.00     0.00  line(int, int, int, int, TGAImage&, TGAColor) 
 19.46      3.78     0.83 204000000     0.00     0.00  TGAImage::set(int, int, TGAColor) 
  8.91      4.16     0.38 207000000     0.00     0.00  TGAColor::TGAColor(TGAColor const&) 
  1.64      4.23     0.07        2    35.04    35.04  TGAColor::TGAColor(unsigned char, unsigned char, unsigned char, unsigned char) 
  0.94      4.27     0.04                             TGAImage::get(int, int)
```
运行时间的 $10\%$ 被用于了颜色信息的拷贝.但是运行时间的 $70\%$ 被消耗在了调用函数 `line()`上! 这个函数就是我们将要优化的地方.
## 继续第四次尝试
我们应该注意,每次除法都有相同的除数,让我们把它从循环中拿出来.误差变量(error)给出了从当前像素(x, y)到实际直线的距离.每当error大于一个像素(即error>0.5),我们让y增加(或者减少)1,并且同时让误差量减1.
这段代码可以在[这里](https://github.com/ssloy/tinyrenderer/tree/2086cc7c082f4aec536661d7b4ab8a469eb0ce06)得到.

```cpp
void line(int x0, int y0, int x1, int y1, TGAImage &image, TGAColor color) { 
    bool steep = false; 
    if (std::abs(x0-x1)<std::abs(y0-y1)) { 
        std::swap(x0, y0); 
        std::swap(x1, y1); 
        steep = true; 
    } 
    if (x0>x1) { 
        std::swap(x0, x1); 
        std::swap(y0, y1); 
    } 
    int dx = x1-x0; 
    int dy = y1-y0; 
    float derror = std::abs(dy/float(dx)); 
    float error = 0; 
    int y = y0; 
    for (int x=x0; x<=x1; x++) { 
        if (steep) { 
            image.set(y, x, color); 
        } else { 
            image.set(x, y, color); 
        } 
        error += derror; 
        if (error>.5) { 
            y += (y1>y0?1:-1); 
            error -= 1.; 
        } 
    } 
} 
```
下面是gprof关于这段代码的分析:
```
%   cumulative   self              self     total 
 time   seconds   seconds    calls  ms/call  ms/call  name 
 38.79      0.93     0.93  3000000     0.00     0.00  line(int, int, int, int, TGAImage&, TGAColor) 
 37.54      1.83     0.90 204000000     0.00     0.00  TGAImage::set(int, int, TGAColor) 
 19.60      2.30     0.47 204000000     0.00     0.00  TGAColor::TGAColor(int, int) 
  2.09      2.35     0.05        2    25.03    25.03  TGAColor::TGAColor(unsigned char, unsigned char, unsigned char, unsigned char) 
  1.25      2.38     0.03                             TGAImage::get(int, int) 
```
## 进一步优化:第五次也是最后一次尝试
为什么我们需要浮点数呢?唯一的理由是一个关于dx的除法并且在循环体中我们需要和.5比较大小,我们可以摆脱浮点数通过用另一个变量来替换error变量.我们称其为error2,并且我们假定它和error\*dx\*2相等,这是等价[代码](https://github.com/ssloy/tinyrenderer/tree/28b766abe59b8635c912ed78b8a6e938a7ef29f2)
```cpp
void line(int x0, int y0, int x1, int y1, TGAImage &image, TGAColor color) { 
    bool steep = false; 
    if (std::abs(x0-x1)<std::abs(y0-y1)) { 
        std::swap(x0, y0); 
        std::swap(x1, y1); 
        steep = true; 
    } 
    if (x0>x1) { 
        std::swap(x0, x1); 
        std::swap(y0, y1); 
    } 
    int dx = x1-x0; 
    int dy = y1-y0; 
    int derror2 = std::abs(dy)*2; 
    int error2 = 0; 
    int y = y0; 
    for (int x=x0; x<=x1; x++) { 
        if (steep) { 
            image.set(y, x, color); 
        } else { 
            image.set(x, y, color); 
        } 
        error2 += derror2; 
        if (error2 > dx) { 
            y += (y1>y0?1:-1); 
            error2 -= dx*2; 
        } 
    } 
} 
```
```
%   cumulative   self              self     total 
 time   seconds   seconds    calls  ms/call  ms/call  name 
 42.77      0.91     0.91 204000000     0.00     0.00  TGAImage::set(int, int, TGAColor) 
 30.08      1.55     0.64  3000000     0.00     0.00  line(int, int, int, int, TGAImage&, TGAColor) 
 21.62      2.01     0.46 204000000     0.00     0.00  TGAColor::TGAColor(int, int) 
  1.88      2.05     0.04        2    20.02    20.02  TGAColor::TGAColor(unsigned char, unsigned char, unsigned char, unsigned char) 
```
现在,只要通过引用(或者在编译时打开O3优化)来传递颜色就可以删除在函数调用时不必要的拷贝.在这段代码中没有一个乘法或者除法.执行时间也从 $2.95s$ 降低到了 $0.64s$.
同时我推荐你看一看这个[讨论](https://github.com/ssloy/tinyrenderer/issues/28),优化是一个非常复杂困难的工作!
## 线框渲染
现在我们已经准备好来创建一个线渲染器,你可以在[这里]()找到代码和测试模型的快照.我使用[wavefront obj]()格式的文件来存储模型.渲染所需要的就是从文件中读入以下列格式来存储的顶点数组:
```
v 0.608654 -0.568839 -0.416318
```
是x,y,z 的坐标,文件中的每一行都表示一个顶点或者面.
```
f 1193/1240/1193 1180/1227/1180 1179/1226/1179
```
我们对每个空格后的第一个数字感兴趣,它是我们之前读入的顶点在数组中的位置.因此,这行表示了一个三角形,他的顶点来自1193,1180和1179.注意,obj格式的文件下标从1开始,这意味着你应该找到1192,1179和1178这三个顶点来代替.文件model.cpp包含一个简单的解析器.把下面的循环写入我们的main.cpp并且运行,我们的渲染器已经准备好了!
```
for (int i=0; i<model->nfaces(); i++) { 
    std::vector<int> face = model->face(i); 
    for (int j=0; j<3; j++) { 
        Vec3f v0 = model->vert(face[j]); 
        Vec3f v1 = model->vert(face[(j+1)%3]); 
        int x0 = (v0.x+1.)*width/2.; 
        int y0 = (v0.y+1.)*height/2.; 
        int x1 = (v1.x+1.)*width/2.; 
        int y1 = (v1.y+1.)*height/2.; 
        line(x0, y0, x1, y1, image, white); 
    } 
}
```
![](https://raw.githubusercontent.com/ssloy/tinyrenderer/gh-pages/img/01-bresenham/5da6818190.png)
下次课程我们将画出2D的三角形并且改善我们的渲染器.
