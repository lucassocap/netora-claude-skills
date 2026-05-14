# Netora Tool Catalog

Complete reference of all 170 tools available through the Netora MCP integration, organized by domain.

---

## 1. Projects & Fields

### list_projects
List all projects with field and well counts.
- **Args:** `limit` (int, default 50), `offset` (int, default 0)
- **Returns:** Project list with id, name, country_code, status, field_count, well_count, facility_count

### get_project_details
Get detailed info about a project including fields, assumptions, and facility counts.
- **Args:** `project_id` (int, required)
- **Returns:** Project details, fields list, assumptions list, facility count, total facility CAPEX

### get_project_full_data
Deep aggregation of all project data — fields, wells (with DCA), facilities, assumptions, economics results.
- **Args:** `project_id` (int, required)
- **Returns:** Complete project snapshot with summary statistics

### create_project
Create a new E&P project.
- **Args:** `name` (str, required), `country_code` (str, default "USA"), `description` (str)
- **Country codes:** USA, VEN, COL, ARG, BRA, PER, ECU, BOL

### update_project
Update project name, country, status, or description.
- **Args:** `project_id` (int, required), `fields` (dict — name, country_code, status, description)

### duplicate_project
Deep-copy entire project: fields, wells, activities, facilities, AFE templates.
- **Args:** `project_id` (int, required), `new_name` (str, optional)

### list_fields
List all fields in a project with well counts and coordinates.
- **Args:** `project_id` (int, required), `limit` (int), `offset` (int)

### create_field
Create a new field (exploration/development area) in a project.
- **Args:** `project_id` (int, required), `name` (str, required), `center_lat` (float), `center_lon` (float), `description` (str)

### update_field
Update a field's name, description, or center coordinates.
- **Args:** `field_id` (int, required), `fields` (dict)

### delete_field
Delete a field and all its wells (CASCADE).
- **Args:** `field_id` (int, required)

### get_field_forecast
Get aggregated field production forecast (all wells combined).
- **Args:** `field_id` (int, required), `n_months` (int, default 120)
- **Returns:** Monthly field rates, cumulative oil, CAPEX schedule, totals

---

## 2. Wells

### list_wells
List wells in a field with key parameters.
- **Args:** `field_id` (int, required), `limit` (int), `offset` (int), `status` (str — planned, drilling, producing, shut_in, abandoned)

### get_well_detail
Full detail for a single well: DCA params, AFE activities, last 12 production records.
- **Args:** `well_id` (int, required)

### create_wells
Batch create wells in a field.
- **Args:** `field_id` (int, required), `wells` (list of dicts)
- **Each well:** name (required), well_type, status, dca_qi, dca_di, dca_b, capex_usd, opex_usd_bbl, spud_date, formation, lat, lon, depth_tvd_ft

### update_well
Update one or more fields on a well.
- **Args:** `well_id` (int, required), `fields` (dict)
- **Updatable:** name, well_type, status, dca_qi, dca_di, dca_b, capex_usd, opex_usd_bbl, spud_date, formation, lift_method, lat, lon, depth_tvd_ft, notes, sort_order, afe_source

### update_wells_batch
Batch update multiple wells at once.
- **Args:** `updates` (list of {well_id, fields})

### delete_well
Delete a well (soft delete).
- **Args:** `well_id` (int, required)

### get_well_activities
Get AFE cost breakdown activities for a well.
- **Args:** `well_id` (int, required)
- **Returns:** Activities with phase, description, duration, cost

### list_well_groups
List well groups (pads/macollas) in a field.
- **Args:** `field_id` (int, required)

### create_well_group
Create a well group in a field.
- **Args:** `field_id` (int, required), `name` (str, required), `color` (str), `description` (str)

### update_well_group
Update group fields or add/remove wells from group.
- **Args:** `group_id` (int, required), `fields` (dict), `add_wells` (list), `remove_wells` (list)

### delete_well_group
Delete a well group.
- **Args:** `group_id` (int, required)

---

## 3. AFE Templates

### list_afe_templates
List AFE (Authority for Expenditure) templates for a project.
- **Args:** `project_id` (int, required)

### create_afe_template
Create a reusable AFE template.
- **Args:** `project_id` (int, required), `name` (str, required), `well_type` (str — vertical, horizontal, deviated), `activities` (list of dicts)

### update_afe_template
Update an AFE template.
- **Args:** `template_id` (int, required), `fields` (dict)

### apply_afe_template
Apply an AFE template to a well (replaces existing activities).
- **Args:** `template_id` (int, required), `well_id` (int, required)

---

## 4. Production

### list_production_records
List monthly production records for a well.
- **Args:** `well_id` (int, required)
- **Returns:** Records with date, oil_bopd, gas_mscfd, water_bwpd

### add_production_records
Add monthly production records (upserts by date).
- **Args:** `well_id` (int, required), `records` (list of {date, oil_bopd, gas_mscfd, water_bwpd})

### well_production_import
Import production data from external source.
- **Args:** `well_id` (int, required), data payload

### well_production_export
Export production data.
- **Args:** `well_id` (int, required)

### well_actual_vs_forecast
Compare actual production against DCA forecast.
- **Args:** `well_id` (int, required)

### well_decline_monitor
Monitor decline rate trends for a well.
- **Args:** `well_id` (int, required)

### well_downtime_list
List downtime events for a well.
- **Args:** `well_id` (int, required)

### well_downtime_create
Record a new downtime event.
- **Args:** well_id, start_date, end_date, reason, etc.

---

## 5. DCA Forecast

### compute_well_forecast
Run Arps DCA forecast for a well.
- **Args:** `well_id` (int, required)
- **Returns:** Monthly rates (oil, gas, water), cumulative volumes, EUR (MSTB)
- **Requires:** Well must have dca_qi and dca_di set

### get_forecast_defaults
Get default DCA parameters.
- **Returns:** qi=500, di=0.05, b=0.5, q_abandon=5, n_periods=120, gor=500, bsw_initial=0.10, bsw_final=0.50

### get_forecast_run
Get a saved forecast run with full time series.
- **Args:** `run_id` (int, required)

### forecast_artificial_lift
Run forecast with artificial lift optimization.
- **Args:** `well_id` (int, required)

### forecast_ml
Run ML-based production forecast.
- **Args:** `well_id` (int, required)

### forecast_auto_report_field
Generate automated forecast report for a field.
- **Args:** `field_id` (int, required)

### forecast_auto_report_project
Generate automated forecast report for a project.
- **Args:** `project_id` (int, required)

---

## 6. Type Curves

### list_type_curves
List available type curves for a project.
- **Args:** `project_id` (int, required)

### create_type_curve
Create a new type curve from DCA parameters.
- **Args:** `project_id` (int, required), name, DCA params

### update_type_curve
Update an existing type curve.
- **Args:** type curve id and fields

### delete_type_curve
Delete a type curve.
- **Args:** `type_curve_id` (int, required)

### apply_type_curve
Apply a type curve's DCA parameters to selected wells.
- **Args:** `type_curve_id` (int, required), `well_ids` (list)

### history_match
Perform history matching on a well's production data.
- **Args:** `well_id` (int, required)

### reserves_classify
Classify reserves for a field (proved/probable/possible).
- **Args:** `field_id` (int, required)

### anomaly_detection
Detect production anomalies for a well.
- **Args:** `well_id` (int, required)

---

## 7. Economics

### compute_well_economics
Run full economics for a single well: DCA + fiscal cascade + sensitivity.
- **Args:** `well_id` (int, required), `project_id` (int, recommended)
- **Returns:** NPV, IRR, payout month, breakeven price, profitability index, F&D cost, government take, sensitivity tornado, NPV profile
- **Requires:** Well must have dca_qi, dca_di, and capex_usd

### run_field_economics
Run field-level economics with aggregated production and CAPEX schedule.
- **Args:** `field_id` (int, required), `assumption_id` (int, required)

### get_economics_defaults
Get default economic parameters.
- **Returns:** Oil price, gas price, OPEX, royalty, tax, discount rate defaults

### get_economics_run
Get a saved economics run with summary and time series.
- **Args:** `run_id` (int, required)

### economics_compare
Compare economics across scenarios or wells.
- **Args:** Comparison parameters

### economics_capex
Get aggregated CAPEX from drilling and facilities modules.
- **Args:** `project_id` (int, required)

---

## 8. Economic Assumptions

### list_assumptions
List economic assumption sets for a project.
- **Args:** `project_id` (int, required)

### get_assumption
Get full detail for an assumption set.
- **Args:** `assumption_id` (int, required)

### create_assumption
Create a new economic assumption set.
- **Args:** `project_id` (int, required), `name` (str, required), `country` (str), `oil_price_usd_bbl` (float, 70.0), `gas_price_usd_mscf` (float, 3.0), `opex_usd_bbl` (float, 12.0), `royalty_rate_pct` (float, 20.0), `ihi_rate_pct` (float, 0.0), `income_tax_rate_pct` (float, 34.0), `gov_equity_share_pct` (float, 0.0), `discount_rate_pct` (float, 10.0), `dca_source` (str — well, type_curve, manual), `fiscal_source` (str — manual, scenario)

### update_assumption
Update an assumption set's parameters.
- **Args:** `assumption_id` (int, required), `fields` (dict)

### delete_assumption
Delete an assumption set.
- **Args:** `assumption_id` (int, required)

---

## 9. Monte Carlo

### run_montecarlo
Run single-well Monte Carlo simulation.
- **Args:** `well_id` (int, required), plus optional triangular ranges for qi, di, b, oil_price, capex, opex (each as {low, base, high})
- **Returns:** P10/P50/P90 for NPV, IRR, EUR, payout. Probability of positive NPV. Histograms and scatter plots.

### run_field_montecarlo
Run field-level Monte Carlo with drill probability and schedule slip.
- **Args:** `field_id` (int, required), `assumption_id` (int, required), plus optional ranges
- **Returns:** P10/P50/P90 for NPV, EUR, peak rate. Fan chart data.

### montecarlo_portfolio
Run portfolio-level Monte Carlo across multiple fields.
- **Args:** Portfolio parameters

### montecarlo_compare
Compare Monte Carlo results across scenarios.
- **Args:** Run IDs to compare

### get_montecarlo_run
Get saved Monte Carlo results.
- **Args:** `run_id` (int, required)
- **Returns:** Summary, histograms, probability metrics

### get_montecarlo_defaults
Get default Monte Carlo parameters.

---

## 10. Fiscal

### fiscal_compare
Side-by-side fiscal regime comparison across countries.
- **Args:** `country_codes` (list), `periods` (list of production/cost data)

### list_fiscal_scenarios
List saved fiscal calculation scenarios.
- **Args:** `project_id` (int), `country_code` (str)

### get_scenario_detail (fiscal)
Get full detail for a fiscal scenario.
- **Args:** `scenario_id` (int, required)

---

## 11. Drilling Engineering

### Profiles
- `list_drilling_profiles(well_id)` — List profiles for a well
- `get_drilling_profile_detail(profile_id)` — Full profile with casing, formations, phase summary
- `create_drilling_profile(well_id, name)` — Create new profile

### Survey Stations
- `list_survey_stations(profile_id)` — Get trajectory data (MD, Inc, Azm, TVD, NS, EW, DLS)
- `create_survey_stations(profile_id, stations[])` — Add survey points
- `update_survey_station(station_id, fields)` — Update a station
- `delete_survey_station(station_id)` — Remove a station
- `interpolate_survey(profile_id, md)` — Interpolate at a given MD
- `survey_qc(profile_id)` — Quality check on survey data

### Targets
- `list_targets(profile_id)` — List directional targets
- `create_target(profile_id, ...)` — Add a target
- `delete_target(target_id)` — Remove a target

### BHA / Drill Strings
- `list_drill_strings(profile_id)` — List BHA assemblies
- `create_drill_string(profile_id, ...)` — Create new BHA
- `delete_drill_string(string_id)` — Remove BHA
- `list_string_components(string_id)` — List components in a BHA
- `create_string_component(string_id, ...)` — Add component
- `delete_string_component(component_id)` — Remove component

### Drill Runs & Bits
- `list_drill_runs(profile_id)` — List drill runs
- `create_drill_run(profile_id, ...)` — Create run
- `delete_drill_run(run_id)` — Remove run
- `get_drill_bit(run_id)` / `set_drill_bit(run_id, ...)` — Bit management
- `get_drill_motor(run_id)` / `set_drill_motor(run_id, ...)` — Motor management

### Slides & Records
- `list_slide_records(profile_id)` — List slide records
- `create_slide_record(profile_id, ...)` — Add slide record
- `list_casing_sections(profile_id)` / `create_casing_section(...)` — Casing program
- `list_mud_records(profile_id)` / `create_mud_record(...)` — Mud program
- `list_pumps(profile_id)` / `create_pump(...)` — Pump data
- `list_formation_tops(profile_id)` / `create_formation_top(...)` — Formation tops

### Well Plan
- `list_well_plan_stages(profile_id)` — List planned stages
- `create_well_plan_stage(profile_id, ...)` — Add stage
- `delete_well_plan_stage(stage_id)` — Remove stage
- `compute_well_plan(profile_id)` — Compute full well plan

### Drilling Phases
- `list_drilling_phases(profile_id)` — List time & cost phases
- `get_drilling_phase_summary(profile_id)` — Summary totals
- `generate_drilling_phases(profile_id)` — Auto-generate phases

### Engineering Calculations
- `ecd_profile(profile_id)` — ECD (Equivalent Circulating Density) profile
- `hole_cleaning(profile_id)` — Hole cleaning analysis
- `motor_yield(profile_id)` — Motor yield curve
- `get_magnetic_reference(lat, lon)` — Magnetic reference data
- `convert_coordinates(...)` — Coordinate conversion

### Analysis
- `run_torque_drag(profile_id)` — Torque & drag analysis
- `run_hydraulics(profile_id)` — Full hydraulics analysis
- `run_proximity_scan(profile_id)` — Anti-collision scan
- `drilling_bha_validate(...)` — BHA validation checks
- `drilling_casing_analyze(...)` — Casing design analysis

### FDP (Field Development Plan)
- `drilling_fdp_gantt(...)` — Drilling Gantt chart
- `drilling_fdp_pad_sequence(...)` — Pad sequencing
- `drilling_fdp_rig_schedule(...)` — Rig schedule optimization
- `drilling_fdp_plateau_target(...)` — Plateau rate targeting

### Templates
- `list_rop_templates(...)` / `create_rop_template(...)` — ROP templates
- `list_flat_time_templates(...)` / `create_flat_time_template(...)` — Flat time templates

---

## 12. Facilities

### Scenarios
- `list_scenarios(project_id)` — List facilities scenarios
- `get_scenario_detail(scenario_id)` — Full detail with units and costs
- `create_scenario(project_id, name, peak_oil_bopd, ...)` — Create scenario
- `auto_generate_scenario(scenario_id)` — Auto-generate, size, and cost all equipment

### Engine
- `run_scenario_sizing(scenario_id)` — Run equipment sizing
- `run_scenario_costing(scenario_id)` — Run cost estimation

### Analysis
- `facilities_emissions(...)` — Emissions calculations
- `facilities_pipelines(...)` — Pipeline sizing
- `facilities_power(...)` — Power requirements
- `facilities_hydraulics(...)` — Process hydraulics

### Facilities CRUD
- `list_facilities(project_id)` · `create_facility(...)` · `update_facility(...)` · `delete_facility(...)`

---

## 13. Reports & Chat

### Reports
- `get_report_data(project_id, report_type)` — Assemble data for a report type
- `list_reports(project_id)` — List saved AI-generated reports
- `get_report(report_id)` — Get full report content
- `update_report(report_id, ...)` — Update report

### Chat Sessions
- `list_chat_sessions(project_id)` — List chat history
- `create_chat_session(project_id, title)` — Start new session
- `get_chat_session(session_id)` — Get messages
- `append_chat_message(session_id, ...)` — Add message
- `delete_chat_session(session_id)` — Delete session

---

## 14. Knowledge Base

- `search_knowledge_base(query)` — Semantic search across knowledge base
- `semantic_search_documents(query)` — Search uploaded documents
- `list_well_analogs(country, formation)` — Find analog wells
- `delete_knowledge_source(source_id)` — Remove a knowledge source

---

## 15. Users & Admin

- `list_users` — List platform users
- `get_user(user_id)` — Get user details
- `create_user(...)` — Create new user
- `update_user(user_id, ...)` — Update user
- `list_organizations` — List organizations
- `list_user_audit(...)` — User audit log
- `list_data_audit(...)` — Data change audit log
- `create_invitation(email, role)` — Send platform invitation
- `list_project_members(project_id)` — List project team
- `add_project_member(project_id, email, role)` — Add member
- `remove_project_member(project_id, user_id)` — Remove member

---

## 16. Analytics Runs

- `list_analytics_runs(project_id)` — List all saved runs (forecast, economics, Monte Carlo)
- `get_economics_run(run_id)` — Get saved economics results
- `get_forecast_run(run_id)` — Get saved forecast results
- `get_montecarlo_run(run_id)` — Get saved Monte Carlo results
- `get_drilling_studio_afe(well_id)` — Get drilling studio AFE data
- `search_reference_wells(country, formation, ...)` — Search reference well database
