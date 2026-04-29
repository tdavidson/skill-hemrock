# Task prompts — Venture Capital Model — Quarterly Forecast

## Orientation

### Explain the fund model structure

Walk me through the sheets in this fund model. Which sheets contain the main inputs, which contain the cash flow calculations, and which contain the performance metrics? What order should I work through them to set up the model?

### Explain key fund metrics

Explain in plain language what TVPI, DPI, RVPI, IRR, and the J-curve mean, how they are calculated in this model, and how they relate to each other. Specifically: which are gross metrics and which are net metrics, and why does TVPI have to be lower than my gross exit multiple assumption?

## Fund Setup

### Set up fund parameters

Help me configure the core fund parameters. My fund details are: [fund size, vintage year, investment period, fund life, management fee structure, carried interest percentage, hurdle rate if any, GP commit if any]. Before entering any numbers, confirm which inputs on the assumptions sheet control each of these parameters and walk me through the order to fill them in.

### Configure management fee structure

Help me set up my management fee schedule correctly. My fee structure is: [describe, e.g. 2% on committed capital during investment period, then 2% on NAV thereafter]. Walk me through how the model calculates fees and confirm that invested capital (fund size minus fees) is being calculated correctly — not overstated.

### Model investment pacing

Help me set up the investment pacing assumptions. I expect to deploy capital over [X years], with approximately [describe pacing, e.g. $2M per quarter starting in Year 1]. Show me which inputs on the assumptions sheet control deployment timing and confirm the total invested capital ties back to fund size minus fees.

## Analysis

### Understand the waterfall

Walk me through how the carried interest waterfall is calculated in this model. Specifically: (1) what waterfall structure is being used (European vs. American), (2) at what point does the GP start receiving carry, (3) is there a hurdle rate, and (4) is carry calculated on gross proceeds or net of returned capital? Show me the logic before I validate the output numbers.

### Model different exit scenarios

I want to model fund performance under different gross exit multiple assumptions: [e.g. 2x, 3x, 5x gross]. Walk me through which inputs to change for each scenario and how TVPI, DPI, and IRR shift. Explain any non-linear effects I should be aware of.

### Explain the J-curve

My J-curve visualization doesn't look right. Walk me through how the J-curve should behave over a fund's life — when should IRR be negative, when should it turn positive, and what inputs most influence the shape of the curve? Then help me identify what might be causing it to look wrong.

## Portfolio

### Model portfolio construction

Help me set up my portfolio construction assumptions. I am targeting [X] investments at an average initial check size of [Y], with reserves for follow-ons of [Z% of fund]. Walk me through how the model handles initial investments and reserves, and confirm the total investment count and capital deployment ties back to investable capital.

### Add a GP commit

I need to add a GP commit of [X%] of fund size. Walk me through how a GP commit affects: (1) the fund's investable capital, (2) management fee calculations, (3) distributions and carried interest. Which inputs on the assumptions sheet control the GP commit?
