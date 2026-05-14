# Skill: Investment Memo

## When to Use

- Investment committee presentation
- Board approval for capital allocation
- Partner proposals
- Internal decision memos

## Prerequisites

- Project with economics and Monte Carlo results
- Or enough data for Claude to run them

## Prompt

```
Generate an investment memo for project [PROJECT_NAME].

Structure:
1. **Executive Summary** (3-4 sentences: what, why, how much, expected return)
2. **Project Overview** (location, operator, partners, stage)
3. **Key Metrics Table** (NPV, IRR, EUR, payout, PI, gov take, breakeven)
4. **Production Forecast** (peak rate, decline profile, EUR per field)
5. **CAPEX & Schedule** (total budget, phasing, key milestones)
6. **Fiscal Framework** (country, regime, government take)
7. **Risk Assessment** (P10/P50/P90 from Monte Carlo, key sensitivities)
8. **Recommendation** (invest / conditional / pass — with justification)

Use data from the platform. Run any missing analyses as needed.
Keep the tone professional and suitable for a board presentation.
```

## What Claude Does

1. `get_project_full_data(project_id)` → complete snapshot
2. `run_field_economics(field_id, assumption_id)` → per-field economics
3. `run_field_montecarlo(field_id, assumption_id)` → risk assessment
4. Compiles all data into structured memo format

## Tips

- Add "in under 2 pages" for concise memos
- Ask for "risks and mitigations" section for balanced presentation
- Request "comparable transactions" for M&A context
- "Include a decision matrix" for multi-project comparisons
