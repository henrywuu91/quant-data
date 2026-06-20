# quant-data

股票量化基础数据 · A股 / 港股 / 美股

**CN / HK / US stock market dataset** — daily OHLCV (K-line) + quarterly financial statements, for quantitative research and backtesting.

## 数据说明

仅供量化学习与研究使用的样本数据集，覆盖三个市场、每市场 50 只股票（按最新交易日成交额选取的代表性研究样本，非全市场覆盖）：

```
stock/
├── cn/   # A股样本（50 只）
├── hk/   # 港股样本（50 只）
└── us/   # 美股样本（50 只）
```

每只股票包含 4 个 CSV 文件（`*_raw` 为原始数据，`*_ext` 为基于原始数据派生的扩展指标）：

| 文件 | 内容 |
|------|------|
| `*_kline_daily_raw.csv` | 日线行情（未复权/后复权开高低收、成交量额、复权因子、股本与市值、换手率） |
| `*_kline_daily_ext.csv` | 日线扩展指标（15 个常用公开技术指标：均线、MACD、RSI、布林带、ATR 等） |
| `*_finance_raw.csv` | 季度财务报表数据 |
| `*_finance_ext.csv` | 财务扩展指标（15 个常用公开财务比率：利润率、ROE/ROA、偿债与周转、现金流质量、同比增速等） |

数据区间：约 2016 年至今（日线）；财务数据为季度频率。

## 样本股票清单

> 以下为当前快照所含样本（每市场 50 只，按最新交易日成交额选取的代表性研究样本），清单可能随后续更新而调整。

### A股（cn，50 只）

```
000021 000032 000063 000066 000100 000333 000338 000426 000630 000636
000657 000725 000733 000792 000807 000831 000938 000960 000977 000988
001696 001896 002008 002028 002049 002050 002056 002080 002119 002129
002138 002149 002156 002171 002179 002185 002192 002202 002222 002230
002240 002245 002273 002297 002353 002354 002585 002625 002741 002747
```

### 港股（hk，50 只）

```
00001 00002 00003 00005 00006 00148 00168 00175 00179 00189
00241 00267 00268 00285 00288 00291 00293 00300 00316 00322
00358 00386 00388 00390 00425 00522 00585 00669 00780 00788
00883 00902 01093 01108 01109 01113 01114 01138 01208 01209
01211 01357 01359 01378 01384 01385 01658 01729 01766 01772
```

### 美股（us，50 只）

```
AAPL ACN ADI ALAB AMAT AMD AMZN APP AVGO BE
BRK_B C CAT CRM CRWV CSCO DELL FLEX GEV GLW
GOOG GOOGL GS HOOD INTC JNJ JPM KLAC LITE LLY
LRCX META MRVL MSFT MU NBIS NFLX NVDA ORCL PLTR
QCOM RKLB SNDK SPCX STX TER TSLA TXN UNH V
```

## 字段说明

> 金额类字段单位：行情/财务原始金额为**计价货币的元**；股本与市值字段单位为**亿**。
> 比率类字段（利润率、ROE、换手率等）均为**小数**（0.15 = 15%）。

### 日线行情 `*_kline_daily_raw.csv`（三市场通用）

| 字段 | 说明 |
|------|------|
| country | 市场（CN / HK / US） |
| code | 股票代码 |
| time | 交易日（YYYY-MM-DD） |
| raw_open / raw_high / raw_low / raw_close | 未复权 开 / 高 / 低 / 收（计价货币） |
| adj_open / adj_high / adj_low / adj_close | 后复权 开 / 高 / 低 / 收（计价货币） |
| volume | 成交量（股） |
| amount | 成交额（计价货币） |
| adj_factor | 复权因子（以最新交易日为基准 1.0） |
| total_shares / float_shares | 总股本 / 流通股本（亿股） |
| total_market_cap / float_market_cap | 总市值 / 流通市值（亿，计价货币） |
| turnover_rate | 换手率（小数） |

### 财务报表 `*_finance_raw.csv`（三市场统一表，字段口径已对齐）

> 三市场财报统一存于一张表，列结构完全一致，按 `country` 区分市场；金额为对应计价货币原值。

公共字段：

| 字段 | 说明 |
|------|------|
| code / name / country | 股票代码 / 名称 / 市场（CN / HK / US） |
| currency | 报告币种 |
| report_type | 报告期类型（Q1–Q4） |
| report_date | 报告期截止日 |
| filing_date | 财报发布日 |

利润表：

| 字段 | 说明 |
|------|------|
| revenue | 营业收入 |
| gross_profit | 毛利 |
| operating_profit | 营业利润 |
| income_before_tax | 税前利润 |
| income_tax_expense | 所得税费用 |
| net_income | 净利润 |
| net_income_parent | 归母净利润 |
| basic_eps | 基本每股收益 |

资产负债表：

| 字段 | 说明 |
|------|------|
| assets_total / assets_current / assets_non_current | 总资产 / 流动资产 / 非流动资产 |
| cash_and_cash_equivalents | 现金及现金等价物 |
| accounts_receivable | 应收账款 |
| property_plant_equipment_net | 固定资产净值（PP&E, Net） |
| liabilities_total / liabilities_current / liabilities_non_current | 总负债 / 流动负债 / 非流动负债 |
| accounts_payable | 应付账款 |
| equity_total / equity_parent | 股东权益合计 / 归母股东权益 |

现金流量表：

| 字段 | 说明 |
|------|------|
| operating_cash_flow / investing_cash_flow / financing_cash_flow | 经营 / 投资 / 筹资活动现金流净额 |
| capital_expenditure | 资本开支 |

### 日线扩展指标 `*_kline_daily_ext.csv`（基于后复权价派生）

> 均为基于 `*_kline_daily_raw.csv` 计算的常用公开技术指标；价格优先取后复权价（`adj_*`），缺失时回退到未复权价（`raw_*`）。前若干行因窗口不足为空值。

| 字段 | 说明 |
|------|------|
| country / code / time | 市场 / 股票代码 / 交易日（与 raw 对齐） |
| pct_chg | 日涨跌幅（%） |
| ma5 / ma10 / ma20 / ma60 | 5 / 10 / 20 / 60 日简单移动平均 |
| ema12 / ema26 | 12 / 26 日指数移动平均 |
| macd | DIF = EMA12 − EMA26 |
| macd_signal | DEA = DIF 的 9 日 EMA |
| macd_hist | MACD 柱 = (DIF − DEA) × 2 |
| rsi14 | 14 日相对强弱指标（Wilder 平滑） |
| boll_upper / boll_lower | 布林带上 / 下轨 = MA20 ± 2 × 20 日总体标准差 |
| atr14 | 14 日平均真实波幅（Wilder 平滑） |
| vol_ma5 | 5 日平均成交量 |

### 财务扩展指标 `*_finance_ext.csv`（基于财报派生）

> 均为基于 `*_finance_raw.csv` 计算的常用公开财务比率；净利润优先取归母（`net_income_parent`），权益优先取归母（`equity_parent`）；分母为空或为 0 时记空值。比率为小数（0.15 = 15%）。

| 字段 | 说明 |
|------|------|
| country / code | 市场 / 股票代码 |
| report_type / report_date / filing_date | 报告期类型 / 报告期截止日 / 财报发布日（与 raw 对齐） |
| gross_margin / operating_margin / net_margin | 毛利率 / 营业利润率 / 净利率 |
| roe / roa | 净资产收益率 / 总资产收益率 |
| current_ratio | 流动比率（流动资产 / 流动负债） |
| debt_to_assets / debt_to_equity | 资产负债率 / 产权比率 |
| asset_turnover | 总资产周转率（营收 / 总资产） |
| equity_multiplier | 权益乘数（总资产 / 权益） |
| ocf_to_revenue / ocf_to_net_income | 经营现金流 / 营收、经营现金流 / 净利润（盈余质量） |
| fcf_margin | 自由现金流利润率（(经营现金流 − 资本开支) / 营收） |
| revenue_yoy / net_income_yoy | 营收 / 归母净利润同比（对上年同期，同 report_type） |

## Disclaimer / 免责声明

**使用本仓库即表示您已阅读、理解并同意以下全部条款。如不同意，请勿使用本仓库的任何内容。**

### 1. 用途限定

- 本仓库数据**仅为量化学习、学术研究与技术演示目的提供的样本数据**（每市场 50 只代表性股票，非全市场覆盖），不构成完整数据集，不具备生产可用性。
- 本仓库**不是数据服务**：不承诺数据更新频率，不承诺数据持续可用，仓库内容可能随时修改或删除，恕不另行通知。
- **严禁将本仓库数据用于任何商业用途**，包括但不限于：转售、商业再分发、集成至商业产品或服务、提供商业数据接口、用于商业模型训练等。

### 2. 非投资建议

- 本仓库的任何内容（包括数据、文档、代码、衍生指标）**均不构成投资建议、财务建议、交易建议或任何其他形式的专业建议**，亦不构成对任何证券的买卖要约或要约邀请。
- 历史数据不代表未来表现。任何人基于本仓库内容做出的任何投资决策及其产生的一切后果，**均由使用者自行承担，与本仓库作者无关**。

### 3. 数据质量免责

- 数据整理自公开市场信息，**按"现状"（AS IS）提供，不附带任何明示或默示的保证**，包括但不限于对准确性、完整性、及时性、连续性、适销性及特定用途适用性的保证。
- 数据可能存在错误、缺失、延迟或偏差（包括但不限于复权处理、币种换算、财务科目映射等环节的误差），**请勿将其用于实际交易或任何对数据准确性有要求的场景**。

### 4. 责任限制

- 在适用法律允许的最大范围内，本仓库作者**不对因使用或无法使用本仓库内容而导致的任何直接、间接、偶然、特殊、惩罚性或后果性损失承担责任**（包括但不限于投资损失、利润损失、数据丢失、业务中断），即使已被告知该等损失的可能性。
- 使用者应自行确保其对本仓库内容的使用符合其所在司法管辖区的法律法规及其与任何第三方（包括数据服务商、交易所）之间的协议。**因使用者违规使用而产生的一切责任由使用者自行承担。**

### 5. 知识产权与侵权处理

- 证券行情等原始数据的相关权利归属于相应交易所及数据提供方。本仓库仅以学习研究为目的少量引用整理，**无意侵犯任何权利人的合法权益**。
- 如您认为本仓库内容侵犯了您的合法权益，请通过 GitHub Issue 联系并附权属说明，**我们将在核实后及时删除相关内容**。

---

### Disclaimer (English)

**By using this repository, you acknowledge that you have read, understood, and agreed to all terms below. If you do not agree, do not use any content of this repository.**

1. **Limited purpose.** This repository provides a sample dataset (50 representative stocks per market, not full-market coverage) **solely for quantitative learning, academic research, and technical demonstration**. It is not a complete dataset, not production-ready, and not a data service. Content may be modified or removed at any time without notice. **Any commercial use is strictly prohibited**, including resale, redistribution, integration into commercial products or services, commercial data APIs, or commercial model training.
2. **No investment advice.** Nothing in this repository constitutes investment, financial, trading, or any other professional advice, nor an offer or solicitation to buy or sell any security. Past performance is not indicative of future results. **Any decision made based on this repository is solely at the user's own risk.**
3. **No warranty.** All data is provided **"AS IS" without warranty of any kind**, express or implied, including accuracy, completeness, timeliness, merchantability, or fitness for a particular purpose. Errors, omissions, and delays may exist. Do not use for actual trading.
4. **Limitation of liability.** To the maximum extent permitted by applicable law, the author shall **not be liable for any direct, indirect, incidental, special, punitive, or consequential damages** (including investment losses, loss of profits, loss of data, or business interruption) arising from the use of, or inability to use, this repository. Users are solely responsible for ensuring their use complies with applicable laws and any third-party agreements.
5. **Intellectual property & takedown.** Rights in the underlying market data belong to the respective exchanges and data providers. This repository quotes a small sample for research purposes only, with no intent to infringe. **If you believe any content infringes your rights, please open a GitHub Issue with proof of ownership, and the content will be removed promptly upon verification.**

## License

**Non-commercial research use only.**

本仓库数据仅授权用于非商业性的学习与研究用途。任何商业用途均不被授权，详见上文 Disclaimer。
The data in this repository is licensed for non-commercial research and educational use only. No commercial use is permitted. See the Disclaimer above for details.

## Keywords / 关键词

quant · quantitative-finance · stock-market · stock-data · financial-data · dataset · OHLCV · K-line · A-shares · Hong-Kong-stocks · US-stocks · financial-statements · fundamentals · algorithmic-trading · backtesting · 量化投资 · 股票数据 · 行情数据 · 财务数据 · A股 · 港股 · 美股
