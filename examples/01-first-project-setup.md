# Example: First Project Setup

Create a Permian Basin development project from scratch with 2 fields, 8 wells, DCA parameters, and economics.

---

## Step 1 — Create the Project

**You say:**
```
Create a new project called "Permian Basin Phase 1" in the USA.
```

**Claude calls:** `create_project(name="Permian Basin Phase 1", country_code="USA")`

**Claude responds:** "Created project 'Permian Basin Phase 1' (ID: 25) in the USA."

---

## Step 2 — Add Fields

**You say:**
```
Add two fields:
1. "Delaware Basin North" at lat 31.85, lon -104.20
2. "Midland Basin South" at lat 31.95, lon -101.90
```

**Claude calls:**
- `create_field(project_id=25, name="Delaware Basin North", center_lat=31.85, center_lon=-104.20)`
- `create_field(project_id=25, name="Midland Basin South", center_lat=31.95, center_lon=-101.90)`

---

## Step 3 — Add Wells

**You say:**
```
Add 4 horizontal wells to Delaware Basin North:
- DBN-001H: qi=800, di=0.06, b=0.8, capex=$7.5MM, spud 2026-07-01, Wolfcamp A
- DBN-002H: qi=750, di=0.055, b=0.8, capex=$7.2MM, spud 2026-08-15, Wolfcamp A
- DBN-003H: qi=850, di=0.065, b=0.7, capex=$7.8MM, spud 2026-10-01, Wolfcamp B
- DBN-004H: qi=700, di=0.05, b=0.9, capex=$6.9MM, spud 2026-11-15, Wolfcamp B

Add 4 horizontal wells to Midland Basin South:
- MBS-001H: qi=600, di=0.05, b=0.9, capex=$6.5MM, spud 2026-09-01, Spraberry
- MBS-002H: qi=650, di=0.055, b=0.85, capex=$6.8MM, spud 2026-10-15, Spraberry
- MBS-003H: qi=550, di=0.045, b=0.95, capex=$6.2MM, spud 2027-01-01, Bone Spring
- MBS-004H: qi=700, di=0.06, b=0.8, capex=$7.0MM, spud 2027-03-01, Bone Spring

All wells: OPEX $10/bbl, status=planned
```

**Claude calls:** Two `create_wells()` calls with 4 wells each.

---

## Step 4 — Create Economic Assumptions

**You say:**
```
Create a base case assumption:
- Oil price: $72/bbl
- Gas price: $3.20/Mscf
- OPEX: $10/bbl
- Fixed OPEX: $25,000/month
- Royalty: 18.75% (private mineral rights)
- Income tax: 21%
- Discount rate: 10%
```

**Claude calls:** `create_assumption(project_id=25, name="Base Case USA", country="USA", oil_price_usd_bbl=72, ...)`

---

## Step 5 — Verify Setup

**You say:**
```
Show me the full project summary to verify everything is correct.
```

**Claude calls:** `get_project_full_data(project_id=25)`

**Claude responds with a summary table like:**

| Item | Count/Value |
|------|------------|
| Fields | 2 |
| Total Wells | 8 |
| Status | All planned |
| Avg qi | 700 bopd |
| Total CAPEX | $55.9 MM |
| Assumption | Base Case USA |

---

## Step 6 — Run Economics

**You say:**
```
Run field economics for both fields and show me a comparison.
```

**Claude calls:**
- `run_field_economics(field_id=X, assumption_id=Y)` for Delaware Basin North
- `run_field_economics(field_id=Z, assumption_id=Y)` for Midland Basin South

**Example results:**

| Metric | Delaware Basin North | Midland Basin South |
|--------|---------------------|---------------------|
| Total CAPEX | $29.4 MM | $26.5 MM |
| Peak Rate | 3,100 bopd | 2,500 bopd |
| EUR | 1,250 MSTB | 1,050 MSTB |
| NPV₁₀% | $18.5 MM | $14.2 MM |
| IRR | 38% | 34% |
| Payout | 14 months | 16 months |
| Gov Take | 35% | 35% |

---

## Step 7 — Run Monte Carlo

**You say:**
```
Run Monte Carlo for Delaware Basin North with:
- qi multiplier: 0.7 / 1.0 / 1.3
- oil price: $55 / $72 / $95
- 1000 simulations

What's the probability of making money?
```

**Example result:**
- P50 NPV: $18.2 MM
- Probability of positive NPV: 92%
- P10: $4.5 MM | P90: $35.8 MM

---

## Total Time

This entire setup takes about 5 minutes of conversation with Claude. Compare that to hours of manual data entry in spreadsheets.
