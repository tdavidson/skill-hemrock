# Sanity checks — Ecommerce Forecasting Tool


## Validate cohort math sums correctly

Confirm that total revenue in any given period equals the sum of revenue from every active cohort in that period. If you sum across cohorts and don't get the period revenue, there is either a missing cohort or a math error. Identify which.

## Validate LTV horizon and assumptions

Confirm the LTV calculation explicitly: (1) what time horizon is used, (2) what retention curve is assumed, (3) what gross margin is applied, and (4) is it discounted to present value? AI tools often produce LTV without stating these assumptions. Make all four explicit.

## Validate contribution margin includes all variable costs

Confirm contribution margin in the model includes COGS plus payment processing, fulfillment, and returns — not just COGS. If any of these variable costs are missing or set to zero, payback and LTV will be overstated. Identify any missing components.

## Validate retention curve shape

Look at the retention curve in the model. Does it follow a realistic shape (high decay early, flattening over time)? If retention is constant or increasing, that is implausible. Flag any cohort age where retention behaves unrealistically.
