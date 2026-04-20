# Venture Valuation Tool

> Append to the universal primer when working on the Hemrock Venture Valuation Tool.

I am working on the Hemrock Venture Valuation Tool, an evaluator for the returns on a single venture investment through graduation and exit. 7 sheets. Dual-mode: a full round-chain model AND a single-page breakpoint evaluator. Pick one, not both.

SHEET MAP:
- Venture Valuation (B1:M165): Full model. One average investment carried through 7 stages (Seed → Series F+), with graduation rates, full nonparticipating waterfall, and expected value per entry round.
- Simple Venture Valuation (A1:AB46): Single-page shortcut. No round chain, just breakpoint analysis on one investment with cumulative dilution.
- Resources, Model Comparison: Reference tables. Informational.
- Changelog: Version history. Keep hidden.

COLUMN LAYOUT (Venture Valuation sheet):
- D=Seed, E=Series A, F=Series B, G=Series C, H=Series D, I=Series E, J=Series F+, K=Exit/Total, M=Notes. Row 5 is the round header.

VENTURE VALUATION — CAP TABLE INPUTS (R9-R49):
Two parallel SAFE/Note blocks: Investor (R10-R20) and All Other Preferred (R22-R32). Each has pre-money (R11-R15, R23-R27) and post-money (R16-R20, R28-R32) sub-blocks. INPUT cells: amount converting, discount rate, valuation cap per round. Share price (R14, R19, R26, R31) is the minimum of equity price, cap-based, and discount-based — assumes investor-friendly conversion.

NEW EQUITY INVESTMENT (R34-R49):
- R36: Investor, new Preferred Equity (INPUT $) — per-round new equity check from modeled investor
- R38: Total Investment Round — FORMULA (=0.2*R40/(1-0.2), assumes 20% sold per round); override with raw $ to set a specific round size
- R39: Option Pool as % of postmoney (INPUT %) — defaults 20/10/10/5/5/5/5
- R40: Premoney Valuation — D40 is INPUT $8M; E40-J40 are chained multipliers (×3, ×3, ×3, ×2, ×1.75, ×1.5). Overwrite each cell to set explicit future valuations.
- R45: Share Price (FORMULA, uses iterative calc)
- R47: Ownership %, Investor (FORMULA)

PROFORMA CAP TABLE (R51-R57):
- C52-C56: Starting cap table INPUTS (before Seed): Common, Investor shares, Other Preferred, Options, New Options
- R52: Common shares (10M default, constant)
- R56: Options New in Round — **circular formula** requiring iterative calculations
- R57: Fully-Diluted Shares, after Round

GRADUATION RATES (R62-R68) — THE KEY PORTFOLIO LAYER:
- R63: % Companies that Fail per stage (INPUT %) — defaults 0/45/35/20/10/5/0/0
- R64: % Companies that Exit per stage (INPUT %) — defaults 0/5/10/25/40/45/50/100
- R62: % Graduate = 1 − Fail − Exit (FORMULA)
- R66-R68: Cumulative probability of reaching / exiting at / failing after each stage (FORMULA). K67 + K68 = 1.

EXIT WATERFALL (R70-R134):
- R72: Exit Price as multiple of last postmoney (INPUT #) — defaults 1.5/1.5/1.5/0.85/0.75/1.15/1.25
- R73: Exit Price $ (FORMULA but INPUT-colored; can be overridden with raw $)
- R74: Total Liquidation Preferences (cumulative)
- R76-R86: Shares converting to common block (FORMULA)
- R88-R98: Shares NOT converting, taking preference (FORMULA)
- R100-R110: Proceeds from liquidation preferences (FORMULA)
- R112-R122: Proceeds from common distributions (FORMULA)
- R123: Check cell (should equal 0)
- R125-R134: Proceeds per share by class

INVESTOR RETURN SUMMARY (R136-R162):
- R140: Proceeds per Company, for Investor, if exited per stage
- R142: Total Proceeds, by type of exit (FORMULA = R140 × R68)
- R144: Gross Return Multiple if exit at each stage
- R147-R153: Gross Multiple per round, invested-through down, held-until right (matrix)
- R156-R162: Expected Value per round (matrix). K156-K162: total EV per $1 invested at each entry round (the money number)

SIMPLE VENTURE VALUATION — SHORTCUTS:
- D8: Pre-existing Liquidation Preferences (INPUT $)
- D11: Investor investment in modeled round (INPUT $, default $500k)
- D13: Premoney (INPUT $, default $6M)
- D20-D22: Shortcut dilution inputs (additional ownership, dilution from others, dilution from options) — bypasses round-by-round modeling
- D26: Exit Price row — 5 columns (D-H) auto-built as breakpoints from the LP stack, then 3x multipliers. Override with raw $ values.
- D36-H36: Probability of Exit per column (INPUT %) — H36 auto-balances to 100%
- D39: Expected Gross IRR via XIRR on R42:D44 — only covers 2 investments; extend the range manually if you have more follow-ons.

CRITICAL RULES:
1. Pick ONE sheet. Venture Valuation (detailed, round-chain) OR Simple Venture Valuation (single-page, breakpoints). They are independent. Using both is redundant.
2. ITERATIVE CALCULATIONS MUST BE ENABLED. R56 on the full sheet is a circular reference for option pool sizing. Excel: Preferences > Calculation > Enable iterative. Sheets: File > Settings > Calculation > Iterative. Without it you will see #REF or #CYCLE errors.
3. Waterfall assumes 1x NON-PARTICIPATING preferred, latest round senior (reverse chronological). No participating preferred, no caps, no anti-dilution. For participating preferred or anti-dilution, use the Cap Table & Exit Waterfall Tool instead.
4. This models ONE investor's returns on ONE average investment, not a whole fund. For fund-level portfolio math, use the Venture Capital Model or Fund Economics Tool.
5. The graduation chain (R62-R68) is the core insight — probabilities compound, so Seed-entry expected value is dominated by early-stage failure rates.
6. Row 38 (Total Investment Round) defaults to formula-driven 20% dilution per round. Overwrite with raw dollars for specific round sizes.
7. Row 40 Premoney is chained multipliers from D40. Each cell can be overwritten with an explicit valuation.
8. Simple sheet's D20-D22 dilution shortcuts are not mathematically exact for every scenario — that is the point. For precise follow-on modeling, use the full Venture Valuation sheet.

<!-- HEMROCK_SHEET_MAP_START -->
## Sheet Reference (auto-generated, do not edit by hand — see _models/)

# Venture Valuation Tool — Sheet Map

## Sheets (7)
README, License, Venture Valuation, Simple Venture Valuation, Resources, Model Comparison, Changelog

The workbook is dual-mode. The full **Venture Valuation** sheet models one average investment carried through 7 rounds (Seed → Series F+ → Exit), with graduation rates, full waterfall, and expected value. The **Simple Venture Valuation** sheet collapses all of that into a single-page, breakpoint-style evaluator for one specific investment. Use one or the other — they are independent.

Both sheets assume nonparticipating preferred, 1x liquidation preferences, and reverse-chronological seniority (latest round senior). They also rely on **iterative calculations** (circular references) to resolve option pool sizing — Excel/Sheets must have iterative calc enabled.

## Venture Valuation (B1:M165) — Full Per-Investment Model

Single working sheet. Columns **D–J** are the 7 round stages (D=Seed, E=Series A, F=Series B, G=Series C, H=Series D, I=Series E, J=Series F+). Column **C** is "Before Seed." Column **K** is totals or "Exit." Column **M** is notes only. Row 5 is the round header row.

### Cap Table Inputs: SAFEs and Notes Converting (R9-R32)
Two parallel blocks for the **modeled Investor** (R10-R20) and **All other Preferred** (R22-R32). Each block has a pre-money convertibles sub-block and a post-money SAFE sub-block.

| Row | Label | Type | Default |
|-----|-------|------|---------|
| R11 | Premoney SAFEs/Notes converting, Investor ($) | INPUT | $250k @ Seed |
| R12 | Discount Rate | INPUT (%) | 20% @ Seed |
| R13 | Valuation Cap ($) | INPUT | 0 |
| R14 | Share Price | FORMULA | min(equity, cap-based, discount-based) |
| R15 | Shares | FORMULA | amount / share price |
| R16 | Postmoney SAFEs converting, Investor ($) | INPUT | 0 |
| R17 | Discount Rate | INPUT (%) | 0 |
| R18 | Valuation Cap ($) | INPUT | 0 |
| R19 | Share Price | FORMULA | YC post-money treatment |
| R20 | Shares | FORMULA | amount / share price |
| R23-R27 | All Other Preferred — pre-money SAFEs/Notes block | INPUT + FORMULA | mirror of R11-R15 |
| R28-R32 | All Other Preferred — post-money SAFEs block | INPUT + FORMULA | mirror of R16-R20 |

The conversion math assumes investor-friendly conversion: share price is the minimum of equity price, cap-based price, and discount-based price. Comment on R11 explicitly says "assuming investor friendly conversion by default; feel free to edit for different conversion methods."

### New Preferred Equity Investment, per Round (R34-R49)
| Row | Label | Type | Default |
|-----|-------|------|---------|
| R35 | Convertibles converting in round | FORMULA | D11+D16 (and R23+R28 for others) |
| R36 | Investor, new Preferred Equity ($) | INPUT | 0 at most rounds; E36 is a circular formula `=D47*E38` seeded to maintain pro-rata at Series A |
| R37 | All other Preferred, new equity | FORMULA | R38 - R36 |
| R38 | Total Investment Round | FORMULA (INPUT-colored) | `=0.2*R40/(1-0.2)` — assumes 20% sold per round by default; edit to change |
| R39 | Option Pool, as % of postmoney cap | INPUT (%) | 20%, 10%, 10%, 5%, 5%, 5%, 5% |
| R40 | Premoney Valuation ($) | INPUT at D40; FORMULAS at E40-J40 | $8M → ×3 → ×3 → ×3 → ×2 → ×1.75 → ×1.5 |
| R41 | Postmoney Valuation | FORMULA | R40 + R38 |
| R42 | % of Company Sold in each round | FORMULA | R38 / R41 |
| R43 | # Shares issued to Investor in round | FORMULA | R53 − prior R53 |
| R44 | # Shares issued to all investors in round | FORMULA | (R53 + R54) − prior |
| R45 | Share Price | FORMULA | `(R40 − R41×R39) / fully-diluted denom` — uses option pool + convertibles + prior shares |
| R46 | Blended Share Price, incl. Convertibles | FORMULA | total dollars / total new shares |
| R47 | Ownership %, Investor | FORMULA | R53 / R57 |
| R48 | Ownership %, all other Preferred | FORMULA | R54 / R57 |
| R49 | Ownership %, all Preferred | FORMULA | R47 + R48 |

Row 38 is INPUT-styled (blue on grey) but shipped as a formula. The default makes total round size = 25% of premoney, giving 20% post-money ownership. Overwrite it with a raw dollar amount to set a specific round size.

Row 40 is the key valuation input — only D40 is a raw value; E40-J40 are formulas that chain valuation multipliers (3x, 3x, 3x, 2x, 1.75x, 1.5x). Edit each cell to set an explicit future valuation.

### Proforma Cap Table (R51-R57)
Standard running cap table.

| Row | Label | Type | Default |
|-----|-------|------|---------|
| R52 | Common shares | INPUT at C52; FORMULA after (`=prior`) | 10,000,000 constant |
| R53 | Investor shares (cumulative) | FORMULA | new round shares + converted SAFEs + prior |
| R54 | All other Preferred shares (cumulative) | FORMULA | same structure |
| R55 | Options and RSUs Available | FORMULA | prior row + prior-round new options |
| R56 | Options, New in Round | FORMULA | `=max(0, sum(R52:R55)*R39/(1-R39))` — **circular reference**, requires iterative calc |
| R57 | Fully-Diluted Shares, after Round | FORMULA | sum(R52:R56) |

C52, C53, C54, C55, C56 are INPUT cells on the "Before Seed" column — use these to seed a non-empty starting cap table. Default is 10M common and everything else zero.

### Graduation Rates and Exits (R59-R68)
The portfolio-level assumption layer. For one average investment, what fraction raises the next round, exits now, or fails.

| Row | Label | Type | Default |
|-----|-------|------|---------|
| R62 | % Companies that Graduate | FORMULA | 1 − R63 − R64 |
| R63 | % Companies that Fail | INPUT (%) | 0%, 45%, 35%, 20%, 10%, 5%, 0%, 0% |
| R64 | % Companies that Exit | INPUT (%) | 0%, 5%, 10%, 25%, 40%, 45%, 50%, 100% |
| R66 | Raise next round (cumulative prob.) | FORMULA | compounds graduation |
| R67 | Fail after this round | FORMULA | prob. of reaching × fail rate; K67 sums to ~70% |
| R68 | Exit after this round | FORMULA | prob. of reaching × exit rate; K68 sums to ~30% |

K67 + K68 = 1. Default distribution: ~70% eventually fail, ~30% eventually exit.

### Proceeds and Returns (R70-R134) — Waterfall Engine
For each hypothetical exit stage (column = round after which exit occurs), the model runs a nonparticipating-preferred waterfall.

| Row | Label | Type | Default |
|-----|-------|------|---------|
| R72 | Exit Price as multiple of last postmoney | INPUT (#) | 1.5, 1.5, 1.5, 0.85, 0.75, 1.15, 1.25 |
| R73 | Exit Price ($) | FORMULA (INPUT-colored) | R72 × R41; can be hard-overridden |
| R74 | Total Liquidation Preferences | FORMULA | running sum of R38 |
| R76-R86 | Shares Converting to Common block | FORMULA | per-class if/then on whether conversion > preference |
| R88-R98 | Shares NOT Converting (taking preference) block | FORMULA | complement of R76-R86 |
| R100-R110 | Proceeds from Liquidation Preferences block | FORMULA | min(preference, residual exit value) |
| R112-R122 | Proceeds from Distributions to Common block | FORMULA | pro-rata share of (exit − preferences) |
| R123 | Check (total proceeds = total exit) | FORMULA | should equal 0 |
| R125-R134 | Proceeds per Share block | FORMULA | per share class |

R72 is the primary input — override to model different exit multiples per round. R73 is formula but INPUT-colored; raw dollar exit values can be typed directly.

The waterfall assumes 1x non-participating preferred, latest round senior (reverse chronological), and common + options pari passu. No participating preferred, no caps, no anti-dilution. Each per-class row (R77-R83, R101-R107) uses `if(preference > pro-rata share, take preference, convert)` logic.

### Investor Return Summary (R136-R162)
Ties it all together for the modeled Investor.

| Row | Label | Type | Default |
|-----|-------|------|---------|
| R138 | Investment per Share, for Investor | FORMULA | $ invested / shares issued |
| R139 | Proceeds per Share, for Investor | FORMULA | from waterfall |
| R140 | Proceeds per Company, if exited per stage | FORMULA | sum across all share classes owned |
| R141 | Average total invested per type of company | INPUT at C141; FORMULA elsewhere | cumulative weighted invested |
| R142 | Total Proceeds, by type of exit | FORMULA | R140 × R68 |
| R143 | % of Total Proceeds, by type of exit | FORMULA | R142 / sum(R142) |
| R144 | Gross Return Multiple, if exit at each stage | FORMULA | R140 / R141 |
| R147-R153 | Gross Multiple per round block | FORMULA | if invested through row-round and held to column-round |
| R156-R162 | Expected Value per round block | FORMULA | R147-R153 × exit probability; K column is total EV |

K156-K162 is the money number: total expected value per $1 invested at each entry round. Default model shows K156 = ~3.08x EV for Seed entry, declining to ~1.25x at Series F+.

## Simple Venture Valuation (A1:AB46) — Single-Page Evaluator

A deliberate shortcut. No round-by-round cap table, no graduation chains. One investment, one Exit column per breakpoint (D-H = 5 exit scenarios), one probability row.

### Inputs (R8-R23)
| Row | Label | Type | Default |
|-----|-------|------|---------|
| R8/D8 | Total Liquidation Preferences, pre-investment ($) | INPUT | $1M |
| R11/D11 | Amount invested in modeled round, Investor ($) | INPUT | $500k |
| R11/E11 | Round date | INPUT (date) | today − 4 years (dummy) |
| R12/D12 | Amount invested in modeled round, All others ($) | INPUT | 0 |
| R13/D13 | Premoney Valuation ($) | INPUT | $6M |
| R14/D14 | Postmoney Valuation | FORMULA | sum of R11-R13 |
| R15/D15 | Ownership %, Investor, post-investment | FORMULA | D11 / D14 |
| R18/D18 | Additional invested, Investor ($) | INPUT | 0 |
| R18/E18 | Additional round date | INPUT (date) | today − 1.5 years (dummy) |
| R19/D19 | Additional invested, All others ($) | INPUT | $3M |
| R20/D20 | Additional ownership % purchased, Investor | INPUT (%) | 0% |
| R21/D21 | Dilution from Additional, All Other Investors | INPUT (%) | 30% |
| R22/D22 | Dilution from Additional Option Pools | INPUT (%) | 20% |
| R23/D23 | Ownership %, post-all investment | FORMULA | D20 + (1−D21) × D15 × (1−D22) |

R20-R22 are explicit shortcuts — instead of modeling each follow-on round, you specify total dilution from others and from options. The comment on R20 says: "intentional shortcut, to not need to model each individual investment round."

### Exit Breakpoints (R25-R32)
Columns D-H are 5 exit price breakpoints built automatically from the liquidation preference stack.

| Row | Label | Type | Default |
|-----|-------|------|---------|
| R26 | Exit Price ($) | FORMULA (INPUT-colored) | Auto-built: D=sum(R18,R19), E=+R11+R12, F=+R8, G=F×3, H=G×3 |
| R27 | Liquidation Preferences | FORMULA | cumulative preference stack |
| R30 | Proceeds from LP (additional invested) | FORMULA | LP share of investor's follow-on at below-preference exits |
| R31 | Proceeds from LP (modeled round) | FORMULA | LP share of investor's original round |
| R32 | Proceeds from Distributions to Common | FORMULA | max(0, exit − total LP) × R23 |
| R33 | Total Proceeds to Investor | FORMULA | sum R30:R32 |
| R35 | Gross Multiple | FORMULA | R33 / (R11 + R18); equivalent to MOIC |
| R36 | Probability of Exit (per column) | INPUT (%) | 0/0/0/0/100% (all weight on highest exit by default) |
| R37 | Expected Proceeds to Investor | FORMULA | sumproduct(R33, R36) |
| R38 | Expected Gross Multiple | FORMULA | R37 / total invested |
| R39 | Expected Gross IRR | FORMULA | xirr on R42:D44 |

R26 default formula chain creates the first 3 breakpoints at key preference points (additional only, + modeled round, + pre-existing), then extrapolates 3x multiples above. Override any cell to set specific exit dollar values.

R36 is where scenario probability is assigned. H36 is a formula (`=1−sum(D36:G36)`) so the row always sums to 100%.

### IRR Support Block (R41-R44)
Three-line cash-flow table used by XIRR in R39. R42 = initial investment (negative), R43 = follow-on investment (negative), R44 = expected proceeds (positive). Dates come from R11, R18, and R39 respectively.

## Resources (A1:F27)
Reference links to other Foresight/Hemrock VC models and third-party resources (Tactyc, Causal, OpenVC, Eniac, AngelList, VC Method). Informational only. Safe to hide.

## Model Comparison (A1:V22)
Feature matrix comparing this tool against the rest of the Foresight/Hemrock VC template lineup. Columns = features (Portfolio Forecast, Fund Performance Metrics, Individual Investment Evaluation, etc.). For this tool (R17), only **Individual Investment Evaluation** is true. Informational. Safe to hide.

## Changelog (B1:D11)
4 entries. v1.0.0 (2023-02-08) → v1.1.2 (2024-03-29). Notable: v1.1.1 added the Simple Venture Valuation sheet; v1.1.2 refined its liquidation preferences and breakpoints. Version history — keep hidden, not deleted.

## Key characteristics
- **Dual-mode**: full round-chain model on Venture Valuation, single-page breakpoint evaluator on Simple Venture Valuation. Pick one.
- **Perspective**: models one investor's returns through one average investment, not a whole fund. For fund-level math use the Venture Capital Model or Fund Economics Tool.
- **Requires iterative calculations** on the full sheet (R56 option pool is circular). Notice at E2: "Seeing a #REF error from a circular reference? Turn on iterative calculations."
- **Waterfall assumptions**: 1x non-participating preferred, latest round senior, no participation, no caps, no anti-dilution. For participating preferred or anti-dilution, use the Cap Table & Exit Waterfall Tool instead.
- **Graduation chain** (Venture Valuation R62-R68) is the core insight: probability of reaching each stage is multiplicative, so Seed-entry expected value weights heavily on early-stage failure.
- **Simple sheet uses shortcuts** instead of round-by-round follow-on: cumulative dilution from others (R21) and options (R22) are single percentages. Not exact, but fast.

## Notes
- Row 38 (`Total Investment Round`) on the full sheet is formula-driven from Premoney (R40) with a hard-coded 20%/80% split. Users wanting a specific $ round size must overwrite the formula. Consider flagging in primer.
- Simple Venture Valuation R39 uses `xirr(D42:D44, E42:E44)` — if the user adds more follow-on investments, the XIRR range does not auto-expand. The note on R39 flags this.
<!-- HEMROCK_SHEET_MAP_END -->
