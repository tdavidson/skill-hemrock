---
name: hemrock-financial-modeling
description: Context, prompts, and sanity checks for editing Hemrock financial models. Covers the Standard Financial Model, Cap Table, Venture Fund Model (flagship + Quarterly Forecast), Fund Economics Tool, Venture Valuation, SaaS, Ecommerce, Unit Economics, and Runway. Point the AI at the template the user is editing; the skill supplies the sheet structure, task-specific prompts, and validation checks so edits match what the spreadsheet actually computes.
---

# Hemrock Financial Modeling

This skill gives you everything you need to edit a Hemrock financial model well:
the universal modeling context, per-template primers (sheet maps, conventions,
warnings), task-specific prompts, sanity checks, and best practices. Point at the
template the user is editing and apply the matching primer before touching cells.

## How to use this skill

1. **Identify the template.** Ask the user which Hemrock model they're editing. The identifiers are:

   - `standard` — Standard Financial Model
   - `cap_table` — Cap Table & Exit Waterfall Tool
   - `venture_fund` — Venture Capital Model (flagship)
   - `runway` — Runway & Cash Budget
   - `saas` — SaaS Forecasting Tool
   - `ecommerce` — Ecommerce Forecasting Tool
   - `unit_economics` — Unit Economics Tool
   - `fund_economics` — Fund Economics Tool
   - `fund_economics_tool_web` — Venture Capital Model — Web (Fund Economics Tool — Web)
   - `venture_valuation` — Venture Valuation Tool
   - `venture_fund_quarterly` — Venture Capital Model — Quarterly Forecast

2. **Load the matching primer.** Read `templates/<template>.md` for the sheet map, input/formula/output conventions, and anything specific to that model.

3. **Pull task prompts as needed.** If the user is doing a task (orientation, revenue, expenses, fundraising, analysis, presentation), read `prompts/<template>.md` and follow the task-specific guidance.

4. **Run the sanity checks.** Before handing back changes, run through `checks/<template>.md` (and `checks/universal.md`) to catch common AI failure modes: hard-coded values, broken references, confused metrics, hallucinated formulas.

5. **Consult best practices by topic** (`best_practices/<topic>.md`) when relevant: `formatting`, `structure`, `inputs`, `assumptions`, `review`, `sharing`.

## Universal modeling context

Apply this to any Hemrock template before the template-specific primer.

I am working on a Hemrock (formerly Foresight) financial model template created by Taylor Davidson (hemrock.com, formerly foresight.is). Before we start, here is how these models are structured:

FORMATTING CONVENTIONS:
- Blue font with light grey background = an input cell (assumption you can change). Only edit these.
- Black font = a formula or calculation. Do not modify these unless you fully understand the formula and its downstream effects.
- All cells and formulas are unlocked — there are no macros.
- Many cells have notes explaining what they do. Read them before changing anything.

SHEET STRUCTURE:
- README / License / Disclaimer: Informational only. Safe to ignore or hide.
- Get Started: Top-level model inputs and settings. Start here.
- Forecast: Detailed assumptions and inputs. A hybrid inputs-and-calculations sheet — treat blue cells as inputs, black cells as hands-off.
- Revenues: Revenue model calculations (Standard Model). Driven by inputs on Get Started and Forecast.
- Statements: Consolidated financial statements (income statement, balance sheet, cash flow).
- Summary / Key Reports / Breakdown / Budget / Sources and Uses: Presentation and analysis sheets. Output only — do not manually edit.
- Changelog: Version history. Do not delete.

CORE PRINCIPLES:
- Inputs, calculations, and presentations are intentionally separated. Never hard-code values into calculation or presentation sheets.
- All current assumptions are illustrative only — they are not market data or standards.
- The model is designed to be used iteratively, not as a static output.
- When in doubt, ask which cells are inputs before suggesting changes.

BEFORE MAKING ANY CHANGES:
1. Confirm with me which cells are blue (inputs) vs. black (calculations).
2. Tell me what downstream effects your proposed change will have.
3. Do not hard-code values into formula cells.
4. If a change requires modifying a formula, explain exactly what you are changing and why.

## If the user has the MCP server connected

The same content is available live via the Hemrock MCP server at `mcp.hemrock.com/mcp`. If you detect MCP tools like `get_context`, `get_prompts`, or `get_checks` are available, prefer those — they're always in sync with the source of truth. The skill is the fallback for users without the connector.

## File index

- `templates/` — one file per model with the template-specific primer and sheet reference
- `prompts/` — task-specific prompts per model (orientation / revenue / expenses / fundraising / analysis / presentation)
- `checks/` — sanity-check prompts per model, plus `checks/universal.md`
- `best_practices/` — cross-template guidance by topic
