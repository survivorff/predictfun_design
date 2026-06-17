# 结果代币 — ERC-1155 多代币标准

> 一个合约管理所有市场的 YES/NO 份额

---

## 为什么用 ERC-1155

| 特性 | 价值 |
|------|------|
| 多代币 | 单合约可管理任意多个市场的 YES/NO tokenId |
| 批量操作 | 批量转移/赎回，节省 Gas |
| 半同质化 | 同一市场的份额同质，不同市场不同 tokenId |

---

## tokenId 派生（与 Polymarket 同源）

```
questionId   = keccak256(问题元数据)
conditionId  = keccak256(oracle, questionId, outcomeSlotCount)
tokenId_YES  = f(conditionId, indexSet=YES, 抵押品)
tokenId_NO   = f(conditionId, indexSet=NO,  抵押品)
```

实际开发中无需自行计算，Markets API 直接返回 tokenId。

---

> 截至 2026 年 6 月。
