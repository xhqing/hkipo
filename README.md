# HKIPO Strategy

A scientific, data-driven strategy for Hong Kong IPO subscription, optimized for the post-2025 HKEX new regulations era.

[中文文档](README_cn.md)

---

## Background

On August 4, 2025, the HKEX IPO new regulations took effect. Approximately 87% of new listings adopted Mechanism B (no clawback, public offering fixed at 10%), causing the median one-lot allocation rate to plummet from ~50% to 1%-2%. The HK IPO market has shifted from a "blind subscription bonus era" to a **"selective + disciplined + multi-account coordination"** era.

This project provides a systematic, quantitative strategy framework to navigate this new environment.

---

## Strategy Overview

The strategy is organized into six stages:

| Stage | Focus | Key Question |
|-------|-------|-------------|
| 1. Entry Screening | Quantitative scoring & veto rules | Should I subscribe? |
| 2. Clawback & Allocation Analysis | Mechanism A vs B, allocation rate dynamics | How does the mechanism affect my odds? |
| 3. Capital & Subscription Tactics | Multi-account, Group A tail, Group B head | How much should I subscribe? |
| 4. Selling Discipline | Grey market & first-day rules | When should I sell? |
| 5. Sector Prioritization | Industry performance ranking | Which sectors to favor? |
| 6. Risk Management | Capital limits, psychological discipline | How to protect my capital? |

---

## Key Highlights

### Quantitative Scoring System (7 Dimensions)

Each IPO is scored across 7 weighted dimensions (cornerstone investors, subscription heat, placement multiplier, sector, sponsor/stabilizer, valuation, share transfer). **Score ≥ 7: subscribe; < 5: skip; 5-7: light position.**

### Automatic Veto Items

Any single veto condition triggers an automatic pass: forced clawback, no path to profitability, fake cornerstones, pricing >15% above range cap, or sponsor with >50% historical break rate.

### Post-Reform Key Insight: Group A Tail Outperforms Group B Head

Under Mechanism B, investors crowd into Group B, making **Group A tail allocation rates higher than Group B head** in most cases — a complete reversal from the pre-reform era.

### Multi-Account Strategy

With one-lot rates at 1-2%, the most effective approach for small capital is **multiple accounts each subscribing one lot** (using family members' identities), yielding 5-8x the allocation rate of a single account.

### Strict Selling Discipline

- Grey market up >20%: sell all immediately
- Grey market up 0-5%: sell all (micro-gains often reverse on listing day)
- Any break below IPO price: market sell without hesitation
- First-day pullback >5% from peak: sell immediately

---

## Project Structure

```
hkipo/
├── hkipo_strategy.md    # Full strategy document (Chinese)
├── LICENSE              # GNU AGPL v3
└── README.md            # This file
```

---

## Data Foundation

The strategy is built on real market data from 2021-2025, including:

- HKEX IPO new regulation impact analysis (Mechanism A vs B adoption rates)
- Allocation rate statistics across Group A/B tiers
- Clawback ratio vs break rate correlation (418 cases, 2020-2024)
- Grey market vs first-day performance correlation (76% positive correlation)
- Cornerstone investor proportion vs first-day performance ("golden zone" at 25-40%)
- Subscription multiplier "bimodal curve" (100-200x is the danger zone)
- Sector performance rankings with representative cases

---

## Disclaimer

This project is for **educational and informational purposes only**. It does not constitute financial advice, investment recommendations, or solicitation to buy or sell any securities. All investment decisions involve risk, and past performance does not guarantee future results. Always conduct your own due diligence and consult a qualified financial advisor before making investment decisions.

---

## License

This project is licensed under the [GNU Affero General Public License v3.0](LICENSE).
