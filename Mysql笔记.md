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

```sql
desc 表名;
desc emp;
```

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

+ 算数运算符: + - *  / %

```sql
# 员工年工资
select * from emp where sal * 12 > 20000;
```

+ 比较运算符: > < >= <= = <>/!= between..and.. (not)in like

```sql
like :
% 匹配任意个任意字符
_ 匹配单个任意字符_
```

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

Data defineition language

#### 创建表

```sql
create table [if not exists] 表名(
    字段1 字段类型 [列级约束条件]
	字段2 字段类型 [列级约束条件]
	...
	[表级约束条件]
)
```

列级约束：not null , primary key

#### 查看表

+ 显示数据库中的表

```sql
show tables;
```

+ 查看表中的基本结构

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

#### 高级查询

##### 排序

order by 子句：对查询结果按指定字段进行排序	

```sql
	order by 字段1[,字段2] [asc|desc]
	select * from emp order by sal desc;
	```

##### 限制数量

limit子句：select语句返回所有匹配的行，它们可能是指定表中的每个行。为了前几行或中间几行，可使用limit子句

```sql
limit 行数（从第一行开始）
limit 开始行（从0开始），行数

select * from emp order by sal limit 1;
select * from emp order by sal limit 3, 5;
```
##### 去重

distinct关键字：用于返回唯一不同的值

```sql
#列出所有岗位，先查询再去重
select distinct job from mep;
```

##### 组合查询

union 操作符：执行多个查询（多条select语句），将结果合并为单个结果集返回

```sql
select 字段1[,字段2,...] from 表1
union
select 字段1[,字段2,...] from 表2;
```

#### 函数
##### 数值函数
+ cell(x): 向上取整
+ floor(x): 向下取整
+ round(x,y=0): 四舍五入
+ truncate(x,y): 截断函数
+ mod(x,y): 返回x/y的余数
+ rand(): 生成0-1的随机数

##### 字符函数

+ concat(s1, s2, ...):：字符串连接，如果任何一个参数为null，则返回值为null
+ concat_ws(x, s1, s2, ...)：指定分隔符的字符连接函数，x是连接分隔符， 如果分隔符为null，则结果为null
+ lower(str)：大写转小写
+ upper(str)：小写转大写
+ length(str)：字符串长度
+ ltrim(str)：删除字符串左侧空格
+ rtrim(str)：删除字符串右侧空格
+ trim(str)：删除字符串两侧空格
+ substr(str, n, len)：截取子字符串，字符串str从n的位置截取长度为len的字符串，如果n为负数，则子字符串的位置起始于字符串结尾的n个字符
+ left(str, n)：返回字符串str的最左边n个字符
+ right(str, n)：返回字符串str的最右边n个字符
+ replace(str, from_str, to_str)：替换函数，字符串str中所有的字符串from_str均被to_str替换，然后返回这个字符串
+ format(x, n)：将数字x格式化，并以四舍五入的方式保留小数点后n位，结果以字符串的形式返回。若n为0， 则返回结果不含小数部分。

##### 日期时间函数

+ curdate()/current_date()：获取当前日期，YYYY-MM-DD 格式
+ curtime()/current_time()：获取当前时间，HH:MM:SS 格式

##### 分组查询

###### 创建分组

group by 子句：根据一个或多个字段对结果进行分组，在分组的字段上可以使用count，sum，avg等函数

```sql
select 字段1[字段2, function(字段1), function(字段2)...]
from 表
group by 字段1;
```

```sql
select count(*) from emp where deptno = 20;

select deptno, coutn(*)
from emp
group by deptno;

```

###### 过滤分组

having子句：having非常类似于where。唯一的差别是where过滤行，而having过滤分组。having必须和group by 一起使用
having和where的区别也可以理解为，where是分组前过滤的，having是分组后过滤的

```sql
select deptno, count(*)
from emp
group by deptno
having count(*) > 5;
```

##### select 完整格式

5. select 字段名
1. from ...
2. where ...
3. group by ...
4. having ...
5. order by ...
6. limit ...
##### 连接查询

```sql
select * from emp, dept;
```

###### 内连接

###### 外连接

##### 子查询

子查询一般与[not] in 结合使用，也可以使用其他运算符：> < = !=
###### 使用子查询过滤

###### 子查询作为计算字段

#### 正则表达式

regexp操作符

like和regexp的区别

##### 匹配单个实例

+ |：表示匹配其中之一，使用 | 从功能上类似or
+ [ ]：匹配字符之一，[ ]是另一种形式的or语句。[123]为[1|2|3]的缩写
+ \[-]: 匹配范围 ，使用-来定义一个范围。例如：[1-3]、[a-z]。
+ \\\\：转义字符，多数正则表达式使用单个反斜杠作为转义字符，但mysql要求两个反斜杠
+ 匹配字符类：存在找出你自己经常使用的 可以使用预定义的字符集，称为字符类

|类|说明|
|--|--|
|\[\[alnum:]]|任意字母和数字|
|\[\[:alpha:]]|任意字符(同\[a-zA-Z0-9])|
|\[\[:blank:]]|空格和制表(同\[\\\\t])|
|...|...|

##### 匹配多个实例

#### 存储过程

##### 使用存储过程

```sql
create procedure 函数名()
begin
	常用语句
end;

# 调用
call 函数名();

# 删除
drop procedure if exists 函数名;

```

##### 参数

```sql
#参数类型
# in    可读不可修改
# out   不可读可修改
# inout 可读可修改
```

##### 变量

```sql
#定义变量
declare 变量名 变量的数据类型 [default 默认值]：
#变量赋值
set 变量名 = 要赋的值;
```

##### 逻辑语句

+ 条件语句(if 、case)

```sql
if condition then
	逻辑代码;
[elseif condition then
	逻辑代码;]
[else
	 逻辑代码;
]
end if;

case
	when condition1 then
		逻辑代码
	when condition2 then
		逻辑代码
	else
		逻辑代码
end case;
```
+ 循环语句(while、repeat)

```sql
while 循环条件 do
end while;

repeat
	逻辑代码
until condition end repeat;
```