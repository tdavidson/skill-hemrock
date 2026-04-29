# Task prompts — Fund Economics Tool

## Orientation

### Explain the tool structure

Walk me through the Fund Economics Tool. What does each tab do (Outputs, Fund Structure, Portfolio Construction, Expenses, Scenarios, Monte Carlo), and what order should I work through them to set up my fund?

### When to use this vs. the full VC Model

I'm trying to decide whether this Fund Economics Tool is enough for my use case or if I need the full Hemrock Venture Capital Model. My goal is [describe: e.g. 'pitch fund strategy to LPs', 'model quarterly capital calls', 'compare two fund strategies with preferred return']. Recommend which one to use and why.

## Fund Setup

### Set up fund structure and fees

Help me configure my fund. Details: [fund size, GP commit %, new-investment period, fund life, management fee %, fee period, carry %, recycled capital %]. Walk me through which tab each input lives on and what to watch for (especially `GP commit counts toward invested` and how that shifts LP vs GP net metrics).

### Build the investment strategy (entry stages)

My fund will deploy into [describe: e.g. 'Seed at $750k with 30% reserved for follow-ons, Series A at $1.5M with no reserves']. Walk me through how to set this up on the Portfolio Construction tab — stage names, % allocation per stage, reserve ratios, and whether to use % of capital or # of companies mode. Then confirm the number of investments that come out the other side.

### Build the return distribution (tiers)

My return expectations are [describe: e.g. '60% writeoffs, 20% return capital (1.5x), 10% good (5x), 10% home runs (32x)']. Walk me through entering this into the Return Expectations table and confirm the engine uses each tier rather than a blended average. If I want 20 total investments, show me the tier counts that result.

## Analysis

### Read the Scenarios tab

Walk me through what the Scenarios tab is showing. The Base column pulls from my current Fund Structure / Return Expectations inputs. Conservative and High vary only the large-exit tier's multiple and its share of investments. Interpret the three Net MOIC / Net IRR outcomes for my fund.

### Interpret the Monte Carlo output

On the Monte Carlo tab, walk me through what the p5/p50/p95 bands mean for each metric. In particular: what does the loss-of-capital probability represent, and how much should I trust it at [X] iterations with σ = [Y]? Flag any distribution that looks suspicious.

### Stress-test fees on net returns

Compare how LP Net MOIC and Net IRR change as I shift my management fee structure from [current, e.g. 2% flat for 10 years] to alternatives [e.g. 2% on committed for 4yr then 2% on invested for 6yr, 2.5% flat, etc.]. Walk me through the per-year fee schedule disclosure on the Expenses tab and confirm LP invested capital is recomputing correctly net of fees.

### Explain why LP and GP net MOIC differ

On the default inputs, LP Net MOIC is below Total Net MOIC and GP Net MOIC (including earned carry) is much higher. Walk me through why — specifically the fee asymmetry when GP commit is counted, how that reduces LP invested capital below pro-rata, and how carry flows to GP.
