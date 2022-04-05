> 这是一个微型软件光栅化渲染器(的教程),如果你在寻找一个微型软件光追渲染器,你可以在[这里](https://github.com/ssloy/tinyraytracer)找到.
> 我的源代码是平台无关的.阅读这个教程并且实现你自己的渲染器,只有当你经历所有琐碎的细节之后你才能明白这其中发生了什么.
> 我希望你得到反馈的邮件[dmitry.sokolov@univ-lorraine.fr](dmitry.sokolov@univ-lorraine.fr);如果你有任何问题,请不要犹豫,立即向我联系.
> 如果你是一个老师并且想使用这作为教学材料用作你的课堂--非常欢迎你这么做,不需要授权.只需要邮件通知我,这会帮助我改善这个课程.  

在这系列文章中,我想通过编写OpenGL的简单实现来展示它是如何工作的.令我惊讶的是,我经常遇到一些人,他们遇到无法克服学习OpenGL/DirectX最初的障碍(毕竟写个三角形都要好几百行:( 来自翻译者的吐槽).因此,我准备了一个短系列课程,之后我的学生们展示了相当棒的渲染器.
所以,这个作品将遵循以下规则:不使用第三方库(尤其是图形库),并且得到这样的画面:
![](https://raw.githubusercontent.com/ssloy/tinyrenderer/gh-pages/img/00-home/africanhead.png)
>注意:这只是一个教学材料,它简单地复刻了OpenGL的实现.**我并不想展示如何为OpenGL编写应用,我想展示OpenGL是如何工作的.** 我深信如果不能理解这些知识是不可能使用3D图形库写出高效的应用的.  

我会尽力把最终的代码控制在500行左右.我的学生们需要10-20小时的编程时间来实现这样一个渲染器.我们会获得一个带有多边形线和纹理图片的测试文件用于输入.程序最终会输出一个渲染出来的模型.没有图形界面,这个程序仅仅生成一张图片.  
因为我的目标是最小化外部依赖,所以我只给我的学生一个允许使用TGA文件的类,这是支持图片使用 RGB/RGBA/black and white 颜色模型的最简单的格式之一.因此,作为一切的开始,我们将会获得一个简单的方法来使用这些图片,你应该注意到在最开始唯一的可用的功能(除了加载和保存图片)是设置一个像素的颜色.  
没有用来绘制线段和三角形的函数,我们将必须自己来实现他们,我提供了我和学生们一起编写的代码.但是我不推荐使用他,这没有意义.完整的代码可以在github上获得,并且在[这里](https://github.com/ssloy/tinyrenderer/tree/909fe20934ba5334144d2c748805690a1fa4c89f)你会找到我提供给我的学生们的源代码.
```cpp
#include "tgaimage.h"
const TGAColor white = TGAColor(255, 255, 255, 255);
const TGAColor red   = TGAColor(255, 0,   0,   255);
int main(int argc, char** argv) {
        TGAImage image(100, 100, TGAImage::RGB);
        image.set(52, 41, red);
        image.flip_vertically(); // i want to have the origin at the left bottom corner of the image
        image.write_tga_file("output.tga");
        return 0;
}
```
output.tga 应该会像这样:
![](https://raw.githubusercontent.com/ssloy/tinyrenderer/gh-pages/img/00-home/reddot.png)  
预告:渲染器一些渲染结果
![](https://raw.githubusercontent.com/ssloy/tinyrenderer/gh-pages/img/00-home/demon.png)  
![](https://raw.githubusercontent.com/ssloy/tinyrenderer/gh-pages/img/00-home/diablo-glow.png)  
![](https://raw.githubusercontent.com/ssloy/tinyrenderer/gh-pages/img/00-home/boggie.png)  
![](https://raw.githubusercontent.com/ssloy/tinyrenderer/gh-pages/img/00-home/diablo-ssao.png)   