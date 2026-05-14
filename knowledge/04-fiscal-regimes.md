# Fiscal Regimes — 8-Country Reference

Detailed fiscal parameters for each country supported by the Netora Upstream Platform.

---

## Summary Table

| Country | Code | Royalty | IHI | Income Tax | State Equity | NOC | Discount Rate |
|---------|------|--------|-----|------------|-------------|-----|---------------|
| USA | USA | 12.5% | 0% | 21% | 0% | — | 10% |
| Venezuela | VEN | 20% | 10% | 34% | 51% | PDVSA | 10% |
| Colombia | COL | 12% | 0% | 34% | 20% | Ecopetrol | 12% |
| Argentina | ARG | 15% | 8% | 34% | 12% | YPF | 10% |
| Brazil | BRA | 10% | 5% | 34% | 30% | Petrobras | 12% |
| Peru | PER | 10% | 0% | 29.5% | 0% | PetroPeru | 10% |
| Ecuador | ECU | 20% | 0% | 25% | 0% | PetroEcuador | 10% |
| Bolivia | BOL | 18% | 0% | 25% | 0% | YPFB | 12% |

---

## USA

**Regime:** Royalty/Tax (R/T)
**Year:** Current federal/state framework

| Parameter | Default | Notes |
|-----------|---------|-------|
| Royalty | 12.5% | Federal lands; private lands typically 12.5-25% |
| Income Tax | 21% | Federal corporate rate (post-TCJA) |
| IHI | 0% | No extraction tax at federal level |
| State Equity | 0% | No government participation |
| Discount Rate | 10% | Industry standard |
| OPEX | $12/bbl | Varies by basin: Permian ~$8-15, offshore ~$15-25 |
| Oil Price | $70/bbl | WTI reference |

**Notes:**
- State severance taxes vary: Texas 4.6%, New Mexico 5.65%, North Dakota 5%+6.5%
- Federal royalty rate on new leases: 16.67% (increased from 12.5% in 2022)
- IDC (Intangible Drilling Costs) 100% deductible in year 1
- Percentage depletion: 15% of gross income for small producers

---

## Venezuela (VEN)

**Regime:** Empresa Mixta (LOH 2026)
**Year:** Ley Orgánica de Hidrocarburos framework

### Contract Types

| Contract | Label | Royalty | Tax | IHI | PDVSA Equity |
|----------|-------|--------|-----|-----|-------------|
| **EMV** | Empresa Mixta | 20% | 34% | 10% | 51% |
| **CPP** | Contrato de Participación Privada | 15% | 34% | 8% | 30% |
| **Servicios** | Contrato de Servicios | 20% | 34% | 0% | 0% |

### Default Parameters (EMV)

| Parameter | Default | Notes |
|-----------|---------|-------|
| Royalty | 20% | On gross revenue |
| IHI | 10% | Impuesto de Hidrocarburos Inicial — on revenue after royalty |
| Income Tax (ISLR) | 34% | Impuesto Sobre La Renta |
| PDVSA Equity | 51% | Minimum state participation |
| Gov CAPEX Contribution | 1.0 | PDVSA pays pro-rata (varies by contract) |
| Discount Rate | 10% | |
| OPEX | $12-18/bbl | Lake Maracaibo operations |

**Fiscal Cascade:**
1. Gross Revenue
2. − Royalty (20% of gross)
3. = Revenue After Royalty (RAR)
4. − IHI (10% of RAR)
5. − OPEX − DD&A
6. = EBIT
7. − ISLR (34% of EBIT, if positive)
8. = Net Income
9. × Partner share (49%) = Partner FCF
10. − Private CAPEX

**Notes:**
- IHI applies AFTER royalty deduction (not on gross)
- PDVSA minimum 51% equity is constitutional requirement
- Country risk premium: consider 5-10% additional discount rate
- FX risk: dual exchange rate regime affects repatriation
- Key basins: Lake Maracaibo, Orinoco Belt, Eastern Venezuela

---

## Colombia (COL)

**Regime:** Royalty/Tax + Ecopetrol participation
**Year:** Current ANH framework

| Parameter | Default | Notes |
|-----------|---------|-------|
| Royalty | 12% | Variable by production: 8% (<5000 bopd) to 25% (>600,000 bopd) |
| Income Tax | 34% | Corporate rate |
| IHI | 0% | No extraction tax |
| Ecopetrol Equity | 20% | Typical in E&P contracts |
| Discount Rate | 12% | |
| OPEX | $10-15/bbl | Llanos ~$10, offshore ~$20 |

**Notes:**
- Sliding-scale royalty based on daily production
- "Precio de Gobierno" — price mechanism for royalty calculation
- Ecopetrol participation varies by block/round
- Key basins: Llanos, Middle Magdalena Valley, offshore Caribbean
- Additional surcharge on profits above threshold

---

## Argentina (ARG)

**Regime:** Royalty/Tax + provincial participation
**Year:** Post-2023 hydrocarbon law framework

| Parameter | Default | Notes |
|-----------|---------|-------|
| Royalty | 15% | Provincial royalty (can vary 12-18%) |
| IHI | 8% | Retenciones a la exportación (export tax) |
| Income Tax | 34% | Ganancias (corporate income tax) |
| YPF Equity | 12% | Varies by block |
| Discount Rate | 10% | |
| OPEX | $8-14/bbl | Vaca Muerta ~$8-10 (improving) |

**Notes:**
- Vaca Muerta is Argentina's flagship shale play (world-class)
- Export taxes ("retenciones") fluctuate with government policy
- Provincial royalties vary by province: Neuquén, Mendoza, etc.
- FX controls affect investment returns
- Vaca Muerta typical well: 2000m lateral, qi 500-800 bopd, CAPEX $8-12MM

---

## Brazil (BRA)

**Regime:** Concession / Production Sharing / Transfer of Rights
**Year:** ANP framework

| Parameter | Default | Notes |
|-----------|---------|-------|
| Royalty | 10% | Fixed for most blocks |
| Special Participation | 5% | Additional levy on high-production fields |
| Income Tax | 34% | IRPJ 25% + CSLL 9% |
| Petrobras Equity | 30% | Varies; mandatory operator in pre-salt |
| Discount Rate | 12% | |
| OPEX | $10-20/bbl | Pre-salt deepwater: $15-20 |

**Notes:**
- Pre-salt blocks: Production Sharing regime (Petrobras mandatory operator)
- Concession blocks: R/T regime
- Transfer of Rights: special regime for Libra/Búzios area
- "Participação Especial" — progressive tax on net revenue
- Pre-salt wells: very high CAPEX ($80-150MM), but very high EUR (50-100 MMSTB)
- Key basins: Santos (pre-salt), Campos, Equatorial Margin

---

## Peru (PER)

**Regime:** License/Concession
**Year:** PeruPetro framework

| Parameter | Default | Notes |
|-----------|---------|-------|
| Royalty | 10% | "Regalía" — varies by contract |
| Income Tax | 29.5% | Impuesto a la Renta |
| IHI | 0% | No extraction tax |
| State Equity | 0% | Generally no state participation |
| Discount Rate | 10% | |
| OPEX | $10-15/bbl | Jungle operations: $15-25 |

**Notes:**
- Relatively investor-friendly regime
- Challenges: Amazon rainforest operations (logistics)
- Key basins: Marañón, Ucayali, Talara (onshore NW)
- Limited offshore development
- Social license and environmental requirements significant

---

## Ecuador (ECU)

**Regime:** Service Contract / Production Sharing
**Year:** Post-reform framework

| Parameter | Default | Notes |
|-----------|---------|-------|
| Royalty | 20% | Variable by contract type |
| Income Tax | 25% | Corporate rate |
| IHI | 0% | |
| State Equity | 0% | PetroEcuador operates state blocks directly |
| Discount Rate | 10% | |
| OPEX | $12-18/bbl | Oriente basin |

**Notes:**
- Government has shifted between regimes multiple times
- Service contracts: contractor paid a fee per barrel
- Key basin: Oriente (Amazon region)
- Heavy oil predominant (12-20° API)
- Transport costs significant (pipeline to coast)

---

## Bolivia (BOL)

**Regime:** Nationalized / Service Contract
**Year:** Post-2006 nationalization framework

| Parameter | Default | Notes |
|-----------|---------|-------|
| Royalty | 18% | IDH (Impuesto Directo a los Hidrocarburos) |
| Income Tax | 25% | IUE (Impuesto a las Utilidades) |
| IHI | 0% | |
| State Equity | 0% | YPFB operates directly |
| Discount Rate | 12% | Higher risk premium |
| OPEX | $8-12/bbl | Primarily gas production |

**Notes:**
- 2006 nationalization: YPFB took operational control
- International companies operate as service providers
- Primarily gas-producing country (exports to Brazil and Argentina)
- Key fields: San Alberto, Sábalo, Margarita
- Declining production; limited new investment

---

## Cross-Country Comparison Guidelines

When comparing fiscal regimes:

1. **Government Take** = Royalty + IHI + Income Tax + State Equity share of profits
2. **Effective Tax Rate** includes all fiscal layers, not just income tax
3. **Partner IRR** is the key metric for investment decisions (not project IRR)
4. **Carry risk** — Does the state company pay its CAPEX share? (gov_capex_contribution)
5. **Above-ground risk** — FX controls, political stability, regulatory changes
6. **Typical government take ranges:**
   - Low: 30-45% (USA, Peru)
   - Medium: 50-65% (Colombia, Argentina, Ecuador, Bolivia)
   - High: 70-85% (Venezuela EMV, Brazil pre-salt)
