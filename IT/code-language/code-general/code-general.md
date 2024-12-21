# 编程基础

## 环境搭建

### 解释器

- 为代码提供运行环境

### 解释器虚拟环境

- 虚拟环境是一个独立的解释器实例，包含了自己的解释器、库和配置。通过虚拟环境，开发者可以为每个项目隔离依赖，避免全局安装的库和版本冲突。

- 每个虚拟环境都记录了特定项目的依赖，通过 `requirements.txt` 等文件，可以轻松管理和复制环境。

### 编辑器

- 编辑器，即集成开发环境（**I**ntegrated **D**evelopment **E**nvironment，简称 IDE） 。它是一种软件应用程序，提供了用于软件开发的各种工具和功能，如代码编辑器、编译器、调试器、版本控制工具等，以帮助开发者更高效地编写、调试和管理代码。常见的 IDE 有 VS Code，PyCharm，IDEA 等。
- **作用**：编写代码 ，调用解释器运行代码。

### 交互式环境

- 即命令行中的环境；
- 临时写代码可在交互式环境中进行，但注意此环境不保存；
- 交互式环境中可省略 print 步骤，写入函数后，回车自动显示执行结果；
- Shell 环境 > `python` > `Enter` > 进入交互式环境；
- `exit()` > 退出交互式环境。

## 代码规范

- **符号**：必须使用英文状态
- **缩进**：
  - 不敏感（Python 敏感）
  - 应使用 `Tab` 键，不能使用 `Space` 键，删除缩进用 `Shift + Tab`
- **空白行**：不敏感
- **换行**：不敏感

## 标识符

- **规范**
  - 只能含有字母、数字、下划线、$，且不能以数字开头
  - 大小写敏感
  - 不能是关键字和保留字
- **命名方法**
  - **蛇形命名法**：即下划线命名法，使用全小（大）写英文单词，多个单词使用下划线连接，例：`my_first_code`（`MY_FIRST_CODE`）
  - **驼峰命名法**：首字母小（大）写，后续每个单词首字母大写，例：`myFirstJavaFunction`（`MyFirstJavaClass`）。
- **命名习惯**
  - **变量名**：小驼峰，例 `maxLength`。
  - **常量名**：大蛇形，例 `MAX_LENGTH`。
  - **类名**：大驼峰，例 `MyFirstJavaClass`。
  - **普通函数（方法）名**：小驼峰，例 `maxLength`。
  - **构造函数名**：首字母大写，例 `Person`。
  - **文件名**：
  - **环境变量**：大蛇形，例 `MAX_LENGTH`。
  - **占位符**：大蛇形

## 注释

- **注释**：注释是对代码的解释说明，不被执行。注释结果：第一行作为说明不执行，其余代码正常执行。
- **单行注释**：`Ctrl + / `，注释一行代码；单行注释可以写在段首，也可写在某行代码的最后，但不能写在前面，否则整行都会变成注释。
- **多行注释**：`Ctrl + Shift + / `，注释多行代码；多行注释都是用特定符号将多行代码包围。

## 字面量、变量、常量

### 字面量

- 字面量其实就是一个值，代表的含义就是字面的信息
- 比如：`1` `100` `“Hello”` `true` `null`

### 常量

- 即不可改变值的内存地址的量，用来接收字面量。
- 比如：`3.1415926`

### 变量

- **变量**：即可以改变值的内存地址的量，用来接收字面量。

- **变量三要素**：变量名、变量值、变量数据类型。

- **变量格式**：变量名 = 变量值

- 变量值是字符串，则变量值需要加引号；否则变量值无需加引号。

  ```python
  a = 1  # 数值型变量值
  print(a)  # 1
  
  b = "1"  # 字符型变量值
  print(b)  # 1
  
  c = "张三"  # 字符型变量值
  print(c)  # 张三
  ```

## 输入与输出

- 可以输出多个变量名，用逗号隔开，可获取多个变量值

  ``` python
  a = "张三"
  b = "李四"
  c = "王五"
  print(a, b, c)  # 张三 李 王五
  ```

## 作用域和闭包

### 作用域

- **全局作用域**：整个程序的作用域。
	- 全局变量具有全局作用域；
	- 全局作用域不能直接使用局部变量。
- **局部作用域**：函数级或块级作用域。
	- 局部变量只具有局部作用域；
	- 局部作用域优先使用局部变量，如果没有，再使用全局变量。
- **函数作用域**：即函数内部的作用域，属于局部作用域。
- **块级作用域**：即代码块内部的作用域，属于局部作用域。

### 闭包

- **闭包**：通过函数嵌套机制，先将外部函数数据封装到内部函数作用域，后续再执行内部函数时，直接获取封装进内部函数作用域的数据即可。

- 闭包的作用就是解决在全局无法调用函数内部定义的函数。

- 在本质上，闭包是将函数内部和函数外部连接起来的桥梁。

- **高阶函数示例**

	```python
	def func():
	    print(123)
	    def new_func():
	        print(456)
	    return new_func
	
	v1 = func()  # 123
	v1()  # 456
	```

## 代码块

**代码块**是由花括号 `{}` 括起来的一组语句。在大多数编程语言中，代码块用于定义一段逻辑代码，通常作为控制流语句（如条件语句和循环语句）的执行体。在 JavaScript 中，代码块也用于创建局部作用域。

### 控制流语句中的代码块

- **if 语句**

	```javascript
	if (condition) {
	  // 这里是 if 语句的代码块
	  // 如果条件为真，这里的代码会被执行
	} else {
	  // 这里是 else 语句的代码块
	  // 如果条件为假，这里的代码会被执行
	}
	```

- **for 循环**

	```javascript
	for (let i = 0; i < 5; i++) {
	  // 这里是 for 循环的代码块
	  // 循环体中的代码会被执行 5 次
	}
	```

- **while 循环**

	```javascript
	let i = 0;
	while (i < 5) {
	  // 这里是 while 循环的代码块
	  // 循环体中的代码会被执行 5 次
	  i++;
	}
	```

### 函数中的代码块

- 在函数中，代码块用于定义函数体，即函数要执行的一系列语句。

	```javascript
	function greet(name) {
	  // 这里是函数体的代码块
	  console.log("Hello, " + name + "!");
	}
	
	greet("Alice"); // 调用函数，执行代码块
	```

### 创建局部作用域

- 在 JavaScript 中，代码块也用于创建局部作用域，这意味着在代码块内声明的变量在代码块外不可见。

	```javascript
	{
	  // 这里是代码块，也是局部作用域
	  let localVar = "I am local!";
	  console.log(localVar); // 可以在代码块内访问
	}
	
	console.log(localVar); // 无法在代码块外访问，会报错
	```

# 数据类型

## 数据类型分类

- **数值型**
	- 整型 `int`
	- 浮点型 `float`
	- 数字 `number`
	- 大整数 `bigint`

- **非数值型**
	- 字符型
	- 字符串
	- 布尔型
	- 空值
	- 列表（数组）
	- 字典
	- 集合
	- ...

## 布尔型

- **布尔值**表示真假的判断，属于不可变数据类型。
- 一个布尔型只有 `True` 和 `False` 两种值（不同语言注意大小写）。

  ```python
  a = True  # 真
  b = False  # 假
  print(5 > 3)  # True
  print(6 < 2)  # False
  ```

## 字符串

- **定义**：字符串是一串字符，用来保存普通文本，属于不可变数据类型。

	```python
	strr1 = "Hello world!"  # 文本形式的字符串
	strr2 = ""  # 空字符串
	strr3 = "6"  # 数值形式的字符串
	```

- **<span id="string-boundary-marking">边界标记</span>**：可以是成对的单引号 `'`、双引号 `"`、三重单引号 `'''`、三重双引号 `"""`。不同语言在处理字符串的边界标记上的语法有所不同，但核心思想（支持单引号、双引号，复杂时支持多行字符串）是一致的。

	- **普通字符串**，通常使用双引号 `"` 作为边界标记。

		```python
		strr = "Hello world!" 
		```

	- **多行字符串**，通常使用三重双引号 `"""` 作为边界标记。（或者使用模板字符串）

		```python
		strr = """
		Hello,
		world!
		"""
		```

	- **子字符串**，子母字符串的边界标记应不同。（或者使用转义）

		```python
		# 字母字符串标记边界相同
		strr1 = "Hello "world"!" 
		print(strr1)  # 报错
		
		# 字母字符串标记边界不同
		strr2 = "Hello 'world'!"
		print(strr2)  # Hello 'world'!
		```

- **转义**：字母字符串边界标记相同或含有其它需要转义的内容（详见[转义字符](../../web-basics/web-basics.md#转义字符)）的时候，需要使用 `\` 转义。

	```python
	strr1 = "Hello world!" 
	print(strr1)  # Hello world!
	
	strr2 = "\"Hello world!\""
	print(strr2)  # "Hello world!"
	```

### 字符串功能

- **获取长度**
	- 用于获取字符串长度，返回字符串长度。

- **索引**
	- 索引用于根据索引号获取字符串片段或者容器元素，返回字符串或者容器元素。
	- 支持索引的数据类型每个元素都有一个索引号（又称下标）。
	- 正序从0开始，逆序从-1开始。有的语言没有直接逆序索引，比如 JavaScript。
	- 功能
		- 获取元素
		- 修改元素
		- 索引切片
		- 多层嵌套。
- **遍历**
	- 使用 `for-of` 语句

- **`in` 包含**
	- 用于判断一个字符串是否含在另一个字符串中，返回布尔值。

- **切片**
	- 切片用于截取字符串的某个片段，返回字符串。
	- 索引号左闭右开。
	- 原字符串不受影响。

- **切割**
	- 用于根据切割标识，将一个字符串切割成多段，返回列表（数组）。

- **合并**
	- 用于将多个数据类型，合并成一个字符串，返回字符串。

- **模板字符串**
	- 跨行输出
	- 嵌套变量 + 拼接

- **替换**
	- 用于使用一段字符串代替一个字符串的某个片段，返回字符串。

- **去除空格、换行**
	- 用于去除字符串开头和结尾的空格以及结尾的换行符，返回新 `str`。
	- 此功能不能去除中间的空格，去除中间空格应使用 `STR.replace(" ", "")`，将空格替换成空白。

- **转大小写**
	- 将原字符串中的全部字母转换成大写或小写，返回字符串。

- **判断起始**
	- 用于判断一个字符串是否以某个字符串片段开头，返回字符串。

- **判断数字**
	- 用于判断一个字符串是否是数字形式的字符串，返回布尔值。

- **找下标**
	- 用于根据匹配项找其在原字符串中的索引号，返回数字。

## 空值

- 空值表示什么也没有；不能理解为 `0`，`0` 有意义，而空值无意义。

## 列表（数组）

### 列表（数组）基础

- 列表（数组）是一个有序的序列结构。
- **特性**

  - 可存放多种数据类型
  - 有序，可索引
  - 元素可重复
  - 元素可修改，属于可变类型。

- **基础示例**

	```python
	lst = ["中国", "上海", 123]
	print(lst)  # ['中国', '上海', 123]
	print(type(lst))  # <class 'list'>
	```

### 列表（数组）公共功能

- 以下功能详见字符串
- 获取长度 `.length`
- 索引（数组不可索引切片）
- 遍历 `for-of 语句`
- `in` 包含 （数组没有）
- 嵌套
- 切片 `.slice()`
- 合并 `.concat()`

### 列表（数组）其它功能

- **修改元素（索引）**
	- 通过索引号修改：`lst[0] = 5`

- **追加元素**
	- 向列表（数组）尾部添加元素

- **插入元素**
	- 向列表（数组）任意位置添加元素

- **删除元素**
	- 删除某个元素

- **清空**
	- 清空所有元素

- **反转**
	- 将列表（数组）所有元素颠倒顺序

- **升序**
	- 将列表（数组）所有元按升序排列顺序

- **连接**
	- 将列表（数组）所有元素，按指定分隔符连接成一个字符串。

## 元祖

- 元组（Tuple）是一种不可变的有序集合。

- **特性**

  - 有序，可索引。
  - 属于不可变类型，元素不可修改（元素为容器时除外）。
  - 轻量级数据结构，占用内存少，存储和检索效率高。

- **基础示例**

  ```python
  tpl = ("中国", "上海", 123)
  print(tpl)  # ('中国', '上海', 123)
  print(type(tpl))  # <class 'tuple'>
  ```

## 集合

- **集合**是一种无序的序列结构；用来去重复值和进行数学集合运算。
- **特性**

	- 可存放多种数据类型
	- 无序，不可索引
	- 元素不可重复
	- 元素可修改，属于可变类型。

- **基础示例**

	```python
	st = {"中国", "上海", 123}
	print(st)  # {123, '上海', '中国'}
	print(type(st))  # <class 'seta'>
	```

## 字典

### 字典基础

- **字典**是一种键值对结构的序列结构，一对键值对被视为一个元素，用在高速查找的地方。
- 键必须是哈希类型：int、bool、str、tuple，一般用字符串作为键，不可重复。
- **基础示例**

	```python
	dict_a = {"A": 1,"B": 2,"C": 3}
	print(dict_a)  # {'A': 1, 'B': 2, 'C': 3}
	print(type(dict_a))  # <class 'dict'>
	```

### 字典公共功能

- 以下功能详见字符串
- 获取长度 `.length`
- 索引（用键作为索引）
- 遍历 `for-in 语句`（获取到键）
- `in` 包含 （判断键）
- 嵌套

### 字典其它功能

- 获取值
- 修改值
- 增加元素
- 删除元素
- 获取所有值
- 获取所有键
- 获取所有键和值
- 构造字典

## 容器嵌套

- **容器嵌套**：容器与容器之间可相互嵌套，得到多维容器。
- **索引示例：找北京**

	```python
	lst1 = [213, 2432, 43, 545, 46]
	lst2 = [1212, 234, 35, 45, "你好", (1, 23, 2, "北京", 535, 4), 68, 12]  # 多维容器
	lst3 = [44, 67, 67, 8798, 64, 646, 5, 345]
	lst4 = [lst1, lst2, lst3, [21, 322, 343, 5, 4, 6, 6]] 
	print(lst4[1][5][3])  # 北京
	```

	**在以上示例中**：

	1. 北京在 `lst2` 中，所以第一个索引为1；
	2. 北京在元组 `(1,23,2,"北京",535,4,)` 中，此元组在 `lst2` 中索引号为5，所以第二个索引号为5；
	3. 北京在元组 `(1,23,2,"北京",535,4,)` 中的索引号为3，所以第三个索引号为3。

## 获取数据类型

- 根据各自语言的不同函数可获到取数据类型，以 Python 为例：

	```python
	lst = ["中国", "江西", "联通"]
	print(type(lst))  # <class 'str'>
	```

## 数据类型转换

- 数据类型转换，可以将数据转换成我们需要的类型。
- **自动转换**：系统按照既定规则自己转换
- **强制转换**：人为干预转换类型

  - **显式转换**：利用函数和方法
  - **隐式转换**：利用运算符

- **说明**：浮点型强制转换成整型，会直接去掉小数部分，损失计算精度。

## 数据的可变性

- **数据的可变性**：是指一个数据对象在创建后是否允许被直接修改。

  - **可变数据类型**（Mutable Data Types）：对原对象修改操作时，会直接改变原对象。
  - **不可变数据类型**（Immutable Data Types）：对原对象修改操作时，不会直接改变原对象，而是生成一个新对象。

- 变量是通过指向对象来引用值的，所以即使一个变量的值是不可变数据类型，也可以通过改变这个变量的指向来改变它的值。

  ```python
  name2 = "root"
  name2 = name2.upper()  # 生成新对象 ROOT，改变变量 name2 的指向对象为 ROOT
  print(name2)  # ROOT  # 变量 name2 的值改变
  ```

- **说明**：数据的可变性取决于语言的内存地址管理和对象模型，不同语言，情况不同。

  - 某些语言的原始数据类型（如数字、字符串）是不可变的，容器（如列表、数组、字典、集合）是可变的。
  - 某些语言（如 C/C++）的普通变量和对象默认可变，只有通过 `const` 关键字创建的变量和对象是不可变的。

- **可变类型和不可变类型对比**

  ```python
  # 操作不可变数据类型
  name1 = "root"
  name1.upper()  # 生成新对象 ROOT（没有变量接收），变量 name1 仍指向原对象 root。
  print(name1)  # root # name1 的值不变

  # 操作可变数据类型
  name2 = ["Jerry", "Peter"]
  name2.append("Andy")  # 未生成新对象，但原对象添加了 Andy，变量 name 仍指向原对象
  print(name2)  # ['Jerry', 'Peter', 'Andy']  # name2 的值增加了 Andy
  ```

- **不可变类型，变量指向变更对比**

  ```python
  # 操作不可变数据类型，变量指向不变
  name1 = "root"
  name1.upper()  # 生成新对象 ROOT（没有变量接收），未改变变量 name1 的指向原对象，仍为 root。
  print(name1)  # root # 变量 name1 的值不变

  # 操作不可变数据类型，变量指向改变
  name2 = "root"
  name2 = name2.upper()  # 生成新对象 ROOT，改变变量 name2 的指向对象为 ROOT
  print(name2)  # ROOT  # 变量 name2 的值改变
  ```

- **通过变量值判断数据的可变性**

  ```python
  # 操作字符串后变量值不变
  strr = "中国江西联通"
  strr.replace("联通", "移动")
  print(strr)  # 中国江西联通  # strr 的值不变
  
  # 操作列表后变量值发生改变
  lst = [1, 2, 3, 4]
  lst.append(5)
  print(lst)  # [1, 2, 3, 4, 5]  # lst 的值发生改变
  ```

# 运算符

运算符是各种表达式中的符号。

## 算术运算符

- **算术运算符**：数学运算中的符号
  - **`+`**：加
  - **`-`**：减
  - **`*`**：乘
  - **`/`**：除
  - **`**`**：幂
  - **`//`**：向下取整除（除法保留整数）
  - **`%`**：取模（除法获取余数）

## 赋值运算符

- **赋值运算符**：赋值运算符用来将一个值赋值给变量。
- **基本赋值运算符**

  - **`=`**：赋值

- **复合赋值运算符**

  - **`+=`**：加赋值
  - **`-=`**：减赋值
  - **`*=`**：乘赋值
  - **`/=`**：除赋值
  - **`**=`**：幂赋值
  - **`++`**：自增，即在自身的基础加1
  - **`--`**：自减，即在自身的基础减1
  - **`%=`**：求余赋值
  - **`//=`**：取整除赋值
  - **`??=`**：空赋值
  -  `<<=`：左移赋值
  -  `>>=`：右移赋值
  - `>>>=`：无符号右移赋值

- **解构赋值运算符**

  ```python
  a, b, c = 1, 2, 3  # 将值 1, 2, 3 分别赋给 a, b, c
  print(a, b, c)  # 输出: 1 2 3
  ```

- **函数默认参数赋值**

  ```python
  def greet(name="Guest"):
    print(f"Hello, {name}")
  
  greet()  # 输出: Hello, Guest
  greet("Alice")  # 输出: Hello, Alice
  ```

## 关系运算符

- **关系运算符**：用来检查两个值之间的关系是否成立，关系运算符运算的结果是**布尔值**

  - **`>`**：大于
  - **`<`**：小于
  - **`>=`**：大于等于
  - **`<=`**：小于等于
  - **`==`**：相等（值相等，类型忽略，返回 `真`）
  - **`!=`**：不等（值不相等，类型忽略，返回 `真`）
  - **`===`**：全等（值相等，类型也相同，返回 `真`）
  - **`!==`**：不全等（值和类型至少有一个相等，返回 `真`）

- 判断数字关系

  ``` python
  a = 5
  b = 6
  print(a > b)  # False
  print(a < b)  # True
  print(a == 5)  # True
  print(a >= b)  # False
  print(a != b)  # True
  ```

- 判断字符串关系示例：用来判断用户输入的内容与存储内容是否一致，比如登录密码。

  ``` python
  c = "hello"
  d = "你好"
  print(c == d)  # False
  print(c != d)  # True
  ```

## 逻辑运算符

- **逻辑运算符**：判断表达式之间的逻辑关系，即判断真假。
- **非**：对原布尔表达式取反，如果原表达式为 `true`，则返回 `false`，否则返回 `true`。
  - **`not`**：非
  - **`!`**：非

- **与**：当两个布尔表达式都为 `true`，则返回 `true`，否则返回 `false`。
  - **`and`**：与
  - **`&&`**：与

- **或**：当两个布尔表达式中全为 `false`，则返回 `false`，否则返回 `true`。
  - **`or`**：或
  - **`||`**：或

- **示例**

  ``` python
  print(5 > 3 and 6 < 3)  # False
  print(5 > 3 or 6 < 3)  # True
  print(not 6 > 3)  # False
  ```

- **逻辑运算顺序**：`非` > `与` > `或`

## 三元条件运算符

- 详见[三元表达式](#三元表达式)


## 运算符优先级

- 各个语言的运算符优先级略有差异
- **技巧**：`()` 具有最高优先级，可以用 `()` 制造符合需求的优先级

# 控制结构

在编程语言中，控制结构用于决定程序的执行流程。主要的控制结构有以下几类：

-  顺序结构
-  选择结构
-  循环结构
-  跳转结构

控制结构可单独使用，也可嵌套使用。

## 顺序结构

顺序结构是默认的执行方式，代码逐行执行，每行代码执行一次。

## 选择结构

选择结构通过条件判断哪些代码执行，哪些不执行。选择结构又称分支结构或判断结构。

- `if`
- `switch`
- 三元表达式

### `if`

- **`if`**：相当于 `如果`，会先对条件表达式进行布尔值判断：
	- 如果结果为 `True`，则执行语句；
	- 如果结果为 `False`，则不执行语句。
- **`elif`**：相当于 `如果不是，那么如果`，即前面的条件不满足，运行另一个执行语句（某些语言写成 `else if`）。
- **`else`**：相当于 `否则`，即前面的条件都不满足时，运行行最后一个执行语句。

### `switch`

- `switch 语句` 类似于 `if-elif-else 语句`，但用于进行全等判断。

- `switch 语句` 在执行时，会依次将 `条件值` 和 `case值` 进行**全等比较**：

	- 如果结果为 `true`，则执行当前语句；
	- 如果结果为 `false`，则不执行语句；
	- 每个 `case` 后都应该有 `break`；
	- 最后的 `case` 后面应该有 `default`，相当于 `if-elif-else` 里的 `else`。

- **JavaScript 示例**

	```javascript
	switch (条件值) {
	  case 值1:
	    执行语句1;
	    break;
	  case 值2:
	    执行语句2;
	    break;
	  default:
	    执行语句3;
	}
	```

	```javascript
	let num = +prompt("请输入数字")
	switch (num) {
	  case 1:
	    console.log("壹");
	    break;
	  case 2:
	    console.log("贰");
	    break;
	  case 3:
	    console.log("叁");
	    break;
	  default:
	    console.log("没有这个数");
	    break;
	}
	```

### 三元表达式

- 三元表达式是一种简单的选择结构，在执行时，会先对条件表达式进行判断：

	- 如果结果为 `true`，则执行语句；
	- 如果结果为 `false`，则不执行语句。

- **JavaScript 示例**

	```javascript
	let money = +prompt("请输入你的存款：");
	console.log(money >= 100 ? "恭喜你！可以买宝马了！" : "继续上班！")
	```

## 循环结构

循环结构用于重复执行某些操作，直到满足特定的退出条件。

- `for`
- `while`
- `do-while`
- 无限循环

### `for`

#### `for` 语句

- 适用于循环次数已知或可以明确计算的场景。

- **语法**

	```javascript
	for (初始化变量; 条件表达式; 更新表达式){
	  循环体;
	}
	```

	**说明**：

	1. **初始化变量**：循环开始时执行一次，通常用于定义或初始化计数器变量。
	2. **条件表达式**：每次循环开始前都会判断，如果结果为 `true`，继续执行循环体；为 `false` 时退出循环。
	3. **更新表达式**：每次执行完循环体后，进行计数器的更新操作。

#### `for-in` 语句

- `for-in` 语句用于遍历对象的**属性键**；适用于。

- **语法**

	```javascript
	for (let 变量名 in 对象){
	  循环体;
	}
	```

- **说明**：如果（不推荐）使用 `for-in` 语句遍历字符串和数组，遍历到的是元素的索引号。（Python 除外）

#### `for-of` 语句

- `for-of` 语句用于遍历可迭代对象的**值**；适用于字符串、数组、集合、Map等。

- **语法**

	```javascript
	for (let 变量名 of 可迭代对象){
	  循环体;
	}
	```

### `while`

- `while` 循环通过判断条件表达式的布尔值，来控制循环体重复执行：

	- 如果结果为 `true`，则执行循环体；
	- 如果结果为 `false`，则循环结束。

- **语法**

	```javascript
	while (条件表达式){
	  循环体;
	}
	```

- **死循环**：如果 `while` 条件表达式永远为 `true`，且没有 `break` 进行终止，就形成了一个无限循环，也叫死循环。

### `do-while`

- `do-while` 与 `while` 的本质区别就是 `do-while` 先执行循环体，再检查条件；它保证无论条件是否成立，循环体至少执行一次。

- `do-while` 循环在执行时，会先执行循环体，再判断条件表达式的布尔值：

	- 如果结果为 `True`，则再执行循环体；
	- 如果结果为 `False`，则循环结束。

- **语法**

	```javascript
	do {
	  循环体
	} while (条件表达式);
	```

### 循环结构嵌套

- 当循环发生嵌套时，外层循环每执行一次，内层循环就会执行一个完整循环周期。

## 跳转结构

跳转结构用于在不同的代码块之间跳转，也称流程控制语句。

- **`continue`**：跳过本次循环的剩余部分，程序继续执行下一次该循环。
- **`break`**：用于跳出当前循环或 `switch` 语句，程序向下执行当前循环或 `switch` 语句以外内容。
- **`return`**：结束函数的执行并返回值。（Python 中的 [`try...except...finally`](../python/python.md#`try...except...finally`) 异常处理除外）
- **`goto`**：无条件跳转到程序的指定位置。

# 函数

**函数**是一段独立的、可重复使用的代码片段，用于封装操作，并实现功能复用。

## 函数组成

一般来说，函数包含以下几个部分：

- **函数名**（可选）：标识函数。
- **参数列表**（可选）：表示函数可以接收的输入。
- **函数体**：包含要执行的逻辑代码。
- **返回值**（可选）：函数执行后返回的结果。

### 函数名

函数名的巧用：函数名也是变量。

- **函数名重复**

	```python
	def func():
	    print(1)
	def func():
	    print(2)
	func()  # 2 执行最后一个func()
	```

- **函数名可用其它变量代替**

	```python
	def f():
	    print(123)
	f()  # 123
	
	f1 = f
	f1()  # 123 f1 = f, 故f1() = f()
	
	lst = [11, "中国联通", (11, 22), f, f()]
	lst[-2]()  # 123  user_list[-2]索引到函数名f，后面加()，整体作为函数名，相当于f()
	lst[-1]  # 123  user_list[-1]索引到函数名f()
	```

- **变量接收函数**

	```python
	def func():
	    print(123)
	    value = 999
	    return value
	
	res = func()  # 123  此时 res 等同于执行 func()
	print(res)  # 999  此时 res 接收 func() 的返回值 value
	```

- **for循环一次性调用多个函数**

	```python
	def send_sms():
	    print("发送短信")
	
	def send_email():
	    print("发送邮件")
	
	def send_dingding():
	    print("发送钉钉")
	
	def send_wechat():
	    print("发送微信")
	
	func_list = [send_sms, send_email, send_dingding, send_wechat]  # 注意此处元素为变量，没有引号
	
	for func in func_list:
	    func()  # 发送短信 发送邮件 发送钉钉 发送微信
	```

- **字典一次性调用多个函数**

	```python
	def register():
	    print("运行注册程序")
	
	def login():
	    print("运行登录程序")
	
	def user_info():
	    print("运行查看用户信息程序")
	
	# 将函数放入字典
	mapping = {
	    "1": register,
	    "2": login,
	    "3": user_info
	}
	
	print("1.注册")
	print("2.登录")
	print("3.查看用户信息")
	
	choice = input("请选择业务编号：")
	func = mapping.get(choice)  # func 将变为 register/login/user_info
	if func:
	    func()
	```

### 参数

- **形参**：函数定义时声明的参数，是一个占位符。
- **实参**：在函数调用时实际传递给函数的参数值，用以替换形参。
- 任意数据类型都可做实参；

#### 传参方式

- **位置传参**

	```py
	def func(x1, x2):
	    pass
	func(1, 2)  # 位置传参
	```

- **关键字传参**

	```python
	def func(x1, x2):
	    pass
	func(x1 = 1, x2 = 2)  # 关键字传参
	```

- **默认传参**：可传可默认

	```python
	def fun(x1, x2, x3 = 999):  # x3 = 999，默认传参
	    pass
	func (1, 2)  # 不传默认参数x3，x3默认等于999
	func (1, 2, x3 = 888)  # 传默认参数x3，x3等于888
	```

- **动态传参**

	- 动态传参：多个位置传参

	```python
	def func(*args):  # 在形参前面加*，可传多个参数
	    return args  # 返回参数
	
	res = func(45, "hj")  # 传两个参数
	print(res)  # (45, 'hj')  得到元组
	print(type(res))  # <class 'tuple'>
	
	res2 = func()  # 不传参数得到空元组
	print(res2)  # () 得到空元组
	print(type(res2))  # <class 'tuple'>
	```

	- 动态传参：关键字传参

	```python
	def func(**kwargs):  # 在形参前面加**，可传多个赋值参数
	    return kwargs  # 返回参数
	
	res = func(v1 = 1, v2 = 2)  # 传两个赋值参数
	print(res)  # {'v1': 1, 'v2': 2}  得到字典
	print(type(res))  # <class 'dict'>
	
	res2 = func()  # 不传参数
	print(res2)  # {}  得到空字典
	print(type(res2))  # <class 'dict'>
	```

	- 动态传参：位置和关键字混合传参

	```python
	def func(*args, **kwargs):  # 混合动态形参
	    return args, kwargs  # 返回参数
	
	res = func(11, 22, v1 = 1, v2 = 2)
	print(res)  # ((11, 22), {'v1': 1, 'v2': 2})  得到元组
	print(type(res))  # <class 'tuple'>
	print(res[0])  # (11, 22)  索引元组
	
	res2 = func()
	print(res2)  # ((), {})  不传参数得到以空元祖和空字典为元素的元组
	print(type(res2))  # <class 'tuple'>
	print(res2[0])  # ()  索引元组
	```

### 返回值

- **语法**

	- 返回值就是函数执行后返回的结果；
	- 函数内部遇到 `return`，函数立即终止；
	
- **基础示例**

	```python
	def get_sum(a, b):
	    result = a + b
	    return result  # 函数的输出结果返回result，函数停止
	    print("求和：", result)  # 由于前面有return，所以此行代码不执行
	
	res = get_sum(4, 5)  # 调用函数并接收返回值
	print(res)  # 9
	```

- **多个返回值示例**

	```python
	def func2():
	    a = 11
	    b = 22
	    c = 33
	    return a, b, c
	
	r1, r2, r3 = func2()  # 把返回值分别赋值给r1, r2, r3
	print(r1, r2, r3)  # 11 22 33
	print(r1)  # 11
	r4 = func2()  # 把返回值赋值给r4，并放入一个元组中
	print(r4)  # (11 22 33)
	print(type(r4))  # <class 'tuple'>
	```

## 创建函数

## 函数类型

### 内置函数

### 自定义函数

### 普通函数

### 构造函数

- 构造函数是一种特殊的函数，主要用于创建和初始化对象。构造函数可以理解为对象的 “模板”。

	```javascript
	function Person(name, age) {
		this.name = name;
		this.age = age;
	}
	
	let person1 = new Person('张三', 20);
	let person2 = new Person('李四', 22);
	```

	在上述代码中，`Person` 就是构造函数。使用 `new` 关键字调用构造函数时，它会创建一个新对象，将函数内的 `this` 指向新对象，并执行函数体中的代码来初始化对象的属性。

### 匿名函数

### 生成器函数

**生成器**是一种特殊的函数，它可以暂停执行并在需要的时候恢复执行，通过 `yield` 关键字来实现暂停功能，避免一次性在内存中创建过多数据。

- **基础示例**

	```python
	def func():
	    print(456)
	    yield "abc"
	    print(789)
	    yield "def"
	    yield "ghi"
	
	func()  # 什么也没有
	obj = func()  # 返回一个生成器对象
	# 生成器对象.__next__()
	v1 = obj.__next__()  # 456  执行yield之前的函数，一旦遇到yield, v1 = yield
	print(v1)  # abc
	
	v2 = obj.__next__()  # 789  继续执行函数，一旦遇到下一个yield, v2 = yield
	print(v2)  # def
	
	v3 = obj.__next__()  # 继续执行函数，一旦遇到下一个yield, v3 = yield
	print(v3)  # ghi
	```

- **简洁示例**

	```python
	def func():
	    yield "abc"
	    yield "def"
	    yield "ghi"
	
	obj = func()  # 返回一个生成器对象
	for item in obj:
	print(item)  # 依次打印abc def ghi
	```

- **应用场景**

	```python
	def func(limit):
	    num = 0
	    while num < limit:
	        yield num
	        num += 1
	
	obj = func(1000)
	for item in obj:
	    print(item)
	```

### 递归函数

## 装饰器

- 装饰器

	- 应用：自定义一个新功能，在不修改源函数内部代码的前提下，可以在源函数执行前后扩展自定义功能。
	- 把 `func()` 的函数名作为 `a` 传给 `outer()`，把 `inner()` 的函数名作为返回值，赋给 `func` 的函数名。
	
	```python
	def outer(a):
	    def inner():
	        print("before")  # 扩展功能
	        res = a()  # res接收func()的返回值
	        print("after")  # 扩展功能
	        return res  # 以res作为inner()的返回值，为后续v1做准备
	    return inner
	@outer  # a = func  func() = inner()
	def func():  # 源函数
	    print(123)
	    return 999
	
	v1 = func()  # 依次打印before 123 after
	# 此处的func()实际就是inner()，用v1接收inner()的返回值
	
	print(v1)  # 999
	# 结果：func()在inner()内执行，执行前后添加其它操作
	```

## 推导器

### 列表推导式

- 用于快速从现有列表生成新列表。
- **语法**

  - `a` 为要输出的内容/与i有关的内容
  - `for` 语句后面也可加 `if` 条件

  ```python
  lst = ["a" for i in range(1, 51)]
  print(lst)  # 生成一个含有50个a的列表
  ```

- **示例**

  ```python
  lst = ["用户_{}".format(i) for i in range(1, 51) if i > 10]
  print(lst)  # [用户_11, 用户12, … , 用户50]
  ```

### 字典推导式

- 格式

	```python
	info = {i: 123 for i in range(10) if i > 5}
	print(info)  # {6: 123, 7: 123, 8: 123, 9: 123}
	```

- 示例

	- 将字典写成key1=v2&key2=v2字符串模式，并将key排序

	```python
	dict = {
	    'sign_type': 'MD5',
	    'refund': '123',
	    'app_id': 'wx55',
	    'mch_id': '15260',
	    'trade': 'ff'
	}
	
	result = "&".join(["{}={}".format(key, dict[key]) for key in sorted(dict.keys())])
	print(result)  # app_id=wx55&mch_id=15260&refund=123&sign_type=MD5&trade=ff
	```

	- 将字符串写成字典

	```python
	dict_string = "name=武沛齐&email=xxx@163.com&gender=男"
	result = {
	    data.split('=')[0]: data.split('=')[1] for data in dict_string.split('&')
	}
	print(result)  # {'name': '武沛齐', 'email': 'xxx@163.com', 'gender': '男'}
	```

# 对象

- 字面量方式
- 构造函数方式
- 面向对象方式
- 工厂函数方式：将对象创建过程封装在一个函数中，如果需要创建多个相似的对象，只需调用该函数即可。

# 面向对象

**面向对象**（Object Oriented）是软件开发方法，一种编程范式，面向对象是相对于面向过程来讲的。面向对象方法，把相关的数据属性和方法组织为一个整体来看待，从更高的层次来进行系统建模，更贴近事物的自然运行模式。

## 类

从通用编程语言的角度来看，**类（Class）** 是面向对象编程（OOP）中的一个核心概念，它定义了一个对象的模板，描述了对象的**属性**（数据）和**方法**（行为）。类将数据和操作数据的方法封装在一起，是程序的基本构建块。

### **类的基本定义**

**类** 是 **对象** 的模板。它包含：

- **属性（或字段）**：描述类的状态或特征，通常以变量形式存在。
- **方法（或函数）**：描述类的行为，通常以函数形式存在。

###  类的特性

#### 封装

- **封装（Encapsulation）**：类将数据和方法封装在一起，外部无法直接访问对象的内部状态，必须通过方法来操作数据。

#### 继承

- **继承（Inheritance）**：子类可以继承父类的属性和方法，从而重用代码，并且可以在子类中重写父类的方法。

	```python
	class Animal:
	    def speak(self):
	        print("Animal makes a sound.")
	
	class Dog(Animal):
	    def speak(self):
	        print("Dog barks.")
	
	dog = Dog()
	dog.speak()  # 输出：Dog barks.
	```

#### 多态

- **多态（Polymorphism）**：允许同一个方法名表现出不同的行为。多态使得子类可以替换父类实现的方法。

	```python
	class Animal:
	    def speak(self):
	        print("Animal makes a sound.")
	
	class Dog(Animal):
	    def speak(self):
	        print("Dog barks.")
	
	class Cat(Animal):
	    def speak(self):
	        print("Cat meows.")
	
	animals = [Dog(), Cat()]
	for animal in animals:
	    animal.speak()  # 输出：Dog barks.  Cat meows.
	```

## 对象

在通用编程语言的语境下，**对象** 是面向对象编程（Object-Oriented Programming, OOP）的核心概念之一，是类的实体。对象抽象了现实世界中的事物，既可以存储数据（属性/状态），也可以定义操作数据的行为（方法）。

### **对象的基本定义**

**对象** 是 **类** 的实例。它包含：

- **属性（Attributes）**：描述对象状态的数据，通常以变量形式存在。
- **方法（Methods）**：描述对象行为的功能，通常以函数形式存在。

在现实中，**对象** 就是对事物的抽象建模：

- 现实中的事物 → **编程中的对象**
- 事物的特征 → **对象的属性**
- 事物的行为 → **对象的方法**

### 对象的特性

#### 封装

- **封装（Encapsulation）**：对象将属性和方法封装在一起，对外提供特定的接口，隐藏内部实现细节。

	```python
	class Dog:
	    def __init__(self, name, age):
	        self.name = name  # 属性
	        self.age = age
	
	    def bark(self):       # 方法
	        print(f"{self.name} is barking!")
	
	dog = Dog("Buddy", 3)
	dog.bark()  # 输出：Buddy is barking!
	```

#### 继承

- **继承（Inheritance）**：对象可以通过继承从其他对象获得属性和方法，从而实现代码重用和扩展。

	```python
	class Animal:
	    def eat(self):
	        print("This animal eats food.")
	
	class Dog(Animal):  # Dog 继承自 Animal
	    def bark(self):
	        print("Dog barks!")
	
	dog = Dog()
	dog.eat()  # 输出：This animal eats food.
	dog.bark() # 输出：Dog barks!
	```

#### 多态

- **多态（Polymorphism）**：不同的对象可以通过相同的接口表现出不同的行为。

	```python
	class Cat:
	    def sound(self):
	        print("Meow")
	
	class Dog:
	    def sound(self):
	        print("Bark")
	
	def make_sound(animal):
	    animal.sound()
	
	make_sound(Cat())  # 输出：Meow
	make_sound(Dog())  # 输出：Bark
	
	```

#### 动态性

- **动态性（Dynamic Behavior）**：对象的属性和方法可以在运行时动态添加、修改或删除（在动态语言中更为常见，如 Python）。

	```python
	class Empty:
	    pass
	
	obj = Empty()
	obj.name = "Dynamic Object"  # 动态添加属性
	print(obj.name)  # 输出：Dynamic Object
	```

###  对象的生命周期

对象的生命周期包括以下阶段：

1. **创建（Creation）**：通过类实例化对象。
2. **使用（Usage）**：通过访问属性或调用方法使用对象。
3. **销毁（Destruction）**：当对象不再被引用时，内存会被释放（例如 Python 中的垃圾回收）。

### 对象与类的关系

- **类（Class）**：定义对象的模板，规定对象的属性和方法。
- **对象（Object）**：类的具体实例，拥有类的属性和方法。

## 面向对象三大特性

### 类的封装

- 封装

	```
	- 封装就是把对象的某个属性，只能通过类内部的方法访问，而不能从外部直接调用。
	- 方法：在定义类属性时，把“self.属性”改成“self.__属性”，然后把该属性的操作创建到一个方法内。
	```

- 将数据封装到对象

	```python
	class Foo:
	    def __init__(self, name, age):
	        self.name = name
	        self.age = age
	obj = Foo("Jerry", 30)
	```

- 将同一类方法封装到类

	```py
	class Message:
	    def email(self):
	        pass
	    def wechat(self):
	        pass
	    def sms(self):
	        pass
	
	class FileHandler:
	    def txt(self):
	        pass
	    def excel(self):
	        pass
	    def word(self):
	        pass
	```

### 类的继承

- 子类自动拥有父类的属性和方法。

- 语法

	```python
	class Base:
	    def func1(self):
	        pass
	
	class Son(Base):
	    def func2(self):
	        pass
	
	obj = Son()  # 创建子类对象
	obj.func1()  # 子类自动拥有父类的属性和方法
	```

	```
	- 子类必须自动拥有父类属性和方法，但父类不拥有子类的属性和方法。
	- 当子类和父类拥有相同属性和方法时，子类只调用自己，而不调用父类。
	- 创建子类对象时，要填写父类的各个属性。
	- 在python中，一个父类可以有多个子类，一个子类也可以有多个父类。
	- 所有类的最终父类是object，如果不填写父类，系统默认为父类就是object。
	```

### 类的多态

​	支持传入多种类型参数

# 模版语法

## 模板语法基础

- **模版语法**：是一种将后端逻辑嵌入到模板文件中（如 HTML ）的规则，用于在模版文件动态显示从后端视图函数传递过来的变量值。

- **模板引擎**：是一种软件工具，用于将数据与模板（通常是文本格式，如 HTML）结合起来，生成最终的文档。
	- 模板引擎首先会解析模板文件，识别其中的模板语法。
	- 后端程序将数据传递给模板引擎，模板引擎会根据模板语法将数据绑定到模板中的相应位置。
	- 在完成数据绑定后，模板引擎会生成最终的输出文档，通常是一个完整的 HTML 页面。
	- **常用引擎**：Jinja2 模板引擎，Django 模板引擎等。
- **缩进**：模板语法和 HTML 元素之间的缩进不是必须的，但为了代码的可读性，建议使用缩进，而且此缩进会被编辑器代码格式化功能破坏掉。
- **标识**
	- `{% 逻辑语句 %}`
	- `{{ 变量 }}`

## 模板语法示例

- Flask 框架使用模板语法示例

- `app.py`

	```python
	from flask import Flask, render_template, session
	
	app = Flask(__name__)
	app.config['SECRET_KEY'] = 'your_secret_key'  
	
	@app.route('/')
	def index():
	    # 模拟用户登录状态和用户姓名
	    session['logged_in'] = True
	    session['user_name'] = '张三'
	    return render_template('index.html', user_name=session['user_name'])
	
	if __name__ == '__main__':
	    app.run(debug=True)
	```

- `templates/index.html`

	```html
	<body>
	  {% if session.logged_in %}
	    <h1>欢迎，{{ user_name }}！</h1>
	    <p>您正在浏览我们的专属页面内容。</p>
	  {% else %}
	    <h1>欢迎，访客！</h1>
	    <p>请登录以获取更多功能和专属内容。</p>
	  {% endif %}
	</body>
	```

	
