# Cap Table & Exit Waterfall Tool

> Append to the universal primer when working on the Cap Table and Exit Waterfall Tool.

I am working on the Hemrock Cap Table and Exit Waterfall Tool. 12 sheets, instructional-grade cap table with copy-paste round extension.

SHEET MAP:
- Cap Table: Main working cap table. Pre-financing (cols B-H) | Proforma (cols J onward). Each round is a column block — copy-paste to the right to add rounds.
- Exit Waterfall: Proceeds distribution at various exit valuations. Seniority, preferences, participation, conversion.
- Exit Waterfall, with Convertibles: Same but includes unconverted SAFEs/notes in the distribution.
- Cap Table, with Anti Dilution: Same as Cap Table but adds per-investor anti-dilution protection (full ratchet, broad-based weighted average, narrow-based).
- Cap Table, Issuing Equity: Isolated example of adding an equity round.
- Cap Table, Issuing Options: Isolated example of option grants.
- Cap Table, Converting SAFEs and Notes: Isolated example of SAFE/note conversion mechanics.
- Glossary: Terminology reference.

CAP TABLE STRUCTURE (per round block):
- R7-R8: Column headers — Shareholder, Common Shares, Preferred Shares, Options, Issued & Outstanding, % I&O, Fully Diluted, % FD | Investment, Actual Investment, Preferred Issued (conversion/new), Options Authorized, Transfers, Recategorizations
- R9: 'Common' section header
- R10-R14: Shareholder rows (INPUT: names in col A, share counts in col B). Default: R10 = 'Shareholder' with 10,000,000 common
- R16-R19: Options and RSUs section. R19 = Option Pool (INPUT)
- R21-R26: Preferred shareholder rows (INPUT)
- R28-R33: Convertible Notes and SAFEs rows (INPUT: investment amount, cap, discount, type — pre/post-money SAFE, convertible note)
- R35-R36: Totals (FORMULA)
- R38-R48: Round Details — R39: Pre-money Valuation (INPUT), R40: Investment Amount (INPUT), R41: Post-money (FORMULA), R42: Price per Share (FORMULA)

EXIT WATERFALL STRUCTURE:
- R5-R6: Exit valuation scenarios (INPUT: enter different exit values across columns)
- R8-R15: Liquidation Preferences — per-investor preference amounts and multiples (INPUT)
- R17-R30: Proceeds Distribution — seniority/pari passu ordering, preference payouts, participation, remaining to common (FORMULA)
- R32: Total distributed (FORMULA — must equal exit valuation)
- R34: Per-share proceeds by class

TO ADD A NEW ROUND: Select the entire column block for a round (from pre-financing through proforma), copy, paste to the right. Update the round-specific inputs (valuation, investment, convertible terms).

CRITICAL RULES:
1. Pre-money vs post-money SAFEs convert differently. Pre-money SAFEs: conversion price = valuation cap / pre-money fully diluted shares. Post-money SAFEs: conversion price = valuation cap / post-money shares (including the SAFE itself). Never treat them interchangeably.
2. Price per share (R42) is a FORMULA. Never hard-code it. The denominator must be exactly right.
3. Small errors in share counts cascade into wrong prices for every security. Audit step by step.
4. Option pool: pre-round vs post-round creation has different dilution implications. The model handles both — check the round details.
5. Anti-dilution: the 'with Anti Dilution' sheet has per-investor protection type and trigger logic. Full ratchet, broad-based weighted average, and narrow-based weighted average produce different outcomes.
6. Iterative calculations may be needed. If you see circular reference warnings, enable iterative calculation (Excel: Preferences > Calculation; Sheets: File > Settings > Calculation).

<!-- HEMROCK_SHEET_MAP_START -->
## Sheet Reference (auto-generated, do not edit by hand — see _models/)

# Cap Table and Exit Waterfall Tool Sheet Map

## Sheets
README, License, Cap Table, Exit Waterfall, Exit Waterfall (with Convertibles), Cap Table (with Anti Dilution), Cap Table (Issuing Equity), Cap Table (Issuing Options), Cap Table (Converting SAFEs and Notes), Resources, Glossary, Changelog

## Cap Table Sheet

### Structure
Two side-by-side blocks: the pre-financing cap table (cols B-I) and the proforma cap table for the new round (cols K-V). Each round is a column-block you copy-paste to the right to add the next round. The share-class rows (rows 9-34) are shared by both blocks.

Shared columns B-I: Shareholder (B), Common Shares (C), Preferred Shares (D), Options (E), Issued and Outstanding (F), % I&O (G), Fully Diluted Shares (H), % Fully Diluted (I).

### Share-class rows (the left block)
- **R9 Common** header; R10-R14 common shareholder rows (INPUT: name in col B, shares in col C; default R10 = 10,000,000 common)
- **R16 Options and RSUs** header; R17 issued and outstanding, R18 shares available for issuance, R19 new shares reserved (the option pool)
- **R21 Equity Investors (from Convertibles)** header; R22-R25 converted SAFE/note rows (FORMULA, pulled from the conversion block)
- **R27 Equity Investors** header; R28-R32 new-round investor rows (INPUT)
- **R34 Total**

### Proforma columns (the new round, cols K-V)
What the round does to each row: Investment (K, INPUT), Actual Investment after share rounding (L), Preferred Shares Issued from conversion (M), Preferred Shares Issued from new investment (N), Options Authorized from new options (O), Common / Preferred / Options Transferred or cancelled (P-R, optional), then the resulting Common / Preferred / Options / I&O (S-V).

### Round Details (col M, rows 36-41)
Total Investment (M37, sum of the round), Premoney Valuation (M38, INPUT assumption, default $10M), Postmoney Valuation (M39, FORMULA), Company Capitalization (M40, the ownership denominator), Price per Share (M41, FORMULA), with the share-rounding method and option-pool target nearby.

### Key Input Cells
- Existing shares: cols C/D/E on the share-class rows
- New investment amount: col K on the investor rows (R28-R32)
- Premoney valuation: M38
- Option pool: R19 and the option-pool target in the round details
- Convertible terms (cap, discount, type) on the conversion block

### Formulas to Never Touch
- Price per share (M41), Postmoney valuation (M39), Company Capitalization (M40)
- Fully diluted counts (col H), ownership percentages (cols G, I)
- The resulting proforma columns (S-V)
- SAFE and note conversion calculations

## Exit Waterfall Sheet

### Structure
One row per share class, one column per exit-price breakpoint. The model runs proceeds down the preference stack and out to common, at a series of increasing exit values.

### Share classes (R23-R37)
Series J down to Seed (preferred), then Common (R34), two Options rows (R35-R36), and Warrants (R37). Inputs per class, across the columns:

| Col | Field | Type |
|-----|-------|------|
| D | Type (Preferred / Common / Options / Warrants) | DROPDOWN |
| E | Seniority (drives the preference-stack order) | INPUT |
| F | Amount Invested | INPUT |
| G | Shares | FORMULA (invested ÷ price; direct INPUT for common/options) |
| H | Conversion Ratio, preferred to common | INPUT (default 1.0) |
| J | Price per Share, or strike price for options/warrants | INPUT |
| L | Liquidity Pref Multiple (multiple of amount invested) | INPUT (default 1.0) |
| M | Liquidity Preferences (= F × L, plus dividends) | FORMULA |
| O | Preferred Participation Rights (non-participating / participating / capped) | DROPDOWN |

R39 is Total shares.

### Distributions to Equity (R41-R47)
R42 Exit Price is a row of breakpoints across cols D-J, auto-built from the preference stack so each step adds the next preference layer; override any cell to set a specific exit value. Then Repayment of Debt (R43), Repayment of Convertibles (R44), Proceeds from Options (R45), Distributions to Equity (R46), and Breakpoint # (R47).

### Liquidation Preferences by seniority (R49 onward)
One row per class, in seniority order (col E drives it), each column computing that class's preference payout at that exit price. Below this the waterfall continues with the conversion decision per class (convert to common versus take the preference), participation, distributions to common, and finally proceeds per share by class.

### Key Input Cells
Per class: Amount Invested (F), Price per Share (J), Conversion Ratio (H), Liquidity Pref Multiple (L), Participation Rights (O), and Seniority (E). Exit prices on R42, or let them auto-build.

### What it can and cannot do
From the sheet's own notes (R5-R19): it handles many preferred classes, participating and non-participating preferred, different preference multiples, a multi-class preference stack, share-class sub-classes, cashless warrants, options at different strikes, preferred dividends, and preferred-to-common conversion ratios. It does not test for unconverted convertibles paying out as debt; use the convertibles version below for that.

## Exit Waterfall, with Convertibles Sheet
Same layout as the Exit Waterfall, with one addition: it calculates proceeds to unconverted SAFEs and notes (item 11 on the can-do list). Use this when convertibles might not convert before the exit.

## Cap Table, with Anti Dilution Sheet
The Cap Table sheet plus a Warrants line (R20) and anti-dilution mechanics: protection type per investor (full ratchet, broad-based or narrow-based weighted average), the trigger calculation when a down round occurs, the adjusted conversion price, and the additional shares issued as a result.

## Instructional Sheets
Stripped-down single-purpose examples, each showing one mechanic in isolation:
- **Cap Table, Issuing Equity** (R2-R23): common plus new equity investors only, no options or convertibles. A priced round at its simplest.
- **Cap Table, Issuing Options** (R2-R28): common, an Options and RSUs block, and equity investors. Option grants and pool mechanics.
- **Cap Table, Converting SAFEs and Notes** (R2-R29): common, equity investors from convertibles, and new equity investors. Conversion mechanics on their own.
<!-- HEMROCK_SHEET_MAP_END -->
