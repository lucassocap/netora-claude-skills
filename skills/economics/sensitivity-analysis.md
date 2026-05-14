# Skill: Sensitivity Analysis

## When to Use

- Identify key value drivers for investment decisions
- Understand which variables matter most to NPV
- Determine breakeven conditions
- Risk communication to management

## Prerequisites

- Completed economics run (well or field level)
- Economic Assumption set with defined parameters

## Prompt

```
Run a sensitivity analysis for well [WELL_NAME or WELL_ID].

Show me:
1. Tornado chart — ±20% swing on: oil price, CAPEX, OPEX, fixed OPEX, royalty, tax, discount rate, IHI
2. Rank variables by NPV impact (highest to lowest)
3. Breakeven oil price where NPV = 0
4. NPV profile at discount rates: 0%, 5%, 8%, 10%, 12%, 15%, 20%, 25%, 30%
5. Key insight: which variable is the single biggest risk?

Format the tornado as a table with Low NPV, Base NPV, and High NPV columns.
```

## What Claude Does

1. Runs `compute_well_economics(well_id, project_id)` which includes sensitivity
2. Extracts the `sensitivity` and `npv_profile` sections
3. Sorts variables by impact and presents as tornado

## Example Output

| Variable | -20% NPV (MM) | Base NPV (MM) | +20% NPV (MM) | Impact (MM) |
|----------|---------------|---------------|---------------|------------|
| Oil Price | $1.8 | $4.2 | $6.6 | $4.8 |
| CAPEX | $5.2 | $4.2 | $3.2 | $2.0 |
| OPEX | $4.8 | $4.2 | $3.6 | $1.2 |
| Royalty | $4.7 | $4.2 | $3.7 | $1.0 |
| Tax Rate | $4.6 | $4.2 | $3.8 | $0.8 |

**Breakeven Oil Price:** $38.50/bbl

## Tips

- If you want custom swing percentages, say "±30% sensitivity" or "±10%"
- Ask for "spider chart" to see how NPV changes continuously with each variable
- For field-level sensitivity, use the field economics prompt first
