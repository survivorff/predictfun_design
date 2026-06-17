# Predict.fun 平台概览与商业模式

> BNB Chain 原生预测市场 — YZi Labs 支持、CZ 站台、半年累计交易量破 $18 亿

---

## 目录

1. [什么是 Predict.fun](#1-什么是-predictfun)
2. [核心业务模式](#2-核心业务模式)
3. [商业模式与收入](#3-商业模式与收入)
4. [市场数据与增长里程碑](#4-市场数据与增长里程碑)
5. [融资历程与资本背景](#5-融资历程与资本背景)

---

## 1. 什么是 Predict.fun

Predict.fun 是建立在 **BNB Chain** 上的链上预测市场平台，由 **Dingaling（@dingalingts，前 Binance 研究负责人、PancakeSwap 联合创始人）** 创立，**YZi Labs（原 Binance Labs）** 在 inception 阶段投资，**CZ（赵长鹏）** 于 2025 年 12 月公开预告站台。

用户在平台上就现实世界事件的结果进行交易——通过买卖「事件份额（YES/NO Shares）」表达对事件发生概率的判断。

官网口号：*"The BNB-native information market where it pays to be right."*

### 平台定位

- **信息聚合工具**：市场价格反映集体智慧
- **投机交易平台**：交易事件概率获利
- **资本高效**：押注期间抵押品经 **Venus Protocol** 生息（最大差异化）
- **大众入口**：通过 **Binance Wallet** 触达 200M+ 用户，Gasless 一键交易

事件类型覆盖：加密价格、体育（NBA/NFL/足球）、政治、宏观经济、娱乐、AI 里程碑。

> **一句话本质**：Predict.fun ≈「Polymarket 成熟架构」+「BNB 链」+「生息抵押（Venus）」+「Binance 2 亿用户渠道」+「亚洲市场」。

---

## 2. 核心业务模式

### 2.1 事件市场运作原理

每个事件是一个**二元问题**（Yes or No），例如："Will BTC close above $120K by Sep 2026?"

| 要素 | 说明 |
|------|------|
| **YES 份额** | 代表事件会发生，价格 $0 ~ $1 |
| **NO 份额** | 代表事件不会发生，价格 $0 ~ $1 |
| **核心恒等式** | `1 YES + 1 NO = $1`（永远成立） |
| **价格 = 概率** | YES 价格 $0.65 意味市场认为有 65% 概率发生 |
| **结算** | 正确结果份额价值变为 $1，错误的变为 $0 |
| **结算资产** | USDT |

### 2.2 交易盈亏示例

```mermaid
flowchart TD
    subgraph 示例["💰 'BTC 是否在 9 月前突破 $120K'"]
        Start["用户花 $65 买入 100 份 YES（$0.65/份）<br/>同时抵押资金在 Venus 生息"]
        Start --> Win["✅ 事件发生<br/>100 × $1 = $100<br/>净利润 = $35 + 持仓期 Venus 收益"]
        Start --> Lose["❌ 事件未发生<br/>100 × $0 = $0<br/>净亏损 = $65（部分被生息收益抵消）"]
        Start --> Early["📊 提前卖出<br/>价格涨到 $0.80 卖出<br/>100 × $0.80 = $80，净利润 = $15"]
    end
    style Win fill:#2ecc71,color:#fff
    style Lose fill:#e74c3c,color:#fff
    style Early fill:#f39c12,color:#fff
```

### 2.3 业务流程总览

```mermaid
flowchart LR
    subgraph 市场创建
        A1[平台创建事件] --> A2[设定二元问题 YES/NO]
        A2 --> A3[发布到链上 CTF 合约]
    end
    subgraph 交易流程
        B1[用户存入 USDT] --> B2[抵押品进入 Venus 生息]
        B2 --> B3[买入 YES/NO 份额]
        B3 --> B4[持有等待结算 或 提前卖出]
    end
    subgraph 结算机制
        C1[事件到期] --> C2[UMA 兼容预言机提议结果]
        C2 --> C3[争议窗口]
        C3 --> C4[结果上链]
        C4 --> C5[胜方份额 = $1 败方 = $0]
    end
    市场创建 --> 交易流程 --> 结算机制
```

---

## 3. 商业模式与收入

### 3.1 费用模型

| 费用类型 | 费率 | 说明 |
|---------|------|------|
| **交易手续费** | ~2% 峰值 | 概率加权，随价格偏离 50% 递减 |
| **Gas 费** | 平台/Binance 承担 | Gasless（账户抽象 + Binance 代付） |
| **生息收益分成** | 待确认 | 抵押品 Venus 收益，平台可能抽取部分 |

### 3.2 收入来源

```mermaid
pie title Predict.fun 收入来源推测
    "交易手续费 (概率加权 ~2%)" : 60
    "生息收益分成 (Venus, 待确认)" : 25
    "做市/价差相关" : 8
    "生态/渠道合作" : 7
```

- **交易手续费**：主收入，概率加权（p×(1−p)），中点最高、极端价格趋零。
- **生息收益分成**：$20M+ 用户资金经 Venus 生息，潜在第二曲线。
- **生态/渠道**：API、Binance 合作分润。

### 3.3 与竞品收入模型对比

| 平台 | 收费方式 | 费率 |
|------|---------|------|
| **Predict.fun** | 概率加权交易费 + 生息分成 | ~2% 峰值 |
| Polymarket | 长期免交易费 | $0（变现靠数据/其他） |
| Kalshi | 交易手续费 | 概率加权 |
| 传统博彩 | 赔率差 (Vig) | 5-10% |

---

## 4. 市场数据与增长里程碑

### 4.1 发展时间线

```mermaid
timeline
    title Predict.fun 发展里程碑
    2025-12-04 : CZ 推特预告 : 约 1.2 万用户 / $30 万累计量
    2025-12-16 : 正式上线 : YZi Labs 初始投资
    2026-03 : 收购 Probable : 累计 $1.5B / 12 万用户 / 330 万笔
    2026-04 : YZi + Susquehanna 复投 : 累计 $1.8B+ / 13 万+用户 / 400 万+订单
    2026-04 : Binance Wallet 集成 : 触达 200M+ 用户 Gasless
    2026-06 : 世界杯 $2M Predict Cup : 3 天 2 万 DAU / 18 万笔每日
```

### 4.2 关键市场指标

| 指标 | 数据 | 时间 |
|------|------|------|
| 累计交易量 | **$1.8B+** | 2026-04 |
| 注册用户 | **130,000+** | 2026-04 |
| 撮合订单 | **4,000,000+** | 2026-04 |
| 生息中资金 | **$20M+** | 2026-04 |
| TVL | ~$16.9M | DefiLlama |
| 2025 行业名义交易量 | ~$44B | CMC |
| Kalshi+Polymarket 行业占比 | ~87.6% | 2025 |

### 4.3 市场类别分布（示意）

```mermaid
pie title Predict.fun 市场类别分布 (示意)
    "体育(含世界杯)" : 40
    "加密价格" : 25
    "政治" : 15
    "宏观经济" : 8
    "娱乐/文化" : 7
    "AI 里程碑" : 5
```

> ⚠️ 类别占比为基于品类与活动的示意推断，非官方披露。

---

## 5. 融资历程与资本背景

```mermaid
flowchart LR
    A["2025.12<br/>YZi Labs<br/>inception 投资"] --> B["2026.03<br/>收购 Probable<br/>整合亚洲社区"]
    B --> C["2026.04<br/>YZi + Susquehanna<br/>follow-on 复投"]
    style A fill:#3498db,color:#fff
    style B fill:#e67e22,color:#fff
    style C fill:#e74c3c,color:#fff
```

### 5.1 关键投资者与团队

| 项目 | 详情 |
|------|------|
| 领投/复投 | **YZi Labs**（原 Binance Labs 分拆的家族办公室） |
| 跟投 | **Susquehanna Crypto**（SIG 加密部门） |
| 公开站台 | **CZ（赵长鹏）** 推特预告 |
| 创始人 | **Dingaling** — 前 Binance 研究负责人、PancakeSwap 联合创始人 |
| 渠道合作 | **Binance Wallet**（200M+ 用户原生集成） |

### 5.2 战略并购：Probable

| 事件 | 意义 |
|------|------|
| 2026-03 收购 Probable | Probable 由 **PancakeSwap + YZi Labs 共同孵化**，同源资本/同链/同期上线；收购本质是 YZi 体系内部资源整合 |
| 岳小鱼（@yuexiaoyu）任亚太负责人 | 接入中文社区与收入机制 |
| 积分迁移 | Probable Points → Predict Points（第 1–6 周 1:1，第 7–10 周 10:1） |

---

> 数据截至 2026 年 6 月，基于公开信息整理。交易量等数据可能因统计口径不同而有所差异。不构成投资建议。
