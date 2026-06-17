# 结果代币 — Gnosis Conditional Token Framework (CTF)

> Predict.fun 预测市场的核心资产：基于 ERC-1155 的条件代币（与 Polymarket 同源）

---

## 什么是条件代币

每个市场生成一对代币 YES/NO，价格始终满足：

```
YES 价格 + NO 价格 = $1.00
```

基于 Gnosis Conditional Token Framework（CTF），遵循 ERC-1155。

| 属性 | 值 |
|------|------|
| 标准 | ERC-1155 |
| 框架 | Gnosis CTF |
| 价值区间 | $0.00 ~ $1.00 |
| 抵押品 | USDT |
| 合约 | ConditionalTokens `0x22DA1810B194ca018378464a58f6Ac2B10C9d244`（非生息） |

> Predict.fun 特有：另有一套 **YieldBearingConditionalTokens** 生息版（见 03-yield-bearing-tokens）。

---

## 生命周期

| 阶段 | 动作 |
|------|------|
| 铸造 (Split) | 锁定 USDT，铸造等量 YES + NO |
| 交易 (Transfer) | 经 CTFExchange 在用户间转移 |
| 合并 (Merge) | 等量 YES + NO 合并销毁，取回 USDT |
| 赎回 (Redeem) | 结算后赢家每份兑换 $1，输家归零 |

---

## 恒等式的意义

- 价格发现：YES 价格即市场对事件概率的共识。
- 订单簿镜像：买 YES @ $0.40 ≈ 卖 NO @ $0.60。
- 无需做市商注入初始流动性即可成立。

---

> 基于 Gnosis CTF 与 Predict.fun 链上合约整理，截至 2026 年 6 月。
