# Skill: Project Summary (One-Pager)

## When to Use

- Quick project overview for stakeholders
- Status update at management meetings
- Portfolio review dashboard
- New team member onboarding

## Prerequisites

- Existing project with fields, wells, and ideally economics results

## Prompt

```
Create a one-page project summary for [PROJECT_NAME].

Include:
1. Project name, country, operator
2. Asset overview: # fields, # wells (by status), # facilities
3. Current production (total bopd)
4. Reserves: total EUR (MSTB)
5. Economics snapshot: NPV, IRR (if available)
6. Total CAPEX invested and remaining
7. Key risks and next steps

Keep it concise — one page maximum. Use a summary table at the top.
```

## What Claude Does

1. `get_project_full_data(project_id)` → all data in one call
2. Formats into concise one-page layout

## Tips

- Great for portfolio reviews: ask for one-pagers for all projects
- Add "Compare to last month" for delta reporting
- Request "traffic light status" (green/yellow/red) for each metric
