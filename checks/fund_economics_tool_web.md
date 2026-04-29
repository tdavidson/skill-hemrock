# Sanity checks — Venture Capital Model — Web (Fund Economics Tool — Web)


## Confirm you're on the Web tool, not Excel

Before answering: am I working on the hosted Web tool at hemrock.com/p/venture-capital-model (tabs: Outputs, Fund Structure, Portfolio Construction, Expenses, Scenarios, Settings; auto-save; share links) or the Excel-based Fund Economics Tool (8 sheets, R-numbered cells)? They share fund-economics math but differ in surface, inputs, and feature set. State which one you're treating my question as.

## Validate the Scenarios tab layout

Confirm Scenarios is a single tab with two views toggled at the top: Named cases (3 columns: Conservative / Base / High, only large-tier multiple + share editable per column) and Simulation (per-investment lognormal draw with σ scaling on log(1 + multiple), histograms truncated at p99). If you're describing separate Scenarios and Monte Carlo tabs, you're describing the older Excel layout — correct yourself.

## Validate sub-row math on Portfolio Construction

On the Investment Strategy table, when a stage has % reserve > 0 it expands into Initial check + Follow-on N sub-rows. Confirm: editable inputs on the parent stage are name, % allocation, % reserve; editable inputs on the sub-rows are the per-row label, % of stage's reserves (sums to 100% across follow-ons), # of investments, and follow-on check size. The parent's 'Avg check' becomes a weighted average and is no longer directly editable when sub-rows are present.

## Validate share-link visibility behavior

Sharing has two modes. Public: URL alone grants read access. Private: URL plus an access code (shown to owner once on mint, hashed server-side, rotation invalidates everyone who already unlocked, 7-day unlock cookie keyed to the (token, code-hash) pair). Disabling clears the token and code. Confirm any advice you give about sharing is consistent with this model.

## Validate collaboration entitlement direction

Collaboration is owner-only paid: the model owner needs the $49/yr web_collaborate license to invite, but the invitee needs no license — receiving invites is free. Removing collaborators is always free, even if the owner's license has lapsed. Confirm any collaborator-related advice respects this — don't tell the invitee they need to buy something.
