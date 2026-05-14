# Data Model Reference

Entity relationships and data flow in the Netora Upstream Platform.

---

## Core Entity Hierarchy

```
Organization
└── Project (country_code, status)
    ├── Field (center_lat/lon, polygon)
    │   ├── Well (DCA params, CAPEX, status, dates)
    │   │   ├── WellActivity (AFE cost breakdown)
    │   │   ├── ProductionRecord (monthly oil/gas/water)
    │   │   └── DrillingProfile
    │   │       ├── SurveyStation (MD, Inc, Azm → TVD, NS, EW, DLS)
    │   │       ├── CasingSection (conductor, surface, intermediate, production)
    │   │       ├── FormationTop (name, MD, TVD)
    │   │       ├── DrillingPhase (section, depth range, time, cost)
    │   │       ├── Mud (name, weight, depth)
    │   │       ├── DrillString (BHA assembly)
    │   │       │   └── StringComponent (tool, OD, ID, weight)
    │   │       ├── DrillRun (bit, motor, depth range)
    │   │       ├── SlideRecord (MD from/to, toolface, BUR)
    │   │       ├── Target (TVD, VS, radius)
    │   │       ├── WellPlanStage (planned depth/time)
    │   │       └── Pump (liner, stroke, rate)
    │   ├── WellGroup (pad/macolla grouping)
    │   └── Facility (type, cost, operation_date)
    │
    ├── EconomicAssumption (fiscal + DCA + CAPEX sources)
    │   └── FieldEconomicsRun (summary: NPV, IRR, EUR)
    │
    ├── FiscalScenario (country, contract_type, periods, results)
    │
    ├── TypeCurve (representative DCA: qi, di, b)
    │
    ├── FacilitiesScenario (peak rates, API gravity)
    │   ├── ProcessUnit (separator, compressor, heater, etc.)
    │   ├── CostEstimate (equipment, installed, total)
    │   └── Timeline (CAPEX schedule by month)
    │
    ├── AFETemplate (reusable drilling cost template)
    │
    ├── ChatSession (AI conversation history)
    │   └── ChatMessage (content, is_report, report_data)
    │
    ├── ForecastRun (saved DCA forecast)
    ├── EconomicsRun (saved economics results)
    ├── MonteCarloRun (saved MC simulation)
    ├── FieldMCRun (saved field-level MC)
    │
    └── KnowledgeSource (uploaded reference data)
        └── KnowledgeChunk (vector embeddings for search)
```

---

## Key Entity Details

### Project
```
id, name, country_code, status, description
created_by, created_at, updated_at
```
- Top-level container for all E&P data
- Country code determines default fiscal regime
- Status: active, archived, draft

### Field
```
id, project_id, name, description
center_lat, center_lon, polygon (GeoJSON)
```
- Geographic area within a project
- Contains wells and facilities
- Has aggregated production forecast

### Well
```
id, field_id, name, well_type, status, api_number
lat, lon, depth_tvd_ft, depth_md_ft, formation
lift_method, spud_date, first_oil_date
drilling_days, completion_days, rig_name

# DCA Parameters (required for forecast + economics)
dca_qi          # Initial rate (bopd)
dca_di          # Nominal decline (fraction/month)
dca_b           # Arps exponent (0-2)
dca_q_abandon   # Abandonment rate (bopd, default 5)
dca_gor_scf_bbl # Gas-oil ratio
dca_bsw_initial_pct  # Initial water cut
dca_bsw_final_pct    # Final water cut
dca_project_months   # Forecast length (default 120)

# Economics
capex_usd       # Total CAPEX ($)
opex_usd_bbl    # Variable OPEX ($/bbl)
afe_source      # template, drilling_studio, manual

sort_order, notes, color
well_group_id   # Optional pad/macolla grouping
```

### Well Status Values
- `planned` — Not yet drilled
- `drilling` — Currently being drilled
- `producing` — On production
- `shut_in` — Completed but not producing
- `abandoned` — Permanently P&A

### Well Types
- `vertical`, `horizontal`, `deviated`, `multilateral`

### WellActivity (AFE Breakdown)
```
id, well_id, sequence, phase, description
duration_days, cost_type (day_rate | fixed)
day_rate_usd, fixed_cost_usd
computed_cost_usd  # auto-calculated
```
- Phases: mobilization, drilling, casing, completion, testing, demobilization, other

### ProductionRecord
```
id, well_id, date (YYYY-MM-DD)
oil_bopd, gas_mscfd, water_bwpd
```
- Monthly granularity
- Upserts by (well_id, date) — adding existing date updates it

### EconomicAssumption
```
id, project_id, name, country
oil_price_usd_bbl, gas_price_usd_mscf
opex_usd_bbl, fixed_opex_usd_mo, capex_usd
royalty_rate_pct, ihi_rate_pct, income_tax_rate_pct
gov_equity_share_pct, gov_capex_contribution_pct
discount_rate_pct

# Source linking
dca_source        # well | type_curve | manual
type_curve_id     # FK to TypeCurve (if dca_source=type_curve)
fiscal_source     # manual | scenario
fiscal_scenario_id  # FK to FiscalScenario
capex_source      # manual | modules (auto from drilling+facilities)

# Manual DCA override
dca_qi, dca_di_pct, dca_b

# Cached results
run_summary       # JSON of last economics run
```

---

## Data Flow Diagram

```
                    ┌─────────────────────────────────────┐
                    │         DATA ENTRY                    │
                    │                                       │
                    │  Wells (DCA, CAPEX, dates)            │
                    │  Production Records                   │
                    │  Drilling Profiles                    │
                    │  Facilities Scenarios                 │
                    │  Assumptions                          │
                    └──────────┬────────────────────────────┘
                               │
                    ┌──────────▼────────────────────────────┐
                    │         COMPUTATION                    │
                    │                                       │
                    │  DCA Forecast ──────► EUR, Rates      │
                    │  Field Forecast ────► Aggregated Curve │
                    │  Drilling Phases ──► Time & Cost      │
                    │  Facilities ───────► Sizing & CAPEX   │
                    │  CAPEX Aggregation ► Total Budget     │
                    └──────────┬────────────────────────────┘
                               │
                    ┌──────────▼────────────────────────────┐
                    │         ECONOMICS                     │
                    │                                       │
                    │  Well Economics ───► NPV, IRR, PI     │
                    │  Field Economics ──► Field NPV, FCF   │
                    │  Fiscal Cascade ──► Government Take   │
                    │  Sensitivity ─────► Tornado           │
                    └──────────┬────────────────────────────┘
                               │
                    ┌──────────▼────────────────────────────┐
                    │         RISK                          │
                    │                                       │
                    │  MC Well ─────────► P10/P50/P90 NPV  │
                    │  MC Field ────────► Fan Chart, EMV    │
                    │  Portfolio ───────► Ranked Projects   │
                    └──────────┬────────────────────────────┘
                               │
                    ┌──────────▼────────────────────────────┐
                    │         REPORTING                     │
                    │                                       │
                    │  70 Report Types                      │
                    │  Chat Sessions (persistent)           │
                    │  Saved Runs (forecast, econ, MC)      │
                    └──────────────────────────────────────┘
```

---

## CAPEX Flow

```
Drilling Studio                    Facilities Studio
├── DrillRun.actual_cost_usd       ├── CostEstimate.total_installed_usd
└── Σ per well                     └── Σ per scenario
         │                                  │
         └──────────┬───────────────────────┘
                    │
         get_project_capex() ──► capex_source on Assumption
                                        │
                              ┌─────────▼──────────┐
                              │  Field Economics     │
                              │  (CAPEX as input)    │
                              └─────────────────────┘
```

- When `capex_source = 'modules'`: CAPEX auto-loaded from drilling + facilities
- When `capex_source = 'manual'`: Uses `capex_usd` from assumption
- Facilities are CAPEX inputs, not separate economic entities

---

## DCA Source Hierarchy

```
1. Well DCA params (dca_qi, dca_di from Well model)     ← highest priority
2. Type Curve (linked via assumption.type_curve_id)
3. Assumption Manual DCA (assumption.dca_qi, etc.)
4. Platform defaults (qi=500, di=0.05, b=0.5)           ← lowest priority
```

---

## Key Relationships

| Parent | Child | Relation | Cascade |
|--------|-------|----------|---------|
| Project | Field | 1:N | Delete fields on project delete |
| Field | Well | 1:N | Delete wells on field delete |
| Well | WellActivity | 1:N | CASCADE |
| Well | ProductionRecord | 1:N | CASCADE |
| Well | DrillingProfile | 1:N | CASCADE |
| DrillingProfile | SurveyStation | 1:N | CASCADE |
| DrillingProfile | CasingSection | 1:N | CASCADE |
| DrillingProfile | DrillString | 1:N | CASCADE |
| DrillString | StringComponent | 1:N | CASCADE |
| Project | EconomicAssumption | 1:N | CASCADE |
| Project | FacilitiesScenario | 1:N | CASCADE |
| Project | AFETemplate | 1:N | CASCADE |
| Project | ChatSession | 1:N | CASCADE |
| Field | WellGroup | 1:N | CASCADE |
| Field | Facility | 1:N | SET NULL |
