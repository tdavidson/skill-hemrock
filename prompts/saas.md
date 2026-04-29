# Task prompts — SaaS Forecasting Tool

## Orientation

### Explain the SaaS model structure

Walk me through this SaaS Forecasting Tool. Explain the difference between Aggregate and Pipeline modes, which sheets correspond to each, and which one I should use for my business based on my customer profile.

### Pick Aggregate or Pipeline

I have [describe your customer profile, e.g. 'mostly SMB self-serve customers with a few enterprise deals']. Help me decide whether to use Aggregate mode, Pipeline mode, or both — and explain how using both at the same time would double-count revenue if I'm not careful.

## Revenue

### Set up subscription tiers and pricing

I have [describe pricing tiers, e.g. '$50/mo Starter, $200/mo Pro, $1000/mo Enterprise']. Walk me through how to enter each tier into the model — which inputs on Get Started or Forecast control tier mix, conversion rates, and revenue per subscriber.

### Model annual vs monthly billing

Some of my customers pay monthly and some pay annually upfront. Help me set this up correctly so the model handles deferred revenue and cash inflow timing accurately. Which inputs control billing cycle and how does it affect MRR, ARR, billings, and revenue?

### Add expansion revenue

I want to model expansion revenue (existing customers buying more). My net revenue retention is approximately [X%]. Show me where to enter expansion assumptions and how they flow through to MRR and ARR.

### Add a specific enterprise contract (Pipeline mode)

I'm closing [describe deal: e.g. '$120k annual contract, paid annually upfront, 2-year term, starts March']. Walk me through adding this to the Pipeline sheet and confirm how it shows up in bookings, billings, deferred revenue, and recognized revenue.

## Analysis

### Compare bookings, billings, and revenue

For [specific month or quarter] in my forecast, show me the difference between bookings, billings, and recognized revenue. Explain why they differ in plain language so I can confidently answer this in an investor meeting.

### Build an MRR build chart

Help me build an MRR walk for [period]: starting MRR + new MRR + expansion MRR − contraction MRR − churned MRR = ending MRR. Pull each component from the model and confirm the math ties to the ending MRR shown in the Forecast sheet.

### Estimate LTV at different churn levels

Show me how LTV changes if monthly churn moves from [current %] to [scenarios, e.g. 3%, 5%, 8%]. Walk me through the calculation and explain why LTV is so sensitive to small churn changes.
