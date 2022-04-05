# 什么是CMake?
CMake是一个构建系统(比如Makefile)的构建系统.
## 什么是构建系统
多文件编译是一个复杂的事情,需要处理各种各样的依赖,并且需要编写复杂的规则和大量重复的脚本.稍有修改就要手动一个一个重新编译,非常的麻烦!  
于是,~~懒惰的~~聪明的程序员们发明了一个叫做make的工具,你只需指明编译项目和文件之间的依赖关系以及生成规则就可以轻松的用几个命令来构建项目.  
综上所述,构建系统的主要优势有:
1. 当更新了一个文件时只会重新编译被更改的那一个文件,而不需要把无关的文件都重新编译一遍.
2. 能够自动并行地发起对不同文件的编译,加快编译速度(make -j).
3. 用通配符批量生成构建规则,避免针对每个.cpp和.o重复写g++命令.
  
但也有一定的缺陷:
1. makefile在Unix类系统上是通用的,但在Windows则不然(不同的开发环境往往有着不同的编译工具链)
> 在windows下一般使用微软的nmake,MSbuild(nmake和Unix系统中的make差不多,MSbuild则主要用来构建VS项目)
1. 需要准确地指明每个项目之间的依赖关系,有头文件时特别头疼
> 相关资料:[头文件与Makefile相关问题](https://github.com/thu-coai/THUOOP/issues/38)
1. makefile的语法非常简单,不像shell或python可以做很多判断
2. 不同的编译器有不同的flag规则,为g++准备的参数可能对MSVC不适用.
## 构建系统的构建系统
为了解决Makefile的以上问题,跨平台的CMake应运而生
# CMakeLists.txt的语法
不管构建多简单或者多复杂的项目,CMakeLists.txt最后具有下面三行
```cmake
# 设置执行该CMakeList.txt的所需的CMake最低版本
cmake_minimum_required(VERSION 3.10)

# 设置项目名称
project(Tutorial)

# 添加最后需要生成的目标
add_executable(Tutorial tutorial.cxx)
```