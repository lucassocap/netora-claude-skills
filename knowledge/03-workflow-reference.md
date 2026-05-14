# Workflow Reference

20 step-by-step workflows for common petroleum engineering tasks using Netora tools.

---

## 1. Full Project Analysis

**When:** Board review, investment decision, project status update.

1. `get_project_full_data(project_id)` — Get complete project structure with all fields, wells, facilities, and current economics
2. `list_assumptions(project_id)` — Review fiscal/economic parameters
3. For each field → `run_field_economics(field_id, assumption_id)` — Field-level NPV, IRR, EUR
4. `run_field_montecarlo(field_id, assumption_id)` — P10/P50/P90 risk analysis
5. **Summarize:** Total NPV, weighted IRR, combined EUR, government take, P50 probability

---

## 2. Single Well Economics

**When:** Pre-drill decision, well justification, AFE approval.

1. `get_well_detail(well_id)` — Verify DCA params (qi, di, b) and CAPEX exist
2. If missing: `update_well(well_id, fields={dca_qi: X, dca_di: Y, dca_b: Z, capex_usd: N})`
3. `compute_well_economics(well_id, project_id)` — Full economics run
4. **Present:** NPV, IRR, payout month, breakeven price, PI, F&D cost, sensitivity tornado

---

## 3. Field Economics

**When:** Field development plan, multi-well economics, CAPEX justification.

1. `list_fields(project_id)` — Get field ID
2. `list_wells(field_id)` — Verify wells have DCA params
3. `list_assumptions(project_id)` — Get assumption ID
4. `run_field_economics(field_id, assumption_id)` — Run economics
5. **Present:** Aggregated NPV, field IRR, CAPEX schedule, production profile, government take

---

## 4. Sensitivity Analysis (Tornado)

**When:** Risk assessment, identify key value drivers.

1. `compute_well_economics(well_id, project_id)` — Run with defaults
2. Extract sensitivity from response (±20% swing on oil_price, capex, opex, royalty, tax, discount)
3. **Present:** Sorted tornado chart showing NPV impact per variable

---

## 5. DCA Forecast

**When:** Production planning, reserves estimation.

1. `get_well_detail(well_id)` — Check current DCA params
2. `compute_well_forecast(well_id)` — Run Arps DCA
3. **Present:** EUR (MSTB), abandonment month, monthly oil/gas/water profiles

---

## 6. Monthly Production Review

**When:** Operations review, performance tracking.

1. `list_production_records(well_id)` — Get last 12 months
2. `well_actual_vs_forecast(well_id)` — Compare actual vs DCA forecast
3. `well_decline_monitor(well_id)` — Check decline rate trends
4. **Present:** Rate table, variance analysis, decline rate change alert

---

## 7. Decline Analysis

**When:** Reserve revisions, well performance diagnosis.

1. `list_production_records(well_id)` — Get production history
2. `history_match(well_id)` — Fit DCA to actual data
3. `compute_well_forecast(well_id)` — Updated forecast with matched params
4. **Present:** Best-fit qi/di/b, updated EUR, remaining reserves

---

## 8. Type Curve Workflow

**When:** New well planning, standardized DCA.

1. `list_type_curves(project_id)` — Available curves
2. If none: `create_type_curve(project_id, name, qi, di, b, ...)`
3. `apply_type_curve(type_curve_id, well_ids)` — Apply to wells
4. For each well: `compute_well_forecast(well_id)` — Verify results
5. **Present:** EUR per well, field EUR total

---

## 9. Drilling Plan Review

**When:** Pre-drill check, engineering review, peer review.

1. `list_drilling_profiles(well_id)` — Get profile ID
2. `get_drilling_profile_detail(profile_id)` — Casing, formations, phase summary
3. `list_survey_stations(profile_id)` — Full trajectory
4. `survey_qc(profile_id)` — Quality check
5. `ecd_profile(profile_id)` — Verify ECD vs mud weight margin
6. `run_torque_drag(profile_id)` — Check hookload limits
7. **Present:** TD, trajectory summary, casing program, time/cost estimate, ECD alerts

---

## 10. Drilling Cost Estimate (AFE)

**When:** Budget preparation, AFE submission.

1. `get_well_detail(well_id)` — Current CAPEX and activities
2. `get_drilling_studio_afe(well_id)` — Drilling profile-based cost
3. Or: `list_afe_templates(project_id)` → `apply_afe_template(template_id, well_id)`
4. `get_well_activities(well_id)` — Verify activity breakdown
5. **Present:** Phase-by-phase cost table, total AFE, comparison to budget

---

## 11. Monte Carlo — Single Well

**When:** Investment risk assessment, probability of success.

1. `get_well_detail(well_id)` — Base case parameters
2. `run_montecarlo(well_id)` with ranges:
   - qi: ±30% of base
   - oil_price: $55/$70/$90
   - capex: −15%/base/+30%
   - 1000 simulations
3. **Present:** P10/P50/P90 NPV and IRR, probability of positive NPV, histogram

---

## 12. Monte Carlo — Field Level

**When:** Field development decision, portfolio ranking.

1. `list_wells(field_id)` — Verify well count
2. `list_assumptions(project_id)` — Get assumption
3. `run_field_montecarlo(field_id, assumption_id)` with:
   - Per-well drill probability, schedule slip
   - Global oil price and qi multiplier ranges
4. **Present:** P10/P50/P90 NPV and EUR, fan chart, probability of positive NPV

---

## 13. Country Fiscal Comparison

**When:** Country entry decisions, partner negotiations.

1. For each country: use `fiscal_compare(country_codes, periods)`
2. Or manually: get defaults per country and run economics
3. **Present:** Side-by-side: royalty, tax, IHI, state equity, gov take %, partner NPV, partner IRR

---

## 14. Facilities Design

**When:** Surface facility planning, CAPEX estimation.

1. `create_scenario(project_id, name, peak_oil_bopd, peak_gas_mscfd, api_gravity, ...)`
2. `auto_generate_scenario(scenario_id)` — Generate + size + cost all equipment
3. `get_scenario_detail(scenario_id)` — Review equipment list and costs
4. **Present:** Equipment list with capacities, individual costs, total project CAPEX

---

## 15. Report Generation

**When:** Any deliverable — monthly report, investment memo, board deck.

1. `get_report_data(project_id, report_type)` — Assemble all required data
2. Analyze and generate narrative with tables/charts
3. `create_chat_session(project_id, title)` + `append_chat_message(...)` to save
4. **Report types:** monthly_summary, single_well, field_economics, investment_summary, one_pager, etc.

---

## 16. Create Project from Scratch

**When:** New project setup, data entry.

1. `create_project(name, country_code)` — Create project
2. `create_field(project_id, name, center_lat, center_lon)` — Add fields
3. `create_wells(field_id, wells=[...])` — Add wells with DCA + CAPEX
4. `create_assumption(project_id, name, oil_price_usd_bbl, ...)` — Set fiscal params
5. Verify: `get_project_full_data(project_id)`

---

## 17. Well Analog Search

**When:** Planning wells in new areas, benchmarking.

1. `search_reference_wells(country, formation, depth_min, depth_max)` — Find analogs
2. `list_well_analogs(country, formation)` — Additional references
3. `search_knowledge_base(query)` — Technical papers and reports
4. **Present:** Analog well parameters (qi, di, EUR, CAPEX), recommended DCA range

---

## 18. Portfolio Comparison

**When:** Ranking multiple projects or fields, capital allocation.

1. For each project: `get_project_full_data(project_id)`
2. For each field: `run_field_economics(field_id, assumption_id)`
3. `montecarlo_portfolio(...)` — Portfolio-level risk
4. **Present:** Ranked table by NPV, IRR, PI, EMV

---

## 19. Production Import & Setup

**When:** Loading historical production data.

1. `list_wells(field_id)` — Get well IDs
2. For each well: `add_production_records(well_id, records=[{date, oil_bopd, gas_mscfd, water_bwpd}])`
3. Verify: `list_production_records(well_id)`
4. `history_match(well_id)` — Fit DCA to actual data

---

## 20. Executive Investment Memo

**When:** Investment committee, partner presentation, board meeting.

1. `get_project_full_data(project_id)` — Full snapshot
2. `run_field_economics(field_id, assumption_id)` — Per-field economics
3. `run_field_montecarlo(field_id, assumption_id)` — Risk assessment
4. `fiscal_compare(country_codes, ...)` — Fiscal context (if multi-country)
5. **Generate:** Executive summary, key metrics table, risk matrix, recommendation
