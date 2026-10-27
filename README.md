
# PS1 Quantitative Financial Model - README, Sources & Assumptions

**Task:** CFA Club, IIT Indore - Induction Task 2026 (PS1: Consulting & Product Management)  
**Case Title:** *Navigating an ATF Price Shock: Strategy for a Regional Airline*  
**Workbook File:** `PS1_Regional_Airline_Route_PnL_Model.xlsx`  
**Companion Deliverables:** `PS1_Regional_Airline_ATF_Strategy_Deck.pptx` (10-Slide Strategy Deck) & `PS1_Regional_Airline_Written_Brief.pdf` (Written Brief, <1,000 Words)

## 1. Model Structure & Tab Guide

We built `PS1_Regional_Airline_Route_PnL_Model.xlsx` as a four-tab Excel model with zero hardcoded outputs. Every route P&L line, breakeven load factor (BLF), and sensitivity cell runs off live formulas linked to public aviation filings.

We model a representative 12-aircraft regional carrier (**DeccanWings Regional**) flying 180-seat Airbus A320ceo jets across eight short-haul routes (320 km to 640 km stage lengths) out of Tier-2 and Tier-3 Indian cities.

1. **`1_Exec_Summary_KPIs` (Inputs & Network Scorecard):** Contains all macro, fuel, fleet, and UDAN regulatory inputs in blue-shaded cells (rows 6-15) and aggregates network ASK, load factor, RASK, CASK, BLF, and annual EBITDAR across all six scenarios (rows 20-25).
2. **`2_Route_PnL_and_BLF` (Step 1 Diagnostic Engine):** Computes unit economics for routes `R1` through `R8` before and after the FY25 fuel spike (`Rs. 86,000/kl` baseline vs. `Rs. 1,04,927/kl` shock, `+22.0%`). Columns X and Y split every rupee of route losses into **Structurally Embedded Losses** (losses that existed even at baseline `Rs. 86,000/kl` fuel because of oversized 180-seat jets or sub-390 km Vande Bharat rail competition) and **Fuel-Driven Losses** (incremental P&L erosion caused strictly by the FY25 fuel spike).
3. **`3_Strategic_Options_ABC` (Step 2 & Step 3 Options Simulation):** Tests four operational configurations at the route level:
   - **Option A (Rows 4-14):** Drop `R7` (Nashik-Mumbai, 320 km) and `R8` (Kanpur-Delhi, 390 km) immediately; apply `+7.5% to +8.0%` peak corporate fare increases on `R1-R3` against a short-haul business price elasticity of `-0.42 to -0.45`; cut `R4-R6` frequency from `2x` to `1x` daily.
   - **Option B (Rows 16-26):** Bid `R4-R8` into the RCS-UDAN scheme (`Rs. 4,450/seat` Viability Gap Funding and `1%` state VAT on ATF) while keeping 180-seat A320 jets.
   - **Option C (Rows 28-38):** Swap four leased A320ceos on Tier-3 routes for 78-seat ATR 72-600 turboprops and shift maintenance to Power-by-the-Hour (PBH) contracts, without exiting `R7-R8`.
   - **Recommended Sequenced Path (Rows 40-50):** Exit `R7-R8` in Month 1 and redeploy those A320 slots to add a 5th daily frequency on `R1-R3` with dynamic yield tiers (Months 1-3); bid `R4-R6` into UDAN while swapping their gauge to 78-seat ATR 72-600 turboprops so the 40-seat UDAN subsidy quota covers `51.3%` of the cabin (Months 4-24).
4. **`4_Risk_Sensitivity_Matrix` (Step 4 Stress Testing):** Runs a 25-cell two-way sensitivity grid varying ATF prices (`Rs. 85,000/kl` to `Rs. 1,25,000/kl`) against yield shifts (`-6.0%` to `+6.0%`), followed by three stress scenarios (Brent `$105/bbl` + `INR 89/USD`, 180-day state VGF payment delays, and a 6-month delay in ATR 72-600 lease deliveries).

## 2. Equations & Accounting Identities

- **Available Seat Kilometres ($\text{ASK}$, in Millions):**
  $$\text{ASK} = \frac{\text{Daily Flights} \times 365 \times \text{Seats per Flight} \times \text{Stage Length (km)}}{10^6}$$
- **Revenue Passenger Kilometres ($\text{RPK}$, in Millions):**
  $$\text{RPK} = \text{ASK} \times \text{Load Factor (LF)}$$
- **Total Revenue per ASK ($\text{RASK}$, in Rs./ASK):**
  $$\text{RASK} = \frac{(\text{RPK} \times \text{Passenger Yield}) + (\text{Annual Passengers} \times \text{Ancillary per Pax} / 10^6)}{\text{ASK}}$$
- **Total Cost per ASK ($\text{CASK}$, in Rs./ASK):**
  $$\text{Total CASK} = \text{Fuel CASK} + \text{Ex-Fuel CASK}, \quad \text{where } \text{Fuel CASK}_{\text{Shock}} = \text{Fuel CASK}_{\text{Base}} \times \left(\frac{\text{ATF}_{\text{Shock}}}{\text{ATF}_{\text{Base}}}\right)$$
- **Breakeven Load Factor ($\text{BLF}$, in %):**
  $$\text{BLF} = \frac{\text{Total CASK}}{\text{Effective Total Yield}} = \frac{\text{Total CASK}}{\text{RASK} / \text{Actual LF}}$$
  When $\text{BLF} > 100\%$ (`R7: ISK-BOM` at `116.2%` and `R8: KNU-DEL` at `116.4%`), the flight loses money even if every seat is sold.
- **Loss Attribution Split:**
  $$\text{Structurally Embedded Loss} = \min\left(0, \; \text{EBITDAR}_{\text{Pre-Shock}}\right)$$
  $$\text{Fuel-Driven Loss} = \text{EBITDAR}_{\text{Post-Shock}} - \text{EBITDAR}_{\text{Pre-Shock}}$$

## 3. Public Data Benchmarks & Citations (Section 1.6 References)

| Parameter / Benchmark | Modeled Input | Public Data Source & Verification Link |
| :--- | :--- | :--- |
| **Domestic Metro ATF Price** | `Rs. 1,04,927 / kl` (`+22.0%` vs. `Rs. 86,000/kl` base) | [IOCL Aviation Fuel Price Archive](https://iocl.com/aviation-fuel) and [IOCL Petroleum Product Prices](https://iocl.com/prices-of-petroleum-products) |
| **Leader Unit Economics (IndiGo)** | RASK `Rs. 5.40` \| CASK `Rs. 4.62-4.83` \| LF `86.7%` | [IndiGo Q1 FY25 Financial Results](https://www.goindigo.in/press-releases/indigo-releases-q1-financial-results-of-fy-2025.html) and [IndiGo FY25 Annual Report](https://nsearchives.nseindia.com/annual_reports/AR_27116_INDIGO_2024_2025_A_26072025103933.pdf) (45 ATR 72-600 regional fleet) |
| **Distressed Narrow-Body CASK** | Total CASK `Rs. 6.50` \| Fuel `Rs. 1.88` \| Ex-Fuel `Rs. 4.62` | [SpiceJet Q3 FY25 Unit Cost Analysis](https://indianexpress.com/article/smart-stocks/less-than-4-market-share-40-fleet-grounded-spicejet-avoid-crash-9902137/) |
| **Regional Sub-80-Seat Benchmark** | 50-76 seat gauge on Tier-3 UDAN spokes (Belagavi, Surat, Indore) | [Star Air Fleet & Network Profile](https://en.wikipedia.org/wiki/Star_Air_(India)) and [Star Air Official Fleet Specs](https://www.starair.in/Home/ourfleet) |
| **UDAN VGF, VAT & Fare Caps** | `Rs. 4,450/seat` VGF \| `1%` ATF VAT \| `40-seat` cap | [MoCA Modified UDAN Scheme v1.2](https://www.google.com/search?q=https://www.civilaviation.gov.in/sites/default/files/2025-09/modified-udan-scheme-v1.2-workshop-1.pdf), [PIB UDAN 10-Year Release](https://www.pib.gov.in/PressReleaseDetail.aspx?PRID=2325359&reg=19&lang=1), and [UDAN Fare Cap Schedule](https://anantamias.com/udaan/) |
| **Domestic Traffic & Load Factors** | Tier-2/3 load factors (`56%-84%`) | [DGCA Monthly Traffic Statistics Portal](https://dgca.gov.in/digigov-portal/) |
| **Conceptual & Pricing References** | Retail unbundling (`Rs. 460/pax`) & OB seat-bucket yield management | [McKinsey Future of Aviation / Retail Reinvention](https://travelweekly.co.uk/in-depth/why-the-future-of-airlines-depends-on-retail-reinvention) and [HBS / HBR American Airlines Revenue Management Case](https://www.hbs.edu/faculty/Pages/item.aspx?num=3408) |

## 4. Key Model Outputs to Know for Your Panel Interview

- **Status Quo Burn:** A `+22.0%` fuel price jump pushes network EBITDAR from `-Rs. 29.9 Cr` (`-6.9%` margin) to `-Rs. 78.3 Cr` (`-18.1%` margin) across `1,001.6M` annual ASKs.
- **Root Cause Split:** Across the network, `-Rs. 48.4 Cr` of the drop comes from higher fuel bills (`-Rs. 28.8 Cr` on `R1-R3`, `-Rs. 11.0 Cr` on `R4-R6`, `-Rs. 8.6 Cr` on `R7-R8`). However, on the five money-losing routes (`R4-R8`), **`Rs. 72.9 Cr` of gross losses were already baked into the network before fuel prices moved** (`-Rs. 19.9 Cr` on `R4-R6` from flying 180-seat jets on 110-passenger Tier-3 routes, and `-Rs. 53.0 Cr` on `R7-R8` from competing against `<4-hour` Vande Bharat trains on `<390 km` sectors).
- **Why Standalone Option B Fails (`-Rs. 19.8 Cr`):** UDAN subsidizes 50% of seats *capped at 40 seats per flight*. On a 180-seat A320, only `22.2%` of seats get VGF while 140 unsubsidized seats cannot fill at profitable fares. On a 78-seat ATR 72-600, those 40 seats cover `51.3%` of the plane, flipping `R4-R6` to `+Rs. 23.4 Cr` EBITDAR.
