## 1 网络面试核心
1. OSI开放式互联参考模型 - 只是个概念性框架
    * [OSI图](https://blog.csdn.net/yaopeng_2005/article/details/7064869)
    * [OSI各层讲解](https://juejin.cn/post/6844903505111547918)
    
2. OSI模型的实现：TCP/IP四层协议
    * [tcp/IP Model](https://www.geeksforgeeks.org/tcp-ip-model/)
    
3. TCP的三次握手 Three-way Handshake
    * TCP的服务端和客户端全双工通道(Full Duplex)，通过sequenceID来保持有序性
    * 了解ACK - 确认序号标志；SYN - 同步序号，用于建立连接过程；FIN - finish标志，用于释放连接
    * URG - 紧急指针标志；PSH - push标志； RST - 重置连接标志

    [TCP三次握手](/images/java/TCP3WayHandshakes.png)
    
    * Linux默认重试1 + 2 + 4 + 8 + 16 + 32 = 63秒才断开TCP连接
        
4. TCP的四次挥手 Four-way Handshake

    [TCP四次挥手](/images/java/TCP4WayHandshakes.png)
    
5. TCP和UDP的区别
    * UDP不支持错误重传，滑动窗口等特征，报文也比较简单
    * 面向非链接，不是全双工
    * 不维护连接状态，支持同时向多个客户端传输相同的消息
    * 数据包的报头只要8个字节(TCP有20个字节)，额外开销小
    * 吞吐量之受限于数据生成速率、传输速率以及机器性能
    * 不保证可靠交付，不需维护复杂的链接状态表，也没有有序性
    * 不对应用程序提交的报文信息进行拆分或者合并
    
* TCP的滑动窗口
    * RTT：发送一个数据包到收到对应的ACK，所花费的时间
    * RTO：重传时间间隔
    * TCP使用滑动窗口做流量控制和乱序重排
    
## 2 数据库

## 3 Redis

## 4 Linux

## 5 JVM

## 6 JVM GC

## 7 JAVA多线程和并发

## 8 JAVA多线程和并发 - 原理

## 9 JAVA常用类库和技巧

## 10 Spring
