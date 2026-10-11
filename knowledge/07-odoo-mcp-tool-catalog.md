# Netora Odoo MCP — Tool Catalog (read-only)

Reference of the **41 tools** of the Netora Odoo MCP (`netora-odoo-mcp`), generated from its registry.
All tools are read-only (`readOnlyHint: true`); none creates, modifies or deletes data.

Connection: Claude.ai → Settings → Connectors → custom connector, URL `https://<host-del-mcp>/mcp`,
authentication *Bearer token* with your personal `nom_…` token (issued per person by the administrator with
`netora-odoo-mcp tokens create --user <name>`). Never paste a token in a prompt, a URL or a document.

Conventions: every response has `as_of`, `source: "odoo"`, `read_only: true`, `units` (per field),
`data_origin` (`flagged` = synthetic rows excluded by Odoo, `unflagged` = model has no flag yet) and optional
`notes`. Lists: `limit` (≤ 500) + `cursor`/`next_cursor`, `total`. Dates: ISO `YYYY-MM-DD`.
`well` / `field` / `job` / `contract` / `rig` accept an id or a name.

## 1. Discovery and master data (9)

| Tool | Args | Returns |
|---|---|---|
| `odoo_whoami` | — | Odoo identity (`mcp_readonly`, groups, readable models, synthetic exclusion), MCP identity, tool count |
| `list_fields` | `country?` (US, CO, AR, VE, BR, PE, EC, BO), `name_like?`, `upstream_project_id?`, `limit`, `cursor` | fields + well counts + Upstream ids |
| `get_field` | `field` | header, pads, facilities, wells by state, dashboard KPIs (today/MTD/YTD) |
| `list_wells` | `field?`, `state?`, `well_type?`, `name_like?`, `has_upstream_link?`, paging | wells |
| `get_well` | `well` | header, wellbores, last forecast, latest production, active jobs, Upstream ids / `netora_uid` |
| `list_rigs` | `name_like?`, `include_inactive?` | rigs with day rate |
| `list_facilities` | `field?`, `facility_type?`, `state?` | facilities |
| `list_assets` | `field?`, `facility?`, `well?`, `asset_type?`, `state?`, `criticality?` | production assets |
| `search_records` | `model` (netora.* only), `domain?`, `fields?`, `order?`, paging | guarded generic read (no binaries) |

## 2. Drilling (13)

| Tool | Args | Returns |
|---|---|---|
| `list_drilling_jobs` | `state?`, `well?`, `field?`, `rig?`, `client_name?`, `date_from?`, `date_to?` | jobs |
| `get_drilling_job` | `job` | header, totals (days, footage ft, hours, NPT %, depth), wellbores/sections/phases, AFE, invoices, costs by currency |
| `list_workdays` | `job`, `date_from?`, `date_to?` | DDR index (depth in/out, footage, hours, ROP, cost, locked) |
| `get_ddr` | `workday_id` or `job` + `date` | full DDR: activities, parameters, mud, tests, cement, BHA in hole, costs, HSE |
| `get_activity_breakdown` | `job`, `date_from?`, `date_to?`, `group_by` (code, phase, npt) | hours/footage per group, NPT % |
| `get_bha_runs` | `job`, `include_components` | BHAs, components, bit and motor details |
| `get_surveys` | `job` or `wellbore_id`, `md_from?`, `md_to?` | survey stations + plan deltas |
| `get_well_plan` | `well` | plan stations, targets, imported drilling plan (days, cost, day-vs-depth) |
| `get_casing_program` | `job` or `well` | casing, tally totals, cement jobs, pressure tests |
| `get_mud_report` | `job`, `date_from?`, `date_to?` | mud checks series, volume balance per day |
| `get_hse_summary` | `job` or `field`, `date_from?`, `date_to?` | incidents and observations with counts |
| `get_drilling_plan_vs_actual` | `well` or `field` | drilling PvA computed by Odoo (unit/currency caveats) |
| `get_equipment` | `serial?`, `state?`, `job?`, `item_type?`, `maintenance_due?` | serialized equipment, usage, maintenance |

## 3. Contracts and costs (4)

| Tool | Args | Returns |
|---|---|---|
| `list_contracts` | `client_name?`, `state?`, `active_on?` | contracts |
| `get_contract` | `contract` | terms, sale order + lines, jobs that consumed it, cost totals |
| `get_daily_costs` | `job?`, `contract?`, `date_from?`, `date_to?`, `invoiced?`, `group_by` (day, term, phase, section, bha) | costs with totals per currency |
| `get_job_invoicing_status` | `job` | invoices, uninvoiced cost, AFE vs actual |

## 4. Production / E&P (12)

| Tool | Args | Returns |
|---|---|---|
| `get_daily_production` | `well` or `field`, `date_from?`, `date_to?` (default 30 d) | daily rows (bbl/d, Mcf/d, pressures, hours on) |
| `get_production_summary` | `field` and/or `wells`, window (90 d), `granularity`, `group_by` | calendar aggregates and averages |
| `get_well_tests` | `well` or `field`, window (365 d) | well tests |
| `get_downtime` | `well` or `field`, window (90 d) | events + totals by failure mode |
| `get_tank_and_tickets` | `field` or `tank`, window (30 d) | tank gauges, run tickets, net bbl |
| `get_dca_forecast` | `well`, `which` (approved, latest, upstream, manual, all), `include_series` | Arps parameters, EUR, series, source |
| `get_production_plan_vs_actual` | `well` or `field` | production PvA computed by Odoo |
| `get_mc_results` | `well` or `field`, `limit`, `include_profiles` | P10/P50/P90 |
| `get_field_ops` | `field`, window | open WOs by priority, overdue maintenance, inspections, assignments |
| `list_work_orders` | `field?`, `asset?`, `well?`, `state?`, `priority?`, `wo_type?`, window | work orders |
| `list_inspections` | `field?`, `asset?`, `well?`, `facility?`, `result?`, `state?`, window, `include_results` | inspections |
| `get_allocation` | `field`, `period?` (YYYY-MM) | production allocation and lines |

## 5. Integration and data quality (3)

| Tool | Args | Returns |
|---|---|---|
| `get_upstream_sync_status` | `limit?` | latest Upstream → Odoo imports, unmatched wells |
| `find_upstream_link` | `well` or `upstream_well_id` or `netora_uid` | cross ids to chain with the Netora Upstream MCP |
| `data_quality_report` | `field?`, `stale_days` | consistency report computed by Odoo |

## Units

Drilling depths/footage **ft**, hours **h**, ROP **ft/h**, mud weight **ppg**, pressures **psi**; production
**bbl/d**, **Mcf/d**, **boe/d**; well header depths `*_m` in **m**; EUR **Mstb**; daily costs in the
**contract currency** (no USD conversion stored yet). Each response repeats the units of its own fields.
