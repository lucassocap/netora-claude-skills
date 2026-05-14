# Skill: Create Project from Scratch

## When to Use

- Setting up a new E&P project in the platform
- Migrating data from spreadsheets
- Creating a demo/test project
- Starting a new country evaluation

## Prerequisites

- Know the project parameters: country, field names, well names, DCA, CAPEX

## Prompt

```
Create a new project in Netora with the following data:

Project: [PROJECT_NAME]
Country: [COUNTRY_CODE]

Field 1: [FIELD_NAME]
  Location: lat [X], lon [Y]
  Wells:
  - [WELL_1]: type=[vertical/horizontal], qi=[X] bopd, di=[Y]/month, b=[Z], capex=$[N]MM, spud=[YYYY-MM-DD]
  - [WELL_2]: type=[type], qi=[X], di=[Y], b=[Z], capex=$[N]MM, spud=[YYYY-MM-DD]
  [... more wells]

Field 2: [FIELD_NAME]
  [... same format]

Assumptions (Base Case):
  Oil price: $[X]/bbl
  Gas price: $[Y]/Mscf
  OPEX: $[Z]/bbl
  Royalty: [X]%
  Income tax: [Y]%
  Discount rate: [Z]%
  [Country-specific: IHI, state equity, etc.]

After creating everything, show me the project summary to verify.
```

**Example:**

```
Create a new project:

Project: "Permian Basin Development"
Country: USA

Field: "Delaware Basin North"
  Location: lat 31.85, lon -104.20
  Wells:
  - DBN-001H: horizontal, qi=800, di=0.06, b=0.8, capex=$7.5MM, spud=2026-07-01
  - DBN-002H: horizontal, qi=750, di=0.055, b=0.8, capex=$7.2MM, spud=2026-08-15
  - DBN-003H: horizontal, qi=850, di=0.065, b=0.7, capex=$7.8MM, spud=2026-10-01
  - DBN-004H: horizontal, qi=700, di=0.05, b=0.9, capex=$6.9MM, spud=2026-11-15

Assumptions: oil $72/bbl, gas $3.2/Mscf, OPEX $10/bbl, royalty 18.75%, tax 21%, discount 10%

After setup, verify and show the full project summary.
```

## What Claude Does

1. `create_project(name, country_code)` → project ID
2. `create_field(project_id, name, lat, lon)` → field ID
3. `create_wells(field_id, wells=[...])` → well IDs
4. `create_assumption(project_id, name, ...)` → assumption ID
5. `get_project_full_data(project_id)` → verify everything

## Tips

- Claude can create dozens of wells in a single call
- Include `opex_usd_bbl` per well if it varies
- Set `first_oil_date` for proper field forecast scheduling
- After creation, ask "Run economics for this project" to get immediate results
