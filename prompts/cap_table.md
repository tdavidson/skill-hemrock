# Task prompts — Cap Table & Exit Waterfall Tool

## Orientation

### Explain the cap table structure

Walk me through the sheets in this cap table model. Which sheet contains the inputs, which contains the waterfall, and which shows the ownership summary? Tell me what order to work through them.

### Explain current ownership

Based on the current inputs in the model, summarize who owns what — shares, fully diluted ownership percentage, and implied value at the current valuation input — for each shareholder class. Present this as a clean table.

## Fundraising

### Model a new equity round with SAFE conversions

I am closing a new equity round. Here are my details: [provide existing cap table summary, SAFE details including type/cap/discount, new round amount and pre-money valuation, option pool changes]. Before calculating anything, confirm you have all the inputs you need and clarify the conversion method for any pre-money SAFEs. Then walk me step by step through the share count and price per share calculation. Do not output a final number until you have shown me the intermediate calculations.

### Calculate price per share

I need to calculate the price per share for a new equity round. Pre-money valuation is [X]. My current fully diluted share count is [X] shares [and I have the following securities converting: list them]. Walk me through the correct denominator to use for the price per share calculation, step by step, before giving me the final number.

### Model option pool expansion

I need to expand my option pool as part of this round. The investor wants a [X%] post-money option pool. Help me calculate the pre-round share increase needed to hit that post-money target, and explain the dilution impact on founders and existing investors.

### Compare pre-money vs post-money SAFE conversion

I have both pre-money and post-money SAFEs converting in this round. Explain to me in plain language how their conversion mechanics differ, which investors bear the dilution from each type, and confirm how the model is handling each one before we run the calculation.

## Analysis

### Model an exit waterfall

I want to model what happens at an exit. My exit scenarios are: [list 2-3 exit valuations, e.g. $10M, $25M, $50M]. Walk me through the liquidation waterfall for each scenario — who gets paid first, at what amounts, and what is left for common shareholders. Show me the liquidation preference stack before calculating distributions.

### Calculate founder dilution across rounds

Walk me through founder dilution from founding to the current cap table — showing ownership percentage after each round, option pool creation, and SAFE conversion. Present this as a table showing pre-round and post-round ownership at each stage.

### Model a down round

I may need to raise a down round at a lower valuation. Explain what anti-dilution provisions are in play for my existing preferred shareholders, which anti-dilution method (broad-based weighted average, narrow-based, or full ratchet) the model is using, and what the impact on founder and common shareholder ownership would be.
