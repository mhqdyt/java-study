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
> * 变长字符串类型（若输入长度小于size，不会利用空格补齐）
>> * varchar(size[byte|char]):存储变长字节或字符串
>>> * size byte：最大能容纳的字节数，size char：最大能容纳的字符数，1-8000字节
>>> * 关键字：varchar
>> * nvarchar(size):用于存储变长字符串
>>> * 1-8000字节
>>> * 关键字：nvarchar
>> * clob:存储大对象变长字符串
>>> * 占用字节：0-4G
>>> * 关键字：clob，text，longtext，long
* 日期类型
> * 不带时区的时间戳（8字节）
>> * datetime/date
>>> * 保存年，月，日，时，分，秒
>>> * 关键字：date，datetime
>>> * 如：2019-08-22 17：29：13
>> * timestamp[(n)]
>>> * 保存年，月，日，时，分，秒，微秒，n取值范围为0-6，默认值为6
>>> * 关键字：timestamp
>>> * 如：2019-08-22 17：29：13.263183 （n=6）  2019-08-22 17：29：13.383 （n=3）
> * 带时区的时间戳
>> * timestamp(n) with time zone
>>> * 保存年，月，日，时，分，秒，微秒，时区，占12字节
>>> * 关键字：timestamp（n）with time zone
>>> * 如：2019-08-22 17：41：30.135428 +08：00
>> timestamp(n) with local time zone
>>> * 不保存时区，存储时转换为数据库时区的timestamp，占8字节
>>> * 关键字：timestamp（n）with local time zone
>>> * 如：存储时：2019-08-22 17：41：30.135428   查看时：2019-08-22 17：41：30.135428 +08：00
### 2.3非常用的数据类型
* 二进制类型
![image](https://github.com/mhqdyt/java-study/blob/master/images/Dadabase-5/5-1.png)
* 布尔类型
![image](https://github.com/mhqdyt/java-study/blob/master/images/Dadabase-5/5-2.png)
* 时间间隔类型
![image](https://github.com/mhqdyt/java-study/blob/master/images/Dadabase-5/5-3.png)
### 2.4数据类型案例介绍
* 创建表
```
SQL> create table T_STUDENT(
student_id number(10),
student_name varchar(100),
student_grade int,
student_is_excellent boolean,
student_date date
);
```
* 添加列
```
SQL> alter table T_STUDENT add student_description clob;
```
* 修改列的数据类型
```
SQL>alter table T_STUDENT modify student_grade double;
```
## 3.系统函数
> * 系统函数是对一些业务逻辑的封装，以完成特定的功能。系统函数可以有参数，也可以没有参数，系统函数执行完成后会返回执行结果
> * 系统函数的分类
>> * 数值计算函数
>> * 字符处理函数
>> * 时间日期函数
>> * 间隔函数
>> * 类型转换函数
### 3.1数值计算函数
![image](https://github.com/mhqdyt/java-study/blob/master/images/Dadabase-5/5-4.png)
![image](https://github.com/mhqdyt/java-study/blob/master/images/Dadabase-5/5-5.png)
![image](https://github.com/mhqdyt/java-study/blob/master/images/Dadabase-5/5-6.png)
### 3.2字符处理函数
![image](https://github.com/mhqdyt/java-study/blob/master/images/Dadabase-5/5-7.png)
![image](https://github.com/mhqdyt/java-study/blob/master/images/Dadabase-5/5-8.png)
![image](https://github.com/mhqdyt/java-study/blob/master/images/Dadabase-5/5-9.png)
### 3.3时间日期函数
![image](https://github.com/mhqdyt/java-study/blob/master/images/Dadabase-5/5-10.png)
![image](https://github.com/mhqdyt/java-study/blob/master/images/Dadabase-5/5-11.png)
### 3.4间隔函数
![image](https://github.com/mhqdyt/java-study/blob/master/images/Dadabase-5/5-12.png)
### 3.5类型转换函数
![image](https://github.com/mhqdyt/java-study/blob/master/images/Dadabase-5/5-13.png)
![image](https://github.com/mhqdyt/java-study/blob/master/images/Dadabase-5/5-14.png)
![image](https://github.com/mhqdyt/java-study/blob/master/images/Dadabase-5/5-15.png)

