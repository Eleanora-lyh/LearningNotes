分布式版本控制系统（Distributed Version Control System，简称 DVCS） 

在这类系统中，客户端并不只提取最新版本的文件快照， 而是把代码仓库完整地镜像下来，包括完整的历史记录。 

 基于差异（delta-based）的版本控制

Git 和其它版本控制系统（包括 Subversion 和近似工具）的主要差别在于 Git 对待数据的方式。其它大部分系统以文件变更列表的方式存储信息，这类系统（CVS、Subversion、Perforce 等等） 将它们存储的信息看作是一组基本文件和每个文件随时间逐步累积的差异 （它们通常称作 基于差异（delta-based）的版本控制）。



反之，Git 更像是把数据看作是对小型文件系统的一系列快照。
