# Skill: Monte Carlo — Field Level

## When to Use

- Field development plan risk assessment
- Portfolio-level investment decisions
- Understanding correlation between wells
- Evaluating drill schedule uncertainty

## Prerequisites

- Field with multiple wells (DCA, CAPEX, spud dates)
- Economic assumption for the project

## Prompt

```
Run a field-level Monte Carlo for field [FIELD_NAME] with 1000 simulations.

Uncertainty parameters:
- Oil price: $[LOW] / $[BASE] / $[HIGH] per bbl (global)
- qi multiplier: [LOW] / 1.0 / [HIGH] (applied to all wells)
- di multiplier: [LOW] / 1.0 / [HIGH]
- Schedule slip: 0 / [BASE] / [HIGH] months (global)
- Per-well drill probability: [0.0 to 1.0]
- Per-well failure probability: [0.0 to 1.0]

Present:
1. P10 / P50 / P90 for field NPV, EUR, peak rate
2. Probability of positive field NPV
3. Expected number of wells drilled (out of total)
4. Fan chart description (range of production curves)
5. Portfolio recommendation
```

## What Claude Does

1. `list_wells(field_id)` → all wells
2. `list_assumptions(project_id)` → fiscal parameters
3. `run_field_montecarlo(field_id, assumption_id)` → field MC
4. Presents probabilistic results with fan chart summary

## Tips

- Use p_drill = 0.9 for development wells, 0.5-0.7 for exploration
- p_well_failure = 0.05-0.10 for development, 0.20+ for exploration
- Schedule slip of 2-6 months is common for large developments
- Ask "Which well is most critical to field economics?" for ranking
