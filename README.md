# Broker Recruiting Scorecard — CoStar Sale Comps

Internal tool for Foremost Commercial Real Estate. Turns weekly CoStar sale-comps exports into a
recruiting scorecard: an auto-scored, auto-organized Excel workbook the sales director uses to track
broker outreach, deal activity, and competitive positioning by market.

**Author / Maintainer:** BG ([e.eufracio@foremost-cre.com](mailto:e.eufracio@foremost-cre.com))
**Primary user:** Ryan, Sales Director

## What it does

- Ingests one or more CoStar sale-comps exports (`.xlsx`) and combines them into a single dataset.
- Auto-classifies every deal into a property-type **universe**: Industrial, Multifamily, Retail, and
  Office each keyword-group (any CoStar subtype or parenthetical — e.g. `Retail (Strip Center)`,
  `Office (CBD)` — collapses into the base type). Every other type (Flex, Land, Hospitality, ...)
  gets its own universe, also collapsing subsection parentheticals to one universe per base type.
- Scores every broker per universe and overall, using a configurable weighted formula (deal count,
  volume, average deal size).
- Builds a **Competitive Landscape** tab ranking brokerage *offices* (Firm × City) by production, so
  multi-office firms (e.g. CBRE, JLL) are compared office-to-office rather than blended into one row.
- Carries the director's touchpoint notes, broker emails, and phone numbers forward automatically
  week to week via a master ledger (`broker_recruiting_ledger.csv`) and the prior week's marked-up
  scorecard.
- Outputs a styled, protected Excel workbook: Dashboard, This Week & Month-to-Date, Top 100 Brokers,
  Competitive Landscape, one tab per universe, Review Queue, Broker Merges, and a READ ME tab.

## Requirements

- Runs in **Google Colab** (uses `google.colab.files` for the upload picker).
- To run outside Colab: install the packages in `requirements.txt` and replace the upload cell with
  local file paths — see the note at the top of `requirements.txt`.

```bash
pip install -r requirements.txt
```

## Weekly usage

1. Open the notebook in Colab and run **Runtime → Run all**.
2. When prompted, upload (you can select several files at once):
   - **CoStar export(s)** (`.xlsx`) — required, one or more (e.g. per city/region).
   - **Last week's `broker_recruiting_ledger.csv`** — carries deal history forward (skip on first run).
   - **Last week's marked-up scorecard** (`Broker_Recruiting_Scorecard.xlsx`) — carries the director's
     Status/Contacted/Notes forward (skip on first run).
3. Download the two output files when the run finishes:
   - `Broker_Recruiting_Scorecard.xlsx` — the scorecard for the director to review and mark up.
   - `broker_recruiting_ledger.csv` — the updated master ledger. **Save this** and upload it next run.

If a download doesn't start automatically, use the Colab **Files panel** (left sidebar) → `/content/`
→ right-click the file → Download.

## Repository structure

```
.
├── Broker_Recruiting_Scorecardv01.ipynb   # the notebook — config, engine, and run cells
├── requirements.txt                       # Python dependencies
├── LICENSE                                # proprietary — all rights reserved
└── .github/                               # issue/PR templates
```

Note: CoStar exports, generated scorecards, and ledger files are **never committed** to this repo —
see `.gitignore`. They contain broker contact information and should stay local or in your own
storage, not in git history.

## Contributing / workflow

This repo tracks work as GitHub Issues, one feature branch per issue, merged into `main` via PR. See
[CONTRIBUTING.md](CONTRIBUTING.md) for the full convention.

## License

Proprietary — all rights reserved. See [LICENSE](LICENSE). This tool is for internal use by Foremost
Commercial Real Estate only.
