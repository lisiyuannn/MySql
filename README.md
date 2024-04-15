# MySql
数据库学习
# 基础shell命令 
* 安装 apt install mysql-server 
* 查看运行状态 systemctl status mysql 
* 启动mysql服务 systemctl start mysql 
* mysql配置文件路径 cd /etc/mysql/debian.cnf 
* 链接mysql服务 mysql -u 用户名 -p  
root用户没有密码，直接 mysql -u root
* 导出数据库 mysqldump -u username -p database_name > /path/name.sql
* 导入数据库 mysql -u username -p database_name < name.sql
----------------------------- 
# DDL数据定义语言
## 数据库操作
* 查询所有数据库
    ```sql
    SHOW DATABASES;
    ```
* 查看当前数据库 
    ```sql
    SELECT DATABASE();
    ```
* 创建新的数据库 
    ```sql
    CREATE DATABASE [IF NOT EXISTS] 数据库名 [DEFAULT CHARSET 字符集] [COLLATE 排序规则];
    ```
* 删除数据库 
    ```sql
    DROP DATABASE [IF EXISTS] 数据库名;
    ```
* 选择要使用的数据库
    ```sql
    USE 数据库名;
    ```
## 表的操作
* 查询数据库中所有表
    ```sql
    SHOW TABLES;
    ``` 
* 查看表的结构
    ```sql
    DESC 表名;
    ```
* 查询指定表的建表语句
    ```sql
    SHOW CREATE TABLE 表名;
    ```
* 创建表
   ```sql
    CREATE TABLE 表名(
        字段1 字段1类型 [COMMENT 字段1注释],
        字段2 字段2类型 [COMMENT 字段2注释],
        ...
        字段n 字段n类型 [COMMENT 字段n注释],
    )[COMMENT 表注释];
    ```
* 删除表
    ```sql
    DROP TABLE [IF EXISTS] 表名;
    TRUNCATE TABLE 表名;
    //TRUNCATE 会将表删除，然后再重新创建一张一样的
    ```

## 修改表
* 添加新的字段
    ```sql
    ALTER TABLE 表名 add 字段名 类型(长度) [COMMENT注释] [约束];
    ```
* 修改字段数据类型
    ```sql
    ALTER TABEL 表名 MODIFY 字段名 新数据类型(长度);
    ```
* 修改字段名何其数据类型
    ```sql
    ALTER TABEL 表名 CHANGE 旧字段名 新字段名 新数据类型(长度) [COMMENT注释] [约束];
    ```
* 删除字段
    ```sql
    ALTER TABEL 表名 DROP 字段名;
    ```
* 修改表名
    ```sql
    ALTER TABEL 表名 RENAME TO 新表名;
    ```
* 修改字段默认值
    ```sql
    alter table table_name modify field_name data_type default value1;
    alter table tabel_name alter column field_name set default value1;
    ```
* 重命名字段
    ```sql
    alter table table_name rename column field_name to new_name;
    ```

## 数据类型
|类型|大小|范围|无符号范围|
|:----:|:----:|:----:|:----:|
| TINYINT|1 byte |(-128, 127)|(0, 255)|
| SMALLINT|2 bytes |(-32,768, 32,767)|(0, 65,535)|
| MEDIUMINT|3 bytes |(-8,388,608, 8,388,607)|(0, 16,777,215)|
| INT / INTEGER|4 bytes |(-2,147,483,648, 2,147,483,647)|(0, 4,294,967,295)|
| BIGINT|8 bytes |(-9,223,372,036,854,775,808, 9,223,372,036,854,775,807)|(0, 18,446,744,073,709,551,615)|
| DECIMAL|可变 |依赖于指定的精度和小数位数|依赖于指定的精度和小数位数|
| FLOAT|4 bytes |(1.175494351e-38, 3.402823466e+38)|(0, 3.402823466e+38)|
| DOUBLE|8 bytes |(2.2250738585072014e-308, 1.7976931348623158e+308)|(0, 1.7976931348623158e+308)|

|类型|大小|描述|
|:----:|:----:|:----:|
| char(n) |n bytes |固定长度字符串，最多包含 n 个字符，性能好|
| varchar(n) |1 byte + 实际存储的字符数 |可变长度字符串，最多包含 n 个字符| 

|类型|大小|范围|格式|描述|
|:----:|:----:|:----:|:----:|:----:|
| DATE |3 bytes |1000-01-01 到 9999-12-31|YYYY-MM-DD|日期，格式为年-月-日|
| TIME |3 bytes |'-838:59:59' 到 '838:59:59'|HH:MM:SS|时间，格式为时:分:秒|
| DATETIME |8 bytes |1000-01-01 00:00:00 到 9999-12-31 23:59:59|YYYY-MM-DD HH:MM:SS|日期和时间，格式为年-月-日 时:分:秒|
| TIMESTAMP |4 bytes |1970-01-01 00:00:01 UTC 到 2038-01-19 03:14:07 UTC|YYYY-MM-DD HH:MM:SS|时间戳，格式为年-月-日 时:分:秒|
| YEAR |1 byte |1901 到 2155|YYYY|年份，格式为年份（四位数）|

----------------------------- 

# DML 数据操作语言

## 添加数据 (INSERT)
* 给指定的字段添加数据
    ```sql
    INSERT INTO 表名 (字段名1, 字段名2，...) VALUES (值1，值2，...);
    ```
* 给全部字段添加数据
    ```sql
    INSERT INTO 表名 VALUES (值1，值2，...);
    ```
* 批量添加数据
    ```sql
    INSERT INTO 表名 (字段名1, 字段名2，...) VALUES (值1，值2，...), (值1，值2，...), ...;
    INSERT INTO 表名 VALUES (值1，值2，...), (值1，值2，...), ...;
    ```
## 修改数据 (UPDATE)
* 修改某条记录中某字段的值
    ```sql
    UPDATE 表名 SET 字段名1 = 值1, 字段名2 = 值2, ...[WHERE 条件];
    ```
## 删除数据 (DELETE)
* 删除表中的记录
    ```sql
    DELETE FROM 表名 [WHERE 条件];
    ```
------------------------------

# DQL 数据查询语言

* DQL 语法
    ```sql
    SELECT 字段列表
    FROM 表名列表
    WHERE 条件列表
    GROUP BY 分组字段列表
    HAVING 分组后条件列表
    ORDER BY 排序字段列表
    LIMIT 分页参数;
    ```

## 基础查询
* 查询多个字段
    ```sql
    SELECT 字段1, ... FROM 表名;
    SELECT * FROM 表名;
    ```
* 设置别名
    ```sql
    SELECT 字段1 [AS 别名1], ... FROM 表名;
    ```
* 去除重复记录
    ```sql
    SELECT DISTINCT 字段列表 FROM 表名;
    ```
## 条件查询
* 语法
    ```sql
    SELECT 字段列表 FROM 表名 WHERE 条件列表;
    ```
* 条件列表

| 条件运算符       | 功能                     |
|--------------|--------------------------|
| `=`          | 检查两个值是否相等       |
| `<>` 或 `!=` | 检查两个值是否不相等     |
| `>`          | 检查一个值是否大于另一个值 |
| `<`          | 检查一个值是否小于另一个值 |
| `>=`         | 检查一个值是否大于或等于另一个值 |
| `<=`         | 检查一个值是否小于或等于另一个值 |
| `BETWEEN`...`AND`    | 检查一个值是否介于两个给定值之间 |
| `IN()`         | 检查一个值是否在给定的一组值之中 |
| `LIKE`       | 在模式匹配时比较值 ，'_' 和 '%'，       |
| `IS NULL`  | 是NULL |

| 逻辑运算符 | 功能                              |
|--------|-----------------------------------|
| `AND`  | 组合两个或多个条件，如果所有条件都为真，则整个条件为真 |
| `OR`   | 组合两个或多个条件，如果任何一个条件为真，则整个条件为真 |
| `NOT`  | 对给定条件的结果进行取反          |

## 聚合函数

| 函数          | 功能                                            |
|---------------|-------------------------------------------------|
| `COUNT()`     | 计算指定列中的行数（不包括NULL值）                |
| `SUM()`       | 计算指定列中所有数值的总和（忽略NULL值）            |
| `AVG()`       | 计算指定列中所有数值的平均值（忽略NULL值）           |
| `MIN()`       | 找出指定列中的最小值（忽略NULL值）                 |
| `MAX()`       | 找出指定列中的最大值（忽略NULL值）                 |

## 分组查询
* 语法
    ```sql
    SELECT 字段列表 FROM 表名 [WHERE 条件列表]
    GROUP BY 分组字段名 [HAVING 分组后过滤条件];
    //WHERE是在分组前进行过滤，HAVING是在分组后进行过滤
    //WHERE不能对聚合函数进行判断，HAVING可以
    //执行顺序：WHERE > 聚合函数 > HAVING
    ```
## 排序查询
* 语法
    ```sql
    SELECT 字段列表 FROM 表名 ORDER BY 字段1 排序方式1 [ASC], 字段2 排序方式2 [DESC];
    //ASC默认升序，DESC可以指定降序
    ```
## 分页查询
* 语法
    ```sql
    SELECT 字段列表 FROM 表名 LIMIT 起始索引,查询记录数;
    //起始索引从0开始，起始索引 = （查询页码-1）*每页记录数
    //如果查询第一页数据，起始索引可以省略，LIMIT 10
    ```
## DQL语句案例
* 查询年龄为20，21，22，23岁的女性员工信息
    ```sql
    SELECT * FROM emp WHERE sex = '女' AND age in (20, 21, 22, 23);
    SELECT * FROM emp WHERE sex = '女' AND age (BETWEEN 20 AND 23);
    SELECT * FROM emp WHERE sex = '女' AND (age >= 20 AND age <= 23);
    ```
* 查询性别为 男，并且年龄再 20-40岁之间的姓名为3个字的员工
    ```sql
    SELECT * FROM emp WHERE sex = '男' AND (age BETWEEN 20 AND 40) AND NAME LIKE '___';
    ```
* 统计员工表中，年龄小于60岁，男性和女性员工的人数
    ```sql
    SELECT sex, count(sex) FROM emp WHERE age < 60 GROUP BY sex;
    ```
* 查询所有年龄小于等于35岁员工的姓名和年龄，并对查询结果按年龄升序排序，如果年龄相同，按照入职时间降序排序
    ```sql
    SELECT name, age FORM emp WHERE age < 35 ORDER BY age, login_date DESC
    ```
* 查询性别为男，且年龄在20-40岁之间的前五个员工信息，对查询结果按年龄升序排序，年龄相同按入职时间升序排序
    ```sql
    SELECT * FROM emp WHERE sex = '男' AND (age BETWEEN 20 AND 40) ORDER BY age, login_date DESC LIMIT 5;
    //先排序，再取前五
    SELECT * 
    FROM (
    SELECT * 
    FROM emp 
    WHERE sex = '男' AND (age BETWEEN 20 AND 40) 
    LIMIT 5
    ) AS subquery
    ORDER BY age, login_date DESC;
    //先取前五，再排序
    ```
## DQL的执行顺序
* DQL执行顺序
    ```sql
    FROM 表名列表
    WHERE 条件列表
    GROUP BY 分组字段列表
    HAVING 分组后条件列表
    SELECT 字段列表
    ORDER BY 排序字段列表
    LIMIT 分页参数;
    ```
--------------------------

# DCL数据控制语言

## 管理用户
* 查询用户
    ```SQL
    USE mysql;
    SELECT * FROM userl
    ```
* 创建用户
    ```SQL
    CREATE USER '用户名'@'主机名' IDENTIFIED BY '密码';
    ```
* 修改用户密码
    ```SQL
    ALTER USER '用户名'@'主机名' IDENTIFIED WITH mysql_native_password BY '新密码';
    ```
* 删除用户
    ```SQL
    DROP USER '用户名'@'主机名';
    ```
## 权限控制

* 查询用户权限
    ```SQL
    SHOW GRANTS FOR '用户名'@'主机名';
    ```
* 授予用户权限
    ```SQL
    GRANT 权限列表 ON 数据库名.表名 TO '用户名'@'主机名';
    //多个权限之间使用逗号分隔
    //授权时，数据库名和表名可以使用 * 进行通配，代表所有
    ```
* 撤销用户权限
    ```SQL
    REVOKE 权限列表 ON 数据库名.表名 FROM '用户名'@'主机名';
    ```

-------------------------------
# 常用语句
* 逻辑运算符 优先级：not>and>or
* 等级大于1小于5，经验大于1小于5
    ```sql
    select * from player where level > 1 and level < 5 or exp > 1 and exp < 5;
    ```
* 使用括号可以改变优先级
    ```sql
    select * from player where level > 1 and (level < 5 or exp > 1) and exp < 5;
    ```
* 查找指定条件 in
    ```sql
    select * from player where level in (1, 3, 5);
    select * from player where level between 1 and 10;  //包含1和10
    ```
* 模糊查询 '%'表示任意字符，'_'表示任意一个字符
    ```sql
    select * from player where name like '王%'; //查找姓王的玩家
    ```
* 匹配正则表达式  关键字 regexp
  '.' 表示任意一个字符
  '^' 开始开头
  '$' 表示结尾
  [abc] 其中任意一个字符
  [a-z] a-z范围内任意一个字符
  A|B A或者B
    ```sql
    select * from player where name regexp '^王.$';
    //查找name中以王开头，并且只有两个子的记录
    select * from player where name regexp '王';
    //查找name中包含 王 字的记录
    select * from player where name regexp '[王张]';
    //查找name中包含 王 或者 张 字的记录
    ```
* 查找某个字段为空的记录 不可以使用等号进行判断
    ~~where email = null~~
    ```sql
    select * from player where email is null;
    //未填写邮箱
    select * from player where email is not null;
    //填写了邮箱
    select * from player where email is null or email = '';
    //为空或者为空字符串
    /*
    +------+-----------+------+-------+-------+------+-------+
    | id   | name      | sex  | email | level | exp  | gold  |
    +------+-----------+------+-------+-------+------+-------+
    |   12 | 吕子乔    | 男   | NULL  |    36 |  100 | 46.00 |
    |   13 | 吕小布    | 男   | NULL  |    81 |   88 | 25.00 |
    |  190 | 吕布      | 男   |       |    77 |   43 | 31.00 |
    +------+-----------+------+-------+-------+------+-------+
    */
    ```

## 子查询，将一个查询的结果作为另一个查询的条件
* 子查询也可以用作 create insert 等关键字
* 查询等级大于平均等级的记录
    ```sql
    select avg(level) from player;
    select * from player where level > (select avg(level) from player); 
    ```
* 查询每条记录中的level与平均level的差值
    ```sql
    select id, name, round((select avg(level) from player)), level - round((select avg(level) from player)) from player;
    //注意子查询必须先用括号括起来 round(select avg(level) from player) 是错误的
    ```
* 判断是否存在使用 exists 关键字，返回 0 或 1
    ```sql
    select exists (select * from player where level > 100);
    ```
---------------------------------
# 函数
## 字符串函数

| 函数名                           | 功能描述                                       |
|----------------------------------|------------------------------------------------|
| `CONCAT(string1, string2, ...)` | 将多个字符串连接成一个字符串。                 |
| `SUBSTRING(string, start, length)` | 从指定位置开始截取指定长度的子字符串。        |
| `LEFT(string, length)`           | 从字符串的左边开始截取指定长度的子字符串。     |
| `RIGHT(string, length)`          | 从字符串的右边开始截取指定长度的子字符串。     |
| `LENGTH(string)`                 | 返回字符串的长度。                             |
| `UPPER(string)`                  | 将字符串转换为大写字母形式。                   |
| `LOWER(string)`                  | 将字符串转换为小写字母形式。                   |
| `TRIM(string)`                   | 移除字符串两端的空格。               |
| `REPLACE(string, old, new)`      | 将字符串中的指定子字符串替换为新的子字符串。   |
| `CHAR_LENGTH(string)`            | 返回字符串的字符数。                           |
| `POSITION(substring IN string)`  | 返回子字符串在字符串中的起始位置。             |
| `REVERSE(string)`                | 反转字符串中的字符顺序。                       |
| `LPAD(string, n, str)`                | 在字符串左侧填充，填充至长度为 n。                       |
| `RPAD(string n, str)`                |  在字符串右侧填充，填充至长度为 n。                      |

## 数值函数

| 函数名                  | 功能描述                                       |
|-------------------------|------------------------------------------------|
| `ABS(number)`           | 返回数值的绝对值。                             |
| `ROUND(number, decimal)`| 将数值四舍五入到指定的小数位数。               |
| `CEIL(number)`       | 向上取整。               |
| `FLOOR(number)`         | 向下取整。               |
| `SQRT(number)`          | 返回数值的平方根。                             |
| `POWER(number, exponent)`| 返回给定数值的指定指数幂。                    |
| `LOG(number)`           | 返回给定数值的自然对数。                       |
| `EXP(number)`           | 返回自然常数e的给定次幂。                      |
| `MOD(dividend, divisor)`| 返回两个数相除的余数。                         |
| `SIGN(number)`          | 返回数值的符号：1（正数）、0（零）、-1（负数）。|
| `RAND()`          | 返回0-1之间的随机数。|

## 日期函数

### SQL 日期函数表

| 函数名                      | 功能描述                                       |
|-----------------------------|------------------------------------------------|
| `CURRENT_DATE()`            | 返回当前日期。                                 |
| `CURRENT_TIME()`            | 返回当前时间。                                 |
| `CURRENT_NOW()`       | 返回当前日期和时间。                           |
| `DATE_ADD(date, INTERVAL)`  | 将指定的时间间隔加到日期上。                   |
| `DATE_SUB(date, INTERVAL)`  | 从日期中减去指定的时间间隔。                   |
| `DATEDIFF(date1, date2)`    | 返回两个日期之间的天数差。                     |
| `DATE_FORMAT(date, format)` | 将日期格式化为指定的格式。                     |
| `EXTRACT(unit FROM date)`   | 从日期中提取指定的单位（如年、月、日等）。     |
| `YEAR(date)`                | 返回日期的年份。                               |
| `MONTH(date)`               | 返回日期的月份。                               |
| `DAY(date)`                 | 返回日期的天数。                               |
| `WEEKDAY(date)`             | 返回日期是一周中的第几天（0表示星期一，1表示星期二，以此类推）。|
| `HOUR(time)`                | 返回时间的小时部分。                           |
| `MINUTE(time)`              | 返回时间的分钟部分。                           |
| `SECOND(time)`              | 返回时间的秒钟部分。                           |


## 流程函数

| 函数名                              | 基本格式                                     | 功能描述                                             |
|-------------------------------------|----------------------------------------------|------------------------------------------------------|
| `IF(condition, value_if_true, value_if_false)` | `IF(condition, value_if_true, value_if_false)` | 如果条件成立，则返回value_if_true，否则返回value_if_false。 |
| `CASE`                              | ```sql CASE expression WHEN value1 THEN result1 WHEN value2 THEN result2 ... ELSE default_result END ``` | 根据条件表达式进行多条件判断，返回对应的结果。如果没有满足条件的结果，则返回默认结果。 |
| `COALESCE(value1, value2, ...)`     | `COALESCE(value1, value2, ...)`             | 返回参数列表中的第一个非NULL值。                        |
| `NULLIF(value1, value2)`            | `NULLIF(value1, value2)`                    | 如果value1等于value2，则返回NULL，否则返回value1。       |

* __示例__
* 使用IF函数
    ```sql
    SELECT name, 
        IF(age >= 18, '成年人', '未成年人') AS age_group
    FROM users;
    ```
* 使用CASE函数
    ```sql
    SELECT name,
       CASE 
           WHEN age >= 18 THEN '成年人'
           ELSE '未成年人'
       END AS age_group
    FROM users;
    ```

* 使用COALESCE函数
    ```sql
    SELECT name,
        COALESCE(phone_number, '暂无联系方式') AS contact
    FROM users;
    ```
* 使用NULLIF函数
    ```sql
    SELECT name,
        NULLIF(email, 'noemail@example.com') AS email
    FROM users;
    ```

# 约束

## 分类

| 约束       | 描述                                         | 关键字       |
|------------|----------------------------------------------|--------------|
| PRIMARY KEY | 主键约束，用于唯一标识表中的每一行数据。       | PRIMARY KEY |
| UNIQUE     | 唯一约束，确保列中的所有值都是唯一的。         | UNIQUE       |
| NOT NULL   | 非空约束，确保列中的值不为空。                | NOT NULL     |
| CHECK      | 检查约束，用于确保列中的值满足特定条件。       | CHECK        |
| DEFAULT    | 默认约束，用于在未提供值时为列设置默认值。      | DEFAULT      |
| FOREIGN KEY| 外键约束，用于在一个表中创建对另一个表中的外键引用。 | FOREIGN KEY  |

## 约束创建
* 在创建表时指定字段的约束
    ```sql
    CREATE TABLE user(
        id INT PRIMARY KEY AUTO_INCREMENT COMMENT '自增主键',
        name VARCHAR(10) NOT NULL UNIQUE COMMENT '非空唯一',
        age INT CHECK (age > 0 and age < =120>) COMMENT '检查约束',
        status CHAR(1) DEFAULT '1' COMMENT '默认为1',
        gender CHAR(1) CHECK (gender in ('男', '女'))
    ) COMMENT '用户表';
    ```
## 外键约束
* 指定外键
    ```sql
    CREATE TABLE 表名(
        字段名 数据类型
        ...
        [CONSTRAINT] [外键名称] FOREIGN KEY (外键字段名) REFERENCES 外表 (外表主键));
    ```
* 添加外键
    ```sql
    ALTER TABLE 表名 ADD CONSTRAINT FK_表名_外键字段名 FOREIGN KEY (外键字段名) REFERENCES 表名(表主键);
    ```
* 删除更新行为
    ```sql
    ALTER TABLE 表名 ADD CONSTRAINT FK_表名_外键字段名 FOREIGN KEY (外键字段名) REFERENCES 表名(表主键); NO UPDATE CASCADE ON DELETE CASCADE;
    //更新时子表也更新，删除时子表也删除
    ALTER TABLE 表名 ADD CONSTRAINT FK_表名_外键字段名 FOREIGN KEY (外键字段名) REFERENCES 表名(表主键); NO UPDATE SET NULL ON DELETE SET NULL;
    //更新时子表置为NULL，删除时子表也置为NULL
    ```

# 多表查询

## 多表关系
* 一对多（多对一）：在多的一方建立外键，指向一的主键
* 多对多：建立第三章中间表，中间表至少包含两个外键，分别关联两方主键
* 一对一：多用于单表拆分，将一张表的基础字段放在一张表中，将其他详情信息放在另一张表中，可以提升操作效率，在任意一方加入外键，关联另一方的主键，并且设置唯一约束（UNIQUE）

## 多表查询

* emp
    | id | name | age | job |salary| entrydate | managerid |dept_id|
    |----|----|----|----|----|----|----|----|

* dept
    | id | name |
    |----|----|

* 基础语法
    ```sql
    SELECT 字段列表 FROM 表1, 表2, ... WHERE 约束条件;
    //不加约束条件会产生笛卡尔积
    ```
### 连接查询

* 分类
    >使用表的主键和外键进行关联
    >内连接只返回两个表中都有的数据
    >左（右）连接返回左（右）表中的所有数据和右（左）表中匹配的数据，没有用null填充
    >自连接，当前表与自身的连接查询，自连接必须使用表别名
    >关键字 inner join,  left join,  right join 
1. 内连接查询
* 隐式内连接语法
    ```sql
    SELECT 字段列表 FROM 表1, 表2 WHERE 条件;
    ```
* 显式内连接
    ```sql
    SELECT 字段列表 FROM 表1 [INNER] JOIN 表2 ON 连接条件;
    ```
* 查询每一个员工的姓名，关联的部门名称（隐式内连接实现）
    ```sql
    SELECT emp.name, dept.name FROM emp, dept WHERE dept.id = emp.dept_id;
    ```
* 查询每一个员工的姓名，关联的部门名称（显式内连接实现）
    ```sql
    SELECT emp.name, dept.name FROM emp INNER JOIN dept ON dept.id = emp.dept_id;
    ```
2. 左外连接查询
* 查询emp表中所有数据，和对应的部门信息（左外连接）
    ```sql
    SELECT emp.*, dept.name FROM emp LEFT JOIN dept ON dept.id = emp.dept_id;
    ```
3. 右外连接查询
* 查询dept表中所有数据，和对应的员工信息（左外连接）
    ```sql
    SELECT dept.*, emp.name  FROM emp RIGHt JOIN dept ON dept.id = emp.dept_id;
    ```
4. 自连接
* 语法
    ```sql
    //必须对表起别名
    SELECT 字段列表 FROM 表1 AS A, 表1 AS B WHERE 条件;
    //内连接隐式
    SELECT 字段列表 FROM 表1 AS A INNER JOIN 表1 AS B ON 条件;
    //内连接显式
    SELECT 字段列表 FROM 表1 AS A LEFT JOIN 表1 AS B ON 条件;
    //左外连接
    ```
* 查询员工及其所属领导的名字
    ```sql
    // id, name, age, job, managerid
    SELECT A.name AS '员工', B.name AS '领导' FROM emp AS A, emp AS B WHERE A.managerid = B.id;
    //隐式连接内写法，显示的需要加上INNER JOIN ON 关键字
    ```
 * 查询 __所有__ 员工及其所属领导的名字，可使用外连接
    ```sql
    // id, name, age, job, managerid
    SELECT A.name AS '员工', B.name AS '领导' FROM emp AS A LEFT JOIN emp AS B ON A.managerid = B.id;
    ```

### 联合查询

* 将多次查询的结果合并起来，形成一个新的查询结果集
* 语法
    ```sql
    SELECT 字段列表 FROM 表1 ...
    UNION [ALL]
    SELECT 字段列表 FROM 表2 ...;
   ```
* 查询薪资低于5000的员工，和年龄大于50岁的员工
    ```sql
    SELECT * FROM emp WHERE salary < 5000
    UNION ALL
    SELECT * FROM emp WHERE age > 50;
    //删除 ALL 关键字后可以对结果进行去重
    //2个查询字段列表必须保持一致
    ```   
* 合并查询结果，将两条查询结果使用union连接起来
    ```sql
    select * from player where level between 1 and 10
    union
    select * from player exp where exp between 1 and 10;
    //union 会默认去除重复的记录，使用union all会输出重复的记录
    ```
* 输出查询结果的交集  关键字 intersect，与union使用方法类似
    ```sql
    select * from player where level between 1 and 10
    intersect
    select * from player exp where exp between 1 and 10;
    ```
* 输出查询结果的差集  关键字 except，与union使用方法类似
    ```sql
    select * from player where level between 1 and 10
    except
    select * from player exp where exp between 1 and 10;
    ```

### 子查询

* SQL语句中嵌套SELECT语句，成为嵌套查询，又称子查询
* 语法
    ```sql
    SELECT * FROM t1 WHERE column1 = (SELECT column1 FROM t1);
    //子查询外部的语句可以是 INSERT/UPDATE/DELETE/SELECT 中任意一个
    ```
* 根据子查询结果不同，可分为：
    >标量子查询（子查询结果为单个值）
    >列子查询（子查询结果为一列）
    >行子查询（子查询结果为一行）
    >表子查询（子查询结果为多行多列）
* 根据查询位置分为：
    >WHERE 之后
    >FROM 之后
    >SELECT 之后
 1. 标量子查询，常用于比较运算，= != > >= < <= 

* 查询销售部所有员工信息，员工表中没有部门字段，只有部门编号
    ```sql
    //先查出销售部部门编号
    SELECT id FROM dept WHERE NAME = '销售部';
    //根据销售部部门 id 查询员工信息
    SELECT * FROM emp WHERE dept_id = (SELECT id FROM dept WHERE NAME = '销售部');
    ```
* 查询'方东白'入职之后的员工信息
    ```sql
    //先找出"方东白"的入职时间
    SELECT entrydate FROM emp WHERE name = '方东白';
    //根据其入职时间查找之后入职的员工信息
    SELECT * FROM emp WHERE entrydate > (SELECT entrydate FROM emp WHERE name = '方东白');
    ```

2. 列子查询，常用操作符：IN, NOT IN, ANY, SOME, ALL

    > IN   在指定集合范围内多选一
    > NOT IN   不在指定的集合范围内
    > ANY  子查询返回列表中，有任意一个满足即可
    > SOME  与ANY相同
    > ALL  子查询返回列表中的所有值都必须满足
* 查询 销售部 和 市场部 的所有员工信息
    ```sql
    //查询 销售部 和 市场部 的部门id
    SELECT id FROM dept WHERE name = '销售部' OR name = '市场部';
    //根据部门信息id查询员工信息
    SELECT * FROM emp WHERE dept_id in (SELECT id FROM dept WHERE name = '销售部' OR name = '市场部');
    ```
* 查询比财务部所有人工资都高的员工信息
    ```sql
    //先获取财务部部门id
    SELECT id FROM dept WHERE name = '财务部';
    //先查询财务部所有人的工资
    SELECT salary FROM emp WHERE dept_id = (SELECT id FROM dept WHERE name = '财务部');
    //查询比他们工资都高的员工信息
    SELECT * FROM emp WHERE salary > ALL (SELECT salary FROM emp WHERE dept_id = (SELECT id FROM dept WHERE name = '财务部'));
    ```
* 查询比研发部其中任意一人工资高的员工信息
    ```sql
    SELECT id FROM dept WHERE name = '研发部';
    SELECT salary FROM emp WHERE dept_id = (SELECT id FROM dept WHERE name = '研发部');
    SELECT * FROM emp WHERE salary > ANY (SELECT salary FROM emp WHERE dept_id = (SELECT id FROM dept WHERE name = '研发部'));
    ```

3. 行子查询 常用操作符 =, != IN, NOT IN
* 查询与"张无忌"的薪资及直属领导相同的员工信息
    ```sql
    //查询张无忌的薪资和直属领导
    SELECT salary, managerid FROM emp WHERE name = '张无忌';
    //查询与"张无忌"的薪资及直属领导相同的员工信息
    SELECT * FROM emp WHERE (salary, managerid) = (SELECT salary, managerid FROM emp WHERE name = '张无忌');
    ```

4. 表子查询，常用 IN

* 查询与"路障客"，"宋远桥"的职位与薪资相同的员工信息
    ```sql
    //查询二者的职位与薪资
    SELECT job, salary FROM emp WHERE name = '路障客' OR name = '宋远桥';
    //查询与"路障客"，"宋远桥"的职位与薪资相同的员工信息
    SELECT * FROM emp WHERE (job, salary) IN (SELECT job, salary FROM emp WHERE name = '路障客' OR name = '宋远桥';);
    ```
* 查询入职日期式"2006-01-01"之后的员工信息，及其部门信息
    ```sql
    //查询日期之后的员工信息
    SELECT * FROM emp WHERE entrydate > '2006-01-01';
    //根据员工查询其部门信息
    SELECT e.*, dept.* FROM (SELECT * FROM emp WHERE entrydate > '2006-01-01') AS e LEFT JOIN dept ON e.dept_id = dept.id;
    ```

5. 多表查询案例

* emp
    | id | name | age | job |salary| entrydate | managerid |dept_id|
    |----|----|----|----|----|----|----|----|

* dept
    | id | name |
    |----|----|

* salgrade
    | grade | losal | hisal |
    |----|----|----|

* 查询员工姓名，年龄，职位，部门信息（隐式内连接）
    ```sql
    SELECT e.name, e.age, e.job, d.name FROM emp AS e, dept AS d WHERE e.dapt_id = d.id;
    ```
* 查询年龄小于30岁的员工姓名，年龄，职位，部门信息
    ```sql
    SELECT e.name, e.age, e.job, d.name FROM emp AS e INNER JOIN dept AS d ON e.dapt_id = d.id WHERE e.age < 30;
    //连接后再筛选
    SELECT e.name, e.age, e.job, d.name FROM emp AS e INNER JOIN dept AS d ON e.dapt_id = d.id AND e.age < 30;
    //连接时筛选
    ```
* 查询 __拥有__ 员工的部门ID、部门名称
    ```sql
    //查询员工表中部门id和部门表中部门id的交集，用内连接，然后去重
    SELECT DISTINCT d.id, d.name FROM emp AS e INNER JOIN dept AS d ON e.dapt_id = d.id;
    ```
* 查询所有年龄大于40岁的员工，及其归属的部门名称，如果员工没有分配部门，也需要展示出来
    ```sql
    SELECT e.*, d.name FROM emp AS e LEFT JOIN dept AS d ON e.dapt_id = d.id AND e.age > 40;
    ```
* 查询所有员工的工资等级
    ```sql
    //工资等级表和员工表的连接条件
    emp.salary >= salgrade.losal and emp.salary < salgrade.hisal
    SELECT e.name e.salary s.grade FROM emp e, salgrade s WHERE emp.salary >= salgrade.losal and emp.salary < salgrade.hisal;
    ```
* 查询研发部所有员工的信息及工资等级
    ```sql
    //研发部部门编号
    SELECT id FROM dept WHERE name = '研发部';
    //研发部员工信息
    SELECT * FROM emp WHERE dept_id = (SELECT id FROM dept WHERE name = '研发部');
    //研发部员工信息与薪资等级表内连接
    SELECT * FROM (SELECT * FROM emp WHERE dept_id = (SELECT id FROM dept WHERE name = '研发部')) AS e INNER JOIN salgrade AS s ON e.salary >= s.losal and e.salary < s.hisal;

    //或者使用三表连接
    SELECT *
    FROM emp e, salgrade s, dept d 
    WHERE e.salary >= s.losal AND e.salary < s.hisal AND e.dept_id = d.id AND d.name = '研发部';
    ```
* 查询研发部员工的平均工资
    ```sql
    SELECT AVG(e.salary) FROM emp AS e INNER JOIN dept AS d ON e.dapt_id = d.id AND d.name = '研发部';
    ```
* 查询工资比 灭绝 高的员工信息
    ```sql
    SELECT salary FROM emp WHERE name = '灭绝';
    SELECT * FROM emp WHERE salary > (SELECT salary FROM emp WHERE name = '灭绝');
    ```
* 查询比平均薪资高的员工信息
    ```sql
    SELECT AVG(salary) FROM emp;
    SELECT * FROM emp WHERE salary > (SELECT AVG(salary) FROM emp);
    ```
* 查询低于本部门平均工资的员工信息
    ```sql
    //查询各个部门的平均薪资
    SELECT avg(salary) FROM emp e1 where e1.dept_id = 1;
    SELECT avg(salary) FROM emp e1 where e1.dept_id = 2;
    //查询低于本部门平均工资的员工信息
    SELECT * FROM emp e2 WHERE e2.salary < (SELECT avg(salary) FROM emp e1 where e1.dept_id = e2.dept_id);
    ```
* 查询所有的部门信息，并统计部门的员工人数
    ```sql
    //部门信息查询
    SELECT d.id, d.name FROM dept d;
    //1号部门的员工人数
    SELECT COUNT(*) FROM emp e WHERE e.dept_id = 1;
    查询所有的部门信息，并统计部门的员工人数
    SELECT d.id, d.name, (SELECT COUNT(*) FROM emp e WHERE e.dept_id = d.id) '人数' FROM dept d;
    ```
* 查询所有学生的选课情况，展示出学生名称，学号，课程名称
    ```sql
    //表：student, course, student_course
    //连接条件：student.id = student_course.student_id, course.id = student_course.course_id
    SELECT s.name, s.no, c.name FROM student s, course c, student_course sc WHERE s.id = sc.student_id AND c.id = sc.coures_id;
    ```
* 
    ```sql
    
    ```
* 
    ```sql
    
    ```
* 
    ```sql
    
    ```

