# 00 — Overview and the Year Loop

**Roadmap to Age 90™ — calculation research**
Tax year basis: **2026** · Market: **United States** · Last verified: **September 2026**

---

## 1. What this system produces

For every year from the client's current age to age 90 (optionally 100), produce one row:

| Column | Meaning |
|---|---|
| `age` / `year` | Client age and calendar year |
| `income` | Gross income from all sources |
| `contributions` | Money going *into* retirement / insurance / real estate |
| `socialSecurity` | Gross Social Security benefit received |
| `rmd` | Required Minimum Distribution forced out of pre-tax accounts |
| `taxes` | Federal + state + payroll tax paid |
| `expenses` | Lifestyle spending |
| `investmentGrowth` | Earnings on invested balances |
| `retirementBalance` | End-of-year pre-tax + Roth balances |
| `insuranceCashValue` | End-of-year policy cash value |
| `realEstateEquity` | Property value − mortgage balance |
| `netWorth` | Sum of all asset balances |
| `estateValue` | Net to heirs if death occurred this year |

---

## 2. The one rule that governs everything: **nominal in, real out**

> **Compute the entire ledger in nominal (future) dollars. Deflate to today's dollars only at the last step, when displaying.**

This is not a style preference. It is required for correctness:

- Tax brackets and the standard deduction **are** inflation-indexed every year.
- The Social Security benefit-taxation thresholds ($25,000 / $32,000 / $34,000 / $44,000) are **frozen in statute since 1983 and 1993 and are never indexed.**

If you deflate before the tax step, the frozen thresholds get compared against shrunken dollars, and the model **under-taxes Social Security in every later year**. The error compounds.

### The deflator

```
realValue(year n) = nominalValue(year n) / (1 + inflation)^n
```

Where `inflation` is the assumed annual CPI rate (e.g. `0.025`). Apply this **once**, to the finished row, immediately before display.

### Two rails, stated plainly

| Rail | Used for | Never used for |
|---|---|---|
| **Nominal** | All tax math, SS thresholds, RMD divisors, contribution limits, IRMAA tiers | Client-facing display |
| **Real** | Charts, milestone cards, the roadmap UI | Any calculation |

---

## 3. Order of operations — the single biggest source of wrong answers

Each year must be processed in **exactly this order**. Steps that look independent are not.

```
FOR each year n, age a:

  STEP 1   Grow income                     → 01
  STEP 2   Grow expenses                   → 01
  STEP 3   Compute retirement contributions → 03
  STEP 4   Compute Social Security benefit → 04
  STEP 5   Compute RMD (if age ≥ RMD age)  → 05
  STEP 6   Assemble taxable income         → 02
  STEP 7   Compute tax on that income      → 02
  STEP 8   Compute cash flow surplus/deficit
  STEP 9   Apply investment growth         → 03
  STEP 10  Roll forward insurance          → 06
  STEP 11  Roll forward real estate        → 07
  STEP 12  Compute estate value            → 08
  STEP 13  Deflate the row to real dollars → this file, §2
```

### Why the order matters

| Steps | Why they cannot be swapped |
|---|---|
| 5 before 6 | The RMD **is** taxable income. Tax it in the same year it is forced out. |
| 4 before 6 | Social Security taxability depends on all *other* income, so the benefit must be known first — but the benefit itself is not fully taxable. See §4 below. |
| 3 before 6 | Pre-tax contributions **reduce** taxable income. Subtract them before taxing. |
| 6/7 before 8 | Cash flow surplus is what's left *after* tax. Taxing after would double-count. |
| 9 after 8 | Growth applies to the balance *including* this year's net contribution. |
| 13 last | Deflating earlier corrupts every threshold test. |

---

## 4. The circularity trap in Social Security taxation

Step 4 (compute benefit) and Step 6 (assemble taxable income) look circular:

- Taxable Social Security depends on other income.
- But the benefit amount itself does *not* depend on tax.

**Resolution:** they are not actually circular. Compute the **gross benefit** in Step 4 (it depends only on earnings history, claiming age, and COLA). Compute the **taxable portion** in Step 6. There is no loop.

**Do not** attempt to iterate to convergence. There is nothing to converge.

---

## 5. How the ten values connect

```
                    INCOME (01)
                       │
        ┌──────────────┼──────────────┐
        ▼              ▼              ▼
  CONTRIBUTIONS   EXPENSES (01)   TAXABLE INCOME (02)
      (03)             │                │
        │              │                │
        ▼              │                ▼
  RETIREMENT           │            TAXES (02)
  BALANCE (03)         │                │
        │              │                │
        │  at age 73/75│                │
        ▼              │                │
     RMD (05) ─────────┼────────────────┘
        │              │            (RMD is taxable)
        │              ▼
        │        CASH FLOW SURPLUS
        │              │
        │      ┌───────┼────────┐
        │      ▼       ▼        ▼
        │  INSURANCE  REAL   INVESTMENT
        │  CASH VAL  ESTATE   GROWTH
        │    (06)     (07)      (03)
        │      │       │        │
        └──────┴───────┴────────┘
                       │
                       ▼
             SOCIAL SECURITY (04)
             adds income from age 62–70
                       │
                       ▼
              NET WORTH → ESTATE VALUE (08)
```

---

## 6. Phases of life

The engine behaves differently in three phases. Every module states which phase it applies to.

| Phase | Ages | What happens |
|---|---|---|
| **Accumulation** | current age → retirement age | Earned income, contributions in, no withdrawals |
| **Early retirement** | retirement age → RMD age | No earned income, withdrawals begin, Social Security may start (62–70), **no RMD yet** |
| **RMD phase** | RMD age (73 or 75) → death | Forced distributions, full Social Security, RMD drives taxable income |

**The gap between retirement and RMD age is the most important planning window** — this is where Roth conversions and low-bracket harvesting happen. The engine must model it as a distinct phase, not lump it into "retirement".

---

## 7. Global inputs

These are set once and used by every module.

| Input | Type | Typical | Notes |
|---|---|---|---|
| `currentAge` | int | 42 | From date of birth |
| `birthYear` | int | 1984 | **Required** — determines RMD age (73 vs 75) |
| `retirementAge` | int | 62–67 | Client's stated target |
| `endAge` | int | 90 | Or 100 |
| `filingStatus` | enum | MFJ | single / MFJ / MFS / HoH |
| `state` | string | CA | Drives the state tax layer |
| `inflation` | rate | 0.025 | CPI assumption; used only for the final deflator and expense growth |
| `incomeGrowth` | rate | 0.03 | Wage growth assumption |
| `investmentReturn` | rate | 0.06–0.07 | Nominal, pre-fee |
| `realEstateReturn` | rate | 0.04 | Nominal appreciation |
| `ssClaimAge` | int | 67 | 62–70 |

### On return assumptions

Use **nominal** returns and let the deflator handle inflation. Do **not** subtract inflation from the return and then also deflate — that double-counts and understates the result badly.

- ❌ Wrong: `realReturn = 0.07 − 0.025` then also deflate the output
- ✅ Right: grow at `0.07` nominal, deflate the finished row by `(1.025)^n`

---

## 8. Rounding

| Quantity | Rule | Authority |
|---|---|---|
| PIA | Round **down** to next lower $0.10 | SSA |
| AIME | Round **down** to next lower $1 | SSA |
| SS bend points | Round to **nearest** $1 | Federal Register 2025-19763 |
| Tax | Round to nearest $1 | IRS |
| RMD | No statutory rounding; round to nearest $1 for display | IRS Pub 590-B |
| Display values | Nearest $1, or nearest $1,000 on milestone cards | Presentation choice |

Round **only at the stated point**. Rounding intermediate values inside a 48-year loop accumulates visible drift.

---

## 9. Reading order

| Read this | To understand |
|---|---|
| `01-INCOME-AND-EXPENSES.md` | Steps 1–2 |
| `02-TAXES.md` | Steps 6–7 |
| `03-RETIREMENT-CONTRIBUTIONS-AND-GROWTH.md` | Steps 3, 9 |
| `04-SOCIAL-SECURITY.md` | Step 4 |
| `05-RMD.md` | Step 5 |
| `06-INSURANCE-CASH-VALUE.md` | Step 10 |
| `07-REAL-ESTATE-EQUITY.md` | Step 11 |
| `08-ESTATE-VALUE.md` | Step 12 |
| `09-WORKED-EXAMPLE.md` | All of it, with real numbers |
| `10-SOURCES-AND-COMPETITORS.md` | Where every figure came from |

---

## 10. Sources

| What | Source | Google this |
|---|---|---|
| 2026 inflation adjustments | [IRS Rev. Proc. 2025-32](https://www.irs.gov/newsroom/irs-releases-tax-inflation-adjustments-for-tax-year-2026-including-amendments-from-the-one-big-beautiful-bill) | `IRS 2026 inflation adjustments Rev. Proc. 2025-32` |
| 2026 SSA parameters | [Federal Register 2025-19763](https://www.federalregister.gov/documents/2025/11/03/2025-19763/cost-of-living-increase-and-other-determinations-for-2026) | `Cost-of-Living Increase and Other Determinations for 2026 Federal Register` |
| SS benefit taxation is not indexed | [CRS RL32552](https://www.congress.gov/crs-product/RL32552) | `CRS Social Security Taxation of Benefits RL32552` |
