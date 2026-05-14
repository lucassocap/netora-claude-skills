# Skill: Well Plan Review

## When to Use

- Pre-spud engineering review
- Peer review of drilling program
- Identifying potential drilling problems
- Verifying trajectory and casing design

## Prerequisites

- Well must have a drilling profile with survey stations
- Casing program and formation tops entered (optional but recommended)

## Prompt

```
Review the drilling plan for well [WELL_NAME or WELL_ID].

Include:
1. Trajectory summary: KOP, build rate, max inclination, final azimuth, TD (MD and TVD)
2. Survey QC: any DLS exceedances, data quality issues?
3. Casing program: conductor, surface, intermediate, production — depths and grades
4. Formation tops crossed
5. Drilling phases: time and cost per section
6. ECD profile: verify mud weight margin vs fracture gradient
7. Torque & drag: hookload at TD, maximum torque
8. Total estimated cost and duration

Flag any concerns (high DLS, tight ECD margin, excessive torque).
```

## What Claude Does

1. `list_drilling_profiles(well_id)` → get profile ID
2. `get_drilling_profile_detail(profile_id)` → casing, formations, phases
3. `list_survey_stations(profile_id)` → trajectory data
4. `survey_qc(profile_id)` → QC check
5. `ecd_profile(profile_id)` → hydraulics
6. `run_torque_drag(profile_id)` → T&D analysis

## Tips

- If no drilling profile exists, ask Claude to create one first
- Ask for "comparison to offset wells" for context
- "Identify the riskiest section" for risk-focused review
