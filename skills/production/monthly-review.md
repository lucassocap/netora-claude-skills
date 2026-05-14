# Skill: Monthly Production Review

## When to Use

- Monthly operations meeting
- Production surveillance
- Identifying wells underperforming vs forecast
- Spotting decline rate changes

## Prerequisites

- Wells with production records loaded
- DCA forecast params set (for actual vs forecast comparison)

## Prompt

```
Generate a monthly production review for field [FIELD_NAME] in project [PROJECT_NAME].

Include:
1. Current month production by well (oil, gas, water)
2. Month-over-month change for each well
3. Actual vs DCA forecast comparison (any well deviating >15%)
4. Decline rate analysis — any wells declining faster than expected?
5. Water cut trends — any wells with rising water cut?
6. Total field production summary
7. Wells requiring attention (shutdowns, underperformers)

Format as a surveillance report with a summary table and action items.
```

## What Claude Does

1. `list_wells(field_id)` → get all wells
2. For key wells: `list_production_records(well_id)` → latest data
3. `well_actual_vs_forecast(well_id)` → variance analysis
4. `well_decline_monitor(well_id)` → decline trends
5. Compiles into surveillance report

## Tips

- If no production data exists, Claude will tell you — add records first
- Ask for "last 6 months trend" for longer-term analysis
- Request "workover candidate list" to get actionable recommendations
