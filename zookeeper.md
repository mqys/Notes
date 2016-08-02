# Content
- [Concepts](#Concepts)

## Concepts
### CAP定理
- 一个分布式系统不可能同时满足CAP: C: 一致性Consistency, A: 可用性Availablity, P: 分区容错性Partition tolerance, 最多只能满足两项.

### BASE理论
- Basic Available(基本可用), Soft state(软状态), Eventually consistent(最终一致性)
  - Basic Available: 响应时间上的损失, 功能上的损失
  - Soft state: 允许系统中的数据存在中间状态
  - Eventually consistent: 系统中的所有数据副本, 在经过一段时间的同步之后, 最终达到一个一致的状态

### 2/3PC
- two / three Phase Commit
- 2PC:
  1. 协调者询问所有参数者是否执行提交; 各个参与者开始事务执行的准备工作; 参数者响应协调者.
  2. 如果所有参与者都回应可以提交, 协调者向所有参与者发送提交命令; 如果有拒绝的参与者, 则发送回滚命令.
- 3PC:
  - 将第一阶段分为询问和锁资源(precommit)

### Paxos
- 大多数的决定会成为整个集群的同一决定
- 增加提案号, 只会执行最新的提案

### zookeeper
- 集群角色:
  - leader, follower, observer
  - leader: 为客户端提供读和写服务
  - observer: 读服务, 不参与选举, 用于提升集群的读性能
  - follower: 读服务
- 节点:
  - 机器节点
  - 数据节点(数据模型中的数据单元)(ZNode)
    - 所有数据存储在内存中
    - 数据模型是一棵树
    - 每个ZNode保存数据内容和一系列属性信息
    - 节点分为临时节点和持久节点
- watcher(时间监听器):
  - 在指定节点注册watcher, 在事件触发时, zookeeper服务器通知相应的客户端
