# 五、SQL语法入门 
## 1.SQL语句概述
### 1.1SQL语句介绍
* 维基百科的定义：SQL（Structured Query Language，结构化查询语言）是一种特定目的的编程语言，用于管理关系数据库管理系统，或在关系流数据管理系统中j进行流处理
* Gauss DB T 是一种关系型数据库，SQL语句包括DDL，DML，DCL和DQL
### 1.2SQL语句分类
* DDL（Data Definition Language）数据定义语言
> * 用于定义或修改数据库中的对象，如：表，索引，视图，序列，用户，角色，表空间
* DML（Data Manilulation Language）数据操纵语言
> * 用于对数据库表中的数据进行操作，如：插入，更新，删除
* DCL（Data Control Language）数据控制语言
> * 用来设置或更改数据库事务，权限操作（用户，角色授权，权限回收），锁表（支持共享索和排他锁），停机
DQL（Data Query Language）数据查询语言
> * 用来查询数据库内的数据，如单表查询，多表查询
## 2.数据类型
### 2.1数据类型
* 数据类型是数据的一个基本属性，主要用于建表时指定字段的数据类型
> * 常用的的数据类型
>> * 数值类型，字符类型，日期类型
> * 非常用数据类型
>> * 二进制类型，布尔类型，时间间隔类型
### 2.2常用的数据类型
* 整性类型
> * integer(32位有符号整数)
>> * 占用字节：4
>> * 关键字：int，integer，binary_integer，int signed，integer signed
> * integer unsigned（32位无符号整数）
>> * 占用字节：4
>> * 关键字：uint，binary_unit32，integer unsigned
> * bigint（64位有符号整数）
>> * 占用字节：
>> * 关键字：bigint，binary_bigint, bigint signed
* 浮点类型
> * float
>> * 占用字节：8
>> * 关键字：real，float，double，binary_double
* 高精度数值类型
> * decimal/number
>> * 占用字节：4-24，长度与其有效数字有关
>> * 关键字：decimal，number，numeric
>> * 语法格式：number/decimal，number/decimal（p），number/decimal（p，s）
> * 数据类型控制参数（USE_NATIVE_DATATYPE)
>> * 数据类型：bigint，double，float，int，integer，real，smallint，tinyint  
>> * TRUE:映射为binary_double类型
>> * FALSE:映射为number类型
* 字符类型
> * 编码类型
>> * UTF8编码：汉字和全角字符占2-8个字节，数字和英文1个字节
>> * GBK编码：汉字和全角字符占2个字节，数字等字符占1个字节
> * 定长字符串类型（1-8000字节，若输入长度小于size，则利用空格在右端补齐）
>> * char（size[byte|char]):存储定长字节或者字符串
>>> * 默认为byte类型，关键字为char
>>> * size byte:最大能容纳的字节数，size char：最大能容纳的字符数
>> * nchar（size):存储定长字符串
>>> * 等同于char（size char）
>>> * 关键字：nchar


