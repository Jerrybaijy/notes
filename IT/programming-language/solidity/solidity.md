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
    - **合约名**：大驼峰

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

## mapping

映射（mapping）是一种键值对类型。

```solidity
mapping(键 => 值) 变量名;
```

```solidity
mapping(address => uint) balance;
```

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

## 函数分类

### Pure 函数

纯函数（pure）不会访问以及修改任何状态变量。

要将一个*函数*定义为 pure 函数，我们需要在*函数头*中使用关键字 pure。

```solidity
function add() public pure {
	//function body 
}
```

使用 pure 定义的函数被调用时不用花费 gas，并且可以保证该函数不会改变状态变量，有益于开发时的模块化管理。

### View 函数

视图函数（view）不会修改状态变量，但可能使用（读取）状态变量。

```solidity
function add() public view {
	//function body 
}
```

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

