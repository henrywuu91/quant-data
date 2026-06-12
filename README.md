# quant-data

股票量化基础数据样本 - A股 / 港股 / 美股

## 数据说明

仅供量化学习与研究使用的样本数据集，覆盖三个市场、每市场 10 只股票：

```
stock_data/
├── cn/   # A股样本（10 只）
├── hk/   # 港股样本（10 只）
└── us/   # 美股样本（10 只）
```

每只股票包含 4 个 CSV 文件：

| 文件 | 内容 |
|------|------|
| `*_kline_daily_raw.csv` | 日线行情（开高低收、成交量、成交额） |
| `*_kline_daily_ext.csv` | 日线扩展（市值、复权因子、换手率） |
| `*_finance_raw.csv` | 季度财务报表数据 |
| `*_finance_ext.csv` | 财务衍生指标（利润率、ROE、TTM、同比等） |

数据区间：约 2016 年至今（日线）；财务数据为季度频率。

## Disclaimer / 免责声明

- 本仓库数据**仅为量化学习与研究目的提供的小规模样本数据**（每市场仅 10 只股票），不构成完整数据集，不提供持续数据服务。
- 数据整理自公开市场信息，**不保证数据的准确性、完整性和及时性**，请勿用于实际交易决策。
- 本仓库内容**不构成任何投资建议**，据此操作风险自负。
- **禁止将本仓库数据用于任何商业用途**（包括但不限于转售、商业再分发、商业数据服务）。
- 如认为本仓库内容侵犯了您的权益，请通过 Issue 联系，我们将及时处理删除。

- This repository provides a **small sample dataset for quantitative research and educational purposes only** (10 stocks per market). It is not a complete dataset and offers no ongoing data service.
- Data is compiled from publicly available market information. **No guarantee of accuracy, completeness, or timeliness.** Do not use for actual trading decisions.
- Nothing in this repository constitutes investment advice.
- **Commercial use of this data is prohibited**, including resale, redistribution, or commercial data services.
- If you believe any content infringes your rights, please open an Issue and it will be removed promptly.
