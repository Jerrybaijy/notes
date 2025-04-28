# Solidity

## Solidity

[Solidity](https://docs.soliditylang.org/zh-cn) 是一门为实现智能合约而创建的面向对象的高级编程语言。智能合约是控制 Ethereum 状态中账户行为的程序。

- Solidity 是一个开源的社区项目，由一个核心团队管理。
- Solidity 受 C++ 的影响最深，但也借用了 Python，JavaScript 等语言的概念。

**Solidity 的特点**：

- 面向对象
- 静态类型
- 强类型

**Solidity 资源**：

- [Solidity 资源](https://docs.soliditylang.org/zh-cn/latest/resources.html)
- [Solidity Docs](https://docs.soliditylang.org/zh-cn)
- [Solidity by Example](https://solidity-by-example.org/)
- [Course on Hackquest](https://www.hackquest.io/zh-cn/home)

## 代码风格

- [Solidity 代码风格指南](https://docs.soliditylang.org/zh-cn/latest/style-guide.html#maximum-line-length)

### 标识符

- **标识符规范**
- **命名习惯**
    - **合约**：大驼峰
    - **结构体**：大驼峰
    - **结构体属性**：num_Student
    - **函数**：小驼峰
    - **函数参数**：小驼峰
    - **局部变量和状态变量**：小驼峰
    - **常量**：大蛇形

## 注释

- 单行注释（ `//` ）和多行注释（ `/*...*/` ）

    ```solidity
    // SPDX-License-Identifier: MIT
    pragma solidity ^0.8.0;
    
    // 这是一个单行注释，描述下面的合约。
    contract HelloWorld {
        // 这是一个单行注释，描述下面的方法。
        function sayHello() public pure returns (string memory) {
            /*
             * 多行注释第一行
             * 多行注释第二行
             * 多行注释第三行
             * 这里是对下面的返回代码块的解释。
             */
            return "Hello World";
        }
    }    
    ```

- NatSpec 注释（ `///`）和（ `/** ... */`），它们应该直接用在函数声明或语句之上。

    ```solidity
    // SPDX-License-Identifier: GPL-3.0
    pragma solidity >=0.4.16 <0.9.0;
    
    /// @author Solidity团队
    /// @title 一个简单的存储例子
    contract SimpleStorage {
        uint storedData;
    
        /// 存储 `x`。
        /// @param x 要存储的新值
        /// @dev 将数字存储在状态变量 `storedData` 中
        function set(uint x) public {
            storedData = x;
        }
    
        /// 返回存储的值。
        /// @dev 检索状态变量 `storedData` 的值
        /// @return 存储的值
        function get() public view returns (uint) {
            return storedData;
        }
    }
    ```

# 变量

## 声明变量

```solidity
int a = 10;
```

## State Variable

**状态变量**（State Variable）是在函数外部声明的变量。如果这个信息应该被记录在区块链上，则将其设置为状态变量。状态变量通常需要更多的 gas 来读写，所以应当仅在必要时使用。

```solidity
contract ContractName {
    //这是一个状态变量
    int a;

    function add(int b) returns (int) {
        //b被定义为函数的输入参数，所以它不是状态变量
        //c是在函数中定义的，所以它也不是状态变量
        int c = a + b;
        return c;
    }
}
```

## Local Variable

**局部变量**（Local Variable）是在函数内部声明的变量，其作用域仅限于该函数内部。

# 数据类型

## 整型

`int` / `uint`：分别表示**有符号**和**无符号**的整型变量。 可以在 uint 或 int 后面添加位数，以指定 uint 和 int 类型所存储的 bit 位大小。

- 位数可以从 8 到 256，而且必须是 8 的倍数。
- `int` 和 `uint` 分别是 `int256` 和 `uint256` 的别名。

```solidity
uint8 a;
int256 b;
int128 c;
uint127 d; //这不是有效的，因为127不是8的倍数。
```

## bool

`bool` ：可能的取值为常数值 `true` 和 `false`。

## address

### address

地址（address）是以太坊区块链上账户或智能合约的唯一标识符。

地址占20个字节，一个字节有8个 bit ,所以地址共有160个 *bit*，一个字节需要两个十六进制数表示，所以需要40个十六进制数表示一个地址。

```solidity
//定义
address address1 = 0x35701d003AF0e05D539c6c71bF9421728426b8A0;

//在以太坊中，每个地址都有一个成员变量，即地址的余额balance
//余额以 uint 形式存在，因为它永远不可能为负值
uint balance = address1.balance;
```

地址分为两类：账户地址或合约地址。

- **账户地址**：它是由用户创建的用于接收或发送资金的地址，由用户控制，也称为钱包。
- **合约地址**：与“账户地址”相反，“合约地址”由合约（程序）控制。将合约放在以太坊上时，系统会为它生成一个独特的地址。其他人通过这个地址与合约进行交互。

### payable

在 Solidity 中，只能对申明为 payable 的地址进行转账。

```solidity
address payable add;

//类型转换
address add1 = 0x5B38Da6a701c568545dCfcB03FcB875f56beddC4;
address payable add2 = payable(add1); //使用 payable() 显式转换
address add3 = add2; //隐式转换

//转账
//从当前合约向address1转移5 Wei
address1.transfer(5);
```

## string

```solidity
string myString = "I will be back!";

//String 作为参数时必须指定其存储的位置，在大多数场景中都使用 memory
constructor(string memory name_, string memory symbol_) {
    _name = name_;
    _symbol = symbol_;
}
```

要连接字符串，我们可以使用 string.concat 函数。

```solidity
//定义两个字符串变量（str_1 和 str_2）
string memory str_1 = "hello ";
string memory str_2 = "world";

//将上面的两个字符串变量传递给 concat 函数，
//该函数将返回这两个字符串的拼接结果"helloworld"
string memory result = string.concat(str_1, str_2);
```

在 Solidity 中，字符串的**长度**通常使用 *uint256* 类型来表示。要确定 Solidity 中字符串的长度，可以使用内置的 bytes 类型，该类型表示动态的 bytes 数组。bytes 类型有一个 length 属性，用来返回数组中的 bytes 数量。通过它我们可以得到字符串的长度。

```solidity
//值为 hello 的字符串变量
string hi = "hello";
//我们将字符串转换为 bytes，然后调用 length 函数获取长度
uint256 len = bytes(hi).length;
```

## mapping

映射（mapping）是一种键值对类型。

```solidity
mapping(键 => 值) 变量名;
```

```solidity
mapping(address => uint) balance;
```

增删改查

```solidity
// 增
balance[address(0x123)] = 10;///这将为地址 0x123 分配一个新值

// 改
balance[address(0x123)] = 20;//这将把值从 10 更新为 20

// 查
uint b = balance[address(0x123)];

// 删
delete balance[address(0x123)];
```

如果要查询的键不存在，则会返回这个值类型的默认值。 例如 uint 的默认值是0，bool 的默认值是 false 。

删除实际上等同于将该值指定为默认值。因此，在执行删除操作后，仍然可以通过访问相应键的方式来获取该元素的值，只不过该值现在是**默认值**而已。

## struct

在 Solidity 中，结构体（struct）是一种用户自定义的数据类型，其中可以包含多个不同类型的属性。

用 {} 将其属性括起来，{} 里面每个属性用“；”隔开，结构体属性的定义与状态变量的定义相同，只是没有作用域这个概念。

```solidity
struct Student {
    string name;
    uint256 age;
}
```

初始化结构体；结构体只能够存储在像 mapping，array 这样的引用类型当中。

```solidity
Student memory student = Student(1, 18, "Alice");
```

访问和修改结构体

```solidity
//访问
string name = student.name;

//修改
student.name = "Thomas";
```

## array

### 定长数组

```solidity
uint256[3] public numbers; // 定义一个长度为3的定长数组

//我们需要使用[元素，元素，元素]的形式为定长数组赋值。
//需要特别注意的是，所有元素的类型必须一致。
//因此在定长数组的定义中，只需要在方括号中指定第一个元素的类型即可（对应下方的[uint256(10), 20, 30]）。
function setNumbers() public {
  uint256[3] memory tempArray = [uint256(10), 20, 30]; // 定义一个临时的长度为3的定长数组
  numbers = tempArray; // 将临时数组赋值给定长数组
}
```

### 动态数组

```solidity
uint256[] arr;
```

静态数组需要在声明时确定的固定大小，而动态数组的大小可以在运行时进行调整。动态数组只占用实际元素所需内存空间，节省内存。

### 数组方法

追加：只有 **storage** 动态数组有 push() 方法；只允许在数组的末尾添加新的元素，而且注意一次只能 push 一个元素。

```solidity
arr.push(1);
```

删除：使用 pop() 方法删除；只允许删除数组的末尾元素，而且注意一次只能 pop 一个元素。

```solidity
arr.pop();
```

获取数组长度：数组的长度是用 *uint256* 类型来存储的。

```solidity
uint256 len = arr.length;
```

索引

```solidity
uint256 num = arr[10];
```



# 数据位置

每种引用类型都有一个数据位置，指明变量值应该存储在哪里。Solidity 提供3种类型的数据位置：**storage**、**memory** 和 **calldata**。

| 数据位置 | 作用范围 | 是否可变 |
| :---: | :---: | :---: |
| storage | contract | yes |
| memory | function | yes |
| calldata | function | no |

而 storage 则是作用于合约的存储结构。这个位置用于存储合约的状态变量。存储在此位置的数据被持久化存储在以太坊区块链上，因此消耗的gas更大。状态变量默认存储在 storage ，我们不需要显示指定。

```solidity
//这个字符串状态变量存储在 storage 中
string str;

function a() {
	//函数体
}
```

memory 在 Solidity 中表示一个临时数据存储区域。与 storage 不同，存储在 memory 中的数据在函数调用结束时会被清空，不具有持久性。

要在 memory 中声明变量，您需要在函数内部定义它，然后加上关键字 memory。

```solidity
pragma solidity ^0.8.4;

contract MemoryExample {
    function example() public pure {
        // tempStr 是存储在memory中的局部变量
        string memory tempStr = "Hello, World!";
    }
}
```

# 控制结构

## 选择结构

Solidity 中有 `if`、`三元表达式`、`require` 语句、和 `assert` 语句四种选择结构。其中 `if`、`三元表达式` 的用法同 Java。

### require

**require** 是一种类似于断言的语法，如果 *require* 当中的条件没有满足，此次调用将会失败。

为了检查条件是否成立，我们使用关键字 require，然后跟上条件，如果不满足条件，则报告错误消息。

```solidity
require(条件表达式, "错误消息")
```

```solidity
require(a > 5, "Value must be greater than 5");
```

Solidity 暂不支持中文编码，错误信息请用英文编写。错误消息为可选参数。

### assert

## 循环结构

Solidity 中有 `for` 、`while`  和 `do-while` 三种循环结构。

Solidity 中没有 `for-each` 循环，可用“for 循环 + 索引”进行遍历，详见 Java。



# 函数

## 定义函数

```solidity
function 函数名() {
	//函数体
}
```

```solidity
function sum() {
	//函数体
}
```

为了保持一致性，我们建议遵循此顺序：函数名称 、参数、作用域、状态可变性、返回值。

## 作用域

要定义一个 *公共变量* 或 *公共函数*，我们使用关键字 public，并将其放在 *变量* 名称之前或 *函数* 参数之后。

```solidity
uint public a;
function aa() public { 
	//funciton body 
}
```

要定义一个仅在合约内部，以及继承它的合约中才能使用的函数，我们使用关键字 internal，并将其放在*函数* 参数之后。

```solidity

   function aa() internal{}

   aa();
```

要定义一个外部用户或其他合约能使用的*函数*，我们使用关键字 external，并将其放在*函数* 参数之后。在本合约中使用时必须加上 this 关键词。

```solidity

   function aa() external{}

   this.aa();
```

## 传参和返回值

要定义一个*函数*的*输入参数*，我们在函数名后的括号中放置它们。如果我们想要多个参数，则使用,进行分隔。

```solidity
//这里有两个输入参数，a 和 b，都是有符号整数 int。
function sum(int a, int b) public {
	//function body 
}
```

要定义*函数*的*输出*，我们在函数花括号前加上 returns 关键字定义返回类型，并且在函数体中使用 return 关键词返回函数输出。

```solidity
//此函数返回一个int型变量。
function sum(int a, int b) public returns(int) {
    return 1;
}
```

## Pure 函数

纯函数（pure）不会访问以及修改任何状态变量。

要将一个*函数*定义为 pure 函数，我们需要在*函数头*中使用关键字 pure。

```solidity
function add() public pure {
	//function body 
}
```

使用 pure 定义的函数被调用时不用花费 gas，并且可以保证该函数不会改变状态变量，有益于开发时的模块化管理。

## View 函数

视图函数（view）不会修改状态变量，但可能使用（读取）状态变量。

```solidity
function add() public view {
	//function body 
}
```

## constructor 函数

**构造函数**（constructor）是在合约部署时自动调用且只被调用一次的函数。

```solidity
constructor(int a, bool b) {
	//函数体
}
```

**构造函数没有名称和返回值**：

- 名称，不需要显式命名。由于每个类中只能有一个构造函数，它将在对象创建时被自动调用。
- 返回值，没有返回值，因为构造函数是用于初始设置的。

# 合约

## Pragma

**pragma** 关键字用于指定编译器版本。它的作用是确保代码能够在特定版本的编译器下正确编译和执行，以避免潜在的兼容性问题。

使用关键字 pragma 并不会直接更改编译器的版本。它也不会启用或禁用编译器的功能。它只是指示编译器检查它的版本是否与 *pragma* 要求的版本匹配。如果不匹配，则编译器会报错。

```solidity
//指定合约的编译器版本仅可为0.8.4
pragma solidity 0.8.4;
//指定合约的编译器版本仅可为≥0.8.4 且 <0.9.0（）
//限制条件“<0.9.0”通过^ 提供，^0.a.b 表示它需要编译器版本 ≥0.a.b 且 <0.(a+1).0。
pragma solidity ^0.8.4;
```

## Contract

**contract** 关键字用于定义合约，一个 Solidity 的 **.sol** 文件可以包含一个或多个 contract。contract 类似于面向对象编程中的类。

```solidity
contract 合约名称 { }
```

```solidity
contract UniswapV2Pair{ }
```

# 其它

## msg.sender

**msg.sender** 可以获取本次调用的调用者地址。

要使用 msg.sender，我们不需要定义它。它在函数中处处可用，代表函数的调用者。

```solidity
function a() {
    //这里 msg.sender 没有定义为状态变量
    //也不作为参数传入，我们可以直接使用它
    address a = msg.sender;
}
```

tx.origin 表示最初初始化整个调用链的账户地址。

<img src="assets/image-20250428135238980.png" alt="image-20250428135238980" style="zoom:50%;" />
