# Petroleum Engineering Domain Glossary

Comprehensive glossary for upstream oil & gas terminology used in the Netora Platform.

---

## Production & Reserves

| Term | Definition | Unit |
|------|-----------|------|
| **BOPD** | Barrels of Oil Per Day | bbl/day |
| **BFPD** | Barrels of Fluid Per Day (oil + water) | bbl/day |
| **BWPD** | Barrels of Water Per Day | bbl/day |
| **MSCFD** | Thousand Standard Cubic Feet per Day (gas) | Mscf/day |
| **MMSCFD** | Million Standard Cubic Feet per Day | MMscf/day |
| **MSTB** | Thousand Stock-Tank Barrels | Mstb |
| **MMSTB** | Million Stock-Tank Barrels | MMstb |
| **BOE** | Barrel of Oil Equivalent (6 Mscf gas = 1 BOE) | bbl |
| **EUR** | Estimated Ultimate Recovery — total recoverable volume | MSTB |
| **GOR** | Gas-Oil Ratio | scf/bbl |
| **BSW** | Basic Sediment & Water (water cut) | fraction or % |
| **WOR** | Water-Oil Ratio | bbl/bbl |
| **PI** | Productivity Index | bbl/day/psi |
| **IPR** | Inflow Performance Relationship | curve |
| **Cum Oil** | Cumulative oil production | MSTB |
| **WC** | Water Cut = water / (oil + water) | fraction |
| **Lift Method** | Artificial lift: ESP, rod pump, gas lift, plunger, natural flow | — |

## Decline Curve Analysis (DCA)

| Term | Definition | Unit |
|------|-----------|------|
| **DCA** | Decline Curve Analysis — Arps method | — |
| **qi** | Initial production rate | bopd |
| **di** | Initial nominal decline rate | fraction/month |
| **b** | Arps decline exponent (0=exponential, 0<b<2=hyperbolic, 1=harmonic) | dimensionless |
| **q_abandon** | Economic limit / abandonment rate | bopd |
| **d_eff** | Effective decline rate | fraction |
| **d_min** | Minimum decline rate (for modified hyperbolic) | fraction/year |
| **Type Curve** | Representative DCA profile for a well category | — |
| **History Match** | Fitting DCA parameters to actual production data | — |
| **Modified Hyperbolic** | Hyperbolic early, switching to exponential at d_min | — |

### Arps Equations
- **Exponential** (b=0): `q(t) = qi × e^(−di × t)`
- **Hyperbolic** (0<b<2): `q(t) = qi × (1 + b × di × t)^(−1/b)`
- **Harmonic** (b=1): `q(t) = qi / (1 + di × t)`

## Economics

| Term | Definition | Unit |
|------|-----------|------|
| **NPV** | Net Present Value | USD |
| **IRR** | Internal Rate of Return | % annual |
| **Payout** | Month when cumulative FCF turns positive | months |
| **Breakeven** | Oil price where NPV = 0 | $/bbl |
| **FCF** | Free Cash Flow = net income + DD&A − CAPEX | USD/month |
| **CAPEX** | Capital Expenditure (drilling + facilities) | USD |
| **OPEX** | Operating Expenditure | $/bbl or $/month |
| **DD&A** | Depreciation, Depletion & Amortization | USD/month |
| **EBIT** | Earnings Before Interest and Taxes | USD |
| **PI** | Profitability Index = NPV / CAPEX | ratio |
| **F&D** | Finding & Development cost = CAPEX / EUR | $/bbl |
| **Government Take** | Total government share: royalty + tax + IHI + equity | % |
| **Discount Rate** | Rate to discount future cash flows | % annual |
| **Sensitivity** | Tornado analysis: ±20% swing on key variables | USD (NPV impact) |
| **Carry** | One partner paying another's share of CAPEX | — |

### Fiscal Cascade (per period)
1. Gross Revenue = oil × price + gas × price
2. Royalty = gross_revenue × royalty_rate
3. IHI = (gross_revenue − royalty) × ihi_rate
4. OPEX = variable + fixed
5. DD&A = CAPEX / amortization_life
6. EBIT = revenue − royalty − IHI − OPEX − DD&A
7. Tax = max(0, EBIT × tax_rate)
8. Net Income = EBIT − tax
9. FCF = (net_income + DD&A) × partner_share − private_capex

## Fiscal Regimes

| Term | Definition |
|------|-----------|
| **Royalty** | Payment to the state based on gross production value |
| **IHI** | Impuesto de Hidrocarburos Inicial — extraction tax (Venezuela/Argentina) |
| **ISLR** | Impuesto Sobre La Renta — income tax (Venezuela) |
| **EMV** | Empresa Mixta — mixed enterprise / joint venture with state company |
| **PSC** | Production Sharing Contract |
| **R/T** | Royalty/Tax regime |
| **Service Contract** | Contractor receives fee; state owns production |
| **State Equity** | Government/NOC share in project equity |
| **Gov CAPEX Contribution** | Whether state pays its CAPEX share (1.0) or private carries (0.0) |
| **Windfall Tax** | Additional tax triggered by high oil prices |

### National Oil Companies
- **PDVSA** — Venezuela (Petróleos de Venezuela)
- **Ecopetrol** — Colombia
- **YPF** — Argentina
- **Petrobras** — Brazil
- **PetroPeru** — Peru
- **PetroEcuador** — Ecuador
- **YPFB** — Bolivia

## Monte Carlo & Risk

| Term | Definition |
|------|-----------|
| **P10** | 10th percentile — 90% probability of exceeding | optimistic |
| **P50** | 50th percentile — median / base case | base |
| **P90** | 90th percentile — 10% probability of exceeding | pessimistic |
| **Triangular Distribution** | Defined by low, mode (base), high | — |
| **EMV** | Expected Monetary Value = probability × NPV | USD |
| **COS** | Chance of Success | % |
| **Fan Chart** | Multiple simulation curves overlaid | — |
| **Tornado Chart** | Sensitivity bars sorted by impact | — |
| **p_drill** | Probability well is drilled (field MC) | 0–1 |
| **p_well_failure** | Post-drill failure probability | 0–1 |
| **Schedule Slip** | Delay in spud/first-oil dates | months |

## Drilling Engineering

| Term | Definition | Unit |
|------|-----------|------|
| **MD** | Measured Depth — along the wellbore | ft |
| **TVD** | True Vertical Depth | ft |
| **VS** | Vertical Section — projected horizontal distance | ft |
| **KOP** | Kickoff Point — where deviated well starts building angle | ft MD |
| **BUR** | Build-Up Rate | °/100ft |
| **DLS** | Dogleg Severity — rate of trajectory change | °/100ft |
| **Inc** | Inclination — angle from vertical | degrees |
| **Azm** | Azimuth — compass direction of wellbore | degrees |
| **BHA** | Bottom Hole Assembly | — |
| **PDC** | Polycrystalline Diamond Compact (bit type) | — |
| **ROP** | Rate of Penetration | ft/hr |
| **WOB** | Weight on Bit | klbs |
| **RPM** | Rotary Speed | rev/min |
| **SPP** | Standpipe Pressure | psi |
| **TFA** | Total Flow Area (bit nozzles) | in² |
| **HSI** | Hydraulic Horsepower per Square Inch | hp/in² |

### Survey
- **Minimum Curvature** — Standard method for computing wellbore position from survey stations
- **ISCWSA** — Industry Steering Committee on Wellbore Survey Accuracy (error model)
- **MWD** — Measurement While Drilling (survey tool)

### Hydraulics
| Term | Definition | Unit |
|------|-----------|------|
| **ECD** | Equivalent Circulating Density | ppg |
| **MW** | Mud Weight | ppg |
| **PV** | Plastic Viscosity | cP |
| **YP** | Yield Point | lb/100ft² |
| **HHP** | Hydraulic Horsepower | hp |
| **Jet Velocity** | Fluid velocity through bit nozzles | ft/s |

### Torque & Drag
| Term | Definition | Unit |
|------|-----------|------|
| **T&D** | Torque & Drag analysis | — |
| **FF** | Friction Factor | dimensionless |
| **BF** | Buoyancy Factor = 1 − (MW/65.5) | dimensionless |
| **Hookload** | Weight measured at surface | klbs |
| **Surface Torque** | Rotational force at surface | ft-lbs |

## Casing & Completion

| Term | Definition |
|------|-----------|
| **Conductor** | First (outermost) casing string — 20" to 30" |
| **Surface Casing** | Second string — protects fresh water zones — 13⅜" |
| **Intermediate** | Third string — isolates problem zones — 9⅝" |
| **Production Casing** | Final string — across pay zone — 7" or 5½" |
| **Liner** | Casing that doesn't extend to surface |
| **Cement** | Annular fill between casing and formation |
| **Shoe** | Bottom of a casing string (shoe depth = setting depth) |

## Facilities

| Term | Definition |
|------|-----------|
| **CPF** | Central Processing Facility |
| **FWKO** | Free Water Knockout |
| **Separator** | Vessel that separates oil, gas, and water |
| **Heater Treater** | Heated vessel for emulsion breaking |
| **Dehydrator** | TEG glycol unit for gas dehydration |
| **Compressor** | Boosts gas pressure for sales or injection |
| **Flare** | Burns excess gas safely |
| **Metering** | Production measurement equipment |
| **CEPCI** | Chemical Engineering Plant Cost Index (cost escalation) |
| **Lang Factor** | Multiplier from equipment cost to installed cost (default 4.0) |
| **Six-Tenths Rule** | Cost scaling: C = C_ref × (Cap/Cap_ref)^0.6 |
| **Souders-Brown** | Method for sizing separator vessels |

## Well Types

| Type | Description |
|------|-------------|
| **Vertical** | Straight down, Inc < 5° |
| **Deviated** | Directional, reaches offset target |
| **Horizontal** | Inc ≈ 90° through pay zone, lateral section |
| **Multilateral** | Multiple laterals from single wellbore |

## Well Status

| Status | Meaning |
|--------|---------|
| **Planned** | Not yet drilled |
| **Drilling** | Currently being drilled |
| **Producing** | Active, flowing or on artificial lift |
| **Shut-in** | Completed but not producing |
| **Abandoned** | Permanently plugged and abandoned |

## Formations (Common)

| Basin | Key Formations |
|-------|---------------|
| **Lake Maracaibo** | La Rosa, Lagunillas, Bachaquero, Misoa, Eoceno |
| **Permian Basin** | Wolfcamp, Spraberry, Bone Spring, Delaware |
| **Eagle Ford** | Eagle Ford Shale (upper/lower) |
| **Llanos (Colombia)** | Carbonera, Guadalupe, Barco |
| **Neuquén (Argentina)** | Vaca Muerta, Quintuco |

## Units Conversion

| From | To | Factor |
|------|----|--------|
| 1 bbl | gallons | × 42 |
| 1 bbl | cubic feet | × 5.615 |
| 6 Mscf gas | 1 BOE | industry standard |
| 1 month | days | 30.44 (platform constant) |
| ppg → psi/ft | × 0.052 | hydrostatic gradient |
| °F → °R | + 460 | Rankine |
