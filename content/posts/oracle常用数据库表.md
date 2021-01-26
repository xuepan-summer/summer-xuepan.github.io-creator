---
title: "Oracle常用数据库表"
date: 2021-01-26T16:35:55+08:00
draft: false
---

**oracle 数据库表**

dba_indexes  索引的统计信息

dba_tables     数据库中的所有表

dba_tab_columns  查询表的列属性

分区相关的数据库表：

dba_part_indexes  数据库中所有分区索引的对象级分区信息，其列与ALL_PART_INDEXES中的列相同

user_ind_subpartitons   USER_IND_SUBPARTITIONS为当前用户拥有的每个索引子分区描述分区级别的分区信息，该子分区的存储参数以及ANALYZE语句收集的各种分区统计信息。 其列与“ ALL_IND_SUBPARTITIONS”中的列相同。 

dba_indexs：

| 字段                    | 说明                                                         |
| ----------------------- | ------------------------------------------------------------ |
| OWNER                   | 索引拥有者                                                   |
| INDEX_NAME              | 索引名字                                                     |
| INDEX_TYPE              | 索引类型                                                     |
| TABLE_OWNER             | 表的拥有者                                                   |
| TABLE_NAME              | 表名                                                         |
| TABLE_TYPE              | 表类型                                                       |
| UNIQUENESS              | 是否唯一                                                     |
| COMPRESSION             | 是否压缩                                                     |
| PREFIX_LENGTH           | 压缩键上前缀的列数量                                         |
| TABLESPACE_NAME         | 属于哪个表空间                                               |
| INI_TRANS               | 事务表的初始大小由对象的INI_TRANS设置指定，默认2             |
| MAX_TRANS               | 最大的MAX_TRANS条目，默认255                                 |
| INITIAL_EXTENT          | 初始化区大小65536                                            |
| NEXT_EXTENT             | 第二个区大小1048576                                          |
| MIN_EXTENTS             | 段中允许的最小区大小                                         |
| MAX_EXTENTS             | 段中允许的最大区大小，默认2g                                 |
| PCT_INCREASE            | 后面区是前面区的增长百分比                                   |
| PCT_THRESHOLD           | 每个块中允许索引入口的百分比阀值                             |
| INCLUDE_COLUMN          | 索引组织表主键索引中包含最后一列的列ID                       |
| FREELISTS               | 分配到这个段的进程自由列表数量                               |
| FREELIST_GROUPS         | 分配到这个段的进程自由列表组的数量                           |
| PCT_FREE                | 一个块中最小自由空间的百分比                                 |
| LOGGING                 | 索引改变是否记录到日志                                       |
| BLEVEL                  | B树索引等级（从根块到叶子块的深度）                          |
| LEAF_BLOCKS             | 索引中叶子块的数量                                           |
| DISTINCT_KEYS           | 不同索引值的数量                                             |
| AVG_LEAF_BLOCKS_PER_KEY | 索引中的每个值平均在多少个叶子块中，如果是唯一或者主键，那么值恒等于1 |
| AVG_DATA_BLOCKS_PER_KEY | 通过索引中的一个值指向表中的数据块，该数据块数量的平均值     |
| CLUSTERING_FACTOR       | 聚集因子，表示表中行基于索引排序程度                         |
| STATUS                  | 表示一个未分区的索引是合法的还是不可用的                     |
| SAMPLE_SIZE             | 分析索引的参样大小                                           |
| LAST_ANALYZED           | 最近分析索引统计信息的日期                                   |
| DEGREE                  | 每个实例扫描索引的线程数                                     |
| INSTANCES               | 索引被多少实例扫描                                           |
| PARTITIONED             | 索引是否分区                                                 |
| TEMPORARY               | 索引是否在临时表中                                           |
| GENERATED               | 索引名字是否是系统产生                                       |
| SECONDARY               | 索引是否通过ODCIndexCreate方法创建                           |
| BUFFER_POOL             | 用于索引块的缓冲池                                           |
| FLASH_CACHE             | 数据库 smart flash cache 的 hint用于索引块                   |
| CELL_FLASH_CACHE        | CELL_FLASH_CACHE的hint用于索引块                             |
| USER_STATS              | 静态统计是否直接被用户使用                                   |
| DURATION                | 临时表空间的持续时间                                         |
| PCT_DIRECT_ACCESS       | 对于索引组织表上的secondary index ,行百分比的合理猜测        |
| ITYP_OWNER              | 对于域索引，索引类型的拥有者                                 |
| ITYP_NAME               | 对于域索引，索引类型名字                                     |
| PARAMETERS              | 对于域索引，参数字符串                                       |
| GLOBAL_STATS            | 索引的统计是否收集齐了                                       |
| DOMIDX_STATUS           | 域索引的状态                                                 |
| DOMIDX_OPSTATUS         | 域索引的操作状态                                             |
| FUNCIDX_STATUS          | 基于函数索引的状态                                           |
| JOIN_INDEX              | 索引是否是结合的                                             |
| IOT_REDUNDANT_PKEY_ELIM | 在索引组织表中，冗余的主键列是否从从索引中删除               |
| DROPPED                 | 索引是否已经被删除，并在recycle中                            |
| VISIBILITY              | 索引是否可见                                                 |
| DOMIDX_MANAGEMENT       | 如果是域索引，主索引是系统管理还是用户管理                   |
| SEGMENT_CREATED         | 索引段是否已经创建                                           |

dba_tables：

| Column                     | Datatype     | NULL     | Description                                                  |
| -------------------------- | ------------ | -------- | ------------------------------------------------------------ |
| OWNER                      | VARCHAR2(30) | NOT NULL | 属主                                                         |
| TABLE_NAME                 | VARCHAR2(30) | NOT NULL | 表名                                                         |
| TABLESPACE_NAME            | VARCHAR2(30) |          | 表空间，分区、临时和索引组织表的值为空                       |
| CLUSTER_NAME               | VARCHAR2(30) |          | 集群                                                         |
| IOT_NAME                   | VARCHAR2(30) |          | 索引组织表的名称（如果有的话），属于溢出或映射表项。如果 iot_type 列不为空，则此列包含基表名称 |
| STATUS                     | VARCHAR2(8)  |          | 如果先前的删除表操作失败，则指示表是否不能使用（无效）或有效（有效）。 |
| PCT_FREE                   | NUMBER       |          | 块中空闲空间的最小百分比；分区表值为空                       |
| PCT_USED                   | NUMBER       |          | 块中使用空间的最小百分比；分区表值为空                       |
| INI_TRANS                  | NUMBER       |          | 初始事务数；分区表值为空                                     |
| MAX_TRANS                  | NUMBER       |          | 事务的最大数量；分区表值为空                                 |
| INITIAL_EXTENT             | NUMBER       |          | 初始区域的大小（以字节为单位）；分区表值为空                 |
| NEXT_EXTENT                | NUMBER       |          | 二级范围的大小（以字节为单位）；分区表值为空                 |
| MIN_EXTENTS                | NUMBER       |          | 段中允许的最小区段数；分区表值为空                           |
| MAX_EXTENTS                | NUMBER       |          | 区段中允许的最大区段数；分区表值为空                         |
| PCT_INCREASE               | NUMBER       |          | 范围大小的百分比增加；分区表值为空                           |
| FREELISTS                  | NUMBER       |          | 用于insert操作的数据块的列表，分区表值为空                   |
| FREELIST_GROUPS            | NUMBER       |          | 用于insert操作的数据块的列表组，分区表值为空                 |
| LOGGING                    | VARCHAR2(3)  |          | 日志表属性，分区表值为空                                     |
| BACKED_UP                  | VARCHAR2(1)  |          | 上次更改后表是否已备份                                       |
| NUM_ROWS*                  | NUMBER       |          | 表中的行数                                                   |
| BLOCKS*                    | NUMBER       |          | 表中使用的数据块的个数                                       |
| EMPTY_BLOCKS*              | NUMBER       |          | 表中空闲的数据块的个数                                       |
| AVG_SPACE*                 | NUMBER       |          | 分配给表的数据块中的平均空闲空间（以字节为单位）             |
| CHAIN_CNT*                 | NUMBER       |          | 在被从一个数据块到另一个表中的行数，或迁移到一个新块，需要保留一部分旧的rowid |
| AVG_ROW_LEN*               | NUMBER       |          | 表中一行的平均长度（以字节为单位）                           |
| AVG_SPACE_FREELIST _BLOCKS | NUMBER       |          | freelist的所有块的平均空间                                   |
| NUM_FREELIST_BLOCKS        | NUMBER       |          | freelist 的块的个数                                          |
| DEGREE                     | VARCHAR2(10) |          | 扫描表的每个实例的线程数                                     |
| INSTANCES                  | VARCHAR2(10) |          | 要扫描该表的实例数。                                         |
| CACHE                      | VARCHAR2(5)  |          | 指示表是否要缓存在缓冲区缓存（y）或不（n）中。               |
| TABLE_LOCK                 | VARCHAR2(8)  |          | 指示是否已启用表锁（启用）或禁用（禁用）。                   |
| SAMPLE_SIZE                | NUMBER       |          | 用于分析此表的样本大小                                       |
| LAST_ANALYZED              | DATE         |          | 最近分析这张表的日期                                         |
| PARTITIONED                | VARCHAR2(3)  |          | 指示此表是否分区。设置 是 如果是分区。                       |
| IOT_TYPE                   | VARCHAR2(12) |          | 如果这是一个索引组织表，值为 IOT, IOT_OVERFLOW, 或者 IOT_MAPPING，否则为NULL |
| TEMPORARY                  | VARCHAR2(1)  |          | 当前会话只能看到它放在这个对象本身中的数据吗？               |
| SECONDARY                  | VARCHAR2(1)  |          | 是否被ODCIIndexCreate 触发创建                               |
| NESTED                     | VARCHAR2(3)  |          | 指示表是否是嵌套表（yes）或否（NO）。                        |
| BUFFER_POOL                | VARCHAR2(7)  |          | 该对象的默认缓冲池。 分区表为空                              |
| ROW_MOVEMENT               | VARCHAR2(8)  |          | 是否已启用或禁用分区行移动                                   |
| GLOBAL_STATS               | VARCHAR2(3)  |          | 对于分区表，指示数据收集表作为一个整体（是）或来自潜在的分区和子分区统计估计（否） |
| USER_STATS                 | VARCHAR2(3)  |          | 指示用户是否直接输入统计数据（是）（否）                     |

| SKIP_CORRUPT  | VARCHAR2(8)  |      | Oracle数据库是否忽略表和索引扫描中标记为已损坏的块（启用）或引发错误（禁用）。要启用此功能，运行 dbms_repair.skip_corrupt_blocksprocedure。 |
| ------------- | ------------ | ---- | ------------------------------------------------------------ |
| MONITORING    | VARCHAR2(3)  |      | 表是否有 监测 属性设置                                       |
| CLUSTER_OWNER | VARCHAR2(30) |      | 表所属的群集的所有者，如果有的话                             |
| DEPENDENCIES  | VARCHAR2(8)  |      | 指示是否启用了行级依赖跟踪（启用）或禁用（禁用）。           |
| COMPRESSION   | VARCHAR2(8)  |      | 指示是否启用表压缩（启用）或禁用（已禁用）；分区表为空值。   |
| DROPPED       | VARCHAR2(3)  |      | 指示表是否已被删除并处于回收站（是）或否（否）中；分区表为空值。 |

dba_tab_columns：

| 名称           | 类型                   | 描述                                                         |
| -------------- | ---------------------- | ------------------------------------------------------------ |
| owner          | character varying(64)  | 表的所有者                                                   |
| table_name     | character varying(64)  | 表名                                                         |
| column_name    | character varying(64)  | 列名                                                         |
| data_type      | character varying(128) | 列的数据类型                                                 |
| column_id      | integer                | 创建表时列的序号                                             |
| data_length    | integer                | 列的字节长度                                                 |
| comments       | text                   | 注释                                                         |
| avg_col_len    | numeric                | 列的平均长度（单位字节）                                     |
| nullable       | bpchar                 | 该列是否允许为空，对于主键约束和非空约束，该值为n            |
| data_precision | integer                | 数据类型的精度，对于numeric数据类型有效，其他类型为NULL      |
| data_scale     | integer                | 小数点右边的位数，对于numeric数据类型有效，其他类型为0       |
| char_length    | numeric                | 列的长度（以字符计），只对varchar，nvarchar2， bpchar，char类型有效 |

