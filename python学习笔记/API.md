#API
----
##Python DB API的模块属性   

apilevel 使用的Python DB API版本

threadsafety 模块的线程安全程度如何

paramstyle 在SQL查询中使用哪种参数风格

-----

##Python DB API指定的异常
异常  
超类  
描述

StandardError  
所有异常的超类

Warning  
StandardError  
发生非致命问题时引发

Error  
StandardError  
所有错误条件的超类

InterfaceError 
Error  
与接口（而不是数据库）相关的错误

DatabaseError  
Error  
与数据库相关的错误的超类

DataError  
DatabaseError  
与数据相关的问题，如值不在合法的范围内

OperationalError  
DatabaseError  
数据库操作内部的错误

IntegrityError  
DatabaseError  
关系完整性遭到破坏，如键未通过检查

InternalError  
DatabaseError  
数据库内部的错误，如游标无效

ProgrammingError  
DatabaseError   
用户编程错误，如未找到数据库表

NotSupportedError  
DatabaseError  
请求不支持的功能，如回滚


------

##函数commect的常用参数
dsn 数据源名称，具体含义随数据库而异 不可选

user 用户名 可选

password 用户密码 可选

host 主机名 可选

database 数据库名称 可选

-----
##连接对象的方法
1. close() 关闭连接对象。之后，连接对象及其游标将不可用

2. commit() 提交未提交的事务——如果支持的话；否则什么都不做

3. rollback() 回滚未提交的事务（可能不可用）

4. cursor() 返回连接的游标对象

 1. 方法rollback可能不可用，因为并非所有的数据库都支持事务（事务其实就是一系列操作）。
可用时，这个方法撤销所有未提交的事务。
 2. 方法commit总是可用的，但如果数据库不支持事务，这个方法就什么都不做。关闭连接时，
如果还有未提交的事务，将隐式地回滚它们——但仅当数据库支持回滚时才如此！如果你不想依
赖于这一点，应在关闭连接前提交。只要提交了所有的事务，就无需操心关闭连接的事情，因为
作为垃圾被收集时，连接会自动关闭。然而，为安全起见，还是调用close吧，因为这样做不需
要长时间敲击键盘。
 3. 说到方法cursor，就必须说说另一个主题：游标对象。你使用游标来执行SQL查询和查看结
果。游标支持的方法比连接多，在程序中的地位也可能重要得多。

----
##游标对象的方法
1. callproc(name[, params]) 使用指定的参数调用指定的数据库过程（可选）
2. close() 关闭游标。关闭后游标不可用
3. execute(oper[, params]) 执行一个SQL操作——可能指定参数
4. executemany(oper, pseq) 执行指定的SQL操作多次，每次都序列中的一组参数
5. fetchone() 以序列的方式取回查询结果中的下一行；如果没有更多的行，就返回None
6. fetchmany([size]) 取回查询结果中的多行，其中参数size的值默认为arraysize
7. fetchall() 以序列的序列的方式取回余下的所有行
8. nextset() 跳到下一个结果集，这个方法是可选的
9. setinputsizes(sizes) 用于为参数预定义内存区域
10. setoutputsize(size[, col]) 为取回大量数据而设置缓冲区长度

----
##游标对象的属性
description 由结果列描述组成的序列（只读）

rowcount 结果包含的行数（只读）

arraysize fetchmany返回的行数，默认为1 

##DB API构造函数和特殊值


1. Date(year, month, day) 创建包含日期值的对象



1. Time(hour, minute, second) 创建包含时间值的对象


1. Timestamp(y, mon, d, h, min, s) 创建包含时间戳的对象


1. DateFromTicks(ticks) 根据从新纪元开始过去的秒数创建包含日期值的对象


1. TimeFromTicks(ticks) 根据从新纪元开始过去的秒数创建包

1. 含时间值的对象

1. imestampFromTicks(ticks) 根据从新纪元开始过去的秒数创建包含时间戳的对象

1. Binary(string) 创建包含二进制字符串值的对象

1. STRING 描述基于字符串的列（如CHAR）

1. BINARY 描述二进制列（如LONG或RAW）

1. NUMBER 描述数字列

1. DATETIME 描述日期/时间列

1. ROWID 描述行ID列