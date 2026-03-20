## 初识Hadoop

### 数据单位：

| 单位  | 全称        |
| --- | --------- |
| B   | Byte      |
| KB  | Kilobyte  |
| MB  | Megabyte  |
| GB  | Gigabyte  |
| TB  | Terabyte  |
| PB  | Petabyte  |
| EB  | Exabyte   |
| ZB  | Zettabyte |
| YB  | Yottabyte |

大数据从硬盘中读取的速度是有限的，HDD（100–200 MB/s）  SSD （500–7000+ MB/s），但如果有100块这样的硬盘同时读取就可以提高读取速度。对多个硬盘中的数据井行进行读／写数据，还有更多问题要解决 。

1、硬件故障问题

一旦开始使用多个硬件，其中个别硬件就很有可能发生故障。常见的做陆是复制（replication）：冗余硬盘阵列（RAID：Redundant Array of Independent Disks）就是按这个原理实现的。Hadoop 的文件系统(Hadoop Distributed FileSystem, HDFS）也是一类 

2、数据分析结合

即从一个硬盘读取的数据可能需要与从另外 99 个硬盘中读取的数据结合使用。各种分布式系统允许结合不同来源的数据进行分析，但保证其正确性是一个非常大的挑战。MapReduce 提出 一个编程模型，该模型抽象出这些硬盘读／写 问题井将其转换为对一个数据集（由键·值对组成）的计算。

简而言之，Hadoop 为我们提供了 一个可靠的且可扩展的存储和分析平台 。 

## 为什么需要Hadoop

计算机硬盘的另一个发展趋势： 寻址时间的提升远远不敌于传输速率的提升。

寻址是将磁头移动到特定硬盘位置进行读／写操作的过程。它是导致硬盘操作延迟的主要原因，而传输速率取决于硬盘的带宽 。

文件系统的索引用红黑树

Hadoop 对非结构化或半结构化数据非常有效，因为它是在处理数据时才对数据进行解释（即所谓的“读时模式”）。这种模式在提供灵活性的同时避免了RDBMS 数据加载阶段带来的 高开销，因为在 Hadoop 中仅仅是一个文件拷贝操作。

## Hadoop发展简述

Hadoop 是 Apache Lucene 创始人道格·卡丁（DougCutting) 创建的。Lucene是一个应用广泛的文本搜索系统库。Hadoop 起源于开源网络搜索引擎 Apache Nutch。

2004，谷歌发表论文向全世界介绍他们的MapReduce 系统。

2005，Nutch 的开发人员在 Nutch 上实现了一个 MapReduce 系统

2006 年 2 月，开发人员将NDFS 和Map Reduce 移出Nutch，形成Lucene的 一 个子项目，命名为Hadoop 。

2008 年 4 月，Hadoop 打破世界纪录，成为最快的 TB 级数据排序系统。（09年1TB排序只需62s）

2014 年， 207 个节点的 Spark 集群对 lOOTB 数据进行排序，只用了1406 秒，每分钟 4.27 TB

## map 和 reduce
