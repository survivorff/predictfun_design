# Predict.fun — 用户体验路径深度分析（产品）

> 数据日期：2026-06-17
> 平台：predict.fun
> 双入口：**predict.fun Web/App（Privy 智能钱包）** 与 **Binance Wallet 集成（Keyless + Gasless，触达 200M+ 用户）**

---

## 1. 用户旅程总览

```mermaid
journey
    title Predict.fun 用户完整体验旅程
    section 发现
      经 CZ/Binance 公告或世界杯活动发现: 4: 用户
      选择 Web 或 Binance Wallet 入口: 4: 用户
    section 开户
      智能钱包/Keyless 自动创建账户: 4: 用户
      可先用虚拟资金试玩 (Demo): 5: 用户
    section 入金
      存入 USDT/USDC (最低 10): 3: 用户
      资金进入 Venus 生息: 5: 用户
    section 交易
      浏览市场 (体育/政治/加密/AI): 5: 用户
      买入 YES/NO 份额: 5: 用户
      持仓期间资金赚 Venus 收益: 5: 用户
      管理持仓/限价挂单赚做市积分: 4: 用户
    section 结算
      事件结束 UMA 裁决: 4: 用户
      赢家份额赎回 1 美元: 5: 用户
    section 提现与增长
      Gasless 提现: 4: 用户
      累积 Predict Points / 邀请返佣: 5: 用户
```

---

## 2. 双入口体验对比（关键差异）

```mermaid
graph TD
    A{选择入口} --> W[predict.fun Web/App]
    A --> B[Binance Wallet 集成]

    W --> W1[Privy 智能钱包/邮箱社交登录]
    W --> W2[或连接 EOA 外部钱包]
    W --> W3[可导出私钥用于 SDK]

    B --> B1[Binance Keyless Wallet 无私钥]
    B --> B2[Binance 代付 Gas - 完全 Gasless]
    B --> B3[统一账户 无需桥接]
    B --> B4[200M+ Binance 用户一键接入]
```

| 维度 | predict.fun Web/App | Binance Wallet 集成 |
|------|--------------------|--------------------|
| 钱包 | Privy 智能钱包 / EOA | Binance Keyless Wallet |
| 私钥 | 可导出（自托管倾向） | 无私钥（Keyless） |
| Gas | 由账户抽象处理（待确认是否全免） | Binance 代付，完全 Gasless |
| 桥接 | 需自行入金/跨链（Rhino） | 无需桥接，统一账户 |
| 目标用户 | 加密原生/开发者 | 主流/Binance 存量用户 |
| 门槛 | 低 | 极低（接近零） |

> Binance Wallet 集成是 predict.fun 体验上的最大杀器：**无私钥、无 Gas、无桥接、可虚拟盘试玩**，把 2 亿 Binance 用户的开户门槛降到接近零。

---

## 3. 开户流程

### 3.1 Web/App 入口（Privy 智能钱包）

```mermaid
flowchart TD
    A[访问 predict.fun] --> B[点击登录/连接]
    B --> C{登录方式}
    C -->|邮箱/社交登录| D[Privy 自动创建 Predict Account 智能钱包]
    C -->|已有钱包 EOA| E[连接外部钱包]
    D --> F[进入主界面]
    E --> F
    F --> G[账户设置可导出 Privy 私钥<br/>用于 SDK 编程交互]
```

### 3.2 Binance Wallet 入口（Keyless，Gasless）

```mermaid
flowchart TD
    A[Binance App → Binance Wallet] --> B[进入 Prediction Markets 板块]
    B --> C[一键创建 Prediction Account<br/>Binance Keyless Wallet 驱动]
    C --> D[无需私钥 / 无需助记词 / 无需桥接]
    D --> E[Binance 作为聚合器代付 Gas]
    E --> F[完全 Gasless 交易与赎回]
```

### 3.3 Demo / 虚拟盘试玩（降低首单门槛）

```mermaid
flowchart LR
    A[新用户] --> B[使用虚拟资金体验]
    B --> C[零风险熟悉下单/结算]
    C --> D{是否转真实交易}
    D -->|是| E[入金 USDT 开始真实交易]
    D -->|否| F[继续体验/流失]
```

> Binance Wallet 集成支持「虚拟资金、零风险体验真实交易场景」，是典型的「先试玩后入金」转化漏斗。

---

## 4. 入金（充值）流程

```mermaid
flowchart TD
    A[进入账户余额] --> B[点击 Deposit 充值]
    B --> C{资金来源}
    C -->|已在 BNB Chain| D[直接存入 USDT/USDC 最低 10]
    C -->|在 Binance 交易所| E[从 Binance 提至 BNB Chain]
    C -->|在其他链| F[通过 Rhino Bridge 跨链至 BNB Chain]
    D --> G[资金进入 Venus 生息抵押层]
    E --> G
    F --> G
    G --> H[激活交易权限]
    H --> I[即便未下注 资金也开始赚 Venus 收益]
```

- **最低入金**：约 10 USDT/USDC 激活交易。
- **跨链**：官方建议用 **Rhino Bridge** 把其他网络资金桥接到 BNB Chain。
- **结算资产**：交易与赎回以 **USDT** 计价。
- **差异点**：入金后资金即进入 Venus 生息层——这是与 Polymarket 体验的本质区别。

---

## 5. 市场发现与交易执行

### 5.1 市场发现

```mermaid
flowchart LR
    A[首页] --> B[按品类浏览<br/>加密/体育/政治/宏观/娱乐/AI]
    A --> C[搜索 关键词]
    A --> D[热门/Trending/Boosted 市场]
    B --> E[进入市场详情]
    C --> E
    D --> E
    E --> F[查看订单簿/价格/概率/历史时序]
```

### 5.2 交易执行

```mermaid
flowchart TD
    A[市场详情页] --> B[查看 YES/NO 价格与订单簿深度]
    B --> C{判断方向}
    C --> D[选择 YES 或 NO]
    D --> E{订单类型}
    E -->|市价 Market| F[输入金额 即时成交]
    E -->|限价 Limit| G[输入价格 + 数量 挂单]
    F --> H[EIP-712 签名订单]
    G --> H
    H --> I[链下订单簿撮合]
    I --> J[撮合结果上链 CTFExchange 结算]
    J --> K[持仓更新 + 实时盈亏]
    G --> L[挂单未成交期间<br/>每分钟快照累积做市积分]
```

### 5.3 价格直觉
- YES 份额价格 = 事件发生隐含概率（$0.42 ≈ 42%）。
- **YES + NO = $1.00**；订单簿只存 YES 侧，NO 侧取补数。
- 结算时赢家份额兑付 **$1**，输家份额归 **$0**。

---

## 6. 持仓管理与赎回

```mermaid
flowchart TD
    A[持仓页面] --> B[查看每个市场的 YES/NO 头寸]
    B --> C[实时盈亏 + 当前市价]
    C --> D{操作}
    D -->|提前平仓| E[卖出份额 锁定盈亏]
    D -->|继续持有| F[等待事件结算 + 抵押持续生息]
    F --> G[事件结束 UMA 裁决]
    G --> H{结果}
    H -->|押对| I[赢家份额赎回 $1/share]
    H -->|押错| J[输家份额归零]
    I --> K[本金/收益回到余额]
```

---

## 7. 结算流程（UMA 兼容乐观预言机）

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
        D->>CTF: 最终结果生效 (耗时数小时~数天)
    end
    CTF->>U: 赢家份额赎回 $1 / 输家归零
```

---

## 8. 提现流程（Gasless）

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

## 9. 增长行为路径（积分与邀请）

```mermaid
flowchart LR
    A[用户行为] --> B[交易量]
    A --> C[做市/提供流动性]
    A --> D[持仓时长]
    A --> E[邀请好友]
    A --> F[赛事活动 世界杯]
    B --> PP[Predict Points]
    C --> PP
    D --> PP
    F --> PP
    E --> R[邀请人 10% 永久返佣]
    PP --> LB[排行榜]
    LB --> AIR[空投预期]
    R --> AIR
```

> 详见 [07_token_points_airdrop/analysis.md](../07_token_points_airdrop/analysis.md)。

---

## 10. 体验边界与待实测

```mermaid
graph TD
    Q[待实测确认] --> Q1[Web 入口 Gas 是否同样全免]
    Q --> Q2[生息收益是否实时反映在余额]
    Q --> Q3[提现到账时延]
    Q --> Q4[争议市场实际等待时长]
    Q --> Q5[地域限制 geo-block 范围]
    Q --> Q6[最低/最高下单限制 滑点保护]
```

⚠️ 以上流程基于官方文档与媒体描述绘制，**未经亲手登录实测**；建议登录 Web 与 Binance Wallet 两条路径核验。

---

## 11. 小结

predict.fun 的产品/体验设计围绕 **「降门槛 + 资金高效 + 强激励」** 三条主线：

1. **降门槛到极致**：Binance Keyless（无私钥）+ Gasless（无 Gas）+ 无桥接 + 虚拟盘试玩，几乎消灭 Web3 所有摩擦点，把 2 亿 Binance 用户变成潜在池。
2. **资金高效**：入金即经 Venus 生息，让闲置资金产生回报，降低持仓机会成本。
3. **去信任结算**：UMA 兼容乐观预言机保证结果公正，多数市场快速兑付。
4. **强激励飞轮**：Predict Points + 邀请 10% 返佣 + 大事件活动，持续拉新留存。
5. **双入口策略**：Web/App 服务加密原生与开发者，Binance Wallet 服务主流大众，覆盖全谱系用户。
