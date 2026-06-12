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

**使用本仓库即表示您已阅读、理解并同意以下全部条款。如不同意，请勿使用本仓库的任何内容。**

### 1. 用途限定

- 本仓库数据**仅为量化学习、学术研究与技术演示目的提供的小规模样本数据**（每市场仅 10 只股票），不构成完整数据集，不具备生产可用性。
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

1. **Limited purpose.** This repository provides a small sample dataset (10 stocks per market) **solely for quantitative learning, academic research, and technical demonstration**. It is not a complete dataset, not production-ready, and not a data service. Content may be modified or removed at any time without notice. **Any commercial use is strictly prohibited**, including resale, redistribution, integration into commercial products or services, commercial data APIs, or commercial model training.
2. **No investment advice.** Nothing in this repository constitutes investment, financial, trading, or any other professional advice, nor an offer or solicitation to buy or sell any security. Past performance is not indicative of future results. **Any decision made based on this repository is solely at the user's own risk.**
3. **No warranty.** All data is provided **"AS IS" without warranty of any kind**, express or implied, including accuracy, completeness, timeliness, merchantability, or fitness for a particular purpose. Errors, omissions, and delays may exist. Do not use for actual trading.
4. **Limitation of liability.** To the maximum extent permitted by applicable law, the author shall **not be liable for any direct, indirect, incidental, special, punitive, or consequential damages** (including investment losses, loss of profits, loss of data, or business interruption) arising from the use of, or inability to use, this repository. Users are solely responsible for ensuring their use complies with applicable laws and any third-party agreements.
5. **Intellectual property & takedown.** Rights in the underlying market data belong to the respective exchanges and data providers. This repository quotes a small sample for research purposes only, with no intent to infringe. **If you believe any content infringes your rights, please open a GitHub Issue with proof of ownership, and the content will be removed promptly upon verification.**
