- 参考

```
- 我要自学网：燎原《JAVA语言入门教程2022版》
```

# Java 基础

## 环境搭建

### JDK

JDK（Java Development Kit）是一个用于开发 Java 应用程序的工具包。它包含了运行 Java 程序所需的所有组件和开发工具。JDK 是 Java 开发的基础，任何想要开发 Java 应用的开发者都必须安装它。

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

1. 确认 Java 开发工具包 JDK 已安装
2. 下载 Eclipse IDE for Enterprise Java and Web Developers
3. 解压到 D 盘，双击 ecplise.exe
4. 配置工作空间，即存项目的文件夹
5. 创建项目：new→java protect→填写项目名称、选择运行环境
6. 创建包：src 右键→new→Package（包名使用域名倒置，例：com.unit1.test）
7. 创建 class：包右键→new→class（类名首字母大写）

### IntelliJ IDEA

IntelliJ IDEA 是一款 IDE，主要用于 Java 开发。

#### IntelliJ IDEA 安装

1. 安装时选择 `添加环境变量` 和 `关联Java`
2. 破解教程见 [`Python` > `Pycharm`](../python/python.md#Pycharm)

#### IntelliJ IDEA 配置

## 代码规范

- 除以下规范，其余同编程语言通用规范。
- **主方法入口**：所有的 Java 程序由 **public static void main(String[] args)** 方法开始执行。

## 标识符

- 除以下规范，其余同编程语言通用规范。
- **源文件名**：源文件名必须和类名相同。

## 注释

- **单行注释**：Ctrl + /    **多行注释**：Ctrl + Shift + /

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

## 变量

- Java 中声明变量时要使用相应数据类型的关键字。

  ```java
  int age = 19;
  ```

## 运算符

- **算术运算符**

  没有幂次方`**`

- **赋值运算符**

- **关系运算符**

- **逻辑运算符**

  与`&&`、或`||`、非`!`

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

1. [官网下载 Maven 二进制 zip 归档文件：apache-maven-3.9.6-bin.zip](https://maven.apache.org/download.cgi)
2. 解压到自己的安装目录，如 D:\Program Files (x86)\apache-maven-3.9.6
3. 设置系统环境变量，如 D:\Program Files (x86)\apache-maven-3.9.6\apache-maven-3.9.6\bin

### 命令

- 命令

  ```bash
  # 构建项目
  mvn clean package -DskipTests
  ```

# 数据类型

Java 语言提供了八种基本类型。六种数字类型（四个整数型，两个浮点型），一种字符型，还有一种布尔型。

## 整型

- Java 语言提供了四种整型：**int**、byte、short、long

## 浮点型

- Java 语言提供了两种浮点型：float、**double**

## 字符型char

- 使用单引号 `'` 标记字符。

### 字符串String

- 字符串用 `String` 表示
- 使用双引号 `"` 标记字符串。

## 布尔型boolean

- Java 中布尔值 true 和 false 首字母小写。

## 数据类型转换

- 不要尝试将数字字符串转换为数值型

- **自动转换**

  byte，short，char—> int —> long—> float —> double 

- **强制转换**

  ```java
  (int)data;
  ```

# 选择结构

Java 中有 `if`、`switch` 和 `三元表达式` 三种选择结构。

## if 语句

### if

- **语法**

    ```javascript
    if (条件表达式) {
        执行语句;
    }
    ```

    ```javascript
    int score = 85;
    
    if (score >= 60) {
        System.out.println("及格！");
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
    int score = 85;
    
    if (score >= 60) {
        System.out.println("及格！");
    } else {
        System.out.println("不及格！");
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

- **语法**

    ```java
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

- **多值匹配**

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

- **语法**

    ```java
    条件表达式 ? 真值 : 假值
    ```

    ```java
    Integer score = 80;
    String result = (score >= 60) ? "及格" : "不及格";
    System.out.println(result);  // 输出：及格
    ```

# 循环结构

- Java 中有 `for` 、`for-each`、`while`  和 `do-while` 四种循环结构。

## for 循环

- **语法**

  ```java
  for (初始化表达式; 条件表达式; 更新表达式){
      循环体
  }
  ```
  
  ```java
  for (int i=0; i<=5; i++) {
      System.out.println(i);  // 0 1 2 3 4 5
  }
  ```

## for-each 循环

- **语法**：用于直接遍历。

  ```java
  for (数据类型 变量名 : 数组或集合){
      循环体
  }
  ```
  
  ```java
  String[] arr = {"中国", "上海", "北京" };
  for (String data : arr) {
      System.out.println(data);  // 中国 上海 北京
  ```
  
- 还可用索引思想遍历

  ```java
  int[] data = { 45, 67, 89 };
  for (int i = 0; i < data.length; i++) {
      System.out.println(data[i]);  // 45 67 89
  }
  ```

## while 循环

- **语法**

    ```java
    while (条件表达式){
        循环体;
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

## do-while 循环

- **语法**

    ```javascript
    do {
        循环体
    } while (条件表达式);
    ```

    ```javascript
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

- **语法**

    ```java
    while (true) {
        循环体;
    }
    ```

    ```java
    do {
        循环体;
    } while (true);
    ```

    ```java
    for (;;){
        循环体;
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

- **`continue` 和 `break` 示例**

    ```java
    public class LoanRepayment {
        public static void main(String[] args) {
            for (int year = 1; year < 11; year++) {
                if (year == 5) {
                    System.out.println("第5年疫情原因，今年不用还款了！");
                    // 此处如果没有 continue，会同时正常显示：第五年到了，还款1.2万
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

- `return`：详见[返回值](#返回值)

# 数组

- 语法

  ```
  - 语法
  	数据类型[] 数组名 = {元素1, 元素2, 元素3...}
  - 特性：类似于Python中的列表
  	- 元素可重复；有序索引（下标）；元素支持修改。
  	- 只能存放一种数据类型
  	- 长度不可改变
  	- 使用for-each代替in包含
  ```

  ```java
  int[] data = { 45, 67, 89 };// 创建数组
  Class<?> componentType = data.getClass().getComponentType();// 获取数据类型
  System.out.println(componentType.getName());// int
  ```

- **获取元素**

  ```
  - 语法
  	数组名[索引号]
  ```

  ```java
  int[] data = { 45, 67, 89 };
  System.out.println(data[0]);// 45
  ```

- **获取长度**

  ```
  - 语法
  	数组名.length
  ```

  ```java
  int[] data = { 45, 67, 89 };
  System.out.println(data.length);// 3
  ```

  

# Spring Boot

## Spring Boot 基础

Spring Boot 是一个 Java 语言的框架。它是基于 Spring Framework 构建的，用于简化和加速 Java 应用程序的开发和部署。

## 基本流程

1. **创建项目**

   1. [进入 Spring Initializr 网站](https://start.spring.io/)
     2. 添加项目信息
        - Group：com.jerrycodes
        - Artifact：$PROJECT_NAME
     3. 添加项目依赖
     4. 生成项目压缩文件
   5. 下载并解压项目压缩文件到项目文件夹
   6. IDEA 打开项目文件夹，设置 JDK
   7. 创建包、类、数据库连接等

2. **本地测试**

   1. 启动 APP 后端
   2. 使用 Postman 模拟前端浏览器与后端交互
   3. 调试通过即可转向前端开发

3. **生成 JAR 文件**

   1. Maven 已安装

   2. 在项目的根目录中运行 Maven 命令来构建项目，这将在 `target` 目录中生成一个名为 `$APPLICATION.jar` 的可执行 JAR 文件。

      ```bash
      mvn clean package -DskipTests
      ```

   3. 将 `.gitignore` 中的 target 注释掉，或者将生成的可执行 JAR 文件 `your-application.jar` 复制到项目根目录

4. **生成 Image**

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

- 

## 包和类

- java /.../...
- Package `controller`：用于与 HTTP 交互，并传递给 service
- Package `model`
  - Class `CLASS_NAME`：定义类的方法
- Package `service`：服务
  - Class - Interfaces `SERVICE_NAME`：服务接口，接收 controller 的信息，并传递给 serviceImpl
  -  Class `SERVICE_NAME_IMPL`：服务实现
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
