## 掌握Kafka重要底层原理
## 根据底层原理内容，不变应万变，总结归纳面试题

### Kafka常见应用场景/你们公司是如何应用Kafka的/Kafka与其它MQ中间件的区别...

* 一般从Kafka的概念出发： kafka是一个“分布式的流处理平台”，跟大数据是一个比较好的结合，因为大数据本身有很多的流处理平台
* Kafka的特性一：提供发布订阅以及Topic支持
* Kafka的特性二：吞吐量高但不保证消息records全局有序，只保证单个partition中消息有序，所有的MQ中间件则是先进先出，保证有序性
* kafka的特性三：提供offset管理（根据日志管理来管理offset，可以消费历史数据，所以如果不清理日志，日志会一直增加），MQ中间件不会，消费完了就结束了

### Kafka常见应用场景：

* 日志收集或流式系统，与别的组件整合
* 消息系统，注意不保证有序性，适合对顺序不敏感的业务，比如订单系统
* 用户活动跟踪与运营指标监控，例如用户画像，推荐系统，优惠券投放，指挥室服务监控等 

### Kafka吞吐量大的原因分析：

* kafka两个优点，吞吐量大，以及可以消费历史数据
* Producer读取消息内容，存储到磁盘上，consumer从磁盘上将消息读取出来，中间涉及到日志存储，消息推送，消息消费，消息检索等步骤
* kafka的优化方向：
    * 日志顺序读写和快速检索
    * Partition机制，可以并行
    * 批量发送接收，和数据压缩机制（Gzip，Snappy等），压缩和解压虽然增大了数据处理时间，但大大减少了网络传输时间和节省带宽
    * 最重要的一点：通过sendfile实现zero copy原则
    
### Kafka底层原理之日志

* Kafka的日志是以partition为单位进行保存
* 日志目录格式为Topic name + 数字
* 日志文件格式是一个“日志条目”序列
* 每条日志消息由4字节整型与N字节消息组成

![Kafka Record](/images/kafka_record.png)

#### 日志分段
* 每个partition的日志会分为N个大小相等的segment中，不会让单个日志文件很大
* 每个segment中消息数量数量不一定相等
* 每个partition只支持顺序读写，在顺序读写的情况下，磁盘io不一定比内存慢，甚至高很多；磁盘随机读写才比较慢
* segment包含排序的数字，可以快速定位位置
* segment存储结构：partition会将消息添加到最后一个segment上
* 当segment达到一定阈值会flush到磁盘上
* 每个segment都分为两个部分： index文件（存放offset元数据） + log文件（data）

#### 日志读操作

* 首先需要在存储的数据中找出segment文件
* 然后通过全局offset计算出segment的中offset
* 通过index中的offset寻找具体数据内容

#### 日志写操作

* 顺序读写，日志允许串行的追缴消息到文件最后
* 当日志文件达到阈值则滚动到新文件上

#### Zero Copy原理

正常JVM Linux的规范，经过app等四个步骤
![Kafka Use](/images/kafka_use.png)

上面图中的内核缓冲区和socket缓冲区是不能节省的，但用户缓冲区可以节省，** sendfile ** 的模式，只剩两步，节省大量拷贝和上下文切换：
![Kafka Zero Copy](/images/kafka_zerocopy.png)

> sendfile在linux中实现，windows中没有实现，这也是为什么不推荐kafka部署到Windows中的原因之一

#### kafka的消费者和消费者组

* kafka消费者组是Kafka消费的单位，用groupid来指定消费者组
* 消费者组最主要的作用 -
    * 前提：一条消息只能被消费一次，单个partition只能由消费者组中的某个消费者消费 （要不然肯定要加锁什么的）
    * 消费者组的某个消费者可以消费多个partitions
    
#### Producer客户端

Producer开启守护进程，不断轮循，追加到队列，然后再推送到kafka broker上
![Kafka Producer Client](/images/kafka_producerclient.png)
![Kafka Producer Client](/images/kafka_producerclient2.png)

#### Kafka如何保证有序性
