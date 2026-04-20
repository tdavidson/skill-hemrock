# SaaS Forecasting Tool

> Append to the universal primer when working on the Hemrock SaaS Forecasting Tool.

I am working on the Hemrock SaaS Forecasting Tool, a focused revenue model for SaaS, subscription, and services businesses. 8 sheets, two modes (Aggregate + Pipeline), no expenses or financial statements.

SHEET MAP:
- Get Started (B1:F29): All key assumptions.
- Forecast (B1:BO78): Aggregate mode — subscriber curves, revenue, MRR.
- Enterprise SaaS (B1:BT45): Pipeline mode — per-client contracts.
- Key Reports: Charts. DO NOT EDIT.

GET STARTED — KEY INPUT CELLS:
- D6: Company Name
- D7: Currency symbol
- D8: First forecast date
- D12: Avg Revenue per Subscriber per month ($, default $30)
- D13: Gross Margin % (default 87.5%)
- D14: CAC per new subscriber ($, default $25)
- D15: Retention cost per renewed subscriber ($, default $5)
- D16: Deferred Revenue beginning ($)
- D19: Date to start growth
- D20: Subscriber label + first month count (default 'Subscribers', 25)
- D21: Subscribers beginning of month 1
- D22: Baseline growth rate (%, default 10%)
- D23: Growth rate decline per month (%, default -5%)
- D24: Churn rate per period (%, default 5%)
- D25: Reactivation rate (%)
- D26: Contract Cycle (months, default 12)
- D27: Billing Cycle (months, default 12)

FORECAST (AGGREGATE MODE) — KEY ROWS:
- R15-R31: Assumptions mirrored from Get Started (FORMULA)
- R34-R43: Subscriber calculations — beginning, not up for renewal, new, renewed, churned, reactivated, end of month, up for billing, growth rates (FORMULA)
- R46: Revenues (FORMULA: avg rev * ending subscribers)
- R47: Marketing Spend (FORMULA: new*CAC + renewed*retention)
- R48: Billings (FORMULA: billing cycle logic)
- R49: Deferred Revenue (FORMULA)
- R52-R58: MRR build — Beginning, Existing, New, Renewed, Churned, Reactivated, Ending MRR (FORMULA)

ENTERPRISE SAAS (PIPELINE MODE) — PER-CLIENT INPUTS:
Rows R17-R30, each row is one client/deal:
- Col B: Client name (INPUT)
- Col D: % Likelihood to Close (INPUT)
- Col E: $ Total Contract Value (INPUT)
- Col F: Contract Cycle months (INPUT)
- Col G: Billing Cycle months (INPUT)
- Col H: Start Date (INPUT)
- Col J: % Revenue Churn or Expansion at end of cycle (INPUT)
R31: 'Insert additional rows above this line' marker
- R36-R38: Bookings, Billings, Revenues (FORMULA from client rows)
- R41-R44: Deferred Revenue schedule (FORMULA)

CRITICAL RULES:
1. Use ONE mode at a time. Aggregate (Forecast sheet) OR Pipeline (Enterprise SaaS sheet). Using both double-counts revenue.
2. Bookings ≠ Billings ≠ Revenue. Bookings = TCV * probability. Billings = amounts invoiced per billing cycle. Revenue = recognized per period.
3. Contract length and billing cycle interact. A 12-month contract billed monthly vs annually produces very different deferred revenue and cash profiles.
4. ARR = ending MRR * 12. It is NOT annual revenue.
5. Do not modify deferred revenue formulas (R49 on Forecast, R41-R44 on Enterprise SaaS).

<!-- HEMROCK_SHEET_MAP_START -->
## Sheet Reference (auto-generated, do not edit by hand — see _models/)

# SaaS Forecasting Tool — Sheet Map

## Sheets (8)
README, License, Disclaimer, Get Started, Key Reports, Forecast, Enterprise SaaS, Changelog

## Get Started (B1:F29)
| Row | Label | Type | Default |
|-----|-------|------|---------|
| R6/D6 | Company Name | INPUT | "Company" |
| R7/D7 | Currency | INPUT | "$" |
| R8/D8 | First forecast date | INPUT (date) | Apr 2026 |
| R9/D9 | Fiscal year end | INPUT (date) | Dec 2026 |
| R12/D12 | Avg Revenue per Subscriber/month | INPUT ($) | $30 |
| R13/D13 | Gross Margin % | INPUT (%) | 87.5% |
| R14/D14 | CAC per new subscriber | INPUT ($) | $25 |
| R15/D15 | Retention cost per renewed sub | INPUT ($) | $5 |
| R16/D16 | Deferred Revenue beginning | INPUT ($) | $0 |
| R19/D19 | Date to start growth | INPUT (date) | Apr 2026 |
| R20/D20 | Subscriber label + first month count | INPUT | "Subscribers", 25 |
| R21/D21 | Subscribers beginning of month 1 | INPUT (#) | 0 |
| R22/D22 | Baseline growth rate | INPUT (%) | 10% |
| R23/D23 | Growth rate decline per month | INPUT (%) | -5% |
| R24/D24 | Churn rate per period | INPUT (%) | 5% |
| R25/D25 | Reactivation rate | INPUT (%) | 0% |
| R26/D26 | Contract cycle months | INPUT (#) | 12 |
| R27/D27 | Billing cycle months | INPUT (#) | 12 |

## Forecast (B1:BO78) — Aggregate Mode
### Timescale (R4-R12): Period, date, FY, quarter — all FORMULA
### Assumptions (R15-R31): Mirror of Get Started inputs — FORMULA references
### Subscribers (R33-R43):
- R34: Subscribers beginning of month (FORMULA)
- R35: Not up for renewal (FORMULA)
- R36: New during month (FORMULA)
- R37: Renewed during month (FORMULA)
- R38: Churned during month (FORMULA)
- R39: Reactivated (FORMULA)
- R40: End of month (FORMULA)
- R41: Up for billing (FORMULA)
- R42: Growth rate new subs (FORMULA)
- R43: Growth rate total subs (FORMULA)
### Revenue (R45-R49):
- R46: Revenues (FORMULA: avg rev * ending subs)
- R47: Marketing Spend (FORMULA: new*CAC + renewed*retention)
- R48: Billings (FORMULA: billing cycle logic)
- R49: Deferred Revenue (FORMULA)
### MRR (R51-R58):
- R52-R57: Beginning, Existing, New, Renewed, Churned, Reactivated MRR (all FORMULA)
- R58: Ending MRR (FORMULA)
### Outputs (R60+): Annual summaries, unit economics — FORMULA

## Enterprise SaaS (B1:BT45) — Pipeline Mode
### Per-client rows (R17-R30, INPUT):
| Column | Purpose |
|--------|---------|
| B | Client name |
| D | % Likelihood to Close |
| E | $ Total Contract Value |
| F | Contract Cycle (months) |
| G | Billing Cycle (months) |
| H | Start Date |
| J | % Revenue Churn or Expansion at end of cycle |
### Calculated rows:
- R33: New Clients (FORMULA)
- R34: Clients end of period (FORMULA)
- R36: Bookings (FORMULA: TCV * probability)
- R37: Billings (FORMULA: billing cycle)
- R38: Revenues (FORMULA: recognition)
- R41-R44: Deferred Revenue schedule (FORMULA)

## Key difference from Standard Model
No expenses, no financial statements, no balance sheet. Revenue-only tool. Two modes (Aggregate on Forecast, Pipeline on Enterprise SaaS) — use one at a time.
<!-- HEMROCK_SHEET_MAP_END -->
