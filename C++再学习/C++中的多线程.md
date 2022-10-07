[TOC]
# 线程的创建
从C++11开始，标准库里已经包含了对线程的支持，`std::thread`是C++11标准库中的多线程的支持库，支持RAII，使用简单，具体使用方法为:`std::thread th(ThreadMain,[args....])`。
如：
```cpp
#include <iostream>
#include <string>
#include <thread>

void ThreadMain(std::string name)
{
    std::cout << "Thread name : " << name << std::endl;
    std::cout << "Thread id : " << std::this_thread::get_id() << std::endl;
}

int main()
{
    std::thread th(ThreadMain, "testThread");
    th.join();
}
```
```txt
运行结果:
Thread name : testThread
Thread id : 12016
```
> std::this_thread::get_id()可以获得当前线程的ID

## 线程的生命周期和线程的等待与分离
`std::thread`和正常的C++对象一样,在离开其作用域时会调用自己的析构函数释放资源.
但是如果`std::thread`在析构时线程还未终止则会导致程序崩溃.
为了解决这个问题,thread有两个方法,分别为join()与detach()
- join : join会阻塞主线程,直到该线程对象终止并返回,然后由主线程回收线程资源并继续运行.
- detach : detach不会阻塞主线程,而是直接将该线程与主线程分离,在后台独立运行,主线程无法再取得该线程的控制权。当主线程结束时，由运行时库负责清理与该线程相关的资源。
> 注意:
> detach同时也带来了一些问题，如果子线程要访问主线程中的对象，而主线程中的对象又因为主线程结束而被销毁时，会导致程序崩溃。

## 线程的参数传递

## 线程的使用方法
### 使用成员函数
### 使用匿名函数(Lambda表达式)

# 多线程通信
## 多线程通信的状态
### 竞争状态和临界区
## 锁
### 互斥锁(mutex)
### 超时锁(timed_mutex)
### 递归锁(recurive_mutex)
### 共享锁(shared_mutex)
## 锁的资源管理
### lock_guard
### unique_lock
### shared_lock
### scoped_lock
## 条件变量(condition_variable)
## 异步通信