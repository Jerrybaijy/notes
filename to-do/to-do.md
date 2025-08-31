# To-Do

## Daily

- [x] [Alpha 积分](https://www.binance.com/zh-CN/alpha/bsc/0xc71b5f631354be6853efe9c3ab6b9590f8302e81)
- [x] [签到](https://www.binance.com/zh-CN/rewards-hub)
- [x] [每日一词](https://www.binance.com/en/activity/word-of-the-day/entry)
- [x] [币安最新活动](https://www.binance.com/zh-CN/support/announcement/list/93)
- [ ] [Air Drop](https://airdrops.io/)
- [ ] [Benjieming 的撸毛之旅](https://www.youtube.com/@Benjieming1Q84/videos)
- [ ] [KAITO](https://yaps.kaito.ai/)
- [ ] [Cookie.fun](https://www.cookie.fun/)
- [ ] [Alpha Batcher](https://www.binance.com/zh-CN/square/profile/alphabatcher)

## Today

- [ ] 根据钱包地址，在浏览器中查看交易信息
- [ ] 在浏览器中，查看某个币的交易情况
- [ ] [Ref 空投](https://medium.com/iost/airdrop-announcement-for-supported-exchanges-f15a57e59929)
- [ ] [dune：做报表](https://dune.com/home)
- [ ] [dune 课程](https://www.youtube.com/playlist?list=PLK3b5d4iK10ext4v-GBySekaA8-GP8quD)
- [ ] B2
- [ ] [币安现货交易者联盟竞赛](https://www.binance.com/zh-CN/support/announcement/detail/42fff57918a3409db989bef3e4d3e6e7)
- [ ] [币圈工具汇总](https://x.com/Benjieming1Q84/status/1874658038264873176)

## 备忘

- 腾讯会议
    - 696-927-9960
    - 588039







# 均线策略

## 开多

条件1：多长时间内，振幅不小

条件2：

- 快线上穿慢线
- 等待 2min，如果 `快线 > 慢线`，则开多

## 平多

条件1：如果 `盈利 3%`，平仓

条件2：如果 `盈利 < 3%` 且 `快线 < 慢线`，等待 1min，如果仍然 `快线 < 慢线`，平仓



1. 如果盈利从未达到3%，那么一旦 `快线 < 慢线`，等待 1min，如果仍然 `快线 < 慢线`，则全部平仓
2. 如果盈利达到3%
    1. 先平仓一半
    2. 一旦 `快线 < 慢线`，等待 1min，如果仍然 `快线 < 慢线`，平仓另一半



## 新平多

1. 开仓之后，在盈利达到1%之前，一旦 `快线 < 慢线`，等待 1min，如果仍然 `快线 < 慢线`，则平仓全部
2. 开仓之后，如果盈利达到1%
    1. 先平仓一半
    2. 平完一半以后，一旦 `快线 < 慢线`，等待 1min，如果仍然 `快线 < 慢线`，则平仓另一半
