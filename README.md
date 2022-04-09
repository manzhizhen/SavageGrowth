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
- [云](#云)
    - [云计算服务](#云计算服务)
    - [云原生](#云原生)
    - [Service Mesh](#ServiceMesh(服务网格))
    - [Serverless](#Serverless(无服务器))
- [存储](#存储)
    - [RDS](#RDS)
        - [MySQL](#MySQL)
    - [NoSQL](#NoSQL)
        - [Redis](#Redis)
- [分布式系统](#分布式系统)
    - [常见的一致性算法（共识算法）](#常见的一致性算法（共识算法）)
        - [2PC&3PC](#2PC&3PC)
        - [TCC](#TCC)
        - [Saga](#Saga)
        - [Paxos](#Paxos)
        - [Raft](#Raft)
        - [Gossip](#Gossip)
        - [ZAB](#ZAB)
        - [为什么要选主](#为什么要选主)
    - [RPC框架](#RPC框架)
        - [Apache Dubbo](#Dubbo)
    - [ZooKeeper](#ZooKeeper)
    - [MQ](#MQ)
- [Web服务器](#Web服务器)
    - [Nginx](#Nginx)
    - [Tomcat](#Tomcat)
- [DevOps](#DevOps)
    - [DevOps定义](#DevOps定义)
    - [持续集成(CI)](#持续集成(CI))
    - [持续交付(CD)](#持续交付(CD))
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
    - [Java对象锁](#Java对象锁)
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

**参考资料：**<br />
* 《恰如其分的软件架构》
* https://blog.christianposta.com/microservices/when-not-to-do-microservices/
* 《Java设计模式（第2版）》
* 《Spring实战（第5版）》

## 响应式编程(Reactive)
在开发应用程序代码时，我们可以编写两种风格的代码，即命令式和反应式。
* 命令式（Imperative）的代码：它由一组任务组成，每次只运行一项任务，每项任务又都依赖于前面的任务。我们一次一个地按照顺序将代码编写为需要遵循的指令列表。在某项任务开始执行之后，程序在开始下一项任务之前需要等待当前任务完成。在整个处理过程中的每一步，要处理的数据都必须是完全可用的，以便将它们作为一个整体进行处理。
* 响应式（Reactive）的代码：它定义了一组用来处理数据的任务，但是这些任务可以并行地执行。每项任务处理数据的一部分子集，并将结果交给处理流程中的下一项任务，同时继续处理数据的另一部分子集。相对于要求将被处理的数据作为一个整体进行处理，响应式流可以在数据可用时立即开始处理。实际上，传入的数据可能是无限的（比如，一个某个地理位置的实时温度测量数据的恒定流）。

**参考资料：**<br />
* https://www.reactivemanifesto.org/
* https://www.reactive-streams.org/
* https://github.com/reactor/reactor-core
* https://github.com/reactor/lite-rx-api-hands-on
* https://projectreactor.io/docs/core/release/reference/index.html#about-doc
* https://projectreactor.io/docs/core/release/reference/index.html
* https://github.com/reactor/lite-rx-api-hands-on
* https://www.xncoding.com/2018/04/05/java/reactor.html
* http://gee.cs.oswego.edu/dl/cpjslides/nio.pdf
* https://docs.spring.io/spring-framework/docs/current/reference/html/web-reactive.html#webflux-concurrency-model
* https://www.baeldung.com/spring-webflux-concurrency
* https://piotrminkowski.com/2020/03/30/a-deep-dive-into-spring-webflux-threading-model/


# 云
云是一种IT环境，可以抽象、汇集和共享整个网络中的可扩展资源。云的主旨是用于进行云计算，也就是在云环境中运行工作负载。云是一种 PaaS，因为会有用户以外的其他方提供底层基础架构（将从中提供基于 Web 的平台）。<br />
**私有云**可广义地定义为一种专为最终用户而创建，而且通常位于用户的防火墙内（有时也是内部部署）的云环境。<br />
**公共云**是一种利用非最终用户所有的资源创建的云环境，可重新分发给其他租户。<br />
**混合云**是一种具有一定程度的工作负载可移植性以及编排和管理能力的多云环境。<br />
**多云**是一个含有多个云环境（公共云或私有云）的 IT 系统，云与云之间可能联网也可能不联网。<br />

## 云计算服务
凡是用户无需下载其他软件而是直接通过互联网就能访问的所有基础架构、平台、软件或技术都可以视为云计算，包括以下即服务类解决方案：IaaS、PaaS、SaaS和FaaS。
![云计算解决方案（英文）](https://user-images.githubusercontent.com/6687462/159231947-f47f50e3-b8a7-4837-9b6d-9ed63117d640.png)

### PaaS
ClickPaaS(https://www.clickpaas.com/) 更快速、更高效、更敏捷成为当下数字化变革的必要条件。

## 云原生
### 定义
* 云原生是一种应用程序开发风格（或者说云原生是一种构建和运行应用程序的方法），它鼓励在持续交付和价值驱动的开发领域采用最佳实践。一个相关的学科是构建12要素应用程序，其中开发实践与交付和运营目标保持一致
* 云原生技术有利于各组织在公有云、私有云和混合云等新型动态环境中，构建和运行可弹性扩展的应用。
* 云原生的代表技术包括容器、服务网格、微服务、不可变基础设施和声明式API。这些技术能够构建容错性好、易于管理和便于观察的松耦合系统。结合可靠的自动化手段，云原生技术使工程师能够轻松地对系统作出频繁和可预测的重大变更。
* 云原生计算基金会（CNCF）致力于培育和维护一个厂商中立的开源生态系统，来推广云原生技术。我们通过将最前沿的模式民主化，让这些创新为大众所用。

### 云原生架构的5大特征
* **12因素应用**：12因素应用是一系列云原生应用架构的模式集合，最初由Heroku提出，这些模式包含代码库、依赖、配置、后端服务、编译&发布&运行、进程、端口绑定、并发、可任意处置性、开发/生产平等、日志、管理进程。
* **微服务**：微服务将单体业务系统分解为多个“仅做好一件事”的可独立部署的服务。这件事通常代表某项业务能力，或者最小可提供业务价值的“原子“服务单元。
* **自服务敏捷架构**：使用云原生应用架构的团队通常负责其应用的部署和持续运营。云原生应用的成功采纳者已经为团队提供了自服务平台。
* **基于API的协作**：在云原生应用架构中，服务之间的唯一互动模式是通过已发布和版本化的API。这些API通常是具有JSON序列化的HTTP REST风格，但也可以是其他协议和序列化格式。
* **抗脆弱性**：Nassim Taleb在他的Antifragile（Random House）一书中介绍了抗脆弱性的概念。如果脆弱性是受到压力源的弱化或破坏的质量系统，那么与之相反呢？许多人会以稳健性或弹性作出回应——在遭受压力时不会被破坏或变弱。然而，Taleb引入了与脆弱性相反的抗脆弱性概念，或者在受到压力源时变得更强的质量系统。什么系统会这样工作？联想下人体免疫系统，当接触病原体时，其免疫力变强，隔离时较弱。我们可以像这样建立架构吗？云原生架构的采用者们已经设法构建它们了。Netflix Simian Army项目就是个例子，其中著名的子模块“混沌猴”，它将随机故障注入到生产组件中，目的是识别和消除架构中的缺陷。通过明确地寻求应用架构中的弱点，注入故障并强制进行修复，架构自然会随着时间的推移而更大程度地收敛。

**参考资料：**
* https://github.com/cncf/toc/blob/master/DEFINITION.md
* https://jimmysong.io/kubernetes-handbook/cloud-native/cloud-native-definition.html
* https://docs.spring.io/spring-cloud-commons/docs/current/reference/html/
* https://tanzu.vmware.com/content/ebooks/migrating-to-cloud-native-application-architectures
* https://12factor.net/
* https://www.redhat.com/zh/topics/cloud-computing/what-are-cloud-services
* https://jimmysong.io/migrating-to-cloud-native-application-architectures/

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
#### 架构
<img width="1070" alt="MySQL架构图" src="https://user-images.githubusercontent.com/6687462/159244881-02febb00-320a-4aa9-9f43-653c7602ab3b.png">

#### MGR
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

#### binlog、redolog、undolog
**binlog**：MySQL Server层记录的归档日志，Base64编码的二进制格式，用于恢复数据和复本同步。binlog采用的是顺序追加写。<br />
**redolog**：InnoDB存储引擎层的重做日志，确保事务的持久性。防止在发生故障的时间点，尚有脏页未写入磁盘，在重启MySQL服务的时候，根据redolog进行重做，从而保证事务的持久性。redolog采用的是循环写，即固定文件大小，如果写到文件末尾，又从头写。<br />
**undolog**：InnoDB存储引擎层的回滚日志，保存了事务发生之前的数据的一个版本，用于事务的回滚。<br />

#### 参考资料
* https://dev.mysql.com/doc/refman/8.0/en/group-replication.html
* https://dev.mysql.com/doc/refman/8.0/en/binlog.html

## NoSQL
NoSQL常见的四种类型：键值对型、文档型、列式存储型和图型。

### Redis
#### 定义
Redis是一种采用内存来作为数据结构存储的数据库、缓存和消息代理。<br />

#### 部署说明
Redis是用ANSI C编写，并且可以在大多数POSIX系统中使用，例如Linux，* BSD，OS X，而无需外部依赖。Linux和OS X是Redis开发和测试最多的两个操作系统，我们建议使用Linux进行部署。<br/>

#### 内部数据结构
简单动态字符串(Simple Dynamic Strings, SDS)、双端链表、跳跃表(skiplist)、压缩列表、快速列表(Redis3.2引入，quicklist)、字典(散列表)、整数集合(intset)。
* **跳跃表**： 考虑一个有序表

    * ![redis跳跃表1](https://user-images.githubusercontent.com/6687462/162159457-d64d7b92-5ad1-40d0-a10d-7a3c7a74e3ec.png)

    * 从该有序表中搜索元素 < 23, 43, 59 > ，需要比较的次数分别为 < 2, 4, 6 >，总共比较的次数为 2 + 4 + 6 = 12 次。有没有优化的算法吗? 链表是有序的，但不能使用二分查找。类似二叉
搜索树，我们把一些节点提取出来，作为索引。得到如下结构：

    * ![redis跳跃表2](https://user-images.githubusercontent.com/6687462/162159488-56f245cf-06b6-44de-84b3-9e884cfb4e37.jpg)

    * 这里我们把 < 14, 34, 50, 72 > 提取出来作为一级索引，这样搜索的时候就可以减少比较次数了。 我们还可以再从一级索引提取一些元素出来，作为二级索引，变成如下结构：

    * ![redis跳跃表3](https://user-images.githubusercontent.com/6687462/162159508-f8d30a4c-a725-4100-b4a9-2ae24309885c.jpg)

    * 这里元素不多，体现不出优势，如果元素足够多，这种索引结构就能体现出优势来了。
    
#### 支持的数据结构
字符串，哈希，列表，集合，带范围查询的排序集合，位图，HyperLogLog，地理空间索引。<br/>

#### Redis是单线程的。如何利用多个多核CPU？
CPU成为Redis瓶颈的情况并不常见，因为Redis通常是内存或网络绑定的。例如，在一个普通的Linux系统上运行的流水线Redis每秒甚至可以传递100万个请求，所以如果您的应用程序主要使用O（N）或O（log（N））命令，它几乎不会占用太多的CPU。
但是，为了最大限度地利用CPU，可以在同一个机器中启动多个Redis实例，并将它们视为不同的服务器。然而，随着Redis 4.0的推出，我们开始让Redis多线程化。目前，这仅限于在后台删除对象，以及阻止通过Redis模块实现的命令。对于未来的版本，计划是让Redis越来越多线程化。

#### Redis6的多线程特性
Redis的多线程部分只是用来处理网络数据的读写和协议解析，执行命令仍然是单线程顺序执行。所以我们不需要去考虑控制 key、lua、事务，LPUSH/LPOP 等等的并发及线程安全问题。

#### 持久化方案
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

#### 复本机制
1. Redis支持主从模式，默认采用异步复制的方式，如果对强一致性有要求，可以使用同步复制。
2. Redis支持将多个副本连接到同一主副本，并且副本还可以按级联结构连接到其他副本。从Redis 4.0开始，所有子副本将从主服务器接收完全相同的数据流。
3. Redis复制时在Master上是无阻塞的。这意味着当一个或多个副本执行初始同步或部分重新同步时，主服务器将继续处理查询。

#### 高可用
Redis官方提供的高可用方案分为Redis Sentinel和Redis Cluster两种。<br/>
**Redis Sentinel**<br/>
这是宏观上Sentinel功能的完整列表：
* 监控。Sentinel会不断检查您的主实例和副本实例是否按预期工作。
* 通知。Sentinel可以通过API通知系统管理员或其他计算机程序，其中一个受监视的Redis实例出了问题。
* 自动故障转移。如果主服务器未按预期工作，则Sentinel可以启动故障转移过程，在该过程中将副本升级为主服务器，将其他附加副本重新配置为使用新的主服务器，并通知使用Redis服务器的应用程序要使用的新地址。连接时。
* 配置提供程序。Sentinel充当客户端服务发现的权威来源：客户端连接到Sentinels，以询问负责给定服务的当前Redis主服务器的地址。如果发生故障转移，Sentinels将报告新地址。

1. 当多个哨兵就给定的主机不再可用这一事实达成共识时，将执行故障检测。这降低了误报的可能性。
2. 即使不是所有的Sentinel进程都在工作，Sentinel仍能正常工作，从而使系统能够应对故障。毕竟，拥有故障转移系统本身就是一个单点故障，这没有任何意思。
3. 一个健壮的部署至少需要三个Sentinel实例。
4. Sentinels，Redis实例（主服务器和副本）以及连接到Sentinel和Redis的客户端的总和也是具有特定属性的大型分布式系统。

![Redis哨兵](https://user-images.githubusercontent.com/6687462/159384118-9c7b5054-2dc0-4e72-93f3-efea36cbf0a0.png)

**Redis Cluster**<br/>
Redis Cluster 提供了一种运行 Redis 的方法，其中数据 自动分片到多个 Redis 节点。Redis Cluster 还在分区期间提供了一定程度的可用性，即在某些节点发生故障或无法通信时继续操作的能力。但是，如果发生较大故障（例如，当大多数主服务器不可用时），集群将停止运行。

*Redis Cluster 不使用一致性散列，而是使用不同形式的分片*，其中每个键在概念上都是我们所谓的散列槽的一部分。 Redis 集群中有 16384 个哈希槽，要计算给定键的哈希槽是多少，我们只需将键的 CRC16 取模 16384。
Redis 集群中的每个节点都负责哈希槽的子集，例如，您可能有一个具有3个节点的集群，其中：
* 节点 A 包含从 0 到 5500 的哈希槽。
* 节点 B 包含从 5501 到 11000 的哈希槽。
* 节点 C 包含从 11001 到 16383 的哈希槽。

这允许在集群中轻松添加和删除节点。例如，如果我想添加一个新节点 D，我需要将一些哈希槽从节点 A、B、C 移动到 D。同样，如果我想从集群中删除节点 A，我可以只移动 A 服务的哈希槽到 B 和 C。当节点 A 为空时，我可以将它完全从集群中删除。因为将哈希槽从一个节点移动到另一个节点不需要停止操作，添加和删除节点，或者更改节点持有的哈希槽的百分比，不需要任何停机时间。
Redis Cluster 支持多个 key 操作，只要涉及到单个命令执行（或整个事务，或 Lua 脚本执行）的所有 key 都属于同一个 hash slot。用户可以通过使用称为哈希标签的概念来强制多个键成为同一个哈希槽的一部分。
哈希标签记录在 Redis Cluster 规范中，但要点是，如果键中的 {} 括号之间有子字符串，则仅对字符串内的内容进行哈希处理，例如this{foo}key和another{foo}key 保证在同一个哈希槽中, 并且可以在具有多个键作为参数的命令中一起使用。

*Redis Cluster 无法保证强一致性*。实际上，这意味着在某些情况下，Redis 集群可能会丢失系统向客户端确认的写入。 Redis Cluster 可能丢失写入的第一个原因是因为它使用异步复制。这意味着在写入期间会发生以下情况：
* 您的客户写信给主 B。
* 主 B 向您的客户回复 OK。
* 主节点 B 将写入传播到其副本 B1、B2 和 B3。

如您所见，B 在回复客户端之前不会等待来自 B1、B2、B3 的确认，因为这对 Redis 来说是一个令人望而却步的延迟惩罚，因此如果您的客户端写入内容，B 会确认写入，但在此之前崩溃能够将写入发送到其副本，其中一个副本（未收到写入）可以提升为主，永远失去写入。这与大多数配置为每秒将数据刷新到磁盘的数据库所发生的情况非常相似，因此由于过去使用不涉及分布式系统的传统数据库系统的经验，您已经能够推断出这种情况。同样，您可以通过强制数据库在回复客户端之前将数据刷新到磁盘来提高一致性，但这通常会导致性能过低。在 Redis Cluster 的情况下，这相当于同步复制。但是请注意，即使使用同步复制，Redis Cluster 也不会实现强一致性：在更复杂的故障场景下，始终有可能将无法接收写入的副本选为 master。

还有另一个值得注意的场景是 Redis 集群会丢失写入，这种情况发生在网络分区期间，其中客户端与少数实例（包括至少一个主实例）隔离。
以我们的 6 节点集群为例，由 A、B、C、A1、B1、C1 组成，具有 3 个主节点和 3 个副本。还有一个客户，我们称之为 Z1。
发生分区后，可能在分区的一侧有 A、C、A1、B1、C1，而在另一侧有 B 和 Z1。
Z1 仍然能够写入 B，B 将接受其写入。如果分区在很短的时间内恢复，集群将继续正常运行。但是，如果分区持续了足够的时间让 B1 在分区的大多数端被提升为主控，那么 Z1 在此期间发送给 B 的写入将丢失。
请注意，Z1 能够发送到 B 的写入量有一个*最大窗口*：如果分区的多数方经过足够的时间来选举副本作为主节点，则少数方的每个主节点都将停止接受写入。 这个时间量是 Redis Cluster 的一个非常重要的配置指令，称为**节点超时**。
节点超时后，主节点被认为发生故障，并且可以由其副本之一替换。类似地，在节点超时后没有主节点能够感知其他主节点的大多数，它进入错误状态并停止接受写入。

![RedisCluster](https://user-images.githubusercontent.com/6687462/159384112-53f1129b-3755-463d-bfa1-e0214ae05d5c.png)

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

antirez提出的**Redlock**算法大概是这样的：
在Redis的分布式环境中，我们假设有N个Redis master。这些节点完全互相独立，不存在主从复制或者其他集群协调机制。我们确保将在N个实例上使用与在Redis单实例下相同方法获取和释放锁。现在我们假设有5个Redis master节点，同时我们需要在5台服务器上面运行这些Redis实例，这样保证他们不会同时都宕掉。
为了取到锁，客户端应该执行以下操作:
1. 获取当前Unix时间，以毫秒为单位。
2. 依次尝试从5个实例，使用相同的key和具有唯一性的value（例如UUID）获取锁。当向Redis请求获取锁时，客户端应该设置一个网络连接和响应超时时间，这个超时时间应该小于锁的失效时间。例如你的锁自动失效时间为10秒，则超时时间应该在5-50毫秒之间。这样可以避免服务器端Redis已经挂掉的情况下，客户端还在死死地等待响应结果。如果服务器端没有在规定时间内响应，客户端应该尽快尝试去另外一个Redis实例请求获取锁。
3. 客户端使用当前时间减去开始获取锁时间（步骤1记录的时间）就得到获取锁使用的时间。当且仅当从大多数（N/2+1，这里是3个节点）的Redis节点都取到锁，并且使用的时间小于锁失效时间时，锁才算获取成功。
4. 如果取到了锁，key的真正有效时间等于有效时间减去获取锁所使用的时间（步骤3计算的结果）。
5. 如果因为某些原因，获取锁失败（没有在至少N/2+1个Redis实例取到锁或者取锁时间已经超过了有效时间），客户端应该在所有的Redis实例上进行解锁（即便某些Redis实例根本就没有加锁成功，防止某些节点获取到锁但是客户端没有得到响应而导致接下来的一段时间不能被重新获取锁）。

**参考资料**
* https://www.jianshu.com/p/c2841d65df4c
* https://redis.io/
* https://redis.io/topics/distlock
* https://redis.io/topics/cluster-tutorial
* https://www.jianshu.com/p/7e47a4503b87
* https://blog.tienyulin.com/redis-master-slave-replication-sentinel-cluster/
* http://doc.redisfans.com/
* https://www.elastic.co/cn/elasticsearch/
* https://github.com/elastic/elasticsearch
* https://redis.io/topics/faq
* https://www.cnblogs.com/madashu/p/12832766.html
* https://redis.io/docs/reference/patterns/distributed-locks/  Redis分布式锁
* http://antirez.com/news/101  RedLock安全吗？

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


# 分布式系统

## 常见的一致性算法（共识算法）
The three most popular consistency levels are eventual, read-your-writes, and strong.
三个最流行的一致性级别是最终一致性、写后读 和 强一致性。
### 2PC&3PC
X/Open 组织（即现在的 Open Group ）定义了分布式事务处理模型。 X/Open DTP 模型（ 1994 ）包括应用程序（ AP ）、事务管理器（ TM ）、资源管理器（ RM ）、通信资源管理器（ CRM ）四部分。一般，常见的事务管理器（ TM ）是交易中间件，常见的资源管理器（ RM ）是数据库，常见的通信资源管理器（ CRM ）是消息中间件。
XA 就是 X/Open DTP 定义的交易中间件与数据库之间的接口规范（即接口函数），交易中间件用它来通知数据库事务的开始、结束以及提交、回滚等。 XA 接口函数由数据库厂商提供。
**2PC**<br />
角色：事务参与方、事务协调者<br />
Two-phaseCommit：第一阶段——准备阶段(投票阶段)、第二阶段——提交阶段（执行阶段）。<br />
![2PC成功](https://user-images.githubusercontent.com/6687462/159493054-d400a20f-fc6a-4bfb-ab30-f2c95dffc13d.jpg) <br />
![2PC失败](https://user-images.githubusercontent.com/6687462/159493070-63c50692-5924-46e0-99cd-ca17bfbc8581.jpg) <br />
![2PC卡死](https://user-images.githubusercontent.com/6687462/159493079-0b6d4ace-74c5-4e47-be8a-84e22d1d8ae9.jpg) <br />
**优点**：<br />

**缺点**：<br />
* 性能问题:无论是在第一阶段的过程中,还是在第二阶段,所有的参与者资源和协调者资源都是被锁住的,只有当所有节点准备完毕，事务协调者才会通知进行全局提交，
参与者 进行本地事务提交后才会释放资源。这样的过程会比较漫长，对性能影响比较大。
* 单节点故障:由于协调者的重要性，一旦协调者发生故障。参与者会一直阻塞下去。尤其在第二阶段，协调者发生故障，那么所有的参与者还都处于锁定事务资源的状态中，而无法继续完成事务操作。

**3PC**<br />
角色：事务参与方、事务协调者<br />
Three-phaseCommit：第一阶段——CanCommit、第二阶段——PreCommit、第三阶段——DoCommit。<br />
![3PC](https://user-images.githubusercontent.com/6687462/123544788-71848880-d787-11eb-9995-16956d31d416.png)
![3PC成功](https://user-images.githubusercontent.com/6687462/159493096-ac7b6f74-060f-4d5e-af57-aa1ddd4dca54.jpg)
![3PC失去共识](https://user-images.githubusercontent.com/6687462/159493108-d6dc6184-43ad-4e70-abab-d8ef7f3e0663.jpg)

**和2PC区别**：
3PC主要是为了解决两阶段提交协议的阻塞问题，2PC存在的问题是当协作者崩溃时，参与者不能做出最后的选择（因为参与者不知道其他参与者CanCommit的结果），因此参与者可能在协作者恢复之前保持阻塞。
1、引入超时机制。同时在协调者和参与者中都引入超时机制。
2、在第一阶段和第二阶段中插入一个准备阶段。保证了在最后提交阶段之前各参与节点的状态是一致的。

优点：<br />
缺点：<br />

### TCC
即 Try-Confirm-Cancel，TCC是应用层的2PC(2 Phase Commit, 两阶段提交)，如果你将应用看做资源管理器的话。一般来说需要业务系统实现try、confirm 和 cancel 三个接口。

### Saga
Saga 是一种补偿协议，在 Saga 模式下，分布式事务内有多个参与者，每一个参与者都是一个冲正补偿服务，需要用户根据业务场景实现其正向操作和逆向回滚操作。
分布式事务执行过程中，依次执行各参与者的正向操作，如果所有正向操作均执行成功，那么分布式事务提交。如果任何一个正向操作执行失败，那么分布式事务会退回去执行前面各参与者的逆向回滚操作，回滚已提交的参与者，使分布式事务回到初始状态。
Saga 理论出自 Hector & Kenneth 1987发表的论文 Sagas。 Saga 正向服务与补偿服务也需要业务开发者实现。

### Paxos
Paxos算法是莱斯利·兰伯特(Leslie Lamport)1990年提出的一种基于消息传递的一致性算法，其解决的问题是分布式系统如何就某个值(决议)达成一致。

### Raft
不同于Paxos算法直接从分布式一致性问题出发推导出来，Raft算法则是从多副本状态机的角度提出，用于管理多副本状态机的日志复制。Raft实现了和Paxos相同的功能，它将一致性分解为多个子问题：Leader选举（Leader election）、日志同步（Log replication）、安全性（Safety）、日志压缩（Log compaction）、成员变更（Membership change）等。
同时，Raft算法使用了更强的假设来减少了需要考虑的状态，使之变的易于理解和实现。

Raft将系统中的角色分为领导者（Leader）、跟从者（Follower）和候选人（Candidate）：
* Leader：接受客户端请求，并向Follower同步请求日志，当日志同步到大多数节点上后告诉Follower提交日志。
* Follower：接受并持久化Leader同步的日志，在Leader告之日志可以提交之后，提交日志。
* Candidate：Leader选举过程中的临时角色。

![Raft算法角色转换](https://user-images.githubusercontent.com/6687462/159512756-7d9a279f-7dfb-4dfb-8f04-889a365410f6.jpg)

### Gossip
Gossip protocol 也叫 Epidemic Protocol （流行病协议），是基于流行病传播方式的节点或者进程之间信息交换的协议。。Gossip protocol在1987年8月由施乐公司帕洛阿尔托研究中心研究员艾伦·德默斯（Alan Demers）发表在ACM上的论文《Epidemic Algorithms for Replicated Database Maintenance》中被提出。

### ZAB

### 为什么要选主
可以运行 Paxos 以就序列中的每个写操作达成一致。但是，每次运行 Paxos 可能会很昂贵。Zab 和 Raft 所做的是他们使用类似 Paxos 的算法来选举领导者。然后领导者决定事件的写操作（及其顺序）应该是什么。

### 参考资料
* https://jepsen.io/consistency/models/read-your-writes
* https://engineering.fb.com/2021/08/06/core-data/zippydb/
* https://www.cs.cornell.edu/projects/Quicksilver/public_pdfs/SWIM.pdf
* https://www.serf.io/docs/internals/gossip.html
* https://www.consul.io/docs/architecture/consensus
* http://publicatio.bibl.u-szeged.hu/1529/1/gossip11.pdf
* https://cloud.tencent.com/developer/article/1662426
* https://raft.github.io/raft.pdf
* https://zhuanlan.zhihu.com/p/35298019
* https://zhuanlan.zhihu.com/p/32052223
* https://www.jianshu.com/p/a4b2507051ef
* https://www.sofastack.tech/blog/sofa-meetup-3-seata-retrospect/
* https://cache.one/read/14973079

## ZooKeeper
定义：ZooKeeper是一个分布式协作框架，用于维护配置信息，命名，提供分布式同步以及提供组服务。

## RPC框架
### Dubbo

#### 部署架构
作为一个微服务框架，Dubbo sdk 跟随着微服务组件被部署在分布式集群各个位置，为了在分布式环境下实现各个微服务组件间的协作， Dubbo 定义了一些中心化组件，这包括：

* 注册中心。协调 Consumer 与 Provider 之间的地址注册与发现
* 配置中心。
  * 存储 Dubbo 启动阶段的全局配置，保证配置的跨环境共享与全局一致性
  * 负责服务治理规则（路由规则、动态配置等）的存储与推送。
* 元数据中心。
  * 接收 Provider 上报的服务接口元数据，为 Admin 等控制台提供运维能力（如服务测试、接口文档等）
  * 作为服务发现机制的补充，提供额外的接口/方法级别配置信息的同步能力，相当于注册中心的额外扩展

![Dubbo部署架构](https://user-images.githubusercontent.com/6687462/161994112-31ff3416-d1f8-4693-9c6b-32b2174186d4.png)

#### 服务发现
就使用方式上而言，Dubbo3 与 Dubbo2 的服务发现配置是完全一致的，不需要改动什么内容。但就实现原理上而言，Dubbo3 引入了全新的服务发现模型 - 应用级服务发现， 在工作原理、数据格式上已完全不能兼容老版本服务发现。

* Dubbo3 应用级服务发现，以应用粒度组织地址数据
* Dubbo2 接口级服务发现，以接口粒度组织地址数据

Dubbo3 格式的 Provider 地址不能被 Dubbo2 的 Consumer 识别到，反之 Dubbo2 的消费者也不能订阅到 Dubbo3 Provider。

概括来说，Dubbo3 引入的应用级服务发现主要有以下优势：
* 适配云原生微服务变革。云原生时代的基础设施能力不断向上释放，像 Kubernetes 等平台都集成了微服务概念抽象，Dubbo3 的应用级服务发现是适配各种微服务体系的通用模型。
* 提升性能与可伸缩性。支持超大规模集群的服务治理一直以来都是 Dubbo 的优势，通过引入应用级服务发现模型，从本质上解决了注册中心地址数据的存储与推送压力，相应的 Consumer 侧的地址计算压力也成数量级下降；集群规模也开始变得可预测、可评估（与 RPC 接口数量无关，只与实例部署规模相关）。

#### RPC通信协议
Dubbo3 提供了 Triple(Dubbo3)、Dubbo2 协议，这是 Dubbo 框架的原生协议。除此之外，Dubbo3 也对众多第三方协议进行了集成，并将它们纳入 Dubbo 的编程与服务治理体系， 包括 gRPC、Thrift、JsonRPC、Hessian2、REST 等。以下重点介绍 Triple 与 Dubbo2 协议。
RPC 协议的设计需要考虑以下内容：
* 通用性： 统一的二进制格式，跨语言、跨平台、多传输层协议支持
* 扩展性： 协议增加字段、升级、支持用户扩展和附加业务元数据
* 性能：As fast as it can be
* 穿透性：能够被各种终端设备识别和转发：网关、代理服务器等 通用性和高性能通常无法同时达到，需要协议设计者进行一定的取舍。

最终我们选择了兼容 gRPC ，以 HTTP2 作为传输层构建新的协议，也就是 Triple。

容器化应用程序和微服务的兴起促进了针对负载内容优化技术的发展。 客户端中使用的传统通信协议（ RESTFUL或其他基于 HTTP 的自定义协议）难以满足应用在性能、可维护性、扩展性、安全性等方便的需求。一个跨语言、模块化的协议会逐渐成为新的应用开发协议标准。自从 2017 年 gRPC 协议成为 CNCF 的项目后，包括 k8s、etcd 等越来越多的基础设施和业务都开始使用 gRPC 的生态，作为云原生的微服务化框架， Dubbo 的新协议也完美兼容了 gRPC。并且，对于 gRPC 协议中一些不完善的部分， Triple 也将进行增强和补充。

那么，Triple 协议是否解决了上面我们提到的一系列问题呢？

* 性能上: Triple 协议采取了 metadata 和 payload 分离的策略，这样就可以避免中间设备，如网关进行 payload 的解析和反序列化，从而降低响应时间。
* 路由支持上，由于 metadata 支持用户添加自定义 header ，用户可以根据 header 更方便的划分集群或者进行路由，这样发布的时候切流灰度或容灾都有了更高的灵活性。
* 安全性上，支持双向TLS认证（mTLS）等加密传输能力。
* 易用性上，Triple 除了支持原生 gRPC 所推荐的 Protobuf 序列化外，使用通用的方式支持了 Hessian / JSON 等其他序列化，能让用户更方便的升级到 Triple 协议。对原有的 Dubbo 服务而言，修改或增加 Triple 协议 只需要在声明服务的代码块添加一行协议配置即可，改造成本几乎为 0。



**参考资料**<br />
* https://dubbo.apache.org/zh/docs/
* https://dubbo.apache.org/zh/docs/concepts/registry-configcenter-metadata/
* https://dubbo.apache.org/zh/docs/migration/migration-service-discovery/

## MQ

### RocketMQ
#### 事务消息
<img width="866" alt="RocketMQ事务消息" src="https://user-images.githubusercontent.com/6687462/162554192-4c1cd170-17b3-4796-8845-04e43956e8aa.png">

### Kafka
Kafka被设计为能够作为一个统一平台来处理大量或实时数据的投递和消费，为此Kafka需要有如下特性：
* 高吞吐：它必须具有高吞吐量才能支持大容量事件流，例如实时日志聚合。 <br />
* 扛积压：它需要优雅地处理大量数据积压，以便能够支持来自离线系统的定期数据加载。 <br />
* 低延迟：这也意味着系统必须处理低延迟交付以处理更传统的消息传递用例。 <br />

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

**参考资料**<br />
* https://kafka.apache.org/documentation/#design
* https://queue.acm.org/detail.cfm?id=1563874


# Web服务器

## Nginx

## Tomcat

# DevOps
## DevOps定义
DevOps是一组用于促进开发和运维人员之间协作以达到缩短软件交付周期的过程、方法和系统的统称。

## 持续集成(CI)
持续集成（Continuous Integration）指的是在软件开发过程中，软件开发人员持续不断地将开发出来的代码和其他的开发人员的代码进行合并，每次合并后自动地进行编译、构建，并运行自动化测试进行验证，而不是等到最后各自开发完成后才合并在一起。
持续集成能从根本上提高一个团队的软件开发效率。在软件开发过程中引入持续集成，可以帮助团队及时的发现系统中的问题，并快速做出修复，不仅可以缩短软件开发的时间，而且可以交付更具质量的系统。

## 持续交付(CD)
持续交付（Continuous Delivery）是一种自动化交付的手段，关注点在于将不同的过程集中起来，并且更快、更频繁地执行这些过程。

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

### BeanFactory遵守的初始化方法顺序
Bean factory implementations should support the standard bean lifecycle interfaces as far as possible. The full set of initialization methods and their standard order is:
1. BeanNameAware's setBeanName
2. BeanClassLoaderAware's setBeanClassLoader
3. BeanFactoryAware's setBeanFactory
4. EnvironmentAware's setEnvironment
5. EmbeddedValueResolverAware's setEmbeddedValueResolver
6. ResourceLoaderAware's setResourceLoader (only applicable when running in an application context)
7. ApplicationEventPublisherAware's setApplicationEventPublisher (only applicable when running in an application context)
8. MessageSourceAware's setMessageSource (only applicable when running in an application context)
9. ApplicationContextAware's setApplicationContext (only applicable when running in an application context)
10. ServletContextAware's setServletContext (only applicable when running in a web application context)
11. postProcessBeforeInitialization methods of BeanPostProcessors
12. InitializingBean's afterPropertiesSet
13. a custom init-method definition
14. postProcessAfterInitialization methods of BeanPostProcessors

On shutdown of a bean factory, the following lifecycle methods apply:
1. postProcessBeforeDestruction methods of DestructionAwareBeanPostProcessors
2. DisposableBean's destroy
3. a custom destroy-method definition


### IoC
org.springframework.beans和org.springframework.context包是Spring框架的IoC容器的基础。

### AOP
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
### 定义
Netty 是一个用于快速开发可维护的高性能协议服务器和客户端的异步事件驱动的网络应用框架。
### 整体架构
![Netty架构](https://user-images.githubusercontent.com/6687462/159733729-4bc62d8c-1523-43dc-bf37-77ba4b4b1293.png)
### 设计特点
* 各种传输类型的统一API - 阻塞和非阻塞套接字
* 基于灵活且可扩展的事件模型，允许明确分离关注点
* 高度可定制的线程模型——单线程、一个或多个线程池，例如SEDA(即Staged Event-Driven Architecture，核心思想是把一个请求处理过程分成几个Stage，不同资源消耗的Stage使用不同数量的线程来处理，Stage间使用事件驱动的异步通信模式。)
* 真正的无连接数据报套接字支持（自 3.1 起）
### Netty的零拷贝
Netty 支持零复制方法，通过ChannelBuffer“指向”所需的缓冲区，从而消除了执行复制的需要。
![Netty的零拷贝](https://user-images.githubusercontent.com/6687462/159741687-ee0ae96d-00e0-4662-8425-3ae3af9b53e4.png)
### Netty4变化

### Netty5变化（已废弃）
为啥废弃Netty5：https://github.com/netty/netty/issues/4466


**参考资料**<br />
* https://spring.io/projects/spring-boot#overview
* https://netty.io/wiki/new-and-noteworthy-in-5.0.html
* https://netty.io/wiki/new-and-noteworthy-in-4.1.html
* https://netty.io/wiki/new-and-noteworthy-in-4.0.html
* https://netty.io/3.8/guide/#architecture



# 常见工具
## Arthas


# JVM
## JVM工具
|  命令   | 描述  |
|  ----  | ----  |
| jps  | JVM Process Status Tool |
| jstat  | JVM Statistics Monitoring Tool |
| jinfo  | Configuration Info for Java |
| jmap  | Memory Map for Java |
| jstat  | JVM Heap Dump Browser |
| jstack  | Stack Trace for Java |

<img width="1361" alt="常用的JVM工具命令" src="https://user-images.githubusercontent.com/6687462/162473127-dbcec47f-f399-4109-a1cf-d0f49f4cfde8.png">

## 运行时数据区域
线程私有的内存区域有**程序计数器**、**Java虚拟机栈**和**本地方法栈**，程序计数器是Java虚拟机规范中唯一没有要求OOM的地方；<br />
线程公用的有**堆**和**方法区**，方法区在JDK8之前的HotSpot叫做永久代，在JDK8以及之后叫做元数据区，元数据区作为直接内存来管理，只受操作系统内存的限制。<br />
<img width="704" alt="JVM运行时数据区域" src="https://user-images.githubusercontent.com/6687462/160827135-059bc22b-7155-472a-a2d0-496860842008.png">

## 内存分配
对象所需要的内存在类加载完成后便可以完全确定，为对象分配空间的任务等同于把一块确定大小的内存从Java堆中划分出来。

内存分配有两种方式：**指针碰撞**（Bump the Point）和**空闲列表**（Free List）。
* 假设Java堆中内存是绝对规整的，所有用过的内存都放在一边，空闲的内存放在另一边，中间有一个指针作为分界点的指示器，那分配内存就仅仅是把那个指针向空闲那边挪动一段与对象大小相等的距离，这种内存分配方式就是**指针碰撞**。
* 如果Java堆中内存不是规整的，已使用的内存和空闲的内存相互交错，那就没办法简单地进行指针碰撞了，虚拟机就必须维护一个列表，记录哪些内存块是可用的，在分配的时候就从列表中找到一块足够大的空间划分给对象，并更新列表上的记录，这种分配方式就是**空闲列表**。

在使用Serial、ParNew等带压缩（compact）过程的收集器时，系统采用的是指针碰撞，而使用CMS这种基于标记清除（Mark-Sweep）算法的收集器时，通常采用空闲列表。

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

![JVM垃圾收集器](https://user-images.githubusercontent.com/6687462/162468976-2048a597-0c5a-45e3-a872-ae005a882ab0.jpeg)

### Serial（串行）收集器
是最基本、发展历史最悠久的收集器，它是采用复制算法的新生代收集器，曾经（JDK 1.3.1之前）是虚拟机新生代收集的唯一选择。

### ParNew收集器
ParNew收集器就是Serial收集器的多线程版本，它也是一个新生代收集器。除了使用多线程进行垃圾收集外，其余行为包括Serial收集器可用的所有控制参数、收集算法（复制算法）、Stop The World、对象分配规则、回收策略等与Serial收集器完全相同，两者共用了相当多的代码。

### Parallel Scavenge 收集器
Parallel Scavenge收集器也是一个并行的多线程新生代收集器，它也使用复制算法。Parallel Scavenge收集器的特点是它的关注点与其他收集器不同，CMS等收集器的关注点是尽可能缩短垃圾收集时用户线程的停顿时间，而Parallel Scavenge收集器的目标是达到一个可控制的吞吐量（Throughput）。

### Serial Old收集器
Serial Old 是 Serial收集器的老年代版本，它同样是一个单线程收集器，使用“标记-整理”（Mark-Compact）算法。
此收集器的主要意义也是在于给Client模式下的虚拟机使用。如果在Server模式下，它还有两大用途：
* 在JDK1.5 以及之前版本（Parallel Old诞生以前）中与Parallel Scavenge收集器搭配使用。
* 作为CMS收集器的后备预案，在并发收集发生Concurrent Mode Failure时使用。

### Parallel Old收集器
Parallel Old收集器是Parallel Scavenge收集器的老年代版本，使用多线程和“标记-整理”算法。前面已经提到过，这个收集器是在JDK 1.6中才开始提供的，在此之前，如果新生代选择了Parallel Scavenge收集器，老年代除了Serial Old以外别无选择，所以在Parallel Old诞生以后，“吞吐量优先”收集器终于有了比较名副其实的应用组合，在注重吞吐量以及CPU资源敏感的场合，都可以优先考虑Parallel Scavenge加Parallel Old收集器。

### CMS(Concurrent Mark Sweep)
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

**参考资料：**
* https://cloud.tencent.com/developer/article/1592943

## 类加载的过程
分为加载、验证、准备、解析和初始化这五个阶段.
  
**参考资料：**
* 深入理解Java虚拟机：JVM高级特性与最佳实践（第3版）

# Java&操作系统基础

## Java对象锁
Java SE 1.6为了减少获得锁和释放锁带来的性能消耗，引入了“偏向锁”和“轻量级锁”，在Java SE 1.6中，锁一共有4种状态，级别从低到高依次是：无锁状态、偏向锁状态、轻量级锁状态和重量级锁状态，这几个状态会随着竞争情况逐渐升级。锁可以升级但不能降级，意味着偏向锁升级成轻量级锁后不能降级成偏向锁。

synchronized是依赖JVM内部对象Monitor实现的，通过进入与退出Monitor对象实现方法与代码块同步。
监视器锁的实现依赖底层操作系统的Mutex lock（互斥锁）实现的，它的性能较低。同步代码块的synchronized关键字在字节码文件中会被翻译成 **monitorenter** 和 **monitorexit** 两条指令来标志同步代码块的开始位置和结束为止。

锁状态的记录主要存储在markword中，markword的结构如下(以64位为例)：<br />

![HotSpot的对象锁](https://user-images.githubusercontent.com/6687462/162550212-0d9e0c4f-cec0-4fe8-a171-f2766dec0d41.jpeg)

其中最后一位记录了当前对象的锁状态，总共分为三种锁状态，**偏向锁**、**自旋锁（轻量级锁）**、**重量级锁**（对象监视器）。

**参考资料**<br />
* https://www.jianshu.com/p/3ed2f122caa9

## Java引用
Java里面分为强引用、软引用、弱引用、虚引用。<br />
每个线程Thread对象中都保存着一个ThreadLocalMap实例，而ThreadLocalMap中有一个Entry的数组（private Entry[] table;），Entry中的key类型是WeakReference<ThreadLocal>而非ThreadLocal，这样做的目的是为了当我们不再使用或短时间不再使用该ThreadLocal时，哪怕运行中线程的ThreadLocalMap实例有该ThreadLocal的Entry，JVM也能在GC时将ThreadLocal回收，避免内存泄露。
* **强引用**：创建一个对象并把这个对象赋给一个引用变量，就是强引用，宁可OOM也不会释放的引用类型。
* **软引用**：如果一个对象具有软引用，内存空间足够，垃圾回收器就不会回收它。
* **弱引用**：用来描述非必需对象的，当JVM进行垃圾回收时，无论内存是否充足，都会回收被弱引用关联的对象。
* **虚引用**：虚引用和前面的软引用、弱引用不同，它并不影响对象的生命周期。在java中用java.lang.ref.PhantomReference类表示。如果一个对象与虚引用关联，则跟没有引用与之关联一样，在任何时候都可能被垃圾回收器回收。要注意的是，虚引用必须和引用队列关联使用，当垃圾回收器准备回收一个对象时，如果发现它还有虚引用，就会把这个虚引用加入到与之 关联的引用队列中。程序可以通过判断引用队列中是否已经加入了虚引用，来了解被引用的对象是否将要被垃圾回收。


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
### 用户空间与内核空间
针对 Linux 操作系统而言，最高的 1G 字节(从虚拟地址 0xC0000000 到 0xFFFFFFFF)由内核使用，称为内核空间。而较低的 3G 字节(从虚拟地址 0x00000000 到 0xBFFFFFFF)由各个进程使用，称为用户空间。
在CPU的所有指令中，有些指令非常危险，如果错用，将导致系统崩溃，比如清内存、设置时钟等。如果允许所有的程序都可以使用这些指令，那么系统崩溃的概率将大大增加。
所以，CPU将指令分为特权指令和非特权指令，对于那些危险的指令，只允许操作系统及其相关模块使用，普通应用程序只能使用那些不会造成灾难的指令。比如Intel的CPU将特权等级分为4个级别：Ring0~Ring3。
其实Linux系统只使用了Ring0和Ring3 两个运行级别(Windows 系统也是一样的)。当进程运行在Ring3级别时被称为运行在用户态，而运行在Ring0级别时被称为运行在内核态。

### 用户态与内核态
当进程运行在内核空间时就处于内核态，而进程运行在用户空间时则处于用户态。

### Unix中5种I/O模型
* 阻塞式I/O
* 非阻塞式I/O
* I/O复用(select和poll)
* 信号驱动式I/O(SIGIO)
* 异步I/O(POSIX的aio_系列函数)

![IO模型示意图](https://user-images.githubusercontent.com/6687462/87288119-8263cc00-c52d-11ea-9385-28a910c22234.png)

**阻塞式I/O**<br />
请求进程阻塞，直到I/O操作完成，默认情况下，所有套接字都是阻塞的，如下图：<br />
![阻塞IO模型](https://user-images.githubusercontent.com/6687462/87281887-45480b80-c526-11ea-80d2-e994498d99e8.png)

**非阻塞式I/O**<br />
应用进程执行系统调用之后，内核返回一个错误码。应用进程可以继续执行，但是需要不断的执行系统调用来获知I/O是否完成，这种方式称为轮询(polling)。 由于CPU要处理更多的系统调用，因此这种模型是比较低效的。：<br />
![非阻塞IO模型](https://user-images.githubusercontent.com/6687462/87282513-edf66b00-c526-11ea-863b-56e0a5a9e885.png)

**I/O复用**<br />
I/O multiplexing这里面的multiplexing指在单个线程通过记录跟踪每一个Socket(I/O流)的状态来同时管理多个I/O流。使用select或者poll等待数据，并且可以等待多个套接字中的任何一个变为可读，这一过程会被阻塞，当某一个套接字可读时返回。之后再使用recvfrom把数据从内核复制到进程中。如果一个Web服务器没有I/O复用，那么每一个Socket连接都需要创建一个线程去处理。如果同时有几万个连接，那么就需要创建相同数量的线程。并且相比于多进程和多线程技术，I/O 复用不需要进程线程创建和切换的开销，系统开销更小。<br />
![IO多路复用](https://user-images.githubusercontent.com/6687462/87282705-20a06380-c527-11ea-9691-13172894e4c6.png)

**信号驱动式I/O**<br />
应用进程使用 sigaction 系统调用，内核立即返回，应用进程可以继续执行，也就是说等待数据阶段应用进程是非阻塞的。内核在数据到达时向应用进程发送 SIGIO 信号，应用进程收到之后在信号处理程序中调用 recvfrom 将数据从内核复制到应用进程中。<br />
![信号驱动IO](https://user-images.githubusercontent.com/6687462/87285347-01ef9c00-c52a-11ea-8f7d-185d04195451.png)

**异步I/O**<br />
异步I/O和上面提的信号驱动式I/O的主要区别在于信号驱动式I/O是由内核通知我们何时可以启动一个I/O操作，而异步I/O是由内核通知我们I/O操作何时完成。<br />
![异步IO](https://user-images.githubusercontent.com/6687462/87289138-d7541200-c52e-11ea-8a0c-15f8cc1fd113.png)

**五大I/O模型比较**<br />
刚才说了，对于一次IO访问（以read举例），数据会先被拷贝到操作系统内核的缓冲区中，然后才会从操作系统内核的缓冲区拷贝到应用程序的地址空间。所以说，当一个read操作发生时，它会经历两个阶段：
1. 等待数据准备 (Waiting for the data to be ready)
2. 将数据从内核拷贝到进程中 (Copying the data from the kernel to the process)
前四种 I/O 模型的主要区别在于第一个阶段，而第二个阶段是一样的: 将数据从内核复制到应用进程过程中，应用进程会被阻塞。<br />
![五大IO模型比较](https://user-images.githubusercontent.com/6687462/160659131-93818a86-e8d7-4814-8a9b-fe7423537f56.png)


**select、poll和epoll**<br />
select，poll，epoll都是IO多路复用的机制。I/O多路复用就是通过一种机制，一个进程可以监视多个描述符，一旦某个描述符就绪（一般是读就绪或者写就绪），能够通知程序进行相应的读写操作。但select，poll，epoll本质上都是同步I/O，因为他们都需要在读写事件就绪后自己负责进行读写，也就是说这个读写过程是阻塞的，而异步I/O则无需自己负责进行读写，异步I/O的实现会负责把数据从内核拷贝到用户空间。<br />

* select：时间复杂度O(n)，它仅仅知道有I/O事件发生了，却并不知道是哪几个流（可能有一个，多个，甚至全部），我们只能无差别轮询所有流，找出能读出数据，或者写入数据的流，对他们进行操作。所以select具有O(n)的无差别轮询复杂度，同时处理的流越多，无差别轮询时间就越长。
* poll：时间复杂度O(n)，poll本质上和select没有区别，它将用户传入的数组拷贝到内核空间，然后查询每个fd对应的设备状态，但是它没有最大连接数的限制，原因是它是基于链表来存储的.
* epoll：时间复杂度O(1)，epoll可以理解为event poll，不同于忙轮询和无差别轮询，epoll会把哪个流发生了怎样的I/O事件通知我们。所以我们说epoll实际上是事件驱动（每个事件关联上fd
）的，此时我们对这些流的操作都是有意义的。（复杂度降低到了O(1)）

**参考资料：**<br />
* https://developer.ibm.com/articles/j-zerocopy/
* https://www.linuxjournal.com/article/6345
* 《Java并发编程的艺术》
* 《Unix网络编程（卷一）》
* https://www.tqwba.com/x_d/jishu/17958.html
* https://www.cnblogs.com/aspirant/p/9166944.html
* https://pdai.tech/md/java/io/java-io-model.html
* https://segmentfault.com/a/1190000003063859

## 零拷贝
零拷贝主要是用来解决操作系统在处理 I/O 操作时，频繁复制数据的问题。关于零拷贝主要技术有 mmap+write、sendfile和splice等几种方式。无论是传统的 I/O 方式，还是引入了零拷贝之后，2 次 DMA copy是都少不了的。因为两次 DMA 都是依赖硬件完成的。所以，所谓的零拷贝，都是为了减少 CPU copy 及减少了上下文的切换。

**参考资料：**<br />
* https://juejin.cn/post/6995519558475841550

## 伪共享
CPU和内存之间还有个CPU缓存的概念，CPU缓存又分为L1、L2和L3三级；级别数字越小容量也越小，同时离CPU也越近访问速度会越快；L1和L2集成在CPU上，L3集成在主板上，CPU缓存是以缓存行（Cache line）为最小数据单位，缓存行是2的整数幂个连续字节，主流大小是64个字节。如果多个变量同属于一个缓存行，在并发环境下同时修改，因为写屏障及内存一致性协议会导致同一时间只能一个线程操作该缓存行，进而因为竞争导致性能下降，这就是“伪共享”。“伪共享”是高并发场景下一个底层细节问题。
一般而言，缓存行有64字节。

### 如何优化伪共享
C和C++的内存管理特性应该需要对“伪共享”考虑的更多，JAVA语境下是一个值得掌握的并发优化细节。在JAVA中我们可以通过字节对齐和@Contended注解两种方式解决。
* 字节对齐（padding） ：字节对齐是指在并发场景下容易产生“伪共享”的变量对象，按照缓存行的大小进行对齐。比如某个变量需要占用32个字节，然后在额外定义多个字段（比如4个long类型变量字段）来补齐整个缓存行。
字节补齐更合理的方式是在变量的前后进行补齐，且按照2倍的缓存行大小来补齐，即128个字节参考JEP-142。因为缓存行也有预加载的机制，按照前后且2倍大小补齐可以优化预加载机制的负面机制。
* @Contended注解 ：sun.misc.Contended是jdk1.8版本中出现的注解，具体实现原理参考JEP-142。该注解可以用在字段和类上，自动帮我们进行字节补齐。1.8以上推荐使用这种方式，比我们自己实现补齐会更鲁棒，要习惯站在巨人的肩膀上。Contended注解的value可以用来定义分组，比如对象中的两个字段均用@Contended修饰，为了避免两个字段所在的缓存行临近连续，可以分别指定不同的value来隔离。

**参考资料：**<br />
* https://juejin.cn/post/6935407834863501349

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

## 动态规划
动态规划(Dynamic Programming)是一种分阶段求解决策问题的数学思想，它通过把原问题分解为简单的子问题来解决复杂问题动态规划在很多领域都有着广泛的应用例如管理学经济学数学生物学.

### 动态规划 vs 分治法
动态规划也是一种分治思想(比如其状态转移方程就是一种分治)但与分治算法不同的是，分治算法是把原问题分解为若干个子问题，自顶向下求解子问题，合并子问题的解，从而得到原问题的解。动态规划也是把原始问题分解为若干个子问题，然后自底向上，先求解最小的子问题，把结果存在表格中，在求解大的子问题时，直接从表格中查询小的子问题的解，避免重复计算，从而提高算法效率。
