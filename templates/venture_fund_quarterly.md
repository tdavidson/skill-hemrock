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

# Venture Capital Model, Quarterly Forecast — Sheet Map

## Sheets (15)
README, License, Get Started, Get Started 2, Forecast 2, Get Started 3, Forecast 3, Scenarios, Key Reports, Forecast, Management Company, Resources, Model Comparison, Glossary, Changelog

## Structure
Three scenarios (base + 2 alternates), each with their own Get Started + Forecast pair. The base scenario uses "Get Started" + "Forecast"; scenarios 2 and 3 use "Get Started 2"/"Forecast 2" and "Get Started 3"/"Forecast 3". The Scenarios sheet compares all three side-by-side.

## Get Started — Core Inputs

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
Four exit outcomes — % of investments by outcome.

| Row | Label | Default |
|-----|-------|---------|
| R109 | Fail | 60% |
| R110 | Low | 20% |
| R111 | Medium | 10% |
| R112 | High | 10% |

### Fund Performance (R115–R131) — FORMULA
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

## Forecast — Quarterly Cash Flows
Quarterly time-series across the fund's life (40+ quarters). Columns are the time periods; rows are the cash-flow components.

Pulled entirely from Get Started inputs:
- Capital Calls per quarter
- Management Fees per quarter
- Fund Expenses per quarter
- Investments per quarter (paced over the active investment period)
- Exits per quarter (driven by hold-period assumptions and exit outcomes)
- Distributions per quarter
- NAV per quarter
- Cumulative metrics: PIC, DPI, RVPI, TVPI, IRR (the J-curve)

## Get Started 2 / Forecast 2, Get Started 3 / Forecast 3
Independent copies of Get Started + Forecast for scenarios 2 and 3. Each scenario can have completely different fund size, strategy, return outcomes, etc.

## Scenarios Sheet
Side-by-side comparison of all 3 scenarios:
- Gross / Net Multiple and IRR for each
- Sensitivity inputs that drive scenarios 2 and 3

## Key Reports
Pre-built summary views and charts pulling from the base scenario.

## Management Company
Separate P&L for the management company entity:
- Management fee revenue
- Operating expenses
- GP commit obligations
- Carry income projections

## Key differences from the flagship Venture Capital Model
- **Exit Outcome structure** (Fail/Low/Medium/High) rather than the flagship's multi-stage graduation chain (Seed → Series A → … → Series F+)
- **Up to two follow-on rounds** modeled explicitly (First Follow + Second Follow), with everything beyond folded into "Additional Dilution"
- **3 full scenario copies** (Get Started 2/3 + Forecast 2/3), independent assumptions
- **No Statements sheet** — the flagship has full fund-level Statement of Operations / Balance Sheet / Cash Flows; the quarterly does not
- **Time periods in quarters** throughout (Active Investment, Fund Duration, Operations, Extension)
<!-- HEMROCK_SHEET_MAP_END -->
