# 先做减法再做加法
## 1. 基础
### 1.1 MapReduce：计算框架和编程模型
* Google三驾马车
    * 分布式系统两大顶级会议：ODSI，SOSP
* MapReduce编程模型（programming model）与MapReduce计算框架（framework）
    * 1. 将输入数据集抽象成集合
    * 2. 将数据处理过程用map和reduce表示
    * 3. 在自定义函数中实现自己的逻辑
* 并发（concurrency）与并行（parallelism）
    * 并发，指能处理多个同时性活动的能力，并发事件之间不一定要同一时刻发生。
    * 并行，指同时发生的两个并发事件，具有并发的含义，而并发则不一定并行。
* 如何理解分布式计算框架德编程接口和背后的工程实现
    * 保存中间结果很重要，数据不是存在一台机器上的内存里面，而是多台计算机的内存或者磁盘里
    * 基于MR编程模型的分布式计算框架，其接口与普通函数式语言的数据处理没有不同，只是工程实现千差万别
    * Spark的目标就是让用户处理海量数据集时，与处理内存中的集合变量并没有什么不同

### 1.2 Hadoop：集群的操作系统
* HDFS + MapReduce = Hadoop （1.0， 2.0， 3.0）, + HBase
* Hadoop 1.0 的三个缺点
    ![hadoop1.0](/images/spark/hadoop_1.0.png)
    * 主节点可靠性差，没有热备；
    * 提交 MapReduce 作业过多的情况下，调度将成为整个分布式计算的瓶颈 - 未把资源管理和作业调度两个组件分开；
    * 资源利用率低，并且不能支持其他类型的分布式计算框架 - 如果一个集群部署了 Hadoop 1.0，那么想要运行 Spark 作业就必须另外再部署一个集群

* Hadoop 2.0基本上改进了1.0的重大缺陷
    * 引入了资源管理与调度系统YARN
    * YARN 将集群内的所有计算资源抽象成一个资源池，资源池的维度有两个：CPU 和内存。
    * 同样是基于 HDFS，我们可以认为 YARN 管理计算资源，HDFS 管理存储资源。
    * 上层的计算框架地位也大大降低，变成了 YARN 的一个用户
    * 另外，YARN 采取了双层调度的设计，大大减轻了调度器的负担
    * 此外，YARN可以兼容多个计算框架，如Spark，Storm， MapReduce等
    ![hadoop2.0](/images/spark/hadoop_2.0.png)

* Hadoop 2.0生态圈部分重要组件
![hadoop2.0](/images/spark/hadoop_2.0_eco.png)

* Hadoop可以理解为一个***计算机集群的操作系统***，而Spark和MarReduce只是这个操作系统支持的编程语言，HDFS则是这个计算机集群的文件系统的抽象，YARN是对计算机集群的资源管理与调度系统抽象

### 1.3 统一资源管理与调度系统的设计和实现
> Spark很多情况下基于YARN运行

* 统一资源管理与调度系统的设计
    * 统一： 指资源并不会与计算框架绑定，所有资源无差别
    * 资源管理： 常见资源的维度有CPU，内存，网络贷款等，对于YARN来说资源的维度有两个，CPU和内存
    * 调度： 调度器范式（scheduler pattern）有三种，通常人为YARN的调度属于第二种双层调度（但严格来说是个很复杂的问题，不深究）
        * 集中式调度器，Monolithic Scheduler - 计算框架的资源申请全部提交给中央调度器来满足，所有的调度逻辑都由中央调度器来实现，高并发作业的情况下，容易出现性能瓶颈， 集中式调度器的实现就是 Hadoop MapReduce 的 JobTracker，实际的资源利用率只有 70% 左右，甚至更低
        ![Monolithic Scheduler](/images/spark/yarn0.png)
        * 双层调度器（最常用），Two-level Scheduler - 整个调度工作划分为两层：中央调度器和框架调度器。中央调度器管理集群中所有资源的状态，它拥有集群所有的资源信息，按照一定策略（例如 FIFO、Fair、Capacity、Dominant Resource Fair）将资源粗粒度地分配给框架调度器，各个框架调度器收到资源后再根据应用申请细粒度将资源分配给容器执行具体的计算任务。
        ![Two-level Scheduler](/images/spark/yarn1.png)
        * 状态共享调度器，Shared-State Scheduler - 由 Google 的 Omega 调度系统所提出的一种新范型，状态共享式调度大大弱化了中央调度器，它只需保存一份集群使用信息，就是图中间的蓝色方块，取而代之的是各个框架调度器，每个调度器都能获取集群的全部信息，并采用乐观锁控制并发。
        > 不用深究：Omega 与双层调度器的不同在于严重弱化了中央调度器，每个框架内部会不断地从主调度器更新集群信息并保存一份，而框架对资源的申请则会在该份信息上进行，一旦框架做出决策，就会将该信息同步到主调度。资源竞争过程是通过事务进行的，从而保证了操作的原子性。由于决策是在自己的私有数据上做出的，并通过原子事务提交，系统保证只有一个胜出者，这是一种类似于 MVCC 的乐观并发机制，可以增加系统的整体并发性能，但是调度公平性有所不足。对于这种调度范式你可以不用深究，这里介绍主要是为了知识的完整性。
        ![Shared-State Scheduler](/imanges/spark/yarn2.png)

* 统一资源管理与调度系统的实现 - YARN

* YARN 的架构是典型的主从架构

主节点是 ResourceManger，也是主调度器，所有的资源的空闲和使用情况都由 ResourceManager 管理。ResourceManager 也负责监控任务的执行，从节点是 NodeManager，主要负责管理 Container 生命周期，监控资源使用情况等 ，Container 是 YARN 的资源表示模型，Task 是计算框架的计算任务，会运行在 Container 中，ApplicationMaster 可以暂时认为是二级调度器，比较特殊的是它同样运行在 Container 中。

![YARN架构图](/images/spark/yarn.png)

* YARN 启动一个 MapReduce 作业的流程
    * 第 1 步：客户端向 ResourceManager 提交自己的应用，这里的应用就是指 MapReduce 作业。
    * 第 2 步：ResourceManager 向 NodeManager 发出指令，为该应用启动第一个 Container，并在其中启动 ApplicationMaster。
    * 第 3 步：ApplicationMaster 向 ResourceManager 注册。
    * 第 4 步：ApplicationMaster 采用轮询的方式向 ResourceManager 的 YARN Scheduler 申领资源。
    * 第 5 步：当 ApplicationMaster 申领到资源后（其实是获取到了空闲节点的信息），便会与对应 NodeManager 通信，请求启动计算任务。
    * 第 6 步：NodeManager 会根据资源量大小、所需的运行环境，在 Container 中启动任务。
    * 第 7 步：各个任务向 ApplicationMaster 汇报自己的状态和进度，以便让 ApplicationMaster 掌握各个任务的执行情况。
    * 第 8 步：应用程序运行完成后，ApplicationMaster 向 ResourceManager 注销并关闭自己。

    ![YARN启动MR](/images/spark/yarn_MR.png)

> Spark on YARN： 由于 Spark 与 MapReduce 相比，是一种 DAG 计算框架，包含一系列的计算任务，比较特殊，所以 Spark 自己实现了一个集中式调度器  *** Driver ***，用来调用作业内部的计算任务。申请到的资源可以看成是申请分区资源，在该分区内，所有资源由 Driver 全权使用，以客户端方式提交的 Spark on Yarn 这种方式可以看成是 Driver 首先在资源管理和调度系统中注册为框架调度器（二级调度器），接收到需要得资源后，再开始进行作业调度。那么这种方式也可以认为是一种曲线救国的双层调度实现方式 。

### 1.4 解析Spark数据处理与分析场景

![Spark Scenario](/images/spark/spark_scenario.png)

#### 1.4.1 按作业类型分
* 批处理，Batch Processing - 数十秒到数小时都可能，对每条数据消耗计算资源少
    * ETL，从数据库中抽取一部分数据进行去重后写入到存储系统
    * 机器学习中的训练模型
    * 缺点是处理任务延迟长，无法与在线系统实时对接
* 流处理，Streaming Processing - 数据是动态源源不断的，来一条处理一条，数据蕴含的价值随着时间流逝而降低，所以需要实时处理
    * 一般与在线系统对接，实时数据分析，业务系统的消息流转等
    * 默认数据一到来就进行处理，每条数据的计算成本高

> 批处理和流处理结合的场景： 比如模型分析师用机器学习算法对一批数据进行训练，得到一个模型，测试完毕后，数据工程师会将这个模型部署到线上环境对数据流进行实时预测。

#### 1.4.2 按需求确定性分
* 需求不确定的情况： 数据探索，了解数据集的最好方式 - 按自己习惯对数据进行一些查询处理
* 需求确定 - 定时、定期运行

#### 1.4.3 按结果响应时间
* 可以在线响应，一般涉及数据库和查询语言相关： OLTP和OLAP（ad-hoc等），一般涉及读优化和写优化两种trade-off
    * HTAP，Hybrid Transaction and Analytical Process，混合事务与分析处理，即可事务处理也可分析处理，近几年的业界提出的新场景，例如TiDB
* 不能在线响应，离线处理
* 在线处理和离线处理具有概念的交叉与重合
* Spark与OLAP并非完全无关 - 例如，在历史订单数据库中，保存了极其巨量的数据（从过去到现在的所有订单），而用户只关心历史某个品类的月度销量数据，但是由于原始数据过于巨大，所以导致普通的查询及其缓慢，在这里，可以用 Spark 将数据从数据库抽取出来并按照时间与品类维度进行转换和汇总（批处理），处理后的数据的大小与原始数据相比可能是上万倍的差距，用户就能很容易地进行在线分析了。

### 1.5 如何选择Spark编程语言以及部署Spark
#### 1.5.1 Spark编程语言种类，如何选择
![Spark Programming Language](/images/spark/spark_programming_language.png)
大数据工程师一般Scala，数据分析师一般Python

#### 1.5.2 部署Spark
共分两步进行部署：
* 1. 选择统一资源管理与调度系统，目前Spark支持的有：
    * Spark standalone - 基本不适合生产环境
    * YARN - Spark on YARN模式是目前最普遍用的
    * Mesos - Spark最先支持的平台，共五步：
        * SparkContext 在 Mesos master 中注册为框架调度器。
        * Mesos slave 持续同步以向 Mesos master 发送资源信息。
        * 一个或者多个资源供给将信息发送给 SparkContext（下发资源）。
        * SparkContext 接收资源供给。
        * 在 Mesos slave 上启动计算任务。
    * Kubernetes - Spark2.4.5版本以上才支持
    * 本地操作系统 - 伪分布模式，学习用
* 2. 提交Spark作业
    * 如果大数据平台使用了统一资源管理与调度系统，那么上层的计算框架就变成了这个资源系统的用户。这样做的结果是直接简化了计算框架的部署。对于部署计算框架这个问题，你可以用客户端/服务端，也就是 C/S 这种模式来理解。把大数据平台看作一个server side，那么节点就是客户端client，例如在Hadoop中，clients可以访问HDFS或者提交作业
    * 这些clients会有一份相应的安装包，按照客户端进行配置，只需在客户端部署一份Spark安装包，并且正确配置
    * 以YARN为例，需要将YARN的配置文件复制到Spark客户端的配置文件夹下，就可以从该节点向大数据平台提交作业并在集群中被调度为计算任务，然后在资源管理系统的容器中运行

#### 1.5.3 如何安装Spark学习环境
* 在本地操作系统以伪分布模式学习
* 也可以用MAVEN来管理
* Python环境则使用Anaconda安装Jupyter Notebook和PySpark

## 2. Spark编程
### 2.1 Spark抽象、架构与运行环境
#### 2.1.1 Spark架构
* 生产环境中，Spark往往作为**统一资源管理平台的用户**，向统一资源管理平台提交作业，Spark作业提交成功后，被调度成计算任务，再资源管理容器中运行
* 在集群运行中的**Spark架构是典型的主从架构master/slave**
    * 所有的分布式架构无外乎两种，主从master/slave和点对点p2p架构
    ![Spark Architect](/images/spark/spark_architect.png)
    ![Spark Architect](/images/spark/spark_architect2.png)
* 1. 首先，Driver 会根据用户编写的代码生成一个计算任务的有向无环图（Directed Acyclic Graph，DAG），这个有向无环图是 Spark 区别 Hadoop MapReduce 的重要特征；
* 2. 接着，DAG 会根据 RDD（弹性分布式数据集，上图中第 1 根虚线和第 2 根虚线中间的圆角方框）之间的依赖关系被 DAG Scheduler 切分成由 Task 组成的 Stage，这里的 Task 就是计算任务，注意这个 Stage 不要翻译为阶段，这是一个专有名词，它表示的是一个计算任务的集合；
* 3. 最后 TaskScheduler 会通过 ClusterManager 将 Task 调度到 Executor 上执行。

> Spark 并不会直接执行用户编写的代码，而用户代码的作用只是告诉 Spark 要做什么，也就是一种“声明”。

#### 2.1.2 Spark抽象（概念）
* 当用户编写好代码向集群提交时，一个作业job就产生了（YARN中的作业叫做application，一个意思）
* Driver根据用户代码生成一个DAG有向无环图

![Spark Architect](/images/spark/spark_dag.png)

上面A 和 C 都是两张表，在分别进行分组聚合和筛选的操作后，做了一次 join 操作。灰色的方框就是分区（partition），它和计算任务是一一对应的，也就是说，有多少个分区，就有多少个计算任务，显然的，一个作业，会有多个计算任务，这也是分布式计算的意义所在，**可以通过设置分区数量来控制每个计算任务的计算量**。在 DAG 中，每个计算任务的输入就是一个分区，一些相关的计算任务所构成的任务集合可以被看成一个 Stage，这里"相关"指的是某个标准，我们后面会讲到。RDD 则是分区的集合（图中 A、B、C、D、E），用户只需要操作 RDD 就可以构建出整个 DAG，从某种意义上来说，它就是为了掩盖上面的概念而存在的。

> 来看看 Executor，一个 Executor 同时只能执行一个计算任务，但一个 Worker（物理节点）上可以同时运行多个 Executor。Executor 的数量决定了同时处理任务的数量，一般来说，分区数远大于 Executor 数量才是合理的。所以同一个作业，在计算逻辑不变的情况下，分区数和 Executor 的数量很大程度上决定了作业运行的时间。

#### 2.1.3 Spark运行环境
* 一共申请10个Executor，每个10g，一共100g，如果改成100个Executor，每个1g，job执行速度是否大大提升呢？答案是不确定
* 因为总量不变的情况下，**每个Executor的资源见少为原来的十分之一**，那么Executor有可能无法胜任单个计算任务的计算量（或许能，但是完成速度会大大降低），这样就不得不提升分区数来降低每个计算任务的计算量
* 所以**完成作业的总时间有可能保持不变，也可能增加，也可能降低**
* Spark的调参和机器学习的调参类似，都是在一定约束下（这里是是资源），通过超参数的改变，来实现某个目标（这里是job执行时间）的最优化
* 以上是调参的简化，只考虑Executor的资源，没考虑Driver所需的资源；另外只考虑了内存，而没有考虑cpu

### 2.3 弹性分布式数据集 RDD
* 一组分布式的JVM**不可变**对象集合，使用时就当作普通集合使用
* RDD类型分为几类：
    * 并行集合 - 将内存中集合变量转化为RDD，学习用，生产环境不用
    * 从HDFS中读取 - 常用
    * 外部数据源 - 例如基于MySQL的JDBC，与Sqoop类似，JdbcRDD需要手动指定数据的上下界，例如MySQL中的某一列的最值
    * PairRDD - 以元组为核心，与上面三种可互相转换

### 2.4 算子（Operator）如何构建数据管道
* Spark编程风格主要是函数式，核心是基于数据处理的需求，用算子与RDD构建出一个数据管道
* 算子种类
    * Transform算子 - Spark 会将转换算子放入一个计算的有向无环图中，并不立刻执行，当 Driver 请求某些数据时，才会真正提交作业并触发计算
    * Action算子 - 行动算子就会触发 Driver 请求数据

### 2.5 函数式编程思想

### 2.6 共享变量
* 广播变量，只能读
* 累加器Accumulator - 只能增加

### 2.7 计算框架的分布式实现，剖析Spark Shuffle原理
* 容错机制
    * Driver报错 - Spark 应用最严重的一种情况，标志整个作业彻底执行失败，需要开发人员手动重启 Driver
    * Executor - Executor 报错通常是因为 Executor 所在的机器故障导致，这时 Driver 会将执行失败的 Task 调度到另一个 Executor 继续执行，重新执行的 Task 会根据 RDD 的依赖关系继续计算，并将报错的 Executor 从可用 Executor 的列表中去掉
    * Task执行失败 - Spark 会对执行失败的 Task 进行重试，重试 3 次后若仍然失败会导致整个作业失败。在这个过程中，Task 的数据恢复和重新执行都用到了 RDD 的血统机制
* Spark Shuffle - 很多算子都会引起 RDD 中的数据进行重分区，新的分区被创建，旧的分区被合并或者被打碎，在重分区的过程中，如果数据发生了跨节点移动，就被称为 Shuffle，体现了从函数式编程接口到分布式计算框架的实现
    * Hash Shuffle
    * Sort-based Shuffle
* 对1TB数据排序，可用Spark的RangePartitioner + sortByKey算子（而不是单纯merge sort，归并会最后把结果归到一个executor上，太大），如果数据倾斜怎么办？分区前抽样，根据权重来。

## 3. Spark高级编程
### 3.1 DataFrame，DataSet和SparkSQL
* DataFrame - 相比底层的RDD + Operator，是高级SQL的封装，也有自己的API，所以首选DataFrame + SparkSQL
* DataFrame和DataSet，DataFrame的API也有算子风格和SQL风格，和RDD一样都是spark平台下的分布式弹性数据集，DataFrame = RDD[Row] + shcema，DataSet则和RDD对比

### 3.2 用户自定义函数 - 复杂需求常用
* 窗口函数
* 函数
* DataFrame API支持用户自定义函数
    * UDF，类似map操作行处理，一行输入，一行输出
    * UDAF，聚合处理，多行输入，一行输出

* 任何情况下，都不推荐RDD——算子的方式
    * 相当于用汇编语言写代码
    * RDD+算子与SQL/DataFrame API/DataSet API相比，更偏于如何做，而不是做什么，优化空间少
    * RDD语言比SQL难很多
    * 其它情况下，优先考虑Dataset，因为静态类型的特点使计算更迅速，但用户也需选择静态语言例如Java和Scala，而Python是没有Dataset API的
    * DataFrame + SQL是综合最好选择

### 3.3 列式存储，针对查询场景的极致优化
* 只是查询的场景，没有增删改，使用列式存储对Spark的效率提高很多
    * 优点：查询时只读取涉及的列，列直接作为索引，行式则必须读入整行
    * 优点：投影操作非常高效
    * 优点：数据稀疏的情况下，压缩率比行式存储高很多
    * 优点：因为直接作用于某一列，所以cluster分析非常迅速
* 实现1： Google Dremel - repetition level和definition level，查询执行树
* 实现2： Apache Parquet - ORC格式大多列式情况都使用
* 实现3： Apache CarbonData，国产

### 3.4 Spark生产环境全方位的性能调优
* 如何查看Spark的作业日志 - 通常是排错的唯一依据
    * 注意Spark Jobs是一个分布式执行过程，所以日志也是分布式的
    * 联想Spark的架构，所以日志也有两个级别，Driver（简单情况）和Executor（复杂情况）
    * YARN-client模式直接输出到客户端，例如nohup/&等
    * 查看Executor需要先将散落在各个节点（container）的日志收集汇总成一个文件
    * 第一件事是利用时间戳和ERROR标记定位最开始报错的那一句日志

#### 3.4.1 硬件维度
* 内存： 256G，内存与CPU大致1：5
* CPU： Intel E5-2640v4，24核心
* 硬盘： 3T * 8
* Spark中上千的集群是非常大的

#### 3.4.2 资源管理平台维度
* 增加并行程度的数量
    * 参数调优和应用调优，在Spark作业划分中，一个Executor只能同时执行一个Task，一个**计算任务的输入**是一个分区partition，所以改变并行程度只有一个办法，就是提高同时运行Executor的个数
    * 通常集群的总量是一定的，这样Exexutor数量增加，单个Executor所分的资源会减少，这时候可以增加分区数来减少每个分区的大小（让计算任务减少）来避免这个问题
* 提高Shuffle的性能
    * Map端中间结果的缓冲区大小，默认32k
    * Map端输出中间结果的文件大小，默认48M，并会与其它文件进行合并
    * Map端输出是否开启压缩，默认开启
* 内存管理 - 计算内存和存储内存
    * spark.memory.fraction
    * spark.memory.storageFraction
    * JVM老年代
* 序列化 - 时间换空间，推荐Kyro格式而非Java原生支持序列化格式

...

#### 3.4.3 使用方式维度
...

### 3.5 Tungsten和Hydrogen：Spark的性能提升与优化计划，前沿探索计划
* Tungsten 
    * 摆脱JVM内存管理器而自主来内存管理，
    * 缓存感知计算
    * Catalyst优化器
* Hydrogen
    * 标准化Spark与各机器学习框架之间的数据交换接口
    * 数据交换
    * 向量化执行模型

### 3.6 实战：葡萄牙银行电话调查结果
* DataSet API - Scala

## 4. Spark流处理
### 4.1 什么是流处理？如何保证消息送达的问题（delivery guarantee）
* delivery guarantee三种机制
    * at least once
    * at most once
    * exact once
* 恰好一次，需要保证both
    * 发送消息的可靠性保障
    * 消费消息的可靠性保障
    * 幂等

### 4.2

### 4.3

### 4.4 

### 4.5 

### 4.6 

## 5. Spark图挖掘

## 6. Spark机器学习

## 7. 商业智能系统实战
