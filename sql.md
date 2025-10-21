---
title: sql
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - database
  - code-language
  - web
---

# SQL 基础

**SQL**（**S**tructured **Q**uery **L**anguage）即结构化查询语言，是用于与**关系型**数据库管理系统（RDBMS）交互的标准操作语言。

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
- **语句尾缀**：以 `;` 作为 SQL 语句的结束标志，但有些系统也允许不写分号。
- **占位符**：由于习惯大写关键字，所以个人笔记占位符前缀加 `$`。
- **字符串**：字符串使用单引号 `'` 包围；双引号有其它用途，各个语言不一样。

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

# SELECT Clause

- **SELECT** clause is used to specify which field to query.

## Basic Example

```sql
SELECT 列名
FROM 表名
[WHERE condition]
[GROUP BY column1, column2, ...]
[HAVING condition]
[ORDER BY 列名]
[LIMIT 行数];
```

```sql
SELECT name FROM students
```

```sql
-- 可用 * 表示所有列
SELECT * FROM students
```

# FROM Clause

# WHERE Clause

- **WHERE** clause is used to filter the query results without aggregating. Different from HAVING.

## Basic Example

- **Syntax**

  ```sql
  SELECT 列名
  FROM 表名
  WHERE 条件;
  ```

  ```sql
  SELECT name
  FROM students
  WHERE age = 18;
  ```

## Operator

- 在 sql 中，**操作符**用于对条件进行分组和限定。
- Example

  ```sql
  SELECT name
  FROM students
  WHERE (age = 18 OR (score > 60 AND gender = 'male'));
  ```

### AND

- `AND` 与条件。

  ```sql
  WHERE 条件1 AND 条件2;
  ```

  ```sql
  WHERE age = 18 AND score > 60 AND gender = 'male';
  ```

### OR

- `OR` 或条件。

  ```sql
  WHERE 条件1 OR 条件2;
  ```

  ```sql
  WHERE age = 18 OR score > 60 OR gender = 'male';
  ```

### IN

- `IN` 操作符用于判断某个字段的值是否在指定的一组值中。替代使用多个 `OR` 条件的复杂写法。
- IN 的基本用法

  ```sql
  WHERE 列名 IN (值1, 值2, ...);
  ```

  ```sql
  WHERE age IN (15, 16, 17);
  ```

- 搭配子查询

  ```sql
  WHERE 列名 IN (SELECT 其它列名 FROM 其他表名);
  ```

  ```sql
  -- 子查询，从 valid_ages 表获取有效年龄
  WHERE age IN (SELECT age FROM valid_ages);
  ```

### BETWEEN

- `BETWEEN` 操作符用于判断某个字段的值是否在指定的范围之内，这个范围包含边界值。

  ```sql
  WHERE 列名 BETWEEN 值1 AND 值2;
  ```

  ```sql
  WHERE age BETWEEN 18 AND 20;
  ```

### LIKE

- `LIKE` 用于对文本字段进行模糊查询。

  ```sql
  WHERE 列名 LIKE 匹配模式;
  ```

  ```sql
  WHERE note LIKE '%先生';
  ```

- **Wildcard**

  - `%`：匹配任意数量（包含零个）字符。
  - `_`：匹配任意单个字符。
  - `[]`：用于指定一个字符范围或一组字符，只要匹配其中一个字符就算匹配成功。

    ```sql
    -- 匹配第二个字符为 “a”、“b” 或者 “c” 的客户
    SELECT * FROM customers WHERE customer_name LIKE '_[abc]%';
    ```

  - `^` 或 `!`：在使用方括号时，`^`（SQL Server）或 `!`（Access）用于表示取反，即匹配不在指定范围内的字符。

    ```sql
    -- 匹配第二个字符不是 “a”、“b” 或者 “c” 的客户
    SELECT * FROM customers WHERE customer_name LIKE '_[^abc]%';
    ```

### NOT

- `NOT` 用于对条件取反。

  ```sql
  -- 对逻辑取反
  WHERE NOT (age = 18 OR (score > 60 AND gender = 'male'));

  -- 对 IN 取反
  WHERE age IN (15, 16, 17);

  -- 对 LIKE 取反
  WHERE note NOT NLIKE '%先生';
  ```

# ORDER Clause

- **ORDER** clause is used to order the query result.

## Basic Example

- **Syntax**

  ```sql
  SELECT 列名
  FROM 表名
  ORDER BY 列名 [ASC|DESC];
  ```

  ```sql
  SELECT *
  FROM students
  ORDER BY name;
  ```

## Order Condition

- 排序条件用于指定排序方式
- **Example**

  ```sql
  // 按字母顺序升序排列
  SELECT * FROM students ORDER BY name [ASC];

  // 按字母顺序降序排列
  SELECT * FROM students ORDER BY name DESC;
  ```

  - **ASC**：默认为升序 (ascending)，可省略；
  - **DESC**: 降序 (descending)。

- Ordered by multiple columns.

  ```sql
  SELECT * FROM students ORDER BY name, id;
  ```

# LIMIT Clause

- **LIMIT** clause is used to limit the number of query results.
- **Syntax**

  ```sql
  SELECT 列名
  FROM 表名
  LIMIT [开始行号] 行数;
  ```

  ```sql
  SELECT * FROM students LIMIT 5;
  ```

# JOIN Clause

- **JOIN** clause is used to join the data from multiple tables.

## INER JOIN

- **INER JOIN** only returns the combinations of all rows in two tables that meet the join condition.
- **INER JOIN** equals to **JOIN**.
- **Syntax**

  ```sql
  SELECT field1, field2
  FROM table1
  INNER JOIN table2
  ON table1.field3 = table2.field3;
  ```

  ```sql
  SELECT students.student_name, courses.course_name
  FROM students
  INNER JOIN courses
  ON students.student_id = courses.student_id;
  ```

  - `students` table

    | student_id | student_name |
    | ---------- | ------------ |
    | 1          | Alice        |
    | 2          | Bob          |
    | 3          | Charlie      |

  - `courses` table

    | course_id | course_name | student_id |
    | --------- | ----------- | ---------- |
    | 101       | Math        | 1          |
    | 102       | English     | 2          |
    | 103       | Science     | 1          |

  - Result table

    | student_name | course_name |
    | ------------ | ----------- |
    | Alice        | Math        |
    | Alice        | Science     |
    | Bob          | English     |

## Other JOIN

- LEFT OUTER JOIN
- RIGHT OUTER JOIN
- FULL OUTER JOIN
- CROSS JOIN
- SELF JOIN

# AS Clause

- **AS** clause is used to specify a alias (similar to variables) for a field.
- **Syntax**

  ```sql
  SELECT 列名 AS 别名
  FROM 表名;
  ```

  ```sql
  SELECT gender, name AS student_name FROM students;
  ```

  | gender | student_name |
  | ------ | ------------ |
  | male   | Jerry        |

- **Notice**

  - Execution order: **FROM** > ... > **SELECT** > **ORDER BY**
  - So, the alias declared last in the behind clause shouldn't be used in the front ones.

    ```sql
    -- Error Example
    SELECT gender, COUNT(name) AS student_count
    FROM students
    GROUP BY gender
    HAVING student_count > 2; -- student_count is declared in SELECT clause

    -- Correct Example
    SELECT e.employee_id, d.department_name
    FROM employees AS e
    JOIN departments AS d ON e.department_id = d.department_id;
    ```

# Aggregate Functions

- **Aggregate Functions** are functions that calculate the values of a specified field.
- **Syntax**

  ```sql
  SELECT {Function}(列名)
  FROM 表名;
  ```

  ```sql
  SELECT COUNT(gender) FROM students;
  ```

- Common Aggregate Function

  - **`COUNT()`**: Include the repeative values. Exclude NULL.
  - **`COUNT(DISTINCT {Field})`**: Exclude the repeative values. Exclude NULL.
  - **`MIN()`**: Also can handle date and time.
  - **`MAX()`**: Also handle date and time.
  - **`AVG()`**
  - **`SUM()`**

# GROUP Clause

- **GROUP** Clause is used to group query results. Usually used together with Aggregate Functions.
- Query results are grouped by fields.
- **Syntax**

  ```sql
  SELECT 列名1, {Function}(列名2) AS 别名
  FROM 表名
  GROUP BY 列名1;
  ```

  ```sql
  SELECT gender, COUNT(name) AS student_count
  FROM students
  GROUP BY gender;
  ```

  | gender | student_count |
  | ------ | ------------- |
  | male   | 3             |
  | female | 2             |

# HAVING Clause

- **HAVING** clause is used to filter the results returned by an aggregate function. Different from WHERE.

- **Syntax**

  ```sql
  SELECT 列名1, {Function}(列名2) AS 别名
  FROM 表名
  GROUP BY 列名1
  HAVING 条件;
  ```

  ```sql
  SELECT gender, COUNT(name) AS student_count
  FROM students
  GROUP BY gender
  HAVING COUNT(name) > 2;
  ```

  | gender | student_count |
  | ------ | ------------- |
  | male   | 3             |

# Database

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

# Table

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

  - **`INT`**：整型
  - **`NOT NULL`**：非空
  - **`AUTO_INCREMENT`**：
  - **`PRIMARY KEY`**：主键

# Field

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

# Row

- **基础命令**

  ```sql
  -- 查看 row
  SELECT * FROM $TABLE [where id=1];
  -- 删除 row
  DELETE FROM $TABLE [where $CONDITION];
  -- 添加 row
  INSERT INTO $TABLE($COLUMN1, $COLUMN2, ...) values('$VALUE1', '$VALUE2', ...);
  ```

# Column

- **基础命令**

  ```sql
  -- 删除 COLUMN
  ALTER TABLE $TABLE DROP COLUMN $COLUMN
  ```

# Data

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

# 其它

- **引用变量**：在 SQL 语句中可以引用其它语言声明的变量，不同语言的引用方式不同。
