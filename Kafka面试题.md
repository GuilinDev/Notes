## 掌握Kafka重要底层原理
## 根据底层原理内容，不变应万变，总结归纳面试题
## mindmap

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

* 主要集中在回答业务上的答案
* kafka只支持单partition有序，但生产环境中一般不直接这样用（否则影响效率，可能还不如一般MQ了），生产环境中一般使用Kafka Key + offset可以做到业务有序，这样就会与业务进行关联
* 例如订单系统，利用订单号作为key，标记业务的先后，当consumer将消息消费下来后，通过key来划分先后；用户画像，可以用用户id来区分前后等
* 并不是所有的业务都适合key + offset的场景，有的也只能用单topic + 单partition来保证整个kafka层面上有序（很少）

#### kafka topic 的删除

* 特殊场景才删除，异步线程 + 延迟操作进行删除
* 删除topic的问题会比较多
* 建议设置auto.create.topics.enable = false，否则增删会出问题
* delete.topic.enable = true
* 尽量停掉kafka停掉再删（通过域名限制流量），生产环境中通知各服务停掉，十分钟之内，

删除流程图，每个版本名字可能还不一样

![Kafka Producer Client](/images/kafka_deleteTopic.png)

#### 消息的重复消费和漏消费原理分析

* 二者本质都是offset的控制出现问题
* 重复消费比较常见，漏消费较少（实时流消息系统，日志系统这些漏了也不容易发现）
* 70% 人为原因，尤其是单次消费超时的情况 - 概率最大的一种可能就是自动提交offset，consumer在unsubscribe时出现异常，再恢复时从之前老的offset读起，与服务端的offset不一致，导致重复消费
* 30% Kafka本身机制，单次消费超时 - 不建议consumer过重，导致线程阻塞（某些records反复消费），可以用事务或者加一层封装线程判断异常
* 30% Kafka本身机制 - 消费者重平衡时offset没控制好，新成员加入组时（joining ）和group）和组成员崩溃时（member failure），主动离组（member leave group）都可能出现

不能完全杜绝重复消费，主要解决办法是1）手动控制offset，consumer.seek() - 每次起始位置可以存入redis中等；2）尽可能一个consumer消费一个partition；3）幂等性操作，业务系统除重

#### 消费者线程安全分析

* Kafka Consumer不是线程安全的
* 如何保证Consumer线程安全性 
    * 多个consumer，每个线程启动一个consumer - 这种经典模式可以比较方便精细化控制consumers和partitions一对一的关系，用起来比较简单，可能会有CPU上下文切换的开销
    * 一个consumer，所有消息通过多线程去处理 - 后续线程池来处理records，每一条消息都用一个线程处理，并行能力更强，流处理更合适，例如订单推物流

#### Kafka的leader选举

* leader出现异常的情况下（leader心跳不过/follower落后太多）
* 新的leader必须尽量包含所有消息，即消息完整性
* 不能产生过多的冗余，导致过多的磁盘io （Kafka没有用多数选举的方式，否则需要保证半数的nodes是存活的，也就是一倍以上的冗余）
* kafka Leader选举过程
    1. Topic/Partition级别出现问题 - 维护ISR列表（包含followers的同步信息，ACKS = 0/1/all），在ISR列表中选择Leader；follower同步leader的时候可能落后
    2. Broker出现问题（批量失败，业务系统中更可能，磁盘内存损坏等）：选举众多的Brokers的一个作为Controller检查broker级别故障，Controller会维护所有节点的元数据
    3. ISR的所有列表都用完了（网络问题等） - 1） 干等ISR列表中任意一个leader恢复，一定时间里没有leader； 2）unclean leader，只能在followers中选举了，followers一般都会有延迟；小型系统可以这样做
    4. unclean.leader.election.enable关闭unclean leader选举，大部分系统这样做，只能人工运维

#### Kafka的幂等性Idempotence

* 幂等性的定义： 最开始出现在接口访问中，多次请求也可以让服务器知道是同一次请求，产生同样的回应
* Kafka为什么会产生幂等性 - leader选举可能导致重发的请求，服务器收到重复的请求时，如果之前没收到，当作新请求，如果之前收到了，就直接抛弃这次请求
* kafka会产生哪些幂等性问题 
    * 单体：针对一个topic的一个partition，不会落在多个节点上，依赖批次id的pid和sequenceNumber，单体幂等性相关配置 enable.idempotence
    * 群体：都在发多个节点，依赖事务来解决
    * 保证幂等性的操作还是会影响吞吐量，如果消息本身就带有类似时间戳的信息，例如日志类的处理，或者GPS导航绘图就自带时间戳，或者对顺序无要求的消息，直接利用records自带的信息就好
    
#### Kafak事务支持的实现和原理

* 跟幂等性关联，更复杂
* Kafka为什么需要事务 - 跨topics/partitions的情况，幂等性搞不定了，只能上事务
* Kafka事务实现方式
    * 添加transactional_id配置
    * 完成事务的初始化和开启
    * 事务完成记得Commit或者abort
    * 事务实现的核心是coordinator - 观察者，检测事务和注册transaction_id
* 事务非必要就不用，性能损耗至少20%+