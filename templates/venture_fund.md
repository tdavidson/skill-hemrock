# Venture Capital Model (flagship)

> Append to the universal primer when working on the Hemrock Venture Capital Model.

I am working on the Hemrock Venture Capital Model, a quarterly fund forecast with 16 sheets, 3 built-in scenarios, fund statements, and management company modeling.

SHEET MAP:
- Get Started (B1:L250): Core fund assumptions, investment strategy, portfolio construction, return expectations, fund performance. ALL key inputs.
- Forecast: Quarterly cash flows over fund life (46+ quarters). Capital calls, fees, investments, exits, distributions, NAV, J-curve.
- Statements: Fund-level Statement of Operations, Balance Sheet, Cash Flows. DO NOT EDIT.
- Management Company: GP entity P&L (fee revenue, expenses, carry income).
- Scenarios: Side-by-side comparison of 3 scenarios with sensitivity inputs.
- Scenario 2/3 Get Started + Forecast: Independent copies for alternate scenarios.
- Key Reports: Charts. DO NOT EDIT.

GET STARTED — CAPITAL AND FUND ASSUMPTIONS (R5-R20):
- D9: Total Committed Capital (Fund Size)
- D10: GP Commit % (treated as LP interest for carry)
- D11: Organizational Expenses (one-time)
- D12: Operational Expenses (annual)
- D13: Management Fees % per year (on committed or called capital)
- D14: Carry %
- D15: Preferred Return % (0% default, uncommon for US venture)
- D16: GP Catchup % (only if preferred return)
- D17: New Investment Period (quarters, default 16 = 4 years)
- D18: Management Fees period (quarters, default 40 = 10 years)
- D19: Fund Operations period (quarters, default 46)
- D20: Extension Period (quarters, default 6)

GET STARTED — RECYCLING (R23-R31):
- D27: Target recycling %
- D28: Based on committed capital or management fees (dropdown)
- D29: From exits within N quarters of investment
- D30: Up to invested capital or proceeds per investment (dropdown)
- D31: Recycled through quarter N

GET STARTED — INVESTMENT STRATEGY (R34-R70) — THIS IS THE KEY SECTION:
Unlike simpler models, this tracks multi-stage graduation across up to 6 rounds.
- R37 columns: New Investment, 2nd Round, 3rd, 4th, 5th, 6th, Exit
- D39-I39: % Allocation of Capital to entry at each stage (INPUT)
- D42-I42: Average invested per new investment (INPUT)
- D44-I44: % of Companies that Graduate to next round (INPUT, e.g. 30%, 50%, 50%, 60%, 70%)
- D68-I68: Average Initial Investment per round (INPUT)
- D69-I69: Post-money Valuation per round (INPUT, e.g. $6M, $18M, $54M, $162M, $324M, $648M)
- D70-I70: Dilution from round (INPUT, e.g. 0%, 20%, 20%, 20%, 20%, 20%)
- R45-R66: Graduation calculations, exit counts, ownership tracking — ALL FORMULA from above inputs

GET STARTED — RETURN EXPECTATIONS (R98-R130):
All FORMULA. Calculated from the Investment Strategy inputs above. Shows exit multiples per round, proceeds per investment, ownership at exit net of dilution, weighted average holding period.

GET STARTED — FUND PERFORMANCE (R133-R153):
All FORMULA. Shows Called Capital, Expenses, Fees, Recycling, Invested Capital, Proceeds, Carry (with waterfall), Distributions (Total/LP/GP), Gross/Net Multiple, Gross/Net IRR, PIC/DPI/RVPI.

FORECAST — QUARTERLY CASH FLOWS:
Each column is a quarter. Tracks: capital calls, management fees, fund expenses, investment pacing (new + follow-on), exit proceeds (based on holding periods), distributions, NAV, cumulative IRR (J-curve).

CRITICAL RULES:
1. Fund size ≠ invested capital. Invested capital = fund size - management fees - expenses + recycling.
2. TVPI is NET (after fees and carry). Always lower than gross exit multiple.
3. Carry is on net profits after return of capital, not on gross proceeds. Default: European whole-fund waterfall, no hurdle.
4. The Investment Strategy section (R34-R70) drives everything downstream. Change graduation rates or valuations there, not in the return calculations.
5. Do not edit Forecast, Statements, or fund performance rows directly — they are all formulas from Get Started.
6. NAV must reach zero at fund end.
7. Three scenarios are independent — each has its own Get Started + Forecast. Edit the scenario's Get Started to change its assumptions.

<!-- HEMROCK_SHEET_MAP_START -->
## Sheet Reference (auto-generated, do not edit by hand — see _models/)

# Venture Capital Model Sheet Map (Flagship)

## Sheets (16)
README, License, Get Started, Scenario 2 Get Started, Scenario 2 Forecast, Scenario 3 Get Started, Scenario 3 Forecast, Forecast, Key Reports, Scenarios, Statements, Management Company, Resources, Model Comparison, Glossary, Changelog

## Get Started (B1:L250): Core Input Sheet

### Capital and Fund Assumptions (R5-R20)
| Row | Label | Type | Default | Notes |
|-----|-------|------|---------|-------|
| R9/D9 | Total Committed Capital | INPUT ($) | $25M | All committed assumed called |
| R10/D10 | GP Commit % | INPUT (%) | 2% | Treated as LP interest for carry |
| R11/D11 | Organizational Expenses | INPUT ($) | $100k | One-time, first quarter |
| R12/D12 | Operational Expenses (annual) | INPUT ($) | $75k | In addition to mgmt fees |
| R13/D13 | Management Fees % per year | INPUT (%) | 2% | Based on committed or called capital |
| R14/D14 | Carry % | INPUT (%) | 20% | |
| R15/D15 | Preferred Return | INPUT (%) | 0% | Uncommon for US venture |
| R16/D16 | GP Catchup % | INPUT (%) | 0% | Only if preferred return |
| R17/D17 | New Investment Period (quarters) | INPUT (#) | 16 (4 years) | |
| R18/D18 | Management Fees period (quarters) | INPUT (#) | 40 (10 years) | |
| R19/D19 | Fund Operations period (quarters) | INPUT (#) | 46 (11.5 years) | |
| R20/D20 | Extension Period (quarters) | INPUT (#) | 6 (1.5 years) | |

### Recycling (R23-R31)
| Row | Label | Type | Default |
|-----|-------|------|---------|
| R27/D27 | Target recycling % | INPUT (%) | 0% |
| R28/D28 | Based on (committed/mgmt fees) | DROPDOWN | "committed capital" |
| R29/D29 | From exits ≤ N quarters post-invest | INPUT (#) | 24 |
| R30/D30 | Up to (invested capital/proceeds) | DROPDOWN | "invested capital" |
| R31/D31 | Recycled through quarter | INPUT (#) | 16 |

### Investment Strategy and Expectations (R34-R70): Unique to This Model
This section models multi-stage graduation, not just return tiers.

| Row | Label | Type |
|-----|-------|------|
| R37 | Column headers: New Investment, 2nd Round, 3rd, 4th, 5th, 6th, Exit | |
| R39/D39-I39 | % Allocation to entry at each stage | INPUT (%) | Default: 100% to New |
| R40 | # First Checks | FORMULA |
| R41 | Capital allocated per strategy | FORMULA |
| R42/D42-I42 | Average invested per new investment | INPUT ($) | $750k |
| R44/D44-I44 | % Graduate to next round | INPUT (%) | 30%, 50%, 50%, 60%, 70%, 0% |
| R45-R65 | Graduation calculations (per entry stage) | FORMULA | |
| R66 | % that exit after each stage | FORMULA | |
| R68/D68-I68 | Average Initial Investment | INPUT ($) | $750k |
| R69/D69-I69 | Post-money Valuation per round | INPUT ($) | $6M, $18M, $54M, $162M, $324M, $648M |
| R70/D70-I70 | Dilution from round | INPUT (%) | 0%, 20%, 20%, 20%, 20%, 20% |

### Portfolio Construction (R73-R95): Detailed per-round
| Row | Label | Type |
|-----|-------|------|
| R76-R95 | Per-round: check size, reserves, follow-on amounts | FORMULA from Strategy section |
| R77 | # of Checks (new + follow) | FORMULA |
| R78 | Total Capital Deployed | FORMULA |

### Return Expectations (R98-R130)
All formula cells, calculated from the Investment Strategy inputs:
- Exit multiples per round
- Proceeds per investment
- Ownership at exit (net of dilution)
- Weighted average holding period
- Return distribution (writeoffs/small/medium/large)

### Fund Performance (R133-R170): all FORMULA
| Row | Metric |
|-----|--------|
| R137 | Called Capital (LP + GP) |
| R138 | Fund Expenses |
| R139 | Management Fees |
| R140 | Recycled Capital |
| R141 | Invested Capital |
| R142 | Proceeds |
| R143 | Carried Interest (with preferred return waterfall) |
| R144 | Distributions (Total / LP / GP) |
| R146 | Gross Multiple |
| R147 | Net Multiple (Total / LP / GP) |
| R148 | Gross IRR |
| R149 | Net IRR (Total / LP / GP) |
| R151-R153 | PIC, DPI, RVPI |

### Fund Details (R155-R250)
Extended calculations: per-investment detail, capital deployment pacing, exit timing, carry waterfall mechanics.

## Forecast: Quarterly Cash Flows

This is where the headline assumptions on Get Started turn into a quarter-by-quarter cash flow. It runs the full life of the fund, one column per quarter, and almost everything flows automatically from Get Started. A handful of cells on this sheet are editable, and they are the ones worth knowing.

**How the sheet is laid out.** Column B is the line label and column C holds inline notes (and, on a few rows, an optional manual override). Column D sets how that row aggregates over time (sum, final, initial, or max), and column E shows the resulting all-period total. The quarters themselves run left to right across columns G onward, one column per quarter, out to the end of fund operations plus any extension. Rows 4 and 5 are the column headers: relative quarter number and the date at the end of each period.

### Triggers (R7-R11)
On/off flags, one value per quarter, that switch fund activities on and off as the fund ages. They are derived from the time periods on Get Started, so you normally leave them alone, but they are exposed here if you want to hand-tune when an activity stops.

| Row | Label | Drives |
|-----|-------|--------|
| R8 | New investment period | Quarters in which new (first-check) investments can be made |
| R9 | Management fees period | Quarters in which management fees are charged |
| R10 | Fund operations period | Quarters the fund is still operating |
| R11 | Proceeds recycling period | Quarters in which exit proceeds can be recycled into new investing |

### Inputs (R13-R20)
The editable assumptions that live on the Forecast sheet itself, separate from Get Started.

| Row | Label | Type | Notes |
|-----|-------|------|-------|
| R14 | Management Fees basis | INPUT | Charge on committed or called capital. Can be changed per quarter across the row. |
| R16 | GP Commit excluded from LP capital | TOGGLE | By default the GP commit is treated as LP interest for carry. |
| R17 | GP Commit excluded from management fees | TOGGLE | Default checked: the GP does not pay management fees on its own commit. |
| R18 | GP Commit covered via cashless contributions | TOGGLE | If management fees are used to satisfy the GP commit. |
| R19 | Committed Capital, % called per year | INPUT (%) | Pacing of capital calls across the call period. |
| R20 | Called Capital, % of total committed | INPUT (%) | Optional manual override to the automatically calculated call schedule. |

### Capital roll-forward (R22-R28)
A simple beginning-to-end cash bridge for each quarter. Capital at the beginning of period (R22), plus called capital (R23), plus proceeds (R24), less distributions and carried interest (R25), less expenses (R26), less investments (R27), equals capital at the end of the period (R28). This is the running cash balance of the fund.

### Detailed cash flows (R30-R58)
The line items that build up the roll-forward. Each is a quarterly series.

| Row | Line |
|-----|------|
| R30-R31 | Committed Capital, Called Capital |
| R32 | Manual Investments (type a specific check into a specific quarter to override the paced schedule) |
| R33-R36 | New Investments, Prorata Opportunities, Reserves for Follow-on, Follow-on Investments |
| R37-R38 | Total Investments by cohort of new investments, Total Investments |
| R39-R41 | Organizational Expenses, Operational Expenses, Management Fees |
| R42-R43 | Recycled Capital, Proceeds |
| R44-R46 | Preferred Return, GP Catchup, Carried Interest (the distribution waterfall, quarter by quarter) |
| R47 | Distributions |
| R48-R53 | Writeoffs, Invested Capital Exited, Change in Invested Capital, Change in Unrealized Gain (Loss), Change in Residual Value, Change in Undrawn Capital Commitments |
| R54-R58 | The same flows split to LPs and GPs: Committed and Called Capital from LPs, change in invested capital from LPs, Distributions to LPs, Distributions to GPs |

### Cumulative versions (R59-R87)
Each detailed flow above repeated as a running cumulative total, so you can read the fund's position at any point in time rather than just the activity in a single quarter. Residual value at the end of a period is the cumulative change in residual value.

### Multiples and exposure (R89-R93)
The standard fund ratios computed per quarter: Paid-in Capital (PIC, R89), Residual Value to Paid-in (RVPI, R90), Distributed Value to Paid-in (DVPI, R91), Total Value to Paid-in (TVPI, R92), and Exposure as a percent of total committed capital (R93).

### Performance (R95-R103)
Gross and net return lines, realized only: Net (Investments) Proceeds and its cumulative (R95-R96), Gross Multiple and Gross IRR (R97-R98), Net (Called Capital) Distributions and its cumulative (R99-R100), Net Multiple and Net IRR (R101-R102), and an Interim Net IRR that includes unrealized value (R103).

### IRR build grid (R104 onward)
One row per quarter, each building the dated cash-flow vector that feeds the IRR formulas above. This is what produces the J-curve: the interim IRR is negative early while capital is being called and invested, then climbs as exits land.

## Statements: Consolidated Financial Statements

GAAP-style fund-level statements, built on the same quarterly grid as the Forecast (R4 and R5 pull the period headers straight from it). Three statements stacked on one sheet. Most lines are wired from the Forecast; a few income and expense lines are blank scaffolding you fill in if your fund has them.

### Statement of Operations (R7-R46)
| Section | Rows | Notes |
|---------|------|-------|
| Interest Income | R9-R13 | Bank, portfolio, and other interest, then Total. Not pulled from the Forecast by default; enter it if relevant. |
| Investment Income | R15-R19 | Operating income, dividend income, other income, then Total. Also manual by default. |
| Operating Expenses | R21-R27 | Fund administration, audit, tax prep, legal, professional fees, then Total. Operational expenses from the Forecast land here by default. |
| Management Fees | R29-R32 | Management Fees, Management Fees Offset, Net Management Fees |
| Organizational Fees | R34 | One-time organizational expense |
| Total Expenses | R36 | |
| Net Investment Income (Expenses) | R38 | Income less expenses, before gains |
| Gain (loss) on investments | R40-R44 | Net realized gain (loss), net change in unrealized appreciation or depreciation, FX (not pre-built), then Net gain (loss) |
| Net Income (loss) | R46 | Net increase or decrease in partners' capital |

### Statement of Financial Condition, the balance sheet (R49-R90)
| Section | Rows | Lines |
|---------|------|-------|
| Assets | R51-R61 | Cost of investments, unrealized gain (loss), investments at fair value, cash, accounts receivable, escrow proceeds receivable, capital contributions receivable, other assets, Total Assets |
| Liabilities | R63-R70 | Line of credit, distributions payable, accrued expenses, management fee payable, accounts payable, capital contributions received in advance, Total Liabilities |
| Investor's Capital | R72-R88 | LP and GP capital contributions, cashless and in-kind contributions, GP note receivable, contributions total; capital distributions, carried interest, GP distributions, tax withholding, distributions total; net income, net realized and unrealized gain (loss); Total Investor's Capital |
| Check | R90 | Assets must equal Liabilities plus Investor's Capital |

### Statement of Cash Flows (R93-R130)
| Section | Rows | Notes |
|---------|------|-------|
| Operating activities | R95-R115 | Net income, then adjustments: realized and unrealized gains, purchases of investments, proceeds from sales, and changes in the operating assets and liabilities (R105-R114 mirror the balance sheet lines). Ends at Net cash from operating activities. |
| Financing activities | R117-R126 | Capital contributions and distributions from the Investor's Capital section, ending at Net cash from financing activities |
| Cash reconciliation | R128-R130 | Cash beginning of period, net change, cash end of period |

## Management Company
A separate profit and loss for the management entity, distinct from the fund itself:
- Revenue from management fees
- Operating and organizational expenses
- GP commit obligations
- Carried interest income
- Net income to the GP

## Scenarios: side-by-side comparison and sensitivity

The model carries three full scenarios. The base case is the main Get Started and Forecast pair. Scenarios 2 and 3 each have their own complete Get Started and Forecast sheets ("Scenario 2 Get Started" with "Scenario 2 Forecast", and the same for Scenario 3). The Scenarios sheet itself is the dashboard that compares all three and the place you drive the two alternates from.

### What the Scenarios sheet shows (B2:N32)
Three columns, left to right: Conservative Case (Scenario 2), Base Case (Scenario 1), and High Case (Scenario 3).

| Rows | Content |
|------|---------|
| R23-R26 | Gross Multiple, Net Multiple, Gross IRR, and Net IRR for each of the three scenarios, pulled from each scenario's Get Started |
| R28 | % Change in # of High Exits, the first sensitivity input (default -50% conservative, +50% high) |
| R29 | % Change in Valuations of High Exits, the second sensitivity input (default -50% conservative, +50% high) |
| R31-R32 | Notes: R28 changes how many of the portfolio's big winners land; R29 changes how large those winning exits are |

### How the two alternate scenarios are driven
Scenario 2 and Scenario 3 Get Started sheets reference the base Get Started for most assumptions, then apply the two sensitivity inputs from the Scenarios sheet to perturb the count and the valuation of high exits. So out of the box you tune two numbers per alternate scenario and the rest follows the base. If you want a fully independent scenario (different fund size, fees, or strategy), overwrite any cell directly on that scenario's Get Started sheet; it will stop tracking the base for that input.

## Key differences from Fund Economics Tool
- **Quarterly cash flows** vs aggregate
- **Investment Strategy section** with graduation rates, multi-stage follow-ons, dilution tracking
- **Preferred return + GP catchup** waterfall support
- **Recycling provisions** with configurable limits
- **Fund Statements** (operations, balance sheet, cash flows)
- **Management Company** entity modeling
- **Per-investment ownership tracking** through dilution across rounds
<!-- HEMROCK_SHEET_MAP_END -->
