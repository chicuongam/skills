# Risk KPI Library — standard decomposition trees

Use the canonical identity for a known metric instead of inventing one. Each entry gives the **root formula** and the **standard driver breakdown**. Tag leaves as Lever (L), Partial (P), or External/Macro (E).

## Table of contents
1. Credit risk
2. Market risk
3. Operational risk
4. Liquidity & funding risk
5. Insurance / actuarial
6. Fraud risk
7. Model risk
8. Conduct / compliance
9. Common commercial KPIs (for non-risk roots)

---

## 1. Credit risk

### Expected Loss (the foundational credit identity)
`Expected Loss (EL, $) = PD × LGD × EAD`

- **PD** — Probability of Default (%) (E/P)
  - Obligor/rating quality at origination (L) · Rating migration / transition (P) · Macro: unemployment, GDP, rates (E) · Vintage & seasoning (P) · Sector concentration (P)
- **LGD** — Loss Given Default (%) (P)
  - 1 − Recovery rate · Collateral coverage / LTV (L) · Collateral value volatility (E) · Seniority / lien position (L) · Time-to-recovery & legal cost (P)
- **EAD** — Exposure at Default ($) (P)
  - Drawn balance (P) · Undrawn commitment × CCF (Credit Conversion Factor) (P) · Limit-setting policy (L)

**Portfolio EL** = `Σ over segments (PD × LGD × EAD)` — split additively by product, geography, rating band, vintage; this exposes **mix** effects.

### Cost of Risk / Provisions
`Cost of Risk (bps) = Net Impairment Charge / Average Gross Loans`
- Stage migration (IFRS 9 Stage 1→2→3) · New defaults (flow) · Model/macro overlay changes · Write-backs & recoveries (offset, −)

### NPL Ratio & coverage
`NPL Ratio = Non-Performing Loans / Gross Loans` → driven by **default inflow − cure − write-off** roll rates.
`Coverage Ratio = Provisions / NPL`.

### Default / delinquency dynamics
`Default Rate = Defaults in period / Accounts at start`
Decompose via **roll rates** through DPD buckets: Current → 1–29 → 30–59 → 60–89 → 90+ (default). Each arrow is a transition probability; the tree's leaves are bucket-to-bucket roll rates (each a lever for collections/forbearance).

---

## 2. Market risk

### Value at Risk
`VaR` decomposes two ways (use both as parallel trees):
- **By risk factor** (additive in variance, or component VaR): Interest rate · FX · Equity · Credit spread · Commodity · Basis. Component VaR sums to total VaR (accounts for diversification).
- **By desk / book / portfolio**: incremental & component VaR per desk.

### P&L sensitivity (Greeks)
`ΔP&L ≈ Σ (sensitivity × factor move)`
- Delta × spot move · Vega × vol move · Gamma × spot²·½ · Theta (time) · Rho × rate move · cross-gammas.
This is the driver tree for "why did the book make/lose money".

Related: **Stressed VaR**, **Expected Shortfall (ES/CVaR)** = average loss beyond VaR; same factor/desk splits.

---

## 3. Operational risk

### Operational loss
`Op Loss ($) = Frequency × Severity` (per event type)
- **Frequency** = Transaction/activity volume × control-failure rate (control-failure rate is the **lever**; volume is P/E)
- **Severity** = Exposure per event × (1 − detection/mitigation rate) − Recovery/insurance (offset)

Partition additively by **Basel II event type**: Internal fraud · External fraud · Employment practices & workplace safety · Clients, products & business practices · Damage to physical assets · Business disruption & system failures · Execution, delivery & process management.

KRIs feeding frequency: failed-trade rate, system downtime, manual-touch rate, staff turnover, overdue reconciliations, audit findings open.

---

## 4. Liquidity & funding risk

### Liquidity Coverage Ratio
`LCR = High-Quality Liquid Assets (HQLA) / Net Cash Outflows over 30 days` (≥ 100%)
- **HQLA**: Level 1 (cash, sovereigns) + Level 2A + Level 2B (haircut)
- **Net outflows** = Stressed outflows − min(inflows, 75% of outflows); outflows = Σ (funding category × run-off rate). Run-off rates by retail stable/less-stable, operational/non-operational wholesale, secured funding.

### Net Stable Funding Ratio
`NSFR = Available Stable Funding / Required Stable Funding` (≥ 100%)
- ASF = Σ (liability × ASF factor); RSF = Σ (asset × RSF factor).

Other: **Survival horizon**, **Funding concentration** (top-10 counterparties / total), **Loan-to-Deposit ratio**, **Encumbrance ratio**.

---

## 5. Insurance / actuarial

### Combined Ratio (underwriting profitability)
`Combined Ratio = Loss Ratio + Expense Ratio` (< 100% = underwriting profit)
- **Loss Ratio** = Incurred Claims / Earned Premium
  - Incurred Claims = `Claim Frequency × Claim Severity` (+ IBNR reserve movement)
  - Frequency drivers: exposure count, peril rate, underwriting quality (L) · Severity drivers: claim inflation (E), large-loss/cat events (E), reserving adequacy (P)
- **Expense Ratio** = (Acquisition + Admin expenses) / Earned (or Written) Premium

Related: **Loss Ratio = Pure Premium / Average Premium**; **Reserve adequacy**; **Renewal/retention rate × rate change** as premium-growth tree.

---

## 6. Fraud risk

`Fraud Loss Rate (bps) = Net Fraud Losses / Total Transaction Value`
- `Gross Fraud $ = Txn volume × fraud attempt rate × avg fraud value × (1 − detection rate)`
  - Attempt rate (E, threat environment) · Detection/decline rate (L, rules & models) · Avg fraud value (P) · Recoveries/chargeback wins (offset, −)
Split by channel (card-present / CNP / ATO / application fraud), product, geography. Tension node: **false-positive rate** (over-blocking) trades off against detection — surface it.

---

## 7. Model risk

`Model performance decay` tree:
- **Discrimination**: Gini / AUC / KS over time (drift)
- **Calibration**: predicted vs actual (PD calibration)
- **Stability**: Population Stability Index (PSI) on score; Characteristic Stability Index on inputs
- **Data quality**: missing-rate, override rate (L)
Roots into model-risk KRIs: % models overdue for validation, # high-severity findings, override frequency.

---

## 8. Conduct / compliance

KRI hierarchy (mostly additive roll-up, not a math identity):
- Complaints per 1,000 customers · Upheld complaint rate · Mis-selling indicators · AML alerts → SAR conversion · KYC overdue rate · Breach count by severity · Training completion (L).
Treat as a **scorecard tree**: weight and roll up sub-indicators into a composite conduct score; document the weighting.

---

## 9. Common commercial KPIs (non-risk roots)

For when the root is a business metric:

- **Revenue** = Customers × ARPU; or Volume × Price; or Traffic × Conversion × AOV.
- **Customers** = Beginning + New − Churned; New = Leads × Conversion rate.
- **Gross Margin** = Revenue − COGS; Margin % = 1 − COGS/Revenue.
- **CLV** = (ARPU × Gross Margin %) / Churn rate.
- **Churn** decomposed by cohort, plan, tenure (mix vs rate).
- **EBITDA**, **ROE = Net Margin × Asset Turnover × Leverage** (DuPont) — DuPont is the classic financial KPI tree.

---

## How to apply an entry

1. Drop the root formula in as level 1.
2. Pull each driver's sub-breakdown as level 2–3, keeping only the branches relevant to the user's question (prune aggressively — a tree answering "why did cost of risk rise" doesn't need the full EAD branch unless EAD moved).
3. Tag L/P/E, attach the user's actual data if provided, then reconcile.
