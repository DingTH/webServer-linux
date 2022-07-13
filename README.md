# A High performance Webserver -linux

## Introduction  

本项目是linux平台下使用C++开发的高性能并发Web服务器，解析了get请求，可处理静态资源，支持HTTP长连接

## Envoirment

* OS: Ubuntu 22.04 LTS

##  Technical points

* 基于C/S服务器模型，采用半同步/半异步的并发编程模式：处理I/O密集型任务
* 使用epoll边沿触发的IO多路复用技术，模拟Proactor事件处理模式，非阻塞I/O
* 主线程通过系统调用监听端口、建立连接并接受数据， 工作线程仅负责业务逻辑，即解析与应答
* 注册epoll的EPOLLONESHOT事件，确保每个连接每次只被一个线程处理
* 使用多线程充分利用CPU的资源， 并使用**线程池**避免线程频繁创建和销毁的开销
* 使用**有限状态机**高效解析请求，并采用**分块写**将多块地址上的内容一起发送
* 基于小顶堆的定时检测活跃连接：关闭超时连接

