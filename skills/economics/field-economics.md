# Skill: Field Economics

## When to Use

- Field development plan economics
- Multi-well investment decision
- CAPEX phasing and production profile analysis
- Board-level field approval

## Prerequisites

- Field with multiple wells (each with DCA params and CAPEX)
- At least one Economic Assumption set for the project
- Preferably wells with spud_date set for CAPEX scheduling

## Prompt

```
Run field-level economics for field [FIELD_NAME] in project [PROJECT_NAME].

Include:
1. Field overview: well count, total CAPEX, average qi
2. Aggregated production forecast (peak rate, EUR)
3. CAPEX schedule (by month)
4. Field economics:
   - Field NPV and IRR
   - Total government take
   - Payout period
5. Per-well contribution (top/bottom performers)
6. Sensitivity analysis on oil price and CAPEX

Present as an executive summary with tables.
```

## What Claude Does

1. `list_fields(project_id)` → find field ID
2. `list_wells(field_id)` → verify well data
3. `list_assumptions(project_id)` → get assumption ID
4. `run_field_economics(field_id, assumption_id)` → full field analysis
5. Formats results with production profile and CAPEX schedule

## Tips

- For large fields (20+ wells), Claude may take 15-20 seconds — this is normal
- Ask for "per-well breakdown" if you want to identify the best/worst wells
- Use "Compare field economics under different oil price scenarios" for price sensitivity
