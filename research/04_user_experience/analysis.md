# Predict.fun — 用户体验路径分析

> 数据日期：2026-06-17
> 平台：predict.fun
> 说明：predict.fun 提供 **Web/App 直连** 与 **Binance Wallet 集成** 两条主要入口，体验差异显著。

---

## 1. 用户旅程总览

```mermaid
journey
    title Predict.fun 用户完整体验旅程
    section 初次接触
      通过 CZ/Binance 公告或世界杯活动发现: 4: 用户
      选择 Web 或 Binance Wallet 入口: 4: 用户
      创建账户 (智能钱包自动生成): 4: 用户
    section 入金
      存入 USDT/USDC (最低 10): 3: 用户
      资金进入生息抵押层: 5: 用户
    section 交易
      浏览市场 (体育/政治/加密): 5: 用户
      买入 YES/NO 份额: 5: 用户
      持仓期间资金赚 DeFi 收益: 5: 用户
    section 结算与提现
      事件结束 UMA 预言机裁决: 4: 用户
      赢家份额兑付 1 美元: 5: 用户
      提现 (Gasless): 4: 用户
    section 增长
      累积 Predict Points: 5: 用户
      邀请好友返佣 10%: 4: 用户
```

---

## 2. 注册 / 开户流程

### 2.1 Web/App 入口（Privy 智能钱包）

```mermaid
flowchart TD
    A[访问 predict.fun] --> B[点击登录/连接]
    B --> C{登录方式}
    C -->|邮箱/社交登录| D[Privy 自动创建 Predict Account 智能钱包]
    C -->|已有钱包 EOA| E[连接外部钱包]
    D --> F[进入主界面]
    E --> F
    F --> G[可在账户设置导出 Privy 私钥<br/>用于 SDK 编程交互]
```

### 2.2 Binance Wallet 入口（Keyless Wallet，Gasless）

```mermaid
flowchart TD
    A[Binance App → Binance Wallet] --> B[进入 Prediction Markets 板块]
    B --> C[创建专用 Prediction Account<br/>Binance Keyless Wallet 驱动]
    C --> D[无需私钥 / 无需助记词]
    D --> E[Binance 作为聚合器代付 Gas]
    E --> F[完全 Gasless 交易与兑付]
    F --> G[可先用虚拟资金体验 零风险 Demo]
```

> Binance Wallet 集成是 predict.fun 体验上的最大杀器：**无私钥、无 Gas、可虚拟盘试玩**，把数千万 Binance 用户的开户门槛降到接近零。

---

## 3. 入金（充值）流程

```mermaid
flowchart TD
    A[进入账户余额] --> B[点击 Deposit 充值]
    B --> C{资金来源}
    C -->|已在 BNB Chain| D[直接存入 USDT/USDC<br/>最低 10]
    C -->|在 Binance 交易所| E[从 Binance 提至 BNB Chain]
    C -->|在其他链| F[通过 Rhino Bridge 跨链至 BNB Chain]
    D --> G[资金进入生息抵押层]
    E --> G
    F --> G
    G --> H[激活交易权限]
    H --> I[即便未下注 资金也开始赚 DeFi 收益]
```

- **最低入金**：约 10 USDT/USDC 激活交易。
- **跨链**：官方建议用 **Rhino Bridge** 把其他网络资金桥接到 BNB Chain。
- **结算资产**：交易与兑付以 **USDT** 计价。
- **差异点**：入金后资金即进入生息层（Yield-Bearing），这是与 Polymarket 体验的本质区别。

---

## 4. 交易执行流程

```mermaid
flowchart TD
    A[进入市场列表] --> B[按分类/标签/搜索筛选<br/>体育 政治 加密 全球事件]
    B --> C[进入市场详情页]
    C --> D[查看订单簿 YES/NO 价格与深度]
    D --> E{判断方向}
    E --> F[选择 YES 或 NO]
    F --> G{订单类型}
    G -->|市价| H[输入金额 即时成交]
    G -->|限价| I[输入价格 + 数量 挂单]
    H --> J[EIP-712 签名订单]
    I --> J
    J --> K[链下订单簿撮合]
    K --> L[撮合结果上链 CTFExchange 结算]
    L --> M[持仓更新 + 实时盈亏]
    I --> N[挂单未成交期间<br/>累积做市 Predict Points]
```

### 价格直觉
- YES 份额价格 = 事件发生的隐含概率（$0.42 ≈ 42%）。
- YES + NO = $1.00；买入成本越低、赔率越高。
- 结算时赢家份额兑付 **$1**，输家份额归 **$0**。

---

## 5. 结算流程（UMA 兼容乐观预言机）

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
    alt 无人挑战
        OO->>CTF: 结果生效
    else 有人质押挑战
        OO->>D: 升级至 DVM
        D->>D: UMA 代币持有者投票仲裁
        D->>CTF: 最终结果生效
    end
    CTF->>U: 赢家份额可兑付 $1 / 输家归零
```

- 多数市场（行业经验约 95%）无争议，走「乐观路径」快速结算。
- 有争议时升级 UMA DVM，由代币持有者投票，耗时可能数天。

---

## 6. 提现流程（Gasless）

```mermaid
flowchart TD
    A[点击 Withdraw 提现] --> B[输入提现地址 BNB Chain]
    B --> C[输入 USDT 金额]
    C --> D{账户类型}
    D -->|Predict Account/Binance| E[ZeroDevWithdrawalHelper<br/>账户抽象 Gasless 提现]
    D -->|EOA| F[标准链上交易]
    E --> G[USDT 到账目标地址]
    F --> G
    G --> H[提现完成]
    %% 注: 提现前需先平仓/结算持仓
    %% 注: 提至 CEX 需确认网络为 BNB Chain
```

---

## 7. 增长行为路径（积分与邀请）

```mermaid
flowchart LR
    A[用户行为] --> B[交易量]
    A --> C[做市/提供流动性]
    A --> D[持仓时长]
    A --> E[邀请好友]
    B --> PP[Predict Points 积分]
    C --> PP
    D --> PP
    E --> R[邀请人 10% 永久返佣]
    PP --> LB[排行榜排名]
    LB --> AIR[空投预期]
    R --> AIR
```

详见 [07_token_points_airdrop/analysis.md](../07_token_points_airdrop/analysis.md)。

---

## 8. 小结

predict.fun 的用户体验设计围绕 **「降门槛 + 强激励」** 两条主线：

1. **降门槛**：Binance Keyless Wallet（无私钥）+ Gasless（无 Gas）+ 虚拟盘试玩，几乎消灭了 Web3 的所有摩擦点。
2. **资金高效**：入金即生息，让「放着不动的钱」也产生回报，降低持仓机会成本。
3. **去信任结算**：UMA 兼容乐观预言机保证结果公正，多数市场快速兑付。
4. **强激励飞轮**：Predict Points + 邀请返佣 + 大事件活动，持续拉新与留存。

⚠️ **待实测确认**：Web 入口的 Gas 是否同样免除、生息收益是否实时反映在余额、提现到账时延、争议市场的实际等待时长等，需登录后实操验证。
