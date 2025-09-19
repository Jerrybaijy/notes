# 基础

**LaTeX** 是一种广泛用于排版学术论文、书籍、技术文档和数学公式的文本排版系统。

LaTeX 提供了一种标记语言，通过简单的命令格式来控制文档的结构和格式，非常适合科学、数学、工程等领域，尤其在排版复杂的数学公式方面具有强大优势。

**注释方式**：`%`

# 格式

## 强调

```latex
\text{标准体文本}
\textbf{粗体文本}
\textit{斜体文本}
\underline{下划线文本}
```

## 段落与对齐

```latex
\begin{flushleft}   % 左对齐
This text is left-aligned.
\end{flushleft}

\begin{center}      % 居中
This text is centered.
\end{center}

\begin{flushright}  % 右对齐
This text is right-aligned.
\end{flushright}

\hspace{-80mm} 公式内容  % 水平移动（向左移动80mm）

第一行内容\\第二行内容  % 换行
```

## 字体大小

```latex
\large 内容  % 稍大
\Large 内容  % 再大
\LARGE 内容  % 再再大
```

# 数学公式

LaTeX 是以其强大的数学公式排版功能而闻名。

## 显示方式

**行内公式**：用美元符号 `$...$` 包裹

```latex
这是行内公式 $E = mc^2$。
```

渲染效果：这是行内公式 $E = mc^2$。

**独立公式**：用 `$$...$$` (或者 `\[...\]`) 包裹<br>输入完 `$$` 直接按 <kbd>Enter</kbd>

```latex
$$
E = mc^2
$$
```

渲染效果：

> $$
> E = mc^2
> $$

## 默认字体

数学变量为斜体，数字为标准体

## 输入方式

- 分数：`\frac{分子}{分母}`
- 上标：`x^2`
- 下标：`x_2`
- 下标不是个位数：`x_{10}`
- 开根号：`\sqrt{x}`<br>N次方：`\sqrt[n]{x}`
- 求和：`\sum_{i=1}^{n} a_i`
