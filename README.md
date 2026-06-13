# quant-data

股票量化基础数据样本 - A股 / 港股 / 美股

## 数据说明

仅供量化学习与研究使用的样本数据集，覆盖三个市场、每市场 50 只股票（按市值与流动性选取的代表性研究样本，非全市场覆盖）：

```
stock_data/
├── cn/   # A股样本（50 只）
├── hk/   # 港股样本（50 只）
└── us/   # 美股样本（50 只）
```

每只股票包含 4 个 CSV 文件：

| 文件 | 内容 |
|------|------|
| `*_kline_daily_raw.csv` | 日线行情（开高低收、成交量、成交额） |
| `*_kline_daily_ext.csv` | 日线扩展（市值、复权因子、换手率） |
| `*_finance_raw.csv` | 季度财务报表数据 |
| `*_finance_ext.csv` | 财务衍生指标（利润率、ROE、TTM、同比等） |

数据区间：约 2016 年至今（日线）；财务数据为季度频率。

## 样本股票清单

> 以下为当前快照所含样本（每市场 50 只，按市值与流动性选取的代表性研究样本），清单可能随后续更新而调整。

### A股（cn，50 只）

```
000063 000636 000657 000725 000988 001309 002156 002281 002371 002384
002407 002409 002428 002463 002475 300136 300274 300285 300308 300346
300394 300433 300475 300476 300502 300604 300666 300750 301308 600176
600183 600487 600498 600522 600549 600584 601138 601899 603986 603993
688008 688012 688041 688072 688126 688146 688256 688498 688525 688981
```

### 港股（hk，50 只）

```
00020 00100 00148 00175 00522 00568 00700 00763 00857 00883
00941 00981 00992 01024 01109 01211 01347 01378 01772 01801
01810 01888 02259 02269 02359 02382 02476 02513 02577 02899
03690 03750 03888 03986 06160 06166 06613 06651 06809 06869
09618 09660 09868 09880 09888 09903 09926 09988 09992 09999
```

### 美股（us，50 只）

```
AAL  AAOI AAPL ADBE AMAT AMD  AMZN APP  ASTS AVGO
BE   CAT  COHR CRDO CRM  CRWD CRWV CSCO DELL GEV
GOOG GOOGL IBM INTC IREN KLAC LITE LLY  LRCX META
MRVL MSFT MU   NBIS NFLX NOW  NVDA ORCL PANW PLTR
QCOM RKLB SMCI SNDK STX  TSLA TXN  WDC  WMT  XOM
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
| open / high / low / close | 开盘 / 最高 / 最低 / 收盘价（未复权，计价货币） |
| volume | 成交量（股） |
| amount | 成交额（计价货币） |

### 日线扩展 `*_kline_daily_ext.csv`（三市场通用）

| 字段 | 说明 |
|------|------|
| country / code / time | 同上 |
| total_shares | 总股本（亿股） |
| float_shares | 流通股本（亿股） |
| total_market_cap | 总市值（亿，计价货币） |
| float_market_cap | 流通市值（亿，计价货币） |
| adj_factor | 复权因子（以最新交易日为基准 1.0） |
| turnover_rate | 换手率（小数） |

### 财务表公共字段（所有 `*_finance_*.csv`）

| 字段 | 说明 |
|------|------|
| country / code | 市场 / 股票代码 |
| symbol | 股票标识 |
| fiscal_year | 财年 |
| period | 报告期（Q1–Q4） |
| report_date | 报告期截止日 |
| reported_currency | 报告币种（raw 表） |
| release_date | 财报发布日（ext 表） |

### A股财务报表 `stock_data/cn/*_finance_raw.csv`

利润表：

| 字段 | 说明 |
|------|------|
| revenue | 营业总收入 |
| total_operating_cost | 营业总成本 |
| cost_of_revenue | 营业成本 |
| taxes_and_surcharges | 税金及附加 |
| selling_expense / admin_expense / finance_expense | 销售 / 管理 / 财务费用 |
| operating_profit | 营业利润 |
| non_operating_income / non_operating_expense | 营业外收入 / 支出 |
| income_tax | 所得税费用 |
| net_income_attr_parent | 归母净利润 |

资产负债表：

| 字段 | 说明 |
|------|------|
| total_shares | 总股本 |
| capital_reserve / surplus_reserve / retained_earnings | 资本公积 / 盈余公积 / 未分配利润 |
| cash_equivalents | 货币资金 |
| accounts_receivable / other_receivables / receivables_and_notes | 应收账款 / 其他应收款 / 应收票据及应收账款 |
| prepayments | 预付款项 |
| inventories | 存货 |
| current_assets / non_current_assets | 流动 / 非流动资产 |
| fixed_assets / fixed_assets_total | 固定资产 / 固定资产合计 |
| intangible_assets | 无形资产 |
| deferred_tax_assets | 递延所得税资产 |
| accounts_payable / other_payables / notes_and_accounts_payable | 应付账款 / 其他应付款 / 应付票据及应付账款 |
| payroll_payable | 应付职工薪酬 |
| taxes_payable | 应交税费 |
| current_liabilities / non_current_liabilities | 流动 / 非流动负债 |
| equity_attr_parent / total_equity | 归母股东权益 / 股东权益合计 |

现金流量表：

| 字段 | 说明 |
|------|------|
| cash_from_sales | 销售商品、提供劳务收到的现金 |
| cash_from_other_operating | 收到其他与经营活动有关的现金 |
| cash_paid_goods | 购买商品、接受劳务支付的现金 |
| cash_paid_employees | 支付给职工以及为职工支付的现金 |
| cash_paid_taxes | 支付的各项税费 |
| cash_paid_other_operating | 支付其他与经营活动有关的现金 |
| operating_cash_flow / investing_cash_flow / financing_cash_flow | 经营 / 投资 / 筹资活动现金流净额 |
| capital_expenditure | 资本开支 |
| net_change_in_cash | 现金及等价物净增加额 |
| cash_end_period | 期末现金余额 |

### 港股财务报表 `stock_data/hk/*_finance_raw.csv`

| 字段 | 说明 |
|------|------|
| revenue | 营业收入 |
| gross_profit | 毛利 |
| operating_profit | 经营溢利 |
| pretax_income | 税前利润 |
| net_income | 净利润 |
| admin_expense | 行政开支 |
| other_income | 其他收入 |
| interest_expense | 利息支出 |
| income_tax | 所得税 |
| comprehensive_income | 综合收益总额 |
| basic_eps | 基本每股收益 |
| operating_cash_flow / investing_cash_flow / financing_cash_flow | 经营 / 投资 / 筹资活动现金流净额 |
| cash_equivalents | 现金及现金等价物 |
| total_assets / net_assets | 总资产 / 净资产 |
| current_assets / fixed_assets | 流动资产 / 固定资产 |
| total_liabilities / current_liabilities | 总负债 / 流动负债 |
| share_capital | 股本 |

### 美股财务报表 `stock_data/us/*_finance_raw.csv`

| 字段 | 说明 |
|------|------|
| revenue | 营业收入 |
| cost_of_revenue | 营业成本 |
| sga_expense | 销售及管理费用（SG&A） |
| operating_expense | 营业费用 |
| ebit | 息税前利润（EBIT） |
| depreciation_amortization | 折旧与摊销 |
| net_interest_income | 净利息收入 |
| pretax_income | 税前利润 |
| net_income | 净利润 |
| shares_basic / shares_diluted | 基本 / 稀释加权股数 |
| cash_equivalents / short_term_investments | 现金及等价物 / 短期投资 |
| current_assets / non_current_assets | 流动 / 非流动资产 |
| ppe_net | 固定资产净值（PP&E, Net） |
| current_liabilities / non_current_liabilities | 流动 / 非流动负债 |
| common_stock | 普通股股本 |
| retained_earnings | 留存收益 |
| shareholders_equity | 股东权益 |
| working_capital_change / other_working_capital | 营运资本变动 / 其他营运资本 |
| other_non_cash_items | 其他非现金项目 |
| operating_cash_flow / investing_cash_flow / financing_cash_flow | 经营 / 投资 / 筹资活动现金流净额 |
| net_change_in_cash | 现金净变动 |
| cash_begin_period | 期初现金余额 |
| capital_expenditure | 资本开支 |

### 财务衍生指标 `*_finance_ext.csv`

| 字段 | 说明 | 适用市场 |
|------|------|----------|
| gross_margin | 毛利率 | 全部 |
| operating_margin | 营业利润率 | 全部 |
| net_margin | 净利率 | 全部 |
| roe / roa | 净资产收益率 / 总资产收益率 | 全部 |
| current_ratio | 流动比率 | 全部 |
| debt_to_equity | 产权比率（负债/权益） | 全部 |
| debt_to_assets | 资产负债率 | 全部 |
| ocf_to_revenue | 经营现金流 / 营收 | 全部 |
| fcf_margin | 自由现金流利润率 | CN / US |
| accrual_ratio | 应计比率 | 全部 |
| revenue_yoy / revenue_qoq | 营收同比 / 环比 | 全部 |
| net_income_yoy / net_income_qoq | 净利润同比 / 环比 | 全部 |
| eps_yoy | EPS 同比 | CN / US |
| revenue_ttm / net_income_ttm | 营收 / 净利润 TTM（滚动 12 个月） | 全部 |
| eps_ttm | EPS TTM | CN / US |
| net_margin_ttm / roe_ttm | 净利率 / ROE TTM | 全部 |
| revenue_ttm_yoy / net_income_ttm_yoy | 营收 / 净利润 TTM 同比 | 全部 |
| eps_basic | 基本每股收益 | CN / US |
| eps_surprise / eps_surprise_pct | EPS 超预期值 / 超预期幅度 | 仅 US |

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
