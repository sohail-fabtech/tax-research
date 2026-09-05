# 10 — Sources, Test Vectors, and Competitor Benchmark

---

## PART A — EVERY CONSTANT, AND WHERE IT CAME FROM

All figures are **tax year 2026**, verified against the primary US government source.
The "Google this" column is the literal phrase that surfaces the source, so nothing here has to be taken on trust.

### Income tax

| Constant | Value | Source | Google this |
|---|---|---|---|
| Standard deduction MFJ | $32,200 | IRS Rev. Proc. 2025-32 | `IRS 2026 inflation adjustments One Big Beautiful Bill` |
| Standard deduction single | $16,100 | same | same |
| Standard deduction HoH | $24,150 | same | same |
| Brackets (7 rates) | see module 02 | same | same |
| LTCG 0%/15% breakpoints MFJ | $98,900 / $613,700 | same | `2026 capital gains tax brackets Rev Proc 2025-32` |
| Senior bonus deduction | $6,000 / $12,000, 2025–2028 | OBBBA (P.L. 119-21) | `OBBBA senior bonus deduction 65 phase out 75000 150000` |
| QBI threshold | $201,750 / $403,500 | Rev. Proc. 2025-32 | `2026 section 199A QBI threshold Rev Proc 2025-32` |
| QBI phase-out ends | $276,750 / $553,500 | Rev. Proc. 2025-32 | same |
| QBI minimum deduction | $400 | OBBBA §70105 | `OBBBA section 70105 QBI minimum deduction $400` |
| **SSTB definition** | health, law, accounting, actuarial, performing arts, consulting, athletics, financial services, investing, trading, plus "reputation or skill" | IRC §199A(d)(2) → §1202(e)(3)(A) | `199A SSTB definition specified service trade or business` |
| **Engineering and architecture excluded** | keep the full 20% at any income | IRC §199A(d)(2) — adopts the §1202 list **minus** those two fields | `199A engineers architects excluded SSTB` |
| "Reputation or skill" scope | narrow — endorsements, name/image/likeness licensing, appearance fees only | Reg. §1.199A-5(b)(2)(xiv) | `199A reputation or skill final regulations narrow` |
| NIIT threshold | $200,000 / $250,000 — **not indexed** | IRC §1411 | `CRS 3.8% Net Investment Income Tax IF11820` |

**Primary link:** <https://www.irs.gov/newsroom/irs-releases-tax-inflation-adjustments-for-tax-year-2026-including-amendments-from-the-one-big-beautiful-bill>

### Retirement

| Constant | Value | Source | Google this |
|---|---|---|---|
| 401(k) deferral | $24,500 | IRS Notice 2025-67 | `IRS 401k limit increases to 24500 for 2026` |
| Catch-up 50+ | $8,000 | same | same |
| Super catch-up 60–63 | $11,250 (**replaces** the $8,000) | same | same |
| IRA / IRA catch-up | $7,500 / $1,100 | same | same |
| Roth IRA phase-out MFJ | $242,000–$252,000 | same | same |
| Mandatory Roth catch-up wage trigger | $150,000 | SECURE 2.0 §603 | `SECURE 2.0 Roth catch-up 2026 150000 wages` |
| QCD limit | $111,000 | Notice 2025-67 | `2026 qualified charitable distribution limit 111000` |

**Primary link:** <https://www.irs.gov/newsroom/401k-limit-increases-to-24500-for-2026-ira-limit-increases-to-7500>

### Social Security

| Constant | Value | Source | Google this |
|---|---|---|---|
| COLA | 2.8% | Federal Register 2025-19763 | `Cost-of-Living Increase and Other Determinations for 2026` |
| Wage base | $184,500 | same | same |
| AWI 2024 | $69,846.57 | same | same |
| PIA bend points | **$1,286 / $7,749** | same | same |
| Family max bend points | $1,643 / $2,371 / $3,093 | same | same |
| Earnings test exempt (monthly) | $2,040 / $5,430 | same | same |
| FRA | 67 (born 1960+) | SSA | `SSA full retirement age chart` |
| Early reduction | 5/9 of 1%, then 5/12 of 1% | 20 CFR 404.313 | `SSA early or late retirement reduction factors` |
| Delayed credit | 2/3 of 1% per month to 70 | SSA | `SSA delayed retirement credits` |
| Benefit tax thresholds | $25k/$34k, $32k/$44k — **never indexed** | IRC §86 | `IRS Publication 915 Social Security benefits taxable` |

**Primary link:** <https://www.federalregister.gov/documents/2025/11/03/2025-19763/cost-of-living-increase-and-other-determinations-for-2026>

> **Note:** `ssa.gov` blocks automated access. The Federal Register notice is the **legally authoritative** publication of these same figures and is freely accessible. Use it as the citation of record.

### RMDs

| Constant | Value | Source | Google this |
|---|---|---|---|
| RMD age | 73 (born 1951–59) / 75 (born 1960+) | SECURE 2.0 §107 | `IRS required minimum distribution FAQs SECURE 2.0` |
| Uniform Lifetime Table | full table in module 05 | **IRS Pub 590-B, Appendix B, Table III** | `IRS Publication 590-B Appendix B Table III Uniform Lifetime` |
| Penalty | 25%, or 10% if corrected in 2 yrs | SECURE 2.0 §302 | `IRS RMD excise tax 25 percent SECURE 2.0` |

**Primary link:** <https://www.irs.gov/pub/irs-pdf/p590b.pdf>

### Real estate (module 07)

| Constant | Value | Source | Google this |
|---|---|---|---|
| ≤7-day average stay → not a rental activity | classification test | Reg. §1.469-1T(e)(3)(ii)(A) | `1.469-1T(e)(3)(ii)(A) seven day average rental activity` |
| Material participation | **7 tests**, any one suffices | Reg. §1.469-5T(a) | `1.469-5T material participation seven tests` |
| REPS | >750 hrs **and** >50% of personal services | IRC §469(c)(7) | `real estate professional 750 hours 469(c)(7)` |
| Aggregation election | all rentals as one activity | Reg. §1.469-9(g) | `1.469-9(g) election group rental real estate` |
| Grouping disclosure | appropriate economic unit | Reg. §1.469-4 · Rev. Proc. 2010-13 | `1.469-4 grouping appropriate economic unit` |
| Self-rental | income non-passive, **loss stays passive** | Reg. §1.469-2(f)(6) | `self-rental rule 1.469-2(f)(6)` |
| §280A personal use | > MAX(14 days, 10% of rental days) → loss capped | IRC §280A | `section 280A vacation home 14 days 10 percent` |
| Augusta rule | ≤14 days rented → income excluded | IRC §280A(g) | `Augusta rule 280A(g)` |
| Recovery periods | 27.5 / 39 / 15 / 5–7 years | IRS Pub 946 · Pub 527 | `IRS Publication 946 MACRS recovery periods` |
| **Bonus depreciation** | **100%, permanent**, placed in service after **19 Jan 2025** | OBBBA · IRC §168(k) | `OBBBA 100% bonus depreciation permanent` |
| §179 limit / phaseout | **$2,560,000 / $4,090,000** | Rev. Proc. 2025-32 | `2026 section 179 limit 2,560,000` |
| §179 on residential rental | **Not available** | IRC §179(d)(1) · §168(e)(2)(A) | `section 179 residential rental not eligible` |
| §1250 recapture | **25%** | IRC §1250 | `unrecaptured section 1250 gain 25 percent` |
| §199A rental safe harbor | **250 hours**, 3 of 5 years; triple-net excluded | Rev. Proc. 2019-38 | `Revenue Procedure 2019-38 rental safe harbor` |
| §1031 | real property only; **45 / 180** days | IRC §1031 | `1031 exchange 45 day 180 day real property only` |
| STR self-employment tax | Schedule C only if **substantial services** | IRC §1402 | `short term rental substantial services Schedule C SE tax` |

**Full mechanics:** [07-REAL-ESTATE-EQUITY.md](07-REAL-ESTATE-EQUITY.md)

### Loss limitations and AMT (module 11)

| Constant | Value | Source | Google this |
|---|---|---|---|
| Excess business loss threshold | **$256,000 / $512,000** — **down** from 2025 | Rev. Proc. 2025-32 · IRC §461(l) | `Rev Proc 2025-32 excess business loss threshold 2026` |
| EBL rule now permanent | no 2028 sunset | OBBBA (P.L. 119-21) | `OBBBA excess business loss permanent` |
| NOL limit | 80% of taxable income, indefinite, no carryback | IRC §172 | `section 172 NOL 80 percent limitation` |
| Capital loss offset | $3,000 ($1,500 MFS) — **not indexed since 1978** | IRC §1211/§1212 | `capital loss carryover $3,000 limit` |
| §469(i) rental allowance | $25,000, phased out $100k–$150k — **not indexed** | IRC §469(i) | `section 469(i) $25,000 rental allowance phaseout` |
| QBI limit | 20% × (taxable income − net capital gain) | IRC §199A | `199A deduction taxable income net capital gain` |
| AMT exemption | $90,100 / $140,200 | Rev. Proc. 2025-32 | `2026 AMT exemption 90,100 140,200` |
| AMT phaseout start | $500,000 / $1,000,000 | Rev. Proc. 2025-32 | same |
| AMT phaseout rate | **50%** — doubled from 25% | OBBBA §70107 | `OBBBA section 70107 AMT phaseout rate` |
| AMT 26%/28% break | $244,500 ($122,250 MFS) | IRC §55(b) · Rev. Proc. 2025-32 | `2026 AMT 28 percent rate threshold 244,500` |
| Minimum tax credit | indefinite, deferral items only | IRC §53 | `IRC 53 minimum tax credit` |

**Full mechanics:** [11-LOSS-LIMITATIONS-AND-CARRYFORWARDS.md](11-LOSS-LIMITATIONS-AND-CARRYFORWARDS.md)

### Estate

| Constant | Value | Source | Google this |
|---|---|---|---|
| Basic exclusion | $15,000,000 | Rev. Proc. 2025-32 / OBBBA | `IRS 2026 estate tax basic exclusion 15 million` |
| Top rate | 40% | IRC §2001 | same |
| Annual gift exclusion | $19,000 | Rev. Proc. 2025-32 | `IRS 2026 annual gift tax exclusion` |
| Step-up in basis | §1014 | 26 U.S.C. §1014 | `IRC 1014 basis property acquired from decedent` |
| IRD — no step-up | §691 | 26 U.S.C. §691 | `IRC 691 income in respect of a decedent` |
| Insurance estate inclusion | §2042 | 26 U.S.C. §2042 | `IRC 2042 incidents of ownership life insurance` |

### Medicare

| Constant | Value | Source | Google this |
|---|---|---|---|
| Standard Part B | $202.90/mo | CMS 2026 fact sheet | `CMS 2026 Medicare Parts A B premiums deductibles` |
| Part B deductible | $283 | same | same |
| IRMAA start | $109,000 / $218,000 (2024 MAGI) | same | same |
| Part B max | $689.90/mo | same | same |

**Primary link:** <https://www.cms.gov/newsroom/fact-sheets/2026-medicare-parts-b-premiums-deductibles>

### Insurance

| Constant | Value | Source | Google this |
|---|---|---|---|
| Max illustrated rate | 145% of portfolio rate, incl. bonuses | NAIC AG 49-B (eff. 1 May 2023) | `NAIC Actuarial Guideline 49-B maximum illustrated rate` |
| §7702 qualification | CVAT or GPT | 26 U.S.C. §7702 | `IRC 7702 life insurance contract defined` |
| MEC 7-pay test | §7702A | 26 U.S.C. §7702A | `IRC 7702A modified endowment contract seven pay` |

---

## PART B — TEST VECTORS

Hand-checkable input→output pairs. If an implementation reproduces all of these, the core math is right.

### T1 — Federal ordinary tax

| Input | Expected |
|---|---|
| MFJ, taxable income $300,000 | **$57,196** |
| MFJ, taxable income $100,800 | **$11,600** |
| Single, taxable income $50,400 | **$5,800** |

Check: any online 2026 bracket calculator.

### T2 — Social Security PIA

| Input | Expected |
|---|---|
| AIME $10,000, eligible 2026 | **$3,563.20/mo** |
| AIME $5,000, eligible 2026 | **$2,345.80/mo** |
| AIME $1,000, eligible 2026 | **$900.00/mo** |

Check: SSA Quick Calculator, or the 90/32/15 formula by hand.

### T3 — Bend point derivation

| Input | Expected |
|---|---|
| $180 × 69,846.57 / 9,779.44 | **$1,286** (rounded) |
| $1,085 × 69,846.57 / 9,779.44 | **$7,749** (rounded) |

Check: Federal Register 2025-19763 states both the inputs and the published results.

### T4 — Taxable Social Security

| Input | Expected |
|---|---|
| MFJ, $40,000 benefit, $60,000 other income | **$34,000 taxable** (85% cap binds) |
| MFJ, $40,000 benefit, $10,000 other income | **$0 taxable** |
| MFJ, $40,000 benefit, $20,000 other income | **$4,000 taxable** |

Check: IRS Publication 915 worksheet.

### T5 — RMD

| Input | Expected |
|---|---|
| $1,000,000 balance, age 75 | **$40,650** |
| $1,000,000 balance, age 73 | **$37,736** |
| $1,000,000 balance, age 90 | **$81,967** |

Check: the $40,650 figure is the worked example printed in IRS Pub 590-B itself.

### T6 — Mortgage amortisation

| Input | Expected |
|---|---|
| $500,000, 6.5%, 30 yr — monthly payment | **$3,160.34** |
| Balance after 10 years | **$423,881** |
| Total interest over 30 years | **$637,722** |

Check: any amortisation calculator.

### T7 — Contribution limits by age

| Age | Expected 401(k) max |
|---|---|
| 45 | **$24,500** |
| 55 | **$32,500** |
| 62 | **$35,750** |
| 64 | **$32,500** ← drops back |

Check: IRS Notice 2025-67.

---

## PART C — COMPETITOR BENCHMARK

### Finding 1: Drake is not actually a competitor for this

Drake Tax is frequently cited as the benchmark for this kind of system. Examined against the requirement, **Drake Tax Planner cannot produce a Roadmap to Age 90 and is not designed to.**

| Drake Tax Planner | Capability |
|---|---|
| Projection horizon | **Current year + 1 year only** |
| State returns | **Not supported** |
| Year-to-year rollover | **Scenarios do not update year to year** |
| Depreciation carry-forward | **Does not carry current-year depreciation into the next scenario** |
| Multiple returns | Not handled |
| Social Security / RMD / estate modelling | None |

Drake is a **compliance and short-horizon scenario tool** — it compares "what if I do X this year vs next year" inside a tax return. A 48-year, multi-asset, tax-aware wealth projection is a different product category entirely.

> **Implication:** benchmarking against Drake sets the bar too low. The real comparison set is financial planning software, not tax preparation software.

### The real competitive landscape

| Product | Category | What it does | Where it stops |
|---|---|---|---|
| **Drake Tax Planner** | Tax prep | 2-year scenario comparison inside a return | No multi-decade projection, no state, no assets |
| **Holistiplan** | Tax analysis | Reads a tax return via OCR, finds planning opportunities, multi-year Roth conversion projections | Not a financial planning platform; no balance-sheet projection |
| **RightCapital** | Financial planning | Full cash-flow retirement projection, tax-aware withdrawal sequencing, Roth conversion analysis, Monte Carlo | Generalist — no tax-strategy deployment engine |
| **MoneyGuidePro** | Financial planning | Goal-based planning, links Roth timing to projected tax outcomes | Weaker on the accumulation/business-owner side |
| **eMoney Advisor** | Financial planning | Integrated tax-aware withdrawal scenarios, account aggregation | Heavy, expensive, advisor-operated |

### What the serious tools all do that this roadmap must also do

These are table stakes. Missing any one of them makes the output non-credible to an advisor:

1. **Year-by-year cash flow**, not a single compound-interest curve
2. **Tax-aware withdrawal sequencing** — taxable → pre-tax → Roth
3. **RMD modelling** with the actual Uniform Lifetime Table
4. **Social Security taxation** via provisional income, not a flat percentage
5. **Roth conversion window analysis** in the retirement-to-RMD gap
6. **Separate account registrations** — pre-tax / Roth / taxable tracked apart
7. **Monte Carlo or at least multi-scenario** ranges, not a single deterministic line

### Finding 2: the real estate software category — and the gap nobody fills

Benchmarking only against tax-prep and financial-planning software missed an entire category. Real estate investors already use dedicated tools:

| Product | What it does | Where it stops |
|---|---|---|
| **Stessa** | Free portfolio bookkeeping, auto depreciation from basis and placed-in-service date, Schedule E reports | Bookkeeping only — no projection, no passive-loss carryforward |
| **REI Hub** | Double-entry accounting per entity/LLC, combined portfolio reporting | Same — a ledger, not a forecast |
| **Landlord Studio** | Mobile expense capture, OTA payout parsing for Airbnb/VRBO | Same |
| **Baselane** | Banking plus bookkeeping, Schedule E | Same |

**The finding:** the two categories are disjoint and neither crosses over.

| | Multi-decade projection | Real estate tax depth |
|---|---|---|
| Drake, Holistiplan | ✗ (1–2 years) | ✗ |
| RightCapital, eMoney, MoneyGuidePro | ✓ | **✗ — property is one appreciating asset** |
| Stessa, REI Hub, Landlord Studio | **✗ — current year only** | ✓ |
| **This roadmap** | ✓ | ✓ |

Planning software models a property as a single line that appreciates. It does not classify the property, does not depreciate it, does not track suspended passive losses across years, and does not know that a 5-day average stay changes the answer by $203,409. Real estate software does all of that — for **this year only**, with no forward projection at all.

**That intersection is the differentiation**, and it is a stronger claim than the earlier Drake comparison suggested.

### Where this roadmap can legitimately differentiate

| Differentiator | Why the incumbents don't do it |
|---|---|
| **Tax-strategy deployment engine** — takes *approved* tax savings and deploys them into buckets | RightCapital/eMoney model existing assets; they don't originate savings from a tax plan |
| **Seven-bucket capital architecture** incl. insurance cash value and disability/LTC | Planning tools treat insurance as a line item, not a growth bucket |
| **Advisor-approved values, front end renders only** (the mockup's Developer Rule) | Most tools let the advisor tinker in the UI; a locked engine is an audit advantage |
| **Estate value net of IRD**, not just net worth | Most tools display net worth and stop |
| **Business-owner entity layer** (C-corp/S-corp, executive bonus — see the worksheet in this folder) | Consumer-oriented planners largely ignore entity-level tax |

### Honest gaps to close

| Gap | Priority | Note |
|---|---|---|
| No Monte Carlo — single deterministic path only | **High** | Every serious planning competitor has it. The largest remaining gap |
| **State conformity not modelled** | **High** | California decouples from federal §461(l), §172 and bonus depreciation. A CA real estate client's state result will not match the federal one |
| No state tax detail beyond a flat rate | High | Graduated states (CA, NY, NJ, OR, MN, HI) need real brackets |
| Insurance modelled without real policy mechanics (COI, caps, lapse) | High | Module 06 specifies what is needed |
| No Roth conversion optimiser | Medium | The pre-RMD window is identified but not optimised |
| No account aggregation / live data | Medium | — |
| Opportunity Zones, DSTs, §721 UPREITs, installment sales | Low | Deliberately out of scope for v1; listed in module 07's edge-case matrix |

### Closed since the first pass

| Was a gap | Now covered |
|---|---|
| Real estate modelled as a single appreciating asset | Module 07: classification, ≤7-day rule, §280A, material participation, REPS, cost segregation, §1031, §199A safe harbor |
| No loss limitation logic | Module 11: the four gates plus the two real estate pre-gates |
| Research framed for one profession | SSTB in/out list with the statutory engineer/architect exclusion; examples rotate across fields |

---

## PART D — MAINTENANCE

These figures change annually. Refresh in this order each year:

| When | What | Where |
|---|---|---|
| **Mid-October** | SSA COLA, wage base, bend points | Federal Register "Cost-of-Living Increase and Other Determinations" |
| **Late October** | IRS inflation adjustments (brackets, deduction, estate) | IRS Rev. Proc. |
| **Early November** | Retirement plan limits | IRS Notice |
| **Mid-November** | Medicare premiums and IRMAA | CMS fact sheet |
| **Late October** | §179 limits, EBL threshold, AMT exemption, QBI thresholds | Same IRS Rev. Proc. as the brackets |
| **Annually** | Uniform Lifetime Table | Rarely changes — last updated 2022 |
| **Never** | Frozen thresholds — NIIT, SS benefit taxation, Additional Medicare, $25,000 rental allowance, $3,000 capital loss | Not indexed by statute. Do **not** inflate them |

### Watch list

| Item | Risk |
|---|---|
| **Senior bonus deduction expires after 2028** | Must switch off in 2029 |
| Social Security trust fund depletion (~2033–2035) | Possible benefit reduction; consider a scenario toggle |
| Frozen thresholds (NIIT, SS taxation, Additional Medicare) | Will capture more clients every year — this is correct behaviour, not a bug |
| OBBBA provisions with sunset dates | Check each against P.L. 119-21 before extending |
| **§461(l) threshold moved DOWN in 2026** | $626,000 → $512,000 MFJ. OBBBA reset the indexing base. Verify direction each year, do not assume it rises |
| **AMT phaseout rate doubled to 50% in 2026** | Thresholds also reverted to $500k / $1M. Any model on 2025 AMT parameters understates AMT |
| Bonus depreciation permanence | 100% is permanent under OBBBA for property placed in service after 19 Jan 2025, but the placed-in-service date still governs older acquisitions |
| Cost segregation → recapture | Accelerated depreciation lowers basis and raises the 25% §1250 recapture on sale. Track `accumulatedDepreciation` for the life of the property |
