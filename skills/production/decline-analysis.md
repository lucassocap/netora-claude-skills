# Skill: Decline Analysis

## When to Use

- Fitting DCA parameters to actual production data
- Reserve revisions and EUR updates
- Identifying wells that need intervention
- Validating type curve assumptions

## Prerequisites

- Well with at least 6 months of production history
- Current DCA parameters (optional — Claude can fit new ones)

## Prompt

```
Perform a decline curve analysis for well [WELL_NAME or WELL_ID].

1. Show current production history (last 12+ months)
2. Fit Arps DCA parameters to actual data (history match)
3. Compare original DCA forecast vs history-matched forecast
4. Calculate updated EUR based on matched parameters
5. Show remaining reserves (EUR - cum production)
6. If decline is steeper than expected, flag it and quantify the difference

Show original vs updated parameters side by side.
```

## What Claude Does

1. `list_production_records(well_id)` → historical data
2. `history_match(well_id)` → fit DCA to actuals
3. `compute_well_forecast(well_id)` → updated forecast
4. Compares and quantifies the difference

## Example Output

| Parameter | Original | History Matched | Change |
|-----------|----------|----------------|--------|
| qi (bopd) | 500 | 480 | -4% |
| di (/month) | 0.050 | 0.065 | +30% |
| b | 0.50 | 0.35 | -30% |
| EUR (MSTB) | 285.4 | 225.1 | -21% |

## Tips

- Ask "Should I update the well with the matched parameters?" — Claude can do it
- For wells declining faster, ask about "workover options" or "artificial lift evaluation"
- Compare decline rates across wells in the same field to spot formation-level trends
