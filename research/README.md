# Predict.fun 深度调研项目

> 调研日期：2026-06-17
> 数据来源：predict.fun 官网与开发者文档、BNB Chain 链上合约、YZi Labs/Binance 公告、加密媒体报道
> 调研对象：**predict.fun 单一平台深度剖析**

---

## 目录结构

```
research/
├── 01_predictfun/       # Predict.fun — BNB 原生预测市场 ✅ 深度完成
│   └── analysis.md      #   含 8 大标准化章节（市场/业务/UX/技术/壁垒/商业/待确认/总结）
└── summary/
    ├── overview.md      # 全景汇总报告
    ├── open_questions.md# 待确认问题清单
    └── limitations.md   # 调研局限性说明
```

> 说明：目录与 `polymarket_research` 保持一致——**每个被调研对象一个文件夹，内含单个 `analysis.md`**，所有维度作为编号章节集中在该文件内。

---

## 报告导航

| # | 平台 | 类型 | 累计交易量 | 状态 | 报告 |
|---|------|------|-----------|------|------|
| 01 | **Predict.fun** | BNB Chain 原生预测市场（生息抵押 + Binance 渠道） | $1.8B+ | ✅ 深度完成 | [查看](./01_predictfun/analysis.md) |

### `analysis.md` 标准化章节

1. **市场情况** — 定位、规模与轨迹、品类覆盖、竞争格局、融资资本、收购 Probable
2. **业务架构** — 五大模块、市场生命周期、资金流、双边市场、利益相关者
3. **用户体验路径** — 双入口对比、注册/入金/交易/持仓/结算/提现全流程 Mermaid
4. **技术架构** — 链下 CLOB + 链上 CTF + UMA 预言机 + Venus 生息合约族 + 账户抽象 + API/SDK
5. **核心功能与交易技术壁垒** — 功能详解 + 壁垒评分表 + 与 Polymarket 对照
6. **商业模式** — 费率数学、收入测算、单位经济性、商业画布、增长飞轮、代币/积分/空投
7. **待确认问题** — 明确标注推测与待验证项
8. **总结** — 核心判断

---

## 核心发现（TL;DR）

1. **生息抵押品是结构性创新**——链上独立部署的 `YieldBearing*` 合约族佐证「押注期间资金不闲置」，抵押品经 **Venus Protocol** 生息，是当前唯一对闲置抵押提供收益的主要预测市场。
2. **Binance 全家桶背书**——YZi 多次投资、CZ 站台、Binance Wallet 原生 Gasless 集成（触达 200M+ 用户）、创始人前 Binance + PancakeSwap 背景。
3. **技术是 Polymarket 的 BNB 改良分叉**——CTF + CLOB + UMA 兼容预言机同源，差异在链选、生息、账户抽象。
4. **东方野心明确**——主服务器东京、收购 Probable、岳小鱼任亚太负责人。
5. **积分驱动增长**——Predict Points + 空投预期，做市积分每分钟快照、三因子计分。
6. **大事件渠道飞轮**——世界杯 $2M 奖池 + Binance 入口，3 天 2 万 DAU。

---

## 调研方法

- **官方开发者文档（dev.predict.fun）**：API、SDK、链上合约地址、订单簿计价机制
- **链上合约核验**：CTF / Yield-Bearing / UMA Adapter / NegRisk / FeeModule 部署地址
- **多来源交叉验证**：融资、收购、交易量、用户数、Venus 生息路由
- **竞品对照**：Polymarket / UMA 官方文档印证架构

## 调研局限性

- 收益分配比例（用户/平台）未公开
- 费率细节来自第三方口径，未逐项官方核验
- 交易量/用户数为不同时间点快照
- 尚未发币，代币经济为推断
- 全流程未经亲手登录实测

详见 [summary/limitations.md](./summary/limitations.md)
