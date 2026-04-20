# Standard Financial Model

> Append to the universal primer when working on the Standard Financial Model.

I am working on the Hemrock Standard Financial Model, a 72-month (6-year) monthly financial model for startups. 19 sheets. Time-series columns run from AA (prior period) through CU (month 72).

SHEET MAP:
- Get Started (B1:G154): Central assumptions hub. ALL key inputs live here. Every other sheet references this.
- Revenues (B1:CU1174): Prebuilt revenue engine. 1,174 rows. Contains growth cohorts, conversion, retention cohorts, revenue recognition, MRR metrics. Duplicated for Segment 1 (R20-R691) and Segment 2 (R693-R1172).
- Forecast (B1:CU689): Main forecast engine. Driver system for expenses. Contains burn/runway calcs (R309-R387), revenue recognition (R389-R405), depreciation (R407-R429), debt repayment (R431-R586), taxes (R593-R611), inventory (R613-R639), MRR/ARR metrics (R651-R674), and valuation (R676-R688).
- Hiring Plan (B1:CU58): Per-role salary forecasting. Same driver system as Forecast.
- Statements (B1:CU121): Auto-generated. Income Statement (R11-R40), Balance Sheet (R43-R88), Cash Flows (R90-R121). DO NOT EDIT.
- Summary: Annual rollup. DO NOT EDIT.
- Key Metrics: SaaS KPIs (ARR waterfall, Magic Number, Rule of 40, LTV:CAC). DO NOT EDIT.
- Unit Economics (B1:BA1001): Per-unit LTV, CAC, payback. Has its own inputs at D7-D47.
- Budget: Forecast vs Actuals variance. DO NOT EDIT (except actuals input on Forecast R165-R228).
- Breakdown: Segment-level P&L. DO NOT EDIT.
- Sources & Uses: Funding deployment summary.

GET STARTED — KEY INPUT CELLS:
- D9: Company Name
- D10: Base Timescale (dropdown: monthly/quarterly/annually)
- D11: # of periods (default 72)
- D12: Date of first period
- D22: Revenue model type (dropdown: recurring, ecommerce, marketplace, advertising, financial services, top down, not applicable)
- D26: New Growth Units in first month (#)
- D28: Initial growth rate (%)
- D29: Growth rate deceleration (%)
- D31: Viral coefficient (K)
- D40: Conversion rate (%)
- D44-E44: Segment names
- D45-E45: % converting to each segment
- D46-E46: Churn rate (%)
- D47-E47: Churn period (months)
- D54-E54: Avg Revenue per Revenue Unit ($)
- D55-E55: Billing period (months)
- D76: Cash on hand beginning ($), C76: Currency symbol
- D79: Use auto revenue recognition (dropdown)
- D93: Depreciation months
- D106: Corporate tax rate
- D120: WACC/NPV discount rate
- D131-D142: Monthly seasonality (Jan-Dec)

FORECAST — DRIVER SYSTEM (per row, columns K-X):
Each expense/revenue row on Forecast (R25-R95) and Hiring Plan (R25-R55) uses this driver system:
- K: Initial Value
- L: Starts in period #
- M: Repeats every N months (1=monthly, 12=annually)
- N: Driver type dropdown ('...', '% of', '# per', '% change', '# change')
- O: Changes every N months
- P: Changing by (the rate)
- Q: Using Driver (references another row's label)
- R: Max N months
- S: Max value
- U-X: Boolean flags (Seasonality, Event, Custom, Escalation)
Alternatively, overwrite any formula cell in columns AB-CU with a direct value.

FORECAST — KEY SECTIONS:
- R25-R28: Operating Metrics (from Revenues sheet — do not overwrite)
- R37-R39: Fundraising (3 equity investment rows — use drivers or direct input)
- R42-R45: Revenue Categories 1-2 + Billings (from Revenues — do not overwrite)
- R50-R59: Salaries from Hiring Plan (formula — edit on Hiring Plan instead)
- R68-R69: Acquisition/Retention Costs (from Revenues)
- R70: Cost of Sales (driver: default 10% of Revenue Cat 1)
- R72-R95: Expense rows (INPUT via drivers, labeled TBD)
- R96: 'Insert new rows above this line' marker
- R165-R228: ACTUALS input section (same categories, enter historical data here)

REVENUES — KEY INPUT ROWS (can overwrite per month in cols AB-CU):
- R22: New Sales Hires per period
- R114: Manual growth adjustments
- R202: Manual conversion adjustments
- R378+: Per-month average revenue overrides

CROSS-SHEET FLOW:
Get Started → Revenues (growth, conversion, churn, pricing) → Forecast R25-R45 (metrics, revenue) → Statements → Summary
Hiring Plan → Forecast R50-R59 (salaries) → Statements
Forecast R165-R228 (actuals) merges with forecast at R231-R294 → Statements

CRITICAL RULES:
1. Never edit Statements, Summary, Key Metrics, Breakdown, or Key Reports — all formula.
2. Revenue showing zero? Check D22 (revenue model type) and D26-D29 (growth inputs) on Get Started first.
3. Adding expenses: use TBD rows R72-R95 on Forecast. Set the label in col B, category in col D (dropdown: R&D, Sales, G&A, Misc SG&A, Cost of Sales), then configure drivers in cols K-P.
4. Adding hires: use TBD rows R26-R55 on Hiring Plan. Set role name, category, salary in col K.
5. Seasonality: set monthly adjustments in D131-D142 on Get Started, then enable per-row in col U on Forecast.
6. The model supports two revenue segments. Configure segment names at D44-E44, splits at D45-E45, and independent churn/pricing per segment.

<!-- HEMROCK_SHEET_MAP_START -->
## Sheet Reference (auto-generated, do not edit by hand — see _models/)

# Standard Financial Model — Sheet Map

## Sheets (19)
README, License, Disclaimer, Get Started, Summary, Snapshot, Key Metrics, Key Reports, Revenues, Forecast, Hiring Plan, Statements, Sources & Uses, Unit Economics, Budget, Breakdown, Model Comparison, Glossary, Changelog

## Get Started Sheet (B1:G154) — CORE INPUT SHEET

### Model Structure (R6-R14)
| Row | Label | Type | Default |
|-----|-------|------|---------|
| R9/D9 | Company Name | INPUT | "Company" |
| R10/D10 | Base Timescale | DROPDOWN | "monthly" |
| R11/D11 | # of periods | INPUT | 72 (6 years) |
| R12/D12 | Date of first period | INPUT | Jan 2026 |
| R13/D13 | Fiscal year end | FORMULA | Dec 2026 |
| R14/D14 | Relative/absolute dates | DROPDOWN | "absolute" |

### Revenue Assumptions (R17-R58) — THE KEY SECTION
| Row | Label | Type | Default |
|-----|-------|------|---------|
| R20/D20 | Growth metric name | INPUT | "Growth Units" |
| R21/D21 | Revenue metric name | INPUT | "Revenue Units" |
| R22/D22 | Revenue model type | DROPDOWN | "recurring" |
| R26/D26 | New Growth Units month 1 | INPUT (#) | 100 |
| R27/D27 | Growth start date | INPUT | =D12 |
| R28/D28 | Initial growth rate | INPUT (%) | 10% |
| R29/D29 | Growth rate deceleration | INPUT (%) | -5% |
| R30/D30 | Use seasonality | DROPDOWN | "yes" |
| R31/D31 | Viral coefficient (K) | INPUT (#) | 1.2 |
| R34/D34 | CPA per paid Growth Unit | INPUT ($) | 0 |
| R35/D35 | % acquired through paid | INPUT (%) | 0 |
| R36/D36 | Use Outbound Sales | DROPDOWN | "no" |
| R40/D40 | Conversion rate | INPUT (%) | 10% |
| R41/D41 | Conversion lag months | INPUT (#) | 0 |
| R44/D44-E44 | Segment names | INPUT | "Segment 1", "Segment 2" |
| R45/D45-E45 | % to each segment | INPUT (%) | 50%/50% |
| R46/D46-E46 | Churn rate | INPUT (%) | -10% each |
| R47/D47-E47 | Churn period months | INPUT (#) | 1 (monthly) |
| R53/D53-E53 | Starting Revenue Units | INPUT (#) | 0 |
| R54/D54-E54 | Avg Revenue per Unit | INPUT ($) | $10 |
| R55/D55-E55 | Billing period months | INPUT (#) | 1 |
| R56/D56-E56 | % billed upfront | INPUT (%) | 100% |

### Revenue Model Types (R61-R70)
D22 selects from: recurring, ecommerce, marketplace, advertising, financial services, top down, not applicable

### Balance Sheet (R73-R97)
| Row | Label | Type | Default |
|-----|-------|------|---------|
| R76/D76 | Cash on hand beginning | INPUT ($) | 0 |
| R76/C76 | Currency symbol | INPUT | "$" |
| R79/D79 | Auto revenue recognition | DROPDOWN | "yes" |
| R83/D83 | Auto cash collection | DROPDOWN | "yes" |
| R84/D84 | Days AR | INPUT (#) | 0 |
| R93/D93 | Depreciation months | INPUT (#) | 36 |
| R97/D97 | Interest income rate | INPUT (%) | 0 |

### Debt (R99-R103)
| Row | Label | Type | Default |
|-----|-------|------|---------|
| R100/D100 | Annual interest rate | INPUT (%) | 0 |
| R101/D101 | Repayment term months | INPUT (#) | 0 |
| R102/D102 | Interest-only months | INPUT (#) | 0 |

### Taxes (R105-R109)
| Row | Label | Type | Default |
|-----|-------|------|---------|
| R106/D106 | Corporate tax rate | INPUT (%) | 0 |
| R107/D107 | Tax schedule | DROPDOWN | "quarterly" |
| R108/D108 | VAT rate | INPUT (%) | 0 |

### Valuation (R118-R126)
| Row | Label | Type | Default |
|-----|-------|------|---------|
| R120/D120 | WACC/NPV discount rate | INPUT (%) | 8% |
| R121/D121 | Long-term growth rate | INPUT (%) | 4% |
| R124/D124 | Multiple base | DROPDOWN | "revenues" |
| R125/D125 | EV multiple | INPUT (#) | 0 |
| R126/D126 | % weight for multiple | INPUT (%) | 50% |

### Seasonality (R128-R143)
R131-R142: Monthly % change inputs (Jan-Dec), R143 = sum check

### Model Checks (R146-R153)
All FORMULA returning yes/no

## Revenues Sheet (B1:CU1174) — REVENUE ENGINE

### Structure
Duplicated for Segment 1 and Segment 2. Contains:
- Outbound Sales cohorts (R20-R100)
- Growth Units cohorts (R103-R195)
- Conversion calculations (R199-R210)
- Revenue Units retention cohorts (R212-R373)
- Revenue calculations per model type (R375-R691)
- MRR metrics (R679-R691)
- Segment 2 repeats (R693-R1172)

### Key INPUT rows (can be overwritten per month in cols AB-CU)
- R22: New sales hires per period
- R99: Growth Units per ramped sales person
- R114: Manual growth adjustments
- R202: Manual conversion adjustments
- R378+: Per-month average revenue overrides

### Formulas to Never Touch
- Cohort tracking matrices (monthly retention/billing cohorts)
- Revenue recognition calculations
- MRR build calculations

## Forecast Sheet (B1:CU689) — FORECAST ENGINE

### Driver System (per row, columns K-X)
| Column | Purpose |
|--------|---------|
| K | Initial Value |
| L | Starts in period # |
| M | Repeats every N months |
| N | Changing based on ("...", "% of", "# per", "% change", "# change") |
| O | Changes every N months |
| P | Changing by % or # |
| Q | Using Driver (references another row label) |
| R | Max N months |
| S | Max value |
| U-X | Use Seasonality/Event/Custom/Escalation (true/false) |

### Main Input Area (R20-R96)
| Section | Rows | Notes |
|---------|------|-------|
| Operating Metrics | R25-R34 | Growth/Revenue Units from Revenues sheet; Salaries from Hiring Plan |
| Fundraising | R37-R39 | 3 equity investment rows |
| Revenues & Billings | R42-R47 | Rev Cat 1-2 from Revenues; Cat 3 is INPUT |
| Hiring Plan | R50-R65 | Salaries + Benefits from Hiring Plan sheet |
| Operating Expenses | R68-R95 | Acquisition/Retention from Revenues; COGS, expenses via drivers |

### Calculated Sections (all FORMULA)
| Section | Rows | Purpose |
|---------|------|---------|
| Forecast by Category | R99-R162 | Aggregates into standard categories |
| Actuals by Category | R165-R228 | INPUT area for actual financial data |
| Actuals + Forecast | R231-R294 | Merged view flowing to Statements |
| Burn/Runway | R309-R387 | Net burn, runway months, cash projection matrix |
| Revenue Recognition | R389-R405 | Deferred revenue, AR |
| Depreciation/Amort | R407-R429 | Schedules |
| Debt Repayment | R431-R586 | Monthly principal + interest |
| Tax Schedules | R593-R611 | Corporate + VAT |
| Inventory | R613-R639 | Purchase/disposal calcs |
| MRR/ARR Metrics | R651-R674 | Monthly/annual recurring revenue |
| Valuation | R676-R688 | DCF + Multiple methods |

## Hiring Plan Sheet (B1:CU58)
- R24: Outbound Sales Staff (FORMULA from Revenues)
- R25: CEO row (INPUT: salary, category)
- R26-R55: 30 TBD hire rows (INPUT)
- Same driver system as Forecast (cols K-X)
- Category dropdown: R&D, Sales, G&A, Misc SG&A
- Segment dropdown: Unallocated, Segment 1, Segment 2

## Statements Sheet — All FORMULA
- R11-R40: Income Statement
- R43-R88: Balance Sheet
- R90-R121: Cash Flow Statement

## Other Sheets (all FORMULA)
- Summary: Annual rollup (5 years)
- Snapshot: 6-month forward cash flow
- Key Metrics: SaaS KPIs (ARR, Magic Number, Rule of 40, LTV:CAC)
- Unit Economics: Per-unit LTV, CAC, payback
- Budget: Forecast vs Actuals variance
- Breakdown: Segment-level P&L
- Sources & Uses: Funding deployment summary

## Cross-Sheet References
```
Get Started → Revenues (growth, conversion, churn, pricing, seasonality)
Get Started → Forecast (timescale, balance sheet, tax, valuation)
Get Started → Unit Economics (revenue per unit, churn)
Revenues → Forecast R25-R28 (operating metrics)
Revenues → Forecast R42-R45 (revenue/billings)
Revenues → Forecast R68-R69 (acquisition/retention costs)
Hiring Plan → Forecast R50-R59 (salaries by category)
Forecast (R231-R294) → Statements
Statements → Summary (annual via SUMIFS)
```
<!-- HEMROCK_SHEET_MAP_END -->
