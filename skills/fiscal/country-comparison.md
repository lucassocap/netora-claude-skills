# Skill: Country Fiscal Comparison

## When to Use

- Evaluating which country offers best returns for same asset
- Partner negotiations on fiscal terms
- Board presentation on country entry strategy
- Understanding government take across jurisdictions

## Prerequisites

- None — uses platform's built-in fiscal defaults per country

## Prompt

```
Compare the fiscal regimes of [COUNTRY_1], [COUNTRY_2], and [COUNTRY_3] for a standard well with:
- Production: [X] bopd initial rate
- CAPEX: $[Y] million
- OPEX: $[Z] per barrel
- Oil price: $[W] per barrel

Show side-by-side:
1. Fiscal parameters (royalty, tax, IHI, state equity)
2. Government take percentage
3. Partner NPV and IRR
4. Payout period
5. Which country offers the best risk-adjusted returns?

Use the platform's default fiscal parameters for each country.
```

**Example:**

```
Compare the fiscal regimes of Venezuela (EMV), Colombia, and USA
for a well producing 500 bopd, $5MM CAPEX, $12/bbl OPEX, at $70/bbl oil price.

Show government take, partner NPV, partner IRR side by side.
Which country gives the best returns to the private partner?
```

## What Claude Does

1. `fiscal_compare(country_codes=["VEN", "COL", "USA"])` → side-by-side
2. Or runs economics individually per country with different assumptions
3. Presents comparative table with recommendation

## Example Output

| Metric | USA | Colombia | Venezuela (EMV) |
|--------|-----|----------|----------------|
| Royalty | 12.5% | 12.0% | 20.0% |
| Income Tax | 21.0% | 34.0% | 34.0% |
| IHI | 0% | 0% | 10.0% |
| State Equity | 0% | 20% | 51% |
| **Gov Take** | **31%** | **55%** | **78%** |
| Partner NPV | $5.8 MM | $3.2 MM | $1.1 MM |
| Partner IRR | 45% | 28% | 14% |
| Payout | 12 mo | 20 mo | 38 mo |

## Tips

- Always specify the contract type for Venezuela (EMV, CPP, or Servicios)
- Ask for "net-back analysis" to see revenue per barrel by country
- "Include above-ground risk factors" for qualitative risk overlay
- Available country codes: USA, VEN, COL, ARG, BRA, PER, ECU, BOL
