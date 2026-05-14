# Example: Venezuela EMV Analysis

Empresa Mixta (EMV) project with PDVSA 51% equity, full fiscal analysis, Monte Carlo with country risk.

---

## Scenario

You're evaluating a Lake Maracaibo development project as a 49% private partner in an Empresa Mixta with PDVSA (51%). 10 vertical wells targeting the Misoa formation.

---

## Step 1 — Create the Project

**You say:**
```
Create a project:
- Name: "Petrocabimas EMV"
- Country: VEN

Field: "Cabimas LLS"
  Location: lat 10.41, lon -71.45

Wells (10 vertical):
- TJ-001 through TJ-010
- qi: 200-400 bopd range (varied)
- di: 0.04-0.06/month
- b: 0.3-0.5
- capex: $2.5-3.5MM each
- formation: Misoa
- spud dates: 2026-07 through 2027-06 (staggered monthly)

Assumption: "EMV Base Case"
- Oil: $65/bbl (Merey basket discount)
- OPEX: $15/bbl
- Royalty: 20%
- IHI: 10%
- ISLR: 34%
- PDVSA equity: 51%
- Gov CAPEX contribution: 1.0 (PDVSA pays pro-rata)
- Discount: 15% (includes country risk premium)
```

Claude creates everything in sequence.

---

## Step 2 — Fiscal Analysis

**You say:**
```
Show me the fiscal cascade for this project. What's the total government take?
Break down: how much goes to royalty, IHI, ISLR, and PDVSA equity share?
```

**Claude response example:**

### Government Take Breakdown (Life of Project)

| Component | Amount (MM) | % of Revenue |
|-----------|-------------|-------------|
| Royalty | $12.8 | 20.0% |
| IHI | $10.2 | 16.0% |
| ISLR (Income Tax) | $7.8 | 12.2% |
| PDVSA Equity Share | $19.5 | 30.5% |
| **Total Gov Take** | **$50.3** | **78.7%** |
| **Partner Share** | **$13.7** | **21.3%** |

> "Government take of 78.7% is typical for Venezuela EMV contracts. The private partner receives 21.3% of total value. Note: IHI applies after royalty deduction, which is why the cascade matters."

---

## Step 3 — Country Fiscal Comparison

**You say:**
```
Compare this same asset under Venezuela EMV, Colombia, and USA fiscal regimes.
Use the same well parameters but apply each country's defaults.
Which country gives the best partner returns?
```

**Claude calls:** `fiscal_compare(country_codes=["VEN", "COL", "USA"], ...)`

| Metric | Venezuela (EMV) | Colombia | USA |
|--------|----------------|----------|-----|
| Royalty | 20% | 12% | 12.5% |
| IHI | 10% | 0% | 0% |
| Tax | 34% | 34% | 21% |
| State Equity | 51% | 20% | 0% |
| **Gov Take** | **78.7%** | **55%** | **31%** |
| Partner NPV | $3.2 MM | $8.5 MM | $14.1 MM |
| Partner IRR | 12% | 25% | 42% |

> "The same asset generates 4.4x more partner NPV in the USA vs Venezuela, driven primarily by PDVSA's 51% equity claim and the IHI tax."

---

## Step 4 — Monte Carlo with Country Risk

**You say:**
```
Run Monte Carlo for Cabimas LLS field:
- Oil price: $45 / $65 / $85 (wider range — Venezuela discount)
- qi multiplier: 0.6 / 1.0 / 1.4 (mature field uncertainty)
- Schedule slip: 0 / 4 / 12 months (operational delays)
- Per-well drill probability: 0.85 (equipment/logistics risk)
- Per-well failure: 0.10 (old wells, mechanical issues)
- 1000 simulations

This is Venezuela — use higher uncertainty ranges.
```

**Result:**

| Metric | P10 | P50 | P90 | Mean |
|--------|-----|-----|-----|------|
| Partner NPV (MM) | -$2.1 | $3.2 | $9.8 | $3.5 |
| Partner IRR | -5% | 12% | 28% | 13% |
| EUR (MSTB) | 380 | 620 | 920 | 640 |
| Wells Drilled | 7 | 9 | 10 | 8.5 |

**Probability of positive NPV (for partner): 68%**

---

## Step 5 — EMV (Expected Monetary Value)

**You say:**
```
Calculate the EMV for this project. What's the risk-adjusted value?
Consider: 80% chance the project proceeds, 20% chance it doesn't (political risk).
```

**Claude calculates:**
- Project EMV = 0.80 × P50 NPV ($3.2MM) + 0.20 × ($0) = **$2.56 MM**
- Risk-adjusted P50 including all uncertainties: **$2.56 MM**

> "Even with 20% non-proceed risk and Venezuelan fiscal terms, the EMV is positive at $2.56 MM. However, the 68% probability of positive NPV means there's a 32% chance the partner loses money. This is marginal — proceed only if the partner has strong operational capabilities in Venezuela."

---

## Step 6 — Investment Memo

**You say:**
```
Generate an investment memo for this Venezuelan EMV project.
Highlight the fiscal burden, country risk, and recommendation.
```

Claude generates a structured memo covering:
1. **Executive Summary:** Marginal returns but positive EMV
2. **Fiscal Framework:** 78.7% government take under EMV
3. **Risk:** 68% probability positive NPV; oil price and schedule are key risks
4. **Recommendation:** Conditional proceed — requires firm oil price above $55/bbl and PDVSA cooperation commitment

---

## Key Takeaways

- Venezuela EMV projects have high government take (~79%) but can still be economic
- IHI tax is unique to Venezuela and significantly impacts returns
- Always use a country risk premium (5-10%) in the discount rate
- Monte Carlo is essential — deterministic analysis alone would miss the 32% downside
- Compare against other countries to demonstrate opportunity cost to the board
