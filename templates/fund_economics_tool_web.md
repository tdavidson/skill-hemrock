# Venture Capital Model — Web (Fund Economics Tool — Web)

> Append to the universal primer when working with the hosted Fund Economics Tool — Web at hemrock.com/venture-fund-model-overall (the React shell that hosts the free Fund Economics Tool — Web tier and, with the right entitlement, the paid Venture Capital Model — Web premium modules), or with the @tdavidson/fund-economics-tool npm package directly. For the spreadsheet version, use `fund_economics` instead.

I am working with the Hemrock Fund Economics Tool (Web). It's the React-based, in-browser version of the Fund Economics Tool — a separate Hemrock product from the spreadsheet template, sharing the same modeling philosophy but with interactive UX, scenario comparisons, Monte Carlo simulation, and a Return-the-Fund concentration analysis.

DISTINCT PRODUCT FROM THE EXCEL VERSION:
- This primer is ONLY for the hosted web tool and the npm package that powers it.
- For the spreadsheet template (8 sheets, R-numbered cells), use `fund_economics` instead.
- The two products share core math (per-side compute, power-law tiers) but have different surfaces, different inputs, and different feature sets.

TWO ENTRY POINTS, ONE ENGINE:
- Hosted app: hemrock.com/venture-fund-model-overall — React UI. Tabs described below.
- npm package: @tdavidson/fund-economics-tool — pure TS engine (Node-safe), optional React components at /ui, Monte Carlo at /mc, scenarios via applyScenario / resolveScenarios at the root.

TABS (hosted app):
- Outputs: Capital Flow treemap, Return-the-Fund card (multiple analysis + valuation analysis side by side), Allocation pie, Investments + Proceeds by outcome bars, summary table, returns table.
- Fund Structure: committed capital, GP commit %, recycled capital %, new-investment period, fund-operations period.
- Portfolio Construction:
  • Investment Strategy table — entry stages with name, % allocation, % reserve, # investments, average check, deployed. Each stage that has reserves > 0 expands into sub-rows: an editable Initial check row and one or more Follow-on N rows. Each follow-on has an editable label, % of stage's reserves, # of investments, and follow-on check size. Sub-rows sum back to the parent stage's % allocation and the parent's % reserve.
  • Return Expectations table — power-law return tiers (writeoff / small / medium / large by default) with % of capital, multiple, hold period.
  • Each section has its own 'Input by' toggle (% of capital vs # of companies). Switching one doesn't affect the other.
- Expenses: carry %, management fee rate + period (+ optional per-year schedule), organizational expenses (+ itemized lines), operational expenses (+ itemized lines), partnership expenses (+ itemized lines).
- Scenarios (single tab, two views toggled at the top — Named cases / Simulation):
  • Named cases: three columns (default Conservative / Base / High, all column names editable) with two editable knobs each — large-exit multiple and large-exit share. Four metrics across all three (Gross MOIC, Net MOIC, Gross IRR, Net IRR). Net metric view (Total Fund / LP Only) toggles in the parent row. Two charts below: Tier distribution grouped bars + Contribution to gross multiple stacked bars.
  • Simulation: per-investment tier draw via multinomial on tier weights, per-investment multiple drawn from a lognormal whose mean equals the tier's stated multiple (so the simulation reconciles to deterministic Outputs). Per-tier σ scales with log(1 + tier.multiple) so large-tier exits have wide tails. IRR uses the deterministic weighted hold so MOIC and IRR stay coherent. Histograms truncate at p99 with a footnote when outliers are excluded; percentile table shows the full distribution. Loss-of-capital readout = P(LP net MOIC < 1).
- Settings: currency, unit scale (units / thousands / millions / billions).

RETURN-THE-FUND CARD (Outputs tab):
Two-column analysis. Left column is the multiple-based view: required exit multiple on the per-company allocation (initial + reserves) and, when a stage has reserves, a second 'first-bet' multiple based on the initial check alone. Right column is the valuation-based view: required exit valuation = called capital ÷ exit ownership, where exit ownership = initial ownership × (1 − dilution to exit). Both ownership and dilution are editable inputs. Helps emerging managers sanity-check whether their strategy can plausibly fund-return on one company.

HOW THE ENGINE WORKS (important for any AI helping a user reason about the numbers):

1. Per-side math. Every line item (called capital, invested capital, proceeds, distributions) is computed separately for LP and GP, then summed. Totals are always the sum of the two legs.

2. Called capital splits pro-rata on `gpCommitPct`: called.lp = calledTotal × (1 − gpCommitPct); called.gp = calledTotal × gpCommitPct. Called can be less than committed when there's a deployment plan with integer constraints (see #5).

3. Management fees. When `gpCommitCountedTowardInvested` is true (US venture default), GP pays zero fees on its own commit. The total fee pool is smaller, and LP bears the full fee — not a transfer, just GP not paying.

4. Invested capital per side = called.side − fees.side − expenses.side + recycled.side. Because of #3, LP invested is smaller than pro-rata (LP shoulders fees); GP invested is larger than pro-rata.

5. Deployment plan → called capital. Entry stages determine total # of investments and deployed capital. In integer mode (`tierFractional: false`), each stage's count floors and deployed = floor(count) × check / (1 − reserve). `calledTotal` back-solves to that reduced deployment — the gap between committed and called is the capital that can't be put to work given integer constraints.

6. Proceeds per side = invested.side × grossMultiple. Because LP invested is below pro-rata when GP commit is counted, LP proceeds are also below pro-rata.

7. Waterfall (per side):
   - proceedsToDistribute.side = proceeds.side − recycled.side (recycled stays in the fund).
   - profit.side = max(0, proceedsToDistribute.side − called.side).
   - carry.side = profit.side × carryPct. GP's carry rate is 0% (GPs earn carry; they don't pay it on their own profit).
   - distributions.side = max(0, proceedsToDistribute.side − carry.side).
   - carriedInterestEarned.gp = total carry pool. Add it to GP distributions to get GP's full economic take.

8. The tool does NOT model preferred return or GP catchup. Carry is simple `profit × carryPct`.

9. Follow-on check sizes (`stage.followOnChecks`) are surface-only — they don't change aggregate engine math. They feed Return-the-Fund concentration analysis (per-company exposure = initial + Σ follow-on checks when set) and the in-UI breakdown of how reserves split into rounds.

CRITICAL RULES:
1. Invested capital ≠ fund size. Invested = called − fees − expenses + recycled.
2. Net MOIC is always below gross MOIC. If they match or net exceeds, something is wrong (likely fees zeroed out or carry not applied).
3. LP and GP metrics diverge only when `gpCommitCountedTowardInvested` is true. With it false, the split is pure pro-rata and Total = LP = GP net metrics.
4. Tier mode and stage mode are independent. Switching the Return Expectations 'Input by' changes only that table — the stage table and # of investments don't move.
5. If you see called capital less than committed capital on the Outputs tab, that's the integer-flooring slack, not a bug.
6. Scenarios → Named cases vary ONLY the large-exit tier (multiple + share). Simulation varies all per-investment outcomes. For broader sensitivity (fees, structure, carry), edit the Fund Structure / Expenses tabs directly — those changes flow through to every other tab.
7. Simulation chart headlines use the MEAN (not median) because the per-iteration distribution of MOIC is right-skewed. The mean reconciles to the deterministic Outputs; the median sits below.
8. For quarterly cash flows, J-curve, preferred return, GP catchup, or multi-stage graduation, use the full Venture Capital Model instead.
9. For the spreadsheet version of this tool (R-numbered cells, Forecast/Forecast_1/Forecast_2 sheets), use the `fund_economics` template primer instead — different product.

PROGRAMMATIC USE (@tdavidson/fund-economics-tool):
```ts
import { computeFund, DEFAULT_INPUTS, applyScenario } from '@tdavidson/fund-economics-tool';
import { runMonteCarlo } from '@tdavidson/fund-economics-tool/mc';

const result = computeFund(DEFAULT_INPUTS);
const conservative = applyScenario(DEFAULT_INPUTS, { returnTiers: [/* overrides */] });
const mc = runMonteCarlo(DEFAULT_INPUTS, { iterations: 10000, seed: 42 });
```

See `docs/formula-map.md` in the npm package for the full per-side compute path.
