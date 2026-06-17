# Predict.fun 钱包体系与资产结构

> 账户分层、Privy/Keyless 钱包、USDT 资产、授权机制

---

## 1. 账户体系总览

Predict.fun 支持三类账户，覆盖从开发者到主流大众的全谱系用户：

```mermaid
flowchart TD
    A{账户类型} --> B[EOA 外部账户]
    A --> C[Predict Account 智能钱包]
    A --> D[Binance Keyless Wallet]
    B --> B1[开发者/高级用户<br/>直接对接协议]
    C --> C1[基于 Privy 自动创建]
    C --> C2[邮箱/社交登录即用]
    C --> C3[可在设置导出私钥用于 SDK]
    D --> D1[Binance Wallet 集成专用]
    D --> D2[无私钥/无助记词]
    D --> D3[Binance 代付 Gas]
    C --> E[ZeroDev 账户抽象]
    D --> E
    E --> F[Gasless 交易/提现]
```

| 账户类型 | 适用人群 | 私钥 | Gas |
|---------|---------|------|-----|
| **EOA** | 开发者/高级用户 | 自管 | 自付 |
| **Predict Account (Privy)** | Web/App 主流用户 | Privy 托管，可导出 | 账户抽象处理 |
| **Binance Keyless Wallet** | Binance 存量用户 | 无私钥 | Binance 代付 |

---

## 2. Predict Account（Privy 智能钱包）

- Web App 用户登录（邮箱/社交）即自动创建，基于 **Privy**。
- 可在 `predict.fun/account/settings` 导出 Privy 私钥，用于 SDK 编程交互。
- 配合 **ZeroDev 账户抽象**，支撑 Gasless 体验。

```mermaid
sequenceDiagram
    participant U as 用户
    participant PM as Predict 前端
    participant Privy as Privy 钱包服务
    participant BNB as BNB Chain
    U->>PM: 选择邮箱/社交登录
    PM->>Privy: OAuth 认证
    Privy->>Privy: 生成 BNB Chain 智能钱包(Predict Account)
    Privy-->>PM: 返回地址 + session
    PM->>BNB: 查询余额
    BNB-->>PM: USDT 余额
    PM-->>U: 开户完成，提示充值
```

---

## 3. 资产结构

| 资产 | 标准 | 作用 |
|------|------|------|
| **USDT** | ERC-20 (BNB Chain) | 交易抵押品与结算货币 |
| **YES/NO 份额** | ERC-1155（条件代币 CTF） | 事件结果头寸，价值 $0~$1 |
| **生息包装抵押品** | YieldBearingWrappedCollateral | USDT 经包装后供给 Venus 生息 |

核心恒等式：`1 YES + 1 NO = $1`。赢家份额结算兑付 $1，输家归 $0。

---

## 4. 授权机制（Allowance）

与 Polymarket 类似，首次交易需完成链上授权（一次性），之后交易仅需 EIP-712 离线签名：

```mermaid
sequenceDiagram
    participant U as 用户
    participant PM as Predict 前端
    participant W as 钱包(Privy/Keyless)
    participant BNB as BNB Chain
    U->>PM: 首次下单
    PM-->>U: 提示完成授权(仅一次)
    PM->>W: 授权 #1 USDT.approve(CTFExchange)
    W->>BNB: 记录授权 (Gas 代付)
    PM->>W: 授权 #2 ERC1155.setApprovalForAll(CTFExchange)
    W->>BNB: 记录授权 (Gas 代付)
    PM-->>U: 授权完成，后续仅需离线签名
```

| 授权 | 作用 |
|------|------|
| `USDT.approve(CTFExchange)` | 允许交易所划转抵押品 |
| `setApprovalForAll(CTFExchange)` | 允许交易所转移 ERC-1155 份额 |

> Gasless：授权与交易的 Gas 由账户抽象 / Binance 代付，用户无需持有 BNB。

---

## 5. 入金与提现

- **入金**：BNB Chain 直接存 USDT/USDC（最低约 10）、从 Binance 提币、或经 **Rhino Bridge** 跨链。入金后资金进入 Venus 生息层。
- **提现**：经 `ZeroDevWithdrawalHelper` 账户抽象 Gasless 提现至 BNB Chain 地址（提现前需先平仓/结算持仓）。

---

> 基于 Predict.fun 开发者文档整理，截至 2026 年 6 月。
