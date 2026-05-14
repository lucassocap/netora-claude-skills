# Netora Claude Skills

> Turn Claude into your petroleum engineering co-pilot — connected to your Netora Upstream Platform data.

Netora Claude Skills is a ready-to-use kit that connects [Claude.ai](https://claude.ai) to the **Netora Upstream Platform** via MCP (Model Context Protocol). Once connected, Claude can read your projects, run economics, forecast production, simulate Monte Carlo risk, compare fiscal regimes across 8 countries, and generate executive reports — all through natural language.

## What Can Claude Do With Netora?

| Domain | Capabilities |
|--------|-------------|
| **Economics** | NPV, IRR, payout, breakeven, sensitivity tornado, government take |
| **Production** | DCA forecasting (Arps), EUR, type curves, actual vs forecast, decline monitoring |
| **Drilling** | Well plans, AFE cost breakdown, BHA validation, T&D, hydraulics, ECD |
| **Facilities** | Auto-generate equipment, Souders-Brown sizing, CEPCI costing |
| **Risk** | Monte Carlo (well & field level), P10/P50/P90, fan charts |
| **Fiscal** | 8-country regimes (USA, VEN, COL, ARG, BRA, PER, ECU, BOL) |
| **Reports** | 70+ report types — from one-pagers to full field development plans |

## Prerequisites

1. A **Netora Upstream Platform** account with API access
2. A **Claude.ai** Pro or Team subscription (MCP integrations require a paid plan)
3. Your Netora **API key** (get it from Settings > API Keys in the platform)

## Quick Setup (5 Minutes)

### Step 1 — Add MCP Integration in Claude.ai

Go to **Claude.ai Settings > Integrations > Add MCP Integration** and enter:

| Field | Value |
|-------|-------|
| **Name** | `Netora Upstream` |
| **URL** | `https://api-production-fa50.up.railway.app/api/ai/tools/mcp/` |
| **Authentication** | Bearer Token |
| **Token** | Your Netora API key |

### Step 2 — Create a Claude Project

1. In Claude.ai, create a new **Project** (e.g., "Netora E&P")
2. Paste the contents of [`system-prompt/netora-system-prompt.md`](system-prompt/netora-system-prompt.md) into the **System Prompt**
3. Upload all files from the [`knowledge/`](knowledge/) folder as **Project Knowledge**

### Step 3 — Start a Conversation

Open a new chat inside your project and try:

```
List all my projects and show me a summary of each one.
```

```
Run economics for well TJ-001 and show me NPV, IRR, and payout.
```

```
Compare the fiscal regime of Venezuela vs Colombia for a 5000 bopd field.
```

See [`examples/`](examples/) for complete walkthroughs.

## Repository Structure

```
netora-claude-skills/
├── setup/                  # Step-by-step setup guides
├── system-prompt/          # System prompts for Claude Projects (EN & ES)
├── knowledge/              # Files to upload as Claude Project knowledge
├── skills/                 # Copy-paste prompts organized by domain
├── examples/               # Complete end-to-end walkthroughs
└── CHANGELOG.md
```

## Skills Library

Ready-to-use prompts you can copy-paste into Claude:

| Domain | Skill | Description |
|--------|-------|-------------|
| Economics | [Single Well Economics](skills/economics/single-well-economics.md) | Full NPV/IRR/payout for one well |
| Economics | [Field Economics](skills/economics/field-economics.md) | Field-level economics with CAPEX schedule |
| Economics | [Sensitivity Analysis](skills/economics/sensitivity-analysis.md) | Tornado chart + breakeven price |
| Production | [Monthly Review](skills/production/monthly-review.md) | Production surveillance report |
| Production | [Decline Analysis](skills/production/decline-analysis.md) | DCA fit + EUR estimate |
| Drilling | [Well Plan Review](skills/drilling/well-plan-review.md) | Trajectory, casing, time & cost |
| Drilling | [Drilling Cost Estimate](skills/drilling/drilling-cost-estimate.md) | AFE buildup from drilling profile |
| Risk | [Monte Carlo Well](skills/risk/montecarlo-well.md) | Probabilistic economics (single well) |
| Risk | [Monte Carlo Field](skills/risk/montecarlo-field.md) | Field-level MC with drill probability |
| Fiscal | [Country Comparison](skills/fiscal/country-comparison.md) | Side-by-side fiscal regime comparison |
| Executive | [Investment Memo](skills/executive/investment-memo.md) | Board-ready investment summary |
| Executive | [Project Summary](skills/executive/project-summary.md) | One-page project overview |
| Data Entry | [Create Project](skills/data-entry/create-project.md) | Set up a new project from scratch |

## Knowledge Files

Upload these to your Claude Project for maximum accuracy:

| File | Content |
|------|---------|
| [01-tool-catalog.md](knowledge/01-tool-catalog.md) | All 170 tools organized by domain |
| [02-domain-glossary.md](knowledge/02-domain-glossary.md) | 200+ petroleum engineering terms |
| [03-workflow-reference.md](knowledge/03-workflow-reference.md) | 20 step-by-step workflows |
| [04-fiscal-regimes.md](knowledge/04-fiscal-regimes.md) | 8-country fiscal details |
| [05-report-catalog.md](knowledge/05-report-catalog.md) | 70 report types with data requirements |
| [06-data-model.md](knowledge/06-data-model.md) | Entity relationships and data flow |

## Troubleshooting

See [setup/TROUBLESHOOTING.md](setup/TROUBLESHOOTING.md) for common issues.

## License

MIT License — see [LICENSE](LICENSE).
