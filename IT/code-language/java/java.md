- 参考

```
- 我要自学网：燎原《JAVA语言入门教程2022版》
```

# Java 基础

## 环境搭建

### JDK

1. JDK 是 Java 语言的软件开发工具包。
2. 安装 Java 开发工具包 JDK17，JDK中已集成运行环境 JRE。
3. 安装其它 IDE

### Eclipse

​	Eclipse 是一款 IDE，主要用于 Java 开发。

#### Eclipse 安装

1. 确认 Java 开发工具包 JDK 已安装
2. 下载 Eclipse IDE for Enterprise Java and Web Developers
3. 解压到 D 盘，双击 ecplise.exe
4. 配置工作空间，即存项目的文件夹
5. 创建项目：new→java protect→填写项目名称、选择运行环境
6. 创建包：src 右键→new→Package（包名使用域名倒置，例：com.unit1.test）
7. 创建 class：包右键→new→class（类名首字母大写）

### IntelliJ IDEA

​	IntelliJ IDEA 是一款 IDE，主要用于 Java 开发。

#### IntelliJ IDEA 安装

- 安装时选择 `添加环境变量` 和 `关联Java`
- 破解教程见《Python笔记 - Pycharm》

#### IntelliJ IDEA 配置

## 代码规范

- 除以下规范，其余同编程语言通用规范
- **主方法入口**：所有的 Java 程序由 **public static void main(String[] args)** 方法开始执行。

## 标识符

- 除以下规范，其余同编程语言通用规范。
- **变量名**：可以使用汉字作为变量名。

- **源文件名**：源文件名必须和类名相同。

## 注释

- **单行注释**：Ctrl + /    **多行注释**：Ctrl + Shift + /

  ```java
  public class HelloWorld {
  	// 这是一个单行注释
      public static void main(String[] args){
  		/*
           * 多行注释第一行
           * 多行注释第二行
           * 多行注释第三行
           */
         System.out.println("Hello World"); 
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
  System.out.println();
  ```


## Maven

​	Maven 是一个用于构建和管理 Java 项目的工具

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

- Java 中字符使用**单**引号

### 字符串String

- Java 中字符串用 `String` 表示，使用**双**引号

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


# 控制结构

## 选择结构

Java 中有if、switch和三元表达式三种选择结构，用法同 JS。

- if
  - if
  - if-else
  - if-else if-else
- 三元表达式
- switch语句

## 循环结构

Java 中有 for 循环、while 循环、do-while 循环和 for-each 循环四种循环结构，前三种用法同 JS。

Java 中也支持嵌套循环、死循环、break和continue关键字，用法同 JS。

### for循环

- **语法**

  ```
  - 语法
  	for (初始化表达式; 条件表达式; 更新表达式){
  		循环体
  	}
  	
  - 执行流程
  	- 1.初始化表达式，初始化变量
      - 2.判断条件表达式（true执行，false终止）
      - 3.如果结果为true，则执行循环体
      	- 如果结果为false，则循环结束
      - 4.更新表达式，对初始化变量修改，继续判断条件表达式，直到判断结果为false
  ```

  ```java
  for(int i=0;i<=5;i++) {
      System.out.println(i);// 0 1 2 3 4 5
  }
  ```

### for-each循环

- Java 中没有 for-in 语句，for-each 循环就是其它语言中的 for-in 语句，用于直接遍历。

  ```
  - 语法
  	for (数据类型 变量名 : 数组){
  		循环体
  	}
  - 执行流程
  	- 数组有几个元素，就会执行几次循环体
      - 每次循环都会将相应元素赋值给变量
  ```

  ```java
  String[] arr = {"中国", "上海", "北京" };
  for (String data : arr) {
      System.out.println(data);// 中国 上海 北京
  ```

- 还可用索引思想遍历

  ```java
  int[] data = { 45, 67, 89 };
  for (int i = 0; i < data.length; i++) {
      System.out.println(data[i]);// 45 67 89
  }
  ```

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

​	Spring Boot 是一个 Java 语言的框架。它是基于 Spring Framework 构建的，用于简化和加速 Java 应用程序的开发和部署。

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
