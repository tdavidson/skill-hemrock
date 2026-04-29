# Sanity checks — Venture Capital Model (flagship)


## Validate invested capital vs fund size

Confirm that invested capital in the model is correctly calculated as fund size minus total management fees and fund expenses — not equal to fund size. Show me the total management fees, total expenses, and resulting investable capital as a sanity check.

## Validate TVPI is net, not gross

Confirm that TVPI in the model is a net metric — calculated on paid-in capital after management fees and carry — and is lower than the gross exit multiple assumption. If TVPI is equal to or higher than the gross exit multiple, there is a logic error. Identify where it is coming from.

## Validate the waterfall carry calculation

Walk me through the carry calculation in the model step by step: (1) total distributions to LPs before carry, (2) return of capital, (3) hurdle (if applicable), (4) catch-up (if applicable), (5) carry split. Confirm carry is calculated on net profits after return of capital — not on gross proceeds.

## Validate NAV reaches zero at fund end

At the end of the fund's life, confirm that NAV (net asset value / unrealized value) reaches zero. If it does not, identify where the residual unrealized value is coming from and whether it represents an error or an intentional modeling choice.

## Validate J-curve uses IRR not cash flows

The J-curve chart should show IRR over time — negative in early years as fees are paid and investments are made, turning positive as exits occur. Confirm the J-curve is using IRR (or a proxy that approximates it), not cumulative net cash flows. If it is using cash flows, explain why the distinction matters.

## Flag AI-generated fund model errors

I received a fund model output from an AI modeling tool. Before I use it, audit the following common AI errors in fund modeling: (1) is invested capital correctly net of fees, (2) is TVPI net of fees and carry, (3) is the carry calculation applied to net profits not gross proceeds, (4) is the waterfall structure correct for a US venture fund (European whole-fund carry, no hurdle by default), (5) does NAV reach zero at fund end, (6) are sensitivity tables formula-based or hard-coded? Flag each one.
