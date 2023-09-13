- -
- 不要把 select 子句写成 `select *`
-
- 返回结果集数量太多了
  collapsed:: true
	- 需要先读取表结构，换成字段名称
- 谨慎使用模糊查询
- -
- 对 order by 排序的字段设置索引
-
- 索引是二叉树机制，索引建立就是有序的了，所以不用做额外的排序计算
- -
- 少用 is null 和 is not null
-
- 会让 mysql 跳过索引，进行全表查询。
-
- null 值无法进行排序，所以不会记录在二叉树里，所以与 null 值有关的判定都不会走索引。
-
- 避免条件语句中的数据类型转换
-
- ```
  select ename from t_emp where deptno='20'
  ```
- ```
  - ```
  - ```
  Copied!
  ```
-
- -
- 在我们的苦衷 deptno 是整数类型，这里写了字符串类型，mysql 需要先转换类型，再匹配，这会影响执行速度
- -
- 在表达式左侧使用 **运算符和函数** 都会让索引失效
- ```
  -- 查询年薪超过 12 万的员工
  select ename from t_emp where salary * 12 > 100000;
  -- 可以改写为
  select ename from t_emp where salary > 100000 / 12;
  -- 查询 2000 年以后入职的员工
  select ename from t_emp where year(hiredate) >= 2
  -- 可以改写为
  select ename from t_emp where year >= '2000-01-01 00:00:00';
  
  ```
-
-
- ## 慢查询日志作用
- 慢查询日志会把查询耗时，超过规定时间的 SQL 语句记录下来
	- 利用慢查询日志，定位分析性能的瓶颈
-
- 默认情况下，MySQL 是不启用慢查询日志的。
-
- ```
  show variables like 'slow_query%';
  ```
- ```
  - ```
  - ```
  Copied!
  ```
- | Variable_name |   | Value |
  | ---- | ---- | ---- |
   | slow_query_log |   | OFF |
   | slow_query_log_file |   | /usr/local/mysql/sql_log/slowlog.log |
-
- `slow_query_log`：慢查询开启状态
-
- `slow_query_log_file`：慢查询日志存放位置
-
- ## EXPLAIN
- 从慢查询日志看到那些 SQL 语句查询慢，那么可以通过 explain 针对这些语句进行执行计划的查看，然后分析它为什么这么慢
-
- ```
  explain
  select id, dname
  from t_dept;
  ```
- ```
  - ```
  - ```
  Copied!
  ```
-
- 执行计划为
- | id |   | select_type |   | table |   | partitions |   | type |   | possible_keys |   | key |   | key_len |   | ref |   | rows |   | filtered |   | Extra |
  | ---- | ---- | ---- |
   | 1 |   | SIMPLE |   | t_dept |   | NULL |   | index |   | NULL |   | unq_dname |   | 802 |   | NULL |   | 7 |   | 100 |   | Using index |
-
- 这里 type=index 说明使用了索引，并使用了索引 kye=unq_dname，返回了 rows=7 行数据；
-
- 如果这里 type=all，那么就是全表扫描，可以考虑优化它，让它走索引
-
- ```
  explain
  select id, dname
  from t_dept
  where id = 10;
  ```
- ```
- ```
- ```
- ```
-
-
	- kettle 连接数据库服务端，对字段使用字段筛选，字符操作，或者Pivot ，switch case 、if 等条件流程控件对数据进行分片， java脚本，sql脚本，增量更新。创建工作项 顺序层层filter 或者计算处理，最终输出各细化维度的表。