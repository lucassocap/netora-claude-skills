# Skill: Drilling Cost Estimate

## When to Use

- AFE preparation
- Budget planning for drilling campaign
- Comparing cost estimates across well types
- Validating drilling cost assumptions

## Prerequisites

- Well with drilling profile and phases defined
- OR AFE template available for the project

## Prompt

```
Generate a drilling cost estimate (AFE) for well [WELL_NAME or WELL_ID].

Include:
1. Phase-by-phase breakdown: mobilization, drilling (per section), casing, completion, testing, demobilization
2. Duration per phase (days)
3. Cost per phase (day rate × days + flat costs)
4. Total well cost (AFE amount)
5. Comparison to project average (if available)
6. Cost per foot drilled

If the well has a drilling profile, use the drilling studio data.
If not, use the AFE template approach.
```

## What Claude Does

1. `get_drilling_studio_afe(well_id)` → check for drilling profile-based estimate
2. If no profile: `list_afe_templates(project_id)` → find matching template
3. `get_well_activities(well_id)` → current cost breakdown
4. Formats into AFE table

## Tips

- Ask "Apply the [template name] AFE template to this well" to auto-populate costs
- "Compare AFE for vertical vs horizontal wells" for decision support
- Request "contingency analysis" — Claude can add 10-15% contingency
