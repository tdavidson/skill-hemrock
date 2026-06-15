# Venture Capital Model — Quarterly Forecast

> Append to the universal primer when working on the Hemrock Venture Capital Model, Quarterly Forecast (the simplified quarterly variant of the flagship VC Model).

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

# Venture Capital Model, Quarterly Forecast Sheet Map

## Sheets (15)
README, License, Get Started, Get Started 2, Forecast 2, Get Started 3, Forecast 3, Scenarios, Key Reports, Forecast, Management Company, Resources, Model Comparison, Glossary, Changelog

## Structure
Three scenarios (base + 2 alternates), each with their own Get Started + Forecast pair. The base scenario uses "Get Started" + "Forecast"; scenarios 2 and 3 use "Get Started 2"/"Forecast 2" and "Get Started 3"/"Forecast 3". The Scenarios sheet compares all three side-by-side.

## Get Started: Core Inputs

### Capital and Fund Assumptions (R5–R18)
All time periods are in **quarters**, not years.

| Row | Label | Type | Default |
|-----|-------|------|---------|
| R9/E9 | Total Committed Capital (Fund Size) | INPUT ($) | $25M |
| R10/E10 | GP Commit, as % of committed capital | INPUT (%) | 2% |
| R11/E11 | Organizational Expenses (one-time) | INPUT ($) | $100k |
| R12/E12 | Operational Expenses (annual) | INPUT ($) | $75k |
| R13/E13 | Management Fees, per year, as % of committed capital | INPUT (%) | 2% |
| R14/E14 | Carry | INPUT (%) | 20% |
| R15/E15 | Active Investment time period (quarters) | INPUT (#) | 16 |
| R16/E16 | Fund Duration / Management Fees time period (quarters) | INPUT (#) | 40 |
| R17/E17 | Fund Operations time period (quarters) | INPUT (#) | 40 |
| R18/E18 | Fund Duration Extension Period (quarters) | INPUT (#) | 0 |

### Recycling (R21–R29)
| Row | Label | Type | Default |
|-----|-------|------|---------|
| R25/E25 | Target recycling %, and max achievable | INPUT (%) | 0% |
| R26/E26 | Based on (committed capital / management fees) | DROPDOWN | committed capital |
| R27/E27 | From exits N quarters or less post-investment | INPUT (#) | 24 |
| R28/E28 | Up to (invested capital / proceeds) per investment exited | DROPDOWN | invested capital |
| R29/E29 | Able to invest in (new investments / follow-on) | DROPDOWN | new investments |

### Investment Strategy and Expectations (R32–R93)
The quarterly model uses an **Exit Outcome** structure (Fail / Low / Medium / High), not a multi-stage graduation chain like the flagship.

#### Investment Performance and Capital Allocation (R37–R45)
Columns are the four exit outcomes. Each row is one metric across all four columns.

| Row | Label | Type |
|-----|-------|------|
| R38 | % of Investments per Exit Outcome | INPUT (%) |
| R39 | # of Companies that achieve each Exit Outcome | FORMULA |
| R40 | Index of average investment per overall average | INPUT (%) |
| R41 | Adjustment to % of Investments → % of Invested Capital | FORMULA |
| R42 | % of Invested Capital per Exit Outcome | FORMULA |
| R43–R45 | % of Initial / First Follow / Second Follow capital per outcome | FORMULA |

#### Initial Investment (R47–R50)
| Row | Label | Type | Default |
|-----|-------|------|---------|
| R48 | Average Initial Investment | INPUT ($) | $500k |
| R49 | Postmoney Valuation | INPUT ($) | $5M |
| R50 | Ownership %, at initial investment | FORMULA | 10% |

#### First Follow-on Round (R52–R60)
| Row | Label | Type | Default |
|-----|-------|------|---------|
| R53 | % of Initial Investments to Participate in Pro-rata | INPUT (%) | 0% |
| R54 | Follow-on Investment Amount | INPUT ($) | $400k |
| R55 | Time from Initial → Follow-on (quarters) | INPUT (#) | 0 |
| R56 | Postmoney Valuation | INPUT ($) | $20M |
| R57 | Dilution from Round (all investors) | INPUT (%) | 20% |
| R58 | Dilution from New Option Pool | INPUT (%) | 10% |
| R59 | Ownership % per company followed on, post follow-on | FORMULA | 9% |
| R60 | Ownership % per average initial investment, post follow-on | FORMULA | 7% |

#### Second Follow-on Round (R62–R70)
Mirror of First Follow-on rows above, with defaults: $1.08M check, $60M postmoney, 20% dilution, 10% option pool.

#### Additional Follow-ons (R72–R73)
| Row | Label | Type | Default |
|-----|-------|------|---------|
| R73 | Additional Dilution from Second Follow-on to Exit | INPUT (%) | 0% |

#### Exit (R75–R93)
| Row | Label | Type |
|-----|-------|------|
| R76 | Average Exit Value | INPUT/FORMULA |
| R77 | Average Hold Period (quarters) | INPUT (#) |
| R78 | Average Investment per Company | FORMULA |
| R79 | Ownership % at Exit | FORMULA |
| R80 | Average Proceeds per Company | FORMULA |
| R81–R88 | Total Initial / First Follow / Second Follow / Total Follow capital per outcome | FORMULA |
| R89–R90 | Total Invested Capital ($ and %) | FORMULA |
| R91–R92 | Total Proceeds ($ and %) | FORMULA |
| R93 | Gross Exit Multiple per Exit Outcome | FORMULA |

### Portfolio Construction (R96–R102)
| Row | Label | Type | Default |
|-----|-------|------|---------|
| R100/E100–F100 | % Allocation of Invested Capital (New / Follow) | INPUT (%) | 100% / 0% |
| R101/E101–F101 | Average Check Size | INPUT ($) | $500k |
| R102/E102–F102 | # of Checks | FORMULA | calculated |

### Return Assumptions (R105–R112)
Four exit outcomes, by % of investments per outcome.

| Row | Label | Default |
|-----|-------|---------|
| R109 | Fail | 60% |
| R110 | Low | 20% |
| R111 | Medium | 10% |
| R112 | High | 10% |

### Fund Performance (R115–R131): all FORMULA
Headline metrics that summarize the model output.

| Row | Metric |
|-----|--------|
| R118 | Called Capital (Paid-in Capital) |
| R119 | Management Fees and Fund Expenses |
| R120 | Budgeted Invested Capital |
| R121 | Recycled Capital |
| R122 | Invested Capital |
| R123 | Proceeds |
| R124 | Carried Interest |
| R125 | Distributions |
| R127 | Gross Multiple |
| R128 | Net Multiple |
| R129 | Gross IRR |
| R130 | Net IRR |
| R131 | Max Exposure, as % of Committed Capital |

## Forecast: Quarterly Cash Flows

Where the Get Started assumptions become a quarter-by-quarter cash flow across the life of the fund. Same engine as the flagship Venture Capital Model. Almost everything flows automatically; a few cells on this sheet are editable.

**Layout.** Column B is the line label, column C holds notes and a few optional overrides, column D is the aggregation method (sum / final / initial / max), column E is the all-period total, and the quarters run left to right across columns G onward, one column per quarter.

### Triggers (R7-R11)
On/off flags per quarter, derived from the Get Started time periods, that switch fund activities on and off as the fund ages: new investment period (R8), management fees period (R9), fund operations period (R10), proceeds recycling period (R11). Normally left alone.

### Inputs (R13-R21)
The editable assumptions that live on the Forecast itself: Management Fees basis (R14, charge on committed or called capital), the three GP-commit treatment toggles (excluded from LP capital R16, excluded from management fees R17, covered via cashless contributions R18), Committed Capital % called per year (R19), and optional manual overrides for the Called Capital and Invested Capital pacing (R20-R21).

### Capital roll-forward (R23-R29)
The quarterly cash bridge: capital beginning of period (R23), plus called capital (R24), plus proceeds (R25), less distributions and carried interest (R26), less fees (R27), less investments (R28), equals capital end of period (R29).

### Detailed cash flows (R31-R60)
Each is a quarterly series:

| Rows | Lines |
|------|-------|
| R31-R32 | Committed Capital, Called Capital |
| R33 | Manual Investments (type a check into a specific quarter to override the paced schedule) |
| R34-R37 | New Investments, Prorata Opportunities, Reserves for Follow-on, Follow-on Investments |
| R38-R39 | Total Investments by cohort, Total Investments |
| R40-R42 | Organizational Expenses, Operational Expenses, Management Fees |
| R43-R44 | Recycled Capital, Proceeds |
| R45-R47 | Preferred Return, GP Catchup, Carried Interest (the waterfall, quarter by quarter) |
| R48 | Distributions |
| R49-R54 | Writeoffs, Invested Capital Exited, Change in Invested Capital, Change in Unrealized Gain (Loss), Change in Residual Value, Change in Undrawn Capital Commitments |
| R55-R59 | The LP and GP splits: Committed and Called Capital from LPs, change in invested capital from LPs, Distributions to LPs, Distributions to GPs |
| R60 | New Investments (number of companies) |

### Cumulative versions (R61-R90)
Each flow above repeated as a running cumulative total, so you can read the fund's position at any point rather than just the activity in one quarter.

### Multiples and exposure (R92-R96)
PIC (R92), RVPI (R93), DVPI (R94), TVPI (R95), and Exposure as a percent of total committed capital (R96).

### Performance (R98-R106)
Realized-only return lines: Net (Investments) Proceeds and cumulative (R98-R99), Gross Multiple and Gross IRR (R100-R101), Net (Called Capital) Distributions and cumulative (R102-R103), Net Multiple and Net IRR (R104-R105), and Interim Net IRR including unrealized value (R106).

### IRR build grid (R107 onward)
One row per quarter, each building the dated cash-flow vector that feeds the IRR formulas. This produces the J-curve.

## Scenarios: side-by-side comparison and sensitivity

The model carries three full scenarios. The base case is the main Get Started and Forecast pair. Scenarios 2 and 3 have their own complete pairs ("Get Started 2" with "Forecast 2", "Get Started 3" with "Forecast 3"). The Scenarios sheet is the dashboard and the place you drive the two alternates from.

### What the Scenarios sheet shows (B2:N32)
Three columns: Conservative Case (Scenario 2), Base Case (Scenario 1), High Case (Scenario 3).

| Rows | Content |
|------|---------|
| R23-R26 | Gross Multiple, Net Multiple, Gross IRR, Net IRR for each scenario, pulled from each scenario's Get Started (E127-E130) |
| R28 | % Change in # of High Exits (default -50% conservative, +100% high) |
| R29 | % Change in Valuations of High Exits (default -25% conservative, +25% high) |
| R31-R32 | Notes on what each sensitivity input changes |

### How the alternates are driven
Get Started 2 and Get Started 3 reference the base Get Started for most assumptions, then apply the two sensitivity inputs from the Scenarios sheet to perturb the count and valuation of high exits. Tune two numbers per alternate and the rest follows the base, or overwrite any cell directly on a scenario's Get Started sheet to make it fully independent (different fund size, strategy, or return outcomes).

## Key Reports
Pre-built summary views and charts pulling from the base scenario.

## Management Company
A separate entity model, distinct from the fund:
- **Revenues** (R7-R10): Management Fees, plus a spare line, totaled
- **Expenses** (R12-R27): Salary, Contractors, Travel, Marketing, Software, Annual LLC filings, Insurance, several Taxes lines, and spare rows, totaled
- **Management Company Cash** (R29-R34): cash beginning of period, revenues, expenses, external funding placeholder, cash end of period
- **GP Carried Interest Entity** (R36-R38): Carried Interest and its disbursements (assumed immediate)

## Key differences from the flagship Venture Capital Model
- **Exit Outcome structure** (Fail/Low/Medium/High) rather than the flagship's multi-stage graduation chain (Seed → Series A → … → Series F+)
- **Up to two follow-on rounds** modeled explicitly (First Follow + Second Follow), with everything beyond folded into "Additional Dilution"
- **3 full scenario copies** (Get Started 2/3 + Forecast 2/3), independent assumptions
- **No Statements sheet**: the flagship has full fund-level Statement of Operations / Balance Sheet / Cash Flows; the quarterly does not
- **Time periods in quarters** throughout (Active Investment, Fund Duration, Operations, Extension)
<!-- HEMROCK_SHEET_MAP_END -->
