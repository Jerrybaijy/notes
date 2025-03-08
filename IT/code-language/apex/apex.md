Apex is a **strongly-typed**, **object-oriented** programming language developed by Salesforce for building applications on the Salesforce platform. It is similar to Java and C# in syntax.

The key features of Apex:

- **Hosted**: Apex is saved, compiled, and executed on the server—the Lightning Platform.
- **Object oriented**: Apex supports classes, interfaces, and inheritance.
- **Strongly typed**: Apex validates references to objects at compile time.

Apex 是 Salesforce 提供的一种**强类型**、**面向对象**编程语言，专门用于在 Salesforce 平台 上进行后端逻辑开发，它的语法类似于 Java。

# Apex 基础

## 运行环境

- **Developer Console**: **Quick access menu (![Setup gear icon](assets/e0d3e5a9b64c98ba5ac2c14623e36609_kix.zbyh4h1n9tpc.jpeg))** | **Developer Console**
- **IDE**

## 代码规范

- 同编程语言通用规范

## 标识符

- 同编程语言通用规范

## 注释

- **单行注释**：Ctrl + /    **多行注释**：Ctrl + Shift + /

    ```java
    public class HelloWorld {
        // 这是一个单行注释
        public static void main(String[] args) {
            /*
             * 多行注释第一行
             * 多行注释第二行
             * 多行注释第三行
             */
            System.debug('Hello World'); 
        }
    }
    ```

- **文档注释**

    文档注释以 **/\**** 开始，以 ***/** 结束，通常出现在类、方法、字段等的声明前面，通常包含一些特定的标签，如 **@param** 用于描述方法参数，**@return** 用于描述返回值，**@throws** 用于描述可能抛出的异常等等。文档注释的格式这些标签有助于生成清晰的API文档，以便其他开发者能够更好地理解和使用你的代码。

    ```java
    /**
     * 这是一个文档注释示例
     * 它通常包含有关类、方法或字段的详细信息
     */
    public class MyClass {
        // 类的成员和方法
    }
    ```

## 声明变量

- **声明基本类型变量**

    ```java
    数据类型 变量名 = 初始值;
    ```

    ```java
    Integer myInteger = 10;  // 声明一个整数并赋初值
    ```

- **声明数组类型变量**

    ```java
    String[] colors = new List<String>();
    ```

- **声明集合类型变量**

    ```java
    集合类型<数据类型> 变量名 = new 集合类型<数据类型>();
    ```

    ```java
    List<String> myList = new List<String>();   // 声明一个 String 类型的列表
    Set<Integer> mySet = new Set<Integer>();    // 声明一个 Integer 类型的集合
    Map<String, Integer> myMap = new Map<String, Integer>(); // 声明一个 Map，键为 String，值Integer
    ```

- **声明自定义对象类型变量**

    ```java
    对象类型 变量名 = new 对象类型(字段 = 字段的值);
    ```

    ```java
    Account myAccount = new Account(Name = 'Acme Corp');  // 声明一个 Account 对象并初始化
    ```

## 输入与输出

- **输出**

    ```java
    System.debug('这是要输出的信息');
    ```

# 数据类型

在 Apex 中，数据类型可以分为两大类：

- **原始数据类型**（Primitive Data Types）
- **引用数据类型**（Reference Data Types）

## 原始数据类型

Apex 中有10种原始数据类型。

### 整数类型

- **`Integer`**：32 位有符号整数，取值范围：-2^31 到 2^31 - 1（大约 -21 亿 到 21 亿）。

- **`Long`**：64 位有符号整数，适用于大数字。

- **`Decimal`**：用于高精度计算，常用于处理货币和财务数据。

### 浮点数类型

- **`Double`**：64 位双精度浮点数，适用于存储较大的浮动数值。

### 字符类型

- **`Char`**：用于存储单个字符，只有一个字符的 Unicode 编码。
- 使用单引号 `'` 标记字符。

### 字符串类型

- **`String`**：用于存储一串字符，类似于 Java 中的 `String` 类型。
- Apex 中使用单引号 `'` 标记字符串。

### 布尔类型

- **`Boolean`**：用于表示逻辑值，可以是 `true` 或 `false`。

### 日期和时间类型

- **`Date`**：只包含日期（年月日）。

- **`Datetime`**：包含日期和时间（年月日 时分秒）。

### ID 类型

- **`ID`**：用于存储 Salesforce 中的记录的唯一标识符，例如 `Account`、`Contact`、`Opportunity` 等对象的记录 ID。

## 引用数据类型

引用数据类型是指存储对象的引用而不是数据本身。Apex 的引用数据类型包括类、接口、数组、集合以及 Salesforce 特有的 SObject 类型。

### SObject 类型

`SObject` 类型代表 Salesforce 数据模型中的记录，例如 `Account`、`Contact` 等。你可以使用 `SObject` 类型来存储 Salesforce 对象的数据。

### 数组类型

数组用于存储一组不同类型的元素。Apex 中的数组可以存储对象、基本数据类型等。

### 集合类型

Apex 中的集合类型包括 **`List`**、**`Set`** 和 **`Map`**。这些集合类型用于存储多个数据项。

- **`List`**：有序集合，允许存储重复元素。
- **`Set`**：无序集合，不允许重复元素。
- **`Map`**：键值对集合，通过键来快速查找值。

### 类和对象

Apex 支持面向对象编程，可以创建类并实例化对象。

### 接口类型

Apex 支持接口（`interface`），可以定义一些方法，然后让类去实现这些方法。

### 枚举类型

Apex 支持枚举（`enum`），枚举用于表示一组常量。

# 选择结构

Apex 中有 `if`、`switch` 和 `三元表达式` 三种选择结构。

## if 语句

### if

- **语法**

    ```javascript
    if (条件表达式) {
        执行语句;
    }
    ```

    ```javascript
    Integer score = 85;
    
    if (score >= 60) {
        System.debug('及格！');
    }
    ```

### if-else

- **语法**

    ```javascript
    if (条件表达式) {
        执行语句A;
    } else {
        执行语句B;
    }
    ```

    ```javascript
    Integer score = 85;
    
    if (score >= 60) {
        System.debug('及格！');
    } else {
        System.debug('不及格！');
    }
    ```

### if-else if-else

- **语法**

    ```javascript
    if (条件表达式1) {
        执行语句A;
    } else if (条件表达式2) {
        执行语句B;
    } else if (条件表达式3) {
        执行语句c;
    } else {
        执行语句D;
    }
    ```

    ```javascript
    Integer score = 85;
    
    if (score >= 90) {
        System.debug('优秀！');
    } else if (score >= 80) {
        System.debug('良好！');
    } else if (score >= 60) {
        System.debug('及格！');
    } else {
        System.debug('不及格！');
    }
    ```

## switch 语句

### 基本语法

- Apex 的 `switch` 语句类似于 Java，但语法稍有不同。
    - Apex 使用 `switch on` 进行变量匹配.
    - Apex 使用 `when` 关键字代替 Java 的 `case`。
    - Apex 的 `switch` 不会发生 Java 中的 Fall-through（贯穿），每个 `when` 代码块都是独立的，不需要 `break`。
    - Apex 使用 `when else` 关键字代替 Java 的 `default`。

- **语法**

    ```java
    switch on 条件值 {
        when 值1 {
            // 执行代码
        }
        when 值2 {
            // 执行代码
        }
        when else {
            // 处理默认情况（类似 Java 的 default）
        }
    }
    ```

    ```java
    String status = 'Processing';
    
    switch on status {
        when 'New' {
            System.debug('订单是新的');
        }
        when 'Processing' {
            System.debug('订单正在处理中');
        }
        when 'Completed' {
            System.debug('订单已完成');
        }
        when else {
            System.debug('未知订单状态');
        }
    }
    ```

- **多值匹配**

    ```java
    Integer day = 6;
    
    switch on day {
        when 1, 2, 3, 4, 5 {
            System.debug('工作日');
        }
        when 6, 7 {
            System.debug('周末');
        }
        when else {
            System.debug('未知');
        }
    }
    ```

## 三元表达式

- Apex 的三元表达式语法和 Java 相同，但 **适用范围** 和 **类型推导** 上有一些不同。

- **语法**

    ```java
    条件表达式 ? 真值 : 假值
    ```

    ```java
    Integer score = 85;
    String result = (score >= 60) ? '及格' : '不及格';
    System.debug(result);  // 输出：及格
    ```

# 循环结构

- Apex 中有 `for` 、`for-each`、`while`  和 `do-while` 四种循环结构，用法同 Java。
- Apex 中支持**无限循环**和**循环嵌套**，用法同 Java。

# 跳转结构

- Apex 中有 `continue`、`break`、`return`、`throw`、`throws` 五种跳转结构，用法同 Java。
