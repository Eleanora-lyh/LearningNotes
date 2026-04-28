[大数据面试题V3.0，约870篇牛客大数据面经480道面试题_牛客网](https://www.nowcoder.com/discuss/353159520220291072)

https://zhuanlan.zhihu.com/p/424296249 [大数据开发面经汇总【持续更新...】_牛客网](https://www.nowcoder.com/discuss/594817738107781120)

https://leetcode.cn/discuss/post/3516212/zi-jie-mian-jing-nian-xin-70wda-shu-ju-s-23r7/

[大数据开发面经_大数据面经-CSDN博客](https://blog.csdn.net/axzy5863/article/details/158429145)

[大数据开发（牛客）面试被问频率最高的几道面试题-腾讯云开发者社区-腾讯云](https://cloud.tencent.com/developer/article/2071876)

---

## 🐘 Hadoop整体理解

把Hadoop想象成一个**超大的仓库管理系统**：

- **HDFS** = 仓库（存东西）
- **MapReduce** = 工人（干活）
- **YARN** = 仓库主管（分配工人和资源）

---

## Hadoop基础

### 什么是Hadoop调度器？说明其工作方法

Hadoop 调度器（Hadoop Scheduler）通常指 YARN Resource Scheduler（在 Hadoop 2.x 之后 Hadoop Scheduler 本质上就是 YARN Scheduler） 中的资源调度组件，负责决定 集群中的 CPU、内存等计算[大数据面试题V3.0，约870篇牛客大数据面经480道面试题_牛客网](https://www.nowcoder.com/discuss/353159520220291072)

https://zhuanlan.zhihu.com/p/424296249 [大数据开发面经汇总【持续更新...】_牛客网](https://www.nowcoder.com/discuss/594817738107781120)

https://leetcode.cn/discuss/post/3516212/zi-jie-mian-jing-nian-xin-70wda-shu-ju-s-23r7/

[大数据开发面经_大数据面经-CSDN博客](https://blog.csdn.net/axzy5863/article/details/158429145)

[大数据开发（牛客）面试被问频率最高的几道面试题-腾讯云开发者社区-腾讯云](https://cloud.tencent.com/developer/article/2071876)

---

## 🐘 Hadoop整体理解

把Hadoop想象成一个**超大的仓库管理系统**：

- **HDFS** = 仓库（存东西）
- **MapReduce** = 工人（干活）
- **YARN** = 仓库主管（分配工人和资源）

---

## Hadoop基础

### 什么是Hadoop调度器？说明其工作方法

Hadoop 调度器（Hadoop Scheduler）通常指 YARN Resource Scheduler（在 Hadoop 2.x 之后 Hadoop Scheduler 本质上就是 YARN Scheduler） 中的资源调度组件，负责决定 集群中的 CPU、内存等计算资源如何分配给各个应用程序（如 MapReduce、Spark、Hive 任务）。当多个用户或任务同时提交作业时，调度器决定谁先运行、谁使用多少资源、资源如何公平分配。

用户提交任务

三种调度器：

| 调度器               | 机制                 | 适用场景    |
| ----------------- | ------------------ | ------- |
| FIFO              | 先进先出               | 简单单用户系统 |
| CapacityScheduler | 多队列 + 优先级高、占资源少的先跑 | 大型企业    |
| FairScheduler     | 尽量公平分配资源           | 多用户共享   |

**FIFO**：

**CapacityScheduler**：

**FairScheduler**：

### 为什么需要调度器？

1、资源有限：Hadoop 集群资源，没有调度器的话：所有任务都在抢资源、可能有的任务占满集群、其他任务一直等待，调度器让系统 可控分配资源。

2、多用户共享：企业 Hadoop 经常是 共享集群（数据开发、算法团队、BI团队）

3、保证公平：让短任务快速运行

4、提高集群利用率：调度器可以实现资源借用、资源借用。提高 Cluster Utilization（集群利用率）

### 什么时候

### hadoop框架的理解、Hadoop的特点

Hadoop = **HDFS**（分布式存储）+ **MapReduce**（分布式计算）+ **YARN**（资源管理）

特点：**高可靠**（多副本容错）、**高扩展**（加机器就能扩容）、**高容错**（节点挂了自动恢复）、**低成本**（普通硬件即可）

### Hadoop生态圈组件及其作用

| 组件        | 作用                     |
| --------- | ---------------------- |
| HDFS      | 分布式文件存储                |
| MapReduce | 分布式批处理计算               |
| YARN      | 资源调度与管理                |
| Hive      | SQL查询工具（SQL转MapReduce） |
| HBase     | 分布式列式NoSQL数据库          |
| ZooKeeper | 分布式协调服务（选主、配置管理）       |
| Kafka     | 高吞吐消息队列                |
| Flume     | 日志采集                   |
| Sqoop     | 关系型数据库与HDFS互导          |
| Spark     | 内存计算引擎，比MR快            |

### Hadoop 1.x，2.x，3.x的区别

- **1.x**：JobTracker同时负责资源管理和任务调度，单点瓶颈；没有HA
- **2.x**：引入YARN把资源管理分出去；HDFS支持NameNode HA和Federation
- **3.x**：支持多个NameNode；引入**纠删码（EC）**替代副本节省存储约50%；支持GPU资源调度

### Hadoop集群工作时启动哪些进程？它们有什么作用？

- **NameNode**：管理HDFS元数据（文件在哪、有几个副本），不存实际数据
- **DataNode**：存储实际数据块，定期向NameNode发心跳汇报状态
- **ResourceManager**：管整个集群资源，接受Job提交，分配资源
- **NodeManager**：管单个节点资源，启动和监控Container
- **SecondaryNameNode**（非HA模式）：辅助NameNode合并日志，**不是**NameNode备份

### 在集群计算的时候，什么是集群的主要瓶颈

**磁盘I/O**是主要瓶颈，尤其是MapReduce的Shuffle阶段（大量数据溢写磁盘+网络传输）。其次是**网络带宽**。

### 搭建Hadoop集群的xml文件有哪些？

- `core-site.xml`：核心配置（HDFS地址等）
- `hdfs-site.xml`：HDFS配置（副本数、块大小等）
- `mapred-site.xml`：MapReduce配置
- `yarn-site.xml`：YARN配置

### Hadoop的checkpoint流程

> **类比：** 就像把流水账（editlog）定期整理成账本快照（fsimage），防止流水账越来越长。

1. SecondaryNameNode从NameNode拉取editlog和fsimage
2. 将editlog回放合并到fsimage，生成新fsimage
3. 将新fsimage推回NameNode，清空旧editlog

作用：防止editlog无限增长，加快NameNode重启速度。

### Hadoop的默认块大小是多少？为什么设置这么大？

默认**128MB**（Hadoop 2.x起）。

原因：磁盘寻址时间约10ms，传输速率约100MB/s，128MB传输约1.28秒，寻址时间占比约1%，效率最优。

- 太小 → Map任务数多，启动开销大
- 太大 → Map并行度低

### Block划分的原因

- 大文件切块后可**多节点并行处理**
- Block分散到各DataNode，**负载均衡**
- 单个Block损坏只需恢复该Block，**容错代价小**

### Hadoop常见的压缩算法？

| 算法     | 是否可切分   | 速度  | 压缩比 | 适用场景       |
| ------ | ------- | --- | --- | ---------- |
| Gzip   | ❌       | 中   | 高   | 冷数据存储      |
| Bzip2  | ✅       | 慢   | 最高  | 需切分的归档     |
| Snappy | ❌       | 最快  | 中   | Map输出、中间数据 |
| LZO    | ✅（需建索引） | 快   | 中   | 大文件、需切分场景  |

> 注意：不可切分的压缩格式（如Gzip）大文件只能一个Map处理，并行度差。

### Hadoop作业提交到YARN的流程？

1. Client向ResourceManager提交Job（上传JAR到HDFS）
2. RM分配Container，启动**ApplicationMaster**
3. AM向RM申请运行MapTask/ReduceTask的Container
4. AM联系NodeManager，在Container中启动任务
5. 任务完成，AM向RM注销，资源释放

### Hadoop的Combiner的作用

在**Map端本地预聚合**，减少传输到Reduce的数据量。

> **类比：** 100人统计词频，传纸条前先自己合并，传"hadoop:50"而不是50张"hadoop:1"。

要求操作满足交换律和结合律：✅ sum/max/min，❌ avg（会丢信息）

### Hadoop序列化和反序列化

Hadoop用`Writable`接口（非Java原生序列化），更紧凑高效，节省带宽。

常用类型：`IntWritable`、`LongWritable`、`Text`、`NullWritable`

### Hadoop的运行模式

- **本地模式**：单机单JVM，无HDFS，用于开发调试
- **伪分布式**：单机模拟集群
- **完全分布式**：多节点，生产环境

### Hadoop小文件处理问题

**问题：** 每个小文件占NameNode约150字节内存；每个小文件启动一个MapTask，启动开销远大于计算本身。

**解决：**

- **CombineFileInputFormat**：合并小文件再处理
- **SequenceFile**：将小文件以KV形式合并存储
- **HAR归档**：打包小文件
- 上游控制，避免产生小文件（如Hive设置合并输出）

### Hadoop为什么要从2.x升级到3.x？

- **纠删码**：存储开销从200%降至约50%，节省大量存储成本
- **多NameNode**：突破单NameNode扩展瓶颈
- **支持GPU/FPGA**资源调度

### Hadoop的优缺点

- **优点**：高容错、低成本、高扩展、适合PB级批量处理
- **缺点**：延迟高（不适合实时）、小文件问题、不支持随机写、不适合迭代计算

---

## 📦 HDFS

> **整体类比：** 图书馆管理系统
> 
> - NameNode = 图书馆目录（记录书在哪，但不存书）
> - DataNode = 书架（真正放书的地方）
> - Block = 把大书撕成若干份（128MB一份）
> - 副本数3 = 每份复印3本放不同书架，防止丢失

### HDFS NameNode高可用如何实现？需要哪些角色？

架构：**Active NameNode + Standby NameNode**

| 角色                 | 作用                           |
| ------------------ | ---------------------------- |
| Active NameNode    | 对外提供服务                       |
| Standby NameNode   | 热备，实时同步editlog               |
| JournalNode集群（≥3个） | 共享editlog，Active写入，Standby读取 |
| ZooKeeper          | 选主，记录谁是Active                |
| ZKFC               | 监控NameNode健康，触发自动切换          |

### HDFS中向DataNode写数据失败了怎么办

1. 将失败的DataNode从pipeline中移除
2. 已写数据标记为损坏
3. NameNode重新分配新DataNode，重建pipeline继续写
4. 写完后NameNode发现副本数不足，触发后台重新复制

### DataNode什么情况下不会备份

强制关闭或非正常断电时。

### HDFS中DataNode怎么存储数据的

- 数据以**Block文件**存在本地磁盘
- 每个Block对应一个`.meta`校验文件（CRC）
- DataNode每3秒向NameNode发**心跳**，每6小时发**块报告**

### NameNode存数据吗？

**不存实际数据**，只存**元数据**：文件目录树、文件与Block的映射、权限等。

持久化方式：`fsimage`（全量快照）+ `editlog`（操作日志）

### HDFS文件写入和读取流程

**写入流程：**

1. Client → NameNode：申请创建文件
2. NameNode返回DataNode列表（DN1→DN2→DN3 流水线）
3. Client将数据切Block，按流水线依次写入（DN1写完传给DN2，DN2传给DN3）
4. 每个packet写完，ack沿流水线反向回传给Client
5. 全部写完，Client通知NameNode完成

**读取流程：**

1. Client → NameNode：请求读文件
2. NameNode返回各Block所在DataNode列表（按距离排序）
3. Client就近选DataNode读取每个Block
4. CRC校验，损坏则自动切换其他副本

### HDFS优缺点及使用场景

- **优点**：高容错、高吞吐（流式读取）、低成本、可扩展
- **缺点**：高延迟、不适合小文件、不支持随机写、不支持并发写
- **使用场景**：日志存储、数据仓库原始数据、离线批处理

### HDFS的容错机制

- **心跳检测**：DataNode超时未发心跳，NameNode触发副本重建
- **CRC校验**：读写时检测数据损坏，自动切换副本
- **多副本**：默认3副本，一个节点坏了不影响数据
- **NameNode HA**：元数据不丢失

### HDFS的副本机制

默认**3副本**放置策略：

- 第1副本：客户端所在节点
- 第2副本：**不同机架**的节点
- 第3副本：与第2副本**同机架**不同节点

兼顾可靠性（跨机架防机架故障）和网络效率。

### HDFS的常见数据格式，列式存储格式和行存储格式异同点，列式存储优点有哪些？

**行存储**：一行数据连续存储，适合OLTP（增删改查整行）

**列式存储**：同一列数据连续存储，适合OLAP（只读少数列的聚合分析）

**列式存储优点：**

- 压缩比高（同列数据类型相同，压缩效果好）
- I/O少（只读需要的列，跳过无关数据）
- 聚合计算快（sum/count等）

常见格式：TextFile（行）、SequenceFile（行）、ORC（列）、Parquet（列）

### HDFS的默认副本数？为什么？如何修改？

默认**3副本**：在可靠性和存储成本之间取平衡（容忍2个节点同时故障）。

修改：

- `hdfs-site.xml` 中 `dfs.replication=3`
- 或命令：`hdfs dfs -setrep -w 2 /path/to/file`

### HDFS的块默认大小，64M和128M是在哪个版本更换的？怎么修改默认块大小？

Hadoop **1.x默认64MB**，**2.x起改为128MB**。

修改：`hdfs-site.xml` 中 `dfs.blocksize=134217728`（单位字节）

### HDFS的block为什么是128M？增大或减小有什么影响？

磁盘寻址约10ms，传输速率约100MB/s，128MB传输约1.28秒，寻址时间占比约1%，效率最优。

- **增大**：Map并行度降低，适合超大文件
- **减小**：Map任务数增多，启动开销大，NameNode元数据增多

### HDFS HA怎么实现？是个什么架构？

见上方"NameNode高可用"部分：Active NN + Standby NN + JournalNode集群 + ZooKeeper + ZKFC

### 导入大文件到HDFS时如何自定义分片？

实现自定义`InputFormat`，重写`getSplits()`方法。或调整参数：

- `mapreduce.input.fileinputformat.split.maxsize`
- `mapreduce.input.fileinputformat.split.minsize`

### HDFS的mapper和reducer的个数如何确定？reducer的个数依据是什么？

- **Mapper数**：由输入Split数决定，一个Split = 一个MapTask（默认Split大小 = Block大小）
- **Reducer数**：手动设置（`job.setNumReduceTasks(n)`），一般设为节点数×1.5~2倍

### HDFS跨节点怎么进行数据迁移

- `hadoop distcp`：分布式拷贝，适合集群间大量数据迁移（推荐）
- 跨集群：`hadoop distcp hdfs://cluster1/path hdfs://cluster2/path`

### HDFS的数据一致性靠什么保证？

- **写入时**：pipeline写入，所有副本ack后才确认写成功
- **读取时**：CRC校验，不一致自动切换副本
- **副本监控**：NameNode持续监控副本数，不足时触发重建

### HDFS怎么保证数据安全

- 多副本（数据冗余）
- CRC校验（检测损坏）
- Kerberos认证（身份验证）
- ACL权限控制（文件级权限）
- 传输加密（TLS）和存储加密（KMS）
- 审计日志

### HDFS写数据过程，写的过程中有哪些故障，分别会怎么处理？

写数据过程见上方"写入流程"。

故障处理：

- **某DataNode宕机**：从pipeline移除，用新DataNode替换，事后补足副本数
- **NameNode宕机（HA模式）**：Standby自动切为Active，Client重连继续写
- **网络超时**：packet重传，超时后报错，Client可重试

### 直接将数据文件上传到HDFS的表目录中，如何在表中查询到该数据？

- **非分区表**：直接可查，Hive会扫描目录下所有文件
- **分区表**：执行 `MSCK REPAIR TABLE 表名;` 刷新分区元数据，或手动 `ALTER TABLE 表名 ADD PARTITION (...)`

---

## ⚙️ MapReduce

> **整体类比：** 统计一本书里每个单词出现多少次
> 
> - **Map** = 把书分给100人，每人数自己那几页的词频，输出(词, 1)
> - **Shuffle** = 把所有"hadoop"汇给同一个人，"spark"汇给另一个人
> - **Reduce** = 每人把收到的同一词的数字加起来，得出最终结果

### 介绍下MapReduce

分布式批处理计算框架，将计算分为两阶段：

- **Map**：对输入数据做转换/过滤，输出KV对
- **Reduce**：对相同key的value做聚合

中间通过**Shuffle**（分区、排序、合并、网络传输）连接两个阶段。

### MapReduce优缺点

- **优点**：简单、高容错、适合超大规模离线批处理
- **缺点**：延迟高（中间结果落磁盘）、不适合实时、不适合迭代计算

### MapReduce工作原理

```
输入文件 → Split切分 → MapTask → 环形缓冲区
→ 溢写（分区+排序）→ 合并 → Shuffle（网络传输）
→ ReduceTask归并排序 → Reduce函数 → 输出文件
```

### MapReduce哪个阶段最费时间

**Shuffle阶段**最耗时：大量磁盘溢写 + 归并排序 + 网络传输。

### MapReduce中的Combine是干嘛的？有什么好处？

在Map端本地预聚合，减少传输到Reduce的数据量。

- 好处：减少网络传输、减轻ReduceTask压力、整体加快
- 要求：操作满足交换律和结合律（✅ sum/max，❌ avg）

### MapReduce为什么一定要有环形缓冲区

Map输出先写内存环形缓冲区（默认100MB），满80%再批量溢写磁盘。

避免每条数据都触发磁盘I/O，批量写效率高得多。环形设计可以边写边溢写，不阻塞。

### MapReduce为什么一定要有Shuffle过程

Map和Reduce之间需要**按key分组**：相同key的数据必须汇聚到同一个ReduceTask处理。Shuffle负责分区→排序→网络传输→归并，没有Shuffle就无法实现分布式聚合。

### MapReduce的Shuffle过程及其优化

**Map端：** Map输出 → 写环形缓冲区 → 满80%溢写（按分区快速排序）→ 多个溢写文件归并合并

**Reduce端：** HTTP拉取各MapTask输出 → 归并排序 → 传给Reducer

**优化：**

- 开启Combiner预聚合，减少传输量
- 压缩Map输出（`mapreduce.map.output.compress=true`，推荐Snappy）
- 调大环形缓冲区（`mapreduce.task.io.sort.mb`）

### Reduce怎么知道去哪里拉Map结果集？

ApplicationMaster追踪所有MapTask完成情况和输出位置。ReduceTask定期询问AM，获取已完成MapTask的输出位置（Host+端口），通过HTTP主动拉取。

### Reduce阶段都发生了什么，有没有进行分组

1. **拉取数据**：从各MapTask HTTP拉取属于本Reducer的分区数据
2. **归并排序**：将多份数据归并排序（相同key相邻）
3. **分组**：相同key的所有value形成一个Iterable（**有分组**）
4. **调用Reduce函数**：对每个key的value集合执行用户逻辑
5. **输出**：写入HDFS

### MapReduce Shuffle的排序算法

- **Map端溢写**：快速排序
- **Map端合并溢写文件**：归并排序
- **Reduce端合并拉取数据**：归并排序

### shuffle为什么要排序？

排序使相同key的数据**相邻**，Reduce端分组只需顺序扫描，无需额外哈希表，内存占用低，效率高。

### 说一下map是怎么到reduce的？

Map输出 → 写环形缓冲区 → 按分区排序 → 溢写磁盘 → 归并合并成一个有序文件 → Reduce通过HTTP拉取 → 归并排序 → 传给Reducer

### MapReduce的数据处理过程

Input → InputFormat切分 → RecordReader读取KV → Map函数 → Partitioner分区 → 排序 → Combiner（可选）→ Shuffle → Reduce函数 → OutputFormat → Output

### mapjoin的原理？应用场景？

**原理：** 将小表通过DistributedCache广播到所有MapTask的内存中，Map阶段直接与大表做join，**无需Reduce和Shuffle**。

> 类比：把城市编码表打印一份给每个工人，工人本地查表，不用汇总给主管。

**应用场景：** 大表 join 小表（小表能装入内存，如几百MB以内），可完全避免数据倾斜。

### reducejoin如何执行（原理）

1. 两张表数据都打上标记（标注来自哪张表）
2. 以join key为Map输出key，相同key的数据到同一Reducer
3. Reducer中按标记区分两张表，做匹配

缺点：所有数据都要Shuffle，数据量大时可能数据倾斜，性能不如MapJoin。

### MapReduce为什么不能产生过多小文件

- 每个小文件对应一个MapTask，JVM启动开销远大于实际计算
- 大量小文件消耗NameNode内存（每文件约150字节元数据）

### MapReduce分区及作用

分区决定Map输出的KV数据发送到哪个ReduceTask。

默认：`HashPartitioner`：`key.hashCode() % numReduceTasks`

保证相同key一定到同一Reducer。可自定义Partitioner实现业务分区。

### ReduceTask数量和分区数量关系

- ReduceTask == 分区数：✅ 正常
- ReduceTask > 分区数：多余的Task空转，产生空文件
- ReduceTask < 分区数：❌ 报错，部分分区数据无处写入

### Map的分片有多大

默认分片大小 = Block大小（128MB）。

分片大小 = `max(minSize, min(maxSize, blockSize))`

### reduce任务什么时候开始？

- **Shuffle拉取数据**：5%的MapTask完成后就开始拉
- **Reduce真正计算**：等所有MapTask完成后才开始

### MapReduce用了几次排序，分别是什么？

共**3次**：

1. **Map端溢写时**：快速排序（对缓冲区内数据）
2. **Map端合并溢写文件时**：归并排序
3. **Reduce端合并拉取数据时**：归并排序

### MapReduce怎么确定MapTask的数量？Map数量由什么决定

MapTask数量 = 输入数据的**Split数量**，一个Split对应一个MapTask。

Split数 = 输入文件大小 / 分片大小（默认=Block大小128MB）

小文件多时，每个文件至少一个Split，MapTask数会爆炸。

### MapReduce作业执行过程中，中间数据存在什么地方？

存在**本地磁盘**（非HDFS）。

Map输出先写内存环形缓冲区（100MB），超过80%溢写到**本地磁盘**，最终合并成本地文件。Reduce拉取后也先写本地磁盘归并，再传给Reducer计算。

### map输出数据超出缓冲区后，落地到磁盘还是HDFS？

**本地磁盘**（不是HDFS）。中间数据走本地磁盘效率更高，HDFS是最终输入输出用的。

### Map到Reduce默认的分区机制是什么？

默认`HashPartitioner`：`(key.hashCode() & Integer.MAX_VALUE) % numReduceTasks`

### MapReduce数据倾斜产生的原因及其解决方案

**原因：** key分布不均，某些key数据量远大于其他，对应Reducer处理时间远长。

> 类比：100人统计词频，"的"字出现100万次全汇给一个人，这人累死其他人都完了。

**解决方案：**

- **MapJoin**：小表广播内存，避免Reduce阶段（最彻底）
- **key加随机前缀**：打散热点key（加1-100随机数前缀），聚合后再二次聚合
- **自定义Partitioner**：将热点key均匀分配
- **Combiner预聚合**：减少传到Reducer的数据
- **过滤NULL或异常key**：提前过滤无效数据

### Map Join为什么能解决数据倾斜

MapJoin完全在Map端完成join，**没有Shuffle没有Reduce**，每个MapTask独立处理一部分数据并查询内存中的小表，数据天然均衡，不存在某节点数据集中的问题。

### MapReduce运行过程中会发生OOM，OOM发生的位置？

- **Map端**：环形缓冲区设置过大，或Map逻辑缓存了太多数据
- **Reduce端**：归并数据时内存不足，或Reduce逻辑缓存太多

解决：调大 `mapreduce.map/reduce.memory.mb` 和对应JVM堆内存参数。

### MapReduce压缩方式

- **Map输出压缩**：减少Shuffle传输量，推荐Snappy（快）
- **最终输出压缩**：减少HDFS存储，推荐Bzip2（可切分）或Gzip

配置：`mapreduce.map.output.compress=true`

### MapReduce中怎么处理一个大文件

- 确保文件**可切分**（避免不可切分的Gzip压缩）
- 使用`FileInputFormat`按Block自动切分
- 调大Map内存和超时时间
- 开启Combiner和Map输出压缩

---

## 🎯 YARN

> **整体类比：** 工厂人力资源部
> 
> - **ResourceManager** = 人事总监（管全厂资源）
> - **NodeManager** = 各车间主任（管自己车间）
> - **ApplicationMaster** = 项目经理（管一个具体项目，向总监要资源）
> - **Container** = 一个工位（固定CPU+内存）

### 介绍下YARN

YARN（Yet Another Resource Negotiator）是Hadoop的资源管理框架，将资源管理和作业调度分离，支持多计算框架（MapReduce/Spark/Flink）共享集群资源。

### YARN有几个模块

4个核心模块：

- **ResourceManager（RM）**：全局资源管理
- **NodeManager（NM）**：单节点资源管理
- **ApplicationMaster（AM）**：每个应用独立，申请资源+任务调度
- **Container**：资源封装单元（CPU + 内存）

### YARN工作机制

1. Client向RM提交应用
2. RM分配Container，启动AM（项目经理上班）
3. AM评估需要多少资源，向RM申请Container列表
4. RM分配Container，AM通知对应NM启动Container执行任务
5. 任务完成，AM向RM注销，资源释放

### YARN有什么优势，能解决什么问题？

解决Hadoop 1.x的JobTracker单点瓶颈（同时负责资源管理和任务调度）。

YARN优势：

- 职责分离，RM专注资源，AM专注应用
- 支持多框架共享集群（MR/Spark/Flink）
- 更好的扩展性（支持数万节点）

### YARN容错机制

- **RM故障**：ZooKeeper实现RM HA，Standby自动接管
- **NM故障**：RM检测到心跳超时，将该节点任务重新调度
- **AM故障**：RM重新启动AM（默认重试2次）
- **Container/Task故障**：AM检测到，重新申请Container重跑

### YARN高可用

Active RM + Standby RM + ZooKeeper（选主+状态存储）

Active故障时Standby自动切换。

### YARN调度器

同Hadoop调度器：FIFO / CapacityScheduler（默认）/ FairScheduler

### YARN中Container是如何启动的？

1. AM向RM申请到Container（包含Host、资源量）
2. AM直接联系对应NM，发送启动命令（包含命令、环境变量、资源文件）
3. NM在本地启动Container进程，设置CPU/内存限制（cgroups）
4. Container向AM汇报状态

### YARN的改进之处，Hadoop3.x相对于Hadoop 2.x？

- 支持GPU/FPGA资源调度
- Opportunistic Container（低优先级抢占式Container，提高利用率）
- 更好的RM HA
- Timeline Service v2（更好的监控和历史记录）

---

## 综合问题

### 为什么Spark比MapReduce快？

|      | MapReduce     | Spark       |
| ---- | ------------- | ----------- |
| 中间结果 | 每步落磁盘         | 放内存         |
| 类比   | 每算完一步存档，下步再读档 | 一直在内存算，最后才存 |
| 速度   | 慢             | 快10-100倍    |

磁盘比内存慢100倍以上，所以Spark快很多。另外Spark用DAG优化执行计划，减少不必要的shuffle。

### 宽依赖窄依赖

- **窄依赖**：父RDD每个分区只被子RDD**一个**分区使用（如map、filter）→ 可pipeline，不需要shuffle
- **宽依赖**：父RDD每个分区被子RDD**多个**分区使用（如groupByKey、join）→ 需要shuffle，是stage划分边界

> 类比：窄依赖 = 一个工人负责一道工序（流水线）；宽依赖 = 所有工人的结果都要汇总再重新分配（需要等待）

### 是否遇到过数据倾斜问题？如何解决的

症状：大多数Task很快完成，少数Task卡住很久。

排查：看Spark UI，找数据量异常大的Task。

解决：

1. 过滤NULL或异常key
2. 大表join小表用MapJoin（广播小表）
3. 热点key加随机前缀打散，聚合后去掉前缀二次聚合
4. 增大shuffle分区数（`spark.sql.shuffle.partitions`）
5. Spark 3.x开启AQE（自适应查询执行）自动处理

### Spark的shuffle有几种方式

- **HashShuffle**（已废弃）：按key哈希写文件，文件数=Map数×Reduce数，文件太多
- **SortShuffle**（默认）：先排序再写一个文件+索引，文件数=Map数，效率更高
- **TungstenSortShuffle**：SortShuffle优化版，使用堆外内存，减少GC

### Hadoop和Spark的主要区别。Spark为什么更有优势？

|      | Hadoop MR       | Spark                |
| ---- | --------------- | -------------------- |
| 计算模型 | 两阶段（Map+Reduce） | DAG多阶段               |
| 中间数据 | 落HDFS磁盘         | 内存（必要时spill磁盘）       |
| 速度   | 慢               | 快10-100倍             |
| 编程模型 | 只有Map/Reduce，复杂 | RDD/DataFrame/SQL，丰富 |
| 适合场景 | 超大规模单次批处理       | 迭代计算、交互查询、流处理        |

**数据超内存时**：Spark自动将RDD分区spill到本地磁盘，性能降低但仍可工作。

### 你如何进行大数据平台的性能调优？

1. **存储层**：列式存储（ORC/Parquet）+压缩，合并小文件
2. **计算层**：合理设置并行度，用MapJoin，开启Combiner
3. **资源配置**：合理分配内存/CPU，调整JVM参数
4. **SQL优化**：谓词下推、分区裁剪、避免SELECT *、减少shuffle
5. **数据倾斜**：加盐打散、广播join
6. **监控定位**：Spark UI/YARN UI找瓶颈任务

### 一个Hive SQL或Spark任务运行很慢，你会从哪些方面排查？

1. **执行计划**：`EXPLAIN`，看是否全表扫描、缺少分区裁剪
2. **数据倾斜**：看各Task数据量是否均匀（Spark UI）
3. **小文件**：Map数过多，每个Task数据量极小
4. **Shuffle量**：是否Shuffle了大量数据
5. **资源**：是否频繁GC，内存是否够用
6. **Join策略**：大表join是否可改为MapJoin

### 对实时流处理的理解。用过哪些流处理框架？

实时流处理：对持续产生的数据流做低延迟处理，相对批处理的T+1，可达秒级甚至毫秒级。

|      | Spark Streaming | Flink           |
| ---- | --------------- | --------------- |
| 处理方式 | 微批（把流切成小批次）     | 真流（逐条处理）        |
| 延迟   | 秒级              | 毫秒级             |
| 吞吐量  | 高               | 高               |
| 语义   | At-Least-Once为主 | Exactly-Once    |
| 适合   | 对延迟要求不极致，吞吐高    | 低延迟、精确计算（对账、风控） |

### 在大数据开发中，如何管理数据权限和保障数据安全？

- **认证**：Kerberos（确保只有合法用户可访问）
- **授权**：Apache Ranger（表/列/行级别细粒度权限控制）
- **传输加密**：TLS/SSL
- **存储加密**：HDFS透明加密（KMS管理密钥）
- **数据脱敏**：敏感字段（手机号、身份证）在查询层脱敏
- **审计日志**：记录所有访问操作，便于追溯

---

## 数据湖

### 你了解数据湖、数据湖仓一体这些概念吗？它们与传统数据仓库相比有何演进？

|      | 数据仓库                    | 数据湖                  | 湖仓一体（Lakehouse）             |
| ---- | ----------------------- | -------------------- | --------------------------- |
| 类比   | 整理好的档案室                 | 什么都往里扔的储物间           | 智能储物室（存得下又找得到）              |
| 数据格式 | 只存结构化                   | 任意格式                 | 任意格式                        |
| 写入方式 | Schema-on-Write（写时定义结构） | Schema-on-Read（读时定义） | Schema-on-Write（有管理）        |
| 查询   | 快，有索引                   | 慢，无组织                | 快（有索引+统计信息）                 |
| 成本   | 贵                       | 便宜（对象存储）             | 便宜                          |
| ACID | 支持                      | 不支持                  | 支持（Delta Lake/Hudi/Iceberg） |
| 缺点   | 灵活性差，不支持非结构化            | 容易变"数据沼泽"，难治理        | 相对复杂                        |

**演进路径：** 数仓（贵但好用）→ 数据湖（便宜但难用）→ 湖仓一体（既便宜又好用）

代表技术：Delta Lake（Databricks）、Apache Hudi（Uber）、Apache Iceberg（Netflix）[大数据面试题V3.0，约870篇牛客大数据面经480道面试题_牛客网](https://www.nowcoder.com/discuss/353159520220291072)

https://zhuanlan.zhihu.com/p/424296249 [大数据开发面经汇总【持续更新...】_牛客网](https://www.nowcoder.com/discuss/594817738107781120)

https://leetcode.cn/discuss/post/3516212/zi-jie-mian-jing-nian-xin-70wda-shu-ju-s-23r7/

[大数据开发面经_大数据面经-CSDN博客](https://blog.csdn.net/axzy5863/article/details/158429145)

[大数据开发（牛客）面试被问频率最高的几道面试题-腾讯云开发者社区-腾讯云](https://cloud.tencent.com/developer/article/2071876)

---

## 🐘 Hadoop整体理解

把Hadoop想象成一个**超大的仓库管理系统**：

- **HDFS** = 仓库（存东西）
- **MapReduce** = 工人（干活）
- **YARN** = 仓库主管（分配工人和资源）

---

## Hadoop基础

### 什么是Hadoop调度器？说明其工作方法

Hadoop 调度器（Hadoop Scheduler）通常指 Hadoop YARN （Yet Another Resource Negotiator） 中的资源调度组件，负责决定 集群中的 CPU、内存等计算资源如何分配给各个应用程序（如 MapReduce、Spark、Hive 任务）。当多个用户或任务同时提交作业时，调度器决定谁先运行、谁使用多少资源、资源如何公平分配。

没有调度器的话：所有任务都在抢资源、可能有的任务占满集群、其他任务一直等待
三种调度器：

| 调度器               | 机制   | 适用场景 |
| ----------------- | ---- | ---- |
| FIFO              | 先进先出 |      |
| CapacityScheduler |      |      |
| FairScheduler     |      |      |

- **FIFO**：先进先出，按提交顺序排队执行，简单但资源利用率低
- **CapacityScheduler（默认）**：多队列，按队列容量分配资源，优先级高、占资源少的先跑
- **FairScheduler**：同一队列内所有作业公平共享资源，动态均衡

### hadoop框架的理解、Hadoop的特点

Hadoop = **HDFS**（分布式存储）+ **MapReduce**（分布式计算）+ **YARN**（资源管理）

特点：**高可靠**（多副本容错）、**高扩展**（加机器就能扩容）、**高容错**（节点挂了自动恢复）、**低成本**（普通硬件即可）

### Hadoop生态圈组件及其作用

| 组件        | 作用                     |
| --------- | ---------------------- |
| HDFS      | 分布式文件存储                |
| MapReduce | 分布式批处理计算               |
| YARN      | 资源调度与管理                |
| Hive      | SQL查询工具（SQL转MapReduce） |
| HBase     | 分布式列式NoSQL数据库          |
| ZooKeeper | 分布式协调服务（选主、配置管理）       |
| Kafka     | 高吞吐消息队列                |
| Flume     | 日志采集                   |
| Sqoop     | 关系型数据库与HDFS互导          |
| Spark     | 内存计算引擎，比MR快            |

### Hadoop 1.x，2.x，3.x的区别

- **1.x**：JobTracker同时负责资源管理和任务调度，单点瓶颈；没有HA
- **2.x**：引入YARN把资源管理分出去；HDFS支持NameNode HA和Federation
- **3.x**：支持多个NameNode；引入**纠删码（EC）**替代副本节省存储约50%；支持GPU资源调度

### Hadoop集群工作时启动哪些进程？它们有什么作用？

- **NameNode**：管理HDFS元数据（文件在哪、有几个副本），不存实际数据
- **DataNode**：存储实际数据块，定期向NameNode发心跳汇报状态
- **ResourceManager**：管整个集群资源，接受Job提交，分配资源
- **NodeManager**：管单个节点资源，启动和监控Container
- **SecondaryNameNode**（非HA模式）：辅助NameNode合并日志，**不是**NameNode备份

### 在集群计算的时候，什么是集群的主要瓶颈

**磁盘I/O**是主要瓶颈，尤其是MapReduce的Shuffle阶段（大量数据溢写磁盘+网络传输）。其次是**网络带宽**。

### 搭建Hadoop集群的xml文件有哪些？

- `core-site.xml`：核心配置（HDFS地址等）
- `hdfs-site.xml`：HDFS配置（副本数、块大小等）
- `mapred-site.xml`：MapReduce配置
- `yarn-site.xml`：YARN配置

### Hadoop的checkpoint流程

> **类比：** 就像把流水账（editlog）定期整理成账本快照（fsimage），防止流水账越来越长。

1. SecondaryNameNode从NameNode拉取editlog和fsimage
2. 将editlog回放合并到fsimage，生成新fsimage
3. 将新fsimage推回NameNode，清空旧editlog

作用：防止editlog无限增长，加快NameNode重启速度。

### Hadoop的默认块大小是多少？为什么设置这么大？

默认**128MB**（Hadoop 2.x起）。

原因：磁盘寻址时间约10ms，传输速率约100MB/s，128MB传输约1.28秒，寻址时间占比约1%，效率最优。

- 太小 → Map任务数多，启动开销大
- 太大 → Map并行度低

### Block划分的原因

- 大文件切块后可**多节点并行处理**
- Block分散到各DataNode，**负载均衡**
- 单个Block损坏只需恢复该Block，**容错代价小**

### Hadoop常见的压缩算法？

| 算法     | 是否可切分   | 速度  | 压缩比 | 适用场景       |
| ------ | ------- | --- | --- | ---------- |
| Gzip   | ❌       | 中   | 高   | 冷数据存储      |
| Bzip2  | ✅       | 慢   | 最高  | 需切分的归档     |
| Snappy | ❌       | 最快  | 中   | Map输出、中间数据 |
| LZO    | ✅（需建索引） | 快   | 中   | 大文件、需切分场景  |

> 注意：不可切分的压缩格式（如Gzip）大文件只能一个Map处理，并行度差。

### Hadoop作业提交到YARN的流程？

1. Client向ResourceManager提交Job（上传JAR到HDFS）
2. RM分配Container，启动**ApplicationMaster**
3. AM向RM申请运行MapTask/ReduceTask的Container
4. AM联系NodeManager，在Container中启动任务
5. 任务完成，AM向RM注销，资源释放

### Hadoop的Combiner的作用

在**Map端本地预聚合**，减少传输到Reduce的数据量。

> **类比：** 100人统计词频，传纸条前先自己合并，传"hadoop:50"而不是50张"hadoop:1"。

要求操作满足交换律和结合律：✅ sum/max/min，❌ avg（会丢信息）

### Hadoop序列化和反序列化

Hadoop用`Writable`接口（非Java原生序列化），更紧凑高效，节省带宽。

常用类型：`IntWritable`、`LongWritable`、`Text`、`NullWritable`

### Hadoop的运行模式

- **本地模式**：单机单JVM，无HDFS，用于开发调试
- **伪分布式**：单机模拟集群
- **完全分布式**：多节点，生产环境

### Hadoop小文件处理问题

**问题：** 每个小文件占NameNode约150字节内存；每个小文件启动一个MapTask，启动开销远大于计算本身。

**解决：**

- **CombineFileInputFormat**：合并小文件再处理
- **SequenceFile**：将小文件以KV形式合并存储
- **HAR归档**：打包小文件
- 上游控制，避免产生小文件（如Hive设置合并输出）

### Hadoop为什么要从2.x升级到3.x？

- **纠删码**：存储开销从200%降至约50%，节省大量存储成本
- **多NameNode**：突破单NameNode扩展瓶颈
- **支持GPU/FPGA**资源调度

### Hadoop的优缺点

- **优点**：高容错、低成本、高扩展、适合PB级批量处理
- **缺点**：延迟高（不适合实时）、小文件问题、不支持随机写、不适合迭代计算

---

## 📦 HDFS

> **整体类比：** 图书馆管理系统
> 
> - NameNode = 图书馆目录（记录书在哪，但不存书）
> - DataNode = 书架（真正放书的地方）
> - Block = 把大书撕成若干份（128MB一份）
> - 副本数3 = 每份复印3本放不同书架，防止丢失

### HDFS NameNode高可用如何实现？需要哪些角色？

架构：**Active NameNode + Standby NameNode**

| 角色                 | 作用                           |
| ------------------ | ---------------------------- |
| Active NameNode    | 对外提供服务                       |
| Standby NameNode   | 热备，实时同步editlog               |
| JournalNode集群（≥3个） | 共享editlog，Active写入，Standby读取 |
| ZooKeeper          | 选主，记录谁是Active                |
| ZKFC               | 监控NameNode健康，触发自动切换          |

### HDFS中向DataNode写数据失败了怎么办

1. 将失败的DataNode从pipeline中移除
2. 已写数据标记为损坏
3. NameNode重新分配新DataNode，重建pipeline继续写
4. 写完后NameNode发现副本数不足，触发后台重新复制

### DataNode什么情况下不会备份

强制关闭或非正常断电时。

### HDFS中DataNode怎么存储数据的

- 数据以**Block文件**存在本地磁盘
- 每个Block对应一个`.meta`校验文件（CRC）
- DataNode每3秒向NameNode发**心跳**，每6小时发**块报告**

### NameNode存数据吗？

**不存实际数据**，只存**元数据**：文件目录树、文件与Block的映射、权限等。

持久化方式：`fsimage`（全量快照）+ `editlog`（操作日志）

### HDFS文件写入和读取流程

**写入流程：**

1. Client → NameNode：申请创建文件
2. NameNode返回DataNode列表（DN1→DN2→DN3 流水线）
3. Client将数据切Block，按流水线依次写入（DN1写完传给DN2，DN2传给DN3）
4. 每个packet写完，ack沿流水线反向回传给Client
5. 全部写完，Client通知NameNode完成

**读取流程：**

1. Client → NameNode：请求读文件
2. NameNode返回各Block所在DataNode列表（按距离排序）
3. Client就近选DataNode读取每个Block
4. CRC校验，损坏则自动切换其他副本

### HDFS优缺点及使用场景

- **优点**：高容错、高吞吐（流式读取）、低成本、可扩展
- **缺点**：高延迟、不适合小文件、不支持随机写、不支持并发写
- **使用场景**：日志存储、数据仓库原始数据、离线批处理

### HDFS的容错机制

- **心跳检测**：DataNode超时未发心跳，NameNode触发副本重建
- **CRC校验**：读写时检测数据损坏，自动切换副本
- **多副本**：默认3副本，一个节点坏了不影响数据
- **NameNode HA**：元数据不丢失

### HDFS的副本机制

默认**3副本**放置策略：

- 第1副本：客户端所在节点
- 第2副本：**不同机架**的节点
- 第3副本：与第2副本**同机架**不同节点

兼顾可靠性（跨机架防机架故障）和网络效率。

### HDFS的常见数据格式，列式存储格式和行存储格式异同点，列式存储优点有哪些？

**行存储**：一行数据连续存储，适合OLTP（增删改查整行）

**列式存储**：同一列数据连续存储，适合OLAP（只读少数列的聚合分析）

**列式存储优点：**

- 压缩比高（同列数据类型相同，压缩效果好）
- I/O少（只读需要的列，跳过无关数据）
- 聚合计算快（sum/count等）

常见格式：TextFile（行）、SequenceFile（行）、ORC（列）、Parquet（列）

### HDFS的默认副本数？为什么？如何修改？

默认**3副本**：在可靠性和存储成本之间取平衡（容忍2个节点同时故障）。

修改：

- `hdfs-site.xml` 中 `dfs.replication=3`
- 或命令：`hdfs dfs -setrep -w 2 /path/to/file`

### HDFS的块默认大小，64M和128M是在哪个版本更换的？怎么修改默认块大小？

Hadoop **1.x默认64MB**，**2.x起改为128MB**。

修改：`hdfs-site.xml` 中 `dfs.blocksize=134217728`（单位字节）

### HDFS的block为什么是128M？增大或减小有什么影响？

磁盘寻址约10ms，传输速率约100MB/s，128MB传输约1.28秒，寻址时间占比约1%，效率最优。

- **增大**：Map并行度降低，适合超大文件
- **减小**：Map任务数增多，启动开销大，NameNode元数据增多

### HDFS HA怎么实现？是个什么架构？

见上方"NameNode高可用"部分：Active NN + Standby NN + JournalNode集群 + ZooKeeper + ZKFC

### 导入大文件到HDFS时如何自定义分片？

实现自定义`InputFormat`，重写`getSplits()`方法。或调整参数：

- `mapreduce.input.fileinputformat.split.maxsize`
- `mapreduce.input.fileinputformat.split.minsize`

### HDFS的mapper和reducer的个数如何确定？reducer的个数依据是什么？

- **Mapper数**：由输入Split数决定，一个Split = 一个MapTask（默认Split大小 = Block大小）
- **Reducer数**：手动设置（`job.setNumReduceTasks(n)`），一般设为节点数×1.5~2倍

### HDFS跨节点怎么进行数据迁移

- `hadoop distcp`：分布式拷贝，适合集群间大量数据迁移（推荐）
- 跨集群：`hadoop distcp hdfs://cluster1/path hdfs://cluster2/path`

### HDFS的数据一致性靠什么保证？

- **写入时**：pipeline写入，所有副本ack后才确认写成功
- **读取时**：CRC校验，不一致自动切换副本
- **副本监控**：NameNode持续监控副本数，不足时触发重建

### HDFS怎么保证数据安全

- 多副本（数据冗余）
- CRC校验（检测损坏）
- Kerberos认证（身份验证）
- ACL权限控制（文件级权限）
- 传输加密（TLS）和存储加密（KMS）
- 审计日志

### HDFS写数据过程，写的过程中有哪些故障，分别会怎么处理？

写数据过程见上方"写入流程"。

故障处理：

- **某DataNode宕机**：从pipeline移除，用新DataNode替换，事后补足副本数
- **NameNode宕机（HA模式）**：Standby自动切为Active，Client重连继续写
- **网络超时**：packet重传，超时后报错，Client可重试

### 直接将数据文件上传到HDFS的表目录中，如何在表中查询到该数据？

- **非分区表**：直接可查，Hive会扫描目录下所有文件
- **分区表**：执行 `MSCK REPAIR TABLE 表名;` 刷新分区元数据，或手动 `ALTER TABLE 表名 ADD PARTITION (...)`

---

## ⚙️ MapReduce

> **整体类比：** 统计一本书里每个单词出现多少次
> 
> - **Map** = 把书分给100人，每人数自己那几页的词频，输出(词, 1)
> - **Shuffle** = 把所有"hadoop"汇给同一个人，"spark"汇给另一个人
> - **Reduce** = 每人把收到的同一词的数字加起来，得出最终结果

### 介绍下MapReduce

分布式批处理计算框架，将计算分为两阶段：

- **Map**：对输入数据做转换/过滤，输出KV对
- **Reduce**：对相同key的value做聚合

中间通过**Shuffle**（分区、排序、合并、网络传输）连接两个阶段。

### MapReduce优缺点

- **优点**：简单、高容错、适合超大规模离线批处理
- **缺点**：延迟高（中间结果落磁盘）、不适合实时、不适合迭代计算

### MapReduce工作原理

```
输入文件 → Split切分 → MapTask → 环形缓冲区
→ 溢写（分区+排序）→ 合并 → Shuffle（网络传输）
→ ReduceTask归并排序 → Reduce函数 → 输出文件
```

### MapReduce哪个阶段最费时间

**Shuffle阶段**最耗时：大量磁盘溢写 + 归并排序 + 网络传输。

### MapReduce中的Combine是干嘛的？有什么好处？

在Map端本地预聚合，减少传输到Reduce的数据量。

- 好处：减少网络传输、减轻ReduceTask压力、整体加快
- 要求：操作满足交换律和结合律（✅ sum/max，❌ avg）

### MapReduce为什么一定要有环形缓冲区

Map输出先写内存环形缓冲区（默认100MB），满80%再批量溢写磁盘。

避免每条数据都触发磁盘I/O，批量写效率高得多。环形设计可以边写边溢写，不阻塞。

### MapReduce为什么一定要有Shuffle过程

Map和Reduce之间需要**按key分组**：相同key的数据必须汇聚到同一个ReduceTask处理。Shuffle负责分区→排序→网络传输→归并，没有Shuffle就无法实现分布式聚合。

### MapReduce的Shuffle过程及其优化

**Map端：** Map输出 → 写环形缓冲区 → 满80%溢写（按分区快速排序）→ 多个溢写文件归并合并

**Reduce端：** HTTP拉取各MapTask输出 → 归并排序 → 传给Reducer

**优化：**

- 开启Combiner预聚合，减少传输量
- 压缩Map输出（`mapreduce.map.output.compress=true`，推荐Snappy）
- 调大环形缓冲区（`mapreduce.task.io.sort.mb`）

### Reduce怎么知道去哪里拉Map结果集？

ApplicationMaster追踪所有MapTask完成情况和输出位置。ReduceTask定期询问AM，获取已完成MapTask的输出位置（Host+端口），通过HTTP主动拉取。

### Reduce阶段都发生了什么，有没有进行分组

1. **拉取数据**：从各MapTask HTTP拉取属于本Reducer的分区数据
2. **归并排序**：将多份数据归并排序（相同key相邻）
3. **分组**：相同key的所有value形成一个Iterable（**有分组**）
4. **调用Reduce函数**：对每个key的value集合执行用户逻辑
5. **输出**：写入HDFS

### MapReduce Shuffle的排序算法

- **Map端溢写**：快速排序
- **Map端合并溢写文件**：归并排序
- **Reduce端合并拉取数据**：归并排序

### shuffle为什么要排序？

排序使相同key的数据**相邻**，Reduce端分组只需顺序扫描，无需额外哈希表，内存占用低，效率高。

### 说一下map是怎么到reduce的？

Map输出 → 写环形缓冲区 → 按分区排序 → 溢写磁盘 → 归并合并成一个有序文件 → Reduce通过HTTP拉取 → 归并排序 → 传给Reducer

### MapReduce的数据处理过程

Input → InputFormat切分 → RecordReader读取KV → Map函数 → Partitioner分区 → 排序 → Combiner（可选）→ Shuffle → Reduce函数 → OutputFormat → Output

### mapjoin的原理？应用场景？

**原理：** 将小表通过DistributedCache广播到所有MapTask的内存中，Map阶段直接与大表做join，**无需Reduce和Shuffle**。

> 类比：把城市编码表打印一份给每个工人，工人本地查表，不用汇总给主管。

**应用场景：** 大表 join 小表（小表能装入内存，如几百MB以内），可完全避免数据倾斜。

### reducejoin如何执行（原理）

1. 两张表数据都打上标记（标注来自哪张表）
2. 以join key为Map输出key，相同key的数据到同一Reducer
3. Reducer中按标记区分两张表，做匹配

缺点：所有数据都要Shuffle，数据量大时可能数据倾斜，性能不如MapJoin。

### MapReduce为什么不能产生过多小文件

- 每个小文件对应一个MapTask，JVM启动开销远大于实际计算
- 大量小文件消耗NameNode内存（每文件约150字节元数据）

### MapReduce分区及作用

分区决定Map输出的KV数据发送到哪个ReduceTask。

默认：`HashPartitioner`：`key.hashCode() % numReduceTasks`

保证相同key一定到同一Reducer。可自定义Partitioner实现业务分区。

### ReduceTask数量和分区数量关系

- ReduceTask == 分区数：✅ 正常
- ReduceTask > 分区数：多余的Task空转，产生空文件
- ReduceTask < 分区数：❌ 报错，部分分区数据无处写入

### Map的分片有多大

默认分片大小 = Block大小（128MB）。

分片大小 = `max(minSize, min(maxSize, blockSize))`

### reduce任务什么时候开始？

- **Shuffle拉取数据**：5%的MapTask完成后就开始拉
- **Reduce真正计算**：等所有MapTask完成后才开始

### MapReduce用了几次排序，分别是什么？

共**3次**：

1. **Map端溢写时**：快速排序（对缓冲区内数据）
2. **Map端合并溢写文件时**：归并排序
3. **Reduce端合并拉取数据时**：归并排序

### MapReduce怎么确定MapTask的数量？Map数量由什么决定

MapTask数量 = 输入数据的**Split数量**，一个Split对应一个MapTask。

Split数 = 输入文件大小 / 分片大小（默认=Block大小128MB）

小文件多时，每个文件至少一个Split，MapTask数会爆炸。

### MapReduce作业执行过程中，中间数据存在什么地方？

存在**本地磁盘**（非HDFS）。

Map输出先写内存环形缓冲区（100MB），超过80%溢写到**本地磁盘**，最终合并成本地文件。Reduce拉取后也先写本地磁盘归并，再传给Reducer计算。

### map输出数据超出缓冲区后，落地到磁盘还是HDFS？

**本地磁盘**（不是HDFS）。中间数据走本地磁盘效率更高，HDFS是最终输入输出用的。

### Map到Reduce默认的分区机制是什么？

默认`HashPartitioner`：`(key.hashCode() & Integer.MAX_VALUE) % numReduceTasks`

### MapReduce数据倾斜产生的原因及其解决方案

**原因：** key分布不均，某些key数据量远大于其他，对应Reducer处理时间远长。

> 类比：100人统计词频，"的"字出现100万次全汇给一个人，这人累死其他人都完了。

**解决方案：**

- **MapJoin**：小表广播内存，避免Reduce阶段（最彻底）
- **key加随机前缀**：打散热点key（加1-100随机数前缀），聚合后再二次聚合
- **自定义Partitioner**：将热点key均匀分配
- **Combiner预聚合**：减少传到Reducer的数据
- **过滤NULL或异常key**：提前过滤无效数据

### Map Join为什么能解决数据倾斜

MapJoin完全在Map端完成join，**没有Shuffle没有Reduce**，每个MapTask独立处理一部分数据并查询内存中的小表，数据天然均衡，不存在某节点数据集中的问题。

### MapReduce运行过程中会发生OOM，OOM发生的位置？

- **Map端**：环形缓冲区设置过大，或Map逻辑缓存了太多数据
- **Reduce端**：归并数据时内存不足，或Reduce逻辑缓存太多

解决：调大 `mapreduce.map/reduce.memory.mb` 和对应JVM堆内存参数。

### MapReduce压缩方式

- **Map输出压缩**：减少Shuffle传输量，推荐Snappy（快）
- **最终输出压缩**：减少HDFS存储，推荐Bzip2（可切分）或Gzip

配置：`mapreduce.map.output.compress=true`

### MapReduce中怎么处理一个大文件

- 确保文件**可切分**（避免不可切分的Gzip压缩）
- 使用`FileInputFormat`按Block自动切分
- 调大Map内存和超时时间
- 开启Combiner和Map输出压缩

---

## 🎯 YARN

> **整体类比：** 工厂人力资源部
> 
> - **ResourceManager** = 人事总监（管全厂资源）
> - **NodeManager** = 各车间主任（管自己车间）
> - **ApplicationMaster** = 项目经理（管一个具体项目，向总监要资源）
> - **Container** = 一个工位（固定CPU+内存）

### 介绍下YARN

YARN（Yet Another Resource Negotiator）是Hadoop的资源管理框架，将资源管理和作业调度分离，支持多计算框架（MapReduce/Spark/Flink）共享集群资源。

### YARN有几个模块

4个核心模块：

- **ResourceManager（RM）**：全局资源管理
- **NodeManager（NM）**：单节点资源管理
- **ApplicationMaster（AM）**：每个应用独立，申请资源+任务调度
- **Container**：资源封装单元（CPU + 内存）

### YARN工作机制

1. Client向RM提交应用
2. RM分配Container，启动AM（项目经理上班）
3. AM评估需要多少资源，向RM申请Container列表
4. RM分配Container，AM通知对应NM启动Container执行任务
5. 任务完成，AM向RM注销，资源释放

### YARN有什么优势，能解决什么问题？

解决Hadoop 1.x的JobTracker单点瓶颈（同时负责资源管理和任务调度）。

YARN优势：

- 职责分离，RM专注资源，AM专注应用
- 支持多框架共享集群（MR/Spark/Flink）
- 更好的扩展性（支持数万节点）

### YARN容错机制

- **RM故障**：ZooKeeper实现RM HA，Standby自动接管
- **NM故障**：RM检测到心跳超时，将该节点任务重新调度
- **AM故障**：RM重新启动AM（默认重试2次）
- **Container/Task故障**：AM检测到，重新申请Container重跑

### YARN高可用

Active RM + Standby RM + ZooKeeper（选主+状态存储）

Active故障时Standby自动切换。

### YARN调度器

同Hadoop调度器：FIFO / CapacityScheduler（默认）/ FairScheduler

### YARN中Container是如何启动的？

1. AM向RM申请到Container（包含Host、资源量）
2. AM直接联系对应NM，发送启动命令（包含命令、环境变量、资源文件）
3. NM在本地启动Container进程，设置CPU/内存限制（cgroups）
4. Container向AM汇报状态

### YARN的改进之处，Hadoop3.x相对于Hadoop 2.x？

- 支持GPU/FPGA资源调度
- Opportunistic Container（低优先级抢占式Container，提高利用率）
- 更好的RM HA
- Timeline Service v2（更好的监控和历史记录）

---

## 综合问题

### 为什么Spark比MapReduce快？

|      | MapReduce     | Spark       |
| ---- | ------------- | ----------- |
| 中间结果 | 每步落磁盘         | 放内存         |
| 类比   | 每算完一步存档，下步再读档 | 一直在内存算，最后才存 |
| 速度   | 慢             | 快10-100倍    |

磁盘比内存慢100倍以上，所以Spark快很多。另外Spark用DAG优化执行计划，减少不必要的shuffle。

### 宽依赖窄依赖

- **窄依赖**：父RDD每个分区只被子RDD**一个**分区使用（如map、filter）→ 可pipeline，不需要shuffle
- **宽依赖**：父RDD每个分区被子RDD**多个**分区使用（如groupByKey、join）→ 需要shuffle，是stage划分边界

> 类比：窄依赖 = 一个工人负责一道工序（流水线）；宽依赖 = 所有工人的结果都要汇总再重新分配（需要等待）

### 是否遇到过数据倾斜问题？如何解决的

症状：大多数Task很快完成，少数Task卡住很久。

排查：看Spark UI，找数据量异常大的Task。

解决：

1. 过滤NULL或异常key
2. 大表join小表用MapJoin（广播小表）
3. 热点key加随机前缀打散，聚合后去掉前缀二次聚合
4. 增大shuffle分区数（`spark.sql.shuffle.partitions`）
5. Spark 3.x开启AQE（自适应查询执行）自动处理

### Spark的shuffle有几种方式

- **HashShuffle**（已废弃）：按key哈希写文件，文件数=Map数×Reduce数，文件太多
- **SortShuffle**（默认）：先排序再写一个文件+索引，文件数=Map数，效率更高
- **TungstenSortShuffle**：SortShuffle优化版，使用堆外内存，减少GC

### Hadoop和Spark的主要区别。Spark为什么更有优势？

|      | Hadoop MR       | Spark                |
| ---- | --------------- | -------------------- |
| 计算模型 | 两阶段（Map+Reduce） | DAG多阶段               |
| 中间数据 | 落HDFS磁盘         | 内存（必要时spill磁盘）       |
| 速度   | 慢               | 快10-100倍             |
| 编程模型 | 只有Map/Reduce，复杂 | RDD/DataFrame/SQL，丰富 |
| 适合场景 | 超大规模单次批处理       | 迭代计算、交互查询、流处理        |

**数据超内存时**：Spark自动将RDD分区spill到本地磁盘，性能降低但仍可工作。

### 你如何进行大数据平台的性能调优？

1. **存储层**：列式存储（ORC/Parquet）+压缩，合并小文件
2. **计算层**：合理设置并行度，用MapJoin，开启Combiner
3. **资源配置**：合理分配内存/CPU，调整JVM参数
4. **SQL优化**：谓词下推、分区裁剪、避免SELECT *、减少shuffle
5. **数据倾斜**：加盐打散、广播join
6. **监控定位**：Spark UI/YARN UI找瓶颈任务

### 一个Hive SQL或Spark任务运行很慢，你会从哪些方面排查？

1. **执行计划**：`EXPLAIN`，看是否全表扫描、缺少分区裁剪
2. **数据倾斜**：看各Task数据量是否均匀（Spark UI）
3. **小文件**：Map数过多，每个Task数据量极小
4. **Shuffle量**：是否Shuffle了大量数据
5. **资源**：是否频繁GC，内存是否够用
6. **Join策略**：大表join是否可改为MapJoin

### 对实时流处理的理解。用过哪些流处理框架？

实时流处理：对持续产生的数据流做低延迟处理，相对批处理的T+1，可达秒级甚至毫秒级。

|      | Spark Streaming | Flink           |
| ---- | --------------- | --------------- |
| 处理方式 | 微批（把流切成小批次）     | 真流（逐条处理）        |
| 延迟   | 秒级              | 毫秒级             |
| 吞吐量  | 高               | 高               |
| 语义   | At-Least-Once为主 | Exactly-Once    |
| 适合   | 对延迟要求不极致，吞吐高    | 低延迟、精确计算（对账、风控） |

### 在大数据开发中，如何管理数据权限和保障数据安全？

- **认证**：Kerberos（确保只有合法用户可访问）
- **授权**：Apache Ranger（表/列/行级别细粒度权限控制）
- **传输加密**：TLS/SSL
- **存储加密**：HDFS透明加密（KMS管理密钥）
- **数据脱敏**：敏感字段（手机号、身份证）在查询层脱敏
- **审计日志**：记录所有访问操作，便于追溯

---

## 数据湖

### 你了解数据湖、数据湖仓一体这些概念吗？它们与传统数据仓库相比有何演进？

|      | 数据仓库                    | 数据湖                  | 湖仓一体（Lakehouse）             |
| ---- | ----------------------- | -------------------- | --------------------------- |
| 类比   | 整理好的档案室                 | 什么都往里扔的储物间           | 智能储物室（存得下又找得到）              |
| 数据格式 | 只存结构化                   | 任意格式                 | 任意格式                        |
| 写入方式 | Schema-on-Write（写时定义结构） | Schema-on-Read（读时定义） | Schema-on-Write（有管理）        |
| 查询   | 快，有索引                   | 慢，无组织                | 快（有索引+统计信息）                 |
| 成本   | 贵                       | 便宜（对象存储）             | 便宜                          |
| ACID | 支持                      | 不支持                  | 支持（Delta Lake/Hudi/Iceberg） |
| 缺点   | 灵活性差，不支持非结构化            | 容易变"数据沼泽"，难治理        | 相对复杂                        |

**演进路径：** 数仓（贵但好用）→ 数据湖（便宜但难用）→ 湖仓一体（既便宜又好用）

代表技术：Delta Lake（Databricks）、Apache Hudi（Uber）、Apache Iceberg（Netflix）资源如何分配给各个应用程序（如 MapReduce、Spark、Hive 任务）。当多个用户或任务同时提交作业时，调度器决定谁先运行、谁使用多少资源、资源如何公平分配。

用户提交任务

三种调度器：

| 调度器               | 机制                 | 适用场景    |
| ----------------- | ------------------ | ------- |
| FIFO              | 先进先出               | 简单单用户系统 |
| CapacityScheduler | 多队列 + 优先级高、占资源少的先跑 | 大型企业    |
| FairScheduler     | 尽量公平分配资源           | 多用户共享   |

**FIFO**：

**CapacityScheduler**：

**FairScheduler**：

### 为什么需要调度器？

1、资源有限：Hadoop 集群资源，没有调度器的话：所有任务都在抢资源、可能有的任务占满集群、其他任务一直等待，调度器让系统 可控分配资源。

2、多用户共享：企业 Hadoop 经常是 共享集群（数据开发、算法团队、BI团队）

3、保证公平：让短任务快速运行

4、提高集群利用率：调度器可以实现资源借用、资源借用。提高 Cluster Utilization（集群利用率）

### 什么时候

### hadoop框架的理解、Hadoop的特点

Hadoop = **HDFS**（分布式存储）+ **MapReduce**（分布式计算）+ **YARN**（资源管理）

特点：**高可靠**（多副本容错）、**高扩展**（加机器就能扩容）、**高容错**（节点挂了自动恢复）、**低成本**（普通硬件即可）

### Hadoop生态圈组件及其作用

| 组件        | 作用                     |
| --------- | ---------------------- |
| HDFS      | 分布式文件存储                |
| MapReduce | 分布式批处理计算               |
| YARN      | 资源调度与管理                |
| Hive      | SQL查询工具（SQL转MapReduce） |
| HBase     | 分布式列式NoSQL数据库          |
| ZooKeeper | 分布式协调服务（选主、配置管理）       |
| Kafka     | 高吞吐消息队列                |
| Flume     | 日志采集                   |
| Sqoop     | 关系型数据库与HDFS互导          |
| Spark     | 内存计算引擎，比MR快            |

### Hadoop 1.x，2.x，3.x的区别

- **1.x**：JobTracker同时负责资源管理和任务调度，单点瓶颈；没有HA
- **2.x**：引入YARN把资源管理分出去；HDFS支持NameNode HA和Federation
- **3.x**：支持多个NameNode；引入**纠删码（EC）**替代副本节省存储约50%；支持GPU资源调度

### Hadoop集群工作时启动哪些进程？它们有什么作用？

- **NameNode**：管理HDFS元数据（文件在哪、有几个副本），不存实际数据
- **DataNode**：存储实际数据块，定期向NameNode发心跳汇报状态
- **ResourceManager**：管整个集群资源，接受Job提交，分配资源
- **NodeManager**：管单个节点资源，启动和监控Container
- **SecondaryNameNode**（非HA模式）：辅助NameNode合并日志，**不是**NameNode备份

### 在集群计算的时候，什么是集群的主要瓶颈

**磁盘I/O**是主要瓶颈，尤其是MapReduce的Shuffle阶段（大量数据溢写磁盘+网络传输）。其次是**网络带宽**。

### 搭建Hadoop集群的xml文件有哪些？

- `core-site.xml`：核心配置（HDFS地址等）
- `hdfs-site.xml`：HDFS配置（副本数、块大小等）
- `mapred-site.xml`：MapReduce配置
- `yarn-site.xml`：YARN配置

### Hadoop的checkpoint流程

> **类比：** 就像把流水账（editlog）定期整理成账本快照（fsimage），防止流水账越来越长。

1. SecondaryNameNode从NameNode拉取editlog和fsimage
2. 将editlog回放合并到fsimage，生成新fsimage
3. 将新fsimage推回NameNode，清空旧editlog

作用：防止editlog无限增长，加快NameNode重启速度。

### Hadoop的默认块大小是多少？为什么设置这么大？

默认**128MB**（Hadoop 2.x起）。

原因：磁盘寻址时间约10ms，传输速率约100MB/s，128MB传输约1.28秒，寻址时间占比约1%，效率最优。

- 太小 → Map任务数多，启动开销大
- 太大 → Map并行度低

### Block划分的原因

- 大文件切块后可**多节点并行处理**
- Block分散到各DataNode，**负载均衡**
- 单个Block损坏只需恢复该Block，**容错代价小**

### Hadoop常见的压缩算法？

| 算法     | 是否可切分   | 速度  | 压缩比 | 适用场景       |
| ------ | ------- | --- | --- | ---------- |
| Gzip   | ❌       | 中   | 高   | 冷数据存储      |
| Bzip2  | ✅       | 慢   | 最高  | 需切分的归档     |
| Snappy | ❌       | 最快  | 中   | Map输出、中间数据 |
| LZO    | ✅（需建索引） | 快   | 中   | 大文件、需切分场景  |

> 注意：不可切分的压缩格式（如Gzip）大文件只能一个Map处理，并行度差。

### Hadoop作业提交到YARN的流程？

1. Client向ResourceManager提交Job（上传JAR到HDFS）
2. RM分配Container，启动**ApplicationMaster**
3. AM向RM申请运行MapTask/ReduceTask的Container
4. AM联系NodeManager，在Container中启动任务
5. 任务完成，AM向RM注销，资源释放

### Hadoop的Combiner的作用

在**Map端本地预聚合**，减少传输到Reduce的数据量。

> **类比：** 100人统计词频，传纸条前先自己合并，传"hadoop:50"而不是50张"hadoop:1"。

要求操作满足交换律和结合律：✅ sum/max/min，❌ avg（会丢信息）

### Hadoop序列化和反序列化

Hadoop用`Writable`接口（非Java原生序列化），更紧凑高效，节省带宽。

常用类型：`IntWritable`、`LongWritable`、`Text`、`NullWritable`

### Hadoop的运行模式

- **本地模式**：单机单JVM，无HDFS，用于开发调试
- **伪分布式**：单机模拟集群
- **完全分布式**：多节点，生产环境

### Hadoop小文件处理问题

**问题：** 每个小文件占NameNode约150字节内存；每个小文件启动一个MapTask，启动开销远大于计算本身。

**解决：**

- **CombineFileInputFormat**：合并小文件再处理
- **SequenceFile**：将小文件以KV形式合并存储
- **HAR归档**：打包小文件
- 上游控制，避免产生小文件（如Hive设置合并输出）

### Hadoop为什么要从2.x升级到3.x？

- **纠删码**：存储开销从200%降至约50%，节省大量存储成本
- **多NameNode**：突破单NameNode扩展瓶颈
- **支持GPU/FPGA**资源调度

### Hadoop的优缺点

- **优点**：高容错、低成本、高扩展、适合PB级批量处理
- **缺点**：延迟高（不适合实时）、小文件问题、不支持随机写、不适合迭代计算

---

## 📦 HDFS

> **整体类比：** 图书馆管理系统
> 
> - NameNode = 图书馆目录（记录书在哪，但不存书）
> - DataNode = 书架（真正放书的地方）
> - Block = 把大书撕成若干份（128MB一份）
> - 副本数3 = 每份复印3本放不同书架，防止丢失

### HDFS NameNode高可用如何实现？需要哪些角色？

架构：**Active NameNode + Standby NameNode**

| 角色                 | 作用                           |
| ------------------ | ---------------------------- |
| Active NameNode    | 对外提供服务                       |
| Standby NameNode   | 热备，实时同步editlog               |
| JournalNode集群（≥3个） | 共享editlog，Active写入，Standby读取 |
| ZooKeeper          | 选主，记录谁是Active                |
| ZKFC               | 监控NameNode健康，触发自动切换          |

### HDFS中向DataNode写数据失败了怎么办

1. 将失败的DataNode从pipeline中移除
2. 已写数据标记为损坏
3. NameNode重新分配新DataNode，重建pipeline继续写
4. 写完后NameNode发现副本数不足，触发后台重新复制

### DataNode什么情况下不会备份

强制关闭或非正常断电时。

### HDFS中DataNode怎么存储数据的

- 数据以**Block文件**存在本地磁盘
- 每个Block对应一个`.meta`校验文件（CRC）
- DataNode每3秒向NameNode发**心跳**，每6小时发**块报告**

### NameNode存数据吗？

**不存实际数据**，只存**元数据**：文件目录树、文件与Block的映射、权限等。

持久化方式：`fsimage`（全量快照）+ `editlog`（操作日志）

### HDFS文件写入和读取流程

**写入流程：**

1. Client → NameNode：申请创建文件
2. NameNode返回DataNode列表（DN1→DN2→DN3 流水线）
3. Client将数据切Block，按流水线依次写入（DN1写完传给DN2，DN2传给DN3）
4. 每个packet写完，ack沿流水线反向回传给Client
5. 全部写完，Client通知NameNode完成

**读取流程：**

1. Client → NameNode：请求读文件
2. NameNode返回各Block所在DataNode列表（按距离排序）
3. Client就近选DataNode读取每个Block
4. CRC校验，损坏则自动切换其他副本

### HDFS优缺点及使用场景

- **优点**：高容错、高吞吐（流式读取）、低成本、可扩展
- **缺点**：高延迟、不适合小文件、不支持随机写、不支持并发写
- **使用场景**：日志存储、数据仓库原始数据、离线批处理

### HDFS的容错机制

- **心跳检测**：DataNode超时未发心跳，NameNode触发副本重建
- **CRC校验**：读写时检测数据损坏，自动切换副本
- **多副本**：默认3副本，一个节点坏了不影响数据
- **NameNode HA**：元数据不丢失

### HDFS的副本机制

默认**3副本**放置策略：

- 第1副本：客户端所在节点
- 第2副本：**不同机架**的节点
- 第3副本：与第2副本**同机架**不同节点

兼顾可靠性（跨机架防机架故障）和网络效率。

### HDFS的常见数据格式，列式存储格式和行存储格式异同点，列式存储优点有哪些？

**行存储**：一行数据连续存储，适合OLTP（增删改查整行）

**列式存储**：同一列数据连续存储，适合OLAP（只读少数列的聚合分析）

**列式存储优点：**

- 压缩比高（同列数据类型相同，压缩效果好）
- I/O少（只读需要的列，跳过无关数据）
- 聚合计算快（sum/count等）

常见格式：TextFile（行）、SequenceFile（行）、ORC（列）、Parquet（列）

### HDFS的默认副本数？为什么？如何修改？

默认**3副本**：在可靠性和存储成本之间取平衡（容忍2个节点同时故障）。

修改：

- `hdfs-site.xml` 中 `dfs.replication=3`
- 或命令：`hdfs dfs -setrep -w 2 /path/to/file`

### HDFS的块默认大小，64M和128M是在哪个版本更换的？怎么修改默认块大小？

Hadoop **1.x默认64MB**，**2.x起改为128MB**。

修改：`hdfs-site.xml` 中 `dfs.blocksize=134217728`（单位字节）

### HDFS的block为什么是128M？增大或减小有什么影响？

磁盘寻址约10ms，传输速率约100MB/s，128MB传输约1.28秒，寻址时间占比约1%，效率最优。

- **增大**：Map并行度降低，适合超大文件
- **减小**：Map任务数增多，启动开销大，NameNode元数据增多

### HDFS HA怎么实现？是个什么架构？

见上方"NameNode高可用"部分：Active NN + Standby NN + JournalNode集群 + ZooKeeper + ZKFC

### 导入大文件到HDFS时如何自定义分片？

实现自定义`InputFormat`，重写`getSplits()`方法。或调整参数：

- `mapreduce.input.fileinputformat.split.maxsize`
- `mapreduce.input.fileinputformat.split.minsize`

### HDFS的mapper和reducer的个数如何确定？reducer的个数依据是什么？

- **Mapper数**：由输入Split数决定，一个Split = 一个MapTask（默认Split大小 = Block大小）
- **Reducer数**：手动设置（`job.setNumReduceTasks(n)`），一般设为节点数×1.5~2倍

### HDFS跨节点怎么进行数据迁移

- `hadoop distcp`：分布式拷贝，适合集群间大量数据迁移（推荐）
- 跨集群：`hadoop distcp hdfs://cluster1/path hdfs://cluster2/path`

### HDFS的数据一致性靠什么保证？

- **写入时**：pipeline写入，所有副本ack后才确认写成功
- **读取时**：CRC校验，不一致自动切换副本
- **副本监控**：NameNode持续监控副本数，不足时触发重建

### HDFS怎么保证数据安全

- 多副本（数据冗余）
- CRC校验（检测损坏）
- Kerberos认证（身份验证）
- ACL权限控制（文件级权限）
- 传输加密（TLS）和存储加密（KMS）
- 审计日志

### HDFS写数据过程，写的过程中有哪些故障，分别会怎么处理？

写数据过程见上方"写入流程"。

故障处理：

- **某DataNode宕机**：从pipeline移除，用新DataNode替换，事后补足副本数
- **NameNode宕机（HA模式）**：Standby自动切为Active，Client重连继续写
- **网络超时**：packet重传，超时后报错，Client可重试

### 直接将数据文件上传到HDFS的表目录中，如何在表中查询到该数据？

- **非分区表**：直接可查，Hive会扫描目录下所有文件
- **分区表**：执行 `MSCK REPAIR TABLE 表名;` 刷新分区元数据，或手动 `ALTER TABLE 表名 ADD PARTITION (...)`

---

## ⚙️ MapReduce

> **整体类比：** 统计一本书里每个单词出现多少次
> 
> - **Map** = 把书分给100人，每人数自己那几页的词频，输出(词, 1)
> - **Shuffle** = 把所有"hadoop"汇给同一个人，"spark"汇给另一个人
> - **Reduce** = 每人把收到的同一词的数字加起来，得出最终结果

### 介绍下MapReduce

分布式批处理计算框架，将计算分为两阶段：

- **Map**：对输入数据做转换/过滤，输出KV对
- **Reduce**：对相同key的value做聚合

中间通过**Shuffle**（分区、排序、合并、网络传输）连接两个阶段。

### MapReduce优缺点

- **优点**：简单、高容错、适合超大规模离线批处理
- **缺点**：延迟高（中间结果落磁盘）、不适合实时、不适合迭代计算

### MapReduce工作原理

```
输入文件 → Split切分 → MapTask → 环形缓冲区
→ 溢写（分区+排序）→ 合并 → Shuffle（网络传输）
→ ReduceTask归并排序 → Reduce函数 → 输出文件
```

### MapReduce哪个阶段最费时间

**Shuffle阶段**最耗时：大量磁盘溢写 + 归并排序 + 网络传输。

### MapReduce中的Combine是干嘛的？有什么好处？

在Map端本地预聚合，减少传输到Reduce的数据量。

- 好处：减少网络传输、减轻ReduceTask压力、整体加快
- 要求：操作满足交换律和结合律（✅ sum/max，❌ avg）

### MapReduce为什么一定要有环形缓冲区

Map输出先写内存环形缓冲区（默认100MB），满80%再批量溢写磁盘。

避免每条数据都触发磁盘I/O，批量写效率高得多。环形设计可以边写边溢写，不阻塞。

### MapReduce为什么一定要有Shuffle过程

Map和Reduce之间需要**按key分组**：相同key的数据必须汇聚到同一个ReduceTask处理。Shuffle负责分区→排序→网络传输→归并，没有Shuffle就无法实现分布式聚合。

### MapReduce的Shuffle过程及其优化

**Map端：** Map输出 → 写环形缓冲区 → 满80%溢写（按分区快速排序）→ 多个溢写文件归并合并

**Reduce端：** HTTP拉取各MapTask输出 → 归并排序 → 传给Reducer

**优化：**

- 开启Combiner预聚合，减少传输量
- 压缩Map输出（`mapreduce.map.output.compress=true`，推荐Snappy）
- 调大环形缓冲区（`mapreduce.task.io.sort.mb`）

### Reduce怎么知道去哪里拉Map结果集？

ApplicationMaster追踪所有MapTask完成情况和输出位置。ReduceTask定期询问AM，获取已完成MapTask的输出位置（Host+端口），通过HTTP主动拉取。

### Reduce阶段都发生了什么，有没有进行分组

1. **拉取数据**：从各MapTask HTTP拉取属于本Reducer的分区数据
2. **归并排序**：将多份数据归并排序（相同key相邻）
3. **分组**：相同key的所有value形成一个Iterable（**有分组**）
4. **调用Reduce函数**：对每个key的value集合执行用户逻辑
5. **输出**：写入HDFS

### MapReduce Shuffle的排序算法

- **Map端溢写**：快速排序
- **Map端合并溢写文件**：归并排序
- **Reduce端合并拉取数据**：归并排序

### shuffle为什么要排序？

排序使相同key的数据**相邻**，Reduce端分组只需顺序扫描，无需额外哈希表，内存占用低，效率高。

### 说一下map是怎么到reduce的？

Map输出 → 写环形缓冲区 → 按分区排序 → 溢写磁盘 → 归并合并成一个有序文件 → Reduce通过HTTP拉取 → 归并排序 → 传给Reducer

### MapReduce的数据处理过程

Input → InputFormat切分 → RecordReader读取KV → Map函数 → Partitioner分区 → 排序 → Combiner（可选）→ Shuffle → Reduce函数 → OutputFormat → Output

### mapjoin的原理？应用场景？

**原理：** 将小表通过DistributedCache广播到所有MapTask的内存中，Map阶段直接与大表做join，**无需Reduce和Shuffle**。

> 类比：把城市编码表打印一份给每个工人，工人本地查表，不用汇总给主管。

**应用场景：** 大表 join 小表（小表能装入内存，如几百MB以内），可完全避免数据倾斜。

### reducejoin如何执行（原理）

1. 两张表数据都打上标记（标注来自哪张表）
2. 以join key为Map输出key，相同key的数据到同一Reducer
3. Reducer中按标记区分两张表，做匹配

缺点：所有数据都要Shuffle，数据量大时可能数据倾斜，性能不如MapJoin。

### MapReduce为什么不能产生过多小文件

- 每个小文件对应一个MapTask，JVM启动开销远大于实际计算
- 大量小文件消耗NameNode内存（每文件约150字节元数据）

### MapReduce分区及作用

分区决定Map输出的KV数据发送到哪个ReduceTask。

默认：`HashPartitioner`：`key.hashCode() % numReduceTasks`

保证相同key一定到同一Reducer。可自定义Partitioner实现业务分区。

### ReduceTask数量和分区数量关系

- ReduceTask == 分区数：✅ 正常
- ReduceTask > 分区数：多余的Task空转，产生空文件
- ReduceTask < 分区数：❌ 报错，部分分区数据无处写入

### Map的分片有多大

默认分片大小 = Block大小（128MB）。

分片大小 = `max(minSize, min(maxSize, blockSize))`

### reduce任务什么时候开始？

- **Shuffle拉取数据**：5%的MapTask完成后就开始拉
- **Reduce真正计算**：等所有MapTask完成后才开始

### MapReduce用了几次排序，分别是什么？

共**3次**：

1. **Map端溢写时**：快速排序（对缓冲区内数据）
2. **Map端合并溢写文件时**：归并排序
3. **Reduce端合并拉取数据时**：归并排序

### MapReduce怎么确定MapTask的数量？Map数量由什么决定

MapTask数量 = 输入数据的**Split数量**，一个Split对应一个MapTask。

Split数 = 输入文件大小 / 分片大小（默认=Block大小128MB）

小文件多时，每个文件至少一个Split，MapTask数会爆炸。

### MapReduce作业执行过程中，中间数据存在什么地方？

存在**本地磁盘**（非HDFS）。

Map输出先写内存环形缓冲区（100MB），超过80%溢写到**本地磁盘**，最终合并成本地文件。Reduce拉取后也先写本地磁盘归并，再传给Reducer计算。

### map输出数据超出缓冲区后，落地到磁盘还是HDFS？

**本地磁盘**（不是HDFS）。中间数据走本地磁盘效率更高，HDFS是最终输入输出用的。

### Map到Reduce默认的分区机制是什么？

默认`HashPartitioner`：`(key.hashCode() & Integer.MAX_VALUE) % numReduceTasks`

### MapReduce数据倾斜产生的原因及其解决方案

**原因：** key分布不均，某些key数据量远大于其他，对应Reducer处理时间远长。

> 类比：100人统计词频，"的"字出现100万次全汇给一个人，这人累死其他人都完了。

**解决方案：**

- **MapJoin**：小表广播内存，避免Reduce阶段（最彻底）
- **key加随机前缀**：打散热点key（加1-100随机数前缀），聚合后再二次聚合
- **自定义Partitioner**：将热点key均匀分配
- **Combiner预聚合**：减少传到Reducer的数据
- **过滤NULL或异常key**：提前过滤无效数据

### Map Join为什么能解决数据倾斜

MapJoin完全在Map端完成join，**没有Shuffle没有Reduce**，每个MapTask独立处理一部分数据并查询内存中的小表，数据天然均衡，不存在某节点数据集中的问题。

### MapReduce运行过程中会发生OOM，OOM发生的位置？

- **Map端**：环形缓冲区设置过大，或Map逻辑缓存了太多数据
- **Reduce端**：归并数据时内存不足，或Reduce逻辑缓存太多

解决：调大 `mapreduce.map/reduce.memory.mb` 和对应JVM堆内存参数。

### MapReduce压缩方式

- **Map输出压缩**：减少Shuffle传输量，推荐Snappy（快）
- **最终输出压缩**：减少HDFS存储，推荐Bzip2（可切分）或Gzip

配置：`mapreduce.map.output.compress=true`

### MapReduce中怎么处理一个大文件

- 确保文件**可切分**（避免不可切分的Gzip压缩）
- 使用`FileInputFormat`按Block自动切分
- 调大Map内存和超时时间
- 开启Combiner和Map输出压缩

---

## 🎯 YARN

> **整体类比：** 工厂人力资源部
> 
> - **ResourceManager** = 人事总监（管全厂资源）
> - **NodeManager** = 各车间主任（管自己车间）
> - **ApplicationMaster** = 项目经理（管一个具体项目，向总监要资源）
> - **Container** = 一个工位（固定CPU+内存）

### 介绍下YARN

YARN（Yet Another Resource Negotiator）是Hadoop的资源管理框架，将资源管理和作业调度分离，支持多计算框架（MapReduce/Spark/Flink）共享集群资源。

### YARN有几个模块

4个核心模块：

- **ResourceManager（RM）**：全局资源管理
- **NodeManager（NM）**：单节点资源管理
- **ApplicationMaster（AM）**：每个应用独立，申请资源+任务调度
- **Container**：资源封装单元（CPU + 内存）

### YARN工作机制

1. Client向RM提交应用
2. RM分配Container，启动AM（项目经理上班）
3. AM评估需要多少资源，向RM申请Container列表
4. RM分配Container，AM通知对应NM启动Container执行任务
5. 任务完成，AM向RM注销，资源释放

### YARN有什么优势，能解决什么问题？

解决Hadoop 1.x的JobTracker单点瓶颈（同时负责资源管理和任务调度）。

YARN优势：

- 职责分离，RM专注资源，AM专注应用
- 支持多框架共享集群（MR/Spark/Flink）
- 更好的扩展性（支持数万节点）

### YARN容错机制

- **RM故障**：ZooKeeper实现RM HA，Standby自动接管
- **NM故障**：RM检测到心跳超时，将该节点任务重新调度
- **AM故障**：RM重新启动AM（默认重试2次）
- **Container/Task故障**：AM检测到，重新申请Container重跑

### YARN高可用

Active RM + Standby RM + ZooKeeper（选主+状态存储）

Active故障时Standby自动切换。

### YARN调度器

同Hadoop调度器：FIFO / CapacityScheduler（默认）/ FairScheduler

### YARN中Container是如何启动的？

1. AM向RM申请到Container（包含Host、资源量）
2. AM直接联系对应NM，发送启动命令（包含命令、环境变量、资源文件）
3. NM在本地启动Container进程，设置CPU/内存限制（cgroups）
4. Container向AM汇报状态

### YARN的改进之处，Hadoop3.x相对于Hadoop 2.x？

- 支持GPU/FPGA资源调度
- Opportunistic Container（低优先级抢占式Container，提高利用率）
- 更好的RM HA
- Timeline Service v2（更好的监控和历史记录）

---

## 综合问题

### 为什么Spark比MapReduce快？

|      | MapReduce     | Spark       |
| ---- | ------------- | ----------- |
| 中间结果 | 每步落磁盘         | 放内存         |
| 类比   | 每算完一步存档，下步再读档 | 一直在内存算，最后才存 |
| 速度   | 慢             | 快10-100倍    |

磁盘比内存慢100倍以上，所以Spark快很多。另外Spark用DAG优化执行计划，减少不必要的shuffle。

### 宽依赖窄依赖

- **窄依赖**：父RDD每个分区只被子RDD**一个**分区使用（如map、filter）→ 可pipeline，不需要shuffle
- **宽依赖**：父RDD每个分区被子RDD**多个**分区使用（如groupByKey、join）→ 需要shuffle，是stage划分边界

> 类比：窄依赖 = 一个工人负责一道工序（流水线）；宽依赖 = 所有工人的结果都要汇总再重新分配（需要等待）

### 是否遇到过数据倾斜问题？如何解决的

症状：大多数Task很快完成，少数Task卡住很久。

排查：看Spark UI，找数据量异常大的Task。

解决：

1. 过滤NULL或异常key
2. 大表join小表用MapJoin（广播小表）
3. 热点key加随机前缀打散，聚合后去掉前缀二次聚合
4. 增大shuffle分区数（`spark.sql.shuffle.partitions`）
5. Spark 3.x开启AQE（自适应查询执行）自动处理

### Spark的shuffle有几种方式

- **HashShuffle**（已废弃）：按key哈希写文件，文件数=Map数×Reduce数，文件太多
- **SortShuffle**（默认）：先排序再写一个文件+索引，文件数=Map数，效率更高
- **TungstenSortShuffle**：SortShuffle优化版，使用堆外内存，减少GC

### Hadoop和Spark的主要区别。Spark为什么更有优势？

|      | Hadoop MR       | Spark                |
| ---- | --------------- | -------------------- |
| 计算模型 | 两阶段（Map+Reduce） | DAG多阶段               |
| 中间数据 | 落HDFS磁盘         | 内存（必要时spill磁盘）       |
| 速度   | 慢               | 快10-100倍             |
| 编程模型 | 只有Map/Reduce，复杂 | RDD/DataFrame/SQL，丰富 |
| 适合场景 | 超大规模单次批处理       | 迭代计算、交互查询、流处理        |

**数据超内存时**：Spark自动将RDD分区spill到本地磁盘，性能降低但仍可工作。

### 你如何进行大数据平台的性能调优？

1. **存储层**：列式存储（ORC/Parquet）+压缩，合并小文件
2. **计算层**：合理设置并行度，用MapJoin，开启Combiner
3. **资源配置**：合理分配内存/CPU，调整JVM参数
4. **SQL优化**：谓词下推、分区裁剪、避免SELECT *、减少shuffle
5. **数据倾斜**：加盐打散、广播join
6. **监控定位**：Spark UI/YARN UI找瓶颈任务

### 一个Hive SQL或Spark任务运行很慢，你会从哪些方面排查？

1. **执行计划**：`EXPLAIN`，看是否全表扫描、缺少分区裁剪
2. **数据倾斜**：看各Task数据量是否均匀（Spark UI）
3. **小文件**：Map数过多，每个Task数据量极小
4. **Shuffle量**：是否Shuffle了大量数据
5. **资源**：是否频繁GC，内存是否够用
6. **Join策略**：大表join是否可改为MapJoin

### 对实时流处理的理解。用过哪些流处理框架？

实时流处理：对持续产生的数据流做低延迟处理，相对批处理的T+1，可达秒级甚至毫秒级。

|      | Spark Streaming | Flink           |
| ---- | --------------- | --------------- |
| 处理方式 | 微批（把流切成小批次）     | 真流（逐条处理）        |
| 延迟   | 秒级              | 毫秒级             |
| 吞吐量  | 高               | 高               |
| 语义   | At-Least-Once为主 | Exactly-Once    |
| 适合   | 对延迟要求不极致，吞吐高    | 低延迟、精确计算（对账、风控） |

### 在大数据开发中，如何管理数据权限和保障数据安全？

- **认证**：Kerberos（确保只有合法用户可访问）
- **授权**：Apache Ranger（表/列/行级别细粒度权限控制）
- **传输加密**：TLS/SSL
- **存储加密**：HDFS透明加密（KMS管理密钥）
- **数据脱敏**：敏感字段（手机号、身份证）在查询层脱敏
- **审计日志**：记录所有访问操作，便于追溯

---

## 数据湖

### 你了解数据湖、数据湖仓一体这些概念吗？它们与传统数据仓库相比有何演进？

|      | 数据仓库                    | 数据湖                  | 湖仓一体（Lakehouse）             |
| ---- | ----------------------- | -------------------- | --------------------------- |
| 类比   | 整理好的档案室                 | 什么都往里扔的储物间           | 智能储物室（存得下又找得到）              |
| 数据格式 | 只存结构化                   | 任意格式                 | 任意格式                        |
| 写入方式 | Schema-on-Write（写时定义结构） | Schema-on-Read（读时定义） | Schema-on-Write（有管理）        |
| 查询   | 快，有索引                   | 慢，无组织                | 快（有索引+统计信息）                 |
| 成本   | 贵                       | 便宜（对象存储）             | 便宜                          |
| ACID | 支持                      | 不支持                  | 支持（Delta Lake/Hudi/Iceberg） |
| 缺点   | 灵活性差，不支持非结构化            | 容易变"数据沼泽"，难治理        | 相对复杂                        |

**演进路径：** 数仓（贵但好用）→ 数据湖（便宜但难用）→ 湖仓一体（既便宜又好用）

代表技术：Delta Lake（Databricks）、Apache Hudi（Uber）、Apache Iceberg（Netflix）[大数据面试题V3.0，约870篇牛客大数据面经480道面试题_牛客网](https://www.nowcoder.com/discuss/353159520220291072)

https://zhuanlan.zhihu.com/p/424296249 [大数据开发面经汇总【持续更新...】_牛客网](https://www.nowcoder.com/discuss/594817738107781120)

https://leetcode.cn/discuss/post/3516212/zi-jie-mian-jing-nian-xin-70wda-shu-ju-s-23r7/

[大数据开发面经_大数据面经-CSDN博客](https://blog.csdn.net/axzy5863/article/details/158429145)

[大数据开发（牛客）面试被问频率最高的几道面试题-腾讯云开发者社区-腾讯云](https://cloud.tencent.com/developer/article/2071876)

---

## 🐘 Hadoop整体理解

把Hadoop想象成一个**超大的仓库管理系统**：

- **HDFS** = 仓库（存东西）
- **MapReduce** = 工人（干活）
- **YARN** = 仓库主管（分配工人和资源）

---

## Hadoop基础

### 什么是Hadoop调度器？说明其工作方法

Hadoop 调度器（Hadoop Scheduler）通常指 Hadoop YARN （Yet Another Resource Negotiator） 中的资源调度组件，负责决定 集群中的 CPU、内存等计算资源如何分配给各个应用程序（如 MapReduce、Spark、Hive 任务）。当多个用户或任务同时提交作业时，调度器决定谁先运行、谁使用多少资源、资源如何公平分配。

没有调度器的话：所有任务都在抢资源、可能有的任务占满集群、其他任务一直等待
三种调度器：

| 调度器               | 机制   | 适用场景 |
| ----------------- | ---- | ---- |
| FIFO              | 先进先出 |      |
| CapacityScheduler |      |      |
| FairScheduler     |      |      |

- **FIFO**：先进先出，按提交顺序排队执行，简单但资源利用率低
- **CapacityScheduler（默认）**：多队列，按队列容量分配资源，优先级高、占资源少的先跑
- **FairScheduler**：同一队列内所有作业公平共享资源，动态均衡

### hadoop框架的理解、Hadoop的特点

Hadoop = **HDFS**（分布式存储）+ **MapReduce**（分布式计算）+ **YARN**（资源管理）

特点：**高可靠**（多副本容错）、**高扩展**（加机器就能扩容）、**高容错**（节点挂了自动恢复）、**低成本**（普通硬件即可）

### Hadoop生态圈组件及其作用

| 组件        | 作用                     |
| --------- | ---------------------- |
| HDFS      | 分布式文件存储                |
| MapReduce | 分布式批处理计算               |
| YARN      | 资源调度与管理                |
| Hive      | SQL查询工具（SQL转MapReduce） |
| HBase     | 分布式列式NoSQL数据库          |
| ZooKeeper | 分布式协调服务（选主、配置管理）       |
| Kafka     | 高吞吐消息队列                |
| Flume     | 日志采集                   |
| Sqoop     | 关系型数据库与HDFS互导          |
| Spark     | 内存计算引擎，比MR快            |

### Hadoop 1.x，2.x，3.x的区别

- **1.x**：JobTracker同时负责资源管理和任务调度，单点瓶颈；没有HA
- **2.x**：引入YARN把资源管理分出去；HDFS支持NameNode HA和Federation
- **3.x**：支持多个NameNode；引入**纠删码（EC）**替代副本节省存储约50%；支持GPU资源调度

### Hadoop集群工作时启动哪些进程？它们有什么作用？

- **NameNode**：管理HDFS元数据（文件在哪、有几个副本），不存实际数据
- **DataNode**：存储实际数据块，定期向NameNode发心跳汇报状态
- **ResourceManager**：管整个集群资源，接受Job提交，分配资源
- **NodeManager**：管单个节点资源，启动和监控Container
- **SecondaryNameNode**（非HA模式）：辅助NameNode合并日志，**不是**NameNode备份

### 在集群计算的时候，什么是集群的主要瓶颈

**磁盘I/O**是主要瓶颈，尤其是MapReduce的Shuffle阶段（大量数据溢写磁盘+网络传输）。其次是**网络带宽**。

### 搭建Hadoop集群的xml文件有哪些？

- `core-site.xml`：核心配置（HDFS地址等）
- `hdfs-site.xml`：HDFS配置（副本数、块大小等）
- `mapred-site.xml`：MapReduce配置
- `yarn-site.xml`：YARN配置

### Hadoop的checkpoint流程

> **类比：** 就像把流水账（editlog）定期整理成账本快照（fsimage），防止流水账越来越长。

1. SecondaryNameNode从NameNode拉取editlog和fsimage
2. 将editlog回放合并到fsimage，生成新fsimage
3. 将新fsimage推回NameNode，清空旧editlog

作用：防止editlog无限增长，加快NameNode重启速度。

### Hadoop的默认块大小是多少？为什么设置这么大？

默认**128MB**（Hadoop 2.x起）。

原因：磁盘寻址时间约10ms，传输速率约100MB/s，128MB传输约1.28秒，寻址时间占比约1%，效率最优。

- 太小 → Map任务数多，启动开销大
- 太大 → Map并行度低

### Block划分的原因

- 大文件切块后可**多节点并行处理**
- Block分散到各DataNode，**负载均衡**
- 单个Block损坏只需恢复该Block，**容错代价小**

### Hadoop常见的压缩算法？

| 算法     | 是否可切分   | 速度  | 压缩比 | 适用场景       |
| ------ | ------- | --- | --- | ---------- |
| Gzip   | ❌       | 中   | 高   | 冷数据存储      |
| Bzip2  | ✅       | 慢   | 最高  | 需切分的归档     |
| Snappy | ❌       | 最快  | 中   | Map输出、中间数据 |
| LZO    | ✅（需建索引） | 快   | 中   | 大文件、需切分场景  |

> 注意：不可切分的压缩格式（如Gzip）大文件只能一个Map处理，并行度差。

### Hadoop作业提交到YARN的流程？

1. Client向ResourceManager提交Job（上传JAR到HDFS）
2. RM分配Container，启动**ApplicationMaster**
3. AM向RM申请运行MapTask/ReduceTask的Container
4. AM联系NodeManager，在Container中启动任务
5. 任务完成，AM向RM注销，资源释放

### Hadoop的Combiner的作用

在**Map端本地预聚合**，减少传输到Reduce的数据量。

> **类比：** 100人统计词频，传纸条前先自己合并，传"hadoop:50"而不是50张"hadoop:1"。

要求操作满足交换律和结合律：✅ sum/max/min，❌ avg（会丢信息）

### Hadoop序列化和反序列化

Hadoop用`Writable`接口（非Java原生序列化），更紧凑高效，节省带宽。

常用类型：`IntWritable`、`LongWritable`、`Text`、`NullWritable`

### Hadoop的运行模式

- **本地模式**：单机单JVM，无HDFS，用于开发调试
- **伪分布式**：单机模拟集群
- **完全分布式**：多节点，生产环境

### Hadoop小文件处理问题

**问题：** 每个小文件占NameNode约150字节内存；每个小文件启动一个MapTask，启动开销远大于计算本身。

**解决：**

- **CombineFileInputFormat**：合并小文件再处理
- **SequenceFile**：将小文件以KV形式合并存储
- **HAR归档**：打包小文件
- 上游控制，避免产生小文件（如Hive设置合并输出）

### Hadoop为什么要从2.x升级到3.x？

- **纠删码**：存储开销从200%降至约50%，节省大量存储成本
- **多NameNode**：突破单NameNode扩展瓶颈
- **支持GPU/FPGA**资源调度

### Hadoop的优缺点

- **优点**：高容错、低成本、高扩展、适合PB级批量处理
- **缺点**：延迟高（不适合实时）、小文件问题、不支持随机写、不适合迭代计算

---

## 📦 HDFS

> **整体类比：** 图书馆管理系统
> 
> - NameNode = 图书馆目录（记录书在哪，但不存书）
> - DataNode = 书架（真正放书的地方）
> - Block = 把大书撕成若干份（128MB一份）
> - 副本数3 = 每份复印3本放不同书架，防止丢失

### HDFS NameNode高可用如何实现？需要哪些角色？

架构：**Active NameNode + Standby NameNode**

| 角色                 | 作用                           |
| ------------------ | ---------------------------- |
| Active NameNode    | 对外提供服务                       |
| Standby NameNode   | 热备，实时同步editlog               |
| JournalNode集群（≥3个） | 共享editlog，Active写入，Standby读取 |
| ZooKeeper          | 选主，记录谁是Active                |
| ZKFC               | 监控NameNode健康，触发自动切换          |

### HDFS中向DataNode写数据失败了怎么办

1. 将失败的DataNode从pipeline中移除
2. 已写数据标记为损坏
3. NameNode重新分配新DataNode，重建pipeline继续写
4. 写完后NameNode发现副本数不足，触发后台重新复制

### DataNode什么情况下不会备份

强制关闭或非正常断电时。

### HDFS中DataNode怎么存储数据的

- 数据以**Block文件**存在本地磁盘
- 每个Block对应一个`.meta`校验文件（CRC）
- DataNode每3秒向NameNode发**心跳**，每6小时发**块报告**

### NameNode存数据吗？

**不存实际数据**，只存**元数据**：文件目录树、文件与Block的映射、权限等。

持久化方式：`fsimage`（全量快照）+ `editlog`（操作日志）

### HDFS文件写入和读取流程

**写入流程：**

1. Client → NameNode：申请创建文件
2. NameNode返回DataNode列表（DN1→DN2→DN3 流水线）
3. Client将数据切Block，按流水线依次写入（DN1写完传给DN2，DN2传给DN3）
4. 每个packet写完，ack沿流水线反向回传给Client
5. 全部写完，Client通知NameNode完成

**读取流程：**

1. Client → NameNode：请求读文件
2. NameNode返回各Block所在DataNode列表（按距离排序）
3. Client就近选DataNode读取每个Block
4. CRC校验，损坏则自动切换其他副本

### HDFS优缺点及使用场景

- **优点**：高容错、高吞吐（流式读取）、低成本、可扩展
- **缺点**：高延迟、不适合小文件、不支持随机写、不支持并发写
- **使用场景**：日志存储、数据仓库原始数据、离线批处理

### HDFS的容错机制

- **心跳检测**：DataNode超时未发心跳，NameNode触发副本重建
- **CRC校验**：读写时检测数据损坏，自动切换副本
- **多副本**：默认3副本，一个节点坏了不影响数据
- **NameNode HA**：元数据不丢失

### HDFS的副本机制

默认**3副本**放置策略：

- 第1副本：客户端所在节点
- 第2副本：**不同机架**的节点
- 第3副本：与第2副本**同机架**不同节点

兼顾可靠性（跨机架防机架故障）和网络效率。

### HDFS的常见数据格式，列式存储格式和行存储格式异同点，列式存储优点有哪些？

**行存储**：一行数据连续存储，适合OLTP（增删改查整行）

**列式存储**：同一列数据连续存储，适合OLAP（只读少数列的聚合分析）

**列式存储优点：**

- 压缩比高（同列数据类型相同，压缩效果好）
- I/O少（只读需要的列，跳过无关数据）
- 聚合计算快（sum/count等）

常见格式：TextFile（行）、SequenceFile（行）、ORC（列）、Parquet（列）

### HDFS的默认副本数？为什么？如何修改？

默认**3副本**：在可靠性和存储成本之间取平衡（容忍2个节点同时故障）。

修改：

- `hdfs-site.xml` 中 `dfs.replication=3`
- 或命令：`hdfs dfs -setrep -w 2 /path/to/file`

### HDFS的块默认大小，64M和128M是在哪个版本更换的？怎么修改默认块大小？

Hadoop **1.x默认64MB**，**2.x起改为128MB**。

修改：`hdfs-site.xml` 中 `dfs.blocksize=134217728`（单位字节）

### HDFS的block为什么是128M？增大或减小有什么影响？

磁盘寻址约10ms，传输速率约100MB/s，128MB传输约1.28秒，寻址时间占比约1%，效率最优。

- **增大**：Map并行度降低，适合超大文件
- **减小**：Map任务数增多，启动开销大，NameNode元数据增多

### HDFS HA怎么实现？是个什么架构？

见上方"NameNode高可用"部分：Active NN + Standby NN + JournalNode集群 + ZooKeeper + ZKFC

### 导入大文件到HDFS时如何自定义分片？

实现自定义`InputFormat`，重写`getSplits()`方法。或调整参数：

- `mapreduce.input.fileinputformat.split.maxsize`
- `mapreduce.input.fileinputformat.split.minsize`

### HDFS的mapper和reducer的个数如何确定？reducer的个数依据是什么？

- **Mapper数**：由输入Split数决定，一个Split = 一个MapTask（默认Split大小 = Block大小）
- **Reducer数**：手动设置（`job.setNumReduceTasks(n)`），一般设为节点数×1.5~2倍

### HDFS跨节点怎么进行数据迁移

- `hadoop distcp`：分布式拷贝，适合集群间大量数据迁移（推荐）
- 跨集群：`hadoop distcp hdfs://cluster1/path hdfs://cluster2/path`

### HDFS的数据一致性靠什么保证？

- **写入时**：pipeline写入，所有副本ack后才确认写成功
- **读取时**：CRC校验，不一致自动切换副本
- **副本监控**：NameNode持续监控副本数，不足时触发重建

### HDFS怎么保证数据安全

- 多副本（数据冗余）
- CRC校验（检测损坏）
- Kerberos认证（身份验证）
- ACL权限控制（文件级权限）
- 传输加密（TLS）和存储加密（KMS）
- 审计日志

### HDFS写数据过程，写的过程中有哪些故障，分别会怎么处理？

写数据过程见上方"写入流程"。

故障处理：

- **某DataNode宕机**：从pipeline移除，用新DataNode替换，事后补足副本数
- **NameNode宕机（HA模式）**：Standby自动切为Active，Client重连继续写
- **网络超时**：packet重传，超时后报错，Client可重试

### 直接将数据文件上传到HDFS的表目录中，如何在表中查询到该数据？

- **非分区表**：直接可查，Hive会扫描目录下所有文件
- **分区表**：执行 `MSCK REPAIR TABLE 表名;` 刷新分区元数据，或手动 `ALTER TABLE 表名 ADD PARTITION (...)`

---

## ⚙️ MapReduce

> **整体类比：** 统计一本书里每个单词出现多少次
> 
> - **Map** = 把书分给100人，每人数自己那几页的词频，输出(词, 1)
> - **Shuffle** = 把所有"hadoop"汇给同一个人，"spark"汇给另一个人
> - **Reduce** = 每人把收到的同一词的数字加起来，得出最终结果

### 介绍下MapReduce

分布式批处理计算框架，将计算分为两阶段：

- **Map**：对输入数据做转换/过滤，输出KV对
- **Reduce**：对相同key的value做聚合

中间通过**Shuffle**（分区、排序、合并、网络传输）连接两个阶段。

### MapReduce优缺点

- **优点**：简单、高容错、适合超大规模离线批处理
- **缺点**：延迟高（中间结果落磁盘）、不适合实时、不适合迭代计算

### MapReduce工作原理

```
输入文件 → Split切分 → MapTask → 环形缓冲区
→ 溢写（分区+排序）→ 合并 → Shuffle（网络传输）
→ ReduceTask归并排序 → Reduce函数 → 输出文件
```

### MapReduce哪个阶段最费时间

**Shuffle阶段**最耗时：大量磁盘溢写 + 归并排序 + 网络传输。

### MapReduce中的Combine是干嘛的？有什么好处？

在Map端本地预聚合，减少传输到Reduce的数据量。

- 好处：减少网络传输、减轻ReduceTask压力、整体加快
- 要求：操作满足交换律和结合律（✅ sum/max，❌ avg）

### MapReduce为什么一定要有环形缓冲区

Map输出先写内存环形缓冲区（默认100MB），满80%再批量溢写磁盘。

避免每条数据都触发磁盘I/O，批量写效率高得多。环形设计可以边写边溢写，不阻塞。

### MapReduce为什么一定要有Shuffle过程

Map和Reduce之间需要**按key分组**：相同key的数据必须汇聚到同一个ReduceTask处理。Shuffle负责分区→排序→网络传输→归并，没有Shuffle就无法实现分布式聚合。

### MapReduce的Shuffle过程及其优化

**Map端：** Map输出 → 写环形缓冲区 → 满80%溢写（按分区快速排序）→ 多个溢写文件归并合并

**Reduce端：** HTTP拉取各MapTask输出 → 归并排序 → 传给Reducer

**优化：**

- 开启Combiner预聚合，减少传输量
- 压缩Map输出（`mapreduce.map.output.compress=true`，推荐Snappy）
- 调大环形缓冲区（`mapreduce.task.io.sort.mb`）

### Reduce怎么知道去哪里拉Map结果集？

ApplicationMaster追踪所有MapTask完成情况和输出位置。ReduceTask定期询问AM，获取已完成MapTask的输出位置（Host+端口），通过HTTP主动拉取。

### Reduce阶段都发生了什么，有没有进行分组

1. **拉取数据**：从各MapTask HTTP拉取属于本Reducer的分区数据
2. **归并排序**：将多份数据归并排序（相同key相邻）
3. **分组**：相同key的所有value形成一个Iterable（**有分组**）
4. **调用Reduce函数**：对每个key的value集合执行用户逻辑
5. **输出**：写入HDFS

### MapReduce Shuffle的排序算法

- **Map端溢写**：快速排序
- **Map端合并溢写文件**：归并排序
- **Reduce端合并拉取数据**：归并排序

### shuffle为什么要排序？

排序使相同key的数据**相邻**，Reduce端分组只需顺序扫描，无需额外哈希表，内存占用低，效率高。

### 说一下map是怎么到reduce的？

Map输出 → 写环形缓冲区 → 按分区排序 → 溢写磁盘 → 归并合并成一个有序文件 → Reduce通过HTTP拉取 → 归并排序 → 传给Reducer

### MapReduce的数据处理过程

Input → InputFormat切分 → RecordReader读取KV → Map函数 → Partitioner分区 → 排序 → Combiner（可选）→ Shuffle → Reduce函数 → OutputFormat → Output

### mapjoin的原理？应用场景？

**原理：** 将小表通过DistributedCache广播到所有MapTask的内存中，Map阶段直接与大表做join，**无需Reduce和Shuffle**。

> 类比：把城市编码表打印一份给每个工人，工人本地查表，不用汇总给主管。

**应用场景：** 大表 join 小表（小表能装入内存，如几百MB以内），可完全避免数据倾斜。

### reducejoin如何执行（原理）

1. 两张表数据都打上标记（标注来自哪张表）
2. 以join key为Map输出key，相同key的数据到同一Reducer
3. Reducer中按标记区分两张表，做匹配

缺点：所有数据都要Shuffle，数据量大时可能数据倾斜，性能不如MapJoin。

### MapReduce为什么不能产生过多小文件

- 每个小文件对应一个MapTask，JVM启动开销远大于实际计算
- 大量小文件消耗NameNode内存（每文件约150字节元数据）

### MapReduce分区及作用

分区决定Map输出的KV数据发送到哪个ReduceTask。

默认：`HashPartitioner`：`key.hashCode() % numReduceTasks`

保证相同key一定到同一Reducer。可自定义Partitioner实现业务分区。

### ReduceTask数量和分区数量关系

- ReduceTask == 分区数：✅ 正常
- ReduceTask > 分区数：多余的Task空转，产生空文件
- ReduceTask < 分区数：❌ 报错，部分分区数据无处写入

### Map的分片有多大

默认分片大小 = Block大小（128MB）。

分片大小 = `max(minSize, min(maxSize, blockSize))`

### reduce任务什么时候开始？

- **Shuffle拉取数据**：5%的MapTask完成后就开始拉
- **Reduce真正计算**：等所有MapTask完成后才开始

### MapReduce用了几次排序，分别是什么？

共**3次**：

1. **Map端溢写时**：快速排序（对缓冲区内数据）
2. **Map端合并溢写文件时**：归并排序
3. **Reduce端合并拉取数据时**：归并排序

### MapReduce怎么确定MapTask的数量？Map数量由什么决定

MapTask数量 = 输入数据的**Split数量**，一个Split对应一个MapTask。

Split数 = 输入文件大小 / 分片大小（默认=Block大小128MB）

小文件多时，每个文件至少一个Split，MapTask数会爆炸。

### MapReduce作业执行过程中，中间数据存在什么地方？

存在**本地磁盘**（非HDFS）。

Map输出先写内存环形缓冲区（100MB），超过80%溢写到**本地磁盘**，最终合并成本地文件。Reduce拉取后也先写本地磁盘归并，再传给Reducer计算。

### map输出数据超出缓冲区后，落地到磁盘还是HDFS？

**本地磁盘**（不是HDFS）。中间数据走本地磁盘效率更高，HDFS是最终输入输出用的。

### Map到Reduce默认的分区机制是什么？

默认`HashPartitioner`：`(key.hashCode() & Integer.MAX_VALUE) % numReduceTasks`

### MapReduce数据倾斜产生的原因及其解决方案

**原因：** key分布不均，某些key数据量远大于其他，对应Reducer处理时间远长。

> 类比：100人统计词频，"的"字出现100万次全汇给一个人，这人累死其他人都完了。

**解决方案：**

- **MapJoin**：小表广播内存，避免Reduce阶段（最彻底）
- **key加随机前缀**：打散热点key（加1-100随机数前缀），聚合后再二次聚合
- **自定义Partitioner**：将热点key均匀分配
- **Combiner预聚合**：减少传到Reducer的数据
- **过滤NULL或异常key**：提前过滤无效数据

### Map Join为什么能解决数据倾斜

MapJoin完全在Map端完成join，**没有Shuffle没有Reduce**，每个MapTask独立处理一部分数据并查询内存中的小表，数据天然均衡，不存在某节点数据集中的问题。

### MapReduce运行过程中会发生OOM，OOM发生的位置？

- **Map端**：环形缓冲区设置过大，或Map逻辑缓存了太多数据
- **Reduce端**：归并数据时内存不足，或Reduce逻辑缓存太多

解决：调大 `mapreduce.map/reduce.memory.mb` 和对应JVM堆内存参数。

### MapReduce压缩方式

- **Map输出压缩**：减少Shuffle传输量，推荐Snappy（快）
- **最终输出压缩**：减少HDFS存储，推荐Bzip2（可切分）或Gzip

配置：`mapreduce.map.output.compress=true`

### MapReduce中怎么处理一个大文件

- 确保文件**可切分**（避免不可切分的Gzip压缩）
- 使用`FileInputFormat`按Block自动切分
- 调大Map内存和超时时间
- 开启Combiner和Map输出压缩

---

## 🎯 YARN

> **整体类比：** 工厂人力资源部
> 
> - **ResourceManager** = 人事总监（管全厂资源）
> - **NodeManager** = 各车间主任（管自己车间）
> - **ApplicationMaster** = 项目经理（管一个具体项目，向总监要资源）
> - **Container** = 一个工位（固定CPU+内存）

### 介绍下YARN

YARN（Yet Another Resource Negotiator）是Hadoop的资源管理框架，将资源管理和作业调度分离，支持多计算框架（MapReduce/Spark/Flink）共享集群资源。

### YARN有几个模块

4个核心模块：

- **ResourceManager（RM）**：全局资源管理
- **NodeManager（NM）**：单节点资源管理
- **ApplicationMaster（AM）**：每个应用独立，申请资源+任务调度
- **Container**：资源封装单元（CPU + 内存）

### YARN工作机制

1. Client向RM提交应用
2. RM分配Container，启动AM（项目经理上班）
3. AM评估需要多少资源，向RM申请Container列表
4. RM分配Container，AM通知对应NM启动Container执行任务
5. 任务完成，AM向RM注销，资源释放

### YARN有什么优势，能解决什么问题？

解决Hadoop 1.x的JobTracker单点瓶颈（同时负责资源管理和任务调度）。

YARN优势：

- 职责分离，RM专注资源，AM专注应用
- 支持多框架共享集群（MR/Spark/Flink）
- 更好的扩展性（支持数万节点）

### YARN容错机制

- **RM故障**：ZooKeeper实现RM HA，Standby自动接管
- **NM故障**：RM检测到心跳超时，将该节点任务重新调度
- **AM故障**：RM重新启动AM（默认重试2次）
- **Container/Task故障**：AM检测到，重新申请Container重跑

### YARN高可用

Active RM + Standby RM + ZooKeeper（选主+状态存储）

Active故障时Standby自动切换。

### YARN调度器

同Hadoop调度器：FIFO / CapacityScheduler（默认）/ FairScheduler

### YARN中Container是如何启动的？

1. AM向RM申请到Container（包含Host、资源量）
2. AM直接联系对应NM，发送启动命令（包含命令、环境变量、资源文件）
3. NM在本地启动Container进程，设置CPU/内存限制（cgroups）
4. Container向AM汇报状态

### YARN的改进之处，Hadoop3.x相对于Hadoop 2.x？

- 支持GPU/FPGA资源调度
- Opportunistic Container（低优先级抢占式Container，提高利用率）
- 更好的RM HA
- Timeline Service v2（更好的监控和历史记录）

---

## 综合问题

### 为什么Spark比MapReduce快？

|      | MapReduce     | Spark       |
| ---- | ------------- | ----------- |
| 中间结果 | 每步落磁盘         | 放内存         |
| 类比   | 每算完一步存档，下步再读档 | 一直在内存算，最后才存 |
| 速度   | 慢             | 快10-100倍    |

磁盘比内存慢100倍以上，所以Spark快很多。另外Spark用DAG优化执行计划，减少不必要的shuffle。

### 宽依赖窄依赖

- **窄依赖**：父RDD每个分区只被子RDD**一个**分区使用（如map、filter）→ 可pipeline，不需要shuffle
- **宽依赖**：父RDD每个分区被子RDD**多个**分区使用（如groupByKey、join）→ 需要shuffle，是stage划分边界

> 类比：窄依赖 = 一个工人负责一道工序（流水线）；宽依赖 = 所有工人的结果都要汇总再重新分配（需要等待）

### 是否遇到过数据倾斜问题？如何解决的

症状：大多数Task很快完成，少数Task卡住很久。

排查：看Spark UI，找数据量异常大的Task。

解决：

1. 过滤NULL或异常key
2. 大表join小表用MapJoin（广播小表）
3. 热点key加随机前缀打散，聚合后去掉前缀二次聚合
4. 增大shuffle分区数（`spark.sql.shuffle.partitions`）
5. Spark 3.x开启AQE（自适应查询执行）自动处理

### Spark的shuffle有几种方式

- **HashShuffle**（已废弃）：按key哈希写文件，文件数=Map数×Reduce数，文件太多
- **SortShuffle**（默认）：先排序再写一个文件+索引，文件数=Map数，效率更高
- **TungstenSortShuffle**：SortShuffle优化版，使用堆外内存，减少GC

### Hadoop和Spark的主要区别。Spark为什么更有优势？

|      | Hadoop MR       | Spark                |
| ---- | --------------- | -------------------- |
| 计算模型 | 两阶段（Map+Reduce） | DAG多阶段               |
| 中间数据 | 落HDFS磁盘         | 内存（必要时spill磁盘）       |
| 速度   | 慢               | 快10-100倍             |
| 编程模型 | 只有Map/Reduce，复杂 | RDD/DataFrame/SQL，丰富 |
| 适合场景 | 超大规模单次批处理       | 迭代计算、交互查询、流处理        |

**数据超内存时**：Spark自动将RDD分区spill到本地磁盘，性能降低但仍可工作。

### 你如何进行大数据平台的性能调优？

1. **存储层**：列式存储（ORC/Parquet）+压缩，合并小文件
2. **计算层**：合理设置并行度，用MapJoin，开启Combiner
3. **资源配置**：合理分配内存/CPU，调整JVM参数
4. **SQL优化**：谓词下推、分区裁剪、避免SELECT *、减少shuffle
5. **数据倾斜**：加盐打散、广播join
6. **监控定位**：Spark UI/YARN UI找瓶颈任务

### 一个Hive SQL或Spark任务运行很慢，你会从哪些方面排查？

1. **执行计划**：`EXPLAIN`，看是否全表扫描、缺少分区裁剪
2. **数据倾斜**：看各Task数据量是否均匀（Spark UI）
3. **小文件**：Map数过多，每个Task数据量极小
4. **Shuffle量**：是否Shuffle了大量数据
5. **资源**：是否频繁GC，内存是否够用
6. **Join策略**：大表join是否可改为MapJoin

### 对实时流处理的理解。用过哪些流处理框架？

实时流处理：对持续产生的数据流做低延迟处理，相对批处理的T+1，可达秒级甚至毫秒级。

|      | Spark Streaming | Flink           |
| ---- | --------------- | --------------- |
| 处理方式 | 微批（把流切成小批次）     | 真流（逐条处理）        |
| 延迟   | 秒级              | 毫秒级             |
| 吞吐量  | 高               | 高               |
| 语义   | At-Least-Once为主 | Exactly-Once    |
| 适合   | 对延迟要求不极致，吞吐高    | 低延迟、精确计算（对账、风控） |

### 在大数据开发中，如何管理数据权限和保障数据安全？

- **认证**：Kerberos（确保只有合法用户可访问）
- **授权**：Apache Ranger（表/列/行级别细粒度权限控制）
- **传输加密**：TLS/SSL
- **存储加密**：HDFS透明加密（KMS管理密钥）
- **数据脱敏**：敏感字段（手机号、身份证）在查询层脱敏
- **审计日志**：记录所有访问操作，便于追溯

---

## 数据湖

### 你了解数据湖、数据湖仓一体这些概念吗？它们与传统数据仓库相比有何演进？

|      | 数据仓库                    | 数据湖                  | 湖仓一体（Lakehouse）             |
| ---- | ----------------------- | -------------------- | --------------------------- |
| 类比   | 整理好的档案室                 | 什么都往里扔的储物间           | 智能储物室（存得下又找得到）              |
| 数据格式 | 只存结构化                   | 任意格式                 | 任意格式                        |
| 写入方式 | Schema-on-Write（写时定义结构） | Schema-on-Read（读时定义） | Schema-on-Write（有管理）        |
| 查询   | 快，有索引                   | 慢，无组织                | 快（有索引+统计信息）                 |
| 成本   | 贵                       | 便宜（对象存储）             | 便宜                          |
| ACID | 支持                      | 不支持                  | 支持（Delta Lake/Hudi/Iceberg） |
| 缺点   | 灵活性差，不支持非结构化            | 容易变"数据沼泽"，难治理        | 相对复杂                        |

**演进路径：** 数仓（贵但好用）→ 数据湖（便宜但难用）→ 湖仓一体（既便宜又好用）

代表技术：Delta Lake（Databricks）、Apache Hudi（Uber）、Apache Iceberg（Netflix）[大数据面试题V3.0，约870篇牛客大数据面经480道面试题_牛客网](https://www.nowcoder.com/discuss/353159520220291072)

https://zhuanlan.zhihu.com/p/424296249 [大数据开发面经汇总【持续更新...】_牛客网](https://www.nowcoder.com/discuss/594817738107781120)

https://leetcode.cn/discuss/post/3516212/zi-jie-mian-jing-nian-xin-70wda-shu-ju-s-23r7/

[大数据开发面经_大数据面经-CSDN博客](https://blog.csdn.net/axzy5863/article/details/158429145)

[大数据开发（牛客）面试被问频率最高的几道面试题-腾讯云开发者社区-腾讯云](https://cloud.tencent.com/developer/article/2071876)

---

## 🐘 Hadoop整体理解

把Hadoop想象成一个**超大的仓库管理系统**：

- **HDFS** = 仓库（存东西）
- **MapReduce** = 工人（干活）
- **YARN** = 仓库主管（分配工人和资源）

---

## Hadoop基础

### 什么是Hadoop调度器？说明其工作方法

Hadoop 调度器（Hadoop Scheduler）通常指 YARN Resource Scheduler（在 Hadoop 2.x 之后 Hadoop Scheduler 本质上就是 YARN Scheduler） 中的资源调度组件，负责决定 集群中的 CPU、内存等计算[大数据面试题V3.0，约870篇牛客大数据面经480道面试题_牛客网](https://www.nowcoder.com/discuss/353159520220291072)

https://zhuanlan.zhihu.com/p/424296249 [大数据开发面经汇总【持续更新...】_牛客网](https://www.nowcoder.com/discuss/594817738107781120)

https://leetcode.cn/discuss/post/3516212/zi-jie-mian-jing-nian-xin-70wda-shu-ju-s-23r7/

[大数据开发面经_大数据面经-CSDN博客](https://blog.csdn.net/axzy5863/article/details/158429145)

[大数据开发（牛客）面试被问频率最高的几道面试题-腾讯云开发者社区-腾讯云](https://cloud.tencent.com/developer/article/2071876)

---

## 🐘 Hadoop整体理解

把Hadoop想象成一个**超大的仓库管理系统**：

- **HDFS** = 仓库（存东西）
- **MapReduce** = 工人（干活）
- **YARN** = 仓库主管（分配工人和资源）

---

## Hadoop基础

### 什么是Hadoop调度器？说明其工作方法

Hadoop 调度器（Hadoop Scheduler）通常指 YARN Resource Scheduler（在 Hadoop 2.x 之后 Hadoop Scheduler 本质上就是 YARN Scheduler） 中的资源调度组件，负责决定 集群中的 CPU、内存等计算资源如何分配给各个应用程序（如 MapReduce、Spark、Hive 任务）。当多个用户或任务同时提交作业时，调度器决定谁先运行、谁使用多少资源、资源如何公平分配。

用户提交任务

三种调度器：

| 调度器               | 机制                 | 适用场景    |
| ----------------- | ------------------ | ------- |
| FIFO              | 先进先出               | 简单单用户系统 |
| CapacityScheduler | 多队列 + 优先级高、占资源少的先跑 | 大型企业    |
| FairScheduler     | 尽量公平分配资源           | 多用户共享   |

**FIFO**：

**CapacityScheduler**：

**FairScheduler**：

### 为什么需要调度器？

1、资源有限：Hadoop 集群资源，没有调度器的话：所有任务都在抢资源、可能有的任务占满集群、其他任务一直等待，调度器让系统 可控分配资源。

2、多用户共享：企业 Hadoop 经常是 共享集群（数据开发、算法团队、BI团队）

3、保证公平：让短任务快速运行

4、提高集群利用率：调度器可以实现资源借用、资源借用。提高 Cluster Utilization（集群利用率）

### 什么时候

### hadoop框架的理解、Hadoop的特点

Hadoop = **HDFS**（分布式存储）+ **MapReduce**（分布式计算）+ **YARN**（资源管理）

特点：**高可靠**（多副本容错）、**高扩展**（加机器就能扩容）、**高容错**（节点挂了自动恢复）、**低成本**（普通硬件即可）

### Hadoop生态圈组件及其作用

| 组件        | 作用                     |
| --------- | ---------------------- |
| HDFS      | 分布式文件存储                |
| MapReduce | 分布式批处理计算               |
| YARN      | 资源调度与管理                |
| Hive      | SQL查询工具（SQL转MapReduce） |
| HBase     | 分布式列式NoSQL数据库          |
| ZooKeeper | 分布式协调服务（选主、配置管理）       |
| Kafka     | 高吞吐消息队列                |
| Flume     | 日志采集                   |
| Sqoop     | 关系型数据库与HDFS互导          |
| Spark     | 内存计算引擎，比MR快            |

### Hadoop 1.x，2.x，3.x的区别

- **1.x**：JobTracker同时负责资源管理和任务调度，单点瓶颈；没有HA
- **2.x**：引入YARN把资源管理分出去；HDFS支持NameNode HA和Federation
- **3.x**：支持多个NameNode；引入**纠删码（EC）**替代副本节省存储约50%；支持GPU资源调度

### Hadoop集群工作时启动哪些进程？它们有什么作用？

- **NameNode**：管理HDFS元数据（文件在哪、有几个副本），不存实际数据
- **DataNode**：存储实际数据块，定期向NameNode发心跳汇报状态
- **ResourceManager**：管整个集群资源，接受Job提交，分配资源
- **NodeManager**：管单个节点资源，启动和监控Container
- **SecondaryNameNode**（非HA模式）：辅助NameNode合并日志，**不是**NameNode备份

### 在集群计算的时候，什么是集群的主要瓶颈

**磁盘I/O**是主要瓶颈，尤其是MapReduce的Shuffle阶段（大量数据溢写磁盘+网络传输）。其次是**网络带宽**。

### 搭建Hadoop集群的xml文件有哪些？

- `core-site.xml`：核心配置（HDFS地址等）
- `hdfs-site.xml`：HDFS配置（副本数、块大小等）
- `mapred-site.xml`：MapReduce配置
- `yarn-site.xml`：YARN配置

### Hadoop的checkpoint流程

> **类比：** 就像把流水账（editlog）定期整理成账本快照（fsimage），防止流水账越来越长。

1. SecondaryNameNode从NameNode拉取editlog和fsimage
2. 将editlog回放合并到fsimage，生成新fsimage
3. 将新fsimage推回NameNode，清空旧editlog

作用：防止editlog无限增长，加快NameNode重启速度。

### Hadoop的默认块大小是多少？为什么设置这么大？

默认**128MB**（Hadoop 2.x起）。

原因：磁盘寻址时间约10ms，传输速率约100MB/s，128MB传输约1.28秒，寻址时间占比约1%，效率最优。

- 太小 → Map任务数多，启动开销大
- 太大 → Map并行度低

### Block划分的原因

- 大文件切块后可**多节点并行处理**
- Block分散到各DataNode，**负载均衡**
- 单个Block损坏只需恢复该Block，**容错代价小**

### Hadoop常见的压缩算法？

| 算法     | 是否可切分   | 速度  | 压缩比 | 适用场景       |
| ------ | ------- | --- | --- | ---------- |
| Gzip   | ❌       | 中   | 高   | 冷数据存储      |
| Bzip2  | ✅       | 慢   | 最高  | 需切分的归档     |
| Snappy | ❌       | 最快  | 中   | Map输出、中间数据 |
| LZO    | ✅（需建索引） | 快   | 中   | 大文件、需切分场景  |

> 注意：不可切分的压缩格式（如Gzip）大文件只能一个Map处理，并行度差。

### Hadoop作业提交到YARN的流程？

1. Client向ResourceManager提交Job（上传JAR到HDFS）
2. RM分配Container，启动**ApplicationMaster**
3. AM向RM申请运行MapTask/ReduceTask的Container
4. AM联系NodeManager，在Container中启动任务
5. 任务完成，AM向RM注销，资源释放

### Hadoop的Combiner的作用

在**Map端本地预聚合**，减少传输到Reduce的数据量。

> **类比：** 100人统计词频，传纸条前先自己合并，传"hadoop:50"而不是50张"hadoop:1"。

要求操作满足交换律和结合律：✅ sum/max/min，❌ avg（会丢信息）

### Hadoop序列化和反序列化

Hadoop用`Writable`接口（非Java原生序列化），更紧凑高效，节省带宽。

常用类型：`IntWritable`、`LongWritable`、`Text`、`NullWritable`

### Hadoop的运行模式

- **本地模式**：单机单JVM，无HDFS，用于开发调试
- **伪分布式**：单机模拟集群
- **完全分布式**：多节点，生产环境

### Hadoop小文件处理问题

**问题：** 每个小文件占NameNode约150字节内存；每个小文件启动一个MapTask，启动开销远大于计算本身。

**解决：**

- **CombineFileInputFormat**：合并小文件再处理
- **SequenceFile**：将小文件以KV形式合并存储
- **HAR归档**：打包小文件
- 上游控制，避免产生小文件（如Hive设置合并输出）

### Hadoop为什么要从2.x升级到3.x？

- **纠删码**：存储开销从200%降至约50%，节省大量存储成本
- **多NameNode**：突破单NameNode扩展瓶颈
- **支持GPU/FPGA**资源调度

### Hadoop的优缺点

- **优点**：高容错、低成本、高扩展、适合PB级批量处理
- **缺点**：延迟高（不适合实时）、小文件问题、不支持随机写、不适合迭代计算

---

## 📦 HDFS

> **整体类比：** 图书馆管理系统
> 
> - NameNode = 图书馆目录（记录书在哪，但不存书）
> - DataNode = 书架（真正放书的地方）
> - Block = 把大书撕成若干份（128MB一份）
> - 副本数3 = 每份复印3本放不同书架，防止丢失

### HDFS NameNode高可用如何实现？需要哪些角色？

架构：**Active NameNode + Standby NameNode**

| 角色                 | 作用                           |
| ------------------ | ---------------------------- |
| Active NameNode    | 对外提供服务                       |
| Standby NameNode   | 热备，实时同步editlog               |
| JournalNode集群（≥3个） | 共享editlog，Active写入，Standby读取 |
| ZooKeeper          | 选主，记录谁是Active                |
| ZKFC               | 监控NameNode健康，触发自动切换          |

### HDFS中向DataNode写数据失败了怎么办

1. 将失败的DataNode从pipeline中移除
2. 已写数据标记为损坏
3. NameNode重新分配新DataNode，重建pipeline继续写
4. 写完后NameNode发现副本数不足，触发后台重新复制

### DataNode什么情况下不会备份

强制关闭或非正常断电时。

### HDFS中DataNode怎么存储数据的

- 数据以**Block文件**存在本地磁盘
- 每个Block对应一个`.meta`校验文件（CRC）
- DataNode每3秒向NameNode发**心跳**，每6小时发**块报告**

### NameNode存数据吗？

**不存实际数据**，只存**元数据**：文件目录树、文件与Block的映射、权限等。

持久化方式：`fsimage`（全量快照）+ `editlog`（操作日志）

### HDFS文件写入和读取流程

**写入流程：**

1. Client → NameNode：申请创建文件
2. NameNode返回DataNode列表（DN1→DN2→DN3 流水线）
3. Client将数据切Block，按流水线依次写入（DN1写完传给DN2，DN2传给DN3）
4. 每个packet写完，ack沿流水线反向回传给Client
5. 全部写完，Client通知NameNode完成

**读取流程：**

1. Client → NameNode：请求读文件
2. NameNode返回各Block所在DataNode列表（按距离排序）
3. Client就近选DataNode读取每个Block
4. CRC校验，损坏则自动切换其他副本

### HDFS优缺点及使用场景

- **优点**：高容错、高吞吐（流式读取）、低成本、可扩展
- **缺点**：高延迟、不适合小文件、不支持随机写、不支持并发写
- **使用场景**：日志存储、数据仓库原始数据、离线批处理

### HDFS的容错机制

- **心跳检测**：DataNode超时未发心跳，NameNode触发副本重建
- **CRC校验**：读写时检测数据损坏，自动切换副本
- **多副本**：默认3副本，一个节点坏了不影响数据
- **NameNode HA**：元数据不丢失

### HDFS的副本机制

默认**3副本**放置策略：

- 第1副本：客户端所在节点
- 第2副本：**不同机架**的节点
- 第3副本：与第2副本**同机架**不同节点

兼顾可靠性（跨机架防机架故障）和网络效率。

### HDFS的常见数据格式，列式存储格式和行存储格式异同点，列式存储优点有哪些？

**行存储**：一行数据连续存储，适合OLTP（增删改查整行）

**列式存储**：同一列数据连续存储，适合OLAP（只读少数列的聚合分析）

**列式存储优点：**

- 压缩比高（同列数据类型相同，压缩效果好）
- I/O少（只读需要的列，跳过无关数据）
- 聚合计算快（sum/count等）

常见格式：TextFile（行）、SequenceFile（行）、ORC（列）、Parquet（列）

### HDFS的默认副本数？为什么？如何修改？

默认**3副本**：在可靠性和存储成本之间取平衡（容忍2个节点同时故障）。

修改：

- `hdfs-site.xml` 中 `dfs.replication=3`
- 或命令：`hdfs dfs -setrep -w 2 /path/to/file`

### HDFS的块默认大小，64M和128M是在哪个版本更换的？怎么修改默认块大小？

Hadoop **1.x默认64MB**，**2.x起改为128MB**。

修改：`hdfs-site.xml` 中 `dfs.blocksize=134217728`（单位字节）

### HDFS的block为什么是128M？增大或减小有什么影响？

磁盘寻址约10ms，传输速率约100MB/s，128MB传输约1.28秒，寻址时间占比约1%，效率最优。

- **增大**：Map并行度降低，适合超大文件
- **减小**：Map任务数增多，启动开销大，NameNode元数据增多

### HDFS HA怎么实现？是个什么架构？

见上方"NameNode高可用"部分：Active NN + Standby NN + JournalNode集群 + ZooKeeper + ZKFC

### 导入大文件到HDFS时如何自定义分片？

实现自定义`InputFormat`，重写`getSplits()`方法。或调整参数：

- `mapreduce.input.fileinputformat.split.maxsize`
- `mapreduce.input.fileinputformat.split.minsize`

### HDFS的mapper和reducer的个数如何确定？reducer的个数依据是什么？

- **Mapper数**：由输入Split数决定，一个Split = 一个MapTask（默认Split大小 = Block大小）
- **Reducer数**：手动设置（`job.setNumReduceTasks(n)`），一般设为节点数×1.5~2倍

### HDFS跨节点怎么进行数据迁移

- `hadoop distcp`：分布式拷贝，适合集群间大量数据迁移（推荐）
- 跨集群：`hadoop distcp hdfs://cluster1/path hdfs://cluster2/path`

### HDFS的数据一致性靠什么保证？

- **写入时**：pipeline写入，所有副本ack后才确认写成功
- **读取时**：CRC校验，不一致自动切换副本
- **副本监控**：NameNode持续监控副本数，不足时触发重建

### HDFS怎么保证数据安全

- 多副本（数据冗余）
- CRC校验（检测损坏）
- Kerberos认证（身份验证）
- ACL权限控制（文件级权限）
- 传输加密（TLS）和存储加密（KMS）
- 审计日志

### HDFS写数据过程，写的过程中有哪些故障，分别会怎么处理？

写数据过程见上方"写入流程"。

故障处理：

- **某DataNode宕机**：从pipeline移除，用新DataNode替换，事后补足副本数
- **NameNode宕机（HA模式）**：Standby自动切为Active，Client重连继续写
- **网络超时**：packet重传，超时后报错，Client可重试

### 直接将数据文件上传到HDFS的表目录中，如何在表中查询到该数据？

- **非分区表**：直接可查，Hive会扫描目录下所有文件
- **分区表**：执行 `MSCK REPAIR TABLE 表名;` 刷新分区元数据，或手动 `ALTER TABLE 表名 ADD PARTITION (...)`

---

## ⚙️ MapReduce

> **整体类比：** 统计一本书里每个单词出现多少次
> 
> - **Map** = 把书分给100人，每人数自己那几页的词频，输出(词, 1)
> - **Shuffle** = 把所有"hadoop"汇给同一个人，"spark"汇给另一个人
> - **Reduce** = 每人把收到的同一词的数字加起来，得出最终结果

### 介绍下MapReduce

分布式批处理计算框架，将计算分为两阶段：

- **Map**：对输入数据做转换/过滤，输出KV对
- **Reduce**：对相同key的value做聚合

中间通过**Shuffle**（分区、排序、合并、网络传输）连接两个阶段。

### MapReduce优缺点

- **优点**：简单、高容错、适合超大规模离线批处理
- **缺点**：延迟高（中间结果落磁盘）、不适合实时、不适合迭代计算

### MapReduce工作原理

```
输入文件 → Split切分 → MapTask → 环形缓冲区
→ 溢写（分区+排序）→ 合并 → Shuffle（网络传输）
→ ReduceTask归并排序 → Reduce函数 → 输出文件
```

### MapReduce哪个阶段最费时间

**Shuffle阶段**最耗时：大量磁盘溢写 + 归并排序 + 网络传输。

### MapReduce中的Combine是干嘛的？有什么好处？

在Map端本地预聚合，减少传输到Reduce的数据量。

- 好处：减少网络传输、减轻ReduceTask压力、整体加快
- 要求：操作满足交换律和结合律（✅ sum/max，❌ avg）

### MapReduce为什么一定要有环形缓冲区

Map输出先写内存环形缓冲区（默认100MB），满80%再批量溢写磁盘。

避免每条数据都触发磁盘I/O，批量写效率高得多。环形设计可以边写边溢写，不阻塞。

### MapReduce为什么一定要有Shuffle过程

Map和Reduce之间需要**按key分组**：相同key的数据必须汇聚到同一个ReduceTask处理。Shuffle负责分区→排序→网络传输→归并，没有Shuffle就无法实现分布式聚合。

### MapReduce的Shuffle过程及其优化

**Map端：** Map输出 → 写环形缓冲区 → 满80%溢写（按分区快速排序）→ 多个溢写文件归并合并

**Reduce端：** HTTP拉取各MapTask输出 → 归并排序 → 传给Reducer

**优化：**

- 开启Combiner预聚合，减少传输量
- 压缩Map输出（`mapreduce.map.output.compress=true`，推荐Snappy）
- 调大环形缓冲区（`mapreduce.task.io.sort.mb`）

### Reduce怎么知道去哪里拉Map结果集？

ApplicationMaster追踪所有MapTask完成情况和输出位置。ReduceTask定期询问AM，获取已完成MapTask的输出位置（Host+端口），通过HTTP主动拉取。

### Reduce阶段都发生了什么，有没有进行分组

1. **拉取数据**：从各MapTask HTTP拉取属于本Reducer的分区数据
2. **归并排序**：将多份数据归并排序（相同key相邻）
3. **分组**：相同key的所有value形成一个Iterable（**有分组**）
4. **调用Reduce函数**：对每个key的value集合执行用户逻辑
5. **输出**：写入HDFS

### MapReduce Shuffle的排序算法

- **Map端溢写**：快速排序
- **Map端合并溢写文件**：归并排序
- **Reduce端合并拉取数据**：归并排序

### shuffle为什么要排序？

排序使相同key的数据**相邻**，Reduce端分组只需顺序扫描，无需额外哈希表，内存占用低，效率高。

### 说一下map是怎么到reduce的？

Map输出 → 写环形缓冲区 → 按分区排序 → 溢写磁盘 → 归并合并成一个有序文件 → Reduce通过HTTP拉取 → 归并排序 → 传给Reducer

### MapReduce的数据处理过程

Input → InputFormat切分 → RecordReader读取KV → Map函数 → Partitioner分区 → 排序 → Combiner（可选）→ Shuffle → Reduce函数 → OutputFormat → Output

### mapjoin的原理？应用场景？

**原理：** 将小表通过DistributedCache广播到所有MapTask的内存中，Map阶段直接与大表做join，**无需Reduce和Shuffle**。

> 类比：把城市编码表打印一份给每个工人，工人本地查表，不用汇总给主管。

**应用场景：** 大表 join 小表（小表能装入内存，如几百MB以内），可完全避免数据倾斜。

### reducejoin如何执行（原理）

1. 两张表数据都打上标记（标注来自哪张表）
2. 以join key为Map输出key，相同key的数据到同一Reducer
3. Reducer中按标记区分两张表，做匹配

缺点：所有数据都要Shuffle，数据量大时可能数据倾斜，性能不如MapJoin。

### MapReduce为什么不能产生过多小文件

- 每个小文件对应一个MapTask，JVM启动开销远大于实际计算
- 大量小文件消耗NameNode内存（每文件约150字节元数据）

### MapReduce分区及作用

分区决定Map输出的KV数据发送到哪个ReduceTask。

默认：`HashPartitioner`：`key.hashCode() % numReduceTasks`

保证相同key一定到同一Reducer。可自定义Partitioner实现业务分区。

### ReduceTask数量和分区数量关系

- ReduceTask == 分区数：✅ 正常
- ReduceTask > 分区数：多余的Task空转，产生空文件
- ReduceTask < 分区数：❌ 报错，部分分区数据无处写入

### Map的分片有多大

默认分片大小 = Block大小（128MB）。

分片大小 = `max(minSize, min(maxSize, blockSize))`

### reduce任务什么时候开始？

- **Shuffle拉取数据**：5%的MapTask完成后就开始拉
- **Reduce真正计算**：等所有MapTask完成后才开始

### MapReduce用了几次排序，分别是什么？

共**3次**：

1. **Map端溢写时**：快速排序（对缓冲区内数据）
2. **Map端合并溢写文件时**：归并排序
3. **Reduce端合并拉取数据时**：归并排序

### MapReduce怎么确定MapTask的数量？Map数量由什么决定

MapTask数量 = 输入数据的**Split数量**，一个Split对应一个MapTask。

Split数 = 输入文件大小 / 分片大小（默认=Block大小128MB）

小文件多时，每个文件至少一个Split，MapTask数会爆炸。

### MapReduce作业执行过程中，中间数据存在什么地方？

存在**本地磁盘**（非HDFS）。

Map输出先写内存环形缓冲区（100MB），超过80%溢写到**本地磁盘**，最终合并成本地文件。Reduce拉取后也先写本地磁盘归并，再传给Reducer计算。

### map输出数据超出缓冲区后，落地到磁盘还是HDFS？

**本地磁盘**（不是HDFS）。中间数据走本地磁盘效率更高，HDFS是最终输入输出用的。

### Map到Reduce默认的分区机制是什么？

默认`HashPartitioner`：`(key.hashCode() & Integer.MAX_VALUE) % numReduceTasks`

### MapReduce数据倾斜产生的原因及其解决方案

**原因：** key分布不均，某些key数据量远大于其他，对应Reducer处理时间远长。

> 类比：100人统计词频，"的"字出现100万次全汇给一个人，这人累死其他人都完了。

**解决方案：**

- **MapJoin**：小表广播内存，避免Reduce阶段（最彻底）
- **key加随机前缀**：打散热点key（加1-100随机数前缀），聚合后再二次聚合
- **自定义Partitioner**：将热点key均匀分配
- **Combiner预聚合**：减少传到Reducer的数据
- **过滤NULL或异常key**：提前过滤无效数据

### Map Join为什么能解决数据倾斜

MapJoin完全在Map端完成join，**没有Shuffle没有Reduce**，每个MapTask独立处理一部分数据并查询内存中的小表，数据天然均衡，不存在某节点数据集中的问题。

### MapReduce运行过程中会发生OOM，OOM发生的位置？

- **Map端**：环形缓冲区设置过大，或Map逻辑缓存了太多数据
- **Reduce端**：归并数据时内存不足，或Reduce逻辑缓存太多

解决：调大 `mapreduce.map/reduce.memory.mb` 和对应JVM堆内存参数。

### MapReduce压缩方式

- **Map输出压缩**：减少Shuffle传输量，推荐Snappy（快）
- **最终输出压缩**：减少HDFS存储，推荐Bzip2（可切分）或Gzip

配置：`mapreduce.map.output.compress=true`

### MapReduce中怎么处理一个大文件

- 确保文件**可切分**（避免不可切分的Gzip压缩）
- 使用`FileInputFormat`按Block自动切分
- 调大Map内存和超时时间
- 开启Combiner和Map输出压缩

---

## 🎯 YARN

> **整体类比：** 工厂人力资源部
> 
> - **ResourceManager** = 人事总监（管全厂资源）
> - **NodeManager** = 各车间主任（管自己车间）
> - **ApplicationMaster** = 项目经理（管一个具体项目，向总监要资源）
> - **Container** = 一个工位（固定CPU+内存）

### 介绍下YARN

YARN（Yet Another Resource Negotiator）是Hadoop的资源管理框架，将资源管理和作业调度分离，支持多计算框架（MapReduce/Spark/Flink）共享集群资源。

### YARN有几个模块

4个核心模块：

- **ResourceManager（RM）**：全局资源管理
- **NodeManager（NM）**：单节点资源管理
- **ApplicationMaster（AM）**：每个应用独立，申请资源+任务调度
- **Container**：资源封装单元（CPU + 内存）

### YARN工作机制

1. Client向RM提交应用
2. RM分配Container，启动AM（项目经理上班）
3. AM评估需要多少资源，向RM申请Container列表
4. RM分配Container，AM通知对应NM启动Container执行任务
5. 任务完成，AM向RM注销，资源释放

### YARN有什么优势，能解决什么问题？

解决Hadoop 1.x的JobTracker单点瓶颈（同时负责资源管理和任务调度）。

YARN优势：

- 职责分离，RM专注资源，AM专注应用
- 支持多框架共享集群（MR/Spark/Flink）
- 更好的扩展性（支持数万节点）

### YARN容错机制

- **RM故障**：ZooKeeper实现RM HA，Standby自动接管
- **NM故障**：RM检测到心跳超时，将该节点任务重新调度
- **AM故障**：RM重新启动AM（默认重试2次）
- **Container/Task故障**：AM检测到，重新申请Container重跑

### YARN高可用

Active RM + Standby RM + ZooKeeper（选主+状态存储）

Active故障时Standby自动切换。

### YARN调度器

同Hadoop调度器：FIFO / CapacityScheduler（默认）/ FairScheduler

### YARN中Container是如何启动的？

1. AM向RM申请到Container（包含Host、资源量）
2. AM直接联系对应NM，发送启动命令（包含命令、环境变量、资源文件）
3. NM在本地启动Container进程，设置CPU/内存限制（cgroups）
4. Container向AM汇报状态

### YARN的改进之处，Hadoop3.x相对于Hadoop 2.x？

- 支持GPU/FPGA资源调度
- Opportunistic Container（低优先级抢占式Container，提高利用率）
- 更好的RM HA
- Timeline Service v2（更好的监控和历史记录）

---

## 综合问题

### 为什么Spark比MapReduce快？

|      | MapReduce     | Spark       |
| ---- | ------------- | ----------- |
| 中间结果 | 每步落磁盘         | 放内存         |
| 类比   | 每算完一步存档，下步再读档 | 一直在内存算，最后才存 |
| 速度   | 慢             | 快10-100倍    |

磁盘比内存慢100倍以上，所以Spark快很多。另外Spark用DAG优化执行计划，减少不必要的shuffle。

### 宽依赖窄依赖

- **窄依赖**：父RDD每个分区只被子RDD**一个**分区使用（如map、filter）→ 可pipeline，不需要shuffle
- **宽依赖**：父RDD每个分区被子RDD**多个**分区使用（如groupByKey、join）→ 需要shuffle，是stage划分边界

> 类比：窄依赖 = 一个工人负责一道工序（流水线）；宽依赖 = 所有工人的结果都要汇总再重新分配（需要等待）

### 是否遇到过数据倾斜问题？如何解决的

症状：大多数Task很快完成，少数Task卡住很久。

排查：看Spark UI，找数据量异常大的Task。

解决：

1. 过滤NULL或异常key
2. 大表join小表用MapJoin（广播小表）
3. 热点key加随机前缀打散，聚合后去掉前缀二次聚合
4. 增大shuffle分区数（`spark.sql.shuffle.partitions`）
5. Spark 3.x开启AQE（自适应查询执行）自动处理

### Spark的shuffle有几种方式

- **HashShuffle**（已废弃）：按key哈希写文件，文件数=Map数×Reduce数，文件太多
- **SortShuffle**（默认）：先排序再写一个文件+索引，文件数=Map数，效率更高
- **TungstenSortShuffle**：SortShuffle优化版，使用堆外内存，减少GC

### Hadoop和Spark的主要区别。Spark为什么更有优势？

|      | Hadoop MR       | Spark                |
| ---- | --------------- | -------------------- |
| 计算模型 | 两阶段（Map+Reduce） | DAG多阶段               |
| 中间数据 | 落HDFS磁盘         | 内存（必要时spill磁盘）       |
| 速度   | 慢               | 快10-100倍             |
| 编程模型 | 只有Map/Reduce，复杂 | RDD/DataFrame/SQL，丰富 |
| 适合场景 | 超大规模单次批处理       | 迭代计算、交互查询、流处理        |

**数据超内存时**：Spark自动将RDD分区spill到本地磁盘，性能降低但仍可工作。

### 你如何进行大数据平台的性能调优？

1. **存储层**：列式存储（ORC/Parquet）+压缩，合并小文件
2. **计算层**：合理设置并行度，用MapJoin，开启Combiner
3. **资源配置**：合理分配内存/CPU，调整JVM参数
4. **SQL优化**：谓词下推、分区裁剪、避免SELECT *、减少shuffle
5. **数据倾斜**：加盐打散、广播join
6. **监控定位**：Spark UI/YARN UI找瓶颈任务

### 一个Hive SQL或Spark任务运行很慢，你会从哪些方面排查？

1. **执行计划**：`EXPLAIN`，看是否全表扫描、缺少分区裁剪
2. **数据倾斜**：看各Task数据量是否均匀（Spark UI）
3. **小文件**：Map数过多，每个Task数据量极小
4. **Shuffle量**：是否Shuffle了大量数据
5. **资源**：是否频繁GC，内存是否够用
6. **Join策略**：大表join是否可改为MapJoin

### 对实时流处理的理解。用过哪些流处理框架？

实时流处理：对持续产生的数据流做低延迟处理，相对批处理的T+1，可达秒级甚至毫秒级。

|      | Spark Streaming | Flink           |
| ---- | --------------- | --------------- |
| 处理方式 | 微批（把流切成小批次）     | 真流（逐条处理）        |
| 延迟   | 秒级              | 毫秒级             |
| 吞吐量  | 高               | 高               |
| 语义   | At-Least-Once为主 | Exactly-Once    |
| 适合   | 对延迟要求不极致，吞吐高    | 低延迟、精确计算（对账、风控） |

### 在大数据开发中，如何管理数据权限和保障数据安全？

- **认证**：Kerberos（确保只有合法用户可访问）
- **授权**：Apache Ranger（表/列/行级别细粒度权限控制）
- **传输加密**：TLS/SSL
- **存储加密**：HDFS透明加密（KMS管理密钥）
- **数据脱敏**：敏感字段（手机号、身份证）在查询层脱敏
- **审计日志**：记录所有访问操作，便于追溯

---

## 数据湖

### 你了解数据湖、数据湖仓一体这些概念吗？它们与传统数据仓库相比有何演进？

|      | 数据仓库                    | 数据湖                  | 湖仓一体（Lakehouse）             |
| ---- | ----------------------- | -------------------- | --------------------------- |
| 类比   | 整理好的档案室                 | 什么都往里扔的储物间           | 智能储物室（存得下又找得到）              |
| 数据格式 | 只存结构化                   | 任意格式                 | 任意格式                        |
| 写入方式 | Schema-on-Write（写时定义结构） | Schema-on-Read（读时定义） | Schema-on-Write（有管理）        |
| 查询   | 快，有索引                   | 慢，无组织                | 快（有索引+统计信息）                 |
| 成本   | 贵                       | 便宜（对象存储）             | 便宜                          |
| ACID | 支持                      | 不支持                  | 支持（Delta Lake/Hudi/Iceberg） |
| 缺点   | 灵活性差，不支持非结构化            | 容易变"数据沼泽"，难治理        | 相对复杂                        |

**演进路径：** 数仓（贵但好用）→ 数据湖（便宜但难用）→ 湖仓一体（既便宜又好用）

代表技术：Delta Lake（Databricks）、Apache Hudi（Uber）、Apache Iceberg（Netflix）[大数据面试题V3.0，约870篇牛客大数据面经480道面试题_牛客网](https://www.nowcoder.com/discuss/353159520220291072)

https://zhuanlan.zhihu.com/p/424296249 [大数据开发面经汇总【持续更新...】_牛客网](https://www.nowcoder.com/discuss/594817738107781120)

https://leetcode.cn/discuss/post/3516212/zi-jie-mian-jing-nian-xin-70wda-shu-ju-s-23r7/

[大数据开发面经_大数据面经-CSDN博客](https://blog.csdn.net/axzy5863/article/details/158429145)

[大数据开发（牛客）面试被问频率最高的几道面试题-腾讯云开发者社区-腾讯云](https://cloud.tencent.com/developer/article/2071876)

---

## 🐘 Hadoop整体理解

把Hadoop想象成一个**超大的仓库管理系统**：

- **HDFS** = 仓库（存东西）
- **MapReduce** = 工人（干活）
- **YARN** = 仓库主管（分配工人和资源）

---

## Hadoop基础

### 什么是Hadoop调度器？说明其工作方法

Hadoop 调度器（Hadoop Scheduler）通常指 Hadoop YARN （Yet Another Resource Negotiator） 中的资源调度组件，负责决定 集群中的 CPU、内存等计算资源如何分配给各个应用程序（如 MapReduce、Spark、Hive 任务）。当多个用户或任务同时提交作业时，调度器决定谁先运行、谁使用多少资源、资源如何公平分配。

没有调度器的话：所有任务都在抢资源、可能有的任务占满集群、其他任务一直等待
三种调度器：

| 调度器               | 机制   | 适用场景 |
| ----------------- | ---- | ---- |
| FIFO              | 先进先出 |      |
| CapacityScheduler |      |      |
| FairScheduler     |      |      |

- **FIFO**：先进先出，按提交顺序排队执行，简单但资源利用率低
- **CapacityScheduler（默认）**：多队列，按队列容量分配资源，优先级高、占资源少的先跑
- **FairScheduler**：同一队列内所有作业公平共享资源，动态均衡

### hadoop框架的理解、Hadoop的特点

Hadoop = **HDFS**（分布式存储）+ **MapReduce**（分布式计算）+ **YARN**（资源管理）

特点：**高可靠**（多副本容错）、**高扩展**（加机器就能扩容）、**高容错**（节点挂了自动恢复）、**低成本**（普通硬件即可）

### Hadoop生态圈组件及其作用

| 组件        | 作用                     |
| --------- | ---------------------- |
| HDFS      | 分布式文件存储                |
| MapReduce | 分布式批处理计算               |
| YARN      | 资源调度与管理                |
| Hive      | SQL查询工具（SQL转MapReduce） |
| HBase     | 分布式列式NoSQL数据库          |
| ZooKeeper | 分布式协调服务（选主、配置管理）       |
| Kafka     | 高吞吐消息队列                |
| Flume     | 日志采集                   |
| Sqoop     | 关系型数据库与HDFS互导          |
| Spark     | 内存计算引擎，比MR快            |

### Hadoop 1.x，2.x，3.x的区别

- **1.x**：JobTracker同时负责资源管理和任务调度，单点瓶颈；没有HA
- **2.x**：引入YARN把资源管理分出去；HDFS支持NameNode HA和Federation
- **3.x**：支持多个NameNode；引入**纠删码（EC）**替代副本节省存储约50%；支持GPU资源调度

### Hadoop集群工作时启动哪些进程？它们有什么作用？

- **NameNode**：管理HDFS元数据（文件在哪、有几个副本），不存实际数据
- **DataNode**：存储实际数据块，定期向NameNode发心跳汇报状态
- **ResourceManager**：管整个集群资源，接受Job提交，分配资源
- **NodeManager**：管单个节点资源，启动和监控Container
- **SecondaryNameNode**（非HA模式）：辅助NameNode合并日志，**不是**NameNode备份

### 在集群计算的时候，什么是集群的主要瓶颈

**磁盘I/O**是主要瓶颈，尤其是MapReduce的Shuffle阶段（大量数据溢写磁盘+网络传输）。其次是**网络带宽**。

### 搭建Hadoop集群的xml文件有哪些？

- `core-site.xml`：核心配置（HDFS地址等）
- `hdfs-site.xml`：HDFS配置（副本数、块大小等）
- `mapred-site.xml`：MapReduce配置
- `yarn-site.xml`：YARN配置

### Hadoop的checkpoint流程

> **类比：** 就像把流水账（editlog）定期整理成账本快照（fsimage），防止流水账越来越长。

1. SecondaryNameNode从NameNode拉取editlog和fsimage
2. 将editlog回放合并到fsimage，生成新fsimage
3. 将新fsimage推回NameNode，清空旧editlog

作用：防止editlog无限增长，加快NameNode重启速度。

### Hadoop的默认块大小是多少？为什么设置这么大？

默认**128MB**（Hadoop 2.x起）。

原因：磁盘寻址时间约10ms，传输速率约100MB/s，128MB传输约1.28秒，寻址时间占比约1%，效率最优。

- 太小 → Map任务数多，启动开销大
- 太大 → Map并行度低

### Block划分的原因

- 大文件切块后可**多节点并行处理**
- Block分散到各DataNode，**负载均衡**
- 单个Block损坏只需恢复该Block，**容错代价小**

### Hadoop常见的压缩算法？

| 算法     | 是否可切分   | 速度  | 压缩比 | 适用场景       |
| ------ | ------- | --- | --- | ---------- |
| Gzip   | ❌       | 中   | 高   | 冷数据存储      |
| Bzip2  | ✅       | 慢   | 最高  | 需切分的归档     |
| Snappy | ❌       | 最快  | 中   | Map输出、中间数据 |
| LZO    | ✅（需建索引） | 快   | 中   | 大文件、需切分场景  |

> 注意：不可切分的压缩格式（如Gzip）大文件只能一个Map处理，并行度差。

### Hadoop作业提交到YARN的流程？

1. Client向ResourceManager提交Job（上传JAR到HDFS）
2. RM分配Container，启动**ApplicationMaster**
3. AM向RM申请运行MapTask/ReduceTask的Container
4. AM联系NodeManager，在Container中启动任务
5. 任务完成，AM向RM注销，资源释放

### Hadoop的Combiner的作用

在**Map端本地预聚合**，减少传输到Reduce的数据量。

> **类比：** 100人统计词频，传纸条前先自己合并，传"hadoop:50"而不是50张"hadoop:1"。

要求操作满足交换律和结合律：✅ sum/max/min，❌ avg（会丢信息）

### Hadoop序列化和反序列化

Hadoop用`Writable`接口（非Java原生序列化），更紧凑高效，节省带宽。

常用类型：`IntWritable`、`LongWritable`、`Text`、`NullWritable`

### Hadoop的运行模式

- **本地模式**：单机单JVM，无HDFS，用于开发调试
- **伪分布式**：单机模拟集群
- **完全分布式**：多节点，生产环境

### Hadoop小文件处理问题

**问题：** 每个小文件占NameNode约150字节内存；每个小文件启动一个MapTask，启动开销远大于计算本身。

**解决：**

- **CombineFileInputFormat**：合并小文件再处理
- **SequenceFile**：将小文件以KV形式合并存储
- **HAR归档**：打包小文件
- 上游控制，避免产生小文件（如Hive设置合并输出）

### Hadoop为什么要从2.x升级到3.x？

- **纠删码**：存储开销从200%降至约50%，节省大量存储成本
- **多NameNode**：突破单NameNode扩展瓶颈
- **支持GPU/FPGA**资源调度

### Hadoop的优缺点

- **优点**：高容错、低成本、高扩展、适合PB级批量处理
- **缺点**：延迟高（不适合实时）、小文件问题、不支持随机写、不适合迭代计算

---

## 📦 HDFS

> **整体类比：** 图书馆管理系统
> 
> - NameNode = 图书馆目录（记录书在哪，但不存书）
> - DataNode = 书架（真正放书的地方）
> - Block = 把大书撕成若干份（128MB一份）
> - 副本数3 = 每份复印3本放不同书架，防止丢失

### HDFS NameNode高可用如何实现？需要哪些角色？

架构：**Active NameNode + Standby NameNode**

| 角色                 | 作用                           |
| ------------------ | ---------------------------- |
| Active NameNode    | 对外提供服务                       |
| Standby NameNode   | 热备，实时同步editlog               |
| JournalNode集群（≥3个） | 共享editlog，Active写入，Standby读取 |
| ZooKeeper          | 选主，记录谁是Active                |
| ZKFC               | 监控NameNode健康，触发自动切换          |

### HDFS中向DataNode写数据失败了怎么办

1. 将失败的DataNode从pipeline中移除
2. 已写数据标记为损坏
3. NameNode重新分配新DataNode，重建pipeline继续写
4. 写完后NameNode发现副本数不足，触发后台重新复制

### DataNode什么情况下不会备份

强制关闭或非正常断电时。

### HDFS中DataNode怎么存储数据的

- 数据以**Block文件**存在本地磁盘
- 每个Block对应一个`.meta`校验文件（CRC）
- DataNode每3秒向NameNode发**心跳**，每6小时发**块报告**

### NameNode存数据吗？

**不存实际数据**，只存**元数据**：文件目录树、文件与Block的映射、权限等。

持久化方式：`fsimage`（全量快照）+ `editlog`（操作日志）

### HDFS文件写入和读取流程

**写入流程：**

1. Client → NameNode：申请创建文件
2. NameNode返回DataNode列表（DN1→DN2→DN3 流水线）
3. Client将数据切Block，按流水线依次写入（DN1写完传给DN2，DN2传给DN3）
4. 每个packet写完，ack沿流水线反向回传给Client
5. 全部写完，Client通知NameNode完成

**读取流程：**

1. Client → NameNode：请求读文件
2. NameNode返回各Block所在DataNode列表（按距离排序）
3. Client就近选DataNode读取每个Block
4. CRC校验，损坏则自动切换其他副本

### HDFS优缺点及使用场景

- **优点**：高容错、高吞吐（流式读取）、低成本、可扩展
- **缺点**：高延迟、不适合小文件、不支持随机写、不支持并发写
- **使用场景**：日志存储、数据仓库原始数据、离线批处理

### HDFS的容错机制

- **心跳检测**：DataNode超时未发心跳，NameNode触发副本重建
- **CRC校验**：读写时检测数据损坏，自动切换副本
- **多副本**：默认3副本，一个节点坏了不影响数据
- **NameNode HA**：元数据不丢失

### HDFS的副本机制

默认**3副本**放置策略：

- 第1副本：客户端所在节点
- 第2副本：**不同机架**的节点
- 第3副本：与第2副本**同机架**不同节点

兼顾可靠性（跨机架防机架故障）和网络效率。

### HDFS的常见数据格式，列式存储格式和行存储格式异同点，列式存储优点有哪些？

**行存储**：一行数据连续存储，适合OLTP（增删改查整行）

**列式存储**：同一列数据连续存储，适合OLAP（只读少数列的聚合分析）

**列式存储优点：**

- 压缩比高（同列数据类型相同，压缩效果好）
- I/O少（只读需要的列，跳过无关数据）
- 聚合计算快（sum/count等）

常见格式：TextFile（行）、SequenceFile（行）、ORC（列）、Parquet（列）

### HDFS的默认副本数？为什么？如何修改？

默认**3副本**：在可靠性和存储成本之间取平衡（容忍2个节点同时故障）。

修改：

- `hdfs-site.xml` 中 `dfs.replication=3`
- 或命令：`hdfs dfs -setrep -w 2 /path/to/file`

### HDFS的块默认大小，64M和128M是在哪个版本更换的？怎么修改默认块大小？

Hadoop **1.x默认64MB**，**2.x起改为128MB**。

修改：`hdfs-site.xml` 中 `dfs.blocksize=134217728`（单位字节）

### HDFS的block为什么是128M？增大或减小有什么影响？

磁盘寻址约10ms，传输速率约100MB/s，128MB传输约1.28秒，寻址时间占比约1%，效率最优。

- **增大**：Map并行度降低，适合超大文件
- **减小**：Map任务数增多，启动开销大，NameNode元数据增多

### HDFS HA怎么实现？是个什么架构？

见上方"NameNode高可用"部分：Active NN + Standby NN + JournalNode集群 + ZooKeeper + ZKFC

### 导入大文件到HDFS时如何自定义分片？

实现自定义`InputFormat`，重写`getSplits()`方法。或调整参数：

- `mapreduce.input.fileinputformat.split.maxsize`
- `mapreduce.input.fileinputformat.split.minsize`

### HDFS的mapper和reducer的个数如何确定？reducer的个数依据是什么？

- **Mapper数**：由输入Split数决定，一个Split = 一个MapTask（默认Split大小 = Block大小）
- **Reducer数**：手动设置（`job.setNumReduceTasks(n)`），一般设为节点数×1.5~2倍

### HDFS跨节点怎么进行数据迁移

- `hadoop distcp`：分布式拷贝，适合集群间大量数据迁移（推荐）
- 跨集群：`hadoop distcp hdfs://cluster1/path hdfs://cluster2/path`

### HDFS的数据一致性靠什么保证？

- **写入时**：pipeline写入，所有副本ack后才确认写成功
- **读取时**：CRC校验，不一致自动切换副本
- **副本监控**：NameNode持续监控副本数，不足时触发重建

### HDFS怎么保证数据安全

- 多副本（数据冗余）
- CRC校验（检测损坏）
- Kerberos认证（身份验证）
- ACL权限控制（文件级权限）
- 传输加密（TLS）和存储加密（KMS）
- 审计日志

### HDFS写数据过程，写的过程中有哪些故障，分别会怎么处理？

写数据过程见上方"写入流程"。

故障处理：

- **某DataNode宕机**：从pipeline移除，用新DataNode替换，事后补足副本数
- **NameNode宕机（HA模式）**：Standby自动切为Active，Client重连继续写
- **网络超时**：packet重传，超时后报错，Client可重试

### 直接将数据文件上传到HDFS的表目录中，如何在表中查询到该数据？

- **非分区表**：直接可查，Hive会扫描目录下所有文件
- **分区表**：执行 `MSCK REPAIR TABLE 表名;` 刷新分区元数据，或手动 `ALTER TABLE 表名 ADD PARTITION (...)`

---

## ⚙️ MapReduce

> **整体类比：** 统计一本书里每个单词出现多少次
> 
> - **Map** = 把书分给100人，每人数自己那几页的词频，输出(词, 1)
> - **Shuffle** = 把所有"hadoop"汇给同一个人，"spark"汇给另一个人
> - **Reduce** = 每人把收到的同一词的数字加起来，得出最终结果

### 介绍下MapReduce

分布式批处理计算框架，将计算分为两阶段：

- **Map**：对输入数据做转换/过滤，输出KV对
- **Reduce**：对相同key的value做聚合

中间通过**Shuffle**（分区、排序、合并、网络传输）连接两个阶段。

### MapReduce优缺点

- **优点**：简单、高容错、适合超大规模离线批处理
- **缺点**：延迟高（中间结果落磁盘）、不适合实时、不适合迭代计算

### MapReduce工作原理

```
输入文件 → Split切分 → MapTask → 环形缓冲区
→ 溢写（分区+排序）→ 合并 → Shuffle（网络传输）
→ ReduceTask归并排序 → Reduce函数 → 输出文件
```

### MapReduce哪个阶段最费时间

**Shuffle阶段**最耗时：大量磁盘溢写 + 归并排序 + 网络传输。

### MapReduce中的Combine是干嘛的？有什么好处？

在Map端本地预聚合，减少传输到Reduce的数据量。

- 好处：减少网络传输、减轻ReduceTask压力、整体加快
- 要求：操作满足交换律和结合律（✅ sum/max，❌ avg）

### MapReduce为什么一定要有环形缓冲区

Map输出先写内存环形缓冲区（默认100MB），满80%再批量溢写磁盘。

避免每条数据都触发磁盘I/O，批量写效率高得多。环形设计可以边写边溢写，不阻塞。

### MapReduce为什么一定要有Shuffle过程

Map和Reduce之间需要**按key分组**：相同key的数据必须汇聚到同一个ReduceTask处理。Shuffle负责分区→排序→网络传输→归并，没有Shuffle就无法实现分布式聚合。

### MapReduce的Shuffle过程及其优化

**Map端：** Map输出 → 写环形缓冲区 → 满80%溢写（按分区快速排序）→ 多个溢写文件归并合并

**Reduce端：** HTTP拉取各MapTask输出 → 归并排序 → 传给Reducer

**优化：**

- 开启Combiner预聚合，减少传输量
- 压缩Map输出（`mapreduce.map.output.compress=true`，推荐Snappy）
- 调大环形缓冲区（`mapreduce.task.io.sort.mb`）

### Reduce怎么知道去哪里拉Map结果集？

ApplicationMaster追踪所有MapTask完成情况和输出位置。ReduceTask定期询问AM，获取已完成MapTask的输出位置（Host+端口），通过HTTP主动拉取。

### Reduce阶段都发生了什么，有没有进行分组

1. **拉取数据**：从各MapTask HTTP拉取属于本Reducer的分区数据
2. **归并排序**：将多份数据归并排序（相同key相邻）
3. **分组**：相同key的所有value形成一个Iterable（**有分组**）
4. **调用Reduce函数**：对每个key的value集合执行用户逻辑
5. **输出**：写入HDFS

### MapReduce Shuffle的排序算法

- **Map端溢写**：快速排序
- **Map端合并溢写文件**：归并排序
- **Reduce端合并拉取数据**：归并排序

### shuffle为什么要排序？

排序使相同key的数据**相邻**，Reduce端分组只需顺序扫描，无需额外哈希表，内存占用低，效率高。

### 说一下map是怎么到reduce的？

Map输出 → 写环形缓冲区 → 按分区排序 → 溢写磁盘 → 归并合并成一个有序文件 → Reduce通过HTTP拉取 → 归并排序 → 传给Reducer

### MapReduce的数据处理过程

Input → InputFormat切分 → RecordReader读取KV → Map函数 → Partitioner分区 → 排序 → Combiner（可选）→ Shuffle → Reduce函数 → OutputFormat → Output

### mapjoin的原理？应用场景？

**原理：** 将小表通过DistributedCache广播到所有MapTask的内存中，Map阶段直接与大表做join，**无需Reduce和Shuffle**。

> 类比：把城市编码表打印一份给每个工人，工人本地查表，不用汇总给主管。

**应用场景：** 大表 join 小表（小表能装入内存，如几百MB以内），可完全避免数据倾斜。

### reducejoin如何执行（原理）

1. 两张表数据都打上标记（标注来自哪张表）
2. 以join key为Map输出key，相同key的数据到同一Reducer
3. Reducer中按标记区分两张表，做匹配

缺点：所有数据都要Shuffle，数据量大时可能数据倾斜，性能不如MapJoin。

### MapReduce为什么不能产生过多小文件

- 每个小文件对应一个MapTask，JVM启动开销远大于实际计算
- 大量小文件消耗NameNode内存（每文件约150字节元数据）

### MapReduce分区及作用

分区决定Map输出的KV数据发送到哪个ReduceTask。

默认：`HashPartitioner`：`key.hashCode() % numReduceTasks`

保证相同key一定到同一Reducer。可自定义Partitioner实现业务分区。

### ReduceTask数量和分区数量关系

- ReduceTask == 分区数：✅ 正常
- ReduceTask > 分区数：多余的Task空转，产生空文件
- ReduceTask < 分区数：❌ 报错，部分分区数据无处写入

### Map的分片有多大

默认分片大小 = Block大小（128MB）。

分片大小 = `max(minSize, min(maxSize, blockSize))`

### reduce任务什么时候开始？

- **Shuffle拉取数据**：5%的MapTask完成后就开始拉
- **Reduce真正计算**：等所有MapTask完成后才开始

### MapReduce用了几次排序，分别是什么？

共**3次**：

1. **Map端溢写时**：快速排序（对缓冲区内数据）
2. **Map端合并溢写文件时**：归并排序
3. **Reduce端合并拉取数据时**：归并排序

### MapReduce怎么确定MapTask的数量？Map数量由什么决定

MapTask数量 = 输入数据的**Split数量**，一个Split对应一个MapTask。

Split数 = 输入文件大小 / 分片大小（默认=Block大小128MB）

小文件多时，每个文件至少一个Split，MapTask数会爆炸。

### MapReduce作业执行过程中，中间数据存在什么地方？

存在**本地磁盘**（非HDFS）。

Map输出先写内存环形缓冲区（100MB），超过80%溢写到**本地磁盘**，最终合并成本地文件。Reduce拉取后也先写本地磁盘归并，再传给Reducer计算。

### map输出数据超出缓冲区后，落地到磁盘还是HDFS？

**本地磁盘**（不是HDFS）。中间数据走本地磁盘效率更高，HDFS是最终输入输出用的。

### Map到Reduce默认的分区机制是什么？

默认`HashPartitioner`：`(key.hashCode() & Integer.MAX_VALUE) % numReduceTasks`

### MapReduce数据倾斜产生的原因及其解决方案

**原因：** key分布不均，某些key数据量远大于其他，对应Reducer处理时间远长。

> 类比：100人统计词频，"的"字出现100万次全汇给一个人，这人累死其他人都完了。

**解决方案：**

- **MapJoin**：小表广播内存，避免Reduce阶段（最彻底）
- **key加随机前缀**：打散热点key（加1-100随机数前缀），聚合后再二次聚合
- **自定义Partitioner**：将热点key均匀分配
- **Combiner预聚合**：减少传到Reducer的数据
- **过滤NULL或异常key**：提前过滤无效数据

### Map Join为什么能解决数据倾斜

MapJoin完全在Map端完成join，**没有Shuffle没有Reduce**，每个MapTask独立处理一部分数据并查询内存中的小表，数据天然均衡，不存在某节点数据集中的问题。

### MapReduce运行过程中会发生OOM，OOM发生的位置？

- **Map端**：环形缓冲区设置过大，或Map逻辑缓存了太多数据
- **Reduce端**：归并数据时内存不足，或Reduce逻辑缓存太多

解决：调大 `mapreduce.map/reduce.memory.mb` 和对应JVM堆内存参数。

### MapReduce压缩方式

- **Map输出压缩**：减少Shuffle传输量，推荐Snappy（快）
- **最终输出压缩**：减少HDFS存储，推荐Bzip2（可切分）或Gzip

配置：`mapreduce.map.output.compress=true`

### MapReduce中怎么处理一个大文件

- 确保文件**可切分**（避免不可切分的Gzip压缩）
- 使用`FileInputFormat`按Block自动切分
- 调大Map内存和超时时间
- 开启Combiner和Map输出压缩

---

## 🎯 YARN

> **整体类比：** 工厂人力资源部
> 
> - **ResourceManager** = 人事总监（管全厂资源）
> - **NodeManager** = 各车间主任（管自己车间）
> - **ApplicationMaster** = 项目经理（管一个具体项目，向总监要资源）
> - **Container** = 一个工位（固定CPU+内存）

### 介绍下YARN

YARN（Yet Another Resource Negotiator）是Hadoop的资源管理框架，将资源管理和作业调度分离，支持多计算框架（MapReduce/Spark/Flink）共享集群资源。

### YARN有几个模块

4个核心模块：

- **ResourceManager（RM）**：全局资源管理
- **NodeManager（NM）**：单节点资源管理
- **ApplicationMaster（AM）**：每个应用独立，申请资源+任务调度
- **Container**：资源封装单元（CPU + 内存）

### YARN工作机制

1. Client向RM提交应用
2. RM分配Container，启动AM（项目经理上班）
3. AM评估需要多少资源，向RM申请Container列表
4. RM分配Container，AM通知对应NM启动Container执行任务
5. 任务完成，AM向RM注销，资源释放

### YARN有什么优势，能解决什么问题？

解决Hadoop 1.x的JobTracker单点瓶颈（同时负责资源管理和任务调度）。

YARN优势：

- 职责分离，RM专注资源，AM专注应用
- 支持多框架共享集群（MR/Spark/Flink）
- 更好的扩展性（支持数万节点）

### YARN容错机制

- **RM故障**：ZooKeeper实现RM HA，Standby自动接管
- **NM故障**：RM检测到心跳超时，将该节点任务重新调度
- **AM故障**：RM重新启动AM（默认重试2次）
- **Container/Task故障**：AM检测到，重新申请Container重跑

### YARN高可用

Active RM + Standby RM + ZooKeeper（选主+状态存储）

Active故障时Standby自动切换。

### YARN调度器

同Hadoop调度器：FIFO / CapacityScheduler（默认）/ FairScheduler

### YARN中Container是如何启动的？

1. AM向RM申请到Container（包含Host、资源量）
2. AM直接联系对应NM，发送启动命令（包含命令、环境变量、资源文件）
3. NM在本地启动Container进程，设置CPU/内存限制（cgroups）
4. Container向AM汇报状态

### YARN的改进之处，Hadoop3.x相对于Hadoop 2.x？

- 支持GPU/FPGA资源调度
- Opportunistic Container（低优先级抢占式Container，提高利用率）
- 更好的RM HA
- Timeline Service v2（更好的监控和历史记录）

---

## 综合问题

### 为什么Spark比MapReduce快？

|      | MapReduce     | Spark       |
| ---- | ------------- | ----------- |
| 中间结果 | 每步落磁盘         | 放内存         |
| 类比   | 每算完一步存档，下步再读档 | 一直在内存算，最后才存 |
| 速度   | 慢             | 快10-100倍    |

磁盘比内存慢100倍以上，所以Spark快很多。另外Spark用DAG优化执行计划，减少不必要的shuffle。

### 宽依赖窄依赖

- **窄依赖**：父RDD每个分区只被子RDD**一个**分区使用（如map、filter）→ 可pipeline，不需要shuffle
- **宽依赖**：父RDD每个分区被子RDD**多个**分区使用（如groupByKey、join）→ 需要shuffle，是stage划分边界

> 类比：窄依赖 = 一个工人负责一道工序（流水线）；宽依赖 = 所有工人的结果都要汇总再重新分配（需要等待）

### 是否遇到过数据倾斜问题？如何解决的

症状：大多数Task很快完成，少数Task卡住很久。

排查：看Spark UI，找数据量异常大的Task。

解决：

1. 过滤NULL或异常key
2. 大表join小表用MapJoin（广播小表）
3. 热点key加随机前缀打散，聚合后去掉前缀二次聚合
4. 增大shuffle分区数（`spark.sql.shuffle.partitions`）
5. Spark 3.x开启AQE（自适应查询执行）自动处理

### Spark的shuffle有几种方式

- **HashShuffle**（已废弃）：按key哈希写文件，文件数=Map数×Reduce数，文件太多
- **SortShuffle**（默认）：先排序再写一个文件+索引，文件数=Map数，效率更高
- **TungstenSortShuffle**：SortShuffle优化版，使用堆外内存，减少GC

### Hadoop和Spark的主要区别。Spark为什么更有优势？

|      | Hadoop MR       | Spark                |
| ---- | --------------- | -------------------- |
| 计算模型 | 两阶段（Map+Reduce） | DAG多阶段               |
| 中间数据 | 落HDFS磁盘         | 内存（必要时spill磁盘）       |
| 速度   | 慢               | 快10-100倍             |
| 编程模型 | 只有Map/Reduce，复杂 | RDD/DataFrame/SQL，丰富 |
| 适合场景 | 超大规模单次批处理       | 迭代计算、交互查询、流处理        |

**数据超内存时**：Spark自动将RDD分区spill到本地磁盘，性能降低但仍可工作。

### 你如何进行大数据平台的性能调优？

1. **存储层**：列式存储（ORC/Parquet）+压缩，合并小文件
2. **计算层**：合理设置并行度，用MapJoin，开启Combiner
3. **资源配置**：合理分配内存/CPU，调整JVM参数
4. **SQL优化**：谓词下推、分区裁剪、避免SELECT *、减少shuffle
5. **数据倾斜**：加盐打散、广播join
6. **监控定位**：Spark UI/YARN UI找瓶颈任务

### 一个Hive SQL或Spark任务运行很慢，你会从哪些方面排查？

1. **执行计划**：`EXPLAIN`，看是否全表扫描、缺少分区裁剪
2. **数据倾斜**：看各Task数据量是否均匀（Spark UI）
3. **小文件**：Map数过多，每个Task数据量极小
4. **Shuffle量**：是否Shuffle了大量数据
5. **资源**：是否频繁GC，内存是否够用
6. **Join策略**：大表join是否可改为MapJoin

### 对实时流处理的理解。用过哪些流处理框架？

实时流处理：对持续产生的数据流做低延迟处理，相对批处理的T+1，可达秒级甚至毫秒级。

|      | Spark Streaming | Flink           |
| ---- | --------------- | --------------- |
| 处理方式 | 微批（把流切成小批次）     | 真流（逐条处理）        |
| 延迟   | 秒级              | 毫秒级             |
| 吞吐量  | 高               | 高               |
| 语义   | At-Least-Once为主 | Exactly-Once    |
| 适合   | 对延迟要求不极致，吞吐高    | 低延迟、精确计算（对账、风控） |

### 在大数据开发中，如何管理数据权限和保障数据安全？

- **认证**：Kerberos（确保只有合法用户可访问）
- **授权**：Apache Ranger（表/列/行级别细粒度权限控制）
- **传输加密**：TLS/SSL
- **存储加密**：HDFS透明加密（KMS管理密钥）
- **数据脱敏**：敏感字段（手机号、身份证）在查询层脱敏
- **审计日志**：记录所有访问操作，便于追溯

---

## 数据湖

### 你了解数据湖、数据湖仓一体这些概念吗？它们与传统数据仓库相比有何演进？

|      | 数据仓库                    | 数据湖                  | 湖仓一体（Lakehouse）             |
| ---- | ----------------------- | -------------------- | --------------------------- |
| 类比   | 整理好的档案室                 | 什么都往里扔的储物间           | 智能储物室（存得下又找得到）              |
| 数据格式 | 只存结构化                   | 任意格式                 | 任意格式                        |
| 写入方式 | Schema-on-Write（写时定义结构） | Schema-on-Read（读时定义） | Schema-on-Write（有管理）        |
| 查询   | 快，有索引                   | 慢，无组织                | 快（有索引+统计信息）                 |
| 成本   | 贵                       | 便宜（对象存储）             | 便宜                          |
| ACID | 支持                      | 不支持                  | 支持（Delta Lake/Hudi/Iceberg） |
| 缺点   | 灵活性差，不支持非结构化            | 容易变"数据沼泽"，难治理        | 相对复杂                        |

**演进路径：** 数仓（贵但好用）→ 数据湖（便宜但难用）→ 湖仓一体（既便宜又好用）

代表技术：Delta Lake（Databricks）、Apache Hudi（Uber）、Apache Iceberg（Netflix）资源如何分配给各个应用程序（如 MapReduce、Spark、Hive 任务）。当多个用户或任务同时提交作业时，调度器决定谁先运行、谁使用多少资源、资源如何公平分配。

用户提交任务

三种调度器：

| 调度器               | 机制                 | 适用场景    |
| ----------------- | ------------------ | ------- |
| FIFO              | 先进先出               | 简单单用户系统 |
| CapacityScheduler | 多队列 + 优先级高、占资源少的先跑 | 大型企业    |
| FairScheduler     | 尽量公平分配资源           | 多用户共享   |

**FIFO**：

**CapacityScheduler**：

**FairScheduler**：

### 为什么需要调度器？

1、资源有限：Hadoop 集群资源，没有调度器的话：所有任务都在抢资源、可能有的任务占满集群、其他任务一直等待，调度器让系统 可控分配资源。

2、多用户共享：企业 Hadoop 经常是 共享集群（数据开发、算法团队、BI团队）

3、保证公平：让短任务快速运行

4、提高集群利用率：调度器可以实现资源借用、资源借用。提高 Cluster Utilization（集群利用率）

### 什么时候

### hadoop框架的理解、Hadoop的特点

Hadoop = **HDFS**（分布式存储）+ **MapReduce**（分布式计算）+ **YARN**（资源管理）

特点：**高可靠**（多副本容错）、**高扩展**（加机器就能扩容）、**高容错**（节点挂了自动恢复）、**低成本**（普通硬件即可）

### Hadoop生态圈组件及其作用

| 组件        | 作用                     |
| --------- | ---------------------- |
| HDFS      | 分布式文件存储                |
| MapReduce | 分布式批处理计算               |
| YARN      | 资源调度与管理                |
| Hive      | SQL查询工具（SQL转MapReduce） |
| HBase     | 分布式列式NoSQL数据库          |
| ZooKeeper | 分布式协调服务（选主、配置管理）       |
| Kafka     | 高吞吐消息队列                |
| Flume     | 日志采集                   |
| Sqoop     | 关系型数据库与HDFS互导          |
| Spark     | 内存计算引擎，比MR快            |

### Hadoop 1.x，2.x，3.x的区别

- **1.x**：JobTracker同时负责资源管理和任务调度，单点瓶颈；没有HA
- **2.x**：引入YARN把资源管理分出去；HDFS支持NameNode HA和Federation
- **3.x**：支持多个NameNode；引入**纠删码（EC）**替代副本节省存储约50%；支持GPU资源调度

### Hadoop集群工作时启动哪些进程？它们有什么作用？

- **NameNode**：管理HDFS元数据（文件在哪、有几个副本），不存实际数据
- **DataNode**：存储实际数据块，定期向NameNode发心跳汇报状态
- **ResourceManager**：管整个集群资源，接受Job提交，分配资源
- **NodeManager**：管单个节点资源，启动和监控Container
- **SecondaryNameNode**（非HA模式）：辅助NameNode合并日志，**不是**NameNode备份

### 在集群计算的时候，什么是集群的主要瓶颈

**磁盘I/O**是主要瓶颈，尤其是MapReduce的Shuffle阶段（大量数据溢写磁盘+网络传输）。其次是**网络带宽**。

### 搭建Hadoop集群的xml文件有哪些？

- `core-site.xml`：核心配置（HDFS地址等）
- `hdfs-site.xml`：HDFS配置（副本数、块大小等）
- `mapred-site.xml`：MapReduce配置
- `yarn-site.xml`：YARN配置

### Hadoop的checkpoint流程

> **类比：** 就像把流水账（editlog）定期整理成账本快照（fsimage），防止流水账越来越长。

1. SecondaryNameNode从NameNode拉取editlog和fsimage
2. 将editlog回放合并到fsimage，生成新fsimage
3. 将新fsimage推回NameNode，清空旧editlog

作用：防止editlog无限增长，加快NameNode重启速度。

### Hadoop的默认块大小是多少？为什么设置这么大？

默认**128MB**（Hadoop 2.x起）。

原因：磁盘寻址时间约10ms，传输速率约100MB/s，128MB传输约1.28秒，寻址时间占比约1%，效率最优。

- 太小 → Map任务数多，启动开销大
- 太大 → Map并行度低

### Block划分的原因

- 大文件切块后可**多节点并行处理**
- Block分散到各DataNode，**负载均衡**
- 单个Block损坏只需恢复该Block，**容错代价小**

### Hadoop常见的压缩算法？

| 算法     | 是否可切分   | 速度  | 压缩比 | 适用场景       |
| ------ | ------- | --- | --- | ---------- |
| Gzip   | ❌       | 中   | 高   | 冷数据存储      |
| Bzip2  | ✅       | 慢   | 最高  | 需切分的归档     |
| Snappy | ❌       | 最快  | 中   | Map输出、中间数据 |
| LZO    | ✅（需建索引） | 快   | 中   | 大文件、需切分场景  |

> 注意：不可切分的压缩格式（如Gzip）大文件只能一个Map处理，并行度差。

### Hadoop作业提交到YARN的流程？

1. Client向ResourceManager提交Job（上传JAR到HDFS）
2. RM分配Container，启动**ApplicationMaster**
3. AM向RM申请运行MapTask/ReduceTask的Container
4. AM联系NodeManager，在Container中启动任务
5. 任务完成，AM向RM注销，资源释放

### Hadoop的Combiner的作用

在**Map端本地预聚合**，减少传输到Reduce的数据量。

> **类比：** 100人统计词频，传纸条前先自己合并，传"hadoop:50"而不是50张"hadoop:1"。

要求操作满足交换律和结合律：✅ sum/max/min，❌ avg（会丢信息）

### Hadoop序列化和反序列化

Hadoop用`Writable`接口（非Java原生序列化），更紧凑高效，节省带宽。

常用类型：`IntWritable`、`LongWritable`、`Text`、`NullWritable`

### Hadoop的运行模式

- **本地模式**：单机单JVM，无HDFS，用于开发调试
- **伪分布式**：单机模拟集群
- **完全分布式**：多节点，生产环境

### Hadoop小文件处理问题

**问题：** 每个小文件占NameNode约150字节内存；每个小文件启动一个MapTask，启动开销远大于计算本身。

**解决：**

- **CombineFileInputFormat**：合并小文件再处理
- **SequenceFile**：将小文件以KV形式合并存储
- **HAR归档**：打包小文件
- 上游控制，避免产生小文件（如Hive设置合并输出）

### Hadoop为什么要从2.x升级到3.x？

- **纠删码**：存储开销从200%降至约50%，节省大量存储成本
- **多NameNode**：突破单NameNode扩展瓶颈
- **支持GPU/FPGA**资源调度

### Hadoop的优缺点

- **优点**：高容错、低成本、高扩展、适合PB级批量处理
- **缺点**：延迟高（不适合实时）、小文件问题、不支持随机写、不适合迭代计算

---

## 📦 HDFS

> **整体类比：** 图书馆管理系统
> 
> - NameNode = 图书馆目录（记录书在哪，但不存书）
> - DataNode = 书架（真正放书的地方）
> - Block = 把大书撕成若干份（128MB一份）
> - 副本数3 = 每份复印3本放不同书架，防止丢失

### HDFS NameNode高可用如何实现？需要哪些角色？

架构：**Active NameNode + Standby NameNode**

| 角色                 | 作用                           |
| ------------------ | ---------------------------- |
| Active NameNode    | 对外提供服务                       |
| Standby NameNode   | 热备，实时同步editlog               |
| JournalNode集群（≥3个） | 共享editlog，Active写入，Standby读取 |
| ZooKeeper          | 选主，记录谁是Active                |
| ZKFC               | 监控NameNode健康，触发自动切换          |

### HDFS中向DataNode写数据失败了怎么办

1. 将失败的DataNode从pipeline中移除
2. 已写数据标记为损坏
3. NameNode重新分配新DataNode，重建pipeline继续写
4. 写完后NameNode发现副本数不足，触发后台重新复制

### DataNode什么情况下不会备份

强制关闭或非正常断电时。

### HDFS中DataNode怎么存储数据的

- 数据以**Block文件**存在本地磁盘
- 每个Block对应一个`.meta`校验文件（CRC）
- DataNode每3秒向NameNode发**心跳**，每6小时发**块报告**

### NameNode存数据吗？

**不存实际数据**，只存**元数据**：文件目录树、文件与Block的映射、权限等。

持久化方式：`fsimage`（全量快照）+ `editlog`（操作日志）

### HDFS文件写入和读取流程

**写入流程：**

1. Client → NameNode：申请创建文件
2. NameNode返回DataNode列表（DN1→DN2→DN3 流水线）
3. Client将数据切Block，按流水线依次写入（DN1写完传给DN2，DN2传给DN3）
4. 每个packet写完，ack沿流水线反向回传给Client
5. 全部写完，Client通知NameNode完成

**读取流程：**

1. Client → NameNode：请求读文件
2. NameNode返回各Block所在DataNode列表（按距离排序）
3. Client就近选DataNode读取每个Block
4. CRC校验，损坏则自动切换其他副本

### HDFS优缺点及使用场景

- **优点**：高容错、高吞吐（流式读取）、低成本、可扩展
- **缺点**：高延迟、不适合小文件、不支持随机写、不支持并发写
- **使用场景**：日志存储、数据仓库原始数据、离线批处理

### HDFS的容错机制

- **心跳检测**：DataNode超时未发心跳，NameNode触发副本重建
- **CRC校验**：读写时检测数据损坏，自动切换副本
- **多副本**：默认3副本，一个节点坏了不影响数据
- **NameNode HA**：元数据不丢失

### HDFS的副本机制

默认**3副本**放置策略：

- 第1副本：客户端所在节点
- 第2副本：**不同机架**的节点
- 第3副本：与第2副本**同机架**不同节点

兼顾可靠性（跨机架防机架故障）和网络效率。

### HDFS的常见数据格式，列式存储格式和行存储格式异同点，列式存储优点有哪些？

**行存储**：一行数据连续存储，适合OLTP（增删改查整行）

**列式存储**：同一列数据连续存储，适合OLAP（只读少数列的聚合分析）

**列式存储优点：**

- 压缩比高（同列数据类型相同，压缩效果好）
- I/O少（只读需要的列，跳过无关数据）
- 聚合计算快（sum/count等）

常见格式：TextFile（行）、SequenceFile（行）、ORC（列）、Parquet（列）

### HDFS的默认副本数？为什么？如何修改？

默认**3副本**：在可靠性和存储成本之间取平衡（容忍2个节点同时故障）。

修改：

- `hdfs-site.xml` 中 `dfs.replication=3`
- 或命令：`hdfs dfs -setrep -w 2 /path/to/file`

### HDFS的块默认大小，64M和128M是在哪个版本更换的？怎么修改默认块大小？

Hadoop **1.x默认64MB**，**2.x起改为128MB**。

修改：`hdfs-site.xml` 中 `dfs.blocksize=134217728`（单位字节）

### HDFS的block为什么是128M？增大或减小有什么影响？

磁盘寻址约10ms，传输速率约100MB/s，128MB传输约1.28秒，寻址时间占比约1%，效率最优。

- **增大**：Map并行度降低，适合超大文件
- **减小**：Map任务数增多，启动开销大，NameNode元数据增多

### HDFS HA怎么实现？是个什么架构？

见上方"NameNode高可用"部分：Active NN + Standby NN + JournalNode集群 + ZooKeeper + ZKFC

### 导入大文件到HDFS时如何自定义分片？

实现自定义`InputFormat`，重写`getSplits()`方法。或调整参数：

- `mapreduce.input.fileinputformat.split.maxsize`
- `mapreduce.input.fileinputformat.split.minsize`

### HDFS的mapper和reducer的个数如何确定？reducer的个数依据是什么？

- **Mapper数**：由输入Split数决定，一个Split = 一个MapTask（默认Split大小 = Block大小）
- **Reducer数**：手动设置（`job.setNumReduceTasks(n)`），一般设为节点数×1.5~2倍

### HDFS跨节点怎么进行数据迁移

- `hadoop distcp`：分布式拷贝，适合集群间大量数据迁移（推荐）
- 跨集群：`hadoop distcp hdfs://cluster1/path hdfs://cluster2/path`

### HDFS的数据一致性靠什么保证？

- **写入时**：pipeline写入，所有副本ack后才确认写成功
- **读取时**：CRC校验，不一致自动切换副本
- **副本监控**：NameNode持续监控副本数，不足时触发重建

### HDFS怎么保证数据安全

- 多副本（数据冗余）
- CRC校验（检测损坏）
- Kerberos认证（身份验证）
- ACL权限控制（文件级权限）
- 传输加密（TLS）和存储加密（KMS）
- 审计日志

### HDFS写数据过程，写的过程中有哪些故障，分别会怎么处理？

写数据过程见上方"写入流程"。

故障处理：

- **某DataNode宕机**：从pipeline移除，用新DataNode替换，事后补足副本数
- **NameNode宕机（HA模式）**：Standby自动切为Active，Client重连继续写
- **网络超时**：packet重传，超时后报错，Client可重试

### 直接将数据文件上传到HDFS的表目录中，如何在表中查询到该数据？

- **非分区表**：直接可查，Hive会扫描目录下所有文件
- **分区表**：执行 `MSCK REPAIR TABLE 表名;` 刷新分区元数据，或手动 `ALTER TABLE 表名 ADD PARTITION (...)`

---

## ⚙️ MapReduce

> **整体类比：** 统计一本书里每个单词出现多少次
> 
> - **Map** = 把书分给100人，每人数自己那几页的词频，输出(词, 1)
> - **Shuffle** = 把所有"hadoop"汇给同一个人，"spark"汇给另一个人
> - **Reduce** = 每人把收到的同一词的数字加起来，得出最终结果

### 介绍下MapReduce

分布式批处理计算框架，将计算分为两阶段：

- **Map**：对输入数据做转换/过滤，输出KV对
- **Reduce**：对相同key的value做聚合

中间通过**Shuffle**（分区、排序、合并、网络传输）连接两个阶段。

### MapReduce优缺点

- **优点**：简单、高容错、适合超大规模离线批处理
- **缺点**：延迟高（中间结果落磁盘）、不适合实时、不适合迭代计算

### MapReduce工作原理

```
输入文件 → Split切分 → MapTask → 环形缓冲区
→ 溢写（分区+排序）→ 合并 → Shuffle（网络传输）
→ ReduceTask归并排序 → Reduce函数 → 输出文件
```

### MapReduce哪个阶段最费时间

**Shuffle阶段**最耗时：大量磁盘溢写 + 归并排序 + 网络传输。

### MapReduce中的Combine是干嘛的？有什么好处？

在Map端本地预聚合，减少传输到Reduce的数据量。

- 好处：减少网络传输、减轻ReduceTask压力、整体加快
- 要求：操作满足交换律和结合律（✅ sum/max，❌ avg）

### MapReduce为什么一定要有环形缓冲区

Map输出先写内存环形缓冲区（默认100MB），满80%再批量溢写磁盘。

避免每条数据都触发磁盘I/O，批量写效率高得多。环形设计可以边写边溢写，不阻塞。

### MapReduce为什么一定要有Shuffle过程

Map和Reduce之间需要**按key分组**：相同key的数据必须汇聚到同一个ReduceTask处理。Shuffle负责分区→排序→网络传输→归并，没有Shuffle就无法实现分布式聚合。

### MapReduce的Shuffle过程及其优化

**Map端：** Map输出 → 写环形缓冲区 → 满80%溢写（按分区快速排序）→ 多个溢写文件归并合并

**Reduce端：** HTTP拉取各MapTask输出 → 归并排序 → 传给Reducer

**优化：**

- 开启Combiner预聚合，减少传输量
- 压缩Map输出（`mapreduce.map.output.compress=true`，推荐Snappy）
- 调大环形缓冲区（`mapreduce.task.io.sort.mb`）

### Reduce怎么知道去哪里拉Map结果集？

ApplicationMaster追踪所有MapTask完成情况和输出位置。ReduceTask定期询问AM，获取已完成MapTask的输出位置（Host+端口），通过HTTP主动拉取。

### Reduce阶段都发生了什么，有没有进行分组

1. **拉取数据**：从各MapTask HTTP拉取属于本Reducer的分区数据
2. **归并排序**：将多份数据归并排序（相同key相邻）
3. **分组**：相同key的所有value形成一个Iterable（**有分组**）
4. **调用Reduce函数**：对每个key的value集合执行用户逻辑
5. **输出**：写入HDFS

### MapReduce Shuffle的排序算法

- **Map端溢写**：快速排序
- **Map端合并溢写文件**：归并排序
- **Reduce端合并拉取数据**：归并排序

### shuffle为什么要排序？

排序使相同key的数据**相邻**，Reduce端分组只需顺序扫描，无需额外哈希表，内存占用低，效率高。

### 说一下map是怎么到reduce的？

Map输出 → 写环形缓冲区 → 按分区排序 → 溢写磁盘 → 归并合并成一个有序文件 → Reduce通过HTTP拉取 → 归并排序 → 传给Reducer

### MapReduce的数据处理过程

Input → InputFormat切分 → RecordReader读取KV → Map函数 → Partitioner分区 → 排序 → Combiner（可选）→ Shuffle → Reduce函数 → OutputFormat → Output

### mapjoin的原理？应用场景？

**原理：** 将小表通过DistributedCache广播到所有MapTask的内存中，Map阶段直接与大表做join，**无需Reduce和Shuffle**。

> 类比：把城市编码表打印一份给每个工人，工人本地查表，不用汇总给主管。

**应用场景：** 大表 join 小表（小表能装入内存，如几百MB以内），可完全避免数据倾斜。

### reducejoin如何执行（原理）

1. 两张表数据都打上标记（标注来自哪张表）
2. 以join key为Map输出key，相同key的数据到同一Reducer
3. Reducer中按标记区分两张表，做匹配

缺点：所有数据都要Shuffle，数据量大时可能数据倾斜，性能不如MapJoin。

### MapReduce为什么不能产生过多小文件

- 每个小文件对应一个MapTask，JVM启动开销远大于实际计算
- 大量小文件消耗NameNode内存（每文件约150字节元数据）

### MapReduce分区及作用

分区决定Map输出的KV数据发送到哪个ReduceTask。

默认：`HashPartitioner`：`key.hashCode() % numReduceTasks`

保证相同key一定到同一Reducer。可自定义Partitioner实现业务分区。

### ReduceTask数量和分区数量关系

- ReduceTask == 分区数：✅ 正常
- ReduceTask > 分区数：多余的Task空转，产生空文件
- ReduceTask < 分区数：❌ 报错，部分分区数据无处写入

### Map的分片有多大

默认分片大小 = Block大小（128MB）。

分片大小 = `max(minSize, min(maxSize, blockSize))`

### reduce任务什么时候开始？

- **Shuffle拉取数据**：5%的MapTask完成后就开始拉
- **Reduce真正计算**：等所有MapTask完成后才开始

### MapReduce用了几次排序，分别是什么？

共**3次**：

1. **Map端溢写时**：快速排序（对缓冲区内数据）
2. **Map端合并溢写文件时**：归并排序
3. **Reduce端合并拉取数据时**：归并排序

### MapReduce怎么确定MapTask的数量？Map数量由什么决定

MapTask数量 = 输入数据的**Split数量**，一个Split对应一个MapTask。

Split数 = 输入文件大小 / 分片大小（默认=Block大小128MB）

小文件多时，每个文件至少一个Split，MapTask数会爆炸。

### MapReduce作业执行过程中，中间数据存在什么地方？

存在**本地磁盘**（非HDFS）。

Map输出先写内存环形缓冲区（100MB），超过80%溢写到**本地磁盘**，最终合并成本地文件。Reduce拉取后也先写本地磁盘归并，再传给Reducer计算。

### map输出数据超出缓冲区后，落地到磁盘还是HDFS？

**本地磁盘**（不是HDFS）。中间数据走本地磁盘效率更高，HDFS是最终输入输出用的。

### Map到Reduce默认的分区机制是什么？

默认`HashPartitioner`：`(key.hashCode() & Integer.MAX_VALUE) % numReduceTasks`

### MapReduce数据倾斜产生的原因及其解决方案

**原因：** key分布不均，某些key数据量远大于其他，对应Reducer处理时间远长。

> 类比：100人统计词频，"的"字出现100万次全汇给一个人，这人累死其他人都完了。

**解决方案：**

- **MapJoin**：小表广播内存，避免Reduce阶段（最彻底）
- **key加随机前缀**：打散热点key（加1-100随机数前缀），聚合后再二次聚合
- **自定义Partitioner**：将热点key均匀分配
- **Combiner预聚合**：减少传到Reducer的数据
- **过滤NULL或异常key**：提前过滤无效数据

### Map Join为什么能解决数据倾斜

MapJoin完全在Map端完成join，**没有Shuffle没有Reduce**，每个MapTask独立处理一部分数据并查询内存中的小表，数据天然均衡，不存在某节点数据集中的问题。

### MapReduce运行过程中会发生OOM，OOM发生的位置？

- **Map端**：环形缓冲区设置过大，或Map逻辑缓存了太多数据
- **Reduce端**：归并数据时内存不足，或Reduce逻辑缓存太多

解决：调大 `mapreduce.map/reduce.memory.mb` 和对应JVM堆内存参数。

### MapReduce压缩方式

- **Map输出压缩**：减少Shuffle传输量，推荐Snappy（快）
- **最终输出压缩**：减少HDFS存储，推荐Bzip2（可切分）或Gzip

配置：`mapreduce.map.output.compress=true`

### MapReduce中怎么处理一个大文件

- 确保文件**可切分**（避免不可切分的Gzip压缩）
- 使用`FileInputFormat`按Block自动切分
- 调大Map内存和超时时间
- 开启Combiner和Map输出压缩

---

## 🎯 YARN

> **整体类比：** 工厂人力资源部
> 
> - **ResourceManager** = 人事总监（管全厂资源）
> - **NodeManager** = 各车间主任（管自己车间）
> - **ApplicationMaster** = 项目经理（管一个具体项目，向总监要资源）
> - **Container** = 一个工位（固定CPU+内存）

### 介绍下YARN

YARN（Yet Another Resource Negotiator）是Hadoop的资源管理框架，将资源管理和作业调度分离，支持多计算框架（MapReduce/Spark/Flink）共享集群资源。

### YARN有几个模块

4个核心模块：

- **ResourceManager（RM）**：全局资源管理
- **NodeManager（NM）**：单节点资源管理
- **ApplicationMaster（AM）**：每个应用独立，申请资源+任务调度
- **Container**：资源封装单元（CPU + 内存）

### YARN工作机制

1. Client向RM提交应用
2. RM分配Container，启动AM（项目经理上班）
3. AM评估需要多少资源，向RM申请Container列表
4. RM分配Container，AM通知对应NM启动Container执行任务
5. 任务完成，AM向RM注销，资源释放

### YARN有什么优势，能解决什么问题？

解决Hadoop 1.x的JobTracker单点瓶颈（同时负责资源管理和任务调度）。

YARN优势：

- 职责分离，RM专注资源，AM专注应用
- 支持多框架共享集群（MR/Spark/Flink）
- 更好的扩展性（支持数万节点）

### YARN容错机制

- **RM故障**：ZooKeeper实现RM HA，Standby自动接管
- **NM故障**：RM检测到心跳超时，将该节点任务重新调度
- **AM故障**：RM重新启动AM（默认重试2次）
- **Container/Task故障**：AM检测到，重新申请Container重跑

### YARN高可用

Active RM + Standby RM + ZooKeeper（选主+状态存储）

Active故障时Standby自动切换。

### YARN调度器

同Hadoop调度器：FIFO / CapacityScheduler（默认）/ FairScheduler

### YARN中Container是如何启动的？

1. AM向RM申请到Container（包含Host、资源量）
2. AM直接联系对应NM，发送启动命令（包含命令、环境变量、资源文件）
3. NM在本地启动Container进程，设置CPU/内存限制（cgroups）
4. Container向AM汇报状态

### YARN的改进之处，Hadoop3.x相对于Hadoop 2.x？

- 支持GPU/FPGA资源调度
- Opportunistic Container（低优先级抢占式Container，提高利用率）
- 更好的RM HA
- Timeline Service v2（更好的监控和历史记录）

---

## 综合问题

### 为什么Spark比MapReduce快？

|      | MapReduce     | Spark       |
| ---- | ------------- | ----------- |
| 中间结果 | 每步落磁盘         | 放内存         |
| 类比   | 每算完一步存档，下步再读档 | 一直在内存算，最后才存 |
| 速度   | 慢             | 快10-100倍    |

磁盘比内存慢100倍以上，所以Spark快很多。另外Spark用DAG优化执行计划，减少不必要的shuffle。

### 宽依赖窄依赖

- **窄依赖**：父RDD每个分区只被子RDD**一个**分区使用（如map、filter）→ 可pipeline，不需要shuffle
- **宽依赖**：父RDD每个分区被子RDD**多个**分区使用（如groupByKey、join）→ 需要shuffle，是stage划分边界

> 类比：窄依赖 = 一个工人负责一道工序（流水线）；宽依赖 = 所有工人的结果都要汇总再重新分配（需要等待）

### 是否遇到过数据倾斜问题？如何解决的

症状：大多数Task很快完成，少数Task卡住很久。

排查：看Spark UI，找数据量异常大的Task。

解决：

1. 过滤NULL或异常key
2. 大表join小表用MapJoin（广播小表）
3. 热点key加随机前缀打散，聚合后去掉前缀二次聚合
4. 增大shuffle分区数（`spark.sql.shuffle.partitions`）
5. Spark 3.x开启AQE（自适应查询执行）自动处理

### Spark的shuffle有几种方式

- **HashShuffle**（已废弃）：按key哈希写文件，文件数=Map数×Reduce数，文件太多
- **SortShuffle**（默认）：先排序再写一个文件+索引，文件数=Map数，效率更高
- **TungstenSortShuffle**：SortShuffle优化版，使用堆外内存，减少GC

### Hadoop和Spark的主要区别。Spark为什么更有优势？

|      | Hadoop MR       | Spark                |
| ---- | --------------- | -------------------- |
| 计算模型 | 两阶段（Map+Reduce） | DAG多阶段               |
| 中间数据 | 落HDFS磁盘         | 内存（必要时spill磁盘）       |
| 速度   | 慢               | 快10-100倍             |
| 编程模型 | 只有Map/Reduce，复杂 | RDD/DataFrame/SQL，丰富 |
| 适合场景 | 超大规模单次批处理       | 迭代计算、交互查询、流处理        |

**数据超内存时**：Spark自动将RDD分区spill到本地磁盘，性能降低但仍可工作。

### 你如何进行大数据平台的性能调优？

1. **存储层**：列式存储（ORC/Parquet）+压缩，合并小文件
2. **计算层**：合理设置并行度，用MapJoin，开启Combiner
3. **资源配置**：合理分配内存/CPU，调整JVM参数
4. **SQL优化**：谓词下推、分区裁剪、避免SELECT *、减少shuffle
5. **数据倾斜**：加盐打散、广播join
6. **监控定位**：Spark UI/YARN UI找瓶颈任务

### 一个Hive SQL或Spark任务运行很慢，你会从哪些方面排查？

1. **执行计划**：`EXPLAIN`，看是否全表扫描、缺少分区裁剪
2. **数据倾斜**：看各Task数据量是否均匀（Spark UI）
3. **小文件**：Map数过多，每个Task数据量极小
4. **Shuffle量**：是否Shuffle了大量数据
5. **资源**：是否频繁GC，内存是否够用
6. **Join策略**：大表join是否可改为MapJoin

### 对实时流处理的理解。用过哪些流处理框架？

实时流处理：对持续产生的数据流做低延迟处理，相对批处理的T+1，可达秒级甚至毫秒级。

|      | Spark Streaming | Flink           |
| ---- | --------------- | --------------- |
| 处理方式 | 微批（把流切成小批次）     | 真流（逐条处理）        |
| 延迟   | 秒级              | 毫秒级             |
| 吞吐量  | 高               | 高               |
| 语义   | At-Least-Once为主 | Exactly-Once    |
| 适合   | 对延迟要求不极致，吞吐高    | 低延迟、精确计算（对账、风控） |

### 在大数据开发中，如何管理数据权限和保障数据安全？

- **认证**：Kerberos（确保只有合法用户可访问）
- **授权**：Apache Ranger（表/列/行级别细粒度权限控制）
- **传输加密**：TLS/SSL
- **存储加密**：HDFS透明加密（KMS管理密钥）
- **数据脱敏**：敏感字段（手机号、身份证）在查询层脱敏
- **审计日志**：记录所有访问操作，便于追溯

---

## 数据湖

### 你了解数据湖、数据湖仓一体这些概念吗？它们与传统数据仓库相比有何演进？

|      | 数据仓库                    | 数据湖                  | 湖仓一体（Lakehouse）             |
| ---- | ----------------------- | -------------------- | --------------------------- |
| 类比   | 整理好的档案室                 | 什么都往里扔的储物间           | 智能储物室（存得下又找得到）              |
| 数据格式 | 只存结构化                   | 任意格式                 | 任意格式                        |
| 写入方式 | Schema-on-Write（写时定义结构） | Schema-on-Read（读时定义） | Schema-on-Write（有管理）        |
| 查询   | 快，有索引                   | 慢，无组织                | 快（有索引+统计信息）                 |
| 成本   | 贵                       | 便宜（对象存储）             | 便宜                          |
| ACID | 支持                      | 不支持                  | 支持（Delta Lake/Hudi/Iceberg） |
| 缺点   | 灵活性差，不支持非结构化            | 容易变"数据沼泽"，难治理        | 相对复杂                        |

**演进路径：** 数仓（贵但好用）→ 数据湖（便宜但难用）→ 湖仓一体（既便宜又好用）

代表技术：Delta Lake（Databricks）、Apache Hudi（Uber）、Apache Iceberg（Netflix）[大数据面试题V3.0，约870篇牛客大数据面经480道面试题_牛客网](https://www.nowcoder.com/discuss/353159520220291072)

https://zhuanlan.zhihu.com/p/424296249 [大数据开发面经汇总【持续更新...】_牛客网](https://www.nowcoder.com/discuss/594817738107781120)

https://leetcode.cn/discuss/post/3516212/zi-jie-mian-jing-nian-xin-70wda-shu-ju-s-23r7/

[大数据开发面经_大数据面经-CSDN博客](https://blog.csdn.net/axzy5863/article/details/158429145)

[大数据开发（牛客）面试被问频率最高的几道面试题-腾讯云开发者社区-腾讯云](https://cloud.tencent.com/developer/article/2071876)

---

## 🐘 Hadoop整体理解

把Hadoop想象成一个**超大的仓库管理系统**：

- **HDFS** = 仓库（存东西）
- **MapReduce** = 工人（干活）
- **YARN** = 仓库主管（分配工人和资源）

---

## Hadoop基础

### 什么是Hadoop调度器？说明其工作方法

Hadoop 调度器（Hadoop Scheduler）通常指 Hadoop YARN （Yet Another Resource Negotiator） 中的资源调度组件，负责决定 集群中的 CPU、内存等计算资源如何分配给各个应用程序（如 MapReduce、Spark、Hive 任务）。当多个用户或任务同时提交作业时，调度器决定谁先运行、谁使用多少资源、资源如何公平分配。

没有调度器的话：所有任务都在抢资源、可能有的任务占满集群、其他任务一直等待
三种调度器：

| 调度器               | 机制   | 适用场景 |
| ----------------- | ---- | ---- |
| FIFO              | 先进先出 |      |
| CapacityScheduler |      |      |
| FairScheduler     |      |      |

- **FIFO**：先进先出，按提交顺序排队执行，简单但资源利用率低
- **CapacityScheduler（默认）**：多队列，按队列容量分配资源，优先级高、占资源少的先跑
- **FairScheduler**：同一队列内所有作业公平共享资源，动态均衡

### hadoop框架的理解、Hadoop的特点

Hadoop = **HDFS**（分布式存储）+ **MapReduce**（分布式计算）+ **YARN**（资源管理）

特点：**高可靠**（多副本容错）、**高扩展**（加机器就能扩容）、**高容错**（节点挂了自动恢复）、**低成本**（普通硬件即可）

### Hadoop生态圈组件及其作用

| 组件        | 作用                     |
| --------- | ---------------------- |
| HDFS      | 分布式文件存储                |
| MapReduce | 分布式批处理计算               |
| YARN      | 资源调度与管理                |
| Hive      | SQL查询工具（SQL转MapReduce） |
| HBase     | 分布式列式NoSQL数据库          |
| ZooKeeper | 分布式协调服务（选主、配置管理）       |
| Kafka     | 高吞吐消息队列                |
| Flume     | 日志采集                   |
| Sqoop     | 关系型数据库与HDFS互导          |
| Spark     | 内存计算引擎，比MR快            |

### Hadoop 1.x，2.x，3.x的区别

- **1.x**：JobTracker同时负责资源管理和任务调度，单点瓶颈；没有HA
- **2.x**：引入YARN把资源管理分出去；HDFS支持NameNode HA和Federation
- **3.x**：支持多个NameNode；引入**纠删码（EC）**替代副本节省存储约50%；支持GPU资源调度

### Hadoop集群工作时启动哪些进程？它们有什么作用？

- **NameNode**：管理HDFS元数据（文件在哪、有几个副本），不存实际数据
- **DataNode**：存储实际数据块，定期向NameNode发心跳汇报状态
- **ResourceManager**：管整个集群资源，接受Job提交，分配资源
- **NodeManager**：管单个节点资源，启动和监控Container
- **SecondaryNameNode**（非HA模式）：辅助NameNode合并日志，**不是**NameNode备份

### 在集群计算的时候，什么是集群的主要瓶颈

**磁盘I/O**是主要瓶颈，尤其是MapReduce的Shuffle阶段（大量数据溢写磁盘+网络传输）。其次是**网络带宽**。

### 搭建Hadoop集群的xml文件有哪些？

- `core-site.xml`：核心配置（HDFS地址等）
- `hdfs-site.xml`：HDFS配置（副本数、块大小等）
- `mapred-site.xml`：MapReduce配置
- `yarn-site.xml`：YARN配置

### Hadoop的checkpoint流程

> **类比：** 就像把流水账（editlog）定期整理成账本快照（fsimage），防止流水账越来越长。

1. SecondaryNameNode从NameNode拉取editlog和fsimage
2. 将editlog回放合并到fsimage，生成新fsimage
3. 将新fsimage推回NameNode，清空旧editlog

作用：防止editlog无限增长，加快NameNode重启速度。

### Hadoop的默认块大小是多少？为什么设置这么大？

默认**128MB**（Hadoop 2.x起）。

原因：磁盘寻址时间约10ms，传输速率约100MB/s，128MB传输约1.28秒，寻址时间占比约1%，效率最优。

- 太小 → Map任务数多，启动开销大
- 太大 → Map并行度低

### Block划分的原因

- 大文件切块后可**多节点并行处理**
- Block分散到各DataNode，**负载均衡**
- 单个Block损坏只需恢复该Block，**容错代价小**

### Hadoop常见的压缩算法？

| 算法     | 是否可切分   | 速度  | 压缩比 | 适用场景       |
| ------ | ------- | --- | --- | ---------- |
| Gzip   | ❌       | 中   | 高   | 冷数据存储      |
| Bzip2  | ✅       | 慢   | 最高  | 需切分的归档     |
| Snappy | ❌       | 最快  | 中   | Map输出、中间数据 |
| LZO    | ✅（需建索引） | 快   | 中   | 大文件、需切分场景  |

> 注意：不可切分的压缩格式（如Gzip）大文件只能一个Map处理，并行度差。

### Hadoop作业提交到YARN的流程？

1. Client向ResourceManager提交Job（上传JAR到HDFS）
2. RM分配Container，启动**ApplicationMaster**
3. AM向RM申请运行MapTask/ReduceTask的Container
4. AM联系NodeManager，在Container中启动任务
5. 任务完成，AM向RM注销，资源释放

### Hadoop的Combiner的作用

在**Map端本地预聚合**，减少传输到Reduce的数据量。

> **类比：** 100人统计词频，传纸条前先自己合并，传"hadoop:50"而不是50张"hadoop:1"。

要求操作满足交换律和结合律：✅ sum/max/min，❌ avg（会丢信息）

### Hadoop序列化和反序列化

Hadoop用`Writable`接口（非Java原生序列化），更紧凑高效，节省带宽。

常用类型：`IntWritable`、`LongWritable`、`Text`、`NullWritable`

### Hadoop的运行模式

- **本地模式**：单机单JVM，无HDFS，用于开发调试
- **伪分布式**：单机模拟集群
- **完全分布式**：多节点，生产环境

### Hadoop小文件处理问题

**问题：** 每个小文件占NameNode约150字节内存；每个小文件启动一个MapTask，启动开销远大于计算本身。

**解决：**

- **CombineFileInputFormat**：合并小文件再处理
- **SequenceFile**：将小文件以KV形式合并存储
- **HAR归档**：打包小文件
- 上游控制，避免产生小文件（如Hive设置合并输出）

### Hadoop为什么要从2.x升级到3.x？

- **纠删码**：存储开销从200%降至约50%，节省大量存储成本
- **多NameNode**：突破单NameNode扩展瓶颈
- **支持GPU/FPGA**资源调度

### Hadoop的优缺点

- **优点**：高容错、低成本、高扩展、适合PB级批量处理
- **缺点**：延迟高（不适合实时）、小文件问题、不支持随机写、不适合迭代计算

---

## 📦 HDFS

> **整体类比：** 图书馆管理系统
> 
> - NameNode = 图书馆目录（记录书在哪，但不存书）
> - DataNode = 书架（真正放书的地方）
> - Block = 把大书撕成若干份（128MB一份）
> - 副本数3 = 每份复印3本放不同书架，防止丢失

### HDFS NameNode高可用如何实现？需要哪些角色？

架构：**Active NameNode + Standby NameNode**

| 角色                 | 作用                           |
| ------------------ | ---------------------------- |
| Active NameNode    | 对外提供服务                       |
| Standby NameNode   | 热备，实时同步editlog               |
| JournalNode集群（≥3个） | 共享editlog，Active写入，Standby读取 |
| ZooKeeper          | 选主，记录谁是Active                |
| ZKFC               | 监控NameNode健康，触发自动切换          |

### HDFS中向DataNode写数据失败了怎么办

1. 将失败的DataNode从pipeline中移除
2. 已写数据标记为损坏
3. NameNode重新分配新DataNode，重建pipeline继续写
4. 写完后NameNode发现副本数不足，触发后台重新复制

### DataNode什么情况下不会备份

强制关闭或非正常断电时。

### HDFS中DataNode怎么存储数据的

- 数据以**Block文件**存在本地磁盘
- 每个Block对应一个`.meta`校验文件（CRC）
- DataNode每3秒向NameNode发**心跳**，每6小时发**块报告**

### NameNode存数据吗？

**不存实际数据**，只存**元数据**：文件目录树、文件与Block的映射、权限等。

持久化方式：`fsimage`（全量快照）+ `editlog`（操作日志）

### HDFS文件写入和读取流程

**写入流程：**

1. Client → NameNode：申请创建文件
2. NameNode返回DataNode列表（DN1→DN2→DN3 流水线）
3. Client将数据切Block，按流水线依次写入（DN1写完传给DN2，DN2传给DN3）
4. 每个packet写完，ack沿流水线反向回传给Client
5. 全部写完，Client通知NameNode完成

**读取流程：**

1. Client → NameNode：请求读文件
2. NameNode返回各Block所在DataNode列表（按距离排序）
3. Client就近选DataNode读取每个Block
4. CRC校验，损坏则自动切换其他副本

### HDFS优缺点及使用场景

- **优点**：高容错、高吞吐（流式读取）、低成本、可扩展
- **缺点**：高延迟、不适合小文件、不支持随机写、不支持并发写
- **使用场景**：日志存储、数据仓库原始数据、离线批处理

### HDFS的容错机制

- **心跳检测**：DataNode超时未发心跳，NameNode触发副本重建
- **CRC校验**：读写时检测数据损坏，自动切换副本
- **多副本**：默认3副本，一个节点坏了不影响数据
- **NameNode HA**：元数据不丢失

### HDFS的副本机制

默认**3副本**放置策略：

- 第1副本：客户端所在节点
- 第2副本：**不同机架**的节点
- 第3副本：与第2副本**同机架**不同节点

兼顾可靠性（跨机架防机架故障）和网络效率。

### HDFS的常见数据格式，列式存储格式和行存储格式异同点，列式存储优点有哪些？

**行存储**：一行数据连续存储，适合OLTP（增删改查整行）

**列式存储**：同一列数据连续存储，适合OLAP（只读少数列的聚合分析）

**列式存储优点：**

- 压缩比高（同列数据类型相同，压缩效果好）
- I/O少（只读需要的列，跳过无关数据）
- 聚合计算快（sum/count等）

常见格式：TextFile（行）、SequenceFile（行）、ORC（列）、Parquet（列）

### HDFS的默认副本数？为什么？如何修改？

默认**3副本**：在可靠性和存储成本之间取平衡（容忍2个节点同时故障）。

修改：

- `hdfs-site.xml` 中 `dfs.replication=3`
- 或命令：`hdfs dfs -setrep -w 2 /path/to/file`

### HDFS的块默认大小，64M和128M是在哪个版本更换的？怎么修改默认块大小？

Hadoop **1.x默认64MB**，**2.x起改为128MB**。

修改：`hdfs-site.xml` 中 `dfs.blocksize=134217728`（单位字节）

### HDFS的block为什么是128M？增大或减小有什么影响？

磁盘寻址约10ms，传输速率约100MB/s，128MB传输约1.28秒，寻址时间占比约1%，效率最优。

- **增大**：Map并行度降低，适合超大文件
- **减小**：Map任务数增多，启动开销大，NameNode元数据增多

### HDFS HA怎么实现？是个什么架构？

见上方"NameNode高可用"部分：Active NN + Standby NN + JournalNode集群 + ZooKeeper + ZKFC

### 导入大文件到HDFS时如何自定义分片？

实现自定义`InputFormat`，重写`getSplits()`方法。或调整参数：

- `mapreduce.input.fileinputformat.split.maxsize`
- `mapreduce.input.fileinputformat.split.minsize`

### HDFS的mapper和reducer的个数如何确定？reducer的个数依据是什么？

- **Mapper数**：由输入Split数决定，一个Split = 一个MapTask（默认Split大小 = Block大小）
- **Reducer数**：手动设置（`job.setNumReduceTasks(n)`），一般设为节点数×1.5~2倍

### HDFS跨节点怎么进行数据迁移

- `hadoop distcp`：分布式拷贝，适合集群间大量数据迁移（推荐）
- 跨集群：`hadoop distcp hdfs://cluster1/path hdfs://cluster2/path`

### HDFS的数据一致性靠什么保证？

- **写入时**：pipeline写入，所有副本ack后才确认写成功
- **读取时**：CRC校验，不一致自动切换副本
- **副本监控**：NameNode持续监控副本数，不足时触发重建

### HDFS怎么保证数据安全

- 多副本（数据冗余）
- CRC校验（检测损坏）
- Kerberos认证（身份验证）
- ACL权限控制（文件级权限）
- 传输加密（TLS）和存储加密（KMS）
- 审计日志

### HDFS写数据过程，写的过程中有哪些故障，分别会怎么处理？

写数据过程见上方"写入流程"。

故障处理：

- **某DataNode宕机**：从pipeline移除，用新DataNode替换，事后补足副本数
- **NameNode宕机（HA模式）**：Standby自动切为Active，Client重连继续写
- **网络超时**：packet重传，超时后报错，Client可重试

### 直接将数据文件上传到HDFS的表目录中，如何在表中查询到该数据？

- **非分区表**：直接可查，Hive会扫描目录下所有文件
- **分区表**：执行 `MSCK REPAIR TABLE 表名;` 刷新分区元数据，或手动 `ALTER TABLE 表名 ADD PARTITION (...)`

---

## ⚙️ MapReduce

> **整体类比：** 统计一本书里每个单词出现多少次
> 
> - **Map** = 把书分给100人，每人数自己那几页的词频，输出(词, 1)
> - **Shuffle** = 把所有"hadoop"汇给同一个人，"spark"汇给另一个人
> - **Reduce** = 每人把收到的同一词的数字加起来，得出最终结果

### 介绍下MapReduce

分布式批处理计算框架，将计算分为两阶段：

- **Map**：对输入数据做转换/过滤，输出KV对
- **Reduce**：对相同key的value做聚合

中间通过**Shuffle**（分区、排序、合并、网络传输）连接两个阶段。

### MapReduce优缺点

- **优点**：简单、高容错、适合超大规模离线批处理
- **缺点**：延迟高（中间结果落磁盘）、不适合实时、不适合迭代计算

### MapReduce工作原理

```
输入文件 → Split切分 → MapTask → 环形缓冲区
→ 溢写（分区+排序）→ 合并 → Shuffle（网络传输）
→ ReduceTask归并排序 → Reduce函数 → 输出文件
```

### MapReduce哪个阶段最费时间

**Shuffle阶段**最耗时：大量磁盘溢写 + 归并排序 + 网络传输。

### MapReduce中的Combine是干嘛的？有什么好处？

在Map端本地预聚合，减少传输到Reduce的数据量。

- 好处：减少网络传输、减轻ReduceTask压力、整体加快
- 要求：操作满足交换律和结合律（✅ sum/max，❌ avg）

### MapReduce为什么一定要有环形缓冲区

Map输出先写内存环形缓冲区（默认100MB），满80%再批量溢写磁盘。

避免每条数据都触发磁盘I/O，批量写效率高得多。环形设计可以边写边溢写，不阻塞。

### MapReduce为什么一定要有Shuffle过程

Map和Reduce之间需要**按key分组**：相同key的数据必须汇聚到同一个ReduceTask处理。Shuffle负责分区→排序→网络传输→归并，没有Shuffle就无法实现分布式聚合。

### MapReduce的Shuffle过程及其优化

**Map端：** Map输出 → 写环形缓冲区 → 满80%溢写（按分区快速排序）→ 多个溢写文件归并合并

**Reduce端：** HTTP拉取各MapTask输出 → 归并排序 → 传给Reducer

**优化：**

- 开启Combiner预聚合，减少传输量
- 压缩Map输出（`mapreduce.map.output.compress=true`，推荐Snappy）
- 调大环形缓冲区（`mapreduce.task.io.sort.mb`）

### Reduce怎么知道去哪里拉Map结果集？

ApplicationMaster追踪所有MapTask完成情况和输出位置。ReduceTask定期询问AM，获取已完成MapTask的输出位置（Host+端口），通过HTTP主动拉取。

### Reduce阶段都发生了什么，有没有进行分组

1. **拉取数据**：从各MapTask HTTP拉取属于本Reducer的分区数据
2. **归并排序**：将多份数据归并排序（相同key相邻）
3. **分组**：相同key的所有value形成一个Iterable（**有分组**）
4. **调用Reduce函数**：对每个key的value集合执行用户逻辑
5. **输出**：写入HDFS

### MapReduce Shuffle的排序算法

- **Map端溢写**：快速排序
- **Map端合并溢写文件**：归并排序
- **Reduce端合并拉取数据**：归并排序

### shuffle为什么要排序？

排序使相同key的数据**相邻**，Reduce端分组只需顺序扫描，无需额外哈希表，内存占用低，效率高。

### 说一下map是怎么到reduce的？

Map输出 → 写环形缓冲区 → 按分区排序 → 溢写磁盘 → 归并合并成一个有序文件 → Reduce通过HTTP拉取 → 归并排序 → 传给Reducer

### MapReduce的数据处理过程

Input → InputFormat切分 → RecordReader读取KV → Map函数 → Partitioner分区 → 排序 → Combiner（可选）→ Shuffle → Reduce函数 → OutputFormat → Output

### mapjoin的原理？应用场景？

**原理：** 将小表通过DistributedCache广播到所有MapTask的内存中，Map阶段直接与大表做join，**无需Reduce和Shuffle**。

> 类比：把城市编码表打印一份给每个工人，工人本地查表，不用汇总给主管。

**应用场景：** 大表 join 小表（小表能装入内存，如几百MB以内），可完全避免数据倾斜。

### reducejoin如何执行（原理）

1. 两张表数据都打上标记（标注来自哪张表）
2. 以join key为Map输出key，相同key的数据到同一Reducer
3. Reducer中按标记区分两张表，做匹配

缺点：所有数据都要Shuffle，数据量大时可能数据倾斜，性能不如MapJoin。

### MapReduce为什么不能产生过多小文件

- 每个小文件对应一个MapTask，JVM启动开销远大于实际计算
- 大量小文件消耗NameNode内存（每文件约150字节元数据）

### MapReduce分区及作用

分区决定Map输出的KV数据发送到哪个ReduceTask。

默认：`HashPartitioner`：`key.hashCode() % numReduceTasks`

保证相同key一定到同一Reducer。可自定义Partitioner实现业务分区。

### ReduceTask数量和分区数量关系

- ReduceTask == 分区数：✅ 正常
- ReduceTask > 分区数：多余的Task空转，产生空文件
- ReduceTask < 分区数：❌ 报错，部分分区数据无处写入

### Map的分片有多大

默认分片大小 = Block大小（128MB）。

分片大小 = `max(minSize, min(maxSize, blockSize))`

### reduce任务什么时候开始？

- **Shuffle拉取数据**：5%的MapTask完成后就开始拉
- **Reduce真正计算**：等所有MapTask完成后才开始

### MapReduce用了几次排序，分别是什么？

共**3次**：

1. **Map端溢写时**：快速排序（对缓冲区内数据）
2. **Map端合并溢写文件时**：归并排序
3. **Reduce端合并拉取数据时**：归并排序

### MapReduce怎么确定MapTask的数量？Map数量由什么决定

MapTask数量 = 输入数据的**Split数量**，一个Split对应一个MapTask。

Split数 = 输入文件大小 / 分片大小（默认=Block大小128MB）

小文件多时，每个文件至少一个Split，MapTask数会爆炸。

### MapReduce作业执行过程中，中间数据存在什么地方？

存在**本地磁盘**（非HDFS）。

Map输出先写内存环形缓冲区（100MB），超过80%溢写到**本地磁盘**，最终合并成本地文件。Reduce拉取后也先写本地磁盘归并，再传给Reducer计算。

### map输出数据超出缓冲区后，落地到磁盘还是HDFS？

**本地磁盘**（不是HDFS）。中间数据走本地磁盘效率更高，HDFS是最终输入输出用的。

### Map到Reduce默认的分区机制是什么？

默认`HashPartitioner`：`(key.hashCode() & Integer.MAX_VALUE) % numReduceTasks`

### MapReduce数据倾斜产生的原因及其解决方案

**原因：** key分布不均，某些key数据量远大于其他，对应Reducer处理时间远长。

> 类比：100人统计词频，"的"字出现100万次全汇给一个人，这人累死其他人都完了。

**解决方案：**

- **MapJoin**：小表广播内存，避免Reduce阶段（最彻底）
- **key加随机前缀**：打散热点key（加1-100随机数前缀），聚合后再二次聚合
- **自定义Partitioner**：将热点key均匀分配
- **Combiner预聚合**：减少传到Reducer的数据
- **过滤NULL或异常key**：提前过滤无效数据

### Map Join为什么能解决数据倾斜

MapJoin完全在Map端完成join，**没有Shuffle没有Reduce**，每个MapTask独立处理一部分数据并查询内存中的小表，数据天然均衡，不存在某节点数据集中的问题。

### MapReduce运行过程中会发生OOM，OOM发生的位置？

- **Map端**：环形缓冲区设置过大，或Map逻辑缓存了太多数据
- **Reduce端**：归并数据时内存不足，或Reduce逻辑缓存太多

解决：调大 `mapreduce.map/reduce.memory.mb` 和对应JVM堆内存参数。

### MapReduce压缩方式

- **Map输出压缩**：减少Shuffle传输量，推荐Snappy（快）
- **最终输出压缩**：减少HDFS存储，推荐Bzip2（可切分）或Gzip

配置：`mapreduce.map.output.compress=true`

### MapReduce中怎么处理一个大文件

- 确保文件**可切分**（避免不可切分的Gzip压缩）
- 使用`FileInputFormat`按Block自动切分
- 调大Map内存和超时时间
- 开启Combiner和Map输出压缩

---

## 🎯 YARN

> **整体类比：** 工厂人力资源部
> 
> - **ResourceManager** = 人事总监（管全厂资源）
> - **NodeManager** = 各车间主任（管自己车间）
> - **ApplicationMaster** = 项目经理（管一个具体项目，向总监要资源）
> - **Container** = 一个工位（固定CPU+内存）

### 介绍下YARN

YARN（Yet Another Resource Negotiator）是Hadoop的资源管理框架，将资源管理和作业调度分离，支持多计算框架（MapReduce/Spark/Flink）共享集群资源。

### YARN有几个模块

4个核心模块：

- **ResourceManager（RM）**：全局资源管理
- **NodeManager（NM）**：单节点资源管理
- **ApplicationMaster（AM）**：每个应用独立，申请资源+任务调度
- **Container**：资源封装单元（CPU + 内存）

### YARN工作机制

1. Client向RM提交应用
2. RM分配Container，启动AM（项目经理上班）
3. AM评估需要多少资源，向RM申请Container列表
4. RM分配Container，AM通知对应NM启动Container执行任务
5. 任务完成，AM向RM注销，资源释放

### YARN有什么优势，能解决什么问题？

解决Hadoop 1.x的JobTracker单点瓶颈（同时负责资源管理和任务调度）。

YARN优势：

- 职责分离，RM专注资源，AM专注应用
- 支持多框架共享集群（MR/Spark/Flink）
- 更好的扩展性（支持数万节点）

### YARN容错机制

- **RM故障**：ZooKeeper实现RM HA，Standby自动接管
- **NM故障**：RM检测到心跳超时，将该节点任务重新调度
- **AM故障**：RM重新启动AM（默认重试2次）
- **Container/Task故障**：AM检测到，重新申请Container重跑

### YARN高可用

Active RM + Standby RM + ZooKeeper（选主+状态存储）

Active故障时Standby自动切换。

### YARN调度器

同Hadoop调度器：FIFO / CapacityScheduler（默认）/ FairScheduler

### YARN中Container是如何启动的？

1. AM向RM申请到Container（包含Host、资源量）
2. AM直接联系对应NM，发送启动命令（包含命令、环境变量、资源文件）
3. NM在本地启动Container进程，设置CPU/内存限制（cgroups）
4. Container向AM汇报状态

### YARN的改进之处，Hadoop3.x相对于Hadoop 2.x？

- 支持GPU/FPGA资源调度
- Opportunistic Container（低优先级抢占式Container，提高利用率）
- 更好的RM HA
- Timeline Service v2（更好的监控和历史记录）

---

## 综合问题

### 为什么Spark比MapReduce快？

|      | MapReduce     | Spark       |
| ---- | ------------- | ----------- |
| 中间结果 | 每步落磁盘         | 放内存         |
| 类比   | 每算完一步存档，下步再读档 | 一直在内存算，最后才存 |
| 速度   | 慢             | 快10-100倍    |

磁盘比内存慢100倍以上，所以Spark快很多。另外Spark用DAG优化执行计划，减少不必要的shuffle。

### 宽依赖窄依赖

- **窄依赖**：父RDD每个分区只被子RDD**一个**分区使用（如map、filter）→ 可pipeline，不需要shuffle
- **宽依赖**：父RDD每个分区被子RDD**多个**分区使用（如groupByKey、join）→ 需要shuffle，是stage划分边界

> 类比：窄依赖 = 一个工人负责一道工序（流水线）；宽依赖 = 所有工人的结果都要汇总再重新分配（需要等待）

### 是否遇到过数据倾斜问题？如何解决的

症状：大多数Task很快完成，少数Task卡住很久。

排查：看Spark UI，找数据量异常大的Task。

解决：

1. 过滤NULL或异常key
2. 大表join小表用MapJoin（广播小表）
3. 热点key加随机前缀打散，聚合后去掉前缀二次聚合
4. 增大shuffle分区数（`spark.sql.shuffle.partitions`）
5. Spark 3.x开启AQE（自适应查询执行）自动处理

### Spark的shuffle有几种方式

- **HashShuffle**（已废弃）：按key哈希写文件，文件数=Map数×Reduce数，文件太多
- **SortShuffle**（默认）：先排序再写一个文件+索引，文件数=Map数，效率更高
- **TungstenSortShuffle**：SortShuffle优化版，使用堆外内存，减少GC

### Hadoop和Spark的主要区别。Spark为什么更有优势？

|      | Hadoop MR       | Spark                |
| ---- | --------------- | -------------------- |
| 计算模型 | 两阶段（Map+Reduce） | DAG多阶段               |
| 中间数据 | 落HDFS磁盘         | 内存（必要时spill磁盘）       |
| 速度   | 慢               | 快10-100倍             |
| 编程模型 | 只有Map/Reduce，复杂 | RDD/DataFrame/SQL，丰富 |
| 适合场景 | 超大规模单次批处理       | 迭代计算、交互查询、流处理        |

**数据超内存时**：Spark自动将RDD分区spill到本地磁盘，性能降低但仍可工作。

### 你如何进行大数据平台的性能调优？

1. **存储层**：列式存储（ORC/Parquet）+压缩，合并小文件
2. **计算层**：合理设置并行度，用MapJoin，开启Combiner
3. **资源配置**：合理分配内存/CPU，调整JVM参数
4. **SQL优化**：谓词下推、分区裁剪、避免SELECT *、减少shuffle
5. **数据倾斜**：加盐打散、广播join
6. **监控定位**：Spark UI/YARN UI找瓶颈任务

### 一个Hive SQL或Spark任务运行很慢，你会从哪些方面排查？

1. **执行计划**：`EXPLAIN`，看是否全表扫描、缺少分区裁剪
2. **数据倾斜**：看各Task数据量是否均匀（Spark UI）
3. **小文件**：Map数过多，每个Task数据量极小
4. **Shuffle量**：是否Shuffle了大量数据
5. **资源**：是否频繁GC，内存是否够用
6. **Join策略**：大表join是否可改为MapJoin

### 对实时流处理的理解。用过哪些流处理框架？

实时流处理：对持续产生的数据流做低延迟处理，相对批处理的T+1，可达秒级甚至毫秒级。

|      | Spark Streaming | Flink           |
| ---- | --------------- | --------------- |
| 处理方式 | 微批（把流切成小批次）     | 真流（逐条处理）        |
| 延迟   | 秒级              | 毫秒级             |
| 吞吐量  | 高               | 高               |
| 语义   | At-Least-Once为主 | Exactly-Once    |
| 适合   | 对延迟要求不极致，吞吐高    | 低延迟、精确计算（对账、风控） |

### 在大数据开发中，如何管理数据权限和保障数据安全？

- **认证**：Kerberos（确保只有合法用户可访问）
- **授权**：Apache Ranger（表/列/行级别细粒度权限控制）
- **传输加密**：TLS/SSL
- **存储加密**：HDFS透明加密（KMS管理密钥）
- **数据脱敏**：敏感字段（手机号、身份证）在查询层脱敏
- **审计日志**：记录所有访问操作，便于追溯

---

## 数据湖

### 你了解数据湖、数据湖仓一体这些概念吗？它们与传统数据仓库相比有何演进？

|      | 数据仓库                    | 数据湖                  | 湖仓一体（Lakehouse）             |
| ---- | ----------------------- | -------------------- | --------------------------- |
| 类比   | 整理好的档案室                 | 什么都往里扔的储物间           | 智能储物室（存得下又找得到）              |
| 数据格式 | 只存结构化                   | 任意格式                 | 任意格式                        |
| 写入方式 | Schema-on-Write（写时定义结构） | Schema-on-Read（读时定义） | Schema-on-Write（有管理）        |
| 查询   | 快，有索引                   | 慢，无组织                | 快（有索引+统计信息）                 |
| 成本   | 贵                       | 便宜（对象存储）             | 便宜                          |
| ACID | 支持                      | 不支持                  | 支持（Delta Lake/Hudi/Iceberg） |
| 缺点   | 灵活性差，不支持非结构化            | 容易变"数据沼泽"，难治理        | 相对复杂                        |

**演进路径：** 数仓（贵但好用）→ 数据湖（便宜但难用）→ 湖仓一体（既便宜又好用）

代表技术：Delta Lake（Databricks）、Apache Hudi（Uber）、Apache Iceberg（Netflix）
