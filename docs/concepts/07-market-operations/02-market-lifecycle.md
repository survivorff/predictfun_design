# 市场运营 — 市场生命周期

> 创建 → 交易 → 锁定 → 结果 → 结算 → 赎回

---

```mermaid
stateDiagram-v2
    [*] --> 创建
    创建 --> 交易中: 开放下单 + 抵押品 Venus 生息
    交易中 --> 锁定: 事件截止
    锁定 --> 结果提交: UMA 乐观提交
    结果提交 --> 已结算: 无争议
    结果提交 --> 争议仲裁: 有挑战
    争议仲裁 --> 已结算
    已结算 --> 赎回: 赢家 $1 / 输家归零
    赎回 --> [*]
```

| 阶段 | 涉及合约 |
|------|---------|
| 创建 | ConditionalTokens / NegRisk |
| 交易中 | CTFExchange / YieldBearingWrappedCollateral / Venus |
| 结果/争议 | UmaCompatibleCtfAdapter / OptimisticOracle / DVM |
| 赎回 | redeemPositions / Venus |

> 详见 basics/11-event-market-lifecycle。截至 2026 年 6 月。
