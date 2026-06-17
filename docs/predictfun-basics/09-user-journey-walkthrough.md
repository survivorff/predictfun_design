# Predict.fun 用户完整体验流程

> 以用户 Leo 的视角走完 Predict.fun 所有核心功能：开户 → 入金（生息）→ 交易 → 持仓 → 结算 → 赎回 → 提现。
> 每阶段配时序图与具体数字示例。

---

## 场景设定

Leo 是一个 Binance 用户，看好阿根廷在 2026 世界杯夺冠。他准备用 $200 在 Predict.fun 交易，并体验「押注期间资金还能生息」。

---

## 阶段一：开户（Binance Wallet 入口）

```mermaid
sequenceDiagram
    participant Leo as Leo
    participant BW as Binance Wallet
    participant PF as Predict.fun
    participant BNB as BNB Chain
    Leo->>BW: 1. 打开 Binance App → Wallet → Prediction Markets
    BW->>PF: 2. 加载 Predict.fun 集成
    Leo->>BW: 3. 一键创建 Prediction Account
    BW->>BW: 4. Binance Keyless Wallet 生成账户(无私钥)
    BW-->>Leo: 5. 开户完成，地址 0xLeo...，余额 $0
    Leo->>PF: 6. 先用虚拟资金试玩一笔(零风险)
    PF-->>Leo: 7. 熟悉下单/结算流程
```

此时 Leo：有了 BNB Chain 账户（Keyless，无需管私钥），余额 $0，可浏览所有市场，并已用虚拟盘熟悉流程。

---

## 阶段二：入金（资金即生息）

```mermaid
sequenceDiagram
    participant Leo as Leo
    participant PF as Predict.fun
    participant Bin as Binance 交易所
    participant BNB as BNB Chain
    participant V as Venus Protocol
    Leo->>PF: 1. 点击 Deposit，选择从 Binance 划转
    Leo->>Bin: 2. 从 Binance 提 200 USDT 到 BNB Chain 地址
    Bin->>BNB: 3. 转账 200 USDT → 0xLeo
    BNB-->>PF: 4. 到账确认
    PF->>V: 5. 抵押品包装并供给 Venus 生息
    PF-->>Leo: 6. 余额 200 USDT，已开始赚 Venus 收益(~8% APY 示意)
```

| 项目 | 金额 |
|------|------|
| 入金 | 200 USDT |
| 到账 | 200 USDT |
| 状态 | 即便未下注，已在 Venus 生息 |

---

## 阶段三：浏览市场与研究

```mermaid
sequenceDiagram
    participant Leo as Leo
    participant PF as Predict 前端
    participant API as Predict API
    Leo->>PF: 1. 进入「体育/世界杯」分类
    PF->>API: 2. GET /markets?category=worldcup&order=volume
    API-->>PF: 3. 返回热门市场列表
    PF-->>Leo: 4. "阿根廷夺冠?" YES $0.25 / NO $0.75，24h量 $2.1M
    Leo->>PF: 5. 点击进入市场详情
    PF->>API: 6. GET /markets/{id} + orderbook + timeseries
    API-->>PF: 7. 概率走势 + 订单簿深度 + 结算规则
    PF-->>Leo: 8. 展示详情页
```

| 字段 | 值 | 含义 |
|------|------|------|
| YES 价格 | $0.25 | 市场认为阿根廷夺冠概率 25% |
| NO 价格 | $0.75 | 75% 概率不夺冠 |
| Best Ask (YES) | $0.26 | Leo 现在买 YES 的最低价 |
| Spread | $0.02 | 买卖价差 |

Leo 认为阿根廷被低估，决定买入 YES。

---

## 阶段四：买入 YES 份额（开仓）

```mermaid
sequenceDiagram
    participant Leo as Leo
    participant PF as Predict 前端
    participant CLOB as CLOB 后端
    participant W as Keyless 钱包
    participant EX as CTFExchange
    Leo->>PF: 1. 输入：YES，$100，市价单
    PF->>CLOB: 2. GET orderbook
    CLOB-->>PF: 3. Best Ask $0.25，深度充足
    PF->>PF: 4. 预览：$100 买 400 份 YES @ $0.25<br/>赢则 400×$1=$400，潜在利润 +$300
    Leo->>PF: 5. 确认
    PF->>W: 6. EIP-712 签名订单(Keyless 内部完成，无感)
    W-->>PF: 7. 返回签名订单
    PF->>CLOB: 8. POST /order (GTC)
    CLOB->>CLOB: 9. 撮合成功
    CLOB->>EX: 10. 链上结算(Gas 由 Binance 代付)
    EX-->>Leo: 11. 持仓 400 YES，花费 $100
```

| 资产 | 变化前 | 变化后 |
|------|--------|--------|
| USDT 余额 | $200 | $100（仍在生息） |
| YES 份额 | 0 | 400 份（市值 $100） |
| 总资产 | $200 | $200 |

> 注意：未下注的 $100 与抵押的 $100 都在 Venus 生息。

---

## 阶段五：持仓管理与实时盈亏

一个月后阿根廷小组赛全胜，YES 价格从 $0.25 涨到 $0.40。

```mermaid
sequenceDiagram
    participant WS as WebSocket
    participant PF as Predict 前端
    participant Leo as Leo
    WS-->>PF: price_change: YES = $0.40
    PF->>PF: 重算：400 份 × $0.40 = $160<br/>浮盈 +$60 (+60%) + 持仓期 Venus 收益
    PF-->>Leo: 持仓页实时更新
```

| 选项 | 操作 | 结果 |
|------|------|------|
| 继续持有 | 不操作 | 等结算，赢则拿 $400；期间持续生息 |
| 提前止盈 | 卖 400 份 @ $0.39 | 立即拿 ~$156，锁定 $56 利润 |
| 部分卖出 | 卖 200 份 | 锁定部分利润，保留仓位 |

Leo 选择卖出一半（200 份）止盈。

---

## 阶段六：提前卖出（部分止盈）

```mermaid
sequenceDiagram
    participant Leo as Leo
    participant PF as Predict 前端
    participant CLOB as CLOB
    participant EX as CTFExchange
    Leo->>PF: 1. 卖出 200 份，市价
    PF->>PF: 2. 预览：200 × $0.39 = $78
    Leo->>PF: 3. 确认 → EIP-712 签名
    PF->>CLOB: 4. POST /order (SELL)
    CLOB->>EX: 5. 撮合 + 链上结算
    EX-->>Leo: 6. 卖出成功，获得 $78
```

| 资产 | 变化前 | 变化后 |
|------|--------|--------|
| USDT 余额 | $100 | $178 |
| YES 份额 | 400 | 200 |
| 已实现利润 | $0 | +$28（200 份成本 $50，卖得 $78） |

---

## 阶段七：事件结算（YES 获胜）

2026 年 7 月世界杯决赛，阿根廷夺冠。结果为 YES。

```mermaid
sequenceDiagram
    participant Real as 现实
    participant P as 提议者
    participant OO as UMA 兼容预言机
    participant CTF as 条件代币合约
    participant Leo as Leo
    Real->>P: 阿根廷夺冠，结果 YES
    P->>OO: 质押保证金 提交 YES
    OO->>OO: 争议窗口内无人挑战
    OO->>CTF: 结果生效 YES=1, NO=0
    CTF-->>Leo: 通知：可赎回 200 份 YES = $200
```

---

## 阶段八：赎回 + 提现

```mermaid
sequenceDiagram
    participant Leo as Leo
    participant PF as Predict 前端
    participant CTF as 条件代币合约
    participant V as Venus
    participant Ext as 外部地址
    Leo->>PF: 1. 点击 Claim
    PF->>CTF: 2. redeemPositions(200 YES)
    CTF->>V: 3. 赎回本金 + 持仓期 Venus 收益
    CTF-->>Leo: 4. 200 USDT + 生息收益到账(扣适用费用)
    Leo->>PF: 5. 点击 Withdraw 提现 $370
    PF->>Ext: 6. ZeroDevWithdrawalHelper Gasless 提现
    Ext-->>Leo: 7. USDT 到账(BNB Chain)
```

---

## 完整收益总结

| 阶段 | 操作 | 金额变化 |
|------|------|---------|
| 入金 | 从 Binance 划转 | +$200（即生息） |
| 买入 | 400 份 YES @ $0.25 | -$100 |
| 卖出 | 200 份 YES @ $0.39 | +$78 |
| 结算 | 200 份 YES 赎回 | +$200 + 生息收益 |
| 生息 | 持仓期 Venus 收益（示意） | +约 $1–$3 |
| Gas | 全程 Gasless | $0 |

**最终盈亏**：投入 $200 → 产出约 $378+ → 净利润约 **+$178+**（含生息），且全程零 Gas。

---

## 附录：如果 Leo 预测错误（NO 获胜）

```mermaid
sequenceDiagram
    participant OO as UMA 兼容预言机
    participant CTF as 条件代币合约
    participant Leo as Leo
    OO->>CTF: 结果 NO，YES=0
    CTF-->>Leo: 200 份 YES 归零，无需操作
    Note over Leo: 仍保留：卖出止盈的 $78 + 持仓期生息收益<br/>生息收益部分抵消亏损
```

失败场景：因提前卖出锁定了 $78，加上生息收益，总亏损被控制——这正是「提前止盈 + 生息缓冲」的价值。

---

> 本文档基于 Predict.fun 公开功能、开发者文档与媒体报道整理，截至 2026 年 6 月。所有数字为示例，实际结果取决于市场条件与官方收益/费率规则。
