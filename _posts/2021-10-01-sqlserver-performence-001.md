---
layout: post
title: ""
date: 2021-10-01
tags: [sql-server, database]
comments: true
author: Jerry8964
---



### Query from a table

* 如果表里面的数据很少，全表扫描(Table Scan)是最有效的方式。
* 如果只有特定键值的几行（即在大量的数据中查找符合特定条件的少数行的时候），则索引可以提高查询效率。
* 如果检索所有行而有一个索引在order by中，则执行索引扫描（Index Scan）可能省去对结果集的单独排序。



### Execute plan

当第一次分析并执行之后，执行计划（Execute Plan）会缓存在SQL Server的Cache中，只有当执行下面的操作的时候，才会把执行计划清理出Cache。

1. Cache满了，而这个执行计划又长时间没有使用了。
2. 有人执行了Alter Procedure （执行计划对应的对象Object）
3. 有人执行了`sp_recompile`，此时会重新编译对象procedure.
4. 有权限的人执行了DBCC FREE PROCCACHE清空了执行计划的Cache
5. SQL Server重新启动了。
6. 某人使用`sp_config`修改了某些参数（视具体情况而定）。

另外，只有下面的对象（Object）才会生成执行计划（Execute Plan）

1. Store Procedure
2. Scalar User-defined Functions
3. Muti-step table-valued Functions
4. Trigger



### option recompile

当表里面的数据量分布不均的时候，SQL Server使用原有的执行计划无法达到最优效果的时候，`option recompile`会通知SQL Server执行的时候重新生成执行计划，这样可能会提高查询的执行效率。

使用方法如下 

```sql
select
 t1.col1, t2.col2
 from table1 t1
 join table2 t2
 on t1.col1 = t2.col1
 option (recomplie)
```





--to be continue--