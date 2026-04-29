# Task prompts — Venture Capital Model — Web (Fund Economics Tool — Web)

## Orientation

### Explain the web tool structure

Walk me through the Venture Capital Model — Web at hemrock.com/p/venture-capital-model. What does each tab do (Outputs, Fund Structure, Portfolio Construction, Expenses, Scenarios, Settings)? Note that auto-save is on by default, the model picker in the header switches between owned + collaborator models, and Scenarios contains both Named cases and Simulation views.

### When to use this vs. the Excel version

I'm choosing between the hosted Web tool and the Excel-based Venture Capital Model. My goal is [describe: e.g. 'share with LPs', 'live editing with a co-GP', 'work offline on a flight', 'integrate with other spreadsheets']. Recommend which surface fits and why, accounting for share links, collaboration, and Excel's offline + statement coverage.

## Fund Setup

### Set up fund structure on the Web tool

Help me configure my fund on the Web tool. Details: [fund size, GP commit %, new-investment period, fund life, management fee %, fee period, carry %, recycled capital %]. Walk me through which tab each input lives on (Fund Structure for capital + structure, Expenses for fees + carry + line items). Confirm what the Outputs tab shows after I save.

### Build the investment strategy with reserves

My fund will deploy into [describe: e.g. 'Seed at $750k with 30% reserves split 60% into First Follow / 40% into Second Follow, Series A at $1.5M with no reserves']. Walk me through entering this in the Portfolio Construction → Investment Strategy table on the Web tool. Specifically: when I set % reserve > 0, the stage row expands into Initial check + Follow-on N sub-rows — show me how those sub-rows work (% of reserve column, # of investments, follow-on check size).

## Share

### Share a model with an LP read-only

Walk me through generating a share link from the model page header. Public mode is just a URL; private mode adds an access code that I see exactly once on mint and can rotate later (rotating invalidates everyone who already unlocked). Tell me when to use which mode, what happens when I disable a link, and how the recipient unlocks a private link.

### Send the share link by email

I want to email the share link directly from the tool. From the Share menu, click 'Send via email', enter the recipient + optional message, and the email goes from shares@mail.hemrock.com with reply-to set to my account email. For private mode, the access code I just minted is included in the email. Confirm the steps and tell me when this is preferable to copy-paste.

### Invite a collaborator

I want to invite [email] to actively edit my fund model alongside me. Walk me through the Collaborators menu: it requires the $49/yr web collaboration license on me as the owner; the invitee needs a Hemrock account but no license of their own. After I invite, what changes for them in their dashboard?

## Analysis

### Read the Scenarios → Named cases view

Walk me through what the Scenarios tab's Named cases view is showing. The Base column pulls from my current Fund Structure / Return Expectations. Conservative and High vary only the large-exit tier's multiple and its share of investments. The Net metric toggle (Total Fund / LP Only) flips the calc. Interpret the three Net MOIC / Net IRR outcomes for my fund.

### Read the Scenarios → Simulation view

On the Simulation view, walk me through what p5/p50/p95 mean for each metric. Per-investment tier is drawn multinomially on tier weights; per-investment multiple is drawn from a lognormal whose mean equals the tier's stated multiple (so the simulation reconciles to deterministic Outputs). Histograms truncate at p99 with a footnote when outliers are excluded. What does the loss-of-capital readout (P(LP net MOIC < 1)) tell me?

### Use Return-the-Fund analysis

On the Outputs tab, the Return-the-Fund card shows two views side by side: a multiple-based view (required exit multiple per company) and a valuation-based view (required exit valuation = called capital ÷ exit ownership). Walk me through both and show me what the assumed exit ownership and dilution-to-exit inputs are doing. Sanity-check whether my fund's strategy can plausibly fund-return on one company.
