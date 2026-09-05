# Roadmap to Age 90™ — Calculation Research

Complete year-by-year calculation logic for the *To Age 90+ Tax & Financial Roadmap*.

**Tax year basis:** 2026 · **Market:** United States · **Verified:** September 2026

Every constant in these documents was taken from the primary US government source and is cited with the exact phrase to re-find it. Nothing needs to be taken on trust.

**Who this covers.** Any US client, not one profession: W-2 employees, service-business owners (health, law, accounting, consulting — SSTBs), product- and project-business owners (engineering, architecture, manufacturing, construction, technology — **not** SSTBs), real estate investors, and any mix of these. Business type is an explicit input, never inferred.

---

## Start here

**→ [HANDBOOK.md](HANDBOOK.md) — to explain or present the system.**

All 21 steps in calculation order, each with a plain-English description, the real formula, **two contrasting examples**, and a risk table. Includes the calculation-order diagram, the top 10 mistakes ranked by money at stake, a risk register and a client glossary. Readable by a client and a developer at the same time.

**→ [MASTER-GUIDE.md](MASTER-GUIDE.md) — to build the system.**

The same flow as a lean developer reference: every formula in execution order, with a table showing which formula came from which source.

---

## The detailed modules

| # | Document | What it covers |
|---|---|---|
| **00** | [Overview and the Year Loop](00-OVERVIEW-AND-YEAR-LOOP.md) | The master loop, the order of operations, the nominal-vs-real rule |
| 01 | [Income and Expenses](01-INCOME-AND-EXPENSES.md) | Income growth, retirement switch, expense inflation |
| 02 | [Taxes](02-TAXES.md) | 2026 brackets, deductions, QBI, NIIT, payroll, IRMAA, state |
| 03 | [Retirement Contributions and Growth](03-RETIREMENT-CONTRIBUTIONS-AND-GROWTH.md) | 2026 limits, catch-ups, account roll-forward |
| 04 | [Social Security](04-SOCIAL-SECURITY.md) | AIME → bend points → PIA → claiming → COLA, and benefit taxation |
| 05 | [RMDs](05-RMD.md) | SECURE 2.0 ages, the official Uniform Lifetime Table |
| 06 | [Insurance Cash Value](06-INSURANCE-CASH-VALUE.md) | §7702, MEC, AG 49-B, policy loans, lapse risk |
| 07 | [Real Estate](07-REAL-ESTATE-EQUITY.md) | **Classification (STR 7-day rule, §280A), equity mechanics, cost segregation + 100% bonus, material participation, REPS, §199A safe harbor, §1031, disposition** |
| 08 | [Ending Estate Value](08-ESTATE-VALUE.md) | Gross estate, step-up, IRD, ILIT, 2026 exclusion |
| 09 | [Worked Example](09-WORKED-EXAMPLE.md) | Age 42 → 100 with real numbers, reconciled to the mockup |
| 10 | [Sources, Test Vectors, Competitors](10-SOURCES-AND-COMPETITORS.md) | Every citation, hand-checkable test cases, market benchmark |
| **11** | [Loss Limitations and Carryforwards](11-LOSS-LIMITATIONS-AND-CARRYFORWARDS.md) | **K-1 clients.** The four gates (basis → at-risk → passive → EBL), NOL/capital-loss/QBI/AMT-credit carryforwards, and the year-to-year state |

---

## The three rules that matter most

**1. Compute in nominal dollars, display in real dollars.**
Tax brackets are inflation-indexed; the Social Security taxation thresholds are frozen in statute. Deflating before the tax step under-taxes every later year.

**2. Follow the order of operations in module 00.**
The RMD must be added to income *before* the tax step. Contributions must reduce income *before* the tax step. Getting the order wrong is the largest single source of wrong answers.

**3. The age 60–63 catch-up replaces the age-50 catch-up.**
It does not stack. Maximum 401(k) at 62 is $35,750, not $43,750 — and it drops back to $32,500 at age 64.

---

## Primary sources of record

| Topic | Source |
|---|---|
| 2026 tax brackets, deductions, estate exclusion | [IRS Rev. Proc. 2025-32](https://www.irs.gov/newsroom/irs-releases-tax-inflation-adjustments-for-tax-year-2026-including-amendments-from-the-one-big-beautiful-bill) |
| 2026 retirement plan limits | [IRS Notice 2025-67](https://www.irs.gov/newsroom/401k-limit-increases-to-24500-for-2026-ira-limit-increases-to-7500) |
| 2026 Social Security parameters | [Federal Register 2025-19763](https://www.federalregister.gov/documents/2025/11/03/2025-19763/cost-of-living-increase-and-other-determinations-for-2026) |
| Uniform Lifetime Table | [IRS Publication 590-B](https://www.irs.gov/pub/irs-pdf/p590b.pdf) |
| 2026 Medicare premiums and IRMAA | [CMS fact sheet](https://www.cms.gov/newsroom/fact-sheets/2026-medicare-parts-b-premiums-deductibles) |

> `ssa.gov` blocks automated access. The Federal Register notice is the **legally authoritative** publication of the same figures and is freely accessible — cite it.

---

## Source material in this folder

- `WhatsApp Image 2026-09-05 at 12.11.10 AM.jpeg` — the roadmap UI mockup
- `2025 Executive Bonus Plan Worksheet(1st_Oct).xlsx - C-Corp 120k.pdf` — executive bonus / C-corp tax stacking worksheet

Module 09 reconciles the mockup's figures against the computed model and documents where they do and do not agree.

---

## Annual maintenance

Figures change every autumn. Refresh order and watch list are in [module 10, Part D](10-SOURCES-AND-COMPETITORS.md#part-d--maintenance).

**Nearest expiry:** the OBBBA senior bonus deduction ends after **2028** — it must be switched off in 2029.

**Watch in 2026:** the §461(l) excess business loss threshold **drops** to $256,000 / $512,000 (from $313,000 / $626,000), and the AMT exemption phaseout rate **doubles to 50%**. Both are OBBBA changes and both worsen outcomes — see [module 11](11-LOSS-LIMITATIONS-AND-CARRYFORWARDS.md).
