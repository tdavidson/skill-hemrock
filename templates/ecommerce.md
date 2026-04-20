# Ecommerce Forecasting Tool

> Append to the universal primer when working on the Hemrock Ecommerce Forecasting Tool.

I am working on the Hemrock Ecommerce Forecasting Tool, a cohort-based revenue model for DTC and ecommerce. 9 sheets, 48-month forecast, optional historicals. No financial statements.

SHEET MAP:
- Get Started (B1:F49): All key assumptions.
- Forecast (B1:BO199): Cohort-based calculations, retention curves, revenue, unit economics.
- Historicals (B1:BO66): Optional — enter actual historical cohort order data.
- Key Reports: Charts. DO NOT EDIT.

GET STARTED — KEY INPUT CELLS:
- D6: Company Name, D7: Currency
- D8: First forecast date, D9: Fiscal year end
- D12-D14: Historical dates (optional, for Historicals sheet)
- D17: Avg Revenue per Order, new customer ($, default $50)
- D18: Avg Revenue per Order, repeat customer ($, default $40)
- D19: Baseline rate of change in AOV (%, default 10%)
- D20: AOV rate decline per month (%, default -5%)
- D22-D24: Cost of Sales % (default 25%, 10%, 0%)
- D28-D29: Shipping Revenue/Cost per order ($)
- D31: CAC new customer ($, default $30)
- D32: CAC repeat customer ($, default $10)
- D37: Date to start growth
- D38: New Customers first month (#, default 550)
- D39: Baseline growth rate (%, default 90%)
- D40: Growth rate decline per month (%, default -15%)
- D41: Conversion Rate — sessions to orders (%, default 2%)
- D42: Customers beginning (#)
- D43: Churn rate per period (%, default 50%)
- D44: Repeat Cycle months (#, default 3)
- D47-D48: Optional cohort performance adjustment (after N customers, change by)

FORECAST — KEY STRUCTURE:
- R15-R48: Assumptions mirrored from Get Started (FORMULA)
- R44: Retention curve — calculated from churn + repeat cycle. Can be overwritten with manual curve.
- R46: Adjustment factor applied to all cohorts (INPUT)
- R50-R100+: Order cohorts — each row is a monthly cohort, columns track orders per period based on retention curve (FORMULA)
- R51: Website Traffic (FORMULA: orders / conversion rate)
- R52: New Customers per period (FORMULA)
- R54: Total Orders (FORMULA: sum of all cohorts)
- Revenue section: Orders * AOV per cohort, separated new vs repeat
- Unit Economics: CAC, LTV, payback, contribution margin

HISTORICALS SHEET (optional INPUT):
- Enter actual order counts per monthly cohort
- Model blends historical retention with forecast assumptions
- Helps calibrate the retention curve

CRITICAL RULES:
1. Each monthly cohort is tracked separately. Do not average across cohorts.
2. Retention in ecommerce ≠ SaaS churn. Retention = probability of repeat purchase, not subscription renewal.
3. AOV is per transaction, not per customer per period.
4. LTV depends on the time horizon. Always state whether it is 12-month, 24-month, or lifetime.
5. Contribution margin must include COGS + payment processing + fulfillment + returns.
6. Do not modify the cohort lookup formulas — they map cohort age to the retention curve.

<!-- HEMROCK_SHEET_MAP_START -->
## Sheet Reference (auto-generated, do not edit by hand — see _models/)

# Ecommerce Forecasting Tool — Sheet Map

## Sheets (9)
README, License, Disclaimer, Get Started, Key Reports, Forecast, Historicals, Model Comparison, Changelog

## Get Started (B1:F49)
### Setup (R5-R14)
| Row | Label | Type | Default |
|-----|-------|------|---------|
| R6/D6 | Company Name | INPUT | "Company" |
| R7/D7 | Currency | INPUT | "$" |
| R8/D8 | First forecast date | INPUT (date) | Jan 2025 |
| R9/D9 | Fiscal year end | INPUT (date) | Dec 2025 |
| R12/D12 | First historical date | INPUT (date) | Jan 2021 |
| R13/D13 | Historical FY end | INPUT (date) | Dec 2021 |
| R14/D14 | Last historical date | INPUT (date) | Dec 2024 |

### Revenue & Marketing (R16-R34)
| Row | Label | Type | Default |
|-----|-------|------|---------|
| R17/D17 | Avg Revenue per Order, new | INPUT ($) | $50 |
| R18/D18 | Avg Revenue per Order, repeat | INPUT ($) | $40 |
| R19/D19 | Baseline rate of change AOV | INPUT (%) | 10% |
| R20/D20 | Rate decline per month | INPUT (%) | -5% |
| R22/D22 | Cost of Sales % | INPUT (%) | 25% |
| R23/D23 | Additional COGS % | INPUT (%) | 10% |
| R24/D24 | Additional COGS % (2nd) | INPUT (%) | 0% |
| R28/D28 | Shipping Revenue per order | INPUT ($) | $0 |
| R29/D29 | Shipping Cost per order | INPUT ($) | $0 |
| R31/D31 | CAC new customer | INPUT ($) | $30 |
| R32/D32 | CAC repeat customer | INPUT ($) | $10 |

### Growth & Churn (R36-R48)
| Row | Label | Type | Default |
|-----|-------|------|---------|
| R37/D37 | Date to start growth | INPUT (date) | Jan 2025 |
| R38/D38 | New Customers first month | INPUT (#) | 550 |
| R39/D39 | Baseline growth rate | INPUT (%) | 90% |
| R40/D40 | Growth rate decline per month | INPUT (%) | -15% |
| R41/D41 | Conversion rate (sessions→orders) | INPUT (%) | 2% |
| R42/D42 | Customers beginning | INPUT (#) | 0 |
| R43/D43 | Churn rate per period | INPUT (%) | 50% |
| R44/D44 | Repeat cycle months | INPUT (#) | 3 |
| R47/D47 | After N total customers adjust | INPUT (#) | 0 |
| R48/D48 | Change cohort performance by | INPUT (#) | 1 |

## Forecast (B1:BO199) — Cohort-based
### Assumptions (R15-R48): Mirrors Get Started — FORMULA
### Retention Curve (R44):
- Calculated from churn rate and repeat cycle
- Can be overwritten with manual retention curve
- R46: Adjustment factor applied to all cohorts
### Orders (R50-R100+):
- R51: Website Traffic (FORMULA from orders ÷ conversion)
- R52: New Customers per period (FORMULA)
- R54: Total Orders (FORMULA: sum of all cohorts)
- R55-R100+: Individual monthly cohorts — each row is a cohort, columns track orders per period (FORMULA based on retention curve)
### Revenue (R103+):
- Orders × AOV per cohort
- Separated into new vs repeat revenue
- COGS, shipping, marketing spend calculated
### Unit Economics (R150+):
- CAC, LTV, payback period
- Contribution margin

## Historicals (B1:BO66) — Optional INPUT
- Monthly cohort data for historical performance
- Users enter actual order counts per cohort
- Model blends historical retention with forecast assumptions

## Key difference
Cohort-based, not subscription. Each monthly cohort tracked separately. Retention = repeat purchase probability, not subscription churn.
<!-- HEMROCK_SHEET_MAP_END -->
