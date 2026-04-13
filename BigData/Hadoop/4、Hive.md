Hive将SQL语句翻译为MapReduce程序运行，提供用户分布式SQL计算的能力

## 4.1、Hive基础架构

![image-20260408225149972](./assets/image-20260408225149972.png)

## 4.2、Hive部署

Hive是单机工具，只需要部署一台服务器，但是他可以提交分布式运行的MapReduce程序运行

### 4.2.1 元数据管理

Hive需要使用元数据管理，所以将Hive本体和MySQL存储在node1服务器上

```bash
# 更新秘钥
rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022
# 安装MySQL yum库
rpm -Uvh http://repo.mysql.com//mysql57-community-release-el7-7.noarch.rpm
# yum 安装 MySQL
yum install -y mysql-community-server
# 启动Mysql，设置开机启动
systemctl start mysqld
systemctl enable mysqld
# 检查mysql状态
systemctl status mysqld
# 第一次启动mysql，会在日志文件中生成
[root@node1 ~]# grep 'temporary password' /var/log/mysqld.log
#2026-04-12T09:51:18.241513Z 1 [Note] A temporary password is generated for root@localhost: zqeldpw<U2fh
# 使用密码登录mysql
[root@node1 ~]# mysql -uroot -p
# 如果相设置简单密码，需要降低MySQL的
set global validate_password_policy=LOW;
set global validate_password_length=4;
# 然后就可以使用简单密码，这里是本地环境，Prod最好不要这样
ALTER USER 'root'@'localhost' IDENTIFIED BY '281211';
# root用户从任意地方主机远程登录权限
grant all privileges on *.* to root@"%" identified by '281211' with grant option;
flush privileges;
# ctrl+shift+D 退出
```

### 4.2.2 配置Hadoop

Hive的运行依赖Hadoop（HDFS、MapReduce、YARN），就会涉及到对HDFS文件系统的访问，需要配置Hadoop的代理用户，即设置hadoop允许代理其他用户。

在hadoop的`core-site.xml`配置允许hadoop用户代理任意的主机和群组。

```bash
vim $HADOOP_HOME/etc/hadoop/core-site.xml

```

添加配置

```xml
<property>
    <name>hadoop.proxyuser.hadoop.hosts</name>
    <value>*</value>
    <description>允许hadoop用户代理任意的主机</description>
</property>

<property>    
    <name>hadoop.proxyuser.hadoop.groups</name>    
    <value>*</value>
    <description>允许hadoop用户代理任意的群组</description>
</property>
```

中分发到其他节点，重启HDFS集群

```bash
[root@node1 hadoop]# scp core-site.xml hdfs-site.xml node2:`pwd`
core-site.xml                                                           100% 1731   541.4KB/s   00:00    
hdfs-site.xml                                                           100% 2424     1.8MB/s   00:00    
[root@node1 hadoop]# scp core-site.xml hdfs-site.xml node3:`pwd`
core-site.xml                                                           100% 1731     1.6MB/s   00:00    
hdfs-site.xml 
```

### 4.2.3 下载解压Hive

切换到root，进入目标安装目录，使用wget从华为云镜像下载（国内速度快）

```bash
su - root
cd /export/server/
wget -c https://mirrors.huaweicloud.com/apache/hive/hive-3.1.3/apache-hive-3.1.3-bin.tar.gz
```

解压到当前目录，并进行软链接

```bash
tar -zxvf apache-hive-3.1.3-bin.tar.gz -C /export/server/
ln -s /export/server/apache-hive-3.1.3-bin /export/server/hive
```

修改权限

```bash
sudo chown -R hadoop:hadoop hive  # 如果用户是hadoop
```

下载mysql的驱动包，并将其移至于 hive的lib目录下

```bash
wget https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-j-8.0.33.tar.gz
tar -xzvf mysql-connector-j-8.0.33.tar.gz 
# 解压出来的文件中包含mysql-connector-j-8.0.33/mysql-connector-j-8.0.33.jar
mv -f mysql-connector-j-8.0.33/mysql-connector-j-8.0.33.jar /export/server/hive/lib/
```

### 4.2.4 配置Hive环境变量

进入Hive的conf目录，新建`hive-env.sh`文件

```bash
cd /export/server/hive/conf/
mv hive-env.sh.template hive-env.sh
vim hive-env.sh
```

填入环境变量内容

```bash
export HADOOP_HOME=/export/server/hadoop
export HIVE_CONF_DIR=/export/server/hive/conf
export HIVE_AUX_JARS_PATH=/export/server/hive/lib
```

在Hive的conf目录，新建`hive-site.xml`文件