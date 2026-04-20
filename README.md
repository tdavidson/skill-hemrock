# Hemrock Skill

> Context, prompts, and sanity checks for editing Hemrock financial models. Covers the Standard Financial Model, Cap Table, Venture Fund Model (flagship + Quarterly Forecast), Fund Economics Tool, Venture Valuation, SaaS, Ecommerce, Unit Economics, and Runway. Point the AI at the template the user is editing; the skill supplies the sheet structure, task-specific prompts, and validation checks so edits match what the spreadsheet actually computes.

This repository is the canonical source for the Hemrock Agent Skill — a drop-in package of financial-modeling context, prompts, and sanity checks for Claude.

**Canonical source:** this repository is generated from the Hemrock content site. Don't edit files directly — edit the prompt library upstream and re-publish.

## Install

### In Claude Projects
1. Clone this repo anywhere:
   ```bash
   git clone https://github.com/tdavidson/skill-hemrock.git ~/claude-skills/hemrock
   ```
2. Open [Claude.ai](https://claude.ai) → Projects → create or open a project.
3. Add every file under the `hemrock/` directory to the project's knowledge.
4. Tell Claude which Hemrock model you're editing (e.g. `I'm working on the cap_table template`) and it loads the matching primer automatically.

### In Claude Desktop or with the Claude Agent SDK
Reference this directory by path as a skill source per your client's docs.

### Updates
```bash
cd ~/claude-skills/hemrock
git pull
```

## What's in here

- `SKILL.md` — entry-point manifest + instructions
- `templates/` — per-model primers (sheet maps, conventions, warnings)
- `prompts/` — task-specific prompts per model
- `checks/` — sanity-check prompts per model + universal checks
- `best_practices/` — cross-template guidance by topic

## Models covered

- `standard` — Standard Financial Model
- `cap_table` — Cap Table & Exit Waterfall Tool
- `venture_fund` — Venture Capital Model (flagship)
- `runway` — Runway & Cash Budget
- `saas` — SaaS Forecasting Tool
- `ecommerce` — Ecommerce Forecasting Tool
- `unit_economics` — Unit Economics Tool
- `fund_economics` — Fund Economics Tool
- `venture_valuation` — Venture Valuation Tool
- `venture_fund_quarterly` — Venture Capital Model — Quarterly Forecast

## Alternative: live MCP server

If you want always-fresh content without cloning, the same data is exposed over MCP at `mcp.hemrock.com/mcp`. Skills and MCP can be used together — see [hemrock.com/mcp](https://www.hemrock.com/mcp) and [hemrock.com/skill](https://www.hemrock.com/skill).

## License

MIT — use freely.
