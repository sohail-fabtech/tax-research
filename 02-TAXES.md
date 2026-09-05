# 02 — Annual Taxes

**Steps 6–7 of the year loop** · Rail: **nominal** (never deflate before this module)

---

## What this computes

Total tax paid in each year: federal income tax, payroll tax, state income tax, the 3.8% NIIT, and Medicare IRMAA surcharges.

---

## 1. The tax stack, in order

```
STEP 6a  Gross income          (module 01)
STEP 6b  − Above-the-line deductions  → ADJUSTED GROSS INCOME (AGI)
STEP 6c  − Standard or itemized deduction
STEP 6d  − QBI deduction (§199A)
                                → TAXABLE INCOME
STEP 7a  Apply ordinary brackets to ordinary income
STEP 7b  Apply capital-gains brackets to LTCG, stacked on top
STEP 7c  + Payroll tax (FICA or self-employment)
STEP 7d  + NIIT 3.8% if applicable
STEP 7e  + State income tax
STEP 7f  + Medicare IRMAA (age 65+)
                                → TOTAL TAX
```

**Critical:** the standard deduction is subtracted **after** AGI, not before. QBI is computed **on** taxable income before the QBI deduction itself. Getting this order wrong shifts every downstream bracket.

---

## 2. Assembling taxable income

```
AGI = w2Income
    + k1Income
    + scheduleCProfit
    + rentalIncome
    + portfolioIncome
    + taxableSocialSecurity      ← module 04, NOT the gross benefit
    + rmd                        ← module 05
    + taxablePortfolioWithdrawal
    − pretaxContributions        ← module 03 (401k, HSA, SEP)
    − deductibleSelfEmploymentTax (half of SE tax)
```

```
taxableIncome = MAX(0, AGI − deduction − qbiDeduction)
```

Where `deduction` is the greater of the standard deduction or itemized deductions, plus the senior bonus deduction if eligible.

---

## 3. Federal ordinary income tax — 2026 brackets

Source: **IRS Rev. Proc. 2025-32**. OBBBA made the TCJA rate structure permanent and gave the bottom two brackets an extra inflation bump.

### Married Filing Jointly

| Rate | Taxable income over | Up to |
|---|---|---|
| 10% | $0 | $24,800 |
| 12% | $24,800 | $100,800 |
| 22% | $100,800 | $211,400 |
| 24% | $211,400 | $403,550 |
| 32% | $403,550 | $512,450 |
| 35% | $512,450 | $768,700 |
| 37% | $768,700 | — |

### Single

| Rate | Taxable income over | Up to |
|---|---|---|
| 10% | $0 | $12,400 |
| 12% | $12,400 | $50,400 |
| 22% | $50,400 | $105,700 |
| 24% | $105,700 | $201,775 |
| 32% | $201,775 | $256,225 |
| 35% | $256,225 | $640,600 |
| 37% | $640,600 | — |

### Formula — marginal, not flat

```
tax = 0
previousCap = 0
FOR each bracket (cap, rate):
    slice = MIN(taxableIncome, cap) − previousCap
    IF slice <= 0: BREAK
    tax = tax + slice × rate
    previousCap = cap
```

> **Never** multiply total income by the top rate. That is the single most common error in projection engines. A $300,000 MFJ taxable income is not taxed at 24% — it is taxed at 10/12/22/24% in slices.

**Worked number** — MFJ, taxable income $300,000:

| Slice | Amount | Rate | Tax |
|---|---|---|---|
| 0 → 24,800 | $24,800 | 10% | $2,480 |
| 24,800 → 100,800 | $76,000 | 12% | $9,120 |
| 100,800 → 211,400 | $110,600 | 22% | $24,332 |
| 211,400 → 300,000 | $88,600 | 24% | $21,264 |
| **Total** | | | **$57,196** |

Effective rate 19.1%, marginal rate 24%. Both matter: the marginal rate drives planning decisions, the effective rate drives the cash-flow line.

---

## 4. Standard deduction — 2026

| Filing status | Amount |
|---|---|
| Single / MFS | $16,100 |
| Married filing jointly / surviving spouse | $32,200 |
| Head of household | $24,150 |

### Additional standard deduction for age 65+

Long-standing provision, separate from the OBBBA bonus below. Add per qualifying person:

| Status | Extra |
|---|---|
| Single / HoH | $2,050 |
| Married (each spouse 65+) | $1,650 each |

### OBBBA senior bonus deduction — TEMPORARY

A **new, separate** above-the-line deduction created by the One Big Beautiful Bill Act.

| Item | Value |
|---|---|
| Amount | $6,000 single / $12,000 MFJ (both spouses 65+) |
| Eligibility | Age 65+ by year end, valid SSN |
| Years | **2025 through 2028 only** |
| Phase-out starts | $75,000 single / $150,000 MFJ MAGI |
| Phase-out rate | 6 cents per $1 over the threshold |
| Fully gone at | $175,000 single / $250,000 MFJ |

```
reduction   = MAX(0, MAGI − threshold) × 0.06
seniorBonus = MAX(0, baseAmount − reduction)
```

> **This deduction expires after 2028.** A model projecting to age 90 must switch it off in 2029. Hard-coding it for all years overstates the after-tax result for decades.

---

## 5. Long-term capital gains — stacked, not separate

LTCG and qualified dividends are taxed at their own rates, but they **stack on top of ordinary income**. The ordinary income fills the lower brackets first.

### 2026 LTCG brackets

| Rate | Single (taxable income) | MFJ (taxable income) |
|---|---|---|
| 0% | up to $49,450 | up to $98,900 |
| 15% | $49,450 – $545,500 | $98,900 – $613,700 |
| 20% | above $545,500 | above $613,700 |

### Formula

```
ordinaryTaxable = taxableIncome − longTermGains
gainsStartAt    = ordinaryTaxable

FOR each LTCG bracket (cap, rate):
    slice = MIN(gainsStartAt + longTermGains, cap) − MAX(gainsStartAt, previousCap)
    IF slice > 0: tax = tax + slice × rate
```

> A client with $90,000 of ordinary income and $50,000 of gains does **not** get the full 0% bracket on the gains. The ordinary income consumes it first.

---

## 6. QBI deduction — §199A

Made **permanent** by OBBBA §70105.

| Item | 2026 value |
|---|---|
| Deduction | 20% of qualified business income |
| Threshold | $201,750 single / $403,500 MFJ |
| Phase-out ends | $276,750 single / $553,500 MFJ |
| New minimum deduction | $400 (requires at least $1,000 of QBI) |

```
tentativeQBI = qualifiedBusinessIncome × 0.20
qbiDeduction = MIN(tentativeQBI, taxableIncomeBeforeQBI × 0.20)
```

### Is the business an SSTB? This decides everything above the threshold

Above the threshold, a **specified service trade or business (SSTB)** phases out to zero. A non-SSTB instead becomes limited by W-2 wages paid and property basis — a limit most profitable businesses can satisfy.

| **SSTB — loses the deduction above the phase-out** | **NOT an SSTB — keeps it** |
|---|---|
| Health (physicians, dentists, nurses, vets, therapists) | **Engineering** — excluded **by statute** |
| Law | **Architecture** — excluded **by statute** |
| Accounting, actuarial science | Manufacturing, construction, wholesale, retail |
| Consulting | **Real estate** — rental, brokerage, development |
| Financial services, investing, investment management, trading | Insurance agents and brokers |
| Performing arts, athletics | Restaurants, hospitality, transport |
| Any business whose principal asset is the **reputation or skill** of its owners | Software, most technology businesses |

**Two points that are routinely got wrong:**

- **Engineers and architects are specifically excluded from SSTB status** by IRC §199A(d)(2), which adopts the §1202(e)(3)(A) list *minus* engineering and architecture. They keep the full 20% at any income level. Their work depends on reputation and skill just as much as a doctor's — the statute simply carves them out.
- The **"reputation or skill"** catch-all is drafted broadly but was interpreted **narrowly** in the final regulations. It reaches only income from endorsing products, licensing a name, image or likeness, and appearance fees — not ordinary businesses run by skilled people.

> **Why this matters for the projection.** Two clients with identical income can be $36,000 apart in deduction purely by field. Flag the client's business type as an explicit input; never infer it.

---

## 7. Payroll tax

### Employee (W-2)

| Component | Rate | Wage cap 2026 |
|---|---|---|
| Social Security (OASDI) | 6.20% | **$184,500** |
| Medicare | 1.45% | No cap |
| Additional Medicare | 0.90% | Above $200,000 single / $250,000 MFJ |

```
ssTax       = MIN(wages, 184500) × 0.062
medicareTax = wages × 0.0145
addlMedicare = MAX(0, wages − threshold) × 0.009
```

### Self-employed

Double the rate (employer + employee halves), applied to 92.35% of net earnings:

```
seBase       = scheduleCProfit × 0.9235
seSocialSec  = MIN(seBase, 184500) × 0.124
seMedicare   = seBase × 0.029
deductibleHalf = (seSocialSec + seMedicare) × 0.5    ← subtract from AGI
```

> The **Additional Medicare thresholds ($200,000 / $250,000) are not indexed** — same statutory freeze as NIIT. Do not inflate them.

---

## 8. Net Investment Income Tax — 3.8%

| Item | Value |
|---|---|
| Rate | 3.8% |
| Threshold | $200,000 single / $250,000 MFJ / $125,000 MFS |
| Indexed? | **No — frozen since 2013** |

```
niit = 0.038 × MIN(netInvestmentIncome, MAX(0, MAGI − threshold))
```

Net investment income = interest + dividends + capital gains + passive rental + annuity income.
**Excluded:** wages, self-employment income, Social Security, and **distributions from qualified retirement plans and IRAs**.

> **An RMD is not subject to NIIT.** But it *raises MAGI*, which can push other investment income over the threshold. That indirect effect is real and must be modelled.

---

## 9. Medicare IRMAA — age 65+

Source: **CMS 2026 Parts A & B fact sheet**. Uses MAGI from **two years prior**.

| MAGI single | MAGI MFJ | Part B/mo | Part D/mo |
|---|---|---|---|
| ≤ $109,000 | ≤ $218,000 | $202.90 | $0.00 |
| $109,001–$137,000 | $218,001–$274,000 | $284.10 | $14.50 |
| $137,001–$171,000 | $274,001–$342,000 | $405.80 | $37.50 |
| $171,001–$205,000 | $342,001–$410,000 | $527.50 | $60.40 |
| $205,001–$499,999 | $410,001–$749,999 | $649.20 | $83.30 |
| ≥ $500,000 | ≥ $750,000 | $689.90 | $91.00 |

Part B annual deductible 2026: **$283**.

```
irmaaAnnual = (partB(magi_from_2_years_ago) + partD(...)) × 12 × numberOfPeopleOnMedicare
```

> **IRMAA is a cliff, not a phase-in.** One dollar over a threshold costs the full tier. This makes the retirement-to-RMD window planning-critical, and the model must show it.

---

## 9b. When filing status changes — the widow's penalty

**The most consequential mid-projection event.** Nothing else in the tax code changes this many parameters at once.

### The transition

```
Year of death           → MARRIED FILING JOINTLY (full year, regardless of date of death)
Next 2 years            → QUALIFYING SURVIVING SPOUSE — but ONLY with a dependent child
No dependent child      → SINGLE, immediately from the following year
```

> **Most retirees have no dependent child**, so the realistic path is **MFJ → Single in one step**. Modelling a two-year QSS grace period for a 78-year-old widow is simply wrong.

### What changes at once

| Parameter | Married filing jointly | Single | Effect |
|---|---|---|---|
| Standard deduction | $32,200 | **$16,100** | halved |
| Age-65 addition | $3,300 (both) | **$2,050** | reduced |
| Every bracket width | full | **half** | same income, higher bracket |
| SS taxation thresholds | $32,000 / $44,000 | **$25,000 / $34,000** | more benefit taxed |
| **IRMAA tier 1** | $218,000 | **$109,000** | halved |
| NIIT threshold | $250,000 | **$200,000** | lower |

### Worked example — income falls, tax rises

A couple aged 78, both 65+, with $70,758 of Social Security ($42,758 + $28,000) and an $80,000 RMD.

| | Both alive (MFJ) | Survivor (Single) |
|---|---|---|
| Social Security | $70,758 | **$42,758** — smaller benefit lost |
| RMD | $80,000 | $80,000 — unchanged |
| **Gross income** | **$150,758** | **$122,758** |
| Taxable Social Security | $60,144 | $36,344 |
| AGI | $140,144 | $116,344 |
| Deduction | $35,500 | **$18,150** |
| Taxable income | $104,644 | $98,194 |
| **Federal tax** | **$12,446** | **$16,315** |
| Effective rate | 8.3% | **13.3%** |
| Medicare | standard, two people — $4,870 | **IRMAA tier 2** — $3,583 for one |
| **After-tax income** | **$133,443** | **$102,860** |

**Gross income fell 19%. Federal tax rose $3,869. After-tax income fell 23%.**

> The survivor is **poorer and taxed harder at the same time**. AGI of $116,344 clears the single IRMAA threshold of $109,000, so Medicare surcharges start as well. Three effects from one event.

### What this implies for planning

The widow's penalty is **predictable**, which makes it plannable. Roth conversions during the years when the couple is still MFJ are cheaper than the same conversions the survivor would face later at single rates. The pre-RMD window and the both-alive window overlap — and the model should surface that.

## 9c. The IRMAA appeal — Form SSA-44

IRMAA uses income from **two years ago**. When income drops because of a life event, the client does not have to wait two years for Medicare to notice.

```
File Form SSA-44 to use CURRENT income instead of the 2-year-old return
```

**Eight qualifying life-changing events — the list is closed:**

| | Event |
|---|---|
| 1 | Marriage |
| 2 | Divorce or annulment |
| 3 | **Death of a spouse** |
| 4 | Work stoppage (retirement) |
| 5 | Work reduction |
| 6 | Loss of income-producing property |
| 7 | Loss of pension income |
| 8 | Employer settlement payment |

> **A one-time income spike is not on the list.** Selling a business or converting a large Roth raises IRMAA two years later and **cannot be appealed** — the appeal exists for income that *fell*, not income that spiked once. The only defence is planning the timing before the event.

> **Retirement itself is event 4.** A client retiring at 65 is billed on their working income from 63. Filing SSA-44 in the first Medicare year is routine and frequently missed.

## 9d. Medical and long-term care costs

```
deductibleMedical = MAX(0, totalMedicalExpenses − 0.075 × AGI)
```

Only the amount above **7.5% of AGI** is deductible, and only if itemising.

**Qualified long-term care insurance premiums count as medical expenses, capped by age (2026):**

| Age at year end | Deductible premium cap |
|---|---|
| 40 or under | $500 |
| 41–50 | $930 |
| 51–60 | $1,860 |
| 61–70 | $4,960 |
| **71 and over** | **$6,200** |

> **Actual long-term care costs are fully deductible medical expenses** — not subject to the premium caps above, which apply only to *insurance premiums*. A year in a nursing home can produce a very large deduction, which in turn creates a rare opportunity: a Roth conversion in the same year can be nearly tax-free.

> **The self-employed exception:** under §162(l) a self-employed client deducts 100% of qualified LTC premiums above the line — no 7.5% floor, no itemising.

## 10. State income tax

Three shapes. Pick per state.

| Shape | States | Formula |
|---|---|---|
| No income tax | TX, FL, NV, WA, WY, SD, AK, TN, NH | `stateTax = 0` |
| Flat rate | CO, IL, IN, MI, NC, PA, UT | `stateTax = stateTaxableIncome × flatRate` |
| Graduated | CA, NY, NJ, OR, MN, HI | Same bracket loop as federal, with state brackets |

California (the worksheet in this folder uses 8.84% corporate) has graduated individual rates topping out at **13.3%** including the 1% mental-health surcharge above $1M.

**Important state divergences to model:**
- Most states use federal AGI as the starting point but apply their **own** standard deduction.
- **Social Security is exempt from state tax in the large majority of states**, including California.
- Some states exempt part or all of retirement plan distributions.

---

## Ordering traps

| Don't | Do |
|---|---|
| Multiply income by the marginal rate | Walk the brackets slice by slice |
| Tax the **gross** Social Security benefit | Tax only the portion from module 04 |
| Index the NIIT / Additional Medicare thresholds | Leave them frozen at $200k/$250k |
| Apply the senior bonus deduction after 2028 | Switch it off in 2029 |
| Treat LTCG as a separate parallel calculation | Stack gains on top of ordinary income |
| Subject the RMD to NIIT | Exclude it from NII, but include it in MAGI |
| Use current-year MAGI for IRMAA | Use MAGI from two years earlier |
| Keep filing status MFJ after a spouse dies | MFJ in the year of death, then Single unless a dependent child qualifies them for QSS |
| Grant a 2-year QSS grace period to everyone | QSS requires a **dependent child** — most retirees go straight to Single |
| Assume a one-time income spike can be appealed | The SSA-44 list is closed; spikes are not on it |
| Apply the LTC premium caps to actual care costs | The caps apply to **premiums** only; care costs are fully deductible medical |

---

## Sources

| What | Source | Google this |
|---|---|---|
| 2026 brackets, deduction, QBI thresholds | [IRS Rev. Proc. 2025-32](https://www.irs.gov/newsroom/irs-releases-tax-inflation-adjustments-for-tax-year-2026-including-amendments-from-the-one-big-beautiful-bill) | `IRS 2026 inflation adjustments One Big Beautiful Bill` |
| NIIT thresholds not indexed | [CRS IF11820](https://www.congress.gov/crs-product/IF11820) · [IRS Topic 559](https://www.irs.gov/taxtopics/tc559) | `CRS 3.8% Net Investment Income Tax IF11820` |
| 2026 Medicare premiums and IRMAA | [CMS fact sheet](https://www.cms.gov/newsroom/fact-sheets/2026-medicare-parts-b-premiums-deductibles) | `CMS 2026 Medicare Parts A B premiums deductibles` |
| SS wage base $184,500 | [Federal Register 2025-19763](https://www.federalregister.gov/documents/2025/11/03/2025-19763/cost-of-living-increase-and-other-determinations-for-2026) | `OASDI contribution and benefit base 2026 Federal Register` |
| §199A permanence, $400 minimum | OBBBA §70105 (P.L. 119-21) | `OBBBA section 70105 QBI deduction permanent minimum` |
| Qualifying surviving spouse status | IRC §2(a) · [IRS Pub 501](https://www.irs.gov/publications/p501) | `IRS Publication 501 qualifying surviving spouse` |
| IRMAA appeal, 8 life-changing events | [20 CFR §418.1205](https://www.ecfr.gov/current/title-20/section-418.1205) · Form SSA-44 | `SSA-44 life changing event IRMAA appeal` |
| Medical expense 7.5% floor | IRC §213 | `IRS medical expense deduction 7.5 percent AGI` |
| 2026 LTC premium caps | Rev. Proc. 2025-32 · IRC §213(d)(10) | `2026 long term care insurance premium deduction limits` |
