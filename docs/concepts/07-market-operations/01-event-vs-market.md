# 市场运营 — Event vs Market

> 一个事件可包含多个可交易市场

---

```mermaid
graph TD
    E[Event 事件主题] --> M1[Market 二元问题1 YES/NO]
    E --> M2[Market 二元问题2 YES/NO]
    M1 & M2 --> NR[NegRisk 多结果互斥组]
```

| 概念 | 说明 |
|------|------|
| Event | 现实事件主题（如「世界杯冠军」），可含多个 Market |
| Market | 具体可交易的二元问题 |
| NegRisk | 将多选一的 Market 组织为互斥组 |

- API 通过 categories / tags / search 组织市场发现。

---

> 截至 2026 年 6 月。
