# Skill: Odoo Operations Review (read-only) — Netora Odoo MCP

## When to Use

- You need **actual** field data (what really happened): daily drilling reports, costs, daily production,
  work orders, inspections, contracts — all of which live in **Netora Odoo**, not in Netora Upstream.
- Plan vs actual: compare the Upstream plan/forecast with the Odoo actuals of the same well.
- Data quality checks before trusting a report (wells without Upstream link, silent jobs, synthetic data).

The Netora Odoo MCP is **read-only**: it exposes **41 tools** and cannot create, modify or delete anything.
Writes (production entry, work orders, notes) are out of scope until the "safe writes" phase.

## Prerequisites

- Connector **Netora Odoo** added in Claude.ai (URL `https://<host-del-mcp>/mcp`, your personal
  `nom_…` bearer token) or the stdio server in Claude Code. See `knowledge/07-odoo-mcp-tool-catalog.md`.
- For cross-system questions, the **Netora Upstream** connector as well.

## Prompt

```
Review drilling job [JOB_NUMBER] in Netora Odoo.

1. Job header and totals (days reported, footage, hours, NPT %, current depth, AFE budget vs actual).
2. Daily drilling reports of the last 7 days: depth in/out, footage, ROP, cost of the day.
3. Activity breakdown by code and NPT share; list the NPT activities with their comments.
4. BHA runs and their performance (footage, hours, reason to pull).
5. Daily costs by contract term and currency; what is still not invoiced.
6. HSE: incidents and observations of the job.
7. Drilling plan vs actual (time vs depth) and whether the job is ahead or behind.

Quote every number with its unit as returned by the tools. If a tool returns nothing, say so.
```

Spanish variant:

```
Revisa el job de perforación [JOB_NUMBER] en Netora Odoo: cabecera y totales, DDR de los últimos 7 días,
desglose de actividades y % NPT, BHAs, costos diarios por término y moneda (y lo no facturado), HSE y plan
vs real. Cita cada cifra con su unidad; si una herramienta no devuelve datos, dilo.
```

## What Claude Does

1. `odoo_whoami()` → confirms the read-only identity and whether synthetic data is excluded.
2. `get_drilling_job(job)` → header + `summary` (days, footage, hours, NPT %, AFE, costs by currency).
3. `list_workdays(job, date_from, date_to)` → DDR index; `get_ddr(job, date)` for the days that matter.
4. `get_activity_breakdown(job, group_by="code")` and `group_by="npt"`.
5. `get_bha_runs(job)` · `get_daily_costs(job, group_by="term")` · `get_job_invoicing_status(job)`.
6. `get_hse_summary(job)` · `get_drilling_plan_vs_actual(well)`.
7. Writes the review with the `units` of each response; flags the `notes` (e.g. costs in contract currency).

## Chaining with Netora Upstream (plan vs actual across systems)

```
Compare the Upstream forecast of well [WELL] with its actual production in Odoo for the last 6 months.
```

1. `find_upstream_link(well="[WELL]")` → `upstream_well_id`, `upstream_project_id`.
2. Netora Upstream: `get_well_detail(well_id=upstream_well_id)` / `well_actual_vs_forecast(well_id=…)`.
3. Netora Odoo: `get_production_summary(wells=["[WELL]"], date_from, date_to, granularity="month")`
   and `get_production_plan_vs_actual(well="[WELL]")`.
4. Report both series side by side; never scale or extrapolate a number yourself.

## Tips

- `well`, `field`, `job`, `contract` accept an id or a name; ambiguous names return the candidates.
- Lists are paginated (`limit` ≤ 500, `next_cursor`); time series take `date_from`/`date_to`.
- Drilling depths are in **feet**; well header depths (`*_m`) in metres; costs in the **contract currency**.
- `data_quality_report(field)` first when numbers look odd (field mismatches, stale production, unmatched
  Upstream wells, synthetic-data filter status).
- `search_records(model, domain, fields)` is the guarded escape hatch for any `netora.*` model.
