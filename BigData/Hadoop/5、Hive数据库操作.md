hive leaning in English：https://www.tutorialspoint.com/hive/hive_introduction.htm

在线hive环境：http://demo.gethue.com/hue/home （demo+demo）

## 5.1 数据库操作

启动beeline 

```bash
[hadoop@node1 ~]$ cd $HIVE_HOME
[hadoop@node1 hive]$ bin/beeline
Beeline version 3.1.3 by Apache Hive
```

使用Beeline连接数据库

```bash
!connect jdbc:hive2://node1:10000
```

输入账号hadoop+无密码

```bash
beeline> !connect jdbc:hive2://node1:10000 
Connecting to jdbc:hive2://node1:10000
Enter username for jdbc:hive2://node1:10000: hadoop
Enter password for jdbc:hive2://node1:10000: 
Connected to: Apache Hive (version 3.1.3)
Driver: Hive JDBC (version 3.1.3)
Transaction isolation: TRANSACTION_REPEATABLE_READ
0: jdbc:hive2://node1:10000> 
```

### 5.1.1 创建数据库

```hive
create database [if not exists] 数据库名 [自定义位置];
```

```hive
create database if not exists myhive;
```

效果
```bash
0: jdbc:hive2://node1:10000> show databases;
+----------------+
| database_name  |
+----------------+
| default        |
+----------------+
1 row selected (0.157 seconds)
0: jdbc:hive2://node1:10000> create database if not exists myhive;
No rows affected (0.954 seconds)
0: jdbc:hive2://node1:10000> show databases;
+----------------+
| database_name  |
+----------------+
| default        |
| myhive         |
+----------------+
2 rows selected (0.032 seconds)
```

查看数据库详细信息（在hive中创建的数据库默认的存储位置都为`user/hive/warehouse/`）

```hive
0: jdbc:hive2://node1:10000> use myhive;
No rows affected (0.04 seconds)
0: jdbc:hive2://node1:10000> desc database myhive;
+----------+----------+--------------------------------------------------+-------------+-------------+-------------+
| db_name  | comment  |                     location                     | owner_name  | owner_type  | parameters  |
+----------+----------+--------------------------------------------------+-------------+-------------+-------------+
| myhive   |          | hdfs://node1:8020/user/hive/warehouse/myhive.db  | hadoop      | USER        |             |
+----------+----------+--------------------------------------------------+-------------+-------------+-------------+
1 row selected (0.032 seconds)

```

验证：可以通过hdfs查看新建数据库（文件夹）的位置

```bash
[hadoop@node1 hive]$ hdfs dfs -ls /user/hive/warehouse
Found 2 items
drwxr-xr-x   - hadoop supergroup          0 2026-04-25 11:29 /user/hive/warehouse/myhive.db
drwxrwxrwx   - hadoop supergroup          0 2026-04-16 22:06 /user/hive/warehouse/test_user
```

指定存储位置

```hive
create database myhive_specific_location location '/user/hive/targetLocation';
```

效果

```hive
0: jdbc:hive2://node1:10000> desc database myhive_specific_location;
+---------------------------+----------+---------------------------------------------+-------------+-------------+-------------+
|          db_name          | comment  |                  location                   | owner_name  | owner_type  | parameters  |
+---------------------------+----------+---------------------------------------------+-------------+-------------+-------------+
| myhive_specific_location  |          | hdfs://node1:8020/user/hive/targetLocation  | hadoop      | USER        |             |
+---------------------------+----------+---------------------------------------------+-------------+-------------+-------------+
1 row selected (0.023 seconds)
```

### 5.1.2 删除数据库

删除空数据库（若数据库中包含表则会报错，删除失败）

```hive
drop database myhive2;
```

删除数据库包括下面的表

```hive
drop database myhive2 cascade;
```

效果
```hive
0: jdbc:hive2://node1:10000> drop database myhive2 cascade;
No rows affected (0.239 seconds)
0: jdbc:hive2://node1:10000> show databases;
+---------------------------+
|       database_name       |
+---------------------------+
| default                   |
| myhive                    |
| myhive_specific_location  |
+---------------------------+
3 rows selected (0.018 seconds)
```



## 5.2 数据表的操作

### 5.2.1 数据类型

基本数据类型

| 类别          | 数据类型    | 描述                                    | 示例                        |
| ------------- | ----------- | --------------------------------------- | --------------------------- |
| **数值型**    | `TINYINT`   | 1字节有符号整数，范围：-128 ~ 127       | `1`, `-5`                   |
|               | `SMALLINT`  | 2字节有符号整数，范围：-32,768 ~ 32,767 | `1000`, `-200`              |
|               | `INT`       | 4字节有符号整数，常用整数类型           | `100000`, `-500`            |
|               | `BIGINT`    | 8字节有符号整数                         | `10000000000L`              |
|               | `FLOAT`     | 4字节单精度浮点数                       | `3.14`, `-2.5`              |
|               | `DOUBLE`    | 8字节双精度浮点数                       | `3.1415926`                 |
|               | `DECIMAL`   | 高精度小数，可指定精度                  | `DECIMAL(10,2)`→ `12345.67` |
| **字符型**    | `STRING`    | 字符串，不指定长度                      | `'hello'`, `"大数据"`       |
|               | `VARCHAR`   | 可变长度字符串(1-65535)                 | `VARCHAR(100)`              |
|               | `CHAR`      | 固定长度字符串(1-255)                   | `CHAR(10)`                  |
| **日期/时间** | `DATE`      | 日期，格式：YYYY-MM-DD                  | `'2024-01-15'`              |
|               | `TIMESTAMP` | 时间戳，纳秒精度                        | `'2024-01-15 10:30:45.123'` |
| **布尔型**    | `BOOLEAN`   | 布尔值                                  | `TRUE`, `FALSE`             |
| **二进制**    | `BINARY`    | 字节数组                                | 用于存储图片、文件等        |

复杂数据类型

| 数据类型    | 描述             | 示例                   | 访问方式           |
| ----------- | ---------------- | ---------------------- | ------------------ |
| `ARRAY`     | 同类型元素数组   | `array(1,2,3)`         | `arr[0]`, `arr[1]` |
| `MAP`       | 键值对集合       | `map('a',1,'b',2)`     | `map['a']`→ `1`    |
| `STRUCT`    | 结构体，类似对象 | `struct('Tom', 25)`    | `struct.name`      |
| `UNIONTYPE` | 联合类型(较少用) | 可存储多种类型中的一个 |                    |

### 5.2.2 创建/删除表

指定数据库创建表

```mysql
USE myhive;
CREATE TABLE test_table(
    id INT,
    name STRING,
    gender STRING
);

# 或者是 

CREATE TABLE myhive.test_table(
    id INT,
    name STRING,
    gender STRING
);
```

删除表

```mysql
DROP TABLE myhive.test_table;
```

### 5.2.3 内部表(Managed Table)

Hive中可以创建的表类型

| 表类型     | 存储控制                                    | 数据删除                     | 主要特点                             | 使用场景                                                     |
| ---------- | ------------------------------------------- | ---------------------------- | ------------------------------------ | ------------------------------------------------------------ |
| **内部表** | Hive 管理，默认存储在`/user/hive/warehouse` | 删除表时**同时删除数据**     | 默认表类型，完全由Hive管理           | 中间表、临时表、不需要保留的测试表                           |
| **外部表** | 外部管理,`LOCATION`关键字指定               | 只删除元数据，**不删除数据** | 数据与元数据解耦，数据在HDFS指定位置 | 源数据表、需要多系统共享的数据（Hive、Spark、Impala等）、数仓ODS层原始数据 |
| **分区表** | 按目录分区                                  | 删除表时同内部/外部表        | 按字段值分区存储，提高查询效率       | 时间序列数据、按地区/类别分类的大表                          |
| **分桶表** | 按文件分桶                                  | 删除表时同内部/外部表        | 按字段哈希分桶，便于抽样和JOIN优化   | 大表JOIN优化、数据抽样、数据倾斜优化                         |

**内部表（Managed Table）**：

默认表类型，不加 `EXTERNAL`就是内部表

数据存储在 Hive 默认仓库路径：`/user/hive/warehouse/数据库名/表名`

删除表时：`DROP TABLE student_managed;`会**同时删除元数据和HDFS数据文件** 

```mysql
-- 创建内部表（默认）
CREATE TABLE IF NOT EXISTS student_managed (
    id INT,
    name STRING,
    score DOUBLE
)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ',';
```

元数据可以通过连接hive配置的mysql数据库的`TBLS`表查看

```mysql
select * from hive.TBLS
```

| TBL_ID | CREATE_TIME   | DB_ID | LAST_ACCESS_TIME | OWNER  | OWNER_TYPE | RETENTION | SD_ID | TBL_NAME   | TBL_TYPE      | VIEW_EXPANDED_TEXT | VIEW_ORIGINAL_TEXT | IS_REWRITE_ENABLED |
| ------ | ------------- | ----- | ---------------- | ------ | ---------- | --------- | ----- | ---------- | ------------- | ------------------ | ------------------ | ------------------ |
| 1      | 1,776,345,676 | 1     | 0                | hadoop | USER       | 0         | 1     | test_user  | MANAGED_TABLE |                    |                    | 0                  |
| 6      | 1,777,272,486 | 6     | 0                | hadoop | USER       | 0         | 6     | test_table | MANAGED_TABLE |                    |                    | 0                  |

Hive行格式

自定义列分隔符（默认子段分隔符是`\001`）

```hive
ROW FORMAT DELIMITED
  [FIELDS TERMINATED BY '分隔符']      -- 字段分隔符
  [ESCAPED BY '转义字符']             -- 转义字符
  [COLLECTION ITEMS TERMINATED BY '分隔符']  -- 数组/集合元素分隔符
  [MAP KEYS TERMINATED BY '分隔符']   -- Map键值对分隔符
  [LINES TERMINATED BY '分隔符']      -- 行分隔符（通常不指定，默认\n）
  [NULL DEFINED AS '字符串']          -- NULL值表示
```

### 5.2.4 外部表(External Table)

表必须使用 `EXTERNAL`关键字修饰，并非是hive拥有的表，是临时关联数据去使用

必须指定 `LOCATION`（指向已存在的HDFS路径）

删除表时：`DROP TABLE student_external;`只删除**元数据**，**HDFS数据文件保留**

通常用于ODS层，连接原始数据

```mysql
-- 创建外部表
CREATE EXTERNAL TABLE student_external (
    id INT,
    name STRING,
    score DOUBLE
)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
LOCATION '/data/students';  -- 指定数据存储位置
```

- 可以先有表，再把数据移动到表指定的LOCAITON中
- 先有数据，再创建表通过LOCATION指向数据

#### 文件->表

1、linux中创建一个测试文件 `/test_external.txt`

```bash
vim test_external.txt
```

填入（`\t`分隔符）

```text
1	name1
2	name2
3	name3
```

2、将文件传入HDFS指定位置 `/data/input/test_external.txt`

```bash
[hadoop@node1 ~]$ hdfs dfs -put test_external.txt /data/input/test_external.txt
[hadoop@node1 ~]$ hdfs dfs -ls /data/input/
Found 1 items
drwxr-xr-x   - hadoop supergroup          0 2026-04-27 17:28 /data/input/test_external.txt
```

3、根据写入的文件格式，创建外部表（`LOCATION 指向目录`）

```hive
CREATE EXTERNAL TABLE test_external(
	id INT,
    name STRING
)
ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t' 
LOCATION '/data/input/';

select * from test_external;
```

效果：

| id   | name  |
| ---- | ----- |
| 1    | name1 |
| 2    | name2 |
| 3    | name3 |

#### 表->文件

反之一样。先创建表后，当路径LOCATION路径中存在文件则立刻可以在hive中查到

#### 删除 

删除hdfs文件

```bash
[hadoop@node1 ~]$ hdfs dfs -rm -r /data/input/test_external.txt
2026-04-27 18:08:07,243 INFO fs.TrashPolicyDefault: Moved: 'hdfs://node1:8020/data/input/test_external.txt' to trash at: hdfs://node1:8020/user/hadoop/.Trash/Current/data/input/test_external.txt
```

删除hive表

```hive
DROP TABLE test_external;
```

### 5.2.5 内外部表转换

查看表类型

```hive
DESC FORMATTED test_table;
DESC FORMATTED test_external;
```

内外部表的区别：

![image-20260427181947687](./assets/image-20260427181947687.png)

转换内外部表

内->外

```hive
ALTER TABLE test_table SET TBLPROPERTIES('EXTERNAL'='TRUE')
```

外->内

```hive
ALTER TABLE test_table SET TBLPROPERTIES('EXTERNAL'='FALSE')
```

注意括号内的参数和值是大小写敏感的，必须全部使用大写