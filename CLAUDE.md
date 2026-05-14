# CLAUDE.md

## Project Overview

HKIPO is a data-driven strategy framework for Hong Kong IPO subscription, optimized for the post-2025 HKEX new regulations era. The project is documentation-centric, providing systematic quantitative analysis and decision-making rules for HK IPO investors.

## Project Structure

```
hkipo/
├── CLAUDE.md              # This file - AI assistant context
├── README.md              # English project overview
├── README_cn.md           # Chinese project overview
├── hkipo_strategy.md      # Full strategy document (Chinese, primary)
├── LICENSE                # GNU AGPL v3
├── .gitignore
└── .trae/
    ├── mcp.json.example   # MCP server configuration template
    └── rules/             # Tool calling rules
```

## Language

- Primary language: **Chinese (简体中文)**
- README files are bilingual (Chinese + English)
- Strategy document (`hkipo_strategy.md`) is written in Chinese
- Code comments should follow Chinese unless otherwise specified

## Domain Knowledge

### Key Concepts

- **机制A (Mechanism A)**: ~13% of IPOs; public offering ratio scales 5%-35% based on subscription multiplier; has clawback
- **机制B (Mechanism B)**: ~87% of IPOs; public offering fixed at ~10%; no clawback; this is the dominant mechanism post-reform
- **甲组 (Group A)**: Public subscription tier for smaller applications
- **乙组 (Group B)**: Public subscription tier for larger applications
- **甲尾 (Group A Tail)**: Top end of Group A subscription — outperforms Group B head under Mechanism B
- **乙头 (Group B Head)**: Bottom end of Group B subscription
- **回拨 (Clawback)**: Reallocating shares from institutional to public tranche
- **暗盘 (Grey Market)**: Pre-listing trading session (T-1, 16:15-18:30)
- **绿鞋 (Green Shoe)**: Over-allotment option
- **基石投资者 (Cornerstone Investors)**: Pre-IPO anchor investors
- **国配 (Placement)**: Institutional placement tranche
- **孖展 (Margin Financing)**: Leveraged subscription financing
- **顶头槌 (Maximum Subscription)**: Subscribing at the maximum allowed amount

### Scoring System

7-dimension weighted scoring for IPO entry decisions:
- Score ≥ 7: Subscribe
- Score 5-7: Light position
- Score < 5: Skip

Dimensions: Cornerstone investors (20%), Subscription heat (20%), Placement multiplier (15%), Sector (15%), Sponsor/Stabilizer (15%), Valuation (10%), Share transfer (5%)

### Veto Items (一票否决)

Any single veto condition triggers automatic pass: forced clawback, no path to profitability, fake cornerstones, pricing >15% above range cap, sponsor with >50% historical break rate.

## MCP Tools Available

The project is configured with financial data MCP servers (see `.trae/mcp.json.example`):

- **market-data-fetcher**: Longport-based market data (requires API keys)
- **financekit**: Financial data toolkit
- **china-stock-mcp**: A-share market data
- **mcp-aktools**: AKTools data access
- **financemcp-dcths**: Tonghuashun (同花顺) financial data
- **akshare-one-mcp**: AKShare data via HTTP
- **发现报告**: Research report discovery
- **tushareMcp**: Tushare financial data
- **Time**: Timezone-aware time server (Asia/Shanghai)

When fetching HK real-time market data, prefer market-data-fetcher (Longport) or financekit; for A-share data use china-stock-mcp or mcp-aktools; for sector/industry data use financemcp-dcths.

## Conventions

- This is a strategy documentation project; code additions should be minimal and purposeful
- All financial data references should cite the time period (e.g., "2021-2025 data")
- Maintain the distinction between pre-reform and post-reform (2025-08-04) market conditions
- Quantitative claims must be backed by historical data
- Risk disclaimers are mandatory for any investment-related content

## License

GNU Affero General Public License v3.0 (AGPL-3.0). Any derivative work must retain this license and provide source code access.
