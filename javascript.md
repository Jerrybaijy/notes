---
title: javascript
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - javascript
  - code-language
  - frontend
  - backend
  - web
---

# JavaScript

[**JavaScript**](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript)（JS）是一种基于对象和事件驱动的**脚本语言**，文件的扩展名为 `.js`。**ECMAScript** 是 JavaScript 的官方标准。

<img src="assets/image-20231111155734150.png" alt="image-20231111155734150" style="zoom:50%;" />

## 主要资源

> [ECMAScript 官方文档](https://tc39.es/ecma262/ "ECMAScript")
>
> [MDN 参考](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference)
>
> [MDN JavaScript](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript)：MDN 关于 JavaScript 的主页面

## 环境搭建

安装 Node.js，详见 [`Node.js`](node-js.md#环境搭建) 笔记。

## 代码规范

- **大小写**：敏感
- **缩进**：不敏感，通常缩进2个空格。
- **分号**：行尾加 `;`
- **空白行**：不敏感
- **换行**：不敏感

## 标识符

- 只能含有字母、数字、下划线、$，且不能以数字开头
- 大小写敏感
- 不能是[关键字和保留字](https://tc39.es/ecma262/#sec-keywords-and-reserved-words)

## 注释

**JavaScript 注释**：

- 单行注释：`Ctrl + /`
- 多行注释：`Ctrl + Shift + /`

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

## 输入与输出

### 输入

**语法**：`prompt("提示语")`

```javascript
let a = prompt("请输入用户名");
console.log(a);
```

**扩展**：`prompt()` 可以输入默认参数

```javascript
let a = prompt("请输入用户名", "张三");
console.log(a);
```

### 输出

**语法**：`console.log("输出内容")`

```javascript
console.log("你猜我在哪？");
```

**查看**：`Live server` 在浏览器查看 `HTML`，浏览器控制台查看输出结果，`F12`。

**扩展**：

- 弹窗：`alert("哈哈哈");`
- 网页输出：`document.write("你猜我在哪");`，注意此种方法在引入脚本时不能使用 `defer`。

## `this`

[`this`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/this) 是 JavaScript 中的一个特殊关键字，用于引用当前上下文中的对象。`this` 的值在不同的场景中会有所不同，其行为依赖于**函数调用的方式**。

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

## 声明变量

### 语法

声明变量：

- 使用关键字
- 不需要指定数据类型

```javascript
// 声明变量并赋值
let myVariable = 19;
console.log(age); // 19
```

重新赋值：

```javascript
let myVariable = 19;

// 给变量重新赋值
myVariable = 20;
console.log(age); // 20
```

### 声明关键字和变量提升

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

# 数据类型

- JS 是一种**弱类型语言**，不用提前声明变量的数据类型，在程序运行过程中，变量的数据类型会被自动确定。

    - 虽说是**弱类型语言**，但各种数据类型在程序执行的时候，会很灵活地自动转换 ，所以要格外小心。

- [**JavaScript 数据类型**](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Data_structures)
  - **原始值**：基本数据类型
  - **对象**：复杂数据类型（或称为引用数据类型）

## 原始值

[**原始值**](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Data_structures#原始值)，除了 `Object` 以外，所有的类型都定义了[不可变的](https://developer.mozilla.org/zh-CN/docs/Glossary/Immutable)、在语言最底层直接表示的值。我们将这些类型的值称为**原始值**，一共7种。

- **`number`**：数字
- **`bigInt`**：大整数
- **`boolean`**：布尔值
- **`string`**：字符串
- **`null`**：空值
- **`undefined`**：未定义
- **`symbol`**：标识

**说明**：原始值是不可变类型，一旦创建，就不能修改。

## `number`

[`number`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Data_structures#number_类型) 类型用于保存整数或浮点数，属于原始值。

- JS 中位数多的 `number` 在输出时不会十分精确，应该使用 `bigint`。
- 浮点数运算时不会十分精确。

### 进制

**JS 中的进制**：

- 常见的进制有二进制、八进制、十进制和十六进制;
- 在 JS 中还可以用八进制和十六进制，输出时统一用十进制表示；

**八进制**：

- 在数字开头加上0，表示八进制数，八进制数由0~7组成，逢8进位。

  ```javascript
  let num1 = 07;
  console.log(num1);  // 7
  
  let num2 = 010;
  console.log(num2);  // 8
  ```

**十六进制**：

- 在数字开头加上 `0x`，表示十六进制数，十六进制数由 `0-9` 和 `a-f` 组成。
- 十六进制数中的 `x` 和 `a~f` 不区分大小写。

    ```javascript
    let numl = 0x9;
    console.log((numl);  // 9
    let num2 = Oxa;
    console.log(num2);  // 10
    ```

### 范围

`number` 有一定的范围：

```javascript
console.log(Number.MAX_VALUE);  // 1.7976931348623157e+308
console.log(Number.MIN_VALUE);  // 5e-324
```

### 特殊值

`number` 有3个特殊值：

- `Infinity` ：无穷大；
  - 大于或等于2的1024次方的数值，JS 无法表示，会返回 `Infinity`。

- `-Infinity` ：无穷小；
- `NaN` ：非数字（Not a Number）；
  - 使用 `isNaN()` 函数检查一个数值是不是 `NaN`，返回 `true` 或 `false`。

## `bigint`

**大整数** [`bigint`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Data_structures#bigint_类型) 用于表示任意精度整数，没有位数的限制，即使超出 `number` 能够表示的安全整数范围，属于原始值。

- `bigint` 表示一些数值比较大的整数
- `bigint` 必须添加后缀 `n`
- `bigint` 与 `number` 是两种值，它们之间并不相等，例如 `100 == 100n;  // false`

## `boolean`

**布尔值** [`boolean`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Data_structures#boolean_类型) 首字母**小写**：`true` 和 `false`，属于原始值。

```javascript
let a = true;
let b = false;
console.log(5 > 3);  // true
console.log(6 < 2);  // false
```

以下类型或值会返回 `false`，其余都返回 `true`：

- `false`
- `undefined`
- `null`
- `0`
- `NaN`
- `''` 空字符串

## `string`

**字符串** [`string`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Data_structures#string_类型) 属于原始值。

### 基础

```javascript
// 字面量方式
let str1 = "hello world";  // 文本形式的字符串
let str2 = "";  // 空字符串
let str3 = "6";  // 数值形式的字符串

// 构造函数方式
let str = new String();  // String 首字母大写，此处 new 可以省略
```

**基本包装类型**： JS 中，只有对象数据类型才有属性和方法，原始值没有。但通过基本类型包装，会暂时将字符串包装成一个对象，可以使字符串暂时拥有属性和方法，结束后对象再被销毁。

### 字符串索引

#### 语法

**语法**：`STR[索引号]`，返回 `string`。

```javascript
//         0 1 2 3 4 5，正向索引号
let str = "中国江西联通";
console.log(str[0]);  // 中
console.log(str[-5]);  // undefined
console.log(typeof str[0]);  // string
```

**注意**：JS 不支持直接逆向索引，会返回 `undefined`。

#### 多级索引

`Arry[一级索引号][二级索引号]...`，返回 `string`。

```javascript
let arr = ["中国", ["上海", "北京", "深圳"], 123];
let str1 = arr[1][0];
let str2 = arr[1][0][0];
console.log(str1);  // 上海
console.log(str2);  // 上
```

#### 扩展

**变相逆向索引**：`STR[STR.length - 索引号]`，返回 `string`。

```javascript
let str = "中国江西联通";
console.log(str[str.length-5]);  // 国
```

**示例**：

```javascript
let str = "中国江西联通";
let index = 0;  // index 为索引号
while (index < str.length) {
    let strNew = str[index];
    console.log(strNew);
    index += 1;
}

// 依次打印“中国江西联通”
```

### 模板字符串

**语法**：用反引号 <code>\`</code> 包围字符串

```javascript
let a = `Hello World`;
```

**跨行输出**：

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

**嵌套变量 + 拼接**：

```javascript
let a = "你好";  // a 可以是任意数据类型
let b = `${a}世界`;  // 注意此处的 $ 是语法的一部分
console.log(b);  // 你好世界
```

### `concat()`

[`concat()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/split) 方法用于合并字符串。

**语法**：`STR.concat(任意数据类型)`，返回 `string`。

```javascript
let str1 = "abc";

let str2 = str1.concat("def");  // 参数为字符串字面量
let str3 = str1.concat(null, 4, "f");  // 参数为零散的任意数据类型

console.log(str2);  // abcdef
console.log(typeof str2)  // string

console.log(str3);  // abcnull4f
console.log(typeof str3)  // string
```

### `includes()`

[`includes()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/includes) 方法用于判断是否可以在一个字符串中找到另一个字符串。

**语法**：`STR.includes(元素)`，返回 `boolean`。

```javascript
let str = "中国联通";
let res = str.includes("中国");
console.log(res);  // true
```

### `indexOf()`

**找下标** [`indexOf()`](http://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/indexOf) 用于找字符串中某个字符的索引号。

**语法**：`STR.indexOf("匹配项")`，返回 `number`。

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

### `length`

`length` 属性用于表示字符串长度。

**语法**：`STR.length`，返回 `number`。

```javascript
let str = "中国江西联通"
let res = str.length;
console.log(res);  // 6
console.log(typeof res);  // number
```

### `replace()`

[`replace()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/replace) 方法用于替换字符串中的一段序列。

**语法**：`STR.replace("旧元素", "新元素")`，返回 `string`。

```javascript
let str = " 中国 联通 联通 ";
let res = str.replace("联通", "移动");
console.log(res);  // " 中国 移动 联通 "
```

**说明**：JS中，`replace()` 只能替换一个符合要求元素（最左侧一个）。

### `slice()`

**切片** [`slice()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/slice) 用于提取字符串的一部分。

**语法**：`STR.slice(INDEX_START, INDEX_END)`，返回 `string`。

```javascript
//      0 1 2 3 4 5，正向索引号
let str = "中国江西联通";

console.log(str.slice(2, 4));  // 江西
console.log(str.slice(2));  // 江西联通（可省略终结索引号）
```

**扩展**：`slice()` 支持逆向索引。

**注意**：JS 不支持索引直接切片。

### `split()`

**切割** [`split()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/split) 方法用于根据切割标识切割字符串。

**语法**：`STR.split(切割标识)`，返回 `Arry`。

```javascript
let str = "马化腾,40,XXXX@qq.com";
let res = str.split(",")  // ","为切割标识

console.log(res);  // ['马化腾', '40', 'XXXX@qq.com']
```

**综合示例**：

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

### `startsWith()`

[`startsWith()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/startsWith) 方法用来判断当前字符串是否以另外一个给定的子字符串开头。

**语法**：`STR.startsWith()`，返回 `boolean`。

```javascript
let str = "中国联通";
let res = str.startsWith("中国");
console.log(res);  // true
```

### `toUpperCase()`

[`toUpperCase()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/toUpperCase) 方法用于将字符串转换为大写形式。

[`toLowerCase()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/toLowerCase) 方法用于将字符串转换为小写形式。

**语法**：`STR.toUpperCase()`，返回 `string`。

```javascript
let str = "abc";
let res = str.toUpperCase();
console.log(res);  // ABC
```

### `trim()`

 [`trim()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/trim) 方法用于去除字符串两端的空格 ` ` 或换行符 `\n`。

**语法**：`STR.trim()`，返回 `string`。

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

let res4 = str.trim();
console.log(res4);  // 中国联通（后面没有换行）
```

**扩展**：`trim()` 不能去除中间的空格，去除中间空格应使用 `str.replace(" ", "")`，将空格替换成空白。

### 其它操作

- 遍历：详见 [for-of 语句](#for-of 语句)
- 判断数字：
    - JS 中没有方法直接判断一个字符串是否是数字形式的字符串
    - 可以结合正则表达式判断

## `null`

JS 中，**空值** [`null`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Data_structures#null_类型) 的字面量是 `null`，数据类型是 `object`，[点击查看原因](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/typeof#typeof_null)，属于原始值。

从逻辑角度，`null` 表示空对象指针。

## `undefined`

**未定义** [`undefined`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Data_structures#undefined_类型) 类型只有一个值：`undefined`。

## `symbol`

**标识** [`symbol`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Data_structures#symbol_类型) 指的是独一无二的值，这是 ES6 新增的数据类型，属于原始值。

- 每个通过 `Symbol()` 生成的值都是唯一的。

- `symbol` 类型的对象永远不相等，即便创建的时候传入相同的值。

```javascript
let a = Symbol();
let b = Symbol();
console.log(a);  // Symbol()
console.log(typeof a);  // symbol
console.log(a == b);  // false
```

## 获取数据类型

[`typeof`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/typeof) 运算符返回一个字符串，表示操作数的类型。

```javascript
let str = "中国江西联通";
console.log(typeof str);  // string
```

`typeof` [可能的返回值](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/typeof#描述)：

<iframe
  src="https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/typeof#描述"
  width="100%"
  height="800"
  title="嵌入的 MDN 页面"
  >你的设备不支持嵌入
</iframe>

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

- 关于数据的可变性，详见 [`code-general | 数据的可变性`](code-general.md/#强类型和弱类型) 笔记。
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

> [表达式和运算符](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators)

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

> [逻辑运算符](https://developer.mozilla.org/zh-CN/docs/Learn_web_development/Core/Scripting/Conditionals#逻辑运算符：与、或、非)

### 逻辑非 `!`

**基础示例**：

```javascript
let a = 5;
a = !a;
console.log(a ,typeof a)  // false 'boolean'
```

**扩展**：如果对其它数据类型进行非运算，系统会先将其转换为布尔值，然后进行非运算。

``` javascript
let a = true;
a = !a;
console.log(a)  // false

let b = 5;
b = !b;
console.log(b, typeof b)  // false 'boolean'
```

**扩展**：连续取非，将其它数据类型转换为布尔值。

```javascript
let b = 5;
console.log(typeof b);  // number

b = !!b;
console.log(b, typeof b)  // true 'boolean'
```

### 逻辑与 `&&`

**基础示例**：

```javascript
let a = 5 > 3 && 6 <3;
console.log(a ,typeof a)  // false 'boolean'
```

**短路运算**：如果第一个值为 `false`，则第二个值不执行，直接返回 `false`；否则执行第二个值。

```javascript
let res = false && alert(123);
console.log(res);  // false 不执行alert(123)
```

```javascript
let res = true && alert(123);
console.log(res)；  // 执行alert(123)
```

如果对其它数据类型进行与运算，系统会先将其转换为布尔值，然后进行与运算，但最终会返回原值。

```javascript
let a = 1 && 2;  // 2 'number'
a = 1 && 0;  // 0 'number'
a = 0 && NaN;  // 0 'number'
console.log(a ,typeof a)
```

### 逻辑或 `||`

**基础示例**：

```javascript
let a = 5 > 3 || 6 <3;
console.log(a ,typeof a)  // true 'boolean'
```

**短路运算**：如果第一个值为 `true`，则第二个值不执行，直接返回 `true`；否则执行第二个。

```javascript
let res = true || alert(123);  // true 不执行alert(123)
res = false || alert(123);  // 执行alert(123)
console.log(res)；
```

如果对其它数据类型进行与运算，系统会先将其转换为布尔值，然后进行与运算，但最终会返回原值。

```javascript
let a = 1 || 2;  // 1 'number'
    a = 0 || 1;  // 0 'number'
    a = 0 || NaN;  // NaN 'number'
    console.log(a ,typeof a)
```

## 三元条件运算符

详见[三元表达式](#三元表达式)。

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

# 选择结构

JS 中有 `if`、`switch` 和 `三元表达式` 三种[选择结构](https://developer.mozilla.org/zh-CN/docs/Learn_web_development/Core/Scripting/Conditionals)。

## if 语句

### if

```javascript
if (条件表达式) {
  // 执行语句;
}
```

```javascript
let score = 85;

if (score >= 60) {
  console.log("及格！");
}
```

### if-else

> [if-else](https://developer.mozilla.org/zh-CN/docs/Learn_web_development/Core/Scripting/Conditionals#if...else_语句)

```javascript
if (条件表达式) {
  // 执行语句A;
} else {
  // 执行语句B;
}
```

```javascript
let score = 85;

if (score >= 60) {
  console.log("及格！");
} else {
  console.log("不及格！");
}
```

### if-else if-else

> [else if](https://developer.mozilla.org/zh-CN/docs/Learn_web_development/Core/Scripting/Conditionals#else_if)

```javascript
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

```javascript
let score = 85;

if (score >= 90) {
  console.log("优秀！");
} else if (score >= 80) {
  console.log("良好！");
} else if (score >= 60) {
  console.log("及格！");
} else {
  console.log("不及格！");
}
```

## switch 语句

>  [switch 语句](https://developer.mozilla.org/zh-CN/docs/Learn_web_development/Core/Scripting/Conditionals#switch_语句)

### 语法

```javascript
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

```javascript
let status = "Processing";

switch (status) {
  case "New":
    console.log("订单是新的");
    break;
  case "Processing":
    console.log("订单正在处理中");
    break;
  case "Completed":
    console.log("订单已完成");
    break;
  default:
    console.log("未知订单状态");
}
```

### 多值匹配

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

## 三元表达式

> [三元表达式](https://developer.mozilla.org/zh-CN/docs/Learn_web_development/Core/Scripting/Conditionals#三元运算符)

```javascript
条件表达式 ? 真值 : 假值
```

```javascript
let score = 80;
let result = score >= 60 ? "及格" : "不及格";
console.log(result); // 及格
```

# 循环结构

JS 中有 `for`、`for-in`、`for-of`、`while` 和 `do-while` 五种[循环结构](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Loops_and_iteration)。

## for 语句

```javascript
for (初始化表达式; 条件表达式; 更新表达式) {
  // 循环体;
}
```

```javascript
for (let i = 0; i <= 5; i++) {
  console.log(i); // 依次输出：0 1 2 3 4 5
}
```

**扩展**：可用“for 循环 + 索引”进行遍历

```javascript
let arr = ["中国", "上海", "北京"];

for (let i = 0; i < arr.length; i++) {
  console.log(arr[i]); // 依次输出：中国 上海 北京
}
```

## for-of 语句

```javascript
for (let 变量名 of 可迭代对象){
  // 循环体;
}
```

```javascript
let arr = ["中国", "上海", 123]
for (let data of arr) {
  console.log(data); // 依次输出：中国 上海 123
}
```

## for-in 语句

```javascript
for (let 变量名 in 对象){
  // 循环体;
}
```

```javascript
let user = {name: "张三", age: 18, gender: "男"};
for (let k in user){
  console.log(1);  // 输出3次1
  console.log(k, user[k]);  // 依次输出属性名和属性值，这里不能使用user.i获取属性值
}
```

**注意**：在 JS 中，`for-in` 语句在遍历数组时，返回的是数组的索引（键名），而不是数组的值。

## while 语句

```javascript
while (条件表达式) {
  // 循环体;
}
```

```javascript
let i = 1;
while (i <= 3) {
  console.log("第" + i + "次打印：Hello World!");
  i += 1; // 条件迭代
}
```

## do-while 语句

```javascript
do {
  // 循环体;
} while (条件表达式);
```

```javascript
let i = 1;
do {
  console.log("第" + i + "次打印：Hello World!");
  i += 1; // 条件迭代
} while (i <= 3);
```

## 无限循环

```javascript
while (true) {
  // 循环体;
}
```

```javascript
do {
  // 循环体;
} while (true);
```

```javascript
for (;;){
  // 循环体;
}
```

# 跳转结构

JS 中有 `continue`、`break`、`return`、`throw`、`throws` 五种跳转结构。

[`continue`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Loops_and_iteration#continue_语句) 和 [`break`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Loops_and_iteration#break_语句) 示例：

```javascript
for (let year = 1; year < 11; year++) {
  if (year === 5) {
    console.log("第5年疫情原因，今年不用还款了！");
    // 此处如果没有 continue，会同时正常显示：第五年到了，还款1.2万。
    continue; // 第5年不用还，本次循环结束，进入下一次该循环，第6年。
  }
  if (year === 6) {
    console.log("第" + year + "年到了！还款2.4万！");
    continue; // 第6年还2.4万，本次循环结束，进入下一次该循环，第7年。
  }
  if (year === 8) {
    console.log("第8年，提前还清，以后都不用还了！");
    break; // 从第9年不用再还款了，当前循环结束。
  }
  console.log("第" + year + "年到了！还款1.2万！");
}
```

# Function

在 JS 中，函数是一个特殊的对象，使用 `typeof` 获取到的数据类型为 `function`。

## 创建函数

### 函数声明

**说明**：函数声明创建的函数，存在变量提升。

```javascript
function 函数名(形参列表) {
  // 函数体;
  return 返回值;
}

// 调用函数
函数名(实参列表);
```

```javascript
function getSum(a, b) {
  let res = console.log(a + b);
  return res;
}

getSum(1, 1); // 2
console.log(typeof getSum); // function
```

### 匿名函数

```javascript
function(参数列表) {函数体;}
```

```javascript
// 作为其它函数的回调函数

let numbers = [1, 2, 3, 4, 5];
// 使用匿名函数作为 forEach 的回调函数，这里对每个元素进行翻倍操作
numbers.forEach(function (element) {
  console.log(element * 2);
});
```

### 函数表达式

**函数表达式**：使用变量接收匿名函数。

```javascript
const 变量名 = function (参数列表) {
  函数体;
  return 返回值;
};
```

```javascript
const getSum = function (a, b) {
  let res = console.log(a + b);
  return res;
};

getSum(1, 1); // 2
console.log(typeof getSum); // function
```

### 箭头函数

箭头函数的语法形式较为灵活，根据 *参数数量* 和 *函数体语句数量* 有不同的写法。

```javascript
// 无参数、单行函数体
const 函数名 = (参数列表) => 函数体;
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

**语法**：

- 如果声明函数想实现自调用，可以想办法将声明函数矮化成函数表达式

  - 给函数前面加一些运算符，如 + - () !
  - 此法可以省略函数名

- 调用方法

  - 在函数体的代码块后加小括号()
  - 自调用函数在IIFE结构以外无法被调用

**函数表达式自调用**：

```javascript
let foo = function () {
  console.log(1);
}();  // 1  ()就是自调用
```

**声明函数自调用**：

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

#### 语法

JS中，函数有一个内置属性 `arguments` 对象，其存储了传递的所有实参。

- `arguments` 是一个伪数组，因此具有数组的一些功能，比如索引，遍历，获取长度...。
- 由于 `arguments` 的存在，JS 中允许实参和形参个数不一致。

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

#### 示例

定义一个求和函数，如果传入 1 个参数，返回它自己；如果传入 2 个参数，返回它们的和；如果传入 3 个参数，先比较前两个的大小，大的与第三个参数求和；如果传入 4 个及以上，输出提示错误。

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

console.log(sum(1)); // 1
console.log(sum(1, 2)); // 3
console.log(sum(1, 2, 3)); // 5
console.log(sum(1, 2, 3, 4)); // 报错
```

### 函数递归

函数内部可以通过函数名调用函数自身的方式，就是**函数递归**。

**示例**：定义一个函数，如果传入的参数是1，则返回1；如果传入的数字是1以上的数字，则返回参数 + 函数调用上一项。

```javascript
function fun(a) {
  if (a < 1) {
    alert("请输入0以上的整数");
  } else if (a === 1) {
    return 1;
  } else {
    return a + fun(a - 1); // 函数内部调用自身
  }
}

console.log(fun(1));
console.log(fun(3));
```

# [Object](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object)

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
      },
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
      this.age = age; // 初始化 age 属性
    
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
        this.age = age; // 初始化 age 属性
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
      // 返回一个包含属性和方法的对象
      return {
        name: name,
        age: age,
        introduce() {
          console.log(`My name is ${this.name}, and I am ${this.age} years old.`);
        },
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
      },
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

## `Array`

### 语法

**数组** [`Array`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array) 对象可以存储**不同**数据类型的元素，是一个特殊的**对象**，数据类型为 `object`。

对数组操作以后，原数组会改变。

**语法**：`[元素1, 元素2, ..., 元素n]`

```javascript
// 字面量方式
let arr = ["中国", "上海", 123];

// 构造函数方式
let arr = Array();  // []
```

```javascript
let arr = ["中国", "上海", 123];
console.log(arr);  // ['中国', '上海', 123]
console.log(typeof arr);  // object
```

**公共功能**：

- 以下功能详见字符串
- 获取长度 `.length`
- 索引（JS 不可索引切片）
- 遍历 `for-of 语句`
- ~~JS 中数组没有 `in` 包含功能~~
- 嵌套
- 切片 `.slice()`
- 合并 `.concat()`

**其它功能**：

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

### 数组索引

#### 语法

数组索引的基础用法同[字符串索引](#字符串索引)。

#### 数组索引赋值

**语法**：`数组名[索引号] = 元素`，原数组被改变。

```javascript
let arr = [1, 2, 3, 4];
arr[0] = 5;
console.log(arr);  // [5, 2, 3, 4]
```

**扩展**：如果索引号超过数组最大项，会创建新元素，并在新元素与旧元素之间创建空属性，同时被动增加数组长度。

```javascript
let arr = [1, 2, 3, 4];
arr[6] = 5;  // 索引号超过数组最大项
console.log(arr);  // [1, 2, 3, 4, 空属性 × 2, 5]
console.log(arr[4], arr[5])  // undefined undefined
console.log(arr.length);  // 7
```

### 数组长度

数组长度 [`length`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/length) 基础用法同字符串 [`length`](#`length`)。

通过数组长度删除元素：`ARRAY.length = 长度值;`，原数组被改变。

```javascript
let arr = [1, 2, 3, 4];
arr.length = 2;
console.log(arr); // [1, 2]
console.log(arr.length); // 2
```

### `join()`

[`join()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/join) 方法用于将一个数组的所有元素连接成一个字符串并返回这个字符串，用逗号或指定的分隔符对字符串进行分隔。如果数组只有一个元素，那么将返回该元素而不使用分隔符。

**语法**：`ARRAY.join(["SEPARATION"])`，返回字符串 `str`。

```javascript
let arr = ["中国", "上海", 123];
let res = arr.join("_");  // "_"为分隔符
console.log(res);  // 中国_上海_123
console.log(arr);  // ["中国", "上海", 123]
```

### `push()`

[`push()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/push) 方法将指定的元素添加到数组的末尾，并返回新的数组长度。

**语法**：`ARRAY.push(元素1, 元素2, ..., 元素n)`，原数组被改变，返回原数组被改变之后的长度 `number`。

```javascript
let arr = [1, 2, 3, 4];
let res = arr.push(5, 6, 7, 8);

console.log(arr);  // [1, 2, 3, 4, 5, 6, 7, 8]
console.log(res);  // 8  // 返回原数组被改变之后的长度
console.log(typeof res);  // number
```

**扩展**：使用扩展运算符添加元素 `[...数组名, 元素1, 元素2, ...]`，原数组不被改变。

```javascript
let arr = [1, 2, 3, 4];
let arrStart = [...arr, 5, 6, 7, 8];
let arrEnd = [5, 6, 7, 8, ...arr];

console.log(arr);  // [1, 2, 3, 4]
console.log(arrStart);  // [1, 2, 3, 4, 5, 6, 7, 8]
console.log(arrEnd);  // [5, 6, 7, 8, 1, 2, 3, 4]
```

### `reverse()`

[`reverse()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse) 方法用于反转数组中的元素，并返回同一数组的引用。

**语法**：`数组名.reverse()`，原数组被改变，返回同一数组的引用。

```javascript
let arr = [1, 2, 3, 4];
let res = arr.reverse();

console.log(arr);  // [4, 3, 2, 1]
console.log(res);  // [4, 3, 2, 1]
console.log(typeof res);  // object
```

**扩展**：`数组名.toReversed()` 方法，原数组不被改变。

### `sort()`

[`sort()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) 方法用于对数组的元素进行排序，并返回对相同数组的引用。

**语法**：`数组名.sort()`

```javascript
let arr = ["80", "9", "700", 40, 1, 5, 200];
let res = arr.sort();

console.log(arr);  // [1, 200, 40, 5, '700', '80', '9']
console.log(res);  // [1, 200, 40, 5, '700', '80', '9']  // 返回升序之后的原数组
```

**说明**：默认排序是将元素转换为字符串，然后按照它们的 UTF-16 码元值升序排序。

**扩展**：`数组名.toSorted()` 方法，原数组不被改变。

**扩展**：以下方法按数字大小进行升序排序

```javascript
let arr = ["80", "9", "700", 40, 1, 5, 200];
function compareFn(a, b) {
  return a - b;
}
let res = arr.sort(compareFn);

console.log(arr);  // [1, 5, '9', 40, '80', 200, '700']
console.log(res);  // [1, 5, '9', 40, '80', 200, '700']
```

### `splice()`

[`splice()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/splice) 方法用于在数组中插入、替换和删除元素。

**语法**：`ARRAY.splice(开始索引, 删除数量[, 元素1, 元素2, ..., 元素n])`，原数组被改变，返回被删除元素组成的 `Array`。

```javascript
// 插入
let arr1 = [1, 2, 3, 4];
let res1 = arr1.splice(0, 0, 5, 6, 7, 8);  // 从第0索引号删除0个，插入 5, 6, 7, 8
console.log(arr1);  // [5, 6, 7, 8, 1, 2, 3, 4]
console.log(res1);  // []  // 返回被删除元素组成的数组
console.log(typeof res1);  // object

// 替换
let arr2 = [1, 2, 3, 4];
let res2 = arr2.splice(1, 2, 22, 33);  // 从第1索引号删除2个元素，并插入 22, 33
console.log(arr2);  // [1, 22, 33, 4]
console.log(res2);  // [2, 3]  // 返回被删除元素组成的数组
console.log(typeof res2);  // object

// 删除
let arr3 = [1, 2, 3, 4];
let res3 = arr3.splice(1, 2);  // 从第1索引号删除2个，不插入新元素
console.log(arr3);  // [1, 4]
console.log(res3);  // [2, 3]  // 返回被删除元素组成的数组
console.log(typeof res3);  // object
```

**扩展**：`toSpliced()` 方法，原数组不被改变。

### 其它操作

- [`length`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/length)：表示数组长度的属性，用法同 [`length`](#`length`)。

