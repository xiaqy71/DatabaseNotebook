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
select * from 表名; -- 适用于在命令行或者可视化工具简单查询 不适用代码中
```

### 条件查询

使用where语句, 放在from后

```sql
select * from 表名 where 条件;
```

### 运算符

+ 算数运算符: +-*/%

%：匹配任意数量的任意字符  
_：匹配任意单个字符

```sql
# 员工年工资
select * from emp where sal * 12 > 20000;
```

+ 比较运算符:
+ 逻辑运算符： and or not

### 表

#### 数据类型

+ 整形
  + TINYINT
  + SAMLLINT
  + MEDIUMINT
  + INT
  + BIGINT
+ 浮点型和定点型
  + FLOAT
  + DOUBLR
  + DECIMAL
+ 日期时间类型
  + YEAR
  + TIME
  + DATE
  + DATETIME
  + TIMESTAMP
+ 字符型
  + CHAR
  + VARCHAR
  + TINYTEXT
  + TEXT
  + MEDIUMTEXT
  + LONGTEXT
  + ENUM
  + SET

### DDL(数据定义语言)

#### 查看表

+ 显示数据库中的表

```sql
show tables;
```

+ 查看表的基本结构

```sql
desc 表名;
```

+ 查看数据库/表的创建语句

```sql
show create database 数据库名;
show create table 表名;
```
  
#### 修改表

+ 添加字段

```sql
alter table 表名
add column 新列名 数据类型 [约束条件] [first | after 列名];
```

+ 修改字段的类型

```sql
alter table 表名
modify column 列名 数据类型 [约束条件];
```

+ 修改字段的位置

```sql
alter table 表名
modify column 列名 数据类型 first | after 列名;
```

+ 修改字段名

```sql
alter table 表名
change column 旧列名 新列名 数据类型;
```

+ 删除字段

```sql
alter table 表名;
drop column 列名;
```

#### 重命名表

```sql
alter table 旧表名
rename to 新表名;
```

#### 删除表

```sql
drop table [if exists] 表1[,表2，表3...];
```

### DML（数据操作语言）

#### 插入数据

```sql
insert into 表名
values(
  字段1的值,
  字段2的值,
  ...
);
```

更安全的方法：指定字段名

```sql
insert into 表名
(
  字段1,
  字段2,
  ...
)
values(
  字段1的值,
  字段2的值,
  ...
);
```

#### 更新数据

```sql
update 表名
set 字段1 = 字段1的值
    字段2 = 字段2的值
where 限制条件;
```

#### 删除数据

```sql
delete from 表名
where 限制条件;
```

### 约束

constraint

|约束条件|非空约束|默认约束|唯一约束|主键约束|外键约束|
|-------|------|------|-------|------|-------|
|关键字|not null|default|unique|primary key|foreign key|

#### 非空约束

+ 创建表时设置非空约束

```sql
create table 表名(
  字段名 字段类型 not null,
  ...
);
```

```sql
drop table if exists users;
create table users(
  id int not null,
  name varchar(20)
);
# 报错，id没有默认值，不允许为空
insert into user(name) values("李四");
```

+ 已有字段添加非空约束

```sql
alter table 表名
modify column 字段名 字段类型 not null;
```

+ 删除非空约束
  
  ```sql
  alter table 表名
  modify column 字段名 字段类型;
  ```

#### 默认约束

```sql
create table 表名(
  字段名 字段类型 default 默认值,
  ...
);
```

```sql
drop table if exists users;
create table users(
  id int not null default 666,
  name varchar(20)
);
# 不报错
insert into users(name) values("李四");
select * from users;
```

#### 唯一约束

+ 列级

```sql
create table 表名(
  字段名 字段类型 unique,
  ...
);
```

```sql
drop table if exists users;
create table users(
  id int not null default 666,
  name varchar(20) unique
);
insert into users(id, name) values(1, "李四");
insert into users(id, name) values(2, "李四")
insert into users(id) values(3);
insert into users(id) values(4);
```

+ 表级

```sql
create table 表名
  字段1 字段类型,
  字段2 字段类型,
  ...
  [constraint 约束名] unqiue(字段1[,字段2, ...])
```

+ 已有字段添加唯一约束

```sql
alter table 表名
modify 字段名 字段类型 unique;

alter table 表名
add [constraint 约束名] unique(字段名) ;
```

+ 删除唯一约束

```sql
alter table 表名
drop index 约束名;

alter table 表名
drop key 约束名;
```

#### 主键约束

+ 每个表都应该定义主键
+ 主键的值不应该修改
+ 不使用可能会修改的列作为主键（与业务无关， 通常使用id作为主键）

```sql
create table 表名(
  字段名 字段类型 primary key,
  ...
);
```

可以给约束起名，可以创建多列的联合主键

```sql
create table 表名(
  字段1 字段类型,
  字段2 字段类型,
  ...
  [constraint 约束名] primary key(字段1[,字段2, ...])

);
```

删除主键

```sql
alter table 表名
drop primary key;
```

自动递增

```sql
create table 表名(
  字段1 字段类型 auto_increment
);
```

#### 外键约束

```sql
[constraint 外键名] foreign key (列名) references 主表名(主键);
```
