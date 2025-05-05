# Solidity

## Solidity

[Solidity](https://docs.soliditylang.org/zh-cn) 是一种面向合约的编程语言。智能合约是控制 Ethereum 状态中账户行为的程序。

- Solidity 是一个开源的社区项目，由一个核心团队管理。
- Solidity 受 C++ 的影响最深，但也借用了 Python，JavaScript 等语言的概念。

**Solidity 的特点**：

- 面向合约
- 编译型
- 静态类型
- 强类型

**Solidity 资源**：

- [Solidity Docs](https://docs.soliditylang.org/zh-cn)
- [Solidity 资源](https://docs.soliditylang.org/zh-cn/latest/resources.html)
- [Solidity by Example](https://solidity-by-example.org/)
- [Course on Hackquest](https://www.hackquest.io/zh-cn/home)

## [源文件结构](https://docs.soliditylang.org/zh-cn/v0.8.24/layout-of-source-files.html)

源文件可以包含任意数量的 contract 定义，import 指令，pragma 指令，using for 指令，struct，enum，function，error 以及 constant 变量的定义。

### [SPDX 许可标识符](https://docs.soliditylang.org/zh-cn/v0.8.24/layout-of-source-files.html#spdx)

**SPDX 许可标识符**用于表示源代码的开源情况。每个开源的源文件都应该以一个 `// SPDX-License-Identifier: MIT` 注释开始。

### [编译指示](https://docs.soliditylang.org/zh-cn/v0.8.24/layout-of-source-files.html#pragma)

**pragma** 关键字用于启用某些编译器特性或检查。

#### [版本编译指示](https://docs.soliditylang.org/zh-cn/v0.8.24/layout-of-source-files.html#version-pragma)

使用 **pragma** 关键字指定编译器版本。

```solidity
//指定合约的编译器版本仅可为0.8.4
// SPDX-License-Identifier: MIT
pragma solidity 0.8.4;


//指定合约的编译器版本仅可为≥0.8.4 且 <0.9.0（）
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.4;
```

pragma 的作用是确保代码能够在特定版本的编译器下正确编译和执行，以避免潜在的兼容性问题。

使用关键字 pragma 并不会直接更改编译器的版本。它也不会启用或禁用编译器的功能。它只是指示编译器检查它的版本是否与 *pragma* 要求的版本匹配。如果不匹配，则编译器会报错。

### [导入其它源文件](https://docs.soliditylang.org/zh-cn/v0.8.24/layout-of-source-files.html#import)

### [注释](https://docs.soliditylang.org/zh-cn/v0.8.24/layout-of-source-files.html#index-9)

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

## 代码风格

- [Solidity 代码风格指南](https://docs.soliditylang.org/zh-cn/latest/style-guide.html#maximum-line-length)

### 标识符

**标识符规范**：

**命名习惯**：

- [命名规范](https://docs.soliditylang.org/zh-cn/latest/style-guide.html#id18)
- **合约**：大驼峰
- **结构体**：大驼峰
- **结构体属性**：num_Student
- **函数**：小驼峰
    - **函数参数**：小驼峰
- **局部变量和状态变量**：小驼峰
- **常量**：大蛇形
- **事件**：大驼峰
    - **事件参数**：小驼峰
- **枚举**：大驼峰
- **修饰符**：大驼峰

# [可见性和 getter 函数](https://docs.soliditylang.org/zh-cn/v0.8.24/contracts.html#getter)

## 可见性说明符

状态变量和函数的可见性通过**[可见性说明符](https://docs.soliditylang.org/zh-cn/v0.8.24/cheatsheet.html#index-10)**表示，可写在如下位置：

- **状态变量**：放在变量名之前
- **函数**：参数列表和返回参数列表之间

```solidity
//状态变量的可见性
变量类型 可见性说明符 变量名;

//函数的可见性
function 函数名() 可见性说明符 { }
```

```solidity
uint public a;
function aa() public { 
	//funciton body 
}
```

- **public**：合约内、外均可见
- **private**：仅在内部可见（继承合约不可见）
- **external**：仅在外部可见（仅可修饰函数）
- **internal**：仅在内部可见（继承合约可见）（默认可见性）

| 可见性 | 适用对象 | 可访问范围 | Getter生成 | 默认可见性 | 特性与限制 |
| :---: | :---: | :---: | :---: | :---: | :---: |
| public | 状态变量、函数 | 合约内外 | 状态变量：是<br>函数：不适用 | 否 | 状态变量自动生成Getter；函数参数复制到内存，Gas消耗较高 |
| private | 状态变量、函数 | 仅当前合约内部（继承合约不可见） | 否 | 否 | 数据仍存于链上，继承合约不可访问 |
| external | 函数 | 仅外部调用（内部需`this.func()`） | 不适用 | 否 | 参数用`calldata`存储，Gas优化；不可修饰状态变量 |
| internal | 状态变量、函数 | 当前合约及继承合约 | 否 | 状态变量：是<br>函数：否 | 状态变量默认可见性；函数需显式声明，常用于继承体系共享逻辑 |

在下面的例子中，合约 `D`, 可以调用 `c.getData()` 来检索状态存储中 `data` 的值， 但不能调用 `f`。 合约 `E` 是从合约 `C` 派生出来的，因此可以调用 `compute`。

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

contract C {
    uint private data;

    function f(uint a) private pure returns(uint b) { return a + 1; }
    function setData(uint a) public { data = a; }
    function getData() public view returns(uint) { return data; }
    function compute(uint a, uint b) internal pure returns (uint) { return a + b; }
}

// 这将不会编译
contract D {
    function readData() public {
        C c = new C();
        uint local = c.f(7); // 错误：成员 `f` 不可见
        c.setData(3);
        local = c.getData();
        local = c.compute(3, 5); // 错误：成员 `compute` 不可见
    }
}

contract E is C {
    function g() public {
        C c = new C();
        uint val = compute(3, 5); // 访问内部成员（从继承合约访问父合约成员）
    }
}
```

## [状态变量的可见性](https://docs.soliditylang.org/zh-cn/v0.8.24/contracts.html#id3)

| 修饰符 | 可访问范围 | 自动生成 Getter | 典型应用场景 | 特性与限制 |
| :---: | :---: | :---: | :---: | :---: |
| public | 合约内外均可读取（通过自动生成的 Getter 函数） | 是 | 需对外公开的状态（如代币总供应量） | 自动生成同名 Getter 函数；存储数据仍可通过事件或链上分析获取 |
| private | 仅在当前合约内部可访问（继承合约不可见） | 否 | 敏感数据（如管理员地址、内部计算中间值） | 编译后数据仍存于链上，仅限制合约层面的直接访问；继承合约不可见 |
| internal | 当前合约及继承合约可访问 | 否 | 需在继承体系中共享的数据（如基础合约配置） | 默认可见性（未显式声明时）；与 `private` 类似但允许继承 |

## [函数的可见性](https://docs.soliditylang.org/zh-cn/v0.8.24/contracts.html#id4)

Solidity 有两种函数调用：确实创建了实际 EVM 消息调用的**外部函数**和不创建 EVM 消息调用的**内部函数**。 此外，派生合约可能无法访问内部函数。 这就产生了四种类型的函数的可见性。Solidity 0.5 及之后：必须显式指定函数的可见性（之前是 public），否则编译报错！

| 修饰符 | 可访问范围 | 典型应用场景 | 特性与限制 |
| :---: | :---: | :---: | :---: |
| public | 合约内外均可调用（包括其他合约、EOA用户、继承合约） | 需对外暴露的接口（如 DApp 前端交互）、状态变量自动生成 getter 函数 | 参数处理需复制到内存，Gas 消耗较高；默认可见性修饰符 |
| private | 仅在当前合约内部可调用（继承合约不可见） | 内部工具函数、敏感逻辑（如权限校验） | 编译后仍可通过链上数据逆向分析，仅防止其他合约调用 |
| external | 仅能通过外部调用（合约或用户），内部需通过 `this.func()` 调用 | 面向外部的高频接口（如代币转账）、需节省 Gas 的场景 | 参数以 `calldata` 存储，避免内存复制，Gas 更优；不支持内部直接调用 |
| internal | 当前合约及其继承合约可调用 | 可复用逻辑封装（如代币铸造）、继承体系中的工具函数 | 参数处理与 `public` 类似 |

## [Getter 函数](https://docs.soliditylang.org/zh-cn/v0.8.24/contracts.html#getter-functions)

# 变量

## 状态变量

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

获取其它合约的状态变量：只有 public 的变量才可以通过 `合约名.参数名()` 的方式获取

```solidity
contract NFTContract {
    //只有 public 的变量才可以通过 `合约名.参数名()` 的方式获取
    uint public totalSupply;
}

contract MarketplaceContract {
    // 必须持有合约 NFTContract 的实例引用才能调用其状态变量
    NFTContract public nft;

    function getTotalSupply() public view returns (uint) {
        // 调用合约 NFTContract 的 状态变量 totalSupply
        return nft.totalSupply();
    }
}
```

## 局部变量

**局部变量**（Local Variable）是在函数内部声明的变量，其作用域仅限于该函数内部。

## 常量

使用 constant 关键字声明常量

```solidity
//将1赋值给了常量NUM。
uint256 constant NUM = 1;
```

constant 只能用于声明**状态变量**，但**不会**被写入合约的 storage 中，而是直接在编译时被硬编码到**字节码**中，而字节码是在合约部署时就生成的值，所以不可能在函数运行时再改变字节码。

## immutable

immutable 修饰的变量可以在构造函数中对其赋值，且赋值后不可更改。immutable 只能用于状态变量的定义，这是因为 immutable 修饰的变量也会硬编码到合约的字节码中。

# [数据类型](https://docs.soliditylang.org/zh-cn/v0.8.24/types.html)

Solidity 是一种**静态类型**语言，在声明变量时，必须先指定其数据类型。

Solidity 中不存在“未定义”或“空”值的概念， 但新声明的变量总是有一个取决于其类型的 [默认值](https://docs.soliditylang.org/zh-cn/v0.8.24/control-structures.html#default-value)。

```
数据类型
│
├─ 值类型
│  ├─ 布尔型 bool
│  ├─ 整型
│  │  ├─ 有符号整型 int
│  │  └─ 无符号整型 uint
│  ├─ 定长浮点型
│  │  ├─ 有符号定长浮点型 fixed
│  │  └─ 无符号定长浮点型 ufixed
│  ├─ 地址型 adress
│  ├─ 定长字节数组 bytes1, …, bytes32
│  └─ 枚举 enum
│
├─ 引用类型
│  ├─ 数组 array
│  ├─ 结构体 struct
│  ├─ 映射 mapping
│  ├─ 字符串 string
│  └─ 动态字节数组 bytes
│
└─ 特殊类型
   ├─ 合约型 contract
   ├─ 函数型 function
   ├─ 存储位置修饰符
   │  ├─ storage：数据永久存储在链上
   │  ├─ memory：临时内存，函数执行后销毁
   │  └─ calldata：只读外部输入，节省 Gas
   └─ 有理数字面量
```

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

在 Solidity 中，**结构体**（struct）是一种用户自定义的数据类型，其中可以包含多个不同类型的属性。

用 {} 将其属性括起来，{} 里面每个属性用“；”隔开，结构体属性的定义与状态变量的定义相同，只是没有作用域这个概念。

```solidity
struct Student {
    string name;
    uint256 age;
}
```

初始化结构体；结构体只能够存储在像 mapping，array 这样的引用类型当中。

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

## enum

使用 **enum** 关键字定义枚举，每个枚举值之间用 `,` 分隔。

```solidity
enum 枚举名 {枚举值列表}
```

```solidity
enum Season {
    Spring,
    Summer,
    Autumn,
    Winter
}
```

枚举类型中的每个**枚举值**将被映射为一个**整数值**，枚举类型是以 uint8 存储的（即0-255），所以一个枚举类型最多可以定义256个值，分别对应到 uint8 的 0-255 。

在上面的例子中，**Spring** 的整数值为0，**Summer** 的整数值为1，**Autumn** 的整数值为2，**Winter** 的整数值为3。

**给枚举类型的变量赋值**

```solidity
枚举类型 变量名 = 枚举名.枚举值
```

```solidity
// 赋值给枚举类型变量
// season1 是一个 Season 枚举类型变量，实际上赋给 season1 的值是 Spring 对应的整数值 0，而不是 Spring
Season season1 = Season.Spring;

// 枚举类型可以与整数进行显式转换，但不能进行隐式转换。
Season season2 = Season(0);
```

**最小值和最大值**

```solidity
枚举类型 变量名 = type(枚举名).min/max
```

```solidity
Season season3 = type(Season).min;
Season season4 = type(Season).max;
```

## [数据类型转换](https://docs.soliditylang.org/zh-cn/v0.8.24/types.html#types-conversion-elementary-types)

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

Solidity 中有 `if` 和 `三元表达式` 两种选择结构，用法同 Java。

## 循环结构

Solidity 中有 `for` 、`while`  和 `do-while` 三种循环结构。

Solidity 中没有 `for-each` 循环，可用“for 循环 + 索引”进行遍历，详见 Java。

## 跳转结构

Solidity 中有 `continue`、`break`、`return`、`revert`、`require` 和 `assert` 六种跳转结构。其中前三种用法与 java 几乎相同。

- 关于 continue 和 break：Solidity **不支持标签跳转**（如跳出多层嵌套循环），仅能在单层循环中使用。

# [contract](https://docs.soliditylang.org/zh-cn/v0.8.24/contracts.html#contracts)

**合约**（Contract）类似于面向对象语言中的类。 

## 定义合约

使用 **contract** 关键字声明合约名称，一个 Solidity 的 **.sol** 文件可以包含一个或多个 contract。

```solidity
contract 合约名称 { }
contract MyContract{ }
```

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

// 声明一个名称为 ContractA 的合约，相当于面向对象中的类
contract ContractA {
    uint256 public data;
}

// 声明一个名称为 ContractB 的合约，相当于面向对象中的类
// 这里有两个合约，是为了展示从一个合约可以引入另一个合约。
contract ContractB {
    //声明一个合约类型的变量 ContractA，相当于面向对象中的对象
    ContractA public contractA;
    ContractA public contractAA;

    constructor(address _contractA) {
        // 方式一：通过 new 的方式实例化 ContractA，相当于面向对象中的实例化对象
        contractA = new ContractA();

        // 方式二：通过指定地址的方式实例化 contractAA，相当于面向对象中的实例化对象
        contractAA = ContractA(_contractA);
    }
}
```

## 合约结构

在 Solidity 中，合约类似于面向对象编程语言中的类。 

每个合约中可以包含如下声明：

- 状态变量
- 函数
- 函数修饰器
- 事件
- 错误
- 结构类型
- 枚举类型

合约可以从其他合约继承。

还有一些特殊种类的合约，叫做**库合约**和**接口合约**。

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

## 传参和返回值

要定义一个*函数*的**输入参数**，我们在函数名后的括号中放置它们。

```solidity
//这里有两个输入参数，a 和 b，都是有符号整数 int。
function sum(int a, int b) public {
	//function body 
}
```

要定义函数的**返回值**，我们在函数花括号前加上 returns 关键字定义返回类型，并且在函数体中使用 return 关键词返回函数输出。

```solidity
//此函数返回一个int型变量。
function sum(int a, int b) public returns(int) {
    return 1;
}
```

## 函数的调用

调用函数本身的限制条件在于函数**可见性**。

- 如果是用户和合约之间，只能调用 public 或 external 的函数。

- 如果是合约内部的函数之间相互调用，则没有限制条件。

- 被 external 修饰的函数可以直接用调用。

- 合约之间的调用需要先定义出要调用的合约类型的变量。

### 合约之间调用

合约之间调用函数，需要先定义出要调用的合约类型的变量。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

// 合约B
contract B {
    uint public result;

    // 关键要求：函数必须声明为 public/external，否则外部合约无法调用
    function foo(uint _input) public {
        result = _input * 2;
    }
}

// 合约A
contract A {
    // 必须持有合约 B 的实例引用才能调用其函数
    // 声明合约 B 的实例变量
    B public b;

    // 通过构造函数传入合约 B 的地址
    constructor(address _bAddress) {
        b = B(_bAddress);
    }

    // 调用合约 B 的foo函数
    function callBFunction(uint _input) public {
        b.foo(_input);
    }
}
```

## [状态可变性](https://docs.soliditylang.org/zh-cn/v0.8.24/contracts.html#state-mutability)

### [Pure 函数](https://docs.soliditylang.org/zh-cn/v0.8.24/contracts.html#pure)

纯函数（pure）不会访问以及修改任何状态变量。

要将一个*函数*定义为 pure 函数，我们需要在*函数头*中使用关键字 pure。

```solidity
function add() public pure {
	//function body 
}
```

使用 pure 定义的函数被调用时不用花费 gas，并且可以保证该函数不会改变状态变量，有益于开发时的模块化管理。

### [View 函数](https://docs.soliditylang.org/zh-cn/v0.8.24/contracts.html#view)

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

## [modifier](https://docs.soliditylang.org/zh-cn/v0.8.24/contracts.html#modifiers)

**函数修饰器**（modifier）允许开发人员在函数执行前后或期间插入代码，以便确保特定的条件得到满足。例如，您可以使用修饰器在执行函数之前自动检查一个条件。

函数修器符内的代码的不能被独立执行。单个“函数”可以有多个“修饰器”， 修饰器按照它们出现的顺序执行。

<img src="assets/image-20250429195435893.png" alt="image-20250429195435893" style="zoom:45%;" />

使用 **modifier** 关键字自定义函数修饰器

```solidity
modifier 修改器名称(可选参数) {
    require(条件, "错误提示"); // 函数执行前执行的代码，这里是条件检查
    _;                       // 表示执行被修饰函数的代码
                             // 函数执行后执行的代码（可选）
}
```

```solidity
contract Owned {
    address owner;
    constructor() { owner = msg.sender; }

    // 定义仅允许所有者调用的 onlyOwner 修饰符
    modifier onlyOwner {
        require(msg.sender == owner, "Not owner");
        _;
    }

    // 使用 onlyOwner 限制函数调用权限
    function destroy() public onlyOwner {
        selfdestruct(payable(owner));
    }
}
```

## 函数签名和选择器

### 函数签名

**函数签名**是*函数名*+*参数字段类型*的字符串。没有空格，不用缩写。

**函数签名**是一个函数的唯一标识符；它由*函数名*和*参数类型*组成，没有空格，不用缩写。在 Solidity 中，所有函数调用都通过*函数签名*作为唯一标识。

```solidity
function hello(uint256 a, address b, bool c) {...}
signature = "hello(uint256,address,bool)"；
```

### 函数选择器

**函数选择器**是*函数签名哈希值*的前四个字节，用于在编码后的数据中唯一标识函数。

```solidity
//方法一：直接获取函数签名 signature 的哈希值的前4个字节
bytes4 selector = bytes4(keccak256(signature));

//方法二：使用 functionName.selector
bytes4 selector = myFunction.selector;
```

```solidity
pragma solidity ^0.8.0;

contract FunctionSignature {
  function dosome(uint256 num, string memory text) public pure returns (bytes4 selector1, bytes4 selector) {
    selector = bytes4(keccak256("dosome(uint256,string)"));
    selector1 = this.dosome.selector;
  }
}
```

# event

**事件**（ *Event* ）是一种用于在智能合约中发布通知和记录信息的机制。它可以在合约执行期间发出消息，允许外部应用程序监听并对这些消息做出响应。事件是合约的可继承成员。

## event

使用 **event** 关键字声明事件

```solidity
event 事件名(参数列表);
```

```solidity
//在这里我们定义了一个名为EventName的事件，其有parameter1和parameter2两个参数。
event EventName(
  uint256 parameter1,
  uint256 parameter2
);
```

## emit

使用 **emit** 关键字初始化并提交一个事件。

```solidity
//在这里我们提交了一个名为MessageSent的事件，参数分别为msg.sender和message。
emit MessageSent(msg.sender, message);
```

当提交事件时，会触发参数存储到交易的日志中，事件的参数存放在交易日志里。这些日志与合约的地址关联，并记录到区块链中。

需要注意的是，虽然这个事件是广播到区块链网络中的，但智能合约是无法监听广播的信息的，只能通过一些工具辅助查询（如 etherscan）或者别的方式监听。

## indexed

在事件声明中的参数类型后面添加 **indexed** 关键字，使参数可搜索。

```solidity
envent 事件名(参数类型 indexed 参数名);
```

```solidity
// 定义事件，其中 id 可被搜索
event LogChange(uint indexed id);
```





# block

**block** 是一个预定义的全局对象，表示当前交易所在的区块，用于访问当前区块的元数据信息。

## block.number

block.number 是一个全局变量，表示当前区块的**编号**，数据类型为 uint。

```solidity
//通过block.number返回当前区块的高度，并赋值给了变量blockNumber。
uint256 blockNumber = block.number;
```

## block.timestamp

**block.timestamp** 是一个全局变量，表示当前区块的**时间戳**，数据类型为 uint。

```solidity
//通过 block.timestamp 返回当前区块的时间戳，并赋值给了变量 blockTimestamp。
uint256 blockTimestamp = block.timestamp;
```

# library

## library

**库**（library）是一种特殊的合约，主要用于**重用代码**。库包含其他合约可以调用的函数。

库的限制：

- 库不能定义状态变量；
- 库不能发送接收以太币；
- 库不可以被销毁，因为它是无状态的；
- 库不能继承和被继承；

**库的定义和调用**：

```solidity
//定义一个名为 MathLibrary 的库。
library MathLibrary {}

//调用 MathLibrary 库中的 dosome 函数
MathLibrary.dosome();
```

## using-for

**using-for** 语句可以将库中的函数附加到某个类型中。

```solidity
//将 MathLibrary 库附加到 uint256 类型上
using MathLibrary for uint256;

//uint256 类型的变量 y 直接调用 MathLibrary 库中的 dosome 函数
y.dosome();
```

如果库函数有参数的话，变量 a.functionName() 的方式会自动把变量作为函数的第一个参数传入。

## import

**导入**（import）用于在一个 Solidity 合约中导入其他文件中的合约或库。类似 Python。

```solidity
// 导入 MathLibrary.sol 文件的合约和库
import "./MathLibrary.sol";
```

# abstract

**抽象合约**（abstract）定义了一些函数和状态变量，并且实现了一些通用的功能。它是一种不能被实例化的合约，只能被继承并作为其他合约的基类。抽象合约和普通合约的唯一区别在于抽象合约不能被部署。

定义抽象合约

```solidity
//定义一个抽象合约 ContractA
abstract contract ContractA { }
```

# Inheritance

## Interitance

使用 **is** 关键字可以继承任意一个合约或接口。功能同面向对象中的继承。

```solidity
// 合约 ChildContract 继承自合约 ParentContract
contract ChildContract is ParentContract { }
```

**多重继承**：一个合约可以从多个父合约继承功能和属性。

```solidity
//合约 Child 会继承自合约 Parent1 和 Parent2
contract Child is Parent1, Parent2 { }
```

## 合约继承接口

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

// 定义一个接口
interface MyInterface {
    function interfaceFunction() external;
}

// 合约继承接口
contract MyContract is MyInterface {
    function interfaceFunction() external override {
        // 实现接口中定义的函数
    }
}
```

## 接口继承接口

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

// 父接口
interface ParentInterface {
    function parentFunction() external;
}

// 子接口继承父接口
interface ChildInterface is ParentInterface {
    function childFunction() external;
}
```

## 合约继承合约

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

// 父合约
contract ParentContract {
    uint public value;

    constructor(uint _value) {
        value = _value;
    }

    function parentFunction() public {
        // 函数体
    }
}

// 子合约继承父合约
contract ChildContract is ParentContract {
    // 在继承时，子合约需要在自己的构造函数中初始化被父合约的构造函数。
    constructor(uint _parentValue) ParentContract(_parentValue) {
        // 函数体
    }

    // 重写父合约函数（可选）
    function parentFunction() public override {
        // 重写后的函数体
    }

    // 子合约独有的函数（可选）
    function childFunction() public {
        // 子合约独有的函数体
    }
}
```

## virtual 和 overide

继承中的**标记**（virtual）是指在父合约中标记一个函数式为可重写的，然后在子合约中使用 override 进行覆盖。

继承中的**函数覆盖**（override）是指在子合约中重写一个函数，以替换掉父合约中原有的同名函数。

```solidity
//在父合约中，使用 virtual 标记 foo 函数为可重写的。
function foo() public virtual returns (uint) { }

//在子合约中，使用 override 覆盖父合约中的 foo 函数。
function foo() public override { }
```

## super

在子合约函数内使用 `super.functionName` 即可调用父合约中的函数。

```solidity
//调用父合约中的init函数
super.init();
```

```solidity
//在多重继承中，super 会调用最后一个合约的函数
contract Child is Parent1, Parent2 {
    function foo() public {
        super.foo(); // 这会调用Paren2的foo函数
    }
}
```

# interface

## 定义接口

**接口**（interface）定义了一组函数头，但没有函数体。

```solidity
// 定义一个接口 MyInterface
interface MyInterface {
    //定义一个 external 的函数，函数名为 myFunction
    function myFunction(uint256 x) external;
}
```

- 接口不能实现任何函数；

- 接口无法继承其它合约，但可以继承其它接口；

- 接口中的所有函数声明必须是 external 的；
- 参数列表可以只有参数类型而省略参数名；

- 接口不能定义构造函数；

- 接口不能定义状态变量；

## 实现接口

实现接口就是在一个合约中实现接口的函数体

```solidity
// 定义一个实现接口的合约 MyContract
contract MyContract {
    //实现接口，即定义先前接口的函数体
    function myFunction(uint256 x) external {
        //函数体
    }
}
```

## 调用接口

```solidity
//接口名(合约地址).函数名()
MyInterface(contractAddress).myFunction();
```

```solidity
// 定义一个调用接口的合约 CallerContract
contract CallerContract {
    //定义实现合约的状态变量 myContract，类型为先前的接口 MyInterface
    MyInterface public myContract;

    //使用构造函数初始化实现合约，传入实现合约 MyContract 的地址
    constructor(address contractAddress) {
        myContract = MyInterface(contractAddress);
    }
    
    function callInterface(uint256 value) public {
        //调用 MyContract中 的 myFunction 函数，以达到调用接口的目的。
        uint256 result = myContract.myFunction(value);
        //其它函数体
    }
}
```

## 接口全过程

此示例是前面定义接口、实现接口和调用接口的合并。

```solidity
pragma solidity ^0.8.0;

// 定义接口
interface MyInterface {
    function myFunction(uint256 x) external;
}

// 实现接口
contract MyContract {
    function myFunction(uint256 x) external {
        //函数体
    }
}

// 调用接口
contract CallerContract {
    MyInterface public myContract;

    constructor(address contractAddress) {
        myContract = MyInterface(contractAddress);
    }
    
    function callInterface(uint256 value) public {
        uint256 result = myContract.myFunction(value);
        //其它函数体
    }
}
```

## 存钱罐示例

### 定义接口

```solidity
// 这个接口就像存钱罐的「遥控器按钮」
interface IPiggyBank {
    // 声明两个按钮：存钱和查余额
    function saveMoney() external payable; // 存钱（需要转账）
    function checkBalance() external view returns (uint); // 查余额
}
```

### 实现接口

```solidity
contract PiggyBank is IPiggyBank { // 必须实现接口里的所有按钮
    uint public money; // 存的钱

    // 存钱按钮的具体功能
    function saveMoney() external payable override {
        money += msg.value; // 把转账的钱存进去
    }

    // 查余额按钮的具体功能
    function checkBalance() external view override returns (uint) {
        return money; 
    }
}
```

### 调用接口

```solidity
contract Person {
    IPiggyBank public myPiggyBank; // 声明自己有一个存钱罐遥控器

    // 设置存钱罐的位置（传入地址）
    constructor(address _piggyBankAddress) {
        myPiggyBank = IPiggyBank(_piggyBankAddress); // 绑定到具体的存钱罐
    }

    // 用遥控器存钱的功能
    function save() external payable {
        myPiggyBank.saveMoney{value: msg.value}(); // 调用存钱罐的存钱功能
    }

    // 用遥控器查余额的功能
    function check() external view returns (uint) {
        return myPiggyBank.checkBalance(); // 调用存钱罐的查余额功能
    }
}
```

# ABI

**应用二进制接口**（Application Binary Interface，简称 **ABI**）是与以太坊智能合约交互的标准。在 EVM 处理数据时，所有的数据根据 **ABI** 标准进行编码。

abi 是一个全局变量。

## 编码

### abi.encode

全局函数 **abi.encode()** 用于对给定的参数进行 **ABI** 编码，返回一个字节数组。

```solidity
bytes memory encodedData = abi.encode(param1, param2);
```

```solidity
pragma solidity ^0.8.0;

contract AbiEncodeExample {
    function encodeParameters(
        uint256 param1,
        string memory param2
    ) public pure returns (bytes memory) {
        
        // 编码
        bytes memory encodedData = abi.encode(param1, param2);
        return encodedData;
    }
}
```

- **param1** 和 **param2**：这是要编码的参数。根据参数的类型，它们将被编码为**字节数组**。
- **encodedData**：这是一个 *bytes* 类型的变量，用于存储通过 `abi.encode(param1, param2)` 对参数进行编码后的数据。编码后的数据将按照参数的类型和顺序进行紧凑的编码，形成一个动态字节数组。

### abi.encodePacked

全局函数 **abi.encodePacked()** 也用于对给定的参数进行 **ABI** 编码，返回一个字节数组；但不会为每个参数添加其类型的长度信息，也不会在参数之间添加分隔符，结果是一个紧密打包的字节数组。

```solidity
bytes memory encodedData = abi.encodePacked(param1, param2);
```

```solidity
pragma solidity ^0.8.0;

contract AbiEncodeExample {
    function encodeParameters(
        uint256 param1,
        string memory param2
    ) public pure returns (bytes memory) {
        
        // 编码
        bytes memory encodedData = abi.encodePacked(param1, param2);
        return encodedData;
    }
}

```

**abi.encodePacked** 不能编码结构体和嵌套数组。

`abi.encode` 和 `abi.encodePack` 主要区别在于数据的压缩。

- **abi.encode** 使用标准的分隔符和填充物进行组织。就像将物品放入不同的袋子，并每个袋子都有标签和规范，以确保物品的结构和类型完整性。尽管可能需要更多的空间，但在解包时更容易处理和识别每个物品。
- **abi.encodePacked** 将参数紧密打包，就像将物品紧密地放在一起，没有任何额外的填充物或间隔。这种打包方式可以节省空间，但在解包时需要小心处理，因为物品之间没有明确的分隔符。

### abi.encodeWithSignature

全局函数 **abi.encodeWithSignature()** 用于对给定的*函数签名*和*参数*进行 **ABI** 编码，返回一个字节数组；这种编码方式可以快捷的将调用函数需要的信息打包。

<img src="assets/image-20250505195955106.png" alt="image-20250505195955106" style="zoom:50%;" />

```solidity
abi.encodeWithSignature("myFunction(uint256,string)", 123, "Hello");
```

```solidity
pragma solidity ^0.8.0;

contract SignatureExample {
    function dosome(uint256 number, string memory message) public pure {
        // 函数体
    }

    function getEncodedSignature() public pure returns (bytes memory) {
        // 使用 abi.encodeWithSignature() 编码dosome函数签名和参数
        bytes memory encodedData = abi.encodeWithSignature(
            "dosome(uint256,string)",
            123,
            "Hello"
        );
        return encodedData;
    }
}
```

### abi.encodeWithSelector

全局函数 **abi.encodeWithSelector()** 用于对给定的*函数选择器*和*参数*进行 **ABI** 编码，返回一个字节数组；

<img src="assets/image-20250505200543225.png" alt="image-20250505200543225" style="zoom:50%;" />

```solidity
// 根据获取选择器的方法不同，有两种方法对选择器和参数进行编码
//方法一
abi.encodeWithSelector(bytes4(keccak256("myFunction(uint256,string)")),123, "Hello");

//方法二
bytes4 selector = this.myFunction.selector;
abi.encodeWithSelector(selector, 123, "Hello");
```

```solidity
pragma solidity ^0.8.0;

contract EncodeWithSelectorExample {
    function myFunction(uint256 amount, string memory message) public pure {
        // 函数体
    }

    function getEncodedData() public pure returns (bytes memory) {
        // 获取函数选择器
        bytes4 selector = this.myFunction.selector;

        // 对选择器和参数进行编码
        bytes memory encodedData = abi.encodeWithSelector(
            selector,
            123,
            "Hello"
        );
        return encodedData;
    }
}
```

## 解码

全局函数 **abi.decode()** 用于对编码后的数据进行解码。第一个参数是编码数据的**字节数组**，第二个参数是解码后的**数据类型**。

```solidity
//对编码数据 encodedData 进行解码，解码后的数据类型为 address
address decodedAddress = abi.decode(encodedData, (address));

//多个参数
(uint256 decodedUint, address decodedAddress, string memory decodedString) = abi.decode(encodedData, (uint256, address, string));
```

```solidity
pragma solidity ^0.8.0;

contract DecodeExample {
    function decodeAddress(bytes memory encodedData) public pure returns (address) {
        
        //解码
        address decodedAddress = abi.decode(encodedData, (address));
        return decodedAddress;
    }
} 
```

# 低级调用

**低级调用**其实是直接和 **EVM**（以太坊虚拟机）交互的一种调用方式，因此它具有更高的灵活性。

## address.call

```solidity
(bool success, bytes memory data) = address(targetAddress).call{value: amount}(abiEncodedData);
```

- **targetAddress**：是目标合约的地址。
- **value**：是可选参数，用于向目标合约发送以太币。
- **abiEncodedData**：是目标合约函数的ABI编码数据（通过 abi.encodeWithSignature 或者 abi.encodeWithSelector 编码）。

```solidity
pragma solidity ^0.8.0;
//目标合约
contract TargetContract {
    uint256 public value;

    function setValue(uint256 newValue) external {
        value = newValue;
    }
}

contract CallerContract {
    function callTargetContract(
        address targetAddress,
        uint256 newValue
    ) external {
        //构造函数调用的ABI编码数据字段，
        bytes memory payload = abi.encodeWithSignature(
            "setValue(uint256)",
            newValue
        );
        //如果不使用bytes data返回值，可以不接收该返回值。
        (bool success, ) = targetAddress.call(payload);
        //判断调用是否成功。
        require(success, "Call to target contract failed");
    }
}
```



## 1

# 异常处理

## require

**require** 是一种类似于断言的语法，如果 *require* 当中的条件没有满足，此次调用将会失败。

为了检查条件是否成立，我们使用关键字 require，然后跟上条件，如果不满足条件，则报告错误消息。

```solidity
require(条件表达式, "错误消息")
```

```solidity
require(a > 5, "Value must be greater than 5");
```

Solidity 暂不支持中文编码，错误信息请用英文编写。错误消息为可选参数。

## [revert](https://docs.soliditylang.org/zh-cn/v0.8.24/control-structures.html#revert)

revert() 函数用于终止函数的执行并回滚所有状态变化。如果附带一个字符串参数，则提供自定义的错误消息；否则它会自动返回一个默认的错误消息。

```solidity
revert("Custom error message");
revert();
```

## assert

assert 语句应用于检查一些被认为永远不应该发生的情况（例如除数为0）。

```solidity
//确认a 和 b在任何情况下都相等
assert(a == b);
```

## error

**错误**（error）是一种自定义的**数据类型**。

```solidity
//使用error关键字定义了一个名为MyCustomError的自定义错误类型
//并指定错误消息类型为string 和 uint。
error MyCustomError(string message, uint number);

function process(uint256 value) public pure {
    //检查value是否超过了100。如果超过了限制，我们使用revert语句抛出自定义错误
    //并传递错误消息"Value exceeds limit" 和value。
    if (value > 100) revert MyCustomError("Value exceeds limit", value);
}
```

## try-catch

用法同 Java。

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

**tx.origin** 表示最初初始化整个调用链的账户地址。

<img src="assets/image-20250428135238980.png" alt="image-20250428135238980" style="zoom:50%;" />

## 支付 ETH

在调用一个 payable 函数时，只需要在函数名和参数之间插入一个 `{value : xx}` 语法即可，其中 xx 代表你需要附加的 ETH 数量。

```solidity
deposit{value: 5}();
```

## 接收 ETH

### payable

使用 **payable** 修饰的函数，表示可以接收 ETH。只有 public 和 external 的函数支持 payable 修饰。

在函数参数后，使用 payable 关键字可以使该函数成为一个可支付函数。

```solidity
function 函数名() payable 外部修饰符 { }
```

```solidity
function receivePayment() payable public { }
```

### msg.value

***msg.value*** 用于获取当前函数调用时传递给合约的 ETH 数量。msg.value 的单位是 Wei，是以太坊最小的货币单位。1 Eth = 10^18 Wei。

```solidity
uint256 value = msg.value;
```

## 哈希算法

哈希计算是一种将任意长度的数据转换为固定长度哈希值的过程。

Keccak256 和 SHA3 是用于哈希计算的两个算法。SHA3 还处于标准化阶段，所以在合约代码中直接使用 Keccak256 是最清晰和推荐的做法。

**keccak256** 是一个全局函数，可以在函数中直接使用该函数进行哈希计算。

- 输入：只接受 bytes 类型的输入。
- 输出：bytes32 长度的字节。

```solidity
//这里我们将字符串”HackQuest"转换成字节数组后，进行哈希的结果赋值给了 res 变量。
bytes32 res = keccak256(bytes("HackQuest"));
```

## receive 函数

**receive** 函数只用于处理接收 ETH。

```solidity
//这里我们定义一个空的 receive 函数。
receive() external payable { }
```

- 一个合约最多只有一个；
- 而且不能有任何的参数；
- 不能返回任何值；
- 必须包含 external 和 payable；
- 并非每个合约都需要 receive 函数。

## fallback 函数

**fallback** 函数充当了合约的默认处理函数，用于处理没有明确定义处理方式的消息。

```solidity
//这里我们定义了一个空的fallback函数。
fallback() external { }
```

- 必须包含 external；
- 并非每个合约都需要 receive 函数。

fallback 函数会在三种情况下被调用：

- 调用者尝试调用一个合约中不存在的函数时；
- 用户给合约发 Ether 但是 *receive* 函数不存在；
- 用户发 Ether，*receive* 存在，但是同时用户还发了别的数据（ msg.data 不为空）。

## selfdestruct 函数

**selfdestruct** 是 solidity 中的一个内置函数，调用该函数后，将触发合约的自毁，自毁将该合约从区块链中删除，在删除前，他还会将合约中存储的剩余 ETH 转移给指定的账户。

```solidity
//我们调用 selfdestruct 函数，指定将合约中剩余的 ETH 发送给 targetAddress 地址。
selfdestruct(targetAddress);
```

## 时间

在 Solidity 中，时间戳以秒为单位表示时间；此外，Solidity 还提供了一些全局变量，如 days，weeks，供开发者使用，以便更方便地表示一段时间。

<img src="assets/image-20250505144508608.png" alt="image-20250505144508608" style="zoom:50%;" />

使用 minutes， hours， days， weeks 这样的时间单位时，需要在前面指定单位的数量。此外，由于月和年的天数不固定，所以不使用 `1 months` 和 `1 years` 这样的数量单位。

```solidity
uint256 minute = 1 minutes;
uint256 minute = minutes; // 错误用法
uint256 hour = 1 hours;
uint256 day = 1 days;
uint256 week = 1 weeks;
```
