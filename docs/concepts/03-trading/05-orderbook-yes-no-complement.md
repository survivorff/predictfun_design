# 交易 — 订单簿（YES 存储 + NO 取补）

> 只维护 YES 侧订单簿，NO 侧由补数计算

---

## 计价规则（官方文档）

订单簿只存 YES 侧 `bids/asks`，格式 `[price, quantity]`，best 价在前。NO 侧取补：

```text
getComplement(price, precision) = (10^precision - round(price * 10^precision)) / 10^precision
NO 最优买价 = getComplement(asks[0][0])   # YES 最低卖价补数
NO 最优卖价 = getComplement(bids[0][0])   # YES 最高买价补数
```

示例：

```json
{
  "asks": [[0.492, 30192.26], [0.493, 20003]],
  "bids": [[0.491, 303518.1], [0.49, 1365.44]]
}
```

---

## 深度、价差、滑点

| 概念 | 说明 |
|------|------|
| 深度 | 各价位挂单量，决定大单冲击 |
| Spread | best ask − best bid，流动性成本 |
| 滑点 | 大单吃穿多个价位的平均成交劣化 |

> 因 YES+NO=1，YES 与 NO 订单簿互为镜像，流动性互相增强。

---

> 基于 Predict.fun 开发者文档「Understanding the Orderbook」，截至 2026 年 6 月。
