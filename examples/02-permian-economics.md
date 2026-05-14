# Example: Permian Basin Full Economics

Complete economics + Monte Carlo + sensitivity analysis for an existing project.

---

## Scenario

You already have a Permian Basin project in Netora with 2 fields and 8 horizontal wells. You want a full investment analysis.

---

## Step 1 — Project Overview

**You say:**
```
Give me a full overview of my Permian Basin project.
```

**Claude calls:** `get_project_full_data(project_id=25)`

**Claude responds:**
> "Your project 'Permian Basin Phase 1' has 2 fields (Delaware Basin North, Midland Basin South) with 8 horizontal wells total. Combined CAPEX is $55.9 MM. Current assumption: Base Case USA at $72/bbl."

---

## Step 2 — Full Economics Run

**You say:**
```
Run economics for both fields. Show NPV, IRR, payout, and government take for each.
Then compare them side by side.
```

Claude runs field economics for each field and presents:

| Metric | Delaware Basin North | Midland Basin South | **Total Project** |
|--------|---------------------|---------------------|-------------------|
| Wells | 4 | 4 | 8 |
| CAPEX | $29.4 MM | $26.5 MM | $55.9 MM |
| EUR | 1,250 MSTB | 1,050 MSTB | 2,300 MSTB |
| Peak Rate | 3,100 bopd | 2,500 bopd | 5,600 bopd |
| NPV₁₀% | $18.5 MM | $14.2 MM | $32.7 MM |
| IRR | 38% | 34% | 36% |
| Payout | 14 mo | 16 mo | 15 mo |
| F&D | $23.52/bbl | $25.24/bbl | $24.30/bbl |

---

## Step 3 — Sensitivity Analysis

**You say:**
```
What's the biggest risk to the project economics? Show me a tornado chart.
```

Claude extracts sensitivity from the economics runs:

| Variable | -20% NPV | Base NPV | +20% NPV | Impact |
|----------|----------|----------|----------|--------|
| Oil Price | $14.8 MM | $32.7 MM | $50.6 MM | $35.8 MM |
| CAPEX | $43.9 MM | $32.7 MM | $21.5 MM | $22.4 MM |
| OPEX | $37.2 MM | $32.7 MM | $28.2 MM | $9.0 MM |
| Royalty | $36.5 MM | $32.7 MM | $28.9 MM | $7.6 MM |
| Tax Rate | $35.1 MM | $32.7 MM | $30.3 MM | $4.8 MM |

> "Oil price is by far the biggest driver. A 20% drop ($72→$58) cuts NPV by $18MM. CAPEX is second — cost overruns of 20% reduce NPV by $11MM."

**Breakeven oil price: $42/bbl** — well below current market.

---

## Step 4 — Monte Carlo Risk Assessment

**You say:**
```
Run Monte Carlo for the whole Delaware Basin North field:
- Oil price: $55 / $72 / $95
- qi multiplier: 0.7 / 1.0 / 1.3
- schedule slip: 0 / 2 / 6 months
- per-well drill probability: 0.95
- 1000 simulations

Show P10/P50/P90 and probability of positive NPV.
```

**Result:**

| Metric | P10 | P50 | P90 | Mean |
|--------|-----|-----|-----|------|
| NPV (MM) | $4.5 | $18.2 | $35.8 | $19.1 |
| EUR (MSTB) | 850 | 1,250 | 1,700 | 1,280 |
| Peak Rate (bopd) | 2,200 | 3,100 | 4,000 | 3,120 |

**Probability of positive NPV: 92%**

> "Even in the P10 case (pessimistic), the project generates $4.5MM NPV. The 92% probability of positive returns indicates this is a low-risk development."

---

## Step 5 — Executive Summary

**You say:**
```
Now generate a 1-page investment memo for this project. Include all the data you just analyzed.
```

Claude generates a formatted memo with:
1. Executive Summary
2. Key Metrics Table
3. Risk Assessment (P10/P50/P90)
4. Top Sensitivities
5. Recommendation

---

## Key Takeaways

- Full project economics in ~3 minutes of conversation
- Monte Carlo confirms high probability of commercial success
- Oil price is the primary risk — but breakeven at $42/bbl provides strong downside protection
- Delaware Basin North outperforms Midland Basin South on NPV and IRR
