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

# Cap Table and Exit Waterfall Tool — Sheet Map

## Sheets
README, License, Cap Table, Exit Waterfall, Exit Waterfall (with Convertibles), Cap Table (with Anti Dilution), Cap Table (Issuing Equity), Cap Table (Issuing Options), Cap Table (Converting SAFEs and Notes), Resources, Glossary, Changelog

## Cap Table Sheet

### Structure
- Pre-financing cap table (cols B-H) | Proforma cap table (cols J onward)
- Each round is a column block that can be copy-pasted to the right to add rounds

### Row Map
- R5: Section header — "Pre-financing cap table" | "Proforma cap table"
- R7-R8: Column headers — Shareholder, Common Shares, Preferred Shares, Options, Issued and Outstanding, % I&O, Fully Diluted, % FD | Investment, Actual Investment, Preferred Issued (conversion), Preferred Issued (new), Options Authorized, Common Transferred, Preferred Transferred, Options Issued/Cancelled, Common, Preferred, Options
- R9: "Common" section header
- R10-R14: Shareholder rows (INPUT: names in col A, share counts in col B)
  - Default: R10 = "Shareholder" with 10,000,000 common shares
- R16: "Options and RSUs" section header
- R17: Options issued and outstanding (FORMULA)
- R18: Shares available for issuance (FORMULA)
- R19: Option pool (INPUT)
- R21: "Preferred" section header
- R22-R26: Preferred shareholder rows (INPUT)
- R28: "Convertible Notes and SAFEs" section header
- R29-R33: Convertible rows (INPUT: investment amount, cap, discount, type)
- R35: Totals section
- R36: Total shares (FORMULA)
- R38: "Round Details" section header
- R39: Pre-money valuation (INPUT)
- R40: Investment amount (INPUT)
- R41: Post-money valuation (FORMULA)
- R42: Price per share (FORMULA)
- R43-R48: Additional round mechanics

### Key Input Cells (per round block)
- Shareholder names: col A, R10-R14, R22-R26
- Share counts: col B (common), col C (preferred), col D (options)
- Convertible details: investment, cap, discount, type (pre/post money SAFE, note)
- Pre-money valuation: R39
- Investment amount: R40
- Option pool: R19

### Formulas to Never Touch
- Price per share (R42)
- Post-money valuation (R41)
- Fully diluted share counts (col G)
- Ownership percentages (cols F, H)
- Conversion calculations for SAFEs and notes

## Exit Waterfall Sheet

### Structure
- Exit valuation scenarios across columns
- Distribution flows top to bottom: preferences first, then participation, then common

### Row Map
- R2: Sheet title
- R5-R6: Exit valuation input row (INPUT: enter different exit values)
- R8: "Liquidation Preferences" section
- R9-R13: Per-investor preference amounts and multiples (INPUT: preference multiple, participation cap)
- R15: Total preferences (FORMULA)
- R17: "Proceeds Distribution" section
- R18-R30: Distribution waterfall — seniority/pari passu, preference payouts, remaining to common
- R32: Total distributed (FORMULA — should equal exit valuation)
- R34: "Per Share" section — proceeds per share by class

### Key Input Cells
- Exit valuations: R5-R6 across columns
- Liquidation preference multiples: per investor
- Participation: participating/non-participating, caps
- Seniority: senior/pari passu ordering

## Exit Waterfall with Convertibles Sheet
Same structure as Exit Waterfall but includes unconverted SAFEs and notes in the distribution.

## Cap Table with Anti Dilution Sheet
Same as Cap Table but adds:
- Anti-dilution protection type per investor (full ratchet, broad-based weighted average, narrow-based)
- Anti-dilution trigger calculations when a down round occurs
- Adjusted conversion prices and additional shares issued

## Instructional Sheets
- Cap Table, Issuing Equity: isolated example of adding an equity round
- Cap Table, Issuing Options: isolated example of option grants
- Cap Table, Converting SAFEs and Notes: isolated example of conversion mechanics
<!-- HEMROCK_SHEET_MAP_END -->
