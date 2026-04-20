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

# Venture Capital Model — Sheet Map (Flagship)

## Sheets (16)
README, License, Get Started, Scenario 2 Get Started, Scenario 2 Forecast, Scenario 3 Get Started, Scenario 3 Forecast, Forecast, Key Reports, Scenarios, Statements, Management Company, Resources, Model Comparison, Glossary, Changelog

## Get Started (B1:L250) — CORE INPUT SHEET

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

### Investment Strategy and Expectations (R34-R70) — UNIQUE TO THIS MODEL
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

### Portfolio Construction (R73-R95) — Detailed per-round
| Row | Label | Type |
|-----|-------|------|
| R76-R95 | Per-round: check size, reserves, follow-on amounts | FORMULA from Strategy section |
| R77 | # of Checks (new + follow) | FORMULA |
| R78 | Total Capital Deployed | FORMULA |

### Return Expectations (R98-R130)
All FORMULA — calculated from Investment Strategy inputs:
- Exit multiples per round
- Proceeds per investment
- Ownership at exit (net of dilution)
- Weighted average holding period
- Return distribution (writeoffs/small/medium/large)

### Fund Performance (R133-R170) — FORMULA
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

## Forecast — Quarterly Cash Flows
Quarterly time-series (up to 46+ quarters):
- Capital calls per quarter
- Management fees per quarter
- Fund expenses per quarter
- Investment pacing (new + follow-on)
- Exit proceeds per quarter (based on holding periods from Strategy)
- Distributions per quarter
- NAV per quarter
- J-curve: cumulative IRR per quarter

## Statements
Fund-level financial statements:
- Statement of Operations
- Balance Sheet (Assets = Investments at cost + Unrealized gains; Liabilities = Carried interest payable)
- Statement of Cash Flows

## Management Company
P&L for the management entity:
- Revenue: Management fees
- Expenses: Operations, organizational
- GP commit obligations
- Carried interest income
- Net income to GP

## Scenarios
3 scenarios (base + 2 alternates), each with independent Get Started + Forecast sheets.
Scenarios sheet shows side-by-side comparison with sensitivity inputs.

## Key differences from Fund Economics Tool
- **Quarterly cash flows** vs aggregate
- **Investment Strategy section** with graduation rates, multi-stage follow-ons, dilution tracking
- **Preferred return + GP catchup** waterfall support
- **Recycling provisions** with configurable limits
- **Fund Statements** (operations, balance sheet, cash flows)
- **Management Company** entity modeling
- **Per-investment ownership tracking** through dilution across rounds
<!-- HEMROCK_SHEET_MAP_END -->
