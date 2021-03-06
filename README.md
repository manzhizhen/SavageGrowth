# SavageGrowth
## 帮助程序员找到适合自己的“成长框架”
**让我们抓住这些关键设计**

念念不忘必有回响，持续更新中...

### 目录
- [架构设计](#架构设计)
    - [架构的定义](#架构的定义)
    - [微服务架构](#微服务架构)
    - [GoF的23种设计模式](#GoF的23种设计模式)
        - [接口型模式](#接口型模式)
        - [职责型模式](#职责型模式)
        - [构造型模式](#构造型模式)
        - [操作型模式](#操作型模式)
    - [面向对象设计原则](#面向对象设计原则)
    - [业务系统设计的基本哲学](#业务系统设计的基本哲学)
    - [响应式编程(Reactive)](#响应式编程(Reactive))
- [云原生](#云原生)
    - [定义](#定义)
    - [Docker](#Docker)
    - [Service Mesh](#ServiceMesh(服务网格))
    - [Serverless](#Serverless(无服务器))
- [存储](#存储)
    - [RDS](#RDS)
        - [MySQL](#MySQL)
    - [NoSQL](#NoSQL)
        - [Redis](#Redis)
- [分布式系统](#分布式系统)
    - [常见的一致性算法](#常见的一致性算法)
        - [2PC&3PC](#2PC&3PC)
        - [Paxos](#Paxos)
        - [Raft](#Raft)
        - [Gossip](#Gossip)
        - [ZAB](#ZAB)
    - [RPC框架](#RPC框架)
        - [Apache Dubbo](#Dubbo)
    - [ZooKeeper](#ZooKeeper)
    - [MQ](#MQ)
- [Web服务器](#Web服务器)
    - [Nginx](#Nginx)
    - [Tomcat](#Tomcat)
- [DevOps](#DevOps)
    - [DevOps定义](#DevOps定义)
- [基础框架](#基础框架) 
    - [Spring](#Spring)
    - [Spring Boot](#SpringBoot)  
- [常见工具](#常见工具) 
    - [Arthas](#Arthas)
- [JVM](#JVM) 
    - [运行时数据区域](#运行时数据区域)
    - [垃圾收集算法](#垃圾收集算法)
    - [垃圾收集器](#垃圾收集器)
    - [类加载的过程](#类加载的过程)
- [Java&操作系统基础](#Java&操作系统基础)
    - [Java引用](#Java引用) 
    - [多线程](#多线程) 
    - [I/O](#I/O)     
    - [零拷贝](#零拷贝)       
    - [伪共享](#伪共享)     
- [网络](#网络)
    - [TCP](#TCP)
- [数据结构](#数据结构)
    - [BitMap](#BitMap)    
- [算法](#算法)
 
 
   
# 架构设计
## 架构的定义
**软件架构定义（之一）：** 软件架构是解释该系统所需的结构体的集合，其中包括：软件元素、元素之间的相互关系，以及二者各自的属性。 
* 架构是必须在项目早期作出的一组设计决策。这通常也被非正式的称为“那些在项目后期难以改变的内容”。
* 架构是对系统恰如其分的施加约束，以便系统获得我们所需质量属性的一门艺术。
* 架构并不仅仅只是设计的宏观部分，如果细节关乎系统的整体质量，那么这些细节也应该属于架构层面的内容。
* 任何软件系统都有自己的架构，架构是客观存在的。

## 微服务架构
**微服务定义：** 微服务是以单一应用程序构成的小服务，自己拥有独立的进程，服务依赖业务功能的设计，以全自动的方式部署，与其他服务使用轻量级的通信协议（例如HTTP
）。同时服务会使用最小的规模的集中管理能力，服务可以用不同的编程语言与数据库等组件实现。

微服务架构是一种架构风格。

## GoF的23种设计模式

### 接口型模式
**适配器模式（Adapter）**<br />
将一个类的接口转换成客户希望的另外一个接口，使得原本由于接口不兼容而不能一起工作的那些类能一起工作。

**外观模式（Facade）**<br />
为多个复杂的子系统提供一个一致的接口，使这些子系统更加容易被访问。

**合成模式（Composite）**<br />
将对象组合成树状层次结构，使用户对单个对象和组合对象具有一致的访问性。

**桥接模式（Bridge）**<br />
将抽象与实现分离，使它们可以独立变化。它是用组合关系代替继承关系来实现，从而降低了抽象和实现这两个可变维度的耦合度。

### 职责型模式
**单例模式（Singleton）**<br />
某个类只能生成一个实例，该类提供了一个全局访问点供外部获取该实例，其拓展是有限多例模式。

**观察者模式（Observer）**<br />
多个对象间存在一对多关系，当一个对象发生改变时，把这种改变通知给其他多个对象，从而影响其他对象的行为。

**调停者模式（Mediator）**<br />
定义一个中介对象来简化原有对象之间的交互关系，降低系统中对象间的耦合度，使原有对象之间不必相互了解。

**代理模式（Proxy）**<br />
为某对象提供一种代理以控制对该对象的访问。即客户端通过代理间接地访问该对象，从而限制、增强或修改该对象的一些特性。

**职责链模式（Chain of Responsibility）**<br />
把请求从链中的一个对象传到下一个对象，直到请求被响应为止。通过这种方式去除对象之间的耦合。

**享元模式（Flyweight）**<br />
运用共享技术来有效地支持大量细粒度对象的复用。

### 构造型模式
**建造者模式（Builder）**<br />
将一个复杂对象分解成多个相对简单的部分，然后根据不同需要分别创建它们，最后构建成该复杂对象。

**工厂方法模式（Factory Method）**<br />
定义一个用于创建产品的接口，由子类决定生产什么产品。

**抽象工厂模式（Abstract Factory）**<br />
提供一个创建产品族的接口，其每个子类可以生产一系列相关的产品。

**原型模式（Prototype）**<br />
将一个对象作为原型，通过对其进行复制而克隆出多个和原型类似的新实例。

**备忘录模式（Memento）**<br />
在不破坏封装性的前提下，获取并保存一个对象的内部状态，以便以后恢复它。

### 操作型模式

**模板方法模式（TemplateMethod）**<br />
定义一个操作中的算法骨架，而将算法的一些步骤延迟到子类中，使得子类可以不改变该算法结构的情况下重定义该算法的某些特定步骤。

**状态模式（State）**<br />
允许一个对象在其内部状态发生改变时改变其行为能力。

**策略模式（Strategy）**<br />
定义了一系列算法，并将每个算法封装起来，使它们可以相互替换，且算法的改变不会影响使用算法的客户。

**命令模式（Command）**<br />
将一个请求封装为一个对象，使发出请求的责任和执行请求的责任分割开。

**解释器模式（Interpreter）**<br />
提供如何定义语言的文法，以及对语言句子的解释方法，即解释器。

### 扩展型模式

**装饰器模式（Decorator）**<br />
动态的给对象增加一些职责，即增加其额外的功能。

**迭代器模式（Iterator）**<br />
提供一种方法来顺序访问聚合对象中的一系列数据，而不暴露聚合对象的内部表示。

**访问者模式（Visitor）**<br />
在不改变集合元素的前提下，为一个集合中的每个元素提供多种访问方式，即每个元素有多个访问者对象访问。

## 面向对象设计原则
最基本的五大设计原则（SOLID）：单一职责原则、开放封闭原则、里式替换原则、接口隔离原则和依赖倒置原则。

## 业务系统架构设计的基本原则
业务系统架构设计四要素：

**1. 可维护性是根本**
* 代码可读性很关键
* 设计权衡时优先考虑简单设计
* 打造可扩展系统

**2. 稳定性是底线**
* 充分了解背后的非功能性诉求
* 尽可能做到可降级
* 实现异常出口

**3. 多参考业界的成功模式**
* GoF的23种设计模式
* 面向对象的X大设计原则
* 业界现有的设计案例

**4. 选择最恰当的设计方案**
* 中间件的设计方式不一定适合业务系统
* 方案选型要考虑团队的技能水位
* 方案要符合项目当前的发展阶段（超前设计需谨慎）
* 重点评估方案的维护成本
* 多套方案中选择最合适的方案

## 响应式编程(Reactive)
在开发应用程序代码时，我们可以编写两种风格的代码，即命令式和反应式。
* 命令式（Imperative）的代码：它由一组任务组成，每次只运行一项任务，每项任务又都依赖于前面的任务。我们一次一个地按照顺序将代码编写为需要遵循的指令列表。在某项任务开始执行之后，程序在开始下一项任务之前需要等待当前任务完成。在整个处理过程中的每一步，要处理的数据都必须是完全可用的，以便将它们作为一个整体进行处理。
* 响应式（Reactive）的代码：它定义了一组用来处理数据的任务，但是这些任务可以并行地执行。每项任务处理数据的一部分子集，并将结果交给处理流程中的下一项任务，同时继续处理数据的另一部分子集。相对于要求将被处理的数据作为一个整体进行处理，反应式流可以在数据可用时立即开始处理。实际上，传入的数据可能是无限的（比如，一个某个地理位置的实时温度测量数据的恒定流）。

**参考资料：**<br />
* 《恰如其分的软件架构》
* https://blog.christianposta.com/microservices/when-not-to-do-microservices/
* 《Java设计模式（第2版）》
* 《Spring实战（第5版）》
* https://www.reactivemanifesto.org/
* https://www.reactive-streams.org/
* https://projectreactor.io/docs/core/release/reference/index.html
* https://github.com/reactor/lite-rx-api-hands-on
* https://www.xncoding.com/2018/04/05/java/reactor.html
* http://gee.cs.oswego.edu/dl/cpjslides/nio.pdf
* https://docs.spring.io/spring-framework/docs/current/reference/html/web-reactive.html#webflux-concurrency-model

# 云原生
## 定义
云原生技术有利于各组织在公有云、私有云和混合云等新型动态环境中，构建和运行可弹性扩展的应用。
云原生的代表技术包括容器、服务网格、微服务、不可变基础设施和声明式API。这些技术能够构建容错性好、易于管理和便于观察的松耦合系统。结合可靠的自动化手段，云原生技术使工程师能够轻松地对系统作出频繁和可预测的重大变更。
云原生计算基金会（CNCF）致力于培育和维护一个厂商中立的开源生态系统，来推广云原生技术。我们通过将最前沿的模式民主化，让这些创新为大众所用。

**参考资料：**
* https://github.com/cncf/toc/blob/master/DEFINITION.md
* https://jimmysong.io/kubernetes-handbook/cloud-native/cloud-native-definition.html

## Docker
定义：Docker是一个Go语言开源的应用容器引擎。Docker可以让开发者打包他们的应用以及依赖包到一个轻量级、可移植的容器中，然后发布到任何流行的Linux机器上，也可以实现虚拟化。

### 镜像
镜像是什么呢？通俗地讲，它是一个只读的文件和文件夹组合。它包含了容器运行时所需要的所有基础文件和配置信息，是容器启动的基础。所以你想启动一个容器，那首先必须要有一个镜像。镜像是 Docker 容器启动的先决条件。

### 容器
容器是什么呢？容器是 Docker 的另一个核心概念。通俗地讲，容器是镜像的运行实体。镜像是静态的只读文件，而容器带有运行时需要的可写文件层，并且容器中的进程属于运行状态。即容器运行着真正的应用进程。容器是基于镜像创建的可运行实例，并且单独存在，一个镜像可以创建出多个容器。运行容器化环境时，实际上是在容器内部创建该文件系统的读写副本。容器有初建、运行、停止、暂停和删除五种状态。

### Docker与虚拟机的区别
![Docker和虚拟机的区别](https://user-images.githubusercontent.com/6687462/99140541-bf77d080-267d-11eb-8ae7-87dedc861035.jpeg)

### Docker常用命令
* docker run --cpus=1 -m=1g --name=nginx -d nginx 
* docker run --privileged=true --publish 2181:2181 -d zookeeper:latest
* docker run -p 8080:8080 -d dubbo-admin
* docker exec -it busybox sh

**参考资料：**<br />
* https://kaiwu.lagou.com/course/courseInfo.htm?courseId=455#/content?courseId=455

## ServiceMesh(服务网格)
定义：服务网格是一个基础设施层，用于处理服务间通信。云原生应用有着复杂的服务拓扑，服务网格保证请求在这些拓扑中可靠地穿梭。在实际应用当中，服务网格通常是由一系列轻量级的网络代理组成的，它们与应用程序部署在一起，但对应用程序透明。

## Serverless(无服务器)
**定义：** Serverless是指构建和运行不需要服务器管理的应用程序的概念。它描述了一个更细粒度的部署模型，在这个模型中，应用程序捆绑成一个或多个功能，被上传到一个平台，然后根据当前确切需求进行执行、缩放和计费。
Serverless利用现代云计算功能和抽象的优势，让您专注于业务逻辑而不是基础架构。在无服务器环境中，您可以专注于编写应用程序代码，而基础平台则负责自动扩容、资源分配、安全性以及其他“服务器”方面的细节。

**特性:**
1. 带触发器的事件驱动代码执行。
2. 平台处理所有运行，停止和缩放的琐事。
3. 缩放为零，空闲时成本低至零。
4. 无状态。

**参考资料：**<br />
* https://spring.io/serverless
* https://developer.aliyun.com/article/574222

# 存储

## RDS

### MySQL
**MGR**<br />
即MySQL Group Replication，是官方提供的MySQL高可用解决方案。我们知道创建容错系统的常见方式是使组件冗余，对于MySQL而言，最终的挑战是将数据复制的逻辑与多个服务器以一致且简单的方式进行协调的逻辑相融合。换句话说，要让多个服务器就系统的状态以及系统所经历的每一次更改的数据达成一致。<br />
MGR为分布式状态机复制提供了服务器之间的强大协调能力，当服务器属于同一组时，它们会自动进行协调。该组可以在具有自动选主（单主）的模式下运行，仅一个服务器接受更新。对于更高级的用户，可以在多主模式下部署，在该模式下，所有服务器都可以接受更新，这种能力的代价是应用程序必须解决此类部署所施加的限制。<br />
所有这些均由组通信系统（Group Communication System，即GCS）协议提供支持，它提供故障检测机制，组成员安全且有序的传递消息，该技术的核心是Paxos算法的实现。

**经典MySQL异步复制和MGR之间的区别**
MySQL异步复制：MySQL提供了两种异步复制机制，一种是“异步复制”，即主执行事务，提交事务，然后将它们稍后（因此异步）发送到从副本以重新执行（在基于语句的复制中）或应用（在基于行的复制中）.<br />
![MySQL异步复制](https://user-images.githubusercontent.com/6687462/86524229-87c87300-beaa-11ea-8ac8-6db2206bfb61.png)<br />
另一种是“半同步复制”，即主执行事务，在等待从服务器确认已接收到事务后再提交事务。<br />
![MySQL半同步复制](https://user-images.githubusercontent.com/6687462/86524236-a29ae780-beaa-11ea-87b0-81d61a748b4d.png)<br />
MGR:<br />
![MGR](https://user-images.githubusercontent.com/6687462/86524273-20f78980-beab-11ea-9fa9-af6e9bb94acf.png)<br />

**binlog、redolog、undolog**<br />
binlog：MySQL Server层记录的归档日志，Base64编码的二进制格式，用于恢复数据和复本同步。binlog采用的是顺序追加写。<br />
redolog：InnoDB存储引擎层的重做日志，确保事务的持久性。防止在发生故障的时间点，尚有脏页未写入磁盘，在重启MySQL服务的时候，根据redolog进行重做，从而保证事务的持久性。redolog采用的是循环写，即固定文件大小，如果写到文件末尾，又从头写。<br />
undolog：InnoDB存储引擎层的回滚日志，保存了事务发生之前的数据的一个版本，用于事务的回滚。<br />

**参考资料：**<br />
* https://dev.mysql.com/doc/refman/8.0/en/group-replication.html
* https://dev.mysql.com/doc/refman/8.0/en/binlog.html

## NoSQL
NoSQL常见的四种类型：键值对型、文档型、列式存储型和图型。

### Redis
**定义**<br />
Redis是一种采用内存来作为数据结构存储的数据库、缓存和消息代理。<br />

**部署说明**<br />
Redis是用ANSI C编写，并且可以在大多数POSIX系统中使用，例如Linux，* BSD，OS X，而无需外部依赖。Linux和OS X是Redis开发和测试最多的两个操作系统，我们建议使用Linux进行部署。<br/>

**内部数据结构**<br />
简单动态字符串(Simple Dynamic Strings, SDS)、双端链表、跳跃表(skiplist)、压缩列表、快速列表(Redis3.2引入，quicklist)、字典(散列表)、整数集合(intset)

**支持的数据结构**<br />
字符串，哈希，列表，集合，带范围查询的排序集合，位图，HyperLogLog，地理空间索引。<br/>

**Redis是单线程的。如何利用多个多核CPU？**<br />
CPU成为Redis瓶颈的情况并不常见，因为Redis通常是内存或网络绑定的。例如，在一个普通的Linux系统上运行的流水线Redis每秒甚至可以传递100万个请求，所以如果您的应用程序主要使用O（N）或O（log（N））命令，它几乎不会占用太多的CPU。
但是，为了最大限度地利用CPU，可以在同一个机器中启动多个Redis实例，并将它们视为不同的服务器。然而，随着Redis 4.0的推出，我们开始让Redis多线程化。目前，这仅限于在后台删除对象，以及阻止通过Redis模块实现的命令。对于未来的版本，计划是让Redis越来越多线程化。

**Redis6的多线程特性**
Redis的多线程部分只是用来处理网络数据的读写和协议解析，执行命令仍然是单线程顺序执行。所以我们不需要去考虑控制 key、lua、事务，LPUSH/LPOP 等等的并发及线程安全问题。

**持久化方案**<br />
Redis持久化方案分为RDB和AOF两种。<br/>
RDB：按指定的时间间隔执行数据集的时间点快照。 <br />
AOF：会记录服务器接收的每个写入操作，这些操作将在服务器启动时再次播放，以重建原始数据集。使用与Redis协议本身相同的格式记录命令，并且采用追加方式。当日志太大时，Redis可以在后台重写日志。 

注意，可以在同一实例中同时合并AOF和RDB。在这种情况下，当Redis重新启动时，将使用AOF文件用于重建原始数据集，因为它可以保证是最完整的。

**RDB优势**<br/>
1. RDB是Redis数据的非常紧凑的单文件时间点表示。RDB文件非常适合备份。可以在灾难发生时轻松将数据恢复到不同版本。
2. 支持文件上传来远程恢复。
3. RDB最大限度地提高了Redis的性能，因为Redis父进程为了持久化而需要做的唯一工作就是forking一个子进程，其余的都交给子进程来做，父实例将永远不会执行磁盘I/O或类似操作。
4. 与AOF相比，采用RDB方式来重启Redis将更快。

**RDB劣势**<br/>
1. 在断电等没有正确关闭的情况下停止工作之后）存在数据丢失的可能。
2. RDB需要经常使用fork()才能使用子进程将其持久化在磁盘上。如果数据集很大，Fork()可能很耗时，如果机器CPU性能不佳，则可能导致Redis停止为客户端服务几毫秒甚至一秒钟。AOF也需要fork()，但我们可以控制重写日志的频率，而无需权衡持久性。

**AOF优势**<br/>
1. 使用AOF Redis更加持久：您可以使用不同的fsync策略：完全没有fsync，每秒fsync，每个查询fsync。使用fsync的默认策略，每秒的写入性能仍然很好（fsync是使用后台线程执行的，并且当没有fsync进行时，主线程将尽力执行写入操作。）但是您只能损失一秒钟的写入时间。
2. AOF以易于理解和解析的格式包含所有操作的日志。您甚至可以轻松导出AOF文件，在某些情况下，便于我们分析Redis的所有操作。

**AOF劣势**<br/>
1. 对于同一数据集，AOF文件通常大于等效的RDB文件。
2. 精确的fsync策略可能会导致AOF可能比RDB慢。通常情况下，设置每秒一次fsync性能仍然很高，并且在禁用fsync的情况下，即使在高负载下，它也应与RDB一样快。即使在巨大的写负载的情况下，RDB仍然能够提供有关最大延迟的更多保证。
3. AOF通过像MySQL或MongoDB那样增量地更新现有状态来工作，而RDB快照一次又一次地创建所有内容，从概念上讲，它更健壮。

如果您要增加一个计数器100次，最终将在数据集中包含最终值的键只有一个，而在AOF中却包含100个条目。不需要其中的99个条目来重建当前状态。因此，Redis支持一个有趣的功能：它能够在后台重建AOF，而不会中断对客户端的服务。每当您发出BGREWRITEAOF时， Redis都会编写最短的命令序列来重建内存中的当前数据集。如果您将AOF与Redis 2.2一起使用，则需要不时运行BGREWRITEAOF。Redis 2.4能够自动触发日志重写。

**复本机制：**<br/>
1. Redis支持主从模式，默认采用异步复制的方式，如果对强一致性有要求，可以使用同步复制。
2. Redis支持将多个副本连接到同一主副本，并且副本还可以按级联结构连接到其他副本。从Redis 4.0开始，所有子副本将从主服务器接收完全相同的数据流。
3. Redis复制时在Master上是无阻塞的。这意味着当一个或多个副本执行初始同步或部分重新同步时，主服务器将继续处理查询。

**高可用：**<br/>
Redis官方提供的高可用方案分为Redis Sentinel和Redis Cluster两种。<br/>
Redis Sentinel<br/>
这是宏观上Sentinel功能的完整列表（即，大图）：
* 监控。Sentinel会不断检查您的主实例和副本实例是否按预期工作。
* 通知。Sentinel可以通过API通知系统管理员或其他计算机程序，其中一个受监视的Redis实例出了问题。
* 自动故障转移。如果主服务器未按预期工作，则Sentinel可以启动故障转移过程，在该过程中将副本升级为主服务器，将其他附加副本重新配置为使用新的主服务器，并通知使用Redis服务器的应用程序要使用的新地址。连接时。
* 配置提供程序。Sentinel充当客户端服务发现的权威来源：客户端连接到Sentinels，以询问负责给定服务的当前Redis主服务器的地址。如果发生故障转移，Sentinels将报告新地址。

1. 当多个哨兵就给定的主机不再可用这一事实达成共识时，将执行故障检测。这降低了误报的可能性。
2. 即使不是所有的Sentinel进程都在工作，Sentinel仍能正常工作，从而使系统能够应对故障。毕竟，拥有故障转移系统本身就是一个单点故障，这没有任何意思。
3. 一个健壮的部署至少需要三个Sentinel实例。
4. Sentinels，Redis实例（主服务器和副本）以及连接到Sentinel和Redis的客户端的总和也是具有特定属性的大型分布式系统。

**分布式锁:**<br/>
有许多库和博客文章描述了如何使用Redis实现DLM（Distributed Lock Manager 分布式锁管理器），但每个库都使用不同的方法，与使用稍微复杂一点的方法相比，许多库使用的方法具有较低的保证设计。
本页面试图提供一种更规范的算法来使用Redis实现分布式锁。我们提出了一种称为Redlock的算法，它实现了我们认为比普通单实例方法更安全的DLM。
我们将仅使用三个属性对我们的设计进行建模，从我们的角度来看，这是以有效方式使用分布式锁所需的最低保证。
* Safety property：互斥。在任何给定时刻，只有一个客户端可以持有锁。
* Liveness property A：无死锁。最终总是有可能获得锁，即使锁定资源的客户端崩溃或被分区。
* Liveness property B：容错。只要大多数Redis节点都已启动，客户端就可以获取和释放锁。
为什么基于故障转移的实现是不够的?
为了了解我们想要改进的地方，让我们分析大多数基于Redis的分布式锁库的当前状态。使用Redis锁定资源的最简单方法是在实例中创建密钥。密钥通常是在有限的生存时间内创建的，使用Redis过期功能，以便最终将其释放（我们列表中的属性 2）。当客户端需要释放资源时，它会删除密钥。
从表面上看，这很有效，但有一个问题：这是我们架构中的单点故障。如果Redis master宕机了怎么办？好吧，让我们添加一个奴隶！如果主人不可用，请使用它。不幸的是，这是不可行的。这样做我们无法实现互斥的安全属性，因为 Redis 复制是异步的。
这个模型有一个明显的竞争条件：
1.客户端 A 获取了 master 中的锁。
2.在对密钥的写入传输到从站之前，主站崩溃。
3.奴隶被提升为主人。
4.客户端B获取对A已经持有锁的同一资源的锁。违反安全！
有时，在特殊情况下（例如在失败期间），多个客户端可以同时持有锁是完全没问题的。如果是这种情况，您可以使用基于复制的解决方案。否则，我们建议实施本文档中描述的解决方案。

### Elasticsearch
**定义**<br />
Elasticsearch是一个分布式、RESTful风格的搜索和数据分析引擎。<br />
它为所有类型的数据提供近乎实时的搜索和分析，无论您是结构化文本还是非结构化文本，数字数据或地理空间数据，Elasticsearch都能以支持快速搜索的方式有效地对其进行存储和索引。
**特点**<br />
建立在Apache Lucene之上、分布式、高可用、多租户、API丰富、面向文档；
**配合使用**<br />
Logstash|Beats（收集） + Elasticsearch（存储、分析） + Kibana（展现）

**扩展知识点：** HyperLogLog<br />

**参考资料：** 
* https://redis.io/
* https://redis.io/topics/distlock
* http://doc.redisfans.com/
* https://www.elastic.co/cn/elasticsearch/
* https://github.com/elastic/elasticsearch
* https://redis.io/topics/faq
* https://www.cnblogs.com/madashu/p/12832766.html

# 分布式系统

## 常见的一致性算法
### 2PC&3PC
**2PC**<br />
**角色**：事务参与方、事务协调者<br />
**Two-phaseCommit**：第一阶段——准备阶段(投票阶段)、第二阶段——提交阶段（执行阶段）。<br />
**优点**：<br />

**缺点**：<br />
* 性能问题:无论是在第一阶段的过程中,还是在第二阶段,所有的参与者资源和协调者资源都是被锁住的,只有当所有节点准备完毕，事务协调者才会通知进行全局提交，
参与者 进行本地事务提交后才会释放资源。这样的过程会比较漫长，对性能影响比较大。
* 单节点故障:由于协调者的重要性，一旦协调者发生故障。参与者会一直阻塞下去。尤其在第二阶段，协调者发生故障，那么所有的参与者还都处于锁定事务资源的状态中，而无法继续完成事务操作。

**3PC**<br />
**角色**：事务参与方、事务协调者<br />
**Three-phaseCommit**：第一阶段——CanCommit、第二阶段——PreCommit、第三阶段——DoCommit。<br />
**和2PC区别**：
3PC主要是为了解决两阶段提交协议的阻塞问题，2PC存在的问题是当协作者崩溃时，参与者不能做出最后的选择（因为参与者不知道其他参与者CanCommit的结果），因此参与者可能在协作者恢复之前保持阻塞。
1、引入超时机制。同时在协调者和参与者中都引入超时机制。
2、在第一阶段和第二阶段中插入一个准备阶段。保证了在最后提交阶段之前各参与节点的状态是一致的。
![3PC](https://user-images.githubusercontent.com/6687462/123544788-71848880-d787-11eb-9995-16956d31d416.png)
**优点**：<br />
**缺点**：<br />

### TCC（Try-Confirm-Cancel）

### Paxos
Paxos算法是莱斯利·兰伯特(Leslie Lamport)1990年提出的一种基于消息传递的一致性算法，其解决的问题是分布式系统如何就某个值(决议)达成一致。

### Raft

### Gossip
### ZAB

## ZooKeeper
定义：ZooKeeper是一个分布式协作框架，用于维护配置信息，命名，提供分布式同步以及提供组服务。

## RPC框架
### Dubbo

## MQ

### Kafka
#### 生产者

#### 消费者
**关于订阅**
* 消费者可以单独订阅分区：可以单独订阅某个Topic的某个分区（assign）
* 消费者可以多订阅：一个消费者可以订阅多个Topic（Topic列表或者Topic名称的正则）
* 基于拉模式：Kafka中的消费是基于拉模式的，一个Topic分区的消息只会被所有订阅消费组中的一个消费者拉到
* 支持正则：使用Topic的正则时新增的Topic会主动订阅
* 消费方式互斥：集合订阅的方式subscribe（Collection）、正则表达式订阅的方式subscribe（Pattern）和指定分区的订阅方式 assign（Collection）分表代表了三种不同的订阅状态：AUTO_TOPICS、AUTO_PATTERN和USER_ASSIGNED（如果没有订阅，那么订阅状态为NONE）。然而这三种状态是互斥的，在一个消费者中只能使用其中的一种
* 位移提交：默认的消费位移的提交方式是自动提交，默认的自动提交不是每消费一条消息就提交一次，而是定期提交，这个定期的周期时间由客户端参数auto.commit.interval.ms配置，默认值为5秒，此参数生效的前提是enable.auto.commit参数为true。
* 新生消费者：每当消费者查找不到所记录的消费位移时，就会根据消费者客户端参数auto.offset.reset的配置来决定从何处开始进行消费，这个参数的默认值为“latest”，表示从分区末尾开始消费消息。



# Web服务器

## Nginx

## Tomcat

# DevOps
## DevOps定义
DevOps是一组用于促进开发和运维人员之间协作以达到缩短软件交付周期的过程、方法和系统的统称。

## 持续集成
持续集成成指的是在软件开发过程中，软件开发人员持续不断地将开发出来的代码和其他的开发人员的代码进行合并，每次合并后自动地进行编译、构建，并运行自动化测试进行验证，而不是等到最后各自开发完成后才合并在一起。持续集成能从根本上提高一个团队的软件开发效率。在软件开发过程中引入持续集成，可以帮助团队及时的发现系统中的问题，并快速做出修复，不仅可以缩短软件开发的时间，而且可以交付更具质量的系统。

**参考资料**<br />
* https://www.infoq.cn/article/pB7D0l9Ho190UWPvM4tZ?utm_source=related_read_bottom&utm_medium=article
* http://book.mixu.net/distsys/index.html  --Distributed systems for fun and profit
* http://principles-wiki.net/principles:fallacies_of_distributed_computing  
* https://www.the-paper-trail.org/post/2014-08-09-distributed-systems-theory-for-the-distributed-systems-engineer/
* https://www.somethingsimilar.com/2013/01/14/notes-on-distributed-systems-for-young-bloods/
* http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.41.7628&rep=rep1&type=pdf
* https://mercyblitz.github.io/2020/05/11/Apache-Dubbo-%E6%9C%8D%E5%8A%A1%E8%87%AA%E7%9C%81%E6%9E%B6%E6%9E%84%E8%AE%BE%E8%AE%A1/
* https://blog.csdn.net/alisystemsoftware/article/details/106615082
* http://thesecretlivesofdata.com/raft/
* 《深入理解Kafka：核心设计与实践原理》
* https://www.cnblogs.com/qdhxhz/p/11167025.html
* https://zhuanlan.zhihu.com/p/21994882
* http://www.tianshouzhi.com/api/tutorials/distributed_transaction/388


# 基础框架
## Spring
Spring中最核心的接口是BeanFactory，它是我们访问Spring Bean容器的根接口，里面定义了很多通过名字或类型来获取Bean的方法，BeanFactory提供了一种高级配置机制，能够管理任何类型的对象。<br />
Spring中另一个核心接口是ApplicationContext，它是BeanFactory的子接口，它提供了如下功能：
1. 与Spring的AOP功能轻松集成
2. 消息资源处理（用于国际化）
3. 事件发布
4. 应用层特定的上下文，例如WebApplicationContext用于Web应用程序中的。

简而言之，BeanFactory提供了配置框架和基本功能，并ApplicationContext增加了更多针对企业的功能。

**IoC**
org.springframework.beans和org.springframework.context包是Spring框架的IoC容器的基础。

**AOP**
Spring通过使用基于Schema的方法或@AspectJ注释样式，提供了编写自定义方面的简单而强大的方式。<br />
**AOP核心概念**<br />
切面（Aspect）：横跨多个类的关注点的模块化<br />
连接点（Join point）：程序执行期间的一个点，在Spring AOP中，连接点总是表示一个方法的执行。<br />
增强（Advice）：一个切面在特定连接点所采取的操作。不同类型的建议包括“around”、“before”和“after”增强。许多AOP框架，包括Spring，都将一个增强建模为一个拦截器，并在连接点周围维护一个拦截器链。
切入点（Ponitcut）：匹配连接点的谓词。Advice与切入点表达式相关联，并在与切入点匹配的任何连接点上运行（例如，使用特定名称的方法的执行）。与切入点表达式匹配的连接点的概念是AOP的核心，Spring默认使用AspectJ切入点表达式语言。
目标对象(Target object)：一个或多个方面建议的对象。也称为“建议对象”。由于Spring AOP是使用运行时代理实现的，因此该对象始终是代理对象。
AOP代理(AOP proxy)：由AOP框架创建的一个对象，用于实现切面合同（增强方法执行等）。在Spring Framework中，AOP代理是JDK动态代理或CGLIB代理。

Spring AOP并未想和AspectJ竞争以提供全面的AOP解决方案，而是和Spring IoC和AspectJ结合，Spring AOP默认将标准JDK动态代理用于AOP代理。这使得可以代理任何接口（或一组接口）。Spring AOP也可以使用CGLIB代理。这对于代理类而不是接口是必需的。默认情况下，如果业务对象未实现接口，则使用CGLIB。

## SpringBoot
**目的：** Spring Boot是为了让我们创建独立的基于Spring的产品级应用更容易，Spring Boot采用"约定优于配置"的思路，让我们只需要少量配置就可以启用Spring Boot应用，降低了Spring应用的建设成本。

**特征**<br />
* 直接嵌入Tomcat，Jetty或Undertow（无需部署WAR文件）。
* 提供“starter”依赖项，以简化构建配置。
* 尽可能自动配置Spring和第三方库。
* 提供可用于生产的功能，例如指标，运行状况检查和外部化配置。
* 完全没有代码生成，也不需要XML配置。

**外部化配置（Externalized Configuration）**<br />
Spring Boot使您可以外部化配置，以便可以在不同环境中使用相同的应用程序代码。您可以使用属性文件，YAML文件，环境变量和命令行参数来外部化配置。属性值可以通过直接注射到你的bean @Value注释，通过Spring的访问Environment抽象，或者通过@ConfigurationProperties绑定到结构化对象。

**自动配置**<br />
您需要非常注意添加bean定义的顺序，因为这些条件是根据到目前为止已处理的内容来评估的。因此，我们建议仅在自动配置类上使用@ConditionalOnBean和@ConditionalOnMissingBean
注释（因为保证在添加任何用户定义的Bean定义后才会加载这些注释）。

## Netty
**Netty5变化**
* 简化的处理程序类型层次结构：ChannelInboundHandler并ChannelOutboundHandler已合并为ChannelHandler。ChannelHandler
现在具有入站和出站处理程序方法。ChannelInboundHandlerAdapter，ChannelOutboundHandlerAdapter和，ChannelDuplexHandlerAdapter已被弃用，并由代替ChannelHandlerAdapter。由于现在无法确定处理程序是入站处理程序还是出站处理程序，因此CombinedChannelDuplexHandler已被替换ChannelHandlerAppender。
* 更加灵活的线程模型：
在Netty 4.x中，每个EventLoop线程都与固定线程紧密耦合，该线程执行其注册的所有I / O事件Channels以及提交给它的所有任务。
从版本5.0开始，EventLoop不再使用线程，而是使用Executor抽象。也就是说，它将Executor对象作为其构造函数中的参数，而不是在无穷循环中轮询I / O事件，每个迭代现在都是提交给this的任务Executor。
如果未指定，Executor默认情况下使用ForkJoinPool。AForkJoinPool具有使用线程本地队列的不错的属性。也就是说，提交给ForkJoinPoolfrom的任务Thread A很可能由执行Thread A again。这应该提供EventLoops高级别的线程亲和力。
此外，开发人员还可以提供自己的Executor（也称为线程池）并接管的调度EventLoops。当Netty用作大型软件系统的一部分时，这可能证明是有用的。假设该系统已经使用具有高度并行性的线程池来最佳地执行其所有任务。Netty 4.x只会产生自己的线程，而完全忽略它是更大系统的一部分的事实。从Netty 5.0开始，开发人员可以在同一线程池中运行Netty和系统的其余部分，并通过应用更好的调度策略和更少的调度开销（由于线程数减少）来潜在地提高性能。有关此更改的详细讨论，请查看GitHub第2250期。
应该提到的是，这种改变绝不影响ChannelHandlers开发的方式。从开发人员的角度来看，唯一改变的是不再保证aChannelHandler将始终由同一线程执行。但是，可以保证它永远不会被两个或多个线程同时执行。此外，Netty还可以解决可能发生的任何内存可见性问题。因此，无需担心volatile内的线程安全性和变量ChannelHandler。
这种变化的一个意义是NioEventLoop，NioEventLoopGroup，EpollEventLoop和 EpollEventLoopGroup做不再需要ThreadFactory的对象构造函数的参数。这些类的构造函数已更新为使用Executor和ExecutorFactory对象。



**参考资料**<br />
* https://spring.io/projects/spring-boot#overview
* https://netty.io/wiki/new-and-noteworthy-in-5.0.html
* https://netty.io/wiki/new-and-noteworthy-in-4.1.html
* https://netty.io/wiki/new-and-noteworthy-in-4.0.html



# 常见工具
## Arthas


# JVM
## 运行时数据区域
线程私有的内存区域有程序计数器、Java虚拟机栈和本地方法栈，程序计数器是Java虚拟机规范中唯一没有要求OOM的地方；<br />
线程公用的有堆和方法区，方法区在JDK8之前的HotSpot叫做永久代，在JDK8以及之后叫做元数据区，元数据区作为直接内存来管理，只受操作系统内存的限制。<br />

## 垃圾收集算法
主要是标记-清除、标记-复制和标记-整理三种。<br />
**标记-清除** 该算法有两个缺点，一个是效率不稳定，如果大量对象都需要标记和清除的话，开销会比较大，另一个是会导致碎片化严重，导致给新对象分配内存空间时需要进行碎片整理，增加了运行时内存分配的成本。<br />
**标记-复制** 如果每次只有少量对象存活（例如新生代内的对象就是如此），那么只需要保留（复制）这少量对象就行了，所以有人提出了该算法，“半区复制”（Semispace Copying）的垃圾收集算法，它将可用内存按容量划分为大小相等的两块，每次只使用其中的一块。当这一块的内存用完了，就将还存活着的对象复制到另外一块上面，然后再把已使用过的内存空间一次清理掉。<br />
**标记-整理** 如果每次都会有大量对象存活（例如老年代），那么标记-复制算法需要复制的对象数量将很多，标记过程仍然与“标记-清除”算法一样，但后续步骤不是直接对可回收对象进行清理，而是让所有存活的对象都向内存空间一端移动，然后直接清理掉边界以外的内存。


## 垃圾收集器
大多数垃圾收集器都遵循分代收集理论（G1除外），一般把堆分为新生代和老年代。

部分收集（Partial GC）：指目标不是完整收集整个Java堆的垃圾收集。<br />
新生代收集（Minor GC/Young GC）：指目标只是新生代的垃圾收集。<br />
老年代收集（Major GC/Old GC）：指目标只是老年代的垃圾收集。目前只有CMS收集器会有单独收集老年代的行为。另外请注意“Major GC”这个说法现在有点混淆，在不同资料上常有不同所指，读者需按上下文区分到底是指老年代的收集还是整堆收集。<br />
混合收集（Mixed GC）：指目标是收集整个新生代以及部分老年代的垃圾收集。目前只有G1收集器会有这种行为。<br />
整堆收集（Full GC）：收集整个Java堆和方法区的垃圾收集。<br />

**CMS(Concurrent Mark Sweep)**
1. 初始标记（CMS initial mark）：标记一下GC Roots能直接关联到的对象，速度很快，但会Stop The World。
2. 并发标记（CMS concurrent mark）：从GC Roots的直接关联对象开始遍历整个对象图的过程，这个过程耗时较长但是可以与用户线程一起并发运行；
3. 重新标记（CMS remark）：为了修正并发标记期间，因用户程序继续运作而导致标记产生变动的那一部分对象的标记记录，这个阶段的停顿时间通常会比初始标记阶段稍长，但也远比并发标记阶段的时间短，该阶段也会Stop The World；
4. 并发清除（CMS concurrent sweep）：清理删除掉标记阶段判断的已经死亡的对象，由于不需要移动存活对象，所以这个阶段也是可以与用户线程同时并发的。

**G1(Garbage First)**
在G1收集器出现之前的所有其他收集器，包括CMS在内，垃圾收集的目标范围要么是整个新生代（Minor GC），要么就是整个老年代（Major GC），再要么就是整个Java堆（Full GC）。而G1跳出了这个樊笼，它面向堆内存任何部分来组成回收集（Collection Set，一般简称CSet）进行回收，衡量标准不再是它属于哪个分代，而是哪块内存中存放的垃圾数量最多，回收收益最大，这就是G1收集器的Mixed GC模式。<br />
G1不再坚持固定大小以及固定数量的分代区域划分，而是把连续的Java堆划分为多个大小相等的独立区域（Region），每一个Region都可以根据需要，扮演新生代的Eden空间、Survivor空间，或者老年代空间。收集器能够对扮演不同角色的Region采用不同的策略去处理，这样无论是新创建的对象还是已经存活了一段时间、熬过多次收集的旧对象都能获取很好的收集效果。<br />
Region中还有一类特殊的Humongous区域，专门用来存储大对象。G1认为只要大小超过了一个Region容量一半的对象即可判定为大对象。每个Region的大小可以通过参数-XX：G1HeapRegionSize设定，取值范围为1MB～32MB，且应为2的N次幂。而对于那些超过了整个Region容量的超级大对象，将会被存放在N个连续的Humongous Region之中.<br />
G1收集器的运作过程大致可划分为以下四个步骤：<br />
1. 初始标记（Initial Marking）：标记一下GC Roots能直接关联到的对象，并且修改TAMS指针的值，让下一阶段用户线程并发运行时，能正确地在可用的Region中分配新对象。这个阶段需要停顿线程，但耗时很短，而且是借用进行Minor GC的时候同步完成的，所以G1收集器在这个阶段实际并没有额外的停顿。
2. 并发标记（Concurrent Marking）：从GC Root开始对堆中对象进行可达性分析，递归扫描整个堆里的对象图，找出要回收的对象，这阶段耗时较长，但可与用户程序并发执行。当对象图扫描完成以后，还要重新处理SATB记录下的在并发时有引用变动的对象。
3. 最终标记（Final Marking）：对用户线程做另一个短暂的暂停，用于处理并发阶段结束后仍遗留下来的最后那少量的SATB记录。
4. 筛选回收（Live Data Counting and Evacuation）：负责更新Region的统计数据，对各个Region的回收价值和成本进行排序，根据用户所期望的停顿时间来制定回收计划，可以自由选择任意多个Region构成回收集，然后把决定回收的那一部分Region的存活对象复制到空的Region中，再清理掉整个旧Region的全部空间。这里的操作涉及存活对象的移动，是必须暂停用户线程，由多条收集器线程并行完成的。
  
## 类加载的过程
分为加载、验证、准备、解析和初始化这五个阶段.
  
**参考资料：**
深入理解Java虚拟机：JVM高级特性与最佳实践（第3版）

# Java&操作系统基础

## Java引用
Java里面分为强引用、软引用、弱引用、虚引用。<br />
每个线程Thread对象中都保存着一个ThreadLocalMap实例，而ThreadLocalMap中有一个Entry的数组（private Entry[] table;），Entry中的key类型是WeakReference<ThreadLocal>而非ThreadLocal，这样做的目的是为了当我们不再使用该ThreadLocal时，哪怕运行中线程的ThreadLocalMap实例有该ThreadLocal的Entry，JVM也能在GC时将ThreadLocal回收。


## 多线程
**Java线程5大状态**
![Java线程状态](https://user-images.githubusercontent.com/6687462/86524741-dbd65600-beb0-11ea-8d52-27dc94f294e5.png)

**内存屏障**
![内存屏障](https://user-images.githubusercontent.com/6687462/86533378-47491380-bf03-11ea-98e0-67837ecf2a5f.png)

**volatile**
volatile是轻量级的synchronized，它在多处理器开发中保证了共享变量的“可见性”，它比synchronized的使用和执行成本更低，因为它不会引起线程上下文的切换和调度。<br />
volatile实现原理：1. Lock前缀指令会引起处理器缓存回写到内存(当写一个volatile变量时，JMM会把该线程对应的本地内存中的共享变量值刷新到主内存。)。 2.一个处理器的缓存回写到内存会导致其他处理器的缓存无效(当读一个volatile变量时，JMM会把该线程对应的本地内存置为无效。线程接下来将从主内存中读取共享变量。)。

**synchronized（JDK6之前称之为重量级锁）**
JVM基于进入和退出Monitor对象来实现方法同步和代码块同步，但两者的实现细节不一样。代码块同步是使用monitorenter和monitorexit指令实现的，而方法同步是使用另外一种方式实现的，细节在JVM规范里并没有详细说明。但是，方法的同步同样可以使用这两个指令来实现。<br />
synchronized用的锁是存在Java对象头里的。如果对象是数组类型，则虚拟机用3个字宽（Word）存储对象头，如果对象是非数组类型，则用2字宽存储对象头。在32位虚拟机中，1字宽等于4字节，即32bit

**偏向锁 < 轻量级锁 < 重量级锁**
在JDK6通过引入锁升级的机制来实现更高效的内置锁（Synchronized），这三种锁的状态是通过对象监视器在对象头中的字段来表明的。<br />
JDK6为了减少获得锁和释放锁带来的开销，引入了“偏向锁”和“轻量级锁”，在JDK6中，锁一共有4种状态，级别从低到高依次是：无锁状态、偏向锁状态、轻量级锁状态和重量级锁状态，这几个状态会随着竞争情况逐渐升级。锁可以升级但不能降级，意味着偏向锁升级成轻量级锁后不能降级成偏向锁。这种锁升级却不能降级的策略，目的是为了提高获得锁和释放锁的效率

**Java内存分配**<br />
常见的堆上分配内存的方法有“指针碰撞”和“空闲列表”。

**Java内存模型（JMM）**<br />
Java线程之间的通信由Java内存模型控制，JMM决定一个线程对共享变量的写入何时对另一个线程可见，如下图：<br />
![JMM](https://user-images.githubusercontent.com/6687462/86532289-65ab1100-befb-11ea-8b0b-7d2b656ab1f1.png)

从JDK5开始，Java使用新的JSR-133内存模型。JSR-133使用happens-before的概念来阐述操作之间的内存可见性。在JMM中，如果一个操作执行的结果需要对另一个操作可见，那么这两个操作之间必须要存在happens-before关系。这里提到的两个操作既可以是在一个线程之内，也可以是在不同线程之间。
与我们密切相关的happens-before规则如下：\
1. 一个线程中的每个操作，happens-before于该线程中的任意后续操作。
2. 监视器锁规则：对一个锁的解锁，happens-before于随后对这个锁的加锁。
3. 对一个volatile域的写，happens-before于任意后续对这个volatile域的读。
4. 如果A happens-before B，且B happens-before C，那么A happens-before C。

## I/O
**用户空间与内核空间**
针对 Linux 操作系统而言，最高的 1G 字节(从虚拟地址 0xC0000000 到 0xFFFFFFFF)由内核使用，称为内核空间。而较低的 3G 字节(从虚拟地址 0x00000000 到 0xBFFFFFFF)由各个进程使用，称为用户空间。
在CPU的所有指令中，有些指令非常危险，如果错用，将导致系统崩溃，比如清内存、设置时钟等。如果允许所有的程序都可以使用这些指令，那么系统崩溃的概率将大大增加。
所以，CPU将指令分为特权指令和非特权指令，对于那些危险的指令，只允许操作系统及其相关模块使用，普通应用程序只能使用那些不会造成灾难的指令。比如Intel的CPU将特权等级分为4个级别：Ring0~Ring3。
其实Linux系统只使用了Ring0和Ring3 两个运行级别(Windows 系统也是一样的)。当进程运行在Ring3级别时被称为运行在用户态，而运行在Ring0级别时被称为运行在内核态。

**用户态与内核态**
当进程运行在内核空间时就处于内核态，而进程运行在用户空间时则处于用户态。

**Unix中5种I/O模型**
* 阻塞式I/O
* 非阻塞式I/O
* I/O复用(select和poll)
* 信号驱动式I/O(SIGIO)
* 异步I/O(POSIX的aio_系列函数)

![IO模型示意图](https://user-images.githubusercontent.com/6687462/87288119-8263cc00-c52d-11ea-9385-28a910c22234.png)

**阻塞式I/O**
请求进程阻塞，直到I/O操作完成，默认情况下，所有套接字都是阻塞的，如下图：
![阻塞IO模型](https://user-images.githubusercontent.com/6687462/87281887-45480b80-c526-11ea-80d2-e994498d99e8.png)

**非阻塞式I/O**
不导致请求进程阻塞：
![非阻塞IO模型](https://user-images.githubusercontent.com/6687462/87282513-edf66b00-c526-11ea-863b-56e0a5a9e885.png)

**I/O复用**
I/O multiplexing这里面的multiplexing指在单个线程通过记录跟踪每一个Socket(I/O流)的状态来同时管理多个I/O流. 
![IO多路复用](https://user-images.githubusercontent.com/6687462/87282705-20a06380-c527-11ea-9691-13172894e4c6.png)

**信号驱动式I/O**
![信号驱动IO](https://user-images.githubusercontent.com/6687462/87285347-01ef9c00-c52a-11ea-8f7d-185d04195451.png)

**异步I/O**
异步I/O和上面提的信号驱动式I/O的主要区别在于信号驱动式I/O是由内核通知我们合适可以启动一个I/O操作，而异步I/O是由内核通知我们I/O操作何时完成。
![异步IO](https://user-images.githubusercontent.com/6687462/87289138-d7541200-c52e-11ea-8a0c-15f8cc1fd113.png)

**select、poll和epoll**
* select：时间复杂度O(n)，它仅仅知道了，有I/O事件发生了，却并不知道是哪那几个流（可能有一个，多个，甚至全部），我们只能无差别轮询所有流，找出能读出数据，或者写入数据的流，对他们进行操作。所以select具有O(n)的无差别轮询复杂度，同时处理的流越多，无差别轮询时间就越长。

* poll：时间复杂度O(n)，poll本质上和select没有区别，它将用户传入的数组拷贝到内核空间，然后查询每个fd对应的设备状态， 但是它没有最大连接数的限制，原因是它是基于链表来存储的.

* epoll：时间复杂度O(1)，epoll可以理解为event poll，不同于忙轮询和无差别轮询，epoll会把哪个流发生了怎样的I/O事件通知我们。所以我们说epoll实际上是事件驱动（每个事件关联上fd
）的，此时我们对这些流的操作都是有意义的。（复杂度降低到了O(1)）

select，poll，epoll都是IO多路复用的机制。I/O多路复用就通过一种机制，可以监视多个描述符，一旦某个描述符就绪（一般是读就绪或者写就绪），能够通知程序进行相应的读写操作。但select，poll，epoll本质上都是同步I/O，因为他们都需要在读写事件就绪后自己负责进行读写，也就是说这个读写过程是阻塞的，而异步I/O则无需自己负责进行读写，异步I/O的实现会负责把数据从内核拷贝到用户空间。  

## 零拷贝



## 伪共享



**参考资料：**<br />
* https://developer.ibm.com/articles/j-zerocopy/
* https://www.linuxjournal.com/article/6345
* 《Java并发编程的艺术》
* 《Unix网络编程（卷一）》
* https://www.tqwba.com/x_d/jishu/17958.html
* https://www.cnblogs.com/aspirant/p/9166944.html

# 网络
## TCP
为了通过IP数据报实现可靠传输，需要考虑很多事情，例如数据的破坏、丢包、重复已经分片顺序混乱等问题，TCP通过校验和、序列号、确认应答、重发控制、连接管理以及窗口控制等机制实现可靠传输。

**三次握手和四次挥手**
![TCP三次握手和四次挥手](https://user-images.githubusercontent.com/6687462/87508147-4fdae000-c6a1-11ea-8e50-974de1e9b49c.png)<br />

**为什么要三次握手**<br />
三次握手是通信双方相互告知序列号起始值，并确认对方已经收到序列号起始值的必经步骤。<br />
第一次握手：证明了接收端能收到消息。<br />
第二次握手：证明了发送端能收到接收端的消息，发送端知道接收端能收到它发送的消息。<br />
第三次握手：证明了接收端知道发送端能收到它发送的消息。<br />

**为什么要四次挥手**<br />


**滑动窗口**<br />
TCP协议中是以段（Segment）为单位来发送数据的，我们也称其为最大消息长度（MSS：Maximum Segment Size），最理想的情况下MSS长度正好是IP中不会被分片处理的最大数据长度。TCP为了可靠传输，需要对每一个段进行确认应答，如果只有前一个发送段被确认后才能发送下一个段，那发送速率或吞吐量就太低了，所以有了“滑动窗口”的概念。窗口的大小就是指无需等待确认应答而可以继续发送的数据的最大值。当采用滑动窗口的情况下，如果出现某些报文段丢失的情况下，接收端会将同一个序号的确认应答重复不断的返回，而发送端主机如果连续3次收到同一个确认应答，就会将其所对应的数据进行重发。

**拥塞窗口（慢启动）**<br />

**Nagle算法**<br />
为了提高网络利用率，会经常使用Nagle算法，该算法是指发送端即使还有应该发送的数据，但如果这部分数据很少的话，则进行延迟发送的一种处理机制。具体来说就是满足如下任意一种条件才能发送数据：
1) 已发送的数据都已经收到确认应答时。
2) 可以发送最大段长度（MSS）的数据时。
一般对实时性要求高的系统会关闭TCP的Nagle算法。

**延迟确认应答**<br />

**参考资料**<br />
* 《图解TCP/IP（第5版）》
* https://ee.lbl.gov/papers/congavoid.pdf



# 数据结构
## BitMap


# 算法
