# 链上合约 — CTFExchange

> 订单结算合约（生息 + 非生息双轨）

---

## 作用

CTFExchange 是交易入口：验证 EIP-712 签名、执行订单匹配、收取费用、铸造/转移条件代币。

| 合约 | 地址（BNB Mainnet） |
|------|------|
| CTFExchange（生息） | `0x6bEb5a40C032AFc305961162d8204CDA16DECFa5` |
| CTFExchange（非生息） | `0x8BC070BEdAB741406F4B1Eb65A72bee27894B689` |
| NegRiskCtfExchange（生息） | `0x8A289d458f5a134bA40015085A8F50Ffb681B41d` |
| NegRiskCtfExchange（非生息） | `0x365fb81bd4A24D6303cd2F19c349dE6894D8d58A` |
| FeeModuleV2（生息） | `0xFbC2259aBB3F01c019ECE1d0200Ee673BB7BA34F` |

```mermaid
graph LR
    A[签名订单] --> B[CTFExchange 验证]
    B --> C[匹配 + 收费 FeeModuleV2]
    C --> D[ConditionalTokens 铸造/转移]
```

> 二元市场与多结果（NegRisk）市场各有独立 Exchange。截至 2026 年 6 月。
