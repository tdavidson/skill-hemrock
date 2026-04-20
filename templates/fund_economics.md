# Fund Economics Tool

> Append to the universal primer when working on the Hemrock Fund Economics Tool.

I am working on the Hemrock Fund Economics Tool, a high-level venture fund model. 8 sheets, aggregate (no quarterly cash flows), 3 built-in scenarios.

SHEET MAP:
- Forecast (B1:K62): Main input and output sheet. All fund assumptions, portfolio construction, return tiers, and performance.
- Forecast_1 / Forecast_2: Copies for conservative and high scenarios.
- Scenarios (B2:N32): Side-by-side comparison with two sensitivity inputs.
- Glossary: VC terminology.

FORECAST — CAPITAL AND FUND ASSUMPTIONS (R5-R19):
- D9: Total Committed Capital ($, default $25M)
- D10: GP Commit % (default 2%), F10: toggle whether GP commit counts toward invested capital
- D11: Organizational Expenses, one-time ($, default $150k)
- D12: Operational Expenses, annual ($, default $100k)
- D13: Management Fees % per year (default 2%)
- D14: Recycled Capital % (default 10%)
- D15: Carry % (default 20%)
- D16: New Investment Period years (default 4)
- D17: Management Fees period years (default 10)
- D18: Fund Operations period years (default 10)
- D19: Extension Period years (default 0)

FORECAST — PORTFOLIO CONSTRUCTION (R22-R28):
- D26-E26: % Allocation New vs Follow-on (INPUT)
- D27-E27: Average Check Size (INPUT, default $750k)
- D28: # of Checks (FORMULA from capital / check size)

FORECAST — RETURN TIERS (R31-R39) — POWER LAW:
| R35 | Writeoff | INPUT: 60% of capital, 0x multiple, 2yr hold |
| R36 | Small    | INPUT: 20%, 1.5x, 3yr |
| R37 | Medium   | INPUT: 10%, 5x, 4yr |
| R38 | Large    | INPUT: 10%, 32x, 6yr |
| R39 | Totals   | FORMULA: weighted 4x, 5.5yr |

FORECAST — FUND PERFORMANCE (R41-R60) — ALL FORMULA:
Shows Total/LP/GP splits for: Called Capital, Expenses, Fees, Recycling, Invested Capital, Proceeds, Carry, Distributions, Gross/Net Multiple, Gross/Net IRR, PIC/DPI/RVPI.

SCENARIOS — SENSITIVITY INPUTS:
- R27: % Change in # of High Exits
- R28: % Change in Valuations of High Exits
These two inputs drive Forecast_1 (conservative) and Forecast_2 (high) return tier adjustments.

CRITICAL RULES:
1. Invested capital = fund size - management fees - expenses + recycling. Not fund size.
2. TVPI is NET. Always lower than gross exit multiple.
3. Use power-law return tiers (R35-R38), not a single average multiple.
4. Carry is on net profits after return of capital.
5. Default: European whole-fund waterfall, no hurdle.
6. No quarterly cash flows. For pacing, J-curve, or LP schedules, use the full Venture Capital Model.

<!-- HEMROCK_SHEET_MAP_START -->
## Sheet Reference (auto-generated, do not edit by hand — see _models/)

# Fund Economics Tool — Sheet Map

## Sheets (8)
README, License, Forecast, Forecast_1, Forecast_2, Scenarios, Glossary, Changelog

## Forecast (B1:K62) — Main Input & Output Sheet

### Capital and Fund Assumptions (R5-R19)
| Row | Label | Type | Default |
|-----|-------|------|---------|
| R9/D9 | Total Committed Capital (Fund Size) | INPUT ($) | $25M |
| R10/D10 | GP Commit % | INPUT (%) | 2% |
| R10/F10 | GP Commit counted toward invested | TOGGLE | true |
| R11/D11 | Organizational Expenses (one-time) | INPUT ($) | $150k |
| R12/D12 | Operational Expenses (annual) | INPUT ($) | $100k |
| R13/D13 | Management Fees % per year | INPUT (%) | 2% |
| R14/D14 | Recycled Capital % | INPUT (%) | 10% |
| R15/D15 | Carry % | INPUT (%) | 20% |
| R16/D16 | New Investment Period years | INPUT (#) | 4 |
| R17/D17 | Management Fees period years | INPUT (#) | 10 |
| R18/D18 | Fund Operations period years | INPUT (#) | 10 |
| R19/D19 | Extension Period years | INPUT (#) | 0 |

### Portfolio Construction (R22-R28)
| Row | Label | Type | Default |
|-----|-------|------|---------|
| R26/D26-E26 | % Allocation (New vs Follow) | INPUT (%) | 100% / 0% |
| R27/D27-E27 | Average Check Size | INPUT ($) | $750k / $0 |
| R28/D28-E28 | # of Checks | FORMULA | 28.6 / 0 |

### Return Assumptions (R31-R39) — POWER LAW TIERS
| Row | Type | % of Capital | # Investments | Avg Gross Multiple | Holding Period |
|-----|------|-------------|---------------|-------------------|----------------|
| R35 | Writeoff | INPUT 60% | FORMULA | 0x | INPUT 2yr |
| R36 | Small | INPUT 20% | FORMULA | INPUT 1.5x | INPUT 3yr |
| R37 | Medium | INPUT 10% | FORMULA | INPUT 5x | INPUT 4yr |
| R38 | Large | INPUT 10% | FORMULA | INPUT 32x | INPUT 6yr |
| R39 | Totals | FORMULA | FORMULA | FORMULA 4x | FORMULA |

### Fund Performance (R41-R60) — ALL FORMULA
| Row | Metric | Total | LP | GP |
|-----|--------|-------|----|----|
| R44 | Called Capital (Paid-in) | $25M | $24.5M | $500k |
| R45 | Fund Expenses | -$1.15M | | |
| R46 | Management Fees | -$4.9M | | |
| R47 | Recycled Capital | $2.5M | | |
| R48 | Invested Capital | -$21.45M | | |
| R49 | Proceeds | $85.8M | | |
| R50 | Carried Interest | | -$11.3M | +$11.3M |
| R51 | Distributions | $85.8M | $72.3M | $13.5M |
| R53 | Gross Multiple | 4.0x | | |
| R54 | Net Multiple | 3.43x | 2.95x | 26.9x |
| R55 | Gross IRR | 28.5% | | |
| R56 | Net IRR | 25.0% | 21.6% | 81.5% |
| R58-R60 | PIC, DPI, RVPI | 1.0 / 3.43 / 0 | | |

## Forecast_1 & Forecast_2 — Scenario Sheets
Identical structure to Forecast. Used for conservative and high cases.
- Assumptions are INPUT (can differ from base)
- Linked to Scenarios sheet for comparison

## Scenarios (B2:N32) — Comparison Output
- Shows Conservative, Base, High side by side
- R22-R25: Gross/Net Multiple, Gross/Net IRR for each
- R27-R28: Two sensitivity inputs (% change in # of high exits, % change in valuations)
- These two inputs drive Forecast_1 and Forecast_2 return tier adjustments

## Key characteristics
- No quarterly cash flows (unlike full VC Model)
- No time-series — everything is aggregate over fund life
- Three scenarios built in via duplicate sheets
- Power-law return tiers (zeros/small/medium/large) — not a single average multiple
<!-- HEMROCK_SHEET_MAP_END -->
