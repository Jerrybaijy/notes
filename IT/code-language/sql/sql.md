# SQL

**SQL**（**S**tructured **Q**uery **L**anguage）即结构化查询语言，是用于与**关系型**数据库管理系统（RDBMS）交互的标准编程语言。

## SQL 基础

### 注释

- **语法**：单行注释 `--`；多行注释 `/* */`

	```sql
	SELECT * FROM users;  -- 这是一个单行注释
	
	/*
	这是一个多行注释
	它可以跨越多行
	并且会被 SQL 引擎忽略
	*/
	```

### SQL 语法规范

- **大小写不敏感**：SQL 中的关键字（如 SELECT、FROM 等）通常不区分大小写，但都习惯大写。
- **缩进与空格**：虽然语法上没有严格要求，但合理使用缩进和空格可以提高 SQL 语句的可读性。
- **语句结束符**：以 `;` 作为 SQL 语句的结束标志，但有些系统也允许不写分号。
- **占位符**：由于习惯大写关键字，所以个人笔记占位符前缀加 `$`。
- **字符串**：字符串使用单引号 `'` 包围；双引号有其它用途，各个语言不一样。

### SQL 关键字

- **`*`**：表示所有。
	- `SELECT * FROM tb_test;`：查看 `tb_test` 数据表中所有 ROW。
- **`WHERE`**：`$COMMAND WHERE $CONDITION;`，用于添加查询条件。
	- `DELETE FROM tb_test WHERE id=1;`：从 `tb_test` 数据表中删除 `id=1` 的 ROW。

### SQL 标准和数据库实现

虽然 SQL 是一个标准语言，但不同的数据库管理系统在 SQL 语言的实现上会有一些差异。常见的差异包括：

- **数据类型**：不同数据库使用不同的命名和支持的类型。
- **SQL 方言**：某些 SQL 语法可能只在特定的数据库中有效。
- **扩展功能**：如特定的函数、存储过程、触发器等。

## 数据库 `DATABASE`

- **基础命令**

	```sql
	-- 查看所有
	SHOW DATABASES; 
	-- 进入
	USE $DATABASE;
	# 创建
	CREATE DATABASE $DATABASE [default charset=utf8];
	-- 删除
	DROP DATABASE $DATABASE;
	```

## 数据表 `TABLE`

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

- **创建数据表**

	```sql
	CREATE TABLE $TABLE(
		$COLUMN $CONDITION,
		$COLUMN $CONDITION,
		$COLUMN $CONDITION,
		$COLUMN $CONDITION
	)DEFAULT CHARSET=utf8;  -- 以 MySQL 为例，其它数据库字符集关键字不同
	```

	```sql
	CREATE TABLE tb_test (
	    id INT PRIMARY KEY AUTO_INCREMENT NOT NULL,  -- 自动递增的主键
	    address VARCHAR(16),                         -- 存储地址，最大16个字符
	    name VARCHAR(16)                             -- 存储名字，最大16个字符
	) DEFAULT CHARSET=utf8;                          -- 设置表的字符集为 UTF-8
	```

## 数据行 `ROW`

- **基础命令**

	```sql
	-- 查看 row
	SELECT * FROM $TABLE [where id=1];
	-- 删除 row
	DELETE FROM $TABLE [where $CONDITION];
	-- 添加 row
	INSERT INTO $TABLE($COLUMN1, $COLUMN2, ...) values('$VALUE1', '$VALUE2', ...);
	```

## 数据列 `COLUMN`

- **基础命令**

	```sql
	-- 删除 COLUMN
	ALTER TABLE $TABLE DROP COLUMN $COLUMN
	```

## 数据 `DATA`

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