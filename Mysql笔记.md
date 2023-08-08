# 课堂笔记

## 软件安装

[安装参考](https://blog.csdn.net/SoloVersion/article/details/123760428 "from csdn")

## 主流数据库

+ 关系型数据库：
  + MySQL
  + SQLite
  + SQL Server
  + Oracle
+ 非关系型数据库：
  + MongoDB
  + Redis

## 基本概念

+ 数据库管理系统(DBMS)
+ 数据库(DB)
+ 表(Table)
+ 列(Column)
+ 行(Row)
+ 主键(Primary Key)
+ SQL(Structured Query Language):结构化查询语言

## MySQL启动

+ 软件启动
  + 开始->MySQL->MySQL5.7->123456
  + net start mysql57
  + Windows+r打开cmd输入: mysql -uroot -p 123456
    + welcome... 安装成功
+ 命令行中退出
  + Exit
  + Quit
  + \q

## 数据库基本命令

+ 显示数据库

```sql
show databases;
```

+ 创建数据库

```sql
create database [if not exists] 数据库名;
```

+ 使用数据库

```sql
use 数据库名;
```

+ 查询当前数据库信息
  
```sql
# 查询当前连接的数据库
select database();
# 查询当前的数据库版本
select version();
# 查询当前的日期
select now();
# 查询当前的用户
select user();
```

+ 删除数据库
  
```sql
drop database [if exists] 数据库名;
```

+ 显示数据库中的表

```c
show tables;
```

+ 导入数据库脚本(结尾不加分号)

```sql
source 脚本文件路径
```

+ 查看表的基本结构

desc 表名;
desc emp;

+ 查看数据库/表的创建语句

```sql
show create database 数据库名;
show create table 表名;
```

## 基本查询

### 查询字段

+ 查询指定字段
  
```sql
select 字段1, 字段2, ... from 表名;
```

+ 查询全部字段

```sql
select * from 表名;
```

### 条件查询

使用where语句, 放在from后

```sql
select * from 表名 where 条件;
```

### 运算符

+ 算数运算符: +-*/%

```sql
# 员工年工资
select * from emp where sal * 12 > 20000;
```

+ 比较运算符:
+ 逻辑运算符： and or not
