---
title: web3-生态平台
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - web3
---

# BTC

[比特币](https://bitcoin.org/zh_CN/)（Bitconin，简称 BTC）是一种去中心化加密货币，由一个化名为中本聪（ Satoshi Nakamoto ）的人或组织在 2009 年创建，但中本聪的真实身份至今未知。比特币是第一个应用区块链技术的加密货币。

# ETH

以太坊（Ethereum，简称 ETH）是一个开源的、去中心化的区块链平台，它不仅支持原生的加密货币：以太币（ ETH ），还提供了一个运行去中心化应用程序（ DApps ）的生态系统。这些应用程序通过智能合约来实现，运行在以太坊虚拟机（ EVM ）上。

| 对比维度 |          比特币          |       以太坊        |
| :------: | :----------------------: | :-----------------: |
|   愿景   | 全球去中心化加密货币系统 | 全球去中心化计算机  |
|  创始人  |          中本聪          |   Vitalik Buterin   |
| 创建时间 |         2009 年          |       2015 年       |
| 共识机制 |           PoW            |     PoW —> PoS      |
| 核心功能 |         货币交易         | 货币交易 + 智能合约 |
| 出块时间 |         10 分钟          |        12 秒        |
| 编程语言 |        比特币脚本        |      Solidity       |

# Binance

## Alpha

币安 **Alpha** 是币安钱包内的一个平台，币安 Alpha 上展示的部分代币未来有望在币安交易平台上架，但并不保证。Alpha 2.0 将币安 Alpha 集成至币安交易平台，使用户无需切换至币安钱包即可浏览和交易精选代币。用户可以直接使用币安现货账户或资金账户的资金购买 Alpha 代币，简化了交易流程，降低了成本。

### Alpha 积分系统规则

**Alpha 积分系统**是币安用于衡量用户参与度和活跃度的机制，通过资产余额和交易量计算。积分直接影响用户是否能参与币安的 TGE 或空投活动。

YouTube 博主介绍：

- [Alpha 积分查询教程](https://www.youtube.com/watch?v=oXHOndGKf8Q&t=324s)
- [币安 Alpha 刷分演示教程](https://www.youtube.com/watch?v=87MEnao9-tk&t=196s)

#### 查询入口

- 币安 App > 首页 > 更多 > 搜索“Alpha” | 选择“Alpha 活动”
- 币安 App > 首页 > “设置”图标 > 更多服务 > 导航栏选择“资讯” > Alpha 活动
- [币安 Alpha 刷分计算器](https://aja-money-saver.github.io/Nightflyer_BinanceAlpha/BinanceAlpha.html)
- [交易额查询](https://www.bn-alpha.site/)

#### 积分组成

- 资产余额：以下各项的总和

  - 币安交易所各账户资产余额
  - 币安无私钥钱包资产余额
  - 流动性

- 交易量：每日买入 Alpha 代币的总交易额。

余额积分规则（每日计算）

- $0 - $100 = 0 积分/天
- $100 - $1,000 = 1 积分/天
- $1,000 - $10,000 = 2 积分/天
- $10,000 - $100,000 = 3 积分/天
- $100,000 及以上 = 4 积分/天

交易量积分规则（每日计算）

| 日总交易额 | 积分 |
| :--------: | :--: |
|     $2     |  1   |
|     $4     |  2   |
|     $8     |  3   |
|    $16     |  4   |
|    $32     |  5   |
|    ...     | ...  |

以下两种方式购买 Alpha 代币，计算交易量时自动翻倍，每天可**多**获得 1 个交易量积分：

- 购买 **BSC 链**的 Alpha 代币
- 在任何链中通过**限价**购买 Alpha 代币
- 以上两种方式不可叠加翻倍

#### 积分时效

- 每天 UTC 23:59:59 (UTC+8 07:59:59) 更新当日积分，即北京时间 8:00 前的交易，计入前一日的积分。
- 当前积分为过去 15 天的累积积分，每天 14:00 (UTC+8) 之前更新。

#### 消耗积分

- 每日积分的窗口有效期为 15 天
- 参与 TGE 活动消耗 15 积分
- 参与 Alpha 空投消耗 15 积分

#### 其它事宜

- 所有子账户中的余额都会合并至主账户计入积分，不可通过分散资金至子账户获取积分
- 按照买入的交易量计算积分，与卖出的交易量无关

### 刷积分

- 币种选择

  - 优先选择 BSC 链（交易量翻倍），市价买卖（买卖迅速，控制风险）
  - 其次选择其它链，限价买卖（交易量翻倍）
  - 币价必须稳定：只选择 24 小时交易量排名靠前的币
  - 尽量不要刷 Sonic 链，损耗大
  - 目前使用 ZKJ 刷积分

- 时间选择

  - UTC+8 早 8 点前，流动性低，币价波动大，不要刷

- 滑点设置 0.1%
- 网络费用选择“正常”
- 关于磨损

  - 网络费用和交易金额无关，可适当增加单次交易金额
  - 使用币安钱包刷分，磨损更低，共计约 1.5U/9000U

- 如果能达到 1000U 网络费用 0.16U，磨损约为 0.02%

  - 每天需要刷 8192$，每次 1000U，即 9 次/天
  - 每天获得积分为 2 + 14 = 16
  - 刷到 240 分需要 8192 \* 0.02% \* 15 ≈ 25U 的网络费用，总磨损费用控制在 50U，那这样的损耗还是比较可观的

- 注意：如果当前窗口期已经获得了 3 次空投，会消耗 15 \* 3 = 45 分，此时如果还按既定策略刷分，那接下来的积分将会一直是 240 - 45 =195，直到有空投的那天滚动出当前窗口期。
- 如果每 15 天参加 3 次空投，刷分总损耗为 50U，平均奖励为 100U/次，纯利润为 100 \* 3 - 50 = 250U/半月 = 500U/月。
- 刷分可结合 BSC Alpha 交易竞赛，每 15 天可交易 120,000 交易额。可获得 Alpha 空投和交易竞赛的双重奖励。

# Fantom

## Fantom

Fantom 是一个 Layer-1 区块链平台，致力于克服区块链的“不可能三角”（去中心化、安全性和扩展性）。

- **主网名**：Opera
- **原生代币**：
  - FTM 是 Fantom 网络的核心代币
  - S Token 是 Sonic 链的原生代币
- **生态优势**：兼容 EVM
- **产品线**：
  - Fantom 是区块链平台
  - Sonic 是技术升级
  - Sonic Labs 是项目孵化器，基于 Sonic 技术栈开发。

Sonic 资源：

- [Sonic Documentation](https://docs.soniclabs.com/)
- [Sonic Points](https://my.soniclabs.com/points?state=e9vek&code=aURJMXcyS3FOc3FzRWViX3E2ckxjNjlfSmFnaTA2Tk51ZlIyTmcxdlliU2kwOjE3NDYxODQ4MTEzODE6MTowOmFjOjE)
- [Sonic (S) Blockchain Explorer](https://sonicscan.org/)
- [Shadow Exchange](https://www.shadow.so/)

## FeeM

[FeeM](https://www.hackquest.io/zh-cn/learn/146e7446-5ed5-8122-a9c3-c9cb1bad6031/146e7446-5ed5-81d4-bc3c-ecba462d4c14) (Fee Monetization) 本质上是一种 Gas 费用分润机制，Fantom 中初始分成比例为 **15%**，而在 Sonic 中这一比例将逐步提高到 **90%**。

## Sonic Gateway

[Sonic Gateway](https://www.hackquest.io/zh-cn/learn/146e7446-5ed5-8122-a9c3-c9cb1bad6031/14ae7446-5ed5-81f1-9674-f40503fa22b5) 是 Sonic Labs 推出的去中心化**跨链桥**，旨在实现 Ethereum 与 Sonic 区块链之间的安全资产转移。

## Sonic 的共识机制

[Sonic 的共识机制](https://www.hackquest.io/zh-cn/learn/146e7446-5ed5-8122-a9c3-c9cb1bad6031/14ae7446-5ed5-8161-a6e8-dec9e4a8a90a)是以异步拜占庭容错 (aBFT) 和有向无环图 (DAG) 为基础的一种新型共识设计。

### aBFT

[异步拜占庭容错](https://www.hackquest.io/zh-cn/learn/146e7446-5ed5-8122-a9c3-c9cb1bad6031/14ae7446-5ed5-81c6-ae75-e3502998dfa7)（aBFT）是分布式系统中一种强大的**容错机制**，旨在解决网络延迟和恶意行为对共识的影响。

### DAG

[有向无环图](https://www.hackquest.io/zh-cn/learn/146e7446-5ed5-8122-a9c3-c9cb1bad6031/14ae7446-5ed5-81d4-8953-fedad75099c0)（Directed Acyclic Graphs，简称 DAG）支持多个交易并行执行，而非严格按顺序。

## 部署合约

- [在 Sonic 测试链部署合约](https://www.hackquest.io/zh-cn/learn/146e7446-5ed5-8122-a9c3-c9cb1bad6031/146e7446-5ed5-8180-9f87-e410c6d883f8)
- [编译的版本选择](https://www.hackquest.io/zh-cn/learn/146e7446-5ed5-8122-a9c3-c9cb1bad6031/146e7446-5ed5-816b-8473-ee95220ac535)
  - **编译器版本**：指的是用于将 Solidity 源代码编译为字节码的编译器版本。
  - **EVM 版本**指的是合约生成的字节码将针对的以太坊虚拟机版本，即区块链节点运行的程序执行环境。它的作用是执行智能合约代码并确保所有节点就区块链的状态达成共识。

## [Sonic Airdrop](https://docs.soniclabs.com/funding/sonic-airdrop)

空投将使用 Sonic Points、Sonic Gems 和 Game Gems 进行分配

### [Sonic Points](https://my.soniclabs.com/points)

- **Passive Points**: Earn passive points by **holding** [whitelisted assets](https://docs.soniclabs.com/funding/sonic-airdrop/sonic-points#whitelisted-assets) directly in their Web3 wallets.

- **Activity Points**: Earn activity points by **deploying** [whitelisted assets](https://docs.soniclabs.com/funding/sonic-airdrop/sonic-points#whitelisted-assets) as liquidity on participating apps.
- **App Points (Gems)**: Earn **S token** on DApp. Similar to [Sonic Gems](https://docs.soniclabs.com/funding/sonic-airdrop/sonic-gems).
- ~~**Sonic Arcade Points**: Earn **airdrop points** by **playing games**. Similar to [Game Gems](https://docs.soniclabs.com/funding/sonic-airdrop/game-gems). **Closed!**~~
