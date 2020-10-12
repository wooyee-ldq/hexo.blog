---
title: SQL语句
date: 2019-08-28 22:06:06
tags: RDBMS
---

## RDBMS，通过SQL语句操作数据库

---

### ***SQL基本操作语句：***

```sql
登录mysql： mysql -uroot -p
显示数据库： show databases;
显示当前数据库版本： select version();
显示当前时间： select now();
执行sql文件： source xx.sql;
创建数据库： create database database_name;
删除数据库： drop database database_name;
显示创建数据库的过程： show create database database_name;
选择使用数据库： use database_name;
显示当前使用的数据库： select database();
显示当前数据库的表： show tables;
创建表： create table table_name(
		字段名 数据类型 约束条件 默认值
		...
		...
	);
注意：{
	基本约束条件有：
		unsigned : 无符号类型 【如：tinyint，-128-127，变成无符号类型，0-255】
		null : 可以为空【默认】
		not null : 不可为空
		primary key : 主键
		auto_increment : 数值递增
		default xxx : 设置默认值为xxx
}
删除表： drop table table_name;
修改表名： rename table old_table_name to  new_table_name;
显示创建表的过程： show create table table_name;
显示某个表结构： desc table_name;
向表插入数据： insert into table_name(字段...) values(对应的值...);
向表查询数据： select 字段名1, 字段名2, ... from table_name;
向表添加字段： alter table table_name add 字段名 数据类型 约束条件 默认值;
向表修改字段的类型和约束： alter table table_name modify 字段名 新的(数据类型 约束条件 默认值);
向表修改字段名或者类型和约束条件： alter table table_name change 原字段名 新字段名 (数据类型 约束条件 默认值);
向表删除字段： alter table table_name drop 字段名;
向表修改记录信息： update table_name set 字段名1=新值， 字段名2=新值，... where 条件(id=？);
向表删除记录： delete from table_name where 条件;
```

---

### ***SQL查询语句：  -- []表示可有可无***

```sql
1. select * from table_name [where 条件1 and 条件2 or 条件3 and not 条件4];  -- where是条件查询
2. select 字段名1, 字段名2,... from table_name [where 条件1 and 条件2 or 条件3 and not 条件4];
3. select table_name.字段名1, table_name.字段名2,... from table_name [where 条件1 and 条件2 or 条件3 and not 条件4];
4. select tn.字段名1, tn.字段名2,... from table_name as tn [where 条件1 and 条件2 or 条件3 and not 条件4];
5. select 字段名1 as 别名, 字段名2 as 别名,... from table_name [where 条件1 and 条件2 or 条件3 and not 条件4];
6. select distinct * from table_name [where 条件1 and 条件2 or 条件3 and not 条件4];  -- distinct是消除重复的结果
7. select * from table_name [where 条件1 and 条件2 or 条件3 and not 条件4]; -- 使用and、or、not的多个条件查询
8. select * from table_name where 字段名 like "%关%键%字%";  -- 模糊查询，%表示0个或多个任意字符，_表示一个任意字符
9. select * from table_name where 字段名 rlike 正则表达式;  --  使用正则表达式来进行模糊查询，效率比较高
10. select * from table_name where 字段名 [not] in (值1, 值2, ...);  -- 范围查询
11. select * from table_name where 字段名 [not] between ... and ...; -- 范围查询
12. select * from table_name where 字段名 is [not] null;  -- 空判断条件，是空或者不是空
13. select * from table_name [where 条件] order by 字段名1 [, 字段名2, ...] [asc(默认)/desc] -- asc是默认值，是升序
14. -- 聚合函数查询：{count(), max(), min(), avg(), sum(), round()} : 
    select count(字段名) from table_name [where 条件];  -- 取总条数
    select max(字段名) from table_name [where 条件];  -- 取最大值
    select min(字段名) from table_name [where 条件];  -- 取最小值
    select avg(字段名) from table_name [where 条件];  -- 取平均值
    select sum(字段名) from table_name [where 条件];  -- 取求和
    select round(xxx.xxx, y) from table_name [where 条件];  -- 四色五入或取位，把 xxx.xxx 取 y 位小数
15. -- 分组操作，一般和聚合函数一起使用 : 
    select 聚合函数, 分组字段/分组条件 from table_name [where 条件] group by 分组字段/分组条件;
    select 分组字段/分组条件, group_concat(字段名1, [, 分隔符,] 字段名2, ...) from table_name [where 条件] group by 分组字段/分组条件;
16. -- having是对查询结果[分组结果]的条件筛选操作，where是对原始表的全部数据进行筛选操作 : 
    select 分组字段/分组条件, ... from table_name [where 条件] group by 分组字段/分组条件 having 条件(集合函数条件或其他条件)
17. -- limit(一般用来进行分页操作) ，注意：limit操作要放在语句最后: 
    select * from table_name [where 条件] limit [0, ] x个数;  -- 表示查询 x 个记录， 默认是从第一条记录开始
18. -- 连接查询{
    - 内连接查询 : 查询结果是两个表匹配到的数据 : (表名1 inner join 表名2 on 条件)
    - 右连接查询 : 查询结果是两个表匹配到的数据，右表特有的数据，对于左边不存在的数据使用null填充 : (表名1 right join 表名2 on 条件)
    - 左连接查询 : 查询结果是两个表匹配到的数据，左表特有的数据，对于右边不存在的数据使用null填充 : (表名1 left join 表名2 on 条件))
      }
      select * from 表1 inner join 表2 on 两个表的字段连接条件 [having 条件] [order by 条件];
      select * from 表1 left join 表2 on 两个表的字段连接条件 [having 条件] [order by 条件];  
      -- 右连接比较少用，如需要直接把左连接的表位置交换
      -- 自关联查询，是同一个表的连接查询，如：省市级联表的自关联操作
19. 子查询： 使用子查询的结果作为父查询的条件查询
    select * from table_name where 字段名/条件=(select xxx from table_name where 条件);
```

---

> ### sql基本操作差不多就是这些了～

