# Mermaid

[Mermaid](https://mermaid.nodejs.cn/) 是一款基于 JavaScript 的开源**图表工具**，通过类 Markdown 的语法将文本描述转换为流程图、时序图、甘特图等可视化图表，实现“代码即图表”的理念。

## 学习资源

- [Mermaid 中文网](https://mermaid.nodejs.cn/)
- [Mermaid 中文文档](https://docs.min2k.com/zh/mermaid/intro/)
- [Mermaid 在线编辑器](https://www.min2k.com/tools/mermaid/)

## 注释

```
%% 这是一个行注释
```

## 语法结构

- [Mermaid 语法结构](https://docs.min2k.com/zh/mermaid/intro/syntax-reference.html)

## 样板示例

```
%% 指定图表类型为流程图，图表方向为从上到下
flowchart TD
    
    %% 定义节点，节点方向和连接线类型
    A[开始] --> B{条件判断}
    B -->|Yes| C[执行操作A]
    B -->|No| D[执行操作B]
    C --> E[结束]
    D --> E
```

# 流程图

## 节点

- [流程图节点](https://docs.min2k.com/zh/mermaid/syntax/flowchart.html#节点)

    ```
    %% 节点ID(显示文本)
    
    A(这是显示文本)
    ```

    ```mermaid
    flowchart LR
        A(这是显示文本)
    ```


- 显示文本可以使用 HTML

    ```
    %% 节点ID("<font color='red'>显示文本</font>")
    
    A("<font color='red'>显示文本</font>")
    ```

    ```mermaid
    flowchart TD
        A("<font color='red'>黄帝</font>")
    ```

## 流程图方向

[流程图节点形状](https://docs.min2k.com/zh/mermaid/syntax/flowchart.html#节点形状)

```
%% 图表方向为从上到下
flowchart TD
```

- `TD` 或 `TB`：从上到下
- `BT`：从下到上
- `RL`：从右到左
- `LR`：从左到右

## 节点形状

- [流程图节点形状](https://docs.min2k.com/zh/mermaid/syntax/flowchart.html#节点形状)
- `A[方形]`：矩形
- `B(圆角矩形)`：圆角矩形
- `C{菱形}`：菱形
- `D((圆形))`：圆形
- ...

## 节点之间的链接

- [流程图节点之间的链接](https://docs.min2k.com/zh/mermaid/syntax/flowchart.html#节点之间的链接)
- `A-->B` 实线箭头
- `A-- 文本 -->B` 实线箭头带文本
- `A-.->B` 虚线箭头
- `A==>B` 粗实线箭头
- `A--B` 实线
- `A-.B` 虚线

## 破坏语法的特殊字符

- [破坏语法的特殊字符](https://docs.min2k.com/zh/mermaid/syntax/flowchart.html#%E7%A0%B4%E5%9D%8F%E8%AF%AD%E6%B3%95%E7%9A%84%E7%89%B9%E6%AE%8A%E5%AD%97%E7%AC%A6)

    ```
    flowchart LR
        id1["这是一段（文本）"]
    ```
    
    ```mermaid
    flowchart LR
        id1["这是一段（文本）"]
    ```
    
    

## 子图

- 子图

    ```mermaid
    flowchart TB
        subgraph one
        a1-->a2
        end
        subgraph two
        b1-->b2
        end
        subgraph three
        c1-->c2
        end
        c1-->a2
    ```

    ```
    subgraph 子节点标题
        节点描述
    end
    ```

    ```
    flowchart TB
        subgraph one
        a1-->a2
        end
        subgraph two
        b1-->b2
        end
        subgraph three
        c1-->c2
        end
        c1-->a2
    ```

## 交互

- [交互](https://docs.min2k.com/zh/mermaid/syntax/flowchart.html#%E4%BA%A4%E4%BA%92)

    ```mermaid
    flowchart LR
        A-->B
        click B "https://www.github.com" _blank
    ```

    

    ```
    click 节点ID "网址" _blank
    ```

    ```
    click B "https://www.github.com" _blank
    ```

## 样式和类

- [样式和类](https://docs.min2k.com/zh/mermaid/syntax/flowchart.html#%E6%A0%B7%E5%BC%8F%E5%92%8C%E7%B1%BB)

### 节点样式

```
style 节点ID fill:#填充颜色,stroke:#边框色,stroke-width:边框线宽,color:#文字颜色
```

```
flowchart TD
    A(开始) --> B(处理)
    style A fill:#4CAF50,stroke:red,stroke-width:2px,color:red
    style B fill:#FF9800,stroke:blue,stroke-width:2px,color:#000
```

### 连线样式

```
linkStyle 索引 stroke:#连接线颜色,stroke-width:连接线线宽,color:#文字颜色
```

```
flowchart TD
    A --> B
    B --> C
    
    %% 修改第一条边 (A --> B)
    linkStyle 0 stroke:red,stroke-width:2px,color:blue;
```

- 注意：索引从 `0` 开始，按定义连线的顺序计算。

### 样式类定义

```
%% 定义样式类
classDef 类名 fill:#填充颜色,stroke:#边框框色,stroke-width:边框线宽,color:#文字颜色;

%% 应用样式类
class 节点ID1,节点ID2 类名;
```

```
flowchart TD
    A(开始) --> B(处理) --> C(结束)
  
    %% 定义两个样式类
    classDef greenNode fill:#4CAF50,stroke:#333,stroke-width:2px,color:red;
    classDef redNode fill:#F44336,stroke:#000,stroke-width:2px,color:#fff;
  
    %% 应用样式类
    class A greenNode;
    class C redNode;
```

### 全局主题

```
%%{init: {"theme":"base", "themeVariables": {"primaryColor":"#FF9800", "edgeLabelBackground":"#fff"}}%%
flowchart TD
    A[全局主题测试] --> B[结束]
```

# 时序图

# ...