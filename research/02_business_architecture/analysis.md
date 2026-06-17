# Predict.fun — 业务架构分析

> 数据日期：2026-06-17
> 平台：predict.fun

---

## 1. 业务全景架构

```mermaid
graph TD
    U[用户/交易者] --> ENT{接入入口}
    ENT --> W[predict.fun Web/App]
    ENT --> BW[Binance Wallet 集成入口]
    ENT --> API[开发者 API / SDK]

    W --> TRADE[交易模块]
    BW --> TRADE
    API --> TRADE

    TRADE --> M1[市场浏览/分类/搜索]
    TRADE --> M2[YES/NO 下单 - CLOB]
    TRADE --> M3[持仓与盈亏]

    TRADE --> YIELD[收益模块 Yield-Bearing]
    YIELD --> Y1[抵押品包装为生息资产]
    Y1 --> Y2[路由 BNB Chain DeFi 策略]
    Y2 --> Y3[持仓期间赚取 APY]

    TRADE --> SETTLE[结算模块]
    SETTLE --> S1[UMA 兼容乐观预言机]
    S1 --> S2[YES/NO 兑付 1 美元/0]

    W --> GROW[增长模块]
    BW --> GROW
    GROW --> G1[Predict Points 积分]
    GROW --> G2[邀请返佣 10%]
    GROW --> G3[赛事活动 如世界杯]
```

---

## 2. 核心业务模块

| 模块 | 描述 | 战略价值 |
|------|------|----------|
| **交易模块** | 二元 YES/NO 市场，链下 CLOB 撮合 + 链上结算 | 平台核心，手续费来源 |
| **收益模块（Yield-Bearing）** | 抵押资金包装为生息资产，路由 DeFi 赚取收益 | 最大差异化护城河 |
| **结算模块** | UMA 兼容乐观预言机裁决事件结果 | 去信任化结果，平台公信力 |
| **增长模块** | Predict Points 积分 + 邀请 + 赛事活动 | 用户获取与留存飞轮 |
| **渠道集成模块** | Binance Wallet Gasless 集成、API/SDK 开放 | 流量入口 + 生态扩张 |

---

## 3. 业务价值链

```mermaid
flowchart LR
    A[用户存入 USDT] --> B[资金进入生息抵押池]
    B --> C[挂单/吃单 交易 YES/NO]
    C --> D[平台收取手续费 ~2%]
    B --> E[抵押期间产生 DeFi 收益]
    C --> F[事件结束 UMA 预言机裁决]
    F --> G[赢家兑付 $1/share 输家归零]
    D --> H[平台收入]
    E --> I[收益归用户/平台分成 待确认]
    C --> J[累积 Predict Points]
    J --> K[空投预期 拉新留存]
```

### 业务闭环说明

1. **入金即生息**：用户存入 USDT 后，即便尚未下注或挂单，资金也可进入生息抵押层（这是与 Polymarket「闲置抵押」的关键差异）。
2. **交易产生手续费**：链下订单簿撮合，平台按概率加权费率（约 2% 基础、随价格偏离 50% 递减）抽成。
3. **结算去信任化**：事件结束后由 UMA 兼容乐观预言机提交并裁决结果，赢家份额兑付 $1，输家归零。
4. **积分预埋增长**：交易/做市/持仓/邀请全程累积 Predict Points，绑定空投预期形成拉新留存飞轮。

---

## 4. 双边市场结构

```mermaid
graph LR
    subgraph 供给侧
        MM[做市商/流动性提供者]
        MM --> LP[双边挂单 YES+NO]
        LP --> PP1[赚取做市 Predict Points]
    end

    subgraph 需求侧
        T[方向性交易者]
        T --> BET[买入 YES 或 NO]
    end

    LP --> OB[(链下订单簿 CLOB)]
    BET --> OB
    OB --> MATCH[撮合引擎]
    MATCH --> CHAIN[BNB Chain 链上结算]
```

predict.fun 是典型的双边市场：
- **供给侧（做市商/LP）**：提供流动性、收窄价差，靠做市积分（每分钟订单簿快照计分）获得激励。
- **需求侧（交易者）**：方向性押注，贡献手续费与交易量。
- 平台通过 **积分激励供给侧** 来解决冷启动的流动性问题——这是预测市场最难的部分。

---

## 5. 小结

predict.fun 的业务架构在标准预测市场（交易 + 结算）之上，叠加了 **收益模块（差异化护城河）** 与 **增长模块（积分飞轮）** 两个引擎，并通过 **Binance Wallet 集成** 打通最大流量入口。其业务设计的核心逻辑是：用「生息抵押」降低持仓成本吸引资金、用「积分空投预期」激励做市与拉新、用「Binance 渠道 + 大事件」做规模化获客。
