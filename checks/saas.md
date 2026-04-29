# Sanity checks — SaaS Forecasting Tool


## Validate bookings vs billings vs revenue

For a specific period, walk me through the relationship between bookings, billings, and recognized revenue in this model. Confirm that bookings are signed contract value (TCV), billings are amounts invoiced in the period, and revenue is the recognized portion. If any two are equal, explain why — they should usually differ.

## Validate deferred revenue makes sense

Confirm that deferred revenue is being calculated correctly. Specifically: (1) annual-paid customers should generate deferred revenue at billing time that decays over the contract length, (2) monthly-paid customers should produce minimal deferred revenue, (3) deferred revenue should never go negative. Walk me through any month where one of these doesn't hold.

## Validate ARR and revenue relationship

Confirm that ending ARR equals ending MRR × 12, and that annual revenue is NOT equal to ARR — annual revenue should be the sum of monthly revenue across the year, which differs from ARR because of growth and churn during the year. If they are equal in the model, there is a logic error. Identify it.

## Audit Aggregate vs Pipeline mode separation

Confirm that the model is using ONE mode (Aggregate or Pipeline) per scenario, not both. If both modes are populated, total revenue may be double-counted. Walk me through which inputs are active in each mode and confirm the active mode reflects my actual business.
