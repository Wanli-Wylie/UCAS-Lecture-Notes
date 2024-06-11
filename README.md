# UCAS-Lecture-Notes

这个仓库包含了我于2024年在国科大就读时的课程笔记。主要可以分为两类：

- AI类课程：
  - 高级人工智能（计算所），闭卷
  - 知识工程（自动化所），开卷
  - 自然语言处理（自动化所），闭卷
  - 计算机视觉（计算所），闭卷
  - 跨模态智能计算（信工所），开卷
- 计算机系统类课程
  - 数据挖掘（计算机学院本部），闭卷
  - 大数据系统与大规模数据分析（计算所），闭卷
  - 分布式与并行计算技术（软件所），开卷
 
其中，CV、NLP技术对跨模态技术的支撑关系无需多言。这里可以分享一下我对于Big Data Systems与Distributed Systems技术两个领域关系的理解：
对于一切暴露API的系统，无论是向内还是向外，都可以从系统管理的资源及其提供的操作这些资源的API角度来理解系统。本质上，所有的API都可以分类为CRUD（Create, Read, Update, Delete）操作，不管系统有多复杂。每种资源抽象——无论是Key-Value Pairs、Files、Documents、Nodes and Edges、Tasks还是Datasets——都有与之相关的CRUD操作，这些操作使与系统的交互成为可能。
在不同场景中，CRUD操作必须满足特定属性以满足系统要求。这些属性可以分类为：

- 硬属性：系统正确运行所必需的基本保证，包括Consistency、Partition Tolerance、Fault Tolerance、Concurrency Control和ACID Properties等。
- 软属性：增强系统性能和用户体验的理想特性，包括Scalability、Availability、Data Locality、高Performance和Efficiency等。

每个属性都需要实施特定的机制。为了确保CRUD操作满足所需属性，人们已经提出了许多机制，举例如下：
- Consistency：确保数据在读取时始终是一致的，主要与Read和Update操作相关，通过Quorum Consensus、Write Concern和ACID Transactions等机制实现。
- Partition Tolerance：保证系统在某些部分网络分区时仍能继续操作，主要影响Create、Read、Update和Delete操作，通过Consistent Hashing和Sharding实现。
- Fault Tolerance：确保系统在某些节点故障时仍能正常运行，主要涉及Create和Update操作，通过Replication、Task Re-execution、Checkpointing、Tuple Acknowledgement和Lineage确保。
- Concurrency Control：管理多个并发操作的执行顺序，防止冲突，主要与Update操作相关，通过Locks、MVCC（Multi-Version Concurrency Control）、Job Scheduling、Vertex Locking和Task Parallelism管理。
- Scalability：系统能够处理不断增长的工作负载，主要影响Create和Read操作，通过Sharding、Horizontal Scaling、Distributed Processing、Partitioning和Parallelism实现。
- Availability：保证系统在大部分时间内可用，主要涉及Read和Update操作，通过Replication维护。
- Data Locality：优化数据放置以减少访问延迟，主要影响Read操作，通过Data Placement、Locality-Aware Scheduling和Edge Partitioning增强。
- High Performance：提升系统的整体响应速度，主要影响Read和Update操作，通过In-Memory Processing和In-Memory Computing实现。
- Efficiency：优化资源使用以提高系统效率，主要涉及Create和Update操作，通过Task Scheduling、Speculative Execution、Vertex Cut和Load Balancing优化。

要全面掌握这些机制的功能及其实现方式，必须从Distributed Systems protocols的角度来理解它们。关键关注领域包括：
- Consensus Protocols：确保多个分布式节点在面对可能存在的网络分区和节点故障时，能够就某一数据或操作达成一致，例如Paxos，Raft等。
- Replication Protocols：用于在多个节点之间复制数据，以提高系统的可用性和容错能力，例如Primary-Backup Replication，Chain Replication，Gossip Protocols，Quorum-based Replication，Transaction Protocols等。
- Transaction Protocols：用于管理分布式事务，确保在多个节点上执行的操作要么全部成功，要么全部失败，例如2PC等。
- Leader Election Protocols：用于在分布式系统中选举一个领导者节点，以协调和管理其他节点，例如Bully等。
- Membership Protocols：用于管理分布式系统中的节点成员资格，包括节点的加入、离开和失败检测，例如SWIM (Scalable Weakly-consistent Infection-style Membership)等。

下表简要列出了常见的大数据系统中的资源抽象与它们应满足的属性：

| System                     | Resource Abstraction       | Medium       | C                     | R                     | U                     | D                     |
|----------------------------|----------------------------|--------------|-----------------------|-----------------------|-----------------------|-----------------------|
| Key-Value Store            | Key-value pairs            | Memory, Local Storage | Consistency, Partition Tolerance | Consistency, Availability | Consistency, Mutual Exclusion | Consistency, Availability |
| Distributed File System    | Files and directories      | Local Storage | Fault Tolerance, Data Locality | Scalability, Fault Tolerance | Fault Tolerance, Concurrency Control | Fault Tolerance |
| Relational Database        | Tables, rows, columns      | Local Storage | ACID, Consistency     | ACID, Concurrency Control | ACID, Concurrency Control | ACID, Consistency     |
| Batch Processing System    | Large datasets             | Local Storage | Scalability           | Data Locality         | -                     | -                     |
| MapReduce                  | Tasks                      | Local Storage | Scalability           | Data Locality         | Fault Tolerance       | Fault Tolerance       |
| MapReduce                  | Data blocks                | Local Storage | Scalability           | Data Locality         | Fault Tolerance       | Fault Tolerance       |
| MongoDB                    | Documents                  | Memory, Local Storage | Consistency, Partition Tolerance | Consistency, Availability | Consistency, Mutual Exclusion | Consistency, Availability |
| Graph Database             | Nodes and edges            | Memory, Local Storage | Consistency, Fault Tolerance | Consistency, Availability | Consistency, Concurrency Control | Consistency, Fault Tolerance |
| Pregel Model               | Vertices and edges         | Memory       | Scalability           | Data Locality         | Concurrency Control   | Fault Tolerance       |
| Hadoop                     | Files                      | Local Storage | Fault Tolerance, Scalability | Scalability, Fault Tolerance | Fault Tolerance, Concurrency Control | Fault Tolerance |
| Hadoop                     | Tasks                      | Local Storage | Fault Tolerance, Scalability | Scalability, Fault Tolerance | Fault Tolerance, Concurrency Control | Fault Tolerance |
| Hive                       | Tables                     | Local Storage | Scalability, Consistency | Consistency, Scalability | Concurrency Control   | Scalability, Consistency |
| Hive                       | Rows, columns              | Local Storage | Scalability, Consistency | Consistency, Scalability | Concurrency Control   | Scalability, Consistency |
| Storm                      | Streams                    | Memory       | High Performance, Scalability | High Performance, Fault Tolerance | Fault Tolerance, Concurrency Control | Scalability, Fault Tolerance |
| Storm                      | Tuples                     | Memory       | High Performance, Scalability | High Performance, Fault Tolerance | Fault Tolerance, Concurrency Control | Scalability, Fault Tolerance |
| Spark                      | RDD (Resilient Distributed Dataset) | Memory, Local Storage | Fault Tolerance, Data Locality | High Performance, Data Locality | Fault Tolerance, Concurrency Control | Fault Tolerance |
| Spark                      | Tasks                      | Memory, Local Storage | Fault Tolerance, Data Locality | High Performance, Data Locality | Fault Tolerance, Concurrency Control | Fault Tolerance |

## 课程简介

### 分布式与并行计算技术

- **并行计算模型：** 

  - **控制流图（CFG）的视角**: 从CFG的视角探讨可并行化程序的控制流和循环并行化技术，重点在于如何识别和优化可并行化的代码段，从而提高计算效率。

  - **共享内存部分**: 除了介绍共享内存的API（如OpenMP等），还重点关注了编译器如何通过OS层面的API实现共享内存编程API。这包括内存分配、同步机制（如互斥锁、信号量）和线程管理等。讨论了在共享内存编程中常见的挑战，如数据竞争和死锁问题，并介绍了相应的调试和优化方法。

  - **MPI部分**: 除了介绍MPI（Message Passing Interface）的基本API（如发送/接收、广播、规约操作等），还简要探讨了这些API在底层的实现机制。这包括内部数据结构、网络通信协议、消息缓冲管理和并行任务调度等。

  - **CUDA部分**: 详细介绍了GPU的体系结构与软件逻辑，包括流处理器与显存架构、warp的调度与执行等内容。讨论了CUDA编程模型中的核心概念（如线程块、网格、共享内存、全局内存），以及如何利用这些特性进行高效的并行计算。

- **分布式系统：**

  - **时间同步算法与分布式Snapshot**: 时间同步算法（如NTP、PTP），在分布式系统中实现一致的时间视图。分布式Snapshot算法（如Chandy-Lamport算法），用于捕获系统的一致性状态，方便故障恢复和调试。

  - **P2P路由与DHT技术**: 点对点（P2P）网络的路由算法和分布式哈希表（DHT）技术。这包括Chord、Kademlia等典型的DHT协议，讨论其节点查找、数据存储和故障恢复机制。分析P2P网络的优势和挑战，如去中心化、扩展性和安全性问题。

  - **资源互斥与选举算法，组播通讯模型**: 分布式系统中的资源互斥问题及其解决方案（如分布式锁、令牌环算法），选举算法（如Bully算法、Ring算法），用于在分布式环境中选举领导者节点。同时，组播通讯模型及其实现（如IP组播、应用层组播），用于高效地在多个节点间传播信息。

  - **共识算法**: Paxos、Raft、PBFT等共识算法。这些算法在分布式系统中用于实现一致性，确保所有节点达成一致决策。分析每种算法的基本原理、工作流程、优缺点以及应用场景。探讨这些算法在容错性、性能和复杂性方面的权衡，并介绍其在实际系统中的应用案例。

### 大数据系统与大规模数据分析

- 大数据系统：从system角度介绍了一系列常用的组件的实现细节与具体思路：

  - **RDBMS的具体架构与实现细节**：深入分析关系型数据库管理系统（RDBMS）的核心组件和工作机制。涵盖SQL解析器（解析SQL查询）、查询优化器（优化查询计划）、执行引擎（执行查询）、缓冲池（管理内存缓存）、数据存储引擎（存储数据）和事务管理系统（维护数据一致性）。SQL解析器本质上是一个parser，查询优化器类似于一个IR optimizer，与编译器技术栈共享相似之处。存储结构如B+树，Join操作的分布式实现等也在此讨论。
  - **分布式文件系统**：讨论NFS（Network File System）、AFS（Andrew File System）和GFS/HDFS（Google File System/ Hadoop Distributed File System）的实现细节，重点在于其文件存储、数据分布和容错机制。
  - **分布式KV-store**：分析Dynamo、Bigtable/HBase和Cassandra的架构和实现，重点介绍其使用的LSM-Tree数据结构以及如何实现高效的键值存储和检索。
  - **No-SQL数据库**：探讨MongoDB和Neo4j的实现细节，涵盖数据一致性、事务管理和负载均衡机制，介绍其在处理非结构化数据和图数据中的应用。
  - **MapReduce的实现**：详细说明MapReduce的工作原理、通讯机制与容错机制，并举例用MapReduce实现Grep操作，探讨其在大规模数据处理中的优势。
  - **同步图计算模型Pregel的实现细节**：探讨Pregel的实现细节，分析其数据流动机制，讨论如何在大规模图计算中实现高效的并行处理。
  - **流数据处理系统**：分析Storm和Kafka的数据模型、实现细节和容错机制，讨论其在实时数据流处理中的应用和优势。
  - **内存数据库**：探讨Memcached和Redis的实现思路与系统架构，分析其在高性能缓存和内存数据库中的应用。
  - **批处理系统Spark**：介绍Spark的系统架构，RDD（Resilient Distributed Dataset）的概念，以及其中心化的管理、执行和调度机制，探讨其在大数据批处理中的应用。

- 大数据计算：

  - **流数据处理算法**：研究在资源有限的情况下高效挖掘数据流的统计特征的算法，讨论其在实时数据分析中的应用。

    **大数据检索**：分析KD树和局部敏感哈希（LSH）等大规模数据检索算法，探讨其在高维数据空间中的应用和优化策略。

### 跨模态智能计算

深度学习框架为视觉和文本等领域的表示学习（representation learning）和对比学习（contrastive learning）提供了理论基础。其核心包括模型架构和训练算法两大部分：

- **模型架构**: 深度学习的架构从最初的多层感知机（MLP）发展到专门针对视觉任务的残差网络（ResNet），处理语言任务的循环神经网络（RNN），以及具备高度可扩展性的Transformer。
- **训练算法**: 训练算法的设计旨在优化监督信号在模型中的有效传递，通常通过伪代码表示。这些监督信号主要由损失函数的梯度组成，并通过如随机梯度下降（SGD）和自适应矩估计（Adam）等优化算法进行优化。除了传统的监督学习，监督信号的来源还包括从教师模型中获取知识的知识蒸馏（Knowledge Distillation）、无监督对比学习如MoCo，以及领域适应（Domain Adaptation, DA）和领域泛化（Domain Generalization, DG）等先进技术。此外，像PyTorch Ignite这样的框架将训练过程抽象为引擎，提供了面向对象的抽象，便于构建和管理复杂的训练流程。

单模态信息的处理和表示学习：

- 单模态信息的处理和表示学习依赖于深度学习的基本技术，构建模块化的数据流水线。例如，像BERT、LLAMA、ResNet、ViT等模型的预训练权重在单模态信息提取中表现出色，这些模型为跨模态信息提取流水线的构建提供了基本的组件。
- **视觉信息理解**: 相比文本，视觉数据的非结构化程度更高，许多工作聚焦于从文本的角度理解视觉数据，从中提取语义信息。目标检测（如R-CNN，Fast R-CNN、Faster R-CNN，YOLO，DETR等）和场景图生成都是具体的例子。直观地说，这些算法构建了从视觉域到文本域的数据降维。
- **生成算法的应用**: 生成算法在单模态任务中的应用也非常值得借鉴，例如用于变长序列生成的seq2seq算法，以及用于图像生成的VAE、GAN和diffusion等算法。即使是在跨模态生成任务中，最终生成的内容也通常体现为某个模态的数据，因此单一模态的生成算法依然具有重要意义。

跨模态信息的处理和表示学习：

- 跨模态信息的处理和表示学习是跨模态智能计算的核心科学问题。这要求从单模态技术中汲取灵感，提出多模态特征提取器（feature extractor）的构建方案。与单一模态不同，不同模态的数据之间存在模态鸿沟，承载着完全不同的信息，信息粒度也不一致。例如，视觉信息由像素、目标、区域等组成，而文本信息由token、词语、短语、句子、文档等组成。如何对这些不同粒度的信息构建一个统一的表示是关键问题。
- **跨模态生成和推理算法**: 跨模态生成和推理算法与单模态技术存在根本性的差异，为弥补模态鸿沟提供了一系列具体的解决方案，如常识推理、变化场景的稳定性等。目前的生成式模型主要采用仅有解码器的架构（decoder-only），这反映了一种权衡，即在参数量继续膨胀的情况下，逐渐不再需要编码器来构建一个中间表示。然而，特征向量在检索和理解等情景下依然具有重要价值。

### 知识工程

TO DO

### 计算机视觉

TO DO

### 高级人工智能

TO DO

### 自然语言处理

TO DO

### 数据挖掘

TO DO
