# Skill: Monte Carlo — Single Well

## When to Use

- Probabilistic investment decision for a single well
- Understanding range of outcomes (best/worst case)
- Communicating risk to management
- Determining probability of commercial success

## Prerequisites

- Well with DCA parameters and CAPEX set
- Economic assumption in the project

## Prompt

```
Run a Monte Carlo simulation for well [WELL_NAME or WELL_ID] with 1000 iterations.

Use these uncertainty ranges:
- qi: [LOW] / [BASE] / [HIGH] bopd
- di: [LOW] / [BASE] / [HIGH] per month
- oil price: $[LOW] / $[BASE] / $[HIGH] per bbl
- CAPEX: $[LOW]MM / $[BASE]MM / $[HIGH]MM
- OPEX: $[LOW] / $[BASE] / $[HIGH] per bbl

Present:
1. P10 / P50 / P90 for NPV, IRR, EUR
2. Probability of positive NPV (commercial success rate)
3. Mean NPV and standard deviation
4. Key risk: which variable drives the most uncertainty?
5. Decision recommendation: invest or pass?
```

**Example with typical values:**

```
Run Monte Carlo for well TJ-001 with 1000 simulations:
- qi: 350 / 500 / 700 bopd
- di: 0.03 / 0.05 / 0.08 per month
- oil price: $55 / $70 / $90 per bbl
- CAPEX: $4.0MM / $5.0MM / $7.0MM
- OPEX: $8 / $12 / $16 per bbl

Show P10/P50/P90, probability of positive NPV, and recommendation.
```

## What Claude Does

1. `get_well_detail(well_id)` → verify base parameters
2. `run_montecarlo(well_id)` with the specified ranges
3. Extracts P10/P50/P90, histograms, probability metrics
4. Generates risk assessment

## Example Output

| Metric | P10 | P50 | P90 | Mean |
|--------|-----|-----|-----|------|
| NPV (MM) | -$0.8 | $4.2 | $9.1 | $4.5 |
| IRR (%) | 5% | 32% | 68% | 35% |
| EUR (MSTB) | 180 | 285 | 420 | 295 |

**Probability of positive NPV: 82%**

## Tips

- Use ±30% of base case as a starting point for ranges
- For exploratory wells (high risk), use wider ranges and add p_drill < 1.0
- "Show me the histogram for NPV" — Claude can describe the distribution shape
- "What oil price makes this well uneconomic at P90?" — great question for risk assessment
