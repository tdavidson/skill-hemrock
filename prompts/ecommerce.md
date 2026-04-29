# Task prompts — Ecommerce Forecasting Tool

## Orientation

### Explain cohort-based modeling

Walk me through how this Ecommerce Forecasting Tool models cohorts. Explain in plain language what a cohort is, how the model tracks each one separately, and why this differs from a simple aggregate revenue model.

### Walk through the retention curve

Show me where the retention curve is defined in the model. Explain how a customer's repeat purchase probability changes by cohort age, and which inputs control the shape of that curve.

## Revenue

### Set up acquisition assumptions

I plan to acquire [describe: e.g. '500 new customers per month growing 5% MoM, at $40 CAC']. Show me which inputs on Get Started control new customer volume and CAC, and confirm how the model translates that into revenue.

### Adjust the retention curve to match my data

I have actual repeat purchase data: [describe: e.g. '30% of new customers buy again within 90 days, 50% within a year']. Help me adjust the model's retention assumptions to match this and explain how the change flows through to revenue.

### Model average order value changes

I'm planning a [pricing change, bundle, or AOV initiative]. My current AOV is [$X] and I expect it to move to [$Y]. Show me which input controls AOV in the model and how the change affects total revenue and contribution margin per cohort.

## Analysis

### Calculate LTV at different horizons

Show me LTV calculated at 6-month, 12-month, and 24-month horizons. Explain why LTV at a longer horizon is higher, and what assumptions most influence the difference. Recommend which horizon I should use when discussing LTV externally.

### Find break-even on customer acquisition

At what point in a customer's lifetime does cumulative contribution margin equal CAC? Walk me through the payback calculation and identify whether the answer is months or transactions, and why.

### Project cohort revenue contribution

For a cohort acquired today, project total revenue contribution over the next [12, 24, or 36] months. Break it down between first-purchase revenue and repeat revenue so I can see the value of retention vs. acquisition.
