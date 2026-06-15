# Runway & Cash Budget

> Append to the universal primer when working on the Runway Tool.

I am working on the Hemrock Runway Tool, a 36-month budget and cash forecast for seed-stage companies. 11 sheets. Same driver system as the Standard Model but simpler — no prebuilt revenue engine.

SHEET MAP:
- Get Started (B1:G77): Model structure, balance sheet assumptions, seasonality, model checks.
- Forecast: Main input sheet. Driver system for revenues, expenses, funding. Same column structure as Standard Model.
- Statements: Auto-generated Income Statement, Balance Sheet, Cash Flows. DO NOT EDIT.
- Summary: Annual rollup (3 years). DO NOT EDIT.
- Key Reports: Charts. DO NOT EDIT.
- Sources & Uses: Funding deployment summary.

GET STARTED — KEY INPUT CELLS:
- D9: Company Name
- D10: Base Timescale (dropdown: monthly/quarterly/annually)
- D11: # of months (default 36)
- D12: Date of first period
- D20: Cash on hand beginning ($), C20: Currency symbol
- D23: Use auto revenue recognition (dropdown)
- D27: Use auto cash collection (dropdown)
- D28: Days Accounts Receivable
- D36: Depreciation straight-line months (default 36)
- D39: Corporate tax rate (default 21%)
- D40: Tax payment schedule (dropdown: monthly/quarterly/annually)
- D41: VAT rate
- D55-D66: Monthly seasonality (Jan-Dec)
- D73-D77: Model checks (FORMULA: balance sheet balances, cash positive, etc.)

FORECAST — DRIVER SYSTEM (same as Standard Model):
Columns K-P per row: Initial Value, Starts in period, Repeats every N months, Changing based on, Changes every N months, Changing by.

FORECAST — KEY ROWS:
- R19: Equity Investment (INPUT, default $500k SAFE in month 1)
- R20-R21: Additional funding rows (INPUT)
- R24: First revenue stream (INPUT via drivers, default $5k/mo)
- R25: Subscribers metric (INPUT, default 100 with 5% monthly growth)
- R26: Second revenue stream (INPUT, uses # per subscriber)
- R27-R28: Additional revenue rows
- R31-R35: Expenses by category (R&D, Sales, G&A, Misc SG&A, Cost of Sales)
- R36-R48: Additional expense rows (TBD, insert above R49 marker)
- R52-R80: Totals by Category (FORMULA — aggregates into standard categories)

CRITICAL RULES:
1. This model has NO prebuilt revenue engine. Revenues are entered directly on the Forecast sheet via the driver system or direct cell overwrite.
2. For detailed SaaS or ecommerce revenue modeling, use the SaaS Forecasting Tool or Ecommerce Forecasting Tool and link results into the Forecast sheet.
3. Adding expenses: use TBD rows R36-R48. Set label, category dropdown, then configure drivers.
4. Cash balance going negative? Check D20 (starting cash) and R19 (funding) first.

<!-- HEMROCK_SHEET_MAP_START -->
## Sheet Reference (auto-generated, do not edit by hand — see _models/)

# Runway Tool Sheet Map

## Sheets
README, License, Disclaimer, Get Started, Summary, Key Reports, Forecast, Sources & Uses, Statements, Glossary, Changelog

## Get Started Sheet (B1:G77)

### Section: Model Structure (R6-R14)
| Row | Label | Type | Default | Notes |
|-----|-------|------|---------|-------|
| R9 | Company Name | INPUT | "Company" | Used in Disclaimer |
| R10 | Base Timescale | INPUT/DROPDOWN | "monthly" | monthly/quarterly/annually |
| R11 | # of months in model | INPUT | 36 | Sets total periods |
| R12 | Date of first period | INPUT (date) | Jan 2026 | End date of first period |
| R13 | Fiscal year end | INPUT (date) | Dec 2026 | End of fiscal year |
| R14 | Relative or absolute dates | INPUT/DROPDOWN | "relative" | |

### Section: Balance Sheet (R17-R49)
| Row | Label | Type | Default | Notes |
|-----|-------|------|---------|-------|
| R20 | Cash on hand, beginning | INPUT ($) | 0 | Col C = currency symbol |
| R23 | Use auto revenue recognition | DROPDOWN | "yes" | |
| R24 | Deferred revenue start month | INPUT (#) | 1 | |
| R27 | Use auto cash collection | DROPDOWN | "yes" | |
| R28 | Days Accounts Receivable | INPUT (#) | 0 | |
| R31 | Prepaid Expenses % of SG&A | INPUT (%) | 0 | |
| R32 | Accounts Payable % of SG&A | INPUT (%) | 0 | |
| R33 | Accrued Liabilities % of SG&A | INPUT (%) | 0 | |
| R36 | Depreciation straight-line months | INPUT (#) | 36 | |
| R39 | Corporate Income Tax rate | INPUT (%) | 21% | |
| R40 | Tax payment schedule | DROPDOWN | "quarterly" | |
| R41 | VAT rate | INPUT (%) | 0 | |
| R42 | VAT payment schedule | DROPDOWN | "quarterly" | |
| R45 | Inventory lead time months | INPUT (#) | 0 | |
| R46 | Safety stock % of COGS | INPUT (%) | 0 | |
| R47 | Minimum order quantity ($) | INPUT ($) | 0 | |
| R48 | % paid at purchase | INPUT (%) | 100% | |
| R49 | Remaining paid N days later | INPUT (#) | 0 | |

### Section: Seasonality (R52-R67)
| Row | Label | Type | Default |
|-----|-------|------|---------|
| R55-R66 | January-December % change | INPUT (%) | 0 each |
| R67 | Estimated impact (should = 0) | FORMULA | |

### Section: Model Checks (R70-R77)
All formula cells that return yes/no:
- R73: Balance sheet balances?
- R74: Cash stays above zero?
- R75: Deferred revenues positive?
- R76: Inventory positive?
- R77: PP&E positive?

## Forecast Sheet (B1:columns through 36+ periods)

### Driver System (columns K-U per row)
| Column | Purpose |
|--------|---------|
| K | Initial Value (INPUT) |
| L | Starts in period # (INPUT) |
| M | Repeats every N months (INPUT) |
| N | Changing based on (DROPDOWN) |
| O | Changes every N months (INPUT) |
| P | Changing by % or # (INPUT) |

### Row Map
| Row | Label | Type | Notes |
|-----|-------|------|-------|
| R5-R11 | Timescale header | FORMULA | Period, date, FY, seasonality |
| **R18** | **Fundraising section** | | |
| R19 | Equity Investment | INPUT | Default: $500k SAFE in month 1 |
| R20-R21 | Additional funding rows | INPUT | TBD |
| **R23** | **Revenues section** | | |
| R24 | First revenue stream | INPUT via drivers | Default: $5k starting month 1 |
| R25 | Subscribers (metric) | INPUT via drivers | Default: 100, 5% monthly growth |
| R26 | Second revenue stream | INPUT via drivers | Uses # per subscriber |
| R27-R28 | Additional revenue rows | INPUT | TBD |
| **R30** | **Expenses section** | | |
| R31 | R&D | INPUT via drivers | |
| R32 | Sales & Marketing | INPUT via drivers | |
| R33 | G&A | INPUT via drivers | |
| R34 | Misc SG&A | INPUT via drivers | |
| R35 | Cost of Sales | INPUT via drivers | |
| R36-R48 | Additional expense rows | INPUT | TBD, insert above R49 |
| R49 | "Insert new rows above" marker | | |
| **R52** | **Totals by Category** | FORMULA | |
| R55-R80 | Category aggregations | FORMULA | Subscribers, GTV, Bookings, Billings, Revenue by stream, SG&A by category, COGS, CAPEX, D&A, Interest, Other, Taxes |

## Statements Sheet
All FORMULA, three monthly statements built from the Forecast. Output only; nothing to edit. Period headers (R4-R7) pull from the Forecast.

### Income Statement (R10-R38)
Revenues with % Growth (R12-R13), COGS (R15), Gross Margin and Gross Margin % (R17-R18), SG&A and % of Revenues (R20-R21), Operating Income (EBITDA) and % (R23-R24), Depreciation and Amortization (R26-R27), Interest Expense (R28), Other Income and Expense (R29-R30), EBT (R32), Taxes (R34), Net Income and Cumulative Net Income (R36-R38).

### Balance Sheet (R41-R86)
| Section | Rows | Lines |
|---------|------|-------|
| Assets | R43-R57 | Cash, Accounts Receivable, Inventory, Prepaid Expense, Other Current Assets, Total Current Assets; PP&E, Accumulated Depreciation, Total Fixed Assets; Other Assets, Accumulated Amortization; Total Assets |
| Current Liabilities | R59-R68 | Accounts Payable, Inventory AP, Deferred Revenue Liability, Accrued Liabilities, Corporate Tax Payable, VAT Payable, Working Capital Loan Facility, Total Current Liabilities |
| Noncurrent Liabilities | R70-R75 | Convertible Notes and SAFEs, Debt Financing, Accrued Interest, Total Noncurrent Liabilities |
| Stockholders Equity | R77-R83 | Owners Equity, Equity Investment, SAFE Investment, Retained Earnings, Net Income, Total Stockholders Equity |
| Check | R85-R86 | Total Liabilities and Shareholder's Equity, and a balance Check |

### Statement of Cash Flows (R89-R117)
Cash beginning of period (R91); Operations (R93-R98): Net Income plus Depreciation, Amortization, Changes in Working Capital; Investing (R100-R103): CAPEX, Other Assets; Financing (R105-R113): changes in equity, SAFE, and convertible debt investments, new debt financing, changes in owners equity, debt repayment, working capital line draw; then Net Cash Flow (R115) and Cash End of Period (R117).

## Summary Sheet
All FORMULA. Annual rollup built from the Statements via SUMIFS by fiscal year. A condensed income statement (Revenues with Y/Y growth and growth multiple, COGS, Gross Margin, SG&A, EBITDA, D&A, Interest, Other, Taxes, Net Income, each with % of revenue), an annual Statement of Cash Flows (operations / investing / financing to cash end of period), and an annual Balance Sheet (Assets, Liabilities, Shareholder's Equity).

## Sources & Uses Sheet
All FORMULA, over a selectable month range (R5-R6). Sources (R8-R11): external funding and revenues. Uses (R14-R23): the expense categories from the Forecast plus working capital as the balancing item. Each line is shown in dollars and as a percent of the total.
<!-- HEMROCK_SHEET_MAP_END -->
