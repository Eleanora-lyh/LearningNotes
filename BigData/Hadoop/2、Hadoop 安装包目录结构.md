**Hadoop 是一个整体生态 / 框架，HDFS 和 YARN 是它里面两个核心组件：**

- **HDFS = 分布式存储** Hadoop Distributed File System（存数据）
- **YARN = 分布式资源调度** Yet Another Resource Negotiator（管资源、分配算力）
- **MapReduce = 第一代分布式计算引擎**
- **Hadoop = HDFS + YARN + MapReduce + 周边工具**

## Hadoop 安装包目录结构

安装位置：`/export/server/hadoop`

| 目录    | 说明                                                         |
| ------- | ------------------------------------------------------------ |
| bin     | Hadoop最基本的管理脚本和使用脚本的目录，脚本时sbin目录下管理脚本的基础实现，用户可以使用这些脚本管理和使用Hadoop |
| sbin    | Hadoop管理脚本所在目录，包含HDFS和YARN中各类服务的启动/关闭脚本 |
| etc     | Hadoop配置文件所在目录                                       |
| share   | Hadoop各个模块编译后的jar包所在目录                          |
| include | 对外提供的变成库头文件（具体动态库+静态库在lib目录中）这些头文件均用C++定义，通常用于C++程序访问HDFS或者编写MapReduce程序 |
| lib     | 包含Hadoop对外提供的变成动态\|静态库，与include目录中的头文件结合使用 |
| libexec | 各个服务对应的shell配置文件所在目录，用于配置日志输出、启动参数，如JVM参数等信息 |
| logs    | 日志                                                         |

### Yarn、HDFS、Hadoop启停命令

“启动 Hadoop” = 启动 HDFS + YARN

启动必须切换为非root用户才行

```bash
[root@node1 ~]# su - hadoop
Last login: Thu Mar 12 21:42:54 CST 2026 on pts/0
[hadoop@node1 ~]$ hdfs namenode -format
# 格式化HDFS（仅首次启动时执行，重复执行会清空数据！）
```

执行原理：执行脚本的机器上，启动SecondaryNameNode-》读取core-site.xml内容，确定NameNode所在机器，启动NameNode-》读取workers内容，确定DataNode所在机器，启动全部DataNode

以下所有命令的文件存储位置均为

```bash
$HADOOP_HOME/sbin/stop-dfs.sh(hadoop-daemon.sh)
```

|            | 手动逐个进程启停(控制所在机器的进程启停)                     | shell脚本一键启停<br />(配置好机器之间的SSH免密登录和workers文件) |
| ---------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| HDFS集群   | # hadoop2.x版本命令($HADOOP_HOME/sbin/hadoop-daemon.sh)<br />`hadoop-daemon.sh (start|status|stop) (namenode|datanode|secondarynamenode)`<br /># hadoop3.x版本命令($HADOOP_HOME/bin/hdfs)<br />`hdfs --daemon (start|stauts|stop) (namenode|datanode|secondarynamenode)` | `start-dfs.sh`<br />`stop-dfs.sh`                            |
| YARN集群   | # yarn2.x版本命令<br />`yarn-daemon.sh start|stop resourcemanager|nodemanager`<br /># yarn3.x版本命令<br />`yarn--daemon start|stop resourcemanager|nodemanager` | `stop-yarn.sh`<br />`stop-yarn.sh`                           |
| Hadoop集群 |                                                              | `start-all.sh`<br />`stop-all.sh`<br />一个命令代替start-dfs.sh和start-yarn.sh |

- 启动完毕之后可以使用`jps命令`查看进程是否启动成功

  ```bash
  [hadoop@node1 ~]$ jps
  4608 NameNode
  5063 SecondaryNameNode
  5421 NodeManager
  5789 Jps
  5294 ResourceManager
  ```

- Hadoop启动日志路径：`/export/server/hadoop-3.3.0/logs/`

### HDFS集群的Web页面

启动成功后就可以看到hdfs的web：http://node1:9870/

## 操作HDFS

HDFS同Linux系统一样均以 / 作为根目录，同一个文件如果同时保存在HDFS、Linux中，此时就无法区分。所以引入协议头的概念(一般会自动识别为file://和hdfs://不用写)

|              | Linux                         | HDFS                                     |
| ------------ | ----------------------------- | ---------------------------------------- |
| 假设文件位置 | /usr/local/hello.txt          | /usr/local/hello.txt                     |
| 协议头       | file://                       | hdfs://namenode:port/                    |
| ＋协议头后   | *file://*/usr/local/hello.txt | *hdfs://node1:8020/*/usr/local/hello.txt |

Hadoop fs [options] `fs` = **File System**（通用文件系统）：是更顶层、通用的命令，支持操作 HDFS、本地文件系统（Linux）、S3 等多种文件系统；

hdfs dfs [options] `dfs` = **Distributed File System**（分布式文件系统）：是专用于 HDFS 的命令，仅针对 HDFS 操作（本质是 `fs` 针对 HDFS 的别名）。

- 早期 Hadoop 只有 HDFS 一种核心文件系统，所以设计了 `hdfs dfs` 专用于 HDFS；
- 后来 Hadoop 支持了更多文件系统（如 S3、本地文件），为了统一入口，推出了 `hadoop fs`，兼容所有文件系统；
- 为了兼容老用户的使用习惯，`hdfs dfs` 被保留，本质上 `hdfs dfs` 就是 `hadoop fs` 针对 HDFS 的 “快捷方式”。