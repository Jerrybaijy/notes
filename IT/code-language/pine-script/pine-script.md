# Pine Script 基础

[Pine Script](https://www.tradingview.com/pine-script-docs/) 是 TradingView 开发的专用脚本语言，主要用于在 TradingView 图表中编写指标、策略、报警等脚本。

**资源**：

- [Pine Script Docs](https://www.tradingview.com/pine-script-docs/)
- [Pine Script Reference](https://cn.tradingview.com/pine-script-reference/v6/)

## 基本用法

```pine
//@version=6

strategy("策略名字", overlay=true, ...)
```

- `//@version=6`：声明脚本版本。TradingView 规定必须写在第一行，否则报错。
- `strategy()`：定义一个策略
- `overlay=true`：画在K线图上（否则会单独开一块窗口）。

```pine
fastLength = input.int(9, "快线周期")
```

- `input.int(...)`：允许你在图表里自定义参数。
- 快线（短期均线）的周期是 9。

```pine
plot(fastMA, color=color.orange, title="快线")
```

- `plot(...)`：把均线画到图表上。

# 均线

```pine
//@version=5
strategy("均线交叉策略", overlay=true, margin_long=100, initial_capital=10000)

// 输入参数
fastLength = input.int(9, "快线周期")
slowLength = input.int(21, "慢线周期")

// 计算均线
// ta.sma(收盘价, 周期)
fastMA = ta.sma(close, fastLength)
slowMA = ta.sma(close, slowLength)

// 画出均线
plot(fastMA, color=color.orange, title="快线")
plot(slowMA, color=color.blue, title="慢线")
```

