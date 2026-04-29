# Sanity checks — Fund Economics Tool


## Validate invested capital vs fund size

Confirm invested capital is fund size minus management fees minus fund expenses plus recycled capital — not equal to fund size. Show me each component (committed, fees, expenses, recycled) and the resulting invested number on both the Outputs summary table and the per-side breakdown.

## Validate LP vs GP net metrics diverge correctly

When `GP commit counts toward invested` is on (default), LP Net MOIC should be below Total Net MOIC (LP shoulders all fees → smaller LP invested → smaller LP proceeds). GP Net MOIC including earned carry should be much higher. Confirm the split looks right and explain the per-side chain.

## Validate called ≤ committed when in integer mode

If `Fractional companies` is off (integer mode), each stage's investment count floors, deployed capital shrinks, and called capital back-solves to the smaller deployment. Confirm called < committed, quantify the slack, and explain which stage(s) contributed most to the loss.

## Validate net vs gross metric distinction

Confirm Net MOIC is below Gross MOIC. Net = distributions / called; Gross = proceeds / invested. If Net ≥ Gross, something is wrong — probably fees or carry zeroed out. Trace through the waterfall (proceeds → less recycled → less carry → distributions) to find the break.

## Validate power-law return tiers

Confirm the model uses a return tier distribution (e.g. writeoffs / small / medium / large) rather than a single average multiple. Venture returns are power-law, so averaging hides the variance that drives net returns. If someone has collapsed to one tier with the mean multiple, the model understates dispersion.

## Validate scenarios vary only the large tier

The Scenarios tab only changes the large-exit tier's multiple and its share of investments (writeoff auto-plugs the gap). Confirm no other inputs are implicitly shifting between columns. If I want to sensitize fees or fund size, do it on the Fund Structure / Expenses tab — the Scenarios tab won't show those.

## Validate Monte Carlo assumptions

For the Monte Carlo run: (1) per-investment tier is drawn from the tier weights on Return Expectations; (2) each investment's multiple is lognormal around the tier's stated multiple with σ = [value]; (3) fees, structure, carry, stages stay fixed. Confirm that matches what I see, and flag if σ or iteration count seems off for the output variance I'm getting.

## Validate waterfall structure (simple carry, no pref)

This tool models simple carry: profit × carryPct per side, GP rate = 0%. No preferred return, no GP catchup. If I need a European waterfall with hurdle + catchup, this tool can't express it — use the Hemrock Venture Capital Model. Confirm that matches what my LPA requires.
