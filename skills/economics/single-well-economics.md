# Skill: Single Well Economics

## When to Use

- Pre-drill investment decision for a specific well
- AFE justification
- Quick sanity check on well-level returns
- Comparing well economics before/after parameter changes

## Prerequisites

- Well must exist in the platform with:
  - DCA parameters: `dca_qi`, `dca_di`, `dca_b`
  - CAPEX: `capex_usd`
- Project must have at least one Economic Assumption set

## Prompt

Copy and paste this into Claude:

```
Run a complete single-well economics analysis for well [WELL_NAME or WELL_ID].

Include:
1. Well parameters verification (DCA, CAPEX, OPEX)
2. DCA forecast summary (EUR, abandonment month)
3. Economics results:
   - NPV (at project discount rate)
   - IRR
   - Payout month
   - Breakeven oil price
   - Profitability Index
   - F&D cost ($/bbl)
4. Government take breakdown
5. Sensitivity analysis (tornado) — top 5 variables
6. NPV profile at multiple discount rates

Format as a professional report with tables.
```

## What Claude Does

1. Calls `get_well_detail(well_id)` to verify parameters
2. Calls `list_assumptions(project_id)` to get fiscal parameters
3. Calls `compute_well_economics(well_id, project_id)` to run the full analysis
4. Formats results into a structured report

## Example Output

| Metric | Value |
|--------|-------|
| EUR | 285.4 MSTB |
| NPV₁₀% | $4.2 MM |
| IRR | 32.5% |
| Payout | 18 months |
| Breakeven Price | $38.50/bbl |
| PI | 0.84 |
| F&D Cost | $17.54/bbl |
| Government Take | 52.3% |

## Tips

- If DCA params are missing, ask Claude to set them first: "Set DCA for well X: qi=500, di=0.05, b=0.5"
- For horizontal wells, typical qi is 300-1000+ bopd; for vertical, 100-500 bopd
- If you want a specific oil price, say so: "Use $80/bbl oil price"
- Ask "Compare this to industry benchmarks" for context
