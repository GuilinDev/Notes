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
    
    [TCP滑动窗口的计算过程](/images/java/TCPSlidingWindow0.png)
    
    * TCP会话发送方四类状态
    
    [TCP会话发送方四类状态](/images/java/TCPSlidingWindow1.png)
    
    * TCP会话接收方的三种状态
    
    [TCP会话接收方的三种状态](/images/java/TCPSlidingWindow2.png)
    
* HTTP相关
    * 客户端/服务器模式
    * 无状态
    * HTTP请求体和响应体结构
    
    [HTTP请求体结构](/images/java/HTTP_0.png)
    
    [HTTP响应体结构](/images/java/HTTP_1.png)
    
    * 浏览器输入URL之后的流程
        * DNS解析
        * TCP连接，三次握手等
        * 发送HTTP请求
        * 服务器处理请求并返回HTTP报文
        * 浏览器收到响应体并渲染页面
        * 连接结束，四次挥手等（与第5步不分先后）
        
    * HTTP状态码Status Code
        * 1xx - 请求已接收，继续处理
        * 2xx - 请求已成功接收、理解，接受
        * 3xx - 重定向，要完成请求必须进行更进一步的操作
        * 4xx - 客户端错误，请求有语法错误或请求无法实现
        * 5xx - 服务器端错误，服务器未能实现合法的请求
        
        常见状态码：
        
        [HTTP常见状态码](/images/java/HTTPStatusCodes.png)
    
    * 常用请求方法，GET和POST请求的区别
        * HTTP报文Message/Packet层面：GET将请求信息放在URL（浏览器都有长度限制），POST放在报文体中，注意这个跟安全性无关
        * DB层面：GET符合幂等性和安全性，POST不符合 
        * 别的：GET可以被缓存、被存储，POST不行
        
    * Cookie和Session
        * HTTP本身是无状态的，这俩让HTTP可以有状态
        * Cookie
            * Cookie是由服务器发送给客户端的特殊信息，以文本的形式存放存放在客户端
            * 客户端再次请求的时候，会把Cookie回发
            * 服务器接收到后，会解析Cookie生成与客户端相对应的内容
            * Cookie的设置及发送过程
            
            [Cookie](/images/java/HTTPCookie.png)
            
        * Session
            * Session是服务器端机制，在服务器上保存的类似散列表的信息
            * 解析客户端请求并操作session id（没有第一次会新创建一个），按需保存状态信息，session id不容易重复和冒充
            * Session的实现方式
                * 使用Cookie实现
                * 使用URL回写来实现
        
        * Cookie和Session区别
            * Cookie数据存放在客户的浏览器上，Session数据在服务器上
            * Session相对于Cookie更安全
            * Session对服务器开销大，Cookie对服务器开销小
            
* HTTP和HTTPS的区别
    * HTTPS简介
    
    [HTTPS简介](/images/java/HTTPS_0.png)
    
    * SSL Security Sockets Layer
        * 为网络通信提供安全及数据完整性的一种安全协议
        * 操作系统对外的API，SSL3.0后更名为TLS
        * 采用“身份验证”和“数据加密”保证网络通信的安全和数据完整性
    
    * 加密的方式
        * 对称加密Symmetric-key algorithm： 加密和解密都使用同一个密钥
        * 非对称加密Public-key cryptography： 加密使用的密钥，解密使用的密钥是不一样的，性能低，安全性高，加密长度有限制，例如RSA，DSA，Linux中的SSH等
        * 哈希算法：将任意长度的信息转换为固定的长度的值，算法不可逆，例如MD5等
        * 数字签名：证明某个消息或文件时某人发出/认同的
        
    * HTTPS的加密
        * 实际生产环境中，通常要多个加密方式结合使用，HTTPS使用证书+各种机密方式
        * HTTPS数据传输流程
            * 浏览器将支持的加密算法信息发给服务器
            * 服务器选择一套浏览器支持的加密算法，以证书的形式回发给浏览器
            * 浏览器收到证书后，验证合法性，随机生成一串密码，并结合证书public key加密信息，利用约定好的握手消息，生成随机数，回发给服务器
            * 网站服务器再接收到加密信息后，用private key解密信息，验证随机数哈希值，加密response消息，回发给浏览器
            * 客户端解密response，并对消息进行验证，完成握手流程并进行机密交互数据
            
    * HTTP与HTTPS的区别
        * HTTPS需要到CA申请证书，HTTP不需要，免费的证书很少，基本上都需要收费
        * HTTPS是密文传输，HTTP只是超文本明文传输
        * 连接方式不一样，HTTPS默认端口443，HTTP默认80
        * HTTPS = HTTP + 加密 + 认证 + 完整性保护
        
    > HTTPS真的安全吗？ 1）浏览器默认http://，请求跳转时有劫持风险；2）HTTPS还未主流，优化的方式不够多
    
* Socket相关
    * 两个进程通信，基本前提是标识两个进程，本地就用PID来唯一标识，但网络中两个进程的PID可能冲突
    * IP地址可以标识唯一的主机，端口号port可以表示该主机的唯一进程，所以IP + protocol + port可以唯一标识进程，这就是Socket的基础
    * Socket是对TCP/IP协议的抽象，是操作系统对外开放的接口
    * Socket通信流程：
    
    [HTTPS简介](/images/java/Socket_0.png)
    
* need a mindmap here
    
## 2 数据库

## 3 Redis

## 4 Linux

## 5 JVM

## 6 JVM GC

## 7 JAVA多线程和并发

## 8 JAVA多线程和并发 - 原理

## 9 JAVA常用类库和技巧

## 10 Spring
