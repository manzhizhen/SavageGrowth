# SavageGrowth
## 帮助程序员找到适合自己的成长框架
念念不忘必有回响，持续更新中...

# <架构设计>
**软件架构定义（之一）：** 软件架构式解释该系统所需的结构体的集合，其中包括：软件元素、元素之间的相互关系，以及二者各自的属性。 
* 架构是必须在项目早期作出的一组设计决策。这通常也被非正式的称为“那些在项目后期难以改变的内容”。
* 架构是对系统恰如其分的施加约束，一遍系统获得我们所需质量属性的一门艺术。
* 架构并不仅仅只是设计的宏观部分，如果细节关乎系统的整体质量，那么这些细节也应该属于架构层面的内容。
* 任何软件系统都有自己的架构，架构是客观存在的。

**参考资料：**
《恰如其分的软件架构》

### 微服务架构
**微服务定义：** 微服务是由以单一应用程序构成的小服务，自己拥有独立的进程，服务依赖业务功能的设计，以全自动的方式部署，与其他服务使用轻量级的通信（例如HTTP）。同时服务会使用最小的规模的集中管理能力，服务可以用不同的编程语言与数据库等组件实现。

微服务架构是一种架构风格。

### GoF的23种设计模式

### 面向对象设计原则
最基本的五大设计原则（SOLID）：单一职责原则、开放封闭原则、里式替换原则、接口隔离原则和依赖倒置原则。


### 业务系统设计的基本原则

**1. 可维护性是根本**
* 代码可读性很关键
* 设计权衡时优先考虑简单设计
* 打造可扩展系统

**2. 多参考业界的成功模式**
* GoF的23种设计模式
* 面向对象的X大设计原则
* 业界现有的设计案例

**3. 稳定性是底线**
* 充分了解背后的非功能性诉求
* 尽可能做到可降级
* 实现异常出口

**4. 选择最恰当的设计方案**
* 中间件的设计方式不一定适合业务系统
* 方案选型要考虑团队的技能水位
* 方案要符合项目当前的发展阶段（超前设计需谨慎）
* 重点评估方案的维护成本
* 多套方案中选择最合适的方案

**4. **

## <云原生>
**定义：** 云原生技术有利于各组织在公有云、私有云和混合云等新型动态环境中，构建和运行可弹性扩展的应用。云原生的代表技术包括容器、服务网格、微服务、不可变基础设施和声明式API。这些技术能够构建容错性好、易于管理和便于观察的松耦合系统。结合可靠的自动化手段，云原生技术使工程师能够轻松地对系统作出频繁和可预测的重大变更。云原生计算基金会（CNCF）致力于培育和维护一个厂商中立的开源生态系统，来推广云原生技术。我们通过将最前沿的模式民主化，让这些创新为大众所用。

**参考资料：**
* https://github.com/cncf/toc/blob/master/DEFINITION.md
* https://jimmysong.io/kubernetes-handbook/cloud-native/cloud-native-definition.html

### Docker

### Service Mesh

### Serverless

## <存储>

### RDS

### NoSQL
NoSQL常见的四种类型：键值对型、文档型、列式存储型和图型。

#### Redis
定义：Redis是一种采用内存来作为数据结构存储的数据库、缓存和消息代理。
支持的数据结构：字符串，哈希，列表，集合，带范围查询的排序集合，位图，HyperLogLog，地理空间索引。
集群模式：
扩展：HyperLogLog、

## <基础框架>

## <常见工具>
### Arthas

