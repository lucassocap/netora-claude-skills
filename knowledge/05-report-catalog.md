# Report Catalog

70 report types available through `get_report_data(project_id, report_type)`.

Each report type assembles all required data from the platform and returns structured information for Claude to analyze and present.

---

## Production Reports

| Code | Name | Data Required | Use Case |
|------|------|--------------|----------|
| `monthly_summary` | Monthly Production Summary | Well production records, field totals | Monthly operations review |
| `actual_vs_forecast` | Actual vs Forecast | Production + DCA forecast | Performance tracking |
| `decline_monitoring` | Decline Rate Monitor | Production history, DCA params | Reserve revisions |
| `downtime_analysis` | Downtime Analysis | Downtime events per well | Uptime optimization |
| `surveillance` | Production Surveillance | All production data + anomalies | Real-time monitoring |
| `field_profile` | Field Production Profile | Aggregated field rates | FDP review |
| `water_cut` | Water Cut Evolution | BSW trends per well | Water management |
| `gor_evolution` | GOR Evolution | Gas-oil ratio trends | Gas handling planning |
| `optimization` | Production Optimization | Well rates, lift method, PI | Workover candidate list |

---

## Reserves Reports

| Code | Name | Data Required | Use Case |
|------|------|--------------|----------|
| `eur_summary` | EUR Summary | DCA params for all wells | Reserves booking |
| `dca_curves` | DCA Curve Display | Well forecast data | Technical review |
| `type_curve_analysis` | Type Curve Analysis | Type curves + well data | Standardization |
| `field_forecast` | Field Forecast Report | Field-level aggregate forecast | FDP planning |
| `reserves_booking` | Reserves Classification | P1/P2/P3 reserves per well | SEC/PRMS reporting |
| `plateau_analysis` | Plateau Rate Analysis | Field forecast + well schedule | Development pacing |
| `analog_benchmarking` | Analog Well Benchmarking | Reference wells + project wells | New well planning |

---

## Economics Reports

| Code | Name | Data Required | Use Case |
|------|------|--------------|----------|
| `single_well` | Single Well Economics | Well DCA + CAPEX + assumption | Well-level decision |
| `field_economics` | Field Economics | Field forecast + assumption + CAPEX | Field-level decision |
| `capex_schedule` | CAPEX Schedule | Drilling + facilities CAPEX by month | Budget planning |
| `opex_profile` | OPEX Profile | Variable + fixed OPEX over time | Operating budget |
| `cash_flow_waterfall` | Cash Flow Waterfall | Full economics time series | Financial review |
| `sensitivity_breakeven` | Sensitivity & Breakeven | Tornado + breakeven analysis | Risk assessment |

---

## Fiscal Reports

| Code | Name | Data Required | Use Case |
|------|------|--------------|----------|
| `fiscal_summary` | Fiscal Summary | Assumption + fiscal params | Fiscal analysis |
| `government_take` | Government Take Analysis | Full fiscal cascade | Partner negotiations |
| `contract_economics` | Contract Economics | Contract terms + economics | Contract evaluation |
| `country_comparison` | Country Comparison | Multiple country defaults | Country entry decision |

---

## Risk Reports

| Code | Name | Data Required | Use Case |
|------|------|--------------|----------|
| `montecarlo_summary` | Monte Carlo Summary | MC run results | Risk presentation |
| `tornado` | Tornado Chart | Sensitivity analysis data | Value driver ID |
| `fan_chart` | Fan Chart | MC production simulations | Production uncertainty |
| `sensitivity` | Full Sensitivity Report | Multi-variable sensitivity | Board presentation |

---

## Drilling Reports

| Code | Name | Data Required | Use Case |
|------|------|--------------|----------|
| `well_engineering` | Well Engineering Summary | Profile + survey + casing + mud | Drilling review |
| `afe_summary` | AFE Summary | Well activities + costs | Budget approval |
| `bha_run_report` | BHA Run Report | Drill strings + runs + bits | BHA performance |
| `bit_performance` | Bit Performance | Bit data from drill runs | Bit selection |
| `slidesheet_summary` | Slide Sheet Summary | Slide records + survey | Directional review |
| `casing_design` | Casing Design Report | Casing sections + formations | Engineering review |
| `time_vs_depth` | Time vs Depth | Drilling phases + actual data | Drilling performance |
| `rig_schedule` | Rig Schedule | FDP rig assignments | Rig planning |
| `field_gantt` | Field Development Gantt | FDP timeline all wells | FDP presentation |

---

## Facilities Reports

| Code | Name | Data Required | Use Case |
|------|------|--------------|----------|
| `process_design` | Process Design Summary | Facilities scenario + units | Engineering review |
| `cost_estimate` | Facilities Cost Estimate | Costing results | Budget planning |
| `equipment_specs` | Equipment Specifications | Sized equipment details | Procurement |

---

## Executive Reports

| Code | Name | Data Required | Use Case |
|------|------|--------------|----------|
| `one_pager` | One-Page Project Summary | All project data | Quick reference |
| `investment_summary` | Investment Summary | Economics + risk + fiscal | Investment committee |

---

## Usage

### Generate a Report

```
Get the report data for project 18, type "single_well"
```

Claude will:
1. Call `get_report_data(project_id=18, report_type="single_well")`
2. Receive all necessary data
3. Generate a formatted analysis with tables and insights

### Save a Report

After generating, Claude can save reports:
1. `create_chat_session(project_id, title="Monthly Review - May 2026")`
2. `append_chat_message(session_id, content="[report content]", is_report=True)`

### List Saved Reports

```
List all reports for project 18
```

Calls `list_reports(project_id=18)` to show saved analyses.

---

## Report Quality Guidelines

When generating reports, Claude should:

1. **Structure:** Title, Executive Summary, Key Metrics (table), Detailed Analysis, Recommendations
2. **Numbers:** Round appropriately — NPV to nearest $0.1MM, IRR to 1 decimal, EUR to 1 decimal
3. **Comparisons:** Use tables for multi-well or multi-scenario comparisons
4. **Flags:** Highlight negative NPV, low IRR, high government take, long payout periods
5. **Context:** Compare against industry benchmarks when possible
6. **Units:** Always include units in table headers and inline references
