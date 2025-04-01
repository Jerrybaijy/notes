# [JavaScript 基础](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript)

**JavaScript**（JS）是一种基于对象和事件驱动的**脚本语言**；JavaScript 文件的扩展名为 `.js`。Ecma 国际以 JavaScript 为基础制定了 ECMAScript 标准。

<img src="assets/image-20231111155734150.png" alt="image-20231111155734150" style="zoom:50%;" />

## JS 主要资源

- [JavaScript 基础](https://developer.mozilla.org/zh-CN/docs/Learn/Getting_started_with_the_web/JavaScript_basics)：了解 JavaScript 的含义和最基本用法
- [JavaScript  概述](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Language_overview)：了解 JavaScript 的基本概况
- [JavaScript 学习区](https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript)：学习 JavaScript 基础知识
- [JavaScript 参考](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference)：查找 JavaScript 的各个属性与概念

## 安装 Node.js

- [官网下载 Node.js 并安装](https://nodejs.org/zh-cn)

- 查看安装

    ```bash
    node -v
    npm -v
    ```

- 更新 `npm`

    ```bash
    npm install -g npm
    ```

## Node.js

**Node.js** 是一个开源、跨平台的 JavaScript 运行时环境，能够在服务器端运行 JavaScript。它最初由 Ryan Dahl 于 2009 年创建，并且使用了 Google 的 **V8 JavaScript 引擎**，该引擎最初是用于 Chrome 浏览器的，用于将 JavaScript 代码编译成高效的机器代码。Node.js 的核心优势在于它的非阻塞、事件驱动架构，使得它在构建高性能的网络应用时非常高效。

## npm

**npm** 是 node.js 的默认包管理工具。

- **命令**

  ```bash
  # 查看 npm 版本
  npm -v
  # 更新 npm 包管理工具到最新版
  npm install -g npm
  # 查看安装过的包
  npm list -g --depth=0
  
  # 创建静态文件夹
  npm run build
  ```

- **选项**

  ```bash
  -g # 全局
  ```

## pnpm

`pnpm` 是一个快速、节省磁盘空间的 JavaScript 包管理器，它是 `npm` 和 `yarn` 的替代品。

- 安装

    ```bash
    pnpm install -g pnpm
    ```

- 命令

    ```bash
    # 查看 pnpm 版本
    pnpm -v
    # 更新 pnpm 包管理工具到最新版
    pnpm install -g pnpm
    # 查看安装过的包
    pnpm list -g --depth=0
    ```


## http-server

- **http-server** 是一个基于 Node.js 的简单的静态文件服务器，可以用来快速地在本地启动一个 HTTP 服务器，用于提供静态文件服务。

  ```bash
  # 安装
  npm install -g http-server
  # 启动
  http-server -p 8080
  ```

## axios

- `axios` 是一个基于 Promise 的 HTTP 客户端，用于浏览器和 Node.js 环境。它可以用于发送 HTTP 请求并处理响应，具有简单易用的 API，支持异步操作，并提供了丰富的配置选项和拦截器功能。在前端开发中，`axios` 经常被用来与后端 API 进行数据交互，例如发送 GET、POST、PUT、DELETE 等请求，然后处理服务器返回的数据。

- Commands

  ```bash
  # Install
  npm install axios
  ```

## JS 位置

- **内联事件处理**： HTML 元素内部直接使用 JavaScript 代码添加事件。

  ```html
  <button onclick="console.log('按钮被点击了')">点击按钮</button>
  ```

- **嵌入式脚本**：将 JavaScript 代码放到在 HTML 文档 `<script>` 元素中。

  - **脚本前置**：将 `<script>` 放到 `<head>` 中。

    ```html
    <head>
      <script>
        console.log("JavaScript in head");
      </script>
    </head>
    
    <body>
      <h1>欢迎使用JavaScript</h1>
    </body>
    ```

  - **脚本后置**：将 `<script>` 放到 `<body>` 底部。

    ```html
    <body>
        <h1 id="title">欢迎使用JavaScript</h1>
        <script>
            document.getElementById('title').style.color = 'green';
        </script>
    </body>
    ```

  - **前置与后置对比**：正常情况，浏览器会按照代码在文件中的顺序加载 HTML。如果先加载的 JavaScript 期望修改其下方的 HTML，那么它可能由于 HTML 尚未被加载而失效。因此，脚本后置比脚本前置更好。

- **外部脚本**：在 HTML 文档的 `<head>` 中使用 `<script>` 元素引入外部 **JS 文件**。

	```html
	<head>
	  <script src="script.js" defer></script>
	</head>
	```

	```javascript
	// script.js
	console.log("External JavaScript file");
	```

	**在以上代码中**：

	1. `difer`：解析渲染 HTML 和加载脚本文件会同时进行（异步加载），HTML 文档解析完毕（`DOMContentLoaded` 事件触发之前）再执行脚本。


## 代码规范

- 除以下规范，其余同编程语言通用规范。
- **缩进**：一般缩进2个空格

## 标识符

- 除以下规范，其余同编程语言通用规范。
  

## 注释

- 同 Java；单行注释：`Ctrl + /`，多行注释：`Ctrl + Shift + /`

	``` javascript
	/**
	 * 这是一个文档注释示例。
	 * 它通常包含有关类、方法或字段的详细信息。
	 * 例如，描述类的作用或方法的功能。
	 */
	
	// 这是一个单行注释，描述下面的方法。
	function main() {
	    /*
	     * 多行注释第一行
	     * 多行注释第二行
	     * 多行注释第三行
	     * 这里是对下面的输出代码块的解释。
	     */
	    
	    console.log("Hello World");
	}
	
	// 调用 main 方法
	main();
	```

## 变量声明

- `无关键字` 声明的变量，具有全局级作用域，考略到代码可维护性和可读性，不推荐。
- `var` 声明的变量，具有函数级作用域；存在变量提升现象。
- `let` 用于声明**变量**，具有块级作用域。优先使用 **let** 声明变量。
- `const` 用于声明**常量**，具有块级作用域；不能被重新赋值。

- **变量提升**：JS 代码的执行是由浏览器中的 JS 解析器执行的，分为两个过程：预解析和代码执行。
- **变量提升**
    - 把变量的声明提升到声明作用域的最前面；
        - 只会提升声明，不会提升赋值，相当于声明但未赋值，此时变量的值为 `undefined`；
    - 把函数的声明提升到当前作用域的最前面；
        - 提升定义，在前面调用后定义的函数可以正常执行；
        	- 注意函数表达式的声明提升，是变量声明提升，而不是函数声明提升；
    - 先提升变量，后提升函数，如果变量与函数同名，函数会覆盖变量。
- 代码执行
  - 预解析之后，按既定规律执行代码

## 输入与输出

### 输入

- **语法**：`prompt("提示语")`

  ```html
  <head>
  	<script src="./test.js" defer></script>
  </head>
  ```
  
  ```javascript
  let a = prompt("请输入用户名");
  console.log(a);
  ```

- **扩展**：`prompt()` 可以输入默认参数

	```html
	<head>
		<script src="./test.js" defer></script>
	</head>
	```

	```javascript
	let a = prompt("请输入用户名", "张三");
	console.log(a);
	```

### 输出

- **语法**：`console.log("输出内容")`

  ```html
  <head>
  	<script src="./test.js" defer></script>
  </head>
  ```

  ```javascript
  console.log("你猜我在哪？");
  ```

- **查看**：`Live server` 在浏览器查看 `HTML`，浏览器控制台查看结果，`F12 | 右键 > 检查`

- **扩展**

	- 弹窗：`alert("哈哈哈");`
	- 网页输出：`document.write("你猜我在哪");`，注意此种方法在引入脚本时不能使用 `defer`。

## [`this`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/this)

`this` 是 JavaScript 中的一个特殊关键字，用于引用当前上下文中的对象。`this` 的值在不同的场景中会有所不同，其行为依赖于**函数调用的方式**。

关于 `this` 的指向如下所述：

- **全局上下文**：指向全局对象
	- 浏览器中是 `window` 对象
	- Node.js 中是 `global` 对象
- **普通函数**：指向 `window` 对象
- **方法**：指向调用该方法的对象
- **箭头函数**：箭头函数不会绑定自己的 `this`，而是继承自外层作用域的 `this`。
- **构造函数**：当使用 `new` 关键字调用构造函数时，`this` 指向新创建的对象。
- **类**：指向该类的实例
- **DOM 事件**：指向绑定事件的 DOM 元素

# [数据类型](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Data_structures)

- JS 是一种**弱类型语言**，不用提前声明变量的数据类型，在程序运行过程中，变量的数据类型会被自动确定。
	- 虽说是**弱类型语言**，但各种数据类型在程序执行的时候，会很灵活地自动转换 ，所以要格外小心。

- **JavaScript 数据类型**
  - **原始值**：基本数据类型
  - **对象**：复杂数据类型（或称为引用数据类型）

## [原始值](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Data_structures#%E5%8E%9F%E5%A7%8B%E5%80%BC)

- **原始值**，除了 `Object` 以外，所有的类型都定义了不可变的、在语言最底层直接表示的值。我们将这些类型的值称为**原始值**，一共7种。
  - **`number`**：数字
  - **`bigInt`**：大整数
  - **`boolean`**：布尔值
  - **`string`**：字符串
  - **`symbol`**：标识
  - **`null`**：空值
  - **`undefined`**：未定义
- **说明**：原始值是不可变类型，一旦创建，就不能修改。

## [数字 `number`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Data_structures#number_%E7%B1%BB%E5%9E%8B)

- **语法**：JS 中的 `number` 可以用来保存整数或浮点数
- **说明**
  
  - JS中位数多的数值在输出时不会十分精确，应该使用大整数。
  - 浮点数运算时不会十分精确

### 进制

- **JS 中的进制**
  
  - 常见的进制有二进制、八进制、十进制和十六进制;
  - 在JS中还可以用八进制和十六进制，输出时统一用十进制表示；
  
- **八进制**

  - 在数字开头加上0，表示八进制数，八进制数由0~7组成，逢8进位。
  
    ```javascript
    let num1 = 07;
    console.log(num1);  // 7
    
    let num2 = 010;
    console.log(num2);  // 8
    ```
  
- **十六进制**

  - 在数字开头加上 `0x`，表示十六进制数，十六进制数由 `0-9` 和 `a-f` 组成。
  - 十六进制数中的 `x` 和 `a~f` 不区分大小写。
  
    ```javascript
    let numl = 0x9;
    console.log((numl);  // 9
    let num2 = Oxa;
    console.log(num2);  // 10
    ```

### 范围

- 数字型有一定的范围

  ```javascript
  console.log(Number.MAX_VALUE);  // 1.7976931348623157e+308
  console.log(Number.MIN_VALUE);  // 5e-324
  ```

### 特殊值

- 数字型有3个特殊值：
- `Infinity` ：无穷大；
  - 大于或等于2的1024次方的数值，JS 无法表示，会返回 `Infinity`。
- `-Infinity` ：无穷小；
- `NaN` ：非数字（Not a Number）；
  - 使用 `isNaN()` 函数检查一个数值是不是 `NaN`，返回 `true` 或 `false`。

## [大整数 `bigint`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Data_structures#bigint_%E7%B1%BB%E5%9E%8B)

- **定义**：`bigint` 是 JS 中的任意精度整数，没有位数的限制，即使超出 `number` 能够表示的安全整数范围。
- **语法**
  - 大整数表示一些数值比较大的整数
  - 大整数必须添加后缀 `n`
  - 大整数与普通整数是两种值，它们之间并不相等，例如
  	`100 == 100n;  // false`

## [布尔值 `boolean`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Data_structures#boolean_%E7%B1%BB%E5%9E%8B)

- JS 中的布尔值首字母**小写**：`true` 和 `false`

  ```javascript
  let a = true;
  let b = false;
  console.log(5 > 3);  // true
  console.log(6 < 2);  // false
  ```

## [字符串 `string`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Data_structures#string_%E7%B1%BB%E5%9E%8B)

### 字符串基础

- **定义字符串**

  ```javascript
  // 字面量方式
  let str1 = "hello world";  // 文本形式的字符串
  let str2 = "";  // 空字符串
  let str3 = "6";  // 数值形式的字符串
  
  // 构造函数方式
  let str = new String();  // String首字母大写，此处new可以省略
  ```

- **基本包装类型**

	在 JS 中，只有对象数据类型才有属性和方法，原始值没有。但通过基本类型包装，会暂时将字符串包装成一个对象，可以使字符串暂时拥有属性和方法，结束后对象再被销毁。

### 获取长度 `length`

- **语法**：`STR.length`，返回 `number`。

  ```javascript
  let str = "中国江西联通"
  let res = name.length;
  console.log(res);  // 6
  console.log(typeof res);  // number
  ```

### 索引

- **语法**：`STR[索引号]`，返回 `string`。

  ```javascript
  //         0 1 2 3 4 5，正向索引号
  let str = "中国江西联通";
  console.log(str[0]);  // 中
  console.log(str[-5]);  // undefined
  console.log(typeof str[0]);  // string
  ```

- **说明**：JS 不支持直接逆向索引，会返回 `undefined`。
- **扩展**

	- **变相逆向索引**：`STR[STR.length - 索引号]`，返回 `string`。

		```javascript
		let str = "中国江西联通";
		console.log(str[str.length-5]);  // 国
		```

	- **多级索引**：`Arry[一级索引号][二级索引号]...`，返回 `string`。

		```javascript
		let arr = ["中国", ["上海", "北京", "深圳"], 123];
		let str1 = arr[1][0];
		let str2 = arr[1][0][0];
		console.log(str1);  // 上海
		console.log(str2);  // 上
		```

	- **示例**

		```javascript
		let str = "中国江西联通";
		let index = 0;  // index为索引号
		while (index < str.length) {
		    let strNew = str[index];
		    console.log(strNew);
		    index += 1;
		}
		
		// 依次打印“中国江西联通”
		```

### 遍历

- 详见 [`for-of` 语句](#`for-of` 语句)

### `in` 包含

- **语法**：`STR.includes(元素)`，返回 `boolean`。

  ```javascript
  let str = "中国联通";
  let res = str.includes("中国");
  console.log(res);  // true
  ```

### 切片 `slice`

- JS 不支持索引直接切片，但可以使用 `slice()` 代替。
- **语法**：`STR.slice(INDEX_START, INDEX_END)`，返回 `string`。

  ```javascript
  //      0 1 2 3 4 5，正向索引号
  let str = "中国江西联通";
  
  console.log(str.slice(2, 4));  // 江西
  console.log(str.slice(2));  // 江西联通（可省略终结索引号）
  ```

- **扩展**：`slice()` 支持逆向索引。

### 切割 `split`

- **语法**：`STR.split(切割标识)`，返回 `Arry`。

	```javascript
	let str = "马化腾,40,XXXX@qq.com";
	let res = str.split(",")  // ","为切割标识
	
	console.log(res);  // ['马化腾', '40', 'XXXX@qq.com']
	```

- **综合示例**

  ```javascript
  let str = "马化腾,40,XXXX@qq.com";
  let res1 = str.split(",")  // 把所有序列都切割，分别放入子字符串，逗号是切割标识依据
  let res2 = str.split(".")  // "."为切割标识
  let res3 = str.split(",", 1)  // 从左到右，保留1个子字符串
  
  console.log(res1);  // ['马化腾', '40', 'XXXX@qq.com']
  console.log(res1[0]);  // 马化腾
  console.log(res2);  // ['马化腾,40,XXXX@qq', 'com']
  console.log(res3);  // ['马化腾']
  ```

### 合并 `concat`

- **语法**：`STR.concat(任意数据类型)`，返回 `string`。

  ```javascript
  let str1 = "abc";
  
  let str2 = str1.concat("def");  // 参数为字符串字面量
  let str3 = str1.concat(null, 4, "f");  // 参数为零散的任意数据类型
  
  console.log(str2);  // abcdef
  console.log(typeof str2)  // string
  
  console.log(str3);  // abcnull4f
  console.log(typeof str3)  // string
  ```

### 模板字符串

- **语法**：用反引号包围字符串

	```javascript
	let a = `Hello World`;
	```
	
- **跨行输出**

  ```javascript
  // 用双引号包围的字符串，每行后面加反斜杠，可以分多行书写，但在一行输出
  let a = "今天天气真不错\
  真不错啊\
  真不错";
  console.log(a);  // 天气真不错真不错啊真不错
  
  // 用反引号包围的字符串，分多行书写，在多行输出
  let b = `今天天气真不错
  真不错啊
  真不错`;
  console.log(b);  // 分多行输出
  // 天气真不错
  // 真不错啊
  // 真不错
  ```

- **嵌套变量 + 拼接**

	```javascript
	let a = "你好";  // a 可以是任意数据类型
	let b = `${a}世界`;  // 注意此处的 $ 是语法的一部分
	console.log(b);  // 你好世界
	```

### 替换 `replace`

- **语法**：`STR.replace("旧元素", "新元素")`，返回 `string`。

  ```javascript
  let str = " 中国 联通 联通 ";
  let res = str.replace("联通", "移动");
  console.log(res);  // " 中国 移动 联通 "
  ```

- **说明**：JS中，`replace()` 只能替换一个符合要求元素（最左侧一个）。

### 去除空格、换行 `strim`

- **语法**：`STR.trim()`，返回 `string`。

	```javascript
	let str = " 中国 联通 ";
	
	// 去除开头和结尾的空格
	let res1 = str.trim();
	console.log(res1);  // "中国 联通"
	
	// 去除开头的空格
	let res2 = str.trimStart();
	console.log(res2);  // "中国 联通 "
	
	// 去除结尾的空格
	let res3 = str.trimEnd();
	console.log(res3);  // " 中国 联通"
	```

	```javascript
	// 去除换行
	let str = "中国联通\n";
	console.log(str);  // 中国联通（后面有换行）
	
	res4 = str.trim();
	console.log(res4);  // 中国联通（后面没有换行）
	```

- **扩展**：`trim()` 不能去除中间的空格，去除中间空格应使用 `str.replace(" ", "")`，将空格替换成空白

### 转大小写

- **语法**

  - 转大写：`STR.toUpperCase()`，返回 `string`。
  - 转小写：`STR.toLowerCase()`，返回 `string`。

  ```javascript
  let str = "abc";
  let res = str.toUpperCase();
  console.log(res);  // ABC
  ```

### 判断起始 `startWith`

- **语法**：`STR.startWith()`，返回 `boolean`。

  ```javascript
  let str = "中国联通";
  let res = str.startsWith("中国");
  console.log(res);  // true
  ```

### 判断数字

- JS 中没有直接判断一个字符串是否是数字形式的字符串
- 可以结合正则表达式判断

### 找下标 `indexOf`

- **语法**：`STR.indexOf("匹配项")`，返回 `number`。

  ```javascript
  let str = "中国江西联通中国";
  
  // 第一个匹配项
  console.log(str.indexOf("国"));  // 1
  console.log(typeof(str.indexOf("国")))  // number
  
  // 最后一个匹配项
  console.log(str.lastIndexOf("国"));  // 7
  
  // 错误的匹配项
  console.log(str.indexOf("海"));  // -1
  ```

## [空值 `null`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Data_structures#null_%E7%B1%BB%E5%9E%8B)

- JS 中，空值的字面量是 `null`，数据类型是 `object`，[点击查看原因](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/typeof#typeof_null)。
- 从逻辑角度，`null` 表示空对象指针。

## [未定义 `undefined`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Data_structures#undefined_%E7%B1%BB%E5%9E%8B)

- JS 中，未定义的字面量是 `undefined`，数据类型是 `undefined`。

## [标识 `symbol`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Data_structures#symbol_%E7%B1%BB%E5%9E%8B)

- `symbol` 指的是独一无二的值，这是 ES6 新增的数据类型。
- 每个通过 `Symbol()` 生成的值都是唯一的。

	- `symbol` 类型的对象永远不相等，即便创建的时候传入相同的值

- **语法**

  ```javascript
  let a = Symbol();
  let b = Symbol();
  console.log(a);  // Symbol()
  console.log(typeof a);  // symbol
  console.log(a == b);  // false
  ```

## 数组 `Array`

### 数组基础

- **特性**：详见 [`code-general` - `列表（数组）`](../../code-general/code-general.md#列表（数组）)

- **语法**：`[ITEM1, ITEM2, ...]`

	```javascript
	// 字面量方式
	let arr = ["中国", "上海", 123];
	
	// 构造函数方式
	let arr = Array();  // []
	```

- **基础示例**

	```javascript
	let arr = ["中国", "上海", 123];
	console.log(arr);  // ['中国', '上海', 123]
	console.log(typeof arr);  // object
	```

- **说明**：数组是一个特殊的**对象**，数据类型为 `object`，具体数据类型为 `Array`。

- **公共功能**

	- 以下功能详见字符串
	- 获取长度 `.length`
	- 索引（JS 不可索引切片）
	- 遍历 `for-of 语句`
	- ~~JS 中数组没有 `in` 包含功能~~
	- 嵌套
	- 切片 `.slice()`
	- 合并 `.concat()`

- **其它功能**

	```javascript
	let arr = [1, 2, 3, 4];
	
	arr[0] = 5;  // 修改
	
	arr.push(5);  // 追加
	
	arr.splice(1, 0, "北京", "上海");  // 插入
	
	arr.splice(1, 2, "北京", "上海");  // 替换
	
	arr.remove(1, 2);  // 删除
	
	arr.length = 0;  // 清空
	
	arr.reverse();  // 反转
	
	arr.sort();  // 排序
	
	strr = arr.join("_");  // join 连接
	```

### 数组修改元素 `索引`

- **语法**：`ARRAY[INDEX] = VALUE`，原数组被改变，

	```javascript
	let arr = [1, 2, 3, 4];
	arr[0] = 5;
	console.log(arr);  // [5, 2, 3, 4]
	```

- **扩展**：如果索引号超过数组最大项，会创建新元素，并在新元素与旧元素之间创建空属性，同时被动增加数组长度。

	```javascript
	let arr = [1, 2, 3, 4];
	arr[6] = 5;  // 索引号超过数组最大项
	console.log(arr);  // [1, 2, 3, 4, 空属性 × 2, 5]
	console.log(arr[4], arr[5])  // undefined undefined
	console.log(arr.length);  // 7
	```

### 数组追加元素 `push`

- **语法**：`ARRAY.push(ITEM1, ITEM2, ...)`，原数组被改变，返回原数组被改变之后的长度 `number`。

	```javascript
	let arr = [1, 2, 3, 4];
	let res = arr.push(5, 6, 7, 8);
	
	console.log(arr);  // [1, 2, 3, 4, 5, 6, 7, 8]
	console.log(res);  // 8  // 返回原数组被改变之后的长度
	console.log(typeof res);  // number
	```

- **扩展**：使用扩展运算符添加元素 `[...ARRAY, ITEM1, ITEM2, ...]`，原数组不被改变。

	```javascript
	let arr = [1, 2, 3, 4];
	let arrStart = [...arr, 5, 6, 7, 8];
	let arrEnd = [5, 6, 7, 8, ...arr];
	
	console.log(arr);  // [1, 2, 3, 4]
	console.log(arrStart);  // [1, 2, 3, 4, 5, 6, 7, 8]
	console.log(arrEnd);  // [5, 6, 7, 8, 1, 2, 3, 4]
	```

### 数组插入、替换和删除元素 `splice`

- **语法**：`ARRAY.splice(INDEX_START, COUNT_DEL[, ITEM1, ITEM2...])`，原数组被改变，返回被删除元素组成的数组 `object`。

	```javascript
	// 插入
	let arr1 = [1, 2, 3, 4];
	let res1 = arr1.splice(0, 0, 5, 6, 7, 8);  // 在第0索引号删除0个，插入 5, 6, 7, 8
	console.log(arr1);  // [5, 6, 7, 8, 1, 2, 3, 4]
	console.log(res1);  // []  // 返回被删除元素组成的数组
	console.log(typeof res1);  // object
	
	// 替换
	let arr2 = [1, 2, 3, 4];
	let res2 = arr2.splice(1, 2, 22, 33);  // 在第1索引号删除2个，插入 22, 33
	console.log(arr2);  // [1, 22, 33, 4]
	console.log(res2);  // [2, 3]  // 返回被删除元素组成的数组
	console.log(typeof res2);  // object
	
	// 删除
	let arr3 = [1, 2, 3, 4];
	let res3 = arr3.splice(1, 2);  // 在第1索引号删除2个，不插入新元素
	console.log(arr3);  // [1, 4]
	console.log(res3);  // [2, 3]  // 返回被删除元素组成的数组
	console.log(typeof res3);  // object
	```

- **扩展**：`ARRAY.toSpliced()` 方法，原数组不被改变。

### 数组清空 `length=0`

- **语法**：`ARRAY.length = 0;`，原数组被改变。

	```javascript
	let arr = [1, 2, 3, 4];
	arr.length = 0;
	console.log(arr);  // []
	```

### 数组反转 `reverse`

- **语法**：`ARRAY.reverse()`，原数组被改变，返回反转之后的原数组。

	```javascript
	let arr = [1, 2, 3, 4];
	let res = arr.reverse();
	
	console.log(arr);  // [4, 3, 2, 1]
	console.log(res);  // [4, 3, 2, 1]  返回反转之后的原数组
	console.log(typeof res);  // object
	```

- **扩展**：`ARRAY.toReversed()` 方法，原数组不被改变。

### 数组升序 `sort`

- **语法**：`ARRAY.sort()`，原数组被改变，返回升序之后的原数组。

	```javascript
	let arr = ["80", "9", "700", 40, 1, 5, 200];
	let res = arr.sort();
	
	console.log(arr);  // [1, 200, 40, 5, '700', '80', '9']
	console.log(res);  // [1, 200, 40, 5, '700', '80', '9']  // 返回升序之后的原数组
	```

- **说明**：默认排序是将元素转换为字符串，然后按照它们的 UTF-16 码元值升序排序。

- **扩展**：`ARRAY.toSorted()` 方法，原数组不被改变。

- **扩展**：以下方法按数字大小进行升序排序

	```javascript
	let arr = ["80", "9", "700", 40, 1, 5, 200];
	function compareFn(a, b) {
	  return a - b;
	}
	let res = arr.sort(compareFn);
	
	console.log(arr);  // [1, 5, '9', 40, '80', 200, '700']
	console.log(res);  // [1, 5, '9', 40, '80', 200, '700']
	```

### 数组连接 `join`

- **语法**：`ARRAY.join(["SEPARATION"])`，返回字符串 `str`。

	```javascript
	let arr = ["中国", "上海", 123];
	let res = arr.join("_");  // "_"为分隔符
	console.log(res);  // 中国_上海_123
	console.log(arr);  // ["中国", "上海", 123]
	```

## [获取数据类型](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/typeof)

- **语法**：`typeof OPERAND | (OPERAND)`，返回代表数据类型的**字符串**。

	```javascript
	let str = "中国江西联通";
	console.log(typeof str);  // string
	```

- `typeof` 可以获取到原始值和对象

	- **原始值（没有 `null`）**
		- **`number`**：数字
		- **`bigInt`**：大整数
		- **`boolean`**：布尔值
		- **`string`**：字符串
		- **`symbol`**：标识
		- ~~**`null`**：获取不到 `null`，会返回 `object`，[点击查看原因](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/typeof#typeof_null)。~~
		- **`undefined`**：未定义

	- **对象**
		- `object`：包括普通对象、数组和 `null`
		- `function`：函数属于特殊的对象

## 数据类型转换

JS 是一门**弱类型语言**，对数据类型要求没那么严格，如果数据类型不符合要求，系统会按规定自动转换为符合要求的类型。

### 转换成字符串

- **语法1**：`String(ITEM)`，调用函数，显式转换。

	```javascript
	let data = true;
	res = String(data);
	
	console.log(res);  // true
	console.log(typeof res)  // string
	```

- **语法2**：`ITEM.toString()`，调用方法，显式转换。

	- `null` 和 `undefined` 没有 `toString()` 方法
	- `ITEM` 可以是数组


  ```javascript
let data = true;
res = data.toString();

console.log(res);  // true
console.log(typeof res)  // string
  ```

- **<span id="string-addition">语法3</span>**：`ITEM + STR`，字符串加法，隐式转换。

	```javascript
	// ITEM也许可以是任意数据类型
	
	let res1 = 10 + "5";  // 将数字 10 转为字符串 "10"
	console.log(res1);  // 105
	console.log(typeof res1);  // string
	
	let res2 = true + "";  // 将布尔值 true 自动转换为字符串 "true"
	console.log(res2);  // true
	console.log(typeof res2)  // string
	```

### 转换成数字

- **语法1**：`Number(ITEM)`，调用函数，显式转换。

	```javascript
	let str = "5";
	res = Number(str);
	
	console.log(res);  // 5
	console.log(typeof res);  // number
	```

- **语法2**：`+ITEM`，算术加法运算符，隐式转换。

	```javascript
	// ITEM也许可以是任意数据类型
	
	let data1 = "5";
	let res1 = +data1;  // 将字符串 "5" 转换为数字 5
	console.log(res1);  // 5
	console.log(typeof res1);  // number
	
	let data2 = ["中国", "上海", 123];
	let res2 = +data2;  // 自动将数组里的元素都作为字符串进行拼接，得到 "中国上海123"，然后转换为 NaN
	console.log(res2);  // NaN
	console.log(typeof res2);  // number
	```

- **说明**

	- **字符串转换为数值**
		- 合法数字的字符串将被转换为相应数值
		- 不合法数字的字符串（如 `123px`）将被转换为 `number` 的特殊值 `NaN`。
		- 空字符串将被转换为 `0`
	- **布尔值转换为数值**
		- `true`：1
		- `false`：0
	- **空值转换为数值**
		- `null`：0
	- **未定义转换为数值**
		- `undefined`：`NaN`

### 转换成布尔值

- **语法1**：`Boolean(ITEM)`，调用函数，显式转换。

	```javascript
	// ITEM也许可以是任意数据类型
	
	let data1 = "5";
	let res1 = Boolean(data1);  // 将字符串 "5" 转换为布尔值 true
	console.log(res1);  // true
	console.log(typeof res1);  // boolean
	
	let data2 = ["中国", "上海", 123];
	let res2 = Boolean(data2);  // 自动将数组里的元素都作为字符串进行拼接，得到 "中国上海123"，然后转换为布尔值 true
	console.log(res2);  // true
	console.log(typeof res2);  // boolean
	```

- **语法2**：`!ITEM`，逻辑非，隐式转换。

	```javascript
	// ITEM也许可以是任意数据类型
	
	let data1 = "5";
	let res1 = !data1;  // 将字符串 "5" 转换为布尔值 falese
	console.log(res1);  // falese
	console.log(typeof res1);  // boolean
	
	let data2 = ["中国", "上海", 123];
	let res2 = !data2;  // 自动将数组里的元素都作为字符串进行拼接，得到 "中国上海123"，然后转换为布尔值 falese
	console.log(res2);  // falese
	console.log(typeof res2);  // boolean
	```

- **说明**：`0`、`NaN`、`null`、`undefined`、`空字符串` 和 `false` 将被转换为 `false`，其它数据将被转换为 `true`。

## 数据的可变性

- 关于数据的可变性，详见 **code-general | 数据的可变性**
- **不可变数据类型：**
	- **`Number`**：数字
	- **`String`**：字符串
	- **`Boolean`**：布尔值
	- **`undefined`**：未定义值
	- **`null`**：空值
	- **`BigInt`**：大整数
	- **`Symbol`**：符号
- **可变数据类型：**
	- **`Object`**：对象
	- **`Array`**：数组
	- **`Function`**：函数
	- **`Map`**：映射
	- **`Set`**：集合
	- **`WeakMap`**：弱映射
	- **`WeakSet`**：弱集合

# 运算符

## 算术运算符

- JS 是一门弱类型语言，当进行数学运算时，除了字符串的加法，其它都会自动转换成数值来完成运算。

  - **`+`**：加
  - **`-`**：减
  - **`*`**：乘
  - **`/`**：除
  - **`**`**：幂
  - **`//`**：向下取整除（除法保留整数）
  - **`%`**：取模（除法获取余数）

- JS 中的算术运算符的几点说明

  - JS 中，`Infiny` 参与数学运算
  	- 作为加减乘除的第一个数，会返回 `Infiny`
  	- 作为取余的第一个数，会返回 `NaN`
  - JS 中，`10/0` 会返回 `Infiny`
  - JS 中，`NaN` 参与的算术运算，都会返回 `NaN`

- **非数字参与算术运算**：其它数据类型将自动转换为数字类型（[字符串加法](#string-addition)例外），进行算术运算。

  ```javascript
  let data = 10 - "5";  // 字符串 "5" 转为数字 5
  console.log(res);  // 5
  console.log(typeof res);  // number
  
  let data = 10 + true;  // 布尔值 true 转为数字 1
  console.log(res);  // 11
  console.log(typeof res);  // number
  
  let data = 10 + NaN;  // number 类型的特殊值 NaN 与任何数据类型相加都等于 NaN
  console.log(res);  // NaN
  console.log(typeof res);  // number
  
  # 字符串加法：将不是字符串的数据类型转为字符串，然后拼接。
  let data = 10 + "5";  // 数字 10 转为字符串 "10"
  console.log(res);  // 105
  console.log(typeof res);  // string
  ```

## 赋值运算符

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
	- **`??=`**：空赋值
	-  `<<=`：左移赋值
	-  `>>=`：右移赋值
	- `>>>=`：无符号右移赋值
	- JS 中没有取整除 `//=`

- **解构赋值运算符**

	```javascript
	let [x, y] = [10, 20];
	console.log(x);  // 输出: 10
	console.log(y);  // 输出: 20
	```

- **函数默认参数赋值运算符**

	```javascript
	function greet(name = "Guest") {
	  console.log(`Hello, ${name}`);
	}
	
	greet();  // 输出: "Hello, Guest"
	greet("Alice");  // 输出: "Hello, Alice"
	
	```

- 变量的值为 `null` 和 `undefined` 时，可以进行空赋值

	```javascript
	let a = null;
	a ??= 5;
	console.log(a);  // 5
	console.log(typeof a);  // number
	```

## 一元运算符

### `+` 和 `-`

- **数值的一元运算符**

  - `+`：取当前符号
  - `-`：取相反符号

  ```javascript
  let a = -10;
  a = +a;
  console.log(a);  // -10
  console.log(typeof a);  // number
  
  let b = -10;
  b = -b;
  console.log(b);  // 10
  console.log(typeof b);  // number
  ```

- **字符串的一元运算符**

  - `+`：自动转换为数值，并取当前符号
  - `-`：自动转换为数值，并取相反符号

  ```javascript
  let a = "-10";
  a = +a;
  console.log(a);  // -10
  console.log(typeof a);  // number
  
  let b = "-10";
  b = -b;
  console.log(b);  // 10
  console.log(typeof b);  // number
  ```

### 自增和自减

- 自增和自减无需再对原变量进行赋值，会立即改变原变量的值
- **自增运算符**：`++`，原变量的值在自身基础上加1

  - `++a`：前自增
  - `a++`：后自增
  - 二者对于原变量 `a` 的自增效果一样，都是在自身基础上加1
  - 二者对于 `自增表达式` 返回的值不同，了解即可
    - `++a` 返回 a 自增后的值
    - `a++` 返回 a 自增前的值

  ```javascript
  // 自增基础用法
  
  let a = 1;
  a++;  // 无需再对a进行赋值，即可改变a的值
  console.log(a);  // 2
  console.log(typeof a);  // number
  ```

  ```javascript
  // 前自增和后自增对比
  
  let a = 1;
  
  console.log(a);  // 1
  console.log(++a);  // 2，返回a自增后的值
  console.log(a);  // 2，经过上一个++a，a变为2
  
  let b = 1;
  
  console.log(b);  // 1
  console.log(b++);  // 1，返回a自增前的值
  console.log(b);  // 2，经过上一个b++，b变为2
  ```

- **练习**

	```javascript
	let n = 5;
	let result = n++ + ++n + n;
	console.log(result);  // 19
	```

	**解释**：

	1. 最开始 n = 5；
	2. 调用第1步的 n = 5，n++ = 5，但此时 n = 6；
	3. 调用第2步的 n = 6，++n = 7，此时 n = 7；
	4. n++ + ++n + n = 5 + 7 +7 = 19。

- **自减运算符**：原变量的值在自身基础上减1，其它同自增运算符

  ```javascript
  let a = 1;
  a--;  // 无需再对a进行赋值，即可改变a的值
  console.log(a);  // 0
  console.log(typeof a);  // number
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

- 当两个值都是数值类型时，即根据数学运算判断得出布尔值

	```javascript
	let a = 5 > 6;
	console.log(a ,typeof a)  // false 'boolean'
	```

- 当两个值都是字符串时，不会自动转换为数值，而是逐位比较字符的 `Unicode编码` 再得出布尔值

	```javascript
	let a = "15" > "6";  // "15"中1的Unicode码在"6"的前面
	console.log(a ,typeof a)  // false 'boolean'
	```

- 当两个值不全是数值/字符串类型时，先自动转换为数值，再进行数学判断得出布尔值

	```javascript
	let a = 5 > "6";  // 先自动将"6"转换成6
	console.log(a ,typeof a)  // false 'boolean'
	```

- **特例**

	- `===` 和 `!==` 运算不会进行自动数据类型转换，如果两个值类型不同，则直接返回 `false`，其它同理。
	- `null`
		- `null` 与其它作比较，会自动转换为 `0`
		- `null` 与 `0` 作比较，只有 `>=` 和 `<=` 会返回 `true`，其余都是 `false`
		- `null == undefined` 会返回 `true`
	- `NaN` 不与任何值（包括本身）等于/相等/全等，都会返回 `false`

## 逻辑运算符

### 逻辑非 `!`

- **基础示例**

	```javascript
	let a = 5;
	a = !a;
	console.log(a ,typeof a)  // false 'boolean'
	```

- **扩展**：如果对其它数据类型进行非运算，系统会先将其转换为布尔值，然后进行非运算

	``` javascript
	let a = true;
	a = !a;
	console.log(a)  // false
	
	let b = 5;
	b = !b;
	console.log(b, typeof b)  // false 'boolean'
	```

- **扩展**：连续取非，将其它数据类型转换为布尔值

	```javascript
	let b = 5;
	console.log(typeof b);  // number
	
	b = !!b;
	console.log(b, typeof b)  // true 'boolean'
	```

### 逻辑与 `&&`

- **基础示例**

  ```javascript
  let a = 5 > 3 && 6 <3;
  console.log(a ,typeof a)  // false 'boolean'
  ```

- **短路运算**：如果第一个值为 `false`，则第二个值不执行，直接返回 `false`；否则执行第二个值

	```javascript
	let res = false && alert(123);
	console.log(res);  // false 不执行alert(123)
	```

	```javascript
	let res = true && alert(123);
	console.log(res)；  // 执行alert(123)
	```

- 如果对其它数据类型进行与运算，系统会先将其转换为布尔值，然后进行与运算，但最终会返回原值

	```javascript
	let a = 1 && 2;  // 2 'number'
	a = 1 && 0;  // 0 'number'
	a = 0 && NaN;  // 0 'number'
	console.log(a ,typeof a)
	```

### 逻辑或 `||`

- **基础示例**

  ```javascript
  let a = 5 > 3 || 6 <3;
  console.log(a ,typeof a)  // true 'boolean'
  ```

- **短路运算**：如果第一个值为 `true`，则第二个值不执行，直接返回 `true`；否则执行第二个

	```javascript
	let res = true || alert(123);  // true 不执行alert(123)
	res = false || alert(123);  // 执行alert(123)
	console.log(res)；
	```

- 如果对其它数据类型进行与运算，系统会先将其转换为布尔值，然后进行与运算，但最终会返回原值

	```javascript
	let a = 1 || 2;  // 1 'number'
	    a = 0 || 1;  // 0 'number'
	    a = 0 || NaN;  // NaN 'number'
	    console.log(a ,typeof a)
	```

## 三元条件运算符

- **语法**：`条件表达式 ? 真值 ： 假值`

  - 如果条件表达式为 `true`，则执行表达式1；
  - 如果条件表达式为 `false`，则执行表达式2。
  
  ```javascript
  true ? alert(1) : alert(2);  // 执行alert(1)
  ```

  ```javascript
  let a = 1;
  let b = 2;
  let max = a > b ? a : b;
  console.log(max);
  ```

## 运算符优先级

1. **括号** `()`
2. **一元运算符** `+`, `-`, `++`, `--`, `!`, `~`, `typeof`, `void`, `delete`
3. **算数运算符**
	1. **指数运算符** `**`
	2. **乘法、除法、取余、取整除** `*`, `/`, `%`
	3. **加法、减法** `+`, `-`
4. **位移运算符** `<<`, `>>`, `>>>`
5. **比较运算符** `==`, `!=`, `===`, `!==`, `<`, `>`, `<=`, `>=`, `instanceof`, `in`
6. **逻辑运算符** `&&`, `||`
7. **赋值运算符** `=`, `+=`, `-=`, `*=`, `/=`, `%=`, `**=`, `<<=`, `>>=`, `&=`, `^=`, `|=`
8. **逗号运算符** `,`

# [选择结构](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Control_flow_and_error_handling)

JS 中有 `if`、`switch` 和 `三元表达式` 三种选择结构，用法同 Java。

## if 语句

- JS 中 `if` 语句的语法格式与 Java 相同。

## switch 语句

- 在 JavaScript 中，`switch` 语句的 `case` 标签不能直接用逗号分隔多个值，因此需要将多个 `case` 分开写。

    ```javascript
    let day = 6;
    
    switch (day) {
      case 1:
      case 2:
      case 3:
      case 4:
      case 5:
        console.log("工作日");
        break;
      case 6:
      case 7:
        console.log("周末");
        break;
      default:
        console.log("未知");
    }
    ```

# [循环结构](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Loops_and_iteration)

- JS 中有 `for`、`for-in`、`for-of`、`while` 和 `do-while` 五种循环结构。
    - 其中 `for`、`while` 和 `do-while` 循环，用法同 Java。
    - 其中 `for-of` 的作用类似于 Java 的 `for-each`，用于遍历可迭代对象。
    - 其中 `for-in` 为 JS 特有，用于遍历对象的 **可枚举属性名**（包括继承的属性）。它也可以用于遍历数组，但它返回的是数组的索引（键名），而不是数组的值。。

- JS 中支持**无限循环**和**循环嵌套**，用法同 Java。

## for-of 循环

- **语法**

    ```javascript
    for (let 变量名 of 可迭代对象){
      循环体;
    }
    ```

    ```javascript
    let arr = ["中国", "上海", 123]
    for (let data of arr) {
      console.log(data);
    }
    ```

## for-in 循环

- **语法**

  ```javascript
  for (let 变量名 in 对象){
    循环体;
  }
  ```
  
  ```javascript
  let user = {name: "张三", age: 18, gender: "男"};
  for (let k in user){
    console.log(1);  // 输出3次1
    console.log(k, user[k]);  // 依次输出属性名和属性值，这里不能使用user.i获取属性值
  }
  ```

# 跳转结构

- JS 中有 `continue`、`break`、`return`、`throw`、`throws` 五种跳转结构，用法同 Java。

# 函数 `function`

在 JS 中，函数是一个特殊的对象，使用 `typeof` 获取到的数据类型为 `function`。

## 创建函数

### 函数声明

- **语法**

	```javascript
	function 函数名(形参列表) {
		函数体
		return 返回值;
	}
	
	函数名(实参列表);  // 调用函数
	```

	```javascript
	function getSum(a, b) {
		let res = console.log(a + b);
		return res;
	}
	
	getSum(1, 1);  // 2
	console.log(typeof getSum);  // function
	```

- **说明**：函数声明创建的函数，存在变量提升。

### 匿名函数

- **语法**

	```javascript
	function(参数列表) {函数体}
	```

	```javascript
	// 作为其它函数的回调函数
	
	let numbers = [1, 2, 3, 4, 5];
	// 使用匿名函数作为forEach的回调函数，这里对每个元素进行翻倍操作
	numbers.forEach(function (element) {
		console.log(element * 2);
	});
	
	
	// 作为其它函数的回调函数
	
	let numbers = [1, 2, 3, 4, 5];
	// 使用匿名函数作为forEach的回调函数，这里对每个元素进行翻倍操作
	numbers.forEach(function (element) {
		console.log(element * 2);
	});
	```

- **函数表达式**：使用变量接收匿名函数。

	```javascript
	const 变量名 = function(参数列表) {
		函数体
		return 返回值;
	};
	```

	```javascript
	const getSum = function(a, b) {
		let res = console.log(a + b);
		return res;
	};
	
	getSum(1, 1);  // 2
	console.log(typeof getSum);  // function
	```

### 箭头函数

箭头函数的语法形式较为灵活，根据 **参数数量** 和 **函数体语句数量** 有不同的写法。

```javascript
// 无参数、单行函数体
const 函数名 = () => 函数体;
```

```javascript
// 当没有参数时，需要使用空括号 () 表示。
const greet = () => 'Hello!';

// 如果只有一个参数，可以省略括号。
const square1 = num => num * num;

// 当有多个参数时，需要用括号将参数括起来。
const square2 = (num1, num2) => num1 * num2;

// 当函数体包含多条语句，需要使用花括号 {} 包裹，并且使用 return 关键字返回值。
const calculate = num => {
    const result = num * 2 + 3;
    return result;
};
```

**说明**

- 箭头函数没有自己的 `this`，`this` 继承自外层作用域。
- 箭头函数没有自己的 `arguments`，它会使用外层函数的 `arguments` 对象。
- 箭头函数不能使用 `yield` 关键字，因此不能用作生成器函数。
- 箭头函数适合用作回调函数。

### 构造函数

- **语法**

	```javascript
	const 函数名 = new Function('参数1', '参数2', '函数体');
	```

	```javascript
	const getSum = new Function('a', 'b', 'console.log(a + b)');
	
	getSum(1, 1);  // 2
	console.log(typeof getSum);  // function
	```

- **扩展**：函数体作为字符串传入，可以动态创建函数，但安全性较低。

### 立即调用函数表达式 (IIFE)

**立即调用函数表达式**（**I**mmediately-**I**nvoked **F**unction **E**xpression，简称 IIFE），也叫做自调用函数，表示函数在定义时就立即调用。

- **语法**

	- 如果声明函数想实现自调用，可以想办法将声明函数矮化成函数表达式
	  - 给函数前面加一些运算符，如 + - () !	
	  - 此法可以省略函数名	
	- 调用方法
	  - 在函数体的代码块后加小括号()
	  - 自调用函数在IIFE结构以外无法被调用

- **函数表达式自调用**

	```javascript
	let foo = function () {
		console.log(1);
	}();  // 1  ()就是自调用
	```

- **声明函数自调用**

	```javascript
	+function fun() {  // 通过+将声明函数矮化成函数表达式，可以替换为-或！
		console.log(1);
	}();  // 自调用函数
	
	(function fun() {  // 通过()将声明函数包围，矮化成函数表达式
		console.log(1);
	})();  // 自调用函数
	```

	```javascript
	// 常用的IIFE结构
	
	(function (a) {  // 通过()将声明函数包围，矮化成函数表达式，并且省略函数名
		console.log(a);
	})(1);  // 1
	```

###  方法定义

### 生成器函数

## 函数其它

### arguments对象

- JS中，函数有一个内置属性 `arguments` 对象，其存储了传递的所有实参。

- 语法

	- arguments是一个伪数组，因此具有数组的一些功能，比如索引，遍历，获取长度...
	- 由于arguments的存在，JS中允许实参和形参个数不一致。
	
	```javascript
	function sum(a, b) {
		console.log(arguments);
	}
	
	sum(1, 2, 3, 4)  // Arguments(4)[1, 2, 3, 4, callee: ƒ, Symbol(Symbol.iterator): ƒ]
	```
	
	```javascript
	function sum(a, b) {
		return a + b;
	}
	
	console.log(sum(1, 2));  // 3
	console.log(sum(1));  // NaN
	console.log(sum(1, 2, 3, 4));  // 3
	```
	
- **示例**：定义一个求和函数，如果传入 1 个参数，返回它自己；如果传入 2 个参数，返回它们的和；如果传入 3 个参数，先比较前两个的大小，大的与第三个参数求和；如果传入 4 个及以上，输出提示错误。

	```javascript
	function sum(a, b, c) {
		switch (arguments.length) {
			case 1:
				return a;
			case 2:
				return a + b;
			case 3:
				return a > b ? a + c : b + c;
			default:
				throw new Error("参数个数不能超过 3 个");
		}
	}
	
	console.log(sum(1));  // 1
	console.log(sum(1, 2));  // 3
	console.log(sum(1, 2, 3));  // 5
	console.log(sum(1, 2, 3, 4));  // 报错
	```

### 函数递归

- 函数内部可以通过函数名调用函数自身的方式，就是函数递归。

- **示例**：定义一个函数，如果传入的参数是1，则返回1；如果传入的数字是1以上的数字，则返回参数 + 函数调用上一项。

	```javascript
	function fun(a) {
		if (a < 1) {
			alert("请输入0以上的整数");
		} else if (a === 1) {
			return 1;
		} else {
			return a + fun(a - 1);  // 函数内部调用自身
		}
	}
	
	console.log(fun(1))
	console.log(fun(3))
	```

# [对象 `object`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object)

**对象**是 JS 中一种复合数据类型 `object`；它用于存储各种键值集合（形式类似于 Python 中的字典）。

JS 中的对象：自定义对象，内置对象，浏览器对象。

## 创建对象

### 字面量方式

- **语法**：`const 对象名 = {属性名1: 属性值1, 属性名2: 属性值2, ...};`

	```javascript
	// 创建一个对象
	const person = {
		name: "Alice", // 定义属性
		age: 25,
	
		// 定义方法
		introduce: function () {
			console.log(`My name is ${this.name}, and I am ${this.age} years old.`);
		}
	};
	
	// 使用对象调用方法
	person.introduce(); // 输出: My name is Alice, and I am 25 years old.
	```

### 构造函数方式

- **语法**：`const 对象名 = new OBJECT();`

	```javascript
	// 定义构造函数
	function Person(name, age) {
		this.name = name; // 初始化 name 属性
		this.age = age;   // 初始化 age 属性
	
		// 添加一个方法
		this.introduce = function () {
			console.log(`My name is ${this.name}, and I am ${this.age} years old.`);
		};
	}
	
	// 创建对象
	const person1 = new Person("Alice", 25);
	const person2 = new Person("Bob", 30);
	
	// 调用方法
	person1.introduce(); // 输出: My name is Alice, and I am 25 years old.
	person2.introduce(); // 输出: My name is Bob, and I am 30 years old.
	```

### 面向对象方式

- **语法**：`const 对象名 = new 类名(属性值1, 属性值2， ...)`

	```javascript
	// 定义类
	class Person {
		// 构造函数
		constructor(name, age) {
			this.name = name; // 初始化 name 属性
			this.age = age;   // 初始化 age 属性
		}
	
		// 定义方法
		introduce() {
			console.log(`My name is ${this.name}, and I am ${this.age} years old.`);
		}
	}
	
	// 创建对象
	const person1 = new Person("Alice", 25);
	const person2 = new Person("Bob", 30);
	
	// 调用方法
	person1.introduce(); // 输出: My name is Alice, and I am 25 years old.
	person2.introduce(); // 输出: My name is Bob, and I am 30 years old.
	```

### 工厂函数方式

- **语法**：`function 函数名(属性1, 属性2, ...) {return {返回值};}`

	```javascript
	// 定义工厂函数
	function createPerson(name, age) {
		# 返回一个包含属性和方法的对象
	  return {
			name: name,
			age: age,
			introduce() {
				console.log(`My name is ${this.name}, and I am ${this.age} years old.`);
			}
		};
	}
	
	// 使用工厂函数创建对象
	const person1 = createPerson("Alice", 25);
	const person2 = createPerson("Bob", 30);
	
	// 调用方法
	person1.introduce(); // 输出: My name is Alice, and I am 25 years old.
	person2.introduce(); // 输出: My name is Bob, and I am 30 years old.
	```

### `Object.create` 方式

- **语法**：`c`

	```javascript
	// 定义一个原型对象
	const personPrototype = {
		introduce() {
			console.log(`My name is ${this.name}, and I am ${this.age} years old.`);
		}
	};
	
	// 使用 Object.create 创建一个新对象
	const person1 = Object.create(personPrototype);
	person1.name = "Alice";
	person1.age = 25;
	
	person1.introduce(); // 输出: My name is Alice, and I am 25 years old.
	```

## 操作属性

### 读取属性

- **语法**：可以通过 **点操作符** (`.`) 或 **方括号** (`[]`) 来访问对象的属性。

	```javascript
	const obj = { name: "Alice", age: 25 };
	
	// 使用点操作符
	console.log(obj.name); // "Alice"
	
	// 使用方括号
	console.log(obj["age"]); // 25
	```

### 增删改查属性

- **以 `.` 为例，`[]` 同理**

	```javascript
	const obj = { name: "Alice" };
	
	// 更新已有属性
	obj.name = "Bob";
	
	// 添加新属性
	obj.age = 25;
	
	// 删除属性
	delete obj.age;
	
	// 检查属性是否存在
	console.log("name" in obj); // false
	```

### 遍历对象

- 详见 [`for-in` 语句](#`for-in` 语句)

# jQuery

jQuery 是一个快速、轻量级、跨浏览器的 JavaScript 库，它简化了 DOM 操作、事件处理、动画效果等任务。

## 版本选择

1. jQuery [官网](https://releases.jquery.com/)
2. **Uncompressed（非压缩版）：**
   - 文件名通常不包含 `.min`，例如：`jquery-3.6.4.js`。
   - 这个版本是未经压缩的，包含所有的注释和可读性更好的代码。通常用于开发和调试目的，方便阅读和调试 jQuery 源码。
3. **Minified（压缩版）***
   - 文件名通常以 ".min.js" 结尾，例如：`jquery-3.6.4.min.js`。
   - 这个版本是经过压缩的，包括了所有 jQuery 功能，但是通过删除不必要的空格、注释等来减小文件大小。
   - 压缩版适合用于生产环境，因为它减小了文件大小，有助于提高页面加载性能。
4. **Slim（精简版）：**
   - 文件名通常包含 `.slim`，例如：`jquery-3.6.4.slim.js`。
   - Slim 版本去除了一些不太常用的功能，例如处理 Ajax 请求的模块，以减小文件大小。适合在项目中需要更轻量级的 jQuery 版本的情况下使用。
5. **Slim Minified（精简压缩版）：**
   - 文件名通常以 `.slim.min.js` 结尾，例如：`jquery-3.6.4.slim.min.js`。
   - 这是 Slim 版本的压缩版，经过了精简和压缩处理，适用于生产环境。

## 引入 jQuery

​	有两种引入方式：使用 CDN（内容分发网络）和本地引入jQuery文件

### 使用 CDN

- **使用 CDN 方式特性**

  - **速度快：** 使用 CDN 可以加速页面加载速度，因为用户可能已经在访问其他网站时加载了相同的 jQuery 版本，从而在访问你的网站时可以从浏览器缓存中获取该文件，而不需要再次下载。
  - **省去本地存储空间：** 不需要将 jQuery 文件存储在本地项目中，可以减少项目大小。
  - **实时更新：** CDN 通常会定期更新和维护文件，因此你的网页可以始终使用最新版本的 jQuery。
  - **简单方便：** 只需在项目中引入一个 `<script>` 标签，就可以使用 jQuery，无需下载和管理本地文件。

- 进入[jQuery官网](https://releases.jquery.com/)，点击 `Minified` 版本，复制引入代码，粘贴到html文件 `<head>` 元素中。

  ```html
  <head>
      <!-- 其它 head 元素 -->
  
      <!-- 使用 CDN 引入 jQuery -->
      <link src="https://code.jquery.com/jquery-3.7.1.min.js">
  </head>
  ```

### 本地引入

- **本地引入方式特性**

  - **离线使用：** 如果你的项目在没有互联网连接的环境中运行，或者你更喜欢掌握自己项目的所有依赖，可以选择下载 jQuery 文件并在本地项目中引入。
  - **更好的控制：** 将 jQuery 文件下载到本地意味着你可以更好地控制文件的版本和更新时间。你可以选择在项目需要时手动更新文件。
  - **不依赖外部网络：** 在使用本地文件的情况下，不需要依赖外部网络资源，这有助于确保你的网页在任何环境中都能正常工作。

- 官网[下载jQuery ](https://code.jquery.com/jquery-3.7.1.js)

- HTML文件同级目录创建名为 `js` 的文件夹，将下载的 `js` 文件复制进该文件夹

  ```html
  <head>
      <!-- 其它 head 元素 -->
  
      <!-- 本地引入 jQuery 文件 -->
  	<script src="js/jquery-3.7.1.js"></script>
  </head>
  ```

## 选择器和筛选器

- 选择器和筛选器

  ``` html
  <div class="c1">
      <div id="c2">北京</div>
      <h1>
          <span class="c1">北京</span>
          <a>北京</a>
      </h1>
      <input type="text"/>
  </div>
  ```

  ``` javascript
  // 选择器
  
  // class选择器
  $(".c1")
  // 标签选择器
  $("h1")
  // ID选择器
  $("c2")
  // 层级选择器
  $(".c1 h1")
  // 属性选择器
  $("input[type=\"text\"]")
  ```

  ``` javascript
  // 筛选器
  
  // 上一个兄弟
  $("h1").prev()
  // 下一个兄弟
  $("h1").next()
  // 所有兄弟
  $("h1").siblings()
  
  // 父亲
  $("h1").parent()  // 即<div class="c1"></div>,可叠加
  // 儿子
  $("h1").children("a")  // 即<a>北京</a>,可叠加
  $("h1").children(".c1")  // 即<span>北京</span>,可叠加
  // 子子孙孙
  $(".c1").find()
  ```


## 读写HTML

- jQuery读写HTML

  ``` javascript
  // 以下tag均为jQuery创建/获取的标签的变量
  
  // 创建标签
  let tag = $("<div>");  // div为标签形式
  
  // 获取标签,可通过各种选择器/筛选器获取标签
  let tag = $("#city");  // city为原HTML标签id
  
  // 添加标签
  tagFather.append(tag);  // 添加至尾部
  tagFarher.prepend(tag);  // 添加至顶部
  
  // 获取标签内容
  let data = tag.text();
  
  // 更改标签内容
  tag.text("666");  // tag 标签变量  666 更改内容
  
  // 获取输入框内容text/password
  let data = tag.val();
  // 清空输入框内容
  tag.val("");
  ```


## 标签转换

- DOM标签和jQuery标签的转换

  ``` javascript
  // DOM标签转换为jQuery标签
  let tag2 = $(tag1);
  // jQuery标签转换为DOM标签
  let tag4 = tag3[0];
  ```


## 框架加载

- 框架加载

  ``` javascript
  $(function (){
      // 当页面框架加载完之后自动执行
      $("#x1").click(function (){
          console.log(123)
      })
  })
  ```


# React

用于构建用户界面的 JavaScript 库，由 Facebook 开发。

## 基本流程

1. **创建项目**

   1. Node.js 已安装，npm 更新至最新版

   2. 创建 React 项目

      ```bash
      npx create-react-app PROJECT_NAME
      ```

   3. 安装组件库

   4. 编写主程序文件和组件文件

2. **本地测试**

   1. 后端与数据库已启动

   2. 调试源文件

      ```bash
      npm start
      ```

3. **生成静态文件**

   1. 在项目的根目录中运行 npm 命令，这将项目根目录中生成一个名为 `build` 的静态文件夹。

      ```bash
      npm run build
      ```

   2. 将 `.gitignore` 中的 build 注释掉

4. **生成 Image**

   1. 使用 GitLab Pipeline 生成 Image

   2. `.gitlab-ci.yml` 按通用格式写

   3. Dockerfile

      ```dockerfile
      FROM node:latest
      WORKDIR /app
      COPY ./build .
      RUN npm install -g http-server
      CMD ["http-server", "-p", "8080"]
      ```

## Reac 管理

- Reac 管理

  ```bash
  # 查看 React 版本
  npm list react
  # 安装 React
  npm install react[@VERSION]
  # 删除 React
  npm uninstall react
  ```

## 组件

### Material UI

​	Material-UI 是一个流行的 React UI 组件库，它基于 Google 的 Material Design 规范，提供了丰富的 React 组件，用于构建美观、易用的用户界面。

- **Material UI 管理**

  ```bash
  # 查看版本
  npm list @mui/material
  
  # 安装 Material UI
  npm install @mui/material @emotion/react @emotion/styled
  # 安装 Material Icons
  npm install @mui/icons-material
  
  # 删除 Material UI
  npm uninstall @mui/material
  ```

- **使用方法**

  1. 注意：组件依赖于 React 不同版本，要根据时下官网进行安装

  2. 此方法以 Material Icons 中的 App Bar 组件为例

  3. [安装组件库 Material UI](https://mui.com/material-ui/getting-started/installation/)

     ```bash
     cd PATH/TO/PROJECT_FILE
     npm install @mui/material @emotion/react @emotion/styled
     ```

  4. [安装图标类 Material Icons](https://mui.com/material-ui/material-icons/)

     ```bash
     cd PATH/TO/PROJECT_FILE
     npm install @mui/icons-material
     ```

  5. [官网搜索 App Bar，复制代码](https://mui.com/material-ui/react-app-bar/)

  6. `src` 文件夹下创建 `components` 文件夹，在里面创建组件文件 `Appbar.js`，粘贴代码

  7. 在主程序文件内引入组件文件 `Appbar.js`，并以标签形式调用 Appbar.js 中的函数

## 主程序文件

- 主程序文件 App.js 有一个主函数，以标签形式调用组件的函数

  源自项目 student-springboot-react-frontend

  ```js
  import './App.css';
  // 引入 Appbar.js 文件
  import Appbar from './components/Appbar';
  // 引入 Student.js 文件
  import Student from './components/Student';
  
  // APP 主函数
  function App() {
    return (
      <div className="App">
        {/* 调用 Appbar.js 中的 Appbar 函数 */}
        <Appbar />
  
        {/* 调用 Student.js 中的 Student 函数 */}
        <Student />
      </div>
    );
  }
  export default App;
  ```

## Router

- From project `Login-flask-react`

- Jump to another page

  ```javascript
  import React, { useState } from 'react';
  import axios from 'axios';
  import { BrowserRouter as Router, Routes, Route, Navigate } from 'react-router-dom';
  import Login from './components/Login';
  import Home from './components/Home';
  
  const App = () => {
    const [isLoggedIn, setIsLoggedIn] = useState(false);
  
    const handleLoginSuccess = () => {
      setIsLoggedIn(true);
    };
  
    return (
      <Router>
        <Routes>
          {/*如果未登录直接访问 Home 页面，则跳转至登录页面*/}
          <Route path="/" element={isLoggedIn ? <Navigate to="/home" /> : <Login onLogin={handleLoginSuccess} />} />
          <Route path="/home" element={isLoggedIn ? <Home /> : <Navigate to="/" />} />
        </Routes>
      </Router>
    );
  };
  
  export default App;
  ```

## 处理方法

### POST 和 GET

- 源自项目 student-springboot-react-frontend

  ```js
  const paperStyle = { padding: '50px 20px', width: 600, margin: '20px auto' }
  
  // POST
  const [name, setName] = React.useState('')
  const [address, setAddress] = React.useState('')
  const handleClick = (e) => {
    e.preventDefault()
    const student = { name, address }
    console.log(student)
    fetch("http://localhost:8080/student/add", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(student)
    }).then(() => {
      console.log("New Student added")
    })
  }
  
  // GET
  const [students, setStudents] = React.useState([])
  React.useEffect(() => {
    fetch("http://localhost:8080/student/getAll")
      .then(res => res.json())
      .then((result) => {
        setStudents(result);
      })
  })
  ```

## React 项目

- Student Spring Boot React Full Stack
- Login Flask React

# Vue.js

用于构建用户界面的渐进式 JavaScript 框架。

