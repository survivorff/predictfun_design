# 结算 — 结果上链与赎回

> reportPayouts / resolveCondition / redeemPositions

---

## 流程

```mermaid
flowchart TD
    A[预言机结果生效] --> B[reportPayouts/resolveCondition]
    B --> C[设定 YES/NO 兑付值 1 或 0]
    C --> D{用户持仓}
    D -->|赢家份额| E[redeemPositions 赎回 $1/份]
    D -->|输家份额| F[价值归零 无需操作]
    E --> G[本金 + Venus 收益 - 适用费用 → USDT]
```

---

## 生息市场的赎回差异

普通市场赎回仅返还兑付本金；Predict.fun 生息市场赎回时一并返还 **本金 + 持仓期 Venus 收益**。

> ⚠️ 收益分配比例（用户/平台）官方未公开。

---

> 截至 2026 年 6 月。
