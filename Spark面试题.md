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
* 生产环境中，Spark往往作为***统一资源管理平台的用户***，向统一资源管理平台提交作业，Spark作业提交成功后，被调度成计算任务，再资源管理容器中运行
* 在集群运行中的***Spark架构是典型的主从架构master/slave***
    * 所有的分布式架构无外乎两种，主从master/slave和点对点p2p架构
    ![Spark Architect](/images/spark/spark_architect.png)
* 

#### 2.1.2 Spark抽象

#### 2.1.3 Spark运行环境

### 2.2

## 3. Spark高级编程

## 4. Spark流处理

## 5. Spark图挖掘

## 6. Spark机器学习

## 7. 商业智能系统实战
