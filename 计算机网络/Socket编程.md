# 概述
Socket是计算机网络中传输层提供给应用层的接口(API),同时是对TCP/IP协议的封装，他使得程序员们可以在一定程度屏蔽底层的细节面向业务逻辑编程，并让不同的(操作系统甚至指令集都不相同)机器直接通过给定接口通讯。

## 从一段Socket代码开始
```c
#include<stdio.h>
#include<string.h>
#include<unistd.h>
#include<sys/socket.h>
#include<sys/types.h>
#include<arpa/inet.h>
#include<netinet/in.h>

int main(int argc,char **argv)
{
    int clientSocket=socket(AF_INET,SOCK_STREAM,IPPROTO_TCP);
    struct sockaddr_in serverAddr;
    serverAddr.sin_family=AF_INET;
    serverAddr.sin_port=htons(12345);
    serverAddr.sin_addr.s_addr=inet_addr(argv[1]);
    printf("try connect...\n");
    int err=connect(clientSocket,(struct sockaddr*)&serverAddr,sizeof(serverAddr)); 
    if(err==-1)
    {
        printf("connect error!\n");
        return 1;
    }
    printf("connect success!\n");
    char data[1024];
    while(1)
    {
        scanf("%s",data);
        send(clientSocket,data,strlen(data),0);
    }
    close(clientSocket);
    return 0;
}
```
这是一个实现TCP通讯的socket客户端代码。下面我们将一步一步的来理解这段代码。
### 从创建一个socket对象开始
程序的第一行首先使用socket函数来创建一个socket对象(套接字),其中socket函数的三个参数分别为地址族，数据格式以及协议。其函数原型如下:  
`int socket (int __domain, int __type, int __protocol) `  
首先,一个基本的问题：什么是socket？  
你可能会回答：socket就是套接字！但是套接字又是什么呢？(毫无疑问套接字是一个非常失败的翻译！)
在英文里，socket通常指插座，或者电灯泡的插槽，实际上这是一个非常形象的解释！  
一方面Socket可以指一组实现tcp/ip协议传输层的api，用户只要使用这些api就可以实现网络通讯而不用了解更多传输层以及以下的细节，从这个方面看Socket确实就像一个插座！用户只要把自己实现的应用层的程序(就好比一个灯泡)实现在Socket的api之上,就可以实现自己的网络应用。
> 注意：一般我们说到socket可能指的是由操作系统提供实现网络通讯的一系列API，也可能指用来标识网络通讯过程中每一个连接的一个数字(我们叫做一个socket对象)
> 在本文中，我使用Socket来表示TCP/IP协议中所提供的一组API，使用socket来表示用socket函数创建的socket对象。  

但是我们这里使用socket函数来创建的对象显然并不是一组api，他可以看成是一个五元组(本地IP地址,本地端口号,目标IP地址,目标端口号,通信协议)。  
为什么要使用五元组来表示一个socket对象呢？  
我们先思考这样一个问题: