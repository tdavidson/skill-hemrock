# Task prompts — Standard Financial Model

## Orientation

### Explain the model structure

Walk me through the sheets in this model and explain what each one does and how they connect to each other. Start with what I should look at first.

### Find all input cells

Look at the Get Started and Forecast sheets. List all of the blue input cells (blue font, grey background) that I need to fill in to get the model running. Group them by category.

### Explain a specific formula

Explain what the formula in [cell reference] is doing, and why it might be structured that way. Do not change it — just help me understand it.

## Revenue

### Configure revenue model for my business

I run a [describe your business model, e.g. B2B SaaS with annual contracts]. Help me identify which revenue model type to select in Get Started, and which input assumptions I need to set up on Get Started and Revenues to accurately reflect my business.

### Debug blank or zero revenues

My revenue model is showing zero or blank revenues. Before touching any formulas, walk me through the most common reasons this happens in this model and which inputs I should check first on the Get Started sheet.

### Model multiple revenue streams

I have [X] distinct revenue streams: [describe each briefly]. Help me figure out how to model each one using the existing revenue structure. If any stream requires a custom row or BYOM approach, tell me before making changes.

### Set up churn and retention inputs

Help me set up the churn and retention inputs correctly for my business. My current monthly churn rate is approximately [X%]. Walk me through which inputs on Forecast or Get Started control this and what the downstream effect looks like on MRR and subscriber counts.

### Model seasonality

My business has seasonal revenue patterns — [describe briefly, e.g. strong Q4, slow summer]. Show me where seasonality inputs live in this model and how to set them without breaking the underlying growth rate logic.

## Expenses

### Set up hiring plan

I want to model my hiring plan. I currently have [X] employees and plan to hire [describe roles and timing]. Walk me through how to enter this on the Forecast sheet, and confirm which rows are inputs vs. calculations before I start.

### Add a new expense line

I need to add [describe expense] to the model. Before adding a new row, tell me if there is already a place for this type of expense in the Forecast sheet. If I do need to add a row, explain exactly where to add it and what category (SG&A or COGS) to assign it to.

### Model CAPEX and depreciation

I have a significant capital expenditure coming up: [describe amount and timing]. Help me enter this correctly so that the model handles depreciation automatically. Which cells on Forecast are the right inputs?

## Fundraising

### Model a funding round

I am planning to raise [amount] at a [pre-money / post-money] valuation of [amount]. Help me enter this into the model correctly — which inputs on Get Started or Forecast control funding events, and how does the model reflect the cash inflow and dilution?

### Calculate runway to next raise

Based on the current inputs in the model, what is my projected runway — in months — before I need to raise again or reach profitability? Walk me through how the model calculates this and which assumptions have the biggest impact on it.

### Model different funding scenarios

I want to model two scenarios: one where I raise [amount] in [month], and one where I extend runway by cutting costs instead. Help me set up a simple way to compare both scenarios using the existing model structure without creating a second copy of the model.

## Analysis

### Explain unit economics

Walk me through the unit economics in this model — specifically CAC, LTV, payback period, and gross margin. Where do these metrics come from in the model and which inputs drive them most?

### Identify key value drivers

Looking at the inputs in this model, which three to five assumptions have the biggest impact on my cash runway and net revenue? Help me identify them so I can focus my planning on what matters most.

### Compare budget to actuals

I want to enter my actual financials from [month/period] to create a budget vs. actual comparison. Which cells on the Forecast or Budget sheet accept actuals, and how does the variance calculation work?

## Presentation

### Prepare model for investors

I am preparing to share this model with investors. Without modifying any calculation cells, help me identify: (1) any assumptions that need a note explaining the rationale, and (2) which sheets I should include or hide before sending. Do not delete any sheets — suggest hiding only.

### Summarize the model in plain language

Based on the inputs and outputs currently in this model, summarize in plain language: revenue trajectory over 3 years, gross margin trend, cash burn, runway, and the key assumptions driving those numbers. Write it as I would explain it to a non-technical investor.

## Customization

### Extend the time period

I want to extend the model's time period from [current period] to [desired period]. Before touching any columns, explain how the time period is set up in this model and the safest way to extend it without breaking downstream formulas.

### Add a business segment

I want to track a separate P&L for [business segment or product line]. Help me understand how the Breakdown sheet works and how to tag my expense and revenue lines to this segment.
