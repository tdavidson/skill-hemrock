# Unit Economics Tool

> Append to the universal primer when working on the Hemrock Unit Economics Tool.

I am working on the Hemrock Unit Economics Tool, a self-contained calculator for CAC, LTV, payback, and contribution margin. Single working sheet (Unit Economics), no time-series forecast, no financial statements.

SHEET: Unit Economics (B1:BA1001)
All inputs and outputs on one sheet. Detail section (R56-R1001) has 48-month per-unit cash flow projections in columns E-BA.

INPUT CELLS:
Revenues:
- D10: Revenue per unit, recurring ($, default $25)
- D11: Revenue per unit, transaction ($)
- D12: Revenue per unit, one-time ($)

Cost of Sales:
- D15: COGS % recurring (default 10%)
- D16: COGS % one-time
- D17: COGS % transaction

Discounts:
- D20: Discount recurring ($)
- D21: Discount transaction ($)

Churn and Growth:
- D24: Billing period months, recurring (#, default 1)
- D25: Churn period months (#, default 1)
- D26: % Growth in gross margin per unit, annual (%, default 5%)
- D27: % Churn per period (%, default 10%)
- D28: Average customer lifetime months (#, default 10)
- D31: Months after acquisition for one-time (#)
- D34-D38: Transaction churn/growth/repeat settings

Discount Rate:
- D40: Discount rate, annual (%, default 10%)

Acquisition Costs:
- D45: CAC ($, default $65)
- D46: Cost of retention, recurring ($)
- D47: Cost of repeat, transaction ($)

OUTPUT CELLS (FORMULA):
- D49: LTV, Recurring
- D50: LTV, One-time
- D51: LTV, Transaction
- D52: LTV (total)
- D53: LTV / CAC
- D54: CAC Payback (months)

CRITICAL RULES:
1. Three revenue types modeled independently: Recurring, One-time, Transaction. Total LTV = sum.
2. Payback is on contribution margin, NOT revenue. Revenue payback overstates for high-COGS businesses.
3. LTV depends on churn assumption, gross margin, and time horizon. State all three.
4. LTV/CAC > 3 is contextual — the bar depends on stage, margins, and payback.
5. This model assumes constant churn. For cohort-decaying churn, LTV here is approximate.

<!-- HEMROCK_SHEET_MAP_START -->
## Sheet Reference (auto-generated, do not edit by hand — see _models/)

# Unit Economics Tool — Sheet Map

## Sheets (7)
README, License, Disclaimer, Unit Economics, Model Comparison, Additional Tools, Changelog

## Unit Economics (B1:BA1001) — Single sheet, all-in-one

### Inputs (R5-R47)
| Row | Label | Type | Default |
|-----|-------|------|---------|
| R7/D7 | Show/hide notes | DROPDOWN | "show" |
| **Revenues** | | | |
| R10/D10 | Revenue per unit (recurring) | INPUT ($) | $25 |
| R11/D11 | Revenue per unit (transaction) | INPUT ($) | $0 |
| R12/D12 | Revenue per unit (one-time) | INPUT ($) | $0 |
| **Cost of Sales** | | | |
| R15/D15 | COGS % (recurring) | INPUT (%) | 10% |
| R16/D16 | COGS % (one-time) | INPUT (%) | 0% |
| R17/D17 | COGS % (transaction) | INPUT (%) | 0% |
| **Discounts** | | | |
| R20/D20 | Discount recurring | INPUT ($) | $0 |
| R21/D21 | Discount transaction | INPUT ($) | $0 |
| **Churn & Growth** | | | |
| R24/D24 | Billing period months (recurring) | INPUT (#) | 1 |
| R25/D25 | Churn period months | INPUT (#) | 1 |
| R26/D26 | % Growth in gross margin/unit (annual) | INPUT (%) | 5% |
| R27/D27 | % Churn per period | INPUT (%) | 10% |
| R28/D28 | Average customer lifetime months | INPUT (#) | 10 |
| R31/D31 | Months after acquisition for one-time | INPUT (#) | 0 |
| R34/D34 | Transaction churn period months | INPUT (#) | 0 |
| R35/D35 | Transaction growth % | INPUT (%) | 0% |
| R36/D36 | Transaction churn % | INPUT (%) | 0% |
| R37/D37 | Repeat transactions per year | INPUT (#) | 0 |
| **Discount Rate** | | | |
| R40/D40 | Discount rate (annual) | INPUT (%) | 10% |
| R41/D41 | K, Recurring | FORMULA | 0.81 |
| R42/D42 | K, Transaction | FORMULA | 0.9 |
| **Acquisition Costs** | | | |
| R45/D45 | CAC | INPUT ($) | $65 |
| R46/D46 | Cost of retention (recurring) | INPUT ($) | $0 |
| R47/D47 | Cost of repeat (transaction) | INPUT ($) | $0 |

### Outputs (R49-R54)
| Row | Label | Type |
|-----|-------|------|
| R49/D49 | LTV, Recurring | FORMULA |
| R50/D50 | LTV, One-time | FORMULA |
| R51/D51 | LTV, Transaction | FORMULA |
| R52/D52 | LTV (total) | FORMULA |
| R53/D53 | LTV / CAC | FORMULA |
| R54/D54 | CAC Payback months | FORMULA |

### Detail Section (R56-R1001, columns E-BA)
- 48-month per-unit cash flow projection
- Monthly: Revenue, COGS, Gross Margin, Growth adjustment, Churn adjustment, Net margin
- Cumulative: Total margin, CAC payback tracking
- Separated by Recurring, One-time, Transaction revenue types

## Key characteristics
- Self-contained single sheet (no cross-sheet references)
- No time-series forecast — purely per-unit economics
- Three revenue types modeled independently: Recurring, One-time, Transaction
- Payback calculated on contribution margin, not revenue
<!-- HEMROCK_SHEET_MAP_END -->
