# Predict.fun 结算机制与预言机

> UMA 兼容乐观预言机、结果上链、赎回机制与争议处理

---

## 1. 结算总览

Predict.fun 使用 **UMA 兼容乐观预言机（UmaCompatibleOptimisticOracle）** 裁定事件结果——这是 Polymarket 同源的去信任结算方案。

```mermaid
sequenceDiagram
    participant E as 现实事件
    participant P as 提议者 Proposer
    participant OO as UmaCompatibleOptimisticOracle
    participant D as UMA DVM 仲裁
    participant CTF as 条件代币合约
    participant U as 用户
    E->>P: 事件结束 (结果已知)
    P->>OO: 质押保证金 提交结果 (乐观提交)
    alt 无人挑战 (约 95% 市场)
        OO->>CTF: 结果生效 (快速结算)
    else 有人质押挑战
        OO->>D: 升级至 DVM
        D->>D: UMA 代币持有者投票仲裁
        D->>CTF: 最终结果生效 (数小时~数天)
    end
    CTF->>U: 赢家份额赎回 $1 / 输家归零
```

---

## 2. 乐观预言机原理

| 阶段 | 说明 |
|------|------|
| **提议 (Propose)** | 提议者质押保证金，乐观提交结果 |
| **争议窗口** | 一段时间内任何人可质押挑战 |
| **乐观路径** | 无挑战 → 结果直接生效（多数市场，行业经验约 95%） |
| **争议升级** | 有挑战 → 升级 UMA DVM，由代币持有者投票裁决 |

> 乐观路径下结算快；争议升级则可能耗时数小时到数天。

---

## 3. 结果上链与赎回

```mermaid
flowchart TD
    A[预言机结果生效] --> B[reportPayouts / resolveCondition]
    B --> C[YES/NO 份额价值确定]
    C --> D{用户持仓}
    D -->|持有赢家份额| E[redeemPositions 赎回 $1/share]
    D -->|持有输家份额| F[价值归零 无需操作]
    E --> G[扣除适用费用后 USDT 到账]
```

- 结果生效后，合约设定 YES/NO 的兑付值（如 YES=1, NO=0）。
- 用户调用赎回（redeem）将赢家份额兑换为 USDT；输家份额自动归零。
- 生息市场下，赎回时本金 + 持仓期 Venus 收益一并返还（收益分配比例待确认）。

---

## 4. 争议机制

```mermaid
flowchart LR
    A[提议结果] --> B{是否被质押挑战?}
    B -->|否| C[乐观路径 结果生效]
    B -->|是| D[升级 UMA DVM]
    D --> E[UMA 代币持有者投票]
    E --> F[最终结果生效]
    F --> G[错误方保证金被罚没]
```

- 争议通过经济激励（质押/罚没）保证提议诚实。
- DVM 作为最终仲裁后盾，确保结果尽可能准确。

---

## 5. 与 Polymarket 结算对比

| 维度 | Predict.fun | Polymarket |
|------|-------------|------------|
| 预言机 | UMA 兼容乐观预言机 | UMA 乐观预言机 |
| 适配器 | UmaCompatibleCtfAdapter | UMA CTF Adapter |
| 争议后盾 | UMA DVM | UMA DVM |
| 结算资产 | USDT | USDC.e |
| 生息赎回 | 本金 + Venus 收益 | 仅本金 |

---

> 基于 Predict.fun 链上合约与 UMA 机制整理，截至 2026 年 6 月。
