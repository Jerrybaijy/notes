---
title: java
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - code-language
  - backend
---

# Java

>  [Java 官方文档](https://dev.java/learn/)

## 环境搭建

### JDK

JDK（Java Development Kit）是一个用于开发 Java 应用程序的工具包。它包含了**Java 编译器（javac）**、**Java 虚拟机（JVM）**、**Java 运行时环境（JRE）**和 **其他工具和类库** 等。

#### Windows

- [官网下载并安装 JDK x64 Installer](https://www.oracle.com/java/technologies/downloads/#jdk21-windows)

#### Linux

- 使用 apt 安装

  ```bash
  sudo apt update
  sudo apt install openjdk-21-jdk
  java -version
  ```

### Eclipse

Eclipse 是一款 IDE，主要用于 Java 开发。

#### Eclipse 安装

- 确认 Java 开发工具包 JDK 已安装
- 下载 Eclipse IDE for Enterprise Java and Web Developers
- 解压到 D 盘，双击 ecplise.exe
- 配置工作空间，即存项目的文件夹
- 创建项目：new→java protect→ 填写项目名称、选择运行环境
- 创建包：src 右键 →new→Package（包名使用域名倒置，例：com.unit1.test）
- 创建 class：包右键 →new→class（类名首字母大写）

### IntelliJ IDEA

IntelliJ IDEA 是一款 IDE，主要用于 Java 开发。

#### IntelliJ IDEA 安装

- 安装时选择 `添加环境变量` 和 `关联Java`
- 破解教程见 [`Python` > `Pycharm`](../python/python.md#Pycharm)

#### IntelliJ IDEA 配置

### VS Code

- 确认 Java 开发工具包 **JDK** 已安装
- VS Code 已安装，扩展 **Extension Pack for Java** 已安装
- **Ctrl + Shift + P** 打开命令面板 | 输入 `Java: Create Java Project` | **Enter** | 选择 **No build tools** | 选择项目目录 | 输入**项目名称** | **Enter**

## 代码规范

- 除以下规范，其余同编程语言通用规范。
- **主方法入口**：所有的 Java 程序由 **public static void main(String[] args)** 方法开始执行。

## 标识符

- 除以下规范，其余同编程语言通用规范。
- **源文件名**：源文件名必须和类名相同。

## 注释

- **单行注释**：Ctrl + / **多行注释**：Ctrl + Shift + /

  ```java
  /**
   * 这是一个文档注释示例。
   * 它通常包含有关类、方法或字段的详细信息。
   * 例如，描述类的作用或方法的功能。
   */
  public class HelloWorld {
  
      // 这是一个单行注释，描述下面的方法。
      public static void main(String[] args) {
  
          /*
           * 多行注释第一行
           * 多行注释第二行
           * 多行注释第三行
           * 这里是对下面的输出代码块的解释。
           */
  
          System.out.println("Hello World");
      }
  }
  ```

## 声明变量

- 在 Java 中，声明变量时要指定相应的**数据类型**。

  ```java
  // 声明原始数据类型的变量时，不使用 new 关键字。
  int age = 19;
  
  // 声明非原始数据类型的变量时，使用 new 关键字。
  List<String> myList = new ArrayList<>();
  ```

## 运算符

- **算术运算符**
  - 没有幂次方 `**`
- **赋值运算符**
- **关系运算符**
- **逻辑运算符**

  - 与 `&&`、或 `||`、非 `!`

## 输入与输出

- **输入**

  ```java
  package com.unit1.test;

  import java.util.Scanner;// 引入内部类Scanner

  public class Test {
      public static void main(String[] args) {
          Scanner input = new Scanner(System.in);// 同一个java类文件，只需创建一次

          System.out.println("请输入你的年龄：");// 提示
          int a = input.nextInt();// 用户输入一个int类型数据，并使用a接收
          System.out.println("你的年龄：" + age);// 返回结果
      }
  }
  ```

- **输出**

  ```java
  System.out.println("这是要输出的信息");
  ```

## Maven

Maven 是一个用于构建和管理 Java 项目的工具

### 安装

#### Windows

- [官网下载 Maven 二进制 zip 归档文件：apache-maven-3.9.6-bin.zip](https://maven.apache.org/download.cgi)
- 解压到自己的安装目录，如 D:\Program Files (x86)\apache-maven-3.9.6
- 设置系统环境变量，如 D:\Program Files (x86)\apache-maven-3.9.6\apache-maven-3.9.6\bin

### 命令

- 命令

  ```bash
  # 构建项目
  mvn clean package -DskipTests
  ```

# 数据类型

Java 是一种静态类型语言，在声明变量时，必须先指定其数据类型。

## 数据类型分类

- [Primitive Data Types (8)](https://dev.java/learn/language-basics/primitive-types/)

  - **整型**：byte，short，int，long
  - **浮点型**：float，double
  - **布尔型**：boolean
  - **字符型**：char

- **引用数据类型**

  - **类**：class
  - **接口**：interface
  - **数组**：array
  - **枚举**：enum
  - **字符串**：String
  - **包装类**
  - ...

## char

- **char**：16 位无符号整数，用于表示单个字符，采用 Unicode 编码，能表示世界上大部分语言的字符，值用单引号括起来。
- 使用单引号 `'` 标记字符。

## boolean

- **boolean**：只有两个取值 `true` 和 `false`，用于表示逻辑上的真和假，常用于条件判断和循环控制。

## enum

- 枚举是一种特殊的数据类型，用于定义一组固定的常量。

## 数据类型转换

- 虽然 Java 是**强类型**语言，但支持 `字符串 + 数值` 的隐式跨类型操作。

  ```java
  System.out.println("hello" + 5); // 输出：hello5
  ```

### 隐式转换

- **语法**

  ```
  byte → short → int → long → float → double
           ↑
         char
  ```

  ```java
  int a = 10;
  double b = a;  // int 自动转换为 double
  System.out.println(b);  // 输出：10.0
  
  char ch = 'A';
  int c = ch;  // char 自动转换为 int（ASCII 值）
  System.out.println(c);  // 输出：65
  
  long l = a;  // int 自动转换为 long
  System.out.println(l);  // 输出：10
  ```

### 显式转换

- **语法**

  ```java
  targetType variable = (targetType) sourceVariable;
  ```

  ```java
  (int)data;
  ```

  ```java
  double a = 10.5;
  int b = (int) a;  // 强制类型转换，丢失小数部分
  System.out.println(b);  // 输出：10
  
  int c = 130;
  byte d = (byte) c;  // 溢出，byte 取值范围 -128~127
  System.out.println(d);  // 输出：-126 (超出范围，数据溢出)
  
  char ch = (char) 66;
  System.out.println(ch);  // 输出：B
  ```

### 字符串与基本数据类型

- 字符串 → 基本数据类型：使用 Java 提供的包装类的 `parseXxx()` 方法

  ```java
  String s1 = "100";
  Double a = Double.parseDouble(s1);
  System.out.println(a);  // 100.0
  ```

- 基本数据类型 → 字符串：使用 `String.valueOf()` 或直接拼接：

  ```java
  int a = 100;
  String s1 = String.valueOf(a);
  String s2 = a + "";  // 拼接方式
  
  System.out.println(s1);  // "100"
  System.out.println(s2);  // "100"
  ```

## 数据的可变性

- **不可变数据类型**

  - Java 的 基本数据类型是不可变的。
  - 字符串
  - ...

- **可变数据类型**

  - ...

# 选择结构

Java 中有 `if`、`switch` 和 `三元表达式` 三种选择结构。

## if 语句

### if

```java
if (条件表达式) {
    // 执行语句;
}
```

```java
int score = 85;

if (score >= 60) {
    System.out.println("及格！");
}
```

### if-else

```java
if (条件表达式) {
    // 执行语句A;
} else {
    // 执行语句B;
}
```

```java
int score = 85;

if (score >= 60) {
    System.out.println("及格！");
} else {
    System.out.println("不及格！");
}
```

### if-else if-else

```java
if (条件表达式1) {
    // 执行语句A;
} else if (条件表达式2) {
    // 执行语句B;
} else if (条件表达式3) {
   // 执行语句C;
} else {
    // 执行语句D;
}
```

```java
int score = 85;

if (score >= 90) {
    System.out.println("优秀！");
} else if (score >= 80) {
    System.out.println("良好！");
} else if (score >= 60) {
    System.out.println("及格！");
} else {
    System.out.println("不及格！");
```

## switch 语句

### 语法

```java
switch (条件值) {
    case 值1:
        // 执行语句1;
        break;
    case 值2:
        // 执行语句2;
        break;
    default:
        // 执行语句3;
}
```

```java
String status = "Processing";

switch (status) {
    case "New":
        System.out.println("订单是新的");
        break;
    case "Processing":
        System.out.println("订单正在处理中");
        break;
    case "Completed":
        System.out.println("订单已完成");
        break;
    default:
        System.out.println("未知订单状态");
}
```

### 多值匹配

```java
int day = 6;

switch (day) {
    case 1, 2, 3, 4, 5:
        System.out.println("工作日");
        break;
    case 6, 7:
        System.out.println("周末");
        break;
    default:
        System.out.println("未知");
}
```

## 三元表达式

```java
条件表达式 ? 真值 : 假值
```

```java
Integer score = 80;
String result = score >= 60 ? "及格" : "不及格";
System.out.println(result);  // 及格
```

# 循环结构

Java 中有 `for` 、`for-each`、`while` 和 `do-while` 四种循环结构。

## for 语句

```java
for (初始化表达式; 条件表达式; 更新表达式){
    // 循环体;
}
```

```java
for (int i = 0; i <= 5; i++) {
    System.out.println(i);  // 依次输出：0 1 2 3 4 5
}
```

**扩展**：可用“for 循环 + 索引”进行遍历

```java
String[] arr = {"中国", "上海", "北京" };
for (int i = 0; i < arr.length; i++) {
    System.out.println(arr[i]);  // 中国 上海 北京
}
```

## for-each 语句

for-each 循环用于直接遍历

```java
for (数据类型 变量名 : 数组或集合){
    // 循环体;
}
```

```java
String[] arr = { "中国", "上海", "北京" };
for (String data : arr) {
    System.out.println(data); // 中国 上海 北京
}
```

## while 语句

```java
while (条件表达式){
    // 循环体;
}
```

```java
public class HelloWorld {
    public static void main(String[] args) {
        int i = 1;
        while (i <= 3) {
            System.out.println("第" + i + "次打印：Hello World!");
            i += 1;  // 条件迭代
        }
    }
}
```

## do-while 语句

```java
do {
    // 循环体;
} while (条件表达式);
```

```java
public class HelloWorld {
    public static void main(String[] args) {
        int i = 1;
        do {
            System.out.println("第" + i + "次打印：Hello World!");
            i += 1;  // 条件迭代
        } while (i <= 3);
    }
}
```

## 无限循环

```java
while (true) {
    // 循环体;
}
```

```java
do {
    // 循环体;
} while (true);
```

```java
for (;;){
    // 循环体;
}
```

## 循环结构嵌套

- **示例**

  ```java
  public class LoanRepayment {
      public static void main(String[] args) {
          for (int year = 1; year <= 10; year++) {
              System.out.println("第" + year + "年到了！");
              for (int month = 1; month <= 12; month++) {
                  System.out.println("第" + year + "年，第" + month + "月，还款1000元！");
              }
          }
      }
  }
  ```

- **遍历多维容器**

  ```java
  import java.util.ArrayList;
  import java.util.Arrays;
  import java.util.List;
  
  public class NestedArrays {
      public static void main(String[] args) {
          // 创建各个数组
          List<Integer> arr1 = Arrays.asList(1, 213, 13, 232, 3, 43, 3, 3);
          List<Integer> arr2 = Arrays.asList(21, 13, 243, 4, 54, 6);
          List<Integer> arr3 = Arrays.asList(23, 545, 465, 65, 6565, 76);
  
          // 创建包含这些数组的二维 List
          List<List<Integer>> arr4 = new ArrayList<>();
          arr4.add(arr1);
          arr4.add(arr2);
          arr4.add(arr3);
  
          // 遍历 arr4 中的每个 List
          for (List<Integer> arrx : arr4) {
              // 遍历每个 List 中的元素
              for (int a : arrx) {
                  System.out.println(a);  // 输出各个值
              }
          }
      }
  }
  ```

# 跳转结构

Java 中有 `continue`、`break`、`return`、`throw`、`throws` 五种跳转结构。

**`continue` 和 `break` 示例**：

```java
public class LoanRepayment {
    public static void main(String[] args) {
        for (int year = 1; year < 11; year++) {
            if (year == 5) {
                System.out.println("第5年疫情原因，今年不用还款了！");
                // 此处如果没有 continue，会同时正常显示：第五年到了，还款1.2万。
                continue;  // 第5年不用还，本次循环结束，进入下一次该循环，第6年。
            }
            if (year == 6) {
                System.out.println("第" + year + "年到了！还款2.4万！");
                continue;  // 第6年还2.4万，本次循环结束，进入下一次该循环，第7年。
            }
            if (year == 8) {
                System.out.println("第8年，提前还清，以后都不用还了！");
                break;  // 从第9年不用再还款了，当前循环结束。
            }
            System.out.println("第" + year + "年到了！还款1.2万！");
        }
    }
}
```

`return`：详见[返回值](#返回值)。

# [Array](https://dev.java/learn/language-basics/arrays/)

## 声明数组

**动态初始化：**

```java
数据类型[] 变量名 = new 数据类型[数组长度];
```

```java
// 初始化
int[] myArray = new int[5];

// 赋值
myArray[0] = 1;
myArray[1] = 2;
myArray[2] = 3;
myArray[3] = 4;
myArray[4] = 5;
```

**静态初始化：**

```java
数据类型[] 变量名 = {元素1, 元素2, 元素3...};
```

```java
int[] myArray = {1, 2, 3, 4, 5};
```

## [数组方法](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/Arrays.html)

- 索引，获取元素，修改元素，遍历，获取长度，多维数组

### 获取元素

```java
String[] address = {"北京", "上海", "广州", "深圳", "杭州"};
System.out.println(address[0]); // 北京
```

### 修改元素

```java
String[] address = { "北京", "上海", "广州", "深圳", "杭州" };
System.out.println(address[0]); // 北京
address[0] = "西安"; // 修改索引号为 0 的元素
System.out.println(address[0]); // 西安
```

### 遍历数组

**for-each 思想遍历：**

```java
String[] address = { "北京", "上海", "广州", "深圳", "杭州" };
for (String city : address) {
    System.out.println(city); // 依次输出每个城市
}
```

**索引思想遍历：**

```java
String[] address = { "北京", "上海", "广州", "深圳", "杭州" };
for (int i = 0; i < address.length; i++) {
    System.out.println(address[i]); // 依次输出每个城市
}
```

### 获取长度

```java
String[] address = { "北京", "上海", "广州", "深圳", "杭州" };
int length = address.length; // 数组的长度
System.out.println(length); // 5
```

### 多维数组

```java
String[][] addressArray = {
    { "北京", "上海", "广州" },
    { "深圳", "杭州" }
};
System.out.println(addressArray[0][0]); // 北京
```

# [String](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/lang/String.html)

- 在 Java 里，字符串是 `java.lang.String` 类的实例，属于不可变类型，它具有原始数据类型的特质。

## 声明字符串

在 Java 中，`String` 类用于表示字符串，创建字符串主要有以下两种方式：

**直接使用字符串字面量：**

```java
String str1 = "Hello, World!";
String str2 = "Hello, World!";
```

当使用字符串字面量创建字符串时，Java 会先在字符串常量池中查找是否存在相同内容的字符串。若存在，直接返回该字符串的引用；若不存在，则在字符串常量池中创建一个新的字符串对象。这里 `str1` 和 `str2` 指向字符串常量池中的同一个 `"Hello, World!"` 对象，**不会重复创建**。

**使用 `new` 关键字：**

```java
String str3 = new String("Hello, World!");
String str4 = new String("Hello, World!");
```

使用 `new` 关键字创建字符串时，会在堆内存中创建一个新的字符串对象，无论字符串常量池中是否已有相同内容的字符串。`str3` 和 `str4` 是两个不同的对象，尽管它们的值相同。

## 边界标记

- **普通字符串**：只能使用双引号 `"` 作为边界标记。

  ```java
  String str = "Hello world!";
  System.out.println(str);  // Hello world!
  ```

- **子字符串**：使用 `\` 转义

  ```java
  String str = "Hello \"world\"!";
  System.out.println(str); // Hello "world"!
  ```

- **多行字符串**：即文本块，使用三重双引号 `"""` 作为边界标记。

  ```java
  String multiLineText = """
          这是一个\
          多行字符串示例，\
          无需使用转义字符来换行。
          """;
  System.out.println(multiLineText);  // 这是一个多行字符串示例，无需使用转义字符来换行。
  ```

## 字符串拼接

```java
String str1 = "Hello";
String str2 = " World!";
// 使用 + 运算符
String result1 = str1 + str2;
// 使用 concat() 方法
String result2 = str1.concat(str2);
```

## 字符串索引

Java 中的字符串不支持 `str[index]` 这种索引方法。

**获取元素：**

```java
String str = "Hello";
char ch = str.charAt(1); // 获取索引1的字符
System.out.println(ch);  // 输出: e
```

**找下标：**

```java
String str = "Hello World";
int index = str.indexOf('o');
System.out.println(index); // 输出: 4（"Hello" 中 'o' 第一次出现的位置）

int lastIndex = str.lastIndexOf('o');
System.out.println(lastIndex); // 输出: 7（"World" 中 'o' 位置）
```

## 获取长度

```java
String str = "Hello, World!";
int length = str.length();
System.out.println(length); // 13
```

## 遍历字符串

**索引思想遍历：**

```java
String str = "Hello";
for (int i = 0; i < str.length(); i++) {
    char ch = str.charAt(i);
    System.out.println(ch);
}
```

**for-each 思想遍历：**

Java 的 `String` 不能直接使用 `for-each` 遍历。需要先利用 `toCharArray` 将字符串转换成数组，再使用 `for-each` 遍历。

```java
String str = "Hello";
for (char ch : str.toCharArray()) {
    System.out.println(ch);
}
```

## 字符串的比较

### 比较引用地址

```java
String a = "Hello";
String b = "Hello";
System.out.println(a == b); // true（指向同一常量池对象）

String c = new String("Hello");
System.out.println(a == c); // false（c 指向堆中的新对象）
```

### 比较内容

```java
String a = new String("Hello");
String b = new String("Hello");
System.out.println(a.equals(b)); // true（值相同）
```

# 集合框架

Java 集合框架主要由两大接口派生而出：`Collection` 和 `Map`。`Collection` 接口存储一组不唯一、无序（部分有序）的对象，它又有三个主要的子接口：`List`、`Set` 和 `Queue`；`Map` 接口存储键值对，键是唯一的，值可以重复。

**常用接口：**

- **`Collection` 接口**：是集合框架的根接口，定义了集合的基本操作，如添加、删除、判断元素是否存在等。

  - **`List` 接口**：继承自 `Collection` 接口，存储有序且可重复的元素。用户可以通过索引访问和操作列表中的元素。
  - **`Set` 接口**：继承自 `Collection` 接口，存储唯一且无序的元素，不允许有重复元素。
  - **`Queue` 接口**：继承自 `Collection` 接口，用于模拟队列这种数据结构，遵循先进先出（FIFO）的原则。

- **`Map` 接口**：存储键值对，键是唯一的，每个键对应一个值。通过键可以快速查找对应的值。

**以下是一些使用 Java 集合框架的示例代码：**

```java
import java.util.*;

public class CollectionExample {
    public static void main(String[] args) {
        // ArrayList 示例
        List<String> arrayList = new ArrayList<>();
        arrayList.add("apple");
        arrayList.add("banana");
        arrayList.add("cherry");
        System.out.println("ArrayList: " + arrayList);

        // HashSet 示例
        Set<Integer> hashSet = new HashSet<>();
        hashSet.add(1);
        hashSet.add(2);
        hashSet.add(3);
        System.out.println("HashSet: " + hashSet);

        // HashMap 示例
        Map<String, Integer> hashMap = new HashMap<>();
        hashMap.put("one", 1);
        hashMap.put("two", 2);
        hashMap.put("three", 3);
        System.out.println("HashMap: " + hashMap);
    }
}
```

# 文件操作

在 Java 里，文件操作主要涵盖文件的创建、读取、写入以及删除等操作。Java 为文件操作提供了多个类和接口，常见的有 `File`、`FileInputStream`、`FileOutputStream`、`FileReader`、`FileWriter`、`BufferedReader`、`BufferedWriter` 等。

## 创建文件

使用 `File` 类检查/创建文件：

```java
import java.io.File;
import java.io.IOException;

public class FileDemo {
    public static void main(String[] args) {
        File file = new File("example.txt");

        // 检查文件是否存在
        if (file.exists()) {
            System.out.println("文件已存在: " + file.getAbsolutePath());
        } else {
            try {
                if (file.createNewFile()) {
                    System.out.println("文件已创建: " + file.getAbsolutePath());
                }
            } catch (IOException e) {
                System.out.println("创建文件时发生错误");
                e.printStackTrace();
            }
        }
    }
}

```

## 写入文件

使用 `FileWriter` 类写入文件：

```java
import java.io.FileWriter;
import java.io.IOException;

public class WriteFileDemo {
    public static void main(String[] args) {
        try {
            FileWriter writer = new FileWriter("example.txt");
            writer.write("Hello, this is a test.\nThis is the second line.");
            writer.close();
            System.out.println("写入成功");
        } catch (IOException e) {
            System.out.println("写入文件时发生错误");
            e.printStackTrace();
        }
    }
}
```

## 读取文件

使用 `BufferedReader` 类读取文件：

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class ReadFileDemo {
    public static void main(String[] args) {
        try {
            BufferedReader reader = new BufferedReader(new FileReader("example.txt"));
            String line;
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
            reader.close();
        } catch (IOException e) {
            System.out.println("读取文件时发生错误");
            e.printStackTrace();
        }
    }
}
```

## 删除文件

```java
import java.io.File;

public class DeleteFileDemo {
    public static void main(String[] args) {
        File file = new File("example.txt");
        if (file.delete()) {
            System.out.println("文件已删除: " + file.getName());
        } else {
            System.out.println("删除失败");
        }
    }
}
```

# Object Oriented

## Class and Method

```java
// 定义一个 Animal 类
public class Animal {
    // 成员变量（属性）
    String name;
    int age;

    // 构造方法
    public Animal(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // 成员方法（行为）
    public void makeSound() {
        System.out.println("Animal makes a sound.");
    }
}

// 定义一个 Dog 类，继承自 Animal 类
public class Dog extends Animal {

    // 构造方法
    public Dog(String name, int age) {
        // 调用父类的构造方法
        super(name, age);
    }

    // 重写父类的方法
    @Override
    public void makeSound() {
        System.out.println("Dog makes a sound.");
    }

    // 添加 Dog 特有的行为
    public void wagTail() {
        System.out.println("Dog wags its tail.");
    }
}

public class Main {
    public static void main(String[] args) {
        // 创建 Animal 类的对象
        Animal animal = new Animal("Generic Animal", 5);
        animal.makeSound();  // 输出：Animal makes a sound.

        // 创建 Dog 类的对象
        Dog dog = new Dog("Buddy", 3);
        dog.makeSound();  // 输出：Dog makes a sound.
        dog.wagTail();    // 输出：Dog wags its tail.
    }
}
```

## Method

方法的定义包含方法头与方法体两部分，其基本语法如下：

```java
访问修饰符 静态或实例指示符 返回值类型 方法名(参数列表) {
    // 方法体
    return 返回值; // 如果返回值类型不是 void，则需要有返回语句
}
```

```java
public class MethodExample {

    // 无参数、无返回值的方法
    public static void printHello() {
        System.out.println("Hello!");
    }

    // 带参数、无返回值的方法
    public static void printNumber(int num) {
        System.out.println("The number is: " + num);
    }

    // 带参数、有返回值的方法
    public static int add(int a, int b) {
        return a + b;
    }

    public static void main(String[] args) {
        // 调用无参数、无返回值的方法
        printHello();

        // 调用带参数、无返回值的方法
        printNumber(10);

        // 调用带参数、有返回值的方法
        int result = add(3, 5);
        System.out.println("The result of addition is: " + result);
    }
}
```

- **访问修饰符**：规定了方法的访问权限

  - `public`：任何地方都能访问
  - `private`：只有在同一个类里能访问
  - `protected`：在同一个类及其子类里能访问

- **静态或实例指示符**

  - 有 `static`：表明该方法是静态方法，能够直接通过类名调用，无需创建类的实例。
  - 无 `static`：表明该方法是实例方法，需要先创建类的实例，再通过实例来调用。

- **返回类型**：

  - 指定方法返回值的类型，例如 `List<Contact>`、`Integer`、`String` 等。
  - 若方法不返回任何值，返回值类型需设为 `void`。

- **方法名**：方法的标识符，要遵循 Java 的命名规范。
- **参数列表**：包含零个或多个参数，参数之间用逗号分隔，每个参数由**类型**和**名称**组成。

## 封装

```java
class Animal {
    // 私有成员变量，外部无法直接访问
    private String name;

    // 公共的访问方法（getter 和 setter）
    public void setName(String name) {
        this.name = name;
    }

    public String getName() {
        return this.name;
    }

    public void eat() {
        System.out.println(name + " is eating.");
    }
}
```

## 继承

```java
// 父类
class Animal {
    void eat() {
        System.out.println("Animal is eating.");
    }
}

// 子类
class Dog extends Animal {
    void bark() {
        System.out.println("Dog is barking.");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.eat(); // 调用父类的方法
        dog.bark(); // 调用子类自己的方法
    }
}
```

## 多态

### 方法重载

在同一个类中，定义多个同名方法，但这些方法的参数列表（参数的类型、个数或顺序）不同。

```java
class Animal {
    public void makeSound() {
        System.out.println("Animal makes a sound.");
    }
}

class Dog extends Animal {

    // 方法重载：带字符串参数
    public void makeSound(String sound) {
        System.out.println("Dog makes this sound: " + sound);
    }

    // 方法重载：带整数参数
    public void makeSound(int times) {
        for (int i = 0; i < times; i++) {
            System.out.println("Dog barks.");
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();

        dog.makeSound("Woof woof!");    // 调用重载方法，带字符串参数
        dog.makeSound(3);               // 调用重载方法，带整数参数
    }
}
```

### 方法重写

子类重写父类的方法，方法名、参数列表和返回值类型都要相同，但方法的实现可以不同。

```java
class Animal {
    public void makeSound() {
        System.out.println("Animal makes a sound.");
    }
}

class Dog extends Animal {
    // 子类重写方法
    @Override
    public void makeSound() {
        System.out.println("Dog makes a sound.");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal dog = new Dog();
        // 调用子类重写的方法
        dog.makeSound(); // Dog makes a sound.
    }
}
```

## 抽象

### 抽象类

**抽象类的特点：**

- 用 `abstract` 关键字声明。
- 可以有**抽象方法**（没有方法体，需要子类去实现），也可以有普通方法。
- 不能被实例化（不能直接用 `new` 来创建对象）。
- 子类必须**实现抽象方法**，除非子类本身也是抽象类。

```java
// 抽象类
abstract class Animal {
    // 抽象方法：没有方法体
    public abstract void makeSound();

    // 普通方法
    public void eat() {
        System.out.println("Animal eats food.");
    }
}

// 子类
class Dog extends Animal {
    // 必须实现抽象方法
    public void makeSound() {
        System.out.println("Dog barks.");
    }

    // 也可以添加自己的方法
    public void wagTail() {
        System.out.println("Dog wags its tail.");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal dog = new Dog();

        dog.makeSound();         // 调用的是 Dog 的实现
        dog.eat();               // 调用的是 Animal 的实现

        // dog.wagTail();       // ❌ 无法直接调用，因为引用类型是 Animal
    }
}
```

### 接口

接口是一种特殊的抽象类型，它只包含抽象方法和常量。接口中的方法默认是 `public abstract` 的，常量默认是 `public static final` 的。一个类可以实现多个接口。

**接口的特点：**

- 用 `interface` 关键字声明。
- 类必须通过 `implements` 关键字来实现接口。
- 只能有常量字段，不能有实例字段。
- 可以有**抽象方法**（没有方法体，需要子类去实现），也可以有普通方法。
- 不能被实例化（不能直接用 `new` 来创建对象）。
- 子类必须**实现抽象方法**，除非子类本身也是抽象类。

```java
// 接口
interface Animal {
    // 接口中的方法默认是 public abstract
    void makeSound();

    // Java 8+ 允许有 default 方法
    default void eat() {
        System.out.println("Animal eats food.");
    }
}

// 子类实现接口
class Dog implements Animal {
    @Override
    public void makeSound() {
        System.out.println("Dog barks.");
    }

    public void wagTail() {
        System.out.println("Dog wags its tail.");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal dog = new Dog();

        dog.makeSound();         // 调用的是 Dog 的实现
        dog.eat();               // 调用的是接口中的 default 方法

        // dog.wagTail();       // ❌ 无法调用，除非类型是 Dog
    }
}
```

# 异常处理

## 异常分类

在 Java 中，异常类都继承自 `Throwable` 类，`Throwable` 有两个重要的子类：`Error` 和 `Exception`。

- **`Error`**：表示系统级的错误，通常是由 Java 虚拟机（JVM）本身的问题引起的，如内存溢出（`OutOfMemoryError`）、栈溢出（`StackOverflowError`）等。这类错误一般无法通过程序代码进行处理，开发者通常只能尽量避免。
- `Exception`：表示程序可以处理的异常，它又可以分为两类：

  - **受检查异常（Checked Exception）**：编译器会检查这类异常，要求程序员在代码中进行显式的处理，否则编译不通过。例如，`IOException`、`SQLException` 等。
  - **非受检查异常（Unchecked Exception）**：也称为运行时异常（`RuntimeException`），编译器不会检查这类异常，它们通常是由程序逻辑错误引起的，如 `NullPointerException`、`ArrayIndexOutOfBoundsException` 等。

## 异常处理机制

Java 提供了 `try`、`catch`、`finally` 和 `throw`、`throws` 关键字来实现异常处理。

### try-catch

用于捕获和处理异常。`try` 块中放置可能会抛出异常的代码，`catch` 块用于捕获并处理特定类型的异常。示例如下：

```java
public class TryCatchExample {
    public static void main(String[] args) {
        try {
            int result = 10 / 0; // 可能会抛出 ArithmeticException 异常
            System.out.println(result);
        } catch (ArithmeticException e) {
            System.out.println("发生除零异常：" + e.getMessage());
        }
    }
}
```

在上述代码中，`try` 块中的 `10 / 0` 操作可能会抛出 `ArithmeticException` 异常，当异常发生时，程序会跳转到对应的 `catch` 块中进行处理。

### finally

`finally` 块中的代码无论是否发生异常都会被执行，通常用于释放资源，如关闭文件、数据库连接等。示例如下：

```java
import java.io.FileInputStream;
import java.io.IOException;

public class FinallyExample {
    public static void main(String[] args) {
        FileInputStream fis = null;
        try {
            fis = new FileInputStream("test.txt");
            // 读取文件内容
        } catch (IOException e) {
            System.out.println("发生 IO 异常：" + e.getMessage());
        } finally {
            try {
                if (fis != null) {
                    fis.close(); // 关闭文件流
                }
            } catch (IOException e) {
                System.out.println("关闭文件流时发生异常：" + e.getMessage());
            }
        }
    }
}
```

### throw

用于手动抛出一个异常对象。示例如下：

```java
public class ThrowExample {
    public static void checkAge(int age) {
        if (age < 0) {
            throw new IllegalArgumentException("年龄不能为负数");
        }
        System.out.println("年龄合法：" + age);
    }

    public static void main(String[] args) {
        try {
            checkAge(-5);
        } catch (IllegalArgumentException e) {
            System.out.println("捕获到异常：" + e.getMessage());
        }
    }
}
```

### throws

用于声明一个方法可能会抛出的异常，将异常处理的责任交给调用该方法的代码。示例如下：

```java
import java.io.FileInputStream;
import java.io.IOException;

public class ThrowsExample {
    public static void readFile() throws IOException {
        FileInputStream fis = new FileInputStream("test.txt");
        // 读取文件内容
        fis.close();
    }

    public static void main(String[] args) {
        try {
            readFile();
        } catch (IOException e) {
            System.out.println("发生 IO 异常：" + e.getMessage());
        }
    }
}
```

### 自定义异常

在某些情况下，你可能需要自定义异常类来表示特定的业务逻辑错误。自定义异常类通常继承自 `Exception` 或 `RuntimeException`。示例如下：

```java
// 自定义异常类
class MyException extends Exception {
    public MyException(String message) {
        super(message);
    }
}

// 使用自定义异常的类
public class CustomExceptionExample {
    public static void validate(int num) throws MyException {
        if (num < 0) {
            throw new MyException("数字不能为负数");
        }
        System.out.println("数字合法：" + num);
    }

    public static void main(String[] args) {
        try {
            validate(-5);
        } catch (MyException e) {
            System.out.println("捕获到自定义异常：" + e.getMessage());
        }
    }
}
```

# Spring Boot

## Spring Boot 基础

Spring Boot 是一个 Java 语言的框架。它是基于 Spring Framework 构建的，用于简化和加速 Java 应用程序的开发和部署。

## 基本流程

### 创建项目

- [进入 Spring Initializr 网站](https://start.spring.io/)
- 添加项目信息

  - Group：com.jerrycodes
  - Artifact：$PROJECT_NAME

- 添加项目依赖
- 生成项目压缩文件
- 下载并解压项目压缩文件到项目文件夹
- IDEA 打开项目文件夹，设置 JDK
- 创建包、类、数据库连接等

### 本地测试

- 启动 APP 后端
- 使用 Postman 模拟前端浏览器与后端交互
- 调试通过即可转向前端开发

### 生成 JAR 文件

- Maven 已安装
- 在项目的根目录中运行 Maven 命令来构建项目，这将在 `target` 目录中生成一个名为 `$APPLICATION.jar` 的可执行 JAR 文件。

  ```bash
  mvn clean package -DskipTests
  ```

- 将 `.gitignore` 中的 target 注释掉，或者将生成的可执行 JAR 文件 `your-application.jar` 复制到项目根目录

### 生成 Image

- 使用 GitLab Pipeline 生成 Image
- `.gitlab-ci.yml` 按通用格式写
- Dockerfile

  ```dockerfile
  FROM openjdk:17.0.1-jdk-slim
  WORKDIR /app
  COPY $APPLICATION.jar app.jar
  EXPOSE 8080
  CMD ["java", "-jar", "app.jar"]
  ```

## 依赖

## 包和类

- java /.../...
- Package `controller`：用于与 HTTP 交互，并传递给 service
- Package `model`

  - Class `CLASS_NAME`：定义类的方法

- Package `service`：服务

  - Class - Interfaces `SERVICE_NAME`：服务接口，接收 controller 的信息，并传递给 serviceImpl
  - Class `SERVICE_NAME_IMPL`：服务实现

- Packge `repository`：数据库接口

  - Class `CLASS_NAME`：数据库接口

## 数据库

- resources / application.properties
- 数据库进入方法和驱动

  ```properties
  # configuration
  spring.application.name=studentsystem
  
  spring.jpa.hibernate.ddl-auto=update
  spring.datasource.url=jdbc:mysql://localhost:3306/fullstack
  spring.datasource.username=root
  spring.datasource.password=
  spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
  ```

## 项目

- student-springboot-react-backend
