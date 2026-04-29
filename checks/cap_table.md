# Sanity checks — Cap Table & Exit Waterfall Tool


## Audit share count math before accepting any calculation

Before I accept any share count or price per share output: walk me through the exact calculation of the fully diluted share count used as the denominator for the price per share. Show me every security type included and its share count. Confirm the total matches the model's output before we proceed.

## Validate SAFE conversion logic

I have [pre-money / post-money] SAFEs converting in this round. Walk me through the conversion calculation step by step, including which share count you used in the denominator. Confirm whether the conversion price is being set by the cap or the discount — and which one is investor-favorable in this scenario.

## Sanity check total ownership adds to 100%

After modeling this round, confirm that total ownership across all shareholder classes sums to exactly 100% on a fully diluted basis. If it does not, identify which class is causing the discrepancy.

## Validate waterfall at multiple exit values

Run the exit waterfall at three different exit valuations: [low], [mid], and [high]. For each, confirm: (1) total distributions equal the exit proceeds, (2) liquidation preferences are applied before common shareholders receive anything, and (3) participation caps (if any) are applied correctly. Flag any scenario where the math doesn't add up.

## Flag structural errors from AI-generated cap tables

I received a cap table or share count calculation from an AI tool. Before I use these numbers, audit them against the Hemrock Cap Table model. Specifically check: (1) is the price per share denominator correct, (2) are pre-money and post-money SAFEs treated differently, (3) does total ownership sum to 100%, and (4) does the option pool treatment match what was agreed.
