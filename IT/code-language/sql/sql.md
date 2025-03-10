# SQL 基础

**SQL**（**S**tructured **Q**uery **L**anguage）即结构化查询语言，是用于与**关系型**数据库管理系统（RDBMS）交互的标准编程语言。

## 注释

- **语法**：单行注释 `--`；多行注释 `/* */`

	```sql
	SELECT * FROM users;  -- 这是一个单行注释
	
	/*
	这是一个多行注释
	它可以跨越多行
	并且会被 SQL 引擎忽略
	*/
	```

## 语法规范

- **大小写不敏感**：SQL 中的关键字（如 SELECT、FROM 等）通常不区分大小写，但都习惯大写；大部分数据库默认对字符串的大小写也不敏感。
- **缩进与空格**：虽然语法上没有严格要求，但合理使用缩进和空格可以提高 SQL 语句的可读性。
- **语句结束符**：以 `;` 作为 SQL 语句的结束标志，但有些系统也允许不写分号。
- **占位符**：由于习惯大写关键字，所以个人笔记占位符前缀加 `$`。
- **字符串**：字符串使用单引号 `'` 包围；双引号有其它用途，各个语言不一样。

## 关键字

- **`*`**：表示所有。
	- `SELECT * FROM tb_test;`：查看 `tb_test` 数据表中所有 ROW。
- **`WHERE`**：`$COMMAND WHERE $CONDITION;`，用于添加查询条件。
	- `DELETE FROM tb_test WHERE id=1;`：从 `tb_test` 数据表中删除 `id=1` 的 ROW。

## SQL 标准和数据库实现

虽然 SQL 是一个标准语言，但不同的数据库管理系统在 SQL 语言的实现上会有一些差异。常见的差异包括：

- **数据类型**：不同数据库使用不同的命名和支持的类型。
- **SQL 方言**：某些 SQL 语法可能只在特定的数据库中有效。
- **扩展功能**：如特定的函数、存储过程、触发器等。

## 多行输入

- **Linux**：未完成行的行尾使用反斜杠 `\` 作为续行符。

	```sql
	SELECT * \
	FROM users \
	WHERE age > 20;
	```

- **Windows**：可以使用 Linux 的方法，但更好的做法是直接按回车键进行换行输入，最后以分号 `;` 结尾就行。

	```sql
	SELECT *
	FROM users
	WHERE age > 20;
	```

# Database 数据库

- **基础命令**

	```sql
	-- 查看所有
	SHOW DATABASES; 
	-- 进入
	USE $DATABASE;
	# 创建
	CREATE DATABASE $DATABASE [DEFAULT CHARSET=utf8];
	-- 删除
	DROP DATABASE $DATABASE;
	```

# Table 数据表

## TABLE 基础

- **基础命令**

	```sql
	-- 查看某个数据库中所有数据表
	SHOW TABLES;
	-- 查看表头
	DESC $TABLE
	-- 删除 TABLE
	DROP TABLE $TABLE
	-- 清空 TABLE
	DELETE FROM $TABLE
	```

- **创建数据表**（以 MySQL 为例）

	```sql
	CREATE TABLE $TABLE(
		$COLUMN $CONDITION,
		$COLUMN $CONDITION,
		$COLUMN $CONDITION,
		$COLUMN $CONDITION
	)DEFAULT CHARSET=utf8;
	```

	```sql
	CREATE TABLE tb_users (
	    id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
	    username VARCHAR(16) NOT NULL UNIQUE,
	    password VARCHAR(255) NOT NULL
	) DEFAULT CHARSET=utf8;
	```
	
	**在以上代码中**：
	
	1. **`INT`**：整型
	2. **`NOT NULL`**：非空
	3. **`AUTO_INCREMENT`**：
	4. **`PRIMARY KEY`**：主键

# Field 字段

**字段**（Field）是数据库中表的一个组成部分，代表了表中的一个列，用于存储数据。

字段由不同属性组成，每种实例表示属性的方式也不相同。

**常用的字段属性**：

- **名称**：字段的标识符，用于区分字段。**命名习惯**：小蛇形，例 `tb_users`。
- **数据类型**：字段中存储数据的类型（如整数、字符串、日期等）。
- **约束**：字段的限制条件（如 `NOT NULL`、`PRIMARY KEY`、`UNIQUE` 等）。
- [`自增`](https://www.w3cschool.cn/sql/2phntfpq.html)：`AUTO_INCREMENT`，在新记录插入表中时生成一个唯一的数字。

**常用数据类型**：

- `INT`：整型
- `VARCHAR`：可变长度字符串

**常用的约束**：

- [PRIMARY KEY](https://www.w3cschool.cn/sql/vle8zfpd.html)：主键
	- 主键必须包含唯一的值。
	- 主键列不能包含 NULL 值。
	- 每个表都应该有一个主键，并且只能有一个主键。
- [FOREIGN KEY](https://www.w3cschool.cn/sql/5dycsfpf.html)：外键
	- 一个表中的 `FOREIGN KEY` 指向另一个表中的 `PRIMARY KEY`。
- [NOT NULL](https://www.w3cschool.cn/sql/6tlpzfpb.html)：非空
- [DEFAULT](https://www.w3cschool.cn/sql/jm8e9fpj.html)：默认
- [UNIQUE](https://www.w3cschool.cn/sql/wxzqsfpc.html)：确保唯一
- [CHECK ](https://www.w3cschool.cn/sql/fsq7hfph.html)：保证列中的所有值满足某一条件
- [INDEX](https://www.w3cschool.cn/sql/cuj91oz2.html)：索引，用于在数据库中快速创建或检索数据

# Row 数据行

- **基础命令**

	```sql
	-- 查看 row
	SELECT * FROM $TABLE [where id=1];
	-- 删除 row
	DELETE FROM $TABLE [where $CONDITION];
	-- 添加 row
	INSERT INTO $TABLE($COLUMN1, $COLUMN2, ...) values('$VALUE1', '$VALUE2', ...);
	```

# Column 数据列

- **基础命令**

	```sql
	-- 删除 COLUMN
	ALTER TABLE $TABLE DROP COLUMN $COLUMN
	```

# Data 数据

- **查看数据**

	```sql
	-- 查看数据行的所有字段数据
	SELECT * FROM $TABLE WHERE $CONDITION;
	
	-- 查看数据行的某些字段数据
	SELECT $COLUMN[, $COLUMN2...] FROM $TABLE WHERE $CONDITION;
	```

- **更新数据**

	```sql
	UPDATE $TABLE SET $COLUMN = $VALUE WHERE $CONDITION;
	```

	```SQL
	UPDATE tb1 SET mobile = '1999999999' WHERE name = 'zhangsan';
	
	UPDATE tb1 SET 
		name = 'zhangsan', 
		mobile = '1999999999' 
	WHERE name = 'zhaoliu';
	```

# SELECT

- 使用 `SELECT $FIELD FROM $TABLE` 用于查询某个字段的数据

## Where

- 使用 `WHERE 子句` 添加查询条件

- WHERE 子句可以包含一个或多个查询条件。

    - **一个条件**

        ```sql
        SELECT Name,Phone FROM Account WHERE Name='SFDC Computing'
        ```

    - **多个条件**：使用逻辑运算符 （AND、OR）和圆括号 `()` 对所有条件进行分组，类似数学运算。

        ```sql
        SELECT Name,Phone FROM Account
           WHERE (Name='SFDC Computing' OR (NumberOfEmployees>25 AND BillingCity='Los Angeles'))
        ```

- **通配符**

    - `%` 匹配任何字符匹配或不匹配任何字符。
    
    - `_` 匹配一个字符。
    
    - 使用 **like** 代替 **=** 匹配通配符
    
        ```sql
        SELECT * FROM books WHERE title LIKE 'The _e%';
        ```

## Order

- 使用 `ORDER BY $FIELD_NAME` 对查询结果排序

- **语法**

    ```sql
    // 按字母顺序升序排列
    SELECT * FROM Contact ORDER BY Name [ASC];
    
    // 按字母顺序降序排列
    SELECT * FROM Contact ORDER BY Name DESC;
    ```

- **升序和降序**

    - **ASC**：默认为升序 (ascending)，可省略；
    - **DESC**: 降序 (descending)。

## Limit

- 使用 `LIMIT n` 限制查询结果的返回的记录数量。

    ```sql
    SELECT Name FROM Account LIMIT 1;
    ```

# 其它

- **引用变量**：在 SQL 语句中可以引用其它语言声明的变量，不同语言的引用方式不同。