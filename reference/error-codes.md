---
title: 错误码与故障诊断
category: reference
---

# 错误码与故障诊断

本篇文档描述在使用 TiDB 过程中会遇到的问题以及解决方法。

## 错误码

TiDB 兼容 MySQL 的错误码，在大多数情况下，返回和 MySQL 一样的错误码。另外还有一些特有的错误码：

| 错误码 | 说明 |
| --------------------- | -------------------------------------------------- |
| 8001 | 请求使用的内存超过 TiDB 内存使用的阈值限制 |
| 8002 | 带有 `SELECT FOR UPDATE` 语句的事务，在遇到写入冲突时，为保证一致性无法进行重试，事务将进行回滚并返回该错误 |
| 8003 | `ADMIN CHECK TABLE` 命令在遇到行数据跟索引不一致的时候返回该错误 |
| 8004 | 单个事务过大，原因及解决方法请参考[这里](/faq/tidb.md#433-transaction-too-large-是什么原因怎么解决) |
| 8005 | 事务在 TiDB 中遇到了写入冲突，原因及解决方法请参考[这里](/faq/tidb.md#九故障排除) |
| 8018 | 插件无法重新载入，原因是没有载入过 |
| 8019 | 重新载入的插件版本与之前不同，无法重新载入 |
| 8020 | 表被锁 |
| 8021 | key 不存在 |
| 8022 | 事务提交失败，但可以进行重试 |
| 8023 | 不能设置空值 |
| 8024 | 非法的事务 |
| 8025 | 写入的单条键值对过大 |
| 8026 | 没有实现的接口 |
| 8027 | 表结构版本过期 |
| 8028 | 表结构发生了变化 |
| 8029 | 错误值 |
| 8030 | 转变为带符号正整数时发生了越界，显示为负数 |
| 8031 | 负数转变为无符号数时，被转变为正数 |
| 8032 | 非法的 year 格式 |
| 8033 | 非法的 year 值 |
| 8034 | 不正确的 datetime 值 |
| 8036 | 非法的 time 格式 |
| 8037 | 非法的 week 格式 |
| 8038 | 字段无法获取到默认值 |
| 8039 | 索引的偏移量超出范围 |
| 8042 | 表结构的状态为不存在 |
| 8043 | 列信息的状态为不存在 |
| 8044 | 索引的状态为不存在 |
| 8045 | 非法的表数据 |
| 8046 | 列信息的状态为不可见 |
| 8047 | 设置了不支持的系统变量值，通常在用户设置了数据库不支持的变量值后的告警信息里出现 |
| 8048 | 设置了不支持的数据库隔离级别 |
| 8049 | 载入权限相关表失败 |
| 8050 | 设置了不支持的权限类型 |
| 8051 | 未知的字段类型 |
| 8052 | 来自客户端的数据包的序列号错误 |
| 8053 | 获取到了非法的自增列值 |
| 8055 | 当前快照过旧，数据可能已经被 GC |
| 8056 | 非法的表 ID |
| 8057 | 非法的字段类型 |
| 8058 | 申请了不存在的自动变量类型 |
| 8059 | 获取自动随机量失败 |
| 8060 | 非法的自增列偏移量 |
| 8061 | 不支持的 SQL Hint |
| 8062 | SQL Hint 中使用了非法的 token，与 Hint 的保留字冲突 |
| 8063 | SQL Hint 中限制内存使用量超过系统设置的上限，设置被忽略 |
| 8064 | 解析 SQL Hint 失败 |
| 8065 | SQL Hint 中使用了非法的整数 |
| 8066 | JSON_OBJECTAGG 函数的第二个参数是非法参数 |
| 8101 | 插件 ID 格式错误，正确的格式是 `[name]-[version]` 并且 name 和 version 中不能带有 '-' |
| 8102 | 无法读取插件定义信息 |
| 8103 | 插件名称错误 |
| 8104 | 插件版本不匹配 |
| 8105 | 插件被重复载入 |
| 8106 | 插件定义的系统变量名称没有以插件名作为开头 |
| 8107 | 载入的插件未指定版本或指定的版本过低 |
| 8108 | 不支持的执行计划类型 |
| 8109 | analyze 索引时找不到指定的索引 |
| 8110 | 不能进行笛卡尔积运算，需要将配置文件里的 `cross-join` 设置为 `true` |
| 8111 | execute 语句执行时找不到对应的 prepare 语句 |
| 8112 | execute 语句的参数个数与 prepare 语句不符合 |
| 8113 | execute 语句涉及的表结构在 prepare 语句执行后发生了变化 |
| 8114 | 未知的执行计划类型 |
| 8115 | 不支持 prepare 多行语句 |
| 8116 | 不支持 prepare DDL 语句 |
| 8118 | 构建执行器失败 |
| 8120 | 获取不到事务的 start tso |
| 8121 | 权限检查失败 |
| 8122 | 指定了通配符，但是找不到对应的表名 |
| 8123 | 带聚合函数的 SQL 中返回非聚合的列，违反了 only_full_group_by 模式 |
| 8200 | 尚不支持的 DDL 语法 |
| 8201 | 当前 TiDB 不是 DDL owner |
| 8202 | 不能对该索引解码 |
| 8203 | 非法的 DDL worker |
| 8204 | 非法的 DDL job |
| 8205 | 非法的 DDL job 标志 |
| 8206 | DDL 的 Reorg 阶段执行超时 |
| 8207 | 非法的存储节点 |
| 8210 | 非法的 DDL 状态 |
| 8211 | DDL 的 Reorg 阶段发生了 panic |
| 8212 | 非法的 region 切分范围 |
| 8213 | 非法的 DDL job 版本 |
| 8214 | DDL 操作被终止 |
| 8215 | Admin Repair 表失败 |
| 8216 | 非法的自动随机列 |
| 8221 | Key 编码错误 |
| 8222 | 索引 Key 编码错误 |
| 8223 | 检测出数据与索引不一致的错误 |
| 8224 | 找不到 DDL job |
| 8225 | DDL 已经完成，无法被取消 |
| 8226 | DDL 几乎要完成了，无法被取消 |
| 8227 | 创建 Sequence 时使用了不支持的选项 |
| 9001 | 请求 PD 超时，请检查 PD Server 状态/监控/日志以及 TiDB Server 与 PD Server 之间的网络 |
| 9002 | 请求 TiKV 超时，请检查 TiKV Server 状态/监控/日志以及 TiDB Server 与 TiKV Server 之间的网络 |
| 9003 | TiKV 操作繁忙，一般出现在数据库负载比较高时，请检查 TiKV Server 状态/监控/日志 |
| 9004 | 当数据库上承载的业务存在大量的事务冲突时，会遇到这种错误，请检查业务代码 |
| 9005 | 某个 Raft Group 不可用，如副本数目不足，出现在 TiKV 比较繁忙或者是 TiKV 节点停机的时候，请检查 TiKV Server 状态/监控/日志 |
| 9006 | GC Life Time 间隔时间过短，长事务本应读到的数据可能被清理了，应增加 GC Life Time |
| 9007 | 事务在 TiKV 中遇到了写入冲突，原因及解决方法请参考[这里](/faq/tidb.md#九故障排除) |
| 9008 | 同时向 TiKV 发送的请求过多，超过了限制 |

## 故障诊断

参见[故障诊断文档](/how-to/troubleshoot/cluster-setup.md)以及 [FAQ](/faq/tidb.md)。
