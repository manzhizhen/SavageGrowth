# SavageGrowth
## 帮助程序员找到适合自己的“成长框架”
**让我们抓住这些关键的技术设计**

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
    - [响应式编程](#响应式编程)
- [云](#云)
    - [云计算服务](#云计算服务)
    - [云原生](#云原生)
    - [Service Mesh](#ServiceMesh(服务网格))
    - [Serverless](#Serverless(无服务器))
    - [Quarkus](#Quarkus)
- [存储](#存储)
    - [RDS](#RDS)
        - [MySQL](#MySQL)
    - [NoSQL](#NoSQL)
        - [Redis](#Redis)
        - [Elasticsearch](#Elasticsearch)
        - [MongoDB](#MongoDB)
    - [NewSQL](#NewSQL)
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
        - [Dubbo](#Dubbo)
    - [ZooKeeper](#ZooKeeper)
    - [MQ](#MQ)
      - [RocketMQ](#RocketMQ)
      - [Kafka](#Kafka)
- [分布式追踪系统](#分布式追踪系统)
    - [OpenTelemetry](#OpenTelemetry)
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
    - [Java内存模型（JMM）](#Java内存模型（JMM）)
    - [类加载器](#类加载器)
    - [JVM工具](#JVM工具)
    - [运行时数据区域](#运行时数据区域)
    - [内存分配](#内存分配)
    - [垃圾收集算法](#垃圾收集算法)
    - [垃圾收集器](#垃圾收集器)
    - [类加载的过程](#类加载的过程)
- [Java&操作系统基础](#Java&操作系统基础)
    - [Java对象锁](#Java对象锁)
    - [Java引用](#Java引用) 
    - [多线程](#多线程) 
    - [Loom](#Loom)
    - [I/O](#I/O)     
    - [零拷贝](#零拷贝)       
    - [伪共享](#伪共享)     
- [网络](#网络)
    - [TCP](#TCP)
    - [HTTP](#HTTP)
    - [WebSocket](#WebSocket)
    - [RSocket](#RSocket)
    - [QUIC](#QUIC)
- [数据结构](#数据结构)
    - [BitMap](#BitMap)    
- [算法](#算法)
- [AIGC](#AIGC)
    - [StableDiffusion](#StableDiffusion)
- [硬件](#硬件)
   
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

## 响应式编程
在开发应用程序代码时，我们可以编写两种风格的代码，即命令式和反应式。
* 命令式（Imperative）的代码：它由一组任务组成，每次只运行一项任务，每项任务又都依赖于前面的任务。我们一次一个地按照顺序将代码编写为需要遵循的指令列表。在某项任务开始执行之后，程序在开始下一项任务之前需要等待当前任务完成。在整个处理过程中的每一步，要处理的数据都必须是完全可用的，以便将它们作为一个整体进行处理。
* 响应式（Reactive）的代码：它定义了一组用来处理数据的任务，但是这些任务可以并行地执行。每项任务处理数据的一部分子集，并将结果交给处理流程中的下一项任务，同时继续处理数据的另一部分子集。相对于要求将被处理的数据作为一个整体进行处理，响应式流可以在数据可用时立即开始处理。实际上，传入的数据可能是无限的（比如，一个某个地理位置的实时温度测量数据的恒定流）。
常见的Java响应式库有RxJava，Project-Reactor，Mutiny（Quarkus），RxPY和RxGO都是响应式编程框架，用于在Python和Go语言中构建异步和反应式的应用程序。

响应式编程（Reactive Programming）是一种基于使用异步和事件驱动来处理可观察数据流的编程范式，强调数据流的一致性和实时性。在这种编程模型中，程序会对数据流的变化做出反应，并能够自动地传播这些变化。响应式编程通常通过使用观察者模式（Observer pattern）来实现，它可以简化异步数据流的处理和管理，提高代码的可读性和可维护性。

### RxJava&Reactor
![RxJava-vs-Reactor](https://user-images.githubusercontent.com/6687462/162885783-3def0d9a-adf5-4cb0-88a1-053f528b0218.jpeg)
以下是 RxJava 与 Reactor 之间的主要区别：
* 就已检查异常而言，反应器在 JDK 中包含并使用标准类型的函数依赖，其 API 保留了函数，并且包括在代码中处理已检查异常的差异，并且不允许使用 java.util.function.Function 抛出异常。
* RxJava 有 io.reactive.function。不依赖约束且代码相似的函数会被正确编译。虽然有时不需要检查异常，但 RxJava 使体验得到了极大的增强，并具有一个主要优势。
* Reactor 中的测试模式非常好，但在 RxJava 的情况下并没有那么令人信服，其中 RxJava 包含带有调度程序的外部化配置，并使其替换为单元测试用例。但是在反应器的情况下，可以通过调度程序方便的所有可用配置使测试范式变得非常精简。
* 假设如果存在许多生产环境，那么在这种情况下，不可能使用 RxJava2，那么最优选的一个将是 Reactor，它的调度程序以一种将整个代码包装成一个的方式定义。
* Reactor 使用虚拟时钟，而 Rxjava 的情况不同，它也可以对复杂性进行排序，因为它使用存根进行任何测试套件分析。
* 与 RxJava 相比，Reactor 中的调试功能非常增强和高效，因为 Reactor 包含 Hooks.onOperatorDebug() 标准库，有助于跟踪用于触发整个流中的流的所有信号。尽管如此，它并没有提供一个适当的堆栈来跟踪信号，因为它本身会触发适当的堆栈跟踪 API。与调试方面相比，Rxjava 的情况并非如此，因为它没有提供这个标准库以方便使用。
* Spring 支持 RxJava 1 和 2，但 reactor 也可以在没有 Spring 框架的情况下工作。如果在没有 Spring 框架的情况下使用 Reactor，那么为了保持一致性，必须与 Webflux 紧密集成，包括 Mono 和 Flux 大量集成。并不是说 RxJava 不能很好地与 spring 配合使用；只是因为它涉及一个不需要额外变体的反应器，所以可重用性目的得到了解决。
* 当谈到 android 开发时，RxJava 经常出现。当时，reactor 并没有被推荐，因为 RxJava 有助于解决两个主要问题，一个是将 UI 事件建模为流，另一个是通过线程来回切换以使 I/O 分布均匀。
* 如果以工具的成熟度来判断，那么与 Reactor 相比，推荐的工具将是 RxJava，因为它已在许多项目中使用，因为它具有许多开发人员喜欢的功能。Reactor虽然也自带了很多场景下开发者需要的很多特性，但与RxJava相比，它并不能满足需求。
* 与 RxJava 相比，Reactor 维护的所有流程和 API 都得到了增强和高效，但在实现方面仍然可以很好地满足需求。

### Why was Spring WebFlux created?
Part of the answer is the need for a non-blocking web stack to handle concurrency with a small number of threads and scale with fewer hardware resources. Servlet non-blocking I/O leads away from the rest of the Servlet API, where contracts are synchronous (Filter, Servlet) or blocking (getParameter, getPart). This was the motivation for a new common API to serve as a foundation across any non-blocking runtime. That is important because of servers (such as Netty) that are well-established in the async, non-blocking space.
The other part of the answer is functional programming. Much as the addition of annotations in Java 5 created opportunities (such as annotated REST controllers or unit tests), the addition of lambda expressions in Java 8 created opportunities for functional APIs in Java. This is a boon for non-blocking applications and continuation-style APIs (as popularized by CompletableFuture and ReactiveX) that allow declarative composition of asynchronous logic. At the programming-model level, Java 8 enabled Spring WebFlux to offer functional web endpoints alongside annotated controllers.

### Define “Reactive”
We touched on “non-blocking” and “functional” but what does reactive mean? <br />
The term, “reactive,” refers to programming models that are built around reacting to change network components reacting to I/O events, UI controllers reacting to mouse events, and others. In that sense, non-blocking is reactive, because, instead of being blocked, we are now in the mode of reacting to notifications as operations complete or data becomes available.
There is also another important mechanism that we on the Spring team associate with “reactive” and that is non-blocking back pressure. In synchronous, imperative code, blocking calls serve as a natural form of back pressure that forces the caller to wait. In non-blocking code, it becomes important to control the rate of events so that a fast producer does not overwhelm its destination.
Reactive Streams is a small spec (also adopted in Java 9) that defines the interaction between asynchronous components with back pressure. For example a data repository (acting as Publisher) can produce data that an HTTP server (acting as Subscriber) can then write to the response. The main purpose of Reactive Streams is to let the subscriber control how quickly or how slowly the publisher produces data.

### Common question
what if a publisher cannot slow down? <br />
The purpose of Reactive Streams is only to establish the mechanism and a boundary. If a publisher cannot slow down, it has to decide whether to buffer, drop, or fail.

**参考资料：**<br />
* https://docs.spring.io/spring-framework/docs/current/reference/html/web-reactive.html#webflux-httphandler
* https://www.infoq.com/articles/reactor-by-example/ 这个讲了很多Reactor和RxJava的关系
* https://rxmarbles.com/ 弹珠图集合
* https://www.infoq.com/articles/rxjava-by-example/
* https://www.reactivemanifesto.org/ 响应式宣言
* https://www.reactive-streams.org/ Java的标准化通过Reactive Streams工作出现了，该规范为JVM上的反应库定义了一组接口和交互规则。它的接口已经在Flow类下集成到Java 9中。
* https://reactivex.io/ Rx官网（例如RxJava）
* https://projectreactor.io/ Reactor官网
* https://projectreactor.io/docs/core/release/reference/ Reactor官网中介绍响应式编程
* https://www.educba.com/rxjava-vs-reactor/
* https://github.com/reactive-streams
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
* https://doc.akka.io/docs/akka/current/general/actors.html


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

## Quarkus
Quarkus 是一个开源的 Java 应用程序框架，旨在为构建基于云原生架构的低内存占用、高启动速度、高性能的微服务提供支持。它支持多种编程语言和框架，包括 Java、Kotlin、Scala、Vert.x 和 Spring，可以在多种云环境中运行，包括 Kubernetes 和 OpenShift。Quarkus 还提供了一些工具和扩展，使开发者可以更轻松地构建、测试和部署应用程序。

Quarkus 可以单独使用而不依赖于 Kubernetes，它可以在任何支持 Java 运行时的环境中运行，例如本地计算机、虚拟机或云服务器。Quarkus 还提供了多种构建和部署选项，如使用 Docker 镜像、JAR 包或原生二进制文件等，可以根据需要选择最适合的部署方式。因此，Quarkus 可以适用于各种不同的应用场景和部署环境。

要在 Maven 项目中使用 Quarkus，需要在项目的 pom.xml 文件中添加 Quarkus 的依赖项。以下是添加 Quarkus 依赖项的基本步骤：

打开项目的 pom.xml 文件。
在 dependencies 标签中添加以下依赖项：
<dependency>
<groupId>io.quarkus</groupId>
<artifactId>quarkus-resteasy</artifactId>
<version>2.2.2.Final</version>
</dependency>
这将添加一个名为 quarkus-resteasy 的依赖项，它包含了 Quarkus 中用于构建 RESTful Web 服务的核心组件。

如果需要使用其他 Quarkus 扩展功能，可以根据需要添加其他依赖项。例如，如果需要使用 Quarkus 中的数据库访问功能，可以添加以下依赖项：
<dependency>
<groupId>io.quarkus</groupId>
<artifactId>quarkus-jdbc-postgresql</artifactId>
<version>2.2.2.Final</version>
</dependency>
这将添加一个名为 quarkus-jdbc-postgresql 的依赖项，它包含了 Quarkus 中用于访问 PostgreSQL 数据库的扩展功能。

Quarkus 是一款新型的 Java 应用程序框架，拥有以下几个优势：<br />
1. 快速启动时间：Quarkus 使用了一系列的优化技术，使得应用程序的启动时间可以缩短到几百毫秒级别，这对于云原生应用场景非常有利。
2. 低内存占用：Quarkus 在设计上非常注重内存占用，可以在极低的内存占用下运行，这对于云原生应用场景也非常有利。
3. 高性能：Quarkus 采用了一系列的优化技术，使得应用程序的性能可以得到很大的提升，例如使用 GraalVM 进行 AOT 编译、使用 Reactive 编程模型等。
4. 易于开发：Quarkus 提供了丰富的开发工具和插件，使得开发者可以更加高效地进行开发和调试。
5. 强大的扩展性：Quarkus 提供了丰富的扩展功能，可以轻松地集成各种不同的技术栈，例如数据库、消息队列、缓存等。
6. 高度可配置：Quarkus 提供了大量的可配置选项，可以根据需求灵活地进行配置，例如容器化、部署方式、日志记录等。
综上所述，Quarkus 具有快速启动时间、低内存占用、高性能、易于开发、强大的扩展性和高度可配置等优势，在云原生应用场景下表现出色。


**Quarkus能使Java应用程序启动更快吗？为什么?**<br />
是的，Quarkus 能够使 Java 应用程序启动更快。 Quarkus 采用了多种技术优化 Java 应用程序的启动时间，包括：
1. 基于 SubstrateVM 的 AOT 编译：Quarkus 使用 GraalVM 的 SubstrateVM 对应用程序进行 AOT 编译，将应用程序编译成本地可执行文件，减少了应用程序的冷启动时间。
2. 懒加载：Quarkus 可以根据需要懒加载应用程序的部分组件，减少了应用程序的启动时间。
3. 小型容器：Quarkus 可以在小型容器中运行，减少了容器的启动时间。
4. 轻量级框架：Quarkus 的设计非常注重轻量级和精简，减少了框架本身的启动时间和内存占用。
上述优化措施使得 Quarkus 应用程序的启动时间可以缩短到几百毫秒级别，甚至更短。这对于云原生应用场景非常有利，可以更快地响应用户请求，提升用户体验。

# 存储

## RDS

### MySQL
#### 架构
<img width="1070" alt="MySQL架构图" src="https://user-images.githubusercontent.com/6687462/159244881-02febb00-320a-4aa9-9f43-653c7602ab3b.png">

#### MySQL执行计划
expain出来的信息有10列，分别是id、select_type、table、type、possible_keys、key、key_len、ref、rows、Extra.

概要描述：
* id:选择标识符
* select_type:表示查询的类型。
* table:输出结果集的表
* partitions:匹配的分区
* type:对表访问方式，表示MySQL在表中找到所需行的方式，又称“访问类型”。 常用的类型有： ALL、index、range、ref、eq_ref、const、system、NULL（从左到右，性能从差到好）
* possible_keys:表示查询时，可能使用的索引
* key:表示实际使用的索引
* key_len:索引字段的长度
* ref:列与索引的比较
* rows:扫描出的行数(估算的行数)
* filtered:按表条件过滤的行百分比
* Extra:执行情况的描述和说明

#### MySQL8.0新特性
1. 隐藏索引：隐藏索引的特性对于性能调试非常有用。在 8.0 中，索引可以被“隐藏”和“显示”。当一个索引隐藏时，它不会被查询优化器所使用。也就是说，我们可以隐藏一个索引，然后观察对数据库的影响。如果数据库性能有所下降，就说明这个索引是有用的，于是将其“恢复显示”即可；如果数据库性能看不出变化，说明这个索引是多余的，可以删掉了。
2. 设置持久化：MySQL 的设置可以在运行时通过 SET GLOBAL 命令来更改，但是这种更改只会临时生效，到下次启动时数据库又会从配置文件中读取。MySQL8新增了 SET PERSIST 命令，例如： SET PERSIST max_connections = 500; MySQL 会将该命令的配置保存到数据目录下的 mysqld-auto.cnf 文件中，下次启动时会读取该文件，用其中的配置来覆盖缺省的配置文件。
3. 默认UTF-8编码：从 MySQL 8 开始，数据库的缺省编码将改为 utf8mb4，这个编码包含了所有 emoji 字符。 多少年来我们使用 MySQL 都要在编码方面小心翼翼，生怕忘了将缺省的 latin 改掉而出现乱码问题。从此以后就不用担心了。 
4. 通用表表达式（Common Table Expressions）：复杂的查询会使用嵌入式表，例如： SELECT t1.a1, t2.a2 FROM (SELECT col1 FROM table1) t1, (SELECT col2 FROM table2) t2; 而有了 CTE，我们可以这样写：
WITH t1 AS (SELECT col1 FROM table1), t2 AS (SELECT col2 FROM table2) SELECT t1.a1, t2.a2 FROM t1, t2;  这样看上去层次和区域都更加分明，改起来也更清晰的知道要改哪一部分。
5. 窗口函数（Window Functions）：MySQL 被吐槽最多的特性之一就是缺少 rank() 函数，当需要在查询当中实现排名时，必须手写@变量。但是从 8.0 开始，MySQL 新增了一个叫窗口函数的概念，它可以用来实现若干新的查询方式。 窗口函数有点像是 SUM()、COUNT() 那样的集合函数，但它并不会将多行查询结果合并为一行，而是将结果放回多行当中。也就是说，窗口函数是不需要 GROUP BY 的。

#### InnoDB的锁
##### 共享锁和独占锁
InnoDB实现标准的行级锁定，其中有两种类型的锁， **共享锁(shared lock)** 和 **独占锁(exclusive lock)**。
* 共享锁(S)：允许持有该锁的事务读取一行，即其他会话可以读取被锁定的行，但是不能修改，直到当前事务结束。例如 select * from T where id=1 lock in share mode;
* 独占锁(X)：允许持有该锁的事务更新或删除一行，其他会话不能读取或修改被锁定的行，直到当前事务结束。例如 select * from T where id=1 for update;

##### 意向锁(Intention Locks)
意向锁（Intention Locks）是为了协调共享锁（Shared Locks）和排他锁（Exclusive Locks）的使用而存在的。意向锁是一种低级别的锁，用于表示事务准备在某个级别（如行级别或表级别）上设置锁定。它们并不是直接用来锁定数据的，而是用来表示某个事务打算在特定级别上设置锁。
共享锁和排他锁是针对具体数据行或数据表的锁定，共享锁用于读操作，允许多个事务同时获取共享锁，而排他锁用于写操作，一次只允许一个事务获取排他锁。
意向锁不会直接锁定数据，它们只是用来指示某个事务打算在更低级别上设置锁定。这种机制可以帮助数据库管理系统更有效地协调锁定，从而提高并发性能和减少死锁的风险。

意向锁属于表级锁，有两种类型的意图锁：
* 意向共享锁(IS)：表示事务打算在表中的各个行上设置 共享 锁 。
* 意向排它锁(IX)：表示事务打算对表中的各个行设置排他锁。
例如，SELECT ... FOR SHARE设置一个意向共享锁，并 SELECT ... FOR UPDATE设置一个意向排它锁。

##### 记录锁(Record Locks)
记录锁是对索引记录的锁。例如， SELECT c1 FROM t WHERE c1 = 10 FOR UPDATE; 阻止任何其他事务插入、更新或删除值为 的t.c1行 10。记录锁总是锁定索引记录，即使定义的表没有索引。对于这种情况，InnoDB创建一个隐藏的聚集索引并将该索引用于记录锁定。

##### 间隙锁(Gap Locks)
间隙锁是在索引记录之间的间隙上的锁，或在第一条索引记录之前或最后一条索引记录之后的间隙上的锁。例如，SELECT c1 FROM t WHERE c1 BETWEEN 10 and 20 FOR UPDATE;阻止其他事务将值15插入 column t.c1，
无论该列中是否已经存在任何此类值，因为该范围内所有现有值之间的间隙都已锁定。

间隙可能跨越单个索引值、多个索引值，甚至是空的。

间隙锁是性能和并发性之间权衡的一部分，并且用于某些事务隔离级别而不是其他级别。

使用唯一索引锁定行以搜索唯一行的语句不需要间隙锁定。（这不包括搜索条件仅包括多列唯一索引的某些列的情况；在这种情况下，确实会发生间隙锁定。）
例如，如果该id列具有唯一索引，则以下语句仅使用值为 100的行的索引记录锁，id其他会话是否在前面的间隙中插入行无关紧要：
SELECT * FROM child WHERE id = 100;
如果id没有索引或具有非唯一索引，则该语句会锁定前面的间隙。

这里还值得注意的是，不同的事务可以在间隙上持有冲突的锁。例如，事务 A 可以在一个间隙上持有一个共享间隙锁（gap S-lock），而事务 B 在同一个间隙上持有一个排他性间隙锁（gap X-lock）。允许冲突间隙锁的原因是，如果从索引中清除记录，则必须合并不同事务在记录上持有的间隙锁。

间隙锁定InnoDB是“纯粹的抑制性”，这意味着它们的唯一目的是防止其他事务插入到间隙中。间隙锁可以共存。一个事务采用的间隙锁不会阻止另一个事务在同一间隙上采用间隙锁。共享和独占间隙锁之间没有区别。它们彼此不冲突，并且执行相同的功能。

可以显式禁用间隙锁定。如果您将事务隔离级别更改为 ，则会发生这种情况 READ COMMITTED。在这种情况下，间隙锁定对搜索和索引扫描禁用，仅用于外键约束检查和重复键检查。

##### Next-Key Locks
下一个键锁是索引记录上的记录锁和索引记录之前的间隙上的间隙锁的组合。
InnoDB执行行级锁定的方式是，当它搜索或扫描表索引时，它会在它遇到的索引记录上设置共享或排他锁。因此，行级锁实际上是索引记录锁。索引记录上的 next-key 锁定也会影响该索引记录之前的“ gap ”。也就是说，next-key 锁是索引记录锁加上索引记录前面的间隙上的间隙锁。如果一个会话在索引中的记录上具有共享或排他锁 R，则另一个会话不能 R在索引顺序中紧接之前的间隙中插入新的索引记录。
假设索引包含值 10、11、13 和 20。该索引可能的下一个键锁定涵盖以下区间，其中圆括号表示排除区间端点，方括号表示包含端点：
(负无穷大, 10]
(10, 11]
(11, 13]
(13, 20]
(20, 正无穷大)
对于最后一个间隔，next-key lock 锁定索引中最大值上方的间隙，并且“ supremum ” 伪记录的值高于索引中的任何实际值。上界不是真正的索引记录，因此，实际上，这个下一个键锁只锁定最大索引值之后的间隙。

默认情况下，InnoDB在 REPEATABLE READ事务隔离级别下运行。在这种情况下，InnoDB使用 next-key 锁进行搜索和索引扫描，这可以防止幻行

##### 插入意向锁
插入意向锁是一种 INSERT在行插入之前由操作设置的间隙锁。该锁表示插入的意图，即如果插入到同一索引间隙中的多个事务没有在间隙内的同一位置插入，则它们不需要相互等待。假设有值为 4 和 7 的索引记录。分别尝试插入值 5 和 6 的单独事务，在获得插入行的排他锁之前，每个使用插入意图锁锁定 4 和 7 之间的间隙，但不要相互阻塞，因为行是不冲突的。

##### InnoDB默认的事务隔离级别
在可重复读隔离级别，对于锁定读取 （SELECT with FOR UPDATE或FOR SHARE）、 UPDATE和 DELETE语句，锁定取决于语句是使用具有唯一搜索条件的唯一索引还是范围类型的搜索条件。
* 对于具有唯一搜索条件的唯一索引， InnoDB只锁定找到的索引记录，而不锁定 它之前 的间隙。
* 对于其他搜索条件，InnoDB 锁定扫描的索引范围，使用 间隙锁 或 Next-Key锁 来阻止其他会话插入该范围所覆盖的间隙。

数据库状态的快照适用 SELECT于事务中的语句，不一定适用于 DML语句。如果您插入或修改某些行然后提交该事务， 则从另一个并发事务发出的DELETE或 语句 可能会影响那些刚刚提交的行，即使会话无法查询它们。
如果一个事务确实更新或删除了由不同事务提交的行，那么这些更改对当前事务是可见的。例如，您可能会遇到如下情况：
```
SELECT COUNT(c1) FROM t1 WHERE c1 = 'xyz';
-- Returns 0: no rows match.
DELETE FROM t1 WHERE c1 = 'xyz';
-- Deletes several rows recently committed by other transaction.

SELECT COUNT(c2) FROM t1 WHERE c2 = 'abc';
-- Returns 0: no rows match.
UPDATE t1 SET c2 = 'cba' WHERE c2 = 'abc';
-- Affects 10 rows: another txn just committed 10 rows with 'abc' values.
SELECT COUNT(c2) FROM t1 WHERE c2 = 'cba';
-- Returns 10: this txn can now see the rows it just updated.
```

#### MVCC(Multi-Version Concurrency Control)
MVCC是为了实现事务的隔离性，通过版本号，避免同一数据在不同事务间的竞争，你可以把它当成基于多版本号的一种乐观锁。当然，这种乐观锁只在事务级别**读已提交**和**可重复读**有效。MVCC最大的好处，相信也是耳熟能详：读不加锁，读写不冲突。在读多写少的OLTP应用中，读写不冲突是非常重要的，极大的增加了系统的并发性能。

InnoDB存储引擎在数据库每行数据的后面添加了三个字段
* 6字节的**事务ID(DB_TRX_ID)**字段：用来标识最近一次对本行记录做修改(insert|update)的事务的标识符，即最后一次修改(insert|update)本行记录的事务id。至于delete操作，在innodb看来也不过是一次update操作，更新行中的一个特殊位将行表示为deleted，并非真正删除。
* 7字节的**回滚指针(DB_ROLL_PTR)**字段：指写入回滚段(rollback segment)的 undo log record (撤销日志记录记录)。如果一行记录被更新, 则 undo log record 包含 ‘重建该行记录被更新之前内容’ 所必须的信息。
* 6字节的**行号(DB_ROW_ID)**字段：包含一个随着新行插入而单调递增的行ID，当由innodb自动产生聚集索引时，聚集索引会包括这个行ID的值，否则这个行ID不会出现在任何索引中。

在多版本并发控制中，为了保证数据操作在多线程过程中，保证事务隔离的机制，降低锁竞争的压力，保证较高的并发量。在每开启一个事务时，会生成一个事务的版本号，被操作的数据会生成一条新的数据行（临时），但是在提交前对其他事务是不可见的，对于数据的更新（包括增删改）操作成功，会将这个版本号更新到数据的行中，事务提交成功，将新的版本号更新到此数据行中，这样保证了每个事务操作的数据，都是互不影响的，也不存在锁的问题。

**MVCC下的CRUD**<br />
* SELECT：当隔离级别是REPEATABLE READ时select操作，InnoDB必须每行数据来保证它符合两个条件： a.InnoDB必须找到一个行的版本，它至少要和事务的版本一样老(也即它的版本号不大于事务的版本号)。这保证了不管是事务开始之前，或者事务创建时，或者修改了这行数据的时候，这行数据是存在的。 b. 这行数据的删除版本必须是未定义的或者比事务版本要大。这可以保证在事务开始之前这行数据没有被删除。  符合这两个条件的行可能会被当作查询结果而返回。
* INSERT：InnoDB为这个新行记录当前的系统版本号。
* DELETE：InnoDB将当前的系统版本号设置为这一行的删除ID。
* UPDATE：InnoDB会写一个这行数据的新拷贝，这个拷贝的版本为当前的系统版本号。它同时也会将这个版本号写到旧行的删除版本里。

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
**undolog**：InnoDB存储引擎层的回滚日志，保存了事务发生之前的数据的一个版本，用于事务的回滚。和redolog一样，也是采用循环写，即固定文件大小，如果写到文件末尾，又从头写。<br />

#### 参考资料
* https://dev.mysql.com/doc/refman/8.0/en/group-replication.html
* https://dev.mysql.com/doc/refman/8.0/en/binlog.html
* https://docs.oracle.com/cd/E17952_01/mysql-8.0-en/innodb-locking-transaction-model.html
* https://docs.oracle.com/cd/E17952_01/mysql-8.0-en/innodb-consistent-read.html

## NoSQL
NoSQL常见的四种类型：键值对型、文档型、列式存储型和图型。

### Redis
#### 定义
Redis是一种采用内存来作为数据结构存储的数据库、缓存和消息代理。<br />

#### 部署说明
Redis是用ANSI C编写，并且可以在大多数POSIX系统中使用，例如Linux，* BSD，OS X，而无需外部依赖。Linux和OS X是Redis开发和测试最多的两个操作系统，我们建议使用Linux进行部署。<br/>

#### 支持的数据结构
String，List，Set，Hash，Sorted Set, Stream(Redis 5.0才有)，Geospatial indexes（地理空间索引），Bitmaps等。<br/>

#### 内部数据结构
简单动态字符串(Simple Dynamic Strings, SDS)、双端链表、跳跃表(skiplist)、压缩列表、快速列表(Redis3.2引入，quicklist)、字典(散列表)、整数集合(intset)。
##### 跳跃表
考虑一个有序表
    * ![redis跳跃表1](https://user-images.githubusercontent.com/6687462/162159457-d64d7b92-5ad1-40d0-a10d-7a3c7a74e3ec.png)
    * 从该有序表中搜索元素 < 23, 43, 59 > ，需要比较的次数分别为 < 2, 4, 6 >，总共比较的次数为 2 + 4 + 6 = 12 次。有没有优化的算法吗? 链表是有序的，但不能使用二分查找。类似二叉
搜索树，我们把一些节点提取出来，作为索引。得到如下结构：
    * ![redis跳跃表2](https://user-images.githubusercontent.com/6687462/162159488-56f245cf-06b6-44de-84b3-9e884cfb4e37.jpg)
    * 这里我们把 < 14, 34, 50, 72 > 提取出来作为一级索引，这样搜索的时候就可以减少比较次数了。 我们还可以再从一级索引提取一些元素出来，作为二级索引，变成如下结构：
    * ![redis跳跃表3](https://user-images.githubusercontent.com/6687462/162159508-f8d30a4c-a725-4100-b4a9-2ae24309885c.jpg)
    * 这里元素不多，体现不出优势，如果元素足够多，这种索引结构就能体现出优势来了。

实际上，Redis中Sorted Set的实现是这样的：
* 当数据较少时，sorted set是由一个ziplist来实现的。
* 当数据多的时候，sorted set是由一个dict + 一个skiplist来实现的。简单来讲，dict用来查询数据到分数的对应关系(例如zscore的查询)，而skiplist用来根据分数查询数据（可能是范围查找）。

#### Redis Pipeline
当客户端使用管道发送命令时，服务器将被迫使用内存对回复进行排队。因此，如果您需要通过管道发送大量命令，最好将它们分批发送，每个批次包含合理的数量，例如 10k 个命令，读取回复，然后再次发送另外 10k 个命令，依此类推。速度几乎相同，但使用的额外内存最多是对这 10k 命令的回复进行排队所需的内存量。

#### Redis是单线程的。如何利用多个多核CPU？
CPU成为Redis瓶颈的情况并不常见，因为Redis通常是内存或网络绑定的。例如，在一个普通的Linux系统上运行的流水线Redis每秒甚至可以传递100万个请求，所以如果您的应用程序主要使用O（N）或O（log（N））命令，它几乎不会占用太多的CPU。
但是，为了最大限度地利用CPU，可以在同一个机器中启动多个Redis实例，并将它们视为不同的服务器。然而，随着Redis 4.0的推出，我们开始让Redis多线程化。
目前，这仅限于在后台删除对象，以及阻止通过Redis模块实现的命令。对于未来的版本，计划是让Redis越来越多线程化。

#### Redis6的多线程特性
Redis的多线程部分只是用来处理网络数据的读写和协议解析，执行命令仍然是单线程顺序执行。所以我们不需要去考虑控制 key、lua、事务，LPUSH/LPOP 等等的并发及线程安全问题。

#### 持久化方案
Redis持久化方案分为RDB和AOF两种。<br/>
RDB(Redis DataBase)：按指定的时间间隔执行数据集的时间点快照。 <br />
AOF(Append Only File)：会记录服务器接收的每个写入操作，这些操作将在服务器启动时再次播放，以重建原始数据集。使用与Redis协议本身相同的格式记录命令，并且采用追加方式。当日志太大时，Redis可以在后台重写日志。 

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

Redis 集群 TCP 端口
每个Redis 集群节点都需要两个开放的TCP 连接：一个用于为客户端提供服务的Redis TCP 端口（例如6379）和第二个端口（称为集群总线端口）。默认情况下，集群总线端口是通过在数据端口上加10000来设置的（例如16379）；但是，您可以在配置中覆盖它cluster-port。

集群总线是一种使用二进制协议的节点到节点的通信通道，由于带宽和处理时间较小，更适合在节点之间交换信息。节点使用集群总线进行故障检测、配置更新、故障转移授权等。客户端永远不应尝试与集群总线端口进行通信，而应使用 Redis 命令端口。但是，请确保在防火墙中打开这两个端口，否则 Redis 集群节点将无法通信。

Redis Cluster 并不直接使用传统的一致性哈希算法，它采用了一种叫做哈希槽（hash slot）的机制来分配和管理键空间。这种方法有点类似于一致性哈希，但在实现和分布策略上有所不同。
在Redis Cluster中，整个键空间被分成了16384个哈希槽（slots），每个键通过CRC16算法计算出一个结果，然后对16384取模来决定应该放入哪个哈希槽。每个Redis节点负责一部分的哈希槽，当添加或移除节点时，会重新分配哈希槽的负责权。

Redis Cluster的哈希槽特点：
1. 固定数量的槽位:哈希槽的数量总是16384，不会随着节点的增加或减少而改变。
2. 键到槽位的映射:通过对键（或者键的一部分）进行哈希运算来确定其属于哪个槽位。
3. 槽位到节点的映射:每个槽位都对应到集群中的一个节点，可以是主节点也可以是从节点。
4. 重分配槽位:当增加或移除节点时，Redis Cluster会自动将部分槽位重新分配到新的节点上，这个过程叫做resharding。
5. 高可用性:Redis Cluster通过使用主从复制来保证每个槽位的高可用性，当主节点失效时，其中一个从节点可以升级为新的主节点。
一致性哈希算法通常用于分布式缓存系统，如Memcached，它通过一个环形的哈希空间来分配数据，当添加或移除节点时，只影响环上相邻位置的数据分配。相比之下，Redis Cluster的哈希槽方法在重新分配槽位时可能会影响较多的键，但它也提供了一个更为直观和简单的系统管理方式。

例如，您可能有一个具有3个节点的集群，其中：
* 节点 A 包含从 0 到 5500 的哈希槽。
* 节点 B 包含从 5501 到 11000 的哈希槽。
* 节点 C 包含从 11001 到 16383 的哈希槽。

Redis Cluster 的哈希槽（hash slots）机制与一致性哈希（Consistent Hashing）在解决数据分布和节点扩展性问题上有相似之处，但它们之间还是存在一些本质区别的。下面我会概述两者的相似之处和区别。

哈希槽和一致性哈希相似之处：
1. 数据分布： 两者都是为了在分布式系统中实现数据的均匀分布。
2. 扩展性： 两者都考虑了节点的动态添加或移除，并尝试在这些操作发生时最小化数据迁移的影响。

哈希槽和一致性哈希的区别：
1. 哈希空间划分：
一致性哈希通常将哈希空间划分为一个连续的环形空间，节点和数据通过哈希函数直接映射到环上的位置。
Redis Cluster将哈希空间划分为固定数量（16384）的哈希槽，数据根据其键计算出的哈希值映射到这些离散的槽中，每个节点负责一部分槽。
2. 数据分配策略：
一致性哈希为了提高均衡性，通常会使用虚拟节点技术，即将每个物理节点映射成多个虚拟节点，以分散到整个哈希环上。
Redis Cluster不使用虚拟节点，而是直接将哈希槽分配给物理节点。
3. 节点变更：
一致性哈希在节点增减时，影响的数据只是环上相邻节点之间的数据，数据迁移量相对较少。
Redis Cluster在节点变更时，受影响的是该节点负责的所有槽以及对应的数据，可能需要大量数据迁移。但由于Redis Cluster中对数据进行了分片，所以在实践中，每个节点变更需要迁移的数据仍然是可控的。
4. 实现复杂性：
一致性哈希通常在实现时较为复杂，需要管理虚拟节点到物理节点的映射，以及在节点变更时对环上的数据重新分配。
Redis Cluster通过预分配的哈希槽简化了实现，管理起来更为直观。

总的来说，虽然Redis Cluster的哈希槽机制与一致性哈希都旨在实现分布式系统中数据的均衡分布和扩展性，但它们在实现细节和原理上有所不同。Redis Cluster的设计选择了一种简化的方法来达到类似的目标，同时也使得集群管理更为容易和直观。

这允许在集群中轻松添加和删除节点。例如，如果我想添加一个新节点 D，我需要将一些哈希槽从节点 A、B、C 移动到 D。同样，如果我想从集群中删除节点 A，我可以只移动 A 服务的哈希槽到 B 和 C。当节点 A 为空时，我可以将它完全从集群中删除。因为将哈希槽从一个节点移动到另一个节点不需要停止操作，添加和删除节点，或者更改节点持有的哈希槽的百分比，不需要任何停机时间。
Redis Cluster 支持多个 key 操作，只要涉及到单个命令执行（或整个事务，或 Lua 脚本执行）的所有 key 都属于同一个 hash slot。用户可以通过使用称为哈希标签的概念来强制多个键成为同一个哈希槽的一部分。
哈希标签记录在 Redis Cluster 规范中，但要点是，如果键中的 {} 括号之间有子字符串，则仅对字符串内的内容进行哈希处理，例如this{foo}key和another{foo}key 保证在同一个哈希槽中, 并且可以在具有多个键作为参数的命令中一起使用。

* Redis Cluster 无法保证强一致性。实际上，这意味着在某些情况下，Redis 集群可能会丢失系统向客户端确认的写入。 Redis Cluster 可能丢失写入的第一个原因是因为它使用异步复制。这意味着在写入期间会发生以下情况：
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


#### Redisson
Redisson是Redis主流的Java客户端之一，相比Jedis原封不动的包装Redis的API，Redisson提供了

```java
    @Override
    public boolean tryLock() {
        return get(tryLockAsync());
    }

    <T> RFuture<T> tryLockInnerAsync(long waitTime, long leaseTime, TimeUnit unit, long threadId, RedisStrictCommand<T> command) {
        return evalWriteAsync(getRawName(), LongCodec.INSTANCE, command,
                "if (redis.call('exists', KEYS[1]) == 0) then " +
                        "redis.call('hincrby', KEYS[1], ARGV[2], 1); " +
                        "redis.call('pexpire', KEYS[1], ARGV[1]); " +
                        "return nil; " +
                        "end; " +
                        "if (redis.call('hexists', KEYS[1], ARGV[2]) == 1) then " +
                        "redis.call('hincrby', KEYS[1], ARGV[2], 1); " +
                        "redis.call('pexpire', KEYS[1], ARGV[1]); " +
                        "return nil; " +
                        "end; " +
                        "return redis.call('pttl', KEYS[1]);",
                Collections.singletonList(getRawName()), unit.toMillis(leaseTime), getLockName(threadId));
    }
```

**参考资料**
* https://redis.io/docs/manual/pipelining/ Redis Pipeline
* https://www.jianshu.com/p/c2841d65df4c
* https://redis.io/
* https://redis.io/topics/distlock
* https://redis.io/docs/management/scaling/   Redis Cluster
* https://redis.io/docs/reference/cluster-spec/  Redis Cluster 规范
* https://www.jianshu.com/p/7e47a4503b87
* https://blog.tienyulin.com/redis-master-slave-replication-sentinel-cluster/
* http://doc.redisfans.com/
* https://www.elastic.co/cn/elasticsearch/
* https://github.com/elastic/elasticsearch
* https://redis.io/topics/faq
* https://www.cnblogs.com/madashu/p/12832766.html
* https://redis.io/docs/reference/patterns/distributed-locks/  Redis分布式锁
* http://antirez.com/news/101  RedLock安全吗？
* https://mp.weixin.qq.com/s?__biz=MzA4NTg1MjM0Mg==&mid=2657261425&idx=1&sn=d840079ea35875a8c8e02d9b3e44cf95&scene=0#wechat_redirect  Redis为什么用跳表而不用平衡树？

### Elasticsearch

#### 定义
Elasticsearch是一个分布式、RESTful风格的搜索和数据分析引擎。<br />
它为所有类型的数据提供近乎实时的搜索和分析，无论您是结构化文本还是非结构化文本，数字数据或地理空间数据，Elasticsearch都能以支持快速搜索的方式有效地对其进行存储和索引。

Elasticsearch：index --> type --> doc --> field<br />
MySQL: 数据库 --> 数据表 --> 行 --> 列

#### Index

#### Type（已废弃）
* 在 5.X 版本中，一个 index 下可以创建多个 type；
* 在 6.X 版本中，一个 index 下只能存在一个 type；
* 在 7.X 版本中，直接去除了 type 的概念，就是说 index 不再会有 type。

#### 特点
建立在Apache Lucene之上、分布式、高可用、多租户、API丰富、面向文档；
**配合使用**<br />
Logstash|Beats（收集） + Elasticsearch（存储、分析） + Kibana（展现）

#### Elasticsearch保证高可用性的方式
* 方式一：副本分片。主分片失效后，副本分片会被提升为主分片。
* 方式二：跨集群复制主从同步。简称：CCR，指的是索引数据从一个 Elasticsearch 集群复制到另一个 Elasticsearch 集群。对于主集群的索引数据的任何修改都会直接复制同步到从索引集群。
* 方式三：快照。快照在给定时刻对集群或者索引按了暂停键且拍摄了当时的全部“照片”。这样，当在之后的某个时间点，倘若集群或索引出现故障，可以基于之前的快照进行快速恢复。

**扩展知识点：** HyperLogLog<br />

**参考资料：** 


### MongoDB
MongoDB是一种高性能、开源、无模式的文档型数据库，它是以键值对（BSON，一种类似JSON的格式）存储数据。MongoDB的设计目标是为了提高可扩展性和易用性，它支持字段、范围查询、正则表达式等高级查询功能，还支持全文搜索和地理空间搜索。
以下是MongoDB的基本架构组件：
1. **文档（Document）**：MongoDB的数据单元是文档，文档类似于JSON对象，实际上是BSON格式的数据。文档可以包含多种数据类型（如字符串、数字、数组、子文档等）。
2. **集合（Collection）**：集合是一组文档，类似于关系型数据库中的表。集合是无模式的，这意味着集合中的文档可以拥有不同的字段。但是实践中，同一集合中的文档通常具有相似的结构。
3. **数据库（Database）**：MongoDB的物理容器，包含集合的集合。每个数据库都有自己的文件集，并独立于其他数据库。
4. **索引（Index）**：为了提高查询效率，可以在一个或多个字段上创建索引。和关系型数据库一样，索引维护一个特定排序的数据结构，使得检索更加快速。

MongoDB支持的一些关键特性包括：
- **复制集（Replication）**：MongoDB可以提供数据的高可用性，通过复制集来实现。一个复制集包含多个MongoDB服务器，其中有一个是主节点（primary）负责处理客户端请求，其他是从节点（secondary）负责复制主节点上的数据。如果主节点宕机，其中一个从节点可以自动晋升为新的主节点。
- **分片（Sharding）**：为了支持大规模的数据分布和查询，MongoDB支持水平分片，即将数据分布在多个服务器上。分片可以提高系统的扩展性和吞吐量。
- **聚合框架（Aggregation Framework）**：它提供了一个操作数据的管道，可以执行诸如过滤、转换、组合等多种数据处理操作。

MongoDB的使用场景广泛，主要包括：
- **内容管理和交付**：MongoDB的文档模型可以很好地映射复杂的内容形式，适合内容管理系统（CMS）。
- **移动和社交基础设施**：由于MongoDB的高扩展性和性能，它适合用于后端数据存储，为大规模移动应用或社交网络提供支持。
- **用作操作数据存储**：在许多实时应用中，比如游戏或交互式服务，MongoDB能够提供快速读写的能力，以及对大量实时数据的处理。
- **物联网（IoT）**：IoT应用往往产生巨量的数据，MongoDB能够存储不同类型的数据，并能快速查询。
- **数据集成和ETL（Extract, Transform, Load）**：MongoDB的灵活性使其成为数据集成项目的理想选择，特别是需要处理多样化和不结构化数据的场合。
- **大数据分析和聚合**：聚合框架使MongoDB成为执行复杂的数据分析和聚合的有力工具。

MongoDB适用于对数据库模式设计不确定、数据结构变化频繁或需要水平扩展的场合。需要注意的是，虽然MongoDB是高性能且灵活的数据库系统，但它并不适合

#### MongoDB集群部署角色
在MongoDB的集群部署中，各个MongoDB实例可能扮演以下几种角色：

* **主节点（Primary）**:
在复制集中，主节点负责处理客户端的所有写操作。
主节点也可以处理读操作，但为了分散读取压力，通常会配置从节点来处理读请求。
在复制集中，同时只能有一个主节点。
主节点将操作记录到操作日志（oplog），从节点会复制并应用这些操作来保持与主节点的数据同步。
* **从节点（Secondary）**:
从节点复制主节点的操作日志并重新应用这些操作，以此来同步数据。
可以配置从节点来处理读请求，以分散从主节点的读取压力。
在主节点宕机的情况下，从节点可以通过选举机制提升为新的主节点。
* **仲裁者（Arbiter）**:
仲裁者是复制集中的一个可选角色，它不存储数据，只参与选举过程。
当复制集成员数量为偶数时，仲裁者可以帮助避免“脑裂”（split-brain）问题，即防止出现两个主节点。
* **查询路由器（mongos）**:
在分片集群中，mongos作为查询路由器，接受客户端请求并将其定向到适当的分片。
它还处理集群中的分片键和路由逻辑，客户端和应用程序通常只与mongos实例交互。
* **配置服务器（Config Server）**:
配置服务器存储了整个分片集群的元数据和配置信息。
它包含了关于集群中分片、分片键以及集群的其它重要信息。
在一个分片集群中，通常会有三个配置服务器，以确保高可用性。
* **分片（Shard）**:
分片可以是单个的MongoDB实例，或者更常见的是一个复制集，负责存储数据集的一个子集。
分片使得MongoDB数据库能够水平扩展，通过增加更多的分片来处理更多数据和更高的负载。
这些角色共同工作，以确保MongoDB集群能够有效地处理大规模数据的存储、查询和更新。在设计MongoDB集群时，需要根据应用程序的需求和预期负载来合理配置各种角色。

#### MongoDB常见部署方式
MongoDB支持几种常见的集群部署方式，以满足不同的应用需求、数据量和系统负载。这些部署方式主要包括：
##### 1. 单节点部署
虽然并非集群部署，但单节点部署是最简单的MongoDB部署方式，通常用于开发、测试环境或者小型应用。
##### 2. 复制集部署
复制集提供了数据冗余和高可用性。一个复制集由多个MongoDB服务器（节点）组成，通常包括一个主节点和多个从节点，还可以包括一个仲裁者节点来参与选举过程。
##### 3. 分片部署（Sharded Cluster）
分片部署是MongoDB的水平扩展解决方案。它由多个分片组成，每个分片可以是单个MongoDB服务器或者一个复制集，用于存储数据的不同部分。分片集群也包括查询路由器（mongos）和配置服务器（config servers）来管理集群的元数据和操作路由。
##### 4. 复制集与分片结合部署
为了同时实现高可用性和水平扩展，一个MongoDB集群可以配置为分片，且每个分片自身为一个复制集。这样的部署方式结合了复制和分片的优点。
##### 5. 多地域部署
多地域部署通过在不同的地理位置部署复制集成员来提供数据局部性和灾难恢复。这种部署方式可以减少数据中心故障的影响，并优化全球分布应用的性能。
##### 6. 云部署
MongoDB也可以部署在云平台上，如Amazon Web Services (AWS)、Google Cloud Platform (GCP)和Microsoft Azure等。MongoDB自己的云服务MongoDB Atlas提供了完全托管的MongoDB部署，包括复制集和分片，以及自动备份、监控和自动扩展等功能。

在选择MongoDB的集群部署方式时，需要考虑以下因素：

- 数据量的大小和增长速度
- 系统的读写负载
- 高可用性和故障恢复的要求
- 数据局部性和全球分布需求
- 维护和管理的复杂性
- 预算和资源限制

每种部署方式都有其使用场景，通常需要在性能、可用性、复杂性和成本之间权衡，以确定最适合应用需求的部署策略。


## NewSQL
### TiDB
TiDB（“Ti”代表 Titanium）是一个开源的 NewSQL 数据库，支持混合事务和分析处理 (HTAP) 工作负载。它兼容 MySQL，具有水平可扩展性、强一致性和高可用性。

#### 参考资料
* https://github.com/pingcap/tidb
* https://docs.pingcap.com/tidb/stable/basic-features
* https://pingcap.com/zh/case/user-case-zhihu TiDB在知乎万亿量级业务数据下的实践 

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
2PC协议相对简单，容易实现，是理解和设计分布式事务系统的基础。
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
1. 引入超时机制。同时在协调者和参与者中都引入超时机制。
2. 在第一阶段和第二阶段中插入一个准备阶段。保证了在最后提交阶段之前各参与节点的状态是一致的。

优点：<br />
1. 非阻塞协议: 3PC通过引入超时机制和额外的阶段来避免参与者在故障情况下无限期等待协调者的决定，从而解决了2PC的阻塞问题。
2. 减少单点故障风险: 增加的“预提交”阶段允许参与者在协调者故障时进行单独的决策，从而避免了因协调者故障导致的系统停滞。
3. 快速失败恢复: 与2PC相比，3PC能够更快地检测故障并作出决策，参与者可以在超时后自动进行提交或回滚，而不是无限等待。
4. 更好的性能:通过降低阻塞和等待时间，3PC通常能提供比2PC更好的性能。

缺点：<br />
1. 复杂性: 3PC比2PC更复杂，对网络通信和协调逻辑都有更高的要求，这增加了实现和维护的难度。
2. 网络开销: 由于增加了额外的阶段，3PC需要更多的消息交换，这可能导致更大的网络开销和延迟。
3. 数据一致性风险: 尽管3PC减少了协调者单点故障的风险，但在某些极端场景下，如果网络分区或其他通信问题发生在关键时刻，仍然可能导致数据不一致。

### TCC
即 Try-Confirm-Cancel，TCC是应用层的2PC(2 Phase Commit, 两阶段提交)，如果你将应用看做资源管理器的话。一般来说需要业务系统实现try、confirm 和 cancel 三个接口。
和2PC的主要区别：
1. 同步性:
2PC是一种阻塞式协议，参与者在等待最终的确认或回滚指令时被锁定。
TCC提供了更大的灵活性，因为它通常不需要长时间的锁定资源，而是通过补偿逻辑来恢复状态。
2. 一致性保证:
2PC提供强一致性保证，它确保所有操作要么全部成功，要么全部失败。
TCC倾向于最终一致性，Cancel阶段可能在失败后的任何时间执行，这可能导致短暂的不一致状态。
3. 性能与资源占用:
2PC在事务期间需要锁住资源，可能导致资源在等待期间无法被其他事务使用，影响系统性能。
TCC允许资源较早释放，并通过异步补偿操作来处理失败，通常对系统性能的影响较小。

**应用场景**：
2PC适用于对一致性要求较高的短事务，例如数据库操作。
TCC更适合长事务处理和对业务逻辑侵入性较高的场景，例如跨服务的业务流程。

### Saga
Saga 是一种补偿协议，在 Saga 模式下，分布式事务内有多个参与者，每一个参与者都是一个冲正补偿服务，需要用户根据业务场景实现其正向操作和逆向回滚操作。
分布式事务执行过程中，依次执行各参与者的正向操作，如果所有正向操作均执行成功，那么分布式事务提交。如果任何一个正向操作执行失败，那么分布式事务会退回去执行前面各参与者的逆向回滚操作，回滚已提交的参与者，使分布式事务回到初始状态。
Saga 理论出自 Hector & Kenneth 1987发表的论文 Sagas。 Saga 正向服务与补偿服务也需要业务开发者实现。

### Paxos
Paxos算法是莱斯利·兰伯特(Leslie Lamport)1990年提出的一种基于消息传递的一致性算法，其解决的问题是分布式系统如何就某个值(决议)达成一致。

### Raft
不同于Paxos算法直接从分布式一致性问题出发推导出来，Raft算法则是从多副本状态机的角度提出，用于管理多副本状态机的日志复制。Raft实现了和Paxos相同的功能，它将一致性分解为多个子问题：
Leader选举（Leader election）、日志同步（Log replication）、安全性（Safety）、日志压缩（Log compaction）、成员变更（Membership change）等。
同时，Raft算法使用了更强的假设来减少了需要考虑的状态，使之变的易于理解和实现。

Raft将系统中的角色分为领导者（Leader）、跟从者（Follower）和候选人（Candidate）：
* Leader：接受客户端请求，并向Follower同步请求日志，当日志同步到大多数节点上后告诉Follower提交日志。
* Follower：接受并持久化Leader同步的日志，在Leader告之日志可以提交之后，提交日志。
* Candidate：Leader选举过程中的临时角色。

![Raft算法角色转换](https://user-images.githubusercontent.com/6687462/159512756-7d9a279f-7dfb-4dfb-8f04-889a365410f6.jpg)
1. 所有节点启动时都是follower状态，在一段时间如果没有收到来自leader的心跳，follower切换为candidate,并发起选举。
2. 如果收到了超半数的选举票（包含自己的一票），那么切换为 leader 状态。
3. 如果发现其他节点比自己更加新，则主动切换为follower。

#### 选举过程
follower 在 timeout 时间内，没有收到来自 leader 的心跳，则会发起选举：<br />
1. 增加节点本地的 current term, 切换为 candidate 状态<br />
2. 投自己一票<br />
3. 并行的发送给其他节点 RequestVotes RPCs<br />
4. 等待其他节点的回复：<br />
   a. 收到了 大多数选票（majority )，那么赢得选举，切换状态为 leader<br />
   b. 被告知别人已经当选，则切换为 follower<br />
   c. 一段时间还是没有收到 majority 的投票结果，保持 candidate 状态，重新发出选举。<br />
每个任期，一个节点只能投票一次，候选人知道的信息不能比自己少，fisrtcome- first-serverd 先到先得。

系统中只会存在一个leader, 如果一段时间内没有 leader, 那么大家通过选举的方式选出 leader. leader 不停的向 follower 发出心跳，表明leader的存活状态，如果leader故障，follower会切换成candidate选举出新leader。

#### 如何防止脑裂
1. 一个节点某一任期内最多只能投一票；
2. 只有获得大多数选票才能成为领导人；

#### 如果候选者每次都先投给自己，再请求别的候选者投票给自己，而且每个候选人每个任期都只能投一票，那都投给自己了，还选举啥？
在Raft算法中，一个节点在成为候选者时确实会首先给自己投一票，但关键是不是所有节点同时都变成候选者。在一般情况下，只有当一个节点认为当前的领导者已经失效（丢失心跳信息）时，它才会启动选举过程，并成为候选者。
这里是一个简化的选举过程：
1. **触发选举**:
    - 一个节点（称为候选者）在一段时间内没有收到领导者的心跳信息后，会认为领导者已失效，并触发新一轮的选举。
2. **自我投票和请求选票**:
    - 候选者首先递增当前任期号（term），然后给自己投票，并向其他节点发送请求投票的消息（RequestVote RPCs）。
3. **其他节点响应**:
    - 收到请求的其他节点会根据自己是否已经在当前任期投过票，以及候选者的日志是否至少和自己的日志一样新，来决定是否投票给该候选者。
    - 如果其他节点已经在当前任期投票给了另一个候选者，或者它们认为候选者的日志不够新，它们将拒绝投票给该候选者。
4. **计算选票**:
    - 如果候选者获得了大多数节点的投票（超过半数），它就成为新的领导者。
    - 如果没有候选者赢得了大多数票，选举失败，可能触发新一轮的选举。

节点不会在没有足够理由的情况下成为候选者；通常是领导者失效或者选举超时导致某个节点发起选举。这意味着，并不是所有节点都会在同一个时刻变成候选者并给自己投票。实际上，节点在收到更高任期号的候选者请求投票时，如果它在当前任期还未投票，则可能投票给那个候选者，而不是自己。
如果多个节点同时触发选举过程，这可能导致选票分散，没有一个候选者能获得多数票。在这种情况下，选举会失败，节点可能会在随机的超时后再次尝试选举。Raft算法通过随机选举超时来减少这种同时选举的可能性，使得通常情况下只有一个节点会率先超时并开始选举。


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

### ZooKeeper集群架构
ZooKeeper 集群中包含 Leader、Follower 以及 Observer 三个角色：
* Leader：负责进行投票的发起和决议，更新系统状态，Leader 是由选举产生;
* Follower： 用于接受客户端请求并向客户端返回结果，在选主过程中参与投票;
* Observer：可以接受客户端连接，接受读写请求，写请求转发给 Leader，但 Observer 不参加投票过程，只同步 Leader 的状态，Observer 的目的是为了扩展系统，提高读取速度。

### ZooKeeper节点类型
ZooKeeper3.6.2后的版本支持7种节点类型分别是：持久、持久顺序、临时、临时顺序、容器、持久 TTL、持久顺序 TTL（之前是四种）。
* 持久、临时：持久不用我多说，是用的最多的一种类型，也是默认的节点类型，临时节点相较于持久节点来说，就是它会随着客户端会话结束而被删除，通常可以用在一些特定的场景，例如分布式锁释放，健康检查等。
* 持久顺序、临时顺序：这两种我放在一起介绍，因为他们相对于上面两种的特性就是 ZK 会自动在这两种节点之后增加一个数字的后缀，而路径 + 数字后缀是能保证唯一的，这数字后缀的应用场景可以实现诸如分布式队列，分布式公平锁等。
* 容器：容器节点是 3.5 以后新增的节点类型，只要在调用create方法时，指定CreateMode 为CONTAINER 即可创建容器的节点类型，容器节点的表现形式和持久节点是一样的，但是区别是 ZK 服务端启动后，会有一个单独的线程去扫描，所有的容器节点，当发现容器节点的子节点数量为0时，会自动删除该节点，除此之外和持久节点没有区别，官方注释给出的使用场景是Container nodes are special purpose nodes useful for recipes such as leader, lock, etc. 说可以用在 leader 或者锁的场景中。
* 持久TTL、持久顺序TTL：关于持久和顺序这两个关键字，不用我再解释了，这两种类型的节点重点是后面的TTL，TTL 是time to live 的缩写，指带有存活时间，简单来说就是当该节点下面没有子节点的话，超过了TTL 指定时间后就会被自动删除，特性跟上面的容器节点很像，只是容器节点没有超时时间而已，但是TTL 启用是需要额外的配置（这个之前也有提过）配置是zookeeper.extendedTypesEnabled 需要配置成true，否则的话创建TTL 时会收到Unimplemented 的报错

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

#### 通信协议
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

### Thrift

### 序列化协议性能对比
![序列化协议性能对比](https://user-images.githubusercontent.com/6687462/166863103-95b8c94c-14ba-4874-b186-3336846af801.png)

![序列化协议空间对比](https://user-images.githubusercontent.com/6687462/166863107-9def934c-032a-4edb-9d7f-766f4e8d8259.png)

**参考资料**<br />
* https://tech.meituan.com/2015/02/26/serialization-vs-deserialization.html

## MQ

### RocketMQ
#### 事务消息
<img width="866" alt="RocketMQ事务消息" src="https://user-images.githubusercontent.com/6687462/162554192-4c1cd170-17b3-4796-8845-04e43956e8aa.png">

### Kafka
Kafka被设计为能够作为一个统一平台来处理大量或实时数据的投递和消费，为此Kafka需要有如下特性：
* 高吞吐：它必须具有高吞吐量才能支持大容量事件流，例如实时日志聚合。
* 扛积压：它需要优雅地处理大量数据积压，以便能够支持来自离线系统的定期数据加载。
* 低延迟：这也意味着系统必须处理低延迟交付以处理更传统的消息传递用例。

#### Topic和分区
从Kafka的底层实现来说，主题和分区都是逻辑上的概念，分区可以有一至多个副本，每个副本对应一个日志文件，每个日志文件对应一至多个日志分段（LogSegment），每个日志分段还可以细分为索引文件、日志存储文件和快照文件等。

如果broker端配置参数auto.create.topics.enable设置为true（默认值就是true），那么当生产者向一个尚未创建的主题发送消息时，会自动创建一个分区数为num.partitions （默认值为1）、副本因子为default.replication.factor（默认值为1）的主题。
除此之外，当一个消费者开始从未知主题中读取消息时，或者当任意一个客户端向未知主题发送元数据请求时，都会按照配置参数num.partitions和default.replication.factor的值来创建一个相应的主题。

生产者的分区分配是指为每条消息指定其所要发往的分区，消费者中的分区分配是指为消费者指定其可以消费消息的分区。每条消息在发送的时候会根据分区规则被追加到指定的分区中，分区中的每条消息都会被分配一个唯一的序列号，也就是通常所说的偏移量（offset）。

**Topic创建**：在创建主题时，如果使用了replica-assignment参数，那么就按照指定的方案来进行分区副本的创建；如果没有使用replica-assignment参数，那么就需要按照内部的逻辑来计算分配方案了。使用kafka-topics.sh脚本创建主题时的内部分配逻辑按照机架信息划分成两种策略：未指定机架信息和指定机架信息。

**分区的本质**：如果分区规则设置得合理，那么所有的消息可以均匀地分布到不同的分区中，这样就可以实现水平扩展。不考虑多副本的情况，一个分区对应一个日志（Log）。为了防止 Log 过大，Kafka又引入了日志分段（LogSegment）的概念，将Log切分为多个LogSegment，相当于一个巨型文件被平均分配为多个相对较小的文件，这样也便于消息的维护和清理。事实上，Log 和LogSegment 也不是纯粹物理意义上的概念，Log 在物理上只以文件夹的形式存储，而每个LogSegment 对应于磁盘上的一个日志文件和两个索引文件，以及可能的其他文件（比如以“.txnindex”为后缀的事务索引文件）。

**Leader分区**：分区使用多副本机制来提升可靠性，但只有leader副本对外提供读写服务，而follower副本只负责在内部进行消息的同步。如果一个分区的leader副本不可用，那么就意味着整个分区变得不可用，此时就需要Kafka从剩余的follower副本中挑选一个新的leader副本来继续对外提供服务。

**Broker分区限制**：针对同一个分区而言，同一个broker节点中不可能出现它的多个副本，即Kafka集群的一个broker中最多只能有它的一个副本。

**Broker宕机**：当集群中的一个节点突然宕机下线时，如果节点上的分区是单副本的，那么这些分区就变得不可用了，在节点恢复前，相应的数据也就处于丢失状态；如果节点上的分区是多副本的，那么位于这个节点上的leader副本的角色会转交到集群的其他follower副本中。总而言之，这个节点上的分区副本都已经处于功能失效的状态，Kafka 并不会将这些失效的分区副本自动地迁移到集群中剩余的可用broker节点上，如果放任不管，则不仅会影响整个集群的均衡负载，还会影响整体服务的可用性和可靠性。

**新增Broker**：当集群中新增broker节点时，只有新创建的主题分区才有可能被分配到这个节点上，而之前的主题分区并不会自动分配到新加入的节点中，因为在它们被创建时还没有这个新节点，这样新节点的负载和原先节点的负载之间严重不均衡。为了解决上述问题，需要让分区副本再次进行合理的分配，也就是所谓的分区重分配。Kafka提供了 kafka-reassign-partitions.sh 脚本来执行分区重分配的工作，它可以在集群扩容、broker节点失效的场景下对分区进行迁移。

**分区复制**：分区重分配本质在于数据复制，先增加新的副本，然后进行数据同步，最后删除旧的副本来达到最终的目的，如果重分配的量太大必然会严重影响整体的性能，尤其是处于业务高峰期的时候。减小重分配的粒度，以小批次的方式来操作是一种可行的解决思路。如果集群中某个主题或某个分区的流量在某段时间内特别大，那么只靠减小粒度是不足以应对的，这时就需要有一个限流的机制，可以对副本间的复制流量加以限制来保证重分配期间整体服务不会受太大的影响。副本间的复制限流有两种实现方式：kafka-config.sh脚本和kafka-reassign-partitions.sh脚本。

**如何选择合适的分区数**：分区是Kafka 中最小的并行操作单元，对生产者而言，每一个分区的数据写入是完全可以并行化的；对消费者而言，Kafka 只允许单个分区中的消息被一个消费者线程消费，一个消费组的消费并行度完全依赖于所消费的分区数。
消息中间件的性能一般是指吞吐量（广义来说还包括延迟）。抛开硬件资源的影响，消息写入的吞吐量还会受到消息大小、消息压缩方式、消息发送方式（同步/异步）、消息确认类型（acks）、副本因子等参数的影响，消息消费的吞吐量还会受到应用逻辑处理速度的影响。

**分区的结构**：一个分区对应一个日志（Log）。为了防止 Log 过大，Kafka又引入了日志分段（LogSegment）的概念，将Log切分为多个LogSegment，相当于一个巨型文件被平均分配为多个相对较小的文件，这样也便于消息的维护和清理。
事实上，Log 和LogSegment 也不是纯粹物理意义上的概念，Log 在物理上只以文件夹的形式存储，而每个LogSegment 对应于磁盘上的一个日志文件和两个索引文件，以及可能的其他文件（比如以“.txnindex”为后缀的事务索引文件）。
向Log 中追加消息时是顺序写入的，只有最后一个 LogSegment 才能执行写入操作，在此之前所有的 LogSegment 都不能写入数据。
为了便于消息的检索，每个LogSegment中的日志文件（以“.log”为文件后缀）都有对应的两个索引文件：偏移量索引文件（以“.index”为文件后缀）和时间戳索引文件（以“.timeindex”为文件后缀）。每个 LogSegment 都有一个基准偏移量baseOffset，用来表示当前 LogSegment中第一条消息的offset。偏移量是一个64位的长整型数，日志文件和两个索引文件都是根据基准偏移量（baseOffset）命名的，名称固定为20位数字，没有达到的位数则用0填充。比如第一个LogSegment的基准偏移量为0，对应的日志文件为00000000000000000000.log。

**消息生产者**：发送消息主要有三种模式：发后即忘（fire-and-forget）、同步（sync）及异步（async）。KafkaProducer中一般会发生两种类型的异常：可重试的异常和不可重试的异常。

**消费进度**：从kafka-0.9版本及以后，kafka的消费者组和offset信息就不存zookeeper了，而是存到broker服务器上，所以，如果你为某个消费者指定了一个消费者组名称（group.id），那么，一旦这个消费者启动，这个消费者组名和它要消费的那个topic的offset信息就会被记录在broker服务器上。
Kafka版本[0.10.1.1]，已默认将消费的 offset 迁入到了 Kafka 一个名为 __consumer_offsets 的Topic中。利用 Kafka 自身的 Topic，以消费的Group，Topic，以及Partition做为组合 Key。所有的消费offset都提交写入到上述的Topic中。因为这部分消息是非常重要，以至于是不能容忍丢数据的，所以消息的 acking 级别设置为了 -1，生产者等到所有的 ISR 都收到消息后才会得到 ack（数据安全性极好，当然，其速度会有所影响）。
所以 Kafka 又在内存中维护了一个关于 Group，Topic 和 Partition 的三元组来维护最新的 offset 信息，消费者获取最新的offset的时候会直接从内存中获取。

**参考资料**
* 《深入理解Kafka:核心设计与实践原理》

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

# 分布式追踪系统
Distributed Tracing
## OpenTelemetry
OpenTelemetry is an Observability framework and toolkit designed to create and manage telemetry data such as traces, metrics, and logs. Crucially, OpenTelemetry is vendor- and tool-agnostic, meaning that it can be used with a broad variety of Observability backends, including open source tools like Jaeger and Prometheus, as well as commercial offerings. OpenTelemetry is a Cloud Native Computing Foundation (CNCF) project.

OpenTelemetry, also known as OTel for short, is a vendor-neutral open source Observability framework for instrumenting, generating, collecting, and exporting telemetry data such as traces, metrics, logs.

OpenTelemetry 是两个先前项目OpenTracing和OpenCensus合并的结果 。这两个项目都是为了解决同一个问题而创建的：缺乏如何检测代码并将遥测数据发送到可观察性后端的标准。然而，这两个项目都无法完全独立解决问题，因此这两个项目合并形成了 OpenTelemetry，这样它们就可以结合各自的优势并真正提供单一标准。

### OpenTelemetry vs SkyWalking
Apache SkyWalking 和 OpenTelemetry 是两个不同的开源项目，它们在应用程序性能监控（APM）和可观测性领域发挥作用，但它们的设计目标和使用方式有所区别。下面列出了它们之间的一些主要差异：<br />
**Apache SkyWalking:**<br />
SkyWalking 是一个完整的应用性能监控（APM）解决方案。它提供了端到端的服务追踪、服务性能分析、仪表盘展示等功能。
它专注于对分布式系统的监控和诊断，尤其是在云原生架构（如微服务、容器、服务网格）中。
SkyWalking 本身包含数据收集、存储、分析和可视化的全部组件。
它提供了自己的一套代理和SDK来收集追踪和度量数据。
虽然 SkyWalking 支持 OpenTracing 与 OpenCensus 数据模型，也在逐步支持 OpenTelemetry，但它是一个独立完整的系统。

**OpenTelemetry:**<br />
OpenTelemetry 是一个遥测数据收集框架，它是由 OpenTracing 和 OpenCensus 两个项目合并而来。
作为一个框架，它为开发者提供了 API、SDK 以及一些工具，用于收集和传输应用程序和系统的追踪、指标和日志数据。
OpenTelemetry 关注于标准化遥测数据的收集和传输方式，并且旨在成为行业标准。
它不包含数据分析和可视化功能，但是可以将收集的数据发送到各种后端系统（如 Prometheus、Jaeger、Zipkin、Elasticsearch 等），这些系统可以对数据进行存储、分析和展示。
OpenTelemetry 提供了一个多语言的生态系统，支持广泛的编程语言和框架。
简而言之，SkyWalking 是一个完整的 APM 系统，提供了从数据收集到分析和可视化的一整套功能，而 OpenTelemetry 主要关注于作为一个通用的和可扩展的遥测数据收集框架，它可以将数据发送到各种兼容的后端处理系统。用户可以选择 OpenTelemetry 来标准化遥测数据的收集工作，并同时使用 SkyWalking 来进行数据的分析和可视化。


### 关键术语
* OTLP: The OpenTelemetry Protocol (OTLP) specification describes the encoding, transport, and delivery mechanism of telemetry data between telemetry sources, intermediate nodes such as collectors and telemetry backends.

### 参考资料
* https://opentelemetry.io/docs/what-is-opentelemetry/  what-is-opentelemetry
* https://opentelemetry.io/docs/specs/otel/protocol/  OTLP
* https://opentelemetry.io/docs/instrumentation/java/  A language-specific implementation of OpenTelemetry in Java.
* https://opentelemetry.io/docs/collector/deployment/agent/ Why and how to send signals to collectors and from there to backends





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
org.springframework.beans和org.springframework.context包是Spring框架的IoC容器的基础。<br />
* 控制 ：指的是对象创建（实例化、管理）的权力
* 反转 ：控制权交给外部环境（Spring 框架、IoC 容器）

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

### Spring AOP和AspectJ AOP
Spring AOP 属于运行时增强，而 AspectJ 是编译时增强。 Spring AOP 基于代理(Proxying)，而 AspectJ 基于字节码操作(Bytecode Manipulation)。 Spring AOP 已经集成了 AspectJ ，AspectJ 应该算的上是 Java 生态系统中最完整的 AOP 框架了。AspectJ 相比于 Spring AOP 功能更加强大，但是 Spring AOP 相对来说更简单，如果我们的切面比较少，那么两者性能差异不大。但是，当切面太多的话，最好选择 AspectJ ，它比 Spring AOP 快很多。

### Bean的作用域
* singleton : 唯一 bean 实例，Spring 中的 bean 默认都是单例的，对单例设计模式的应用。
* prototype : 每次请求都会创建一个新的 bean 实例。
* request : 每一次 HTTP 请求都会产生一个新的 bean，该 bean 仅在当前 HTTP request 内有效。
* session : 每一次来自新 session 的 HTTP 请求都会产生一个新的 bean，该 bean 仅在当前 HTTP session 内有效。
* global-session ： 全局 session 作用域，仅仅在基于 portlet 的 web 应用中才有意义，Spring5 已经没有了。Portlet 是能够生成语义代码(例如：HTML)片段的小型 Java Web 插件。它们基于 portlet 容器，可以像 servlet 一样处理 HTTP 请求。但是，与 servlet 不同，每个 portlet 都有不同的会话。

### Bean的生命周期
1. Bean 容器找到配置文件中 Spring Bean 的定义。
2. Bean 容器利用 Java Reflection API 创建一个 Bean 的实例。
3. 如果涉及到一些属性值 利用 set()方法设置一些属性值。
4. 如果 Bean 实现了 BeanNameAware 接口，调用 setBeanName()方法，传入 Bean 的名字。
5. 如果 Bean 实现了 BeanClassLoaderAware 接口，调用 setBeanClassLoader()方法，传入 ClassLoader对象的实例。
6. 如果 Bean 实现了 BeanFactoryAware 接口，调用 setBeanFactory()方法，传入 BeanFactory对象的实例。
7. 与上面的类似，如果实现了其他 *.Aware接口，就调用相应的方法。
8. 如果有和加载这个 Bean 的 Spring 容器相关的 BeanPostProcessor 对象，执行postProcessBeforeInitialization() 方法
9. 如果 Bean 实现了InitializingBean接口，执行afterPropertiesSet()方法。
10. 如果 Bean 在配置文件中的定义包含 init-method 属性，执行指定的方法。
11. 如果有和加载这个 Bean 的 Spring 容器相关的 BeanPostProcessor 对象，执行postProcessAfterInitialization() 方法
12. 当要销毁 Bean 的时候，如果 Bean 实现了 DisposableBean 接口，执行 destroy() 方法。
13. 当要销毁 Bean 的时候，如果 Bean 在配置文件中的定义包含 destroy-method 属性，执行指定的方法。

### Spring中用到了哪些设计模式
* 工厂设计模式 : Spring 使用工厂模式通过 BeanFactory、ApplicationContext 创建 bean 对象。
* 代理设计模式 : Spring AOP 功能的实现。
* 单例设计模式 : Spring 中的 Bean 默认都是单例的。
* 模板方法模式 : Spring 中 JdbcTemplate、RestTemplate 等以 Template 结尾的对数据库操作的类，它们就使用到了模板模式。
* 包装器设计模式 : 我们的项目需要连接多个数据库，而且不同的客户在每次访问中根据需要会去访问不同的数据库。这种模式让我们可以根据客户的需求能够动态切换不同的数据源。
* 观察者模式: Spring 事件驱动模型就是观察者模式很经典的一个应用。
* 适配器模式 : Spring AOP 的增强或通知(Advice)使用到了适配器模式、Spring MVC 中也是用到了适配器模式适配Controller。

### Spring的Environment
Environment接口是集成在容器中的抽象，它对应用程序环境的两个关键方面进行建模：配置文件 和属性。

### Spring MVC
SpringMVC流程
1. 用户发送请求至前端控制器DispatcherServlet。
2. DispatcherServlet收到请求调用HandlerMapping处理器映射器。
3. 处理器映射器找到具体的处理器(可以根据xml配置、注解进行查找)，生成处理器对象及处理器拦截器(如果有则生成)一并返回给DispatcherServlet。
4. DispatcherServlet调用HandlerAdapter处理器适配器。
5. HandlerAdapter经过适配调用具体的处理器(Controller，也叫后端控制器)。
6. Controller执行完成返回ModelAndView。
7. HandlerAdapter将controller执行结果ModelAndView返回给DispatcherServlet。
8. DispatcherServlet将ModelAndView传给ViewReslover视图解析器。
9. ViewReslover解析后返回具体View。
10. DispatcherServlet根据View进行渲染视图（即将模型数据填充至视图中）。
11. DispatcherServlet响应用户。

**参考资料**<br />
* https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-environment
* https://github.com/Snailclimb/JavaGuide/blob/main/docs/system-design/framework/spring/spring-knowledge-and-questions-summary.md

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

## 类加载
类加载的主要步骤
* 装载：根据查找路径找到相应的class文件，然后导入。
* 链接：链接又可分为3个小步：<br />
（1）检查：检查待加载的class文件的正确性。<br />
（2）准备：给类中的静态变量分配存储空间。<br />
（3）解析：将符号引用转换为直接引用（这一步可选）<br />
* 初始化：对静态变量和静态代码块执行初始化工作。

类装载的方式，有两种：
* 隐式装载，程序在运行过程中当碰到通过new等方式生成对象时，隐式调用类装载器对应的类到jvm中
* 显示装载，通过Class.forName()等方式，显示加载需要的类

## 类加载器
实现通过类的全限定名获取该类的二进制字节流的代码块叫做类加载器，它把类的.class文件的数据读入到内存中，通常是创建一个字节数组读入.class文件，然后产生与所加载类对应的class对象，加载完成后，Class对象还不完整，所以此时的类还不可用。

主要有以下四种类加载器：
1. **启动类加载器**（Bootstrap ClassLoader）：使用C/C++语言实现，嵌套在JVM内部。用来加载Java核心类库。 并不继承于java.lang.ClassLoader没有父加载器。
2. **扩展类加载器**（Extensions ClassLoader）：用来加载java的扩展库。java虚拟机的实现会提供一个扩展库目录。该类加载器在此目录里面查找并加载java类，它的父类加载器是Bootrap。
3. **系统类加载器**（System ClassLoader）：根据java应用的类路径（CLASSPATH）来加载java类。一般来说，java应用的类都是由它来完成加载的。可以通过ClassLoader.getSystemLoader()来获取它，它是应用最广泛的类加载器。。
4. **用户自定义类加载器**：通过继承java.lang.ClassLoader类的方式实现。

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

## JVM对象结构
HotSpot虚拟机中，对象在内存中存储的布局可以分为三块区域：**对象头**（Header）、**实例数据**（Instance Data）和**对齐填充**（Padding）
* MarkWord:用于存储对象自身的运行时数据，如哈希码（HashCode）、GC分代年龄、锁状态标志、线程持有的锁、偏向线程ID、偏向时间戳等等，这部分数据的长度在32位和64位的虚拟机（暂 不考虑开启压缩指针的场景）中分别为32个和64个Bits，官方称它为“Mark Word”。
* KlassWord，即类型指针，即是对象指向它的类的元数据的指针，虚拟机通过这个指针来确定这个对象是哪个类的实例。并不是所有的虚拟机实现都必须在对象数据上保留类型指针，换句话说查找对象的元数据信息并不一定要经过对象本身。另外，如果对象是一个Java数组，那在对象头中还必须有一块用于记录数组长度的数据，因为虚拟机可以通过普通Java对象的元数据信息确定Java对象的大小，但是从数组的元数据中无法确定数组的大小。
![Java对象内存结构](https://user-images.githubusercontent.com/6687462/163525387-3109920c-71d1-4da9-ac89-f95f6e8492da.png)

## 垃圾收集算法
主要是标记-清除、标记-复制和标记-整理三种。<br />
**标记-清除** 该算法有两个缺点，一个是效率不稳定，如果大量对象都需要标记和清除的话，开销会比较大，另一个是会导致碎片化严重，导致给新对象分配内存空间时需要进行碎片整理，增加了运行时内存分配的成本。<br />
**标记-复制** 如果每次只有少量对象存活（例如新生代内的对象就是如此），那么只需要保留（复制）这少量对象就行了，所以有人提出了该算法，“半区复制”（Semispace Copying）的垃圾收集算法，它将可用内存按容量划分为大小相等的两块，每次只使用其中的一块。当这一块的内存用完了，就将还存活着的对象复制到另外一块上面，然后再把已使用过的内存空间一次清理掉。<br />
**标记-整理** 如果每次都会有大量对象存活（例如老年代），那么标记-复制算法需要复制的对象数量将很多，标记过程仍然与“标记-清除”算法一样，但后续步骤不是直接对可回收对象进行清理，而是让所有存活的对象都向内存空间一端移动，然后直接清理掉边界以外的内存。

## 方法区、永久代、元数据区的关系
方法区是JVM定义的一种规范，是所有虚拟机都需要遵守的约定，而“永久代（PermGen space）”和“元数据（MetaSpace）”都是实际某个虚拟机针对“方法区”的一种实现，“永久代”是的JDK1.7之前Hotspot虚拟机对方法区的实现，而“元数据”则是1.8之后Hotspot虚拟机针对方法区的一种实现而已。
不管是PermGen space 还是 MetaSpace 他们都是Hotspot针对方法区的一种实现，两者最大的区别在于PermGen space是在JVM虚拟机中分配内存的，而Metaspace则是在虚拟机之外的系统本地分配内存。因为很多类是在运行期间加载的，这部分类加载的空间不可控，如果这部分内存是在JVM内存里分配的话，永久代分配太大那么JVM其他区域（比如说堆）的内存就会变小，反之如果设置太小，就容易出现方法区内存溢出，因为本身存储的类信息属于不确定大小，类信息在我们运行的时候可以动态加载。所以jdk1.8中选择把Metaspace内存分配在本地内存，如果这样做的好处是]Metaspace空间的大小不会受限于虚拟机分配的内存大小，只会受限于机器内存，可分配的内存大了那么就不会那么容易出现内存溢。因为很多类是在运行期间加载的，这部分类加载的空间不可控，如果这部分内存是在JVM内存里分配的话，永久代分配太大那么JVM其他区域（比如说堆）的内存就会变小，反之如果设置太小，就容易出现方法区内存溢出，因为本身存储的类信息属于不确定大小，类信息在我们运行的时候可以动态加载。所以jdk1.8中选择把Metaspace内存分配在本地内存，如果这样做的好处是]Metaspace空间的大小不会受限于虚拟机分配的内存大小，只会受限于机器内存，可分配的内存大了那么就不会那么容易出现内存溢。

## 字符串常量、静态变量数据存放区域
JDK6中所有常量池数据是存放在永久代中，但到JDK7后 Hostpot 把永久代中的字符串常量、静态变量数据迁移到了堆中，后面的java 8并没有对这部分内容进行迁移，在JDK8中字符串常量、静态变量数据还是放到堆中，所以常量池只是在JVM规范定义上属于方法区，但Hotspot在实现的时候部分常量池的内容实际上是保存在堆中了。

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
G1垃圾收集器的垃圾收集过程可以分为几个阶段：<br />
1. 初始标记（Initial Marking）：这个阶段标志着垃圾收集周期的开始。初始标记阶段与一个正在进行的年轻代收集（Young GC）同步执行，并且需要一个较短的停顿时间。在这一阶段，G1标记了从根集合（例如活跃的线程、静态变量等）直接可达的对象。初始标记也负责识别任何被年轻代中的对象引用的老年代对象，这些被称为“GC Roots”。
2. 根区域扫描（Root Region Scanning）：在这个阶段，G1垃圾收集器扫描老年代中的那些在初始标记阶段发现的根区域。此阶段在应用线程运行的同时进行，并且在下一次年轻代收集之前必须完成。
3. 并发标记（Concurrent Marking）：这是一个并发阶段，G1在整个堆中标记存活的对象。这个过程是在应用程序线程继续运行的同时完成的，因此不需要停止应用程序的执行。这个阶段可能会经历多轮更新，以保持标记状态与应用程序的变化一致。
4. 最终标记（Final Marking）：这个阶段在并发标记完成后发生，并且需要短暂的停顿。在最终标记阶段，G1处理剩余的标记任务，这包括处理在并发标记阶段由于程序继续运行而出现变化的那部分数据。
5. 筛选回收（Evacuation）：在此阶段，G1将选择一些区域进行清理。这些区域包括年轻代区域以及可能的一些老年代区域。G1会将存活的对象从这些即将被清理的区域复制到空闲的区域中。筛选回收阶段通常包含在“混合收集（Mixed GC）”中，不仅处理年轻代，还包括老年代的一部分。这也是一个需要停顿的阶段，G1会尽量限制停顿时间以满足用户设置的性能目标。
上述阶段中，初始标记、最终标记和筛选回收需要停顿应用线程（Stop-the-World）。G1垃圾收集器的目标是通过限制这些停顿的时间和频率，来提供尽可能平滑的性能表现。

G1（Garbage-First）垃圾收集器也分为年轻代（Young Generation）和老年代（Old Generation）。G1垃圾收集器是一个服务器端的垃圾收集器，用于处理大量内存和多核CPU的系统，旨在达到高吞吐量和低延迟。
与其他垃圾收集器（如Parallel GC或CMS）相比，G1有一些不同之处：
1. 区域化堆内存（Region-based heap）：G1将Java堆划分为多个大小相等的区域（Region），每个区域可以充当年轻代或老年代的一部分。这种划分使得G1能够更灵活地管理内存，减少整体的垃圾收集开销。
2. 增量收集（Incremental collection）：G1可以逐步完成垃圾收集任务，选择一部分区域进行收集。这可以控制停顿时间（Stop-the-World pauses），使得G1在保持良好吞吐量的同时还能提供可预期的低延迟。
3. 混合收集（Mixed collections）：G1的收集周期中包括只针对年轻代的收集（Young GC），以及同时包括年轻代和一部分老年代的混合收集。通过这种方式，G1可以在维持低停顿时间的目标下逐步清理老年代空间，避免长时间的全堆收集。
4. 可预测的停顿时间模型（Predictable pause time model）：G1的设计目标之一是让用户可以指定停顿时间目标（例如，停顿不超过50毫秒），然后G1会尽量在这个目标内完成垃圾收集。

在使用G1收集器时，Java堆虽然在逻辑上被划分为年轻代和老年代，但物理上并非连续的内存块。年轻代通常由多个区域组成，这些区域通常是连续分配的，以便优化年轻代的垃圾收集。老年代则由那些不再被年轻代使用的区域组成，这些区域可能在堆内存中分布较为分散。


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

1. 保证可见性，volatile只能保证对单次读/写的原子性，因为long和double两种数据类型的操作可分为高32位和低32位两部分，因此普通的long或double类型读/写可能不是原子的。因此，鼓励大家将共享的long和double变量设置为volatile类型，这样能保证任何情况下对long和double的单次读/写操作都具有原子性。
* 修改volatile变量时会强制将修改后的值刷新的主内存中。
* 修改volatile变量后会导致其他线程工作内存中对应的变量值失效。因此，再读取该变量值的时候就需要重新从读取主内存中的值。

2. 禁止指令重排
   JSR 133中定义了哪些happen-before规则
* 同一个线程中的，前面的操作 happen-before 后续的操作。（即单线程内按代码顺序执行。但是，在不影响在单线程环境执行结果的前提下，编译器和处理器可以进行重排序，这是合法的。换句话说，这一是规则无法保证编译重排和指令重排）。
* 监视器上的解锁操作 happen-before 其后续的加锁操作。（Synchronized 规则）
* 对volatile变量的写操作 happen-before 后续的读操作。（volatile 规则）
* 线程的start() 方法 happen-before 该线程所有的后续操作。（线程启动规则）
* 线程所有的操作 happen-before 其他线程在该线程上调用 join 返回成功后的操作。
* 如果 a happen-before b，b happen-before c，则a happen-before c（传递性）。

为了实现volatile可见性和happen-before的语义。JVM底层是通过一个叫做“**内存屏障**”的东西来完成。内存屏障，也叫做内存栅栏，是一组处理器指令，用于实现对内存操作的顺序限制。下面是完成上述规则所要求的内存屏障：

a. LoadLoad 屏障
执行顺序：Load1—>Loadload—>Load2
确保Load2及后续Load指令加载数据之前能访问到Load1加载的数据。

b. StoreStore 屏障
执行顺序：Store1—>StoreStore—>Store2
确保Store2以及后续Store指令执行前，Store1操作的数据对其它处理器可见。

c. LoadStore 屏障
执行顺序： Load1—>LoadStore—>Store2
确保Store2和后续Store指令执行前，可以访问到Load1加载的数据。

d. StoreLoad 屏障
执行顺序: Store1—> StoreLoad—>Load2
确保Load2和后续的Load指令读取之前，Store1的数据对其他处理器是可见的。

**synchronized（JDK6之前称之为重量级锁）**
JVM基于进入和退出Monitor对象来实现方法同步和代码块同步，但两者的实现细节不一样。代码块同步是使用monitorenter和monitorexit指令实现的，而方法同步是使用另外一种方式实现的，细节在JVM规范里并没有详细说明。但是，方法的同步同样可以使用这两个指令来实现。<br />
synchronized用的锁是存在Java对象头里的。如果对象是数组类型，则虚拟机用3个字宽（Word）存储对象头，如果对象是非数组类型，则用2字宽存储对象头。在32位虚拟机中，1字宽等于4字节，即32bit

synchronized关键字最主要有以下3种应用方式，下面分别介绍:
* 修饰实例方法，作用于当前实例加锁，进入同步代码前要获得当前实例的锁
* 修饰静态方法，作用于当前类对象加锁，进入同步代码前要获得当前类对象的锁
* 修饰代码块，指定加锁对象，对给定对象加锁，进入同步代码库前要获得给定对象的锁。

Java 虚拟机中的同步(Synchronization)基于进入和退出管程(Monitor)对象实现， 无论是显式同步(有明确的 monitorenter 和 monitorexit 指令,即同步代码块)还是隐式同步都是如此。
在 Java 语言中，同步用的最多的地方可能是被 synchronized 修饰的同步方法。同步方法 并不是由 monitorenter 和 monitorexit 指令来实现同步的，而是由方法调用指令读取运行时常量池中方法的 ACC_SYNCHRONIZED 标志来隐式实现的，关于这点，稍后详细分析。


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

JMM规定了所有的变量都存储在主内存（Main Memory）中。每个线程还有自己的工作内存（Working Memory）,线程的工作内存中保存了该线程使用到的变量的主内存的副本拷贝，线程对变量的所有操作（读取、赋值等）都必须在工作内存中进行，而不能直接读写主内存中的变量（volatile变量仍然有工作内存的拷贝，但是由于它特殊的操作顺序性规定，所以看起来如同直接在主内存中读写访问一般）。不同的线程之间也无法直接访问对方工作内存中的变量，线程之间值的传递都需要通过主内存来完成。
从抽象的角度来看，JMM定义了线程和主内存之间的抽象关系：线程之间的共享变量存储在主内存（main memory）中，每个线程都有一个私有的本地内存（local memory），本地内存中存储了该线程以读/写共享变量的副本。本地内存是JMM的一个抽象概念，并不真实存在。本地内存它涵盖了缓存，写缓冲区，寄存器以及其他的硬件和编译器优化之后的一个数据存放位置

JMM是围绕着并发编程中**原子性**、**可见性**、**有序性**这三个特征来建立的.

## Loom
Loom是Java语言中的一个新项目，旨在通过增强Java的并发性能和可扩展性来提高Java开发者的生产力。Loom的主要目标是为Java引入“协程”（Coroutine）的概念，将协程作为并发模型的一种选择，以取代Java语言中现有的线程和锁机制。
协程是一种轻量级的线程，它可以在一个或多个线程之间切换，但不需要线程上下文切换所需的开销。协程可以更好地利用CPU资源、减少内存占用和提高程序的性能。Loom的协程实现将基于Java的Fiber API，使用Java的协程可以像普通的方法调用一样简单，避免了线程和锁带来的复杂性和性能问题。
除了协程，Loom还引入了一些其他的新特性，如Virtual Threads、Continuations和Async IO等，以提高Java的并发性能和可扩展性，使Java更加适合处理高并发的任务。
总之，Loom是Java语言中的一个新项目，旨在通过增强Java的并发性能和可扩展性来提高Java开发者的生产力。Loom引入协程的概念，提高了Java的并发性能和可扩展性，同时还引入了其他的新特性，如Virtual Threads、Continuations和Async IO等，以更好地满足Java程序开发者的需求。
https://openjdk.org/projects/loom/

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

* select：时间复杂度O(n)，它仅仅知道有I/O事件发生了，却并不知道是哪几个流（可能有一个，多个，甚至全部），我们只能无差别轮询所有流，找出能读出数据，或者写入数据的流，对他们进行操作。所以select具有O(n)的无差别轮询复杂度，同时处理的流越多，无差别轮询时间就越长。但单个进程可监视的fd数量被限制，即能监听端口的大小有限。但大量的fd的数组被整体复制于用户态和内核地址空间之间，而不管这样的复制是不是有意义，poll还有一个特点是“水平触发”，如果报告了fd后，没有被处理，那么下次poll时会再次报告该fd。
* poll：时间复杂度O(n)，poll本质上和select没有区别，它将用户传入的数组拷贝到内核空间，然后查询每个fd对应的设备状态，但是它没有最大连接数的限制，原因是它是基于链表来存储的.
* epoll：时间复杂度O(1)，epoll可以理解为event poll，不同于忙轮询和无差别轮询，epoll会把哪个流发生了怎样的I/O事件通知我们。所以我们说epoll实际上是事件驱动（每个事件关联上fd）的，此时我们对这些流的操作都是有意义的。（复杂度降低到了O(1)）

**水平触发和边缘触发**<br />
* Level_triggered(水平触发)：当被监控的文件描述符上有可读写事件发生时，epoll_wait()会通知处理程序去读写。如果这次没有把数据一次性全部读写完(如读写缓冲区太小)，那么下次调用 epoll_wait()时，它还会通知你在上没读写完的文件描述符上继续读写，当然如果你一直不去读写，它会一直通知你！！！如果系统中有大量你不需要读写的就绪文件描述符，而它们每次都会返回，这样会大大降低处理程序检索自己关心的就绪文件描述符的效率！！！
* Edge_triggered(边缘触发)：当被监控的文件描述符上有可读写事件发生时，epoll_wait()会通知处理程序去读写。如果这次没有把数据全部读写完(如读写缓冲区太小)，那么下次调用epoll_wait()时，它不会通知你，也就是它只会通知你一次，直到该文件描述符上出现第二次可读写事件才会通知你！！！这种模式比水平触发效率高，系统不会充斥大量你不关心的就绪文件描述符！！！

select 和 poll 模型都是水平触发模式，信号驱动IO是边缘触发模式，epoll()模型即支持水平触发，也支持边缘触发，默认是水平触发。

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
零拷贝主要是用来解决操作系统在处理 I/O 操作时，频繁复制数据的问题。关于零拷贝主要技术有 mmap+write、sendfile和splice等几种方式。
无论是传统的I/O方式，还是引入了零拷贝之后，2次DMAcopy是都少不了的。因为两次 DMA 都是依赖硬件完成的。所以，所谓的零拷贝，都是为了减少CPU copy及减少了上下文的切换。

![零拷贝](https://user-images.githubusercontent.com/6687462/163912641-1c0dfdcb-06f2-4fda-859c-b815566f4d79.png)

|    | CPU拷贝 | 	DMA拷贝 | 系统调用| 上下文切换 |
|  ----  | ----  | ----  | ----  | --------  |
| 传统方法 | 2	| 2	| read+write	| 4 |
| 内存映射 |	1	| 2	| mmap+write	| 4 |
| sendfile |	1	| 2	| sendfile	| 2 |
| scatter/gather copy	| 0	| 2	|sendfile	| 2 |
|splice	| 0	| 2	| splice | 0 |

**参考资料：**<br />
* https://juejin.cn/post/6995519558475841550
* https://blog.csdn.net/h1012946585/article/details/109175511

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

### 三次握手和四次挥手
![TCP三次握手和四次挥手](https://user-images.githubusercontent.com/6687462/87508147-4fdae000-c6a1-11ea-8e50-974de1e9b49c.png)<br />

**为什么要三次握手**<br />
三次握手是通信双方相互告知序列号起始值，并确认对方已经收到序列号起始值的必经步骤。<br />
第一次握手：证明了接收端能收到消息。<br />
第二次握手：证明了发送端能收到接收端的消息，发送端知道接收端能收到它发送的消息。<br />
第三次握手：证明了接收端知道发送端能收到它发送的消息。<br />

**为什么要四次挥手**<br />
那四次分手又是为何呢？TCP协议是一种面向连接的、可靠的、基于字节流的运输层通信协议。TCP是全双工模式，这就意味着，当主机1发出FIN报文段时，只是表示主机1已经没有数据要发送了，主机1告诉主机2，它的数据已经全部发送完毕了；但是，这个时候主机1还是可以接受来自主机2的数据；当主机2返回ACK报文段时，表示它已经知道主机1没有数据发送了，但是主机2还是可以发送数据到主机1的；当主机2也发送了FIN报文段时，这个时候就表示主机2也没有数据要发送了，就会告诉主机1，我也没有数据要发送了，之后彼此就会愉快的中断这次TCP连接。

### 滑动窗口
TCP协议中是以段（Segment）为单位来发送数据的，我们也称其为最大消息长度（MSS：Maximum Segment Size），最理想的情况下MSS长度正好是IP中不会被分片处理的最大数据长度。TCP为了可靠传输，需要对每一个段进行确认应答，如果只有前一个发送段被确认后才能发送下一个段，那发送速率或吞吐量就太低了，所以有了“滑动窗口”的概念。窗口的大小就是指无需等待确认应答而可以继续发送的数据的最大值。当采用滑动窗口的情况下，如果出现某些报文段丢失的情况下，接收端会将同一个序号的确认应答重复不断的返回，而发送端主机如果连续3次收到同一个确认应答，就会将其所对应的数据进行重发。

### 拥塞控制算法
TCP的4种拥塞控制算法(慢开始、拥塞避免、快重传、快恢复)，发送方维护一个叫做拥塞窗口cwnd(congestion window)的状态变量，其值取决于网络的拥塞状况，会动态变化
* 拥塞窗户的维护原则：只要网络没有出现拥塞，cwnd就增大一些；但只要网络出现拥塞，拥塞窗口就减小一些
* 以分组发生超时重传作为发生网络拥塞的依据

通常在一条TCP连接开始时，cwnd被设置为1个MSS（最大报文段），也即cwnd=1
该阶段，每当TCP发送方将发送窗口的数据发送完，并顺利接收到所有的确认后，就会将拥塞窗口大小翻倍，也即慢启动阶段，cwnd以指数形式增长，如上图所示；注意这里忽略了接收窗口的影响，上文也提到了。
拥塞窗口会一直增长直到到达慢开始门限ssthresh，开始执行拥塞避免算法.

![TCP拥塞算法](https://user-images.githubusercontent.com/6687462/163093187-7ffb867f-bfcc-47f3-8e41-608d4e473475.png)

**Nagle算法**<br />
为了提高网络利用率，会经常使用Nagle算法，该算法是指发送端即使还有应该发送的数据，但如果这部分数据很少的话，则进行延迟发送的一种处理机制。具体来说就是满足如下任意一种条件才能发送数据：
1) 已发送的数据都已经收到确认应答时。
2) 可以发送最大段长度（MSS）的数据时。
一般对实时性要求高的系统会关闭TCP的Nagle算法。

**延迟确认应答**<br />

**参考资料**<br />
* 《图解TCP/IP（第5版）》
* https://ee.lbl.gov/papers/congavoid.pdf
* https://blog.csdn.net/qq_40459977/article/details/123079343

## HTTP
### HTTP1.0和HTTP1.1的区别
1. 长连接(Persistent Connection)：HTTP1.1支持长连接和请求的流水线处理，在一个TCP连接上可以传送多个HTTP请求和响应，减少了建立和关闭连接的消耗和延迟，在HTTP1.1中默认开启长连接keep-alive，一定程度上弥补了HTTP1.0每次请求都要创建连接的缺点。HTTP1.0中的keep-alive不算标准协议，客户端需要使用keep-alive参数来告知服务器端要建立一个长连接。
2. 断点续传：HTTP1.0中存在一些浪费带宽的现象，例如客户端只是需要某个对象的一部分，而服务器却将整个对象送过来了，并且不支持断点续传功能。HTTP1.1支持只发送header信息（不带任何body信息），如果服务器认为客户端有权限请求服务器，则返回100，客户端接收到100才开始把请求body发送到服务器；如果返回401，客户端就可以不用发送请求body了节约了带宽。断点续传通过在Header里两个参数实现的，客户端发请求时对应的是Range，服务器端响应时对应的是Content-Range
3. HOST域：在HTTP1.0中认为每台服务器都绑定一个唯一的IP地址，因此，请求消息中的URL并没有传递主机名（hostname），HTTP1.0没有host域。随着虚拟主机技术的发展，在一台物理服务器上可以存在多个虚拟主机（Multi-homed Web Servers），并且它们共享一个IP地址。HTTP1.1的请求消息和响应消息都支持host域，且请求消息中如果没有host域会报告一个错误（400 Bad Request）。
4. 缓存处理：在HTTP1.0中主要使用header里的If-Modified-Since,Expires来做为缓存判断的标准，HTTP1.1则引入了更多的缓存控制策略例如Entity tag，If-Unmodified-Since, If-Match, If-None-Match等更多可供选择的缓存头来控制缓存策略。
5. 新增多个错误码：在HTTP1.1中新增了24个错误状态响应码，如409（Conflict）表示请求的资源与资源的当前状态发生冲突；410（Gone）表示服务器上的某个资源被永久性的删除。
6. 新增了六种请求方法：OPTIONS、PUT、PATCH、DELETE、TRACE 和 CONNECT 方法。

### HTTP1.1和HTTP2.0的区别
1. 多路复用：客户端和服务端可以并行发起或者回复，避免串行带来的阻塞。做到同一个连接并发处理多个请求，而且并发请求的数量比HTTP1.1大了好几个数量级。HTTP1.1也可以多建立几个TCP连接，来支持处理更多并发的请求，但是创建TCP连接本身也是有开销的。
2. 二进制分帧：HTTP2 把 HTTP 协议通信的基本单位缩小为一个一个的帧，这些帧对应着逻辑流中的消息。并行地在同一个TCP连接上双向交换消息。二进制分帧层在 应用层(HTTP/2)和传输层(TCP or UDP)之间。HTTP2并没有去修改TCP协议而是尽可能的利用TCP的特性。在二进制分帧层中， HTTP/2 会将所有传输的信息分割为帧（frame）,并对它们采用二进制格式的编码 ，其中首部信息会被封装到 HEADER frame，而相应的 Request Body 则封装到 DATA frame 里面。
3. 报文压缩：在HTTP1.1中，HTTP请求和响应都是由状态行、请求/响应头部、消息主体三部分组成。一般而言，消息主体都会经过gzip压缩，或者本身传输的就是压缩过后的二进制文件，但状态行和头部却没有经过任何压缩，直接以纯文本传输。随着Web功能越来越复杂，每个页面产生的请求数也越来越多，导致消耗在头部的流量越来越多，尤其是每次都要传输UserAgent、Cookie这类不会频繁变动的内容，完全是一种浪费。 HTTP1.1不支持header数据的压缩，HTTP2.0使用HPACK算法对header的数据进行压缩，这样数据体积小了，在网络上传输就会更快。
4. 服务端推送：一种在客户端请求之前发送数据的机制。网页使用了许多资源：HTML、样式表、脚本、图片等等。在HTTP1.1中这些资源每一个都必须明确地请求。这是一个很慢的过程。浏览器从获取HTML开始，然后在它解析和评估页面的时候，增量地获取更多的资源。因为服务器必须等待浏览器做每一个请求，网络经常是空闲的和未充分使用的。为了改善延迟，HTTP2.0引入了server push，它允许服务端推送资源给浏览器，在浏览器明确地请求之前，免得客户端再次创建连接发送请求到服务器端获取。这样客户端可以直接从本地加载这些资源，不用再通过网络。

## WebSocket
**简介**：WebSocket用于基于现有的HTTP基础设施来解决双向通信的问题，所以它也使用了HTTP端口80和443以及支持HTTP代理和中介机构，但是，该设计并未将WebSocket限制为HTTP，未来的实现可以使用更简单的握手而不是专用端口。
现代浏览器都已经支持WebSocket协议，服务器则需要底层框架支持。Java的Servlet规范从3.1开始支持WebSocket，所以，必须选择支持Servlet 3.1或更高规范的Servlet容器，才能支持WebSocket。最新版本的Tomcat、Jetty等开源服务器均支持WebSocket。
WebSocket协议是一个独立的基于TCP的协议。它的 与 HTTP 的唯一关系是它的握手被解释为 HTTP 服务器作为升级请求。

**二进制帧**：WebSocket采用了二进制帧结构，语法、语义与HTTP完全不兼容，相比HTTP2，WebSocket更侧重于“实时通信”，而HTTP2更侧重于提高传输效率，所以两者的帧结构也有很大的区别。WebSocket握手成功后，客户端和服务器传回数据
并在本规范中称为概念单位 “消息”。在网络上，一条消息由一个或多个帧。WebSocket 消息不一定对应一个 特定的网络层成帧，因为可能是分段消息由中间人合并或拆分。
属于同一帧的每一帧 消息包含相同类型的数据。从广义上讲，有文本数据的类型（被解释为 UTF-8 [ RFC3629 ]文本），二进制数据（其解释由应用程序）和控制帧（不打算携带应用程序的数据，而不是协议级信令， 例如表示应该关闭连接）。

**协议名**：引入ws和wss分别代表明文和密文的websocket协议。

**设计原则**：WebSocket协议的设计原则是最小的框架（唯一存在的框架是使 协议基于帧而不是基于流，并支持 Unicode 文本和二进制帧之间的区别）。

### 什么时候使用WebSocket
WebSockets 可以使网页动态和交互。但是，在许多情况下，Ajax 和 HTTP 流或长轮询的组合可以提供简单有效的解决方案。
例如，新闻、邮件和社交订阅源需要动态更新，但每隔几分钟更新一次可能完全没问题。另一方面，协作、游戏和金融应用程序需要更接近实时。
延迟本身并不是决定性因素。如果消息量相对较少（例如，监控网络故障），HTTP 流式传输或轮询可以提供有效的解决方案。**正是低延迟、高频率和高容量的组合，才成为使用 WebSocket 的最佳案例**。
还要记住，在 Internet 上，不受您控制的限制性代理可能会阻止 WebSocket 交互，因为它们未配置为传递 Upgrade标头，或者因为它们关闭了看起来空闲的长期连接。这意味着将 WebSocket 用于防火墙内的内部应用程序是一个比面向公众的应用程序更直接的决定。

### WebSocket握手流程
这次握手的要求如下：
1. 握手必须是一个有效的 HTTP 请求。
2.请求的方法必须是GET，并且HTTP版本必须至少为 1.1。
3.请求的“Request-URI”部分必须匹配/resource name/ 在第 3 节中定义（相对 URI）或绝对http/https URI，在解析时具有 /resource name/、/host/、 和 /port/ 匹配相应的 ws/wss URI。
4. 请求必须包含一个 |Host| 其值的标头字段，包含 /host/ 加上可选的 ":" 后跟 /port/ （如果不是使用默认端口）。
5. 请求必须包含 |Upgrade| 其值的标头字段，必须包含“websocket”关键字。
6. 请求必须包含一个 |Connection| 其值的标头字段必须包含“Upgrade”令牌。
7. 请求必须包含一个标题字段，名称为|Sec-WebSocket-Key|。这个头域的值必须是 nonce 由随机选择的 16 字节值组成，该值具有已被 base64 编码（参见[RFC4648] 的第 4 节）。随机数必须为每个连接随机选择。
8. 请求必须包含一个名称为 |Origin| 的标头字段。
9. 请求必须包含一个带有名称的头域 |Sec-WebSocket-Version|。这个头域的值必须是13。
10. 请求可以包含一个带有名字的头域 |Sec-WebSocket-Protocol|。如果存在，该值表示一个或客户希望发言的更多逗号分隔的子协议，按偏好排序。构成此值的元素必须是非空字符串。
11. 请求可以包含一个带有名字的头域|Sec-WebSocket-Extensions|。如果存在，该值表示客户端希望发言的协议级扩展。
12. 请求可以包含任何其他头域。

**参考资料**<br />
* https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#websocket
* https://datatracker.ietf.org/doc/html/rfc6455

## RSocket
RSocket是在2018年发布的。RSocket最初是由Netifi公司和Facebook公司合作开发的，旨在解决网络通信协议不足的问题，并针对互联网应用和分布式系统做了优化。RSocket协议随后被开源并加入到Reactive Foundation，得到了广泛的关注和应用。
RSocket是一种异步、消息驱动、全双工的网络通信协议，旨在解决传统网络协议不足的问题。它提供了一种可靠、高效、灵活的通信机制，适用于多种应用场景。
RSocket提供了四种通信模式：请求/响应、请求/流、流/响应和流/流，可以满足不同的应用需求。在RSocket中，每个请求都是一个消息，可以携带任意数据类型，可以在请求头中指定通信协议版本、消息类型、序列化方式等信息。RSocket还支持各种负载均衡、流量控制和服务发现机制，可以让应用系统更加可靠和高效地运行。
RSocket与传统的Socket协议不同。传统的Socket协议是面向连接的，即在通信之前需要建立连接，而RSocket协议则是无连接的。传统的Socket协议是单向的，即在通信时只能进行一方向的数据传输，而RSocket协议是全双工的，可以同时进行双向数据传输。传统的Socket协议是同步阻塞的，即在请求和响应之间需要等待，而RSocket协议是异步非阻塞的，可以提高系统的并发性和响应速度。
总之，RSocket是一种新型的异步通信协议，具有可靠、高效、灵活等特点，可以适用于多种应用场景，特别适用于互联网应用和分布式系统。

RSocket协议可以使用HTTP/2作为传输协议，从而可以获得HTTP/2的一些优点，例如多路复用、流量控制、头部压缩等。但RSocket协议不仅限于使用HTTP/2，也可以使用其他传输协议，如TCP、WebSocket等。
总之，RSocket和HTTP都是网络通信协议，但RSocket是一种新型的异步通信协议，与HTTP在设计和应用场景上有很大的差异。RSocket可以使用HTTP/2作为传输协议，但也可以使用其他传输协议。
RSocket协议可以使用WebSocket作为传输协议，从而可以获得WebSocket的一些优点，例如实时性好、降低延迟等。RSocket协议与WebSocket的关系类似于HTTP/2和WebSocket的关系，即RSocket协议可以使用WebSocket作为底层传输协议，提供更好的性能和可靠性。
总之，RSocket和WebSocket都是用于实现双向通信的协议，但它们在设计和实现方式上有很大的差异。RSocket协议可以使用WebSocket作为传输协议，从而获得WebSocket的一些优点。


在Java中使用RSocket需要引入RSocket库。RSocket库可以通过Maven等构建工具进行引入。以下是使用Maven引入RSocket库的示例：
```xml
<dependency>
    <groupId>io.rsocket</groupId>
    <artifactId>rsocket-core</artifactId>
    <version>1.1.0</version>
</dependency>
```
在引入RSocket库后，可以使用Java代码实现RSocket通信。以下是一个简单的RSocket客户端实例：

```java
RSocket rsocket = RSocketConnector.connectWith(TcpClientTransport.create("localhost", 7000)).block();

Mono<Payload> response = rsocket.requestResponse(DefaultPayload.create("Hello RSocket!"));

response.subscribe(payload -> {
    System.out.println("Response: " + payload.getDataUtf8());
});

rsocket.dispose();
```
该示例中，首先通过RSocketConnector建立与RSocket服务器的TCP连接，并创建一个RSocket实例。然后，使用requestResponse方法发送请求消息，并使用subscribe方法订阅响应消息。最后，使用dispose方法关闭RSocket连接。
除了上述示例中的requestResponse方法外，RSocket还提供了其他的通信方法，例如requestStream、requestChannel等。每种通信方法都有不同的使用方式和适用场景。需要根据具体需求来选择合适的通信方法。
总之，RSocket是一种新型的异步通信协议，在Java中使用RSocket需要引入RSocket库，并根据具体需求来选择合适的通信方法。

## QUIC
QUIC（Quick UDP Internet Connection）是一种基于UDP协议的快速网络传输协议，由Google公司开发。QUIC旨在取代TCP协议，提供更快、更可靠、更安全的网络传输服务。
QUIC的优势有以下几个方面：
1. 快速连接建立：QUIC使用了0-RTT（Zero Round Trip Time）技术，可以在第一次连接时就进行身份验证，省去了TCP握手的开销，加快了连接的建立速度。
2. 可靠传输：QUIC使用了基于流的传输协议，每个数据包都有独立的编号和确认机制，能够有效地避免数据包的丢失和重传，提高了传输的可靠性。
3. 流量控制和拥塞控制：QUIC支持流量控制和拥塞控制，可以自动调整数据包的发送速率，避免网络拥塞和数据包丢失，提高了网络传输的效率和可靠性。
4. 安全性：QUIC使用了TLS加密技术，能够保证数据的安全性和隐私性，有效地避免了中间人攻击和数据泄露等安全问题。
总之，QUIC是一种基于UDP协议的快速网络传输协议，具有快速连接建立、可靠传输、流量控制和拥塞控制、安全性等优势。QUIC的目标是取代TCP协议，提供更快、更可靠、更安全的网络传输服务，已经被越来越多的网站和应用所采用。

## 跨域
跨域问题通常指的是在Web开发中遇到的一个安全性限制，它是由浏览器的同源策略（Same-Origin Policy）引起的。同源策略是浏览器的一个安全特性，旨在防止不同源之间的恶意文档或脚本相互干扰，这样可以保护用户的个人信息安全不被窃取。

同源策略规定，如果两个页面的协议、域名和端口号有任一不同，则它们就是不同的源。例如，以下几个URL：

```
http://www.example.com/dir/page.html
https://www.example.com/dir/other.html
http://www.example.com:81/dir/other.html
http://en.example.com/dir/other.html
```

第一个和第二个URL的协议不同，第一个和第三个的端口不同，第一个和第四个的子域名不同，它们都属于不同的源。

在同源策略的限制下，当一个网页试图去请求另一个不同源的资源时（比如通过AJAX），浏览器会拦截这些请求，导致跨域问题。这种限制主要影响到以下几个方面：

- AJAX请求：不能发起非同源的HTTP请求。
- Web字体（如CSS中通过@font-face嵌入跨域字体）：某些浏览器拒绝跨源字体。
- WebGL纹理：部分浏览器禁止跨域纹理。
- Cookie、LocalStorage和IndexedDB：JS不能读写其他源的数据。

为了解决跨域问题，开发者通常会使用以下几种方法：

1. **CORS（Cross-Origin Resource Sharing）：** 服务器可以通过设置Access-Control-Allow-Origin来允许特定的外域访问资源。CORS是一个W3C标准，允许服务器进行细粒度的控制，比如允许哪些方法、哪些头部、哪些源等。

2. **JSONP（JSON with Padding）：** 古老的解决方案，通过动态创建`<script>`标签的方式绕过同源策略，因为`<script>`标签的src属性加载的脚本不受同源策略的限制。但是JSONP只支持GET请求，并且安全性较差。

3. **代理服务器：** 在服务器端创建一个代理，将前端发来的跨域请求转发到目标服务器，再将响应返回给前端。因为服务器之间的请求不受同源策略限制。

4. **document.domain：** 如果两个页面仅域名不同，而主域相同（如example.com和sub.example.com），可以通过设置document.domain来实现同源。

5. **Window.postMessage：** 提供了一种在两个窗口之间进行安全跨源通信的方法。

6. **Web Sockets：** Web Sockets协议不实行同源策略，因此可以用于跨域通信。

解决跨域问题是为了在保障网站安全的前提下，实现不同域之间资源的合理共享与通信。开发者需要根据具体场景选择合适的解决方案。

### CORS
CORS（Cross-Origin Resource Sharing，跨源资源共享）是一种机制，它通过新增一系列HTTP头部，使得浏览器能够放宽同源策略的限制，从而允许来自不同源的Web页面执行跨域请求，获取受限的资源。

当一个跨域请求被发起时，浏览器会自动进行一些背后的工作来应用CORS：

1. **预检请求（Preflight Request）：** 对于那些可能对服务器数据产生副作用的请求方法（如PUT、DELETE等），或者含有非简单请求头部的HTTP请求，浏览器会先发送一个“预检”请求到服务器。这个预检请求是一个HTTP OPTIONS请求，询问服务器是否允许跨域请求，并且检查允许的方法和头部信息。

2. **简单请求：** 对于简单请求（如GET、HEAD、或POST（仅限于某些MIME类型）），浏览器直接发起跨域请求，并在请求中包含一个`Origin`头部，表示这个请求来自哪个源。

在接收到跨域请求后，服务器可以通过设置相应的CORS响应头部来告诉浏览器是否允许这个跨域请求：

- `Access-Control-Allow-Origin`: 指定了允许访问该资源的外域URI。如果服务器允许请求的外域，则这个头部会包含请求中的`Origin`头部的值，或者是`*`，表示允许任何域名的访问。

- `Access-Control-Allow-Methods`: 指定了服务器支持的所有跨域请求的方法。

- `Access-Control-Allow-Headers`: 用在对预检请求的响应中，指定了实际请求中允许携带的自定义头部字段。

- `Access-Control-Allow-Credentials`: 指定了当浏览器的credentials设置为`include`时，是否可以将请求的响应暴露给前端JavaScript代码。它的值只能是`true`，如果服务器不设置这个头部，浏览器将不会暴露响应给前端代码，无法读取响应内容。

如果服务器确认请求是安全可接受的，则会在响应中包含上述头部之一或全部，并返回正常的响应内容。浏览器接收到这些头部后，会根据这些头部信息判断是否允许响应内容被前端JavaScript访问。

因此，通过服务器端的配置来显式声明允许跨域，浏览器就不会拦截这些经过授权的跨域请求，从而实现跨域资源的共享。

抱歉让您感到困惑，这里需要澄清一下：

在CORS的上下文中，我们通常讨论两种不同类型的请求：预检请求（Preflight Request）和实际请求（Actual Request）。

1. **预检请求**：这是由浏览器自动发出的HTTP OPTIONS请求，用于查询服务器是否允许来自某个源的跨域请求。预检请求不会包含任何业务数据（如请求体或者实际的请求参数），仅包含一些CORS验证相关的头部信息。预检请求的响应也只是告诉浏览器允许的方法、头部等信息，并不包含业务层面的响应数据。

2. **实际请求**：这是在预检请求成功后，浏览器发出的实际业务请求。实际请求会包含应用层面的数据，如POST请求的请求体，GET请求的查询参数等。如果实际请求符合服务器在预检请求响应中声明的CORS策略，服务器将处理这个请求并返回业务数据。

因此，当我之前提到“服务器确认请求是安全可接受的，则会在响应中包含上述头部之一或全部，并返回正常的响应内容”，实际上是指两个步骤：

- 对于预检请求，服务器返回的是CORS相关的头部，确认是否允许跨域请求。
- 对于实际请求，一旦被允许，服务器处理业务逻辑，并返回业务数据，同时也会包含必要的CORS头部（如`Access-Control-Allow-Origin`），以便浏览器确定是否可以将响应暴露给前端JavaScript。

如果是简单请求（不触发预检的那种请求），则服务器在返回业务数据的同时，也会包含CORS相关的头部信息，让浏览器判断是否允许前端代码读取响应。

当你通过页面中的JavaScript发起一个跨域请求时，如果这个请求不符合浏览器定义的"简单请求"标准，浏览器会自动发起一个预检请求（Preflight Request）。

一个请求是否被判定为"简单请求"取决于以下几点：

1. 请求方法是以下三种之一：
    - GET
    - HEAD
    - POST

2. HTTP头信息不超出以下几种字段：
    - Accept
    - Accept-Language
    - Content-Language
    - Last-Event-ID
    - Content-Type（但仅限于三个值：`text/plain`、`multipart/form-data`、`application/x-www-form-urlencoded`）

3. 请求中没有使用任何自定义头部，比如`X-Custom-Header`。

4. 请求中没有使用ReadableStream对象。

如果请求不符合以上所有条件，它就不是一个简单请求。在这种情况下，浏览器会先发送一个OPTIONS请求作为预检请求，询问目标服务器是否允许该跨域请求。预检请求的目的是为了检查服务器是否同意并能够处理实际的请求。

预检请求会包含以下特定的HTTP头部：

- `Origin`：当前页面的源信息。
- `Access-Control-Request-Method`：实际请求中将会使用的HTTP方法。
- `Access-Control-Request-Headers`：实际请求中将会包含的自定义头部列表。

服务器在收到预检请求后，将根据自己的CORS策略来决定是否在响应中加入相应的CORS响应头部，比如`Access-Control-Allow-Origin`、`Access-Control-Allow-Methods`和`Access-Control-Allow-Headers`等，来明确告诉浏览器它是否接受这样的跨域请求。

浏览器在收到服务器的预检响应后会解析这些头部，并决定是否继续发起之前阻止的实际请求。如果服务器不允许跨域请求或预检请求失败（比如网络错误或预检响应没有包含正确的CORS头部），浏览器将不会发送实际请求，并且通常会在控制台中显示一个错误信息。

### 参考资料
* https://datatracker.ietf.org/doc/html/rfc9000 QUIC RFC
* https://datatracker.ietf.org/doc/html/rfc9001 QUIC TLS
* https://datatracker.ietf.org/doc/html/rfc9114 HTTP3 RFC
* https://developer.volcengine.com/articles/7268132377786843147   全面揭秘：抖音集团 QUIC 千万 QPS 应用实践
* https://github.com/maufl/quic_toy/blob/master/performance.markdown     Performance evaluation 
* https://cloud.tencent.com/developer/article/1031802      微信C2C渐进式图片流式传输系统简介
* https://datatracker.ietf.org/doc/html/rfc9000#section-18.2
* https://cloud.tencent.com/developer/article/1908451       提速 30%！腾讯TQUIC 网络传输协议
* https://youle.zhipin.com/articles/0da7ce03c37bcc5bqxB72Nq7Fg~~.html   Trip.com APP QUIC 应用和优化实践

# 数据结构
## BitMap

# 算法

## 动态规划
动态规划(Dynamic Programming)是一种分阶段求解决策问题的数学思想，它通过把原问题分解为简单的子问题来解决复杂问题动态规划在很多领域都有着广泛的应用例如管理学经济学数学生物学.

### 动态规划 vs 分治法
动态规划也是一种分治思想(比如其状态转移方程就是一种分治)但与分治算法不同的是，分治算法是把原问题分解为若干个子问题，自顶向下求解子问题，合并子问题的解，从而得到原问题的解。动态规划也是把原始问题分解为若干个子问题，然后自底向上，先求解最小的子问题，把结果存在表格中，在求解大的子问题时，直接从表格中查询小的子问题的解，避免重复计算，从而提高算法效率。

### 回溯算法 vs 深度优先遍历
**回溯法**：采用试错的思想，它尝试分步的去解决一个问题。在分步解决问题的过程中，当它通过尝试发现现有的分步答案不能得到有效的正确的解答的时候，它将取消上一步甚至是上几步的计算，再通过其它的可能的分步解答再次尝试寻找问题的答案。回溯法通常用最简单的递归方法来实现，在反复重复上述的步骤后可能出现两种情况：
1. 找到一个可能存在的正确的答案；
2. 在尝试了所有可能的分步方法后宣告该问题没有答案。

**深度优先搜索算法（英语：Depth-First-Search，DFS）**：是一种用于遍历或搜索树或图的算法。这个算法会 尽可能深 的搜索树的分支。当结点 v 的所在边都己被探寻过，搜索将 回溯 到发现结点 v 的那条边的起始结点。这一过程一直进行到已发现从源结点可达的所有结点为止。如果还存在未被发现的结点，则选择其中一个作为源结点并重复以上过程，整个进程反复进行直到所有结点都被访问为止。

我刚开始学习「回溯算法」的时候觉得很抽象，一直不能理解为什么递归之后需要做和递归之前相同的逆向操作，在做了很多相关的问题以后，我发现其实「回溯算法」与「 深度优先遍历 」有着千丝万缕的联系。

## 淘汰算法
### 最近最少使用(LRU)
最近最少使用(Least Recently Used)：这个缓存算法将最近使⽤的条⽬存放到靠近缓存顶部的位置。当⼀个新条⽬被访问时，LRU将它放置到缓存的顶部。当缓存达到极限时，较
早之前访问的条⽬将从缓存底部开始被移除。这⾥会使⽤到昂贵的算法，⽽且它需要记录“年龄位”来精确显⽰条⽬是何时被访问的。此外，当⼀个LRU缓存算法删除某个条⽬后，“年龄位”将随其他条⽬发⽣改变。

### 最不经常使用(LFU)
最不经常使用(Least Frequently Used)：这个缓存算法使⽤⼀个计数器来记录条⽬被访问的频率。通过使⽤LFU缓存算法，最低访问数的条⽬⾸先被移除。这个⽅法并不经常使⽤，
因为它⽆法对⼀个拥有最初⾼访问率之后长时间没有被访问的条⽬缓存负责。


# AIGC
## StableDiffusion
下载地址：https://stable-diffusion-ui.github.io/docs/installation/

## ChatGPT
### windows安装wget
从https://eternallybored.org/misc/wget/下载wget.ext后，不是双击安装，而是放到git的安装bin目录下（例如：D:\Git\mingw64\bin）

### 参考资料
* https://www.anaconda.com/
* https://github.com/microsoft/visual-chatgpt

# 硬件
## CPU
CPU周期和CPU时钟都是计算机中处理器（CPU）的重要概念，它们的区别和联系如下：
1. CPU周期：CPU周期是指CPU执行一条指令所需的时间，包括取指令时间、指令译码时间、执行时间和写回结果时间等。CPU周期的长短决定了CPU的性能，一个CPU周期越短，处理器的执行效率就越高。
2. CPU时钟：CPU时钟是指处理器中的时钟信号，用于同步CPU内部各个部件的工作，是CPU周期的基础。CPU时钟的频率越高，说明处理器的工作速度越快。
CPU周期和CPU时钟的关系是，CPU周期与CPU时钟频率的倒数成反比。也就是说，如果CPU时钟频率提高，CPU周期时间就会变短。例如，如果CPU的时钟频率为1GHz，那么每秒会产生10^9个时钟信号，每个时钟信号对应一个CPU周期，每个CPU周期时间为1/10^9秒，即1纳秒。
总之，CPU周期和CPU时钟都是计算机中处理器的重要概念，CPU周期是CPU执行一条指令所需的时间，CPU时钟是处理器中的时钟信号，用于同步CPU内部各个部件的工作。CPU周期与CPU时钟频率的倒数成反比，两者共同决定了CPU的性能



# IM框架
* https://github.com/52im/fastim2023
* https://github.com/XiaoWeiKIN/hermes
